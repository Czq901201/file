# **android 项目jar包冲突问题解决**

大家在做开发中竟然需要用到一些三方库 或者 需要集成三方的SDK开发包，尤其是项目特别庞大的时候，引用的三方的东西特别多，那么肯定会碰到一些jar包冲突的情况。

常见的情况有以下几种：

1. 项目自己引用jar包重复

2. 项目中jar包和三方SDK

3. 三方sdk之间都含有相同类

4. 打包时候出现编译错误，出现冲突

   

## 1.项目自己引用jar包重复

com.android.dex.DexException: Multiple dex files define Landroid/support/v4/accessibilityservice，类似这种 v4包重复 ，直接删掉其中一个包就可以了。



## 2.项目中jar包和三方SDK

这其实有两种情况

1)  将一些三方的框架源码引用到项目中了比如 GSON ，Vollery这些，我们将里面的一些文件重写了，引用的是源码，这个和我们引用的三方库里面的冲突了 。

 这种情况，我们可以将三方库设置为私有 provided，如果还是有冲突我们可以将

 2) 直接导入的jar包 或者 gradle中配置的依赖 和项目中原有的一些jar包出现冲突。



## 3.三方sdk之间都含有相同类

比如你集成了友盟的sdk，又集成了支付的sdk，还集成了一些其他的sdk。这些sdk之间会有一些冲突。



## 4.打包时候出现编译错误，出现冲突

这种情况是正常手机调试运行没有问题，但是一打正式包就报错，冲突。

说了这么多，这些碰到这种项目中有冲突，或者有重复文件的情况我们如何解决呢？

一般常用的解决办法

1.双击shift 可以调出搜索 这个搜索是全局含jar搜索，可以快速定位到你搜索的东西存在哪个包下。

![20180813164309519](C:\Users\11635\Desktop\20180813164309519.png)

2.找到后 按上面讲的，解决也有几种情况

1）如果是两个相同的jar ，直接删掉一个

2）如果不同的jar有相同的引用 用exclude解决,大概意思就是去掉 你不需要的类

![20180813164659692](C:\Users\11635\Desktop\20180813164659692.png)

 3）打包出现的错误冲突等，我们可以找到 ，或者删除，或者修改，引入的方式可以修改为provided

这种方式只提供编译支持，但是不会写入apk。使用provide可以避免支持包版本冲突和重复打包导致安装包体积徒增。



# android导入aar文件与项目原来的冲突怎么办

> 1.选择File - New - Newmodule，如下图所示，将 aar 以 Module 的方式添加到工程中。

![20200426164344161](C:\Users\11635\Desktop\20200426164344161.png)



![20200426164413233](C:\Users\11635\Desktop\20200426164413233.png)



![20200426164549922](C:\Users\11635\Desktop\20200426164549922.png)



> 2.在 app Module 中添加 Module 的依赖，如下图所示：

![20200426164819790](C:\Users\11635\Desktop\20200426164819790.png)