---
title: 创建自定义配置项目
titleSuffix: Configuration Manager
description: 使用 Windows 台式机和服务器的自定义配置项目管理 Windows 计算机和服务器的设置
ms.date: 04/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 63f11066918854d72af0f1160d7d7569a93d7ebe
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692515"
---
# <a name="create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>为使用 Configuration Manager 客户端管理的 Windows 台式机和服务器计算机创建自定义配置项目

适用范围：  Configuration Manager (Current Branch)


使用 Configuration Manager 自定义 Windows 台式机和服务器  配置项目，为 Configuration Manager 客户端管理的 Windows 计算机和服务器管理设置。  



## <a name="start-the-wizard"></a>启动向导

1. 在 Configuration Manager 控制台中，转到“资产和符合性”  工作区，展开“符合性设置”  ，再选择“配置项目”  节点。  

2. 在功能区的“主页”  选项卡上，选择“创建”  组中的“创建配置项目”  。  

3. 在“创建配置项目向导”  的“常规”  页面上，指定配置项目的名称和可选描述。  

4. 在“指定要创建的配置项目的类型”  下，选择“Windows 台式机和服务器(自定义)”  。  

    > [!TIP]  
    > 如果要提供检查应用程序是否存在的检测方法设置，请选择“此配置文件包含应用程序设置”  。  

5. 选择“类别”  以创建和分配类别，这样有助于在 Configuration Manager 控制台中搜索和筛选配置项目。  



## <a name="detection-methods"></a>检测方法  

使用此过程可为配置项目提供检测方法信息。  

> [!NOTE]  
> 只有在向导的“常规”  页上选中“此配置项目包含应用程序设置”  后，此信息才适用。  

Configuration Manager 中的检测方法包含用于检测应用程序是否在计算机上安装的规则。 此检测发生之前，客户端会针对配置项目评估其符合性。 若要检测是否安装了应用程序，则可以检测到该应用程序的 Windows Installer 文件是否存在，请使用自定义脚本，或者选择 **始终假设安装应用程序** 来评估法规遵从性而不考虑是否安装了该应用程序的配置项目。  


### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>使用 Windows Installer 文件检测应用程序安装的具体步骤  

1. 在“创建配置项目向导”  的“检测方法”  页上，选择“使用 Windows Installer 检测”  选项。  

2. 单击“打开”  ，转到要检测的 Windows Installer (.msi) 文件，再选择“打开”  。  

3. “版本”字段自动填充 Windows Installer 文件的版本号  。 如果显示的值不正确，请在此处输入新版本号。  

4. 若要检测计算机上的所有用户配置文件，请选中“此应用程序是针对一个或多个用户进行安装”  。  


### <a name="to-detect-a-specific-application-and-deployment-type"></a>若要检测特定应用程序和部署类型  

1. 在“创建配置项目向导”  的“检测方法”  页上，选择“检测特定应用程序和部署类型”  。 选择“选择”  。   

2. 在“指定应用程序”  对话框中，选择要检测的应用程序和关联部署类型。  


### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>若要使用自定义脚本检测应用程序安装  

1. 在“创建配置项目向导”  的“检测方法”  页上，选择“使用自定义脚本来检测此应用程序”  选项。  

2. 在列表中，选择脚本语言。 从下面的格式中进行选择：  

    - **VBScript**  

    - **JScript**  

    - **PowerShell**  

        > [!Note]  
        > 从版本 1810 开始，当 Windows PowerShell 脚本作为检测方法运行时，Configuration Manager 客户端会使用 `-NoProfile` 参数调用 PowerShell。 此选项在没有配置文件的情况下启动 PowerShell。 PowerShell 配置文件是在 PowerShell 启动时运行的脚本。 <!--3607762-->  

3. 选择“打开”  ，转到要使用的脚本，再选择“打开”  。  



## <a name="specify-supported-platforms"></a>指定支持的平台  

在“创建配置项目向导”  的“支持的平台”  页上，选择要为其评估配置项目符合性的 Windows 版本，或单击“全选”  。

也可以手动指定 Windows 的版本  。 选择“添加”并指定 Windows 内部版本号的每个部分  。

> [!NOTE]
> 指定 Windows Server 2016 时，对 `All Windows Server 2016 and higher 64-bit)`的选择还包括 Windows Server 2019。 若要仅指定 Windows Server 2016，请使用“手动指定 Windows 版本选项”  。 <!--5866480-->



##  <a name="configure-settings"></a>配置设置  

使用此过程可在配置项目中配置设置。  

设置表示业务或技术用于评估客户端设备上的符合性的条件。 你可以配置新设置，或浏览到引用计算机上的现有设置。  

1. 在“创建配置项目向导”  的“设置”  页上，选择“新建”  。  

2. 在上 **常规** 选项卡上 **创建设置** 对话框框中，提供以下信息：  

    - **名称**：输入设置的唯一名称。 最多可以使用 256 个字符。  

    - **描述**：输入设置的描述。 最多可以使用 256 个字符。  

    - **设置类型**：在列表中，选择和配置要用于此设置的以下设置类型之一：  
        - [Active Directory 查询](#bkmk_adquery)
        - [程序集](#bkmk_assembly)
        - [文件系统](#bkmk_file)
        - [IIS 元数据库](#bkmk_iis)
        - [注册表项](#bkmk_regkey)
        - [注册表值](#bkmk_regval)
        - [脚本](#bkmk_script)
        - [SQL 查询](#bkmk_sql)
        - [WQL 查询](#bkmk_wql)
        - [XPath 查询](#bkmk_xpath)

    - **数据类型**：选择条件在用于评估设置之前返回数据的格式。 不是所有设置类型都有对应的“数据类型”  列表显示。  

        > [!Tip]  
        > “浮点”  数据类型仅支持小数点后 3 个数字。  

3. 配置此设置下的更多详情 **设置类型** 列表。 可配置的项目因已选择的设置类型而异。  

4. 单击“确定”  以保存设置，并关闭“创建设置”  对话框。  


### <a name="active-directory-query"></a><a name="bkmk_adquery"></a> Active Directory 查询

- **LDAP 前缀**：指定 Active Directory 域服务查询的有效前缀，以在客户端计算机上评估符合性。 若要执行全局编录搜索，请使用 `LDAP://` 或 `GC://`。  

- **可分辨名称 (DN)** ：指定在客户端计算机上评估其符合性的 Active Directory 域服务对象的可分辨名称。  

- **搜索筛选器**：指定可选的 LDAP 筛选器以缩小 Active Directory 域服务查询的结果范围，从而在客户端计算机上评估符合性。 要从查询返回所有结果，请输入 `(objectclass=*)`。  

- **搜索范围**：指定在 Active Directory 域服务中的搜索范围  

    - **基础**：仅查询指定对象  

    - **一级**：这一版 Configuration Manager 不使用此选项  

    - **子树**：查询指定对象及其在目录中的完整子树  

- **属性**：指定用于在客户端计算机上评估符合性的 Active Directory 域服务对象的属性。  

    例如，若要查询用于存储用户错误输入密码次数的 Active Directory 属性，请在此字段中输入 `badPwdCount`。  

- **查询**：显示根据“LDAP 前缀”  、“可分辨名称 (DN)”  、“搜索筛选器”  （若已指定）和“属性”  中的条目构造而成的查询。  


### <a name="assembly"></a><a name="bkmk_assembly"></a> 程序集

程序集是可在应用程序之间共享的一段代码。 程序集可以具有 .dll 或 .exe 文件扩展名。 全局程序集缓存是客户端计算机上的文件夹 `%SystemRoot%\Assembly`。 此缓存是 Windows 存储所有共享程序集的位置。  

- **程序集名称：** 指定要搜索的程序集对象的名称。 名称不能与相同类型的其他程序集对象相同。 首先在全局程序集缓存中注册它。 程序集名称最多可以含有 256 个字符。  


### <a name="file-system"></a><a name="bkmk_file"></a> 文件系统

- **类型**：在列表中，选择要搜索“文件”  还是“文件夹”  。  

- **路径**：指定客户端计算机上的指定文件或文件夹的路径。 你可以在路径中指定系统环境变量和 `%USERPROFILE%` 环境变量。  

    > [!NOTE]  
    > 如果在“路径”或“文件或文件夹名称”框中使用 `%USERPROFILE%` 环境变量，则 Configuration Manager 客户端将搜索客户端计算机上的所有用户配置文件   。 此行为可能导致它查找文件或文件夹的多个实例。  
    >   
    > 如果符合性设置无权访问指定路径，便会生成发现错误。 此外，如果您要搜索的文件当前正在使用，则生成发现错误。  

    > [!Tip]  
    > 选择“浏览”以配置基准计算机上的值设置  。   

- **文件或文件夹名称**：指定要搜索的文件或文件夹对象的名称。 你可以在文件或文件夹名称中指定系统环境变量和 `%USERPROFILE%` 环境变量。 还可以在文件名中使用通配符 `*` 和 `?`。  

    > [!NOTE]  
    > 如果指定文件名或文件夹名称并使用通配符，这样的组合可能会生成许多结果。 这还可能会导致客户端计算机上的资源使用率高，并导致在向 Configuration Manager 报告结果时网络流量高。  

- **包括子文件夹**：还可以搜索指定路径下面的所有子文件夹。  

- **此文件或文件夹与 64 位应用程序相关联**：如果启用，则仅搜索 64 位计算机上的 64 位文件位置，如 `%ProgramFiles%`。 如果未启用此选项，则会同时搜索 64 位位置和 32 位位置，如 `%ProgramFiles(x86)%`。  

    > [!NOTE]  
    > 如果在同一 64 位计算机上的 64 位和 32 位系统文件位置中存在相同的文件或文件夹，则全局条件会发现多个文件。  

    “文件系统”  设置类型不支持在“路径”  框中指定网络共享的 UNC 路径。  


### <a name="iis-metabase"></a><a name="bkmk_iis"></a> IIS 元数据库

- **元数据库路径**：指定 Internet Information Services (IIS) 元数据库的有效路径。 例如，`/LM/W3SVC/`。  

- **属性 ID**：指定 IIS 元数据库设置的数值属性。  


### <a name="registry-key"></a><a name="bkmk_regkey"></a> 注册表项

- **配置单元**：选择要搜索的注册表配置单元

    > [!Tip]  
    > 选择“浏览”以配置基准计算机上的值设置  。 若要浏览到远程计算机上的注册表项，请在远程计算机上启用“远程注册表”服务  。  

- **密钥**：指定要搜索的注册表项名称。 使用格式 `key\subkey`。  

- **此注册表项与 64 位应用程序相关联**：在正在运行 64 位版本 Windows 的客户端上，除了搜索 32 位注册表项外，还搜索 64 位注册表项。  

    > [!NOTE]  
    > 如果在同一 64 位计算机上的 64 位和 32 位注册表位置中存在相同的注册表项，则全局条件会发现两个注册表项。  


### <a name="registry-value"></a><a name="bkmk_regval"></a> 注册表值

- **配置单元**：选择要搜索的注册表配置单元。  

    > [!Tip]  
    > 选择“浏览”以配置基准计算机上的值设置  。 若要浏览到远程计算机上的注册表项值，请在远程计算机上启用“远程注册表”服务  。 还需具有管理员权限才能访问远程计算机。  

- **密钥**：指定要搜索的注册表项名称。 使用格式 `key\subkey`。  

- **值**：指定必须包含在指定注册表项中的值。  

- **此注册表项与 64 位应用程序相关联**：在正在运行 64 位版本 Windows 的客户端上，除了搜索 32 位注册表项外，还搜索 64 位注册表项。  

    > [!NOTE]  
    > 如果在同一 64 位计算机上的 64 位和 32 位注册表位置中存在相同的注册表项，则全局条件会发现两个注册表项。  


### <a name="script"></a><a name="bkmk_script"></a> 脚本

脚本返回的值用于评估全局条件的符合性。 例如，使用 VBScript 时，可以使用命令“WScript.Echo Result”  将 *Result* 变量值返回给全局条件。  

- **发现脚本**：选择“添加脚本”，然后输入或浏览到脚本  。 此脚本用于查找值。 您可以使用 Windows PowerShell、 VBScript、 或 Microsoft JScript 脚本。  

- **修正脚本(可选)** ：选择“添加脚本”，然后输入或浏览到脚本  。 此脚本用于修正不符合的设置值。 您可以使用 Windows PowerShell、 VBScript、 或 Microsoft JScript 脚本。  

- **使用登录用户凭据运行脚本**：如果你启用此选项，脚本会在使用登录用户凭据的客户端计算机上运行。  

> [!Note]  
> 从版本 1810 开始，当将 Windows PowerShell 脚本作为发现或修正脚本时，Configuration Manager 客户端会使用 `-NoProfile` 参数调用 PowerShell。 此选项在没有配置文件的情况下启动 PowerShell。 PowerShell 配置文件是在 PowerShell 启动时运行的脚本。 <!--3607762-->  


### <a name="sql-query"></a><a name="bkmk_sql"></a> SQL 查询

- **SQL Server 实例**：选择是要对默认实例、所有实例，还是对指定数据库实例名称运行 SQL 查询。  

    > [!NOTE]  
    > 实例名称必须引用 SQL Server 的本地实例。 为了引用群集的 SQL Server 实例，应该使用脚本设置。  

- **数据库**：指定要对其运行 SQL 查询的 Microsoft SQL Server 数据库的名称。  

- **列**：指定用于评估全局条件的符合性的 Transact-SQL 语句返回的列名。  

- **Transact-SQL 语句**：指定要用于全局条件的完整 SQL 查询。 若要使用现有的 SQL 查询，请选择“打开”  。  

    > [!IMPORTANT]  
    > SQL 查询设置不支持任何修改数据库的 SQL 命令。 只能使用从数据库读取信息的 SQL 命令。  


### <a name="wql-query"></a><a name="bkmk_wql"></a> WQL 查询

- **命名空间**：指定客户端计算机上要评估其符合性的 WMI 命名空间。 默认值为 `root\cimv2`。  

- **类**：在上述命名空间中指定目标 WMI 类。  

- **属性**：在上述类中指定目标 WMI 属性。  

- **WQL 查询 WHERE 子句**：指定有限制的子句以减少结果。 例如，若要只查询 Win32_Service 类中的 DHCP 服务，WHERE 子句可以是 `Name = 'DHCP' and StartMode = 'Auto'`。   


### <a name="xpath-query"></a><a name="bkmk_xpath"></a> XPath 查询

- **路径**：指定客户端计算机上用于评估符合性的 .xml 文件的路径。 Configuration Manager 支持在路径名称中使用所有 Windows 系统环境变量和 `%USERPROFILE%` 用户变量。  

- **XML 文件名**：指定在上述路径中包含 XML 查询的文件名。  

- **包括子文件夹**：启用此选项可以搜索指定路径下的任何子文件夹。  

- **此文件与 64 位应用程序相关联**：在运行 64 位版本 Windows 的 Configuration Manager 客户端上，除了搜索 32 位系统文件位置 `%Windir%\Syswow64`，还可以搜索 64 位系统文件位置 `%Windir%\System32`。  

- **XPath 查询**：指定有效的完整 XML 路径语言 (XPath) 查询。  

- **命名空间**：标识要在 XPath 查询期间使用的命名空间和前缀。  

如果你尝试发现加密的 .xml 文件，符合性设置会查找文件，但 XPath 查询不会生成任何结果。 Configuration Manager 客户端未生成错误。  

如果 XPath 查询无效，设置会在客户端计算机上被评估为不符合。  



##  <a name="configure-compliance-rules"></a>配置符合性规则  

符合性规则指定定义配置项目的符合性的条件。 设置必须具有至少一个符合性规则，才能对它评估符合性。 WMI、 注册表和脚本设置可以修正找到要不符合要求的值。 您可以创建新的规则或浏览到要在其中选择规则任何配置项目中的现有设置。  


### <a name="to-create-a-compliance-rule"></a>若要创建符合性规则  

1. 在“创建配置项目向导”  的“符合性规则”  页上，选择“新建”  。  

2. 在 **Create Rule** 对话框框中，提供以下信息：  

    - **名称**：输入符合性规则的名称。  

    - **描述**：输入符合性规则的说明。  

    - **选定的设置**：选择“浏览”  以打开“选择设置”  对话框。 选择要为其定义规则的设置，或单击“新建设置”  。 完成后，选择“选择”  。  

        > [!Tip]  
        > 如要查看当前选定设置的相关信息，请选择“属性”  。  

    - **规则类型**：选择要使用的符合性规则的类型：  

        - **值**：创建可以将配置项目返回的值与指定的值进行比较的规则。 有关其他设置的详细信息，请参阅[值规则](#bkmk_value)。  

        - **现有**：创建根据设置是否存在于客户端设备上或根据找到它的次数来评估设置的规则。 有关其他设置的详细信息，请参阅[现有规则](#bkmk_exist)。  

3. 单击“确定”  ，以关闭“创建规则”  对话框。  




### <a name="value-rules"></a><a name="bkmk_value"></a> 值规则  

- **属性**：要检查的对象的属性取决于选定的设置。 可用属性因设置类型而异。 

- **设置必须符合以下规则**：可用的规则或权限因设置类型而异。

- **在支持时修正非符合性规则**：如果希望 Configuration Manager 自动修正不符合性规则，请选择此选项。 Configuration Manager 通过以下规则类型支持此操作：  

    - **注册表值**：如果不符合，客户端将设置注册表值。 如果不存在，客户端将创建该值。  

    - **脚本**：客户端使用通过设置指定的修正脚本。  

    - **WQL 查询**  

    > [!IMPORTANT]  
    > 仅当规则运算符设置为“等于”  时，才能修正非符合性规则。  

- **在找不到此设置实例时报告不相容**：如果在客户端计算机上找不到此设置，请为配置项目启用此选项以报告不符合项。  

- **报表的不符合性严重程度**：指定不符合此符合性规则时报告的严重性级别（在 Configuration Manager 报表中）。 可用的严重性级别如下：  
    - **无**  
    - **信息**  
    - **警告**  
    - **严重**  
    - **严重事件**：不符合此符合性规则的计算机将报告故障严重性“严重”  。 应用程序事件日志中也会以 Windows 事件的形式记录此严重性级别。  


### <a name="existential-rules"></a><a name="bkmk_exist"></a> 现有规则 

> [!NOTE]  
> 显示的选项可能视为其配置规则的设置类型而异。  

- **此设置必须存在于客户端设备**  

- **设置不得存在于客户端设备**  

- **该设置会发生以下次数：**  

- **报表的不符合性严重程度**：指定不符合此符合性规则时报告的严重性级别（在 Configuration Manager 报表中）。 可用的严重性级别如下：  
    - **无**  
    - **信息**  
    - **警告**  
    - **严重**  
    - **严重事件**：不符合此符合性规则的计算机将报告故障严重性“严重”  。 应用程序事件日志中也会以 Windows 事件的形式记录此严重性级别。  


## <a name="track-configuration-item-remediations"></a><a name="bkmk_track"></a> 跟踪配置项目修正
<!--4261411-->
（从版本 2002 中引入） 

从 Configuration Manager 版本 2002 开始，可在配置项目符合性规则上“跟踪修正历史记录(如支持)”  。 启用此选项后，客户端上发生的配置项目的任何修正都会生成状态消息。 历史记录存储在 Configuration Manager 数据库中。

使用公共视图“v_CIRemediationHistory”生成自定义报表以查看修正历史记录  。 `RemediationDate` 列是客户端执行修正的时间（以 UTC 为单位）。 `ResourceID` 用于标识设备。 使用“v_CIRemediationHistory”视图生成自定义报表有助于  ：

- 确定修正脚本可能存在的问题
- 找出修正的趋势，如每个评估周期中始终不符合要求的客户。

### <a name="enable-the-track-remediation-history-when-supported-option"></a>启用“跟踪修正历史记录(如支持)”选项

- 对于新配置项目，在向导的“设置”页面上创建新设置时，请在“符合性规则”选项卡中添加“跟踪修正历史记录(如支持)”选项    。
- 对于现有配置项，请在配置项目“属性”中的“符合性规则”选项卡上添加“跟踪修正历史记录(如支持)”选项    。
[ ![版本 2002 中的“跟踪修正历史记录(如支持)”](./media/4261411-remediation-history.png)](./media/4261411-remediation-history.png#lightbox)

## <a name="next-steps"></a>后续步骤

[创建配置基线](create-configuration-baselines.md)
