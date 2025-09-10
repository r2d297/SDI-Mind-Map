8.1 OS Scheduler Mechanics
8.1 操作系统调度器机制

Transcript  课程文稿

00:00:00

(upbeat music) - [Announcer] Ardan Labs, specializing in high-performance software consulting, training, staffing and development. Welcome to Module 8, goroutines. Let's get started with Lesson 8.1, OS Scheduler Mechanics. - We're about to move into talking about multi-threaded software
（活泼的音乐）- [主持人] Ardan Labs，专门从事高性能软件咨询、培训、人员配置和开发。欢迎来到第 8 模块，goroutine。让我们开始学习第 8.1 课：操作系统调度器机制。- 我们即将讨论多线程软件


00:00:20

and I always like starting with the operating system mechanics 'cause they really give us a good understanding and background for how all this multi-threaded software is going to work, even in Go, which is sitting a layer above the operating system. And there's a bunch of terms that we're gonna need to define along the way as well. Like what does concurrency actually mean?
我总是喜欢从操作系统机制开始讲解，因为它们为我们提供了关于多线程软件如何工作的深入理解和背景，即便是在位于操作系统之上的 Go 语言中也是如此。在这个过程中，我们还需要定义一些术语。比如并发到底是什么意思？


00:00:40

What does parallelism actually mean? And concurrency, we could start with that right now, means out-of-order execution. That's really the only thing that I want you to keep in your head. The idea that we have a sequence of instructions that we're looking to execute from beginning to end, but we're gonna execute them out of order, still get them all executed
并发和并行到底是什么意思？并发首先意味着无序执行。这是我希望你记住的唯一一点。我们有一系列指令要从头到尾执行，但我们将以无序的方式执行它们，


00:01:01

and hopefully get to the same result. So we're always gonna be thinking about out-of-order execution when it comes to concurrency. Parallelism, that means that we're executing two or more instructions at the same time. It's about doing a lot of work at once. And what's interesting is sometimes
同时仍然能执行所有指令，并希望最终得到相同的结果。所以在讨论并发时，我们始终要考虑无序执行。而并行则意味着同时执行两个或多个指令。它关乎同时做大量工作。有趣的是，


00:01:20

these terms blend into each other, sometimes they're just polar opposites. And we'll figure out when that is as we continue to talk about OS and then Go scheduler mechanics. But let's focus on what we need to know about the operating system. So let's say I was asking you to write an operating system scheduler.
有时这些术语会相互交织，有时又完全对立。随着我们继续讨论操作系统和 Go 调度器机制，我们将逐渐厘清这一点。但现在让我们专注于操作系统需要了解的内容。比如，如果让你设计一个操作系统调度器，


00:01:40

What are the things that you need to kind of consider if you're gonna be doing that sort of engineering? And one of the ideas here that we gotta really cement ourselves in is this idea that we want to create an illusion that a lot of work is happening on the machine at once. In other words, we should be able to run multiple programs, multiple applications at the same time,
你需要考虑哪些因素？这里有一个关键的想法，我们必须牢记：要创造一种所有工作都在机器上同时进行的假象。换句话说，我们应该能够同时运行多个程序、多个应用，


00:02:02

and create that illusion that they're all running at the same time. Now, physically, they're not gonna be able to do that. It's all gonna depend on the hardware that we have and we can create some imaginary hardware for this as well as we learn our mental models. So let's start off with a very simple hardware
并创造出它们好像都在同时运行的假象。现在，从物理上讲，它们无法真正同时运行。这完全取决于我们拥有的硬件，随着我们学习心智模型，我们还可以创建一些虚拟硬件。让我们从一个非常简单的硬件开始


00:02:20

where all we have is a single processor and that processor has a single hardware thread. And let's represent that hardware thread as the ability to execute instructions. So every hardware thread that we have in the machine gives us the ability to execute instructions. So if I only have one hardware thread,
在这里，我们只有一个处理器，且只有一个硬件线程。让我们将这个硬件线程表示为执行指令的能力。因此，机器中的每个硬件线程都赋予我们执行指令的能力。所以如果我只有一个硬件线程，


00:02:41

then I could only execute one instruction at any given time. If I had two hardware threads, then I could run executions or execute instructions in parallel. You get it? Now, my machine is an eight hardware thread machine. So technically, I can run eight instructions in parallel at any given time.
那么在任何给定时刻我只能执行一条指令。如果我有两个硬件线程，那么我就可以并行运行执行或执行指令。明白了吗？现在，我的机器是一个八硬件线程的机器。因此，从技术上讲，我在任何给定时刻可以并行运行八条指令。


00:03:01

But for now, let's imagine that our hardware is single hardware threaded. Now, that's at the hardware level. We've got to, in our operating system scheduler, leverage this. So what we're gonna do is we're gonna define the idea of an operating system thread. If there's gonna be a hardware thread, we're gonna represent the idea
但现在，让我们假设我们的硬件是单硬件线程的。这是在硬件层面。在操作系统调度器中，我们必须利用这一点。所以我们要做的是定义操作系统线程的概念。如果有硬件线程，我们将表示


00:03:20

of an operating system thread, our own thread. And I always want us to think of threads as paths of execution. So our program is gonna be a series of instructions. Those instructions are laid out to execute in sequence and it's the job of the thread, our operating system thread right now, to execute those instructions one at a time,
操作系统线程，我们自己的线程。我总是希望我们将线程视为执行路径。我们的程序将是一系列指令。这些指令按顺序排列以执行，而线程的工作，目前是我们的操作系统线程，是一次执行这些指令。


00:03:41

do the accounting and to leverage this hardware thread to do it. So the operating system is going to execute those instructions in sequence, leveraging the hardware thread that does the actual execution. All right? Now, when we think about these operating system threads, we're gonna have three different states
进行管理并利用这个硬件线程来完成。因此操作系统将按顺序执行这些指令，利用执行实际操作的硬件线程。明白了吗？现在，当我们思考这些操作系统线程时，我们将有三种不同的状态


00:04:00

that that operating system thread can be in. And there's a lot more really, like sub states, but remember, we don't have to have full understandings of implementation details here. What we need are good mental models of how things work and behave, and that will help us make better engineering decisions. So there's gonna be three states
操作系统线程可能处于的状态。实际上还有更多子状态，但请记住，我们不必完全了解实现细节。我们需要的是对事物如何工作和表现的良好心智模型，这将帮助我们做出更好的工程决策。所以会有三种状态


00:04:21

that a thread can be in. A thread could be in a running state. And when a thread is in a running state, that means we've placed it on this hardware thread right here and it's executing its instructions that it's responsible for. A thread can be in a runable state, and when it's in a runable state, it means that it wants time on that hardware thread.
线程可以处于的状态。线程可以处于运行状态。当线程处于运行状态时，意味着它已被放置在这个硬件线程上并正在执行其负责的指令。线程可以处于可运行状态，当处于可运行状态时，意味着它希望获得硬件线程的执行时间。


00:04:40

It just has to wait its turn. And then, a thread can be in a waiting state. When a thread's in a waiting state, we really consider it kind of off the radar, right? It's gone and it's waiting for something to happen. It could be waiting for the operating system to come back with a system call. It could be waiting for something on the network to come back in and it's in a waiting state.
它只需要等待轮到自己。然后，一个线程可能处于等待状态。当一个线程处于等待状态时，我们实际上认为它已经处于"雷达"之外，对吧？它已经消失并在等待某些事情发生。它可能在等待操作系统返回系统调用，也可能在等待网络上的某些内容返回，处于等待状态。


00:05:00

And from our scheduler's point of view, we only care about threads that are running or runable, right? Threads that are waiting, don't put any load on us. They're not our concern, okay? So imagine the following scenario. We have a couple of programs running, which means we have a few threads
从调度器的角度来看，我们只关心正在运行或可运行的线程，对吧？处于等待状态的线程不会给我们带来任何负载。它们不是我们关心的对象，好吗？假设以下场景。我们有几个正在运行的程序，这意味着我们有几个


00:05:20

that are in play, and the idea is that we want to create this illusion, even with one hardware thread, that all the threads that we have that are either in a running or a runnable state are actually running at the same time. So how could we create this illusion with our scheduler? So one idea is that we can define
正在运行的线程，其想法是即使只有一个硬件线程，也要创造一种幻觉，让我们所有处于运行或可运行状态的线程看起来是同时运行的。那么我们的调度器如何创造这种幻觉？一个想法是我们可以定义


00:05:42

what we'll call a scheduler period. So let's define our scheduler period. Now, the scheduler period, what it's responsible for is our ability to execute any thread that's in a runnable state at the beginning of this period to get that thread to execute within this time.
我们将其称为调度器周期。让我们来定义一下调度器周期。调度器周期的职责是在周期开始时能够执行任何处于可运行状态的线程，并在此周期内使该线程得以执行。


00:06:02

And if we can do that, then we can create the illusion at least within the scope of the scheduler period that everything's running at the same time. Now, we could play with some, you know, fun numbers here. I'll give you some real numbers for certain things, other numbers, we'd have to really look at our operating system scheduler to see what they are.
如果我们能做到这一点，那么至少在调度器周期的范围内，我们就可以营造出所有任务同时运行的假象。现在，我们可以尝试一些有趣的数字。对于某些数据，我给你一些实际的数字，而对于其他数据，我们需要仔细查看操作系统调度器才能了解具体情况。


00:06:21

But we can use some base numbers to get an idea. And let's just say right now that our scheduler period is gonna be, let's just say 100 milliseconds. Let's just say that that's what we're gonna use. Our scheduler period is gonna be 100 milliseconds. So the idea is that what we want is to make sure that every thread that we have in a runable state executes
但是我们可以用一些基本数字来了解情况。现在就假设我们的调度周期是 100 毫秒。就用这个数值。我们的调度周期将是 100 毫秒。所以我们的想法是确保每个处于可运行状态的线程都能执行


00:06:41

within this 100 millisecond timeframe to create the illusion that everything is running at the same time. So let's start off our scheduler. When we do that, and right at the beginning of the scheduler period, what we notice is that we have just one thread in a runnable state. That's all we have.
在这 100 毫秒的时间范围内创造一种所有事情似乎同时运行的假象。让我们开始讨论调度器。当我们这样做时，在调度器周期的一开始，我们注意到只有一个线程处于可运行状态。这就是我们所拥有的全部。


00:07:00

So if we only have one thread in a runnable state and and our hardware only has that single hardware thread, remember only one thread can physically execute at any given time, then this thread, we'll call this thread A. Thread A is going to get the full 100 milliseconds of time to execute its instructions.
如果我们只有一个处于可运行状态的线程，而我们的硬件只有那个单一的硬件线程，请记住在任何给定时间只能有一个线程物理执行，那么这个线程，我们称之为线程 A。线程 A 将获得全部 100 毫秒的时间来执行其指令。


00:07:20

It gets the full 100 milliseconds. It's brilliant, right? A whole lot of time to do work. And remember some of the numbers that we talked about earlier in the video. We said that every nanosecond of time, remember that, right, every nanosecond of time,
它获得全部的 100 毫秒。这是不是很棒？有大量的时间来完成工作。还记得我们之前在视频中讨论的一些数字。我们说过每一个纳秒的时间，记得吗，每一个纳秒的时间，


00:07:40

one nanosecond of time equals 12 instructions. I want you to remember that number. One nanosecond represents those 12 instructions. Okay, great. So we're gonna keep that number in our head as we continue to go through this exercise. Now, we've got the A goroutine.
一纳秒的时间等于 12 条指令。我希望你记住这个数字。一纳秒代表这 12 条指令。好的，很好。我们在继续这个练习时，请将这个数字记在心里。现在，我们有了 A goroutine。


00:08:00

It was in a runnable state before that scheduler period started and now it's off doing its work. Now, the scheduler period is done, and once the scheduler period is done, we go back and we look at how many threads we have in a runnable state. Let's say right now we have two threads in a runnable state. So what does that mean? Well, it means now that we're gonna schedule both threads
在调度器周期开始之前，它处于可运行状态，现在正在执行自己的工作。现在，调度器周期已经结束，当调度器周期结束后，我们回过头来查看有多少线程处于可运行状态。假设现在我们有两个处于可运行状态的线程。那么这意味着什么呢？这意味着我们将在同一个 100 毫秒的调度器周期内调度这两个线程


00:08:20

to execute within our same 100 millisecond scheduler period. So we decide to run thread A again, but we know that thread A is only gonna get what, 50 milliseconds this time, which now means that we're gonna schedule that other thread, thread B, to run and thread B is only gonna get 50 milliseconds.
执行。所以我们决定再次运行线程 A，但我们知道这次线程 A 只能获得大约 50 毫秒的运行时间，这意味着我们将调度另一个线程，即线程 B 运行，而线程 B 也只能获得 50 毫秒的运行时间。


00:08:42

So let's look at what just happened here. We did create the illusion that two threads ran within the scope of our scheduler period. But if we start looking at what's happening to our A thread, it got 100 milliseconds of runtime the first time, but now it got cut in half. Its throughput across the next 100 milliseconds
让我们看看刚才发生了什么。我们创造了一个假象，即在调度器周期内有两个线程同时运行。但如果我们仔细观察 A 线程发生的情况，它第一次获得了 100 毫秒的运行时间，但现在被减半了。它在接下来的 100 毫秒内的吞吐量


00:09:02

got cut in half. We're not executing as many instructions as we otherwise did in the previous run. Okay, no problem. Let's keep going. Schedule A period is over. We look again and what do we notice? We notice now that we have five, five threads now
被减半了。我们执行的指令数比之前的运行要少。好的，没问题。让我们继续。调度周期 A 结束。我们再次查看，发现什么？我们注意到现在有五个、五个线程处于可运行状态。


00:09:22

ready to to run in a runable state. So what does that mean? Now it means that we've gotta cut this down again, right? And so this time, what is thread A gonna get? Thread A is only gonna get what? It's only gonna get 20 milliseconds this time. So now, thread A is gonna get 20 milliseconds. We now know that thread B
这意味着什么？现在意味着我们必须再次缩减，对吧？这次线程 A 将获得什么？线程 A 只会获得什么？它只会获得 20 毫秒。所以现在，线程 A 将获得 20 毫秒。我们现在知道之前的线程 B


00:09:41

that we had is gonna get its 20 milliseconds. 20 milliseconds for thread B. And then what are we gonna do with that remaining 60 milliseconds here, right? The remaining 60 milliseconds now is gonna go across those other threads, C, D and E, right? That's gonna be the remainder of that 60 milliseconds of time.
将获得它的 20 毫秒。线程 B 的 20 毫秒。那剩余的 60 毫秒我们将如何处理？剩余的 60 毫秒现在将分配给其他线程 C、D 和 E，对吧？这将是剩余的 60 毫秒时间。


00:10:01

And I want you to notice again that every time more threads show up to be run within this scheduler period, the time starts to get smaller and smaller and smaller, right? If eventually we had 100 threads that wanted to run within this scheduler period, we had 100 threads, we're now at the point
我希望你再次注意到，每当在这个调度周期内出现更多可运行线程时，时间就会变得越来越小，越来越小，对吧？如果最终我们有 100 个线程想在这个调度周期内运行，我们有 100 个线程，现在我们已经到了这个点


00:10:21

where this thread right here, thread A, is gonna be down to what? One millisecond of time, one millisecond of runtime. And what that means is that at some point there's gonna be a diminishing return on the time a given thread really gets to do any work.
在这里，这个线程 A 将会降低到什么程度？一毫秒的时间，一毫秒的运行时间。这意味着在某个时刻，给定线程真正能够完成工作的时间将会出现递减的收益。


00:10:41

And it's mainly because there's a cost here that I haven't touched upon, and that is the context switch cost. Now, think about this for a second. We have thread A and thread A is coming in and says, okay, I want time on this hardware thread. So we go in here and we place A on the hardware thread
这主要是因为有一个我还没有提到的成本，那就是上下文切换成本。现在，思考一下这个情况。我们有线程 A，线程 A 进来并说，好的，我想使用这个硬件线程。所以我们将 A 放置到硬件线程上


00:11:01

and it's doing its work for that 100 milliseconds. And now we decide, okay, now thread B, thread B is gonna run for its, let's say, one millisecond. Well, we've got to take some time to pull this thread off the hardware, right, and then we've gotta put this thread on the hardware.
它在这里工作了 100 毫秒。然后我们决定，好的，现在轮到线程 B 运行，假设运行一毫秒。嗯，我们需要花一些时间将这个线程从硬件上移除，然后再将另一个线程放到硬件上。


00:11:22

I mean, that's not free. That's going to take some time. This is what we call a context switch. Taking one thread off, putting another thread on. Now, on average, on average at the operating system level, a context switch like this is gonna be anywhere from one millisecond to two milliseconds.
我的意思是，这不是免费的。这将会花费一些时间。这就是我们所说的上下文切换。将一个线程移除，再放置另一个线程。现在，平均来说，在操作系统层面，这样的上下文切换大约需要一到两毫秒的时间。


00:11:43

In other words, 1000 nanoseconds to 2000 nanoseconds. Let's start doing the math again. Remember, a nanosecond of time represents 12 instructions. So what are we looking at here
换句话说，是从 1000 纳秒到 2000 纳秒。让我们再次进行数学计算。请记住，一纳秒的时间代表 12 条指令。那么我们这里看到的是什么呢


00:12:00

when we talk about a one to two millisecond context switch? What we're talking about here really is a 12,000 to 24,000 instruction loss, right? Instructions we otherwise could have been executing, but we can't because of this context switch.
当我们谈论一个一到两毫秒的上下文切换时？我们实际上讨论的是损失了 12,000 到 24,000 条指令，对吗？这些本可以执行的指令，因为这个上下文切换而无法执行。


00:12:22

So, think about where we're at. If you have this many threads context switching at one millisecond, or even worse, what if this gets down to 1000 threads? Oh my goodness, 1000 threads. Now we're talking about microseconds, right? Microseconds of time that a thread gets
那么，想象一下我们现在的情况。如果有这么多线程在一毫秒内上下文切换，或者更糟的是，如果线程数量达到 1000 个？天啊，1000 个线程。现在我们谈论的是微秒，对吧？线程在一到两微秒的上下文切换之上执行的微秒时间


00:12:42

to execute on top of the one to two microseconds of context switch. What eventually happens is that you're doing more context switch work than you are actual work. And this is not good. So there's a point of diminishing return
最终发生的情况是，你进行的上下文切换工作比实际工作还多。这是不好的。因此，存在一个收益递减的点


00:13:00

where that time slice gets to a point where, and the number of threads where you're doing more context switch work than actual work, and we're not really getting any throughput from the machine or our apps. So what are we going to do, because if we just stick with a scheduler period of 100 milliseconds
在那个时间片达到一定程度时，以及线程数量导致上下文切换工作比实际工作多的时候，我们实际上无法从机器或应用程序中获得任何吞吐量。那么我们该怎么办？因为如果我们仍然坚持调度器周期为 100 毫秒


00:13:20

and we end up getting 500 to 1000 threads that we have to schedule, we just said none of this is gonna work. That's a huge loss. So what we're gonna have to do in our scheduler is define another parameter. And what we'll do is we'll define the minimal time slice. In other words, this is the bare minimum time slice,
最终得到了 500 到 1000 个需要调度的线程，我们刚才说过这是行不通的。这将是巨大的损失。所以我们必须在调度器中定义另一个参数。我们将定义最小时间片。换句话说，这是最基本的时间片，


00:13:40

regardless of our scheduler period time, that will allow any thread to at least get some runtime. And maybe what we'll say is 10 milliseconds is that point of diminishing return. We never really want to go below 10 milliseconds of a time slice because once we get below the 10 millisecond time slice our context switches are actually
无论我们的调度器周期时间是多少，都能让任何线程至少获得一些运行时间。我们可能会说 10 毫秒是那个收益递减的点。我们从不真正希望将时间片降到 10 毫秒以下，因为一旦时间片低于 10 毫秒，我们的上下文切换实际上就会


00:14:01

really causing our performance problem like we discussed. But that gets interesting now because if we think about a minimum of a 10 millisecond time slice, remember we were at 100 threads right here, we were at 100 threads, so now, we're never gonna dip below that 10 millisecond. So what does that mean for 100 threads?
就像我们之前讨论的那样，确实会造成性能问题。现在变得有趣了，因为如果我们考虑至少 10 毫秒的时间片，还记得我们这里有 100 个线程吗？我们有 100 个线程，所以现在，我们永远不会低于 10 毫秒。那么对于 100 个线程意味着什么呢？


00:14:21

It means that our scheduler period is no longer gonna be 10 milliseconds over 100 threads, right? It's gonna be what? Like 10 seconds. (whistling) So start thinking about that for a second. Even though we had this scheduler period that gave us this reasonable, reasonable amount of time to create the illusion,
这意味着我们的调度器周期不再是在 100 个线程上的 10 毫秒，对吧？它将变成什么？比如说 10 秒。（吹口哨）所以先思考一下这个。即便我们有这样一个调度器周期，它曾给予我们一个合理的、合理的时间来制造这种幻觉，


00:14:40

once we get to those 100 threads with a minimal time slice of 10 milliseconds, right, now we start realizing that our scheduler period is in the seconds, like 10 seconds to create this illusion. That's not necessarily working for us either right? Now we also gonna start feeling some throughput issues because any given thread might have to wait a total
一旦我们达到 100 个线程，每个线程的时间片只有 10 毫秒，现在我们开始意识到调度器周期可能需要 10 秒钟来创造这种假象。这对我们来说显然是行不通的，对吧？现在我们还会开始感受到吞吐量问题，因为任何给定的线程可能需要等待


00:15:02

of 10 seconds before it even what? Gets to run again. (whistling) All right, you can see how complicated this stuff is. So in this world, it's always gonna be about less is more, less is more. The less threads that we have to schedule during any giving scheduler period
总共 10 秒钟才能再次运行。（吹口哨）好的，你可以看出这是多么复杂的事情。在这个世界里，始终遵循的是"少即是多"的原则。在任何给定的调度器周期中，需要调度的线程越少，


00:15:20

means that each thread's gonna get more time and that thread's gonna be able to come back into play sooner. So we're always needing to balance out this idea. All right, this idea on the operating system side. Now there's another concept that we really do have to understand if you're gonna be a multi-threaded software developer,
就意味着每个线程能获得更多时间，并且能更快地重新投入运行。所以我们始终需要平衡这个思路。好的，这是操作系统层面的概念。现在还有另一个概念，如果你想成为一名多线程软件开发者，必须真正理解，


00:15:41

and that's workload. And there are two types of workloads that we've got to be able to identify early on if we're gonna be making smart engineering decisions here with our scheduler. The first type of workload is called CPU bound. Now, a CPU bound workload is a workload where a thread naturally
这就是工作负载。如果我们要在调度器上做出明智的工程决策，就必须尽早识别出两种类型的工作负载。第一种工作负载称为 CPU 密集型。CPU 密集型工作负载是指线程自然


00:16:01

does not move into a waiting state. It never moves into a waiting state. So an example of a CPU bound workload would be an algorithm that's gonna be counting integers. So imagine I gave you a list of 1 million integerS and I said, hey, count these integer up from beginning to end.
不会进入等待状态。它永远不会进入等待状态。举个例子，CPU 密集型工作负载可能是一个计数整数的算法。想象一下，我给你一个 100 万个整数的列表，并说："嘿，从头到尾把这些整数加起来。"


00:16:20

There is nothing in the processing of adding that would cause the thread to naturally pause or wait for anything. That's a CPU bound workload. What that means is that every thread is gonna get its full time slice all the time. Essentially what I've been describing here is a CPU bound workload where when the A thread gets on the hardware thread,
在执行加法的过程中，没有什么会导致线程自然暂停或等待任何事情。这就是一个 CPU 密集型工作负载。这意味着每个线程都将始终获得其完整的时间片。我一直描述的本质上是一个 CPU 密集型工作负载，当 A 线程进入硬件线程时，


00:16:43

it's gonna get its full-time slice from beginning to end and it won't be switched off until that time slice is over. Now, the opposite of a CPU bound workload is what we would call an I/O bound or blocking workload. And these I/O bound workloads are workloads where the thread never actually uses
它将从头到尾获得其完整的时间片，直到该时间片结束才会被切换。现在，与 CPU 密集型工作负载相反的是我们称之为 I/O 密集型或阻塞型工作负载。这些 I/O 密集型工作负载是指线程实际上从未


00:17:01

its full time slice because at some point within the scope of its time slice, it's gonna make a call to the operating system over the network. It's gonna do something that will cause it to move from a running state into a waiting state. Now, in those situations, even if I had 100 threads, right,
因为在其时间片的某个时刻，它将通过网络向操作系统发起调用。它将执行某些会导致其从运行状态转移到等待状态的操作。现在，即使在这种情况下有 100 个线程，对吧，


00:17:20

or I had 1000 threads, the chances of the scheduler period over 1000 threads in our simulated operating system here getting to 10 seconds is pretty slim because most likely that thread very early on, maybe within its first millisecond or so, will make that call to the operating system maybe to read something over the network
如果我有 1000 个线程，在我们这个模拟的操作系统中，调度器在 1000 个线程上达到 10 秒的可能性是相当低的，因为那个线程很可能在很早的阶段，也许在其第一个毫秒左右，就会向操作系统发出调用，比如读取网络上的某些内容


00:17:40

and immediately it will get context switched out. When it comes to these I/O bound workloads, the context switches actually are our friend, right? When it comes to CPU bound workloads, the context switches are hurting us. Think about that. It's hurting us because we're gonna be taking these 12,000 to 24,000 instruction hits for every context switch.
并且它将立即被上下文切换出去。对于这些 I/O 密集型工作负载，上下文切换实际上是我们的朋友，对吧？当涉及 CPU 密集型工作负载时，上下文切换会对我们造成伤害。想想看。这会伤害我们，因为每次上下文切换我们都要承受 12,000 到 24,000 条指令的开销。


00:18:02

And those instructions could have been work that we otherwise could have been doing, but when it comes to an IO bound workload, the context switches are our friend, because since the thread is going to be stalling out, right, it's gonna go into a waiting state which would keep the hardware thread idle, we can now leverage those 12,000
而这些指令本可以用于实际工作，但对于 I/O 密集型工作负载，上下文切换是我们的朋友，因为线程将会停滞，进入等待状态，这会使硬件线程处于空闲状态，我们现在可以利用这 12,000


00:18:23

to 24,000 instructions to do the context switch to get another thread up and running. So that's why understanding our workload is so important because if it's a CPU bound workload, then we really don't ever want more threads than we have hardware threads
到 24,000 条指令进行上下文切换，让另一个线程运行起来。这就是为什么理解我们的工作负载如此重要，因为如果是 CPU 密集型工作负载，我们真的不希望线程数超过硬件线程数。


00:18:40

because the context switch is hurting us. It's extending that scheduler period out and it's causing that throughput issue the more threads you have. But if it's an I/O bound workload, now these context switches are our friend. They're helping us get more work done faster because we're not allowing the CPU or in this case, the hardware thread, to stay idle.
因为上下文切换正在伤害我们。随着线程数量的增加，它正在延长调度周期并造成吞吐量问题。但如果是一个 I/O 密集型工作负载，这些上下文切换现在反而成为我们的朋友。它们帮助我们更快地完成更多工作，因为我们不会让 CPU 或在这种情况下的硬件线程保持空闲状态。


00:19:02

Now, just as a small side note, you have to understand that our operating system scheduler is gonna be a preemptive scheduler. Now, what does that mean? What it means is that the operating system has to handle events. Think about it. Your hardware is dealing with events all the time.
现在，作为一个小小的旁注，你必须理解我们的操作系统调度器将是一个抢占式调度器。那么，这意味着什么呢？这意味着操作系统必须处理事件。想想看，你的硬件一直在处理事件。


00:19:21

I mean, just the clock, just to keep the clock up to date, there is an event that's occurring on the machine and every time an event occurs on the machine, a thread has to respond to it. So part of our scheduler also is going to have to create a mapping of hardware events to operating system threads
我的意思是，仅仅是时钟，为了保持时钟的更新，就有一个事件正在机器上发生，每当机器上发生一个事件时，一个线程就必须对其作出响应。因此，我们的调度器的一部分还将不得不创建硬件事件到操作系统线程的映射。


00:19:41

and setting certain operating system threads to have a high priority. So even if we were doing a CPU bound workload here, even if we're doing this CPU bound workload, every time the clock has to run, we will have to interrupt that workload, get the thread for the clock to run quickly, do its thing and pull it off.
并且将某些操作系统线程设置为高优先级。即使我们在这里执行的是受 CPU 限制的工作负载，每当时钟需要运行时，都必须中断该工作负载，让时钟线程快速运行，完成其任务后再恢复回来。


00:20:01

Now, I don't want the fact that we have a preemptive scheduler that's event-based to get in the way of our mental models, and we're not going to, we're gonna forget about that. But it does lend something that we do have to understand, and that is scheduling is unpredictable. When all things are equal,
现在，我不希望我们拥有基于事件的抢占式调度器这一事实妨碍我们的思维模型，我们不会让它干扰，我们将忽略它。但它确实带来了一些我们必须理解的东西，那就是调度是不可预测的。在所有条件相同的情况下，


00:20:20

we never really know what the scheduler's going to do, and we're gonna have to keep that in our heads while we design code because no matter what we're doing, especially in multi-threaded software, there has to be moments of guarantees. And it's gonna be our job to deal with synchronization and orchestration. In other words, putting points of guarantees in the code,
我们永远无法真正预知调度器将会做什么，在设计代码时我们必须始终牢记这一点，因为无论我们在做什么，尤其是在多线程软件中，都必须存在一些保证的时刻。我们的任务是处理同步和编排。换言之，就是在代码中设置保证点，


00:20:41

so we can guarantee that the algorithms do run, even if they're executing out of order, they do run correctly. So even though it's a preemptive scheduler, I wanna kind of throw that out. Let's just forget about that right now and we'll just focus on those ideas of CPU bound and I/O bound and what they mean.
以确保算法能够正确运行，即使它们执行顺序不同。所以即便是抢占式调度器，我想先把这一点放在一边。现在让我们专注于 CPU 绑定和 I/O 绑定这些概念及其含义。


00:21:01

All right, so we now understand a little bit about our scheduling period, wanting to create the illusion that all threads are running at the same time. We now understand that there is a point of diminishing return when the time slice gets too small. And that's because our context switch, which is causing us 12,000 to 24,000 instruction losses eventually catch up with us.
好的，现在我们对调度周期有了一些理解，希望创造出所有线程同时运行的假象。我们现在明白了，当时间片变得太小时，就会出现收益递减的情况。这是因为我们的上下文切换最终会导致 12,000 到 24,000 条指令的损失。


00:21:24

So as a scheduler, we're gonna have to tune these numbers. But for our purpose right now, the one to two microsecond latency cost on a context switch is a really good number for us to use. We'd have to really look at what our time slice and scheduler period are for the operating system.
作为一个调度器，我们需要调整这些数值。但就目前而言，上下文切换的一到两微秒延迟成本对我们来说是一个很好的参考数字。我们还需要仔细研究操作系统的时间片和调度周期。


00:21:41

Regardless of what they are, this model is a good mental model to work with. So let's sum up a little bit here by thinking about two algorithms that will help us better understand this. So there's two algorithms that we can play with, our CPU bound one and an I/O bound one. So let's focus on our CPU bound algorithm first.
无论它们是什么，这个模型都是一个很好的思维模型。让我们总结一下，思考两个可以帮助我们更好地理解的算法。我们有两种算法可以探讨，一种是 CPU 密集型的，另一种是 I/O 密集型的。我们先来关注 CPU 密集型算法。


00:22:03

So let's say that I truly did ask you to write an algorithm that can take a collection of numbers. Let's say a million numbers, here it is. Let's draw that collection out. There it is. A big collection of a million numbers, integers,
假设我确实要求你编写一个可以处理一系列数字的算法。比如说，这里有一百万个数字。让我们把这个集合画出来。就是这样。一个包含一百万个整数的大型集合，


00:22:20

and I say to you, I want you to add up every number in this collection and then tell me what the value is. Now, anytime we're gonna be doing anything like this, especially around multi-threaded software, the first thing we need to do is write a sequential version of the algorithm. So writing a sequential version of add basically
然后我对你说，我希望你把这个集合中的每个数字相加，然后告诉我总值是多少。每当我们要做这类事情，尤其是在多线程软件中，我们首先需要做的就是编写算法的顺序版本。所以基本上编写加法的顺序版本


00:22:40

would be about five lines of code, right? We're gonna range over this collection. It's integer based. We'll use our value semantics around our iteration. We'll have a local variable and we'll add into it. So the sequential version just says, start from the beginning, go to the end, five lines of code, and we're done. And now that we have a sequential version,
大概会是五行代码，对吧？我们将遍历这个集合。它是基于整数的。我们将围绕迭代使用值语义。我们将有一个局部变量并将其累加。所以顺序版本只是说，从开头开始，到结尾结束，五行代码，就完成了。现在我们有了顺序版本，


00:23:01

the next question is always going to be, is this work that can be done concurrently? Now, let's talk about that again. Concurrency means out of order execution. So now we can come back and say, does it matter what order I add these integer in? Will that affect the final result?
接下来要问的问题总是：这项工作是否可以并发执行？现在，让我们再次讨论这个问题。并发意味着无序执行。所以现在我们可以回过头来说，加这些整数的顺序是否重要？这会影响最终结果吗？


00:23:22

Now, when it comes to adding a collection of integers, the answer is no. We can do concurrent work here. It doesn't matter what order I add these integer up in, as long as we add them all up. That's really cool. We do have a problem in front of us that can leverage concurrency, right?
当涉及到加一个整数集合时，答案是否定的。我们可以在这里进行并发工作。不管我们以什么顺序相加这些整数，只要最终把它们全部加起来就可以。这真的很酷。我们面前确实有一个可以利用并发的问题，对吧？


00:23:42

One idea could be no problem. I could split the list in half, right? And I can say, let's get one of our operating system threads to add this half. I can get another operating system thread to add that half, out of order, and then we can take that and sum those two values and get that result.
这个想法看起来似乎没问题。我可以将列表一分为二，对吧？然后我可以让操作系统的一个线程处理这一半，再让另一个操作系统线程处理另一半，顺序可以不同，最后将这两个值相加，得到最终结果。


00:24:02

In fact, I could argue that I could break this up in multiple lists and multiple threads, and you may be like, wow, yeah, we can get a bunch of threads, maybe we can get 100 threads, adding small sections of numbers up, and then do the add. That would be brilliant.
事实上，我可以说我可以将它分解成多个列表和多个线程，你可能会想，哇，是的，我们可以获得很多线程，也许可以获得 100 个线程，分别对数字的小部分进行相加，然后再做加法。那将会非常出色。


00:24:20

It could be. But remember, the only reason to add this level of complexity, and trust me, there's complexity here, is because we can get the work done faster. We can get some better throughput. Now, let's go back to the idea of parallelism. Remember, parallelism means executing instructions at the same time, two or more, right?
这是有可能的。但请记住，增加这种复杂性的唯一原因（相信我，这里确实很复杂）是因为我们可以更快地完成工作。我们可以获得更高的吞吐量。现在，让我们回到并行性的概念。还记得吗，并行性意味着同时执行两个或更多条指令，对吧？


00:24:41

It's being able to do work at the same time, right? That's what we're talking about here. So let's go back to our imaginary hardware for a second. Remember, our imaginary hardware is just a single hardware thread. That's it. Which means how many threads can I execute
同时执行工作，对吗？这就是我们现在讨论的内容。让我们暂时回到我们的假想硬件。记住，我们的假想硬件只有一个硬件线程。这意味着在任何给定时刻


00:25:00

at any given time physically? And the answer is one. Only one thread can execute at any given time. So think about this for a second. I have this array of a million integers. Let's say I do break it up into four lists here, and I throw a thread at every list.
我可以物理执行多少个线程？答案是一个。在任何给定时刻只能执行一个线程。那么请想一想。我有一个包含一百万个整数的数组。假设我将它分成四个列表，并为每个列表分配一个线程。


00:25:20

Thread, thread, thread, thread. Question, will running this algorithm sequentially be faster or slower than running it in parallel with four threads when we have a single hardware? Think about that. Because this is CPU bound, and because I can physically
线程，线程，线程，线程。问题是，当我们只有一个硬件时，顺序运行这个算法会比用四个线程并行运行更快还是更慢？想想这个问题。因为这是 CPU 密集型的，并且因为我可以实际


00:25:42

only execute one thread at a time, running the sequential version is going to be faster, because every time we have to swap that thread off the, and it's gonna have to do that four times, right, every time we swap that thread off the hardware, what are we taking?
每次只执行一个线程，运行顺序版本会更快，因为每次我们必须将线程切换出去，而且需要切换四次，对吧？每次将线程切换出硬件时，我们会损失什么？


00:26:00

We're taking that 12,000 instruction loss. There it is. 12,000 instruction losses. And that's to say that that got all that work done within the time slice. If it didn't, we're gonna incur more of these 12,000 instruction losses. And think about it, these are 12,000 instructions that we could have been using to add integers
我们会损失 12,000 条指令。就是这样。12,000 条指令的损失。也就是说，这些工作已经在时间片内完成了。如果没有完成，我们将会产生更多这样的 12,000 条指令损失。想想看，这些是本可以用于整数相加的 12,000 条指令。


00:26:21

that we are now not. So one thing you need to understand here with CPU bound workloads, if we only have one hardware thread, then we really can only run one operating system thread efficiently. But what if I change my hardware? What if I turn my hardware
也就是我们现在无法做到的。关于 CPU 密集型工作负载，你需要理解的是，如果我们只有一个硬件线程，那么我们实际上只能有效地运行一个操作系统线程。但是，如果我改变了我的硬件呢？如果我调整了硬件


00:26:40

into a two hardware thread processor? Here it is. Now how many threads can I run? I can run two threads in parallel. Ah, think about this now. Think about it now. Now, the fact that this is concurrent gets interesting to me because since I can run two threads in parallel,
进入一个双硬件线程处理器？就是这样。那么我可以运行多少线程？我可以并行运行两个线程。啊，现在请仔细想想。现在请仔细想想。现在，这种并发性对我来说变得很有趣，因为既然我可以并行运行两个线程，


00:27:02

I could now break this list up in half, give this thread and this thread its own list, right? They can run in parallel. We could get this work done now at the same time, then we come up and we get our value. Now, if I had four hardware threads, now I could use four operating system threads
现在我可以将这个列表分成两半，给这个线程和那个线程各自一个列表，对吧？它们可以并行运行。我们现在可以同时完成这些工作，然后得到我们的结果。如果我有四个硬件线程，那么我现在可以使用四个操作系统线程


00:27:22

and get it done even faster. So one of the things I want you to recognize here is that when it's a CPU bound workload, if you wanna get more throughput, and the algorithm is concurrent, then you need parallelism, right? This is where I said that sometimes these words blend and sometimes they don't.
并且可以更快地完成任务。因此，我想让你注意的是，对于 CPU 密集型工作负载，如果你想获得更高的吞吐量，并且算法是并发的，那么就需要并行，对吧？这就是我之前说过的，有时这些词会混淆，有时又不会。


00:27:41

Without parallelism, there is no efficiency with concurrency or out-of-order execution because the context switches are hurting us. Yeah, but let's go back to our single hardware thread again. This is it. That's what our hardware looks like. And in this case, let's say that this isn't a list of integers.
没有并行，并发或乱序执行就没有效率，因为上下文切换会损害我们的性能。是的，但让我们再次回到单个硬件线程。就是这样。这就是我们的硬件 looks like。在这种情况下，假设这不是一个整数列表。


00:28:00

No, no, no, no, no. This is a list of URLs, a list of URLs that we want to go fetch and process. What does that mean? This is no longer CPU bound. It is now I/O bound work, which means that when any given thread makes that network call, it's gonna move into a waiting state. Ah, so think about it.
不，不，不，不，不。这是一个网址列表，是我们想要获取和处理的网址列表。这是什么意思？这不再是 CPU 密集型工作。现在是 I/O 密集型工作，这意味着当任何给定线程进行网络调用时，它将进入等待状态。啊，好好想想。


00:28:20

If I build that algorithm sequentially, right, it will have some particular amount of time it takes. But since it's I/O bound, right, what does that mean? It means that I could break this list up on multiple threads, even if I have one hardware thread and get it done faster.
如果我按顺序构建这个算法，它需要一定的执行时间。但由于它是 I/O 密集型的，这意味着什么呢？这意味着即使只有一个硬件线程，我也可以将这个列表拆分到多个线程上，从而更快地完成任务。


00:28:40

Why? Because now the context switches are helping me, right? This thread starts, maybe it gets, you know, one millisecond in and then it makes the network call and it goes into a waiting state. Now what happen? We take our 12,000 instruction hit to pull that thread off and to put this thread on. Up until then,
为什么会这样？因为现在上下文切换在帮助我，对吧？这个线程开始执行，可能运行了一毫秒，然后进行网络调用并进入等待状态。接下来会发生什么？我们需要付出 12,000 条指令的代价来将该线程切出并切入另一个线程。直到那时，


00:29:00

that thing, the hardware would've been idle. So now we're one millisecond in, but guess what? This gets to start running one millisecond in. And now all of these threads are being able to get work done while that processor was going to be idle, because all of these threads said, I don't need time anymore.
如果没有这个机制，硬件本来是处于空闲状态的。现在我们已经过了一毫秒，但是猜怎么着？这些线程可以在一毫秒后开始运行。而现在所有这些线程都能够在本来会空闲的处理器上完成工作，因为所有这些线程都表示它们不再需要时间了。


00:29:21

But here's the interesting part about I/O bound workloads. It's really complicated to figure out what is the most efficient number of threads. In other words, there's still a point of diminishing return if you use two less or diminishing return on two more. Even if you use two less, you're gonna have a problem. You have to find what's called that magic number.
但是关于 I/O 密集型工作负载，有一个有趣的部分。要确定最高效的线程数是非常复杂的。换句话说，无论是减少两个线程还是增加两个线程，都会出现收益递减的情况。即使减少两个线程，也会遇到问题。你必须找到所谓的"最佳数量"。


00:29:41

And really the idea is that is there a magic number where there's only ever one thread really in that runnable state? That's what we're looking for, right? We only have one thread ever in a runnable state staged to go. Then we're gonna have the most efficient number of threads for that I/O bound workload.
实际上，关键是是否存在某个神奇的数字，使得在任何时候只有一个线程处于可运行状态？这就是我们要寻找的，对吧？我们只需要有一个处于可运行状态、准备就绪的线程。这样，对于这种 I/O 密集型工作负载，我们就能拥有最高效的线程数量。


00:30:02

This stuff is very, very complicated. CPU bound workloads are nice, and they're simple and they're really efficient, right? We know that for any CPU bound workload, the number of threads we use equals the number of hardware threads we use. That parallelism is important, but when it comes to I/O bound workloads,
这些内容非常、非常复杂。CPU 密集型工作负载是很好的，它们简单且非常高效，对吧？我们知道对于任何 CPU 密集型工作负载，我们使用的线程数量等于我们使用的硬件线程数量。这种并行性很重要，但当涉及到 I/O 密集型工作负载时，


00:30:21

we don't need parallelism to see improvement with concurrency because the threads can take turns on this hardware right here. And those context switches are helping us, helping us get more work done over time. Again, we don't really know how many. And so when it comes to operating system level stuff like this,
我们不需要并行性就能通过并发看到改进，因为线程可以在这里的硬件上轮流执行。这些上下文切换正在帮助我们，帮助我们随着时间推移完成更多工作。再次强调，我们并不真正知道具体数量。所以当涉及到操作系统层面的这类事情时，


00:30:41

we always tended to use thread pools. We used thread pools to do this. I mean, imagine you were building a web service and you decided to create a operating system thread for every request that came into the server, and you had 50,000 requests coming in. I mean, we were playing with just 100 threads. Imagine 50,000 threads,
我们过去总是倾向于使用线程池。我们使用线程池来处理这个问题。我的意思是，想象你正在构建一个 Web 服务，并决定为每个进入服务器的请求创建一个操作系统线程，而且你有 5 万个请求。我的意思是，我们当时只是玩弄了 100 个线程。想象一下 5 万个线程，


00:31:00

what that problem would cause. It wouldn't work, right? So we would wanna have a pool of threads that we would post work into, and we've gotta find that magic number. We gotta find the number where if we use too many threads, now the context switches are hurting us. We have too many threads in a runnable state, right? If we use too low of a number,
这会造成什么问题。它是行不通的，对吧？所以我们希望有一个线程池，可以往里面提交工作，但我们必须找到那个神奇的数字。我们必须找到一个线程数量，如果使用太多线程，上下文切换就会对我们造成伤害。如果运行状态的线程太多，对吧？如果使用的线程数量太少，


00:31:20

then we're also going to not perform very well, because now we're gonna have more idle time on the processor, 'cause I don't have a thread that's ready to go. These are complicated, complicated problems at the operating system level. Okay. So just to recap a little bit here,
那么我们的性能也不会很好，因为现在处理器上会有更多的空闲时间，因为我没有一个已准备就绪的线程。这些都是操作系统级别的复杂问题。好的，让我们稍微回顾一下。


00:31:41

concurrency means out-of-order execution, right? And parallelism means executing two or more instructions at the same time. We have to know what state of thread is in, and we have to know if our workload is I/O bound or CPU bound. CPU bound workloads mean that threads don't naturally move into waiting states,
并发意味着乱序执行，对吗？而并行则意味着同时执行两个或更多指令。我们必须了解线程的状态，还要知道我们的工作负载是 I/O 密集型还是 CPU 密集型。CPU 密集型工作负载意味着线程不会自然地转入等待状态，


00:32:02

which means that we need parallelism to get any throughput with concurrency. I/O bound workloads mean that threads do naturally move into waiting states. That means that we do not need parallelism, right, for that concurrency to give us throughput, that the context switch is helping us get more work done, even on our single hardware, single-threaded hardware.
这意味着我们需要并行性才能获得并发的吞吐量。I/O 密集型工作负载意味着线程自然地会进入等待状态。这表明对于这种并发，我们不需要并行性就能获得吞吐量，上下文切换可以帮助我们在单一硬件、单线程硬件上完成更多工作。


00:32:23

These are things that we're gonna want to carry on. And just finalizing, remember that CPU bound workloads are the most efficient workloads that we could do on the machine. So the next thing for us to now do is talk about the Go scheduler and how that sits on top of the operating system and some of those mechanical sympathies
这些是我们将要继续进行的事情。最后要记住，CPU 密集型工作负载是我们在机器上可以执行的最高效的工作负载。接下来我们要讨论的是 Go 调度器，以及它是如何建立在操作系统之上的，以及一些机械共情的概念。


00:32:41

that we're gonna need as Go developers to make sure that our algorithms and work are gonna be efficient with the Go scheduler that's sitting on top of the operating system scheduler that's sitting on top of the hardware. (upbeat music)
作为 Go 开发者，我们需要了解这些知识，以确保我们的算法和工作能够高效地与 Go 调度器配合，而 Go 调度器又运行在操作系统调度器之上，操作系统调度器又运行在硬件之上。(活泼的音乐)