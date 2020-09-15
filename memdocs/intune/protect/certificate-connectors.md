---
title: 适用于 Microsoft Intune 的 C 证书连接器 - Azure | Microsoft Docs
description: 了解 Microsoft Intune 与简单证书注册协议 (SCEP) 或公钥加密标准 (PKCS) 证书和证书配置文件的证书连接器。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9f891e7989ad3f0f8d798dd9a5f0207a19ac5b95
ms.sourcegitcommit: b95eac00a0cd979dc88be953623c51dbdc9327c5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89428888"
---
# <a name="certificate-connectors-for-microsoft-intune"></a>Microsoft Intune 的证书连接器

为支持使用证书进行身份验证以及使用 S/MIME 对电子邮件进行签名和加密，Intune 要求使用证书连接器。 证书连接器是你在本地服务器上安装的软件。 连接器使云托管设备可以从本地基础结构（例如正在颁发证书的颁发机构）预配证书。

本文介绍可用的连接器及其生命周期和使用先决条件，以及如何使其保持最新状态。  

## <a name="available-connectors"></a>可用连接器

Intune 有两个证书连接器。 它们各有自己的用途和要求。

### <a name="pfx-certificate-connector-for-microsoft-intune"></a>Microsoft Intune 的 PFX 证书连接器

PFX 证书连接器支持针对 PKCS #12 证书请求的证书部署，并处理对导入到 Intune 中的 PFX 文件的请求，从而为特定用户实现 S/MIME 电子邮件加密。

> [!TIP]
> 在此连接器的 8 月更新之前，由 Intune 证书连接器处理 PKCS #12 证书请求。 在 8 月更新中，PFX 证书连接器中合并了所有 PKCS 证书请求的功能，该功能支持将连接器自动更新为新版本，并且要求使用 .NET Framework 4.7.2 版。
>
> Microsoft Intune 连接器的功能并未弃用，可以继续将其用于 PKCS 证书配置文件。 但如果不使用 SCEP 或以其他方式要求使用 NDES，可以切换到 PFX 证书连接器并从服务器删除 NDES。 

**PFX 证书连接器**：

- 为每个 Intune 租户支持此连接器的多个实例。 连接器的每个实例必须安装在 Windows Server 上，并且可以访问用于加密上传的 PFX 文件的密码的私钥。
- 可以安装在托管 Microsoft Intune 连接器实例的服务器上。
- 支持[自动更新](#automatic-update)为新版本。 若要自动安装新版本，托管连接器的计算机必须在端口 443 上访问 autoupdate.msappproxy.net 。 如果连接器未能自动更新，你可以手动更新连接器。
- 支持证书吊销（需要连接器运行版本 6.2008.60.607 或更高版本）
- 网络要求与[受管理设备](../fundamentals/intune-endpoints.md#access-for-managed-devices)相同

  有关详细信息，请参阅 [Microsoft Intune 的网络终结点](../fundamentals/intune-endpoints.md)和 [Intune 网络配置要求和带宽](../fundamentals/network-bandwidth-use.md)。

**安装连接器的 Windows 服务器**：

- 必须运行 Windows Server 2012 R2 或更高版本。
- 运行 .NET 4.7.2 Framework。  

**若要安装 PFX 证书连接器**：

有关此连接器的安装指南，请参阅[下载、安装和配置 PFX 证书连接器](certficates-pfx-configure.md)。

### <a name="microsoft-intune-connector"></a>Microsoft Intune 连接器

Microsoft Intune 连接器有时也称为 Microsoft Intune 证书连接器。 在你使用简单证书注册协议 (SCEP) 并具有 Active Directory 证书服务证书颁发机构 (CA) 时，此连接器支持证书部署。 这一类型的 CA 也称为 Microsoft CA。

结合使用 SCEP 和 Microsoft CA 时，你还必须配置网络设备注册服务 (NDES)。 因此，此连接器通常称为 NDES 证书连接器。

如果你使用[第三方证书颁发机构](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration)，则无需使用此连接器和 NDES。

**Microsoft Intune 连接器**：

- 安装在还可以托管 PFX 证书连接器实例的 Windows 服务器上。
- 支持每个租户最多有此连接器的 100 个实例，每个实例位于不同的 Windows Server 上。 使用多个连接器时：
  - 环境中 Microsoft Intune 连接器的所有实例都应为同一版本。
  - 基础结构支持冗余和负载均衡，因为任何可用连接器实例都可以处理证书请求。
- 需要[手动更新](#manual-update)才能安装新版连接器。 手动更新需要卸载当前的连接器，然后才能安装新版连接器。 不需要其他操作。
- 支持美国联邦信息处理标准 (FIPS) 模式。 FIPS 不是必需的。 启用 FIPS 后，就可颁发和吊销证书。
- 网络要求与[受管理设备](../fundamentals/intune-endpoints.md#access-for-managed-devices)相同。

  有关详细信息，请参阅 [Microsoft Intune 的网络终结点](../fundamentals/intune-endpoints.md)和 [Intune 网络配置要求和带宽](../fundamentals/network-bandwidth-use.md)。

**安装连接器的 Windows 服务器**：

- 必须运行 Windows Server 2012 R2 或更高版本。
- 运行 .NET 4.5 Framework。 此连接器与 PFX 证书连接器安装在同一服务器上时，必须使用 .NET 4.7.2 Framework，这是 PFX 连接器的要求。
- 不能是托管正在颁发的证书颁发机构 (CA) 的服务器。
- 与 Microsoft CA 一起用于 SCEP 时，需要能够访问运行 NDES 的服务器。 NDES 在 Windows 服务器上运行，并且可以与此连接器在同一服务器上运行。

**如果 NDES 是必需的**：

- 必须在托管 NDES 和 Microsoft Intune 连接器的服务器上[禁用](/previous-versions/windows/it-pro/windows-server-2003/cc775800(v=ws.10)) Internet Explorer 增强型安全配置。
- 连接器需要其他配置才能与 NDES 通信。 你将找到安装和配置 NDES 的流程以及安装 Microsoft Intune 连接器的流程。

  有关 NDES 的详细信息，请参阅[网络设备注册服务指南](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498(v=ws.11))。

**若要安装 Microsoft Intune 连接器**：

有关安装此连接器的指南，请参阅[配置基础结构以支持在 Intune 中使用 SCEP](certificates-scep-configure.md)。

## <a name="connector-lifecycle"></a>连接器生命周期

定期发布更新版的证书连接器。 新版连接器的公告显示在 Intune 的[新增功能](../fundamentals/whats-new.md)一文中，以及本文结尾处的[连接器的新增功能](#whats-new-for-connectors)部分。

发布新版本后，弃用对旧版本的支持，可在有限的宽限期内继续使用旧版本。 宽限期到期时，终止对该弃用版本的支持，并且可能会随时停止运行。 宽限期为六个月。

计划尽快将连接器更新为最新版本。 每个连接器都有不同的更新路径：

- **Microsoft Intune 的 PFX 证书连接器** - 支持自动更新。
- **Microsoft Intune 连接器** - 需要手动更新。

### <a name="automatic-update"></a>自动更新

如果受连接器类型和环境支持，Intune 可以在发布该连接器版本后立即将连接器自动更新为最新版本。  

若要自动更新，托管连接器的服务器必须访问 Azure 更新服务：

- 端口：**443**
- 终结点：autoupdate.msappproxy.net

如果防火墙、基础结构或网络配置限制自动更新，请解决阻塞性问题或将连接器手动更新为新版本。

### <a name="manual-update"></a>手动更新

手动更新证书连接器的流程与重新安装连接器的流程相同。

即使证书连接器支持自动更新，你也可以手动更新。 例如，当网络配置阻止自动更新时，可以手动更新连接器。  

### <a name="to-reinstall-a-certificate-connector"></a>重新安装证书连接器

1. 在托管连接器的 Windows 服务器上，使用“Windows 应用和功能”卸载连接器。

2. 若要安装新版本，请按以下流程安装新版连接器。 安装较新版本的连接器时，请务必检查是否有任何新增的或更新的先决条件：
   - SCEP：[配置基础结构以支持在 Intune 中使用 SCEP](certificates-scep-configure.md)
   - PKCS：[下载、安装和配置 Microsoft Intune 的 PFX 证书连接器](certficates-pfx-configure.md)

## <a name="connector-status-and-version"></a>连接器状态和版本

在 Microsoft Endpoint Manager 管理中心，可以选择证书连接器以查看其状态信息并确认其版本：

1. 登录到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)

2. 转到“租户管理” > “连接器和令牌” > “证书连接器”  。

3. 选择连接器以查看其状态。

查看连接器状态时：

- 已弃用的连接器旁边将显示警告。 六个月的宽限期到期后，该警告将变为错误。
- 超出宽限期的连接器将显示错误。 这些连接器不再受支持，并且随时可能停止工作。

## <a name="whats-new-for-connectors"></a>连接器的新增功能

我们将定期发布这两个证书连接器的更新。 更新连接器时，你可以在此处阅读有关更改的信息。

### <a name="pfx-certificate-connector-release-history"></a>PFX 证书连接器版本历史记录

Microsoft Intune 的 PFX 证书连接器[支持自动更新](#automatic-update)。

#### <a name="august-26-2020"></a>2020 年 8 月 26 日

**版本 6.2008.60.607** - 此版本中的更改：

- 需要 .NET Framework 版本 4.7.2
- 请替换 Microsoft Intune 连接器，以与 PKCS 证书配置文件一起使用。 目前，PFX 证书连接器是使用 PKCS #12 或导入的 PFX 证书所需的唯一连接器。
- 添加了对在除 Windows 8.1 以外的所有支持平台上使用 PKCS 证书配置文件的支持。
- 添加了对 Outlook S/MIME 的证书吊销的支持。

#### <a name="november-18-2019"></a>2019 年 11 月 18 日

**版本：6.1911.11.602** - 此版本中的更改：

- 添加了对 PFX 导入的 S/MIME 支持。  

#### <a name="may-17-2019"></a>2019 年 5 月 17 日

**版本 6.1905.0.404** - 此版本中的更改：

- 修复了以下问题：因现有 PFX 证书持续重新处理而导致连接器停止处理新请求。 

#### <a name="may-6-2019"></a>2019 年 5 月 6 日

**版本 6.1905.0.402** - 此版本中的更改：

- 连接器的轮询间隔从 5 分钟降到了 30 秒。

#### <a name="april-2-2019"></a>2019 年 4 月 2日

**版本 6.1904.0.401** - 此版本中的更改：

- 此连接器目前支持自动更新。
- 解决了使用全局管理员帐户登录连接器后连接器可能无法注册到 Intune 的问题。

### <a name="microsoft-intune-connector-release-history"></a>Microsoft Intune 连接器版本历史记录

#### <a name="april-2-2019"></a>2019 年 4 月 2 日

**版本 6.1904.1.0** - 此版本中的更改：  

- 解决了使用全局管理员帐户登录连接器后连接器可能无法注册到 Intune 的问题。
- 包括证书吊销的可靠性修补程序。
- 包括性能修补程序，以提高处理 PKCS 证书请求的速度。

## <a name="next-steps"></a>后续步骤

为要使用的每个平台创建 SCEP、PKCS 或 PKCS 导入的证书配置文件。 请参阅以下文章进一步了解：

- [配置基础结构以支持在 Intune 中使用 SCEP 证书](certificates-scep-configure.md)  
- [使用 Intune 配置和管理 PKCS 证书](certficates-pfx-configure.md)  
- [创建 PKCS 导入的证书配置文件](certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)
