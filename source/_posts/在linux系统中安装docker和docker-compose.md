---
title: 在ubuntu系统中安装docker和docker-compose
date: 2023-3-29
updated:
tags: docker
categories: vps
keywords:
description:
top_img:
comments: 
cover: https://s1.ax1x.com/2023/03/29/ppcGDsA.png
toc:
toc_number:
toc_style_simple:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
---

# 在linux系统中安装docker和docker-compose

 开个新坑吧, 以后给大家分享一些实用有趣的`docker`项目. 

这个算是前期工作, 先在自己的linux系统上安装好`docker`和`docker-compose`. 两者的安装工作就比较简单了, 其中`docker`有一键安装脚本. `docker-compose` 的安装也不是很复杂.

### step1 使用一键脚本安装docker

#### 海外vps

1. **更新、安装必备软件**

```bash
apt-get update && apt-get install -y wget vim curl
```

2. **一键安装脚本**

```bash
sudo su  #获取root权限
wget -qO- get.docker.com | bash
```

3. **卸载docker**

   ```bash
   sudo apt-get purge docker-ce docker-ce-cli containerd.io
   sudo rm -rf /var/lib/docker
   sudo rm -rf /var/lib/containerd
   ```

#### 国内linux设备

1. **docker一键安装脚本**

```bash
sudo su # 获取root权限
bash <(curl -sSL https://gitee.com/SuperManito/LinuxMirrors/raw/main/DockerInstallation.sh)
```
在安装的过程中会让你选择镜像源的地址,阿里云/网易云/腾讯云都可以的.

2. **卸载docker**

```bash
sudo apt-get remove docker docker-engine docker.io containerd runc
sudo rm -rf /var/lib/docker/
sudo rm -rf /var/lib/containerd
```

在安装完成之后, 使用

```shell
docker --version
```

查看是否已经安装成功. 如果提示版本号即为已经安装成功. 

![image-20230331111143137](https://gcore.jsdelivr.net/gh/jth445600/picgo@master/img/2023/03/31/c91c60626d888ce6b9536dec21eb10aa-20230331111146-3acfe8.png)

### step 2 安装docker-compose

#### 海外vps

1. **docker-compose** 一键安装脚本

   下列支持自动判断`CPU`架构, 并且默认安装最新版本.

   ```bash
   tag=$(wget -qO- -t1 -T2 "https://api.github.com/repos/docker/compose/releases/latest" | grep "tag_name" | head -n 1 | awk -F ":" '{print $2}' | sed 's/\"//g;s/,//g;s/ //g')
    sudo curl -L "https://github.com/docker/compose/releases/download/$tag/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   sudo chmod +x /usr/local/bin/docker-compose
   docker-compose --version
   ```

   如果看到提示版本号, 即为安装成功.

   ![image-20230331110354418](https://gcore.jsdelivr.net/gh/jth445600/picgo@master/img/2023/03/31/53b7ec138a7bc3010c55f76fb8885b92-20230331110402-296f5e.png)



2. 卸载**docker-compose** 

```bash
sudo rm -rf /usr/local/bin/docker-compose
```

#### 国内Linux设备

1. **docker-compose** 一键安装脚本

​	下列支持自动判断`CPU`架构, 并且默认安装最新版本.

```bash
tag=$(wget -qO- -t1 -T2 "https://api.github.com/repos/docker/compose/releases/latest" | grep "tag_name" | head -n 1 | awk -F ":" '{print $2}' | sed 's/\"//g;s/,//g;s/ //g')
 sudo curl -L "https://ghproxy.com/https://github.com/docker/compose/releases/download/$tag/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

如果看到提示版本号, 即为安装成功.

![image-20230331110354418](https://gcore.jsdelivr.net/gh/jth445600/picgo@master/img/2023/03/31/53b7ec138a7bc3010c55f76fb8885b92-20230331110402-296f5e.png)

2. 卸载**docker-compose** 

```bash
sudo rm -rf /usr/local/bin/docker-compose
```

