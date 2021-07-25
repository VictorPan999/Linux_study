# snap
###### tags: `Linux`

## 一.snap简介
　　什麼是snap，snap是一種全新的軟體包管理方式，它類似一個容器擁有一個應用程式所有的文件和庫，各個應用程式之間完全獨立。所以使用snap包的好處就是它解決了應用程式之間的依賴問題，使應用程式之間更容易管理。但是由此帶來的問題就是它占用更多的磁盤空間。

Snap的安裝包擴展名是.snap，類似於一個容器，它包含一個應用程式需要用到的所有文件和庫（snap包包含一個私有的root文件系統，裡麵包含了依賴的軟體包）。它們會被安裝到單獨的目錄；各個應用程式之間相互隔離。使用snap有很多好處，首先它解決了軟體包的依賴問題；其次，也使應用程式更容易管理。
現在支持snap的應用並不多，snap軟體包一般安裝在/snap目錄下
### Reason1
Not only does the program itself go into the package, but also all the required libraries.

On the other hand, this space is compensated by the ability to install recent versions of applications on older systems. 
### Reason2
Security also plays an important role, because snap applications are isolated from the rest of the system and applications. This makes it impossible for a program to modify essential parts of the system.

[Source](https://www.atechtown.com/snap-ubuntu/)

### About snap
* Snaps are slower to load. This will be more noticeable on old hardware.
* Snaps take up more hard disk space.
* Snaps are updated automatically.
* Snaps might not match your installed themes.
* Snaps are not always “official.” They’re often built by well-intentioned volunteers.

Snap use more hard drive real estate. With snaps, every application that needs a particular resource installs its own copy. This isn’t the most efficient use of hard drive space. Although hard drives are getting bigger and cheaper, traditionalists still balk at the extravagance of each application running in its own mini-container. Launching applications is slower, too.

Snaps do what they’re supposed to with the ring-fencing of different versions of the same application.

Also, installing applications from the command line with apt or apt-get is the same as it always was, and isn’t affected by snaps at all.

[Source](https://www.howtogeek.com/670084/what-you-need-to-know-about-snaps-on-ubuntu-20.04/)
## 二.snap安装
```
　　$ sudo apt-get install snapd
　　$ sudo apt-get install snapcraft
```
## 三.一些常用的命令
列出已经安装的snap包  
`$ sudo snap list`
搜索要安装的snap包  
`$sudo snap find <text to search>`
安装一个snap包  
`$ sudo snap install <snap name>`
更新一个snap包，如果你后面不加包的名字的话那就是更新所有的snap包  
`$ sudo snap refresh <snap name>`
把一个包还原到以前安装的版本
  `$sudo snap revert <snap name>`
删除一个snap包
`$ sudo snap remove <snap name>`
四.常用软件
clion
`$ sudo snap install clion`
pycharm
`$ sudo snap install pycharm`
网易云音乐
`$ sudo snap install netease-music --devmode --beta`

[Source](https://blog.csdn.net/anshujun7558/article/details/101250276?utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control)

