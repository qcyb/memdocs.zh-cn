---
title: 安装程序参考
titleSuffix: Configuration Manager
description: 查看此参考可帮助做好 Configuration Manager 站点或层次结构安装准备。
ms.date: 04/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d948452da54a41e35095b01cb0e942e02a7a597f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700555"
---
# <a name="reference-for-configuration-manager-setup"></a>Configuration Manager 安装程序参考

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 安装程序提供了几个主题的链接，以下部分对相关内容进行了详细介绍。 此处提供的信息有助于准备安装 Configuration Manager 站点或层次结构，且有助于为某些必须在安装过程中做出的决定做好准备。  


##  <a name="before-you-begin"></a><a name="bkmk_start"></a> 在开始之前  
在安装新的 Configuration Manager 站点之前，请确保已经查看以下信息，这些信息有助于为成功完成部署设计做好准备：  

-   [Configuration Manager 基础知识](../../../../core/understand/fundamentals.md)  
-   [规划 Configuration Manager 的基础架构](../../../plan-design/network/configure-firewalls-ports-domains.md)  
-   [准备安装 Configuration Manager 站点](prepare-to-install-sites.md)  

##  <a name="assess-server-readiness"></a><a name="bkmk_assess"></a> 评估服务器准备情况  
在开始安装新站点之前，请确保计划用于站点的站点服务器和远程站点系统服务器（如承载站点数据库的服务器）满足所有必备项配置。 文档库中的下列主题可有所帮助：  

-   [Configuration Manager 支持的配置](../../../../core/plan-design/configs/supported-configurations.md)  
-   [先决条件检查程序](prerequisite-checker.md)  

##  <a name="clients-for-additional-operating-systems"></a><a name="bkmk_Addclients"></a> 其他操作系统的客户端  
可从 Microsoft 下载中心为以下操作系统下载 Configuration Manager 的客户端软件：  

- macOS (Apple)
- UNIX
- Linux

使用以下链接下载所使用的 Configuration Manager 版本的客户端：  

- [Microsoft Endpoint Configuration Manager - macOS 客户端（64 位）](https://www.microsoft.com/download/details.aspx?id=100850)

- [适用于其他操作系统的 Microsoft Configuration Manager 客户端](https://www.microsoft.com/download/details.aspx?id=47719)

##  <a name="usage-data-levels-and-settings"></a><a name="bkmk_usage"></a> 使用情况的数据级别和设置  
安装第一个 Configuration Manager 站点时，Configuration Manager 会在站点服务器上自动安装和配置新站点系统角色“服务连接点”  。 服务连接点具有以下默认设置：  

-   “联机”  模式（也提供脱机模式）  
-   数据收集级别为“增强”  （也提供“基本”和“完整”这两个数据收集级别）  

当服务连接点站点系统角色处于联机状态时，Microsoft 可通过 Internet 自动收集诊断和使用情况信息。 收集的信息可帮助我们：  

-   识别和解决问题  
-   改进我们的产品和服务  
-   标识适用于所使用的 Configuration Manager 版本的 Configuration Manager 更新  

### <a name="levels-of-data-collection"></a>数据收集级别  
数据收集包括以下三个级别：

-   “基本”  包括有关安装和升级的数据，如站点的数目和启用的 Configuration Manager 功能。 不会传输任何个人身份信息。  

-   “增强”  包括“基本”级别设置中的数据，并传输有关层次结构、每个功能的使用方式（频率和持续时间）的数据以及增强的诊断信息（如出现系统或应用故障时，服务器的内存状态）。 不会传输任何个人身份数据。  

-   “完整”  包括“基本”和“增强”级别设置中的数据，并且还将发送高级诊断信息，如系统文件和内存快照。 此选项可能包括个人身份信息，但我们不会使用这些信息来确定你的身份或联系你，或定向发送广告。  

有关详细信息（包括各级别所收集详情的披露），请参阅 [Configuration Manager 的诊断和使用情况数据](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)。  

若要在线查看 Configuration Manager 隐私声明，请转到 [https://go.microsoft.com/fwlink/?LinkID=626527](https://go.microsoft.com/fwlink/?LinkID=626527)。
