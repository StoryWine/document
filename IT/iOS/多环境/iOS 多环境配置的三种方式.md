# iOS 多环境配置的三种方式

### 概念：
 Project：包含项目所有代码、资源文件、所有信息。
 Target：对指定代码和资源文件的具体构建方式。
 Scheme：对指定的Target的环境配置。

### 一、使用多targets配置环境

创建新的Target，我将使用一个事例项目引导学者们一步步探讨整个过程（通用Objective-C、Swift）

1.首先新建一个项目取名MultipleEnvironments，可以看到只有一个TARGETS，我们把这个target作为公开版本。

![image-20230823110205887](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/image-20230823110205887.png)

2.配置测试版本和预发布版本。

![image-20230823110546944](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/image-20230823110546944.png)

3.修改测试版本和预发布版本Target 名称。

<img src="/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/image-20230823110900501.png" alt="image-20230823110900501" style="zoom: 50%;" />

![image-20230823111353997](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/image-20230823111353997.png)

![image-20230823111803385](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/image-20230823111803385.png)

4.现在打开相应target的`Build Settings`，滚动到`Packaging`，并将值改为相应的`plist`文件。

注意：这三个targets对应的代码相同，但Plist和设置是不同的

![image-20230823112657094](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/image-20230823112657094.png)

5.可选操作：但强烈推荐。如果你想简单地区分不同版本构建，你应该为每个版本使用单独的icon和启动页。这将使测试人员更清晰地知道正在使用哪个app,防止上传开发版本。

sets` 添加一个新的图标。右击图标 > iOS >New iOS App Icon . 新图标重命名为“AppIcon-Release”同时添加自己的图片。

![image-20230823135614531](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/image-20230823135614531.png)





弊端：
 1.生成多个info.plist文件
 2.配置繁琐且乱，容易配置遗忘其它targets
 3.通过声明宏的方式，容易写错
 4.真机测试需要的描述文件等比较多

### 二、使用多Scheme配置环境

正常情况下，选择`Edit Scheme ...` -> `Run` -> `Info` 只有两个`Build Configuration`可以选择（Debug/Release）

![1487527-e314e97ceab6e09f.png](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-e314e97ceab6e09f.png.webp)

这个`Build Configuration`是对应于 `PROJECT` 里的 `Info` ->  `Configuration`的

![1487527-7f774d9daa76f347](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-7f774d9daa76f347.webp)

于是乎可以自定义添加我们所需要的`Configuration`环境

![1487527-2b52fa792f7d7e39](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-2b52fa792f7d7e39.webp)

![1487527-b7b88f1acfa164f5](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-b7b88f1acfa164f5.webp)

![1487527-f2670e7b41581520](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-f2670e7b41581520.webp)

因为当前只有一个`Scheme`，当我们运行的时候，每次都来回点到`Edit Scheme...`切换环境，这无疑会导致容易操作疏漏的情况。

于是乎可以创建另外的`Scheme`，来配对刚才的配置环境，那每次选择环境的时候，只需要选择对应的`Scheme`就可以了：

![1487527-b562c5ccc0452060](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-b562c5ccc0452060.webp)

![1487527-26d22acb5ea95265](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-26d22acb5ea95265.webp)

![1487527-426c8005ae87727a](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-426c8005ae87727a.webp)

此时就可以选择对应的`Scheme`去到`Edit Scheme...`配对它对应的配置环境了

![1487527-76d10e79ba93c4a7](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-76d10e79ba93c4a7.webp)

![1487527-744ae8e2bc0ed3cb](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-744ae8e2bc0ed3cb.webp)

![1487527-18d6038425ab977b](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-18d6038425ab977b.webp)

那如果要区分环境去定义`不同的 主机hostUrl`呢？我们通过`Add User-Defined Setting`，自定义一个参数我起名为`HOST_URL`，它自动会分配三个环境，依次填入自己的主机域名即可（下图我做举例用）。

![1487527-6e4208f29f330382](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-6e4208f29f330382.webp)

通过定义了这个自定义参数，要如何读取出来呢？通过在`Info.plist`去声明

![1487527-d1ed98bfa11bc8cc](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-d1ed98bfa11bc8cc.webp)

Info.plist

访问`HOST_URL`就是读取Info.plist



```swift
// Swift
let mainBundle = Bundle.main
let identifer = mainBundle.bundleIdentifier
let info = mainBundle.infoDictionary
let CFBundleName = mainBundle.object(forInfoDictionaryKey: "CFBundleName")
let HOST_URL = mainBundle.object(forInfoDictionaryKey: "HOST_URL")
print("[identifer]:\(identifer!)")
print("[info]:\(info!)")
print("[CFBundleName]:\(CFBundleName!)")
print("[HOST_URL]: \(HOST_URL!)")
```



```objectivec
// OC 
NSString *path = [NSBundle.mainBundle pathForResource:@"Info" ofType:@"plist"];
NSDictionary *infoDic = [[NSDictionary alloc] initWithContentsOfFile:path];
NSLog(@"%@", infoDic[@"HOST_URL"]);
```

在`Building Settings`里所有的参数都会分三个不同的环境，这就意味着可以设置不一样的Icons、图标、名称等等...

弊端：在`Building Settings`里可能会不断地去找对应的配置然后三个环境不断地配置，不方便。

### 三、使用 Scheme + Configurations 配置（推荐）

本文仅做操作教学，对`.xcconfig`一点都不懂的同学可以看这里：[Swift进阶-工程化实践（一）](https://www.jianshu.com/p/13ba72edc61a)。

在上面demo的基础上，找到`Build Settings` -> `User-Defined`，将之前自定义个`HOST_URL`删掉
 接下来新建三个.xcconfig文件，命名规则 `目录-项目名.环境.xcconfig`

![1487527-f787319f76d8ee13](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-f787319f76d8ee13.webp)

![1487527-09ce92df59b29ac6](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-09ce92df59b29ac6.webp)

![1487527-5ac5c4e9837a7452](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-5ac5c4e9837a7452.webp)

让`.xcconfig`生效，配置到对应的`Configuration`下

![1487527-50302a9e49c6e5eb](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-50302a9e49c6e5eb.webp)

生效后可以在`Build Settings`中看到这个配置了

![1487527-c0dfa9c441921259](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-c0dfa9c441921259.webp)

附上[demo](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2F2448305504%2FSchemeXcconfigProject)
 喜欢的老铁，点个⭐️

### 问题集锦

适配好多环境工程后仍存在一些问题的

#### 问题一：

在我们没有配置`xcconfig`文件的工程，通过`Cocoapods`导入第三方库 `$ pod install` 后，我们的工程会自动配置成默认生效是使用了`Pods-ProjectName.Debug.xcconfig`和 `ProjectName.Debug.xcconfig`这两个环境的xcconfig，那我们自定义的xcconfig就没法生效了。
 解决问题一的方法：
 在我们自定义的xcconfig中去导入`Pods-ProjectName.Debug.xcconfig`

![1487527-c54161f4e99a3840](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-c54161f4e99a3840.webp)

xcconfig生效的地方设置成我们自定义的xcconfig文件即可。

#### 问题二：

比如我们用`Cocoapods`导入第三方库`AFNetworking`，在自定义的`Config-SchemeProject.Debug.xcconfig`里有这样一句

```bash
OTHER_LDFLAGS = -framework "AFNetworking"
```

而`Cocoapods`生成的xcconfig里也会有同一个设置值并且还有其它参数呢：

![1487527-f965272d55b573f3](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-f965272d55b573f3.webp)

最后生效的只有我们自定义的xcconfig (解决完问题一的情况)，而`Cocoapods`的`OTHER_LDFLAGS`的其它参数并没有生效了

![1487527-226e48483273e845](/Users/linggongbang/Desktop/笔记/IT/iOS/多环境/assets/1487527-226e48483273e845.png)

解决问题的的方法：
 在自定义的xcconfig声明参数钱加上 `$(inherited)` 即可。 `$(inherited)`是继承的意思。

```jsx
OTHER_LDFLAGS = $(inherited) -framework "AFNetworking"
```
