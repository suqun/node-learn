《Ubuntu下git安装》
==========

如果你碰巧用Debian或Ubuntu Linux，通过一条**sudo apt-get install git**就可以直接完成Git的安装，非常简单。


![图1](https://github.com/suqun/node-learn/blob/master/Lesson0/git.png)


老一点的Debian或Ubuntu Linux，要把命令改为sudo apt-get install git-core，因为以前有个软件也叫GIT（GNU Interactive Tools），结果Git就只能叫git-core了。由于Git名气实在太大，后来就把GNU Interactive Tools改成gnuit，git-core正式改为git。

如果是其他Linux版本，可以直接通过源码安装。先从Git官网下载源码，然后解压，依次输入：./config，make，sudo make install这几个命令安装就好了。

[参考Git教程][1] 
[1]:http:://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000  
