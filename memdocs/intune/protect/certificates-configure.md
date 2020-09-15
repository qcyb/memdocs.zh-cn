---
title: 在 Microsoft Intune 中创建证书配置文件 - Azure | Microsoft Docs
description: 介绍如何配合使用 Microsoft Intune 与简单证书注册协议 (SCEP) 或公钥加密标准 (PKCS) 证书和配置文件。
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
ms.assetid: 5eccfa11-52ab-49eb-afef-a185b4dccde1
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 22bfe44b95eedcdf87a41cfaaf959c72cfbe93e2
ms.sourcegitcommit: b95eac00a0cd979dc88be953623c51dbdc9327c5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89423809"
---
# <a name="use-certificates-for-authentication-in-microsoft-intune"></a>在 Microsoft Intune 中使用证书进行身份验证

使用 Intune 证书通过 VPN、Wi-Fi 或电子邮件配置文件向用户验证应用程序和公司资源。 使用证书对这些连接进行身份验证时，最终用户无需输入用户名和密码即可实现无缝访问。 证书还用于使用 S/MIME 对电子邮件进行签名和加密。

## <a name="intune-supported-certificates-and-usage"></a>Intune 支持的证书和使用情况

| 类型              | 身份验证 | S/MIME 签名 | S/MIME 加密  |
|--|--|--|--|
| 公钥加密标准 (PKCS) 导入证书 |  | ![支持](./media/certificates-configure/green-check.png) | ![支持](./media/certificates-configure/green-check.png)|
| PKCS#12（或 PFX）    | ![支持](./media/certificates-configure/green-check.png) | ![支持](./media/certificates-configure/green-check.png) |  |
| 简单证书注册协议 (SCEP)  | ![支持](./media/certificates-configure/green-check.png) | ![支持](./media/certificates-configure/green-check.png) | |

若要部署这些证书，需要创建证书配置文件并将其分配给设备。

创建的每个证书配置文件都支持单一平台。 例如，如果使用 PKCS 证书，则需要为 Android 创建 PKCS 证书配置文件，并为 iOS/iPadOS 创建单独的 PKCS 证书配置文件。 如果还对这两个平台使用 SCEP 证书，则需要为 Android 创建一个 SCEP 证书配置文件，并为 iOS/iPadOS 也创建一个。

### <a name="general-considerations-when-you-use-a-microsoft-certification-authority"></a>使用 Microsoft 证书颁发机构时的一般注意事项

使用 Microsoft 证书颁发机构 (CA) 时：

- 使用 SCEP 证书配置文件：
  - [设置网络设备注册服务 (NDES) 服务器](certificates-scep-configure.md#set-up-ndes)以便与 Intune 配合使用。
  - [安装 Microsoft 证书连接器](certificates-scep-configure.md#install-the-microsoft-intune-connector)：

- 若要使用 PKCS 证书配置文件，请执行以下操作：
  - [安装适用于 Microsoft Intune 的 PFX 证书连接器](certificates-imported-pfx-configure。
  
- 使用 PKCS 导入的证书：
  - [安装 Microsoft Intune 的 PFX 证书连接器](certificates-imported-pfx-configure.md#download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune)。
  - 从证书颁发机构导出证书，然后将其导入 Microsoft Intune。 请参阅 [PFXImport PowerShell 项目](https://github.com/Microsoft/Intune-Resource-Access/tree/develop/src/PFXImportPowershell)。

- 使用下列机制部署证书：
  - [受信任的证书配置文件](certificates-configure.md#create-trusted-certificate-profiles)可将受信任的根 CA 证书从根或中间（颁发）CA 部署到设备
  - SCEP 证书配置文件
  - PKCS 证书配置文件
  - PKCS 导入的证书配置文件

### <a name="general-considerations-when-you-use-a-third-party-certification-authority"></a>使用第三方证书颁发机构时的一般注意事项

使用第三方（非 Microsoft）证书颁发机构 (CA) 时：

- 使用 SCEP 证书配置文件：
  - 设置与来自[受支持合作伙伴之一](certificate-authority-add-scep-overview.md#third-party-certification-authority-partners)的第三方 CA 的集成。 设置包括按照第三方 CA 的说明完成其 CA 与 Intune 的集成。
  - [在 Azure AD 中创建应用程序](certificate-authority-add-scep-overview.md#set-up-third-party-ca-integration)，该应用程序将权限委派给 Intune 进行 SCEP 证书质询验证。

- PKCS 导入的证书需要[安装适用于 Microsoft Intune 的 PFX 证书连接器](certificates-imported-pfx-configure.md#download-install-and-configure-the-pfx-certificate-connector-for-microsoft-intune)。

- 使用下列机制部署证书：
  - [受信任的证书配置文件](certificates-configure.md#create-trusted-certificate-profiles)可将受信任的根 CA 证书从根或中间（颁发）CA 部署到设备
  - SCEP 证书配置文件
  - PKCS 证书配置文件（仅受 [Digicert PKI 平台](certificates-digicert-configure.md)支持）
  - PKCS 导入的证书配置文件

## <a name="supported-platforms-and-certificate-profiles"></a>支持的平台和证书配置文件

| 平台              | 受信任的证书配置文件 | PKCS 证书配置文件 | SCEP 证书配置文件 | PKCS 导入的证书配置文件  |
|--|--|--|--|---|
| Android 设备管理员 | ![支持](./media/certificates-configure/green-check.png) | ![支持](./media/certificates-configure/green-check.png) | ![支持](./media/certificates-configure/green-check.png)|  ![支持](./media/certificates-configure/green-check.png) |
| Android Enterprise <br> - 完全托管（设备所有者）   | ![支持](./media/certificates-configure/green-check.png) | ![支持](./media/certificates-configure/green-check.png)  | ![支持](./media/certificates-configure/green-check.png) |  ![支持](./media/certificates-configure/green-check.png)  |
| Android Enterprise <br> - 专用（设备所有者）   | ![支持](./media/certificates-configure/green-check.png)  | ![支持](./media/certificates-configure/green-check.png) | ![支持](./media/certificates-configure/green-check.png)  | ![支持](./media/certificates-configure/green-check.png)|
| Android Enterprise <br> - 公司拥有的工作配置文件   | ![支持](./media/certificates-configure/green-check.png)  | ![支持](./media/certificates-configure/green-check.png)  | ![支持](./media/certificates-configure/green-check.png)  | ![支持](./media/certificates-configure/green-check.png)  |
| Android Enterprise <br> - 工作配置文件    | ![支持](./media/certificates-configure/green-check.png) | ![支持](./media/certificates-configure/green-check.png) | ![支持](./media/certificates-configure/green-check.png) | ![支持](./media/certificates-configure/green-check.png) |
| iOS/iPadOS                   | ![支持](./media/certificates-configure/green-check.png) | ![支持](./media/certificates-configure/green-check.png) | ![支持](./media/certificates-configure/green-check.png) | ![支持](./media/certificates-configure/green-check.png) |
| macOS                 | ![支持](./media/certificates-configure/green-check.png) |  ![支持](./media/certificates-configure/green-check.png) |![支持](./media/certificates-configure/green-check.png)|![支持](./media/certificates-configure/green-check.png)|
| Windows 8.1 及更高版本 |![支持](./media/certificates-configure/green-check.png)  |  |![支持](./media/certificates-configure/green-check.png) |   |
| Windows 10 及更高版本  | ![支持](./media/certificates-configure/green-check.png) | ![支持](./media/certificates-configure/green-check.png) | ![支持](./media/certificates-configure/green-check.png) | ![支持](./media/certificates-configure/green-check.png) |

## <a name="export-the-trusted-root-ca-certificate"></a>导出受信任的根 CA 证书

若要使用 PKCS、SCEP 和 PKCS 导入的证书，设备必须信任根证书颁发机构。 若要建立信任，请将受信任的根 CA 证书以及任何中间证书或证书发证机构证书导出为公共证书 (.cer)。 可从颁发 CA 或信任颁发 CA 的任何设备获取这些证书。

若要导出证书，请参阅关于证书颁发机构的文档。 需要将公共证书导出为 .cer 文件。  请勿导出私钥（.pfx 文件）。

[创建受信任的证书配置文件](#create-trusted-certificate-profiles)以将该证书部署到设备时，将使用此 .cer 文件。

## <a name="create-trusted-certificate-profiles"></a>创建受信任的证书配置文件

必须先创建和部署受信任的证书配置文件，才能创建 SCEP、PKCS 或 PKCS 导入的证书配置文件。 将受信任的证书配置文件部署到接收其他证书配置文件类型的相同组，可确保每个设备都可以识别 CA 的合法性。 这包括针对 VPN、Wi-Fi 和电子邮件等的配置文件。

SCEP 证书配置文件直接引用受信任的证书配置文件。 PKCS 证书配置文件不直接引用受信任的证书配置文件，而是直接引用托管 CA 的服务器。 PKCS 导入的证书配置文件不直接引用受信任的证书配置文件，但可以在设备上使用它。 将受信任的证书配置文件部署到设备可确保建立此信任。 如果设备不信任根 CA，SCEP 或 PKCS 证书配置文件策略将失败。

为要支持的每个设备平台创建单独的受信任证书配置文件，就像对 SCEP、PKCS 和 PKCS 导入的证书配置文件执行的操作一样。

> [!IMPORTANT]
> 为平台 Windows 10 及更高版本创建的受信任的根配置文件在 Microsoft Endpoint Manager 管理中心内显示为平台 Windows 8.1 及更高版本的配置文件。 
>
> 这是受信任的证书配置文件的已知平台显示问题。 虽然配置文件显示的平台为 Windows 8.1 及更高版本，但它适用于 Windows 10 及更高版本。

> [!NOTE]
> Intune 中的“受信任证书”配置文件只能用于传递根证书或中间证书。 部署此类证书的目的是建立一个信任链。 Microsoft 不支持使用受信任的证书配置文件来传送根证书或中间证书以外的证书。 在 Intune 门户中选择受信任的证书配置文件时，可能会禁止你导入不被视为根证书或中间证书的证书。 即使你可以使用此配置文件类型导入和部署不是根证书或中间证书的证书，你也可能会在 iOS 和 Android 等不同平台之间遇到意外结果。

### <a name="to-create-a-trusted-certificate-profile"></a>要创建“可信证书”配置文件

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。

2. 选择并转到“设备” > “配置文件” > “创建配置文件”。

   ![导航到 Intune 并为受信任的证书创建新的配置文件](./media/certificates-configure/certificates-configure-profile-new.png)

3. 输入以下属性：
   - **平台**：选择将接收此配置文件的设备的平台。
   - **配置文件**：选择“受信任的证书”
  
4. 选择“创建”。

5. 在“基本信息”中，输入以下属性：
   - **名称**：输入配置文件的描述性名称。 为配置文件命名，以便稍后可以轻松地识别它们。 例如，配置文件名称最好是“整个公司的受信任证书配置文件”。
   - **描述**：输入配置文件的说明。 此设置是可选的，但建议进行。

6. 选择“下一步”  。

7. 在“配置设置”中，指定之前导出的受信任根 CA 证书的 .cer 文件。 

   从以下位置选择受信任证书的**目标存储区**（仅适用于 Windows 8.1 和 Windows 10 设备）：

   - **计算机证书存储区 - 根**
   - **计算机证书存储区 - 中间**
   - **用户证书存储区 - 中间**

   ![创建配置文件并上传受信任的证书](./media/certificates-configure/certificates-configure-profile-fill.png)

8. 选择“下一步”。

9. 在“作用域标记”（可选）中，分配一个标记以将配置文件筛选到特定 IT 组（如 `US-NC IT Team` 或 `JohnGlenn_ITDepartment`）。 有关范围标记的详细信息，请参阅[将 RBAC 和范围标记用于分布式 IT](../fundamentals/scope-tags.md)。

   选择“下一步”。

10. 在“分配”中，选择将接收配置文件的用户或组。 有关分配配置文件的详细信息，请参阅[分配用户和设备配置文件](../configuration/device-profile-assign.md)。

    选择“下一步”  。

11. （仅适用于 Windows 10）在“适用性规则”中，指定适用性规则以优化此配置文件的分配。 可以根据操作系统版本或设备版本来选择是否分配配置文件。

  有关详细信息，请参阅“在 Microsoft Intune 中创建设备配置文件”中的[适用性规则](../configuration/device-profile-create.md#applicability-rules)。

12. 在“查看并创建”中查看设置。 选择“创建”时，将保存所做的更改并分配配置文件。 该策略也会显示在配置文件列表中。

## <a name="additional-resources"></a>其他资源

- [分配设备配置文件](../configuration/device-profile-assign.md)  
- [使用 S/MIME 对电子邮件进行签名和加密](certificates-s-mime-encryption-sign.md)  
- [使用第三方证书颁发机构](certificate-authority-add-scep-overview.md)  

## <a name="next-steps"></a>后续步骤

为要使用的每个平台创建 SCEP、PKCS 或 PKCS 导入的证书配置文件。 请参阅以下文章进一步了解：

- [配置基础结构以支持在 Intune 中使用 SCEP 证书](certificates-scep-configure.md)  
- [使用 Intune 配置和管理 PKCS 证书](certficates-pfx-configure.md)  
- [创建 PKCS 导入的证书配置文件](certificates-imported-pfx-configure.md#create-a-pkcs-imported-certificate-profile)

了解[证书连接器](certificate-connectors.md)