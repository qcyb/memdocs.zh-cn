---
title: Microsoft 互连缓存
titleSuffix: Configuration Manager
description: 将 Configuration Manager 分发点用作传递优化的本地缓存服务器
ms.date: 05/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c5cb5753-5728-4f81-b830-a6fd1a3e105c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 70d4930da712eccff8bdb1f1986a68aa5fe77644
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455270"
---
# <a name="microsoft-connected-cache-in-configuration-manager"></a>Configuration Manager 中的 Microsoft Connected Cache

适用范围：Configuration Manager (Current Branch)

<!--3555764-->

从版本 1906 开始，你可以在分发点上安装 Microsoft Connected Cache 服务器。 通过将此内容缓存在本地，你的客户端可以从传递优化功能中受益，但你可帮助保护 WAN 链接。

> [!NOTE]
> 从版本 1910 开始，此功能现在称为“Microsoft Connected Cache”。 它旧称为“传递优化网络内缓存”。

此缓存服务器充当由传递优化下载的内容的按需透明缓存。 使用客户端设置以确保此服务器仅提供给本地 Configuration Manager 边界组的成员。

此缓存独立于 Configuration Manager 分发点内容。 如果选择和分发点角色一样的驱动，它将单独存储内容。

> [!Note]  
> Connected Cache 服务器是安装在 Windows Server 上的应用程序。 此应用程序仍在开发中。

## <a name="how-it-works"></a>工作原理

当你配置客户端以使用 Connected Cache 服务器时，它们不再从 Internet 请求 Microsoft 云托管内容。 客户端从安装在分发点上的缓存服务器请求此内容。 本地服务器使用 IIS 功能的应用程序请求路由 (ARR) 缓存此内容。 然后，缓存服务器可快速响应对同一内容的任何未来请求。 如果 Connected Cache 服务器不可用，或者尚未缓存内容，客户端将从 Internet 下载内容。 客户端还使用传递优化，因此从其网络中的对等端下载部分内容。

![Connected Cache 的工作原理示意图](media/3555764-microsoft-connected-cache.png)

1. 客户端检查更新并获取内容分发网络 (CDN) 的地址。

2. Configuration Manager 在客户端上配置传递优化 (DO) 设置，其中包括缓存服务器名称。

3. 客户端 A 从 DO 缓存服务器请求内容。

4. 如果缓存不包含该内容，则 DO 缓存服务器从 CDN 获取该内容。

5. 如果缓存服务器无法响应，客户端将从 CDN 下载该内容。

6. 客户端使用 DO 从对等方获取内容的片段。

## <a name="prerequisites-and-limitations"></a>先决条件和限制

- 具有以下配置的本地分发点：

  - 运行 Windows Server 2012、Windows Server 2012 R2、Windows Server 2016 或 Windows Server 2019

  - 在端口 80 上启用默认网站

  - 请勿预安装 IIS [应用程序请求路由](https://docs.microsoft.com/iis/extensions/planning-for-arr/application-request-routing-version-2-overview) (ARR) 功能。 Connected Cache 安装 ARR 并配置其设置。 Microsoft 不能保证 Connected Cache 的 ARR 配置不会与服务器上同时使用此功能的其他应用程序发生冲突。

  - 分发点需要具有 Internet 连接才能访问 Microsoft 云。 特定 URL 可以基于特定于云的内容而不同。 确保还允许终结点进行传递优化。 有关详细信息，请参阅 [Internet 访问要求](../network/internet-endpoints.md)。

  - 从版本 2002 开始，联网缓存应用程序可以使用未经身份验证的代理服务器进行 Internet 访问。 有关详细信息，请参阅[配置站点系统服务器的代理](../network/proxy-server-support.md#configure-the-proxy-for-a-site-system-server)。<!-- 5856396 -->

- 运行 Windows 10 版本 1709 或更高版本的客户端

## <a name="enable-connected-cache"></a>启用 Connected Cache

1. 在 Configuration Manager 控制台中，转到“管理”工作区，并选择“分发点”节点 。

1. 选择“本地”分发点，然后在功能区中选择“属性”。

1. 在分发点角色的属性中的“常规”选项卡中，配置以下设置：  

    1. 启用选项“使此分发点用作 Microsoft Connected Cache 服务器”  

        查看并接受许可条款。

    2. **要使用的本地驱动器**：选择要用于缓存的磁盘。 “自动”是默认值，使用可用空间最多的磁盘。<sup>[备注 1](#bkmk_note1)</sup>  

        > [!Note]  
        > 可以在以后更改此驱动器。 除非将缓存内容复制到新驱动器，否则会丢失任何缓存内容。

    3. **磁盘空间**：选择要保留的磁盘空间 (GB)，或占磁盘总空间的百分比。 默认情况下，此值为 100 GB。

        > [!Note]  
        > 默认缓存大小对于大多数客户来说应该已足够。 可以在以后调整缓存大小。
        >
        > 如果磁盘上的缓存大小超出分配的空间，则 ARR 基于其内置的启发式选项通过删除内容来清除空间。<!-- SCCMDocs#2045 -->

    4. **禁用 Connected Cache 服务器时保留缓存**：如果删除缓存服务器并启用此选项，服务器会将缓存内容存储在磁盘上。  

1. 在“传递优化”组的客户端设置中，配置“使 Configuration Manage 管理的设备能够对下载的内容使用 Microsoft Connected Cache 服务器”设置 。  

### <a name="note-1-about-drive-selection"></a><a name="bkmk_note1"></a> 注释 1：关于驱动器选择

如果选择“自动”，则 Configuration Manager 安装 Connected Cache 组件时，将优先采用 no_sms_on_drive.sms 文件 。 例如，分发点具有 `C:\no_sms_on_drive.sms` 文件。 即使 C: 驱动器具有的可用空间最多，Configuration Manager 也会将 Connected Cache 配置为使用另一个驱动器进行缓存。

如果选择已具有 no_sms_on_drive.sms 文件的特定驱动器，则 Configuration Manager 将忽略该文件。 将 Connected Cache 配置为使用该驱动器是一个明确的意图。 例如，分发点具有 `F:\no_sms_on_drive.sms` 文件。 将分发点属性显式配置为使用“F:”驱动器时，Configuration Manager 会将 Connected Cache 配置为使用 F: 驱动器进行缓存。

若要在安装 Connected Cache 后更改驱动器，请执行以下操作：

- 手动将分发点属性配置为使用特定的驱动器号。

- 如果设置为自动，请首先创建 no_sms_on_drive.sms 文件。 然后对分发点属性进行一些更改，以触发配置更改。

### <a name="automation"></a>自动化

<!-- SCCMDocs#1911 -->

可以使用 Configuration Manager SDK 自动配置分发点上的 Microsoft 联网缓存设置。 与所有站点角色一样，请使用 [SMS_SCI_SysResUse WMI 类](../../../develop/reference/core/servers/configure/sms_sci_sysresuse-server-wmi-class.md)。 有关详细信息，请参阅[站点角色编程](../../../develop/osd/about-operating-system-deployment-site-role-configuration.md#programming-the-site-roles)。

更新分发点的 SMS_SCI_SysResUse 实例时，请设置以下属性：

- AgreeDOINCLicense：设置为 `1` 以接受许可条款。
- Flags：启用 `|= 4`，禁用 `&= ~4`
- DiskSpaceDOINC：设置为 `Percentage` 或 `GB`
- RetainDOINCCache：设置为 `0` 或 `1`
- LocalDriveDOINC：设置为 `Automatic` 或特定驱动器号，如 `C:` 或 `D:`

## <a name="verify"></a>验证

客户端下载云托管的内容时，它们使用安装在分发点上的缓存服务器中的传递优化。 云托管的内容包括以下类型：

- Microsoft Store 应用
- 按需 Windows 功能，例如语言
- 如果启用[适用于企业的 Windows 更新策略](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)：Windows 10 功能和质量更新
- 对于[共同管理工作负载](../../../comanage/workloads.md)：
  - 适用于企业的 Windows 更新：Windows 10 功能和质量更新
  - Office 即点即用应用：Office 应用和更新
  - 客户端应用：Microsoft Store 应用和更新
  - Endpoint Protection：Windows Defender 定义更新

在 Windows 10 版本 1809 或更高版本中，使用 Get-DeliveryOptimizationStatus Windows PowerShell cmdlet 验证此操作。 在 cmdlet 输出中，查看 BytesFromCacheServer 值。 有关详细信息，请参阅[监视传递优化](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-setup#monitor-delivery-optimization)。

如果缓存服务器返回任何 HTTP 故障，则传递优化客户端退回到原始云源。

有关更多详细信息，请参阅 [Configuration Manager 中的 Microsoft Connected Cache 疑难解答](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md)。

## <a name="support-for-intune-win32-apps"></a><a name="bkmk_intune"></a> 对 Intune Win32 应用的支持

<!--5032900-->

自版本 1910 开始，在 Configuration Manager 分发点上启用 Connected Cache 后，可以为共同管理的客户端提供 Microsoft Intune Win32 应用。

### <a name="prerequisites"></a>必备条件

#### <a name="client"></a>客户端

- 将客户端更新到最新版本。

- 客户端设备需要至少具有 4 GB 的内存。

    > [!TIP]
    > 使用以下组策略设置：计算机配置 > 管理模板 > Windows 组件 > 传递优化 > 启用对等缓存时所需的最小 RAM 容量（包含）（以 GB 为单位）。

#### <a name="site"></a>站点

- 在分发点上启用互联缓存。 有关详细信息，请参阅 [Microsoft Connected Cache](microsoft-connected-cache.md)。

- 客户端和支持互联缓存的分发点必须位于同一个边界组中。

- 在[传递优化](../../clients/deploy/about-client-settings.md#delivery-optimization)组中启用以下客户端设置：

  - **将 Configuration Manager 边界组用于传递优化组 ID**
  - **使 Configuration Manager 托管的设备可使用 Microsoft 互联缓存服务器来下载内容**

- 启用预发行功能“适用于共同管理设备的客户端应用”。 有关详细信息，请参阅[预发行功能](../../servers/manage/pre-release-features.md)。

- 启用共同管理，并将“客户端应用”工作负载切换到“试点 Intune”或“Intune”。 有关详细信息，请参阅下列文章：

  - [工作负载 - 客户端应用](../../../comanage/workloads.md#client-apps)
  - [如何启用共同管理](../../../comanage/how-to-enable.md)
  - [将工作负载切换到 Intune](../../../comanage/how-to-switch-workloads.md)

    如果在试点中，请将客户端添加到客户端应用的试点集合。

#### <a name="intune"></a>Intune

- 此功能仅支持 Intune Win32 应用类型。

  - 在 Intune 中创建和分配（部署）新应用来实现此目的。 （在 Intune 版本 1811 之前创建的应用无效。）有关详细信息，请参阅 [Intune Win32 应用管理](https://docs.microsoft.com/intune/apps/apps-win32-app-management)。

  - 此应用至少需要 100 MB。
  
    > [!TIP]
    > 使用以下组策略设置：计算机配置 > 管理模板 > Windows 组件 > 传递优化 > 对等缓存的最小内容文件大小（以 MB 为单位）。

## <a name="see-also"></a>另请参阅

[通过传递优化来优化 Windows 10 更新](../../../sum/deploy-use/optimize-windows-10-update-delivery.md)

[Configuration Manager 中的 Microsoft Connected Cache 疑难解答](../../servers/deploy/configure/troubleshoot-microsoft-connected-cache.md)
