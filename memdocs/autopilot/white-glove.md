---
title: 用于白手套部署的 Windows Autopilot
description: 用于白手套部署的 Windows Autopilot
keywords: mdm，安装程序，windows，windows 10，oobe，管理，部署，autopilot，ztd，零接触，合作伙伴，msfb，intune，预配
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: low
ms.sitesec: library
ms.pagetype: deploy
audience: itproF
manager: laurawi
ms.audience: itpro
author: greg-lindsay
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: e08c69412fef2149d71c684fed6b900b88c9cb60
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756115"
---
# <a name="windows-autopilot-for-white-glove-deployment"></a>用于白手套部署的 Windows Autopilot

**适用于： Windows 10，版本1903** 

Windows Autopilot 使组织能够轻松地预配新的设备-利用预安装的 OEM 映像和驱动程序，该过程可由最终用户执行，以帮助其设备企业就绪。

 ![OEM](images/wg01.png)

Windows Autopilot 还可以提供一个<I>白色的手套</I>服务，让合作伙伴或 IT 人员预配 WINDOWS 10 PC，使其完全配置和业务就绪。 从最终用户的角度来看，Windows Autopilot 用户驱动的体验是不变的，但使其设备进入完全预配状态的速度更快。

通过**Windows Autopilot for 白手套部署**，将拆分预配过程。 由 IT、合作伙伴或 Oem 执行耗时的部分。 最终用户只需完成一些必要的设置和策略，然后就可以开始使用其设备。

 ![OEM](images/wg02.png)

在 Windows 10 版本1903及更高版本中 Microsoft Intune 启用，手套部署功能在现有 Windows Autopilot[用户驱动方案](user-driven.md)之上构建，同时支持用于 Azure Active Directory 联接的用户驱动模式模式，以及混合 Azure Active Directory 加入方案的用户驱动模式。

## <a name="prerequisites"></a>先决条件

除了[Windows Autopilot 要求](windows-autopilot-requirements.md)外，windows Autopilot for 白手套部署还添加了以下内容：

- 需要 Windows 10 版本1903或更高版本。
- Intune 订阅。
- 支持 TPM 2.0 和设备证明的物理设备;不支持虚拟机。  白色手套预配过程利用 Windows Autopilot 的自部署功能，因此需要 TPM 2.0。
- 具有以太网连接的物理设备;由于需要选择语言、区域设置和键盘来建立 Wi-fi 连接，因此不支持 wi-fi 连接;在预配过程中执行此操作可以防止用户在收到设备时选择自己的语言、区域设置和键盘。

>[!IMPORTANT]
>因为 OEM 或供应商执行了白色的手套过程，所以这<u>不需要访问最终用户的本地域基础结构</u>。 这不同于典型的混合 Azure AD 联接方案，因为重新启动设备会被延迟。 设备在与域控制器之间建立连接时 resealed，并在最终用户对设备进行取消装箱本地时联系到域网络。

## <a name="preparation"></a>准备

为手套预配预配的设备是通过正常注册过程为 Autopilot 注册的。 

若要准备尝试使用 Windows Autopilot 进行白手套部署，请确保你可以首先成功使用现有的 Windows Autopilot 用户驱动方案：

- 用户驱动的 Azure AD 联接。  可以使用 Windows Autopilot 部署设备，并将其加入 Azure Active Directory 租户。
- 用户驱动的混合 Azure AD 联接。  可以使用 Windows Autopilot 部署设备，并将其加入本地 Active Directory 域，然后向 Azure Active Directory 注册，以启用混合 Azure AD 加入功能。

如果无法完成这些方案，则 Windows Autopilot for 白色手套部署也将不会成功，因为它基于这些方案进行构建。

若要启用白手套部署，必须在预配服务设施中开始使用白色手套过程之前，由客户或 IT 管理员通过其 Intune 帐户配置附加的 Autopilot 配置文件设置：

 ![允许白色手套](images/allow-white-glove-oobe.png)

Windows Autopilot for 手套 deployment 预配过程将应用 Intune 提供的所有设备目标策略。  这包括证书、安全模板、设置、应用，等等–面向设备的任何内容。  此外，还将安装配置为安装在设备上下文中并面向已预先分配到 Autopilot 设备的用户的任何应用 (Win32 或 LOB) 。 请确保不要将 win32 和 LOB 应用程序都定位到相同的设备。 

> [!NOTE]
> 选择 "语言模式" 作为 "Autopilot 配置文件" 中指定的用户，以确保轻松访问白手套预配模式。 "白手套技术人员" 阶段将安装所有面向设备的应用以及以指定用户为目标的所有用户目标设备上下文应用。 如果没有分配的用户，则它将只安装设备目标应用。 在用户登录到设备之前，将不会应用其他用户目标策略。 若要验证这些行为，请确保创建针对设备和用户的相应应用和策略。

## <a name="scenarios"></a>方案

Windows Autopilot for 白色手套部署支持两种不同的方案：
- 具有 Azure AD 联接的用户驱动的部署。  设备将加入 Azure AD 租户。
- 具有混合 Azure AD 联接的用户驱动的部署。  设备将加入本地 Active Directory 域，并分别注册到 Azure AD 中。
其中每个方案都由两个部分组成：技术人员流和用户流。  在高级别中，这些部件对于 Azure AD 联接和混合 Azure AD 联接是相同的;差异主要由最终用户在身份验证步骤中查看。

### <a name="technician-flow"></a>技术员 flow

当客户或 IT 管理员通过 Intune 将他们所需的所有应用和设置定向到其设备后，手套技术人员可以开始使用白色手套过程。  技术人员可以是 IT 人员、服务合作伙伴或 OEM 的成员–每个组织都可以决定应该执行这些活动的人员。 无论方案如何，技术人员执行的过程都是相同的：
- 启动设备 (运行 Windows 10 专业版、企业版或教育版 Sku) 版本1903或更高版本。
- 在第一个 OOBE 屏幕 (可能是语言选择或区域设置选择屏幕) ，请不要单击 "**下一步**"。  而是按 Windows 键5次以查看其他选项对话框。  在该屏幕中，选择 " **Windows Autopilot 预配**" 选项，然后单击 "**继续**"。

  ![choice](images/choice.png)

- 在**Windows Autopilot 配置**屏幕上，将显示有关设备的信息：
    - 分配给设备的 Autopilot 配置文件。
    - 设备的组织名称。
    - 如果有一个) ，则分配给设备 (的用户。
    - 一个 QR 码，其中包含设备的唯一标识符，用于在 Intune 中查找设备以进行任何所需的配置更改 (例如，分配用户，将设备添加到应用或策略目标) 所需的任何其他组。
    - **注意**：可以使用辅助应用扫描 QR 码，这也会将设备配置为指定其所属的用户。  Autopilot 团队已将与 Intune 集成的[伴随应用的开源示例](https://github.com/Microsoft/WindowsAutopilotCompanion)通过图形 API 发布到 GitHub。
- 验证显示的信息。  如果需要进行任何更改，请进行更改，然后单击 "**刷新**" 以重新下载更新后的 Autopilot 配置文件详细信息。

  ![登录](images/landing.png)

- 单击 "**预配**" 开始预配过程。

如果预配过程成功完成：
- 此时会显示一个绿色状态屏幕，其中包含有关设备的信息，其中包括前面所述的相同细节 (例如 Autopilot profile、组织名称、已分配用户、QR 码) ，以及预配步骤的运行时间。
 ![手套-结果](images/white-glove-result.png)
- 单击 "重新**封装**" 关闭设备。  此时，可以将设备寄送到最终用户。

>[!NOTE]
>技术员 Flow 继承[自部署模式](self-deploying.md)的行为。 在自行部署模式文档中，它利用 "注册状态" 页将设备置于预配状态，并防止用户在注册之后但在应用软件和配置之前继续进入桌面。 因此，如果 "注册状态" 页处于禁用状态，则在完成 "软件和配置" 之前，可能会出现 "重新封装" 按钮，使用户可以在完成技术流设置之前继续执行用户流。 绿色屏幕验证注册是否成功，而不是必须完成技术人员流。

如果预配过程失败：
- 此时将显示一个红色状态屏幕，其中包含有关设备的信息，其中包括前面介绍的相同细节 (例如 Autopilot profile、组织名称、已分配的用户、QR 码) ，以及预配步骤的运行时间。
- 诊断日志可以从设备收集，然后可以重置，以便重新启动该过程。

### <a name="user-flow"></a>用户流

如果预配过程已成功完成，并且设备已 resealed，则可以将其传递给最终用户，以完成正常的 Windows Autopilot 用户驱动过程。  它们将执行一组标准步骤：

- 打开设备电源。
- 选择相应的语言、区域设置和键盘布局。
- 如果使用 Wi-fi) ，请连接到网络 (。  始终需要 Internet 访问。  如果使用混合 Azure AD 联接，则还必须连接到域控制器。
- 在 "署名登录" 屏幕上，输入用户的 Azure Active Directory 凭据。
- 如果使用混合 Azure AD 联接，则设备将重新启动;重新启动后，输入用户的 Active Directory 凭据。
- 其他策略和应用会传递到设备，由 "注册状态" 页 (ESP) 跟踪。  完成后，用户将能够访问桌面。

## <a name="related-topics"></a>相关主题

[白色手套视频](https://youtu.be/nE5XSOBV0rI)
