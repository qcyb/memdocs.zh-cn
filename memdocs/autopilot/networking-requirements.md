---
title: Windows Autopilot 网络连接要求
ms.reviewer: ''
manager: laurawi
description: 自行通知 Windows Autopilot 部署的网络要求。
keywords: mdm，安装程序，windows，windows 10，oobe，管理，部署，Autopilot，ztd，0-touch，合作伙伴，msfb，intune
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
ms.custom:
- CI 116757
- CSSTroubleshooting
ms.openlocfilehash: 3c24610a2ac10dfae6a8ba73062edf29188938ea
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907985"
---
# <a name="windows-autopilot-networking-requirements"></a>Windows Autopilot 网络连接要求

**适用于： Windows 10**

Windows Autopilot 依赖于各种基于 internet 的服务。 若要使 Autopilot 正常工作，必须提供对这些服务的访问权限。 在最简单的情况下，可通过确保满足以下条件来实现正确的功能：

- 确保域名服务 (DNS) 名称解析以获取 internet DNS 名称
- 允许通过端口 80 (HTTP)、443 (HTTPS) 和 123 (UDP/NTP) 访问所有端口

在以下环境中，可能需要进行其他配置才能授予对所需服务的访问权限：
- 具有限制性更强的 Internet 访问。
- 需要进行身份验证才能获得 internet 访问权限。 

> [!NOTE]
> OOBE 期间不支持智能卡和基于证书的身份验证。 有关详细信息，请参阅 [智能卡和基于证书的身份验证](/azure/active-directory/devices/azureadjoin-plan#smartcards-and-certificate-based-authentication)。

有关每项服务及其具体要求的更多详情，请查看以下详细信息：

<table><th>服务<th>信息
<tr><td><b>Windows Autopilot 部署服务<b><td>建立网络连接后，每个 Windows 10 设备将与 Windows Autopilot 部署服务联系。 在 Windows 10 版本1903及更高版本中，使用以下 Url： https://ztd.dds.microsoft.com 、 https://cs.dds.microsoft.com 。 <br>

<tr><td><b>Windows 激活<b><td>Windows Autopilot 需要 Windows 激活服务。 有关激活服务需要访问的 Url 的详细信息，请参阅 <a href="https://support.microsoft.com/help/921471/windows-activation-or-validation-fails-with-error-code-0x8004fe33">Windows 激活或验证失败，错误代码为 0x8004FE33</a>。<br>

<tr><td><b>Azure Active Directory<b><td>用户凭据由 Azure Active Directory 进行验证，还可以将设备联接到 Azure Active Directory。 有关详细信息，请参阅 <a href="https://docs.microsoft.com/office365/enterprise/office-365-ip-web-service">Office 365 IP 地址和 URL Web 服务</a>。
<tr><td><b>Intune<b><td>经过身份验证后，Azure Active Directory 会触发设备注册到 Intune 移动设备管理 (MDM) 服务。 有关网络通信要求的详细信息，请参阅以下链接： <a href="https://docs.microsoft.com/intune/network-bandwidth-use#network-communication-requirements">Intune 网络配置要求和带宽</a>。
<tr><td><b>Windows 更新<b><td>在 OOBE 过程中以及 Windows 10 OS 配置之后，Windows 更新服务将检索所需的更新。 如果连接到 Windows 更新时出现问题，请参阅 <a href="https://support.microsoft.com/help/818018/how-to-solve-connection-problems-concerning-windows-update-or-microsof">如何解决与 Windows 更新或 Microsoft 更新有关的连接问题</a>。<br>

如果 Windows 更新无法访问，则 Autopilot 进程仍将继续，但无法获得关键更新。

<tr><td><b>传递优化<b><td>下载应用和更新时，Autopilot 会与 <a href="/windows/deployment/update/waas-delivery-optimization">传送优化</a> 服务联系。 此联系人建立了对等共享内容，以便只有几个设备需要从 Internet 下载。
- Windows 更新 - Microsoft Store 应用和应用更新 - Office 更新 - Intune Win32 应用<br>

如果无法访问传递优化服务，则 Autopilot 进程仍将继续从云 (进行传递优化下载，无需对等) 。

<tr><td><b>网络时间协议 (NTP) 同步<b><td>Windows 设备启动时，它会与网络时间服务器通信，以确保设备上的时间正确。 确保 time.windows.com 的 UDP 端口 123 无法访问。
<tr><td><b>域名服务 (DNS) <b><td>为了为所有服务解析 DNS 名称，设备会与通常通过 DHCP 提供的 DNS 服务器通信。 此 DNS 服务器必须能够解析 Internet 名称。
<tr><td><b>诊断数据<b><td>从 Windows 10、1903开始，默认情况下将启用诊断数据收集。 若要禁用 Windows Analytics 和相关诊断功能，请参阅 <a href="https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#manage-enterprise-diagnostic-data-level">管理企业诊断数据级别</a>。<br>

如果无法发送诊断数据，Autopilot 进程仍将继续。 但是，依赖于诊断数据的服务（如 Windows Analytics）将不起作用。
<tr><td><b>网络连接状态指示器 (NCSI) <b><td>Windows 必须能够知道设备可以访问 internet。 有关详细信息，请参阅 <a href="https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#14-network-connection-status-indicator">网络连接状态指示器 (NCSI) </a>。

<code>www.msftconnecttest.com</code> 必须可通过 DNS 解析，并可通过 HTTP 访问。
<tr><td><b>Windows Notification Services (WNS) <b><td>此服务使 Windows 能够接收来自应用和服务的通知。 有关详细信息，请参阅 <a href="https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#26-microsoft-store">Microsoft Store</a>。<br>

如果 WNS 服务不可用，则在没有通知的情况下，Autopilot 进程仍将继续。
<tr><td><b>Microsoft Store，业务 Microsoft Store<b><td>Microsoft Store 中的应用可以推送到设备，通过 Intune (MDM) 触发。在用户首次登录时，可能还需要应用更新和其他应用。 有关详细信息，请参阅 <a href="/microsoft-store/prerequisites-microsoft-store-for-business">商业和教育 Microsoft Store 的先决条件</a> (还包括 Azure AD 和 Windows Notification Services) 。<br>

如果 Microsoft Store 不可访问，则 Autopilot 进程仍将继续运行，而不 Microsoft Store 应用。

<tr><td><b>Office 365<b><td>在 Intune 设备配置过程中，可能需要安装适用于企业的 Microsoft 365 应用。 有关详细信息，请参阅 <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2">Office 365 url 和 IP 地址范围</a>。 本文包含所有 Office 服务、DNS 名称和 IP 地址。 它还包括与上面列出的服务重叠的 Azure AD 和其他服务。
<tr><td><b>证书吊销列表 (Crl) <b><td>其中某些服务还需要检查证书吊销列表 (CRL) 来确定服务中使用的证书。有关完整列表，请参阅 <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_crl">office 365 url 和 IP 地址范围</a> 和 <a href="https://aka.ms/o365chains">Office 365 证书链</a>。
<tr><td><b>混合 Azure AD 加入<b><td>设备可以 Azure AD 联接的混合。 计算机应位于企业网络上，以便混合 Azure AD 加入工作。 查看<a href="user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join">Windows Autopilot 用户驱动模式下</a>的详细信息
<tr><td><b>Autopilot 自助部署模式和 Autopilot 白色手套<b><td>固件 TPM 设备仅由 Intel、AMD 或 Qualcomm 提供，在引导时不包括所有所需的证书，并且必须能够在第一次使用时从制造商检索它们。 具有独立 TPM 芯片的设备 (包括任何其他制造商提供的设备) 附带预安装这些证书。 有关详细信息，请参阅 <a href="https://docs.microsoft.com/windows/security/information-protection/tpm/tpm-recommendations">TPM 建议</a>。 对于每个固件 TPM 提供程序，请确保可以访问这些 Url，以便成功请求证书：

 <br>媒体 <code>https://ekop.intel.com/ekcertservice</code>
 <br>Qualcomm <code>https://ekcert.spserv.microsoft.com/EKCertificate/GetEKCertificate/v1</code>
 <br>采用 <code>https://ftpm.amd.com/pki/aia</code>

</table>

**后续步骤**

[Windows Autopilot 许可要求](licensing-requirements.md)