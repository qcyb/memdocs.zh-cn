---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: c576a4466ce8685cb440d8c804c9a675fbbecb8b
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126440"
---
### <a name="endpoints-required-for-configuration-manager-managed-devices"></a>Configuration Manager 管理的设备所需的终结点

Configuration Manager 管理的设备通过 Configuration Manager 角色上的连接器将数据发送到 Intune，它们不需要直接访问 Microsoft 公有云。

| 终结点  | 函数  |
|-----------|-----------|
| `https://graph.windows.net` | 用于在 Configuration Manager 服务器角色上将层次结构附加到终结点分析时自动检索设置。 有关详细信息，请参阅[配置站点系统服务器的代理](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server)。 |
| `https://*.manage.microsoft.com` | 用于仅在 Configuration Manager 服务器角色上同步设备集合和设备与终结点分析。 有关详细信息，请参阅[配置站点系统服务器的代理](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server)。 |

### <a name="endpoints-required-for-intune-managed-devices"></a>Intune 管理的设备所需的终结点

若要向终结点分析注册设备，它们需要将所需的功能数据发送到 Microsoft 公有云。 终结点分析使用 Windows 10 和 Windows Server 已连接的用户体验和遥测组件 (DiagTrack) 从 Intune 管理的设备收集数据。 确保设备上的“已连接的用户体验和遥测”服务正在运行。

| 终结点  | 函数  |
|-----------|-----------|
| `https://*.events.data.microsoft.com` | 由 Intune 管理的设备使用，用于将[必需的功能数据](../../../../../analytics/data-collection.md#bkmk_datacollection)发送到 Intune 数据收集终结点。 |
