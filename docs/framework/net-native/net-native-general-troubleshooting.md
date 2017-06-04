---
title: ".NET Native 一般疑难解答 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ee8c5e17-35ea-48a1-8767-83298caac1e8
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# .NET Native 一般疑难解答
该主题介绍了如何解决你在使用 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 开发应用时可能会遇到的问题。  
  
-   **问题：**你的生成输出窗口未适当更新。  
  
     **解决方法：**该生成输出窗口在生成完成之前不会更新。  生成时间可能会长达数分钟，因此在可能看到更新之前可能会有一个延误。  
  
-   **问题：**你应用的 ARM 零售生成时间已经后推。  
  
     **解决方法：**在你的 ARM 设备上部署应用时，调用 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 基础结构。  该编译执行了大量的优化，同时还确保反射等非静态语义继续工作。  此外，.NET 框架中应用使用的那部分得到动态链接，以达到最佳性能，并且还必须编译到本机代码之中。  这就是编译花费时间较长的原因。  
  
     然而，对于标准开发机器上的大多数应用而言，标准编译的编译时间仍在一分钟以内。  通常，在标准开发机器上仅为 .NET Framework 生成本机映像就要花上数分钟。  即使所有的优化可改善生成的代码并且包含 .NET 框架，应用版本时间通常要花费一两分钟。  
  
     我们将继续工作，通过调查多线程编译和其他优化方法来提升编译性能。  
  
-   **问题：**你不知道自己的应用是否使用 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 进行编译。  
  
     **解决方法：**如果调用 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 编译器，你会注意到生成时间变长，并且任务管理器会显示不同的 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 组件进程，如 ILC.exe 和 nutc\_driver.exe。  
  
     在使用 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 成功生成你的项目后，你可在 obj\\*config*\\ *arch*\\*projectname*.ilc\\out 目录下找到该输出。  最终原始包内容可在 bin\\*arch*\\*config*\\AppX 目录下找到。  如果你已部署了该应用，最终原始包内容位于 \\bin\\*arch*\\*config*\\AppX 目录下。  
  
-   **问题：**你的 .NET Native 编译的应用正在引发运行时异常（通常为 [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md) 或 [MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md) 异常），而应用未使用 .NET Native 进行编译时则不会引发该异常。  
  
     **分辨率：**由于 .NET Native 未提供元数据或通过反射可用的实现代码而引发异常。  （有关详细信息，请参阅 [.NET Native 和编译](../../../docs/framework/net-native/net-native-and-compilation.md)。） 若要消除此异常，必须将条目添加到你的[运行时指令 \(rd.xml\) 文件](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)，以便 .NET Native 工具链可以使元数据或实现代码在运行时可用。  有两个可用的故障排除程序，将生成要添加到运行时指令文件的必需条目：  
  
    -   [MissingMetadataException 故障排除程序](http://dotnet.github.io/native/troubleshooter/type.html)，用于类型。  
  
    -   [MissingMetadataException 疑难解答程序](http://dotnet.github.io/native/troubleshooter/method.html)，用于方法。  
  
     有关详细信息，请参阅[反射和 .NET Native](../../../docs/framework/net-native/reflection-and-net-native.md)。  
  
## 请参阅  
 [将 Windows 应用商店应用迁移到 .NET Native](../../../docs/framework/net-native/migrating-your-windows-store-app-to-net-native.md)