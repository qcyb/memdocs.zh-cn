---
title: BitLocker 疑难解答
titleSuffix: Configuration Manager
description: 了解如何排查 Configuration Manager 中的 BitLocker 管理问题
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: troubleshooting
ms.assetid: 134c5b50-edeb-4d60-aaca-944d26deb9ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0158738f77a0070835bec2385dd85c42dfd763fd
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127808"
---
# <a name="troubleshoot-bitlocker"></a>BitLocker 疑难解答

适用范围：  Configuration Manager (Current Branch)

本文中的信息可帮助你排查 Configuration Manager 中的 BitLocker 管理问题。

## <a name="server-error-in-self-service"></a>自助服务中出现服务器错误

在你首次尝试打开自助服务门户 (`https://webserver.contoso.com/SelfService`) 时，你会看到以下错误消息：

``` error
Configuration Error - Server Error in '/SelfService' Application

Description: An error occurred during the processing of a configuration file required to service this request. Please review the specific error details below and modify your configuration file appropriately.

Parser Error Message: Could not load file or assembly 'System.Web.Mvc, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.
```

要解决此问题，请确保在 Web 服务器上安装了 Microsoft ASP.NET MVC 4.0 的[必备项](../../plan-design/bitlocker-management.md#prerequisites)。

## <a name="see-also"></a>请参阅

要详细了解如何使用 BitLocker 事件日志，请参阅 [BitLocker 事件日志](about-event-logs.md)。

有关事件日志条目的已知错误和可能原因列表，请参阅以下文章：

- [客户端事件日志](client-event-logs.md)
- [服务器事件日志](server-event-logs.md)

若要了解客户端报告不符合 BitLocker 管理策略的原因，请参阅[不符合性代码](non-compliance-codes.md)。
