---
title: 兼容性评估
titleSuffix: Configuration Manager
description: 了解桌面分析中 Windows 应用和驱动程序的兼容性评估。
ms.date: 03/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0d5397dca3c8abff056b7944bde7d27794c45401
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707815"
---
# <a name="compatibility-assessment-in-desktop-analytics"></a>桌面分析中的兼容性评估

先前解决方案中的升级评估是通用的，例如：需要注意或修补程序可用。 对于如何对有问题或升级见解的应用或驱动程序设置优先级，它不提供任何可视标志。 桌面分析将此功能替换为**兼容性风险**。 桌面分析仅在升级前方案的部署视图中显示应用评估。 它基于 Microsoft 从包含在当前部署计划中的计算机获得的见解对应用进行分类。

桌面分析使用以下兼容性评估类别：

- **低**：该服务未找到任何使此应用面临 Windows 升级风险的信号。 可能会按原样在目标操作系统上运行。

- **中**：分析表明，尽管可能会进行补救，但应用程序的功能可能受损。

- **高**：升级期间或之后，该应用程序几乎肯定会出现故障。 可能需要进行补救。

- **未知**：该应用未经评估。 没有其他任何见解，如“MS 已知问题”  。

在部署计划中的应用或驱动程序资产列表中，你将在“兼容性风险”  列中看到每个资产的这项值。

## <a name="app-risk-assessment"></a>应用风险评估

![应用风险评估来源图](media/app-risk-assessment-sources.png)

桌面分析使用以下几种来源来生成应用程序的评估等级：

- [Microsoft 已知问题](#microsoft-known-issues)
- [高级见解](#advanced-insights)

你可以在桌面分析中的应用上找到针对每个来源的评估。 在部署计划中的应用资产列表中，选择单个应用以打开其属性浮出窗格。 你将看到整体建议和评估级别。 **兼容性风险因素**部分显示了这些评估的详细信息。

## <a name="microsoft-known-issues"></a>Microsoft 已知问题

桌面分析会查看 Microsoft 应用程序兼容性数据库中的任何已知问题。 它使用此数据库来确定来自 Microsoft 或其他发布者的公开可用的应用程序的任何现有兼容性块。 此检查仅适用于所选部署计划的目标操作系统。

你将在“应用属性”窗格上看到以下作为“MS 已知问题”  的问题：

### <a name="asset-is-removed-during-upgrade"></a>资产在升级期间被删除

Windows 检测到应用程序或驱动程序的兼容性问题。 资产不能迁移到新的操作系统版本。 无需执行任何操作即可继续升级。 在新的操作系统版本上安装应用程序或驱动程序的兼容版本。

<!-- 3594545 -->
Windows 可以部分或完全删除这些资产：

- 完全删除：Windows 安装程序会在升级期间从设备中完全删除应用或驱动程序。
- 部分删除：Windows 安装程序会在升级期间从设备中部分删除应用或驱动程序。 升级 Windows 后，需要手动卸载它。

在这两种情况下，在升级 Windows 后，用户无法使用该应用或与驱动程序相关的硬件。

若要在桌面分析门户中查看此建议：

1. 在部署计划中，选择“准备试点”  。
1. 选择“应用”选项卡  。
1. 选择一个应用，然后在侧窗格中查看兼容性风险因素和建议。

[![桌面分析门户中资产建议的屏幕截图](media/3594545-app-removed.png)](media/3594545-app-removed.png#lightbox)

### <a name="blocking-upgrade"></a>阻止升级

Windows 检测到阻塞性问题，因此无法在升级期间删除此应用程序。 它可能无法在新的操作系统版本上运行。 在升级之前，请删除此应用程序。 在新的操作系统版本上重新安装并进行测试。

### <a name="blocking-upgrade-but-can-be-reinstalled-after-upgrading"></a>阻止升级，但可以在升级后重新安装

应用程序与新的操作系统版本兼容，但不会迁移。 请在升级 Windows 之前删除此应用程序。 在新的操作系统版本上重新安装。

### <a name="blocking-upgrade-update-application-to-newest-version"></a>阻止升级，将应用程序更新到最新版本

此应用程序的现有版本与新的操作系统版本不兼容，将不会迁移。 有此应用程序的兼容版本可用。 请在升级之前更新此应用程序。

### <a name="disk-encryption-blocking-upgrade"></a>磁盘加密阻止升级

应用程序的加密功能会阻止升级。 在升级 Windows 之前禁用加密功能，升级后再启用。

### <a name="does-not-work-with-new-os-but-wont-block-upgrade"></a>不适用于新操作系统，但不会阻止升级

此应用程序与新的操作系统不兼容，但不会阻止升级。 无需执行任何操作即可继续升级。 在新的操作系统版本上安装应用程序的兼容版本。

### <a name="does-not-work-with-new-os-and-will-block-upgrade"></a>不适用于新操作系统，但不会阻止升级

此应用程序与新的操作系统不兼容，将阻止升级。 请在升级之前删除此应用程序。 可以使用应用程序的兼容版本。

### <a name="evaluate-application-on-new-os"></a>在新的操作系统上评估应用程序

Windows 将迁移此应用程序，但它检测到可能会影响应用在新系统版本上的性能的问题。 无需执行任何操作即可继续升级。 在新的操作系统版本上测试此应用程序。

### <a name="may-block-upgrade-test-application"></a>可能会阻止升级、测试应用程序

Windows 检测到可能会干扰升级但需要进一步调查的问题。 在升级期间测试应用程序的行为。 如果它阻止升级，请在升级前将其删除。 然后在新的操作系统版本上重新安装并测试。

### <a name="multiple"></a>多个

有多个问题影响此应用程序。 选择“查询”  以查看 Windows 检测到的问题详情。

### <a name="reinstall-application-after-upgrading"></a>在升级后重新安装应用程序

应用程序与新的操作系统版本兼容，但需要在升级 Windows 后重新进行安装。 升级过程会删除此应用程序。 无需执行任何操作即可继续升级。 在新的操作系统版本上重新安装此应用程序。

### <a name="safeguards"></a>安全防护

<!-- 5746559 -->

Windows 兼容性数据通过防护措施对一些应用和驱动程序进行分类，这可能导致 Windows 10 的更新失败或回滚  。 Windows 还可能会升级，但会删除应用或驱动程序。 而现在，桌面分析可帮助你提前确定这些防护措施，让你能够在部署更新之前对资产进行修正。

1. 在桌面分析门户中，选择一项部署计划。

1. 选择菜单中的“计划资产”，然后切换到“应用”选项卡   。

1. 筛选名称列，显示其值中带有 `Safeguard` 一词的项目。 选择结果以查看详细信息。

    > [!NOTE]
    > 此条目并非是安装到你的设备上的真实应用。 它是一个占位符，帮助通过防护兼容性标记确定你环境中的应用或驱动程序。

1. 在“建议”部分中，选择指向“了解详细信息”的链接  。 此链接将打开 Windows 网站，上面有带防护标记的应用或驱动程序的当前列表。

1. 根据你环境中的资产列表来比较当前已发布的列表。 通过更新到兼容版本来修正任何潜在的问题应用或驱动程序。

[![桌面分析中的保护应用屏幕截图](media/5746559-safeguards.png)](media/5746559-safeguards.png#lightbox)

## <a name="advanced-insights"></a>高级见解

桌面分析还使用以下其他见解检测问题：

### <a name="adopted-version-available"></a>可采用版本

此应用的另一个版本已被其他客户广泛采用。 此信号使用来自 Windows 生态系统的采用数据。 如果当前版本中有任何程序阻止升级，则考虑部署替代版本。 若要查找备用应用程序采用的版本，请参阅“准备生产”下的应用程序运行状况。

### <a name="driver-dependency"></a>驱动程序依赖关系

此应用依赖于驱动程序。 桌面分析建议将此应用进行试点测试以发现任何回归。 如果你有任何疑问，请联系发布者以请求与 Windows 10 兼容的版本。

### <a name="additional-insights"></a>其他见解

<!-- 4021225 -->
当你将 Configuration Manager 站点和客户端升级至版本 1906 时，客户还可以报告这些其他见解，当诊断数据级别设为增强受限时：

> [!Important]  
> 若要利用 Configuration Manager 的新功能，更新站点后，还请将客户端更新到最新版本。 除非此客户端版本也是最新版本，否则此方案不起作用。

#### <a name="16-bit-apps"></a>16 位应用

从应用程序中删除所有 16 位组件，然后替换为 32 位或 64 位等效组件。 有关详细信息，请参阅 [Windows Vista 和 Windows Server 2008 开发人员案例：应用程序兼容性指南](https://docs.microsoft.com/previous-versions/aa480152\(v=msdn.10\))。

另一个选项是在 Windows 10 上启用 NT 虚拟 DOS 机 (NTVDM) 以获得支持。

#### <a name="requires-admin-privileges"></a>需要管理员权限

此应用要求用户拥有设备的管理访问权限。 针对这些需要管理员权限的应用使用应用清单。 有关详细信息，请参阅[创建和嵌入应用程序清单](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\))。

桌面分析建议将此应用进行试点测试以发现任何回归。

#### <a name="java-dependency"></a>Java 依赖关系

许多 Java 应用程序依赖于单独安装的 Java Runtime Environment (JRE)。 尽管较旧的 JRE 版本可能会继续在 Windows 10 上运行，但 Oracle 仅支持最新的 JRE 版本。 使用不受支持的较旧 JRE 可能会产生安全漏洞。 查看你的应用程序是否在最新的 JRE 版本上运行。

#### <a name="not-dpi-aware"></a>非 DPI 感知

此应用在 Windows 10 上可能会出现高级屏幕分辨率显示问题。 使用应用清单以避免出现任何高 DPI 分辨率问题。 有关详细信息，请参阅[应用程序清单](https://docs.microsoft.com/windows/desktop/SbsCs/application-manifests)。

桌面分析建议将此应用进行试点测试以发现任何回归。

#### <a name="silverlight-framework"></a>Silverlight 框架

Microsoft 建议非基于浏览器的应用不要使用 Silverlight。 Silverlight 5 的支持结束日期为 2021 年 10 月。

大多数当前 Web 浏览器不支持 Silverlight。

| 浏览器 | 支持 |
|---------|---------|
| Google Chrome | 结束支持：2015 年 9 月 |
| FireFox | 结束支持：2017 年 3 月 |
| Microsoft Edge | 无可用插件 |

桌面分析建议将此应用进行试点测试以发现任何回归。

#### <a name="net-framework-1011"></a>.NET Framework 1.0/1.1

Windows 10 不支持 .NET Framework 版本1.0。 版本 1.1 在 Windows 10 上不兼容。 如果此应用来自第三方发布者，请与供应商联系，以请求兼容 Windows 10 的版本。 否则，请重新开发此应用程序以使用 .NET 的受支持版本。

#### <a name="net-framework-2030"></a>.NET Framework 2.0/3.0

Windows 10 上支持 .NET 2.0 和 3.5 框架。 你可能需要启用此 Windows 功能。 有关更多信息，请参阅[在 Windows 10 上安装 .NET Framework 3.5](https://docs.microsoft.com/dotnet/framework/install/dotnet-35-windows-10)。

#### <a name="ui-access"></a>UI 访问

具有 UI 访问权限的应用程序可以绕过用户界面控制级别，以将输入驱动到桌面上具有更高权限的窗口。 仅对用户界面辅助技术应用程序使用此设置。

如果未在应用中使用辅助功能，则在应用清单中将 UI 访问标志设置为“false”。 有关详细信息，请参阅[创建和嵌入应用程序清单](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\))。

桌面分析建议将此应用进行试点测试以发现任何回归。

## <a name="driver-risk-assessment"></a>驱动程序风险评估

桌面分析还按可用性列出了不迁移到操作系统版本的任何驱动程序并进行了分组。

你可以在桌面分析中找到对驱动程序的评估。 在部署计划中的驱动程序资产列表中，选择单个驱动程序以打开其属性浮出窗格。 你将看到整体建议和评估级别。 **兼容性风险因素**部分显示了这些评估的详细信息。

| 驱动程序可用性 | 需要执行操作？ | 含义 | 指南 |
|---------------------|------------------|---------------|----------|
| 可从产品包装获取 | 否，仅供了解 | 当前安装的应用程序或驱动程序版本不会迁移到新的操作系统版本。 新的操作系统安装了兼容版本。 | 无需执行任何操作即可继续升级。 |
| 从 Windows 更新导入 | 是 | 当前安装的驱动程序版本不会迁移到新的操作系统版本。 Windows 更新提供兼容版本。 | 如果计算机自动接收来自“Windows 更新”的更新，则无需执行任何操作。 否则，请在升级 Windows 后从 Windows 更新导入新的驱动程序。 |
| 可从产品包装和 Windows 更新中获取 | 是 | 当前安装的驱动程序版本不会迁移到新的操作系统版本。 尽管在升级期间安装了新的驱动程序，但 Windows 更新提供了较新版本。 | 如果计算机自动接收来自“Windows 更新”的更新，则无需执行任何操作。 否则，请在升级 Windows 后从 Windows 更新导入新的驱动程序。 |
| 与供应商核实 | 是 | 驱动程序不会迁移到新的操作系统版本，桌面分析无法找到兼容版本。 | 对于解决方案，与生产驱动程序的独立硬件供应商 (IHV) 或提供此设备的原始设备供应商 (OEM) 核实。 |

## <a name="see-also"></a>另请参阅

适用于 Windows 10 的 FastTrack 中心权益提供**桌面应用保证**的访问权限。 此权益是一项旨在解决 Windows 10 和 Office 365 ProPlus 应用兼容性问题的新服务。 有关详细信息，请参阅[桌面应用保证](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure)。
