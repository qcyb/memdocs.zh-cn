---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/13/2020
ms.openlocfilehash: 54e00688c1375f9ec54ada86d2b2c4b9347d5405
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691845"
---
### <a name="cant-delete-collections"></a><a name="ki_coll"></a> 无法删除集合

<!--6245446-->
在此版本的技术预览版分支中，无法删除集合。

若要解决此问题，请使用以下 Configuration Manager PowerShell cmdlet 来删除集合：

- [Remove-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollection?view=sccm-ps)
