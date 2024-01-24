---
sidebar_position: 2
---

# 配置运行环境

配置过程不区分是否需要热更新等功能。

## 1.项目结构

建议的目录结构如下，且不在主场景内放置任何GameObject，为一些预制体单独创建场景用来预览和修改，以防止多人协作时的场景资源冲突。

![image-20240123154420604](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401231548184.png)

## 2.AOT配置

转到AOTConfig.cs，我们需要按照此处指示的名称配置YooAsset

![image-20240123154907621](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401231549648.png)

![image-20240123154922263](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401231549328.png)

对于前三个成员，我们不需要进行修改。对于后三个，我们可以按照需要进行修改，其中

- GameLogicPackage   --- 逻辑包名（在YooAsset进行分包，需要将HotFix目录下的逻辑dll收集到这个包内）
- MetaDataDllBytesTag ---通过资源Tag快速加载补充元数据
- HotUpdateDllBytesTag ---通过资源的Tag快速加载热更新程序集(默认只有Assembly-CSharp是热更程序集)

![需要被管理的DLL](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401231553440.png)

通过标签快速加载这两个文件夹下的内容

![image-20240123155614633](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401231556685.png)

![image-20240123155623676](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401231556698.png)

![image-20240123155941895](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401231559931.png)

通过RawFileBuildPipeline构建逻辑资源包并作为首包资源,但是此时请不要构建，配置并没有完成。

![image-20240123191633390](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401231921207.png)

![image-20240123191749593](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401231921949.png)

GameArts等其他资源包使用BuiltInBuildPipeline，可以作为后来热更新的资源包（同时游戏逻辑也能热更）

![image-20240123192128840](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401231921895.png)

Mode中有三种模式，现在显示的就是模拟模式，此模式下YooAsset使用模拟构建，HybridCLR也将直接使用程序集而不是加载bytes的方式，有更高的开发效率。

Offline为不需要热更新，需要把所有资源内置到包内。Host则为需要热更新。



对于HybridCLR,需要配置热更程序集为Assembly-CSharp(可以检查一下，一般不会丢失)

![image-20240123192543465](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401231925505.png)

