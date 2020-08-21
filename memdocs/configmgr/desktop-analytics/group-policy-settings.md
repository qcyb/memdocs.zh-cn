---
title: 组策略设置
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 和桌面分析使用的 Windows 中的本地和组策略设置
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 004ca404-e6fa-47f0-ae77-e44e18a08b33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 2ee472b89f45e744e43915e51e98f11841208b73
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125793"
---
# <a name="group-policy-settings-for-desktop-analytics"></a>桌面分析的组策略设置

适用范围：Configuration Manager (Current Branch)

本文详细介绍了 Configuration Manager 和桌面分析所使用的 Windows 中的本地和组策略设置。

当 Configuration Manager 将设备注册到桌面分析时，它会设置 Windows 策略来配置设备。 在大多数情况下，仅使用 Configuration Manager 来配置这些设置。

## <a name="windows-settings"></a>Windows 设置

Configuration Manager 在以下一个或两个注册表项中设置 Windows 策略：

- 组策略对象 (GPO)：`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

- 本地策略首选项：`HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`

| 策略 | 路径 | 适用范围 | 值 |
|--------|------|------------|-------|
| **CommercialId** | 本地 | 所有 Windows 版本 | 为了让设备显示在桌面分析中，请使用组织的商业 ID 对其进行配置。 |
| **AllowTelemetry**  | GPO | Windows 10 | 为“基本”（“必需”）诊断数据设置“`1`”，为“增强”诊断数据设置“`2`”，或为“完整”（“可选”）诊断数据设置“`3`”。 桌面分析至少需要基本诊断数据。 Microsoft 建议对桌面分析使用“可选(受限)”（“增强(受限)”）级别。 有关详细信息，请参阅[配置组织中的 Windows 诊断数据](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization)。 |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | GPO | Windows 10 版本 1803 及更高版本 | 此设置仅在 AllowTelemetry 设置为 `2` 时适用。 它将发送给 Microsoft 的增强诊断数据事件限制为仅限桌面分析所需的那些事件。 有关详细信息，请参阅 [通过限制增强诊断数据策略收集的 Windows 10 诊断数据事件和字段](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields)。 |
| **AllowDeviceNameInTelemetry** | GPO | Windows 10 版本 1803 及更高版本 | 允许设备发送设备名。 默认情况下，不会将设备名称发送给 Microsoft。 如果不发送设备名称，它将在桌面分析中显示为“未知”。 有关详细信息，请参阅[设备名称](enroll-devices.md#device-name)。 |
| **CommercialDataOptIn** | 本地 | Windows 8.1 及更早版本 | 桌面分析需要值为 `1`。 有关详细信息，请参阅 [Windows 7 上的商业数据选择加入](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\))。 |
| **RequestAllAppraiserVersions** | 两者 | Windows 8.1 及更早版本 | 桌面分析需要值为 `1` 才能使数据收集正常工作。 |
| **DisableEnterpriseAuthProxy** | GPO | 所有 Windows 版本 | 如果你的环境需要一个经用户身份验证的代理来对 Internet 访问进行 Windows 集成身份验证，则桌面分析需要值为 `0` 才能使数据收集正常工作。 有关详细信息，请参阅[代理服务器身份验证](enable-data-sharing.md#proxy-server-authentication)。 |

> [!IMPORTANT]
> 在大多数情况下，仅使用 Configuration Manager 来配置这些设置。 也不要在域组策略对象中应用这些设置。 有关详细信息，请参阅[冲突解决](enroll-devices.md#conflict-resolution)。

### <a name="settings-from-upgrade-readiness"></a>来自升级就绪情况的设置

Windows Analytics 还通过升级就绪情况脚本设置以下策略：

- CommercialId
- AllowDeviceNameInTelemetry
- CommercialDataOptIn
- RequestAllAppraiserVersions

如果在设备上运行了升级就绪情况载入脚本，则这些策略设置可能仍然存在。 不要使用旧脚本。 在将设备注册到桌面分析之前，请删除以前的策略设置。

## <a name="group-policy-settings"></a>组策略设置

一般情况下，使用 Configuration Manager 集合来定位桌面分析设置和注册。 使用直接成员身份或查询来包括或排除集合中的设备。 有关详细信息，请参阅[如何创建集合](../core/clients/manage/collections/create-collections.md)。

Configuration Manager 在目标集合上配置商业 ID 和诊断数据设置。 如果需要为不同的设备组配置不同的诊断数据设置，请使用组策略设置来替代 Configuration Manager 设置。 例如，需要为一些设备设置“可选(受限)”级别，并为另一些设备设置“必需”级别。 某些设备可能具有不同的[代理服务器身份验证](enable-data-sharing.md#proxy-server-authentication)设置。

相关组策略设置位于以下路径：“计算机配置” > “管理模板” > “Windows 组件” > “数据集合和预览版本”   。

组策略设置仅修改以下项中的注册表设置：`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

> [!IMPORTANT]
> 使用组策略设置启用复杂方案时，请特别注意可能会导致配置冲突的策略设置。 如果值尚不存在，则 Configuration Manager 仅配置 [Windows 设置](#windows-settings)。 组策略设置优先于 Configuration Manager 设置，因此某些组策略配置可能会导致桌面分析出现问题。

### <a name="group-policy-settings-that-could-conflict-with-configuration-manager-settings-for-desktop-analytics"></a>可能与桌面分析的 Configuration Manager 设置冲突的组策略设置

下表中的组策略设置最有可能导致与 Configuration Manager 在注册到桌面分析的设备上所设置的 Windows 设置 之间的冲突：

| 显示名称 | 注册表值 | 在桌面分析中注册的设备上的效果 |
|--------------|----------------|-------------------------------------------------|
| **配置商业 ID** | CommercialId | 如果将此策略设置为其他值，该值会替代 Configuration Manager 设置的商业 ID。 如果其 ID 不相同，则配置的设备可能不会出现在桌面分析中。 |
| **允许遥测** | AllowTelemetry | 如果将此策略设置为其他值，该值会替代你在 Configuration Manager 中为目标集合设置的全局诊断数据级别。 |
| **将增强的诊断数据限制为 Windows Analytics 所需的最小值** | LimitEnhancedDiagnosticDataWindowsAnalytics | 此策略依赖于先前的 AllowTelemetry 设置。 根据你在 Configuration Manager 中设置的级别或使用组策略设置的级别，此策略可以将设备上的诊断数据级别更改为“增强”或“增强（受限）” 。 仅当 AllowTelemetry 设置为 `2`（增强）时，此策略才适用。 |
| **允许在 Windows 诊断数据中发送设备名** | AllowDeviceNameInTelemetry | 如果选择在 Configuration Manager 中发送设备名，可以通过将此策略配置为“已禁用”来替代它。 禁用此设置后，设备名在桌面分析中显示为“未知”。 有关详细信息，请参阅[设备名称](enroll-devices.md#device-name)。 |
| **为“连接用户体验和遥测”服务配置“使用经验证的代理”** | DisableEnterpriseAuthProxy | 如果将 Configuration Manager 设备配置为“经用户身份验证的代理”(`0`)，且如果随后将此策略配置为“禁止使用经验证的代理”(`1`)，则设备将在系统上下文而不是用户上下文中发送诊断数据。 如果未使用系统上下文中的代理配置设备，或者设备无法对代理进行身份验证，则 Windows 将无法向桌面分析发送诊断数据。 |

> [!NOTE]
> 旧策略“配置连接用户体验和遥测”(TelemetryProxy) 允许 Windows 将诊断数据转发到专用代理，而不是使用用户 (WinINET) 或设备 (WinHTTP) 代理。 某些 Windows 组件不支持此策略。 如果使用此策略，则可能会导致桌面分析中出现数据质量问题。

#### <a name="behavior-of-disabled-settings"></a>禁用的设置的行为

如果将这些组策略设置配置为“禁用”，则其会对系统行为产生不同的影响。

- 禁用“CommercialId”策略时，Windows 将删除该注册表值。 然后，商业 ID 的 Configuration Manager 设置（在本地策略注册表路径中设置）将应用于该设备。

- 对于 Configuration Manager 在与组策略位置相同的注册表位置中设置的策略，在禁用组策略中的设置时，Windows 将删除该注册表值。 Configuration Manager 将在下一个策略处理周期再次对其进行设置，然后 Windows 将在下一次组策略刷新时将其删除。 配置中的这种不断更改可能会导致桌面分析出现不希望发生的行为。

  - 如果将这些组策略设置设为“未配置”，则 Windows 将删除该值一次，但不会持续将其删除。 此配置使 Configuration Manager 能够按预期应用其值。

### <a name="group-policy-settings-to-customize-the-user-experience"></a>用于自定义用户体验的组策略设置

Configuration Manager 或桌面分析不需要这些组策略设置。 你可以在组策略中对其进行配置，以便使用 Windows 诊断数据配置用户体验。

| 显示名称 | 注册表值 | 在桌面分析中注册的设备上的效果 |
|--------------|----------------|-------------------------------------------------|
| **配置遥测选择加入更改通知** | DisableTelemetryOptInChangeNotification | 从 Windows 10 版本 1803 开始，Windows 会在诊断数据级别发生更改时通知用户。 使用此策略可禁用通知。 |
| **配置遥测选择加入设置用户界面** | DisableTelemetryOptInSettingsUx | 配置诊断数据级别时，请设置设备的上限。 从 Windows 10 版本 1803 开始，用户可以设置较低的级别。 使用此策略防止用户更改诊断级别。 有关详细信息，请参阅[配置组织中的 Windows 诊断数据](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management)。 |
| **禁止删除诊断数据** | DisableDeviceDelete | 从 Windows 10 版本 1809 开始，用户可以从“诊断和反馈”设置页删除诊断数据。 使用此策略以防止删除 Microsoft 从设备收集的诊断数据。 |
| **禁用诊断数据查看器** | DisableDiagnosticDataViewer | 从 Windows 10 版本 1809 开始，用户可以从“诊断和反馈”设置页启用并打开诊断数据查看器。 使用此策略以禁用 Windows 设置中的诊断数据查看器，并阻止其显示 Microsoft 从设备收集的诊断数据。|
