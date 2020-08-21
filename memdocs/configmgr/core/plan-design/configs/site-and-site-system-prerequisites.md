---
title: 站点先决条件
titleSuffix: Configuration Manager
description: 了解如何将 Windows 计算机配置为 Configuration Manager 站点系统服务器。
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ce3420a6e229b5987616c5c0c1c41d50cdc499c8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700344"
---
# <a name="site-and-site-system-prerequisites-for-configuration-manager"></a>用于 Configuration Manager 的站点和站点系统先决条件

适用范围：  Configuration Manager (Current Branch)

基于 Windows 的计算机要求特定配置，以支持用作 Configuration Manager 站点系统服务器。

对于某些产品，例如软件更新点的 Windows Server Update Services (WSUS)，需要参考产品文档来确定使用的其他先决条件和限制。 此处仅包含直接应用于 Configuration Manager 的配置。

有关 .NET Framework 的详细信息，请参阅[生命周期常见问题解答 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)。


## <a name="general-requirements-and-limitations"></a><a name="bkmk_generalprerewq"></a>常规要求和限制

以下要求适用于所有站点系统服务器：

- 每个站点系统服务器必须使用 64 位 OS。 唯一的例外是分发点站点系统角色，它可以安装在某些 32 位操作系统上。  

- 在任意操作系统的 Server Core 安装上，站点系统不受支持。 例外是分发点站点系统角色支持 Server Core 安装。 有关详细信息，请参阅 [Configuration Manager 站点系统服务器支持的操作系统](supported-operating-systems-for-site-system-servers.md)。  

- 安装站点系统服务器后，不支持进行更改：  

    - 站点系统计算机所在域的域名（也称为**域重命名**）。  

    - 计算机的域成员身份。  

    - 计算机的名称。  

    如果必须更改其中任何项，请先从计算机中删除站点系统角色。 然后在更改完成后重新安装该角色。 对于影响站点服务器的更改，请首先卸载该站点。 然后在更改完成后重新安装该站点。  

- 在 Windows Server 群集实例上，站点系统角色不受支持。 唯一例外是站点数据库服务器。 有关详细信息，请参阅[对 Configuration Manager 站点数据库使用 SQL Server 群集](../../servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md)。  

    从版本 1810 开始，Configuration Manager 设置进程不再阻止在具有适用于故障转移群集的 Windows 角色的计算机上安装站点服务器角色。 SQL Always On 需要此角色，因此，以前你无法在站点服务器上共置站点数据库。 进行此更改后，你可以通过在被动模式下使用 SQL Always On 和站点服务器创建具有更少服务器的高可用站点。 有关详细信息，请参阅[高可用性选项](../../servers/deploy/configure/high-availability-options.md)。 <!--3607761, fka 1359132-->  

- 不支持更改任意 Configuration Manager 服务的启动类型或“登录身份”设置。 这样做可能会阻止关键服务正常运行。  

### <a name="prerequisites-for-windows-server-2012-and-later-operating-systems"></a><a name="bkmk_2012Prereq"></a> Windows Server 2012 和更高版本操作系统的先决条件  

有关 Windows Server 2012 及更高版本上的站点系统服务器和角色的特定先决条件，请参阅本文的主要部分：

- [管理中心站点和主站点服务器](#bkmk_2012sspreq)
- [辅助站点服务器](#bkmk_2012secpreq)
- [数据库服务器](#bkmk_2012dbpreq)
- [SMS 提供程序服务器](#bkmk_2012smsprovpreq)
- [应用程序目录网站点](#bkmk_2012acwspreq)
- [应用程序目录 Web 服务点](#bkmk_2012ACwsitepreq)
- [资产智能同步点](#bkmk_2012AIpreq)
- [证书注册点](#bkmk_2012crppreq)
- [分发点](#bkmk_2012dppreq)
- [Endpoint Protection 点](#bkmk_2012EPPpreq)
- [注册点](#bkmk_2012Enrollpreq)
- [注册代理点](#bkmk_2012EnrollProxpreq)
- [回退状态点](#bkmk_2012FSPpreq)
- [管理点](#bkmk_2012MPpreq)
- [Reporting Services 点](#bkmk_2012RSpoint)
- [服务连接点](#bkmk_SCPpreq)
- [软件更新点](#bkmk_2012SUPpreq)
- [状态迁移点](#bkmk_2012SMPpreq)

## <a name="central-administration-site-and-primary-site-servers"></a><a name="bkmk_2012sspreq"></a>管理中心站点和主站点服务器

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- .NET Framework 3.5

- 远程差分压缩  

- 如果在除站点服务器以外的服务器上使用软件更新点，请在站点服务器上安装 WSUS 管理控制台。

### <a name="net-framework"></a>.NET Framework

启用 .NET Framework 3.5 的 Windows 功能。

同时安装受支持的 .NET Framework 版本 4.5 或更高版本。 从版本 1906 开始，Configuration Manager 支持 .NET Framework 4.8。

有关 .NET Framework 版本的详细信息，请参阅以下文章：

- [.NET Framework 版本和依赖关系](/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命周期常见问题解答 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-adk"></a>Windows ADK  

- 安装或升级管理中心站点或主站点之前，安装要安装或升级到的 Configuration Manager 版本所需的 Windows 评估和部署工具包 (ADK) 版本。 有关详细信息，请参阅 [Windows 10 ADK](support-for-windows-10.md#windows-10-adk)。  

- 有关此要求的详细信息，请参阅 [OS 部署的基础架构要求](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md)。  

### <a name="visual-c-redistributable"></a>Visual C++ Redistributable  

- Configuration Manager 在安装站点服务器的每台计算机上安装 Microsoft Visual C++ 2013 可再发行组件包。  

- 管理中心站点和主站点需要适用的可再发行文件的 x86 和 x64 版本。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

在安装新站点时，Configuration Manager 会自动将 SQL Server Native Client 作为可再发行组件安装。 安装站点后，Configuration Manager 不会升级 SQL Server Native Client。 确保此组件是最新的。 有关详细信息，请参阅[先决条件检查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="secondary-site-server"></a><a name="bkmk_2012secpreq"></a>辅助站点服务器

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- .NET Framework 3.5

- 远程差分压缩  

### <a name="net-framework"></a>.NET Framework

启用 .NET Framework 3.5 的 Windows 功能。

同时安装受支持的 .NET Framework 版本 4.5 或更高版本。 从版本 1906 开始，Configuration Manager 支持 .NET Framework 4.8。

有关 .NET Framework 版本的详细信息，请参阅以下文章：

- [.NET Framework 版本和依赖关系](/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命周期常见问题解答 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Visual C++ Redistributable

- Configuration Manager 在安装站点服务器的每台计算机上安装 Microsoft Visual C++ 2013 可再发行组件包。  

- 辅助站点仅需要 x64 版本。  

### <a name="default-site-system-roles"></a>默认站点系统角色  

- 默认情况下，辅助站点将安装**管理点**和**分发点**。  

- 请确保辅助站点服务器满足这些站点系统角色的先决条件。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

在安装新站点时，Configuration Manager 会自动将 SQL Server Native Client 作为可再发行组件安装。 安装站点后，Configuration Manager 不会升级 SQL Server Native Client。 确保此组件是最新的。 有关详细信息，请参阅[先决条件检查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="database-server"></a><a name="bkmk_2012dbpreq"></a>数据库服务器  

### <a name="remote-registry-service"></a>远程注册表服务  

- 在安装 Configuration Manager 站点的过程中，在托管站点数据库的计算机上启用“远程注册表”服务  。  

### <a name="sql-server"></a>SQL Server  

- 在安装管理中心站点或主站点之前，要安装受支持的 SQL Server 版本以托管站点数据库。 有关详细信息，请参阅[支持的 SQL Server 版本](support-for-sql-server-versions.md)。  

- 在安装辅助站点之前，可以安装受支持的 SQL Server 版本。  

- 如果选择让 Configuration Manager 将 SQL Server Express 作为辅助站点安装的一部分安装，请确保计算机满足运行 SQL Server Express 的要求。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

在安装新站点时，Configuration Manager 会自动将 SQL Server Native Client 作为可再发行组件安装。 安装站点后，Configuration Manager 不会升级 SQL Server Native Client。 确保此组件是最新的。 有关详细信息，请参阅[先决条件检查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="sms-provider-server"></a><a name="bkmk_2012smsprovpreq"></a> SMS 提供程序服务器  

### <a name="windows-adk"></a>Windows ADK

- 安装 SMS 提供程序实例的计算机必须具备要安装或升级到的 Configuration Manager 版本所需的 Windows ADK 版本。 有关详细信息，请参阅 [Windows 10 ADK](support-for-windows-10.md#windows-10-adk)。  

- 有关此要求的详细信息，请参阅[操作系统部署的基础架构要求](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md)。  

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- 如果使用的是[管理服务](../../../develop/adminservice/overview.md)，则托管 SMS 提供程序角色的服务器需要 .NET 4.5 或更高版本  <!-- SCCMDocs issue #1203 -->

    > [!NOTE]
    > Configuration Manager 1810 版需要 .NET 4.5.2 或更高版本。

- Web 服务器 (IIS)：每个提供程序都会尝试安装[管理服务](../../../develop/adminservice/overview.md)。 此服务具有对 IIS 的依赖，以便将证书绑定到 HTTPS 端口 443。 Configuration Manager 使用 IIS API 检查此证书配置。 如果将站点配置为[增强型 HTTP](../hierarchy/enhanced-http.md)，Configuration Manager 会使用 IIS API 绑定站点生成的证书。 从版本 2002 开始，站点会自动使用站点的自签名证书。

### <a name="sql-server-native-client"></a>SQL Server Native Client

在安装新站点时，Configuration Manager 会自动将 SQL Server Native Client 作为可再发行组件安装。 安装站点后，Configuration Manager 不会升级 SQL Server Native Client。 确保此组件是最新的。 有关详细信息，请参阅[先决条件检查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="application-catalog-website-point"></a><a name="bkmk_2012acwspreq"></a> 应用程序目录网站点  

> [!Important]  
> 从 Current Branch 版本 1806 开始，不支持应用程序目录的 Silverlight 用户体验。 自版本 1906 起，更新后的客户端自动使用管理点进行用户可用的应用程序部署。 仍然无法安装新的应用程序目录角色。 版本 1910 已终止对应用程序目录角色的支持。  
>
> 有关详细信息，请参阅下列文章：
>
> - [配置软件中心](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已删除和已弃用的功能](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- .NET Framework 3.5

- ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

启用 .NET Framework 3.5 的 Windows 功能。

同时安装受支持的 .NET Framework 版本 4.5 或更高版本。

有关 .NET Framework 版本的详细信息，请参阅以下文章：

- [.NET Framework 版本和依赖关系](/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命周期常见问题解答 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS 配置  

- 常见的 HTTP 功能：  

    - 默认文档  

    - 静态内容  

- 应用程序开发：  

    - ASP.NET 3.5（和自动选择的选项）  

    - ASP.NET 4.5（和自动选择的选项）  

    - .NET Extensibility 3.5  

    - .NET Extensibility 4.5  

- 安全性：  

    - Windows 身份验证  

- IIS 6 管理兼容性：  

    - IIS 6 元数据库兼容性  


## <a name="application-catalog-web-service-point"></a><a name="bkmk_2012ACwsitepreq"></a> 应用程序目录 Web 服务点  

> [!Important]  
> 从 Current Branch 版本 1806 开始，不支持应用程序目录的 Silverlight 用户体验。 自版本 1906 起，更新后的客户端自动使用管理点进行用户可用的应用程序部署。 仍然无法安装新的应用程序目录角色。 版本 1910 已终止对应用程序目录角色的支持。  
>
> 有关详细信息，请参阅下列文章：
>
> - [配置软件中心](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已删除和已弃用的功能](../changes/deprecated/removed-and-deprecated-cmfeatures.md)  

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- .NET Framework 3.5

- ASP.NET 4.5：  

    - HTTP 激活（和自动选择的选项）  

### <a name="net-framework"></a>.NET Framework

启用 .NET Framework 3.5 的 Windows 功能。

同时安装受支持的 .NET Framework 版本 4.5 或更高版本。

有关 .NET Framework 版本的详细信息，请参阅以下文章：

- [.NET Framework 版本和依赖关系](/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命周期常见问题解答 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS 配置

- 常见的 HTTP 功能：  

    - 默认文档  

- IIS 6 管理兼容性：  

    - IIS 6 元数据库兼容性  

- 应用程序开发：  

    - ASP.NET 3.5（和自动选择的选项）  

    - .NET Extensibility 3.5  

    - ASP.NET 4.5（和自动选择的选项）  

    - .NET Extensibility 4.5  

### <a name="computer-memory"></a>计算机内存  

- 托管此站点系统角色的计算机必须具有最少 5% 的计算机可用内存来启用站点系统角色以处理请求。  

- 当此站点系统角色与具有该相同要求的另一站点系统角色并存时，对计算机的该内存要求将不会增加，而是保持为最少 5% 的值。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

在安装新站点时，Configuration Manager 会自动将 SQL Server Native Client 作为可再发行组件安装。 安装站点后，Configuration Manager 不会升级 SQL Server Native Client。 确保此组件是最新的。 有关详细信息，请参阅[先决条件检查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="asset-intelligence-synchronization-point"></a><a name="bkmk_2012AIpreq"></a>资产智能同步点  

### <a name="net-framework"></a>.NET Framework

安装受支持的 .NET Framework 版本 4.5 或更高版本。 从版本 1906 开始，Configuration Manager 支持 .NET Framework 4.8。

有关 .NET Framework 版本的详细信息，请参阅以下文章：

- [.NET Framework 版本和依赖关系](/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命周期常见问题解答 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-native-client"></a>SQL Server Native Client

在安装新站点时，Configuration Manager 会自动将 SQL Server Native Client 作为可再发行组件安装。 安装站点后，Configuration Manager 不会升级 SQL Server Native Client。 确保此组件是最新的。 有关详细信息，请参阅[先决条件检查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="certificate-registration-point"></a><a name="bkmk_2012crppreq"></a>证书注册点  

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- .NET Framework

    - HTTP 激活  

### <a name="net-framework"></a>.NET Framework

安装受支持的 .NET Framework 版本 4.5 或更高版本。 从版本 1906 开始，Configuration Manager 支持 .NET Framework 4.8。

有关 .NET Framework 版本的详细信息，请参阅以下文章：

- [.NET Framework 版本和依赖关系](/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命周期常见问题解答 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS 配置

- 应用程序开发：  

    - ASP.NET 3.5（和自动选择的选项）  

    - ASP.NET 4.5（和自动选择的选项）  

- IIS 6 管理兼容性：  

    - IIS 6 元数据库兼容性  

    - IIS 6 WMI 兼容性  

### <a name="sql-server-native-client"></a>SQL Server Native Client

在安装新站点时，Configuration Manager 会自动将 SQL Server Native Client 作为可再发行组件安装。 安装站点后，Configuration Manager 不会升级 SQL Server Native Client。 确保此组件是最新的。 有关详细信息，请参阅[先决条件检查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="distribution-point"></a><a name="bkmk_2012dppreq"></a>分发点  

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- 远程差分压缩  

#### <a name="iis-configuration"></a>IIS 配置

- 应用程序开发：  

    - ISAPI 扩展  

- 安全性：  

    - Windows 身份验证  

- IIS 6 管理兼容性：  

    - IIS 6 元数据库兼容性  

    - IIS 6 WMI 兼容性  

### <a name="powershell"></a>PowerShell  

- 在安装分发点之前，需要在 Windows Server 2012 或更高版本上安装 PowerShell 3.0 或 4.0。  

### <a name="visual-c-redistributable"></a>Visual C++ Redistributable

- Configuration Manager 在托管分发点的每台计算机上安装 Microsoft Visual C++ 2013 可再发行组件包。  

- 安装的版本取决于计算机平台（x86 或 x64）。  

### <a name="microsoft-azure"></a>Microsoft Azure  

- 可以使用 Microsoft Azure 中的云服务来托管分发点。  

### <a name="to-support-pxe-or-multicast"></a>支持 PXE 或多播  

- 在没有 Windows 部署服务的情况下在分发点上启用 PXE 响应程序。  

- 安装和配置 Windows 部署服务 (WDS) Windows Server 角色。  

    > [!NOTE]  
    > 当配置分发点以在运行 Windows Server 2012 或更高版本的服务器上支持 PXE 或多播时，将自动安装和配置 WDS。  

- 对于启用多播的分发点，确保已安装 SQL Server Native Client 并保持最新状态。 有关详细信息，请参阅[先决条件检查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。

有关详细信息，请参阅[安装和配置分发点](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)。

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> 当分发点传输内容时，它将使用内置于 Windows 的“后台智能传输服务”(BITS) 进行传输  。 分发点角色不需要安装可选的 BITS IIS 服务器扩展功能，因为客户端不会向其上传信息。  


## <a name="endpoint-protection-point"></a><a name="bkmk_2012EPPpreq"></a> Endpoint Protection 点  

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能  

- .NET Framework 3.5

- Windows Defender 功能（Windows Server 2016 或更高版本）  

### <a name="sql-server-native-client"></a>SQL Server Native Client

在安装新站点时，Configuration Manager 会自动将 SQL Server Native Client 作为可再发行组件安装。 安装站点后，Configuration Manager 不会升级 SQL Server Native Client。 确保此组件是最新的。 有关详细信息，请参阅[先决条件检查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="enrollment-point"></a><a name="bkmk_2012Enrollpreq"></a>注册点  

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- .NET Framework 3.5

    - HTTP 激活（和自动选择的选项）  

    - ASP.NET 4.5  

    - Windows Communication Foundation (WCF) 服务<!-- SCCMDocs issue #1168 -->  

### <a name="net-framework"></a>.NET Framework

启用 .NET Framework 3.5 的 Windows 功能。

同时安装受支持的 .NET Framework 版本 4.5 或更高版本。 从版本 1906 开始，Configuration Manager 支持 .NET Framework 4.8。

> [!Note]
> 此站点系统角色安装时，Configuration Manager 将自动安装 .NET Framework 4.5.2。 此安装可将服务器置于重启挂起状态。 如果挂起对 .NET Framework 的重启，在服务器重启和安装完成之前，.NET 应用程序可能失败。  

有关 .NET Framework 版本的详细信息，请参阅以下文章：

- [.NET Framework 版本和依赖关系](/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命周期常见问题解答 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS 配置

- 常见的 HTTP 功能：  

    - 默认文档  

- 应用程序开发：  

    - ASP.NET 3.5（和自动选择的选项）  

    - .NET Extensibility 3.5  

    - ASP.NET 4.5（和自动选择的选项）  

    - .NET Extensibility 4.5  

- IIS 6 管理兼容性：  

    - IIS 6 元数据库兼容性  

### <a name="computer-memory"></a>计算机内存

- 托管此站点系统角色的计算机必须具有最少 5% 的计算机可用内存来启用站点系统角色以处理请求。  

- 当此站点系统角色与具有该相同要求的另一站点系统角色并存时，对计算机的该内存要求将不会增加，而是保持为最少 5% 的值。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

在安装新站点时，Configuration Manager 会自动将 SQL Server Native Client 作为可再发行组件安装。 安装站点后，Configuration Manager 不会升级 SQL Server Native Client。 确保此组件是最新的。 有关详细信息，请参阅[先决条件检查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="enrollment-proxy-point"></a><a name="bkmk_2012EnrollProxpreq"></a>注册代理点  

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- .NET Framework 3.5

### <a name="net-framework"></a>.NET Framework

启用 .NET Framework 3.5 的 Windows 功能。

同时安装受支持的 .NET Framework 版本 4.5 或更高版本。 从版本 1906 开始，Configuration Manager 支持 .NET Framework 4.8。

> [!Note]
> 此站点系统角色安装时，Configuration Manager 将自动安装 .NET Framework 4.5.2。 此安装可将服务器置于重启挂起状态。 如果挂起对 .NET Framework 的重启，在服务器重启和安装完成之前，.NET 应用程序可能失败。  

有关 .NET Framework 版本的详细信息，请参阅以下文章：

- [.NET Framework 版本和依赖关系](/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命周期常见问题解答 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS 配置

- 常见的 HTTP 功能：  

    - 默认文档  

    - 静态内容  

- 应用程序开发：  

    - ASP.NET 3.5（和自动选择的选项）  

    - ASP.NET 4.5（和自动选择的选项）  

    - .NET Extensibility 3.5  

    - .NET Extensibility 4.5  

- 安全性：  

    - Windows 身份验证  

- IIS 6 管理兼容性：  

    - IIS 6 元数据库兼容性  

### <a name="computer-memory"></a>计算机内存

- 托管此站点系统角色的计算机必须具有最少 5% 的计算机可用内存来启用站点系统角色以处理请求。  

- 当此站点系统角色与具有该相同要求的另一站点系统角色并存时，对计算机的该内存要求将不会增加，而是保持为最少 5% 的值。  


## <a name="fallback-status-point"></a><a name="bkmk_2012FSPpreq"></a>回退状态点

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- BITS 服务器扩展（和自动选择的选项），或后台智能传输服务 (BITS)（和自动选择的选项）

#### <a name="iis-configuration"></a>IIS 配置

需要带有以下添加内容的默认 IIS 配置：  

- IIS 6 管理兼容性：  

    - IIS 6 元数据库兼容性  


## <a name="management-point"></a><a name="bkmk_2012MPpreq"></a>管理点  

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- BITS 服务器扩展（和自动选择的选项），或后台智能传输服务 (BITS)（和自动选择的选项）  

### <a name="net-framework"></a>.NET Framework

安装受支持的 .NET Framework 版本 4.5 或更高版本。 从版本 1906 开始，Configuration Manager 支持 .NET Framework 4.8。

有关 .NET Framework 版本的详细信息，请参阅以下文章：

- [.NET Framework 版本和依赖关系](/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命周期常见问题解答 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS 配置

- 应用程序开发：  

    - ISAPI 扩展  

- 安全性：  

    - Windows 身份验证  

- IIS 6 管理兼容性：  

    - IIS 6 元数据库兼容性  

    - IIS 6 WMI 兼容性  

### <a name="sql-server-native-client"></a>SQL Server Native Client

在安装新站点时，Configuration Manager 会自动将 SQL Server Native Client 作为可再发行组件安装。 安装站点后，Configuration Manager 不会升级 SQL Server Native Client。 确保此组件是最新的。 有关详细信息，请参阅[先决条件检查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="reporting-services-point"></a><a name="bkmk_2012RSpoint"></a> Reporting Services 点  

### <a name="net-framework"></a>.NET Framework

安装受支持的 .NET Framework 版本 4.5 或更高版本。 从版本 1906 开始，Configuration Manager 支持 .NET Framework 4.8。

有关 .NET Framework 版本的详细信息，请参阅以下文章：

- [.NET Framework 版本和依赖关系](/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命周期常见问题解答 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services  

- 在安装报表点之前，安装并配置至少一个 SQL Server 实例以支持 SQL Server Reporting Services。  

- 用于 SQL Server Reporting Services 的实例可以是用于站点数据库的同一实例。  

- 此外，只要其他 System Center 产品对共享 SQL Server 实例没有限制，则你使用的实例可与其他 System Center 产品共享。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

在安装新站点时，Configuration Manager 会自动将 SQL Server Native Client 作为可再发行组件安装。 安装站点后，Configuration Manager 不会升级 SQL Server Native Client。 确保此组件是最新的。 有关详细信息，请参阅[先决条件检查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="service-connection-point"></a><a name="bkmk_SCPpreq"></a>服务连接点  

### <a name="net-framework"></a>.NET Framework

启用 .NET Framework 3.5 的 Windows 功能。

同时安装受支持的 .NET Framework 版本 4.5 或更高版本。 从版本 1906 开始，Configuration Manager 支持 .NET Framework 4.8。

> [!Note]
> 此站点系统角色安装时，Configuration Manager 将自动安装 .NET Framework 4.5.2。 此安装可将服务器置于重启挂起状态。 如果挂起对 .NET Framework 的重启，在服务器重启和安装完成之前，.NET 应用程序可能失败。  

有关 .NET Framework 版本的详细信息，请参阅以下文章：

- [.NET Framework 版本和依赖关系](/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命周期常见问题解答 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="visual-c-redistributable"></a>Visual C++ Redistributable

- Configuration Manager 在托管分发点的每台计算机上安装 Microsoft Visual C++ 2013 可再发行组件包。  

- 站点系统角色需要 x64 版本。  

### <a name="sql-server-native-client"></a>SQL Server Native Client

在安装新站点时，Configuration Manager 会自动将 SQL Server Native Client 作为可再发行组件安装。 安装站点后，Configuration Manager 不会升级 SQL Server Native Client。 确保此组件是最新的。 有关详细信息，请参阅[先决条件检查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="software-update-point"></a><a name="bkmk_2012SUPpreq"></a>软件更新点  

### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- .NET Framework 3.5

需要默认 IIS 配置。

### <a name="net-framework"></a>.NET Framework

启用 .NET Framework 3.5 的 Windows 功能。

同时安装受支持的 .NET Framework 版本 4.5 或更高版本。 从版本 1906 开始，Configuration Manager 支持 .NET Framework 4.8。

有关 .NET Framework 版本的详细信息，请参阅以下文章：

- [.NET Framework 版本和依赖关系](/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命周期常见问题解答 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="windows-server-update-services"></a>Windows Server 更新服务  

- 安装软件更新点之前，在计算机上安装 Windows 服务器角色 Windows Server Update Services。  

- 有关详细信息，请参阅[规划软件更新](../../../sum/plan-design/plan-for-software-updates.md)。  

> [!NOTE]  
> 如果在除站点服务器以外的服务器上使用软件更新点，必须在站点服务器上安装 WSUS 管理控制台。

### <a name="sql-server-native-client"></a>SQL Server Native Client

在安装新站点时，Configuration Manager 会自动将 SQL Server Native Client 作为可再发行组件安装。 安装站点后，Configuration Manager 不会升级 SQL Server Native Client。 确保此组件是最新的。 有关详细信息，请参阅[先决条件检查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。


## <a name="state-migration-point"></a><a name="bkmk_2012SMPpreq"></a> 状态迁移点

<!--SCCMDocs issue 645-->
### <a name="windows-server-roles-and-features"></a>Windows Server 角色和功能

- .NET Framework 3.5

    - HTTP 激活（和自动选择的选项）  

    - ASP.NET 4.5  

### <a name="net-framework"></a>.NET Framework

启用 .NET Framework 3.5 的 Windows 功能。

同时安装受支持的 .NET Framework 版本 4.5 或更高版本。 从版本 1906 开始，Configuration Manager 支持 .NET Framework 4.8。

> [!Note]
> 此站点系统角色安装时，Configuration Manager 将自动安装 .NET Framework 4.5.2。 此安装可将服务器置于重启挂起状态。 如果挂起对 .NET Framework 的重启，在服务器重启和安装完成之前，.NET 应用程序可能失败。  

有关 .NET Framework 版本的详细信息，请参阅以下文章：

- [.NET Framework 版本和依赖关系](/dotnet/framework/migration-guide/versions-and-dependencies)
- [生命周期常见问题解答 - .NET Framework](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)

### <a name="iis-configuration"></a>IIS 配置

- 常见的 HTTP 功能：  

    - 默认文档  

- 应用程序开发：  

    - ASP.NET 3.5（和自动选择的选项）  

    - .NET Extensibility 3.5  

    - ASP.NET 4.5（和自动选择的选项）  

    - .NET Extensibility 4.5  

- IIS 6 管理兼容性：  

    - IIS 6 元数据库兼容性  

### <a name="sql-server-native-client"></a>SQL Server Native Client

在安装新站点时，Configuration Manager 会自动将 SQL Server Native Client 作为可再发行组件安装。 安装站点后，Configuration Manager 不会升级 SQL Server Native Client。 确保此组件是最新的。 有关详细信息，请参阅[先决条件检查 - SQL Server Native Client](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。