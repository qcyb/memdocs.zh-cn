---
title: 本地 MDM
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中的本地移动设备管理（MDM）
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 38d68447093d098f1a8157a2e18e19a6c4f88364
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724671"
---
# <a name="on-premises-mdm-in-configuration-manager"></a>Configuration Manager 中的本地 MDM

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 本地移动设备管理（MDM）是一个设备管理解决方案，它依赖于 Windows 的内置管理功能。 此功能基于开放移动联盟（OMA）设备管理（DM）标准。 它使用组织的 Configuration Manager 基础结构来管理和维护设备。 你的组织需要 Microsoft Intune 许可证才能使用此功能，但它不需要任何云连接。 Configuration Manager 将有关你的设备的所有数据存储在本地站点数据库中。

本地 MDM 与 Microsoft Intune 不同，后者还依赖于内置的 OMA DM 功能。 Intune 中的所有管理功能都通过云服务提供。 本地 MDM 也不同于传统的基于客户端的管理解决方案 Configuration Manager 提供。 它依赖于类似的基础结构，但不会在它所管理的设备上使用单独安装的客户端软件。  

## <a name="comparison"></a>比较

以下各部分列出了本地 MDM 的优点和缺点，与传统的基于客户端的管理相比：  

### <a name="advantages"></a>优点

- **简化的基础结构**：需要的站点系统角色更少。

- **更易于维护**：由于管理功能是内置于设备操作系统的，因此当向站点引入新的管理功能时，不需要新版本的 Configuration Manager 客户端。

- **本地**：-所有管理和数据均保留在本地。

### <a name="disadvantages"></a>缺点

**更少的客户端管理功能**：无业务流程、软件计数、第三方集成、任务序列或软件中心支持。

- **有限设备支持**：本地 MDM 不支持与 Configuration Manager 客户端一样多的操作系统版本。 有关详细信息，请参阅[客户端和设备支持的 OS 版本](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS)。

## <a name="next-step"></a>后续步骤

了解在本地 MDM 中设置 Configuration Manager 基础结构和规划设备注册时要考虑的事项。

> [!div class="nextstepaction"]
> [规划本地 MDM](../plan-design/plan-on-premises-mdm.md)  
