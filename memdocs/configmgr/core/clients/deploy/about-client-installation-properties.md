---
title: 客户端安装参数和属性
titleSuffix: Configuration Manager
description: 了解用于安装 Configuration Manager 客户端的 ccmsetup 命令行参数和属性。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fda1e877f8e0bc211b36e288af13de204305cc5a
ms.sourcegitcommit: 0b30c8eb2f5ec2d60661a5e6055fdca8705b4e36
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2020
ms.locfileid: "84455032"
---
# <a name="about-client-installation-parameters-and-properties-in-configuration-manager"></a>关于 Configuration Manager 中的客户端安装参数和属性

适用范围：Configuration Manager (Current Branch)

使用 CCMSetup.exe 命令安装 Configuration Manager 客户端。 如果在命令行上提供客户端安装参数，这些参数会修改安装行为。 如果在命令行上提供客户端安装属性，这些属性会修改已安装客户端代理的初始配置。

## <a name="about-ccmsetupexe"></a><a name="aboutCCMSetup"></a> 关于 CCMSetup.exe

CCMSetup.exe 命令从管理点或源位置下载所需的文件以安装客户端。 这些文件可能包括：  

- 安装客户端软件的 Windows Installer 包 client.msi

- 客户端先决条件

- Configuration Manager 客户端的更新和修补程序

> [!NOTE]
> 不能直接安装 client.msi。  

CCMSetup.exe 提供了可自定义安装的命令行参数。 参数以斜杠 (`/`) 作为前缀，按照约定为小写。 在必要时，使用一个冒号 (`:`) 紧跟值来指定参数的值。 有关详细信息，请参阅 [CCMSetup.exe 命令行参数](#ccmsetupexe-command-line-parameters)。

还可在 CCMSetup.exe 命令行中指定属性来修改 client.msi 的行为。按照约定属性均采用大写。 使用等于号 (`=`) 紧跟值来指定参数的值。 有关详细信息，请参阅 [Client.msi 属性](#clientMsiProps)。

> [!IMPORTANT]  
> 指定 client.msi 的属性之前，先指定 CCMSetup 参数。  

CCMSetup.exe 及支持文件位于 Configuration Manager 安装文件夹内“Client”文件夹中的站点服务器上。 Configuration Manager 会将此文件夹共享到网络的站点共享下。 例如，`\\SiteServer\SMS_ABC\Client`。

在命令提示符处，CCMSetup.exe 命令使用下列格式：  

`CCMSetup.exe [<Ccmsetup parameters>] [<client.msi setup properties>]`  

例如：  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

此示例将执行以下操作：  

- 指定名为 SMSMP01 的管理点以请求用于下载客户端安装文件的分发点列表。  

- 指定在计算机已有客户端的某个版本时停止安装。  

- 指示 client.msi 将客户端分配到站点代码 S01。  

- 指示 client.msi 使用名为 SMSFP01 的回退状态点。  

> [!TIP]  
> 如果属性值包含空格，则用引号括起来。  

如果为 Configuration Manager 扩展了 Active Directory 架构，站点会在 Active Directory 域服务中发布许多客户端安装属性。 Configuration Manager 客户端会自动读取这些属性。 有关详细信息，请参阅 [关于发布到 Active Directory 域服务的客户端安装属性](about-client-installation-properties-published-to-active-directory-domain-services.md)  

## <a name="ccmsetupexe-command-line-parameters"></a>CCMSetup.exe 命令行参数

### <a name=""></a><a name="bkmk_help"></a> /?

显示 ccmsetup.exe 的可用命令行参数。  

示例：`ccmsetup.exe /?`

### <a name="source"></a>/source

指定文件下载位置。 使用本地路径或 UNC 路径。 设备使用服务器消息块 (SMB) 协议下载文件。 若要使用“/source”，用于客户端安装的 Windows 用户帐户需要具有对该位置的“读取”权限 。

若要详细了解 ccmsetup 如何下载内容，请参阅[边界组 - 客户端安装](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup)。 如果你同时使用 /mp 和 /source 参数，还可以参阅这篇文章中包含的 ccmsetup 行为详细信息。

> [!TIP]  
> 可在命令行上多次使用 /source 参数，以指定备用下载位置。  

示例：`ccmsetup.exe /source:"\\server\share"`

### <a name="mp"></a>/mp

指定计算机要连接到的源管理点。 计算机使用此管理点来查找最近的安装文件分发点。 如果没有分发点或者计算机在 4 个小时后无法从分发点下载文件，则将从指定的管理点下载文件。  

若要详细了解 ccmsetup 如何下载内容，请参阅[边界组 - 客户端安装](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup)。 如果你同时使用 /mp 和 /source 参数，还可以参阅这篇文章中包含的 ccmsetup 行为详细信息。

> [!IMPORTANT]  
> 此参数指定初始管理点，以供计算机查找下载源，此管理点可以是任何站点中的任何管理点。 它不会将客户端分配到指定的管理点。

计算机通过 HTTP 或 HTTPS 连接下载文件，具体情况视客户端连接的站点系统角色配置而定。 如果要进行配置，也可通过使用 BITS 限制进行下载。 如果所有分发点和管理点都仅针对 HTTPS 客户端连接进行配置，则需验证客户端计算机是否具有有效的客户端证书。  

可使用 /mp 命令行参数来指定多个管理点。 如果计算机无法连接到第一个管理点，则会尝试连接指定列表中的下一个管理点。 在指定多个管理点时，请使用分号分隔各个值。

如果客户端使用 HTTPS 连接到管理点，请指定 FQDN 而不是计算机名。 值必须匹配管理点的 PKI 证书“使用者”或“使用者可选名称” 。 尽管 Configuration Manager 对于 Intranet 上的连接支持使用证书中的计算机名，但建议使用 FQDN。

计算机名的示例：`ccmsetup.exe /mp:SMSMP01`  

FQDN 的示例：`ccmsetup.exe /mp:smsmp01.contoso.com`  

还可使用该参数指定云管理网关 (CMG) 的 URL。 使用此 URL 在基于 Internet 的设备上安装客户端。 要获取此参数的值，请按以下步骤操作：

- 创建 CMG。 有关详细信息，请参阅[设置 CMG](../manage/cmg/setup-cloud-management-gateway.md)。
- 在活动的客户端上，以管理员身份打开 Windows PowerShell 命令提示符。
- 运行以下命令：

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP
    ```

- 附加 `https://` 前缀以与 /mp 参数一起使用。

使用云管理网关 URL 时的示例：`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> 为 /mp 参数指定云管理网关的 URL 时，它必须以 `https://` 开头。

### <a name="regtoken"></a>/regtoken

<!--5686290-->

从版本 2002 开始，使用此参数提供批量注册令牌。 基于 Internet 的设备通过云管理网关 (CMG) 在注册过程中使用此令牌。 有关详细信息，请参阅[基于令牌的 CMG 身份验证](deploy-clients-cmg-token.md)。

使用此参数时，还应包括以下参数和属性：

- [ **/mp**](#mp)
- [**CCMHOSTNAME**](#ccmhostname)
- [**SMSSiteCode**](#smssitecode)
- [**SMSMP**](#smsmp)

下面的示例命令行包含其他必需的设置参数和属性：

`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

### <a name="retry"></a>/retry

如果 CCMSetup.exe 无法下载安装文件，请使用此参数指定重试间隔（以分钟为单位）。 除非达到 [/downloadtimeout](#downloadtimeout) 参数中指定的限制，否则 CCMSetup 将不断重试。

示例：`ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

此参数阻止 CCMSetup 作为服务运行的默认行为。 当 CCMSetup 作为服务运行时，它在计算机的本地系统帐户的上下文中运行。 此帐户可能没有足够权限访问安装所需的网络资源。 借助 **/noservice**，CCMSetup.exe 将在你用于启动安装过程的用户帐户的上下文中运行。

示例：`ccmsetup.exe /noservice`  

### <a name="service"></a>/service

指定 CCMSetup 应作为使用本地系统帐户的服务运行。  

> [!TIP]
> 如果使用脚本来运行带 /service 参数的 CCMSetup.exe，CCMSetup.exe 将在服务启动后退出。 它可能无法正确报告脚本的安装详细信息。

示例：`ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

使用此参数卸载 Configuration Manager 客户端。 有关详细信息，请参阅[卸载客户端](../manage/manage-clients.md#BKMK_UninstalClient)。

示例：`ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

如果已安装客户端的任何版本，该参数会指定应停止客户端安装。  

示例：`ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

如果需要完成安装，请使用此参数强制计算机重启。 如果未指定此参数，则 CCMSetup 会在需要重启时退出。 然后在下一次手动重启后继续。

示例：`CCMSetup.exe /forcereboot`

### <a name="bitspriority"></a>/BITSPriority

当设备通过 HTTP 连接下载客户端安装文件时，请使用此参数指定下载优先级。 指定以下可能的值之一：

- `FOREGROUND`

- `HIGH`

- `NORMAL`（默认值）

- `LOW`

示例：`ccmsetup.exe /BITSPriority:HIGH`

### <a name="downloadtimeout"></a>/downloadtimeout

如果 CCMSetup 未能下载客户端安装文件，则此参数指定最大超时时间（以分钟为单位）。 此超时时间之后，CCMSetup 将停止尝试下载安装文件。 默认值为 1440 分钟（一天）。

使用 [/retry](#retry) 参数指定重试尝试之间的间隔。

示例：`ccmsetup.exe /downloadtimeout:100`

### <a name="usepkicert"></a>/UsePKICert

为客户端指定此参数以使用 PKI 客户端身份验证证书。 如果不包含此参数，或客户端找不到有效证书，则它会使用带自签名证书的 HTTP 连接。

示例：`CCMSetup.exe /UsePKICert`  

> [!NOTE]
> 在某些情况下，不必指定此参数，但仍可使用客户端证书。 例如，基于客户端推送和软件更新的客户端安装。 手动安装客户端时使用此参数，并对已启用 HTTPS 的管理点使用 /mp 参数。
>
> 安装客户端进行仅限 Internet 的通信时，也请指定此参数。 将 CCMALWAYSINF=1 属性与基于 Internet 的管理点 (CCMHOSTNAME) 和站点代码 (SMSSITECODE) 的属性一起使用  。 若要详细了解基于 Internet 的客户端管理，请参阅[来自 Internet 或不受信任林的客户端通信的注意事项](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)。  

### <a name="nocrlcheck"></a>/NoCRLCheck

指定客户端在使用 PKI 证书通过 HTTPS 进行通信时应不检查证书吊销列表 (CRL)。 如果未指定此参数，客户端会在建立 HTTPS 连接之前检查 CRL。 有关客户端 CRL 检查的详细信息，请参阅 [PKI 证书吊销的规划](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs)。

示例：`CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="config"></a>/config

此参数指定列出客户端安装属性的文本文件。

- 如果 CCMSetup 作为服务运行，请将此文件放入 CCMSetup 系统文件夹：`%Windir%\Ccmsetup`。

- 如果指定 [/noservice](#noservice) 参数，请将此文件与 CCMSetup.exe 放在同一文件夹中。

示例：`CCMSetup.exe /config:"configuration file name.txt"`

若要提供正确的文件格式，请使用站点服务器上 Configuration Manager 安装目录中 `\bin\<platform>` 文件夹中的“mobileclienttemplate.tcf”文件。 此文件也包含有关各个部分及其使用方式的注释。 指定 `[Client Install]` 部分中的客户端安装属性，其后紧跟下列文本 `Install=INSTALL=ALL`。

示例 `[Client Install]` 部分条目：`Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereq"></a>/skipprereq

此参数指定 CCMSetup.exe 不安装指定的先决条件。 你可以输入多个值。 使用分号字符 (`;`) 来分隔各个值。

例如：

- `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe`

- `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;windowsupdateagent30_x86.exe`

有关客户端先决条件的详细信息，请参阅 [Windows 客户端先决条件](prerequisites-for-deploying-clients-to-windows-computers.md)。

### <a name="forceinstall"></a>/forceinstall

指定 CCMSetup.exe 卸载任何现有客户端，并安装新客户端。  

### <a name="excludefeatures"></a>/ExcludeFeatures

此参数指定 CCMSetup.exe 不安装指定的功能。

示例：`CCMSetup.exe /ExcludeFeatures:ClientUI` 不在客户端上安装软件中心。  

> [!NOTE]  
> `ClientUI` 是 /ExcludeFeatures 参数唯一支持的值。

## <a name="ccmsetupexe-return-codes"></a><a name="ccmsetupReturnCodes"></a> CCMSetup.exe 返回代码

CCMSetup.exe 命令提供以下返回代码。 若要进行故障排除，请查看客户端上的 `%WinDir%\ccmsetup\ccmsetup.log`，以获取返回代码的上下文以及其他详细信息。

|返回代码|含义|  
|-----------|-------|  
|0|成功|  
|6|错误|  
|7|需要重新启动|  
|8|安装程序已在运行|  
|9|先决条件评估失败|  
|10|安装程序清单哈希验证失败|  

## <a name="ccmsetupmsi-properties"></a><a name="ccmsetupMsiProps"></a> Ccmsetup.msi 属性

下面的属性可修改 ccmsetup.msi 的安装行为。

### <a name="ccmsetupcmd"></a>CCMSETUPCMD

使用此 ccmsetup.msi 属性将其他命令行参数和属性传递给 ccmsetup.exe 。 将其他参数和属性括在引号 (`"`) 内。 使用 [Intune MDM 安装方法](plan/client-installation-methods.md#microsoft-intune-mdm-installation)启动 Configuration Manager 客户端时可使用此属性。

示例：`ccmsetup.msi CCMSETUPCMD="/mp:https://mp.contoso.com CCMHOSTNAME=mp.contoso.com"`

> [!Tip]
> Microsoft Intune 将该命令行限制为 1024 个字符。

## <a name="clientmsi-properties"></a><a name="clientMsiProps"></a> Client.msi 属性

以下属性可以修改 ccmsetup.exe 安装的 client.msi 的安装行为。 如果使用[客户端请求安装方法](plan/client-installation-methods.md#client-push-installation)，请在 Configuration Manager 控制台中“客户端请求安装属性”的“客户端”选项卡上指定这些属性 。

### <a name="aadclientappid"></a>AADCLIENTAPPID

指定 Azure Active Directory (Azure AD) 客户端应用标识符。 在为云管理[配置 Azure 服务](../../servers/deploy/configure/azure-services-wizard.md)时，需创建或导入客户端应用。 Azure 管理员可从 Azure 门户获取该属性的值。 有关详细信息，请参阅[获取应用程序 ID](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)。 对于 AADCLIENTAPPID 属性，此应用程序 ID 用于“本机”类型应用程序 。

示例：`ccmsetup.exe AADCLIENTAPPID=aa28e7f1-b88a-43cd-a2e3-f88b257c863b`

### <a name="aadresourceuri"></a>AADRESOURCEURI

指定 Azure AD 服务器应用标识符。 在为云管理[配置 Azure 服务](../../servers/deploy/configure/azure-services-wizard.md)时，需创建或导入服务器应用。 创建服务器应用时，在“创建服务器应用程序”窗口中，该属性为 App ID URI。

Azure 管理员可从 Azure 门户获取该属性的值。 在“Azure Active Directory”中，找到“应用注册”下的服务器应用 。 查找应用程序类型“Web 应用/API”。 打开应用，选择“设置”，然后选择“属性” 。 使用此 AADRESOURCEURI 客户端安装属性的 App ID URI 值 。

示例：`ccmsetup.exe AADRESOURCEURI=https://contososerver`

### <a name="aadtenantid"></a>AADTENANTID

指定 Azure AD 租户标识符。 为云管理[配置 Azure 服务](../../servers/deploy/configure/azure-services-wizard.md)时，Configuration Manager 会链接到此租户。 要获取此属性的值，请按以下步骤操作：

- 在加入同一 Azure AD 租户的 Windows 10 设备上，打开命令提示符。
- 运行以下命令：`dsregcmd.exe /status`
- 在“设备状态”部分中，找到 TenantId 值。 例如 `TenantId : 607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

  > [!Note]
  > Azure 管理员还可在 Azure 门户中获取此值。 有关详细信息，请参阅[获取租户 ID](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)。

示例：`ccmsetup.exe AADTENANTID=607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

<!-- 
### AADTENANTNAME

Specifies the Azure AD tenant name. This tenant is linked to Configuration Manager when you [configure Azure services](../../servers/deploy/configure/azure-services-wizard.md) for Cloud Management. To obtain the value for this property, use the following steps:
- On a Windows 10 device that is joined to the same Azure AD tenant, open a command prompt.
- Run the following command: `dsregcmd.exe /status`
- In the Device State section, find the **TenantName** value. For example, `TenantName : Contoso`

Example: `ccmsetup.exe AADTENANTNAME=Contoso`
-->

### <a name="ccmadmins"></a>CCMADMINS  

指定可访问客户端设置和策略的一个或多个 Windows 用户帐户或组。 如果客户端计算机上没有本地管理凭据，此属性会非常有用。 指定由分号 (`;`) 分隔的帐户列表。

示例：`CCMSetup.exe CCMADMINS="domain\account1;domain\group1"`

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

如有必要，允许计算机在客户端安装后无提示重启。

> [!IMPORTANT]  
> 使用此属性时，计算机将在没有警告的情况下重启。 即使用户已登录到 Windows，也会发生此行为。

示例：`CCMSetup.exe CCMALLOWSILENTREBOOT`

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

若要指定客户端始终以 Internet 为基础并永远不会连接到 Intranet，请将此属性值设置为 `1`。 客户端的连接类型显示为“始终连接 Internet” 。  

将此属性与 [CCMHOSTNAME](#ccmhostname) 结合使用可指定基于 Internet 的管理点的 FQDN。 还可以将其与 CCMSetup 参数 [/UsePKICert](#usepkicert) 和站点代码 ([SMSSITECODE](#smssitecode)) 结合使用 。

若要详细了解基于 Internet 的客户端管理，请参阅[来自 Internet 或不受信任林的客户端通信的注意事项](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)。

示例：`CCMSetup.exe /UsePKICert CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

使用此属性指定证书颁发者列表。 此列表包括 Configuration Manager 站点信任的受信任根证书颁发机构 (CA) 的证书信息。  

此值是根 CA 证书中主题属性的匹配（区分大小写）。 用逗号 (`,`) 或分号 (`;`) 分隔属性。 使用分隔线 (`|`) 指定多个根 CA 证书。

示例：`CCMCERTISSUERS="CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US | CN=Litware Corporate Root CA; O=Litware, Inc."`

> [!TIP]
> 在站点的 mobileclient.tcf 文件中使用 CertificateIssuers 属性的值 。 此文件位于站点服务器的 Configuration Manager 安装目录的 `\bin\<platform>` 子文件夹中。

若要详细了解证书颁发者列表以及客户端如何在证书选择过程中使用该列表，请参阅[规划 PKI 客户端证书选择](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection)。

### <a name="ccmcertsel"></a>CCMCERTSEL

如果客户端有多个用于 HTTPS 通信的证书，则此属性指定其选择有效客户端身份验证证书的条件。

使用以下关键字搜索证书使用者名称或使用者可选名称：

- **主题**：查找完全匹配项
- **SubjectStr**：查找部分匹配项

例如：

- `CCMCERTSEL="Subject:computer1.contoso.com"`：搜索在“使用者名称”或“使用者可选名称”中与计算机名称“`computer1.contoso.com`”完全匹配的证书。

- `CCMCERTSEL="SubjectStr:contoso.com"`：搜索在“使用者名称”或“使用者可选名称”中包含“`contoso.com`”的证书。

使用 SubjectAttr 关键字在“使用者名称”或“使用者可选名称”中搜索对象标识符 (OID) 或可分辨名称属性。

例如：

- `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"`：搜索以对象标识符表示且名为 `Computers` 的组织单位属性。

- `CCMCERTSEL="SubjectAttr:OU = Computers"`：搜索以可分辨名称表示且名为 `Computers` 的组织单位属性。

> [!IMPORTANT]
> 如果使用“使用者名称”，则 Subject 关键字区分大小写，而 SubjectStr 关键字不区分大小写 。
>
> 如果使用“使用者可选名称”框，Subject 和 SubjectStr 关键字均不区分大小写 。

有关可用于证书选择的完整属性列表，请参阅[对于 PKI 证书选择条件支持的属性值](#BKMK_attributevalues)。

如果有多个证书与搜索匹配，并且将 [CCMFIRSTCERT](#ccmfirstcert) 设置为 `1`，则客户端安装程序将选择有效期最长的证书。

### <a name="ccmcertstore"></a>CCMCERTSTORE

如果客户端安装程序在计算机的默认“个人”证书存储中找不到有效证书，请使用此属性指定备用证书存储名称。

示例：`CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

此属性在客户端安装时启用调试日志记录。 此属性将使客户端记录有助于故障排除的低级信息。 避免在生产站点中使用此属性。 因为这会产生过多日志记录，可能导致难以在日志文件中查找相关信息。 同时启用 [CCMENABLELOGGING](#ccmenablelogging)。

支持的值：

- `0`：关闭调试日志记录（默认）
- `1`：启用调试日志记录

示例：`CCMSetup.exe CCMDEBUGLOGGING=1`  

有关详细信息，请参阅[关于日志文件](../../plan-design/hierarchy/about-log-files.md)。

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

默认情况下，Configuration Manager 会启用日志记录。

支持的值：

- `TRUE`：启用日志记录（默认值）
- `FALSE`：关闭日志记录

示例：`CCMSetup.exe CCMENABLELOGGING=TRUE`  

有关详细信息，请参阅[关于日志文件](../../plan-design/hierarchy/about-log-files.md)。

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL

客户端运行状况评估工具 (ccmeval.exe) 运行时的频率（以分钟为单位）。 指定介于 `1` 到 `1440` 之间的整数值。 默认情况下，ccmeval 每天（1440 分钟）运行一次。

示例：`CCMSetup.exe CCMEVALINTERVAL=1440`

有关客户端运行状况评估的详细信息，请参阅[监视客户端](../manage/monitor-clients.md#bkmk_health)。

### <a name="ccmevalhour"></a>CCMEVALHOUR

客户端运行状况评估工具 (ccmeval.exe) 运行时的时间。 指定介于 `0`（午夜）到 `23`（晚上 11:00）之间的整数值。 默认情况下，ccmeval 在午夜运行。

有关客户端运行状况评估的详细信息，请参阅[监视客户端](../manage/monitor-clients.md#bkmk_health)。

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

如果将此属性设置为 `1`，则客户端将选择有效期最长的 PKI 证书。

示例：`CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`

### <a name="ccmhostname"></a>CCMHOSTNAME

如果客户端是通过 Internet 进行管理，则此属性指定基于 Internet 的管理点的 FQDN。  

请勿使用 SMSSITECODE=AUTO 的安装属性指定此选项.。 可直接将基于 Internet 的客户端分配给基于 Internet 的站点。

示例：`CCMSetup.exe /UsePKICert CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

该属性可指定云管理网关 (CMG) 的地址。 要获取此属性的值，请按以下步骤操作：

- 创建 CMG。 有关详细信息，请参阅[设置 CMG](../manage/cmg/setup-cloud-management-gateway.md)。
- 在活动的客户端上，以管理员身份打开 Windows PowerShell 命令提示符。
- 运行以下命令：

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
    ```

- 将返回值按原样与 CCMHOSTNAME 属性一起使用。

例如：`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> 为 CCMHOSTNAME 属性指定 CMG 的地址时，请勿附加诸如 `https://` 之类的前缀。 仅将此前缀与 CMG 的 /mp URL 一起使用。

### <a name="ccmhttpport"></a>CCMHTTPPORT

指定客户端通过 HTTP 与站点系统服务器通信时使用的端口。 默认情况下，此值为 `80`。

示例：`CCMSetup.exe CCMHTTPPORT=80`

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

指定客户端通过 HTTPS 与站点系统服务器通信时使用的端口。 默认情况下，此值为 `443`。

示例：`CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`

### <a name="ccminstalldir"></a>CCMINSTALLDIR

使用此属性设置用于安装 Configuration Manager 客户端文件的文件夹。 默认情况下，它使用 `%WinDir%\CCM`。

> [!TIP]
> 无论在何处安装客户端文件，它始终都会在 `%WinDir%\System32` 文件夹中安装 ccmcore.dll 文件。 在 64 位操作系统上，它会在 `%WinDir%\SysWOW64` 文件夹中安装 ccmcore.dll 的副本。 此文件支持使用来自 Configuration Manager SDK 的 32 位版本的客户端 API 的 32 位应用程序。

示例：`CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`

### <a name="ccmloglevel"></a>CCMLOGLEVEL

使用此属性指定要写入 Configuration Manager 日志文件的详细级别。

支持的值：

- `0`：详细
- `1`：默认
- `2`：警告和错误
- `3`：仅错误

示例：`CCMSetup.exe CCMLOGLEVEL=0`

有关详细信息，请参阅[关于日志文件](../../plan-design/hierarchy/about-log-files.md)。

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Configuration Manager 日志文件的大小达到上限时，客户端会将其重命名为备份，并创建新的日志文件。 此属性指定保留先前版本的日志文件个数。 默认值为 `1`。 如果将该值设置为 `0`，则客户端不会保留任何日志文件历史记录。

示例：`CCMSetup.exe CCMLOGMAXHISTORY=5`

有关详细信息，请参阅[关于日志文件](../../plan-design/hierarchy/about-log-files.md)。

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

此属性用于指定日志文件的大小（以字节为单位）。 当日志增长到指定大小时，客户端会将其重命名为历史文件，并创建一个新的日志文件。 默认大小为 250000 个字节，最小大小为 10000 个字节。

例如：`CCMSetup.exe CCMLOGMAXSIZE=300000`（300000 个字节）

### <a name="disablesiteopt"></a>DISABLESITEOPT

将此属性设置为 `TRUE` 以阻止管理员在 Configuration Manager 控制面板中更改分配的站点。

例如：**CCMSetup.exe DISABLESITEOPT=TRUE**

### <a name="disablecacheopt"></a>DISABLECACHEOPT

如果设置为 TRUE，则此属性会禁止管理用户更改 Configuration Manager 控制面板中的客户端缓存文件夹设置。  

示例：`CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

为客户端指定 DNS 域以查找在 DNS 中发布的管理点。 当客户端找到管理点时，它会告知客户端有关层次结构中的其他管理点。 此行为意味着客户端从 DNS 中找到的管理点可以是层次结构中的任何一个管理点。

> [!NOTE]
> 如果客户端与发布的管理点位于同一域中，则不必指定此属性。 在此情况下，客户端会自动使用其域来搜索 DNS 以查找管理点。

有关 DNS 发布作为 Configuration Manager 客户端的服务定位方法的详细信息，请参阅[服务定位和客户端如何确定向其分配的管理点](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location)。

> [!NOTE]  
> 默认情况下，Configuration Manager 不启用 DNS 发布。

示例：`CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`

### <a name="fsp"></a>FSP

指定接收和处理 Configuration Manager 客户端发送的状况消息的回退状态点。

有关详细信息，请参阅[确定是否需要回退状态点](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point)。

示例：`CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

如果将此属性设置为 `TRUE`，则客户端安装程序不会检查最低所需版本的 Microsoft Application Virtualization (App-V)。

> [!IMPORTANT]  
> 如果在未安装 App-V 的情况下安装 Configuration Manager 客户端，则无法[部署虚拟应用程序](../../../apps/get-started/deploying-app-v-virtual-applications.md)。

示例：`CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`

### <a name="notifyonly"></a>NOTIFYONLY

如果启用此属性，则客户端会报告状态，但不修复发现的问题。

示例：`CCMSetup.exe NOTIFYONLY=TRUE`

有关详细信息，请参阅[如何配置客户端状态](configure-client-status.md)。

### <a name="provisionts"></a>预配

<!--5526972-->

从版本 2002 开始，在客户端成功注册到站点后，使用此属性可在客户端上启动任务序列。

例如，使用 Windows Autopilot 预配新的 Windows 10 设备，将其自动注册到 Microsoft Intune，然后安装 Configuration Manager 客户端以进行共同管理。 如果指定此新选项，则新预配的客户端将运行一个任务序列。 通过此过程，可以更灵活地安装应用程序和软件更新，或配置设置。

请按以下过程操作：

1. [创建非 OS 部署任务序列](../../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)以安装应用、安装软件更新和配置设置。

1. 向新的内置集合“所有预配设备”[部署此任务序列](../../../osd/deploy-use/deploy-a-task-sequence.md)。 请注意任务序列部署 ID，例如 `PRI20001`。

1. 在设备上[安装 Configuration Manager 客户端](deploy-clients-to-windows-computers.md#BKMK_Manual)，并包括以下属性：`PROVISIONTS=PRI20001`。 将此属性的值设置为任务序列部署 ID。

    - 如果在共同管理注册过程中从 Intune 安装客户端，请参阅[如何准备基于 Internet 的设备以实现共同管理](../../../comanage/how-to-prepare-Win10.md)。

      > [!NOTE]
      > 此方法可能具有其他先决条件。 例如将站点注册到 Azure Active Directory，或创建启用内容的云管理网关。

安装客户端并正确注册到站点后，它启动引用的任务序列。 如果客户端注册失败，则任务序列不会启动。

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

如果客户端具有错误的 Configuration Manager 受信任的根密钥，则无法与受信任的管理点联系，因此无法接收受信任的新根密钥。 请使用此属性手动删除旧的受信任的根密钥。 此情况可能在将客户端从一个站点层次结构移至另一个站点层次结构时发生。 此属性适用于使用 HTTP 和 HTTPS 客户端通信的客户端。 有关详细信息，请参阅[规划受信任的根密钥](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。

示例：`CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

与 [SMSSITECODE](#smssitecode)=AUTO 一起使用时，请启用自动站点重新分配进行客户端升级。

示例：`CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

指定客户端计算机上客户端缓存文件夹的位置。 默认情况下，缓存位置是 `%WinDir%\ccmcache`。

示例：`CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

将此属性与 [SMSCACHEFLAGS](#smscacheflags) 属性结合使用可控制客户端缓存文件夹位置。 示例：将客户端缓存文件夹安装在最大的可用客户端磁盘驱动器上：`CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE`

### <a name="smscacheflags"></a>SMSCACHEFLAGS

请使用此属性指定客户端缓存文件夹的进一步安装详细信息。 可以单独或组合使用 SMSCACHEFLAGS 属性，组合使用时须以分号 (`;`) 隔开。

如果不包含此属性：

- 客户端根据 [SMSCACHEDIR](#smscachedir) 属性安装缓存文件夹
- 文件夹未压缩
- 客户端使用 [SMSCACHESIZE](#smscachesize) 属性作为缓存的大小限制（以 MB 为单位）

升级现有客户端时，客户端安装程序将忽略此属性。

#### <a name="values-for-the-smscacheflags-property"></a>SMSCACHEFLAGS 属性的值

- **PERCENTDISKSPACE**：将缓存大小设置为总磁盘空间的百分比。 如果指定此属性，请将 [SMSCACHESIZE](#smscachesize) 设置为百分比值。

- **PERCENTFREEDISKSPACE**：将缓存大小设置为可用磁盘空间的百分比。 如果指定此属性，请将 [SMSCACHESIZE](#smscachesize) 设置为百分比值。 例如，该磁盘的可用空间为 10 MB ，你可以指定 `SMSCACHESIZE=50`。 客户端安装程序将缓存大小设置为 5 MB。 你不能将此属性与 PERCENTDISKSPACE 属性结合使用。

- **MAXDRIVE**：将缓存安装在最大的可用磁盘上。 如果使用 [SMSCACHEDIR](#smscachedir) 属性指定路径，则客户端安装程序将忽略此值。

- **MAXDRIVESPACE**：将缓存安装在具有最大可用空间的磁盘驱动器上。 如果使用 [SMSCACHEDIR](#smscachedir) 属性指定路径，则客户端安装程序将忽略此值。

- **NTFSONLY**：仅在 NTFS 格式化的磁盘驱动器上安装缓存。 如果使用 [SMSCACHEDIR](#smscachedir) 属性指定路径，则客户端安装程序将忽略此值。

- **COMPRESS**：以压缩形式存储缓存。

- **FAILIFNOSPACE**：如果没有足够的空间安装缓存，请删除 Configuration Manager 客户端。

示例：`CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`

### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> 客户端设置可用于指定客户端缓存文件夹的大小。 添加这些客户端设置有效地替代了使用 SMSCACHESIZE 作为 client.msi 属性指定客户端缓存的大小。 有关详细信息，请参阅[有关缓存大小的客户端设置](about-client-settings.md#client-cache-settings)。  

升级现有客户端时，客户端安装程序将忽略此设置。 客户端在下载软件更新时也会忽略缓存大小。

示例：`CCMSetup.exe SMSCACHESIZE=100`

> [!NOTE]  
> 如果重新安装客户端，则无法使用 SMSCACHESIZE 或 SMSCACHEFLAGS 将缓存大小设置为小于以前的值 。 先前的大小是最小值。

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

使用此属性指定客户端安装程序检查配置设置的位置和顺序。 它是一个含一个或多个字符的字符串，其中每个字符都定义了一个特定的配置源：

- `R`：检查注册表中的配置设置。

  有关详细信息，请参阅[预配客户端安装属性](deploy-clients-to-windows-computers.md#BKMK_Provision)。

- `P`：检查在命令行上提供的安装属性中的配置设置。

- `M`：升级旧客户端时检查现有设置。

- `U`：将安装的客户端升级为较新版本，并使用分配的站点代码。

默认情况下，客户端安装程序使用 `PU`。 它首先检查安装属性 (`P`)，然后检查现有设置 (`U`)。  

示例：`CCMSetup.exe SMSCONFIGSOURCE=RP`

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

指定客户端是否能使用 Windows Internet 名称服务 (WINS) 来查找接受 HTTP 连接的管理点。 如果客户端无法在 Active Directory 域服务或 DNS 中查找管理点，则会使用此方法。

此属性对客户端是否将 WINS 用于名称解析没有影响。

可以为此属性配置两种不同的模式：

- **NOWINS**：此值是该属性最安全的设置。 它会阻止客户端查找 WINS 中的管理点。 如果使用此设置，客户端必须有备用方法来查找 Intranet 上的管理点。 例如，Active Directory 域服务或 DNS 发布。

- **WINSSECURE**（默认值）：在此模式中，使用 HTTP 通信的客户端可使用 WINS 来查找管理点。 但是，该客户端必须具有受信任的根密钥的副本，然后才能成功地连接到管理点。 有关详细信息，请参阅[规划受信任的根密钥](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。

示例：`CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### <a name="smsmp"></a>SMSMP

指定供 Configuration Manager 客户端使用的初始管理点。  

> [!IMPORTANT]  
> 如果管理点仅接受通过 HTTPS 进行的客户端连接，请为管理点名称加上前缀 `https://`。

例如：

- `CCMSetup.exe SMSMP=smsmp01.contoso.com`

- `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  

### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

如果客户端无法从 Active Directory 域服务获取 Configuration Manager 受信任的根密钥，请使用此属性指定密钥。 此属性适用于使用 HTTP 和 HTTPS 通信的客户端。 有关详细信息，请参阅[规划受信任的根密钥](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。

示例：`CCMSetup.exe SMSPUBLICROOTKEY=<keyvalue>`

> [!TIP]
> 从站点服务器上的 mobileclient.tcf 文件中获取站点受信任的根密钥的值。 有关详细信息，请参阅[使用文件预先设置客户端和受信任的根密钥](../../plan-design/security/plan-for-security.md#bkmk_trk-provision-file)。

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

使用此属性重新安装 Configuration Manager 受信任的根密钥。 它指定包含受信任的根密钥的文件的完整路径和名称。 此属性适用于使用 HTTP 和 HTTPS 客户端通信的客户端。 有关详细信息，请参阅[规划受信任的根密钥](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。

示例：`CCMSetup.exe SMSROOTKEYPATH=C:\folder\trk`

### <a name="smssigncert"></a>SMSSIGNCERT

在站点服务器上指定导出的自签名证书的完整路径和名称。 站点服务器将此证书存储在 SMS 证书存储中。 它具有使用者名称“站点服务器”和易记名称“站点服务器签名证书” 。

示例：`CCMSetup.exe /UsePKICert SMSSIGNCERT=C:\folder\smssign.cer`

### <a name="smssitecode"></a>SMSSITECODE

此属性指定将客户端分配到的 Configuration Manager 站点。 此值可以是三个字符的站点代码，也可以是单词 `AUTO`。 如果指定了 `AUTO` 或者未指定此属性，则客户端会尝试从 Active Directory 域服务或指定的管理点确定其站点分配。 若要启用 `AUTO` 进行客户端升级，还必须设置 [SITEREASSIGN=TRUE](#sitereassign)。

> [!NOTE]  
> 如果还使用 [CCMHOSTNAME](#ccmhostname) 属性指定基于 Internet 的管理点，请勿将 `AUTO` 与 SMSSITECODE 结合使用 。 通过指定站点代码直接将客户端分配到其站点。

示例：`CCMSetup.exe SMSSITECODE=XZY`

## <a name="attribute-values-for-certificate-selection-criteria"></a><a name="BKMK_attributevalues"></a> 证书选择条件的属性值

对于 PKI 证书选择条件，Configuration Manager 支持 下列属性值：

|OID 属性|可分辨名称属性|属性定义|
|-------------|----------------------------|--------------------|
|0.9.2342.19200300.100.1.25|DC|域组件|  
|1.2.840.113549.1.9.1|E 或 E-mail|电子邮件地址|  
|2.5.4.3|CN|公用名|  
|2.5.4.4|SN|使用者名称|  
|2.5.4.5|SERIALNUMBER|序列号|  
|2.5.4.6|C|国家/地区代码|  
|2.5.4.7|L|区域|  
|2.5.4.8|S 或 ST|省或自治区名称|  
|2.5.4.9|STREET|街道地址|  
|2.5.4.10|O|组织名称|  
|2.5.4.11|OU|组织单位|  
|2.5.4.12|T 或 Title|标题|  
|2.5.4.42|G 或 GN 或 GivenName|给定名称|  
|2.5.4.43|I 或 Initials|缩写|  
|2.5.29.17|（没有值）|使用者可选名称|  
