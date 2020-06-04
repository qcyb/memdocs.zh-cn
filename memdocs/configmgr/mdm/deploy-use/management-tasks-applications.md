---
title: 为本地 MDM 管理应用
titleSuffix: Configuration Manager
description: 为 Configuration Manager 中的本地移动设备管理（MDM）管理应用程序。
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f9fafcc4b5462afb1b8e528837ea6ba61203e73d
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347129"
---
# <a name="manage-apps-for-on-premises-mdm-in-configuration-manager"></a>为 Configuration Manager 中的本地 MDM 管理应用

适用范围：  Configuration Manager (Current Branch)

当你通过 Configuration Manager 本地移动设备管理（MDM）管理设备时，你可以管理以下应用程序类型：

- Windows Phone 应用包（*.xap 文件）
- Windows Phone 应用包（在 Windows Phone 应用商店中）
- 通过 MDM 的 Windows 安装程序
- Web 应用程序

有关管理 Configuration Manager 应用程序和部署类型的更多常规信息，请参阅[Configuration Manager 应用程序的管理任务](../../apps/deploy-use/management-tasks-applications.md)。

## <a name="create-windows-phone-application"></a><a name="bkmk_winphone"></a>创建 Windows Phone 应用程序

Configuration Manager 应用程序具有一个或多个部署类型。 部署类型包括将软件部署到设备所需的安装文件和信息。 部署类型还具有指定软件的部署时间和方法的规则。

有关创建应用和部署类型的一般步骤，请参阅[创建应用程序](../../apps/deploy-use/create-applications.md#bkmk_create)。

Configuration Manager 支持适用于 Windows 移动设备的以下应用文件类型：

|设备类型|支持的文件类型|
|-----------------|---------------------|
|Windows Phone 8|xap|
|Windows Phone 8.1|xap, appx, appxbundle|
|Windows 10 移动版|xap, appx, appxbundle|

将 Windows Phone 应用部署为“可用”或“必需”********。 还可使用部署来卸载应用。

## <a name="deploy-and-monitor-apps"></a>部署和监视应用

为中的移动设备部署和监视应用程序 Configuration Manager 与在其他设备（如桌面和服务器）中相同。 有关详细信息，请参阅下列文章：

- [部署应用程序](../../apps/deploy-use/deploy-applications.md)
- [监视应用程序](../../apps/deploy-use/monitor-applications-from-the-console.md)

查看特定于移动设备的以下限制：

- 已注册 MDM 的设备不支持模拟部署、用户体验或计划设置。

- 不要向单个应用添加超过100的区域设置。 此操作可防止在设备上安装应用。

## <a name="next-step"></a>后续步骤

若要使用新应用程序进行更改、卸载或替换已部署的应用程序，请将其管理 Configuration Manager 中的任何应用。 有关详细信息，请参阅 [修改和取代应用程序](../../apps/deploy-use/revise-and-supersede-applications.md)。
