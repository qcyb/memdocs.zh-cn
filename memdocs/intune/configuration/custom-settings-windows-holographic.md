---
title: 自定义设置 - Windows Holographic for Business 设备 - Microsoft Intune | Microsoft Docs
description: 在 Microsoft Intune 中为运行 Windows Holographic for Business（包括 Microsoft Hololens）的设备添加或创建自定义配置文件，以使用 OMA-URI 设置。 可以设置 AllowFastReconnect、AllowVPN、AllowUpdateService、UpdateServiceURL、RequireUpdatesApproval、ApprovedUpdates 和 ApplicationLaunchRestrictions 策略配置服务提供程序 (CSP) 设置。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/19/2020
ms.article: article
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.topic: reference
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 43199009740f259c6a6484e455b0205da76492ba
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "80084046"
---
# <a name="use-custom-settings-for-windows-holographic-for-business-devices-in-intune"></a>在 Intune 中使用适用于 Windows Holographic for Business 设备的自定义设置

借助 Microsoft Intune，可以使用“自定义配置文件”添加或创建适用于 Windows Holographic for Business 设备的自定义设置。 自定义配置文件是 Intune 中的一项功能。 这项功能用于添加未内置到 Intune 的设备设置和功能。

Windows Holographic for Business 自定义配置文件使用开放移动联盟统一资源标识符 (OMA-URI) 设置配置不同的功能。 移动设备制造商通常使用这些设置来控制设备上的功能。

通过 Windows Holographic for Business 可以进行很多配置服务提供程序 (CSP) 设置。 有关 CSP 的概述，请参阅[面向 IT 专业人员的配置服务提供程序 (CSP) 简介](https://technet.microsoft.com/itpro/windows/manage/how-it-pros-can-use-configuration-service-providers)。 如需了解 Windows Holographic 支持的具体 CSP，请参阅 [Windows Holographic 中支持的 CSP](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens)。

如果正在寻找特定设置，建议 [Windows Holographic for Business 设备限制配置文件](device-restrictions-windows-holographic.md)包含许多内置设置。 因此，可能不需要输入自定义值。

本文介绍如何创建适用于 Windows Holographic for Business 设备的自定义配置文件。 文中还包括建议的 OMA-URI 设置列表。

## <a name="create-the-profile"></a>创建配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备”   > “配置文件”   > “创建配置文件”  。
3. 输入以下设置：

    - **名称**：输入配置文件的描述性名称。 为配置文件命名，以便稍后可以轻松地识别它们。 例如，将配置文件命名为“Hololens 自定义配置文件”就很不错  。
    - **描述**：输入包含设置概述以及其他所有重要详细信息的说明。
    - **平台**：选择“Windows 10 及更高版本”  。
    - **配置文件类型**：选择“自定义”  。

4. 在“自定义 OMA-URI 设置”中，选择“添加”   。 输入以下设置：

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

    - **值**：输入要与已输入的 OMA-URI 关联的数据值。 值取决于所选的数据类型。 例如，如果选择了“日期和时间”，则从日期选取器中选择值  。

    添加一些设置后，可以选择“导出”  。 “导出”将创建逗号分隔值 (.csv) 文件中添加的所有值的列表  。

5. 选择“确定”，保存所做更改  。 根据需要继续添加更多设置。
6. 完成后，选择“确定”   > “创建”  ，以创建 Intune 配置文件。 完成后，配置文件将显示在“设备 - 配置文件”列表中  。

## <a name="recommended-custom-settings"></a>推荐的自定义设置

以下设置也可用于运行 Windows Holographic for Business 的设备：

### <a name="allowfastreconnect"></a>[AllowFastReconnect](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-allowfastreconnect)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Authentication/AllowFastReconnect|整数<br/>0 - 不允许<br/>1 - 允许（默认值）|

### <a name="allowupdateservice"></a>[AllowUpdateService](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-allowupdateservice)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/AllowUpdateService|整数<br/>0 – 不允许更新服务 <br/>1 – 允许更新服务（默认值）。|

### <a name="allowvpn"></a>[AllowVPN](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-settings#settings-allowvpn)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Settings/AllowVPN|整数<br/>0 - 不允许<br/>1 - 允许（默认值）|

### <a name="requireupdateapproval"></a>[RequireUpdateApproval](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-requireupdateapproval)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/RequireUpdateApproval|此设置在 RS5（内部版本 17763）及更早版本中可用。 从 19H1（内部版本 18362）开始，使用[适用于企业的 Windows 更新](../protect/windows-update-for-business-configure.md)。<br/><br/>整数<br/>0 – 未配置。 设备安装所有适用的更新。<br/>1 – 设备仅安装既适用又在已批准更新列表中的更新。 如果 IT 想控制设备上的更新部署（例如部署前需要测试），请将此策略设置为 1。|

### <a name="scheduledinstalltime"></a>[ScheduledInstallTime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-scheduledinstalltime)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/ScheduledInstallTime|整数 0-23，其中 0 表示中午 12 点，23 表示晚上 11 点<br/>默认值为 3。|

### <a name="updateserviceurl"></a>[UpdateServiceURL](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-update#update-updateserviceurl)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Policy/Config/Update/UpdateServiceUrl|此设置在 RS5（内部版本 17763）及更早版本中可用。 从 19H1（内部版本 18362）开始，使用[适用于企业的 Windows 更新](../protect/windows-update-for-business-configure.md)。<br/><br/>字符串<br/>URL - 设备从指定的 URL 上的 WSUS 服务器检查更新。<br/>未配置 - 设备从 Microsoft 更新检查更新。|

### <a name="approvedupdates"></a>[ApprovedUpdates](https://docs.microsoft.com/windows/client-management/mdm/update-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |---|---|
> |./Vendor/MSFT/Update/ApprovedUpdates/GUID <br/><br/>**重要说明**<br/>必须代表最终用户阅读和接受更新 EULA。 如果不这样做，将被视为违反法律或合同义务。|更新批准的节点和代表最终用户的 EULA 接受。<br/><br/>有关详细信息，请参阅[更新 CSP](https://docs.microsoft.com/windows/client-management/mdm/update-csp)。|

### <a name="applicationlaunchrestrictions"></a>[ApplicationLaunchRestrictions](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |----|---|
> |./Vendor/MSFT/AppLocker/ApplicationLaunchRestrictions/*Grouping*/*ApplicationType*/Policy<br/><br/>**重要说明**<br/>AppLocker CSP 一文使用转义 XML 示例。 若要使用 Intune 自定义配置文件配置设置，必须使用纯 XML。|字符串<br/>有关详细信息，请参阅 [AppLocker CSP](https://docs.microsoft.com/windows/client-management/mdm/applocker-csp)。|

### <a name="deletionpolicy"></a>[DeletionPolicy](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/DeletionPolicy|整数<br/>0 - 设备返回到当前没有活动用户的状态时立即删除<br/>1 - 按存储容量阈值删除（默认）<br/>2 - 按存储容量阈值和配置文件非活动阈值删除|

### <a name="enableprofilemanager"></a>[EnableProfileManager](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/EnableProfileManager|布尔值<br/>True - 启用<br/>False - 禁用（默认值）|

### <a name="profileinactivitythreshold"></a>[ProfileInactivityThreshold](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/ProfileInactivityThreshold|整数<br/>默认值为 30。|


### <a name="storagecapacitystartdeletion"></a>[StorageCapacityStartDeletion](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStartDeletion|整数<br/>默认值为 25。|

### <a name="storagecapacitystopdeletion"></a>[StorageCapacityStopDeletion](https://docs.microsoft.com/windows/client-management/mdm/accountmanagement-csp)

> [!div class="mx-tableFixed"]
> |OMA-URI|数据类型|
> |----|---|
> |./Vendor/MSFT/AccountManagement/UserProfileManagement/StorageCapacityStopDeletion|整数<br/>默认值为 50。|

## <a name="find-the-policies-you-can-configure"></a>查找可以配置的策略

在 [Windows Holographic 中支持的 CSP](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens) 中，可以找到 Windows Holographic 支持的所有配置服务提供程序 (CSP) 的完整列表。 并非所有设置都与所有 Windows Holographic 版本兼容。 [Windows Holographic 中支持的 CSP](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens) 中的表格列出了每个 CSP 受支持的版本。

此外，Intune 并不支持 [Windows Holographic 中支持的 CSP](https://docs.microsoft.com/windows/client-management/mdm/configuration-service-provider-reference#hololens) 中列出的所有设置。 若要查明 Intune 是否支持所需的设置，请打开针对该设置的文章。 每个设置页面都将显示其支持的操作。 若要使用 Intune，设置必须支持“添加”  或“替换”  操作。

## <a name="next-steps"></a>后续步骤

配置文件已创建，但它尚未起到任何作用。 下一步，[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

在 [Windows 10 设备上创建自定义配置文件](custom-settings-windows-10.md)。
