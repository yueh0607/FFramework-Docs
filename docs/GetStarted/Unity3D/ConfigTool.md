---
sidebar_position: 6
---

# ConfigTool的使用

FFramework提供了Excel导表工具

- 传统工具是  Excel->中间高效文件->代码异步读取
- 而此工具是 Excel->CSharp代码常量->代码直接读取

仔细一想其实并没有太大优势，如果硬要分析一下的话...

- 行数少的时候效率非常高，new 一个对象能有多大损失...
- 行数多的时候，可能new一个对象需要0.05s左右（测试过10000条数据），两个加一起也是0.05s
- 可能不方便运行时修改Excel
- 可能修改代码需要重新编译（不过这个不是问题，可以在文件夹里添加一个程序集定义直接变成热更新程序集）
- 非常直观，一眼就能看会，没有什么门槛
- 非常灵活，因为转C#代码，格子内可以填出很多自由的东西，比如Type，Func，而且容易拓展
- 和传统的一样支持字母表，表中可以关联其他表

同样也有检查机制，自定义表检查，所以客观来讲其实也就差不多那样....但是肯定跟luban那种有专门团队维护的比不了的，作者维护不起这种东西（跟字符串终日纠缠QAQ）...

生成速度也并不低，可以跟踪生成变化的文件，也可以忽略文件

![image-20240124214345543](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401242143583.png)

![image-20240124215331002](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401242153036.png)

![image-20240124215349605](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401242153639.png)

![image-20240124215433640](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401242154718.png)

如果有拓展需求的话

![image-20240124215735095](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401242157133.png)

照着这个里面的模板写就可以了，但是要特别注意上面打的特性之类的，不要复制之后忘改，会变得不幸。

![image-20240124215831430](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401242158478.png)