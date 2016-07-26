#emacs用法
Emacs不仅仅是一个文本编辑器，更几乎是一个操作系统，对于很多人而言，在Emacs里几乎可以做所有工作。它通过为不同类型任务提供一个集成环境来使得你工作更高效。
如果Emacs不能以你喜欢的方式工作，你可以使用Emacs Lisp语言来定制Emacs。
启动Emacs后，C-h t查看tutorial。C-h r查看Emacs manual。C-h C-h查看所有帮助。
Emacs命令很多，把它们都对应到CONTROL和META组合键上不太可能。Emacs用扩展命令解决这个问题，扩展命令有两种风格：
 1. C-x 字符扩展。 C-x之后输入另一个字符或者组合键
 2. M-x 命令名扩展。 M-x之后输入一个命令名

M-x通常并不常用，只用在部分模式下。如替换
 - C-x C-f：打开文件
 - C-x C-s：保存文件
 - C-x C-b：列出缓冲区
 - C-x C-c：离开Emacs
 - C-x 1：关掉其它所有窗口，只保留一个
 - C-x u：撤销
 - C-v：向前移动一屏，M-v 向后移动一屏
 - C-l：将光标所在行置于屏幕的中央
 - C-p, C-n：上下行移动

META系列组合键用来操作“由语言定义的单位（比如词，句子，段落）；CONTROL系列组合键用来操作“与语言无关的基本单位（比如字符，行等）
 - C-a, C-e移动到“一行”的头尾，M-a, M-e移动到“一句”的头尾。
 - C-f, C-b移动“字符”，M-f, M-b移动“词”
 - M-<, M->移动到文件的头尾
 - C-u 8 C-f向前移动8个字符

### 重复次数：大部分Emacs命令都可以指定，默认是4次。 
 - C-u 8 C-v：屏幕向下滚动8行
 - C-u C-u C-n：向下移动16行
 - C-u 100 C-g C-f，C-g：终止命令，取消参数

C-g：终止命令，取消参数。不小心按了ESC，可以用C-g来取消。不过取消ESC的正确做法是再连按两次ESC

### 搜索
 - C-s：前向搜索，再按一次C-s，跳到下一个命中位置，按退格键光标返回，按enter结束搜索。
 - C-r：后向搜索
 - C-s M-p：搜索历史中上一项
 - C-s M-n：搜索历史中下一项

### 标签
 - C-SPC/C-@：Set mark to the current location,在当前位置设置标签
 - C-x C-x：Swap point and mark，选中当前点和标签之间的内容，返回到上个标签位置

### 区域：point和mark之间的区域，很多命令只对该区域操作
 - C-x h
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
 - C-w：删除区域("cut")
 - M-w：保持区域

### 召回(Yanking,"pasting")
将被移除的文字恢复的动作称为“召回”
 - C-y：召回你最后移除的文字
 - M-y：用C-y召回最近移除的文字后，紧接着再按M-y召回再前一次被移除的内容，再按M-y召回再上一次，重复。

### 撤销Undo：三种方法
 - C-x u
 - C-_
 - C-/

### 搜索和替换
 - M-% 

### 正则表达式搜索
 - C-M-s
 - 

### 正则表达式搜索与替换
 
### 多窗格
 - C-u 0 C-l：移动光标到这一行
 - C-x 2：将屏幕分成两个
 - C-M-v：滚动下方的窗格
 - C-X o：光标转移到下方的窗格
 - C-x 1：关掉下方窗格
### 命令帮助
 - C-h c：再输入一个组合键，Emacs会给出这个命令的简要说明
 - C-h k：再输入一个组合键，Emacs会打开一个窗格显示函数的名称及其文档，C-x 1关闭窗格。
 - C-h f：解释给定的命令
 - C-h a：通过关键词或正则搜索命令

### 安装
在ubuntu中，执行sudo apt-get -f install emacs24
### 配置
emacs配置的核心是初始化文件init.el，在linux系统中，文件放置在C:/.emacs.d/init.el

http://www.open-open.com/lib/view/open1451802607011.html



 - emacs http://www.gnu.org/software/emacs/download.html
 - http://www.gnu.org/software/emacs/manual/pdf/emacs.pdf
 - http://www.jesshamrick.com/2012/09/10/absolute-beginners-guide-to-emacs/
 - https://www.gnu.org/software/emacs/tour/

#vim用法总结

http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO-1.html
