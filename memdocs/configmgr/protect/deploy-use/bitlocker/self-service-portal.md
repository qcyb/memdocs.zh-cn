---
title: BitLocker 自助服务门户
titleSuffix: Configuration Manager
description: 如何在 Configuration Manager 中使用用户自助服务门户来恢复 BitLocker
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 88e0ad46-7f0c-4f5c-9b48-54773c23768d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fda719aed4d70cd9783d158e17d546b698497997
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699685"
---
# <a name="bitlocker-self-service-portal"></a>BitLocker 自助服务门户

适用范围：  Configuration Manager (Current Branch)

<!--3601034-->

[安装 BitLocker 自助服务门户](setup-websites.md)后，如果 BitLocker 锁定用户的设备，这些用户可独立地访问其计算机。 自助服务门户无需技术支持人员提供任何帮助。

[![默认 BitLocker 自助服务门户的屏幕截图](media/bitlocker-self-service-portal.png)](media/bitlocker-self-service-portal.png#lightbox)

> [!IMPORTANT]
> 要从自助服务门户获取恢复密钥，用户必须至少成功登录一次计算机。 该登录必须是到设备的本地登录，不能在远程会话中进行。 否则，他们需要联系技术支持以恢复密钥。 技术支持管理员可使用[管理和监视网站](helpdesk-portal.md)来请求恢复密钥。

BitLocker 可在下列情况下锁定设备：

- 用户忘记 BitLocker 密码或 PIN

- 设备的操作系统文件、BIOS 或受信任的平台模块 (TPM) 出现更改

若要从自助服务门户请求 BitLocker 恢复密钥：

1. 当 BitLocker 锁定设备时，会在启动过程中显示 BitLocker 恢复屏幕。 记下 32 位数的 BitLocker 恢复密钥 ID。

1. 在另一台计算机上，在 Web 浏览器中转到自助服务门户，例如 `https://webserver.contoso.com/SelfService`。

1. 阅读并接受通知。

1. 在“恢复密钥 ID”字段中，输入 BitLocker 恢复密钥 ID 的前 8 位数  。 如果它与多个密钥匹配，则输入全部的 32 位数。

1. 为此请求的“原因”选择下列某个选项  ：

    - BIOS/TPM 已更改
    - 归档的操作系统已修改
    - PIN/密码已丢失

1. 选择“获取密钥”  。 自助服务门户会显示 48 位数的 BitLocker 恢复密钥  。

1. 在计算机上的 BitLocker 恢复屏幕输入此 48 位代码。

> [!NOTE]
> 一段时间不活动后，BitLocker 自助服务门户可能会超时。 例如，在 5 分钟后，你可能会看到包含 60 秒计数器的超时警告。
>
> ![BitLocker 自助服务门户超时警告](media/bitlocker-self-service-portal-timeout-warning.png)
>
> 如果倒计时结束之前未作出响应，则会话将过期。
>
> ![BitLocker 自助服务门户会话过期页面](media/bitlocker-self-service-portal-session-expired.png)
