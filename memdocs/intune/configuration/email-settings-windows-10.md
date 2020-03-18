---
title: Microsoft Intune 中适用于 Windows 10 设备的电子邮件设置 - Azure | Microsoft Docs
description: 创建使用 Exchange 服务器的设备配置电子邮件配置文件，并从 Azure Active Directory 检索属性。 还可启用 SSL，并使用 Microsoft Intune 在 Windows 10 设备上同步电子邮件和日程安排。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/29/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 86a792505a07a48d545ab0c5fd115f3aa8dae0eb
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79343630"
---
# <a name="email-profile-settings-for-devices-running-windows-10---intune"></a>适用于运行 Windows 10 的设备的电子邮件配置文件设置 - Intune

使用电子邮件配置文件设置可以在运行 Windows 10 的设备上配置邮件应用。

- **电子邮件服务器**：输入 Exchange 服务器的主机名。
- **帐户名**：输入电子邮件帐户的显示名称。 该名称将显示在用户的设备上。
- **AAD 中的用户名属性**：此名称是 Intune 从 Azure Active Directory (AAD) 获取的属性。 Intune 将动态生成此配置文件使用的用户名。 选项包括：
  - **用户主体名称**：获取名称，如 `user1` 或 `user1@contoso.com`
  - **主 SMTP 地址**：获取格式为电子邮件地址的名称，如 `user1@contoso.com`
  - **SAM 帐户名**：需要域，如 `domain\user1`。

    此外请输入：  
    - **用户域名源**：选择“AAD”  (Azure Active Directory) 或“自定义”  。

      选择从 AAD 获取属性时，请输入  ：
      - **AAD 中的用户域名属性**：选择获取用户的“完整域名”  或“NetBIOS 名称”  属性

      选择使用自定义属性时，请输入  ：
      - **要使用的自定义域名**：输入 Intune 用于域名的值，如 `contoso.com` 或 `contoso`

- **AAD 中的电子邮件地址属性**：选择用户电子邮件地址的生成方式。 选择“用户主体名称”（`user1@contoso.com` 或 `user1`）以使用完整主体名称作为电子邮件地址，或选择“主 SMTP 地址”(`user1@contoso.com`) 以使用主 SMTP 地址登录到 Exchange   。

## <a name="security-settings"></a>安全设置

- **SSL**：发送电子邮件、接收电子邮件以及与 Exchange Server 通信时，请使用安全套接字层 (SSL) 通信。

## <a name="synchronization-settings"></a>同步设置

- **要同步的电子邮件数**：选择你想要同步的电子邮件的天数。 或选择“无限制”以同步所有可用的电子邮件  。
- **同步计划**：选择设备同步 Exchange 服务器中的数据的时间表。还可以选择“在邮件到达时”（在邮件到达时同步数据），或选择“手动”（设备用户必须启动同步）   。

## <a name="content-sync-settings"></a>内容同步设置

- **要同步的内容类型**：选择要从以下项同步到设备的内容类型：
  - **联系人**
  - **日历**
  - **任务**

## <a name="next-steps"></a>后续步骤
[在 Intune 中配置电子邮件设置](email-settings-configure.md)
