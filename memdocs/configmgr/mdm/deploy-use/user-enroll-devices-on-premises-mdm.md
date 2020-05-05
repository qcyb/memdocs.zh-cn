---
title: 用户如何注册设备
titleSuffix: Configuration Manager
description: 了解用户如何向 Configuration Manager 中的本地移动设备管理（MDM）注册设备。
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 59004b34-b64f-4d77-898c-07bf3dc75430
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f80b77d6a25d7af701ded249118e95201bcb9cc1
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724881"
---
# <a name="how-users-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>用户如何在 Configuration Manager 中向本地 MDM 注册设备

适用范围：  Configuration Manager (Current Branch)

通过 Configuration Manager 本地移动设备管理（MDM），用户可以注册其设备。 有两个先决条件：

- 对于客户端设置，你向用户授予注册权限。

- 在设备上安装所需的受信任的根证书。

有关如何设置注册的详细信息，请参阅为[本地 MDM 设置设备注册](../get-started/set-up-device-enrollment-on-premises-mdm.md)。

## <a name="enroll-windows-10"></a><a name="bkmk_enrollDesk"></a>注册 Windows 10

1. 在 Windows 10 计算机上，转到“设置” ****。

1. 选择 "**帐户**"，然后选择 "**访问工作单位或学校**"。

1. 选择 "**连接**"，输入用户主体名称（UPN），然后选择 "**继续**"。 UPN 可能与电子邮件地址相同，例如jdoe@contoso.com。

1. 输入注册代理点的完全限定的域名（FQDN），然后选择 "**继续**"。

1. 输入密码，然后选择 "**登录**"。

1. Windows 不需要记住此操作的登录信息，因此请选择 "**跳过**"。

短时间之后，设备将使用 Configuration Manager 进行注册。

## <a name="enroll-windows-10-mobile"></a><a name="bkmk_enrollMob"></a>注册 Windows 10 移动版

1. 在 Windows 10 移动版设备上，转到“设置” ****。

1. 选择 "**帐户**"，然后选择 "**工作访问**"。

1. 选择“连接”  。

1. 输入 UPN 和注册代理点的 FQDN。 然后选择“连接”****。

1. 在下一个屏幕上，输入你的 UPN 和密码，然后选择 "**登录**"。

短时间之后，设备将使用 Configuration Manager 进行注册。 选择“完成”  。

## <a name="verify-enrollment"></a><a name="bkmk_verify"></a>验证注册

使用 Configuration Manager 控制台验证是否已成功注册设备。 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，并选择“设备”********。 在设备列表中浏览或搜索已注册的设备。
