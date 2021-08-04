# Tips-for-Geek

记录工作中遇到的一些小知识小技巧

## apt-file

当运行一个程序发现缺少库时：

```
$ ./jadx/bin/jadx-gui
Exception in thread "main" java.lang.UnsatisfiedLinkError: Can't load library: /usr/lib/jvm/java-11-openjdk-amd64/lib/libawt_xawt.so
```

可以使用 apt-file 进行搜索，然后安装对应的软件包即可：

```
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

## 开源协议

Vehicle-Security-Toolkit use SATA(Star And Thank Author) [License](./LICENSE), so you have to star this project before using. 🙏
