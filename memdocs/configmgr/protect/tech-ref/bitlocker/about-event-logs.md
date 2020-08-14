---
title: BitLocker 事件日志
titleSuffix: Configuration Manager
description: 了解如何使用 Windows 事件日志中的 BitLocker 信息来排查问题
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: troubleshooting
ms.assetid: a9ece9e8-37ec-441d-937c-be4941afce7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ef1d5f9a7e8f3c009d1993b82ddef22ce22e235d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127995"
---
# <a name="bitlocker-event-logs"></a>BitLocker 事件日志

适用范围：  Configuration Manager (Current Branch)

BitLocker 管理代理和 Web 服务使用 Windows 事件日志来记录消息。 在事件查看器中，依次转到“应用程序和服务日志”  、“Microsoft”  和“Windows”  。 日志通道（节点）因计算机和组件而异：

- MBAM  ：客户端计算机上的 BitLocker 管理代理
- MBAM-Web  ：
  - 管理点上的恢复服务
  - 自助服务门户
  - 管理和监视网站

若要详细了解这些日志中的特定消息，请参阅以下文章：

- [客户端事件日志](client-event-logs.md)
- [服务器事件日志](server-event-logs.md)

默认情况下，每个节点中显示两个日志通道：“管理”  和“操作”  。 如需了解更多故障排除详情，还可以选择[“显示分析和调试日志”](#bkmk_debug)。

## <a name="log-properties"></a>日志属性

在 Windows 事件查看器中，选择特定日志。 例如，“管理”  。转到“操作”  菜单，然后选择“属性”  。 配置下列设置：

- 日志大小上限 (KB)  ：默认情况下，此设置对所有日志都设为 `1028` (1 MB)。
- 达到事件日志最大大小时  ：默认情况下，“管理”  和“操作”  日志都将此设置设为“按需要覆盖事件(旧事件优先)”  。

## <a name="analytic-and-debug-logs"></a><a name="bkmk_debug"></a>分析和调试日志

可以启用更详细的日志来进行故障排除。 在事件查看器中，转到“查看”  菜单，然后选择“显示分析和调试日志”  。 现在，当你浏览到日志通道时，将会看到两个额外的日志：“分析”  和“调试”  。

> [!TIP]
> 这两个日志默认具有以下属性：
>
> - 日志大小上限 (KB)  ：`1028` (1 MB)
> - **不覆盖事件（手动清除日志）**

## <a name="export-logs-to-text"></a>将日志导出为文本

你可能会发现在一个文本文件中审阅日志条目更容易，尤其是在使用[分析和调试日志](#bkmk_debug)时。 若要将事件日志条目导出为文本文件，请运行以下 PowerShell 命令：

``` PowerShell
# Out-String with a larger -Width does a better job compared to using Out-File with -Width. -Oldest is only required with debug/analytic logs.

# Debug log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Debug -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Debug.txt

# Analytic log
Get-WinEvent -LogName Microsoft-Windows-MBAM/Analytic -Oldest | Format-Table -AutoSize | Out-String -Width 4096 | Out-File C:\Temp\MBAM_Log_Analytic.txt

# Admin log
# The above command truncates the output from the admin log, this sample reformats the strings
Get-WinEvent -LogName Microsoft-Windows-MBAM/Admin |
    Select TimeCreated, LevelDisplayName, TaskDisplayName, @{n='Message';e={$_.Message.trim()}} |
    Format-Table -AutoSize -Wrap | Out-String -Width 4096 |
    Out-File -FilePath C:\Temp\MBAM_Log_Admin.txt
```
