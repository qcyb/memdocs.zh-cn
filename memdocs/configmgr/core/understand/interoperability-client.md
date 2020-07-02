---
title: 扩展互操作性客户端
titleSuffix: Configuration Manager
description: 了解如何使用扩展互操作性客户端为具有 Current Branch 站点的静态 Configuration Manager 客户端提供长期支持。
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 78e89307e66107b259d818a84fa4dbca878a843c
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590892"
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>使用 Configuration Manager 客户端软件，实现与未来 Current Branch 站点版本的扩展互操作性

适用范围：Configuration Manager (Current Branch)  

业务要求可能不允许定期更新某些设备上的 Configuration Manager 客户端。 例如，需要遵循变更管理策略，或设备属于任务关键型。 可通过安装一个长期使用的新客户端来满足这些需求，这一客户端称为扩展互操作性客户端 (EIC)。 EIC 应仅用于无法经常更新的特定设备，如展台或销售点设备。 继续对大多数客户端使用[自动客户端升级](../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)。

## <a name="how-it-works"></a>工作原理

通常，为 Configuration Manager 安装新的[控制台中更新](../servers/manage/install-in-console-updates.md)时，客户端会自动更新其客户端软件以使用这些新功能。 在此方案中，仍可更新到 Current Branch 并接收新功能和更新。 大多数设备会通过你安装的每个版本更新来更新 Configuration Manager 客户端软件。 但在不想接收客户端软件更新的关键系统子集上，安装扩展互操作性客户端。 在显式部署新版客户端软件之前，此类客户端不会安装新的客户端软件。

## <a name="supported-versions"></a>支持的版本

下表列出了此方案支持的 Configuration Manager 客户端版本：

| 版本 | 可用日期 | 支持结束日期 |
|---------|---------|---------|
| 1902<br/>5.00.8790 | 2019 年 3 月 27 日 | 不早于 2021 年 3 月 27 日 |
| 1802<br/>5.00.8634 | 2018 年 5 月 1 日 | 不早于 2020 年 5 月 1 日 |
| 1606<br/>5.00.8412 | 2016 年 11 月 18 日 | 2019 年 5 月 1 日 |

> [!TIP]  
> 从发布之日起，EIC 至少在两年内受支持。 有关发布日期的详细信息，请参阅[对 Configuration Manager Current Branch 版本的支持](../servers/manage/current-branch-versions-supported.md)。  

计划在客户端的支持到期之前，在使用 Current Branch 管理的设备上更新扩展互操作性客户端。 为此，请从 Microsoft 下载新版客户端，然后在使用当前扩展互操作性客户端的设备上，部署更新后的客户端软件。

## <a name="how-to-use-the-eic"></a>如何使用 EIC

1. 将这些设备添加到一个集合，从自动客户端升级中排除该集合。 有关详细信息，请参阅[如何从升级中排除客户端](../clients/manage/upgrade/exclude-clients-windows.md)。  

1. 从 Configuration Manager 更新安装介质的 `\SMSSETUP\Client` 文件夹中获取受支持的 EIC 版本。 请务必复制文件夹的全部内容。  

<!--
    > [!TIP]
    > To find Configuration Manager media in the [Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC), go to the **Downloads and Keys** tab, and search for **Microsoft Endpoint Configmgr (current branch)**.
-->

1. 在这些设备上手动安装 EIC。 有关详细信息，请参阅[手动安装客户端](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual)。  

    > [!Important]  
    > 将版本 1606 客户端升级到版本 1802 时，请使用 CCMSETUP 选项“/AlwaysExcludeUpgrade:True”。 否则，客户端可能从管理点接收策略，以在排除策略之前自动升级。  

## <a name="limitations"></a>限制

- 扩展互操作性客户端软件的更新不可通过控制台内更新进行。 有关如何升级 EIC 的详细信息，请参阅[如何升级排除的客户端](../clients/manage/upgrade/exclude-clients-windows.md#bkmk_override)。  

- EIC 仅支持以下功能：  

  - 软件更新  
  - 硬件和软件清单
  - 包和程序

## <a name="next-steps"></a>后续步骤

[如何从升级中排除客户端](../clients/manage/upgrade/exclude-clients-windows.md)

为确保客户端已正确安装到所需设备上，请参阅[如何监视客户端](../clients/manage/monitor-clients.md)。
