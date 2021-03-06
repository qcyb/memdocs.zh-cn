---
title: 管理 Linux 和 UNIX 客户端
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中管理 Linux 和 UNIX 服务器上的客户端。
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 716441bd146e9172b3f183c497fcaa4036ad0084
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690045"
---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-configuration-manager"></a>如何在 Configuration Manager 中管理 Linux 和 UNIX 服务器上的客户端

适用范围：Configuration Manager (Current Branch)

> [!Important]  
> 从版本 1902 开始，Configuration Manager 不支持 Linux 或 UNIX 客户端。 
> 
> 请考虑使用 Microsoft Azure 管理来管理 Linux 服务器。 Azure 解决方案具有广泛的 Linux 支持（包括面向 Linux 的端到端补丁管理），在大多数情况下优于 Configuration Manager 的功能。

使用 Configuration Manager 管理 Linux 和 UNIX 服务器时，可以配置集合、维护时段和客户端设置，以帮助管理服务器。 此外，尽管适用于 Linux 和 UNIX 的 Configuration Manager 客户端没有用户界面，但可以强制客户端手动轮询客户端策略。

##  <a name="collections-of-linux-and-unix-servers"></a><a name="BKMK_CollectionsforLnU"></a> Linux 和 UNIX 服务器的集合  
 使用集合管理 Linux 和 UNIX 服务器组的方式与使用集合管理其他客户端类型的方式相同。 集合可以是直接成员身份集合，也可以是基于查询的集合。 基于查询的集合用于确定客户端操作系统、硬件配置或有关站点数据库中存储的客户端的其他详细信息。 例如，你可以使用包括 Linux 和 UNIX 服务器的集合来管理下列设置：  

- 客户端设置  

- 软件部署  

- 强制维护时段  

  必须先从客户端收集[硬件清单](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md)，然后才可通过客户端操作系统或分发来标识 Linux 或 UNIX 客户端。  

  硬件清单的默认客户端设置包括有关客户端计算机的操作系统的信息。 你可以使用 **Operating System** 类的 **Caption** 属性来标识 Linux 或 UNIX 服务器的操作系统。  

  在 Configuration Manager 控制台的“资产和符合性”工作区中的“设备”节点下，可查看有关运行 Linux 和 UNIX 的 Configuration Manager 客户端的计算机的详细信息。 在 Configuration Manager 控制台的“资产和符合性”工作区中，可在“操作系统”列中查看每台计算机的操作系统名称。  

  默认情况下，Linux 和 UNIX 服务器属于 **所有系统** 集合的成员。 建议生成仅包括 Linux 和 UNIX 服务器或其子集的自定义集合。 通过自定义集合，可管理向诸如计算机组部署软件或分配客户端设置等操作，以便准确衡量部署是否成功。   

  在为 Linux 和 UNIX 服务器生成自定义集合时，请包含成员身份规则查询，并在这些查询中包括操作系统特性的 Caption 特性。 有关创建集合的信息，请参阅[如何创建集合](../../../core/clients/manage/collections/create-collections.md)。  

##  <a name="maintenance-windows-for-linux-and-unix-servers"></a><a name="BKMK_MaintenanceWindowsforLnU"></a> Linux 和 UNIX 服务器的维护时段  
 Linux 和 UNIX 服务器的 Configuration Manager 客户端支持使用[维护时段](../../../core/clients/manage/collections/use-maintenance-windows.md)。 与对基于 Windows 的客户端的支持相比，此支持并无变化。  

##  <a name="client-settings-for-linux-and-unix-servers"></a><a name="BKMK_ClientSettingsforLnU"></a> Linux 和 UNIX 服务器的客户端设置  
 可使用与配置其他客户端设置相同的方式配置适用于 Linux 和 UNIX 服务器的[客户端设置](../../../core/clients/deploy/configure-client-settings.md)。  

 默认情况下， **默认客户端代理设置** 适用于 Linux 和 UNIX 服务器。 还可以创建自定义客户端设置，并将其部署到特定客户端的集合中。  

 没有仅适用于 Linux 和 UNIX 客户端的其他客户端设置。 但是，有不适用于 Linux 和 UNIX 的客户端的默认客户端设置。 Linux 和 UNIX 客户端仅应用所支持功能的设置。  

 例如，Linux 和 UNIX 服务器会忽略启用并配置了远程控制设置的自定义客户端设备设置，因为 Linux 和 UNIX 客户端不支持远程控制。  

##  <a name="computer-policy-for-linux-and-unix-servers"></a><a name="BKMK_PolicyforLnU"></a> Linux 和 UNIX 服务器的计算机策略  
 Linux 和 UNIX 服务器的客户端定期轮询其站点中的计算机策略，以了解请求的配置，并检查部署。  

 也可以强制 Linux 或 UNIX 服务器的客户端立即轮询计算机策略。 为此，请使用服务器上的**根**凭据运行以下命令： **/opt/microsoft/configmgr/bin/ccmexec -rs policy**  

 有关计算机策略轮询的详细信息包含在共享的客户端日志文件 **scxcm.log**中。  

> [!NOTE]  
>  Linux 和 UNIX 的 Configuration Manager 客户端从不请求或处理用户策略。  

##  <a name="how-to-manage-certificates-on-the-client-for-linux-and-unix"></a><a name="BKMK_ManageLinuxCerts"></a> 如何管理适用于 Linux 和 UNIX 的客户端上的证书  
 安装适用于 Linux 和 UNIX 的客户端后，你可以使用 **certutil** 工具来更新包含新 PKI 证书的客户端，并导入新的证书吊销列表 (CRL)。 安装适用于 Linux 和 UNIX 的客户端时，此工具位于 `/opt/microsoft/configmgr/bin/certutil` 中。 

 若要管理证书，请使用以下选项之一在每个客户端上运行 certutil：  

|选项|更多信息|  
|------------|----------------------|  
|`importPFX`|使用此选项可指定证书，以替换客户端当前使用的证书。<br /><br /> 使用 `-importPFX` 时，还必须使用 `-password` 命令行参数来提供与 PKCS#12 文件关联的密码。<br /><br /> 使用 `-rootcerts` 可指定任何其他根证书要求。<br /><br /> 示例：`certutil -importPFX <path to the PKCS#12 certificate> -password <certificate password> [-rootcerts <comma-separated list of certificates>]`|  
|`importsitecert`|使用此选项可更新管理服务器上的站点服务器签名证书。<br /><br /> 示例：`certutil -importsitecert <path to the DER certificate>`|  
|`importcrl`|使用此选项可通过一个或多个 CRL 文件路径更新客户端上的 CRL。<br /><br /> 示例：`certutil -importcrl <comma separated CRL file paths>`|  
