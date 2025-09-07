00:01
Well, so we're going to post in each discussion section what topics we're going to cover, in case there might be some differences, sometimes between the discussion sections, what will be covered, but tomorrow the first week all of you guys will cover Project one, how to start that, maybe how to run test scripts, how to run debugger gdb
嗯 所以我们将在每个讨论部分发布我们将覆盖的主题 以防可能会有一些差异 有时在讨论部分之间 将覆盖什么 但明天的第一周 所有的TA们都将覆盖 项目一 如何开始那个 也许如何运行测试脚本 如何运行调试器 Gdb

00:21
What makes a file look like What does lint and valgrind look like Are these static and dynamic analysis tools so you can see if there are obvious problems in the code or memory allocation So you can check out the web page for more information on what will be discussed in the discussion section Everyone should sign up for piazza
使文件看起来像什么 lint和valgrind看起来像什么 这些是静态和动态分析工具吗 以便你可以查看代码或内存分配中是否有明显的问题 所以你可以查看网页以获取更多关于 讨论部分将讨论什么 每个人都应该注册piazza

00:40
The last time I looked at it, there were already countless questions and answers that had been asked and answered, maybe two hundred people signed up for that, but there were a lot of people and a lot of people who didn't sign up, oh, I hope that happens soon, okay, the lecture recording, okay, so a lot of people like the idea of the lecture being recorded
上次我看的时候，已经有无数的问题和答案已经被问到并回答了 也许有两百多人报名参加了那个 但是还有很多人 还有很多没有报名的人 哪 我希望这种情况能尽快发生 好的 讲座录音 好的 所以很多人喜欢讲座被录制的想法

00:58
In an ideal world, you could look back at them and look back and now, all of us have unanimously found a lot of things in many different classes where people have found many times that everyone has the best intentions that you think oh I'll skip class and watch that lecture recording later in the day and what happens is if you watch it
在理想的世界里，你可以回看他们并回顾 而现在，我们所有人都一致地发现了很多 在许多不同的班级中，人们多次发现每个人都有最好的意图 你 think 哦 我会翘课，晚些时候看那个讲座录音 结果发生的是 如果你看了它

01:17
You might as well sit here and understand it, like if you're here, living with other people, what often happens is that you just feel that those lectures are accessible to me, and I'll watch them later, and you don't end up looking at them at all, I mean, I've talked about so many people who thought they would do it
你仍然不如在这里坐着理解它 好像如果你在这里 与别人一起生活 常常发生的事情是 你只是觉得 那些讲座对我而言是可达的 我会晚些时候看它们 而你最终根本不会看它们 我的意思是 我谈论过那么多人，他们以为自己会做

01:33
And they don't actually watch those lectures at all, so attendance is pretty low, last semester when they recorded all the lectures, and I've never done that before, it's not that I'm teaching it, but in the past, attendance has been good, so I'm going to try it as an experiment, and I'm going to make the lecture recordings available during the week
而他们实际上根本不看那些讲座 所以出席率相当低 上个学期当他们录制了所有的讲座时 而且我之前从未做过那样 不是我在教它 但在过去，出勤率一直很好 所以我打算作为一个实验来尝试 我会将讲座录音在一周内提供

01:53
So if you really miss a lecture you can watch it right after class and keep up with other people but the point is that you should get back in sync and go to the next lecture you can and then I might offer them again you know, a few days before the midterm and the end so you can review but not to make you believe and trick yourself into thinking
所以如果你真的错过了讲座 你可以在课后立即观看它，并与其他人保持同步 但关键是你应该恢复同步并参加下一个讲座 你可以 然后我可能会再次提供它们 你知道，在期中和期末的几天前 以便你可以复习 但不是为了让你相信并欺骗自己认为

02:13
You can watch all these lectures on the last day of the midterm and the end of the term and catch up on all the material It's an experiment I'll try it I hope it's a good compromise for everyone, right, I think we're making good progress on the waiting list But if you're still on the waiting list Meet me after class and sign the form
你可以在期中和期末的最后一天观看所有这些讲座 并赶上所有材料 这是一个实验 我会尝试它 我希望这是一个好的妥协 对每个人都适用，对吧 我认为我们正在等待名单上取得良好进展 但如果你还在等待名单上 课后来见我并签名表格

02:31
Okay, the lecture ends at 1:15 p.m., why do I say that, okay, I promise I'll always finish the lecture on time at 1:15 p.m., so that you can go to your next lesson, sometimes I may finish before 1:12 or 1:14 p.m., but I won't go beyond that, but I hope all of you wait until I actually finish the lecture
好的 讲座在下午一点十五结束 我为什么这么说 好的 我保证我会总是准时在下午一点十五结束讲座 以便你可以去你的下一节课 有时我可能在下午一点十二或一点十四之前结束 但我不会超过 但我希望所有的你们等到我真的结束讲座

02:49
And then start packing and going to your next class, because the class is big, and when some people start packing, it's really noisy so that other people who want to hear my final summary statements can't hear it, and actually hear those statements, okay, 1:15 p.m., and that's when we're done, and then finally, the microphone I'm using the microphone
再开始打包并去你的下一节课，因为班级很大 当一些人开始打包 真的很吵 使得其他想听我的最后总结陈述的人无法听到 实际上听到那些陈述 好的 下午一点十五 那时我们就结束了 然后最后，麦克风 我在使用麦克风

03:08
If it doesn't work at some point, raise your hand to let me know, and of course, you can also raise your hand in class and ask questions about other materials Oh, it's picked up in a different way, but okay so about all that setup side of the question okay today we're going to talk about virtualization or how we abstract the CPU
如果它在某个时候不工作 举起手让我知道 当然，你也可以在课堂上举起手问关于其他材料的问题 哦，它就以不同的方式拾取了 但好的了 所以关于所有那个设置方面的问题 好的 今天我们将讨论虚拟化 或我们如何抽象CPU

03:36
So that users can use the CPU more easily and efficiently So by the end of this afternoon you're going to understand what a process is, what is its general lifecycle and then you're going to understand these mechanisms about how the operating system gets and runs processes How processes interact with the operating system through system calls and then how we do context switching
以便用户可以更容易、更有效地使用CPU 所以到今天下午结束 你将了解什么是进程，什么是其一般生命周期 然后你将了解这些机制 关于操作系统如何获取并运行进程的机制 进程如何通过系统调用与操作系统交互 然后我们如何进行上下文切换

03:57
Okay, in last week's lecture we briefly talked about what an operating system is, so for now it's just a rhetorical question, but can you remember in your head that if you had to define an operating system, how would you define it I would say it's software, transforming hardware into a form that is useful for applications and it's a standard library
好的 在上周的讲座中 我们简要讨论了什么是操作系统 所以现在这只是一个修辞性问题 但你能否在你的脑海中记住 如果你必须定义操作系统，你会如何定义它 我会说它是软件，将硬件转换为对应用程序有用的形式 它是标准库

04:20
And it is the resource manager What is the abstraction that the operating system provides for the CPU and that is what we are going to talk about today It is a process or thread What is the abstraction that the operating system provides for memory virtual address space or just address space What are some of the advantages that the operating system provides resource management that we need to provide protection or isolate competing applications that share the same resources
并且它是资源管理器 操作系统为CPU提供的抽象是什么 这就是我们今天要讨论的 它是进程或线程 操作系统为内存提供的抽象是什么 虚拟地址空间 或只是地址空间 操作系统提供资源管理的一些优势是什么 我们需要它来提供保护或隔离竞争的应用程序，它们共享相同的资源

04:45
This will allow us to share resources more fairly and possibly better performance and efficiency with our operating system policies OK so let's dive into many details Let's change the order OK One of our advanced goals is to virtualize the CPU and we want each process to have the impression that it seems to be running on the only CPU
这将使我们能够更公平地共享资源 并且可能以我们的操作系统政策获得更好的性能和效率 好的 所以让我们深入探讨许多细节 让我们改变一下顺序 好的 我们的高级目标之一是虚拟化CPU 我们想要每个进程都有印象 它似乎是在唯一的CPU上运行

05:12
It's completely isolated from other people, and we usually do this for all our resources, we can share a resource, we can multiplex a resource in time and space, just like if we can close this room, another class can come in here, we share this space, this room, this resource, in time
它与其他人完全隔离 我们通常这样为我们的所有资源进行 我们可以共享一个资源 我们可以在时间和空间上多路复用一个资源 就像如果我们可以关闭这个房间 另一个班级可以进来这里 我们共享这个空间 这个房间这个资源在时间上

05:33
Other classrooms You can think of it as different spaces In different classrooms, different classes do different spaces at the same time Of course this can be applied to any resource Not just computer systems We are going to share CPUs in time In this class, we assume that we only have a single unit processor or a single core
其他教室你可以视为不同的空间 在不同的教室里，不同的班级在同一时间进行不同的空间 当然这可以应用于任何资源 不仅仅是计算机系统 我们将在时间上共享CPU 在这堂课中，我们假设我们只有单个单位处理器或单个核心

05:54
It gets really interesting when there are multiple processors and you're sharing processes or threads across those cores, even spatially in a spatial way but you can learn that in today's subsequent lessons just need a single core okay so how do we process in parallel or share memory We usually do that on a space where you have a lot of memory
当有多个处理器时，情况会变得非常有趣 并且您正在跨这些核心共享进程或线程，甚至在空间上也是如此 以空间共享的方式 但是你可以在今天的后续课程中学习那个 只需要单核 好的 那么我们如何并行处理或共享内存 我们通常会在你有很多内存的空间上进行那个

06:16
Different applications can have different pagination in memory We will talk about that in detail later Then the hard disk will also be space shared, the hard disk is very large We have a lot of blocks We can assign different chunks to different processes and share that also spatially but the CPU is now time sharing
不同的应用程序可以在内存中有不同的分页 我们稍后会详细讨论那个 然后硬盘也会是空间共享的，硬盘非常大 我们有很多块 我们可以将不同的分块分配给不同的过程，并在空间上也共享那个 但是CPU 现在是时间共享

06:32
Okay, so these are high-level stuff, let's start talking about what actually happens in a process, what is a process, so I think um, you may have used that term at once, not very precise, so we want to talk about a process very precisely in this course, so you guys usually talk about that
好的 所以这些都是高层次的东西 让我们开始谈论在进程中实际发生的事情 什么是进程 所以我认为 嗯 你可能曾经使用过这个术语 不是很精确 所以我们在这个课程中想要非常精确地讨论一个过程 所以你们通常谈论那个

06:48
You write a program, you should think of the program as static code that you write, and you save it, it's not a running version of that program, the program is just a static thing that you write, and you can even compile it, you can have an executable, and the executable is still just a program, but when you actually run that thing
你们编写程序 你们应该把程序看作是你们写的静态代码 并且你们保存了它 它不是那个程序的运行版本 程序只是您写的静态东西 而且您可以甚至编译它 您可以有一个可执行文件 可执行文件仍然只是一个程序 但是当你实际上运行那个东西时

07:07
That's when it becomes a process, so for a single program, you can have multiple processes, yes, you can start that program multiple times, and have them all run at the same time, or at the same time, so what exactly is a process, we say it's an executing instruction stream, which is the code that you write, that runs in sequence until you hit a branch, a jump, or something like that
那就是它变成一个过程的时候 所以对于单个程序 你可以有多个进程 对 你可以多次启动那个程序，让他们都同时运行 或者同时 那么到底什么是进程 我们说它是一条执行中的指令流 就是你写的代码，按照顺序运行的 直到你遇到分支、跳转或者类似的东西

07:31
Along with all the context associated with its address space or memory So what is the context that's the dynamic part that changes as we run this program So it's the contents of each register It's all the addresses that you might have in the register It's your program counter or instruction pointer that shows you where you're running right now
连同与其地址空间或内存相关联的所有上下文 那么上下文是什么 那是随着我们运行这个程序而变化的动态部分 所以它是每个寄存器的内容 它是你可能在寄存器中的所有地址 它是你的程序计数器或指令指针 显示给你 你现在正在运行在哪里

07:53
In your static code, this is a pointer to your heap that shows you exactly which programs you are calling and which parameters you are pushing into that heap so that you can return them, and it is recording exactly where you are running the instruction stream right now, and maybe we'll get other states later on, such as open file descriptors
在你的静态代码 这是一个指向你的堆的指针 显示你确切地知道你调用了哪些程序 以及你将哪些参数推入那个堆 以便你可以返回它们 它正在精确地记录你现在在运行指令流的位置 并且可能我们后来会得到其他状态 如打开的文件描述符

08:14
The communication things that this process does to other processes, like through sockets or stacks, so any questions about processes Okay, I'll ask all of you later, because someday we'll need to talk about it, but I'm not going to really do that today, okay, when you create a process, you have that static program that lives on disk or persistent storage
这个进程对其他进程所做的通信事情 如通过套接字 或堆栈 所以任何关于进程的问题 好的 我会稍后问你们所有人 因为总有一天我们需要谈谈 但我今天不会真正那样做 好的 当你创建一个进程时 你有那个在磁盘或持久存储上生活的静态程序

08:41
It contains all the static elements associated with it, the program code and the static data, you know you have some global variables, and you initialize them to some known static value, which is the static part of the program, and then the process is forked or created, and then we need to make it alive, so we need to copy those things in memory
它包含了与它相关联的所有静态元素 程序代码和静态数据 你知道你有一些全局变量 并且你将它们初始化为一些已知的静态值 那就是程序的静态部分 然后进程被fork或创建 然后我们需要使它活起来 因此我们需要在内存中复制那些东西

09:03
It's tied to this new unique process, so it's fairly easy to get that initial state, you can basically just load those things from persistent storage, copy them in memory, and you'll have the code, and you'll have the instruction pointer that you start with a pointer to the first instruction, and you initialize the registers to some known state
与这个新的独特进程相关联 所以获取那个初始状态相当容易 你可以基本上只是从持久存储中加载那些东西 在内存中复制它们 你会有代码 你会有 你开始以一个指针 指向第一个指令的指令指针 你初始化寄存器到一些已知的状态

09:24
You initialize all the static data into the program file and you start with a small heap that grows as the process calls malloc You start with a heap with almost nothing and a heap pointer to it, and then when that process runs you change those registers you change the heap pointer on the PC
你初始化所有所有静态数据到程序文件中说的 你开始以一个小的堆，它随着进程调用malloc而增长 你开始以一个几乎什么都没有的堆 并且一个指向它的堆指针 然后当那个进程运行时 你会改变那些寄存器 你会改变pc上的堆指针

09:44
So every running process will have its own share of those things in memory Okay, that's pretty straightforward, you're saying, I'm not sure if I'm getting new information now, okay, it's probably new So what's the difference between a process and a thread So you can think of the default process as having only one thread in it
所以每个运行的进程都会在内存中都有自己的一份那些东西 好的 这相当直接 你是说 我现在是否得到了新的信息 你不确定，好吧 这可能是新的 那么进程和线程之间的区别是什么 所以你可以认为默认的过程只有一个线程在其中

10:07
So if you have two processes, and they access the same address in their address space, they're going to see different values, and if you have two threads in a process that share the same address space, so they're actually going to see the same value, and they're both going to have access to each other's heap, so let's do a demonstration
所以如果你有两个过程，并且它们访问它们地址空间中的同一个地址 它们将看到不同的值 而如果你有一个进程中有两个线程 它们共享相同的地址空间 所以它们实际上将看到相同的值 它们两者都可以访问彼此的堆 所以让我们来做一个演示

10:30
It's similar to the presentation I did on Thursday, but I'm trying to simplify it a little bit, I was going to bring my reading glasses, you guys won't see, okay, so I'm blind here, do you believe it, so it's process.c It's very, very simple, it has a value that we assign on the heap, and we take a parameter
这与我在周四讲座中做的演示类似 但我试图简化它一点 我本意是要带我的阅读眼镜 你们将看不到 好的 所以我在这里是盲的 你相信吗 所以这是process.c 它非常非常简单 它有一个我们在堆上要分配的值 我们接受一个参数

11:08
It should be the value that we're going to store in that variable so I think when you run this, what happens we run the process and then let's say the value we give it is eleven what it should print and it will say 'the initial value of this process is' for this process it's ten and then I copy it there
它应该是我们要存储在那个变量中的值 所以我认为当运行这个时，会发生什么 我们运行process 然后 假设我们给它的值是十一 它应该打印什么 它将说'这个进程的初始值为' 对于这个进程 它是十 然后我复制它那里

11:30
And then forever it will say it's eleven after ten, then forever it's eleven ten, then forever after it's eleven and then forever it's eleven and then if I have one, I start it I say I want this one to have a value that is twelve and it's going to be completely independent of the other processes that are running No sharing happens in their name
然后永远它将说它是十一之后 对 十，然后永远之后它是十一 十，然后永远之后它是十一 然后如果我有一个，我开始它 我说我想要这个有一个值是十二 它将完全独立于正在运行的其他过程 没有共享发生在他们的名称中

11:53
Again, but it doesn't matter, it also sees that one initial value is ten, and while other processes are running, it sees twelve in that variable, why does the other see eleven, so it makes it understandable that this is your daily life about how you write the program and the head process is running all the time, is there any problem with that
同样 但这并不重要 它也看到了一个初始值是十 同时在其他过程运行时 它在那个变量中看到十二 为什么另一个看到十一呢 所以这使每个人都能理解 这是你的日常生活 关于你如何编写程序和头进程一直在运行 关于那个有任何问题吗

12:19
Okay, so let's look at the version with threads, not thread point zero point c okay so about how you start a thread we'll talk about that later, for now, I just want to focus on that value that is shared, these two threads that belong to the same process, okay, so now I have a shared variable that's on the global heap
好的 所以让我们看看带有线程的版本 而不是 线程点零点c 好的 所以关于你怎么启动 线程 我们稍后再讨论 目前 我只想关注被共享的那个值 这两个属于同一进程的线程 好的所以现在我有一个位于全局堆上的共享变量

12:45
I've told the compiler that it's volatile because I know both threads will access it and I want to make sure that value is therefore kept in memory and not in the register What Maine is doing is it starts two threads, calls this worker function and passes it to the first worker The first argument of the second worker function
我已经告诉编译器它是易变的 因为我知道两个线程都将访问它 我想要确保那个值因此被保留在内存中，而不是在寄存器中 缅因州正在做的是 它启动了两个线程，调用了这个工人函数 并将它传递给了第一个工人 第二个工人函数的第一个参数

13:04
The second parameter, because I want them to each set that um, variable to a different value So I'm only running it once now on thread v0 Let's give it 13 and 14 are parameters So, what we expect to happen When the first thread runs it will print out the initial value of the value which will be ten
第二个参数，因为我想让它们各自设置那个 嗯，变量到一个不同的值 所以我现在只在线程v0上运行一次 让我们给它13和14是参数 那么，我们期待什么会发生 当第一个线程运行时 它将打印出value的初始值 这将是十

13:28
And then it will print out what it sets it to This Will Be Thirteen And it will continue to spin without resetting it And then at the same time, that other thread is started I created it before it did that so the other person has a chance to start "We don't have any race conditions" "Because we don't know how to do locks and syncs right now"
然后它将打印出什么 它将它设置为 这将是十三 并且它将继续旋转而不重置它 然后与此同时，那个其他线程被启动起来 我在它做那个之前创建了它 所以另一个人有了开始的机会 "我们没有任何竞争条件" "因为我们现在还不知道如何做锁和同步"

13:47
So we're just making them less competitive "The second thread is up" and it's going to access the same memory" "The first worker thread is also accessing it" "So, its initial value will be the value that the previous one set to it" "And then when it goes down, when it goes down, it has value."
所以我们只是在让他们不那么争强好胜 "第二个线程启动起来" "并且它将访问相同的内存" "第一个工人线程也在访问它" "所以，它的初始值将会是前一个设置给它的值" "然后，当它落山时，当它落山时，它就有了价值。"

14:07
They're all going to see the change, okay, so let's see this happening, and I'm just calling it a threat, great, so they're both going to see the value is fourteen, so the first thread sees the initial value is ten, and then it's set to thirteen, and the second thread sees the value is thirteen, because that's shared, and it's the same variable in both of them
他们都会看到变化 好的 那么让我们看看这个发生 我只是把它叫做威胁 太好了 所以他们都将看到值的是十四 所以第一个线程看到初始值是十 然后它设置为十三 第二个线程然后看到值是十三 因为那是共享的 它在他们两者中都是同一个变量

14:34
Set it to fourteen and then they both see fourteen because there's only one variable OK that makes sense so threads You can think of a process as usually only one thread one control thread but you can have multiple threads in the same process and they share the same variables
把它设置为十四 然后他们两个都看到了十四 因为只有一个变量 好的 这 makes sense 所以线程你可以认为过程通常只有有一个线程 一个控制线程 但你可以在同一个过程中有多个线程 并且它们共享相同的变量

14:51
Okay, you do things on the stack that are a little more subtle, threads have their own stack compared to the heap, but we'll get to that later, yes, so they all print very well because they're all running this worker code and they both get control even though they're in a while loop
好的 你做在堆栈上的动作会稍微微妙一些 与堆相比，线程有自己的堆栈 但我们稍后会讨论这个问题 是的 所以 他们都打印得很好 因为他们都在运行这个工人代码 而且他们都能获得控制 即使他们在while循环中

15:17
They can all "the dispatcher switches back and forth between the two" yes "so that's what we're doing today" "in the classroom" "we're exploring how to switch between these two threats in the world." When we only have one CPU "despite this machine" of course, it has multiple CPUs
他们都能 "调度器在两者之间来回切换" 是的 "所以这就是我们今天在做的事情" "在课堂上" "我们正在探索如何在世界上切换这两种威胁。" 当我们只有一台CPU时 "尽管这台机器" 当然，它有多个CPU

15:30
yes so yes to this stage when you create a total of two threads there are actually three so that's a good question because I have a parent thread here that I've been ignoring and my parent thread doesn't have anything interesting to do because it's just waiting or merging with the worker thread I started
是的 所以 是的 到这个阶段 当你总共创建了两个线程时 实际上有三个 所以那是一个很好的问题 因为我这里有一个我一直在忽视的父线程 而且我的父线程没有什么有趣的事情要做 因为它只是在等待或与我开始的工人线程合并

15:56
But they're never done, so this one is never done, but yes, this one has a three, because I created two, and the greatness of the parents, other questions about threads, don't worry, we're going to talk about threads for weeks, weeks, okay, so another term for threads is sometimes lightweight process or LP
但他们永远不会完成 所以这一个永远不会完成 但是是的 这个有一个三个 因为我创建了两个 还有父辈的伟大 关于线程的其他问题 不要担心 我们将谈论线程几个星期几个星期 好的 所以线程的另一个术语有时是轻量级的进程或lp

16:27
It's the execution flow that it controls and it's going to share the address space with other threads those threads that belong to the same process so they see the same memory there as other threads Okay okay why do we need processes So processes are our CPU abstraction This is how we abstract CPU so how do we basically share CPU to multiple processes
就是它控制的执行流 它将与其他线程共享地址空间 那些属于同一进程的线程 因此，它们在那里看到的内存与其他线程相同 好的 好的 我们为什么需要进程 所以进程是我们的CPU抽象 这是我们如何抽象CPU的 所以我们如何基本上将CPU共享给多个进程

16:50
There are three processes that we want to run, and in this case, they can't all run on the same CPU, and we have to switch it in time or in multitasking, so in this example, the first process that we load first loads its context from memory to the actual CPU hardware to the registers
我们想要运行的有三个进程 在这个例子中 它们不能全部在同一个CPU上运行 我们必须在时间上或多任务共享中切换它 所以在这个例子中 我们首先加载的第一个进程将其上下文从内存加载到实际的CPU硬件上 到寄存器

17:08
To the PC heap pointer etc while the other two processes, they are just practically suspended They do not use the CPU and they do not access the registers of the CPU at that time The operating system then at some point decides to pause the running process and switch to another process, wake it up, and load its state on the CPU
到PC 堆指针等 而其他两个进程，它们只是实际上被暂停 它们不使用CPU 它们没有在那个时候访问CPU的寄存器 然后，操作系统会在某个时候决定暂停运行进程 并切换到另一个进程，唤醒它，并加载其状态到CPU上

17:30
How can we do all of this we basically have to keep the context or state of the process when it's not running in memory and it has to be memory that the operating system can access, but the user process can't because we don't want them to interfere, so that's the job of the operating system scheduler again, which holds the context of the paused process
我们如何能做到这一切 我们基本上必须保持进程的上下文或状态 当它不在内存中运行时 并且它必须是操作系统可以访问的记忆 但是用户进程不能 因为我们不想让它们去干扰 所以这是操作系统调度器的工作再次 它保存暂停的进程的上下文

17:51
And then when you run it again, it goes back to that context So that's why we're going to call that context switching We're just switching contexts, right, so these are the states that the process will go through It's simplified a bit but basically one process at a time, a unit processor system can be in a running state
然后当您再次运行它时，它恢复那个上下文 所以这就是为什么我们会叫那个上下文切换 我们只是在切换上下文，对吧 所以这些是进程将经历的状态 它被简化了一些 但基本上一个进程一次，一个单元处理器系统可以在运行状态

18:10
And then the operating system can make a decision at some point and cancel it and say now, this process is ready and put it in this ready queue, if there is an operating system that decides to run them, but you may have many ready processes and then, at some point, the operating system will decide which process to schedule the most ready
然后，操作系统可以在某个时候做出决定并取消它 并说现在，这个进程就准备好了 并将它放置在这个就绪队列中的过程，如果有操作系统决定运行它们 但你可能会有许多就绪进程 然后，在某个时候，操作系统将决定要调度最就绪的进程

18:29
So it schedules it Another process has to be canceled So today we're going to talk about how to make this transition and in a future lecture we're going to look at other policies that should happen when a running process does something like writing to a hard disk, for example, it's very, very slow and you're not using CPU
所以它会调度它 另一个进程必须被取消 所以今天我们将讨论如何进行这个过渡 在以后的讲座中 我们将看一下应该发生的其他政策 当一个运行中的进程执行一些操作时 例如，当它像写入硬盘一样时 这非常非常慢 你没有使用CPU

18:48
When you write to the hard disk, because maybe that right takes milliseconds to complete, so we block that process, we put it in a separate queue, where we don't run that process until the I/O is done, and when the I/O is done, that process is ready to run again, and maybe the operating system scheduler picks it up
当你向硬盘写入时 因为也许那个权利完成需要毫秒 所以我们阻塞那个过程 我们将其放在单独的队列中 在那里我们不会运行那个过程，直到I/O完成 当I/O完成时 那个过程又准备好运行 也许操作系统调度器会挑选它

19:04
Okay, but today we are focused on the transition from running to readiness process Okay okay so well, if you want um, um, I might add these extra bonus points, or maybe they are just for your pleasure and enjoyment But the step-by-step books have a lot of assignments related to reading, and in these lectures they are mainly these small simulators, already written in Python
好的 但是今天我们专注于从运行到就绪过程的过渡 好的 好的 所以嗯 如果您愿意 嗯 我可能会添加这些额外的奖励点 或者它们可能只是为了您的快乐和享受 但是步骤书与阅读相关的作业很多 在这些讲座中 他们主要是这些小型模拟器，已经被编写为Python

19:33
It's just a way to exercise the different components and let you play with policy decisions mainly so that you can see that you understand everything, so if well, I highly recommend that you look at these assignments, and if you do, the first thing you see is a one called process running, so let's take a very brief look at what this does, okay, so I unpacked this thing
这只是锻炼不同组件并让你主要玩转政策决策的方式 以便你看到你理解一切 所以如果嗯我强烈建议你查看这些作业 如果你这样做 你首先看到的是叫做过程运行的一个 让我们很简短地看一下这个做什么 好的 所以我解压了这个东西

20:00
Uni unzipped it I have a couple of things in this file There is always a readme that gives you tons of details on how this thing works We won't go into detail about all of this instead I'm going to run this for you with some basic parameters Can you see these things okay
Uni解压了它 我在这个文件中有几件事 总是有一个readme，它给你提供了大量的细节，说明这个东西如何工作 我们不会详细讨论所有这些 相反 我将为您运行这个，使用一些基本的参数 你能看到这些东西吗 好的

20:24
So I ran it with two parameters, basically which means starting two processes, each process is going to execute three instructions, and there's a 50% chance that the instruction will be executed by the CPU, and this instruction has a 40% probability that it's going to be executed, or vice versa, I don't know some probabilities that it's either CPU or I/O
所以我用两个参数运行了它 基本上这是说 启动两个进程 每个进程将执行三条指令 并且有50%的概率这条指令将被CPU执行 而这一条指令有40%的概率 或者反过来 我不知道有些概率它要么是CPU执行要么是I/O执行

20:45
I forgot how it was defined, but then it generated this trace for us, which we can then use to do some exercises, so we should figure out what is going to be arranged if process zero wants to do two I/O operations and then one CPU instruction However, process one wants to execute a CPU instruction and then two I/O operations
我忘了它是怎么定义的 但是然后它就为我们生成了这个跟踪 我们可以然后用来做一些练习 所以我们应该找出什么将被安排 如果进程零想要执行两个I/O操作然后一个CPU指令 然而，过程一想要执行一个CPU指令，然后是两个I/O操作

21:05
So you have to know a whole bunch of assumptions about the scheduler what's going on here we just assume that a process can use the CPU just once, and we don't take the CPU from the process or until it does I/O We assume that I/O takes five cycles or instructions to complete and I/O first requires you to get the CPU for one cycle
所以你必须知道关于调度器的一大堆假设 在这里发生了什么 我们只是假设一个过程可以使用CPU 只要它一次，我们并不会从过程中拿走CPU 或者直到它进行I/O 我们假设I/O需要五个周期或指令来完成 并且I/O首先需要您获取CPU一个周期

21:30
So that you can start the I/O and this doesn't happen for no reason You need to run some code to start the I/O so check the magic sign of the result So the idea is that you are trying to think about the timeline of what will happen and then add -dash c and you see if your answer is correct This shows what is actually going on for that trace
以便您可以启动I/O 这不会无缘无故发生 您需要运行一些代码来启动I/O 所以检查结果的魔法标志 所以想法是 你试图思考会发生什么时间线 然后添加-dash c，你看看你的答案是否正确 这显示了对于那个跟踪的实际情况

21:52
So you see process zero running first it executes the I/O instructions first and then it needs to wait four more before it is ready to run, and then it will transition to a ready state, but it doesn't necessarily interrupt other processes if it is running well, the process starts in a ready state because at any point in time only one process can use the CPU
所以你会看到过程零首先运行 它首先执行的是I/O指令 然后它需要等待四个更多才能准备好运行 到那时它将过渡到就绪状态 但它不一定会中断其他过程 如果它在运行 嗯，过程一开始在就绪状态 因为任何一点时间只有一个过程可以使用CPU

22:16
But once process zero goes into a blocking or waiting state then it can be scheduled and run, so then it gets it's an instruction from the CPU and then it executes its I/O instructions and it needs to wait five before it is ready to run again You can do some tests like this um-with this job if you have any questions about this issue
但一旦过程零进入阻塞或等待状态 那么它可以被调度并运行，所以然后它得到 它是CPU的一个指令 然后它执行其I/O指令 它需要等待五才能再次准备好运行 你可以做这样的一些测试 嗯 与这个作业 如果您有任何关于这个问题的问题

22:39
yes, I think it's saying something like, it assumes that this weighting, that I/O takes five units of time to complete, it's just kind of pointing out that this is making such a decision, and if we change this, so that I/O actually needs ten instructions, and this transition will be different, yes, there's a lot of information hidden in these things
是的 我想它说的是像 它假设这个加权 那个I/O需要五个单位时间来完成 它只是 kind of 指出这里是在做这样的决策 如果我们改变这个 所以那个I/O实际上需要十指令 这个过渡将是不同的 是的 在这些东西中有很多信息被隐藏

23:07
Once you get into it, if you really care about all the little details, but we'll keep it at an advanced level okay so look at the homework if you're willing okay okay so in this class, we're going to talk about a lot of differences between mechanisms and policies So mechanisms are the things that make things happen and it does the underlying work
一旦你深入进去 如果你真的在乎所有小细节 但我们会保持在高级水平 好的 所以看看作业 如果您愿意 好的 好的 所以在这门课上，我们将讨论机制和政策之间的差异很多 所以机制是使事情发生的东西 它做底层的工作

23:36
So in this case, the mechanism is just being able to run a process to do context switching For our mechanism, we're going to have it's usually about efficiency high performance We don't want to add too much overhead by doing very expensive context switching So the policy uses the mechanism to achieve something smarter So actually, the goal of the policy is to choose the best process to run at a certain point
所以在这种情况下，机制只是能够运行一个进程来执行上下文切换 对于我们的机制，我们将有 它通常关于效率 高性能 我们不想通过做非常昂贵的上下文切换来添加太多的开销 所以政策使用机制来实现更聪明的东西 所以实际上，政策的目标是在某一时刻选择最佳的进程来运行

24:03
So you can have a lot of different metrics here It could be your metric is throughput you have a lot of computations to do and you just want to make sure you get a lot of CPU cycles per second or your metric might be latency you care about response time So eventually you're going to have different policies if you want to optimize for different goals
所以你可以有很多不同的指标在这里 它可能是你的指标是吞吐量 你有很多计算需要完成 并且你只是想确保每秒钟得到很多CPU周期 或者你的指标可能是延迟 你关心响应时间 所以最终你会制定不同的政策 如果你想优化为不同的目标

24:25
We'll talk about that later, but today we're just focusing on the mechanics of how we do context switching okay so we need to make context switching efficient, or at least running our virtualization process efficient, so probably the most efficient way to do this is to just run this process just execute it directly and let things run on the CPU
我们稍后会讨论这个问题 但今天我们只是专注于机制 我们如何做上下文切换 好的 所以我们需要使上下文切换效率 或者至少运行我们的虚拟化进程效率 所以最有效的方法可能是只是运行这个进程 只是直接执行并让东西在CPU上运行

24:48
Um, so when you create a process, the operating system will just run, will just jump to main and let it run, until it calls exit and then the operating system will be controlled again, which may work in very cooperative systems if you have a live system where each process can trust the other
嗯 所以当你创建一个进程时 操作系统将只是运行 将只是跳转到main并让它运行，直到它调用exit 然后操作系统将再次得到控制 这可能在非常合作的系统中工作 如果你有一个实时系统 其中每个进程都可以信任另一个

25:07
But it's not practical in today's environment, so we have to deal with two challenges, one is how do we deal with the restricted actions that a process might want to do It wants to access the I/O device We can't give user-level processes direct access to the I/O device because they can cause problems They can read data from other processes
但在今天的环境中不实用 所以我们必须处理两个挑战 一个是我们如何处理一个进程可能想要执行的受限操作 它想要访问 I/O设备 我们不能让用户级别的进程直接访问I/O设备，因为它们可能会引起问题 它们可能会读取其他进程的数据

25:25
We also have to worry if the process runs indefinitely If it contains a wild program the programmer doesn't even intend to do it but it has a bug If the process runs indefinitely If it contains a wild program the programmer doesn't even intend to do it, but it has an error and it never quits
我们还必须担心如果进程运行无限期 如果它包含一个野的程序 程序员甚至没有打算这样做 但它有一个错误 如果进程运行无限期 如果它包含一个野的程序 程序员甚至没有打算这样做，但它有一个错误 并且它永远不会退出

25:41
Call Exit so we must have a way so that we can regain control of the operating system So, instead of just executing it directly we will do what is called limited direct execution Most of the time, we just run the process and its instructions but we have some ways that, when we want, can take control
呼叫 退出 因此我们必须有一种方法，以便重新获得对操作系统的控制 所以，而不是只是直接执行 我们将执行被称为有限直接执行的方法 大多数时候，我们只是运行进程及其指令 但我们有一些方法，当我们想要时，可以获取控制权

25:59
Okay, so how will we solve the first problem, which is when the user process wants to do something restricted For the solution to this problem, we need the help of hardware Every modern architecture will have at least two levels of privilege One lower level of privilege for user level processes and then a higher privilege for the operating system
好的 那么，我们将如何解决第一个问题，即 当用户进程想要执行一些受限的操作时 对于这个问题的解决方案，我们需要硬件的帮助 每个现代架构都将至少有两个特权级别 一个较低级别的特权用于用户级别进程 然后，一个较高的特权用于操作系统

26:23
Modern architectures have many more levels of this because it is useful for virtual machines to be able to make more distinctions, but we will assume that we have two levels, the user level and the kernel level, so when you run at the kernel level the hardware can execute whatever instructions it wants to execute without causing any pitfalls or exceptions
现代架构有许多更多的这个级别 因为它对于虚拟机能够有更多的区分是有用的 但我们将假设我们有两个级别 用户级别和内核级别 所以，当你在内核级别运行时 硬件可以执行它想要执行的任何指令，而不会导致任何陷阱或异常

26:45
You know, to access certain registers and if the user process tries to do that you will get an exception and trap the operating system okay so now the question is how do we get them to access the device if the user level process can't access the device So the solution to this problem is to add a system call
你知道，要访问某些寄存器 而如果用户进程试图这样做 你将得到异常并陷阱到操作系统 好的 所以现在的问题是 如果用户级别进程无法访问设备 我们如何让他们访问设备 因此，对于这个问题的解决方案是添加系统调用

27:04
I'm sure you've all called system calls but you probably haven't seen how they're implemented So, a system call is basically a function implemented by the operating system So, let's look at that in detail okay it's a memory diagram um address space of the process plus the contents of the operating system So, process p or user level process wants to use its system call and call sys read
我相信你们大家都叫过系统调用 但你可能没有看到它们是如何实现的 所以，系统调用基本上是由操作系统实现的一个函数 所以，让我们详细看看那个 好的 这是一张内存图 嗯 进程的地址空间 加上操作系统的内容 所以，进程p或用户级别进程想要使用它的系统调用并调用sys read

27:33
That read function lives in the address space of the operating system, but he can't call this read directly because if you can jump from a process anywhere in the operating system at will, then you can do arbitrary weird functions with all these types of security vulnerabilities, so we have to restrict entry points into the operating system
那个read函数生活在操作系统的地址空间中 但他不能直接调用这个read 因为如果你可以任意地从一个进程跳转到操作系统的任何地方 那么你就可以做任意的奇怪函数，并具有所有这些类型的安全漏洞 所以我们必须限制进入操作系统的入口点

27:54
Only so that they can jump to very specific places Generally the process can't see what the operating system is in memory where that's not part of its visible address space So, if p wants to call read it will have to find another way to do it The way we do this is by using a system call
只使它们可以跳转到非常特定的地方 一般来说，进程无法看到操作系统在内存中的内容那里 那不是其可见地址空间的一部分 所以，如果p想要调用read 它将不得不找到另一种方法来做这件事 我们这样做的方法是使用系统调用

28:14
So maybe you've seen this in three, four, five, maybe it's not the idea that when you want to call a system call, the exact instructions are different on every architecture, we're using a style architecture like xeighty-six, which is very similar to what you do in our xv project, six, and unified environment
所以也许你已经在三四五中看到过这个 也许不是主意是当你想要调用系统调用时 确切的指令在每个架构上都有所不同 我们在这里使用类似于x八十六的风格架构 这将非常类似于你在我们的xv项目中所做的项目 六和统一的环境

28:40
But the idea is that there's this special interrupt instruction that you pass to different interrupts with different numbers and sixty-four corresponds to the system calling the interrupt, so before we make that interrupt, even though the process moves a special value to a special register, the operating system knows how to interpret it, and it's just a convention being set
但主意是有这个特殊的中断指令 你传递给不同中断的不同数字 六十四对应于系统调用中断 所以在我们做出那个中断之前 尽管这个过程将一个特殊值移动到一个特殊寄存器 操作系统知道如何解释它 这只是一个正在设置的约定

29:03
Exactly which system calls correspond to which numbers what we put in which register But that's the convention here is that reading the system call will correspond to the number six We know to look for it in this particular register What happens when we call break sixty-four Of course, the call just moves to a specific register
确切是哪些系统调用 对应于哪些数字 我们放什么东西在哪个寄存器中 但这是这里的约定 是读取系统调用将对应于数字六 我们知道要在这个特定寄存器中查找它 当我们调用中断六十四时发生什么 当然，调用只是移动到一个特定寄存器

29:25
It's just a normal instruction, and then the process calls this special interrupt instruction.64 The hardware knows what to do at that point is to move to kernel mode, it sets the magic bits in the processor, it tells us what mode we're in and switches from user to kernel, and then it knows that it needs to look for the entry number or index number in this trap table
这只是一个正常指令 然后过程调用这个特殊的中断指令六十四 硬件知道在那个点应该做什么 是转移到内核模式 它设置处理器中的魔法位 告诉我们我们当前处于什么模式 并切换从用户到内核 然后它知道需要查找这个陷阱表中的入口号或索引号

29:54
Sixty-four what's going to be in there There's going to be a function pointer pointing to the system call code Okay, because there's other pitfalls like dividing zeros or memory failures All of these have functional pointers associated with it, but sixty-four is the system call Okay, I think I've said everything, so we have a table
六十四 里面会有什么 那里会有一个函数指针指向系统调用代码 好的 因为这里有其他陷阱 如除零或内存故障 所有这些都有与之关联的功能指针 但六十四是系统调用 好的，我认为我已经说过所有了 所以我们有一个表

30:14
That's the system call table, and the entry six there is what we care about, okay, so when we call this interrupt, and then we jump into kernel mode, and we find the entry of sixty-four there, which is a function pointer, and we execute a function from there, and that's the system call code, and the system call code mainly handles the system call
那是系统调用表 在那里的入口六是我们关心的 好的 所以当我们调用这个中断时 然后我们跳入内核模式 我们在那里找到六十四的入口 这是一个函数指针 我们从那里开始执行一个函数 这是系统调用代码，系统调用代码主要处理系统调用

30:42
And look at you know, it's just the operating system code, and you're going to look at it in detail in project two, and you can look at the value of that register, and then you use that value to index your system call table and follow that pointer to call that function, because there's really a function pointer there, so you're going to look at those functions in project two
并查看你知道的 这只是操作系统代码，你将在项目二中详细查看 你可以查看那个寄存器的值 然后你使用那个值来索引你的系统调用表 并跟随那个指针来调用那个函数 因为那里确实有一个函数指针 所以您将在项目二中查看这些函数

31:10
New system calls are being created so added to this table is looking at how all of this works So if you have any questions about this yes yes I think this slide might answer your question When you call read you have a buffer This buffer exists in user space
正在创建新的系统调用 所以添加到这个表中 正在查看所有这些如何工作 所以有任何关于这个问题的疑问 是的 是的 我认为这个幻灯片可能会回答你的问题 当你调用read时 你有一个缓冲区 这个缓冲区存在于用户空间

31:38
The kernel has to be very careful to trust that it has to do some checks to make sure you don't give it a bad pointer but once it passes those checks and cv does its job, it can And then, you have a few different ways to do it You can imagine that the way cis read works is by reading suggestions and using some temporary memory
内核必须非常小心地信任那个 它必须做一些检查来确保你没有给它一个坏指针 但是一旦它通过了那些检查，cv完成了工作，它就可以 然后，你有几种不同的方式来做它 你可以想象cis read的工作方式是通过读取建议并使用一些临时内存

31:59
And then, one last replication, back to your user level, that's the most straightforward way to do that, some people are able to do something complicated, and they call it a zero-copy read or a zero-copy network operation, in which case you can read directly to the buffer, but let's assume we're doing replication
然后，在最后进行一次复制，返回到你的用户级别 这是实现这一目标的最直接的方式 有些人能够做一些复杂的事情 他们会把它叫做零复制读取或零复制网络操作 在这种情况下，你可以直接读取到缓冲区 但我们假设我们在进行复制

32:18
In most cases from the buffer that you store here back to the user So, is that enough to answer the question yes there is no well So think about this because it's still like the process that thread pthread is running and now it's doing this work in the OS under the name of process p we'll see later
在大多数情况下 从你存储在这里的缓冲区返回到用户 那么，这是否足够回答问题 是的 没有井 所以想想这个 因为它仍然像线程pthread正在运行的过程一样 而现在它正在os中做这项工作，以过程p的名义 我们稍后将看

32:49
Here we are going to use a mechanism similar to here for context switching but in this case we are not switching to another thread we are actually going to use a different stack related to procedure p because the stack used at the user level must be different from the stack you use in the kernel because we cannot always trust the user level
在这里我们将如何使用与这里类似的机制进行上下文切换 但是但是，在这种情况下，我们不是在切换到另一个线程 我们将实际上使用与过程p相关的不同堆栈 因为用在用户级别的堆栈 必须不同于你在内核中使用的堆栈 因为我们不能总是信任用户级别的

33:12
So we're going to switch stacks but it's going to be a stack that's still tied to a specific process and once you're in the operating system, you can see any process in the address space and other good issues okay so overall we basically need to have both modes user-level and kernel where you can execute any instruction when you're in kernel mode
因此我们将切换栈 但将是一个仍然与特定过程相关联的栈 而且一旦你在操作系统中，你可以看到任何过程 地址空间 还有其他很好的问题 好的 所以总的来说 我们基本上需要有这两种模式 用户级别和内核 当你处于内核模式时，你可以执行任何指令

33:39
The key to getting into kernel mode is executing the system call instruction to execute that special interrupt instruction after you finish executing that and there's also a special trap return instruction that switches you back to user mode which switches you back to using your own stack, and so on okay let's take a break now okay
进入内核模式的关键在于执行系统调用指令 执行那个特殊的中断指令 在你执行完那个之后 还有一个特殊的陷阱返回指令，它可以将你切换回用户模式 嗯 它将你切换回使用自己栈的方式，等等 好的 我们现在休息一下 好的

34:04
Again, I think it's important for both of you to get to know new people you need new project partners So please talk to at least two people at this stage of the semester about the courses what your favorite courses have been so far why you like it What courses have you enjoyed outside of us yes
再次 我认为对你们都很重要去了解 新的人 你们需要新的项目伙伴 所以请至少与两个人交谈 在这个学期的这个阶段，谈谈课程 到目前为止，你最喜欢的课程是什么 你为什么喜欢它 你在我们之外喜欢过哪些课程 是的

34:18
Please talk to two people okay okay let's start again Can I hear something about a good course outside of us Has anyone heard of a course outside of us that is really good would you recommend a course to others here I've been imagining I see hands but I see no one raises their hands
请与两个人交谈 好的 好的 让我们再次开始 我可以听一些关于我们之外好课程的事情吗 有人听说过我们之外的课程吗 那真的很好 你愿意推荐给在这里的其他人的课程吗 我一直在想象 我看到手 但我看 没有人举手

35:55
Some good courses outside of us yes thank you amazing what are you doing you read drama oh sounds wonderful yes There are other courses that you would recommend to others please forgive me yes psychology 532 sounds like other people have taken this class as well, what course is this oh okay
我们之外的一些好课程 是的 谢谢你，太棒了 你在做什么 你读戏剧 哦 听起来很美妙 是的 还有其他的课程你愿意推荐给别人吗 请原谅 是的 心理学532 听起来像是其他人也上过这门课，这是什么课程 哦 好的

36:28
They're all positive, right, they're all beneficial, and everything we do in computer science is good, of course, good, so we're going to move on to context switching, so we've figured out how to get user processes to do system calls to privileged instructions that are inside the operating system, and the next problem we're going to solve
他们都是积极的，对吧 都是有益的 我们计算机科学所做的一切都有益处 当然棒极了 好的 所以我们将继续讨论上下文切换 所以我们已经解决了如何让用户进程能够执行 这些在操作系统内部的特权指令的系统调用 我们接下来要解决的问题是

36:50
How to take CPU from a process that doesn't want to call exit or malicious or buggy OK so how do we do that, again "There are two parts" "Here's the policy on when to take CPU from a process" "We'll talk about that in the next few lessons today"
如何从不想调用exit的进程中夺取CPU 或者是恶意的或者是有bug的 好的 那么我们如何做到这一点，再次 "这有两个部分" "这里有政策决定何时从进程中拿走CPU" "我们今天的接下来的几堂课里会讨论那个问题"

37:10
"This is the mechanism of how you physically tear it apart" "From the CPU of a process that still wants to use it" "It's still ready to run" So we often see the separation between policy and mechanism as an important topic.
"这就是你如何物理撕开的机制" "来自还想使用它的进程的CPU" "它仍然处于运行准备状态" 因此，我们经常会看到政策与机制之间的分离是一个重要的主题。

37:25
"Without those two things mixed together, keeping it clean can be very helpful." "This mechanism is really just some kind of low-level thing" "The policy can be summoned and dependenced" that works well that way okay so the mechanism again we're thinking about scheduling mechanisms how we can actually switch contexts between different processes
"没有那些两件事混在一起，保持清洁就会很有帮助。" "这个机制实际上只是某种低层次的东西" "该政策可以召唤和依赖" 那就是那样工作得很好 好的 所以机制再次 我们正在考虑调度机制 我们如何实际上在不同进程之间切换上下文

37:45
So the operating system has something called a scheduling loop basically whenever it's running it's switching from one process to another but you can think of it as a running process when it's actually running the operating system isn't so it's just an abstraction where the running process is going to run what we call a time slice
所以操作系统有一个被称为调度循环的东西 基本上每当它在运行时 它是从一个进程切换到另一个进程 但你可以想 作为一个正在运行的进程 当然，当它实际上运行时 操作系统不是 所以 这只是一种抽象 正在运行的进程将运行我们所称的时间片

38:07
Like the amount of time in a hundred milliseconds this will be very standard and then, at some point, the operating system will gain control and we will see how the operating system gains control and it stops processing a process and it saves its context including all its registers and so on and so on and so on and then it loads the context of that other process onto the architecture
就像一百毫秒的时间量 这将是非常标准的 然后，在某个时候，操作系统将获得控制 我们将看到如何做到这一点 操作系统获得控制 并且它停止处理a进程 并且它保存其上下文 包括其所有寄存器和如此等等 然后它将那个其他进程的上下文加载到架构上

38:27
So how do we actually take control of the operating system and then exactly what context do we need to save and recover okay so fifty years ago many years ago people would do something called collaborative multitasking So like MS DOS, it would do that The idea here is that you probably don't have a way to remove the CPU directly from the runtime
那么我们如何实际获取操作系统的控制权 然后确切我们需要保存和恢复哪些上下文 好的 所以五十年前 很多年以前 人们会做被称为协作多任务处理的事情 所以像ms dos一样，它会这样做 这里的想法是，你可能没有直接从运行过程中移除CPU的方法

38:50
You need to wait for the process to voluntarily release it so that it can release it like we see with a system call Before you can imagine it, you're going to call the operating system instead of just doing a system call for you and it decides to switch to another person we're in the operating system and we can do whatever we want
你需要等待该过程自愿释放它 这样它才能通过系统调用像我们看到的那样释放它 在你能够想象之前，你会调用操作系统 而不是仅仅为你做系统调用 它决定切换到另一个人 我们在操作系统中 我们可以做任何事情 我们想要什么就做什么

39:06
Or that process might visit a page that isn't currently in main memory and the operating system will take over control at that point so that it can swap out that memory page and swap out from the hard drive into main memory at that point, like switching to another process or when you do anything that doesn't work if you divide by zero
或者那个过程可能访问一个目前不在主内存中的页面 操作系统会在那个点接管控制 以便它可以将那个内存页面换出 并从硬盘换入主内存 在那个点，s可以做其他事情 比如切换到另一个过程 或者在你做任何事情无效时 如果你除以零

39:26
That's the trap of the operating system, the operating system can do whatever it wants, so it's not enough to be a point of control, so these collaborative multitasking environments, they include this other system call which our system also does, called yield yield just does one thing, which is to get into the OS
那就是操作系统的陷阱 操作系统可以随心所欲地做任何事情 所以这不足以成为控制点 所以这些协作多任务环境 它们包括这个其他系统调用 哪个我们的系统也做，叫做yield yield只是做了一件事，就是进入os

39:45
And let the OS decide if you want to schedule another process or not so in many ways it's like a null operation or a null system call It's just a hint that the OS doesn't need to switch to another process if you don't want to So you can imagine working this way, p one yield system call is called or not
并让os决定是否想要安排另一个进程或不 所以从许多角度来看，它就像是无效操作或null系统调用 它只是os不需要切换到另一个进程的提示 如果不想 所以你可以想象这种方式工作，p one yield系统调用是否被调用

40:01
It looks like what we've seen earlier except what happens is that the OS will go back to process two and it will look like it just called back from that system but it will go back to another process because process two may have called yield sometime in the past and it's just waiting for yield
它看起来就像我们之前看到的一样 除了发生的是，os将返回到过程二 它将看起来就像刚刚从该系统调用返回一样 但它将返回到另一个过程 因为过程二可能在过去某个时候调用了yield 并且它只是在等待yield

40:24
So when p-two calls yield again, it will return to that yield call from process one that was called before, so it's kind of like a function call, but when you return from those functions, you switch stack and address space Okay, let's look at this in more detail
所以当p二再次调用yield时 它将返回到 它将从之前调用过的process one返回该yield调用 所以这就有点像函数调用 但是当你从那些函数返回时，你会切换堆栈和地址空间 好的，让我们更详细地看看这个

40:48
Obviously you can't just have collaborative multitasking because we can't guarantee that we're actually going to call yield or we have a page glitch or a system call so we need a mechanism to make sure that the operating system gets control over a scheduled interval so the way we do that is we have a timer
显然你不能仅仅有协作多任务处理 因为我们不能保证我们实际上会调用yield 或者我们有页面故障或系统调用 所以我们需要一个机制，以确保操作系统在定期间隔内获得控制 所以我们这样做的方式就是我们有一个定时器

41:08
Periodic startup like every millisecond is one thing that is done on the hardware It could be a timer chip that is separate from the main CPU or part of the main CPU and you have a way of generating and interrupting every millisecond or some fixed duration, so when that timer interrupt happens it's like that piece of code path that we looked at to handle the interrupt before
定期启动 就像每一毫秒 这将是硬件上完成的一件事 它可能是一个与主cpu分离的定时器芯片 或者是主cpu的一部分 你有一种生成和中断的方式 每隔一毫秒或某个固定的持续时间 所以当那个定时器中断发生时 它就像之前我们查看以处理中断的那段代码路径一样

41:30
We switch to kernel mode and we go into that interrupt handler and we look at which interrupt is being processed and it's going to be a timer interrupt and then we do the work related to that OK and of course, there's a lot of detail there for example that users can't block timer interrupts Sometimes interrupts are maskable which means they don't actually cause interrupts
我们切换到内核模式 我们进入那个中断处理程序 我们查看正在被处理的中断是哪个 它将是定时器中断 然后我们做与那相关的工作 好的 当然，那里的细节有很多 例如，用户不能屏蔽定时器中断 有时中断是可屏蔽的 这意味着它们实际上不会导致中断

41:53
Um, if the user can mask that, it won't work okay so let's look at how this works So we have a non-collaborative process running it's not doing system calls or calling yield It's running in user space doing whatever it wants to do and then, at some point, this timer break happens
嗯 如果用户可以屏蔽那个，它就不会工作 好的 所以让我们来看看这是如何工作的 所以我们有一个非协作的过程在运行 它不在做系统调用或调用yield 它正在用户空间运行 做它想做的任何事情 然后，在某个时候，这个定时器中断发生

42:17
This is generated by the hardware, so the hardware does a whole bunch of things related to that timer, and then, oh, it will save the value of a register to the kernel stack, and you can think of this as what happens when you go into any program or function, and you have to save the pre-run state so that we can go back and know the value of the register and other things
这是由硬件生成的 所以硬件做了与那个定时器相关的一大堆事情 然后，哦 它将保存一个寄存器的值到内核栈 你可以把这看作是当你进入任何程序或函数时发生的情况 你必须保存运行前的状态 以便我们可以返回并知道寄存器的值和其他东西

42:39
We can't just push these registers into the user stack because the user stack may not be in a known state At this point, it may already have some problems we don't trust the user stack so we will have a kernel stack associated with each process here and we will save the state here It's like an array that you push things in
我们不能只是将这些寄存器推入用户栈 因为用户栈可能不在已知的状态 在这个点上，它可能已经有一些问题 我们不信任用户栈 所以我们将有一个与每个进程相关的内核栈 我们将在这里保存状态 它就像一个数组 你推入东西

43:03
You track where you are, you have memory available there, and then, we switch to kernel mode, and that's what I said earlier, remember that we have user mode and kernel mode, and we're transitioning to kernel mode, and then we jump into the trap handler associated with this timer and it's like the previous picture where we look at which interrupt number is the timer interrupt
你跟踪你的位置 你在那里有可用的内存 然后，我们切换到内核模式 这就是我之前所说的 记住我们有用户模式和内核模式 我们正在过渡到内核模式 然后，我们跳入与这个定时器相关的陷阱处理程序 这就像之前的图片 我们查看是哪个中断号是定时器中断

43:21
We get the function pointer, and then we call that timer interrupt handler, so it makes sense so far, it's just a hardware event happening, and then we transition to the operating system when that timer interrupt happens, so now we start running the code associated with the trap handler
我们获取到函数指针 然后我们调用那个定时器中断处理程序 所以到目前为止这是有意义的 那只是硬件事件发生了而已 然后我们过渡到操作系统 当那个定时器中断发生时 所以现在我们开始运行与陷阱处理程序相关联的代码

43:41
For handling timer interrupts it will have some policy here that will decide whether it wants to keep running or which ready process should be scheduled What should it schedule So, a whole piece of policy code that will be related to this statement that we will look at later, but at some point, it may decide that it does want to switch to another process
用于处理定时器中断 它这里会有一些策略 它将决定 它想要继续保持运行吗 还是应该调度哪个就绪的进程 它应该安排什么 所以，将与这个陈述相关的一整段政策代码 我们将稍后查看 但到某个时候，它可能会决定是 它确实想要切换到另一个进程

44:06
B, that's where we get into the scheduler the mechanism of doing the underlying work after the policy decides which process we should switch to so let me stand in a different place so I can take a better look at this with you OK so now we need to save the register of a again So notice that we have already saved the register of a once on the kernel stack
B，这就是我们进入调度器的地方 执行底层工作的机制 在政策决定我们应该切换到哪个进程之后 那么让我在一个不同的地方站住 这样我就可以和大家一起更好地看看这个 好的 所以现在我们需要再次保存a的寄存器 所以请注意我们在内核栈上已经一次保存了a的寄存器

44:31
These are the registers that are active when this user-level process is executed, and we've modified those registers a little bit now, right, because we've gone through this kernel code, done some policy work, done some things, so we need to save the registers for this process because it's already running somewhere in the operating system
这些是在执行这个用户级别进程时活跃的寄存器 我们现在已经稍微修改了那些寄存器，对吧 因为我们已经走过了这个内核代码，做了一些政策工作，做了一些事情 所以我们需要保存这个进程的寄存器 因为它已经在操作系统中运行在某个地方

44:53
We are going to save it to memory and it will be called process structure or process control block or PCB is a different term that you may hear there so that each process will have a process structure that is associated with it PCB it is some memory and some data structure that the OS wants to manage so that the policies can be viewed
我们将将其保存到内存中 这将是 它被称为进程结构或进程控制块 或pcb是您可能会在那里听到的不同术语 所以每个进程都将有一个进程结构 与它相关的pcb 它是一些内存和一些数据结构，os想要管理，以便可以查看政策

45:13
Maybe that way we can save our registers into memory that's the register that we're changing here and then, now we've chosen a difficult point where we want to run b so we need to restore our current register to the value of b whatever is stored in its procedure structure so we're basically going to untangle and go into b
也许这样我们可以将我们的寄存器保存到内存中 那是我们在这里更改的寄存器 然后，现在我们已经选择了一个困难的点 我们想要运行b 所以我们需要将我们的当前寄存器恢复 b的值 无论其过程结构中存储了什么 所以我们基本上要解开并进入b

45:39
Well, then we're going to switch to B's kernel stack and then we call this special instruction return from trap which will now go back to B because we're using B's kernel stack now and we have B's registers so when we execute that special instruction
嗯，然后我们将切换到b的kernel栈 然后我们调用这个特殊指令return from trap 这将现在返回到b 因为我们现在正在使用b的kernel栈 并且我们有b的寄存器 所以当我们执行那个特殊指令时

45:56
What is the hardware associated with the trap instruction return What does it do Um, it knows the kernel What are all the stacks of the current kernel Um, it will recover anything on the stack that is pointed to the register It will be the bee Um the register associated with the user-level process It will switch back to user mode and then it will jump to the instruction pointer or PC of B
与陷阱指令返回相关联的硬件是什么 它做什么 嗯，它知道内核 当前内核的所有栈是什么 嗯 它将恢复栈上的任何内容 那是被指向到寄存器的 这将是蜜蜂 嗯 与用户级别进程相关联的寄存器 它将切换回用户模式 然后它将跳转到b的指令指针或pc

46:22
Because that's part of being saved here by the kernel stack and then when we do that we're back to process b so what's so difficult about this a lot of difficult things it's a little bit less intuitive You know before process a, we've seen some signs that process a just made a system call and the interrupt associated with it
因为这是在这里被内核栈保存的一部分 然后当我们这样做时 我们就回到了过程b 所以这个有什么困难的地方 有很多困难的地方 它有些不太直观 你知道 在过程a之前，我们已经看到了一些迹象 过程a刚刚做了系统调用，并与其相关联的中断

46:45
It's doing the same thing when we just simply do a system call or it saves our registers to the kernel stack and we just go to a different trap processor when we do a system call so you go into the operating system, so um, it's a little confusing sometimes like why do you save a register twice
当我们只是简单地做了系统调用时，它也在做同样的事情 或者它将我们的寄存器保存到内核栈 我们只是去了不同的陷阱处理器 当我们做系统调用时 所以你进入操作系统，所以嗯 它有些困惑 有时像为什么你要保存寄存器两次

47:01
So think about it here as we are saving the registers associated with the user level process again here we are saving the registers associated with what process A is doing in the operating system when we make this switch So the challenging question for you is when we restore the registers from B
所以想想这里 正如我们正在保存与用户级别进程相关联的寄存器 再次在这里 我们正在保存与过程a在操作系统中做的内容相关联的寄存器 当我们进行这个切换时 所以对你来说，挑战性的问题在于当我们从b恢复寄存器时

47:20
What it might be doing where it returns at that point Basically, what b does when it calls the operating system is it just called the switch as well, so B just made this statement and we now tell it the recovery register that is associated with what it did last time in the operating system when it last entered the operating system
它可能正在做什么 它在那个点返回到哪里 基本上，b在调用操作系统时做的事情就是 它也刚刚调用了switch 所以b刚刚做了这个声明 我们现在告诉它恢复寄存器 那与它上次在操作系统中做的内容相关联的 在它最后一次进入操作系统时

47:48
So it's a set invariant that you always go back to this state, right, and that's where you did this toggle here, and that's why you can b-back what it did last time in the operating system, restore its kernel stack, go back from there, } um, and then it goes back to it, you know what it used to do at the user level
所以这是一种被设置的不变量 你是总是返回到这个状态的对吗 你在这里做了这个切换的地方 这就是你为什么可以恢复b回它上次在操作系统中做的内容 恢复它的内核栈 从那里返回 } 嗯 然后它会回到它的 你知道它在用户级别曾经做什么的

48:21
So unfortunately, this topic is like one of the more complex ones I think the whole semester is on the first day of content, but that might motivate you to try to remember some things about registers and program counters and stacks and other things that you learned at 354 Well, the specifics of this that we'll look at again in the next class
所以不幸的是，这个话题像是其中更复杂的一个 我想整个学期都在第一天的内容上 但这可能会激励你尝试记住一些关于寄存器和程序计数器的东西 和栈 以及你在354学到的其他东西 嗯 这个的具体细节 我们将在下一次课堂上再次查看

48:44
This will become more specific later in the semester again when you do a project in xv6 you look at some scheduling code because you need to implement a new scheduling policy so you don't need to deal with it may not be this mechanism scheduling code but you look at the policy code that uses that, so because if you do these things wrong
这将变得更加具体 在本学期的后期再次 当你在xv6中做项目时 你看一些调度代码 因为你需要实现一个新的调度策略 所以你不需要处理 可能不是这个机制 调度代码 但你会看使用那个的政策代码，所以 因为如果你做错了这些

49:07
It's like painful debugging, and that's why I love it, often you have to save registers to the kernel stack like hardware does, and if there's no hardware to support that, and you need to write instructions that you know save registers to stack, it's really hard to do that without modifying any registers in your code, so the hardware does all the copying work for you
就像痛苦 痛苦的调试 这就是我为什么也喜欢它 常常必须像硬件那样将寄存器保存到内核栈 如果没有硬件支持那个 并且你需要写 你知道保存寄存器到栈的指令 做那项工作真的很难 没有修改你代码中的任何寄存器 所以硬件就负责为你做所有需要的复制工作

49:35
This is described in similar detail in textbooks so I highly recommend that you read this part of the chapter if it's not clear if it's still clear I think it usually takes a few readings to make this part clear Okay I finished today much faster than expected but I'll go back a little bit to this summary So today we learned how to virtualize the CPU
这在教科书中描述得相似详细 所以我强烈建议你阅读这一章的这一部分 如果这还不清楚 我认为通常需要阅读几次才能使这部分清楚 好的 我今天结束得比预期快得多 但我会稍微回顾一下这个总结 所以今天我们学习了如何虚拟化CPU

50:00
Our abstraction is that there are processes and then there are threads We are going to use time sharing to share the processor across multiple processes A key part of this event is being able to perform system calls that allow us to access the device using special instructions in the kernel and then this is the mechanism of switching contexts, it allows us to switch to different processes
我们的抽象是进程 有进程 然后有线程 我们将使用时间共享来共享处理器跨多个进程 这一事件的关键部分是能够执行系统调用 那允许我们使用内核中的特殊指令访问设备 然后这是切换上下文的机制，它允许我们切换到不同的进程

50:26
Okay, in the next class, we're going to talk about strategy, strategy is much easier than understanding, we just have to make high-level decisions, it's not yet 12:15, policy is going to be a lot simpler, because we just have to decide what processes to run, let me summarize the details, thank you, because it's still early
好的 在下一次课堂上我们将讨论策略 策略比理解要容易得多 我们只需要做出高层次的决定 现在还不是十二点十五分 政策将会变得简单得多 因为我们只需要决定要运行哪些过程 让我来总结一下细节 谢谢 因为现在还很早

50:51
Okay, so remember that the lecture starts at 12:15 p.m. Our Project One is already available, please come to the discussion section to answer the questions to get all your questions, and now the teaching assistants and peer mentors have a lot of hours in the lab to help you with the lab definitely register on Piazza
好的 所以记住讲座在下午十二点十五分开始 我们的项目一已经可用 请来讨论部分回答问题，以获取所有你的问题 回答完毕 现在助教和同伴导师在实验室里有大量的工作时间 来帮助你在实验室 肯定在piazza上注册

51:07
If you're still on the waiting list, come to me, we'll add you to the course and I'll talk to you about the policy to close this on Thursday
如果你还在等待名单上 来找我，我们会把你加进课程 周四我会和大家讨论政策 关闭这个
