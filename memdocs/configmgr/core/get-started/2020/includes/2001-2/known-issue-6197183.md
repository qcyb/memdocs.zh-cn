---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: c7fce3664d23d6402d28b053129fb2b15b540a87
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89644377"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> 无法创建或编辑某些集合

<!--6197183-->
在此版本的技术预览版分支中，无法创建新的集合。 也不能编辑现有用户集合的属性。

若要解决此问题，请使用 Configuration Manager PowerShell cmdlet 创建新集合并编辑现有用户集合。 用于管理集合的一些可用 cmdlet 包括：

- [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection)

- [Get-CMCollection](/powershell/module/configurationmanager/get-cmcollection)

- [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection#related-links)

- [Add-CMCollectionMembershipRule](/powershell/module/configurationmanager/add-cmcollectionmembershiprule)