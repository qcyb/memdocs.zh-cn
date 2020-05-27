---
title: 使用设备注册管理员帐户注册设备
titleSuffix: Microsoft Intune
description: 使用设备注册管理器帐户在 Intune 中注册设备。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/28/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7196b33e-d303-4415-ad0b-2ecdb14230fd
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: cb5dec2fd96c5b5dfe0b82bb30bf653250786c95
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "83986759"
---
# <a name="enroll-devices-in-intune-by-using-a-device-enrollment-manager-account"></a>使用设备注册管理员帐户在 Intune 中注册设备

通过使用设备注册管理器 (DEM) 帐户，可以使用单个 Azure Active Directory 帐户注册多达 1,000 个移动设备。 DEM 是一种 Intune 权限，可以应用于 AAD 用户帐户，并允许用户最多注册 1,000 个设备。 将设备交付给设备的用户之前，使用 DEM 帐户注册和准备设备非常有用。 根据设计，Microsoft Intune 限制为 150 个设备注册管理员 (DEM) 帐户。

## <a name="limitations-of-devices-that-are-enrolled-with-a-dem-account"></a>使用 DEM 帐户注册的设备限制

使用 DEM 用户帐户注册的 DEM 用户帐户和设备具有以下限制：

- 必须为 DEM 帐户用户分配 Intune 许可证。
- 无法通过公司门户进行擦除。 可以从 Azure 门户中的 Intune 擦除通过 DEM 用户帐户注册的设备。
- 公司门户应用或网站中仅显示本地设备。
- 由于应用管理的每用户 Apple ID 要求，DEM 用户帐户无法将 Apple Volume Purchase Program (VPP) 应用与 Apple VPP 用户许可证一起使用。
- 通过 Apple 自动设备注册 (ADE) 注册设备时，不能使用 DEM 帐户。
- 如果设备具有 Apple VPP 许可证，则可以安装 VPP 应用。
- 设备出于条件访问而被阻止，Windows 10 1803+ 除外
- 向 DEM 帐户注册的每台设备都需要获得适当许可才能由 Intune 托管。 许可证可以是 Intune 用户许可证，也可以是 Intune 设备许可证。
- 如果使用 DEM 帐户[注册 Android Enterprise 工作配置文件设备](android-work-profile-enroll.md)，则每个帐户最多可注册 10 台设备。
- 不支持使用 DEM 帐户[注册 Android Enterprise 完全托管设备](android-fully-managed-enroll.md)。
- 如果将 Azure AD 设备限制应用于 DEM 帐户，可防止你达到 DEM 帐户可以注册的 1,000 台设备限制。

## <a name="enrollment-methods-supported-by-dem-accounts"></a>DEM 帐户支持的注册方法

可以通过以下方法来使用 DEM 帐户注册设备：

- [Windows Autopilot](enrollment-autopilot.md)
- [Windows 设备批量注册](windows-bulk-enroll.md)
- DEM 通过公司门户启动

## <a name="add-a-device-enrollment-manager"></a>添加一个设备注册管理器

1. 登录 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，选择“设备” > “注册设备” > “设备注册管理器”    。

2. 选择“添加”  。

3. 在“添加用户”  边栏选项卡上，输入 DEM 用户的用户主体名称，并选择“添加”  。 DEM 用户将添加到 DEM 用户列表。

## <a name="permissions-required-to-create-dem-accounts"></a>创建 DEM 帐户所需的权限

需要全局管理员或 Intune 服务管理员 Azure AD 角色
- 才能为 Azure AD 用户帐户分配 DEM 权限
- 查看全部 DEM 用户

如果用户未分配到全局管理员或 Intune 服务管理员角色，但分配给他们的设备注册管理器角色启用了读取权限，则这些用户将只能查看自己创建的 DEM 用户。

## <a name="remove-device-enrollment-manager-permissions"></a>删除设备注册管理器权限

删除设备注册管理器不会影响已注册的设备。

**删除设备注册管理器**

1. 登录 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，选择“设备” > “注册设备” > “设备注册管理器”    。
2. 在“设备注册管理员”边栏选项卡上，选择 DEM 用户，然后选择“删除”   。

