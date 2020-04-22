---
title: UNIX/Linux 客户端组件服务和命令
titleSuffix: Configuration Manager
description: 了解 Configuration Manager 中 Linux 和 UNIX 客户端的组件服务和命令。
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e5a8c79f-5791-49c5-8055-086d742e5559
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de564595ce51a336b5f11d4050928fa812269601
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693885"
---
# <a name="linux-and-unix-clients-component-services-and-commands-for-configuration-manager"></a>Configuration Manager 的 Linux 和 UNIX 客户端组件服务和命令

适用范围：  Configuration Manager (Current Branch)

> [!Important]  
> 从版本 1902 开始，Configuration Manager 不支持 Linux 或 UNIX 客户端。 
> 
> 请考虑使用 Microsoft Azure 管理来管理 Linux 服务器。 Azure 解决方案具有广泛的 Linux 支持（包括面向 Linux 的端到端补丁管理），在大多数情况下优于 Configuration Manager 的功能。


 下表标识了适用于 Linux 和 UNIX 的 Configuration Manager 客户端的客户端组件服务。  

|文件名|更多信息|  
|---------------|----------------------|  
|ccmexec.bin|此服务类似于基于 Windows 的客户端上的 ccmexc 服务。 它负责与 Configuration Manager 站点系统角色的所有通信，并且还可与 omiserver.bin 服务通信，以便从本地计算机收集硬件清单。<br /><br /> 有关支持的命令行参数的列表，请运行 `ccmexec -h`|  
|omiserver.bin|此服务是 CIM 服务器。 CIM 服务器为被称为提供程序的可插拔软件模块提供框架。 提供程序与 Linux 和 UNIX 计算机资源进行交互，并且收集硬件清单数据。 例如， **进程内提供程序** Linux 计算机收集与 Linux 操作系统进程关联的数据。|  

 以下表列表命令可用于启动、 停止或重新启动上每个版本的 Linux 或 UNIX 的客户端服务 (ccmexec.bin 和 omiserver.bin)。 在启动或停止 ccmexec 服务时，omiserver 服务也会启动或停止。  

|操作系统|命令|  
|----------------------|--------------|  
|通用代理<br /><br /> RHEL 4 和 SLES 9|启动：`/etc/init d/ccmexecd start`<br /><br /> 停止：`/etc/init d/ccmexecd stop`<br /><br /> 重启：`/etc/init d/ccmexecd restart`|  
|Solaris 9|启动：`/etc/init d/ccmexecd start`<br /><br /> 停止：`/etc/init d/ccmexecd stop`<br /><br /> 重启：`/etc/init d/ccmexecd restart`|  
|Solaris 10|启动：<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> 停止：<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|Solaris 11|启动：<br /><br /> `svcadm enable -s svc:/application/management/omiserver`<br /><br /> `svcadm enable -s svc:/application/management/ccmexecd`<br /><br /> 停止：<br /><br /> `svcadm disable -s svc:/application/management/ccmexecd`<br /><br /> `svcadm disable -s svc:/application/management/omiserver`|  
|AIX|启动：<br /><br /> `startsrc -s omiserver`<br /><br /> `startsrc -s ccmexec`<br /><br /> 停止：<br /><br /> `stopsrc -s ccmexec`<br /><br /> `stopsrc -s omiserver`|  
|HP-UX|启动：`/sbin/init.d/ccmexecd start`<br /><br /> 停止：`/sbin/init.d/ccmexecd stop`<br /><br /> 重启：`/sbin/init.d/ccmexecd restart`|  
