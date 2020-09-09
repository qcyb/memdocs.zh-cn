---
title: Windows Autopilot 注册状态页
ms.reviewer: ''
manager: laurawi
description: 概述注册状态页功能，配置
keywords: Autopilot 即插即用，Windows 10
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: deploy
ms.localizationpriority: medium
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: a7d368aef0b10fbe78e2c4ca141a39aa4ed6d803
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606602"
---
# <a name="windows-autopilot-enrollment-status-page"></a>Windows Autopilot 注册状态页

**适用于**

-  Windows 10 版本 1803 及更高版本 

用户第一次登录设备时，"注册状态" 页 (ESP) 显示设备的配置进度。 ESP 还可以确保设备在用户首次访问桌面之前处于预期状态。

ESP 跟踪应用程序、安全策略、证书和网络连接的安装。 管理员可以将 ESP 配置文件部署到许可的 Intune 用户，并在 ESP 配置文件中配置特定设置。 其中一些设置为：
- 强制安装指定的应用程序。
- 允许用户收集疑难解答日志。
- 指定用户在设备安装失败时可以执行的操作。

有关详细信息，请参阅如何 [在 Intune 中设置注册状态页](/intune/windows-enrollment-status)。  
 
![注册状态页](images/enrollment-status-page.png)
 

## <a name="more-information"></a>详细信息

有关配置 "注册状态" 页的详细信息，请参阅 [Microsoft Intune 文档](/intune/windows-enrollment-status)。<br>
有关基础实现的详细信息，请参阅 [DMCLIENT CSP 文档中的 FirstSyncStatus 详细信息](/windows/client-management/mdm/dmclient-csp)。<br>
有关应用程序安装阻止的详细信息，请执行以下操作：
- 正在[使用注册状态页阻止应用程序安装](/archive/blogs/mniehaus/blocking-for-app-installation-using-enrollment-status-page)。
- [支持提示：现在，在 ESP 期间跟踪 OFFICE C2R 安装](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Office-C2R-installation-is-now-tracked-during-ESP/ba-p/295514)。
