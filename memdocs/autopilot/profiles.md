---
title: 配置 Autopilot 配置文件
description: 了解如何在执行 Windows Autopilot 部署时配置设备配置文件。
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
ms.openlocfilehash: 648793f68aef98659d068009e278fe35dec062e4
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907965"
---
# <a name="configure-autopilot-profiles"></a>配置 Autopilot 配置文件

**适用于**

-   Windows 10

对于已定义为 Windows Autopilot 部署服务的每个设备，需要应用设置配置文件，以便在部署时指定该设备的确切行为。 有关如何配置配置文件设置和注册设备的详细过程，请参阅 [注册设备](add-devices.md#registering-devices)。

## <a name="profile-settings"></a>配置文件设置

提供以下配置文件设置：

-   **跳过 Cortana、OneDrive 和 OEM 注册设置页**。 注册到 Autopilot 的所有设备都会在 (OOBE) 进程的全新体验期间自动跳过这些页面。

-   **自动为工作或学校设置**。 注册到 Autopilot 的所有设备都被自动视为工作或学校设备，因此，在 OOBE 过程中不会出现此问题。

-   **公司品牌的登录体验**。 注册到 Autopilot 的所有设备将显示自定义的登录页，其中包含组织的名称、徽标和其他帮助文本（如 Azure Active Directory 中配置的那样），而不是显示通用 Azure Active Directory 登录页。 若要自定义这些设置，请参阅 [将公司品牌添加到你的目录](/azure/active-directory/customize-branding#add-company-branding-to-your-directory) 。

-   **跳过隐私设置**。 此可选的 Autopilot 配置文件设置使组织无在 OOBE 过程中询问隐私设置。 这通常是必需的，以便组织可以通过 Intune 或其他管理工具来配置这些设置。

-   **禁用设备上的本地管理员帐户创建**。 组织可决定在完成该过程后，设置设备的用户是否应具有管理员访问权限。

-   ** (EULA) ，跳过最终用户许可协议 **。 在 Windows 10 版本1709及更高版本中，组织可以决定跳过 OOBE 过程中显示的 EULA 页面。 这表示组织代表其用户接受 EULA 条款。

-   **禁用 Windows 使用者功能**。 在 Windows 10 版本1803及更高版本中，组织可禁用 Windows 消费者功能，以便在用户首次登录设备时，设备不会自动安装任何其他 Microsoft Store 应用。 有关详细信息，请参阅 [MDM 文档](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsconsumerfeatures)。

## <a name="related-topics"></a>相关主题

[配置文件下载](troubleshooting.md#profile-download)<br>
[注册设备](add-devices.md)