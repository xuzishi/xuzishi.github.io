---
title: Install ROS Noetic on Ubuntu 20.04
subtitle: 

# Summary for listings and search engines
summary: Install ROS Noetic on Ubuntu 20.04

# Link this post with a project
projects: []

# Date published
date: '2023-02-12T00:00:00Z'

# Date updated
lastmod: '2023-02-12T00:00:00Z'

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: ''
  focal_point: ''
  placement: 2
  preview_only: false

authors:
  - admin

tags:
  - ROS
  - Ubuntu

categories:
  - Notes
---

# Ubuntu 20.04 安装 ROS Noetic

Author: xuzishi  
Update: Nov 23, 2022  

参考原文：https://zhuanlan.zhihu.com/p/515361781

------


## 1. 配置系统源

将原本的系统软件源备份一下，以防后续需要

```linux
sudo cp /etc/apt/sources.list /etc/apt/sources.list.backup
```

<br>

编辑系统软件源

```
sudo gedit /etc/apt/sources.list
```

将全部内容替换为

```
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-proposed main restricted universe multiverse
```

> 替换内容为[清华源](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/)。因国内有墙，如不替换为国内源，后续会有东西安装不上。也可以替换为其他国内源。

<br>

更新软件源的更改

```
sudo apt update
```

<br>


## 2. 添加 ROS 源

设置 sources.list

```
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
```

<br>

添加 ROS 密钥

```
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
```

<br>

确保软件索引是最新的

```
sudo apt update
```

<br>


## 3. 安装ROS

安装 `aptitude` 和 `git` 

```
sudo apt-get install aptitude git
```

<br>

安装桌面完整版 ROS Noetic

```
sudo aptitude install ros-noetic-desktop-full
```

需要一段时间，请等待

> ROS Noetic 只适配 Ubuntu 20.04，Ubuntu 16.04 请安装 ROS Kinetic，Ubuntu 18.04 请安装 ROS Melodic

<br>

安装完成后，设置环境变量

```
echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
```
```
source ~/.bashrc
```

<br>


## 4. 安装 rosdep

> 因国内 `https://raw.githubusercontent.com` 被屏蔽，因此需要手动下载 `rosdistro` 文件并修改配置

### * rosdepc 方案

[鱼香ROS](https://zhuanlan.zhihu.com/p/398754989) 给出了一个一键解决方案：`rosdepc`：

``` 
sudo pip install rosdepc 
```

```
sudo rosdepc init
```

```
rosdepc update
```

为防止一键解决方案失效，下面给出原版解决方案。

### * 原版方案
克隆文件放置在指定的本地文件夹下，这里放置在了 `/opt/ros/` 文件夹下 

```
cd /opt/ros/
```

```
sudo git clone https://github.com/ros/rosdistro.git
```

<br>

修改文件1

```
sudo gedit /opt/ros/rosdistro/rosdep/sources.list.d/20-default.list
```

修改全文为

```
# os-specific listings first
yaml file:///opt/ros/rosdistro/rosdep/osx-homebrew.yaml osx

# generic
yaml file:///opt/ros/rosdistro/rosdep/base.yaml
yaml file:///opt/ros/rosdistro/rosdep/python.yaml
yaml file:///opt/ros/rosdistro/rosdep/ruby.yaml
gbpdistro file:///opt/ros/rosdistro/releases/fuerte.yaml fuerte

# newer distributions (Groovy, Hydro, ...) must not be listed anymore, they are being fetched from the rosdistro index.yaml instead
```

<br>

修改文件2

```
sudo gedit /usr/lib/python3/dist-packages/rosdep2/gbpdistro_support.py
```

修改其中一行

```
FUERTE_GBPDISTRO_URL = 'file:///opt/ros/rosdistro/' \
    'releases/fuerte.yaml'
```

<br>

修改文件3

```
sudo gedit /usr/lib/python3/dist-packages/rosdep2/rep3.py
```

修改其中一行

```
REP3_TARGETS_URL = 'file:///opt/ros/rosdistro/releases/targets.yaml'
```

<br>

修改文件4

```
sudo gedit /usr/lib/python3/dist-packages/rosdistro/__init__.py
```

修改其中一行

```
DEFAULT_INDEX_URL = 'file:///opt/ros/rosdistro/index-v4.yaml'
```

<br>

> 注意：原 URL 为 `'https://raw.githubusercontent.com/ros/rosdistro/master/xxx'`，现 URL 为 `file:///opt/ros/rosdistro/xxx`。更改时不仅要把前面的 `https://raw.githubusercontent.com` 改为 `file:///opt/ros`，而且要注意删去后面的 `master/`

<br>

安装 rosdep  

```
sudo apt-get install python3-rosdep python3-rosinstall  python3-rosinstall-generator python3-wstool  build-essential
```

<br>


## 5. 初始化 rosdep

同样手动更改 URL

```
sudo mkdir -p /etc/ros/rosdep/sources.list.d
```

```
sudo gedit /etc/ros/rosdep/sources.list.d/20-default.list
```

<br>

向文件中添加

```
#os-specific listings first
yaml file:///opt/ros/rosdistro/rosdep/osx-homebrew.yaml osx
#generic
yaml file:///opt/ros/rosdistro/rosdep/base.yaml
yaml file:///opt/ros/rosdistro/rosdep/python.yaml
yaml file:///opt/ros/rosdistro/rosdep/ruby.yaml
gbpdistro file:///opt/ros/rosdistro/releases/fuerte.yaml fuerte
#newer distributions (Groovy, Hydro, ...) must not be listed anymore, they are being fetched from the rosdistro index.yaml instead
```

<br>

完成初始化 rosdep

```
rosdep update
```

<br>


## 6. 测试安装是否成功

打开 ROS 内核

```
roscore
```

如无报错，则安装妥当

<br>

打开一个 demo：

新建一个终端，打开小海龟节点

```
rosrun turtlesim turtlesim_node
```

会弹出一个小海龟图形化界面

<br>

再新建一个终端，打开键盘控制节点

```
rosrun turtlesim turtle_teleop_key
```

在该终端中用方向键控制上一步图形化界面中小海龟的位置

<br>

再新建一个终端，打开节点示意图

```
rosrun rqt_graph rqt_graph
```

会弹出当前的节点示意图

<br>

------


## 7. 一些可选配置

### 创建工作区并设为默认

```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make

echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
```


### 将 python 默认为 python3

```
sudo mv /usr/bin/python /usr/bin/python.bak
sudo ln -s /usr/bin/python3 /usr/bin/python
```


### 
