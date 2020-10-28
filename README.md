# Homebrew 下载

下载`brew_install.rb`

# 执行

在`brew_install.rb`所在文件下

执行`ruby brew_install.rb`

# 方法二

```sh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

> 如果报错 `--RPC failed，curl 18 transfer closed with outstanding read data remaining`是因为项目太久，tag资源文件太大。
可以通过`git config --global http.postBuffer 524288000`解决

# 使用国内镜像安装HomeBrew

Mac下使用国内镜像安装Homebrew

First

MBP上的brew很老了，就想把brew更新一下，顺便安装一下NodeJs。无奈更新的过程一直卡在网络下载，毫不动弹。想想，应该是Repo访问不到的原因，于是重装brew。

根据官网上的方法，在终端输入：

```sh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
结果还是被卡在下载阶段，怎么办呢？于是上网搜索到了“Homebrew 的安装方法(官方的方法老是安装失败) 第三方”这篇文章。

依文中所述，进行安装。由于官方弃用了旧的homebrew仓库，将homebrew程序与软件包拆分成了两个仓库。与文中描述不符，也未能成功安装。于是稍作修改，记录于此。

## 国内的镜像
新增brew.git与homebrew-core.git镜像

由于官方弃用了旧的homebrew仓库，将homebrew程序与软件包拆分成了两个仓库。为保证用户正常升级，旧镜像将暂时保留一段时间，择期删除。

仓库对应关系：

> github.com/Homebrew/brew -> mirrors.ustc.edu.cn/brew.git

> github.com/Homebrew/homebrew-core -> mirrors.ustc.edu.cn/homebrew-core.git

> github.com/Homebrew/homebrew(弃用) -> mirrors.ustc.edu.cn/homebrew.git

引自：新增brew.git与homebrew-core.git镜像

## 安装
获取install文件并编辑
```sh
cd ~
curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install >> brew_install
```

编辑brew_install文件
```sh
#!/System/Library/Frameworks/Ruby.framework/Versions/Current/usr/bin/ruby
# This script installs to /usr/local only. To install elsewhere you can just
# untar https://github.com/Homebrew/brew/tarball/master anywhere you like or
# change the value of HOMEBREW_PREFIX.
HOMEBREW_PREFIX = "/usr/local".freeze
HOMEBREW_REPOSITORY = "/usr/local/Homebrew".freeze
HOMEBREW_CACHE = "#{ENV["HOME"]}/Library/Caches/Homebrew".freeze
HOMEBREW_OLD_CACHE = "/Library/Caches/Homebrew".freeze
#BREW_REPO = "https://github.com/Homebrew/brew".freeze
BREW_REPO = "git://mirrors.ustc.edu.cn/brew.git".freeze
#CORE_TAP_REPO = "https://github.com/Homebrew/homebrew-core".freeze
CORE_TAP_REPO = "git://mirrors.ustc.edu.cn/homebrew-core.git".freeze
```

注释掉BREW_REPO = "https://github.com/Homebrew/brew".freeze和CORE_TAP_REPO = "https://github.com/Homebrew/homebrew-core".freeze

修改为BREW_REPO = "git://mirrors.ustc.edu.cn/brew.git".freeze和CORE_TAP_REPO = "git://mirrors.ustc.edu.cn/homebrew-core.git".freeze

安装
```sh
/usr/bin/ruby ~/brew_install 
```

运行修改了的brew_install文件。

## 替换homebrew源

替换homebrew默认源
```sh
cd "$(brew --repo)"
git remote set-url origin git://mirrors.ustc.edu.cn/brew.git
```

## 替换homebrew-core源
```sh
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin git://mirrors.ustc.edu.cn/homebrew-core.git
```

## brew更新
```sh
brew update
```

## 设置 bintray镜像
```sh
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile
source ~/.bash_profile
```
