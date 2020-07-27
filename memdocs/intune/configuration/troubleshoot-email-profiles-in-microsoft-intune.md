---
title: Microsoft Intune 中的电子邮件配置文件疑难解答 - Azure | Microsoft Docs
description: 请参阅 Microsoft Intune 中电子邮件配置文件的常见问题和解决方案，包括重复的电子邮件配置文件和 Samsung KNOX 标准版 Android 设备上的错误。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/20/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: f5c944ea-32a6-48af-bb57-16d5f1f3c588
ROBOTS: ''
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 717ad28625b5eac97c26bcd09a21ef34250a7d39
ms.sourcegitcommit: d3992eda0b89bf239cea4ec699ed4711c1fb9e15
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86565710"
---
# <a name="common-issues-and-resolutions-with-email-profiles-in-microsoft-intune"></a>Microsoft Intune 中电子邮件配置文件的常见问题和解决方法

回顾一些常见电子邮件配置文件问题，并了解如何排查并解决这些问题。

## <a name="users-are-repeatedly-prompted-to-enter-their-password"></a>反复提示用户输入密码

反复提示用户输入电子邮件配置文件的密码。 如果使用证书对用户进行身份验证和授权，请检查所有证书配置文件的分配。 通常，这些证书配置文件分配给用户组，而非设备组。 如果其中一个证书配置文件未针对用户，则 Intune 会继续尝试部署电子邮件配置文件。

如果将电子邮件配置文件链分配给用户组，请确保将证书配置文件也分配给用户组。

## <a name="profiles-deployed-to-device-groups-show-errors-and-latency"></a>部署到设备组的配置文件显示错误和延迟

通常会将电子邮件配置文件分配给用户组。 在某些情况下，可能会将它们分配给设备组。

- 例如，如果希望将基于证书的电子邮件配置文件仅部署到 Surface 设备，而不部署到台式机。 这种情况下，就可以分配给设备组。 这些设备可能显示为不合规，可能会返回错误，也可能不会立即获取电子邮件配置文件。

  在此示例中，将创建电子邮件配置文件，并将该配置文件分配给设备组。 设备会重启，并且用户登录之前有延迟。 在此延迟期间，将部署分配给用户组的 PKCS 证书配置文件。 由于还没有用户，PKCS 证书配置文件导致设备不合规。 事件查看器也可能显示设备上的错误。

  若要变得合规，用户需要登录设备，并与 Intune 同步以接收策略。 用户可以手动重新同步，或等待下一次同步。

- 例如，使用动态组。 如果 Azure AD 不立即更新动态组，则这些设备可能显示为不合规。

在这些情况下，需要决定是使用设备组更重要，还是将所有策略显示为合规更重要。

## <a name="device-already-has-an-email-profile-installed"></a>设备已安装电子邮件配置文件

如果用户在 Intune 或 Office 365 MDM 中注册之前创建电子邮件配置文件，则 Intune 部署的电子邮件配置文件可能不会按预期方式工作：

- **iOS/iPadOS**：Intune 基于主机名和电子邮件地址检测到现有的重复电子邮件配置文件。 用户创建电子邮件配置文件会阻止部署 Intune 创建的配置文件。 这种情况是一个常见问题，因为 iOS/iPadOS 用户通常会创建一个电子邮件配置文件，然后进行注册。 公司门户应用指明用户不符合策略，并可能会提示用户删除电子邮件配置文件。

  用户应删除其电子邮件配置文件，以便可部署 Intune 配置文件。 若要避免此问题，请通知用户注册 Intune，并允许 Intune 部署电子邮件配置文件。 然后，用户可以创建其电子邮件配置文件。

- **Windows**：Intune 基于主机名和电子邮件地址检测到现有的重复电子邮件配置文件。 Intune 会覆盖由用户创建的现有电子邮件配置文件。

- **Samsung KNOX 标准版**：Intune 基于电子邮件地址识别重复的电子邮件帐户，并使用 Intune 配置文件将其覆盖。 如果用户配置该帐户，则 Intune 配置文件将再次覆盖该帐户。 此行为可能会导致其帐户配置被覆盖的用户感到困惑。

Samsung KNOX 不使用主机名识别配置文件。 不建议创建多个电子邮件配置文件以部署到不同主机上的同一电子邮件地址，因为这样会导致它们相互覆盖。

## <a name="error-0x87d1fde8-for-knox-standard-device"></a>KNOX 标准版设备的错误 0x87D1FDE8

**问题**：为不同的 Android 设备创建并部署适用于 Samsung KNOX 标准的 Exchange Active Sync 电子邮件配置文件后，设备的“属性”>“策略”选项卡中会显示错误“0x87D1FDE8”或“修正失败”。

请查看适用于 Samsung KNOX 的 EAS 配置文件的配置以及源策略。 Samsung Notes 同步选项不再受支持，因此，不应在配置文件中选择此选项。 确保设备有足够的时间处理策略，最多为 24 小时。

## <a name="unable-to-send-images-from--email-account"></a>无法从电子邮件帐户发送图像

自动配置了电子邮件帐户的用户无法从其设备发送图片或图像。 未启用“允许从第三方应用程序发送电子邮件”时，可能会发生此情况。

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备” > “配置文件”。
3. 选择电子邮件配置文件 >“属性” > “设置”。
4. 将“允许从第三方应用程序发送电子邮件”设置设为“启用”。

## <a name="next-steps"></a>后续步骤

[从 Microsoft 获取支持帮助](../fundamentals/get-support.md)，或使用[社区论坛](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune)。
