---
title: Intune 终结点安全攻击面减少设置 | Microsoft Docs
description: Microsoft Intune 中的终结点安全攻击面减少策略设置
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 3ebca81f459f0e49345db08f992c288514a7331a
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461600"
---
# <a name="attack-surface-reduction-policy-settings-for-endpoint-security-in-intune"></a>Intune 终结点安全的攻击面减少策略设置

查看可以在 Intune 终节点安全节点“攻击面减少”策略的配置文件中作为[终结点安全策略](../protect/endpoint-security-policy.md)的一部分配置的设置。

受支持的平台和配置文件：

- **Windows 10 及更高版本**：
  - 配置文件：**应用和浏览器隔离**
  - 配置文件：**Web 保护**
  - 配置文件：**应用程序控制**
  - 配置文件：**攻击面减少规则**
  - 配置文件：**设备控制**
  - 配置文件：**Exploit protection**

## <a name="app-and-browser-isolation-profile"></a>应用和浏览器隔离配置文件

### <a name="app-and-browser-isolation"></a>应用和浏览器隔离

- **启用 Edge 应用程序防护（选项）**  
  CSP：[AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)

  - **未配置**（默认）
  - **为 Microsoft Edge 启用** - 应用程序防护将在通过 Hyper-V 虚拟化的浏览容器中打开未受批准的站点。

  设置为“为 Microsoft Edge 启用”时，可使用以下设置：
  
  - **剪贴板行为**  
    CSP：[ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    选择可以从本地电脑和应用程序防护虚拟浏览器中执行的复制和粘贴操作。
    - **未配置**（默认）
    - **阻止在电脑和浏览器之间进行复制和粘贴**
    - **仅允许从浏览器复制和粘贴到电脑**
    - **仅允许从电脑复制和粘贴到浏览器**
    - **允许在电脑和浏览器之间进行复制和粘贴**

  - **阻止来自非企业认可网站的外部内容**  
    CSP：[BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **未配置**（默认）
    - **是** - 阻止加载未经批准的网站中的内容。

  - **收集应用程序防护浏览会话内发生的事件的日志**  
    CSP：[AuditApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872418)

    - **未配置**（默认）
    - **是** - 收集应用程序防护虚拟浏览会话内发生的事件的日志。

  - **允许保存用户生成的浏览器数据**  
    CSP：[AllowPersistence](https://go.microsoft.com/fwlink/?linkid=872419)

    - **未配置**（默认）
    - **是** - 允许保存在应用程序防护虚拟浏览会话期间创建的用户数据。 用户数据的示例包括密码、收藏夹和 Cookie。

  - **启用硬件图形加速**  
    CSP：[AllowVirtualGPU](https://go.microsoft.com/fwlink/?linkid=872420)

    - **未配置**（默认）
    - **是** - 在应用程序防护虚拟浏览会话中，使用虚拟图形处理单元更快地加载图形密集型网站。

  - **允许用户将文件下载到主机上**  
    CSP：[SaveFilesToHost](https://go.microsoft.com/fwlink/?linkid=872421)

    - **未配置**（默认）
    - **是** - 允许用户将文件从虚拟浏览器下载到主机操作系统上。

- **应用程序防护允许打印到本地打印机**  

  - **未配置**（默认）
  - **是** - 允许打印到本地打印机。

- **应用程序防护允许打印到网络打印机**  

  - **未配置**（默认）
  - **是** - 允许打印到网络打印机。

- **应用程序防护允许打印为 PDF**  

  - **未配置**（默认）
  - **是** - 允许打印为 PDF。

- **应用程序防护允许打印为 XPS**  

  - **未配置**（默认）
  - **是** - 允许打印为 XPS。

- **Windows 网络隔离策略**  
  
  - **未配置**（默认）
  - **是** - 配置 Windows 网络隔离策略。  
  
  设置为“是”时，可以配置以下设置。

  - **IP 范围**  
    展开下拉列表，选择“添加”，然后依次指定下层地址和上层地址 。

  - **云资源**  
    展开下拉列表，选择“添加”，然后指定 IP 地址或 FQDN 和代理 。

  - **网络域**  
   展开下拉列表，选择“添加”，然后指定网络域。

  - **代理服务器**  
    展开下拉列表，选择“添加”，然后指定代理服务器。

  - **内部代理服务器**  
    展开下拉列表，选择“添加”，然后指定内部代理服务器。

  - **非特定资源**  
    展开下拉列表，选择“添加”，然后指定非特定资源。

  - **禁止自动检测其他企业代理服务器**  
    - **未配置**（默认）
    - **是** - 禁止自动检测其他企业代理服务器。

  - **禁止自动检测其他企业 IP 范围**  
    - **未配置**（默认）
    - **是** - 禁止自动检测其他企业 IP 范围。

## <a name="web-protection-profile"></a>Web 保护配置文件

### <a name="web-protection"></a>Web 保护

- **启用网络保护**  
  CSP：[EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **未配置**（默认）- 设置将还原为 Windows 默认设置，即禁用。
  - **用户定义**
  - **启用** - 为系统上的所有用户启用网络保护。
  - **审核模式** - 不阻止用户访问危险域，而是引发 Windows 事件。

- **Microsoft Edge SmartScreen**  
  CSP：[Browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **是** - 使用 SmartScreen 防止用户受潜在网络钓鱼诈骗和恶意软件侵袭。
  - **未配置**（默认）

- **阻止恶意网站访问**  
  CSP：[Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **是** - 阻止用户忽略 Microsoft Defender SmartScreen 筛选器警告并阻止他们访问该站点。
  - **未配置**（默认）

- **阻止下载未经验证的文件**  
  CSP：[Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **是** - 阻止用户忽略 Microsoft Defender SmartScreen 筛选器警告并阻止他们下载未经验证的文件。
  - **未配置**（默认）

## <a name="application-control-profile"></a>应用程序控制配置文件

### <a name="microsoft-defender-application-control"></a>Microsoft Defender 应用程序控制

- **App Locker 应用程序控件**  
  - **未配置**（默认）
  - **强制使用组件和应用商店应用**
  - **审核组件和应用商店应用**
  - **强制使用组件、应用商店应用和 Smartlocker**
  - **审核组件、应用商店应用和 Smartlocker**

- **阻止用户忽略 SmartScreen 警告**  
  [PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

  - **未配置**（默认）- 用户可以忽略针对文件和恶意应用的 SmartScreen 警告。
  - **是** - 启用 SmartScreen，且用户无法绕过针对文件或恶意应用的警告。

- **启用 Windows SmartScreen**  
  CSP：[SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **未配置**（默认）- 设置将还原为 Windows 默认设置，即启用 SmartScreen，但用户可以更改此设置。 要禁用 SmartScreen，请使用自定义 URI。
  - **是** - 强制所有用户使用 SmartScreen。

## <a name="attack-surface-reduction-rules-profile"></a>攻击面减少规则配置文件

### <a name="attack-surface-reduction-rules"></a>攻击面减少规则

- **阻止从 Windows 本地安全机构子系统 (lsass.exe) 中窃取凭据**  
  <!-- Defender ATP security baseline, Device configuration Endpoint protection profile -->
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=874499)

  此攻击面减少 (ASR) 规则通过以下 GUID 进行控制：9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **未配置**（默认）- 设置将还原为 Windows 默认设置，即关闭。
  - **用户定义**
  - **启用** - 阻止尝试通过 lsass.exe 窃取凭据。
  - **审核模式** - 不阻止用户访问危险域，而是引发 Windows 事件。

- **阻止 Adobe Reader 创建子进程**  
  [通过攻击面减少规则减少攻击面](https://go.microsoft.com/fwlink/?linkid=853979)
  
  此 ASR 规则通过以下 GUID 进行控制：7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c
  - **未配置**（默认）- 设置将还原为 Windows 默认设置，即不阻止创建子进程。
  - **用户定义**
  - **启用** - 阻止 Adobe Reader 创建子进程。
  - 审核模式 - 引发 Windows 事件，而不是阻止子进程。

- **阻止 Office 应用程序将代码注入其他进程**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=872974)

  此 ASR 规则通过以下 GUID 进行控制：75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **未配置**（默认）- 设置将还原为 Windows 默认设置，即关闭。
  - **阻止** - 阻止 Office 应用程序将代码注入其他进程。
  - **审核模式** - 引发 Windows 事件，而不是阻止。

- **阻止 Office 应用程序创建可执行内容**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=872975)

  此 ASR 规则通过以下 GUID 进行控制：3B576869-A4EC-4529-8536-B80A7769E899
  - **未配置**（默认）- 设置将还原为 Windows 默认设置，即关闭。
  - **阻止** - 阻止 Office 应用程序创建可执行内容。
  - **审核模式** - 引发 Windows 事件，而不是阻止。

- **阻止所有 Office 应用程序创建子进程**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=872976)

  此 ASR 规则通过以下 GUID 进行控制：D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **未配置**（默认）- 设置将还原为 Windows 默认设置，即关闭。
  - **阻止** - 阻止 Office 应用程序创建子进程。
  - **审核模式** - 引发 Windows 事件，而不是阻止。

- **阻止来自 Office 宏的 Win32 API 调用**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=872977)

  此 ASR 规则通过以下 GUID 进行控制：92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **未配置**（默认）- 设置将还原为 Windows 默认设置，即关闭。
  - **阻止** - 阻止 Office 宏使用 Win32 API 调用。
  - **审核模式** - 引发 Windows 事件，而不是阻止。

- **阻止 Office 通信应用创建子进程**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=874499)  

  此 ASR 规则通过以下 GUID 进行控制：26190899-1602-49e8-8b27-eb1d0a1ce869。
  - **未配置**（默认）- 设置将还原为 Windows 默认设置，即不阻止创建子进程。
  - **用户定义**
  - **启用** - 阻止 Office 通信应用程序创建子进程。
  - 审核模式 - 引发 Windows 事件，而不是阻止子进程。

- **阻止执行可能经过模糊处理的脚本 (js/vbs/ps)**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=872978)

  此 ASR 规则通过以下 GUID 进行控制：5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **未配置**（默认）- 设置将还原为 Windows 默认设置，即关闭。
  - **阻止** - Defender 阻止执行经过模糊处理的脚本。
  - **审核模式** - 引发 Windows 事件，而不是阻止。

- **阻止 JavaScript 或 VBScript 启动下载的可执行内容**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=872979)

   此 ASR 规则通过以下 GUID 进行控制：D3E037E1-3EB8-44C8-A917-57927947596D
  - **未配置**（默认）- 设置将还原为 Windows 默认设置，即关闭。
  - **阻止** - Defender 阻止执行从 Internet 下载的 JavaScript 或 VBScript 文件。
  - **审核模式** - 引发 Windows 事件，而不是阻止。

- **阻止来自 PSExec 和 WMI 命令的进程创建**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=874500)

  此 ASR 规则通过以下 GUID 进行控制：d1e49aac-8f56-4280-b9ba-993a6d77406c
  - **未配置**（默认）- 设置将还原为 Windows 默认设置，即关闭。
  - **阻止** - 阻止 PSExec 或 WMI 命令创建进程。
  - **审核模式** - 引发 Windows 事件，而不是阻止。

- **阻止从 USB 运行不受信任和未签名的进程**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=874502)

  此 ASR 规则通过以下 GUID 进行控制：b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **未配置**（默认）- 设置将还原为 Windows 默认设置，即关闭。
  - **阻止** - 阻止从 USB 驱动器运行的不受信任和未签名的进程。
  - **审核模式** - 引发 Windows 事件，而不是阻止。

- **阻止运行可执行文件，除非它们符合传播、年龄或受信任列表条件**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=874503)

  此 ASR 规则通过以下 GUID 进行控制：01443614-cd74-433a-b99e-2ecdc07bfc25e
  - **未配置**（默认）- 设置将还原为 Windows 默认设置，即关闭。
  - **阻止**
  - **审核模式** - 引发 Windows 事件，而不是阻止。

- **阻止从电子邮件和 Web 邮件客户端下载可执行内容**  
  [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=872980)

  - **未配置**（默认）- 设置将还原为 Windows 默认设置，即关闭。
  - **阻止** - 阻止从电子邮件和 Web 邮件客户端下载的可执行内容。
  - **审核模式** - 引发 Windows 事件，而不是阻止。

- **启用针对勒索软件的高级防护**  
   [保护设备免遭攻击](https://go.microsoft.com/fwlink/?linkid=874504)

  此 ASR 规则通过以下 GUID 进行控制：c1db55ab-c21a-4637-bb3f-a12568109d35
  - **未配置**（默认）- 设置将还原为 Windows 默认设置，即关闭。
  - **用户定义**
  - **启用**
  - **审核模式** - - 引发 Windows 事件，而不是阻止。

- **启用文件夹保护**  
  CSP：[EnableControlledFolderAccess](https://go.microsoft.com/fwlink/?linkid=872614)

  - **未配置**（默认）- 此设置还原为默认设置，即不阻止读取或写入操作。
  - **启用** - 对于不受信任的应用，Defender 阻止尝试修改或删除受保护文件夹中的文件，或写入磁盘扇区的操作。 Defender 自动确定可以信任哪些应用程序。 或者，你可以定义自己的受信任应用程序列表。
  - **审核模式** - 当不受信任的应用程序访问受控文件夹时，将引发 Windows 事件，但不会强制执行任何阻止。
  - **阻止磁盘修改** - 仅阻止尝试写入磁盘扇区的操作。
  - **审核磁盘修改** - 引发 Windows 事件，而不是阻止尝试写入磁盘扇区。
  
- **从攻击面减少规则中排除文件和路径**  
  CSP：[AttackSurfaceReductionOnlyExclusions](https://go.microsoft.com/fwlink/?linkid=872981)

  展开下拉列表，然后选择“添加”，定义要从攻击面减少规则中排除的文件或文件夹的“路径” 。

## <a name="device-control-profile"></a>设备控制配置文件

### <a name="device-control"></a>设备控制

- **按设备标识符安装硬件设备**  
  [PreventInstallationOfMatchingDeviceIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  使用此设置可以指定禁止 Windows 安装的设备的即插即用硬件 ID 和兼容 ID 的列表。 此策略设置优先于任何其他允许 Windows 安装设备的策略设置。  如果在某个远程桌面服务器上启用了此策略设置，则此策略设置会影响指定设备从远程桌面客户端到该远程桌面服务器的重定向。

  - 未配置
  - 允许安装硬件设备 - 可根据其他允许或禁止策略设置来安装和更新设备。
  - 阻止安装硬件设备（默认）- 禁止 Windows 安装你所定义的列表中列出了其硬件 ID 或兼容 ID 的设备。

  设置为“阻止安装硬件设备”时，可以配置以下设置：

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

- **在完全扫描期间扫描可移动驱动器**  
  CSP：[Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946)

  - **未配置**（默认）- 设置将还原为客户端默认设置，即扫描可移动驱动器，但用户可以禁用此扫描。
  - **是** - 在完全扫描期间，会扫描可移动驱动器（例如 U 盘）。

- **阻止直接内存访问**  
  CSP：[DataProtection/AllowDirectMemoryAccess](https://go.microsoft.com/fwlink/?linkid=2067031)

  只在启用了 BitLocker 或设备加密时才执行此策略设置。

  - **未配置**（默认）
  - “是”- 阻止所有热插拔 PCI 下游端口的直接内存访问 (DMA)，直到用户登录 Windows。 用户登录后，Windows 会枚举连接到热插拔 PCI 端口的 PCI 设备。 用户每次锁定计算机都会阻止无子设备的热插拔 PCI 端口进行 DMA，直到用户再次登录。 解锁机器时已经枚举的设备将继续起作用，直到拔出插头为止。

- **与内核 DMA 保护不兼容的外部设备的枚举**  
  CSP：[DmaGuard/DeviceEnumerationPolicy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  此策略可针对支持 DMA 的外部设备提供额外的安全保障。 它让用户能够更好地控制与 DMA 重新映射/设备内存隔离和沙盒不兼容但支持 DMA 的外部设备的枚举。

  仅当内核 DMA 保护受到支持且已由系统固件启用时，此策略才有效。 内核 DMA 保护是一项平台功能，在制造时系统必须支持该功能。 要检查系统是否支持内核 DMA 保护，查看 MSINFO32.exe 的“摘要”页中的“内核 DMA 保护”字段。

  - 未配置（默认）
  - 全部阻止
  - 全部允许

- **阻止蓝牙连接**  
  CSP：[Bluetooth/AllowDiscoverableMode](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

  - **未配置**（默认）
  - “是”- 阻止与设备进行蓝牙连接。

- **阻止蓝牙可发现性**  
  CSP：[Bluetooth/AllowDiscoverableMode](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

  - **未配置**（默认）
  - “是”- 防止其他启用蓝牙的设备发现该设备。

- **阻止蓝牙预配对**  
  CSP：[Bluetooth/AllowPrepairing](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowprepairing)

  - **未配置**（默认）
  - “是”- 阻止特定的蓝牙设备自动与主机设备配对。

- **阻止蓝牙广告**  
  CSP：[Bluetooth/AllowAdvertising](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

  - **未配置**（默认）
  - “是”- 阻止设备发送蓝牙广告。  

- **阻止蓝牙近端连接**  
  CSP：[Bluetooth/AllowPromptedProximalConnections](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections) 阻止用户使用 Swift Pair 和其他基于邻近的场景

  - **未配置**（默认）
  - “是”- 阻止设备用户使用 Swift Pair 和其他基于邻近的场景。  

  [Bluetooth/AllowPromptedProximalConnections CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections)

- **蓝牙允许的服务**  
  CSP：[Bluetooth/ServicesAllowedList](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-servicesallowedlist)  
  有关服务列表的更多详细信息，请参阅 [ServicesAllowedList 使用指南](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-bluetooth#servicesallowedlist-usage-guide)

  - “添加”- 将允许的蓝牙服务和配置文件指定为十六进制字符串，例如 `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`。
  - “导入”- 导入一个 .csv 文件，该文件包含一个蓝牙服务和配置文件列表作为十六进制字符串，例如 `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`

## <a name="exploit-protection-profile"></a>Exploit Protection 配置文件

### <a name="exploit-protection"></a>Exploit Protection

- **上传 XML**  
  CSP：[ExploitProtectionSettings](https://go.microsoft.com/fwlink/?linkid=2067035)

  使 IT 管理员能够将表示所需系统和应用程序缓解选项的配置推送到组织中的所有设备。 配置由 XML 文件表示。 Exploit Protection 有助于保护设备免受利用攻击进行传播的恶意软件的侵袭。 使用 Windows 安全性应用或 PowerShell 来创建一组缓解方案（称为配置）。 然后，可将此配置导出为 XML 文件，并与网络中的多台计算机共享，使其全部拥有相同的一组缓解设置。 此外，还可将现有的 EMET 配置 XML 文件转换为和导入到 Exploit Protection 配置 XML。

  选择“选择 XML 文件”，指定 XML 文件上传，然后单击“选择” 。
  - **未配置**（默认）
  - **是**

- **阻止用户编辑 Exploit Guard 保护接口**  
  CSP：[DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **未配置**（默认）- 本地用户可以在 Exploit Protection 设置区域中进行更改。
  - **是** - 阻止用户更改 Microsoft Defender 安全中心的 Exploit Protection设置区域。

## <a name="next-steps"></a>后续步骤

[ASR 的终结点安全策略设置](../protect/endpoint-security-asr-policy.md)
