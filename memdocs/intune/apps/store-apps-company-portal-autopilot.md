---
title: 为 Autopilot 预配的设备添加和分配 Windows 10 公司门户应用
titleSuffix: Microsoft Intune
description: 为 Autopilot 预配的设备添加 Windows 10 公司门户应用并将其分配给 Intune。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4d45d73f9c10c9bf7562def73b005c0dd63c7613
ms.sourcegitcommit: 91519f811b58a3e9fd116a4c28e39341ad8af11a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88559515"
---
# <a name="add-and-assign-the-windows-10-company-portal-app-for-autopilot-provisioned-devices"></a>为 Autopilot 预配的设备添加和分配 Windows 10 公司门户应用

若要管理设备和安装应用，你的用户可以使用公司门户应用。 可以直接从 Intune 分配 Windows 10 公司门户应用。 

## <a name="prerequisites"></a>必备条件

对于 Windows 10 Autopilot 预配的设备，建议将适用于企业的 Microsoft Store 帐户与 Intune 进行关联。 有关详细信息，请参阅[如何使用 Microsoft Intune 管理从适用于企业的 Microsoft Store 批量采购的应用](windows-store-for-business.md)。

可以选择使用以下步骤安装公司门户（脱机）应用。 如果将公司门户应用分配给 Autopilot 组并在用户登录之前将其安装在设备上，则将在设备上下文中安装该应用。

## <a name="configure-the-store-settings-to-show-the-offline-app"></a>配置应用商店设置以显示脱机应用

1. 使用管理员帐户登录到[适用于企业的 Microsoft Store](https://www.microsoft.com/business-store)。
2. 选择窗口顶部附近的“管理”选项卡  。
3. 在左窗格中，选择“设置”  。
4. 在“购物体验”下，将“显示脱机应用”设置为“开”    。  
   将显示脱机许可的应用。

## <a name="get-the-offline-company-portal-app-from-the-store"></a>从应用商店中获取脱机公司门户应用

1. 搜索并选择“公司门户”应用  。
2. 将“许可证类型”设置为“脱机”   。
3. 选择“获取应用”以获取脱机公司门户应用，并将其添加到清单中  。
   为了在 Intune 中列出应用，必须等待同步计划完成，或者从 Microsoft 终结点管理器管理中心执行手动同步。

## <a name="manually-sync-company-portal-app-with-intune"></a>手动将公司门户应用与 Intune 同步

1.  使用管理员帐户登录到  [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“租户管理” > “连接器和令牌” > “适用于企业的 Microsoft Store”。
3. 单击 **“启用”** 。
4. 如果尚未这样做，请单击适用于企业的 Microsoft 应用商店的注册链接，并按之前详述的步骤关联帐户。
5. 在“语言”下拉列表中，选择适用于企业的 Microsoft Store 中的应用在 Azure 门户中的显示语言****。 无论以何种语言显示，都会以最终用户的语言（如果有）进行安装。
6. 单击“同步”****，将从 Microsoft 应用商店购买的应用同步到 Intune。

## <a name="assign-the-company-portal-app"></a>分配公司门户应用

1.  使用管理员帐户登录到  [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“应用” > “Windows”。
3. 在 Windows 应用列表中，选择“公司门户(脱机)”。
4. 将公司门户应用作为所需应用[分配](apps-deploy.md)到你所选的 Autopilot 设备组。

## <a name="next-steps"></a>后续步骤

- 如需了解有关分配应用的详细信息，请参阅[将应用分配给组](apps-deploy.md)。

