# Tips-for-Geek

记录工作中遇到的一些小知识小技巧。

## apt-file

当运行一个程序发现缺少库时：

```sh
$ ./jadx/bin/jadx-gui
Exception in thread "main" java.lang.UnsatisfiedLinkError: Can't load library: /usr/lib/jvm/java-11-openjdk-amd64/lib/libawt_xawt.so
```

可以使用 apt-file 进行搜索，然后安装对应的软件包即可：

```sh
$ sudo apt install apt-file
$ sudo apt-file update
$ apt-file search libawt_xawt
openjdk-11-jre: /usr/lib/jvm/java-11-openjdk-amd64/lib/libawt_xawt.so
openjdk-11-jre-headless: /usr/lib/jvm/java-11-openjdk-amd64/lib/libawt_xawt.so
openjdk-13-jre-headless: /usr/lib/jvm/java-13-openjdk-amd64/lib/libawt_xawt.so
openjdk-14-jre-headless: /usr/lib/jvm/java-14-openjdk-amd64/lib/libawt_xawt.so
openjdk-16-jre: /usr/lib/jvm/java-16-openjdk-amd64/lib/libawt_xawt.so
openjdk-8-jre-headless: /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/amd64/libawt_xawt.so
$ sudo apt install openjdk-11-jre
```

## Ubuntu 20.04 VNC

打开远程桌面：

```sh
$ sudo apt install vino dconf-editor
$ dconf write /org/gnome/desktop/remote-access/require-encryption false
```

然后点击 `settings -> Sharing -> Screen Sharing` 进行设置即可。

## git 清理大文件

我有个仓库 security-paper 是收集各种 pdf 资料的，随着更新 `.git` 目录增长到近2G，导致clone很慢。这时候可以清理掉提交历史中遗留的大文件，达到瘦身的目的，推荐一个工具 [BFG Repo-Cleaner](https://rtyley.github.io/bfg-repo-cleaner/)，使用方法：

```sh
$ git clone --mirror git://example.com/some-big-repo.git
$ java -jar bfg.jar --strip-blobs-bigger-than 100M some-big-repo.git
$ cd some-big-repo.git
$ git reflog expire --expire=now --all && git gc --prune=now --aggressive
$ git push
```

## DEBIAN_FRONTEND 环境变量

DEBIAN_FRONTEND 环境变量告知系统应该从哪儿获得用户输入。如果设置为 `noninteractive`，你就可以直接运行命令，而无需向用户请求输入（所有操作都是非交互式的）。这在运行 apt-get 命令时格外有用，非交互模式会选择默认选项并以最快的速度完成构建。

```sh
# 使用ARG而不是ENV
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get -qq install {your-package}
# 或者
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -qq install {your-package}
```

## 路由器抓包

结合使用本机ssh、wireshark和远程tcpdump，路由器抓包竟如此丝滑：

```sh
$ ssh root@192.168.12.3 "tcpdump -i lo -s 0 -w -" | wireshark -k -i -
```

## 开源协议

Vehicle-Security-Toolkit use SATA(Star And Thank Author) [License](./LICENSE), so you have to star this project before using. 🙏
