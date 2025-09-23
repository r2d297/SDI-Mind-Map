
```
docker system prune
```


-: In the last section I had mentioned that I'd cleared out -: 在上一节我提到我已经清理了

all the stopped containers on my machine, 我机器上所有已停止的容器，

and so I thought you might be curious on how I did that. 所以我想你可能会好奇我是怎么做到的。

If I run docker ps --all right now, 如果我现在运行 docker ps --all，

I can see that I currently have two stopped containers. 我可以看到我当前有两个已停止的容器。

So these containers right now are essentially 所以这些容器现在本质上是

just taking up disk space on my computer, 只是占用了我电脑的磁盘空间，

and so it might be to my advantage 所以对我来说可能有利

to try to entirely delete them 尝试将它们完全删除

and not just leave them in this stopped state. 而不是把它们都保留在这个已停止的状态。

To delete all these containers, 要删除所有这些容器，

I can run docker system prune. 我可以运行 docker system prune。

I'll then be presented with a warning here. 然后这里会显示一个警告。

So just to be clear, 所以要明确一点，

this is not only going to delete stopped containers, 这不仅仅会删除已停止的容器，

it's also going to delete a couple of other items as well, 它还会删除其他几个项目，

most notably your build cache. 最显著的是你的构建缓存。

The build cache is any image 构建缓存是任何镜像

that you have fetched from Docker Hub. 这些是你从 Docker Hub 拉取下来的。

So after running docker prune 所以在运行 docker prune 之后

you will have to re-download images from Docker Hub, 你将不得不重新从 Docker Hub 下载镜像，

which is not a really big deal. 这并不是什么大问题。

Just be aware that you're gonna have to wait 只要注意，你得等一会儿

a couple of minutes the next time you start up a container. 下次启动容器时会花几分钟时间。

Not really a couple minutes, but a couple of seconds really. 不是真的几分钟，实际上是几秒钟。

So we can enter in "yes", hit Enter, 所以我们可以输入 "yes"，按回车，

and then it will tell us about the deleted containers 然后它会告诉我们被删除的容器情况

and it'll tell me also how much space 并且它还会告诉我通过删除这些资源回收了多少空间

has been reclaimed by deleting those resources. 已经通过删除这些资源回收了多少空间。

If I then do another docker ps --all, 如果我接着再运行 docker ps --all，

I'll see that I do not have 我会确认自己没有

any stopped containers whatsoever. 任何已停止的容器。

I really recommend you keep 我强烈建议你保留

the docker system prune command in mind, 记住 docker system prune 命令，

because anytime that you're kind of done working with docker 因为每当你差不多完成使用 Docker 时

for a period of weeks or months, 数周或数月期间，

or if you decide you just don't wanna work 或者如果你决定你就是不想再工作

with docker again at all, 再也不想使用 docker，

you will want to run this command to delete any containers 你会想运行此命令来删除任何容器

that are still just kind of sitting around 仍然就那样闲置着

eating up disk space. 占用磁盘空间。

All right, let's take another quick break, 好吧，我们再稍作休息，

and we'll continue in the next section. 我们将在下一节继续。