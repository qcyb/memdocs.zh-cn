---
title: 将软件更新点配置为结合使用 TLS/SSL 与 PKI 证书教程
titleSuffix: Configuration Manager
description: 教程 - 将 Windows Server Update Services (WSUS) 服务器和软件更新点配置为结合使用 TLS/SSL 与 PKI 证书。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/16/2020
ms.topic: tutorial
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: bd9989b8-ccaf-4d51-8262-b4a99b600d12
ms.openlocfilehash: e8359077ac363d2d732b2ffa6712c9b938a2c709
ms.sourcegitcommit: 6176a7825d6c663faa318a6818b7764bc70f08fc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90718894"
---
# <a name="tutorial-configure-a-software-update-point-to-use-tlsssl-with-a-pki-certificate"></a>教程：将软件更新点配置为结合使用 TLS/SSL 与 PKI 证书

适用范围：Configuration Manager (Current Branch)

将 Windows Server Update Services (WSUS) 服务器及其对应的软件更新点 (SUP) 配置为使用 TLS/SSL 可能会降低潜在攻击者远程入侵客户端的能力并提升特权。 为了确保最佳安全协议就位，我们强烈建议你使用 TLS/SSL 协议来帮助保护软件更新基础结构。 本文将指导你完成将每个 WSUS 服务器和软件更新点配置为使用 HTTPS 所需的步骤。 有关如何保护 WSUS 的详细信息，请参阅 WSUS 文档中的[使用安全套接字层协议保护 WSUS](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) 一文。

在本教程中，将：
> [!div class="checklist"]
> * 获取 PKI 证书（如果需要）
> * 将证书绑定到 WSUS 管理网站
> * 将 WSUS Web 服务配置为需要 SSL
> * 将 WSUS 应用程序配置为使用 SSL
> * 验证 WSUS 控制台连接是否可以使用 SSL
> * 将软件更新点配置为需要与 WSUS 服务器进行 SSL 通信
> * 使用 Configuration Manager 验证功能

## <a name="considerations-and-limitations"></a>注意事项和限制

WSUS 使用 TLS/SSL 向上游 WSUS 服务器验证客户端计算机和下游 WSUS 服务器的身份。 WSUS 还使用 TLS/SSL 来加密更新元数据。 WSUS 不会对更新的内容文件使用 TLS/SSL。 内容文件已签名，并且该文件的哈希包含在更新的元数据中。 在客户端下载并安装文件之前，将同时检查数字签名和哈希。 如果任一检查失败，则不会安装更新。

使用 TLS/SSL 保护 WSUS 部署时，请考虑以下限制：

- 使用 TLS/SSL 会增加服务器工作负载。 对通过网络发送的所有元数据进行加密应该会有一些性能损失。
- 如果将 WSUS 与远程 SQL Server 数据库结合使用，则 WSUS 服务器与数据库服务器之间的连接不受 TLS/SSL 保护。 如果必须保护数据库连接，请考虑以下建议：
   - 将 WSUS 数据库移动到 WSUS 服务器。
   - 将远程数据库服务器和 WSUS 服务器移动到专用网络。
   - 部署 Internet 协议安全性 (IPsec) 以帮助保护网络流量。

将 WSUS 服务器及其软件更新点配置为使用 TLS/SSL 时，可能需要逐步完成大型 Configuration Manager 层次结构的更改。 如果选择逐步完成这些更改，请从层次结构的底部开始，向上移动并以管理中心站点结束。

## <a name="prerequisites"></a>必备知识

本教程介绍了获取用于 Internet Information Services (IIS) 的证书的最常见方法。 无论组织使用哪种方法，都要确保证书满足 Configuration Manager 软件更新点的 [PKI 证书要求](../../core/plan-design/network/pki-certificate-requirements.md)。 与任何证书一样，证书颁发机构必须受与 WSUS 服务器通信的设备信任。

- 安装了软件更新点角色的 WSUS 服务器
- 验证是否已遵循在启用 TLS/SSL 之前禁止回收和配置 WSUS 的内存限制的[最佳做法](/troubleshoot/mem/configmgr/windows-server-update-services-best-practices#disable-recycling-and-configure-memory-limits)。
- 以下两个选项之一：
   - 已存在于 WSUS 服务器的个人证书存储中的相应 PKI 证书。
   - 从企业根证书颁发机构 (CA) 请求和获取 WSUS 服务器的相应 PKI 证书的功能。
      - 默认情况下，包括 Web 服务器证书模板的大多数证书模板只会颁发给域管理员。 如果登录用户不是域管理员，则需要向他们的用户帐户授予对证书模板的“注册”权限。

## <a name="obtain-the-certificate-from-the-ca-if-needed"></a><a name="bkmk_pki"></a> 从 CA 获取证书（如果需要）

如果 WSUS 服务器的个人证书存储中已有相应的证书，请跳过本部分并从[绑定证书](#bkmk_bind)部分开始。 若要将证书请求发送到内部 CA 以安装新证书，请按照本部分中的说明进行操作。
 
1. 从 WSUS 服务器打开管理命令提示符，然后运行 `certlm.msc`。 你的用户帐户必须是本地管理员才能管理本地计算机的证书。

   此时将显示本地设备的“证书管理器”工具。

1. 展开“个人”，然后右键单击“证书”。
1. 依次选择“所有任务”、“请求新证书”。
1. 选择“下一步”以开始证书注册。
1. 选择要注册的证书类型。 证书目的是“服务器身份验证”，要使用的 Microsoft 证书模板是“Web 服务器”或已将“服务器身份验证”指定为“增强型密钥使用”的自定义模板。 系统可能会提示你输入其他信息来注册证书。 通常，你将至少指定以下信息：
   - 公用名：可在“主题”选项卡上找到，将值设置为 WSUS 服务器的 FQDN。
   - 友好名称：可在“常规”选项卡上找到，将值设置为描述性名称以帮助以后标识证书。
:::image type="content" source="media/certificate-properties.png" alt-text="用于指定注册的详细信息的“证书属性”窗口":::
1. 依次选择“注册”、“完成”以完成注册过程。
1. 如果要查看证书的详细信息（如证书的指纹），请将其打开。

> [!TIP]
> 如果 WSUS 服务器面向 Internet，则需要在证书的“使用者”或“使用者可选名称 (SAN)”中使用外部 FQDN。

## <a name="bind-the-certificate-to-the-wsus-administration-site"></a><a name="bkmk_bind"></a> 将证书绑定到 WSUS 管理站点

WSUS 服务器的个人证书存储中一有证书，就将其绑定到 IIS 中的 WSUS 管理站点。

1. 在 WSUS 服务器上，打开 Internet Information Services (IIS) 管理器。
1. 转到“站点” > “WSUS 管理”。
1. 通过操作菜单或右键单击站点来选择“绑定”。
1. 在“站点绑定”窗口中，选择 https 对应的行，然后选择“编辑...”。
   - 不要删除 HTTP 站点绑定。 WSUS 对更新内容文件使用 HTTP。
1. 在“SSL 证书”选项下，选择要绑定到 WSUS 管理站点的证书。 证书的友好名称将显示在下拉菜单中。 如果未指定友好名称，则将显示证书的 `IssuedTo` 字段。 如果你不确定要使用哪个证书，请选择“查看”并验证指纹是否与你获取的证书匹配。  
   :::image type="content" source="media/edit-site-binding.png" alt-text="编辑包含 SSL 证书选择的“站点绑定”窗口":::
1. 完成后选择“确定”，然后选择“关闭”以退出站点绑定。 在后续步骤中保持 Internet Information Services (IIS) 管理器打开。



## <a name="configure-the-wsus-web-services-to-require-ssl"></a><a name="bkmk_webserv"></a> 将 WSUS Web 服务配置为需要 SSL

1. 在 WSUS 服务器上的 IIS 管理器中，转到“站点” > “WSUS 管理”。
1. 展开 WSUS 管理站点，以便查看 WSUS 的 Web 服务和虚拟目录的列表。
1. 对于以下每个 WSUS Web 服务：
   - ApiRemoting30
   - ClientWebService
   - DSSAuthWebService
   - ServerSyncWebService
   - SimpleAuthWebService

   进行以下更改：

      1. 选择“SSL 设置”。
      1. 启用“需要 SSL”选项。
      1. 验证“客户端证书”选项是否设置为“忽略”。
      1. 选择“应用”。

不要在顶层 WSUS 管理站点上设置 SSL 设置，因为某些功能（如内容）需要使用 HTTP。

## <a name="configure-the-wsus-application-to-use-ssl"></a><a name="bkmk_wsusutil"></a> 将 WSUS 应用程序配置为使用 SSL

将 Web 服务设置为需要 SSL 后，需要通知 WSUS 应用程序，以便它可以执行一些其他配置来支持更改。

1. 在 WSUS 服务器上打开管理员命令提示符。 运行此命令的用户帐户必须是 WSUS 管理员组或本地管理员组的成员。
1. 将目录更改为 WSUS 的工具文件夹：  
   `cd "c:\Program Files\Update Services\Tools"`
1. 使用以下命令将 WSUS 配置为使用 SSL：

    `WsusUtil.exe configuressl server.contoso.com`
   
   其中 server.contoso.com 是 WSUS 服务器的 FQDN。
1. WsusUtil 返回 WSUS 服务器的 URL，并在末尾指定端口号。 端口为 8531（默认值）或 443。 验证返回的 URL 是否与预期的 URL 相同。 如果键入错误，则可以再次运行该命令。

   :::image type="content" source="media/wsusutil.png" alt-text="返回 WSUS 的 HTTPS URL 的 wsusutil configuressl 命令":::

> [!TIP] 
> 如果 WSUS 服务器面向 Internet，请在运行 `WsusUtil.exe configuressl` 时指定外部 FQDN。

## <a name="verify-the-wsus-console-can-connect-using-ssl"></a><a name="bkmk_wsus_console"></a> 验证 WSUS 控制台是否可以使用 SSL 进行连接

WSUS 控制台使用 ApiRemoting30 Web 服务进行连接。 Configuration Manager 软件更新点 (SUP) 还使用同一个 Web 服务来指示 WSUS 执行特定操作，例如：

- 启动软件更新同步
- 为 WSUS 设置正确的上游服务器，具体取决于 SUP 的站点在 Configuration Manager 层次结构中的位置
- 添加或删除从层次结构的顶层 WSUS 服务器同步的产品和分类。
- 删除过期的更新

打开 WSUS 控制台，验证是否可以使用与 WSUS 服务器的 ApiRemoting30 Web 服务的 SSL 连接。 稍后我们将测试某些其他 Web 服务。

1. 打开 WSUS 控制台，然后选择“操作” > “连接到服务器”。
1. 为“服务器名称”选项输入 WSUS 服务器的 FQDN。
1. 选择通过 WSUSutil 在 URL 中返回的端口号。
1. 在选择 8531（默认值）或 443 时自动启用“使用安全套接字层(SSL)连接到此服务器”选项。
       :::image type="content" source="media/connect-wsus-console.png" alt-text="通过 HTTPS 端口连接到 WSUS 控制台":::
1. 如果 Configuration Manager 站点服务器远离软件更新点，请从站点服务器启动 WSUS 控制台，并验证 WSUS 控制台是否可以通过 SSL 连接。
   - 如果无法连接远程 WSUS 控制台，则可能表示信任证书、名称解析或被阻止的端口有问题。

## <a name="configure-the-software-update-point-to-require-ssl-communication-to-the-wsus-server"></a><a name="bkmk_cm_sup"></a> 将软件更新点配置为需要与 WSUS 服务器进行 SSL 通信

将 WSUS 设置为使用 TLS/SSL 后，还需要将相应的 Configuration Manager 软件更新点更新为需要 SSL。 进行此更改时，Configuration Manager 将：

- 验证它是否可以为软件更新点配置 WSUS 服务器
- 当提示客户端扫描此 WSUS 服务器时，指示客户端使用 SSL 端口。

若要将软件更新点配置为需要与 WSUS 服务器进行 SSL 通信，请执行以下步骤： 

1. 打开 Configuration Manager 控制台并连接到管理中心站点或主站点服务器，以获取需要编辑的软件更新点。
1. 转到“管理” > “概述” > “站点配置” > “服务器和站点系统角色”。
1. 选择安装了 WSUS 的站点系统服务器，然后选择软件更新点站点系统角色。
1. 在功能区中，选择“属性”。
1. 启用“需要与 WSUS 服务器进行 SSL 通信”选项。

   :::image type="content" source="media/sup-properties.png" alt-text="显示“需要与 WSUS 服务器进行 SSL 通信”选项的 SUP 属性":::
1. 在站点的 [WCM.log](../../core/plan-design/hierarchy/log-files.md#BKMK_SUPLog) 中，应用更改时会看到以下条目：

   ```
   SCF change notification triggered.
   Populating config from SCF
   Setting new configuration state to 1 (WSUS_CONFIG_PENDING)
   ...
   Attempting connection to local WSUS server
   Successfully connected to local WSUS server
   ...
   Setting new configuration state to 2 (WSUS_CONFIG_SUCCESS)
   ```

已编辑日志文件示例，以删除此方案中不需要的信息。  

## <a name="verify-functionality-with-configuration-manager"></a><a name="bkmk_cm_verify"></a> 使用 Configuration Manager 验证功能

### <a name="verify-the-site-server-can-sync-updates"></a>验证站点服务器是否可以同步更新

1. 将 Configuration Manger 控制台连接到顶层站点。
1. 转到“软件库” > “概述” > “软件更新” > “所有软件更新”。
1. 在功能区中，选择“同步软件更新”。
1. 对于询问你是否想要为软件更新启动站点范围的同步的通知，选择“是”。
   - 由于 WSUS 配置已更改，因此将执行完整的软件更新同步，而不是增量同步。
1. 打开站点的 wsyncmgr.log。 如果要监视子站点，则需要等待父站点先完成同步。 通过查看日志中是否有类似于以下内容的条目，验证服务器是否成功同步：

   ```
   Starting Sync
   ...
   Full sync required due to changes in main WSUS server location.
   ...
   Found active SUP SERVER.CONTOSO.COM from SCF File.
   ...
   https://SERVER.CONTOSO.COM:8531
   ...
   Done synchronizing WSUS Server SERVER.CONTOSO.COM
   ...
   sync: Starting SMS database synchronization
   ...
   Done synchronizing SMS with WSUS Server SERVER.CONTOSO.COM
   ```

### <a name="verify-a-client-can-scan-for-updates"></a>验证客户端是否可以扫描更新

将软件更新点更改为需要 SSL 时，Configuration Manager 客户端会在向软件更新点提出位置请求时接收更新的 WSUS URL。 通过测试客户端，可以：
-  确定客户端是否信任 WSUS 服务器的证书。 
- 确定 WSUS 的 SimpleAuthWebService 和 ClientWebService 是否正常运行。
-  确定在扫描期间客户端意外收到 EULA 时，WSUS 内容虚拟目录正常运行

1. 标识针对最近更改为使用 TLS/SSL 的软件更新点扫描的客户端。 如果需要有关标识客户端的帮助，请通过以下 PowerShell 脚本使用[运行脚本](../..//apps/deploy-use/create-deploy-scripts.md)：

   ```powershell
   $Last = (Get-CIMInstance -Namespace "root\CCM\Scanagent" -Class "CCM_SUPLocationList").LastSuccessScanPath
   $Current= Write-Output (Get-CIMInstance -Namespace "root\CCM\Scanagent" -Class "CCM_SUPLocationList").CurrentScanPath
   Write-Host "LastGoodSUP- $last"
   Write-Host "CurrentSUP- $current"
   ```

1. 在测试客户端上运行软件更新扫描周期。 可以使用以下 PowerShell 脚本强制执行扫描：

   ```powershell
   Invoke-WMIMethod -Namespace root\ccm -Class SMS_CLIENT -Name TriggerSchedule "{00000000-0000-0000-0000-000000000113}"
   ```

1. 查看客户端的 ScanAgent.log，验证是否已收到扫描软件更新点的消息。

   ```
   Message received: '<?xml version='1.0' ?>
   <UpdateSourceMessage MessageType='ScanByUpdateSource'>
      <ForceScan>TRUE</ForceScan>
      <UpdateSourceIDs>
            <ID>{A1B2C3D4-1234-1234-A1B2-A1B2C3D41234}</ID>
      </UpdateSourceIDs>
    </UpdateSourceMessage>'
   ```

1. 查看 LocationServices.log，验证客户端是否可以看到正确的 WSUS URL。
**LocationServices.log**
   ```
   WSUSLocationReply : <WSUSLocationReply SchemaVersion="1
   ...
   <LocationRecord WSUSURL="https://SERVER.CONTOSO.COM:8531" ServerName="SERVER.CONTOSO.COM"
   ...
   </WSUSLocationReply>
   ```

1. 查看 WUAHandler.log，验证客户端是否可以成功扫描。

   ```
   Enabling WUA Managed server policy to use server: https://SERVER.CONTOSO.COM:8531
   ...
   Successfully completed scan.
   ```

## <a name="next-steps"></a>后续步骤

[部署软件更新](../deploy-use/deploy-software-updates.md)