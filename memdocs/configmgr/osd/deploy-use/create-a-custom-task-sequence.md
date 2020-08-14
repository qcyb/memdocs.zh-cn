---
title: 创建自定义任务序列
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中编辑自定义任务序列以将步骤添加到任务序列。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f390c3857ad5a277002839c4c14ab1307d9ab281
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125570"
---
# <a name="create-a-custom-task-sequence-with-configuration-manager"></a>使用 Configuration Manager 创建自定义任务序列

适用范围：  Configuration Manager (Current Branch)

当在 Configuration Manager 中创建自定义任务序列时，它不包含任何任务序列步骤。 创建任务序列后，对其进行编辑，并添加所需的任务序列步骤。  

## <a name="create-a-custom-task-sequence"></a><a name="BKMK_CustomTS"></a> 创建自定义任务序列

使用下列过程来创建自定义任务序列：

1. 在 Configuration Manager 控制台中，转到“软件库”  工作区，展开“操作系统”  ，然后选择“任务序列”  节点。  

1. 在功能区的“主页”选项卡上的“创建”组中，选择“创建任务序列”    。 此操作会启动“创建任务序列向导”。  

1. 在“创建新的任务序列”  页面上，选择“创建新的自定义任务序列”  。  

1. 在“任务序列信息”页面上，指定  ：

    - 任务序列的名称
    - 任务序列的描述
    - 用于任务序列的可选启动映像

完成“创建任务序列向导”之后，Configuration Manager 会将自定义任务序列添加到“任务序列”节点  。 你现在可以编辑此任务序列以向其中添加任务序列步骤。  

## <a name="see-also"></a>另请参阅

有关可用的任务序列步骤列表，请参阅[任务序列步骤](../understand/task-sequence-steps.md)。  

有关如何编辑任务序列的信息，请参阅[使用任务序列编辑器](../understand/task-sequence-editor.md)。  

通常使用任务序列来自动执行 OS 部署的任务，但你可以创建自定义任务序列来自动执行不同类型的任务。 有关详细信息，请参阅[创建用于非 OS 部署的任务序列](create-a-task-sequence-for-non-operating-system-deployments.md)。

从版本 2002 开始，可以通过应用程序模型使用任务序列安装复杂的应用程序。 将部署类型添加到作为任务序列的应用，以安装或卸载应用。 有关详细信息，请参阅[创建 Windows 应用程序](../../apps/get-started/creating-windows-applications.md#bkmk_tsdt)。<!-- 3555953 -->

## <a name="next-steps"></a>后续步骤

[部署任务序列](deploy-a-task-sequence.md)
