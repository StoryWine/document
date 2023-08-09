### 查看本地源

```undefined
pod repo
```



### 默认master镜像

```dart
master
- Type: git (master)
- URL:  https://github.com/CocoaPods/Specs
- Path: /Users/xxx/.cocoapods/repos/master
```



### 修改默认镜像

国内网络限制，github源下载麻烦，可以切换默认master源
 清华源：[https://mirrors.tuna.tsinghua.edu.cn/help/CocoaPods/](https://links.jianshu.com/go?to=https%3A%2F%2Fmirrors.tuna.tsinghua.edu.cn%2Fhelp%2FCocoaPods%2F)
 gitee源：[https://gitee.com/mirrors/CocoaPods-Specs.git](https://links.jianshu.com/go?to=https%3A%2F%2Fgitee.com%2Fmirrors%2FCocoaPods-Specs.git)

#### 以清华源为例

> 对于旧版的 CocoaPods 可以使用如下方法使用 tuna 的镜像：

```ruby
$ pod repo remove master
$ pod repo add master https://mirrors.tuna.tsinghua.edu.cn/git/CocoaPods/Specs.git
$ pod repo update
```

> 新版的 CocoaPods 不允许用pod repo add直接添加master库了，但是依然可以：

```ruby
$ cd ~/.cocoapods/repos 
$ pod repo remove master
$ git clone https://mirrors.tuna.tsinghua.edu.cn/git/CocoaPods/Specs.git master
```

> 最后进入自己的工程，在自己工程的podFile第一行加上：

```bash
source 'https://mirrors.tuna.tsinghua.edu.cn/git/CocoaPods/Specs.git'
```



### 恢复默认gihub源

```bash
cd ~/.cocoapods/repos
pod repo remove master
git clone https://github.com/CocoaPods/Specs master
```

> 最后别忘了修改podfile文件：

```bash
source 'https://github.com/CocoaPods/Specs'
```

### 重要来了，如果还是想用gihub源，git clone又不能成功怎么办

可以在github上直接下载，Chrome具有断网续连功能，可以下载zip

```cpp
https://github.com/CocoaPods/Specs
```

![2915897-53bf1b0335a0ee3e](/Users/linggongbang/Desktop/笔记/IT/iOS/Cococapods/assets/2915897-53bf1b0335a0ee3e.jpeg)

然后把压缩包解压在

```undefined
/Users/xxx/.cocoapods/repos/
```

取名master，然后**新建一个隐藏文件夹.git**或者从其他源中复制一份.git文件夹，然后修改里面的config文件

```ruby
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true
    ignorecase = true
    precomposeunicode = true
[remote "origin"]
    url = https://github.com/CocoaPods/Specs
    fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
    remote = origin
    merge = refs/heads/master
```

然后在执行pod repo，查看当前源，就可以使用自己下载的github源了。