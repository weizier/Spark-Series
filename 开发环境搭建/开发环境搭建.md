
　　由于Spark是用Scala来写的，所以Spark对Scala肯定是原生态支持的，因此这里以Scala为主来介绍Spark环境的搭建，主要包括四个步骤，分别是：JDK的安装，Scala的安装，Spark的安装，Hadoop的下载和配置。为了突出"From Scratch"的特点（都是标题没选好的缘故），所以下面的步骤稍显有些啰嗦，老司机大可不必阅读，直接跳过就好。
　　
# 一．JDK的安装与环境变量的设置

## 1.1 JDK的安装

　　**JDK**（全称是JavaTM Platform Standard Edition Development Kit）的安装，下载地址是[Java SE Downloads](http://www.oracle.com/technetwork/java/javase/downloads/index.html)，一般进入页面后，会默认显示一个最新版的JDK，如下图所示，当前最新版本是JDK 8，更为详细具体的地址是[Java SE Development Kit 8 Downloads](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)：<br>
![](http://i.imgur.com/Pmniwky.png)<br>


　　上图中两个用红色标记的地方都是可以点击的，点击进去之后可以看到这个最新版本的一些更为详细的信息，如下图所示：<br>

![](http://i.imgur.com/XQM36qh.png)<br>

　　首先，这里主要包含有8u101和8u102这两个版本，Java给出的官方说明是：
> “Java SE 8u101 includes important security fixes. Oracle strongly recommends that all Java SE 8 users upgrade to this release. Java SE 8u102 is a patch-set update, including all of 8u101 plus additional features (described in the release notes). ”

　　也就是说Java推荐所有开发人员从以前的版本升级到JDK 8u101，而JDK 8u102则除了包括101的所有特性之外，还有一些其他的特性。对于版本的选择，自行选择就好了，其实对于普通开发人员来说，体现不了太大的区别，我这里就是使用的JDK 8u101版本。

　　选好8u101版本后，再选择你的对应开发平台，由于我的机器是64位的，所以我这里选择Windows64位的版本。记得在下载之前，必须要接受上方的许可协议，在上图中用红色圈出。
　　
　　除了下载最新版本的JDK，也可以在[Oracle Java Archive](http://http://www.oracle.com/technetwork/java/javase/archive-139210.html)下载到历史版本的JDK，但官方建议只做测试用。
　　
　　JDK在windows下的安装非常简单，按照正常的软件安装思路去双击下载得到的exe文件，然后设定你自己的安装目录（安装目录在设置环境变量的时候需要用到）即可。
　　
## 1.2 环境变量的设置
　　接下来设置相应的环境变量，设置方法为：在桌面右击【计算机】－－【属性】－－【高级系统设置】，然后在系统属性里选择【高级】－－【环境变量】，然后在系统变量中找到**“Path”**变量，并选择**“编辑”**按钮后出来一个对话框，可以在里面添加上一步中所安装的JDK目录下的bin文件夹路径名，我这里的bin文件夹路径名是：F:\Program Files\Java\jdk1.8.0_101\bin，所以将这个添加到path路径名下，注意用英文的分号“;”进行分割。这样设置好后，便可以在任意目录下打开的cmd命令行窗口下运行
```java
java -version
```
观察是否能够输出相关java的版本信息，如果能够输出，说明JDK安装这一步便全部结束了。<br>

　　全部流程如下图所示（后续软件安装的系统变量设置都是这套流程）：<br>
![](http://i.imgur.com/4JP1bzc.png)

## 1.3 一些题外话
　
　　这里讲两句题外话，各位看官不关心的话可以跳过这里，不影响后续的安装步骤。
　　在软件安装的时候，相信各位没少遇到过环境变量和系统变量，所以这里就来扒一扒令人头疼的**PATH**, **CLASSPATH**和**JAVA_HOME**等参数的具体含义。

### 1.3.1 环境变量、系统变量和用户变量
- 环境变量包括系统变量和用户变量
- 系统变量的设置针对该操作系统下的所有用户起作用；
- 用户变量的设置只针对当前用户起作用

如果对这些概念还不是特别熟悉的，建议先看完下面几个点之后，再回过头来看这三句话。


### 1.3.2 PATH
　　也就是上一步设置的系统变量，告诉操作系统去哪里找到Java.exe的执行路径，当你在命令行窗口冷不丁的敲上如下命令的时候，
```
java -version
```
  操作系统首先会一惊，What the hell does "java" mean? 不过吐槽归吐槽，活还是得干，于是悠悠的记起来了盖茨爸爸说过的三句话：
> 1. 当你看不懂命令行窗口中的一个命令的时候，你首先去你所在的当前目录下找找，是否有这个命令的.exe程序？如果有，那就用它来启动执行；
> 2. 如果没有，千万别放弃，记得要去**Path**系统变量下的那些目录下去找一找，如果找到了，启动并执行命令；
> 3. 如果上面两个地方依然还没找到，那你就撒个娇，报个错好了。

所以我们将JDK安装目录下的bin文件夹添加到**Path**系统变量的目的也就在这里，告诉操作系统：如果在当前目录下找不到java.exe，就去**Path**系统变量里的那些路径下挨个找一找，直到找到java.exe为止。那为什么要设置bin文件夹，而不是JDK安装的根目录呢？原因就在于根目录下没有java.exe啊，只有bin文件夹下才有啊喂......

如果只是在命令行窗口下运行一下java的命令，那其实也可以不设置系统变量，只是每次在命令行窗口运行java的命令时，都必须带上一长串路径名，来直接指定java.exe的位置，如下所示。
```
C:\Users\weizierxu>F:\Program Files\Java\jdk1.8.0_101\bin\java.exe -version
'F:\Program' 不是内部或外部命令，也不是可运行的程序
或批处理文件。
```
注意：这里报错的原因并不是说直接指定java.exe的路径名这种方式有问题，而是命令行下无法解析带有空格的路径名，所以需要用到双引号，如下：
```
C:\Users\weizierxu>"F:\Program Files"\Java\jdk1.8.0_101\bin\java.exe -version
java version "1.8.0_101"
Java(TM) SE Runtime Environment (build 1.8.0_101-b13)
Java HotSpot(TM) 64-Bit Server VM (build 25.101-b13, mixed mode)
```

### 1.3.3 CLASSPATH
　　CLASSPATH是在Java执行一个已经编译好的class文件时，告诉Java去哪些目录下找到这个class文件，比如你的程序里用到某个Jar包（Jar包里的都是已经编译好的class文件），那么在执行的时候，Java需要找到这个Jar包才行，去哪找呢？从CLASSPATH指定的目录下，从左至右开始寻找（用分号区分开的那些路径名），直到找到你指定名字的class文件，如果找不到就会报错。这里做一个实验，就能明白具体是什么意思了。<br>
　　首先，我在F:\Program Files\Java目录下，利用Windows自带的记事本写了一个类似于Hello World的程序，保存为testClassPath.java文件（注意后缀名得改成java），内容如下：
```java
public class testClassPath{
	public static void main(String[] args){
		System.out.println("Hello, this is a test on CLASSPATH!");
	}
}
```
然后，我将cmd的当前目录切换到（通过`cd`命令）F:\Program Files\Java目录下，然后用`javac`命令来对这个`.java`文件进行编译，如下图所示：<br>
![](http://i.imgur.com/iA7dOqN.png)
<br>
从上图中可以看到，`javac`命令可以正常使用（没有任何输出的就表明正确编译了），这是因为执行该命令的javac.exe同样存在于JDK安装路径下的bin目录中，而这个目录我们已经添加到**Path**系统变量中去了，所以cmd能够认识这个命令。这个时候可以看到F:\Program Files\Java目录下多了一个testClassPath.class文件。不过运行这个class文件的时候，报错了。这个时候，CLASSPATH就派上用场了，和**1.2**节中对**Path**系统变量设置的方法一样，这里在CLASSPATH（如果系统变量的列表中没有CLASSPATH这个选项，那么点击**新建**，然后添加路径即可）中最后面添加上`;.`，英文的分号表示和前面已有的路径分割开，后面的小点`.`表示当前目录的意思。<br>
这个时候记得要另起一个新的cmd窗口，然后利用`cd`命令切换到testClassPath.class所在目录，然后再去执行，便可以成功得到结果了。
```
F:\Program Files\Java>java testClassPath
Hello, this is a test on CLASSPATH!
```
　　因此，和**Path**变量不同的是，Java在执行某个class文件的时候，并不会有默认的先从当前目录找这个文件，而是只去**CLASSPATH**指定的目录下找这个class文件，如果**CLASSPATH**指定的目录下有这个class文件，则开始执行，如果没有则报错（这里有去当前目录下找这个class文件，是因为当前路径通过`.`的方式，已经添加到了**CLASSPATH**系统变量中）。<br>
　　上面讲的指定**CLASSPATH**系统变量的方法，都是直接写死在系统变量中的，为了避免造成干扰（比如多个同名class文件存在于多个路径中，这些路径都有添加到**CLASSPATH**系统变量中，由于在找class文件的时候，是从左往右扫描**CLASSPATH**系统变量中的路径的，所以在利用`java testClassPath`方法执行的时候，运行的便是位置在**CLASSPATH**系统变量中最左边的那个路径中，对应的class文件，而这显然不是我们想要的结果），因此在诸如Eclipse等等这些IDE中，并不需要人为手动设定**CLASSPATH**系统变量，而是只设定当前程序的特定的**CLASSPATH**系统变量，这样便不会影响到其他程序的运行了。


### 1.3.4 JAVA_HOME
**JAVA_HOME**并不是Java本身所需要的参数，而是其他的一些第三方工具需要这个参数来配置它们自己的参数，它存在的意义无非是告诉那些软件，我的JDK安装在这个目录下，你如果要用到我的Java程序的话，直接来我这个目录下找就好了，而JAVA_HOME就是JDK的安装路径名。比如我的JDK安装在`F:\Program Files\Java\jdk1.8.0_101`目录下（注意该目录下的bin目录，就是在**1.3.2**节里**Path**系统变量中要添加的值），那么**JAVA_HOME**里要添加的值便是`F:\Program Files\Java\jdk1.8.0_101`，以后碰到类似`HOME`的系统变量，都是软件的安装目录。


# 二. Scala的安装

　　首先从[DOWNLOAD PREVIOUS VERSIONS](http://www.scala-lang.org/download/all.html)下载到对应的版本，在这里需要注意的是，Spark的各个版本需要跟相应的Scala版本对应，比如我这里使用的Spark 1.6.2就只能使用Scala 2.10的各个版本，目前最新的Spark 2.0就只能使用Scala 2.11的各个版本，所以下载的时候，需要注意到这种Scala版本与Spark版本相互对应的关系。我这里现在用的是Scala 2.10.6，适配Spark从1.3.0到Spark 1.6.2之间的各个版本。在版本页面[DOWNLOAD PREVIOUS VERSIONS](http://www.scala-lang.org/download/all.html)选择一个适合自己需要的版本后，会进入到该版本的具体下载页面，如下图所示，记得下载二进制版本的Scala，点击图中箭头所指，下载即可：

![](http://i.imgur.com/u3rO4M0.png)

　　下载得到Scala的msi文件后，可以双击执行安装。安装成功后，默认会将Scala的bin目录添加到**PATH**系统变量中去（如果没有，和JDK安装步骤中类似，将Scala安装目录下的bin目录路径，添加到系统变量**PATH**中），为了验证是否安装成功，开启一个新的cmd窗口，输入`scala`然后回车，如果能够正常进入到Scala的交互命令环境则表明安装成功。如下图所示：<br>
![](http://i.imgur.com/9pwLEUH.png)<br>
如果不能显示版本信息，并且未能进入Scala的交互命令行，通常有两种可能性：
- Path系统变量中未能正确添加Scala安装目录下的bin文件夹路径名，按照JDK安装中介绍的方法添加即可。
- Scala未能够正确安装，重复上面的步骤即可。


# 三. Spark的安装

　　Spark的安装非常简单，直接去[Download Apache Spark](http://spark.apache.org/downloads.html)。有两个步骤：

- 选择好对应Hadoop版本的Spark版本，如下图中所示；
- 然后点击下图中箭头所指的`spark-1.6.2-bin-hadoop2.6.tgz`，等待下载结束即可。<br>

![](http://i.imgur.com/3ymBUON.png)<br>

　　这里使用的是Pre-built的版本，意思就是已经编译了好了，下载来直接用就好，Spark也有源码可以下载，但是得自己去手动编译之后才能使用。下载完成后将文件进行解压（可能需要解压两次），最好解压到一个盘的根目录下，并重命名为`Spark`，简单不易出错。并且需要注意的是，在Spark的文件目录路径名中，不要出现空格，类似于“Program Files”这样的文件夹名是不被允许的。<br>

　　解压后基本上就差不多可以到cmd命令行下运行了。但这个时候每次运行spark-shell（spark的命令行交互窗口）的时候，都需要先`cd`到Spark的安装目录下，比较麻烦，因此可以将Spark的bin目录添加到系统变量**PATH**中。例如我这里的Spark的bin目录路径为`D:\Spark\bin`，那么就把这个路径名添加到系统变量的**PATH**中即可，方法和JDK安装过程中的环境变量设置一致，设置完系统变量后，在任意目录下的cmd命令行中，直接执行`spark-shell`命令，即可开启Spark的交互式命令行模式。




# 四．HADOOP下载

　　系统变量设置后，就可以在任意当前目录下的cmd中运行spark-shell，但这个时候很有可能会碰到各种错误，这里主要是因为Spark是基于Hadoop的，所以这里也有必要配置一个Hadoop的运行环境。在[Hadoop Releases](https://archive.apache.org/dist/hadoop/common/)里可以看到Hadoop的各个历史版本，这里由于下载的Spark是基于Hadoop 2.6的（在Spark安装的第一个步骤中，我们选择的是`Pre-built for Hadoop 2.6`），我这里选择2.6.4版本，选择好相应版本并点击后，进入详细的下载页面，如下图所示，选择图中红色标记进行下载，这里上面的src版本就是源码，需要对Hadoop进行更改或者想自己进行编译的可以下载对应src文件，我这里下载的就是已经编译好的版本，即图中的`hadoop-2.6.4.tar.gz`文件。<br>

![](http://i.imgur.com/CfyCM1Y.png)<br>
　　
　　下载并解压到指定目录，然后到环境变量部分设置**HADOOP_HOME**为Hadoop的解压目录，我这里是`F:\Program Files\hadoop`，然后再设置该目录下的bin目录到系统变量的**PATH**下，我这里也就是`F:\Program Files\hadoop\bin`，如果已经添加了**HADOOP_HOME**系统变量，也可以用`%HADOOP_HOME%\bin`来指定bin文件夹路径名。这两个系统变量设置好后，开启一个新的cmd，然后直接输入`spark-shell`命令。

　　正常情况下是可以运行成功并进入到Spark的命令行环境下的，但是对于有些用户可能会遇到空指针的错误。这个时候，主要是因为Hadoop的bin目录下没有winutils.exe文件的原因造成的。这里的解决办法是：
　　
- 去 https://github.com/steveloughran/winutils 选择你安装的Hadoop版本号，然后进入到bin目录下，找到`winutils.exe`文件，下载方法是点击`winutils.exe`文件，进入之后在页面的右上方部分有一个`Download`按钮，点击下载即可。
- 下载好`winutils.exe`后，将这个文件放入到Hadoop的bin目录下，我这里是`F:\Program Files\hadoop\bin`。
- 在打开的cmd中输入
   ```
F:\Program Files\hadoop\bin\winutils.exe chmod 777 /tmp/hive
  ```
  这个操作是用来修改权限的。注意前面的`F:\Program Files\hadoop\bin`部分要对应的替换成实际你所安装的bin目录所在位置。

　　经过这几个步骤之后，然后再次开启一个新的cmd窗口，如果正常的话，应该就可以通过直接输入`spark-shell`来运行Spark了。
正常的运行界面应该如下图所示：<br>
![](http://i.imgur.com/neY5UZW.png)<br>
从图中可以看到，在直接输入`spark-shell`命令后，Spark开始启动，并且输出了一些日志信息，大多数都可以忽略，需要注意的是两句话：

```
Spark context available as sc.
SQL context available as sqlContext.
```

`Spark context`和`SQL context`分别是什么，后续再讲，现在只需要记住，只有看到这两个语句了，才说明Spark真正的成功启动了。

# 五. Python下的PySpark

　　针对Python下的Spark，和Scala下的spark-shell类似，也有一个PySpark，它同样也是一个交互式的命令行工具，可以对Spark进行一些简单的调试和测试，和spark-shell的作用类似。对于需要安装Python的来说，这里建议使用Python(x,y)，它的优点就是集合了大多数的工具包，不需要自己再单独去下载而可以直接import来使用，并且还省去了繁琐的环境变量配置，下载地址是[Python(x,y) - Downloads](https://python-xy.github.io/downloads.html)，下载完成后，双击运行安装即可。因为本教程主要以Scala为主，关于Python的不做过多讲解。

# 六. 小结

　　至此，基本的Spark本地调试环境便拥有了，对于初步的Spark学习也是足够的。但是这种模式在实际的Spark开发的时候，依然是不够用的，需要借助于一个比较好用的IDE来辅助开发过程。下一讲就主要讲解ItelliJ IDEA以及Maven的配置过程。
　　
# 参考
- [PATH and CLASSPATH](http://https://docs.oracle.com/javase/tutorial/essential/environment/paths.html)（Oracle官方给出的一些关于Path和CLASSPATH的解释，推荐）
- [Difference among JAVA_HOME,JRE_HOME,CLASSPATH and PATH](http://https://coderanch.com/t/600047/java/Difference-JAVA-HOME-JRE-HOME)
- [Java中设置classpath、path、JAVA_HOME的作用](http://http://www.cnblogs.com/echomyecho/p/3334617.html)
- [Why does starting spark-shell fail with NullPointerException on Windows?](http://stackoverflow.com/questions/32721647/why-does-starting-spark-shell-fail-with-nullpointerexception-on-windows)(关于如何解决启动spark-shell时遇到的NullPointerException问题)