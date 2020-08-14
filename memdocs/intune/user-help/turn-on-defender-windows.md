---
title: 开启 Windows Defender | Microsoft Docs
description: 了解如何打开 Windows Defender 以访问公司资源。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/07/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d16dd2de-3ed5-474f-a04b-36dcd350162c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: shburbid
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: a57010a5c8089b0ac979cf43c3706467d83faea2
ms.sourcegitcommit: 532a06163f462527254d23e7dc505b18c0c4f938
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/11/2020
ms.locfileid: "88110692"
---
# <a name="turn-on-windows-defender-to-access-company-resources"></a>打开 Windows Defender 以访问公司资源

组织需要确保访问其资源的设备受到保护，因此可能会要求你使用 [Windows Defender](https://www.microsoft.com/safety/pc-security/windows-defender.aspx)。 Windows Defender 是 Windows 随附的防病毒软件，可帮助保护设备免受病毒以及其他恶意软件和威胁的侵害。 

本文介绍如何更新设备设置，以满足组织的防病毒要求并解决访问问题。 

## <a name="turn-on-windows-defender"></a>打开 Windows Defender
完成以下步骤可在设备上打开 Windows Defender。 

1. 选择“开始”菜单。
2. 在搜索栏中，键入“组策略”。 然后从列出的结果中选择“编辑组策略”。 这将打开“本地组策略编辑器”。
4. 选择“计算机配置” > “管理模板” > “Windows 组件” > “Windows Defender 防病毒”   。 
5. 滚动到列表底部，选择“关闭 Windows Defender 防病毒”。  
6. 选择“已禁用”或“未配置” 。 选择这些选项可能会让人感觉不合理，因为这些名称表明你将关闭 Windows Defender。 别担心，这些选项实际上是确保它已打开。 
7. 选择“应用” > 确定” 。  


## <a name="turn-on-real-time-and-cloud-delivered-protection"></a>启用实时保护和云提供的保护

请完成以下步骤，启用实时保护和云提供的保护。 这些防病毒功能共同防范间谍软件，并可通过云提供针对恶意软件问题的修补程序。 

1. 选择“开始”菜单。
2. 在搜索栏中，键入“Windows 安全”。 选择匹配的结果。 
3. 选择“病毒和威胁防护”。
4. 在“病毒和威胁防护设置”中，选择“管理设置” 。
5. 按“实时保护”和“云提供的保护”下的每个开关，将它们打开 。 

如果在屏幕上看不到这些选项，它们可能被隐藏了。 请完成以下步骤使其可见。  

1. 选择“开始”菜单。  
2. 在搜索栏中，键入“组策略”。 然后从列出的结果中选择“编辑组策略”。 这将打开“本地组策略编辑器”。
3. 选择“计算机配置” > “管理模板” > “Windows 组件” > “Windows 安全性” > “病毒和威胁防护”    。
4. 选择“隐藏病毒和威胁防护区域”。
5. 选择“已禁用” > “应用” > “确定”  。  

## <a name="update-your-antivirus-definitions"></a>更新防病毒定义
请完成以下步骤，更新防病毒定义。  
1. 选择“开始”菜单。
2. 在搜索栏中，键入“Windows 安全”。 选择匹配的结果。 
3. 选择“病毒和威胁防护”。
4. 在“病毒和威胁防护更新”下，选择“检查更新” 。 如果在屏幕上看不到此选项，请完成[启用实时保护](turn-on-defender-windows.md#turn-on-real-time-and-cloud-delivered-protection)中的第一组步骤。 然后再次尝试检查更新。 

## <a name="next-steps"></a>后续步骤  

仍需帮助？ 请与公司支持人员联系。 有关他们的联系信息，请查看[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)。
