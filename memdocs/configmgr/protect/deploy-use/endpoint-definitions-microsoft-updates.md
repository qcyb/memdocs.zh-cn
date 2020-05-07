---
title: 从 Microsoft 下载定义
titleSuffix: Configuration Manager
description: 了解如何可以实现从 Microsoft 更新为 Configuration Manager 下载 Endpoint Protection 的恶意软件定义。
ms.date: 11/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1f0d8ac635d514e750584126458bfde6b5fc24ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697235"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates"></a>启用 Endpoint Protection 恶意软件定义，以便从 Microsoft 更新下载定义

适用范围：  Configuration Manager (Current Branch)

当你选择从 Microsoft 更新下载定义更新时，客户端将按照反恶意软件策略对话框的“安全智能更新”  部分定义的间隔检查 Microsoft 更新网站。

 当客户端不具有到 Configuration Manager 站点的连接或当你希望用户能够启动定义更新时，此方法会很有用。

> [!IMPORTANT]
> - 客户端必须在 Internet 上具有对 Microsoft 更新的访问权限，才能够使用此方法下载定义更新。
> - 自 Configuration Manager 版本 1902 起，“定义更新”  部分已重命名为“安全智能更新”  。

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>使用 Microsoft 恶意软件防护中心下载定义
 你可以将客户端配置为从 Microsoft 恶意软件防护中心下载定义更新。 如果 Endpoint Protection 客户端未能够从另一源下载更新，则使用此选项下载定义更新。 如果 Configuration Manager 基础结构存在阻止更新交付的问题，此更新方法会很有用。

> [!IMPORTANT]
>  客户端必须在 Internet 上具有对 Microsoft 更新的访问权限，才能够使用此方法下载定义更新。
> 
> 
> [!div class="button"]
> [下一步 >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [返回 >](endpoint-configure-alerts.md)
