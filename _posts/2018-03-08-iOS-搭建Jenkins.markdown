## 一.环境配置

环境配置请参考[jenkins持续集成iOS项目](http://www.jianshu.com/p/53636eb87fe8)

  ​

## 二.安装jenkins

#### 1.pkg安装包(不推荐)


![屏幕快照 2017-10-21 下午2.57.55.png](http://upload-images.jianshu.io/upload_images/2280085-b31dd586f612606b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 2.brew安装包

- brew install jenkins-lts(稳定版)

#### 3.下载.war安装包

- [jenkins官网](https://jenkins.io/download/)下载.war包


![屏幕快照 2017-10-21 下午2.58.21.png](http://upload-images.jianshu.io/upload_images/2280085-ca16fc0e4a826cb0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 新建jenkins文件然后增加权限 —>chmod 777 jenkins

  > \#!/bin/bash
  >
  > export JENKINS_HOME=${PWD}/.jenkins
  >
  > JENKINS_PORT=9999
  >
  > java -Dhudson.DNSMultiCast.disabled=true -jar jenkins.war --httpPort=$JENKINS_PORT -Dfile.encoding=UTF-8**%** 

- 终端执行./jenkins 启动,然后打开浏览器输入 localhost:9999 

  > *http://localhost:9999/exit*       //退出Jenkins
  >
  > *[http://localhost:9999/](http://localhost:8080/exit)restart*  //重启
  >
  > *[http://localhost:9999/](http://localhost:8080/exit)reload * //重新加载
  >
  > 第一次启动后会有一串密钥， 复制到下面这个框里，然后一路安装
  >

![1194012-c8468fd91737f725.png](http://upload-images.jianshu.io/upload_images/2280085-7dbefffb522409f8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![1194012-cd9979b853d14ac6.png](http://upload-images.jianshu.io/upload_images/2280085-eb7632f1dac41db6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![1194012-56431c2d22013dcd.png](http://upload-images.jianshu.io/upload_images/2280085-67ebb4f95ea654ba.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![1194012-578857333787630a.png](http://upload-images.jianshu.io/upload_images/2280085-1d6b6999a2bf6082.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![1194012-a5636c896f987a50.png.jpeg](http://upload-images.jianshu.io/upload_images/2280085-cb1d587764e5663a.jpeg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![1194012-7ac78a54760114dd.png.jpeg](http://upload-images.jianshu.io/upload_images/2280085-b998378152951223.jpeg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
##三.安装插件

- **安装GitLab插件**

  > 因为我们用的是GitLab来管理源代码，Jenkins本身并没有自带GitLab插件，所以我们需要依次选择 **系统管理**->**管理插件**，在“**可选插件**”中选中“**GitLab Plugin**”和“**Gitlab Hook Plugin**”这两项，然后安装。

- **安装Xcode插件**

  >同安装GitLab插件的步骤一样，我们依次选择**系统管理**->**管理插件**，在“**可选插件**”中选中“**Xcode integration**”安装。

- **安装签名证书管理插件**

  >iOS打包内测版时，需要发布证书及相关签名文件，因此这两个插件对于管理iOS证书非常方便。还是在系统管理->管理插件，在“可选插件”中选中“Credentials Plugin”和“Keychains and Provisioning Profiles Management”安装。

- **安装脚本插件**

  >这个插件的功能主要是用于在build后执行相关脚本。在**系统管理**->**管理插件**，在“**可选插件**”中选中“**Post-Build Script Plug-in**”安装

- **安装FTP插件**

  >在**系统管理**->**管理插件**，在“**可选插件**”中选中“**Publish over FTP**”安装。

## 四.新建项目

- **新建一个项目**

![1194012-06d0118a5e04dadf.png.jpeg](http://upload-images.jianshu.io/upload_images/2280085-3feff85fd85f620c.jpeg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![1194012-b52d3d102c21f004.png.jpeg](http://upload-images.jianshu.io/upload_images/2280085-1def61a2bd9d8123.jpeg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![屏幕快照 2017-10-21 下午3.55.17.png](http://upload-images.jianshu.io/upload_images/2280085-ee6d88ae94c8c7ae.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![屏幕快照 2017-10-18 下午2.14.09.png](http://upload-images.jianshu.io/upload_images/2280085-81b33eadbbf9e655.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![屏幕快照 2017-10-18 下午2.14.19.png](http://upload-images.jianshu.io/upload_images/2280085-782a280577df4999.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![屏幕快照 2017-10-18 下午2.14.25.png](http://upload-images.jianshu.io/upload_images/2280085-1e7d1d71ca827267.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
## 五.脚本文件

- ##### gym 命令

  >​

  ​

## 六.卸载jenkins

- PKG卸载

  >/Library/Application Support/Jenkins/Uninstall.command

- brew卸载

  >brew uninstall jenkins
  >
  >sudo launchctl unload /Library/LaunchDaemons/org.jenkins-ci.plist  
  >sudo rm !$  
  >sudo rm -rf /Applications/Jenkins "/Library/Application Support/Jenkins" /Library/Documentation/Jenkins  
  >sudo rm -rf /Users/Shared/Jenkins  
  >
  >#######if you want to get rid of all the jobs and builds:
  >
  >sudo dscl . -delete /Users/jenkins  
  >#######delete the jenkins user and group (if you chose to use them):
  >
  >sudo dscl . -delete /Groups/jenkins

- .war卸载

  直接删除目录

## 七.完整的持续集成流程


![1194012-60e101c4e6cc14fd.png](http://upload-images.jianshu.io/upload_images/2280085-37934fcc1be5cd60.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##参考：

[在Mac下搭建jenkins+github环境](http://crazysky.iteye.com/blog/1763673)

[Jenkins For iOS安装](http://www.jianshu.com/p/5cad74906159)

[Mac中jenkins的使用——自动构建](http://blog.csdn.net/potato512/article/details/52289136)

[Mac OSX搭建Jenkins持续集成环境](http://blog.csdn.net/sbsujjbcy/article/details/51166525)

[手把手教你利用 Jenkins 持续集成 iOS 项目](https://halfrost.com/ios_jenkins/)

[使用GitLab，Mac下如何生成SSH Key](http://www.jianshu.com/p/46aaccc71ce8)

[Mac环境下如何配置Jenkins](http://www.jianshu.com/p/b4efe5a3b442)

[组件化开发之-基于Jenkins搭建iOS持续集成开发环境](http://www.jianshu.com/p/31547d866f20)

[Jenkins & Docker 持续集成实践](https://mp.weixin.qq.com/s/xi7pZmMMVZZlBNee-Md-Ig)