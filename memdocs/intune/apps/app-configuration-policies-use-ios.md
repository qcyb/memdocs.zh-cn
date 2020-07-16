---
title: 为受管理的 iOS/iPadOS 设备添加应用配置策略
titleSuffix: Microsoft Intune
description: 了解如何使用应用配置策略，为运行中的 iOS/iPadOS 应用提供配置数据。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/10/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c9163693-d748-46e0-842a-d9ba113ae5a8
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 730a8974753575b2726d821106f7b3c937b30207
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2020
ms.locfileid: "86239974"
---
# <a name="add-app-configuration-policies-for-managed-iosipados-devices"></a>为受管理的 iOS/iPadOS 设备添加应用配置策略

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

使用 Microsoft Intune 中的应用配置策略可提供适用于 iOS/iPadOS 应用的自定义配置设置。 基于应用供应商的说明，可利用这些配置设置对应用进行自定义。 必须从应用供应商处获得这些设置配置（键和值）。 要配置应用，需以键和值的形式指定设置，或以包含键和值的 XML 进行指定。

作为 Microsoft Intune 管理员，可控制将哪些用户帐户添加到托管设备上的 Microsoft Office 应用程序。 可以将访问权限限制为仅允许的组织用户帐户，并阻止已注册设备上的个人帐户。 支持性应用程序将处理应用配置并删除和阻止未经批准的帐户。 只要应用检测到配置策略设置（通常在其首次运行时），即会使用它们。

添加应用配置策略后，即可设置应用分配策略的配置。 设置策略分配时，可选择包括和排除应用该策略的用户组。 选择包括一个或多个组时，可以选择要包括的特定组或选择内置组。 内置组包括“所有用户”、“所有设备”和“所有用户 + 所有设备”  。 

> [!NOTE]
> 为方便起见，Intune 在具有内置优化的控制台中提供了预先创建的“所有用户”和“所有设备”组 。 强烈建议针对所有用户和所有设备使用这些组，而不要使用你自己创建的任何“所有用户”或“所有设备”组。

为应用程序配置策略选择了包括的组之后，也可以选择要排除的特定组。 有关详细信息，请参阅[在 Microsoft Intune 中包括和排除应用分配](apps-inc-exl-assignments.md)。

> [!TIP]
> 此策略类型目前仅适用于运行 iOS/iPadOS 8.0 及更高版本的设备。 它支持下列应用安装类型：
>
> - **应用商店的托管 iOS/iPadOS 应用**
> - **iOS 应用包**
>
> 有关应用安装类型的详细信息，请参阅[如何将应用添加到 Microsoft Intune](apps-add.md)。 有关如何将应用配置合并到托管设备的 .ipa 应用包中的详细信息，请参阅 [iOS 开发人员文档](https://developer.apple.com/library/archive/samplecode/sc2279/Introduction/Intro.html)中的托管应用配置。

## <a name="create-an-app-configuration-policy"></a>创建应用配置策略

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“应用” > “应用配置策略” > “添加” > “托管设备”。 请注意，可以在“受管理设备”和“托管应用”之间进行选择。 有关详细信息，请参阅[支持应用配置的应用](app-configuration-policies-overview.md#apps-that-support-app-configuration)。
3. 在“基本信息”页上，设置以下详细信息：
    - **名称** - 在 Azure 门户中显示的配置文件名。
    - **说明** - 在 Azure 门户中显示的配置文件说明。
    - **设备注册类型** - 此设置设为“托管设备”。
4. 选择“iOS/iPadOS”作为“平台”。
5. 单击“目标应用”旁边的“选择应用”。 随即将显示“关联应用”窗格。 
6. 在“目标应用”窗格上，选择要与配置策略关联的托管应用，然后单击“确定”。
7. 单击“下一步”以显示“设置”页面 。
8. 在下拉框中，选择“配置设置格式”。 选择下列方法之一来添加配置信息：
    - **使用配置设计器**
    - **输入 XML 数据**<br><br>
    有关使用配置设计器的详细信息，请参阅[使用配置设计器](#use-configuration-designer)。 有关输入 XML 数据的详细信息，请参阅[输入 XML 数据](#enter-xml-data)。 
9. 单击“下一步”以显示“分配”页面 。
10. 在“分配给”旁边的下拉框中，选择“选定组”、“所有用户”、“所有设备”或“所有用户和所有设备”以分配应用配置策略。

    ![策略分配“包括”选项卡的屏幕截屏](./media/app-configuration-policies-use-ios/app-config-policy01.png)

11. 在下拉框中选择“所有用户”。

    ![策略分配“所有用户”下拉列表选项的屏幕截图](./media/app-configuration-policies-use-ios/app-config-policy02.png)

12. 单击“选择要排除的组”以显示相关窗格。

    ![策略分配“选择要排除的组”窗格的屏幕截图](./media/app-configuration-policies-use-ios/app-config-policy03.png)

13. 选择想要排除的组，然后单击“选择”。

    >[!NOTE]
    >添加组时，如果给定的分配类型中已包括任何其他组，则在其他包括分配类型中，会预先选定该组且无法更改。 因此，已被使用的组无法用作排除组。

14. 单击“下一步”以显示“查看 + 创建”页。
15. 单击“创建”，将应用配置策略添加到 Intune。

## <a name="use-configuration-designer"></a>使用配置设计器

Microsoft Intune 提供对应用而言唯一的配置设置。 可对已注册或未注册 Microsoft Intune 的设备上的应用使用配置设计器。 使用设计器可配置特定配置键和值，有助于创建基础 XML。 还须指定每个值的数据类型。 安装应用时，这些设置会自动提供给应用。

### <a name="add-a-setting"></a>添加设置

1. 对于配置中的每个项和值，请设置以下内容：
   - **配置键** - 对特定设置配置进行唯一标识的键。
   - **值类型** - 配置值的数据类型。 类型包括整数、实数、字符串或布尔值。
   - **配置值** - 该配置的值。
2. 选择“确定”以设置配置设置。

### <a name="delete-a-setting"></a>删除设置

1. 选择设置旁边的省略号 (...)。
2. 选择“删除”。

\{\{ 和 \}\} 字符仅供令牌类型使用，不得用于其他目的。

### <a name="allow-only-configured-organization-accounts-in-multi-identity-apps"></a>仅允许在多身份应用中配置组织帐户 

作为 Microsoft Intune 管理员，你可以控制将哪些工作或学校帐户添加到托管设备上的 Microsoft 应用中。 可以将访问权限限制为仅允许的组织用户帐户，并阻止已注册设备上的个人帐户。 对于 iOS/iPadOS 设备，请在托管设备应用配置策略中使用以下键/值对：

| **Key** | **值** |
|----|----|
| IntuneMAMAllowedAccountsOnly | <ul><li>**启用**：唯一允许的帐户是由 [IntuneMAMUPN](data-transfer-between-apps-manage-ios.md#configure-user-upn-setting-for-microsoft-intune-or-third-party-emm) 键定义的托管用户帐户。</li><li>**禁用**（或任何不是与“启用”值大小写严格匹配的值）：允许任何帐户。</li></ul> |
| IntuneMAMUPN | <ul><li>允许登录到应用中的帐户的 UPN。</li><li> 对于已注册 Intune 的设备，<code>{{userprincipalname}}</code> 令牌可用于表示已注册的用户帐户。</li></ul>  |

   > [!NOTE]
   > 以下应用处理上述应用配置，并且仅允许组织帐户：
   > - iOS 版 Microsoft Edge（44.8.7 和更高版本）
   > - iOS 版 OneDrive（10.34 和更高版本）
   > - iOS 版 Outlook（2.99.0 或更高版本）

## <a name="enter-xml-data"></a>输入 XML 数据

可键入或粘贴 XML 属性列表，此列表包含将设备注册到 Intune 所需的应用配置设置。 根据你所配置的应用，XML 属性列表的格式可能有所不同。 若需了解要使用的确切格式的详细信息，请联系应用供应商。

Intune 会验证 XML 格式。 但是，Intune 不会检查 XML 属性列表 (PList) 是否适用于目标应用。

了解有关 XML 属性列表的详细信息：

- 请参阅 iOS 开发人员库中的[了解 XML 属性列表](https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/PropertyLists/UnderstandXMLPlist/UnderstandXMLPlist.html)。

### <a name="example-format-for-an-app-configuration-xml-file"></a>应用配置 XML 文件的示例格式

在创建应用配置文件时，你可以指定下面的一个或多个使用此格式的值：

```xml
<dict>
  <key>userprincipalname</key>
  <string>{{userprincipalname}}</string>
  <key>mail</key>
  <string>{{mail}}</string>
  <key>partialupn</key>
  <string>{{partialupn}}</string>
  <key>accountid</key>
  <string>{{accountid}}</string>
  <key>deviceid</key>
  <string>{{deviceid}}</string>
  <key>userid</key>
  <string>{{userid}}</string>
  <key>username</key>
  <string>{{username}}</string>
  <key>serialnumber</key>
  <string>{{serialnumber}}</string>
  <key>serialnumberlast4digits</key>
  <string>{{serialnumberlast4digits}}</string>
  <key>udidlast4digits</key>
  <string>{{udidlast4digits}}</string>
  <key>aaddeviceid</key>
  <string>{{aaddeviceid}}</string>
</dict>
```

### <a name="supported-xml-plist-data-types"></a>支持的 XML 属性列表数据类型

Intune 支持属性列表中的以下数据类型：

- &lt;整数&gt;
- &lt;实数&gt;
- &lt;字符串&gt;
- &lt;数组&gt;
- &lt;dict&gt;
- &lt;true /&gt; 或 &lt;false /&gt;

### <a name="tokens-used-in-the-property-list"></a>属性列表中使用的令牌

此外，Intune 支持属性列表中的以下令牌类型：
- \{\{userprincipalname\}\}—例如，John\@contoso.com
- \{\{mail\}\}—例如，John\@contoso.com
- \{\{partialupn\}\} - 例如 John
- \{\{accountid\}\} - 例如 fc0dc142-71d8-4b12-bbea-bae2a8514c81
- \{\{deviceid\}\} - 例如 b9841cd9-9843-405f-be28-b2265c59ef97
- \{\{userid\}\} - 例如 3ec2c00f-b125-4519-acf0-302ac3761822
- \{\{username\}\} - 例如 John Doe
- \{\{serialnumber\}\} - 例如 F4KN99ZUG5V2（用于 iOS/iPadOS 设备）
- \{\{serialnumberlast4digits\}\} - 例如 G5V2（用于 iOS/iPadOS 设备）
- \{\{aaddeviceid\}\} - 例如，ab0dc123-45d6-7e89-aabb-cde0a1234b56

## <a name="configure-the-company-portal-app-to-support-ios-and-ipados-dep-devices"></a>配置公司门户应用，使其支持 iOS 和 iPadOS DEP 设备

DEP（Apple 的设备注册计划）注册与 App Store 版公司门户应用不兼容。 但是，可以使用以下步骤配置公司门户应用以支持 iOS/iPadOS DEP 设备。

1. 在 Intune 中，通过转到“Intune” > “应用” > “所有应用” > “添加”来添加 Intune 公司门户应用（如有必要）。
2. 转到“应用” > “应用配置策略”，为公司门户应用创建应用配置策略。
3. 使用以下 XML 创建应用配置策略。 有关如何创建应用配置策略和输入 XML 数据的详细信息，请参阅[为受管理的 iOS/iPadOS 设备添加应用配置策略](app-configuration-policies-use-ios.md)。

    - 在需要用户关联才能注册的 DEP 设备上使用公司门户：

        ``` xml
        <dict>
            <key>IntuneCompanyPortalEnrollmentAfterUDA</key>
            <dict>
                <key>IntuneDeviceId</key>
                <string>{{deviceid}}</string>
                <key>UserId</key>
                <string>{{userid}}</string>
            </dict>
        </dict>
        ```
    - 在无需用户关联即可注册的 DEP 设备上使用公司门户：

        > [!NOTE]
        > 将登录到公司门户的用户设置为设备的主要用户。

        ``` xml
        <dict>
            <key>IntuneUDAUserlessDevice</key>
            <string>{{SIGNEDDEVICEID}}</string>
        </dict>
        ```     

4. 使用面向所需组的应用配置策略将公司门户部署到设备。 请确保将策略仅部署到已注册 DEP 的设备组。
5. 告诉最终用户在自动安装公司门户应用后登录到该应用。

## <a name="monitor-iosipados--app-configuration-status-per-device"></a>监视每个设备的 iOS/iPadOS 应用配置状态 
分配配置策略后，可监视每个受管理设备的 iOS/iPadOS 应用配置状态。   从 Azure 门户的“Microsoft Intune”中，选择“设备” > “所有设备”。 从受管理设备列表中选择特定设备，以显示该设备的窗格。 在该设备的窗格上，选择“应用配置”。  

## <a name="additional-information"></a>其他信息

- [部署 Outlook for iOS/iPadOS 和 Outlook for Android 应用配置设置](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune)

## <a name="next-steps"></a>后续步骤

继续[分配](apps-deploy.md)和[监视](apps-monitor.md)应用。
