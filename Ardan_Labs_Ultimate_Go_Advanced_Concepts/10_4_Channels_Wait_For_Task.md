Transcript  转录本

00:00:00

(bright music) - [Announcer] Ardan Labs. Specializing in high-performance software consulting, training, staffing, and development. Module 10 channels. You are now watching lesson 10.4. Wait for task. (screen whooshing) - Let's now look at another base pattern. This one is called wait for task.
（明快音乐）- [播报] Ardan Labs。专注于高性能软件咨询、培训、招聘和开发。第 10 模块 通道。您现在正在观看第 10.4 课 等待任务。（屏幕呼啸）- 现在让我们来看看另一个基本模式。这个叫做等待任务。


00:00:20

It's the opposite of the other ones that we've been looking at. And wait for task, the idea is that we have a goroutine we're gonna launch to do some work, but this goroutine doesn't know what to do yet. It's going to wait to be told what is the task for it. This is gonna be something that we're gonna use in pooling patterns where we have a pool of goroutines.
它与我们之前看的那些模式相反。等待任务的想法是我们会启动一个 goroutine 去做一些工作，但这个 goroutine 还不知道要做什么。它会等待被告知任务是什么。这将用于池化模式，在那里我们有一个 goroutine 池。


00:00:40

We're posting work into the pool and those goroutines are waiting for the task to be performed. So on line 93, we're starting with that unbuffered channel again. Remember, unbuffered channels mean guarantees, a guarantee that the signal being sent has been received. So when we look at line 93, what we're gonna say is we have a channel
我们把工作放入池中，那些 goroutine 在等待任务被执行。所以在第 93 行，我们又从那个无缓冲通道开始。记住，无缓冲通道意味着保证——保证发送的信号已经被接收。所以当我们看第 93 行时，我们要说的是我们有一个通道


00:01:00

that has guarantees and we're signaling with string data. There we are. Now on line 95, we go ahead and we create that goroutine again. And once the goroutine is created, again, the goroutine does not know, does not know what it wants to do yet, or it doesn't know what to do yet. So there it is on line 96 waiting, it's blocked waiting for us essentially
它带有保证，并且我们用字符串数据来发出信号。就是这样。现在在第 95 行，我们继续并再次创建那个 goroutine。一旦 goroutine 被创建，同样地，goroutine 还不知道，要做什么，或者说它还不知道该做什么。所以在第 96 行它就在那儿等待，本质上是被阻塞等待我们


00:01:22

to get that work done. Then we move on to line 100. And now that guarantee, right, the latency for the guarantee, the unknown latency is now going to be happening on line 100. That goroutine and the receive is blocked, waiting for an unknown amount of time for us to prepare the work.
去完成那项工作。然后我们继续到第 100 行。现在那个保证的延迟，对吧，未知的延迟现在将在第 100 行发生。那个 goroutine 和接收操作被阻塞，等待我们准备好工作所需的未知时间。


00:01:41

Eventually we prepare the work, and then on line 101, we perform the send. And that's when line 101 and 96 come together. Again, there's a guarantee, so the receive on line 96 happens before the send on line 101, nanoseconds before, but nonetheless before,
最终我们准备好工作，然后在第 101 行执行发送。就是在第 101 行和第 96 行相遇。再次说明，这里有一个保证，所以第 96 行的接收发生在第 101 行的发送之前，可能早几纳秒，但无论如何是发生在前，


00:02:01

and then we're able to move on. So in this scenario that wait for task, the sender, again, is gonna get a guarantee that that goroutine that's gonna be doing the work has received it. This is, again, an important pattern for pooling, and when it comes to pooling patterns, we definitely want the guarantees,
然后我们就能够继续。因此在这个等待任务的场景中，发送方同样会得到一个保证：将要执行工作的那个 goroutine 已经收到了任务。这对于连接池来说又是一个重要的模式，而谈到连接池模式时，我们确实需要这些保证，


00:02:20

and we're gonna see that pooling pattern next. (bright music) (logo buzzing)
接下来我们将看到那个连接池模式。 (明快音乐) (标志嗡嗡声)