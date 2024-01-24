---
sidebar_position: 7
---

# RefBuilder的使用

在物体上添加这样的组件

![image-20240124220136120](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401242201153.png)

通过引用构建工具生成代码，为BuildTarget拖入一个物体（需要有ScriptMark）之后，再Build Target会生成引用脚本。

也能在场景内自动搜寻，或者搜寻全部预制体。

- BuildTarget  构建目标
- BuildPath 脚本生成到的位置
- CreatePath 位置不存在是否创建
- ClassName 生成的类名（拖入BuildTarget自动更新）
- BaseClass 基类名
- BinderName 属性监听器类名
- IncreaseGen  增强生成的名称的唯一性
- Partial 生成分部类
- Awakeinit 是否在Awake时自动初始化

![image-20240124220029551](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401242200621.png)

例如生成这样的代码（不建议大量为字段生成，只在必要时使用，尽量只使用组件）

![image-20240124220100633](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401242201675.png)