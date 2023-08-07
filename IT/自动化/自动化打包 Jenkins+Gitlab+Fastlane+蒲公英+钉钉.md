# 自动化打包 Jenkins+Gitlab+Fastlane+蒲公英+钉钉

## **前言**

我们先介绍下下面用到的工具：

  1、Jenkins：借用一句官方介绍 Jenkins是一个开源软件项目，是基于Java开发的一种持续集成工具，用于监控持续重复的工作，旨在提供一个开放易用的软件平台，使软件的持续集成变成可能。这句话我们能提炼出的重点就是 Java,相信大家电脑都有装Java环境。这个我们就不在累赘了。具体的Jenkins的安装方式我们下面再介绍。

  2、Fastlane：照例我们找官方介绍，它是用Ruby语言编写的一套自动化工具集和框架，每一个工具实际都对应一个Ruby脚本，用来执行某一个特定的任务，而Fastlane核心框架则允许使用者通过类似配置文件的形式，将不同的工具有机而灵活的结合在一起，从而形成一个个完整的自动化流程。这句话的重点就是Ruby语言，要是在编写修改脚本的过程中遇到什么问了（后面的确有一个问题把我困扰住了）我们可以至少查一下该怎么写。她的安装我们也是放下后面一起说。

  3、Gitlab 可能基本上公司内部的代码仓库都是在Gitlab上吧，当然可能也不是，反正这就是你代码的远程仓库，大家也都理解。

  4、蒲公英 + 钉钉 这个可能大家在用，也可能没用。具体的按你们的实际情况。当让蒲公英这个也是可以被替代的，甚至可以是自己的平台，通知到的也不一定非得是钉钉，也可能是微信或者手机短信等等，具体的按照实际需求去定去探索。

## **前期准备**

- **Ruby:**

  fastlane的安装需要Ruby2.0版本以上，虽然mac自带ruby，但是版本可能较低，并且权限较少，所以推荐使用RVM管理ruby版本。

- **xcode命令行工具**

  ```lua
  xcode-select --install 
  ```

  如果已经安装会提示 ![img](/Users/linggongbang/Desktop/笔记/IT/自动化/assets/16d04de1208ffb7f~tplv-t2oaga2asx-zoom-in-crop-mark:4536:0:0:0.awebp)

  如果没有安装会出现

   ![xcode-select --install](/Users/linggongbang/Desktop/笔记/IT/自动化/assets/16d00cac5370c798~tplv-t2oaga2asx-zoom-in-crop-mark:4536:0:0:0.awebp)

   直接点击安装就可以了，安装完成后再次执行 `xcode-select --install` 之后出现已经安装的提示了。

- **Java JDK** （这个是Jenkins安装用的，如果不需要jenkins可直接忽略）

  
  可先查看 当前安装的java版本
  
  ```shell
  shell
  复制代码java -version
  ```
  
  如果未安装请先前往 [JDK下载链接](https://www.oracle.com/java/technologies/downloads/) 下载

## **安装**

### 一、Fastlane 安装

参考官网：[ fastlane docs](https://docs.fastlane.tools/)

#### 第一种方式：Homebrew

```lua
brew install fastlane --cask
```

#### 第二种方式：RubyGems

```shell
sudo gem install fastlane
```



### 二、Jenkins 安装

首先我采用的是Homebrew的安装方式，需要提前安装好Homebrew环境，或者也可以采用线面第二种方式安装

#### 第一种方式：Homebrew  

安装之前执行命令检查自己的Homebrew环境：`brew doctor`

有问题就按检查中给的提示解决，注意，多仔细看看爆出的问题，根据问题去寻找答案。

参考官网：[macOS Installers for Jenkins LTS](https://www.jenkins.io/download/lts/macos/)  

👆🏻官网把它主要的一些使用命令也都告诉我们了，总结如下：

![image-20230801105258993](/Users/linggongbang/Desktop/笔记/IT/自动化/assets/image-20230801105258993.png)

以下是安装成功示例：

![image-20230801110737580](/Users/linggongbang/Desktop/笔记/IT/自动化/assets/image-20230801110737580.png)

#### 第二种方式  war文件方式  

首先下载 .war文件，这个就在 [官网下载](https://www.jenkins.io/download/) 位置如下：

参考官网：[Download and run Jenkins](https://www.jenkins.io/doc/pipeline/tour/getting-started/)

![image-20230801112321453](/Users/linggongbang/Desktop/笔记/IT/自动化/assets/image-20230801112321453.png)

### 三、Jenkins 安装后设置向导

使用以上方式安装、启动Jenkins后设置向导开始

当您首次访问新的Jenkins实例时，系统会要求您使用自动生成的密码来解锁它。

1. 浏览到`http://localhost:8080`（或您在安装Jenkins时为Jenkins配置的任何端口），并等待出现**Unlock Jenkins**页面。

   ![Unlock Jenkins](/Users/linggongbang/Desktop/笔记/IT/自动化/assets/setup-jenkins-01-unlock-jenkins-page.jpg)

2. 从Jenkins控制台日志输出中，复制自动生成的字母数字密码（在2组星号之间）。

   ![Password](/Users/linggongbang/Desktop/笔记/IT/自动化/assets/setup-jenkins-02-copying-initial-admin-password.png)

  **笔记：**

   - 命令：`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`将在控制台打印密码。
   - 如果您使用官方`jenkins/jenkins`映像在Docker中运行Jenkins，您可以使用`sudo docker exec ${CONTAINER_ID or CONTAINER_NAME} cat /var/jenkins_home/secrets/initialAdminPassword`在控制台中打印密码，而无需执行进入容器。
   - Jenkins控制台日志指示了也可以获得此密码的位置（在Jenkins主目录中）。必须在新Jenkins安装的设置向导中输入此密码，然后才能访问Jenkins的主用户界面。如果您碰巧跳过设置向导中的后续用户创建步骤，此密码也可以作为默认管理员帐户的密码（用户名“admin”）。

3. 在**解锁Jenkins**页面上，将此密码粘贴到**管理员密码**字段中，然后单击**继续**。

4. [解锁Jenkins](https://www.jenkins.io/doc/book/installing/macos/#unlocking-jenkins)后，会出现**自定义Jenkins**页面。在这里，您可以安装任意数量的有用插件，作为初始设置的一部分。

   单击显示的两个选项之一：

   - **安装建议的插件**-安装推荐的插件集，这些插件基于最常见的用例。
   - **选择要安装的插件**-选择要最初安装的插件集。当您首次访问插件选择页面时，默认情况下会选择建议的插件。
   - 如果您不确定您需要什么插件，请选择**安装建议的插件**。您可以在稍后通过Jenkins中的[**管理Jenkins**](https://www.jenkins.io/doc/book/managing)>[**插件**](https://www.jenkins.io/doc/book/managing/plugins/)页面安装（或删除）其他Jenkins插件。

设置向导显示正在配置的Jenkins的进度以及您选择的Jenkins插件集正在安装。这个过程可能需要几分钟。

## **配置**



## 错误集锦：

### 一、 brew services start jenkins-lts 启动Jenkins如遇到下面错误   执行`brew update` 

```python
Error: uninitialized constant Homebrew::Service::System
/opt/homebrew/Library/Homebrew/macos_version.rb:153:in `const_missing'
/opt/homebrew/Library/Taps/homebrew/homebrew-services/cmd/services.rb:61:in `services'
/opt/homebrew/Library/Homebrew/brew.rb:94:in `<main>'
```

#### [[Brew\]brew update命令：Warning: No remote 'origin' in /opt/homebrew/Library/Taps/homebrew/homebrew-services, skipping update!]

最近在使用brew update的时候，遇到了：

```python
 ****** Second, We should find the update. [brew update] ****** 
fatal: not in a git directory
Warning: No remote 'origin' in /opt/homebrew/Library/Taps/homebrew/homebrew-services, skipping update!
Already up-to-date.
```

很受启发的是这条comment：

![1324794-20230122220040133-1301400066](/Users/linggongbang/Desktop/笔记/IT/自动化/assets/1324794-20230122220040133-1301400066.png)在homebrew-core目录下，执行了git remote -v:

```python
mokin.li@MoKinLiMacBook-Pro homebrew-core % git remote -v
origin	https://github.com/Homebrew/homebrew-core (fetch)
origin	https://github.com/Homebrew/homebrew-core (push)
```

然后去homebrew-services目录下执行：

```python
mokin.li@MoKinLiMacBook-Pro homebrew % cd homebrew-services 
mokin.li@MoKinLiMacBook-Pro homebrew-services % git remote -v       
fatal: detected dubious ownership in repository at '/opt/homebrew/Library/Taps/homebrew/homebrew-services'
To add an exception for this directory, call:
 
	git config --global --add safe.directory /opt/homebrew/Library/Taps/homebrew/homebrew-services
mokin.li@MoKinLiMacBook-Pro homebrew-services % git config --global --add safe.directory /opt/homebrew/Library/Taps/homebrew/homebrew-services
 
mokin.li@MoKinLiMacBook-Pro homebrew-services % git remote -v
origin	https://gitee.com/cunkai/homebrew-services.git (fetch)
origin	https://gitee.com/cunkai/homebrew-services.git (push)
```

通过这种方式成功解决了问题：

```python
mokin.li@MoKinLiMacBook-Pro ~ % ./BrewToolsDaily.sh                   
 ****** First, We require brew version. [brew -v] ****** 
Homebrew 3.6.20
Homebrew/homebrew-core (git revision 69deebcfe1d; last commit 2023-01-22)
Homebrew/homebrew-cask (git revision 201da9195e; last commit 2023-01-22)
 
 
 ****** Second, We should find the update. [brew update] ****** 
Already up-to-date.
 ****** Third, We should find the package update. [brew upgrade] ****** 
```
