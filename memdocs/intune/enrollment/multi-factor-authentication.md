---
title: 对 Intune 设备注册要求多重身份验证
titleSuffix: Microsoft Intune
description: 如何在 Azure AD 中要求对 Intune 设备注册进行多重身份验证。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/22/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 94280c73-c05c-4e72-b0dd-a7cb997782f9
ROBOTS: ''
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2ec03d186b0b5d64b5b867cf413f477d9ded79e9
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79345099"
---
# <a name="require-multi-factor-authentication-for-intune-device-enrollments"></a>对 Intune 设备注册要求多重身份验证

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune 可以使用 Azure Active Directory (AD) 多重身份验证 (MFA) 进行设备注册，从而帮助保护公司资源的安全。

MFA 需要使用以下任意两种或多种验证方法：

- 你知道的信息（通常为密码或 PIN）。
- 你拥有的东西（不容易复制的受信任设备，如手机）。
- 你的生物特征（指纹等生物特征）。

iOS/iPadOS、Android、Windows 8.1 或更高版本、Windows Phone 8.1、Windows 10 移动版或更高版本的设备均支持 MFA。

启用 MFA 后，最终用户必须提供两种形式的凭据才能注册设备。

## <a name="configure-intune-to-require-multi-factor-authentication-at-device-enrollment"></a>将 Intune 配置为要求对设备注册进行多重身份验证

若要在注册设备时需要 MFA，请执行以下步骤：

>[!Important]
>必须将 Azure Active Directory Premium P1 或更高版本分配给用户才能实现此策略。

>[!Important]
>请勿为 Microsoft Intune 注册配置基于设备的访问规则  。

1. 登录 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，选择“设备” > “条件访问”   。 从 Intune 访问的条件访问节点与从 Azure AD 访问的节点相同   。
2. 选择“新策略”  。
3. 在“新建”策略中，为策略键入描述性名称  。
4. 在“分配”部分中，选择“用户和组”   。 
5. 在“用户和组”中，选择“选择用户或组”，然后选择“用户和组”    。 然后选择将接收此策略的用户和/或组，再选择“完成”  。
6. 在“分配”部分中，选择“云应用”   。
7. 在“云应用”的“包括”选项卡上，选择“选择应用”，然后选择“选择” > “Microsoft Intune 注册”，然后选择“完成”       。 通过选择“Microsoft Intune 注册”  ，条件访问 MFA 仅应用于设备注册（一次性 MFA 提示）。
8. 在“分配”部分中，对于“条件”，无需为 MFA 配置任何设置   。
9. 在“访问控制”部分中，选择“授予”   。
10. 在“授予”中，选择“授予访问权限”，然后选择“要求多重身份验证”    。 不要选择“要求设备标记为合规”，因为设备要注册之后才能进行评估以确定其是否合规  。 然后选取“选择”  。
11. 在“新建策略”中，选择“启用策略” > “开”，然后选择“创建”     。



## <a name="next-steps"></a>后续步骤

现在最终用户注册其设备时，必须使用 PIN、电话或生物特征等第二种形式进行身份验证。
