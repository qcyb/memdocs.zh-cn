---
title: Microsoft Intune 中的电子邮件配置文件疑难解答 - Azure | Microsoft Docs
description: 请参阅 Microsoft Intune 中电子邮件配置文件的常见问题和解决方案，包括重复的电子邮件配置文件和 Samsung KNOX 标准版 Android 设备上的错误。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
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
ms.openlocfilehash: 4d7e3b5b9a169baf336b0d4e7d8d66b06af38061
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79361414"
---
# <a name="common-issues-and-resolutions-with-email-profiles-in-microsoft-intune"></a>Microsoft Intune 中电子邮件配置文件的常见问题和解决方法

回顾一些常见电子邮件配置文件问题，并了解如何排查并解决这些问题。

## <a name="what-you-need-to-know"></a>须知内容

- 电子邮件配置文件是为注册设备的用户部署的。 为了配置电子邮件配置文件，Intune 会在注册期间使用用户的电子邮件配置文件中的 Azure Active Directory (AD) 属性。 [将电子邮件设置添加到设备](email-settings-configure.md)可能是一个不错的资源。
- 对于 Android Enterprise，使用托管 Google Play 商店部署 Gmail 或 Nine for Work。 [添加托管 Google Play 应用](../apps/apps-add-android-for-work.md)中列出了相关步骤。
- 适用于 iOS/iPadOS 和 Android 的 Microsoft Outlook 不支持电子邮件配置文件。 应为它们部署应用配置策略。 有关详细信息，请参阅 [Outlook 配置设置](../apps/app-configuration-policies-outlook.md)。
- 可能无法将针对设备组（不是用户组）的电子邮件配置文件传递到设备。 如果设备具有主要用户，则设备定位应正常工作。 如果电子邮件配置文件包括用户证书，请确保以用户组为目标。
- 系统可能会反复提示用户输入其电子邮件配置文件的密码。 在这种情况下，请检查电子邮件配置文件中引用的所有证书。 如果其中一个证书不是针对用户的，Intune 会重试部署电子邮件配置文件。

## <a name="device-already-has-an-email-profile-installed"></a>设备已安装电子邮件配置文件

如果用户在 Intune 或 Office 365 MDM 中注册之前创建电子邮件配置文件，则 Intune 部署的电子邮件配置文件可能不会按预期方式工作：

- **iOS/iPadOS**：Intune 基于主机名和电子邮件地址检测到现有的重复电子邮件配置文件。 用户创建电子邮件配置文件会阻止部署 Intune 创建的配置文件。 这是一个常见问题，因为 iOS/iPadOS 用户通常会创建电子邮件配置文件，然后注册。 公司门户应用指明用户不符合策略，并可能会提示用户删除电子邮件配置文件。

  用户应删除其电子邮件配置文件，以便可部署 Intune 配置文件。 若要避免此问题，请通知用户注册 Intune，并允许 Intune 部署电子邮件配置文件。 然后，用户可以创建其电子邮件配置文件。

- **Windows**：Intune 基于主机名和电子邮件地址检测到现有的重复电子邮件配置文件。 Intune 会覆盖由用户创建的现有电子邮件配置文件。

- **Samsung KNOX 标准版**：Intune 基于电子邮件地址识别重复的电子邮件帐户，并使用 Intune 配置文件将其覆盖。 如果用户配置该帐户，则 Intune 配置文件将再次覆盖该帐户。 这可能会让帐户配置被覆盖的用户感到困惑。

Samsung KNOX 不使用主机名识别配置文件。 不建议创建多个电子邮件配置文件以部署到不同主机上的同一电子邮件地址，因为这样会导致它们相互覆盖。

## <a name="error-0x87d1fde8-for-knox-standard-device"></a>KNOX 标准版设备的错误 0x87D1FDE8

**问题**：为不同的 Android 设备创建并部署适用于 Samsung KNOX 标准的 Exchange Active Sync 电子邮件配置文件后，设备的“属性”>“策略”选项卡中会显示错误“0x87D1FDE8”  或“修正失败”  。

请查看适用于 Samsung KNOX 的 EAS 配置文件的配置以及源策略。 Samsung Notes 同步选项不再受支持，因此，不应在配置文件中选择此选项。 确保设备有足够的时间处理策略，最多为 24 小时。

## <a name="unable-to-send-images-from--email-account"></a>无法从电子邮件帐户发送图像

自动配置了电子邮件帐户的用户无法从其设备发送图片或图像。 未启用“允许从第三方应用程序发送电子邮件”时，可能会发生此情况  。

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备”   > “配置文件”  。
3. 选择电子邮件配置文件 >“属性”   > “设置”  。
4. 将“允许从第三方应用程序发送电子邮件”  设置设为“启用”  。

## <a name="next-steps"></a>后续步骤

[从 Microsoft 获取支持帮助](../fundamentals/get-support.md)，或使用[社区论坛](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune)。
