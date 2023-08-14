# 自动化打包 Jenkins+Gitlab+Fastlane+蒲公英+钉钉

## **前言**

我们先介绍下下面用到的工具与基础名称：

  1、Jenkins：借用一句官方介绍 Jenkins是一个开源软件项目，是基于Java开发的一种持续集成工具，用于监控持续重复的工作，旨在提供一个开放易用的软件平台，使软件的持续集成变成可能。这句话我们能提炼出的重点就是 Java,相信大家电脑都有装Java环境。这个我们就不在累赘了。具体的Jenkins的安装方式我们下面再介绍。

  2、Fastlane：照例我们找官方介绍，它是用Ruby语言编写的一套自动化工具集和框架，每一个工具实际都对应一个Ruby脚本，用来执行某一个特定的任务，而Fastlane核心框架则允许使用者通过类似配置文件的形式，将不同的工具有机而灵活的结合在一起，从而形成一个个完整的自动化流程。这句话的重点就是Ruby语言，要是在编写修改脚本的过程中遇到什么问了（后面的确有一个问题把我困扰住了）我们可以至少查一下该怎么写。她的安装我们也是放下后面一起说。

  3、Gitlab 可能基本上公司内部的代码仓库都是在Gitlab上吧，当然可能也不是，反正这就是你代码的远程仓库，大家也都理解。

  4、蒲公英 + 钉钉 这个可能大家在用，也可能没用。具体的按你们的实际情况。当让蒲公英这个也是可以被替代的，甚至可以是自己的平台，通知到的也不一定非得是钉钉，也可能是微信或者手机短信等等，具体的按照实际需求去定去探索。

 5、Ruby，一种简单快捷的面向对象（面向对象程序设计）脚本语言

 6、RVM是一个命令行工具，它允许您轻松地安装，管理和使用从解释器到多组gems多个ruby环境。

 7、Gems RubyGems简称gems，是一个用于对 Ruby组件进行打包的 Ruby 打包系统。例如经常用的cocoapods就需要 gem 来管理。



## **前期准备**

- **Ruby:**

  fastlane的安装需要Ruby2.0版本以上，虽然mac自带ruby，但是版本可能较低，并且权限较少，所以推荐使用RVM管理ruby版本。

- **xcode命令行工具**

  ```shell
  xcode-select --install 
  ```

  如果已经安装会提示 ![img](/Users/linggongbang/Desktop/笔记/IT/自动化/assets/16d04de1208ffb7f~tplv-t2oaga2asx-zoom-in-crop-mark:4536:0:0:0.awebp)

  如果没有安装会出现

   ![xcode-select --install](/Users/linggongbang/Desktop/笔记/IT/自动化/assets/16d00cac5370c798~tplv-t2oaga2asx-zoom-in-crop-mark:4536:0:0:0.awebp)

   直接点击安装就可以了，安装完成后再次执行 `xcode-select --install` 之后出现已经安装的提示了。

- **Java JDK** （这个是Jenkins安装用的，如果不需要jenkins可直接忽略）

  
  可先查看 当前安装的java版本
  
  ```shell
  java -version
  ```
  
  如果未安装请先前往 [JDK下载链接](https://www.oracle.com/java/technologies/downloads/) 下载
  
  

## **安装**

### **一、Fastlane 安装**

[Fastlane](https://fastlane.tools/) 是一整套的客户端 CI 工具集合，替代开发者处理构建和发布 App 中繁琐的任务，可以非常快速简单的搭建一个自动化发布服务，并且支持Android，iOS，MacOS。Fastlane本身没有一套特殊语法，使用的 Ruby 语言。

**Fastlane 的能力**

- [为 Appstore 自动生成截图](https://docs.fastlane.tools/getting-started/ios/screenshots/)
- [轻松地将测试版分发给测试人员](https://docs.fastlane.tools/getting-started/ios/beta-deployment/)
- [快速地将新版本发布到应用商店](https://docs.fastlane.tools/getting-started/ios/appstore-deployment/)
- [对 App 进行代码签名，管理 App的证书、设备和描述文件](https://docs.fastlane.tools/codesigning/getting-started/)
- 为代码生成文档

参考官网文档：[ fastlane docs](https://docs.fastlane.tools/)

**注：安装之前确保你已经安装了最新版本的Xcode命令行工具：`xcode-select *--install*`**

#### **第一种方式：Homebrew**

```shell
brew install fastlane
```

#### **第二种方式：RubyGems**

```shell
sudo gem install fastlane
```

### **二、Jenkins 安装**

首先我采用的是Homebrew的安装方式，需要提前安装好Homebrew环境，或者也可以采用线面第二种方式安装

#### **第一种方式：Homebrew**  

安装之前执行命令检查自己的Homebrew环境：`brew doctor`

有问题就按检查中给的提示解决，注意，多仔细看看爆出的问题，根据问题去寻找答案。

参考官网：[macOS Installers for Jenkins LTS](https://www.jenkins.io/download/lts/macos/)  

👆🏻官网把它主要的一些使用命令也都告诉我们了，总结如下：

![image-20230801105258993](/Users/linggongbang/Desktop/笔记/IT/自动化/assets/image-20230801105258993.png)

以下是安装成功示例：

![image-20230801110737580](/Users/linggongbang/Desktop/笔记/IT/自动化/assets/image-20230801110737580.png)

#### **第二种方式  war文件方式**  

首先下载 .war文件，这个就在 [官网下载](https://www.jenkins.io/download/) 位置如下：

参考官网：[Download and run Jenkins](https://www.jenkins.io/doc/pipeline/tour/getting-started/)

![image-20230801112321453](/Users/linggongbang/Desktop/笔记/IT/自动化/assets/image-20230801112321453.png)

### **三、Jenkins 安装后设置向导**

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



## **项目配置**

上面已经介绍了如何安装相关软件，下面开始介绍如何通过Fastlane+Jenkins+Gitlab+蒲公英+钉钉进行自动化打包：

### **一、Fastlane 配置**

#### **Fastlane 初始化**

打开命令行工具`cd`到项目目录下，然后执行`fastlane init` 

```shell
cd 项目目录下（项目路径）

fastlane init

#请注意，如果您想在 App Store Connect 帐户上创建第一个应用程序，则需要使用环境变量设置开发者名称 ( company_name) ：PRODUCE_COMPANY_NAME
PRODUCE_COMPANY_NAME="你的公司名称" fastlane init
```

**注：** 若遇到`command not found: fastlane`错误请看**错误集锦**中的第二种错误

如下，这里选择4（自定义配置）之后回车三连击。2是TestFilght配置、3是App Store配置，我这里暂时用不上，所以不选，后续也可以自己加上。

```shell
linggongbang@bogon CI % fastlane init
[✔] 🚀
[✔] Looking for iOS and Android projects in current directory...
[15:14:33]: Created new folder './fastlane'.
[15:14:33]: Detected an iOS/macOS project in the current directory: 'CI.xcworkspace'
[15:14:33]: -----------------------------
[15:14:33]: --- Welcome to fastlane 🚀 ---
[15:14:33]: -----------------------------
[15:14:33]: fastlane can help you with all kinds of automation for your mobile app
[15:14:33]: We recommend automating one task first, and then gradually automating more over time
[15:14:33]: What would you like to use fastlane for?
# 为 App Store 生成本地化的 iOS 屏幕截图 
1. 📸  Automate screenshots
# 自动发布beta版本到testFlight
2. 👩‍✈️  Automate beta distribution to TestFlight
# 自动发布到App Store
3. 🚀  Automate App Store distribution
# 自定义手动设置
4. 🛠  Manual setup - manually setup your project to automate your tasks
?  4
[16:01:07]: ------------------------------------------------------------
[16:01:07]: --- Setting up fastlane so you can manually configure it ---
[16:01:07]: ------------------------------------------------------------
[16:01:07]: Installing dependencies for you...
[16:01:07]: $ bundle update
[16:03:33]: --------------------------------------------------------
[16:03:33]: --- ✅  Successfully generated fastlane configuration ---
[16:03:33]: --------------------------------------------------------
[16:03:33]: Generated Fastfile at path `./fastlane/Fastfile`
[16:03:33]: Generated Appfile at path `./fastlane/Appfile`
[16:03:33]: Gemfile and Gemfile.lock at path `Gemfile`
[16:03:33]: Please check the newly generated configuration files into git along with your project
[16:03:33]: This way everyone in your team can benefit from your fastlane setup
[16:03:33]: Continue by pressing Enter ⏎

[16:36:06]: fastlane will collect the number of errors for each action to detect integration issues
[16:36:06]: No sensitive/private information will be uploaded, more information: https://docs.fastlane.tools/#metrics
[16:36:06]: ----------------------
[16:36:06]: --- fastlane lanes ---
[16:36:06]: ----------------------
[16:36:06]: fastlane uses a `Fastfile` to store the automation configuration
[16:36:06]: Within that, you'll see different lanes.
[16:36:06]: Each is there to automate a different task, like screenshots, code signing, or pushing new releases
[16:36:06]: Continue by pressing Enter ⏎

[16:36:07]: --------------------------------------
[16:36:07]: --- How to customize your Fastfile ---
[16:36:07]: --------------------------------------
[16:36:07]: Use a text editor of your choice to open the newly created Fastfile and take a look
[16:36:07]: You can now edit the available lanes and actions to customize the setup to fit your needs
[16:36:07]: To get a list of all the available actions, open https://docs.fastlane.tools/actions
[16:36:07]: Continue by pressing Enter ⏎

[16:36:07]: ------------------------------
[16:36:07]: --- Where to go from here? ---
[16:36:07]: ------------------------------
[16:36:07]: 📸  Learn more about how to automatically generate localized App Store screenshots:
[16:36:07]: 		https://docs.fastlane.tools/getting-started/ios/screenshots/
[16:36:07]: 👩‍✈️  Learn more about distribution to beta testing services:
[16:36:07]: 		https://docs.fastlane.tools/getting-started/ios/beta-deployment/
[16:36:07]: 🚀  Learn more about how to automate the App Store release process:
[16:36:07]: 		https://docs.fastlane.tools/getting-started/ios/appstore-deployment/
[16:36:07]: 👩‍⚕️  Learn more about how to setup code signing with fastlane
[16:36:07]: 		https://docs.fastlane.tools/codesigning/getting-started/
[16:36:07]:
[16:36:07]: To try your new fastlane setup, just enter and run
[16:36:07]: $ fastlane custom_lane
```

当命令执行到 `bundle update`可能会卡住，需要打开项目目录下新增的文件`GemFile`，修改一下ruby源。保存后，继续在当前目录下执行`bundle update`即可。

```shell
#旧
#source "https://rubygems.org"
#新
source "https://gems.ruby-china.com"
```

若出现以上问题如果有条件的小伙伴可以翻墙重新运行`fastlane init` ，就不会出现卡主的情况

#### FastLane 配置文件说明

| 文件名                                                     | 描述                                                         |
| ---------------------------------------------------------- | ------------------------------------------------------------ |
| [Appfile](https://docs.fastlane.tools/advanced/Appfile/) | 从 Apple Developer Portal 获取的开发者账号相关信息           |
| [Fastfile](https://docs.fastlane.tools/advanced/Fastfile/)                                                   | 核心文件，用于命令行调用和处理具体的流程，lane相对于一个action方法或函数 |
| Gemfile                                                    | 类似于cocopods 的Podfile文件                                 |
| [Matchfile](https://docs.fastlane.tools/actions/match/#handle-multiple-apps-per-developerdistribution-certificate)                                                  | Match管理证书和描述文件的配置文件                            |
| .env                                                       | 配置环境变量（在fastlane init进行初始化后并不会自动生成，如果需要可以自己创建Deliverfile: deliver工具的配置文件，上传截图苹果和后台一些app信息  (默认不生成，需要sudo gem install deliver安装)然后在fastlane 目录下执行deliver init 即可，执行 deliver init 将会生成Deliverfile、screenshots、metadata文件） |
| Deliverfile                                                | deliver工具的配置文件,从 iTunes Connect 获取和项目相关的信息详细 |
| metadata                                                   | 同步iTC中的元数据                                            |
| screenshots                                                | 同步iTC中的截图                                              |

####  Fastlane[工具集](https://docs.fastlane.tools/actions/)

| 文件名                                                       | 描述                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [match](https://docs.fastlane.tools/actions/match/) | 证书和配置文件管理工具会重置证书，推荐新项目使用。🌟🌟🌟🌟🌟      |
| [cert](https://docs.fastlane.tools/actions/cert/) | 自动创建管理iOS代码签名证书,会去自动创建证书，永远不会撤销现有的证书。如不能创建会报错。 |
| [sigh](https://docs.fastlane.tools/actions/sigh/) | 用来创建、更新、下载、修复Provisioning Profile的工具         |
| [gym](https://docs.fastlane.tools/actions/gym/) | 自动化编译打包工具.shenzhen的代替品.🌟🌟🌟🌟🌟                    |
| [pem](https://docs.fastlane.tools/actions/pem/) | 自动生成、更新推送配置文件                                   |
| [produce](https://docs.fastlane.tools/actions/produce/) | 如果你的产品还没在iTunes Connect(iTC)或者Apple Developer Center(ADC)建立，produce可以自动帮你完成这些工作 |
| [deliver](https://docs.fastlane.tools/actions/deliver/) | 自动上传截图，APP的元数据，二进制(ipa)文件到iTunes Connect   |
| [snapshot](https://docs.fastlane.tools/actions/snapshot/) | 自动截图（基于Xcode7的UI test）                              |
| [frameit](https://docs.fastlane.tools/actions/frameit/) | 可以把截的图片自动套上一层外边框                             |
| [pilot](https://docs.fastlane.tools/actions/pilot/) | 管理TestFlight的测试用户，上传二进制文件                     |
| [boarding](https://docs.fastlane.tools/actions/boarding/) | 建立一个添加测试用户界面，发给测试者，可自行添加邮件地址，并同步到iTunes Connect(iTC) |
| [scan](https://docs.fastlane.tools/actions/scan/) | 自动运行测试工具，并且可以生成漂亮的HTML报告                 |
| [spaceship](https://docs.fastlane.tools/actions/spaceship/) | 为pilot，boarding和deliver等工具提供和 iTC 和 ADC 的交互API。spaceship本来是个独立的项目，后来被Fastlane收编进来 |
| [WatchBuild](https://docs.fastlane.tools/actions/WatchBuild/) | 是一个独立的iTC监控工具，开启WatchBuild可以监控iTC上的文件状态，弹出MacOS自带的Notification |
| [supply](https://docs.fastlane.tools/actions/supply/) | Android自动上传到Google Play工具(如果有时间，我想把国内提供API的Android Store都写个插件自动上传，这个问题从10年我刚开始工作就觉得是个痛点) |
| [screengrab](https://docs.fastlane.tools/actions/screengrab/) | Android的自动截图工具                                        |



#### FastLane 脚本编写

##### Appfile文件配置

`Appfile`中包含App Store Connect 和 Apple Developer Portal 相关信息，以便更快地部署您的通道并根据您的项目需求进行定制。

`Appfile`必须位于您的项目的`./fastlane`目录内。

执行`fastlane init`后`Appfile`文件默认配置如下：

```shell
# [[APP_IDENTIFIER]] 替换为项目 Bundle Identifier，若有多个 Bundle Identifier 请用逗号隔开
#app_identifier("[[APP_IDENTIFIER]]") # The bundle identifier of your app
# [[APPLE_ID]] 替换为可以打包的开发者账号
#apple_id("[[APPLE_ID]]") # Your Apple Developer Portal username

# For more information about the Appfile, see:
#     https://docs.fastlane.tools/advanced/#appfile

```

只需要把默认配置下的配置内容替换为自己开发者账号与项目信息就可以了。以下是我的文件配置

```shell
# The bundle identifier of your app (项目 Bundle Identifier)
# 若有多个 Bundle Identifier 请用逗号隔开
app_identifier("com.**.**") 

# Your Apple Developer Portal username (可打包的开发者账号)
apple_id("*******@qq.com") 

# For more information about the Appfile, see:
#     https://docs.fastlane.tools/advanced/#appfile
```

##### Fastfile文件配置



## **错误集锦：**

### **一、 brew services start jenkins-lts 启动Jenkins如遇到下面错误   执行`brew update` **

```python
Error: uninitialized constant Homebrew::Service::System
/opt/homebrew/Library/Homebrew/macos_version.rb:153:in `const_missing'
/opt/homebrew/Library/Taps/homebrew/homebrew-services/cmd/services.rb:61:in `services'
/opt/homebrew/Library/Homebrew/brew.rb:94:in `<main>'
```

**[[Brew\]brew update命令：Warning: No remote 'origin' in /opt/homebrew/Library/Taps/homebrew/homebrew-services, skipping update!]**

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

### **二、执行`fastlane init` 遇到`command not found: fastlane`错误 **

```shell
#原因一：
没有安装Fastlane,检查是否安装成功Fastlane, 若没有安装则执行`brew install fastlane`安装
#原因二：
没有安装Xcode命令行工具，执行`xcode-select --install`命令验证是否安装Xcode命令行工具、
#原因三：
没有配置环境变量，分别打开`~/.profile`, `~/.zshrc` ，`~/.bashrc`配置文件分别添加以下环境变量中的一种：
export PATH="$HOME/.fastlane/bin:$PATH" 
export PATH="$HOME/.fastlane/bin/fastlane_lib:$PATH"
```

检查完之后，再次执行`fastlane init` 不出意外的情况下会顺利通过

