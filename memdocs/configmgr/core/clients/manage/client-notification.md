---
title: 客户端通知
titleSuffix: Configuration Manager
description: 通过立即从中央 Configuration Manager 控制台执行操作来管理客户端。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb8aac8-2bd9-4980-a25b-5f8d93051226
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7680c8f955773f169d56f36eb9bbe6507d2d7ce6
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2020
ms.locfileid: "83427823"
---
# <a name="client-notification-in-configuration-manager"></a>Configuration Manager 中的客户端通知

适用范围：Configuration Manager (Current Branch)

若要立即对远程客户端执行操作，请从 Configuration Manager 控制台发送客户端通知操作。 在单个设备或一组设备上启动这些操作。

## <a name="actions"></a>操作

以下操作位于功能区上的“主页”选项卡的“设备”或“集合”组中。

### <a name="install-client"></a>安装客户端

将打开“安装客户端向导”。 此向导使用客户端请求安装来安装 Configuration Manager 客户端。 有关详细信息，请参阅[客户端请求安装](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)。

#### <a name="permissions---install-client"></a>权限 - 安装客户端

此操作需要“集合”对象上的“修改资源”和“读取”权限  。

默认情况下，以下内置角色具有这些权限：

- 应用程序管理员  
- 完全权限管理员  
- 基础结构管理员  
- 操作管理员  
- OS Deployment Manager  

向所有需要推送客户端的自定义角色添加这些权限。

### <a name="run-script"></a>运行脚本

将打开“运行脚本”向导以在所有集合中的客户端上运行 PowerShell 脚本。 有关详细信息，请参阅[创建和运行 PowerShell 脚本](../../../apps/deploy-use/create-deploy-scripts.md)。

#### <a name="permissions---run-script"></a>权限 - 运行脚本

此操作需要“集合”对象上的“运行脚本”权限 。

默认情况下，以下内置角色具有此权限：

- 完全权限管理员  
- 基础结构管理员  
- 操作管理员  

向所有需要运行脚本的自定义角色添加此权限。

### <a name="start-cmpivot"></a>启动 CMPivot

启动 **CMPivot**，以便针对目标设备运行实时查询。 有关详细信息，请参阅 [CMPivot](../../servers/manage/cmpivot.md)。

#### <a name="permissions---start-cmpivot"></a>权限 - 启动 CMPivot

此操作需要具有与[运行脚本](#run-script)操作相同的权限。

自版本 1906 起，可以对集合对象使用“运行 CMPivot”权限。 

## <a name="client-notification"></a>客户端通知

以下操作位于“客户端通知”菜单下，此菜单位于功能区上的“主页”选项卡的“设备”或“集合”组中。

在 1806 版或更早版本中，“客户端通知”选项仅在“设备集合”节点中或在查看了“设备集合”的成员身份时显示。 从 1810 版开始，可以直接从“设备”节点启动“客户端通知” 。 不再要求必须在集合成员资格视图内。 <!--SCCMDocs-pr issue 2972-->

#### <a name="permissions---client-notification"></a>权限 - 客户端通知

<!--SCCMDocs-pr issue #2972-->
从 1810 版开始，客户端通知操作现在需要“集合”对象上的“通知资源”权限。 此权限适用于“客户端通知”菜单下的所有操作。

默认情况下，以下内置角色具有此权限：

- 完全权限管理员  
- 操作管理员  

向所有需要使用客户端通知操作的自定义角色添加此权限。

### <a name="download-computer-policy"></a>下载计算机策略

刷新设备策略。 有关详细信息，请参阅[启动 Configuration Manager 客户端的策略检索](manage-clients.md#BKMK_PolicyRetrieval)。  

### <a name="download-user-policy"></a>下载用户策略

刷新用户策略。  

### <a name="collect-discovery-data"></a>收集发现数据

触发客户端发送发现数据记录 (DDR)。 有关详细信息，请参阅[检测信号发现](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat)。  

### <a name="collect-software-inventory"></a>收集软件清单

触发客户端运行软件清单周期。 有关详细信息，请参阅[软件清单简介](inventory/introduction-to-software-inventory.md)。  

### <a name="collect-hardware-inventory"></a>收集硬件清单

触发客户端运行硬件清单周期。 有关详细信息，请参阅[硬件清单简介](inventory/introduction-to-hardware-inventory.md)。  

### <a name="evaluate-application-deployments"></a>评估应用程序部署

触发客户端运行应用程序部署评估周期。 有关详细信息，请参阅[计划部署的重新评估](../deploy/about-client-settings.md#schedule-re-evaluation-for-deployments)。  

### <a name="evaluate-software-update-deployments"></a>评估软件更新部署

触发客户端运行软件更新部署评估周期。 有关详细信息，请参阅[软件更新简介](../../../sum/understand/software-updates-introduction.md)。  

### <a name="switch-to-the-next-software-update-point"></a>切换到下一个软件更新点

触发客户端切换到下一个可用的软件更新点。 有关详细信息，请参阅[软件更新点切换](../../../sum/plan-design/plan-for-software-updates.md#BKMK_SUPSwitching)。  

### <a name="evaluate-device-health-attestation"></a>评估设备运行状况证明

触发 Windows 10 客户端检查和发送其最新的设备运行状况。 有关详细信息，请参阅[运行状况证明](../../servers/manage/health-attestation.md)。  

### <a name="wake-up"></a>唤醒

从版本 1810 开始，使用同一子网上的其他设备触发配置为支持使用 LAN 唤醒进行唤醒的设备，以发送 LAN 唤醒包。 有关详细信息，请参阅[如何配置 LAN 唤醒](../deploy/configure-wake-on-lan.md)。

### <a name="restart"></a>重启

触发选定设备重启。 有关详细信息，请参阅[重启客户端](manage-clients.md#restart-clients)。

## <a name="client-diagnostics"></a>客户端诊断
<!--4433455-->

从版本 1910 开始，Configuration Manager 控制台中提供了“客户端诊断”的新设备操作。 已添加以下操作：

- 启用详细日志记录：将 CCM 组件的全局日志级别更改为详细，并启用调试日志记录。
- 禁用详细日志记录：将全局日志级别更改为默认值，并禁用调试日志记录。
- 收集客户端日志（从 2002 开始）：向所选客户端发送客户端通知消息以收集 CCM 日志。 使用软件清单文件收集返回日志。 <!--4226618-->
   - 压缩客户端日志的大小限制为 100 MB。 <!--6366098-->
   - 使用[资源浏览器](inventory/use-resource-explorer-to-view-software-inventory.md#bkmk_diag)管理和查看这些文件。

   [![从控制台收集客户端日志](./media/4226618-collect-client-logs.png)](./media/4226618-collect-client-logs.png#lightbox)

> [!IMPORTANT]
> - 这些操作仅更改日志详细程度，而不会更改日志大小或历史记录。 越详细的日志记录可以生成越多的日志内容。
> - 管理点角色也使用 CCM 组件。 如果目标设备也是管理点，则此操作也适用于该角色。

有关这些设置的详细信息，请参阅[关于日志文件](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-client)。

在客户端上的 diagnostics.log 中跟踪任务的状态。 收集客户端日志时，其他信息会记录在管理点上的 MP_SinvCollFile.log 中以及站点服务器上的 sinvproc.log 中。

> [!Tip]
> 根据软件清单文件收集设置存储收集的客户端日志。 文件存储在站点服务器上的 Inboxes\sinv.box\FileCol 目录中。 版本数量没有限制。 [删除过期的已收集文件](../../servers/manage/reference-for-maintenance-tasks.md#delete-aged-collected-files)站点维护任务会按计划删除文件，默认为每 90 天一次。

### <a name="prerequisites---client-diagnostics"></a>先决条件 - 客户端诊断

- 将目标客户端更新到最新版本。

- Configuration Manager 管理用户需要“通知资源”权限。

  默认情况下，以下内置角色具有此权限：

  - 完全权限管理员  
  - 基础结构管理员  

  向所有需要使用客户端通知操作的自定义角色添加此权限。


## <a name="endpoint-protection"></a>Endpoint Protection

以下操作位于“Endpoint Protection”菜单下。 此菜单位于功能区上的“主页”选项卡的“集合”组中。当选择一个或多个设备时，这些操作位于功能区的“选定对象”选项卡上。

有关详细信息，请参阅 [Configuration Manager 中的 Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)。

### <a name="permissions---endpoint-protection"></a>权限 - Endpoint Protection

此操作需要“集合”对象上的“强制安全性”权限 。

默认情况下，以下内置角色具有此权限：

- 完全权限管理员  
- Endpoint Protection 管理员  
- 操作管理员  

向所有需要触发 Endpoint Protection 操作的自定义角色添加此权限。

### <a name="full-scan"></a>完整扫描

触发 Endpoint Protection 或 Windows Defender 运行*完整*反恶意软件扫描。  

### <a name="quick-scan"></a>快速扫描

触发 Endpoint Protection 或 Windows Defender 运行*快速*反恶意软件扫描。  

### <a name="download-definition"></a>下载定义

触发 Endpoint Protection 或 Windows Defender 下载最新的反恶意软件定义。  

## <a name="see-also"></a>另请参阅

- [如何管理客户端](manage-clients.md)
- [如何管理集合](collections/manage-collections.md)
