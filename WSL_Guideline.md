# Guideline for `WSL`

本文档包含基础的`WSL`命令并涉及了一部分`WSL`配置

如果在运行`WSL`时有其他的问题，可以参阅`Ubuntu_CheatSheet`来尝试解决

*This Document Contains Basic `WSL` Commands and Involves Some `WSL` Configurations*

*If you encounter problems when using `WSL`, you can try to read `Ubuntu_CheatSheet` to find the method.*



## Contents

[前言/*Readme*](#Readme)

[1.常用指令/*Common Commands*](#1)

- [基础指令/*Basic Commands*](#Basic)
- [设置版本相关命令/*Version Setting*](#Version)
- [图形化/*GUI*](#gui)

[2.WSL相关配置/*WSL Configuration*](#wsl相关配置wsl-configuration)
- [`WSL`常用指令/*`WSL` Common Commands*](#wsl常用指令wsl-common-commands)
- [WSL相关配置/*WSL Configuration*](#wsl相关配置wsl-configuration)
  - [迁移WSL/*Move WSL* (For Windows)](#迁移wslmove-wsl-for-windows)
  - [WSL设置最大内存/*Set maximium Memory for WSL*](#wsl设置最大内存set-maximium-memory-for-wsl)


## 前言/*ReadMe*

<span id="Readme"></span>

- 本文档介绍的内容更多是关于`WSL 2`的，因为`Docker`可以使用`WSL 2`作为后端，这些命令更多的是在我配置`Docker`的`WSL 2`后端时用到的常用指令。

- This document contains more about `WSL 2 commands` for the reason that `Docker` can use `WSL 2` as backend. Most of the commands are used when I build the environment for `Docker`.




### `WSL`常用指令/*`WSL` Common Commands*

<span id="1"></span>

[官方文档/*Official Reference*](https://docs.microsoft.com/zh-cn/windows/wsl/reference)

```powershell
# Powershell自带的WSL帮助文档/The help documents in powershell
wsl --help
```



- <span id="Basic">基础指令/*Basic Commands*</span>

  ```bash
  # List WSL Distro Information/列出发行版信息
  wsl --list --quiet：列出发行版名称
  wsl --list --verbose：显示发行版的详细信息
  ```

  Eg:

  ![image-20201106152217419](https://cdn.jsdelivr.net/gh/AlstarWU/Picture@Markdown/Markdown/WSL_l.png)



  ```bash
  # Set Default Distro/设置默认的发行版
  wslconfig /setdefault Name
  ```

  Eg:

  ![](https://cdn.jsdelivr.net/gh/AlstarWU/Picture@Markdown/Markdown/WSL-SetDefault.png)



  ```bash

  ```


- <span id="Version">设置版本相关命令/*Version Setting*</span>

  ```bash
  # Set default Distro Version/设置新的发行版的默认版本
  wsl --set-default-version 2#Set default Distro Version as WSL 2/设置新的发行版的默认版本为WSL2
  wsl --set-default-version 1#Set default Distro Version as WSL 1/设置新的发行版的默认版本为WSL1

  # Set version of a Distro/设置某一发行版的版本

  ```




- <span id="gui">图形化/*GUI*</span>
-----
  安装`VcXsrv`/*Install `VcXsrv`*
  - 安装`VcXsrv`/*Install `VcXsrv`*

  - 在`WSL`设置`X-Server`显示/*Set `X-Server`Display  in `WSL`*

    ```bash
    #WSL 1
    export DISPLAY=localhost:0
    #WSL 2
    export DISPLAY=`cat /etc/resolv.conf | grep nameserver | awk '{print $2}'`:0
    ```

----

  显示图片/*Show image*

  参考/*Reference*:  [CSDN](https://blog.csdn.net/weixin_30834783/article/details/102144314)

  - 安装`imagemagpick`来显示图片/*Install `imagemagpick` to display image*

    ```bash
    sudo apt install imagemagick-6.q16
    ```

  - 通过命令显示图片/*Show image by command*

    ```bash
    display directory/name.jpg
    #directory/name.jpg:image directory/图片路径
    ```




-----

  利用`xfce4`来为`WSL`建立可视化界面/*Use `xfce4` to build `WSL` GUI*

  参考/*Reference*: [简书](https://www.jianshu.com/p/9fdea59ae8a2)

- 更新软件源/*Update the Sources*

  ```bash
  sudo apt update
  sudo apt-get update
  ```

- 安装`xfce4`/*Install `xfce4`

  ```bash
  sudo apt install xfce4
  sudo apt install xfce4-session
  ```

- 开启`X-Server`并映射/*Open `X-server` and export*

  - 开启`X-launch`/*Open `X-launch`*

    - 1

      ![image-20201107184933012](https://cdn.jsdelivr.net/gh/AlstarWU/Picture@Markdown/Markdown/image-20201107184933012.png)

    - 2

      ![image-20201107185213493](https://cdn.jsdelivr.net/gh/AlstarWU/Picture@Markdown/Markdown/image-20201107185213493.png)

    - 3

      ![image-20201107185257796](https://cdn.jsdelivr.net/gh/AlstarWU/Picture@Markdown/Markdown/image-20201107185257796.png)

  - 在`WSL`中映射/*Export in `WSL`*

  ```bash
  #WSL 1
  export DISPLAY=localhost:0
  #WSL 2
  export DISPLAY=`cat /etc/resolv.conf | grep nameserver | awk '{print $2}'`:0
  ```

  - 打开`xfce4`/*Open `xfce4`*

  ```bash
  # 下面两个命令使用其一即可开启xfce4/Use any one of commands below can open xfce4*GUI*
  xfce4-session
  startxfce4
  # 在终端中使用CTRL+C退出/Use CTRL+C to quit in terminal# 在终端中使用CTRL+C退出/Use CTRL+C to quit in terminal
  ```

  ![image-20201107190008803](https://cdn.jsdelivr.net/gh/AlstarWU/Picture@Markdown/Markdown/image-20201107190008803.png)


## WSL相关配置/*WSL Configuration*
#### 迁移WSL/*Move WSL* (For Windows)
需要的工具/*Tools Needed*: [pxlrbt/Move-WSL](https://github.com/pxlrbt/move-wsl) on *Github*<br><br>

- 下载并解压缩压缩包/*Download and Unzip the Compressed Package*
  - 下载压缩包/*Download Zip*
  ![](https://cdn.jsdelivr.net/gh/AlstarWU/Picture@Markdown/Markdown/20201108162744.png)
  - 解压压缩包/*Unzip the Compressed Package*
- 进入解压缩目录/*Enter in the folder you unzip it*<br>
![](https://cdn.jsdelivr.net/gh/AlstarWU/Picture@Markdown/Markdown/20201108162947.png)
- 使用Move-WSL/*Use `Move-WSl`* 
  - `Shift+右键`，选择`在Powershell中打开`/*`Shift+Right Click` and Click `Open in Powershell`
  - 使用下面命令/*Use Following Commands*
    ```powershell
    ./move-wsl.ps1
    ```
  - 按程序介绍来依次执行并迁移WSL/*Follow the introduction of the program and move WSL*
    - 1<br>
    ![](https://cdn.jsdelivr.net/gh/AlstarWU/Picture@Markdown/Markdown/20201108165147.png)
    - 2<br>
    ![](https://cdn.jsdelivr.net/gh/AlstarWU/Picture@Markdown/Markdown/20201108165300.png)
    - 3<br>
    ![](https://cdn.jsdelivr.net/gh/AlstarWU/Picture@Markdown/Markdown/20201108165517.png)
- 操作完成后关闭即可/*Just close the shell after operation*

#### WSL设置最大内存/*Set maximium Memory for WSL*

 参考/*Reference*:  [Microsoft](https://docs.microsoft.com/zh-cn/windows/wsl/wsl-config#configure-global-options-with-wslconfig)
- 打开用户文件夹/*Open User's Folder*
  `Win + R`打开运行，输入`%UserProfile%`，回车进入文件夹/*`Win + R`, input `%UserProfile%`, and then Press `enter` to Enter in the Folder*
  ![](https://cdn.jsdelivr.net/gh/AlstarWU/Picture@Markdown/Markdown/20201108170551.png)
- 创建`.wslconfig`文档，并编辑/*Create a `.wslconfig` file then edit it
  - 推荐使用`Visual Studio Code`编辑/*Recommand to Edit it by `Visual Studio Code`*
  - 我的设置/*My Configuration*
    ```bash
    [wsl2]
    memory=4GB
    processors=4
    swap=512MB
    ```
    编辑完成后保存文件/*Save the file after yoou edited it*
  - 在powershell通过`wsl --shutdown`来关闭全部WSL进程，重启WSL即可生效/*Shut down all the processes by `wsl --shutdown` in powershell and restart WSL to take effect*
