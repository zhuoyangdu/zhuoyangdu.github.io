---
title: Ubuntu16.04 + Anaconda 中安装 Tensorflow + MuJoCo
date: 2018-01-20 00:03:10
tags:
categories: Deep Learning
---

为了做伯克利深度强化学习的课程作业安装了Tensorflow+MoJoCo+OpenAI gym，记录下安装过程和自己踩过的坑~

**安装Anaconda和tensorflow**

Anaconda的安装过程可直接参照官网，选择安装3.5版本的python，新建conda运行环境。

```
# Python 3.5
$ conda create -n tensorflow python=3.5 
```

选择pip工具安装Tensorflow，首先需要激活conda环境：

```
$ source activate tensorflow
```

根据要安装的不同版本的tensorflow设置环境变量（操作系统，Python版本，CPU版本还是CPU+GPU版本）。本文环境为：Ubuntu/Linux 64-bit, CPU-only, Python3.5。

```
# Ubuntu/Linux 64-bit, CPU only, Python 3.5  
(tensorflow)$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.10.0-cp35-cp35m-linux_x86_64.whl  
```

根据Python版本进行安装：

```
# Python 3  
(tensorflow)$ pip3 install --ignore-installed --upgrade $TF_BINARY_URL  
```

---
**安装MuJoCo**

安装教程可参见：[https://github.com/openai/mujoco-py](https://github.com/openai/mujoco-py)

安装过程主要分两步，需要首先安装MuJoCo，然后安装mujoco-py，由于课程要求使用mujoco1.31，因此这里安装1.31的版本，注意mujoco-py的版本需要和MuJoCo版本对应上，如果安装mujoco1.31，则mujoco-py需要安装0.5.7的版本，否则会安装失败。

Linux版本需要首先安装依赖：

```
(tensorflow)$ sudo apt-get install -y curl git libgl1-mesa-dev libgl1-mesa-glx libglew-dev libosmesa6-dev python3-pip python3-numpy python3-scipy net-tools unzip vim wget xpra
```

安装MuJoCo：

1. 在[MuJoCo Website](https://www.roboti.us/license.html)申请30天试用或学生免费证书，这里需要获取Computer id，下载对应系统(Linux)的脚本运行得到id（脚本需要设置运行权限 ` chmod 777 getid_linux`），邮件中会收到license文件mjkey.txt。

2. 下载对应版本的mjpro，[https://www.roboti.us/index.html](https://www.roboti.us/index.html)，本文选择mjpro131 linux。

3. 解压`mjpro131.zip`到`~/.mujoco/mjpro131`，并将license文件放在`~/.mujoco/`和`~/.mujoco/mjpro131/bin`目录下。

4. 设置环境变量：

```
export LD_LIBRARY_PATH=/home/user/.mujoco/mjpro131/bin
```

 *测试是否安装成功：*
 
 在`~/.mujoco/mjpro131/bin`下运行`./simulate ../model/humanoid.xml`，弹出仿真界面即为安装成功。
 
 
安装mujoco-py:
 
 ```
 (tensorflow)$ pip3 install mujoco-py==0.5.7
 ```

---

**安装OpenAI gym**

```
 (tensorflow)$ git clone https://github.com/openai/gym.git
 (tensorflow)$ cd gym
 (tensorflow)$ pip install -e .
```

---

测试：通过运行`./homework/hw1/demo.bash`测试是否安装成功。









