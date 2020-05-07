---
title: 对 Endpoint Protection 进行故障排除
titleSuffix: Configuration Manager
description: 了解如何对 Windows Defender 和 Endpoint Protection 进行故障排除。
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: efd31eaee987a7e28557cf0601608ca97c914999
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709415"
---
# <a name="troubleshoot-windows-defender-or-endpoint-protection-client"></a>对 Windows Defender 或 Endpoint Protection 客户端进行故障排除

适用范围：  Configuration Manager (Current Branch)

如果在使用 Windows Defender 或 Endpoint Protection 时遇到问题，请参考本文来排查以下问题：  

- [更新 Windows Defender 或 Endpoint Protection](#update-windows-defender-or-endpoint-protection)  
- [启动 Windows Defender 或 Endpoint Protection 服务](#starting-windows-defender-or-endpoint-protection-service)  
- [Internet 连接问题](#internet-connection-issues)  
- [无法解决检测到的威胁](#detected-threat-cant-be-remediated)  

## <a name="update-windows-defender-or-endpoint-protection"></a>更新 Windows Defender 或 Endpoint Protection

### <a name="symptoms"></a>症状

Windows Defender 或 Endpoint Protection 会自动与 Microsoft 更新一同运行，以便确保你保持最新的病毒和间谍软件定义。  

本部分介绍了有关自动更新的常见问题，包括以下情况：  

- 你看见表示更新失败的错误消息。  

- 当你检查更新时，你会收到一条错误消息，指出无法检查、下载或安装病毒和间谍软件定义更新。  

- 即使设备已连接到 Internet，更新也会失败。  

- 不按计划自动安装更新。  

### <a name="causes"></a>原因

更新问题的最常见原因是 Internet 连接的问题。 如果你知道设备已连接到 Internet，因为你可以浏览其他网站，那么该问题可能是由与 Windows 中的 Internet 设置冲突引起的。  

### <a name="options-to-resolve"></a>解决方法

#### <a name="step-1-reset-your-internet-settings"></a>步骤 1：重置 Internet 设置  

1. 退出所有打开的程序（包括 Web 浏览器）。  

    > [!NOTE]  
    > 重置这些 Internet 设置可能会删除浏览器临时文件、Cookie、浏览历史记录和联机密码。 但不会删除收藏夹。  

2. 转到“开始”  菜单，然后打开“`inetcpl.cpl`”。  

3. 切换到“高级”  选项卡。  

4. 在“重置 Internet Explorer 设置”  部分中，选择“重置”  ，然后再次选择“重置”  进行确认。  

5. 在设置重置后，选择“确定”  。

6. 尝试再次更新 Windows Defender。

如果此问题仍然存在，请继续执行下一步。  

#### <a name="step-2-make-sure-that-the-date-and-time-are-set-correctly-on-your-computer"></a>步骤 2:确保你的计算机上的日期和时间设置正确  

如果错误消息中包含代码 0x80072f8f，那么该问题很可能是由你的计算机上不正确的日期或时间设置引起的。 转到“开始”  菜单，然后依次选择“设置”  、“时间和语言”  和“日期和时间”  。

#### <a name="step-3-rename-the-software-distribution-folder-on-your-computer"></a>步骤 3：重命名你的计算机上的 Software Distribution 文件夹  

1. 停止“Windows 更新”  服务。  

    1. 转到“开始”  ，然后打开“services.msc”  。  

    2. 选择“Windows 更新”  服务。 转到“操作”  菜单，然后选择“停止”  。

2. 重命名 SoftwareDistribution  目录。  

    1. 以管理员身份打开命令提示符。  

    2. 输入以下命令：

        ```cmd
        cd %windir%
        ren SoftwareDistribution SDTemp
        exit
        ```

3. 重启“Windows 更新”  服务。

    1. 切换回“服务”  窗口。  

    2. 选择“Windows 更新”  服务。 转到“操作”  菜单，然后选择“启动”  。

    3. 关闭“服务”窗口。  

#### <a name="step-4-reset-the-microsoft-antivirus-update-engine-on-your-computer"></a>步骤 4：重置你的计算机上的 Microsoft 防病毒更新引擎  

1. 以管理员身份打开命令提示符。

2. 输入以下命令：

    ```cmd
    cd \

    cd program files\windows defender

    MpCmdRun -RemoveDefinitions -all

    exit
    ```

3. 重新启动计算机。  

4. 尝试再次更新 Windows Defender。

如果此问题仍然存在，请继续执行下一步。  

#### <a name="step-5-manually-install-the-definition-updates"></a>步骤 5：手动安装定义更新  

[手动下载最新更新](https://www.microsoft.com/en-us/wdsi/defenderupdates)。  

#### <a name="step-6-contact-microsoft-support"></a>步骤 6：联系 Microsoft 支持部门  

如果执行这些步骤仍未解决此问题，请联系 Microsoft 支持部门。 有关详细信息，请参阅[支持选项和社区资源](../../core/understand/find-help.md#BKMK_SupportOptions)。  

## <a name="starting-windows-defender-or-endpoint-protection-service"></a>启动 Windows Defender 或 Endpoint Protection 服务

### <a name="symptom"></a>症状

你收到一条消息，通知你“**Windows Defender 或 Endpoint Protection 未监视你的计算机，因为该程序的服务已停止。应该立即重新启动该程序。** ”

### <a name="solution"></a>解决方案

#### <a name="step-1-restart-your-computer"></a>步骤 1：重启计算机

关闭所有应用程序并重新启动计算机。  

#### <a name="step-2-check-the-windows-service"></a>步骤 2:检查 Windows 服务

1. 转到“开始”  ，然后打开“services.msc”  。  

2. 选择“Windows Defender 防病毒服务”  。  

3. 确保“启动类型”  设置为“自动”  。

4. 转到“操作”  菜单，然后选择“启动”  。

    1. 如果没有此操作，请选择“停止”  。 等待服务停止，然后选择“启动”  操作来重启服务。  

请注意此过程中可能出现的任何错误。 [请联系 Microsoft 支持部门](../../core/understand/find-help.md#BKMK_SupportOptions)，并提供错误信息。  

#### <a name="step-3-remove-any-third-party-security-programs"></a>步骤 3：删除任何第三方安全程序  

> [!NOTE]  
> 有些安全应用程序无法完全卸载。 可能需要下载并运行先前的安全应用程序的清理实用程序，才能将其完全删除。  

1. 转到“开始”  ，然后打开“appwiz.cpl”  。  

2. 在安装的程序列表中，卸载所有第三方安全程序。

3. 重新启动计算机。  

> [!CAUTION]  
> 删除安全程序后，你的计算机可能处于不受保护的状态。 如果在删除现有安全程序后无法安装 Windows Defender，请联系 [Microsoft 支持部门](https://support.microsoft.com/supportforbusiness/productselection)。 依次选择“安全性”  产品系列和“Windows Defender”  产品。

## <a name="internet-connection-issues"></a>Internet 连接问题

将要从 Windows 更新接收最新更新的计算机连接到 Internet。  

1. 转到“开始”  ，然后打开“ncpa.cpl”  。  

2. 打开连接名称，以查看连接“状态”  。  

3. 如果计算机已连接，则“IPv4 连接”  和/或“IPv6 连接”  状态为“Internet”  。  

4. 如果计算机似乎没有连接，请依次选择连接名称和“诊断这个连接”  。

关闭任何已打开的程序并重新启动计算机。  

## <a name="detected-threat-cant-be-remediated"></a>无法解决检测到的威胁

检测到潜在威胁时，Windows Defender 或 Endpoint Protection 会尝试通过隔离或删除威胁来缓解威胁。 这些威胁可能会隐藏在压缩的存档 (`.zip`)，也可能会隐藏在网络共享中。

### <a name="remove-or-scan-the-file"></a>删除或扫描文件  

- 如果检测到的威胁位于压缩的存档文件中，请浏览到文件。 删除或手动扫描文件。 右键单击文件，然后选择“使用 Windows Defender 扫描”  。 如果在文件中检测到其他威胁，Windows Defender 会通知你。 然后，你可以选择适当的操作。  

- 如果检测到的威胁位于网络共享中，请打开并手动扫描共享。 右键单击文件，然后选择“使用 Windows Defender 扫描”  。 如果在网络共享中检测到其他威胁，Windows Defender 会通知你。 然后，你可以选择适当的操作。  

- 如果你不确定文件的来源，请对计算机运行完全扫描。 完全扫描可能需要一段时间才能完成。  

## <a name="see-also"></a>另请参阅

[Endpoint Protection 客户端的常见问题](endpoint-protection-client-faq.md)

[Endpoint Protection 客户端帮助](endpoint-protection-client-help.md)
