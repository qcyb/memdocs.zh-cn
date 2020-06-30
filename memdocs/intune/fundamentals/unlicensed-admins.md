---
title: 注册或登录到 Microsoft Intune
description: 如何注册 Microsoft Intune 订阅或登录以开始你的订阅。
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
ms.openlocfilehash: ae30e03a03b4d690bdaa9e6a4c73da6ab15226f7
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2020
ms.locfileid: "85095743"
---
# <a name="unlicensed-admins"></a>未经许可的管理员

可以向没有 Intune 许可证的管理员授予 Intune/Microsoft Endpoint Manager 管理中心访问权限。

1. 登录到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431) > “租户管理” > “管理员授权”。
2.  选择“允许未授权的管理员访问” > “是”。
    >[!WARNING]
    >单击“是”后，无法撤消此设置。

3. 从现在开始，登录到 Microsoft Endpoint Manager 管理中心的用户不需要 Intune 许可证。 它们的可访问范围由分配给它们的角色定义。

对于每个安全组 Intune 最多支持 350 个未授权的管理员。 超过此限制的管理员会遇到不可预知的行为。




