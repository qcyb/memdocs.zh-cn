---
title: 硬件清单安全和隐私
titleSuffix: Configuration Manager
description: 获取 Configuration Manager 中硬件清单的安全和隐私信息。
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 62e20d86-db6d-4a1f-b14a-905a9de31698
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a5989c80818ac45bb8dd6a4f768595dbd56b846d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690105"
---
# <a name="security-and-privacy-for-hardware-inventory-in-configuration-manager"></a>Configuration Manager 中硬件清单的安全和隐私

适用范围：  Configuration Manager (Current Branch)

此主题包含 Configuration Manager 中硬件清单的安全和隐私信息。  

##  <a name="security-best-practices-for-hardware-inventory"></a><a name="BKMK_Security_HardwareInventory"></a> 硬件清单的最佳安全方案  
 从客户端收集硬件清单数据时使用下列最佳安全方案：  

|最佳安全方案|更多信息|  
|----------------------------|----------------------|  
|签名和加密清单数据|当客户端使用 HTTPS 与管理点通信时，他们发送的所有数据都使用 SSL 进行加密。 但是，当客户端计算机使用 HTTP 与内部网上的管理点通信时，客户端清单数据和收集的文件可以在未签名和未加密的状态下发送。 请确保将该站点配置为要求签名和使用加密。 此外，如果客户端可以支持 sha-256 的算法，选择需要 sha-256 选项。|  
|不会收集 IDMIF 和 NOIDMIF 文件在高安全性环境中|IDMIF 和 NOIDMIF 文件集合可用于扩展硬件清单收集。 如有必要，Configuration Manager 创建新表或修改 Configuration Manager 数据库中现有的表，以容纳 IDMIF 和 NOIDMIF 文件中的属性。 但是，Configuration Manager 不会验证 IDMIF 和 NOIDMIF 文件，因此可以使用这些文件来更改不希望更改的表。 无效数据可以覆盖有效数据。 此外，可以添加大量数据，但处理此数据可能会导致所有 Configuration Manager 功能出现延迟。 若要降低这些风险，请将硬件清单客户端设置“收集 MIF 文件”  配置为“无”  。|  

### <a name="security-issues-for-hardware-inventory"></a>硬件清单的安全问题  
 收集清单会暴露潜在的漏洞。 攻击者可以执行以下操作：  

- 发送无效数据，即使禁用了软件清单客户端设置并启用文件收集，管理点也会接受这些数据。  

- 在一个或多个文件中发送超大量数据，这可能导致拒绝服务。  

- 在将清单信息传输到 Configuration Manager 时访问清单信息。  

  由于具有本地管理权限的用户可以发送任何信息作为清单数据，因此请不要认为 Configuration Manager 收集的清单数据具有权威性。  

  默认情况下，客户端设置中启用了硬件清单。  

##  <a name="privacy-information-for-hardware-inventory"></a><a name="BKMK_Privacy_HardwareInventory"></a> 硬件清单的隐私信息  
 硬件清单允许检索 Configuration Manager 客户端上注册表和 WMI 中存储的任何信息。 软件清单允许您发现具有指定类型的所有文件或从客户端收集任何指定的文件。 通过扩展硬件和软件清单并添加新的许可证管理功能，资产智能增强了清单功能。  

 默认情况下，客户端设置中启用了硬件清单，并且收集的 WMI 信息由你选择的选项确定。 默认情况下，软件清单处于启用状态，但默认情况下不收集文件。 尽管你可以选择启用硬件清单报告类，但资产智能数据集合会自动启用。  

 清单信息不会发送到 Microsoft。 清单信息存储在 Configuration Manager 数据库中。 当客户端使用 HTTPS 来连接到管理点时，它们向站点发送的清单数据在传输过程中是加密的。 如果客户端使用 HTTP 来连接到管理点，你可以选择启用清单加密。 清单数据不会以加密格式存储在数据库中。 信息将保留在数据库中，直到每 90 天后被站点维护任务“删除过期的清单历史”  或“删除过期的收集文件”  。 可以配置删除间隔。  

 在配置硬件清单、软件清单、文件收集或资产智能数据集合前，请考虑你的隐私要求。  
