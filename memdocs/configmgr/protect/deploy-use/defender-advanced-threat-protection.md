---
title: Microsoft Defender 高级威胁防护
titleSuffix: Configuration Manager
description: 了解如何管理和监视 Microsofts Defender 高级威胁防护 - 这是一项可帮助企业应对高级安全攻击的新服务。
ms.date: 06/17/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5feaf05a6829d902b1d8dcbe57722dfce410de6f
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88693533"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender 高级威胁防护

适用范围：Configuration Manager (Current Branch)

Endpoint Protection 可帮助管理和监视 [Microsoft Defender 高级威胁防护 (ATP)](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)（之前称为 Windows Defender ATP）。 Microsoft Defender ATP 可帮助企业检测和调查其网络上的高级攻击并作出应对。 Configuration Manager 策略可帮助加入和监视 Windows 10 客户端。

Microsoft Defender ATP 是 [Microsoft Defender 安全中心](https://securitycenter.windows.com)提供的一项服务。 通过添加和部署客户端加入配置文件，Configuration Manager 可监视部署状态和 Microsoft Defender ATP 代理运行状况。 可在运行 Configuration Manager 客户端的电脑上或[由 Microsoft Intune 托管](/intune/protect/advanced-threat-protection)的电脑上使用 Microsoft Defender ATP。

## <a name="prerequisites"></a>必备条件

- Microsoft Defender 高级威胁防护联机服务的订阅  
- 运行 Configuration Manager 客户端的客户端计算机
- 使用以下[支持的客户端操作系统](#bkmk_os)部分中列出的 OS 的客户端。

### <a name="supported-client-operating-systems"></a><a name="bkmk_os"></a> 支持的客户端操作系统

根据所运行的 Configuration Manager 版本，可以加入以下客户端操作系统：

#### <a name="configuration-manager-version-1910-and-prior"></a>Configuration Manager 版本 1910 及更早版本

- 运行 Windows 10、版本 1607 及更高版本的客户端计算机

#### <a name="configuration-manager-version-2002-and-later"></a>Configuration Manager 版本 2002 及更高版本
<!--5229962-->
自 Configuration Manager 版本 2002 起，可以加入以下操作系统：

- Windows 8.1
- Windows 10 1607 或更高版本
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2016 版本 1803 或更高版本
- Windows Server 2019

## <a name="about-onboarding-to-atp-with-configuration-manager"></a>关于使用 Configuration Manager 加入 ATP

不同操作系统对于加入 ATP 有不同要求。 Windows 8.1 和其他下级操作系统设备需要“工作区密钥”和“工作区 ID”才可加入 。 诸如 Windows Server 版本 1803 等上级设备需要加入配置文件。 Configuration Manager 还会在加入的设备需要时安装 Microsoft Monitoring Agent (MMA)，但不会自动更新该代理。

上级操作系统包括：
- Windows 10 1607 版及更高版本
- Windows Server 2016 版本 1803 或更高版本
- Windows Server 2019

下级操作系统包括：
- Windows 8.1
- Windows Server 2012 R2
- Windows Server 2016 版本 1709 及更早版本

使用 Configuration Manager 将设备加入 ATP 时，会将 ATP 策略部署到目标集合或多个集合。 有时，目标集合包含的设备可运行任意数量的受支持操作系统。 根据目标集合是否包含运行上级和/或下级操作系统的设备，加入这些设备的说明有所不同。

- 如果目标集合同时包含上级和下级设备，请按照说明[加入运行任何受支持操作系统的设备](#bkmk_any_os)（推荐）。
- 如果集合仅包含上级设备，则可以使用[上级加入说明](#bkmk_uplevel)。
- 如果集合仅包含下级设备，则可以使用[下级加入说明](#bkmk_downlevel)。

> [!Warning]
> - 如果目标集合包含上级设备，而你使用针对下级设备的说明，则不会加入上级设备。
> - 如果目标集合包含下级设备，而你使用针对上级设备的说明，则不会加入下级设备。

## <a name="onboard-devices-with-any-supported-operating-system-to-atp-recommended"></a><a name="bkmk_any_os"></a>将运行任何受支持操作系统的设备加入 ATP（建议）
 可让通过向 Configuration Manager 提供配置文件、工作区密钥和工作区 ID，将运行任何[受支持操作系统](#bkmk_os)的设备加入 ATP 。

### <a name="get-the-configuration-file-workspace-id-and-workspace-key"></a>获取配置文件、工作区 ID 和工作区密钥

1. 转到 [Microsoft Defender ATP 联机服务](https://securitycenter.windows.com/)并登录。
1. 选择“设置”，然后在“设备管理”标题下选择“加入”  。
1. 对于操作系统，选择“Windows 10”。
1. 对于部署方法，选择“Microsoft Endpoint Configuration Manager 当前分支及更高版本”。
1. 单击“下载包”。
   
   :::image type="content" source="media/5229962-onboarding-configuration.png" alt-text="加入配置文件下载" lightbox="media/5229962-onboarding-configuration.png":::
1. 下载压缩的存档 (.zip) 文件并将内容解压缩。
1. 选择“设置”，然后在“设备管理”标题下选择“加入”  。
1. 对于操作系统，请从列表中选择“Windows 7 SP1 和 8.1”或“Windows Server 2008 R2 Sp1、2012 R2 和 2016” 。
   - 无论选择哪个选项，“工作区密钥”和“工作区 ID”都相同 。
1. 从“配置连接”部分复制“工作区密钥”和“工作区 ID”的值。  

   > [!IMPORTANT]
   > Microsoft Defender ATP 配置文件包含敏感信息，应保障其安全。


### <a name="onboard-the-devices"></a>加入设备

1. 在 Configuration Manager 控制台中，导航到“资产和符合性” > “Endpoint Protection” > “Microsoft Defender ATP 策略”  。
1. 选择“创建 Microsoft Defender ATP 策略”，打开“Microsoft Defender ATP 策略向导”。 
1. 键入 Microsoft Defender ATP 策略的名称和说明，然后选择“加入”  。
1. 浏览到从下载的 .zip 文件中提取的配置文件。
1. 提供“工作区密钥”和“工作区 ID”，然后单击“下一步”  。

   :::image type="content" source="media/5229962-create-atp-policy-wizard.png" alt-text="创建 Microsoft Defender ATP 策略向导" lightbox="media/5229962-create-atp-policy-wizard.png":::

1. 指定从托管设备收集和共享的文件示例以进行分析。  
   - **无**
   - **所有文件类型**  
1. 查看摘要，然后完成该向导。  
1. 右键单击创建的策略，然后选择“部署”，将 Microsoft Defender ATP 策略定向到客户端。

## <a name="onboard-devices-running-up-level-operating-systems-to-atp"></a><a name="bkmk_uplevel"></a>将运行上级操作系统的设备加入 ATP

上级客户端需要加入配置文件才能加入 ATP。 上级操作系统包括：
- Windows 10 1607 版及更高版本 
- Windows Server 2016 版本 1803 及更早版本
- Windows Server 2019

如果目标集合同时包含上级和下级设备，或你不确定其包含何种设备，请按照说明[加入运行任何受支持操作系统的设备](#bkmk_any_os)（推荐）。

### <a name="get-an-onboarding-configuration-file-for-up-level-devices"></a>获取适用于上级设备的加入配置文件

1. 转到 [Microsoft Defender ATP 联机服务](https://securitycenter.windows.com/)并登录。
1. 选择“设置”，然后在“设备管理”标题下选择“加入”  。
1. 对于操作系统，选择“Windows 10”。
1. 对于部署方法，选择“Microsoft Endpoint Configuration Manager 当前分支及更高版本”。
1. 单击“下载包”。
1. 下载压缩的存档 (.zip) 文件并将内容解压缩。

> [!IMPORTANT]
> Microsoft Defender ATP 配置文件包含敏感信息，应保障其安全。


### <a name="onboard-the-up-level-devices"></a>加入上级设备

1. 在 Configuration Manager 控制台中，导航到“资产和符合性” > “Endpoint Protection” > “Microsoft Defender ATP 策略”，然后选择“创建 Microsoft Defender ATP 策略”   。 Microsoft Defender ATP 策略向导将打开。  
1. 键入 Microsoft Defender ATP 策略的名称和说明，然后选择“加入”  。
1. 浏览到从下载的 .zip 文件中提取的配置文件。
   > [!Note]
   > 对于 Configuration Manager 版本 2002，即使你仅加入上级设备，也需要“工作区密钥”和“工作区 ID” 。 要获取这些至，请从 [Microsoft Defender ATP 联机服务](https://securitycenter.windows.com/)中选择“设置” > “加入” > “Windows 7 和 8.1”  。 <!--7054188-->
1. 指定从托管设备收集和共享的文件示例以进行分析。  
   - **无**
   - **所有文件类型**  
1. 查看摘要，然后完成该向导。  
1. 右键单击创建的策略，然后选择“部署”，将 Microsoft Defender ATP 策略定向到客户端。

## <a name="onboard-devices-running-down-level-operating-systems-to-atp"></a><a name="bkmk_downlevel"></a>将运行下级操作系统的设备加入 ATP

下级客户端需要“工作区密钥”和“工作区 ID”才可加入 ATP 。 下级操作系统包括：
- Windows 8.1
- Windows Server 2012 R2
- Windows Server 2016 版本 1709 及更早版本

如果目标集合同时包含上级和下级设备，或你不确定其包含何种设备，请按照说明[加入运行任何受支持操作系统的设备](#bkmk_any_os)（推荐）。

### <a name="get-the-workspace-id-and-workspace-key-for-down-level-devices"></a>获取下级设备的工作区 ID 和工作区密钥

1. 转到 [Microsoft Defender ATP 联机服务](https://securitycenter.windows.com/)并登录。
1. 选择“设置”，然后在“设备管理”标题下选择“加入”  。
1. 对于操作系统，请从列表中选择“Windows 7 SP1 和 8.1”或“Windows Server 2008 R2 Sp1、2012 R2 和 2016” 。
   - 无论选择哪个选项，“工作区密钥”和“工作区 ID”都相同 。
1. 从“配置连接”部分复制“工作区密钥”和“工作区 ID”的值。  

### <a name="onboard-the-down-level-devices"></a>加入下级设备

1. 在 Configuration Manager 控制台中，导航到“资产和符合性” > “Endpoint Protection” > “Microsoft Defender ATP 策略”，然后选择“创建 Microsoft Defender ATP 策略”   。 Microsoft Defender ATP 策略向导将打开。  
1. 键入 Microsoft Defender ATP 策略的名称和说明，然后选择“加入”  。
1. 提供“工作区密钥”和“工作区 ID” 。
   > [!Note]
   > - 对于 Configuration Manager 版本 2002，即使你仅加入下级设备，也需要配置文件。 要获取这些值，请从 [Microsoft Defender ATP 联机服务](https://securitycenter.windows.com/)中选择“设置” > “加入” > “Windows 10”  。 <!--7054188--> 
   > - Microsoft Defender ATP 配置文件包含敏感信息，应保障其安全。
1. 指定从托管设备收集和共享的文件示例以进行分析。  
   - **无**
   - **所有文件类型**  
1. 查看摘要，然后完成该向导。  
1. 右键单击创建的策略，然后选择“部署”，将 Microsoft Defender ATP 策略定向到客户端。


## <a name="monitor"></a>监视

1. 在 Configuration Manager 控制台中，导航到“监视” > “安全”，然后选择“Microsoft Defender ATP”  。  

1. 查看 Microsoft Defender 高级威胁防护仪表板。  

    - **Microsoft Defender ATP 代理载入状态**：已加入可用 Microsoft Defender ATP 策略的合格托管客户端计算机的数量和百分比  

    - **Microsoft Defender ATP 代理运行状况**：报告其 Microsoft Defender ATP 代理状态的计算机客户端的百分比  

        - **运行状况** - 运行正常  

        - **非活动** - 在时间段内没有数据发送到服务  

        - **代理状态** - Windows 中代理的系统服务未运行  

        - **未载入** - 策略已应用，但代理尚未报告已加入策略  

## <a name="create-an-offboarding-configuration-file"></a>创建载出配置文件  

1. 登录到 [Microsoft Defender ATP 联机服务](https://securitycenter.windows.com/)。
1. 选择“设置”，然后在“设备管理”标题下选择“脱离”  。
1. 对于操作系统，选择“Windows 10”，对于部署方法，选择“Microsoft Endpoint Configuration Manager 当前分支及更高版本” 。
   - 使用“Windows 10”选项，确保集合中的所有设备都已脱离，并在需要时卸载 MMA。
1. 下载压缩的存档 (.zip) 文件并将内容解压缩。 载出文件的有效期为 30 天。

1. 在 Configuration Manager 控制台中，导航到“资产和符合性” > “Endpoint Protection” > “Microsoft Defender ATP 策略”，然后选择“创建 Microsoft Defender ATP 策略”   。 Microsoft Defender ATP 策略向导将打开。  

1. 键入 Microsoft Defender ATP 策略的名称和说明，然后选择“登出”  。

1. 浏览到从下载的 .zip 文件中提取的配置文件。

1. 查看摘要，然后完成该向导。  

选择“部署”，将 Microsoft Defender ATP 策略定向到客户端。  

> [!IMPORTANT]
> Microsoft Defender ATP 配置文件包含敏感信息，应保障其安全。

## <a name="next-steps"></a>后续步骤

- [Microsoft Defender 高级威胁防护](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Microsoft Defender 高级威胁防护加入问题疑难解答](/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)