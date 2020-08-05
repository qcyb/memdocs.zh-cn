---
title: Windows Autopilot 用户驱动模式
description: Windows Autopilot 用户驱动模式允许将设备部署到可用状态，而无需 IT 人员的帮助。
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
ms.openlocfilehash: b5e7c88272f8da386d25e7e7bca1973026f4407a
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756121"
---
# <a name="windows-autopilot-user-driven-mode"></a>Windows Autopilot 用户驱动模式

**适用于： Windows 10 版本1809或更高版本**

Windows Autopilot 用户驱动模式旨在使新的 Windows 10 设备从其初始工厂状态转换为随时可用状态，而无需 IT 人员触摸设备。  此过程的设计非常简单，因此任何人都可以完成此过程，使设备能够通过简单的说明直接运送或分发给最终用户：

- 取消装箱设备，将其插入，然后将其打开。
- 仅当安装了多种语言) 、区域设置和键盘时，才 (需要选择语言。
- 将其连接到具有 internet 访问权限的无线或有线网络。  如果使用无线，则用户必须建立 Wi-fi 链接。  
- 指定你的组织帐户的电子邮件地址和密码。

完成这些简单步骤后，该过程的剩余部分将自动执行，并且设备将加入到组织，在 Intune 中注册 (或另一个 MDM 服务) ，并完全按组织定义的方式进行配置。  在全新体验 (OOBE) 的任何其他提示都可以取消;有关可用选项，请参阅[配置 Autopilot 配置文件](profiles.md)。

Windows Autopilot 用户驱动模式 Azure Active Directory 和混合 Azure Active Directory 连接的设备支持。  有关这两个联接选项的详细信息，请参阅[什么是设备标识](https://docs.microsoft.com/azure/active-directory/devices/overview)。

从处理流的角度来看，在用户驱动过程中执行的任务如下所示：

- 连接到网络后，设备将下载 Windows Autopilot 配置文件，该配置文件指定应使用的设置 (例如，在 OOBE 期间应禁止显示) 的提示。
- Windows 10 会检查是否有关键的 OOBE 更新。 如果有可用的更新，则在需要时 (重新启动，它们会自动安装) 。
- 系统将提示用户输入 Azure Active Directory 凭据，并显示 Azure AD 租户名称、徽标和登录文本的自定义用户体验。
- 设备将基于 Windows Autopilot 配置文件设置来联接 Azure Active Directory 或 Active Directory。
- 设备将在 Intune 中注册 (或其他配置的 MDM 服务) 。   (此注册是通过 MDM 自动注册 Azure Active Directory 加入过程的一部分，或者在 Active Directory 加入过程之前，根据需要进行。 ) 
- 如果已配置，将显示 (ESP) 的 "[注册状态" 页](enrollment-status.md)。
- 设备配置任务完成后，用户将使用之前提供的凭据登录 Windows 10。   (注意：如果设备在设备 ESP 过程中重启，用户将需要重新输入凭据，因为这些详细信息不会在重新启动后保留。 ) 
- 登录后，将再次为用户目标配置任务显示 "注册状态" 页。

如果在此过程中遇到任何问题，请参阅[Windows Autopilot 故障排除](troubleshooting.md)文档。

有关可用联接选项的详细信息，请参阅以下部分：

- 如果设备无需加入本地 Active Directory 域， [Azure Active Directory 联接](#user-driven-mode-for-azure-active-directory-join)可用。
- [混合 Azure Active Directory 联接](#user-driven-mode-for-hybrid-azure-active-directory-join)适用于必须联接到 Azure Active Directory 和本地 Active Directory 域的设备。

## <a name="user-driven-mode-for-azure-active-directory-join"></a>Azure Active Directory 联接的用户驱动模式

为了使用 Windows Autopilot 执行用户驱动的部署，需要完成以下准备步骤：

- 确保将执行用户驱动模式部署的用户能够将设备加入到 Azure Active Directory。  有关详细信息，请参阅 Azure Active Directory 文档中的 "[配置设备设置](https://docs.microsoft.com/azure/active-directory/device-management-azure-portal#configure-device-settings)"。
- 使用所需设置为用户驱动模式创建 Autopilot 配置文件。  在 Microsoft Intune 中，将在创建配置文件时显式选择此模式。 对于业务和合作伙伴中心的 Microsoft Store，用户驱动模式是默认模式，无需选择。
- 如果使用 Intune，请在 Azure Active Directory 中创建一个设备组，并将 Autopilot 配置文件分配给该组。

对于将使用用户驱动的部署进行部署的每个设备，需要执行以下附加步骤：

- 确保已将设备添加到 Windows Autopilot。  此添加操作可以在设备购买时由 OEM 或合作伙伴自动完成，也可以稍后通过手动收集过程来完成。  有关详细信息，请参阅向[Windows Autopilot 添加设备](add-devices.md)。
- 确保已向设备分配 Autopilot 配置文件：
  - 如果使用 Intune 并 Azure Active Directory 动态设备组，则可以自动执行此分配。
  - 如果使用 Intune 并 Azure Active Directory 静态设备组，请将设备手动添加到设备组。
  - 如果使用其他方法 (例如，Microsoft Store 适用于企业或合作伙伴中心) ，请手动将 Autopilot 配置文件分配到设备。


## <a name="user-driven-mode-for-hybrid-azure-active-directory-join"></a>混合 Azure Active Directory 联接的用户驱动模式

Windows Autopilot 要求 Azure Active Directory 连接设备。 如果你有本地 Active Directory 环境，同时想要将设备加入本地域，则可以将 Autopilot 设备配置为[混合加入到 Azure Active Directory (Azure AD) ](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)。  

### <a name="requirements"></a>要求

若要使用 Windows Autopilot 执行用户驱动的混合 Azure AD 联接的部署：

- 必须创建用户驱动模式的 Windows Autopilot 配置文件，并 
  - 在 Autopilot 配置文件中，必须将**混合 Azure AD 联接**指定为 "**联接到 Azure AD** " 下的所选选项。
- 如果使用 Intune，Azure Active Directory 中的设备组必须与分配给该组的 Windows Autopilot 配置文件存在。
- 设备必须运行 Windows 10 版本1809或更高版本。
- 设备必须能够访问 Active Directory 域控制器，因此它必须连接到组织的网络 (可在其中解析 AD 域和 AD 域控制器的 DNS 记录，并与域控制器进行通信，以便对用户) 进行身份验证。
- 设备必须能够访问 Internet，遵循所[述的 Windows Autopilot 网络要求](windows-autopilot-requirements.md)。
- 必须安装 Active Directory 的 Intune 连接器。
  - 注意： Intune 连接器将执行本地 AD join，因此，用户不需要本地 AD 联接权限，前提是该连接器[配置为代表用户执行此操作](https://docs.microsoft.com/intune/windows-autopilot-hybrid#increase-the-computer-account-limit-in-the-organizational-unit)。 
- 如果使用代理，必须启用并配置 WPAD 代理设置选项。

**Azure AD 设备加入**：混合 Azure AD 联接过程使用系统上下文来执行 Azure AD 加入设备，因此不受基于用户的 Azure AD 联接权限设置的影响。 此外，默认情况下，所有用户都可以将设备加入到 Azure AD。

## <a name="user-driven-mode-for-hybrid-azure-active-directory-join-with-vpn-support"></a>具有 VPN 支持的混合 Azure Active Directory 联接的用户驱动模式

加入到 Active Directory 的设备需要连接到 Active Directory 的域控制器来执行各种活动，例如用户登录 (验证用户的凭据) 和组策略应用程序。  因此，Windows Autopilot 用户驱动混合 Azure AD 联接过程将验证设备是否能够通过 ping 域控制器与 Active Directory 域控制器联系。

利用此方案的其他 VPN 支持，现在可以指定在混合 Azure AD 联接过程中跳过该连接检查。  这并不是为了与 Active Directory 域控制器进行通信，而是允许在用户尝试登录 Windows 之前通过 Intune 传递所需的 VPN 配置，并允许连接到组织的网络。

### <a name="requirements"></a>要求

以下附加要求适用于具有 VPN 支持的混合 Azure AD 联接：

- 受支持的 Windows 10 版本：
  - Windows 10 1903 + 12 月10日累积更新 (KB4530684、OS build 18362.535) 或更高版本 
  - Windows 10 1909 + 12 月10日累积更新 (KB4530684、OS build 18363.535) 或更高版本  
  - Windows 10 2004 或更高版本 
- 启用混合 Azure AD 联接 Autopilot 配置文件中的新 "跳过域连接检查" 切换。
- 可以通过 Intune 部署的 VPN 配置，该配置允许用户通过 Windows 登录屏幕手动建立 VPN 连接，或根据需要自动建立 VPN 连接。  

所需的特定 VPN 配置取决于所使用的 VPN 软件和身份验证。  对于第三方 (非 Microsoft) VPN 解决方案，这通常涉及到部署包含 VPN 客户端软件本身的 Win32 应用 (，以及任何特定的连接信息，例如：通过 Intune 管理扩展) VPN 终结点主机名。  有关特定于提供程序的配置详细信息，请参阅 VPN 提供程序的文档。

> [!NOTE]
> VPN 要求并不特定于 Windows Autopilot。 例如，如果你已经实现了 VPN 配置来启用远程密码重置，而用户需要在不在组织网络中使用新密码登录到 Windows，则可以在 Windows Autopilot 中使用相同的配置。  用户登录到缓存其凭据后，后续登录尝试不需要连接，因为可以使用缓存的凭据。 

如果 VPN 软件需要证书身份验证，则还应通过 Intune 部署所需的计算机证书。  可以使用 Intune 证书注册功能完成此部署，将证书配置文件定向到设备。

请注意，不支持用户证书，因为在用户登录之前无法部署这些证书。  此外，也不支持从 Windows 应用商店提供的非 Microsoft UWP VPN 插件，因为在用户登录之前，这些插件不会安装。

### <a name="validation"></a>验证

在尝试使用 VPN 进行混合 Azure AD 联接之前，首先确认是否可以在组织的网络上执行用户驱动的混合 Azure AD 联接进程，然后再添加下面所述的其他要求。  这简化了故障排除，方法是在添加所需的其他 VPN 配置之前确保核心过程正常运行。

接下来，验证 VPN 配置 (Win32 应用、证书以及任何其他要求) 是否可以通过 Intune 部署到已加入混合 Azure AD 的现有设备。  例如，某些 VPN 客户端会在安装过程中创建每台计算机 VPN 连接，因此可以使用以下步骤验证配置：

- 在 PowerShell 中，验证是否已使用 "VpnConnection-AllUserConnection" 命令创建了至少一台每台计算机 VPN 连接。
- 尝试使用以下命令手动启动 VPN 连接： RASDIAL.EXE "ConnectionName"
- 注销并验证是否可以在 Windows 登录页上查看 "VPN 连接" 图标。
- 将设备移出公司网络，尝试使用 Windows 登录页上的图标建立连接，并登录到没有缓存凭据的帐户。

对于自动连接的 VPN 配置，验证步骤可能会有所不同。

> [!NOTE]
> Always On VPN 可用于此方案。  有关详细信息，请参阅[部署 ALWAYS ON VPN](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy-deployment)文档。  请注意，Intune 尚未部署所需的每个计算机 VPN 配置文件。 

若要验证端到端过程，请确保在 Windows 10 1903 或 Windows 10 1909 上安装了所需的 Windows 10 累积更新。 可以通过先从中下载最新的累积 https://catalog.update.microsoft.com ，然后手动安装，在 OOBE 期间手动完成此更新：

- 按 Shift-F10 打开命令提示符。
- 插入包含已下载更新的 USB 密钥。
- 使用命令安装更新 (替换真实文件名) ： WUSA.EXE <filename> msu/quiet
- 使用以下命令重新启动计算机： shutdown.exe/r/t 0

或者，你可以通过此过程调用 Windows 更新来安装最新的更新：

- 按 Shift-F10 打开命令提示符。
- 运行命令 "start ms-settings："
- 导航到 "更新 & 安全" 节点并检查更新。
- 安装更新后重新启动。

### <a name="step-by-step-instructions"></a>分步说明

请参阅[使用 Intune 和 Windows Autopilot 部署混合 Azure AD 加入的设备](https://docs.microsoft.com/intune/windows-autopilot-hybrid)。



