---
title: Windows Autopilot 要求
ms.reviewer: ''
manager: laurawi
description: 自行通知 Windows Autopilot 部署的软件、网络、许可和配置要求。
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
ms.openlocfilehash: 400a6ea8b63ccb560c62740a4519a6db002fd01e
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907878"
---
# <a name="windows-autopilot-requirements"></a>Windows Autopilot 要求

**适用于： Windows 10**

Windows Autopilot 依赖于 Windows 10、Azure Active Directory 和 Microsoft Intune 等 MDM 服务中的特定功能。  为了使用 Windows Autopilot 并利用这些功能，必须满足某些要求。

**注意**：有关当前支持 windows Autopilot 的 oem 列表，请参阅 [windows Autopilot](https://aka.ms/windowsAutopilot)上的 "参与者设备制造商" 部分。

## <a name="software-requirements"></a>软件要求

- 需要 Windows 10 半年频道的 [受支持版本](/windows/release-information/) 。 还支持 Windows 10 企业版2019长期服务通道 (LTSC) 。
- 支持以下版本：
  - Windows 10 专业版
  - Windows 10 专业教育版
  - Windows 10 专业工作站版
  - Windows 10 企业版
  - Windows 10 教育版
  - Windows 10 企业版 2019 LTSC

>[!NOTE]
>部署 Windows Autopilot 的过程可能是指特定的产品和版本。 此内容中包含这些产品并不表示扩展支持超出其支持生命周期的版本。 Windows Autopilot 不支持超出其支持生命周期的产品。 有关详细信息，请参阅 [Microsoft 生命周期策略](https://go.microsoft.com/fwlink/p/?LinkId=208270)。

## <a name="networking-requirements"></a>网络要求

Windows Autopilot 依赖于各种基于 internet 的服务。 若要使 Autopilot 正常工作，必须提供对这些服务的访问权限。 在最简单的情况下，通过确保以下各项可实现正常功能：

- 确保 Internet DNS 名称的 DNS 名称解析
- 允许通过端口 80 (HTTP)、443 (HTTPS) 和 123 (UDP/NTP) 访问所有端口

在具有限制性更强的 Internet 访问权限的环境中，或在获得 internet 访问权限之前需要进行身份验证的环境中，可能需要进行其他配置才能允许对所需服务进行访问。 

> [!NOTE]
> OOBE 期间不支持智能卡和基于证书的身份验证。 有关详细信息，请参阅 [智能卡和基于证书的身份验证](/azure/active-directory/devices/azureadjoin-plan#smartcards-and-certificate-based-authentication)。

有关每项服务及其具体要求的更多详情，请查看以下详细信息：

<table><th>服务<th>信息
<tr><td><b>Windows Autopilot 部署服务<b><td>建立网络连接后，每个 Windows 10 设备将与 Windows Autopilot 部署服务联系。  在 Windows 10 版本1903及更高版本中，使用以下 Url： https://ztd.dds.microsoft.com 、 https://cs.dds.microsoft.com 。 <br>

<tr><td><b>Windows 激活<b><td>Windows Autopilot 还需要 Windows 激活服务。 有关激活服务需要访问的 Url 的详细信息，请参阅 <a href="https://support.microsoft.com/help/921471/windows-activation-or-validation-fails-with-error-code-0x8004fe33">Windows 激活或验证失败，并显示错误代码 0x8004FE33</a> 。<br>

<tr><td><b>Azure Active Directory<b><td>用户凭据由 Azure Active Directory 进行验证，还可以将设备联接到 Azure Active Directory。 有关详细信息，请参阅 <a href="/office365/enterprise/office-365-ip-web-service">Office 365 IP 地址和 URL Web 服务</a> 。
<tr><td><b>Intune<b><td>经过身份验证后，Azure Active Directory 会触发设备注册到 Intune MDM 服务。 有关网络通信要求的详细信息，请参阅以下链接： <a href="https://docs.microsoft.com/intune/network-bandwidth-use#network-communication-requirements">Intune 网络配置要求和带宽</a>。
<tr><td><b>Windows 更新<b><td>在 OOBE 过程中以及 Windows 10 OS 完全配置后，利用 Windows 更新服务来检索所需的更新。 如果连接到 Windows 更新时出现问题，请参阅 <a href="https://support.microsoft.com/help/818018/how-to-solve-connection-problems-concerning-windows-update-or-microsof">如何解决与 Windows 更新或 Microsoft 更新有关的连接问题</a>。<br>

如果 Windows 更新无法访问，Autopilot 进程仍将继续，但关键更新将不可用。

<tr><td><b>传递优化<b><td>当下载 Windows 更新、Microsoft Store 应用和应用更新、Office 更新和 Intune Win32 应用程序时，将与 <a href="/windows/deployment/update/waas-delivery-optimization">传递优化</a> 服务联系，以便对内容进行对等共享，以便只有少数设备需要从 internet 下载。<br>

如果无法访问传递优化服务，则 Autopilot 进程仍将继续从云 (进行传递优化下载，无需对等) 。

<tr><td><b>网络时间协议 (NTP) 同步<b><td>Windows 设备启动时，它会与网络时间服务器通信，以确保设备上的时间准确无误。 确保 time.windows.com 的 UDP 端口 123 无法访问。
<tr><td><b>域名服务 (DNS) <b><td>为了为所有服务解析 DNS 名称，设备会与通常通过 DHCP 提供的 DNS 服务器通信。此 DNS 服务器必须能够解析 Internet 名称。
<tr><td><b>诊断数据<b><td>从 Windows 10、1903开始，默认情况下将启用诊断数据收集。 若要禁用 Windows Analytics 和相关诊断功能，请参阅 <a href="https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#manage-enterprise-diagnostic-data-level">管理企业诊断数据级别</a>。<br>

如果无法发送诊断数据，Autopilot 进程仍将继续，但依赖于诊断数据的服务（如 Windows Analytics）将不起作用。
<tr><td><b>网络连接状态指示器 (NCSI) <b><td>Windows 必须能够判断出设备可以访问 Internet。 有关详细信息，请参阅 <a href="https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#14-network-connection-status-indicator">网络连接状态指示器 (NCSI) </a>。

<code>www.msftconnecttest.com</code> 必须可通过 DNS 解析，并可通过 HTTP 访问。
<tr><td><b>Windows Notification Services (WNS) <b><td>此服务使 Windows 能够接收来自应用和服务的通知。 有关详细信息，请参阅 <a href="/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#26-microsoft-store">Microsoft Store</a> 。<br>

如果 WNS 服务不可用，则在没有通知的情况下，Autopilot 进程仍将继续。
<tr><td><b>Microsoft Store，业务 Microsoft Store<b><td>Microsoft Store 中的应用可以推送到设备，通过 Intune (MDM) 触发。在用户首次登录时，可能还需要应用更新和其他应用。 有关详细信息，请参阅 <a href="/microsoft-store/prerequisites-microsoft-store-for-business">商业和教育 Microsoft Store 的先决条件</a> (还包括 Azure AD 和 Windows Notification Services) 。<br>

如果 Microsoft Store 不可访问，则 Autopilot 进程仍将继续运行，而不 Microsoft Store 应用。

<tr><td><b>Office 365<b><td>在 Intune 设备配置过程中，可能需要安装适用于企业的 Microsoft 365 应用。 有关详细信息，请参阅 <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2">office 365 url 和 IP 地址范围</a> (包括所有 Office 服务、DNS 名称、ip 地址、包括 Azure AD 和其他可能与上面列出的服务重叠) 的服务。
<tr><td><b>证书吊销列表 (Crl) <b><td>其中某些服务还需要检查证书吊销列表 (CRL) 来确定服务中使用的证书。<a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_crl">Office 365 url 和 IP 地址范围</a>和<a href="https://aka.ms/o365chains">Office 365 证书链</a>中介绍了这些说明的完整列表。
<tr><td><b>混合 AAD 联接<b><td>设备可以加入混合 AAD。 计算机应位于企业网络上，以使混合 AAD 加入工作正常。 查看<a href="user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join">Windows Autopilot 用户驱动模式下</a>的详细信息
<tr><td><b>Autopilot 自助部署模式和 Autopilot 白色手套<b><td>固件 TPM 设备（仅由 Intel、AMD 或 Qualcomm 提供）在引导时不包括所有所需的证书，因此在首次使用时必须能够从制造商那里检索它们。 具有独立 TPM 芯片的设备 (包括任何其他制造商提供的设备) 附带预安装这些证书。 有关更多详细信息，请参阅 <a href="/windows/security/information-protection/tpm/tpm-recommendations">TPM 建议</a> 。 请确保每个固件 TPM 提供程序都可以访问这些 Url，以便成功请求证书： 

  <br>Intel- https://www.intel.com/  <br>Qualcomm- https://ekcert.spserv.microsoft.com/EKCertificate/GetEKCertificate/v1  <br>采用 https://ftpm.amd.com/pki/aia

</table>

## <a name="licensing-requirements"></a>许可要求

Windows Autopilot 取决于 Windows 10 和 Azure Active Directory 中提供的特定功能。 它还需要一个 MDM 服务，如 Microsoft Intune。 可以通过各种版本和订阅计划获得这些功能：

若要提供所需的 Azure Active Directory (自动 MDM 注册和公司品牌功能) 和 MDM 功能，需满足以下要求之一：
- [Microsoft 365 商业版高级订阅](https://www.microsoft.com/microsoft-365/business)
- [Microsoft 365 F1 或 F3 订阅](https://www.microsoft.com/microsoft-365/enterprise/firstline)
- [Microsoft 365 学术 A1、A3 或 A5 订阅](https://www.microsoft.com/education/buy-license/microsoft365/default.aspx)
- [Microsoft 365 企业版 E3 或 E5 订阅](https://www.microsoft.com/microsoft-365/enterprise)，其中包括所有 Windows 10、Office 365 和 EM + S 功能 (Azure AD 和 Intune) 。
- [企业移动性 + 安全性 E3 或 E5 订阅](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)，其中包括所有所需的 Azure AD 和 Intune 功能。
- [Intune for Education 订阅](/intune-education/what-is-intune-for-education)，其中包括所有所需的 Azure AD 和 Intune 功能。
- [Azure Active Directory Premium P1 或 P2](https://azure.microsoft.com/services/active-directory/) 和 [Microsoft Intune 订阅](https://www.microsoft.com/cloud-platform/microsoft-intune) (或其他 MDM 服务) 。

> [!NOTE]
> 即使使用 Microsoft 365 订阅，仍需要向 [用户分配 Intune 许可证](/intune/fundamentals/licenses-assign)。

此外，还建议使用以下 (但不是必需的) ：
- [Microsoft 365 适用于企业的应用](https://www.microsoft.com/p/office-365-proplus/CFQ7TTC0K8R0)，可通过 Intune (或其他 MDM 服务) 轻松部署。
- [Windows 订阅激活](/windows/deployment/windows-10-enterprise-subscription-activation)，将设备从 Windows 10 专业版自动单步执行到 Windows 10 企业版。

## <a name="configuration-requirements"></a>配置要求

在可以使用 Windows Autopilot 之前，需要执行一些配置任务来支持常见的 Autopilot 方案。  

- 配置 Azure Active Directory 自动注册。  有关 Microsoft Intune，请参阅 [启用 Windows 10 自动注册](/intune/windows-enroll#enable-windows-10-automatic-enrollment) 以获取详细信息。  如果使用不同的 MDM 服务，请与供应商联系，以了解这些服务所需的特定 Url 或配置。
- 配置 Azure Active Directory 自定义品牌。  若要在 Autopilot 过程中显示特定于组织的登录页，需要使用应显示的图像和文本来配置 Azure Active Directory。  有关更多详细信息，请参阅 ["快速入门：将公司品牌添加到 Azure AD 中的登录页"](/azure/active-directory/fundamentals/customize-branding) 。  请注意，"方形徽标" 和 "登录页文本" 是 Autopilot 的关键元素，并且 Azure Active Directory 租户名称 (在 Azure AD 租户属性) 中单独配置。
- 如果需要，请启用 [Windows 订阅激活](/windows/deployment/windows-10-enterprise-subscription-activation) ，以便从 Windows 10 Pro 自动单步执行到 Windows 10 企业版。

具体方案将具有其他要求。  通常有两个特定任务：

- 设备注册。  需要将设备添加到 Windows Autopilot 以支持大多数 Windows Autopilot 方案。  有关更多详细信息，请参阅向 [Windows Autopilot 添加设备](add-devices.md) 。
- 配置文件配置。  在将设备添加到 Windows Autopilot 后，需要将设置的配置文件应用于每个设备。  有关详细信息，请参阅 [配置 Autopilot 配置文件](profiles.md) 。  请注意，Microsoft Intune 可以自动执行此配置文件分配;有关详细信息，请参阅 [创建 Autopilot 设备组](/intune/enrollment-Autopilot#create-an-Autopilot-device-group) 和 [将 Autopilot 部署配置文件分配到设备组](/intune/enrollment-Autopilot#assign-an-Autopilot-deployment-profile-to-a-device-group) 。

有关更多详细信息，请参阅 [Windows Autopilot 方案](windows-Autopilot-scenarios.md) 。

有关部分和相关步骤的演练，请观看此视频：

</br>

<iframe width="560" height="315" src="https://www.youtube.com/embed/KYVptkpsOqs" frameborder="0" allow="accelerometer; autoplay; encrypted-media" gyroscope; picture-in-picture" allowfullscreen></iframe>


除了[运行 Windows 10 的要求](https://www.microsoft.com/windows/windows-10-specifications)之外，使用 Windows 10 Autopilot 时没有其他硬件要求。

## <a name="related-topics"></a>相关主题

[Windows Autopilot 概述](windows-Autopilot.md)