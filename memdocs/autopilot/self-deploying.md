---
title: Windows Autopilot 自部署模式
description: 自部署模式允许部署设备，几乎不需要用户交互。 此模式旨在将 Windows 10 部署为展台、数字告示设备或共享设备。
keywords: mdm, 设置, windows, windows 10, oobe, 管理, 部署, autopilot, ztd, 零接触, 合作伙伴, msfb, intune
ms.reviewer: mniehaus
manager: laurawi
ms.technology: windows
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
ms.openlocfilehash: 13b45b972ed17d24efedaa048c0e48ea2f2d90d2
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90568607"
---
# <a name="windows-autopilot-self-deploying-mode"></a>Windows Autopilot 自部署模式

**适用于： Windows 10 版本1903或更高版本**

Windows Autopilot 自部署模式使你可以部署设备，几乎不需要用户交互。 对于具有以太网连接的设备，无需用户交互。 对于通过 Wi-fi 连接的设备，用户只能：
- 选择语言、区域设置和键盘。
- 建立网络连接。 

自部署模式提供以下所有内容：
- 将设备加入到 Azure Active Directory。
- 使用 Azure AD 自动进行 MDM 注册，在 Intune (或另一个 MDM 服务) 中注册设备。
- 确保在设备上预配所有策略、应用程序、证书和网络配置文件。
- 使用 "注册状态" 页来阻止访问，直到设备完全预配。

>[!NOTE]
>自部署模式不支持 Active Directory 联接或混合 Azure AD 联接。 所有设备将加入到 Azure Active Directory。

通过自我部署模式，你可以将 Windows 10 设备部署为展台、数字告示设备或共享设备。

设置展台设备时，可以使用 [展台浏览器](https://www.microsoft.com/p/kiosk-browser/9ngb5s5xg2kp?rtc=1&activetab=pivot:overviewtab) 。 此应用构建于 Microsoft Edge 之上，可用于创建一个定制的 MDM 管理的浏览体验。

可以通过将 deploing 模式与 MDM 策略结合使用来完全自动完成设备配置。 使用 MDM 策略创建配置为自动登录的本地帐户。 有关详细信息，请参阅：
- [通过 Windows 10 简化展台管理](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/simplifying-kiosk-management-for-it-with-windows-10/ba-p/187691)。
- [在 Intune 或其他 MDM 服务中设置展台或数字签名](/windows/configuration/setup-kiosk-digital-signage#set-up-a-kiosk-or-digital-sign-in-intune-or-other-mdm-service)。

>[!NOTE]
>自部署模式目前不会将用户与设备 (相关联，因为未在进程) 中指定用户 ID 或密码。 因此，某些 Azure AD 和 Intune 功能 (例如 BitLocker 恢复、从公司门户安装应用或条件访问) 可能对登录到设备的用户不可用。 有关详细信息，请参阅 [Windows Autopilot 方案和功能](windows-autopilot-scenarios.md) 和 [为 Autopilot 设备设置 BitLocker 加密算法](bitlocker.md)。

![Windows Autopilot 自行部署模式的用户体验](images/self-deploy-welcome.png)

## <a name="requirements"></a>要求

自部署模式使用设备的 TPM 2.0 硬件向组织的 Azure AD 租户中对设备进行身份验证。 因此，不能在此模式下使用不带 TPM 2.0 的设备。 设备还必须支持 TPM 设备证明。 所有新的 Windows 设备都应满足这些要求。

>[!IMPORTANT]
>如果在不支持 TPM 2.0 的设备上或在虚拟机上尝试自行部署模式部署，则在使用0x800705B4 超时错误验证设备时，该过程将失败 (不支持 Hyper-v 虚拟 Tpm) 。 另请注意，由于 Windows 10 版本1809中的 TPM 设备证明存在问题，因此需要使用 Windows 10 版本1903或更高版本。 由于 Windows 10 企业版 2019 LTSC 基于 Windows 10 版本1809，Windows 10 Enterprise 2019 LTSC 也不支持自部署模式。 若要查看其他已知的错误和解决方案，请参阅 [Windows Autopilot 的已知问题](known-issues.md) 。

你可以在 Autopilot 过程中显示组织特定的徽标和组织名称。 为此，必须将 Azure AD 公司品牌配置为包含要显示的图像和文本。 有关更多详细信息，请参阅 ["快速入门：将公司品牌添加到 Azure AD 中的登录页"](/azure/active-directory/fundamentals/customize-branding) 。 

## <a name="step-by-step"></a>分步操作

若要在自部署模式下部署 Windows Autopilot，需要完成以下准备步骤：

1. 使用所需的设置创建自部署模式的 Autopilot 配置文件。 在 Microsoft Intune 中，将在创建配置文件时显式选择此模式。 无法在适用于企业或合作伙伴中心的 Microsoft Store 中创建配置文件进行自我部署。
2. 如果使用 Intune，请在 Azure Active Directory 中创建一个设备组，并将 Autopilot 配置文件分配给该组。 尝试部署设备之前，请确保已将该配置文件分配到设备。
3. 启动设备，如有必要，将其连接到 Wi-fi，然后等待预配过程完成。

## <a name="validation"></a>验证

使用 Windows Autopilot 在自我部署模式下部署时，应遵循以下最终用户体验：

-  连接到网络后，将下载 Autopilot 配置文件。
- 如果连接到以太网，并将 Autopilot 配置文件配置为跳过这些配置文件，则不会显示以下页面：语言、区域设置和键盘布局。 否则，需要手动步骤：
  -  如果在 Windows 10 中预安装了多种语言，则用户必须选择一种语言。
  -  用户必须选取区域设置和键盘布局，并选择性地选择另一种键盘布局。
-  如果通过以太网连接，则不需要网络提示。 如果没有可用的以太网连接，并且在中内置了 Wi-fi，则用户需要连接到无线网络。
-  Windows 10 会检查重要的 OOBE 更新，如果有任何可用的更新，则会自动安装 (重新启动（如有必要）) 。
-  设备将联接 Azure Active Directory。
-  加入 Azure Active Directory 之后，设备将在 Intune (或其他配置的 MDM 服务) 中进行注册。
-  将显示 " [注册状态" 页](enrollment-status.md) 。
-  根据所部署的设备设置，设备将：
  -  在登录屏幕上，组织的任何成员都可以通过指定其 Azure AD 凭据进行登录。
  -  对于配置为展台或数字告示的设备，自动以本地帐户身份登录。

>[!NOTE]
>对于展台部署，使用自部署模式部署 EAS 策略将导致自动登录功能失败。 

如果观察到的结果与这些预期不符，请参阅 [Windows Autopilot 故障排除](troubleshooting.md) 文档。
