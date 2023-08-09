## 一、Charles是什么？ 

![img](https:////upload-images.jianshu.io/upload_images/2327528-080aa170abbd95ca.png?imageMogr2/auto-orient/strip|imageView2/2/w/475)

Charles是在 Mac或Windows下常用的http协议网络包截取工具，是一款屌的不行的抓包工具，在平常的测试与调式过程中，掌握此工具就基本可以不用其他抓包工具了。

## 二、为什么是Charles？ 

为什么要用抓包工具？大家在平常移动App调试测试中是如何进行抓包的？

在我们做开发与测试的过程中，总免不了碰到网络问题，特别是重后台的产品，这个时候我们往往的处理方法是抓个网络包，看看到底应用发送和接收了些什么鬼.....这个时候Charles上场了；Charles是一款屌的不行的截包工具，好用到没朋友。

**那么Charles屌在哪里呢？？？主要特点如下：**

1.支持SSL代理，可以截取分析SSL的请求

2.支持流量控制。可以模拟慢速网络(2G,3G)，以及等待时间较长的请求。

3.支持AJAX调试。可以自动把JSON或者XML数据格式化，方便查看。

4.支持重发网络请求，方便后端调试。

5.支持修改网络请求参数。

6.支持网络请求的截取和动态修改。

7.最重要的一个优点就是有不同平台的版本（Mac，Windows、Linux）即学一个打遍天下。

## 三、Charles基本工作原理 

charles是通过网络代理来进行抓包的，下面先了解一下http代理的原理：

*1.普通http请求过程*

![img](https:////upload-images.jianshu.io/upload_images/2327528-48722d8553b99de0.png?imageMogr2/auto-orient/strip|imageView2/2/w/406)

•一般情况下的HTTP请求与响应：

**2.加入了Charles的HTTP代理的请求与响应过程\*
*

**
**

![img](https:////upload-images.jianshu.io/upload_images/2327528-a5310b3abce9f59b.png?imageMogr2/auto-orient/strip|imageView2/2/w/436)

中间的代理服务器就是Charles

## 四、Charles的下载与安装过程 

1.官网下载地址：

> [http](https://link.jianshu.com/?t=http://www.charlesproxy.com/download/)[://www.charlesproxy.com/download](https://link.jianshu.com/?t=http://www.charlesproxy.com/download/)[/](https://link.jianshu.com/?t=http://www.charlesproxy.com/download/)

2.Mac下安装：

是一个安装包是一个dmg后缀的文件。打开后将Charles拖到Application目录下即完成安装。



![img](https:////upload-images.jianshu.io/upload_images/2327528-329dc3623e212342.png?imageMogr2/auto-orient/strip|imageView2/2/w/345)

在Mac下你打开Launchpad即可看到一个像花瓶一样的Charles程序图标

3.Windows下安装：

下载后直接双击根据安装向导一步一步安装即可

## 五、Http抓包操作步骤 

> Step 1：开启Charleshttp代理；

> Step 2：手机端Wifi添加代理；

> Step 3：开启Charles录制功能；

> Step 4：启动应用开始抓包；

> Step 5：分析抓取的数据包。

#### Step 1: 开启Charleshttp代理

  a.设置Charles代理

![img](https:////upload-images.jianshu.io/upload_images/2327528-91a2016d1ca23038.png?imageMogr2/auto-orient/strip|imageView2/2/w/472)

第一次启动默认会开启本机的系统代理，因为我们只是监控移动端的所以将此选去除（去掉选项前面的小钩）

a.激活http代理功能

![img](https:////upload-images.jianshu.io/upload_images/2327528-faa0da5558647eaf.png?imageMogr2/auto-orient/strip|imageView2/2/w/583)

#### Step 2: 手机端Wifi添加代理 

#### a. Android手机：

1.在手机端打开你的Wifi设置然后长按已经连接的Wifi在弹出来的菜单中选择【修改网络】

2.沟上[显示高级]选项--【手动】

3.输入代理服务器的IP与端口，IP即安装了Charles的电脑IP地址，端口就是前面一步设置Charles时所设置的端口。

![img](https:////upload-images.jianshu.io/upload_images/2327528-bad5ad9b7bb0d4f3.png?imageMogr2/auto-orient/strip|imageView2/2/w/365)

注意：手机所连接Wifi要与电脑在同一个LAN(局域网)。

#### b. iOS手机： 

1.点击你所连接的wifi

2.输入代理服务器的IP与端口，

IP即安装了Charles的电脑IP地址，端口就是前面一步设置Charles时所设置的端口。

![img](https:////upload-images.jianshu.io/upload_images/2327528-1608f589c4a06f7f.png?imageMogr2/auto-orient/strip|imageView2/2/w/399)

注意：手机所连接Wifi要与电脑在同一个LAN(局域网)。

#### Step 3:开启Charles录制功能 



![img](https:////upload-images.jianshu.io/upload_images/2327528-fb506210dc91714b.png?imageMogr2/auto-orient/strip|imageView2/2/w/410)

1.当手机连接上代理后Charles会弹出相应的提示框，点击Allow即可。2.点击工具栏上的开始录制按钮，即启动了Charles的抓包功能了。

#### Step 4：启动应用开始抓包 

![img](https:////upload-images.jianshu.io/upload_images/2327528-e1f4be53e6619542.png?imageMogr2/auto-orient/strip|imageView2/2/w/549)

1.在手机上操作相应的App进行抓包。2.在Charles的主界面上就可看到相应的请求内容。

#### Step 5：分析抓取的数据包 



![img](https:////upload-images.jianshu.io/upload_images/2327528-5bcafc5573125e31.png?imageMogr2/auto-orient/strip|imageView2/2/w/507)

1.Charles 主要提供两种查看封包的视图，分别名为 “Structure”和 “Sequence”：

  a.Structure 视图将网络请求按访问的域名分类；

  b.Sequence 视图将网络请求按访问的时间排序。

2.大家可以根据具体的需要在这两种视图之前来回切换。请求多了有些时候会看不过来，Charles提供了一个简单的Filter功能，可以输入关键字来快速筛选出URL 中带指定关键字的网络请求。

3.对于某一个具体的网络请求，你可以查看其详细的请求内容和响应内容。如果请求内容是POST 的表单，Charles 会自动帮你将表单进行分项显示。如果响应内容是 JSON 格式的，那么 Charles可以自动帮你将JSON 内容格式化，方便你查看。如果响应内容是图片，那么 Charles可以显示出图片的预览。

#### 六、Https抓包操作步骤

> Step 1：了解一下https的基本原理；

> Step 2：在手机端安装SSL证书；

> Step 3：激活Charles的SSL代理；

> Step 4：将指定的URL请求开启SSL代理功能

> Step 5：其他步骤与Http抓包相同，请参考[四、Http抓包操作步骤](https://link.jianshu.com/?t=http://四、Http抓包操作步骤)

#### Step 1：了解一下https的基本原理； 



![img](https:////upload-images.jianshu.io/upload_images/2327528-846818e091a616cb.png?imageMogr2/auto-orient/strip|imageView2/2/w/691)

HTTPS其实是有两部分组成：HTTP+ SSL / TLS，也就是在HTTP上又加了一层处理加密信息的模块。服务端和客户端的信息传输都会通过TLS进行加密，所以传输的数据都是加密后的数据。具体是如何进行加密，解密，验证的，且看图,下面这个图的解说

详细说明，请参考：

> [http://blog.csdn.net/clh604/article/details/22179907](https://link.jianshu.com/?t=http://blog.csdn.net/clh604/article/details/22179907)

#### Step 2：在手机端安装SSL证书 

​    1.将证书文件从Charles导出

​    2.然后通过adb或者其他工具将其复制到手机的SD卡中。

![img](https:////upload-images.jianshu.io/upload_images/2327528-e047ba31fd769693.png?imageMogr2/auto-orient/strip|imageView2/2/w/577)

从Charles导出证书文件

   3.将证书文件导入Android手机



![img](https:////upload-images.jianshu.io/upload_images/2327528-adb197fcbcc3afec.png?imageMogr2/auto-orient/strip|imageView2/2/w/433)

在手机的设置界面找到【安全】---》【从内部存储设备或SD卡安装】----》选择SD卡上的证书---》弹出设置证书名对话框，输入一个易记的名字，然后根据提示进行导入即呵。

4.将证书文件导入iOS手机

![img](https:////upload-images.jianshu.io/upload_images/2327528-4b46ecae7426f95c.png?imageMogr2/auto-orient/strip|imageView2/2/w/430)

1.在iPhone手机上打开Safari浏览器，然后在地址栏中输入www.charlesproxy.com/getssl。2.稍后会弹出安装描述文件提示，点击右上角的【安装】按钮进行证书安装即可。

#### Step 3：激活Charles的SSL代理 



![img](https:////upload-images.jianshu.io/upload_images/2327528-d69cf0feddcb0445.png?imageMogr2/auto-orient/strip|imageView2/2/w/583)

1.选择【Proxy】--->【SSL Proxying Settings..】设置。2.在弹出来的对话框中沟选【Enable SSL Proxying】。

#### Step 4：将指定的URL请求开启SSL代理功能 



![img](https:////upload-images.jianshu.io/upload_images/2327528-6e13cb8fe12d52de.png?imageMogr2/auto-orient/strip|imageView2/2/w/630)

1.选择抓取的https链接，然后右键选择【Enable SSL Proxying】。2.如果不激活SSL代理，所以https请求都是乱码无法查看。



![img](https:////upload-images.jianshu.io/upload_images/2327528-33571c901fea867d.png?imageMogr2/auto-orient/strip|imageView2/2/w/566)

再次请求这个Https时，其请求内容已经一目了然了。

#### 七、Charles进阶---修改请求也响应的内容 

> Step 1：设置Charless断点。

> Step 2：对指定的URL开启断点功能。

> Step 3：编辑请求与响应的内容。

#### Step 1：设置Charless断点 



![img](https:////upload-images.jianshu.io/upload_images/2327528-3c9b94f84ddbf1db.png?imageMogr2/auto-orient/strip|imageView2/2/w/587)

选择【Breakpoint Settings…】--->勾选【Enable Breakpoints】来激活断点功能

#### Step 2：对指定的URL开启断点功能。 

![img](https:////upload-images.jianshu.io/upload_images/2327528-318cafd35ac2069b.png?imageMogr2/auto-orient/strip|imageView2/2/w/348)

1.选择一个URL链接-à右键开启菜单---》选择【Breakpoints】即可开启此请求的断点。2.这样Charles会遇到此请求时会弹出中断对话框。

#### Step 3：编辑请求与响应的内容。 

a.编辑请求内容

![img](https:////upload-images.jianshu.io/upload_images/2327528-9a5bf8fa59dbc0a1.png?imageMogr2/auto-orient/strip|imageView2/2/w/645)

在中断对话框中，用户可以点击Edit Request来编辑请求的内容，编辑完成后然后点击【Execute】发出去这个请求给服务端

b.编辑服务器响应的内容

![img](https:////upload-images.jianshu.io/upload_images/2327528-6877db31db07dd36.png?imageMogr2/auto-orient/strip|imageView2/2/w/628)

在【Edit Request】对话中点击【Execute】发出请求后，服务端返回来数据后，用户点击【Edit Response】可对响应内容进行编辑完成后然后点击【Execute】发出去这个数据给客户端。

#### 八、Charles进阶---弱网模拟 

1.菜单中选择【Proxy】--->【Throttle Settings..】-à激活【Enable Throttling】。

2.在Throttle Configuration设置弱网的参数。

3.以下是各种网制式的速率参考文档：

[移动网络制式与网速的参考文档](https://link.jianshu.com/?t=http://wenku.baidu.com/link?url=buoPWkwmfW3B216gtRzIBbLZST3EEqxnAHNEabaVu2tXlGlkCMUl_E4tor_408BRG4eRSd4p5VQd_k4xiq14VXvJIrrfZq7l9CJhU8ht7Nq)



![img](https:////upload-images.jianshu.io/upload_images/2327528-4e0677e8f9207856.png?imageMogr2/auto-orient/strip|imageView2/2/w/510)

弱网模拟设置