---
title: 使用资源浏览器查看软件清单
titleSuffix: Configuration Manager
description: 使用资源浏览器来查看 Configuration Manager 中的软件清单。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 08905a72b6af6e9eae4d2cef9f4732ef692dc134
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690065"
---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-configuration-manager"></a>如何使用资源浏览器来查看 Configuration Manager 中的软件清单

适用范围：  Configuration Manager (Current Branch)

使用 Configuration Manager 中的资源浏览器查看从层次结构中的计算机中收集的软件清单的相关信息。  

> [!NOTE]  
>  在客户端上运行软件清单周期后，资源浏览器才会显示清单数据。  

 资源浏览器提供下列软件清单信息：  

-   **软件**：  

    -   **收集的文件** - 在软件清单期间所收集的文件。  

    -   **文件详细信息** - 在软件清单期间清点的与特定产品或制造商无关的文件。  

    -   **上次软件扫描** - 客户端计算机上最后一次软件清单和文件收集的日期和时间。  

    -   **产品详细信息** - 由软件清单清点的按制造商分组的软件产品。  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>若要从 Configuration Manager 控制台运行资源浏览器  

1.  在 Configuration Manager 控制台中，选择“资产和符合性” 

2.  在“资产和符合性”  工作区中，选择“设备”  或打开显示设备的任何集合。  

3.  选择包含想要查看的清单的计算机，然后在“主页”  选项卡 >“设备”  组中，选择“启动”   > “资源浏览器”  。

4.  可以右键单击“资源浏览器”窗口右窗格中的任意项，然后选择“属性”  ，以可读性更强的格式查看收集的清单信息。  
 
## <a name="view-and-manage-collected-diagnostic-files"></a><a name="bkmk_diag"> </a> 查看和管理收集的诊断文件

从 Configuration Manager 版本 2002 开始，可使用资源浏览器来查看和管理在使用客户端通知[收集客户端日志](../client-notification.md#client-diagnostics)时收集的文件。 

1. 从“设备”节点，右键单击要查看其日志的设备。 
1. 选择“开始”，然后选择“资源浏览器”。  
1. 从“资源浏览器”中，单击“诊断”。  
1. 在“诊断文件”列表中，可以看到文件的收集日期。  客户端日志的名称格式为 `Support_<guid>.zip`。
1. 右键单击 zip 文件，然后选择下列选项之一：
    - **打开支持中心**：启动[支持中心](../../../support/support-center.md)。
    - **复制**：从资源浏览器复制行信息。
    - **查看文件**：通过文件资源管理器打开 zip 文件所在的文件夹。
    - **保存**：打开所选文件的“保存文件”对话框。
    - **导出**：保存“诊断文件”中显示的资源浏览器列。 
    - **刷新**：刷新文件列表。
    - **属性**：返回所选文件的属性。 

[![使用资源浏览器查看并保存客户端日志](./../media/4226618-view-collected-client-logs.png)](./../media/4226618-view-collected-client-logs.png#lightbox)

## <a name="next-steps"></a>后续步骤

[使用支持中心](../../../support/support-center.md)查看收集的诊断文件。
