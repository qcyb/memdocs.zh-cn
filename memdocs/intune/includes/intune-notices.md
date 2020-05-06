---
title: 包含文件
description: 包含文件
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: fbf352c3bccfb17efc35e34a2a822b6bbbcc215d
ms.sourcegitcommit: 53bab52e42de28b87e53596646a3532e25eb9c14
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82183036"
---
本文中的通知提供了重要信息，可以帮助你为未来的 Intune 更改和功能做好准备。

### <a name="microsoft-intune-support-for-windows-10-mobile-ending--3544938--"></a>Microsoft Intune 对 Windows 10 移动版的支持即将结束<!--3544938-->
Microsoft 对 Windows 10 移动版的主流支持已于 2019 年 12 月结束。 如本支持声明所述，Windows 10 移动版用户将不再有资格从 Microsoft 接收新的安全更新、非安全修补程序、免费的辅助支持选项或联机技术内容更新。 基于对移动 OS 的全面支持，Microsoft Intune 现在将于 2020 年 8 月 10 日结束对 Windows 10 移动版应用的公司门户和 Windows 10 移动版操作系统的支持。

#### <a name="how-does-this-affect-me"></a>这对我有何影响？
如果贵组织中已部署 Windows 10 移动版设备，那么从现在到 2020 年 8 月 10 日，你可以注册新设备、添加或删除策略和应用，或更新任何管理设置。 8 月 10 日之后，我们将停止新的注册，并最终从 Intune UI 中删除 Windows 10 移动版管理。 设备将不再签入 Intune 服务，我们将删除设备和策略数据。  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>我需要如何准备应对此项变化？
你可以查看 Intune 报告，了解可能受影响的设备或用户。 转到“设备”   > “所有设备”  ，并按“OS”进行筛选。 你可以添加附加列，帮助确定你的组织中哪些人员的设备正在运行 Windows 10 移动版。 要求最终用户升级其设备或停止使用这些设备进行公司访问。


### <a name="end-of-support-for-legacy-pc-management"></a>停止支持旧版 PC 管理

将于 2020 年 10 月 15 日停止支持旧版 PC 管理。 请将设备升级到 Windows 10，并将它们重新注册为“移动设备管理”(MDM) 设备，以便继续由 Intune 托管它们。

[了解详细信息](https://go.microsoft.com/fwlink/?linkid=2107122)


### <a name="decreasing-support-for-android-device-administrator--5857738--"></a>减少对 Android 设备管理员的支持<!--5857738-->
Android 设备管理员（有时称为“旧版”Android 管理，随 Android 2.2 发布）是一种管理 Android 设备的方法。 不过，[Android Enterprise](../enrollment/connect-intune-android-enterprise.md)（随 Android 5.0 发布）现在提供改进的管理功能。 为了实现更现代化、更丰富、更安全的设备管理，Google 正在减少新 Android 版本中对设备管理员的支持。

#### <a name="how-does-this-affect-me"></a>这对我有何影响？
由于 Google 的这些变化，Intune 用户将受到以下几个方面的影响：  
- Intune 将只能在 2020 年第二季度之前为运行 Android 10 及更高版本的设备管理员管理的 Android 设备提供完全支持。 在此之后运行 Android 10 或更高版本的设备管理员管理的设备将无法再进行完全管理。 特别是，受影响的设备将不会收到新的密码要求。
    - Samsung Knox 设备在此期间不受影响，因为通过 Intune 与 Knox 平台的集成提供了扩展支持。 这使你有更多时间来规划过渡弃用设备管理员管理。    
- 设备管理员管理的仍在低于 Android 10 的 Android 版本上运行的 Android 设备将不会受到影响，可以继续完全由设备管理员进行管理。    
- 对于运行 Android 10 及更高版本的所有设备，Google 限制了设备管理员管理代理（如公司门户）访问设备标识符信息的能力。 在设备更新到 Android 10 或更高版本后，此限制将影响以下 Intune 功能：  
    - VPN 的网络访问控制将不再有效。   
    - 使用 IMEI 或序列号将设备识别为公司拥有的设备将不会自动将设备标记为公司拥有的设备。  
    - 在 Intune 中，IMEI 和序列号将不再对 IT 管理员可见。 
        > [!NOTE]
        > 这只会影响 Android 10 及更高版本上设备管理员管理的设备，并且不会影响作为 Android Enterprise 管理的设备。 

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>我需要如何准备应对此项变化？
为避免在即将到来的 2020 年第三季度出现功能降低的情况，建议采取如下操作：
- 不要将新设备加入设备管理员管理中。
- 如果希望设备接收到 Android 10 的更新，请将其从设备管理员管理迁移到 Android Enterprise 管理和/或应用保护策略。

#### <a name="additional-information"></a>其他信息
- [从设备管理员迁移到 Android Enterprise 的 Google 指南](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [弃用设备管理员 API 计划的 Google 文档](https://developers.google.com/android/work/device-admin-deprecation)