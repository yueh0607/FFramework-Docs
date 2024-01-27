---
sidebar_position: 12
---

# UI

![image-20240124224037894](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401242240917.png)

UI面板需要实现 `UIPanel<TView>`，基类也有虚的OnLoad和OnUnload，与MVVM不同的是UI管理器将会保证面板的唯一性。一个面板只能有一个实例，而具体实现取决于用户，甚至OnHide和OnLoad不会对UI进行任何操作。您可以使用SetActive或者CanvasGroup进行显隐性操作。

另外要求Panel的预制体，必须带有画布！！能够独立显示

![image-20240124223449005](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401242234043.png)

栈UI是不被支持的，可以GetPanel入栈，然后逐个`await panel.Hide()`进行关闭...

UI部分的更多内容，请参考UI.cs

![image-20240124224008029](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401242240086.png)
