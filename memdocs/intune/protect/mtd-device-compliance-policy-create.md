---
title: 使用 Microsoft Intune 创建 MTD 设备符合性策略
titleSuffix: Microsoft Intune
description: 创建使用 MTD 合作伙伴威胁级别的 Intune 设备符合性策略，以确定移动应用是否可以访问公司资源。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/20/2019
ms.topic: conceptual
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
ms.openlocfilehash: c5c9baa75474161d7ae5260522a1e28f8c05c2a3
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79351534"
---
# <a name="create-mobile-threat-defense-mtd-device-compliance-policy-with-intune"></a>使用 Intune 创建移动威胁防御 (MTD) 设备符合性策略

搭载 MTD 的 Intune 可帮助检测移动设备上存在的威胁和评估相关风险。 可创建评估风险的 Intune 设备符合性策略规则，确定设备是否合规。 然后可使用[条件访问策略](create-conditional-access-intune.md)，根据设备符合性阻止对服务的访问。

> [!NOTE]
> 此信息适用于所有移动威胁防御合作伙伴。

## <a name="before-you-begin"></a>在开始之前

在 MTD 设置过程中，需在 MTD 合作伙伴控制台中创建一个将各种威胁分类为高、中和低的策略。 现在需要在 Intune 设备符合性策略中设置移动威胁防御级别。

MTD 设备符合性策略先决条件：

- 使用 Intune 设置 MTD 集成

## <a name="to-create-an-mtd-device-compliance-policy"></a>创建 MTD 设备符合性策略

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“设备”   > “符合性策略”   > “创建策略”  。

3. 指定“名称”  、“说明”  ，选择“平台”  ，然后选择“设置”  部分下的“配置”  。

4. 在“符合性策略”窗格中，选择“设备运行状况”   。

5. 在“设备运行状况”  窗格中，从“要求设备不高于设备威胁级别”  的下拉列表中选择移动威胁级别。

   - **安全**：此级别是最安全的。 设备不能存在任何威胁，且仍可访问公司资源。 如果发现了任何威胁，设备都会被评估为不符合。

   - **低**：如果设备上仅存在低级威胁，则该设备符合要求。 低级以上的任意威胁都将使设备不合规。

   - **中**：如果有低级别或中等级别威胁，则设备符合要求。 如果检测到高级别威胁，则设备会被确定为不合规。

   - **高**：此级别是最不安全的威胁级别。 此选项将许可所有威胁级别，且仅将移动威胁防御用作报告目的。 设备必须使用此设置激活 MTD 应用。

6. 选择“确定”  两次，然后选择“创建”  以创建策略。

> [!IMPORTANT]
> 如果为 Office 365 或其他服务创建条件访问策略，将评估设备的符合性并阻止不符合设备访问公司资源，直到解决威胁。

## <a name="to-assign-an-mtd-device-compliance-policy"></a>分配 MTD 设备符合性策略

向用户分配设备符合性策略：

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“设备”   > “符合性策略”  。

3. 选择要分配给用户的策略，然后选择“分配”  。 使用可用选项包括  和排除  组以接收此策略。  

4. 选择“保存”以完成分配。 保存分配时，会将策略部署到所选用户，并评估其设备的符合性。

## <a name="next-steps"></a>后续步骤

[通过 Intune 启用 MTD](mtd-connector-enable.md)
