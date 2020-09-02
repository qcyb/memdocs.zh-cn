---
title: 将条件访问迁移到 Azure 门户
titleSuffix: Microsoft Intune
description: 将先前在 Intune 经典门户中创建的条件访问策略重新分配给 Azure 门户。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/02/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 301159ad-5f7e-4fcc-86c7-f72a71701ff4
ms.reviewer: chrisgree
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fa5593486f51d28c33ed280c97f819426be60fa2
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88911312"
---
# <a name="reassign-conditional-access-policies-from-intune-classic-portal-to-the-azure-portal"></a>将条件访问策略从 Intune 经典门户重新分配到 Azure 门户

从新 Azure 门户开始，条件访问按应用提供多策略支持和更高的可自定义度。 如果先前在 Intune 经典门户中创建了条件访问策略，则可将其迁移到 Azure 门户。 

## <a name="before-you-begin"></a>在开始之前

如果准备迁移到 Azure 门户，请按照本主题中的步骤重新分配先前在 Intune 经典门户中创建的条件访问策略：

- 收集以前创建的条件访问策略，以便了解之后需要重新分配哪些设置。

- 按照本主题中的步骤，在 Azure 门户中重新创建这些策略。

- 验证新策略可以按预期在 Azure 门户中运行后，在 Intune 经典门户中禁用条件策略。
<br /><br />
  - 在 Intune 典门户中“禁用”  条件访问策略之前，需先规划如何将用户转移到新策略。 有两种方法：
<br /><br />
    - 使用相同的包含组来应用在 Azure 门户中创建的策略，并创建一个新免除组，以与 Intune 经典门户应用的策略配合使用  。
      - 逐渐将某些用户移动到经典门户中指定的免除组中。 这样可以阻止应用 Intune 经典门户所面向的策略。 除 Intune 经典门户中应用的策略外，还会应用在 Azure 门户中创建的、针对同一用户组的策略。 
<br /><br />
    - **在 Azure 门户中创建一个要实施条件访问策略的新组**。 如果选择此方法，需要执行以下操作：
      - 逐渐从在 Intune 经典门户中应用条件访问策略的安全组中删除用户。
      - 确认新策略适用于这些用户后，可在 Intune 经典门户中禁用该策略。 
<br /><br />
- 如果条件访问策略设置配置为在 Intune 经典门户中使用 Exchange ActiveSync (EAS)，请参阅[本主题中的说明](#reassign-intune-device-based-conditional-access-policies-for-eas-clients)，了解如何在 Azure 门户中重新分配 EAS 条件访问策略设置  。

### <a name="to-verify-your-device-based-conditional-access-policies-in-the-intune-classic-portal"></a>验证 Intune 经典门户中基于设备的条件访问策略

1. 转到 [Intune 经典门户](https://manage.microsoft.com)，并用自己的凭据登录。

2. 在左侧菜单中选择“策略”  。

3. 选择“条件访问”，然后选择为其创建条件访问策略的 Microsoft 云服务（例如 Exchange Online 或 SharePoint Online）  。

4. 记下条件访问设置，并参考这些设置在 Azure 门户中创建相同的条件访问策略。

### <a name="app-and-device-based-conditional-access-policies-working-together"></a>配合使用基于应用和基于设备的条件访问策略

通过使用 Azure 门户中的“Intune 应用保护”边栏选项卡，管理员可以设置基于应用的条件规则，以便仅允许支持 Intune 应用保护策略的应用访问公司资源  。 可使用基于设备的条件访问策略覆盖这些基于应用的条件访问策略。 可以合并基于设备的和基于应用的条件策略（逻辑 AND），还可以提供其中一个选项（逻辑 OR）。 如果条件访问策略的要求是：

- 需要兼容设备和 (AND) 使用已批准的应用  。
  - 应使用[“Azure Active Directory 条件访问”边栏选项卡](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies)和[“Intune 应用保护”边栏选项卡](https://portal.azure.com/#blade/Microsoft_Intune/SummaryBlade/0)来设置条件访问策略。
<br /><br />
- 需要兼容设备或 (OR) 使用已批准的应用  。
  - 应使用 [Intune 经典门户](https://manage.microsoft.com)和[“Intune 应用保护”边栏选项卡](https://portal.azure.com/#blade/Microsoft_Intune/SummaryBlade/0)来设置条件访问策略。

> [!TIP] 
> 本主题提供一些屏幕截图，用于比较 Intune 经典门户和 Azure 门户的用户体验。

## <a name="reassign-intune-device-based-conditional-access-policies"></a>重新分配基于设备的 Intune 条件访问策略

1. 转到 [Azure 门户中的条件访问](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies)，并用自己的凭据登录。

2. 选择“新策略”  。

3. 提供策略的名称。

4. 在“分配”部分下，选择“用户和组”以应用新条件访问策略   。

    ![Intune 和 Azure 门户之间的用户组用户界面比较图](./media/conditional-access-intune-reassign/reassign-ca-1.png)

    > [!IMPORTANT] 
    > 对 Azure 门户做出的选择应与之前对经典门户做出的选择相对应。 例如，如果在 Intune 经典门户中选择了所有用户，则应在 Azure 门户中选择“所有用户”  。 另外，如果在 Intune 经典门户中选择了“免除组”选项，则还需要在 Azure 门户中排除所选的这些组  。

5. 选择组后，单击“选择”，然后单击“完成”   。

6. 在“分配”部分下，选择“云应用”   。

7. 在“云应用”  边栏选项卡上，选择“选择应用”  。

8. 选择要应用新条件访问策略的应用，然后单击“选择”  。

9. 单击“Done”（完成）  。

    ![Intune 和 Azure 门户之间的云应用用户界面比较图](./media/conditional-access-intune-reassign/reassign-ca-3.png)

    > [!TIP] 
    > 如果多个应用具有相同的策略，请考虑在 Azure 门户中将其并入一个策略。

10. 在“分配”部分下，选择“条件”   。

11. 在“条件”边栏选项卡上，选择“设备平台”，然后选择适用的设备平台   。

12. 选完设备平台后，单击两次“完成”  。

    ![Intune 和 Azure 门户之间的设备平台用户界面比较图](./media/conditional-access-intune-reassign/reassign-ca-4.png)

    > [!TIP] 
    > 如果在 Intune 经典门户中选择了单个平台，请在 Azure 门户中选择单个平台。

    > [!NOTE] 
    > 可在以后指定适用于 Windows 的域加入或兼容选项。

13. 在“分配”部分下，选择“条件”   。

14. 在“条件”边栏选项卡上，选择“客户端应用”，然后选择适用的客户端应用   。

15. 选完客户端应用后，单击两次“完成”  。

    ![Intune 和 Azure 门户之间的客户端应用用户界面比较图](./media/conditional-access-intune-reassign/reassign-ca-6.png)

16. 如果在 Intune 经典门户中选择了浏览器设置，请在 Azure 门户中同时选择“浏览器”和“移动应用和桌面客户端”   。 如果在 Intune 经典门户中未选择浏览器设置，则只需选择“移动应用和桌面客户端”  。 

17. 在“访问控制”部分下，选择“授予”   。

18. 在“授予访问控制”下，选择“要求设备标记为兼容”，然后单击“选择”    。

19. 如果有一个策略需要加入域的 Windows 设备，但同时需要允许注册了 Intune 的兼容 Windows 设备，请同时选择“需要加入域的设备”、“要求设备标记为兼容”和“需要一个所选控制”    。

20. 如果不允许注册了 Intune 的兼容 Windows 设备，则将 Windows 策略从当前策略中免除。 然后创建一个单独的策略，其中将“设备平台”设置为“Windows”，并按上述方式设置来包含其他条件，然后在“授予访问控制”下选择“需要加入域的设备”     。

21. 在“新建条件访问策略”边栏选项卡上，打开“启用策略”开关，然后单击“创建”    。

    ![Intune 和 Azure 之间的启用条件访问策略用户界面比较图](./media/conditional-access-intune-reassign/reassign-ca-11.png)

## <a name="reassign-intune-device-based-conditional-access-policies-for-eas-clients"></a>为 EAS 客户端重新分配基于设备的 Intune 条件访问策略

如果在 Intune 经典门户中将 Exchange ActiveSync 设置配置为了 Exchange Online 策略的一部分，则需要在 Azure 门户中创建第二个条件访问策略。

1. 转到 [Azure 门户中的条件访问](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/Policies)，并用自己的凭据登录。

2. 选择“新策略”  。

3. 提供策略的名称。

4. 在“分配”部分下，选择“用户和组”以应用新条件访问策略   。

    ![Azure 和 Intune 门户之间的用户组用户界面比较图](./media/conditional-access-intune-reassign/reassign-ca-12.png)

    > [!IMPORTANT] 
    > 对 Azure 门户做出的选择应与之前对 Azure 门户做出的选择相对应。 例如，如果在 Intune 经典门户中选择了所有用户，则应在 Azure 门户中选择“所有用户”  。 另外，如果在 Intune 经典门户中选择了“免除组”选项，则还需要在 Azure 门户中排除所选的这些组  。

5. 选择组后，单击“选择”，然后单击“完成”   。

6. 在“分配”部分下，选择“云应用”   。

7. 在“云应用”边栏选项卡上，单击“选择应用”，然后选择“Exchange Online”    。 然后依次单击“选择”和“完成”   。

    ![Intune 和 Azure 门户之间的云应用用户界面比较图](./media/conditional-access-intune-reassign/reassign-ca-14.png)

    > [!IMPORTANT] 
    > EAS 客户端的条件性访问策略不能包含任何其他云应用。

8. 在“条件”边栏选项卡上，选择“客户端应用”，然后选择适用的客户端应用   。 如果选择阻止 Intune 不支持的客户端，请使用“仅将策略应用于支持的平台”选项  。

    ![Azure 和 Intune 门户之间的客户端应用用户界面比较图](./media/conditional-access-intune-reassign/reassign-ca-15.png)

9. 选完客户端应用后，单击两次“完成”  。

10. 在“访问控制”部分下，选择“授予”   。

11. 在“授予访问控制”下，选择“要求设备标记为兼容”，然后单击“选择”    。

    ![Intune 和 Azure 门户之间的授予访问权限用户界面比较图](./media/conditional-access-intune-reassign/reassign-ca-16.png)

12. 在“新建条件访问策略”边栏选项卡上，打开“启用策略”开关，然后单击“创建”    。

    ![Intune 和 Azure 之间的启用条件访问策略用户界面比较图](./media/conditional-access-intune-reassign/reassign-ca-17.png)

> [!NOTE]
> 如果配置“设备平台”，则保存策略会失败，并会显示错误“不支持策略配置”  。 Exchange ActiveSync 无法识别连接设备所使用的平台。 因此，为 Exchange ActiveSync 设备创建策略时，配置特定设备平台不受支持。

## <a name="disable-conditional-access-policies-in-the-intune-classic-portal"></a>禁用 Intune 经典门户中的条件访问策略

在 Azure 门户中重新分配条件访问策略后，请务必逐渐禁用之前在 Intune 经典门户中创建的条件访问策略。 此外，可能需要使用同一安全组来应用在 Azure 门户中创建的条件访问策略。

> [!NOTE]
> 在 Intune 经典门户中禁用条件访问策略之前，请先阅读本主题开头部分的[开始前的准备工作](#before-you-begin)。

### <a name="to-disable-the-conditional-access-policies"></a>禁用条件访问策略

由于已从 Intune 经典门户中删除 MDM，因此提供了以下链接来查看/禁用这些经典策略：

[https://portal.azure.com/?microsoft_aad_iam_classicPolicyDontHide=true#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/ClassicPolicies](https://portal.azure.com/?microsoft_aad_iam_classicPolicyDontHide=true#blade/Microsoft_AAD_IAM/ConditionalAccessBlade/ClassicPolicies)

## <a name="see-also"></a>另请参阅

- [使用 Intune 条件访问的常见方式](conditional-access-intune-common-ways-use.md)
- [基于应用的 Intune 条件访问](app-based-conditional-access-intune.md)
- [Azure Active Directory 中的条件访问](/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)