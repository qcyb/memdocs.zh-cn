---
author: brenduns
ms.author: brenduns
ms.service: microsoft-intune
ms.subservice: protect
ms.topic: include
ms.date: 08/24/2020
ms.openlocfilehash: ff48e8117437e45be42551ebffff7cdcf5bce184
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820285"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
使用 Configuration Manager Current Branch 2006 或更高版本通过租户附加方案管理的设备支持以下配置文件：
<!--The following profiles are supported for devices you manage with Configuration Manager Technical Preview 2007 or later, through the tenant attach scenario:-->

- 平台：**Windows 10 和 Windows Server**

  - 配置文件：**Microsoft Defender 防病毒策略 (ConfigMgr)**
  
    使用租户附加时，管理 [Configuration Manager 设备的防病毒策略设置](../../protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md)。

    此配置文件支持附加租户和运行以下平台的设备：
    - Windows 10 及更高版本(x86, x64, ARM64)
    - Windows 8.1 (x84, x64)
    - Windows Server 2019 及更高版本 (x64)
    - Windows server 2016 (x64)
    - Windows Server 2012 R2 (x64)
    - Windows Server 2008 R2 SP1 (x64)
