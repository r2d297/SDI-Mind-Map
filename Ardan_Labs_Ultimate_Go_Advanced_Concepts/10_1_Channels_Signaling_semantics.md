00:00:00

(bright chiming music) - [Narrator] Ardan Labs specializing in high-performance software consulting, training, staffing and development. Welcome to Module 10 Channels. Let's get started with Lesson 10.1 Signaling Semantics. - So the other part of being a multi-threaded software developer is the orchestration.
（明亮的钟声音乐）- [旁白] Ardan Labs 专注于高性能软件咨询、培训、招聘和开发。欢迎来到第 10 单元 通道。让我们从第 10.1 课 信号语义开始。 - 作为多线程软件开发人员的另一部分职责是编排。


00:00:20

And I've shown you already how to use weight groups to do orchestration, but one of go's biggest features is the channel. And it's the channel that allows us to do orchestration in a much simpler way, simpler than we've ever had the ability to do it before. And there are some real basic patterns around channels
我已经向你展示过如何使用 wait group 来做编排，但 Go 的最大特性之一是 channel。正是 channel 让我们能够以更简单的方式进行编排，比我们以前有过的任何方式都要简单。有一些围绕 channel 的基本模式，


00:00:42

that if you learn, it's gonna help you be better at thinking about orchestration. For me, too many developers make a mistake by thinking about channels as a data structure as a queue. And I don't want you to think about a channel as a data structure queue. Channels really provide one basic semantic.
如果你学会了，会帮助你更好地思考编排。对我来说，太多开发者把 channel 错误地当作一种数据结构、当作队列来思考。我不希望你把 channel 看作数据结构或队列。channel 实际上提供了一种基本语义。


00:01:02

And for me that is signaling. A channel allows one go routine to signal to another go routine about some event. Sometimes we can signal with data and sometimes we can't. But it's the signaling semantics that are very important here and that's what we have to talk about.
对我来说那就是信号。channel 允许一个 goroutine 向另一个 goroutine 发出某个事件的信号。有时我们可以用数据来发信号，有时不能。但正是这种信号语义非常重要，这也是我们必须讨论的内容。


00:01:21

So let's get into these signaling semantics. Now, the first thing, the first thing you want to think about when it comes to signaling is on the send side. I always like focusing on the send side. So the question becomes, does the go routine that is performing the send,
那么我们来讲讲这些信号语义。现在，关于信号传递你首先要考虑的第一件事是在发送端。我总是喜欢把注意力放在发送端。所以问题变成了，执行发送的那个 goroutine 是否...


00:01:41

and remember this is signaling, so we say send and receive, not read and write. Is the go routine that is signaling performing the send, does that go routine? Need a guarantee that the signal being sent has been received. That is the very first question that we want to ask. Does the go routine performing the send need a guarantee
并且要记住这是信号传递，所以我们说 send 和 receive，而不是 read 和 write。发出信号的 goroutine 是在执行发送吗？那个 goroutine 是否需要保证所发送的信号已经被接收？这是我们要提出的第一个问题：执行 send 的 goroutine 是否需要一个保证？


00:02:03

that their signal has been received? The answer is yes, that changes the dynamics. If the answer is no, then obviously, the dynamics change in the opposite direction. So let me give you a kind of a little bit of a storyline where we can think about how this would work in our code.
他们是否收到了信号？答案是肯定的，那会改变动态。如果答案是否定的，那么动态显然会向相反的方向改变。让我给你讲一个小小的情节，来说明这在我们的代码中会如何工作。


00:02:21

And I always love to think about go routines as people. And I always love the idea of a manager and employee relationship. And we're gonna use these ideas as well to read code to find problems. So let's say that I work with Jack every day. And normally what happens is I come in in the morning, and I go over to Jack,
我总喜欢把 goroutine 想象成人。也总喜欢经理和员工关系这个比喻。我们也会用这些想法来读代码、发现问题。比方说我每天都和 Jack 一起工作。通常的情况是我早上来，然后走到 Jack 那儿，


00:02:42

and I give Jack work to do in the morning, and Jack gets it done and he usually has it done before lunch and I can go and I can pick it up. And we have this relationship. And the reality is, is that Jack's not always in on time and it's never really mattered before. 'Cause I would just in over to Jack's desk
把早上的工作交给 Jack，Jack 会完成，通常在午饭前就能做好，我可以去拿。我们就是这种关系。现实是，Jack 并不总是准时到，这以前从没什么大碍。因为我只要走到 Jack 的办公桌前，


00:03:01

and put some work on his desk, and walk away knowing that Jack was gonna get it done. But a couple days ago, unfortunately, Jack decided to throw me under the bus. You see, I left the work with him like I always do. And then when I came back in the afternoon, it hadn't gotten done. We got into a little bit of a argument.
把工作放在他桌上，然后离开，知道 Jack 会去完成。但就在几天前，不幸的是，Jack 决定把我推到车轮下。你看，我像往常一样把工作留给他，下午我回来的时候却发现还没做完。我们因此有了点争执。


00:03:21

And at the end of the day it got back to our managers and I got in trouble for the work not getting done. Not Jack, you know, I did. And now I'm at a point where I cannot trust Jack anymore with just getting the work. You know, Jack basically told the manager that he'd never gotten that work from me and that's why he hadn't gotten it done.
到头来这事传到了我们经理那儿，工作没有完成，我被批评了。不是杰克，你知道的，是我被责备。现在我已经不能再信任杰克会把工作做好了。你知道，杰克基本上向经理说他从来没有从我这里拿到过那份工作，所以他才没做成。


00:03:41

Obviously, I put it on his desk, right? And I wouldn't be lying. But here we are in a little bit of a row. So moving forward with Jack. Now I need a guarantee that when I give him work that he's received it. So the next morning, now I come into work, it's nine o'clock
很明显，我把它放在他桌子上了，对吧？我没有撒谎。但我们现在有点争执。接着说到 Jack。现在我需要一个保证：当我交给他工作时，他确实收到了。于是第二天早上，我来上班，九点钟。


00:04:01

and Jack is not in. As far as Jack's concerned, 10:00 a.m. is the new nine. But here I am again, I'm stuck, right? I have to get the guarantee that Jack receives this work. So now I'm stuck at Jack's desk waiting for Jack to come in. Now, eventually Jack comes into work. Maybe he gets in at 9:30.
杰克不在。就杰克而言，上午 10 点就是新的 9 点。但是我又回到了原地，卡住了，对吧？我必须确保杰克能收到这份工作。所以现在我在杰克的办公桌旁等着他来。后来杰克终于上班了。也许他在 9:30 就到了。


00:04:20

And when he does, I take the work that I need to give him and I perform this send. So here I am, right here performing that signal right with the send. But remember now the way to get the guarantee is for Jack to come in. So here I am on the send side. Jack comes in on the receive side. Here's Jack, here I am.
当他来了的时候，我把需要给他的工作拿出来并执行这个发送。所以现在我就在这里，正在用这个发送来发出那个信号。但记住，要获得保证的方式是让 Jack 来接收。所以现在我在发送端。Jack 在接收端进来了。看，Jack，在这里，我在这儿。


00:04:41

And the only way we get this guarantee is if the receive happens before the send. In other words, Jack pulls this out of my hand that says, okay, now I have it. That's where we get this guarantee of delivery, that Jack pulls it out, the receive happens before the send. I can look at my hand and go, oh, oh, yep, it's gone.
而我们获得这种保证的唯一方式是接收发生在发送之前。换句话说，Jack 从我手里把它拉走，说“好，我现在有了”。这就是我们得到传递保证的地方：Jack 把它拉走，接收发生在发送之前。我可以看着我的手说，哦，哦，是的，它没了。


00:05:00

Jack took it and we move on. Then in the afternoon I come back to get that work, and Jack's again, not at his desk. Maybe Jack went to lunch early. There's guarantees involved now because of the problems that we were having. I'm now stuck at his desk again. I wait for Jack to come back from lunch.
杰克拿了它，我们继续前进。然后下午我回来取那份工作，杰克又不在座位上。也许杰克提前去吃午饭了。现在因为我们之前遇到的问题，事情变得有了保障。我现在又被困在他的桌前。我等着杰克从午饭回来。


00:05:20

Maybe it takes him 45 minutes. He comes back, then Jack performs his send. I can perform the receive, we come together. Receive happens before the send, and now Jack gets the guarantee. So guarantees are critically important. They're gonna help us with consistency. They're gonna help us know that things are happening when they happen.
也许他花了 45 分钟。等他回来，Jack 然后执行他的发送。我可以执行接收，我们就同时进行了。接收发生在发送之前，现在 Jack 得到了保证。因而，保证非常重要。它们会帮助我们保持一致性，帮助我们确定事情发生的时间。


00:05:40

But like everything that we've talked about right now, nothing is free. And if you want the guarantee that a signal being sent has been received, if we have to wait for the receive to happen before the send, then what you have to live with is this unknown latency cost. And remember what's slowing down your programs throughput, latency.
但正如我们刚才讨论的一切，天下没有免费午餐。如果你想保证发送的信号已被接收——即必须等到接收发生后才发送——那么你要承担的就是这个未知的延迟成本。别忘了，拖慢程序吞吐量的是延迟。


00:06:01

So there's nothing free here. To get the guarantee, you have to appreciate the fact that there may be unknown and high latencies while you are waiting, maybe on the send side, to be able to perform that send. 'Cause the receiver has to come along. Or even on the other side, the receiver happens,
所以这里没有什么白吃的。要获得保证，你必须意识到在等待期间可能存在未知且很高的延迟——比如在发送方等待能够执行那次发送时。因为接收方必须过来。或者即便是在另一端，接收方一来，


00:06:20

comes in first, but we're waiting for the sender. In other words, the send and the receiver have to come together. Now, I'm losing a lot of time on this guarantee with Jack. So I have a conversation with Jack and I say, Jack, you know what? Let's make up, let's not fight anymore. You know, and I don't really care what time you get into work, it's not my problem.
先到达的是我，但我在等发送者。换句话说，发送者和接收者必须同时到位。现在，我在这个保证上和 Jack 浪费了很多时间。所以我和 Jack 谈了一次，我说，Jack，你知道吗？我们和好吧，别再争了。你知道的，我并不在乎你什么时候到公司，那不是我的问题。


00:06:40

But I need to get back to the way things where Jack and I make up. So now this time when Jack, I'm sorry, this time when I come into work, Jack again is not at his desk. I don't care, I can perform my signal, my send, right? I can perform the send, place that piece of work on his desk and walk away.
但我需要让事情回到以前 Jack 和我和好的状态。所以这次当我，抱歉，这次当我来到公司时，Jack 又不在他的办公桌旁。我不在乎，我可以执行我的 signal，也就是发送，对吧？我可以执行发送，把那份工作放在他桌上然后离开。


00:07:00

The send happens before the receive. And I'm gonna get the benefit of not having to incur all of that extra latency, especially the unknown latency. But remember, there's nothing free about that. Now I have the cost of risk. Because now again, I don't know when Jack is coming in, I don't know when he's gonna take the work. I don't know it.
发送发生在接收之前。这样我就能不必承担所有那些额外的延迟，特别是不可预知的延迟。但记住，这并非没有代价。现在我承担的是风险的成本。因为现在我仍然不知道 Jack 什么时候会来，不知道他什么时候会接手这项工作。我不知道。


00:07:20

I'm really taking a risk that Jack is gonna come in and do something. That's the problem with not taking the guarantee. But what's the benefit? The latency has been either removed or reduced. And so we've gotta be very clear that whatever benefit we're taking the risk, the risk is worth it. We're gonna walk away from the guarantee for the benefit
我真的冒着杰克可能进来做点什么的风险。这就是不采用保证的麻烦所在。但好处是什么？延迟要么被消除了，要么被降低了。所以我们必须非常清楚：我们为了获得某种好处而承担的风险，是值得的。我们将为了这个好处放弃那个保证。


00:07:41

of that reduced latency. The risk of not having the guarantee better be worth it. And in different patterns, we're able to take those guarantees. And sometimes we can't. Sometimes we can not necessarily say can't, but sometimes we can walk away from 'em and still make sure that we have these high levels of integrity. At the end of the day, there's a guarantee somewhere.
这种降低延迟带来的风险，如果没有相应的保证，就必须值得。不同的模式下，我们能够接受这些保证。有时候我们不能。也不是绝对不能，但有时我们可以放弃这些保证，同时仍然确保高度的数据完整性。归根结底，总有某种保证存在。


00:08:00

If it's not gonna be on the channel signaling, then it's gotta be somewhere in the code. So we know that some concurrent, say operation, has been completed. Alright, so that first question we talked about was on the signaling semantics. Do we need a guarantee that the signal being sent has been received?
如果不是通过信道的信号来告知，那就必须在代码的某处去体现。所以我们知道某个并发操作，比如说某个操作，已经完成了。好，那么我们刚才讨论的第一个问题是关于信号语义的。我们是否需要保证发送的信号已经被接收？


00:08:22

Now the other question we can ask is, do we want to signal with data or without data? The example that I showed you was signaling with data. We had a piece of data that left my hands, went into Jack hands, left Jack's hands went into mine. And when you're doing signaling with data, that's only a one-to-one signal, okay, a one-to-one.
现在我们可以问的另一个问题是，我们想要带数据的信号还是不带数据的信号？我之前给你看的例子是带数据的信号。我们有一份数据从我手里传到 Jack 手里，又从 Jack 手里传回到我手里。当你用数据进行信号传递时，那只是一个一对一的信号，好吧，一个一对一。


00:08:43

But what if we wanted to do a one to many? What if we needed a bunch of go routines to know about an event? Well, there's only one piece of data, so I could signal individually, but that would take some time. So we have the ability to signal without data,
但如果我们想做一对多呢？如果我们需要一堆 goroutine 知道某个事件怎么办？嗯，只有一份数据，所以我可以逐个发送信号，但那会花费一些时间。因此我们有能力发送不带数据的信号，


00:09:00

and we do that by closing a channel. So the idea there is that we basically turn the lights off. If there was an auditorium of people and we turn the lights off, everybody would see that event. They wouldn't have anything to take home with them, but they would see it. And that's what closing the channel does.
我们通过关闭一个 channel 来做到这一点。这里的想法基本上就是把灯关掉。如果有一个礼堂里的人，我们把灯关了，大家都会看到那个事件。他们不会带走任何东西，但会看到它。这就是关闭 channel 所做的事情。


00:09:20

You don't need to close the channel for memory leaks or issues like that. It's literally just a state change from open to close. And a channel can be in one of three states. A channel can be in an open state. And we do that by making a channel. So we gotta use the built-in function make to put it into an open state.
你不需要为了避免内存泄漏或类似问题而关闭通道。它本质上只是从“打开”变为“关闭”的状态变化。通道可以处于三种状态之一。通道可以处于“打开”状态。我们通过创建通道来实现这一点。因此我们必须使用内置函数 make 将其置为“打开”状态。


00:09:40

Then receives and sends can happen in many of the ways that we describe. A channel could be in its zero value state or a nil state. That means sends and receives are gonna block. We can use that for short term shortages like rate limiting and things like that. Maybe in event loops. And then finally a channel can be closed. We're gonna use that mainly for cancellation and shutdowns,
然后接收和发送可以以我们所描述的多种方式发生。通道可能处于其零值状态或 nil 状态。那意味着发送和接收会被阻塞。我们可以将其用于短期缺乏资源的情况，比如速率限制之类的场景。也可能用于事件循环。最后，通道可以被关闭。我们主要用那种方式来做取消和关闭，


00:10:03

and we'll see all of that. So these are those signaling semantics that we're gonna be using moving forward. One, does the sender need a guarantee that their signal has been received? How does that work? The receive happens before the send. And both send and receiver have to come together
我们会看到所有这些。这些就是我们将来要使用的那些信号语义。其一，发送者是否需要保证他们的信号已经被接收？这是如何工作的？接收发生在发送之前。发送者和接收者必须在同一时间点汇合。


00:10:21

at that moment in time. When I say that the receive happens before the send, it's gonna happen nanoseconds before. Remember it's still in a multi-threaded environment here, and it happens nanoseconds before. So do we need that guarantee? If we take the guarantee, we gotta live with the unknown latency. If we don't take a guarantee that signals being sent has been received, we can reduce
当我说接收发生在发送之前时，实际上是发生在纳秒级之前。记住这里仍然是在多线程环境中，并且确实是在纳秒级之前发生的。那么我们需要那种保证吗？如果我们接受该保证，就必须接受未知的延迟。如果我们不要求信号被接收的保证，我们可以减少


00:10:42

or almost eliminate that latency. But there's risk. And the more risk, the more problems. Then we need to know the state of the channel. So that's gonna tell us how it's gonna operate. And then finally we want to know, do we need to deliver that signal with or without data?
或者几乎消除那种延迟。但这有风险。风险越大，问题越多。那样我们就需要知道通道的状态。这会告诉我们它将如何工作。最后我们还要知道，我们是否需要在传递该信号时附带数据，还是不附带数据？


00:11:02

(bright chiming music)  （明亮的铃声音乐）