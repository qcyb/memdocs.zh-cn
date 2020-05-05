---
title: 为本地 MDM 安装角色
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中为本地移动设备管理（MDM）安装所需的站点系统角色。
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f47d78eeafb745732d4917dd7abd80f752f4dd20
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724701"
---
# <a name="install-site-system-roles-for-on-premises-mdm-in-configuration-manager"></a>在 Configuration Manager 中为本地 MDM 安装站点系统角色

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 本地移动设备管理（MDM）在 Configuration Manager 站点中需要以下站点系统角色：

- 注册点

- 注册代理点

- 分发点

- 设备管理点，它是你允许用于移动设备的管理点

## <a name="requirements-and-limitations"></a>要求和限制

- 本地 MDM 要求你启用站点系统角色以进行 HTTPS 通信。 有关详细信息，请参阅[在本地 MDM 中为受信任通信设置证书](set-up-certificates-on-premises-mdm.md)。

- Configuration Manager 的 current branch 仅支持从设备到分发点的*intranet*连接和本地 MDM 的设备管理点。 但是，如果你还管理 macOS 计算机，则这些客户端需要与那些相同的角色建立*internet*连接。 当你配置分发点和设备管理点时，请使用选项 "**允许 intranet 和 internet 连接**"。

- 为 intranet 连接配置的分发点需要为其配置站点边界。 Configuration Manager 仅支持用于本地 MDM 的 IPv4 范围边界。 有关详细信息，请参阅[定义站点边界和边界组](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)。

- 如果将[数据库副本](../../core/servers/deploy/configure/database-replicas-for-management-points.md)用于设备管理点，则新注册的设备最初将无法连接。 出现这种连接失败的原因是数据库副本没有关于成功连接所需的新注册设备的信息。 副本每5分钟同步一次。 注册后的前五分钟，设备将无法连接，这通常是两次连接尝试。 然后，设备将成功连接。

## <a name="add-roles"></a>添加角色

如果要将本地 MDM 添加到具有 Configuration Manager 客户端管理的大多数设备的站点，则可能已在站点中安装了其中一些角色。 例如，分发点是一个常见的角色，并且需要设备管理点来管理 macOS 设备。

有关如何向网站添加角色的详细信息，请参阅[添加站点系统角色](../../core/servers/deploy/configure/install-site-system-roles.md)。

## <a name="configure-roles"></a>配置角色

配置新的或现有的角色来管理移动设备。 按照以下步骤配置分发点和设备管理点，以便为本地 MDM 正确运行：

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“服务器和站点系统角色”节点    。

1. 选择包含要配置的分发点或设备管理点的站点系统服务器。 在列表中选择服务器，然后在 "站点系统角色" 详细信息窗格中选择**站点系统**角色。 在功能区中的 "**站点角色**" 选项卡上，选择 "**属性**"。

    > [!TIP]
    > 在大型站点中，你可以将视图的作用域限定为仅显示具有特定角色的服务器。 选择 "**服务器和站点系统角色**" 节点后，在功能区的 "主页" 标记中，选择 "**具有角色的服务器**"。 然后从站点中当前可用的角色列表中选择所需的角色。

    在**站点系统属性**的 "**常规**" 选项卡上，确保**名称**是完全限定的域名（FQDN）。 关闭属性。

1. 在控制台列表中，选择具有本地分发点角色的服务器。 选择 "站点系统角色" 详细信息窗格中的**分发点**角色。 在功能区中的 "**站点角色**" 选项卡上，选择 "**属性**"。 在**分发点属性**的 "**通信**" 选项卡上：

    1. 选择 " **HTTPS**"，并选择 "**仅允许 intranet 连接**"。

        > [!IMPORTANT]
        > 如果你还使用 Configuration Manager 客户端管理 macOS 计算机，请改用 "**允许 intranet 和 internet 连接**"。

    1. 启用 "**允许移动设备连接到此分发点**" 选项，然后关闭属性。

1. 打开**管理点**站点系统角色的 "属性"。

    1. 在 "**常规**" 选项卡上，选择 " **HTTPS**"，并选择 "**仅允许 intranet 连接**"。

        > [!IMPORTANT]
        > 如果你还使用 Configuration Manager 客户端管理 macOS 计算机，请改用 "**允许 intranet 和 internet 连接**"。

    1. 启用 "**允许移动设备和 Mac 计算机使用此管理点**" 选项，然后关闭属性。

        > [!NOTE]
        > 此选项实际上会将管理点变为*设备*管理点。  

## <a name="next-step"></a>后续步骤

添加并配置用于管理移动设备的角色后，请将服务器配置为受信任终结点。 此信任使角色能够与托管设备通信并注册这些设备。

> [!div class="nextstepaction"]
> [Set up certificates for trusted communications](set-up-certificates-on-premises-mdm.md)
