title: Ecliplse
author: Kenny Tang
date: 2017-08-04 17:13:35
tags:
---
Eclipse配置
将整个工程的编码设置为UTF-8

Windows-->Preferences-->General-->Workspace 在右侧版面中，选择 Text file encoding 选择 UTF-8。

将JSP页面的默认编码设置为UTF-8

Windows-->Web-->JSP Files   在右侧版面中，选择Encoding 为UTF-8

使用 Tab 键时，默认插入空格
![](/images/1.png)

关于在项目中使用tab还是使用空格，都有自己的喜好，我自己更倾向于使用空格，起源于之前在一个Android项目，使用tab出现无法正确的对齐的情况，导致界面出现错乱。各种编译器，平台对tab的支持可能是不相同的，这就可能导致不同的结果，但是无论那种平台对space的支持肯定是一致的。因此建议使用space代替tab进行操作。
![](/images/3.png)
之前在kepler中使用的是如上的配置，后来升级了一下版本，现在使用的是Luna使用如上的设置，发现不管用了。于是又细心的找了一下。
![](/images/4.png)
修改Eclipse的启动配置

eclipse.ini
```
-vm  
D:\Program Files\Java\jdk1.7.0_06\bin  
-startup  
plugins/org.eclipse.equinox.launcher_1.1.0.v20100507.jar  
--launcher.library  
plugins/org.eclipse.equinox.launcher.win32.win32.x86_1.1.0.v20100503  
-product  
org.eclipse.epp.package.jee.product  
--launcher.defaultAction  
openFile  
--launcher.XXMaxPermSize  
128M  
-showsplash  
org.eclipse.platform  
--launcher.XXMaxPermSize  
128m  
--launcher.defaultAction  
openFile  
-vmargs  
-Dosgi.requiredJavaVersion=1.6  
-Xverify:none  
-XX:+UseParallelGC  
-XX:+DisableExplicitGC  
-Xms728m  
-Xmx728m  
-Xmn273m  
```

-Xverify:none，Eclipse对字节码的验证，我们可以忽略这个验证过程，认为我们的类文件都是安全的
-XX:+UseParallelGC  使用并行的垃圾回收
-XX:+DisableExplicitGC 禁止使用System.gc 进行手动的垃圾回收
-Xms728m                    定义堆内存初始化大小
-Xmx728m                   定义堆内存的最大大小，定义最小与最大的堆大小相同减少堆调整的次数，默认空余堆内存小于40%时，JVM就会增大堆直到最大堆内存；空余堆内存大于70%时JVM会减少堆内存直到最小堆内存。
-Xmn273m    年轻带堆内存 官方建议为堆内存的 3/8
堆内存的组成	总堆内存 = 年轻带堆内存 + 年老带堆内存 + 持久带堆内存
年轻带堆内存	对象刚创建出来时放在这里
年老带堆内存	对象在被真正会回收之前会先放在这里
持久带堆内存	class文件，元数据等放在这里
　关闭Preferences中Validation
![](/images/5.png)
这些校验在使用Eclipse进行开发的过程中并没有感受到其带来的便利，但是使用这些功能会消耗eclipse的内存。所以还是关了吧。Disble All 然后确定。
![](/images/6.png)

关闭即时编译

一般Eclipse会在3s左右检查一次代码有没有改变，如果存在则进行编译，通常的情况下我们是不需要这种及时编译的，在我们运行代码之前编译一次就行了。Ctrl+B Shift+W 都是很好的选择。而且大家通常做的都是ＷＥＢ开发项目在发布前会进行编译。