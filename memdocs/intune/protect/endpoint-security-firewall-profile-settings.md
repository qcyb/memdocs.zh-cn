---
title: Intune 终结点安全性防火墙设置 |Microsoft Docs
description: Microsoft Intune 中适用于 Windows 和 macOS 的终结点安全防火墙策略设置
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/28/2020
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
ms.openlocfilehash: 10d9320932e7835b8c2ecac46e35ea5a57375904
ms.sourcegitcommit: 42882de75c8a984ba35951b1165c424a7e0ba42e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89068127"
---
# <a name="firewall-policy-settings-for-endpoint-security-in-intune"></a>Intune 中终结点安全的防火墙策略设置

查看可以在 Intune 终结点安全节点防火墙策略的配置文件中作为[终结点安全策略](../protect/endpoint-security-policy.md)的一部分进行配置的设置。

受支持的平台和配置文件：

- **macOS**：
  - 配置文件：macOS 防火墙

- **Windows 10 及更高版本**：
  - 配置文件：**Microsoft Defender 防火墙**

## <a name="macos-firewall-profile"></a>macOS 防火墙配置文件

### <a name="firewall"></a>防火墙

以下设置配置为[适用于 macOS 防火墙的终结点安全策略](../protect/endpoint-security-firewall-policy.md)

- **启用防火墙**

  - **未配置**（默认）
  - **是** - 启用防火墙。
  
  设置为“是”时，可以配置以下设置。  

  - **阻止所有传入连接**

    - **未配置**（默认）
    - **是** - 阻止所有传入连接，DHCP、Bonjour 和 IPSec 等基本 Internet 服务需要的连接除外。 这会阻止所有共享服务。

  - **启用隐藏模式**

    - **未配置**（默认）
    -  - 防止计算机对探测请求做出响应。 计算机仍然会响应授权应用的传入请求。

  - **防火墙应用** 展开下拉列表选择“添加”，然后指定应用和应用的传入连接规则。
    - **允许传入的连接**
      - 未配置
      - 阻止
      - Allow

    - **程序包 ID** - ID 用于标识应用。 例如：com.apple.app

## <a name="microsoft-defender-firewall-profile"></a>Microsoft Defender 防火墙配置文件

### <a name="microsoft-defender-firewall"></a>Microsoft Defender 防火墙

以下设置配置为[适用于 Windows 10 防火墙的终结点安全策略](../protect/endpoint-security-firewall-policy.md)。

- **禁用有状态的文件传输协议(FTP)**  
  CSP：[MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)

  - **未配置**（默认）- 防火墙使用 FTP 来检查和筛选二级网络连接，这可能会导致防火墙规则被忽略。
  - **是**
  
- **安全关联在被删除之前可处于空闲状态的秒数**  
  CSP：[MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  指定一个介于 300 秒和 3600 秒之间的时间，作为网络流量不再可见后安全关联的保留时长。
  
  如果未指定任何值，则系统会在安全关联处于空闲状态 300 秒后将其删除。
  
- **预共享密钥编码**  
  CSP：[MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

  如果不需要 UTF-8，则最初可使用 UTF-8 对预共享密钥进行编码。 之后，设备用户可以选择另一种编码方法。

  - **未配置**（默认）
  - **无**
  - **UTF8**

- **防火墙 IP 秒免除允许邻域发现**  
  CSP：[MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **未配置**（默认）
  - **是** - 防火墙 IPsec 免除允许邻域发现。

- **防火墙 IP 秒免除允许 ICMP**  
  CSP：[MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **未配置**（默认）
  - **是** - 防火墙 IPsec 免除允许 ICMP。

- **防火墙 IP 秒免除允许路由器发现**  
  CSP：[MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **未配置**（默认）
  - **是** - 防火墙 IPsec 免除允许路由器发现。

- **防火墙 IP 秒免除允许 DHCP**  
  CSP：[MdmStore/Global/IPsecExempt](https://go.microsoft.com/fwlink/?linkid=872547)

  - **未配置**（默认）
  - **是** - 防火墙 IP 秒免除允许 DHCP

- **证书吊销列表 (CRL) 验证**  
  CSP：[MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

   指定证书吊销列表 (CRL) 验证的强制执行方法。
  - **未配置**（默认）- 客户端默认设置为禁用 CRL 验证。
  - **无**
  - 尝试
  - **需要**

- **要求键控模块仅忽略它们不支持的身份验证套件**  
  CSP：[MdmStore/Global/OpportunisticallyMatchAuthSetPerKM](https://go.microsoft.com/fwlink/?linkid=872550)

  - **未配置**（默认）
  - **是** - 键控模块忽略不受支持的身份验证套件。

- **数据包排队**  
  CSP：[MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  指定如何针对 IPsec 隧道网关方案为加密接收和明文转发启用接收端上的软件缩放。 这将确保数据包顺序得到保留。
  - **未配置**（默认）- 数据包队列将返回到客户端默认值，即禁用。
  - **禁用**
  - 对入站请求排队
  - 对出站请求排队
  - 对两者排队

- **为域网络启用 Microsoft Defender 防火墙**  
  CSP：[EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **未配置**（默认）- 客户端恢复默认值，即启用防火墙。
  - **是** - 已打开并强制实施适用于“域”网络类型的 Microsoft Defender 防火墙。
  - **否** - 禁用防火墙。

- **为专用网络启用 Microsoft Defender 防火墙**  
  CSP：[EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **未配置**（默认）- 客户端恢复默认值，即启用防火墙。
  - **是** - 已打开并强制实施适用于“专用”网络类型的 Microsoft Defender 防火墙。
  - **否** - 禁用防火墙。

- **为公用网络启用 Microsoft Defender 防火墙**  
  CSP：[EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

  - **未配置**（默认）- 客户端恢复默认值，即启用防火墙。
  - **是** - 已打开并强制实施适用于“公用”网络类型的 Microsoft Defender 防火墙。
  - **否** - 禁用防火墙。

<!-- Microsoft Defender Firewall rules added in 2005  -->

### <a name="microsoft-defender-firewall-rules"></a>Microsoft Defender 防火墙规则

此配置文件为预览版状态。

以下设置配置为[适用于 Windows 10 防火墙的终结点安全策略](../protect/endpoint-security-firewall-policy.md)。

#### <a name="windows-firewall-rule"></a>Windows 防火墙规则

- **Name**  
  指定规则的友好名称。 此名称将出现在规则列表中，以帮助你识别它。

- **描述**  
  提供规则的说明。

- **方向**  
  - **未配置**（默认）- 此规则默认为出站流量。
  - **OUT** - 此规则应用于出站流量。
  - **In** - 此规则应用于入站流量。

- **操作**  
  - **未配置**（默认）- 规则默认为允许流量。
  - **阻止** - 流量在配置的方向上被阻止。
  - **允许** - 在配置的方向上允许流量。

- **网络类型**  
  指定规则所属的网络类型。 你可以选择以下一个或多个选项。 如果未选择选项，则该规则将应用于所有网络类型。
  - **域**
  - **专用**
  - **公共**
  - 未配置

- **包系列名称**  
  [Get-AppxPackage](/previous-versions//hh856044(v=technet.10))

  可通过从 PowerShell 运行 Get-AppxPackage 命令来检索包系列名称。

- **文件路径**  
  CSP：[FirewallRules/FirewallRuleName/App/FilePath](/windows/client-management/mdm/firewall-csp#filepath)

  若要指定应用的文件路径，请在客户端设备上输入应用位置。 例如：`C:\Windows\System\Notepad.exe` 或 `%WINDIR%\Notepad.exe`

- **服务名称**  
  [FirewallRules/FirewallRuleName/App/ServiceName](/windows/client-management/mdm/firewall-csp#servicename)

  当服务（而不是应用程序）发送或接收流量时，使用 Windows 服务短名称。 通过从 PowerShell 运行 `Get-Service` 命令来检索服务短名称。

- **协议**  
  CSP：[FirewallRules/FirewallRuleName/Protocol](/windows/client-management/mdm/firewall-csp#protocol)

  指定此端口规则的协议。
  - 传输层协议（如 TCP(6) 和 UDP(17)）允许指定端口或端口范围 。
  - 对于自定义协议，请输入表示 IP 协议的 0 到 255 之间的数字 。
  - 如果未指定任何内容，则规则默认为“任何”。

- **接口类型**  
  指定规则所属的接口类型。 你可以选择以下一个或多个选项。 如果未选择选项，则该规则将应用于所有接口类型：
  - **远程访问**
  - **无线**
  - **局域网**
  - 未配置

- **授权的用户**  
  [FirewallRules/FirewallRuleName/LocalUserAuthorizationList](/windows/client-management/mdm/firewall-csp#localuserauthorizedlist)

  指定此规则的授权本地用户列表。 如果此策略中的服务名称设置为 Windows 服务，则无法指定授权用户列表。 如果未指定授权用户，则默认值为“所有用户”。

- **任何本地地址**  
  **未配置**（默认）- 使用以下设置“本地地址范围”*配置要支持的地址范围 。
  - **是** - 支持任何本地地址而不配置地址范围。

- **本地地址范围**  
  CSP：[FirewallRules/FirewallRuleName/LocalAddressRanges](/windows/client-management/mdm/firewall-csp#localaddressranges)  

  管理此规则的本地地址范围。 你可以：
  - 将一个或多个地址添加为该规则所涵盖的本地地址的逗号分隔列表。
  - 导入 .csv 文件，其中包含要用作本地地址范围的地址列表。
  - 将当前的本地地址范围列表导出为 .csv 文件。

  有效条目（令牌）包括以下选项：
  - **星号** - 星号 (\*) 指示任何本地地址。 如果存在星号，则星号必须是包含的唯一标记。
  - **子网** - 使用子网掩码或网络前缀表示法指定子网。 如果未指定子网掩码或网络前缀，则子网掩码默认为 255.255.255.255。
  - **有效 IPv6 地址**
  - **IPv4 地址范围** - IPv4 范围必须是“起始地址 - 结束地址”格式，不包含空格，其中的起始地址小于结束地址。
  - **IPv6 地址范围** - IPv6 范围必须是“起始地址 - 结束地址”格式，不包含空格，其中的起始地址小于结束地址。

  如果未指定任何值，则此设置默认为使用任何地址。

- **任何远程地址**  
  **未配置**（默认）- 使用以下设置“远程地址范围”*配置要支持的地址范围 。
  - **是** - 支持任何远程地址而不配置地址范围。

- **远程地址范围**  
  CSP：[FirewallRules/FirewallRuleName/RemoteAddressRanges](/windows/client-management/mdm/firewall-csp#remoteaddressranges)  

  管理此规则的远程地址范围。 你可以：
  - 将一个或多个地址添加为该规则所涵盖的远程地址的逗号分隔列表。
  - 导入 .csv 文件，其中包含要用作远程地址范围的地址列表。
  - 将当前的远程地址范围列表导出为 .csv 文件。

  有效条目（令牌）包括以下选项，不区分大小写：
  - **星号** - 星号(\*) 指示任何远程地址。 如果存在星号，则星号必须是包含的唯一标记。
  - **Defaultgateway**
  - **DHCP**
  - **DNS**
  - **WINS**
  - **Intranet** - 在运行 Windows 1809 或更高版本的设备上受支持。
  - **RmtIntranet** - 在运行 Windows 1809 或更高版本的设备上受支持。
  - **Ply2Renders** - 在运行 Windows 1809 或更高版本的设备上受支持。
  - **LocalSubnet** - 表示本地子网上的任何本地地址。
  - **子网** - 使用子网掩码或网络前缀表示法指定子网。 如果未指定子网掩码或网络前缀，则子网掩码默认为 255.255.255.255。
  - **有效 IPv6 地址**
  - **IPv4 地址范围** - IPv4 范围必须是“起始地址 - 结束地址”格式，不包含空格，其中的起始地址小于结束地址。
  - **IPv6 地址范围** - IPv6 范围必须是“起始地址 - 结束地址”格式，不包含空格，其中的起始地址小于结束地址。

  如果未指定任何值，则此设置默认为使用任何地址。

<!-- End of 2005 additions  -->

## <a name="next-steps"></a>后续步骤

[防火墙的终结点安全策略](../protect/endpoint-security-firewall-policy.md)