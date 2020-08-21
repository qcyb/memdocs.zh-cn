---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 02/03/2020
ms.openlocfilehash: fca1d884b75380f90a2e2e3cdc2fb0cac357b6b5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88703391"
---
### <a name="cant-create-or-edit-some-collections"></a><a name="ki_coll"></a> 无法创建或编辑某些集合

<!--6197183-->
在此版本的技术预览版分支中，无法创建新的集合。 也不能编辑现有用户集合的属性。

若要解决此问题，请使用 Configuration Manager PowerShell cmdlet 创建新集合并编辑现有用户集合。 用于管理集合的一些可用 cmdlet 包括：

- [New-CMCollection](/powershell/module/configurationmanager/new-cmcollection?view=sccm-ps)

- [Get-CMCollection](/powershell/module/configurationmanager/get-cmcollection?view=sccm-ps)

- [Set-CMCollection](/powershell/module/configurationmanager/set-cmcollection?view=sccm-ps#related-links)

- [Add-CMCollectionMembershipRule](/powershell/module/configurationmanager/add-cmcollectionmembershiprule?view=sccm-ps)