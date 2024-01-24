---
sidebar_position: 1
---

# 创建一个项目

通过GitBash进行克隆

```bash
git clone https://github.com/yueh0607/FFramework.git 
```

找到其中的Unity文件夹，使用UnityHub打开（不要修改文件夹名称）

![image-20240123153046129](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401231530024.png)

正常情况下会有报错，原因是Unity的包有部分丢失

需要手动在PackageManager内安装以下两个包，其中第一个是YooAsset所依赖的，因为丢失这个包，导致YooAsset.dll不能正确被引用，所以这里需要手动恢复它的引用（YooAsset.Editor的使用在Build时将会自动去除，主要用于便于模拟）

![image-20240123153456843](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401231534877.png)

![image-20240123153653114](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401231536161.png)

另一个则是FFramework依赖的，安装对应版本即可

![image-20240123153511344](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401231535379.png)

![image-20240123153851388](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401231538424.png)

此时所有编译错误都已经得到解决，创建项目完成。
