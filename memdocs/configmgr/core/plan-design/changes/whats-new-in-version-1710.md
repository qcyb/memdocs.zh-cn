---
title: 新版本 1710 |Microsoft Docs
titleSuffix: Configuration Manager
description: 获取有关 Configuration Manager 版本 1710 中引入的更改和新功能的详细信息。
ms.date: 01/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc6c3e5f-b9e2-400e-9d9d-446ff93c520c
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c541c257d885ee5cba9e174a86a6859b078c8594
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702405"
---
# <a name="what39s-new-in-version-1710-of-configuration-manager"></a>Configuration Manager 版本 1710 中的新增功能

适用范围：  Configuration Manager (Current Branch)

Configuration Manager Current Branch 的更新 1710 作为控制台内更新提供，用于运行版本 1610、1702 或 1706 的以前安装的站点。

除了新增功能外，这一版还有其他变化（如缺陷修复）。 有关详细信息，请参阅 [Configuration Manager Current Branch（版本 1710）的更改摘要](https://support.microsoft.com/help/4056470/summary-of-changes-in-system-center-configuration-manager-current-bran)。

此外，现在还可以获取这一版的以下附加更新：
- [Configuration Manager Current Branch（版本 1710）更新汇总](https://support.microsoft.com/help/4057517/update-rollup-for-system-center-configuration-manager-current-branch-v)
- [Configuration Manager Current Branch（版本 1710）更新汇总 2](https://support.microsoft.com/en-us/help/4086143/update-rollup-2-for-system-center-configuration-manager-current-branch)

> [!TIP]  
> 若要安装新站点，必须使用 Configuration Manager 的基准版本。  
>
> 了解详细信息：    
> - [安装新站点](../../servers/deploy/install/installing-sites.md)  
> - [在站点上安装更新](../../servers/manage/updates.md)  
> - [基准和更新版本](../../servers/manage/updates.md#bkmk_Baselines)

以下各节提供有关 Configuration Manager 版本 1710 中引入的更改和新功能的详细信息。  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1710 drops support for the following products:
-->


## <a name="site-infrastructure"></a>站点基础结构

### <a name="updates-for-peer-cache-----sms500850---"></a>对等缓存更新  <!-- sms500850 -->
从这个版本开始，对等缓存不再属于预发行功能。  此版本中没有引入对等缓存的其他更改。 有关详细信息，请参阅[用于 Configuration Manager 客户端的对等缓存](../hierarchy/client-peer-cache.md)。

### <a name="cloud-distribution-point-support-for-azure-government-cloud------sms491428---"></a>对 Azure 政府云的云分发点支持   <!-- sms491428 -->
现在可以在 Azure 政府云中使用[基于云的分发点](../hierarchy/use-a-cloud-based-distribution-point.md)。   

### <a name="inventory-default-unit-revision----sms503697---"></a>清单默认单位修订 <!-- sms503697 -->
由于设备现在包含的硬件大小单位为 GB、TB 和更大的规模，此版本将很多视图中使用的默认单位 (SMS_Units) 从 MB 更改为了 GB。 例如，v_gs_LogicalDisk.FreeSpace 值现在将以 GB 为单位进行报告。


<!-- ## Migration  -->


## <a name="client-management"></a>客户端管理

### <a name="co-management-for-windows-10-devices"></a>适用于 Windows 10 设备的共同管理    
<!-- 1350871 -->
在以前的 Windows 10 更新中，已经可以将 Windows 10 设备同时联接到本地 Active Directory (AD) 和基于云的 Azure AD（混合 Azure AD）。 从 Configuration Manager 1710 版本开始，共同管理利用此项改进来使你能够使用 Configuration Manager 和 Intune 来同时管理 Windows 10 设备版本 1709（也称为 Fall Creators Update）。 它是一种解决方案，在传统管理与现代管理之间架起一座桥梁，为你提供利用分阶段的方法实现转换的途径。 有关详细信息，请参阅[适用于 Windows 10 设备的共同管理](../../../comanage/overview.md)。

### <a name="restart-computers-from-the-configuration-manager-console-----1356283---"></a>从 Configuration Manager 控制台重启计算机  <!-- 1356283 -->
从此版本开始，用户可以使用 Configuration Manager 控制台标识需要重启的客户端设备，然后使用客户端通知操作来重启它们。

请参阅[如何管理客户端](../../clients/manage/manage-clients.md#restart-clients)


<!-- ## Compliance settings -->


## <a name="application-management"></a>应用程序管理
### <a name="improvements-for-run-scripts------1236459---"></a>对“运行脚本”的改进   <!-- 1236459 -->
此版本中将多项改进引入 **“运行脚本”** 功能，可将 PowerShell 脚本部署为在托管设备上运行。 1706 版本首次引入了此功能。

改进包括：
- 采用安全作用域帮助控制使用“运行脚本”的人员
- 实时监视你运行的脚本
- 脚本参数显示在“创建脚本”向导、支持验证中，并标识为强制或可选。

有关使用“运行脚本”的详细信息，请参阅[创建和运行脚本](../../../apps/deploy-use/create-deploy-scripts.md)。

### <a name="new-mobile-application-management-policy-settings"></a>新移动应用程序管理策略设置
<!-- 1324760 -->
以下设置已添加到移动应用程序管理策略设置：
- **禁用联系人同步**：阻止应用将数据保存到设备上的本机“联系人”应用。
- **禁用打印**：阻止应用打印工作或学校数据。

### <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>软件中心不会再使大于 250 x 250 的图标失真  
<!-- 1356194 -->

在此版本中，软件中心不会再使大于 250 x 250 的图标失真。 软件中心曾使此类图标看起来很模糊。 现在图标的像素大小最大可设置为 512 x 512，并在显示时不会失真。

若要在软件中心添加你的应用图标，请参阅[创建应用程序](../../../apps/deploy-use/create-applications.md)。

## <a name="operating-system-deployment"></a>操作系统部署
 > [!TIP]   
 > <!-- 1354281 -->
 > 从 Windows 10 版本 1709（也称为 Fall Creators Update）开始，Windows Media 包括多个版本。 在配置用于使用操作系统升级包或操作系统映像的任务序列时，请务必选择[支持供 Configuration Manager 使用的版本](../configs/support-for-windows-10.md#windows-10-as-a-client)。

### <a name="add-child-task-sequences-to-a-task-sequence"></a>将子任务序列添加到任务序列
<!-- 1261338 -->

可以添加一个运行其他任务序列的新任务序列步骤，该步骤在任务序列之间创建父/子关系。 这允许创建更多可重复使用的模块式任务序列。  

若要了解有关子任务序列的详细信息，请参阅[子任务序列](../../../osd/understand/task-sequence-steps.md#child-task-sequence)。

## <a name="software-center-customization"></a>软件中心自定义
<!-- 1351224 -->
可以添加企业品牌元素，并在“软件中心”上指定选项卡的可见性。 可以添加“软件中心”特定公司名称、设置“软件中心”配置颜色主题、设置公司徽标，并设置客户端设备的可见选项卡。

有关详细信息，请参阅[规划和配置应用程序管理](../../../apps/plan-design/plan-for-and-configure-application-management.md)。

## <a name="software-updates"></a>软件更新

### <a name="surface-driver-updates-----1098490---"></a>Surface 驱动程序更新  <!-- 1098490 -->
从此版本开始，管理 Surface 驱动程序更新不再是预发行功能。  


## <a name="reporting"></a>报表

### <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>限制 Windows 10 增强数据只发送与 Windows Analytics 设备运行状况相关的数据
<!-- 1356148 -->

现在可以将 Windows 10 诊断数据收集级别设置为“增强(受限)”  。 该设置使你能够在环境中获得对设备的可操作见解，而无需设备通过 Windows 10 版本 1709 或更高版本报告“增强”  级别的所有数据。

<!-- ## Inventory  -->


## <a name="mobile-device-management"></a>移动设备管理

### <a name="actions-for-non-compliance"></a>针对非符合性的操作 
<!--1321366 -->    
现在可配置一系列以时间排序的应用于不符合设备的操作。 例如，可通过电子邮件通知不符合设备的最终用户，或将这些设备标记为不符合。

### <a name="windows-10-arm64-device-support"></a>Windows 10 ARM64 设备支持
<!-- 1355000 -->

运行 Windows 10 的 ARM64 设备支持混合移动设备管理 (MDM) 方案（当这些设备可用时）。

### <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>改进了 Configuration Manager 控制台中的 VPN 配置文件体验 
<!-- 1318232 -->

在此版本中，我们更新了 VPN 配置文件向导和属性页，以显示选定平台相应的设置：


- 每个平台均有其自己的工作流，这意味着新的 VPN 配置文件仅包含平台支持的设置。
- 如今，“支持的平台”页在“常规”页后显示   。  现在于设置属性值之前选择平台。
- 如果将平台设置为“Android”、“Android for Work”或“Windows Phone 8.1”，则不需要“支持的平台”页，该页也不会显示     。
- 基于 Configuration Manager 客户端的工作流已与基于混合移动设备 (MDM) 客户端的 Windows 10 工作流相结合，它们支持相同的设置。
- 每个平台工作流仅包含适用于该工作流的设置。  例如，Android 工作流包含适用于 Android 的设置；Android 工作流中将不再显示适用于 iOS 或 Windows 10 移动版的设置。
- “自动 VPN”页已过时且已删除。

这些更改适用于新的 VPN 配置文件。  

为把兼容性风险降至最低，现有的 VPN 配置文件保持不变。  编辑现有的配置文件时，设置将以创建该配置文件时的形式显示。  

有关详细信息，请参阅[移动设备上的 VPN 配置文件](../../../protect/deploy-use/vpn-profiles.md)。

### <a name="limited-support-for-cryptography-next-generation-cng-certificates----1356191---"></a>提供一定程度的加密支持：下一代 (CNG) 证书 <!-- 1356191 -->

Configuration Manager 提供一定程度的加密支持：下一代 (CNG) 证书. Configuration Manager 客户端可以通过 CNG 密钥存储提供者 (KSP) 中的私钥使用 PKI 客户端身份验证证书。 通过 KSP 支持，Configuration Manager 客户端可支持基于硬件的私钥，如用于 PKI 客户端身份验证证书的 TPM KSP。

有关详细信息，请参阅 [CNG 证书概述](../network/cng-certificates-overview.md)。

## <a name="protect-devices"></a>保护设备

### <a name="create-and-deploy-exploit-guard-policies"></a>创建和部署攻击防护策略
<!-- 1355468 -->

可以[创建和部署策略](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md)以管理 Windows Defender 攻击防护的全部四个组成部分，包括攻击面减少、受控文件夹访问权限、攻击防护和网络保护。

### <a name="create-and-deploy-windows-defender-application-guard-policy"></a>创建和部署 Windows Defender 应用程序防护策略
<!-- 1351960 -->

可以使用 Configuration Manager Endpoint Protection [创建和部署 Windows Defender 应用程序防护策略](../../../protect/deploy-use/create-deploy-application-guard-policy.md)。

### <a name="device-guard-policy-changes"></a>设备防护策略更改
<!-- 1355092 -->
下面是三个与设备防护策略相关的更改：

- 设备防护策略已被重命名为 Windows Defender 应用程序控制策略。 因此，举例来说，“创建设备防护策略”向导  现命名为“创建 Windows Defender 应用程序控制策略”向导  。
- 使用 Windows 版本 1709 Fall Creators Update 的设备无需重启就能应用 Windows Defender 应用程序控制策略。 重新启动仍是默认设置，但你可以[关闭重启](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)。
- 可以[将设备设置为自动运行](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md)受 Intelligent Security Graph 信任的软件。





## <a name="next-steps"></a>后续步骤
准备好安装此版本时，请参阅 [Configuration Manager 的更新](../../servers/manage/updates.md)。
