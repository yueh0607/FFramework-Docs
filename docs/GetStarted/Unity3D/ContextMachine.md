---
sidebar_position: 5
---

# AOT ContextMachine

FFramework为了热更新更多的逻辑，以及想要在热更新程序集内进行自我重新加载，引入了一个ContextMachine

此状态机将维护AppDomain/AssemblyLoadContext的调用和卸载，从能实现这样的自重载流程，并保证旧的AppDomain/AssemblyLoadContext能够正确卸载，同时保证所有调用来自Unity线程，并不发生阻塞。

由于在.NET Framework中以及.NET Core 3.0 以前，使用AppDomain管理程序边界，而在.NET Core 3.0及以后版本，使用更加轻量的AssemblyLoadConext来隔离程序运行环境，所以此处可能有两种实现。

> 热更新程序集->AOT程序集->热更程序集 

下图为笔者手绘的图解（有点丑，还少打字母，别介意）

![image-20240124212908485](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401242140319.png)