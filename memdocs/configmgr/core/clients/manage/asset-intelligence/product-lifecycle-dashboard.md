---
title: 产品生命周期仪表板
titleSuffix: Configuration Manager
description: 通过 Configuration Manager 中的产品生命周期仪表板查看 Microsoft 生命周期策略。
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 178331865c8f3efd660e4a0037674eed3621fe6b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695165"
---
# <a name="manage-microsoft-lifecycle-policy-with-configuration-manager"></a>使用 Configuration Manager 管理 Microsoft 生命周期策略

适用范围：  Configuration Manager (Current Branch)

从版本 1806 开始，可以使用 Configuration Manager 产品生命周期仪表板来查看 Microsoft 生命周期策略。 该仪表板显示 Microsoft 产品（安装在由 Configuration Manager 托管的设备上）的 Microsoft 生命周期策略的状态。 它还提供有关环境中 Microsoft 产品的信息、可支持性状态以及支持结束日期。 使用仪表板了解对每个产品的支持的可用性。 这些信息有助于规划在到达当前支持结束日期之前，何时更新使用的 Microsoft 产品。  

有关详细信息，请参阅 [Microsoft 生命周期策略](https://support.microsoft.com/lifecycle)。

自版本 1810 起，仪表板包含 System Center 2012 Configuration Manager 及更高版本的信息。<!--1358702-->  



## <a name="prerequisites"></a>必备条件 

 若要查看产品生命周期仪表板中的数据，需要以下组件：  

- 必须在运行 Configuration Manager 控制台的计算机上安装 Internet Explorer 9 或更高版本。  

- 必须安装和配置服务连接点角色。 若要在此仪表板上获取数据更新，服务连接点必须处于联机状态，或必须定期同步（如果处于脱机状态的话）。 有关详细信息，请参阅[关于服务连接点](../../../servers/deploy/configure/about-the-service-connection-point.md)。

- 仪表板中的超链接功能需要一个 Reporting Services 点。 仪表板链接到 SQL Server Reporting Services (SSRS) 报表。 有关详细信息，请参阅[报表简介](../../../servers/manage/introduction-to-reporting.md)。  

- 必须配置并同步资产智能同步点。 该仪表板使用资产智能目录作为产品标题的元数据。 元数据将与层次结构中的清单数据进行比较。 有关详细信息，请参阅[在 Configuration Manager 中配置资产智能](configuring-asset-intelligence.md)。  
  - 如果是首次配置资产智能服务点，请确保[启用资产智能硬件清单类](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence)。 生命周期仪表板的内容取决于这些资产智能硬件清单类。 在客户端扫描并返回硬件清单后，仪表板才会显示数据。  
  - 要查看有关此仪表板中扩展安全更新 (ESU) 的信息，请启用硬件清单类“软件授权产品 - 资产智能 (SoftwareLicensingProduct)”  。 有关详细信息，请参阅[启用资产智能硬件清单类](configuring-asset-intelligence.md#BKMK_EnableAssetIntelligence)。 <!--4962901-->



## <a name="use-the-product-lifecycle-dashboard"></a>使用产品生命周期仪表板

根据站点从托管设备中收集的清单数据，仪表板将显示有关所有当前产品的信息。 但是，显示的有关操作系统和 SQL Server 的信息仅限于以下版本：

- Windows Server 2008 及更高版本
- Windows XP 及更高版本
- SQL Server 2008 及更高版本

若要访问 Configuration Manager 控制台中的生命周期仪表板，请转到“资产和符合性”工作区，展开“资产智能”并选择“产品生命周期”节点    。

> [!NOTE]  
> 仪表板中的数据基于 Configuration Manager 控制台连接到的站点。 如果控制台连接到顶层站点，你会看到整个层次结构的数据。 当连接到子主站点时，只显示来自该站点的数据。

### <a name="product-lifecycle-dashboard"></a>产品生命周期仪表板

![控制台中的产品生命周期仪表板的屏幕截图](media/product-lifecycle-dashboard.png)

通过从“产品类别”列表中选择以下选项之一来更改视图：   
- **全部**：同时查看所有产品  
- **Windows 客户端**：查看 Windows 客户端操作系统版本  
- **Windows Server**：查看 Windows Server 操作系统版本  
- **数据库**：查看 SQL Server 版本  
- **Configuration Manager**：从版本 1810 开始，查看 Configuration Manager 版本 
- **Microsoft Office**：自版本 1902 起，可查看已安装的 Office 2003 至 Office 2016 版本的信息 <!--3556026-->

该仪表板具有以下磁贴：  

- **已过期的前五大产品**：此磁贴是一个整合的数据视图，显示在环境中找到的已过期的产品。 此图显示与操作系统及 SQL Server 产品的支持生命周期相比较已过期的已安装软件。  

- **即将过期的前五大产品**：此磁贴是一个整合的数据视图，显示在环境中找到的即将在 18 个月内过期的产品。 此图显示与操作系统及 SQL Server 产品的支持生命周期相比较，将在 18 个月内过期的已安装软件。  

- **已安装产品的生命周期数据**：通过此磁贴可大致了解产品从支持到过期状态的转换过程。 该图表详细介绍了在其中安装产品的客户端数量、支持可用性状态，并提供了一个链接，用于详细了解要执行的后续步骤。 图表中包含以下信息：     
    - 剩余支持时间
    - 环境中的数量 
    - 主流支持结束日期
    - 延长的支持结束日期
    - 后续步骤  

> [!IMPORTANT]  
> 为方便起见，我们提供了此仪表板中显示的信息，并且仅供公司内部使用。 不应仅依赖此信息来确认符合性。 请务必验证提供过来的信息的准确性，并通过访问 [Microsoft 生命周期策略](https://support.microsoft.com/lifecycle)来验证支持信息的可用性。  



## <a name="reporting"></a>报表

其他报表也同样可用。 在 Configuration Manager 控制台中，转到“监视”工作区，展开“报表”并展开“报表”节点    。 在“资产智能”类别下添加了以下新报表：   

- **生命周期 01A - 具有特定软件产品的计算机**：查看检测到指定产品的计算机列表。  

- **生命周期 02A - 组织中具有已过期产品的计算机列表**：查看具有已过期产品的计算机。 可以按产品名称筛选此报表。

- **生命周期 03A - 组织中发现的已过期产品列表**：查看环境中生命周期已过期的产品的详细信息。  

- **生命周期 04A - 产品生命周期总体概览**：查看产品生命周期列表。 按产品名称和有效期对列表进行筛选。  

- **生命周期 05A - 产品生命周期仪表板**：从版本 1810 开始，此报表包含与控制台内仪表板类似的信息。 选择一个类别以查看环境中的产品数量以及剩余支持的天数。  

有关详细信息，请参阅[报告列表](../../../servers/manage/list-of-reports.md#asset-intelligence)。<!--SCCMDocs issue 997-->  
