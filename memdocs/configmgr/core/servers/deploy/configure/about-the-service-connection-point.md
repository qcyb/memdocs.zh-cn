---
title: 服务连接点
titleSuffix: Configuration Manager
description: 了解此 Configuration Manager 站点系统角色，并了解和规划其使用范围。
ms.date: 01/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d167ea14537d88c31ca3930614fc24d8ebc92a02
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704945"
---
# <a name="about-the-service-connection-point-in-configuration-manager"></a>关于 Configuration Manager 中的服务连接点

适用范围：  Configuration Manager (Current Branch)

服务连接点是一个站点系统角色，为层次结构提供几个重要的功能。 设置服务连接点之前，需了解和规划它的使用范围。 规划使用可能会影响设置此站点系统角色的方式：

- 下载适用于 Configuration Manager 基础结构的更新。 基于所上传的使用情况数据，仅适用于基础结构的相关更新可用。

- 从 Configuration Manager 基础结构上传使用情况数据。 可以控制上传的详细信息的级别或数量。 有关详细信息，请参阅[使用情况数据级别和设置](../install/setup-reference.md#bkmk_usage)。

- 在 Azure 中部署[云管理网关](../../../clients/manage/cmg/plan-cloud-management-gateway.md)

- 同步[适用于企业和教育的 Microsoft Store](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) 中的应用

- 发现 [Azure Active Directory (Azure AD)](about-discovery-methods.md#azureaddisc) 中的用户和组

- 使用[桌面分析](../../../../desktop-analytics/overview.md)来深入了解 Windows 10 的更新和应用准备情况

每个层次结构支持此角色的单一实例。 它只能安装在层次结构的顶层站点上，即管理中心站点 (CAS) 或独立主站点。 如果将独立主站点扩展到更大的层次结构中，请从主站点中卸载此角色，然后可将其安装在 CAS 上。

## <a name="modes-of-operation"></a><a name="bkmk_modes"></a>操作模式

服务连接点支持两种操作模式：

- **联机**：服务连接点每 24 小时自动检查一次是否有更新。 它会自动下载可用于当前基础结构和产品版本的更新，使其在 Configuration Manager 控制台中可用。

- **脱机**：服务连接点不会连接到 Microsoft 云服务。 要手动导入可用更新，请使用[服务连接工具](../../manage/use-the-service-connection-tool.md)。

### <a name="change-mode"></a>更改模式

安装了服务连接点之后，如果在联机模式或脱机模式之间切换，请重新启动 SMS_Executive 服务的 SMS_DMP_DOWNLOADER 线程  。 重新启动此线程会使更改生效。 若要重新启动此线程，请使用 Configuration Manager 服务管理器。

> [!TIP]
> 也可以重新启动 Configuration Manager 的 SMS_Executive 服务，从而重新启动大多数站点组件。 或者也可以等待计划任务（如站点备份）停止，然后为你重新启动 SMS_Executive 服务。

要使用 Configuration Manager 服务管理器重新启动 SMS_DMP_DOWNLOADER 线程，请执行以下操作：

1. 在 Configuration Manager 控制台中，转到“监视”工作区，展开“系统状态”，然后选择“组件状态”节点    。 在功能区中，选择“启动”，然后选择“Configuration Manager 服务管理器”   。

1. 在服务管理器导航窗格中，依次展开站点和“组件”，然后选择要重新启动的组件  ：**SMS_DMP_DOWNLOADER**。

1. 转到“组件”菜单，选择“查询”   。

1. 确认组件的当前状态。 然后转到“组件”菜单，选择“停止”   。  

1. 单击“查询”，再次查询组件，确认它已停止  。 然后选择“启动”组件操作以重新启动它  。

## <a name="remote-site-system-requirements"></a>远程站点系统要求

在远离站点服务器的站点系统服务器上安装服务连接点时，请配置以下要求：

- 站点服务器的计算机帐户必须是承载远程服务连接点的计算机上的本地管理员。

- 设置站点系统服务器，用于承载具有[站点系统安装帐户](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)的角色。 站点服务器上的分发管理器使用该站点系统安装帐户来传输服务连接点的更新。

## <a name="internet-access-requirements"></a><a name="bkmk_urls"></a> Internet 访问要求

如果你的组织使用防火墙或代理设备限制与 Internet 的网络通信，则需要允许服务连接点访问 Internet 终结点。

有关详细信息，请参阅 [Internet 访问要求](../../../plan-design/network/internet-endpoints.md#bkmk_scp)。

## <a name="install"></a>安装

运行“安装程序”以安装层次结构的顶层站点时，可以安装服务连接点  。

在安装程序运行后，或者若要重新安装该角色，请使用“添加站点系统角色”向导或“创建站点系统服务器”向导   。 （在层次结构顶层站点上安装服务连接点。）有关详细信息，请参阅[安装站点系统角色](install-site-system-roles.md)。

## <a name="move-the-role"></a><a name="bkmk_move"></a> 移动角色

<!-- SCCMDocs#922 -->
在以下几种情况下，你可能需要将服务连接点移动到另一台服务器上：

- [恢复](../../manage/recover-sites.md)
- [站点服务器高可用性](site-server-high-availability.md)
- [站点扩展](../install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)

在移动服务连接点后，请选中“所有站点功能”。 例如，你可能需要续订 Azure Active Directory (Azure AD) 租户的任何连接的机密密钥。 有关详细信息，请参阅[续订密钥](azure-services-wizard.md#bkmk_renew)。

## <a name="log-files"></a>日志文件

若要查看有关 Microsoft 上传的信息，请参阅运行服务连接点的服务器上的 Dmpuploader.log  。 如需了解更新的下载进度，请查看 Dmpdownloader.log  。 有关与服务连接点相关的日志的完整列表，请参阅[日志文件 - 服务连接点](../../../plan-design/hierarchy/log-files.md#BKMK_WITLog)。

## <a name="next-steps"></a>后续步骤

使用以下流程图了解处理流和密钥日志条目。 此过程包括下载更新并将更新复制到其他站点。

- [流程图 - 下载更新](../../manage/download-updates-flowchart.md)

- [流程图 - 更新复制](../../manage/update-replication-flowchart.md)
