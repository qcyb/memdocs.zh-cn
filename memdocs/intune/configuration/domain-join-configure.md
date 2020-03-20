---
title: Microsoft Intune 中适用于 Windows 10 的域加入配置文件设置 - Azure | Microsoft Docs
description: 为已加入混合 Azure AD 的设备创建域加入设备配置文件。 使用此配置文件将本地 Active Directory 域信息部署到使用 Windows Autopilot 和 Microsoft Intune 预配的设备。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 207b3983c214ad4e166ae58ea0ccd18ea23bf418
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79364391"
---
# <a name="configuration-domain-join-settings-for-hybrid-azure-ad-joined-devices-in-microsoft-intune"></a>Microsoft Intune 中适用于已加入混合 Azure AD 的设备的配置域加入设置

许多环境使用本地 Active Directory (AD)。 当已加入 AD 域的设备同时加入到 Azure AD 时，它们被称为已加入混合 Azure AD 的设备。 使用 Windows Autopilot，可以在 Intune 中[注册已加入混合 Azure AD 的设备](../enrollment/windows-autopilot-hybrid.md)。 若要注册，还需要“域加入”配置文件  。

“域加入”配置文件包括本地 Active Directory 域信息  。 当设备正在预配（且通常处于脱机状态）时，此配置文件会部署 AD 域详细信息，以便设备知道要加入哪个本地域。 如果不创建域加入配置文件，这些设备可能无法部署。

此功能适用于：

- Windows 10 及更高版本
- 已加入混合 Azure AD 的设备
- 通过 Autopilot + Intune 进行混合部署

本文介绍了如何为混合 Autopilot 部署创建域加入配置文件。 你还可以查看可用的设置。

## <a name="create-the-profile"></a>创建配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备”   > “配置文件”   > “创建配置文件”  。
3. 输入以下属性：

    - **名称**：输入策略的描述性名称。 为策略命名，以便稍后可以轻松地识别它们。 例如，将策略名称命名为“Windows 10:  域加入配置文件，其中包含本地域信息，用于向 Windows Autopilot 注册已加入混合 AD 的设备”就很不错。
    - **描述**：输入策略的说明。 此设置是可选的，但建议进行。
    - **平台**：选择“Windows 10 及更高版本”  。
    - **配置文件类型**：选择“域加入(预览版)”  。

4. 选择“设置”  。 输入以下属性：

    - **计算机名称前缀**：输入设备名称的前缀。 计算机名称长度为 15 个字符。 前缀后的剩余 15 个字符是随机生成的。
    - **域名**：输入设备要加入的完全限定的域名 (FQDN)。 例如，输入 `americas.corp.contoso.com.`
    - **组织单位**（可选）：输入要在其中创建计算机帐户的组织单位 (OU) 的完整路径（[可分辨名称](https://docs.microsoft.com/windows/win32/ad/object-names-and-identities#distinguished-name)）。 例如，输入 `"CN=Users,DC=Contoso,DC=com"`。 如果未输入值，则使用已知的计算机对象容器。

      有关此设置的详细信息和建议，请参阅[部署已加入混合 Azure AD 的设备](../enrollment/windows-autopilot-hybrid.md)。

5. 完成后，选择“确定”   > “创建”  以保存所做的更改。

此时，配置文件创建完成，并出现在配置文件列表中。 现在，可以[使用 Intune 和 Windows Autopilot 部署已加入混合 Azure AD 的设备](../enrollment/windows-autopilot-hybrid.md)。

## <a name="next-steps"></a>后续步骤

创建配置文件后，即可进行分配。 下一步，[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

[使用 Intune 和 Windows Autopilot 部署已加入混合 Azure AD 的设备](../enrollment/windows-autopilot-hybrid.md)。
