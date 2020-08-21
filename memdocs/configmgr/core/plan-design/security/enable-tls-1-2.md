---
title: 启用传输层安全性 (TLS) 1.2 概述
titleSuffix: Configuration Manager
description: 有关如何为 Configuration Manager 启用 TLS 1.2 的概述。
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 31de47c9-891b-4de7-8d5e-fbbc1bff7c60
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8e1334603bcf60ea3eb8c3d18b73d511570cdc5d
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699732"
---
# <a name="how-to-enable-tls-12"></a>如何启用 TLS 1.2

适用范围：  Configuration Manager (Current Branch)

传输层安全性 (TLS) 像安全套接字层 (SSL) 一样，是一种加密协议，可在通过网络传输数据时保护数据安全。 这些文章介绍了确保 Configuration Manager 使用 TLS 1.2 协议安全通信所需的步骤。 这些文章还介绍了常用组件的更新要求，以及常见问题的故障排除。

## <a name="enabling-tls-12"></a>启用 TLS 1.2

Configuration Manager 依赖于许多不同的组件来实现安全通信。 用于给定连接的协议取决于客户端和服务器端相关组件的功能。 如果任何组件过期或未正确配置，则通信可能使用较旧的、安全性较差的协议。 要让 Configuration Manager 能够支持使用 TLS 1.2 进行所有安全通信，必须为所有必需的组件启用 TLS 1.2。 所需的组件取决于环境和所用的 Configuration Manager 功能。

> [!IMPORTANT]
> 使用客户端启动此进程（尤其是 Windows 早期版本）。 在 Configuration Manager 服务器上启用 TLS 1.2 并禁用较旧的协议前，先确保所有客户端都支持 TLS 1.2。 否则，客户端将无法与服务器通信，从而可能会被孤立。


## <a name="tasks-for-configuration-manager-clients-site-servers-and-remote-site-systems"></a>Configuration Manager 客户端、站点服务器和远程站点系统的任务

若要为 Configuration Manager 依赖的组件启用 TLS 1.2 以实现安全通信，需在客户端和站点服务器上执行多个任务。

### <a name="enable-tls-12-for-configuration-manager-clients"></a>为 Configuration Manager 客户端启用 TLS 1.2

- [更新 Windows 8.0、Windows Server 2012（非 R2）及更早版本上的 Windows 和 WinHTTP](enable-tls-1-2-client.md#bkmk_winhttp)
- [确保在操作系统级别启用 TLS 1.2 作为 SChannel 协议](enable-tls-1-2-client.md#bkmk_protocol)
- [更新并配置 .NET Framework 以支持 TLS 1.2](enable-tls-1-2-client.md#bkmk_net)


### <a name="enable-tls-12-for-configuration-manager-site-servers-and-remote-site-systems"></a>为 Configuration Manager 客户端、站点服务器和远程站点系统启用 TLS 1.2

- [确保在操作系统级别启用 TLS 1.2 作为 SChannel 协议](enable-tls-1-2-server.md#bkmk_protocol)
- [更新并配置 .NET Framework 以支持 TLS 1.2](enable-tls-1-2-server.md#bkmk_net)
- [更新 SQL Server 和 SQL Native Client](enable-tls-1-2-server.md#bkmk_sql)
- [更新 Windows Server Update Services (WSUS)](enable-tls-1-2-server.md#bkmk_wsus)


## <a name="features-and-scenario-dependencies"></a>功能和场景依赖项

本部分介绍特定 Configuration Manager 功能和场景的依赖项。 请找到适用于你所在环境的项目，以确定后续步骤。

|功能或方案|更新任务|
|--- |--- |
|站点服务器（中央站点服务器、主站点服务器或辅助站点服务器）| - [更新 .NET Framework](enable-tls-1-2-server.md#bkmk_net)<br/> - 验证强加密设置|
|站点数据库服务器|[更新 SQL Server 及其客户端组件](enable-tls-1-2-server.md#bkmk_sql)|
|辅助站点服务器|[更新 SQL Server 及其客户端组件](enable-tls-1-2-server.md#bkmk_sql) 至 SQL Express 兼容版本|
|站点系统角色| - [更新 .NET Framework](enable-tls-1-2-server.md#bkmk_net)，并验证强加密设置 <br/> - 在需要 SQL Server 的角色上[更新 SQL Server 及其客户端组件](enable-tls-1-2-server.md#bkmk_sql)包括 [SQL Server Native Client](enable-tls-1-2-server.md#bkmk_sql-client)|
|Reporting Services 点|- 在站点服务器、SQL Reporting Services 服务器及使用此控制台的任意计算机上[更新 .NET Framework](enable-tls-1-2-server.md#bkmk_net)<br/> - 根据需要重新启动 SMS_Executive 服务|
|软件更新点|[更新 WSUS](enable-tls-1-2-server.md#bkmk_wsus)|
|云管理网关|[强制执行 TLS 1.2](../../clients/manage/cmg/security-and-privacy-for-cloud-management-gateway.md#bkmk_tls)|
|Configuration Manager 控制台| - [更新 .NET Framework](enable-tls-1-2-client.md#bkmk_net)<br/> - 验证强加密设置|
|Configuration Manager 客户端与 HTTPS 站点系统角色|[更新 Windows 以支持通过使用 WinHTTP 进行客户端服务器通信的 TLS 1.2](enable-tls-1-2-client.md#bkmk_winhttp)|
|软件中心| - [更新 .NET Framework](enable-tls-1-2-client.md#bkmk_net)<br/> - 验证强加密设置|
|Windows 7 客户端| 在任何服务器组件上启用 TLS 1.2 前，请先[更新 Windows 以支持通过使用 WinHTTP 进行客户端服务器通信的 TLS 1.2](enable-tls-1-2-client.md#bkmk_winhttp)。  若先在服务器组件上启用了 TLS 1.2，可能会孤立客户端的早期版本。|

## <a name="frequently-asked-questions"></a>常见问题解答

### <a name="why-use-tls-12-with-configuration-manager"></a>为什么要将 TLS 1.2 用于 Configuration Manager？

TLS 1.2 比以前的加密协议（例如 SSL 2.0、SSL 3.0、TLS 1.0 和 TLS 1.1）更安全。 实质上，TLS 1.2 可以使在网络上传输的数据更安全。

### <a name="where-does-configuration-manager-use-encryption-protocols-like-tls-12"></a>Configuration Manager 在哪里使用 TLS 1.2 等加密协议？

Configuration Manager 基本上会在 5 方面使用 TLS 1.2 等加密协议：

- 角色配置为使用 HTTPS 时客户端与基于 IIS 的站点服务器角色的通信。 这些角色的示例包括分发点、软件更新点和管理点。
- 管理点、SMS Executive 和 SMS 提供程序与 SQL 的通信。 Configuration Manager 始终加密 SQL 通信。
- WSUS 配置为使用 HTTPS 时，站点服务器到 WSUS 的通信。
- SSRS 配置为使用 HTTPS 时，Configuration Manager 控制台与 SQL Reporting Services (SSRS) 的通信。
- 与基于 Internet 的服务的任何连接。 示例包括云管理网关 (CMG)、服务连接点同步和 Microsoft 更新更新元数据同步。

### <a name="what-determines-which-encryption-protocol-is-used"></a>所用加密协议由什么决定？

HTTPS 将始终在加密对话中协商客户端和服务器均支持的最高协议版本。 建立连接后，客户端会立即向服务器发送消息，告知其最高可用协议版本。 如果服务器也支持该版本，它将使用该版本发送消息。 这个经协商的版本会用于连接。 如果服务器不支持客户端提议的版本，服务器消息将制定它可用的最高版本。 有关 TLS 握手协议的详细信息，请参阅[使用 TLS 建立安全会话](/windows/win32/secauthn/tls-handshake-protocol#establishing-a-secure-session-by-using-tls)。

### <a name="what-determines-which-protocol-version-the-client-and-server-can-use"></a>客户端和服务器可使用的协议版本由什么确定？

一般说来，以下项可确定所用的协议版本：

- 应用程序可指定要协商的特定协议版本。
  - 最佳做法指定避免在应用程序级别硬编码特定协议版本，并遵循在组件和操作系统协议级别定义的配置。
  - Configuration Manager 遵循此最佳做法。
- 对于使用 .NET Framework 编写的应用程序，默认协议版本取决于用于编译的框架的版本。  
  - 低于 4.6.3 的 .NET 版本的默认待协商协议列表中不包含 TLS 1.1 和 1.2。
- 使用 WinHTTP 进行 HTTPS 通信的应用程序（例如 Configuration Manager 客户端）依赖于操作系统版本、补丁级别和协议版本支持配置。


## <a name="additional-resources"></a>其他资源

- [加密控制技术参考](cryptographic-controls-technical-reference.md)
- [.NET Framework 中的传输层安全性 (TLS) 最佳做法](/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244：支持 Microsoft SQL Server 的 TLS 1.2](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)

## <a name="next-steps"></a>后续步骤

- [在客户端上启用 TLS 1.2](enable-tls-1-2-client.md)
- [在站点服务器上启用 TLS 1.2](enable-tls-1-2-server.md)