---
title: 电源管理的安全和隐私
titleSuffix: Configuration Manager
description: 获取 Configuration Manager 中电源管理的安全和隐私信息。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 469ff35f-59a1-484d-902b-107dd6070baf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c019faee1ffa035bde626778bb15b8f5feabc243
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696505"
---
# <a name="security-and-privacy-for-power-management-in-configuration-manager"></a>Configuration Manager 中电源管理的安全和隐私

适用范围：  Configuration Manager (Current Branch)

本部分包含 Configuration Manager 中电源管理的安全和隐私信息。  

## <a name="security-best-practices-for-power-management"></a>电源管理的最佳安全方案  
 电源管理没有相关的最佳安全方案。  

## <a name="privacy-information-for-power-management"></a>电源管理的隐私信息  
 电源管理使用内置于 Windows 监视电源使用情况和在营业时间和非工作时间期间将电源设置应用于计算机的功能。 Configuration Manager 收集计算机的电源使用情况信息，其中包括用户使用计算机时间的相关数据。 虽然 Configuration Manager 监视集合而不是每台计算机的电源使用情况，但集合可以只包含一台计算机。 默认情况下不启用电源管理，必须由管理员配置。  

 电源使用情况信息存储在 Configuration Manager 数据库中，不会发送给 Microsoft。 详细信息在数据库中保留 31 天，摘要信息保留 13 个月。 不能配置删除时间间隔。  

 在配置电源管理之前，请考虑隐私要求。  
