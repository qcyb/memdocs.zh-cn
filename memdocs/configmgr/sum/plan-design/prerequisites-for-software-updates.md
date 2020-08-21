---
title: 软件更新的先决条件
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中软件更新的先决条件。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 08/22/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.openlocfilehash: 4604b6d2c0396b9192c031264cffef8b8641d557
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696675"
---
# <a name="prerequisites-for-software-updates-in-configuration-manager"></a>Configuration Manager 中的软件更新的先决条件

适用范围：  Configuration Manager (Current Branch)

本文列出了 Configuration Manager 中软件更新的先决条件。 对于这些先决条件中的每一个，在不同的表格中列出了外部依赖关系和内部依赖关系。  

## <a name="software-update-dependencies-that-are-external-to-configuration-manager"></a>Configuration Manager 外部的软件更新依赖关系  
 以下部分列出了软件更新的外部依赖关系。  

### <a name="internet-information-services"></a>Internet Information Services  
 Internet Information Services (IIS) 必须安装在站点系统服务器上才可运行软件更新点、管理点和分发点。 有关详细信息，请参阅[站点系统角色的先决条件](../../core/plan-design/configs/site-and-site-system-prerequisites.md)。  

### <a name="windows-server-update-services"></a>Windows Server 更新服务  
 软件更新同步和在客户端上进行的软件更新适用性扫描都需要使用 Windows Server Update Services (WSUS)。 在创建软件更新点角色之前，必须安装 WSUS 服务器。 软件更新点支持以下版本的 WSUS：  

- WSUS 10.0.14393（Windows Server 2016 中的角色）
- WSUS 10.0.17763（Windows Server 2019 中的角色）（需要使用 Configuration Manager 1810 或更高版本）
- WSUS 6.2 和 6.3（Windows Server 2012 和 Windows Server 2012 R2 中的角色）
  - 如果部署 Windows 10 升级，则 WSUS 6.2 及 6.3 需要 [KB 3095113 和 KB 3159706（或等效更新）](#BKMK_wsus2012)。

> [!NOTE]
> - 如果在一个站点上有多个软件更新点，请确保它们全都运行相同版本的 WSUS。

### <a name="wsus-administration-console"></a>WSUS 管理控制台  
当软件更新点位于远程站点系统服务器上，且该站点服务器并未安装 WSUS 时，Configuration Manager 站点服务器上需要安装 WSUS 管理控制台。  

> [!IMPORTANT]  
> - 站点服务器上的 WSUS 版本必须与在软件更新点上运行的 WSUS 版本相同。
> - 不要使用 WSUS 管理控制台配置 WSUS 设置。 Configuration Manager 连接到在软件更新点上运行的 WSUS 的实例，并配置适当的设置。  


### <a name="windows-update-agent"></a>Windows 更新代理  
 需要在客户端上安装 Windows 更新代理 (WUA) 客户端，这样客户端才能连接到 WSUS 服务器。 WUA 检索为实现符合性而必须扫描的软件更新列表。  

 安装 Configuration Manager 时，会下载 WUA 的最新版本。 之后，安装 Configuration Manager 客户端时，如有必要会升级 WUA。 如果安装失败，必须使用另一种方法升级 WUA。  

## <a name="software-update-dependencies-that-are-internal-to-configuration-manager"></a>Configuration Manager 内部的软件更新依赖关系  
 以下部分列出了 Configuration Manager 中软件更新的内部依赖关系。  

### <a name="management-points"></a>管理点  
 管理点在客户端计算机和 Configuration Manager 站点之间传输信息。 管理点对于软件更新是必需的。  

### <a name="software-update-points"></a>软件更新点  
 必须在 WSUS 服务器上安装软件更新点，才能在 Configuration Manager 中部署软件更新。 有关详细信息，请参阅[安装和配置软件更新点](../get-started/install-a-software-update-point.md)。

### <a name="distribution-points"></a>分发点  
 需要使用分发点来存储软件更新的内容。 有关如何安装分发点和管理内容的详细信息，请参阅[管理内容和内容基础结构](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

### <a name="client-settings-for-software-updates"></a>软件更新的客户端设置  
客户端默认会启用软件更新。 还可以使用其他一些设置来控制客户端评估软件更新符合性的方法和时间，以及控制软件更新的安装方式。  

 有关详细信息，请参阅下列文章：  

- [软件更新的客户端设置](../get-started/manage-settings-for-software-updates.md#BKMK_ClientSettings)   

- [软件更新客户端设置](../../core/clients/deploy/about-client-settings.md#software-updates)  

### <a name="reporting-services-points"></a>Reporting Services 点  
 Reporting Services 点站点系统角色可以显示软件更新的报表。 此角色是可选的，但建议使用它。 有关 Reporting Services 点创建方法的详细信息，请参阅[配置报表](../../core/servers/manage/configuring-reporting.md)。  

## <a name="which-updates-are-required-on-wsus-62-and-63"></a><a name="BKMK_wsus2012"></a>WSUS 6.2 及 6.3 需要哪些更新？

要在 WSUS 6.2 及 6.3 中同步“升级”分类，需要这两个更新  。 有时，如果在安装 KB3095113 和 KB3159706 之前同步升级项，你可能会在下载或部署这些升级项时看到错误。 下一部分介绍了可能出现的问题。  

- 必须在你的软件更新点和站点服务器上安装 2015 年 10 月发布的 [ 3095113](https://support.microsoft.com/kb/3095113)，然后再同步“升级”  分类。
  - 此更新会启用“升级”分类  。
- 要为 Windows 10 版本 1607 或更高版本提供服务，必须安装和配置 [KB 3159706](https://support.microsoft.com/help/3159706)。 KB 3159706 是 2016 年 5 月发布的。
  - 通过此更新，WSUS 可以本机方式解密用于升级 Windows 10 版本 1607 或更高版本的文件。

>[!IMPORTANT]
> 自 2017 年 7 月起，KB 3095113 和 KB 3159706 都包含在安全性月度质量汇总中  。 这意味着，你可能不会在已安装的更新中看到 KB 3095113 和 KB 3159706，因为它们可能尚未与汇总一起安装。 但是，如果需要其中一种更新，则建议安装在 2017 年 10 月之后发布的安全性月度质量汇总，因为它们包含额外的 WSUS 更新，以减少在 WSUS 的客户端 Web 服务上的内存占用  。

## <a name="download-of-windows-10-upgrades-fails-with-error-invalid-certificate-signature-or-0xc1800118"></a><a name="BKMK_RecoverUpgrades"></a>Windows 10 升级下载失败，出现“错误:证书签名无效”或 0xc1800118

本部分中所述的更新和问题仅适用于在 Windows Server 2012 或 Windows Server 2012 R2 计算机运行的 WSUS（WSUS 6.2 及 6.3）。 通常，如果你已在 2017 年 7 月之前安装 WSUS，并且你最近已启用“升级”分类，则你将仅看到本部分中所述的问题  。 但是，也可能在其他情况下看到这些问题。

### <a name="historical-information-about-kb-3095113"></a>关于 KB 3095113 的历史信息

 [KB 3095113](https://support.microsoft.com/kb/3095113) 于 2015 年 10 月[作为修补程序发布](/archive/blogs/wsus/important-update-for-wsus-4-0-kb-3095113)，添加了对 Windows 10 升级到 WSUS 的操作的支持。 借助此更新，WSUS 可在 Windows 10 的“升级”分类中同步和分发更新  。

如果未先安装 [KB 3095113](https://support.microsoft.com/kb/3095113) 就同步任何升级，则会使用不可用数据填充 WSUS 数据库 (SUSDB)。 必须先清除该数据，才能正确部署升级。 无法使用“下载软件更新”向导来下载此状态中的 Windows 10 升级。

“下载软件更新”向导的“完成”页面上会显示如下所示的错误：

``` Output
Error: Upgrade to Windows 10 Pro, version 1511, 10586
Failed to download content id {content_id}. Error: Invalid certificate signature
```

此外，PatchDownloader.log 文件会记录如下所示的错误：

``` Log
Download http://wsus.ds.b1.download.windowsupdate.com/d/upgr/2015/12/10586.0.151029-1700.th2_release_...esd...
Authentication of file C:\Users\{username}\AppData\Local\Temp\2\{temporary_filename}.tmp failed, error 0x800b0004
ERROR: DownloadContentFiles() failed with hr=0x80073633
# This log is truncated for readability.
```

过去，当发生这些错误时，会通过执行修改后的 [WSUS 解决步骤](/archive/blogs/wsus/how-to-delete-upgrades-in-wsus)来解决它们。 由于这些步骤与不执行安装 KB 3159706 后所需的手动步骤的解决方案类似，因此我们在下一部分，将这两套步骤结合在了一个解决方案中：

- [在安装 KB 3095113 或 KB 3159706 之前从同步升级中恢复](#bkmk_fix-upgrades)。

### <a name="historical-information-about-kb-3159706"></a>关于 KB 3159706 的历史信息

KB 3148812 最初发布于 2016 年 4 月，它使 WSUS 能够以本机方式解密升级 Windows 10 包时所用的 .esd 文件。 [KB 3148812 给某些客户造成了一些问题](/archive/blogs/wsus/the-long-term-fix-for-kb3148812-issues)，而它已被 [KB 3159706](https://support.microsoft.com/help/3159706) 取代。 需要在你的所有软件更新点和站点服务器上安装 KB 3159706，然后你才能为 Windows 10 版本 1607 及更高版本的设备提供服务。 但是，如果你不知道到 KB 在安装后需要手动操作，则可能会出现问题：

1. 从提升的命令提示符运行 `"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing`。
1. 在所有 WSUS 服务器上重启 WSUS 服务。

如果你不知道 KB 3159706 在安装后需要手动操作，或者你已在安装 KB 3159706 之前对 Windows 10 1607 的升级进行了同步，则在连接到 WSUS 控制台和部署升级时，会分别遇到问题。 在客户端下载升级文件时，它会收到 [0xC1800118 错误代码](https://support.microsoft.com/help/3194588/0xc1800118-error-when-you-push-windows-10-version-1607-by-using-wsus)  。

由于解决方案步骤与安装 KB 3095113 前升级同步的解决方案类似，因此我们在下一部分，将这两套步骤结合在一个解决方案中。
 

### <a name="to-recover-from-synchronizing-the-upgrades-before-you-install-kb-3095113-or-kb-3159706"></a><a name="bkmk_fix-upgrades"></a>在安装 KB 3095113 或 KB 3159706 之前从同步升级中恢复

按照以下步骤来解决 0xc1800118 错误和“错误:证书签名无效”：

1. 在 WSUS 和 Configuration Manager 中禁用“升级”分类  。 在按照这些说明操作之前，你不希望进行同步。  
   - 在顶级站点的软件更新点组件属性中取消选中“升级”分类  。
     - 有关详细信息，请参阅[配置分类和产品](../get-started/configure-classifications-and-products.md)。
   - 在[“选项”页面](/windows-server/administration/windows-server-update-services/manage/setting-up-update-synchronizations)上的“产品和分类”下取消选择 WSUS 的“升级”分类，或者使用以管理员身份运行的 PowerShell ISE    。
      ```PowerShell
      Get-WsusClassification | Where-Object -FilterScript {$_.Classification.Title -Eq "Upgrades"} | Set-WsusClassification -Disable
      ```  
     - 如果在多个 WSUS 服务器之间共享 WSUS 数据库，则只需对每个数据库取消勾选“升级”一次  。  
1. 在每个 WSUS 服务器上，从提升的命令提示符处运行：`"C:\Program Files\Update Services\Tools\wsusutil.exe" postinstall /servicing`。 然后，在所有 WSUS 服务器上重启 WSUS 服务。
   -  WSUS 会将数据库置于[单用户模式](/sql/relational-databases/databases/set-a-database-to-single-user-mode)下，然后会检查是否需要维护。 维护操作是否运行由检查结果而定。 然后，数据库会恢复到多用户模式。 
   - 如果在多个 WSUS 服务器之间共享 WSUS 数据库，则只需对每个数据库执行一次此维护。
1. 使用以管理员身份运行的 PowerShell ISE 从每个 WSUS 数据库删除所有 Windows 10 升级。
   ```PowerShell
   [reflection.assembly]::LoadWithPartialName("Microsoft.UpdateServices.Administration")
   $wsus = [Microsoft.UpdateServices.Administration.AdminProxy]::GetUpdateServer();
   $wsus.GetUpdates() | Where {$_.UpdateClassificationTitle -eq 'Upgrades' -and $_.Title -match 'Windows 10'} `
   | ForEach-Object {$wsus.DeleteUpdate($_.Id.UpdateId.ToString()); Write-Host $_.Title removed}
   ```
1. 从软件更新点使用的每个 WSUS 数据库的 tbFile 表中删除文件。 在 WSUS 数据库中，从 SQL Server Management Studio 运行以下命令：
   ```SQL
   declare @NotNeededFiles table (FileDigest binary(20) UNIQUE)
   insert into @NotNeededFiles(FileDigest) (select FileDigest from tbFile where FileName like '%.esd%'  except select FileDigest from tbFileForRevision)
   delete from tbFileOnServer where FileDigest in (select FileDigest from @NotNeededFiles)
   delete from tbFile where FileDigest in (select FileDigest from @NotNeededFiles)
   ```
1. 在 Configuration Manager 中的顶层站点上开始软件更新同步，然后等待更新完成。 会进行完全同步，原因是我们在删除“升级”分类时更改了 Configuration Manager 分类  。 有关详细信息，请参阅[同步软件更新](../get-started/synchronize-software-updates.md)。
1. 在软件更新点组件属性中选择“升级”分类  。 然后，开始另一个软件更新同步，将“升级”分类返回到 WSUS 和 Configuration Manager  。 你无需在 WSUS 中启用“升级”分类，因为 Configuration Manager 会代你操作  。
1. 如果客户端在下载升级时收到 0xC1800118 错误代码，则需要删除 Windows 更新代理使用的数据存储  。 可能还需要删除设备上隐藏的 ~BT 文件夹。 客户端下次扫描时，会针对 WSUS 服务器执行完全扫描，而不是执行增量扫描。 可使用类似于下面的示例脚本的 PowerShell 脚本：  
   ```PowerShell
   stop-service wuauserv
   remove-item -path c:\windows\softwaredistribution\datastore -recurse -force
   # If the device has a hidden ~BT folder on the c drive, delete it too by uncommenting the next line.
   # remove-item -path c:\~BT -recurse -force
   start-service wuauserv
   ```

## <a name="next-steps"></a>后续步骤
[准备软件更新管理](../get-started/prepare-for-software-updates-management.md)