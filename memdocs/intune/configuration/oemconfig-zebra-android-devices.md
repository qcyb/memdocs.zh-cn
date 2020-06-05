---
title: 使用 Microsoft Intune 将多个 OEMConfig 配置文件部署到 Zebra 设备 - Azure | Microsoft Docs
description: 使用 Microsoft Intune 在运行 Android Enterprise 的 Zebra 设备上创建和部署多个 OEMConfig 设备配置文件。 使用 Zebra 操作和步骤对配置文件进行排序。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: jieyan
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2227face347e6d82cf7807bea241eda4856c1d67
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988690"
---
# <a name="deploy-multiple-oemconfig-profiles-to-zebra-devices-in-microsoft-intune"></a>在 Microsoft Intune 中将多个 OEMConfig 配置文件部署到 Zebra 设备

在 Microsoft Intune 中，使用 OEMConfig 自定义适用于 Android Enterprise 设备的 OEM 特定设置。 这些设置特定于设备制造商，并使用 Intune 中的配置文件进行部署。

在 Zebra 设备上，可以将多个配置文件部署或分配给同一设备。 现有的 OEMConfig 配置文件可以在下次设备与 Intune 同步时使用此功能。

此功能适用于：

- 运行 Android Enterprise 的 Zebra 设备

若要了解有关 OEMConfig 的更多信息，包括它的功能和使用方法，请参阅 [OEMConfig 配置文件](android-oem-configuration-overview.md)。

本文介绍如何将 OEMConfig 多个配置文件部署到 Zebra 设备，并介绍如何在 Microsoft Intune 中排序以及使用报告功能。

## <a name="prerequisites"></a>必备条件

创建 [OEMConfig 配置文件](android-oem-configuration-overview.md)。

## <a name="use-multiple-profiles"></a>使用多个配置文件

在 Zebra 设备上，你可以同时在每个设备上拥有多个配置文件。 此功能允许你将 Zebra OEMConfig 设置拆分为更小的配置文件。 Zebra 的 OEMConfig 架构还使用“Actions”。 Actions 是在设备上运行的操作。 它们不会配置任何设置。 使用这些操作可以触发文件下载、清除剪贴板等。 有关支持的操作的完整列表，请参阅 [Zebra 的文档](https://techdocs.zebra.com/oemconfig/10-0/about/)（打开 Zebra 的网站）。

例如，创建一个 Zebra OEMConfig 配置文件，该配置文件将某些设置应用于设备。 另一个 Zebra OEMConfig 配置文件包含一个清除剪贴板的操作。 将第一个配置文件指定给 Zebra 设备组。 稍后，你需要清除这些设备上的剪贴板。 将第二个配置文件分配给同一个设备组，而不更改第一个配置文件。 清除设备剪贴板时，不会重新发送或影响在第一个配置文件中创建的配置设置。

在另一个示例中，你分配了一个 OEMConfig 配置文件，该配置文件配置了一些 Zebra 设备设置。 最近，用户报告特定应用程序出现问题，你想要清除该应用程序的缓存。 创建只包含“清除缓存”操作的新 OEMConfig 配置文件。 将配置文件分配给需要它的设备。

## <a name="ordering"></a>排序

如果每台设备上都有多个配置文件，则无法保证配置文件的部署顺序。 此行为属于 Google Play 限制。 若要按顺序运行操作，可以使用 [Zebra 的事务功能](https://techdocs.zebra.com/oemconfig/9-1/mc/)（打开 Zebra 的网站）。 让我们分析一个示例。

有两个配置文件：

- **配置文件 1**：打开蓝牙。 此配置文件将在星期一分配给“所有设备”组。
- **配置文件 2**：配置任何其他设置。 此配置文件将在星期二分配给“所有设备”组。

在配置其他设置之前，必须打开蓝牙。

星期三，你将使用 Intune 注册 10 台新的 Zebra 设备。 配置文件 1 和配置文件 2 均已分配给“所有设备”组。 新设备与 Intune 同步后，它们将接收配置文件。 这些设备可能会在配置文件 1 之前收到配置文件 2。

使用 Zebra 架构中的“步骤”功能确认操作按顺序运行。 在这种情况下，你将创建一个包含两个事务步骤的配置文件。 第一步包括蓝牙设置，第二步配置其他设置。 当 Zebra 的 OEMCong 应用接收到配置文件时，它会按顺序运行步骤，这一顺序由 Zebra 保证。

有关详细信息，请参阅 [Zebra 的事务步骤](https://techdocs.zebra.com/oemconfig/9-1/mc/)（打开 Zebra 的网站）。

## <a name="enhanced-reporting"></a>增强型报告

部署配置文件后，它由设备上的 Zebra OEMConfig 应用执行。 Zebra OEMConfig 应用会向 Intune 报告配置文件状态。 在 Endpoint Manager 管理中心中，你可以看到已部署的 OEMConfig 配置文件的状态，以及任何错误或警告。

1. 打开 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择 Zebra OEMConfig 配置文件 >“监视器” > “设备状态” 。 此选项显示已分配 OEMConfig 配置文件的设备。
3. 选择设备 >“设备配置”> 选择 Zebra OEMConfig 配置文件。 此选项显示成功或失败的配置文件设置。

    选择失败的行。 随即显示有关失败原因的详细信息。

## <a name="next-steps"></a>后续步骤

- 详细了解 [OEMConfig 配置文件](android-oem-configuration-overview.md)。
- 使用 Android 设备管理员身份配置 [Mobility Extensions (MX)](android-zebra-mx-overview.md)。
- [监视配置文件状态](device-profile-monitor.md)。
