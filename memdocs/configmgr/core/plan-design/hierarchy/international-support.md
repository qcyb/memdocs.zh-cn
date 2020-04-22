---
title: 国际支持
titleSuffix: Configuration Manager
description: 配置 Configuration Manager 以符合特定的国际要求。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05e90466ec3ee9529e4eb770839347ad7ac94447
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704595"
---
# <a name="international-support-in-configuration-manager"></a>Configuration Manager 中的国际支持

适用范围：  Configuration Manager (Current Branch)

以下部分提供技术详细信息，帮助使 Configuration Manager 符合特定的国际要求。  

## <a name="gb18030-requirements"></a>GB18030 要求  
 Configuration Manager 符合在 GB18030 中定义的标准，因此，可以在中国使用 Configuration Manager。 Configuration Manager 部署必须具有下列配置才能符合 GB18030 要求：  

-   与 Configuration Manager 一起使用的每台站点服务器计算机和 SQL Server 计算机都必须使用中文操作系统。  

-   层次结构中的每个站点数据库和 SQL Server 的每个实例都必须使用相同的排序规则，而且必须是下列排序规则之一：  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  对于[对 Configuration Manager 的 SQL Server 版本的支持](../../../core/plan-design/configs/support-for-sql-server-versions.md)中所述的要求，这些数据库排序规则是一个例外。  

-   必须将名为 **GB18030.SMS** 的文件放在层次结构中的每台站点服务器计算机的系统卷根文件夹下。 此文件不包含任何数据，而且可能是按照此要求命名的空白文本文件。  
