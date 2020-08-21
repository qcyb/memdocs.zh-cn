---
title: 站点的先决条件
titleSuffix: Configuration Manager
description: 了解安装不同类型的 Configuration Manager 站点所需的先决条件。
ms.date: 07/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: bf9ad15266c4e6615ba100d5ea5270e23b93ece7
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699120"
---
# <a name="prerequisites-for-installing-configuration-manager-sites"></a>安装 Configuration Manager 站点的先决条件

适用范围：Configuration Manager (Current Branch)

在开始站点安装之前，先了解安装不同类型的 Configuration Manager 站点的先决条件。


## <a name="primary-sites-and-the-central-administration-site"></a>主站点和管理中心站点

以下先决条件适用于安装以下类型之一：

- 管理中心站点作为层次结构的第一个站点
- 独立主站点
- 子主站点

如果在层次结构扩展期间安装管理中心站点，请参阅[扩展独立主站点](#bkmk_expand)。

### <a name="prerequisites-for-installing-a-primary-site-or-a-central-administration-site"></a><a name="bkmk_PrereqPri"></a>安装主站点或管理中心站点的先决条件  

- 必须安装必要的 Windows Server 角色、功能和 Windows 组件。 有关详细信息，请参阅[站点系统先决条件](../../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012sspreq)  

- 安装站点的用户帐户必须具有以下权限：  

    - 下列服务器上的管理员权限：  
        - 站点服务器  
        - 托管站点数据库的每个服务器  
        - 站点的每个 SMS 提供程序实例  

    - 托管站点数据库的 SQL Server 实例上的 **Sysadmin**  

        > [!IMPORTANT]  
        > Configuration Manager 安装完成后，站点服务器计算机帐户必须保留对 SQL Server 的 sysadmin 权限。 请勿从此帐户中删除 SQL sysadmin 权限。  

    > [!NOTE]
    > 若要详细了解在安装完成后是否需要这些权限，请参阅[提升的权限](../../../plan-design/hierarchy/accounts.md#elevated-permissions)。

- 如果安装的是主站点，则需要下列附加权限：  

    - 安装初始管理点和分发点的其他服务器上的管理员权限（若不在站点服务器上）  

- 如果在管理中心站点下安装新的子级主站点，需要下列附加权限：  

    - 托管管理中心站点的服务器上的管理员权限  

    - Configuration Manager 中基于角色的管理权限，这些权限相当于**基础结构管理员**或**完全权限管理员**的安全角色  

- 使用正确的安装源文件，并从该位置运行安装程序。 若要了解用于安装不同站点类型的适当源文件，请参阅[不同类型站点的安装选项](prepare-to-install-sites.md#bkmk_options)。  

- 站点服务器必须可通过以下某种方式访问更新的 Microsoft 安装程序文件：  

    - 开始安装前，可在本地网络上下载这些文件并存储其副本。 有关详细信息，请参阅[安装程序下载程序](setup-downloader.md)。  

    - 如果这些文件的本地副本不可用，则站点服务器必须具有 Internet 访问权限。 它在安装过程中从 Microsoft 下载这些文件。  

- 站点服务器和站点数据库服务器必须满足所有先决条件配置。 在启动 Configuration Manager 安装程序之前，可[手动运行必备组件检查程序](prerequisite-checker.md)以识别并修复问题。  

### <a name="prerequisites-to-expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> 扩展独立主站点的先决条件

在你将独立主站点扩展到带管理中心站点的层次结构之前，独立主站点必须满足下列先决条件：

#### <a name="source-file-version-matches-site-version"></a>源文件版本与站点版本匹配

使用 CD.Latest 文件夹中的介质安装与独立主站点的版本匹配的新管理中心站点。 要确保版本匹配，请使用在独立主站点上的 [CD.Latest 文件夹](../../manage/the-cd.latest-folder.md)中找到的源文件。

若要深入了解用于安装不同站点的适当源文件，请参阅[不同类型站点的安装选项](prepare-to-install-sites.md#bkmk_options)。  

#### <a name="stop-active-migration-from-another-hierarchy"></a>停止从另一个层次结构进行活动迁移

无法将独立主站点配置为从另一 Configuration Manager 层次结构迁移数据。 停止从其他 Configuration Manager 层次结构活动迁移到独立主站点，并删除迁移的所有配置。 这些配置包括：

- 尚未完成的迁移作业  
- 数据收集  
- 活动源层次结构的配置  

此配置是必需的，因为 Configuration Manager 从层次结构的顶层站点迁移数据。 扩展独立主站点时，迁移配置不会传输到管理中心站点。  

扩展独立主站点后，如果在主站点上重新配置迁移，管理中心站点将执行迁移操作。

若要深入了解如何配置迁移，请参阅[配置源层次结构和迁移源站点](../../../migration/configuring-source-hierarchies-and-source-sites-for-migration.md)。  

#### <a name="computer-account-as-administrator"></a>管理员身份的计算机帐户

承载新管理中心站点的服务器的计算机帐户必须是独立主站点服务器上“管理员”组的成员。

若要成功扩展独立主站点，新管理中心站点的计算机帐户必须具有独立主站点的“管理员”权限。 仅在站点扩展期间需要。 站点扩展完成后，可从主站点的用户组中删除该帐户。  

#### <a name="installation-account-permissions"></a>安装帐户权限

运行 Configuration Manager 安装程序以安装新管理中心站点的用户帐户必须在独立主站点上具有基于角色的管理权限。

若要在站点扩展期间安装管理中心站点，必须在独立主站点的基于角色的管理中，将运行安装程序以安装管理中心站点的用户帐户定义为“完全权限管理员”或“基础结构管理员”。

有关详细信息（包括所需权限的完整列表），请参阅[站点安装帐户](../../../plan-design/hierarchy/accounts.md#site-installation-account)。

#### <a name="top-level-site-roles"></a>顶层站点角色

必须先从独立主站点中卸载下列站点系统角色才能扩展站点：

- 资产智能同步点  
- Endpoint Protection 点  
- 服务连接点  

Configuration Manager 仅在层次结构的顶层站点上支持这些角色。 必须先卸载这些站点系统角色才能扩展独立主站点。 在扩展站点后，在管理中心站点重新安装这些站点系统角色。  

所有其他站点系统角色仍然可以安装在主站点中。  

#### <a name="open-the-sql-server-service-broker-port"></a>打开 SQL Server Service Broker 端口

在独立主站点和管理中心站点的服务器之间，SQL Server Service Broker (SSB) 的网络端口必须打开。  

若要在管理中心站点和主站点之间成功复制数据，Configuration Manager 需要在两个站点之间打开端口以供 SSB 使用。 在安装管理中心站点和扩展独立主站点时，先决条件检查不会验证你为 SSB 指定的端口是否在主站点上打开。  

#### <a name="known-issues-with-azure-services"></a>Azure 服务的已知问题

展开站点后，需要通过 Configuration Manager 重新配置以下 Azure 服务：

- [Log Analytics](/azure/azure-monitor/platform/collect-sccm)  
- [适用于企业的 Microsoft Store](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)  
- [云管理网关](../../../clients/manage/cmg/plan-cloud-management-gateway.md)

最简单的方法是，续订 Azure Active Directory 租户密钥。 有关详细信息，请参阅[续订密钥](../configure/azure-services-wizard.md#bkmk_renew)。

或者，删除并重新创建与该服务的连接：

1. 在 Configuration Manager 控制台中，从“Azure 服务”节点删除 Azure 服务。  

2. 在 Azure 门户中，从“Azure Active Directory 租户”节点删除与该服务关联的租户。 此操作还会删除与该服务关联的 Azure AD Web 应用。  

3. 重新配置与 Azure 服务的连接，用于 Configuration Manager。  


## <a name="secondary-sites"></a><a name="bkmk_secondary"></a>辅助站点

以下是安装辅助站点的先决条件：  

- 必须安装必要的 Windows Server 角色、功能和 Windows 组件。 有关详细信息，请参阅[站点系统先决条件](../../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012secpreq)  

- 在 Configuration Manager 控制台中配置辅助站点安装的管理员必须具有基于角色的管理权限，且这些权限相当于“基础结构管理员”或“完全权限管理员”的安全角色。  

- 父级主站点的计算机帐户必须是辅助站点服务器上的管理员。  

- 当辅助站点使用以前安装的 SQL Server 实例承载辅助站点数据库时：  

    - 父级主站点的计算机帐户必须具有对辅助站点服务器上 SQL Server 实例的 sysadmin 权限。  

    - 辅助站点服务器计算机的本地系统帐户必须具有对辅助站点服务器上 SQL Server 实例的 sysadmin 权限。  

        > [!IMPORTANT]  
        > Configuration Manager 安装完成后，两个帐户都必须保留 SQL Server 的 sysadmin 权限。 请勿从这些帐户中删除 sysadmin 权限。  

- 辅助站点服务器必须满足所有先决条件配置。 这些配置包括 SQL Server 以及管理点和分发点的默认站点系统角色。  


## <a name="next-steps"></a>后续步骤

确认先决条件后，便可以运行安装程序了。 有关详细信息，请参阅[使用安装向导安装 Configuration Manager 站点](use-the-setup-wizard-to-install-sites.md)。