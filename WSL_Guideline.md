# CheatSheet_Docker—Windows

## `Docker`推荐参考/*Recommanded Reference for `Docker`*:  [菜鸟教程](https://www.runoob.com/docker/docker-tutorial.html)

## 目录/*Contents*
[0.Docker安装/*Install Docker*](#docker安装install-docker)
[1.Docker_Ubuntu](#docker_ubuntu)
- [CheatSheet_Docker—Windows](#cheatsheet_dockerwindows)
  - [`Docker`推荐参考/*Recommanded Reference for `Docker`*:  菜鸟教程](#docker推荐参考recommanded-reference-for-docker-菜鸟教程)
  - [目录/*Contents*](#目录contents)
    - [Docker安装/*Install Docker*](#docker安装install-docker)
    - [Docker_Ubuntu](#docker_ubuntu)
      - [Docker_Ubuntu安装/*Install Docker_Ubuntu*](#docker_ubuntu安装install-docker_ubuntu)
      - [WSL设置默认登陆账户/*Set default user for WSL*](#wsl设置默认登陆账户set-default-user-for-wsl)




### Docker安装/*Install Docker*
[Docker官网/*Docker Official Site*](https://www.docker.com/get-started)
[*Docker Hub*](https://hub.docker.com/signup)
- 在`Docker Hub`注册账号/*Sign up in `Docker Hub`*
- 在`Docker`官网下载安装包/*Download installation packages in `Docker Official Site`*
- 安装并使用`Docker`/*Install and Use `Docker`*

Windows注意事项/*Reminder for Windows*:
- 需要`Hyper-V`(`WSL2`可选)/`Hyper-V` is nedded(`WSL2` is alternative)
- 启动`Docker`时乱码错误可在`PowerShell(Admin)`运行以下代码尝试解决<br>*You may try to run code below to solve a garbled error in `PowerShell(Admin)`*
  - 错误示例/*Error Example*
  ![](https://cdn.jsdelivr.net/gh/AlstarWU/Picture@Markdown/Markdown/20201108010137.png)
  - 解决代码/*Code to Run*
    ```powershell
    netsh winsock reset
    ```
- 在安装了`WSL升级包`后，可使用`WSl`作为后端，让`Docker`运行更加流畅<br>*After install `WSL update msi`, you can use `WSL` as `Docker Backend`, and it will run smoother* 
WSL升级包/*WSL Update MSI*: [Click Here](https://docs.microsoft.com/en-us/windows/wsl/wsl2-kernel)


### Docker_Ubuntu
#### Docker_Ubuntu安装/*Install Docker_Ubuntu*
- `XLaunch`本地显示

  ````Bash
   export DISPLAY=host.docker.internal:0
  ````


- Docker 挂载本地目录

  ```bash
  docker run -it -v /test:/soft ubuntu /bin/bash
  ```

  命令中，`/test:/soft`里/test为Linux系统本地目录（在Windows中即为WSL里Ubuntu的目录），/test为在docker容器中对应的目录，若没有则会在docker容器中自动生成。<br>
  *In this command, `/test` in `/test:/soft` is a local folder of Ubuntu system, `/soft` is a synced folder in docker `ubuntu container`, and it will be created automatically if it isn't exist.*
  <br>

- `Docker-ubuntu`更换软件源/*`Docker-Ubuntu` Change Software Source* 
    Reference/参考: [*CSDN*](https://blog.csdn.net/Primavera37/article/details/106171470/)
    `Docker-ubuntu` don't have vi, so use `echo` command to redirect/由于`Docker-ubuntu`不含vi,所以用`echo`指令来重定向
  <br>
    ```bash
    # 备份sources.list/Backup
    mv /etc/apt/sources.list /etc/apt/sources.list.back #备份原始文件以防万一/Back up the original file
  
    # 一行一行运行以下命令/Run Commands One Line by One Line
    echo "deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse" >>/etc/apt/sources.list
    echo "deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse" >>/etc/apt/sources.list
    ectricted universe multiverse" >>/etc/apt/sources.list
    echho "deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse" >>/etc/apt/sources.list
    echo "deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main reso "deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse" >>/etc/apt/sources.list
    echo "deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse" >>/etc/apt/sources.list
    echo "deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse" >>/etc/apt/sources.list
    echo "deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse" >>/etc/apt/sources.list
    echo "deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse" >>/etc/apt/sources.list
    echo "deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse" >>/etc/apt/sources.list
    ```
    运行完成后安装`vim`/*After run these commands we install `vim`*
    ```bash
    apt update
    apt install vim
    ```
    简便方法：在`Ubuntu`镜像上挂载本机的目录，将`/etc/apt/sources.list`拷贝至挂载的目录，在`Windows`中访问并编辑。/*Easier Way:Load your `Windows Folder` on `Ubuntu` image and copy `/etc/apt/sources.list` to your loaded folder, and then use `Windows` to access and edit it.
    <br>
    示例代码/Example
    - 在`WSL上`/In `WSL`
    ```bash
    # 在WSL中，/mnt/可以访问windows的目录，例如/mnt/d/test即代表D:/test
    # In WSL, /mnt/ represents Windows computer folder, for example, /mnt/d/test represents D:/test

    #将D盘中的desktop文件夹挂载到Ubuntu镜像中的 /share 文件夹
    # Sync "/share" in ubuntu image with "D:/desktop" in windows
    docker run -it -v /mnt/d/desktop:/share ubuntu /bin/bash

    # 备份soures.list
    # Backup sources.list
    cp /etc/apt/sources.list /etc/apt/sources.list.bak

    # 拷贝sources.list到挂载的目录
    # Copy "sources.list" to the synced folder
    cp /etc/apt/sources.list /share/sources.list
    ```
    <br>

    - 在`Windows`中/In `Windows`
    使用文本编辑器编辑`sources.list`/*Edit `sources.list` in `Windows`*
    <br>
    - 切换至`Ubuntu`镜像/Switch to `Ubuntu` image
      ```bash
      docker ps -a #显示所有容器/Show all Containers
      ```
      ![](https://cdn.jsdelivr.net/gh/AlstarWU/Picture@Markdown/Markdown/20201108201200.png)
    
      切换至容器/*Switch to Previous Container*
      ```bash
      docker attach <id> # id=Container id
      ```
#### WSL设置默认登陆账户/*Set default user for WSL*
WSL有时会默认使用root账户登陆，众所周知，这样是不安全的，因此可以使用以下代码来设置指定用户为默认登陆用户
*Sometimes WSL may use `root` as the default user, it's not safe as we all know,so we can use code below to set default user*
```powershell
<distro> config --default-user <user>
```
> 在`Powershell`使用下面命令列出分发版(distro)/*Use command below in `Powershell` to show distro
```powershell
wsl -l # <wsl --list> also works
```
![](https://cdn.jsdelivr.net/gh/AlstarWU/Picture@Markdown/Markdown/20201109184800.png)

    
