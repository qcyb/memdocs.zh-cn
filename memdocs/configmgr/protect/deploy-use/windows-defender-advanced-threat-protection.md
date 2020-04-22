---
title: Microsoft Defender 高级威胁防护
titleSuffix: Configuration Manager
description: 了解如何管理和监视 Microsofts Defender 高级威胁防护 - 这是一项可帮助企业应对高级安全攻击的新服务。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a5fc033e-828e-4e45-9097-bbbd0697ebdf
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 186751bb8b1768b34573e2b614ce992b58fa9232
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706235"
---
# <a name="microsoft-defender-advanced-threat-protection"></a>Microsoft Defender 高级威胁防护

适用范围：  Configuration Manager (Current Branch)

Endpoint Protection 可帮助管理和监视 [Microsoft Defender 高级威胁防护 (ATP)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)（之前称为 Windows Defender ATP）。 Microsoft Defender ATP 可帮助企业检测和调查其网络上的高级攻击并作出应对。 Configuration Manager 策略可帮助加入和监视 Windows 10 客户端。

Microsoft Defender ATP 是 [Windows Defender 安全中心](https://securitycenter.windows.com)提供的一项服务。 通过添加和部署客户端加入配置文件，Configuration Manager 可监视部署状态和 Microsoft Defender ATP 代理运行状况。 可在运行 Configuration Manager 客户端的电脑上或[由 Microsoft Intune 托管](https://docs.microsoft.com/intune/protect/advanced-threat-protection)的电脑上使用 Microsoft Defender ATP。

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
- Windows 7 SP1
- Windows 8.1
- Windows 10 1607 或更高版本
- Windows Server 2008 R2 SP1
- Windows Server 2012 R2
- Windows Server 2016
- Windows Server 2016 版本 1803
- Windows Server 2019

## <a name="create-an-onboarding-configuration-file"></a>创建加入配置文件

1. 转到 [Microsoft Defender ATP 联机服务](https://securitycenter.windows.com/)并登录。
1. 在“设置”下选择“计算机管理”，然后选择“加入”    。
1. 从列表中选择要加入的操作系统。
   - 如果要加入 Windows 10、Windows Server 1803 和 Windows Server 2019：
      1. 请选择“Configuration Manager (Current Branch) 版本 1606”，然后选择“下载包”   。
      1. 下载压缩的存档 (.zip) 文件并将内容解压缩。
   - 如果要加入另一个 Windows 操作系统： 
      1. 从列表中选择要加入的操作系统。 可选择“Windows 7 和 8.1”或“Windows Server 2008 R2 SP1、2012 R2 和 2016”   。
      1. 完成此过程后，从“配置连接”部分复制“工作区密钥”和“工作区 ID”。   

> [!IMPORTANT]
> Microsoft Defender ATP 配置文件包含敏感信息，应保障其安全。

## <a name="onboard-devices"></a>加入设备

1. 在 Configuration Manager 控制台中，导航到“资产和符合性” > “Endpoint Protection” > “Windows Defender ATP 策略”，然后选择“创建 Windows Defender ATP 策略”     。 Microsoft Defender ATP 策略向导将打开。  
1. 键入 Microsoft Defender ATP 策略的名称和说明，然后选择“加入”    。
1. 浏览到组织的 Microsoft Defender ATP 云服务租户提供的配置文件  。
   - 对于“Windows 7 和 8.1”或“Windows Server 2008 R2 SP1、2012 R2 和 2016”，请提供“工作区密钥”和“工作区 ID”     。
1. 指定从托管设备收集和共享的文件示例以进行分析。  

   - **无**

   - **所有文件类型**  
1. 查看摘要，然后完成该向导。  

选择“部署”，将 Microsoft Defender ATP 策略定向到客户端  。

## <a name="monitor"></a>监视

1. 在 Configuration Manager 控制台中，导航到“监视” > “安全”，然后选择“Windows Defender ATP”    。  

1. 查看 Microsoft Defender 高级威胁防护仪表板。  

    - **Windows Defender 代理部署状态**：已加入可用 Microsoft Defender ATP 策略的合格托管客户端计算机的数量和百分比  

    - **Windows Defender ATP 代理运行状况**：报告其 Microsoft Defender ATP 代理状态的计算机客户端的百分比  

        - **运行状况** - 运行正常  

        - **非活动** - 在时间段内没有数据发送到服务  

        - **代理状态** - Windows 中代理的系统服务未运行  

        - **未载入** - 策略已应用，但代理尚未报告已加入策略  

## <a name="create-an-offboarding-configuration-file"></a>创建载出配置文件  

1. 登录到 [Microsoft Defender ATP 联机服务](https://securitycenter.windows.com/)。

1. 在“设置”下选择“计算机管理”，然后选择“加入”    。  

1. 选择“Configuration Manager (Current Branch) 版本 1606”，然后选择“终结点载出”   。  

1. 下载压缩的存档 (.zip) 文件并将内容解压缩。 载出文件的有效期为 30 天。

1. 在 Configuration Manager 控制台中，导航到“资产和符合性” > “Endpoint Protection” > “Windows Defender ATP 策略”，然后选择“创建 Windows Defender ATP 策略”     。 Microsoft Defender ATP 策略向导将打开。  

1. 键入 Microsoft Defender ATP 策略的名称和说明，然后选择“登出”    。

1. 浏览到组织的 Microsoft Defender ATP 云服务租户提供的配置文件  。

1. 查看摘要，然后完成该向导。  

选择“部署”，将 Microsoft Defender ATP 策略定向到客户端  。  

> [!IMPORTANT]
> Microsoft Defender ATP 配置文件包含敏感信息，应保障其安全。

## <a name="next-steps"></a>后续步骤

- [Microsoft Defender 高级威胁防护](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)

- [Microsoft Defender 高级威胁防护加入问题疑难解答](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/troubleshoot-onboarding)
