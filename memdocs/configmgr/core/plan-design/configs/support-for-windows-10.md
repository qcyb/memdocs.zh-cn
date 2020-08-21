---
title: 支持 Windows 10
titleSuffix: Configuration Manager
description: 了解支持作为客户端或 OSD 对 Configuration Manager 使用的 Windows 10 版本
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 6a30fc55fb4129b8ea3493b76fd6871a2a62f881
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126733"
---
# <a name="support-for-windows-10-in-configuration-manager"></a>Configuration Manager 支持使用 Windows 10  

适用范围：Configuration Manager (Current Branch)

了解 Configuration Manager 支持的 Windows 10 版本，包括：

- [作为 Configuration Manager 客户端的 Windows 10](#windows-10-as-a-client)
- [适用于 Windows 10 的 Windows 评估和部署工具包 (ADK)](#windows-10-adk)

> [!TIP]
> 如同支持 Windows 10 版本一样支持作为客户端的 Windows Server 内部版本。 例如，Windows Server 2016 是与 Windows 10 LTSB 2016 相同的内部版本，Windows Server 版本 1803 是与 Windows 10 版本 1803 相同的内部版本。
>
> 有关作为站点系统的 Windows Server 的详细信息，请参阅 [Configuration Manager 站点系统服务器支持的操作系统](supported-operating-systems-for-site-system-servers.md#bkmk_core)。

## <a name="windows-10-as-a-client"></a>作为客户端的 Windows 10

在每个 Windows 10 新版本发布后，Configuration Manager 会尽快提供支持，允许将新版本用于客户端。 由于产品有单独的开发和发布计划，因此 Configuration Manager 提供的支持取决于每个产品的发布时间。

Configuration Manager 版本将在[对该版本的支持](../../servers/manage/current-branch-versions-supported.md)结束后从列表中删除。 同样，对 Enterprise 2015 LTSB 或 1511 等 Windows 10 版本的支持也将在它们不受支持时从列表中删除。

- Configuration Manager Current Branch 的最新版本会接收安全更新和关键更新，其中可能包括 Windows 10 版本中问题的修补程序。 当 Microsoft 发布新版本的 Configuration Manager Current Branch 时，以前的版本将仅接收安全更新。 有关详细信息，请参阅[对 Configuration Manager Current Branch 版本的支持](../../servers/manage/current-branch-versions-supported.md)。  

    > [!NOTE]
    > 使 Windows 10 保持最新的最佳方式是随时关注 Configuration Manager 的最新动态。 有关详细信息，请参阅 [Configuration Manager 和 Windows 即服务](../../understand/configuration-manager-and-windows-as-service.md)。  

- 此信息补充了[客户端和设备支持的操作系统](supported-operating-systems-for-clients-and-devices.md)。  

- 如果使用 Configuration Manager 的 Long-Term Servicing Branch，请参阅 [Long-Term Servicing Branch 的支持配置](../../understand/supported-configurations-for-ltsb.md)。  

下表列出了 Windows 10 的版本，这些版本可用作具有不同 Configuration Manager 版本的客户端。

| Windows 10 版本 | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 | ConfigMgr 2006 |
|---------------------|-----|-----|-----|-----|-----|-----|
| **1709**<br>(10.0.16299)   <!--10/13/2020-->   | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |
| **1803**<br>(10.0.17134)   <!--11/10/2020-->   | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |
| **1809**<br>(10.0.17763)   <!--05/11/2021-->   | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |
| **1903**<br>(10.0.18362)   <!--12/08/2020-->   | ![不支持](media/Red_X.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |
| **1909**<br>(10.0.18363)   <!--05/10/2022-->   | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |
| 2004<br>(10.0.19041)   <!--12/14/2021-->   | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |

当前支持的所有 Configuration Manager Current Branch 版本都支持以下 Windows 10 LTSB/LTSC 版本：

- **Enterprise 2015 LTSB** <!--10/14/2025-->
- **Enterprise 2016 LTSB** <!--10/13/2026-->
- **Enterprise LTSC 2019** <!--01/09/2029-->

若要详细了解 Windows 生命周期，请参阅 [Windows 生命周期情况说明书](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)。

| Key |
|--|
| ![支持](media/green_check.png) = **支持**  |
| ![不支持](media/Red_X.png) = **不支持** |

### <a name="windows-10-client-support-notes"></a><a name="bkmk_win10-notes"></a> Windows 10 客户端支持说明

- 支持 Windows 10 半年频道版本的版本包括：企业版、专业版、教育版和专业教育版。  

- 从版本 1906 开始，Configuration Manager 支持适用于工作站的 Windows 10 Pro。

- 对于 Windows 10 版本 1909，操作系统部署媒体显示版本为 10.0.18362.418。

### <a name="windows-10-on-arm64"></a><a name="bkmk_arm64"></a> ARM64 上的 Windows 10

Configuration Manager 在 Windows 10 ARM64 设备上支持客户端。 不支持 OS 部署。<!-- 1353704 -->

从版本 2002 开始，<!--5954175--> 可在具有要求规则或适用性列表的对象上的受支持 OS 版本列表中找到“所有 Windows 10 (ARM64)”平台。

> [!NOTE]
> 如果之前选择了顶层 Windows 10 平台，则此操作会自动选择“所有 Windows 10 (64 位)”和“所有 Windows 10 (32 位)”  。 不会自动选择此新平台。 如果要添加“所有 Windows 10 (ARM64)”，请在列表中手动选择它。

### <a name="support-for-windows-insider"></a><a name="bkmk_WIfB-support"></a> 支持 Windows 预览体验成员

从 Configuration Manager 版本 1906 开始，可以[更新和维护 Windows 预览体验成员](../../../sum/get-started/configure-classifications-and-products.md#bkmk_WIfB)版本。 此功能旨在为客户提供便利。 在此功能工作期间，对它的支持是最佳支持。 若此功能停止工作，Configuration Manager 无法提供它的修补程序。  

若要提供 Windows 预览体验人员的反馈，请使用[反馈中心](https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-feedback)。

## <a name="windows-10-adk"></a>Windows 10 ADK

使用 Configuration Manager 部署操作系统时，Windows ADK 是必需的外部依赖项。 有关详细信息，请参阅下列文章：

- [OS 部署的基础架构要求](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10)

- [下载适用于 Windows 10 的 Windows ADK](https://docs.microsoft.com/windows-hardware/get-started/adk-install)

    > [!IMPORTANT]
    > 从 Windows 10 版本 1809 开始，Windows PE 是单独的安装程序。 但是功能上没有任何区别。
    >
    > 确保同时下载适用于 Windows 10 的 Windows ADK 和适用于 ADK 的 Windows PE 加载项。

下表列出了可用于不同版本 Configuration Manager 的 Windows 10 ADK 的版本。

| Windows 10 ADK 版本  | ConfigMgr 1810 | ConfigMgr 1902 | ConfigMgr 1906 | ConfigMgr 1910 | ConfigMgr 2002 | ConfigMgr 2006 |
|--------------------|-----|-----|-----|-----|-----|-----|
| **1709**<br>(10.1.16299) | ![不支持](media/Red_X.png)   | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) |
| **1803**<br>(10.1.17134) | ![后向兼容](media/blue_compat.png) | ![后向兼容](media/blue_compat.png) | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) |
| **1809**<br>(10.1.17763) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![后向兼容](media/blue_compat.png) | ![后向兼容](media/blue_compat.png) | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) |
| **1903**<br>(10.1.18362) | ![不支持](media/Red_X.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) | ![后向兼容](media/blue_compat.png) |
| 2004<br>(10.1.19041) | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) | ![不支持](media/Red_X.png) | ![支持](media/green_check.png) | ![支持](media/green_check.png) |

|Key|
|--|
| ![支持](media/green_check.png) = **支持** <br/> 此表仅显示与 Configuration Manager 版本相关的 Windows ADK 可支持性。 Microsoft 建议使用与要部署的 Windows 版本匹配的 Windows ADK。 部署最新的 Windows 10 版本时，请使用最新的 Windows ADK 版本。 最新的 Windows ADK 版本可能支持部署较低的 OS 版本，如 Windows 8.1。<!-- SCCMDocs issue 1229 --> 有关 Windows ADK 组件支持能力的详细信息，请参阅 [DISM supported platforms](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms)（DISM 支持的平台）和 [USMT requirements](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1)（USMT 要求）。 |
| ![Backwards compatible](media/blue_compat.png)  = 后向兼容 <br/> 此组合未经测试，但应该适用。 我们会记录任何已知问题或注意事项。 |
| ![不支持](media/Red_X.png) = **不支持** |

### <a name="windows-10-adk-support-notes"></a><a name="bkmk_adk-notes"></a> Windows 10 ADK 支持说明

- Configuration Manager 仅支持 Windows 10 ADK 的 x86 和 amd64 组件。 当前不支持 ARM 或 ARM64 组件。

- Windows Server 内部版本具有与关联的 Windows 10 版本相同的 Windows ADK 需求。 例如，Windows Server 2016 的生成版本与 Windows 10 LTSB 2016 相同。
