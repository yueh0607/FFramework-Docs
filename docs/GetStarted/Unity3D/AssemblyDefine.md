---
sidebar_position: 4
---

# 程序集划分

由于框架需要支持热更新，所以使用了较为先进的C#热更新方案  [使用指南 | HybridCLR (code-philosophy.com)](https://hybridclr.doc.code-philosophy.com/docs/basic)

需要将程序集划分为

- AOT程序集
- 热更新程序集

其中AOT程序集在游戏全流程内不可热更（只能通过整包更新方式替换），而热更程序集可以任意更改。



在FFramework中，AOT程序集包括以下内容：

1. AOT入口（如程序入口，以及程序域/上下文状态机）
2. YooAsset（仅运行时，虽然编辑器处于此文件夹内，但是仅用于编辑器内模拟运行使用）
3. HybridCLR（不包括其生成的代码和DLL）
4. UnityEngine（也就是说UnityEngine的运行时算入AOT内不能热更）

注意更新以上内容均需要覆盖安装，否则可能引发程序异常。

其余的内容均属于热更新程序集，也就是说框架大部分均可热更新



您也可以直接通过YooAsset更新GameLogicPackage的dll内容，然后在热更新程序集入口内，重新调用AOT程序入口内的LoadDll协程即可加载dll到后台，再调用AOT入口的ContextMachine machine.MoveNext(),  将会自动从AOT程序集重新加载热更程序集，重启整个框架，直接利用新的代码加载入游戏。此过程不需要重启应用程序，但是在加载时可能出现一定的卡顿。如果有需要可以修改AOT使其在新的线程加载和补充元数据。