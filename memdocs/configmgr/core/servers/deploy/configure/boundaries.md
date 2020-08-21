---
title: 定义边界
titleSuffix: Configuration Manager
description: 了解如何在 Intranet 上定义可包含你要管理的设备的网络位置。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 13312c20edbda290daaa0d51908adeb7ab4a6860
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700055"
---
# <a name="define-network-locations-as-boundaries-for-configuration-manager"></a>将网络位置定义为 Configuration Manager 的边界

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 边界是网络上的位置，其中包含你要管理的设备。 可以创建不同类型的边界，例如 Active Directory 站点或网络 IP 地址。 当 Configuration Manager 客户端标识类似的网络位置时，相应设备就是边界的一部分。

Configuration Manager支持以下边界类型：

- IP 子网
- Active Directory 站点
- IPv6 前缀
- IP 地址范围
- VPN（自版本 2006 起）

可以手动创建各个边界，也可以使用 [Active Directory 林发现](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest)。 此发现方法自动查找并创建 IP 子网和 Active Directory 站点的边界。 当 Active Directory 林发现方法标识 Active Directory 站点的超网时，Configuration Manager 就会将超网转换为 IP 地址范围边界。

如果设备不在预期的边界内，可能是因为你没有将它的网络位置定义为边界。 当设备的网络位置不能确定时，请在设备上使用以下 Windows 命令进行确认：

- IP 地址：`ipconfig`
- Active Directory 站点：`nltest /dsgetsite`
- VPN：`ipconfig /all`

## <a name="boundary-types"></a>边界类型

### <a name="ip-subnet"></a>IP 子网

IP 子网边界类型需要子网 ID。 例如 `169.254.0.0`。 如果你提供“网络”（默认网关）和“子网掩码”值，Configuration Manager 会自动计算“子网 ID”。 当你保存边界时，Configuration Manager 只保存“子网 ID”值。

> [!NOTE]
> Configuration Manager 不支持直接输入超网作为边界。 作为替代，请使用 IP 地址范围边界类型。

### <a name="active-directory-site"></a>Active Directory 站点

对于“Active Directory 站点”边界类型，请指定站点名称。 可以键入名称，也可以浏览站点服务器的本地林。

如果你指定 Active Directory 站点边界，则边界包括作为此 Active Directory 站点成员的每个 IP 子网。 如果 Active Directory 站点的配置在 Active Directory 中发生变化，则此边界中包括的网络位置也会更改。  

Active Directory 站点边界不适用于纯 Azure Active Directory (Azure AD) 设备（亦称为“云域加入设备”）。 如果它们在本地漫游，而你只创建了 Active Directory 站点类型边界，那么这些设备将不会处于边界中。

> [!TIP]
> 运行以下 Windows 命令可以查看设备的当前 Active Directory 站点：`nltest /dsgetsite`。
>
> 若要确定客户端是否是云域加入客户端，请运行以下 Windows 命令：`dsregcmd /status`。 有关详细信息，请参阅 [dsregcmd 命令 - 设备状态](/azure/active-directory/devices/troubleshoot-device-dsregcmd)。

### <a name="ipv6-prefix"></a>IPv6 前缀

对于“IPv6 前缀”边界类型，请指定“前缀”。 例如 `2001:1111:2222:3333`。

### <a name="ip-address-range"></a>IP 地址范围

对于“IP 地址范围”边界类型，请指定地址范围的“起始 IP 地址”和“结束 IP 地址”。 地址范围可以包括一个 IP 子网的一部分，也可以包括多个 IP 子网。 使用 IP 地址范围边界类型来支持超网。

还可以使用此类型来定义单个 IP 地址的边界。 将起始和结束 IP 地址设置为相同的值。 此配置可能对独特设备或测试环境有用。

### <a name="vpn"></a>VPN

<!--7020519-->

自版本 2006 起，为了简化管理远程客户端，请创建 VPN 边界类型。 当客户端发送位置请求时，它包含有关其网络配置的其他信息。 根据此信息，服务器将确定客户端是否在 VPN 上。 为了使 Configuration Manager 能够在边界中关联客户端，请将设备连接到 VPN。

可以通过多种方式来配置 VPN 边界：

- 自动检测 VPN：Configuration Manager 检测任何使用点对点隧道协议 (PPTP) 的 VPN 解决方案。 如果它未检测到 VPN，请使用其他选项之一。 控制台列表中的边界值将为 `Auto:On`。

- **连接名称**：指定设备上 VPN 连接的名称。 这是 Windows 中用于 VPN 连接的网络适配器的名称。 Configuration Manager 匹配字符串的前 250 个字符，但不支持通配符或部分字符串。 控制台列表中的边界值将为 `Name:<name>`，其中 `<name>` 是指定的连接名称。

  例如，在设备上运行 `ipconfig` 命令，其中一个部分以 `PPP adapter ContosoVPN:` 开头。 使用字符串 `ContosoVPN` 作为“连接名称”。 它在列表中显示为 `Name:CONTOSOVPN`。

- 连接说明：指定 VPN 连接的说明。 Configuration Manager 匹配字符串的前 243 个字符，但不支持通配符或部分字符串。 控制台列表中的边界值将为 `Description:<description>`，其中 `<description>` 是指定的连接说明。

  例如，在设备上运行 `ipconfig /all` 命令，其中一个连接包含以下行：`Description . . . . . . . . . . . : ContosoMainVPN`。 使用字符串 `ContosoMainVPN` 作为“连接说明”。 它在列表中显示为 `Description:CONTOSOMAINVPN`。

> [!IMPORTANT]
> 若要充分利用此功能，更新站点后，还请将客户端更新到最新版本。 更新站点和控制台后，将在 Configuration Manager 控制台中显示新功能。 只有当客户端版本也是最新版本时，完整的方案才起作用。
>
> 要在操作系统部署过程中使用此 VPN 边界，请务必同时更新启动映像以包含最新的客户端二进制文件。

## <a name="create-a-boundary"></a>创建边界

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“层次结构配置”，然后选择“边界”节点。

1. 在功能区的“主页”选项卡上，选择“创建”组中的“创建边界”。

1. 在“创建边界”窗口的“常规”选项卡上，指定以下信息：

    - **描述**：通过易记名称或引用来标识边界。

        > [!NOTE]
        > Configuration Manager 会根据边界的类型和范围自动命名边界。 你无法修改此名称。

    - **类型**：选择要创建的边界的类型。 然后，指定此类型所需的其他信息。 有关详细信息，请参阅[边界类型](#boundary-types)。

1. 切换到“边界组”选项卡。如果站点中已有边界组，你可以立即将新建的此边界添加到一个或多个组中。

1. 选择“确定”，以保存新边界。

## <a name="configure-a-boundary"></a>配置边界

> [!TIP]
> 当你创建边界时，Configuration Manager 会根据边界的类型和范围自动命名边界。 你无法修改此名称。 为了帮助在 Configuration Manager 控制台中标识边界，请指定说明。

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“层次结构配置”，然后选择“边界”节点。

1. 选择要修改的边界。 在功能区“主页”选项卡的“属性”组中，选择“属性”。

1. 在边界的“属性”窗口的“常规”选项卡中，可以配置以下设置：

    - 编辑“说明”
    - 更改边界的“类型”
    - 通过编辑边界的网络位置来更改边界的范围。 例如，对于 Active Directory 站点边界，你可以指定新的 Active Directory 站点名称。

1. 若要查看与此边界关联的站点系统，请切换到“站点系统”选项卡。无法通过边界属性来更改此配置。

    > [!TIP]
    > 对于要作为边界的站点系统列出的服务器，请将它关联为至少一个包含此边界的边界组的站点系统服务器。 在边界组的“引用”选项卡上进行此配置。 有关详细信息，请参阅[配置站点分配并选择站点系统服务器](boundary-group-procedures.md#bkmk_references)。

1. 若要修改此边界的边界组成员资格，请选择“边界组”选项卡：

    - 若要将此边界添加到一个或多个边界组，请选择“添加”。 依次选择一个或多个边界组和“确定”。

    - 若要从边界组中删除此边界，请依次选择此边界组和“删除”。

1. 选择“确定”，以关闭边界属性，并保存配置。

## <a name="next-steps"></a>后续步骤

每个边界都可供层次结构中的每个站点使用。 创建边界后，将边界添加到一个或多个[边界组](boundary-groups.md)。