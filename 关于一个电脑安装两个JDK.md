## 关于一个电脑安装两个JDK

接单，使用到了JDK8和JDK17，需要在两个JDK之间切换，如果在一台电脑上安装多个JDK，**需要切换的话修改下[环境变量](https://so.csdn.net/so/search?q=环境变量&spm=1001.2101.3001.7020)即可**，这样工程开发起来就很方便了。

示例如下：

1 . 准备两个版本的jdk，下载到你习惯的路径，比如我的如下：
D:\Java\jdk1.8.0_321
D:\Java\jdk17

![image-20220523151338890](https://raw.githubusercontent.com/sunmiao0301/Public-Pic-Bed/main/imgfromPicGO/202205231513015.png)

2 . 添加环境变量:
**JAVA_HOME8(新增)**
D:\Java\jdk1.8.0_321

**JAVA_HOME17(新增)**
D:\Java\jdk17

**JAVA_HOME** **(新增)**
// 此处JAVA_HOME设置即为你更换jdk版本是所要修改的地方
%JAVA_HOME8%（或者是JAVA_HOME17）

比如我现在想切换到JDK17，则设置如下：

![image-20220523152842679](https://raw.githubusercontent.com/sunmiao0301/Public-Pic-Bed/main/imgfromPicGO/202205231528728.png)

> ~~**2.4 CLASSPATH路径最后面增加如下内容:**~~ 
>
> ~~.;%JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar;~~
>
> ~~**2.5 Path路径在\**最前面\**增加如下内容:**~~
>
> ~~%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;~~
>
> ~~一定要在最前面增加~~

3 . 查看版本是否更换成功

新开一个CMD窗口，命令行中输入：
java -version  

 ![image-20220523152941063](https://raw.githubusercontent.com/sunmiao0301/Public-Pic-Bed/main/imgfromPicGO/202205231529115.png)

**~~未成功解决方案：**~~

  ~~删除C:\Windows\System32下的java.exe、javaw.exe、javaws.exe~~

  ~~因为C:\Windows\System32目录优先级高于JAVA_HOME配置目录，所以有可能导致切换不生效。~~

  ~~个人是没有遇到过这种情况。~~



## 后来，准备调整回来的时候，发现尽管我将JAVA_HOME的值改为%JAVA_HOME8%，在cmd中java --version的时候仍然得到是java 17

问题原因见[链接](https://www.jianshu.com/p/0f972d981fad)

解决方案：
找到系统环境变量的Path，将其中的%JAVA_HOME%\bin上移到C盘的javapath之上，如下：

![image-20220528223443258](https://raw.githubusercontent.com/sunmiao0301/Public-Pic-Bed/main/imgfromPicGO/202205282234358.png)

然后重启cmd，然后再去cmd检查一下，没有问题了。

![image-20220528223634138](https://raw.githubusercontent.com/sunmiao0301/Public-Pic-Bed/main/imgfromPicGO/202205282236189.png)

此时再切换回java17之后，也没有问题：

![image-20220528223858837](https://raw.githubusercontent.com/sunmiao0301/Public-Pic-Bed/main/imgfromPicGO/202205282238897.png)

重启cmd之后，情况如下：

![image-20220528223825825](https://raw.githubusercontent.com/sunmiao0301/Public-Pic-Bed/main/imgfromPicGO/202205282238885.png)
