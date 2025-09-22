Installation of Docker Desktop on Native Hardware
在本地物理硬件上安装 Docker Desktop
Native Hardware means a physical laptop or desktop computer. If you are using WSL on Windows, then you should be installing Docker Desktop for Windows NOT Linux. If you are installing within a VM like VirtualBox or Parallels, or, a cloud server such as AWS, then, you must use the Installation on Cloud Servers or inside Virtual Machines instructions instead. Docker Desktop does not work with nested virtualization.
本地硬件是指物理笔记本或台式电脑。如果你在 Windows 上使用 WSL，则应安装 Docker Desktop for Windows 而不是 Linux。如果你要在像 VirtualBox、Parallels 这样的虚拟机中，或在 AWS 等云服务器上安装，则必须改为使用“在云服务器或虚拟机内安装”的说明。Docker Desktop 不支持嵌套虚拟化。

Currently Docker Desktop currently only works with the Ubuntu, Debian, or Fedora distributions. If you are using any other distribution, you will need to follow the "Installation on Cloud Servers or inside Virtual Machines" instructions.
目前 Docker Desktop 仅支持 Ubuntu、Debian 或 Fedora 发行版。如果你使用其他发行版，需要遵循“在云服务器或虚拟机内安装”的说明。

Create Dockerhub account
创建 Dockerhub 帐户
https://hub.docker.com/signup

Install Docker Desktop for Linux
为 Linux 安装 Docker Desktop
Simply follow the generic installation instructions for your particular distribution:
只需按照适用于您具体发行版的通用安装说明操作：

https://docs.docker.com/desktop/install/linux-install/#generic-installation-steps

Login to the Dockerhub
登录 Dockerhub
In order to push and pull images, you will need to log in to the Dockerhub. In your terminal, run docker login and then enter your Dockerhub account username and password.
为了推送和拉取镜像，您需要登录 Dockerhub。在终端中运行 docker login ，然后输入您的 Dockerhub 账户用户名和密码。

Test Docker installation
测试 Docker 安装
After completing the installation steps, test out Docker by running docker run hello-world. This should download and run the test container printing "hello world" to your console.
完成安装步骤后，通过运行 docker run hello-world 来测试 Docker。此命令应当下载并运行测试容器，并在控制台打印 "hello world"。

Installation on Cloud Servers or inside Virtual Machines
在云服务器或虚拟机内的安装
The steps listed below are for Ubuntu Desktop LTS. You can find the full official docs and steps for other Linux distributions here:
下面列出的步骤适用于 Ubuntu Desktop LTS。您可以在此处找到完整的官方文档以及其他 Linux 发行版的安装步骤：

Ubuntu: https://docs.docker.com/install/linux/docker-ce/ubuntu/

CentOS: https://docs.docker.com/install/linux/docker-ce/centos/
(Note: Students have encountered issues when using CentOS or RHEL as the host related to Docker container communication. You may need to research some workaround for the errors you run into or search the QA for already posted solutions)
（注：学生在将 CentOS 或 RHEL 用作主机时遇到过与 Docker 容器通信相关的问题。您可能需要针对遇到的错误寻找一些变通方法，或在问答区搜索已发布的解决方案）

Debian: https://docs.docker.com/install/linux/docker-ce/debian/

Create Dockerhub account
创建 Dockerhub 帐户
https://hub.docker.com/signup

Install Docker  安装 Docker
The Docker docs suggest setting up a Docker repository to install and update from.
Docker 文档建议设置一个 Docker 仓库以便从中安装和更新。
This is where you should start: https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository
你应该从这里开始：https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository

Login to the Dockerhub
登录 Dockerhub
In order to push and pull images, you will need to log in to the Dockerhub. In your terminal, run docker login and then enter your Dockerhub account username and password.
为了推送和拉取镜像，您需要登录 Dockerhub。在终端中运行 docker login ，然后输入您的 Dockerhub 账户用户名和密码。

Test Docker installation
测试 Docker 安装
After completing the installation steps, test out Docker by running sudo docker run hello-world. This should download and run the test container printing "hello world" to your console.
完成安装步骤后，通过运行 sudo docker run hello-world 来测试 Docker。此命令应当下载并运行测试容器，并在控制台打印 "hello world"。

Testing Docker Compose  测试 Docker Compose
Important! The version of Docker Compose that is now installed with Docker does not include a symlink to the docker-compose (with a hyphen) command. This only exists in Docker Desktop. So, all commands should be run without a hyphen.
重要！现在随 Docker 一起安装的 Docker Compose 版本不包含指向带连字符的 docker-compose 命令的符号链接。只有 Docker Desktop 中存在该链接。因此，所有命令都应不带连字符运行。
After completing, test your installation by running:
完成后，通过运行以下命令测试您的安装：
 docker compose -v
This should print the version and build numbers to your console.
这会将版本和构建编号打印到你的控制台。

Run without Sudo  无需使用 Sudo
Follow these instructions to run Docker commands without sudo:
按照以下说明在不使用 sudo 的情况下运行 Docker 命令：
https://docs.docker.com/install/linux/linux-postinstall/#manage-docker-as-a-non-root-user

Start on Boot  开机启动
Follow these instructions so that Docker and its services start automatically on boot:
按照以下说明使 Docker 及其服务在开机时自动启动：
https://docs.docker.com/install/linux/linux-postinstall/#configure-docker-to-start-on-boot

You may need to restart your system before starting the course material.
在开始课程内容之前，您可能需要重启系统。