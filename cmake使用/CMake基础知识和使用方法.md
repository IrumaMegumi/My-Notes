<center>

# CMake基础知识和使用方法

</center>

# 1 gcc的使用和Linux下编译C++的流程

## 1.1 gcc/g++的使用

在windows中，我们常常使用visual studio运行C/C++程序代码，只需要按下ctrl+F5即可运行。但是，作为一个新的系统，Linux和微软是死对头一般的存在，因此Visual Studio是不提供Linux版本的。为了能够利用号Linux系统的优良特性，gcc/g++和CMake两大工具就应运而生了。它们可以实现输入一些简单的命令行编译C/C++程序。

这里首先介绍一下gcc/g++的使用方法，并让大家熟悉以下在Linux系统下编译C/C++程序的流程。

### (1)创建文件
假如你的电脑没有VScode，那么创建一个.c/cpp文件需要使用touch，vim等命令。首先使用下面命令创建并且转到相应文件夹：

    mkdir test
    cd test

mkdir是创建文件夹的指令，在Linux下打开终端后使用此命令，即可在对应的路径下创建test文件夹。cd是修改终端运行路径的指令。

后运行下面指令在test下新建和编辑文件：

    touch test.cpp
    vim test.cpp

touch是创建新文件的命令，vim是在终端窗口编辑文件的命令。如果你的电脑下载了vscode，vim可以使用code代替。

打开vim后界面如下所示：

<center>
<img src="./01.png" width=70%>
</center>

文件中的～表示这一行没有任何东西。下面会有文件的文件名，行数，存储内存的信息，若你此时按下了键盘的i键，你会发现界面变成了如下图所示的图案：

<center>
<img src="./02.png" width=70%>
</center>

最后一行变成了插入，这种模式叫做编辑模式，只有处于编辑模式下，你才可以在文件中输入内容。如果输入完，想要推出进行保存，需要按下esc键，并输入：wq，即可完成保存。这里我就现输入常规的hello,world代码。

如果你想要查看文件的内容，可以使用cat指令查看，具体如下：

    cat test.cpp

此时文件的内容会在终端显示出来。

关于vim的更多细节，可以参考下面的链接：https://www.runoob.com/linux/linux-vim.html 。

### (2)使用gcc/g++编译文件

写完代码后，接下来要做的事情就是编译了。如果对于单独的文件或者数量较少的文件，你可以直接使用gcc(针对C语言)或g++(针对C++)工具编译。具体格式如下：

    gcc/g++ 你需要编译的文件名 -o 生成的可执行文件名
    eg:
    g++ test.cpp -o Hello

此时使用ls查看，你会发现目录下多了一个绿色的东西，名称为Hello，这个文件就是Linux下的可执行文件，相当于windows中的.exe文件。
<center>
<img src="./03.png" width=70%>
</center>

然后在命令行中把可执行文件的路径输入进去，就可以运行输出Hello，world了。

<center>
<img src="./04.png" width=70%>
</center>

注意：./的含义为在当前文件夹下。

## 1.2 C/C++文件在Linux下整个的编译流程

在了解之前，我们首先看一下gcc/g++的帮助文档。

<center>
<img src="./05.png" width=70%>
</center>

可以看到有only compile, compile but not link一类的字样，说明和windows一样，使用gcc/g++编译的时候也是有一定流程将其一步一步转化的。

在windows中，编译cpp程序的步骤为：.cpp--->.obj--->.exe。linux中分为四个步骤，按照顺序，在gcc/g++中分别对应 -E，-S，-c，gcc/g++连接三个后缀和一个连接指令，依次编译生成.i(预处理后的文件)、.s(编译后产生的文件)、.o(编译整合后产生的文件)、.out(可执行文件)，后缀-o是用来修改生成文件的名称的。

例如：

    g++ -E test.cpp -o Hello   生成Hello.i文件
    g++ -S Hello.i -o Hello    生成Hello.s文件
    g++ -c Hello.s -o Hello    生成Hello.o文件
    g++ Hello.o Hello          生成Hello.out，如果你用ls查看会发现是一个绿色的文件

但是如果你的源文件非常多，你使用gcc/g++工具，只能一路.cpp，就修改一次你就要输入一次，非常麻烦，这时就需要使用工具CMake了。

# 2 CMake的使用

## 2.1 MakeFile和CMakeList

MakeFile和CMakeList可以近似地理解为程序编译的说明文档。写好一个编译文档后，你在Linux系统的命令行中，只要使用一个make指令，就可以对所有的.c/.cpp文件进行编译运行了，效果与前面的gcc/g++，后面跟了一大堆.c/.cpp相同。维护的时候，只需要修改对应的编译文档即可，较为简便。但是二者也有不同之处。

MakeFile是CMakeList编译后产生的产物，也是系统编译的时候make指令直接运行的文件，可以手写，但是不同的系统下写法不同，比如，你在Linux下是一种写法，在Windows下就是另一种写法，会给开发造成不便，因此不太推荐使用，除非你是某个系统的忠实粉丝。CMakeList具有统一的语法格式，一个CMakeList在不同的系统下，只要有CMake，都可以运行起来。教程的后续都会围绕CMakeList进行展开说明。

## 2.2 只有一个文件时CMakeList的写法

### (1)创建CMakeList
创建一个CMakeList。CMakeList的格式一般为.txt，如果你的电脑上有VSCode，可以直接在VSCode上创建。没有的话可以使用指令touch或指令vi进行创建。这里展示使用touch创建的方法，使用和上面相同的指令：

    touch CMakeLists.txt
    vim CMakeLists.txt

名字比较长，在vim那一行，你可以使用Tab键自动补全文件名。注意：文件名一定要是CMakeLists.txt，s不可以省略！！！

### (2)CMakeList的书写

由于CMakeList的语法较杂，因此在后面的部分中会进行简单的介绍，在第三部分会对语法进行一个总结。

首先，一般的CMakeList的第一行都会指定要求最低版本要求，以避免有功能无法运行的情况。具体格式如下：

    CMAKE_MINIMUM_REQUIRED(VERSION 版本号 错误信息)

含义为：前面的<code>CMAKE_MINIMUM_REQUIRED</code>是固定的指令，表示所需最低版本号，特别注意，要全部大写！！！VERSION也是固定的，后面跟随的是你需要的最低版本，错误信息可有可无，表示如果我的CMake版本低于当前版本，那么系统在编译的时候会报什么错误。

CMakeList的第二行一般为指定工程名称。格式如下：

    PROJECT(工程名 使用的语言)

使用的语言只支持C、C++和java，C++要用CXX表示，什么也不写默认为C++。

然后添加可执行文件及其对应的依赖。可执行文件就是前面我说的.out或这ls查看后那个绿色的文件。依赖的意思是，我的可执行文件是通过什么头文件编译出来的。比如前面的命令：g++ main.cpp，产生了main.out，我们就称main.cpp是main.out的依赖文件。具体的命令格式如下：

ADD_EXECUTABLE(可执行文件名称 依赖文件名称)

如果你是单独的一个文件编译，那么到这里你就写完啦。之后使用cmake工具编译当前目录即可，具体的命令格式如下：

    cmake ./

如果没有错误编译成功后，你会发现所在的文件夹下多了一些文件，如下图所示：
<center>
    <img src="./06.png" width=60%>
</center>

你会发现多了MakeFile文件，说明我们可以编译了，然后再输入命令<code>make</code>，就可以编译生成可执行文件了。

我的CMakeLists.txt的代码如下所示：

    CMAKE_MINIMUM_REQUIRED(VERSION 3.0)
    PROJECT(test_01 CXX)
    ADD_EXECUTABLE(test_02 test.cpp)

在编译后，你会发现，产生的可执行文件名叫做test_02，test_01找不到踪迹，说明工程名是无关紧要的，重要的是可执行文件名称。所以，往往编译者更加倾向于把工程名、可执行文件名统一命名。