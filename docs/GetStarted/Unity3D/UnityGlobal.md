---
sidebar_position: 10
---

# UnityGlobal与UnityThread

UnityGlobal为在Unity内的全局单例，其中包含了一个UnityThread为MainThread，可以静态访问

可以按照相同的方式拓展更多生命周期，按照Core中的事件系统进行发布，内置仅提供Update一种生命周期。

![image-20240124221809094](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401242218137.png)

