---
title: 创建远程连接配置文件
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 远程连接配置文件使用户可以远程连接到工作计算机。
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 8c6eabc4-5dda-4682-b03e-3a450e6ef65a
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c9a06e1b7c14cda02a8029925785c2109ea4204b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692465"
---
# <a name="remote-connection-profiles-in-configuration-manager"></a>Configuration Manager 中的远程连接配置文件

适用范围：  Configuration Manager (Current Branch)

使用 Configuration Manager 远程连接配置文件使用户可以远程连接到工作计算机。 利用这些配置文件，你可以将远程桌面连接设置部署到层次结构中的用户。 用户可以经 VPN 连接通过远程桌面访问他们的任何主要工作计算机。  

> [!IMPORTANT]  
> 使用 Configuration Manager 指定远程连接配置文件设置时，客户端会将设置存储在 Windows 本地策略中。 这些设置可能会替代另一个应用程序配置的远程桌面设置。 此外，如果你使用 Windows 组策略配置远程桌面设置，则组策略中指定的设置将会替代 Configuration Manager 设置。

Configuration Manager 会在客户端上创建“远程电脑连接”安全组  。 部署远程连接配置文件时，客户端会将计算机的主要用户添加到此组。 本地管理员可以手动将用户添加到此组或从此组删除用户，但 Configuration Manager 在下次评估配置文件的符合性时会更新成员身份。

> [!IMPORTANT]  
> 如果用户和设备之间的用户设备相关性发生更改，Configuration Manager 将禁用远程连接配置文件和 Windows 防火墙设置以防止连接到该计算机。

## <a name="prerequisites"></a>必备条件  

### <a name="external-dependencies"></a>外部依赖关系  

- 如果要允许用户连接 Internet，则必须安装和配置远程桌面网关服务器。 有关如何安装和配置远程桌面网关服务器的详细信息，请参阅[远程桌面服务器 - 从任意位置访问](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-plan-access-from-anywhere)。

- 如果客户端运行基于主机的防火墙，该防火墙必须启用 mstsc.exe 程序。 在配置远程连接配置文件时，请启用“对 Windows 域和专用网络上的连接允许 Windows 防火墙例外”设置  。 此设置允许 Configuration Manager 自动配置 Windows 防火墙。

    > [!TIP]
    > 用于配置 Windows 防火墙的组策略设置可能会覆盖在 Configuration Manager 中设置的配置。 如果使用组策略来配置 Windows 防火墙，请确保组策略设置不会阻止 mstsc.exe。

    如果客户端运行其他基于主机的防火墙，请手动配置此防火墙依赖关系。  

### <a name="configuration-manager-dependencies"></a>Configuration Manager 依赖关系  

- 为了使用户连接到工作计算机，该计算机必须是用户的主设备。 有关详细信息，请参阅[将用户和设备与用户设备相关性进行链接](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)。

- 若要管理远程连接配置文件，则用户帐户需要 Configuration Manager 中的特定权限。 “符合性设置管理员”内置角色包括管理这些配置文件所需的权限  。 有关详细信息，请参阅[配置基于角色的管理](../../core/servers/deploy/configure/configure-role-based-administration.md)。

## <a name="security-and-privacy-considerations"></a>安全和隐私注意事项

### <a name="security-considerations"></a>安全注意事项  

- 手动指定用户设备相关性，而不是允许用户确定其主设备。 不要启用基于使用情况的配置。

  - 在部署远程连接配置文件之前，需要启用“允许工作计算机的所有主要用户进行远程连接”选项  。 通过此配置，可始终手动指定用户设备相关性。 不考虑 Configuration Manager 从用户或从极可信赖的设备中收集的信息。 如果部署配置文件，并且受信任的管理用户未指定用户设备相关性，则未授权用户可能会收到提升的权限，并能远程连接到计算机。

  - Configuration Manager 通过状况消息收集基于使用情况的信息，这是一种快速但不安全的通信通道。 为了帮助减轻此威胁，请在客户端计算机和管理点之间使用服务器消息块 (SMB) 签名或 Internet 协议安全性 (IPsec)。

- 限制站点服务器计算机上的本地管理员权限。 站点服务器上的本地管理员可向 Configuration Manager 自动创建和维护的“远程 PC 连接”安全组中手动添加成员  。 由于成员会接收远程桌面权限，因此此操作可能会导致权限提升。

### <a name="privacy-considerations"></a>隐私注意事项  

用户远程连接到工作计算机时，会下载 .wsrdp 文件。 此文件包含设备名称和远程桌面网关服务器名称。 创建远程桌面会话需要这些值。 会自动下载并以本地方式保存 .wsrdp 文件。 用户下次运行“远程桌面”会话时，会覆盖此文件。  

## <a name="create-a-profile"></a>创建配置文件

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，展开“符合性设置”，然后选择“远程连接配置文件”    。  

1. 在功能区的“主页”选项卡上，选择“创建”组中的“创建远程连接配置文件”    。  

1. 在“创建远程连接配置文件向导”的“常规”页上，为每个配置文件指定名称和可选描述   。 两个值的最大限制为 256 个字符。  

1. 在“配置文件设置”页上指定下列设置  ：  

    - **远程桌面网关服务器的完整名称和端口(可选)** ：指定要用于连接的远程桌面网关服务器的名称。 此值具有下列要求：

        - 服务器名称不得超过 256 个字符。
        - 可以包含大写字母、小写字母和数字字符。
        - 除段之间的句点 (`.`) 和端口前的冒号 (`:`) 以外，允许使用的其他特殊字符为破折号 (`–`) 和下划线 (`_`)。
        - Configuration Manager 不支持使用此值的国际化域名。

    - **只允许通过网络级别身份验证运行远程桌面的计算机中的连接**：默认启用，此设置能提升连接的安全级别。 有关详细信息，请参阅[授予远程桌面访问权限](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#why-allow-connections-only-with-network-level-authentication)。

    - 启用以下连接设置：

        - **允许至工作计算机的远程连接**

        - **允许工作计算机的所有主要用户进行远程连接**

        - **对 Windows 域和专用网络上的连接允许 Windows 防火墙例外**

        > [!IMPORTANT]  
        > 所有三个设置必须相同，然后才能继续操作。

        仅在部署配置文件以关闭远程连接时禁用这些设置。

1. 完成向导。

新的配置文件将显示在“资产和符合性”工作区的“远程连接配置文件”节点中   。  

## <a name="deploy"></a>部署

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区，展开“符合性设置”，然后选择“远程连接配置文件”    。

1. 在“远程连接配置文件”列表中，选择要部署的配置文件  。 在功能区的“主页”选项卡上，在“部署”组中，选择“部署”    。  

1. 在“部署远程连接配置文件”窗口中，指定下列信息  ：

    - **集合**：浏览以选择要在其中部署配置文件的设备集合。

    - **在支持时修正非符合性规则**：启用此设置可在配置文件设置不符合设备时自动进行修正。 如果配置文件不存在，则它可能是不符合的。

    - **允许维护时段外的修正**：如果为其中部署了配置文件的集合配置维护时段，请启用此选项以让 Configuration Manager 在维护时段外修正它。 有关详细信息，请参阅[如何使用维护时段](../../core/clients/manage/collections/use-maintenance-windows.md)。

    - **生成警报**：启用此选项可配置符合性警报。

    - **指定此配置基线的符合性评估计划**：指定客户端评估配置文件所依据的简单或自定义计划。

1. 选择“确定”，关闭窗口并创建部署  。

### <a name="client-evaluation"></a>客户端评估

用户登录时，客户端会评估配置文件。

如果设备保留其中部署了远程连接配置文件的集合，则 Configuration Manager 会禁用设备上的设置。 但是，要使此进程正常发生，你必须已至少部署了一个配置项目或包含站点中的配置项目的配置基线。

### <a name="conflict-resolution"></a>冲突解决

请勿在同一设备上部署多个具有冲突设置的远程连接配置文件。 例如，将两个具有不同设置的配置文件部署到同一集合。 仅将一个配置文件部署配置为“在支持时修正非符合性规则”  。 此部署可能会替代其他配置文件中的设置。 Configuration Manager 不支持这种类型的远程连接配置文件部署。

## <a name="monitor"></a>监视

在 Configuration Manager 控制台中，转到“监视”工作区，然后选择“部署”   。 在“部署”列表中，选择远程连接配置文件部署  。

你可以在主页上查看有关远程连接配置文件部署符合性的摘要信息。 若要查看更多详细信息，请选择配置文件部署。 然后在功能区的“主页”选项卡上的“部署”组中，选择“查看状态”    。 此操作会打开“部署状态”页面  。  

“部署状态”  页包含下列选项卡：  

- **符合**：显示基于受影响资产数量的远程连接配置文件的符合性。

    > [!IMPORTANT]  
    > 如果不适用，客户端不会评估远程连接配置文件。 但它仍会报告符合性。

- **错误**：显示基于受影响资产数量的所选远程连接配置文件部署的所有错误的列表。

- **不符合**：显示基于受影响资产数量的远程连接配置文件内所有不符合规则的列表。

- **未知**：显示没有为所选远程连接配置文件部署报告符合性的所有设备的列表，以及设备的当前客户端状态。

在任何选项卡上，打开规则以在“资产和符合性”工作区中的“用户”节点下创建一个临时子节点   。 此子节点包含具有所选选项卡符合性状态的所有设备。

“资产详细信息”窗格显示具有此配置文件所选符合性状态的设备  。 打开列表中的设备以显示其他信息。

## <a name="reports"></a>报表

Configuration Manager 中包括内置报表，可用于监视有关远程连接配置文件的信息。 这些报表的报表类别为“符合性和设置管理”  。  

> [!IMPORTANT]  
> 在符合性设置报表中使用参数“设备筛选器”和“用户筛选器”时，请使用通配符 (`%`)   。  

有关如何在 Configuration Manager 中配置报表的详细信息，请参阅[报表简介](../../core/servers/manage/introduction-to-reporting.md)。  
