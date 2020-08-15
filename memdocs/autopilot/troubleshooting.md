---
title: Windows Autopilot 故障排除
description: 了解如何处理 Windows Autopilot 部署过程中出现的问题。
keywords: mdm, 设置, windows, windows 10, oobe, 管理, 部署, autopilot, ztd, 零接触, 合作伙伴, msfb, intune
ms.reviewer: mniehaus
manager: laurawi
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: c89731edddd94da99e114cf98c10547c096ebb53
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252010"
---
# <a name="troubleshooting-windows-autopilot"></a>Windows Autopilot 故障排除

**适用于： Windows 10**

Windows Autopilot 旨在简化 Windows 设备生命周期的所有部分，但有时会出现问题。 查看以下信息，以帮助进行故障排除。

## <a name="troubleshooting-process"></a>疑难解答过程

无论是执行用户驱动的还是自行部署的设备部署，故障排除过程都是一样的。 了解特定设备的流程很有用：

1. 建立网络连接。 该连接可以是无线 (Wi-fi) 或有线 (以太网) 连接。
2. 已下载 Windows Autopilot 配置文件。 当你使用有线连接或手动建立无线连接时，配置文件将在网络连接到位时立即从 Autopilot 部署服务下载。
3. 用户身份验证发生。 当执行用户驱动的部署时，用户将输入其 Azure Active Directory 凭据，将对其进行验证。
4. Azure Active Directory 联接。 对于用户驱动的部署，使用指定的用户凭据将设备加入到 Azure AD。 对于自行部署方案，设备将加入，无需指定任何用户凭据。
5. 自动进行 MDM 注册。 作为 Azure AD 联接过程的一部分，设备将在 Azure AD 中配置的 MDM 服务 (例如，Microsoft Intune) 。
6. 应用设置。 如果配置了 " [注册状态" 页](enrollment-status.md) ，则将在显示 "注册状态" 页时应用大多数设置。 如果未配置或不可用，则将在用户登录后应用设置。

对于疑难解答，要执行的关键活动是：

- 配置：有 Azure Active Directory 和 Microsoft Intune (，或者) 按照 [Windows Autopilot 配置要求](configuration-requirements.md)中的规定配置了等效的 MDM 服务？
- 网络连接：设备是否可以访问 [Windows Autopilot 网络要求](networking-requirements.md)中所述的服务？
- Autopilot 现成 (OOBE) 行为：是否只显示了预期的现成体验屏幕？ Azure AD 凭据页是否已根据预期的特定于组织的详细信息进行了自定义？
- Azure AD 联接问题：设备是否能够加入 Azure Active Directory？
- MDM 注册问题：设备是否能够) 注册 Microsoft Intune (或等效的 MDM 服务？

## <a name="troubleshooting-autopilot-device-import"></a>Autopilot 设备导入疑难解答

### <a name="clicking-import-after-selecting-csv-does-nothing-400-error-appears-in-network-trace-with-error-body-cannot-convert-the-literal-devicehash-to-the-expected-type-edmbinary"></a>选择 CSV 后单击 "导入" 不执行任何操作，出现 "400" 错误，出现在错误正文的网络跟踪中 **"无法将文本 ' [DEVICEHASH] ' 转换为所需的类型 ' Edm"。**

此错误指向设备哈希的格式不正确。 损坏所收集哈希的任何内容都会导致此错误。 一种可能的情况是哈希本身 (即使其有效) 未能解码也是如此。

设备哈希为 Base64。 在设备级别，其编码为未填充 Base64，但 Autopilot 需要填充的 Base64。 通常情况下，负载不需要填充，并且该过程将起作用。 但是，有时负载并不完全对齐，并且需要填充。 在这种情况下，你将收到上面显示的错误。 PowerShell 的 Base64 解码器还需要使用已填充的 Base64，因此，我们可以使用此解码器来验证是否已正确填充哈希。

哈希末尾的 "A" 字符实际上是空的数据。 Base64 中的每个字符都是6位，在 Base64 中为6位等于0。 在结尾删除 **或添加将**不会更改实际有效负载数据。

若要解决此问题，我们需要修改哈希值，然后测试新值，直到 PowerShell 成功解码哈希。 结果很难以辨认，这很好。 我们只是找不到该错误，这不会引发错误 "为64字符数组或字符串的长度无效"。 

若要测试 base64，可以使用以下 PowerShell：
```powershell
[System.Text.Encoding]::ascii.getstring( [System.Convert]::FromBase64String("DEVICE HASH"))
```

因此，作为一个示例 (这不是设备哈希，而是未填充的 Base64，因此它非常适合测试) ：
```powershell
[System.Text.Encoding]::ascii.getstring( [System.Convert]::FromBase64String("Q29udG9zbwAAA"))
```

现在为填充规则提供。 填充字符为 "="。 填充字符只能位于哈希的末尾，并且最多只能有两个填充字符。 下面是基本逻辑。

- 解码哈希失败了吗？
 - 是：是否为最后两个字符 "="？
   - 是：将 "=" 替换为单个 "A" 字符，然后重试
   - 否：在末尾添加另一个 "=" 字符，然后重试
 - 否：哈希有效

在上面的示例哈希上循环遍历以上逻辑，我们将获得以下排列：
- Q29udG9zbwAAA
- Q29udG9zbwAAA =
- Q29udG9zbwAAA = =
- Q29udG9zbwAAAA
- Q29udG9zbwAAAA =
- **Q29udG9zbwAAAA = =** (此项具有有效的空白) 

将收集的哈希替换为此新填充的哈希，然后重试导入。

## <a name="troubleshooting-autopilot-oobe-issues"></a>解决 Autopilot OOBE 问题

当 OOBE 包含意外的 Autopilot 行为时，检查设备是否接收到 Autopilot 配置文件会很有用。 如果是这样，请检查配置文件包含的设置。 可以使用不同的机制来执行此操作，具体取决于 Windows 10 版本。

### <a name="windows-10-version-1803-and-above"></a>Windows 10 版本1803及更高版本

Windows 10 版本1803及更高版本添加了事件日志条目。 可以使用 og 项来查看与 Autopilot 配置文件设置和 OOBE 流相关的详细信息。 可以使用事件查看器查看这些条目。 查看 **应用程序和服务日志中的信息– > Microsoft – > Windows – > 预配-诊断-提供** 程序-在1903之前的版本 > Autopilot。 对于版本1903及更高版本，请参阅 **应用程序和服务日志– > Microsoft – > Windows – > ModernDeployment – > Autopilot**。 根据方案和配置文件的配置，可能会记录以下事件：

| 事件 ID | 类型 | 说明 |
|----------|------|-------------| 
| 100 | 警告 | "找不到 Autopilot 策略 [名称]。" 此错误通常是暂时性的问题，而设备正在等待下载 Autopilot 配置文件。 |
| 101 | 信息 | "AutopilotGetPolicyDwordByName succeeded： policy name = [setting name];策略值 = [值]。 " 此消息显示 Autopilot 检索和处理数值 OOBE 设置。 |
| 103 | 信息 | "AutopilotGetPolicyStringByName 已成功：策略名称 = [名称];值 = [值]。 " 此消息显示 Autopilot 检索和处理 OOBE 设置字符串，例如 Azure AD 租户名称。 |
| 109 | 信息 | "AutopilotGetOobeSettingsOverride succeeded： OOBE 设置 [设置名称];状态 = [状态]。 此消息显示 Autopilot 检索和处理与状态相关的 OOBE 设置。 |
| 111 | 信息 | "AutopilotRetrieveSettings 成功。" 此消息表示已成功检索到控制 OOBE 行为的 Autopilot 配置文件中存储的设置。 |
| 153 | 信息 | "AutopilotManager 报告状态已从 [原始状态] 改为 [新状态]。" 通常，此消息应显示 "ProfileState_Unknown" 到 "ProfileState_Available"。 这种情况表示配置文件已可用，并且已为该设备下载。 因此，设备已准备好使用 Autopilot 进行部署。 |
| 160 | 信息 | "AutopilotRetrieveSettings 开始购置"。 此消息显示 Autopilot 正在准备下载所需的 Autopilot 配置文件设置。 |
| 161 | 信息 | "AutopilotManager 检索设置成功。" 已成功下载 Autopilot 配置文件。 |
| 163 | 信息 | "AutopilotManager 确定不需要下载并且设备已预配。 清除或重置设备以更改此设置。 " 此消息表示设备上有 Autopilot 配置文件;它通常仅由 **Sysprep/Generalize** 进程删除。 |
| 164 | 信息 | "AutopilotManager 确定 Internet 可用于尝试下载策略。" |
| 171 | 错误 | "AutopilotManager 未能设置 TPM 标识确认。 HRESULT = [错误代码]。 " 此消息表示执行 TPM 证明的问题，该问题是完成自我部署模式进程所必需的。 | 
| 172 | 错误 | "AutopilotManager 未能将 Autopilot 配置文件设置为可用。 HRESULT = [错误代码]。 " 此错误通常与事件 ID 171 相关。 |

除了事件日志条目，以下注册表和 ETW 跟踪选项还适用于 Windows 10 版本1803及更高版本。

### <a name="windows-10-version-1709-and-above"></a>Windows 10 版本1709及更高版本

从 Autopilot 部署服务收到的 Autopilot 配置文件设置存储在设备的注册表中。 此信息可在 **HKLM\SOFTWARE\Microsoft\Provisioning\Diagnostics\Autopilot**上找到。 可用的注册表项包括：

| 值 | 描述 |
|-------|-------------|
| AadTenantId | 用户登录到的 Azure AD 租户的 GUID。 如果此条目与用于注册设备的租户不匹配，则用户会收到错误。 |
| CloudAssignedTenantDomain | 已注册设备的 Azure AD 租户，例如 "contosomn.onmicrosoft.com"。 如果设备未注册到 Autopilot，此值将为空。 |
| CloudAssignedTenantId | 注册了设备的 Azure AD 租户的 GUID。 GUID 对应于 CloudAssignedTenantDomain 注册表值中的租户域。 如果设备未注册到 Autopilot，此值将为空。|
| IsAutopilotDisabled | 如果设置为1，则此注册表值表示设备未注册到 Autopilot。 此状态也可能指示无法下载 Autopilot 配置文件，因为网络连接或防火墙问题或网络超时。 |
| TenantMatched | 如果用户的租户 ID 与设备注册到的租户 ID 匹配，则此项设置为1。 如果此注册表值为0，则用户将显示错误并强制重新开始。 |
| CloudAssignedOobeConfig | 显示配置了哪些 Autopilot 设置的位图。 值包括： SkipCortanaOptIn = 1、OobeUserNotLocalAdmin = 2、SkipExpressSettings = 4、SkipOemRegistration = 8、SkipEula = 16 |

### <a name="windows-10-semi-annual-channel-supported-versions"></a>Windows 10 半年频道支持的版本

在运行 [受支持版本](https://docs.microsoft.com/windows/release-information/) 的 Windows 10 半年频道的设备上，可以使用 ETW 跟踪从 Autopilot 和相关组件获取详细信息。 可以使用 Windows 性能分析器或类似工具查看 ETW 跟踪文件。 有关详细信息，请参阅 [高级疑难解答博客](https://blogs.technet.microsoft.com/mniehaus/2017/12/13/troubleshooting-windows-autopilot-level-300400/)。

## <a name="troubleshooting-azure-ad-join-issues"></a>解决 Azure AD 联接问题

将设备加入 Azure AD 最常见的问题是与 Azure AD 权限相关。 请确保 [正确配置已准备就绪](configuration-requirements.md) ，使用户能够将设备加入 Azure AD。 如果用户超过了允许加入的设备数，也会发生错误。 此限制在 Azure AD 中进行配置。

导入时，将创建一个 Azure AD 设备。 这一点很重要，此对象不会被删除。 对象充当 Autopilot 在组成员身份和目标 (Azure AD 的定位点，包括配置文件) 。 删除它可能会导致联接错误。 如果删除此对象，可以通过删除并重新导入此 autopilot 哈希来解决该问题，以便可以重新创建关联的对象。

通常会在错误页上报告错误代码801C0003，其中标题为 "出现错误"。 此错误表示 Azure AD 联接失败。

## <a name="troubleshooting-intune-enrollment-issues"></a>Intune 注册问题疑难解答

请参阅 [此知识库文章](https://support.microsoft.com/help/4089533/troubleshooting-windows-device-enrollment-problems-in-microsoft-intune) ，了解 Intune 注册问题。 常见问题可能包括 "
- 分配给用户的许可证不正确或缺失。
- 为用户注册的设备太多。

通常会在错误页上报告错误代码80180018，其中标题为 "出现错误"。 此错误表示 MDM 注册失败。

如果 Autopilot 重置失败，则错误会出现 **问题。请使用管理员帐户登录，以了解为何要手动重置**，有关详细信息，请参阅 [排查 Autopilot reset 问题](https://docs.microsoft.com/education/windows/autopilot-reset#troubleshoot-autopilot-reset) 。

## <a name="profile-download"></a>配置文件下载

当连接 Internet 的 Windows 10 设备启动时，它将尝试连接到 Autopilot 服务并下载 Autopilot 配置文件。 注意：在此阶段存在一个配置文件，使空白配置文件不会缓存到计算机本地。 若要在 Windows 10 版本1803及更早版本中删除当前缓存的本地配置文件，则需要使用 **sysprep/generalize/oobe**重新通用化操作系统，重新安装操作系统，或者重新映像电脑。 在 Windows 10 版本1809及更高版本中，你可以通过重新启动电脑来检索新的配置文件。

下载配置文件的时间取决于计算机上运行的 Windows 10 版本。 请参见下表。

| Windows 10 版本 | 配置文件下载行为 |
| --- | --- |
| 1709 | 配置文件将在 "OOBE 网络连接" 页后下载。 使用有线连接时，不会显示此页。 在这种情况下，会在 EULA 屏幕之前下载配置文件。 |
| 1803 | 配置文件将尽快下载。 如果是有线，则会在 OOBE 开始时下载。 如果是无线，则会在网络连接页面后下载。 |
| 1809 | 配置文件将尽快下载 (与 1803) 相同，并在每次重新启动后再次下载。 |

如果需要在 OOBE 期间重新启动计算机：
- 按 Shift-F10 打开命令提示符。
- 输入 **shutdown/r/t 0** 立即重新启动，或 **关闭/s/t 0** 立即关闭。

有关详细信息，请参阅 [Windows 安装程序命令行选项](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options)。

## <a name="related-topics"></a>相关主题

[Windows Autopilot-已知问题](known-issues.md)<br>
[诊断 Windows 10 中的 MDM 故障](https://docs.microsoft.com/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)<br>
