---
title: 适用于 Windows Phone 8.1 的 Microsoft Intune 电子邮件设置
titleSuffix: ''
description: 了解可用于在运行 Windows Phone 8.1 的设备上配置电子邮件连接的 Intune 设置。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 3/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 369e856b26ecbf8a7d6d7f8c0a87a9bfdf69e318
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086930"
---
# <a name="email-profile-settings-in-microsoft-intune-for-devices-running-windows-phone-81"></a>Microsoft Intune 中适用于运行 Windows Phone 8.1 的设备的电子邮件配置文件设置

本文介绍可为运行 Windows Phone 8.1 的设备配置的电子邮件配置文件设置。

>[!IMPORTANT]
>Windows Phone 8.1 电子邮件配置文件也适用于 Windows 10 设备。

## <a name="before-you-begin"></a>在开始之前

[创建 Windows Phone 8.1 电子邮件配置文件](email-settings-configure.md)。

## <a name="email-settings"></a>电子邮件设置

- **电子邮件服务器**：输入 Exchange 服务器的主机名。 例如，输入 `outlook.office365.com`。
- **帐户名**：输入电子邮件帐户的显示名称。 该名称将显示在用户的设备上。
- **AAD 中的用户名属性**：此名称是 Intune 从 Azure Active Directory (AAD) 获取的属性。 Intune 将动态生成此配置文件使用的用户名。 选项包括：
  - **用户主体名称**：获取名称，如 `user1` 或 `user1@contoso.com`。
  - **主 SMTP 地址**：获取格式为电子邮件地址的名称，如 `user1@contoso.com`。
  - **SAM 帐户名**：需要域，如 `domain\user1`。 此外请输入：
    - **用户域名源**：选项包括：
      - **AAD** (Azure Active Directory)：输入“AAD 中的用户域名属性”  。 选择以获取用户的“完整域名”  或“NetBIOS 名称”  属性。
      - **自定义**：输入“要使用的自定义域名”  。 输入 Intune 用于域名的值，如 `contoso.com` 或 `contoso`。

- **AAD 中的电子邮件地址属性**：Intune 从 Azure Active Directory (AAD) 获取此属性。 选择用户电子邮件地址的生成方式。 选项包括：
  - **用户主体名称**：使用完整的主体名称作为电子邮件地址，如 `user1@contoso.com` 或 `user1`。
  - **主 SMTP 地址**：使用主 SMTP 地址登录 Exchange，如 `user1@contoso.com`。

## <a name="security-settings"></a>安全设置

- **SSL**：选择“启用”后，可在发送电子邮件、接收电子邮件以及与 Exchange 服务器通信时使用安全套接字层 (SSL) 通信  。 “禁用”  不需要 SSL。

## <a name="synchronization-settings"></a>同步设置

- **要同步的电子邮件数**：选择你想要同步的电子邮件的天数。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 选择“无限制”  ，以同步所有可用的电子邮件。
- **同步计划**：选择设备同步 Exchange 服务器中数据的计划。 还可以选择“当邮件到达时”  ，这会在邮件达到时立即同步数据。 或者，选择“手动”  ，以便设备用户开始同步。

## <a name="content-sync-settings"></a>内容同步设置

- **要同步的内容类型**：选择想要同步到设备的内容类型：
  - **联系人**：“开”  会同步联系人。 “关”  不会自动同步联系人。 用户手动同步。
  - **日历**：“开”  会同步日历。 “关”  不会自动同步联系人。 用户手动同步。
  - **任务**：“开”  会同步任务。 “关”  不会自动同步任务。 用户手动同步。

## <a name="next-steps"></a>后续步骤

还可以在 [Android](email-settings-android.md)、[Android Enterprise](email-settings-android-enterprise.md)、[iOS/iPadOS](email-settings-ios.md) 和 [Windows 10](email-settings-windows-10.md) 上配置电子邮件设置。

[在 Intune 中配置电子邮件设置](email-settings-configure.md)。
