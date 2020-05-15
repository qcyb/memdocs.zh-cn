---
title: 在桌面分析中注册设备
titleSuffix: Configuration Manager
description: 了解如何在桌面分析中注册设备。
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: acb8900a57408152133637ead3b8a0cf4732b4a7
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268719"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>如何在桌面分析中注册设备

[将 Configuration Manager 连接](connect-configmgr.md)到桌面分析时，可配置设置以将设备注册到桌面分析。 你可以随时更改这些设置。 还要确保设备处于最新状态。

## <a name="update-devices"></a>更新设备

桌面分析使用两个主要 Windows 组件：

- 兼容性组件  ：兼容性组件（评估程序  ）在 Windows 设备上运行诊断，以评估设备与最新版 Windows 10 的兼容性状态。

- “已连接的用户体验和遥测”服务  ：在 Windows 诊断数据启用后，“已连接的用户体验和遥测”服务 (DiagTrack  ) 收集系统、应用程序和驱动器数据。 Microsoft 会分析这些数据，并通过桌面分析将其共享给你。

安装这些组件的最新版本，以获取最佳桌面分析体验。

下表列出了每个组件在支持的 OS 版本上的更新：

| OS 版本 | 评估程序 | DiagTrack |
| --------------| ----------------------- | -------------------|
| Windows 10 1909 | 包含<sup>[注释 1](#bkmk_note1)</sup> | [最新累积更新](https://support.microsoft.com/help/4529964) |
| Windows 10 1903 | 包含 | [最新累积更新](https://support.microsoft.com/help/4498140) |
| Windows 10 1809 | 包含 | [最新累积更新](https://support.microsoft.com/help/4464619) |
| Windows 10 1803 | 包含 | [最新累积更新](https://support.microsoft.com/help/4099479) |
| Windows 10 1709 | 包含 | [最新累积更新](https://support.microsoft.com/help/4043454) |
| Windows 8.1 | [KB 2976978](https://support.microsoft.com/help/2976978)<sup>[注释 2](#bkmk_note2)</sup> | [最新每月汇总](https://support.microsoft.com/help/4009470) |
| Windows 7 SP1 | [KB 2952664](https://support.microsoft.com/help/2952664)<sup>[注释 3](#bkmk_note3)</sup> | [最新每月汇总](https://support.microsoft.com/help/4009469) |

> [!TIP]
> 使用 Configuration Manager 自动安装这些更新。 有关详细信息，请参阅[部署软件更新](../sum/deploy-use/deploy-software-updates.md)。
>
> 首次安装兼容性更新后，重新启动设备。

### <a name="note-1-windows-10"></a><a name="bkmk_note1"></a> 注释 1：Windows 10

虽然 Windows 10 默认包含这些组件，但 Windows 10 设备要求必须安装最新累积更新，才能获得完整的桌面分析功能。 例如，评估设备是否与最新 OS 版本兼容，以及获取有关部署和注册状态的准实时信息。

### <a name="note-2-windows-81"></a><a name="bkmk_note2"></a> 注释 2：Windows 8.1

Microsoft 会定期递增此组件的更新，但关联的 KB 数不会改变。 请确保始终拥有最新版本的更新。

此组件在加入 Windows 客户体验改善计划的 Windows 8.1 系统上运行诊断。 这些诊断帮助确定升级到 Windows 10 时是否可能存在兼容性问题。

### <a name="note-3-windows-7"></a><a name="bkmk_note3"></a> 注释 3：Windows 7

如果组织没有对 Windows 7 设备应用“每月质量汇总”更新，而是只应用了“仅安全”更新，那么你会在[取代 KB 2952664 的更新列表](https://www.catalog.update.microsoft.com/ScopedViewInline.aspx?updateid=ad3652cd-2689-4726-b3ef-b086ded23c7c)中发现一些“仅安全”更新。 可以安装这些较新的更新，而不是 KB 2952664。

> [!NOTE]
> 对于 Windows 8.1，Microsoft 只修订 KB 2976978，作为“每月质量汇总”更新的一部分。

## <a name="device-enrollment"></a>设备注册

桌面分析服务没有要安装的代理。 设备注册要求在想要该服务监控的设备上配置设置。 这些设置控制此设备应将其数据和其他配置选项发送到哪个桌面分析实例。

> [!Note]  
> 如果以前使用过 Windows Analytics，请为桌面分析使用相同的工作区。 需要将设备重新注册到以前在 Windows Analytics 中注册的桌面分析。
>
> 每个 Azure AD 租户只能有一个桌面分析工作区。 设备只能向一个工作区发送诊断数据。  

Configuration Manager 提供了管理这些设置并将其部署到客户端的集成体验。 为获得最佳体验，请使用 Configuration Manager。

将 Configuration Manager 连接到桌面分析时，可配置设置以注册设备。 有关详细信息，请参阅[如何将 Configuration Manager 与桌面分析连接](connect-configmgr.md#bkmk_connect)。

要更改这些设置，请按以下过程操作：

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure 服务”节点    。 选择“连接到桌面分析”，并在功能区中选择“属性”  。

2. 在“诊断数据”  页上，根据需要更改以下设置：  

    - **商业 ID**：此值应自动填充你组织的 ID。 如果未填充，请确保将代理服务器配置为允许所有必需的[终结点](enable-data-sharing.md#endpoints)，然后再继续。 也可以手动从[桌面分析门户](monitor-connection-health.md#bkmk_ViewCommercialID)中检索商业 ID。

    - **Windows 10 诊断数据级别**：有关详细信息，请参阅[诊断数据级别](enable-data-sharing.md#diagnostic-data-levels)。  

    - **允许诊断数据中含有设备名称**：有关详细信息，请参阅[设备名称](#device-name)。  

    对此页进行更改时，“可用功能”  页将显示桌面分析功能的预览，其中包含所选的诊断数据设置。  

3. 在“桌面分析连接”  页上，根据需要更改以下设置：

    - **显示名称**：桌面分析门户使用此名称显示此 Configuration Manager 连接。  

    - **目标集合**：此集合包括 Configuration Manager 使用你的商业 ID 和诊断数据设置配置的所有设备。 它是 Configuration Manager 连接到桌面分析服务的完整设备集。  

    - **目标集合中的设备使用经用户身份验证的代理进行出站通信**：默认情况下，此值为“否”  。 如果你的环境需要，请设置为“是”  。 有关详细信息，请参阅[代理服务器身份验证](enable-data-sharing.md#proxy-server-authentication)。

    - **选择要与桌面分析同步的特定集合**：选择“添加”  以包括“目标集合”  层次结构中的其他集合。 这些集合可在桌面分析门户中用于按照部署计划分组。 确保包括试点和试点排除集合。  <!-- 4097528 -->

        > [!IMPORTANT]
        > 这些集合在其成员身份更改时会继续同步。 例如，你的部署计划使用具有 Windows 7 成员身份规则的集合。 当这些设备升级到 Windows 10，且 Configuration Manager 评估集合成员身份时，这些设备将退出集合和部署计划。

### <a name="windows-settings"></a>Windows 设置

当 Configuration Manager 将设备注册到桌面分析时，它会设置 Windows 策略来为设备配置桌面分析。 在大多数情况下，仅使用 Configuration Manager 来配置这些设置。 也不要在域组策略对象中应用这些设置。

有关详细信息，请参阅[桌面分析的组策略设置](group-policy-settings.md)。

### <a name="device-name"></a>设备名称

自 Windows 10 版本 1803 起，默认不再收集设备名称。 使用诊断数据收集设备名称需要单独选择加入。 如果没有设备名称，则在评估升级到新版本 Windows 时，将更难识别需要关注的设备。

如果你不发送设备名称，它在桌面分析中显示为“未知”：

![显示“未知”名称的桌面分析设备列表](media/unknown-device-name.png)

Configuration Manager 设置中的一个选项可供桌面分析配置此选项：**允许诊断数据中含有设备名称**。 此 Configuration Manager 设置控制 [Windows 策略设置](group-policy-settings.md) AllowDeviceNameInTelemetry  。

### <a name="conflict-resolution"></a>冲突解决

一般情况下，使用 Configuration Manager 集合来定位桌面分析设置和注册。 使用直接成员身份或查询来包括或排除集合中的设备。 有关详细信息，请参阅[如何创建集合](../core/clients/manage/collections/create-collections.md)。

如果值尚不存在，Configuration Manager 仅配置 Windows 设置。 如果需要为唯一设备组配置不同的设置，可以使用[“组策略”](group-policy-settings.md)。 组策略定位的设置优先于 Configuration Manager 设置。

配置诊断数据级别时，请设置设备的上限。 默认情况下，在 Windows 10 版本 1803 及更高版本中，用户可以选择设置较低的级别。 你可以使用组策略设置“配置遥测选择使用设置用户界面”来控制此行为  。 有关详细信息，请参阅[桌面分析的组策略设置](group-policy-settings.md)。

### <a name="proxy-settings"></a>代理设置

如果组织使用代理服务器身份验证来访问 Internet，请务必正确配置它或你的设备。 有关详细信息，请参阅[代理服务器身份验证](enable-data-sharing.md#proxy-server-authentication)。

## <a name="next-steps"></a>后续步骤

转到下一篇文章，以便在桌面分析中创建部署计划。
> [!div class="nextstepaction"]
> [创建部署计划](create-deployment-plans.md)
