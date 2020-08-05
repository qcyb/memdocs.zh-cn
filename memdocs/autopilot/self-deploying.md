---
title: Windows Autopilot 自部署模式
description: 自部署模式允许部署设备，几乎不需要用户交互。 此模式模式旨在将 Windows 10 作为展台、数字告示设备或共享设备进行部署。
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
ms.openlocfilehash: 5fccc36ff1ecacaee3d2aa3ed7c317faaaefc113
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756122"
---
# <a name="windows-autopilot-self-deploying-mode"></a>Windows Autopilot 自部署模式

**适用于： Windows 10 版本1903或更高版本**

Windows Autopilot 自部署模式允许部署设备，几乎不需要用户交互。 对于具有以太网连接的设备，无需用户交互;对于通过 Wi-fi 连接的设备，建立 Wi-fi 连接后不需要进行任何交互 (选择语言、区域设置和键盘，然后) 建立网络连接。  

自部署模式将设备加入到 Azure Active Directory、在 Intune 中注册设备 (或另一个 MDM 服务) 利用 Azure AD 进行自动 MDM 注册，并确保在设备上预配所有策略、应用程序、证书和网络配置文件，并利用 "注册状态" 页来阻止访问桌面，直到设备完全预配。 

>[!NOTE]
>自部署模式不支持 Active Directory 联接或混合 Azure AD 联接。  所有设备将加入到 Azure Active Directory。

自部署模式旨在将 Windows 10 部署为展台、数字告示设备或共享设备。 设置展台时，你可以利用新的展台浏览器，这是一个基于 Microsoft Edge 构建的应用，可用于创建一个定制的 MDM 管理的浏览体验。 与 MDM 策略结合使用来创建本地帐户并将其配置为自动登录时，可以自动完成设备的完整配置。 阅读使用 Windows 10 简化展台管理，了解有关这些选项的详细信息。  有关更多详细信息，请参阅[在 Intune 或其他 MDM 服务中设置展台或数字签名](https://docs.microsoft.com/windows/configuration/setup-kiosk-digital-signage#set-up-a-kiosk-or-digital-sign-in-intune-or-other-mdm-service)。

>[!NOTE]
>自部署模式目前不会将用户与设备 (相关联，因为未在进程) 中指定用户 ID 或密码。  因此，某些 Azure AD 和 Intune 功能 (例如 BitLocker 恢复、从公司门户安装应用或条件访问) 可能对登录到设备的用户不可用。 有关详细信息，请参阅[Windows Autopilot 方案和功能](windows-autopilot-scenarios.md)和[为 Autopilot 设备设置 BitLocker 加密算法](bitlocker.md)。

![Windows Autopilot 自行部署模式的用户体验](images/self-deploy-welcome.png)

## <a name="requirements"></a>要求

由于自我部署模式使用设备的 TPM 2.0 硬件向组织的 Azure AD 租户中对设备进行身份验证，因此不能在此模式下使用不带 TPM 2.0 的设备。  设备还必须支持 TPM 设备证明。   (所有新生产的 Windows 设备应满足这些要求。 ) 

>[!IMPORTANT]
>如果在不支持 TPM 2.0 的设备上或在虚拟机上尝试自行部署模式部署，则在使用0x800705B4 超时错误验证设备时，该过程将失败 (不支持 Hyper-v 虚拟 Tpm) 。 另请注意，由于 Windows 10 版本1809中的 TPM 设备证明存在问题，因此需要使用 Windows 10 版本1903或更高版本。 由于 Windows 10 企业版 2019 LTSC 基于 Windows 10 版本1809，Windows 10 Enterprise 2019 LTSC 也不支持自部署模式。 若要查看其他已知的错误和解决方案，请参阅[Windows Autopilot 的已知问题](known-issues.md)。

为了在 Autopilot 过程中显示组织特定的徽标和组织名称，需要使用应显示的图像和文本来配置 Azure Active Directory 公司品牌。  有关更多详细信息，请参阅["快速入门：将公司品牌添加到 Azure AD 中的登录页"](https://docs.microsoft.com/azure/active-directory/fundamentals/customize-branding) 。 

## <a name="step-by-step"></a>分步操作

为了使用 Windows Autopilot 执行自我部署模式部署，需要完成以下准备步骤：

-   使用所需的设置创建自部署模式的 Autopilot 配置文件。  在 Microsoft Intune 中，将在创建配置文件时显式选择此模式。  (请注意，无法在企业或合作伙伴中心的 Microsoft Store 中为自部署模式创建配置文件。 ) 
-   如果使用 Intune，请在 Azure Active Directory 中创建一个设备组，并将 Autopilot 配置文件分配给该组。  尝试部署设备之前，请确保已将该配置文件分配到设备。
-   启动设备，如有必要，将其连接到 Wi-fi，然后等待预配过程完成。

## <a name="validation"></a>验证

使用 Windows Autopilot 执行自我部署模式部署时，应遵循以下最终用户体验：

-   连接到网络后，将下载 Autopilot 配置文件。
-   如果将 Autopilot 配置文件配置为自动配置语言、区域设置和键盘布局，则只要以太网连接可用，就会跳过这些 OOBE 屏幕。  否则，需要手动步骤：
    -   如果在 Windows 10 中预安装了多种语言，则用户必须选择一种语言。
    -   用户必须选取区域设置和键盘布局，并选择性地选择另一种键盘布局。
-   如果通过以太网连接，则不需要网络提示。  如果没有可用的以太网连接，并且在中内置了 Wi-fi，则用户需要连接到无线网络。
-   Windows 10 会检查是否有关键的 OOBE 更新，如果有任何可用的更新，则会自动安装 (重新启动（如果需要）) 。
-   设备将联接 Azure Active Directory。
-   加入 Azure Active Directory 之后，设备将在 Intune (或其他配置的 MDM 服务) 中进行注册。
-   将显示 "[注册状态" 页](enrollment-status.md)。
-   根据所部署的设备设置，设备将：
    -   在登录屏幕上，组织的任何成员都可以通过指定其 Azure AD 凭据进行登录。
    -   对于配置为展台或数字告示的设备，自动以本地帐户身份登录。

>[!NOTE]
>对于展台部署，使用自部署模式部署 EAS 策略将导致自动登录功能失败。 

如果观察到的结果与这些预期不符，请参阅[Windows Autopilot 故障排除](troubleshooting.md)文档。
