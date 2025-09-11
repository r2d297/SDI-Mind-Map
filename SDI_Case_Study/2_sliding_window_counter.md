当然。下面是 **Sliding Window Counter** 算法的伪代码，并且我将附上详细的注释和执行示例，以确保你完全理解它的工作原理。

这个算法的核心是**用极低的内存成本来估算过去一个时间窗口内的请求数**。

### 核心思想

我们将时间划分为固定的“桶”（例如，每分钟一个桶）。为了估算过去60秒的请求数，我们使用**当前桶**的完整计数，并加上**前一个桶**的一部分计数，这部分的权重取决于当前时间在当前桶中的位置。

### 需要存储的状态

对于每个需要限流的实体（比如每个用户ID），我们需要在 Redis 中存储以下信息（通常使用一个 Hash 来存储，以保证原子性操作）：

*   `window_start_timestamp`: 当前时间桶的开始时间戳。
*   `current_count`: 当前时间桶内的请求计数。
*   `previous_count`: 上一个时间桶内的请求计数。

---

### 伪代码

```
FUNCTION isRequestAllowed(userId, limit, windowSizeInSeconds):
    // 1. 获取当前时间和计算当前窗口的开始时间戳
    now = getCurrentTimestamp()
    current_window_start = now - (now % windowSizeInSeconds) // 向下取整到窗口的开始

    // 2. 从 Redis 获取该用户的状态
    // 使用 HGETALL 获取一个哈希，保证原子性读取
    state = redis.HGETALL("rate_limit:" + userId)
    stored_window_start = state.window_start_timestamp ?: 0
    previous_count = state.previous_count ?: 0
    current_count = state.current_count ?: 0

    // 3. 检查窗口是否已经移动，并更新计数器
    // 这个是算法的核心逻辑
    IF now > stored_window_start + (2 * windowSizeInSeconds):
        // 情况A: 距离上次请求已经过去了至少一个完整的窗口
        // 因此，前一个窗口和当前窗口的计数都应归零
        previous_count = 0
        current_count = 0
    ELSE IF now > stored_window_start + windowSizeInSeconds:
        // 情况B: 刚好进入下一个新窗口
        // 将上一个窗口的'current_count'变成'previous_count'
        // 并将'current_count'重置为0
        previous_count = current_count
        current_count = 0
    
    // 如果窗口没有移动（在情况B和情况A之外），则计数器保持不变

    // 4. 计算估算的请求数
    // 计算当前时间在当前窗口中的位置百分比
    percentage_in_current_window = (now - current_window_start) / windowSizeInSeconds
    
    // 估算值 = (前一个窗口的计数 * 在滑动窗口中剩余的权重) + 当前窗口的计数
    estimated_count = (previous_count * (1 - percentage_in_current_window)) + current_count

    // 5. 做出决策
    IF estimated_count < limit:
        // 允许请求
        // 增加当前窗口的计数
        current_count = current_count + 1

        // 6. 将更新后的状态写回 Redis
        // 使用 HSET 或 Lua 脚本保证原子性写入
        redis.HMSET("rate_limit:" + userId, {
            "window_start_timestamp": current_window_start,
            "current_count": current_count,
            "previous_count": previous_count
        })
        
        RETURN TRUE
    ELSE:
        // 拒绝请求
        RETURN FALSE
```

---

### 执行示例

让我们用一个具体的例子来走一遍流程：

*   **限流规则**: 每分钟（60秒）最多100次请求。
*   **当前时间**: `10:30:45`

**1. 初始状态 (10:29:00 - 10:29:59)**
*   在 `10:29` 这一分钟内，用户总共请求了 **80** 次。
*   Redis中存储的状态 (`rate_limit:user123`):
    *   `window_start_timestamp`: `10:29:00` 的时间戳
    *   `current_count`: `80`
    *   `previous_count`: `...` (之前的值，现在不重要)

**2. 新请求到达 (时间: 10:30:15)**
*   `now` = `10:30:15`
*   `current_window_start` = `10:30:00`
*   从 Redis 读取到 `stored_window_start` = `10:29:00`。
*   **检查窗口移动**:
    *   `now` (`10:30:15`) > `stored_window_start` + `windowSize` (`10:29:00` + 60s = `10:30:00`)
    *   触发了 **情况B**。
    *   更新计数器：
        *   `previous_count` = `current_count` (变成 `80`)
        *   `current_count` = `0`
*   **计算估算值**:
    *   `percentage_in_current_window` = (`10:30:15` - `10:30:00`) / 60s = 15 / 60 = **0.25**
    *   `estimated_count` = (`previous_count` * (1 - 0.25)) + `current_count`
    *   `estimated_count` = (80 * 0.75) + 0 = **60**
*   **决策**:
    *   `60 < 100`。请求被**允许**。
*   **更新状态**:
    *   `current_count` 增加 1，变为 `1`。
    *   将新状态写回 Redis:
        *   `window_start_timestamp`: `10:30:00`
        *   `current_count`: `1`
        *   `previous_count`: `80`

**3. 另一个请求到达 (时间: 10:30:45)**
*   `now` = `10:30:45`
*   `current_window_start` = `10:30:00`
*   从 Redis 读取到 `stored_window_start` = `10:30:00`。
*   **检查窗口移动**:
    *   `now` (`10:30:45`) 和 `stored_window_start` (`10:30:00`) 在同一个窗口内，不触发情况A或B。
    *   计数器保持不变：`previous_count` = `80`, `current_count` = `1` (来自上一步)。
*   **计算估算值**:
    *   `percentage_in_current_window` = (`10:30:45` - `10:30:00`) / 60s = 45 / 60 = **0.75**
    *   `estimated_count` = (`previous_count` * (1 - 0.75)) + `current_count`
    *   `estimated_count` = (80 * 0.25) + 1 = 20 + 1 = **21**
*   **决策**:
    *   `21 < 100`。请求被**允许**。
*   **更新状态**:
    *   `current_count` 增加 1，变为 `2`。
    *   将新状态写回 Redis:
        *   `window_start_timestamp`: `10:30:00`
        *   `current_count`: `2`
        *   `previous_count`: `80`

### 关于原子性的重要说明

伪代码中的“读-改-写”流程（第2, 5, 6步）在分布式环境中**必须是原子操作**。否则，在高并发下，两个请求可能会同时读取到旧的计数值，都判断请求合法，然后都去增加计数，从而导致最终计数超过限制。

在实践中，这通常通过 **Redis Lua 脚本** 来实现，将整个逻辑封装在一个脚本中，由 Redis 保证其原子执行。