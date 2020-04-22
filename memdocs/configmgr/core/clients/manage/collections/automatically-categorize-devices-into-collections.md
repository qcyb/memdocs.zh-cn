---
title: 自动将设备分类到集合
titleSuffix: Configuration Manager
description: 自动将设备分类到集合。
ms.date: 04/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: f91f150a095838484c516226da0d3e44e1f5b331
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695265"
---
# <a name="automatically-categorize-devices-into-collections"></a>自动将设备分类到集合

适用范围：  Configuration Manager (Current Branch)

可创建设备类别，可将其用于配合使用 Microsoft Intune 和 Configuration Manager 时自动在设备集合中放置设备。 然后用户在 Intune 中注册设备时需要选择某个设备类别。 可从 Configuration Manager 控制台中更改设备类别。

> [!IMPORTANT]
>  此功能适用于 **2016 年 6 月**及以后版本的 Microsoft Intune。 试用这些过程前，请确保已更新到此版本。

## <a name="create-device-categories"></a>创建设备类别

1.  转到“资产和符合性”   > “概述”   > “设备集合”  。
2.  在“主页”  选项卡上的“设备集合”  组中，选择“管理设备类别”  。
3.  创建、编辑或删除类别。

## <a name="associate-a-collection-with-a-device-category"></a>将集合与设备类别相关联

将集合与设备类别关联后，该类别中的所有设备都会添加到该集合。 无法将设备类别规则添加到内置集合（如“所有系统”  ）。

1.  在设备集合“属性”  对话框的“成员身份规则”  选项卡上，选择“添加规则”   > “设备类别规则”  。
2.  在“选择设备类别”  对话框中，选择一个或多个设备类别，所选类别将应用到集合中的所有设备。

## <a name="change-the-category-of-a-device"></a>更改设备的类别

1.  在“资产和符合性”   > “概述”   > “设备”  中，从“设备”  列表中选择一个设备。
2.  在“主页”  选项卡的“设备”  组中，选择“更改类别”  。
3.  选择一个类别，然后选择“确定”  。

## <a name="view-which-category-a-device-belongs-to"></a>查看设备所属的类别

在“资产和符合性”   > “概述”   > “设备”  中的“设备”  列表中，此类别在“设备类别”  列中显示。

如果“设备类别”  列未显示，请在“设备”  列（如“名称”  ）中右键单击其中一个列标题，然后选择“设备类别”  。

如果将某个设备分配到某个类别，随后又删除该类别，则“按用户在 Microsoft Intune 中注册的设备的列表”  报表将在“设备类别”  列显示 GUID，而不显示类别名称。
