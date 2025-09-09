00:02
Art & High Performance Software Professional Lab Consulting Training Talent Acquisition & Development Welcome to Module 8 Who Programs Let's start lesson 8 One OS Scheduling Mechanism But we're about to start talking about multithreaded software I always like to start with OS mechanics because they really give us a good understanding and background
艺术和高性能软件专业实验室 咨询 培训 人才招聘和开发 欢迎来到第八模块谁程序 让我们开始第八课 一操作系统调度机制 但我们即将开始讨论多线程软件 我总是喜欢从操作系统机制开始 因为它们确实给我们提供了一个很好的理解和背景

00:26
About how all this multithreaded software is going to work, and even going to the operating system that sits on one layer above the operating system and we need to define some terms on the road like what does concurrency actually mean what parallelism actually means what parallelism actually means concurrency we can start from now on which this means out of order execution
关于所有这些多线程软件将如何工作，甚至和去 它坐在一个层以上操作系统 并且我们需要定义一些术语 在路上 像并发实际上意味着什么 什么是平行的平行主义实际上意味着什么 并发我们可以从现在开始这意味着无序执行

00:48
That's the only thing I want you to keep in your head We have a sequence of instructions we're looking for execution from start to end but we're going to execute them sequentially and still execute them all and hope for the same result So we always have to think about out-of-order execution When it comes to concurrency parallelism, which means we're executing two or more instructions at the same time
那就是我想让你在你的头脑中保持的唯一东西 我们有一个指令序列 我们正在寻找从开始到结束执行 但我们将按顺序执行它们 仍然执行它们全部并希望得到相同的结果 所以我们总是要考虑无序执行 当谈到并发时 并行主义这意味着我们同时执行两个或多个指令

01:14
It's about doing a lot of work at the same time, and it's interesting that sometimes these terms blend in with each other, sometimes they're just opposites, and we'll figure it out when we go on and talk about the operating system and then go to the scheduling mechanism Let's focus on the operating system that we need to know Let's say I'm asking you to write an operating system scheduler
这是关于同时做很多工作 有趣的是 有时这些术语相互融合 有时它们只是相对的对立面 我们会弄清楚当我们继续谈论操作系统 然后去调度机制时 让我们专注于我们需要了解的操作系统 假设我正在问你编写操作系统调度程序

01:40
The thing you need to think about, if you're going to do that kind of engineering, and here's an idea that we need to really cement ourselves, is that we want to create an illusion where a lot of work happens on the same machine, in other words, we should be able to run multiple programs running multiple applications at the same time and create the illusion that they are running at the same time
你需要考虑的事情 如果你要做那种工程 并且这里有一个想法我们需要真正巩固自己 是我们想要创造一个幻觉 许多工作在同一台机器上发生 换句话说 我们应该能够运行多个程序 同时运行多个应用程序 并创造它们同时运行的幻觉

02:06
Actually they can't do that, it all depends on the hardware we have, and we can create some imaginary hardware for this one as we learn our mental model, so let's start with a very simple piece of hardware where we only have one processor and this processor has a single hardware thread
实际上它们不能做到这一点 这完全取决于我们有的硬件 并且我们可以为这个创建一些想象中的硬件 当我们学习我们的心理模型时 所以让我们从一个非常简单的硬件开始 我们只有一个处理器 并且这个处理器有一个单一的硬件线程

02:28
And let's represent this hardware thread as the ability to execute instructions, so every hardware thread in our machine gives us the ability to execute instructions, if I only have one hardware thread, then I can only execute one instruction at any time, if I have two hardware threads, then I can execute instructions in parallel, you get it now
并且让我们将这个硬件线程表示为执行指令的能力 因此，我们机器中的每个硬件线程都给我们执行指令的能力 如果我只有一个硬件线程 那么我任何时候只能执行一条指令 如果我有两个硬件线程 那么我可以并行执行指令 你现在明白了吧

02:52
My machine hat is an eight-threaded hardware machine, so in theory I can execute eight instructions in parallel at any time, but now let's assume that our hardware is single-threaded hardware, which is at the hardware level and we have to take advantage of this in the operating system scheduler, so what we are going to do is we are going to define the concept of operating system threads
我的机器帽子是一个八线程硬件机器 因此，理论上我任何时候可以并行执行八条指令 但现在让我们假设我们的硬件是单线程硬件 这是在硬件层面上 我们在操作系统调度器中必须利用这一点 所以我们要做的是 我们将定义操作系统线程的概念

03:14
If there are hardware threads we will represent the concept of operating system threads Our threads I always want to make us think that threads are the path to execution Our program will be a series of instructions that are arranged in order to execute The task of executing those instructions is our thread Our operating system threads now they will execute those instructions in order
如果有硬件线程 我们将表示操作系统线程的概念 我们的线程 我总是想让我们想到线程是执行的路径 我们的程序将是一系列指令 这些指令按顺序排列以执行 执行那些指令的任务是我们的线程 我们的操作系统线程现在 它们将按顺序执行那些指令

03:40
One instruction at a time to do the bill and utilize the hardware threads to do it The operating system will execute those instructions in sequence Utilizing the hardware threads that are actually executed When we think about these operating system threads we will have three states, and the operating system thread can be in it There are actually a lot of more substates but we don't need to fully understand the implementation details
一次一条指令 做账 并利用硬件线程来完成 操作系统将按顺序执行那些指令 利用实际执行的硬件线程 当我们考虑这些操作系统线程时 我们将有三种状态，操作系统线程可以处于其中 实际上有很多更多的子状态 但我们不需要完全理解实现细节

04:10
What we need is to have a good mental model of how things work and behave that will help us make better engineering decisions, so, a thread can have three states A thread can be in a running state When a thread is running it means that we've placed it on this hardware thread and it's executing the instructions it's responsible for
我们需要的是对事物如何工作和行为有一个良好的心理模型 这将帮助我们做出更好的工程决策 所以，线程可以有三种状态 线程可以处于运行状态 当线程处于运行状态时 这意味着我们已经将其放置在这个硬件线程上 它正在执行它负责的指令

04:32
A thread can be in a runnable state When it's in a runnable state that means it wants that hardware thread for a long time it just has to wait for its turn The thread can be in a waiting state When a thread is in a waiting state, we actually think it's off the radar, it's gone, it's waiting for something to happen
线程可以处于可运行状态 当它处于可运行状态时 这意味着它想要那个硬件线程的时间 它只需要等待它的轮次 线程可以处于等待状态 当线程处于等待状态时 我们实际上认为它已经离开了雷达 它不见了 它正在等待某事发生

04:52
It may be waiting for the operating system to return a system call It may be waiting for the data on the network to return It is in a waiting state From our dispatcher's point of view we only care about the threads that are running or about to run Correct threads that are waiting do not burden us in any way They are not our concern
它可能在等待操作系统返回系统调用 可能在等待网络上的数据返回 它处于等待状态 从我们的调度员角度来看 我们只关心正在运行或即将运行的线程 正确 正在等待的线程 不会给我们带来任何负担 它们不是我们的关注点

05:13
So imagine a scenario where we have several programs running, which means there are several threads running, and our idea is to create the illusion that even if there's only one hardware thread, all of our threads, whether they're running or ready, are actually running at the same time, so how does our scheduler create that illusion
所以想象一下以下情景 我们有几个正在运行的程序 这意味着有几个线程正在运行 我们的想法是创造这种假象 即使只有一个硬件线程 我们所有的线程 无论是运行状态还是就绪状态，实际上都是在同一时间运行的 那么我们的调度器是如何创造这种假象的呢

05:39
One idea is that we can define a so-called scheduler cycle, let's define our scheduler cycle, and now the scheduler cycle, and its job is that we can execute any thread that is ready at the beginning of the cycle, so that this thread can execute in this time, and if we can do that
一种想法是我们可以定义一个所谓的调度器周期 让我们定义我们的调度器周期 现在调度器周期 它的职责是我们能够执行任何在周期开始时处于就绪状态的线程 使这个线程在这个时间内执行 使这个线程在这个时间内执行 如果我们能做到这一点

06:03
So we can create illusions At least within the scope of the scheduler, we can create illusions where everything is going on at the same time We can play with some interesting numbers You know we can play with some interesting numbers here I'll give you some specific numbers Other numbers We need to take a closer look at our operating system scheduler to understand what they are
那么我们可以创造出幻觉 至少在调度器的范围内，我们可以创造出所有事情同时进行的幻觉 我们可以玩一些有趣的数字 你知道的 我们可以在这里玩一些有趣的数字 我会给你一些具体的数字 其他数字 我们需要仔细研究我们的操作系统调度器来了解它们是什么

06:21
But we can use some base numbers to get an idea that let's say right now, our scheduling cycle will be 100 milliseconds, let's say we're going to use this, our scheduling cycle will be 100 milliseconds, so the idea is that we want to make sure that all of our threads are up and running
但我们可以使用一些基础数字来获得一个想法 让我们现在就说，我们的调度周期将是 让我们就说是100毫秒 让我们就说我们将使用这个 我们的调度周期将是100毫秒 所以想法是 我们希望确保我们所有的线程处于可运行状态

06:40
Executing in this 100 millisecond timeframe creates the illusion that everything is running at the same time, so let's start our scheduling, but we do this at the beginning of the scheduling cycle and we find that only one thread is running, and that's all our threads, if we only have one thread running
在这个100毫秒的时间框架内执行 创造出一切都在同一时间运行的错觉 所以让我们开始我们的调度 但我们这样做 在调度周期开始时 我们发现只有一个线程处于可运行状态 这就是我们所有的线程 如果我们只有一个线程处于可运行状态

07:03
And our hardware only has this single hardware thread Remember, at any given moment, there is only one physical thread that can execute Well, we call this thread Thread A Thread A will get a full 100 milliseconds to execute its instructions It will get a full 100 milliseconds It's excellent has a lot of time to do the job and remember some of the numbers that we're talking about
而我们的硬件只有这个单一的硬件线程 记住，任何给定时刻，只有一条物理线程可以执行 那么，我们将这条线程称为线程A 线程A 将获得完整的100毫秒时间来执行其指令 它将获得完整的100毫秒 它很出色 有大量的时间来做作业并记住我们讨论的一些数字

07:29
Well, early in the video, we say time per nanosecond, remember right, time per nanosecond, one nanosecond is equal to twelve instructions, and I want you to remember this number, one nanosecond is for those twelve instructions, okay, great, so we're going to leave that number in our heads as we continue with this exercise
嗯 在视频中的早期 我们说每一纳秒的时间 记得对吧 每一纳秒的时间 一纳秒的时间等于十二条指令 我希望你记住这个数字 一纳秒代表那十二条指令 好的，太好了 所以我们要把这个数字留在我们的头脑中 随着我们继续进行这个练习

07:56
Now we have a go routine that is in a runnable state before the scheduling cycle starts Now it's doing its work Now the scheduling cycle is complete Once the scheduling cycle is complete we go back and see how many threads are in the runnable state Let's say we have two threads in the runnable state now
现在我们有了一个go例程 在调度周期开始之前，它处于可运行状态 现在，它在进行它的工作 现在调度周期已经完成 一旦调度周期完成 我们回去看看有多少线程处于可运行状态 假设现在我们有两个线程处于可运行状态

08:16
So what does that mean, well, it means that now we're going to schedule to have our two threads execute in the same hundred-millisecond scheduling cycle, so we decide to run thread A again, but we know that this time thread A will only get 50 milliseconds, which means we're going to schedule the other thread B to run, and thread B will only get 50 milliseconds
那么这意味着什么 嗯 这意味着 现在我们将要安排 让我们的两个线程在同一百毫秒调度周期内执行 所以我们决定再次运行线程a 但我们知道这次线程a只能得到50毫秒 这意味着我们将安排其他线程线程b运行 而线程b也只会得到50毫秒

08:42
So let's look at what happened just now, we created the illusion that two threads were running within our scheduling cycle, but if we started looking at what happened to our thread, the first time it got 100 milliseconds of runtime, but now it's cut in half, and in the next 100 milliseconds its throughput is cut in half
所以让我们看看刚才发生了什么 我们创造了一种错觉，即两个线程在我们的调度周期内运行 但如果我们开始看我们的线程发生了什么 第一次它获得了100毫秒的运行时间 但现在它被切成了一半 在接下来的100毫秒内它的吞吐量被切成了一半

09:03
We didn't execute as many instructions that we ran earlier OK OK continue scheduling The cycle is over We look again What we found We found that now we have five threads, now they're ready to run in a runnable state which means we have to reduce this again Okay, what will thread A get this time
我们没有执行我们之前运行那么多的指令 好的 没问题 继续调度 周期结束了 我们再次查看 我们发现了什么 我们发现 现在我们有五个线程，现在它们已经准备好运行在可运行状态 这意味着我们必须再次减少这个 好的，这次线程A将得到什么

09:31
Thread A will only get what this time it will only get 20 milliseconds So now thread A will get 20 milliseconds Now we know that thread B will get 20 milliseconds of it Twenty milliseconds to thread B and then we will see how to utilize the remaining sixty milliseconds here The remaining sixty milliseconds will now go through the other threads
线程A将只获得什么 这次它只能得到20毫秒 所以现在线程A将得到20毫秒 现在我们知道线程B将得到它的20毫秒 二十毫秒给线程b 然后我们将如何利用剩下的六十毫秒在这里 剩下的六十毫秒现在将遍历其他线程

09:55
cd and e that will be the rest of that sixty milliseconds of time, and I want you to notice again that every time more threads appear in the scheduler cycle, the time starts to get smaller and smaller, and if eventually we have a hundred threads that want to run in this scheduler cycle, we have a hundred threads, and we're now at this point in this thread
cd和e 这将是那六十毫秒时间的剩余部分 我再次想要你注意 每次有更多的线程出现在调度器周期内 时间开始变得越来越小 如果最终我们有一百个线程想在这个调度器周期内运行 我们有一百个线程 我们现在已经到了这个线程这里的这个点

10:22
Thread A is going to drop to millisecond run time, which means that at some point, the return in time may diminish, and a given thread can really do anything, and mainly because there's a cost here that I haven't touched, and that's the cost of context switching right now
线程a将要下降到毫秒级的时间 一毫秒的运行时间 那就是意味着 在某个时刻，时间上的回报可能会递减 一个给定的线程确实可以做任何工作 而且主要是因为这里有一个我没有触及到的成本 那就是上下文切换的成本 现在

10:50
Think about this one second we have thread A and thread A come in and say okay I want time on this hardware thread so we're going to put it on the hardware thread here and it works in those 100 milliseconds Now we decide okay now thread B and thread B is going to run Let's say, a thousand milliseconds
考虑这一点 一秒钟 我们有线程a和线程a进来说 好的 我想要在这个硬件线程上的时间 所以我们在这里把它放在硬件线程上 它在那100毫秒内工作 现在我们决定 好的 现在线程b 线程b将要运行 让我们说，一千毫秒

11:12
We have to take a moment to unplug this thread from the hardware and then we have to put this thread on the hardware I mean, it's not free and it's going to take some time and that's what we call context switching Take it out of one thread Now put another thread on top of it, on average, on average, at the operating system level
我们必须花点时间来从硬件上拔掉这个线程 然后我们必须将这个线程放在硬件上 我的意思是，这不是免费的 这将花费一些时间 这就是我们所说的上下文切换 从一个线程中取出 现在将另一个线程放在上面 平均而言，平均而言，在操作系统级别上

11:35
Context switching like this would go from one thousand milliseconds to two thousand milliseconds, in other words, a thousand nanoseconds to two thousand nanoseconds, so let's start doing the math again, remember, nanoseconds represent twelve instructions, so what do we see here when we talk about a thousand to two thousand milliseconds context switching that we're talking about here
像这样的上下文切换将会 从一千毫秒到两千毫秒 换句话说 一千纳秒到两千纳秒 让我们再次开始做数学 记住，纳秒的时间代表十二条指令 那么我们在这里看到什么 当我们谈论一个一千到两千毫秒的上下文切换时 我们在这里谈论的

12:05
It's actually twelve to twenty-four thousand lost instructions losing the right instructions, otherwise we wouldn't be able to execute but we can't because of context switching, so think about where we are now if you have these threads context switching in a millisecond or worse if that increases to a thousand threads Oh my God
实际上是一万二千到两万四千 损失 指令损失 正确的指令，否则我们将无法执行 但由于上下文切换，我们不能 所以想想我们现在在哪里 如果你有这些线程在一个毫秒内上下文切换 甚至更糟 如果这增加到一千个线程 哦，我的天啊

12:34
Now we're talking about microseconds to the time of microseconds the time a thread does plus one or two microseconds of context switching and what ends up being that you do more context switching work than you actually do, which is not a good thing, so there's a marginal benefit point where you get to a point in that time slice, and the number of threads, you do more context
现在谈论的是微秒 对 微秒的时间 一个线程执行的时间 加上一到两微秒的上下文切换 最终发生的事情是你做的上下文切换工作比你的实际工作要多 这不是好事 所以有一个边际效益点 在那个时间片到达一个点， 和线程的数量，你做的更多上下文

13:07
Work instead of actual work We don't get any throughput from the machine or the application So what do we do because if we just stick to the 100 millisecond scheduler cycle and if we end up with 500 to 1000 threads that need to be scheduled, we say it's not going to work, and that's a huge loss
工作而不是实际工作 我们不会从机器或应用程序中获得任何吞吐量 那么我们该怎么办 因为我们如果只坚持使用100毫秒的调度器周期 如果我们最终得到500到1000个线程需要调度 我们就说了这不会起作用 这是一个巨大的损失

13:27
So we have to define another parameter in the scheduler, we're going to define the minimum time slice, in other words, which is the minimum time slice that allows any thread to get at least some runtime, regardless of our scheduler cycle, maybe we'll say 10 milliseconds is the marginal benefit point, and we'll never go below a 10 millisecond time slice
所以我们在调度器中必须定义另一个参数 我们将定义最小时间片 换句话说 这是允许任何线程至少获得一些运行时间的最小时间片，无论我们的调度器周期 也许我们会说10毫秒 是边际效益点 我们永远不会低于10毫秒的时间片

13:48
Because when we're below 10 millisecond time slices, our context switching is actually causing us performance problems, like we discussed, but this is getting interesting now, because if we think about a minimal 10 millisecond time slice, remembering that we only have 100 threads here, now we will never go below 10 milliseconds
因为当我们低于10毫秒的时间片 我们的上下文切换实际上正在造成我们的性能问题 就像我们讨论的那样 但这现在变得有趣了 因为如果我们考虑一个最小的10毫秒时间片 记住我们在这里只有100个线程 现在我们永远不会低于10毫秒

14:11
That means that our scheduler cycle will no longer be 10 milliseconds for 100 threads, right, it will be like 10 seconds, so think about this, even if we have this to give us a reasonable timeframe cycle to create illusions, once we have those 100 threads, or even worse
这意味着我们的调度器周期不再会是10毫秒 对于100个线程，对吗 它将是像10秒 所以想想这一点 即使我们有了这个给我们一个合理的 合理的时间创建幻觉的调度器周期 一旦我们有了这些100个线程 甚至更糟

14:32
Even if we have this scheduler cycle that gives us a reasonable amount of time to create illusions, once we have these 100 threads with a minimum time slice of 10 milliseconds, now we start to realize that our scheduling cycle is in seconds, like 10 seconds to create this illusion, which doesn't necessarily work for us
即使我们有了这个给我们一个合理的 合理的时间创建幻觉的调度器周期 一旦我们有了这些100个线程 以10毫秒的最小时间片 现在我们开始意识到我们的调度周期在秒级 比如10秒来创造这种幻觉，这不一定适合我们

14:54
Now we're also starting to feel some throughput issues, because any given thread may have to wait a total of 10 seconds before it can even run again, okay, you can see how complicated that is, so in this world, it's always about less, more less is more The fewer threads we schedule means more time per thread in a given scheduling cycle
现在我们也会开始感受到一些吞吐量问题 因为任何给定的线程可能需要等待总共10秒才 甚至才能再次运行 好的 你可以看到这有多复杂 所以在这个世界里，总是关于更少，更多 更少即是更多 我们调度的线程越少 在给定的调度周期内意味着每个线程将获得更多时间

15:23
And that thread will be able to get back into operation faster, so we always need to balance this idea with this idea in terms of the operating system, and now another concept that we have to understand, if you're going to be a multithreaded software developer, that's workloads, and we have to be able to identify both workloads early
并且那个线程将能够更快地重新进入运行 所以我们总是需要平衡这个想法 操作系统方面的这个想法 现在我们必须理解的另一个概念 如果你要成为一名多线程软件开发者 那就是工作负载 并且我们必须能够早期识别两种工作负载

15:48
If we are going to make smart engineering decisions here in the scheduler The first workload type is called CPU bound Now a CPU-bound workload is a workload where the thread naturally does not go into a wait state It never goes into a wait state So an example of a CPU-bound workload is an algorithm
如果我们要在调度器这里做出明智的工程决策 第一种工作负载类型被称为CPU绑定 现在 CPU绑定的工作负载是一种工作负载 其中线程自然不会进入等待状态 它永远不会进入等待状态 因此，CPU绑定的工作负载的一个例子是一个算法

16:11
It's going to compute integers Imagine I gave you a list of a million integers and I said, hey, compute those integers from start to finish There's nothing in the process of adding processing that causes the thread to naturally pause or wait for anything This is a CPU-bound workload that means
它将计算整数 想象一下，我给了你一份包含100万整数的列表 然后我说，嘿 从开始到结束计算这些整数 在添加处理过程中没有任何东西 会导致线程自然暂停或等待任何事情 这是一个CPU绑定的工作负载 这意味着

16:30
Each thread will always get its full time slice What I am describing is essentially a CPU-bound workload When the eighth thread enters the hardware thread it will get the full time slice from start to end It will not switch until the end of this time slice Now the opposite of CPU-bound workload is what we call IO-bound or blocking workload
每个线程都将始终获得其完整的时间片 我描述的实质上是一个CPU绑定的工作负载 当第八个线程进入硬件线程时 它将从开始到结束获得完整的时间片 直到这个时间片结束才会切换 现在 cpu绑定工作量的对立面是我们称之为IO绑定或阻塞工作量

16:54
This IO binding or blocking workload These IO binding workloads These IO binding workloads are workloads, the thread never actually uses its full time slice because within the scope of its time slice it makes a network call to the operating system It does something that causes it to go from running to waiting even in this case I have 100 threads and I have 1000 threads
这种IO绑定或阻塞工作量 这些IO绑定工作量 这些IO绑定工作量是工作量，线程从未实际使用其完整时间片 因为在其时间片的范围内 它会向操作系统发出网络调用 它会做某事 这会导致它从运行状态进入等待状态 即使在这种情况下，我有100个线程，我有1000个线程

17:22
The scheduler periodically processes 1,000 threads in our simulated operating system, and the time to get to 10 seconds is very tight, because there's a good chance that that thread is very early, maybe in its first millisecond, or we'll make a call to the operating system, maybe read something from the network, and it's going to be switched out immediately
调度器周期性地在我们模拟的操作系统这里处理1000个线程的机会 达到十秒的时间非常紧张 因为很有可能那个线程很早 可能在它的第一个毫秒内 或者我们会向操作系统发出调用 也许去读取网络中的内容 并且立即会被切换出去

17:42
For these I/O constrained workloads, context switching is actually our friend, yes, when it comes to CPU-constrained workloads, context switching is hurting us, think about it, it's hurting us because we have to take this 12,000 to 24,000 instructions every time we switch context
对于这些I/O受限的工作负载 上下文切换实际上是我们的朋友 没错 当涉及到CPU受限的工作负载 上下文切换正在伤害我们 想想看，它在伤害我们 因为我们每次上下文切换要承受这一万二到两万四千条指令的打击 每次上下文切换

18:02
And these instructions could have been part of our work, but for an I/O constrained workload, context switching is our friend, because the thread will get stuck, it will go into a waiting state, which will keep the hardware thread idle, and we can now use these 12,000 to 24,000 instructions to do context switching
而这些指令本可以成为我们工作的一部分 但对于一个I/O受限的工作负载 上下文切换是我们的朋友 因为线程会陷入停滞 它会进入等待状态 这会让硬件线程保持空闲 我们现在可以利用这十二千到两万四千条指令来做上下文切换

18:27
So that you start another thread That's why it's so important to understand our workload because if it's a CPU-bound workload then we really don't want to have more threads because of our hardware threads because context switching is hurting us It extends the scheduling cycle the more threads you have
以便启动另一个线程 这就是为什么理解我们的工作负载如此重要 因为如果是CPU绑定的工作负载 那么我们真的不想有更多的线程 因为我们的硬件线程 因为上下文切换在伤害我们 它延长了调度周期 你拥有的线程越多

18:48
But if it's an I/O-bound workload, right now, these context switches are our friends, they help us get more done faster because we don't allow the CPU or in this case the hardware threads stay idle, and by the way, you have to understand that our operating system scheduler will be a preemptive scheduler
但如果它是I/O绑定的工作负载 现在 这些上下文切换是我们的朋友 它们帮助我们更快地完成更多工作 因为我们不允许CPU 或者这种情况下硬件线程保持空闲 顺便说一句 你必须明白 我们的操作系统调度器将是一个抢占式调度器

19:11
What does that mean that the operating system has to process events Think about it, your hardware is processing events all the time, and I just mean, just to keep the clock updating an event happening on the machine Whenever an event happens on the machine, a thread has to respond to it So, part of the scheduler also has to create a mapping of hardware events to the operating system threads
这意味着什么 这意味着操作系统必须处理事件 想想看 你的硬件一直在处理事件 我只是说，仅仅为了保持时钟同步更新 机器上正在发生一个事件 每当机器上发生一个事件 一个线程必须对它做出响应 所以，调度器的一部分也必须创建一个硬件事件到操作系统线程的映射

19:39
Set some operating system threads to high priority even if we're working on a CPU-bound workload So, even if we're working on a CPU-bound workload even if we're doing this CPU-bound workload every time the clock has to run We have to interrupt that workload Get the clock thread to run fast
将某些操作系统线程设置为高优先级 即使我们在处理一个CPU绑定的工作负载 所以，即使我们在处理一个CPU绑定的工作负载 即使我们在进行这个由CPU限制的工作量 每次时钟必须运行 我们必须中断那个工作量 获取时钟线程以快速运行

19:59
Get it done and immediately remove it I don't want the preemptive scheduler that we have to be affected based on events and we don't forget that, but it does provide something that we need to understand and that is that scheduling is uncertain and that all things being equal we never know what the scheduler will do
完成它的事情并立即移除 我不想我们具有的抢占式调度器 基于事件而受到影响 我们不会忘记这一点 但它确实提供了一些我们需要理解的东西 那就是调度是不确定的 在所有事情都平等的情况下 我们永远不知道调度器会做什么

20:23
We have to keep this in mind when we design our code, whatever we do, especially in multithreaded software, there must be a guaranteed moment, and that is that our work processes synchronization and coordination, in other words, putting guaranteed points in the code so that we can guarantee that the algorithms run even if they are executed out of order
我们必须将这个放在心中 在我们设计代码时 无论我们做什么 特别是在多线程软件中 必须有保证时刻 那就是我们的工作处理同步和协调 换句话说 在代码中放置保证的点 这样我们可以保证算法运行 即使它们以非顺序执行

20:46
They will work correctly so even if it's a preemptive scheduler I want to throw it out for a moment Let's forget about that now we just look at the CPU-limited and the I/O limited and understand what they mean Now we understand a little bit of our scheduling cycle wants to create the illusion of all threads running at the same time
它们将正确运行 所以 即使它是抢占式调度器 我想暂时将其抛出 让我们现在就忘记这一点 我们只关注CPU限制的和I/O限制的 并且了解它们的含义 现在我们理解了一点我们的调度周期 想要创建所有线程同时运行的错觉

21:09
Now we understand that when the time slice becomes too small, there is a point where the return is reduced because our context switching causes us to lose 12,000 to 24,000 instructions that end up catching up with us, so as a scheduler, we have to adjust those numbers, but for our purposes, now context switching at the cost of a delay of 1 to 2 microseconds
现在我们理解了当时间片变得太小时 存在减少回报的点 那是因为我们的上下文切换 导致我们损失12000到24000条指令最终会赶上我们 所以作为调度器 我们必须调整这些数字 但对于我们的目的 现在 在1到2微秒的延迟成本上上下文切换

21:34
It's a good number for us, we have to really look at our time slices and the scheduling cycle of the operating system, whatever they are, this model is a good mental model, so let's summarize, by thinking about two algorithms, well, it can help us understand it better There are two algorithms that we can play with
是一个对我们很好的数字 我们必须真正看看 我们的时间片和操作系统的调度周期 无论它们是什么 这个模型是一个良好的心理模型 所以让我们总结一下 通过思考两个算法 嗯可以帮助我们更好地理解它 有两个算法我们可以玩

21:59
One is CPU limited and one is I/O bounded, let's focus on the CPU-limited algorithm first So let's assume me I'm sincerely asking you to write an algorithm that can handle a set of numbers Let's say there are a million numbers here This is Let's draw this set here
一个是CPU限制的，一个是I/O限制的，让我们首先关注CPU限制的算法 那么让我们假设我 我真诚地要求你编写一个算法，它可以处理一个数字集合 假设这里有一百万个数字 这是一个 让我们在这里画一下这个集合

22:15
It's a set of a million integers, and I say, I want you to add up each number in this set and then tell me what that value is, whatever we do, especially in multithreaded software, and the first thing we need to do is write a sequential version of the algorithm, so we need to write a sequential version of the ad
这是一个包含一百万个整数的集合，我说 我想让你在这个集合中每个数字相加 然后告诉我这个值是多少 无论我们做任何事情 尤其是在多线程软件中 我们需要做的第一件事是编写算法的顺序版本 所以我们需要编写一个顺序版本的ad

22:39
Basically this will be five lines of code We will go through this set it is based on integers We will iterate using our value semantics We will have a local variable and we will add to it the sequential version just from the beginning to the end of the five lines of code, done Now we have a sequential version of the next question always
基本上这将是五行代码 我们将遍历这个集合 它是基于整数的 我们将使用我们的值语义来迭代 我们将有一个局部变量并且我们将添加到它 顺序版本只是 从开始 到结束 五行代码，搞定 现在我们有了一个顺序版本 下一个问题总是

23:03
Now can we work in parallel Let's talk about this again Concurrency means asynchronous execution Now we can say does it matter the order of these integers that I add Does this affect the final result When adding a set of integers the answer is no We can do concurrent work here The order in which these integers are added does not matter I am here...
现在是否可以并行工作 我们再来谈谈这个问题 并发意味着异步执行 现在我们可以说 这重要吗 顺序 我添加的这些整数 这会影响最终的结果吗 在添加整数集合时 答案是不 我们可以在这里进行并发工作 添加这些整数的顺序无关紧要 我在...

23:32
As long as we add them all up, it's really cool that we have a problem in front of us that can take advantage of concurrency One right idea might not be a problem I can split the list in two, just right I can say, let our OS thread add this half and have the other OS thread add that half irregularly
只要我们把它们都加起来 这真的很酷 我们面前有一个可以利用并发的问题 一个正确的想法可能没有问题 我可以将列表一分为二，正好 我可以说，让我们的操作系统线程来添加这个一半 并且让另一个操作系统线程在不规则地添加那半个

23:56
Then we can add these two values together to get that result.
然后我们可以将这两个值相加，得到那个结果。

24:01
I can actually argue that I can split it into multiple lists and multiple threads You might be thinking, wow, yes, we can get a bunch of threads, maybe we can get a hundred threads by adding decimal segments, and then advertise that would be great it could be, but remember, the only reason we add this complexity is because we can get things done faster
实际上我可以争论说我可以将其拆分为多个列表和多个线程 你可能觉得 哇哦 是的 我们可以得到一堆线程 也许我们可以通过添加小数段的方式来得到一百个线程 然后做广告 那将非常棒 它可以是 但请记住，我们添加这种复杂性的唯一原因是因为我们可以更快地完成工作

24:25
Trust me, the complexity here is because we can get work done faster we can get higher throughput Let's go back to the idea of parallelism Remember, parallelism means executing instructions at the same time two or more which is what it means to be able to do work at the same time Yes that's what we're talking about here So let's go back to the hardware we imagined
相信我 这里的复杂性是因为我们可以更快地完成工作 我们可以获得更高的吞吐量 让我们回到并行性的想法 记住，并行性意味着同时执行指令 两个或更多 这是能够同时做工作的意思 对 这就是我们在这里谈论的 所以让我们回到想象中的硬件

24:52
Remember, our imaginary hardware is just a single thread, that's all What is the number of threads I can execute at the same time Physically, the answer is one can only execute one thread at a time Think about it I have this array of millions of integers Let's say I split it into four lists
记住，我们的想象中的硬件只是一个单一的硬件 线程，仅此而已 我可以同时执行的线程数量是多少 从物理上来说，答案是一个 在同一时间只能执行一个线程 想一想 我有这个数百万整数的数组 假设我将其分成四个列表

25:18
And I throw a thread on each list thread, thread, thread, thread question whether executing this algorithm sequentially is faster or slower than executing it in parallel with four threads when we only have one piece of hardware think about it, because it's a CPU-bound job since I can only physically execute one thread at the same time
并且我在每个列表上投掷一个线程 线程，线程，线程，线程 问题 顺序执行这个算法 与使用四个线程并行执行相比，速度是更快还是更慢 当我们只有一个硬件时 想想，因为这是一项CPU绑定的工作 由于我只能在物理上同时执行一个线程

25:44
The sequential version will be faster because every time we switch threads we lose 12,000 instructions We will have to switch threads four times What are we losing every time we switch threads We lose 12,000 instructions This is the loss of 12,000 instructions means we do all the work in a time slice
顺序版本将更快 因为我们每次切换线程时 我们都会损失12000条指令 我们将不得不四次切换线程 每次我们切换线程时 我们失去的是什么 我们损失了12000条指令 这是12000条指令的损失 这意味着我们在时间片内完成了所有工作

26:10
If we don't do it, we're going to lose 12,000 more instructions, which are 12,000 instructions that we can use to add integers, and one thing you need to understand in CPU binding is that if we only have one hardware thread, then we can actually only run one operating system thread efficiently
如果没完成 我们将遭受更多的12000条指令的损失 这些都是我们可以用来加整数的12000条指令 在CPU绑定的工作中，你需要理解的一点是 如果我们只有一个硬件线程 那么我们实际上只能高效地运行一个操作系统线程

26:36
But if I change my hardware, if I change my hardware to a dual-hardware, threaded processor, how many threads can I run now, I can run two threads at the same time, think about it, think about it, now this concurrency fact is interesting to me, because I can run two threads at the same time, and now I can split this list in half
但如果我改变我的硬件 如果我将我的硬件改为双硬件线程处理器 我现在可以运行多少个线程 我可以同时运行两个线程啊 想一想 现在考虑一下 现在 这个并发的事实对我很有趣 因为我可以同时运行两个线程 现在我可以将这个列表分成两半

27:05
Give this thread and this thread their respective lists correct they can run in parallel and we can do this now and at the same time, when we get the value If I have four hardware threads I can use the OS threads, do it faster So I want you to recognize this when it's a CPU-constrained workload
给这个线程和这个线程各自的列表 正确 它们可以并行运行 我们现在可以完成这项工作 同时，当我们得到值时 如果我有四个硬件线程 我可以使用操作系统线程，更快地完成 所以我想让你认识到这一点 当它是一个CPU受限的工作负载时

27:30
If you want to get higher throughput, if the algorithm is concurrent, then you need parallelism right This is where I say these words are sometimes confused, sometimes not confused because context switching is hurting us But let's go back to a single hardware thread and that's what our hardware looks like assuming it's not an integer list
如果你想获得更高的吞吐量 如果算法是并发的 那么你需要并行性 正确 这是我说这些词有时混淆，有时不混淆的地方 因为上下文切换在伤害我们 但是让我们回到单硬件线程 这就是我们的硬件看起来的样子 假设这不是整数列表

27:55
No, no, no, no, this is a list of URLs that we need to go to get and process What does that mean This is not CPU constrained Now IO limited work means that when any given thread makes a network call, it goes into a waiting state Ah so think about it if I build that algorithm sequentially
不，不，不，不，不 这是一个URL列表 我们需要去获取和处理的URL列表 这意味着什么 这不是CPU受限的 现在是IO受限的工作 这意味着任何给定的线程进行网络调用时 它会进入等待状态 啊 所以想想 如果我顺序构建那个算法

28:20
It's going to take a specific amount of time but since it's IO constrained what that means I can split the list into multiple threads and do it faster even if I have a hardware thread because now context switching is helping me this thread start maybe it took 1 millisecond and then make a network call and go into a wait state
它将需要特定的时间 但由于它是IO受限的 这意味着什么 这意味着我可以将列表分成多个线程 即使我有一个硬件线程，也能更快完成 因为现在上下文切换在帮助我 这个线程开始 也许它花费了1毫秒 然后进行网络调用并进入等待状态

28:46
You know 1 millisecond and then it goes into a waiting state and now what's going on we get 12,000 instructions to complete that task, until then put this wire on and the hardware will be idle Now we've passed 1 millisecond but guess what, this will start running from 1 millisecond Now all these threads are starting to work
你懂吗 1毫秒 然后它进入等待状态 现在 发生了什么 我们得到了12000条指令 要完成那个任务，直到那时把这个线穿上 硬件将处于闲置状态 现在我们已经过去了1毫秒 但猜猜看，这会从1毫秒开始运行 现在所有这些线程都能开始工作

29:13
Because this processor will be idle because these threads are all saying I don't need time anymore The interesting part about IO-bound workloads is that it's hard to determine the most efficient number of threads, in other words, there's still the problem of diminishing marginal benefit if you use two less or diminishing marginal benefit at two more
因为这个处理器将处于闲置状态 因为这些线程都说我不再需要时间了 关于IO绑定工作负载的有趣部分是 很难确定最有效的线程数量 换句话说 仍然存在边际效益递减的问题 如果你使用两个更少或边际效益递减在两个更多

29:36
Even if you use two less, you're going to have a problem where you have to find that magic number that is called the real question is, is there a magic number, only one thread at that weight in that runnable state, and that's what we're looking for, right, we only have one thread in any runnable state
即使你使用两个更少 你将会遇到一个问题 你必须找到所谓的那个魔法数字 实际上的问题是，是否存在一个魔法数字，只有一个线程 在那个重量 在那个可运行状态 这就是我们正在寻找的，对吧 我们只有一个线程 在任何可运行状态

29:56
Then we will have the most efficient number of threads for IO-bound workloads These things are very complex CPU-bound workloads are good, simple and very efficient Right, we know that for any CPU-bound workload the number of threads we use is equal to the number of hardware threads we use
然后我们将拥有最有效的线程数量 对于IO绑定的工作负载 这些东西非常复杂 CPU绑定的工作负载很好，简单且非常有效 对吧 我们知道，对于任何CPU绑定的工作负载 我们使用的线程数量等于我们使用的硬件线程数量

30:16
Parallelism is important but when it comes to IO-bound workloads we don't need parallelism to see concurrency improvements because threads can take turns using hardware here, right, these context switches are helping us to get more done over time that we don't really know how much
并行性很重要 但当涉及到IO绑定的工作负载时 我们不需要并行性来看到并发的改进 因为线程可以在这里轮流使用硬件，对吧 这些上下文切换正帮助我们 帮助我们随着时间的推移完成更多的工作 我们真的不知道有多少

30:37
So when it comes to something like an operating system we always use thread pools and we use thread pools to do this Imagine if you are building a web service and you decide to create an operating system thread for each request that comes into the server if you have 50,000 requests
因此，当涉及到像操作系统这样的东西时 我们总是使用线程池 我们使用线程池来做这件事 想象一下，如果你正在构建一个Web服务 并且你决定为每个进入服务器的请求创建一个操作系统线程 如果你有50,000个请求

30:56
We're just playing with 100 threads Imagine 50,000 threads what problems this will cause This is not going to work So we want a thread pool where we send our work We have to find that magic number We have to find the number that uses too many threads Right now, context switching is hurting us
我们只是在玩100个线程 想象50,000个线程 这将导致什么问题 这不会起作用 所以我们想要一个线程池，我们将工作发送到其中 我们必须找到那个魔法数字 我们必须找到使用太多线程的数字 现在，上下文切换正在伤害我们

31:16
We have too many threads in a runnable state If we use numbers that are too low then we won't do very well because the idle time of our processor will increase because I don't have threads ready These problems are complicated at the operating system level Okay, so let's summarize a little bit here Concurrency means out of order, right
我们有太多的线程处于可运行状态 如果使用太低的数字 那么我们的表现也不会很好 因为我们处理器的闲置时间会增加 因为我没有准备好的线程 这些问题在操作系统层面上很复杂 好的 所以让我们在这里稍微总结一下 并发意味着无序执行，对吧

31:44
Parallelism means executing two or more instructions at the same time We have to know the state of the thread and we have to know if our workload is I/O constrained or CPU constrained CPU-constrained workloads mean that threads do not naturally enter the waiting state which means we need parallelism to get any throughput with concurrency
并行意味着同时执行两个或更多指令 我们必须知道线程的状态 并且我们必须知道我们的工作负载是 I/O 受限还是CPU 受限 CPU 受限的工作负载意味着 线程不会自然地进入等待状态 这意味着我们需要并行来通过并发获得任何吞吐量

31:58
I/O constrained workloads mean threads naturally go into a waiting state This means we don't need parallelism Concurrency gives us throughput Context switching helps us get more done on single hardware Single threaded hardware These are the things we need to continue to focus on and finalize Remember, CPU-constrained workloads are the ones we have the most efficient workloads on our machines
I/O 受限的工作负载意味着线程会自然地进入等待状态 这意味着我们不需要并行 并发就能给我们带来吞吐量 上下文切换帮助我们在单硬件上完成更多工作 单线程硬件 这些都是我们需要继续关注和最终确定的事情 记住，CPU 受限的工作负载是我们在机器上最有效的工作负载

32:16
Now what we need to do is talk about the scheduler and its place in the operating system and some mechanical sympathy that we need As Go developers, we need to make sure that our algorithms and work work efficiently with the Go scheduler The Go scheduler runs on top of the operating system, and the OS runs on top of the hardware
现在我们需要做的是谈论调度程序 以及它在操作系统中的位置 以及我们需要的一些机械同情 作为 Go 开发人员，我们需要确保我们的算法和工作与 Go 调度程序高效配合 Go 调度程序运行在操作系统之上，操作系统运行在硬件之上

32:33
scheduler scheduler
调度程序 调度程序 调度程序 调度程序 调度程序 调度程序
