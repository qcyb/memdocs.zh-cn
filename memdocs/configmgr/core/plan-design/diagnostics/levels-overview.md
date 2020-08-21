---
title: 诊断使用情况数据的级别
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 收集的诊断和使用情况数据的级别
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 3c46bdb2-5bda-47c8-b5f4-9365a4b3521c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0d27e4a2f82de75cde853f3ce95c98ea8a12c465
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126498"
---
# <a name="levels-of-diagnostic-usage-data"></a>诊断使用情况数据的级别

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 收集三个级别的诊断和使用情况数据：“基本”、“增强”和“完全”    。 默认情况下，此功能设置为增强级别。

> [!IMPORTANT]
> Configuration Manager 不会在基本或增强级别收集站点代码、站点名称、IP 地址、用户名、计算机名、物理地址或电子邮件地址。 在“完全”级别收集这类信息并无目的性。 它可能包含在日志文件或内存快照等高级诊断信息中。 Microsoft 不会使用这些信息来识别你的身份、与你联系或进行广告宣传。

## <a name="levels"></a>级别

### <a name="basic"></a>基本

“基本”级别包括有关层次结构的数据。 它有助于改善安装或升级体验。 此数据还有助于确定适用于层次结构的 Configuration Manager 更新。

### <a name="enhanced"></a>已增强

安装完成后，默认级别为增强级别。 此级别包括在基本级别和特定于功能的数据中收集的数据。 它显示了不同功能的使用频率和持续时间。 还包括 Configuration Manager 客户端设置数据：组件名称、状态和某些设置（如轮询间隔）。 有关软件更新的信息是有关功能使用情况的基本信息，此级别不包括有关更新合规性的数据。

Microsoft 建议使用此级别，因为它提供了最少的数据来改进产品和服务。

此级别不收集的一些数据示例包括：

- 站点、用户、计算机或其他对象的名称

- 与安全性相关的对象的详细信息

- 需要软件更新的系统计数等漏洞

### <a name="full"></a>完整

完全级别包括基本和增强级别的所有数据。 它还包括有关 Endpoint Protection、更新符合性百分比和软件更新信息的其他信息。 此级别还可以包括高级诊断信息，如系统文件和内存快照。 此高级数据可能包括捕获时存储在内存或日志文件中的个人信息。

## <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> 如何更改级别

要更改数据收集级别，需要修改站点对象类的权限   。

1. 在 Configuration Manager 控制台中，转到“管理”  工作区，展开“站点配置”  ，然后选择“站点”  节点。
1. 选择功能区中的“层次结构设置”  。
1. 切换到“诊断和使用情况数据”  选项卡，然后选择数据级别。

## <a name="version-specific-details"></a><a name="bkmk_versions"></a> 指定版本的详细信息

以下文章详细介绍了每个受支持版本的 Configuration Manager 在每个级别上收集的特定数据：

- [版本 2006 收集的诊断和使用情况数据](levels-of-diagnostic-usage-data-collection-2006.md)
- [2002 的诊断和使用情况数据](levels-of-diagnostic-usage-data-collection-2002.md)
- [1910 的诊断和使用情况数据](levels-of-diagnostic-usage-data-collection-1910.md)
- [1906 的诊断和使用情况数据](levels-of-diagnostic-usage-data-collection-1906.md)
- [1902 的诊断和使用情况数据](levels-of-diagnostic-usage-data-collection-1902.md)

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [常见问题解答](frequently-asked-questions.md)
