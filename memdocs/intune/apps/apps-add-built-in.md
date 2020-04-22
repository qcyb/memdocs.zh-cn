---
title: 使用 Microsoft Intune 将内置应用添加到移动设备
titleSuffix: ''
description: 了解如何使用 Intune 更轻松地在移动设备上安装内置应用。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/22/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 0ec8de66-5a0f-4c8d-afbf-c2becc7d6eec
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 74db26a3d5f80a0192e996913177745c0b438ac6
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "80324935"
---
# <a name="add-built-in-apps-to-microsoft-intune"></a>将内置应用添加到 Microsoft Intune

通过使用内置的  应用类型，可以轻松地将特选的托管应用（例如 Office 365 应用）分配给 iOS/iPadOS 和 Android 设备。 可以为此应用类型分配特定的应用，例如 Excel、OneDrive、Outlook、Skype 等。 添加应用后，应用类型将显示为“内置 iOS 应用”  或“内置 Android 应用”  。 通过使用内置应用类型，可以选择将其中哪些应用发布给设备用户。

在早期版本的 Intune 控制台中，Intune 提供了几个默认的托管 Office 365 应用，如 Outlook 和 OneDrive。 这些托管应用的应用类型被标记为“托管 iOS 应用商店应用”  或“托管 Android 应用”  。 我们建议使用内置应用类型，而不是使用这些应用类型。 通过使用内置应用类型，用户在编辑和删除 Office 365 应用方面将具有更多灵活性。

>[!NOTE]
>删除所有分配时，也会从应用列表中删除被标记为“托管 iOS 应用商店”  和“托管 Android 应用”  的默认 Office 365 应用。

## <a name="add-a-built-in-app"></a>添加内置应用

若要将内置应用添加到 Microsoft Intune 中的可用应用中，请执行以下步骤：
1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“应用”   > “所有应用”   > “添加”  。
3. 在“选择应用类型”  窗格中的可用“应用商店应用”  类型下，选择“内置应用”  。
4. 单击“选择”  。 将显示“添加应用”  步骤。
5. 在“选择内置应用”  页面中，单击“选择应用”  以选择要包括的应用。
6. 选择想要包括的内置应用。 
7. 选择应用后，在“选择内置应用”  窗格中单击“选择”  。
8. 单击“下一步”  以显示“作用域标记”  页面。
9. 单击“选择作用域标记”  可以选择为应用添加作用域标记。 有关详细信息，请参阅[对分布式 IT 使用基于角色的访问控制 (RBAC) 和作用域标记](../fundamentals/scope-tags.md)。
10. 单击“下一步”以显示“分配”页面   。
11. 为应用选择组分配。 有关详细信息，请参阅[添加用于组织用户和设备的组](../fundamentals/groups-add.md)。 
12. 单击“下一步”  以显示“查看 + 创建”页  。 查看为应用输入的值和设置。
13. 完成后，单击“创建”  将应用添加到 Intune。

    随即显示创建的应用的“概述”  边栏选项卡。

## <a name="configure-app-information"></a>配置应用信息

可以修改有关内置应用的信息。 此信息有助于在 Intune 中识别应用，也有助于用户在公司门户中找到该应用。
1. 选择“应用” > “所有应用”，然后选择想要修改的内置应用   。  
   随即显示该内置应用的窗格。
2. 选择“属性”  。
3. 选择“应用信息”  旁边的“编辑”  。
4. 在“应用信息”  窗格中可以修改以下信息：
    - **名称**：输入内置应用的名称，该名称将在公司门户中显示。 请确保使用的所有名称都是唯一的。 如果同一应用名称存在两次，则在公司门户中将仅向用户显示其中一个应用。
    - **描述**：输入应用的描述。 
    - **发布者**：输入应用发布者的名称。
    - **类别**：（可选）选择一个或多个内置应用类别。 设置此选项可让用户在浏览公司门户时更轻松地查找应用。
    - **在公司门户中将此应用显示为特色应用**：当用户浏览应用时，在公司门户的主页上突出显示应用。
    - **信息 URL**：（可选）输入包含此应用相关信息的网站的 URL。 在公司门户中向用户显示该 URL。
    - **隐私 URL**：（可选）输入包含此应用相关隐私信息的网站的 URL。 在公司门户中向用户显示该 URL。
    - **开发者**：（可选）输入应用开发者的名称。
    - **所有者**：（可选）输入此应用的所有者的名称（例如，HR 部门  ）。
    - **备注**：输入想与此应用关联的任何备注。
    - **上传图标**：上传用户浏览公司门户时与应用一同显示的图标。
5. 单击“查看并保存”  以显示“查看 + 创建”页  。 查看为应用输入的值和设置。
13. 完成后，单击“保存”以更新 Intune 中的应用  。

    随即显示创建的应用的“概述”  边栏选项卡。

## <a name="next-steps"></a>后续步骤

- 现在，可将应用分配到所选组。 有关详细信息，请参阅[将应用分配到组](apps-deploy.md)。
