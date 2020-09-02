---
title: 在 Microsoft Intune 中使用终结点安全功能管理设备 | Microsoft Docs
description: 了解安全管理员如何在 Microsoft Endpoint Manager 中使用终结点安全性节点查看设备并对其进行管理。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 98b1380254a784dfe8939c607ab574f7bdaa8752
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914984"
---
# <a name="manage-devices-with-endpoint-security-in-microsoft-intune"></a>在 Microsoft Intune 中使用终结点安全功能管理设备

安全管理员可通过 Microsoft Endpoint Manager 管理中心内的“所有设备”视图查看设备并对其进行管理。 此视图会显示 Azure Active Directory (Azure AD) 中所有设备的列表。 其中包括 Intune 托管的设备、Configuration Manager 托管的设备，以及由 Intune 和 Configuration Manager [共同管理](/configmgr/comanage/overview)的设备。 与 Azure AD 集成时后，设备可位于云中和本地基础结构中。

 要查找此视图，请打开 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，然后选择“终结点安全” > “所有设备” 。

初始的“所有设备”视图显示了你的设备，还包含各设备的下述关键信息：

- 设备的托管方式
- 符合性状态
- 操作系统详细信息
- 设备的上次签入时间
- 及其他信息

![管理中心内的“所有设备”视图](./media/endpoint-security-manage-devices/all-device-view.png)

查看设备详细信息时，可选择一个设备来深入了解其详细信息。

## <a name="available-details-by-management-type"></a>按管理类型列出的可用详细信息

在 Microsoft Endpoint Manager 管理中心查看设备时，请考虑设备的托管方式。 管理源会影响在管理中心显示的信息以及可用于管理设备的操作。

请考虑下列字段：

- **托管方式** - 此列可确定设备的托管方式。 托管方式选项包括：

  - **MDM** - 这些设备由 Intune 托管。 符合性数据由 Intune 收集并报告给管理中心。

  - **ConfigMgr** - 使用“租户附加”添加用 Configuration Manager 管理的设备时，这些设备将在 Microsoft Endpoint Manager 管理中心显示。 要托管设备，设备必须运行 Configuration Manager 客户端并符合以下条件：

    - 在工作组中（已加入 AAD，否则）
    - 已加入域
    - 已加入混合 AAD（已加入 AD 和 AAD）

    通过 Configuration Manager 管理的设备的符合性状态在 Microsoft Endpoint Manager 管理中心内不可见。

    有关详细信息，请参阅 Configuration Manager 文档中的[启用租户附加](/configmgr/tenant-attach/device-sync-actions)。

  - **MDM/ConfigMgr 代理** - 这些设备由 Intune 和 Configuration Manager 共同管理。

    通过共同管理，可[选择不同的共同管理工作负载](/configmgr/comanage/how-to-switch-workloads)来确定由 Configuration Manager 或 Intune 管理哪些方面。 这些选项将影响设备应用的策略，还将影响如何向管理中心报告符合性数据。

    例如，可使用 Intune 配置防病毒、防火墙和加密方面的策略。 这些策略类型被视为 Endpoint Protection 的策略。 要让共同管理的设备使用 Intune 策略而不是 Configuration Manager 策略，请将 Endpoint Protection 的共同管理滑块设置为“Intune”或“试点 Intune” 。 如果将滑块设置为 Configuration Manager，则设备将改为使用 Configuration Manager 的策略和设置。

- **符合性**：符合性是根据分配给设备的符合性策略进行评估的。 这些策略的来源以及控制台中显示的信息由设备的托管方式（Intune、Configuration Manager 或共同管理）决定。 要使共同管理的设备报告符合性状态，请将设备符合性的共同管理滑块设置为“Intune”或“试点 Intune”。  

  将符合性报告给设备的管理中心后，可深入查看更多详细信息。 如果设备不符合条件，可深入查看其详细信息，了解该设备不符合哪些策略。 该信息有助于调查设备并让设备达到符合条件。

- **上次签入时间**：此字段确定设备上次报告其状态的时间。

## <a name="review-a-devices-policy"></a>查看设备策略

查看设备列表时，若需深入了解某设备的详细信息，请选择该设备并打开其“概述”页面。

在设备的“概述”页面中，可选择“终结点安全配置”，查看应用于该设备的终结点安全策略。 可查看由 MDM 和 Intune 管理的设备的策略详细信息。

![查看终结点安全策略详细信息](./media/endpoint-security-manage-devices/view-policy-details.png)

由 Configuration Manager 管理的设备不显示策略详细信息。 要查看这些设备的其他信息，请使用 Configuration Manager 控制台。

## <a name="remote-actions-for-devices"></a>适用于设备的远程操作

远程操作是可通过 Microsoft Endpoint Manager 管理中心启动或应用到设备的操作。 查看设备的详细信息时，可访问适用于设备的远程操作。

这些远程操作显示在设备“概述”页面的顶部。 通过选择右侧的省略号，可看到由于屏幕空间限制而隐藏的操作：

![查看其他操作](./media/endpoint-security-manage-devices/view-additional-actions.png)

可用的远程操作取决于设备的托管方式：

- **Intune**：适用于设备平台的所有 [Intune 远程操作](../remote-actions/device-management.md)都可用。  
- **Configuration Manager**：可使用以下 Configuration Manager 操作：

  - 同步计算机策略
  - 同步用户策略
  - 应用评估周期

- 共同管理：可访问 Intune 远程操作和 Configuration Manager 操作。

某些 Intune 远程操作有助于保护设备或其上可能存在的数据。 可通过远程操作：

- 锁定设备
- 重置设备
- 删除公司数据
- 在计划运行之外扫描恶意软件
- 轮换 BitLocker 密钥

下面是安全管理员需要的 Intune 远程操作，它们在[完整列表](../remote-actions/device-inventory.md#view-the-device-details)列出。 并非所有操作都适用于所有设备平台。 通过下列链接，可查看提供每项操作深度详细信息的内容。

- [同步设备](../remote-actions/device-sync.md) - 使设备立即使用 Intune 签入。 设备签入时，会收到已分配给它的所有挂起的操作或策略。  

- [重启](../remote-actions/device-restart.md) - 强制 Windows 10 设备在 5 分钟内重启。 设备所有者不自动收到重启通知，且可能丢失工作内容。

- [快速扫描](../configuration/device-restrictions-windows-10.md) - 让 Defender 对设备运行快速扫描，查看是否存在恶意软件，然后将结果提交到 Intune。 快速扫描会查看可能注册恶意软件的常见位置，例如注册表项和已知的 Windows 启动文件夹。

- [完全扫描](../configuration/device-restrictions-windows-10.md) - 让 Defender 对设备运行扫描，查看是否存在恶意软件，然后将结果提交到 Intune。 完全扫描会查看可能注册恶意软件的常见位置，并扫描设备上的每个文件和文件夹。

- 更新 Windows Defender 安全智能 - 让设备更新其 Microsoft Defender 防病毒的恶意软件定义。 此操作不会开始扫描。

- [BitLocker 密钥轮替](../protect/encrypt-devices.md#to-rotate-the-bitlocker-recovery-key) -远程轮替运行 Windows 10 1909 或更高版本的设备的 BitLocker 恢复密钥。

还可使用“批量设备操作”管理部分操作，例如同时停用和擦除多台设备的操作 。 可在“所有设备”视图中找到[批量操作](../remote-actions/bulk-device-actions.md)。 请选择平台和操作，然后指定设备数量（最高 100 台）。

![选择批量操作](./media/endpoint-security-manage-devices/select-bulk-actions.png)

在使用 Intune 签入设备之前，为设备管理的选项不会生效。

## <a name="next-steps"></a>后续步骤

[在 Intune 中管理终结点安全性](../protect/endpoint-security.md)