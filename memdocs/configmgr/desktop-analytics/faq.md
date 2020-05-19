---
title: 桌面分析常见问题解答
titleSuffix: Configuration Manager
description: 桌面分析常见问题解答。
ms.date: 02/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: fb217a1e1ddf114155e43e8edef0c1b34842db64
ms.sourcegitcommit: 7b224e138c0618e978be59832b3486f3745abacc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/13/2020
ms.locfileid: "83381513"
---
# <a name="desktop-analytics-faq"></a>桌面分析常见问题解答

## <a name="prerequisites"></a>必备条件

### <a name="can-i-use-cloud-enabled-analytics-with-intune-managed-devices"></a><a name="bkmk_intune"></a> 我可以在支持 Intune 的设备上使用支持云的分析吗？

目前不可以，但请参阅 Microsoft Ignite 2019 关于[见解驱动的设备管理](https://myignite.techcommunity.microsoft.com/sessions/81690?source=sessions)的公告。 此计划解决方案是设备运行状况和升级就绪情况的后续产品。

从桌面分析工作流受益的大部分客户都使用 Configuration Manager 部署 Windows。 我们知道 Intune 客户喜爱分析数据产生的额外见解，因此我们也正在努力寻找与他们共享见解的方法。

### <a name="its-been-over-72-hours-and-the-portal-is-still-processing-data-what-next"></a>已超过 72 小时了，门户仍在处理数据，接下来要做什么？

第一次设置桌面分析时，Configuration Manager 和桌面分析门户中的报表可能不会立即显示完整的数据。 此服务完成数据处理可能需要 2-3 天的时间。 若已超过 72 小时，而门户仍在处理数据，请按照以下步骤操作：

- 使用[连接运行状况仪表板](monitor-connection-health.md)确认是否已正确配置活动设备。 此仪表板不会实时更新。
- 请确保设备正在将诊断数据发送至桌面分析服务。 有关详细信息，请参阅[启用数据分享](enable-data-sharing.md)。
- 在 Azure AD 上预配 [Azure AD 应用程序](troubleshooting.md#bkmk_AzureADApps)。
- 查看最近 7 天内与组织关联的设备。 在[桌面分析门户](https://aka.ms/desktopanalytics)中，转到“连接的服务”窗格。 选择“注册设备”，然后选择“查看最新数据” 

  > [!IMPORTANT]
  > 桌面分析选项“查看最新数据”已弃用。 此操作将在桌面分析服务的未来版本中删除。 有关详细信息，请参阅[已弃用的功能](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)。<!--7080949-->  

若已正确配置设备，但工作区仍然未显示数据，请[联系 Microsoft 支持部门](https://support.microsoft.com/hub/4343728/support-for-business)。

## <a name="connect-configuration-manager"></a>连接 Configuration Manager

### <a name="can-i-change-the-target-or-additional-collections"></a>我能否更改目标集合或其他集合？

可以，请使用下列过程进行更改：

- 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure 服务”节点  。 打开与桌面分析服务关联的项的属性。

- 在 **“桌面分析连接”** 选项卡上，更改 **“目标集合”** ，或者管理其他集合。

<!-- 7130169 -->
> [!Note]
> 在附加集合的列表中添加的集合不要超过 20 个。 要注意每个集合中的设备总数。 始终包括[全局试点包含和排除集合](deploy-pilot.md#bkmk_GlobalPilot)。  

> [!IMPORTANT]  
> Configuration Manager 使用设置策略配置目标集合中的设备。 此策略包括允许设备向 Microsoft 发送数据的诊断数据设置。 更改目标集合无法撤销对于不再属于目标集合的设备的设置策略。 若不希望设备继续发送诊断数据，请[重新配置设备](account-close.md#reconfigure-clients)。

## <a name="windows-upgrade"></a>Windows 升级

### <a name="can-i-upgrade-windows-and-change-architecture"></a>我能否升级 Windows 并更改体系结构？

桌面分析专门用于最大程度地支持就地升级。 就地升级不支持从 32 位迁移到 64 位体系结构。 若需要在此方案中迁移计算机，请使用刷新方案。 桌面分析见解对于此方案仍然有用，但你可以忽略特定于升级的指南。

有关详细信息，请参阅[使用新版本的 Windows 刷新现有的计算机](../osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)。

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>升级 Windows 时，我能否从 BIOS 更改为 UEFI？

是。 有关详细信息，请参阅[进行就地升级时，从 BIOS 转换为 UEFI](../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#convert-from-bios-to-uefi-during-an-in-place-upgrade)。

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>我能否将桌面分析用于 Windows 10 LTSC？

桌面分析不支持 Windows 10 长期服务频道 (LTSC) 设备。 有关详细信息，请参阅 [Windows 即服务概述](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel)。

### <a name="can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal"></a>我能否减少在桌面分析门户中刷新数据所需的时间？

桌面分析门户有两种数据类型：管理员数据和诊断数据。 打开数据流通浮出控件，并选择“应用更改”，可按需刷新管理员数据。 此操作会立即触发对工作区中任何挂起的管理员更改的一次性刷新。 更改会进行传播，通常会在 15-60 分钟内可用。 具体取决于工作区的大小以及挂起的更改的范围。 最多可在 24 小时内请求六次按需数据刷新。

即使未请求按需数据刷新，所有数据每天也会自动更新一次。 无法触发对诊断数据的按需刷新。 有关桌面分析中各种数据类型的详细信息，请参阅[数据延迟](troubleshooting.md#data-latency)。

## <a name="privacy"></a>隐私

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>若没有客户端直接连接到 Microsoft 数据管理服务，能否使用桌面分析？

不能，整个服务由 Windows 诊断数据提供支持，而此数据需要设备进行直接连接。

### <a name="can-i-choose-the-data-center-location"></a>我能否选择数据中心位置？

对于 Azure 日志分析：可以在设置桌面分析并创建日志分析工作区时进行选择。

对于 Microsoft 数据管理服务和 Azure 存储分析：不可以，这两个服务的托管位置是在美国。

### <a name="where-is-my-organizations-data-stored"></a>组织的数据存储在何处？

来自你的计算机的 Windows 诊断数据会被加密并发送到 Microsoft 托管的安全数据中心（位于美国）进行处理。 Microsoft 通过 Azure 门户中的桌面分析解决方案提供对桌面分析相关数据的分析。 大多数的[日志分析可用地区](https://azure.microsoft.com/global-infrastructure/services/?products=monitor&regions=all)都支持桌面分析。 若选择国际 Azure 区域，你的诊断数据仍会发送到位于美国的 Microsoft 安全数据中心进行处理。

## <a name="existing-windows-analytics-customers"></a>现有 Windows Analytics 客户

> [!Important]  
> Windows Analytics 服务自 2020 年 1 月 31 日起停用。
>
> 有关详细信息，请参阅 [KB 4521815：Windows Analytics 将于 2020 年 1 月 31 日停用](https://support.microsoft.com/help/4521815/windows-analytics-retirement)。

### <a name="can-i-use-update-compliance-together-with-desktop-analytics"></a>我能否将更新符合性和桌面分析一起使用？

是。 若目前在 Azure 门户中使用了[更新符合性](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started)，现在及 2020 年 1 月以后可以继续使用。

有关详细信息，请参阅 [KB 4521815：Windows Analytics 将于 2020 年 1 月 31 日停用](https://support.microsoft.com/help/4521815/windows-analytics-retirement)。

### <a name="are-there-any-windows-analytics-features-that-arent-available-in-desktop-analytics"></a>桌面分析是否无法提供某些 Windows Analytics 功能？

<!-- 3616924 -->
是的，以下 Windows Analytics 功能已停用，或尚未在桌面分析中提供：

#### <a name="general"></a>常规

- 支持不需要 Configuration Manager 的方案。 如 [Intune 支持](#bkmk_intune)。
- 任何有效的 Windows 许可证与 E3、E5 的许可先决条件
- 每个 Azure AD 租户支持多个工作区
- 能够运行自定义查询并导出原始解决方案数据
- 自定义报表的数据模型文档

#### <a name="upgrade-readiness"></a>Upgrade Readiness

- Internet Explorer 站点发现数据
- Office 加载项见解（现在[可从 Configuration Manager 获取](#bkmk_office)）
- 反馈中心见解

#### <a name="update-compliance"></a>更新符合性

- 支持适用于企业的 Windows 更新
- 传递优化见解
- 支持 Windows 10 长期服务渠道 (LTSC)
- Windows 预览体验报告
- Windows Defender 状态

> [!Note]
> 所有现有的更新符合性功能（包括桌面分析未提供的功能）在 Azure 门户中的[更新符合性](/windows/deployment/update/update-compliance-get-started)解决方案中继续提供。

#### <a name="device-health"></a>设备运行状况

- 驱动程序运行状况
- 应用运行状况（在部署计划之外）
- 频繁崩溃的设备或驱动程序引发的故障
- Windows 登录运行状况
- Windows 信息保护
- 对 Windows Server 的支持

## <a name="other"></a>其他

### <a name="can-i-use-desktop-analytics-for-my-office-365-proplus-upgrades"></a><a name="bkmk_office"></a> 我能否将桌面分析用于 Office 365 ProPlus 升级？

不能，桌面分析主要针对 Windows。 Microsoft 与许多客户密切合作开发出了桌面分析。 客户反馈表示，桌面分析提高了他们的能力，使他们能够自信地管理 Windows 部署。 此外，他们还表示希望提高 [Office 365 ProPlus 就绪情况](../sum/deploy-use/office-365-dashboard.md#bkmk_o365_readiness)与 Configuration Manager 和 Intune 中的 Office 管理工具的集成程度。 在重点关注桌面分析的 Windows 方案的同时，Microsoft 会继续向这些领域投资。

### <a name="how-can-i-provide-feedback-about-desktop-analytics"></a>如何提供关于桌面分析的反馈？

选择门户顶部的“发送笑脸”图标，可分享你对于桌面分析的反馈。 请在提交时附带屏幕截图，以便于 Microsoft 理解你的反馈。 还可以提交产品建议，以及在 [UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas?category_id=366805) 上为其他想法点赞。

> [!Note]
> 切勿通过“发送笑脸”或 UserVoice 分享私人信息。 此处的私人信息包括租户 ID 或商业 ID。Microsoft 无法通过“发送笑脸”或 UserVoice 渠道提供支持。 要获得桌面分析工作区方面的帮助，请在导航菜单中选择“帮助和支持”链接打开支持票证。
