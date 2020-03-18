---
title: 通过 Microsoft Intune 使用 PIN 登录 Windows 10 设备 - Azure | Microsoft Docs
description: 使用 Windows Hello 企业版，用户可使用 PIN、指纹等登录设备。 在 Intune 中为包含这些设置的 Windows 10 设备创建标识保护配置文件，并将配置文件分配到用户组和设备组。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/18/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c64a860a8d132fafac575545c16573c5fa0c940b
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79352002"
---
# <a name="use-windows-hello-for-business-on-windows-10-devices-with-microsoft-intune"></a>结合使用 Windows 10 设备上的 Windows Hello 企业版与 Microsoft Intune

Windows Hello 企业版是一种取代密码、智能卡和虚拟智能卡登录 Windows 设备的方法。 Intune 包括内置设置，因此管理员可以配置和使用 Windows Hello 企业版。 例如，这些设置可用于：

- 为设备和用户启用 Windows Hello 企业版
- 设置设备 PIN 要求，包括 PIN 长度下限或上限
- 允许使用用户可以（或不能）用来登录设备的指纹等手势

此功能适用于运行以下版本的设备：

- Windows 10 及更高版本
- Windows 10 移动版
- Windows Holographic for Business

Intune 使用“配置文件”创建和自定义这些设置，从而满足组织需求。 在配置文件中添加这些功能后，将这些设置推送或部署到组织中的用户组和设备组。

本文介绍了如何创建设备配置文件。 有关所有设置及其用途的列表，请参阅[启用 Windows Hello 企业版的 Windows 10 设备设置](identity-protection-windows-settings.md)。

## <a name="create-the-device-profile"></a>创建设备配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择“设备”   > “配置文件”   > “创建配置文件”  。

3. 输入以下属性：

   - **名称**：输入新配置文件的描述性名称。
   - **描述**：输入配置文件的说明。 此设置是可选的，但建议进行。
   - **平台**：选择“Windows 10 及更高版本”  。 仅运行 Windows 10 及更高版本的设备支持 Windows Hello 企业版。
   - **配置文件类型**：选择“标识保护”  。

4. 在“Windows Hello 企业版”  窗格中，配置以下选项：

   - **配置 Windows Hello 企业版**：选择要如何配置 Windows Hello 企业版：

     - **未配置**（默认）：在设备上[预配 Windows Hello 企业版](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-how-it-works-provisioning)。 在仅向用户分配标识保护配置文件时，设备上下文将默认为“未配置”  。

     - **已禁用**：如果不想使用 Windows Hello 企业版，请选择此选项。 此选项对所有用户禁用 Windows Hello 企业版。

     - **启用**：选择此选项可以在 Intune 中[预配](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-how-it-works-provisioning)并配置 Windows Hello 企业版设置。 输入要配置的设置。 有关所有设置及其用途的列表，请参阅[启用 Windows Hello 企业版的 Windows 10 设备设置](identity-protection-windows-settings.md)。

   - **使用安全密钥登录**：启用 Windows Hello 安全密钥作为租户中所有 PC 的登录凭据。

     - **启用**
     - **未配置**（默认）

5. 完成后，选择“确定”   > “创建”  以保存所做的更改。

此时，配置文件创建完成，并出现在配置文件列表中。 接下来，将此配置文件[分配](../configuration/device-profile-assign.md)给用户和设备组，以满足需求。

> [!IMPORTANT]
> 要允许将多个用户预配到设备，请指定将 Windows Hello for Business 策略应用到设备。 如果策略仅应用于用户，则只能将一个用户预配到一个设备。

<!--  Removing image as part of design review; retaining source until we known the disposition.

## Example of device restriction settings

In this high-level example, you'll create a device restriction policy that blocks the use of the built-in camera app on Android devices.

![How to disable the camera on Android devices](./media/identity-protection-configure/disable-android-camera.png)

-->

## <a name="next-steps"></a>后续步骤

- 查看所有[设置及其用途](identity-protection-windows-settings.md)的列表。
- [分配配置文件](../configuration/device-profile-assign.md)并[监视其状态](../configuration/device-profile-monitor.md)。
