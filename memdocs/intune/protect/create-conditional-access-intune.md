---
title: 设置基于设备的 Intune 条件访问
titleSuffix: Microsoft Intune
description: 了解如何根据 Microsoft Intune 设备符合性和移动应用管理创建基于设备的条件访问策略。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/18/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2af62dd8480c1e804e1ab8558d270b95fe97bbd4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "82079784"
---
# <a name="create-a-device-based-conditional-access-policy"></a>创建基于设备的条件访问策略

使用 Intune，可以通过向访问控制添加移动设备符合性来增强 Azure Active Directory 中的条件访问。 通过 Intune 合规性策略（该策略定义设备的符合性要求），可以使用设备的符合性状态来允许或阻止对应用和服务的访问。 可以通过创建使用“要求设备标记为兼容”  设置的条件访问策略来实现这一点。

条件访问策略指定要保护的应用或服务、可以访问应用或服务的条件，以及向其应用策略的用户。 尽管条件访问是一项 Azure AD 高级功能，但从 Intune 访问的“条件访问”节点与从 Azure AD 访问的节点相同   。

> [!IMPORTANT]
> 在设置条件访问之前，需要设置 Intune 设备符合性策略，以便根据设备是否满足特定需求对其进行评估。 请参阅 [Intune 中的设备符合性策略入门](device-compliance-get-started.md)。

## <a name="create-conditional-access-policy"></a>创建条件访问策略

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“设备” > “条件访问” > “策略” > “新建策略”     。
  ![创建新的条件访问策略](./media/create-conditional-access-intune/create-ca.png)

3. 在“分配”  下，选择“用户和组”  。

4. 在“包含”  选项卡上，确定向其应用此条件访问策略的用户或组。 选择要包含的组或用户后，如果希望从此策略中排除任何用户、角色或组，可以使用“排除”  选项卡。

   - **所有用户**：选择此选项可将策略应用到所有用户和组，其中包括内部用户和来宾用户。

   - **选择用户和组**：选择此选项并指定一个或多个以下选项：
  
     1. **所有来宾用户**：选择此选项以包含或排除外部来宾用户（例如合作伙伴、外部协作者）

     2. **目录角色**：选择一个或多个 Azure AD 角色以包含或排除分配了这些角色的用户。

     3. **用户和组**：选择此选项以搜索并选择希望包含或排除的单个用户或组。

        > [!TIP]
        > 针对较小的用户组测试策略，以确保它按预期工作。

5. 选择“完成”  。

6. 在“分配”  下，选择“云应用或操作”  。

7. 在“包含”选项卡  上，使用可用选项来标识希望使用此条件访问策略保护的应用和服务。 如果希望从该策略中排除任何应用或服务，则可以使用“排除”  选项卡。

   - **所有云应用**：选择此选项可将策略应用到所有应用。
     > [!IMPORTANT]
     > 访问 Azure 门户的 Microsoft Azure 管理应用包含在此列表中。 无论是在此处还是在“用户和组”  选项中，请务必使用“排除”  选项卡，确保你（或指定的用户或组）能够登录到 Azure 门户。 

   - **选择应用**：选择此选项，选择“选择”  ，然后使用应用程序列表搜索并选择要保护的应用或服务。

   准备就绪后，选择“完成”  。

8. 在“分配”  下，选择“条件”  。

   - **登录风险**：选择“是”会将 Azure AD 标识保护登录风险检测与此策略结合使用，然后选择策略适用的登录风险级别  。

   - **设备平台**：在“包含”  选项卡上，确定你希望向其应用此条件访问策略的设备平台。 使用“排除”  选项卡从此策略中排除平台。

   - **位置**：在“包含”  选项卡上，指定策略是否应用于：
     - 任何位置
     - 受 IT 部门控制的受信任网络位置
     - 特定网络位置。

     使用“排除”  选项卡从此策略中排除网络位置。

   - **客户端应用**：选择“是”  来指定策略是否应该应用于浏览器应用、移动应用和桌面客户端。

   - **设备状态**：条件访问策略将应用于所有设备状态，除非选择“是”，并专门排除“已加入设备混合 Azure AD”或“标记为兼容的设备”状态（或两者兼而有之）。

     > [!TIP]
     > 如果希望同时保护“新式身份验证”  客户端和“Exchange ActiveSync”客户端  ，请创建两个单独的条件访问策略，分别针对每种客户端类型。 虽然 Exchange ActiveSync 支持新式身份验证，但 Exchange ActiveSync 支持的惟一条件是平台。 不支持其他条件，包括多重身份验证。 为有效防止 Exchange ActiveSync 对 Exchange Online 的访问，请创建指定云应用 Office 365 Exchange Online 和客户端应用 Exchange ActiveSync 的条件访问策略，同时仅将策略应用于所选的支持平台。

9. 选择“完成”  。

10. 在“访问控制”  下，选择“授予”  。 根据设置的条件配置发生的情况。  可以从以下选项中选择：

    - **阻止访问**：根据你指定的条件，拒绝此策略中指定的用户访问应用。
    - **授予访问权限**：在此策略中指定的用户将被授予访问权限，但你可以要求进一步执行任何以下操作：
      - **需要多重身份验证**：用户将需要完成其他安全要求，如电话呼叫或发送短信。
      - **需要标记为兼容的设备**：设备必须与 Intune 兼容。 如果设备不兼容，将为用户提供在 Intune 中注册设备的选项。
      - **需要加入混合 Azure AD 的设备**：设备必须已加入混合 Azure AD。
      - **需要批准的客户端应用**：设备必须使用经批准的客户端应用。 
      - **对于多个控件**：选择“需要所有已选的控件”  ，以便在设备试图访问应用时强制执行所有要求。

      ![访问控制授权设置](./media/create-conditional-access-intune/create-ca-grant-access-settings.png)

11. 在“启用策略”  下，选择“开启”  。

12. 选择“创建”。 

## <a name="next-steps"></a>后续步骤

[基于应用的 Intune 条件访问](app-based-conditional-access-intune.md)

[对 Intune 条件访问进行故障排除](https://support.microsoft.com/help/4456106)
