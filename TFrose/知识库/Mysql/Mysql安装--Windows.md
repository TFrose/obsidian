##  一. 安装之前需要注意的几点

-   建议不要安装最新版本，一般找mysql5.0系列版本即可；
-   mysq1官网有.zip和.msi两种安装形式；
-   zip是压缩包，直接解压缩以后使用的，需要自己配置各种东西；msi是安装包，系统直接帮我们安装搞定；
-   新手建议使用msi安装方式；

## 二. Mysql下载地址

[https://dev.mysql.com/downloads/windows/installer](https://link.zhihu.com/?target=https%3A//dev.mysql.com/downloads/windows/installer)

![](https://pic4.zhimg.com/v2-f6080ab6d03039e990da89004d5cbbe3_r.jpg)

##  三. 安装步骤
 **1）双击下面这个程序。**

![](https://pic1.zhimg.com/80/v2-9329589f8dfd3b7bd04d70be18e838fc_720w.png)

**2）出现如下这个界面后，勾选"I accept the license terms"，点击"Next"。**

![](https://pic1.zhimg.com/v2-e90b34d9c35c818a79a87f9bb4d4478c_r.jpg)

**3）出现如下这个界面后，选择"Custom"，，点击"Next"。**

![](https://pic2.zhimg.com/v2-6490c1fb4964cda56b88835a082bf731_r.jpg)

**4）出现如下界面后，我们进行如下的操作。**

![](https://pic2.zhimg.com/v2-ac08ad709afa91da3d1534fadafa3d89_r.jpg)

**5）同时在这个界面中，还可以查看"MySQL Server 5.7.21-X64"默认安装路径。**

注：这里的第5步操作，你一定要按照我这里说的，操作一遍。

**第一步：先选中"MySQL Server 5.7.21-X64"。**

![](https://pic3.zhimg.com/80/v2-39c7fab7373b58121545b9f7f3fb827e_720w.png)

**第二步：点击右下角"Acvanced Options"。**

![](https://pic2.zhimg.com/80/v2-fdbda1442d3bb9b945dab4162ae6a08d_720w.png)

**第三步：此时，会出现如下界面。**

![](https://pic4.zhimg.com/v2-ca07b8951abebf4f59c56fea924dddf3_r.jpg)

**注意如下：**

![](https://pic1.zhimg.com/v2-c1b811644df2e1609bd00c5c6dd90af8_r.jpg)

**6）出现如下界面后，证明可以了，点击"Execute"。**

![](https://pic4.zhimg.com/v2-3bea1ebd6b40ca893e878b97c7e6898f_r.jpg)

**7）当出现如下界面后，点击"Next"。**

![](https://pic3.zhimg.com/v2-5f67f3d9ce671491159f7cc76e4c9bf6_r.jpg)

**8）当出现如下界面后，点击"Next"。**

![](https://pic2.zhimg.com/v2-dfa1ee8dc861d3653262b16fafd56899_r.jpg)

**9）当出现如下界面后，勾选红黄色方框中内容，点击"Next"。**

![](https://pic1.zhimg.com/v2-273b3b72c4ad3925268fce70e6212aac_r.jpg)

**10）当出现如下界面后，使用界面默认内容即可，点击"Next"。**

![](https://pic3.zhimg.com/v2-eae2ea588e15eb77b76ed441664d14be_r.jpg)

**11）当出现如下界面后，设置好密码后，点击"Next"。**

![](https://pic3.zhimg.com/v2-49ddb3f25eb927fa449d661456d96b66_r.jpg)

**12）当出现如下界面后，进行如下设置后，点击"Next"。**

![](https://pic3.zhimg.com/v2-3975b7704307703b785777b167b707fe_r.jpg)

**13）当出现如下界面后，直接点击"Next"。**

![](https://pic4.zhimg.com/v2-ba192820b056d5db3baea3b6e0eaa4ab_r.jpg)

**14）当出现如下界面后，直接点击"Next"。**

![](https://pic2.zhimg.com/v2-f6adcdecdf630457471166e40e38fe45_r.jpg)

**15）当出现如下界面后，直接点击"Execute"。**

![](https://pic2.zhimg.com/v2-dd8c02999bcfa17ee3a02ad59b8988a1_r.jpg)

**16）当出现如下界面后，直接点击"Finish"。**

![](https://pic1.zhimg.com/v2-bfd9e24cc3e081b4da716150ff2e7410_r.jpg)

**17）当出现如下界面后，直接点击"Next"。**

![](https://pic4.zhimg.com/v2-af480ce6570dfe16424981b8a4c6e63b_r.jpg)

**18）当出现如下界面后，直接点击"Finish"。**

![](https://pic1.zhimg.com/v2-b82a6c3a7ea8f86612694450f2760090_r.jpg)

**19）配置环境变量**

在上述第5步的时候，我们知道了数据库管理系统(Mysql Server)是安装在如下目录中：

![](https://pic2.zhimg.com/80/v2-687cff4e210a1e401548c7fde2c7cb3d_720w.jpg)

我们找到mysql server的安装目录：C\Program Files\MySQL\MySQL Server 5.7，并进入bin目录，里面会有很多“二进制可执行文件”。

![](https://pic1.zhimg.com/v2-ac12b9103e65add2f2d641b9fbaf92ac_r.jpg)
## 四. 环境变量配置
-   利用mysql.exe可执行文件，就能实现对mysql的接，但是你不能在这里直接双击，即使你双击，也只是出现一个“闪屏”。mysql.exe可执行文件，只能在CMD黑窗口中运行。在CMD黑窗口中，其实你配置不配置环境变量，都可以执行这个可执行文件。当你不配置环境变量，就只能切换到mysql.exe所在的目录，才能执行mysql的启动命令；当你配置了环境变量，只要是你打开了CMD窗口，你在任何一个路径下就可以执行mysql的启动命令。
-   当没有配置环境变量；

![](https://pic2.zhimg.com/v2-d56ca0069ea6cd5a496aaf273aa29f3d_r.jpg)
-   配置环境变量；打开我的电脑->属性->高级->环境变量，在系统变量里选择PATH。
-   只需要添加如下两处内容即可：

![](https://pic4.zhimg.com/v2-68fa535c9839c7a5618b44954f75c4d7_r.jpg)

**①** **为什么需要配置环境变量？**
-   环境变量，代表系统的一个全局搜索路径。
-   当你没有配置环境变量的时候，你想要执行某个目录下的某个程序，就必须找到它的具体位置，才能够执行它。你仔细想一下，假如你在其它的文件路径下，想要执行另外一个目录下的某个程序，你觉得可以吗？
-   当不配置环境变量，想要执行某个程序可以吗？当然也是可以的，就拿启动mysql来说，你如果不配置环境变量，就必须在CMD黑窗口中，使用cd命令切换到mysql server下的bin目录下，才可以执行启动。你每次这样启动是不是觉得很麻烦，当你需要经常使用mysql，需要经常执行mysql启动。这就是为什么我们需要配置环境变量的原因。
-   当配置了某个环境变量，如果你想要执行某个程序，你可以在任何路径下，执行这个称序。首先，系统会在当前目录下，搜索是否存在想要执行的某个程序，假如没有，系统会再去系统环境变量中的目录进行一个个搜索，当搜索到了该程序，便会立即执行。

## 五. 重要安装目录讲解

在上述第5步的时候，我们知道了数据库管理系统是安装在如下目录中：

![](https://pic2.zhimg.com/80/v2-687cff4e210a1e401548c7fde2c7cb3d_720w.jpg)

**1）进入该路径下：C:\ProgramData\MySQL\MySQL Server 5.7。**

这里面有一个重要的目录和一个重要的配置文件，需要我们注意：

![](https://pic1.zhimg.com/v2-5feb5463fed280b0be798fccb29bc994_r.jpg)

对于配置文件my.ini的详细说明，这里不介绍，可以参考如下网址：[https://blog.csdn.net/hanwuqia0370/article/details/85680775](https://link.zhihu.com/?target=https%3A//blog.csdn.net/hanwuqia0370/article/details/85680775)对于这个data目录，先看看里面有什么：

![](https://pic4.zhimg.com/v2-36906c578795c30aa919dc90babb4e3f_r.jpg)

从上图中可以看到：

![](https://pic4.zhimg.com/v2-eb1c9decf1b69bdec98c90145a077807_r.jpg)

系统默认的数据库：

![](https://pic2.zhimg.com/80/v2-a6ccf91ca42784762af84ad51d07dc25_720w.png)

**2）安装mysql后，注意区分如下几个目录的作用。**

![](https://pic1.zhimg.com/v2-e12008921171f57d346661164d1017bc_r.jpg)

上述各个目录的具体安装位置，都是在安装mysql步骤的第4、5步进行了详细说明：

![](https://pic4.zhimg.com/v2-7744a75f8cccf369774547cca97be3ff_r.jpg)

**怎么查看MYSQL服务是否在Windows启动？**

**1）在左下角输入框(或win7中使用Win + R可以打开搜索框)中，输入"services.msc"。**

![](https://pic1.zhimg.com/v2-c628264ea282b25e818243bb86aa44cc_r.jpg)

**2)当启动了MySQL后，会在这里出现一个MYSQL服务进程，可以检查MYSQL是否启动。**

![](https://pic3.zhimg.com/v2-3102fa9f0b3365c56de5ad6813e41136_r.jpg)
