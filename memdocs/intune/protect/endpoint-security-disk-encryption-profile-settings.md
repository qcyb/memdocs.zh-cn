---
title: Intune 终结点安全磁盘加密策略设置 |Microsoft Docs
description: Microsoft Intune 中 BitLocker 和 FileVault 的终结点安全磁盘加密策略设置
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: db23ee1742934e8545c03c529d6a05c13cc59f1a
ms.sourcegitcommit: 6ca5e75ed7a6fd2186fbe51c177960004d5ec81f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83633282"
---
# <a name="disk-encryption-policy-settings-for-endpoint-security-in-intune"></a>Intune 中终结点安全的磁盘加密策略设置

查看可在 Intune 终结点安全性节点中的“磁盘加密”策略的配置文件配置的设置，这些设置是[终结点安全策略](../protect/endpoint-security-policy.md)的一部分。

受支持的平台和配置文件：

- **macOS**：
  - 配置文件：**FileVault**
- **Windows 10 及更高版本**：
  - 配置文件：**BitLocker**

## <a name="filevault"></a>FileVault

### <a name="encryption"></a>加密

**启用 FileVault**  
- **未配置**（默认）
- **是** - 在运行 macOS 10.13 及更高版本的设备上，通过 FileVault 使用 XTS-AES 128 启用全磁盘加密。 当用户注销设备时，将启用 FileVault。

  设置为“是”时，可配置 FileVault 的其他设置。

  - **恢复密钥类型**
    个人密钥：为设备创建恢复密钥。 为个人密钥配置以下设置：

    - **个人恢复密钥轮替**  
      指定设备的个人恢复密钥的轮替频率。 可以选择默认的“未配置”，或选择 1 到 12 个月其中一个值  。
    - **个人恢复密钥的托管位置说明**  
      指定一条发给用户的简短消息，向他们说明如何检索个人恢复密钥。 当用户因忘记密码而被提示输入个人恢复密钥时，他们会在登录屏幕上看到此消息。

  - **允许的免验证次数**  
    设置在系统要求用户提供 FileVault 才能登录之前用户可忽略“启用 FileVault”提示的次数。
    - **未配置**（默认）- 需要在设备上进行加密，才能允许下次登录。
    - 1 到 10 - 允许用户在要求对设备进行加密之前忽略 1 到 10 次的提示 。
    - **无限制，始终提示** - 系统会提示用户启用 FileVault，但绝不要求加密。

  - **允许推迟到注销后**  
    - **未配置**（默认）
    - **是** - 推迟到用户注销后再显示启用 FileVault 的提示。  

  - **禁止在注销时提示**  
    禁止在用户注销时提示他们启用 FileVault。如果设置为“禁用”，则会禁止在用户注销时提示，而在用户登录时提示。
    - **未配置**（默认）
    - **是** - 禁止在用户注销时向其显示启用 FileVault 的提示。

## <a name="bitlocker"></a>BitLocker

### <a name="bitlocker--base-settings"></a>BitLocker - 基本设置

- **对 OS 和固定数据驱动器启用全磁盘加密**  
  CSP：[RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  如果在应用此策略之前已对驱动器进行了加密，则不会执行额外的操作。 如果加密方法和选项与此策略匹配，则配置应返回成功。 如果就地 BitLocker 配置选项与此策略不匹配，则配置可能会返回错误。
  
  要将此策略应用到已加密的磁盘，请解密该驱动器，然后重新应用 MDM 策略。 默认情况下，Windows 不需要 BitLocker 驱动器加密。 但在加入 Azure AD 和注册/登录 Microsoft 帐户 (MSA) 时，可能会应用自动加密，从而启用 XTS-AES 128 位加密的 BitLocker。

  - **未配置**（默认） - 不强制使用 BitLocker。
  - **是** - 强制使用 BitLocker。

- **需要加密存储卡(仅限移动设备)**  
  CSP：[RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  此设置仅适用于 Windows Mobile 和 Mobile Enterprise SKU 设备。
  - **未配置**（默认） - 设置会返回到 OS 默认设置，即不需要存储卡加密。
  - **是** - 移动设备需要加密存储卡。

- **隐藏关于第三方加密的提示**  
  CSP：[AllowWarningForOtherDiskEncryption](https://go.microsoft.com/fwlink/?linkid=872525)

  如果在已由第三方加密产品加密的系统上启用 BitLocker，可能会导致设备不可用。 数据可能会丢失，并且可能需要重新安装 Windows。 强烈建议不要在已安装或启用第三方加密的设备上启用 BitLocker。

  默认情况下，BitLocker 安装向导会提示用户确认没有进行第三方加密。

  - **未配置**（默认） - BitLocker 安装向导将显示警告，并提示用户确认不存在第三方加密。
  - **是** - 不向用户显示 BitLocker 安装向导提示。

  如果需要“BitLocker 无提示启用”功能，则必须隐藏第三方加密警告，因为任何所需的提示都将中断无提示启用工作流。

  设置为“是”时，可配置以下设置：

  - **允许标准用户在 Autopilot 期间启用加密**  
    CSP：[AllowStandardUserEncryption](https://go.microsoft.com/fwlink/?linkid=2114200)
    - **未配置**（默认） - 在 Azure Active Directory 加入 (AADJ) 无提示启用方案中，用户无需成为本地管理员即可启用 BitLocker。
    - **是** - 设置保留为客户端默认值，需要具备本地管理员访问权限才能启用 BitLocker。

    对于有提示启用和 Autopilot 方案，用户必须是本地管理员才能完成 BitLocker 安装向导。

- **启用客户端驱动的恢复密码**  
  CSP：[ConfigureRecoveryPasswordRotation](https://go.microsoft.com/fwlink/?linkid=2114201)

  密钥轮替不支持“添加工作帐户”（缩写为 AWA，正式称为“已加入工作区”）设备。
  - **未配置**（默认） - 客户端不轮换 BitLocker 恢复密钥。
  - **禁用**
  - **已加入 Azure AD 的设备**
  - **已加入 Azure AD 和混合的设备**

### <a name="bitlocker---fixed-drive-settings"></a>BitLocker - 固定驱动器设置

- **BitLocker 固定驱动器策略**  
  [BitLocker 组策略设置](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **固定驱动器恢复**  
    CSP：[FixedDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872538)

    控制在缺少必需的启动密钥信息时如何恢复受 BitLocker 保护的固定数据驱动器。

    - **未配置**（默认） - 支持数据恢复代理 (DRA) 等默认恢复选项。 最终用户可指定恢复选项，而且恢复信息不备份到 Azure Active Directory。
    - **配置** - 启用访问权限来配置各种驱动器恢复技术。

    设置为“配置”时，可使用以下设置：

    - **用户创建恢复密钥**  
      - **已阻止**（默认）
      - **必需**
      - **允许**

    - **配置 BitLocker 恢复包**
      - **密码和密钥**（默认） - 包含 Active Directory 中管理员和用户用于解锁受保护的驱动器的 BitLocker 恢复密码，以及管理员用于恢复数据的恢复密钥包。
      - **仅密码** - 恢复密钥包可能在需要时无法访问。

    - **要求设备将恢复信息备份到 Azure AD**
      - **未配置**（默认） - 即使恢复密钥未能备份到 Azure AD，也将启用 BitLocker。 这可能会导致不在外部存储恢复信息。
      - **是** - 在将恢复密钥成功保存到 Azure Active Directory 之前，BitLocker 不会启用。

    - **用户创建恢复密码**  
      - **已阻止**（默认）
      - **必需**
      - **允许**

    - **在 BitLocker 安装期间隐藏恢复选项**
      - **未配置**（默认） - 允许用户访问其他恢复选项。
      - **是** - 阻止最终用户在 BitLocker 安装向导中选择其他恢复选项（例如打印恢复密钥）。

    - **存储恢复信息后启用 BitLocker**
      - **未配置**（默认）  
      - **是**

    - **阻止使用基于证书的数据恢复代理 (DRA)**
      - **未配置**（默认） - 允许设置 DRA 的使用。 要设置 DRA，需要使用企业 PKI 和组策略对象来部署 DRA 代理和证书。
      - **是** - 阻止使用数据恢复代理 (DRA) 来恢复已启用 BitLocker 的驱动器。

  - **阻止对不受 BitLocker 保护的固定数据驱动器的写权限**  
    CSP：[FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    此设置在“BitLocker 固定驱动器策略”设置为“配置”时可用 。

    - **未配置**（默认）- 可将数据写入非加密的固定驱动器。
    - **是** - Windows 将不允许向不受 BitLocker 保护的固定驱动器写入任何数据。 如果未对固定驱动器进行加密，则在授予写入权限之前，用户将需要完成驱动器的 BitLocker 安装向导。

  - **配置固定数据驱动器的加密方法**  
    CSP：[EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  

    配置固定数据驱动器磁盘的加密方法和密码长度。 XTS-AES 128 位是 Windows 默认加密方法和建议的值。

    - **未配置**（默认）
    - AES 128 位 CBC
    - AES 256 位 CBC
    - AES 128 位 XTS
    - AES 256 位 XTS

### <a name="bitlocker---os-drive-settings"></a>BitLocker - OS 驱动器设置

- **BitLocker 系统驱动器策略**  
  CSP：[BitLocker 组策略设置](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **配置**（默认）  
  - 未配置

  设置为“配置”时，可配置以下设置：

  - **需要启动身份验证**  
    CSP：[SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

    - **未配置**（默认）
    - **是** - 配置系统启动时的其他身份验证要求，包括使用受信任的平台模块 (TPM) 或启动 PIN 要求。

    设置为“是”时，可配置以下设置：

    - **兼容的 TPM 启动**  
      CSP：[SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      建议要求 BitLocker 使用 TPM。 此设置仅适用于首次启用 BitLocker 的情况；如果已启用 BitLocker，则不起作用。

      - **已阻止**（默认） - BitLocker 不使用 TPM。
      - **必需** - 仅当 TPM 存在且可用时，BitLocker 才启用。
      - **允许** - BitLocker 使用 TPM（若存在）。

    - **兼容的 TPM 启动 PIN**  
      CSP：[SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **已阻止**（默认） - 阻止使用 PIN。
      - **必需** - 需要使用 PIN 和 TPM 才能启用 BitLocker。
      - **允许** - BitLocker 使用 TPM（若存在），并允许用户配置启动 PIN。

      对于无提示启用方案，必须设置为“已阻止”。 需要用户交互时，无提示启用方案（包括 Autopilot）将失败。

    - **兼容的 TPM 启动密钥**  
      CSP：[SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **已阻止**（默认） - 阻止使用启动密钥。
      - **必需** - 需要使用启动密钥和 TPM 才能启用 BitLocker。
      - **允许** - BitLocker 使用 TPM（若存在），并允许存在配置启动密钥（例如 U 盘）来解锁驱动器。

      对于无提示启用方案，必须设置为“已阻止”。 需要用户交互时，无提示启用方案（包括 Autopilot）将失败。

    - **兼容的 TPM 启动密钥和 PIN**  
      CSP：[SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      - **已阻止**（默认） - 阻止组合使用启动密钥和 PIN。
      - **必需** - 要求 BitLocker 具有启动密钥和 PIN 才能启用。
      - **允许** - BitLocker 使用 TPM（若存在），并允许组合使用启动密钥和 PIN。

      对于无提示启用方案，必须设置为“已阻止”。 需要用户交互时，无提示启用方案（包括 Autopilot）将失败。

    - **在 TPM 不兼容的设备上禁用 BitLocker**  
    CSP：[SystemDrivesRequireStartupAuthentication](https://go.microsoft.com/fwlink/?linkid=872527)

      如果没有 TPM，则 BitLocker 需要使用密码或 U 盘才能启动。

      此设置仅适用于首次启用 BitLocker 的情况；如果已启用 BitLocker，则不起作用。

      - **未配置**（默认）
      - **是** - 在没有兼容的 TPM 芯片时阻止配置 BitLocker。

    - **启用预启动恢复消息和 URL**  
      CSP：[SystemDrivesRecoveryMessage](https://go.microsoft.com/fwlink/?linkid=872530) 配置

      - **未配置**（默认） – 使用默认的 BitLocker 预启动恢复信息。
      - **是** - 允许配置自定义预启动恢复消息和 URL，帮助用户了解如何查找其恢复密码。 当用户电脑在恢复模式下被锁定时，他们将看到预启动消息和 URL。

      设置为“是”时，可配置以下设置：

      - **预启动恢复消息**  
        指定自定义预启动恢复消息。

      - **预启动恢复 URL**  
        指定自定义预启动恢复 URL。

    - **系统驱动器恢复**  
      CSP：[SystemDrivesRecoveryOptions](https://go.microsoft.com/fwlink/?linkid=872529)

      - **未配置**（默认）  
      - **配置** - 启用其他设置的配置。

      设置为“配置”时，可使用以下设置：

      - **用户创建恢复密钥**  
        - **已阻止**（默认）
        - **必需**
        - **允许**

      - **配置 BitLocker 恢复包**
        - **密码和密钥**（默认） - 包含 Active Directory 中管理员和用户用于解锁受保护的驱动器的 BitLocker 恢复密码，以及管理员用于恢复数据的恢复密钥包。
        - **仅密码** - 恢复密钥包可能在需要时无法访问。

      - **要求设备将恢复信息备份到 Azure AD**
        - **未配置**（默认） - 即使恢复密钥未能备份到 Azure AD，也将启用 BitLocker。 这可能会导致不在外部存储恢复信息。
        - **是** - 在将恢复密钥成功保存到 Azure Active Directory 之前，BitLocker 不会启用。

      - **用户创建恢复密码**  
        - **已阻止**（默认）
        - **必需**
        - **允许**

      - **在 BitLocker 安装期间隐藏恢复选项**
        - **未配置**（默认） - 允许用户访问其他恢复选项。
        - **是** - 阻止最终用户在 BitLocker 安装向导中选择其他恢复选项（例如打印恢复密钥）。

      - **存储恢复信息后启用 BitLocker**
        - **未配置**（默认）  
        - **是**

      - **阻止使用基于证书的数据恢复代理 (DRA)**
        - **未配置**（默认） - 允许设置 DRA 的使用。 要设置 DRA，需要使用企业 PKI 和组策略对象来部署 DRA 代理和证书。
        - **是** - 阻止使用数据恢复代理 (DRA) 来恢复已启用 BitLocker 的驱动器。

    - **最小 PIN 长度**  
      CSP：[SystemDrivesMinimumPINLength](https://go.microsoft.com/fwlink/?linkid=872528)

      指定在 BitLocker 启用期间需要 TPM + PIN 时启动 PIN 的最小长度。 PIN 的长度必须介于 4 到 20 位之间。

      如果未配置此设置，则用户可配置 4 到 20 位之间任意长度的启动 PIN

      此设置仅适用于首次启用 BitLocker 的情况；如果已启用 BitLocker，则不起作用。

  - **配置操作系统驱动器的加密方法**  
   CSP：[EncryptionMethodByDriveType]( https://go.microsoft.com/fwlink/?linkid=872526)

    配置 OS 驱动器的加密方法和密码长度。 XTS-AES 128 位是 Windows 默认加密方法和建议的值。

    - **未配置**（默认）
    - AES 128 位 CBC
    - AES 256 位 CBC
    - AES 128 位 XTS
    - AES 256 位 XTS

### <a name="bitlocker---removable-drive-settings"></a>BitLocker - 可移动驱动器设置

- **配置操作系统驱动器的加密方法**  
  CSP：[BitLocker 组策略设置](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **未配置**（默认）  
  - **将“报表”**

  设置为“配置”时，可配置以下设置。

  - **配置可移动数据驱动器的加密方法**  
    CSP：[EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)

    为可移动数据驱动器磁盘选择所需的加密方法。

    - **未配置**（默认）
    - AES 128 位 CBC
    - AES 256 位 CBC
    - AES 128 位 XTS
    - AES 256 位 XTS

  - **阻止对不受 BitLocker 保护的可移动数据驱动器的写权限**  
    CSP：[RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

    - **未配置**（默认）- 可将数据写入非加密的可移动驱动器。
    - **是** - Windows 禁止向不受 BitLocker 保护的可移动驱动器写入数据。 如果未对插入的可移动驱动器进行加密，则在授予对驱动器的写入权限之前，用户必须完成 BitLocker 安装向导。

    - **阻止对不受 BitLocker 保护的可移动数据驱动器的写权限**  
      CSP：[RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)

      - **未配置**（默认） - 可使用 BitLocker 加密的任何驱动器。
      - **是** - 阻止访问可移动驱动器，除非已在组织拥有的计算机上对其进行加密。

## <a name="next-steps"></a>后续步骤

[磁盘加密的终结点安全策略](../protect/endpoint-security-disk-encryption-policy.md)
