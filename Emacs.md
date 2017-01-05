#emacs用法
Emacs不仅仅是一个文本编辑器，更几乎是一个操作系统，对于很多人而言，在Emacs里几乎可以做所有工作。它通过为不同类型任务提供一个集成环境来使得你工作更高效。
如果Emacs不能以你喜欢的方式工作，你可以通过Emacs Lisp语言来定制Emacs。
启动Emacs后，C-h t查看tutorial，C-h r查看Emacs manual，C-h C-h查看所有帮助。
Emacs命令很多，把它们都对应到CONTROL和META组合键上不太可能，Emacs用扩展命令解决这个问题，扩展命令有两种风格：
 1. C-x 字符扩展。 C-x之后输入另一个字符或者组合键
 2. M-x 命令名扩展。 M-x之后输入一个命令名。M-x通常并不常用，只用在部分模式下，如替换

##启动Emacs
emacs --nw或emacs myFileName


下面介绍Emacs的基本操作：
 - C-x C-f：打开文件
 - C-x C-s：保存文件
 - C-x C-b：列出缓冲区，every file is shown in a “buffer”. (You can think of “buffer” as opened file or tabbed window without the tab.)
 - C-x b：切换缓冲
 - C-x k：kill buffer，关闭当前文件
 - C-x C-c：离开Emacs
 - C-x u：撤销
 - C-v：向前移动一屏，M-v 向后移动一屏
 - C-l：将光标所在行置于屏幕的中央
 - C-p, C-n：上下行移动

META系列组合键用来操作“由语言定义的单位（比如词，句子，段落）；CONTROL系列组合键用来操作“与语言无关的基本单位（比如字符，行等）
 - C-a, C-e移动到“一行”的头尾，M-a, M-e移动到“一句”的头尾。
 - C-f, C-b移动“字符”，M-f, M-b移动“词”
 - C-d删除一个字母，M-d删除一个单词
 - M-<, M->移动到文件的头尾
 - C-u 8 C-f向前移动8个字符

### 重复次数：大部分Emacs命令都可以指定命令重复次数，默认是4次。 
 - C-u 8 C-v：屏幕向下滚动8行
 - C-u C-u C-n：光标向下移动16行
 - C-u 100 C-g C-f：C-g使得命令终止，取消参数

C-g：终止命令，取消参数。不小心按了ESC，可以用C-g来取消。不过取消ESC的正确做法是再连按两次ESC

### 搜索
 - C-s：前向搜索，再按一次C-s，跳到下一个命中位置，按退格键光标返回到上一个命中位置，按enter结束搜索。
 - C-r：后向搜索
 - C-s C-s：search the same word searched last time, C-s C-w: search the word under the cursor.
 - C-s M-p：搜索历史中上一项
 - C-s M-n：搜索历史中下一项

### 标签
 - C-SPC/C-@：在当前位置设置标签。然后移动到复制结束点，“M-w"复制选中区域到系统的缓冲区，“C-w”剪贴选中区域。
 - C-x C-x：Swap point and mark，选中当前点和标签之间的内容，返回到上个标签位置

### 区域：point和mark之间的区域，很多命令只对该区域操作，如下
 - C-x h：全选
 - M h
 - C-x n n
 - C-x n w

### 移除(Killing,"cutting")
 - C-k: 移除从光标到“行尾”间的字符
 - M-k: 移除从光标到“句尾”间的字符
 - <Delback>：删除光标前的一个字符
 - C-d：删除光标后的一个字符
 - M-<Delback>：移除光标前的一个词
 - M-d：移除光标后的一个词
 - C-u 10 C-k：删除10行
 - C-w：剪切
 - M-w：保持区域

### 召回(Yanking,"pasting")
将被移除的文字恢复的动作称为“召回”
 - C-y：召回你最后移除的文字，粘帖
 - M-y：用C-y召回最近一次移除的文字后，紧接着再按M-y召回再前一次被移除的内容，再按M-y召回再上一次，重复。

### 撤销Undo：三种方法
 - C-x u
 - C-/

### 搜索和替换
 - M-x repl(tab补全) s(tab补全) replacedfloat replacement  

### 正则表达式搜索
 - C-M-s

### 正则表达式搜索与替换
 
### 多窗格
 - C-u 0 C-l：移动光标到这一行
 - C-x 3：左右切屏
 - C-x 2：上下切屏
 - C-x 1：关掉其它所有窗口，只保留一个
 - C-M-v：滚动下方的窗格
 - C-X o：光标转移到下方的窗格
### 帮助命令
 - C-h c：再输入一个组合键，Emacs会给出这个命令的简要说明
 - C-h k：再输入一个组合键，Emacs会打开一个窗格显示函数的名称及其文档，C-x 1关闭窗格。
 - C-h f：解释给定的命令
 - C-h a：通过关键词或正则搜索命令
### [note](http://ergoemacs.org/emacs/emacs_fun.html)
#### call a command by name, type M-x, q quit
calendar,calc,list-colors-display,dired,shell

 - split-window-below → split top/bottom.
 - split-window-right → split side-by-side.
 - delete-other-windows → unsplit.
 - other-window → move cursor to another pane. (or click mouse)
 - whiterspace-mode: make spaces and tabs visible
 - How to disable automatic "backup~" or "#aucto-save#" file: put `(setq make-backup-files nil) ; stop creating those backup~ files` or `(setq auto-save-default nil) ; stop creating those #auto-save# files` in your emacs init file
 - How to set emacs so that all backups are placed into one backup folder?
 
 ```
 ;; backup in one place. flat, no tree structure
(setq backup-directory-alist '(("" . "~/.emacs.d/emacs-backup")))
 ```
 
 
 
 

### 安装emacs24
在ubuntu中，执行sudo apt-get -f install emacs24
### 配置init.el
emacs配置的核心是初始化文件（Initialization File）init.el，在linux系统中，文件放置在C:/.emacs.d/init.el。如果你将 init.el 文件放在了正确地路径中，Emacs将会自动加载该文件。另外，你也可以在命令行输入emacs -q --load <path to init.el> 命令，启动Emacs。

配置示例代码的第一部分安装了better-defaults和material-theme两个插件包，第二部分是基本自定义。
http://www.open-open.com/lib/view/open1451802607011.html

### 包管理
启动emacs后，会有一个叫ELPA(Emacs Lisp Package Archive)的包仓库，用来安装和管理插件包。打开包管理：M-x package-list-packages


    【Enter ↵】 (package-menu-describe-package) → Describe the package under cursor.
    【i】 (package-menu-mark-install) → mark for installation.
    【u】 (package-menu-mark-unmark) → unmark.
    【d】 (package-menu-mark-delete) → mark for deletion (removal of a installed package).
    【x】 (package-menu-execute) → for “execute” (start install/uninstall of marked items).
    【r】 (package-menu-refresh) → refresh the list from server.
upgrade packages, just press 【U x】.
New packages are installed at ~/.emacs.d/elpa/.
#### elpy——python开发插件
安装elpy插件包
```
(defvar myPackages
  '(better-defaults
    elpy ;; add the elpy package
    material-theme))
```
启用插件
```
(elpy-enable)
```
Python缓冲区按下 C-c C-c 即可运行这个脚本。

### Lisp语言
```
;; 我们要让Emacs工作在lisp-interaction-mode工作模式下，
;; 这个模式可以让我们在缓冲区中和Emacs进行互动，并且直接执行Lisp命令,得到结果。
;; 进入lisp-interaction-mode的方法： 把光标移动到辅助输入区，键入M-x lisp-interaction-mode 

;; 冒号在Lisp中表示注释
;; 计算一个表达式,(+ 3 (+ 1 2))把光标放在这里，并且键入Ctrl-j 

```
### 其他
Emacs在编辑时会为每个文件提供“自动保存”的机制，自动保存的文件的文件名前后都有一个#，用户正常保存后，Emacs就会删除这个#文件。

### org-mode
参考[一年成为emacs高手](https://github.com/redguardtoo/mastering-emacs-in-one-year-guide/blob/master/guide-zh.org)，
[org](http://orgmode.org/)是全能的笔记工具，需要安装这个插件。
 > M-x package-install RET org

### c++配置
[Emacs as C++ IDE](http://blog.binchen.org/posts/emacs-as-c-ide-easy-way.html)

### 已有配置

#### Emacs 显示行号
```
Emacs需要第三方插件显示行号
1.下载 linum.el。在网上搜一下，许多网站都提供下载。
2.复制 linum.el 到“/usr/share/emacs/site-lisp/”

3.配置  ~/.emacs 。如果主目录下，没有这个文件，需要新建。
;;(setq column-number-mode t)
;;(setq line-number-mode t)
(global-linum-mode t)
4.或者在Emacs下执行 M-x linum-mode 来显示或者取消行号
M-x ： Alt + x
输入： linum-mode
```
#### Emacs更改背景颜色
```
Emacs的配置文件在~/.emacs。现在就用Emacs打开这个文件吧，如果没有就创建一个。首先改一下颜色配置，让Emacs看起来更酷一些:
(set-background-color "black/#CCE8CF") ;; 使用黑色背景
(set-foreground-color "white") ;; 使用白色前景
(set-face-foreground 'region "green")  ;; 区域前景颜色设为绿色
(set-face-background 'region "blue") ;; 区域背景色设为蓝色
```
## 参考
 - emacs http://www.gnu.org/software/emacs/download.html
 - http://www.gnu.org/software/emacs/manual/pdf/emacs.pdf
 - http://www.jesshamrick.com/2012/09/10/absolute-beginners-guide-to-emacs/
 - https://www.gnu.org/software/emacs/tour/
 - http://ergoemacs.org/emacs/emacs_package_system.html
## vim用法
 - http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO-1.html
