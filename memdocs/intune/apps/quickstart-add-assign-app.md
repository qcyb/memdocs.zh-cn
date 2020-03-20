---
title: 快速入门 - 添加和分配客户端应用
titleSuffix: Microsoft Intune
description: 本快速入门将使用 Microsoft Intune 来添加和分配客户端应用。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/26/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: dab6f5c8-1ebb-42c4-a7a7-7af001f94e15
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c5b6762669e4d816010982c63a119bffdec2f055
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79334270"
---
# <a name="quickstart-add-and-assign-a-client-app"></a>快速入门：添加并分配客户端应用

本快速入门将使用 Intune 来添加客户端应用并将其分配给公司的员工。 管理员的首要任务之一是，确保最终用户能够访问他们在执行工作时所需的应用。

如果没有 Intune 订阅，请[注册免费试用帐户](../fundamentals/free-trial-sign-up.md)。

## <a name="prerequisites"></a>必备条件

- 要完成本快速入门，必须[创建用户](../fundamentals/quickstart-create-user.md)、[创建组](../fundamentals/quickstart-create-group.md)以及[注册设备](../enrollment/quickstart-setup-auto-enrollment.md)。

## <a name="sign-in-to-intune"></a>登录到 Intune

以[全局管理员或 Intune 服务管理员](../fundamentals/users-add.md#types-of-administrators)身份登录 [Intune](https://aka.ms/intuneportal)。 如果已创建 Intune 试用版订阅，则用于创建订阅的帐户就是全局管理员。

## <a name="add-the-client-app-to-intune"></a>将客户端应用添加到 Intune

可以包含应用，以便 Intune 可以管理应用的各个方面。 

可使用以下步骤将应用添加到 Intune：

1. 在 [Intune](https://aka.ms/intuneportal) 中，选择“应用”   > “所有应用”   > “添加”  。 
2. 在“选择应用类型”  窗格的“Office 365 套件”  部分中选择“Windows 10”  。
3. 单击“选择”  。 将显示“添加应用”  步骤。
4. 确认“应用套件信息”  页中的默认详细信息。
5. 单击“下一步”  以显示“配置应用套件”  页。
6. 在“更新通道”  旁从下拉框中选择“每月”  。
7. 确认“配置应用套件”  页中的剩余默认详细信息。
8. 单击“下一步”  以显示“作用域标记”  页面。
9. 单击“选择作用域标记”  可以选择为应用添加作用域标记。 有关详细信息，请参阅[对分布式 IT 使用基于角色的访问控制 (RBAC) 和作用域标记](../fundamentals/scope-tags.md)。
10. 单击“下一步”以显示“分配”页面   。
11. 为应用选择组分配。 有关详细信息，请参阅[添加用于组织用户和设备的组](../fundamentals/groups-add.md)。
12. 单击“下一步”  以显示“查看 + 创建”页  。 查看为应用输入的值和设置。
13. 完成后，单击“创建”  将应用添加到 Intune。

## <a name="assign-the-app-to-a-group"></a>将应用分配给组

向 Microsoft Intune 添加应用后，可将应用分配给用户组或设备组。

> [!NOTE]
> 本快速入门以本系列前面的快速入门为基础。 有关详细信息，请参阅本快速入门中的[先决条件](quickstart-add-assign-app.md#prerequisites)。

可使用以下步骤将应用分配给组：

1. 在 [Intune](https://aka.ms/intuneportal) 中，选择“应用”   > “所有应用”  。 
2. 选择要分配给组的应用。
3. 单击“分配” > “添加组”，显示“添加组”窗格    。
4. 在“分配类型”下拉框中，选择“适用于已注册设备”   。 
5. 单击“包括的组” >  选择要包括的组  > “Contoso 测试人员”    。
6. 单击“选择” > “确定” > “确定” > “保存”即可分配组     。

现已将应用分配给“Contoso 测试人员”组  。

## <a name="install-the-app-on-the-enrolled-device"></a>在已注册设备上安装应用

必须安装并使用公司门户应用才能安装 Intune 提供的“Contoso 的待办事项”应用  。 使用以下步骤验证该应用是否可供已注册设备的用户使用。

1. 登录到已注册的 Windows 10 桌面版设备。

    > [!IMPORTANT]
    > 设备必须[已向 Intune 注册](../enrollment/quickstart-enroll-windows-device.md)。 此外，必须使用分配给应用的组中包含的帐户登录设备。

2. 从“开始”菜单中，打开“Microsoft Store”   。 然后，找到“公司门户”应用并安装  。
3. 启动“公司门户”应用  。
4. 单击使用 Intune 添加的应用。 在本快速入门中，添加了“Microsoft Office 365 应用套件”应用  。

    > [!NOTE]
    > 如果未成功将任何应用分配给 Intune 用户，你将看到以下消息：IT 管理员未向你提供任何应用。 

5. 单击“安装”  。

如果业务需求需要将公司门户应用分配给员工，则可直接从 Intune 手动分配 Windows 10 公司门户应用。 有关详细信息，请参阅[使用 Microsoft Intune 手动添加 Windows 10 公司门户应用](company-portal-app.md)。

## <a name="next-steps"></a>后续步骤

在本快速入门中，已将应用添加到了 Intune、向组分配了应用，并在已注册的 Windows 10 桌面版设备上安装了应用。 有关在 Intune 中管理应用的详细信息，请参阅[什么是 Microsoft Intune 应用管理？](app-management.md)

要完成这一系列的 Intune 快速入门，请继续学习下一篇快速入门。

> [!div class="nextstepaction"]
> [快速入门：创建并分配应用保护策略](quickstart-create-assign-app-policy.md)
