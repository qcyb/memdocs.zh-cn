---
title: 扩展硬件清单
titleSuffix: Configuration Manager
description: 了解扩展 Configuration Manager 中硬件清单的方法。
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 380ba550a6edb0f639644280df74c500663e19f4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695415"
---
# <a name="how-to-extend-hardware-inventory-in-configuration-manager"></a>如何扩展 Configuration Manager 中的硬件清单

适用范围：  Configuration Manager (Current Branch)

硬件清单通过使用 Windows Management Instrumentation (WMI) 从 Windows 电脑读取信息。 WMI 是基于 Web 的企业管理 (WBEM) 的 Microsoft 实现，是用于访问企业中管理信息的行业标准。 在以前版本的 Configuration Manager 中，通过修改站点服务器上的文件 sms_def.mof 扩展硬件清单。 此文件包含可由硬件清单读取的 WMI 类的列表。 编辑此文件，可以启用和禁用现有类，还能将新类创建到清单。  

Configuration.mof 文件用于定义要通过客户端上的硬件清单列出清单的数据类，与 Configuration Manager 2012 相比并无变化。 你可以创建数据类，以列出客户端系统上存在的现有或自定义 WMI 存储库数据类或注册表项的清单。  

 Configuration.mof 文件还定义并注册 WMI 提供程序用于访问在硬件清单期间的设备信息。 通过注册提供程序，可以定义要使用的提供程序类型和提供程序支持的类。  

 当 Configuration Manager 客户端请求策略时，Configuration.mof 将被附加到策略正文。 然后下载此文件并对其进行了编译的客户端。 当添加、 修改或删除 Configuration.mof 文件中的数据类时，客户端将自动编译对清单相关的数据类进行这些更改。 不需要执行进一步的操作来列出 Configuration Manager 客户端上新数据类或已修改数据类的清单。 此文件在主站点服务器上的位置是 **<CMInstallLocation\>\Inboxes\clifiles.src\hinv\\** 。  

 在 Configuration Manager 中，不能再像在 Configuration Manager 2007 中那样编辑 sms_def.mof 文件。 相反，你可以启用和禁用 WMI 类，并通过使用客户端设置来添加硬件清单将收集的新类。 Configuration Manager 提供了以下方法来扩展硬件清单。  

> [!NOTE]  
>  如果手动更改了 Configuration.mof 文件以添加自定义清单类，则在更新到版本 1602 时，这些更改将被覆盖。 若要在更新后继续使用自定义类，必须在更新到 1602 后将这些类添加到 Configuration.mof 文件的“已添加扩展”部分中。  
> 但是，请勿修改此部分上的任何内容，因为这些部分保留供 Configuration Manager 修改。 自定义 Configuration.mof 的备份位于：  
> **<CM Install dir\>\data\hinvarchive\\** 。  

|方法|更多信息|  
|------------|----------------------|  
|启用或禁用现有的清单类|启用或禁用默认清单类，或创建允许你从指定的客户端集合收集不同的硬件清单类的自定义客户端设置。 请参阅本文中的[启用或禁用现有清单类](#BKMK_Enable)过程。|  
|添加一个新的清单类|从另一台设备的 WMI 命名空间添加一个新的清单类。 请参阅本文中的[添加新的清单类](#BKMK_Add)过程。|  
|导入和导出硬件清单类|从 Configuration Manager 控制台导入和导出包含清单类的托管对象格式 (MOF) 文件。 请参阅本文中的[导入硬件清单类](#BKMK_Import)和[导出硬件清单类](#BKMK_Export)过程。|  
|创建 NOIDMIF 文件|使用 NOIDMIF 文件可收集有关无法由 Configuration Manager 列出清单的客户端设备的信息。 例如，您可能想要收集设备资产编号的信息仅作为在设备上的标签存在。 NOIDMIF 清单是自动与收集从客户端设备相关联。 请参阅本文中的[创建 NOIDMIF 文件](#BKMK_NOIDMIF)。|  
|创建 IDMIF 文件|使用 IDMIF 文件收集组织中不与 Configuration Manager 客户端关联的资产的相关信息，例如，投影仪、复印机和网络打印机。 请参阅本文中的[创建 IDMIF 文件](#BKMK_IDMIF)。|  

## <a name="procedures-to-extend-hardware-inventory"></a>扩展硬件清单的过程  
这些过程帮助您配置硬件清单的默认客户端设置和它们适用于层次结构中的所有客户端。 如果希望这些设置仅应用于某些客户端，请创建自定义客户端设备设置，并将它分配给特定客户端的集合。 请参阅[如何配置客户端设置](../../../../core/clients/deploy/configure-client-settings.md)。  

###  <a name="to-enable-or-disable-existing-inventory-classes"></a><a name="BKMK_Enable"></a> 若要启用或禁用现有清单类  

1.  在 Configuration Manager 控制台中，选择“管理”   > “客户端设置”   > “默认客户端设置”  。  

4.  在“主页”  选项卡上的“属性”  组中，选择“属性”  。  

5.  在“默认客户端设置”  对话框中，选择“硬件清单”  。  

6.  在**设备设置**列表中，单击**设置类**。  

7.  在 **硬件清单类** 对话框框中，选中或清除的类和类属性，以按照硬件清单收集。 您可以展开以选择或清除使该类中的各个属性的类。 使用 **清单类搜索** 字段以单个类中搜索。  

    > [!IMPORTANT]  
    >  将新类添加到 Configuration Manager 硬件清单时，收集和发送到站点服务器的清单文件的大小将增加。 这可能会对你的网络和 Configuration Manager 站点的性能产生负面影响。 启用您想要收集的清单类。  


###  <a name="to-add-a-new-inventory-class"></a><a name="BKMK_Add"></a> 若要添加新的清单类  

只能从层次结构的顶层服务器并通过修改默认客户端设置来添加清单类。 当创建自定义设备设置此选项不可用。

1. 在 Configuration Manager 控制台中，选择“管理”   > “客户端设置”   > “默认客户端设置”  。  

2. 在“主页”  选项卡上的“属性”  组中，选择“属性”  。  

3. 在“默认客户端设置”  对话框中，选择“硬件清单”  。  

4. 在“设备设置”  列表中，选择“设置类”  。  

5. 在“硬件清单类”  对话框中，选择“添加”  。  

6. 在 **添加硬件清单类** 对话框中，单击 **连接**。  

7. 在 **连接到 Windows Management Instrumentation (WMI)** 对话框框中，指定将用于检索 WMI 类要用于检索这些类的 WMI 命名空间的计算机的名称。 如果您想要检索您指定的 WMI 命名空间下的所有类中，单击 **递归**。 如果您要连接到计算机不是本地计算机，提供有权访问远程计算机上的 WMI 的帐户的登录凭据。  

8. 选择“连接”  。  

9. 在“添加硬件清单类”  对话框的“清单类”  列表中，选择想要添加到 Configuration Manager 硬件清单的 WMI 类。  

10. 如果想要编辑所选的 WMI 类的相关信息，请选择“编辑”  ，然后在“类限定符”  对话框框中，提供以下信息：  

    - **显示名称** - 此名称将显示在资源浏览器中。  

    - **属性** - 指定将在其中显示 WMI 类的每个属性的单元。  

      此外可以将属性指定为键属性来帮助唯一地标识每个类的实例。 如果类未定义任何键，从客户端报告的类的多个实例只能找到的最新的实例存储在数据库中。  

      完成属性配置后，单击“确定”关闭“类限定符”对话框和其他打开的对话框   。 

###  <a name="to-import-hardware-inventory-classes"></a><a name="BKMK_Import"></a> 若要导入硬件清单类  

当您修改默认客户端设置时，只可以导入清单类。 但是，可以使用自定义客户端设置导入不包含架构更改的信息，例如将现有类的属性从“True”更改为“False”   。  

1.  在 Configuration Manager 控制台中，选择“管理”   >  “客户端设置”   > “默认客户端设置”  。  

4.  在“主页”  选项卡上的“属性”  组中，选择“属性”  。  

5.  在“默认客户端设置”  对话框中，选择“硬件清单”  。  

6.  在“设备设置”  列表中，选择“设置类”  。  

7.  在“硬件清单类”  对话框中，选择“导入”  。  

8.  在“导入”  对话框中，选择想要导入的托管对象格式 (MOF) 文件，然后选择“确定”  。 查看要导入的项，然后单击“导入”  。  

###  <a name="to-export-hardware-inventory-classes"></a><a name="BKMK_Export"></a> 若要导出硬件清单类  

1.  在 Configuration Manager 控制台中，选择“管理”   > “客户端设置”   > “默认客户端设置”  。  

4.  在“主页”  选项卡上的“属性”  组中，选择“属性”  。  

5.  在“默认客户端设置”  对话框中，选择“硬件清单”  。  

6.  在“设备设置”  列表中，选择“设置类”  。  

7.  在“硬件清单类”  对话框中，选择“导出”  。  

    > [!NOTE]  
    >  导出类时，将导出所有当前所选的类。  

8.  在“导出”  对话框中，指定想要将类导出到的托管对象格式 (MOF) 文件，然后选择“保存”  。  

### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a><a name="bkmk_GreaterThan255"></a>配置硬件清单以收集超过 255 个字符的字符串
从 Configuration Manager 1802 开始，可以针对硬件清单属性将字符串长度指定为超过 255 个字符。 此更改仅适用于新添加的类和不为键的硬件清单属性。 <!-- 1357389 -->

1. 单击“管理”工作区中的“客户端设置”，突出显示客户端设备设置以便编辑，右键单击然后选择“属性”    。

2. 依次选择“硬件清单”、“设置类”和“添加”    。

3. 单击“连接”按钮  。

4. 填写“计算机名称”、“WMI 命名空间”，如有必要，选择“递归”    。 如有必要，请提供凭据以连接。 单击“连接”以查看命名空间类  。

5. 选择新类，然后单击“编辑”  。

6. 将非键且为字符串的属性的长度更改为大于 255  。 单击" **确定**"。 

7. 确保为“添加硬件清单类”选择编辑的属性，并单击“确定”   。 


## <a name="how-to-use-management-information-files-mif-files-to-extend-hardware-inventory"></a>如何使用管理信息文件（MIF 文件）扩展硬件清单  
 使用管理信息格式 (MIF) 文件扩展 Configuration Manager 从客户端收集的硬件清单信息。 在硬件清单过程中，存储在 MIF 文件中的信息被添加到客户端清单报表并存储在站点数据库中，使用站点数据库中数据的方式可以与使用默认客户端清单数据的方式相同。 有两种类型的 MIF 文件：NOIDMIF 和 IDMIF。

> [!IMPORTANT]  
>  必须为 MIF 文件创建或导入类信息，才能将其中数据添加到 Configuration Manager 数据库。 有关详细信息，请参阅本文中的[添加新的清单类](#BKMK_Add)和[导入硬件清单类](#BKMK_Import)部分。  

###  <a name="to-create-noidmif-files"></a><a name="BKMK_NOIDMIF"></a> 若要创建 NOIDMIF 文件  
 NOIDMIF 文件可用于将信息添加到通常不能被 Configuration Manager 收集且与特定客户端设备相关联的客户端硬件清单。 例如，许多公司用一个资产编号标记组织中的每台计算机，然后对这些编号进行手动分类。 创建 NOIDMIF 文件时，可将此信息添加到 Configuration Manager 数据库并用于查询和报告。 有关创建 NOIDMIF 文件的信息，请参阅 Configuration Manager SDK 文档。  

> [!IMPORTANT]  
>  创建 NOIDMIF 文件时，必须以 ANSI 编码格式保存。 Configuration Manager 无法读取以 UTF-8 编码格式保存的 NOIDMIF 文件。  

 创建 NOIDMIF 文件后，将其存储在每个客户端上的 %Windir%  \CCM\Inventory\Noidmifs  文件夹中。 Configuration Manager 将在下一个计划的硬件清单周期中从此文件夹中的 NODMIF 文件收集信息。  

###  <a name="to-create-idmif-files"></a><a name="BKMK_IDMIF"></a> 若要创建 IDMIF 文件  
 IDMIF 文件可用于将有关资产（通常不能被 Configuration Manager 列出清单并且不与特定客户端设备相关联）的信息添加到 Configuration Manager 数据库。 例如，可以使用 IDMIFS 收集有关投影仪、DVD 播放机、复印机或不具有 Configuration Manager 客户端的其他设备的信息。 有关创建 IDMIF 文件的信息，请参阅 Configuration Manager SDK 文档。  

 创建 IDMIF 文件后，将其存储在客户端计算机上的 %Windir%  \CCM\Inventory\Idmifs  文件夹中。 Configuration Manager 将在下一个计划的硬件清单周期中从此文件收集信息。 您必须声明通过添加或将其导入该文件中包含的信息的新类。  

> [!NOTE]
> MIF 文件可能包含大量数据，收集这些数据可能对你网站的性能产生负面影响。 仅在需要时启用 MIF 收集，并在硬件清单设置中配置“最大自定义 MIF 文件大小 (KB)”  选项。 有关详细信息，请参阅[硬件清单简介](introduction-to-hardware-inventory.md)。
