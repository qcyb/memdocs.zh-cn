---
title: 包含文件
description: 包含文件
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: 0b3af293ebc83c14f85abeb0dbaa38ca5187b267
ms.sourcegitcommit: 6a6a713fc1090e03893d80f4259dc7300fb1d5ff
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2020
ms.locfileid: "80438708"
---
本文中的通知提供了重要信息，可以帮助你为未来的 Intune 更改和功能做好准备。

### <a name="microsoft-intune-support-for-windows-10-mobile-ending--3544938--"></a>Microsoft Intune 对 Windows 10 移动版的支持即将结束<!--3544938-->
Microsoft 对 Windows 10 移动版的主流支持已于 2019 年 12 月结束。 如本支持声明所述，Windows 10 移动版用户将不再有资格从 Microsoft 接收新的安全更新、非安全修补程序、免费的辅助支持选项或联机技术内容更新。 基于对移动 OS 的全面支持，Microsoft Intune 现在将于 2020 年 5 月 11 日结束对 Windows 10 移动版应用的公司门户和 Windows 10 移动版操作系统的支持。

#### <a name="how-does-this-affect-me"></a>这对我有何影响？
如果贵组织中已部署 Windows 10 移动版设备，那么从现在到 2020 年 5 月 11 日，你可以注册新设备、添加或删除策略和应用，或更新任何管理设置。 5 月 11 日之后，我们将停止新的注册，并最终从 Intune UI 中删除 Windows 10 移动版管理。 设备将不再签入 Intune 服务，我们将删除设备和策略数据。  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>我需要如何准备应对此项变化？
你可以查看 Intune 报告，了解可能受影响的设备或用户。 转到“设备”   > “所有设备”  ，并按“OS”进行筛选。 你可以添加附加列，帮助确定你的组织中哪些人员的设备正在运行 Windows 10 移动版。 要求最终用户升级其设备或停止使用这些设备进行公司访问。


### <a name="updated-support-statement-for-adobe-acrobat-reader-for-intune-mobile-app--5746776--"></a>针对“Adobe Acrobat Reader for Intune”移动应用的更新支持声明<!--5746776-->
我们在 8 月底的 MC188653 上得知，Adobe Acrobat Reader for Intune 移动应用将于 2019 年 12 月 1 日到期，且 Adobe 计划在其主要的 Acrobat Reader 应用中支持 Intune 应用保护策略。 自那以后，我们收到客户反馈，我们需要提供更多的时间来继续允许 IT 管理员瞄准目标，并让最终用户开始使用 Adobe Acrobat Reader for Intune。 鉴于 Adobe Acrobat Reader for Intune 在最终用户设备上的高使用率及其在企业场景中的重要性，我们希望确保任何体验都能满足组织的应用保护需求。 

虽然由于 Acrobat Reader 移动应用支持应用保护策略并且已经集成了 Intune SDK，我们仍然建议在策略中面向一般的 Acrobat Reader 移动应用，但 Adobe Acrobat Reader for Intune 应用将继续得到支持至 2020 年 3 月 31 日。 

#### <a name="how-does-this-affect-me"></a>这对我有何影响？
你收到此消息是因为我们的报告表明，贵组织中的一个或多个策略针对的是 Adobe Acrobat Reader for Intune 应用程序，并且/或者你可能已经收到了我们以前的 EOL 通信。 

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>我需要如何准备应对此项变化？
让最终用户和技术支持人员得知晓此更改。 可以使用[公司门户的支持信息功能](../apps/company-portal-app.md#support-information)来建立与 Intune 相关的问题通道。

#### <a name="additional-information"></a>其他信息
https://helpx.adobe.com/acrobat/kb/intune-app-end-of-life.html

### <a name="take-action-use-microsoft-edge-for-your-protected-intune-browser-experience--5728447--"></a>执行操作：使用 Microsoft Edge 获取受保护的 Intune 浏览器体验<!--5728447-->
正如我们在过去一年中一直分享的那样，Microsoft Edge 移动版支持与 Managed Browser 相同的一组管理功能，同时提供了更好的最终用户体验。 为了让 Microsoft Edge 提供强大的体验，我们将停用 Intune Managed Browser。 自 2020 年 1 月 27 日开始，Intune 将不再支持 Intune Managed Browser。  

#### <a name="how-does-this-affect-me"></a>这对我有何影响？ 
自 2020 年 2 月 1 日开始，Google Play 商店或 iOS 应用商店中将不再提供 Intune Managed Browser。 届时，虽然新用户将无法下载 Intune Managed Browser 应用，但你仍可以将新的应用保护策略定向到 Intune Managed Browser。 此外，在 iOS 上，向下推送到已注册 MDM 设备的新 Web 剪辑将在 Microsoft Edge 中打开，而不是在 Intune Managed Browser 中打开。  

2020 年 3 月 31 日，Intune Managed Browser 将从 Azure 控制台中删除。 这意味着你将无法再为 Intune Managed Browser 创建新策略。 现有的 Intune Managed Browser 策略不会受到影响。 Intune Managed Browser 将在控制台中显示为无图标的 LOB 应用程序，但现有策略将仍显示为应用的定向策略。 届时，我们还会在“应用程序保护策略”的“数据保护”部分中删除将 Web 内容重定向到 Intune Managed Browser 的选项。  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>我需要如何准备应对此项变化？ 
若要确保从 Intune Managed Browser 平稳过渡到 Microsoft Edge，我们建议你主动执行以下步骤： 

1. 使用应用保护策略（也称为 MAM）和应用配置设置，将 Microsoft Edge 定向到 iOS 和 Android。 将这些现有策略定向到 Microsoft Edge，即可对 Microsoft Edge 重复使用 Intune Managed Browser 策略。  
2. 确保环境中所有受 MAM 保护的应用都将应用保护策略设置“限制与其他应用的 Web 内容传输”设置为“策略托管浏览器”。 
3. 通过将托管应用配置设置“com.microsoft.intune.useEdge”设置为 true 来定位所有受 MAM 保护的应用。 从下个月的 1911 版本开始，只需配置“限制与其他应用的 Web 内容传输”设置，以在应用保护策略的“数据保护”部分中选中“Microsoft Edge”，即可完成步骤 2 和步骤 3。 

即将支持 iOS 和 Android 上的 Web 剪辑。 发布此支持后，你需要重定向预先存在的 Web 剪辑，以确保它们在 Microsoft Edge 中而不是在 Managed Browser 中打开。 

#### <a name="additional-information"></a>其他信息
如需了解更多信息，请访问有关[将 Microsoft Edge 与应用保护策略结合使用](../apps/manage-microsoft-edge.md)的文档，或查看我们的[支持博客文章](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Use-Microsoft-Edge-for-your-Protected-Intune-Browser-Experience/ba-p/1004269)。

### <a name="end-of-support-for-legacy-pc-management"></a>停止支持旧版 PC 管理

将于 2020 年 10 月 15 日停止支持旧版 PC 管理。 请将设备升级到 Windows 10，并将它们重新注册为“移动设备管理”(MDM) 设备，以便继续由 Intune 托管它们。

[了解详细信息](https://go.microsoft.com/fwlink/?linkid=2107122)


