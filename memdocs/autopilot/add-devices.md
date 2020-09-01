---
title: 添加设备
ms.reviewer: ''
manager: laurawi
description: 如何将设备添加到 Windows Autopilot
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
ms.openlocfilehash: 0070492304fc75bf51b6eda929c274076c7b2452
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193811"
---
# <a name="adding-devices-to-windows-autopilot"></a>将设备添加到 Windows Autopilot

**适用于**

- Windows 10

使用 Windows Autopilot 部署设备之前，必须向 Windows Autopilot 部署服务注册设备。 理想情况下，此注册由购买设备的 OEM、经销商或分销商执行。 不过，也可以通过收集硬件标识并手动上载来在你的组织内完成注册。

## <a name="oem-registration"></a>OEM 注册

从 OEM 购买设备时，OEM 可以使用 Windows Autopilot 自动注册设备。 有关支持注册的 Oem 列表，请参阅 [Windows Autopilot 页面](https://aka.ms/windowsautopilot)的 "参与方设备制造商和经销商" 部分。

在 OEM 可以为组织注册设备之前，组织必须授予 OEM 权限才能执行此操作。 OEM 会开始此过程，批准由组织的 Azure AD 全局管理员授予。 请参阅 [客户同意页](registration-auth.md#oem-authorization)的 "客户同意" 一节。

> [!Note]
> 尽管硬件哈希 (也称为硬件 Id) 在 OEM 设备制造过程中生成，但不应直接向客户或 CSP 合作伙伴提供这些 Id。 相反，OEM 应代表客户注册设备。 在 CSP 合作伙伴注册设备的情况下，Oem 可能会向这些合作伙伴提供 PKID 信息，以支持设备注册过程。

## <a name="reseller-distributor-or-partner-registration"></a>经销商、分销商或合作伙伴注册

客户可以从经销商、分销商或其他合作伙伴购买设备。 只要这些经销商、分销商和合作伙伴是 [云解决方案合作伙伴 (CSP) 计划](https://partner.microsoft.com/cloud-solution-provider)的一部分，他们也可以为客户注册设备。 

与 Oem 一样，必须授予 CSP 伙伴为组织注册设备的权限。 你可以使用 [客户同意页](registration-auth.md#csp-authorization)上所述的过程。 CSP 合作伙伴请求与组织之间的关系。 该组织的全局管理员批准该请求。 批准后，CSP 合作伙伴将使用 [合作伙伴中心](https://partner.microsoft.com/pcv/dashboard/overview)直接添加设备，无论是直接通过网站还是通过可用的 api，可以自动执行相同的任务。

在 CSP 伙伴和组织之间建立关系时，Windows Autopilot 不需要委派的管理员权限。 作为全局管理员审批过程的一部分，他们可以选择取消选中 "包括委派的管理权限" 复选框。

> [!Note]
> 虽然经销商、分销商或合作伙伴可以启动每个新的 Windows 设备以获取硬件哈希 (以便向客户提供这些硬件哈希，或由合作伙伴) 直接注册，但不建议这样做。 相反，这些合作伙伴应使用从设备打包 (获取的 PKID 信息注册设备，) 或从 OEM 或上游 (合作伙伴（例如分销商) ）以电子方式获取。

## <a name="automatic-registration-of-existing-devices"></a>自动注册现有设备

如果存在以下情况，可以自动注册现有设备：
- 运行受支持版本的 Windows 10 半年频道
- 已在 Intune 服务（如 Intune）中注册。

对于同时满足这两个要求的设备，MDM 服务可以要求设备提供硬件哈希。 完成后，它可以自动向 Windows Autopilot 注册设备。
有关如何使用 Microsoft Intune 执行此操作的说明，请参阅 [创建 Autopilot 部署配置文件](/intune/enrollment-autopilot#create-an-autopilot-deployment-profile) 文档，其中介绍了 "将所有目标设备转换为 Autopilot" 设置。 

可以使用 Intune **将所有目标设备转换为 Autopilot** 设置，自动将此类设备转换为 Windows。 有关详细信息，请参阅[创建 Autopilot 部署配置文件](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-deployment-profile)。 

使用 [Windows Autopilot for 现有设备](existing-devices.md) 方案时，无需在 windows Autopilot 中预注册设备。 而是使用) 包含所有 Windows Autopilot 配置文件设置的的配置 ( 文件。 然后，可以使用相同的 "将所有目标设备转换为 Autopilot" 设置向 Windows Autopilot 注册设备。

## <a name="manual-registration"></a>手动注册

若要手动注册设备，必须先捕获其硬件哈希。 完成此过程后，可以将生成的硬件哈希上传到 Windows Autopilot 服务。 由于此过程需要将设备引导到 Windows 10 以获取硬件哈希，因此，手动注册主要用于测试和评估方案。

> [!Note]
> 客户只能向硬件哈希注册设备。  (PKID、元组) 的其他方法可通过 Oem 或 CSP 合作伙伴获得，如前一部分中所述。

## <a name="device-identification"></a>设备标识

若要使用 Windows Autopilot 标识设备，必须捕获设备的唯一硬件哈希，并将其上传到服务。 此步骤理想的做法是，硬件供应商 (OEM、经销商或分销商) 自动将设备与组织相关联。 还可以使用从正在运行的 Windows 10 安装中收集设备的收集过程来识别设备。

硬件哈希包含有关设备的详细信息：
- 制造商
- model
- 设备序列号
- 硬盘驱动器序列号
- 有关 ID 生成时间的详细信息
- 可用于唯一标识设备的许多其他属性

每次生成硬件哈希都会发生更改，因为它包括有关生成时间的详细信息。 当 Windows Autopilot 部署服务尝试匹配某个设备时，它会考虑此类更改。 它还考虑了一些大的更改，例如新的硬盘，并且仍能够成功匹配。 但对硬件的大更改（如主板更换）不匹配，因此需要生成并上传新的哈希。

### <a name="collecting-the-hardware-hash-from-existing-devices-using-microsoft-endpoint-configuration-manager"></a>使用 Microsoft 终结点从现有设备收集硬件哈希 Configuration Manager

Microsoft 端点 Configuration Manager 自动收集现有 Windows 10 设备的硬件哈希。 有关详细信息，请参阅 [从 Windows Autopilot 的 Configuration Manager 中收集信息](/configmgr/comanage/how-to-prepare-win10#windows-autopilot)。 可以将哈希信息从 Configuration Manager 提取到 CSV 文件中。

> [!Note]
> 在 Intune 上上传 CSV 文件之前，请确保第一行包含设备序列号、Windows 产品 ID、硬件哈希、组标记和分配的用户。 如果 CSV 文件顶部有标题信息，请删除该标头信息。 请参阅在 [Intune 中注册 Windows 设备中](/intune/enrollment/enrollment-autopilot)的详细信息。

### <a name="collecting-the-hardware-hash-from-existing-devices-using-powershell"></a>使用 PowerShell 从现有设备收集硬件哈希

可以通过 Windows Management Instrumentation (WMI) 获取现有设备的硬件哈希，只要该设备运行的是受支持版本的 Windows 10 半年频道即可。 可以使用 PowerShell 脚本 ([Get-WindowsAutoPilotInfo.ps1](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo) 获取设备的硬件哈希和序列号。 序列号可用于快速查看硬件哈希所属的设备。

若要使用此脚本，可以使用以下方法之一：
- 从 PowerShell 库下载并在每台计算机上运行。
- 直接从 PowerShell 库安装。

若要直接安装并捕获本地计算机中的硬件哈希，请在提升的 Windows PowerShell 提示符下使用以下命令：

```powershell
md c:\\HWID
Set-Location c:\\HWID
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted
Install-Script -Name Get-WindowsAutoPilotInfo
Get-WindowsAutoPilotInfo.ps1 -OutputFile AutoPilotHWID.csv
```

如果以下两个条件均为 true，则可以远程运行命令：
- WMI 权限已准备就绪
- 可以通过远程计算机上的 Windows 防火墙访问 WMI。

有关运行脚本的详细信息，请参阅 [WindowsAutoPilotInfo](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo) 脚本的帮助，方法是使用 "get-help Get-WindowsAutoPilotInfo.ps1"。

>[!IMPORTANT]
>在捕获硬件哈希和创建 Autopilot 设备配置文件之前，请不要将设备连接到 Internet。 这包括收集硬件哈希，并上传。CSV 到 MSfB 或 Intune，分配配置文件，然后确认配置文件分配。 在此过程完成之前，将设备连接到 Internet 会导致设备下载存储在设备上的空白配置文件，直到显式删除。 在 Windows 10 版本1809中，可以通过重新启动 OOBE 来清除缓存的配置文件。 在以前的版本中，清除存储的配置文件的唯一方法是重新安装操作系统、重置 PC 映像或运行 **sysprep/generalize/oobe**。 <br>
>Intune 报告配置文件准备就绪后，只应将设备连接到 Internet。

>[!NOTE]
>如果 OOBE 重启的次数太多，则可以进入恢复模式，并且无法运行 Autopilot 配置。 如果 OOBE 在同一页面上显示多个配置选项（包括语言、区域和键盘布局），则可以确定此方案。 一般 OOBE 在单独的页面上显示每个。 以下值键跟踪 OOBE 重试计数： <br>
>**HKCU\SOFTWARE \\ Microsoft \\ Windows \\ CurrentVersion \\ UserOOBE** <br>
>若要确保 OOBE 的重新启动次数过多，可以将此值更改为1。

## <a name="registering-devices"></a>注册设备

<img src="./images/image2.png" width="511" height="249" alt="process" />


从现有设备中捕获硬件哈希后，可以通过以下任一方式上传它们：

- [Microsoft Intune](enrollment-autopilot.md)。 这是适用于所有客户的首选机制。
  - Microsoft 终结点管理器管理中心用于 Intune 设备注册。
- [合作伙伴中心](https://msdn.microsoft.com/partner-center/autopilot)。 CSP 合作伙伴使用此方法代表客户注册设备。
- [Microsoft 365 商业版 & Office 365 管理员](https://support.office.com/article/Create-and-edit-AutoPilot-profiles-5cf7139e-cfa1-4765-8aad-001af1c74faa)。这通常由小型和中型企业使用， (使用 Microsoft 365 商业版管理其设备的 Smb) 。
- [适用于企业的 Microsoft Store](/microsoft-store/add-profile-to-devices#manage-autopilot-deployment-profiles)。 可能已在使用 MSfB 管理应用和设置。

下面提供每个平台的功能的摘要。<br>
<br>
<table>
<tr>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">平台/门户</font></td>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">注册设备？</font></td>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">创建/分配配置文件</font></td>
<td BGCOLOR="#a0e4fa"><B><font color="#000000">可接受的 DeviceID</font></td>
</tr>

<tr>
<td>OEM 直接 API</td>
<td>是-1000，最大时间</td>
<td>是</td>
<td>元组或 PKID</td>
</tr>

<tr>
<td><a href="https://docs.microsoft.com/partner-center/autopilot">合作伙伴中心</a></td>
<td>是-1000，最大时间</td>
<td>是<b><sup>34</sup></b></td>
<td>元组或 PKID 或 4K HH</td>
</tr>

<tr>
<td><a href="enrollment-autopilot.md">Intune</a></td>
<td>是-500，最大值为<b><sup>1</sup></b></td> 
<td>是<b><sup>12</sup></b></td> 
<td>4K HH</td>
</tr>

<tr>
<td><a href="https://docs.microsoft.com/microsoft-store/add-profile-to-devices#manage-autopilot-deployment-profiles">适用于企业的 Microsoft Store</a></td>
<td>是-1000，最大时间</td>
<td>是<b><sup>4</sup></b></td>
<td>4K HH</td>
</tr>

<tr>
<td><a href="https://docs.microsoft.com/microsoft-365/business/create-and-edit-autopilot-profiles">Microsoft 365 商业高级版</a></td>
<td>是-1000，最大时间</td>
<td>是<b><sup>3</sup></b></td>
<td>4K HH</td>
</tr>

</table>

><b><sup>1</sup></b>要使用的 Microsoft 推荐平台<br>
><b><sup>2</sup></b>需要 Intune 许可证<br>
><b><sup>3</sup></b>功能有限<br>
><b><sup>4</sup></b>在未来几个月，将从 MSfB 和合作伙伴中心停用设备配置文件分配<br>

有关设备 Id 的详细信息，请参阅以下主题：
- [设备标识](#device-identification)
- [Windows Autopilot 设备指南](autopilot-device-guidelines.md)
- [向客户帐户添加设备](/partner-center/autopilot)


## <a name="summary"></a>“摘要”

使用 Windows Autopilot 部署新设备时，需要执行以下步骤：

1. [注册设备](#registering-devices)。 理想情况下，此步骤由购买设备的 OEM、经销商或分销商执行。 不过，也可以通过收集硬件标识并手动上传来完成注册。
2. [配置设备配置文件](profiles.md)。 指定应如何部署设备以及应显示的用户体验。
3. 启动设备。 如果设备已连接到具有 internet 访问权限的网络，则它将与 Windows Autopilot 部署服务联系，以查看设备是否已注册。 如果已注册，则会下载配置文件设置，如 [注册状态页](enrollment-status.md)，这些设置用于自定义最终用户体验。

## <a name="next-steps"></a>后续步骤

[Bitlocker 加密设置](bitlocker.md)：可以将 bitlocker 加密设置配置为在开始自动加密之前应用。