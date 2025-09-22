-: In the last section, -: 在上一节中，

we downloaded and installed Docker for Windows 我们已在个人电脑上下载并安装了 Docker for Windows

or Docker for Mac on your personal computer. 或 Docker for Mac。

You should now be able to ran the command Docker version 现在你应该能够运行命令 Docker version

at the command line 在命令行中

and see a little bit of text like this appear. 并看到像这样的少量文本出现。

I now want to write out 我现在想写出

our very first kind of meaningful command 我们的第一个真正有意义的命令

with the Docker client or the Docker CLI. 通过 Docker 客户端或 Docker CLI。

We're going to run a very quick command here, 我们将运行一个非常快速的命令，

and then we're gonna go 然后我们将要进行

through a very specific flow of actions that occurred 一系列非常具体的操作流程，这些操作是在那个命令被执行时发生的

when that command got executed. 。

So, here's the command. 所以，命令就是这个。

We're gonna write docker run hello-world. 我们要写 docker run hello-world。

Yes, it is kind of a hello world thing of sorts. 是的，这有点类似某种 hello world 示例。

Don't worry, it's gonna be rather interesting. 别担心，这会相当有趣。

I'll then press enter, 然后我会按回车键，

and we're gonna very quickly see 我们很快就会看到

a lot of text start to scroll along the screen. 大量文本开始在屏幕上滚动。

Now, I'm gonna scroll up a little bit 现在，我要向上滚动一点

and you'll see 你就会看到

a little hello from Docker message right here. 来自 Docker 的一条小小问候消息就在这里。

And then you'll notice underneath that 然后你会注意到下面

it list out these series of steps that just occurred 它列出了刚刚发生的这一系列步骤

when you ran that command. 当你运行那个命令时。

Now, we're going to go over the series of steps right here 现在，我们要在这里逐步详细讲解这一系列步骤

in great detail. 非常详细。

So, if you want to, 所以，如果你想的话，

you can kind of ignore that text for right now. 你现在可以暂时忽略那些文字。

I'm gonna scroll up a little bit further 我要把页面向上再滚一点

and I want you to see up here it says, 并且我希望你看到上面写着，

"Unable to find image hello world locally." “Unable to find image hello world locally.”

All right, so with that mind, 好了，带着这个想法，

let's go take a look at a couple of diagrams 我们来看看几张图表

that are gonna help explain what just occurred 这些图表将有助于解释刚才发生的情况

when we run that command. 当我们运行那个命令时。

All right, here we go. 好了，我们开始。

So, at the Terminal, 所以，在终端上，

you and I executed the command, docker run hello-world. 你和我一起执行了命令：docker run hello-world。

That starts up that Docker client or the Docker CLI. 这会启动那个 Docker 客户端或 Docker CLI。

Again, the Docker CLI 再次说明，Docker CLI

is in charge of taking commands from you, 负责接收来自你的命令，

kind of doing a little bit of processing on them, 在对它们做一点处理，

and then communicating the commands 然后传达这些命令

over to something called the Docker server. 转到称为 Docker server 的某个东西。

And it's that docker server that is really in charge 而真正负责的是那个 docker 服务器

of the heavy lifting. 来完成繁重的工作。

When we ran the command, docker run hello-world, 当我们运行命令 docker run hello-world 时,

that meant that we wanted to start up a new container 那意味着我们想要启动一个新的容器

using the image with the name of hello world. 使用名为 hello world 的镜像。

The hello world image hello world 镜像

has a tiny little program inside of it 里面有一个很小的程序

whose sole purpose, sole job, 它的唯一目的，唯一的任务，

issue print-out the message that you see right here. 打印出你在这里看到的那条消息。

That's the only purpose of that image. 那张镜像就只有那个用途。

Now, when we ran that command 现在，当我们运行那个命令时

and it was issued over to the Docker server, 并且它被发送到 Docker 服务器，

a series of actions very quickly occurred in the background. 一系列操作在后台非常快速地发生。

The Docker server Docker 服务器

saw that we were trying to start up a new container 检测到我们正在尝试启动一个新容器

using an image called hello world. 使用名为 hello world 的镜像。

The first thing that the Docker server did Docker 服务器做的第一件事

was check to see if it already had a local copy. 是检查它是否已经有本地副本。

Like a copy on your personal machine 就像你本机上的一个副本

of the hello world image or that hello world file. 例如 hello world 镜像或那个 hello world 文件。

So, the Docker server 因此，Docker 服务器

looked into something called the ImageCash. 研究了一个叫 ImageCash 的东西。

Now, because you and I just installed Docker 现在，因为你和我刚在个人电脑上安装了 Docker

on our personal computers, 。

the ImageCache is currently empty. ImageCache 目前是空的。

We have no images that have already been downloaded before. 我们没有任何已经下载过的镜像。

So, because the ImageCache was empty, 所以，因为 ImageCache 是空的，

the Docker server decided to reach out Docker 服务器决定发起请求

to a free service called Docker Hub. 到一个名为 Docker Hub 的免费服务。

The Docker Hub is a repository of free public images Docker Hub 是一个免费公共镜像仓库

so you can freely download and run 因此你可以自由下载并运行

on your personal computer. 在你的个人电脑上。

So, Docker server reached out to Docker Hub and said, 于是，Docker 服务器访问了 Docker Hub 并说，

"Hey, I'm looking for an image called hello world. “嘿，我在找一张名为 hello world 的镜像。

Do you have one?" 你有吗？”

Of course, the Docker hub does. 当然，Docker Hub 有。

So, Docker server downloaded this hello world file 所以，Docker 服务器下载了这个 hello world 文件

and stored it on your personal computer in this ImageCache 并将它存储在你个人电脑上的这个 ImageCache 中

where it can now be reran 现在它可以被重新运行

at some point in the future very quickly 在未来的某个时点，很快地

without having to re-download it from the Docker Hub. 无需从 Docker Hub 重新下载它。

So, essentially, we downloaded it over here like some. 所以，基本上，我们在这里像某种方式下载了它。

After that, the Docker server then said, 之后，Docker 服务器接着说，

"Okay, great. I've got this image “好了，太棒了。我拿到这个镜像了

and now, it's time to use it 现在，是时候使用它了”

to create an instance of a container." 创建容器实例。"

And I remember 我还记得

what we just said about a container a moment ago. 我们刚才关于容器所说的话。

An instant container is an instance of an image. 一个即时容器是镜像的一个实例。

Its sole purpose is to run one very specific program. 它的唯一目的是运行一个非常特定的程序。

So, the Docker server 因此，Docker 服务器

then essentially took that single file, 然后基本上把那个单一文件，

loaded it up into memory, 加载到内存中，

created a container out of it, 从中创建了一个容器，

and then ran a single program inside of it. 然后在其中运行了一个单一的程序。

And that single program's purpose 而那个单一程序的目的

was to print out the message that you see right here. 就是打印出你现在看到的这条信息。

So, that's pretty much it. 就这些了。

That's what happens when you run this Docker run command. 这就是运行这个 Docker run 命令时发生的情况。

It reaches out to Docker Hub, 它会访问 Docker Hub，

it grabs the image, 它拉取镜像，

and then it creates a container out of that image. 然后基于该镜像创建一个容器。

Now, one thing that you'll notice that's kind of interesting 现在，你会注意到一件有趣的事情

if we run the docker run hello-world command a second time, 如果我们第二次运行 docker run hello-world 命令，

you'll notice that we are not going to see the message 你会注意到我们不会看到正在下载的消息，

of downloading or container image not found locally 也不会看到本地未找到容器镜像的提示

that we saw the first time. 这是我们第一次看到的。

So, scroll back up to the very top. 所以，向上滚动回到最顶部。

Here's the first time that we ran the command. 这是我们第一次运行该命令的地方。

You'll notice it up here it said, 你会注意到在上面它写着，

"Unable to find image locally." “Unable to find image locally.”

But now the second time, 但现在是第二次，

we did not see that message 我们没有看到那条信息

and that is because we already downloaded it 那是因为我们已经把它下载到了

to our ImageCache on our personal computer. 我们个人电脑上的 ImageCache。

So, the big lesson here 所以，这里的重要教训是

is that the first time that you try 第一次尝试

to make use of any of these public images over here, 使用这些公共镜像中的任何一个时，

you're gonna have to do a little bit of a download. 你需要先下载一小部分东西。

But then in the future after that, 但之后在未来，

you can start up a container 你就可以启动一个容器了

using that image much more quickly 使用该镜像要快得多

because the image has already been downloaded 因为该镜像已经被下载

to your computer. 到你的计算机上。

All right, now in this entire flow, 好，现在在整个流程中，

one thing that we've been kind of light on at this point 有一件事到目前为止我们讲得有点少

is talking about exactly what a container is. 就是到底什么是容器。

So, let's take a quick pause right here. 那么，我们在这里稍作停顿。

We're gonna come back the next section 我们将在下一节回来

and go into a little bit greater detail 并深入讲解更多细节

on exactly what a container is. 关于容器到底是什么的确切解释。

So, quick break and I'll see you in just a minute. 现在短暂休息一下，一分钟后见。
