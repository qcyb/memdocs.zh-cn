---
title: 发行说明
titleSuffix: Configuration Manager
description: 了解有关产品中尚未解决或 Microsoft 支持知识库文章中未涵盖的紧急问题。
ms.date: 05/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 131b6104d5724c8a4eeb0bb68c4afd9a5319abb7
ms.sourcegitcommit: 2f9999994203194a8c47d8daa6406c987a002e02
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2020
ms.locfileid: "83823956"
---
# <a name="release-notes-for-configuration-manager"></a>Configuration Manager 发行说明

适用范围：Configuration Manager (Current Branch)

在 Configuration Manager 中，产品发布说明仅限于紧急问题。 产品中尚未解决这些紧急问题，Microsoft 支持知识库文章中也未对此进行详细介绍。  

特定于功能的文档包含有关影响核心方案的已知问题的信息。  

本文包含 Configuration Manager Current Branch 的发行说明。 有关技术预览分支的信息，请参阅[技术预览](../../../get-started/technical-preview.md)  

有关不同版本引入的新功能的信息，请参阅以下文章：

- [2002 版中的新增功能](../../../plan-design/changes/whats-new-in-version-2002.md)
- [1910 版中的新增功能](../../../plan-design/changes/whats-new-in-version-1910.md)
- [版本 1906 中的新增功能](../../../plan-design/changes/whats-new-in-version-1906.md)  
- [版本 1902 中的新增功能](../../../plan-design/changes/whats-new-in-version-1902.md)

若要了解桌面分析中的新功能，请参阅[桌面分析的新变化](../../../../desktop-analytics/whats-new.md)。

> [!Tip]  
> 若要在此页面更新时收到通知，请将以下 URL 复制并粘贴到 RSS 源阅读器中：`https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`

## <a name="set-up-and-upgrade"></a>设置和升级  

### <a name="client-automatic-upgrade-happens-immediately-for-all-clients"></a>所有客户端立即执行客户端自动升级

<!-- 6040412 -->

适用于版本 1910

若站点使用[自动客户端升级](../../../clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)，当将站点更新到版本 1910 时，站点更新成功后所有客户端立即进行升级。 唯一的随机化是客户端何时收到此策略，默认情况下是每个小时。 对于拥有许多客户端的大型站点，此行为可能会占用大量网络流量和压力分发点。

有关受影响版本的详细信息，请参阅 [Configuration Manager Current Branch（版本 1910）客户端更新](https://support.microsoft.com/help/4538166)。

### <a name="site-server-in-passive-mode-doesnt-update-configurationmof"></a>被动模式下的站点服务器不会更新 configuration.mof

<!-- 5787848 -->

适用于版本 1910

如果站点包含[处于被动模式的站点服务器](../configure/site-server-high-availability.md)，则更新站点时可能会丢失清单自定义设置。 当故障转移站点服务器时，站点当前不会同步 configuration.mof。

若要解决此问题，请手动备份并还原站点的 configuration.mof。

### <a name="setup-prerequisite-warning-on-domain-functional-level-on-server-2019"></a>服务器 2019 上有关域功能级别的安装程序先决条件警告

<!-- 4904376 -->

*适用于版本 1906*

在具有运行 Windows Server 2019 的域控制器的环境中安装版本 1906 的更新时，域功能级别的先决条件检查将返回以下警告：

`[Completed with warning]:Verify that the Active Directory domain functional level is Windows Server 2003 or later`

若要解决此问题，请忽略此警告。

### <a name="azure-ad-user-discovery-and-collection-group-sync-dont-work-after-site-expansion"></a>站点扩展后，Azure AD 用户发现和集合组同步不起作用

<!-- 4797313 -->
*适用于版本 1906*

配置以下任一功能后：

- Azure Active Directory 用户组发现
- 将集合成员身份结果同步到 Azure Active Directory 组

如果随后将独立主站点扩展为具有管理中心站点的层次结构，则会在 SMS_AZUREAD_DISCOVERY_AGENT.log 中显示以下错误：

`Could not obtain application secret for tenant xxxxx. If this is after a site expansion, please run "Renew Secret Key" from admin console.`

若要解决此问题，请续订与 Azure AD 中的应用注册相关联的密钥。 有关详细信息，请参阅[续订密钥](../configure/azure-services-wizard.md#bkmk_renew)。

## <a name="role-based-administration"></a>基于角色的管理

### <a name="security-scopes-for-certain-folders-dont-replicate-from-cas-to-primary-sites"></a>特定文件夹的安全作用域不会从 CA 复制到主站点
<!--6306759-->
适用于版本 1910

升级到版本 1910 后，用户集合和设备集合中的[文件夹安全作用域](../configure/configure-role-based-administration.md#bkmk_config-folder)不会从 CA 复制到主站点。

## <a name="application-management"></a>应用程序管理

### <a name="unable-to-get-certificate-for-powershell-error-when-deploying-microsoft-edge-version-77-and-later"></a>部署 Microsoft Edge 77 及更高版本时无法获取 Powershell 错误的证书
<!--5769384-->
适用范围：Configuration Manager 版本 1910

如果在语言为瑞典语、匈牙利语或日语的操作系统上运行 Configuration Manager 控制台，则在部署 Microsoft Edge 77 及更高版本时将收到以下错误：

`Unable to get certificate for Powershell`

发生此错误的原因是瑞典语、匈牙利语或日语的 `AdminConsole\bin` 目录下没有 `scripts` 文件夹。 脚本文件夹在这些操作系统语言中进行了本地化。

若要解决此问题，请在 `AdminConsole\bin` 目录中创建名为 `scripts` 的文件夹。 将文件从本地化文件夹复制到新创建的 `scripts` 文件夹。 复制文件后，部署 Microsoft Edge 版本 77 及更高版本。

## <a name="os-deployment"></a>OS 部署

### <a name="task-sequences-cant-run-over-cmg"></a>任务序列无法通过 CMG 运行

适用范围：Configuration Manager 版本 2002

在以下两个实例中，任务序列无法在通过云管理网关 (CMG) 通信的设备上运行：

- 将站点配置为增强型 HTTP，并将管理点配置为 HTTP。<!-- 6358851 -->

    若要解决此问题，请配置 HTTPS 管理点。

- 你使用用于进行身份验证的批量注册令牌安装并注册了客户端。<!-- 6377921 -->

    若要解决此问题，请使用以下身份验证方法之一进行操作：

  - 在内部网络上预先注册设备
  - 使用客户端身份验证证书来配置设备
  - 将设备加入 Azure AD

### <a name="after-passive-site-server-is-promoted-the-default-boot-image-packages-still-have-package-source-on-the-previous-active-server"></a>提升被动站点服务器之后，默认启动映像包在上一个活动服务器上仍有包源

<!--3453224, SCCMDocs-pr issue 3097-->
适用范围：Configuration Manager 版本 1810

如果站点服务器处于被动模式（服务器 B），在将其提升为活动模式时，默认启动映像的内容位置将继续引用先前活动的服务器（服务器 A）。 如果服务器 A 出现硬件故障，则无法更新或更改默认启动映像。

此问题没有任何解决方法。

## <a name="software-updates"></a>软件更新

### <a name="security-roles-are-missing-for-phased-deployments"></a>分阶段部署缺少安全角色

<!--3479337, SCCMDocs-pr issue 3095-->
适用范围：Configuration Manager 版本 1810、1902

OS Deployment Manager 内置安全角色具有[分阶段部署](../../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md)的权限。 以下角色缺少这些权限：  

- **应用程序管理员**  
- **应用程序部署管理员**  
- **软件更新管理员**  

“应用创建者”角色可能看起来对分阶段部署具有某些权限，但无法创建部署。

具有这些角色的用户可以启动“创建分阶段部署”向导，并可以查看应用程序或软件更新的分阶段部署。 他们无法完成向导，也无法对现有部署进行任何更改。

若要解决此问题，请创建自定义安全角色。 复制现有安全角色，并在“分阶段部署”对象类上添加以下权限：

- 创建  
- 删除  
- 修改  
- 读取  

有关详细信息，请参阅[创建自定义安全角色](../configure/configure-role-based-administration.md#BKMK_CreateSecRole)。

## <a name="desktop-analytics"></a>桌面分析

### <a name="an-extended-security-update-for-windows-7-causes-them-to-show-as-unable-to-enroll"></a><a name="dawin7-diagtrack"></a> Windows 7 扩展安全更新程序导致它们显示为“无法注册”

<!-- 7283186 -->
适用范围：Configuration Manager 版本 1902、1906、1910 和 2002

Windows 7 的 2020 年 4 月扩展安全更新程序 (ESU) 已将 diagtrack.dll 的最低要求版本从 10586 更改为 10240。 此更改会导致 Windows 7 设备在桌面分析“连接运行状况”仪表板中显示为“无法注册”。 当你向下钻取到此状态的设备视图时，会看到 DiagTrack 服务配置属性显示以下状态：`Connected User Experience and Telemetry (diagtrack.dll) component is outdated. Check requirements.`

此问题不需要任何解决方法。 请勿卸载 4 月 ESU。 如果配置正确，Windows 7 设备仍会向桌面分析服务报告诊断数据，并仍会显示在门户中。

### <a name="if-you-use-hardware-inventory-for-distributed-views-you-cant-onboard-to-desktop-analytics"></a>如果将硬件清单用于分布式视图，则无法载入桌面分析

<!-- 4950335 -->
适用范围：*包含更新汇总的 Configuration Manager 版本 1902 和版本 1906*

如果你具有层次结构，并且在任何站点复制链接上启用[分布式视图](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews)的硬件清单站点数据，则在 Configuration Manager 中配置桌面分析连接后，将在 M365UploadWorker.log 中显示以下错误：

`Unexpected exception 'System.Data.SqlClient.SqlException' Remote access is not supported for transaction isolation level "SNAPSHOT".:    at System.Data.SqlClient.SqlConnection.OnError(SqlException exception, Boolean breakConnection, Action'1 wrapCloseInAction)`

若要解决此问题，请在每个站点复制链接上禁用分布式视图的硬件清单站点数据。

### <a name="console-unexpectedly-closes-when-removing-collections"></a>删除集合时控制台意外关闭

<!-- 4749443 -->
适用范围：*包含更新汇总的 Configuration Manager 版本 1902*

将网站连接到[桌面分析](../../../../desktop-analytics/connect-configmgr.md)后，可以选择要与桌面分析同步的特定集合。 如果删除集合并应用更改，则立即添加新集合会导致未处理的异常。 控制台意外关闭。

若要解决此问题，删除集合时，请选择“确定”以关闭“属性”窗口。 然后再次打开“属性”窗口，在“桌面分析连接”选项卡中添加新集合。

### <a name="pilot-status-tile-shows-some-devices-as-undefined"></a>试点状态图块显示某些设备为“未定义”

<!-- 4547783 -->
适用范围：*包含更新汇总的 Configuration Manager 版本 1902*

使用 Configuration Manager 控制台来监视试点部署状态时，在该部署计划的 Windows 目标版本上处于最新状态的试点设备在试点状态图块中显示为“未定义”。  

对此部署计划而言，这些未定义的设备具有 OS 目标版本，处于最新状态 。 无需进一步操作。

## <a name="cloud-services"></a>云服务

### <a name="azure-service-for-us-government-cloud-shows-as-public-cloud"></a>美国政府云 Azure 服务显示为公有云

<!-- 6036748 -->

适用于版本 1910

如果创建与 Azure 服务的连接，并将 Azure 环境设置为政府云，则连接属性会将环境显示为 Azure 公有云。 此问题只是控制台的显示问题，服务位于政府云中。 若要确认配置，请在站点数据库上运行以下 SQL 查询：

```SQL
Select Environment, Name, TenantID From AAD_Tenant_Ex
```

对于政府云，此查询的结果是针对特定租户的 `2`。

### <a name="cant-download-content-from-a-cloud-management-gateway-enabled-for-tls-12"></a>无法从为 TLS 1.2 启用的云管理网关下载内容

<!-- 5771680 -->

适用于版本 1906、1910 早期更新通道

如果启用云管理网关 (CMG)“充当云分发点，并提供 Azure 存储中的内容”且“强制执行 TLS 1.2”，则可能会看到内容下载失败 。

客户端上的 DataTransferService.log 中显示以下错误：

``` log
Request to https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04 failed with 400
Successfully queued event on HTTP/HTTPS failure for server 'cmg1.contoso.com'.
Error sending DAV request. HTTP code 400, status 'Bad Request'
GetDirectoryList_HTTP('https://cmg1.contoso.com:443/downloadrestservice.svc/getcontentxmlsecure?pid=CMG00013&cid=CMG00013&tid=GUID:3fb5cf5d-28a5-4460-ab39-9184ca214369&iss=CMDP.IAAS2.CONTOSO.COM&alg=1.2.840.113549.1.1.11&st=2019-11-19T01:44:04&et=2019-11-19T09:44:04') failed with code 0x87d0027e.
Error retrieving manifest (0x87d0027e).
```

服务器上的 CMGContentService.log 中显示以下错误：

``` log
ERROR: Exception processing request. Microsoft.WindowsAzure.Storage.StorageException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.Net.WebException: The underlying connection was closed: An unexpected error occurred on a receive. ---> System.ComponentModel.Win32Exception: The client and server cannot communicate, because they do not possess a common algorithm...
```

若要解决此问题，请执行以下操作：

- 将站点更新为公开发布版本 1910，该版本于 2019 年 12 月 20 日发布。 （如果之前已更新为 1910 早期更新通道，则需要在该版本可用时更新到此版本。）

- 或者，使用传统[云分发点](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)。 该角色不强制执行 TLS 1.2，但与需要 TLS 1.2 的客户端兼容。

## <a name="protection"></a>保护

### <a name="bitlocker-management-appears-in-version-1906"></a>版本 1906 中显示了 BitLocker 管理

*适用于版本 1906*

<!-- 5984688 -->

2019 年 11 月 21 日之后，如果你从版本 1902 或更低版本更新到版本 1906，BitLocker 管理功能将处于启用状态且可用。 从版本 1910 开始，此功能是一项可选功能。 版本 1906 不支持此功能。 如果在版本 1906 中尝试使用它，可能会遇到意外结果。 如果不使用此功能，则不会产生任何影响。

若要使用 [BitLocker 管理功能](../../../../protect/plan-design/bitlocker-management.md)，请更新到版本 1910。

<!--
## Backup and recovery

## Client deployment and upgrade
-->
