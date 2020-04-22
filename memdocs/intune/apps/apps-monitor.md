---
title: 监视应用信息和分配
titleSuffix: Microsoft Intune
description: 将应用分配给用户或设备后，请使用此信息来帮助你监视应用状态。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 64e5133d-1e23-4ee6-b556-f5d32c0e95da
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c505b73b37daefac7027ff6b18f209583db99f0a
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "80324488"
---
# <a name="monitor-app-information-and-assignments-with-microsoft-intune"></a>使用 Microsoft Intune 监视应用信息和分配

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune 提供了多种方式来监视你管理的应用的属性以及管理应用分配状态。

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“应用”   > “所有应用”  。
3. 在应用列表中，选择要监视的应用。 随后将看到“应用”窗格，其中概述了设备状态和用户状态。

> [!NOTE]
> 部署为“可用的”的 Android 应用商店应用不会报告其安装状态  。
>
> 对于部署到 Android Enterprise 工作配置文件设备的托管 Google Play 应用，可以使用 Intune 查看设备上安装的应用的状态和版本号。 

## <a name="app-overview-pane"></a>应用概述窗格

在“应用”窗格中，可以查看有关环境中应用状态的详细信息。

### <a name="essentials"></a>Essentials
“软件包”部分包含有关该应用的以下信息  ：

 | **应用详细信息**            | **描述**                                                      |
|------------------------|------------------------------------------------------------------|
| **发布者**          | 应用发布者。                                            |
| **操作系统**   | 应用程序操作系统（Windows、iOS/iPadOS、Android 等）。 |
| **创建时间**             | 创建此修订版本的日期和时间。 <b>**注意**：此日期值在 IT 管理员更改应用元数据（例如，更改应用类别或应用说明）时更新。                        |
| **已分配**           | 是否已分配应用（  “是”或“否”  ）。                  |

### <a name="device-and-user-status-graphs"></a>设备和用户状态关系图
这些图形显示了以下状态的应用数量：

| **设备状态**       | **描述**                                       |
|-----------------------|-------------------------------------------------------|
| **已安装**         | 已安装的应用数。                         |
| **未安装**     | 未安装的应用数。                     |
| **已失败**            | 失败的安装次数。                   |
| **安装挂起**   | 正在安装的应用的数量。 |
| **不适用**           | 状态不适用的应用的数量。            |

> [!NOTE]
> 此外，请注意，部署为“注册与否都可用”的 Android LOB 应用 (.APK) 仅报告已注册设备的应用安装状态  。 无法获取未在 Intune 中注册的设备的应用安装状态。

### <a name="device-install-status"></a>设备安装状态

在菜单的“监视器”  部分中选择  “设备安装状态”时，会显示设备状态列表。 详细信息表包括以下列：

| **设备列**      | **描述**                                                                                                                                                                                                                                            |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **设备名**      | 允许命名设备的平台上的设备名称。 在其他平台上，Intune 从其他属性创建名称。 此属性不适用于任何其他设备。                                                                       |
| **用户名**        | 用户的名称。                                                                                                                                                                                                                                      |
| **平台**         | 设备的操作系统（Windows、iOS/iPadOS、Android 等）。                                                                                                                                                                                           |
| **版本**          | 应用的版本号。 对于业务线 (LOB) 应用和适用于企业的 Microsoft Store，显示应用的完整版本号。 完整版本号标识应用的特定版本。 该号码显示为“版本号(内部版本号)”   。 例如，2.2(2.2.17560800)。 对于标准应用商店应用，不显示任何版本。 |
| **状态**           | 应用的状态。                                                                                                                                                                                                                                     |
| **状态详细信息**   | 状态详细信息。                                                                                                                                                                                                                                     |
| **上次签入**    | 设备上次与 Intune 同步的日期。                                                                                                                                                                                                                  |


### <a name="user-install-status"></a>用户安装状态

在菜单的“监视器”  部分中选择  “用户安装状态”时，会显示用户状态列表。 详细信息表包括以下列：

| **用户列**     | **描述**                           |
|---------------------|-------------------------------------------|
| **Name**            | Azure Active Directory 中的用户名称。         |
| **用户名**       | 用户的唯一名称。              |
| **安装**   | 用户已安装的应用数。 |
| **失败**        | 用户安装应用失败的次数。     |
| **未安装**   | 用户未安装的应用数。 |


## <a name="next-steps"></a>后续步骤

- 要了解有关使用 Intune 数据的详细信息，请参阅[使用 Intune 数据仓库](../developer/reports-nav-create-intune-reports.md)。
- 若要了解应用配置策略，请参阅 [Intune 的应用配置策略](app-configuration-policies-overview.md)。
