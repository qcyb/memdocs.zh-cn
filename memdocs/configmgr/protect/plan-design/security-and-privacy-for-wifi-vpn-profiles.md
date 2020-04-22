---
title: Wi-Fi 和 VPN 配置文件的安全和隐私
titleSuffix: Configuration Manager
description: 了解在 Configuration Manager 中管理设备的 Wi-Fi 和 VPN 配置文件的安全建议。
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a6f444e35e16a3b42414fdc6fbee50687cf76f2f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705975"
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Configuration Manager 中 Wi-Fi 和 VPN 配置文件的安全和隐私

适用范围：  Configuration Manager (Current Branch)

## <a name="security-recommendations"></a>安全建议

在管理设备的 Wi-Fi 和 VPN 配置文件时，请使用下列安全最佳做法。

### <a name="choose-the-most-secure-options-that-your-wi-fi-and-vpn-infrastructure-and-client-operating-systems-can-support"></a>选择 Wi-Fi 和 VPN 基础结构和客户端操作系统支持的最安全选项

Wi-Fi 和 VPN 配置文件提供了一种简便的方法来集中分发和管理设备已支持的 Wi-Fi 和 VPN 设置。 Configuration Manager 不会添加 Wi-Fi 或 VPN 功能。 确定、实施和遵循针对你的设备和基础结构提出的任何安全建议。

## <a name="privacy-information"></a>隐私信息

可以使用 Wi-Fi 和 VPN 配置文件将客户端设备配置为连接到 Wi-Fi 和 VPN 服务器。 然后，使用 Configuration Manager 评估这些设备在配置文件应用后是否合规。 管理点会将符合性信息发送到站点服务器，该信息存储在站点数据库中。 设备在将信息发送到管理点时会对其进行加密，但信息不会以加密格式存储在站点数据库中。 数据库将保留该信息，直到站点维护任务“删除过期的配置管理数据”  将其删除为止。 默认删除间隔是 90 天，但你可以更改它。 符合性信息不会被发送到 Microsoft。

默认情况下，设备不评估 Wi-Fi 和 VPN 配置文件。 此外，必须对配置文件进行配置，然后将其部署到用户。  

配置 Wi-Fi 或 VPN 配置文件前，请考虑隐私要求。  
