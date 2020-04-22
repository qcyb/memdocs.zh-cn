---
title: Windows 客户端部署先决条件
titleSuffix: Configuration Manager
description: 了解将 Configuration Manager 客户端部署到 Windows 计算机的先决条件。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1a2a9b48-a95b-4643-b00c-b3079584ae2e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1d4cd7ffe38f7191a5361ad2e89817ea80f9f093
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694785"
---
# <a name="prerequisites-for-deploying-clients-to-windows-computers-in-configuration-manager"></a>在 Configuration Manager 中将客户端部署到 Windows 计算机的先决条件

适用范围：  Configuration Manager (Current Branch)

在环境中部署 Configuration Manager 客户端有下列外部依赖关系和产品内部依赖关系。 此外，每个客户端部署方法有其自己的先决条件，要成功安装客户端，必须满足其自己的先决条件。  

要详细了解 Configuration Manager 客户端的最低硬件和 OS 要求，请参阅[支持的配置](../../plan-design/configs/supported-configurations.md)。  

> [!NOTE]  
> 本文中显示的软件版本号仅列出所需的最低版本号。  


## <a name="prerequisites-for-windows-clients"></a><a name="BKMK_prereqs_computers"></a>Windows 客户端的先决条件  

请查看下列信息，确定在 Windows 设备上安装 Configuration Manager 客户端的先决条件。  

### <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 的外部依赖关系  

|组件|说明|  
|---|---|  
|Windows Installer 版本 3.1.4000.2435|这是支持将 Windows Installer 更新文件 (.msp) 用于包和软件更新所必需的。|  
|Microsoft 后台智能传输服务 (BITS) 2.5 版|需要允许客户端计算机和 Configuration Manager 站点系统之间的受限数据传输。 客户端安装过程中不会自动下载 BITS。 在计算机上安装 BITS 后，通常需要重启来完成安装。<br /><br /> 大多数操作系统都包括 BITS。 如果未包括，请在安装 Configuration Manager 客户端之前安装 BITS。|  
|Microsoft 任务计划程序|在客户端上启用此服务，以便完成客户端安装。|  
|SHA-2 代码签名支持|从版本 1906 开始，客户端需要对 SHA-2 代码签名算法的支持。 有关详细信息，请参阅 [SHA-2 代码签名支持](#bkmk_sha2)。|

#### <a name="sha-2-code-signing-support"></a><a name="bkmk_sha2"></a> SHA-2 代码签名支持

<!--SCCMDocs-pr#3404-->
由于 SHA-1 算法中存在缺点，并且为了符合行业标准，Microsoft 现在仅使用更安全的 SHA-2 算法来对 Configuration Manager 二进制文件进行签名。 旧式 Windows OS 版本需要更新才能获得 SHA-2 代码签名支持。 有关详细信息，请参阅 [Windows 和 WSUS 的 2019 SHA-2 代码签名支持要求](https://support.microsoft.com/help/4472027/2019-sha-2-code-signing-support-requirement-for-windows-and-wsus)。

如果未更新这些 OS 版本，则无法安装 Configuration Manager 客户端版本 1906。 此行为适用于新的客户端安装或从以前的版本进行更新。

如果需要在未更新的 Windows 版本或早于上面列出的版本的 Windows 版本上管理客户端，请使用 Configuration Manager 扩展互操作性客户端 (EIC) 版本 1902。 有关详细信息，请参阅[扩展互操作性客户端](../../understand/interoperability-client.md)。

> [!Tip]  
> 如果未使用[自动客户端更新](../manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate)，并且未使用其他机制更新客户端，请确保更新 ccmsetup 的版本。 更早版本的 ccmsetup 可能无法正确验证版本 1906 客户端二进制文件中的新 SHA-2 代码签名证书。 例如，如果将 ccmsetup.exe 复制到文件共享，或者将 ccmsetup.msi 与组策略结合使用。<!-- 4963362 -->
>
> 不应影响以下客户端更新机制：
>
> - 客户端请求安装：它使用站点中的客户端包
> - 基于软件更新的安装：站点更新重新发布到 WSUS
> - Intune MDM 托管的 Windows 设备：此机制支持的版本已支持 SHA-2 代码签名，但使用最新的 ccmsetup.msi 仍很重要

### <a name="dependencies-external-to-configuration-manager-and-automatically-downloaded-during-installation"></a><a name="bkmk_ExternalDependencies"></a>Configuration Manager 外部的、在安装过程中自动下载的依赖项  

Configuration Manager 客户端具备外部依赖项。 这些依赖项取决于 OS 版本以及客户端计算机上安装的软件。  

如果客户端需要这些依赖项来完成安装，则它会自动安装这些依赖项。  

|组件|说明|  
|---|---|  
|Windows Update 代理版本 7.0.6000.363|Windows 要求支持更新检测和部署。|  
|Microsoft Core XML Services (MSXML) 版本 6.20.5002 或更高版本|要求支持在 Windows 中处理 XML 文档。|  
|Microsoft 远程差分压缩 (RDC)|需要该项以优化网络上的数据传输。|  
|Microsoft Visual C++ 2013 可再发行组件版本 12.0.21005.1|需要该项以支持客户端操作。 在客户端计算机上安装此更新时，可能需要重启才能完成安装。|  
|Microsoft Visual C++ 2005 可再发行组件版本 8.0.50727.42|对于 1606 或更早版本，需要该项以支持 Microsoft SQL Server Compact 操作。|  
|Windows 映像 API 6.0.6001.18000|需要该项以允许 Configuration Manager 管理 Windows 映像 (.wim) 文件。|  
|Microsoft 策略平台 1.2.3514.0|需要该项以允许客户端评估符合性设置。|  
|Microsoft .NET Framework 版本 4.5.2|需要该项以支持客户端操作。 如果未安装 Microsoft .NET Framework 4.5 或更高版本，则自动将其安装在客户端计算机上。 有关详细信息，请参阅[有关 Microsoft .NET Framework 版本 4.5.2 的其他详细信息](#dotNet)。|  
|Microsoft SQL Server Compact 4.0 SP1 组件|需要该项以存储与客户端操作相关的信息。|  

> [!Important]
> 从 Current Branch 版本 1806 开始，不支持应用程序目录的 Silverlight 用户体验。 自版本 1906 起，更新后的客户端自动使用管理点进行用户可用的应用程序部署。 仍然无法安装新的应用程序目录角色。 版本 1910 已终止对应用程序目录角色的支持。  
>
> 有关详细信息，请参阅下列文章：
>
> - [配置软件中心](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已删除和已弃用的功能](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  
>
> 如果仍在使用应用程序目录网站用户体验，则客户端需要 Microsoft Silverlight 5.1.41212.0。 客户端不自动安装 Silverlight。 应用程序目录的主要功能现在包含在软件中心内。<!--1356195-->

#### <a name="additional-details-about-microsoft-net-framework-version-452"></a><a name="dotNet"></a>有关 Microsoft .NET Framework 版本 4.5.2 的其他详细信息  

> [!NOTE]  
> 不再支持 .NET 4.0、4.5 和 4.5.1。 有关详细信息，请参阅 [Microsoft .NET Framework 支持生命周期策略常见问题解答](https://support.microsoft.com/help/17455/lifecycle-faq-net-framework)。  

Microsoft .NET Framework 版本 4.5.2 可能需要重启才能完成安装。 用户将在系统托盘中看到“需要重启”  通知。 下面是需要客户端计算机重启的常见情况：  

- 计算机上正在运行.NET 应用程序或服务。  

- .NET 安装所需的一个或多个软件更新丢失。  

- 计算机正在等待从 .NET Framework 软件更新的先前安装中重启。  

安装 .NET Framework 4.5.2 后，可能需要其他更新。 这些后续更新可能需要再次重启计算机。  

### <a name="configuration-manager-dependencies"></a>Configuration Manager 依赖关系  

有关详细信息，请参阅[确定客户端的站点系统角色](plan/determine-the-site-system-roles-for-clients.md)。  

|组件|说明|  
|---|---|  
|管理点|无需管理点即可部署 Configuration Manager 客户端。 客户端需具备管理点才可通过站点传输信息。 没有管理点就无法管理客户端计算机。|  
|分发点|分发点是可选的，但建议使用该站点系统角色部署和管理客户端。 所有分发点都托管客户端源文件。 客户端在客户端部署或更新过程中找到从中下载源文件的最近分发点。 如果站点没有分发点，则计算机从其管理点中下载客户端源文件。|  
|回退状态点|回退状态点是可选的，但建议为客户端部署使用该站点系统角色。 当 Configuration Manager 站点中的计算机不能与管理点通信时，回退状态点会跟踪客户端部署并允许这些计算机发送状态消息。|  
|Reporting Services 点|Reporting Services 点是可选的，但建议使用该站点系统角色。 它会显示与客户端部署和管理相关的报表。 有关详细信息，请参阅[报表简介](../../servers/manage/introduction-to-reporting.md)。|  

### <a name="installation-method-dependencies"></a>安装方法依赖项  

以下先决条件特定于客户端的各种不同安装方法。  

#### <a name="client-push-installation"></a>客户端请求安装  

- 站点通过客户端请求安装帐户连接到计算机来安装客户端。 在客户端请求安装属性的“帐户”选项卡上指定这些帐户  。 该帐户必须是目标计算机上本地管理员组的成员。  

    如果未指定客户端请求安装帐户，站点服务器则使用其自己的计算机帐户。  

- 站点需要发现要在其上安装客户端的计算机。 至少需要一个 Configuration Manager 发现方法。  

- 计算机具有 ADMIN$ 共享。  

- 要对所发现的资源自动推送 Configuration Manager 客户端，请在客户端请求安装属性中选择“对已分配资源启用客户端请求安装”  。  

- 客户端计算机需要与分发点或管理点进行通信，以便下载源文件。  

- 如果需要 Kerberos 相互身份验证，客户端必须位于受信任的 Active Directory 林中。 Windows 中的 Kerberos 依赖 Active Directory 进行相互身份验证。<!--1358204-->  

要使用客户端请求，需要具备以下安全权限：  

- 配置客户端请求安装帐户：“站点”对象的“修改”和“读取”权限    。  

- 使用客户端请求将客户端安装到集合、设备和查询：“集合”对象的“修改资源”和“读取”权限    。  

“基础结构管理员”默认安全角色包括管理客户端请求安装所需的权限  。  

#### <a name="software-update-point-based-installation"></a>基于软件更新点的安装  

- 如果尚未扩展 Active Directory 架构，或者要从另一个林安装客户端，请使用组策略预配 CCMSetup.exe 的安装参数。 有关详细信息，请参阅[如何预配客户端安装属性](deploy-clients-to-windows-computers.md#BKMK_Provision)。  

- 将 Configuration Manager 客户端发布到软件更新点。  

- 要下载源文件，客户端计算机需要与分发点或管理点进行通信。  

有关管理 Configuration Manager 软件更新所需的安全权限，请参阅[软件更新的先决条件](../../../sum/plan-design/prerequisites-for-software-updates.md)。  

#### <a name="group-policy-based-installation"></a>基于组策略的安装  

- 如果尚未扩展 Active Directory 架构，或者要从另一个林安装客户端，请使用组策略预配 CCMSetup.exe 的安装参数。 有关详细信息，请参阅[如何预配客户端安装属性](deploy-clients-to-windows-computers.md#BKMK_Provision)。  

- 要下载源文件，客户端计算机需要与分发点或管理点进行通信。  

#### <a name="logon-script-based-installation"></a>基于登录脚本的安装  

要下载源文件，客户端计算机需要与分发点或管理点进行通信。 除非使用命令行参数 `ccmsetup /source` 指定 CCMSetup.exe  

#### <a name="manual-installation"></a>手动安装  

要下载源文件，客户端计算机需要与分发点或管理点进行通信。 除非使用命令行参数 `ccmsetup /source` 指定 CCMSetup.exe  

#### <a name="microsoft-intune-mdm-installation"></a>Microsoft Intune MDM 安装

- 需要 Microsoft Intune 订阅和相应的许可证。  

- 要求设备能访问 Internet，即使它不基于 Internet。  

- 根据用例，可能还需要以下一种或两种技术：  

    - Azure Active Directory  

    - 云管理网关  

#### <a name="workgroup-computer-installation"></a>工作组计算机安装  

要访问 Configuration Manager 站点服务器域中的资源，请为该站点配置网络访问帐户。  

有关如何配置网络访问帐户的详细信息，请参阅[内容管理的基本概念](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md)。  

#### <a name="software-distribution-based-installation-for-upgrades-only"></a>基于软件分发的安装（仅针对升级）  

- 如果尚未扩展 Active Directory 架构，或者要从另一个林安装客户端，请使用组策略预配 CCMSetup.exe 的安装参数。 有关详细信息，请参阅[如何预配客户端安装属性](deploy-clients-to-windows-computers.md#BKMK_Provision)。

- 要下载源文件，客户端计算机需要与分发点或管理点进行通信。  

有关使用应用程序管理升级 Configuration Manager 客户端所需的安全权限，请参阅[应用程序管理的安全和隐私](../../../apps/plan-design/security-and-privacy-for-application-management.md)。  

#### <a name="automatic-client-upgrades"></a>自动客户端升级  

你必须是“完全权限管理员”  安全角色的成员才能配置自动客户端升级。  

### <a name="firewall-requirements"></a>防火墙要求  

如果站点系统服务器与你要在其上安装 Configuration Manager 客户端的计算机之间存在防火墙，请参阅[客户端的 Windows 防火墙和端口设置](windows-firewall-and-port-settings-for-clients.md)。  


## <a name="prerequisites-for-mobile-device-clients"></a><a name="BKMK_prereqs_mobiledevices"></a>移动设备客户端的先决条件  

在移动设备上安装 Configuration Manager 客户端并注册设备时，请使用此信息来确定先决条件。  

### <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 的外部依赖关系

- Microsoft 企业证书颁发机构 (CA) 及证书模板，用于部署和管理移动设备所需的证书。  

    颁发 CA 必须在注册过程中自动批准来自移动设备用户的证书请求。  

    有关证书要求的详细信息，请参阅[证书配置文件的安全和隐私](../../../protect/plan-design/security-and-privacy-for-certificate-profiles.md)。  

- 一个安全组，其中包含可注册其移动设备的用户。  

    此安全组用于配置在移动设备注册过程中使用的证书模板。  

- 可选但建议使用：名为 ConfigMgrEnroll（CNAME 记录）的 DNS 别名  。 为注册代理点的服务器名称配置此别名。  

    需要此 DNS 别名以支持注册服务的自动发现。 如果未配置此 DNS 记录，则用户必须在注册过程中手动指定注册代理点的名称。  

- 运行注册点和注册代理点站点系统角色的计算机的站点系统角色依赖项。  

    有关详细信息，请参阅[站点系统服务器支持的操作系统](../../plan-design/configs/supported-operating-systems-for-site-system-servers.md)。  

### <a name="configuration-manager-dependencies"></a>Configuration Manager 依赖关系

有关详细信息，请参阅[确定客户端的站点系统角色](plan/determine-the-site-system-roles-for-clients.md)。  

- 为 HTTPS 客户端连接配置并为移动设备启用的管理点  

    必须使用管理点才能在移动设备上安装 Configuration Manager 客户端。 除了 HTTPS 要求和为移动设备启用的要求外，还必须将管理点配置为具有 Internet FQDN 并接受来自 Internet 的客户端连接。  

- 注册点和注册代理点  

    注册代理点管理来自移动设备的注册请求，注册点完成注册过程。 注册点必须位于站点服务器所在的 Active Directory 林中，但注册代理点则可位于另一个林中。  

- 移动设备注册的客户端设置  

    配置客户端设置以允许用户注册移动设备并至少配置一个注册配置文件。  

- Reporting Services 点  

    Reporting Services 点是可选的，但建议使用该站点系统角色，它能够显示与移动设备注册和客户端管理相关的报表。  

    有关详细信息，请参阅[报表简介](../../servers/manage/introduction-to-reporting.md)。  

- 要针对移动设备配置注册，你必须具有下列安全权限：  

    - 添加、修改和删除注册站点系统角色：“站点”对象的“修改”权限   。  

    - 配置注册的客户端设置：默认客户端设置需要“站点”对象的“修改”权限，自定义客户端设置需要“客户端代理”权限    。  

    “完全权限管理员”默认安全角色包括配置注册站点系统角色所需的权限  。  

- 要管理注册的移动设备，你必须具有下列安全权限：  

    - 擦除或停用移动设备：“集合”对象的“删除资源”权限   。  

    - 取消擦除或停用命令：“集合”对象的“删除资源”权限   。  

    - 允许和阻止移动设备：“集合”对象的“修改资源”权限   。  

    - 远程锁定或重置移动设备上的密码：“集合”对象的“修改资源”权限   。  

    “操作管理员”默认安全角色包括管理移动设备所需的权限  。  

    有关如何配置安全权限的详细信息，请参阅[基于角色的管理的基础](../../understand/fundamentals-of-role-based-administration.md)和[配置基于角色的管理](../../servers/deploy/configure/configure-role-based-administration.md)。  

### <a name="firewall-requirements"></a>防火墙要求

诸如路由器和防火墙以及 Windows 防火墙（如果适用）等干预网络设备必须允许与移动设备注册相关联的通讯：  

- 移动设备和注册代理点之间：HTTPS（默认为 TCP 443）  

- 注册代理点和注册点之间：HTTPS（默认为 TCP 443）  

如果使用的是代理 Web 服务器，则必须针对 SSL 隧道对其进行配置。 移动设备不支持 SSL 桥接。  
