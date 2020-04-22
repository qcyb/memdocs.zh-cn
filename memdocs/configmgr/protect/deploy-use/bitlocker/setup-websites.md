---
title: 设置 BitLocker 门户
titleSuffix: Configuration Manager
description: 安装用于自助服务门户以及管理和监视网站的 BitLocker 管理组件。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 1cd8ac9f-b7ba-4cf4-8cd2-d548b0d6b1df
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cbd7c516515718cca96bff9b1715233964cb2aa5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699625"
---
# <a name="set-up-bitlocker-portals"></a>设置 BitLocker 门户

适用范围：  Configuration Manager (Current Branch)

<!--3601034-->

必须先安装以下 BitLocker 管理组件，然后才能在 Configuration Manager 中使用它们：

- 用户自助服务门户
- 管理和监视网站（支持门户）

可以在包含 IIS 的现有站点服务器上安装这些门户，也可以使用独立 Web 服务器来托管它们。

> [!NOTE]
> 请仅使用主站点数据库安装自助门户以及管理和监视网站。 在层次结构中，为每个主站点安装这些网站。

开始前，请先确认是否满足这些组件的[先决条件](../../plan-design/bitlocker-management.md#prerequisites)。

## <a name="script-usage"></a>脚本使用情况

此过程使用 PowerShell 脚本 MBAMWebSiteInstaller.ps1 将这些组件安装在 Web 服务器上。 它接受以下参数：

- `-SqlServerName <ServerName>`（必需）：主站点数据库服务器的完全限定的域名。

- `-SqlInstanceName <InstanceName>`：主站点数据库的 SQL Server 实例名称。 如果 SQL 使用默认实例，请勿添加此参数。

- `-SqlDatabaseName <DatabaseName>`（必需）：主站点数据库的名称（例如，`CM_ABC`）。

- `-ReportWebServiceUrl <ReportWebServiceUrl>`：主站点的报告服务点的 Web 服务 URL。 这是“Reporting Services 配置管理器”  中的“Web 服务 URL”  值。

    > [!NOTE]
    > 此参数用于安装关联自管理和监视网站的恢复审核报告  。 默认情况下，Configuration Manager 包括其他 BitLocker 管理报告。

- `-HelpdeskUsersGroupName <DomainUserGroup>`：例如，`contoso\BitLocker help desk users`。 其成员有权访问 Administration and Monitoring 网站的“管理 TPM”和“驱动器恢复”区域的域用户组   。 使用这些选项时，此角色需要填写所有字段，包括用户的域和帐户名。

- `-HelpdeskAdminsGroupName <DomainUserGroup>`：例如，`contoso\BitLocker help desk admins`。 一个域用户组，其成员有权访问管理和监视网站的所有恢复区域。 当帮助用户恢复其驱动器时，此角色仅需要输入恢复密钥。

- `-MbamReportUsersGroupName <DomainUserGroup>`：例如，`contoso\BitLocker report users`。 一个域用户组，其成员拥有管理和监视网站的“报表”区域的只读访问权限  。

    > [!NOTE]
    > 安装程序脚本不会创建你在 -HelpdeskUsersGroupName  、-HelpdeskAdminsGroupName  和 -MbamReportUsersGroupName  参数中指定的域用户组。 运行脚本前，请务必先创建这些组。
    >
    > 如果指定 -HelpdeskUsersGroupName  、-HelpdeskAdminsGroupName  和 -MbamReportUsersGroupName  参数，请务必同时指定域名和组名。 使用格式 `"domain\user_group"`。 请勿排除域名。 如果域名或组名包含空格或特殊字符，请用引号 (`"`) 将参数引起来。

- `-SiteInstall Both`：指定要安装的组件。 有效选项包括：
  - `Both`：安装全部两个组件
  - `HelpDesk`：仅安装 administration and monitoring 网站
  - `SSP`：仅安装自助服务门户

- `-IISWebSite`：脚本将在其中安装 MBAM Web 应用程序的网站。 默认情况下，它使用 IIS 默认网站。 使用此参数前，请创建自定义网站。

- `-InstallDirectory`：脚本将在其中安装 Web 应用程序文件的路径。 默认情况下，此路径为 `C:\inetpub`。 使用此参数前，请创建自定义目录。

- `-Uninstall`：在以前安装了 BitLocker 管理支持/自助服务 Web 门户站点的 Web 服务器上卸载这些站点。


## <a name="run-the-script"></a>运行脚本

在目标 Web 服务器上，执行以下操作：

> [!NOTE]
> 可能需要多次运行脚本，具体视站点设计而定。 例如，在管理点上运行脚本，以安装管理和监视网站。 然后，在独立 Web 服务器上再次运行它，以安装自助服务门户。

1. 将站点服务器上 Configuration Manager 安装文件夹内 `SMSSETUP\BIN\X64` 中的以下文件复制到目标服务器上的本地文件夹：

    - `MBAMWebSite.cab`
    - `MBAMWebSiteInstaller.ps1`

1. 以管理员身份运行 PowerShell，然后运行如下命令行的脚本：

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName <ServerName> -SqlInstanceName <InstanceName> -SqlDatabaseName <DatabaseName> -ReportWebServiceUrl <ReportWebServiceUrl> -HelpdeskUsersGroupName <DomainUserGroup> -HelpdeskAdminsGroupName <DomainUserGroup> -MbamReportUsersGroupName <DomainUserGroup> -SiteInstall Both
    ```

    例如，

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName sql.contoso.com -SqlInstanceName instance1 -SqlDatabaseName CM_ABC -ReportWebServiceUrl https://rsp.contoso.com/ReportServer -HelpdeskUsersGroupName "contoso\BitLocker help desk users" -HelpdeskAdminsGroupName "contoso\BitLocker help desk admins" -MbamReportUsersGroupName "contoso\BitLocker report users" -SiteInstall Both
    ```

    > [!IMPORTANT]
    > 此示例命令行使用所有可能参数来展示它们的用法。 请根据你环境中的要求来调整你的使用。

安装完成后，通过以下 URL 访问门户：

- 自助服务门户：`https://webserver.contoso.com/SelfService`
- 管理和监视网站：`https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> Microsoft 建议但不要求使用 HTTPS。 有关详细信息，请参阅[如何在 IIS 上设置 SSL](https://docs.microsoft.com/iis/manage/configuring-security/how-to-set-up-ssl-on-iis)。

## <a name="verify"></a>验证

使用以下日志进行监视和故障排除：

- Microsoft-Windows-MBAM-Web  下的 Windows 事件日志。 有关详细信息，请参阅[关于 BitLocker 事件日志](../../tech-ref/bitlocker/about-event-logs.md)和[服务器事件日志](../../tech-ref/bitlocker/server-event-logs.md)。

- 每个组件的跟踪日志位于以下默认位置：

  - 自助服务门户：`C:\inetpub\Microsoft BitLocker Management Solution\Logs\Self Service Website`

  - Administration and monitoring 网站：`C:\inetpub\Microsoft BitLocker Management Solution\Logs\Help Desk Website`

若要详细了解如何排除故障，请参阅[排除 BitLocker 故障](../../tech-ref/bitlocker/troubleshoot.md)。

## <a name="next-steps"></a>后续步骤

[自定义自助服务门户](customize-self-service-portal.md)

若要详细了解如何使用已安装的组件，请参阅以下文章：

- [BitLocker administration and monitoring 网站](helpdesk-portal.md)
- [BitLocker 自助服务门户](self-service-portal.md)
