# Linux系统go语言环境配置

## 1、下载最新安装包

​		到官网下载最新安装包，命令实例：

```shell
mkdir ~/install
cd ~/install
wget https://golang.google.cn/dl/go1.21.5.linux-amd64.tar.gz
```

## 2、解压安装包

```shell
tar -zxvf go1.21.5.linux-amd64.tar.gz -C ~/
```

## 3、检查go语言工具包是否存在

```shell
zewardwang@iZbp13y5onmmubvs06mc94Z:~$ ls $HOME/go/bin
go  gofmt
```

## 4、设置GOROOT、GOPATH、GOBIN、PATH环境变量

```shell
echo 'export GOROOT=$HOME/go' >> ~/.bashrc
mkdir ~/gowork
echo 'export GOPATH=$HOME/gowork' >> ~/.bashrc
echo 'export GOBIN=$GOROOT/bin' >> ~/.bashrc
echo 'export PATH=$GOBIN:$GOPATH/bin:$PATH' >> ~/.bashrc
```

## 5、刷新环境变量并查看

```shell
source .bashrc 
go env

GO111MODULE=''
GOARCH='amd64'
GOBIN='/home/zewardwang/go/bin'
GOCACHE='/home/zewardwang/.cache/go-build'
GOENV='/home/zewardwang/.config/go/env'
GOEXE=''
GOEXPERIMENT=''
GOFLAGS=''
GOHOSTARCH='amd64'
GOHOSTOS='linux'
GOINSECURE=''
GOMODCACHE='/home/zewardwang/gowork/pkg/mod'
GONOPROXY=''
GONOSUMDB=''
GOOS='linux'
GOPATH='/home/zewardwang/gowork'
GOPRIVATE=''
GOPROXY='https://proxy.golang.org,direct'
GOROOT='/home/zewardwang/go'
GOSUMDB='sum.golang.org'
GOTMPDIR=''
GOTOOLCHAIN='auto'
GOTOOLDIR='/home/zewardwang/go/pkg/tool/linux_amd64'
GOVCS=''
GOVERSION='go1.21.5'
GCCGO='gccgo'
GOAMD64='v1'
AR='ar'
CC='gcc'
CXX='g++'
CGO_ENABLED='1'
GOMOD='/dev/null'
GOWORK=''
CGO_CFLAGS='-O2 -g'
CGO_CPPFLAGS=''
CGO_CXXFLAGS='-O2 -g'
CGO_FFLAGS='-O2 -g'
CGO_LDFLAGS='-O2 -g'
PKG_CONFIG='pkg-config'
GOGCCFLAGS='-fPIC -m64 -pthread -Wl,--no-gc-sections -fmessage-length=0 -ffile-prefix-map=/tmp/go-build2323199315=/tmp/go-build -gno-record-gcc-switches'
```



