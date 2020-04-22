---
title: 软件中心的共享应用程序
titleSuffix: Configuration Manager
description: 在 Configuration Manager 的软件中心共享应用程序链接。
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: be2e930e3f59bc5a4d7db9e27ce2f875814fd358
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689235"
---
# <a name="share-an-application-from-software-center"></a>从软件中心共享应用程序

适用范围：  Configuration Manager (Current Branch) <!-- 1706 -->

可以使用软件中心“应用程序详细信息”视图中的 ![Share](media/share15.png)“共享”  按钮复制应用程序的超链接。 只能共享应用程序的超链接。 如果应用程序不再可用，则超链接打开的窗口将显示应用程序不可用的消息。

1. 选择“应用程序”  ，然后选择相应的应用程序。
2. 单击![共享](media/share15.png)“共享”  按钮。
3. 单击窗口中的“复制”  。
4. 将 URL 粘贴到电子邮件中，以共享此应用程序。  

> [!TIP]  
>  要在 Outlook 电子邮件中创建链接，请按下“Ctrl” + “K”，然后粘贴该 URL   。  
>  
> 默认情况下，Outlook 会在收件人单击链接时显示软件中心协议的安全警报。 可通过向注册表添加可信协议密钥防止在环境中出现这种情况。 例如 `HKCU\Software\Policies\Microsoft\Office\16.0\Common\Security\Trusted Protocols\All Applications\softwarecenter:`  
