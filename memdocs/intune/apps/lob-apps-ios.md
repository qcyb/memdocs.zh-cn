---
title: 将 iOS 业务线应用添加到 Microsoft Intune
titleSuffix: ''
description: 了解如何将 iOS 业务线 (LOB) 应用添加到 Microsoft Intune。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 099101e8-4b22-40ac-ba19-82ba5c71944c
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4e1850249acab42c3284b3e77c96a764bfad9898
ms.sourcegitcommit: dc2cca9eb70aef15037e8f7d18d671c513bfde85
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/14/2020
ms.locfileid: "90081784"
---
# <a name="add-an-ios-line-of-business-app-to-microsoft-intune"></a>将 iOS 业务线应用添加到 Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

本文中提供的信息可帮助你将 iOS 业务线 (LOB) 应用添加到 Microsoft Intune。 业务线 (LOB) 应用是从 IPA 应用安装文件添加到 Intune 的应用。 此类应用通常在内部编写。 首先需要加入 iOS 开发人员企业计划。 有关如何执行此操作的详细信息，请参阅 [Apple 网站](https://developer.apple.com/programs/ios/enterprise/)。

> [!NOTE]
> iOS 设备用户可删除部分内置 iOS 应用（如“股市”和“地图”）。 无法使用 Intune 重新部署这些应用。 如果用户删除这些应用，则必须前往 App Store，并手动重新安装它们。
>
> 每个 iOS LOB 应用的大小上限为 2 GB。
>
> Apple 共享的 iPad 不支持 LOB 应用。

> [!NOTE]
> 捆绑包标识符（例如 com.contoso.app）应为应用的唯一标识符。 例如，若要在生产版本旁边安装用于测试的 LOB 应用的 beta 版本，则 beta 版本必须具有不同的唯一标识符（例如 com.contoso.app-beta）。 否则，beta 版本将与生产重叠，并被视为升级。 重命名 .ipa 文件不会对此行为产生任何影响。

## <a name="select-the-app-type"></a>选择应用类型

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“应用” > “所有应用” > “添加”。
3. 在“选择应用类型”窗格中的“其他”应用类型下，选择“业务线应用”。
4. 单击“选择”。 将显示“添加应用”步骤。

## <a name="step-1---app-information"></a>步骤 1 - 应用信息

### <a name="select-the-app-package-file"></a>选择应用包文件

1. 在“添加应用”窗格中，单击“选择应用包文件”。 
2. 在“应用包文件”窗格中，选择“浏览”按钮。 然后选择扩展名为 .ipa 的 iOS 安装文件。
   将显示应用详细信息。
3. 完成后，在“应用包文件”窗格中选择“确定”以添加应用。

### <a name="set-app-information"></a>设置应用信息

1. 在“应用信息”页中，添加应用的详细信息。 此窗格中的某些值可能已自动填充，具体取决于所选应用。
    - **名称**：输入显示在公司门户中的应用的名称。 请确保使用的所有应用名称都是唯一的。 如果同一应用名称存在两次，则公司门户中仅显示其中一个应用。
    - **描述**：输入应用的说明。 描述显示在公司门户中。
    - **发布者**：输入应用发布者的名称。
    - **** 最低操作系统：从列表中选择可安装应用的最低操作系统版本。 如果将应用分配到具有较低操作系统的设备，则不会安装该应用。
    - **类别**：选择一个或多个内置应用类别，或选择你创建的类别。 “类别”可让用户在浏览公司门户时更轻松地查找应用。
    - **在公司门户中将此应用显示为特色应用**：当用户浏览应用时，在公司门户的主页上突出显示应用。
    - **信息 URL**：（可选）输入包含此应用相关信息的网站的 URL。 此 URL 显示在公司门户中。
    - **隐私 URL**：（可选）输入包含此应用相关隐私信息的网站的 URL。 此 URL 显示在公司门户中。
    - **开发者**：（可选）输入应用开发者的名称。
    - **所有者**：（可选）输入此应用的所有者的名称。 例如，“HR 部门”。
    - **备注**：输入想与此应用关联的任何备注。
    - **徽标**：上传与应用关联的图标。 用户浏览公司门户时，此图标将与应用一同显示。
2. 单击“下一步”  以显示“作用域标记”  页面。

## <a name="step-2---select-scope-tags-optional"></a>步骤 2 - 选择作用域标记（可选）
可以使用作用域标记来确定谁可以在 Intune 中查看客户端应用信息。 若要详细了解作用域标记，请参阅[将基于角色的访问控制和作用域标记用于分布式 IT](../fundamentals/scope-tags.md)。

1. 单击“选择作用域标记”  可以选择为应用添加作用域标记。 
2. 单击“下一步”以显示“分配”页面 。

## <a name="step-3---assignments"></a>步骤 3 - 分配

1. 为应用选择“必需”、“适用于已注册的设备”、“不论是否注册均可使用”或“卸载”组分配   。 有关详细信息，请参阅[添加用于组织用户和设备的组](../fundamentals/groups-add.md)和[使用 Microsoft Intune 将应用分配到组](apps-deploy.md)。
2. 单击“下一步”  以显示“查看 + 创建”页  。

## <a name="step-4---review--create"></a>步骤 4 - 查看 + 创建

1. 查看为应用输入的值和设置。
2. 完成后，单击“创建”  将应用添加到 Intune。

    将显示业务线应用的“概述”边栏选项卡。

你创建的应用现在显示在应用列表中。 从列表中，可以将应用分配到所选组。 如需帮助，请参阅[如何将应用分配到组](apps-deploy.md)。

> [!NOTE]
> iOS LOB 应用的预配配置文件在过期前 30 天将发送通知。

## <a name="step-5-update-a-line-of-business-app"></a>步骤 5：更新业务线应用

[!INCLUDE [shared-proc-lob-updateapp](../includes/shared-proc-lob-updateapp.md)]

将自动安装业务线应用的更新。

> [!NOTE]
> 为了使 Intune 服务能够成功地将新的 IPA 文件部署到设备上，必须在 IPA 包的 Info.plist 文件中递增 `CFBundleVersion` 字符串。

## <a name="next-steps"></a>后续步骤

- 你创建的应用显示在应用列表中。 现在，可将其分配到所选组。 如需帮助，请参阅[如何将应用分配到组](apps-deploy.md)。

- 详细了解可用于监视应用的属性和分配的方法。 请参阅[如何监视应用信息和分配](apps-monitor.md)。

- 详细了解 Intune 中应用的上下文。 请参阅[设备和应用生命周期概述](../fundamentals/device-lifecycle.md)。
