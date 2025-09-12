Transcript  抄本

00:00:02

- [Presenter] Arden Labs, (pensive music) specializing in high performance software consulting, training, staffing and development. (graphics whirring) Module eight, Go routines. You are now watching lesson 8.2, "Go Scheduler Mechanics." (graphics whirring) - With the operating system mechanics in place with understanding concurrency and workloads,
- [Presenter] Arden Labs，（沉思的音乐）专注于高性能软件咨询、培训、人员配置和开发。（图形嗡鸣）第八模块，Go routines。您现在正在观看第 8.2 课，“Go 调度器机制”。（图形嗡鸣）- 在操作系统机制到位并理解并发和工作负载之后，


00:00:21

now it's time to learn about how the Go Scheduler semantics work and how it sits on top of the operating system. So when your Go program starts up, what the runtime is gonna do is try to identify how many hardware threads you have on that host machine. I've got eight hardware threads on my machine,
现在是时候了解 Go 调度器的语义如何工作以及它如何位于操作系统之上。所以当你的 Go 程序启动时，runtime 会尝试识别宿主机器上有多少硬件线程。我的机器上有八个硬件线程，


00:00:41

so that means that when any program starts up on my laptop here, I'm gonna be getting eight of these logical processors, one per hardware thread on that machine. And every logical processor is given a real live operating system thread,
所以这意味着当任何程序在我的笔记本上启动时，我会得到八个这样的逻辑处理器，每个硬件线程对应一个。每个逻辑处理器都会被赋予一个真实存在的操作系统线程，


00:01:00

exactly what we had talked about, and that operating system thread will execute on the hardware and remember the operating system is still responsible for making sure that those operating system threads get on the hardware. And then we have one more thing, which is the Go routine. Now the Go routine is an application level thread.
正是我们之前讨论过的那样，该操作系统线程会在硬件上执行，记住操作系统仍然负责确保这些操作系统线程能够运行在硬件上。然后我们还有一项，就是 Go routine。现在 Go routine 是一种应用层线程。


00:01:22

So remember what we have here, we have our app layer thread, we have our operating system level thread, and then we've got our hardware level thread. We've got these three layers that are all working together and we're really a layer of indirection away from the hardware. We talked about how those operating system threads work,
所以记住我们这里有什么：我们的应用层线程、我们的操作系统级线程，以及我们的硬件级线程。我们有这三层在协同工作，而我们实际上距离硬件只有一层间接层。我们已经讨论了那些操作系统线程是如何工作的，


00:01:43

we talked earlier about how they have stacks, Go routine, have stacks. Operating system threads can operate in one of three states, they can be waiting, running, or runnable, guess what? Go routines can be waiting, running, or runnable. From my perspective, that Go routine or application level thread
我们之前讨论过它们有栈，Go routine 有栈。操作系统线程可以处于三种状态之一：waiting（等待）、running（运行）或 runnable（可运行）。猜猜看？Go routine 也可以是 waiting、running 或 runnable。在我看来，那个 Go routine 或应用程序级线程


00:02:00

is almost identical to those behaviors that the operating system threads have. The only difference, the really, the only difference is that that Go doesn't have priorities and one of the reasons Go routines don't have priorities is because we're not dealing with events up in our application space. The operating system has to deal with events, we don't.
几乎与操作系统线程的那些行为完全相同。唯一的不同，真正唯一的不同是 Go 没有优先级，而 Go 协程没有优先级的原因之一是我们在应用层不处理事件。操作系统必须处理事件，而我们不需要。


00:02:22

So everything we've talked about applies at the Go scheduler level, even though we're a layer above the operating system, except for those priorities, which is great because again, they're not really gonna make us necessarily a better Go developer. So here we are, this is our model, the P, the M, the G,
所以我们讨论的所有内容都适用于 Go 调度器层面，即使我们是在操作系统之上的一层，除了那些优先级，因为那并不会真正让我们成为更好的 Go 开发者。这很棒。所以这里是我们的模型，P、M、G，


00:02:43

with an M for every hardware thread. Now what I'm doing is I'm showing you a single threaded Go program now, like the Go playground. Now another thing about this scheduler is that we consider it to be a cooperating scheduler,
每个硬件线程对应一个 M。现在我展示的是一个单线程的 Go 程序，就像 Go playground。关于这个调度器的另一点是，我们把它看作是一个协作式调度器，


00:03:00

which means that we need events that are occurring at the application level to perform scheduling. But these aren't like hardware events that are happening in this like preemptive mode where we're not really sure, because this is a cooperating scheduler, what this means is that we've gotta find safe points
这意味着我们需要在应用级别发生的事件来执行调度。但这些并不像在抢占式模式下发生的硬件事件——在那种模式下我们并不完全确定，因为这是一个协作式调度器——这就意味着我们必须找到安全点


00:03:22

in the code that we can yield these Go routines on and off that M, that's what we're looking for. So the job of the scheduler is to behave like the operating system scheduler and that there are time slices and that there are events, but our events have to occur at safe points
在代码中我们可以在这些 Go 协程（goroutine）与 M 之间切换，这是我们要的。因此调度器的工作就是表现得像操作系统的调度器，存在时间片和事件，但我们的事件必须在安全点发生


00:03:40

and right now today, with Go, and at least in 1.11, that these safe points happen during function call transitions. So we're waiting for these function call transitions to occur in Go. Now they're looking at in 1.12 and maybe 1.13, but at least they're looking at 1.12,
而在现在的 Go（至少在 1.11）中，这些安全点发生在函数调用转换期间。所以我们要等待这些函数调用转换在 Go 中发生。现在他们在考虑在 1.12 甚至可能 1.13 中做这件事，但至少是在看 1.12。


00:04:01

to add some preemptive techniques to the scheduler to make it a little bit more random, similar to the way the OS works. But for now today as we're talking that Go scheduler is a cooperative scheduler, that means Go routines have to yield their time and instead of asking developers to call yield,
为调度器增加一些抢占技术，让它变得更随机一些，类似操作系统的工作方式。但就目前我们讨论的来说，Go 的调度器是协作式的，这意味着 Go routine 必须主动让出自己的时间，而不是要求开发者去调用 yield，


00:04:22

the Go scheduler is the one that's calling yield on behalf of those Go routines. Again, under the idea that there's a minimal time slice and all that good stuff. So let's take a look at that here. Now there are really four classes of events that can occur with function call transitions
Go 调度器会代表这些 Goroutine 调用 yield。仍然基于最小时间片等假设。我们来看看这里。实际上有四类事件会在函数调用转换时发生


00:04:41

that give the scheduler an opportunity to make a context switch. We've got the keyword Go, anytime we've got a Go routine that we're gonna be creating, there it is. And in fact, when we create Go routines, there's actually two more data structures here. Every P has a local run queue
从而给调度器提供进行上下文切换的机会。我们有关键字 Go，每当我们要创建一个 Goroutine，就会用到它。实际上，当我们创建 Goroutine 时，还有另外两个数据结构。每个 P 都有一个本地运行队列


00:05:02

and that's gonna be for Go routines in that runnable state, so if we use the key word Go in front of a function call, we're gonna end up with more Go routines, Go routines in a runnable state will end up in some local run queue, Go routines that are executing right there on the M and there's actually another data structure
那将是处于 runnable 状态的 goroutine，所以如果我们在函数调用前使用关键字 Go，就会产生更多 goroutine。处于 runnable 状态的 goroutine 会进入某个本地运行队列，正在 M（机器线程）上执行的 goroutine 就在那里，还有另外一个数据结构


00:05:21

called the global run queue, which is another queue of Go routines that are in a runnable state but haven't been assigned to a P yet. So there's Go. A garbage collection, anytime the garbage collector runs, there's gonna be a lot of chaos here and you're gonna see a lot of scheduling happening.
被称为全局运行队列，这是另一个保存处于可运行状态但尚未分配到任何 P 的 Go 协程的队列。所以就是 Go。当垃圾回收运行时，这里会有很多混乱，你会看到大量的调度发生。


00:05:40

We're gonna see that when we get into some tracing later on. System calls, anytime there's a system call that occurs, we're gonna be making system calls quite a bit. There's lots of system calls that are gonna happen, you're logging, you're producing output, you're hitting the network. Almost anything you do outside of your app
系统调用，任何发生系统调用的时刻，我们都会相当频繁地进行系统调用。会有许多系统调用发生，比如日志记录、产生输出、访问网络。几乎你在应用外做的任何事情都会触发系统调用。


00:06:00

is gonna be a system call in Go and that's gonna give the scheduler an opportunity to make a scheduling decision. Remember, these are opportunities, it doesn't have to happen, there's still minimal time slices, there's still moments where we've gotta get into these safe points, but there are opportunities for the scheduler to yield Go routines on and off that M. By the way, taking a Go routine on and off the M
将会在 Go 中触发一次系统调用，这会给调度器提供做出调度决策的机会。记住，这些只是机会，不一定会发生，仍然存在最小时间片，仍然有时刻我们必须进入这些安全点，但这些机会允许调度器把 Go routine 在该 M 上切换下去或切换上来。顺便说一下，把一个 Go routine 从 M 上切下或切上


00:06:24

is what we call a context switch in Go. Remember the context switch at the operating system was one to two microseconds, 1000 to 2000 nanoseconds, here in Go that same context switch, that's gonna be roughly 200 nanoseconds, so about 200.
这就是我们所说的 Go 中的上下文切换。记住操作系统中的上下文切换大约是 1 到 2 微秒，即 1000 到 2000 纳秒，而在 Go 中，相同的上下文切换大约是 200 纳秒左右，大约是 200。


00:06:44

So a significant difference in the context switch, that's gonna help us too at the Go level. So we're gonna go from like 2000 to 200, really great. System calls and there's two types of system calls, there are asynchronous and synchronous system calls,
所以在上下文切换方面有显著差异，这也会在 Go 级别上帮助我们。所以我们会从大约 2000 降到 200，效果非常好。系统调用有两类：异步和同步系统调用，


00:07:04

we're gonna have to learn how to do that. Now the last one, we got the use of the Go, we got garbage collection, we got system calls and there are other types of blocking calls that are gonna happen in your software. In multi-threaded software,
我们需要学习如何处理这些。最后一点，我们已经讨论了 Go 的使用、垃圾回收、系统调用，软件中还会发生其他类型的阻塞调用。在多线程软件中，


00:07:20

these blocking calls could be synchronization and orchestration, mutexes, atomic instructions. You also have potentially C-Go issues, C-Go is the C compiler for Go. So you can call into C libraries and in cases where we've got C functions that could be blocking that M,
这些阻塞调用可能是同步和编排相关的，比如互斥锁、原子指令。你也可能遇到 C-Go 问题，C-Go 是 Go 的 C 编译器接口。你可以调用 C 库，在某些情况下，如果我们有可能会阻塞的 C 函数，那 M，


00:07:40

we've gotta be able to detect that. So we'll talk about that as well. So we've got our four classes of events that are occurring at the scheduler that give the scheduler an opportunity. The two interesting ones, really, are the system calls and those blocking calls, so let's go a little deeper into how those work. So GO has something that's called the network polar.
我们必须能够检测到这一点。我们也会讨论这一点。现在有四类在调度器发生的事件，它们为调度器提供了机会。真正有趣的两个事件是系统调用和那些阻塞调用，所以让我们更深入地看看它们是如何工作的。GO 有一个叫做 network poller 的东西。


00:08:03

And the network polar starts out with a single thread and EPOL or K event on the Mac an IOCP on the windows, those kind of thread pooling technologies, that's what's being used here with the network polar
network poller 从单个线程和 EPOL（在 Mac 上是 Kevent，在 Windows 上是 IOCP）开始，那些线程池技术就是这里使用的，这就是 network poller 的工作原理。


00:08:21

and the network polar's job is to handle asynchronous system calls, asynchronous system calls. And we call it the network polar really because the only asynchronous system call we really work with today are the networking calls. All three operating systems have excellent support
network poller 的工作是处理异步系统调用，异步系统调用。我们之所以把它称为 network poller，实际上是因为目前我们真正使用的唯一异步系统调用是网络调用。所有三个操作系统对这种异步网络都有很好的支持，


00:08:41

for that asynchronous networking, excellent support. Unfortunately the operating systems, except for Windows, doesn't have strong support for file IO in an asynchronous way. So anytime we're doing file IO, we're gonna be using those synchronous system calls when we're doing networking,
对异步网络有很好的支持。不幸的是，除 Windows 外，操作系统对以异步方式进行文件 IO 的支持并不强。因此每当我们进行文件 IO 时，我们将使用那些同步系统调用，而在进行网络时，


00:09:00

luckily because the real bulk of the work we do is over the network, we're gonna be leveraging a synchronous system calls and the network polar. So let's run a quick scenario here with the network polar and our asynchronous system calls. Let's say right now this Go routine, what it's doing is it's going to be wanting to perform
幸运的是，因为我们实际执行的大部分工作都是通过网络进行的，所以我们将利用同步系统调用和网络极点（network polar）。现在让我们用网络极点和我们的异步系统调用运行一个快速场景。假设此时这个 Go 协程正在做的是，它将想要执行


00:09:22

a read operation, there it is, it's gonna perform a read on the network. So as soon as that happens, what the schedule is gonna do is gonna say, no problem. Since you're about to perform a read, we're gonna take you off this M and we're gonna put you right here on the network polar,
一次读取操作，就在那里，它会对网络执行一次读取。 所以一旦发生这种情况，调度器会这样做：没问题。既然你要执行读取，我们就把你从这个 M 上摘下来，然后把你放到网络轮询（network poll）那里。


00:09:40

we're gonna issue that asynchronous system call and you're gonna wait here 'til the operating system can complete that read operation. Now what's brilliant about that is we've taken the G off of this M, we've moved it onto essentially another M or a pool of M's over here, which frees up the M to do more work. So now the scheduler can come in,
我们会发出那个异步系统调用，然后你会在这里等待，直到操作系统完成那个读取操作。现在精彩的地方在于我们把 G 从这个 M 上移走了，本质上把它移动到另一个 M 或者这边的 M 池上，这释放了该 M 去做更多工作。所以现在调度器可以进来，


00:10:02

choose another Go routine from the local run queue for that P and we can start getting some more work done. Remember that's that 200 nanosecond contact switch, but it's helping us here, because that M gets to stay busy doing more work. Now once that system call is complete,
从该 P 的本地运行队列中选择另一个 Go routine，我们就可以开始做更多工作。记住那 200 纳秒的上下文切换，但它在这里对我们有帮助，因为那个 M 可以保持忙碌去做更多工作。现在一旦系统调用完成，


00:10:20

we'll take that Go routine off the network polar, we'll bring it back into the local run queue and we can start all of that again. Really great workflow here, because we're efficiently using the threads that we have. But what if this read call wasn't a network call, it was file IO?
我们会把那个 Go routine 从网络轮换队列中取回，把它放回本地运行队列，然后我们可以重新开始所有这些。这里的工作流程非常棒，因为我们高效利用了现有的线程。但如果这个 read 调用不是网络调用，而是文件 IO 呢？


00:10:41

Now we got a little bit more complication, we can't use the network polar anymore, might as well not even be there. So what are we going to do? Because the last thing we want is this Go routine to block this M. If this Go routine makes a read call to open up a file, which is gonna take a minimum of a few microseconds of time,
现在情况更复杂了，我们不能再使用那个 network poller 了，甚至可以说它根本不存在。那么我们该怎么办？因为我们最不希望的就是这个 goroutine 阻塞这个 M。如果这个 goroutine 发起一次读取文件的调用，而那至少会花费几个微秒的时间，


00:11:02

a minimum of a few microseconds of time, well we're not getting any work done during that blocking. We don't want that. So what the schedule is gonna do is identify that this Go routine's about to do some file IO read and it will take this M and it'll take this G
至少会花费几个微秒的时间，那么在那段阻塞期间我们就无法做任何工作。我们不希望这样。所以调度器要做的是识别出这个 goroutine 即将进行一些文件 IO 读取操作，然后它会拿走这个 M，并把这个 G


00:11:20

and it will detach it off that P and there it is right there, that Go routine now blocks that original M right over here on the side. We move it off, but now we're still not getting any extra work done. So what's gonna happen? Well we're gonna bring in a brand new M. Now if we've already have an M that's parked, brilliant,
从那个 P 上分离出来，就像这样，现在那个 Go routine 就把原来的 M 在旁边阻塞住了。我们把它移开了，但现在我们仍然没有获得额外的工作。那么会发生什么呢？我们会引入一个全新的 M。如果我们已经有一个被停放的 M，那就太好了，


00:11:42

we'll just bring it in and we'll get it going, but if we don't, we'll have to create one. And now what we can do is take another G off the Q and get it running. So we're still able to get a lot of work done here, it's just that we have to create a new thread, in this case to make that happen.
我们就把它拉进来并让它开始运行，但如果我们没有，就得创建一个。现在我们可以把另一个 G 从队列中取出来并让它运行。所以我们仍然能完成很多工作，只是我们必须创建一个新的线程，在这个例子中为了实现那点。


00:12:01

What happens once that Go routine system call is complete? Well, once that's complete we're gonna take this G off that M, we're gonna put it back into the local run queue and now what we're gonna do is park this M over on the side when we have to do it again. The chance that this Go routine is doing the same sort of read work is pretty good,
一旦那个 goroutine 的系统调用完成会发生什么？一旦完成，我们会把这个 G 从那个 M 上拿下来，把它放回本地运行队列，现在我们会在一旁把这个 M 停放起来，等我们需要再次使用它时再调用。这个 goroutine 还在做相同类型的读取工作的可能性相当大，


00:12:22

so we'll see that whole transition happen again. Now what if this Go routine is doing some other sort of blocking work? What if like with the C library, remember something about Go, when Go first got released about eight years ago,
所以我们会看到整个转换再次发生。现在如果这个 goroutine 在执行其他类型的阻塞工作会怎样？比如像使用 C 库，记得 Go 吗，当 Go 大约八年前首次发布时，


00:12:42

we had a great standard library, but a bulk of the third party libraries that are out today like Kafka for example, wasn't there. We needed to rely on a lot of the C library support early on in Go to be able to write programs. And since Go manages memory in its runtime, C isn't part of the runtime.
我们有一个很棒的标准库，但现在大多数第三方库，比如 Kafka，当时并不存在。早期我们需要依赖很多 C 库支持来编写程序。由于 Go 在其运行时管理内存，C 并不是运行时的一部分。


00:13:02

These are also decisions that had to be made on an engineering side. So the problem is is that as soon as we call into a C function, we're kind of out of our managed state. So how does the Go scheduler know that a Go routine making a C function call isn't now gonna be blocked for a long period of time?
这些也是工程上必须做出的决策。所以问题在于，一旦我们调用一个 C 函数，我们就脱离了受管状态。那么 Go 调度器如何知道一个正在调用 C 函数的 goroutine 不会在很长一段时间内被阻塞呢？


00:13:22

Well there's another thing that's part of the scheduler, called the system monitor. And the system monitor is monitoring these Go routines and the work that they're doing. So let's say what's happening is this Go routine's making a read call, but it's from some sort of C library. What the system monitor's gonna be able to do
调度器还有另一个组成部分，叫做系统监视器。系统监视器会监视这些 goroutine 及其正在执行的工作。比如说，某个 goroutine 正在进行一个读取调用，但这是来自某个 C 库。系统监视器能够做的是


00:13:40

is look to see how long it's been since that Go routine is executed at instruction. And it's a little bit of an interesting algorithm, but for our purposes right now, 20 nanoseconds is that base time period of inactivity. So essentially if the system monitor notices that this Go routine has been inactive for 20 nanoseconds,
查看自该 goroutine 上次执行指令以来已经过去了多长时间。这个算法有点有趣，但就我们目前的用途而言，20 纳秒是判定不活动的基本时间周期。所以实质上，如果系统监视器注意到该 goroutine 已经 20 纳秒没有活动，


00:14:03

it's going to assume that it's blocked and then we're gonna go through the same exact cycle that you saw before. We're gonna move that M two off with the Go routine that's making the C call that's blocked. We're gonna bring another M in and then we're gonna be able to pull another Go routine
它会假定它被阻塞，然后我们会经历你之前看到的完全相同的循环。我们会把那个执行被阻塞的调用 C 的 Go 协程所占用的 M 移走。我们会把另一个 M 拉进来，然后我们就能调度出另一个 Go 协程。


00:14:23

from that local run queue and keep things going. So when the system monitor identifies that something is stalled for about 20 nanoseconds, it's the same kind of activity that we saw with synchronous system calls. The goal is to keep those Go routines running
从本地运行队列中拿出并保持运行。所以当系统监视器发现某个东西大约停滞了 20 纳秒时，这与我们在同步系统调用中看到的活动类型相同。目标是保持这些 goroutine 运行。


00:14:41

that are in a runnable state and ideally the asynchronous system calls give us the most efficiency, because we're not creating and parking new threads, we're leveraging the operating system threads that are there. It's one of the reasons that Go is so fast, so fast with its networking, 'cause we're leveraging
这些处于可运行状态，并且理想情况下异步系统调用为我们提供了最高的效率，因为我们并不是在创建并挂起新的线程，而是在利用已经存在的操作系统线程。这也是 Go 在性能上，尤其是网络方面如此迅速的原因之一，因为我们在利用


00:15:00

those asynchronous system calls really effectively. Let's kind of take a look at everything that we've now done and sum up some of the efficiencies that we're gonna get from this programming model. And another really cool efficiency actually when we think about it is when we start
那些异步系统调用确实非常有效。现在让我们回顾一下已经完成的所有工作，并总结一下我们将从这种编程模型中获得的一些效率提升。还有一个非常酷的效率，实际上当我们开始考虑时会发现，……


00:15:20

dealing with running Go routines in parallel. So we've been demonstrating a single threaded Go program. Look at what I have now, now I've got a multi-threaded Go program, there it is. I've got two Ps, two threads, each thread on its own hardware thread,
处理并行运行的 Go 协程。所以我们一直在演示单线程的 Go 程序。看看我现在的情况，现在我有了一个多线程的 Go 程序，就在这里。我有两个 P，两个线程，每个线程在它自己的硬件线程上运行，


00:15:41

Now these Go routines, this one and this one can run in parallel. I now have two Go routines executing instructions on two operating system threads with two operating systems threads running on two hardware threads, now we're able to run Go routines in parallel. Again, we have to think about our workloads.
现在这些 Go 协程，这个和那个可以并行运行。我现在有两个 Go 协程在两个操作系统线程上执行指令，两个操作系统线程运行在两个硬件线程上，现在我们能够并行运行 Go 协程。再次强调，我们必须考虑我们的工作负载。


00:16:01

IO bound and CPU are blocking, IO bound and CPU bound, but this is what we're gonna have. Now another interesting thing here when we've got these Ps is that the Go scheduler is also a work stealing scheduler. Think about this right now, I've got two Go routines running in parallel,
IO 受限和 CPU 受限，IO 受限和 CPU 受限，但这就是我们将要面对的情况。现在当我们有这些 P 时，另一个有趣的事情是 Go 调度器也是一个工作窃取调度器。现在想想这个，我有两个并行运行的 Go 协程，


00:16:20

I've got three Go routines in Q here, I've got one Go routine in here and let's even imagine that I've got two Go routines in the global run queue, in the global run queue, they haven't been assigned to a P yet. So imagine this scenario. Suddenly the P over here on the right, this P finishes all of its work.
这里的运行队列 Q 中有三个 Go 协程，这里有一个 Go 协程，甚至假设我在全局运行队列中有两个 Go 协程，它们还没有被分配给任何 P。想象这样的场景。突然右边这个 P 完成了它的所有工作。


00:16:40

There is no more work for this P to do, what's gonna happen? Well Go is a work stealing scheduler as well. We have this CPU capacity here, but it's not being leveraged and we want to use it. So there's a little algorithm around work stealing and part of the algorithm says, go see if there's another P with a lot of work in it
这个 P 已经没有更多工作要做了，会发生什么？Go 的调度器也有工作窃取机制。我们这里有 CPU 容量，但它没有被利用，而我们想要利用它。所以有一个关于工作窃取的小算法，算法的一部分是：去看看是否有另一个 P 有大量工作在排队


00:17:02

and if there is, steal half the work that it has. In this case, this is a P that has four Go routines. So quite possibly what that P might do is steal half of the Go routines here, put one in Q and start executing the other one, work stealing.
如果有，就窃取它一半的工作。在这个例子中，这是一个有四个 Go routine 的 P。所以那个 P 很可能会窃取其中一半的 Go routine，把一个放到 Q 中并开始执行另一个，进行工作窃取。


00:17:20

We will definitely do some of that. And when that's happening, when the work stealing is happening, what we say is that M is now spinning. Remember the last thing we want is this M to fall into a waiting state, 'cause then it'll be pulled off that hardware and we're not gonna be able to execute Go routines as quickly as we otherwise could. Now imagine if this P suddenly finishes its work,
我们肯定会做一些这样的事情。当工作窃取发生时，我们说 M 现在处于自旋状态。记住我们最不希望的就是这个 M 进入等待状态，因为那样它会从硬件上被移走，我们就不能像本来那样快速地执行 Go routine。现在想象如果这个 P 突然完成了它的工作，


00:17:44

now it's got no work to do. Maybe it wants to steal some work out of this P, but there really isn't a lot. Another part of the algorithm says, you know what? Another place you can look is the global run queue. In this case, there are two Go routines in the global run queue. Most likely this P is gonna come in,
现在它没有工作可做。也许它想从这个 P 中偷一些工作，但实际上并没有太多。算法的另一部分说，你知道吗？你还可以看一下全局运行队列。在这种情况下，全局运行队列中有两个 Go 协程。很可能这个 P 会进来，


00:18:01

steal work from the global run queue now and we'll get that work going as well. So work stealing is a big part of the scheduler, especially as we start to have the ability to run Go routines in parallel. Alright, with that in place, let's do a small little exercise to kind of see the real sympathies here
现在从全局运行队列中窃取工作，我们也会把那些工作启动起来。因此，工作窃取是调度器的重要部分，特别是当我们开始能够并行运行 Go 协程时。好了，有了这些，让我们做一个小练习，来看看我们从 Go 调度器获得的真实“同情”是什么样的，


00:18:22

that we're getting from the Go scheduler, sitting on top of the operating system scheduler, sitting on top of hardware threads. Alright, now let's start with a multi-threaded program at the operating system level and what we're gonna do is create two operating system threads,
它位于操作系统调度器之上，操作系统调度器又位于硬件线程之上。好，现在让我们从操作系统级别的多线程程序开始，我们要做的是创建两个操作系统线程，


00:18:41

here's thread one and thread two, two operating system threads, maybe this is a program written in C and what these threads are gonna be doing is passing messages back and forth. It's not important how they're doing it, what's important is that this is IO bound work. So we're waiting for some sort of context switch to get into that executing or running state
这是线程一和线程二，两个操作系统线程，可能这是用 C 写的程序，这些线程要做的是来回传递消息。实现方式并不重要，重要的是这是 I/O 绑定的工作。所以我们在等待某种上下文切换以进入执行或运行状态。


00:19:02

and then we're gonna do a little bit of work and then we're gonna send that message across to the other thread. Now, when we send the message across to the other thread, we're gonna context switch off, because we're no longer gonna be running, we're now gonna move into that waiting state. We move into a waiting state, we come off the core.
然后我们会做一点工作，然后把那条消息发送到另一个线程。现在，当我们把消息发送到另一个线程时，我们会发生上下文切换，因为我们不再运行，我们现在会进入等待状态。我们进入等待状态，离开了核。


00:19:20

Let's say that we're on core one. Now when that message shows up on the other end, there'll be an event to let that know, then we're gonna have a context switch, we're gonna move from that waiting state to a running state. Then we're gonna need that context switch to move into an executing state, we're gonna pick the message up, we're gonna do some work,
假设我们在核一上。现在当那条消息在另一端出现时，会有一个事件通知到那边，然后我们会发生一次上下文切换，我们会从等待状态转为运行状态。接着我们需要那次上下文切换进入执行状态，我们会取出消息，做一些工作，


00:19:42

we're gonna send that message back, we're gonna move into that waiting state again. Now we're gonna get an event on this side. We're gonna go from that waiting to running, then we're gonna go into that executing state and we're gonna do this and we're gonna do it again. Every time this thread passes a message back and forth,
我们会把那条消息发回去，我们会再次进入等待状态。现在这边会收到一个事件。我们会从等待转为运行，然后进入执行状态，我们会做这个操作，然后再做一次。每次这个线程来回传递消息，


00:20:01

we're gonna have context switches. Maybe this was also on core two, maybe this ends up being on core three. We're also gonna be bouncing cores, because we don't really know which core is idle at any given time. So you could see that with this IO bound workload, we've got context switches going from waiting to running to executing.
我们会发生上下文切换。也许这也发生在核心二上，也许最终在核心三上。我们也会在核心之间跳转，因为我们并不知道在任何给定时间哪个核心是空闲的。因此你可以看到在这个以 IO 为主的工作负载下，我们有从等待到运行再到执行的上下文切换。


00:20:21

We're doing a little bit of work, we're passing messages, we're moving around, we're bouncing around course. Okay, good, let's switch over now to the Go scheduler. When we use the Go scheduler, this diagram actually is gonna stay the same, but I'm gonna add just a couple of little changes to it. Let's change these from T's now to G's
我们在做一点工作，传递消息，四处移动，来回在核心间跳跃。好，现在切换到 Go 调度器。当我们使用 Go 调度器时，这个图实际上保持不变，但我会对它做一些小改动。我们把这些从 T 改成 G。


00:20:41

to represent that Go routine. Go routine one and Go routine two. And let's also do something interesting here. Let's set up just a single P with a single M, running on a single hardware thread, let's just say that's running on core one. Now if I do all of that, the only thing that changes
来表示那个 Go routine。Go routine 一号 和 Go routine 二号。我们这里也做点有趣的事。我们只设置一个 P 和一个 M，在单个硬件线程上运行，假设它在核心一上运行。现在如果我这样做，唯一改变的就是


00:21:00

is what core we're running on, because we know that we're only gonna be running on core one. But what's interesting is that this is IO bound work, so the rest of the diagram stays the same, because the Go routines have to transition in the same state as those operating system threads did.
是我们运行在哪个核心，因为我们知道我们只会在核心一上运行。但有趣的是，这是 IO 受限的工作，所以图的其余部分保持不变，因为 Go 协程必须以与那些操作系统线程相同的状态转换。


00:21:20

The only real difference here is that instead of these context switches taking one to two microseconds, they're now only taking roughly the 200 nanoseconds. We just went from 1000 to 2000 nanoseconds down to about 200, because the context switches are happening here
这里唯一真正的区别是，这些上下文切换不再花费一到两微秒，而是现在大约只需 200 纳秒。我们刚刚从大约 1000 到 2000 纳秒降到了大约 200 纳秒，因为上下文切换发生在这里


00:21:41

on the thread, they're not happening on the hardware. If you step back and look at this a little bit more, what you're gonna see is really where the magic is. Because what Go has really done is that it's turned aisle bound work into CPU bound work
在线程上，而不是在硬件上。如果你退一步多看一下，你会真正看到魔法所在。因为 Go 做的事情实际上是把走道受限（aisle bound）的工作在操作系统层面变成了 CPU 受限的工作


00:22:01

at the operating system level. Take a look at this again, the context switches are absolutely happening. They're happening in our application level, on the thread. From the operating system's point of view, this M is always running, always in an executing or running state, always, always!
再看一遍，上下文切换确实在发生。它们发生在我们的应用层，在线程上。从操作系统的角度来看，这个 M 始终在运行，始终处于执行或运行状态，总是，总是！


00:22:24

From an operating systems point of view, we are doing CPU bound work, even though it's really IO bound and this is one of the reasons why we don't need more threads in our Go programs and we have hardware threads, because the scheduler is converting all of the work that we do,
从操作系统的角度来看，我们正在做 CPU 密集型工作，尽管实际上这是 IO 密集型的，这也是为什么我们的 Go 程序不需要更多线程以及为什么我们有硬件线程的原因之一，因为调度器正在转换我们所做的所有工作，


00:22:41

CPU and IO bound work always into CPU bound work at the operating system level. And I told you in the operating system mechanics, the most efficient work that you can do is CPU bound, it's also the simplest, because we know that we only need one thread per hardware
CPU 较多、IO 较多的工作在操作系统层面最终都会变成以 CPU 为主的工作。我在操作系统机制中告诉过你，最有效率的工作是以 CPU 为主的工作，它也最简单，因为我们知道每个硬件只需要一个线程。


00:23:01

and if we're doing concurrent work, then we know how to maximize our efficiency. More threads than you have cores, never is going to give you better throughput. That CPU bound workloads are beautiful and what Go is just done is it's reduced a huge amount of load off the operating system,
如果我们在做并发工作，那么我们就知道如何最大化效率。线程数超过 CPU 核心数，从来不会带来更好的吞吐量。CPU 密集型工作负载是理想的，而 Go 所做的，就是大幅减轻了操作系统的负担，


00:23:20

because the operating system basically just maintains a level of CPU bound workloads. We could use a lot less threads, which cost us more and since we're using less, that cost is less. And since the context switches cost a lot less we're going again from that one to 2000 nanoseconds
因为操作系统基本上只是维持一定级别的 CPU 绑定工作负载。我们可以使用更少的线程，这些线程成本更高，而因为我们使用更少，成本也就更低。并且由于上下文切换的开销小得多，我们又从那 1 到 2000 纳秒


00:23:41

to 200 nanoseconds, then even this, these transitions between states are happening a lot faster. This is the real beauty, this is the real synergy of what's happening here and the mechanical sympathies between the two schedulers. But I wanna stress something very, very clearly. Even though we've got this scheduler
降到了 200 纳秒，那么即便如此，这些状态之间的转换也发生得快得多。这才是真正的美妙之处，也是两者调度器之间机械性相互作用的真正协同。但我想非常非常明确地强调一点。即便我们有这个


00:24:02

that's doing all this wonderful stuff, you still have to be sympathetic with the scheduler. In other words, we still have to know what our workloads is. More Go routines than you have M's for CPU bound workloads are not going to make you get your work done faster,
在做所有这些精彩工作的调度器，你仍然必须对调度器保持“同理心”。换句话说，我们仍然必须知道我们的工作负载是什么。对于 CPU 绑定的工作负载，Go routine 的数量超过你拥有的 M（线程）并不会让你更快完成工作，


00:24:21

because you still have 200 nanoseconds. That's like 2,400 instruction losses that you're hitting when you have a context switch. And if it's CPU bound workloads like adding numbers, that's still 2,400 instructions or 2,400 numbers you could have added that's you're otherwise not adding,
因为你仍然有 200 纳秒。那相当于在发生上下文切换时损失了大约 2,400 条指令。如果是像加法这样的 CPU 绑定工作负载，那仍然是 2,400 条指令或者本可以相加的 2,400 个数字，你却无法相加，


00:24:42

'cause of the context switch. When it comes to IO bound workloads, we're gonna gain real efficiencies here, because that context switch is less and again, now we can have more Go routines than we have let's say M's. And what's really brilliant is that application thread, that Go routine is so lightweight
因为上下文切换。对于 IO 绑定的工作负载来说，我们将在这里获得真正的效率，因为上下文切换更少，而且我们现在可以拥有比比如说 M 更多的 Go routine。更妙的是，那个应用线程，也就是那个 Go routine，非常轻量级


00:25:01

that for the first time in our programming models, we could build a web service that could throw a Go routine at every request. In other words, we could have 50,000 Go routines in flight. It would be reasonable and practical to do that and those types of programming patterns are a lot simpler than trying to figure out
这意味着在我们的编程模型中，我们第一次可以为每个请求启动一个 goroutine。换句话说，我们可以同时运行 50,000 个 goroutine。这么做是合理且可行的，而且这种编程模式比试图去弄清楚要复杂得多。


00:25:20

what is the magic number of Go routines we need to create for some sort of thread pool here. This is some of that cognitive load that Go is taking off our backs, instead of just saying, let's find some magic number, let's just throw a Go routine at every problem that comes into the server, every request, every task and let the scheduler handle it.
我们需要创建多少个 Go routine 的“魔法数字”来作为某种线程池？这是 Go 为我们减轻的一部分认知负担；与其去寻找某个魔法数字，不如把一个 Go routine 丢到进入服务器的每个问题、每个请求、每个任务上，让调度器去处理它。


00:25:41

And it may not be the fastest way to solve the problem, but guess what? It tends to be fast enough and remember what we're always gonna be talking about, we need to balance the performance with the complexity. If it's fast enough and you've reduced a huge amount of complexity, that's a big, big, big win. If you're looking for pure performance,
这可能不是解决问题最快的方法，但知道吗？它通常已经足够快了，并且记住我们一直要讨论的，就是需要在性能和复杂性之间取得平衡。如果速度足够，而你却大幅降低了复杂性，那就是一个非常非常大的胜利。如果你追求纯粹的性能，


00:26:00

really, Go is not your answer. You gotta start looking at C again and assembly, maybe even Rust, Rust looks like a really interesting language to me. But if you're gonna have the mindset that it's fast enough, now this programming model, this multi-threaded programming model that Go's given us is really reducing load, cognitive load on us. We still gotta know what our workload is,
说实话，Go 并不是你的答案。你得重新看看 C 甚至汇编，可能还有 Rust，Rust 对我来说看起来是个非常有趣的语言。但如果你要抱着“它已经足够快”这种心态，那么现在这种由 Go 提供的多线程编程模型确实在降低我们的负担、认知负荷。我们仍然需要了解我们的工作负载是什么，


00:26:21

gotta know when we can leverage and not have to leverage parallelism. We still have to know these Go routine states. Less is still more. Complexity needs to be less, so stuff is complex. But we have these opportunities now, thanks to Go. So moving forward, we're gonna take these mental models that we now have of the operating system scheduler and the Go scheduler.
我们必须知道什么时候可以利用并行性、什么时候不必利用。我们仍然需要了解这些 Go 协程状态。更少仍然是更多。复杂性需要更低，所以某些事情本身就是复杂的。但现在得益于 Go，我们有了这些机会。所以接下来，我们要把现在关于操作系统调度器和 Go 调度器的这些心理模型带入实践。


00:26:42

We're gonna start looking at code, we're gonna start understanding what it means around synchronization and orchestration, 'cause that's on you, we'll talk about that stuff. We'll start looking at code, we'll start looking at patterns and I'm gonna do my best, to try to at least give you the knowledge and the tooling so you can make some better engineering decisions as you start to write multi-threaded software in Go.
我们将开始看代码，开始理解同步和编排的含义，因为那取决于你，我们会讨论这些内容。我们会开始看代码，开始研究模式，我会尽力至少提供给你知识和工具，这样当你开始用 Go 编写多线程软件时，就能做出更好的工程决策。


00:27:03

(relaxing music)  （轻松的音乐）