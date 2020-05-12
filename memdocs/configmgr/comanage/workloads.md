---
title: 共同管理工作负载
titleSuffix: Configuration Manager
description: 了解可以从 Configuration Manager 切换到 Microsoft Intune 的工作负载。
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
ms.openlocfilehash: 928ef8a8ebc90807912f22901743725df9aa67e7
ms.sourcegitcommit: 79fb3b0f0486de1644904be348b7e08048e93b18
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82842217"
---
# <a name="co-management-workloads"></a>共同管理工作负载

不必切换工作负载，或可以在准备好后单独执行这些工作负载。 Configuration Manager 持续管理所有其他工作负载（其中包括不切换到 Intune 的那些工作负载）以及共同管理不支持的的所有其他 Configuration Manager 功能。

如果将工作负载切换到 Intune，但后来改了主意，则可以将其切换回 Configuration Manager。

共同管理支持以下工作负载：

- [符合性策略](#compliance-policies)  

- [Windows 更新策略](#windows-update-policies)  

- [资源访问策略](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [设备配置](#device-configuration)  

- [Office 即点即用应用](#office-click-to-run-apps)  

- [客户端应用](#client-apps)  

## <a name="compliance-policies"></a>相容性策略

符合性策略定义设备必须遵从的规则和设置，以便将设备视为符合条件访问策略。 也可使用符合性策略来监视和修正独立于条件访问的设备符合性问题。 自 Configuration Manager 版本 1910 开始，可以将自定义配置基线评估添加为合规性策略评估规则。 有关详细信息，请参阅[将自定义配置基线包含在合规性策略评估中](../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines)。

有关 Intune 功能的详细信息，请参阅[设备符合性策略](https://docs.microsoft.com/intune/device-compliance-get-started)。  

## <a name="windows-update-policies"></a>Windows 更新策略

通过适用于企业的 Windows 更新策略，可以针对 Windows 10 功能更新或直接由适用于企业的 Windows 更新托管的 Windows 10 设备的质量更新，配置延迟策略。

有关 Intune 功能的详细信息，请参阅[配置适用于企业的 Windows 更新延迟策略](https://docs.microsoft.com/intune/windows-update-for-business-configure)。  

## <a name="resource-access-policies"></a>资源访问策略

资源访问策略在设备上配置 VPN、Wi-Fi、电子邮件以及证书设置。

有关 Intune 功能的详细信息，请参阅[部署资源访问配置文件](https://docs.microsoft.com/intune/device-profiles)。

> [!Note]  
> 资源访问工作负载也是设备配置的一部分。 切换[设备配置](#device-configuration)工作负载时，这些策略由 Intune 托管。

## <a name="endpoint-protection"></a>Endpoint Protection

<!--1357365-->

Endpoint Protection 工作负载包括 Windows Defender 反恶意软件保护功能套件：

- Windows Defender 反恶意软件
- Windows Defender 应用程序防护  
- Windows Defender 防火墙  
- Windows Defender SmartScreen  
- Windows 加密
- Windows Defender 攻击防护  
- Windows Defender 应用程序控制  
- Windows Defender 安全中心  
- Windows Defender 高级威胁防护（现称为 Microsoft Defender 威胁防护）

有关 Intune 功能的详细信息，请参阅 [Microsoft Intune 的 Endpoint Protection](https://docs.microsoft.com/intune/endpoint-protection-windows-10)。

> [!Note]  
> 在切换此工作负载时，Configuration Manager 策略将保留在设备上，直到 Intune 策略覆盖它们。 此行为可确保设备在过渡期间仍具有保护策略。
>
> Endpoint Protection 工作负载也是设备配置的一部分。 当切换[设备配置](#device-configuration)工作负载时，同样的行为适用。<!-- SCCMDocs.nl-nl issue #4 --> 切换设备配置工作负载时，它还包括“Windows 信息保护”功能策略，但其未包含在 Endpoint Protection 工作负载中。<!-- 4184095 -->
>
> 如果 Microsoft Defender 防病毒设置属于 Intune 设备配置的设备限制配置文件类型，则这些设置不在 Endpoint Protection 滑块的范围内。 要为启用了 Endpoint Protection 滑块的共同管理的设备管理 Microsoft Defender 防病毒设置，请使用“Microsoft Endpoint 管理中心” > “终结点安全性” > “防病毒”中新的防病毒策略    。 此策略类型提供了改进后的新选项，还支持可在设备限制配置文件中使用的设置。 <!--6609171-->
>
> Windows 加密功能包括 BitLocker 管理。 要详细了解此功能与共同管理一起使用时的行为，请参阅[部署 BitLocker 管理](../protect/deploy-use/bitlocker/deploy-management-agent.md#co-management-and-intune)。<!-- SCCMDocs#2321 -->

## <a name="device-configuration"></a>设备配置

<!--1357903-->

设备配置工作负载包括管理组织中的设备的设置。 切换此工作负载时一并移动“资源访问”和“Endpoint Protection”工作负载   。

即使设备配置颁发机构是 Intune，你仍可将 Configuration Manager 中的设置部署到共同托管的设备。 此异常可用于配置组织需要但在 Intune 中尚不可用的设置。 在 [Configuration Manager 配置基线](../compliance/deploy-use/create-configuration-baselines.md)上指定此异常。 创建基线时，启用“即使是共同托管客户端也要始终应用此基线”选项  。 稍后，可以在现有基线属性的“常规”  选项卡上进行更改。  

有关 Intune 功能的详细信息，请参阅[在 Microsoft Intune 中创建设备配置文件](https://docs.microsoft.com/intune/device-profile-create)。  

> [!NOTE]
> 切换设备配置工作负载时，它还包括“Windows 信息保护”功能策略，但其未包含在 Endpoint Protection 工作负载中。<!-- 4184095 -->

## <a name="office-click-to-run-apps"></a>Office 即点即用应用

<!--1357841-->

此工作负载管理共同管理的设备上的 Office 365 应用。

- 移动工作负荷后，此应用将显示在设备上的“公司门户”中   

- 除非重启设备，否则 Office 更新可能约在 24 小时后才能显示在客户端上  

- 存在一个新的全局条件，即“Office 365 应用程序是否在设备上由 Intune 进行托管”  。 默认情况下将此条件作为一项要求添加到新的 Office 365 应用程序。 如果在转换此工作负荷时，共同托管客户端不满足应用程序的要求。 则不会安装通过 Configuration Manager 部署的 Office 365。  

有关 Intune 功能的详细信息，请参阅[将 Office 365 应用分配给具有 Microsoft Intune 的 Windows 10 设备](https://docs.microsoft.com/intune/apps-add-office365)。

## <a name="client-apps"></a>客户端应用

<!--1357892-->

使用 Intune 在共同管理的 Windows 10 设备上管理客户端应用和 PowerShell 脚本。 转移此工作负荷之后，任何从 Intune 部署的可用应用在公司门户中也变得可用。 从 Configuration Manager 部署的应用在软件中心可用。

有关 Intune 功能的详细信息，请参阅[什么是 Microsoft Intune 应用管理？](https://docs.microsoft.com/intune/app-management)。

> [!Tip]  
> 此功能在版本 1806 中作为[预发行功能](../core/servers/manage/pre-release-features.md)首次引入。 从版本 2002 开始，此功能不再属于预发行功能。  
>
> 此功能可能以“适用于共同托管设备的移动应用”的形式在功能列表中显示  。<!-- 5849669 -->

自版本 1910 开始，在 Configuration Manager 分发点上启用 Microsoft Connected Cache 后，现在可以为共同管理的客户端提供 Microsoft Intune Win32 应用。 有关详细信息，请参阅 [Configuration Manager 中的 Microsoft Connected Cache](../core/plan-design/hierarchy/microsoft-connected-cache.md#bkmk_intune)。

## <a name="diagram-for-app-workloads"></a>应用工作负载的关系图

![共同管理应用工作负载的关系图](media/co-management-apps.svg)

[以完整尺寸查看关系图](media/co-management-apps.svg)

## <a name="known-issues"></a>已知问题

在将 Endpoint Protection 工作负载移动到 Intune 时，客户端可能仍会采用 Configuration Manager 和 Microsoft Defender 设置的策略。 <!--5024559-->

要解决此问题，请在客户端收到 Intune 策略之后，按照以下步骤使用 ConfigSecurityPolicy.exe 来应用 CleanUpPolicy.xml：

1. 复制以下文本并将它保存为 `CleanUpPolicy.xml`。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <SecurityPolicy xmlns="http://forefront.microsoft.com/FEP/2010/01/PolicyData" Name="FEP clean-up policy"><PolicySection Name="FEP.AmPolicy"><LocalGroupPolicySettings><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Microsoft Antimalware"/><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Windows Defender"/></LocalGroupPolicySettings></PolicySection></SecurityPolicy>
   ```
1. 打开提升的命令提示符来转到 `ConfigSecurityPolicy.exe`。 通常，该可执行文件位于下列目录之一：
   - C:\Program Files\Windows Defender
   - C:\Program Files\Microsoft Security Client
1. 从命令提示符处，传入 xml 文件以清理策略。 例如，`ConfigSecurityPolicy.exe C:\temp\CleanUpPolicy.xml`。  

## <a name="next-steps"></a>后续步骤

[如何切换工作负载](how-to-switch-workloads.md)  
