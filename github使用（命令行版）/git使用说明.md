# Git使用命令说明

## 1 克隆一个项目
命令格式如下：
	git clone 网址
网址是在github上你自己复制的url，通常以https打头，eg:
	git clone https://github.com/Alliance-Algorithm/UGAS.git
上面的操作，默认克隆的是master分支，如果你想要克隆项目中的一个分支，要选择后缀，格式为：
	git clone -b 分支名称 项目的url
举例如下：
我的项目中有一个cmake_support分支和一个master分支，想要克隆cmake_support分支。
	git clone -b cmake_support https://github.com/Alliance-Algorithm/UGAS.git

## 2 更改项目
在你把项目克隆到你的电脑上以后，你会发现项目整个的文件夹都跑到你的电脑上了。如果你把隐藏的文件打开，你会发现有一个.git文件夹，不要动他，他告诉了你这个项目是从git上面拉下来的。你后面在这里做的更改都会被github看到并且比对到。
如果你想要更改你的项目，只需要正常修改就行，改变会被github自动监测到。

## 3 提交更改
先把更改的文件夹加入进去，然后写提交说明，具体格式为：
	git add 更改的文件/文件夹
	git commit -m "你描述的信息"
描述的信息可以任意写，但是更改的文件夹不可以。

## 4 上交到github主页
格式如下：
	git	push origin 分支名称
在不断网的情况下，你就把你的更改提交到了对应的分支上。

## 5 Fork和pull request
在github上，你可以把别人的项目克隆到你自己的github平台上，此时你在这个平台上就拥有了这个项目，它就相当于你自己的。你可以将你自己平台上的这份项目做出更改。这种操作在github上属于fork操作。具体流程如下：

<ol>
<li> 打开github项目，在右上角有一个fork按钮。
<li> 点击fork按钮，你就把项目fork到了你的github上。
<li> 在进行fork操作时，系统会让你建立仓库，选择你要克隆的分支。如果你想要把全部项目克隆下来，下面有个选项：copy the master branch only，不要选他，否则你就只能把master克隆下来了。点击下面的绿色create按钮后，你就可以把项目克隆过来了。
</ol>

然后你把这个项目克隆到你的电脑，即可进行修改，而且此修改不会影响到你原始克隆的项目。如果你做出了修改并提交，你登录github网页后会发现一个黄色提醒框，提醒你是否要创建Pull request，如果你要创建，按照提示走就可以啦。