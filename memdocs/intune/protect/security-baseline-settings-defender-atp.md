---
title: 用于 Microsoft Defender 高级威胁防护的 Intune 安全基线设置
titleSuffix: Microsoft Intune
description: Intune 支持用于管理 Microsoft Defender 高级威胁防护的安全基线设置
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
zone_pivot_groups: atp-baseline-versions
ms.openlocfilehash: 330a4387ef1a079b2a0f691bfb0b887117dd9e4b
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429344"
---
<!-- Pivots in use: 
::: zone pivot="atp-april-2020"
::: zone-end

::: zone pivot="atp-march-2020"
::: zone-end

::: zone pivot="atp-march-2020,atp-april-2020"
::: zone-end
-->

# <a name="microsoft-defender-advanced-threat-protection-baseline-settings-for-intune"></a>Intune 的 Microsoft Defender 高级威胁防护基线设置

查看 Microsoft Intune 支持的 Microsoft Defender 高级威胁防护基线设置。 高级威胁防护 (ATP) 基线默认值表示针对 ATP 的建议配置，可能与其他安全基线中的基线默认值不匹配。

::: zone pivot="atp-april-2020"

本文中的详细信息适用于 2020 年 4 月 21 日发布的 Microsoft Defender ATP 基线版本 4。 若要了解此版本的基线较以前版本的更改情况，请使用[比较基线](../protect/security-baselines.md#compare-baseline-versions)操作，该操作在查看此基线的“版本”窗格时可用。

::: zone-end
::: zone pivot="atp-march-2020"

本文中的详细信息适用于 2020 年 3 月 1 日发布的 Microsoft Defender ATP 基线版本 3。 若要了解此版本的基线较以前版本的更改情况，请使用[比较基线](../protect/security-baselines.md#compare-baseline-versions)操作，该操作在查看此基线的“版本”窗格时可用。

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"


当环境满足使用 [Microsoft Defender 高级威胁防护](advanced-threat-protection.md#prerequisites)的先决条件时，Microsoft Defender 高级威胁防护基线才可用。

此基线针对物理设备进行了优化，目前不建议在虚拟机 (VM) 或 VDI 终结点上使用。 某些基线设置可能会影响虚拟化环境中的远程交互式会话。 有关详细信息，请参阅 Windows 文档中的[提高 Microsoft Defender ATP 安全基线的符合性](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline)。


## <a name="application-guard"></a>应用程序防护

有关详细信息，请参阅 Windows 文档中的 [WindowsDefenderApplicationGuard CSP](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp)。  

使用 Microsoft Edge 时，Microsoft Defender 应用程序防护可保护环境免受组织不信任的站点的影响。 用户访问独立网络边界中未列出的站点时，这些站点将在 Hyper-V 虚拟浏览会话中打开。 受信任的站点由网络边界定义。  

- **启用 Edge 应用程序防护（选项）**  
  CSP：[Settings/AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)
  
  - **为 Edge 启用**（默认）- 应用程序防护在通过 Hyper-V 虚拟化的浏览容器中打开未受批准的站点。
  - **未配置** - 在该设备上（而不是在虚拟化容器中）打开任何站点（受信任和不受信任）。  
  
  在设置为“为 Edge 启用”时，可以配置“阻止来自非企业认可网站的外部内容”和“剪贴板行为”  。

  - **阻止来自非企业认可网站的外部内容**  
    CSP：[Settings/BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **是**（默认）- 阻止加载未经批准的网站中的内容。
    - **未配置** - 可以在设备上打开非企业站点

  - **剪贴板行为**  
    CSP：[Settings/ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    选择允许在本地电脑和应用程序防护虚拟浏览器之间执行的复制和粘贴操作。 选项包括：
    - **未配置**  
    - **阻止在电脑和浏览器之间进行复制和粘贴**（默认）- 阻止两者。 无法在电脑和虚拟浏览器之间传输数据。
    - **仅允许从浏览器复制和粘贴到电脑** - 数据无法从电脑传输到虚拟浏览器。
    - **仅允许从电脑复制和粘贴到浏览器** - 数据无法从虚拟浏览器传输到主机电脑。
    - **允许在电脑和浏览器之间进行复制和粘贴** - 不阻止任何内容。

- **Windows 网络隔离策略**  
  CSP：[策略 CSP - NetworkIsolation](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-networkisolation)

  指定网络域列表，这些域是应用程序防护将其视为企业站点的云中托管的企业资源
  - 配置（默认）
  - 未配置

  如果设置为“配置”，则可以定义网络域 。

  - **网络域**  
    选择“添加”并指定域、IP 地址范围和网络边界。 默认情况下，会配置 securitycenter.windows.com。

## <a name="bitlocker"></a>BitLocker

有关详细信息，请参阅 Windows 文档中的 [BitLocker 组策略设置](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings)。

- **需要加密存储卡(仅限移动设备)**  
  CSP：[RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  此设置仅适用于 Windows Mobile 和 Mobile Enterprise SKU 设备。
  - **是**（默认）- 移动设备需要加密存储卡。
  - **未配置** - 设置会返回到 OS 默认设置，即不需要存储卡加密。

- **对 OS 和固定数据驱动器启用全磁盘加密**  
  CSP：[RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  如果在应用此策略之前已对驱动器进行了加密，则不会执行额外的操作。 如果加密方法和选项与此策略匹配，则配置应返回成功。 如果就地 BitLocker 配置选项与此策略不匹配，则配置可能会返回错误。
  
  要将此策略应用到已加密的磁盘，请解密该驱动器，然后重新应用 MDM 策略。 Windows 默认设置为不需要 BitLocker 驱动器加密，但在注册/登录 Azure AD 联接和 Microsoft 帐户 (MSA) 时，可能会应用自动加密，以启用 XTS-AES 128 位加密的 BitLocker。

  - **是**（默认）- 强制使用 BitLocker。
  - **未配置** - 不会强制使用 BitLocker。

- **BitLocker 系统驱动器策略**  
  [BitLocker 组策略设置](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **配置**（默认）
  - 未配置

  设置为“配置”时，你可以配置“配置操作系统驱动器的加密方法” 。

  - **配置操作系统驱动器的加密方法**  
    CSP：[EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    此设置在“BitLocker 系统驱动器策略”设置为“配置”时可用 。  

    配置系统驱动器的加密方法和密码长度。  XTS-AES 128 位是 Windows 默认加密方法和建议的值。

    - **未配置**（默认）
    - AES 128 位 CBC
    - AES 256 位 CBC
    - AES 128 位 XTS
    - AES 256 位 XTS

- **BitLocker 固定驱动器策略**  
  [BitLocker 组策略设置](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **配置**（默认）
  - 未配置

  设置为“配置”时，你可以配置“阻止对不受 BitLocker 保护的固定数据驱动器的写权限”和“配置固定数据驱动器的加密方法”  。

  - **阻止对不受 BitLocker 保护的固定数据驱动器的写权限**  
    CSP：[FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    此设置在“BitLocker 固定驱动器策略”设置为“配置”时可用 。

    - **未配置**（默认）- 可将数据写入非加密的固定驱动器。
    - 是 - Windows 将不允许向不受 BitLocker 保护的固定驱动器写入任何数据。 如果未对固定驱动器进行加密，则在授予写入权限之前，用户将需要完成驱动器的 BitLocker 安装向导。

  - **配置固定数据驱动器的加密方法**  
    CSP：[EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    此设置在“BitLocker 固定驱动器策略”设置为“配置”时可用 。

    配置固定数据驱动器磁盘的加密方法和密码长度。 XTS-AES 128 位是 Windows 默认加密方法和建议的值。

    - **未配置**（默认）
    - AES 128 位 CBC
    - AES 256 位 CBC
    - AES 128 位 XTS
    - AES 256 位 XTS

- **BitLocker 可移动驱动器策略**  
  [BitLocker 组策略设置](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **配置**（默认）
  - 未配置

  设置为“配置”时，你可以配置“配置可移动数据驱动器的加密方法”和“阻止对不受 BitLocker 保护的可移动数据驱动器的写权限”  。

  - **配置可移动数据驱动器的加密方法**  
    CSP：[EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    此设置在“BitLocker 可移动驱动器策略”设置为“配置”时可用 。

    配置可移动数据驱动器磁盘的加密方法和密码长度。 XTS-AES 128 位是 Windows 默认加密方法和建议的值。

    - 未配置
    - AES 128 位 CBC
    - AES 256 位 CBC（默认）
    - AES 128 位 XTS
    - AES 256 位 XTS

  - **阻止对不受 BitLocker 保护的可移动数据驱动器的写权限**  
    CSP：[RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)  
    此设置在“BitLocker 可移动驱动器策略”设置为“配置”时可用 。

    - **未配置**（默认）- 可将数据写入非加密的可移动驱动器。  
    - 是 - Windows 将不允许向不受 BitLocker 保护的可移动驱动器写入任何数据。 如果未对可移动驱动器进行加密，则在授予写入权限之前，用户必须完成驱动器的 BitLocker 安装向导。

## <a name="browser"></a>浏览器

- **Microsoft Edge SmartScreen**  
  CSP：[Browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **是**（默认）- 使用 SmartScreen 防止用户受潜在网络钓鱼诈骗和恶意软件侵袭。
  - 未配置

- **阻止恶意网站访问**  
  CSP：[Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **是**（默认）- 阻止用户忽略 Microsoft Defender SmartScreen 筛选器警告并阻止他们访问该站点。
  - 未配置

- **阻止下载未经验证的文件**  
  CSP：[Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **是**（默认）- 阻止用户忽略 Microsoft Defender SmartScreen 筛选器警告并阻止他们下载未经验证的文件。
  - 未配置

## <a name="data-protection"></a>数据保护

- **阻止直接内存访问**  
  CSP：[DataProtection/AllowDirectMemoryAccess](https://go.microsoft.com/fwlink/?linkid=2067031)  

  只在启用了 BitLocker 或设备加密时才执行此策略设置。

  - **是**（默认）- 阻止所有热插拔 PCI 下游端口进行直接内存访问 (DMA)，直到用户登录 Windows。 用户登录后，Windows 会枚举连接到热插拔 PCI 端口的 PCI 设备。 用户每次锁定计算机都会阻止无子设备的热插拔 PCI 端口进行 DMA，直到用户再次登录。 已在计算机解锁时枚举的设备继续工作，直到拔出。
  - 未配置

## <a name="device-guard"></a>Device Guard  

- **启用 Credential Guard**  
  CSP：[DeviceGuard/ConfigureSystemGuardLaunch](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard 使用 Windows 虚拟机监控程序来提供保护，这需要安全启动和 DMA 保护才能正常运行，因此必需满足硬件要求。

  - **未配置** - 禁用 Credential Guard，这是 Windows 的默认设置。
  - 启用且具有 UEFI 锁定（默认）- 启用 Credential Guard 并且不允许远程禁用该功能，因为必须手动清除 UEFI 保存的配置。
  - 启用但不具有 UEFI 锁定 - 启用 Credential Guard，并允许在没有对计算机进行物理访问的情况下将其关闭。

## <a name="device-installation"></a>设备安装

- **按设备标识符安装硬件设备**  
  [DeviceInstallation/PreventInstallationOfMatchingDeviceIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  使用此策略设置可以指定禁止 Windows 安装的设备的即插即用硬件 ID 和兼容 ID 的列表。 此策略设置优先于任何其他允许 Windows 安装设备的策略设置。  如果在某个远程桌面服务器上启用了此策略设置，则此策略设置会影响指定设备从远程桌面客户端到该远程桌面服务器的重定向。

  - 未配置
  - 允许安装硬件设备 - 可根据其他允许或禁止策略设置来安装和更新设备。
  - 阻止安装硬件设备（默认）- 禁止 Windows 安装你所定义的列表中列出了其硬件 ID 或兼容 ID 的设备。

  设置为“阻止安装硬件设备”时，你可以配置“删除匹配的硬件设备”和“已阻止的硬件设备标识符”  。

  - **删除匹配的硬件设备**

    仅“按设备标识符安装硬件设备”设置为“阻止安装硬件设备”时，此设置才可用 。
    - **是**
    - 未配置

  - **已阻止的硬件设备标识符**  
    
    仅“按设备标识符安装硬件设备”设置为“阻止安装硬件设备”时，此设置才可用 。

    选择“添加”，然后指定要阻止的硬件设备标识符。

- **按安装程序类安装硬件设备**  
  CSP：[DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses](https://go.microsoft.com/fwlink/?linkid=2067048)  
  
  使用此策略设置可以指定禁止 Windows 安装的设备驱动程序的设备安装程序类全局唯一标识符 (GUID) 列表。 此策略设置优先于任何其他允许 Windows 安装设备的策略设置。 如果在某个远程桌面服务器上启用了此策略设置，则此策略设置会影响指定设备从远程桌面客户端到该远程桌面服务器的重定向。

  - 未配置
  - 允许安装硬件设备 - Windows 可根据其他允许或禁止策略设置来安装和更新设备。
  - 阻止安装硬件设备（默认）- 禁止 Windows 安装你所定义的列表中列出了其安装程序类 GUID 的设备。

  设置为“阻止安装硬件设备”时，你可以配置“删除匹配的硬件设备”和“已阻止的硬件设备标识符”  。

  - **删除匹配的硬件设备**

    仅“按设备标识符安装硬件设备”设置为“阻止安装硬件设备”时，此设置才可用 。
    - **是**
    - 未配置

  - **已阻止的硬件设备标识符**

    仅“按设备标识符安装硬件设备”设置为“阻止安装硬件设备”时，此设置才可用 。

    选择“添加”，然后指定要阻止的硬件设备标识符。

## <a name="dma-guard"></a>DMA Guard

- **与内核 DMA 保护不兼容的外部设备的枚举**  
  CSP：[DmaGuard/DeviceEnumerationPolicy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  此策略可针对支持 DMA 的外部设备提供额外的安全保障。 它让用户能够更好地控制与 DMA 重新映射/设备内存隔离和沙盒不兼容但支持 DMA 的外部设备的枚举。
  
  仅当内核 DMA 保护受到支持且已由系统固件启用时，此策略才有效。 内核 DMA 保护是一项平台功能，在制造时系统必须支持该功能。 要检查系统是否支持内核 DMA 保护，查看 MSINFO32.exe 的“摘要”页中的“内核 DMA 保护”字段。

  - 未配置（默认）
  - 全部阻止
  - 全部允许

## <a name="endpoint-detection-and-response"></a>终结点检测和响应

有关以下设置的详细信息，请参阅 Windows 文档中的 [WindowsAdvancedThreatProtection](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp) CSP。

- **所有文件的示例共享**  
  CSP：[Configuration/SampleSharing](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  返回或设置 Microsoft Defender 高级威胁防护示例共享配置参数。  
  
  - **是**（默认）
  - 未配置

- **加快遥测报告频率**  
  CSP：[Configuration/TelemetryReportingFrequency](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  提高 Microsoft Defender 高级威胁防护遥测报告频率。  

  - **是**（默认）
  - 未配置

## <a name="firewall"></a>防火墙

有关详细信息，请参阅 Windows 文档中的 [Firewall CSP](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp)（防火墙 CSP）。

- **禁用有状态的文件传输协议(FTP)**  
  CSP：[MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)  

  - **是**（默认）
  - **未配置** - 防火墙将使用 FTP 来检查和筛选二级网络连接，这可能会导致防火墙规则被忽略。

- **安全关联在被删除之前可处于空闲状态的秒数**  
CSP：[MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  指定在网络流量不再可见后安全关联的保留时长。 如果未配置，则系统会在安全关联处于空闲状态 300 秒（默认值）后将其删除。
  
  该数字必须介于 300 到 3600 秒之间 。

- **预共享密钥编码**  
  CSP：[MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

   如果不需要 UTF-8，则最初可使用 UTF-8 对预共享密钥进行编码。 之后，设备用户可以选择另一种编码方法。

  - 未配置
  - **无**
  - UTF8（默认）

- **证书吊销列表 (CRL) 验证**  
  CSP：[MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

  指定证书吊销列表 (CRL) 验证的强制执行方法。  

  - **未配置**（默认）- 禁用 CRL 验证。
  - **无**
  - 尝试
  - **需要**

- **数据包排队**  
  CSP：[MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  指定如何针对 IPsec 隧道网关方案为加密接收和明文转发启用接收端上的软件缩放。 此设置可确保数据包顺序得到保留。

  - **未配置**（默认）- 数据包队列返回到客户端默认值，即禁用。
  - **禁用**
  - 对入站请求排队
  - 对出站请求排队
  - 对两者排队

- **专用防火墙配置文件**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067041)

  - **配置**（默认）
  - 未配置

  设置为“配置”时，可以配置以下其他设置。

  - **已阻止入站连接**  
    CSP：[/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **是**（默认）
    - 未配置

  - **需要针对多播广播的单播响应**  
    CSP：[/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **是**（默认）
    - 未配置

  - **需要隐藏模式**  
    CSP：[/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **是**（默认）
    - 未配置

  - **需要出站连接**  
    CSP：[/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **是**（默认）
    - 未配置

  - **已阻止入站通知**  
    CSP：[/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **是**（默认）
    - 未配置

  - **已合并来自组策略的全局端口规则**  
    CSP：[/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **是**（默认）
    - 未配置

  - **已阻止隐藏模式**  
    CSP：[/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **是**（默认）
    - 未配置

  - **防火墙已启用**  
    CSP：[/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - 未配置
    - **已阻止**
    - 允许（默认）

  - **未合并来自组策略的已授权的应用程序规则**  
    CSP：[/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **是**（默认）
    - 未配置

  - **未合并来自组策略的连接安全规则**  
    CSP：[/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **是**（默认）
    - 未配置

  - **需要传入流量**  
    CSP：[/Shielded](https://go.microsoft.com/fwlink/?linkid=872561)

    - **是**（默认）
    - 未配置

  - **未合并来自组策略的策略规则**  
    CSP：[/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **是**（默认）
    - 未配置

- **公共防火墙配置文件**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067143)

  - **配置**（默认）
  - 未配置

  设置为“配置”时，可以配置以下其他设置。

  - **已阻止入站连接**  
    CSP：[/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **是**（默认）
    - 未配置

  - **需要针对多播广播的单播响应**  
    CSP：[/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **是**（默认）
    - 未配置

  - **需要隐藏模式**  
    CSP：[/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **是**（默认）
    - 未配置

  - **需要出站连接**  
    CSP：[/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **是**（默认）
    - 未配置

  - **未合并来自组策略的已授权的应用程序规则**  
    CSP：[/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **是**（默认）
    - 未配置

  - **已阻止入站通知**  
    CSP：[/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **是**（默认）
    - 未配置

  - **已合并来自组策略的全局端口规则**  
    CSP：[/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **是**（默认）
    - 未配置

  - **已阻止隐藏模式**  
    CSP：[/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **是**（默认）
    - 未配置

  - **防火墙已启用**  
    CSP：[/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - 未配置
    - **已阻止**
    - 允许（默认）

  - **未合并来自组策略的连接安全规则**  
    CSP：[/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **是**（默认）
    - 未配置

  - **需要传入流量**  
    CSP：[/Shielded](https://go.microsoft.com/fwlink/?linkid=872561)

    - **是**（默认）
    - 未配置

  - **未合并来自组策略的策略规则**  
    CSP：[/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **是**（默认）
    - 未配置

- **防火墙配置文件域**  
  CSP：[2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2066796)

  - **需要针对多播广播的单播响应**  
    CSP：[/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

  - **未合并来自组策略的已授权的应用程序规则**  
    CSP：[/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **是**（默认）
    - 未配置  

  - **已阻止入站通知**  
    CSP：[/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **是**（默认）
    - 未配置

  - **已合并来自组策略的全局端口规则**  
    CSP：[/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **是**（默认）
    - 未配置

  - **已阻止隐藏模式**  
    CSP：[/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **是**（默认）
    - 未配置

  - **防火墙已启用**  
    CSP：[/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - 未配置
    - **已阻止**
    - 允许（默认）

  - **未合并来自组策略的连接安全规则**  
    CSP：[/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **是**（默认）
    - 未配置

  - **未合并来自组策略的策略规则**  
    CSP：[/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **是**（默认）
    - 未配置

## <a name="microsoft-defender"></a>Microsoft Defender

- **每日快速扫描运行时间**  
  CSP：[Defender/ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053&clcid=0x409)
  
   配置每日快速扫描的运行时间。 默认情况下，扫描运行时间设置为凌晨 2 点。

- **计划扫描开始时间**  
  
  默认情况下，此时间设置为凌晨 2 点。

- **配置计划扫描的低 CPU 优先级**  
  CSP：[Defender/EnableLowCPUPriority](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority)  

  -**是**（默认）
  - 未配置

- **阻止 Office 通信应用创建子进程**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=874499)  

  此 ASR 规则通过以下 GUID 进行控制：26190899-1602-49e8-8b27-eb1d0a1ce869。
  - **未配置** - 将还原 Windows 默认设置，即不阻止创建子进程。
  - **用户定义**
  - 启用（默认）- 阻止 Office 通信应用程序创建子进程。
  - 审核模式 - 引发 Windows 事件，而不是阻止子进程。

- **阻止 Adobe Reader 创建子进程**  
  [通过攻击面减少规则减少攻击面](https://go.microsoft.com/fwlink/?linkid=853979)  

  - **未配置** - 将还原 Windows 默认设置，即不阻止创建子进程。
  - **用户定义**
  - 启用（默认）- 阻止 Adobe Reader 创建子进程。
  - 审核模式 - 引发 Windows 事件，而不是阻止子进程。

- **扫描传入的电子邮件**  
  CSP：[Defender/AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052&clcid=0x409)

  - **是**（默认）- 扫描电子邮件邮箱和邮件文件（例如 PST、DBX、MNX、MIME 和 BINHEX）。
  - **未配置** - 设置返回到客户端默认设置，即不扫描电子邮件文件。

- **启用实时保护**  
  CSP：[Defender/AllowRealtimeMonitoring](https://go.microsoft.com/fwlink/?linkid=2114050&clcid=0x409)

  - **是**（默认）- 强制执行实时监视，并且用户无法将其禁用。
  - **未配置** - 设置返回到客户端默认设置，即启用，但用户可以对其进行更改。 要禁用实时监视，请使用自定义 URI。

- **已隔离的恶意软件的保留天数(0-90)**  
  CSP：[Defender/DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055&clcid=0x409)

  配置项在被删除前保留在隔离文件夹中的天数。 默认值为零 (0)，这会导致隔离的文件永远不会被删除。

- **Defender 系统扫描计划**  
  CSP：[Defender/ScheduleScanDay](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)

  计划 Defender 扫描设备的日期。 默认情况下，该扫描为“用户定义”，但可以设置为“每日”、一周中的某一天或“没有计划的扫描” 。

- **云保护超时的额外时间(0-50 秒)**  
  CSP：[Defender/CloudExtendedTimeout](https://go.microsoft.com/fwlink/?linkid=2113940&clcid=0x409)

  Defender 防病毒会自动阻止可疑文件 10 秒钟，使其可以扫描云中的文件以确保安全性。 使用此设置，最多可以将此超时值增加 50 秒。  默认情况下，超时时间设置为零 (0)。

- **在完全扫描期间扫描映射的网络驱动器**  
  CSP：[Defender/AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945&clcid=0x409)

  - **是**（默认）- 在完全扫描期间，包含映射的网络驱动器。
  - **未配置** - 客户端将返回到其默认设置，这将禁止对映射的网络驱动器进行扫描。

- **启用网络保护**  
  CSP：[Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939&clcid=0x409)
  
  - **是**（默认）- 阻止网络检查系统 (NIS) 中的签名检测到的恶意流量。
  - 未配置

- **扫描所有已下载的文件和附件**  
  CSP：[Defender/AllowIOAVProtection](https://go.microsoft.com/fwlink/?linkid=2113934&clcid=0x409)

  - **是**（默认）- 扫描所有已下载的文件和附件。 设置返回到客户端默认设置，即启用，但用户可以对其进行更改。 要禁用此设置，请使用自定义 URI。
  - **未配置** - 设置返回到客户端默认设置，即启用，但用户可以对其进行更改。 要禁用此设置，请使用自定义 URI。

::: zone-end
::: zone pivot="atp-april-2020"

- **阻止访问保护**  
  CSP：[Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **是**
  - **未配置**（默认）

::: zone-end
::: zone pivot="atp-march-2020"

- **阻止访问保护**  
  CSP：[Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **是**（默认）
  - 未配置

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **扫描浏览器脚本**  
  CSP：[Defender/AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054&clcid=0x409)

  - **是**（默认）- 强制实施 Microsoft Defender 脚本扫描功能，并且用户无法将其关闭。
  - **未配置** - 设置将还原为客户端默认设置，即启用脚本扫描，但用户可将其关闭。

- **阻止用户访问 Microsoft Defender 应用**  
  CSP：[Defender/AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043&clcid=0x409)

  - **是**（默认）- 无法访问 Microsoft Defender 用户界面 (UI)，并且会禁止通知
  - **未配置** 如果设置为“是”，则将无法访问 Windows Defender 用户界面 (UI)，并且会禁止通知。 如果设置为“未配置”，则设置将还原为客户端默认设置，此情况允许访问 UI 和通知

- **每次扫描允许的最大 CPU 使用率(0-100%)**  
  CSP：[Defender/AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046&clcid=0x409)

  指定要用于扫描的最大 CPU 量（百分比）。 默认值为 50。

- **扫描类型**  
  CSP：[Defender/ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045&clcid=0x409)

  - **用户定义**
  - **禁用**
  - **快速扫描**（默认）
  - **完全扫描**

- **输入检查安全智能更新的频率(0-24 小时)**  
  CSP：[Defender/SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936&clcid=0x409)

  指定检查更新签名的频率（以小时为单位）。 例如，如果值为 1，将每小时检查一次。 如果值为 2，将每隔两小时检查一次，依此类推。

  如果未定义任何值，设备将使用客户端默认值，即 8 小时。

- **Defender 示例提交同意**  
  CSP：[Defender/SubmitSamplesConsent](https://go.microsoft.com/fwlink/?linkid=2067131)

  检查 Microsoft Defender 中用户的同意级别是否可发送数据。 如果已获取所需同意，Microsoft Defender 会将其提交。 如果未获取（且用户已指定绝不要求），则发送数据前启动 UI 申请获取用户同意（当“云提供的保护”设置为“是”时 ）。

  - **自动发送安全示例**（默认）
  - **始终提示**
  - **从不发送**
  - **自动发送所有示例**

- **云提供的保护级别**  
  CSP：[CloudBlockLevel](https://go.microsoft.com/fwlink/?linkid=2113942)

  配置 Defender 防病毒在阻止和扫描可疑文件方面的积极程度。
  - **未配置**（默认值）- 默认的 Defender 阻止级别。
  - **高** - 主动阻止未知文件，同时针对客户端性能进行优化（误报的可能性更大）。
  - **超高** - 主动阻止未知文件，并应用额外的保护措施（可能影响客户端的性能）。
  - **零容差** - 阻止所有未知的可执行文件。

- **扫描存档文件**  
  CSP：[Defender/AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047&clcid=0x409)

  - **是**（默认）- 强制扫描存档文件（例如 ZIP 或 CAB 文件）。
  - **未配置** - 设置将还原为客户端默认设置，即扫描存档文件，但用户可以禁用扫描。

- **启用行为监视**  
  CSP：[Defender/AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048&clcid=0x409)

  - **是**（默认）- 强制执行行为监视，并且用户无法将其禁用。
  - **未配置** - 设置返回到客户端默认设置，即启用，但用户可以对其进行更改。 要禁用实时监视，请使用自定义 URI。
  
- **在完全扫描期间扫描可移动驱动器**  
  CSP：[Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946&clcid=0x409)

  - **是**（默认）- 在完全扫描期间，会扫描可移动驱动器（例如 U 盘）。
  - **未配置** - 设置返回到客户端默认设置，即扫描可移动驱动器，但用户可以禁用此扫描。
  
- **扫描网络文件**  
  CSP：[Defender/AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&clcid=0x409)

  - **是**（默认）- Microsoft Defender 扫描网络文件。
  - **未配置** - 客户端将返回到其默认设置，这将禁止对网络文件进行扫描。
  
- **Defender 可能不需要的应用操作**  
  CSP：[Defender/PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

  指定潜在有害应用程序 (PUA) 的检测级别。 当正在下载或尝试在设备上安装潜在有害软件时，Defender 会向用户发出警报。
  - **设备默认值**
  - **阻止**（默认）- 已阻止检测到的项，它们将与其他威胁一同显示在历史记录中。
  - **审核** - Defender 检测可能不需要的应用程序，但不执行任何操作。 可以通过在事件查看器中搜索 Defender 创建的事件，查看有关 Defender 将对其执行操作的应用程序的信息。

- **启用云提供的保护**  
  CSP：[AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  默认情况下，Windows 10 桌面版设备上的 Defender 将有关发现的任何问题的信息发送给 Microsoft。 Microsoft 分析该信息，详细了解影响你和其他客户的问题，并提供改进的解决方案。

  - **是**（默认）- 启用云提供的保护。  设备用户无法更改此设置。
  - **未配置** - 设置将还原为系统默认值。

- **阻止 Office 应用程序将代码注入其他进程**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=872974)

  此 ASR 规则通过以下 GUID 进行控制：75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **未配置** - 设置返回到 Windows 默认设置，即关闭。
  - **阻止**（默认）- 阻止 Office 应用程序将代码注入其他进程。
  - **审核模式** - 引发 Windows 事件，而不是阻止。

- **阻止 Office 应用程序创建可执行内容**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=872975)

  此 ASR 规则通过以下 GUID 进行控制：3B576869-A4EC-4529-8536-B80A7769E899
  - **未配置** - 设置返回到 Windows 默认设置，即关闭。
  - **阻止**（默认）- 阻止 Office 应用程序创建可执行内容。
  - **审核模式** - 引发 Windows 事件，而不是阻止。
  
- **阻止 JavaScript 或 VBScript 启动下载的可执行内容**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=872979)

   此 ASR 规则通过以下 GUID 进行控制：D3E037E1-3EB8-44C8-A917-57927947596D
  - **未配置** - 设置返回到 Windows 默认设置，即关闭。
  - **阻止**（默认）- Defender 阻止执行从 Internet 下载的 JavaScript 或 VBScript 文件。
  - **审核模式** - 引发 Windows 事件，而不是阻止。
  
- **启用网络保护**  
  CSP：[Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **未配置** - 设置返回到 Windows 默认设置，即禁用。
  - **用户定义**
  - **启用** - 为系统上的所有用户启用网络保护。
  - **审核模式**（默认）- 不阻止用户访问危险域，而是引发 Windows 事件。

- **阻止从 USB 运行不受信任和未签名的进程**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=874502)

  此 ASR 规则通过以下 GUID 进行控制：b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **未配置** - 设置返回到 Windows 默认设置，即关闭。
  - **阻止**（默认）- 阻止从 USB 驱动器运行的不受信任和未签名的进程。
  - **审核模式** - 引发 Windows 事件，而不是阻止。

- **阻止从 Windows 本地安全机构子系统 (lsass.exe) 中窃取凭据**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=874499)

  此 ASR 规则通过以下 GUID 进行控制：9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **未配置** - 设置返回到 Windows 默认设置，即关闭。
  - **用户定义**
  - **启用**（默认）- 阻止尝试通过 lsass.exe 窃取凭据。
  - **审核模式** - 不阻止用户访问危险域，而是引发 Windows 事件。

- **阻止从电子邮件和 Web 邮件客户端下载可执行内容**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=872980)

  - **未配置** - 设置返回到 Windows 默认设置，即关闭。
  - **阻止**（默认）- 阻止从电子邮件和 Web 邮件客户端下载可执行内容。
  - **审核模式** - 引发 Windows 事件，而不是阻止。

- **阻止所有 Office 应用程序创建子进程**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=872976)

  此 ASR 规则通过以下 GUID 进行控制：D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **未配置** - 设置返回到 Windows 默认设置，即关闭。
  - **阻止**（默认）
  - **审核模式** - 引发 Windows 事件，而不是阻止。

- **阻止执行可能经过模糊处理的脚本 (js/vbs/ps)**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=872978)

  此 ASR 规则通过以下 GUID 进行控制：5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **未配置** - 设置返回到 Windows 默认设置，即关闭。
  - **阻止**（默认）- Defender 将阻止执行经过模糊处理的脚本。
  - **审核模式** - 引发 Windows 事件，而不是阻止。

- **阻止来自 Office 宏的 Win32 API 调用**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=872977)

  此 ASR 规则通过以下 GUID 进行控制：92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **未配置** - 设置返回到 Windows 默认设置，即关闭。
  - **阻止**（默认）- 将阻止 Office 宏使用 Win32 API 调用。
  - **审核模式** - 引发 Windows 事件，而不是阻止。

## <a name="microsoft-defender-security-center"></a>Microsoft Defender 安全中心

- **阻止用户编辑 Exploit Guard 保护接口**  
  CSP：[WindowsDefenderSecurityCenter/DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **是**（默认）- 阻止用户更改 Microsoft Defender 安全中心的 exploit protection 设置区域。
  - **未配置** - 本地用户可以在 Exploit Protection 设置区域中进行更改。

## <a name="smart-screen"></a>SmartScreen

- **阻止用户忽略 SmartScreen 警告**  
  CSP：[SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

   此设置需要启用“对应用和文件强制实施 SmartScreen”设置。
  - **是**（默认）- SmartScreen 将不会显示一个让用户忽略警告并运行应用的选项。 将显示警告，但用户将能够绕过它。
  - **未配置** - 将设置返回到 Windows 默认设置，这允许用户重写。

- **仅需要应用商店中的应用**  

  - **是**（默认）
  - 未配置

- **启用 Windows SmartScreen**  
  CSP：[SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **是**（默认）- 强制所有用户使用 SmartScreen。
  - **未配置** - 将设置返回到 Windows 默认设置，即启用 SmartScreen，但用户可以更改此设置。 要禁用 SmartScreen，请使用自定义 URI。

## <a name="windows-hello-for-business"></a>Windows Hello 企业版

有关详细信息，请参阅 Windows 文档中的 [PassportForWork CSP](https://docs.microsoft.com/windows/client-management/mdm/passportforwork-csp)。

- **阻止 Windows Hello 企业版**  

   Windows Hello 企业版是一种取代密码、智能卡和虚拟智能卡登录 Windows 的替代方法。

  - **未配置** - 设备预配 Windows Hello 企业版，这是 Windows 默认设置。
  - **禁用**（默认）- 设备预配 Windows Hello 企业版。
  - **启用** - 设备不为任何用户预配 Windows Hello 企业版。

  设置为“禁用”时，可以配置以下设置：

  - **PIN 中的小写字母**  
    - **不允许**
    - **必需**
    - **允许**（默认）

  - **PIN 中的特殊字符**
    - **不允许**
    - **必需**
    - **允许**（默认）

  - **PIN 中的大写字母**
    - **不允许**
    - **必需**
    - **允许**（默认）

::: zone-end

## <a name="next-steps"></a>后续步骤

- [了解安全基线](security-baselines.md)
- [避免冲突](security-baselines.md#avoid-conflicts)
- [在 Intune 中对策略和配置文件进行故障排除](../configuration/troubleshoot-policies-in-microsoft-intune.md)