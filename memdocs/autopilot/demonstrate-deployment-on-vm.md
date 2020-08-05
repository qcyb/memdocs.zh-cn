---
title: 演示 Autopilot 部署
ms.reviewer: ''
manager: laurawi
description: 有关如何使用 Windows Autopilot 部署设置虚拟机的分步说明
keywords: mdm，安装程序，windows，windows 10，oobe，管理，部署，autopilot，ztd，零接触，合作伙伴，msfb，intune，升级
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.custom: autopilot
ms.openlocfilehash: 7ff25816c0398389fc23bbde4983f4bc9556d192
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756471"
---
# <a name="demonstrate-autopilot-deployment"></a>演示 Autopilot 部署

**适用于**

- Windows 10

若要开始使用 Windows Autopilot，应使用 (VM) 的虚拟机进行尝试，也可以使用需要擦除的物理设备，然后重新安装 Windows 10。

在本主题中，你将了解如何使用 Hyper-v 为 VM 设置 Windows Autopilot 部署。

> [!NOTE]
> 尽管有[多个平台](add-devices.md#registering-devices)可用于启用 Autopilot，但此实验室主要使用 Intune。

> 此实验室不需要 hyper-v 和 VM。 你还可以使用物理设备。 但是，说明假定你使用的是 VM。 若要使用物理设备，请跳过有关安装 Hyper-v 和创建 VM 的说明。 本指南中对 "device" 的所有引用都引用客户端设备（物理或虚拟）。

以下视频概述了该过程：

</br>
<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/KYVptkpsOqs" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

> 有关本指南中使用的术语的列表，请参阅[术语表](#glossary)部分。

## <a name="prerequisites"></a>先决条件

下面是完成此实验室所需的操作：
<table><tr><td>Windows 10 安装媒体</td><td>Windows 10 专业版或企业版 (ISO file) ，获取受支持版本的 Windows 10、半年频道。 如果尚未使用 ISO，则会提供一个链接，用于下载<a href="https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise" data-raw-source="[evaluation version of Windows 10 Enterprise](https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise)">Windows 10 企业版的评估版</a>。</td></tr>
<tr><td>Internet 访问权限</td><td>如果你位于防火墙后面，请参阅详细的<a href="windows-autopilot-requirements.md#networking-requirements" data-raw-source="[networking requirements](windows-autopilot-requirements.md#networking-requirements)">网络要求</a>。 否则，只需确保已连接到 Internet。</td></tr>
<tr><td>Hyper-v 或运行 Windows 10 的物理设备</td><td>本指南假定你将使用 Hyper-v VM，并提供有关安装和配置 Hyper-v 的说明（如果需要）。 若要使用物理设备，请跳过安装和配置 Hyper-v 的步骤。</td></tr>
<tr><td>高级 Intune 帐户</td><td>本指南将介绍如何获取可用于完成实验室的免费30天试用版帐户。</td></tr></table>

## <a name="procedures"></a>过程

下面提供了实验室中部分和过程的摘要。 按显示的顺序跟踪每个部分，跳过不适用于您的部分。 附录中提供了可选过程。

[验证 Hyper-v 支持](#verify-support-for-hyper-v)
<br>[启用 Hyper-V](#enable-hyper-v)
<br>[创建演示 VM](#create-a-demo-vm)
<br>&nbsp;&nbsp;&nbsp;[设置 ISO 文件位置](#set-iso-file-location)
<br>&nbsp;&nbsp;&nbsp;[确定网络适配器名称](#determine-network-adapter-name)
<br>&nbsp;&nbsp;&nbsp;  [使用 Windows PowerShell 创建演示 VM](#use-windows-powershell-to-create-the-demo-vm)
<br>&nbsp;&nbsp;&nbsp;[安装 Windows 10](#install-windows-10)
<br>[捕获硬件 ID](#capture-the-hardware-id)
<br>[将 VM 重置回全新体验 (OOBE) ](#reset-the-vm-back-to-out-of-box-experience-oobe)
<br>[验证订阅级别](#verify-subscription-level)
<br>[配置公司品牌](#configure-company-branding)
<br>[配置 Microsoft Intune 自动注册](#configure-microsoft-intune-auto-enrollment)
<br>[注册 VM](#register-your-vm)
<br>&nbsp;&nbsp;&nbsp;[使用 Intune 注册 Autopilot](#autopilot-registration-using-intune)
<br>&nbsp;&nbsp;&nbsp;[使用 MSfB 的 Autopilot 注册](#autopilot-registration-using-msfb)
<br>[创建和分配 Windows Autopilot 部署配置文件](#create-and-assign-a-windows-autopilot-deployment-profile)
<br>&nbsp;&nbsp;&nbsp;[使用 Intune 创建 Windows Autopilot 部署配置文件](#create-a-windows-autopilot-deployment-profile-using-intune)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[分配配置文件](#assign-the-profile)
<br>&nbsp;&nbsp;&nbsp;[使用 MSfB 创建 Windows Autopilot 部署配置文件](#create-a-windows-autopilot-deployment-profile-using-msfb)
<br>[查看 Windows Autopilot 的操作](#see-windows-autopilot-in-action)
<br>[从 Autopilot 删除设备](#remove-devices-from-autopilot)
<br>&nbsp;&nbsp;&nbsp;[删除 (取消注册) Autopilot 设备](#delete-deregister-autopilot-device)
<br>[附录 A：验证对 Hyper-v 的支持](#appendix-a-verify-support-for-hyper-v)
<br>[附录 B：将应用添加到配置文件](#appendix-b-adding-apps-to-your-profile)
<br>&nbsp;&nbsp;&nbsp;[添加 Win32 应用](#add-a-win32-app)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[准备 Intune 应用](#prepare-the-app-for-intune)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[在 Intune 中创建应用](#create-app-in-intune)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[将应用分配到 Intune 配置文件](#assign-the-app-to-your-intune-profile)
<br>&nbsp;&nbsp;&nbsp;[添加 Office 365](#add-office-365)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[在 Intune 中创建应用](#create-app-in-intune)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[将应用分配到 Intune 配置文件](#assign-the-app-to-your-intune-profile)
<br>[术语表](#glossary)

## <a name="verify-support-for-hyper-v"></a>验证 Hyper-v 支持

如果还没有 Hyper-v，则必须先在运行 Windows 10 或 Windows Server (2012 R2 或更高版本) 的计算机上启用它。

> 如果已启用 Hyper-v，请跳到[创建演示 VM](#create-a-demo-vm)步骤。 如果使用的是物理设备而不是 VM，请跳到[安装 Windows 10](#install-windows-10)。

如果你不确定设备是否支持 Hyper-v，或者安装 Hyper-v 时遇到问题，请参阅下面的[附录 A](#appendix-a-verify-support-for-hyper-v) ，详细了解如何验证是否能成功安装 hyper-v。

## <a name="enable-hyper-v"></a>启用 Hyper-V

若要启用 Hyper-v，请打开提升的 Windows PowerShell 提示符，并运行以下命令：

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```

此命令适用于支持 Hyper-v 的所有操作系统，但在 Windows Server 操作系统上，你必须在) 下键入附加命令 (，才能添加 Hyper-v Windows PowerShell 模块和 Hyper-v 管理器控制台。 以下命令还将安装 Hyper-v （如果尚未安装），因此，如果使用的是 Windows Server，只需键入以下命令，而不是使用 WindowsOptionalFeature 命令：

```powershell
Install-WindowsFeature -Name Hyper-V -IncludeManagementTools
```

在提示你重启计算机时，选择**是**。 计算机可能会重启多次。

> 或者，你可以使用 Windows 控制面板中的**打开或关闭 Windows 功能**（客户端操作系统）或者使用服务器管理器的**添加角色和功能向导**（服务器操作系统）来安装 Hyper-V，如下所示：

   ![Hyper-v 功能](images/hyper-v-feature.png)

   ![Hyper-V](images/svr_mgr2.png)

<P>如果选择使用服务器管理器安装 Hyper-V，请接受所有默认选择。 此外，请确保安装 <strong>Role Administration Tools\Hyper-V Management Tools</strong> 下的两项。

安装完成后，通过在提升的命令提示符处键入**virtmgmt** ，或在 "开始" 菜单搜索框中键入 " **hyper-v** "，打开 hyper-v 管理器。

若要了解有关 Hyper-v 的详细信息，请参阅 windows [10 上的 hyper-v](https://docs.microsoft.com/virtualization/hyper-v-on-windows/about/)和[windows Server 上的 hyper-v](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-on-windows-server)。

## <a name="create-a-demo-vm"></a>创建演示 VM

现在 Hyper-v 已启用，我们需要创建运行 Windows 10 的虚拟机。 我们可以使用 Hyper-v 管理器[创建 VM](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/create-virtual-machine)和[虚拟网络](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/connect-to-network)，但使用 Windows PowerShell 更为简单。

若要使用 Windows PowerShell，只需了解两项内容：

1. Windows 10 ISO 文件的位置。
   - 在此示例中，我们假定位置是**c:\iso\win10-eval.iso**。
2. 连接到 Internet 的网络接口的名称。
   - 在此示例中，我们使用 Windows PowerShell 命令来自动确定这一点。

设置 ISO 文件位置并确定适当的网络接口的名称后，可以安装 Windows 10。

### <a name="set-iso-file-location"></a>设置 ISO 文件位置

你可以在[此处](https://www.microsoft.com/evalcenter/evaluate-windows-10-enterprise)下载最新版本的 Windows 10 企业版的 ISO 文件。
- 当系统要求选择平台时，选择**64 位**。

下载此文件后，该名称将非常长 (例如： 17763.107.101029-1455. rs5_release_svc_refresh_CLIENTENTERPRISEEVAL_OEMRET_x64FRE_en-us) 。

1. 为了更轻松地键入和记住，请将该文件重命名为**win10-eval**。
2. 在计算机上创建一个名为**c:\iso**的目录，并将**win10-eval**文件移到该处，因此该文件的路径为**c:\iso\win10-eval.iso**。
3. 如果要为文件使用其他名称和位置，必须修改以下 Windows PowerShell 命令，以使用自定义名称和目录。

### <a name="determine-network-adapter-name"></a>确定网络适配器名称

下面使用 NetAdaper cmdlet 来自动找到最有可能是你用来连接到 Internet 的网络适配器。 应该先通过在权限提升的 Windows PowerShell 提示符下运行以下命令来测试此命令：

```powershell
(Get-NetAdapter |?{$_.Status -eq "Up" -and !$_.Virtual}).Name
```

此命令的输出应为用于连接到 Internet 的网络接口的名称。 验证此接口名称是否正确。 如果接口名称不正确，则需要编辑下面的第一个命令，以便使用您的网络接口名称。

例如，如果上面的命令显示以太网，但你想要使用 Ethernet2，则下面的第一个命令将是 AutopilotExternal-AllowManagementOS $true-NetAdapterName **Ethernet2**的第一个命令。

### <a name="use-windows-powershell-to-create-the-demo-vm"></a>使用 Windows PowerShell 创建演示 VM

所有 VM 数据都将在 PowerShell 提示符下的当前路径下创建。 在运行以下命令之前，请考虑导航到新的文件夹。

> [!IMPORTANT]
> **Vm 交换机**： vm 交换机是指 hyper-v 如何将 vm 连接到网络。 <br><br>如果以前启用了 Hyper-v，并且 Internet 连接的网络接口已绑定到 VM 交换机，则下面的 PowerShell 命令将失败。 在这种情况下，你可以删除现有的 VM 交换机 (以便下面的命令可以创建一个) ，也可以通过跳过下面的第一个命令，并修改第二个命令将开关名称**AutopilotExternal**替换为你的开关的名称，或者将现有交换机重命名为 "AutopilotExternal" 来重复使用此 vm 交换机。<br><br>如果之前从未创建过外部 VM 交换机，只需运行以下命令即可。

```powershell
New-VMSwitch -Name AutopilotExternal -AllowManagementOS $true -NetAdapterName (Get-NetAdapter |?{$_.Status -eq "Up" -and !$_.Virtual}).Name
New-VM -Name WindowsAutopilot -MemoryStartupBytes 2GB -BootDevice VHD -NewVHDPath .\VMs\WindowsAutopilot.vhdx -Path .\VMData -NewVHDSizeBytes 80GB -Generation 2 -Switch AutopilotExternal
Add-VMDvdDrive -Path c:\iso\win10-eval.iso -VMName WindowsAutopilot
Start-VM -VMName WindowsAutopilot
```

输入这些命令后，连接到刚创建的 VM，并等待按下某个键并从 DVD 启动的提示。  可以通过在 Hyper-v 管理器中双击 VM 来连接到该 VM。

请参阅下面的示例输出。 在此示例中，将在**c:\autopilot**目录下创建 VM，并使用 vmconnect.exe 命令 (仅在 Windows Server) 上可用。 如果在 Windows 10 上安装了 Hyper-v，请使用 Hyper-v 管理器连接到你的 VM。

<pre style="overflow-y: visible">
PS C:\autopilot&gt; dir c:\iso


    Directory: C:\iso


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/12/2019   2:46 PM     4627343360 win10-eval.iso

PS C:\autopilot&gt; (Get-NetAdapter |?{$<em>.Status -eq &quot;Up&quot; -and !$</em>.Virtual}).Name
Ethernet
PS C:\autopilot&gt; New-VMSwitch -Name AutopilotExternal -AllowManagementOS $true -NetAdapterName (Get-NetAdapter |?{$<em>.Status -eq &quot;Up&quot; -and !$</em>.Virtual}).Name

Name              SwitchType NetAdapterInterfaceDescription
----              ---------- ------------------------------
AutopilotExternal External   Intel(R) Ethernet Connection (2) I218-LM

PS C:\autopilot&gt; New-VM -Name WindowsAutopilot -MemoryStartupBytes 2GB -BootDevice VHD -NewVHDPath .\VMs\WindowsAutopilot.vhdx -Path .\VMData -NewVHDSizeBytes 80GB -Generation 2 -Switch AutopilotExternal

Name             State CPUUsage(%) MemoryAssigned(M) Uptime   Status             Version
----             ----- ----------- ----------------- ------   ------             -------
WindowsAutopilot Off   0           0                 00:00:00 Operating normally 8.0

PS C:\autopilot&gt; Add-VMDvdDrive -Path c:\iso\win10-eval.iso -VMName WindowsAutopilot
PS C:\autopilot&gt; Start-VM -VMName WindowsAutopilot
PS C:\autopilot&gt; vmconnect.exe localhost WindowsAutopilot
PS C:\autopilot&gt; dir

    Directory: C:\autopilot

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        3/12/2019   3:15 PM                VMData
d-----        3/12/2019   3:42 PM                VMs

PS C:\autopilot&gt;
</pre>

### <a name="install-windows-10"></a>安装 Windows 10

确保从安装 ISO 启动 VM，单击 "**下一步**"，然后单击 "**立即安装**" 并完成 Windows 安装过程。 请看以下示例：

   ![Windows 安装程序 windows 安装程序 windows ](images/winsetup1.png) ![ ](images/winsetup2.png) ![ 安装 ](images/winsetup3.png) ![ ](images/winsetup4.png) ![ ](images/winsetup5.png) ![ 程序 windows 安装程序 windows 安装程序](images/winsetup6.png)

VM 重启后，在 OOBE 期间，请改为选择 "**设置为个人用途**" 或 "**加入域**"，然后在**登录**屏幕上选择 "脱机帐户"。  这将为桌面提供最快的方法。 例如：

   ![Windows 安装程序](images/winsetup7.png)

安装完成后，登录并验证你是否在 Windows 10 桌面上，然后创建你的第一个 Hyper-v 检查点。 使用检查点将虚拟机还原到以前的状态。 你将在此实验室中创建多个检查点，以后可以使用这些检查点再次执行该过程。

   ![Windows 安装程序](images/winsetup8.png)

若要创建第一个检查点，请在运行 Hyper-v 的计算机上打开提升的 Windows PowerShell 提示符 (不在 VM) 上，并运行以下命令：

```powershell
Checkpoint-VM -Name WindowsAutopilot -SnapshotName "Finished Windows install"
```

单击 "Hyper-v 管理器" 中的**WindowsAutopilot** VM，并验证是否已在 "检查点" 窗格中看到 "**已完成 Windows 安装**"。

## <a name="capture-the-hardware-id"></a>捕获硬件 ID

> [!NOTE]
> 通常，设备 ID 是由 OEM 捕获的，因为它们在工厂中的每个设备上运行 OA3 工具。  然后，OEM 将由 OA3 工具创建的 4K HH 提交给 Microsoft，方法是将它与计算机生成报表一起提交， (CBR) 。  出于本实验室的目的，你将充当捕获 4K HH) 的 OEM (，但不打算使用 OA3 工具捕获完整的 4K (HH，因为你需要安装 OA3 工具、你的设备不能具有批量许可版本的 Windows，而是比使用 PS 脚本等 ) 更复杂。  相反，你将通过运行 PowerShell 脚本来模拟运行 OA3 工具，该脚本将捕获设备 4K HH，就像 OA3 工具一样。

请按照以下步骤运行 PS 脚本：

1. 打开提升的 Windows PowerShell 提示符，并运行以下命令。 无论你使用的是 VM 还是物理设备，这些命令都是相同的：

    ```powershell
    md c:\HWID
    Set-Location c:\HWID
    Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted -Force
    Install-Script -Name Get-WindowsAutopilotInfo -Force
    $env:Path += ";C:\Program Files\WindowsPowerShell\Scripts"
    Get-WindowsAutopilotInfo.ps1 -OutputFile AutopilotHWID.csv
    ```

当系统提示你安装 NuGet 包时，请选择 **"是"**。

请参阅下面的示例输出。

<pre>
PS C:\> md c:\HWID

    Directory: C:\

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        3/14/2019  11:33 AM                HWID

PS C:\> Set-Location c:\HWID
PS C:\HWID> Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted -Force
PS C:\HWID> Install-Script -Name Get-WindowsAutopilotInfo -Force

NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet
 provider must be available in 'C:\Program Files\PackageManagement\ProviderAssemblies' or
'C:\Users\user1\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running
 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and
import the NuGet provider now?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y
PS C:\HWID> $env:Path += ";C:\Program Files\WindowsPowerShell\Scripts"
PS C:\HWID> Get-WindowsAutopilotInfo.ps1 -OutputFile AutopilotHWID.csv
PS C:\HWID> dir

    Directory: C:\HWID

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/14/2019  11:33 AM           8184 AutopilotHWID.csv

PS C:\HWID>
</pre>

验证**c:\HWID**目录中是否有一个大小约为 8 KB 的**AutopilotHWID.csv**文件。  此文件包含完整的 4K HH。

> [!NOTE]
> 尽管 .csv 扩展名可能与 Microsoft Excel 相关联，但您不能通过双击来正确查看文件。 若要正确分析逗号分隔符并在 excel 中查看文件，必须使用 excel 中**的**  >  **文本/CSV**函数导入相应的数据列。 不需要在 Excel 中查看该文件，除非您感到好奇。 文件格式将在导入到 Autopilot 时进行验证。 下面显示了此文件中的数据示例。

![序列号和硬件哈希](images/hwid.png)

需要将此数据上传到 Intune，以便为 Autopilot 注册设备，因此需要将其传输到将用于访问 Azure 门户的计算机。  如果你使用的是物理设备而不是 VM，则可以将该文件复制到 USB 记忆棒。  如果你使用的是 VM，则可以右键单击 AutopilotHWID.csv 文件并复制它，然后右键单击并将该文件粘贴到 VM) 外的桌面 (。

如果复制和粘贴该文件时遇到问题，只需在 VM 上的记事本中查看其内容，然后将该文本复制到 VM 外部的记事本中。 不要使用其他文本编辑器来执行此操作。

> [!NOTE]
> 当在 Vm 之间进行复制和粘贴时，请避免在复制和粘贴过程之间用鼠标光标单击其他东西，因为这样可以清空或覆盖剪贴板，并需要重新开始。 直接从 "复制" 以粘贴。

## <a name="reset-the-vm-back-to-out-of-box-experience-oobe"></a>将 VM 重置回全新体验 (OOBE) 

使用在文件中捕获的硬件 ID，为 Windows Autopilot 部署准备虚拟机，方法是将其重置回 OOBE。

在虚拟机上，转到**设置 > 更新和安全 > 恢复**，然后在**重置此电脑**下单击**开始使用**。
选择**删除所有内容**和**仅删除我的文件**。 最后，单击**重置**。

![重置此电脑最终提示](images/autopilot-reset-prompt.jpg)

重置 VM 或设备可能需要一段时间。 继续执行下一步 (验证重置过程中的订阅级别) 。

![重置此电脑的屏幕截图](images/autopilot-reset-progress.jpg)

## <a name="verify-subscription-level"></a>验证订阅级别

对于此实验，需要一个 AAD Premium 订阅。  可以通过导航到 " [MDM 注册配置](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Mobility)" 边栏选项卡来判断是否具有高级订阅。 请参阅以下示例：

**Azure Active Directory**  > ** (MDM 和 MAM) **  >  的移动性**Microsoft Intune**

![MDM 和 Intune](images/mdm-intune2.png)

如果上面显示的配置边栏选项卡未出现，则很可能你没有**高级**订阅。  自动注册是一项仅适用于 AAD 高级版的功能。

若要将 Intune 试用帐户转换为免费的高级试用帐户，请导航到 "所有产品的**Azure Active Directory**  >  **许可证**"，  >  **All products**  >  **Try / Buy**并选择 "**免费试用 Azure AD Premium 版**" 或 "EMS E5"。

![重置此电脑最终提示](images/aad-lic1.png)

## <a name="configure-company-branding"></a>配置公司品牌

如果你已在 Azure Active Directory 中配置了公司品牌，则可以跳过此步骤。

> [!IMPORTANT]
> 请确保使用全局管理员帐户进行登录。

在 Azure Active Directory 中导航到 "[公司品牌](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/LoginTenantBranding)"，单击 "**配置**"，并配置在 OOBE 期间要查看的任何类型的公司品牌。

![配置公司品牌](images/branding.png)

完成后，单击“保存”。****

> [!NOTE]
> 应用对公司品牌所做的更改最多可能需要 30 分钟。

## <a name="configure-microsoft-intune-auto-enrollment"></a>配置 Microsoft Intune 自动注册

如果你已在 Azure Active Directory 中配置了 MDM 自动注册，则可以跳过此步骤。

[在 Azure Active Directory 打开移动 (MDM 和 MAM) ](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Mobility) ，然后选择 " **Microsoft Intune**"。 如果看不到 Microsoft Intune，请单击 "**添加应用程序**"，然后选择 " **Intune**"。

为了此演示目的，在 **MDM 用户范围**下选择**全部**，然后单击**保存**。

![“移动性”边栏选项卡中的“MDM 用户范围”](images/autopilot-aad-mdm.png)

## <a name="register-your-vm"></a>注册 VM

你的 VM (或设备) 可以通过 Intune 或 Microsoft Store for Business (MSfB) 进行注册。  此处显示了这两个进程，但只是为了此实验室<u>选取一个</u>进程。 我们强烈建议使用 Intune，而不是 MSfB。

### <a name="autopilot-registration-using-intune"></a>使用 Intune 注册 Autopilot

1. 在 Azure 门户的 Intune 中，选择 "**设备注册**" "  >  **Windows 注册**  >  **设备**" "  >  **导入**"。

    ![Intune 设备导入](images/device-import.png)

    > [!NOTE]
    > 如果菜单项（如**Windows 注册**）未处于活动状态，请查看 UI 中最右侧的边栏选项卡。  可能需要在出现的质询窗口中提供 Intune 配置特权。

2. 在最右侧窗格中的 "**添加 Windows Autopilot 设备**" 下，浏览到你之前复制到本地计算机的**AutopilotHWID.csv**文件。  该文件应包含 VM (或设备) 的序列号和 4K HH。  如果 Windows 产品 ID)  (的其他字段保留为空，则没关系。

    ![HWID CSV](images/hwid-csv.png)

    如上所示，在上传文件之前，应收到文件格式正确的确认。

3. 单击 "**导入**" 并等待导入过程完成。 此过程最长需要 15 分钟。

4. 单击 "**同步**" 以同步刚注册的设备。 请等待几分钟，然后刷新，以验证 VM 或设备是否已添加。 请参阅以下示例。

   ![导入 HWID](images/import-vm.png)

### <a name="autopilot-registration-using-msfb"></a>使用 MSfB 的 Autopilot 注册

> [!IMPORTANT]
> 如果已使用 Intune (或设备) 注册了 VM，请跳过此步骤。

可选：有关过程的概述，请参阅以下视频。

&nbsp;

> [!video https://www.youtube.com/embed/IpLIZU_j7Z0]

首先，需要一个 MSfB 帐户。  您可以使用您在上面为 Intune 创建的同一个，或者按照[以下说明](https://docs.microsoft.com/microsoft-store/windows-store-for-business-overview)创建一个新的。

接下来，通过单击主页右上角的 "**登录**"，登录到[Microsoft Store for Business](https://businessstore.microsoft.com/en-us/store) 。

从顶部菜单中选择 "**管理**"，然后单击 "**设备**" 卡下的 " **Windows Autopilot 部署程序**" 链接。 请参阅以下示例：

![适用于企业的 Microsoft Store](images/msfb.png)

单击 "**添加设备**" 链接上传 CSV 文件。 系统将显示一条消息，指示你的请求正在处理中。 请稍等片刻，然后再刷新，以查看新设备是否已添加。

![设备](images/msfb-device.png)

## <a name="create-and-assign-a-windows-autopilot-deployment-profile"></a>创建和分配 Windows Autopilot 部署配置文件

> [!IMPORTANT]
> 可以通过 Intune 或 MSfB 创建 Autopilot 配置文件并将其分配到已注册的 VM 或设备。  此处显示了这两个进程，但只是<U>为了此实验室选取一个</U>进程：

选择一个：
- [使用 Intune 创建配置文件](#create-a-windows-autopilot-deployment-profile-using-intune)
- [使用 MSfB 创建配置文件](#create-a-windows-autopilot-deployment-profile-using-msfb)

### <a name="create-a-windows-autopilot-deployment-profile-using-intune"></a>使用 Intune 创建 Windows Autopilot 部署配置文件

> [!NOTE]
> 即使你已在 MSfB 中注册设备，它仍会出现在 Intune 中，但你可能需要先**同步**然后**刷新**设备列表：

![设备](images/intune-devices.png)

> 上面的示例列出了物理设备和 VM。 列表中只应包含其中一项。

若要创建 windows Autopilot 配置文件，请选择 "**设备注册**" "  >  **Windows 注册**  >  **部署配置文件**"

![部署配置文件](images/deployment-profiles.png)

单击 "**创建配置文件**"。

![创建部署配置文件](images/create-profile.png)

在 "**创建配置文件**" 边栏选项卡中，使用以下值：

| 设置 | 值 |
|---|---|
| 名称 | Autopilot 实验室配置文件 |
| 说明 | blank |
| 将所有目标设备转换为 Autopilot | 否 |
| 部署模式 | 用户驱动 |
| 作为 Azure AD 联接 | 已加入 Azure AD |

单击 " ** (OOBE) 的全新体验**，并配置以下设置：

| 设置 | 值 |
|---|---|
| EULA | 隐藏 |
| 隐私设置 | 隐藏 |
| 隐藏更改帐户选项 | 隐藏 |
| 用户帐户类型 | Standard |
| 应用设备名称模板 | 否 |

请参阅以下示例：

![部署配置文件](images/profile.png)

单击 **"确定"** ，然后单击 "**创建**"。

> 如果要通过 Intune 将应用添加到配置文件，可在[附录 B：向配置文件添加应用](#appendix-b-adding-apps-to-your-profile)中找到用于执行此操作的可选步骤。

#### <a name="assign-the-profile"></a>分配配置文件

仅可将配置文件分配到组，因此，首先必须创建一个组，其中包含配置文件应应用到的设备。 本指南将提供有关分配配置文件的简单说明，有关详细说明，请参阅[创建 Autopilot 设备组](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-device-group)和[将 Autopilot 部署配置文件分配到设备组](https://docs.microsoft.com/intune/enrollment-autopilot#assign-an-autopilot-deployment-profile-to-a-device-group)（作为可选读取）。

若要创建组，请打开 Azure 门户，然后选择 " **Azure Active Directory**  >  **组**" "  >  **所有组**"：

![所有组](images/all-groups.png)

从 "组" 边栏选项卡中选择 "新建组" 以打开 "新组" UI。  选择 "安全" 组类型，为组命名，并选择 "分配" 成员资格类型：

单击 "**创建**" 之前，展开 "**成员**" 面板，单击设备序列号， (该设备将出现在 "**所选成员**" 下) 然后单击 "**选择**" 将该设备添加到此组。

![新建组](images/new-group.png)

现在，单击 "**创建**" 以完成创建新组的操作。

单击 "**所有组**"，然后单击 "**刷新**"，验证是否已成功创建新组。

如果已创建包含设备的组，现在可以返回并将配置文件分配给该组。 向后导航到 Azure 门户中的 Intune 页面 (一种方法是在顶部横幅搜索栏中键入**intune** ，并从结果) 选择 " **intune** "。

从 Intune，选择 "**设备注册**" "  >  **Windows 注册**  >  **部署配置文件**" 以打开 "配置文件" 边栏选项卡。  单击之前创建的配置文件的名称， (Autopilot Lab profile) 打开该配置文件的 "详细信息" 边栏选项卡：

![实验室配置文件](images/deployment-profiles2.png)

在 "**管理**" 下，单击 "**分配**"，然后选中 "**包括**" 选项卡，展开 "**选择组**" 边栏选项卡，然后单击 " **AP 实验室组 1** (组将出现在"**所选成员**") 下。

![包括组](images/include-group.png)

单击“选择”，并单击“保存”。********

![包括组](images/include-group2.png)

还可以将特定用户分配到配置文件，但我们不会在实验室中介绍这种情况。 有关更多详细信息，请参阅[使用 Windows Autopilot 在 Intune 中注册 Windows 设备](https://docs.microsoft.com/intune/enrollment-autopilot)。

### <a name="create-a-windows-autopilot-deployment-profile-using-msfb"></a>使用 MSfB 创建 Windows Autopilot 部署配置文件

如果已使用上述步骤通过 Intune 创建并分配了配置文件，则跳过此部分。

提供了一种[视频](https://www.youtube.com/watch?v=IpLIZU_j7Z0)，其中包含在 MSfB 中创建和分配配置文件所需的步骤。 下面也总结了这些步骤。

首先，使用最初为此实验室创建的 Intune 帐户登录到[Microsoft Store](https://businessstore.microsoft.com/manage/dashboard) 。

单击顶部菜单中的 "**管理**"，然后单击左侧导航树中的 "**设备**"。

![MSfB 管理](images/msfb-manage.png)

单击 "**设备**" 磁贴中的 " **Windows Autopilot 部署程序**" 链接。

创建配置文件：

从 "**设备**" 列表中选择你的设备：

![MSfB 创建](images/msfb-create1.png)

在 "Autopilot 部署" 下拉菜单上，选择 "**创建新配置文件**"：

![MSfB 创建](images/msfb-create2.png)

为配置文件命名，选择所需的设置，然后单击 "**创建**"：

![MSfB 创建](images/msfb-create3.png)

新配置文件将添加到 Autopilot 部署列表中。

要分配配置文件：

若要将配置文件 (或重新分配) 到设备，请选中为此实验室注册的设备旁边的复选框，然后从**Autopilot 部署**下拉菜单中选择要分配的配置文件，如下所示：

![MSfB 分配](images/msfb-assign1.png)

通过检查**配置文件**列的内容确认已成功将配置文件分配给目标设备：

![MSfB 分配](images/msfb-assign2.png)

> [!IMPORTANT]
> 新配置文件将仅在设备尚未启动并通过 OOBE 的情况下应用。 应用另一个配置文件时，不能应用不同配置文件的设置。 要在设备上重新安装 Windows，才能将第二个配置文件应用于设备。

## <a name="see-windows-autopilot-in-action"></a>查看 Windows Autopilot 的操作

如果在上一次重置后关闭了 VM，则可以重新启动它，以便它可以通过 Autopilot OOBE 体验，但不要再次尝试启动设备，直到 Intune 中设备的**配置文件状态**从 "**未分配**"**改为 "** 最终**分配**" 为止：

![服务状态](images/device-status.png)

此外，请确保等待至少30分钟后再[配置公司品牌](#configure-company-branding)的时间，否则这些更改可能不会显示。

> [!TIP]
> 如果你之前在收集 4K HH 信息之后重置设备，然后让它重新启动到第一个 OOBE 屏幕，则你可能需要再次重新启动设备以确保设备被识别为 Autopilot 设备，并显示你预期的 Autopilot OOBE 体验。  如果看不到 Autopilot OOBE 体验，则再次重置设备 (设置 > 更新 & 安全 > 恢复并单击 "入门"。  在 "重置此电脑" 下，选择 "删除所有内容"，只需删除文件。 单击 "重置") 。

- 确保你的设备具有 internet 连接。
- 打开设备
- 验证是否显示了相应的公司品牌 (相应的 OOBE 屏幕) 。  应会看到 "区域选择" 屏幕、键盘选择屏幕和第二个键盘选择屏幕 (可以跳过) 。

![OOBE 登录页面](images/autopilot-oobe.jpg)

到达桌面后，设备应在 Intune 中显示为**已启用**的 Autopilot 设备。  进入 Intune Azure 门户，选择 "设备" " **> 所有设备**"，然后**刷新**数据，验证设备是否已从 "已禁用" 更改为 "已启用"，以及设备的名称是否已更新。

![设备已启用](images/enabled-device.png)

在选择语言和键盘布局后，应该会显示公司品牌化的登录屏幕。 提供你的 Azure Active Directory 凭据，大功告成。

Windows Autopilot 将转到自动将设备加入 Azure Active Directory，并将其注册到 Microsoft Intune 中。 使用已创建的检查点以不同的设置再次执行此过程。

## <a name="remove-devices-from-autopilot"></a>从 Autopilot 删除设备

若要在此实验室完成后将设备 (或 VM) 用于其他目的，你将需要通过 Intune 或 MSfB 从 Autopilot 中删除 (取消注册) ，然后重置它。  有关注销设备的说明，请[参阅此处和下面](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-device-group)[的。](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)

### <a name="delete-deregister-autopilot-device"></a>删除 (取消注册) Autopilot 设备

在从 Autopilot 注销设备之前，你需要从 Intune 中删除 (或停用，或者) 设备进行恢复出厂设置。 若要从 Intune 中删除设备 (不 Azure Active Directory) ，请登录 Intune Azure 门户，然后导航到 " **intune > 设备" "所有设备**"。  选择要删除的设备旁边的复选框，并单击顶部菜单中的 "删除" 按钮。

![删除设备](images/delete-device1.png)

完成此操作时，请单击 " **X** "。

![删除设备](images/delete-device2.png)

这将从 Intune 管理中删除设备，并将从**intune > 设备 > 所有设备**中消失。 但这并不是从 Autopilot 取消注册设备，因此设备仍应显示在**Intune > 设备注册 > Windows 注册 > Windows Autopilot 部署计划 > 设备**。

![删除设备](images/delete-device3.png)

**Intune > 设备 > 所有设备**列表和**Intune > 设备注册 > Windows 注册 > Windows Autopilot 部署计划 > 设备**列表意味着不同的东西，并且是两个完全不同的数据存储。  先前 ("所有设备") 是当前注册到 Intune 中的设备的列表。

> [!NOTE]
> 设备启动后，它才会显示在 "所有设备" 列表中。  后者 (Windows Autopilot Deployment Program > 设备) 是当前从该 Intune 帐户注册到 Autopilot 程序的设备列表，这些设备可能会也可能不会注册到 Intune。

若要从 Autopilot 程序中删除该设备，请选择该设备，然后单击 "删除"。

![删除设备](images/delete-device4.png)

此时会出现一条警告消息，提醒您首先从 Intune 中删除该设备。

![删除设备](images/delete-device5.png)

此时，你的设备已从 Intune 取消注册，并还从 Autopilot 取消注册。  几分钟后，单击 "**同步**" 按钮，然后单击 "**刷新**" 按钮，确认设备不再列在 Autopilot 程序中：

![删除设备](images/delete-device6.png)

设备不再显示后，可随时将其用于其他目的。

如果还 (（可选）) 要从 AAD 中删除设备，请导航到 " **Azure Active Directory" > > 设备 "" 所有设备**"，选择设备，然后单击" 删除 "按钮：

![删除设备](images/delete-device7.png)

## <a name="appendix-a-verify-support-for-hyper-v"></a>附录 A：验证对 Hyper-v 的支持

从 Windows 8 开始，主计算机的微处理器必须支持二级地址转换 (SLAT) 才可安装 Hyper-V。 有关详细信息，请参阅 [Hyper-V：支持 SLAT 的 CPU 的主机列表](https://social.technet.microsoft.com/wiki/contents/articles/1401.hyper-v-list-of-slat-capable-cpus-for-hosts.aspx)。

若要验证你的计算机是否支持 SLAT，请打开管理员命令提示符，键入**systeminfo.exe**，按 enter，向下滚动，并查看输出底部显示的 "hyper-v 要求" 旁边的部分。 请参阅以下示例：

<pre style="overflow-y: visible">
C:>systeminfo

...
Hyper-V Requirements:      VM Monitor Mode Extensions: Yes
                           Virtualization Enabled In Firmware: Yes
                           Second Level Address Translation: Yes
                           Data Execution Prevention Available: Yes
</pre>

在本示例中，计算机支持 SLAT 和 Hyper-V。

> 如果一个或多个要求的评估结果为**否**，则计算机不支持安装 Hyper-V。  但是，仅当虚拟化设置不兼容时，你才能够在 BIOS 中启用虚拟化并将**已在固件中启用虚拟化**设置从**否**更改为**是**。 此设置的位置取决于制造商和 BIOS 版本，但通常与 BIOS 安全设置关联在一起。

你还可以使用处理器制造商提供的[工具](https://blogs.msdn.microsoft.com/taylorb/2008/06/19/hyper-v-will-my-computer-run-hyper-v-detecting-intel-vt-and-amd-v/)、 [msinfo32](https://technet.microsoft.com/library/cc731397.aspx)版工具来确定 hyper-v 支持，也可以下载[Coreinfo](https://technet.microsoft.com/sysinternals/cc835722)实用工具并运行它，如以下示例中所示：

<pre style="overflow-y: visible">
C:>coreinfo -v

Coreinfo v3.31 - Dump information on system CPU and memory topology
Copyright (C) 2008-2014 Mark Russinovich
Sysinternals - www.sysinternals.com

Intel(R) Core(TM) i7-2600 CPU @ 3.40GHz
Intel64 Family 6 Model 42 Stepping 7, GenuineIntel
Microcode signature: 0000001B
HYPERVISOR      -       Hypervisor is present
VMX             *       Supports Intel hardware-assisted virtualization
EPT             *       Supports Intel extended page tables (SLAT)
</pre>

> [!NOTE]
> 运行 Hyper-v 需要64位操作系统。

## <a name="appendix-b-adding-apps-to-your-profile"></a>附录 B：将应用添加到配置文件

### <a name="add-a-win32-app"></a>添加 Win32 应用

#### <a name="prepare-the-app-for-intune"></a>准备 Intune 应用

在将应用程序提取到 Intune 以使其成为我们的 AP 配置文件的一部分之前，需要使用[IntuneWinAppUtil.exe 命令行工具](https://github.com/Microsoft/Microsoft-Win32-Content-Prep-Tool)对应用程序进行 "打包"。  下载此工具后，收集以下三位信息以使用该工具：

1. 应用程序的源文件夹
2. 安装程序可执行文件的名称
3. 新文件的输出文件夹

出于本实验室的目的，我们将使用记事本 + + 工具作为 Win32 应用程序。

[在此处](https://www.hass.de/content/notepad-msi-package-enterprise-deployment-available)下载记事本 + + msi 包，然后将该文件复制到一个已知位置，如 C:\Notepad + + msi。

运行 IntuneWinAppUtil 工具，提供以下三个问题的答案，例如：

![添加应用](images/app01.png)

工具运行完毕后，输出文件夹中应包含一个 intunewin 文件，你现在可以使用以下步骤将其上传到 Intune。

#### <a name="create-app-in-intune"></a>在 Intune 中创建应用

登录到 Azure 门户并选择**Intune**。

导航到**Intune > 客户端应用 "> 应用**，然后单击"**添加**"按钮以创建新的应用程序包。

![添加应用](images/app02.png)

在 "**应用类型**" 下，选择 " **Windows 应用 (Win32) **：

![添加应用](images/app03.png)

在 "**应用包文件**" 边栏选项卡上，浏览到输出文件夹中的**npp**文件，将其打开，然后单击 **"确定"**：

![添加应用](images/app04.png)

在 "**应用信息配置**" 边栏选项卡上，提供友好名称、说明和发布者，如：

![添加应用](images/app05.png)

在 "**程序配置**" 边栏选项卡上，提供安装和卸载命令：

安装： msiexec/i "npp.7.6.3.installer.x64.msi"/q Uninstall： msiexec/x "{F188A506-C3C6-4411-BE3A-DA5BF1EA6737}"/q

> [!NOTE]
> 很可能是因为[IntuneWinAppUtil.exe 命令行工具](https://github.com/Microsoft/Microsoft-Win32-Content-Prep-Tool)在将 .msi 文件转换为 intunewin 文件时自动生成命令行工具，因此不必自行编写 install 和 uninstall 命令。

![添加应用](images/app06.png)

只需使用类似于 "记事本 + + .exe/S" 的安装命令，就不会实际安装记事本 + +;它将仅启动该应用程序。  若要实际安装该程序，我们需要改用 .msi 文件。  记事本 + + 实际上不具有其程序的 .msi 版本，但我们从[第三方提供商](https://www.hass.de/content/notepad-msi-package-enterprise-deployment-available)那里获取了 .msi 版本。

单击 **"确定"** 以保存输入并激活 "**要求**" 边栏选项卡。

在 "**要求配置**" 边栏选项卡上，指定**操作系统体系结构**和**最低操作系统版本**：

![添加应用](images/app07.png)

接下来，配置**检测规则**。  对于我们的目的，我们将选择 "手动" 格式：

![添加应用](images/app08.png)

单击 "**添加**" 以定义规则属性。  对于 "**规则类型**"，请选择 " **msi**"，它会自动将正确的 MSI 产品代码导入到规则中：

![添加应用](images/app09.png)

单击 **"确定"** 两次以保存，因为你需要再次返回到主 "**添加应用**" 边栏选项卡进行最终配置。

**返回代码**：出于我们的目的，请将返回代码保留默认值：

![添加应用](images/app10.png)

单击 **"确定"** 退出。

你可以跳过配置最终**范围 (标记) **边栏选项卡。

单击 "**添加**" 按钮完成并保存您的应用程序包。

指示器消息显示已完成添加。

![添加应用](images/app11.png)

你将能够在应用程序列表中找到你的应用程序：

![添加应用](images/app12.png)

#### <a name="assign-the-app-to-your-intune-profile"></a>将应用分配到 Intune 配置文件

> [!NOTE]
> 如果你之前在[Intune 中创建了组，并且为其分配了一个配置文件](#assign-the-profile)，则以下步骤将起作用。  如果尚未执行此操作，请返回到实验室的主要部分并完成这些步骤，然后再返回此处。

在**Intune > 客户端应用 "> 应用**" 窗格中，选择已创建的应用包以显示其 "属性" 边栏选项卡。  然后单击菜单中的 "**分配**"：

![添加应用](images/app13.png)

选择“添加组”以打开与该应用相关的“添加组”窗格。

对于我们而言，请从 "**分配类型**" 下拉菜单中选择 "**必需**"：

> **可用于已注册的设备**，意味着用户从公司门户应用或公司门户网站安装应用。

选择 "**包含的组**"，并分配你之前创建的、将使用此应用的组：

![添加应用](images/app14.png)

![添加应用](images/app15.png)

在 "**选择组**" 窗格中，单击 "**选择**" 按钮。

在 "**分配组**" 窗格中，选择 **"确定"**。

在“添加组”窗格中，选择“确定”。

在应用的“分配”窗格中，选择“保存”。

![添加应用](images/app16.png)

此时已完成将 Win32 应用添加到 Intune 的步骤。

有关将应用添加到 Intune 的详细信息，请参阅[Intune 独立-Win32 应用管理](https://docs.microsoft.com/intune/apps-win32-app-management)。

### <a name="add-office-365"></a>添加 Office 365

#### <a name="create-app-in-intune"></a>在 Intune 中创建应用

登录到 Azure 门户并选择**Intune**。

导航到**Intune > 客户端应用 "> 应用**，然后单击"**添加**"按钮以创建新的应用程序包。

![添加应用](images/app17.png)

在 "**应用类型**" 下，选择 " **Office 365 Suite > Windows 10**：

![添加应用](images/app18.png)

在 "**配置应用套件**" 窗格下，选择要安装的 Office 应用。  对于此 labe，我们只选择了 Excel：

![添加应用](images/app19.png)

单击“确定”。

在 "**应用套件信息**" 窗格中，输入<i>唯一</i>的套件名称和适当的说明。

> 输入应用套件的名称，该名称将显示在公司门户中。 请确保使用的所有套件名称都是唯一的。 如果同一应用套件名称存在两次，则在公司门户中将仅向用户显示其中一个应用。

![添加应用](images/app20.png)

单击“确定”。

在 "**应用套件设置**" 窗格中，选择 "**每月**" 作为**更新通道** (任何选择都适用于此实验室) 。  同时，为 "**自动接受应用最终用户许可协议** **" 选择 "是"** ：

![添加应用](images/app21.png)

单击 **"确定"** ，然后单击 "**添加**"。

#### <a name="assign-the-app-to-your-intune-profile"></a>将应用分配到 Intune 配置文件

> [!NOTE]
> 如果你之前在[Intune 中创建了组，并且为其分配了一个配置文件](#assign-the-profile)，则以下步骤将起作用。  如果尚未执行此操作，请返回到实验室的主要部分并完成这些步骤，然后再返回此处。

在**Intune > 客户端应用 "> 应用**" 窗格中，选择已创建的 Office 包以显示其 "属性" 边栏选项卡。  然后单击菜单中的 "**分配**"：

![添加应用](images/app22.png)

选择“添加组”以打开与该应用相关的“添加组”窗格。

对于我们而言，请从 "**分配类型**" 下拉菜单中选择 "**必需**"：

> **可用于已注册的设备**，意味着用户从公司门户应用或公司门户网站安装应用。

选择 "**包含的组**"，并分配你之前创建的、将使用此应用的组：

![添加应用](images/app23.png)

![添加应用](images/app24.png)

在 "**选择组**" 窗格中，单击 "**选择**" 按钮。

在 "**分配组**" 窗格中，选择 **"确定"**。

在“添加组”窗格中，选择“确定”。

在应用的“分配”窗格中，选择“保存”。

![添加应用](images/app25.png)

此时，你已完成将 Office 添加到 Intune 的步骤。

有关将 Office 应用添加到 Intune 的详细信息，请参阅[将 office 365 应用分配到带有 Microsoft Intune 的 Windows 10 设备](https://docs.microsoft.com/intune/apps-add-office365)。

如果已按照此实验室中的说明安装了 win32 应用 (记事本 + +) 和 Office (只是 Excel) ，则 VM 会将其显示在 "应用程序" 列表中，但可能需要花费几分钟的时间来填充：

![添加应用](images/app26.png)

## <a name="glossary"></a>术语表

<table border="1">
<tr><td>OEM</td><td>原始设备制造商</td></tr>
<tr><td>CSV</td><td>逗号分隔值</td></tr>
<tr><td>MPC</td><td>Microsoft 合作伙伴中心</td></tr>
<tr><td>CSP</td><td>云解决方案提供商</td></tr>
<tr><td>MSfB</td><td>适用于企业的 Microsoft Store</td></tr>
<tr><td>AAD</td><td>Azure Active Directory</td></tr>
<tr><td>4K HH</td><td>4K 硬件哈希</td></tr>
<tr><td>高于</td><td>计算机生成报表</td></tr>
<tr><td>EC</td><td>Enterprise Commerce (server) </td></tr>
<tr><td>DDS</td><td>设备目录服务</td></tr>
<tr><td>OOBE</td><td>全新体验</td></tr>
<tr><td>VM</td><td>虚拟机</td></tr>
</table>
