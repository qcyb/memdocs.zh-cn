---
title: Office 应用策略
titleSuffix: Microsoft Intune
description: 了解适用于 Office 应用的策略。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: ca558b40ad3d006aa764819a0fbccc16a03fd0e2
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2020
ms.locfileid: "89644020"
---
# <a name="policies-for-office-apps"></a>Office 应用策略

Intune 提供专用于 Microsoft Office 应用的策略。 可以选择特定选项，为连接到 Microsoft 365 服务的 Office 移动应用创建移动应用管理策略。 有许多适用于 Office 应用的策略，可以将它们添加到 Microsoft Intune 并应用于最终用户组。

下面是一些 Office 应用策略的示例：
- Microsoft Word：为从 Outlook 打开的附件禁用受保护的视图
- Microsoft Visio：禁止宏在来自 Internet 的 Office 文件中运行
- Microsoft Project：允许网络上的受信任位置
- Microsoft Publisher：Publisher 自动化安全级别
- Microsoft PowerPoint：为从 Outlook 打开的附件禁用受保护的视图

> [!NOTE]
> 当你选择配置每个特定应用策略时，会获得其他策略详细信息。 可以筛选 Office 策略列表以快速选择建议的安全基线策略。

此外，还可以通过为启用了混合现代身份验证的 iOS/iPadOS 和 Android 的 Outlook 创建 Intune 应用保护策略来保护对 Exchange 本地邮箱的访问。 在使用此功能之前，必须满足使用 Office 云策略服务的要求。 连接到本地 Exchange 或 SharePoint 服务的其他应用不支持应用保护策略。 要了解相关信息，请参阅[适用于 Microsoft 365 企业应用版的 Office 云策略服务概述](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service)。

## <a name="prerequisites"></a>先决条件

必须满足使用 Office 应用策略的要求。 有关详细信息，请参阅[使用 Office 云策略服务的要求](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service#requirements-for-using-the-office-cloud-policy-service)。

## <a name="to-add-an-office-app-policy"></a>添加 Office 应用策略

设置组织的 Intune 后，可以创建 Office 应用策略。

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“应用” > “Office 应用策略” > “创建”。
3. 添加下列值：
    - **名称：** 键入新策略的名称（必填）。
    - **描述：** （可选）键入说明。
    - 选择类型：选择将如何应用此策略配置。
    - 选择组：选择此策略配置的组。
    - 配置策略：选择要应用的 Office 策略。 可以根据策略、平台、应用程序、建议和状态对提供的列表进行排序。
4. 选择“创建”。 此时会创建策略，并在“策略配置”窗格的表中显示该策略。

   > [!TIP]
   > “策略配置”窗格提供每个策略的运行状况状态。

## <a name="additional-information"></a>其他信息

- [适用于Microsoft 365 企业应用版的 Office 云策略服务概述](https://docs.microsoft.com/deployoffice/overview-office-cloud-policy-service)
- [使用策略设置来管理 Microsoft 365 企业应用版的隐私控件](https://docs.microsoft.com/deployoffice/privacy/manage-privacy-controls)
- [使用首选项来管理 Office for Mac 的隐私控件](https://docs.microsoft.com/deployoffice/privacy/mac-privacy-preferences)
- [使用首选项来管理 iOS 设备上 Office 的隐私控件](https://docs.microsoft.com/deployoffice/privacy/ios-privacy-preferences)
- [使用策略设置来管理 Android 设备上 Office 的隐私控件](https://docs.microsoft.com/deployoffice/privacy/android-privacy-controls)

## <a name="next-steps"></a>后续步骤

- [使用 Microsoft Intune 监视应用信息和分配](apps-monitor.md)