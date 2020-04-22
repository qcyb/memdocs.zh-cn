---
title: 基于令牌的 CMG 身份验证
titleSuffix: Configuration Manager
description: 在内部网络上注册客户端以获得唯一令牌，或为基于 Internet 的设备创建批量注册令牌。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f0703475-85a4-450d-a4e8-7a18a01e2c47
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ae92fa2f8e3ee3270de4777fd889bc5fc16a6de4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694135"
---
# <a name="token-based-authentication-for-cloud-management-gateway"></a>为云管理网关进行基于令牌的身份验证

适用范围：  Configuration Manager (Current Branch)

<!--5686290-->

云管理网关 (CMG) 支持许多类型的客户端，但是即使使用[增强的 HTTP](../../plan-design/hierarchy/enhanced-http.md)，这些客户端也需要[客户端身份验证证书](../manage/cmg/certificates-for-cloud-management-gateway.md#for-internet-based-clients-communicating-with-the-cloud-management-gateway)。 如果客户端不经常连接到内部网络、无法加入 Azure Active Directory (Azure AD) 且无法安装 PKI 颁发的证书的基于 Internet，则在其上预配此证书要求可能非常困难。

从版本 2002 开始，Configuration Manager 通过以下方法扩展其设备支持：

- 在内部网络上注册以获得唯一令牌

- 为基于 Internet 的设备创建批量注册令牌

若要充分利用此功能，更新站点后，还请将客户端更新到最新版本。 只有当客户端版本也是最新版本时，完整的方案才起作用。 如有必要，请确保[将新的客户端版本提升为生产版本](../manage/upgrade/test-client-upgrades.md#to-promote-the-new-client-to-production)。

Configuration Manager 客户端与管理点一起管理此令牌，因此不存在操作系统版本依赖关系。 此功能适用于任何[受支持的客户端 OS 版本](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md)。

> [!NOTE]
> 这些方法仅支持以设备为中心的管理方案。
>
> Microsoft 建议将设备加入 Azure AD。 基于 Internet 的设备可以使用 Azure AD 向 Configuration Manager 进行身份验证。 无论设备是在 Internet 上还是连接到内部网络，它都同时支持设备和用户方案。 有关详细信息，请参阅[使用 Azure AD 标识安装和注册客户端](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity)。

## <a name="register-on-the-internal-network"></a>在内部网络上注册

此方法要求客户端先注册到内部网络上的管理点。 通常在客户端安装后注册客户端。 管理点为客户端提供唯一令牌，显示该客户端正在使用自签名证书。 客户端漫游到 Internet 时，为了与 CMG 进行通信，它会将其自签名证书与管理点颁发的令牌配对。 客户端每月续订一次令牌，有效期为 90 天。

站点默认启用此行为。

## <a name="create-a-bulk-registration-token"></a>创建批量注册令牌

如果无法在内部网络上安装和注册客户端，可以创建批量注册令牌。 客户端安装在基于 Internet 的设备上并通过 CMG 进行注册时，使用此令牌。 批量注册令牌的有效期较短，且不会存储在客户端或站点上。 批量注册令牌允许客户端生成与其自签名证书配对的唯一令牌，使客户端能够向 CMG 进行身份验证。

1. 使用本地管理员权限登录到层次结构中的顶级站点服务器。

1. 以管理员身份打开命令提示符。

1. 从站点服务器上 Configuration Manager 安装目录的 `\bin\X64` 文件夹中运行该工具：`BulkRegistrationTokenTool.exe`。 使用 `/new` 参数创建新令牌。 例如，`BulkRegistrationTokenTool.exe /new`。 有关详细信息，请参阅[批量注册令牌工具的用法](#bulk-registration-token-tool-usage)。

1. 复制令牌并将其保存在安全的位置。

1. 在基于 Internet 的设备上安装 Configuration Manager 客户端。 包括客户端安装参数：[ **/regtoken**](about-client-installation-properties.md#regtoken)。 下面的示例命令行包含其他必需的设置参数和属性：

    `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

    > [!TIP]
    > 有关此命令行的详细信息，请参阅[使用 Azure AD 标识安装和注册客户端](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity)。 此过程类似，只是不使用 Azure AD 属性。

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

与 `/new` 参数结合使用，用于指定令牌的令牌有效期。 指定以分钟为单位的整数值。 默认值为 4,320（三天）。

示例：`BulkRegistrationTokenTool.exe /lifetime:4320`

## <a name="see-also"></a>另请参阅

- [规划云管理网关](../manage/cmg/plan-cloud-management-gateway.md)

- [安装并分配 Configuration Manager Windows 10 客户端（使用 Azure AD 进行身份验证）](deploy-clients-cmg-azure.md)
