---
title: 在 Intune 中对分布式 IT 使用基于角色的访问控制 (RBAC) 和范围标记 | Microsoft Docs
description: 使用作用域标记将配置文件筛选到特定角色。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/06/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.technology: ''
ms.assetid: a21d3039-f2ed-4f43-b6fa-d00c071edbc4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d0ffd06d86106b07224edc40aefc7407673a0391
ms.sourcegitcommit: bbb63f69ff8a755a2f2d86f2ea0c5984ffda4970
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79526251"
---
# <a name="use-role-based-access-control-rbac-and-scope-tags-for-distributed-it"></a>对分布式 IT 使用基于角色的访问控制 (RBAC) 和范围标记

可使用基于角色的访问控制和范围标记来确保适当的管理员对适当的 Intune 对象具有适当的访问权限并可适当查看这些对象。 角色确定了管理员对哪些对象具有哪种访问权限。 而范围标记确定了管理员可查看哪些对象。

例如，假设向西雅图区域办事处的一名管理员分配了“策略和配置文件管理员”角色。 而你希望该管理员仅查看和管理只适用于西雅图区域设备的配置文件和策略。 若要设置此访问权限，请执行以下操作：

1. 创建一个名为“西雅图”的范围标记。
2. 通过下列项为“策略和配置文件管理员”角色创建角色分配： 
    - 成员（组）：一个名为“西雅图 IT 管理员”的安全组。 该组中的所有管理员都将有权管理范围（组）中用户/设备的策略和配置文件。
    - 范围（组）：一个名为“西雅图用户”的安全组。 该组中的所有用户/设备都可让成员（组）中的管理员管理其配置文件和策略。 
    - 范围（标记）：西雅图。 成员（组）中的管理员可查看还具有“西雅图”范围标记的 Intune 对象。
3. 将“西雅图”范围标记添加到希望成员（组）中的管理员可访问的策略和配置文件中。
4. 将“西雅图”范围标记添加到希望在成员（组）中向管理员显示的设备。 

## <a name="default-scope-tag"></a>默认作用域标记
默认作用域标记将自动添加到支持作用域标记的所有未标记对象。

默认作用域标记功能类似于 Microsoft Endpoint Configuration Manager 中的安全作用域功能。 

## <a name="to-create-a-scope-tag"></a>创建作用域标记

1. 在 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“租户管理” > “角色” > “作用域(标记)” > “创建”     。
2. 在“基本信息”页上，提供“名称”和可选“说明”    。 选择“下一步”  。
3. 在“分配”页面上，选择包含要分配此作用域标记的设备的组  。 选择“下一步”  。
4. 在“查看 + 创建”页上，选择“创建”   。

## <a name="to-assign-a-scope-tag-to-a-role"></a>向角色分配作用域标记

1. 在 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“租户管理” > “角色” > “所有角色”> 选择角色 >“分配” > “分配”      。
2. 在“基本信息”页上，提供分配名称和说明    。 选择“下一步”  。
3. 在“管理组”页面上，选择“选择要包含的组”，然后选择要作为此分配一部分的组   。 此组中的用户将具有管理作用域（组）中的用户/设备的权限。 选择“下一步”  。

    ![选择成员组的屏幕截图。](./media/scope-tags/select-member-groups.png)

4. 在“作用域组”页面上，为“分配给”选择下列选项之一  
    - **所选组**：选择包含要管理的用户/设备的组。 所选组中的所有用户/设备将由管理组中的用户管理。
    - **所有用户**：所有用户都可以由管理组中的用户管理。
    - **所有设备**：所有设备都可以由管理组中的用户管理。
    - **所有用户和所有设备**：所有用户和设备都可以由管理组中的用户管理。

5. 选择“下一步” 
6. 在“作用域标记”页面上，选择要添加到此角色的标记  。 管理组中的用户将可以访问也具有相同作用域标记的 Intune 对象。 最多可以为角色分配 100 个范围标记。
7. 选择“下一步”转到“查看 + 创建”页面，然后选择“创建”    。

## <a name="assign-scope-tags-to-other-objects"></a>将作用域标记分配给其他对象

对于支持作用域标记的对象，作用域标记通常出现在“属性”下  。 例如，若要将作用域标记分配给配置配置文件，请执行以下步骤：

1. 在 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“设备” > “配置文件”>“选择配置文件”   。

2. 选择“属性” > “范围(标记)” > “编辑” > “选择作用域标记”> 选择要添加到配置文件的标记     。 最多可以为对象分配 100 个范围标记。
4. 选择“选择” > “查看 + 保存”   。

## <a name="scope-tag-details"></a>范围标记详细信息
使用范围标记时，请谨记下列详细信息： 

- 如果租户可以有该对象的多个版本（如角色分配或应用），则可以将作用域标记分配给 Intune 对象类型。
  以下 Intune 对象是此规则的例外，当前不支持作用域标记：
    - Windows ESP 配置文件
    - 设备类别
    - 注册限制
    - 公司设备标识符
    - Autopilot 设备
    - 设备符合性位置
    - Jamf 设备
- 与 VPP 令牌关联的 VPP 应用和电子书继承分配给关联 VPP 令牌的作用域标记。
- 与 DEP 令牌关联的设备注册程序 (DEP) 设备和 DEP 配置文件继承分配给关联 DEP 令牌的作用域标记。
- 管理员在 Intune 中创建对象时，分配给该管理员的所有范围标记都将自动分配给新对象。
- Intune RBAC 不适用于 Azure Active Directory 角色。 因此，无论 Intune 服务管理员和全局管理员角色具有哪些范围标记，它们都对 Intune 具有完整的管理员访问权限。
- 如果角色分配没有作用域标记，则 IT 管理员可以查看基于 IT 管理员权限的所有对象。 没有作用域标记的管理员实际上拥有所有作用域标记。
- 只能在角色分配中分配所拥有的范围标记。
- 仅可面向在角色分配的范围（组）中列出的组。
- 如果向角色分配了范围标记，则无法删除 Intune 对象上的所有范围标记。 必须至少有一个范围标记。

## <a name="next-steps"></a>后续步骤

了解当存在[多个角色分配](role-based-access-control.md#multiple-role-assignments)时作用域标记的行为。
管理[角色](role-based-access-control.md)和[配置文件](../configuration/device-profile-assign.md)。


