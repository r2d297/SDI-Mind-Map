![alt text](image-22.png)


image: snapshot of the file ssystem
![alt text](image-23.png)

![alt text](image-24.png)

-: In the last section, we had a long discussion -: 在上一节中，我们进行了长时间的讨论

about the relationship between a container and an image. 关于容器与镜像之间的关系。

We had said that a container is a running process 我们曾说过容器是一个正在运行的进程

along with a subset of physical resources on your computer 以及计算机上分配给该进程的一部分物理资源

that are allocated to that process specifically. 专门分配给该进程的那些资源。

We also spoke a little bit about the relationship 我们也稍微谈了一下它们之间的关系

between an image and a running container. 镜像和正在运行的容器之间。

Remember, an image 请记住，镜像

is really kind of a snapshot of the file system, 实际上有点像文件系统的快照，

along with a very specific startup command as well. 以及一个非常具体的启动命令。

Now, one thing that I wanna mention very quickly here, 现在，我想在这里快速提到一件事，

in the last section, we spoke a little bit 在上一节中，我们稍微讨论了一些。

about the separation or the kind of the isolation 关于这些资源的分离或隔离方式

of these resources through a technique called namespacing. 通过一种称为 namespacing 的技术实现。

And we also said that we could limit 我们还说过我们可以限制

the amount of resources used 所使用的资源数量

by these control group things as well. 也被这些控制组（control group）机制所使用。

Now, this feature of namespacing and control groups 现在，这个命名空间（namespacing）和控制组（control groups）的特性

is not included by default with all operating systems, 并非所有操作系统默认都包含，

even though in the last section, 即便在上一节中，

I had kind of specifically said like, 我当时有点明确地说过，

oh yeah, your operating system has a kernel, too. 哦对了，你的操作系统也有一个内核。

These features of namespacing and control groups 这些命名空间和控制组的特性

are specific to the Linux operating system. 是特定于 Linux 操作系统的。

So namespacing control groups belong to Linux, 所以命名空间和控制组属于 Linux，

not to Windows, not to macOS. 不属于 Windows，也不属于 macOS。

So that might make you kind of question or wonder 所以这可能会让你有点疑问或好奇

how are you running Docker right now? 你现在是如何运行 Docker 的？

You know, we are running a Docker client 你知道，我们正在运行一个 Docker 客户端

and we are running Docker containers 并且我们正在运行 Docker 容器

on a macOS or a Windows operating system. 在 macOS 或 Windows 操作系统上。

How is that happening if these are Linux-specific features? 如果这些是 Linux 特定的功能，那这是怎么发生的？

Well, here's what's happening behind the scenes. 好吧，下面是幕后发生的情况。

When you installed Docker for Windows or Docker for Mac 当你安装 Docker for Windows 或 Docker for Mac 时

just a moment ago in the last couple sections, 就在前几节的刚刚那一会儿，

you installed a Linux virtual machine. 你安装了一个 Linux 虚拟机。

So, so long as Docker up here is running, 只要上面的 Docker 在运行，

you technically have a Linux virtual machine 从技术上讲，你有一台 Linux 虚拟机

running on your computer. 在您的计算机上运行。

Inside of this virtual machine is 在这个虚拟机内部是

where all of these containers are going to be created. 这些容器将被创建的地方。

So inside the virtual machine, we have a Linux kernel, 所以在虚拟机内部，我们有一个 Linux 内核，

and that Linux kernel is going to be 并且那个 Linux 内核将会

hosting, running processes inside of containers. 在容器内托管、运行进程。

And it's that Linux kernel 而且就是那个 Linux 内核

that's going to be in charge of limiting access 这将负责限制访问

or kind of constraining access or isolating access 或某种程度上约束访问或隔离访问

to different hardware resources on your computer. 到你电脑上的不同硬件资源。

You can actually kind of see 你现在实际上可以通过打开终端来实际看到

this Linux virtual machine in practice 这个 Linux 虚拟机的运行情况

by opening up your terminal right now. 就现在。

And if you run that Docker version command again 如果你再次运行那个 Docker version 命令

and look at your server, 然后查看你的服务器，

you'll notice that there's actually an OS entry on here 你会注意到这里实际上有一个 OS 条目

and you'll notice 你会注意到

that it probably doesn't have your operating system listed. 它可能没有列出你的操作系统。

Mine, for example, right here says very specifically Linux 例如我的，在这里非常明确地写着 Linux

as the operating system. 作为操作系统。

So that is kind of specifying 所以这有点在指定

that I'm running a Linux virtual machine 我正在运行一个 Linux 虚拟机

and that's what's being used 这就是正在被使用的东西

to host all these different containers 来托管所有这些不同的容器

that you and I are going to be working with. 你和我将要一起使用的容器。

So just a little bit of interesting trivia. 所以来点有趣的小知识。

Now let's take another quick break right here. 现在我们在这里再稍作短暂休息。

We're gonna continue the next section 我们将在下一节继续。

and start digging into the Docker client a little bit more. 并开始更深入地探索 Docker 客户端。

So quick break and I'll see you in just a minute. 所以短暂休息一下，一分钟后见。


