---
title: 自定义设置 - Windows Holographic for Business 设备 - Microsoft Intune | Microsoft Docs
description: 在 Microsoft Intune 中为运行 Windows Holographic for Business（包括 Microsoft Hololens）的设备添加或创建自定义配置文件，以使用 OMA-URI 设置。 可以设置 AllowFastReconnect、AllowVPN、AllowUpdateService、UpdateServiceURL、RequireUpdatesApproval、ApprovedUpdates 和 ApplicationLaunchRestrictions 策略配置服务提供程序 (CSP) 设置。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.article: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.topic: reference
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3928cd13b5368c8ab196a67669cb3a9f7d3fc2e9
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910020"
---
# <a name="use-custom-settings-for-windows-holographic-for-business-devices-in-intune"></a>在 Intune 中使用适用于 Windows Holographic for Business 设备的自定义设置

借助 Microsoft Intune，可以使用“自定义配置文件”添加或创建适用于 Windows Holographic for Business 设备的自定义设置。 自定义配置文件是 Intune 中的一项功能。 这项功能用于添加未内置到 Intune 的设备设置和功能。

Windows Holographic for Business 自定义配置文件使用开放移动联盟统一资源标识符 (OMA-URI) 设置配置不同的功能。 移动设备制造商通常使用这些设置来控制设备上的功能。

通过 Windows Holographic for Business 可以进行很多配置服务提供程序 (CSP) 设置。 有关 CSP 的概述，请参阅[面向 IT 专业人员的配置服务提供程序 (CSP) 简介](/windows/configuration/provisioning-packages/how-it-pros-can-use-configuration-service-providers)。 如需了解 Windows Holographic 支持的具体 CSP，请参阅 [Windows Holographic 中支持的 CSP](/windows/client-management/mdm/configuration-service-provider-reference#hololens)。

如果正在寻找特定设置，建议 [Windows Holographic for Business 设备限制配置文件](device-restrictions-windows-holographic.md)包含许多内置设置。 因此，可能不需要输入自定义值。

本文介绍如何创建适用于 Windows Holographic for Business 设备的自定义配置文件。 文中还包括建议的 OMA-URI 设置列表。

## <a name="before-you-begin"></a>在开始之前

[创建 Windows 10 自定义配置文件](custom-settings-configure.md#create-the-profile)。

## <a name="custom-oma-uri-settings"></a>自定义 OMA-URI 设置

**添加**：输入以下设置：

- **名称**：输入 OMA-URI 设置的唯一名称，以帮助你在设置列表中识别它。
- **描述**：输入包含设置概述以及其他所有重要详细信息的说明。
- **OMA-URI**（区分大小写）：输入要用作设置的 OMA-URI。
- **数据类型**：选择用于此 OMA-URI 设置的数据类型。 选项包括：

  - 字符串
  - 字符串（XML 文件）
  - 日期和时间
  - 整数
  - 浮点
  - 布尔值
  - Base64（文件）

- **值**：输入要与已输入的 OMA-URI 关联的数据值。 值取决于所选的数据类型。 例如，如果选择了“日期和时间”，则从日期选取器中选择值。

添加一些设置后，可以选择“导出”。 “导出”将创建逗号分隔值 (.csv) 文件中添加的所有值的列表。

## <a name="recommended-custom-settings"></a>推荐的自定义设置

以下设置也可用于运行 Windows Holographic for Business 的设备：

### <a name="allowfastreconnect"></a>[AllowFastReconnect](/windows/client-management/mdm/policy-csp-authentication#authentication-allowfastreconnect)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Authentication/AllowFastReconnect|整数<br/>0 - 不允许<br/>1 - 允许（默认值）|

### <a name="allowupdateservice"></a>[AllowUpdateService](/windows/client-management/mdm/policy-csp-update#update-allowupdateservice)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/AllowUpdateService|整数<br/>0 – 不允许更新服务 <br/>1 – 允许更新服务（默认值）。|

### <a name="allowvpn"></a>[AllowVPN](/windows/client-management/mdm/policy-csp-settings#settings-allowvpn)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Settings/AllowVPN|整数<br/>0 - 不允许<br/>1 - 允许（默认值）|

### <a name="requireupdateapproval"></a>[RequireUpdateApproval](/windows/client-management/mdm/policy-csp-update#update-requireupdateapproval)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/RequireUpdateApproval|此设置在 RS5（内部版本 17763）及更早版本中可用。 从 19H1（内部版本 18362）开始，使用[适用于企业的 Windows 更新](../protect/windows-update-for-business-configure.md)。<br/><br/>整数<br/>0 – 未配置。 设备安装所有适用的更新。<br/>1 – 设备仅安装既适用又在已批准更新列表中的更新。 如果 IT 想控制设备上的更新部署（例如部署前需要测试），请将此策略设置为 1。|

### <a name="scheduledinstalltime"></a>[ScheduledInstallTime](/windows/client-management/mdm/policy-csp-update#update-scheduledinstalltime)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/ScheduledInstallTime|整数 0-23，其中 0 表示中午 12 点，23 表示晚上 11 点<br/>默认值为 3。|

### <a name="updateserviceurl"></a>[UpdateServiceURL](/windows/client-management/mdm/policy-csp-update#update-updateserviceurl)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/UpdateServiceUrl|此设置在 RS5（内部版本 17763）及更早版本中可用。 从 19H1（内部版本 18362）开始，使用[适用于企业的 Windows 更新](../protect/windows-update-for-business-configure.md)。<br/><br/>字符串<br/>URL - 设备从指定的 URL 上的 WSUS 服务器检查更新。<br/>未配置 - 设备从 Microsoft 更新检查更新。|

### <a name="approvedupdates"></a>[ApprovedUpdates](/windows/client-management/mdm/update-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Update/ApprovedUpdates/GUID<br/><br/>**重要说明**<br/>必须代表最终用户阅读和接受更新 EULA。 如果不这样做，将被视为违反法律或合同义务。|更新批准的节点和代表最终用户的 EULA 接受。<br/><br/>有关详细信息，请参阅[更新 CSP](/windows/client-management/mdm/update-csp)。|

### <a name="applicationlaunchrestrictions"></a>[ApplicationLaunchRestrictions](/windows/client-management/mdm/applocker-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |----|---|
> |./Vendor/MSFT/AppLocker/ApplicationLaunchRestrictions/*Grouping*/*ApplicationType*/Policy<br/><br/>**重要说明**<br/>AppLocker CSP 一文使用转义 XML 示例。 若要使用 Intune 自定义配置文件配置设置，必须使用纯 XML。|字符串<br/>有关详细信息，请参阅 [AppLocker CSP](/windows/client-management/mdm/applocker-csp)。|

### <a name="deletionpolicy"></a>[DeletionPolicy](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/DeletionPolicy|整数<br/>0 - 设备返回到当前没有活动用户的状态时立即删除<br/>1 - 按存储容量阈值删除（默认）<br/>2 - 按存储容量阈值和配置文件非活动阈值删除|

### <a name="enableprofilemanager"></a>[EnableProfileManager](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/EnableProfileManager|布尔值<br/>True - 启用<br/>False - 禁用（默认值）|

### <a name="profileinactivitythreshold"></a>[ProfileInactivityThreshold](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/ProfileInactivityThreshold|整数<br/>默认值为 30。|

### <a name="storagecapacitystartdeletion"></a>[StorageCapacityStartDeletion](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStartDeletion|整数<br/>默认值为 25。|

### <a name="storagecapacitystopdeletion"></a>[StorageCapacityStopDeletion](/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStopDeletion|整数<br/>默认值为 50。|

## <a name="find-the-policies-you-can-configure"></a>查找可以配置的策略

在 [Windows Holographic 中支持的 CSP](/windows/client-management/mdm/configuration-service-provider-reference#hololens) 中，可以找到 Windows Holographic 支持的所有配置服务提供程序 (CSP) 的完整列表。 并非所有设置都与所有 Windows Holographic 版本兼容。 [Windows Holographic 中支持的 CSP](/windows/client-management/mdm/configuration-service-provider-reference#hololens) 中的表格列出了每个 CSP 受支持的版本。

此外，Intune 并不支持 [Windows Holographic 中支持的 CSP](/windows/client-management/mdm/configuration-service-provider-reference#hololens) 中列出的所有设置。 若要查明 Intune 是否支持所需的设置，请打开针对该设置的文章。 每个设置页面都将显示其支持的操作。 若要使用 Intune，设置必须支持“添加”或“替换”操作。

## <a name="next-steps"></a>后续步骤

[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

在 [Windows 10 设备上创建自定义配置文件](custom-settings-windows-10.md)。

详细了解 Intune 中的[自定义配置文件](custom-settings-configure.md)。