---
title: 用户设备关联 - Intune 数据仓库
titleSuffix: Microsoft Intune
description: UserDeviceAssociation 实体包含组织中的用户设备关联。
keywords: Intune 数据仓库
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 777484A7-09CE-4409-987F-76B3F87DFE93
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f095c011f85ea280b6bf1c37140152ac27ef8817
ms.sourcegitcommit: 118587ddb31ce26b27801839db9b3b59f1177f0f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84165203"
---
# <a name="reference-for-user-device-association-entity"></a>用户设备关联实体参考

userDeviceAssociation  实体包含组织中的用户设备关联。

## <a name="userdeviceassociations"></a>userDeviceAssociations


|        Name        |                                           Description                                            |        示例         |
|--------------------|--------------------------------------------------------------------------------------------------|------------------------|
|      userKey       |              数据仓库中用户的唯一标识符。 （代理键）。               |          123           |
|     deviceKey      |                      数据仓库中设备的唯一标识符。                      |          123           |
| createdDateTimeUTC |           创建用户设备关联时的日期和时间。 使用 UTC 格式。           | 2016/11/23 - 中午 12:00:00 |
|     isDeleted      | 指示用户已取消设备注册，并且该关联不再活跃。 |       True/False       |
|  endedDateTimeUTC  |              IsDeleted 更改为 True 时的 UTC 日期和时间。               | 2017/06/23 凌晨 12:00:00 |

## <a name="next-steps"></a>后续步骤

- 了解有关 [Intune 数据仓库](reports-nav-create-intune-reports.md)的详细信息。
