---
title: cmdlet 隐私声明
titleSuffix: Configuration Manager
description: 了解 Microsoft 如何收集和使用与 Configuration Manager cmdlet 相关的数据
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bec00fb4-1ac0-4e49-b330-0871b3722459
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 551a8086894f877d07c57fbe2848c2befacfc5b5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695745"
---
# <a name="configuration-manager-cmdlet-library-privacy-statement"></a>Configuration Manager Cmdlet 库隐私声明

适用范围：  Configuration Manager (Current Branch)

本隐私声明涵盖 Configuration Manager Cmdlet 库的功能。  

## <a name="usage-data"></a>使用情况数据  

#### <a name="what-this-feature-does"></a>此功能的作用

Configuration Manager cmdlet 库允许通过 Windows PowerShell cmdlet 和脚本来管理 Configuration Manager 层次结构。 Cmdlet 库收集有关如何使用库中的 cmdlet 来确定趋势和使用模式的信息。 Cmdlet 库还收集使用 cmdlet 时收到的错误类型和数目信息。  

#### <a name="information-collected-processed-or-transmitted"></a>收集、处理或传输的信息
   
收集的使用情况数据包括 cmdlet 的启动、停止和终止数据，弃用的 cmdlet 的运行数据，以及与这些 cmdlet 相关的 SMS 提供程序操作的活动指标。 此类信息不能确定个人身份。 收集的错误信息包括 cmdlet 返回的错误以及异常错误的详情。 某些错误详情报告可能无意中包含个人身份标识符，如连接到计算机的设备的序列号。 Cmdlet 库筛选并匿名化错误报告中的信息，以删除个人身份标识符，然后再将错误报告发送给 Microsoft。  

#### <a name="use-of-information"></a>使用信息
   
Microsoft 利用此信息来提高所提供产品和服务的质量、安全性和完整性。  

#### <a name="choicecontrol"></a>选择/控制   

此“使用数据”功能默认处于启用状态。 Configuration Manager cmdlet 库具有控制此功能的两个注册表项。  

 若要完全退出，请设置这两个注册表项的值。 每个值针对一个 Windows 事件跟踪 (ETW) 提供程序：  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Provider:CeipLevel=0（驱动器提供程序“使用情况数据”功能的退出）  

- HKLM\Software\Microsoft\ConfigMgr10\PowerShell\Microsoft.ConfigurationManagement.PowerShell.Cmdlets:CeipLevel=0（cmdlet“使用情况数据”功能的退出）  

  “使用情况数据”设置的更改特定于在其中进行更改的计算机。  


## <a name="next-steps"></a>后续步骤

[Configuration Manager Cmdlet 库文档](https://docs.microsoft.com/powershell/sccm/configurationmanager/)。   
