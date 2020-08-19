---
title: 将 Microsoft Store 应用添加到 Microsoft Intune
titleSuffix: ''
description: 了解如何将 Microsoft Store (Windows Store) 应用添加到 Microsoft Intune。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 07241b6d-86d8-4abb-83a2-3fc5feae5788
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c816bf41933346a568ff0419ea8daccbeffebd3d
ms.sourcegitcommit: 1aeb4a11e89f68e8081d76ab013aef6b291c73c1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2020
ms.locfileid: "88217304"
---
# <a name="add-microsoft-store-apps-to-microsoft-intune"></a>将 Microsoft Store 应用添加到 Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

必须首先将应用添加到 Intune 中，才可以分配、监视、配置或保护它们。 

## <a name="add-an-app-to-intune"></a>将应用添加到 Intune
通过执行以下操作可将 Microsoft Store 应用添加到 Intune：

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“应用”   > “所有应用”   > “添加”  。
3. 在“选择应用类型”  窗格中的可用“应用商店应用”  类型下，选择“Windows 应用商店应用”  。
4. 单击“选择”  。 将显示“添加应用”  步骤。
5. 若要为 Windows 应用商店应用配置“应用信息”  ，请导航到 [Microsoft Store](https://www.microsoft.com/store/apps) 并搜索要部署的应用。 显示应用页并记下应用详细信息。 
6. 在“应用信息”  页中，添加应用详细信息：
    - **名称**：输入要在公司门户中显示的应用名称。 请确保使用唯一的应用名称。 如果应用名称重复，则在公司门户中仅向用户显示一个名称。
    - **描述**：输入应用的描述。 在公司门户中向用户显示该描述。
    - **发布者**：输入应用发布者的名称。
    - **应用商店 URL**：键入要创建的应用的应用商店 URL。 可以通过在所需应用的 [Microsoft Store](https://www.microsoft.com/store/apps) 中搜索来找到该 URL。 使用浏览器地址栏中的 URL。
    - **类别**：（可选）选择一个或多个内置应用类别或所创建的类别。 此操作可让用户在浏览公司门户时更轻松地查找应用。
    - **在公司门户中将此应用显示为特色应用**：当用户浏览应用时，选择此选项以在公司门户的主页上突出显示应用套件。
    - **信息 URL**：（可选）输入包含此应用相关信息的网站的 URL。 在公司门户中向用户显示该 URL。
    - **隐私 URL**：（可选）输入包含此应用相关隐私信息的网站的 URL。 在公司门户中向用户显示该 URL。
    - **开发者**：（可选）输入应用开发者的名称。
    - **所有者**：（可选）输入此应用的所有者的名称（例如，HR 部门  ）。
    - **备注**：（可选）输入要与此应用关联的任何备注。
    - **徽标**：（可选）：上传将与应用关联的图标。 用户浏览公司门户时，此图标将与应用一同显示。
7. 单击“下一步”  以显示“作用域标记”  页面。
8. 单击“选择作用域标记”  可以选择为应用添加作用域标记。 有关详细信息，请参阅[对分布式 IT 使用基于角色的访问控制 (RBAC) 和作用域标记](../fundamentals/scope-tags.md)。
9. 单击“下一步”以显示“分配”页面   。
10. 为应用选择组分配。 有关详细信息，请参阅[添加用于组织用户和设备的组](../fundamentals/groups-add.md)。 
11. 单击“下一步”  以显示“查看 + 创建”页  。 查看为应用输入的值和设置。
12. 完成后，单击“创建”  将应用添加到 Intune。

随即显示创建的应用的“概述”  边栏选项卡。

此时，已创建的应用显示在应用列表中，可在此列表中将其分配到选择的组。

> [!IMPORTANT]
> Microsoft Store 应用仅分配到分配类型为“适用于已注册设备”的组（用户从公司门户应用或网站安装应用）  。

## <a name="next-steps"></a>后续步骤

- [将应用分配给组](apps-deploy.md)
