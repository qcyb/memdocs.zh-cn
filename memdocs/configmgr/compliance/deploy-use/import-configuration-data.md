---
title: 导入配置数据
titleSuffix: Configuration Manager
description: 如果配置数据为 cabinet 文件格式，并且符合受支持的服务建模语言架构，则将它导入。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 309b9a09-a611-4ba2-90ab-dde51582cf87
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 7d9760a49815b9eb33c7886f4d9a8f9637dedd21
ms.sourcegitcommit: 9f072da27aa64f46a9409470b5dac5bfac3a0fe5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2020
ms.locfileid: "89468305"
---
# <a name="import-configuration-data-with-configuration-manager"></a>使用 Configuration Manager 导入配置数据

适用范围：  Configuration Manager (Current Branch)

除了在 Configuration Manager 控制台中创建配置基线和配置项目之外，还可以导入配置数据（如果它采用 cabinet (.cab) 文件格式并符合受支持的服务建模语言 (SML) 架构）。 可从以下位置导入配置数据：  

- 从 Microsoft 或从其他软件供应商站点下载的最佳做法配置数据（配置包）。  

- 从 System Center 2012 Configuration Manager 及更高版本导出的配置数据。  

- 在外部创建且符合 SML 架构的配置数据。  

当导入配置基线时，配置基线中引用的部分或全部配置项目也可能包含在 CAB 文件中。 在导入过程中，Configuration Manager 会验证配置基线中引用的所有配置项目是否也包括在 Cabinet 文件中或在 Configuration Manager 站点中已存在。 如果尝试导入的配置基线引用了 Configuration Manager 无法找到的配置数据，导入过程会失败。  

导入过程可能失败的其他情况包括：  

-   配置数据引用了 Configuration Manager 在其数据库中或在 CAB 文件自身中找不到的配置数据。  

-   Configuration Manager 数据库中已存在一些具有相同名称和配置数据版本，但具有不同内容版本的配置数据。  

-   Configuration Manager 数据库中已存在具有相同内容版本的配置数据，但哈希计算将它识别为不同内容版本。  

-   在 Configuration Manager 数据库中已存在或最近已删除具有相同名称的配置数据的较新版本。  

-   在多站点 Configuration Manager 层次结构中，配置数据最初是从父站点中导入的。 必须从同一站点而非一个子站点更新配置数据。  

### <a name="import-configuration-data"></a>导入配置数据  

1.  在 Configuration Manager 控制台中，单击“资产和符合性” > “配置项目”或“配置基线”
2.  在“主页”**** 选项卡上的“创建”**** 组中，单击“导入配置数据”****。  
3.  在“导入配置数据向导” **** 的“选择文件” **** 页上，单击“添加” ****，然后在“打开” **** 对话框中，选择要导入的 .cab 文件。  
4.  如果希望可以在 Configuration Manager 控制台中编辑导入的配置数据，请选中“**创建已导入配置基线和配置项目的新副本”** 复选框。  
5.  在“摘要”**** 页上，查看将执行的操作，然后完成向导。  

导入的配置数据会显示在“资产和符合性”**** 工作区的“符合性设置”**** 节点中。  
