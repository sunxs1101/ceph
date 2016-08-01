# GO语言学习


## 下载和安装go

```
wget https://golang.org/doc/install?download=go1.6.3.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.6.3.linux-amd64.tar.gz
```

注意，一定要解压到 `/usr/local`。

随后在`/etc/profile`中添加

```
export PATH=$PATH:/usr/local/go/bin
```


## Go的工作空间

具体请参见 https://golang.org/doc/code.html#Workspaces

Go语言编程一般把所有Go代码放到一个workspace，比如`~/work`：

```
mkdir -p ~/work/
export GOPATH=$HOME/work
```

Go 编译器根据 `$GOPATH` 知道 workspace 在哪儿。


## 写一个和执行程序

```
mkdir -p src/helloworld
cd src/helloworld
vim src/hello.go
```

其中, `hello.go` 的内容如下：

```
package main

import "fmt"

func main(){
  fmt.Printf("Hello, World!\n")
}
```

### 编译和执行

一个简单的（但是不常用的）方法是 `go run`：

```
cd ~/work/src/helloworld
go run hello.go
```

规范的方式是用 `go install`，它build执行程序，并且输出到 `~/work/bin/helloworld`：

```
cd helloworld && go install
ls ~/work/bin/helloworld
```

注意，可执行文件的名字 helloworld 来自源码目录的名字 helloworld，而不是源码文件 hello.go 。


## 写一个Package

```
mkdir ~/work/src/stringutil
cd ~/work/src/stringutil
vim strutil.go
```
其中 `strutil.go` 的内容如下：

```
package stringutil

func Reverse(s string) string {
	r := []rune(s)
	for i, j := 0, len(r)-1; i < len(r)/2; i, j = i+1, j-1 {
		r[i], r[j] = r[j], r[i]
	}
	return string(r)
}
```

### 编译

```
go install stringutil
```

或者等价于

```
cd ~/work/src/stringutil
go install
```

结果输出在 `$GOPATH/pkg/*/stringutil.a`。注意 `.a`文件的名字是源码目录名字`stringutil`，而不是源码文件名字`strutil.go`。


## 让hello.go调用strutil.go里的内容

修改 `~/work/src/helloworld/hello.go`：

```
package main

import (
	"fmt"

	"stringutil"
)

func main() {
	fmt.Printf(stringutil.Reverse("!oG ,olleH"))
}
```

注意，这里的import path `stringutil` 是相对于 `$GOPATH/src` 的。这也是为什么一定要设置 $GOPATH 的原因。


## 获取和编译Github上的Go项目

```
go get github.com/wangkuiyi/sh
```

相当于

```
mkdir -p ~/work/src/github.com/wangkuiyi
cd  ~/work/src/github.com/wangkuiyi
git clone https://github.com/wangkuiyi/sh
go install github.coim/wangkuiyi/sh
```

`go get` 会自动分析git clone得到的Go源码中的`import`指令，并且递归地git clone相应的项目。


### 从私有Github repo里获取Go项目

1. 在Github页面里生成一个personal access token。一个tokens是一串数字，作用相当于账户和密码。所以一定要私密保存。
2. 告诉 git 每次访问 `github.com` 都通过 `https://<token>:x-oauth-basic@github.com` 来访问。

具体做法，请参见 https://github.com/k8sp/auto-install/issues/29


## 从Github获取和安装Go项目

go get .../goimports （需要翻墙，因为很多基础库在Google服务器上）
 - 
 - ls $GOPATH/bin/goimports
 - $GOPATH/bin/goimports ~/work/src/helloworld/hello.go
 - goimports -w ~/work/src/helloworld/hello.go

 - tree $GOPATH/pkg/
 - go install helloworld/$GOPATH/bin/helloworld
 - $GOPATH/src/github.com/user/stringutil
 - $GOPATH/src/stringutil
 - git config --global url."https://c61axxxxxxxxxxxxxxx:x-oauth-basic@github.com/".insteadOf "https://github.com/" ,vim ~/.gitconfig 你会发现~/.gitconfig中有一些配置
 - export http_proxy=http://10.200.19.203:8118; export https_proxy=http://10.200.19.203:8118。这两句是为了翻墙
 - 运行 go get github.com/k8sp/auto-install/cloud-config-server
 - ls $GOPATH/bin/ | grep cloud-config
 - cd ~/work/src/github.com/k8sp/auto-install/cloud-config-server
 - grep cloud-config*.go
 - vim server.go
   - tp "cloud-config-server/template"==>tp"github.com/k8sp/auto-install/cloud-config-server/template"
 - go install
 - go install github.com/k8sp/auto-install/cloud-config-server

   - 等价与cd ~/work/src/github.com/k8sp/auto-install/cloud-config-server && go install


## 使用 goimports 排版Go源码

Go没有code style。因为Go的作者提供了工具来自动重写源码：

```
go get golang.org/x/tools/cmd/goimports
export PATH=$GOPATH/bin:$PATH
```

注意，goimports 依赖 `golang.org/x/...`，所以执行以上命令之前必须翻墙。最简单的办法是通过环境变量设置http代理：

```
export http_proxy=...
export https_proxy=...
```

这样，就可以用 goimports 自动重新排版源码了：

```
goimports -w ~/work/src/helloworld/hello.go
```

通常我们配置编辑器，在存盘的时候先调用 gopimports 重新排版，然后再存盘。


### 配置Vim

使用这个Vim插件：https://github.com/fatih/vim-go

### 配置Emacs

按照这个流程 http://tleyden.github.io/blog/2014/05/27/configure-emacs-as-a-go-editor-from-scratch-part-2/



## 预先排除任何潜在bug

```
go get -u github.com/alecthomas/gometalinter
gometalinter --install --update --no-vendored-linters
```

注意，对于Go 1.6，必须使用 ` --no-vendored-linters`选项。

随后，即可

```
gometalinter helloworld
```

或者

```
gometalinter stringutil
```


几乎任何潜在的bug，比如并发程序逻辑中的死锁、程序中的死循环、公开的函数或者变量没有写document comment，都会被检查出来。我们提交PR的Go源码，应该是通过gometalinter检查的。


## Travis CI

每个Go项目的Github repo里都应该配置Travis CI做自动检查。自动检查（build和跑unit test）通不过的，PR页面里会用红色或者黄色圆圈标志，不应该被Merge。具体配置方法，请参加Travis页面里的帮助信息。

Travis CI应该被配置成除了build和unit test，还要调用 gometalinter 做检查。（TODO：王益）


## Unit Test

关于如何写 unit test，请参见 https://golang.org/pkg/testing/ 。Unit test源码都在有 `_test`后缀的源文件里，比如 `strutil_test.go`。

写好之后，运行 `go test <package-path-based-on-$GOPATH/src>` 来测试。

注意，`go install` 只编译没有 `_test` 后缀的源文件，所以那些 `_test.go` 里的代码尽可以不优化执行效率，尽可以导致产生很大的可执行文件。


## 文档

任何开源项目的文档都可以通过 godoc.org 自动生成。比如 https://github.com/wangkuiyi/sh 的文档在 https://godoc.org/github.com/wangkuiyi/sh 。

godoc.org会去读取URL里指定的repo的默认branch（一般都是master），分析其中源码，根据package和函数定义之前的注释，自动生成文档。


