---
title: 迁移安全和隐私
titleSuffix: Configuration Manager
description: 获取迁移到 Configuration Manager Current Branch 环境的最佳安全做法和隐私信息。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6893fce1-7ad5-4151-9ba9-3096871e8e4a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ad92e4906c45b5c720ab35efc055449a27cc0850
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906216"
---
# <a name="security-and-privacy-for-migration-to-configuration-manager-current-branch"></a>迁移到 Configuration Manager Current Branch 的安全和隐私

适用范围：  Configuration Manager (Current Branch)

本主题包含迁移到 Configuration Manager Current Branch 环境的最佳安全做法和隐私信息。  

## <a name="security-best-practices-for-migration"></a>迁移的最佳安全方案  
 使用下列最佳安全方案进行迁移。  

|最佳安全方案|更多信息|  
|----------------------------|----------------------|  
|使用计算机帐户作为源站点 SMS 提供程序帐户和源站点 SQL Server 帐户，而不是使用用户帐户。|如果必须使用用户帐户进行迁移，请在完成迁移后删除帐户详细信息。|  
|将内容从源站点中的分发点迁移到目标站点中的分发点时，请使用 IPsec。|虽然会对迁移的内容进行哈希处理以检测篡改，但如果在传输过程中修改了数据，则迁移将失败。|  
|限制和监视可以创建迁移作业的管理用户。|目标层次结构的数据库完整性取决于管理用户选择从源层次结构中导入的数据的完整性。 此外，此管理用户可以读取源层次结构中的所有数据。|  

### <a name="security-issues-for-migration"></a>迁移的安全问题  
迁移具有以下安全问题：  

-   在迁移从源站点中阻止的客户端的记录之前，这些客户端或许能够成功地分配给目标层次结构。  

     虽然 Configuration Manager 会保留迁移的客户端的阻止状态，但如果在完成客户端记录迁移之前进行分配，则客户端可以成功地分配给目标层次结构。  

-   将不迁移审核消息。  

将数据从源站点迁移到目标站点时，会丢失源层次结构中的任何审核信息。  

## <a name="privacy-information-for-migration"></a>迁移的隐私信息  
 迁移会从站点数据库中发现你在来源基础结构中标识的信息，并将此数据存储到目标层次结构内的数据库中。 Configuration Manager 可从源站点或层次结构中发现的信息取决于在源环境中启用的功能，以及在该源环境中执行的管理操作。  

 有关安全和隐私信息的详细信息，请参阅下列主题之一：  

-   有关 Configuration Manager 2007 隐私信息的详细信息，请参阅 Configuration Manager 2007 文档库中的[ Configuration Manager 2007 安全性和隐私](https://docs.microsoft.com/previous-versions/system-center/configuration-manager-2007/bb680768(v=technet.10))。  

-   有关 System Center 2012 Configuration Manager 隐私信息的详细信息，请参阅 System Center 2012 Configuration Manager 文档库中的 [System Center 2012 Configuration Manager 安全性和隐私](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/gg682033(v=technet.10))。  

-   有关 Configuration Manager 的隐私信息的详细信息，请参阅 [Configuration Manager 的安全和隐私](../../core/plan-design/security/security-and-privacy.md)。  

你可以从源站点中将部分或全部支持数据迁移到目标层次结构。  

迁移默认情况下未启用并且需要一些配置步骤。 迁移信息不会发送给 Microsoft。  

从源层次结构中迁移数据之前，请考虑隐私要求。  
