---
title: 添加适用于 macOS 的公司门户应用
titleSuffix: Microsoft Intune
description: 添加 macOS 公司门户应用。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/16/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a58e22af70a3cf119cb044a15b40ba581fe6452c
ms.sourcegitcommit: 5c15b59cde085787b85f032f88add70a11d8e9a2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2020
ms.locfileid: "86452841"
---
# <a name="add-the-macos-company-portal-app"></a>添加 macOS 公司门户应用

要管理设备、安装可选应用并获得受具有用户关联性的 macOS 设备上的条件访问保护的资源的访问权限，用户必须安装并登录公司门户应用。 你可以向用户提供说明，以安装适用于 macOS 的公司门户或将其安装在直接从 Intune 注册的设备上。

你可以使用以下任何选项来安装适用于 macOS 的公司门户应用：
- [指导用户下载并安装公司门户](#instruct-users-to-download-and-install-company-portal)
- [将适用于 macOS 的公司门户安装为 macOS LOB 应用](#install-company-portal-for-macos-as-a-macos-lob-app)
- [使用 macOS Shell 脚本安装适用于 macOS 的公司门户](#install-company-portal-for-macos-by-using-a-macos-shell-script)

为帮助确保应用安装后更安全和最新，公司门户应用随附 Microsoft 自动更新 (MAU)。

> [!NOTE]
> 公司门户应用只能自动安装在使用 Intune 的设备上，而这些设备已通过直接注册或自动设备注册进行了注册。 对于个人设备或手动注册，必须下载并安装公司门户应用才能启动注册。 请参阅[指导用户下载并安装公司门户](#instruct-users-to-download-and-install-company-portal)。
## <a name="instruct-users-to-download-and-install-company-portal"></a>指导用户下载并安装公司门户

你可以指导用户下载、安装和登录适用于 macOS 的公司门户。 有关下载、安装和登录公司门户的说明，请参阅 [使用公司门户应用注册 macOS 设备](https://docs.microsoft.com/mem/intune/user-help/enroll-your-device-in-intune-macos-cp)。

##  <a name="install-company-portal-for-macos-as-a-macos-lob-app"></a>将适用于 macOS 的公司门户安装为 macOS LOB 应用

可以使用 [macOS LOB 应用](lob-apps-macos.md)功能下载和安装适用于 macOS 的公司门户。 下载的版本是将始终安装的版本，可能需要定期进行更新以确保用户在初始注册期间获得最佳体验。

1. 从 https://go.microsoft.com/fwlink/?linkid=853070 下载适用于 macOS 的公司门户。 

2. 请按照 [macOS LOB 应用](lob-apps-macos.md)中的“创建 macOS LOB 应用”说明进行操作。

> [!NOTE]
> 安装后，适用于 macOS 的公司门户应用将使用 Microsoft AutoUpdate (MAU) 自动更新。
## <a name="install-company-portal-for-macos-by-using-a-macos-shell-script"></a>使用 macOS Shell 脚本安装适用于 macOS 的公司门户

可以使用 [macOS Shell 脚本](macos-shell-scripts.md)功能下载和安装适用于 macOS 的公司门户。 此选项将始终安装适用于 macOS 的当前版本的公司门户，但不会为你提供使用 [macOS LOB 应用](lob-apps-macos.md)部署应用程序时可能使用的应用程序安装报告。

1. 从 [Intune Shell 脚本示例 - 公司门户](https://github.com/microsoft/shell-intune-samples/tree/master/Apps/Company%20Portal)下载用于安装适用于 macOS 的公司门户的示例脚本。

2. 按照使用 [macOS Shell 脚本](macos-shell-scripts.md)部署 macOS Shell 脚本的说明进行操作。 
    - 将“以登录用户身份运行脚本”设置为“否”（在系统上下文中运行） 。
    - 将“脚本失败后重试的最大次数”设置为“3” 。

> [!NOTE]
> 此脚本在运行时需要 Internet 访问权限，以便下载最新版适用于 macOS 的公司门户。 
## <a name="next-steps"></a>后续步骤
- 如需了解有关分配应用的详细信息，请参阅[将应用分配给组](apps-deploy.md)。
- 如需深入了解有关配置自动设备注册的信息，请参阅[设备注册程序 - 注册 macOS](https://docs.microsoft.com/mem/intune/enrollment/device-enrollment-program-enroll-macos)。
- 如需深入了解在 macOS 上配置 Microsoft 自动更新设置的信息，请参阅 [Mac 更新](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/mac-updates)。