---
title: 创建应用程序组
titleSuffix: Configuration Manager
description: 创建一组可以在 Configuration Manager 中作为单个部署发送到用户或设备集合的应用程序。
ms.date: 04/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: e67c691e-62ef-4f43-9cfb-0e957d1e7a5f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f63c52fcd2aaccbfbe04160581318126bc53db12
ms.sourcegitcommit: 2aa97d1b6409575d731c706faa2bc093c2b298c4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82643134"
---
# <a name="create-application-groups"></a>创建应用程序组

适用范围：  Configuration Manager (Current Branch)

<!--3555907-->

从版本 1906 开始，创建一组可以作为单个部署发送到用户或设备集合的应用程序。 指定的有关应用组的元数据在软件中心中显示为单个实体。 可以在组中对应用排序，以便客户端将其以特定顺序安装。

> [!Note]  
> 在该 Configuration Manager 版本中，应用组是预发形功能。 若要启用此功能，请参阅[预发行功能](../../core/servers/manage/pre-release-features.md)。  

1. 在 Configuration Manager 控制台中，转到“软件库”工作区  。 展开“应用程序管理”，然后选择“应用程序组”节点   。  

1. 在功能区的“创建”组中，选择“创建应用程序组”  。

1. 在“常规信息”页上，指定有关应用组的信息  。  

1. 在“软件中心”页上，包含软件中心中显示的信息  。  

1. 在“应用程序组”页上，选择“添加”   。 为此组选择一个或多个应用。 使用“上移”和“下移”操作对其重新排序   。  

1. 完成向导。  

使用与部署应用程序相同的过程部署应用组。 有关详细信息，请参阅[部署应用程序](deploy-applications.md)。 从版本 1910 开始，你可将应用组部署到设备或用户集合。

部署组后：

- 如果将新应用添加到组中，则必须将新应用内容单独分发到分发点。

- 如果修改应用组中的应用，则请重新分发内容。

要对应用组部署进行排除故障，请使用客户端上的以下日志文件：

- **AppGroupHandler.log**
- **AppEnforce.log**
- **SettingsAgent.log**

> [!Important]  
> 在将整个层次结构和目标客户端更新到至少版本 1906 之前，不要创建或部署应用组。

### <a name="known-issues"></a>已知问题

- *版本 1906*：组中的应用只能包含“Windows Installer”或“脚本”部署类型   。
  - *版本 1906*：将部署类型安装行为设置为“为系统安装”  。
- 以下部署选项可能无效：警报、审批、分阶段部署、修复。
- 无法导出或导入应用组。
- 不要在组中包含任何需要重启的应用，否则组部署可能会失败。
- *版本 1906*：无法将应用组部署到用户集合。
- *版本 1906*：用户无法在软件中心卸载  应用组。
- 如果删除应用组中的应用，则在下次查看应用组的属性时，你将看到以下警告：“无法加载组中所有应用程序的信息。” 对应用组进行简单的更改并保存。 例如，在“管理员备注”  中添加一个空格。 保存更改时，会将已删除的应用从组中清除。<!-- 7099542 -->
