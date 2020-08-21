---
title: 删除 CAS
titleSuffix: Configuration Manager
description: 删除管理中心站点 (CAS)，以便将 Configuration Manager 基础结构简化为单个独立主站点。
ms.date: 06/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 16975644-8dfa-4f22-b45a-c54a9250dbd2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5a1d9d4ce8cdd19efb440d4d73fafdc96a514bcd
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699154"
---
# <a name="remove-the-central-administration-site"></a>删除管理中心站点

适用范围：Configuration Manager (Current Branch)

<!-- 3607277 -->

从版本 2002 开始，如果层次结构由管理中心站点 (CAS) 和单个子级主站点组成，则可以删除 CAS。 此操作可将 Configuration Manager 基础结构简化为单个独立主站点。 它可消除站点到站点复制的复杂性，并将管理任务集中到单个站点。

> [!IMPORTANT]
> 在此版本的 Configuration Manager 中，此功能是预发行版，默认情况下未启用。 此功能当前可供 Microsoft 顶级支持客户使用。
>
> 若要启用此功能，请与技术客户经理联系以获得帮助：
>
> - TAM 会建立一个咨询案例，它将使用你的 Microsoft 顶级支持时数。
> - 无法更改案例严重性。
> - Microsoft 支持部门会在正常工作日营业时间内帮助为这些咨询案例提供帮助。

## <a name="plan"></a>计划

- 层次结构需要由 CAS 和单个子级主站点组成。 主站点可以具有辅助站点。 若要从层次结构中删除其他子级主站点，请查看[卸载主站点](uninstall-sites-and-hierarchies.md#bkmk_primary)的规划步骤和先决条件。

- 请确保子级主站点满足[独立主站点](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_pri)的大小和规模要求。

- 在 CAS 上移动或停用任何站点角色，服务连接点和软件更新点除外。 删除 CAS 时，Configuration Manager 安装程序会处理这两个角色。

  以下角色在 CAS 上最常见，需要停用或移动到主站点：

  - 资产智能同步点
  - Endpoint Protection 点
  - Reporting Services 点
  - 数据仓库服务点
  - 云管理网关 (CMG)

    > [!NOTE]
    > 如果已为内容启用 CMG，则计划在主站点上重新创建 CMG 之后重新分发内容。<!-- 6608659 -->

- 关闭分布式视图

- Configuration Manager 会自动处理内置包（如 Configuration Manager 客户端）的包源位置。 查看所有其他内容源位置，以确保它们不使用 CAS 上的共享。

- 停止任何活动迁移作业，并删除迁移的所有配置。 有关详细信息，请参阅[停止从另一个层次结构进行活动迁移](prerequisites-for-installing-sites.md#stop-active-migration-from-another-hierarchy)。

- 如果对软件更新使用自动部署规则，请在子级主站点上重新创建它们。

- 如果使用 Configuration Manager 或 System Center Updates Publisher 管理[第三方软件更新](../../../../sum/deploy-use/third-party-software-updates.md)，请从 CAS 上的软件更新点导出 WSUS 签名证书。

  - 删除 CAS 之前，等待任何必需的第三方软件更新部署的最后期限。 客户端会预下载必需部署的内容，更改软件更新点时，内容哈希会随软件更新的本地发布而更改。 （此行为不会影响其他内容类型，只影响第三方软件更新进行本地发布。）如果在这些必需部署仍在进行时删除 CAS，则它们会在客户端上失败，并出现哈希不匹配错误。

- 检查可能依赖于 CAS 的任何第三方软件。

## <a name="prerequisites"></a>必备条件

- 运行 Configuration Manager 安装程序的管理用户需要以下安全权限：

  - CAS 服务器上的本地“管理员”权限

  - 如果 CAS 数据库服务器是站点服务器的远程服务器，则为 CAS 的远程站点数据库服务器上的本地“管理员”权限。

  - CAS 站点数据库上的 Sysadmin 权限

  - 主站点服务器上的本地“管理员”权限

  - 如果主站点数据库服务器是主站点服务器的远程服务器，则为主站点的远程站点数据库服务器上的本地“管理员”权限。

  - 主站点数据库上的 Sysadmin 权限

  - CAS 和主站点上的“基础结构管理员”或“完全权限管理员”安全角色

- 层次结构中只有一个子级主站点。 有关详细信息，请参阅[卸载主站点](uninstall-sites-and-hierarchies.md#bkmk_primary)。

## <a name="process"></a>过程

1. 使用以下方法之一在 CAS 服务器上启动 Configuration Manager 安装程序：

    - 在“开始”菜单上，选择“Configuration Manager 安装程序”。

    - 在 Configuration Manager 安装介质的目录中，打开 `\SMSSETUP\BIN\X64\setup.exe`。 确保此版本与站点版本相同。

    - 在安装 Configuration Manager 的目录中，打开 `\BIN\X64\setup.exe`。

1. 查看“准备工作”页上的信息。

1. 在“开始使用”页上，选择“执行站点维护或重置此站点”。

1. 在“站点维护”页上，选择“删除管理中心站点”。 <!-- or is it still "delete"? -->

1. 在“重新配置现有站点系统角色”页上：

    - 服务连接点：输入主站点中的站点系统的完全限定域名，以托管此必需角色。 有关详细信息，请参阅[关于服务连接点](../configure/about-the-service-connection-point.md)。

    - 软件更新点：选择主站点中的现有软件更新点。 安装程序会将此软件更新点配置为与 CAS 配置同步。

    安装程序会检查指定服务器是否满足先决条件。 准备好继续时，选择“开始安装”。

如果安装程序出现问题，请使用向导重试该过程。

安装完成后，它会重置主站点。 有关详细信息，请参阅[运行站点重置](../../manage/modify-your-infrastructure.md#bkmk_reset)。

## <a name="monitor-and-verify"></a>监视和验证

在安装过程中查看以下日志：

- CAS 服务器上的 `C:\ConfigMgrSetup.log`

- 主站点服务器上的 Configuration Manager 日志目录中的 hman.log

使用“监视”工作区中的“站点层次结构”节点可直观显示层次结构的更改。 例如，下图显示了 SHY CAS、HAW 主站点和 VWT 辅助站点的事前与事后比较：

| 以前  | 完成   |
|---------|---------|
|![CAS、主站点和辅助站点的示例站点层次结构视图](media/3607277-cas-primary-secondary.png)|![主站点和辅助站点的示例站点层次结构视图](media/3607277-primary-secondary.png)|

## <a name="post-setup-tasks"></a>安装后任务

删除 CAS 之后，请查看适用于你的环境的以下步骤。

- 从主站点本地组中手动删除 CAS 服务器计算机帐户。

- 受信任的根密钥已更改，这可能需要执行其他操作：

  - 更新 OS 部署启动映像以包含最新 Configuration Manager 二进制文件。

  - 重新创建 [OS 部署介质](../../../../osd/deploy-use/create-task-sequence-media.md)。

- 如果将 Configuration Manager 与 [Azure Monitor](/azure/azure-monitor/platform/collect-sccm?context=/mem/configmgr/core/context/core-context) 连接，则需要重置连接。 解决任何问题的第一步是[续订密钥](../configure/azure-services-wizard.md#bkmk_renew)。 如果这无法解决问题，请重新创建连接。<!-- 5584635 -->

- 在版本 2002 中，如果启用了 Surface 驱动程序的同步，请在删除 CAS 之后重新配置此功能。 有关详细信息，请参阅 [Microsoft Surface 驱动程序和固件更新](../../../../sum/deploy-use/surface-drivers.md)。<!-- 5728727 -->

- 如果管理第三方软件更新：

  1. 从 CAS 上的软件更新点导出 WSUS 签名证书（如果尚未这样做）。

  1. 创建新部署之前，从任何现有部署和软件更新包中删除更新。

  1. 若要将软件更新元数据恢复为可用状态，请重新同步订阅的目录。 还可以等待 Configuration Manager 自动重新同步。

  1. 启动或等待正常软件更新同步过程，以使用 WSUS 中的当前状态更新 Configuration Manager。 （可选）使用 SCUP 或 WSUS PowerShell cmdlet 删除和重新添加更新。

  1. 为需要部署的更新重新发布内容。