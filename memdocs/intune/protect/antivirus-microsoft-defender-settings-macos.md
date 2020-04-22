---
title: Intune 中 Microsoft Defender 防病毒的 macOS 防病毒策略设置| Microsoft Docs
description: 参阅适用于 macOS 的 Microsoft Defender 防病毒配置文件中的设置列表。 此配置文件是 Microsoft Intune 中适用于 macOS 的终结点安全防病毒策略的一部分。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: samyada
ms.openlocfilehash: 9a0687b9e3938c93cfaebe0e064fd994077a92af
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "80086684"
---
# <a name="settings-for-microsoft-defender-atp-for-mac-in-microsoft-intune"></a>Microsoft Intune 中适用于 Mac 的 Microsoft Defender ATP 的设置

查看可以在 Microsoft Intune 中为适用于 Mac 的 Microsoft Defender ATP 的防病毒配置文件设置  。 有关这些设置的详细信息，请参阅 Windows 文档中的[适用于 Mac 的 Microsoft Defender 高级威胁防护](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac)。

**Microsoft Defender ATP**

- **实时保护**  
  需要 macOS 设备上的 Defender，才能使用实时监视功能。 实时监视可查找恶意软件并阻止其在设备上安装或运行。 可以短时间先关闭此设置，然后它会自动重新启用。

  - **未配置**（默认值）  - 设置将还原为系统默认值
  - **已启用** - 强制使用实时监视。 设备用户无法更改此设置。
  - **已禁用** - 设置已禁用。 设备用户无法更改此设置。

- **云提供的保护**  
  默认情况下，Defender 将有关发现的任何问题的信息发送给 Microsoft。 Microsoft 分析该信息，详细了解影响你和其他客户的问题，并提供改进的解决方案。 将“自动示例提交”  设置为“开”时，保护效果最佳。

  - **未配置**（默认值）  - 设置将还原为系统默认值。
  - **已启用** - 已启用云提供的保护。 设备用户无法更改此设置。
  - **已禁用** - 设置已禁用。 设备用户无法更改此设置。

- **自动示例提交**  
  向 Microsoft 发送示例文件，帮助保护设备用户和组织免受潜在威胁。

  - **未配置**（默认值）  - 设置将还原为系统默认值。
  - **已启用** - 已启用云提供的保护。  设备用户无法更改此设置。
  - **已禁用** - 设置已禁用。 设备用户无法更改此设置。

- **诊断数据收集**

  配置与 Microsoft 共享诊断和使用情况数据的方式。

  - **未配置**（默认值）  - 设置将还原为系统默认值。
  - **必需**
  - **可选**

- **排除在扫描范围之外的文件夹**  
  选择“添加”  ，然后指定要在扫描过程中忽略的文件夹。

- **排除在扫描范围之外的文件**  
  选择“添加”  ，然后指定要在扫描过程中忽略的文件。

- **排除在扫描范围之外的文件类型**  
  选择“添加”  ，然后指定要在扫描过程中忽略的文件扩展。

- **排除在扫描范围之外的进程**  
  选择“添加”  ，然后指定要在扫描过程中忽略的进程。
