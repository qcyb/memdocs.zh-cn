---
title: BitLocker 管理和监视网站
titleSuffix: Configuration Manager
description: 如何使用 Configuration Manager 中的 BitLocker 管理和监视网站（技术支持门户）
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 81f03922-90f6-4e8f-be65-da64ccb21cf2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf9301e4fcb279b7d79a6f6c3d0a90ab3d15e277
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697307"
---
# <a name="bitlocker-administration-and-monitoring-website"></a>BitLocker 管理和监视网站

适用范围：  Configuration Manager (Current Branch)

<!--3601034-->

BitLocker 管理和监视网站是 BitLocker 驱动器加密的管理界面。 它亦称为“技术支持门户”。 使用此网站，可以审阅报告、恢复用户驱动器，并管理设备 TPM。

[![默认 BitLocker 管理和监视网站 屏幕截图](media/bitlocker-helpdesk-website.png)](media/bitlocker-helpdesk-website.png#lightbox)

请先在 Web 服务器上安装此组件，然后才能使用它。 有关详细信息，请参阅[设置 BitLocker 报告和门户](setup-websites.md)。

通过以下 URL 访问管理和监视网站：`https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> 可从 Administration and Monitoring 网站查看“恢复审核报告”  。 将其他 BitLocker 管理报告添加到 Reporting Services 点。 有关详细信息，请参阅[查看 BitLocker 报告](view-reports.md)。

## <a name="groups"></a>组

用户帐户必须属于以下组之一，才能访问管理和监视网站的特定区域。 使用所需的任意名称在 Active Directory 中创建这些组。 在安装此网站时，指定这些组名称。 有关详细信息，请参阅[设置 BitLocker 报告和门户](setup-websites.md)。

|组|说明|
|--- |--- |
|BitLocker 技术支持管理员|提供对 administration and monitoring 网站所有区域的访问权限。 帮助用户恢复其驱动器时，你只输入恢复密钥，而无需输入域和用户名。 如果用户同时是此组和 BitLocker 技术支持用户组的成员，管理员组权限会替代用户组权限。|
|BitLocker 技术支持用户|提供对 administration and monitoring 网站“管理 TPM”和“驱动器恢复”区域的访问权限   。 使用任何一个区域时，都需要填写所有字段，包括用户的域名和帐户名。 如果用户同时是此组和 BitLocker 技术支持管理员组的成员，管理员组权限会替代用户组权限。|
|BitLocker 报告用户|提供对 Administration and Monitoring 网站中的“报告”的访问权限  。|

## <a name="manage-tpm"></a>管理 TPM

如果用户输入不正确 PIN 的次数太多，可能会锁定 TPM。 用户在 TPM 锁定之前可以输入的不正确 PIN 的次数因制造商而异。 从管理和监视网站的“管理 TPM”  区域中，访问集中式密钥恢复数据系统。

若要详细了解 TPM 所有权，请参阅[配置 MBAM 以托管 TPM 并存储 OwnerAuth 密码](/microsoft-desktop-optimization-pack/mbam-v25/mbam-25-security-considerations#bkmk-tpm)。

> [!NOTE]
> 自 Windows 10 版本 1607 起，Windows 不会在预配 TPM 时保留 TPM 所有者密码。

1. 在 Web 浏览器中，转到管理和监视网站（例如，`https://webserver.contoso.com/HelpDesk`）。

1. 在左侧窗格中，选择“管理 TPM”  区域。

    ![BitLocker 管理和监视网站的“管理 TPM”页](media/bitlocker-admin-manage-tpm.png)

1. 输入计算机的完全限定域名和计算机名。

1. 根据需要，输入用户的域名和用户名，以检索 TPM 所有者密码文件。

1. 选择“请求获取 TPM 所有者密码文件的原因”  的下列选项之一：

    - 重置 PIN 锁定
    - 打开 TPM
    - 关闭 TPM
    - 更改 TPM 密码
    - 清除 TPM
    - 其他

    在你提交  表单后，网站返回以下响应之一：

    - 如果找不到匹配的 TPM 所有者密码文件，它返回错误消息。

    - 提交的计算机的 TPM 所有者密码文件

    检索到 TPM 所有者密码文件后，网站显示所有者密码。

1. 若要将密码保存到文件中，请选择“保存”  。

1. 在“管理 TPM”  区域中，选择“重置 TPM 锁定”  选项，并提供 TPM 所有者密码文件。

    此时，TPM 锁定会重置。 BitLocker 恢复用户对设备的访问权限。

    > [!IMPORTANT]
    > 请勿共享 TPM 哈希值或 TPM 所有者密码文件。

## <a name="drive-recovery"></a>驱动器恢复

### <a name="recover-a-drive-in-recovery-mode"></a><a name="bkmk_recovery"></a>在恢复模式下恢复驱动器

驱动器在以下情况下进入恢复模式：

- 用户丢失或忘记自己的 PIN 或密码
- 受信任的平台模块 (TPM) 检测到计算机的 BIOS 或启动文件发生了更改

若要获取恢复密码，请使用 Administration and Monitoring 网站的“驱动器恢复”区域  。

> [!IMPORTANT]
> 恢复密码会在使用一次之后过期。 在 OS 驱动器和固定数据驱动器上，一次性使用规则是自动应用的。 在可移动驱动器上，此规则在你拆除并重新插入驱动器时应用。

1. 在 Web 浏览器中，转到管理和监视网站（例如，`https://webserver.contoso.com/HelpDesk`）。

1. 在左侧窗格中，选择“驱动器恢复”  区域。

    ![BitLocker 管理和监视网站的“驱动器恢复”页](media/bitlocker-admin-drive-recovery.png)

1. 根据需要，输入用户的域名和用户名，以查看恢复信息。

1. 若要查看包含可能匹配的恢复密钥的列表，请输入恢复密钥 ID 的前八位数字。 若要获取确切的恢复密钥，请输入整个恢复密钥 ID。

1. 选择“解除锁定驱动器的原因”  的下列选项之一：

    - 已更改操作系统启动顺序
    - 已更改 BIOS
    - 操作系统文件被修改
    - 丢失启动密钥
    - 丢失 PIN
    - TPM 重置
    - 丢失密码
    - 丢失智能卡
    - 其他

    在你提交  表单后，网站返回以下响应之一：

    - 如果用户具有多个匹配的恢复密码，则返回多个可能的匹配项。

    - 已提交的用户的恢复密码和恢复包。

        > [!NOTE]
        > 如果你正在恢复已损坏的驱动器，则恢复包选项会为 BitLocker 提供恢复驱动器所需的重要信息。

    - 如果找不到匹配的恢复密码，它返回错误消息。

    在检索到恢复密码和恢复包后，网站显示恢复密码。

1. 若要复制密码，请选择“复制密钥”  。 要将恢复密码保存到文件中，请选择“保存”  。

若要解除锁定驱动器，请输入恢复密码或使用恢复包。

### <a name="recover-a-moved-drive"></a><a name="bkmk_moved"></a>恢复已移动的驱动器

如果你将驱动器移到新计算机中，由于 TPM 不同，因此 BitLocker 不接受旧 PIN。 若要恢复移动的驱动器，请获取恢复密钥 ID 以检索恢复密码。

若要恢复移动的驱动器，请使用 Administration and Monitoring 网站的“驱动器恢复”区域  。

1. 在包含移动的驱动器的计算机上，在 Windows 恢复环境 (WinRE) 模式下启动计算机。

1. 在 WinRE 中，BitLocker 将移动的 OS 驱动器视为固定数据驱动器。 BitLocker 显示驱动器的恢复密码 ID，并提示输入恢复密码。

    > [!NOTE]
    > 在某些情况下，在启动过程中选择“忘记了 PIN”  选项（若有）。 然后，进入恢复模式，以显示恢复密钥 ID。

1. 使用恢复密钥 ID 从管理和监视网站中获取恢复密码。 有关详细信息，请参阅[在恢复模式下恢复驱动器](#bkmk_recovery)。

如果移动的驱动器配置为使用原始计算机上的 TPM 芯片，请完成以下步骤。 否则，恢复过程已完成。

1. 解除锁定驱动器后，在 WinRE 模式下启动计算机。 在 WinRE 中打开命令提示符，并运行 `manage-bde` 命令来解密驱动器。 此工具是唯一一种不采用原始 TPM 芯片而删除 TPM + PIN 保护的方法  。 有关此命令的详细信息，[请参阅 ](/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-managebde)Manage-bde。

1. 完成后，正常启动计算机。 Configuration Manager 会强制执行 BitLocker 策略，以使用新计算机的 TPM 及 PIN 对驱动器进行加密。

### <a name="recover-a-corrupted-drive"></a><a name="bkmk_corrupted"></a>恢复已损坏驱动器

使用恢复密钥 ID 从管理和监视网站中获取恢复密钥包。 有关详细信息，请参阅[在恢复模式下恢复驱动器](#bkmk_recovery)。

1. 将“恢复密钥包”  保存到你的计算机上，然后将它复制到包含损坏驱动器的计算机上。

1. 以管理员身份打开命令提示符并键入以下命令：

    `repair-bde <corrupted drive> <fixed drive> -kp <key package> -rp <recovery password>`

    替换以下值：

    - `<corrupted drive>`：损坏驱动器的驱动器号（例如，`D:`）
    - `<fixed drive>`：与损坏驱动器大小相似或更大的可用硬盘驱动器的驱动器号。 BitLocker 恢复损坏驱动器上的数据，并将数据移到指定驱动器中。 此驱动器上的所有数据都被覆盖。
    - `<key package>`：恢复密钥包的位置
    - `<recovery password>`：关联的恢复密码

    例如：

    `repair-bde C: D: -kp F:\RecoveryKeyPackage -rp 111111-222222-333333-444444-555555-666666-777777-888888`

有关此命令的详细信息，请参阅 [Repair-bde](/windows/security/information-protection/bitlocker/bitlocker-use-bitlocker-drive-encryption-tools-to-manage-bitlocker#bkmk-repairbde)。

## <a name="reports"></a>报表

管理和监视网站包含“恢复审核报告”  。 其他报告可以从 Configuration Manager Reporting Services 点获取。 有关详细信息，请参阅[查看 BitLocker 报告](view-reports.md)。

1. 在 Web 浏览器中，转到管理和监视网站（例如，`https://webserver.contoso.com/HelpDesk`）。

1. 在左侧窗格中，选择“报告”  区域。

1. 在顶部的菜单栏中，选择“恢复审核报告”  。

若要详细了解此报告，请参阅[恢复审核报告](view-reports.md#bkmk-audit)

> [!TIP]
> 若要保存报告结果，请选择“报告”  菜单栏上的“导出”  。