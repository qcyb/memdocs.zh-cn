---
title: 导入和导出应用程序
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中导入和导出应用程序，以在不同的层次结构之间共享。
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: dba00e54-9d5b-4f6b-916d-ead48c66e288
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3db127deb353f30566a1f03cbc6ac0eef666cb37
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88695250"
---
# <a name="import-and-export-applications"></a>导入和导出应用程序

适用范围：  Configuration Manager (Current Branch)

使用 Configuration Manager 在两个层次结构之间导入和导出应用程序。 例如，将应用程序从测试环境复制到生产环境。

## <a name="export"></a>导出

1. 在 Configuration Manager 控制台中，选择“应用程序”节点  。 在功能区的“创建”组中，选择“导出应用程序”  。
1. 在“常规”屏幕上，输入要导出到的新 ZIP 文件的路径  。 （可选）指定是否导出*依赖项、取代关系、条件和虚拟环境*，以及*所选应用程序和依赖项的内容*。  如果需要，输入管理员注释，然后选择“下一步”  。
1. 确保应用程序和所有依赖项都列在“相关对象”页上，然后选择“下一步”   。
1. 在“摘要”页上，选择“下一步”  。
1. 该过程完成后，将创建 ZIP 文件，你可以关闭向导。

> [!IMPORTANT]
> 如果要将此应用程序复制到另一个环境，请使用该 ZIP 文件及其附带的文件夹。 该 ZIP 文件必须与创建的文件夹位于同一目录中。

## <a name="import"></a>导入

> [!NOTE]
> 只能从 UNC 路径导入应用程序，不能直接从本地磁盘导入。

1. 在 Configuration Manager 控制台中，选择“应用程序”节点  。 在功能区的“创建”组中，选择“导入应用程序”  。
1. 选择要导入的 ZIP 文件，然后选择“下一步”  。
1. “文件内容”窗口显示导入应用程序时发生的情况。 选择“下一步”  。
1. 查看摘要屏幕，然后选择“下一步”  。
1. 关闭向导。 应用程序现在出现在站点中。

## <a name="see-also"></a>另请参阅
 
使用 PowerShell 自动导入和导出应用程序。

* [Import-CMApplication](/powershell/module/configurationmanager/import-cmapplication)
* [Export-CMApplication](/powershell/module/configurationmanager/export-cmapplication)