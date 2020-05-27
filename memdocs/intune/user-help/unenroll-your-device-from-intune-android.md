---
title: 如何从 Intune 删除 Android 设备 | Microsoft Docs
description: 如何从 Intune 公司门户删除 Android 设备
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/19/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: f40aab26-7613-48cc-a74e-de83df9465a4
searchScope:
- User help
ROBOTS: ''
ms.reviewer: arnab
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 0715cce163d999ef0c978f9c085ce9df10b5155a
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881696"
---
# <a name="unenroll-your-android-device-from-management"></a>取消注册 Android 设备管理  

删除已注册的 Android 设备，使其不再由组织管理。 本文介绍如何从公司门户应用中删除设备。 删除设备后：  

* 设备将无法访问组织受保护的数据和资源。
* 设备不再显示在公司门户中。
* 不能通过“公司门户”安装应用。
* 将不再应用当添加设备时在设备上更改的任何设置（例如禁用相机，或需要一定的密码长度）。  

> [!NOTE]
> 无法从 Microsoft Intune 应用取消注册或删除公司拥有的设备。 设备在初始设备设置过程中进行注册，并且必须进行注册才能访问组织的资源。  

1. 在公司门户中，转到右上角并点击三个垂直点。 “操作”菜单随即打开。

   ![Android 公司门户应用的屏幕截图，其中操作菜单已在右上角打开。 新的“删除公司门户”选项是第三个选项，位于“我的配置文件“和“设置”的下方，以及“条款和条件”、“帮助和反馈”和“关于”的上方。](./media/android_remove_cp_menu_action_after_1705.png)

2. 点击“删除公司门户”  。  

3. 将显示一条消息，说明取消注册设备后会发生的情况。 点击“确定”，确认要从公司门户中删除设备  。

   ![在操作菜单中选择新的“删除公司门户”选项后出现确认的屏幕截图。](./media/android_remove_cp_menu_confirmation_after_1705.png)

## <a name="remove-data-collected-by-the-company-portal-app"></a>删除由公司门户应用收集的数据  

若要删除 Android 适用的公司门户应用存储在设备上的所有数据，请执行以下操作：

- 通过点击“应用程序” >  [应用名称]  > “清除数据”来清除应用数据    。
- 删除以下文件夹：\storage\internal storage\Android\data\com.microsoft.windowsintune.companyportal。

## <a name="uninstall-the-company-portal-app"></a>卸载公司门户应用

公司门户是一种设备管理应用。 因此在取消注册设备管理之前，都无法将其卸载。 该操作完成后，请点击并按住公司门户应用图标，直到看到“卸载”  。 点击“卸载”，从设备中删除应用  。  

或者，点击“设置” > “应用” > “公司门户” > “卸载”     。  

### <a name="remove-the-company-portal-app-as-a-device-administrator"></a>以设备管理员身份删除公司门户应用

还有最后一种办法，以设备管理员的身份从设备卸载该应用。  

如果有公司拥有的设备，组织可能会要求始终在该设备上安装公司门户。 卸载该应用后，除非重新安装它，否则可能无法访问受保护的公司资源，例如电子邮件、应用、Wi-Fi 或 VPN。 若要详细了解如何安装、更新或删除所需应用，请参阅[向 Microsoft Intune 添加应用](/intune/apps/apps-add#apps-that-are-added-automatically-by-intune)。

以下是以设备管理员身份禁用公司门户的步骤。 在 Android 设备上，每项设置的实际名称可能会有所不同。  

**选项 1**：  

1. 选择“设置” > “安全性” > “其他安全设置” > “设备管理员”     。  
2. 清除“公司门户”选择  。  

**选项 2**：

1. 选择“设置” > “锁屏界面和安全性” > “其他安全设置” > “设备管理应用”     。
2. 清除“公司门户”选择  。

仍需帮助？ 请与公司支持人员联系。 有关联系信息，请查看[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)。
