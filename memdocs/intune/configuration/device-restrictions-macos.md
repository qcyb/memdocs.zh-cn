---
title: Microsoft Intune 中的 macOS 设备设置 - Azure | Microsoft Docs
titleSuffix: ''
description: 添加、配置或创建 macOS 设备上的设置可限制设置密码要求等功能、控制锁屏、使用内置应用、添加限制使用或批准使用的应用、处理蓝牙设备、连接到云进行备份和存储、启用展台模式、添加域以及控制用户如何与 Microsoft Intune 中的 Safari Web 浏览器交互。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 50dd3d245b9a89836e3858d71a7ad124189e0973
ms.sourcegitcommit: e2877d21dfd70c4029c247275fa2b38e76bd22b8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2020
ms.locfileid: "80407853"
---
# <a name="macos-device-settings-to-allow-or-restrict-features-using-intune"></a>便于使用 Intune 允许或限制功能的 macOS 设备设置

本文列出并介绍了可以在 macOS 设备上控制的各种设置。 在移动设备管理 (MDM) 解决方案中，请通过这些设置允许使用或禁用功能、设置密码规则、允许使用或限制使用特定应用等。

我们将这些设置添加到 Intune 中的设备配置配置文件中，然后分配或部署到 macOS 设备。

## <a name="before-you-begin"></a>在开始之前

[创建设备限制配置文件](device-restrictions-configure.md)。

> [!NOTE]
> 这些设置适用于不同的注册类型。 有关不同注册类型的详细信息，请参阅 [macOS 注册](../enrollment/macos-enroll.md)。

## <a name="general"></a>常规

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>设置适用范围：设备注册和自动设备注册

- **定义查找**：“阻止”可阻止用户突出显示某个字词，然后在设备上查找其定义  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许定义查找功能。
- **听写**：设置为“阻止”可阻止用户通过语音输入来输入文本  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许用户使用听写输入功能。
- **内容缓存**：设置为“阻止”可阻止内容缓存  。 内容缓存在设备上本地存储应用数据、Web 浏览器数据、下载内容等。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能会启用内容缓存。

  有关 macOS 上内容缓存的详细信息，请参阅[管理 Mac 上的内容缓存](https://support.apple.com/guide/mac-help/manage-content-caching-on-mac-mchl3b6c3720/mac)（打开另一个网站）。

  此功能适用于：  
  - macOS 10.13 及更高版本

- **延迟软件更新**：“启用”允许用户在设备上显示软件更新时，将更新时间延迟 0-90 天  。 此设置不会控制何时安装或不安装更新。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，在 Apple 发布更新时，OS 可能会在设备上显示软件更新。 例如，如果 Apple 在特定日期发布了 macOS 更新，则该更新自然会大约在发布日期显示在设备上。 允许在不延迟的情况下进行种子生成更新。  

  - **延迟软件更新的可见性**：输入一个 0-90 天之间的值。 延迟到期时，用户会收到通知，通知更新到触发延迟时可用的最早版本的操作系统。

    例如，如果 macOS 更新在 1 月 1 日发布，“延迟可见性”设置为“5 天”，那么此更新不会显示为可用更新    。 在发布后第六天，该更新可用，最终用户可进行安装  。

    此功能适用于：  
    - macOS 10.13.4 及更高版本

- **屏幕截图**：必须将设备注册到 Apple 的自动设备注册 (DEP) 中。 设置为“阻止”可阻止用户保存显示的屏幕截图  。 它还会阻止 Classroom 应用查看远程屏幕。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许用户捕获屏幕截图，并允许 Classroom 应用查看远程屏幕。

### <a name="settings-apply-to-automated-device-enrollment"></a>设置适用范围：自动设备注册

- **通过 Classroom 应用远程观察屏幕**：选择“禁用”  可防止教师使用 Classroom 应用查看学生的屏幕。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许教师查看学生的屏幕。

  若要使用此设置，请将设置“屏幕截图”  设置为“未配置”  （允许屏幕截图）。

- **通过 Classroom 应用以静默方式观察屏幕**：设置为“允许”可让教师无需学生同意即可查看学生的屏幕  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能要求学生在教师查看屏幕之前同意。

  若要使用此设置，请将设置“屏幕截图”  设置为“未配置”  （允许屏幕截图）。

- **学生必须请求退出 Classroom 课堂的权限**：如果选择“需要”，则会强制参加非托管理的 Classroom 课程学生在获得老师的批准后才能退出课程  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许学生在每次选择退出后即可退出课程。

- **教师可在 Classroom 应用中自动锁定设备或应用**：如果选择“允许”，教师无需学生的批准即可锁定其设备或应用  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能需要学生同意，教师才能锁定设备或应用。

- **学生可自动加入 Classroom 课堂**：如果选择“允许”，学生无需提示老师即可加入一个班级  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能需要教师批准后，学生才能加入课程。

## <a name="password"></a>Password

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>设置适用范围：设备注册和自动设备注册

- **密码**：设置为“需要”时，用户必须输入密码才能访问设备  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能不需要密码。 也不强制执行任何限制，如阻止简单密码或设置最小长度。
  - **所需的密码类型**：输入组织所需的密码复杂性级别。 选项包括：
    - **未配置**：Intune 不会更改或更新此设置。
    - **数字**：密码只能使用数字，例如 123456789。
    - **字母数字**：包括大写字母、小写字母和数字字符。

    此功能适用于：  
    - macOS 10.10.3 及更高版本

  - **密码中的非字母数字字符数**：输入密码中所需的复杂字符数，范围为 0-4 个。 复杂字符是一个符号，如 `?`
  - **最短密码长度**：输入密码必须具有的最小长度（介于 4 到 16 个字符之间）。
  - **简单密码**：允许使用简单密码，如 `0000` 或 `1234`。
  - **屏幕锁定后要求输入密码前的最大分钟数**：输入设备在需要密码才能解锁之前必须处于非活动状态的时间长度。 值为空或设置为“未配置”时，Intune 不会更改或更新此设置  。
  - **屏幕锁定前的最大非活动分钟数**：输入设备在屏幕自动锁定前必须处于空闲状态的时间长度。 例如，输入 5 可在空闲 5 分钟后锁定设备。 值为空或设置为“未配置”时，Intune 不会更改或更新此设置  。
  - **密码过期(天)** ：输入在用户必须更改设备密码前，设备密码保持有效的天数（介于 1-65535 天之间）。 例如，要使密码在 90 天后过期，请输入 `90`。 密码到期后，系统会提示用户创建新密码。 如果该值为空，Intune 不会更改或更新此设置。
  - **防止重用以前的密码**：使用此设置可限制用户创建以前用过的密码。 输入以前用过的不能重用的密码数，从 1 到 24。 例如，输入 5 意味着用户不能将其新密码设置为当前密码或以前四个密码中的任何一个。 如果该值为空，Intune 不会更改或更新此设置。

- **阻止用户修改密码**：设置为“阻止”可阻止更改、添加或删除密码  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许添加、更改或删除密码。
- **阻止指纹解锁**：设置为“阻止”可阻止使用指纹解锁设备  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许用户使用指纹对设备解锁。

- **阻止密码自动填充**：设置为“阻止”可阻止在 macOS 上使用“自动填充密码”功能  。 选择“阻止”还有以下影响  ：

  - 系统不会提示用户在 Safari 或任何应用中使用已保存的密码。
  - 自动强密码处于禁用状态，不建议用户使用强密码。

  设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许使用这些功能。

- **阻止密码临近感应请求**：设置为“阻止”可阻止设备从附近的设备请求密码  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许这些密码请求。

- **阻止密码共享**：“阻止”可阻止使用 AirDrop 在设备之间共享密码  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许共享密码。

## <a name="built-in-apps"></a>内置应用

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>设置适用范围：设备注册和自动设备注册

- **阻止 Safari 自动填充**：设置为“阻止”可禁用设备上 Safari 中的自动填充功能  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许用户更改 Web 浏览器中的自动完成设置。
- **阻止相机**：设置为“阻止”可阻止访问设备上的照相机  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许访问设备的照相机。

  Intune 只管理对设备照相机的访问。 它无法访问图片或视频。

- **阻止 Apple Music**：设置为“阻止”可将音乐应用还原为经典模式并禁用音乐服务  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许使用 Apple“音乐”应用。
- **阻止聚焦 Internet 搜索结果**：“阻止”阻止 Spotlight 从 Internet 搜索返回任何结果  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许 Spotlight 搜索连接到 Internet，并获取搜索结果。
- **使用 iTunes 阻止文件传输**：选择“阻止”可禁用应用程序文件共享服务  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许应用程序文件共享服务。

  此功能适用于：  
  - macOS 10.13 及更高版本

## <a name="restricted-apps"></a>受限制的应用

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>设置适用范围：设备注册和自动设备注册

- **受限应用类型列表**：创建不允许用户安装或使用的应用的列表。 选项包括：

  - **未配置**（默认）：Intune 不会更改或更新此设置。 默认情况下，用户有权访问你分配的应用，以及内置的应用。
  - **禁止的应用**：列出不允许用户安装和运行的应用（未由 Intune 托管）。 不阻止用户安装禁止的应用。 如果用户安装了此列表中的应用，则会在 Intune 中报告。
  - **允许的应用：** 列出允许用户安装的应用。 为了保持兼容性，用户不得安装其他应用。 系统会自动允许由 Intune 管理的应用，包括公司门户应用。 不会阻止用户安装不在已批准列表中的应用。 但如果有，则会在 Intune 中报告。

- **应用捆绑 ID**：输入所需的应用的应用[捆绑 ID](bundle-ids-built-in-ios-apps.md)。 可以显示或隐藏内置应用和业务线应用。 可在 Apple 网站上查看[内置的 Apple 应用](https://support.apple.com/HT208094)列表。
- **应用名称**：输入所需应用的应用名称。 可以显示或隐藏内置应用和业务线应用。 可在 Apple 网站上查看[内置的 Apple 应用](https://support.apple.com/HT208094)列表。
- **发布者**：输入应用发布者。

若要将应用添加到这些列表，可以：

- **添加**：选择以创建应用列表。
- 导入包含应用详细信息的 CSV 文件，包括 URL  。 使用 `<app bundle ID>, <app name>, <app publisher>` 格式。 或者，选择“导出”，使用相同的格式创建所添加的应用列表  。

## <a name="connected-devices"></a>已连接的设备

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>设置适用范围：设备注册和自动设备注册

- **阻止 AirDrop**：设置为“阻止”可阻止在设备上使用 AirDrop  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许使用 AirDrop 功能与附近的设备交换内容。
- **阻止 Apple Watch 自动解锁**：选择“阻止”可阻止用户使用其 Apple Watch 解锁 macOS 设备  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许用户使用其 Apple Watch 解锁 macOS 设备。

## <a name="cloud-and-storage"></a>云和存储

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>设置适用范围：设备注册和自动设备注册

- **阻止 iCloud 密钥链同步**：设置为“阻止”可  禁止将密钥链中存储的凭据同步到 iCloud。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许用户同步这些凭据。
- **阻止 iCloud 文档同步**：“阻止”  则阻止 iCloud 同步文档和数据。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许将文档和键值同步到 iCloud 存储空间。
- **阻止 iCloud 邮件备份**：选择“阻止”可阻止 iCloud 同步到 macOS 邮件应用  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许“邮件”同步到 iCloud。
- **阻止 iCloud 联系人备份**：设置为“阻止”可阻止 iCloud 同步设备联系人  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能会允许使用 iCloud 的联系人同步。
- **阻止 iCloud 日历备份**：选择“阻止”可阻止 iCloud 同步到 macOS 日历应用  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许“日历”同步到 iCloud。
- **阻止 iCloud 提醒事项备份**：选择“阻止”可阻止 iCloud 同步到 macOS 提醒事项应用  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许“提醒事项”同步到 iCloud。
- **阻止 iCloud 书签备份**：设置为“阻止”可阻止 iCloud 同步设备书签  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许“书签”同步到 iCloud。
- **阻止 iCloud 备忘录备份**：设置为“阻止”可阻止 iCloud 同步设备备忘录  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许“备忘录”同步到 iCloud。
- **阻止 iCloud 照片库**：设置为“阻止”将禁用 iCloud 照片库，并防止 iCloud 同步设备照片  。 会从设备的本地存储中删除尚未从 iCloud 照片库完全下载的所有照片。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许在设备与 iCloud 照片库之间同步照片。
- **切换**：此功能允许用户在 macOS 设备上启动工作，然后在其他 iOS/iPadOS 或 macOS 设备上继续已开始的工作。 设置为“阻止”可阻止设备上的 Handoff 功能  。 设置为“未配置”（默认）时，Intune 不会更改或更新此设置  。 默认情况下，OS 可能允许在设备上使用此功能。

  此功能适用于：  
  - macOS 10.15 及更高版本

## <a name="domains"></a>域

### <a name="settings-apply-to-device-enrollment-and-automated-device-enrollment"></a>设置适用范围：设备注册和自动设备注册

- **电子邮件域 URL**：向列表添加一个或多个 URL  。 当用户从所配置的域以外的域接收电子邮件时，该电子邮件在 macOS 邮件应用中被标记为不受信任。

## <a name="next-steps"></a>后续步骤

[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

还可以在 [iOS/iPadOS](device-restrictions-ios.md) 设备上限制设备功能和设置。
