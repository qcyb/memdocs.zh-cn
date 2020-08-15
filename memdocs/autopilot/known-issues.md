---
title: Windows Autopilot 的已知问题
ms.reviewer: ''
manager: laurawi
description: 就 Windows Autopilot 部署过程中可能出现的已知问题进行通知。
keywords: mdm, 设置, windows, windows 10, oobe, 管理, 部署, autopilot, ztd, 零接触, 合作伙伴, msfb, intune
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
ms.openlocfilehash: d7c92d2e999ffe9a4e503359a81e6422cd24ee30
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252020"
---
# <a name="windows-autopilot---known-issues"></a>Windows Autopilot-已知问题

**适用于**

- Windows 10

<table>
<th>问题<th>详细信息

<tr><td>在设备 ESP 期间将忽略在用户目标注册状态配置文件中指定的阻止应用。</td>
<td>负责确定设备 ESP 期间应阻止的应用列表的服务无法确定包含应用列表的正确 ESP 配置文件，因为他们不知道用户标识。 作为一种解决方法，启用) 的所有用户和设备的默认 ESP 配置文件 (，并将阻止应用列表放置在此处。 将来，可以改为将 ESP 配置文件定位到设备组，以避免此问题。</tr>

<tr><td>该用户名看起来就像是另一个组织。 再次尝试登录或使用其他帐户重新开始。</td>
 <td>确认 \SOFTWARE\Microsoft\Provisioning\Diagnostics\AutoPilot. 中的所有信息正确 HKEY_LOCAL_MACHINE 无误 有关详细信息，请参阅 <a href="troubleshooting.md#windows-10-version-1709-and-above">Windows Autopilot 故障排除</a>。</td></tr>

<tr><td>Windows Autopilot 用户驱动的混合 Azure AD 部署即使在 Windows Autopilot 配置文件中指定，也不会授予用户管理员权限。</td>
<td>如果设备上有另一个用户已具有管理员权限，则会出现此问题。 例如，PowerShell 脚本或策略可能会创建作为 Administrators 组成员的其他本地帐户。 若要确保此功能正常工作，请在 Windows Autopilot 进程完成后再创建其他帐户。</tr>

<tr><td>Windows Autopilot 设备预配可能会失败，并会导致在实时时钟关闭的设备上出现 TPM 证明错误或 ESP 超时 (例如，几分钟或更长时间) 。</td>
<td>解决此问题： <ol><li>启动设备以启动 (OOBE) 的全新体验。
<li> (有线或无线) 建立网络连接。
<li>运行命令 <b>w32tm/resync/force</b> ，以将时间与默认时间服务器 (time.windows.com) 同步。</ol>
</tr>

<tr><td>Windows Autopilot for 现有设备不适用于 Windows 10 版本1903或 1909;你会看到已在 Windows Autopilot 配置文件中禁用的屏幕，例如 Windows 10 许可协议屏幕。
<br>&nbsp;<br>
发生此问题的原因是 Windows 10 版本1903和1909删除了文件上的 AutopilotConfigurationFile.js。
<td>解决此问题： <ol><li>编辑 Configuration Manager 任务序列，并禁用 " <b>准备 Windows 以便捕获</b> " 步骤。
<li>添加<b>c:\windows\system32\sysprep\sysprep.exe/oobe/reboot</b>运行的新<b>运行命令行</b>步骤。</ol>
<a href="https://oofhours.com/2019/09/19/a-challenge-with-windows-autopilot-for-existing-devices-and-windows-10-1903/">详细信息</a></tr>
 
<tr><td>由于 EK 证书中缺少空格扩展，在 Windows 10 1903 上的 TPM 证明失败。  (在 Windows 10 1903 中添加的其他验证，以检查 TPM EK 证书是否具有适当的属性，具体取决于 TCG 规范是否发现了某个数量的属性，以便在) 删除验证。
<td>下载并安装 <a href="https://support.microsoft.com/help/4517211/windows-10-update-kb4517211">KB4517211 更新</a>。
<tr><td>以下已知问题通过将2019年8月30日 KB4512941 更新安装 (OS Build 18362.329) 来解决：

- Windows Autopilot for 现有设备功能在 OOBE 期间不会正确抑制 "活动" 页。  (由于此问题，你会在 OOBE) 中看到该额外页面。
- Sysprep/generalize 不会清除 TPM 证明状态，这会导致以后的 OOBE 流中发生 TPM 证明失败。  (这不是一个特别常见的问题，但如果你运行的是 sysprep/generalize，然后重新启动或重置设备，然后重新启动或重置设备的映像，则可以在) 的情况下运行它。
- 如果设备具有有效的 AIK 证书但没有 EK 证书，则 TPM 证明可能会失败。 (此问题与以前的项目) 相关。
- 如果 TPM 证明在 Windows Autopilot 白手套过程中失败，则登陆页面似乎已挂起。  (主要是手套登陆页，单击 "预配" 启动白色手套过程时，不会正确报告错误) 。
- TPM 证明在更新的 Infineon Tpm (固件版本 > 7.69) 失败。  (此修补之前，只) 接受特定的固件版本列表。
- 设备命名模板可以将计算机名称截断为14个字符，而不是15个字符。
- 分配的访问策略会导致重新启动，这可能会干扰单应用展台设备的配置。
<td>下载并安装 <a href="https://support.microsoft.com/help/4512941">KB4512941 更新</a>。 <br><br>请参阅 " <b>如何获取此更新</b> " 部分，了解有关可用于获取更新的特定发布通道的信息。
<tr><td>以下已知问题通过将2019年7月26日 KB4505903 更新安装 (OS Build 18362.267) 来解决：

- 对于非英语操作系统，Windows Autopilot 白手套不起作用，你会看到一个红色屏幕，其中显示 "成功"。
- Windows Autopilot 在 sysprep、重置或其他变体之后，在 OOBE 期间报告 AUTOPILOTUPDATE 错误。 如果重置 OS 或使用自定义的经过系统准备映像，通常会发生此问题。
- BitLocker 加密配置不正确。 例如：在应用策略后，BitLocker 未收到预期通知以开始加密。
- 无法从 Microsoft Store 安装 UWP 应用，导致在 Windows Autopilot 期间发生故障。 如果在 Windows Autopilot ESP 期间将公司门户作为阻止应用部署，则可能会看到此错误。
- 在 Windows Autopilot 用户驱动混合 Azure AD 联接方案中，不向用户授予管理员权限。 这是另一个非英语操作系统问题。
<td>下载并安装 <a href="https://support.microsoft.com/help/4505903">KB4505903 更新</a>。 <br><br>请参阅 " <b>如何获取此更新</b> " 部分，了解有关可用于获取更新的特定发布通道的信息。
<tr><td>Windows Autopilot <a href="self-deploying.md">自部署模式</a> 失败，出现错误代码：
<td><table>
<tr><td>0x800705B4<td>这是一个指示超时的一般错误。 在自行部署模式下，此错误的一个常见原因是设备不支持 TPM 2.0， (例如：虚拟机) 。 不支持 TPM 2.0 的设备不能与自部署模式一起使用。
<tr><td>0x801c03ea<td>此错误表示 TPM 证明失败，导致无法将 Azure Active Directory 与设备令牌联接。
<tr><td>0xc1036501<td>设备无法执行自动 MDM 注册，因为 Azure AD 中有多个 MDM 配置。 请参阅 <a href="https://oofhours.com/2019/10/01/inside-windows-autopilot-self-deploying-mode/">Windows Autopilot 自部署模式内部</a>。
</table>
<tr><td>白色手套提供红屏， <b>Microsoft Windows 用户设备注册/管理</b> 事件日志显示 <b>HResult 错误代码 0x801C03F3</b><td>如果 Azure AD 无法找到要部署的设备的 Azure AD 设备对象，则可能出现此问题。 如果手动删除该对象，将出现此问题。 若要修复此问题，请从 Azure AD、Intune 和 Autopilot 中删除该设备，然后将其重新注册到 Autopilot，这将重新创建 Azure AD 设备对象。<br> 
<br>若要获取疑难解答日志，请使用： <b>Mdmdiagnosticstool.exe-Area Autopilot;TPM-cab c:\autopilot.cab</b>
<tr><td>白色手套提供红屏<td>虚拟机上不支持手套。
<tr><td>从 .csv 文件导入 Windows Autopilot 设备时出错<td>确保你未在 Microsoft Excel 或记事本以外的其他编辑器中编辑 .csv 文件。 其中一些编辑器可能会引入额外字符，导致文件格式无效。 
<tr><td>Windows Autopilot for 现有设备不遵循 Autopilot OOBE 体验。<td>确保 JSON 配置文件以 <b>ANSI/ASCII</b> 格式保存，而不是 UNICODE 或 utf-8 格式。
<tr><td>在 OOBE 期间显示了<b>错误</b>的页面。<td>客户端可能无法访问所有必需的 Azure AD/MSA 相关 Url。 有关详细信息，请参阅 [网络要求](networking-requirements.md)。
<tr><td>将预配包与 Windows Autopilot 结合使用可能会导致问题，特别是在 PPKG 包含联接、注册或设备名称信息时。<td>不建议将 PPKGs 与 Windows Autopilot 结合使用。
</table>

## <a name="related-topics"></a>相关主题

[诊断 Windows 10 中的 MDM 故障](https://docs.microsoft.com/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10)<br>
[Windows Autopilot 故障排除](troubleshooting.md)
