---
title: 集合安全和隐私
titleSuffix: Configuration Manager
description: 获取 Configuration Manager 中集合的最佳安全做法和隐私。
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 30bf2451-5415-4be2-ba8d-21759370cd83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 42345ee91baaad7dcc82eab537fbeb697d6cd7ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695525"
---
# <a name="security-and-privacy-for-collections-in-configuration-manager"></a>Configuration Manager 中集合的安全和隐私

适用范围：  Configuration Manager (Current Branch)

本主题包含 Configuration Manager 中集合的最佳安全做法和隐私信息。  

 没有专门针对 Configuration Manager 中的集合的隐私信息。 集合是资源（如用户和设备）的容器。 集合成员身份通常依赖于 Configuration Manager 在标准操作过程中收集的信息。 例如，通过使用从发现或清单收集的资源信息，可以将集合配置为包含满足指定条件的设备。 集合还可以基于客户端管理操作的当前状态信息，例如正在部署软件和正在检查符合性。 除了这些基于查询的集合，管理用户也可以将资源添加到集合。  

 有关集合的详细信息，请参阅[集合简介](../../../../core/clients/manage/collections/introduction-to-collections.md)。 有关 Configuration Manager 操作（可用于配置集合成员身份）的任何最佳安全做法和隐私信息的详情，请参阅 [Configuration Manager 的最佳安全做法和隐私信息](../../../../core/plan-design/security/security-best-practices-and-privacy-information.md)。  

## <a name="security-best-practices-for-collections"></a>集合的最佳安全方案  
 可将以下最佳安全方案用于集合。  

|最佳安全方案|更多信息|  
|----------------------------|----------------------|  
|当你使用保存到网络位置的托管对象格式 (MOF) 文件导出或导入集合时，请保护该位置和网络通道的安全。|限制可访问网络文件夹的人员。<br /><br /> 在网络位置与站点服务器之间使用服务器消息块 (SMB) 签名或 Internet 协议安全性 (IPsec)，以防止攻击者篡改导出的集合数据。 使用 IPsec 对网络上的数据进行加密以防止信息泄漏。|  

### <a name="security-issues-for-collections"></a>集合的安全问题  
 集合具有以下安全问题：  

-   如果使用集合变量，本地管理员可以读取可能敏感的信息。  

     在部署操作系统时，可以使用集合变量。  
