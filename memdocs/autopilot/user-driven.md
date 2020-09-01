---
title: Windows Autopilot 用户驱动模式
description: 使用 Windows Autopilot 用户驱动模式，可以将设备配置为部署到可用状态，而无需 IT 人员提供帮助。
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
ms.openlocfilehash: f5299db1c151d3338fb2060246a7d07beb462779
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193649"
---
# <a name="windows-autopilot-user-driven-mode"></a>Windows Autopilot 用户驱动模式

**适用于： Windows 10 版本1809或更高版本**

Windows Autopilot 用户驱动模式允许配置新的 Windows 10 设备，以自动将其从工厂状态转换为随时可用状态。 此过程不需要 IT 人员触摸设备。

此过程很简单，因此任何人都可以完成此过程。 可以通过简单的说明直接将设备交付或分发给最终用户：

1. 取消装箱设备，将其插入，然后将其打开。
2. 仅当安装了多种语言) 、区域设置和键盘时，才 (需要选择语言。
3. 将其连接到具有 internet 访问权限的无线或有线网络。 如果使用无线，则用户必须建立 Wi-fi 链接。 
4. 指定你的组织帐户的电子邮件地址和密码。

此过程的其余部分将自动执行，作为设备：
1. 加入组织。
2. 在 Intune 中注册 (或另一个 MDM 服务) 
3. 按组织定义的方式进行配置。

在全新体验 (OOBE) 的任何其他提示都可以取消;有关可用选项，请参阅 [配置 Autopilot 配置文件](profiles.md) 。

Windows Autopilot 用户驱动模式 Azure Active Directory 和混合 Azure Active Directory 连接的设备支持。 有关这两个联接选项的详细信息，请参阅 [什么是设备标识](/azure/active-directory/devices/overview)。

用户驱动过程中完成的流程如下所示：

1. 连接到网络后，设备会下载 Windows Autopilot 配置文件。 配置文件定义用于设备的设置。 例如，定义在 OOBE 期间禁止显示的提示。
2. Windows 10 检查是否存在关键的 OOBE 更新。 如果有可用更新，它们会自动安装 (重新启动（如有必要）) 。
3. 系统将提示用户输入 Azure Active Directory 凭据。 此自定义的用户体验显示 Azure AD 租户名称、徽标和登录文本。
4.  设备根据 Windows Autopilot 配置文件设置，加入 Azure Active Directory 或 Active Directory。
5. 设备在 Intune 中注册 (或其他配置的 MDM 服务) 。 根据组织的需要，将发生此注册：
    - 在使用 MDM 自动注册的 Azure Active Directory 联接过程中
    - 或在 Active Directory 联接过程之前。
6. 如果已配置，将显示 (ESP) 的 " [注册状态" 页](enrollment-status.md) 。
7. 设备配置任务完成后，用户将使用之前提供的凭据登录到 Windows 10。  (如果设备在设备 ESP 过程中重启，用户必须重新输入其凭据，因为这些详细信息不会在重新启动后保留。 ) 
8. 登录后，将为用户目标配置任务显示 "注册状态" 页。

如果在此过程中发现任何问题，请参阅 [Windows Autopilot 故障排除](troubleshooting.md) 文档。

有关可用联接选项的详细信息，请参阅以下部分：

- 如果设备无需加入本地 Active Directory 域， [Azure Active Directory 联接](#user-driven-mode-for-azure-active-directory-join)可用。
- [混合 Azure Active Directory 联接](#user-driven-mode-for-hybrid-azure-active-directory-join) 适用于必须联接到 Azure Active Directory 和本地 Active Directory 域的设备。

## <a name="user-driven-mode-for-azure-active-directory-join"></a>Azure Active Directory 联接的用户驱动模式

若要使用 Windows Autopilot 完成用户驱动的部署，请执行以下准备步骤：

1. 请确保将执行用户驱动模式部署的用户可以将设备加入到 Azure Active Directory。 有关详细信息，请参阅 Azure Active Directory 文档中的 " [配置设备设置](/azure/active-directory/device-management-azure-portal#configure-device-settings) "。
2. 使用所需设置为用户驱动模式创建 Autopilot 配置文件。 在 Microsoft Intune 中，将在创建配置文件时显式选择此模式。 对于业务和合作伙伴中心的 Microsoft Store，用户驱动模式是默认模式，无需选择。
3. 如果使用 Intune，请在 Azure Active Directory 中创建一个设备组，并将 Autopilot 配置文件分配给该组。

对于将使用用户驱动的部署进行部署的每个设备，需要执行以下附加步骤：

- 请确保设备已添加到 Windows Autopilot。 可以通过两种方式将设备添加到 Windows Autopilot：
  - 在购买设备时由 OEM 或合作伙伴自动进行
  - 手动收集，如 [将设备添加到 Windows Autopilot](add-devices.md)中所述。
- 确保已向设备分配 Autopilot 配置文件：
 - 如果使用 Intune 并 Azure Active Directory 动态设备组，则可以自动执行此分配。
 - 如果使用 Intune 并 Azure Active Directory 静态设备组，请将设备手动添加到设备组。
 - 如果使用其他方法 (例如，Microsoft Store 适用于企业或合作伙伴中心) ，请手动将 Autopilot 配置文件分配到设备。


## <a name="user-driven-mode-for-hybrid-azure-active-directory-join"></a>混合 Azure Active Directory 联接的用户驱动模式

Windows Autopilot 要求 Azure Active Directory 连接设备。 如果你有本地 Active Directory 环境，则可以将设备加入你的本地域。 要加入设备，你必须将 Autopilot 设备配置为 [混合联接到 Azure Active Directory (Azure AD) ](/azure/active-directory/devices/hybrid-azuread-join-plan)。 

### <a name="requirements"></a>要求

若要使用 Windows Autopilot 执行用户驱动的混合 Azure AD 联接的部署：

- 设备必须运行 Windows 10 版本1809或更高版本。 
- 必须创建用户驱动模式的 Windows Autopilot 配置文件，并 
 - 在 Autopilot 配置文件中，必须将**混合 Azure AD 联接**指定为 "**联接到 Azure AD** " 下的所选选项。
- 如果使用 Intune，Azure Active Directory 中的设备组必须与分配给该组的 Windows Autopilot 配置文件存在。
- 如果使用 intune，请创建并分配域加入配置文件。 域加入配置文件包括本地 Active Directory 域信息
- 设备必须有权访问 Active Directory 域控制器。 它必须连接到组织的网络。 它必须能够解析 AD 域和 AD 域控制器的 DNS 记录。 它必须能够与域控制器进行通信，以便对用户进行身份验证。
- 设备必须能够访问 Internet，遵循所 [述的 Windows Autopilot 网络要求](networking-requirements.md)。
- 必须安装 Active Directory 的 Intune 连接器。
 - 注意： Intune 连接器将执行本地 AD join。 因此，用户不需要本地 AD 联接权限。 这假设将连接器 [配置为代表用户执行此操作](/intune/windows-autopilot-hybrid#increase-the-computer-account-limit-in-the-organizational-unit) 。 
- 如果使用代理，必须启用并配置 WPAD 代理设置选项。

**Azure AD 设备加入**：混合 Azure AD 联接过程使用系统上下文来执行设备 Azure AD 加入。 它不受基于用户的 Azure AD 联接权限设置的影响。 默认情况下，所有用户都可以将设备加入 Azure AD。

## <a name="user-driven-mode-for-hybrid-azure-active-directory-join-with-vpn-support"></a>具有 VPN 支持的混合 Azure Active Directory 联接的用户驱动模式

加入到 Active Directory 的设备需要连接到 Active Directory 域控制器进行许多活动。 这些活动包括用户登录 (验证用户的凭据) 和组策略应用程序。 因此，Windows Autopilot 用户驱动混合 Azure AD 联接过程将验证设备是否能够通过 ping 域控制器与 Active Directory 域控制器联系。

在此方案中添加 VPN 支持后，可以将混合 Azure AD 联接进程配置为跳过连接性检查。 这样就不需要与 Active Directory 域控制器进行通信。 若要允许连接到组织的网络，Intune 会在用户尝试登录 Windows 之前提供所需的 VPN 配置。 


### <a name="requirements"></a>要求

以下附加要求适用于具有 VPN 支持的混合 Azure AD 联接：

- 受支持的 Windows 10 版本：
 - Windows 10 1903 + 12 月10日累积更新 (KB4530684、OS build 18362.535) 或更高版本 
 - Windows 10 1909 + 12 月10日累积更新 (KB4530684、OS build 18363.535) 或更高版本 
 - Windows 10 2004 或更高版本 
- 启用混合 Azure AD 联接 Autopilot 配置文件中的新 "跳过域连接检查" 切换。
- VPN 配置：
  - 可以使用 Intune 进行部署，并允许用户通过 Windows 登录屏幕手动建立 VPN 连接，或
  - 一个根据需要自动建立 VPN 连接。 

所需的特定 VPN 配置取决于所使用的 VPN 软件和身份验证。 对于第三方 (非 Microsoft) VPN 解决方案，这通常涉及到部署包含 VPN 客户端软件本身的 Win32 应用 (和任何特定的连接信息，例如： VPN 终结点主机名称) 通过 Intune 管理扩展。 有关特定于提供程序的配置详细信息，请参阅 VPN 提供程序的文档。

> [!NOTE]
> VPN 要求并不特定于 Windows Autopilot。 例如，如果你已经实现了 VPN 配置来启用远程密码重置，而用户需要在不在组织网络中使用新密码登录到 Windows，则可以在 Windows Autopilot 中使用相同的配置。 用户登录以缓存其凭据后，后续登录尝试不需要连接，因为可以使用缓存的凭据。 

如果 VPN 软件需要证书身份验证，则还应通过 Intune 部署所需的计算机证书。 可以使用 Intune 证书注册功能完成此部署，将证书配置文件定向到设备。

用户证书不受支持，因为在用户登录之前无法部署它们。 此外，由于在用户登录后它们不会安装，因此不支持从 Windows 应用商店提供的非 Microsoft UWP VPN 插件。

### <a name="validation"></a>验证

尝试使用 VPN 进行混合 Azure AD 联接之前，请务必确认是否可以在组织的网络上执行用户驱动的混合 Azure AD 联接进程。 此确认可在添加所需的其他 VPN 配置之前确保核心过程正常运行，从而简化了故障排除。

接下来，验证是否可以使用 Intune 向已加入混合 Azure AD 的现有设备部署 VPN 配置 (Win32 应用、证书和其他任何要求) 。 例如，某些 VPN 客户端会在安装过程中创建每台计算机的 VPN 连接。 因此，你可以使用以下步骤验证配置：

- 在 PowerShell 中，验证是否已使用 "VpnConnection-AllUserConnection" 命令创建了至少一台每台计算机 VPN 连接。
- 尝试使用以下命令手动启动 VPN 连接： RASDIAL.EXE "ConnectionName"
- 注销并验证是否可以在 Windows 登录页上查看 "VPN 连接" 图标。
- 将设备移出公司网络，尝试使用 Windows 登录页上的图标建立连接。 登录到没有缓存的凭据的帐户。

对于自动连接的 VPN 配置，验证步骤可能会有所不同。

> [!NOTE]
> Always On VPN 可用于此方案。 有关详细信息，请参阅 [部署 ALWAYS ON VPN](/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy-deployment) 文档。 请注意，Intune 尚未部署所需的每个计算机 VPN 配置文件。 

若要验证该过程，请确保在 Windows 10 1903 或 Windows 10 1909 上安装了所需的 Windows 10 累积更新。 您可以通过先从下载最新的累积性，在 OOBE 期间手动安装更新 https://catalog.update.microsoft.com 。 执行以下步骤:

1. 按 Shift-F10 打开命令提示符。
2. 插入包含已下载更新的 USB 密钥。
3. 使用命令安装更新 (替换真实文件名) ： WUSA.EXE <filename> msu/quiet
4. 使用以下命令重新启动计算机： shutdown.exe/r/t 0

或者，你可以开始 Windows 更新来安装最新的更新：

1. 按 Shift-F10 打开命令提示符。
2. 运行命令 "start ms-settings："
3. 导航到 "更新 & 安全" 节点并检查更新。
4. 安装更新后重新启动。

### <a name="step-by-step-instructions"></a>分步说明

请参阅 [使用 Intune 和 Windows Autopilot 部署混合 Azure AD 加入的设备](/intune/windows-autopilot-hybrid)。
