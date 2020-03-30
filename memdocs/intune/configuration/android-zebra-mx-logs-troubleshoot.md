---
title: 在 Microsoft Intune 中的 Android Zebra 设备上使用 StageNow 日志 - Azure | Microsoft Docs
description: 在安装了 Microsoft Intune 的 Android 设备上使用 StageNow 时，请参阅常见问题和解决方法。 另外，若需了解如何获取日志，请参阅有关如何读取成功日志或错误日志的示例。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/26/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 607e2303cbec9ec7fc069db602d51684b71e6575
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083845"
---
# <a name="troubleshoot-and-see-potential-issues-on-android-zebra-devices-in-microsoft-intune"></a>对 Microsoft Intune 中的 Android Zebra 设备进行故障排除并查看出现的潜在问题



在 Microsoft Intune 中，可以使用 [ Zebra Mobility Extensions (MX) 来管理 Android Zebra 设备](android-zebra-mx-overview.md)。 使用 Zebra 设备时，可以在 StageNow 中创建配置文件以管理设置，并将其上传到 Intune。 Intune 使用 StageNow 应用在设备上应用设置。 StageNow 应用还会在设备上创建用于进行故障排除的详细日志文件。

此功能适用于：

- Android

例如，在 StageNow 中创建配置文件以配置设备。 创建 StageNow 配置文件时，最后一步会生成一个用于测试配置文件的文件。 可以通过设备上的 StageNow 应用使用此文件。

再举一个例子，在 StageNow 中创建一个配置文件，并对其进行测试。 在 Intune 中，添加 StageNow 配置文件，然后将其分配给 Zebra 相关设备。 检查分配的配置文件的状态时，配置文件将显示概要状态。

在这两种情况下，你都可以从 StageNow 日志文件中获取更多详细信息，该文件在每次应用 StageNow 配置文件时都会保存在设备上。

有些问题与 StageNow 配置文件的内容不相关，这些问题不会显示在日志中。

本文介绍了如何读取 StageNow 日志，并列出了可能不会在日志中显示的 Zebra 设备的一些其他潜在问题。

有关此功能的详细信息，请参阅[通过 Zebra Mobility Extensions 使用和管理 Zebra 设备](android-zebra-mx-overview.md)。

## <a name="get-the-logs"></a>获取日志

### <a name="use-the-stagenow-app-on-the-device"></a>在设备上使用 StageNow 应用
当你在计算机上直接使用 StageNow 测试配置文件，而不是使用 [Intune 部署配置文件](android-zebra-mx-overview.md#step-4-create-a-device-management-profile-in-stagenow)时，设备上的 StageNow 应用将保存测试中的日志。 若要获取日志文件，请使用设备上的 StageNow 应用中的“更多(…)”选项  。

### <a name="get-logs-using-android-debug-bridge"></a>使用 Android Debug Bridge 获取日志
要在通过 Intune 部署配置文件后获取日志，请使用 [Android Debug Bridge (adb)](https://developer.android.com/studio/command-line/adb)（打开 Android 网站）将设备连接到计算机。

在设备上，日志保存在 `/sdcard/Android/data/com.microsoft.windowsintune.companyportal/files`

### <a name="get-logs-from-email"></a>通过电子邮件获取日志
要在通过 Intune 部署配置文件后获取日志，最终用户可以使用设备上的电子邮件应用通过电子邮件向你发送日志。 在 Zebra 设备上，打开公司门户应用，然后[发送日志](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android)。 使用发送日志功能还会创建 PowerLift 事件 ID，如需与 Microsoft 支持部门联系，可参考此 ID。

## <a name="read-the-logs"></a>读取日志

查看日志时，每当查看 `<characteristic-error>` 标记时都会出错。 错误详细信息将写入 `<parm-error>` 标记 > `desc` 属性中。

## <a name="error-types"></a>错误类型

Zebra 设备包括不同的错误报告级别：

- 设备上不支持 CSP。 例如，设备不是移动设备，也没有移动电话管理器。
- MX 或 OSX 版本不匹配。 每个 CSP 都会纳入版本控制。 有关完整的支持矩阵，请参阅 [Zebra 的文档](http://techdocs.zebra.com/mx/)（打开 Zebra 的网站）。
- 设备报告其他问题或错误。

## <a name="examples"></a>示例

例如，你拥有以下输入配置文件：

```xml
<wap-provisioningdoc>
    <characteristic type="Clock">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

在日志中，XML 与输入完全相同。 此匹配的输出表示配置文件已成功应用于设备且没有出错：

```xml
<wap-provisioningdoc>
    <characteristic type="Clock" version="6.0">
        <parm name="AutoTime" value="false"/>
        <parm name="TimeZone" value="GMT-5"/>
        <parm name="Date" value="2014-12-03"/>
        <parm name="Time" value="11:11:11"/>
    </characteristic>
</wap-provisioningdoc>
```

再例如，你具有以下输入：

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2" >
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic type="AppMgr" version="4.2" >
        <parm name="Action" value="Install"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic>
</wap-provisioningdoc>
```

日志显示错误，因为它包含 `<characteristic-error>` 标记。 在此场景中，配置文件尝试安装给定路径中不存在的 Android 包 (APK)：

```xml
<wap-provisioningdoc>
    <characteristic type="XmlMgr" version="4.2">
        <parm name="ProcessingMode" value="1"/>
    </characteristic>
    <characteristic-error type="AppMgr" version="5.1" desc="missing">
        <parm-error name="Action" value="Install" desc="apk doesnot exist in the path"/>
        <parm name="APK" value="/sdcard/test.apk"/>
    </characteristic-error>
</wap-provisioningdoc>
```

## <a name="other-potential-issues-with-zebra-devices"></a>Zebra 设备的其他潜在问题

本部分列出了设备管理员在使用 Zebra 设备时可能会遇到的其他问题。 StageNow 日志中不报告这些问题。

### <a name="android-system-webview-is-out-of-date"></a>Android System WebView 已过时

当旧设备使用公司门户应用登录时，用户可能会看到一条消息，该消息指出 System WebView 组件已过时，需要升级。 如果设备已安装 Google Play，请将其连接到 Internet，然后检查更新。 如果设备未安装 Google Play，请获取组件的更新版本，然后将其应用于设备。 或者，更新到 Zebra 发布的最新设备 OS。

### <a name="management-actions-take-a-long-time"></a>管理操作需要很长时间

如果 Google Play 服务不可用，则一些任务最多需要 8 个小时才能完成。 [适用于 Android 的 Intune 公司门户应用的限制](https://support.microsoft.com/help/3211588/limitations-of-intune-company-portal-app-for-android-in-china)（打开另一个 Microsoft 网站）可能是不错的资源。

### <a name="device-spoofing-suspected-shows-in-intune"></a>Intune 中显示“设备涉嫌欺骗”

此错误表示，Intune 怀疑某个非 Zebra 的 Android 设备将其模型和制造商报告为 Zebra 设备。

### <a name="company-portal-app-is-older-than-minimum-required-version"></a>公司门户应用的版本低于所需的最低版本

Intune 可能会更新公司门户应用所需的最低版本。 如果设备上未安装 Google Play，则公司门户应用不会自动更新。 如果所需的最低版本比安装的版本更高，则公司门户应用将停止运行。 使用 [Zebra 设备上的旁加载](android-zebra-mx-overview.md#sideload-the-company-portal-app)更新到最新的公司门户应用。

## <a name="next-steps"></a>后续步骤

[Zebra 讨论板](https://developer.zebra.com/community/home/discussions)（打开 Zebra 的网站）

[通过 Intune 中的 Zebra Mobility Extensions 使用和管理 Zebra 设备](android-zebra-mx-overview.md)
