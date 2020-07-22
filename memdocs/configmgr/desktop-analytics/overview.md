---
title: 桌面分析
titleSuffix: Configuration Manager
description: 与 Configuration Manager 集成的桌面分析服务的概述。
ms.date: 06/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 09f829bd1695426211ff94381a63b8f23d1b4fe8
ms.sourcegitcommit: 86c2c438fd2d87f775f23a7302794565f6800cdb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86411008"
---
# <a name="what-is-desktop-analytics"></a>什么是桌面分析？

桌面分析是一项基于云的服务，可与 Configuration Manager 集成。 该服务为你提供见解和情报，让你在了解更多信息的情况下决定 Windows 客户端的更新是否就绪。 它将组织中的数据与从数百万台连接到 Microsoft 云服务的设备中聚合得到的数据进行组合。

结合使用桌面分析和 Configuration Manager 来：  

- 创建一个清单，其中列出在你组织中运行的应用  

- 评估应用与最新 Windows 10 功能更新的兼容性  

- 确定兼容性问题，并接收根据云端数据见解给出的缓解建议  

- 创建表示跨最小设备集的整个应用程序驱动程序资产的试点组  

- 将 Windows 10 部署到试点和生产管理的设备  

![Azure 门户中的桌面分析主页的屏幕截图](media/portal-home.png)

以下视频录制的是 Ignite 2019 大会的一场研讨会，其中详细介绍了桌面分析：

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3085]

[使用桌面分析和 Configuration Manager 通过管理、维护和支持方面的数据驱动的见解来降低 Windows TCO](https://myignite.techcommunity.microsoft.com/sessions/81689?source=sessions)

请跳至 10:00 查看深度演示。

> [!Note]  
> 桌面分析是 Windows Analytics 的后继版本，它自 2020 年 1 月 31 日起停用。
>
> Windows Analytics 的功能都合并到桌面分析服务中。 桌面分析还与 Configuration Manager 紧密集成。 有关详细信息，请参阅 [Windows Analytics 客户的常见问题解答](faq.md#existing-windows-analytics-customers)。

## <a name="benefits"></a>好处

许多客户在获取并保持最新的 Windows 10 方面面临着挑战。 主要挑战是测试应用程序。 此过程通常需手动完成。 IT 管理员和应用程序所有者要不断分析现有应用程序 并解决出现的任何问题，这需要花费很长时间。

桌面分析提供了以下好处：

- **设备和软件清单**：关键因素（如应用和 Windows 版本）清单。  

- **试点识别**：识别覆盖最广泛因素的最小设备集。 它侧重于对 Windows 升级和更新的试点最为重要的因素。 确保试点更成功可以让你更快、更自信地在生产环境中广泛部署。  

- **问题识别**：使用聚合的市场数据以及环境中的数据，该服务可预测获取并保持 Windows 最新状态的潜在问题。 然后，它会建议可能的缓解措施。  

- **Configuration Manager 集成**：该服务云支持你现有的本地基础结构。 使用此数据和分析在设备上部署和管理 Windows。  

## <a name="prerequisites"></a>必备条件

若要使用桌面分析，请确保你的环境满足以下先决条件。

### <a name="technical"></a>技术条件

- 有效的全局 Azure 订阅，以及[全局管理员](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions)权限。 不支持 [Microsoft 帐户](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts)。  

    > [!IMPORTANT]
    > 桌面分析是 Azure 全球版中托管的一项 Windows 服务，它利用 Windows 诊断数据。 尽管桌面分析是适用于美国政府客户的 Azure 全球服务，但它不符合[美国政府社区合规性 (GCC)](https://docs.microsoft.com/office365/servicedescriptions/office-365-platform-service-description/office-365-us-government/gcc#us-government-community-compliance) 属性。 有关 Microsoft 产品和服务的符合性服务/产品列表，请参阅 [Microsoft 信任中心](https://docs.microsoft.com/microsoft-365/compliance/offering-home?view=o365-worldwide)。 桌面分析不适用于 GCC High 或美国国防部 (DOD) 客户。 不支持使用 Azure 政府订阅来托管桌面分析工作区。

    - 设置工作区的工作区所有者权限，以及以下角色 ：  

      - [**桌面分析管理员**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions)角色。

      - 资源组上的 [**Log Analytics 参与者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor)和[**用户访问管理员**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator)，可使用现有工作区或在现有资源组中创建新工作区。

      - 订阅上的[**所有者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner)或[**参与者**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor)和[**用户访问管理员**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator)权限，可在新资源组中创建工作区。  

    - 要在载入后访问门户，你需要：

      - 创建的 Log Analytics 工作区的[桌面分析管理员](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions)角色和[所有者](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner)或[参与者](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor)权限。

- 包含更新汇总 (4500571) 的 Configuration Manager 版本 1902 或更高版本。 有关详细信息，请参阅[更新 Configuration Manager](connect-configmgr.md#bkmk_hotfix)。  

    - Configuration Manager 中的[**完全权限管理员**](../core/understand/fundamentals-of-role-based-administration.md#bkmk_Planroles)角色  

    > [!NOTE]
    > 桌面分析支持多个 Configuration Manager 层次结构向一个 Azure AD 租户报告。<!-- 4814075 --> 如果你的环境中有多个层次结构，则有以下选项：
    >
    > - 使用不同的商业 ID 和 Azure AD 租户。
    > - 将这两个层次结构配置为使用相同的 商业 ID 来共享 Azure AD 租户和桌面分析实例。 使用[不同的应用](connect-configmgr.md#bkmk_connect)连接每个层次结构。 在断开层次结构的连接后，门户最长可能需要 30 天才能反映出更改。 

- 运行 Windows 7、Windows 8.1 或 Windows 10 的设备  

    - 安装最新更新。 有关详细信息，请参阅[更新设备](enroll-devices.md#update-devices)。  

    - 设备还需要具有包含更新汇总 (4500571) 的 Configuration Manager 客户端版本 1902 或更高版本。 有关详细信息，请参阅[更新 Configuration Manager](connect-configmgr.md#bkmk_hotfix)。  

    > [!Note]  
    > 桌面分析不支持以 Windows 10 长期服务频道 (LTSC) 为源或目标的升级。 有关详细信息，请参阅 [Windows 即服务概述](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel)。
    >
    > 桌面分析专门用于最大程度地支持就地升级方案。 如果需要进行重大更改（例如，从 32 位更改为 64 位体系结构），请使用映像方案。 桌面分析见解对于这些经典 OS 部署方案仍然有用，但你可以忽略特定于就地升级的指南。 有关详细信息，请参阅[使用 Configuration Manager 部署企业操作系统的方案](../osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems.md)。

- Windows 诊断数据。 有关详细信息，请参阅下列文章：  

    - [诊断数据级别](enable-data-sharing.md#diagnostic-data-levels)  

    - [桌面分析隐私](privacy.md)  

- 从设备到 Microsoft 公有云的网络连接。 有关详细信息，请参阅[如何启用数据分享](enable-data-sharing.md)  

> [!Important]
> Microsoft 坚定地承诺提供用于让你自己控制隐私的工具和资源。 因此，Microsoft 不会从位于欧洲国家/地区（EEA 和瑞士）的设备中收集以下数据：
>
> - 来自 Windows 8.1 设备的 Windows 诊断数据
> - Windows 7 的应用使用情况数据

### <a name="licensing-and-costs"></a>许可和成本

- 一个有效的全球 Azure 订阅。

    > [!NOTE]
    > Configuration Manager 的大多数等效订阅还包括 Azure AD。 有关示例，请参阅 [Microsoft 365 计划](https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans)和[企业移动性 + 安全性授权](https://www.microsoft.com/licensing/product-licensing/enterprise-mobility-security)。

- 注册到桌面分析的设备需要有效的 Configuration Manager 许可证。 有关详细信息，请参阅 [Configuration Manager 授权](../core/understand/product-and-licensing-faq.md)。

- 设备用户需要以下许可证之一：

  - Windows 10 企业版 E3 或 E5（包含在 Microsoft 365 F3、E3 或 E5 中）

  - Windows 10 教育版 A3 或 A5（包含在 Microsoft 365 A3 或 A5 中）

  - Windows 虚拟桌面访问 E3 或 E5  

> [!NOTE]
> 除了许可订阅的成本之外，在 Azure Log Analytics 内使用桌面分析无需额外费用。 桌面分析引入的数据类型无需任何 Log Analytics 数据引入和保留费用。 作为非计费数据类型，此数据也不受任何 Log Analytics 每日数据引入上限的限制。 有关详细信息，请参阅 [Log Analytics 使用情况和成本](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage)。

## <a name="next-steps"></a>后续步骤

以下教程提供了有关桌面分析和 Configuration Manager 入门的分步指南：
  
> [!div class="nextstepaction"]
> [将 Windows 10 部署到试点](tutorial-windows10.md)
