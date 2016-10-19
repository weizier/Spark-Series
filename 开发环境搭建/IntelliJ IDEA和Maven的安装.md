IntelliJ IDEA安装及配置
　　首先在https://www.jetbrains.com/idea/?fromMenu#chooseYourEdition 这里选择community版本，这个版本是免费提供的，并且对我们的Spark使用来说，用这个版本已经足够了。如下图所示：

　　直接点击黑色的“DOWNLOAD”按钮会默认开始下载Windows版本的IntelliJ IDEA，如果需要其他平台的可以点击旁边的“.EXE”进行选择即可。
　　下载完成后，双击exe文件，进行安装，其中所有选项按照默认的即可，然后运行IntelliJ IDEA，这个时候也有一些配置需要选择，全部按照默认的即可，直到来到下面的界面，这里对IntelliJ IDEA做一些全局配置。一般来说，在IntelliJ IDEA中，默认的代码字体大小比较偏小一些，所以可以配置一下字体的大小，在欢迎界面有一个“Configure”选项，点击后选择“Settings”，顺序是：Configure - Settings - Editor - Color&Fonts - Font，来到字体设置的界面。
　　
　　如下图所示，首先要将当前的模版保存一下，直接点击“Save As”即可，然后这个时候就可以调整字体大小了，我一般将默认的12调整为20。这个可以按照自己的习惯进行设置。
　　
　　
　　然后是最重要的，下载所需要的Scala插件，在欢迎界面的“Configure”选项下选择“Plugins”，然后在插件安装的界面点击“Install JetBrains plugins”，如果能够正常连接上网络的话，这个时候应该会显示一系列可以安装的插件，如果因为在公司的内网，无法安装插件的话，需要按照下图所示的方法进行代理设置（另附公司的代理设置指引）：
　　
　　
　　代理设置成功后，应该会显示出下图中的插件安装界面，选中Scala，然后在右边对话框里选择安装。
　　
　　如果没法通过在线的方式安装scala的插件，也可以去官网上下载好插件的zip格式文件，注意要下载到与IntelliJ IDEA版本对应的Scala插件，我这里是2016.2.1版本，所以选择下图标识的Scala插件版本。
　　
　　然后在“Plugins”界面，选择“Install plugin from disk”选项，从弹出的对话框中选择刚下载的zip格式文件进行安装即可，安装完后要重启IntelliJ IDEA。如下图所示：
　　
　　
　　创建maven工程
　　Maven是一个用于项目构建和管理的工具，可以利用它来便捷的管理项目的生命周期，最大特点是当一个项目使用了某一些jar包时，可以使用maven来集中管理这些jar包，比如，本地项目使用了某个jar包，现在需要在其他地方使用这个项目，那么便可以在maven的pom.xml文件中加入这个jar包的依赖，一般来说，在pom.xml.文件中的各种包的依赖关系，都需要有一个远程的中央仓库，这个中央仓库里包含了各种jar包，在各个项目中只需要在pom.xml进行一些简单的配置，即可使用这些jar包，从而避免开发人员去分别下载这些jar包并进行配置的烦恼，另外，也方便了团队合作时各种jar包版本统一配置的问题。
　　基于这些优势，在这里主要使用maven进行项目管理。
　　首先，在欢迎界面点击“Create New Project”，然后在左边对话框中选择“Maven”，表示将创建一个maven工程，右边对话框中，选择JDK的安装路径，将“Create from archetype”，然后再选择下边如图所示，并进入下一步。
　　
　　进入下一步后，有三个字段需要填写。其中，GroupId用来标识这个工程所属的项目群组，比如一个公司的某个大项目，例如org.apache.hadoop和org.apache.spark等等，“ArtifactId”用来标示这个工程，比GroupId的范围要小一些，例如hadoop-yarn-common与spark-core-2.10等等，而“Version”顾名思义就是版本号了。
　　
　　
　　配置好自己工程的这三个名字后，进入到下一个页面，如下所示：
　　
　　这里有两个重要的概念，首先是setting.xml文件，一般默认会在C:\Users\用户名\.m2路径下，但是这里由于是刚安装，所以还没有这个文件（需要在本工程创建完成并生成.m2目录后，使用公司内网的settings.xml文件），这个文件的主要功能是配置中央仓库，从而pom.xml文件中添加的依赖，可以从这个中央仓库中下载得到。
　　第二个便是本地仓库的概念，即上图中的“Local repository”，这里在刚安装的时候，也是没有的。本地仓库中存储所有maven工程曾经从中央仓库或者远程仓库中下载得到的jar包文件，为什么要有本地仓库的存在？这主要是为了避免频繁从中央仓库和远程仓库中下载重复的jar包文件。
　　一般来说，在pom.xml中添加某个jar包的依赖后，maven会自动依顺序从下列三个地方寻找这个jar包：
　　首先从本地仓库中寻找，即上面提到的“Local repository”，一般默认在C:\Users\用户名\.m2路径下；
　　然后从中央仓库中寻找，这里的中央仓库包括两部分，一部分是maven默认的The Central Repository，另一部分是在settings.xml中指定的中央仓库，这个一般是公司内网所使用的中央仓库，比如http://maven.oa.com/。
　　如果pom.xml中在<repository></repository>中指定仓库的话，最后一步会从这里寻找。
如果上述三个方式都没有找到这个jar包的话，程序会报错。
  
接着，下一步命名工程名称，这里命名为和artifactId同名，然后是设置工程的路径。由于是新创建，所以并没有这个路径名，因此会弹出下面这个对话框，直接点击OK即可。


    工程创建成功后，可以看到工程根目录下的pom.xml文件中有上述配置过的groupId, artifactId和version等信息，这些信息都是用来唯一确定本工程并区别于其他工程的字段。
　　虽然此时pom.xml中还没有任何依赖，但是maven工程本身是有一些依赖的，正常情况下，本工程刚创建的时候，就会在.m2目录下生成一个repository文件夹，用来存放历次maven下载的jar包。这里因为在公司内网进行开发，所以主要使用公司内网的maven中央仓库，首先将IntelliJ IDEA关闭，然后需要做两件事：
　　将C:\Users\用户名\.m2路径下的repository文件夹删除；
　　将包含了内网中央仓库和服务器等配置信息的settings.xml文件放在C:\Users\用户名\.m2路径下（如果已经存在，则替换之）

　　为了更好的适应公司内网的开发环境，最好pom.xml文件也使用一个统一的模板（模板里已经包含了一些最为常用的spark开发jar包），然后再在这个模板上添加本工程特定的jar包依赖关系。
　　另外，如果此时在左侧的工程层级关系对话框中，没有源程序的目录（即上图中的src，main，scala这些目录），那么在工程名上（即firstMavenProject）上点击右键，选择New - Directory可以创建一个src文件夹，然后在src文件夹上右键同样可以创建main和scala文件夹，最后在创建的scala文件夹上邮件选择“Mark Directory as”，然后选择“Source Root”，这个时候应该可以观察到scala文件夹颜色变为蓝色。
　　将scala文件夹标记为源程序的根目录后，如果在scala的右键菜单的“New”选项中没有找到“Scala Class”选项，则表明scala的SDK还未能够正确的添加到本工程中，添加方法是：File - Project Structure - Global Libraries，然后如下图所示，点击绿色的“+”符号，选择系统中安装的scala SDK，点击确认即可。
　　

添加SDK后，再去scala右键菜单的“New”选项中，便可发现可以创建一个Scala Class了，点击它便可以根据逐步引导创建一个scala的object，class或trait.