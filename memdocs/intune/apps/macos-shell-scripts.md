---
title: 在 Microsoft Intune 中的 macOS 设备上使用 Shell 脚本 | Microsoft Docs
description: 为 Microsoft Intune 中的 macOS 设备创建、分配、监视和排查 Shell 脚本。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/30/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c5839154ab0c884e933e8d11055e745d54503433
ms.sourcegitcommit: 8a8378b685a674083bfb9fbc9c0662fb0c7dda97
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82619536"
---
# <a name="use-shell-scripts-on-macos-devices-in-intune-public-preview"></a>在 Intune 中的 macOS 设备上使用 Shell 脚本（公共预览版）

> [!NOTE]
> macOS 设备的 Shell 脚本当前处于预览状态。 使用此功能之前，请查看[预览版中的已知问题](macos-shell-scripts.md#known-issues)列表。

使用 Shell 脚本将 Intune 上的设备管理功能扩展到 macOS 操作系统支持的功能之外。 

## <a name="prerequisites"></a>必备条件
确保在编写 Shell 脚本并将其分配给 macOS 设备时满足以下先决条件。 
 - 设备正在运行 macOS 10.12 或更高版本。
 - 设备由 Intune 管理。 
 - Shell 脚本从 `#!` 开始，必须位于有效的位置，如 `#!/bin/sh` 或 `#!/usr/bin/env zsh`。
 - 安装了适用 Shell 的命令行解释器。

## <a name="important-considerations-before-using-shell-scripts"></a>使用 Shell 脚本之前的重要注意事项
 - Shell 脚本要求 Microsoft Intune 管理代理已成功安装在 macOS 设备上。 有关详细信息，请参阅[适用于 macOS 的 Microsoft Intune 管理代理](macos-shell-scripts.md#microsoft-intune-management-agent-for-macos)。
 - Shell 脚本作为单独的进程在设备上并行运行。
 - 作为登录用户运行的 Shell 脚本将在运行时为设备上的所有当前登录用户帐户运行。
 - 最终用户需要登录到设备才能执行以登录用户身份运行的脚本。
 - 如果脚本需要进行标准用户帐户无法更改的更改，则需要根用户权限。
 - 某些情况下，如磁盘已满、存储位置被篡改、本地缓存被删除或 Mac 设备重启，Shell 脚本将尝试频繁运行并且运行频率高于普通脚本。
 
## <a name="create-and-assign-a-shell-script-policy"></a>创建并分配 Shell 脚本策略
1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“设备” > “macOS” > 脚本” > “添加”     。
3. 在“基本信息”中，输入以下属性并选择“下一步”   ：
   - **名称**：输入 Shell 脚本的名称。
   - **描述**：输入 Shell 脚本的说明。 此设置是可选的，但建议进行。
4. 在“脚本设置”中，输入以下属性并选择“下一步”   ：
   - **上传脚本**：浏览 Shell 脚本。 脚本文件大小必须小于 200 KB。
   - **以登录用户的身份运行脚本**：选择“是”，可以使用设备上的用户凭据运行脚本  。 选择“否”（默认值），作为根用户运行该脚本  。 
   - 在设备上隐藏脚本通知：  默认情况下，脚本通知对运行的每个脚本都会显示。 最终用户会在 macOS 设备上看到 Intune 发送的通知“IT 人员正在配置你的计算机”  。
   - 脚本运行频率：  选择脚本运行频率。 选择“未配置”  （默认）表示只运行一次脚本。
   - 脚本失败后重试的最大次数：  选择在脚本返回非零退出代码（零表示成功）后应运行多少次脚本。 选择“未配置”  （默认）表示在脚本失败时不重试。
5. 在“作用域标签”中，可以为脚本添加作用域标签，然后选择“下一个”   。 可以使用作用域标记来确定可在 Intune 中查看脚本的人员。 若要详细了解作用域标记，请参阅[将基于角色的访问控制和作用域标记用于分布式 IT](../fundamentals/scope-tags.md)。
6. 选择“分配” >  选择要包含的组   。 随即显示 Azure AD 组的现有列表。 选择一个或多个设备组，其中的用户的 macOS 设备会接收该脚本。 选择“选择”  。 所选组将显示在列表中，并将收到脚本策略。
   > [!NOTE]
   > - Intune 中的 Shell 脚本只能分配给 Azure AD 设备安全组。 预览版中不支持用户组分配。 
   > - 如果更新 Shell 脚本的分配，则还会更新[适用于 macOS 的 Microsoft Intune 管理代理](macos-shell-scripts.md#microsoft-intune-management-agent-for-macos)的分配。
7. 在“查看 + 添加”中，将显示你配置的设置的摘要  。 选择“添加”以保存脚本  。 选择“添加”后，脚本策略将部署到所选组  。

创建的脚本现在将显示在脚本列表中。 

## <a name="monitor-a-shell-script-policy"></a>监视 Shell 脚本策略
可通过选择以下报告之一来监视用户和设备所有分配脚本的运行状态：
- “脚本” > “选择要监视的脚本” > “设备状态”   
- “脚本” > “选择要监视的脚本” > “用户状态”   

>[!IMPORTANT]
> 无论选择的“脚本频率”如何，脚本运行状态都仅在首次运行脚本时才会报告  。 脚本运行状态不会在后续运行时更新。 但是，更新的脚本将视为新脚本，并将再次报告运行状态。

脚本运行后，它将返回以下状态之一：
- 脚本运行状态为“失败”表示脚本返回了非零退出代码或脚本格式不正确  。 
- 脚本运行状态为“成功”表示脚本返回零作为退出代码  。 

## <a name="troubleshoot-macos-shell-script-policies-using-log-collection"></a>使用日志收集对 macOS Shell 脚本策略进行排除故障

你可收集设备日志来帮助排查 macOS 设备上的脚本问题。 

### <a name="requirements-for-log-collection"></a>日志收集的要求
要在 macOS 设备上收集日志，需满足以下要求：
- 必须指定完整的绝对日志文件路径。
- 文件路径必须仅使用分号 (;) 分隔。
- 上传的日志集合大小不超过 60 MB （压缩格式）或 25 个文件，以先达到者为准。
- 允许日志收集的文件类型包括以下扩展名：.log、.zip、.gz、.tar、.txt、.xml、.crash、.rtf 

#### <a name="collect-device-logs"></a>收集设备日志
1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 在“设备状态”或“用户状态”报表中，选择一台设备   。
3. 选择“收集日志”，提供仅由分号 (;) 分隔的日志文件的文件夹路径，路径之间不使用空格或换行符  。<br>例如，多个路径应编写为 `/Path/to/logfile1.zip;/Path/to/logfile2.log`。 

   >[!IMPORTANT]
   > 如果多个日志文件路径用逗号、句点、换行符或引号（无论是否有空格）分隔，则将导致日志收集错误。 路径之间也不允许使用空格作为分隔符。

4. 选择“确定”  。 在下次设备上的 Intune 管理代理向 Intune 签入时，会收集日志。 此签入通常每 8 小时执行一次。

   >[!NOTE]
   > 
   > - 收集的日志在设备上加密、进行传输并在 Microsoft Azure 存储空间存储 30 天。 存储的日志根据需要进行解密，并通过 Microsoft Endpoint Manager 管理中心下载。
   > - 除了管理员指定的日志之外，还会从 `/Library/Logs/Microsoft/Intune` 和 `~/Library/Logs/Microsoft/Intune` 文件夹收集 Intune 管理代理日志。 代理日志文件名为 `IntuneMDMDaemon date--time.log` 和 `IntuneMDMAgent date--time.log`。 
   > - 如果管理员指定的任何文件丢失或文件扩展名错误，你可在 `LogCollectionInfo.txt` 中找到这些文件名。     

### <a name="log-collection-errors"></a>日志收集错误
由于下表中列出以下任一原因，日志收集可能会失败。 要解决这些错误，请执行修正步骤。

| 错误代码（十六进制） | 错误代码（十进制） | 错误消息 | 修正步骤 |
|------------------|------------------|---------------|-------------------|
| 0X87D300D1 | 2016214834 | 日志文件大小不能超过 60 MB。 | 请确保压缩后的日志小于 60 MB。 |
| 0X87D300D1 | 2016214831 | 提供的日志文件路径必须存在。 系统用户文件夹对于日志文件来说无效。 | 请确保提供的文件路径有效且可访问。 |
| 0X87D300D2 | 2016214830 | 上传 URL 过期，因此日志收集文件上传失败。 | 重试“收集日志”操作  。 |
| 0X87D300D3、0X87D300D5、0X87D300D7 | 2016214829、2016214827、2016214825 | 加密失败，因此日志收集文件上传失败。 请重试日志上传。 | 重试“收集日志”操作  。 |
| | 2016214828 | 日志文件数超出允许的 25 个文件上限。 | 一次最多只能收集 25 个日志文件。 |
| 0X87D300D6 | 2016214826 | 由于 zip 错误，日志收集文件上传失败。 请重试日志上传。 | 重试“收集日志”操作  。 |
| | 2016214740 | 无法加密日志，因为找不到已压缩的日志。 | 重试“收集日志”操作  。 |
| | 2016214739 | 日志已收集，但无法存储。 | 重试“收集日志”操作  。 |

## <a name="frequently-asked-questions"></a>常见问题解答
### <a name="why-are-assigned-shell-scripts-not-running-on-the-device"></a>为什么分配的 Shell 脚本未在设备上运行？
可能有以下几个原因：
* 代理可能需要签入才能接收新的或更新的脚本。 此签入过程每 8 小时发生一次，且与 MDM 签入不同。 确保设备处于唤醒状态并连接到网络以成功签入代理，并等待代理签入。
* 代理可能未安装。 检查代理是否已安装在 macOS 设备上的 `/Library/Intune/Microsoft Intune Agent.app`。
* 代理可能未处于正常状态。 如果仍分配 Shell 脚本，代理将尝试恢复 24 小时，删除自身并重新安装。

### <a name="how-frequently-is-script-run-status-reported"></a>报告脚本运行状态的频率如何？
脚本运行状态在脚本运行完成后立即报告给 Microsoft Endpoint Manager 管理控制台。 如果脚本计划以设定的频率定期运行，则它仅在首次运行时报告状态。

### <a name="when-are-shell-scripts-run-again"></a>何时再次运行 Shell 脚本？
仅当“脚本失败时最大重试次数”设置已配置且脚本运行失败时，才会再次运行脚本  。 如果未配置“脚本失败时最大重试次数”，并且脚本在运行时失败，则它将不会再次运行，并且运行状态将报告为“失败”   。 

### <a name="what-intune-role-permissions-are-required-for-shell-scripts"></a>Shell 脚本需要哪些 Intune 角色权限？
分配的 Intune 角色需要“设备配置”权限才能删除、分配、创建、更新或读取 Shell 脚本  。

## <a name="microsoft-intune-management-agent-for-macos"></a>适用于 macOS 的 Microsoft Intune 管理代理
 ### <a name="why-is-the-agent-required"></a>为什么需要代理？
Microsoft Intune 管理代理必须安装在托管 macOS 设备上，以便启用本机 macOS 操作系统不支持的高级设备管理功能。
 
 ### <a name="how-is-the-agent-installed"></a>代理是如何安装的？
 代理会以无提示方式自动安装在 Intune 管理的 macOS 设备上，你需要在 Microsoft Endpoint Manager 管理中心为这些设备至少分配一个 Shell 脚本。 如果适用，代理会安装在 `/Library/Intune/Microsoft Intune Agent.app` 中，并且不会显示在 macOS 设备上的“查找器” > “应用程序”中   。 在 macOS 设备上运行时，代理会在“活动监视器”中显示为 `IntuneMdmAgent` 。

### <a name="what-does-the-agent-do"></a>代理有什么作用？
 - 代理在签入之前使用 Intune 服务静默进行身份验证，以接收 macOS 设备的已分配的 Shell 脚本。
 - 代理接收分配的 Shell 脚本，并根据配置的计划、重试尝试、通知设置以及管理员设置的其他设置运行脚本。
 - 代理通常每 8 小时使用 Intune 服务检查新的脚本或更新的脚本。 此签入过程与 MDM 签入无关。 
 
 ### <a name="how-can-i-manually-initiate-an-agent-check-in-from-a-mac"></a>我如何从 Mac 手动启动代理签入？
在已安装代理的托管 Mac 上，打开“终端”  ，运行 `sudo killall IntuneMdmAgent` 命令，以终止 `IntuneMdmAgent` 进程。 `IntuneMdmAgent` 进程会立即重启，这会通过 Intune 启动签入。

也可以执行以下操作：
1. 依次打开“活动监视器”   > “视图”   >  选择“所有进程” ** 。 
2. 搜索名为“`IntuneMdmAgent`”的进程。 
3. 退出为根  用户运行的进程。 

> [!NOTE]
> 公司门户中的“检查设置”  操作和 Microsoft Endpoint Manager 管理控制台中用于设备的“同步”  操作会启动 MDM 签入，但不会强制执行代理签入。

 ### <a name="when-is-the-agent-removed"></a>何时删除代理？
 有几个条件可能导致从设备中删除代理，例如：
 - 不再将 Shell 脚本分配给设备。 
 - 不再管理 macOS 设备。
 - 代理处于不可恢复状态超过 24 小时（设备唤醒时间）。

 ### <a name="how-to-turn-off-usage-data-sent-to-microsoft-for-shell-scripts"></a>如何为 Shell 脚本关闭发送给 Microsoft 的使用情况数据？
 若要关闭从 Intune 管理代理发送到 Microsoft 的使用情况数据，请打开公司门户并选择“菜单” > “首选项” > 取消选中“允许 Microsoft 收集使用情况数据”    。 这将关闭为该代理和公司门户发送的使用情况数据。

## <a name="known-issues"></a>已知问题
- **用户组分配：** 分配给用户组的 Shell 脚本不适用于设备。 预览版当前不支持用户组分配。 使用设备组分配分配脚本。
- **收集日志：** “收集日志”操作可见。 但尝试日志收集时，它会显示“发生错误”，并且不捕获日志。 预览版当前不支持日志收集。
- **无脚本运行状态：** 如果设备上收到脚本，并且设备在报告运行状态之前脱机，则设备将不会报告管理控制台中脚本的运行状态。
- **用户状态报告：** 存在空报表问题。 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“监视”  。 用户状态显示空报表。

## <a name="next-steps"></a>后续步骤

- [在 Microsoft Intune 中创建合规性策略](..\protect\create-compliance-policy.md)
