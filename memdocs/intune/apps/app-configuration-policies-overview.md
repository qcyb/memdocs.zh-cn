---
title: Microsoft Intune 的应用配置策略
titleSuffix: ''
description: 了解如何在 Microsoft Intune 中的 iOS/iPadOS 或 Android 设备上使用应用配置策略。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/06/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 834B4557-80A9-48C0-A72C-C98F6AF79708
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8e5abdfe69d5553be420d96da60f34df93a6b2f4
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083675"
---
# <a name="app-configuration-policies-for-microsoft-intune"></a>Microsoft Intune 的应用配置策略

借助应用配置策略，可在用户运行应用之前向已分配给他们的策略分配配置设置，从而消除应用设置问题。 当应用程序在最终用户设备上配置时，这些设置会自动提供，最终用户无需采取执行任何操作。 每个应用的配置设置都是唯一的。 

可创建并使用应用配置策略提供适用于 iOS/iPadOS 或 Android 应用的配置设置。 通过这些配置设置可以使用应用配置和管理对应用进行自定义。 只要应用检测到配置策略设置（通常在应用首次运行时），就会使用这些设置。 

例如，应用配置设置可能要求指定以下任意详细信息：

- 自定义端口号
- 语言设置
- 安全设置
- 公司徽标之类的品牌设置

如果最终用户要改为输入这些设置，则可能会错误地执行此操作。 应用配置策略有助于跨企业提供一致性，并减少来自最终用户尝试自行配置设置的技术支持呼叫。 通过使用应用配置策略，可以更轻松、更快速地采用新的应用。

可用配置参数最终由应用程序的开发人员决定。 应查看应用程序供应商提供的文档，以了解应用是否支持配置以及哪些配置可用。 对于某些应用程序，Intune 将填充可用的配置设置。 

> [!NOTE]
> 在托管的 Google Play 商店中，将按如下所示标记支持配置的应用：
> 
> ![已配置的应用的屏幕截图](./media/app-configuration-policies-overview/configured-app.png)
>
> 使用托管设备作为 Android 设备的注册类型时，只能看到[托管的 Google Play 商店](https://play.google.com/work)中的应用，而不是 [Google Play 商店](https://play.google.com/store/apps)中的应用。 托管的 Google Play 商店（也称为 Android for Work (AfW) 和 Android Enterprise）是工作配置文件中的应用，工作配置文件中还包含支持应用配置的应用版本。

可通过将[包括和排除分配](apps-inc-exl-assignments.md)相结合来向一组最终用户和设备分配应用配置策略。 添加应用配置策略后，即可设置应用分配策略的配置。 设置策略分配时，可选择包括和排除应用该策略的最终用户 [组](../fundamentals/groups-add.md)。 选择包括一个或多个组时，可以选择要包括的特定组或选择内置组。 内置组包括“所有用户”、“所有设备”和“所有用户 + 所有设备”    。

在 Intune 中使用应用配置策略有两个选项：
- **受管理设备** - 设备由 Intune 作为移动设备管理 (MDM) 提供程序进行管理。 应用必须设计为支持应用配置。
- **托管应用** - 已开发的用于集成 Intune App SDK 的应用。 这就是不要求注册的移动应用管理 ([MAM-WE](app-management.md#mobile-application-management-mam-basics))。 还可包装应用程序以实现和支持 Intune App SDK。 如需获取包装应用的详细信息，请参阅[针对应用保护策略准备业务线应用](../developer/apps-prepare-mobile-application-management.md)。

    > [!NOTE]
    > Intune 托管应用将在与 Intune 应用保护策略一起部署时进行签入，其中 Intune 应用配置策略状态的间隔为 30 分钟。 如果没有为用户分配 Intune 应用保护策略，则 Intune 应用配置策略签入间隔设置为 720 分钟。

## <a name="apps-that-support-app-configuration"></a>支持应用配置的应用

### <a name="managed-devices"></a>托管设备
可对支持应用配置策略的应用使用该策略。 要在 Intune 中支持应用配置，应用必须编写为支持使用由 OS 定义的应用配置。 有关支持的应用配置密钥的详细信息，请咨询应用供应商。

### <a name="managed-apps"></a>托管应用
可通过如下方式准备业务线应用：将 [Intune App SDK](../developer/app-sdk.md) 合并到应用，或使用 [Intune App Wrapping Tool](../developer/apps-prepare-mobile-application-management.md) 在开发应用后对其进行包装。 Intune App SDK 努力使应用开发者所需的代码更改数量降到最低。 有关详细信息，请参阅 [Intune App SDK 概述](../developer/app-sdk.md)。 有关 Intune App SDK 与 Intune App Wrapping Tool 之间的比较，请参阅[针对应用保护策略准备业务线应用](../developer/apps-prepare-mobile-application-management.md#feature-comparison)。

选择“托管应用”作为设备注册类型特指由 Intune 配置策略在设备（未在设备管理中进行注册）上配置的应用，而“托管设备”则是指通过 MDM 通道部署的应用，因此由 Intune 管理    。 根据这些说明选择合适的选项。 

![设备注册类型](./media/app-configuration-policies-overview/device-enrollment-type.png)

> [!NOTE]
> 对于多标识应用（如 Microsoft Outlook），可以考虑用户首选项。 例如，重点收件箱将遵循用户设置，而不会更改配置。 使用其他参数可控制用户是否可以或不可以更改设置。 有关详细信息，请参阅[部署 Outlook for iOS/iPadOS 和 Outlook for Android 应用配置设置](https://docs.microsoft.com/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune)。

## <a name="validate-the-applied-app-configuration-policy"></a>验证托管应用配置策略

可使用以下三种方法来验证应用配置策略：

   1. 在设备上的可见。 目标应用是否会展示在应用配置策略中应用的行为？
   2. 通过诊断日志（请参阅下面的“诊断日志”部分）。
   3. 在 Intune 门户中。 策略的“监视”部分可提供相关状态  ：

      ![设备安装状态的第一个屏幕截图](./media/app-configuration-policies-overview/device-install-status-1.png)

      ![设备安装状态的第二个屏幕截图](./media/app-configuration-policies-overview/device-install-status-2.png)

      此外，在屏幕左侧的“Intune” -> “设备” -> “所有设备”下，“应用配置”选项将显示所有已分配的策略及其状态     ：

      ![应用配置的屏幕截图](./media/app-configuration-policies-overview/app-configuration.png)

## <a name="diagnostic-logs"></a>诊断日志

### <a name="iosipados-configuration-on-unmanaged-devices"></a>非托管设备上的 iOS/iPadOS 配置

可以在托管应用配置的非托管设备上使用 Intune 诊断日志  验证 iOS/iPadOS 配置。 除以下步骤外，还可以使用 Microsoft Edge 访问托管的应用日志。 有关详细信息，请参阅[在 iOS/iPadOS 上使用 Microsoft Edge 访问托管的应用日志](manage-microsoft-edge.md#use-microsoft-edge-to-access-managed-app-logs)。

1. 如果尚未安装在设备上，请从应用商店下载并安装 Microsoft Edge  。 有关详细信息，请参阅[受 Microsoft Intune 保护的应用](apps-supported-intune-apps.md)。
2. 启动 Microsoft Edge  ，并从导航栏中选择“关于”   > “Intune 帮助”  。
3. 单击“开始使用”  。
4. 单击“共享日志”  。
5. 使用你选择的邮件应用将日志发送给你自己，以便可以在你的电脑上查看它们。 
6. 查看文本文件查看器中的 IntuneMAMDiagnostics.txt  。
7. 搜索 `ApplicationConfiguration`。 结果将显示如下：

    ``` JSON
        {
            (
                {
                    Name = "com.microsoft.intune.mam.managedbrowser.BlockListURLs";
                    Value = "https://www.aol.com";
                },
                {
                    Name = "com.microsoft.intune.mam.managedbrowser.bookmarks";
                    Value = "Outlook Web|https://outlook.office.com||Bing|https://www.bing.com";
                }
            );
        },
        {
            ApplicationConfiguration =             
            (
                {
                Name = IntuneMAMUPN;
                Value = "CMARScrubbedM:13c45c42712a47a1739577e5c92b5bc86c3b44fd9a27aeec3f32857f69ddef79cbb988a92f8241af6df8b3ced7d5ce06e2d23c33639ddc2ca8ad8d9947385f8a";
                },
                {
                Name = "com.microsoft.outlook.Mail.NotificationsEnabled";
                Value = false;
                }
            );
        }
    ```

应用程序配置详细信息应与为租户配置的应用程序配置策略匹配。 

![目标应用配置](./media/app-configuration-policies-overview/targeted-app-configuration-3.png)

### <a name="iosipados-configuration-on-managed-devices"></a>托管设备上的 iOS/iPadOS 配置

可以在托管应用配置的托管设备上使用 Intune 诊断日志  验证 iOS/iPadOS 配置。

1. 如果尚未安装在设备上，请从应用商店下载并安装 Microsoft Edge  。 有关详细信息，请参阅[受 Microsoft Intune 保护的应用](apps-supported-intune-apps.md)。
2. 启动 Microsoft Edge  ，并从导航栏中选择“关于”   > “Intune 帮助”  。
3. 单击“开始使用”  。
4. 单击“共享日志”  。
5. 使用你选择的邮件应用将日志发送给你自己，以便可以在你的电脑上查看它们。 
6. 查看文本文件查看器中的 IntuneMAMDiagnostics.txt  。
7. 搜索 `AppConfig`。 结果应与为租户配置的应用程序配置策略匹配。

### <a name="android-configuration-on-managed-devices"></a>托管设备上的 Android 配置

可以在托管应用配置的托管设备上使用 Intune 诊断日志  验证 iOS/iPadOS 配置。

若要从 Android 设备中收集日志，你或最终用户必须通过 USB 连接（或设备上等效的文件资源管理器  ）从设备下载日志。 下面是相关步骤：

1. 使用 USB 电缆将 Android 设备连接到计算机。
2. 在计算机上，查找具有你的设备名的目录。 在该目录中，查找 `Android Device\Phone\Android\data\com.microsoft.windowsintune.companyportal`。
3. 在 `com.microsoft.windowsintune.companyportal` 文件夹中，打开 Files 文件夹并打开 `OMADMLog_0`。
3. 搜索 `AppConfigHelper` 以查找与应用配置相关的消息。 结果将如以下数据块所示：

    `2019-06-17T20:09:29.1970000       INFO   AppConfigHelper     10888  02256  Returning app config JSON [{"ApplicationConfiguration":[{"Name":"com.microsoft.intune.mam.managedbrowser.BlockListURLs","Value":"https:\/\/www.aol.com"},{"Name":"com.microsoft.intune.mam.managedbrowser.bookmarks","Value":"Outlook Web|https:\/\/outlook.office.com||Bing|https:\/\/www.bing.com"},{"Name":"com.microsoft.intune.mam.managedbrowser.homepage","Value":"https:\/\/www.arstechnica.com"}]},{"ApplicationConfiguration":[{"Name":"IntuneMAMUPN","Value":"AdeleV@M365x935807.OnMicrosoft.com"},{"Name":"com.microsoft.outlook.Mail.NotificationsEnabled","Value":"false"},{"Name":"com.microsoft.outlook.Mail.NotificationsEnabled.UserChangeAllowed","Value":"false"}]}] for user User-875363642`
    
## <a name="graph-api-support-for-app-configuration"></a>应用配置的图形 API 支持

可使用图形 API 完成应用配置任务。 有关详细信息，请参阅[针对 Graph API 参考 MAM 的配置](https://docs.microsoft.com/graph/api/resources/intune-shared-targetedmanagedappconfiguration?view=graph-rest-beta)。有关 Intune 和 Graph 的详细信息，请参阅[在 Microsoft Graph 中使用 Intune](https://docs.microsoft.com/graph/api/resources/intune-graph-overview?view=graph-rest-beta)。

## <a name="troubleshooting"></a>疑难解答

### <a name="using-logs-to-show-a-configuration-parameter"></a>使用日志显示配置参数
当日志显示已确认要应用但看起来不起作用的配置参数时，应用开发人员可能会遇到配置实现问题。 请首先与应用程序开发人员联系，或检查其知识库，这可免去与 Microsoft 支持联系。 如果在应用中处理配置的方式有问题，则必须在该应用的未来更新版本中解决此问题。

## <a name="next-steps"></a>后续步骤

### <a name="managed-devices"></a>托管设备

- 了解如何将应用配置用于 iOS/iPadOS 设备。  请参阅[为受管理的 iOS/iPadOS 设备添加应用配置策略](app-configuration-policies-use-ios.md)。
- 了解如何将应用配置用于 Android 设备。  请参阅[为受管理的 Android 设备添加应用配置策略](app-configuration-policies-use-android.md)。

### <a name="managed-apps"></a>托管应用

- 了解如何将应用配置用于受管理的应用。 请参阅[为受管理应用添加应用配置策略（无需设备注册）](app-configuration-policies-managed-app.md)。
