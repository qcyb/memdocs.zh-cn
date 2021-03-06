---
title: 日志文件引用
titleSuffix: Configuration Manager
description: Configuration Manager 客户端、服务器和依赖组件的所有日志文件的引用。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c1ff371e-b0ad-4048-aeda-02a9ff08889e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e24a7fe6a81408de48a73889db923cc8c5094ea
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700542"
---
# <a name="log-file-reference"></a>日志文件引用

适用范围：Configuration Manager (Current Branch)

在 Configuration Manager 中，客户端和站点服务器组件都将进程信息记录在单独的日志文件中。 可以使用日志文件中的信息来帮助排除可能出现的问题。 Configuration Manager 默认启用客户端和服务器组件的日志记录。

有关 Configuration Manager 中的日志文件的更一般信息，请参阅[关于 Configuration Manager 日志文件](about-log-files.md)。 本文包含有关要使用的工具、如何配置日志以及在何处查找日志的信息。

下列部分提供了可用的有关不同日志文件的详细信息。 监视 Configuration Manager 客户端和服务器日志以了解操作详细信息，并查看可帮助解决问题的错误信息。  

- [客户端日志文件](#BKMK_ClientLogs)  

  - [客户端操作](#BKMK_ClientOpLogs)  

  - [客户端安装](#BKMK_ClientInstallLog)  

  - [适用于 Linux 和 UNIX 的客户端](#BKMK_LogFilesforLnU)  

  - [适用于 Mac 计算机的客户端](#BKMK_LogfilesforMac)  

- [服务器日志文件](#BKMK_ServerLogs)  

  - [站点服务器和站点系统](#BKMK_SiteSiteServerLog)  

  - [站点服务器安装](#BKMK_SiteInstallLog)

  - [数据仓库服务点](#BKMK_DataWarehouse)

  - [回退状态点](#BKMK_FSPLog)  

  - [管理点](#BKMK_MPLog)  

  - [服务连接点](#BKMK_WITLog)  

  - [软件更新点](#BKMK_SUPLog)  

- [日志文件（按功能）](#BKMK_FunctionLogs)  

  - [应用程序管理](#BKMK_AppManageLog)  

  - [资产智能](#BKMK_AILog)  

  - [备份和恢复](#BKMK_BnRLog)  

  - [证书注册](#BKMK_CertificateEnrollment)

  - [客户端通知](#BKMK_BGB)

  - [云管理网关](#cloud-management-gateway)

  - [符合性设置和公司资源访问](#BKMK_CompSettingsLog)  

  - [Configuration Manager 控制台](#BKMK_ConsoleLog)  

  - [内容管理](#BKMK_ContentLog)  

  - [桌面分析](#desktop-analytics)

  - [发现](#BKMK_DiscoveryLog)  

  - [终结点分析](#bkmk_analytics)
  
  - [Endpoint Protection](#BKMK_EPLog)  

  - [扩展](#BKMK_Extensions)  

  - [清单](#BKMK_InventoryLog)  

  - [迁移](#BKMK_MigrationLog)  

  - [移动设备](#BKMK_MDMLog)  

  - [OS 部署](#BKMK_OSDLog)  

  - [电源管理](#BKMK_PowerMgmtLog)  

  - [远程控制](#BKMK_RCLog)  

  - [报表](#BKMK_ReportLog)  

  - [基于角色的管理](#BKMK_RBALog)  

  - [软件计数](#BKMK_MeteringLog)  

  - [软件更新](#BKMK_SU_NAPLog)  

  - [LAN 唤醒](#BKMK_WOLLog)  

  - [Windows 10 维护服务](#BKMK_WindowsServicingLog)

  - [Windows 更新代理](#BKMK_WULog)  

  - [WSUS 服务器](#BKMK_WSUSLog)  

## <a name="client-log-files"></a><a name="BKMK_ClientLogs"></a> 客户端日志文件

下列部分列出与客户端操作和客户端安装相关的日志文件。  

### <a name="client-operations"></a><a name="BKMK_ClientOpLogs"></a>客户端操作

下表列出了位于 Configuration Manager 客户端的日志文件。  

|日志名称|说明|  
|--------------|-----------------|  
|ADALOperationProvider.log|有关向 Azure Active Directory (Azure AD) 身份验证库 (ADAL) 请求端身份验证令牌的信息。|
|BitLockerManagementHandler.log|记录有关 BitLocker 管理策略的信息。|
|CAS.log|内容访问服务。 维持客户端上的本地包缓存。|  
|Ccm32BitLauncher.log|记录用于启动客户端上标记为“以 32 位方式启动”的应用程序的操作。|  
|CcmEval.log|记录 Configuration Manager 客户端状态评估活动以及 Configuration Manager 客户端所需的组件的详细信息。|  
|CcmEvalTask.log|记录由评估计划任务启动的 Configuration Manager 客户端状态评估活动。|  
|CcmExec.log|记录客户端和 SMS 代理主机服务的活动。 此日志文件还包括有关启用和禁用唤醒代理的信息。|  
|CcmMessaging.log|记录与客户端和管理点之间的通信相关的活动。|  
|CCMNotificationAgent.log|记录与客户端通知操作相关的活动。|  
|Ccmperf.log|记录与数据维护和捕获（与客户端性能计数器相关）关联的活动。|  
|CcmRestart.log|记录客户端服务重启活动。|  
|CCMSDKProvider.log|记录客户端 SDK 接口的活动。|  
|ccmsqlce.log|记录客户端使用的 SQL 精简版的活动。 通常仅在你启用调试日志记录，或者组件存在问题时，才使用此日志。 客户端运行状况任务 (ccmeval) 通常会自行纠正此组件的问题。|
|CertificateMaintenance.log|维护 Active Directory 域服务和管理点的证书。|  
|CIDownloader.log|记录有关配置项目定义下载的详细信息。|  
|CITaskMgr.log|记录每种应用程序和部署类型的任务，例如内容下载和安装/卸载操作。|  
|ClientAuth.log|记录客户端的签名和身份验证活动。|  
|ClientIDManagerStartup.log|创建和维护客户端 GUID，并确定客户端注册和分配期间的任务。|  
|ClientLocation.log|记录与客户端站点分配相关的任务。|  
|CMHttpsReadiness.log|记录运行 Configuration Manager HTTPS 准备情况评估工具的结果。 此工具检查计算机是否具有可用于 Configuration Manager 的公钥基础结构 PKI 客户端身份验证证书。|  
|CmRcService.log|记录远程控制服务的信息。|  
|CoManagementHandler.log|用于对客户端的共同管理进行故障排除。|
|ContentTransferManager.log|计划后台智能传输服务 (BITS) 或服务器消息块 (SMB) 以下载或访问包。|  
|DataTransferService.log|记录策略或包访问的所有 BITS 通信|  
|DeltaDownload.log|记录有关使用传递优化下载的快速更新和更新的相关下载信息。|  
|Diagnostics.log|记录客户端诊断操作的状态。|
|EndpointProtectionAgent|记录有关 System Center Endpoint Protection 客户端的安装以及将反恶意软件策略应用于该客户端的信息。|  
|execmgr.log|记录有关客户端上运行的包和任务序列的详细信息。|  
|ExpressionSolver.log|记录打开详细或调试日志记录时使用的增强检测方法的详细信息。|  
|ExternalEventAgent.log|记录 Endpoint Protection 恶意软件检测的历史记录以及与客户端状态相关的事件。|  
|FileBITS.log|记录所有 SMB 包访问任务|  
|FileSystemFile.log|记录软件清单和文件集合的 Windows Management Instrumentation (WMI) 提供程序的活动。|  
|FSPStateMessage.log|记录由客户端发送到回退状态点的状态消息的活动。|  
|InternetProxy.log|记录客户端的网络代理配置和使用活动。|  
|InventoryAgent.log|记录客户端上的硬件清单、软件清单和检测信号发现操作的活动。|  
|LocationCache.log|记录客户端的位置缓存使用和维护的活动。|  
|LocationServices.log|记录用于查找管理点、软件更新点和分发点的客户端活动。|  
|M365AHandler.log|有关桌面分析设置策略的信息|
|MaintenanceCoordinator.log|记录客户端的一般维护任务的活动。|  
|Mifprovider.log|记录管理信息格式 (MIF) 文件的 WMI 提供程序的活动。|  
|mtrmgr.log|监视所有软件计数过程。|  
|PolicyAgent.log|记录通过使用数据传输服务进行的策略请求。|  
|PolicyAgentProvider.log|记录策略更改。|  
|PolicyEvaluator.log|记录有关客户端计算机上的策略评估的详细信息，其中包括来自软件更新的策略。|  
|PolicyPlatformClient.log|记录位于 \Program Files\Microsoft Policy Platform 的所有提供程序（文件提供程序除外）的修正过程和符合性。|  
|PolicySdk.log|记录策略系统 SDK 接口的活动。|  
|Pwrmgmt.log|记录有关启用或禁用以及配置唤醒代理客户端设置的信息。|  
|PwrProvider.log|记录 WMI 服务中承载的电源管理提供程序 (PWRInvProvider) 的活动。 在所有支持的 Windows 版本上，提供程序会在列出硬件清单期间枚举计算机上的当前设置并应用电源计划设置。|  
|SCClient_&lt;*domain*\>@&lt;*username*\>_1.log|记录客户端计算机上的指定用户在软件中心中的活动。|  
|SCClient_&lt;*domain*\>@&lt;*username*\>_2.log|记录客户端计算机上的指定用户在软件中心中的历史活动。|  
|Scheduler.log|记录所有客户端操作的计划任务的活动。|  
|SCNotify_&lt;*domain*\>@&lt;*username*\>_1.log|记录用于为指定用户将有关软件的信息通知用户的活动。|  
|SCNotify_&lt;*domain*\>@&lt;*username*\>_1-&lt;*date_time*>.log|记录用于为指定用户将有关软件的信息通知用户的历史信息。|
|SensorWmiProvider.log|记录终结点分析传感器的 WMI 提供程序的活动。|
|SensorEndpoint.log|记录执行终结点分析策略以及将客户端数据上传到站点服务器的过程。|
|SensorManagedProvider.log|记录收集和处理用于终结点分析的事件和信息的过程。|
|setuppolicyevaluator.log|记录 WMI 中的配置和清单策略创建。|  
|SleepAgent_&lt;*domain*\>@SYSTEM_0.log|唤醒代理的主日志文件。|  
|smscliui.log|记录控制面板中 Configuration Manager 客户端的使用。|  
|SrcUpdateMgr.log|记录使用当前分发点源位置更新的已安装 Windows Installer 应用程序的活动。|  
|StatusAgent.log|记录客户端组件创建的状态消息。|  
|SWMTRReportGen.log|生成一个由计数代理收集的使用数据报表。 此数据记录在 Mtrmgr.log 中。|  
|UserAffinity.log|记录有关用户设备相关性的详细信息。|  
|VirtualApp.log|记录特定于 Application Virtualization (App-V) 部署类型评估的信息。|  
|Wedmtrace.log|记录与 Windows Embedded 客户端上的写入筛选器相关的操作。|  
|wakeprxy-install.log|记录当客户端接收客户端设置选项以打开唤醒代理时的安装信息。|  
|wakeprxy-uninstall.log|记录有关在客户端接收客户端设置选项以关闭唤醒代理时卸载唤醒代理的信息（如果以前打开了唤醒代理）。|  

### <a name="client-installation"></a><a name="BKMK_ClientInstallLog"></a> 客户端安装

下表列出的日志文件包含与 Configuration Manager 客户端安装相关的信息。  

|日志名称|说明|  
|--------------|-----------------|  
|ccmsetup.log|记录客户端安装、客户端升级和客户端删除的 ccmsetup.exe 任务。 可用于排除客户端安装问题。|  
|ccmsetup-ccmeval.log|记录客户端状态和修正的 ccmsetup.exe 任务。|  
|CcmRepair.log|记录客户端代理的维修活动。|  
|client.msi.log|记录 client.msi 执行的安装任务。 可用于排除客户端安装问题或删除问题。|  

### <a name="client-for-linux-and-unix"></a><a name="BKMK_LogFilesforLnU"></a>适用于 Linux 和 UNIX 的客户端

> [!Important]  
> 从版本 1902 开始，Configuration Manager 不支持 Linux 或 UNIX 客户端。
>
> 请考虑使用 Microsoft Azure 管理来管理 Linux 服务器。 Azure 解决方案具有广泛的 Linux 支持（包括面向 Linux 的端到端补丁管理），在大多数情况下优于 Configuration Manager 的功能。

适用于 Linux 和 UNIX 的 Configuration Manager 客户端将信息记录在以下日志文件中：  

> [!TIP]
> 使用 CMTrace 查看 Linux 和 UNIX 客户端的日志文件。

|日志名称|详细信息|
|-------------------|-----------------------------------------------------------------|
|Scxcm.log| 适用于 Linux 和 UNIX 的 Configuration Manager 客户端的核心服务 (ccmexec.bin) 的日志文件。 此日志文件包含有关 ccmexec.bin 的安装和当前操作的信息。 默认情况下，此日志文件位于 /var/opt/microsoft/scxcm.log。 要更改该日志文件的位置，请编辑“/opt/microsoft/configmgr/etc/scxcm.conf”  并更改“PATH”  字段。 你无需重启客户端计算机或服务，即可使更改生效。 可以将日志级别设置为四个不同的设置之一。 |
| Scxcmprovider.log |适用于 Linux 和 UNIX 的 Configuration Manager 客户端的 CIM 服务 (omiserver.bin) 的日志文件。 此日志文件包含有关 nwserver.bin 的当前操作的信息。 此日志位于 `/var/opt/microsoft/configmgr/scxcmprovider.log`。 若要更改该日志文件的位置，请编辑“/opt/microsoft/omi/etc/scxcmprovider.conf”并更改“PATH”字段。 你无需重启客户端计算机或服务，即可使更改生效。 可以将日志级别设置为三个设置之一。|

这两个日志文件支持多个级别的日志记录：  

- **scxcm.log**。 若要更改日志级别，请编辑 **/opt/microsoft/configmgr/etc/scxcm.conf**，并将 **MODULE** 标记的每个实例更改为所需的日志级别：  

  - 错误：指示需要引起注意的问题  

  - 警告：指示客户端操作可能出现的问题  

  - 信息：更详细的日志记录，指示客户端上的各个事件的状态  

  - 跟踪：通常用于诊断问题的详细日志记录  

- **scxcmprovider.log**。 若要更改日志级别，请编辑 **/opt/microsoft/omi/etc/scxcmprovider.conf**，并将 **MODULE** 标记的每个实例更改为所需的日志级别：  

  - 错误：指示需要引起注意的问题  

  - 警告：指示客户端操作可能出现的问题

  - 信息：更详细的日志记录，指示客户端上的各个事件的状态  

在正常操作情况下，使用“错误”日志级别。 此日志级别创建最小的日志文件。 随着日志级别从“错误”提升至“警告”、“信息”直至“跟踪”，由于会将更多数据写入文件，因此将生成更大的日志文件。  

#### <a name="manage-log-files-for-the-linux-and-unix-client"></a><a name="BKMK_ManageLinuxLogs"></a>管理适用于 Linux 和 UNIX 客户端的日志文件

适用于 Linux 和 UNIX 的客户端不会限制客户端日志文件的最大大小。 也不会将其 .log 文件的内容自动复制到其他文件，如 lo_ 文件。 如果要控制日志文件的最大大小，请实施一个过程来管理独立于适用于 Linux 和 UNIX 的 Configuration Manager 客户端的日志文件。  

例如，可以使用标准 Linux 和 UNIX 命令 **logrotate** 来管理客户端日志文件的大小和轮换。 适用于 Linux 和 UNIX 的 Configuration Manager 客户端具有接口，该接口使 **logrotate** 能够在日志轮换完成时通知客户端，以便客户端将日志记录恢复到日志文件。  

有关 **logrotate**的信息，请参阅你使用的 Linux 和 UNIX 分发版的文档。  

### <a name="client-for-mac-computers"></a><a name="BKMK_LogfilesforMac"></a>适用于 Mac 计算机的客户端

适用于 Mac 计算机的 Configuration Manager 客户端将信息记录在 Mac 计算机的以下日志文件中：  

|日志名称|详细信息|位置|
|--------------|-------------|-------------|
|CCMClient-&lt;*date_time*>.log|记录与 Mac 客户端操作相关的活动，包括应用程序管理、清单和错误日志记录。| `/Library/Application Support/Microsoft/CCM/Logs`|  
|CCMAgent-&lt;*date_time*>.log|记录与客户端操作相关的信息，包括用户登录和注销操作以及 Mac 计算机活动。| `~/Library/Logs`|  
|CCMNotifications-&lt;*date_time*>.log|记录与在 Mac 计算机上显示的 Configuration Manager 通知相关的活动。| `~/Library/Logs`|  
|CCMPrefPane-&lt;*date_time*>.log|记录与 Mac 计算机上的 Configuration Manager 偏好设置对话框相关的活动，包括常规状态和错误记录。| `~/Library/Logs`|  

站点系统服务器上的日志文件 SMS_DM.log 也会记录 Mac 计算机与为移动设备和 Mac 计算机设置的管理点之间的通信。  

## <a name="server-log-files"></a><a name="BKMK_ServerLogs"></a> 服务器日志文件

下列部分列出在站点服务器上或者与特定站点系统角色相关的日志文件。  

### <a name="site-server-and-site-systems"></a><a name="BKMK_SiteSiteServerLog"></a> 站点服务器和站点系统

下表列出 Configuration Manager 站点服务器和站点系统服务器上的日志文件。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|adctrl.log|记录注册处理活动。|站点服务器|  
|ADForestDisc.log|记录 Active Directory 林发现操作。|站点服务器|  
|adminservice.log|记录 SMS 提供程序管理服务 REST API 的操作|带有 SMS 提供程序的计算机|
|ADService.log|记录 Active Directory 中的帐户创建和安全组详细信息。|站点服务器|  
|adsgdis.log|记录 Active Directory 组发现操作。|站点服务器|  
|adsysdis.log|记录 Active Directory 系统发现操作。|站点服务器|  
|adusrdis.log|记录 Active Directory 用户发现操作。|站点服务器|  
|BusinessAppProcessWorker.log|记录适用于企业的 Microsoft Store 应用的处理。|站点服务器|
|ccm.log|记录客户端请求安装的活动。|站点服务器|  
|CertMgr.log|记录站点内通信的证书活动。|站点系统服务器|  
|chmgr.log|记录客户端健康状况管理器的活动。|站点服务器|  
|Cidm.log|使用客户端安装数据管理器 (CIDM) 记录客户端设置的更改。|站点服务器|  
|CollectionAADGroupSyncWorker.log | 自版本 2002 起，是指记录将集合成员身份结果同步到 Azure Active Directory 的日志文件。 在 1910 及更低版本中，此功能的日志记录合并到 SMS_AZUREAD_DISCOVERY_AGENT.log 中。 | 站点服务器|
|colleval.log|记录有关集合计算器创建、更改和删除集合时的详细信息。|站点服务器|  
|compmon.log|记录为站点服务器监视的组件线程的状态。|站点系统服务器|  
|compsumm.log|记录组件状态摘要生成器任务。|站点服务器|  
|ComRegSetup.log|记录站点服务器的 COM 初始安装的注册结果。|站点系统服务器|  
|dataldr.log|记录有关处理 Configuration Manager 数据库中的 (MIF) 文件和硬件清单的信息。|站点服务器|  
|ddm.log|记录发现数据管理器的活动。|站点服务器|  
|despool.log|记录传入的站点到站点通信传输|站点服务器|  
|distmgr.log|记录有关包创建、压缩、增量复制和信息更新的详细信息。 它还可包括分发管理器组件中的其他活动。 例如，安装分发点、连接尝试和安装组件。 要详细了解使用此日志的其他功能，请参阅[服务连接点](#BKMK_WITLog)和[操作系统部署](#BKMK_OSDLog)。|站点服务器|  
|EPCtrlMgr.log|记录有关将来自 Endpoint Protection 站点系统角色服务器的恶意软件威胁信息与 Configuration Manager 数据库同步的信息。|站点服务器|  
|EPMgr.log|记录 Endpoint Protection 站点系统角色的状态。|站点系统服务器|  
|EPSetup.log|提供有关安装 Endpoint Protection 站点系统角色的信息。|站点系统服务器|  
|EnrollSrv.log|记录注册服务过程的活动。|站点系统服务器|  
|EnrollWeb.log|记录注册网站过程的活动。|站点系统服务器|  
|fspmgr.log|记录回退状态点站点系统角色的活动。|站点系统服务器|  
|hman.log|记录有关站点配置更改以及在 Active Directory 域服务中发布站点信息的信息。|站点服务器|  
|Inboxast.log|记录从管理点移到站点服务器上的相应 INBOXES 文件夹的文件。|站点服务器|  
|inboxmgr.log|记录收件箱文件夹之间的文件传输活动。|站点服务器|  
|inboxmon.log|记录对收件箱文件的处理和性能计数器的更新。|站点服务器|  
|invproc.log|记录从辅助站点到其父站点的 MIF 文件转发。|站点服务器|  
|migmctrl.log|记录有关涉及到迁移作业、共享分发点和分发点升级的迁移操作的信息。|Configuration Manager 层次结构中的顶层站点，以及每个子主站点。 在多主站点的层次结构中，使用在管理中心站点中创建的日志文件。|  
|mpcontrol.log|记录管理点在 Windows Internet 名称服务 (WINS) 中的注册。 每 10 分钟记录一次管理点的可用性。|站点系统服务器|  
|mpfdm.log|记录将客户端文件移到站点服务器上的相应 INBOXES 文件夹的管理点组件的操作。|站点系统服务器|  
|mpMSI.log|记录有关管理点安装的详细信息。|站点服务器|  
|MPSetup.log|记录管理点安装包装过程|站点服务器|  
|netdisc.log|记录网络发现操作。|站点服务器|  
|NotiCtrl.log|应用程序请求通知。|站点服务器|  
|ntsvrdis.log|记录站点系统服务器的发现活动。|站点服务器|  
|Objreplmgr|记录对复制的对象更改通知的处理。|站点服务器|  
|offermgr.log|记录播发更新。|站点服务器|  
|offersum.log|记录部署状态消息的摘要。|站点服务器|  
|OfflineServicingMgr.log|记录将更新应用到操作系统映像文件的活动。|站点服务器|  
|outboxmon.log|记录对发件箱文件的处理和性能计数器的更新。|站点服务器|  
|PerfSetup.log|记录性能计数器的安装结果。|站点系统服务器|  
|PkgXferMgr.log|记录负责将主站点中的内容发送到远程分发点的 SMS_Executive 组件的操作。|站点服务器|  
|policypv.log|记录客户端策略的更新，以反映对客户端设置或部署的更改。|主站点服务器|  
|rcmctrl.log|记录层次结构中的站点之间的数据库复制活动。|站点服务器|  
|replmgr.log|记录站点服务器组件与计划程序组件之间的文件复制。|站点服务器|  
|ResourceExplorer.log|记录有关运行资源管理器的错误、警告和信息。|运行 Configuration Manager 控制台的计算机|  
|RESTPROVIDERSetup.log|安装 SMS 提供程序管理服务 REST API|带有 SMS 提供程序的计算机|
|ruleengine.log|记录有关自动部署规则（涉及到标识、内容下载以及软件更新组和部署创建）的详细信息。|站点服务器|  
|schedule.log|记录有关站点间作业和文件复制的详细信息。|站点服务器|  
|sender.log|记录在站点之间通过基于文件的复制来传输的文件。|站点服务器|  
|sinvproc.log|将有关软件清单数据的处理信息记录到站点数据库。|站点服务器|  
|sitecomp.log|记录有关对安装在站点中的所有站点系统服务器上的站点组件进行维护的详细信息。|站点服务器|  
|sitectrl.log|记录对数据库中的站点控制对象所做的站点设置更改。|站点服务器|  
|sitestat.log|记录所有站点系统的监视进程的可用性和磁盘空间。|站点服务器|
|SMS_AZUREAD_DISCOVERY_AGENT.log| 记录 Azure Active Directory (Azure AD) 用户和用户组发现的日志文件。 在 1910 及更低版本中，它还记录了将集合成员结果同步到 Azure AD 的情况。| 站点服务器|
|SMS_BUSINESS_APP_PROCESS_MANAGER.log|用于同步来自适用于企业的 Microsoft Store 的应用的组件的日志文件。|站点服务器|
|SMS_DataEngine.log|管理见解的日志文件。|站点服务器|
|SMS_ISVUPDATES_SYNCAGENT.log| 用于同步第三方软件更新的日志文件。| Configuration Manager 层次结构中的顶层软件更新点。|
|SMS_OrchestrationGroup.log| 业务流程组的日志文件|站点服务器|
|SMS_PhasedDeployment.log| 分阶段部署的日志文件|Configuration Manager 层次结构中的顶层站点|
|SMS_REST_PROVIDER.log|SMS 提供程序管理服务 REST API 的服务运行状况，包括证书信息|带有 SMS 提供程序的计算机|
|SmsAdminUI.log|记录 Configuration Manager 控制台活动。|运行 Configuration Manager 控制台的计算机|  
|SMSAWEBSVCSetup.log|记录应用程序目录 Web 服务的安装活动。|站点系统服务器|  
|smsbkup.log|记录站点备份过程的输出。|站点服务器|  
|smsdbmon.log|记录数据库更改。|站点服务器|  
|SMSENROLLSRVSetup.log|记录注册 Web 服务的安装活动。|站点系统服务器|  
|SMSENROLLWEBSetup.log|记录注册网站的安装活动。|站点系统服务器|  
|smsexec.log|记录对所有站点服务器组件线程的处理。|站点服务器或站点系统服务器|  
|SMSFSPSetup.log|记录由回退状态点安装生成的消息。|站点系统服务器|  
|SMSPORTALWEBSetup.log|记录应用程序目录网站的安装活动。|站点系统服务器|  
|SMSProv.log|记录 WMI 提供程序对站点数据库的访问。|带有 SMS 提供程序的计算机|  
|srsrpMSI.log|记录来自 MSI 输出的报表点安装过程的详细结果。|站点系统服务器|  
|srsrpsetup.log|记录报表点安装过程的结果。|站点系统服务器|  
|statesys.log|记录对状态系统消息的处理。|站点服务器|  
|statmgr.log|记录将所有状态消息写入到数据库的操作。|站点服务器|  
|swmproc.log|记录对计数文件和设置的处理。|站点服务器|
|UXAnalyticsUploadWorker.log|记录将数据上传到终结点分析服务的过程。|站点服务器|

### <a name="site-server-installation"></a><a name="BKMK_SiteInstallLog"></a> 站点服务器安装

下表列出了包含与站点安装相关的信息的日志文件。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|ConfigMgrPrereq.log|记录必备组件的评估和安装活动。|站点服务器|  
|ConfigMgrSetup.log|记录站点服务器安装程序的详细输出。|站点服务器|  
|ConfigMgrSetupWizard.log|记录与安装向导中的活动相关的信息。|站点服务器|  
|SMS_BOOTSTRAP.log|记录有关启动辅助站点安装过程的进度的信息。 实际安装过程的详细信息包含在 ConfigMgrSetup.log 中。|站点服务器|  
|smstsvc.log|记录有关 Windows 服务安装、使用和删除的信息。 Windows 使用此服务来测试服务器之间的网络连接和权限。 它会使用创建连接的服务器的计算机帐户。|站点服务器和站点系统服务器|  

### <a name="data-warehouse-service-point"></a><a name="BKMK_DataWarehouse"></a> 数据仓库服务点

下表列出了包含与数据仓库服务点相关的信息的日志文件。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|DWSSMSI.log|记录由数据仓库服务点安装生成的消息。|站点系统服务器|  
|DWSSSetup.log|记录由数据仓库服务点安装生成的消息。|站点系统服务器|  
|Microsoft.ConfigMgrDataWarehouse.log|记录有关站点数据库和数据仓库数据库之间的数据同步的信息。|站点系统服务器|  

### <a name="fallback-status-point"></a><a name="BKMK_FSPLog"></a>回退状态点

下表列出了包含与回退状态点相关的信息的日志文件。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|FspIsapi|记录有关从移动设备旧客户端和客户端计算机到回退状态点的通信的详细信息。|站点系统服务器|  
|fspMSI.log|记录由回退状态点安装生成的消息。|站点系统服务器|  
|fspmgr.log|记录回退状态点站点系统角色的活动。|站点系统服务器|  

### <a name="management-point"></a><a name="BKMK_MPLog"></a>管理点

下表列出了包含与管理点相关的信息的日志文件。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|CcmIsapi.log|记录终结点上的客户端消息活动。|站点系统服务器|
|CCM_STS.log|记录身份验证令牌的活动，令牌来自 Azure Active Directory 或是站点发出的客户端令牌。|站点系统服务器|
|ClientAuth.log|记录签名和身份验证活动。|站点系统服务器|
|MP_CliReg.log|记录管理点处理的客户端注册活动。|站点系统服务器|  
|MP_Ddr.log|从客户端记录 XML.ddr 记录的转换，然后将这些记录复制到站点服务器。|站点系统服务器|  
|MP_Framework.log|记录核心管理点和客户端框架组件的活动。|站点系统服务器|  
|MP_GetAuth.log|记录客户端授权活动。|站点系统服务器|  
|MP_GetPolicy.log|记录来自客户端计算机的策略请求活动。|站点系统服务器|  
|MP_Hinv.log|记录有关转换来自客户端的 XML 硬件清单记录并将这些文件复制到站点服务器的详细信息。|站点系统服务器|  
|MP_Location.log|记录来自客户端的位置请求和回复活动。|站点系统服务器|  
|MP_OOBMgr.log|记录与从客户端接收 OTP 相关的管理点活动。|站点系统服务器|  
|MP_Policy.log|记录策略通信。|站点系统服务器|  
|MP_RegistrationManager.log|记录与客户端注册相关的活动，例如验证证书、CRL 和令牌。|站点系统服务器|
|MP_Relay.log|记录从客户端收集的文件的传输。|站点系统服务器|  
|MP_Retry.log|记录硬件清单重试过程。|站点系统服务器|  
|MP_Sinv.log|记录有关转换来自客户端的 XML 软件清单记录并将这些文件复制到站点服务器的详细信息。|站点系统服务器|  
|MP_SinvCollFile.log|记录有关文件集合的详细信息。|站点系统服务器|  
|MP_Status.log|记录有关转换来自客户端的 XML.svf 状态消息文件并将这些文件复制到站点服务器的详细信息。|站点系统服务器|
|mpcontrol.log|记录管理点在 WINS 中的注册。 每 10 分钟记录一次管理点的可用性。|站点服务器|  
|mpfdm.log|记录将客户端文件移到站点服务器上的相应 INBOXES 文件夹的管理点组件的操作。|站点系统服务器|  
|mpMSI.log|记录有关管理点安装的详细信息。|站点服务器|  
|MPSetup.log|记录管理点安装包装过程|站点服务器|  
|UserService.log|记录来自软件中心的用户请求，从服务器检索/安装用户可用的应用程序。|站点系统服务器|

### <a name="service-connection-point"></a><a name="BKMK_WITLog"></a>服务连接点

下表列出了包含与服务连接点相关的信息的日志文件。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|CertMgr.log|记录证书和代理帐户信息。|站点服务器|  
|colleval.log|记录有关集合计算器创建、更改和删除集合时的详细信息。|主站点和管理中心站点|  
|Cloudusersync.log|记录为用户启用许可证的情况。|具有服务连接点的计算机|  
|dataldr.log|记录有关对 MIF 文件的处理的信息。|站点服务器|  
|ddm.log|记录发现数据管理器的活动。|站点服务器|  
|distmgr.log|记录有关内容分发请求的详细信息。|顶层站点服务器|  
|Dmpdownloader.log|记录有关通过 Microsoft Intune 进行的下载的详细信息。|具有服务连接点的计算机|  
|Dmpuploader.log|记录有关将数据库更改上传到 Microsoft Intune 的详细信息。|具有服务连接点的计算机|  
|hman.log|记录有关邮件转发的信息。|站点服务器|  
|MSfBSyncWorker.log|记录与适用于企业的 Microsoft Store 的通信的相关信息。|具有服务连接点的计算机|
|objreplmgr.log|记录对策略和分配的处理。|主站点服务器|  
|policypv.log|记录所有策略的策略生成情况。|站点服务器|  
|outgoingcontentmanager.log|记录上传到 Microsoft Intune 的内容。|具有服务连接点的计算机|  
|ServiceConnectionTool.log|基于所用的参数，记录有关[服务连接工具](../../servers/manage/use-the-service-connection-tool.md)使用情况的详细信息。 每次运行该工具时，该工具都将替换现有的任何日志文件。|它与工具所在的位置相同|
|sitecomp.log|记录服务连接点安装的详细信息。|站点服务器|  
|SmsAdminUI.log|记录 Configuration Manager 控制台活动。|运行 Configuration Manager 控制台的计算机|  
|SMS_CLOUDCONNECTION.log|记录有关云服务的信息。|具有服务连接点的计算机|
|SMSProv.log|记录 SMS 提供程序的活动。 Configuration Manager 控制台活动使用 SMS 提供程序。|带有 SMS 提供程序的计算机|  
|SrvBoot.log|记录关于服务连接点安装程序服务的详细信息。|具有服务连接点的计算机|  
|Statesys.log|记录对移动设备管理消息的处理。|主站点和管理中心站点|  

### <a name="software-update-point"></a><a name="BKMK_SUPLog"></a>软件更新点

下表列出了包含与软件更新点相关的信息的日志文件。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|objreplmgr.log|记录有关将软件更新通知文件从父站点复制到子站点的详细信息。|站点服务器|  
|PatchDownloader.log|记录有关从更新源将软件更新下载到站点服务器上的下载目的地的过程的详细信息。|手动下载更新时，此文件位于使用控制台的计算机上的 `%temp%` 目录中。 对于自动部署规则，如果 Configuration Manager 客户端安装在站点服务器上，则此文件位于 `%windir%\CCM\Logs` 中的站点服务器上。|  
|ruleengine.log|记录有关自动部署规则（涉及到标识、内容下载以及软件更新组和部署创建）的详细信息。|站点服务器|
|SMS_ISVUPDATES_SYNCAGENT.log| 用于同步第三方软件更新的日志文件。| Configuration Manager 层次结构中的顶层软件更新点。|
|SUPSetup.log|记录有关软件更新点安装的详细信息。 当软件更新点安装完成后，会向此日志文件写入 **Installation was successful** 。|站点系统服务器|  
|WCM.log|记录有关软件更新点配置的详细信息，以及有关连接到 WSUS 服务器的详细信息（以获取有关订阅的更新类别、分类和语言等信息）。|连接到 WSUS 服务器的站点服务器|  
|WSUSCtrl.log|记录有关站点的配置、数据库连接和 WSUS 服务器健康状况的详细信息。|站点系统服务器|  
|wsyncmgr.log|记录有关软件更新同步过程的详细信息。|站点系统服务器|  
|WUSSyncXML.log|记录有关 Microsoft 更新清单工具的同步过程的详细信息。|配置为 Microsoft 更新清单工具的同步主机的客户端计算机|  


## <a name="log-files-by-functionality"></a><a name="BKMK_FunctionLogs"></a> 日志文件（按功能）

下列部分列出了与 Configuration Manager 功能相关的日志文件。  

### <a name="application-management"></a><a name="BKMK_AppManageLog"></a>应用程序管理

下表列出了包含与应用程序管理相关的信息的日志文件。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|AppIntentEval.log|记录有关应用程序的当前和预期状态、它们的适用性、是否满足了要求、部署类型和依赖关系的详细信息。|客户端|  
|AppDiscovery.log|记录有关客户端计算机上的应用程序发现或检测的详细信息。|客户端|  
|AppEnforce.log|记录有关为客户端上的应用程序执行的强制操作（安装和卸载）的详细信息。|客户端|  
|AppGroupHandler.log|从版本 1906 开始，应用程序组的检测和强制信息|客户端|
|awebsctl.log|记录针对应用程序目录 Web 服务点站点系统角色的监视活动。|站点系统服务器|  
|awebsvcMSI.log|记录应用程序目录 Web 服务点站点系统角色的详细安装信息。|站点系统服务器|  
|BusinessAppProcessWorker.log|记录适用于企业的 Microsoft Store 应用的处理。|站点服务器|
|CCMSDKProvider.log|记录应用程序管理 SDK 的活动。|客户端|  
|colleval.log|记录有关集合计算器创建、更改和删除集合时的详细信息。|站点系统服务器|  
|ConfigMgrSoftwareCatalog.log|记录应用程序目录的活动（包括它使用 Silverlight 的情况）。|客户端|  
|MSfBSyncWorker.log|记录与适用于企业的 Microsoft Store 的通信的相关信息。|具有服务连接点的计算机|
|NotiCtrl.log|应用程序请求通知。|站点服务器|  
|portlctl.log|记录针对应用程序目录网站点站点系统角色的监视活动。|站点系统服务器|  
|portlwebMSI.log|记录应用程序目录网站角色的 MSI 安装活动。|站点系统服务器|  
|PrestageContent.log|记录有关在远程预留分发点上使用 ExtractContent.exe 工具的详细信息。 此工具提取已导出到文件的内容。|站点系统服务器|  
|ServicePortalWebService.log|记录应用程序目录 Web 服务的活动。|站点系统服务器|  
|ServicePortalWebSite.log|记录应用程序目录网站的活动。|站点系统服务器|  
|SettingsAgent.log|特定应用程序的强制信息，记录应用程序组评估的业务流程，以及共同管理策略的详细信息。|客户端|
|SMS_BUSINESS_APP_PROCESS_MANAGER.log|用于同步来自适用于企业的 Microsoft Store 的应用的组件的日志文件。|站点服务器|
|SMS_CLOUDCONNECTION.log|记录有关云服务的信息。|具有服务连接点的计算机|
|SMSdpmon.log|记录有关在分发点上配置的分发点健康状况监视计划任务的详细信息。|站点服务器|  
|SoftwareCatalogUpdateEndpoint.log|记录管理在软件中心中显示的应用程序目录的 URL 的活动。|客户端|  
|SoftwareCenterSystemTasks.log|记录与软件中心必备组件验证相关的活动。|客户端|  
|TSDTHandler.log|对于任务序列部署类型。 它记录了从应用实施（安装或卸载）到任务序列启动的过程。 将其与 AppEnforce.log 和 smsts.log 一起使用。|客户端|<!-- MEMDocs#336 -->

#### <a name="packages-and-programs"></a>包和程序

下表列出了包含与部署包和程序相关的信息的日志文件。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|colleval.log|记录有关集合计算器创建、更改和删除集合时的详细信息。|站点服务器|  
|execmgr.log|记录有关包和运行的任务序列的详细信息。|客户端|  

### <a name="asset-intelligence"></a><a name="BKMK_AILog"></a>资产智能

下表列出的日志文件包含与资产智能相关的信息。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|AssetAdvisor.log|记录资产智能清单操作的活动。|客户端|  
|aikbmgr.log|记录有关收件箱中用于更新资产智能目录的 XML 文件处理的详细信息。|站点服务器|  
|AIUpdateSvc.log|记录资产智能同步点与云服务的交互。|站点系统服务器|  
|AIUSMSI.log|记录有关资产智能同步点站点系统角色安装的详细信息。|站点系统服务器|  
|AIUSSetup.log|记录有关资产智能同步点站点系统角色安装的详细信息。|站点系统服务器|  
|ManagedProvider.log|记录有关发现具有关联软件标识标志的软件的详细信息。 也记录与硬件清单相关的活动。|站点系统服务器|  
|MVLSImport.log|记录有关导入的许可文件处理的详细信息。|站点系统服务器|  

### <a name="backup-and-recovery"></a><a name="BKMK_BnRLog"></a>备份和恢复

下表列出的日志文件包含与备份和恢复操作（包括站点重置以及站点更改为 SMS 提供程序）相关的信息。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|ConfigMgrSetup.log|记录有关当 Configuration Manager 从备份恢复站点时的设置和恢复任务的信息。|站点服务器|  
|smsbkup.log|记录有关站点备份活动的详细信息。|站点服务器|  
|smssqlbkup.log|记录站点数据库备份过程的输出（如果 SQL Server 安装在不是站点服务器的服务器上）。|站点数据库服务器|  
|Smswriter.log|记录有关备份过程使用的 Configuration Manager VSS 编写器的状态的信息。|站点服务器|  

### <a name="certificate-enrollment"></a><a name="BKMK_CertificateEnrollment"></a>证书注册

下表列出的 Configuration Manager 日志文件包含与证书注册相关的信息。 证书注册在运行网络设备注册服务 (NDES) 的服务器上使用证书注册点和 Configuration Manager 策略模块。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|Crp.log|记录注册活动。|证书注册点|  
|Crpctrl.log|记录证书注册点的操作运行状况。|证书注册点|  
|Crpsetup.log|记录有关证书注册点的安装和配置的详细信息。|证书注册点|  
|Crpmsi.log|记录有关证书注册点的安装和配置的详细信息。|证书注册点|  
|NDESPlugin.log|记录质询验证和证书注册活动。|Configuration Manager 策略模块和网络设备注册服务|  

除了 Configuration Manager 日志文件外，请在运行网络设备注册服务的服务器和承载证书注册点的服务器上的事件查看器中查看 Windows 应用程序日志。 例如，从“NetworkDeviceEnrollmentService”源中查找消息。

你还可以使用下列日志文件：  

- 网络设备注册服务的 IIS 日志文件：%SYSTEMDRIVE%\inetpub\logs\LogFiles\W3SVC1  

- 证书注册点的 IIS 日志文件：%SYSTEMDRIVE%\inetpub\logs\LogFiles\W3SVC1  

- 网络设备注册策略日志文件： **mscep.log**  

    > [!NOTE]  
    > 此文件位于 NDES 帐户配置文件的文件夹中，例如，位于 C:\Users\SCEPSvc 中。 有关如何启用 NDES 日志记录的详细信息，请参阅 NDES wiki 的[启用日志记录](https://social.technet.microsoft.com/wiki/contents/articles/9063.active-directory-certificate-services-ad-cs-network-device-enrollment-service-ndes.aspx#Enable_Logging)部分。  

### <a name="client-notification"></a><a name="BKMK_BGB"></a>客户端通知

下表列出的日志文件包含与客户端通知相关的信息。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|bgbmgr.log|记录与客户端通知任务以及处理联机和任务状态文件相关的站点服务器活动的详细信息。|站点服务器|  
|BGBServer.log|记录通知服务器的活动，如客户端服务器之间的通信和将任务推送至客户端。 也记录要发送到站点服务器的联机和任务状态文件生成的相关信息。|管理点|  
|BgbSetup.log|在安装和卸载过程中记录通知服务器安装封装进程的活动。|管理点|  
|bgbisapiMSI.log|记录有关通知服务器安装和卸载的详细信息。|管理点|  
|BgbHttpProxy.log|记录通知 HTTP 代理在使用 HTTP 将客户端的消息转播到通知服务器或从中转播该消息时的活动。|客户端|  
|CCMNotificationAgent.log|记录通知代理的活动（例如客户端服务器之间的通信）以及有关已接收并分派给其他客户端代理的任务的信息。|客户端|  

### <a name="cloud-management-gateway"></a>云管理网关

下表列出的日志文件包含与云管理网关相关的信息。

|日志名称|说明|带有日志文件的计算机|
|--------------|-----------------|----------------------------|  
|CloudMgr.log|记录有关部署云管理网关服务、正在进行的服务状态，以及与服务相关联的使用数据的详细信息。 要配置日志记录级别，请在以下注册表项中编辑“日志记录级别”值：`HKLM\SOFTWARE\ Microsoft\SMS\COMPONENTS\ SMS_CLOUD_ SERVICES_MANAGER`|主站点服务器或 CAS 上的 installdir 文件夹。|
|CMGSetup.log <sup>[备注 1](#bkmk_note1)</sup>|记录有关云管理网关部署（Azure 中的本地部署）的第二阶段的详细信息。 要配置日志记录级别，请使用“Azure 门户\云服务配置”选项卡上的“跟踪级别”设置，即“信息”（默认）、“详细”和“错误”    。|你的 Azure 服务器上的 **%approot%\logs**，或站点系统服务器上的 SMS/Logs 文件夹|
|CMGService.log <sup>[备注 1](#bkmk_note1)</sup>|记录有关 Azure 中云管理网关服务核心组件的详细信息。 要配置日志记录级别，请使用“Azure 门户\云服务配置”选项卡上的“跟踪级别”设置，即“信息”（默认）、“详细”和“错误”    。|你的 Azure 服务器上的 **%approot%\logs**，或站点系统服务器上的 SMS/Logs 文件夹|
|SMS_Cloud_ProxyConnector.log|记录有关设置云管理网关服务和云管理网关连接点之间的连接的详细信息。|站点系统服务器|
|CMGContentService.log <sup>[备注 1](#bkmk_note1)</sup>|<!--SCCMDocs-pr issue #2822-->启用 CMG 从 Azure 存储中提供内容时，此日志会记录该服务的详细信息。|你的 Azure 服务器上的 **%approot%\logs**，或站点系统服务器上的 SMS/Logs 文件夹|

- 对于部署疑难解答，请使用 **CloudMgr.log** 和 **CMGSetup.log**。
- 对于服务运行状况疑难解答，请使用 **CMGService.log** 和 **SMS_Cloud_ProxyConnector.log**。
- 对于客户端流量疑难解答，请使用 **CMGHttpHandler.log**、**CMGService.log** 和 **SMS_Cloud_ProxyConnector.log**。

#### <a name="note-1-logs-synchronized-from-azure"></a><a name="bkmk_note1"></a> 注释 1：从 Azure 同步的日志

这些是云服务管理器每 5 分钟从 Azure 存储同步的本地 Configuration Manager 日志文件。 云管理网关每 5 分钟将日志推送到 Azure 存储。 所以最大延迟为 10 分钟。 详细的开关将影响本地日志和远程日志。 实际文件名包含服务名称和角色实例标识符。 例如，CMG-ServiceName-RoleInstanceID-CMGSetup.log 

### <a name="compliance-settings-and-company-resource-access"></a><a name="BKMK_CompSettingsLog"></a>符合性设置和公司资源访问

下表列出的日志文件包含与符合性设置和公司资源访问相关的信息。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|CIAgent.log|记录有关符合性设置、软件更新和应用程序管理的修正过程和符合性的详细信息。|客户端|  
|CITaskManager.log|记录有关配置项目任务计划的信息。|客户端|  
|DCMAgent.log|记录有关配置项目和应用程序的评估、冲突报告以及修正的高级信息。|客户端|  
|DCMReporting.log|记录有关为配置项目将策略平台结果报告到状态消息中的信息。|客户端|  
|DcmWmiProvider.log|记录有关从 WMI 中读取配置项目 synclet 的信息。|客户端|  

### <a name="configuration-manager-console"></a><a name="BKMK_ConsoleLog"></a> Configuration Manager 控制台

下表列出的日志文件包含与 Configuration Manager 控制台相关的信息。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|ConfigMgrAdminUISetup.log|记录 Configuration Manager 控制台安装。|运行 Configuration Manager 控制台的计算机|  
|SmsAdminUI.log|记录有关 Configuration Manager 控制台的操作的信息。|运行 Configuration Manager 控制台的计算机|  
|SMSProv.log|记录 SMS 提供程序的活动。 Configuration Manager 控制台活动使用 SMS 提供程序。|站点服务器或站点系统服务器|  

### <a name="content-management"></a><a name="BKMK_ContentLog"></a>内容管理

下表列出的日志文件包含与内容管理相关的信息。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|CloudDP-&lt;guid\>.log|记录基于特定云的分发点的详细信息，包括有关存储和内容访问的信息。|站点系统服务器|  
|CloudMgr.log|记录有关内容设置、收集存储和带宽统计数据以及管理员发起的用于启动或停止云服务（运行基于云的分发点）的操作的详细信息。|站点系统服务器|  
|DataTransferService.log|记录策略或包访问的所有 BITS 通信 请求分发点也使用此日志进行内容管理。|配置为请求分发点的计算机|  
|PullDP.log|记录有关请求分发点从源分发点传输的内容的详细信息。|配置为请求分发点的计算机|  
|PrestageContent.log|记录有关在远程预留分发点上使用 ExtractContent.exe 工具的详细信息。 此工具提取已导出到文件的内容。|站点系统角色|  
|SMSdpmon.log|记录有关在分发点上配置的分发点运行状况监视计划任务的详细信息。|站点系统角色|  
|smsdpprov.log|记录有关提取从主站点接收的压缩文件的详细信息。 此日志由远程分发点的 WMI 提供程序生成。|未与站点服务器共置的分发点计算机|  
|smsdpusage.log|记录有关运行的 smsdpusage.exe 的详细信息，并收集分发点使用情况摘要报告的数据。|站点系统角色|  

### <a name="desktop-analytics"></a>桌面分析

使用以下日志文​​件来帮助解决与 Configuration Manager 集成的桌面分析问题。

服务连接点上的日志文件位于以下目录中：`%ProgramFiles%\Configuration Manager\Logs\M365A`。
Configuration Manager 客户端上的日志文件位于以下目录中：`%WinDir%\CCM\logs`。

| 日志 | 说明 |带有日志文件的计算机|
|---------|---------|---------|
| M365ADeploymentPlanWorker.log | 有关部署计划从桌面分析云服务同步到本地 Configuration Manager 的信息 |服务连接点|
| M365ADeviceHealthWorker.log | 有关从 Configuration Manager 到 Microsoft 云的设备运行状况上载的信息 |服务连接点|
| M365AHandler.log | 有关桌面分析设置策略的信息 |客户端|
| M365AUploadWorker.log | 有关从 Configuration Manager 到 Microsoft 云的收集和设备上载的信息 |服务连接点|
| SmsAdminUI.log | 有关 Configuration Manager 控制台活动（例如配置 Azure 云服务）的信息  |服务连接点|

### <a name="discovery"></a><a name="BKMK_DiscoveryLog"></a>发现

下表列出了包含与发现相关的信息的日志文件。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|adsgdis.log|记录 Active Directory 安全组发现操作。|站点服务器|  
|adsysdis.log|记录 Active Directory 系统发现操作。|站点服务器|  
|adusrdis.log|记录 Active Directory 用户发现操作。|站点服务器|  
|ADForestDisc.log|记录 Active Directory 林发现操作。|站点服务器|  
|ddm.log|记录发现数据管理器的活动。|站点服务器|  
|InventoryAgent.log|记录客户端上的硬件清单、软件清单和检测信号发现操作的活动。|客户端|  
|netdisc.log|记录网络发现操作。|站点服务器|  

### <a name="endpoint-analytics"></a><a name="bkmk_analytics"></a> 终结点分析

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|UXAnalyticsUploadWorker.log|记录将数据上传到终结点分析服务的过程。|站点服务器|  
|SensorWmiProvider.log|记录终结点分析传感器的 WMI 提供程序的活动。|客户端|  
|SensorEndpoint.log|记录执行终结点分析策略以及将客户端数据上传到站点服务器的过程。|客户端|
|SensorManagedProvider.log|记录收集和处理用于终结点分析的事件和信息的过程。|客户端|

### <a name="endpoint-protection"></a><a name="BKMK_EPLog"></a> Endpoint Protection

下表列出的日志文件包含与 Endpoint Protection 相关的信息。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|EndpointProtectionAgent.log|记录有关 Endpoint Protection 客户端的安装以及将反恶意软件策略应用于该客户端的详细信息。|客户端|  
|EPCtrlMgr.log|记录有关将来自 Endpoint Protection 角色服务器的恶意软件威胁信息与 Configuration Manager 数据库同步的详细信息。|站点系统服务器|  
|EPMgr.log|监视 Endpoint Protection 站点系统角色的状态。|站点系统服务器|  
|EPSetup.log|提供有关安装 Endpoint Protection 站点系统角色的信息。|站点系统服务器|  

### <a name="extensions"></a><a name="BKMK_Extensions"></a>扩展

下表列出的日志文件包含与扩展相关的信息。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|AdminUI.ExtensionInstaller.log|记录有关从 Microsoft 下载所有扩展插件以及安装和卸载所有扩展插件的信息。|运行 Configuration Manager 控制台的计算机|  
|FeatureExtensionInstaller.log|在 Configuration Manager 控制台启用或禁用各个扩展时，记录有关其安装和删除的信息。|运行 Configuration Manager 控制台的计算机|  
|SmsAdminUI.log|记录 Configuration Manager 控制台活动。|运行 Configuration Manager 控制台的计算机|  

### <a name="inventory"></a><a name="BKMK_InventoryLog"></a>清单

下表列出的日志文件包含与处理清单数据相关的信息。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|dataldr.log|记录有关处理 Configuration Manager 数据库中的 (MIF) 文件和硬件清单的信息。|站点服务器|  
|invproc.log|记录从辅助站点到其父站点的 MIF 文件转发。|辅助站点服务器|  
|sinvproc.log|将有关软件清单数据的处理信息记录到站点数据库。|站点服务器|  

### <a name="metering"></a><a name="BKMK_MeteringLog"></a>计费

下表列出的日志文件包含与计数相关的信息。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|监视所有软件计数过程。|客户端|  
|SWMTRReportGen.log|生成一个由计数代理收集的使用数据报表。 此数据记录在 Mtrmgr.log 中。|客户端|
|swmproc.log|记录对计数文件和设置的处理。|站点服务器|

### <a name="migration"></a><a name="BKMK_MigrationLog"></a>迁移

下表列出的日志文件包含与迁移相关的信息。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|migmctrl.log|记录有关涉及到迁移作业、共享分发点和分发点升级的迁移操作的信息。|Configuration Manager 层次结构中的顶层站点，以及每个子主站点。 在多主站点的层次结构中，使用在管理中心站点中创建的日志文件。|  

### <a name="mobile-devices"></a><a name="BKMK_MDMLog"></a>移动设备

下列部分列出的日志文件包含与管理移动设备相关的信息。  

#### <a name="enrollment"></a><a name="BKMK_EnrollmentLog"></a>注册

下表列出的日志包含与移动设备注册相关的信息。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|DMPRP.log|记录为移动设备启用的管理点与管理点终结点之间的通信。|站点系统服务器|  
|dmpmsi.log|记录针对移动设备启用的管理点配置的 Windows Installer 数据。|站点系统服务器|  
|DMPSetup.log|记录管理点的配置（如果为移动设备启用了管理点）。|站点系统服务器|  
|enrollsrvMSI.log|记录注册点的配置的 Windows Installer 数据。|站点系统服务器|  
|enrollmentweb.log|记录移动设备和注册代理点之间的通信。|站点系统服务器|  
|enrollwebMSI.log|记录注册代理点的配置的 Windows Installer 数据。|站点系统服务器|  
|enrollmentservice.log|记录注册代理点和注册点之间的通信。|站点系统服务器|  
|SMS_DM.log|记录移动设备、Mac 计算机与为移动设备和 Mac 计算机启用的管理点之间的通信。|站点系统服务器|  

#### <a name="exchange-server-connector"></a><a name="BKMK_ExchSrvLog"></a> Exchange Server 连接器

以下日志包含与 Exchange Server 连接器相关的信息。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|easdisc.log|记录 Exchange Server 连接器的活动和状态。|站点服务器|  

#### <a name="mobile-device-legacy"></a><a name="BKMK_MDLegLog"></a>移动设备旧客户端

下表列出的日志包含与移动设备旧客户端相关的信息。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|DmCertEnroll.log|记录有关移动设备旧客户端上的证书注册数据的详细信息。|客户端|  
|DMCertResp.htm|记录当移动设备旧客户端注册器程序请求 PKI 证书时来自证书服务器的 HTML 响应。|客户端|  
|DmClientHealth.log|记录与为移动设备启用的管理点通信的所有移动设备旧客户端的 GUID。|站点系统服务器|  
|DmClientRegistration.log|记录发送到移动设备旧客户端的注册请求以及来自移动设备旧客户端的响应。|站点系统服务器|  
|DmClientSetup.log|记录移动设备旧客户端的客户端安装数据。|客户端|  
|DmClientXfer.log|记录移动设备旧客户端和 ActiveSync 部署的客户端传输数据。|客户端|  
|DmCommonInstaller.log|记录用于配置移动设备旧客户端传输文件的客户端传输文件安装。|客户端|  
|DmInstaller.log|记录 DMInstaller 是否正确调用 DmClientSetup，以及 DmClientSetup 为移动设备旧客户端退出时是成功还是失败。|客户端|  
|DmpDatastore.log|记录为移动设备启用的管理点进行的所有站点数据库连接和查询。|站点系统服务器|  
|DmpDiscovery.log|记录为移动设备启用的管理点上的移动设备旧客户端中的所有发现数据。|站点系统服务器|  
|DmpHardware.log|记录为移动设备启用的管理点上的移动设备旧客户端中的硬件清单数据。|站点系统服务器|  
|DmpIsapi.log|记录移动设备旧客户端与为移动设备启用的管理点的通信。|站点系统服务器|  
|dmpmsi.log|记录针对移动设备启用的管理点配置的 Windows Installer 数据。|站点系统服务器|  
|DMPSetup.log|记录管理点的配置（如果为移动设备启用了管理点）。|站点系统服务器|  
|DmpSoftware.log|记录为移动设备启用的管理点上的移动设备旧客户端中的软件分发数据。|站点系统服务器|  
|DmpStatus.log|记录为移动设备启用的管理点上的移动设备客户端中的状态消息数据。|站点系统服务器|  
|DmSvc.log|记录移动设备旧客户端与为移动设备启用的管理点的客户端通信。|客户端|  
|FspIsapi.log|记录有关从移动设备旧客户端和客户端计算机到回退状态点的通信的详细信息。|站点系统服务器|  

### <a name="os-deployment"></a><a name="BKMK_OSDLog"></a> OS 部署

下表列出了包含与 OS 部署相关的信息的日志文件。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|CAS.log|在为引用的内容找到分发点时记录详细信息。|客户端|  
|ccmsetup.log|记录客户端安装、客户端升级和客户端删除的 ccmsetup 任务。 可用于排除客户端安装问题。|客户端|  
|CreateTSMedia.log|记录任务序列媒体创建的详细信息。|运行 Configuration Manager 控制台的计算机|  
|Dism.log|记录脱机维护的驱动程序安装操作或更新应用操作。|站点系统服务器|  
|distmgr.log|记录有关为预启动执行环境 (PXE) 启用分发点的配置的详细信息。|站点系统服务器|  
|DriverCatalog.log|记录有关已导入到驱动程序目录的设备驱动程序的详细信息。|站点系统服务器|  
|mcsisapi.log|记录多播包传输和客户端请求响应的信息。|站点系统服务器|  
|mcsexec.log|记录运行状况检查、命名空间、会话创建和证书检查操作。|站点系统服务器|  
|mcsmgr.log|记录配置、安全模式和可用性的更改。|站点系统服务器|  
|mcsprv.log|记录多播提供程序与 Windows 部署服务 (WDS) 的交互。|站点系统服务器|  
|MCSSetup.log|记录有关多播服务器角色安装的详细信息。|站点系统服务器|  
|MCSMSI.log|记录有关多播服务器角色安装的详细信息。|站点系统服务器|  
|Mcsperf.log|记录有关多播性能计数器更新的详细信息。|站点系统服务器|  
|MP_ClientIDManager.log|记录管理点对任务序列从 PXE 或启动媒体中发起的客户端 ID 请求的响应。|站点系统服务器|  
|MP_DriverManager.log|记录管理点对“自动应用驱动程序”任务序列操作请求的响应。|站点系统服务器|  
|OfflineServicingMgr.log|记录针对操作系统 Windows 映像格式 (WIM) 文件的脱机维护计划和更新应用操作的详细信息。|站点系统服务器|  
|Setupact.log|记录有关 Windows Sysprep 和安装日志的详细信息。 有关详细信息，请参阅[日志文件](/windows/deployment/upgrade/log-files)。|客户端|  
|Setupapi.log|记录有关 Windows Sysprep 和安装日志的详细信息。|客户端|  
|Setuperr.log|记录有关 Windows Sysprep 和安装日志的详细信息。|客户端|  
|smpisapi.log|记录有关客户端状态捕获和还原操作的详细信息以及阈值信息。|客户端|  
|Smpmgr.log|记录有关状态迁移点运行状况检查结果和配置更改的详细信息。|站点系统服务器|  
|smpmsi.log|记录有关状态迁移点的安装和配置详细信息。|站点系统服务器|  
|smpperf.log|记录状态迁移点性能计数器更新。|站点系统服务器|  
|smspxe.log|记录有关使用 PXE 启动的客户端作出的响应的详细信息，以及有关启动映像和启动文件的扩展的详细信息。|站点系统服务器|  
|smssmpsetup.log|记录有关状态迁移点的安装和配置详细信息。|站点系统服务器|
| SMS_PhasedDeployment.log| 分阶段部署的日志文件|Configuration Manager 层次结构中的顶层站点|
|Smsts.log|记录任务序列活动。|客户端|  
|TSAgent.log|记录在启动任务序列之前的任务序列依赖项结果。|客户端|  
|TaskSequenceProvider.log|记录在导入、导出或编辑任务序列时有关任务序列的详细信息。|站点系统服务器|  
|loadstate.log|记录有关用户状态迁移工具 (USMT) 和还原用户状态数据的详细信息。|客户端|  
|scanstate.log|记录有关用户状态迁移工具 (USMT) 和捕获用户状态数据的详细信息。|客户端|  

### <a name="power-management"></a><a name="BKMK_PowerMgmtLog"></a>电源管理

下表列出了包含与电源管理相关的信息的日志文件。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|Pwrmgmt.log|记录有关客户端计算机上的电源管理活动的详细信息，包括电源管理客户端代理执行的监视活动和设置实施活动。|客户端|  

### <a name="remote-control"></a><a name="BKMK_RCLog"></a>远程控制

下表列出了包含与远程控制相关的信息的日志文件。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|CMRcViewer.log|记录有关远程控制查看者的活动的详细信息。|运行远程控制查看器的计算机上的 %temp% 文件夹中。|  

### <a name="reporting"></a><a name="BKMK_ReportLog"></a>报表

下表列出的 Configuration Manager 日志文件包含与报表相关的信息。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|srsrp.log|记录有关 Reporting Services 点的活动和状态的信息。|站点系统服务器|  
|srsrpMSI.log|记录来自 MSI 输出的 Reporting Services 点安装过程的详细结果。|站点系统服务器|  
|srsrpsetup.log|记录 Reporting Services 点安装过程的结果。|站点系统服务器|  

### <a name="role-based-administration"></a><a name="BKMK_RBALog"></a>基于角色的管理

下表列出了包含与管理基于角色的管理相关的信息的日志文件。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|hman.log|记录有关站点配置更改以及将站点信息发布到 Active Directory 域服务的信息。|站点服务器|  
|SMSProv.log|记录 WMI 提供程序对站点数据库的访问。|带有 SMS 提供程序的计算机|  

### <a name="software-metering"></a><a name="BKMK_MeteringLog"></a> 软件计数

下表列出了包含与软件计数相关的信息的日志文件。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|监视所有软件计数过程。|站点服务器|  

### <a name="software-updates"></a><a name="BKMK_SU_NAPLog"></a>软件更新

下表列出了包含有关软件更新信息的日志文件。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|AlternateHandler.log|在客户端调用 Office 即点即用 COM 接口以下载和安装 Microsoft 365 企业应用版客户端更新时，会记录详细信息。 它类似于在调用 Windows 更新代理 API 以下载和安装 Windows 更新时使用 WuaHandler。<!-- SCCMDocs#888 -->|客户端|
|Ccmperf.log|记录与数据维护和捕获（与客户端性能计数器相关）关联的活动。|客户端|
|DeltaDownload.log|记录有关使用传递优化下载的快速更新和更新的相关下载信息。|客户端|  
|PatchDownloader.log|记录有关从更新源将软件更新下载到站点服务器上的下载目的地的过程的详细信息。|手动下载更新时，此日志文件将位于运行控制台的计算机上运行控制台的用户的 %temp% 目录中。 对于自动部署规则，如果在站点服务器上安装了 ConfigMgr 客户端，则此日志文件将位于 %windir%\CCM\Logs 中的站点服务器上。|  
|PolicyEvaluator.log|记录有关客户端计算机上的策略评估的详细信息，其中包括来自软件更新的策略。|客户端|  
|RebootCoordinator.log|记录有关安装软件更新后在客户端计算机上协调系统重新启动的过程的详细信息。|客户端|  
|ScanAgent.log|记录有关软件更新的扫描请求、WSUS 位置和相关操作的详细信息。|客户端|  
|SdmAgent.log|记录有关对修正和符合性进行的跟踪的详细信息。 但是，软件更新日志文件 Updateshandler.log 可提供有关安装符合性所需的软件更新的更详细信息。 此日志文件与符合性设置共享。|客户端|  
|ServiceWindowManager.log|记录有关维护时段评估的详细信息。|客户端|
|SMS_ISVUPDATES_SYNCAGENT.log| 用于同步第三方软件更新的日志文件。| Configuration Manager 层次结构中的顶层软件更新点。|
|SMS_OrchestrationGroup.log| 业务流程组的日志文件|站点服务器|
|SmsWusHandler.log|记录有关 Microsoft 更新清单工具的扫描过程的详细信息。|客户端|  
|StateMessage.log|记录有关创建并发送到管理点的软件更新状态消息的详细信息。|客户端|  
|SUPSetup.log|记录有关软件更新点安装的详细信息。 当软件更新点安装完成后，会向此日志文件写入 **Installation was successful** 。|站点系统服务器|  
|UpdatesDeployment.log|记录有关客户端上的部署的详细信息，包括软件更新激活、评估和强制执行。 详细日志记录显示有关与客户端用户界面交互的其他信息。|客户端|  
|UpdatesHandler.log|记录有关软件更新符合性扫描以及在客户端上下载和安装软件更新的详细信息。|客户端|  
|UpdatesStore.log|记录有关在符合性扫描周期中接受评估的软件更新的符合性状态的详细信息。|客户端|  
|WCM.log|记录有关软件更新点配置的详细信息，以及有关连接到 WSUS 服务器的详细信息（以获取有关订阅的更新类别、分类和语言等信息）。|站点服务器|  
|WSUSCtrl.log|记录有关站点的配置、数据库连接和 WSUS 服务器健康状况的详细信息。|站点系统服务器|  
|wsyncmgr.log|记录有关软件更新同步过程的详细信息。|站点服务器|  
|WUAHandler.log|记录有关客户端上的搜索软件更新的 Windows 更新代理的详细信息。|客户端|  

### <a name="wake-on-lan"></a><a name="BKMK_WOLLog"></a> LAN 唤醒

下表列出了包含与使用 LAN 唤醒相关的信息的日志文件。  

> [!NOTE]  
> 使用唤醒代理对 LAN 唤醒进行补充时，会在客户端上记录此活动。 例如，请参阅本文的[客户端操作](#BKMK_ClientOpLogs)部分中的 CcmExec.log 和 SleepAgent_<*domain*\>@SYSTEM_0.log。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|wolcmgr.log|记录有关需要向哪些客户端发送唤醒数据包、发送的唤醒数据包的数量和重试唤醒数据包的次数的详细信息。|站点服务器|  
|wolmgr.log|包含有关唤醒过程的详细信息，例如何时唤醒为 LAN 唤醒配置的部署。|站点服务器|  

### <a name="windows-10-servicing"></a><a name="BKMK_WindowsServicingLog"></a> Windows 10 维护服务

下表列出了包含与 Windows 10 维护服务相关的信息的日志文件。  
服务使用与软件更新相同的基础结构和进程。 有关适用于服务方案的其他日志，请参阅[软件更新](#BKMK_SU_NAPLog)。

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|CBS.log|记录与 Windows 更新或角色和功能的更改相关的维护失败。|客户端|
|DISM.log|使用 DISM 记录所有操作。 如有必要，DISM.log 将指向 CBS.log 以提供更多详细信息。|客户端|
|setupact.log|在 Windows 安装过程中发生的大多数错误的主日志文件。 该日志文件位于 %windir%\$Windows.~BT\sources\panther 文件夹。|客户端|

有关详细信息，请参阅[在线服务相关的日志文件](/windows-hardware/manufacture/desktop/deployment-troubleshooting-and-log-files#online-servicing-related-log-files)。

### <a name="windows-update-agent"></a><a name="BKMK_WULog"></a> Windows 更新代理

下表列出了包含与 Windows 更新代理相关的信息的日志文件。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|WindowsUpdate.log|记录有关的详细信息，涉及到 Windows 更新代理何时连接到 WSUS 服务器并为符合性评估检索软件更新，以及代理组件是否有更新。|客户端|  

有关详细信息，请参阅 [Windows 更新日志文件](/windows/deployment/update/windows-update-logs)。

### <a name="wsus-server"></a><a name="BKMK_WSUSLog"></a> WSUS 服务器

下表列出了包含与 WSUS 服务器相关的信息的日志文件。  

|日志名称|说明|带有日志文件的计算机|  
|--------------|-----------------|----------------------------|  
|Change.log|记录有关已更改的 WSUS 服务器数据库信息的详细信息。|WSUS 服务器|  
|SoftwareDistribution.log|记录有关从已配置的更新源同步到 WSUS 服务器数据库的软件更新的详细信息。|WSUS 服务器|  

这些日志文件位于 `%ProgramFiles%\Update Services\LogFiles` 文件夹中。

## <a name="see-also"></a>另请参阅

- [关于日志文件](about-log-files.md)

- [支持中心 OneTrace](../../support/support-center-onetrace.md)

- [支持中心日志文件查看器](../../support/support-center.md#support-center-log-file-viewer)

- [CMTrace](../../support/cmtrace.md)