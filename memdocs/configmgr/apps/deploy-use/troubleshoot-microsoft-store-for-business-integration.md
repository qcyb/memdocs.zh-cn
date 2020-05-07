---
title: MSfB 集成故障排除
titleSuffix: Configuration Manager
description: 提供建议和解决方案，以排查适用于企业和教育的 Microsoft Store 集成中的一些最常见的问题。
ms.date: 04/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 09929057-ecf2-4d49-aee0-709916932b14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 694083bbce34b9e1b62f77a1d18cf79663704b2a
ms.sourcegitcommit: af8a3efd361a7f3fa6e98e5126dfb1391966ff76
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2020
ms.locfileid: "82149089"
---
# <a name="troubleshoot-the-microsoft-store-for-business-and-education-integration-with-configuration-manager"></a>排查适用于企业和教育的 Microsoft Store 与 Configuration Manager 的集成问题

本文提供了一些关键的排除故障提示和修复方法，它们可用来处理你在适用于企业和教育的 Microsoft Store 与 Configuration Manager 的集成方面可能遇到的一些主要问题。

要详细了解如何将适用于企业和教育的 Microsoft Store 与 Configuration Manager 结合使用，请参阅[使用 Configuration Manager 来管理适用于企业和教育的 Microsoft Store 中的应用](manage-apps-from-the-windows-store-for-business.md)。

## <a name="monitor"></a>监视

### <a name="component-status"></a>组件状态

在 Configuration Manager 控制台中，转到“监视”工作区，展开“系统状态”，然后选择“组件状态”节点    。 监视下列组件的状态：

- SMS_BUSINESS_APP_PROCESS_MANAGER
- SMS_CLOUDCONNECTION

### <a name="sync-status"></a>同步状态

在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“适用于企业的 Microsoft Store”节点    。 查看“上次同步状态”列  。

### <a name="view-synchronized-apps"></a>查看同步的应用

在 Configuration Manager 控制台中，转到“软件库”工作区中，展开“应用程序管理”，然后选择“应用商店应用的许可证信息”节点    。


## <a name="log-files"></a>日志文件

### <a name="wsfbsyncworkerlog"></a>WSfBSyncWorker.log

此日志文件位于服务连接点上，在 Configuration Manager 安装目录的 `\Logs` 下。 它记录了与云服务通信的相关信息。 此信息包括元数据、图标、包和许可证文件检索结果。

要更改日志级别，请将 `HKLM\SOFTWARE\Microsoft\SMS\Tracing\SMS_CLOUDCONNECTION` 注册表项中的 `LoggingLevel` 值更改为 `0`。 有关详细信息，请参阅[配置日志记录选项](../../core/plan-design/hierarchy/about-log-files.md#bkmk_reg-site)。

### <a name="sms_cloudconnectionlog"></a>SMS_CLOUDCONNECTION.log

此日志文件位于服务连接点上，在 Configuration Manager 安装目录的 `\Logs` 下。 如果 WSfBSyncWorker 服务未启动或重复启动和停止，请查看此日志文件中的条目。

> [!NOTE]
> 此日志文件与其他功能共享。

### <a name="businessappprocessworkerlog"></a>BusinessAppProcessWorker.log

此日志文件位于层次结构中顶级站点的站点服务器上。 它在 Configuration Manager 安装目录的 `\Logs` 下。 它记录了下列过程的相关信息：

- 将 BusinessAppProcessWorker 组件同步的元数据信息插入数据库
- 处理 `\InstallDir\inboxes\businessappprocess.box` 中的文件

### <a name="sms_business_app_process_managerlog"></a>SMS_BUSINESS_APP_PROCESS_MANAGER.log

此日志文件位于层次结构中顶级站点的站点服务器上。 它在 Configuration Manager 安装目录的 `\Logs` 下。 如果 BusinessAppProcessWorker 服务未启动或重复启动和停止，请查看此日志文件中的条目。



## <a name="last-sync-failed"></a>上次同步失败

当上次同步状态为“失败”时，请先查看以下[日志文件](#log-files)来确定故障表现  ：

- WSfbSyncWorker.log
- SMS_CLOUDCONNECTION.log

如果是常见问题，则接下来查看下列部分之一：

- [授权错误](#bkmk_fail-symptom1)
- [密钥无效](#bkmk_fail-symptom2)
- [获取应用程序令牌时出错](#bkmk_fail-symptom3)
- [内容位置不存在或权限不正确](#bkmk_fail-symptom4)
- [发出调用“GET”方法的 http 请求时出错](#bkmk_fail-symptom5)
- [无法将更多字节写入缓冲区](#bkmk_fail-symptom6)

### <a name="authorization-error"></a><a name="bkmk_fail-symptom1"></a> 授权错误

#### <a name="cause"></a>原因

如果配置的 Azure Active Directory (Azure AD) 应用程序无权为该租户管理适用于企业和教育的 Microsoft Store，则会出现此问题。

#### <a name="workaround"></a>解决方法

1. 以管理员身份登录适用于企业或教育的 Microsoft Store 门户。
1. 转到“设置”，然后选择“管理工具”   。
1. 如果未列出应用程序，请选择“添加管理工具”  。 然后按名称搜索，再选择与 Configuration Manager 具有相同 ClientID 关联的 Azure AD 应用程序。
1. 如果状态未显示“活动”，则在“操作”部分中选择“激活”    。
1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“适用于企业的 Microsoft Store”节点    。 与存储同步，或等待出现下一个同步间隔。

> [!Tip]
> 若要在 Configuration Manager 中查找 ClientID：
>
> 1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure Active Directory 租户”节点    。
> 1. 选择要对适用于企业和教育的 Microsoft Store 集成使用的租户。
> 1. 在“结果”窗格中，找到匹配的应用程序，并查看“客户端 ID”列  。

### <a name="the-secret-key-is-invalid"></a><a name="bkmk_fail-symptom2"></a>密钥无效

#### <a name="cause"></a>原因

如果在 Azure AD 应用上，适用于企业和教育的 Microsoft Store 配置的密钥过期，则会出现此问题。

#### <a name="resolution"></a>解决方法

续订 Azure AD 应用程序的密钥。 有关详细信息，请参阅[续订密钥](../../core/servers/deploy/configure/azure-services-wizard.md#bkmk_renew)。

### <a name="error-getting-application-token"></a><a name="bkmk_fail-symptom3"></a>获取应用程序令牌时出错

#### <a name="cause"></a>原因

如果连接的应用在 Azure AD 中不复存在，则会出现此问题。

#### <a name="resolution"></a>解决方法

删除再重新创建与适用于企业和教育的 Microsoft Store 的连接。

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“适用于企业的 Microsoft Store”节点    。
1. 选择现有连接。
1. 在功能区中，选择“删除”  。

然后重新创建连接。 有关详细信息，请参阅下列文章：

- [配置 Azure 服务](../../core/servers/deploy/configure/azure-services-wizard.md)
- [设置适用于企业和教育的 Microsoft Store 同步](manage-apps-from-the-windows-store-for-business.md#bkmk_setup)

### <a name="content-location-doesnt-exist-or-incorrect-permissions"></a><a name="bkmk_fail-symptom4"></a> 内容位置不存在或权限不正确

#### <a name="cause"></a>原因

设置适用于企业和教育的 Microsoft Store 连接时，请指定用于存储同步内容的网络共享。 如果此共享不存在或权限不正确，则会出现此问题。 服务连接点的计算机帐户应是此目录及任何子目录的所有者。<!-- memdocs#146 --> 如果不是，则你将看到如下所示的错误：

```
Failed to download package d788cc1b-ab00-bb5f-1548-f2dfe717583b-X86-Arm for product 9WZDNCRFJ3PS\0015.
System.IO.IOException: This security ID may not be assigned as the owner of this object.
```

若要查看配置的位置：

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“适用于企业的 Microsoft Store”节点    。

1. 选择帐户并打开“属性”  。

1. 切换到“配置”选项卡  。“位置”设置会显示从适用于企业和教育的 Microsoft Store 下载的应用程序内容的网络存储路径  。

#### <a name="workaround"></a>解决方法

1. 如果该共享不存在，则创建它。

1. 检查文件夹上的 NTFS 权限以及网络共享上的权限。 向服务连接点的计算机帐户授予“读取”和“写入”权限   。

如果要重新配置位置，请删除现有连接，再重新创建与新的内容位置的连接。

### <a name="error-occurred-making-http-request-calling-get-method"></a><a name="bkmk_fail-symptom5"></a>发出调用“GET”方法的 http 请求时出错

#### <a name="cause"></a>原因

如果来自应用商店的应用程序的同步所耗时间太长，以致于内容 URL 已过期，则会出现此问题。

#### <a name="workaround"></a>解决方法

重试同步过程

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“适用于企业的 Microsoft Store”节点    。
1. 选择连接。 在功能区中，选择“从适用于企业的 Microsoft Store 同步”  。

每次都会继续同步。 根据以下因素，可能需要重试多次：

- 脱机应用程序的数量
- 包的大小
- 网络速度

每次尝试后，看到错误的次数会更少。 如果错误数不减少，则表示还有一个问题。

### <a name="cannot-write-more-bytes-to-the-buffer"></a><a name="bkmk_fail-symptom6"></a>无法将更多字节写入缓冲区

#### <a name="cause"></a>原因

如果应用程序的包大于 500 MB，则会出现此问题。 Configuration Manager 仅支持自动同步包小于 500 MB 的脱机应用程序。

#### <a name="workaround"></a>解决方法

无法自动同步这些应用，但可下载内容并手动创建应用程序：

1. 从 WSfbSynWorker.log 中的以下行获取失败的应用程序 ID  ：

    `Error(s) syncing or downloading application <ApplicationID> from the Microsoft Store for Business.`

1. 以管理员身份登录适用于企业或教育的 Microsoft Store 门户。 查找此应用程序的页面。

    > [!Tip]
    > 页面的 URL 类似于：`https://businessstore.microsoft.com/en-us/store/p/app/ApplicationID`

    1. 如果尚未选择“脱机”，请选择它  。 然后选择“管理”  。

    1. 在应用程序内容共享上，为所有支持的平台创建单独的文件夹。

    1. 将包下载到该包文件夹中。

    1. 将编码的许可证文件作为 `.bin` 文件下载到该包文件夹中。

    1. 将所有必需框架下载到该包文件夹中。

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“应用程序管理”，然后选择“应用程序”节点    。

1. [创建应用程序](create-applications.md)，手动指定应用程序信息。

    1. 为之前下载的每个受支持的平台创建一个部署类型。

    1. 类型：**Windows 应用包（\*.appx、\*.appxbundle）**

    1. 为实际应用包（而非所需的依赖项包）指定 appx/appxbundle。

在最后的“导入信息”页面上，确认以下详细信息  ：

- **许可证文件：** 指定 `.bin` 文件。 脱机应用需要此许可证文件。
- **Windows 应用依赖项：** 验证是否已下载此包所需的全部依赖项。


## <a name="sync-doesnt-run"></a>同步不运行

本部分涵盖了下列同步问题：

- 你手动启动了同步进程，但它不运行
- 网站不会每天都自动同步

请先查看以下[日志文件](#log-files)来确定故障表现：

- BusinessAppProcessWorker.log
- SMS_BUSINESS_APP_PROCESS_MANAGER.log
- WsfbSyncWorker.log
- SMS_CLOUDCONNECTION.log

如果是常见问题，则接下来查看下列部分之一：

- [手动同步未启动](#bkmk_sync-symptom1)
- [无法运行每日自动同步，SMS-BUSINESS-APP-PROCESS-MANAGER.log 中出现“正在关闭 # 个辅助角色”错误](#bkmk_sync-symptom2)

### <a name="manual-sync-doesnt-start"></a><a name="bkmk_sync-symptom1"></a>手动同步未启动

#### <a name="cause"></a>原因

如果在上次同步后 10 分钟内开始同步，则会出现此问题。同步频率最大是每 10 分钟一次。

#### <a name="resolution"></a>解决方法

请等待至少 10 分钟，然后再开始新的同步。

### <a name="automatic-daily-sync-doesnt-run-and-shutting-down--workers-error-in-sms_business_app_process_managerlog"></a><a name="bkmk_sync-symptom2"></a>无法运行每日自动同步，SMS-BUSINESS-APP-PROCESS-MANAGER.log 中出现“正在关闭 # 个辅助角色”错误

#### <a name="cause"></a>原因

如果 SMS_BUSINESS_APP_PROCESS_MANAGER 组件停止 WsfbSyncWorker 线程，则会出现此问题。 该错误可能导致指定了 `2` 或 `4` 个辅助角色。

#### <a name="workaround"></a>解决方法

重新启动 SMS_EXECUTIVE 服务  。

如果无法重启主服务，请使用 MSfB 辅助角色停止这两个组件，然后再启动它们：

1. 在运行服务连接点的服务器上打开 Windows 注册表

1. 转到 `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_CLOUDCONNECTION`

    1. 将请求的操作设置为“停止”  。

    1. 刷新以验证当前状态是否为“已停止”  。

1. 转到 `HKLM\SOFTWARE\Microsoft\SMS\COMPONENTS\SMS_EXECUTIVE\Threads\SMS_BUSINESS_APP_PROCESS_MANAGER`

    1. 将请求的操作设置为“停止”  。

    1. 刷新以验证当前状态是否为“已停止”  。

1. 在 SMS_CLOUDCONNECTION 中，将“请求的操作”设置为“开始”   。

1. 在 SMS_BUSINESS_APP_PROCESS_MANAGER 中，将“请求的操作”设置为“开始”   。


## <a name="language-related-issues"></a>与语言相关的问题

本部分涵盖了以下常见问题：

- [未应用对语言选择的更改](#bkmk_lang-symptom1)
- [并非所有许可证信息都用所有选定语言显示](#bkmk_lang-symptom2)

### <a name="language-selection-changes-arent-applied"></a><a name="bkmk_lang-symptom1"></a>未应用对语言选择的更改

#### <a name="cause"></a>原因

如果缓存了语言选择，并且在更改属性值后未清除所作选择，则会出现此问题。

#### <a name="workaround"></a>解决方法

要解决此问题，请重启 SMS_Executive 服务  。

### <a name="not-all-selected-languages-are-present-for-all-license-information"></a><a name="bkmk_lang-symptom2"></a>并非所有许可证信息都用所有选定语言显示

#### <a name="cause"></a>原因

如果适用于企业和教育的 Microsoft Store 应用程序的许可证信息不包含指定语言的本地化数据，则会出现此问题。

#### <a name="workaround"></a>解决方法

为创建的应用程序手动添加所有缺少的语言。


## <a name="offline-applications"></a>脱机应用程序

本部分涵盖了以下常见问题：

- [无法验证内容，因此无法创建脱机应用程序](#bkmk_off-symptom1)
- [无法安装基于脱机许可证信息创建的应用程序](#bkmk_off-symptom2)

### <a name="fail-to-create-offline-application-because-content-cant-be-verified"></a><a name="bkmk_off-symptom1"></a>无法验证内容，因此无法创建脱机应用程序

#### <a name="cause"></a>原因

如果脱机应用程序的同步内容已损坏或已修改，则会出现此问题。

#### <a name="workaround"></a>解决方法

开始新的同步。同步完成后，应验证是否有内容文件出错，并下载相应的正确文件。

### <a name="fail-to-install-application-created-from-offline-license-information"></a><a name="bkmk_off-symptom2"></a>无法安装基于脱机许可证信息创建的应用程序

#### <a name="cause"></a>原因

如果将应用程序部署到运行早于版本 1511 的 Windows 10 版本的客户端，则会出现此问题。 只有在 Windows 10 版本 1511 及更高版本上才支持适用于企业和教育的 Microsoft Store 的脱机许可应用。

#### <a name="resolution"></a>解决方法

安装最新版的 Windows 10。


## <a name="next-steps"></a>后续步骤

要查找其他帮助，请参阅[查找有关使用 Configuration Manager 的帮助](../../core/understand/find-help.md)。
