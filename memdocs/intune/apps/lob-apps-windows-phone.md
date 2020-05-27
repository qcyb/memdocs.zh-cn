---
title: 将 Windows Phone 业务线应用添加到 Microsoft Intune
titleSuffix: ''
description: 了解如何使用 Microsoft Intune 添加 Windows Phone 业务线 (LOB) 应用。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/23/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a097b7b2-d01d-454b-954c-da4f3cd0ae86
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7b5c12d9e0a3e2eb7ba0f996063c3d3be3d4b6f9
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990632"
---
# <a name="add-a-windows-phone-line-of-business-app-to-microsoft-intune"></a>将 Windows Phone 业务线应用添加到 Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

使用本文中提供的信息将 Windows Phone 业务线 (LOB) 应用添加到 Microsoft Intune。 LOB 应用是从应用安装文件添加到 Intune 的应用。 此类应用通常在内部编写。 Intune 在用户设备上安装 LOB 应用。 

## <a name="select-the-app-type"></a>选择应用类型

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“应用”   > “所有应用”   > “添加”  。
3. 在“选择应用类型”  窗格中的“其他”  应用类型下，选择“业务线应用”  。
4. 单击“选择”  。 将显示“添加应用”  步骤。

## <a name="step-1---app-information"></a>步骤 1 - 应用信息

### <a name="select-the-app-package-file"></a>选择应用包文件

1. 在“添加应用”  窗格中，单击“选择应用包文件”  。 
2. 在“应用包文件”  窗格中，选择“浏览”按钮。 然后选择扩展名为 .xap  的 Windows Phone 安装文件。
   将显示应用详细信息。
3. 完成后，在“应用包文件”  窗格中选择“确定”  以添加应用。

### <a name="set-app-information"></a>设置应用信息

1. 在“应用信息”  页中，添加应用的详细信息。 此窗格中的某些值可能已自动填充，具体取决于所选应用。
    - **名称**：输入显示在公司门户中的应用的名称。 请确保使用的所有应用名称都是唯一的。 如果同一应用名称存在两次，则公司门户中仅显示其中一个应用。
    - **描述**：输入应用的说明。 描述显示在公司门户中。
    - **发布者**：输入应用发布者的名称。
    - **最低操作系统**：从列表中选择可安装应用的最低操作系统版本。 如果将应用分配到具有较低操作系统的设备，则不会安装该应用。
    - **类别**：选择一个或多个内置应用类别，或选择你创建的类别。 “类别”可让用户在浏览公司门户时更轻松地查找应用。
    - **在公司门户中将此应用显示为特色应用**：当用户浏览应用时，在公司门户的主页上突出显示应用。
    - **信息 URL**：（可选）输入包含此应用相关信息的网站的 URL。 此 URL 显示在公司门户中。
    - **隐私 URL**：（可选）输入包含此应用相关隐私信息的网站的 URL。 此 URL 显示在公司门户中。
    - **开发者**：（可选）输入应用开发者的名称。
    - **所有者**：（可选）输入此应用的所有者的名称。 例如，“HR 部门”  。
    - **备注**：输入想与此应用关联的任何备注。
    - **徽标**：上传与应用关联的图标。 用户浏览公司门户时，此图标将与应用一同显示。
2. 单击“下一步”  以显示“作用域标记”  页面。

## <a name="step-2---select-scope-tags-optional"></a>步骤 2 - 选择作用域标记（可选）
可以使用作用域标记来确定谁可以在 Intune 中查看客户端应用信息。 若要详细了解作用域标记，请参阅[将基于角色的访问控制和作用域标记用于分布式 IT](../fundamentals/scope-tags.md)。

1. 单击“选择作用域标记”  可以选择为应用添加作用域标记。 
2. 单击“下一步”以显示“分配”页面   。

## <a name="step-3---assignments"></a>步骤 3 - 分配

1. 为应用选择“必需”  、“适用于已注册的设备”  或“卸载”  组分配。 有关详细信息，请参阅[添加用于组织用户和设备的组](../fundamentals/groups-add.md)和[使用 Microsoft Intune 将应用分配到组](apps-deploy.md)。
2. 单击“下一步”  以显示“查看 + 创建”页  。

## <a name="step-4---review--create"></a>步骤 4 - 查看 + 创建

1. 查看为应用输入的值和设置。
2. 完成后，单击“创建”  将应用添加到 Intune。

    将显示业务线应用的“概述”  边栏选项卡。

你创建的应用现在显示在应用列表中。 从列表中，可以将应用分配到所选组。 如需帮助，请参阅[如何将应用分配到组](apps-deploy.md)。

## <a name="next-steps"></a>后续步骤

- 你创建的应用显示在应用列表中。 现在，可将其分配到所选组。 如需帮助，请参阅[如何将应用分配到组](apps-deploy.md)。

- 详细了解可用于监视应用的属性和分配的方法。 请参阅[如何监视应用信息和分配](apps-monitor.md)。

- 详细了解 Intune 中应用的上下文。 请参阅[设备和应用生命周期概述](../fundamentals/device-lifecycle.md)。
