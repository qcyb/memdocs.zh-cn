---
title: 适用于 Linux 和 UNIX 的硬件清单
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中使用 Linux 和 UNIX 的硬件清单。
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1026d616-2a20-4fb2-8604-d331763937f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 84f4b822475111352c5dcf23f4868a1fa43ec3a7
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906274"
---
# <a name="hardware-inventory-for-linux-and-unix-in-configuration-manager"></a>Configuration Manager 中适用于 Linux 和 UNIX 的硬件清单

适用范围：  Configuration Manager (Current Branch)

> [!Important]  
> 从版本 1902 开始，Configuration Manager 不支持 Linux 或 UNIX 客户端。 
> 
> 请考虑使用 Microsoft Azure 管理来管理 Linux 服务器。 Azure 解决方案具有广泛的 Linux 支持（包括面向 Linux 的端到端补丁管理），在大多数情况下优于 Configuration Manager 的功能。

适用于 Linux 和 UNIX 的 Configuration Manager 客户端支持硬件清单。 收集硬件清单后，可在资源浏览器或 Configuration Manager 报表中运行查看清单，并可使用此信息来创建能够实现以下操作的查询和集合：  

- 软件部署  

- 强制维护时段  

- 部署自定义客户端设置  

适用于 Linux 和 UNIX 服务器的硬件清单使用基于标准的通用信息模型 (CIM) 服务器。 CIM 服务器作为软件服务（或后台程序）运行，并提供基于分布式管理任务组 (DMTF) 标准的管理基础结构。 CIM 服务器提供类似于在基于 Windows 的计算机上可用的 Windows Management Infrastructure (WMI) CIM 功能的功能。  

从累积更新 1 开始，适用于 Linux 和 UNIX 的客户端使用“开放组”的开放源代码 omiserver 版本 1.0.6   。 （在累积更新 1 之前，客户端使用 **nanowbem** 作为其 CIM 服务器）。  

CIM 服务器作为适用于 Linux 和 UNIX 的客户端的一部分安装。 适用于 Linux 和 UNIX 的客户端直接与 CIM 服务器进行通信，并且不使用 CIM 服务器的 WS-MAN 接口。 在客户端安装时，会禁用 CIM 服务器上的 WS-MAN 端口。 Microsoft 开发了 CIM 服务器，现已通过开放式管理基础结构 (OMI) 项目成为可用的开放源代码。 有关开放式管理基础结构项目的详细信息，请参阅 [开放组](https://www.opengroup.org/) 网站。  

Linux 和 UNIX 服务器上的硬件清单通过将现有 Win32 WMI 类和属性映射到 Linux 和 UNIX 服务器的等效类和属性实现运行。 这种类和属性的一对一映射使 Linux 和 UNIX 硬件清单能够与 Configuration Manager 集成。 Linux 和 UNIX 服务器的清单数据与 Configuration Manager 控制台和报表中基于 Windows 的计算机的清单一起显示。 此行为提供了一致的异构管理体验。  

> [!TIP]  
>  你可以使用“操作系统”  类的“标题”  值标识查询和集合中的不同 Linux 和 UNIX 操作系统。  

##  <a name="configuring-hardware-inventory-for-linux-and-unix-servers"></a><a name="BKMK_ConfigHardwareforLnU"></a> 配置适用于 Linux 和 UNIX 服务器的硬件清单  
 可以使用默认客户端设置或创建自定义客户端设备设置来配置硬件清单。 当使用自定义客户端设备设置时，可以配置你希望仅从你的 Linux 和 UNIX 服务器中收集的类和属性。 还可以指定自定义计划确定何时从你的 Linux 和 UNIX 服务器中收集完整清单和增量清单。  

 适用于 Linux 和 UNIX 的客户端支持以下在 Linux 和 UNIX 服务器上可用的硬件清单类：  

- Win32_BIOS  

- Win32_ComputerSystem  

- Win32_DiskDrive  

- Win32_DiskPartition  

- Win32_NetworkAdapter  

- Win32_NetworkAdapterConfiguration  

- Win32_OperatingSystem  

- Win32_Process  

- Win32_Service  

- Win32Reg_AddRemovePrograms  

- SMS_LogicalDisk  

- SMS_Processor  

并非这些清单类的所有属性都在 Configuration Manager 中的 Linux 和 UNIX 计算机上启用。  

##  <a name="operations-for-hardware-inventory"></a><a name="BKMK_OperationsforHardwareforLnU"></a> 硬件清单的操作  
 从你的 Linux 和 UNIX 服务器上收集硬件清单后，可以使用与查看收集自其它计算机的清单一样的方式查看和使用此信息：  

- 使用资源浏览器查看有关 Linux 和 UNIX 服务器硬件清单的详细信息  

- 基于特定的硬件配置创建查询  

- 创建基于特定硬件配置的基于查询的集合  

- 运行显示硬件配置的特定详细信息的报表  

Linux 或 UNIX 服务器上的硬件清单会根据客户端设置中配置的计划运行。 默认情况下，此计划为每七天运行一次。 适用于 Linux 和 UNIX 的客户端支持的完整清单周期和增量清单周期。  

也可以强制 Linux 或 UNIX 服务器上的客户端立即运行硬件清单。 若要运行硬件清单，在客户端上使用“根”  凭据运行以下命令以启动硬件清单周期：`/opt/microsoft/configmgr/bin/ccmexec -rs hinv`  

针对硬件清单的操作会输入到客户端日志文件，“scxcm.log”  。  

##  <a name="how-to-use-open-management-infrastructure-to-create-custom-hardware-inventory"></a><a name="BKMK_CustomHINVforLinux"></a> 如何使用开放式管理基础结构来创建自定义硬件清单  
 适用于 Linux 和 UNIX 的客户端支持可以使用开放式管理基础结构 (OMI) 创建的自定义硬件清单。 若要完成此操作，可以使用下列步骤：  

1.  通过使用 OMI 源创建自定义清单提供程序  

2.  将计算机配置为可使用新的提供程序报告清单  

3.  使 Configuration Manager 支持新的提供程序  

###  <a name="create-a-custom-hardware-inventory-provider-for-linux-and-unix-computers"></a><a name="BKMK_LinuxProvider"></a> 创建适用于 Linux 和 UNIX 计算机的自定义硬件清单提供程序。  
 若要创建适用于 Linux 和 UNIX 的 Configuration Manager 客户端的自定义硬件清单提供程序，请使用 **OMI 源-v.1.0.6** 并按照 OMI 入门指南中的说明进行操作。 此过程包括创建托管对象格式 (MOF) 文件，该文件用于定义新提供程序的架构。 随后，将 MOF 文件导入 Configuration Manager 以支持新自定义清单类。  

 OMI 源-v.1.0.6 和 OMI 入门指南均可以从 [开放组](https://github.com/microsoft/omi/blob/master/README.md) 网站下载。 可以在 OpenGroup.org 网站上的以下网页中的“文档”选项卡上找到这些下载内容  ：[开放式管理基础结构 (OMI)](https://collaboration.opengroup.org/omi/)。  

###  <a name="configure-each-computer-that-runs-linux-or-unix-with-the-custom-hardware-inventory-provider"></a><a name="BKMK_AddProvidertoLinux"></a> 使用自定义硬件清单提供程序对每个运行 Linux 或 UNIX 的计算机进行配置：  
 创建自定义清单提供程序后，必须在具有你想收集的清单的每个计算机上复制并注册提供程序库文件。  

1.  将提供程序库复制到想要从中收集清单的每个 Linux 和 UNIX 计算机。 提供程序库的名称类似于以下名称：**XYZ_MyProvider.so**  

2.  接下来，在每台 Linux 和 UNIX 计算机上，向 OMI 服务器注册提供程序库。 当安装适用于 Linux 和 UNIX 的 Configuration Manager 客户端时，OMI 服务器会安装在计算机上，但必须手动注册自定义提供程序。 使用以下命令行来注册提供程序：`/opt/microsoft/omi/bin/omireg XYZ_MyProvider.so`  

3.  注册新提供程序后，使用 **omicli** 工具测试提供程序。 安装适用于 Linux 和 UNIX 的 Configuration Manager 客户端时， **omicli** 工具会安装在每台 Linux 和 UNIX 计算机上。 例如，当创建的提供程序的名称是 **XYZ_MyProvider** 时，则在计算机上运行后列命令： **/opt/microsoft/omi/bin/omicli ei root/cimv2 XYZ_MyProvider**  

     关于 **omicli** 和测试自定义提供程序的信息，请参阅 OMI 入门指南。  

> [!TIP]  
>  若要部署自定义提供程序，以及如何注册每个 Linux 和 UNIX 的客户端计算机上的自定义提供程序使用软件分发。  

###  <a name="enable-the-new-inventory-class-in-configuration-manager"></a><a name="BKMK_AddLinuxProvidertoCM"></a> 在 Configuration Manager 中启用新清单类：  
 必须首先导入用于定义自定义提供程序架构的托管对象格式 (MOF) 文件，Configuration Manager 才可以报告由 Linux 和 UNIX 计算机上的新提供程序报告的清单。  

 若要将自定义 MOF 文件导入 Configuration Manager，请参阅[如何配置硬件清单](../../../../core/clients/manage/inventory/configure-hardware-inventory.md)。  
