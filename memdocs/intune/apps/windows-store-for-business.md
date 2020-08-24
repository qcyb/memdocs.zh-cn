---
title: 管理来自适用于企业的 Microsoft Store 的 VPP 应用
titleSuffix: Microsoft Intune
description: 了解如何将应用从适用于企业的 Microsoft Store 同步到 Intune。
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
ms.assetid: 2ed5d3f0-2749-45cd-b6bf-fd8c7c08bc1b
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, seoapril2019
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5be1c4fd42d27386b4fdc51cac6167625432491f
ms.sourcegitcommit: 91519f811b58a3e9fd116a4c28e39341ad8af11a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88559559"
---
# <a name="how-to-manage-volume-purchased-apps-from-the-microsoft-store-for-business-with-microsoft-intune"></a>如何使用 Microsoft Intune 管理从适用于企业的 Microsoft Store 批量采购的应用

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

可在[适用于企业的 Microsoft 应用商店](https://www.microsoft.com/business-store)中为组织查找和购买应用（单个或批量）。 通过将此应用商店与 Microsoft Intune 相连，可以在 Azure 门户中管理批量购买的应用。 例如：

* 可以将从应用商店中购买（或免费）的应用列表与 Intune 同步。
* Intune 管理控制台中将显示已同步的应用，可以像分配所有其他应用那样分配这些应用。
* 应用的联机和脱机许可版本均同步到 Intune。 门户中的应用名称将附加“联机”或“脱机”。
* 你可以跟踪可用许可证的数量以及正在 Intune 管理控制台中使用的许可证数量。
* 如果可用许可证数量不足，Intune 将阻止应用的分配和安装。
* 用户离开企业或管理员删除用户和用户设备时，由适用于企业的 Microsoft Store 托管的应用会自动撤销许可证。

## <a name="before-you-start"></a>开始之前

从适用于企业的 Microsoft 应用商店同步并分配应用之前，请查看以下信息：

- 将 Intune 配置为组织的移动设备管理机构。
- 必须已在适用于企业的 Microsoft 应用商店中注册帐户。
- 将适用于企业的 Microsoft Store 帐户与 Intune 关联后，该帐户将来无法更改为其他帐户。
- 无法在 Intune 中手动添加或删除从应用商店购买的应用。 这些应用只能与适用于企业的 Microsoft 应用商店同步。
- 从适用于企业的 Microsoft Store 中购买的联机和脱机授权应用都会同步到 Intune 门户。 然后，可以将这些应用部署到设备组或用户组。
- 在线应用安装由应用商店管理。
- 免费的脱机应用也可同步到 Intune。 这些应用由 Intune 安装，而不是由应用商店安装。
- 设备必须已加入 Active Directory 域服务、Azure AD 联接或工作区才可使用此功能。
- 已注册的设备必须使用 Windows 10 的 1511 版本或更高版本。

> [!NOTE]
> 如果禁用对受管理设备上的 Store（通过策略或组策略手动进行）的访问权限，将无法安装联机许可应用。

## <a name="associate-your-microsoft-store-for-business-account-with-intune"></a>将适用于企业的 Microsoft 应用商店帐户与 Intune 关联

在 Intune 控制台中启用同步之前，必须将你的应用商店帐户配置为将 Intune 作为一种管理工具使用：

1. 请确保登录[适用于企业的 Microsoft Store](https://www.microsoft.com/business-store) 与登录 Intune 时使用的租户帐户相同。
2. 在“业务应用商店”中，依次选择“管理”  选项卡、“设置”  和“分发”  选项卡。
3. 如果没有专门将 Microsoft Intune  用作移动设备管理工具，请选择“添加管理工具”  来添加“Microsoft Intune”  。 如果尚未将 Microsoft Intune 激活为移动设备管理工具，请单击“Microsoft Intune”旁边的“激活”。 请注意，应激活“Microsoft Intune”  ，而不是“Microsoft Intune 注册”  。

> [!NOTE]
> 以前只能将一个用于分配应用的管理工具关联到适用于企业的 Microsoft 应用商店。 现在可将多种管理工具与该应用商店关联，例如 Intune 和 Configuration Manager。

现在可以继续，并在 Intune 控制台中设置同步。

## <a name="configure-synchronization"></a>配置同步

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“租户管理”   > “连接器和令牌”   > “适用于企业的 Microsoft Store”  。
3. 单击“启用”  。
4. 如果尚未这样做，请单击适用于企业的 Microsoft 应用商店的注册链接，并按之前详述的步骤关联帐户。
5. 在“语言”下拉列表中，选择适用于企业的 Microsoft Store 中的应用在 Azure 门户中的显示语言  。 无论以何种语言显示，都会以最终用户的语言（如果有）进行安装。
6. 单击“同步”  ，将从 Microsoft 应用商店购买的应用同步到 Intune。

## <a name="synchronize-apps"></a>同步应用
如果已将适用于企业的 Microsoft Store 帐户与 Intune 管理员凭据关联，则可以使用以下步骤手动将适用于企业的 Microsoft Store 应用与 Intune 同步。

1. 选择“租户管理” > “连接器和令牌” > “适用于企业的 Microsoft Store”。
2. 单击“同步”****，将从 Microsoft 应用商店购买的应用同步到 Intune。

> [!NOTE]
> 当前不支持具有加密应用包的应用，并且不会将其同步到 Intune。

## <a name="assign-apps"></a>分配应用

分配应用商店中应用的方式与分配任何其他 Intune 应用的方式相同。 有关详细信息，请参阅[如何使用 Microsoft Intune 将应用分配到组](apps-deploy.md)。

脱机应用可面向用户组、设备组或同时具有用户和设备的组。
可为设备上的特定用户或所有用户安装脱机应用。

分配适用于企业的 Microsoft 应用商店的应用时，安装此应用的每个用户都会使用一个许可证。 如果使用了分配应用的所有可用许可证，则无法再分配任何副本。 请执行以下一项操作：

* 从一些设备上卸载应用。
* 减小当前分配的范围，仅针对具有足够许可证的用户。
* 从适用于企业的 Microsoft 应用商店中购买应用的更多副本。

## <a name="remove-apps"></a>删除应用

要删除从适用于企业的 Microsoft Store 同步的应用，需要登录适用于企业的 Microsoft Store 并退还应用。 无论应用免费与否，过程都一样。 对于免费应用，应用商店不退款。 下面的示例展示了免费应用的退款。 

![删除应用详情的屏幕截图](./media/windows-store-for-business/microsoft-store-for-business-01.png)

> [!NOTE]
> 在专用应用商店中隐藏应用不会阻止 Intune 同步应用。 必须执行应用退款，才能完全删除应用。

## <a name="next-steps"></a>后续步骤

* [使用 Microsoft Intune 管理批量采购的应用和书籍](vpp-apps.md)
