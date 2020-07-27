---
title: 在 Microsoft Intune 中检查安全基线是否成功部署 - Azure | Microsoft Docs
description: 在 Microsoft Intune MDM 中，检查部署到用户和设备的安全基线的错误、冲突和成功状态。 了解如何使用 Intune 中的客户端日志和报告功能排除故障。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cecd39bcba7e16cc933086c99bbc0b403381d75d
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461787"
---
# <a name="monitor-security-baselines-and-profiles-in-microsoft-intune"></a>使用 Microsoft Intune 监视安全基线和配置文件

Intune 提供了用于监视安全基线的多个选项。 你可以：

- 监视安全基线，以及与建议值匹配（或不匹配）的任何设备。
- 监视应用于用户和设备的安全基线配置文件。
- 查看如何在所选设备上设置所选配置文件的设置。

你还可以查看应用于单个设备（包括安全基线）的终结点安全配置。

本文介绍了这些监视选项。

[Intune 中的安全基线](security-baselines.md)详细介绍了 Microsoft Intune 中的安全基线功能。

## <a name="monitor-the-baseline-and-your-devices"></a>监视基线和设备

监视基线时，你根据 Microsoft 的建议深入了解设备的安全状态。 若要查看这些见解，请登录到 [管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，转到“终结点安全” > “安全基线”，并选择一种安全基线类型，如“MDM 安全基线”。 然后，从“配置文件”窗格中，选择要查看详细信息的配置文件实例。 此时将打开配置文件“属性”窗格，然后可从“监视”部分选择任何配置文件报表 。 

首次分配基线后，最多 24 小时后会显示数据。 之后进行的更改最多六个小时后会显示。

深入查看报表和设备，了解各种详细信息。

<!-- UI is changing, unclear how yet: 


- **Device view** – A summary of how many devices are in each status category for the baseline.
- **Per-category** - A view that displays each category in the baseline and includes the percentage of devices for each status group for each baseline category.

Each device is represented by one of the following statuses (used in the *device* view and also the *per-category* views):

- **Matches baseline** - All the settings in the baseline match the recommended settings.
- **Does not match baseline** - One or more settings in the baseline were modified from their default values in the original baseline. The default values in each security baseline are the recommended values for that baseline.

  > [!NOTE]
  > When you create or edit a baseline profile, any change that is made to a default value or configuration setting causes a *Does not match baseline* status to occur. For help to determine the settings that were changed, contact Microsoft Support. 

- **Misconfigured** - At least one setting isn't correctly configured. This status means that the setting is in a conflict, error, or pending state.
- **Not applicable** - At least one setting isn't applicable and isn't applied.

### Device view

The Overview pane displays a chart-based summary of how many devices have a specific status for the baseline; **Security baseline posture for assigned Windows 10 devices**.

![Check the status of the devices](./media/security-baselines-monitor/overview.png)

When a device has different status from different categories in the baseline, the device is represented by a single status. The status that represents the device is taken from the following order of precedence: **Misconfigured**, **Does not match baseline**, **Not applicable**, **Matches baseline**.

For example, if a device has a setting that's classified as *misconfigured* and one or more settings that are classified as *Does not match baseline*, the device is classified as *Misconfigured*.

You can click on the chart to drill through and view a list of devices with various statuses. You can then select individual devices from that list to view details about individual devices. For example:

- Select **Device configuration** > Select the profile with an Error state:

  ![View the status of a profile](./media/security-baselines-monitor/device-configuration-profile-list.png)

- Select the Error profile. A list of all settings in the profile, and their state is shown. Now, you can scroll to find the setting causing the error:

  ![See the setting causing the error](./media/security-baselines-monitor/profile-with-error-status.png)

Use this reporting to see any settings in a profile that are causing an issue. Also get more details of policies and profiles deployed to devices.

> [!NOTE]
> When a property is set to **Not configured** in the baseline, the setting is ignored, and no restrictions are enforced. The property isn't shown in any reporting.

### Per category view

The Overview pane displays a per-category chart for the baseline named **Security baseline posture by category**.  This view displays each category from the baseline, and identifies the percentage of devices that fall into a status classification for each of those categories.

![Per-Category view of status](./media/security-baselines-monitor/monitor-baseline-per-category.png)

Status for **Matches baseline** doesn't display until 100% of devices report that status for the category.

You can sort the by-category view by each column, by selecting up-down arrow icon at the top of the column.
-->

## <a name="monitor-the-profile"></a>监视配置文件

通过监视配置文件，可以根据基线建议深入了解设备部署状态，而不是安全状态。

1. 在 Intune 中，选择“安全基线”，然后选择基线以打开其“配置文件”窗格。

<!-- More churn  
2. Select a profile. In **Overview**, the image shows how many devices and users have this profile assigned:

   ![See how many devices and users are assigned the security baselines profile](./media/security-baselines-monitor/existing-profile-overview.png)
--> 
3. “管理” > “属性”下列出了基线中的所有设置。 还可以更改其中任何设置：

   ![查看和更新安全基线配置文件中的设置](./media/security-baselines-monitor/manage-settings.png)

4. 在“监视”中，可以查看各个设备上配置文件的部署状态、每个用户的状态，以及基线中每个设置的状态：

   ![查看安全基线配置文件的其他监视选项](./media/security-baselines-monitor/monitor-status-options.png)

## <a name="view-settings-from-profiles-that-apply-to-a-device"></a>查看应用于设备的配置文件中的设置

可以为安全基线选择一个配置文件，并在应用于单个设备的情况下深入查看该配置文件中的设置列表。  若要查看该列表，请钻取到“终结点安全” > “安全基线” > “选择安全基线类型” > “选择要查看的配置文件” > “设备状态”。 也可以通过转到“终结点安全” > “所有设备” > “选择设备” > “终结点安全配置” > “选择基线版本”来查看列表。

选择设备后，Microsoft Endpoint Manager 管理中心将显示来自该配置文件的设置列表，其中包括设置所属的类别，以及设备上的配置状态。 配置状态包括以下值：

- **成功** - 设备上的设置与配置文件中配置的值相匹配。 这要么是基线默认值和建议值，要么是管理员在配置配置文件时指定的自定义值。
- **冲突** - 此设置与另一个策略冲突，出现错误，或者正在等待更新。
- **不适用**：此设置不适用于配置文件。

> [!NOTE]
> 设置的状态值将在未来版本中更新，以提供更精细的详细信息。

## <a name="view-endpoint-security-configurations-per-device"></a>查看每个设备的终结点安全配置

查看有关适用于单个设备的安全配置详细信息，这有助于隔离配置错误的设置。

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 转到“设备” > 所有设备”，然后选择要查看的设备 。

3. 在“监视器”类别中，选择“终结点安全配置”，查看适用于该设备的安全配置列表。

4. 可选择终结点安全配置，进一步探索并查看有关在设备上评估该安全配置的其他详细信息。

## <a name="troubleshoot-using-per-setting-status"></a>使用每个设置状态排除故障

已部署安全基线，但部署状态显示错误。 下面逐步介绍了对错误进行故障排除。

1. 在 Intune 中，依次选择“安全基线”、“基线”和“配置文件” 。

2. 选择配置文件，在依次转到“监视” > “每个设置状态”下。

3. 此时，表中显示所有设置以及每个设置的状态。 选择“错误”列或“冲突”列，以查看导致错误出现的设置。

### <a name="mdm-diagnostic-information"></a>MDM 诊断信息

现在，你知道哪个设置有问题。 下一步是确定此设置为什么会导致错误或冲突出现。

Windows 10 设备上内置有 MDM 诊断信息报告。 此报告包含默认值、当前值，不仅会列出策略，还会显示是部署到设备还是部署到用户等。 使用此报告有助于确定设置为什么会导致冲突或错误出现。

1. 在设备上，依次转到“设置” > “帐户” > “访问工作或学校”。

2. 选择帐户，再依次选择“信息” > “高级诊断报告” > “生成报告”。

3. 选择“导出”，再打开所生成的文件。

4. 在报告的不同部分中查找错误或冲突设置。

  例如，在“已注册的配置源和目标资源”部分或“非托管策略”部分中查找。 这样可能就会知道设置为什么会导致错误或冲突出现。

[在 Windows 10 中诊断 MDM 故障](https://docs.microsoft.com/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)详细介绍了此内置报告。

> [!TIP]
>
> - 一些设置还列出了 GUID。 可以在本地注册表 (regedit) 中搜索此 GUID 是否是任何设定值。
> - 事件查看器日志可能还包括有问题设置的一些错误信息（依次转到“事件查看器” > “应用和服务日志” > “Microsoft” > “Windows” > “DeviceManagement-Enterprise-Diagnostics-Provider” > “管理员”）。

## <a name="next-steps"></a>后续步骤

- [了解安全基线](security-baselines.md)
- [避免冲突](security-baselines.md#avoid-conflicts)
- [监视设备配置文件](../configuration/device-profile-monitor.md) 
- [常见问题和解决方法](../configuration/device-profile-troubleshoot.md)。
- [在 Intune 中对策略和配置文件进行故障排除](../configuration/troubleshoot-policies-in-microsoft-intune.md)