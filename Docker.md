# 1、安装Docker

## 1.1 Ubuntu安装

```shell
# Run the following command to uninstall all conflicting packages:
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done

# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

# To install the latest version, run:
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Verify that the Docker Engine installation is successful by running the hello-world image.
sudo docker run hello-world
```

## 1.2 centOS安装

```shell
# Uninstall old versions
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
                  
# Set up the repository
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

# Install Docker Engine
# latest
sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Start Docker.
sudo systemctl start docker

# 测试安装是否完成
sudo docker -v
sudo docker images

# Verify that the Docker Engine installation is successful by running the hello-world image.
sudo docker run hello-world
```

## 1.3 启动和校验

```shell
# 启动docker
sudo systemctl start docker.service

# 停止docker
sudo systemctl stop docker.service

# 重启
sudo systemctl restart docerk.service

# 开机自动启动docker
sudo systemctl enable docker.service 

# 执行docker ps命令，如果不报错，说明安装启动成功
docker ps
```

## 1.4 配置docker镜像加速

以阿里云镜像加速为例

### 1.4.1 注册阿里云账号

https://cn.aliyun.com/

### 1.4.2 开通镜像服务

在首页的产品中，找到阿里云的**容器镜像服务**：

![image-20240103135022415](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240103135022415.png)

点击后进入控制台：

![image-20240103135056013](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240103135056013.png)

首次可能需要选择立刻开通，然后进入控制台。

### 1.4.3 配置镜像加速

找到**镜像工具**下的**镜像加速器**：

![image-20240103135237984](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240103135237984.png)

页面向下滚动，即可找到配置的文档说明：

![image-20240103135245495](https://wuriteup.oss-cn-qingdao.aliyuncs.com/writeupLeast/image-20240103135245495.png)

具体命令如下（centos）：

```shell
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://mt6zj1r3.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

具体命令如下（ubuntu）：

```shell
sudo mkdir -p /etc/docker

sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://mt6zj1r3.mirror.aliyuncs.com"]
}
EOF

sudo systemctl daemon-reload
sudo systemctl restart docker
```

## 1.5 删除命令

```shell
# 停止所有容器
sudo docker stop $(docker ps -aq)

# 删除所有容器
sudo docker rm $(docker ps -aq)

# 删除所有镜像
sudo docker rmi $(docker images -q)

# 卸载docker引擎
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine

# 删除docker数据目录
sudo rm -rf /var/lib/docker

# 查看是否有漏掉的docker依赖
yum list installed | grep docker
yum remove <xxxxx>
```

# 2、Docker快速入门

## 2.1 部署MySql

而使用Docker安装，仅仅需要一步即可，在命令行输入下面的命令（建议采用CV大法）：

```shell
docker run -d \
  --name mysql \
  -p 3306:3306 \
  -e TZ=Asia/Shanghai \
  -e MYSQL_ROOT_PASSWORD=123 \
  mysql
```

Docker会自动搜索并下载MySQL。注意：这里下载的不是安装包，而是**镜像（image）。**镜像中不仅包含了MySQL本身，还包含了其运行所需要的环境、配置、系统级函数库。因此它在运行时就有自己独立的环境，就可以跨系统运行，也不需要手动再次配置环境了。这套独立运行的隔离环境我们称为**容器（container）**。

**镜像仓库**：Docker官方提供了一个专门管理、存储镜像的网站，并对外开放了镜像上传、下载的权利。Docker官方提供了一些基础镜像，然后各大软件公司又在基础镜像基础上，制作了自家软件的镜像，全部都存放在这个网站。这个网站就成了Docker镜像交流的社区：https://hub.docker.com

