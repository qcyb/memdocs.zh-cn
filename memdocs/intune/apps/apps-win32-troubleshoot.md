---
title: Microsoft Intune 中的 Win32 应用疑难解答
titleSuffix: ''
description: 了解在 Microsoft Intune 中排查 Win32 应用问题的最常见方法。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: efdc196b-38f3-4678-ae16-cdec4303f8d2
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: bbdc929f5d3a9703f3d299b8e3a68dd624c450c2
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083907"
---
# <a name="troubleshoot-win32-app-issues"></a>Win32 应用问题的疑难解答

排查在 Microsoft Intune 中使用的 Win32 应用的问题时，可以使用多种方法。 本文详细介绍如何排查问题，并提供有助于解决 Win32 应用问题的信息。 有关详细信息，请参阅 [Win32 应用安装疑难解答](troubleshoot-app-install.md#win32-app-installation-troubleshooting)资源。

> [!NOTE]
> 此应用管理功能支持适用于 Windows 应用程序的 32 位和 64 位操作系统体系结构。

> [!IMPORTANT]
> 部署 Win32 应用时，建议专门使用 [Intune 管理扩展](../apps/intune-management-extension.md)方法，特别是在有多文件 Win32 应用安装程序时。 如果在 AutoPilot 注册期间混合安装 Win32 应用和业务线 (LOB) 应用，则应用安装可能会失败。 如果 PowerShell 脚本或 Win32 应用分配给用户或设备，Intune 管理扩展就会自动安装。

## <a name="app-troubleshooting-details"></a>应用疑难解答详细信息

可查看安装问题，如应用的创建时间、修改时间、定目标时间以及传递给设备的时间。 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)在“疑难解答 + 支持”窗格中提供了这些详细信息和其他详细信息。 有关详细信息，请参阅[应用疑难解答详细信息](troubleshoot-app-install.md#app-troubleshooting-details)。

## <a name="troubleshooting-app-issues-by-using-logs"></a>使用日志排查应用问题

查看日志的详细信息有助于确定所遇到的问题的原因，并帮助解决问题。 可以选择查看 [Intune 中显示的日志](apps-win32-troubleshoot.md#logs-displayed-in-intune)，或查看[通过 CMTrace 显示的日志](apps-win32-troubleshoot.md#logs-displayed-through-cmtrace)。 

### <a name="logs-displayed-in-intune"></a>Intune 中显示的日志

当 Win32 应用出现安装问题时，可以在 Intune 中的应用“安装详细信息”窗格中选择“收集日志”选项。 有关更多详细信息，请参阅 [Win32 应用安装疑难解答](troubleshoot-app-install.md#win32-app-installation-troubleshooting)。

### <a name="logs-displayed-through-cmtrace"></a>通过 CMTrace 显示的日志

客户端计算机上的代理日志通常位于 C:\ProgramData\Microsoft\IntuneManagementExtension\Logs 中。 可以使用 *CMTrace.exe* 查看这些日志文件。 有关详细信息，请参阅 [CMTrace](https://docs.microsoft.com/configmgr/core/support/cmtrace)。

![客户端计算机上代理日志的屏幕截图。](./media/apps-win32-app-management/apps-win32-app-10.png)

> [!IMPORTANT]
> 为了能够正确安装和执行 LOB Win32 应用，反恶意软件设置应不扫描以下目录：<p>
> 在 x64 客户端计算机上：<br>
> C:\Program Files (x86)\Microsoft Intune Management Extension\Content<br>
> C:\windows\IMECache
>  
> 在 x86 客户端计算机上：<br>
> C:\Program Files\Microsoft Intune Management Extension\Content<br>
> C:\windows\IMECache
>
> 有关详细信息，请参阅[针对运行当前受支持 Windows 版本的企业计算机的病毒扫描建议](https://support.microsoft.com/help/822158/virus-scanning-recommendations-for-enterprise-computers)。

## <a name="detecting-the-win32-app-file-version-by-using-powershell"></a>使用 PowerShell 检测 Win32 应用文件版本

如果难以检测到 Win32 应用文件版本，请考虑使用或修改以下 PowerShell 命令：

``` PowerShell

$FileVersion = [System.Diagnostics.FileVersionInfo]::GetVersionInfo("<path to binary file>").FileVersion
#The below line trims the spaces before and after the version name
$FileVersion = $FileVersion.Trim();
if ("<file version of successfully detected file>" -eq $FileVersion)
{
#Write the version to STDOUT by default
$FileVersion
exit 0
}
else
{
#Exit with non-zero failure code
exit 1
}
```

在上面的 PowerShell 命令中，使用 Win32 应用文件的路径替换 `<path to binary file>` 字符串。 示例路径类似于以下内容：

`C:\Program Files (x86)\Microsoft SQL Server Management Studio 18\Common7\IDE\ssms.exe`

另外，使用需要检测的文件版本替换 `<file version of successfully detected file>` 字符串。 示例文件版本字符串类似于以下内容：

`2019.0150.18118.00 ((SSMS_Rel).190420-0019)`

如果需要获取 Win32 应用的版本信息，可使用以下 PowerShell 命令：

``` PowerShell

[System.Diagnostics.FileVersionInfo]::GetVersionInfo("<path to binary file>").FileVersion

```

在上面的 PowerShell 命令中，使用文件路径替换 `<path to binary file>`。

## <a name="additional-troubleshooting-areas-to-consider"></a>需要考虑的其他故障排除方面
- 检查目标以确保设备上已安装代理。 如果某个 Win32 应用针对某个组，或者某个 PowerShell 脚本针对某个组，则会为安全组创建代理安装策略。
- 检查 OS 版本：Windows 10 1607 及更高版本。  
- 检查 Windows 10 SKU。 Windows 10 S 或以 S 模式运行的 Windows 版本不支持 MSI 安装。

有关对 Win32 应用进行故障排除的更多信息，请参阅 [Win32 应用安装故障排除](troubleshoot-app-install.md#win32-app-installation-troubleshooting)。 有关 ARM64 设备上的应用类型的信息，请参阅 [ARM64 设备支持的应用类型](../apps/troubleshoot-app-install.md#app-types-supported-on-arm64-devices)。

## <a name="next-steps"></a>后续步骤

- [排查应用安装问题](troubleshoot-app-install.md)
