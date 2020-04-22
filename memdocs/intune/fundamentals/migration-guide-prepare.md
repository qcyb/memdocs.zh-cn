---
title: 为移动设备管理准备 Intune
titleSuffix: Microsoft Intune
description: 迁移到 Microsoft Intune 之前，请评估业务和技术需求。
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 58591442-6606-4f39-a06b-f17a1f25af25
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 46e717478078ab13cc2c8783cdacbde0911e83a5
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "79358190"
---
# <a name="phase-1-prepare-microsoft-intune-for-mobile-device-management-mdm"></a>阶段 1：为移动设备管理 (MDM) 准备 Microsoft Intune

在深入了解 Intune 设置的详细信息之前，让我们回顾一下组织的移动设备管理要求。 它可能有助于在当前 MDM 提供程序中运行活动用户的报告，以识别关键用户组。 然后，就可以开始解决[评估 MDM 要求](migration-guide-prepare.md#assess-mdm-requirements)部分中提到的问题。

## <a name="assess-mdm-requirements"></a>评估 MDM 要求

### <a name="what-kinds-of-devices-do-you-need-to-manage"></a>你需要管理哪些类型的设备？

- 需要支持哪些[平台](supported-devices-browsers.md)？

- 这些是不是需要用来支持公司或个人的设备？

- 使用哪种连接？ Wi-Fi、手机网络还是 VPN？

### <a name="what-do-your-users-need-to-do-on-managed-devices"></a>用户需要在受管理设备上执行哪些操作？

- 是否需要为最终用户预配应用？

- 是否使用自定义业务线应用？ 或者，你是否只需要公共应用商店应用？

- 是否需要预配电子邮件帐户？

### <a name="what-kinds-of-users"></a>用户属于哪些类型？

- 一台设备将由多少用户使用？

- 需要哪些使用条款？

  - 请务必让法律部门尽早参与到其中。
  - 何种本地化是必需的？

- 用户是否熟悉常规技术和 IT？

### <a name="what-is-your-device-security-policy"></a>什么是设备安全策略？

- 是否需要设备级别的加密？

- 当前使用的设备密码/PIN 码长度是？

- 是否需要禁用设备功能，或限制某些设备行为？ 可通过设备配置配置文件控制各种特定于平台的设置，例如：
  - 禁用摄像头
  - 锁定到单应用模式<br/>

- 必须支持哪些类型的身份验证？ 如果需要基于证书的身份验证，必须预配哪些类型的证书？
  - Intune 可以为注册设备预配具备资源访问配置文件的证书。
  - 你需要支持哪种类型的公钥基础结构 (PKI)？
  <br></br>
- 是否需要支持设备或应用级别的虚拟专用网 (VPN)？

  - Intune 可以预配第三方 VPN 提供程序的 VPN 配置。
  <br/><br/>
- 是否可以针对某些要求允许临时异常来避免故障时间？ 或者，具有访问权限的设备是否必须始终符合所有安全要求？

## <a name="next-steps"></a>后续步骤
请阅读来自各行业领域的[案例研究](https://customers.microsoft.com/story/mwh-global-now-part-of-stantec-secures-mobile-devices-with-intune)，了解组织如何评估其移动设备管理要求。

查看[基本 Intune 设置](migration-guide-setup.md)。
