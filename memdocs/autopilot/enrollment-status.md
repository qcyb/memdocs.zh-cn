---
title: Windows Autopilot 注册状态页
ms.reviewer: ''
manager: laurawi
description: 概述注册状态页功能，配置
keywords: Autopilot 即插即用，Windows 10
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
ms.openlocfilehash: dd60c47e0e22aa24cf1d4d4df3324f3b1bfed21c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908251"
---
# <a name="windows-autopilot-enrollment-status-page"></a>Windows Autopilot 注册状态页

**适用于**

-   Windows 10 版本 1803 及更高版本 

"注册状态" 页 (ESP) 显示在 MDM 管理的用户首次登录设备时完成设备配置过程的状态。  ESP 将帮助用户了解设备预配的进度，并确保设备在用户首次访问桌面之前已经满足组织所需的状态。

ESP 将跟踪应用程序的安装、安全策略、证书和网络连接。  使用 Intune，管理员可以将 ESP 配置文件部署到已获许可的 Intune 用户，并配置 ESP 配置文件中的特定设置;其中的几个设置是：强制安装指定的应用程序，允许用户收集疑难解答日志，指定用户在设备安装失败的情况下可以执行的操作。  有关详细信息，请参阅如何 [在 Intune 中设置注册状态页](/intune/windows-enrollment-status)。   
 
 ![注册状态页](images/enrollment-status-page.png)
 

## <a name="more-information"></a>详细信息

有关配置 "注册状态" 页的详细信息，请参阅 [Microsoft Intune 文档](/intune/windows-enrollment-status)。<br>
有关基础实现的详细信息，请参阅 [DMCLIENT CSP 文档中的 FirstSyncStatus 详细信息](/windows/client-management/mdm/dmclient-csp)。<br>
有关应用程序安装阻止的详细信息，请执行以下操作：
- 正在[使用注册状态页阻止应用程序安装](/archive/blogs/mniehaus/blocking-for-app-installation-using-enrollment-status-page)。
- [支持提示：现在，在 ESP 期间跟踪 OFFICE C2R 安装](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Office-C2R-installation-is-now-tracked-during-ESP/ba-p/295514)。