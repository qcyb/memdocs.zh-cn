---
title: iOS/iPadOS 用户如何获取其应用
description: 使 iOS/iPadOS 应用可供最终用户使用的方法
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7e3135c1-df26-48c9-aa4c-cdab6168897a
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 957c63c760dcc576ab30bb85440d52833307818d
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79344085"
---
# <a name="how-your-iosipados-users-get-their-apps"></a>iOS/iPadOS 用户如何获取其应用

使用此信息可了解最终用户如何以及在何处获取你通过 Microsoft Intune 分发的应用。

**必需应用** -- 管理员所要求并且在用户参与程度最小的情况下安装在设备上的应用（具体取决于平台）。

**可用应用** -- 在公司门户应用列表中提供的应用和用户可以根据需要选择安装的应用。

**托管应用** - 可通过策略管理，并由 Intune“包装”或使用 Intune 应用软件开发工具包 (SDK) 生成的应用。 这些应用可以由 Intune 进行管理，应用保护策略可以应用于它们。

**非托管应用** - 用户可从 iOS/iPadOS App Store 下载的未与 Intune 应用 SDK 集成的应用。 Intune 不能控制这些应用的分发、管理或选择性擦除。  

在公司门户应用上的“应用”屏幕上，已注册用户可以通过点击以下磁贴获取他们的应用：

- **所有应用**指向[公司门户网站](https://portal.manage.microsoft.com)“全部”选项卡中所有应用的列表。

- **特色应用**使用户进入公司门户网站的“特别推荐”选项卡。

- **类别**指向公司门户网站的“类别”选项卡。

![iOS 公司门户应用屏幕](./media/end-user-apps-ios/ios-cp-app-main-apps-screen.png)

有关如何添加应用的相关信息，请参阅[如何将应用添加到 Microsoft Intune](../apps/apps-add.md)。

## <a name="app-management-takeover"></a>应用管理接管
如果某个应用已安装在最终用户的设备上，则 iOS/iPadOS 设备将显示一个警报，以允许组织对应用进行管理。 最终用户必须允许组织对应用进行管理，然后才能将应用配置应用到托管设备。 如果用户取消了警报，但只要管理设备并分配应用，就会定期显示警报。  


![“应用管理更改”警报的图像，其中显示了“取消”和“管理”选项。](./media/end-user-apps-ios/intune-app-management-confirmation-2002.png)

## <a name="see-also"></a>另请参阅  

[Android 用户如何获取其应用](end-user-apps-android.md)

[Windows 用户如何获取其应用](end-user-apps-windows.md)
