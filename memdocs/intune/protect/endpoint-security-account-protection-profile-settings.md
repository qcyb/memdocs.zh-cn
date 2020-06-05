---
title: Intune 终结点安全帐户保护策略设置 | Microsoft Docs
description: Microsoft Intune 中的终结点安全帐户保护策略设置
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: f4e67c434af9eb7f88c3e7d3997ef7c7d829c860
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431990"
---
# <a name="account-protection-policy-settings-for-endpoint-security-in-intune"></a>Intune 中的终结点安全帐户保护策略设置

查看可以在 Intune 终结点安全节点“帐户保护”策略的配置文件中作为[终结点安全策略](../protect/endpoint-security-policy.md)的一部分进行配置的设置。

受支持的平台和配置文件：

- **Windows 10 及更高版本**：
  - 配置文件：**帐户保护**（预览）


## <a name="account-protection-profile"></a>帐户保护配置文件

### <a name="account-protection"></a>帐户保护

- **阻止 Windows Hello 企业版**

  Windows Hello 企业版是一种取代密码、智能卡和虚拟智能卡登录 Windows 的替代方法。
  - **未配置**（默认）- 设备预配 Windows Hello 企业版。
  - **禁用** - 设备预配 Windows Hello 企业版。
  - **启用** - 设备不为任何用户预配 Windows Hello 企业版
  
- **启用以使用安全密钥登录**

  启用 Windows Hello 安全密钥作为租户中所有电脑的登录凭据。
  - **未配置**（默认）
  - **是**

- **启用 Credential Guard**  
  [CSP: []DeviceGuard](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard 使用 Windows 虚拟机监控程序提供保护。 Credential Guard 要求硬件支持安全启动和 DMA 保护。 此设置仅在满足硬件要求的设备上成功。
  - **未配置**（默认） - 禁用 Credential Guard，这是 Windows 的默认设置。
  - **启用且具有 UEFI 锁定** - 启用 Credential Guard 并阻止远程关闭它，因为必须手动清除 UEFI 保存的配置。
  - 启用但不具有 UEFI 锁定 - 启用 Credential Guard，并允许在没有对计算机进行物理访问的情况下将其关闭。

## <a name="next-steps"></a>后续步骤

[帐户保护的终结点安全策略](../protect/endpoint-security-account-protection-policy.md)
