---
title: Microsoft Endpoint Configuration Manager 常见问题解答
titleSuffix: Configuration Manager
description: 关于 Microsoft Endpoint Configuration Manager 的常见问题解答
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: be276b34-e283-4386-8b45-5629e431c50d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e0b59ffa73bb2c7524f2eed29326f238d856adef
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699307"
---
# <a name="microsoft-endpoint-configuration-manager-faq"></a>Microsoft Endpoint Configuration Manager 常见问题解答

适用范围：  Configuration Manager（Current Branch、技术预览版分支）

从版本 1910 开始，Configuration Manager 现在是 Microsoft Endpoint Manager 的一部分。 本文提供常见问题的解答。

## <a name="summary"></a>“摘要”

首先观看以下 Microsoft 365 公司副总裁 Brad Anderson 发布的两分钟视频：

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## <a name="faqs"></a>常见问题解答

### <a name="what-is-microsoft-endpoint-manager"></a>什么是 Microsoft Endpoint Manager？

Microsoft Endpoint Manager 是用于管理所有设备的集成解决方案。 只通过简化授权 Microsoft 就可以将 Configuration Manager 和 Intune 组合在一起。 继续利用现有的 Configuration Manager 投资，同时按照自己的进度获取 Microsoft 云的优势。

以下 Microsoft 管理解决方案现已成为 Microsoft Endpoint Manager  品牌的一部分：

- [Configuration Manager](/configmgr)
- [Intune](/intune)
- [桌面分析](../../desktop-analytics/overview.md)
- [Autopilot](/intune/enrollment/enrollment-autopilot)
- [设备管理管理员控制台](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760)中的其他功能

有关详细信息，请参阅以下 Microsoft 公司副总裁 Brad Anderson 发布的关于 Microsoft 365 的帖子：

- [公告博客文章](https://aka.ms/cmannounce)
- [远见报告](https://aka.ms/MEMVisionPaper)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>使用 Microsoft Endpoint Manager 在 Configuration Manager 中有什么变化？

在版本 1910 中，除了名称更改之外，Configuration Manager 的功能仍然相同。

最值得注意的是，常用组件的“开始”菜单文件夹名已更改，例如 [Configuration Manager 控制台](../servers/manage/admin-console.md#bkmk_open)和[软件中心](software-center.md#bkmk_open)。

### <a name="how-do-we-refer-to-the-product-now"></a>现在我们是如何引用产品的呢？

- 引用包含所有组件的整个解决方案时：**Microsoft Endpoint Manager**

- 引用本地组件时：
  - 第一次引用时，请使用完整品牌名称：**Microsoft Endpoint Configuration Manager**
  - 对于常规用途：**Configuration Manager**
  - 对于空间受限用途：**ConfigMgr**，仅在常规用途名称不适合的情况下

### <a name="are-there-any-licensing-changes"></a>是否有任何许可更改？

可以！ 正如 Microsoft Ignite 2019 中所述，如果你获得了 Configuration Manager 的许可，那么你现在也获得了 Intune 的许可，可以[共同管理](../../comanage/overview.md) Windows 电脑。 有关详细信息，请参阅[产品和许可常见问题解答](product-and-licensing-faq.md#bkmk_mem)。

### <a name="why-do-i-still-see-system-center-configuration-manager-some-places"></a>为什么某些地方仍然看到“System Center Configuration Manager”？

在所有产品、服务和支持材料（如文档）中进行更改需要时间。

还有一些基本组件可能永远不会改变。 站点服务器上的主 Windows 服务仍是“SMS_Executive”  。 支持此文档的 GitHub 存储库仍是“SCCMDocs”  。

## <a name="next-steps"></a>后续步骤

了解有关 [Configuration Manager 增量版本中的新增功能](../plan-design/changes/whats-new-incremental-versions.md)的详细信息。