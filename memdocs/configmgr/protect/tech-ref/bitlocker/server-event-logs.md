---
title: 服务器事件日志
titleSuffix: Configuration Manager
description: Windows 事件日志中可能的 BitLocker (MBAM) 服务器条目的技术参考
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c3279b7d-654d-444b-bd17-1262894590c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8d49a24b6fea08f12d1fe70c1e0b7415adf98719
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074803"
---
# <a name="server-event-logs"></a>服务器事件日志

适用范围：  Configuration Manager (Current Branch)

<!--3601034-->

在 Configuration Manager 中使用 Windows 事件查看器来查看以下 BitLocker 管理服务器组件的事件日志：

- 管理点上的恢复服务
- 自助服务门户
- Administration and monitoring 网站

在承载其中一个或多个组件的服务器上，打开事件查看器。 然后，依次转到“应用程序和服务日志”、“Microsoft”和“Windows”，再展开“MBAM-Web”     。 默认情况下，存在[管理](#admin)和[操作](#operational)事件日志。

在下面各部分中，有使用 BitLocker 管理服务器组件时可生成的事件 ID 的消息和疑难解答信息。

## <a name="admin"></a>管理

### <a name="1-webappspnerror"></a>1：WebAppSpnError

应用程序: {SiteName}{VirtualDirectory} 缺少以下服务主体名称(SPN):{ListOfSpns} 在帐户 {ExecutionAccount} 上注册所需的 SPN。

要使集成 Windows 身份验证成功，需要部署必要的 SPN。 此消息表示应用程序所需的 SPN 配置错误。 此事件中包含的详情应会提供更多信息。

<!-- See "Service Principal Name (SPN)" in MBAM 2.5 Server Prerequisites for Stand-alone and Configuration Manager Integration Topologies for more information. -->

### <a name="100-adminservicerecoverydberror"></a>100：AdminServiceRecoveryDbError

可能的错误消息：

- GetMachineUsers：在从数据库中获取用户信息时出错。
- GetRecoveryKey：在从数据库中获取恢复密钥时出错。
- GetRecoveryKey：在从数据库中获取用户信息时出错。
- GetRecoveryKeyIds：在从数据库中获取恢复密钥 ID 时出错。
- GetTpmHashForUser：在从恢复数据库中获取 TPM 哈希数据时出错。
- GetTpmHashForUser：在从恢复数据库中获取 TPM 哈希数据时出错。
- QueryDriveRecoveryData：在从数据库中获取驱动器恢复数据时出错。
- QueryRecoveryKeyIdsForUser：在从数据库中获取恢复密钥 ID 时出错。
- QueryVolumeUsers：在从数据库中获取用户信息时出错。

在与恢复数据库通信时，每当出现异常，就会记录此消息。 请通读跟踪中包含的信息，了解有关异常的特定详细信息。

### <a name="101-adminservicecompliancedberror"></a>101：AdminServiceComplianceDbError

可能的错误消息：

- GetRecoveryKey：在将审核事件记录到符合性数据库时出错。
- GetRecoveryKeyIds：在将审核事件记录到符合性数据库时出错。
- GetTpmHashForUser：在将审核事件记录到符合性数据库时出错。
- QueryRecoveryKeyIdsForUser：在将审核事件记录到符合性数据库时出错。
- QueryDriveRecoveryData：在将审核事件记录到符合性数据库时出错。

在与符合性数据库通信时，每当出现异常，就会记录此消息。 请通读跟踪中包含的信息，了解有关异常的特定详细信息。

### <a name="102-agentservicerecoverydberror"></a>102：AgentServiceRecoveryDbError

此消息表示在服务尝试与恢复数据库通信时出现异常。 请通读事件中包含的消息，了解有关异常的特定信息。

请验证 MBAM 应用池帐户是否具有连接恢复数据库所需的权限。

### <a name="103-agentserviceerror"></a>103：AgentServiceError

可能的错误消息：

- 无法检测到客户端计算机帐户或数据迁移用户帐户。

    每次对 `PostKeyRecoveryInfo`、`IsRecoveryKeyResetRequired`、`CommitRecoveryKeyRest` 或 `GetTpmHash` Web 方法进行调用时，它会检索调用方上下文来获取调用方凭据。 如果调用方上下文为 null 或为空，则服务会记录此消息。

- 调用方标识的帐户验证失败。

    如果 Web 方法要求调用方是计算机帐户，但该调用方不是，则会记录此消息。 如果 Web 方法要求调用方是用户帐户，但它不是用户帐户，也不是数据迁移组帐户的成员，则也可能导致此情况。

### <a name="104-statusservicecompliancedbconfigerror"></a>104：StatusServiceComplianceDbConfigError

注册表中的符合性数据库连接字符串为空。

每当符合性 db 连接字符串无效，都会记录此消息。 验证注册表项 `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString` 处的值。

### <a name="105-statusservicecompliancedberror"></a>105：StatusServiceComplianceDbError

此错误表示网站或 Web 服务未能连接到符合性数据库。 验证 IIS 应用池帐户是否可连接到该数据库。

### <a name="106-helpdeskerror"></a>106：HelpdeskError

已知错误和可能的原因：

- 对 URL 的请求导致出现内部错误。

    管理和监视网站（支持人员）的应用程序中出现了未经处理的异常。 请查看“管理”事件日志，查找特定异常  。

- 获取执行上下文信息时出错。 无法验证服务主体名称 (SPN) 的注册情况。

    在初始支持人员网站加载操作期间，它会检查 SPN。 为了验证 SPN，它需要与支持人员网站对应的帐户信息、IIS 网站名称和 ApplicationVirtualPath。 如果其中一个或多个属性无效或缺失，则会记录此错误消息。

- 验证服务主体名称 (SPN) 的注册情况时出错。

    此消息表示在验证 SPN 时引发安全性异常。 请参阅事件详细信息中包含的异常。

### <a name="107-selfserviceportalerror"></a>107：SelfServicePortalError

已知错误和可能的原因：

- 在为用户获取恢复密钥时出错

    表示在发出请求来检索恢复密钥时引发了意外异常。 请参阅事件详细信息中的异常消息。 如果对支持人员应用启用了跟踪，请参阅跟踪数据来取详细的异常消息。

- 获取执行上下文信息时出错。 无法验证服务主体名称 (SPN) 的注册情况

    在初始加载操作期间，自助服务门户会索自助服务网站的帐户信息、IIS 网站名称和 ApplicationVirtualPath，以验证 SPN。 如果其中一个或多个属性无效，则会记录此错误消息。

- 验证服务主体名称 (SPN) 的注册情况时出错。 事件详细信息：{ExceptionMessage}

    此消息表示在验证 SPN 时引发了安全性异常。 请参阅事件详细信息中包含的异常。

### <a name="108-domaincontrollererror"></a>108：DomainControllerError

已知错误和可能的原因：

- 解析域名 {DomainName} 时出错，出现了内存分配失败的问题。

    为解析域名，它会调用 `DsGetDcName` Windows API。 当此 API 返回 `ERROR_NOT_ENOUGH_MEMORY`（指示内存分配失败）时，会记录此消息。

- 无法调用 DsGetDcName 方法

    此消息表示 `DsGetDcName` API 在主机上不可用。

### <a name="109-webapprecoverydberror"></a>109：WebAppRecoveryDbError

已知错误和可能的原因：

- 读取恢复数据库的配置时出错。 未配置恢复数据库的连接字符串。

    此消息表示 `HKLM\Software\Microsoft\MBAM Server\Web\RecoveryDBConnectionString` 上的恢复数据库连接字符串信息无效。 验证给定的注册表项值。

如果看到以下任何消息，请验证来自 IIS 服务器的应用池凭据是否可与恢复数据库建立连接：

- DoesUserHaveMatchingRecoveryKey：在为用户获取恢复密钥 ID 时出错。
- QueryDriveRecoveryData：获取驱动器恢复数据时出错。
- QueryRecoveryKeyIdsForUser：在为用户获取恢复密钥 ID 时出错。
- 在从恢复数据库中获取 TPM 密码哈希时出错。

### <a name="110-webappcompliancedberror"></a>110：WebAppComplianceDbError

已知错误和可能的原因：

- 读取符合性数据库的配置时出错。 未配置符合性数据库的连接字符串。

    此消息表示 `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString` 上的符合性数据库连接字符串信息无效。 验证此注册表项的值。

如果看到以下任何消息，请验证来自 IIS 服务器的应用池凭据是否可与符合性数据库建立连接：

- GetRecoveryKeyForCurrentUser：在将审核事件记录到符合性数据库时出错。
- QueryRecoveryKeyIdsForUser：在将审核事件记录到符合性数据库时出错。
- QueryRecoveryKeyIdsForUser：在将审核事件记录到符合性数据库时出错。

### <a name="111-webappdberror"></a>111：WebAppDbError

这些错误表示下面两种情况之一

- MBAM 网站/Web 服务未能连接到符合性数据库或恢复数据库
- MBAM 网站/Web 服务执行帐户（应用池帐户）无法在符合性数据库或恢复数据库上运行 `GetVersion` 存储过程

事件中包含的消息提供了有关异常的更多详细信息。

请验证应用池帐户是否可连接到符合性数据库或恢复数据库。 确认它具有运行 `GetVersion` 存储过程的权限。

### <a name="112-webapperror"></a>112：WebAppError

验证服务主体名称 (SPN) 的注册情况时出错。

为了验证 SPN，它会查询 Active Directory 来检索 SPN 已映射执行帐户的列表。 它还会查询 `ApplicationHost.config` 以获取网站绑定。 此错误消息表示它无法与 Active Directory 通信，或者无法加载 `ApplicationHost.config` 文件。

验证应用池帐户是否有权查询 Active Directory 或 `ApplicationHost.config` 文件。 另外，还要验证 `ApplicationHost.config` 文件中的站点绑定项。

## <a name="operational"></a>操作

### <a name="4-performancecountererror"></a>4：PerformanceCounterError

检索性能计数器时出错。

跟踪消息包含实际的异常消息，其中一些如下所示：

- ArgumentNullException：如果请求的性能计数器的类别、计数器或实例无效，则会引发此异常。
- System.InvalidOperationException：categoryName 为空字符串 ("")。 counterName 为空字符串 ("")。
- 请求的读/写权限设置对此计数器无效。
- 指定的类别不存在（如果 readOnly 为 true）。
- 指定的类别不是 .NET Framework 自定义类别（如果 readOnly 为 false）。
- 指定的类别被标记为多实例，并且要求使用实例名称创建性能计数器。
- instanceName 的长度超过 127 个字符。
- categoryName 和 counterName 已本地化为不同的语言。
- System.ComponentModel.Win32Exception：访问系统 API 时出错。
- System.UnauthorizedAccessException：在没有管理权限的情况下执行的代码尝试读取性能计数器。

事件中的消息提供了有关异常的更多详细信息。

对于 `System.UnauthorizedAccessException`，请验证应用池帐户是否有权访问性能计数器 API。

### <a name="200-helpdeskinformation"></a>200：HelpDeskInformation

已成功找到管理网站应用程序，并且它已成功连接到受支持的恢复/符合性数据库版本。

表示从支持人员网站成功连接到了恢复数据库或符合性数据库。

### <a name="201-selfserviceportalinformation"></a>201：SelfServicePortalInformation

已成功找到自助服务门户应用程序，并且它已成功连接到受支持的恢复/符合性数据库版本。

表示从自助服务门户成功连接到了恢复数据库或符合性数据库。

### <a name="202-webappinformation"></a>202：WebAppInformation

应用程序已正确注册了其 SPN。

表示已针对执行帐户正确注册了支持人员网站所需的 SPN。

## <a name="see-also"></a>另请参阅

要详细了解如何使用这些日志，请参阅 [BitLocker 事件日志](about-event-logs.md)。

若要详细了解如何排除故障，请参阅[排除 BitLocker 故障](troubleshoot.md)。

要详细了解如何安装这些网站，请参阅[设置 BitLocker 报表和门户](../../deploy-use/bitlocker/setup-websites.md)。
