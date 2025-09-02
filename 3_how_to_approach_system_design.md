00:00
So in this part, let's talk about how to do system design let's say you're suddenly thrown at a question Assuming someone throws a question at you how you're going to respond because it seems to be related to well-being because there are so many components and so many things to decide like how to solve any problem -- these are the principles I've followed throughout my career
所以在这个部分，我们来谈谈如何进行系统设计 假设你突然被抛到 假设有人向你抛出一个问题 你会如何应对 因为这似乎与福祉相关 因为组件数量众多 需要决定的事情太多 比如如何解决任何问题的方法 这些都是我职业生涯中一直遵循的原则

00:21
Whenever I'm designing any system, I first need to make it clear that system design is very practical, no matter what system you're designing, think in a very realistic way, imagine that you're the one who actually built it, who will be responsible for writing the code, how to design it, not just frame for the frame's sake, it's not the right way to think in a very pragmatic way
每当我在设计任何系统时 首先需要明确系统设计极具实践性 无论你设计什么系统 都要以非常现实的方式思考 想象你就是实际构建它的人 谁将负责编写代码 如何设计而非只为画框而画框 这不是正确的方法 要以非常务实的方式思考

00:51
And then solve the problem one by one, and my point is that I say take it gradually, no matter what the situation is, whatever the resources you have, take really small steps, like starting small, and you end up building a great system, and I usually follow four or five steps, and that's what I recommend for system design, first of all, to clarify the problem description
然后逐个解决问题 我的观点是 我说要循序渐进 无论什么情况 无论手中有什么资源 都要迈出真正的小步 就像一步步从小处着手 最终你会构建出优秀的系统 我通常遵循四到五个步骤 这就是我推荐的系统设计方法 首先明确问题描述

01:21
The most important step is to fully understand the problem, if you lack a problem understanding, it's easy to get lost, don't focus on the problem that really needs to be solved, but start expanding the system in other random directions, this is not the way to deal with the problem, be clear about what you need to do, understand the constraints of the problem, for example, if someone asks
最重要的一步是充分理解问题 如果缺乏问题理解 很容易迷失方向 没有聚焦真正需要解决的问题 却开始向其他随机方向扩展系统 这不是处理问题应有的方式 明确自己需要完成的任务 理解问题的约束条件 例如 如果有人问

01:54
Let's design a short URL Let's design a URL shortener to handle a million requests per month Oh my gosh, a million requests per month Just a million requests per month But if you design a system that can handle a billion requests it's easy to deviate from the goal Over-engineered when it comes to designing when it comes to specific constraints
让我们设计一个短网址 让我们设计一个网址缩短器 需要处理每月一百万次请求 天啊 每月一百万次请求 只需处理每月一百万次请求 但如果设计能处理十亿次请求的系统 很容易偏离目标 设计时会过度工程化 当收到特定约束时

02:22
You have to work within a given range, and you're going to design a highly optimized system, and most of the time, if the system is highly optimized, it's more than 100 million, it's 200 million, it's more than a billion, and you can handle this skill with a little bit of tweaking here, but it's very critical, it's very necessary to limit yourself to constraints
必须在既定范围内运作 你将设计一个高度优化的系统 而大多数情况下 如果该系统高度优化 超越一亿 达到两亿 突破十亿 只需在此处做些小调整 你就能处理这项技能 但这非常关键 非常有必要将自己限制在约束条件内

02:45
You need to ask yourself those key questions Hey whatever you design how we design what constraints are there what core features have to be preserved and built around them Don't deviate from those elements That's what really matters So building a deep understanding of the problem is the first step in system design The second step is to break down the problem into components
你需要向自己提出那些关键问题 嘿 无论你设计什么 我们如何设计 有哪些约束条件 哪些核心功能必须保留并围绕其构建 不要偏离这些要素 这才是真正重要的 因此建立对问题的深刻理解 这是系统设计的第一步 第二步是将问题分解为组件

03:13
It's critical to say for example if someone says to you now let's design Facebook, and when someone asks you to design a system as big as Facebook, the first thing that should come to mind is what are the features I'm designing, in this case, Facebook and nothing else
这至关重要 例如 假设有人对你说 现在让我们设计facebook 当有人抛出这样的问题 让你设计像facebook这样庞大的系统 首先应该想到的是 我正在设计的功能有哪些 在这种情况下是facebook而非其他

03:37
Instead of being overwhelmed by it, it has to be broken down, because no one can solve the whole Facebook at once, and it has to be split into almost mutually exclusive subcomponents, such as components, or functions, for example, let me give you an example to make this clearer, so let's say if you are given the task of designing Facebook
而不是被其压垮 必须进行分解 因为没有人能一次性解决整个facebook 必须将其拆分为多个 几乎互斥的子组件 例如 可以是组件 也可以是功能 例如 我举个例子让这更清楚 所以假设 如果你接到设计facebook的任务

04:04
You say, there's a component that's responsible for authentication, a component handling notifications, a component that's responsible for that, and I've picked three basic features that are large enough to be independent microservices, and then work on them one by one, and if the problem is complex enough, like Facebook, splitting it into functional modules, okay, that's it
你会说 有一个组件负责认证 一个组件处理通知 一个组件负责这部分 我选取了三个基础功能 规模足够成为独立的微服务 然后逐一攻克 如果问题足够复杂 比如像Facebook将其拆分为功能模块 好的 这就是该功能

04:30
Single authentication I need notifications I need to build dynamic content around it yes once you have this and then pick and pick and dive into this module ah, let's choose authentication and dive in, or let's say we choose dynamic content and dig deeper, that's the first step, if the problem is complex enough
单一身份验证 我需要通知功能 我需要围绕它构建动态内容 没错 一旦拥有这个 然后逐一挑选并深入研究这个模块啊 让我们选择身份验证并深入探讨 或者假设我们选择动态内容并深入分析 这就是第一步 如果问题足够复杂

04:50
When you choose a component as the third step, you need to disassemble the component and then dig deeper into the module, let's say I want to choose dynamic content for implementation, in order to implement what I need, in order to implement dynamic content, you definitely need a web server to provide the content when the user goes online
需分解为更小的组件 然后逐一攻克 当选择组件作为第三步时 需拆解该组件 然后深入研究这个模块啊 假设我要选择动态内容进行实现 为了实现 我需要什么 为了实现动态内容 肯定需要一个提供内容的网络服务器 当用户上线时

05:18
The user makes a request The web server interacts with the database to get the content and send it to the user This is the most basic operation so we need a web server We haven't started designing it yet, we just broke it down into smaller components smaller quotes end quotes subcomponents If we need it, so we need a web server
用户发起请求 网络服务器与数据库交互 获取内容并发送给用户 这是最基本的操作 因此需要网络服务器 我们还未开始设计 只是拆解为更小组件 更小的引号 结束引号 子组件 如果我们需要的话 所以我们需要网络服务器

05:40
We also need a database, but if you think about it, we're only solving the read part, so who writes the data to the database, so we need a generator to generate the content, which is not yet determined, but you've drawn the boundary, the web server is responsible for serving the content from the database, there must be a component that writes to the database, and then we're going to do it
还需要数据库 但若仔细想想 我们只解决了读取部分 那谁来向数据库写入数据 因此需要生成器 负责生成内容 这部分还未确定 但你已经划定了边界 网络服务器负责从数据库提供内容 必须要有向数据库写入的组件 接下来我们

06:10
Define the generator to write data to the database, so that the boundaries are clear, yes, once you become a one-time and you're basically familiar enough when you design enough systems, you realize hey, it's not just about generating like my feed might want to aggregate my feed, let's say there's a lot of content that can be aggregated into a post
定义生成器向数据库写入数据 这样就明确了边界 没错 一旦你成为一次 你基本足够熟悉 当你设计足够多的系统 你会意识到嘿 这不仅仅是关于生成 比如我的动态可能想聚合我的动态 假设有很多内容可以聚合成一条帖子

06:34
Or I can filter the content to optimize, so maybe an optional aggregator for aggregation dynamics, other content filters for you, etc., you just add aggregators around it, but if you're not sure, and I'm going to add on purpose, if you're not sure what the responsibility for this is, just skip it, don't frame for the sake of the frame, even when I'm explaining
或者我可以过滤内容以优化 所以或许一个可选的聚合器用于聚合动态 其他内容为你过滤 等等你只需围绕它添加聚合器 但如果你不确定 并且我特意添加 如果你不确定这个的责任是什么 直接跳过 不要为了画框而画框 即使我在解释时

07:01
I wrote this specifically to convey this message It doesn't seem like I'm really sure about the responsibility for this aggregator so it's better to skip that we know we need a web server to provide the dynamics We know we need a generator to generate the dynamics We're not sure just gave it a fancy noun called aggregator and then we added it
我特意写下这个来传达这个信息 似乎对这个聚合器的责任不太确定 所以最好跳过 我们知道需要网络服务器来提供动态 我们知道需要生成器来生成动态 我们不确定只是给它起了个叫聚合器的 fancy 名词 然后我们添加了它

07:26
But we're not sure what it does, remove this part when in doubt, because once you build or go into each subcomponent, you realize hey, that's what we definitely need, and then you add it, and that's the core of structured thinking, skip when in doubt, and once you dig deeper, you realize hey, something like this has to exist
但我们不确定它会做什么 有疑问时移除这部分 因为一旦你构建 或者深入每个子组件 你会意识到嘿 这就是我们肯定需要的 然后你添加它 这就是结构化思维的核心 有疑问时跳过 一旦深入分析 你会意识到嘿 这样的东西必须存在

07:51
And then you add it Frame for the sake of the frame It's not good Once you know the boundaries to divide Define the set of responsibilities for each component That's when you know hey I need this everything else can be backed down in this graph I don't recommend adding anything around the aggregator at all because I'm not sure what the responsibility is Draw for the sake of drawing
然后你添加它 为了画框而画框不好 一旦你知道要划分的边界 明确每个组件的责任集合 那时你才知道嘿 我需要这个 其他都可以退后 在这张图中 我完全不建议围绕聚合器添加内容 因为我不确定责任是什么 为了画图而画图

08:20
Bad idea, right, okay, now let's look at each subcomponent, because we're engineers, we need to dig deeper, yes, what will this web server look like, what will it do, is it based on Python or Java, is it based on Java or Node, is it based on JavaScript or whatever
不好主意 对吧 好的 现在我们来看每个子组件 因为我们是工程师 需要深入探讨一下 没错 那么这个网络服务器会是什么样的 它会有哪些功能 是基于Python还是Java 基于Java还是Node 基于JavaScript或者其他什么

08:38
What kind of database do we use, how the generator generates the data source, these details need to be considered, and the next step should be Once you understand this, you have enough depth to now it's time to make a technical decision, and that's the process of making four technical decisions for each component, and these are the four key points to decide
我们使用哪种数据库 生成器如何生成数据源 这些细节都需要考虑 接下来的步骤应该是 一旦你了解了这些 你已经掌握了足够的深度 现在是时候做出技术决策了 这就是为每个组件制定四项技术决策的过程 这是需要决定的四个关键点

09:01
I'll go into more detail about each part in a subsequent video, but I still want to convey these ideas to you, the first technical components to consider are the database and the cache, everything related to storage How data is stored Is it needed Caching If caching is needed to speed up where the cache should be placed, how the components interact with it
将在后续视频中详细讲解每个部分 但我仍想把这些思路传达给你 首先需要考虑的技术组件 是数据库和缓存，所有与存储相关的内容 数据是如何存储的 是否需要缓存 如果需要缓存来提升速度 缓存应该放在哪里 组件如何与之交互

09:26
In the sub-component, the primary technical decision is the database and cache so the storage issue The second is scalability and fault tolerance How the network server scales If there is only one server When there are millions of users A single server cannot handle Multiple servers are required Deploy through a load balancer These decisions require immediate consideration of fault tolerance
在子组件中首要的技术决策是数据库和缓存 所以存储问题 第二个是扩展性和容错性 网络服务器如何扩展 如果只有一个服务器 当有百万用户时 单个服务器无法处理 需要多个服务器 通过负载均衡器部署 这些决策需要立即考虑容错性

09:50
What to do if the database crashes How my system recovers from failure is very important In the details of scalability and fault tolerance, each new technical component needs to be considered, to think about how each component scales from these perspectives, how to be fault-tolerant of each component, and the third point is the most critical, that is, asynchronous processing
如果数据库崩溃怎么办 我的 系统如何从故障中恢复 非常重要 在扩展性和容错性细节中 每个新增的技术组件都需要考虑 要思考 要从这些角度出发 每个组件如何扩展 每个组件如何容错 第三点最为关键 即异步处理

10:16
We'll explain message queues and message blocking in detail, but to give you a preliminary understanding, asynchronous processing is something you don't do right away, but push a message for the consumer to handle on their own, like you tell someone you're going to...
将详细讲解消息队列和消息阻塞 但为了让你有个初步了解 异步处理是你不会立即执行的操作 而是推送一条消息让消费者自行处理 就像你告诉某人你要...

10:34
For example, you need to perform certain tasks, and you don't do it yourself, but you ask your friend to do it for you, you delegate the task to your friend, you don't have to worry, you know your friend will do it for you, and then you just give it to the other person to do the task that needs to be done immediately, and that's the concept of synchronization, and we're going to dive into synchronization
例如你需要执行某些任务 你并没有亲自做这件事 而是让你的朋友代劳 你将任务委托给了朋友 你无需担忧 你知道朋友会为你完成 然后只需交给对方 需要立即完成的任务 这就是同步处理的概念 我们将深入探讨同步处理

10:56
But the core idea is this: for any situation, for example, if my web server or other component needs to generate a data source, do I need to do it immediately when I run the app, when a user makes a request, should I generate the data immediately, then should it be pre-configured, imagine when you log in to Instagram
但核心思想是这样 对于任何情况 例如 如果我的网页服务器或其他组件需要生成数据源 是否需要在运行应用时立即执行 当用户发起请求时 是否应立即生成数据 那么 还是应该预先生成呢 想象你登录Instagram时

11:17
If it takes five minutes to load the dynamics because the data is being generated in real time, at that point in time, which is obviously not appropriate, so it should be synchronized, and the data source is continuously generated and maintained in the background, ready for you to browse, right, that's synchronization, and the fourth point is about the communication mechanism, how different components communicate with each other, when I mentioned communication
如果加载动态需要五分钟 因为数据正在实时生成 在那个时间点 这显然不妥 因此应采用同步方式 后台持续生成并维护数据源 随时准备供你浏览 对吧 这就是同步处理 第四点涉及通信机制 不同组件如何互相通信 当我提到通信时

11:44
Here are the technical details TCP, UDP, GDP, WebSocket, gRPC, or other protocols How to communicate How a web server interacts with a database How a build service communicates with a web service (such as a server) How a generator reads other data sources such as a communication part Web server
这是技术细节 TCP UDP GDP WebSocket gRPC或其他协议 如何进行通信 网页服务器与数据库如何交互 生成服务与网页服务（如服务器）如何通信 生成器如何读取其他数据源 例如通信部分 网页服务器

12:04
Or sorry, um, WebSocket, gRPC, HTTP, REST, endpoints, these parts, right, these are things, these are the four key points that you need to focus on, all the subcomponents that you design, because that's the hallmark of a well-designed system, right, now that you've broken down each part in detail
或者说 抱歉 嗯 WebSocket gRPC HTTP REST端点 这些部分对吧 这些都是东西 这些都是你需要关注的四个关键点 你设计的所有子组件 因为这就是设计良好系统的标志 对了现在既然你已经详细分析了每个部分

12:28
But now you might find that the need for a web server is good enough, and I know it's like I can pretty much start writing code to build a web server like Flask or Django Spring Boot, but when it comes to generators, I'm not so sure like I know I can
但现在你可能会发现需求 Web服务器已经足够好了 我知道这像 我几乎可以直接开始编写代码来搭建Web服务器 比如Flask或Django Spring Boot之类的框架 但谈到生成器 我不太确定像 我还是更清楚自己可以

12:48
I still need to split this generator into smaller parts, because this generator doesn't stand alone, it needs to read data from somewhere else, right, so the next thing you want to think about is I need to split the generator into smaller components, each with a specific responsibility, and when we design other systems, you will have a clearer understanding
我仍需要将这个生成器拆分为更小的部分 因为这个生成器不是独立存在的 它需要从其他地方读取数据 对的所以接下来你要考虑的是 我需要将生成器拆分为更小的组件 每个组件负责特定职责 当我们设计其他系统时 你会有更清晰的理解

13:17
But first understand what we're talking about, if you find that you need to split the component, and that component is versatile enough as a generator, how to be practical, that's what I mean, as an engineer, you need to think about how to code the generator in the implementation process, how to actually implement it, and then you go into the details, and you will find that you may need to read and merge data from other services
但先理解我们讨论的内容 如果发现需要拆分组件 而该组件作为生成器足够通用 那该如何实际 这就是我说的作为工程师需要思考的 在实现过程中 如何编写生成器的代码 如何实际实现它 深入细节后 你会发现 可能需要从其他服务读取并合并数据

13:53
And do the merge and probably also need a database to store temporary information This is your generator So the generator itself is made up of two or three components or finer subcomponents and needs to be integrated with e.g. post services recommendation services and follow services only people who know these because to generate dynamic content for my generator
并进行合并 可能还需要一个数据库存储临时信息 这就是你的生成器 所以生成器本身由两到三个组件组成 或更细的子组件 并且需要与 例如 帖子服务 推荐服务和关注服务 只有了解这些的人 因为要为我的生成器生成动态内容

14:20
It needs to know who you follow This means leveraging information from the recommendation engine in order to recommend content for which you are more likely to be liked, shared and subscribed to, etc. And then populated with details through the post service That's right, that's information like likes from your fans uh people you follow, system-generated recommendations, and post services
它需要知道你关注的用户 这意味着利用推荐引擎的信息 以便为其推荐内容 这些内容更可能被你喜欢、分享和订阅等 然后通过帖子服务填充详细信息 没错，这就是来自粉丝的点赞等信息 呃 你关注的人、系统生成的推荐以及帖子服务

14:45
You need to merge them and put them in a database that is used by the web server, and when you start thinking about implementation, you'll see that these are different parts that I need to interface with these interfaces, and that's what I'm talking about, to deal with it in a very structured way, and it's better to analyze it from the top down when you have big problems, like Facebook's design
需要将它们合并并存入数据库 由Web服务器使用该数据库 当你开始考虑实现时 你会发现 这些都是不同的部分 我需要对接这些接口 这就是我说的 要以非常结构化的方式处理 面对大问题时，从上往下分析更好 比如Facebook的设计

15:08
Facebook design Uber design Tinder and start with functions Break down each function to solve one by one If you encounter specific problems, you should start from the bottom up First design the database and other foundations There are usually two ways to deal with big problems Analyze from top to bottom Deal with small details or very focused problems
Facebook的设计 Uber的设计 Tinder和从功能开始 拆解每个功能逐一解决 如果遇到具体问题 应从下往上入手 先设计数据库等基础 通常有两种方法 处理大问题 从上往下分析 处理小细节 或者非常聚焦的问题

15:28
Building from the bottom up is the general way most senior engineers approach systems, yes, so that's all I want to talk about, it's all about how to do system design, again, need to reiterate, very practical, every system design problem you have, it's extremely practical
从下往上构建 这是大多数资深工程师处理系统的一般方法 没错 所以就是这样 这就是我想讲的全部 这全部关于如何进行系统设计 再次强调 需要重申 非常实用 每个系统设计问题 每个你遇到的系统设计问题都极其实际

15:49
It has to be structured and it is not a chaotic process You can't rote it needs to develop intuition I want to show how to develop that intuition as we design more systems to understand how to solve problems step by step yes that's what this part is about I hope you find it interesting I hope you find it wonderful
必须以结构化方式处理 这不是混乱的过程 不能死记硬背 需要培养直觉 我希望展示了如何培养这种直觉 当我们设计更多系统时 能更清晰理解如何逐步解决问题 是的 这就是这一部分的内容 希望你觉得有趣 我希望你们觉得精彩

16:15
That's all for this issue We'll see you next time Thank you again
这就是本期的全部内容 我们下期再见 再次感谢
