---
title: 桌面分析数据隐私
titleSuffix: Configuration Manager
description: 桌面分析致力于保护客户数据隐私
ms.date: 12/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: dd970dc1517a6fcc197b2bf39a141871b4999a02
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268413"
---
# <a name="desktop-analytics-data-privacy"></a>桌面分析数据隐私

桌面分析致力于围绕以下原则保护客户数据隐私：

- **透明度：** 我们会全面记录 Windows 诊断事件。 与贵公司的安全性和合规性团队一起查看它们。 Windows 诊断数据查看器可用于查看从给定设备发送的诊断数据。 有关详细信息，请参阅[诊断数据查看器概述](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview)。  

- **控制：** 可以控制要与 Microsoft 共享的诊断数据级别。 Windows 10 版本 1709 添加了一项新策略，可将增强的诊断数据限制为桌面分析所需的最小量。  

- **安全性：** Microsoft 通过强大的安全和加密措施来保护数据。  

- **信任：** 桌面分析支持 Microsoft [隐私声明](https://privacy.microsoft.com/privacystatement)和[联机服务条款](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46)。  

有关详细信息，请参阅 [Microsoft 依照 GDPR 充当处理者的 Windows 服务](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance#windows-services-where-microsoft-is-the-processor-under-the-gdpr)。<!-- 5353168 -->

## <a name="data-flow"></a>数据流

下图显示了各个设备中的诊断数据如何通过诊断数据服务、暂时存储流向 Log Analytics 工作区：

![说明设备中诊断数据流的关系图](media/da-data-flow.png)

1. 登录到 Azure 门户，并载入桌面分析。 创建 Azure AD 应用以与 Configuration Manager 连接。 设置桌面分析时，会在所选位置创建 Azure Log Analytics 工作区。  

2. 连接 Configuration Manager 并注册设备  

    1. 在 Configuration Manager 中配置桌面分析云服务，其中包含 Azure AD 应用详细信息。  

    2. 在 15 分钟内，Configuration Manager 使用你的租户 ID 将以下数据与桌面分析同步。 此过程每小时重复一次。

      - 有关[创建部署计划](create-deployment-plans.md)所需的设备集合的信息。 此信息包括集合 ID、层次结构 ID、集合名称和设备计数。 
      - [注册设备](enroll-devices.md)所需的信息。 此信息包括集合 ID、SMS 唯一标识符、OS 内部版本、设备名称和序列号。
      - [监视器连接运行状况](monitor-connection-health.md)仪表板中的信息。 此信息包括处于每个运行状态的设备计数和设备属性。
      - 有关部署计划的信息，包括集合 ID、部署 ID、试点或生产部署类型以及每个升级决策的设备计数。

    3. Configuration Manager 为目标集合中的设备设置商业 ID、诊断数据级别和其他设置。 此配置指定要在桌面分析工作区中显示的设备。  

    4. 将兼容性更新部署到所有目标设备。  

3. 设备将诊断数据发送到适用于 Windows 的 Microsoft 诊断数据管理服务。 此服务托管于美国。  

4. Microsoft 每天都会生成一个以 IT 为中心的见解快照。 此快照合并了来自 Windows 的诊断数据与已注册设备的输入信息。 此过程发生在暂时存储中，仅供桌面分析使用。 暂时存储托管于美国的 Microsoft 数据中心。 所有数据都通过 SSL (HTTPS) 加密通道发送。 快照按商业 ID 进行隔离。  

5. 然后，快照会被复制到你的 Azure Log Analytics 工作区。 此数据传输在 HTTPS Webhook 引入协议下发生，这是 Log Analytics 的一项特性。 桌面分析对 Log Analytics 存储没有任何读取或写入权限。 桌面分析使用共享访问签名 (SAS) URI 调用 Webhook API。 然后 Log Analytics 通过 HTTPS 获取存储表中的数据。

6. 桌面分析将你的输入存储在 Log Analytics 存储中。 这些配置包括部署计划，以及升级和重要性的资产决策。  

## <a name="other-resources"></a>其他资源

有关桌面分析的隐私相关常见问题解答，请参阅[隐私常见问题解答](faq.md#privacy)。

相关隐私方面的详细信息，请参阅以下文章：

- [Windows 10 和 GDPR：面向 IT 决策者的信息](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [配置组织中的 Windows 诊断数据](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

- [Windows 7、Windows 8 和 Windows 8.1 评估程序诊断数据事件与字段](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields)。  

- [Windows 10 版本 1809 基本级别 Windows 诊断事件与字段](https://docs.microsoft.com/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)  

- [桌面分析所使用的 Windows 10 版本 1709 增强的诊断数据事件与字段](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  

- [诊断数据查看器概述](https://docs.microsoft.com/windows/privacy/diagnostic-data-viewer-overview)  

- [许可条款和文档](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  

- [Log Analytics 数据安全性](https://docs.microsoft.com/azure/azure-monitor/platform/data-security)

- [Microsoft Azure 数据中心的安全和隐私](https://azure.microsoft.com/global-infrastructure/)  

- [受信任云中的置信度](https://azure.microsoft.com/overview/trusted-cloud/)  

- [信任中心](https://www.microsoft.com/trustcenter)  

- [隐私保护协议](https://www.privacyshield.gov/)  

Configuration Manager 独立于桌面分析向 Microsoft 发送诊断和使用情况数据。 Microsoft 使用此数据改进 Configuration Manager 将来版本的安装体验、质量和安全性。 有关详细信息，请参阅 [Configuration Manager 的诊断和使用情况数据](../core/plan-design/diagnostics/diagnostics-and-usage-data.md)。
