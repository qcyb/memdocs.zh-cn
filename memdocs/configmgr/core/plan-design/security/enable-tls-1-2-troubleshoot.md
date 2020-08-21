---
title: 启用传输层安全性 (TLS) 1.2 时的常见问题
titleSuffix: Configuration Manager
description: 描述启用传输层安全性 (TLS) 1.2 时的常见问题
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 15083f28-8ff2-4e23-9f5e-b5dbd0859839
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 316387bc42ed51dd9b581a25208091ed93cad1d1
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699749"
---
# <a name="common-issues-when-enabling-tls-12"></a>启用 TLS 1.2 时的常见问题

本文针对在 Configuration Manager 中启用 TLS 1.2 支持时出现的常见问题提供建议。

## <a name="unsupported-platforms"></a>不受支持的平台

以下客户端平台受 Configuration Manager 的支持，但不受 TLS 1.2 环境的支持：

- Windows CE
- Apple OS X
- 使用本地 MDM 托管的 Windows 10 设备

## <a name="reports-dont-show-in-the-console"></a>控制台未显示报表

若 Configuration Manager 控制台未显示报表，请务必更新运行该控制台的计算机。 [更新 .NET Framework](enable-tls-1-2-client.md#bkmk_net)，并启用强加密。

## <a name="fips-security-policy-enabled"></a>已启用 FIPS 安全策略

若为客户端或服务器启用了 FIPS 安全策略设置，安全通道 (Schannel) 协商可能会导致它们使用 TLS 1.0。 即使在注册表中禁用此协议，也会发生此行为。

若要进行研究，请启用安全通道事件日志记录，然后在系统日志中检查 Schannel 事件。 有关详细信息，请参阅[如何限制 Schannel.dll 中某些加密算法和协议的使用](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc)。

## <a name="sql-server-communication-failure"></a>SQL Server 通信失败

如果 SQL Server 通信失败并返回 SslSecurityError  错误，请确认以下设置：

- [更新 .NET Framework](enable-tls-1-2-server.md#bkmk_net)，并在各个计算机上启用强加密
- 在主机服务器上[更新 SQL Server](enable-tls-1-2-server.md#bkmk_sql)
- 在与 SQL 通信的所有系统上[更新 SQL 客户端组件](enable-tls-1-2-server.md#bkmk_sql-client)。 例如，站点服务器、SMS 提供程序和站点角色服务器。

## <a name="configuration-manager-client-communication-failures"></a>Configuration Manager 客户端通信失败

若 Configuration Manager 客户端无法与站点角色通信，请验证是否已[更新 Windows](enable-tls-1-2-client.md#bkmk_winhttp) 以支持使用 WinHTTP 进行客户端服务器通信的 TLS 1.2。 常见的站点角色包括分发点、管理点和状态迁移点。

## <a name="reporting-services-point-fails-and-returns-an-expected-error"></a>Reporting Services 点失败并返回预期错误

如果 Reporting Services 点没有配置报表，请检查 SRSRP.log  是否存在以下错误条目：

`The underlying connection was closed:`
`An expected error occurred on a receive.`

若要解决此问题，请执行下列步骤：

1. [更新 .NET Framework](enable-tls-1-2-client.md#bkmk_net)，并在所有相关计算机上启用强加密。

1. 在安装任意更新后，重新启动 SMS_Executive 服务。

## <a name="application-catalog-doesnt-initialize"></a>应用程序目录未初始化

> [!Important]  
> 版本 1910 已终止对应用程序目录角色的支持。 有关详细信息，请参阅[已删除和已弃用的功能](../changes/deprecated/removed-and-deprecated-cmfeatures.md)。

如果应用程序目录未初始化，请检查 ServicePortalWebSite.svclog  文件是否存在以下错误条目：

`SOAP security negotiation failed. The client and server can't communicate because they don't share a common algorithm.`

若要解决此问题，请执行下列步骤：

1. [更新 .NET Framework](enable-tls-1-2-client.md#bkmk_net)，并在所有相关计算机上启用强加密。

1. 在应用程序目录服务器的 `%WinDir%\System32\InetSrv` 文件夹中，使用以下内容创建 W2SP.exe.config  文件：

    ``` XML
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <runtime>
      <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
      </runtime>
    </configuration>
    ```

    > [!NOTE]
    > 如果应用程序是使用 .NET Framework 4.6.3 生成的，则这是要创建的默认文件。

1. 为应用程序目录角色使用 HTTPS 传输安全性。

    > [!Important]
    > 当为应用程序目录角色使用 HTTP 消息安全性时，WCF 将被硬编码为只使用 SSL 3.0 和 TLS 1.0。 这可以防止使用 TLS 1.2。

1. 如果有任何更改，请重新启动计算机。

## <a name="software-center-or-browser-doesnt-communicate-with-the-application-catalog"></a>软件中心或浏览器不与应用程序目录通信

> [!Important]  
> 版本 1910 已终止对应用程序目录角色的支持。 有关详细信息，请参阅[已删除和已弃用的功能](../changes/deprecated/removed-and-deprecated-cmfeatures.md)。

若要让软件中心使用启用了 TLS 1.2 的站点中的用户可用的应用，最好的方法是删除应用程序目录角色。 然后让软件中心直接与管理点通信。 有关详细信息，请参阅[删除应用程序目录](../../../apps/plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat)。

如需解决应用程序目录与软件中心之间的通信故障，请验证以下条件：

- [更新 .NET Framework](enable-tls-1-2-client.md#bkmk_net)，并在各个计算机上启用强加密。

- 执行更改后，重新启动所有受影响的计算机。

<!-- - Configure the browser is configured to support TLS 1. Prior to Windows 10, this option was disabled by default. removing, Silverlight experience is out of support-->

## <a name="service-connection-point-upload-failures"></a>服务连接点上传失败

如果服务连接点没有将数据上传到 SCCMConnectedService，请[更新 .NET Framework](enable-tls-1-2-server.md#bkmk_net)，并在每台计算机上都启用强加密。 更改完成后，请务必重新启动计算机。

## <a name="configuration-manager-console-displays-intune-onboarding-dialog-box"></a>Configuration Manager 控制台显示 Intune 载入对话框

如果控制台尝试连接到 Intune 门户时出现了 Intune 载入对话框，请[更新 .NET Framework](enable-tls-1-2-client.md#bkmk_net)，并在每台计算机上启用强加密。 更改完成后，请务必重新启动计算机。

## <a name="configuration-manager-console-displays-failure-to-sign-in-to-azure"></a>Configuration Manager 控制台显示登录到 Azure 失败

尝试在 Azure Active Directory (Azure AD) 中创建应用程序时，如果在选择“登录”  后 Azure Services 载入对话框立即失败，请[更新 .NET Framework](enable-tls-1-2-server.md#bkmk_net)，并启用强加密。 更改完成后，请务必重新启动计算机。

## <a name="configuration-manager-cloud-services-and-tls-12"></a>Configuration Manager 云服务和 TLS 1.2

云管理网关和云分发点使用的 Azure 虚拟机支持 TLS 1.2。 支持的客户端版本会自动使用 TLS 1.2。

SMSAdminui.log  可能包含如下所示的错误：

``` Log
Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationException
Service returned error. Check InnerException for more details
at Microsoft.ConfigurationManager.CloudBase.AAD.AADAuthenticationContext.GetAADAuthResultObject
...
Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException
Service returned error. Check InnerException for more details
at Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext.RunAsyncTask
...
System.Net.WebException
The underlying connection was closed: An unexpected error occurred on a receive.
at System.Net.HttpWebRequest.GetResponse
```

在系统事件日志中，SChannel EventID 36874 可能记录了下面的描述：`An TLS 1.2 connection request was received from a remote client application, but none of the cipher suites supported by the client application are supported by the server. The TLS connection request has failed.`
<!--SCCMDocs issue #1608-->

## <a name="additional-resources"></a>其他资源

- [.NET Framework 中的传输层安全性 (TLS) 最佳做法](/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)
- [KB 3135244：支持 Microsoft SQL Server 的 TLS 1.2](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server)
- [加密控制技术参考](cryptographic-controls-technical-reference.md)

## <a name="next-steps"></a>后续步骤

- [在客户端上启用 TLS 1.2](enable-tls-1-2-client.md)
- [在站点服务器和远程站点系统上启用 TLS 1.2](enable-tls-1-2-server.md)