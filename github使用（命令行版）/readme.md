# Git的使用命令集锦

## 1 克隆别人的代码到自己的仓库

我一般使用的是Git.exe，在windows和linux版本上都有。如果你是第一次下载Git，建议首先执行下面命令：

	git config --global http.sslVerify false

否则你后面会报fatal error。

然后，新建一个文件夹（个人建议在你的电脑里面专门新建一个文件夹用于存放Git下来的代码。然后进入到这个文件夹，右击，选择<code>Git Bash here</code>，弹出黑色框。在黑色框输入下面的命令：
	git clone 你要克隆代码的网址
我一般选择https的网址，回车，你就把代码克隆进来了。
