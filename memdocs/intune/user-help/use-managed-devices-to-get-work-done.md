---
title: 什么是设备注册 | Microsoft Docs
description: 了解向公司门户和 Microsoft Intune 应用注册设备的意义。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/13/2019
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 523caa6b-d792-4bb6-bddb-24b2479932d8
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: 3f80fffc21ac4dcd256120b03dc1e0bebe20ab52
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "83880700"
---
# <a name="what-is-device-enrollment"></a>什么是设备注册？
若要从设备访问工作或学校资源，需要向 Intune 公司门户应用或 Microsoft Intune 应用注册设备。 

在设备注册过程中：

* 会向组织注册你的设备。 此步骤可确保向你授权访问组织的电子邮件、应用和 Wi-Fi。 
* 组织的设备管理策略会应用于你的设备。 策略可以包含对设备密码和加密等方面的要求。 这些要求的目的是使设备和组织的数据保持安全，不受未经授权的访问。

更新设备设置以满足组织的要求后，注册便会完成。 几乎可以从任何位置安全地登录到工作或学校帐户。  

本文介绍注册的其他方面，例如如何获取应用、支持的设备以及删除或重置设备。  

## <a name="company-portal-and-microsoft-intune-app"></a>公司门户和 Microsoft Intune 应用

公司门户和 Microsoft Intune 应用会向你提醒策略或设置更改，以便你可以采取措施，而不会失去对工作或学校的访问权限。 

公司门户应用将个人信息和工作信息分开，因此你可以保持工作效率和专注力。 它还使工作和学校应用可供你使用，以便你可以查找并安装与你的行业相关的应用。  

### <a name="get-company-portal"></a>获取公司门户

在某些情况下，组织会在你的设备上为你安装公司门户应用。 也可以从应用商店（例如 Microsoft Store、App Store 和 Google Play 商店）安装该应用。 若要通过 Web 浏览器访问该应用，请使用工作或学校帐户登录到[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)。  

### <a name="get-microsoft-intune-app"></a>获取 Microsoft Intune 应用

如果需要使用 Microsoft Intune 应用，则组织会在你的设备上为你安装它。  

## <a name="whats-the-difference-between-the-apps-and-the-website"></a>应用与网站有何区别？
公司门户应用适用于 Windows 10、iOS、macOS 和 Android 设备。 它与设备的相应平台无缝集成。 网站版本可以从任意设备访问，无论你使用何种设备，都会为你提供相同的通用体验。 

Microsoft Intune 应用适用于公司拥有的 Android 设备，没有网站。  

## <a name="what-kind-of-devices-can-you-enroll-with-company-portal"></a>可以向公司门户注册哪些类型的设备？
可以向公司门户注册以下设备：  

- Windows 设备
  - Windows 10 移动版
  - Windows 10 桌面版
  - Windows Phone 8。1
  - Windows 8。1
- Apple 设备
    - iOS
    - macOS
- Android 设备


## <a name="what-kind-of-devices-can-you-enroll-with-the-microsoft-intune-app"></a>可以向 Microsoft Intune 应用注册哪些类型的设备？  
可以注册组织已设置为与该应用一起使用的公司拥有的 Android 设备。 该应用支持 Android 6.0 及更高版本。 

## <a name="can-you-remove-a-device-from-the-company-portal"></a>是否可以从公司门户中删除设备？
可以从公司门户中删除或重置设备。 **删除**和**重置**有所不同。

在设备删除过程中，公司门户会取消注册并注销设备。 该设备会无法访问公司门户。 还可能会删除工作或学校数据。 

当重置设备时，公司门户会尝试将计算机或设备重置回制造商默认设置。 会从设备中删除所有工作或学校数据以及所有个人数据。 例如，如果丢失设备，则重置会十分有用。 可以从公司门户网站远程重置。  

## <a name="can-you-remove-a-device-from-the-microsoft-intune-app"></a>是否可以从 Microsoft Intune 应用中删除设备？
不能，无法从 Microsoft Intune 应用中删除公司拥有的设备。  

## <a name="what-if-i-cant-see-my-device-in-the-company-portal-or-microsoft-intune-app"></a>如果在公司门户或 Microsoft Intune 应用中看不到我的设备该怎么办？
若要在公司门户中查看设备，必须先注册它。 如果注册之后仍看不到所有设备，请尝试通过公司门户同步或检查访问。 你无法查看你公司所拥有和管理的设备。

在 Microsoft Intune 应用中，只会看到当前正在使用的设备。 在该应用中，其他已注册的设备对你不可见。  

## <a name="where-else-can-i-go-for-help"></a>可以从其他哪些地方获取帮助？  
若要解决常见问题，请查看以下特定于平台的文档：  

- [解决 Android 设备的常见问题](check-compliance-on-your-device-android.md)  
- [解决 iOS 设备的常见问题](troubleshoot-your-device-ios.md)
- [解决 macOS 设备的常见问题](troubleshoot-your-device-macos.md)
- [解决 Windows 设备的常见问题](troubleshoot-your-device-windows.md)

还可以与 IT 支持人员联系。 公司门户和 Microsoft Intune 应用提供了帮助和支持页面，其中列出了联系信息以及报告问题的方式。 还可在组织的[公司门户网站](https://go.microsoft.com/fwlink/?linkid=2010980)上获得联系信息。  

## <a name="next-steps"></a>后续步骤  

如果已准备好访问工作或学校帐户，请按照组织的说明注册设备。 也可以在以下文章中找到分步注册指导。

* [注册 Windows 10 设备](enroll-windows-10-device.md)
* [注册 Android 设备](enroll-device-android-company-portal.md)
* [使用 Android 工作配置文件注册](enroll-device-android-work-profile.md)
* [使用 Microsoft Intune 应用注册](enroll-device-android-microsoft-intune-app.md)
* [注册 iOS 设备](enroll-your-device-in-intune-ios.md)
* [注册组织提供的 iOS 设备](enroll-your-device-dep-ios.md)
* [注册 macOS 设备](enroll-your-device-in-intune-macos-cp.md)
* [注册组织提供的 macOS 设备](enroll-company-device-macos.md)
