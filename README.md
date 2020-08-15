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
