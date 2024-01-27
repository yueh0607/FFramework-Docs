---
sidebar_position: 3
---

# 初始化框架

框架的主入口放置于Game.cs下

![image-20240124205105697](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401242051818.png)

![image-20240124205125351](https://raw.githubusercontent.com/yueh0607/MyPicueres/main/202401242051385.png)

Initialize一般用于全局环境的初始化，而Process代表游戏流程

在初始化中，我们首先需要初始化YooAsset，详情请参考YooAsset文档   [初始化 | YooAsset](https://www.yooasset.com/docs/guide-runtime/CodeTutorial1)

```csharp
    public static async FTask Initialize()
    {
        //初始化YooAsset
        ResourcePackage defaultPackage = YooAssets.CreatePackage("GameArts");
        YooAssets.SetDefaultPackage(defaultPackage);

#if FF_SIMULATED
        var initParameters = new EditorSimulateModeParameters();
        var simulateManifestFilePath = EditorSimulateModeHelper.SimulateBuild(EDefaultBuildPipeline.BuiltinBuildPipeline, "GameArts");
        initParameters.SimulateManifestFilePath = simulateManifestFilePath;
#endif
#if FF_OFFLINE
        OfflinePlayModeParameters initParameters = new OfflinePlayModeParameters();
#endif
        await defaultPackage.InitializeAsync(initParameters);
        Debug.Log($"GameArts 资源包初始化状态: {defaultPackage.InitializeStatus}");

        MVVM.Package = defaultPackage;
        MVVM.LoadConverter = (type) => type.Name;
        Debug.Log("MVVM初始化完成");

        await FTask.CompletedTask;
    } 
```



其中FF_开头的宏均为框架提供的，通过FFramework/MainPanel进行调整模式将会自动改变宏。

您也可以在初始化中调用框架的任意模块，包括热更新资源和重启框架等，将会在后续内容给出。

等待初始化完毕后，将会自动开始执行Process

