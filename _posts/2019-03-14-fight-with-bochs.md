---
layout: post
title: 与Bochs的战斗第一回合
author: "我不叫大脸猫"
header-style: text

---


##  与Bochs的战斗第一回合

最近正在读《一个64位操作系统的设计与实现》，一本不可多得的好书，如果你对操作系统内核实现原理感兴趣，并且你是一个爱动手的好孩子，那么你应该入手一本。作为一个爱动手的好孩子之一，并且作为一个自带踩坑buff的好孩子，在动手过程中不遇到点儿坑怎么行呢。果不其然，又双叒叕被我遇到一个奇葩的问题。本书推荐的开发调试环境是Centos6，模拟器是bochs，作为一个踩坑高手，怎么可能这么听话，我偏要在Ubuntu18.04上跑。嗯。。。还真遇到问题了。

贴一下我骚操作的过程，首先下载了个bochs2.6.8，注意这里的版本号并不重要，因为我后来还试过2.6.9。先配置一下编译选项：
```
./configure --with-x11 --with-wx --enable-debugger --enable-disasm --enable-all-optimizations --enable-readline --enable-long-phy-address --enable-ltdl-install --enable-idle-hack --enable-plugins --enable-a20-pin --enable-x86-64 --enable-smp --enable-cpu-level=6 --enable-large-ramfile --enable-repeat-speedups --enable-fast-function-calls--enable-handlers-chaining  --enable-trace-linking --enable-configurable-msrs --enable-show-ips --enable-cpp --enable-debugger-gui --enable-iodebug --enable-logging --enable-assert-checks --enable-fpu --enable-vmx=2 --enable-svm --enable-3dnow --enable-alignment-check  --enable-monitor-mwait --enable-avx  --enable-evex --enable-x86-debugger --enable-pci --enable-usb --enable-voodoo
```
然后是常规操作：
```
make && sudo make install
```
接着把一个nasm汇编文件编译成一个boot.bin，此处略去180个字。。。
执行bochs -f ./bochsrc:
然后进入工作模式选择，选6，然后咔擦，报错了：
```
usb_uhci file not found
```
接下来是常规的谷百环节，发现一个读者朋友写的博客，提到了如何解决这个问题，去svn下载代码，这个思路果然才智过人，而且这位老铁居然成功了。这里我们都忽略了一个细节，就是这个细节让我又花了1个小时请教了各路大佬，最终只能靠去除enable-usb的编译条件来规避这个问题。好巧不巧的，在跟群里各路大佬打完嘴仗，居然偶遇博文作者，我们在确定了Ubuntu内核版本等是否一致之后，把关注点放在了svn的版本上，果不其然，我看到博客去svn co的时候，bochs的仓库版本已经是13556了，而这位老铁svn co的时候版本是13534。换句话说就是他checkout代码的时候这个问题是应fixed的，而我checkout的时候这个问题不知道怎么回事儿又被改出来了。。。

然后为了解答我们心中的疑问，再次co 13534这个版本，居然真的没问题，确定就是bochs的各位大佬把这里又双叒叕给改坏了，心中一万头草泥马路过。。。

写个博客记录一下经验教训，防止后面还有其他小朋友也被坑。