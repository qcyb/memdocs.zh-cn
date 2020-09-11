---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/13/2020
ms.openlocfilehash: 979760d1ebdd9d8f91993361921ae437ed5b81b1
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89644046"
---
### <a name="cant-delete-collections"></a><a name="ki_coll"></a> 无法删除集合

<!--6245446-->
在此版本的技术预览版分支中，无法删除集合。

若要解决此问题，请使用以下 Configuration Manager PowerShell cmdlet 来删除集合：

- [Remove-CMCollection](/powershell/module/configurationmanager/remove-cmcollection)