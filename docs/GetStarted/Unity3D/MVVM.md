---
sidebar_position: 11
---

# MVVM / MVC

- M  ： Model 模型层
- VM：ViewModel 视图-模型层
- V   ：View 视图层



其实这里的MVVM不是严格意义上的，你也可以叫他MVC，接下来将会具体的介绍一下，无非是将M和V进行分离解耦的手段，区别仅仅是这个中间层叫ViewModel还是Controller，怎么写中间层就叫什么（不要纠结这个到底叫什么，先预防一下）。



下图为对MVVM管理器进行初始化的举例，而UI管理器依赖于此MVVM管理器

![image-20240124222119452](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401242221504.png)

MVVM管理器只提供了Load和Unload，获取Model，释放句柄（关联预制体资源），不管理加载的实例T，T需要是ViewModel类型，K需要是View类型,加载出的实例需要自己管理，通过加载出的实例

![image-20240124222812229](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401242228269.png)

实现ViewModel一般可以使用下面两个虚方法。**View则是RefBuilder生成的，M可以是ConfigTool生成的，或者自己编写的实现IModel的任意类。**

![image-20240124223104107](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401242231137.png)
