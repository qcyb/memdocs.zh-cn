---
author: brenduns
ms.author: brenduns
ms.service: microsoft-intune
ms.subservice: protect
ms.topic: include
ms.date: 08/24/2020
ms.openlocfilehash: 01179c35274ff14d4a91283e9a38aa5e6fee8e03
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88823468"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
1. 在连接到顶层站点的 Configuration Manger 控制台中，右键单击同步到 Microsoft Endpoint Manager 管理中心的设备集合，然后选择“属性”。

2. 在 **“云同步”** 选项卡上，启用此选项以**使此集合能够通过 Microsoft Endpoint Manager 管理中心分配终结点安全策略**。

   - 如果 Configuration Manager 层次结构未配置租户附加，则无法选择此选项。
   - 可用于此选项的集合受[为租户附加上传选择的集合范围](../../../configmgr/tenant-attach/device-sync-actions.md#bkmk_edit)的限制。 <!--CM7423168-->
  
   ![配置云同步](../media/tenant-attach-intune/cloud-sync.png)

3. 选择“确定”保存配置。

   此集合中的设备现在可以加入 Microsoft Defender ATP，并支持使用 Intune 终结点安全策略。
