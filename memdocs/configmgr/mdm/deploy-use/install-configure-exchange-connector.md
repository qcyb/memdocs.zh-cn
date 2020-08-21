---
title: 安装 Exchange Connector
titleSuffix: Configuration Manager
description: 安装并配置 Exchange connector for Configuration Manager 通过 ActiveSync 来管理移动设备。
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: e179e30a-a1fc-461e-8087-ff3a55803450
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e0db550369ca2d81f42a25e68960b5f8f27be168
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700474"
---
# <a name="install-and-configure-the-exchange-connector"></a>安装和配置 Exchange connector

适用范围：  Configuration Manager (Current Branch)

使用此过程来安装和配置 Exchange Server 连接器来管理移动设备。 Configuration Manager 仅支持一个 Exchange 组织包含一个连接器。

在为 Configuration Manager 安装 Exchange Server 连接器之前，请确保具有所需的权限和版本。 有关详细信息，请参阅 [Exchange 和 Configuration Manager 的设备管理](manage-mobile-devices-with-exchange-activesync.md#prerequisites)。

## <a name="exchange-connection-account"></a>Exchange 连接帐户

决定哪个帐户将连接到 Exchange 客户端访问服务器来管理移动设备。 该帐户可以是站点服务器的计算机帐户或 Windows 用户帐户。

然后，在 Exchange 角色组中配置此帐户以运行以下 Exchange Server cmdlet：

- **Clear-ActiveSyncDevice**  

- **Get-ActiveSyncDevice**  

- **Get-ActiveSyncDeviceAccessRule**  

- **Get-ActiveSyncDeviceStatistics**  

- **Get-ActiveSyncMailboxPolicy**  

- **Get-ActiveSyncOrganizationSettings**  

- **Get-ExchangeServer**  

- **Get-Mailbox**

- **Get-Recipient**  

- **Set-ADServerSettings**  

- **Set-ActiveSyncDeviceAccessRule**  

- **Set-ActiveSyncMailboxPolicy**  

- **Set-CASMailbox**  

- **New-ActiveSyncDeviceAccessRule**  

- **New-ActiveSyncMailboxPolicy**  

- **Remove-ActiveSyncDevice**  

- **Get-CasMailbox**  

- **获取-用户**  

- **Set-ActiveSyncOrganizationSettings**  

以下 Exchange Server 管理角色包括这些 cmdlet：

- 收件人管理
- 仅查看组织管理
- 服务器管理

有关详细信息，请参阅 Exchange Server 2013 文档中的 [了解管理角色组](/exchange/understanding-management-role-groups-exchange-2013-help) 。

> [!TIP]  
> 如果你尝试在没有所需 cmdlet 的情况下安装或使用 Exchange Server 连接器，你将在站点服务器计算机上的 Easdisc.log 文件中看到以下错误： `Invoking cmdlet <cmdlet> failed` 。

## <a name="install-the-connector"></a>安装连接器

1. 在 Configuration Manager 控制台中，打开 " **管理** " 工作区，展开 " **层次结构配置**"，然后选择 " **Exchange Server 连接器**"。

1. 在功能区的 " **主页** " 选项卡的 " **创建** " 组中，选择 " **添加 Exchange 服务器**"。

1. 在 "添加 Exchange Server 向导" 的 " **常规** " 页上，选择一个 Exchange Server 环境：

    - **本地 Exchange server**：为每个 Active Directory 站点指定单一服务器或客户端访问服务器阵列。

        如果服务器或阵列脱机，Configuration Manager 将尝试发现要使用的客户端访问服务器。 如果该操作失败，Configuration Manager 将回退，使用邮箱服务器来建立与客户端访问服务器的连接。 当它重试连接时，它将在站点服务器计算机上的 Easdisc.log 文件中记录以下警告： `Failed to open runspace for site <site_name>` 。

    - **托管 Exchange Server**：指定 exchange Online 环境的服务器地址。

    然后选择要运行 Exchange Server 连接器的主站点。

1. 在 " **帐户** " 页上，指定要连接到 Exchange 服务器的帐户。 有关详细信息，请参阅 [Exchange 连接帐户](#exchange-connection-account)。

1. 在 " **发现** " 页上，配置用于查找设备的同步计划和规则。

1. 在 " **设置** " 页上，配置以下组中的移动设备设置：

    - **常规**
    - **密码**
    - **电子邮件管理**
    - **安全性**
    - **应用程序**

    有关详细信息，请参阅 [Exchange connector 设置](manage-mobile-devices-with-exchange-activesync.md#policies)。

    如果还使用 Configuration Manager [本地 MDM](../understand/manage-mobile-devices-with-on-premises-infrastructure.md)注册移动设备，请启用 " **允许外部移动设备管理**" 选项。 此设置允许这些移动设备在 Configuration Manager 注册它们后继续从 Exchange 接收电子邮件。

1. 完成向导。

## <a name="verify-and-monitor"></a>验证和监视

验证 Exchange Server 连接器的安装是否具有状态消息和日志文件：

- 确认站点组件管理器已成功安装 Exchange Server 连接器。 从**SMS_EXCHANGE_CONNECTOR**组件中查找消息状态 ID **1015** 。

    如果指定的客户端访问服务器脱机，安装可能会失败。 如果 Configuration Manager 无法成功安装连接器，Configuration Manager 每60分钟重试一次安装。 它将继续重试，直到安装成功或者你删除 Exchange Server 连接器为止。

- 在站点服务器计算机上，查看 **sitecomp.log** 中的以下条目： `Component SMS_EXCHANGE_CONNECTOR flagged for installation` 。 然后，它会记录成功安装，其中包含以下文本： `STATMSG: ID=1015` 。

完成安装后，请监视连接器找到和管理的移动设备。 查看移动设备的集合，并使用移动设备的报表。

> [!NOTE]  
> Configuration Manager 将为它找到的移动设备生成名称。 它使用 *用户名*_*设备类型*格式。 例如， **jdoe_WindowsPhone**。 如果用户有多台具有相同设备类型的移动设备，Configuration Manager 将在控制台和报表中对这些移动设备显示同一名称。  

## <a name="see-also"></a>另请参阅

- [配置客户端和站点系统使用的端口](../../core/plan-design/hierarchy/ports.md#BKMK_PortsExchangeConnectorHosted)
- [代理服务器支持](../../core/plan-design/network/proxy-server-support.md#site-system-roles-that-use-a-proxy)
- [移动设备的安全建议](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#bkmk_mobile)
- [通过 Exchange Server 连接器管理的移动设备的隐私信息](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#BKMK_Privacy_ExchangeConnector)