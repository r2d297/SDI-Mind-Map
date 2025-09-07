00:26
Okay good morning everyone this is the microphone catching my voice yes okay so thumbs up If you guys can hear me, thank you, okay so today we're going to talk about CPU scheduling and you'll see that it's a very different topic than what we talked about earlier Just Tuesday It's a common theme in this course
好的 早上好 所有人 这是麦克风捕捉到我的声音 是的 好的 所以点赞 如果你们能听到我，谢谢，好的 所以今天我们要谈论CPU调度 你会发现这是一个与我们之前谈论的主题大相径庭的主题 就在周二 这是这门课程的常见主题

00:45
Different resources or strategies with mechanics it feels completely different so if you don't like part of the course very likely you're going to like the part that follows which can be encouraging And one thing is, yes what okay I'm going to turn up the volume on the mic is it's better okay great, well, if I'm going to be quick
不同的资源或策略与机制 它感觉完全不同 所以如果你不喜欢课程的一部分 非常有可能你会喜欢紧随其后的部分 这可以是鼓励人的 还有一件事是，是的 什么 好的 我会提高麦克风的音量 这更好吗 好的 太好了，嗯，如果我要快速地

01:15
Please raise your hand and say, can you repeat those things or hopefully you'll all start asking more questions as we move forward We're going to start with a bunch of announcements That's great news for all of you, I have a lot of announcements yes okay you guys know Project One is due Monday night and we have piazza
请举起手并说 你能重复那些东西吗 或者希望你们都会在我们前进的过程中开始问更多的问题 我们将从一堆公告开始 这对你们所有人来说是个好消息，我有很多公告 是的 好的 你们知道 项目一 到期 星期一晚上 我们有piazza

01:33
I think everybody is doing a great job answering your questions There are so many answers I answered too fast I am answering so amazing We don't want you all to rely too much on us to answer your questions at the last minute you need to start looking at these things ahead of time To encourage that, we are going to not answer any of your questions on Monday afternoon in piazza
我想每个人都在做得很好地回答你们的问题 答案太多了 我回答得太快了 太神奇了 我们不希望你们都太依赖我们回答你们的问题 在最后一刻 你需要开始提前看这些东西 为了鼓励这一点，我们将在星期一下午不回答任何你们的问题在piazza

01:55
Of course, Piazza is still there, you can look at old questions, maybe you can answer other students' questions, but tas and peer assessments won't answer any questions Monday afternoon and then we do have a lot of lab time, and if you look at that lab schedule, you'll see that we have lab time almost every day
当然，piazza还在那里 你可以看旧问题 也许你可以回答其他学生的问题 但tas和同伴评估将不会回答任何问题 星期一下午 然后我们确实有大量的实验室时间 如果你看那个实验室日程表 你会发现我们几乎每天都有实验室时间

02:11
From ten a.m. to ten p.m. so we're going to stop at ten p.m. Your projects are due at midnight and you're going to have a period without a mentor so please start those projects early anyway Well, in yesterday's discussion part, the TA told me that it seems like a lot of people haven't started the project yet, so you have some of you who are already fully done
从早上十点到晚上十点 所以我们在晚上十点会停止 你的项目在午夜到期 你将有一段没有导师的时间 所以请无论如何尽早开始这些项目 嗯 在昨天的讨论部分 助教告诉我，似乎很多人还没有开始项目 所以你有一些人已经完全完成

02:31
They are worried about all the parity test cases and others don't seem to be looking at the spec yet, so we strongly recommend that you look at the spec before the discussion section to ask better questions in the discussion section, knowing that Project 2 is now available Yes Yes In the past, we called this project Project 1a and Project 1b
他们在担心所有的奇偶测试用例 而其他人似乎还没有看规范 所以我们强烈建议你在讨论部分之前看规范 以便在讨论部分中问出更好的问题 因为知道项目二现在可用 是的 是的 在过去，我们将这个项目称为项目一a和项目一b

02:54
This time they're all going to be available We're trying to be clearer about project one Project two we want to give you enough time to work on the project yes it's available now and will expire on the Monday after project one expires so you have you know you have a week and a half to work on that yes to finish project one and start looking at project two right away
这次它们将全部可用 我们试图对项目一更清楚 项目二 我们想给你足够的时间工作在项目上 是的 它现在是可用的，并将到期 在项目一到期后的周一 所以你有 你知道有一个半周的时间来工作在那个上面 是的 完成项目一并立即开始看项目二

03:16
Project 2 is going to be much more difficult than Project 1 It uses an XP six kernel environment A mock kernel that you need to understand very well You don't have to understand the whole codebase but there will be a lot of code you need to figure out which parts are relevant and modify it a little bit to make it work So please look at the description of that specification so that you can start it before the discussion part next Wednesday
项目二将比项目一难得多 它使用xp六内核环境 一个你需要理解得很好的模拟内核 你不必理解整个代码库 但将有很多代码 你需要找出哪些部分相关 并稍微修改它使其工作 所以请看那个规范的说明 以便在下周三的讨论部分之前开始它

03:37
So that in the discussion section you can ask the teaching assistant some good questions about how to do project two okay more good news I decided that you can do some homework in this course The idea of the assignment is I want to make sure you understand the lecture before the exam so this is actually a test Can I set up a quiz on the canvas
以便在讨论部分中你可以向助教问一些关于如何做项目二的好问题 好的 更多的好消息 我决定你可以在这个课程中做一些作业 作业的想法是 我想要确保你在考试前理解讲座内容 所以这实际上是一个测试 我可以在画布上设置一个测验吗

03:59
It's really easy The purpose of this is actually to give you some opportunities to practice with the sample exam questions I set up the quiz so that you can take it at any time and we will also show you the correct answer when you finish the quiz so just try again if you have any mistakes and only four questions
这真的很容易 这个的目的实际上是让你有一些与样本考试问题进行实践的机会 我设置了测验，以便你可以任何时间取它 我们还将显示正确的答案 当你完成测验时 所以只需再试一次 如果你有任何错误 而且只有四个问题

04:15
So it's really simple, see if we can start here with that okay so let's just do that week and then the last thing is that I made a mistake when I was scheduling the midterm exam I signed it was supposed to be on Wednesday, October 9th unfortunately it was a holiday so we changed that to Thursday, October 10th
所以这真的很简单，看看我们是否能在这里用那个开始 好的 所以那一周就那样吧 然后最后的事情是我犯了一个错误 当我安排中期考试时 我签署了 它应该在十月九日的星期三 不幸的是 那是一个假期 所以我们将那个更改为十月十日的星期四

04:37
So let me know if there is a problem on Thursday, October 10 then we will schedule an alternative exam for you as we would have done but we will talk about the exam later Okay that's all the announcements Any questions about the announcement Okay Let's get into some topics So today we are talking about how the operating system determines the process to be scheduled on the CPU
所以请告诉我如果十月十日的星期四有问题 然后我们将为您安排替代考试 就像我们原本会做的一样 但我们稍后会讨论考试 好的 这就是所有公告 关于公告有任何问题吗 好的 让我们进入一些主题 所以今天我们正在谈论操作系统如何确定要安排在CPU上的过程

05:02
In our last lecture, we looked at how to actually do context switching, and today we're looking at strategies, so we're going to learn how the operating system decides which process to run, and we're going to talk about different metrics that the operating system might want to optimize, like throughput or turnaround time or response time, and you're going to learn that there are a lot of different task scheduling strategies
在我们的上次讲座中 我们了解了如何实际进行上下文切换 今天我们正在研究策略 所以我们将学习操作系统如何决定要运行哪个过程 我们将讨论操作系统可能想要优化的不同指标 如通过量或周转时间或响应时间 你将学习存在许多不同的任务调度策略

05:24
We will learn how real schedulers handle a mix of interactive and batch tasks and then what you do in these practical situations when the operating system does not have perfect information Theoretically, about what the work will do Okay what we talked about on Tuesday We introduced the concept of processes, which is the abstraction that we offer to users
我们将学习真实调度器如何处理交互式和批处理任务的混合 然后在这些实际情况下，操作系统没有完美的信息时，你会做什么 从理论上讲，关于工作将要做什么 好的 我们周二讨论了什么 我们引入了进程的概念，这是我们提供给用户的抽象

05:45
So that we can virtualize the CPUs in each process can consider that they have exclusive ownership of the CPU We see that we will use time sharing in the operating system to make context switching between competing processes Yes, we have briefly discussed the three states that each process can be in when you are using the CPU
以便我们可以在每个进程中虚拟化CPU 可以认为它们对CPU有独占所有权 我们看到我们将在操作系统中使用时间共享 以在竞争的进程之间进行上下文切换 是的，我们简要讨论了每个进程可能处于的三个状态 当你在使用CPU时

06:05
You're running and then you might be canceled but you still have useful work to do You'll be put in the ready queue At that point you want to use the CPU but the scheduler doesn't allow you to use the CPU at some point you'll be scheduled again You're going to run again Maybe then you'll start some Io when you start
你在运行 然后你可能被取消 但你仍有有用的工作要做 你将被放在就绪队列中 在那个时候你想使用CPU 但调度器不允许 你使用CPU 在某个时候你会再次被调度 你将再次运行 也许那时你会启动一些 我o 当你启动

06:24
I'm in a blockage state and can't do any useful work There's no reason to put you on the CPU because you're waiting for information that you know read from the disk and come back or you're waiting for a packet on the network or you're waiting for a user input on the keyboard You're waiting for information in that state
我o 然后你处于阻塞状态，无法做任何有用的工作 没有理由把你放在CPU上 因为你在等待 你知道从盘上读取并返回的信息 或者你在等待网络上的数据包 或者你在等待键盘上的用户输入 你在等待处于那个状态的信息

06:42
So when you get that message when the read is complete you go back to the ready queue maybe you're going to be scheduled by cp by the operating system So, how do you implement all these transformations today, that's a mechanism we're talking about which process to pick from the ready queue and put it into the running state okay
所以当你收到那个信息时 当读取完成时 你会回到就绪队列 也许你会被cp调度 由操作系统调度 所以，你今天是如何实现所有这些转换的，那是一个机制 我们正在讨论从就绪队列中选择哪个进程并将其放入运行状态 好的

07:00
It's as simple as thinking about how many processes might be simultaneously in each state, let's say it's a unit processor system, so at most there's only one process running, and we're just having one core, and that's what we're assuming here, to keep things simple, what is the number of processes that are ready yes any number
这么简单的问题 思考一下每个状态中可能同时存在的进程数量 假设是一个单元处理器系统 所以最多只有一个进程正在运行 我们只有一块核心 这是我们在这里假设的，以保持事情简单 就绪的进程数量是多少 是的 任何数字

07:24
yes all the other processes that you want to run so many may be ready And then what some people don't know is how many processes are probably blocked You may have thousands of processes that are doing me oh all waiting for some I oh to finish okay yes absolutely and we're not going to talk about that
是的 想要运行的其他所有进程 那么多可能已经就绪 然后，一些人不知道的是，可能有多少进程被阻塞 你可能有千千万万的进程，都在做 我哦 都在等待一些 我哦要完成 好的 是的 是的 绝对地 而且我们不打算谈论那个

07:48
There are a lot of interesting policies that you can do by how do you decide where to run which process right now, not just when the foundation starts with this and then they build on top of it, but multiple cores, you will have multiple running processes, and we assume that one core is okay, so we learned about finite direct execution for optimal performance
有很多有趣的政策你可以通过 你现在如何决定在哪个地方运行哪个过程 而不是仅仅当基础从这个开始 然后他们就在上面构建 但是 多个核心你将有多个运行的过程 我们假设一个核心是可以的 所以我们学习了关于有限直接执行的知识，以获得最佳性能

08:11
We basically just want the user process to run and do all the arithmetic instructions or whatever they need to do, and only if those processes need to do a special task when they need to access a device with special privileges and that's where we switch to the OS, through the system call and the OS will do all the checks it needs to do
我们基本上只是想让用户进程运行并执行所有的算术指令 或者他们需要做的任何事情 并且只有在那些进程需要执行特殊任务时 当他们需要访问具有特殊特权的设备时 那就是我们切换到os的地方，通过系统调用 并且os将做它需要做的所有检查

08:30
Make sure this process has the right permissions to access the file like one and then do that in the kernel Then another thing we need to add is that we need these timer interrupts so that we can periodically grab control from the process and force it to switch to another OK so this is something new today
确保这个进程有正确的权限来访问文件 例如 一 然后在内核中做那个 然后我们需要添加的另一件事是我们需要这些定时器中断 这样我们定期可以抓取 从进程中控制并迫使它切换到另一个人 好的 所以这是今天的新东西

08:50
Well, we're going to have a lot of terms We're going to have a workload like each of you has a course workload that's trying to balance out that we're trying to get the best performance and we're going to have a workload that's trying to get the best performance for how we're going to describe the work in the workload is there's some arrival time and then there's some amount of CPU that needs to be used
嗯我们将有许多术语 我们将有一个工作负载 就像你们每个人都有一个课程工作负载，正在努力平衡 我们有一份工作负载，正在努力获取最佳性能 对于我们将如何描述工作负载中的工作 是存在一些到达时间 然后存在一些CPU需要使用的量

09:09
What is the runtime in this current CPU burst and then we don't use the term process anymore We're going to talk about work So because scheduling is a more abstract concept than that, because we've been doing scheduling for work You know, in manufacturing and many other fields other than operating systems, so we use the term work
在这个当前CPU爆发中的运行时间是多少 然后我们不再使用术语进程 我们将谈论工作 所以因为调度是一个比那更抽象的概念 因为我们一直在做工作的调度 你知道在制造业和许多其他领域 除了操作系统之外 所以我们使用术语工作

09:30
But you should basically think of work as just the next CPU burst of the process When the process moves between ready and waiting or blocking you are going to divide the process into tasks These are just doing CPU burst work so we don't calculate that I/O time ok and then we will have a lot of different task scheduling strategies
但你应该基本上认为工作只是进程的下一个CPU爆发 当进程在就绪和等待或阻塞之间移动时 你将将进程分成工作 这些只是在做CPU爆发的工作 所以我们没有计算那个I/O时间 好的 然后我们将有 我们将看许多不同的任务调度策略

09:49
The scheduler just needs to choose among all the ready tasks to decide which one should go into the running state and then we'll have a range of different performance metrics so depending on our workload depending on whether this is a desktop machine is not a cloud provider Whether this is an embedded system or not you may be optimizing for different performance metrics
调度器只需要在所有就绪的任务中选择 决定哪一个应该进入运行状态 然后我们将有一系列不同的性能指标 因此，取决于我们的工作负载 取决于这是不是一台桌面机 这是不是云提供商 这是不是嵌入式系统 你可能在优化不同的性能指标

10:09
In this case, you're going to make a different scheduler so those are all of them, but not all of them These are some of the metrics that the operating system might care about Today we're only talking about the two in red So, a common metric is the job turnaround time that you want to minimize and that's the time it takes for that job to complete
在这种情况下，你会制定一个不同的调度器 所以这些都是所有这些，但不是所有的 这些是操作系统可能关心的一些指标 今天我们只谈论红色的两个 所以，一个常见的指标是 你想要最小化的作业周转时间 这就是那个作业完成所需的时间

10:35
Subtract the time it arrives, when you schedule a job, it's in progress, it's going to finish, and we want to minimize that time, so you might take the average of the job turnaround time across all your workloads, response time is a similar metric, but now you just look at the time we start scheduling this job minus the arrival time
减去它到达的时间 当你安排作业时 它在进行中 它会最终完成 我们想要最小化这个时间 因此 你可能取你所有工作负载中作业周转时间的平均值 响应时间是一个类似的指标 但现在你只看我们开始安排这个作业的时间 减去到达时间

10:57
So, the idea here is that the scheduler has no control over how much work the job needs to do If it needs to run for a minute It's weird to calculate that part of it as a scheduling metric Response time excludes the time it takes to finish that job actually work The intuition here is that the scheduler wants to minimize the response time because like an interactive job
所以，这里的想法是 调度器对作业需要做多少工作没有控制权 如果它需要运行一分钟 把它的一部分作为调度指标来计算有些奇怪 响应时间排除了完成那个作业实际工作的时间 这里的直觉是，调度器想要最小化响应时间 因为像交互作业一样

11:21
You need to schedule it immediately so that it can send the next prompt to the user to do some work or it can quickly start that i o and get i o the system is working for it so you just want to schedule things as soon as possible so that they can do a small part of their work and not be a bottleneck in the system
你需要立即安排它 以便它可以向用户发送下一个提示，让用户做一些工作 或者它可以快速启动那个i O 并获取i O 系统在为其工作 所以你只是想尽快安排事情 以便他们可以做他们的小部分工作 不要在系统中成为瓶颈

11:41
Other metrics you may care about Many systems try to maximize throughput, like the amount of work that can be done per second The number of jobs that can be done in a certain amount of time You may be worried about resource utilization You can imagine that you are a cloud provider and you have these CPUs and you want to get more money out of them from the people who buy them
你可能关心的其他指标 许多系统试图最大化通量，就像 每秒可以完成的工作量 在一定时间内完成的作业数量 你可能担心资源利用率 你可以想象你是云提供商 你有这些CPU 你想要从中获得更多的钱 从购买它们的人中

12:04
So you want to keep those devices busy all the time because when the devices are busy that's when you're charging customers cloud providers may try to maximize resource utilization through their scheduling If you're really worried about overloading you may want to make sure that you're reducing the number of context switches so that you don't do any useful work
所以你想要始终保持这些设备忙碌 因为当设备忙碌时 那就是你向客户收费的时候 云提供商可能会试图最大化资源利用率，通过他们的调度 如果你真的很担心过载 你可能想要确保你减少了上下文的切换次数 这样你就不会做任何有用的工作

12:20
For any process that is useful work, when you're doing these context switches, that's the extra overhead that the operating system adds, and we saw in the last lesson that the work involved in doing context switching you need to save some registers, jumps, save stacks, and so on, but what is the really important feature of context switching
对于任何进程 有用的工作 当你在进行这些上下文切换时 对 这就是操作系统添加的额外开销 我们在上一堂课中看到了执行上下文切换所涉及的工作 你需要保存一些寄存器 跳转 保存栈 诸如此类 但是关于上下文切换的真正重要特性是什么

12:45
It's that it hurts the cache locality of the running process, so you're running a process, and its cache is all kept very good, it's loaded, and then if you switch to another process, the next process needs to load the cache of its working set, so if you do a lot of context switching, you're going to have more overhead, and that's probably something you're worried about
是它损害了正在运行的进程的缓存局部性 所以你正在运行一个进程 它的缓存都保持得很好，加载了 然后如果你切换到另一个进程 下一个进程需要加载其工作集的缓存 所以如果你做很多上下文切换 你将有更多的开销 这可能是你担心的事情

13:04
Or maybe you're worried about fairness, we want all processes to be treated fairly, and you also want to minimize the change in CPU time that you give to each process, and fair, but we're not going to look at any of these metrics in order to keep it simple in this class, but if you keep digging into scheduling, you're going to see good
或者你可能担心公平性 我们想要所有进程都被公平对待 你也希望最小化你给予每个进程的CPU时间的变化 并且公平 但我们不会看任何这些指标 为了在这门课上保持简单 但如果你继续深入研究调度，你一定会看到 好的

13:27
So what we're going to do today is we're going to start with a lot of assumptions about our workload We're going to start with very easy assumptions We're going to look at the best scheduling strategy for those assumptions We're going to look at a metric and we're going to gradually remove the assumptions and see how we need to change our scheduling strategy to do better
所以今天我们要做的是 我们将开始以对我们工作负载的许多假设开始 我们将从非常容易的假设开始 我们将查看针对这些假设的最佳调度策略 我们将看一个指标 然后我们将逐渐删除假设 并看看我们需要如何更改我们的调度策略来做得更好

13:44
Based on these new assumptions look at some new metrics Okay These assumptions are very unrealistic from the beginning We're going to gradually remove these to make them more realistic So we're going to start assuming that each task is running for the same amount of time Sounds easy We're going to assume that all tasks arrive at the same moment We're going to assume that all tasks are using only the CPU
基于这些新的假设 看一些新的指标 好的 这些假设从一开始就非常不现实 我们将逐渐删除这些，使它们更现实 所以我们将开始假设每个任务运行相同的时间 听起来容易 我们将假设所有任务都在相同的时刻到达 我们将假设所有任务只使用CPU

14:06
We don't worry about IO first, and then we're going to assume that we know exactly how much CPU it takes to complete the task before we know it's done, and obviously that's very unrealistic, and we do this a lot in computer science, we assume we have perfect knowledge, and we assume that there's a god who can tell us the perfect answer
我们首先不担心IO 然后我们将假设在我们知道任务完成之前 确切地知道它需要多少CPU才能完成 显然这非常不现实 我们在计算机科学中经常这样做 我们假设我们有完美的知识 我们假设有一个神可以告诉我们完美的答案

14:25
And then we look at what kind of algorithm we can develop, and with this perfect knowledge, we can compare how our system would perform in practice, how it would behave if we had perfect knowledge, so we're going to start with that perfect knowledge and then remove it OK so our first metric as I said before
然后我们看看我们可以开发出什么样算法，有了这个完美的知识 我们可以比较我们的系统在实际中的表现，它与如果有完美知识时会如何表现 所以我们将从那个完美的知识开始，然后删除它 好的 所以我们的第一个指标 如我之前所说

14:44
Will be the turnaround time The turnaround time is just when that job is done and subtract the time it actually arrives so we should be able to calculate this very simply ok so process a arrives at time twenty and finishes at time thirty What will its turnaround time be, everyone whisper to me thank you if process b arrives at time ten and finishes at time fifty
将是周转时间 周转时间只是当那个工作完成时 并减去它实际上到达的时间 所以我们应该能够非常简单地计算这个 好的 所以过程a在时间二十到达 并在时间三十完成 它的周转时间将是什么，大家小声地告诉我 谢谢，如果过程b在时间十到达并在时间五十完成

15:12
Its turnaround time will be forty Thank you very much fifty minus ten is forty and then the average of these two will be thirty for our workload Thank you guys, okay that's how to calculate turnaround time So far, it's pretty straightforward so we're going to start looking at scheduling strategies that will optimize turnaround time so our first and easiest policy might be fifo or first-come, first-served
它的周转时间将是四十 非常感谢 五十减去十是四十 然后这两个的平均值将为我们的工作量是三十 谢谢大家，好的 这就是如何计算周转时间 到目前为止，这还相当直接 所以我们将开始看调度策略 这将优化周转时间 所以我们的第一个也是最简单的政策可能是fifo或先到先服务

15:37
We do this a lot in real life right, the first person to get to the counter gets served, then the person behind gets served, and after that, we get a lot of inspiration in the operating system from what people do in real life, and we just try to borrow all these things and make it work, and that's going to be our first simplest policy
我们在现实生活中经常这样做 对，第一个到达柜台的人得到服务 然后后面的人得到服务，在那之后 我们在操作系统中得到了很多灵感 从人们在现实生活中做的事情 我们只是试图借所有这些东西并使它工作 这将是我们的第一个最简单的政策

15:59
It's a very simple amount of work, under all these assumptions, I told you guys, we're going to get all the work to arrive at the same time about when they seem to arrive at a similar time, and I think you guys assume that work A actually arrives a little earlier than B, B arrives a little earlier than C OK and then they're each using the same CPU burst
这是一个非常简单的工作量 在所有这些假设下 我告诉过你们，我们将使所有工作在同一时间到达 大约当他们看起来到达的时间相似时 我想你们假设工作 a实际上比b早一点到达，b比c早一点到达 好的 然后它们各自在使用相同的CPU爆发量

16:20
Okay, let's calculate the turnaround time for this amount of work, using first-come, first-served services, we always have to draw these Gantt charts, and these are the most intuitive things. You can imagine that you just show which work is scheduled when, and it's a timeline, but we all call them Gantt charts, okay, now we know what Gantt charts are
好的 让我们计算这个工作量的周转时间 使用先到先服务f 我们总是要绘制 这些甘特图 这些是最直观的东西你可以想象 你只是显示哪个工作在何时被安排 它就是一个时间线 但我们都叫他们甘特图 好的 现在我们知道什么是甘特图

16:44
Work A arrives first So, it's scheduled in the first place it runs from time zero to time ten because that's the CPU time it needs B is placed in second place from ten to twenty at the next point in time C is placed in the third position it runs from thirty to forty So, what is the average turnaround time for this simplest workload
工作a首先到达 所以，它被安排在第一位 它从时间零运行到时间十 因为那就是它需要的CPU时间 B在下一个时间点从十到二十被安排在第二位 C被安排在第三位 它从三十运行到四十 那么，这个最简单的工作负载的平均周转时间是多少

17:04
Let's add up the turnaround time of ten plus the twenty turnaround time of B Thirty turnaround time of C that averages twenty seconds Okay, any questions about calculating the average turnaround time, or, how prioritization will affect this very simple workload Okay, it's going to be even more interesting Okay, so my first question is for you
我们将十的周转时间相加 再加上B的二十周转时间 C的三十周转时间 那个平均为二十秒 好的 关于计算平均周转时间有任何问题吗 或者，优先处理将如何影响这个非常简单的工作负载 好的 它将变得更加有趣 好的 所以我的第一个问题对你来说

17:35
All you need to discuss with your neighbor is let's remove the first assumption Let's take the first assumption let's say the job uses a different amount of CPU which workload performs the worst under FIFO or priority So, come up with some workloads that you can describe by workloads with different runtimes So change the column here
你所需要与邻居讨论的一切是让我们移除第一个假设 假设工作使用不同量的CPU 哪种工作负载在FIFO或优先处理下表现最差 所以，想出一些你可以通过具有不同运行时间的工作负载来描述的工作负载 所以更改这里的一列

17:54
Then, which workload will have a bad average turnaround time So spend two minutes talking to people around you talking to as many neighbors as possible who come up with a workload that doesn't perform well under FIFO Yes if the first workload that arrives runs longer it will look really bad
然后，哪种工作负载的平均周转时间将不好 所以花两分钟 与周围的人交谈 你 与尽可能多的邻居交谈 好的 好的 好的 谁提出了一个在FIFO下表现不佳的工作负载 是的 如果第一个到达的工作负载运行时间更长 这将看起来非常糟糕

19:32
Now, work A runs for a hundred seconds it runs first Now we calculate the average runtime A's runtime Sorry, not the runtime A has a turnaround time of a hundred B is not placed in second place until a hundred seconds So, its turnaround time is when it finishes minus its arrival time which is far away
现在，工作A运行一百秒 它首先运行 现在我们计算平均运行时间 A的运行时间 抱歉，不是运行时间 A的周转时间是一百 B直到一百秒才被安排在第二位 所以，它的周转时间是它完成时 减去它的到达时间 这在很远的地方

19:53
So, its turnaround time is one hundred and ten, and C has been waiting for a long time, so its turnaround time is one hundred and twenty, and we divide all of that by three, and we get a very long turnaround time for this workload, and for this schedule, so first-come, first-served, the service can be really bad, just a matter of luck
所以，它的周转时间是一百一十 C也等了很长时间 所以，它的周转时间是一百二十 将所有这些除以三 我们得到一个对于这个工作负载非常长的周转时间 对于这个时间表来说 所以先来先服务 服务可能会非常糟糕 只是运气问题在于

20:09
So I think this gives a good understanding of what kind of scheduling strategy we should have, intuitively we do it better, if we schedule that long task ahead of time for those short tasks, so in real life we see a lot of that, so of course you can think, there's a very slow kind of task
谁到达的时候 所以我认为这个给得很好的理解 对于应该采取什么样的调度策略来说，没有什么比这更好了 直觉上我们做得更好 如果我们提前为那些短任务安排了那个长任务 所以在现实生活中我们也看到了很多这种情况 所以当然你可以想，有一种非常慢的任务

20:29
The cars that control this race No one is allowed to overtake it when you're in a single lane on the highway and there's a really slow vehicle driving you crazy and they're slowing you down too, so of course, whenever you go to the store you see somebody with a lot of stuff in their cart and you only have small purchases and you really want to be at the front of that line and get served first
控制这场比赛的汽车 没有人被允许超过它 当你在高速公路上开单车道时 并且有一辆真的很慢的车辆在让你发狂 他们也让你慢下来 所以当然，每当你去商店时 你看到有人购物车里有很多东西 而你只有小小的购买 你真的很想能排在那个队伍的前面，首先得到服务

20:57
This happens a lot and it's not just limited to computer systems okay so what we want to do is we don't want this short task to wait for a long task So that's the name of our next scheduler It's intuitively called shortest job first or sjf we're going to choose the task with the shortest running time but again let's say we have this crazy thing, we have the perfect message
这种情况经常发生 不仅限于计算机系统 好的 所以我们想做的是 我们不想让这个短任务 等待长任务 所以这就是我们下一个调度器的名字 它被直觉地称为最短作业优先或sjf 我们将选择运行时间最短的任务 但是再次假设我们有这种疯狂的事情，我们有完美的信息

21:18
This will remove this assumption later, but now we know how long the task will take, so now when we draw the Gantt chart, B and C go first, A comes in third, and when we calculate the average run time of the fifo, it's 110, but for this new schedule, B has a turnaround time of 10
这将在后来移除这个假设 但现在我们知道任务需要多长时间运行 所以现在当我们绘制甘特图时 B和C首先去 A排在第三 当我们计算fifo的平均运行时间时 它是110 但对于这个新的时间表 B的周转时间为10

21:39
C has a turnaround time of 20 and A has a turnaround time of 120 but you divide that by 3 and then you get 50 seconds as the average turnaround time for this workload compared to the shortest job priority If you like theory theory and the operating system sometimes mix this is a small example where you can prove that the shortest job priority is optimal
C的周转时间为20 A的周转时间为120 但你将那个除以3 然后你得到50秒作为这个工作负载的平均周转时间 与最短作业优先相比 如果你喜欢理论 理论与操作系统有时会混合 这是一个你可以证明最短作业优先是最优的例子的小例子

22:09
If you assume you're minimizing the mean turnaround time and that's the metric you're concerned about, you can't prove that the attributes are for different criteria, and you assume there's no preemption, so let's assume that when the task arrives, you can't simply switch to another task, and we'll consider changing that assumption later
如果你假设你在最小化平均周转时间 并且那是你关心的度量 你不能证明这些属性对于不同的标准 并且你假设没有预emption 所以，我们假设当任务到达时 你不能简单地切换到另一个任务 我们将 later 考虑改变这个假设

22:30
Well, so, we're not going to prove that because I think the intuition is pretty straightforward is that if you move a shorter task in our schedule before a longer task, that will improve the turnaround time for that short task, and that's that we move in front of you more than damage the long task, and after that short job is done, we're going to move
嗯 所以，我们将不会证明那个 因为我认为直觉相当直接 那就是如果你在我们的日程中移动一个较短的任务之前，一个较长的任务 这将提高那个短任务的周转时间 那就是我们移动在前面比伤害长任务的周转时间更多 在那份短暂的工作完成后，我们将搬家

22:48
So in general, we help more than we hurt, so it's always best to push short work first, yes, great, one of the problems with SJF is that you may have hunger, where that long-term job keeps being postponed, because short jobs keep coming, so we do this in practice, and we can't allow hunger to be possible
所以总的来说 我们帮助的一方比伤害的一方多 所以总是最佳的先推短工作 是的 太好了 sjf的一个问题是你可能有饥饿 那里那项长期工作就一直被推迟 因为短工作不断到来 所以我们在实际操作中这样做 我们不能允许饥饿成为可能

23:19
People hope that their work will eventually work, so when we look at the last reality scheduler, there's a hunger mechanism to make sure that doesn't happen, but yes that's a question of these optimal things yes okay hunger problem is understood by all people is great okay so let's remove the second hypothesis now
人们希望他们的工作最终能够运行 因此，当我们看到最后的现实调度器时 会有一种饥饿机制来确保这不会发生 但是，是的 这是这些最优化事物的一个问题 是的 好的 饥饿问题是否所有人都理解了 太好了 好的 那么让我们现在删除第二个假设

23:41
Let's assume that now work can arrive at different times so this could be what our workload looks like Can you take a minute to draw a Gantt chart and the average turnaround time for this workload takes precedence over the shortest work So make sure you see the fact that they arrive at different times So what will the Gantt chart look like
让我们假设现在工作可以以不同的时间到达 所以这可能是我们的工作量看起来的样子 你能否花一分钟时间绘制甘特图 并且这个工作量的平均周转时间以最短工作优先 所以请确保你看到他们以不同的时间到达的事实 那么甘特图会是什么样子

24:05
Your turnaround time will take two minutes to discuss please okay so I think you all see "But, the main question is clear" "What do you do when jobs B and C arrive at ten?" The problem with shortest job priority is that it is a non-preemptive scheduler" and it has to run that task until it is complete
你的回转时间将花费两分钟讨论 请 好的 所以我认为你们大家都看到了 "但是，主要问题是明确的" "当工作B和C在十点时到达时，你做什么？" "最短作业优先的问题在于它是非抢占式调度器" 它就必须运行那个任务，直到完成

25:33
"Until it voluntarily frees up the CPU by performing input/output operations" or simply by calling exit, making the scheduler prioritize the shortest task It can't do anything When b and c arrive and make a different decision, time cannot be turned back.
"直到它自愿通过执行输入输出操作释放CPU" 或者仅仅通过调用exit，使得调度器优先处理最短的任务 它做不了任何事情 当b和c到达并做出不同的决定时，时间无法倒流。

25:47
It's stuck on scheduling until one releases the processor at time one hundred, and then it can make a decision for the shortest job priority when that job completes, those jobs that are now in the ready queue, so that doesn't do a very good job if we calculate our average turnaround time of a is one hundred b
它卡住了在安排 直到一个在时间一百时释放处理器 然后它可以为最短作业优先做出决定 当那个作业完成时，那些现在在就绪队列中的作业 所以这并没有做得很好 如果我们计算我们的平均周转时间 的周转时间为a是一百b

26:10
It arrives at time ten so this is a common mistake people make not assume that the turnaround time is one hundred and one ten It is not the same as the finish time You have to remember to subtract the time it arrives so don't make this little mistake For c, it finishes at one point twenty but it arrives at time ten so it has a turnaround time of one hundred and ten
它到达时间十 所以这是人们常犯的错误 不假设周转时间为一百一十 它不是与完成时间相同的 你必须记住要减去它到达的时间 所以不要做这个小错误 对于c来说，它在一点二十完成 但它在时间十到达 所以它的周转时间为一百一十

26:30
Take the average of this and we get a really bad number Okay, so it's not optimal, once you can have preemption in your system, that's what we're going to add now, so first come first, prioritize the shortest jobs, those are non-preemption schedulers, they can only choose when a running process leaves the system or starts
取这个的平均值 我们得到一个非常糟糕的数字 好吧 所以这不是最优的 一旦你可以在你的系统中有预emption 这就是我们现在要添加的 所以先来先 优先处理最短作业 那些是非预emption调度器 他们只能选择当一个运行中的进程离开系统或启动时

26:51
I o then it can go to that ready queue and look at all the processes there and choose the best job or the shortest job to schedule at that time it doesn't have the option to take a running job and force cancel it doesn't allow to take a running job and choose another better job to replace it
我o 然后它可以去那个就绪队列并查看那里的所有进程 并选择最佳作业或最短作业进行安排 在那个时候 它没有选择夺取一个运行中的作业并将其强制取消的选项 不允许夺取一个运行中的作业 并选择另一个更好的作业以取代它

27:13
Okay, so we're going to look at some preemption schedulers that are able to grab a running job and force it to cancel and put it in the red queue, so the preemption version of the shortest job priority will be called the shortest completion time priority because that's the metric we want to consider
好的 所以我们现在 将看看一些预emption调度器 能够夺取一个运行中的作业并将其强制取消 并将它放入红色队列 所以最短作业优先的预emption版本 将被称为最短完成时间优先 因为那是我们想要考虑的度量

27:32
We want to see how long it will take for this job to finish Not the total time of that job because maybe it has run in the past it has been canceled now now it is back We want to see how long it will take for it to finish now Well, so it always has to run yikes everything is fine it always wants to run this job
我们想要查看这个作业完成还需要多长时间 不是该作业的总时间 因为也许它在过去运行过 它被取消过 现在它回来了 我们想要查看它现在完成还需要多长时间 嗯，所以它总是要运行yikes 一切都好 它总是要运行这个作业

27:55
But we're going to do the quickest good so let's say um, is the mic in a mode where I'm screaming in it, or you can't hear me or can you usually hear okay okay if you can't hear it, you're going to start complaining if you can't hear, that's good So that's the Gantt chart that we prioritize by the shortest completion time
但是，我们将完成最迅速的 好的 所以让我们说 嗯，麦克风是否处于一种模式，我在其中尖叫，或者你听不到我 或者你通常能听到吗 好的 好的 好吧 如果你听不到，你会开始抱怨 如果你听不到，那就好 所以这就是我们按照完成时间最短优先的甘特图

28:20
Sometimes we call this CTF the shortest completion time priority, I don't care how you abbreviate this algorithm Okay, so with this amount of work, what we do now is we start scheduling from time zero because that point is the only ready work, and then, at ten o'clock, when B and C arrive
有时候我们也叫这个为ctf 就是按照完成时间最短优先 我不在意 你怎么缩写这个算法 好的 所以以这个工作量 我们现在要做什么 是我们开始从时间零开始安排 因为那个点是唯一准备好的工作 然后，到了十点钟 当b和c到达时

28:42
We can look at those two and we're going to compare the time a has left to finish which is ninety and you have to remember to subtract from the work that a has done But my example is too simple for this question Well, but you do need to think about how much time a has left when you decide whether you should schedule B or C so in this case, it doesn't matter if you schedule B and C to finish
我们可以看看那两样 我们将比较a剩余的完成时间 那是九十 你一定要记住从a已经完成的工作中减去 但我的例子对于这个问题过于简单 嗯 但你确实需要考虑a还剩下多少时间 在你决定时 你是否应该安排B或C 所以在这种情况下，安排B和C完成并不重要

29:07
And then we go back to A because it's the only work we have left, so now when we calculate the average turnaround time what it will be so the turnaround time for B is ten it's arrival time minus twenty for C it's thirty minus ten for twenty and for it's one hundred and twenty seconds to finish is it
然后，我们回到A，因为它是我们剩下的唯一工作，所以 现在当我们计算平均周转时间 这将是多少 所以B的周转时间为十 它是到达时间减去二十 对于C 它是三十 减去十为二十 并且对于 完成需要一百二十秒的是它

29:31
So that's its turnaround time Ask first about the shortest completion time yes so your question is how does the CPU or operating system know the remaining time for this process So now we're just assuming that we magically know that we have some oracle in a perfect way to know these types of theoretical algorithms
所以这就是它的周转时间 关于完成时间最短的问题先问 是的 所以您的问题就是 CPU或操作系统如何知道剩余的时间供此过程使用 所以现在我们只是假设我们神奇地知道这一点 我们有一些神谕 一种完美的方式来知道这些类型的理论算法

30:00
And then we're going to figure out how to approximate this knowledge and learn this we haven't taken into account the response time metrics yet, we're going to think about this very quickly, yes, for the PC, this but what speed is it running, yes, for now, it's like this, when B and C arrive at the system, we're going to have some ways to look at and see
然后，我们将找出如何近似这种知识和学习这种知识 我们还没有考虑响应时间指标 我们将很快考虑这个问题 是的 对于电脑 这个 但它正在运行什么速度 是的 就目前而言，是这样的 当B和C到达系统时 我们将有一些方法可以查看并看到

30:41
How much time is left in B It's ninety, which is greater than ten for B and C So we're going to preemption A this is the remaining time which is the important thing here It's the time to finish or the time left for that task so you can come up with more interesting workloads, and that's really important where you really want to see the last bit of what you want to get that task scheduled for you
B还剩下多少时间 它是九十，大于B和C的十 因此，我们将预emption A 这是剩余时间 这是重要的事情在这里 它是完成时间或那个任务的剩余时间 所以你可以想出更有趣的工作负载，在那里这确实很重要 你真的想要见到你想要得到那个任务的最后一点点被安排

31:05
Instead of looking at what is the length of the full task, if it's only a little bit of work left, you definitely want to schedule that task to do that little bit of work, that's what you want to look at, what is the time left, yes, so that's a good example, what run time should we look at here, let's set this to fifteen
而不是看 全任务的长度是多少 如果它只剩下一点点工作 你肯定想要安排那个任务来完成那点点工作 这就是你想要看的 剩余时间是多少 是的 所以那是一个好例子 在这里我们应该看什么运行时间 让我们把这个设置为十五

31:28
If this is this, we're going to schedule A first, but at this point it's only five left, so it's going to stay scheduled instead of switching to B or C, which is a good counterexample, imagine this for fifteen, see how that changes things, questions about minimum finish time or minimum time remaining first That's another good name
如果这是这个 我们将首先安排A 但在这个时候它只剩下五剩余 所以它将保持安排而不是切换到B或C 这是一个好的反例 想象这个为十五 看看这会如何改变事情 关于最短完成时间或最短剩余时间首先的问题 这是一个好的另一个名字

31:55
Okay, okay, now, we're going to remove that they only use the CPU okay so we haven't really thought about the CPU yet, a way that you can visualize like this is not what I want you to do is think about this as a big task it's a process A that alternates CPU and hard drive so if you think of all of that as a CPU
好的 好的 现在，我们将删除那个 他们只使用CPU 好的 所以我们还没有真正考虑CPU 一种你可以这样可视化的方式 这并不是我想要你做的 是思考这个作为一个大任务 它是过程A 它交替使用CPU和硬盘 所以如果你将所有这些视为CPU

32:21
Burst things are not going well we are holding the CPU and we are blocking on the hard drive What we want to happen We want B to run in these small intervals A is blocked It is using the hard drive We want B to be arranged there in these intervals that will naturally arise from what we are talking about
爆发 事情并不顺利 我们正握着CPU 我们在硬盘上阻塞 我们希望发生的事情 我们希望B在这些小间隔中运行 A被阻塞 它正在使用硬盘 我们希望B在这些间隔中安排在那里 这将自然地从我们正在谈论的事项中自然产生

32:50
As long as we think of A as each being a separate little work package So, we can think of it as one, two, three, four, five each has its arrival time okay so if you think it's awareness of knowing IO state Now we have B which is a really long CPU binding work we have a one
只要我们将A视为每个都是单独的小工作包 所以，我们可以将其视为一、二、三、四、五 每个都有其到达时间 好的 所以 如果你认为这是了解IO状态的意识 现在我们有B 这是一个真的很长的CPU绑定工作 我们有一个一

33:12
When we look at that one that has a tiny CPU burst so we're going to schedule this one first and use the shortest job first or the shortest completion time first because it has a short CPU burst so naturally that's what we're going to choose first that it's going to use the CPU and then it's going to go and make this hard drive request
当我们看那个 它有一个微小的CPU爆发 所以我们将首先安排这个一，使用最短作业优先或最短完成时间优先 因为它有一个短的CPU爆发 所以自然这就是我们会首先选择的 它将使用CPU 然后它会去发起这个硬盘请求

33:28
At this point A will be in a blocking state, right, it can't be scheduled, it has no work to do until the IO is done, so now A has left the system, it's not in the ready queue, it's in the blocking queue, the operating system can schedule another process to schedule, in our case, only B is there so it will schedule B for a while
这时A将处于阻塞状态，对吗 它无法被安排 它没有工作要做，直到IO完成 所以现在A已经从系统中离开了 它不在就绪队列中 它在阻塞队列中 操作系统可以安排另一个过程进行调度 在我们的例子中，只有B在那里 所以它将为B安排一段时间

33:54
Now when A finishes its hard disk at time twenty we can think of another job A two is arriving in the system and it also has a really short CPU burst Since A's CPU burst is shorter than B's, it's a very long running job, and if we just follow the natural TCF algorithm, then A should preempt B, right?
现在 当A在时间二十完成其硬盘时 我们可以考虑另一个工作 一个二正在系统到达，它也有一个真的很短的CPU爆发 由于A的CPU爆发比B短 这是一个运行很长的工作 如果我们只是按照自然的TCF算法来做 那么A应该预emption B，对吗

34:17
And that's what we're going to do, and then A doesn't use the CPU again for a long time because it's this IO binding or interactivity work it goes to send some work to the hard disk and there's nothing running on the CPU We run B and we do this forever and always good so it's natural as long as you think of the process as if it's made up of multiple bursts
这就是我们会做的 然后A不会再次使用CPU很长时间 因为它是这个IO绑定或交互工作 它去发送一些工作到硬盘 CPU上没有任何运行 我们运行B，我们做这个永远和永远 好的 所以这就自然而然的 只要你把过程看作是由多个爆发组成的

34:38
They use the CPU there, and then they go to the hard drive, and we use my shortest finish time to schedule each small burst, and first of all, you're going to get very efficient results with the CPU and the hard drive, so whatever you have on that, yes, we're talking about how to do it today, like in those charts when I say runtime
他们在那里使用CPU 然后它们去使用硬盘 我们就使用我最短的完成时间来安排每个小爆发 首先 你将得到使用CPU和硬盘非常高效的结果 所以有任何关于这个问题的 是的 我们今天谈论的是如何做到的 就像那些图表中当我说运行时间时

35:07
Oh, that's terrible, yes, it's like CPU burst time, that's the same thing, CPU burst of this thing, it's like CPU burst here, yes, so of course, if we're talking about a process and not a task, then run time is like if you do top or look at some stats of a process in Linux
哦 这太糟糕了 是的 这就像CPU爆发时间 那就是同样的事情 这个东西的CPU爆发 这就像CPU爆发在这里 是的 所以当然 如果我们在谈论的是过程而不是任务 那么运行时间就像 如果你做了top 或者在Linux中查看某个过程的一些统计

35:29
It's going to tell you the total runtime, unlike the runtime of just individual tasks or the CPU bursting with a piece of different hardware yes that's exactly what you need to do on the CPU but then you're going to have you know the hard drive controller or network card that's responsible for that job and you don't have to run on the CPU for that job
它将告诉你总运行时间，不像只有个别任务的运行时间 或者CPU爆发 一块不同硬件 是的 正是如此，你在CPU上需要进行一些设置 但是然后你将有 你知道 负责那项工作的硬盘控制器或网络卡 你不必为那项工作运行在CPU上

35:54
I'm going to finish So that's why we want to do enough work just on that CPU to move the work to other resources so that it does something for other resources That's exactly what yes that's very important And then we always assume that you can have multiple processes all of which are using the hard disk at the same time and that's what we're assuming
我将完成 所以这就是我们想要只在那个CPU上完成足够工作的原因 将工作移动到其他资源上，使其为其他资源做点什么 正是如此 是的 这非常重要 然后我们总是假设你可以有多个进程 所有这些都在同时使用硬盘 这就是我们的假设

36:17
All of these things can be waiting for I/O and they're all doing some progress We're not actually modeling how much slower the hard drive will be when you have five processes waiting for I/O compared to having just one process okay so the most interesting assumptions now Let's start removing the knowledge of exactly how long the work will take
所有这些事情都可能在等待I/O 而且它们都在做一些进步 我们实际上不会建模 当你有五个正在等待I/O的进程时，硬盘的速度会慢多少 与只有一个进程相比 好的 所以现在最有趣的假设 让我们开始移除对工作将需要多长时间精确了解的知识

36:41
Okay, let's say we don't actually know how long this work will take Let's go back and see how our algorithm performs If all the work has the same length then in terms of average turnaround time, then FIFO is enough No difference so you're better off still using FIFO But when there is a big difference in job length, you need to deal with short jobs first
好的 假设我们实际上不知道这项工作需要多长时间 让我们回顾一下我们的算法是如何表现的 如果所有的工作都有相同的长度 那么在平均周转时间方面，fifo是足够的 没有差异 所以你最好还是使用fifo 但当工作长度有很大的差异时，你需要首先处理短工作

37:02
In this case, it's better to work on the shortest tasks first um, but now we're going to assume that we don't know which are short tasks and which are long tasks, so what we're going to do is we just simply try each task and the short tasks will be done naturally, and then we'll finish them, so we're just giving each a little bit of CPU time
在这种情况下，最先处理最短工作要更好 嗯 但是现在我们要假设我们不知道哪些是短任务 哪些是长任务 所以我们要做的是 我们只是简单地尝试每个任务 自然短任务会完成 然后我们就完成了它们 所以我们只是给每个一点CPU时间

37:22
And then the short tasks will eventually be done, and that's the concept of the rotating scheduler, or just r, we have a bunch of ready tasks, and we'll alternate or poll which of those tasks to run, and we'll assign a fixed time slice to each task, like two hundred milliseconds, which in modern systems is very long
然后短任务最终会完成 这就是轮转调度器的概念 或者只是r r，我们有一堆就绪的任务 我们就会交替或者轮询，让这些任务中的哪一个运行 我们会为每个任务分配一个固定的时间片 比如两百毫秒 在现代系统中，这个时间片很长

37:44
You allow the task to run that length of time and then switch to other tasks whether it wants to or not, so the intuition here is that the short tasks will be completed in fewer time slices than the long tasks, so you do move the short tasks to the front of the queue, right, so let's look at some examples here with stupid microphones
你允许任务运行那个时间长度 然后切换到其他任务 无论它愿不愿意 所以这里的直觉是，短的任务 它们将用比长任务少的时间片完成 所以你确实把短任务移到了队列的前面，对吧 那么让我们来看看一些例子在这里 愚蠢的麦克风

38:08
Okay, so we have three jobs of different lengths This is the case with FIFO and it's not doing a good job Our average turnaround time is ten plus twelve plus fourteen divided by three, now the average twelve Let's take the polling method, run a loop the second time in this example, and then wait another second for a
好的 所以我们有三份工作，长度不同 这是fifo的情况 它做得并不好 我们的平均周转时间为十加十二加十四 除以三，现在为平均的十二 让我们采用轮询方法，运行一个循环第二次 在这个例子中 然后为a再等待一秒钟

38:28
And then wait another second for c and then we go back to a and b, c is now done, just like b because they only need two seconds of CPU so then we just run a until it finishes so the rotation scheduling is preemptive even if that task still has work to do The scheduler takes it off the CPU and puts it in the ready queue
然后为c再等待一秒钟 然后我们回到a和b，c现在已经完成，就像b一样 因为他们只需要两秒钟的CPU 所以然后我们就只运行a，直到它完成 所以轮转调度是抢占式的 即使那个任务还有工作要做 调度器将其从CPU上取下，并将其放入就绪队列

38:49
Okay, so the average turnaround time of the rotation scheduling Please help me calculate what the completion time of this task B is about 14 in this very clear diagram of mine, that task is completed at time 5 when it reaches zero, so its completion time is five, task c is about 6, task A is about fourteen
好的 所以轮转调度的平均周转时间 请帮我计算这个 b的任务完成时间大约是多少 能在我的这个非常清晰的图中指出来吗 那个任务在时间五完成 它到达零时 所以它的完成时间就是五 任务c的完成时间大约是六 任务a的完成时间大约是十四

39:36
And then you need to do some math and that's what you end up with, right, so it does a lot better than FIFO but it doesn't do it better than that optimal shortest job first but it gets you closer to that so if you don't know the run time rotation scheduling can do well with a lot of job length variations
然后您需要做一些数学 这就是您最终得到的结果，对吗 所以它比fifo做得好多了 但它不会比那个最优的最短作业优先做得好 但它能让你更接近那个 所以如果你不知道运行时间 轮转调度在作业长度差异很大的情况下可以做得很好

39:59
But can you think of an example where rotation scheduling is going to be extremely bad in turnaround time units yes three great so if you have three tasks of equal length, rotation scheduling is going to be the worst thing you possibly can do because now they're done at the same time it's very far behind
但你能想到一个例子吗 在哪里轮转调度将会极其糟糕 在周转时间单位上 是的 三个伟大 所以如果你有三项长度相等的任务 轮转调度将是你 possibly 能做的最糟糕的事情 因为现在它们同时完成 这是非常靠后的

40:19
So if all of our tasks are about the same length, first of all, the service will choose to be decisive and make some decisions and at least get a way to make people happy and get it done quickly, um, but rotation, it's like trying everybody to see how you're going to do it, are you fast or slow, and finally find out that they're all slow
所以如果我们的所有任务都大约相同长度 首先 最先 服务会选择 是决定性的 做出了一些决定 并且至少得到了一种能让人快乐并很快完成的方式 嗯 但是轮换制 这就像尝试每个人 看看你将如何完成 你是快还是慢 最后发现他们都很慢

40:40
They all took the same amount of time, so on a first-come, first-served basis, the average turnaround time has been only the last ten, however, if they are all the same length, we would average out thirteen fourteen and fifteen with an average turnaround time of fourteen there, so rotation scheduling is good when you have tasks of different lengths
他们都花了相同的时间 所以以先到先得的方式，平均周转时间 已经只有过去十个 然而，如果它们的长度都一样 我们将将十三个平均起来 十四和十五的平均周转时间为十四那里 所以轮转调度很好 当你有长度各异的任务时

40:59
But it's extremely bad when all the same so you should think of these schedulers as working on ready tasks who aren't doing me oh and who's in any ready queue those are jobs that we can choose if a job I finish it goes into a blocking state on its own, and the scheduler can't even think about it
但它在所有都是相同的时候极其糟糕 所以你应该将这些调度器视为正在处理就绪的任务 谁不在做 我哦 以及谁在任何就绪队列中 那些是我们可以选择的工作 如果一份工作 我完成 它会自己进入阻塞状态，调度器甚至无法考虑它

41:25
It's just doing some other work when that I/O is done When it's done that job will be put back into the ready queue and then the scheduler can think about it again Great, when the work comes back, we'll try to stay calm so that the microphone doesn't get mad at me Well, when the job comes back, we'll treat it as a new CPU
它只是在做一些其他工作 当那个I/O完成 完成后 那份工作将被重新放入就绪队列 然后调度器可以再次考虑它 太好了 当工作返回时 我们将尽力保持冷静 以便麦克风不会因为我而生气 嗯 当工作返回时 我们将将其视为一个新的CPU

41:59
Burst a new job and follow the algorithm so it's still the same process But that's why we don't use the term 'process' where we're just scheduling these little jobs and they're CPU bursts of the process So does that answer your question I lost your tracking
爆发一个新的工作并按照算法进行操作 所以仍然是同一个过程 但这就是我们为什么不使用术语'过程'的原因 在这里 我们只是在调度这些小工作 它们是过程的CPU爆发 那么这是否回答了你的问题 我失去了你的跟踪

42:13
yes um-hmm okay great, great, so I think that's what we're going to talk about I don't know it's not the next one so yes the scheduler needs to decide how long the time slice should be There are a lot of different factors to consider there, so if it's very long then it's going to degrade to the same thing as the first-come, first-served service
是的 嗯哼 好的 太好了太好了 我认为这就是我们要讨论的 我不知道它不是下一个 所以是的 调度器需要决定时间片的长度应该多长 那里有很多不同的因素需要考虑 所以如果它非常长 那么它将退化到与先到先服务相同的东西

42:41
If a job can be done in a time slice you don't do a rotation but if it's too short then you're going to need extra overhead to do all the necessary context switching You are going to pollute the cache state by making the work switch frequently If you have a fixed time slice people will look at us we want to spread the cost of starting the cache
如果一份工作可以在时间片内完成 你没有进行轮转 但如果它太短 那么你将需要额外的开销来做所有必要的上下文切换 你将通过使工作频繁切换来污染缓存状态 如果你有一个固定的时间片 人们会看 我们想要分散启动缓存的成本

43:01
So in modern systems the time slices can be between 10 milliseconds and 200 milliseconds, but what we're going to do later today is that we're going to dynamically change the length of the time slices so that short jobs get shorter time slices and computationally intensive jobs get longer time slices, which is a good question
因此，在现代系统中 时间片可能在10毫秒到200毫秒之间 但我们今天晚些时候将要做的 我们将动态改变时间片的长度 以便短工作可以得到更短的时间片 而计算密集型工作可以得到更长的时间片 这是一个很好的问题

43:21
Yes there are more questions okay so now we will start looking at the response time for the second metric As we said, the response time is how long it takes you to receive the work schedule So in this graph B arrives at time ten and its turnaround time is the completion time thirty minus the arrival time to get twenty
是的 有更多的问题 好的 所以现在我们将开始查看第二个指标的响应时间 正如我们所说，响应时间是你收到工作安排需要多长时间 所以在这张图中 B在时间十到达 它的周转时间是完成时间三十 减去到达时间得到二十

43:48
But the response time is how long it takes to actually schedule that job, that's ten, so we start thinking about the response time, okay, because um, the rotation scheduler does a great job with response time, and I think you all have a gut feeling, so if we look at the response time of the first one, first come, first served, it has zero response time
但响应时间是实际安排那个工作需要多长时间 那就是十个 所以我们开始考虑响应时间 好的 因为嗯 轮转调度器在响应时间上做得很好 我想你们大家都有直觉 所以 如果我们看第一个的响应时间 先来先服务 它的响应时间是零

44:14
Immediately scheduled B now needs to wait five seconds, C needs to wait ten seconds Let's look at the response time for polling scheduling It would be great A needs to wait zero seconds B needs to wait one second, C needs to wait two seconds So the response time will be excellent So, if this is an interactive job or an I/O binding job
立即被安排 B现在需要等待五秒钟，C需要等待十秒钟 让我们看看轮询调度的回应时间 这将很棒 A需要等待零秒 B需要等待一秒钟，C需要等待两秒钟 因此，响应时间将非常出色 所以，如果这个是交互式工作或i/O绑定的工作

44:33
O work polling will be great because it will be able to process those requests quickly Oh for each task, the requests will be made as fast as possible So, the characteristics of the tasks really matter what are their actual characteristics They usually have these bursts, they go through them when they use the CPU and then I/O
O 工作 轮询将会很棒，因为它将能够快速处理这些请求 哦 对于每个任务，请求都将尽可能快速地发出 因此，任务的特性确实很重要 它们的实际特性是什么 它们通常具有这些爆发，它们在使用CPU时通过它们 然后进行I/O

44:51
They're not just theoretical 10 seconds with the CPU Most workloads alternating between CPU and I/O Okay, and in some cases, polling works really well, but we have to figure out how much that time slice should be set like we talked about earlier, so I think it's a good time for all of you to take a five-minute break
它们不仅仅是理论上的 使用CPU进行10秒钟的时间 大多数工作负载交替在CPU和I/O之间 好的 在一些情况下，轮询工作得非常好 但我们必须找出那个时间片应该被设置为多少 像我们之前讨论的那样 所以我认为现在是你们所有人休息五分钟的好时机

45:16
So maybe talk to your neighbors about what you all did this summer What was your best summer What was your worst summer Think back to that long summer By this time please meet some new people okay all of us now we're going to talk about the best tuna processor scheduler So, this is the best single processor scheduler that we know
所以也许和你的邻居谈谈你们这个夏天都做了什么 你最好的夏天是哪一天 你最糟糕的夏天是哪一天 回想那么久远的夏天 到这个时候 请见一些新的人 好的 所有人 我们现在要讨论最好的金枪鱼处理器调度器 所以，这是我们所知道的单处理器调度器中最佳的

46:09
It's now the basis of most schedulers and it's going to be very realistic I mean it has to be completely realistic because that's what people do So, it's going to be called a multi-level feedback queue or mlf q That's how it works basically So this works well for a general purpose operating system where you have all kinds of jobs
它现在是大多数调度器的基础 它将非常现实 我意思是它必须完全现实 因为那是人们做的事情 所以，它将被称为多级反馈队列或mlf q 这就是基本工作方式 因此，这对于通用目的的操作系统来说效果很好 你有各种工作

46:29
So you have some interactive jobs, they're short-lived, you need to get a quick response to these jobs, and then, you have some batch work, and that's what we call They're very computationally intensive, they're computationally intensive, and they're computationally intensive, and they're using a lot of CPU time, and we need to get a good response time to these interactive jobs
所以你有一些交互式工作，它们寿命短 你需要对这些工作得到快速响应 然后，你有一些批处理工作，这就是我们所说的 它们非常计算密集 它们计算量大 它们使用CPU大量时间 我们需要对这些交互式工作得到良好的响应时间

46:47
Throughput for batch tasks So we're going to have multiple priority levels We're going to rotate over work at the same priority level If you have a higher priority level you're going to be able to pre-load the lower levels So let's go get this okay how we set the priority levels for different systems
批处理任务的吞吐量 所以我们将有多个优先级级别 我们将在相同优先级级别的工作中进行轮转 如果你有一个更高的优先级级别 你将能够预占较低级别 所以让我们去获取这个 好的 我们应该怎么样设置不同系统的优先级级别

47:08
There are different numbers and we will use eight For example you can certainly have three Two priorities, it is not crazy that there are more differences between and you also have to decide how to number which are high priority levels and which are low priority levels Surprisingly, there is no generally accepted convention on this issue
有不同的数字 我们将使用八个 例如 你当然可以有三个 两个优先级，之间有更多区别的情况并不算疯狂 你还必须决定如何编号 哪些是高优先级级别，哪些是低优先级级别 令人惊讶的是 在这个问题上并没有普遍接受的惯例

47:24
In different systems it seems to me to say it's intuitive obviously, bigger numbers have higher priority but when you think about how we usually number things first class second class then the lower priority is the lower number if you sort them and sort so there's no known way you always have to ask
在不同的系统中 对我来说 似乎说它是直觉的 显然，更大的数字具有更高的优先级 但是，当你考虑我们通常如何编号事物时 一等座 二等座 然后，优先级是较低的数字 如果你把它们排序并排序 所以没有已知的方法 你总是只能问

47:42
Which has a high priority so for us Q eight is the highest priority job, where you're going to have multiple jobs, maybe some queues can be vacated, etc., so let's just look at the multilevel Q doesn't have any feedback on how this basically works, if one job has a higher priority than the other, we're always going to just run A better than C
哪个优先级高 所以对我们来说 Q八是最高优先级的工作 在那里你将有多个工作 也许一些队列可以空出来等等 所以让我们首先只看多级 Q没有任何反馈 这基本上如何工作 如果一个工作的优先级高于另一个 我们总是只会运行a优于c

48:06
We never run c if a is ready, again it's just work ahead of time If a job is blocked we don't have work in these queues It's in a separate queue If this job is waiting i to finish but if we have two jobs with the same priority then we'll rotate between them
我们永远不会运行c 如果a就绪，再次 这只是超前的工作 如果一个工作被阻塞 我们没有这些队列中的工作 它在一个单独的队列中 如果这个工作正在等待i 以完成 但如果我们有两个优先级相同的工作 然后我们将在它们之间进行轮转

48:22
Because they look pretty similar so the next question is how to prioritize work in some systems you can have a purely static approach so like in a live system if you know that something is really important and needs to be run and there are some background tasks
因为它们看起来相当相似 所以下一个问题是 如何在一些系统中设置工作的优先级 你可以有一个纯粹的静态方法 所以像在实时系统中 如果你知道a是 something真的很重要并且需要真正运行和d有一些背景任务

48:40
You can probably set those priorities statically and the system will work very well because you have complete control over everything that is running, but in a system for general purpose when we don't know what work is going to arrive and we have to keep everyone happy We're going to do something dynamic, and we're going to move work between priority levels
你可能可以静态设置那些优先级，系统将工作得很好 因为你对正在运行的一切都有完全的控制 但在通用目的的系统中 当我们不知道什么工作将要到达 并且我们必须让每个人都满意 我们将做一些动态的，我们将工作移动到优先级级别之间

48:57
And see where they fit naturally because the idea is that we want those interactive work to permeate to the top we want CPU-bound work to go down and we want longer time slices here, shorter time slices there yes so we're going to dive into how we're going to do some feedback here
并看看他们自然适合在哪里 因为想法是我们想要那些交互性的工作渗透到顶部 我们想要CPU绑定的工作下去 并且我们想要这里更长的时间片，那里的时间片更短 是的 所以我们将深入探讨我们将如何在这里进行一些反馈

49:21
So in the operating system, what we usually do is at least we use the past behavior of the process to predict the future that we don't know and how this thing will behave in the future So let's assume that it will do everything it did in the past that you can imagine that if you know what is happening, you could probably play the game
所以在操作系统中，我们通常做的事情 至少是我们使用过程的过去行为来预测未来 我们不知道 和未来这个事物将如何行为 所以让我们假设它将做它过去所做的一切 你可以想象 如果你知道那是在发生的事情，你可能可以玩游戏

49:40
But that's the best way we know that we're going to see again that when we look at the memory system, as we assume that a process has memory access similar to past accesses, so maybe you've seen in architecture courses you know why cache works so well because it's what memory addresses in the past are very close to how close the process access matches
但这是我们所知道的最好的方法 我们将再次看到当我们看内存系统时，我们假设的那样 一个过程的内存访问类似于过去的访问 所以也许你在架构课程中看过 你知道 为什么缓存工作得好 因为它是过去什么内存地址是过程访问的匹配程度非常接近

49:58
What is it going to do in the future, so it's very common to do okay, so we're guessing it's going to act like it used to, so we can make some simple rules to get the process to get the right priority level, so we're going to add a new one, just say, we're going to be optimistic, and we're going to give this process a suspicious benefit
未来它将做什么 所以这是很常见的做法 好的 所以我们猜测它像过去一样行动 因此我们可以制定一些简单的规则来获取过程 以获取正确的优先级级别 所以我们将添加一个新的，只说 我们将乐观的 我们将给予这个进程怀疑的益处

50:18
We start it as qeight we assume it will be interactive when it says it's not We're going to downgrade it and move it down How does it downgrade is if it uses its entire time slice Let's say it's a millisecond time slice if it reaches milliseconds and it still wants to use the CPU and it doesn't move to a blocked state
我们将其启动为q八 我们假设它将是交互式的 当它显示它不是时 我们将降级它并移动它下来 工作如何降级是 如果它使用其整个时间片 让我们说这里是一个毫秒的时间片 如果它到达毫秒 并且它仍然想要使用CPU 它没有移动到阻塞状态

50:40
We say hey, you're using too much CPU, you don't deserve to be at this highest priority level, we're going to downgrade you to the next one, this one is going to have a slightly longer time slice, if it uses the entire time slice, it's going to be downgraded even further, the work is going to move down the system in this way, until it finds a time slice that matches like the time slice of the CPU bursts
我们说嘿 你使用CPU太多 你不配处于这个最高优先级级别 我们将降级你到下一个 这个将拥有一个稍微更长的时间片 如果它使用整个时间片 它将被降级得更远 工作将以这种方式在系统中向下移动 直到它找到像CPU爆发的时间片一样匹配的时间片

51:03
It's a really bad picture of what would happen if there were only 3 priority levels Our work starts here It's a CPU intensive job It's still using CPU when the time slice expires The scheduler says hey you don't belong here move it here I think they should have a longer time slice
这是一个非常糟糕的图片 如果只有3个优先级级别 这将发生什么 我们的工作从这里开始 这是一个CPU密集型的工作 它仍在使用CPU 当时间片到期时 调度器说嘿 你不属于这里 把它移动到这里 我认为他们应该有一个更长的时间片

51:24
So the picture is clearer It uses the whole time slice and then it's relegated to the bottom This is how a process works, it's not very interesting how to combine with an interactive process We have a low priority job running and it's just using the CPU so the idea is now any new work that comes into the system it's going to come in with a higher priority
这样图片会更清楚 它使用整个时间片 然后它被降级到底部 这就是一个过程的工作，不很有趣 如何与交互式过程结合 我们有一个低优先级的工作正在运行 它只是在使用CPU 所以想法现在是任何新进入系统的工作 它将以更高的优先级进入

51:48
It will preempt or interrupt that work It will use the CPU and find out if the process is interactive or if it will also move to q-zero so if both jobs move to q-zero what happens with rotation scheduling we will rotate between these two, the time slice is very long so we get good throughput for those jobs
它将预emption或中断那个工作 它将使用CPU并找出该过程是否交互式 或者是否也会移动到q零 所以如果两个工作都移动到q零 会发生什么 轮转调度 我们将在这些两个之间轮转调度，时间片很长 所以我们对这些工作得到了良好的吞吐量

52:12
Because it looks like it only cares about this, so let's look at some more examples, so in this example, we have a CPU binding job that is downgraded to q-zero, and then this is supposed to be used by two interactive jobs, taking up only a fraction of their time slice, and then they go to do the I/O operation, which is another job, and behaves the same
因为看起来它只关心这个 所以让我们看一些更多的例子 所以在这个例子中，我们有一个被降级到q零的CPU绑定工作 然后这是应该被两个交互式工作使用的 只占用他们时间片的一小部分 然后他们去执行I/O操作 这是另一个工作，行为相同

52:36
So each one stays at the highest priority and each one runs so the question is this looks like a good idea, who would be upset about this question that was asked before, about hunger So here we obviously work on hunger this low priority because our rules say if you're in a higher queue
所以每个都保持在最高优先级 每个都运行 所以问题是 这看起来像是一个好主意，谁会不高兴 之前有人问过这个问题，关于饥饿的问题 所以这里我们明显在饥饿这个低优先级工作 因为我们的规则说，如果你在一个更高的队列中

53:04
You can always run lower level queues without rotation between queues We managed to rotate between those two, but low-priority work is starving to death And of course, as there are more jobs in the system, it's more likely that low-priority jobs will starve to death, so we need to fix this
你总是能运行过更低级别的队列 没有队列之间的轮转 我们成功地在这些两个之间进行了轮转调度 但是，低优先级的工作被饿死了 当然，随着系统中工作的增加 低优先级的工作被饿死的可能性就越来越大 所以我们需要解决这个问题

53:23
So there are all kinds of ways to solve it, one is that we can solve it like this, it's called starvation, it's the technical term that we use in the operating system, when you don't give any resources to a process, the process is starved to death, so when we want to happen is after this happens to the system
所以有各种各样的方法来解决它一种方法是 我们可以这样解决它 这就是所谓的饥饿 这是我们在操作系统中使用的技术术语 当您不向进程提供任何资源时 该进程就被饿死了 所以当我们想要发生的事情是 在系统发生这种情况后

53:51
After this time, we say, hey, q-zero hasn't been scheduled yet, you know, I don't know if it's like fifty, but all of these times are meaningless, but you're going to have a regular timer, maybe every second, every two seconds, it scans all the work and says hey, which jobs aren't scheduled in this interval if they're not scheduled in this interval
过了这个时间 我们说嘿，q零还没有被调度 你知道 我不知道是不是像五十 但这些时间都毫无意义 但你会有一个定期的定时器 可能每秒 每两秒 它扫描过所有的工作并说嘿 哪些工作在这个间隔内都没有被调度 如果他们在这个间隔内都没有被调度

54:14
The hunger mechanic kicks in, we raise the priority of the process, it gets another try, somebody drew this chart, I borrowed it from it, and I looked at it, and the chart doesn't make any sense at all, so what's wrong with this chart, um, somebody, another person, yes, because of it
饥饿机制就会启动 我们提高该进程的优先级 它又得到了一次尝试的机会 有人绘制了这个图表，我从中借来了 然后我看了看它 而且这个图表一点意义也没有 所以这个图表有什么毛病 嗯 有人 另一个人 是的 因为它

54:48
Oh, so what should this be going on in this The block that is marked as a dark shade has been promoted to this priority level, it's priority is secondary So we polled between these You know I don't like this picture at all right right now but I really like it because it should be placed there
哦，那么这应该在这个里面发生什么 被标记为暗色阴影的块已经被升级到这个优先级水平，它的优先级是二级 所以我们在这些之间进行了轮询 你知道我现在一点也不喜欢这张照片 但我真的很喜欢它 因为它应该被安排在那里

55:10
Well, this one is after every one of those gets a time slice, so it doesn't make sense, so that's one of its problems, and then what happens if this one runs here, it should be downgraded to q1, so when it runs out of the whole time slice, it should move here, and then when it uses up the whole time slice
嗯 这个在每个那些都得到了时间片之后 所以这不有意义 所以这是它其中一个问题 然后如果这个在这里跑了会发生什么 它应该被降级为q1 所以当它耗尽了整个时间片后 它应该移动到这里 然后当它使用满整个时间片后

55:33
Because it's a CPU-bound task and then it's going to move to qzero and then maybe it's not scheduled there I mean it's not going to be scheduled there with those lower priority wells I guess that's what he's showing okay so there's no scheduling and it has to start the hunger mechanism to boost it at that time
因为它是CPU绑定的任务 然后它将移动到q零 然后可能它不会那里被调度 我意思是它不会在那些更低优先级的那里被调度 嗯 我想这就是他在显示的 好的 所以没有安排 并且它不得不启动饥饿机制来提升它 在那个时候

55:50
Too good so I think the only thing I don't like is who knows okay maybe the picture isn't that bad So the only reason it was scheduled was because the hunger mechanic promoted it here so we didn't show it being relegated to q one after the run but it was never scheduled there
太好了 所以我认为唯一我不喜欢的是，谁知道 好的 也许图片并不那么坏 所以它之所以能被安排，唯一的原因 是因为饥饿机制把它提升到这里 所以我们没有在运行后展示它被降级到q one 但是，它从未在那里被安排

56:10
Then the hunger mechanism has to raise it back to q2 and make it run the same as before if it uses up the entire time slice then we see that this is not the right clue to do this so we downgrade it to q1 but it simply won't be scheduled and that's why it doesn't show up in the graph
然后，饥饿机制必须提高它 回到q2并使它运行 与以前相同 如果它耗尽了整个时间片 那么我们看到这不是完成这项工作的正确线索 所以我们把它降级到q1 但是它 simply不会被安排 这就是为什么它在图中不显示

56:42
And then, the starvation mechanism kicks in after a few seconds and then it's boosted to Q2 again You can come up with whatever policy you want, and that's the thing about the policy, you can come up with something that is more effective for one workload and slightly worse for another workload So these are usually like configurable parameters
然后，饥饿机制在几秒钟后启动 然后它会再次被提升到q2 你可以想出任何你想要的政策 这就是关于政策的事情 你可以想出一种对于一种工作负载更有效，对于另一种工作负载稍微差的东西 所以这些通常就像可配置的参数

57:05
It's always changing like how much should you boost yes should you boost it all to the top you should boost it to some middle level That's the policy of dancing you can run some simulations and figure out what you can get with the best throughput It's different for everyone yes
它总是在变化 比如你应该提升多少 是的 你应该提升它吗 全部提升到顶部 你应该提升它到某个中间水平 这就是手舞足蹈的政策 你可以运行一些模拟并找出你以最佳吞吐量可以获得什么 对于每个人来说都是不同的 是的

57:24
More questions yes so if you're posting your low priority work, don't let the advantage of being able to run for a long time that's what the priority level is all about, at the lowest priority, yes, I mean, if you're in run mode, at a time when you have a lot of hungry work, your system is just overutilizing
更多的问题 是的 所以如果你正在发布你的低优先级工作 不要让失去能够长时间运行的优势 这是优先级级别的全部意义 在最低优先级 是的 我的意思是 如果你在运行模式 在你有很多饥饿的工作的时候 你的系统只是在过度利用

57:43
There's too much load on that system, and it's not going to perform well, but you're right, because we hope it's just a small burst that you're not scheduled and we hope that the load will go away, the system will react, and eventually those other jobs will disappear, and then this work can go back to where it belongs, yes, how to elevate the priority
那个系统上有太多的负载 而且它不会表现得很好 但你是对的因为我们希望这只是一个小爆发 你没有被安排 我们希望那个负载会消失，系统会反应 最终那些其他工作会消失 然后这个工作可以回到它属于的地方 是的 如何提升优先级

58:13
It's going to just be a separate mechanism You might have a timer and when the scheduler sees it say, hey, I'm going to see if anyone is hungry, if it sees there's a job hunger, it just needs to increase its priority, and then the natural scheduling mechanism will see that it's a high priority job, and it's going to be scheduled
它将只是一个单独的机制 你可能有一个定时器，当调度器看到它时 说嘿 我要看看是否有任何人饥饿 如果它看到有一个工作饥饿 它只需要提高其优先级 然后自然的调度机制 我们将看到这是一个高优先级的工作 它会被安排

58:34
So it's easy to implement just need to have one thing to find the work that hasn't been scheduled and then if they haven't been scheduled, raise its priority and it will be different in different systems Of course, the administrator can change how all of this is done Oh well yes so there's always a concept of static prioritization
所以很容易实现 只需要有一个东西来查找尚未安排的工作 然后如果它们尚未安排，提高其优先级 这将是 在不同的系统中可能会有所不同 当然，管理员可以改变所有这些是如何做的 哦 嗯 是的 所以总是有一种静态优先级的概念

59:05
Likewise, for example, for the good you can add priorities to things and then that gives you a boost in addition to these other things that are going on yes but how to combine static and dynamic is really a difficult thing yes it will cut evenly on all priority levels and then cut longer sections on different threads
同样 比如对于美好的 你可以为事物添加优先级 然后这就给你带来了提升 除了这些正在发生的其他事情之外 是的 但是，如何结合静态和动态确实是一个难题 是的 没错 是的 它将在所有优先级级别上均匀切割 然后在不同的线索上切割更长的部分

59:33
yes okay okay that's great so another problem that you may have noticed besides hunger you can now play the scheduler So, malicious process a very smart process that knows the exact length of the time slice what you can do when you have information you can say okay I'm going to do a little bit
是的 好的 好的 这太棒了 所以你可能已经注意到的另一个问题 除了饥饿之外 你现在可以游戏调度器 所以，恶意进程 一个非常聪明的进程 它知道时间片的确切长度 当你有信息时，你可以做什么 你可以说 好的 我要做一点点

59:56
I you know sleep you know nanoseconds and free up the CPU before my time slice expires so I won't be downgraded I'll keep it on high priority when you're not running the system can schedule other tasks and then when you wake up you still have high priority So, it's interesting to think about how malicious processes can play your scheduler
我 你知道 睡眠 你知道 纳秒，并将CPU释放 在我时间片到期之前 所以我不会被降级 我会一直保持在高优先级 当你不运行时 系统可以安排其他任务 然后当你醒来时 你仍然有高优先级 所以，思考如何恶意进程可以游戏你的调度器是很有趣的

1:00:23
Whatever algorithm you propose, there may be a way to get it, but the solution to this problem is not bad, so we can't just focus on the time you're using in the current time slice To fix this, you need to look at your total runtime on this priority What you need to fix is that you need to look at your total runtime on that priority
无论你提出什么算法 可能有一种方法可以获取它 但这个问题的解决方案并不坏 所以我们不能只关注你在当前时间片中使用的时间 要修复这个问题，你需要看看你在这个优先级上的总运行时间 你需要修复的是，你需要看看你在这个优先级上的总运行时间

1:00:38
That's what you need to look at, your total runtime on this priority so even if you're sleeping here when we come back and start running we're going to see that as they ran even though it's a different launch and we're going to downgrade them at that point so we're going to look at the total runtime that you get in this scheduling interval
这就是你需要看的，你在这个优先级上的总运行时间 所以即使你在这里睡觉 当我们回来开始跑步时 我们将把这也视为他们跑了 尽管它是一次不同的发射 到那时我们将降级他们 所以我们将看看你在这个调度间隔中获取的总运行时间

1:00:58
To determine if you're over that amount of time and downgrade you so it's just your policies and the little things and the small changes that you're doing and how the way you account ends up having a big impact on the process through all these things okay that's how modern systems work and they might do their rules work a little differently
以确定你是否超过了这个时间量并降级你 所以只有你的政策和小事和你在做的微小变化 以及会计方式如何最终对过程通过产生重大影响 所有这些事情 好的 好的 好的 这就是现代系统的工作方式 他们可能会以稍微不同的方式做他们的规则工作

1:01:31
But they will have multiple levels They will have some rules to move work and how to set time slices depending on where you are there so there so there there are other schedulers so we are thinking of doing something like a universal scheduler on your desktop on Linux but if you are a cloud provider you want to sell some resources in exchange for some money
但他们将有多个级别 他们将有一些规则来移动工作 以及如何根据您在那里的位置设置时间片 所以有其他调度器 所以我们正在考虑像通用调度器一样 在Linux上您的桌面机上做的事情 但如果你是云提供商，你想要出售一些资源以换取一些钱

1:01:56
So what is usually going to be done is you better just give a fixed resource like you give one user and then give another user a fixed resource or you want to give a proportional share of the user who pays twice as much as they should get twice the CPU time of the other user a proportional share scheduler, very clever and simple
那么通常将会做的事情是 你最好只是像给一个用户一样提供固定的资源 然后给另一个用户提供固定的资源 或者你想要提供比例份额 支付他们两倍费用的用户 他们应该得到其他用户的两倍CPU时间 一种比例份额调度器，非常聪明且简单

1:02:19
Known as a lottery scheduler the idea here is that you give the process some lottery tickets if you are a higher priority job you just get more lottery tickets We will hold lotteries regularly Users who have winning tickets are get scheduled jobs and you don't have to worry about their outbursts or anything about them
被称为彩票调度器 这里的想法是您给过程 一些彩票票 如果你是一个优先级更高的工作 你只是得到更多的彩票票 我们将定期举行彩票 拥有获胜彩票的用户是得到安排的工作 你不必担心他们的爆发或任何关于他们的事情

1:02:42
You just give them the lottery ticket and then schedule the winner The code to do this is very straightforward Um, we hold the lottery, which is just a random number between 0 and the total number of tickets, and then we have some simple data structure, maybe sorted, we better sort, you can organize it into a tree, do whatever you want with your working list data structure
你只给他们彩票 然后安排获胜者 做这件事的代码非常直接 嗯 我们举行彩票 这只是在0到总彩票数之间的随机数字 然后我们有一些简单的数据结构，可能是排序的 我们最好排序 你可以把它组织成一个树 做你想做的任何事情与你的工作列表数据结构

1:03:07
Well, then we see who has the winning ticket for example if we draw the lottery number fifty we will look at the person who holds the ticket number fifty this holds the ticket number zero and then a one we just keep incrementing to see where the fifty lands and it will be the work c which is the winner of this game so that's our policy to determine the winning process
嗯，然后我们看到谁有获胜彩票 例如 如果我们拉了彩票号码五十 我们将查看持有票号五十的人 这持有票号零 然后一个我们只是不断递增以查看五十落在何处 并且这将是工作c 这是这次比赛的赢家 所以这就是我们确定获胜过程的政策

1:03:29
And then we still have the same scheduling mechanism as we did before Actually, and then schedule work at the end of this time slice so it's going to still be a time slice rotation type of thing We just want to figure out who should be the winner so if it's a high priority job it has more votes it wins more times
然后我们仍然有与我们之前相同的调度机制 实际上，然后在这个时间片结束时安排工作c 所以它将仍然是一种时间片轮转类型的东西 我们只是想找出应该成为赢家的人 所以如果它是一项高优先级的工作 它拥有更多的票 它赢得的次数更多

1:03:48
It's scheduled more times it gets more of these time slices so it's kind of interesting if we have you know different tickets you can figure out which is the job that's going to run so you might think it sounds really simple and silly But the reason people love it is because it's hard to play the scheduler
它被安排的次数更多 它获得更多的这些时间片 所以这有点有趣 嗯 如果我们有 你知道不同的票 你可以找出即将运行的工作是哪个 所以你可能会认为这听起来真的很简单和愚蠢 但是人们喜欢它的原因是因为它很难游戏调度器

1:04:11
You can't come up with any clever way to get more votes or be scheduled more These tickets allow you to shift priorities from one job to another very gracefully Mainly because it's really easy to implement um so there's a lot of research on operating systems and they'll try um change the structure of the operating system and give some responsibility
你不能想出任何聪明的方法来获得更多的票或被安排得更多 这些票允许你非常优雅地将优先级从一个工作转移到另一个工作 主要是因为它真的很容易实现 嗯 所以有很多关于操作系统的研究，他们会尝试 嗯 改变操作系统的结构并赋予一些责任

1:04:34
Maybe to the user level service so they'll eventually implement a lottery-based scheduler so if you do some research on the operating system you'll come across these lottery schedulers a lot but some people don't like the randomness It's just a random choice of luck Some jobs may be scheduled more so you can do a definitive version
也许到用户级别服务 所以他们最终会实现基于彩票的调度器 所以如果你做一些关于操作系统的研究 你会经常遇到这些彩票调度器 但是有些人不喜欢它随机性 这只是运气的随机选择 一些工作可能会被安排得更多 所以你可以做一个确定的版本

1:04:56
Sometimes called a step scheduler, you still do rotations, but you just make sure that the jobs with more votes are scheduled at a precise frequency proportional to the number of votes they have relative to other people, and you just figure out how long they should be scheduled and schedule them, instead of doing all these random things any problem
有时被称为步长调度器 你仍然做轮转 但你只是确保拥有更多票的工作被安排在精确的频率 与他们相对于其他人的票数成正比 你只是计算出他们应该被安排在多久 并安排他们，而不是做所有这些随机的事情 有任何问题吗

1:05:24
yes, that should be the number of votes they have, this is the number of votes they have, so a is not a very important job, d is the most important, so you know the matter of luck, it should be like this, work d is scheduled in two hundred and four hundredths of a time, yes, yes, you don't know how big the data is
是的 这应该是他们拥有的票数 这是他们拥有的票数 所以a不是一个非常重要的工作 d是最重要的 所以由你知道 运气问题 应该是这样的 工作d被安排在四百零二分之二百次的时间里 是的 是的 你不知道数据有多大

1:05:55
And that's what we're pushing, always like this, how do you decide anything, so it's going to be based on the importance of the job, so it's going to be to the people who pay you the most you're going to give them the most votes You don't care if they're using their tickets effectively You don't care what they're doing, you're just paying you a lot of money
这就是我们正在推动的问题 总是像这样 你怎么决定任何事情 所以这将基于工作的重要性 所以将给支付你最多的人 你将给他们最多的票 你不在乎他们是否有效地使用他们的票 你不在乎他们在做什么，你只是 他们付给你很多钱

1:06:12
They're scheduled for more time yes yes multi-level feedback queues yes so the reason we're doing rotations right now is because we just want to be fair to those two jobs yes So, rotations have a lot of different advantages for different types of workloads Well that's true here even though you're giving all the processes that are at the highest priority a try, you're giving them a chance to showcase
他们被安排在更多的时间里 是的 是的 多级反馈队列 是的 所以 我们目前做轮转的原因 是因为我们只是想公平地对待那两个工作 是的 所以，轮转有许多不同的优势，适用于不同类型的工作负载 嗯 在这里是真的 尽管你正在给予处于最高优先级的所有过程一个尝试，你在给它们一个展示的机会

1:06:58
Is it long or short when it shows up to be long it will eventually be moved down but the short task still has a chance to run So, the carousel is a very fair way to give everyone a chance So, through this you may not like it We certainly won't know before but once it runs and uses it
它是长还是短 当它显示出来是长的时候 它最终会被移动到下面 但短任务仍然有机会运行 所以，轮转是一种非常公平的方式，给每个人都一个机会 所以，通过 这个 你可能不喜欢 我们当然不会知道在此之前 但是一旦它运行并使用了它

1:07:25
And then it shows us what it does, and we assume what it's going to do in the future yes so, it runs and does some things and then we make all the decisions based on what it actually does so it's very, very practical and works very well in practice Any questions about the multi-level feedback queue scheduler
然后它就向我们展示了它做了什么，并且我们假设它将在未来做什么 是的 所以，它运行并做了一些事情 然后我们基于它实际上做了什么来做出所有决定 所以它是非常 非常实用的 在实践中工作得很好 还有任何关于多级反馈队列调度器的问题吗

1:07:41
Okay, so I'll wrap it up and then let's wrap up the discussion about multi-level feedback queue schedulers Okay, so I'm done with that, so what we're seeing today is that there's no perfect scheduler, it really depends on your workload or your mix of short and long tasks and the metrics that you care about
好的，那我来总结一下 然后让我们结束关于多级反馈队列调度器的讨论 好的 那么，我就结束了 所以今天我们看到的是，没有完美的调度器 它确实取决于你的工作负载 或者是你短任务和长任务的混合 以及你关心的度量

1:07:59
We really only thought about turnaround time and response time but if fairness is important to you need a different scheduler If we developed this multi-level feedback queue scheduler, it works very well In many cases past behavior is a good predictor Wait another minute Let's make sure all of you remember the deadline for this project
我们实际上只考虑了周转时间和响应时间 但如果公平对你来说很重要 你需要一个不同的调度器 如果我们开发出了这个多级反馈队列调度器，它工作得很好 在许多情况下 过去的行为是一个好的预测者 再等一分钟 让我们确保你们所有人都记住这个项目的截止日期

1:08:18
It's Monday night, and that's before I see you again, so when I see you on Tuesday, I'll be very happy that Project 2 has been submitted and is available for viewing, please check it out as soon as possible, and this simple assignment, which is due in a week, so if you have any questions about that, let me know, see you next week
是周一晚上 那是我再见到你们之前 所以当我在周二见到你们 我会非常高兴 项目二已经提交，可供查看 请尽快查看 还有这简单的作业，一周后截止 所以如果你有任何关于那个的问题 让我知道 下周见
