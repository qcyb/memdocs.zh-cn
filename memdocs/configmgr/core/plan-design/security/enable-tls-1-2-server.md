---
title: 在站点服务器和远程站点系统上启用传输层安全性 (TLS) 1.2
titleSuffix: Configuration Manager
description: 有关如何为 Configuration Manager 站点服务器启用 TLS 1.2 的信息。
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0ce9b428-cb0f-46f3-bf69-c465e6623d6f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 15377520b76b9b3a3813e6ad4253548f29e011db
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704095"
---
# <a name="how-to-enable-tls-12-on-the-site-servers-and-remote-site-systems"></a>如何在站点服务器和远程站点系统上启用 TLS 1.2

适用范围：  Configuration Manager (Current Branch)

为 Configuration Manager 环境启用 TLS 1.2 时，请先从[为客户端启用 TLS 1.2](enable-tls-1-2-client.md)开始。 然后再在站点服务器和远程站点系统上启用 TLS 1.2。 最后，测试客户端到站点系统的通信，然后在服务器端禁用较旧的协议（若适用）。 在站点服务器和远程站点系统上启用 TLS 1.2 需要完成以下任务：

- 确保在操作系统级别启用 TLS 1.2 作为 SChannel 协议
- 更新并配置 .NET Framework 以支持 TLS 1.2
- 更新 SQL Server 和客户端组件
- 更新 Windows Server Update Services (WSUS)

有关特定 Configuration Manager 功能和场景依赖项的详细信息，请参阅[关于启用 TLS 1.2](enable-tls-1-2.md)。 

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a> 确保在操作系统级别启用 TLS 1.2 作为 SChannel 协议

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a> 更新并配置 .NET Framework 以支持 TLS 1.2

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="update-sql-server-and-client-components"></a><a name="bkmk_sql"></a> 更新 SQL Server 和客户端组件

Microsoft SQL Server 2016 及更高版本支持 TLS 1.1 和 TLS 1.2。 早期版本和依赖库可能需要更新。 有关详细信息，请参阅 [KB 3135244：支持 Microsoft SQL Server 的 TLS 1.2](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)。

辅助站点服务器需要至少使用包含服务包 2 (13.2.50.26) 的 SQL Server 2016 Express，或更高版本。

### <a name="sql-server-native-client"></a><a name="bkmk_sql-client"></a> SQL Server Native Client

> [!NOTE]
> [KB 3135244](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) 还介绍了 SQL Server 客户端组件的要求。

此外，还要务必将 SQL Server Native Client 至少更新到 SQL 2012 SP4 (11.*.7001.0) 版本。 从版本 1810 起，此要求属于[先决条件检查（警告）](../../servers/deploy/install/list-of-prerequisite-checks.md#sql-server-native-client)。

Configuration Manager 对以下站点系统角色使用 SQL Server Native Client：

- 站点数据库服务器
- 站点服务器：管理中心站点、主站点或辅助站点
- 管理点
- 设备管理点
- 状态迁移点
- SMS 提供程序
- 软件更新点
- 启用多播的分发点
- 资产智能更新服务点
- Reporting Services 点
- 应用程序目录 Web 服务
- 注册点
- Endpoint Protection 点
- 服务连接点
- 证书注册点
- 数据仓库服务点


## <a name="update-windows-server-update-services-wsus"></a><a name="bkmk_wsus"></a> 更新 Windows Server Update Services (WSUS)

若要在 WSUS 的早期版本中支持 TLS 1.2，请在 WSUS 服务器上安装以下更新：

- 对于运行 Windows Server 2012 的 WSUS 服务器，安装[更新 4022721](https://support.microsoft.com/help/4022721) 或更高版本的汇总更新。
- 对于运行 Windows Server 2012 R2 的 WSUS 服务器，安装[更新 4022720](https://support.microsoft.com/help/4022720) 或更高版本的汇总更新。

从 Windows Server 2016 开始，WSUS 默认支持 TLS 1.2。  只需在 Windows Server 2012 和 Windows Server 2012 R2 WSUS 服务器上进行 TLS 1.2 更新。

## <a name="next-steps"></a>后续步骤

- [启用 TLS 1.2 时的常见问题](enable-tls-1-2-troubleshoot.md)
