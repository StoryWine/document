# 前言

Mac M1系列安装JDK与多JDK版本管理的教程，包含手动安装与Homebrew安装、手动配置JAVA_HOME环境、Jenv多版本控制JDK版本

[TOC]

## JVM、JRE 与 JDK

JVM 是 JavaVirtualMachine（Java虚拟机）的缩写，是 java 程序跨平台运行的基础。JVM 可以理解为 java 程序运行的容器，这样程序不需要直接和内核交互，达到跨平台的目的。
JRE 是 Java Runtime Environment（Java 运行时环境）的缩写，单纯的 JVM 并不能运行 java 程序，因为程序编写时会引用很多类库，而 JVM 并没有提供这些库文件。运行 java 程序所需要的类库、容器的合集，即为 JRE。
JRE 可以保证已编译 java 程序的运行，不过我们开发程序时，为了方便我们编译、调试，官方提供了相应的语言开发工具包（Java Development Kit），即 JDK。
所以：
JDK = JRE + 开发工具集（如 javac 编译工具）
JRE = JVM + Java SE 类库

> ## 资源站网址
>
> 1. https://www.java.com/zh-CN/
> 2. https://www.azul.com/downloads/?package=jdk#zulu
> 3. https://www.oracle.com/java/technologies/downloads/

## 安装JAVA环境

使用安装包安装 JDK 时，安装路径一般为 `/Library/Java/JavaVirtualMachines`，这也是 mac OS JDK 的默认路径
使用 HomeBrew 安装 JDK 时，会安装在 `/opt/homebrew` 目录下，如果其他程序需要使用 HomeBrew 安装的 JDK，可以通过软连接映射到 `/Library/Java/JavaVirtualMachines` 目录下。

- ### 普通手动方式

  1. #### 通过官网地址下载 

     JAVA 8 下载地址`https://www.java.com/zh-CN/`

     注意：这里的JAVA8没有arm架构的版本，只有x86_64的版本，在mac m1/m2 的机型上无法安装，如果需要jdk8，可以在azul中安装：[Azul Downloads](https://link.zhihu.com/?target=https%3A//www.azul.com/downloads-new/%3Fversion%3Djava-8-lts%26package%3Djdk%23zulu)

     JDK 8 以上下载地址 `https://www.oracle.com/cn/java/technologies/downloads/`

     下载JDK包，建议下载.dmg

     

  2. 安装JDK包

     点击继续，接下来安装，输入本机密码，安装成功

     ![image-20230506152315607](/Users/linggongbang/Desktop/笔记/assets/image-20230506152315607.png)

     ###### 检查安装是否成功

     查看是否安装成功，可以通过查看JDK版本来确定

     打开终端，输入以下命令

     ```shell
     java -version
     ```

     若输出的非安装的版本则在终端输入以下命令，查看本机安装的全部JDK版本是否有上面安装的版本

     ```shell
     /usr/libexec/java_home -V
     ```

  3. #### 安装目录

     使用安装包安装 JDK 时，安装路径一般为 `/Library/Java/JavaVirtualMachines`，这也是 mac OS JDK 的默认路径。

     如果未找到安装 JDK，可以在终端输入以下命令查看路径：

     ```shell
     /usr/libexec/java_home -V
     ```

     如下图标红区域则是安装JDK路径：

     ![image-20230506153930334](/Users/linggongbang/Desktop/笔记/assets/image-20230506153930334.png)

     可以通过软连接映射到 `/Library/Java/JavaVirtualMachines` 目录下。

     ```shell
     sudo ln -sfn /opt/homebrew/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk
     ```

     

- ### Homebrew安装

  1. #### 通过Homebrew查找openjdk版本

     ```shell
     brew search openjdk
     ```

     返回结果显示

     ![image-20230504145027991](/Users/linggongbang/Desktop/笔记/assets/image-20230504145027991.png)

     根据需要安装相应版本

     注意：这里的openjdk@8没有arm架构的版本，只有x86_64的版本，在mac m1/m2 的机型上无法安装，如果需要jdk8，可以在azul中安装：[Azul Downloads](https://link.zhihu.com/?target=https%3A//www.azul.com/downloads-new/%3Fversion%3Djava-8-lts%26package%3Djdk%23zulu)

     以下M1/M2安装openjdk@8的错误信息：

     ![image-20230504145314530](/Users/linggongbang/Desktop/笔记/assets/image-20230504145314530.png)

     

  2. #### 安装对应版本的openjdk

     在Mac M1/M2 的机型上无法安装，如果需要jdk8，可以在azul中安装：建议下载.dmg，这个是安装包，可以省掉手动配置环境的工作。

     通过[Azul Downloads](https://link.zhihu.com/?target=https%3A//www.azul.com/downloads-new/%3Fversion%3Djava-8-lts%26package%3Djdk%23zulu)安装JAVA8，以下是安装过程

     1. 下载JDK包，建议下载.dmg

        <img src="/Users/linggongbang/Desktop/笔记/assets/image-20230504162649589.png" alt="image-20230504162649589" style="zoom:50%;" />

     2. 安装JAVA8

     <img src="/Users/linggongbang/Desktop/笔记/assets/image-20230504163112676.png" alt="image-20230504163112676" style="zoom: 50%;" />

     

     3. 通过Homebrew安装指定版本的命令

        ```shell
         brew install openjdk@xxx
        ```

          以下是安装openjdk（最新版本）的过程

        ![1683186396016](/Users/linggongbang/Desktop/笔记/assets/1683186396016.jpg)

        ![1683186452865](/Users/linggongbang/Desktop/笔记/assets/1683186452865.jpg)

        ![image-20230504145928759](/Users/linggongbang/Desktop/笔记/assets/image-20230504145928759.png)

        ###### 检查安装是否成功

        查看是否安装成功，可以通过查看JDK版本来确定

        打开终端，输入以下命令

        ```shell
        java -version
        ```

  

  3. #### 安装目录

     使用 HomeBrew 安装 JDK 时，会安装在 `/opt/homebrew` 目录下，如果其他程序需要使用 HomeBrew 安装的 JDK，可以通过软连接映射到 `/Library/Java/JavaVirtualMachines` 目录下。

     ```shell
     sudo ln -sfn /opt/homebrew/opt/openjdk/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk.jdk
     ```


## JAVA_HOME 环境变量

不同程序依赖的 JDK 版本不同，为了保持兼容，我们可能会在环境中安装多个版本的 JDK。
上面提到，java 程序需要 JRE 才能运行，而存在多个 JDK 时，就需要一种可以定位到特定 JDK 的方法。一般程序中会通过 JAVA_HOME 环境变量来定位相应的 JDK/JRE，该变量可以理解为一个指向 JAVA 环境的指针。

我们可以在`~/.zshrc` 或者 `~/.bash_profile` 中设置 JAVA_HOME，为了便于切换，我们给每个 JDK 单独定义了变量,修改后调用`source ~/.zshrc`或`source ~/.bash_profile`使配置文件生效

1. 可以通过 `export JAVA_HOME=$JAVA_X_HOME` 在不同版本 JDK 间切换。

   ```shell
   #java enviorment 路径中的X代表JDK文件名
   #配置JDK路径
   export JAVA_X_HOME="/Library/Java/JavaVirtualMachines/X.jdk/Contents/Home"
   #设置默认JDK版本
   export JAVA_HOME=$JAVA_X_HOME
   ```

2. 可以通过 `alias` 方式（使用命令javaX）快速在不同版本 JDK 间切换。

   ```shell
   #java enviorment 路径中的X代表JDK文件名
   #配置JDK路径
   export JAVA_X_HOME="/Library/Java/JavaVirtualMachines/X.jdk/Contents/Home"
   #配置alias 动态切换版本
   alias javaX='export JAVA_HOME=$JAVA_X_HOME'、
   #设置默认JDK版本
   export JAVA_HOME=$JAVA_X_HOME
   ```

3. /usr/libexec/java_home 程序

   os x 10.5 之后，mac 内置了 java_home 程序来管理 java 环境，`/usr/libexec/java_home -V` 可以查看默认路径下所有的 java 环境版本。
   同时，java_home 会使用当前环境中最新版作为默认版本，也可使用 `/usr/libexec/java_home -- v` 查看默认环境版本。

   未设置 JAVA_HOME 时，java 命令使用 java_home 默认版本，及路径下最新版本

   设置 JAVA_HOME 或 JAVA_HOME 不是有效 JVM 路径时，java 命令以 $JAVA_HOME 设置的路径版本为准。

   上面我们通过固定路径来设置 JAVA_HOME 环境变量，当路径变化时（如升级时卸载了老版本）。会造成 JAVA_HOME 不是有效 JVM 路径，影响部分程序运行。
    java_home 支持通过 `-v` 来筛选版本，目标版本不存在时，则返回路径下最新版本。
    所以，最好的方式通过 java_home 来设置 JAVA_HOME 变量，最大限度保证 JAVA_HOME 可用。

   可以通过`/usr/libexec/java_home`程序快速在不同版本 JDK 间切换

   ```shell
   #java enviorment 路径中的X代表JDK版本号
   #配置JDK路径
   export JAVA_8_HOME=$(/usr/libexec/java_home -v 1.8.0_372)
   #配置alias 动态切换版本
   alias java8='export JAVA_HOME=$JAVA_8_HOME'
   #设置默认JDK版本
   export JAVA_HOME=$JAVA_8_HOME
   ```

4. `~/.zshrc` 或者 `~/.bash_profile` 中设置 JAVA_HOME的环境变量，在`~/.zshrc` 或者 `~/.bash_profile`添加以下命令

   ```shell
   unset JAVA_HOME
   ```

## 安装jenv管理多个JDK版本

Jenv地址`https://www.jenv.be/`

查看本地默认环境JDK版本路径命令

```shell
echo $JAVA_HOME
```

1. 使用Homebrew安装`jenv`

   ```shell
   brew install jenv
   ```

   可能会遇到的问题，错误信息如下 在下载到最后时会出现下面的错误 这时是未下载成功的

   ```
   ==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sh
   ######################################################################## 100.0%
   fatal: not in a git directory
   Error: Command failed with exit 128: git
   ————————————————
   ```

   ![在这里插入图片描述](https://img-blog.csdnimg.cn/619cf03b8dbb4c9caf7a2b86e86a6347.jpeg#pic_center)

   输入下面两行命令解决上面的错误：

   ```shell
   git config --global --add safe.directory /opt/homebrew/Library/Taps/homebrew/homebrew-core
   git config --global --add safe.directory /opt/homebrew/Library/Taps/homebrew/homebrew-cask
   ```

2. 配置环境

   查看Shell配置环境命令

   ```
   echo $0
   ```

   本地环境变量包含两种`.bash_profile`和`.zshrc`，本地环境环境默认是`.zshrc`

   方式一 ： .zshrc

   ```shell
   echo 'export PATH="$HOME/.jenv/bin:$PATH"' >> ~/.zshrc
   echo 'eval "$(jenv init -)"' >> ~/.zshrc
   # 刷新配置文件，使其生效
   source ~/.zshrc
   ```

   方式二 ：.bash_profile

   ```shell
   echo 'export PATH="$HOME/.jenv/bin:$PATH"' >> ~/.bash_profile
   echo 'eval "$(jenv init -)"' >> ~/.bash_profile
   # 刷新配置文件，使其生效
   source ~/.bash_profile
   ```

3. 验证Jenv是否配置成功（检查命令）输入以下命令

   ```shell
   jenv doctor
   ```

   若出现以下问题，请根据以下步骤排查：

   1. $JAVA_HOME环境变量问题

      问题分析：错误信息中描述了由于已经设置了$JAVA_HOME环境变量，所以无法再通过jenv来设置$JAVA_HOME环境变量，通俗解释就是 jenv无法拿到设置$JAVA_HOME环境变量的控制权，拿不到控制权就无法切换版本

      ![image-20230506164159442](/Users/linggongbang/Desktop/笔记/assets/image-20230506164159442.png)

      解决方式如下：

       到配置文件中将设置的$JAVA_HOME变量注释掉，在 `/.zshrc` 或`.bash_profile`文件中配置的释掉或删除即可

      ```shell
      
      # Add RVM to PATH for scripting. Make sure this is the last PATH variable change.
      export PATH="$PATH:$HOME/.rvm/bin"
      export PATH="$HOME/.jenv/bin:$PATH"
      eval "$(jenv init -)"
      
      #########################################################################
      ## Java环境
      ##清除 JAVA_HOME 环境变量
      #unset JAVA_HOME
      
      #export JAVA_8_HOME=$(/usr/libexec/java_home -v 1.8.0_372)
      #alias java8='export JAVA_HOME=$JAVA_8_HOME'
      
      #export JAVA_20_HOME=$(/usr/libexec/java_home -v 20)
      #alias java20='export JAVA_HOME=$JAVA_20_HOME'
      
      #export JAVA_HOME=$JAVA_8_HOME
      #########################################################################
      ```

      注释完成后执行以下命令

      ```shell
      # 刷新配置文件，使其生效
      source ~/.zshrc
      或者
      source ~/.bash_profile
      ```

   2. 若注释或删除$JAVA_HOME环境变量后依然出现上图的问题，可能是jenv上没有JDK版本,通过`jenv add`命令添加JDK版本

      ```
      jenv add /Library/Java/JavaVirtualMachines/openjdk.jdk/Contents/Home
      ```

      出现以下提示则成功

      ![image-20230506173015070](/Users/linggongbang/Desktop/笔记/assets/image-20230506173015070.png)

4. 查找已安装的JDK目录

   ```shell
   /usr/libexec/java_home -V
   ```

   ```shell
   linggongbang@bogon ~ % /usr/libexec/java_home -V
   Matching Java Virtual Machines (3):
       20 (arm64) "Homebrew" - "OpenJDK 20" /opt/homebrew/Cellar/openjdk/20/libexec/openjdk.jdk/Contents/Home
       17.0.7 (arm64) "Oracle Corporation" - "Java SE 17.0.7" /Library/Java/JavaVirtualMachines/jdk-17.jdk/Contents/Home
       1.8.0_372 (arm64) "Azul Systems, Inc." - "Zulu 8.70.0.23" /Library/Java/JavaVirtualMachines/zulu-8.jdk/Contents/Home
   /opt/homebrew/Cellar/openjdk/20/libexec/openjdk.jdk/Contents/Home
   ```

5. 向Jenv添加JDK版本

   通过`jenv add`命令就可以把需要管理的JDK添加到jenv

   ```shell
   jenv add /Library/Java/JavaVirtualMachines/openjdk.jdk/Contents/Home
   jenv add /Library/Java/JavaVirtualMachines/jdk-17.jdk/Contents/Home
   jenv add /Library/Java/JavaVirtualMachines/zulu-8.jdk/Contents/Home
   ```

6.  删除添加到 jenv 的 JDK 版本

   添加新版本时，每个版本都会一次性自动加入多个不同版本，有些就是简称而已，其实都指向同一个版本，这里便于区分，可以将简略版本删除

   ```
   jenv remove xx(版本号)
   ```

7. Jenv 常用命令

   ```shell
   # 查看Jenv管理的JDK版本
   jenv versions
   # 查看当前JDK路径
   jenv which java
   # 配置全局JDK版本
   $ jenv global xx(版本号)
   # 配置本地版本（每个目录）
   $ jenv local xx(版本号)
   # 配置shell实例版本
   $ jenv shell xx(版本号)
   ```

8. 配置别名`alias`实现快速切换

   我们可以在`~/.zshrc` 或者 `~/.bash_profile` 中设置 `alias`，为了便于切换，我们给每个 JDK 单独定义了变量,修改后调用`source ~/.zshrc`或`source ~/.bash_profile`使配置文件生效

   ```
   alias jdk8='jenv global zulu64-1.8.0.372'
   alias jdk17='jenv global 20'
   alias jdk18='jenv global 17.0.7'
   ```

   

## 小提示

```
.bash_profile 中修改的环境变量只针对当前登录用户的配置，修改完.bash_profile之后记得在终端输入source ~/.bash_profile使之生效。
.zshrc 开机加载的环境变量在电脑每次自启时都会生效（永久有效），修改完之后在终端输入source ~/.zshrc使之生效。
```

```tex
使用命令 where java 查找 JAVA 位置
使用命令 java -version 查看 JAVA 版本号
使用命令 /usr/libexec/java_home -V 查看默认路径下所有的 java 环境版本
使用命令 /usr/libexec/java_home -- v 查看默认环境版本
使用命令 echo $JAVA_HOME 查看默认环境版本路径
```



## 卸载JAVA环境

```shell
sudo rm -fr /Library/Internet\ Plug-Ins/JavaAppletPlugin.plugin 
sudo rm -fr /Library/PreferencePanes/JavaControlPanel.prefPane 
sudo rm -fr ~/Library/Application\ Support/Oracle/Java
sudo rm -rf /Library/Java
```

