---
title: 查询的安全和隐私
titleSuffix: Configuration Manager
description: 从站点数据库查询信息时，请了解最佳安全做法和隐私。
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 882eedd1be029d5824fbd5d26a3f08d8f8f0021d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695695"
---
# <a name="security-and-privacy-for-queries-in-configuration-manager"></a>Configuration Manager 中查询的安全和隐私

适用范围：  Configuration Manager (Current Branch)

使用 Configuration Manager 中的查询，可以根据指定条件从站点数据库中检索信息。 Configuration Manager 会在标准操作过程中收集站点数据库信息。 例如，通过使用在发现或清单期间收集的信息，可以配置查询来发现满足指定条件的设备。  

 若要详细了解查询，请参阅[查询简介](../../../core/servers/manage/introduction-to-queries.md)。 有关 Configuration Manager 操作（即收集可使用查询检索的数据）的最佳安全做法和隐私信息，请参阅 [Configuration Manager 安全与隐私](../../../core/plan-design/security/security-and-privacy.md)。  

## <a name="security-best-practices-for-queries"></a>查询安全性最佳做法

 将此最佳安全做法用于查询。  

|最佳安全方案|更多信息|  
|----------------------------|----------------------|  
|导出或导入保存到网络位置的查询时，请保护位置和网络通道。|限制可访问网络文件夹的人员。<br /><br /> 在网络位置与站点服务器之间使用服务器消息块 (SMB) 签名或 Internet 协议安全性 (IPsec)，以防攻击者在查询数据导入前篡改它。|  

## <a name="next-steps"></a>后续步骤
  
[Configuration Manager 安全和隐私](../../../core/plan-design/security/security-and-privacy.md)
