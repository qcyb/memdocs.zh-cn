---
title: 客户端设置
titleSuffix: Configuration Manager
description: 了解用于控制客户端行为的默认和自定义设置
ms.date: 08/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: reference
ms.assetid: f7560876-8084-4570-aeab-7fd44f4ba737
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8045df681560972a353e08ee43c10b6ae86dc50f
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693414"
---
# <a name="about-client-settings-in-configuration-manager"></a>关于 Configuration Manager 中的客户端设置

适用范围：Configuration Manager (Current Branch)

通过“管理”工作区中的“客户端设置”节点来管理 Configuration Manager 控制台中的所有客户端设置 。 Configuration Manager 附带一组默认设置。 如果更改默认的客户端设置，则这些设置将应用于层次结构中的所有客户端。 你也可以配置自定义客户端设置，当将这些设置分配给集合时，它们将替代默认客户端设置。 有关详细信息，请参阅[如何配置客户端设置](configure-client-settings.md)。

下列部分更详细地描述了设置和选项。  


## <a name="background-intelligent-transfer-service-bits"></a>后台智能传输服务(BITS)  

### <a name="limit-the-maximum-network-bandwidth-for-bits-background-transfers"></a>限制 BITS 后台传输的最大网络带宽

当此选项为“是”时，客户端使用 BITS 带宽限制。 若要在此组中配置其他设置，则必须启用此设置。

### <a name="throttling-window-start-time"></a>限制时段开始时间

指定 BITS 限制时段的本地开始时间。  

### <a name="throttling-window-end-time"></a>限制时段结束时间

指定 BITS 限制时段的本地结束时间。 如果结束时间与“限制时段开始时间”相等，则会始终启用 BITS 限制。  

### <a name="maximum-transfer-rate-during-throttling-window-kbps"></a>限制时段期间的最大传输速率(Kbps)

指定客户端在此时段可以使用的最大传输速率。  

### <a name="allow-bits-downloads-outside-the-throttling-window"></a>允许 BITS 在限制时段外下载

允许客户端使用指定时段外的单独 BITS 设置。  

### <a name="maximum-transfer-rate-outside-the-throttling-window-kbps"></a>限制时段外的最大传输速率(Kbps)

指定客户端可在 BITS 限制时段外使用的最大传输速率。  



## <a name="client-cache-settings"></a>客户端缓存设置

### <a name="configure-branchcache"></a>配置 BranchCache

设置客户端计算机的 [Windows BranchCache](../../plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache
)。 若要允许客户端上的 BranchCache 缓存，请将“启用 BranchCache”设置为“是”。

- **启用 BranchCache**：在客户端计算机上启用 BranchCache。

- **最大 BranchCache 缓存大小(占磁盘的百分比)** ：允许 BranchCache 使用的磁盘百分比。

> [!TIP]
> 如果将“配置 BranchCache”设置为“否”，则 Configuration Manager 不会配置任何 BranchCache 设置。
>
> 若要禁用 BranchCache，请将“配置 BranchCache”设置为“是”，然后将“启用 BranchCache”设置为“否”。<!-- 6244852 -->

### <a name="configure-client-cache-size"></a>配置客户端缓存大小

Windows 计算机上的 Configuration Manager 客户端缓存会存储用于安装应用程序和程序的临时文件。 如果此选项设置为“否”，则默认大小为 5,120 MB。

如果选择“是”，则指定：

- **最大缓存大小 (MB)**
- **最大缓存大小(占磁盘的百分比)** ：客户端缓存大小可扩展到最大大小（按 MB 或磁盘百分比指定），以较小者为准。

### <a name="enable-as-peer-cache-source"></a>启用为对等缓存源

> [!Note]  
> 在版本 1902 及更早版本中，此设置称为“在完整的 OS 中启用 Configuration Manager 客户端以共享内容”。 此设置的行为不会发生变化。

启用用于 Configuration Manager 客户端的[对等缓存](../../plan-design/hierarchy/client-peer-cache.md)。 选择“是”，然后指定客户端通过其与对等计算机通信的端口。

- **用于初始网络广播的端口**（默认 UDP 8004）：Configuration Manager 在 Windows PE 或完整的 Windows OS 中使用此端口。 Windows PE 中的任务序列引擎先发送广播来获取内容位置，再启动任务序列。<!--SCCMDocs issue 910-->

- **用于从对等机下载内容的端口**（默认 TCP 8003）：Configuration Manager 会自动配置 Windows 防火墙规则以允许此流量。 如果使用其他防火墙，则必须手动配置规则以允许此流量。  

    有关详细信息，请参阅[用于连接的端口](../../plan-design/hierarchy/ports.md#BKMK_PortsClient-ClientWakeUp)。  

### <a name="minimum-duration-before-cached-content-can-be-removed-minutes"></a>可以删除缓存内容前的最短持续时间（以分钟为单位）

<!--4485509-->
从版本 1906 开始，可以指定 Configuration Manager 客户端保留缓存内容的最短时间。 此客户端设置定义了在需要更多空间的情况下，Configuration Manager 代理可以从缓存中删除内容之前应等待的最短时间。

默认情况下，此值为 1,440 分钟（24 小时）。
此设置的最大值为 10,080 分钟（1 周）。

使用此设置，可以更好地控制不同类型设备上的客户端缓存。 可以减小具有小型硬盘驱动器的客户端的值，并且在另一个部署运行之前不需要保留现有内容。


## <a name="client-policy"></a>客户端策略  

### <a name="client-policy-polling-interval-minutes"></a>客户端策略轮询间隔(分钟)

指定以下 Configuration Manager 客户端下载客户端策略的频率：

- Windows 计算机（例如，台式机、服务器、便携计算机）  
- Configuration Manager 注册的移动设备  
- Mac 计算机  
- 运行 Linux 或 UNIX 的计算机  

此值默认为 60 分钟。 减小此值会增加客户端对站点的轮询频率。 如果有许多客户端，此行为可能会对站点性能产生负面影响。 [大小和缩放指南](../../plan-design/configs/size-and-scale-numbers.md)是以默认值为依据。 增加此值会减少客户端对站点的轮询频率。 客户端需要更长时间来下载和处理客户端策略的任何更改（包括新部署）。<!-- SCCMDocs issue 823 -->

### <a name="enable-user-policy-on-clients"></a>在客户端上启用用户策略

如果此选项设置为“是”并且使用[用户发现](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)，客户端会接收面向登录用户的应用程序和程序。  

如果此设置为“否”，则用户不会收到你为用户部署的所需应用程序。 用户也不会收到用户策略中的任何其他管理任务。  

当用户的计算机位于 Intranet 或 Internet 时，此设置会应用到用户。 如果还想在 Internet 上启用用户策略，则此设置必须为“是”。  

> [!Note]  
> 从版本 1906 开始，更新后的客户端自动使用管理点进行用户可用应用程序部署。 无法安装新的应用程序目录角色。
>
> 如果仍使用应用程序目录，它会从站点服务器接收用户的可用软件列表。 因此，此设置不必为“是”，用户也可从应用程序目录中查看和请求应用程序。 如果此设置为“否”，则用户无法安装他们在应用程序目录中看到的应用程序。  

### <a name="enable-user-policy-requests-from-internet-clients"></a>启用来自 Internet 客户端的用户策略请求

将此选项设置为“是”，以便用户接收到基于 Internet 的计算机上的用户策略。 此外还需要满足以下要求：  

- 将客户端和站点配置为[基于 Internet 的客户端管理](../manage/plan-internet-based-client-management.md)或[云管理网关](../manage/cmg/plan-cloud-management-gateway.md)。  

- “在客户端上启用用户策略”设置为“是”。  

- 基于 Internet 的管理点可通过使用 Windows 身份验证（Kerberos 或 NTLM）成功地对用户进行身份验证。 有关详细信息，请参阅[来自 Internet 的客户端通信的注意事项](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)。  

- 云管理网关可使用 Azure Active Directory 成功对用户进行身份验证。 有关详细信息，请参阅[部署用户可用的应用程序](../../../apps/deploy-use/deploy-applications.md#deploy-user-available-applications)。

如果将此选项设置为“否”，或不满足之前的任何一个条件，则 Internet 上的计算机将仅收到计算机策略。 在此情况下，用户仍然能够查看、请求和安装基于 Internet 的应用程序目录中的应用程序。 如果此设置为“否”，但“在客户端上启用用户策略”为“是”，则在计算机连接到 Intranet 之前，用户不会收到用户策略  。  

> [!NOTE]  
> 对于基于 Internet 的客户端管理，来自用户的应用程序批准请求不需要用户策略或用户身份验证。 云管理网关不支持应用程序批准请求。  

### <a name="enable-user-policy-for-multiple-user-sessions"></a>为多个用户会话启用用户策略

<!--4737447-->

适用于版本 1910

默认情况下，此设置处于禁用状态。 即使启用了用户策略，从版本 1906 开始，客户端在任何允许多个并发活动用户会话的设备上也默认禁用这些策略。 例如，[Windows 虚拟桌面](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#windows-virtual-desktop)中的终端服务器或 Windows 10 企业版多会话。

客户端仅在新的安装期间检测到此类设备时才会禁用用户策略。 对于已更新到 1906 或更高版本的现有此类客户端而言，以前的行为仍然存在。 在现有设备上，即使检测到设备支持多个用户会话，它也会配置用户策略设置。

如果在此方案中需要用户策略，并且接受任何潜在的性能影响，请启用此客户端设置。


## <a name="cloud-services"></a>云服务

### <a name="allow-access-to-cloud-distribution-point"></a>允许访问云分发点

将此选项设置为“是”，以便客户端从云分发点获取内容。 此设置不需要设备基于 Internet。

### <a name="automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory"></a>在 Azure Active Directory 中自动注册已加入域的新 Windows 10 设备

配置 Azure Active Directory 支持混合联接时，Configuration Manager 会针对此功能配置 Windows 10 设备。 有关详细信息，请参阅[如何配置混合 Azure Active Directory 联接设备](/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)。

### <a name="enable-clients-to-use-a-cloud-management-gateway"></a>允许客户端使用云管理网关

默认情况下，所有 Internet 漫游客户端均使用任何可用的[云管理网关](../manage/cmg/plan-cloud-management-gateway.md)。 有关何时将此设置配置为“否”的一个示例就是了解服务的使用情况，例如在试点项目期间或为了节省成本。



## <a name="compliance-settings"></a>符合性设置  

### <a name="enable-compliance-evaluation-on-clients"></a>启用在客户端上的符合性评估

将此选项设置为“是”，以在此组中配置其他设置。

### <a name="schedule-compliance-evaluation"></a>计划符合性评估

选择“计划”，创建配置基线部署的默认计划。 可在“部署配置基线”对话框中为每个基线配置此值。  

### <a name="enable-user-data-and-profiles"></a>启用用户数据和配置文件

如果希望部署[用户数据和配置文件](../../../compliance/deploy-use/create-user-data-and-profiles-configuration-items.md)配置项目，请选择“是”。



## <a name="computer-agent"></a>计算机代理  

### <a name="user-notifications-for-required-deployments"></a>所需部署的用户通知

有关以下三个设置的详细信息，请参阅[所需部署的用户通知](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)：

- **部署截止时间大于 24 小时，每(小时)提醒用户**
- **部署截止时间少于 24 小时，每(小时)提醒用户**
- **部署截止时间少于 1 小时，每(分钟)提醒用户**

### <a name="default-application-catalog-website-point"></a>默认应用程序目录网站点

> [!Important]  
> 从 Current Branch 版本 1806 开始，不支持应用程序目录的 Silverlight 用户体验。 自版本 1906 起，更新后的客户端自动使用管理点进行用户可用的应用程序部署。 仍然无法安装新的应用程序目录角色。 版本 1910 已终止对应用程序目录角色的支持。  
>
> 有关详细信息，请参阅下列文章：
>
> - [配置软件中心](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已删除和已弃用的功能](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Configuration Manager 使用此设置将用户连接到软件中心中的应用程序目录。 选择“设置网站”，指定托管应用程序目录网站点的服务器。 输入其 NetBIOS 名称或 FQDN，指定自动检测，或指定自定义部署的 URL。 在大多数情况下，自动检测是最佳选择。

### <a name="add-default-application-catalog-website-to-internet-explorer-trusted-sites-zone"></a>向 Internet Explorer 受信任的站点区域添加默认应用程序目录网站

> [!Important]  
> 从 Current Branch 版本 1806 开始，不支持应用程序目录的 Silverlight 用户体验。 自版本 1906 起，更新后的客户端自动使用管理点进行用户可用的应用程序部署。 仍然无法安装新的应用程序目录角色。 版本 1910 已终止对应用程序目录角色的支持。  
>
> 有关详细信息，请参阅下列文章：
>
> - [配置软件中心](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [已删除和已弃用的功能](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

如果此选项为“是”，则客户端会将当前默认的应用程序目录网站 URL 自动添加到 Internet Explorer 受信任的站点区域。  

此设置确保不启用 Internet Explorer 的“保护模式”设置。 如果启用“保护模式”，则 Configuration Manager 客户端可能无法安装应用程序目录中的应用程序。 默认情况下，受信任的站点区域还支持应用程序目录用户登录，这需要 Windows 身份验证。  

如果将此选项保留为“否”，则 Configuration Manager 客户端可能无法安装应用程序目录中的应用程序。 替代方法是在客户端使用的应用程序目录 URL 的另一个区域中配置这些 Internet Explorer 设置。  

### <a name="allow-silverlight-applications-to-run-in-elevated-trust-mode"></a>允许 Silverlight 应用程序在提升的信任模式下运行

> [!Important]  
> 客户端不自动安装 Silverlight。
>
> 从版本 1806 开始，应用程序目录网站点的 Silverlight 用户体验不再受支持。 用户应使用新的软件中心。 有关详细信息，请参阅[配置软件中心](../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)。  

此设置必须为“是”，以便用户使用应用程序目录。  

如果更改此设置，则当用户下次加载其浏览器或刷新其当前打开的浏览器窗口时，更改将生效。  

有关此设置的详细信息，请参阅 [Microsoft Silverlight 5 的证书以及应用程序目录所需的提升的信任模式](../../../apps/plan-design/security-and-privacy-for-application-management.md#BKMK_CertificatesSilverlight5)。  

### <a name="organization-name-displayed-in-software-center"></a>软件中心中显示的组织名称

键入用户在软件中心中看到的名称。 此品牌信息有助于用户将此应用程序识别为受信任的源。 有关此设置优先级的详细信息，请参阅[软件中心品牌打造](../../../apps/plan-design/plan-for-software-center.md#brand-software-center)。  

### <a name="use-new-software-center"></a>使用新的软件中心

默认设置为“是”。

如果将此选项设置为“是”，则所有客户端计算机均使用软件中心。 软件中心显示你部署到用户或设备的软件、软件更新和任务序列。

### <a name="enable-communication-with-health-attestation-service"></a>启用与运行状况证明服务的通信

将此选项设置为“是”，以便 Windows 10 设备使用[运行状况证明](../../servers/manage/health-attestation.md)。 启用此设置时，还可配置以下设置。

### <a name="use-on-premises-health-attestation-service"></a>使用本地运行状况证明服务

将此选项设置为“是”，以便设备使用本地服务。 设置为“否”，以便设备使用 Microsoft 基于云的服务。  

### <a name="install-permissions"></a>安装权限

配置用户安装软件、软件更新和任务序列的方式：  

- **所有用户**：除“来宾”之外的拥有任何权限的用户。  

- **仅限管理员**：用户必须是本地管理员组的成员。  

- **仅限管理员和主要用户**：用户必须是本地管理员组的成员或计算机的主要用户。  

- **无用户**：登录到客户端计算机的用户无法安装软件、软件更新和任务序列。 计算机的必需部署始终在截止日期安装。 用户无法通过软件中心安装软件。  

### <a name="suspend-bitlocker-pin-entry-on-restart"></a>重新启动时挂起 Bitlocker PIN 项

如果计算机需要 BitLocker PIN 条目，则在软件安装之后重启计算机时，此选项可以略过输入 PIN 的要求。  

- **始终**：在安装需要重启的软件并重启计算机之后，Configuration Manager 会临时暂停 BitLocker。 仅当 Configuration Manager 重启计算机时，此设置才适用。 当用户重启计算机时，此设置不会暂停输入 BitLocker PIN 的要求。 在 Windows 启动后恢复 BitLocker PIN 输入要求。

- **从不**：在安装需要重启的软件之后，Configuration Manager 不会暂停 BitLocker。 在此情况下，直到用户输入 PIN 来完成标准启动过程并加载 Windows，才能完成软件安装。

### <a name="additional-software-manages-the-deployment-of-applications-and-software-updates"></a>其他用于管理应用程序部署和软件更新的软件

只有在下列条件之一成立时才启用此选项：  

- 你使用需要启用此设置供应商解决方案。  

- 使用 Configuration Manager 软件开发工具包 (SDK)，管理客户端代理通知以及应用程序和软件更新的安装。  

> [!WARNING]  
> - 如果在任一条件都不适用时选择此选项，则客户端不会安装软件更新和所需的应用程序。 此设置不会阻止用户从软件中心安装可用软件（包括应用程序、包和任务序列）。  
> -  若启用此设置，客户端上不会出现新软件或所需软件的 toast 通知。 <!--6347668-->

### <a name="powershell-execution-policy"></a>PowerShell 执行策略

配置 Configuration Manager 客户端运行 Windows PowerShell 脚本的方式。 这些脚本可能用于检测配置项目中的符合性设置。 还可以在部署中以标准脚本的形式发送脚本。  

- **不使用**：Configuration Manager 客户端在客户端计算机上不使用 Windows PowerShell 配置，以便未签名的脚本可以运行。  

- **受限**：Configuration Manager 客户端在客户端计算机上使用当前的 PowerShell 配置。 这些配置可确定未签名的脚本是否可以运行。  

- **已全部签名**：只有当受信任的发行者对脚本进行了签名，Configuration Manager 客户端才能运行这些脚本。 系统将应用此限制，而与客户端计算机上的当前 PowerShell 配置无关。  

此选项至少需要 Windows PowerShell 版本 2.0。 默认值为“已全部签名”。  

> [!TIP]  
> 如果由于此客户端设置的缘故而无法运行未签名的脚本，则 Configuration Manager 会用以下方法报告此错误：  
>
> - 控制台中的“监视”工作区显示部署状态错误 ID“0x87D00327”。 还显示“脚本未签名”说明。  
> - 报表显示错误类型“发现错误”。 然后报表显示错误代码“0x87D00327”和“脚本未签名”说明，或错误代码“0x87D00320”和“尚未安装脚本宿主”说明。 其中一个示例报表为：“资产配置基线中配置项目的错误详细信息”。  
> - DcmWmiProvider.log 文件显示消息：**脚本未签名(错误: 87D00327；源: CCM)** 。  

### <a name="show-notifications-for-new-deployments"></a>显示关于新部署的通知

选择“是”可显示未来一周内的部署的通知。 此消息会在客户端代理每次启动时显示。

### <a name="disable-deadline-randomization"></a>禁用截止时间随机化

达到部署截止时间后，此设置确定客户端是否使用长达两个小时的激活延迟来安装所需的软件更新。 默认情况下，激活延迟处于禁用状态。  

对于虚拟桌面基础结构 (VDI) 情况，此延迟有助于为具有多个虚拟机的主机分发 CPU 处理和数据传输。 即使不使用 VDI，许多客户端同时安装相同更新也可能会增加站点服务器上的 CPU 使用率，造成负面影响。 此行为还会减慢分发点的速度，大大减小可用网络带宽。  

如果达到部署截止时间时，客户端必需毫不延迟地安装所需软件更新，请将此设置配置为“是”。

### <a name="grace-period-for-enforcement-after-deployment-deadline-hours"></a>部署截止日期后强制的宽限期（小时）

若要宽限用户更多时间（超过截止时间）来安装所需的应用程序或软件更新部署，请设置此选项的值。 此宽限期适用于计算机延期关闭以及用户需要安装大量应用程序或更新部署的情况。 例如，如果用户休假回来，客户端安装的应用程序部署已过期，而需要等待很长时间，此设置将有所帮助。

设置介于 0 和 120 小时之间的宽限期。 将此设置和“根据用户偏好延迟此强制部署”的部署属性结合使用。 有关详细信息，请参阅[部署应用程序](../../../apps/deploy-use/deploy-applications.md#delay-enforcement-with-a-grace-period)。


### <a name="enable-endpoint-analytics-data-collection"></a>启用终结点分析数据收集

在客户端上启用本地数据收集以上传到终结点分析。 若要配置用于本地数据收集的设备，请设置为“是”。 若要禁用本地数据收集，请设置为“否”。 有关详细信息，请参阅[向终结点分析注册 Configuration Manager 设备](../../../../analytics/enroll-configmgr.md)。

## <a name="computer-restart"></a>计算机重启

有关这些设置的详细信息，请参阅[设备重启通知](device-restart-notifications.md)。<!-- 7182335 -->

## <a name="delivery-optimization"></a>传递优化

<!-- 1324696 -->
使用 Configuration Manager 边界组来定义和控制跨公司网络和到远程办公室的内容分发。 [Windows 传递优化](/windows/deployment/update/waas-delivery-optimization)是一种基于云的对等技术，用于在 Windows 10 设备之间共享内容。 配置传递优化以在对等方之间共享内容时使用边界组。

> [!Note]
> - 传递优化仅可用于 Windows 10 客户端。
> - 要利用其对等功能，需具有对传递优化云服务的 Internet 访问。 有关所需的 Internet 终结点的信息，请参阅[有关传递优化的常见问题](/windows/deployment/update/waas-delivery-optimization#frequently-asked-questions)。
> - 将 CMG 用于内容存储时，如果“在有可用内容时下载增量内容”[客户端设置](#allow-clients-to-download-delta-content-when-available)已启用，则第三方更新内容不会下载到客户端。 <!--6598587--> 

### <a name="use-configuration-manager-boundary-groups-for-delivery-optimization-group-id"></a>将 Configuration Manager 边界组用于交付优化组 ID

选择“是”将边界组标识符用作客户端上的传递优化组标识符。 当客户端与传递优化云服务进行通信时，它使用此标识符来查找具有内容的对等方。 启用此设置还会将目标客户端上的传递优化下载模式设置为“组(2)”选项。

> [!Note]
> Microsoft 建议让客户端通过本地策略（而不是通过组策略）来配置此设置。 这样就可将边界组标识符设置为客户端上的传递优化组标识符。 有关详细信息，请参阅[传递优化](../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#delivery-optimization)。

### <a name="enable-devices-managed-by-configuration-manager-to-use-microsoft-connected-cache-servers-for-content-download"></a>使 Configuration Manager 托管的设备可使用 Microsoft Connected Cache 服务器来下载内容

<!--3555764-->
选择“是”以允许客户端从用作 Microsoft Connected Cache 服务器的本地分发点下载内容。 有关详细信息，请参阅 [Configuration Manager 中的 Microsoft Connected Cache](../../plan-design/hierarchy/microsoft-connected-cache.md)。


## <a name="endpoint-protection"></a>Endpoint Protection

> [!Tip]
> 除了以下信息，还可以在[示例方案：使用 Endpoint Protection 来保护计算机免受恶意软件攻击](../../../protect/deploy-use/scenarios-endpoint-protection.md)中查找关于使用 Endpoint Protection 客户端设置的详细信息。

### <a name="manage-endpoint-protection-client-on-client-computers"></a>在客户端计算机上管理 Endpoint Protection 客户端

若要在层次结构中的计算机上管理现有的 Endpoint Protection 和 Windows Defender 客户端，请选择“是”。  

如果已经安装了 Endpoint Protection 客户端并且想要使用 Configuration Manager 来管理它，请选择此选项。 此单独安装包括使用 Configuration Manager 应用程序或包和程序的脚本化进程。 Windows 10 设备不需要安装 Endpoint Protection 代理。 但是，这些设备仍需启用“管理客户端计算机上的 Endpoint Protection 客户端”。 <!--503654-->

### <a name="install-endpoint-protection-client-on-client-computers"></a>在客户端计算机上安装 Endpoint Protection 客户端

选择“是”可在尚未运行该客户端的客户端计算机上安装和启用 Endpoint Protection 客户端。 Windows 10 客户端不需要安装 Endpoint Protection 代理。  

> [!NOTE]  
> 如果已安装 Endpoint Protection 客户端，选择“否”不会卸载 Endpoint Protection 客户端。 要卸载 Endpoint Protection 客户端，请将“在客户端计算机上管理 Endpoint Protection 客户端”客户端设置设为“否”。 然后，部署包和程序以卸载 Endpoint Protection 客户端。  

### <a name="allow-endpoint-protection-client-installation-and-restarts-outside-maintenance-windows-maintenance-windows-must-be-at-least-30-minutes-long-for-client-installation"></a>允许安装 Endpoint Protection 客户端和在维护时段以外重启。 维护时段必须至少为 30 分钟，以便安装客户端

将此选项设置为“是”，使用维护时段替代典型的安装行为。 此设置符合可确保安全的系统维护优先级业务要求。

### <a name="for-windows-embedded-devices-with-write-filters-commit-endpoint-protection-client-installation-requires-restarts"></a>对于带有写入筛选器的 Windows Embedded 设备，提交 Endpoint Protection 客户端安装（需要重新启动）

选择“是”以对 Windows Embedded 设备禁用写入筛选器并重启该设备。 此操作在设备上提交安装。  

如果选择“否”，则客户端在临时覆盖区上安装，当设备重启时清除。 在此情况下，Endpoint Protection 客户端直到另一个安装将更改提交到设备时才会完全安装。 默认为此配置。  

### <a name="suppress-any-required-computer-restarts-after-the-endpoint-protection-client-is-installed"></a>在安装 Endpoint Protection 客户端后取消任何所需的计算机重启

安装 Endpoint Protection 客户端后，请选择“是”取消重启计算机。  

> [!IMPORTANT]  
> 如果 Endpoint Protection 客户端需要重启计算机，并且此设置为“否”，则计算机都会重启，且与任何配置的维护时段无关。  

### <a name="allowed-period-of-time-users-can-postpone-a-required-restart-to-complete-the-endpoint-protection-installation-hours"></a>允许用户将要求的重启推迟一段时间，以完成 Endpoint Protection 安装（小时）

如果在安装 Endpoint Protection 客户端后需要重启，该设置会指定用户可以延迟所需重启的小时数。 此设置要求你禁用以下设置：**在安装 Endpoint Protection 客户端后取消任何所需的计算机重启**。

### <a name="disable-alternate-sources-such-as-microsoft-windows-update-microsoft-windows-server-update-services-or-unc-shares-for-the-initial-definition-update-on-client-computers"></a>禁用替代源（例如 Microsoft Windows Update、Microsoft Windows Server Update Services 或 UNC 共享）来更新客户端计算机的初始定义

如果希望 Configuration Manager 在客户端计算机上仅安装初始定义更新，请选择“是”。 此设置有助于在初次安装定义更新期间避免不必要的网络连接并减小网络带宽。  



## <a name="enrollment"></a>注册

### <a name="polling-interval-for-mobile-device-legacy-clients"></a>移动设备旧客户端的轮询间隔

选择“设置间隔”，指定旧移动设备轮询策略的时间长度（以分钟或小时为单位）。 这些设备包括 Windows CE、macOS，以及 Unix 或 Linux 等平台。

### <a name="polling-interval-for-modern-devices-minutes"></a>新式设备的轮询间隔（分钟）

输入新式设备轮询策略的分钟数。 此设置适用于通过本地移动设备管理托管的 Windows 10 设备。

### <a name="allow-users-to-enroll-mobile-devices-and-mac-computers"></a>允许用户注册移动设备和 Mac 计算机

要启用基于用户注册旧设备，请将此选项设置为“是”，然后配置以下设置：

- **注册配置文件**：选择“设置配置文件”，创建或选择一个注册配置文件。 有关详细信息，请参阅[为注册配置客户端设置](deploy-clients-to-macs.md#configure-client-settings)。

### <a name="allow-users-to-enroll-modern-devices"></a>允许用户注册新式设备

要启用基于用户注册新式设备，请将此选项设置为“是”，然后配置以下设置：

- **新式设备注册配置文件**：选择“设置配置文件”，创建或选择一个注册配置文件。 有关详细信息，请参阅[创建允许用户注册新式设备的注册配置文件](../../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md#bkmk_createProf)。



## <a name="hardware-inventory"></a>硬件清单  

### <a name="enable-hardware-inventory-on-clients"></a>针对客户端启用硬件清单

默认情况下，此设置为“是”。 有关详细信息，请参阅[硬件清单简介](../manage/inventory/introduction-to-hardware-inventory.md)。

### <a name="hardware-inventory-schedule"></a>硬件清单计划

选择“计划”，调整客户端运行硬件清单周期的频率。 默认情况下，该周期为每七天执行一次。

### <a name="maximum-random-delay-minutes"></a>最长随机延迟（分钟）

指定最大分钟数，以便 Configuration Manager 客户端从定义的计划中随机化硬件清单周期。 这种跨所有客户端的随机化操作有助于实现站点服务器上清单处理的负载均衡。 可以指定介于 0 到 480 分钟之间的任何值。 默认情况下，此值设置为 240 分钟（4 小时）。

### <a name="maximum-custom-mif-file-size-kb"></a>最大自定义 MIF 文件大小(KB)

指定在硬件清单周期过程中客户端收集的每个自定义管理信息格式 (MIF) 文件所允许的最大大小 (KB)。 Configuration Manager 硬件清单代理不会处理任何超过此大小的自定义 MIF 文件。 可指定介于 1 KB 到 5,120 KB 之间的大小。 默认情况下，此值设置为 250 KB。 此设置不影响常规硬件清单数据文件的大小。  

> [!NOTE]  
> 此设置仅在默认客户端设置中可用。  

### <a name="hardware-inventory-classes"></a>硬件清单类

选择“设置类”可扩展从客户端中收集的硬件信息，而无需手动编辑 sms_def.mof 文件。 有关详细信息，请参阅[如何配置硬件清单](../manage/inventory/configure-hardware-inventory.md)。  

### <a name="collect-mif-files"></a>收集 MIF 文件

使用此设置指定是否在硬件清单过程中从 Configuration Manager 客户端收集 MIF 文件。  

为了按照硬件清单收集 MIF 文件，此文件必须位于客户端计算机上的正确位置。 默认情况下，这些文件位于下列路径中：  

- IDMIF 文件应位于 Windows\System32\CCM\Inventory\Idmif 文件夹中。

- NOIDMIF 文件应位于 Windows\System32\CCM\Inventory\Noidmif 文件夹中。

> [!NOTE]  
> 此设置仅在默认客户端设置中可用。

## <a name="metered-internet-connections"></a>按流量计费的 Internet 连接

管理 Windows 8 及更高版本计算机如何使用按流量计费的 Internet 连接与 Configuration Manager 通信。 Internet 提供商有时会根据你通过按流量计费的 Internet 连接发送和接收的数据量来计费。

> [!NOTE]
> 配置的客户端设置不适用于以下情况：
>
> - 如果计算机采用漫游数据连接，Configuration Manager 客户端不会执行需要将数据传输到 Configuration Manager 站点的任何任务。  
> - 如果 Windows 网络连接属性配置为不按流量计费，Configuration Manager 客户端的行为类似于连接不按流量计费，因此会将数据传输至站点。  

### <a name="client-communication-on-metered-internet-connections"></a>客户端通过按流量计费的 Internet 连接进行的通信

为此设置选择下列某个选项：

- **允许**：除非客户端设备正在使用漫游数据连接，否则允许通过按流量计费的 Internet 连接进行所有客户端通信。

- **限制**：客户端只对以下行为通过按流量计费的 Internet 连接进行通信：

  - 下载客户端策略

  - 发送客户端状态消息

  - 向软件中心请求安装软件

  - 在安装截止时间下载必需部署的其他策略和内容

  如果客户端达到按流量计费的 Internet 连接的数据传输限制，客户端就不再与站点通信。

- **阻止**：如果设备使用按流量计费的 Internet 连接，Configuration Manager 客户端就不会尝试与站点通信。 此选项为默认设置。

> [!IMPORTANT]
> 客户端始终允许从软件中心安装软件，与按流量计费的 Internet 连接设置无关。 如果用户在设备处于按流量计费的网络中时请求安装软件，软件中心会尊重用户的意图。<!-- MEMDocs#285 -->

自版本 2006 起，如果你将此客户端设置配置为“允许”或“限制”时，客户端安装和更新都可以进行。 借助此行为，客户端可以不断更新，但仍管理通过按流量计费的网络进行的客户端通信。 可以在客户端安装期间使用 ccmsetup 参数 /AllowMetered 来控制此行为。 有关详细信息，请参阅[关于客户端安装参数和属性](../../clients/deploy/about-client-installation-properties.md#allowmetered)。<!--6976145-->

## <a name="power-management"></a>电源管理  

### <a name="allow-power-management-of-devices"></a>允许设备的电源管理

将此选项设置为“是”，以启用客户端上的电源管理。 有关详细信息，请参阅[电源管理简介](../manage/power/introduction-to-power-management.md)。

### <a name="allow-users-to-exclude-their-device-from-power-management"></a>允许用户从电源管理中排除其设备

选择“是”允许软件中心的用户从任何配置的电源管理设置中排除其计算机。  

### <a name="allow-network-wake-up"></a>允许网络唤醒

如果启用此设置，客户端会将计算机上的电源设置配置为允许网络适配器唤醒设备。 如果禁用此设置，则计算机的网络适配器无法唤醒设备。

### <a name="enable-wake-up-proxy"></a>启用唤醒代理

指定“是”以在为单播包配置站点 LAN 唤醒设置后对其进行补充。  

有关唤醒代理的详细信息，请参阅[规划如何唤醒客户端](plan/plan-wake-up-clients.md)。  

> [!WARNING]  
> 在未首先了解唤醒代理的工作原理以及在测试环境中对其进行评估之前，请不要在生产网络中启用唤醒代理。  

然后根据需要配置以下附加设置：

- **唤醒代理端口号 (UDP)** ：客户端用于向处于睡眠状态的计算机发送唤醒数据包的端口号。 保留默认端口 25536，或将数字更改为所选的值。  

- **LAN 唤醒端口号 (UDP)** ：保留默认值 9，除非在站点“属性”的“端口”选项卡上更改了 LAN 唤醒 (UDP) 端口号 。  

    > [!IMPORTANT]  
    > 此数字必须与站点“属性”中的数字匹配。 如果在一个位置更改此数字，则不会在其他位置自动更新此数字。  

- **针对唤醒代理的 Windows Defender 防火墙例外**：Configuration Manager 客户端自动配置运行 Windows Defender 防火墙的设备上的唤醒代理端口号。 选择“配置”指定防火墙配置文件。  

    如果客户端运行其他防火墙，请手动将其配置为允许“唤醒代理端口号 (UDP)”。  

- **DirectAccess 或其他介入的网络设备的 IPv6 前缀(如果需要)。请使用逗号指定多个项**：输入唤醒代理在网络上运行所需的 IPv6 前缀。



## <a name="remote-tools"></a>远程工具  

### <a name="enable-remote-control-on-clients-and-firewall-exception-profiles"></a>在客户端上启用远程控制及防火墙例外配置文件

选择“配置”，启用 Configuration Manager 远程控制功能。 根据需要将防火墙设置配置为允许远程控制在客户端计算机上工作。  

默认情况下，禁用了远程控制。  

> [!IMPORTANT]  
> 如果未配置防火墙设置，则远程控制可能无法正常工作。  

### <a name="users-can-change-policy-or-notification-settings-in-software-center"></a>用户可以在软件中心内更改策略或通知设置

选择用户是否可以从软件中心中更改远程控制选项。  

### <a name="allow-remote-control-of-an-unattended-computer"></a>允许远程控制无人参与的计算机

选择管理员是否可以使用远程控制来访问注销或锁定的客户端计算机。 禁用此设置后，只能远程控制登录和解锁的计算机。  

### <a name="prompt-user-for-remote-control-permission"></a>提示用户提供远程控制权限

选择客户端计算机是否要显示一条消息，以在允许远程控制会话之前请求提供用户的权限。  

### <a name="prompt-user-for-permission-to-transfer-content-from-shared-clipboard"></a>提示用户获取从共享剪贴板传输内容的权限

在远程控制会话中从共享剪贴板传输内容前，允许用户选择接受或拒绝文件传输。 用户只需要在每个会话中授予一次权限。 查看者无法授予自身传输文件的权限。

### <a name="grant-remote-control-permission-to-local-administrators-group"></a>将远程控制权限授予本地管理员组

选择服务器上启动远程控制连接的本地管理员是否可以与客户端计算机建立远程控制会话。  

### <a name="access-level-allowed"></a>允许的访问级别

指定将要允许的远程控制访问级别。 从以下设置中选择：  

- **无访问权限**
- **仅查看**
- **完全控制**  

### <a name="permitted-viewers-of-remote-control-and-remote-assistance"></a>允许查看远程控制和远程协助的用户

选择“设置查看者”，指定可以与客户端计算机建立远程控制会话的 Windows 用户的名称。  

### <a name="show-session-notification-icon-on-taskbar"></a>在任务栏上显示会话通知图标

将此设置配置为“是”，以在客户端的 Windows 任务栏上显示一个图标，指示远程控制会话处于活动状态。  

### <a name="show-session-connection-bar"></a>显示会话连接栏

将此选项设置为“是”，以在客户端上显示高可见性会话连接栏，指示远程控制会话处于活动状态。  

### <a name="play-a-sound-on-client"></a>在客户端上播放声音

设置此选项，以当远程控制会话在客户端计算机上处于活动状态时用声音指示。 选择下列选项之一：

- **无声音**
- **会话的开始和结束**（默认）
- **在会话过程中重复**  

### <a name="manage-unsolicited-remote-assistance-settings"></a>管理未经请求的远程协助设置

通过将此设置配置为“是”，Configuration Manager 可以管理未经请求的远程协助会话。  

在未经请求的远程协助会话中，客户端计算机上的用户没有通过请求协助来启动会话。  

### <a name="manage-solicited-remote-assistance-settings"></a>管理经请求的远程协助设置

将此选项设置为“是”，允许 Configuration Manager 管理经请求的远程协助会话。  

在经请求的远程协助会话中，客户端计算机上的用户向管理员发送远程协助请求。  

### <a name="level-of-access-for-remote-assistance"></a>远程协助访问级别

选择访问级别，分配给在 Configuration Manager 控制台中启动的远程协助会话。 选择下列选项之一：

- **无**（默认）
- **远程查看**
- **完全控制**

> [!NOTE]  
> 客户端计算机用户必须始终允许发生远程帮助会话。  

### <a name="manage-remote-desktop-settings"></a>管理远程桌面设置

将此选项设置为“是”，允许 Configuration Manager 管理计算机的远程桌面会话。  

### <a name="allow-permitted-viewers-to-connect-by-using-remote-desktop-connection"></a>允许获得许可的查看者使用远程桌面连接进行连接

将此选项设置为“是”，将允许查看者列表中指定的用户添加到客户端上的远程桌面本地用户组。  

### <a name="require-network-level-authentication-on-computers-that-run-windows-vista-operating-system-and-later-versions"></a>在运行 Windows Vista 和更高版本的操作系统的计算机上要求网络级别身份验证

将此选项设置为“是”，可使用网络级别身份验证 (NLA) 与客户端计算机建立远程桌面连接。 NLA 最初需要较少的远程计算机资源，因为它会在建立远程桌面连接之前完成用户身份验证。 使用 NLA 是一种更安全的配置。 因为 NLA 有助于保护计算机不受恶意用户或软件的攻击，并且可减小拒绝服务攻击带来的风险。  



## <a name="software-center"></a>软件中心

### <a name="select-the-user-portal"></a>选择用户门户

<!--CMADO-3601237,INADO-4297660-->
从版本 2006 开始，如果将公司门户部署到共同管理的设备，请将此设置配置为“公司门户”。 此设置可确保用户仅接收来自公司门户的通知。

如果将公司门户安装在共同管理的设备上，但将此设置配置为“软件中心”，用户将看到来自这两个门户的通知。 这种体验可能会让用户感到困惑。

如果更改公司门户的客户端设置，那么，当用户选择 Configuration Manager 通知时，它将启动公司门户。 如果通知的场景是公司门户不支持的，则选择通知会启动软件中心。

公司门户的行为取决于你的共同管理工作负载配置。 有关详细信息，请参阅[在共同受管理设备上使用公司门户应用](../../../comanage/company-portal.md)。

### <a name="select-these-new-settings-to-specify-company-information"></a>选择这些新设置来指定公司信息

将此选项设置为“是”，然后指定以下设置来打造组织的软件中心：

- **公司名称**：输入用户在软件中心看到的组织名称。  

- **软件中心的配色方案**：单击“选择颜色”，定义软件中心使用的主色调。  

- **选择在软件中心使用的徽标**：单击“浏览”，选择要在软件中心显示的图像。 徽标必须为 400 x 100 像素的 JPEG、PNG 或 BMP 格式，最大尺寸为 750 KB。 徽标文件名称不能包含空格。  

### <a name="hide-unapproved-applications-in-software-center"></a><a name="bkmk_HideUnapproved"></a>在软件中心隐藏未批准的应用程序

启用此选项后，软件中心会隐藏需要审批的用户可用的应用程序。<!--1355146-->

### <a name="hide-installed-applications-in-software-center"></a><a name="bkmk_HideInstalled"></a>在软件中心隐藏安装的应用程序

启用此选项后，已安装的应用程序将不再显示在“应用程序”选项卡中。安装或升级到 Configuration Manager 时，此选项会设置为默认选项。 仍可以在安装状态选项卡下查看已安装的应用程序。 <!--1357592-->

### <a name="hide-application-catalog-link-in-software-center"></a><a name="bkmk_HideAppCat"></a>隐藏软件中心中的应用程序目录链接

指定应用程序目录网站链接在软件中心的可见性。 设置此选项后，用户将不会在软件中心的安装状态节点中看到应用程序目录网站链接。 <!--1358214-->

> [!Important]  
> 从 Current Branch 版本 1806 开始，不支持应用程序目录的 Silverlight 用户体验。 自版本 1906 起，更新后的客户端自动使用管理点进行用户可用的应用程序部署。 仍然无法安装新的应用程序目录角色。 版本 1910 已终止对应用程序目录角色的支持。  

### <a name="software-center-tab-visibility"></a>软件中心选项卡的可见性

#### <a name="starting-in-version-1906"></a>从版本 1906 开始
<!--4063773-->

选择应在软件中心中显示的选项卡。 使用“添加”按钮可将选项卡移动到“可见”选项卡 。 使用“删除”按钮可将选项卡移动到“隐藏”选项卡列表 。 使用“上移”或“下移”按钮可对选项卡进行排序 。 

可用选项卡：
- **应用程序**
- **更新**
- **操作系统**
- **安装状态**
- **设备符合性**
- **选项**
- 通过单击“添加选项卡”按钮，最多可添加 5 个自定义选项卡。
  - 指定自定义选项卡的“选项卡名称”和“内容 URL”。
  - 选择“删除选项卡”删除自定义选项卡。  

  >[!Important]  
  > - 若要将一些网站功能用作软件中心内的自定义选项卡，它们可能无法正常运行。 将结果部署到客户端之前，请确保测试结果。 <!--519659-->
  > - 添加自定义选项卡时，仅指定受信任的地址或 Intranet 网站地址。<!--SCCMDocs issue 1575-->

#### <a name="version-1902-and-earlier"></a>版本1902 及更早版本

将此组中的其他设置配置为“是”，以在软件中心显示以下选项卡：

- **应用程序**
- **更新**
- **操作系统**
- **安装状态**
- **设备符合性**
- **选项**
- **为软件中心指定自定义选项卡** <!--1358132-->
    - **选项卡名称**
    - **内容 URL**

    >[!Important]  
    > 若要将一些网站功能用作软件中心内的自定义选项卡，它们可能无法正常运行。 将结果部署到客户端之前，请确保测试结果。 <!--519659-->
    >
    > 添加自定义选项卡时，仅指定受信任的地址或 Intranet 网站地址。<!--SCCMDocs issue 1575-->

例如，如果你的组织不使用符合性策略，并且你希望在软件中心隐藏“设备符合性”选项卡，请将“启用‘设备符合性’选项卡”设置为“否” 。

### <a name="configure-default-views-in-software-center"></a><a name="bkmk_swctr_defaults"></a> 在软件中心配置默认视图
<!--3612112-->
（从版本 1902 中引入）

- 将“默认应用程序筛选器”配置为对“所有”应用程序或仅对“必要”  应用程序应用。  

  - 软件中心始终使用默认设置。 用户可以更改此筛选器，但软件中心不会保留其首选项。  

- 将“默认应用程序视图用”设置为“平铺视图”或“列表视图”  。

  - 如果用户更改此配置，则软件中心以后会保留用户的首选项。


## <a name="software-deployment"></a>软件部署  

### <a name="schedule-re-evaluation-for-deployments"></a>计划部署的重新评估

配置 Configuration Manager 为所有部署重新评估要求规则的计划。 默认值为每七天一次。  

> [!IMPORTANT]  
> 与网络或站点服务器相比，此设置对本地客户端更具侵入性。 更加主动的重新评估计划会对网络和客户端计算机的性能产生负面影响。 Microsoft 不建议将该值设置为低于默认值。 如果更改此值，请密切监视性能。  

按以下步骤从客户端启动此操作：从“Configuration Manager”控制面板的“操作”选项卡中，选择“应用程序部署评估周期”。  



## <a name="software-inventory"></a>软件清单  

### <a name="enable-software-inventory-on-clients"></a>在客户端上启用软件清单

默认情况下，此选项设置为“是”。 有关详细信息，请参阅[软件清单简介](../manage/inventory/introduction-to-software-inventory.md)。

### <a name="schedule-software-inventory-and-file-collection"></a>计划软件清单和文件收集

选择“计划”，调整客户端运行软件清单和文件收集周期的频率。 默认情况下，该周期为每七天执行一次。

### <a name="inventory-reporting-detail"></a>清单报告详细信息

指定要列出清单的以下某个文件信息级别：

- **仅文件**
- **仅产品**
- **完整详细信息**（默认）

### <a name="inventory-these-file-types"></a>列出这些文件类型的清单

如果想要指定要列出清单的文件类型，请选择“设置类型”，然后配置以下各项：  

> [!NOTE]  
> 如果对计算机应用了多个自定义客户端设置，则会合并每个设置返回的清单。  

- 选择“新建”，将新文件类型添加到清单。 然后在“清单文件属性”对话框中，指定以下信息：  

    - **名称**：提供要列出清单的文件的名称。 使用星号 (`*`) 通配符表示任意文本字符串，使用问号 (`?`) 表示任何一个字符。 例如，若要列出扩展名为 .doc 的所有文件的清单，请指定文件名 `*.doc`。  

    - **位置**：选择“设置”，打开“路径属性”对话框 。 将软件清单配置为，在所有客户端硬盘中搜索指定文件、搜索指定路径（例如 `C:\Folder`），或搜索指定变量（例如 `%windir%`）。 还可以搜索指定路径下面的所有子文件夹。  

    - **排除加密文件和压缩文件**：如果选择此选项，则不会列出任何压缩或加密文件的清单。  

    - **排除 Windows 文件夹中的文件**：如果选择此选项，则不会列出 Windows 文件夹及其子文件夹中任何文件的清单。  

    选择“确定”以关闭“清单文件属性”对话框。 添加想要列出清单的所有文件，然后选择“确定”关闭“配置客户端设置”对话框。  

### <a name="collect-files"></a>收集文件

如果想从客户端计算机中收集文件，请选择“设置文件”，然后配置以下各项设置：  

> [!NOTE]  
> 如果对计算机应用了多个自定义客户端设置，则会合并每个设置返回的清单。  

- 在“配置客户端设置”对话框中，选择“新建”，添加要收集的文件。  

- 在“收集的文件属性”  对话框中，提供以下信息：  

    - **名称**：为要收集的文件提供名称。 使用星号 (`*`) 通配符表示任意文本字符串，使用问号 (`?`) 表示任何一个字符。  

    - **位置**：选择“设置”，打开“路径属性”对话框 。 将软件清单配置为，在所有客户端硬盘中搜索要收集的文件、搜索指定路径（例如 `C:\Folder`），或搜索指定变量（例如 `%windir%`）。 还可以搜索指定路径下面的所有子文件夹。  

    - **排除加密文件和压缩文件**：如果选择此选项，则不会收集任何压缩或加密文件。  

    - **当文件的总大小超过以下值 (KB) 时停止文件收集**：指定文件大小（以 KB 为单位），然后客户端停止收集指定的文件。  

    > [!NOTE]  
    > 站点服务器收集五个最近更改的收集文件版本，并将它们存储在 `<ConfigMgr installation directory>\Inboxes\Sinv.box\Filecol` 目录中。 如果自上次软件清单周期以来文件未发生更改，则不会再收集该文件。  
    >
    > 软件清单不收集超过 20 MB 的文件。  
    >
    > “配置客户端设置”对话框中的“所有收集的文件的最大大小(KB)”值显示所有收集的文件的最大大小。 达到该大小后，文件的收集将停止。 已收集的任何文件都会被保留并发送到站点服务器。  

    > [!IMPORTANT]
    > 如果将软件清单配置为收集许多大型文件，此配置可能会对网络和站点服务器的性能产生负面影响。  

    有关如何查看收集的文件的信息，请参阅[如何使用资源浏览器查看软件清单](../manage/inventory/use-resource-explorer-to-view-software-inventory.md)。  

    选择“确定”以关闭“收集的文件属性”对话框。 添加想要收集的所有文件，然后选择“确定”以关闭“配置客户端设置”对话框。  

### <a name="set-names"></a>设置名称

软件清单代理从文件标头信息中检索制造商和产品名称。 文件标头信息中并未始终标准化这些名称。 在资源浏览器中查看软件清单时，可能会显示同一制造商或产品名称的不同版本。 要标准化这些显示名称，请选择“设置名称”，然后配置以下各项设置：  

- **名称类型**：软件清单收集关于制造商和产品的信息。 选择要为“制造商”还是“产品”配置显示名称。  

- **显示名称**：指定想要用来替代“清单名称”列表中的名称的显示名称。 要指定新的显示名称，请选择“新建”。  

- **清单名称**：若要添加清单名称，请选择“新建”。 在软件清单中，此名称被“显示名称”列表中选择的名称替换。 可添加多个名称进行替换。  



## <a name="software-metering"></a>软件计数

### <a name="enable-software-metering-on-clients"></a>在客户端上启用软件计数

默认情况下，此设置设为“是”。 有关详细信息，请参阅 [软件计数](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md#configure-software-metering)。

### <a name="schedule-data-collection"></a>计划数据收集

选择“计划”，调整客户端运行软件计数周期的频率。 默认情况下，该周期为每七天执行一次。



## <a name="software-updates"></a>软件更新  

### <a name="enable-software-updates-on-clients"></a>在客户端上启用软件更新

使用此设置在 Configuration Manager 客户端上启用软件更新。 禁用此设置时，Configuration Manager 会从客户端删除现有部署策略。 当重新启用此设置时，客户端会下载当前部署策略。  

> [!IMPORTANT]  
> 禁用此设置时，依赖于软件更新的符合性策略将不再起作用。  

### <a name="software-update-scan-schedule"></a>软件更新扫描计划

选择“计划”，指定客户端启动符合性评估扫描的频率。 此扫描确定客户端上的软件更新的状态（例如必需或者已安装）。 有关符合性评估的详细信息，请参阅[软件更新符合性评估](../../../sum/understand/software-updates-introduction.md#BKMK_SUMCompliance)。  

默认情况下，此扫描使用简单的计划，每七天启动一次。 可以创建自定义计划。 可以指定确切的开始日期和时间，是使用通用协调时间 (UTC) 还是使用本地时间，并为一周中的特定日配置重复间隔。  

> [!NOTE]  
> 如果指定的间隔小于 1 天，Configuration Manager 会自动默认为 1 天。  

> [!WARNING]  
> 客户端计算机上的实际开始时间是开始时间加上随机的一段时间（最多为 2 小时）。 这种随机化可以防止客户端计算机启动扫描和同时连接到活动软件更新点。  

### <a name="schedule-deployment-re-evaluation"></a>计划部署重新评估

选择“计划”可配置软件更新客户端代理重新评估软件更新在 Configuration Manager 客户端计算机上的安装状态的频率。 当客户端上再也无法找到以前安装的软件更新，但仍然需要这些更新时，客户端会重新安装这些软件更新。

根据软件更新符合性的公司策略，以及用户是否可以卸载软件更新调整此计划。 每个部署重新评估周期都会导致网络和客户端计算机处理器活动。 默认情况下，此设置使用简单的计划，每七天启动一次部署重新评估扫描。  

> [!NOTE]  
> 如果指定的间隔小于 1 天，Configuration Manager 会自动默认为 1 天。  

### <a name="when-any-software-update-deployment-deadline-is-reached-install-all-other-software-update-deployments-with-deadline-coming-within-a-specified-period-of-time"></a>在达到任何软件更新部署截止时间时，安装所有截止时间在指定时间段内的其他软件更新部署

将此选项设置为“是”，可安装截止时间在指定时间段内的所需部署中的所有软件更新。 在所需软件更新部署达到截止时间时，客户端会开始安装部署中的软件更新。 此设置确定是否要安装截止时间在指定时间段内的其他所需部署中的软件更新。  

使用此设置可加快所需软件更新的安装速度。 此设置还有可能增加客户端安全性、减少对用户的通知并减少客户端重启次数。 默认情况下，此设置设为“否” 。  

### <a name="period-of-time-for-which-all-pending-deployments-with-deadline-in-this-time-will-also-be-installed"></a>在此时间段内截止的所有挂起的部署在一定时间内也将进行安装。

使用此设置可指定前一个设置的时间段。 可以输入介于 1 到 23 个小时和介于 1 到 365 天的值。 默认情况下，此设置配置为七天。  

### <a name="allow-clients-to-download-delta-content-when-available"></a>在有可用内容时，允许客户端下载增量内容

（从版本 1902 中引入）

通过将此选项设置为“是”，允许客户端使用增量内容文件。 此设置允许设备上的 Windows 更新代理确定所需内容并有选择地下载内容。 

- 在启用此客户端设置之前，请确保为环境正确配置了传递优化。 有关详细信息，请参阅 [Windows 传递优化](../../../sum/deploy-use/optimize-windows-10-update-delivery.md#windows-delivery-optimization)和[传递优化客户端设置](#delivery-optimization)。
 - 此客户端设置会替换“在客户端上启用快速安装文件的安装”。 通过将此选项设置为“是”，客户端可以使用快速安装文件。 有关详细信息，请参阅[管理 Windows 10 更新的快速安装文件](../../../sum/deploy-use/manage-express-installation-files-for-windows-10-updates.md)。
 - 从 Configuration Manager 版本 1910 开始，设置此选项后，增量下载将用于所有 Windows 更新安装文件，而不仅仅是快速安装文件。
    - 将 CMG 用于内容存储时，如果“在有可用内容时下载增量内容”客户端设置已启用，则第三方更新内容不会下载到客户端。 <!--6598587--> 


### <a name="port-that-clients-use-to-receive-requests-for-delta-content"></a>客户端用于接收增量内容请求的端口

（从版本 1902 中引入）

此设置为 HTTP 侦听器配置本地端口，以下载增量内容。 它默认设置为 8005。 无需在客户端防火墙中打开此端口。 

> [!NOTE]
>此客户端设置会替换“用于为快速安装文件下载内容的端口”。


### <a name="enable-management-of-the-office-365-client-agent"></a>启用 Office 365 客户端代理的管理

当你将此选项设置为“是”时，它将启用配置 Microsoft 365 Apps 安装设置。 还可以从 Office 内容分发网络 (CDN) 下载文件，以及将文件部署为 Configuration Manager 中的应用程序。 有关详细信息，请参阅[管理 Microsoft 365 Apps](../../../sum/deploy-use/manage-office-365-proplus-updates.md)。

### <a name="enable-installation-of-software-updates-in-all-deployments-maintenance-window-when-software-update-maintenance-window-is-available"></a><a name="bkmk_SUMMaint"></a>当“软件更新”维护时段可用时，在“所有部署”维护时段中启用软件更新安装

将此选项设置为“是”且客户端定义了至少一个"软件更新"维护时段时，将在"所有部署"维护时段安装软件更新。

默认情况下，此设置设为“否” 。 此值使用与以前相同的行为：如果两种类型都存在，则它将忽略时段。 <!--2839307-->

> [!NOTE]
> 此设置还适用于配置为应用于“任务序列”的维护时段。<!-- SCCMDocs-pr #4596 -->
>
> 如果客户端只有“所有部署”时段可用，它仍会在该时段内安装软件更新或任务序列。

#### <a name="maintenance-window-example"></a>维护时段示例

例如，可以配置以下维护时段：

- **所有部署**：02:00 - 04:00
- **软件更新**：04:00 - 06:00

默认情况下，客户端仅在第二个维护时段期间安装软件更新。 它忽略了此方案中所有部署的维护时段。 将此设置更改为“是”时，客户端将在 02:00 到 06:00 之间安装软件更新。


### <a name="specify-thread-priority-for-feature-updates"></a><a name="bkmk_thread-priority"></a>为功能更新指定线程优先级

<!--3734525-->
从 Configuration Manager 版本 1902 开始，可以调整 Windows 10 版本 1709 或更高版本客户端通过 [Windows 10 维护服务](../../../osd/deploy-use/manage-windows-as-a-service.md)安装功能更新的优先级。 此设置对 Windows 10 就地升级任务序列没有影响。

此客户端设置提供以下选项：

- **未配置**：Configuration Manager 不更改设置。 管理员可以预暂存自己的 setupconfig.ini 文件。 该值为默认值。

- **常规**：Windows 安装程序使用更多系统资源，更新更快。 它使用更多的处理器时间，因此总安装时间更短，但用户的服务中断时间更长。  

    - 使用 `/Priority Normal` [Windows 安装程序命令行选项](/windows-hardware/manufacture/desktop/windows-setup-command-line-options)在设备上配置 setupconfig.ini 文件。

- **低**：可继续使用设备，而它在后台进行下载和更新。 总安装时间更长，但用户的服务中断时间更短。 可能需要增加更新最大运行时间以避免在使用此选项时超时。  

    - 从 setupconfig.ini 文件中删除 `/Priority` [Windows 安装程序命令行选项](/windows-hardware/manufacture/desktop/windows-setup-command-line-options)。


### <a name="enable-third-party-software-updates"></a>启用第三方软件更新

如果你将此选项设置为“是”，它会设置“允许 Intranet Microsoft 更新服务位置的签名更新”策略，并将签名证书安装到客户端上受信任的发布者库。

### <a name="enable-dynamic-update-for-feature-updates"></a><a name="bkmk_du"></a>启用功能更新的动态更新
<!--4062619-->
从 Configuration Manager 版本 1906 开始，可以配置 [Windows 10 动态更新](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847)。 动态更新通过指示客户端从 Internet 下载这些更新，在 Windows 安装过程中安装语言包、按需功能、驱动程序和累积更新。 如果将此设置设置为“是”或“否”，Configuration Manager 将修改功能更新安装期间使用的 [setupconfig](/windows-hardware/manufacture/desktop/windows-setup-command-line-options) 文件 。

- **未配置** - 默认值。 未更改 setupconfig 文件。
  - 默认情况下，在所有受支持的 Windows 10 版本上启用动态更新。
    - 对于 Windows 10 版本 1803 及更早版本，动态更新会检查设备的 WSUS 服务器是否有批准的动态更新。 在 Configuration Manager 环境中，绝不会在 WSUS 服务器中直接批准动态更新，因此这些设备不会安装这些更新。
    - 从 Windows 10 版本 1809 开始，动态更新使用设备的 Internet 连接从 Microsoft 更新获取动态更新。 不会发布这些动态更新以供 WSUS 使用。
- **是** - 启用动态更新。
- **否** - 禁用动态更新。


## <a name="state-messaging"></a>状态消息

### <a name="state-message-reporting-cycle-minutes"></a>状况消息报告周期（分钟）

指定客户端报告状况消息的频率。 此设置默认为 15 分钟。



## <a name="user-and-device-affinity"></a>用户和设备相关性  

### <a name="user-device-affinity-usage-threshold-minutes"></a>用户设备相关性使用情况阈值(分钟)

指定在 Configuration Manager 创建用户设备相关性映射之前的分钟数。 默认情况下，此值为 2880 分钟（两天）。

### <a name="user-device-affinity-usage-threshold-days"></a>用户设备相关性使用情况阈值(天)

指定客户端测量基于使用情况的设备相关性阈值的天数。 默认情况下，此值为 30 天。

> [!NOTE]  
> 例如，将“用户设备相关性使用情况阈值(分钟)”指定为 60 分钟，将“用户设备相关性使用情况阈值(天)”指定为 5 天。 然后用户在 5 天内使用该设备必须达到 60 分钟，以创建该设备的自动相关性。  

### <a name="automatically-configure-user-device-affinity-from-usage-data"></a>利用使用情况数据自动配置用户设备相关性

选择“是”可基于 Configuration Manager 收集的使用情况信息自动创建用户设备相关性。  

### <a name="allow-user-to-define-their-primary-devices"></a>允许用户定义其主要设备
<!--3485366-->
当此设置为“是”时，用户可在软件中心内标识自己的主要设备。 有关详细信息，请参阅[软件中心用户指南](../../understand/software-center.md#work-information)。

## <a name="windows-diagnostic-data"></a>Windows 诊断数据

> [!IMPORTANT]
> 此组旧称为“Windows Analytics”。 Microsoft 已于 2020 年 1 月 31 日停用了 Windows Analytics 服务。 有关详细信息，请参阅 [KB 4521815：Windows Analytics 将于 2020 年 1 月 31 日停用](https://support.microsoft.com/help/4521815/windows-analytics-retirement)。
>
> Windows Analytics 演变为桌面分析。 使用桌面分析来管理 Windows 诊断数据设置。 有关详细信息，请参阅[什么是桌面分析](../../../desktop-analytics/overview.md)。