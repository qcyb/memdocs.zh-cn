---
title: 查看 BitLocker 报表
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中的 BitLocker 管理报表
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: reference
ms.assetid: 0bae9477-0500-41cf-8aa3-5e6efadd0554
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7c44ec9a9ed91d8543fedbdd5fba191b3989da19
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129200"
---
# <a name="view-bitlocker-reports"></a>查看 BitLocker 报表

适用范围：  Configuration Manager (Current Branch)

<!--3601034-->

在 Reporting Services 点上[安装报表](setup-websites.md)后，可以查看报表。 这些报表显示企业和单个设备的 BitLocker 符合性。 它们提供表格形式的信息和图表，并且具有使你能够从不同的角度查看数据的筛选器。

在 Configuration Manager 控制台中，转到“监视”工作区，展开“报表”，然后选择“报表”节点    。 以下报表位于“BitLocker 管理”类别中  ：

- [BitLocker 计算机相容性](#bkmk-compliancereport)

- [Bitlocker 企业相容性仪表板](#bkmk-dashboard)

- [BitLocker 企业相容性详细信息](#bkmk-compliancedetails)

- [Bitlocker 企业相容性摘要](#bkmk-compliancesummary)

- [恢复审核报告](#bkmk-audit)

可以直接从 Reporting Services 点网站访问以上全部报表。

> [!NOTE]
> 为了使这些报表显示完整的数据：
>
> - 创建 BitLocker 管理策略并将其部署到设备集合
> - 目标集合中的客户端需要发送硬件清单

## <a name="bitlocker-computer-compliance"></a><a name="bkmk-compliancereport"></a>BitLocker 计算机相容性

使用此报告收集特定于计算机的信息。 它提供有关操作系统 (OS) 驱动器以及任何固定数据驱动器的详细加密信息。 要查看每个驱动器的详细信息，请展开“计算机名”项。 它还指示应用于计算机上每种驱动器类型的策略。

:::image type="content" source="media/bitlocker-computer-compliance.png" alt-text="BitLocker 计算机符合性报表的示例屏幕截图" lightbox="media/bitlocker-computer-compliance.png":::

还可以使用此报表来确定丢失或被盗计算机的最后已知 BitLocker 加密状态。 Configuration Manager 根据所部署的 BitLocker 策略确定设备的符合性。 尝试确定设备的 BitLocker 加密状态之前，请先验证已部署到其中的策略。

> [!NOTE]
> 此报表不显示可移动数据卷的加密状态。

### <a name="computer-details"></a>计算机详细信息

|列&nbsp;名称|说明|
|----------------|----|
|计算机名称|由用户指定的 DNS 计算机名。|
|域名|计算机的完全限定域名。|
|计算机类型|计算机类型，有效类型为“非便携式”和“便携式”   。|
|操作系统|计算机 OS 类型。|
|总体相容性|计算机的总体 BitLocker 符合性状态。 有效状态为“相容”和“不相容”   。 [每个驱动器的符合性状态](#bkmk_volume)可能指示不同的符合性状态。 但是，此字段依据指定的策略来表示该相容性状态。|
|操作系统相容性|计算机上的 OS 的相容性状态。 有效状态为“相容”和“不相容”   。|
|固定数据驱动器相容性|计算机上固定数据驱动器的符合性状态。 有效状态为“相容”和“不相容”   。|
|上次更新日期|计算机上次与服务器联系以报告相容性状态的日期和时间。|
|例外|表明用户是否从 BitLocker 策略中免除。|
|免除的用户|从 BitLocker 策略中免除的用户。|
|免除日期|准予免除的日期。|
|符合性状态详细信息|基于指定策略的计算机相容性状态的相关错误和状态消息。|
|策略密码长度|在 BitLocker 管理策略中选择的密码长度。|
|策略：操作系统驱动器|指示是否需要加密 OS 驱动器以及合适的保护程序类型。|
|策略：固定数据驱动器|指示是否需要加密固定数据驱动器。|
|制造商|计算机 BIOS 中显示的计算机制造商名称。|
|型号|计算机 BIOS 中显示的计算机制造商型号名称。|
|设备用户|计算机上的已知用户。|

### <a name="computer-volume"></a><a name="bkmk_volume"></a> 计算机卷

|列&nbsp;名称|说明|
|----------------|----|
|驱动器号|计算机上的驱动器号。|
|驱动器类型|驱动器的类型。 有效值为“操作系统驱动器”和“固定数据驱动器”   。 这些项是物理驱动器，而不是逻辑卷。|
|密码长度|在 BitLocker 管理策略中选择的密码长度。|
|保护程序类型|在策略中选择的用于加密驱动器的保护程序类型。 OS 驱动器的有效保护程序类型为“TPM”或“TPM+PIN”   。 固定数据驱动器的有效保护程序类型为“密码”  。|
|保护程序状态|指示计算机已启用在策略中指定的保护程序类型。 有效状态为“打开”或“关闭”   。|
|加密状态|驱动器的加密状态。 有效状态为“已加密”、“未加密”或“加密进行中”    。|

## <a name="bitlocker-enterprise-compliance-dashboard"></a><a name="bkmk-dashboard"></a>BitLocker 企业相容性仪表盘

此报告提供以下关系图，它们显示了整个组织中的 BitLocker 符合性状态：

- 相容性状态分发

- 不相容 - 错误分发

- 按驱动器类型进行的相容性状态分发

:::image type="content" source="media/bitlocker-enterprise-compliance-dashboard.png" alt-text="BitLocker 企业相容性仪表板 示例屏幕截图" lightbox="media/bitlocker-enterprise-compliance-dashboard.png":::

### <a name="compliance-status-distribution"></a>相容性状态分发

此饼图显示组织中计算机的符合性状态。 它还显示具有该相容性状态的计算机与所选集合中的计算机总数相比所占的百分比。 此外还显示每种状态下的计算机的实际数量。

此饼图显示下列相容性状态：

- 合规

- 不符合

- 用户例外

- 临时用户例外

- 未强制实施的策略

- 未知。 这些计算机报告了状态错误，或属于集合，但是从未报告其相容性状态。 如果计算机与组织断开连接，则可能缺少相容性状态。

### <a name="non-compliant---errors-distribution"></a>不相容 - 错误分发

此饼图显示组织中不符合 BitLocker 驱动器加密策略的计算机类别。 它还显示每个类别中的计算机数量。 该报表根据集合中不符合的计算机总数计算每个类别的百分比。

- 用户推迟加密

- 找不到兼容的 TPM

- 系统分区不可用或不足够大

- TPM 可见，但未初始化

- 策略冲突

- 正在等待 TPM 自动设置

- 发生了未知错误

- 无信息。 这些计算机未安装 BitLocker 管理代理，或者已安装但未激活。 例如，服务无法正常工作。

### <a name="compliance-status-distribution-by-drive-type"></a>按驱动器类型进行的相容性状态分发

此条形图按驱动器类型显示当前的 BitLocker 相容性状态。 状态是“相容”和“不相容”   。 将为固定数据驱动器和 OS 驱动器显示条形。 该报表包括没有固定数据驱动器的计算机，并且仅在“操作系统驱动器”栏中显示值  。 图形中不包括已从 BitLocker 驱动器加密策略或“无策略”类别中免除的用户。

## <a name="bitlocker-enterprise-compliance-details"></a><a name="bkmk-compliancedetails"></a>BitLocker 企业相容性详细信息

此报表显示有关整个组织中部署了 BitLocker 管理策略的计算机集合的总体 BitLocker 符合性信息。

:::image type="content" source="media/bitlocker-enterprise-compliance-details.png" alt-text="BitLocker 企业相容性详细信息 示例屏幕截图" lightbox="media/bitlocker-enterprise-compliance-details.png":::

|列名称|说明|
|--- |--- |
|被管理的计算机|已部署 BitLocker 管理策略的计算机的数量。|
|% 符合|组织中的相容计算机的百分比。|
|% 不符合|组织中的不相容计算机的百分比。|
|% 未知相容性|相容性状态为未知的计算机的百分比。|
|% 例外|未免除 BitLocker 加密要求的计算机的百分比。|
|% 无例外|未免除 BitLocker 加密要求的计算机的百分比。|
|合规|组织中的相容计算机计数。|
|不符合|组织中的不相容计算机计数。|
|未知相容性|相容性状态为未知的计算机的计数。|
|例外|免除 BitLocker 加密要求的计算机的总数。|
|无例外|未免除 BitLocker 加密要求的计算机的总数。|

### <a name="computer-details"></a>计算机详细信息

|列名称|说明|
|--- |--- |
|计算机名称|受管理设备的 DNS 计算机名。|
|域名|计算机的完全限定域名。|
|符合性状态|计算机的总体相容性状态。 有效状态为“相容”和“不相容”   。|
|例外|表明用户是否从 BitLocker 策略中免除。|
|设备用户|设备的用户。|
|符合性状态详细信息|基于指定策略的计算机相容性状态的相关错误和状态消息。|
|上次联系|计算机上次与服务器联系以报告相容性状态的日期和时间。|

## <a name="bitlocker-enterprise-compliance-summary"></a><a name="bkmk-compliancesummary"></a>BitLocker 企业相容性摘要

使用此报表显示整个组织的 BitLocker 符合性情况。 它还显示了部署了 BitLocker 管理策略的单个计算机的符合性。

:::image type="content" source="media/bitlocker-enterprise-compliance-summary.png" alt-text="BitLocker 企业相容性摘要 示例屏幕截图" lightbox="media/bitlocker-enterprise-compliance-summary.png":::

|列名称|说明|
|--- |--- |
|被管理的计算机|使用 BitLocker 策略进行管理的计算机的数量。|
|% 符合|组织中的相容计算机的百分比。|
|% 不符合|组织中的不相容计算机的百分比。|
|% 未知相容性|相容性状态为未知的计算机的百分比。|
|% 例外|未免除 BitLocker 加密要求的计算机的百分比。|
|% 无例外|未免除 BitLocker 加密要求的计算机的百分比。|
|合规|组织中符合的计算机的计数。|
|不符合|组织中不符合的计算机的计数。|
|未知相容性|相容性状态为未知的计算机的计数。|
|例外|免除 BitLocker 加密要求的计算机的总数。|
|无例外|未免除 BitLocker 加密要求的计算机的总数。|

## <a name="recovery-audit-report"></a><a name="bkmk-audit"></a>恢复审核报告

> [!NOTE]
> 自版本 2002 起，只能从 [BitLocker 管理和监视网站](helpdesk-portal.md#reports)获取此报表。<!-- 7629549 -->

使用此报告审核已请求对 BitLocker 恢复密钥进行访问的用户。 可根据以下条件进行筛选：

- 特定类型的用户，例如支持人员用户或最终用户
- 如果请求失败或成功
- 请求的特定类型的密钥：恢复密钥密码、恢复密钥 ID 或 TPM 密码哈希
- 日期范围，在此期间会发生检索

:::image type="content" source="media/bitlocker-recovery-audit-report.png" alt-text="BitLocker 恢复审核报表的示例屏幕截图" lightbox="media/bitlocker-recovery-audit-report.png":::

|列&nbsp;名称|说明|
|----------------|----|
|请求日期和时间|最终用户或支持人员用户请求密钥的日期和时间。|
|审核请求源|发出请求的站点。 有效值为“自助服务门户”或“支持人员” 。|
|请求结果|请求的状态。 有效值为“成功”或“失败” 。|
|支持人员用户|请求密钥的管理用户。 如果支持管理员在未指定用户名的情况下恢复密钥，则“最终用户”字段为空。 标准支持人员用户必须指定将在此字段中显示的用户名。 对于通过自助服务门户进行的恢复，此字段和“最终用户”字段将显示发出请求的用户的名称。|
|最终用户|请求密钥检索的用户的名称。|
|Computer|恢复的计算机的名称。|
|密钥类型|用户请求的密钥类型。 三种密钥类型为：<br/><br/>-  恢复密钥密码：用于在恢复模式下恢复计算机<br/>- 恢复密钥 ID：用于在恢复模式下恢复另一个用户的计算机****<br/>-  TPM 密码哈希：用于恢复具有锁定的 TPM 的计算机|
|原因说明|用户为何基于其在表单中选择的选项来请求指定的密钥类型。|
