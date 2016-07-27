# GO语言说明

用Vim编辑Go程序的话，貌似应该安装这个Vim插件：https://github.com/fatih/vim-go
## 下载和安装go
从https://golang.org/doc/install?download=go1.6.3.linux-amd64.tar.gz 下载
 - sudo tar -C /usr/local -xzf go1.6.3.linux-amd64.tar.gz
 - 在etc/profile中添加export PATH=$PATH:/usr/local/go/bin
 - source /etc/profile

## Go的开发目录
https://golang.org/doc/code.html#Workspaces
 - mkdir ~/work
 - cd ~/work
 - export GOPATH=$(pwd)
 - mkdir -p src/helloworld
 - cd src/helloworld

## 写一个Go程序(helloworld)
 - vim src/helloworld.go

 ```
package main
   import "fmt"
   func main(){
    fmt.Printf("Hello,world.\n")
   }
``` 
 - go run helloworld.go
 - 在目录里执行go install
 - ls ~/work/bin/helloworld 这是go install输出
 - 打开https://golang.org/doc/code.html，查看workspace中的目录树，前面是手动创建src，在src下创建helloworld，接下来创建一个library
## 写一个Go库
 - mkdir ~/work/src/stringutil
 - cd ~/work/src/stringutil
 - vim s.go
 ```
// Package stringutil contains utility functions for working with strings.
package stringutil

// Reverse returns its argument string reversed rune-wise left to right.
func Reverse(s string) string {
	r := []rune(s)
	for i, j := 0, len(r)-1; i < len(r)/2; i, j = i+1, j-1 {
		r[i], r[j] = r[j], r[i]
	}
	return string(r)
}
 ```
 - go install stringutil
 - ls $GOPATH/pkg/
 - tree $GOPATH/pkg/
 - go install helloworld/$GOPATH/bin/helloworld

 - git config --global url."https://133bf72ae1273a750e9094c4080613e8e232ca85:x-oauth-basic@github.com/".insteadOf "https://github.com/"
 - vim ~/.gitconfig
 - export http_proxy=http://10.200.19.203:8118
 - export https_proxy=http://10.200.19.203:8118
 - go get github.com/k8sp/auto-install/cloud-config-server
 - ls $GOPATH/bin/ | grep cloud-config
 - cd ~/work/src/github.com/k8sp/auto-install/cloud-config-server
 - grep cloud-config*.go
 - vim server.go
   - tp "cloud-config-server/template"==>tp"github.com/k8sp/auto-install/cloud-config-server/template"
 - go install
 - go install github.com/k8sp/auto-install/cloud-config-server

   - 等价与cd ~/work/src/github.com/k8sp/auto-install/cloud-config-server && go install

## go install

## go get .../goimports （需要翻墙，因为很多基础库在Google服务器上）
 - go get golang.org/x/tools/cmd/goimports
 - ls $GOPATH/bin/goimports
 - $GOPATH/bin/goimports ~/work/src/helloworld/helloworld.go
 - goimports -w ~/work/src/helloworld/helloworld.go

## 使用 goimports 排版Go源码

## 配置Vim和Emacs在存盘时自动调用goimports
 - http://tleyden.github.io/blog/2014/05/27/configure-emacs-as-a-go-editor-from-scratch-part-2/

## go get from private Github repo
 - go get github.com/k8sp/auto-install/cloud-config-server

## go命令解释
 - go install：用于编译并安装指定的代码包及它们的依赖包。
 - go get ==> go clone+go install 
 - go test:go test编译所有go文件包括test。运行go时忽略_test.go文件。
   - go test -v 
 - go build：用于编译我们指定的源码文件或代码包以及它们的依赖包。

## Github personal access token 的生成和意思
#### the problem
参考[这篇文档](https://github.com/k8sp/auto-install/issues/29)
 - 个人github页面 -> settings -> Personal access tokens
 - 这个token包括用户名和密码，私密保存

## 配置 git 使用 token 访问 Github.com


 
## 参考
- http://wiki.jikexueyuan.com/project/go-command-tutorial/0.2.html

