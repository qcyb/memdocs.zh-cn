---
title: Configuration Manager 工具
titleSuffix: Configuration Manager
description: 了解可帮助管理 Configuration Manager 基础结构并对其进行故障排除的工具。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 06e308a54ee9636a7781667823e7b7f98ae6f25c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701265"
---
# <a name="configuration-manager-tools"></a>Configuration Manager 工具

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 工具包括[基于客户端的工具](#client-tools)和[基于服务器的工具](#server-tools)。 使用这些工具，帮助支持 Configuration Manager 基础结构并对其进行故障排除。

从 Configuration Manager 版本 1806 开始，这些工具包含在站点服务器上的 `CD.Latest\SMSSETUP\Tools` 文件夹中。 无需进行其他安装。<!--1357145--> 将这些版本的工具与 Configuration Manager 版本 1806 及更高版本一起使用。

所有在[客户端和设备支持的操作系统](https://docs.microsoft.com/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices)中列为受支持客户端的 Windows 操作系统均支持使用这些工具。

> [!Note]  
> 仍可从 Microsoft 下载中心获取 [System Center 2012 R2 Configuration Manager 工具包](https://www.microsoft.com/download/details.aspx?id=50012)。 对于 Configuration Manager 版本 1806 及更高版本，在站点服务器上的 CD.Latest 文件夹中使用这些版本的工具。 有些工具之前位于工具包中，但不包括在版本 1806 中。 不再支持这些旧工具。


## <a name="client-tools"></a>客户端工具

这些工具位于 `ClientTools` 子文件夹中：

- [CMTrace](cmtrace.md)：查看、监视并分析 Configuration Manager 日志文件  

- [客户端 Spy](clispy.md)：对与软件分发、清单和计数相关的问题进行故障排除

- [部署监视工具](deployment-monitoring-tool.md)：对应用程序、更新和基线部署进行故障排除  

- [策略监视](policy-spy.md)：查看策略分配  

- [电源查看器工具](power-viewer-tool.md)：查看电源管理功能状态  

- [发送计划工具](send-schedule-tool.md)：触发配置基线的计划和评估  

> [!Note]  
> `ClientTools` 文件夹还包含文件 Microsoft.Diagnostics.Tracing.EventSource.dll。 好几个客户端工具都需要此库。 不能直接使用它。  


## <a name="server-tools"></a>服务器工具

这些工具位于 `ServerTools` 子文件夹中：

- [DP 作业队列管理器](dp-job-manager.md)：对面向分发点的内容分发作业进行故障排除  

- [集合评估查看器](ceviewer.md)：查看集合评估详细信息  

- [内容库资源管理器](content-library-explorer.md)：查看内容库单一实例存储的内容  

- [内容库转让](content-library-transfer.md)：在驱动器之间转让内容库  

- [内容所有权工具](content-ownership-tool.md)：更改孤立包的所有权。 这些包存在于没有自有站点服务器的站点。

- [基于角色的管理和审核工具](rbaviewer.md)：帮助管理员审核角色配置  

- [运行计量摘要工具](run-meter-summ.md)：运行计数摘要任务并分析计量数据

> [!Note]  
> ServerTools 文件夹还包括以下文件：
>
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll
>
> 好几个服务器工具都需要这些库。 不能直接使用它们。  

## <a name="other-tools-and-toolkits"></a>其他工具和工具包

- [支持中心](support-center.md)：进行故障排除时，请从客户端收集信息以便于分析。

    从版本 1906 开始，OneTrace  是一个带有支持中心的新日志查看器。 它的工作方式与 CMTrace 类似，同时进行了一些改进。 有关详细信息，请参阅[支持中心 OneTrace](support-center-onetrace.md)。

- [将本地站点扩展并迁移到 Microsoft Azure](azure-migration-tool.md)：帮助你以编程方式为 Configuration Manager 创建 Azure 虚拟机 (VM)。 <!--3556022--> 

- [内容库清理工具](../plan-design/hierarchy/content-library-cleanup-tool.md)：使用 `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` 中的 ContentLibraryCleanup.exe 来从分发点删除孤立的内容  。  

- [层次结构维护工具](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md)：使用站点服务器上 `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` 共享文件夹中的 Preinst.exe 将命令传送到层次结构管理器组件  。  

- [更新重置工具](../servers/manage/update-reset-tool.md)：在控制台中更新出现下载或复制问题时，可使用 `CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` 中的 CMUpdateReset.exe 修复这些问题  。  

- [服务连接工具](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md)：服务连接点处于脱机状态时，可使用 `CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool` 中的 ServiceConnectionTool.exe 使站点保持最新状态  。   

- [Microsoft Deployment Toolkit (MDT)](../../mdt/use-the-mdt.md)：一系列工具、流程和指南，用于自动执行桌面和服务器 OS 部署。

- [System Center Updates Publisher (SCUP)](../../sum/tools/updates-publisher.md)：用于管理和导入自定义软件更新的独立工具。

- [包转换管理器](../../apps/pcm/package-conversion-manager.md)：将旧包转换为应用程序。
