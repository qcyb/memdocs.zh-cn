---
title: BitLocker 设置参考
titleSuffix: Configuration Manager
description: Configuration Manager 中可用的所有 BitLocker 管理设置
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f7ade768-2b2b-4aab-8ee1-73624d03a9c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9ce6a9c566fec22e69c0a4a7fde01b911330ec1d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708615"
---
# <a name="bitlocker-settings-reference"></a>BitLocker 设置参考

适用范围：  Configuration Manager (Current Branch)

<!-- 5925683 -->

Configuration Manager 中的 BitLocker 管理策略包含以下策略组：

- Setup
- 操作系统驱动器
- 固定驱动器
- 可移动驱动器
- 客户端管理

以下部分介绍和建议每个组中的设置的配置。

> [!NOTE]
> 这些设置基于 Configuration Manager 版本 2002。 版本 1910 并不包含所有这些设置。

## <a name="setup"></a>Setup

此页上的设置配置全局 BitLocker 加密选项。

### <a name="drive-encryption-method-and-cipher-strength"></a>驱动器加密方法和密码长度

建议的配置  ：对于默认或更高加密方法，为“已启用”  。

> [!NOTE]
> “设置”  属性页对于不同版本的 Windows 包含两组设置。 此部分会介绍这两组设置。

#### <a name="windows-81-devices"></a>Windows 8.1 设备

对于 Windows 8.1 设备，启用“驱动器加密方法和密码长度”  选项，然后选择以下加密方法之一：

- 含有扩散器的 AES 128 位
- 含有扩散器的 AES 256 位
- AES 128 位（默认）
- AES 256 位

#### <a name="windows-10-devices"></a>Windows 10 设备

对于 Windows 10 设备，请启用“驱动器加密方法和密码强度(Windows 10)”选项  。 然后分别为 OS 驱动器、固定数据驱动器和可移动数据驱动器选择以下加密方法：

- AES-CBC 128 位
- AES-CBC 256 位
- XTS-AES 128 位(默认)
- XTS-AES 256 位

> [!TIP]
> BitLocker 使用高级加密标准 (AES) 作为其加密算法，可配置的密钥长度为 128 或 256 位。 在 Windows 10 设备上，AES 加密支持加密块链接 (CBC) 或密码文本窃用 (XTS)。
>
> 如果需要在不运行 Windows 10 的设备上使用可移动驱动器，请使用 AES-CBC。

#### <a name="general-usage-notes-for-drive-encryption-and-cipher-strength"></a>驱动器加密和密码长度的一般使用说明

- 如果禁用或未配置这些设置，BitLocker 将采用默认加密方法。

- 打开 BitLocker 时，Configuration Manager 会应用这些设置。

- 如果驱动器已加密或正在处理中，则对这些策略设置的任何更改都不会更改设备上的驱动器加密状况。

- 如果使用默认值，则 BitLocker 计算机合规性报告可能会将密码长度显示为“未知”  。 若要解决此问题，请启用此设置并为密码长度设置显式值。

### <a name="prevent-memory-overwrite-on-restart"></a>禁止在重新启动时覆盖内存

建议的配置  ：未配置 

将此策略配置为提高重新启动性能，而不在重新启动时覆盖内存中的 BitLocker 机密。

未配置此策略时，BitLocker 会在计算机重新启动时从内存中删除其机密。

### <a name="validate-smart-card-certificate-usage-rule-compliance"></a>验证智能卡证书使用规则符合性

建议的配置  ：未配置 

将此策略配置为使用基于智能卡证书的 BitLocker 保护。 然后指定证书对象标识符  。

未配置此策略时，BitLocker 会使用默认对象标识符 `1.3.6.1.4.1.311.67.1.1` 指定证书。

### <a name="organization-unique-identifiers"></a>组织唯一标识符

建议的配置  ：未配置 

将此策略配置为使用基于证书的数据恢复代理或 BitLocker To Go 读取器。

未配置此策略时，BitLocker 不会使用“标识”  字段。

如果组织需要更高安全性度量，请配置“标识”  字段。 在所有目标 USB 设备上设置此字段，并使它与此设置保持一致。

## <a name="os-drive"></a>OS 驱动器

此页上的设置为安装 Windows 的驱动器配置加密设置。

### <a name="operating-system-drive-encryption-settings"></a>操作系统驱动器加密设置

建议的配置  ：**Enabled**

如果启用此设置，用户必须保护 OS 驱动器，并且 BitLocker 会加密驱动器。 如果禁用该设置，用户无法保护驱动器。 如果未配置此策略，则 OS 驱动器上不需要 BitLocker 保护。

> [!NOTE]
> 如果驱动器已加密，并且禁用此设置，BitLocker 将解密驱动器。  

如果设备没有[受信任的平台模块 (TPM)](https://docs.microsoft.com/windows/security/information-protection/tpm/trusted-platform-module-top-node)，请使用选项“没有兼容的 TPM 时允许 BitLocker (需要密码)”  。 即使设备没有 TPM，此设置也允许 BitLocker 加密 OS 驱动器。 如果允许使用此选项，则 Windows 会提示用户指定 BitLocker 密码。

在具有兼容的 TPM 的设备上，可以在启动时使用两种类型的身份验证方法，以便为加密的数据提供额外的保护。 在计算机启动时，它只能使用 TPM 进行身份验证，或者它还可能要求输入个人标识号 (PIN)。 配置下列设置：

- **选择操作系统驱动器的保护程序**：将其配置为使用 TPM 和 PIN 或只使用 TPM。

- **配置启动时的最小 PIN 长度**：如果要求使用 PIN，则此值是用户可以指定的最短长度。 在计算机启动以解锁驱动器时，用户输入此 PIN。 默认情况下，最小 PIN 长度为 `4`。

> [!TIP]
> 为了提高安全性，在使用 TPM + PIN 保护程序启用设备时，考虑在“系统”   > “电源管理”   > “睡眠设置”  中禁用  以下组策略设置：
>
> - 睡眠时允许待机状态(S1-S3)(接通电源)
>
> - 睡眠时允许待机状态(S1-S3)(使用电池)

### <a name="allow-enhanced-pins-for-startup"></a>允许增强型启动 PIN

建议的配置  ：未配置 

将 BitLocker 配置为使用增强型启动 PIN。 这些 PIN 允许使用附加字符，如大写和小写字母、符号、数字和空格。 打开 BitLocker 时会应用此设置。

> [!IMPORTANT]
> 并非所有计算机都可以在预启动环境中支持增强型 PIN。 启用其使用之前，请评估设备是否与此功能兼容。

如果启用此设置，则所有新 BitLocker 启动 PIN 都会允许用户创建增强型 PIN。

- 需要纯 ASCII PIN  ：帮助使增强型 PIN 更加与限制可以在预启动环境中输入的字符类型或数量的计算机兼容。

如果禁用或未配置此策略设置，则 BitLocker 不使用增强型 PIN。

### <a name="operating-system-drive-password-policy"></a>操作系统驱动器密码策略

建议的配置  ：未配置 

使用这些设置设置密码约束，以解锁受 BitLocker 保护的 OS 驱动器。 如果在 OS 驱动器上允许非 TPM 保护程序，请配置以下设置：

- 为操作系统驱动器配置密码复杂性  ：若要对密码强制执行复杂性要求，请选择“需要密码复杂性”  。

- 操作系统驱动器的最短密码长度  ：默认情况下，最小长度为 `8`。

- 可移动操作系统驱动器需要纯 ASCII 密码 

如果启用此策略设置，则用户可以配置与你定义的要求相符的密码。

#### <a name="general-usage-notes-for-os-drive-password-policy"></a>OS 驱动器密码策略的一般使用说明

- 若要使这些复杂性要求设置生效，还需要启用“计算机配置”   > “Windows 设置”   > “安全设置”   > “帐户策略”   > “密码策略”  中的组策略设置“密码必须符合复杂性要求”  。

- BitLocker 会在打开它时强制执行这些设置，而在解锁卷时不强制执行。 BitLocker 使你能够使用驱动器上可用的任何保护程序来解锁驱动器。

- 如果使用组策略启用符合 FIPS 标准的算法来进行加密、哈希和签名，则不能允许将密码作为 BitLocker 保护程序。

### <a name="reset-platform-validation-data-after-bitlocker-recovery"></a>BitLocker 恢复之后重置平台验证数据

建议的配置  ：未配置 

控制 Windows 在 BitLocker 恢复之后启动时是否刷新平台验证数据。

如果启用或未配置此设置，则在这种情况下，Windows 会刷新平台验证数据。

如果禁用此策略设置，则在这种情况下，Windows 不刷新平台验证数据。

### <a name="pre-boot-recovery-message-and-url"></a>预启动恢复消息和 URL

建议的配置  ：未配置 

当 BitLocker 锁定 OS 驱动器时，使用此设置可在预启动 BitLocker 恢复屏幕上显示自定义恢复消息或 URL。 此设置仅适用于 Windows 10 设备。

启用此设置时，为预启动恢复消息选择以下选项之一：

- 使用默认恢复消息和 URL  ：在预启动 BitLocker 恢复屏幕中显示默认 BitLocker 恢复消息和 URL。 如果以前配置了自定义恢复消息或 URL，请使用此选项恢复为默认消息。

- 使用自定义恢复消息  ：在预启动 BitLocker 恢复屏幕中包含自定义消息。

  - 自定义恢复消息选项  ：键入要显示的自定义消息。 如果还要指定恢复 URL，请将它包含在此自定义恢复消息中。 最大字符串长度为 32,768 个字符。

- 使用自定义恢复 URL  ：替换显示在预启动 BitLocker 恢复屏幕中的默认 URL。

  - 自定义恢复 URL 选项  ：键入要显示的 URL。 最大字符串长度为 32,768 个字符。

> [!NOTE]
> 并非所有字符和语言都在预启动中受支持。 首先测试自定义消息或 URL，以确保它可正确显示在预启动 BitLocker 恢复屏幕上。

### <a name="encryption-policy-enforcement-settings-os-drive"></a>加密策略强制执行设置（OS 驱动器）

建议的配置  ：**Enabled**

配置用户可以为 OS 驱动器延期 BitLocker 合规性的天数。 不合规宽限期在 Configuration Manager 首次检测到它不合规时开始  。 此宽限期过期之后，用户无法延期所需操作或请求免除。

如果加密过程需要用户输入，则会在 Windows 中出现一个对话框，用户在提供所需信息之前无法关闭它。 将来的错误或状态通知不会具有此限制。

如果 BitLocker 不需要用户交互即可添加保护程序，则在宽限期过期之后，BitLocker 会在后台启动加密。

如果禁用或未配置此设置，则 Configuration Manager 不要求用户遵守 BitLocker 策略。

若要立即强制执行策略，请将宽限期设置为 `0`。

## <a name="fixed-drive"></a>固定驱动器

此页上的设置为设备中的其他数据驱动器配置加密。

### <a name="fixed-data-drive-encryption"></a>固定数据驱动器加密

建议的配置  ：**Enabled**

管理对固定数据驱动器加密的要求。 如果启用此设置，BitLocker 会要求用户将所有固定数据驱动器置于被保护状态。 然后对数据驱动器进行加密。

启用此策略时，请启用自动解锁或“固定数据驱动器密码策略”设置  。

- **为固定数据驱动器配置自动解锁**：允许或要求 BitLocker 自动解锁任何加密的数据驱动器。 若要使用自动解锁，还需要使用 BitLocker 加密 [OS 驱动器](#os-drive)。

如果未配置此设置，则 BitLocker 不要求用户将固定数据驱动器置于被保护状态。

如果禁用此设置，则用户无法用 BitLocker 保护固定数据驱动器。 如果在 BitLocker 加密固定数据驱动器之后禁用此策略，则 BitLocker 会对固定数据驱动器进行解密。

### <a name="deny-write-access-to-fixed-drives-not-protected-by-bitlocker"></a>拒绝对不受 BitLocker 保护的固定驱动器的写访问

建议的配置  ：未配置 

要求进行 BitLocker 保护以便 Windows 将数据写入设备上的固定驱动器。 BitLocker 会在你启用它时应用此策略。

启用此设置时：

- 如果 BitLocker 保护固定数据驱动器，则 Windows 会使用读写访问权限装载它。

- 对于 BitLocker 不保护的任何固定数据驱动器，Windows 会将它装载为只读状态。

未配置此设置时，Windows 会使用读写访问权限装载所有固定数据驱动器。

<!-- ### Allow access to BitLocker-protected fixed drives from earlier versions of Windows -->

### <a name="fixed-data-drive-password-policy"></a>固定数据驱动器密码策略

建议的配置  ：未配置 

使用这些设置设置密码约束，以解锁受 BitLocker 保护的固定数据驱动器。

如果启用此设置，则用户可以配置与你定义的要求相符的密码。

为提高安全性，请启用此设置，然后配置以下设置：

- 需要对固定数据驱动器使用密码  ：用户必须指定密码才能解锁受 BitLocker 保护的固定数据驱动器。

- 为固定数据驱动器配置密码复杂性  ：若要对密码强制执行复杂性要求，请选择“需要密码复杂性”  。

- 固定数据驱动器的最小密码长度  ：默认情况下，最小长度为 `8`。

如果禁用此设置，则用户无法配置密码。

未配置此策略时，BitLocker 会支持具有默认设置的密码。 默认设置不包括密码复杂性要求，只需要八个字符。

#### <a name="general-usage-notes-for-fixed-data-drive-password-policy"></a>固定数据驱动器密码策略的一般使用说明

- 若要使这些复杂性要求设置生效，还需要启用“计算机配置”   > “Windows 设置”   > “安全设置”   > “帐户策略”   > “密码策略”  中的组策略设置“密码必须符合复杂性要求”  。

- BitLocker 会在打开它时强制执行这些设置，而在解锁卷时不强制执行。 BitLocker 使你能够使用驱动器上可用的任何保护程序来解锁驱动器。

- 如果使用组策略启用符合 FIPS 标准的算法来进行加密、哈希和签名，则不能允许将密码作为 BitLocker 保护程序。

### <a name="encryption-policy-enforcement-settings-fixed-data-drive"></a>加密策略强制执行设置（固定数据驱动器）

建议的配置  ：**Enabled**

配置用户可以为固定数据驱动器延期 BitLocker 合规性的天数。 不合规宽限期在 Configuration Manager 首次检测到固定数据驱动器不合规时开始  。 它不强制执行固定数据驱动器策略，直到 OS 驱动器符合要求。 宽限期过期之后，用户无法延期所需操作或请求免除。

如果加密过程需要用户输入，则会在 Windows 中出现一个对话框，用户在提供所需信息之前无法关闭它。 将来的错误或状态通知不会具有此限制。

如果 BitLocker 不需要用户交互即可添加保护程序，则在宽限期过期之后，BitLocker 会在后台启动加密。

如果禁用或未配置此设置，则 Configuration Manager 不要求用户遵守 BitLocker 策略。

若要立即强制执行策略，请将宽限期设置为 `0`。

## <a name="removable-drive"></a>可移动驱动器

此页上的设置为可移动驱动器（如 U 盘）配置加密。

### <a name="removable-data-drive-encryption"></a>可移动数据驱动器加密

建议的配置  ：**Enabled**

此设置控制 BitLocker 在可移动驱动器上的使用。

- 允许用户对可移动数据驱动器应用 BitLocker 保护  ：用户可以为可移动驱动器启用 BitLocker 保护。

- 允许用户对可移动数据驱动器暂停和解密 BitLocker  ：用户可以从可移动驱动器中删除或临时暂停 BitLocker 驱动器加密。

如果启用此设置并允许用户应用 BitLocker 保护，Configuration Manager 客户端会将有关可移动驱动器的恢复信息保存到管理点上的恢复服务。 此行为允许用户在忘记或丢失保护手段（密码）的情况下恢复驱动器。

启用此设置时：

- 启用“可移动数据驱动器密码策略”  设置

- 对于用户和计算机配置，禁用  “系统”   > “可移动存储访问”  中的以下组策略设置：

  - 所有可移动存储类:  拒绝所有权限
  - 可移动磁盘:  拒绝写入权限
  - 可移动磁盘:  拒绝读取权限

如果禁用此设置，则用户无法在可移动驱动器上使用 BitLocker。

### <a name="deny-write-access-to-removable-drives-not-protected-by-bitlocker"></a>拒绝对不受 BitLocker 保护的可移动驱动器的写访问

建议的配置  ：未配置 

要求进行 BitLocker 保护以便 Windows 将数据写入设备上的可移动驱动器。 BitLocker 会在你启用它时应用此策略。

启用此设置时：

- 如果 BitLocker 保护可移动驱动器，则 Windows 会使用读写访问权限装载它。

- 对于 BitLocker 不保护的任何可移动驱动器，Windows 会将它装载为只读状态。

- 如果启用“拒绝对其他组织中配置的驱动器的写访问”  ，则 BitLocker 仅向标识字段与允许的标识字段匹配的可移动驱动器授予写入访问权限。 在[“设置”](#setup)页上，使用“组织唯一标识符”  全局设置定义这些字段。

禁用或未配置此设置时，Windows 会使用读写访问权限装载所有可移动驱动器。

> [!NOTE]
> 可以使用“系统”   > “可移动存储访问”  中的组策略设置覆盖此设置。 如果启用组策略设置“可移动磁盘:  拒绝写入权限”，则 BitLocker 会忽略此 Configuration Manager 设置。

<!-- ### Allow access to BitLocker-protected removable data drives from earlier versions of Windows -->

### <a name="removable-data-drive-password-policy"></a>可移动数据驱动器密码策略

建议的配置  ：**Enabled**

使用这些设置设置密码约束，以解锁受 BitLocker 保护的可移动驱动器。

如果启用此设置，则用户可以配置与你定义的要求相符的密码。

为提高安全性，请启用此设置，然后配置以下设置：

- 需要对可移动数据驱动器使用密码  ：用户必须指定密码才能解锁受 BitLocker 保护的可移动驱动器。

- 为可移动数据驱动器配置密码复杂性  ：若要对密码强制执行复杂性要求，请选择“需要密码复杂性”  。

- 可移动数据驱动器的最小密码长度  ：默认情况下，最小长度为 `8`。

如果禁用此设置，则用户无法配置密码。

未配置此策略时，BitLocker 会支持具有默认设置的密码。 默认设置不包括密码复杂性要求，只需要八个字符。

#### <a name="general-usage-notes-for-removable-data-drive-password-policy"></a>可移动数据驱动器密码策略的一般使用说明

- 若要使这些复杂性要求设置生效，还需要启用“计算机配置”   > “Windows 设置”   > “安全设置”   > “帐户策略”   > “密码策略”  中的组策略设置“密码必须符合复杂性要求”  。

- BitLocker 会在打开它时强制执行这些设置，而在解锁卷时不强制执行。 BitLocker 使你能够使用驱动器上可用的任何保护程序来解锁驱动器。

- 如果使用组策略启用符合 FIPS 标准的算法来进行加密、哈希和签名，则不能允许将密码作为 BitLocker 保护程序。

## <a name="client-management"></a>客户端管理

此页上的设置配置 BitLocker 管理服务和客户端。

### <a name="bitlocker-management-services"></a>BitLocker 管理服务

建议的配置  ：**Enabled**

启用此设置时，Configuration Manager 会自动且无提示地备份站点数据库中的密钥恢复信息。 如果禁用或未配置此设置，则 Configuration Manager 不会保存密钥恢复信息。

- **选择要存储的 BitLocker 恢复信息**：将密钥恢复服务配置为备份 BitLocker 恢复信息。 它提供了一种恢复 BitLocker 加密的数据的管理方法，可帮助防止因缺少密钥信息而发生数据丢失。

- 允许以纯文本格式存储恢复信息  ：如果没有 SQL Server 的 BitLocker 管理加密证书，Configuration Manager 会以纯文本形式存储密钥恢复信息。 有关详细信息，请参阅[加密恢复数据](../../deploy-use/bitlocker/encrypt-recovery-data.md)。

- 客户端检查状态频率（以分钟为单位）  ：客户端会按配置的频率检查计算机上的 BitLocker 保护策略和状态，还会备份客户端恢复密钥。 默认情况下，Configuration Manager 客户端每 90 分钟更新一次其 BitLocker 恢复信息。

### <a name="user-exemption-policy"></a>使用例外策略

建议的配置  ：未配置 

配置联系方法，以便用户请求免除 BitLocker 加密。

如果启用此策略设置，请提供以下信息：

- 最长延迟天数  ：用户可以延迟强制执行策略的天数。 默认情况下，此值为 `7` 天（一周）。

- 联系方法  ：指定用户如何请求免除：URL、电子邮件地址或电话号码。

- 联系人  ：输入 URL、电子邮件地址或电话号码。 当用户请求免除 BitLocker 保护时，他们将看到一个 Windows 对话框，其中包含有关如何申请的说明。 Configuration Manager 不会验证输入的信息。

  - **URL**：使用标准 URL 格式 `https://website.domain.tld`。 Windows 将 URL 显示为超链接。

  - **电子邮件地址**:使用标准电子邮件地址格式 `user@domain.tld`。 Windows 将地址显示为以下超链接：`mailto:user@domain.tld?subject=Request exemption from BitLocker protection`。

  - 电话号码  ：指定希望用户拨打的号码。 Windows 会显示号码以及以下说明：`Please call <your number> for applying exemption`。

如果禁用或未配置此设置，则 Windows 不会向用户显示免除请求说明。

> [!NOTE]
> BitLocker 按用户（而不是按计算机）管理免除。 如果多个用户登录到相同计算机并且任何一个用户都未免除，则 BitLocker 会对该计算机进行加密。

### <a name="url-for-the-security-policy-link"></a>安全策略链接的 URL

建议的配置  ：**Enabled**

指定要在 Windows 中向用户显示为“公司安全策略”  的 URL。 使用此链接可向用户提供有关加密要求的信息。 它会在 BitLocker 提示用户加密驱动器时显示。

如果启用此设置，请配置安全策略链接 URL  。

如果禁用或未配置此设置，则 BitLocker 不显示安全策略链接。
