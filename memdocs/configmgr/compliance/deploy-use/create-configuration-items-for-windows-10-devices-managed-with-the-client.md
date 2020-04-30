---
title: 创建 Windows 10 配置项目
titleSuffix: Configuration Manager
description: 使用 Windows 10 配置项目管理由 Configuration Manager 客户端托管的 Windows 10 计算机的设置。
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 14226fbe-dd07-4432-910b-130790624a4e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 9a1bda440ab3ccd02432f0b023a134b9f54cdafb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692535"
---
# <a name="create-configuration-items-for-windows-10-devices"></a>创建 Windows 10 设备的配置项目

使用 Configuration Manager Windows 10  配置项目管理由 Configuration Manager 客户端托管的 Windows 10 计算机的设置。  
  
> [!IMPORTANT]  
>  在此版本中，如果你创建了“密码”设置并将其设为“Windows 10”类型的配置项目的一部分（针对使用 Configuration Manager 客户端进行管理的设备），请注意以下问题   。 如果该设置尚不存在，或者未在 Windows 10 设备上配置，则该设备将被错误地评估为“符合”。  
>   
>  作为解决方法，在为这些设备创建设置时，请确保在创建配置项目向导的设置页上选择“修正非符合性设置”  。 此外，如果部署的配置基线中的 Windows 10 配置项目包含密码设置，还请选择“在支持时修正不相容规则”  。 在“部署配置基线”对话框中选择此项。 使用此解决方法，可以监视设置，并在发现它不相容时修正设置。 修正后，设置会正确报告为“相容”  （除非遇到问题，在这种情况下，它会报告“错误”  ）。  
  
### <a name="to-create-a-windows-10-configuration-item"></a>创建 Windows 10 配置项目  
  
1. 在 Configuration Manager 控制台中，选择“资产和合规性”  。  
  
2. 在“资产和合规性”  工作区中，展开“合规性设置”  ，再选择“配置项目”  。  
  
3. 在“主页”  选项卡的“创建”  组中，选择“创建配置项目”  。  
  
4. 在“创建配置项目”  向导的“常规”  页上，指定配置项目的名称和可选说明。  
  
5. 在“指定要创建的配置项目的类型”  下，选择“Windows 10”  。  
  
6. 若要创建和分配有助于在 Configuration Manager 控制台中搜索和筛选配置项目的类别，请选择“类别”  。  
  
7. 在向导的“支持的平台”  页上，选择将评估配置项目的特定 Windows 10 平台。  
  
8. 在向导的“设备设置”  页面上，选择要配置的设置组。 （有关详细信息，请参阅本文中的 [Windows 10 配置项目设置参考](#BKMK_Ref)。）然后选择“下一步”  。  
  
   > [!TIP]  
   >  如果所需设置未列出，请选中“配置默认设置组以外的其他设置”  复选框。  
  
9. 在每个设置页上，配置所需设置，以及是否要在它们在设备上不符合要求时修正它们（如果支持这样做）。  
  
10. 对于每个设置组，还可以配置在发现配置项目不相容时报告的严重性：  
  
    -   **无**：对于 Configuration Manager 报表，不符合此合规性规则的设备不报告故障严重性。  
  
    -   **信息**：对于 Configuration Manager 报表，不符合此符合性规则的设备将故障严重性报告为**信息**。  
  
    -   **警告**：对于 Configuration Manager 报表，不符合此符合性规则的设备将故障严重性报告为**警告**。  
  
    -   **严重**：对于 Configuration Manager 报表，不符合此符合性规则的设备将故障严重性报告为**严重**。  
  
    -   **严重事件**：对于 Configuration Manager 报表，不符合此符合性规则的设备将故障严重性报告为**严重**。 应用程序事件日志中也会以 Windows 事件的形式记录此严重性级别。  
  
11. 在向导的“平台适用性”  页上，查看任何与先前选择的受支持平台不兼容的设置。 你可以返回并删除这些设置，也可以继续。  
  
    > [!TIP]  
    >  不会对不受支持的设置评估符合性。  
  
12. 完成向导。  
  
    可以在“资产和符合性”  工作区的“配置项目”  节点中查看新配置项目。  
  
## <a name="windows-10-configuration-item-settings-reference"></a><a name="BKMK_Ref"></a> Windows 10 configuration item settings reference  
  
### <a name="password"></a>Password  
  
|设置|详细信息|  
|-------------|-------------|  
|**设备上需要密码设置**|支持的设备上需要密码。|  
|**最短密码长度（字符）**|密码的最短长度（以字符为单位）。|  
|**密码过期天数**|必须更改密码前的天数。|  
|**记住的密码数**|防止重复使用以前的密码。|  
|**擦除设备前的失败登录尝试次数**|如果登录失败次数达到此次数，则擦除设备。|  
|**锁定设备前的空闲时间**|指定设备在自动锁定之前必须处于非活动状态的分钟数。|  
|**密码复杂性**|选择是否可以指定一个 PIN（例如“1234”），或是否必须提供一个强密码。|
|**密码中需要的复杂字符集数**|如果选择“强”  密码，使用此设置配置所需的复杂字符集数量。 对于强密码，至少应将此设置设为“3”  ，表示必须包含字母和数字。 若要强制执行必须额外包含特殊字符（如 (%$  ）的密码，请选择“4”  。<br>（仅 Windows 10）  |
  
###  <a name="device"></a>设备  
  
|设置名|详细信息|  
|------------------|-------------|  
|**蓝牙**|允许在设备上使用蓝牙功能。|  
  
### <a name="cloud"></a>云  
  
|设置名|详细信息|  
|------------------|-------------|  
|**设置同步**|允许设备之间的设置同步。|  
|**凭据同步**|允许设备之间的凭据同步。|  
|**通过按流量计费的连接进行设置同步**|允许在 Internet 连接按流量计费时同步设置。|  
  
### <a name="roaming"></a>漫游  
  
|设置名|详细信息|  
|------------------|-------------|  
|**数据漫游**|允许在访问数据时在网络之间进行漫游。|  
  
### <a name="encryption"></a>加密  
  
|设置名|详细信息|  
|------------------|-------------|  
|**设备上的文件加密**|要求对设备上的文件进行加密。|  
  
### <a name="system-security"></a>系统安全  
  
|设置名|详细信息|  
|------------------|-------------|  
|**用户帐户控制**|配置设备上的 Windows 用户帐户控制的工作方式。<br />例如，可以禁用它，或设置它通知你时所处的级别。|  
|**网络防火墙**|启用或禁用 Windows 防火墙。|  
|**SmartScreen**|启用或禁用 Windows SmartScreen。|  
|**病毒保护**|要求必须安装并配置防病毒软件。|  
|**病毒保护签名为最新**|要求设备上的防病毒软件的签名文件必须保持最新状态。|  
  
### <a name="windows-information-protection"></a>Windows 信息保护

随着企业中员工自带设备数量的增加，通过应用和服务（如电子邮件、社交媒体和公有云）意外泄露数据的风险也在不断增加。 这些超出了组织的控制范围。 例如，当员工：

- 从个人电子邮件帐户发送最新的工程图片。
- 将产品信息复制粘贴到推文中。
- 将正在进行的销售报表保存到其公有云存储中。

Windows 信息保护（WIP，旧称为“企业数据保护”）有助于防止这种潜在的数据泄露，而不会干扰员工的体验。 WIP 还有助于防范企业应用和数据在企业自有设备和员工工作使用的个人设备上发生意外数据泄露。 WIP 无需更改环境或其他应用。

Configuration Manager Windows 信息保护配置项目会管理以下各项：

- 由 WIP 保护的应用列表
- 企业网络位置
- 保护级别
- 加密设置
  
要了解如何使用 Configuration Manager 来配置 WIP，请参阅：

- [使用 Windows 信息保护 (WIP) 保护企业数据](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [使用 Configuration Manager 创建和部署 Windows 信息保护 (WIP) 策略](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)
- [使用 Windows 信息保护 (WIP) 时的限制](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/limitations-with-wip)

## <a name="see-also"></a>另请参阅  
[为使用 Configuration Manager 客户端管理的设备配置项目](../../compliance/deploy-use/create-configuration-items.md)
