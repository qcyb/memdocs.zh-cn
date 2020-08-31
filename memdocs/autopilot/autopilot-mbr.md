---
title: Windows Autopilot 主板更换
ms.reviewer: ''
manager: laurawi
description: Windows Autopilot 部署主板替换 (MBR) 方案
keywords: mdm, 设置, windows, windows 10, oobe, 管理, 部署, autopilot, ztd, 零接触, 合作伙伴, msfb, intune
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
ms.openlocfilehash: 69257cb42357ad3110dd94b79cefe5a9f98a90ba
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057298"
---
# <a name="windows-autopilot-motherboard-replacement-scenario-guidance"></a>Windows Autopilot 主板更换方案指南

**适用于**

- Windows 10

本文档提供 Windows Autopilot 设备修复方案的指南，Microsoft 合作伙伴可以 (在) 的情况下使用该方案，以及其他维护方案。

修复 Autopilot 注册的设备是一种复杂的方法，因为它会尝试根据 Windows Autopilot 要求来平衡 OEM 需求。 具体而言，OEM 要求包括各种主板、MAC 地址等严格的唯一性。 Windows Autopilot 要求每个设备的硬件哈希级别严格唯一，才能成功注册。 硬件哈希并不一定能满足所有 OEM 硬件组件要求。 因此，这些要求有时会导致某些修复方案出现问题。 硬件哈希也称为硬件 ID。

**主板更换 (MBR) **

如果 Windows Autopilot 设备上需要更换主板，建议执行以下操作：

1. 从 Windows Autopilot 取消[注册设备](#deregister-the-autopilot-device-from-the-autopilot-program)
2. [更换主板](#replace-the-motherboard)
3. [捕获新设备 ID (4K HH) ](#capture-a-new-autopilot-device-id-4k-hh-from-the-device)
4. 通过 Windows Autopilot 重新[注册设备](#reregister-the-repaired-device-using-the-new-device-id)
5. [重置设备](#reset-the-device)
6. [返回设备](#return-the-repaired-device-to-the-customer)

以下描述了上述每一个步骤。

## <a name="deregister-the-autopilot-device-from-the-autopilot-program"></a>从 Autopilot 程序取消注册 Autopilot 设备

在设备到达 repair 设施之前，必须由注册它的实体对其取消注册。
- 如果 **IT 管理员** 注册了设备，则他们可能通过 Intune (或可能是业务) Microsoft Store。 如果是这样，则他们应该从 Intune (或 MSfB) 中取消注册设备，因为在 Intune 中注册的设备不会显示在 Microsoft 合作伙伴中心 (MPC) 。
- 如果 **OEM 或 CSP 合作伙伴** 注册了设备，则可能是通过 MPC 进行的。 在这种情况下，它们应该从 MPC 中取消注册设备，这也会将其从客户 IT 管理员的 Intune 帐户中删除。

下面我们介绍了 IT 管理员将如何从 Intune 取消注册设备所需执行的步骤，以及 OEM 或 CSP 从 MPC 取消注册设备的步骤。

为避免出现问题，OEM 或 CSP 应尽可能注册 Autopilot 设备。 如果客户注册了设备，则 Oem 或 Csp 不能将其取消注册（例如，如果客户租赁设备，则会在自行注销设备之前）使用。

如果客户授予 OEM 权限以代表其使用自动同意过程注册设备，则 OEM 可以使用该 API 取消注册自己未注册的设备。 此取消注册只会从 Autopilot 程序中删除这些设备。 它不会从 Intune 取消注册它们，也不会将其从 Azure AD 中脱离。 客户只能通过 Intune 执行这些步骤。 

### <a name="deregister-from-intune"></a>从 Intune 取消注册

若要从 Intune 中取消注册 Autopilot 设备，IT 管理员应：

1. 登录到其 Intune 帐户
2. 导航到 > 所有组的 Intune > 组
3. 从组中删除设备
4. 导航到 Intune > 设备 > 所有设备
5. 选择要删除的设备旁边的复选框，然后单击顶部菜单中的 "删除" 按钮
6. 导航到 Intune > 设备 > Azure AD 设备
7. 选择要删除的设备旁边的复选框，并单击顶部菜单中的 "删除" 按钮
8. 导航到 Intune > 设备注册 > Windows 注册 > 设备
9. 选择要取消注册的设备旁边的复选框
10. 单击扩展菜单图标 ( "..." ) 在包含要取消注册的设备的行的最右端，以显示包含 "取消分配用户" 选项的附加菜单
11. 如果先前已将设备分配给用户，请单击 "取消分配用户"。 如果不是，则此选项将显示为灰色，并可被忽略。
12. 如果仍选择了未分配的设备，请单击顶部菜单中的 "删除" 按钮以删除此设备

这些步骤从 Autopilot 取消注册设备，同时从 Intune 取消注册设备，并从 Azure AD 中脱离设备。 可能会出现，只需要从 Autopilot 取消注册设备。 不过，Intune 中有一些屏障需要上述所有步骤来避免设备丢失或不可恢复的问题。 若要防止 Autopilot 数据库、Intune 或 Azure AD 中存在孤立的设备，最好完成所有步骤。 如果设备进入不可恢复状态，你可以联系相应的 [Microsoft 支持别名](autopilot-support.md) 以获得帮助。

注销过程需要大约15分钟。 可以通过单击 "同步" 按钮，然后单击 "刷新" 显示，直到设备不再存在。

可在 [此处](/intune/enrollment-autopilot#create-an-autopilot-device-group)找到有关从 Intune 注销设备的更多详细信息。

### <a name="deregister-from-mpc"></a>从 MPC 取消注册

若要从 Microsoft 合作伙伴中心 (MPC) 取消注册 Autopilot 设备，CSP 应：

1. 登录到 MPC
2. 导航到客户 > 设备
3. 选择要取消注册的设备，然后单击 "删除设备" 按钮

![删除设备的屏幕截图](images/devices.png)

从 MPC 中的 Autopilot 注销设备仅执行此项。 它不会执行以下操作之一：
- 从 MDM (Intune 取消注册设备) 
- 从 Azure AD 脱离设备

因此，在可能的情况下，OEM/CSP 理想情况下应与客户 IT 管理员一起使用，以便按照上一部分中的 Intune 步骤来完全删除设备。

或者，已集成 OEM 直接 Api 的 OEM 合作伙伴可以使用 AutopilotDeviceRegistration API 取消注册设备。 请确保 TenantID 和 TenantDomain 字段留空。 

由于修复工具不会有用户的登录凭据，因此在修复过程中，他们必须将设备重置为映像。 在将设备发送到设备之前，客户应执行三项操作：
1. 复制设备中的所有重要数据。
2. 让 repair 设备知道应该在修复后重新安装哪个版本的 Windows。
3. 如果适用，请让 repair 设备知道应该在修复后重新安装哪个版本的 Office。

## <a name="replace-the-motherboard"></a>更换主板

技术人员将主板 (或其他硬件) 更换为损坏的设备。 插入 (DPK) 的替换数字产品密钥。

设备之间的修复和密钥替换过程各不相同。 有时，修复设备将从已注入替换 DPKs 的 Oem 接收主板备用部件，但有时不会。 有时，修复工具会从 Oem 接收功能齐全的 BIOS 工具，但有时不能。 因此，在 MBR 发生变化后，BIOS 中的数据质量会有所变化。 若要确保修复后的设备仍可 Autopilot 支持，请检查以确保新 (修复后) BIOS 可以成功地收集和填充以下信息：

- DiskSerialNumber
- SmbiosSystemSerialNumber
- SmbiosSystemManufacturer
- SmbiosSystemProductName
- SmbiosUuid
- TPM EKPub
- MacAddress
- ProductKeyID
- OSType

为简单起见，因为进程在修复工具之间有所不同，所以我们排除了通常在 MBR 中使用的其他一些步骤，如：
- 验证设备是否仍正常工作
- 禁用 BitLocker *
- 修复引导配置数据 (BCD) 
- 修复和验证网络驱动程序操作

* 如果技术人员可以在修复后恢复 BitLocker，则可以将其挂起而不是禁用。

## <a name="capture-a-new-autopilot-device-id-4k-hh-from-the-device"></a>从设备捕获 (4K HH) 的新的 Autopilot 设备 ID

修复技术人员必须登录到已修复的设备，才能捕获新的设备 ID。 如果修复技术人员无法访问客户的登录凭据，则他们必须重置设备的映像才能获得访问权限：

1. 修复技术人员创建 [WinPE 可启动 USB 驱动器](/windows-hardware/manufacture/desktop/oem-deployment-of-windows-10-for-desktop-editions#create-a-bootable-windows-pe-winpe-partition)。
2. 修复技术人员将设备引导到 WinPE。
3. 修复技术人员将 [新的 Windows 映像应用到设备](/windows-hardware/manufacture/desktop/work-with-windows-images)。

    理想情况下，在设备上原来的相同 Windows 版本应重置映像到设备上。 维修设施与客户之间需要进行某种协调，以便在设备到达时捕获此信息。 例如，这种协调可能包括客户通过 USB 驾驶贴) 自定义映像 ( .ppk 文件。
 
4. 修复技术人员将设备引导到新的 Windows 映像。
5. 一旦进入桌面，修复技术人员就会使用 OA3 工具或 PowerShell 脚本) 设备上 (4K HH 捕获新的设备 ID，如下所述。

那些可以访问 OA3 工具的修复工具 (是 ADK) 的一部分，它可以使用该工具来捕获4K 硬件哈希 (4K HH) 。

相反，可以通过执行以下步骤，使用 [WindowsAutoPilotInfo PowerShell 脚本](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo) 捕获 4k HH：

1. 从 [PowerShell 库](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo) 或从命令行安装脚本 (命令行安装如下) 所示。
2. 当设备处于完整 OS 或审核模式时，导航到脚本目录并在设备上运行它。 请参阅以下示例。

   ```powershell
   md c:\HWID
   Set-Location c:\HWID
   Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted -Force
   Install-Script -Name Get-WindowsAutopilotInfo -Force
   Get-WindowsAutopilotInfo.ps1 -OutputFile AutopilotHWID.csv
   ```

  - 如果系统提示你安装 NuGet 程序包，请选择 **"是"**。<br>
  - 如果在安装脚本后收到 Get-WindowsAutopilotInfo.ps1 找不到的错误，请验证路径变量中是否存在 C:\Program Files\WindowsPowerShell\Scripts。<br>
  - 如果安装脚本 cmdlet 失败，请验证是否已将默认 PowerShell 存储库注册 (**register-psrepository**) 或使用 **register-psrepository-default-Verbose**注册默认存储库。

此脚本创建一个 .csv 文件，其中包含设备信息，包括完整的 4K HH。 保存此文件，以便以后可以访问它。 服务设施将使用此 4K HH 重新注册设备，如下所述。 请确保在保存文件时使用-OutputFile 参数，这样可确保文件格式正确。 请勿尝试手动通过管道将命令输出传递给文件。

> [!NOTE]
> 如果修复功能无法运行 OA3 工具或 PowerShell 脚本来捕获新的 4K HH，则 CSP (或 OEM) 伙伴必须为其执行此操作。 如果没有某些实体捕获新的 4K HH，就无法将此设备重新注册为 Autopilot 设备。


## <a name="reregister-the-repaired-device-using-the-new-device-id"></a>使用新的设备 ID 重新注册已修复的设备

如果 OEM 无法重新注册该设备，则有两个选项：
- 修复工具或 CSP 可以使用 MPC 重新注册设备。
- 客户 IT 管理员应通过 Intune (或 MSfB) 重新注册设备。

重新注册设备的两种方法如下所示。

### <a name="reregister-from-intune"></a>从 Intune 注册

若要从 Intune 注册 Autopilot 设备，IT 管理员需要：
1. 登录 Intune。
2. 导航到 "设备注册" > Windows 注册 > 设备 ">" 导入 "。
3. 单击 " **导入** " 按钮上载包含要重新注册的设备的设备 ID 的 csv 文件。 设备 ID 为 4K HH，此操作由本文档前面所述的 PowerShell 脚本或 OA3 工具捕获。

以下视频概述了如何 (通过 MSfB 重新) 注册设备。<br>

> [!VIDEO https://www.youtube.com/embed/IpLIZU_j7Z0]

### <a name="reregister-from-mpc"></a>从 MPC 注册

若要从 MPC 重新注册 Autopilot 设备，OEM 或 CSP 将：

1. 登录到 MPC。
2. 导航到 "客户 > 设备" 页，然后单击 " **添加设备** " 按钮上传 csv 文件。

!["添加设备" 按钮的屏幕截图](images/device2.png)<br>
!["添加设备" 页面的屏幕截图](images/device3.png)

当通过 MPC 重新注册修复的设备时，上传的 csv 文件必须包含该设备的 4K HH，而不只是 PKID 或元组 (SerialNumber + OEMName + ModelName) 。 如果只使用了 PKID 或元组，则 Autopilot 服务在 Autopilot 数据库中找不到匹配项。 找不到匹配项，因为以前没有为此 "新" 设备提交 4K HH 信息。 上传将会失败，并且可能会返回 ZtdDeviceNotFound 错误。 同样，仅上传 4K HH，而不是元组或 PKID。

在 csv 文件中包含 4K HH 时，还不需要包含 PKID 或元组。 这些列可能留空，如下所示：

![hash](images/hh.png)

## <a name="reset-the-device"></a>重置设备

在将映像返回给客户之前，修复设备必须将其重置回之前的 OOBE 状态。 此重置是必需的，因为设备需要处于完全 OS 或审核模式才能捕获 4K HH。 重置映像的一种方法是使用 Windows 中的内置 reset 功能，如下所示：

在设备上，转到 "设置" > 更新 & 安全 > 恢复 "，然后单击" 入门 "。 在 "重置此电脑" 下，选择 "删除所有内容"，只需删除文件。 最后，单击重置。

![这台电脑的 rest 屏幕截图](images/reset.png)

但是，修复工具可能无法访问 Windows，因为他们缺少用于登录的用户凭据。 在这种情况下，他们需要使用其他方法来重置设备的映像，例如 [部署映像服务和管理工具](/windows-hardware/manufacture/desktop/oem-deployment-of-windows-10-for-desktop-editions#use-a-deployment-script-to-apply-your-image)。

## <a name="return-the-repaired-device-to-the-customer"></a>将修复的设备返回给客户

已修复的设备现在可以返回给客户。 在 OOBE 期间首次启动时，它将自动注册到 Autopilot 程序中。

> [!IMPORTANT]
> 如果修复设备未重置设备的映像，则它们可能会将其发送回可能已损坏的状态。 例如，没有办法登录到设备，因为它与唯一的已知用户帐户是分离的。 因此，他们应该告诉组织他们需要自行修复注册和操作系统。
> 在接通电源之前，可以为 Autopilot "注册" 设备。 但在通过 OOBE 之前，设备并不是实际 "部署" 到 Autopilot。 因此，需要将设备重置回之前的 OOBE 状态。

## <a name="specific-repair-scenarios"></a>特定修复方案

本部分介绍最常见的修复方案及其对 Autopilot 启用的影响。

有关测试结果的说明：

- 以下方案仅适用于使用 Intune 测试 (未) 测试任何其他 MDMs 的情况。
- 在下面的大多数测试方案中，已修复并重新注册的设备需要再次通过 OOBE 才能启用 Autopilot。
- 主板更换方案通常会导致数据丢失。 在修复之前，应提醒维修中心或客户在可能) 备份数据 (。
- 当 repair 设施无法将设备信息写入已修复设备的 BIOS 时，需要创建新的进程才能成功启用 Autopilot。
- 在捕获新的 4K HH (设备 ID 之前，已修复的设备应在 BIOS 中具有产品密钥 (DPK) preinjected) 

在下表中：<br>
- 支持的 = **是**：可为 Autopilot 重新启用设备
- 支持的 = **No**：无法为 Autopilot 重新启用设备

<table>
<th>场景<th>支持<th>Microsoft 建议
<tr><td>通常 (MBR) 的主板更换<td>是<td>对于 MBR 方案，建议的操作过程是：

1. 从 Autopilot 程序取消注册 Autopilot 设备
2. 主板被替换
3. 设备是重置映像 (BIOS 信息和 DPK 重新插入文本) *
4. 在设备上捕获 (4K HH) 的新的 Autopilot 设备 ID
5. 使用新的设备 ID 重新注册 Autopilot 程序的已修复设备
6. 已修复的设备将重置为启动到 OOBE
7. 将修复的设备寄回给客户

* 如果修复技术人员有权访问客户的登录凭据，则无需重置设备的映像。 从技术上讲，可以成功地重新启用不带密钥的 MBR 和 Autopilot，或者某些 BIOS 信息 (如序列号、型号名称等) 。 但这只是出于测试/教育目的建议。

<tr><td>如果主板上 (启用了 TPM 芯片，则) 并且只会更换一个内置网卡 () <td>是<td>

1. 取消注册损坏的设备
2. 更换主板
3. 重置设备 (以获取访问) ，除非你有权访问客户的登录凭据
4. 将设备信息写入 BIOS
5. 捕获新的 4K HH
6. 重新注册修复的设备
7. 将设备重置回 OOBE
8. 浏览 Autopilot OOBE (customer) 
9. 已成功启用 Autopilot

<tr><td>如果主板上启用了 TPM 芯片 () 并且第二个网卡 (或未更换为主板的网络接口) <td>否<td>此方案打破了 Autopilot 体验。 在完成 TPM 证明之前，生成的设备 ID 将不稳定。 即使这样，注册也可能导致错误的结果，因为 MAC 地址解析存在歧义。 因此，我们不建议采用这种方案。


<tr><td>NIC 卡、HDD 和 WLAN 都在修复之后保持不变的 MBR<td>是<td>

1. 取消注册损坏的设备
2. 在 BIOS 中将主板替换为新的替换数字产品密钥 (RDPK) preinjected
3. 重置设备 (以获取访问) ，除非你有权访问客户的登录凭据
4. 将旧设备信息写入 BIOS (相同的 s/n、型号) *
5. 捕获新的 4K HH
6. 重新注册修复的设备
7. 将设备重置回 OOBE
8. 浏览 Autopilot OOBE (customer) 
9. 已成功启用 Autopilot

* 对于此方案和更高版本，重写旧设备信息不会包含 TPM 2.0 认可密钥，因为关联的私钥已锁定到 TPM 设备

<tr><td>NIC 卡保持不变，但 HDD 和 WLAN 被替换的 MBR<td>是<td>

1. 取消注册损坏的设备
2. 将主板 (替换为 BIOS) 中的新的 RDPK preinjected
3. 插入新 HDD 和 WLAN
4. 将旧设备信息写入 BIOS (相同的 s/n、型号) 
5. 捕获新的 4K HH
6. 重新注册修复的设备
7. 将设备重置回 OOBE
8. 浏览 Autopilot OOBE (customer) 
9. 已成功启用 Autopilot

<tr><td>NIC 卡和 WLAN 保持不变的 MBR，但会替换 HDD<td>是<td>

1. 取消注册损坏的设备
2. 将主板 (替换为 BIOS) 中的新的 RDPK preinjected
3. 插入新 HDD
4. 将旧设备信息写入 BIOS (相同的 s/n、型号) 
5. 捕获新的 4K HH
6. 重新注册修复的设备
7. 将设备重置回 OOBE
8. 浏览 Autopilot OOBE (customer) 
9. 已成功启用 Autopilot

<tr><td>仅替换为 MB 的 MBR (所有其他部分保持相同) 。 新 MB 是从未为 Autopilot 启用的以前使用过的设备中获取的。<td>是<td>

1. 取消注册损坏的设备
2. 将主板 (替换为 BIOS) 中的新的 RDPK preinjected
3. 重置设备 (以获取访问) ，除非你有权访问客户的登录凭据
4. 将旧设备信息写入 BIOS (相同的 s/n、型号) 
5. 捕获新的 4K HH
6. 重新注册修复的设备
7. 将设备重置回 OOBE
8. 浏览 Autopilot OOBE (customer) 
9. 已成功启用 Autopilot

<tr><td>仅替换为 MB 的 MBR (所有其他部分保持相同) 。 新 MB 是从以前使用过 Autopilot 的设备中获取的。<td>是<td>

1. 取消注册旧设备，将从其获取 MB
2. 取消注册要修复的已损坏设备 () 
3. 在 BIOS) 中，将 (Autopilot 设备中的主板替换为 MB，并将其替换为新的 RDPK preinjected。
4. 重置设备 (以获取访问) ，除非你有权访问客户的登录凭据
5. 将旧设备信息写入 BIOS (相同的 s/n、型号) 
6. 捕获新的 4K HH
7. 重新注册修复的设备
8. 将设备重置回 OOBE
9. 浏览 Autopilot OOBE (customer) 
10. 已成功启用 Autopilot

已修复的设备还可以作为普通的非 Autopilot 设备成功使用。

<tr><td>从 MBR 设备排除的 BIOS 信息<td>否<td>修复工具没有 BIOS 工具，无法在 MBR 之后将设备信息写入 BIOS。

1. 取消注册损坏的设备
2. 更换主板 (BIOS 不包含设备信息) 
3. 重新映像并将 DPK 写入图像
4. 捕获新的 4K HH
5. 重新注册修复的设备
6. 为设备创建 Autopilot 配置文件
7. 浏览 Autopilot OOBE (customer) 
8. Autopilot 无法识别修复的设备

<tr><td>没有 TPM 芯片时的 MBR<td>是<td>建议不要在不使用 TPM 芯片的情况下启用 Autopilot 设备 (这种情况下，建议) BitLocker 加密。 但是，可以在 "标准用户" 模式下启用 Autopilot 设备 (但不能) 没有 TPM 芯片的自我部署模式。 在这种情况下，您可以：

1. 取消注册损坏的设备
2. 更换主板
3. 重置设备 (以获取访问) ，除非你有权访问客户的登录凭据
4. 将旧设备信息写入 BIOS (相同的 s/n、型号) 
5. 捕获新的 4K HH
6. 重新注册修复的设备
7. 将设备重置回 OOBE
8. 浏览 Autopilot OOBE (customer) 
9. 已成功启用 Autopilot

<tr><td>新的 DPK 在已修复 Autopilot 设备上写入映像，新的 MB 为 MB<td>是<td>修复功能会在损坏的设备上替换正常 MB。 MB 不包含 BIOS 中的任何 DPK。 修复设备在 MBR 之后将 DPK 写入映像。 

1. 取消注册损坏的设备
2. 更换主板-BIOS 不包含 DPK 信息
3. 重置设备 (以获取访问) ，除非你有权访问客户的登录凭据
4. 将设备信息写入 BIOS (相同的 s/n、型号) 
5. 捕获新的 4K HH
6. 将设备重置或重新映像到预 OOBE，并将 DPK 写入映像
7. 重新注册修复的设备
8. 遍历 Autopilot OOBE
9. 已成功启用 Autopilot

<tr><td>新的修复产品密钥 (RDPK) <td>是<td>将主板用于新的 RDPK preinjected 会导致成功的 Autopilot 翻新情况。 

1. 取消注册损坏的设备
2. 将主板 (替换为 BIOS) 中的新的 RDPK preinjected
3. 重新映像或 rest 映像到预 OOBE
4. 将设备信息写入 BIOS 
5. 捕获新的 4K HH
6. 重新注册修复的设备
7. 重新映像或重置映像到预 OOBE
8. 遍历 Autopilot OOBE
9. 已成功启用 Autopilot

<tr><td>未插入 (RDPK) 的修复产品密钥<td>否<td>此方案违反了 Microsoft 策略，并打破了 Windows Autopilot 体验。
<tr><td>重置损坏的 Autopilot 设备，在修复之前未取消注册<td>是，但设备仍将与以前的租户 ID 相关联，因此应该只返回给同一客户<td>

1. 重置损坏的设备
2. 将 DPK 写入图像
3. 遍历 Autopilot OOBE
4. 已 (到以前的租户 ID，已成功启用 Autopilot) 

<tr><td>从非 Autopilot 设备到 Autopilot 设备的磁盘替换<td>是<td>

1. 请勿在修复之前取消注册已损坏的设备
2. 更换损坏设备上的 HDD
3. 重新映像或重置映像回 OOBE
4. 浏览 Autopilot OOBE (customer) 
5. Autopilot 已成功启用 (修复的设备被识别为其以前的) 

<tr><td>从一个 Autopilot 设备到另一个 Autopilot 设备的磁盘替换<td>可能<td>如果从中取出 HDD 的设备以前从 Autopilot 中注销了，则可以在修复设备中使用该 HDD。 如果在修复的设备中使用 HDD 之前未对其进行注销，则新修复的设备不会获得适当的 Autopilot 体验。

假定在此修复) 中使用之前已用过的 HDD (，请执行以下操作：

1. 取消注册损坏的设备
2. 使用来自另一个取消注册 Autopilot 设备的 HDD 替换受损设备上的 HDD
3. 重新映像或将修复后的设备放回预处理状态
4. 浏览 Autopilot OOBE (customer) 
5. 已成功启用 Autopilot

<tr><td>非 Microsoft 网卡更换 <td>否<td>在更换了第三方 () 网卡的情况下，将会破坏 Autopilot 体验。 这包括以下任何方案：

- 从非 Autopilot 设备到 Autopilot 设备
- 从一个 Autopilot 设备到另一个 Autopilot 设备
- 从 Autopilot 设备到非 Autopilot 设备

不建议采用这些方案中的任何一种。


<tr><td>设备修复了三次以上<td>否<td>重复修复设备时不支持 Autopilot。 未替换的部分将与已被替换的部分过多关联。 这使得将来很难唯一识别该设备。
<tr><td>内存替换<td>是<td>更换损坏设备上的内存不会对设备上的 Autopilot 体验产生负面影响。 不需要 de/重新注册。 修复技术人员只需更换内存即可。
<tr><td>GPU 替换<td>是<td>替换损坏设备上的 GPU () 不会对该设备上的 Autopilot 体验产生负面影响。 不需要 de/重新注册。 修复技术人员只需替换 GPU。
</table>

>当清理其他 Autopilot 设备中的部件时，我们建议从 Autopilot 取消注册的设备，对其进行清理，然后永远不会再次将清理的 (设备注册到 AUTOPILOT) ，因为重复使用此方法可能会导致两个活动设备最终具有相同的 ID，因此，不可能区分这两者。

以下部分可能会被替换，而不会影响 Autopilot 启用或需要特殊的额外修复步骤：
- 内存 (RAM 或 ROM) 
- 电源
- 视频卡片
- 读卡器
- 声卡
- 扩展卡
- 麦克风
- 摄像头
- 风扇
- 散热器
- CMOS 电池

尚未测试和验证的其他修复方案包括：
- Daughterboard 替换
- CPU 更换
- Wifi 替换
- 替换以太网

## <a name="faq"></a>常见问题解答

| 问题 | Answer |
| --- | --- |
| 我们有一种工具，该工具会在 MBR 之后将产品信息计划给 BIOS。 是否仍需要提交 CBR 报表，使设备能够进行 Autopilot？ | 不是。 如果单元中的工具将所需的最少信息写入到 Autopilot 程序查找来识别设备的 BIOS 中，如本文档前面所述。 |
| 如果只替换部分组件而不是完整的主板，会发生什么情况呢？ | 很多情况是，某些有限修复不会阻止 Autopilot 算法成功将修复后设备与预修复设备匹配。 即使是这样，也最好通过执行上述 MBR 步骤来确保100% 的成功，即使是只需有限修复的设备。 |
| 如果客户没有客户的登录凭据，修复技术人员如何获取对损坏设备的访问权限？ | 技术人员必须在修复过程中重新映像设备，并使用其自己的凭据。 |

## <a name="related-topics"></a>相关主题

[设备指导原则](autopilot-device-guidelines.md)<br>