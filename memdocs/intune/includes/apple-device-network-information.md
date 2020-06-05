---
title: 包含文件
description: 包含文件
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 06/02/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: bc8bb79d4f950edc303fb12504ef1a4a8dda9a64
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347234"
---
## <a name="apple-device-network-information"></a>Apple 设备网络信息

|**用途**|**主机名（IP 地址/子网）**|**协议**|**端口**|
|------------|-----------|------------|-----------|
|检索并显示 Apple 服务器的内容|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br>\*.phobos.itunes-apple.com.akadns.net|HTTP|80|
|与 APNS 服务器通信|#-courier.push.apple.com<br>“#”是 0 到 50 范围内的一个随机数字。|TCP|5223 和 443|
|各种功能，包括访问 Internet、iTunes 商店、macOS 应用商店、iCloud、消息等。|phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net|HTTP/HTTPS|80 或 443|

有关详情，请参阅：

- [Apple 软件产品使用的 TCP 和 UDP 端口](https://support.apple.com/HT202944)
- [关于 macOS、iOS/iPadOS 和 iTunes 服务器主机连接和 iTunes 后台进程](https://support.apple.com/HT201999)
- [如果你的 macOS 和 iOS/iPadOS 客户端不获取 Apple 推送通知](https://support.apple.com/HT203609)