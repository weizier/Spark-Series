

# 一. IntelliJ IDEA安装及配置


## 1.1 IntelliJ IDEA下载及安装


　　首先在 [CHOOSE YOUR EDITION](https://www.jetbrains.com/idea/?fromMenu#chooseYourEdition) 这里选择`Community`版本，这个版本是免费提供的，对我们的Spark使用来说，用这个版本已经足够了。如下图所示：

![](http://i.imgur.com/4KKdcHX.png)


　　直接点击黑色的 **`DOWNLOAD`** 按钮会默认开始下载Windows版本的`IntelliJ IDEA`，如果需要其他平台的版本，可以点击旁边的 **`.EXE`** ，然后在打开的下拉菜单中，选择相应平台即可。

　　下载完成后，双击得到的`.exe`文件（我这里主要以Windows平台为例，下载得到的文件为`ideaIC-2016.2.1.exe`），开始进行安装，其中所有选项按照默认的即可（其中有一个安装路径的配置，按照普通软件安装的方法自行设置即可，当然使用默认的路径也可以，**记住这里的安装路径，后面要用到**），一路点击`Next`，最后点击`Finish`按钮结束安装过程。

默认情况下，`IntelliJ IDEA`并不会在桌面上创建快捷键，我们可以去它的安装目录下的`bin`文件夹中，找到它的可执行`.exe`文件，我这里的`bin`文件夹路径是`C:\Program Files (x86)\JetBrains\IntelliJ IDEA Community Edition 2016.2.1\bin`，在该目录下，你可以找到两个如下的文件：
```java
idea.exe//对应32位机器
idea64.exe//对应64位机器
```
根据自己电脑是32位还是64位的，进行相应版本的选择，如果怕麻烦，建议在该文件上点击右键，然后选择`发送到` --> `桌面快捷方式`选项，这样以后在启动的时候，直接在桌面上双击快捷方式即可（如果是细心的读者，其实可以发现，在IDEA安装过程中，其中有一个步骤就是问：需不需要在桌面上创建快捷方式，默认下是不会创建的）。

选择好32位还是64位的文件后，然后双击运行IntelliJ IDEA，一般来说首次运行，都会碰到如下页面：

![](http://i.imgur.com/Yr3YpA0.png)

因为IntelliJ IDEA本身都会有一些配置文件，所以这里在询问是否需要导入一个配置文件，这里选择图中标示的选项即可，并点击`OK`。然后来到如下所示的UI主题选择界面，大多数使用IntelliJ IDEA的开发人员，一般都会毫无例外的选用第二个UI，这种灰黑色的主题简洁大方，给人一种深邃的质感，也确实是很多人选择IntelliJ IDEA的一个重要原因之一，用很多人的话说，写代码都能写出“高潮”来，是否属实，你们试试就知道了。

![](http://i.imgur.com/CJb49lr.png)

## 1.2 Scala插件的安装

后续的几个页面按照默认的配置即可，一直`Next`来到下面的界面。因为我们主要用Scala来写Spark程序，而IntelliJ IDEA需要使用Scala插件来支持Scala，安装方法如下图所示，首先点击`Configure`，然后点击下拉菜单中的`Plugins`。

![](http://i.imgur.com/lbAsLty.png)

随后打开的页面会显示出IntelliJ IDEA当前已安装的插件列表，现在我们要安装Scala插件，所以点击页面左下方的`Install JetBrains plugin...`按钮，然后来到安装插件的页面，如果网络正常的话，在页面左上方的搜索框内搜索"scala"，即可出现Scala插件的安装界面，点击右侧页面中的`Install`进行安装后，可以看到安装的进度条，如下图所示：

![](http://i.imgur.com/JI470lx.png)

但是如果你在公司内网，这个时候你可能需要配置代理，步骤如下图所示，在图中的`Host name`和`Port number`中填写公司自己的代理即可，如果需要，在下方的账号和密码框中按情况填写上相应信息。填写完毕，记得先检查一下是否能够正确连上外部网络，可以点击图中的`Check connection`，输入一个外网的地址，比如`http://www.baidu.com/`，测试一下代理是否正确配置了。一切正常后，点击`OK`退出即可。然后按照上一步中不需要配置代理的情况下，进行Scala插件的安装。

![](http://i.imgur.com/aBdZES6.png)

**注意：插件安装完了之后，记得重启一下IntelliJ IDEA使得插件能够生效。**


## 1.3 全局JDK和Library的设置


因为Scala代码的编写需要依赖JDK，并且以后编写Spark的程序，肯定会用到各种外部Jar包，如果自己手动去下载这些Jar包然后再引入项目，不仅费时费力，而且尤其在多人协作开发一个项目的时候，各种Jar包版本的管理将会变得非常混乱，因此，在这里建议：从一开始就习惯来用Maven对项目依赖到的Jar包进行理（后面会讲到Maven），然而在创建Maven工程的时候，首先便需要指定JDK。

因此为了后续创建Spark项目（正如上面所说，一方面是Scala本身需要依赖JDK，另一方面用来管理项目构建的Maven，其创建也需要依赖JDK）的时候不用每次都去配置JDK，这里先进行一次全局配置。首先在欢迎界面点击`Configure`，然后在`Project Defaults`的下拉菜单中选择`Project Structure`，如下图所示：

![](http://i.imgur.com/ZPEnfo4.png)

然后在打开的`Default Project Structure`界面的左侧边栏选择`Project`，在右侧打开的页面中创建一个新的JDK选项（一定要本机已经安装过JDK了），如下图所示步骤在下拉菜单中点击`JDK`后，在打开的对话框中选择你所安装JDK的位置，注意是JDK安装的根目录，不是bin文件夹的目录，如果你对上一篇文章中讲到的`JAVA_HOME`还很有印象的话，这里的目录就是`JAVA_HOME`中设置的目录。

![](http://i.imgur.com/wQyn1z9.png)

这一步的全局`Project JDK`设置完毕后，回到欢迎页面。

除了要依赖JDK之外，Scala的编写肯定也离开不了自身的SDK（全称为Software Development Kit，即软件开发工具包。实际上，JDK就是Java的SDK），我们在IntelliJ IDEA编写Scala的程序的时候，比如要用到Scala自身提供的某个类，比如`Seq`（暂时不知道不要紧，后续文章会讲到），那IntelliJ IDEA到哪里去找这个`Seq`呢？只能去Scala自身提供的SDK里面去找，因此各种程序语言的软件开发者，是离不开这些语言的SDK的，Scala也自然不例外。而为了避免每次创建一个Scala工程的时候，都要去设置一遍Scala的SDK，这里做一些全局配置，主要是将Scala SDK引入到项目的Library中，并将其当做默认配置。

首先，在欢迎页面的右下角点击`Configure`，然后在`Project Defaults`的下拉菜单中选择`Project Structure`，在打开的页面左侧选择`Global Libraries`，然后在中间一栏中有一个绿色的加号标志 **`+`**，点击后在下拉菜单中选择 `Scala SDK`（如果没有的话，回顾上面的步骤，仔细观察一下是不是有哪些步骤错了，比如Scala的插件没安装成功，本机还未安装Scala，亦或者Scala的bin文件夹路径未能添加到系统的 **PATH** 环境变量中去等等），然后在打开的对话框中选择系统本身所安装的Scala（即System对应的版本），点击`OK`确定，这时候会在中间一栏位置处出现Scala的SDK，在其上右键点击后选择`Copy to Project Libraries...`，这个操作是为了将Scala SDK添加到项目的默认Library中去。整个流程如下面的动图所示。


![](http://i.imgur.com/Nv0Vhjq.gif)


# 二. 创建一个Maven工程

## 2.1 创建Maven工程
上面的安装和配置都完成后，现在可以开始创建一个Maven工程了。

在欢迎界面点击`Create New Project`，在打开的页面左侧边栏中，选择`Maven`，然后在右侧的`Project SDK`一项中，查看是否是正确的JDK配置项（如果每一步严格按照上文中的步骤操作的话，正常来说这一栏会自动填充的，因为我们之前在1.3中已经配置过了全局的Project JDK了，如果这里没有正常显示JDK的话，可以点击右侧的`New...`按钮，然后指定JDK安装路径的根目录即可），然后点击`Next`，来到Maven项目最重要三个参数的设置页面，这三个参数分别为：`GroupId`, `ArtifactId`和`Version`.

为了更好的解释这三个字段，用Spark 1.6.2的核心组件的Maven标识符为例来进行讲解。

```xml
    <groupId>org.apache.spark</groupId>
    <artifactId>spark-core_2.11</artifactId>
    <version>1.6.2</version>
```


- GroupId，可以理解为用来标志你整个项目组的，或者你这些代码属于某一个完整的项目，比如上面的`org.apache.spark`就可以非常好的来标志Apache的Spark这个项目了。一般来说可以使用倒序的公司网址来作为GroupId，这可以类比为，沿袭了Java项目中使用倒序公司网址来作为Package名称的一个惯例。
- ArtifactId，一般是用来在整个项目组来标志本项目的，相比`GroupId`的范围，其概念要稍微小一些，比如`spark-core_2.11`就非常好的表示出了本项目主要是关于Spark的核心基础组件的，从而能够与Spark其他各种组件或架构很好的区分开来。
- Version，正如字面意思，就是本项目的迭代版本的信息，如上面的`1.6.2`.

现在，比如你的公司名称叫做`abc`，然后你的项目组叫做`test`，那就可以使用`com.abc.test`来作为`GroupId`，然后将`ArtifactId`取做`myFirstProject`，版本号就使用它默认的就好了（当然，如果你的项目以后有迭代更新版本的话，这个是需要按照实际情况进行改动的）。这三个字段设置完毕后，点击`Next`，来到项目名称设置页面，一般可以和`ArtifactId`字段保持一致，当然也可以不一致，这个只是为了给本项目取个名字而已。

整个流程如下面的Gif动图所示。


![](http://i.imgur.com/nMWyDDj.gif)


## 2.2 属于你的"Hello World!"

在上一步中，我们已经创建了一个Maven工程，不出意外的话，这个时候会打开这个项目，并且首先映入眼帘的将是项目的 `pom.xml` 文件（暂时不清楚的不要紧，后面会讲到），细心如你，一定可以惊奇的发现 `pom` 文件中居然有我们刚才设置的 `GroupId`, `ArtifactId` 和 `Version` 这些信息（如下），这些信息相当于就给了本项目一个唯一的标识符，有了这个标识符，别人将会在浩如烟海的Maven仓库中，一眼识别到你（本段话有装B嫌疑，不懂的话请暂时忽略）。

```xml
    <groupId>com.abc.test</groupId>
    <artifactId>myFirstProject</artifactId>
    <version>1.0-SNAPSHOT</version>
```

好，现在开始要真正在这个Maven项目中创建一个属于自己的Scala程序了，在开干之前，为了给Scala营造一个顺利的环境，有几件事需要先做。下面我将分点罗列如下：

- 首先，为了让你的首次体验Scala更清爽一些，将一些暂时无关的文件和文件夹都勇敢的删除掉吧，主要有 `main\java`, `main\resources` 和 `test` 这三个；
- 将Scala的框架添加到这个项目中，方法是在左侧栏中的项目名称上右键菜单中点击`Add Framework Support...`，然后在打开的对话框左侧边栏中，勾选`Scala`前面的复选框，然后点击确定即可（前提是上文中所述步骤都已正确走通，否则你很有可能看不到Scala这个选项的）；
- 在main文件夹中建立一个名为 `scala` 的文件夹，并右键点击 `scala` 文件夹，选择 `Make Directory as`，然后选择`Sources Root` ，这里主要意思是将 `scala` 文件夹标记为一个源文件的根目录，然后在其内的所有代码中的 `package` ，其路径就从这个根目录下开始算起。举个例子，假如你在 `scala` 文件夹中建立了一个程序，这个程序的 `package` 属性为 `com.abc.test`，那么这个程序就一定要保存在 `scala\com\abc\test` 目录下，否则项目就找不到这个程序了；
- 在已经标记好为源文件根目录的  `scala` 文件夹 上，右键选择 `New`，然后选择 `Scala Class`，随后设置好程序的名称，并且记得将其设置为一个 `Object`(类似于Java中含有静态成员的静态类)，正常的话，将会打开这个 `Object` 代码界面，并且可以看到IntelliJ IDEA自动添加了一些最基本的信息；
- 在创建的 `Object` 中输入如下语句：
```Scala
def main(args: Array[String]):Unit = {
  println("Hello World!")
}
```
- 在程序界面的任意位置，右键单击后选择 `Run '你的程序名称'`，静待程序的编译和运行，然后在下方自动打开的窗口中，你就可以看到振奋人心的 `Hello World!`了。

整个流程的Gif动图已经做好，双手奉上。

![](http://i.imgur.com/3gxInru.gif)


## 三. 小结


至此，整个的IntelliJ IDEA安装与配置，以及基本的Maven工程创建流程，就全然结束了，写的比较啰嗦，一个很简单的IDE使用问题，嚼了这么多口舌，不过啰嗦之外，若果真对各位好学的你们，有稍稍的竟然之外的益处，那也就不枉我这么苦逼的制作这些Gif动图了。

此外，本文只介绍了一些最基本的内容，关于IntelliJ IDEA和Maven的更为细致的内容，以及关于如何在本地写一个Spark程序都还没有提到，不着急，后续我会慢慢更新。

Tips:
> 若上文中有些Gif图看不太清，可以在这些图上点击右键，并选择"在新标签页中打开图片"（在Chrome中，是这个选项，可能不同浏览器中的说法不一样，不过相信一定难不到你），然后将这个图片在新的浏览器窗口打开后，就会变大一些，从而看的也更清楚一些了。


# 参考
1. [https://github.com/judasn/IntelliJ-IDEA-Tutorial](https://github.com/judasn/IntelliJ-IDEA-Tutorial)（非常好的IntelliJ IDEA教程）