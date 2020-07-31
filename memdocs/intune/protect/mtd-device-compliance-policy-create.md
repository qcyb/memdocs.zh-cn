---
title: 使用 Microsoft Intune 创建移动威胁防御 (MTD) 设备合规性策略
titleSuffix: Microsoft Intune
description: 创建使用 MTD 合作伙伴威胁级别的 Intune 设备符合性策略，以确定移动应用是否可以访问公司资源。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/28/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5d12254f-ffab-4792-b19c-ab37f5e02f35
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 88f8a2ff04f536370f613341170e7fae0a808ff6
ms.sourcegitcommit: 19f5838eb3eb8724d22382f36f9564ac9a978b97
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "87365519"
---
# <a name="create-mobile-threat-defense-mtd-device-compliance-policy-with-intune"></a>使用 Intune 创建移动威胁防御 (MTD) 设备符合性策略

搭载 MTD 的 Intune 可帮助检测移动设备上存在的威胁和评估相关风险。 可创建评估风险的 Intune 设备符合性策略规则，确定设备是否合规。 然后可使用[条件访问策略](create-conditional-access-intune.md)，根据设备符合性阻止对服务的访问。

> [!NOTE]
> 此信息适用于所有移动威胁防御合作伙伴。

## <a name="before-you-begin"></a>在开始之前

在 MTD 设置过程中，需在 MTD 合作伙伴控制台中创建一个将各种威胁分类为高、中和低的策略。 接下来，将在 Intune 设备合规性策略中设置移动威胁防御级别。

MTD 设备符合性策略先决条件：

- 使用 Intune 设置 MTD 集成

## <a name="to-create-an-mtd-device-compliance-policy"></a>创建 MTD 设备符合性策略

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“终结点安全性” > “设备合规性” > “创建策略”。

3. 选择“平台”，然后选择“创建”。

4. 在“基本”上，指定设备合规性策略“名称”和“描述”（可选）。 选择“下一步”继续操作。


5. 在“符合性设置”上，展开并配置“设备运行状况”。 从“要求设备不超过设备威胁级别”的下拉列表中选择“移动威胁级别”。

   - **安全**：此级别是最安全的。 设备不能存在任何威胁，且仍可访问公司资源。 如果发现了任何威胁，设备都会被评估为不符合。

   - **低**：如果设备上仅存在低级威胁，则该设备符合要求。 低级以上的任意威胁都将使设备不合规。

   - **中**：如果有低级别或中等级别威胁，则设备符合要求。 如果检测到高级别威胁，则设备会被确定为不合规。

   - **高**：此威胁级别的安全性最低并且允许所有威胁级别，且仅将移动威胁防御用作报告目的。 设备必须使用此设置激活 MTD 应用。

6. 选择“下一步”前进到“分配”。 选择将接收此配置文件的组。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](../configuration/device-profile-assign.md)。

   选择“下一步”。

7. 完成后，在“查看 + 创建”页上，选择“创建” 。 为创建的配置文件选择策略类型时，新配置文件将显示在列表中。

> [!IMPORTANT]
> 如果为 Office 365 或其他服务创建条件访问策略，将评估设备的符合性并阻止不符合设备访问公司资源，直到解决威胁。

## <a name="to-assign-an-mtd-device-compliance-policy"></a>分配 MTD 设备符合性策略

若要将设备合规性策略分配给用户或更改其分配，请执行以下操作：

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“终结点安全性” > “设备合规性”。

3. 选择要分配给用户的策略，然后选择“属性”。

4. 选择“编辑”进行分配，然后使用可用选项包括和排除组以接收此策略。   

5. 选择“查看 + 保存”以完成分配。 保存分配时，会将策略部署到所选用户，并评估其设备的符合性。

## <a name="next-steps"></a>后续步骤

[通过 Intune 启用 MTD](mtd-connector-enable.md)
