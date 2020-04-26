---
title: 在无 Internet 连接的情况下同步 Office 365 更新
titleSuffix: Configuration Manager
description: 在断开 Internet 连接的顶层软件更新点上同步 Office 365 更新。
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: a8fa7e7a-bf55-42de-b0c2-c56777dc1508
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 3627d2f7772b7b9e133d742b0ee4f94dba6e457a
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110349"
---
# <a name="synchronize-office-365-updates-from-a-disconnected-software-update-point"></a><a name="bkmk_O365"></a> 从断开连接的软件更新点同步 Office 365 更新

适用范围：  Configuration Manager (Current Branch)
<!--4065163-->
从 Configuration Manager 版本 2002 开始，可使用工具将 Office 365 更新从连接了 Internet 的 WSUS 服务器导入到已断开连接的 Configuration Manager 环境中。 以前，当你导出和导入在已断开连接的环境中更新的软件的元数据时，无法部署 Office 365 更新。 Office 365 更新需要从 Office API 和 Office CDN 下载的其他元数据，这对于已断开连接的环境是不可能的。

> [!Note]
> 自 2020 年 4 月 21 日起，Office 365 专业增强版已重命名为 Microsoft 365 企业应用版  。 有关详细信息，请参阅 [Office 365 专业增强版的名称变更](https://docs.microsoft.com/deployoffice/name-change)。 在控制台更新期间，你可能仍会看到 Configuration Manager 控制台和支持文档中引用的是旧名称。

## <a name="prerequisites"></a>必备条件

- 连接了 Internet 的 WSUS 服务器至少运行 Windows Server 2012。
- WSUS 服务器需要连接到这两个 Internet 终结点：
   - `officecdn.microsoft.com`
   - `config.office.com`
- 将 OfflineUpdateExporter 工具及其依赖项复制到连接了 Internet 的 WSUS 服务器。
  - 该工具及其依赖项位于 &lt;ConfigMgrInstallDir>/tools/OfflineUpdateExporter 目录中  。
- 运行该工具的用户必须属于 WSUS 管理员组  。
- 为存储 Office 更新元数据和内容而创建的目录应具有相应的访问控制列表 (ACL) 来保护文件。
    - 此目录还必须为空。
- 应安全地移动从联机 WSUS 服务器移动到已断开连接的环境的数据。

> [!IMPORTANT]
> 将下载所有 Office 365 语言的内容。 每个更新可以有大约 10 GB 的内容。

## <a name="synchronize-then-decline-unneeded-office-365-updates"></a>同步后，拒绝不需要的 Office 365 更新

1. 在连接了 Internet 的 WSUS 上，打开 WSUS 控制台。
1. 依次选择“选项”、“产品和分类”   。
1. 在“产品”选项卡中选择“Office 365 客户端”并在“分类”选项卡中选择“更新”     。[![WSUS 中的 Office 365 更新的产品和分类](./media/4065163-o365-updates-product-classification.png)](./media/4065163-o365-updates-product-classification.png#lightbox)
1. 转到“同步”并选择“立即同步”以将 Office 365 更新同步到 WSUS 中   。
1. 同步完成后，拒绝不希望使用 Configuration Manager 部署的任何 Office 365 更新。 不需要批准 Office 365 更新即可下载。  
   - 在 WSUS 中拒绝不需要的 Office 365 更新不会阻止在 WsusUtil.exe 导出期间导出这些更新，但会阻止 OfflineUpdateExporter 工具下载相关内容。
   - OfflineUpdateExporter 工具可为你下载 Office 365 更新。 如果要导出其他产品的更新，则这些产品仍需获得批准以便下载。
    - [在 WSUS 中创建新的更新视图](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/manage/viewing-and-managing-updates#to-create-a-new-update-view-on-wsus)，以便在 WSUS 中轻松查看和拒绝不需要的 Office 365 更新。
1. 如果要批准其他产品更新以便下载和导出，请等待内容下载完成，然后再运行 WsusUtil.exe 导出并复制 WSUSContent 文件夹的内容。 有关详细信息，请参阅[从断开连接的软件更新点中同步软件更新](synchronize-software-updates-disconnected.md)

## <a name="exporting-the-office-365-updates"></a>导出 Office 365 更新

1. 将 OfflineUpdateExporter 文件夹从 Configuration Manager 复制到连接了 Internet 的 WSUS 服务器。
    - 该工具及其依赖项位于 &lt;ConfigMgrInstallDir>/tools/OfflineUpdateExporter 目录中  。
1. 在连接了 Internet 的 WSUS 服务器上的命令提示符下，使用以下用法运行该工具：**OfflineUpdateExporter.exe -O -D &lt;destination path>**

   |OfflineUpdateExporter Parameter|说明|
   |---|---|
   |**-O**|  **-Office**。 指定用于更新导出的产品为 Office 365|
   |**-D**|**-Destination**。 Destination 是必需的参数，需要目标文件夹的整个路径。|

   - OfflineUpdateExporter 工具执行以下操作  ：
      - 连接到 WSUS
      - 读取 WSUS 中的 Office 365 更新元数据
      - 将 Office 365 更新所需的内容和任何其他元数据下载到目标文件夹

1. 在连接了 Internet 的 WSUS 服务器上的命令提示符下，导航到包含 WsusUtil.exe 的文件夹。 默认情况下，该工具位于 %ProgramFiles%\Update Services\Tools  。 例如，如果该工具位于默认位置中，则键入 **cd %ProgramFiles%\Update Services\Tools**。
   - 如果使用的是 Windows Server 2012，请确保 WSUS 服务器上安装了 [KB2819484](https://support.microsoft.com/help/2819484/cab-file-that-is-exported-by-using-the-wsusutil-exe-command-is-display)。
   - 运行 WsusUtil 工具的用户必须是服务器上的本地管理员组的成员。

1. 键入下列命令以将软件更新元数据导出为一个 GZIP 文件：  

    **WsusUtil.exe export**  *packagename*  *logfile*  

    例如：  

    **WsusUtil.exe export export.xml.gz export.log**

1. 将 export.xml.gz 文件复制到已断开连接的网络上的顶层 WSUS 服务器  。
1. 如果已批准其他产品的更新，请将 WSUSContent 文件夹的内容复制到已断开连接的顶层 WSUS 服务器的 WSUSContent 文件夹。
1. 将用于 OfflineUpdateExporter 的目标文件夹复制到已断开连接的网络上的顶层 Configuration Manager 站点服务器  。

## <a name="import-the-office-365-updates"></a>导入 Office 365 更新

1. 在已断开连接的顶层 WSUS 服务器上，从 export.xml.gz 导入在连接了 Internet 的 WSUS 服务器上生成的更新元数据  。
   
    例如：  

    **WsusUtil.exe import export.xml.gz import.log**
    
    默认情况下，WsusUtil.exe 工具位于 %ProgramFiles%\Update Services\Tools  。

1. 导入完成后，需要在已断开连接的顶层 Configuration Manager 站点服务器上配置站点控制属性。 此配置更改将 Configuration Manager 指向 Office 365 的内容。 若要更改属性的配置，请执行以下操作：
   1. 将 [O365OflBaseUrlConfigured PowerShell 脚本](#bkmk_o365_script)复制到已断开连接的顶层 Configuration Manager 站点服务器。
   1. 将 `"D:\Office365updates\content"` 更改为包含 Office 内容和 OfflineUpdateExporter 生成的元数据的复制目录的完整路径。
      > [!IMPORTANT]
      > 只有本地路径适用于 O365OflBaseUrlConfigured 属性。
   1. 将脚本另存为 `O365OflBaseUrlConfigured.ps1`
   1. 在已断开连接的顶层 Configuration Manager 站点服务器上的提升的 PowerShell 窗口中，运行 `.\O365OflBaseUrlConfigured.ps1`。
   1. 在站点服务器上，重新启动 SMS_Executive 服务  。
1. 在 **Configuration Manager** 控制台中，导航到“管理”   > “站点配置”   > “站点”  。
1. 右键单击顶层站点，依次选择“配置站点组件” > “软件更新点”   。
1. 在“分类”选项卡上，选择“更新”   。 在“产品”  选项卡中，选择“Office 365 客户端”  。
1. [同步 Configuration Manager 软件更新](synchronize-software-updates.md#manually-start-software-updates-synchronization)
1. 同步完成后，使用正常过程来部署 Office 365 更新。

## <a name="proxy-configuration"></a><a name="bkmk_O365_ki"></a> 代理配置

- 代理配置未在本机内置于工具。 如果在运行该工具的服务器上的“Internet 选项”中设置了代理，理论上将使用它并正常运行。
   - 在命令提示符下，运行 `netsh winhttp show proxy` 以查看配置的代理。



## <a name="modify-o365oflbaseurlconfigured-property"></a><a name="bkmk_o365_script"></a> 修改 O365OflBaseUrlConfigured 属性

```powershell
# Name: O365OflBaseUrlConfigured.ps1
#
# Description: This sample sets the O365OflBaseUrlConfigured property for the SMS_WSUS_CONFIGURATION_MANAGER component on the top-level site.
# This script must be run on the disconnected top-level Configuration Manager site server
#
# Replace "D:\Office365updates\content" with the full path to the copied directory containing all the Office metadata and content generated by the OfflineUpdateExporter tool.
# Only local paths work for the O365OflBaseUrlConfigured property.

$PropertyValue = "D:\Office365updates\content"

# Don't change any of the lines below
$PropertyName = "O365OflBaseUrlConfigured"

# Get provider instance
$providerMachine = Get-WmiObject -namespace "root\sms" -class "SMS_ProviderLocation"

if($providerMachine -is [system.array])
{
    $providerMachine=$providerMachine[0]
}

$SiteCode = $providerMachine.SiteCode

$component = gwmi -ComputerName $providerMachine.Machine -namespace root\sms\site_$SiteCode -query 'select comp.* from sms_sci_component comp join SMS_SCI_SiteDefinition sdef on sdef.SiteCode=comp.SiteCode where sdef.ParentSiteCode="" and comp.componentname="SMS_WSUS_CONFIGURATION_MANAGER"'
$properties = $component.props

Write-host "Updating $PropertyName property for site " $SiteCode

foreach ($property in $properties)
{
  if ($property.propertyname -eq $PropertyName) 
  {
    Write-host "Current value for $PropertyName is $($property.value2)"
    $property.value2 = $PropertyValue
    Write-host "Updating value for $PropertyName to $($property.value2)"
    break
  }
}

$component.props = $properties
$component.put()
```

## <a name="next-steps"></a>后续步骤

[将软件更新添加到更新组](../deploy-use/add-software-updates-to-an-update-group.md)