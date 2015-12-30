# 使用jenv管理多个java版本
## 安装jenv
使用brew安装  `brew install jenv`.

如果使用的是Bash
```shell
$ echo 'export PATH="$HOME/.jenv/bin:$PATH"' >> ~/.bash_profile
$ echo 'eval "$(jenv init -)"' >> ~/.bash_profile
```

如果使用的Zsh
```shell
$ echo 'export PATH="$HOME/.jenv/bin:$PATH"' >> ~/.zshrc
$ echo 'eval "$(jenv init -)"' >> ~/.zshrc
```

可能还需要创建`~/.jenv/versions`目录

## 安装jdk
没什么说的，去Oracle下载mac下各版本的jdk就行了，下载完成，直接安装。

## 配置JAVA_HOME
```shell
$ jenv add /System/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home
  oracle64-1.6.0.39 added
$ jenv add /Library/Java/JavaVirtualMachines/jdk17011.jdk/Contents/Home
  oracle64-1.7.0.11 added
```

## 使用jenv管理java版本
- 列出管理的jdk

```shell
$ jenv versions
  system
  oracle64-1.6.0.39
* oracle64-1.7.0.11 (set by /Users/hikage/.jenv/version)
```
- 切换jdk版本

```shell
$ jenv global oracle64-1.6.0.39
```
