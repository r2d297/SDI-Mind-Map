Transcript  抄本

00:00:00

(upbeat music) - [Announcer] Ardan Labs, specializing in high-performance software consulting, training, staffing and development. Welcome to Module 8, goroutines. Let's get started with Lesson 8.1, OS Scheduler Mechanics. - We're about to move into talking about multi-threaded software
（欢快的音乐）-【播报员】Ardan Labs，专注于高性能软件咨询、培训、招聘和开发。欢迎来到第 8 模块，goroutine。让我们从第 8.1 课，操作系统调度器机制开始。- 我们即将开始讨论多线程软件


00:00:20

and I always like starting with the operating system mechanics 'cause they really give us a good understanding and background for how all this multi-threaded software is going to work, even in Go, which is sitting a layer above the operating system. And there's a bunch of terms that we're gonna need to define along the way as well. Like what does concurrency actually mean?
我总是喜欢从操作系统机制开始，因为它们能让我们很好地理解和掌握所有这些多线程软件的工作原理，即使是在位于操作系统之上的 Go 中也是如此。沿途我们还需要定义许多术语。比如并发到底是什么意思？


00:00:40

What does parallelism actually mean? And concurrency, we could start with that right now, means out-of-order execution. That's really the only thing that I want you to keep in your head. The idea that we have a sequence of instructions that we're looking to execute from beginning to end, but we're gonna execute them out of order, still get them all executed
并行到底又是什么意思？我们现在可以先从并发开始讲，它意味着乱序执行。这实际上是我希望你记住的唯一一点。即我们有一系列要从头到尾执行的指令，但我们将以乱序执行它们，同时仍然把它们全部执行完毕


00:01:01

and hopefully get to the same result. So we're always gonna be thinking about out-of-order execution when it comes to concurrency. Parallelism, that means that we're executing two or more instructions at the same time. It's about doing a lot of work at once. And what's interesting is sometimes
并且希望得到相同的结果。所以在谈论并发时，我们总会考虑乱序执行。并行则意味着我们同时执行两个或更多指令。它关乎一次做大量工作。有趣的是，有时


00:01:20

these terms blend into each other, sometimes they're just polar opposites. And we'll figure out when that is as we continue to talk about OS and then Go scheduler mechanics. But let's focus on what we need to know about the operating system. So let's say I was asking you to write an operating system scheduler.
这些术语会相互融合，有时它们则截然相反。随着我们继续讨论操作系统以及 Go 的调度器机制，我们会弄清楚何时是何种情况。但先把注意力放在我们需要了解的操作系统上。假设我让你去实现一个操作系统调度器。


00:01:40

What are the things that you need to kind of consider if you're gonna be doing that sort of engineering? And one of the ideas here that we gotta really cement ourselves in is this idea that we want to create an illusion that a lot of work is happening on the machine at once. In other words, we should be able to run multiple programs, multiple applications at the same time,
如果你要做那种工程，需要考虑哪些方面？这里我们必须真正把一个想法牢牢树立起来：我们要创造一种错觉，让人觉得机器上同时有大量工作在进行。换句话说，我们应该能够同时运行多个程序、多个应用。


00:02:02

and create that illusion that they're all running at the same time. Now, physically, they're not gonna be able to do that. It's all gonna depend on the hardware that we have and we can create some imaginary hardware for this as well as we learn our mental models. So let's start off with a very simple hardware
并制造出它们都在同时运行的错觉。实际上，它们并不能真的同时运行。这完全取决于我们的硬件，我们在学习心智模型时也可以为此构建一些假想的硬件。那我们从一个非常简单的硬件开始吧


00:02:20

where all we have is a single processor and that processor has a single hardware thread. And let's represent that hardware thread as the ability to execute instructions. So every hardware thread that we have in the machine gives us the ability to execute instructions. So if I only have one hardware thread,
在这个硬件上我们只有一个处理器，而该处理器只有一个硬件线程。我们把这个硬件线程表示为执行指令的能力。所以机器中每个硬件线程都赋予了我们执行指令的能力。因此如果我只有一个硬件线程，


00:02:41

then I could only execute one instruction at any given time. If I had two hardware threads, then I could run executions or execute instructions in parallel. You get it? Now, my machine is an eight hardware thread machine. So technically, I can run eight instructions in parallel at any given time.
那么在任何时刻我最多只能执行一条指令。如果我有两个硬件线程，那么我就可以并行运行或并行执行指令。明白了吗？现在，我的机器是一个有八个硬件线程的机器。所以从技术上讲，我在任何给定时间可以并行运行八条指令。


00:03:01

But for now, let's imagine that our hardware is single hardware threaded. Now, that's at the hardware level. We've got to, in our operating system scheduler, leverage this. So what we're gonna do is we're gonna define the idea of an operating system thread. If there's gonna be a hardware thread, we're gonna represent the idea
但现在，假设我们的硬件是单硬件线程的。这是在硬件层面。我们必须在操作系统调度器中利用这一点。所以我们要做的是定义操作系统线程的概念。如果要有硬件线程，我们要去表示这个概念


00:03:20

of an operating system thread, our own thread. And I always want us to think of threads as paths of execution. So our program is gonna be a series of instructions. Those instructions are laid out to execute in sequence and it's the job of the thread, our operating system thread right now, to execute those instructions one at a time,
操作系统线程，我们自己的线程。我希望大家始终把线程看作执行路径。所以我们的程序将是一系列指令。这些指令按顺序排列执行，而线程的工作——此刻是我们的操作系统线程——就是一次执行一条指令，


00:03:41

do the accounting and to leverage this hardware thread to do it. So the operating system is going to execute those instructions in sequence, leveraging the hardware thread that does the actual execution. All right? Now, when we think about these operating system threads, we're gonna have three different states
去做记账并利用这个硬件线程来执行。因此操作系统会按顺序执行那些指令，利用实际执行的硬件线程。明白了吗？现在，当我们考虑这些操作系统线程时，我们会有三种不同的状态


00:04:00

that that operating system thread can be in. And there's a lot more really, like sub states, but remember, we don't have to have full understandings of implementation details here. What we need are good mental models of how things work and behave, and that will help us make better engineering decisions. So there's gonna be three states
该操作系统线程可以处于的状态。实际上还有很多子状态，但记住，我们不需要完全理解实现细节。我们需要的是关于事物如何工作和表现的良好心理模型，这将帮助我们做出更好的工程决策。所以会有三种状态


00:04:21

that a thread can be in. A thread could be in a running state. And when a thread is in a running state, that means we've placed it on this hardware thread right here and it's executing its instructions that it's responsible for. A thread can be in a runable state, and when it's in a runable state, it means that it wants time on that hardware thread.
线程可以处于的状态。线程可以处于运行状态。当线程处于运行状态时，意味着我们把它放在这个硬件线程上，并且它正在执行它负责的指令。线程可以处于可运行状态，当它处于可运行状态时，意味着它想要在那个硬件线程上获得运行时间。


00:04:40

It just has to wait its turn. And then, a thread can be in a waiting state. When a thread's in a waiting state, we really consider it kind of off the radar, right? It's gone and it's waiting for something to happen. It could be waiting for the operating system to come back with a system call. It could be waiting for something on the network to come back in and it's in a waiting state.
它只需要等到轮到它。然后，线程可以处于等待状态。当线程处于等待状态时，我们实际上会认为它有点脱离视线，对吧？它消失了，正在等待某些事情发生。它可能在等待操作系统返回系统调用的结果。也可能在等待网络上的某些响应回来，总之它处于等待状态。


00:05:00

And from our scheduler's point of view, we only care about threads that are running or runable, right? Threads that are waiting, don't put any load on us. They're not our concern, okay? So imagine the following scenario. We have a couple of programs running, which means we have a few threads
从调度器的角度来看，我们只关心处于运行或可运行状态的线程，对吧？处于等待状态的线程不会给我们增加负载，它们不在我们的关注范围内，明白吗？所以想象下面这种场景。我们有几个程序在运行，这意味着我们有一些线程在活动中


00:05:20

that are in play, and the idea is that we want to create this illusion, even with one hardware thread, that all the threads that we have that are either in a running or a runnable state are actually running at the same time. So how could we create this illusion with our scheduler? So one idea is that we can define
并且我们的想法是，即使只有一个硬件线程，也要创造出一种错觉：所有处于运行或可运行状态的线程实际上是同时运行的。那么我们如何通过调度器来创造这种错觉呢？一种想法是我们可以定义


00:05:42

what we'll call a scheduler period. So let's define our scheduler period. Now, the scheduler period, what it's responsible for is our ability to execute any thread that's in a runnable state at the beginning of this period to get that thread to execute within this time.
我们把它称为调度周期。那么让我们先定义一下调度周期。调度周期负责的是：在这个周期开始时处于可运行状态的任何线程，都能在这段时间内获得执行机会。


00:06:02

And if we can do that, then we can create the illusion at least within the scope of the scheduler period that everything's running at the same time. Now, we could play with some, you know, fun numbers here. I'll give you some real numbers for certain things, other numbers, we'd have to really look at our operating system scheduler to see what they are.
如果我们能做到这一点，那么至少在调度周期的范围内，我们就能制造出一种错觉，仿佛所有东西都在同时运行。现在，我们可以玩一些有趣的数值。我会给出一些特定事情的真实数值，其他数值则需要我们深入查看操作系统的调度器来确定。


00:06:21

But we can use some base numbers to get an idea. And let's just say right now that our scheduler period is gonna be, let's just say 100 milliseconds. Let's just say that that's what we're gonna use. Our scheduler period is gonna be 100 milliseconds. So the idea is that what we want is to make sure that every thread that we have in a runable state executes
但我们可以用一些基准数值来形成一个概念。暂且假设我们的调度周期为——我们就说 100 毫秒。就用这个数。我们的调度周期是 100 毫秒。其想法是，我们要确保每一个处于可运行状态的线程都能执行。


00:06:41

within this 100 millisecond timeframe to create the illusion that everything is running at the same time. So let's start off our scheduler. When we do that, and right at the beginning of the scheduler period, what we notice is that we have just one thread in a runnable state. That's all we have.
在这个 100 毫秒的时间范围内创造出一切好像同时运行的错觉。好了，我们开始调度器。当我们这么做时，在调度周期的一开始，我们注意到只有一个线程处于可运行状态。仅此而已。


00:07:00

So if we only have one thread in a runnable state and and our hardware only has that single hardware thread, remember only one thread can physically execute at any given time, then this thread, we'll call this thread A. Thread A is going to get the full 100 milliseconds of time to execute its instructions.
所以如果我们只有一个处于可运行状态的线程，而且我们的硬件实际上也只有那一个硬件线程，记住在任何给定时刻只有一个线程能真正执行，那么我们把这个线程称为线程 A。线程 A 将获得完整的 100 毫秒来执行它的指令。


00:07:20

It gets the full 100 milliseconds. It's brilliant, right? A whole lot of time to do work. And remember some of the numbers that we talked about earlier in the video. We said that every nanosecond of time, remember that, right, every nanosecond of time,
它获得完整的 100 毫秒。这很妙，对吧？有整整一大段时间来做工作。还记得我们在视频前面提到的一些数字。我们说每一纳秒时间，记住这一点，对吧，每一纳秒时间，


00:07:40

one nanosecond of time equals 12 instructions. I want you to remember that number. One nanosecond represents those 12 instructions. Okay, great. So we're gonna keep that number in our head as we continue to go through this exercise. Now, we've got the A goroutine.
一纳秒的时间等于 12 条指令。我希望你记住这个数字。一纳秒代表那 12 条指令。好，我们在接下来做这个练习时会把这个数字记在心里。现在，我们有了 A 协程。


00:08:00

It was in a runnable state before that scheduler period started and now it's off doing its work. Now, the scheduler period is done, and once the scheduler period is done, we go back and we look at how many threads we have in a runnable state. Let's say right now we have two threads in a runnable state. So what does that mean? Well, it means now that we're gonna schedule both threads
在那个调度周期开始之前它处于可运行状态，现在它正在执行它的工作。现在，调度周期结束了，一旦调度周期结束，我们会回去查看有多少线程处于可运行状态。假设现在有两个线程处于可运行状态。这意味着什么呢？这意味着我们现在要在同一个 100 毫秒调度周期内调度两个线程执行


00:08:20

to execute within our same 100 millisecond scheduler period. So we decide to run thread A again, but we know that thread A is only gonna get what, 50 milliseconds this time, which now means that we're gonna schedule that other thread, thread B, to run and thread B is only gonna get 50 milliseconds.
所以我们决定再次运行线程 A，但我们知道线程 A 这次只会得到多少时间，50 毫秒，这现在意味着我们会调度另一个线程，线程 B，运行，而线程 B 也只会得到 50 毫秒。


00:08:42

So let's look at what just happened here. We did create the illusion that two threads ran within the scope of our scheduler period. But if we start looking at what's happening to our A thread, it got 100 milliseconds of runtime the first time, but now it got cut in half. Its throughput across the next 100 milliseconds
所以让我们看看刚才发生了什么。我们确实创造了在调度周期范围内两个线程运行的错觉。但如果我们开始看看 A 线程发生了什么，它第一次得到了 100 毫秒的运行时间，但现在它被减半了。在接下来的 100 毫秒内它的吞吐率...


00:09:02

got cut in half. We're not executing as many instructions as we otherwise did in the previous run. Okay, no problem. Let's keep going. Schedule A period is over. We look again and what do we notice? We notice now that we have five, five threads now
被砍了一半。我们执行的指令不像上次运行那样多。好，没问题，继续。调度周期 A 结束。我们再看，有什么发现？我们现在注意到有五个、五个线程现在


00:09:22

ready to to run in a runable state. So what does that mean? Now it means that we've gotta cut this down again, right? And so this time, what is thread A gonna get? Thread A is only gonna get what? It's only gonna get 20 milliseconds this time. So now, thread A is gonna get 20 milliseconds. We now know that thread B
处于可运行状态。那么这意味着什么？现在意味着我们必须再次把它缩减，对吧？所以这次，线程 A 会得到什么？线程 A 这次只会得到什么？这次它只会得到 20 毫秒。所以现在，线程 A 将获得 20 毫秒。我们现在知道线程 B


00:09:41

that we had is gonna get its 20 milliseconds. 20 milliseconds for thread B. And then what are we gonna do with that remaining 60 milliseconds here, right? The remaining 60 milliseconds now is gonna go across those other threads, C, D and E, right? That's gonna be the remainder of that 60 milliseconds of time.
会得到它的 20 毫秒。线程 B 得到 20 毫秒。然后我们要怎么处理剩下的那 60 毫秒，对吧？剩下的 60 毫秒现在会分配给其他那些线程，C、D 和 E，对吧？那将是那 60 毫秒时间的剩余部分。


00:10:01

And I want you to notice again that every time more threads show up to be run within this scheduler period, the time starts to get smaller and smaller and smaller, right? If eventually we had 100 threads that wanted to run within this scheduler period, we had 100 threads, we're now at the point
我还想让你注意，每次在这个调度周期内出现更多要运行的线程时，可分配的时间就会越来越少，对吧？如果最终有 100 个线程想在这个调度周期内运行，假设我们有 100 个线程，我们现在就到了这种情况


00:10:21

where this thread right here, thread A, is gonna be down to what? One millisecond of time, one millisecond of runtime. And what that means is that at some point there's gonna be a diminishing return on the time a given thread really gets to do any work.
这条线程，也就是线程 A，在这里将会减少到多少？一毫秒的时间，一毫秒的运行时间。这意味着在某个时候，某个线程真正能做工作的时间会出现收益递减。


00:10:41

And it's mainly because there's a cost here that I haven't touched upon, and that is the context switch cost. Now, think about this for a second. We have thread A and thread A is coming in and says, okay, I want time on this hardware thread. So we go in here and we place A on the hardware thread
这主要是因为这里有一个我还没提到的成本，那就是上下文切换成本。现在，想一想这件事。我们有线程 A，线程 A 进来并说，好吧，我想在这个硬件线程上运行。于是我们把 A 放到这个硬件线程上


00:11:01

and it's doing its work for that 100 milliseconds. And now we decide, okay, now thread B, thread B is gonna run for its, let's say, one millisecond. Well, we've got to take some time to pull this thread off the hardware, right, and then we've gotta put this thread on the hardware.
它在那儿工作了那 100 毫秒。现在我们决定，好吧，现在线程 B，要运行它的，比如说，一毫秒。好吧，我们得花一些时间把这个线程从硬件上取下来，对吧，然后我们得把这个线程放到硬件上。


00:11:22

I mean, that's not free. That's going to take some time. This is what we call a context switch. Taking one thread off, putting another thread on. Now, on average, on average at the operating system level, a context switch like this is gonna be anywhere from one millisecond to two milliseconds.
我的意思是，这不是免费的。这会花费一些时间。这就是我们所说的上下文切换。把一个线程移下去，把另一个线程放上来。现在，在操作系统层面上，平均来说，这样的上下文切换大约在一到两毫秒之间。


00:11:43

In other words, 1000 nanoseconds to 2000 nanoseconds. Let's start doing the math again. Remember, a nanosecond of time represents 12 instructions. So what are we looking at here
换句话说，1000 纳秒到 2000 纳秒。我们再开始算一下。记住，一纳秒的时间代表 12 条指令。那么我们在这里谈论的是什么


00:12:00

when we talk about a one to two millisecond context switch? What we're talking about here really is a 12,000 to 24,000 instruction loss, right? Instructions we otherwise could have been executing, but we can't because of this context switch.
当我们谈论一到两毫秒的上下文切换时？我们真正谈论的是 12,000 到 24,000 条指令的损失，对吧？原本我们可以执行的指令，却因为这个上下文切换而不能执行。


00:12:22

So, think about where we're at. If you have this many threads context switching at one millisecond, or even worse, what if this gets down to 1000 threads? Oh my goodness, 1000 threads. Now we're talking about microseconds, right? Microseconds of time that a thread gets
所以，想想我们现在处于什么情况。如果有这么多线程在每一毫秒发生上下文切换，或者更糟糕的是，如果这下降到 1000 个线程？天哪，1000 个线程。现在我们谈论的是微秒，对吧？线程获得的执行时间是以微秒计的


00:12:42

to execute on top of the one to two microseconds of context switch. What eventually happens is that you're doing more context switch work than you are actual work. And this is not good. So there's a point of diminishing return
再加上那一到两微秒的上下文切换时间。最终发生的情况是，你花在上下文切换上的时间超过了实际做工作的时间。这不是好事。所以会有一个收益递减的点


00:13:00

where that time slice gets to a point where, and the number of threads where you're doing more context switch work than actual work, and we're not really getting any throughput from the machine or our apps. So what are we going to do, because if we just stick with a scheduler period of 100 milliseconds
当时间片变到某个程度，以及线程数量达到某个程度时，你做的上下文切换工作比实际工作更多，机器或我们的应用并没有得到任何吞吐量提升。那么我们该怎么办，因为如果我们只是坚持使用 100 毫秒的调度器周期


00:13:20

and we end up getting 500 to 1000 threads that we have to schedule, we just said none of this is gonna work. That's a huge loss. So what we're gonna have to do in our scheduler is define another parameter. And what we'll do is we'll define the minimal time slice. In other words, this is the bare minimum time slice,
我们最终会得到 500 到 1000 个需要调度的线程，这样一来我们刚才说的所有方法都行不通了。这是一个巨大的损失。所以在调度器中我们不得不定义另一个参数。我们要做的是定义最小时间片。换句话说，这就是最小允许的时间片，


00:13:40

regardless of our scheduler period time, that will allow any thread to at least get some runtime. And maybe what we'll say is 10 milliseconds is that point of diminishing return. We never really want to go below 10 milliseconds of a time slice because once we get below the 10 millisecond time slice our context switches are actually
不管我们的调度周期时间是多少，这都能让任何线程至少获得一些运行时间。也许我们会说 10 毫秒就是那个收益递减点。我们其实永远不想把时间片降到低于 10 毫秒，因为一旦低于 10 毫秒时间片，我们的上下文切换实际上会...


00:14:01

really causing our performance problem like we discussed. But that gets interesting now because if we think about a minimum of a 10 millisecond time slice, remember we were at 100 threads right here, we were at 100 threads, so now, we're never gonna dip below that 10 millisecond. So what does that mean for 100 threads?
真正造成我们性能问题的正是我们讨论的那些。但事情变得有趣，因为如果我们考虑至少 10 毫秒的时间片，记住我们这里有 100 个线程，处于 100 个线程的状态，所以现在我们永远不会低于那个 10 毫秒。那么对 100 个线程来说这意味着什么？


00:14:21

It means that our scheduler period is no longer gonna be 10 milliseconds over 100 threads, right? It's gonna be what? Like 10 seconds. (whistling) So start thinking about that for a second. Even though we had this scheduler period that gave us this reasonable, reasonable amount of time to create the illusion,
这意味着我们的调度器周期不再是针对 100 个线程的 10 毫秒，对吧？会变成什么？像 10 秒。（口哨声）所以想一想这个问题。尽管我们有这个调度器周期，给了我们创建“幻觉”的一个相当合理的时间量，


00:14:40

once we get to those 100 threads with a minimal time slice of 10 milliseconds, right, now we start realizing that our scheduler period is in the seconds, like 10 seconds to create this illusion. That's not necessarily working for us either right? Now we also gonna start feeling some throughput issues because any given thread might have to wait a total
一旦我们达到了那 100 个线程并且最小时间片是 10 毫秒，对吧，现在我们开始意识到我们的调度器周期是以秒为单位的，像 10 秒来创建这个“幻觉”。这对我们来说也不一定可行，对吧？现在我们还会开始感受到一些吞吐量问题，因为任何给定的线程可能必须总共等待


00:15:02

of 10 seconds before it even what? Gets to run again. (whistling) All right, you can see how complicated this stuff is. So in this world, it's always gonna be about less is more, less is more. The less threads that we have to schedule during any giving scheduler period
10 秒才能再次做什么？得以运行。（口哨声）好吧，你可以看到这些事情有多复杂。所以在这个世界里，总是“少即是多，少即是多”。在任何给定的调度器周期内，我们需要调度的线程越少，...


00:15:20

means that each thread's gonna get more time and that thread's gonna be able to come back into play sooner. So we're always needing to balance out this idea. All right, this idea on the operating system side. Now there's another concept that we really do have to understand if you're gonna be a multi-threaded software developer,
意味着每个线程将获得更多时间，并且该线程能够更快地重新投入运行。所以我们始终需要平衡这个想法。好，这是操作系统方面的这个概念。现在还有另一个概念，如果你要成为一个多线程软件开发者，确实必须理解，


00:15:41

and that's workload. And there are two types of workloads that we've got to be able to identify early on if we're gonna be making smart engineering decisions here with our scheduler. The first type of workload is called CPU bound. Now, a CPU bound workload is a workload where a thread naturally
那就是工作负载。我们必须能够尽早识别两种类型的工作负载，这样在为调度器做出明智的工程决策时才有依据。第一种工作负载称为 CPU bound（CPU 密集型）。CPU bound 工作负载是指一个线程在自然情况下


00:16:01

does not move into a waiting state. It never moves into a waiting state. So an example of a CPU bound workload would be an algorithm that's gonna be counting integers. So imagine I gave you a list of 1 million integerS and I said, hey, count these integer up from beginning to end.
不会进入等待状态。它永远不会进入等待状态。一个 CPU 密集型工作负载的例子是一个会一直进行整数计数的算法。想象我给你一份包含 100 万个整数的列表，然后我说，嘿，从头到尾把这些整数数一遍。


00:16:20

There is nothing in the processing of adding that would cause the thread to naturally pause or wait for anything. That's a CPU bound workload. What that means is that every thread is gonna get its full time slice all the time. Essentially what I've been describing here is a CPU bound workload where when the A thread gets on the hardware thread,
在执行加法处理时不会导致线程自然暂停或等待任何东西。这就是 CPU bound 工作负载。这意味着每个线程将始终获得它的完整时间片。本质上我在这里描述的是一种 CPU bound 工作负载，当 A 线程占用硬件线程时，


00:16:43

it's gonna get its full-time slice from beginning to end and it won't be switched off until that time slice is over. Now, the opposite of a CPU bound workload is what we would call an I/O bound or blocking workload. And these I/O bound workloads are workloads where the thread never actually uses
它将从头到尾获得完整的时间片，并且在该时间片结束之前不会被切换掉。现在，CPU 限制的工作负载的相反就是我们所说的 I/O 限制或阻塞型工作负载。这类 I/O 限制的工作负载是指线程从未真正使用完


00:17:01

its full time slice because at some point within the scope of its time slice, it's gonna make a call to the operating system over the network. It's gonna do something that will cause it to move from a running state into a waiting state. Now, in those situations, even if I had 100 threads, right,
它的完整时间片，因为在其时间片的某个时刻，它会向操作系统或通过网络发出调用。它会做一些导致其从运行状态转为等待状态的事情。现在，在这些情况下，即便我有 100 个线程，嗯，


00:17:20

or I had 1000 threads, the chances of the scheduler period over 1000 threads in our simulated operating system here getting to 10 seconds is pretty slim because most likely that thread very early on, maybe within its first millisecond or so, will make that call to the operating system maybe to read something over the network
或者我有 1000 个线程，在我们这里模拟的操作系统中，调度器在 1000 个线程上轮询到十秒的概率非常低，因为很可能那个线程在很早的时候，可能在它的第一个毫秒左右，就会向操作系统发出调用，比如去通过网络读取某些东西


00:17:40

and immediately it will get context switched out. When it comes to these I/O bound workloads, the context switches actually are our friend, right? When it comes to CPU bound workloads, the context switches are hurting us. Think about that. It's hurting us because we're gonna be taking these 12,000 to 24,000 instruction hits for every context switch.
然后它会立即被切换出去。对于这些 I/O 密集型工作负载，上下文切换实际上是我们的朋友，对吧？对于 CPU 密集型工作负载，上下文切换会伤害我们。想一想，这是有害的，因为我们每次上下文切换都要付出大约 12,000 到 24,000 条指令的代价。


00:18:02

And those instructions could have been work that we otherwise could have been doing, but when it comes to an IO bound workload, the context switches are our friend, because since the thread is going to be stalling out, right, it's gonna go into a waiting state which would keep the hardware thread idle, we can now leverage those 12,000
而那些指令本来可能是我们可以用来做其他工作的，但对于 I/O 密集型工作负载来说，上下文切换是我们的朋友，因为线程会发生阻塞，会进入等待状态，使硬件线程闲置，我们现在可以利用那大约 12,000 条指令


00:18:23

to 24,000 instructions to do the context switch to get another thread up and running. So that's why understanding our workload is so important because if it's a CPU bound workload, then we really don't ever want more threads than we have hardware threads
进行上下文切换并让另一个线程开始运行，大约需要 24,000 条指令。理解我们的工作负载因此非常重要，因为如果是 CPU 密集型的工作负载，我们就真的不希望线程数量超过硬件线程数量


00:18:40

because the context switch is hurting us. It's extending that scheduler period out and it's causing that throughput issue the more threads you have. But if it's an I/O bound workload, now these context switches are our friend. They're helping us get more work done faster because we're not allowing the CPU or in this case, the hardware thread, to stay idle.
因为上下文切换会损害性能。它会拉长调度周期，线程越多就越会导致吞吐量问题。但如果是 I/O 密集型的工作负载，这些上下文切换反而对我们有利。它们能帮助我们更快完成更多工作，因为我们不会让 CPU，或者在这个例子里，硬件线程保持空闲。


00:19:02

Now, just as a small side note, you have to understand that our operating system scheduler is gonna be a preemptive scheduler. Now, what does that mean? What it means is that the operating system has to handle events. Think about it. Your hardware is dealing with events all the time.
现在，作为一个小的旁注，你必须理解我们的操作系统调度器将是抢占式调度器。那这是什么意思？意思是操作系统必须处理各种事件。想一想，你的硬件一直在处理事件。


00:19:21

I mean, just the clock, just to keep the clock up to date, there is an event that's occurring on the machine and every time an event occurs on the machine, a thread has to respond to it. So part of our scheduler also is going to have to create a mapping of hardware events to operating system threads
我的意思是，仅仅是时钟，为了保持时钟更新，机器上会发生一个事件，每次机器上发生事件时，线程都必须对它作出响应。因此我们的调度器的一部分也需要创建从硬件事件到操作系统线程的映射。


00:19:41

and setting certain operating system threads to have a high priority. So even if we were doing a CPU bound workload here, even if we're doing this CPU bound workload, every time the clock has to run, we will have to interrupt that workload, get the thread for the clock to run quickly, do its thing and pull it off.
并为某些操作系统线程设置较高的优先级。所以即使我们在这里做的是 CPU 限制的工作负载，即使我们在做这个 CPU 限制的工作负载，每当时钟需要运行时，我们也必须中断该工作负载，让时钟的线程快速运行，完成它的任务然后把它拉下来。


00:20:01

Now, I don't want the fact that we have a preemptive scheduler that's event-based to get in the way of our mental models, and we're not going to, we're gonna forget about that. But it does lend something that we do have to understand, and that is scheduling is unpredictable. When all things are equal,
现在，我不希望我们因为调度器是基于事件的抢占式而干扰我们的思维模型，所以我们要暂时忘掉这一点。但这确实带来一个我们必须理解的事实，那就是调度是不可预测的。在所有条件相同的情况下，


00:20:20

we never really know what the scheduler's going to do, and we're gonna have to keep that in our heads while we design code because no matter what we're doing, especially in multi-threaded software, there has to be moments of guarantees. And it's gonna be our job to deal with synchronization and orchestration. In other words, putting points of guarantees in the code,
我们从来不知道调度器会做什么，我们在设计代码时必须记住这一点，因为无论我们在做什么，特别是在多线程软件中，都必须存在某些保证的时刻。处理同步和协调将是我们的工作。换句话说，就是在代码中放置保证点，


00:20:41

so we can guarantee that the algorithms do run, even if they're executing out of order, they do run correctly. So even though it's a preemptive scheduler, I wanna kind of throw that out. Let's just forget about that right now and we'll just focus on those ideas of CPU bound and I/O bound and what they mean.
所以我们可以保证这些算法确实会运行，即使它们是乱序执行的，它们也会正确运行。尽管它是一个可抢占的调度器，我想先把这一点放到一边。现在我们先忘掉它，专注于那些关于 CPU 密集型和 I/O 密集型以及它们的含义的概念。


00:21:01

All right, so we now understand a little bit about our scheduling period, wanting to create the illusion that all threads are running at the same time. We now understand that there is a point of diminishing return when the time slice gets too small. And that's because our context switch, which is causing us 12,000 to 24,000 instruction losses eventually catch up with us.
好了，所以我们现在对调度周期有了一些了解，知道它试图制造所有线程同时运行的错觉。我们也明白当时间片太小时会出现收益递减的点。那是因为我们的上下文切换导致我们损失的 12,000 到 24,000 条指令最终会赶上我们。


00:21:24

So as a scheduler, we're gonna have to tune these numbers. But for our purpose right now, the one to two microsecond latency cost on a context switch is a really good number for us to use. We'd have to really look at what our time slice and scheduler period are for the operating system.
作为调度器，我们需要调整这些参数。但就目前而言，切换上下文时每次一到两微秒的延迟代价对我们来说是一个很好的参考值。我们还需要仔细查看操作系统的时间片和调度周期是多少。


00:21:41

Regardless of what they are, this model is a good mental model to work with. So let's sum up a little bit here by thinking about two algorithms that will help us better understand this. So there's two algorithms that we can play with, our CPU bound one and an I/O bound one. So let's focus on our CPU bound algorithm first.
不管它们具体是什么，这个模型是一个很好的思维模型。所以我们通过两个算法来总结一下，帮助我们更好地理解。这有两个算法可以供我们试验：一个是 CPU 密集型，另一个是 I/O 密集型。我们先把注意力放在 CPU 密集型算法上。


00:22:03

So let's say that I truly did ask you to write an algorithm that can take a collection of numbers. Let's say a million numbers, here it is. Let's draw that collection out. There it is. A big collection of a million numbers, integers,
假设我真的让你写一个算法，能够接受一组数字。比如说一百万个数字，就在这里。我们把这组集合画出来。就是它。一大堆一百万个整数的集合，


00:22:20

and I say to you, I want you to add up every number in this collection and then tell me what the value is. Now, anytime we're gonna be doing anything like this, especially around multi-threaded software, the first thing we need to do is write a sequential version of the algorithm. So writing a sequential version of add basically
然后我对你说，我要你把这个集合里的每个数字都加起来，然后告诉我结果是多少。现在，任何时候我们要做这种事情，尤其是在多线程软件中，第一件事就是先编写算法的顺序（串行）版本。所以编写一个顺序版本的 add 基本上...


00:22:40

would be about five lines of code, right? We're gonna range over this collection. It's integer based. We'll use our value semantics around our iteration. We'll have a local variable and we'll add into it. So the sequential version just says, start from the beginning, go to the end, five lines of code, and we're done. And now that we have a sequential version,
大约五行代码，对吧？我们会对这个集合进行 range。它是基于整数的。我们会在迭代中使用值语义。会有一个局部变量并向它累加。因此顺序版本只需说，从开始到结束，五行代码，然后完成。现在我们有了顺序版本，


00:23:01

the next question is always going to be, is this work that can be done concurrently? Now, let's talk about that again. Concurrency means out of order execution. So now we can come back and say, does it matter what order I add these integer in? Will that affect the final result?
下一个问题总是：这项工作能并发完成吗？再说一次，并发意味着乱序执行。所以现在我们可以回过头来问，我以什么顺序把这些整数相加重要吗？那会影响最终结果吗？


00:23:22

Now, when it comes to adding a collection of integers, the answer is no. We can do concurrent work here. It doesn't matter what order I add these integer up in, as long as we add them all up. That's really cool. We do have a problem in front of us that can leverage concurrency, right?
就把一组整数相加而言，答案是否定的。这里可以做并发工作。只要把它们都加起来，顺序并不重要。这很酷。我们确实面临一个可以利用并发的问题，对吧？


00:23:42

One idea could be no problem. I could split the list in half, right? And I can say, let's get one of our operating system threads to add this half. I can get another operating system thread to add that half, out of order, and then we can take that and sum those two values and get that result.
一个想法可能没问题。我可以把列表一分为二，对吧？我可以让我们的一个操作系统线程去加这一半，另一个操作系统线程去加那一半，顺序可以不一样，然后我们再把这两个值相加得到结果。


00:24:02

In fact, I could argue that I could break this up in multiple lists and multiple threads, and you may be like, wow, yeah, we can get a bunch of threads, maybe we can get 100 threads, adding small sections of numbers up, and then do the add. That would be brilliant.
事实上，我可以说我可以把它分成多个列表和多个线程，你可能会想，哇，是的，我们可以弄很多线程，也许可以弄 100 个线程，分别加小段数字，然后再做汇总。那会很棒。


00:24:20

It could be. But remember, the only reason to add this level of complexity, and trust me, there's complexity here, is because we can get the work done faster. We can get some better throughput. Now, let's go back to the idea of parallelism. Remember, parallelism means executing instructions at the same time, two or more, right?
可能是这样。但请记住，添加这种复杂性的唯一理由，而且相信我，这里确实有复杂性，是因为我们可以更快地完成工作。我们可以获得更好的吞吐量。现在，让我们回到并行性的概念。记住，并行性意味着同时执行指令，两个或更多，对吧？


00:24:41

It's being able to do work at the same time, right? That's what we're talking about here. So let's go back to our imaginary hardware for a second. Remember, our imaginary hardware is just a single hardware thread. That's it. Which means how many threads can I execute
就是能够同时做工作，对吧？这就是我们在这里讨论的。所以让我们回到我们想象中的硬件。记住，我们想象中的硬件只是单个硬件线程。仅此而已。这意味着我能执行多少个线程


00:25:00

at any given time physically? And the answer is one. Only one thread can execute at any given time. So think about this for a second. I have this array of a million integers. Let's say I do break it up into four lists here, and I throw a thread at every list.
在任意时刻物理上能运行多少个线程？答案是一个。在任意时刻只能有一个线程在执行。想想这个。我有这个包含一百万个整数的数组。假设我把它分成四个子列表，然后为每个子列表都派一个线程。


00:25:20

Thread, thread, thread, thread. Question, will running this algorithm sequentially be faster or slower than running it in parallel with four threads when we have a single hardware? Think about that. Because this is CPU bound, and because I can physically
线程、线程、线程、线程。问题是：当只有单个硬件时，把这个算法顺序执行会比用四个线程并行执行更快还是更慢？好好想想。因为这是 CPU 密集型，并且因为我物理上能...


00:25:42

only execute one thread at a time, running the sequential version is going to be faster, because every time we have to swap that thread off the, and it's gonna have to do that four times, right, every time we swap that thread off the hardware, what are we taking?
只执行一个线程时，运行顺序版本会更快，因为每次我们都得把那个线程从硬件上换下去，而且这得做四次，对吧？每次我们把线程从硬件上换下时，会有什么开销？


00:26:00

We're taking that 12,000 instruction loss. There it is. 12,000 instruction losses. And that's to say that that got all that work done within the time slice. If it didn't, we're gonna incur more of these 12,000 instruction losses. And think about it, these are 12,000 instructions that we could have been using to add integers
我们要承担那 12,000 条指令的损失。看到了吧。12,000 条指令的损失。这意味着那些工作都是在时间片内完成的。如果没完成，我们就会产生更多这样的 12,000 条指令损失。想想看，这些本可以用来做整数相加的 12,000 条指令


00:26:21

that we are now not. So one thing you need to understand here with CPU bound workloads, if we only have one hardware thread, then we really can only run one operating system thread efficiently. But what if I change my hardware? What if I turn my hardware
现在却没被用上。因此，在 CPU 绑定的工作负载下，你需要理解的一点是：如果我们只有一个硬件线程，那么实际上我们只能高效地运行一个操作系统线程。但如果我更换我的硬件呢？如果我把硬件


00:26:40

into a two hardware thread processor? Here it is. Now how many threads can I run? I can run two threads in parallel. Ah, think about this now. Think about it now. Now, the fact that this is concurrent gets interesting to me because since I can run two threads in parallel,
换成一个双硬件线程的处理器呢？就像现在这样。现在我可以并行运行多少个线程？我可以并行运行两个线程。啊，想想现在。现在，这种并发对我来说变得有趣了，因为既然我可以并行运行两个线程，


00:27:02

I could now break this list up in half, give this thread and this thread its own list, right? They can run in parallel. We could get this work done now at the same time, then we come up and we get our value. Now, if I had four hardware threads, now I could use four operating system threads
我现在可以把这个列表一分为二，给这条线程和那条线程各自一半对吧？它们可以并行运行。我们现在可以同时完成这些工作，然后再汇总得到我们的值。现在，如果我有四个硬件线程，我就可以使用四个操作系统线程


00:27:22

and get it done even faster. So one of the things I want you to recognize here is that when it's a CPU bound workload, if you wanna get more throughput, and the algorithm is concurrent, then you need parallelism, right? This is where I said that sometimes these words blend and sometimes they don't.
并且更快完成。所以我要你认识到的一点是，当工作负载受限于 CPU 时，如果你想获得更高的吞吐量，并且算法是并发的，那么你就需要并行，对吧？这就是我所说的有时这些词会混淆，有时又不会的情况。


00:27:41

Without parallelism, there is no efficiency with concurrency or out-of-order execution because the context switches are hurting us. Yeah, but let's go back to our single hardware thread again. This is it. That's what our hardware looks like. And in this case, let's say that this isn't a list of integers.
没有并行，单靠并发或乱序执行是无法高效的，因为上下文切换会拖慢我们。好，我们回到那单个硬件线程。就是这个。这就是我们的硬件长这样。在这种情况下，假设这不是一串整数。


00:28:00

No, no, no, no, no. This is a list of URLs, a list of URLs that we want to go fetch and process. What does that mean? This is no longer CPU bound. It is now I/O bound work, which means that when any given thread makes that network call, it's gonna move into a waiting state. Ah, so think about it.
不，不，不，不，不。这是一串 URL，一串我们想去抓取并处理的 URL。这意味着什么？这不再是受 CPU 限制的工作了。它现在是 I/O 绑定的工作，这意味着当任一线程发起网络调用时，它会进入等待状态。啊，所以想想看。


00:28:20

If I build that algorithm sequentially, right, it will have some particular amount of time it takes. But since it's I/O bound, right, what does that mean? It means that I could break this list up on multiple threads, even if I have one hardware thread and get it done faster.
如果我按顺序构建那个算法，对吧，它会花费一定的时间。但既然它是 I/O 绑定的，这意味着什么？意味着即使我只有一个硬件线程，我也可以把这个列表拆分到多条线程上，从而更快完成。


00:28:40

Why? Because now the context switches are helping me, right? This thread starts, maybe it gets, you know, one millisecond in and then it makes the network call and it goes into a waiting state. Now what happen? We take our 12,000 instruction hit to pull that thread off and to put this thread on. Up until then,
为什么？因为现在上下文切换在帮我，对吧？这个线程开始运行，可能只运行了一毫秒，然后它发起了网络调用并进入等待状态。现在发生了什么？我们为了把这个线程切出去并把这个线程调入，付出了 12,000 条指令的代价。在那之前，


00:29:00

that thing, the hardware would've been idle. So now we're one millisecond in, but guess what? This gets to start running one millisecond in. And now all of these threads are being able to get work done while that processor was going to be idle, because all of these threads said, I don't need time anymore.
硬件本来会是空闲的。所以现在我们已经运行到一毫秒，但你猜怎么着？这个线程可以在一毫秒时开始运行。现在所有这些线程都能在处理器本来会空闲的时候做工作，因为所有这些线程都说，我现在不需要运行时间了。


00:29:21

But here's the interesting part about I/O bound workloads. It's really complicated to figure out what is the most efficient number of threads. In other words, there's still a point of diminishing return if you use two less or diminishing return on two more. Even if you use two less, you're gonna have a problem. You have to find what's called that magic number.
但关于 I/O 受限的工作负载，有趣的部分是：要弄清最有效的线程数到底是多少，真的很复杂。换句话说，如果你少用两个或多用两个，仍然会出现收益递减的情况。即使你少用两个，也会有问题。你必须找到所谓的那个“魔术数字”。


00:29:41

And really the idea is that is there a magic number where there's only ever one thread really in that runnable state? That's what we're looking for, right? We only have one thread ever in a runnable state staged to go. Then we're gonna have the most efficient number of threads for that I/O bound workload.
真正的想法是，是否存在一个“神奇数字”，使得在可运行状态下的线程永远只有一个？这就是我们要寻找的，对吧？我们希望始终只有一个线程处于可运行并已准备好执行的状态。这样对于那种以 I/O 为主的工作负载，我们将得到最有效的线程数。


00:30:02

This stuff is very, very complicated. CPU bound workloads are nice, and they're simple and they're really efficient, right? We know that for any CPU bound workload, the number of threads we use equals the number of hardware threads we use. That parallelism is important, but when it comes to I/O bound workloads,
这些东西非常非常复杂。CPU 绑定的工作负载很友好，简单且效率非常高，对吗？我们知道对于任何 CPU 绑定的工作负载，我们使用的线程数等于硬件线程数。那种并行性很重要，但对于 I/O 绑定的工作负载来说，


00:30:21

we don't need parallelism to see improvement with concurrency because the threads can take turns on this hardware right here. And those context switches are helping us, helping us get more work done over time. Again, we don't really know how many. And so when it comes to operating system level stuff like this,
我们不需要并行性也能通过并发看到性能提升，因为线程可以在这块硬件上轮流运行。那些上下文切换在帮助我们，随着时间推移帮助我们完成更多工作。再说一次，我们并不确切知道数量。所以当涉及到像这样的操作系统级别的东西时，


00:30:41

we always tended to use thread pools. We used thread pools to do this. I mean, imagine you were building a web service and you decided to create a operating system thread for every request that came into the server, and you had 50,000 requests coming in. I mean, we were playing with just 100 threads. Imagine 50,000 threads,
我们总是倾向于使用线程池。我们用线程池来做这件事。也就是说，想象你在构建一个 Web 服务，你决定为每一个到达服务器的请求创建一个操作系统线程，而有 50,000 个请求进来。我们的实验只是用 100 个线程。想想看 50,000 个线程会怎样，


00:31:00

what that problem would cause. It wouldn't work, right? So we would wanna have a pool of threads that we would post work into, and we've gotta find that magic number. We gotta find the number where if we use too many threads, now the context switches are hurting us. We have too many threads in a runnable state, right? If we use too low of a number,
会引发什么问题。它行不通，对吧？所以我们会想要有一个线程池，把工作投递进去，而且我们必须找到那个魔法数字。我们得找到这样一个线程数，如果用得太多，线程切换会对我们造成伤害。我们有太多线程处于可运行状态，对吧？如果我们使用的线程数太少，


00:31:20

then we're also going to not perform very well, because now we're gonna have more idle time on the processor, 'cause I don't have a thread that's ready to go. These are complicated, complicated problems at the operating system level. Okay. So just to recap a little bit here,
那么性能也不会很好，因为处理器上会有更多空闲时间，因为没有可立即运行的线程。这些是在操作系统层面上复杂、复杂的问题。好了，总结一下，


00:31:41

concurrency means out-of-order execution, right? And parallelism means executing two or more instructions at the same time. We have to know what state of thread is in, and we have to know if our workload is I/O bound or CPU bound. CPU bound workloads mean that threads don't naturally move into waiting states,
并发意思是无序执行，对吧？而并行意味着同时执行两个或更多指令。我们必须知道线程处于什么状态，还要知道我们的工作负载是 I/O 绑定还是 CPU 绑定。CPU 绑定的工作负载意味着线程不会自然进入等待状态，


00:32:02

which means that we need parallelism to get any throughput with concurrency. I/O bound workloads mean that threads do naturally move into waiting states. That means that we do not need parallelism, right, for that concurrency to give us throughput, that the context switch is helping us get more work done, even on our single hardware, single-threaded hardware.
这意味着我们需要并行性才能在并发下获得任何吞吐量。I/O 绑定的工作负载意味着线程会自然进入等待状态。这表示我们不需要并行性，对吧，那个上下文切换就能让并发为我们带来吞吐量，即便在单个硬件、单线程的硬件上，上下文切换也能帮助我们完成更多工作。


00:32:23

These are things that we're gonna want to carry on. And just finalizing, remember that CPU bound workloads are the most efficient workloads that we could do on the machine. So the next thing for us to now do is talk about the Go scheduler and how that sits on top of the operating system and some of those mechanical sympathies
这些都是我们需要持续关注的内容。最后总结一下，记住 CPU 绑定的工作负载是在机器上最有效率的工作负载。接下来我们要讨论的是 Go 调度器，以及它如何运行在操作系统之上和一些相关的机械性细节。


00:32:41

that we're gonna need as Go developers to make sure that our algorithms and work are gonna be efficient with the Go scheduler that's sitting on top of the operating system scheduler that's sitting on top of the hardware. (upbeat music)
作为 Go 开发者，我们需要掌握这些内容，以确保在运行于操作系统调度器之上、又运行于硬件之上的 Go 调度器上，我们的算法和工作能够高效运行。(欢快的音乐)