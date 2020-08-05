---
title: Windows Autopilot 重置
description: Windows Autopilot Reset 使设备恢复到业务就绪状态，允许下一个用户登录并快速轻松地进行工作。
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
ms.openlocfilehash: 8388febead5953fd6c76e7e40571d3b2e1b91e4d
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756109"
---
# <a name="windows-autopilot-reset"></a>Windows Autopilot 重置

- 适用于： Windows 10 版本1709和更高版本 (本地重置) 
- 适用于： Windows 10 版本1809和更高版本 (远程重置) 

Windows Autopilot Reset 删除个人文件、应用和设置，并重新应用设备的原始设置，并将其标识连接 Azure AD 及其与 Intune 的管理连接，使设备能够再次准备好使用。 Windows Autopilot Reset 使设备恢复到业务就绪状态，使下一个用户可以登录并迅速获得工作效率。 

Windows Autopilot 重置过程自动保留现有设备中的信息：
 
-   将区域、语言和键盘设置为最初配置的值。
-   Wi-fi 连接详细信息。
-   预配包以前应用到设备，并在启动重置过程时在 USB 驱动器上提供预配包。 
-   Azure Active Directory 设备成员身份和 MDM 注册信息。

Windows Autopilot Reset 会阻止用户访问桌面，直到还原此信息，包括重新应用任何预配包。  对于在 MDM 服务中注册的设备，Windows Autopilot Reset 还会在 MDM 同步完成之前阻止。  
如果设备使用 Autopilot 重置，设备的主要用户将会遭删除。 在重置后登录的下一个用户将被设置为主要用户。
 
 
>[!NOTE]
>Autopilot 重置不支持已联接的设备混合 Azure AD。

## <a name="scenarios"></a>方案

Windows Autopilot Reset 支持两种方案：

-   IT 人员或组织中的其他管理员启动的[本地重置](#reset-devices-with-local-windows-autopilot-reset)。
-   IT 人员通过 MDM 服务（如 Microsoft Intune）远程启动[远程重置](#reset-devices-with-remote-windows-autopilot-reset)。

其他要求和配置详细信息适用于每个方案;有关详细信息，请参阅上面的详细链接。

## <a name="reset-devices-with-local-windows-autopilot-reset"></a>用本地 Windows Autopilot 重置设备 

**适用于： Windows 10，版本1709及更高版本**

需要 Intune 服务管理员角色才能执行此任务。  有关详细信息，请参阅[添加用户并授予对 Intune 的管理权限](https://docs.microsoft.com/intune/users-add)。

IT 管理员可以执行本地 Windows Autopilot Reset，以快速删除个人文件、应用和设置，并随时从锁定屏幕重置 Windows 10 设备，并将原始设置和管理注册 (Azure Active Directory 和设备管理) ，使设备可供使用。 使用本地 Autopilot 重置时，设备将返回到完全配置或已知 IT 批准状态。

在 Windows 10 中启用本地 Autopilot 重置：

1. [启用该功能的策略](#enable-local-windows-autopilot-reset)
2. [为每台设备触发重置操作](#trigger-local-windows-autopilot-reset)

### <a name="enable-local-windows-autopilot-reset"></a>启用本地 Windows Autopilot 重置

若要启用本地 Windows Autopilot Reset，必须配置**DisableAutomaticReDeploymentCredentials**策略。 [策略 CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-credentialproviders)， **CredentialProviders/DisableAutomaticReDeploymentCredentials**中介绍了此策略。 默认情况下，本地 Windows Autopilot 处于禁用状态。 这可确保不会因意外触发本地 Autopilot 重置。

你可以使用以下方法之一设置此策略：

- MDM 提供程序

    - 使用 Intune 时，你可以创建新的设备配置文件，并为平台指定 "Windows 10 或更高版本"、配置文件类型的 "设备限制" 和 "常规" 作为 "设置" 类别。  **自动重新部署**设置应设置为 "**允许**"。  将此设置部署到应允许本地重置的所有设备。
    - 如果你使用的是 Intune 以外的 MDM 提供程序，请查看 MDM 提供程序文档以了解如何设置此策略。 

- Windows 配置设计器

    你可以[使用 Windows 配置设计器](https://docs.microsoft.com/windows/configuration/provisioning-packages/provisioning-create-package)将**运行时设置 > 策略 > CredentialProviders > DisableAutomaticReDeploymentCredentials**设置设置为0，然后创建预配包。

- “设置学校电脑”应用

    "设置 School Pc" 应用的最新版本支持启用本地 Windows Autopilot Reset。

### <a name="trigger-local-windows-autopilot-reset"></a>触发本地 Windows Autopilot Reset

执行本地 Windows Autopilot 重置是一个两步过程：触发它然后进行身份验证。 完成这两个步骤后，就可以执行该过程，并在完成后再使用该设备。 

**触发本地 Autopilot 重置**

1. 从 Windows 设备锁屏界面上，按下以下键：**CTRL + ![Windows 键](images/windows_glyph.png) + R**。 

    ![在 Windows 锁屏界面上输入 CTRL + Windows 键 + R](images/autopilot-reset-lockscreen.png)

    这会打开一个自定义登录屏幕，用于本地 Autopilot 重置。 该屏幕有两个用途：
    1. 确认/验证最终用户是否有权触发本地 Autopilot Reset
    2. 如果使用 Windows 配置设计器创建的预配包将用作该过程的一部分，则通知用户。

    ![用于本地 Autopilot 重置的自定义登录屏幕](images/autopilot-reset-customlogin.png)

2. 使用管理员凭据登录。 如果你创建了一个预配包，请插入该 u 盘，并触发本地 Autopilot 重置。

    一旦触发了本地 Autopilot 重置，就会启动重置过程。 预配完成后，设备将重新可供使用。

## <a name="reset-devices-with-remote-windows-autopilot-reset"></a>重置具有远程 Windows Autopilot 的设备

**适用于： Windows 10 版本1809或更高版本**

执行远程 Windows Autopilot 重置时，可以使用 MDM 服务之类的 Microsoft Intune 来启动重置过程，从而使 IT 员工或其他管理员无需访问每台计算机即可启动该过程。

若要为远程 Windows Autopilot Reset 启用设备，该设备必须是 MDM 管理的并且加入到 Azure AD。 使用[Autopilot self 部署模式](self-deploying.md)注册的设备不支持此功能。

### <a name="triggering-a-remote-windows-autopilot-reset"></a>触发远程 Windows Autopilot Reset

若要通过 Intune 触发远程 Windows Autopilot 重置，请执行以下步骤：
 
-   在 Intune 控制台中导航到 "**设备**" 选项卡。 
-   在 "**所有设备**" 视图中，选择目标重置设备，然后单击 "**更多**" 以查看设备操作。 
-   选择**Autopilot "重置**" 以启动重置任务。 

>[!NOTE]
>对于未运行 Windows 10 版本17672或更高版本的设备，Microsoft Intune 中将不会启用 Autopilot Reset 选项。

>[!IMPORTANT]
>Autopilot 重置功能将保持灰显，**除非**使用 Autopilot 重置设备 (使用全新重置或手动 sysprep 设备) 。

重置完成后，设备将再次可供使用。
 


## <a name="troubleshooting"></a>疑难解答

Windows Autopilot Reset 要求在设备上正确配置和启用[Windows 恢复环境 (WinRE) ](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference) 。 如果未对其进行配置和启用，则会报告诸如这样的错误 `Error code: ERROR_NOT_SUPPORTED (0x80070032)` 。

若要确保启用 WinRE，请使用[REAgentC.exe 工具](https://docs.microsoft.com/windows-hardware/manufacture/desktop/reagentc-command-line-options)运行以下命令：

```
reagentc /enable
```

如果在启用 WinRE 后 Windows Autopilot 重置失败，或者如果无法启用 WinRE，请联系[Microsoft 支持部门](https://support.microsoft.com)获取帮助。
