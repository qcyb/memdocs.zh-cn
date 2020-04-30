---
title: Microsoft Store 应用
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 来管理和部署适用于企业和教育的 Microsoft Store 中的应用。
ms.date: 12/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b8ba727aff682e3efbba6a91941a5499f9f00e8b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689315"
---
# <a name="manage-apps-from-the-microsoft-store-for-business-and-education-with-configuration-manager"></a>使用 Configuration Manager 来管理适用于企业和教育的 Microsoft Store 中的应用

在[适用于企业和教育的 Microsoft Store](https://docs.microsoft.com/microsoft-store/) 中可以为组织查找和获取 Windows 应用。 将适用于企业的 Microsoft Store 连接到 Configuration Manager 时，会同步已获取的应用列表。 在 Configuration Manager 控制台中查看这些应用，并按照部署任何其他应用的方式进行部署。

## <a name="online-and-offline-apps"></a><a name="bkmk_apps"></a>联机和脱机应用

适用于企业和教育的 Microsoft Store 支持两种类型的应用：

- **联机**：此许可类型要求用户和设备连接到 Microsoft Store，以获取应用及其许可。 Windows 10 设备必须已加入 Azure Active Directory (Azure AD) 或已加入混合 Azure AD。  

- **脱机**：使用此类型的应用能够缓存应用和许可证，以便直接在本地网络中部署。 设备无需连接到适用于企业的 Microsoft Store 或 Internet。

有关详细信息，请参阅[适用于企业和教育的 Microsoft Store 概述](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview)。

### <a name="summary-of-capabilities"></a>功能摘要

Configuration Manager 支持在具有 Configuration Manager 客户端的 Windows 10 设备上管理适用于企业和教育的 Microsoft Store 应用，也支持使用 Microsoft Intune 注册的 Windows 10 设备。 Configuration Manager 对联机和脱机应用提供以下功能：

|功能|脱机应用|联机应用|
|------------|------------|------------|
|将应用数据同步到 Configuration Manager<br>（每 24 小时同步一次）|是|是|
|从应用商店应用创建 Configuration Manager 应用程序|是|是|
|对应用商店中免费应用的支持|是|是|
|对应用商店中收费应用的支持|否|是<sup>[注释 1](#bkmk_note1)</sup>|
|支持针对用户或设备集合必需的部署|是|是|
|支持对用户或设备集合可用的部署|是|是|
|来自应用商店的业务线应用的支持|是|是|
|为设备上的所有用户配置应用商店应用<sup>[备注 2](#bkmk_note2)</sup><!--1358310-->|是|是|

#### <a name="note-1-online-licensed-apps-version-requirement"></a><a name="bkmk_note1"></a> 注释 1：线上授权应用版本要求

要使用 Configuration Manager 客户端将在线许可的应用部署到 Windows 10 设备，这些应用必须在 Windows 10 版本 1703 或更高版本上运行。  

#### <a name="note-2-configuration-manager-minimum-version"></a><a name="bkmk_note2"></a> 注释 2：Configuration Manager 最低版本

从版本 1806 开始。 有关详细信息，请参阅[创建 Windows 应用程序](../get-started/creating-windows-applications.md#bkmk_provision)。  

### <a name="deploying-online-apps-using-the-microsoft-store-for-business-and-education-to-devices-that-run-the-configuration-manager-client"></a>使用适用于企业和教育的 Microsoft Store 将联机应用部署到运行 Configuration Manager 客户端的设备上

在将适用于企业和教育的 Microsoft Store 应用部署到运行完整的 Configuration Manager 客户端的设备前，请考虑以下几点：

- 要获取完整的功能，设备必须运行 Windows 10 版本 1703 或更高版本。  

- 将设备注册到或使其加入将适用于企业和教育的 Microsoft Store 注册为管理工具的同一 Azure AD 租户中。  

- 本地管理员帐户登录设备时，无法访问适用于企业和教育的 Microsoft Store 应用。  

- 设备必须具有适用于企业和教育的 Microsoft Store 的实时 Internet 连接。 有关包括代理配置在内的详细信息，请参阅[先决条件](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business)。  

### <a name="notes-for-devices-running-earlier-versions-of-windows-10"></a>运行 Windows 10 较早版本的设备的说明

对于具有 Configuration Manager 客户端且运行 Windows 10 版本 1607 或更早版本的设备，以下功能适用：  

通过以下某种方法，在设备上强制安装应用时：  

- 用户安装应用  

- 部署达到其安装截止日期

- 对所需的部署进行安装后重新评估  

会发生以下行为：  

- Configuration Manager 客户端通过启动 Microsoft Store 应用“强制执行”该应用  

- 用户必须从应用商店完成安装  

- 在 Configuration Manager 控制台中，应用部署状态报告失败，并显示以下错误：“在客户端电脑上打开了 Microsoft Store 应用，正在等待用户完成安装。”  

在下一步的应用程序评估周期中：  

- 如果用户从应用商店安装了应用程序，则应用程序会报告状态“成功”   

- 如果用户未尝试从应用商店安装应用：  

  - 对于所需部署，Configuration Manager 客户端会尝试再次启动应用商店  

  - Configuration Manager 不重复强制执行可用部署

#### <a name="devices-running-earlier-versions-of-windows-10"></a>运行 Windows 10 较早版本的设备

- 不能部署来自适用于企业和教育的 Microsoft Store 的业务线应用

- 部署来自应用商店的付费应用时，用户必须登录应用商店并自行获取应用  

- 如果部署组策略来禁用对 Microsoft Store 的使用者版本的访问权限，则适用于企业和教育的 Microsoft Store 中的部署将不起作用。 即使启用了适用于企业和教育的 Microsoft Store，也会发生此行为。  

## <a name="set-up-synchronization"></a><a name="bkmk_setup"></a> 设置同步

通过同步你的组织获得的适用于企业和教育的 Microsoft Store 应用列表，可在 Configuration Manager 控制台中查看这些应用。

将 Configuration Manager 站点连接到 Azure AD 和适用于企业和教育的 Microsoft Store。 有关此流程的详细信息，请参阅[配置 Azure 服务](../../core/servers/deploy/configure/azure-services-wizard.md)。 创建适用于企业的 Microsoft Store 服务的连接  。

确保服务连接点和目标设备可以访问云服务。 有关详细信息，请参阅[适用于企业和教育的 Microsoft Store 的先决条件 - 代理配置](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration)。

### <a name="supplemental-information-and-configuration"></a><a name="bkmk_config"></a>补充信息和配置

在 Azure 服务向导的“应用”页面上，首先配置“Azure环境”和“Web 应用”    。 然后阅读页面底部的“详细信息”部分  。 此信息包括在适用于企业和教育的 Microsoft Store 门户中的以下附加操作：  

- 将 Configuration Manager 配置为存储管理工具。 有关详细信息，请参阅[配置管理提供程序](https://docs.microsoft.com/microsoft-store/configure-mdm-provider-microsoft-store-for-business)。  

- 启用对脱机许可应用的支持。 有关详细信息，请参阅[分发脱机应用](https://docs.microsoft.com/microsoft-store/distribute-offline-apps)。  

- 至少获取一个应用。 有关详细信息，请参阅[查找并获取应用](https://docs.microsoft.com/microsoft-store/find-and-acquire-apps-overview)。  

在 Azure 服务向导的“配置”页面上，指定以下信息  ：  

- **适用于企业的 Microsoft Store 应用内容存储的路径**：指定共享网络路径，包括文件夹。 例如，`\\server\share\folder`。 当站点服务器与应用商店同步时，它在此位置缓存内容。 在 Configuration Manager 中创建应用程序时，站点服务器会将应用内容从本地缓存复制到站点的内容库中。  

- **所选语言**：从 Microsoft Store 中选择要同步的语言，并在软件中心中向用户显示。 例如，如果用户将 Windows 配置为德语，那么软件中心会在应用商店中显示德语字符串。 此行为要求语言同步并且针对特定应用程序存在。

- **默认语言**：如果用户的语言不可用，请选择要使用的默认语言。  

## <a name="create-and-deploy-the-app"></a><a name="bkmk_deploy"></a> 创建并部署应用

同步后，创建并部署适用于企业和教育的 Microsoft Store 应用，过程与任何其他 Configuration Manager 应用程序相似。

1. 在 Configuration Manager 控制台的“软件库”工作区中，展开“应用程序管理”，然后单击“应用商店应用的许可证信息”节点    。  

2. 选择要部署的应用，然后选择功能区中的“创建应用程序”  。  

该站点将创建包含适用于企业和教育的 Microsoft Store 应用的 Configuration Manager 应用程序。

然后，可以像对任何其他 Configuration Manager 应用程序一样部署并监视此应用程序。 有关详细信息，请参阅下列文章：  

- [部署应用程序](deploy-applications.md)
- [从控制台监视应用程序](monitor-applications-from-the-console.md)

## <a name="next-steps"></a>后续步骤

在“软件库”工作区中，展开“应用程序管理”，然后选择“应用商店应用的许可证信息”节点    。

对于你管理的每个应用商店，请查看有关该应用的以下信息：

- 应用名称
- 应用平台
- 你拥有的应用的许可证数量
- 可用许可证的数量

部署联机应用后，该应用的任何更新都直接来自 Microsoft Store。 此外，Configuration Manager 不会检查联机应用的版本合规性，只是 Windows 会报告应用为已安装。  

使用 Configuration Manager 客户端将脱机应用部署到 Windows 10 设备时，用户不能更新 Configuration Manager 部署外部的应用程序。 控制脱机应用的更新在多用户环境（如教室）中尤为重要。 用户可以选择使用[组策略](https://docs.microsoft.com/windows/configuration/stop-employees-from-using-microsoft-store#block-microsoft-store-using-group-policy)来禁用 Microsoft Store。

适用于企业和教育的 Microsoft Store 管理员获取脱机应用后，请勿通过应用商店将应用发布给用户。 此配置可确保用户无法联机安装或联机更新。 用户仅通过 Configuration Manager 接收脱机应用更新。

## <a name="see-also"></a>另请参阅

[排查适用于企业和教育的 Microsoft Store 与 Configuration Manager 的集成问题](troubleshoot-microsoft-store-for-business-integration.md)
