---
title: Microsoft Intune 中未授权的管理员
description: 了解如何为未授权的管理员授予访问 Intune 的权限。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/02/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: c6dcd41377234bbb1b40e513f16c3393d763b17f
ms.sourcegitcommit: e713f8f4ba2ff453031c9dfc5bfd105ab5d00cd9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2020
ms.locfileid: "86088184"
---
# <a name="unlicensed-admins"></a>未经许可的管理员

可以向没有 Intune 许可证的管理员授予 Intune/Microsoft Endpoint Manager 管理中心访问权限。

1. 登录到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > “租户管理” > “角色” > “管理员授权”  。
2.  选择“允许未授权的管理员访问” > “是”。
    >[!WARNING]
    >单击“是”后，无法撤消此设置。

3. 从现在开始，登录到 Microsoft Endpoint Manager 管理中心的用户不需要 Intune 许可证。 它们的可访问范围由分配给它们的角色定义。

对于每个安全组，Intune 最多支持 350 个未授权的管理员，并仅适用于直接成员。 超过此限制的管理员会遇到不可预知的行为。




