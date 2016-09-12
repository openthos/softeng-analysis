Systematic Testing for Resource Leaks in Android Applications

1.Android Java虚拟机的堆内存一般为16-64M，一般的操作系统的堆内存是好几百M。资源一般是 内存 bitmap 文件句柄 线程 binder，当软件耗费太多的这些资源的时候，就会造成系统缓慢，死机。

2.资源泄露发生在Activity的生命周期中。

3.文中举例APV（PDF阅读软件），当打开一个pdf然后back关闭文件（重复执行这个动作），由于代码bug的原因造成资源泄露。

4.作者提出了一个基础GUI模型的测试方法（自然循环---一个GUI事件的序列，这个序列不应该导致资源使用量的增加。通过测试用例可以暴露资源泄露的情况。），这个GUI模型就是一个有向图，节点代表activity，边缘代表GUI事件，有向图中的一条路径代表一个GUI事件序列。
GUI模型是基于FSM创建出来的。

6.使用反响工程软件AndroidRipper可用于产生GUI MODEL

7.作者开发了一个leakdroid的工具，这个工具主要是遍历模型中的路径产生相应的一个测试用例,测试用例中的GUI事件是通过Robotium testing framework触发产生的，这样可疑行为的资源使用量会被检测到。
