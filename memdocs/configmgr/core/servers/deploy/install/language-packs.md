---
title: 语言包
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中可用的语言支持。
ms.date: 06/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2f07f1277a9e87ea3266473fc54dc96907a0f0e6
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698967"
---
# <a name="language-packs-in-configuration-manager"></a>Configuration Manager 中的语言包

适用范围：  Configuration Manager (Current Branch)

本文提供有关 Configuration Manager 中的语言支持的技术详细信息。 Configuration Manager 站点服务器和客户端被认为语言中性。 通过在管理中心站点和主站点中安装服务器语言包  或客户端语言包  ，添加对显示语言的支持。 在站点安装过程中，从可用的语言包文件中选择要在该站点支持的服务器和客户端语言。
 
在每个站点安装多种语言。 你只需要安装使用的语言。  

- 每个站点都支持多种 Configuration Manager 控制台语言。  

- 通过在每个站点安装单个客户端语言包，添加对你想要支持的客户端语言的支持。  

安装对匹配以下组件的语言的支持时：  

- 计算机的显示语言：在该计算机上运行的 Configuration Manager 控制台和客户端用户界面都以该语言显示信息。  

- 计算机的 Web 浏览器正在使用的语言首选项：基于 Web 的信息的连接（包括应用程序目录或 SQL Server Reporting Services）将以该语言显示。  


运行 Configuration Manager 安装程序时，会作为先决条件和可再发行文件的一部分下载语言包文件。 在运行安装程序之前，你还可以使用[安装下载程序](setup-downloader.md)来下载这些文件。   



## <a name="server-languages"></a>服务器语言  

使用下表将区域设置 ID 对应到你要在服务器上支持的语言。 有关区域设置 ID 的详细信息，请参阅 [Microsoft 指定的区域设置 ID](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)。  

|服务器语言|区域设置 ID (LCID)|3 个字母的代码|  
|---------------------|------------------------|-----------------------|  
|英语（默认）|0409|ENU|  
|中文（简体）|0804|CHS|  
|中文（繁体，台湾）|0404|CHT|  
|捷克语|0405|CSY|  
|荷兰语 - 荷兰|0413|NLD|  
|法语|040c|FRA|  
|德语|0407|DEU|  
|匈牙利语|040e|HUN|  
|意大利语 - 意大利|0410|ITA|  
|日语|0411|JPN|  
|朝鲜语|0412|KOR|  
|波兰语|0415|PLK|  
|葡萄牙语 - 巴西|0416|PTB|  
|葡萄牙语 - 葡萄牙|0816|PTG|  
|俄语|0419|RUS|  
|西班牙语 - 西班牙|0c0a|ESN|  
|瑞典语|041d|SVE|  
|土耳其语|041f|TRK|  



## <a name="client-languages"></a>客户端语言  

使用下表将区域设置 ID 对应到你要在客户端计算机上支持的语言。 有关区域设置 ID 的详细信息，请参阅 [Microsoft 指定的区域设置 ID](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)。  

|客户端语言|区域设置 ID (LCID)|3 个字母的代码|  
|---------------------|------------------------|-----------------------|  
|英语（默认）|0409|CHS|  
|中文 - 简体|0804|CHS|  
|中文（繁体，台湾）|0404|CHT|  
|捷克语|0405|CSY|  
|丹麦语|0406|DAN|  
|荷兰语 - 荷兰|0413|NLD|  
|芬兰语|040b|FIN|  
|法语|040c|FRA|  
|德语|0407|DEU|  
|希腊语|0408|ELL|  
|匈牙利语|040e|HUN|  
|意大利语 - 意大利|0410|ITA|  
|日语|0411|JPN|  
|朝鲜语|0412|KOR|  
|挪威语|0414|NOR|  
|波兰语|0415|PLK|  
|葡萄牙语（巴西）|0416|PTB|  
|葡萄牙语（葡萄牙）|0816|PTG|  
|俄语|0419|RUS|  
|西班牙语 - 西班牙|0c0a|ESN|  
|瑞典语|041d|SVE|  
|土耳其语|041f|TRK|  


### <a name="mobile-device-client-languages"></a>移动设备客户端语言  
添加对移动设备语言的支持时，会将所有支持的移动设备客户端语言都包括在内。 对于移动设备支持，你无法选择单个语言包。  



## <a name="identify-installed-language-packs"></a>识别已安装的语言包  
若要识别在运行 Configuration Manager 客户端的计算机上安装的语言包，请在该计算机的注册表中查找已安装语言包的区域设置 ID (LCID)。 此信息位于以下注册表路径：  

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs`  

自定义硬件清单以收集此信息。 然后构建自定义报表，以查看语言详情。 有关收集自定义硬件清单的详细信息，请参阅[如何配置硬件清单](../../../clients/manage/inventory/configure-hardware-inventory.md)。 有关详细信息，请参阅[创建报表](../../manage/operations-and-maintenance-for-reporting.md#create-reports)。