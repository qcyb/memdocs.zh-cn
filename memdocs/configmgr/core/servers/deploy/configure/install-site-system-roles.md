---
title: 安装站点系统角色
titleSuffix: Configuration Manager
description: 将站点系统角色添加到站点中的现有站点系统服务器或新站点系统服务器。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 61f5c774-7667-44ae-b8e4-a4951318b183
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 30b57de75e637aa083070832783647b8ad35b4a7
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700525"
---
# <a name="install-site-system-roles-for-configuration-manager"></a>为 Configuration Manager 安装站点系统角色

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 控制台提供两种方法用于安装站点系统角色：

- **添加站点系统角色**：将站点系统角色添加到站点中的现有站点系统服务器。

- **创建站点系统服务器**：将新服务器指定为站点系统服务器，然后安装一个或多个角色。 除第一页外，此方法与**添加站点系统角色**相同。 首先，指定服务器的名称以及要在其中安装服务器的站点。

> [!TIP]
> 在远程计算机上安装角色时，Configuration Manager 会将远程计算机的计算机帐户添加到站点服务器上的本地组。
>
> 在域控制器上安装站点时，站点服务器上的组是域组而不是本地组。 在这种情况下，远程站点系统角色不会立即生效。 需要重启站点系统服务器，或刷新远程服务器计算机帐户的 Kerberos 票证。 有关详细信息，请参阅[使用的帐户](../../../plan-design/hierarchy/accounts.md)。

在安装站点系统角色前，Configuration Manager 会检查目标计算机，以确保其满足所选角色的先决条件。

默认情况下，当 Configuration Manager 安装站点系统角色时，它会将文件安装在具有最多可用磁盘空间的第一个 NTFS 格式的可用磁盘驱动器上。 若要防止 Configuration Manager 在特定驱动器上安装，请在安装站点系统服务器前，在驱动器的根目录中创建名为 **no_sms_on_drive.sms** 的空文件。

Configuration Manager 使用**站点系统安装帐户**来安装角色。 在安装角色时指定此帐户。 默认情况下，此帐户是站点服务器计算机的本地系统帐户。 可将域用户帐户指定为站点系统安装帐户。 有关详细信息，请参阅[帐户 - 站点系统安装帐户](../../../plan-design/hierarchy/accounts.md#site-system-installation-account)。

## <a name="install-roles-on-an-existing-site-system-server"></a><a name="bkmk_addrole"></a> 在现有站点系统服务器上安装角色

1. 在 Configuration Manager 控制台中，转到“管理”  工作区。 展开“站点配置”，然后选择“服务器和站点系统角色”节点   。 选择要在其上安装新站点系统角色的现有站点系统服务器。

1. 在功能区的“主页”选项卡上，在“服务器”组中，选择“添加站点系统角色”    。

1. 在“常规”页上，查看设置  。

    > [!TIP]
    >  若要从 Internet 访问站点系统角色，请确保指定 Internet 完全限定的域名 (FQDN)。

1. 在“代理”页上，如果此服务器上的角色需要 Internet 代理，则指定代理服务器的设置  。 有关详细信息，请参阅[代理服务器支持](../../../plan-design/network/proxy-server-support.md)。

1. 在“系统角色选择”页上，选择要添加的站点系统角色  。

1. 完成向导。 可能会显示针对特定角色的其他页面。 有关详细信息，请参阅[站点系统角色的配置选项](configuration-options-for-site-system-roles.md)。

> [!TIP]
> Windows PowerShell cmdlet **New-CMSiteSystemServer** 执行与此过程相同的功能。 有关详细信息，请参阅 [New-CMSiteSystemServer](/powershell/module/configurationmanager/new-cmsitesystemserver?view=sccm-ps)。

## <a name="install-roles-on-a-new-site-system-server"></a><a name="bkmk_createnew"></a> 在新站点系统服务器上安装角色

1. 在 Configuration Manager 控制台中，转到“管理”  工作区。 展开“站点配置”，然后选择“服务器和站点系统角色”节点   。

1. 在功能区的“主页”选项卡上，在“创建”组中，选择“创建站点系统服务器”    。

1. 在“常规”  页上，指定站点系统的常规设置。

    > [!TIP]
    > 若要从 Internet 访问新的站点系统角色，请确保指定 Internet FQDN。

1. 在“代理”页上，如果此服务器上的角色需要 Internet 代理，则指定代理服务器的设置  。 有关详细信息，请参阅[代理服务器支持](../../../plan-design/network/proxy-server-support.md)。

1. 在“系统角色选择”页上，选择要添加的站点系统角色  。

1. 完成向导。 可能会显示针对特定角色的其他页面。 有关详细信息，请参阅[站点系统角色的配置选项](configuration-options-for-site-system-roles.md)。

> [!TIP]
> Windows PowerShell cmdlet **New-CMSiteSystemServer** 执行与此过程相同的功能。 有关详细信息，请参阅 [New-CMSiteSystemServer](/powershell/module/configurationmanager/new-cmsitesystemserver?view=sccm-ps)。

## <a name="next-steps"></a>后续步骤

- [站点系统角色的配置选项](configuration-options-for-site-system-roles.md)

- [删除角色](../install/uninstall-sites-and-hierarchies.md#bkmk_role)