---
title: 修改基础结构
titleSuffix: Configuration Manager
description: 更改 Configuration Manager 基础结构或采取可能对其产生影响的操作。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 92bf86225cf869622fd4b496fd3e8e852b651a70
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694355"
---
# <a name="modify-your-configuration-manager-infrastructure"></a>修改 Configuration Manager 的基础结构

适用范围：  Configuration Manager (Current Branch)

安装一个或多个站点后，你可能需要修改配置，或采取会影响基础结构的操作。

## <a name="manage-the-sms-provider"></a><a name="BKMK_ManageSMSprovider"></a> 管理 SMS 提供程序

SMS 提供程序为一个或多个 Configuration Manager 控制台提供管理联系点。 安装多个 SMS 提供程序时，可以提供联系点冗余以管理站点和层次结构。

在每个 Configuration Manager 站点，均可以重新运行安装程序以执行下列操作：

- 添加 SMS 提供程序的其他实例。 SMS 提供程序的每个其他实例都必须位于单独的计算机上。

- 删除 SMS 提供程序的实例。 若要删除站点的最后一个 SMS 提供程序，你必须卸载该站点。

通过查看在其中运行安装程序的站点服务器的根文件夹中的 **ConfigMgrSetup.log**，可以监视 SMS 提供程序的安装或删除。

在站点上修改 SMS 提供程序前，请参阅[规划 SMS 提供程序](../../plan-design/hierarchy/plan-for-the-sms-provider.md)。

### <a name="manage-the-sms-provider-configuration-for-a-site"></a>管理站点的 SMS 提供程序配置  

1. 通过 Configuration Manager 站点安装文件夹中的 `\BIN\X64\setup.exe` 运行 **Configuration Manager 安装程序**。

1. 在“开始使用”页上，选择“执行站点维护或重置此站点”   。

1. 在“站点维护”页上，选择“修改 SMS 提供程序配置”   。

1. 在“管理 SMS 提供程序”页上，选择以下选项之一  ：

    - **添加新的 SMS 提供程序**：指定计算机的 FQDN，用于托管当前未托管的 SMS 提供程序。

    - **卸载指定的 SMS 提供程序**：选择要从中删除 SMS 提供程序的计算机的名称。

    > [!TIP]  
    > 若要在两台计算机之间移动 SMS 提供程序，请先将其安装到新计算机上。 然后将其从原始位置删除。 无法在计算机之间移动 SMS 提供程序。

安装向导完成后，SMS 提供程序配置即完成。 在站点“属性”的“常规”选项卡上，验证为站点安装了 SMS 提供程序的计算机   。

## <a name="manage-the-configuration-manager-console"></a><a name="bkmk_Console"></a>管理 Configuration Manager 控制台

以下任务可帮助你管理 Configuration Manager 控制台：

- 若要修改 Configuration Manager 控制台中显示的语言，请参阅[管理 Configuration Manager 控制台语言](#BKMK_ManageConsoleLanguages)部分。

- 若要安装其他控制台，请参阅[安装 Configuration Manager 控制台](../deploy/install/install-consoles.md)。

- 若要配置 DCOM 权限以启用站点服务器的远程控制台，请参阅[为远程 Configuration Manager 控制台配置 DCOM 权限](#BKMK_ConfigDCOMforRemoteConsole)部分。

- 若要修改用于限制用户在控制台中可以看到的内容和可以进行的操作的管理权限，请参阅[修改管理用户的管理作用域](../deploy/configure/configure-role-based-administration.md#BKMK_ModAdminUser)。

### <a name="manage-configuration-manager-console-language"></a><a name="BKMK_ManageConsoleLanguages"></a>管理 Configuration Manager 控制台语言

安装站点服务器期间，Configuration Manager 控制台安装文件和站点的支持语言包会复制到站点服务器上的 Configuration Manager 安装路径的 `\Tools\ConsoleSetup` 子文件夹中。

- 在站点服务器上从此文件夹中启动 Configuration Manager 控制台安装时，会将 Configuration Manager 控制台和支持的语言包文件复制到计算机中。

- 如果语言包可用于计算机上的当前语言设置，则会以该语言打开 Configuration Manager 控制台。

- 如果关联的语言包不可用于 Configuration Manager 控制台，则以“英语(美国)”打开控制台。

例如，从支持英语、德语和法语的站点服务器安装 Configuration Manager 控制台。 如果在配置了法语设置的计算机上打开 Configuration Manager 控制台，则将以法文打开控制台。 如果在配置了日语的计算机上打开 Configuration Manager 控制台，则会以英语打开控制台，因为日语语言包不可用。  

每次打开 Configuration Manager 控制台时：

- 确定计算机配置的语言设置
- 验证关联的语言包是否可用于 Configuration Manager 控制台
- 使用适当的语言包打开控制台

如果想要用英语打开 Configuration Manager 控制台而不考虑计算机上配置的语言设置，请删除或重命名该计算机上的语言包文件。

使用以下过程用英文启动 Configuration Manager 控制台而不考虑计算机上配置的区域设置。  

#### <a name="install-an-english-only-version-of-the-configuration-manager-console-on-computers"></a>在计算机上安装纯英语版的 Configuration Manager 控制台  

1. 在 Windows 资源管理器中，浏览到 Configuration Manager 安装路径中的 `\Tools\ConsoleSetup\LanguagePack`。

1. 重命名 **.msp** 和 **.mst** 文件。 例如，你可以将 **&lt;file name\>.MSP** 更改为 **&lt;file name\>.MSP.disabled**。

1. 在计算机上安装 Configuration Manager 控制台。

    > [!IMPORTANT]
    > 当为站点服务器配置新服务器语言时，.msp 和 .mst 文件会再次复制到 **LanguagePack** 文件夹中，并且必须重复此过程以安装纯英文的新 Configuration Manager 控制台。  

#### <a name="temporarily-disable-a-console-language-on-an-existing-configuration-manager-console-installation"></a>对现有 Configuration Manager 控制台安装临时禁用某种控制台语言

1. 在运行 Configuration Manager 控制台的计算机上，关闭 Configuration Manager 控制台。

1. 在 Windows 资源管理器中，浏览到 Configuration Manager 控制台计算机上的 &lt;*ConsoleInstallationPath*>\Bin\。  

1. 针对在计算机上配置的语言重命名相应的语言文件夹。 例如，为德文设置了计算机语言设置，则可以将“de”  文件夹重命名为“de.disabled”  。  

1. 若要以为计算机配置的语言打开 Configuration Manager 控制台，请将此文件夹重命名为原始名称。 例如，将“de.disabled”  重命名为“de”  。  

## <a name="configure-dcom-permissions-for-remote-consoles"></a><a name="BKMK_ConfigDCOMforRemoteConsole"></a> 为远程控制台配置 DCOM 权限

运行 Configuration Manager 控制台的用户帐户需要通过 SMS 提供程序访问站点数据库的权限。 但是，使用远程 Configuration Manager 控制台的管理用户也需要以下位置的**远程激活** DCOM 权限：

- 站点服务器计算机

- 托管 SMS 提供程序的实例的每台计算机

名为 **SMS 管理员**的安全组可授予访问计算机上的 SMS 提供程序的权限，还可用于授予所需的 DCOM 权限。 当 SMS 提供程序在成员服务器上运行时，此组是计算机的本地组。 当 SMS 提供程序在域控制器上运行时，它是域的本地组。

> [!IMPORTANT]
> Configuration Manager 控制台使用 WMI 连接到 SMS 提供程序，而 WMI 在内部使用 DCOM。 如果 Configuration Manager 控制台在 SMS 提供程序计算机以外的计算机上运行，则它需要在 SMS 提供程序计算机上激活 DCOM 服务器的权限。 默认情况下，只会为内置“管理员”组的成员授予“远程激活”。
>
> 如果允许“SMS 管理员”组具有远程激活权限，则此组的成员可能会尝试对 SMS 提供程序计算机进行 DCOM 攻击。 此配置还会增大计算机的受攻击面。 为了减轻此威胁，请仔细监视“SMS 管理员”组的成员身份。

使用下列过程来配置每个管理中心站点 (CAS)、主站点服务器以及每台安装 SMS 提供程序的计算机，以便为管理用户授予远程 Configuration Manager 控制台访问权限。

### <a name="configure-dcom-permissions-for-remote-configuration-manager-console-connections"></a>为远程 Configuration Manager 控制台连接配置 DCOM 权限

1. 作为目标计算机上的管理员，运行 `Dcomcnfg.exe` 以打开“组件服务”  。

1. 依次展开“组件服务”、“计算机”，然后选择“我的电脑”    。 在“操作”菜单中，选择“属性”   。

1. 在“我的电脑属性”窗口中，切换到“COM 安全”选项卡   。在“启动和激活权限”部分中，单击“编辑限制”   。

1. 在“启动和激活权限”窗口中，选择“添加”   。

1. 在“选择用户、计算机、服务帐户或组”窗口中，在“输入要选择的对象名称”字段中键入 `SMS Admins`，然后选择“确定”    。

   > [!TIP]
   > 若要查找“SMS 管理员”组，你可能必须更改以下设置：“查找位置”  。 如果 SMS 提供程序在成员服务器上运行，则此组是计算机的本地组，如果 SMS 提供程序在域控制器上运行，则此组是域的本地组。

1. 在“SMS 管理员的权限”部分，若要允许远程激活，请选择“远程激活”行的“允许”列    。

1. 选择“确定”以保存更改并关闭所有窗口  。

计算机现在已配置为允许“SMS 管理员”组的成员远程访问 Configuration Manager 控制台。

在每台支持远程 Configuration Manager 控制台的 SMS 提供程序计算机上重复此过程。

## <a name="modify-the-site-database-configuration"></a><a name="bkmk_dbconfig"></a>修改站点数据库配置

安装站点后，可以修改站点数据库和站点数据库服务器的配置。 在 CAS 服务器或主站点服务器上运行 Configuration Manager 安装程序以进行更改。 你可以将站点数据库转移到同一计算机上的新 SQL Server 实例，或转移到运行支持的 SQL Server 版本的其他计算机。 辅助站点的数据库配置不支持这些更改。

有关支持的限制的详细信息，请参阅 [Configuration Manager 环境中手动数据库更改的支持策略](https://support.microsoft.com/kb/3106512)。  

> [!NOTE]
> 当修改站点的数据库配置时，Configuration Manager 将在站点服务器和与数据库通信的远程站点系统服务器上重启或重新安装 Configuration Manager 服务。

### <a name="modify-the-database-configuration"></a>修改数据库配置

在站点服务器上运行 Configuration Manager 安装程序，并选择“执行站点维护或重置此站点”选项  。 然后，选择“修改 SQL Server 配置”选项  。 你可以更改下列站点数据库配置：

- 承载数据库的基于 Windows 的服务器。

- 承载 SQL Server 数据库的服务器上使用的 SQL Server 实例。

- 数据库名称。

- Configuration Manager 正在使用的 SQL Server 端口。

- Configuration Manager 正在使用的 SQL Server Service Broker 端口。

### <a name="move-the-site-database"></a>移动站点数据库

如果移动站点数据库，还请查看以下配置：

- 如果将站点数据库移动到新计算机，请将站点服务器的计算机帐户添加到运行 SQL Server 的计算机上的本地**管理员**组。 如果为站点数据库使用 SQL Server 群集，请将计算机帐户添加到每台 Windows Server 群集节点计算机的本地**管理员**组。

- 如果将数据库移动到 SQL Server 上的新实例或新的 SQL Server 计算机，请启用公共语言运行时 (CLR) 集成。 使用 **SQL Server Management Studio** 连接到托管站点数据库的 SQL Server 实例。 然后，以查询形式运行以下存储过程：`sp_configure 'clr enabled',1; reconfigure`

- 确保新的 SQL Server 可以访问备份位置。 数据库移动到新服务器后，如果使用 UNC 存储站点数据库备份，请确保新 SQL Server 的计算机帐户具有对 UNC 位置的**写入**权限。 此配置包括移动到 SQL Server AlwaysOn 可用性组或 SQL Server 群集的情况。

> [!IMPORTANT]
> 在移动具有一个或多个管理点数据库副本的数据库前，请先删除数据库副本。 完成数据库转移后，你可以重新配置数据库副本。 有关详细信息，请参阅[管理点的数据库副本](../deploy/configure/database-replicas-for-management-points.md)。

## <a name="manage-the-spn-for-the-site-database-server"></a><a name="bkmk_SPN"></a>管理站点数据库服务器的 SPN

你可为站点数据库选择运行 SQL 服务的帐户：

- 使用计算机系统帐户运行服务时，它会自动为你注册服务主体名称 (SPN)。

- 使用域本地用户帐户运行服务时，请手动注册 SPN。 SPN 允许 SQL 客户端和其他站点系统通过 Kerberos 进行身份验证。 若未进行 Kerberos 身份验证，与数据库的通信可能失败。

有关 SPN 和 Kerberos 连接的详细信息，请参阅[为 Kerberos 连接注册服务主体名称](https://docs.microsoft.com/sql/database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections)。

通过使用 **Setspn** 工具为站点数据库服务器的 SQL Server 服务帐户注册 SPN。 在与 SQL Server 处于同一域中的计算机上，以域管理员身份运行 Setspn。

以下过程是如何为 SQL Server 服务帐户管理 SPN 的示例。 有关 Setspn 的详细信息，请参阅 [Setspn 概述](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc731241\(v=ws.11\))。

### <a name="manually-create-a-domain-user-spn-for-the-sql-server-service-account"></a>手动为 SQL Server 服务帐户创建域用户 SPN

1. 以管理员身份打开命令提示符。

1. 输入有效命令用于为 NetBIOS 名称和 FQDN 创建 SPN：

    > [!IMPORTANT]
    > 在为群集 SQL Server 创建 SPN 时，请指定 SQL Server 群集的虚拟名称作为 SQL Server 计算机名。

    - NetBIOS 名称：`setspn -A MSSQLSvc/<SQL Server computer name>:<port> <Domain\Account>`

        例如：`setspn -A MSSQLSvc/sqlserver:1433 contoso\sqlservice`

    - FQDN：`setspn -A MSSQLSvc/<SQL Server FQDN>:<port> <Domain\Account>`

        例如：`setspn -A MSSQLSvc/sqlserver.contoso.com:1433 contoso\sqlservice`

    > [!NOTE]
    > 用于为 SQL Server 命名实例注册 SPN 的命令与为默认实例注册 SPN 时使用的命令相同。 唯一的例外是端口号必须与命名实例使用的端口匹配。

### <a name="verify-the-domain-user-spn-is-registered-correctly"></a>验证域用户 SPN 是否已正确注册

1. 以管理员身份打开命令提示符。

1. 输入以下命令：`setspn -L <domain\SQL service account>`

    例如：`setspn -L contoso\sqlservice`

1. 查看已注册的 **ServicePrincipalName**。 确保为 SQL Server 创建了有效的 SPN。

### <a name="change-the-sql-server-service-account-from-local-system-to-a-domain-user-account"></a>将 SQL Server 服务帐户从本地系统更改为域用户帐户

1. 创建或选择要用作 SQL Server 服务帐户的域或本地系统用户帐户。

1. 打开“SQL Server 配置管理器”  。

1. 选择“SQL Server 服务”，然后打开“SQL Server&lt;INSTANCE NAME\>”   。

1. 切换到“登录”选项卡  。选择“此帐户”，然后输入步骤 1 中的域用户帐户的用户名和密码  。

1. 确认服务帐户更改，然后重启 SQL Server 服务。

## <a name="run-a-site-reset"></a><a name="bkmk_reset"></a>运行站点重置

在 CAS 或主站点中运行站点重置时，站点会：

- 重新应用默认 Configuration Manager 文件和注册表权限

- 重新安装所有站点组件和所有站点系统角色

辅助站点不支持站点重置。

可以手动重置站点。 修改站点配置后，它们也可以自动运行。 例如：

- 如果对 Configuration Manager 组件使用的帐户进行了更改，请考虑手动进行站点重置。 此操作可确保站点组件更新为使用新帐户详细信息。

- 如果修改站点上的客户端或服务器语言，则 Configuration Manager 会自动运行站点重置。 站点需要进行重置才能使用新语言。

> [!NOTE]
> 站点重置不会重置对非 Configuration Manager 对象的访问权限。

### <a name="what-happens-during-a-site-reset"></a>站点重置期间发生的情况

运行站点重置时：

1. 安装程序会停止并重启“SMS_SITE_COMPONENT_MANAGER”  服务和“SMS_EXECUTIVE”  服务的线程组件。

1. 安装程序会删除本地计算机和远程站点系统计算机上的站点系统共享文件夹和 **SMS Executive** 组件，然后再重新创建。

1. 安装程序会重启 **SMS_SITE_COMPONENT_MANAGER** 服务，此服务会安装 **SMS_EXECUTIVE** 和 **SMS_SQL_MONITOR** 服务。

站点重置会还原下列对象：

- “SMS”  或“NAL”  注册表项，以及这些项下的任何默认子项。

- Configuration Manager 文件目录树，以及此文件目录树中的任何默认文件或子目录。

### <a name="prerequisites-for-site-reset"></a>站点重置的先决条件

用于重置站点的帐户必须具有以下权限：

- 重置 CAS：

  - CAS 服务器上的本地**管理员**

  - 等同于基于**完全权限管理员**角色的管理安全角色的权限

- 重置主站点：

  - 主站点服务器上的本地**管理员**

  - 等同于基于**完全权限管理员**角色的管理安全角色的权限
  
  - 如果主站点位于具有 CAS 的层次结构中，则此帐户还必须是 CAS 服务器上的本地**管理员**。

### <a name="limitations-for-a-site-reset"></a>站点重置的限制

如果将层次结构配置为支持[在预生产集合中测试客户端升级](../../clients/manage/upgrade/test-client-upgrades.md)，则不能使用站点重置来更改站点上的服务器或客户端语言包。

### <a name="run-a-site-reset"></a>运行站点重置

1. 使用以下方法之一在站点服务器上启动 Configuration Manager 安装程序：

    - 在“开始”菜单上，选择“Configuration Manager 安装程序”   。

    - 在 Configuration Manager 安装介质  的目录中，打开 `\SMSSETUP\BIN\X64\setup.exe`。 确保此版本与站点版本相同。

    - 在*安装* Configuration Manager 的目录中，打开 `\BIN\X64\setup.exe`。

1. 在“开始使用”页上，选择“执行站点维护或重置此站点”   。

1. 在“站点维护”页上，选择“重置站点而不更改配置”   。

1. 选择“是”以开始站点重置  。

## <a name="manage-language-packs-at-a-site"></a><a name="bkmk_sitelang"></a>管理站点上的语言包

安装站点后，你可以更改正在使用的服务器和客户端语言包。

### <a name="server-language-packs"></a>服务器语言包

适用范围：*Configuration Manager 控制台安装，适用站点系统角色的新安装*

更新站点中的服务器语言包之后，可以将语言包支持添加到 Configuration Manager 控制台。

若要向 Configuration Manager 控制台添加服务器语言包支持，请从站点服务器的 **ConsoleSetup** 文件夹（其中包括想使用的语言包）安装 Configuration Manager 控制台。 如果已安装 Configuration Manager 控制台，则必须先卸载它，以使新安装能够识别当前支持的语言包的列表。

### <a name="client-language-packs"></a>客户端语言包

更改客户端语言包会更新客户端安装源文件。 新的客户端安装和升级增加对客户端语言更新列表的支持。

更新站点中的客户端语言包后，请使用包含客户端语言包的源文件来安装将使用这些语言包的每个客户端。

有关 Configuration Manager 支持的客户端和服务器语言的详细信息，请参阅[语言包](../deploy/install/language-packs.md)。

### <a name="modify-the-supported-language-packs-at-a-site"></a>修改站点支持的语言包

1. 使用以下方法之一在站点服务器上启动 Configuration Manager 安装程序：

    - 在“开始”菜单上，选择“Configuration Manager 安装程序”   。

    - 在 Configuration Manager 安装介质  的目录中，打开 `\SMSSETUP\BIN\X64\setup.exe`。 确保此版本与站点版本相同。

    - 在*安装* Configuration Manager 的目录中，打开 `\BIN\X64\setup.exe`。

1. 在“开始使用”页上，选择“执行站点维护或重置此站点”   。

1. 在“站点维护”页上，选择“修改语言配置”   。

1. 在“先决条件下载”页上，选择以下选项之一  ：

    - **下载所需文件**：获取语言包的更新。

    - **使用之前下载的文件**：使用之前下载的文件，其中包括要添加到站点的语言包。

1. 在“服务器语言选择”页上，选择此站点支持的服务器语言  。

1. 在“客户端语言选择”页上，选择此站点支持的客户端语言  。

1. 完成向导以修改站点的语言支持。

    > [!NOTE]
    > Configuration Manager 会启动站点重置（也会在该站点重新安装所有站点系统角色）。

## <a name="modify-the-database-server-alert-threshold"></a><a name="BKMK_ModDBAlert"></a>修改数据库服务器警报阈值

默认情况下，当站点数据库服务器上的可用磁盘空间不足时，Configuration Manager 会生成警报：

- 在可用磁盘空间不足 10 GB 时生成警告
- 在可用磁盘空间不足 5 GB 时生成关键警报

可以为每个站点修改这些值或禁用警报：

1. 在 Configuration Manager 控制台中，转到“管理”  工作区，展开“站点配置”  ，然后选择“站点”  节点。

1. 选择要配置的站点。 在功能区中，选择“属性”  。

1. 切换到“警报”选项卡，然后编辑设置  。

## <a name="uninstall-sites-and-hierarchies"></a>卸载站点和层次结构

可能需要卸载 Configuration Manager 站点系统角色、站点或层次结构。 有关详细信息，请参阅[卸载角色、站点和层次结构](../deploy/install/uninstall-sites-and-hierarchies.md)。

从版本 2002 开始，还可以从层次结构中删除 CAS，但保留主站点。 有关详细信息，请参阅[删除 CAS](../deploy/install/remove-central-administration-site.md)。
