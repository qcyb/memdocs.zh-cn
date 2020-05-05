---
title: 在本地 MDM 中管理设备
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 本地移动设备管理（MDM），通过完全擦除、选择性擦除、远程锁定或密码重置保护设备数据。
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9849f3bef5aa67dcc45b00f64487242230edc2e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724721"
---
# <a name="manage-devices-and-protect-data-with-on-premises-mdm-in-configuration-manager"></a>在 Configuration Manager 中利用本地 MDM 管理设备和保护数据

适用范围：  Configuration Manager (Current Branch)

移动设备可以存储敏感数据并提供对许多组织资源的轻松访问。 若要帮助保护设备和数据，请使用 Configuration Manager 以下设备管理操作：

- **完全擦除**：将设备还原为其出厂设置

- **选择性擦除**：仅删除组织数据

- **密码重置**：在用户忘记密码时删除或重置密码

- **远程锁定**：帮助保护可能丢失的设备

## <a name="full-wipe"></a>完全擦除  

如果需要保护丢失的设备或停用正在使用的设备，可以在其上启动完全擦除。 此操作可将设备还原为其出厂默认设置。 它删除所有组织和用户数据和设置。

1. 在 Configuration Manager 控制台中，请在 "**资产和符合性**" 工作区中，选择 "**设备**" 节点。 你还可以选择 "**设备集合**" 并选择设备所属的集合。

1. 选择要擦除的设备。

1. 在功能区的 "设备" 组中，选择 "**远程设备操作**"，然后选择 "**停用/擦除**"。

1. 在 "**停用 Configuration Manager** " 窗口中，选择 "**擦除移动设备并将其从 Configuration Manager 中停**用" 选项。

## <a name="selective-wipe"></a>选择性擦除

若要仅从设备中删除组织数据，请启动选择性擦除。

### <a name="behaviors-by-os-version"></a>按 OS 版本的行为

下表描述了在选择性擦除后删除哪些数据以及对设备上保留的数据的影响。

#### <a name="windows-10-windows-81-windows-rt-81-and-windows-rt"></a>Windows 10、Windows 8.1、Windows RT 8.1 和 Windows RT

|内容|选择性擦除行为|  
|-------|--------|
|Configuration Manager 安装的应用和关联的数据|它将卸载应用程序，并删除所有旁加载密钥。 它将吊销使用 Windows 选择性擦除的应用的加密密钥，并且数据将不再可访问。|
|VPN 和 Wi-Fi 配置文件|删除配置文件|
|证书|删除和吊销证书|
|设置|删除要求|
|电子邮件配置文件|删除启用了 EFS 的电子邮件，其中包括适用于 Windows 电子邮件的邮件应用以及附件。|

#### <a name="windows-10-mobile-windows-phone-80-and-windows-phone-81"></a>Windows 10 移动版、Windows Phone 8.0 和 Windows Phone 8.1

|内容|选择性擦除行为|  
|-------|--------|
|Configuration Manager 安装的公司应用和关联的数据|它将卸载应用并删除组织应用数据。|
|VPN 和 Wi-Fi 配置文件|删除 Windows 10 移动版和 Windows Phone 8.1 的配置文件|
|证书|删除 Windows Phone 8.1 的证书|
|电子邮件配置文件|删除配置文件（Windows Phone 8.0）|

还从 Windows 10 移动版和 Windows Phone 8.1 设备删除了以下设置：  

- **需要密码才可解锁移动设备**  
- **允许简单密码**  
- **最短密码长度**  
- **所需的密码类型**
- **密码过期（天数）**  
- **记住密码历史**  
- **擦除设备前允许的重复登录失败次数**  
- **需要提供密码之前处于非活动状态的分钟数**  
- **所需密码类型 - 最小字符集数**  
- **允许相机**
- **需要对移动设备加密**  
- **允许使用可移动存储**  
- **允许使用 Web 浏览器**  
- **允许应用程序商店**  
- **允许屏幕捕获**  
- **允许使用地理位置**  
- **允许 Microsoft 帐户**  
- **允许复制和粘贴**  
- **允许使用 Wi-Fi tethering**  
- **允许自动连接到免费 Wi-Fi 热点**  
- **允许 Wi-Fi 热点报告**  
- **允许恢复出厂设置**
- **允许使用蓝牙**  
- **允许使用 NFC**
- **允许 Wi-Fi**

### <a name="start-a-selective-wipe"></a>开始选择性擦除

1. 在 Configuration Manager 控制台中，请在 "**资产和符合性**" 工作区中，选择 "**设备**" 节点。 你还可以选择 "**设备集合**" 并选择设备所属的集合。

1. 选择要擦除的设备。

1. 在功能区的 "设备" 组中，选择 "**远程设备操作**"，然后选择 "**停用/擦除**"。

1. 在 "**停用 Configuration Manager** " 窗口中，选择以下选项： "**擦除公司内容" 和 "从 Configuration Manager 中停用移动设备"**。

### <a name="recommendations-for-selective-wipe"></a>选择性擦除建议

- 若要成功擦除电子邮件，请设置电子邮件配置文件以 Windows Phone 8.1 设备。

- 确保通过移动设备应用管理分发了应用，以便成功擦除应用。

## <a name="passcode-reset"></a>密码重置

如果用户忘记了自己的密码，请使用此操作在设备上强制使用新的临时密码。 你还可以完全删除密码。 下表列出了在不同移动平台上重置密码的方法。

| OS 版本 | 密码重置 |
|------------|----------------|
| Windows 10 | 不支持 |
| Windows 10 移动版 | 支持，排除 Azure Active Directory 联接的设备 |
| Windows Phone 8 和 Windows Phone 8.1 | 支持 |
| Windows RT 8.1 | 不支持 |
| Windows 8.1 | 不支持 |

> [!Note]
> 从顶层站点启动密码重置操作。 例如，如果你使用管理中心站点，则只能在该站点上执行操作。 如果你使用的是独立主站点，则只能从该站点执行操作。

### <a name="remotely-reset-the-passcode-on-a-mobile-device"></a>远程重置移动设备上的密码

1. 在 Configuration Manager 控制台中，请在 "**资产和符合性**" 工作区中，选择 "**设备**" 节点。 你还可以选择 "**设备集合**" 并选择设备所属的集合。

1. 选择要重置密码的一台或多台设备。

1. 在功能区的 "设备" 组中，选择 "**远程设备操作**"，然后选择 "**密码重置**"。  

### <a name="show-the-state-of-the-passcode-reset"></a>显示密码重置状态  

1. 在 Configuration Manager 控制台中，请在 "**资产和符合性**" 工作区中，选择 "**设备**" 节点。 你还可以选择 "**设备集合**" 并选择设备所属的集合。

1. 选择要显示密码重置状态的一台或多台设备。

1. 在功能区的 "设备" 组中，选择 "**远程设备操作**"，然后选择 "**显示密码状态**"。  

## <a name="remote-lock"></a>远程锁定

如果用户丢失其设备，你可以远程锁定该设备。 下表列出了是如何在不同的移动平台上进行远程锁定的。  

|OS 版本|远程锁定|
|----------|-----------|
|Windows 10|不支持|
|Windows Phone 8 和 Windows Phone 8.1|支持|
|Windows RT 8.1|如果设备的当前用户是注册设备的相同用户，则支持。|
|Windows 8.1|如果设备的当前用户是注册设备的相同用户，则支持。|

> [!Note]
> 从顶层站点启动 "远程锁定" 操作。 例如，如果你使用管理中心站点，则只能在该站点上执行操作。 如果使用的是独立主站点，请从该站点执行操作。

### <a name="remotely-lock-a-mobile-device"></a>远程锁定移动设备

1. 在 Configuration Manager 控制台中，请在 "**资产和符合性**" 工作区中，选择 "**设备**" 节点。 你还可以选择 "**设备集合**" 并选择设备所属的集合。

1. 选择要锁定的一台或多台设备。

1. 在功能区的 "设备" 组中，选择 "**远程设备操作**"，然后选择 "**远程锁定**"。 确认操作。

### <a name="show-the-state-of-the-remote-lock"></a>显示远程锁定状态

1. 在 Configuration Manager 控制台中，请在 "**资产和符合性**" 工作区中，选择 "**设备**" 节点。 你还可以选择 "**设备集合**" 并选择设备所属的集合。

1. 选择要显示远程锁定状态的设备。

1. 在功能区的 "设备" 组中，选择 "**远程设备操作**"，然后选择 "**显示远程锁定状态**"。
