---
title: 适用于托管应用的配置策略（无需设备注册）
titleSuffix: Microsoft Intune
description: 了解如何为托管应用配置策略（无需设备注册）。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: E61C1618-79D0-41A1-B61F-4123FB6672FC
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 42547885c5f791749517415b325c8c785ec52c13
ms.sourcegitcommit: 47ed9af2652495adb539638afe4e0bb0be267b9e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/10/2020
ms.locfileid: "88051397"
---
# <a name="add-app-configuration-policies-for-managed-apps-without-device-enrollment"></a>为受管理应用添加应用配置策略（无需设备注册）

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

可将应用配置策略用于托管应用，这些应用甚至在未注册设备上也支持 Intune App SDK。 

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“应用”   > “应用配置策略”   > “添加”   > “托管应用”  。
3. 在“基本信息”  页上，设置以下详细信息：
    - **名称**：在 Azure 门户中显示的配置文件名称。
    - **描述**：在 Azure 门户中显示的配置文件说明。
    - **设备注册类型**：已选择托管应用。
4. 选择“选择公共应用”  或“选择自定义应用”  以选择要配置的应用。 从已同意并与 Intune 同步的应用列表中选择应用。
5. 单击“下一步”以显示“设置”页面   。
6. “设置页面”提供的选项基于要配置应用进行显示：

    - **常规配置设置** - 对于该应用支持的每个常规配置设置，请键入“名称”和“值” 。 
 
        启用了 Intune App SDK 的应用支持键值对形式的配置。 若要详细了解支持哪些键值配置，请参阅每个应用的相关文档。 请注意，可使用将由应用程序生成的数据动态填充的令牌。 若要删除常规配置设置，请选择省略号 (…)，然后选择“删除” 。 有关详细信息，请参阅[为使用令牌配置值](app-configuration-policies-managed-app.md#configuration-values-for-using-tokens)。 

    - **Outlook 配置设置** - Outlook for iOS 和 Outlook for Android 使管理员能够为多个应用内设置自定义默认配置。 有关详细信息，请参阅 [Outlook for iOS 和 Outlook for Android 常规应用配置方案](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#general-app-configuration-scenarios)。
   
    - **S/MIME** - 安全多用途 Internet 邮件扩展 (S/MIME) 是一种规范，它让用户能够发送和接收数字签名和加密的电子邮件。
        - **启用 S/MIME** - 指定是否要在撰写电子邮件时启用 S/MIME 控件。 默认值：“不配置”。
        - **允许用户更改设置** - 指定是否允许用户更改设置。 必须启用 S/MIME。 默认值：“是”。
        
    有关 Outlook 应用配置策略设置的详细信息，请参阅[部署 Outlook for iOS 和 Outlook for Android 应用配置设置](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune)。

7. 单击“下一步”以显示“分配”页面 。
8. 单击“选择要包含的组”。
9. 在“选择要包含的组”窗格中选择一个组，然后单击“选择”。
10. 单击“选择要排除的组”以显示相关窗格。
11. 选择想要排除的组，然后单击“选择”。

    >[!NOTE]
    >添加组时，如果给定的分配类型中已包括任何其他组，则在其他包括分配类型中，会预先选定该组且无法更改。 因此，已被使用的组无法用作排除组。

12. 单击“下一步”以显示“查看 + 创建”页。
13. 单击“创建”，将应用配置策略添加到 Intune。

## <a name="configuration-values-for-using-tokens"></a>为使用令牌配置值

Intune 可以生成特定令牌，并将其发送至托管的应用程序。 例如，如果应用配置可使用电子邮件设置，则可通过使用令牌添加动态电子邮件。 在“名称”字段键入应用所需名称，然后在“值”字段键入 `{{mail}}` 。

Intune 支持在配置设置中使用以下令牌类型。 不支持其他自定义键/值对。

- \{\{userprincipalname\}\} - 例如 John@contoso.com
- \{\{mail\}\} - 例如 John@contoso.com
- \{\{partialupn\}\} - 例如 John
- \{\{accountid\}\} - 例如 fc0dc142-71d8-4b12-bbea-bae2a8514c81
- \{\{userid\}\} - 例如 3ec2c00f-b125-4519-acf0-302ac3761822
- \{\{username\}\} - 例如 John Doe
- \{\{PrimarySMTPAddress\}\} - 例如 testuser@ad.domain.com

> [!Note]  
> \{\{ 和 \}\} 字符仅供令牌类型使用，不得用于其他目的。

## <a name="next-steps"></a>后续步骤

照常继续[分配](apps-deploy.md)和[监视](apps-monitor.md)应用。
