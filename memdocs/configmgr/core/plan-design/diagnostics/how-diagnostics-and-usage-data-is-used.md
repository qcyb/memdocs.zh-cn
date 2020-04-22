---
title: 使用诊断数据
titleSuffix: Configuration Manager
description: 了解 Microsoft 如何使用 Configuration Manager 收集的诊断和使用情况数据。
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6a014d60c49b0ff7e10cd74c101294dd002266d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697125"
---
# <a name="how-microsoft-uses-configuration-manager-diagnostics-and-usage-data"></a>Microsoft 如何使用 Configuration Manager 诊断和使用情况数据

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 收集的诊断和使用数据为 Microsoft 提供有关产品使用情况的近乎即时的反馈，并可用于调整将来的更新。 Microsoft 还可以查看配置数据，这些数据可帮助他们设计并测试生产中使用的配置。 例如：

- 站点服务器上使用的 Windows Server 版本

- 已安装的语言包

- SQL 架构针对产品默认值的增量

此数据帮助工程团队计划将来的测试，以确保通过最常见的配置获得最佳体验。 此数据对于快速调整和适应频繁的发布周期至关重要。

同样重要的一点是，了解诊断和使用数据不适用于哪些方面。 Microsoft 不会将此数据用于以下方面：

- 许可审核，例如按照许可协议比较客户使用情况

- 不支持的产品的审核

- 基于功能使用情况或地理位置（时区）等可用数据进行广告宣传

Microsoft 使用可用数据来改进产品。 例如：

- Configuration Manager Current Branch 提供的初始支持对 Windows Server 2008 R2 的支持时间线加以限制。 Microsoft 检查了已升级到 Configuration Manager 当前分支的客户的使用情况数据， 然后确定需要修改并延长此时间线，以支持仍使用此 OS 的客户。

- Microsoft 改进了安装更新的先决条件检查。 删除了过时的规则，考虑到其他情况并自动修复了一些问题。  

> [!div class="nextstepaction"]
> [Configuration Manager 如何收集数据](how-diagnostics-and-usage-data-is-collected.md)
