---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/13/2020
ms.openlocfilehash: d887f842b789b41260a49b149b61f28741937613
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88704478"
---
### <a name="cant-delete-collections"></a><a name="ki_coll"></a> 无法删除集合

<!--6245446-->
在此版本的技术预览版分支中，无法删除集合。

若要解决此问题，请使用以下 Configuration Manager PowerShell cmdlet 来删除集合：

- [Remove-CMCollection](/powershell/module/configurationmanager/remove-cmcollection?view=sccm-ps)