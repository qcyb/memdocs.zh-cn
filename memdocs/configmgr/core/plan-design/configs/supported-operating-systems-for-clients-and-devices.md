---
title: 支持的客户端和设备
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 在客户端和设备上支持的操作系统版本。
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 87f4e041-67df-4c61-aa98-7444faffe565
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8e3f375fb515808c1df39d1fdd786abb8f89a0a2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691365"
---
# <a name="supported-os-versions-for-clients-and-devices-for-configuration-manager"></a>Configuration Manager 在客户端和设备上支持的操作系统版本

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 支持在 Windows 和 macOS 计算机上安装客户端软件。  

## <a name="general-requirements-and-limitations"></a>常规要求和限制

请查看以下对所有客户端的要求和限制：

- 不支持更改任意 Configuration Manager 服务的启动类型或“登录身份”  设置。 此更改可能会阻止关键服务正常运行。

## <a name="windows-computers"></a>Windows 计算机  

若要管理以下 Windows OS 版本，请使用 Configuration Manager 随附的客户端。 有关详细信息，请参阅[如何将客户端部署到 Windows 计算机](../../clients/deploy/deploy-clients-to-windows-computers.md)。  

### <a name="supported-client-os-versions"></a>受支持的客户端 OS 版本

- **Windows 10**  

    有关详细信息，请参阅 [Windows 10 支持](support-for-windows-10.md)。  

- **Windows 8.1** (x86, x64)：Professional、Enterprise

#### <a name="windows-virtual-desktop"></a>Windows 虚拟桌面

<!--3556025-->
[Windows 虚拟桌面](https://docs.microsoft.com/azure/virtual-desktop/)是在 Microsoft Azure 上运行的桌面和应用虚拟化服务。 从版本 1906 开始，可以使用 Configuration Manager 管理在 Azure 中运行 Windows 的这些虚拟设备。

与终端服务器类似，其中某些虚拟设备支持多个并发的活动用户会话。 为帮助提高客户端性能，Configuration Manager 现在任何可支持多个用户会话的设备上禁用了用户策略。 即使启用用户策略，客户端上的这些设备（包括 Windows 10 企业版多会话和终端服务器）也会默认禁用这些用户策略。

客户端仅在新的安装期间检测到此类设备时才会禁用用户策略。 对于已更新到此版本的现有此类客户端而言，以前的行为仍然存在。 在现有设备上，即使检测到设备支持多个用户会话，它也会配置用户策略设置。

如果在此方案中需要用户策略，并且接受任何潜在的性能影响，请使用以下方法之一来启用用户策略：

- 在版本 1910 及更高版本中，使用[客户端设置](../../clients/deploy/configure-client-settings.md)。 在“客户端策略”组中，配置以下设置  ：“为多个用户会话启用用户策略”  。<!-- 4737447 -->

- 在版本 1906 中，将 Configuration Manager SDK 与 [SMS_PolicyAgentConfig 服务器 WMI 类](../../../develop/reference/core/clients/config/sms_policyagentconfig-server-wmi-class.md)一起使用。 将新的 `PolicyEnableUserPolicyOnTS` 属性设置为 `true`。

> [!Note]  
> 不能对运行 Windows 10 企业版多会话的客户端使用共同管理。 <!-- SCCMDocs-pr#3950 -->

### <a name="supported-server-os-versions"></a>受支持的服务器 OS 版本

- **Windows Server 2019**：标准版、数据中心版<sup>[注释 1](#bkmk_note1)</sup>  
    （自 Configuration Manager 版本 1806 起。）

- **Windows Server 2016**：标准版、数据中心版<sup>[注释 1](#bkmk_note1)</sup>  

- **Windows Storage Server 2016**：标准版、工作组版  

- **Windows Server 2012 R2** (x64)：标准版、数据中心版<sup>[注释 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012 R2** (x64)

- **Windows Server 2012** (x64)：标准版、数据中心版<sup>[注释 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012** (x64)

#### <a name="server-core"></a>Server Core

以下版本专指 OS 的服务器核心安装。 <sup>[注 3](#bkmk_note3)</sup>  

Windows Server 半年频道版本是服务器核心安装，如 Windows Server 版本 1809。 作为 Configuration Manager 客户端，它们与相关的 Windows 10 半年频道版本一样受到相同的支持。 有关详细信息，请参阅 [Windows 10 支持](support-for-windows-10.md)。

- **Windows Server 2019** (x64) <sup>[注 2](#bkmk_note2)</sup>

- **Windows Server 2016** (x64) <sup>[注 2](#bkmk_note2)</sup>

- **Windows Server 2012 R2** (x64) <sup>[注 2](#bkmk_note2)</sup>

- **Windows Server 2012** (x64) <sup>[注 2](#bkmk_note2)</sup>

#### <a name="note-1"></a><a name="bkmk_note1"></a>注释 1

Configuration Manager 测试并支持 Windows Server Datacenter 版本，但没有 Windows Server 正式认证。 对于 Windows Server Datacenter Edition 专属问题，我们未提供 Configuration Manager 修补程序支持。 若要详细了解 Windows Server 认证计划，请参阅 [Windows Server Catalog](https://www.windowsservercatalog.com/)。

#### <a name="note-2"></a><a name="bkmk_note2"></a>注释 2

若要支持[客户端请求安装](../../clients/deploy/plan/client-installation-methods.md#client-push-installation)，请添加文件和存储服务服务器角色的文件服务器服务。 若要详细了解如何在服务器核心上安装 Windows 功能，请参阅[使用 Windows PowerShell cmdlet 安装角色、角色服务和功能](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#install-roles-role-services-and-features-by-using-windows-powershell-cmdlets)。  

#### <a name="note-3"></a><a name="bkmk_note3"></a>注释 3

任何版本的 Windows Server Core 都不支持新的软件中心应用。<!--SCCMDocs issue 683-->

## <a name="windows-embedded-computers"></a>Windows Embedded 计算机  

通过在设备上安装 Configuration Manager 客户端来管理 Windows Embedded 设备。 有关详细信息，请参阅[规划对 Windows Embedded 设备的客户端部署](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md)。  

### <a name="requirements-and-limitations"></a>要求和限制

- 未启用写入筛选器的 Windows Embedded 系统上支持所有客户端功能。  

- 使用下列其中一项的客户端受除电源管理以外的所有功能支持：  

  - 增强型写入筛选器 (EWF)

  - 基于 RAM 文件的写入筛选器 (FBWF)

  - 统一写入筛选器 (UWF)  

- 应用程序目录不受任何 Windows Embedded 设备支持。  

### <a name="supported-os-versions"></a>支持的操作系统版本  

- **Windows 10 企业版**（x86、x64）  

- **Windows 10 IoT 企业版**（x86、x64）  
    此版本包括长期服务频道 (LTSC)。 有关详细信息，请参阅 [Windows 10 IoT 企业版概述](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise)。<!--SCCMDocs issue 560-->  

- **Windows Embedded 8.1 Industry**（x86、x64）

- **Windows Embedded 8 标准版**（x86、x64）

- **Windows Thin PC**（x86、x64）

- **Windows Embedded POSReady 7**（x86、x64）

- **Windows Embedded Standard 7 SP1**（x86、x64）

## <a name="windows-ce-computers"></a>Windows CE 计算机

使用 Configuration Manager 附带的 Configuration Manager 移动设备旧客户端管理 Windows CE 设备。  

### <a name="requirements-and-limitations"></a>要求和限制

- 安装移动设备客户端需要 0.78 MB 的存储空间。 登录可能需要高达 256 KB 的额外存储空间。

- 这些移动设备的功能因平台和客户端类型而异。 有关支持的管理功能的详细信息，请参阅[选择设备管理解决方案](../choose-a-device-management-solution.md)。  

### <a name="supported-os-versions"></a>支持的操作系统版本

- Windows CE 7.0（ARM 和 x86 处理器）  

    > [!Note]
    > 对 Configuration Manager 中 Windows CE 7.0 的支持已弃用。 有关详细信息，请参阅 [Configuration Manager 客户端已删除和已弃用的项](../changes/deprecated/removed-and-deprecated-client.md)。

#### <a name="supported-languages-include"></a>支持的语言包括

- 中文（简体和繁体）

- 英语（美国）

- 法语（法国）

- 德语

- 意大利语

- 日语  

- 朝鲜语  

- 葡萄牙语（巴西）  

- 俄语  

- 西班牙语（西班牙）  

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a> 扩展的安全更新和 Configuration Manager

如果客户需要运行某些已停止支持的 Microsoft 旧产品，[扩展的安全更新 (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) 计划则是他们的终极选项。 例如，Windows 7。 它包括关键和/或重要安全更新（根据 [Microsoft 安全响应中心 (MSRC)](https://www.microsoft.com/msrc) 的定义），并且在超出产品的外延支持结束日期后最多可保存三年。

不支持将超出其支持生命周期的产品与 Configuration Manager 一起使用。 它包括 ESU 计划包含的所有产品。 通过 ESU 计划发布的安全更新将发布到 Windows Server Update Services (WSUS)。 这些更新将在 Configuration Manager 控制台中显示。 尽管不再支持将 ESU 计划包含的产品与 Configuration Manager 一起使用，但仍可使用 [Configuration Manager 当前分支的最新版本](../../servers/manage/updates.md#version-details)部署并安装通过此计划发布的 Windows 安全更新。 最新发行版还可用于将 Windows 10 部署到运行 Windows 7 的设备。

将不再在 ESU 计划包含的操作系统上测试与 Windows 软件更新管理或 OS 部署无关的客户端管理功能，并且不保证它们会继续工作。 强烈建议尽快升级或迁移到操作系统的最新版本，以获得客户端管理支持。

## <a name="mac-computers"></a>Mac 计算机  

使用适用于 macOS 的 Configuration Manager 客户端管理 Apple Mac 计算机。  

macOS 客户端安装包未与 Configuration Manager 媒体一同提供。 请从 Microsoft 下载中心下载，[Microsoft Endpoint Configuration Manager - macOS 客户端（64 位）](https://www.microsoft.com/download/details.aspx?id=100850)。  

有关详细信息，请参阅[如何将客户端部署到 Mac](../../clients/deploy/deploy-clients-to-macs.md)。  

### <a name="requirements-and-limitations"></a>要求和限制

- 不支持在根以外的其他帐户下的计算机上安装或运行适用于 macOS 的 Configuration Manager 客户端。 这样做可能会阻止关键服务正常运行。  

### <a name="supported-versions"></a>支持的版本

- macOS Catalina (10.15)  （需要 Configuration Manager 站点版本 1910 或更高版本，以及针对 macOS 版本 5.0.8742.1000 或更高版本的 Configuration Manager 客户端）

- **macOS Mojave (10.14)**

- **macOS High Sierra (10.13)**

## <a name="linux-and-unix-servers"></a>Linux 和 UNIX 服务器  

> [!Important]  
> Configuration Manager 版本 1902 不再支持将 Linux 和 UNIX 作为客户端。 已在[版本 1802](../changes/whats-new-in-version-1802.md#deprecation-announcement-for-linux-and-unix-client-support) 中宣布弃用。 请考虑使用 Microsoft Azure 管理来管理 Linux 服务器。 Azure 解决方案具有广泛的 Linux 支持（包括面向 Linux 的端到端补丁管理），在大多数情况下优于 Configuration Manager 的功能。

Linux 和 UNIX 客户端安装包未与 Configuration Manager 媒体一同提供。 可从 [Microsoft 下载中心](https://go.microsoft.com/fwlink/?LinkID=525184)下载**适用于其他操作系统的客户端**。 除了客户端安装包，客户端下载内容还包括在每台计算机上管理客户端安装的脚本。  

### <a name="requirements-and-limitations"></a>要求和限制

- 若要查看适用于 Linux 和 UNIX 客户端的操作系统文件依赖项，请参阅[将客户端部署到 Linux 和 UNIX 服务器的先决条件](../../clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_ClientDeployPrereqforLnU)。  

- 有关支持的 Linux 或 UNIX 管理功能概述，请参阅[如何将客户端部署到 UNIX 和 Linux 服务器](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md)。  

- 对于支持的 Linux 和 UNIX 版本，列出的版本包括所有后续的次要版本。 例如，CentOS 6 版本包括 CentOS 6.3。 同样，对使用 Service Pack 的操作系统（例如 SUSE Linux Enterprise Server 11 SP1）的支持包括该操作系统版本的后续 Service Pack。  

- 有关客户端安装包和通用代理的信息，请参阅[如何将客户端部署到 UNIX 和 Linux 服务器](../../clients/deploy/deploy-clients-to-unix-and-linux-servers.md)。  

### <a name="supported-versions"></a>支持的版本

使用指示的 .tar 文件，支持以下版本。  

#### <a name="aix"></a>AIX  

|版本|TAR 文件|  
|-|-|  
|版本 6.1（电源）|ccm-Aix61ppc.&lt;build\>.tar|  
|版本 7.1（电源）|ccm-Aix71ppc.&lt;build\>.tar|  

#### <a name="centos"></a>CentOS  

|版本|TAR 文件|  
|-|-|  
|版本 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="debian"></a>Debian  

|版本|TAR 文件|  
|-|-|  
|版本 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 7 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 7 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 8 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 8 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="hp-ux"></a>HP-UX  

|版本|TAR 文件|  
|-|-|  
|版本 11iv3 IA64|ccm-HpuxB.11.31i64.&lt;build\>.tar|  

#### <a name="oracle-linux"></a>Oracle Linux  

|版本|TAR 文件|  
|-|-|  
|版本 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="red-hat-enterprise-linux-rhel"></a>Red Hat Enterprise Linux (RHEL)  

|版本|TAR 文件|  
|-|-|  
|版本 5 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 5 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 6 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 6 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 7 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="solaris"></a>Solaris  

|版本|TAR 文件|  
|-|-|  
|版本 10 x86|ccm-Sol10x86.&lt;build\>.tar|  
|版本 10 SPARC|ccm-Sol10sparc.&lt;build\>.tar|  
|版本 11 x86|ccm-Sol11x86.&lt;build\>.tar|  
|版本 11 SPARC|ccm-Sol11sparc.&lt;build\>.tar|  

#### <a name="suse-linux-enterprise-server-sles"></a>SUSE Linux Enterprise Server (SLES)  

|版本|TAR 文件|  
|-|-|  
|版本 10 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 10 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 11 SP1 x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 11 SP1 x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 12 x64|ccm-Universalx64.&lt;build\>.tar|  

#### <a name="ubuntu"></a>Ubuntu  

|版本|TAR 文件|  
|-|-|  
|版本 10.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 10.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 12.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 12.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 14.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 14.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  
|版本 16.04 LTS x86|ccm-Universalx86.&lt;build\>.tar|  
|版本 16.04 LTS x64|ccm-Universalx64.&lt;build\>.tar|  


## <a name="on-premises-mdm"></a><a name="bkmk_OnpremOS"></a> 本地 MDM

Configuration Manager 提供内置功能来管理本地移动设备，无需安装客户端软件。 有关详细信息，请参阅[使用本地基础结构管理移动设备](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)。  

### <a name="supported-operating-systems"></a>支持的操作系统

- **Windows 10 Pro**（x86、x64）  

- **Windows 10 Pro Enterprise**（x86、x64）  

- **Windows 10 IoT 企业版**（x86、x64）  
    此版本包括长期服务频道 (LTSC)。 有关详细信息，请参阅 [Windows 10 IoT 企业版概述](https://docs.microsoft.com/windows/iot-core/windows-iot-enterprise)。<!--SCCMDocs issue 560-->  

- **Windows 10 IoT 移动企业版**  

- **Surface Hub 的 Windows 10 协同版**  

- **Windows 10 移动版**  

- **Windows 10 移动企业版**  

    > [!Note]
    > Configuration Manager 对 Windows 10 移动版和 Windows 10 移动企业版的支持已弃用。 有关详细信息，请参阅 [Configuration Manager 客户端已删除和已弃用的项](../changes/deprecated/removed-and-deprecated-client.md)。


## <a name="exchange-server-connector"></a><a name="bkmk_ExSrvConOS"></a> Exchange Server 连接器  

Configuration Manager 支持连接到 Exchange Server 的设备的有限管理，无需安装 Configuration Manager 客户端。 有关详细信息，请参阅[使用 Configuration Manager 和 Exchange 管理移动设备](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)。  

### <a name="supported-versions-of-exchange-server"></a>受支持的 Exchange Server 版本

- **Exchange Online (Office 365)** ：此版本包括 Business Productivity Online Standard Suite  

- **Exchange Server 2016**  

- **Exchange Server 2013**  

- **Exchange Server 2010 SP1** 或 **Exchange Server 2010 SP2**
