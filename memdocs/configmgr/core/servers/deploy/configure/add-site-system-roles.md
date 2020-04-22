---
title: 添加站点系统角色
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 站点系统角色，以及如何添加它们以扩展站点的功能和容量。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8a4ef1c4377e7b5ffba4ab0f04394ff1253c40df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704895"
---
# <a name="add-site-system-roles-for-configuration-manager"></a>为 Configuration Manager 添加站点系统角色

适用范围：  Configuration Manager (Current Branch)

每个 Configuration Manager 站点都支持多个站点系统角色。 每个角色可扩展站点的功能和容量，以为站点提供服务并管理设备和用户。 站点系统服务器上的每个站点系统角色必须来自同一站点。

Configuration Manager 不支持单一站点系统服务器上用于多个站点的站点系统角色。

> [!TIP]
> 如果不熟悉站点系统角色的基础知识或站点服务器、站点系统服务器和站点系统角色之间的差别，请参阅 [Configuration Manager 基础知识](../../../understand/fundamentals.md)。

以下文章详细介绍了安装站点系统角色的过程和相关详细信息：

- [安装站点系统角色](install-site-system-roles.md)：有关使用两个控制台中向导安装新站点系统角色的基本指南。

- [安装基于云的分发点](install-cloud-based-distribution-points-in-microsoft-azure.md)：使用 Microsoft Azure 托管部署到客户端的内容。

- [为本地移动设备管理 (MDM) 安装站点系统角色](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)：设置站点系统角色，以支持使用 Configuration Manager 本地 MDM 管理新式设备。

- [站点系统角色的配置选项](configuration-options-for-site-system-roles.md)：某些站点系统角色支持需要比用户界面中可以说明的更多详细信息的配置。

- [删除站点系统角色](../install/uninstall-sites-and-hierarchies.md#bkmk_role)：有关从站点系统服务器中删除角色的指南和过程。
