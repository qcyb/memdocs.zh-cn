---
title: 在 Azure 中我的 Intune 功能处于哪个位置？
titleSuffix: Microsoft Intune
description: 有助于在 Azure 门户中找到 Microsoft Intune 功能。
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 1/4/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 809d9d76-20f8-4329-9e18-cd7d4946a9af
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5ff2898f97bbef4cba0d14d4810a503d613cff18
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "82077914"
---
# <a name="where-did-my-intune-feature-go-in-azure"></a>在 Azure 中我的 Intune 功能处于哪个位置？
我们已将 Intune 移动到 Azure 门户，借此机会我们以更有逻辑的方式整理了某些任务。 但每一次改进都需要熟悉新的布局整理。 本参考指南面向非常熟悉经典门户中的 Intune 且想知道如何使用 Azure 门户中的 Intune 完成工作的用户。 如果本文不含你要查找的功能，请在文章末尾处留下评论，以便我们能够更新本文。
## <a name="quick-reference-guide"></a>快速参考指南

|功能 |经典门户中的路径|Azure 门户中 Intune 内的路径|
|------------|---------------|---------------|
|设备注册计划 (DEP) [仅限 iOS]|管理员 > 移动设备管理 > iOS > 设备注册计划|[设备注册 > Apple 注册 > 注册计划令牌](#where-did-apple-dep-go) |
|设备注册计划 (DEP) [仅限 iOS]| 管理员 > 移动设备管理 > iOS 和 Mac OS X > 设备注册计划 |[设备注册 > Apple 注册 > 注册计划序列号](#where-did-apple-dep-go) |
|注册规则 |管理员 > 移动设备管理 > 注册规则|[设备注册 > 注册限制](#where-did-enrollment-rules-go) |
|按 iOS 序列号分组 |组 > 所有设备 > 企业预注册设备 > 按 iOS 序列号|[设备注册 > Apple 注册 > 注册计划序列号](#where-did-corporate-pre-enrolled-devices-go) |
|按 iOS 序列号分组 |组 > 所有设备 > 企业预注册设备 > 按 iOS 序列号| [设备注册 > Apple 注册 > AC 序列号](#where-did-corporate-pre-enrolled-devices-go)|
|按 IMEI 分组（所有平台）| 组 > 所有设备 > 企业预注册设备 > 按 IMEI（所有平台） | [设备注册 > 公司设备标识符](#by-imei-all-platforms)|
| 公司设备注册配置文件| 策略 > 企业设备注册 | [设备注册 > Apple 注册 > 注册计划配置文件](#where-did-corporate-pre-enrolled-devices-go) |
| 公司设备注册配置文件 | 策略 > 企业设备注册 | [设备注册 > Apple 注册 > AC 配置文件](#where-did-corporate-pre-enrolled-devices-go) |
| Android for Work | 管理员 > 移动设备管理 > Android for Work | 设备注册 > Android 注册 |
| 条款和条件 | 策略 > 条款和条件 | 设备注册 > 条款和条件 |
“公司门户”设置|“管理”>“公司门户”|“管理”  >“移动应用”<br> “设置”  >“‘公司门户’品牌”


## <a name="where-do-i-manage-groups"></a>在哪个位置管理组？
Azure 门户中 Intune 使用 [Azure Active Directory (AD)](https://docs.microsoft.com/azure/active-directory/active-directory-groups-create-azure-portal) 管理组。

## <a name="where-did-enrollment-rules-go"></a>注册规则在处于哪个位置？
在经典门户中，可以设置规则来管理新式移动 Windows 和 macOS 设备的 MDM 注册。

![经典移动设备注册规则的图像](./media/ui-changes/01-classic-rules.png)

这些规则适用于你的 Intune 帐户中没有异常的所有用户。 在 Azure 门户中，这些规则现在以两种不同的策略类型显示：设备类型限制和设备限制限制。

![Azure 移动设备注册限制的图像](./media/ui-changes/02-azure-enroll-restrictions.png)

默认的“设备限制”对应于经典门户中的“设备注册限制”。

![Azure 设备限制的图像](./media/ui-changes/03-azure-device-limit.png)

默认的“设备类型限制”对应于经典门户中的“平台限制”。

![Azure 设备类型限制的图像](./media/ui-changes/04-azure-platform-restrictions.png)

现在，允许或阻止个人拥有的设备的功能在“设备类型限制”的“平台配置”下进行管理。

![Azure 个人设备阻止块设置的图像](./media/ui-changes/05-azure-personal-block.png)

新限制功能仅添加到 Azure 门户。

## <a name="where-did-my-conditional-access-policies-go"></a>我的条件访问策略会去向何处？
在你的租户迁移到 Azure 门户后，还会继续强制执行你租户的条件访问策略。 但是，你无法在 Azure 门户中的 Intune 中查看或修改这些策略。

若要在 Azure 门户中查看和修改条件访问策略，需要从经典门户中删除旧策略。 然后在 Azure 门户中创建策略。 若要详细了解如何迁移条件访问策略，请参阅[在 Azure 门户中迁移经典策略](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-migration)。 

## <a name="where-did-my-compliance-policies-go"></a>符合性策略去哪了？
你的租户迁移到 Azure 门户后，租户的符合性策略将继续强制使用。 但是，你无法在 Azure 门户中的 Intune 中查看或修改这些策略。

如果希望在 Azure 门户中查看和修改符合性策略，需要从经典门户中删除旧策略。 然后在 Azure 门户中创建策略。 有关设备符合性策略的详细信息，请参阅 [Intune 中的设备符合性策略入门](../protect/device-compliance-get-started.md)。 

## <a name="where-did-apple-dep-go"></a>Apple DEP 处于哪个位置？
在经典门户中，可以将 Intune 设置为与 Apple 设备注册计划集成，并手动请求与 Apple 服务同步：

![经典 DEP 令牌的图像](./media/ui-changes/06-classic-dep-token.png)

在 Azure 门户中，你将使用 Intune 经典控制台中所用的相同步骤设置 Apple 设备注册计划：

![Azure DEP 令牌的图像](./media/ui-changes/07-azure-dep-token.png)

不过，经典门户中的“同步”  选项已迁移到序列号管理工作流，因为手动同步结果已列于其中：

![Azure DEP 同步的图像](./media/ui-changes/08-azure-dep-sync.png)

## <a name="where-did-corporate-pre-enrolled-devices-go"></a>企业预注册设备处于哪个位置？
### <a name="by-ios-serial-number"></a>按 iOS 序列号排列
在经典门户中，可以通过 Apple 设备注册计划 (DEP) 和 Apple 配置器工具注册 iOS 设备。 这两种方法都按序列号提供设备预注册，并且设计分配特殊企业设备注册的配置文件。 注册之前，可以通过“按 iOS 序列号排列的企业预注册设备”  设备组管理注册配置文件的分配：

![经典 Apple 序列号的图像](./media/ui-changes/09-classic-apple-serials.png)

这将列出单个列表中 Apple DEP 和 Configurator 注册的序列号。 为了减少配置文件的不匹配分配（将 DEP 配置文件分配到 AC 序列号，反之亦然），我们在 Azure 门户上将序列号分成两个列表：

**DEP 序列号**
![Azure DEP 序列号的图像](./media/ui-changes/10-azure-dep-serials.png)

**Apple Configurator 序列号**
![Azure Apple Configurator 序列号的图像](./media/ui-changes/11-azure-ac-serials.png)

### <a name="by-imei-all-platforms"></a>按 IMEI 排列（所有平台）

在经典门户中，可以预先列出设备的 IMEI 号码，以便在注册到 Intune 时将它们标记为公司设备：

![IMEI 号码经典列表的图像](./media/ui-changes/12-classic-corp-imei.png)

在 Azure 门户中，必须使用逗号分隔值 (csv) 文件，将相同的 IMEI 上传到公司设备标识符列表。 新门户不支持手动输入 IMEI 号码：

![IMEI 号码 Azure 列表的图像](./media/ui-changes/13-azure-corp-imei.png)

除了 IMEI，Azure 门户中的 Intune 还会适应未来，支持其他类型的标识符，但目前只允许预先列出 IMEI号码。

## <a name="where-did-corporate-device-enrollment-profiles-go"></a>公司设备注册配置文件处于哪个位置？
若要通过 Apple 设备注册计划或 Apple 配置器工具注册 iOS 设备，则必须提供要分配给设备的公司设备注册配置文件。 在经典门户中，这些配置文件是在一个列表中进行创建和管理：

![经典设备注册配置文件的图像](./media/ui-changes/14-classic-corp-profiles.png)

此列表显示可用于 Apple 设备注册计划的配置文件（**DEP 开启**）和仅可用于 Apple 配置器工具的配置文件（**DEP 关闭**）。

为了减少两种配置文件类型之间的混淆以及潜在的不匹配分配（将 DEP 配置文件分配到配置器设备，反之亦然），我们将注册计划配置文件（支持 Apple 设备注册计划和 Apple 校园教务管理）与 Apple 配置器配置文件的创建和管理进行了分离：

**DEP 配置文件**
![Azure DEP 配置文件的图像](./media/ui-changes/15-azure-dep-profiles.png)

**Apple 配置器配置文件**
![Azure Apple 配置器配置文件的图像](./media/ui-changes/16-azure-ac-profiles.png)
