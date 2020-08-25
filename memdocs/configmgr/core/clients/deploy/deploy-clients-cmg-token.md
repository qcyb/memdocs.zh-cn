---
title: 基于令牌的 CMG 身份验证
titleSuffix: Configuration Manager
description: 在内部网络上注册客户端以获得唯一令牌，或为基于 Internet 的设备创建批量注册令牌。
ms.date: 08/17/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f0703475-85a4-450d-a4e8-7a18a01e2c47
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 55997c9185a221d105aa8ad40bbb14021463d07b
ms.sourcegitcommit: da5bfbe16856fdbfadc40b3797840e0b5110d97d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88512693"
---
# <a name="token-based-authentication-for-cloud-management-gateway"></a>为云管理网关进行基于令牌的身份验证

适用范围：Configuration Manager (Current Branch)

<!--5686290-->

云管理网关 (CMG) 支持许多类型的客户端，但是即使使用[增强的 HTTP](../../plan-design/hierarchy/enhanced-http.md)，这些客户端也需要[客户端身份验证证书](../manage/cmg/certificates-for-cloud-management-gateway.md#for-internet-based-clients-communicating-with-the-cloud-management-gateway)。 如果客户端不经常连接到内部网络、无法加入 Azure Active Directory (Azure AD) 且无法安装 PKI 颁发的证书的基于 Internet，则在其上预配此证书要求可能非常困难。

为了克服这些问题，从版本 2002 开始，Configuration Manager 通过向设备颁发自己的身份验证令牌来扩展其设备支持。 若要充分利用此功能，更新站点后，还请将客户端更新到最新版本。 只有当客户端版本也是最新版本时，完整的方案才起作用。 如有必要，请确保[将新的客户端版本提升为生产版本](../manage/upgrade/test-client-upgrades.md#to-promote-the-new-client-to-production)。

 客户端最初使用以下两种方式之一注册这些令牌：

- 内部网络

- 批量注册

Configuration Manager 客户端与管理点一起管理此令牌，因此不存在操作系统版本依赖关系。 此功能适用于任何[受支持的客户端 OS 版本](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md)。

> [!NOTE]
> 这些方法仅支持以设备为中心的管理方案。
>
> Microsoft 建议将设备加入 Azure AD。 基于 Internet 的设备可以使用 Azure AD 向 Configuration Manager 进行身份验证。 无论设备是在 Internet 上还是连接到内部网络，它都同时支持设备和用户方案。 有关详细信息，请参阅[使用 Azure AD 标识安装和注册客户端](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity)。

## <a name="internal-network-registration"></a>内部网络注册

此方法要求客户端先注册到内部网络上的管理点。 通常在客户端安装后注册客户端。 管理点为客户端提供唯一令牌，显示该客户端正在使用自签名证书。 客户端漫游到 Internet 时，为了与 CMG 进行通信，它会将其自签名证书与管理点颁发的令牌配对。

站点默认启用此行为。

## <a name="bulk-registration-token"></a>批量注册令牌

如果无法在内部网络上安装和注册客户端，可以创建批量注册令牌。 客户端安装在基于 Internet 的设备上并通过 CMG 进行注册时，使用此令牌。 批量注册令牌的有效期较短，且不会存储在客户端或站点上。 批量注册令牌允许客户端生成与其自签名证书配对的唯一令牌，使客户端能够向 CMG 进行身份验证。

> [!NOTE]
> 不要将批量注册令牌与 Configuration Manager 向单个客户端颁发的那些令牌混淆。 通过批量注册令牌，客户端可以进行初始安装并与站点通信。 这个初始通信的时间足以让站点向客户端颁发自己的唯一客户端身份验证令牌。 然后，客户端将自己的身份验证令牌用于它在 Internet 上与站点的所有通信。 除了初始注册之外，客户端不使用或存储批量注册令牌。

若要创建在基于 Internet 的设备上安装客户端期间使用的批量注册令牌，请完成以下操作：

1. 使用本地管理员权限登录到层次结构中的顶级站点服务器。

1. 以管理员身份打开命令提示符。

1. 从站点服务器上 Configuration Manager 安装目录的 `\bin\X64` 文件夹中运行该工具：`BulkRegistrationTokenTool.exe`。 使用 `/new` 参数创建新令牌。 例如，`BulkRegistrationTokenTool.exe /new`。 有关详细信息，请参阅[批量注册令牌工具的用法](#bulk-registration-token-tool-usage)。

1. 复制令牌并将其保存在安全的位置。

1. 在基于 Internet 的设备上安装 Configuration Manager 客户端。 包括客户端安装参数：[ **/regtoken**](about-client-installation-properties.md#regtoken)。 下面的示例命令行包含其他必需的设置参数和属性：

    `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

    > [!TIP]
    > 有关此命令行的详细信息，请参阅[使用 Azure AD 标识安装和注册客户端](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity)。 此过程类似，只是不使用 Azure AD 属性。

若要进行验证，请查看以下日志文件以获取类似条目：<!-- bug 7357499 -->

```ClientLocation.log
Rotating internet management point, new management point [1] is: https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 (0) with capabilities: <Capabilities SchemaVersion ="1.0"><Property Name="SSL" Version="1" /></Capabilities>
```

若要排查安装问题，请查看客户端上的 `%WinDir%\ccmsetup\logs\ccmsetup.log`。 安装之后，查看 `%WinDir%\ccm\logs\ClientIDManagerStartup.log`。

在服务器上，查看以下日志：

- [CMG 日志](../../plan-design/hierarchy/log-files.md#cloud-management-gateway)
- 管理点
  - CCM_STS.log
  - MP_RegistrationManager.log
  - ClientAuth.log

### <a name="known-issues"></a>已知问题

无法在站点服务器处于被动模式的站点上创建批量注册令牌。<!-- 6399087 -->

### <a name="bulk-registration-token-tool-usage"></a>批量注册令牌工具的用法

`BulkRegistrationTokenTool.exe` 工具位于站点服务器上 Configuration Manager 安装目录的 `\bin\X64` 文件夹中。 登录到站点服务器，并以管理员身份运行。 它支持以下命令行参数：

- `/?`
- `/new`
- `/lifetime`

#### <a name=""></a>/?

显示此用法信息。

示例：`BulkRegistrationTokenTool.exe /?`

#### <a name="new"></a>/new

创建新的批量注册令牌。

示例：`BulkRegistrationTokenTool.exe /new`

此工具显示以下信息：
  
- 站点用于跟踪已颁发令牌的 GUID
- 令牌有效期，默认为三天。
- 批量注册令牌。

令牌不会存储在客户端或站点上。 请确保通过命令提示符复制令牌，并将其存储在安全的位置。

#### <a name="lifetime"></a>/lifetime

与 `/new` 参数结合使用，用于指定令牌的令牌有效期。 指定以分钟为单位的整数值。 默认值为 4,320（三天）。 最大值为 10,080（7 天）。

示例：`BulkRegistrationTokenTool.exe /lifetime 4320`

## <a name="bulk-registration-token-management"></a>批量注册令牌管理

可以在 Configuration Manager 控制台中查看以前创建的批量注册令牌及其生存期，并在必要时阻止使用它们。 不过，站点数据库并不存储批量注册令牌。

### <a name="review-a-bulk-registration-token"></a>查看批量注册令牌

1. 在 Configuration Manager 控制台中，转到“管理”工作区。

2. 展开“安全性”，然后选择“证书”节点 。 控制台在细节窗格中列出所有与站点相关的证书以及批量注册令牌。

3. 选择要审阅的批量注册令牌。

你可以对“类型”列进行筛选或排序。 可根据特定的批量注册令牌 GUID 进行识别。 创建批量注册令牌时，工具会显示 GUID。

### <a name="block-a-bulk-registration-token"></a>阻止批量注册令牌

1. 在 Configuration Manager 控制台中，转到“管理”工作区。

2. 展开“安全性”，选择“证书”节点，然后选择要阻止的批量注册令牌 。

3. 在功能区栏的“主页”选项卡中或通过右键单击上下文菜单，选择“阻止” 。 若要取消阻止先前阻止的批量注册令牌，请选择“取消阻止”操作。

## <a name="token-renewal"></a>令牌续订

客户端每月续订一次其唯一的、由 Configuration Manager 颁发的令牌，其有效期为 90 天。 客户端在续订其令牌时不需要连接到内部网络。 只要该令牌仍然有效，就可以使用 CMG 连接到站点。 如果 90 天内未续订令牌，则客户端必须直接连接到内部网络上的管理点才能接收新令牌。

不能续订批量注册令牌。 批量注册令牌过期后，使用 CMG 为基于 Internet 的设备注册生成一个新令牌。

## <a name="see-also"></a>另请参阅

- [规划云管理网关](../manage/cmg/plan-cloud-management-gateway.md)

- [安装并分配 Configuration Manager Windows 10 客户端（使用 Azure AD 进行身份验证）](deploy-clients-cmg-azure.md)
