---
title: '将更新添加到更新组 '
titleSuffix: Configuration Manager
description: 手动或自动将软件更新添加到环境中的软件更新组。
ms.date: 03/18/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: a0767664-fd60-46a8-9da5-86cc431ce53c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: c38ed629e606d3f891a6473866d0e8eda40eade1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708585"
---
# <a name="add-software-updates-to-an-update-group"></a>将软件更新添加到更新组  

适用范围：  Configuration Manager (Current Branch)

 软件更新组会为你提供行之有效的方法来组织你的环境中的软件更新。 你可以将软件更新手动添加到软件更新组，或通过运用 ADR，将软件更新自动添加到软件更新组。 你还可以手动部署软件更新组，或通过运用 ADR 自动部署该组。 在部署软件更新组后，你可以将新的软件更新添加到组，Configuration Manager 将自动对它们进行部署。 使用下列过程以将软件更新添加到新的或现有的软件更新组。  

#### <a name="to-add-software-updates-to-a-new-software-update-group"></a>将软件更新添加到新的软件更新组  

1.  在 Configuration Manager 控制台中，单击“软件库”  。  

2.  在“软件库”工作区中，展开“软件更新”  ，然后单击“所有软件更新”  。  

3.  选择要添加到新软件更新组的软件更新。  

4.  在“主页”  选项卡上的“更新”  组中，单击“创建软件更新组”  。  

5.  指定软件更新组的名称并根据需要提供描述。 使用名称和描述提供足够的信息，供你确定软件更新组中软件更新的类型。 要继续，请单击“创建”  。  

6.  单击“软件更新组”  以显示新的软件更新组。  

7.  选择软件更新组，在“主页”  选项卡内的“更新”  组中，单击“显示成员”  以显示组中所包含的软件更新的列表。  

#### <a name="to-add-software-updates-to-an-existing-software-update-group"></a>将软件更新添加到现有软件更新组中  

1.  在 Configuration Manager 控制台中，单击“软件库”  。  

2.  在“软件库”工作区中，展开“软件更新”  ，然后单击“所有软件更新”  。  

3.  选择要添加到新软件更新组的软件更新。  

    > [!NOTE]  
    >  在“所有软件更新”  节点上，Configuration Manager 将显示所有更新，但“升级”  分类和“Office 365 客户端”  产品分类中的更新除外。  

4.  在“主页”  选项卡上的“更新”  组中，单击“编辑成员身份”  。  

5.  选择要添加软件更新的软件更新组。  

6.  单击“软件更新组”  节点以显示软件更新组。  

7.  选择软件更新组，并在“主页”  选项卡中的“更新”  组中单击“显示成员”  ，以显示软件更新组中所包括的软件更新列表。  
