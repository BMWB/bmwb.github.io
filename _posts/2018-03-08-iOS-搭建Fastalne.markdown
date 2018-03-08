### 一、环境配置

- #### 安装rbenv

  ##### 1.安装rbenv

  rbenv的源代码托管在github，在终端中，从github上将rbenv源码克隆到本地，然后设置$ PATH。

  ```
  git clone git://github.com/sstephenson/rbenv.git ~/.rbenv
  echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
  echo 'eval "$(rbenv init -)"' >> ~/.bashrc

  ```

  注意zsh用户是〜/ .zshrc

  ##### 2.安装ruby-build

  `git clone git://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build`

  ##### 3.安装Ruby

  查看可用的ruby版本

  `rbenv install --list`

  这里从列表中选择*2.4.2*进行安装：

  `rbenv install 2.4.2`

  等待一会儿，安装完毕后可以查看已经安装的所有Ruby版本：

  `rbenv versions`

  ##### 4.选择一个Ruby版本

  rbenv中的Ruby版本有三个不同的作用域：全局（global），本地（local），当前终端（shell）。

  查找版本的优先级是当前终端>本地>全局。

  4.1设置全局版本

  全局版本是在没有找到“当前终端”或“本地”作用域的设置时执行通过以下命令设置：

  `rbenv global 2.1.2`

  4.2设置本地版本

  “本地”作用域是针对各个项目的，通过项目文件夹中的.rbenv-version这个文件进行管理，需要将相应的Ruby版本号写入这个文件。所以一般设置这个选项就可以了，这个过程可以通过以下命令执行：

  `rbenv local 2.1.2`

  4.3设置当前终端版本

  “当前终端”作用域的优先级最高通过以下命令设置：

  `rbenv shell 2.1.2`

  4.4使用系统Ruby

  如果要使用系统原有的Ruby，则通过系统指定：

  `rbenv global system`

  设置完毕后可以通过以下命令进行验证：

  ```
  which ruby  # ~/.rbenv/shims/ruby 

  rbenv version # 2.1.2 (set by ~/.rbenv/version)

  ```

  ## 

- #### 安装Gem

  使用rbenv后，gem还是按照原有的方式进行安装、升级，只是gem的安装路径是在~/.rbenv 文件夹中当前Ruby版本文件夹下。而且安装带有可执行文件的gem后，需要执行一个特别的命令，告诉rbenv更新相应的映射关系，这个命令在安装新版本的Ruby后也需要执行

  ```
  rbenv rehash
  ```

  安装rails

  ```
  gem install bundler rails
  ```

  检查安装后的软件版本

  ```
  ruby -v gem -v rake -V rails -v
  ```

  告诉Rubygems安装软件包的时候不安装文档

  ```
  echo "gem: --no-ri --no-rdoc" > ~/.gemrc
  ```

  安装后在.zshrc中添加

  > export PATH="$HOME/.rbenv/shims:$PATH"

  > **查看gem源**
  >
  > gem sources
  >
  > **删除默认的gem源**
  >
  > gem sources --remove https://rubygems.org/
  >
  > **增加taobao作为gem源**
  >
  > gem sources -a https://ruby.taobao.org/
  >
  > **查看当前的gem源**
  >
  > gem sources
  >
  > *** CURRENT SOURCES ***
  >
  > http://ruby.taobao.org
  >
  > **清空源缓存**
  >
  > gem sources -c
  >
  > **更新源缓存**
  >
  > gem sources -u

  ​

- #### 配置bundler

  安装gem后bundler是自带文件你可以运行

  > gem list 查看版本

  删除/Users/wtj/.bundle/config，或者更改config中的BUNDLE_PATH路径,要不然会生成一堆项目目录下文件

  > BUNDLE_PATH: "vendor/bundle"
  >
  > BUNDLE_DISABLE_SHARED_GEMS: "true"

  项目中的Gemfile文件可通过如下命令生产，也可以自己创建填写内容

  > bundle init 生成Gemfile文件

  > bundle install --path /Users/wtj/Public/vendor/bundle 指定路径

  **bundler配置文件:**

  - 项目特定配置文件, 放在项目根目录下的.bundle/config文件中.
  - 全局的配置文件, 放在 ~/.bundle/config文件中.

  比如你在当前项目运行bundle install --without production, 后面的参数"--withou production"会自动被保存到项目根目录的.bundle/config文件中. 下一次运行bundle install会自动为你加上参数.

- #### 安装xcode-select --install

- #### 安装fastalne

  #####运行sudo gem install fastlane --verbose

  fastlane是一套自动化打包的工具集，用 Ruby 写的，用于 iOS 和 Android 的自动化打包和发布等工作。

  fastlane包含了我们日常编码之后要上线时候进行操作的所有命令。

  > ```
  > deliver：上传屏幕截图、二进制程序数据和应用程序到AppStore
  > snapshot：自动截取你的程序在每个设备上的图片
  > frameit：应用截屏外添加设备框架
  > pem：可以自动化地生成和更新应用推送通知描述文件
  > sigh：生成下载开发商店的配置文件
  > produce：利用命令行在iTunes Connect创建一个新的iOS app
  > cert：自动创建iOS证书
  > pilot：最好的在终端管理测试和建立的文件
  > boarding：很容易的方式邀请beta测试
  > gym：建立新的发布的版本，打包
  > match：使用git同步你成员间的开发者证书和文件配置
  > scan：在iOS和Mac app上执行测试用例
  > ```

  整个发布过程可以用fastlane描述成下面这样

  > ```
  > lane :appstore do
  >   increment_build_number
  >   cocoapods
  >   xctool
  >   snapshot
  >   sigh
  >   deliver
  >   frameit
  >   sh "./customScript.sh"
  >
  >   slack
  > en
  > ```


###二、fastlane脚本编写

**fastlane文件夹下在新建一个Fastfile**

> ```
> # Customise this file, documentation can be found here:
> # https://github.com/fastlane/fastlane/tree/master/fastlane/docs
> # All available actions: https://github.com/fastlane/fastlane/blob/master/fastlane/docs/Actions.md
> # can also be listed using the `fastlane actions` command
>
> # Change the syntax highlighting to Ruby
> # All lines starting with a # are ignored when running `fastlane`
>
> # If you want to automatically update fastlane if a new version is available:
> # update_fastlane
>
> # This is the minimum version number required.
> # Update this, if you use features of a newer version
> fastlane_version "1.110.0"
>
> default_platform :ios
>
> platform :ios do
>
>   before_all do
>     ENV["SLACK_URL"] = "https://hooks.slack.com/services/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" # Webhook URL created in Slack
>   end
>
>   # 编译测试版本
>   desc "Jenkins"
>   lane :jenkins do |options|
>     branch = 'master'
>
>     ensure_git_branch(branch: branch)
>     ensure_git_status_clean
>     git_pull
>     #increment_build_number
>     # commit_version_bumpi
>     # push_to_git_remote(remote:'origin', local_branch: branch, remote_branch: branch)
>     # add_badge(shield: "v#{get_version_number}-#{get_build_number}-orange", no_badge: true)
>
>     ipaFileName = “ test.ipa”;#”DailyBuild_v#{get_version_number}.#{get_build_number}.ipa";
>     gym(
>       workspace: './test.xcworkspace',
>       scheme: 'test',
>       clean: true,
>       output_directory: ENV['SP_OUTPUT_DIRECTORY'],
>       output_name: ipaFileName,
>       configuration: 'Release',
>       include_symbols: 'true',
>       include_bitcode: 'false',
>       archive_path: ENV['SP_ARCHIVE_PATH'],
>       export_method: 'ad-hoc',
>       codesigning_identity: 'XXXX(123456)',
>       xcargs: "PROVISIONING_PROFILE_SPECIFIER='ad-hoc' DEVELOPMENT_TEAM='123456'",
>       export_options: {
>       provisioningProfiles: {"com.XXXX.XXXX" => "ad-hoc"},
>       method:'ad-hoc',
>       signingStyle:'manual'
>    }
>     )
>     
>     pgyer(
>       api_key: "", 
>       user_key: "",
>       ipa: "#{ENV['SP_OUTPUT_DIRECTORY']}#{ipaFileName}")
>   end
>
> end
> ```

**安装Plugin**

到目前为止，大约有30个Plugin发布到了RubyGems下，我们可以通过如下命令来查找：

> fastlane search_plugins [query]

详情可以看这里
[AvailablePlugins](https://docs.fastlane.tools/plugins/AvailablePlugins/)

假设我们的项目中需要使用一个名叫version_from_last_tag，用于获取git的最近一个tag，那么我们在终端的项目目录下执行：

> fastlane add_plugin version_from_last_tag

添加完成后，项目中会多出一个Gemfile，Gemfile.lock，fastlane/Pluginfile三个文件，其中这个Pluginfile实际上就是一个Gemfile，里面包含对于Plugin的引用，格式如下：

```
# Autogenerated by fastlane
#
# Ensure this file is checked in to source control!

gem 'fastlane-plugin-version_from_last_tag'
gem 'fastlane-plugin-badge'
gem 'fastlane-plugin-pgyer'
```

而Pluginfile本身又被Gemfile引用，所以又印证上上文中的那句话：对Plugin的管理其实就是对RubyGem的管理。

此后的Plugin是实际用法和使用Action是一致的，所以就不在此赘述了。



###三、Xcode工程配置

在Product —>Scheme —>Manage Schemes —>你的工程Scheme的Shared为YES

在.gitignore添加如下两句，防止report.xml和README.md自动生成每次commit带入

> fastlane/report.xml
>
> fastlane/README.md

### 参考：

[升级Cocoapods 1.1.0](http://www.jianshu.com/p/e9588deecf5b)

[http://bundler.io/](http://bundler.io/v1.2/bundle_install.html)

[使用 rbenv 安装和管理Ruby版本](https://gist.github.com/sandyxu/8aceec7e436a6ab9621f)

[使用rbenv安装和管理Ruby版本](https://www.hi-linux.com/posts/41737.html)

[Fastlane入门:安装篇](http://www.jianshu.com/p/78e324a4962c)

[fastlane 之截图自动化](https://zhuanlan.zhihu.com/p/20739972?refer=cocoanotes)（看着很蛋疼）

[fastlane deliver 上传app到App Store](http://www.jianshu.com/p/e0891a9c94d8)

[Fastlane自动化构建工具(完整解决测试和发布流程)](http://www.jianshu.com/p/edcd8d9430f6)

[使用 Jenkins 实现持续集成 (iOS)](https://www.pgyer.com/doc/view/jenkins_ios)

[Fastlane实战（五）：高级用法](http://www.jianshu.com/p/faae6f95cbd8)

[ fastlane docs](https://docs.fastlane.tools/)

[Fastlane实战（四）：自动化测试篇](http://www.jianshu.com/p/607363a3fd46)

[深入浅出 Fastlane 一看你就懂](https://icyleaf.com/2016/07/fastlane-in-action/)

 