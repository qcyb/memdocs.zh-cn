---
title: UUP 预览版
titleSuffix: Configuration Manager
description: 有关 UUP 集成预览版的说明
ms.date: 11/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: f06955ac-70ed-424d-a3e7-6b80ff2e114f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3871b51c85d0474c4bea2da24fc5a2f31d02f59f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81702935"
---
# <a name="uup-private-preview-instructions"></a>UUP 个人预览版说明

> [!Note]  
> 该信息涉及预览功能，该预览功能可能会在其商业发行之前进行大幅度修改。 对于此处提供的信息，Microsoft 不提供任何明示或暗示的担保。  

## <a name="introduction"></a>简介

统一更新平台 (UUP) 是一个打包和发布平台，消费者和企业设备使用该平台接收来自适用于企业的 Windows 更新的更新。 UUP 个人预览计划面向以下客户：同意帮助 Microsoft 验证 Configuration Manager 中 UUP 更新的使用效果，旨在帮助解决客户目前使用维护窗口所报告的问题。 这些更新当前不公开提供。

有关 UUP 的详细信息，请参阅以下 Windows 博客文章：[统一更新平台 (UUP) 上的更新](https://blogs.windows.com/windowsexperience/2017/03/02/an-update-on-our-unified-update-platform-uup/)。

## <a name="benefits"></a>好处

Windows 10 UUP 功能和积累更新有助于解决客户目前通过维护窗口报告的多个问题。

### <a name="feature-updates"></a>功能更新

- 使用 UUP 功能更新，Windows 更新过程将保留按需功能 (FOD) 和语言包。

- 直接更新到最新的安全符合性级别。 功能更新后，无需立即安装安全更新。 Microsoft 每月发布一个新功能更新，以及最新的累积安全更新。 无需每月下载或分发大部分功能更新内容。 你只下载安全更新，UUP 与累积更新共享该更新。

### <a name="cumulative-updates"></a>累积更新

- UUP 累积更新包括含每月累积安全更新的服务堆栈更新 (SSU)。 这样可解决协调这两种更新的难题。 它确保服务堆栈更新已到位，已可安装累积更新。 无需管理和协调这些关系。

- UUP 的累积更新允许离线分发 FOD 和语言包内容。 此行为使用户能够按需添加它们。 用户不需要从 Internet 下载，也不需要了解如何预安排此内容。

## <a name="set-up"></a>开始参与

### <a name="1-send-your-wsus-id-to-microsoft"></a>1.将 WSUS ID 发送给 Microsoft

若要加入 UUP 个人预览计划，请与 UUP 预览联系人共享 WSUS ID。 Microsoft 批准 WSUS 环境加入 UUP 预览计划。 若没有此 ID，在预览版发布之前，你无法看到任何 UUP 更新。

运行以下 PowerShell 脚本以获取 WSUS ID：

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId

# also check MUUrl
$config.MUUrl
```

MUUrl 属性应为 `https://sws.update.microsoft.com` 。 若要更改它，请参阅以下支持文章中的解决办法：[WSUS 同步失败，出现 SoapException](https://support.microsoft.com/help/4482416/wsus-synchronization-fails-with-soapexception)。

### <a name="2-update-configuration-manager"></a>2.更新 Configuration Manager

对 Configuration Manager 站点进行以下更改，以支持此 UUP 预览版：

#### <a name="diagnostics-and-usage-data-level"></a>诊断和使用情况数据级别

请考虑在此预览期间提高 Configuration Manager 诊断和数据使用情况级别。 “完整”级别可帮助 Microsoft 更好地分析和排查此新功能的问题  。 有关详细信息，请参阅 [1906 版的诊断使用情况数据收集的级别](../../core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1906.md)。

#### <a name="install-the-latest-update"></a>安装最新更新

1. 使用以下更新之一更新站点：

    - 版本 1902 提供[更新汇总](https://support.microsoft.com/help/4500571)
    - [版本 1906](../../core/servers/manage/checklist-for-installing-update-1906.md)

    有关详细信息，请参阅[安装控制台内部更新](../../core/servers/manage/install-in-console-updates.md)。

2. 更新客户端。  

    - 若要简化此过程，请考虑使用自动客户端升级。 有关详细信息，请参阅[升级客户端](../../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)。  

    - 若要防止不必要地将大约 6 GB 的未使用内容下载到客户端  ，请更新所有针对 UUP 更新的客户端。

### <a name="3-update-windows-clients-to-a-supported-version"></a>3.将 Windows 客户端更新为支持的版本

若要成功安装 UUP 更新，请安装以下两个更新：

1. 特定的最小累积每月符合性级别。

2. 来自 Microsoft 更新目录的特定非累积、非安全性更新。 若要将更新导入 Configuration Manager 以进行部署，请参阅[从 Microsoft 更新目录导入更新](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog)。

#### <a name="supported-versions-of-windows-10-and-required-updates"></a>支持的 Windows 10 版本和所需更新

| Windows 10 版本 | 最低符合性级别 | 其他目录更新 |
| ------------------ | ------------------------ | ------------------ |
| **Windows 10 版本 1903** | RTM | 2019 年 11 月 7 日，[KB4529943](https://www.catalog.update.microsoft.com/search.aspx?q=4529943) |
| **Windows 10 版本 1809** | 2019 年 8 月，[KB4511553](https://support.microsoft.com/help/4511553/windows-10-update-kb4511553) | 2019 年 11 月 7 日，[KB4514987](https://www.catalog.update.microsoft.com/search.aspx?q=4514987) |
| **Windows 10 版本 1803** | 2019 年 4 月，[KB4493464](https://support.microsoft.com/help/4493464/windows-10-update-kb4493464) | 2019 年 11 月 7 日，[KB4512745](https://www.catalog.update.microsoft.com/search.aspx?q=4512745) |
| **Windows 10 版本 1709** | 2019 年 4 月，[KB4493441](https://support.microsoft.com/help/4493441/windows-10-update-kb4493441) | 2019 年 11 月 7 日，[KB4512744](https://www.catalog.update.microsoft.com/search.aspx?q=4512744) |

> [!IMPORTANT]
> - 如果在应用 2019 年 11 月 7 日的其他目录更新之前将 2019 年 11 月 12 日更新应用于客户端，则支持 UUP 所需的 Windows 更新代理更改将被覆盖。 若要修复此方案中的客户端，请在安装 2019 年 11 月 12 日更新后应用其他目录更新。
> - 如果向客户端应用功能更新，则需要在升级完成后重新安装其他目录更新。
> - 为了更轻松地测试功能更新，请将更新导入 Configuration Manager。 有关详细信息，请参阅[从 Microsoft 更新目录导入更新](../get-started/synchronize-software-updates.md#import-updates-from-the-microsoft-update-catalog)。 功能更新完成后，其他目录更新将显示为“必需”，这允许自动部署到高级 OS 版本  。

### <a name="4-allow-clients-to-download-delta-content-when-available"></a>4.在有可用内容时，允许客户端下载增量内容

若要正确下载 UUP 更新，请启用客户端设置“在有可用内容时，允许客户端下载增量内容”  。 通过此设置，Configuration Manager 能够让 Windows 更新代理 (WUA) 确定要下载到客户端的必要内容。 此行为会取代默认行为，即 Configuration Manager 客户端下载与 UUP 更新有关的所有内容。 启用此设置后，WUA 会确定每个 UUP 更新所必需的其他内容。 例如，仅必需的 FOD 和语言包。

启用此设置时，它不会影响从 Internet 下载服务器内容。 这仅适用于客户端下载。 将 UUP 更新部署到客户端之前，请将此设置应用于具有 UUP 支持的版本的客户端。 该必备的客户端更新修复了 WSUS 和 Configuration Manager 中 UUP 更新的兼容性问题。

有关此客户端设置的详细信息，请参阅[关于客户端设置 - 软件更新](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available)

### <a name="5-review-your-software-update-infrastructure"></a>5.查看软件更新基础结构

在同步 UUP 更新之前，请查看自动部署规则 (ADR) 和维护服务计划。 如果不希望这些更新自动部署，请修改 ADR，将其筛选掉。有关详细信息，请参阅[如何查找同步 UUP 更新](#how-to-find-synced-uup-updates)。 默认情况下，现有维护服务计划仅部署非 UUP 更新。 可以修改维护服务计划来更改此行为。

查看合规报告并根据需要进行修改。 例如，如果现在评估所有产品的符合性，会同时看到 UUP 和非 UUP 累积更新。 设备会同时针对两种类型的更新来提供符合性报告。 确保合规报告反映出此更改。

## <a name="enable-uup-and-start-testing"></a>启用 UUP 并开始测试

### <a name="select-products-and-classifications-to-sync"></a>选择要同步的产品和分类

准备好开始同步 UUP 更新且 Microsoft 已批准 WSUS ID 后，便可启用新产品：

1. [同步软件更新](../get-started/synchronize-software-updates.md)以填充新产品。  

2. 在 Configuration Manager 控制台中，转到“管理”  工作区，展开“站点配置”  ，然后选择“站点”  节点。

3. 选择顶层站点，它是管理中心站点 (CAS) 或独立主站点。

4. 在功能区中，选择“配置站点组件”，然后选择“软件更新点”   。

5. 切换到“产品”选项卡，然后选择以下一个或多个产品  ： 

    - **Windows 10 UUP 预览版**
    - **Windows Server UUP 预览版**

6. 切换到“分类”选项卡，然后选择以下选项  ：  

    - **安全更新**：查看 UUP 累积更新  
    - **升级**：查看 UUP 功能更新  

7. 再次同步软件更新以查看新的 UUP 更新。

### <a name="how-to-find-synced-uup-updates"></a>如何查找同步的 UUP 更新

将 UUP 更新同步到环境中后，请在 Configuration Manager console 控制台中找到它们进行测试。 有两种方法查找预览更新：

- 由于这些预览版更新位于不同的产品中，因此请使用该产品筛选以查找这些更新。 使用维护服务计划的产品筛选器部署 UUP 或非 UUP 功能更新。  

- 在软件库的“所有软件更新”和“所有 Windows 10 更新”节点中，都有一个新的可选列，即“标记”     。 此属性也可作为 ADR 中的筛选器提供。 对于 UUP 更新，在此字段中搜索 `UUP`。 对于非 UUP 更新为空。  

### <a name="updates-available-during-preview"></a>在预览期间可用的更新

有关 Microsoft 发布的所有 Windows 10 更新的详细信息，请参阅 [ Windows 10 发布信息](https://docs.microsoft.com/windows/release-information/)。

#### <a name="cumulative-updates-to-test"></a>要测试的累积更新

尽管可能会有多个标记了 UUP 的可用更新，但请使用版本不早于 2019 年 9 月 (2019-09) 的更新  。 例如：

- 适用于 x64 系统和 Windows 10 版本 1809 的 2019-09 累积更新 (KB4512578)
- 适用于基于 x64 系统 的 Windows 10 版本 1803 的 2019-09 累积更新 (KB4516058)
- 适用于基于 x64 系统 的 Windows 10 版本 1709 的 2019-09 累积更新 (KB4516066)

#### <a name="feature-updates-to-test"></a>要测试的功能更新

尽管你可能会看到多个 UUP 标记的更新可用，但请从 2019 年 9 月 (2019-09B) 更新或更高版本开始  。 例如：

- Windows 10 版本 1809 x64 2019-09B 的功能更新
- Windows 10 版本 1803 x64 2019-09B 的功能更新

## <a name="scenarios-to-test"></a>测试方案

### <a name="test-feature-updates"></a>测试功能更新

- 直接更新到所选择的安全符合性级别  

- 在更新之前安装 FOD 和语言包。 确保更新保留这些组件。  

### <a name="test-cumulative-updates"></a>测试累积更新

在预览期间，使用 UUP 类型更新保持客户端符合多个连续更新要求。 此测试可帮助你了解当前的行为。

### <a name="test-content"></a>测试内容

每个主要版本（1809、1803、1709）、体系结构和语言组合的第一次更新似乎规模都比较大。 与之前的非 UUP 更新相比，不管是文件数量还是磁盘空间，都有较大程度的增长。 此额外内容主要用于所有 FOD 和语言包以进行累积更新。 对于功能更新，第一次更新还包括其他大容量内容。

在此之后的未来累积和功能更新，其站点下载和分发的新内容的量要小得多。 UUP 的更新共享所有 FOD 和语言包内容，很智能。 不需要重新下载或重新分发此共享内容。 在预览期间，在 Windows 10 版本 1709 和 1803 中，此每月下载与非 UUP 方案中累积更新的大小大致相同。 在 Windows 10 版本 1809 及更高版本中，每月累积更新的增量下载要少得多。

如果查看 12 个月内下载和分发的 non-express 的总内容，会发现不具有 UUP 的 Windows 10 版本 1803 与带有 UUP 的版本 1809 大致相同  。 在带有 UUP 的版本 1809 中，整个版本生命周期中下载和分发的总内容量相对较小。

### <a name="supported-content-channels"></a>支持的内容通道

对于预览版，请测试常用的真实应用场景。 UUP 支持所有内容通道，包括：

- Windows 传递优化 (DO)
  - 使用 DO 时，请确保配置正确。 有关详细信息，请参阅[优化 Windows 10 更新传递](optimize-windows-10-update-delivery.md)。
- Configuration Manager 对等缓存
- Windows BranchCache
- 使用“无部署包”选项，客户端直接从 Microsoft 更新下载  。 将此选项与“交付优化”配合使用。
- 第三方替换内容提供程序

有关内容通道的详细信息，请参阅[优化 Windows 10 更新传递](optimize-windows-10-update-delivery.md)。

<!-- TODO: Addlink to WSUS Perf documentation-->
