

```
docker start -a 4b263884282
```

-: In the last section -: 在上一部分

we started investigating the life cycle of a container 我们开始研究容器的生命周期

by using the docker create and docker start commands. 通过使用 docker create 和 docker start 命令。

We're now gonna start to investigate the status 我们现在要开始调查状态

of some of those containers that we've already 这些我们已经创建的一些容器的日志/输出（或状态）

started up on our machine, 已在我们的机器上启动，

but have closed down for some particular reason. 但因某些特定原因已关闭。

So we can print those all out with dockerps--all. 所以我们可以用 docker ps --all 把它们全部打印出来。

You'll notice that I have just one container 你会注意到我现在只有一个容器

listed as exited now, 显示为 exited。

whereas before I had like 30. 而之前我大约有 30 个。

The reason for that is that I ran a command 原因是我在上一个视频和这个视频之间运行了一个命令

between the last video and this one 。

to kind of par down that list. 把那份列表缩减一下。

And of course I will show you that command 当然我会向你展示那个命令

in just a second as well. 很快就好。

So at this point, the only stopped or exited container 所以此时，我机器上唯一已停止或已退出的容器

that I have on my machine, is this one right here. 就是这个了。

Let's try creating and running and then stopping 我们来试着创建并运行，然后再停止它

one more container just to make sure 再运行一个容器以确保万无一失

that we're kind of on level footing. 以便我们处于同一水平线上。

So I'm going to execute docker run BusyBox echo hi there. 所以我要执行 docker run BusyBox echo hi there。

If I then do dockerps--all again, 如果我再运行 docker ps --all，

and then zoom out so I can see this a little bit better, 然后缩小一点以便我可以更好地看到这一点，

there we go, 好了，

I'll see the ID of that container. 我会查看那个容器的 ID。

I'll see the echo hi there, and I can definitely verify 我会看到 echo hi there，并且我可以明确验证

that its status is definitely exited right now. 它的状态现在确实是 exited。

When a container is exited, we can still start it back up. 当一个容器退出后，我们仍然可以把它重新启动。

So just because a container's stopped, 所以仅仅因为一个容器已停止，

doesn't mean that it's like dead or cannot be used again. 并不意味着它就像死掉了一样或不能再次使用。

We can very easily stop and then start containers again 我们可以非常容易地停止容器，然后在将来某个时候再次启动它们

at some point in the future. 在将来的某个时间点。

To start a container back up, 要重新启动一个容器，

we can take its ID and then execute docker start 我们可以获取它的 ID，然后执行 docker start

and paste that ID in. 并粘贴该 ID。

Remember that if we use docker start without the -a flag, 请记住，如果我们在没有 -a 标志的情况下使用 docker start，

however, we won't see any output from it. 但是，我们不会看到它的任何输出。

And so it might be a little bit more useful 所以这样可能会更有用一些

to do docker start -a and then the ID. 执行 docker start -a 然后加上 ID。

And when I do that, you'll notice that it 当我那样做时，你会注意到它

printed out hi there again, 又打印出 hi there，

which is kind of interesting. 这挺有趣的。

Let's take a look at a diagram to really understand 让我们看一张图来真正理解

this entire series of commands that we just issued. 我们刚刚发出的这一整系列命令。

All right, here we go. 好了，我们开始。

So we've got our BusyBox image, and at some point in time 所以我们有我们的 BusyBox 镜像，并且在某个时间点

we definitely ran docker create or docker run, 我们确实运行了 docker create 或 docker run，

that took our file system snapshot 那会对我们的文件系统做快照

and essentially got a reference to it inside the container. 并且本质上在容器内部获得了对它的引用。

We then provided that override command of echo hi there. 然后我们提供了那个覆盖命令：echo hi there。

So that was the primary running command 所以那就是主要的运行命令

inside the container. 容器内部。

That command ran, it then completed, 该命令运行后就完成了，

the container exited it naturally, 容器自然退出了，

and we then ran the docker start command a second time. 然后我们第二次运行了 docker start 命令。

What happened was the running process 发生的情况是正在运行的进程

or this primary command, 或者这个主命令，

was issued a second time inside the container. 在容器内部第二次被执行。

When you have a container that's already been created, 当你有一个已经创建的容器，

we cannot replace that default command. 我们无法替换那个默认命令。

As soon as you start it up with the default command, 一旦你用默认命令启动它，

that's it, the default command is then in place. 就是这样，默认命令就被设置好了。

So we cannot do something like say docker start -a the ID, 所以我们不能像运行 docker start -a 容器 ID 那样去做，

and then try to replace the default command. 然后尝试替换默认命令。

I can't do something like echo bye there. 我不能像 echo bye 那样去做。

So in theory, this would be us trying to replace 所以理论上，这将是我们试图替换

the default command. 默认命令。

Again, can't do that. 同样，不能那样做。

And if we try to run it, 如果我们尝试运行它，

it's going to misinterpret the command that we just issued. 它会误解我们刚刚发出的命令。

It's thinking that we're trying to start up 它认为我们正在尝试启动

multiple containers at the same time. 多个容器同时运行。

So, once we have started up a container, and let it exit, 因此，一旦我们启动了一个容器并让它退出，

we can start it back up again, 我们可以再次将其启动，

which is going to reissue the default command 这将重新发出默认命令

that was used when the container was first created. 该命令是在容器首次创建时使用的。

All right, now it might seem like 好吧，现在这看起来可能像是

going over all this life cycle stuff is kind of unimportant. 讨论所有这些生命周期的内容并不太重要。

It might seem like I'm going 这可能看起来像我在

really far into the weeds with it, 深入到细枝末节。

but trust me, having a solid understanding 但相信我，牢固理解

of the life cycle of a container 容器的生命周期

is gonna be so incredibly useful later on, 以后会非常有用，

when it really comes down to figuring out 当真正需要弄清楚时

how to troubleshoot these things 如何排查这些问题

and debug a running container. 并调试正在运行的容器。

So I think we got a better idea 所以我想我们对容器的生命周期有了更清晰的认识

on the the life cycle of a container. 关于容器的生命周期。

So let's take another quick break, 那么我们再短暂休息一下，

and continue in the next section. 并在下一部分继续。