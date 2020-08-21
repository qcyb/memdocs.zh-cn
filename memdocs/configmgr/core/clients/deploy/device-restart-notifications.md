---
title: 设备重新启动通知
titleSuffix: Configuration Manager
description: 重新启动 Configuration Manager 中各种客户端设置的通知行为。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 5ef1bff8-9733-4b5a-b65f-26b94accd210
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: feb9f4206df65ee34228577a9e589ddd1be72870
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127235"
---
# <a name="device-restart-notifications-in-configuration-manager"></a>Configuration Manager 中的设备重新启动通知

适用范围：Configuration Manager (Current Branch)

用户收到等待设备重启的通知可能因[计算机重启客户端设置](#client-settings)和所使用的 Configuration Manager 版本而异。 本文可帮助你配置等待设备重启通知的用户体验。

## <a name="deployment-types-for-restart-notifications"></a>重新启动通知的部署类型

[计算机重新启动客户端设置](#client-settings)可更改需要重新启动以下类型的所有必需部署的用户体验：

- [应用程序](../../../apps/deploy-use/deploy-applications.md)
- [任务序列](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)
- [软件更新](../../../sum/deploy-use/deploy-software-updates.md)

## <a name="restart-notification-types"></a>重新启动通知类型

当设备需要重启时，客户端会向最终用户显示即将重启的通知。

### <a name="toast-notification"></a>Toast 通知

Windows toast 通知会通知用户设备需要重启。 Toast 通知中的信息可能因所运行的 Configuration Manager 版本而异。 此类通知是 Windows 操作系统的本机通知。 你还可以看到第三方软件使用此类通知。

:::image type="content" source="media/3555947-restart-toast.png" alt-text="等待重新启动的 Toast 通知":::

### <a name="software-center-notification-with-snooze"></a>带有推迟按钮的软件中心通知

软件中心将显示一个通知，其中带有一个推迟选项以及在强制设备重启之前的剩余时间。 该消息可能因 Configuration Manager 版本而异。

:::image type="content" source="media/3976435-snooze-restart-countdown.png" alt-text="带有暂停按钮的等待重新启动软件中心通知":::

### <a name="software-center-final-countdown-notification"></a>软件中心最终倒计时通知

软件中心显示此最终倒计时通知，用户无法关闭或推迟此通知。

:::image type="content" source="media/3976435-final-restart-countdown.png" alt-text="软件中心最终倒计时通知":::

从版本 1906 开始，在等待重启时间小于 24 小时之前，用户在重启通知中将无法看到进度条。

### <a name="software-center-notification-before-deadline"></a>截止时间之前的软件中心通知

如果用户在截止时间之前主动安装需要重启的必需软件，他们将看到不同的通知。 当用户体验设置允许通知，并且不使用部署的 Toast 通知时，将显示以下通知。 有关配置这些设置的详细信息，请参阅[部署用户体验设置](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)和[所需部署的用户通知](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)。

:::image type="content" source="media/3976435-proactive-user-restart-notification.png" alt-text="主动安装的软件的通知":::

#### <a name="available-apps"></a>可用应用

当你不使用 Toast 通知时，标记为“可用”的软件的对话框与主动安装的软件类似。 对于可用软件，通知没有重新启动的截止时间，用户可以选择自己的暂停间隔。 有关详细信息，请参阅[批准设置](../../../apps/deploy-use/deploy-applications.md#bkmk_approval)。

:::image type="content" source="media/3555947-deployment-marked-available-restart.png" alt-text="可用软件在通知中没有重启截止时间":::

### <a name="software-center-notification-of-required-restart"></a>提示必须重启的软件中心通知

<!--3601213-->

自版本 2006 起，可以配置客户端设置，以防设备在部署需要时自动重启。 如果必需部署需要重启设备，但你禁用了客户端设置“Configuration Manager 可强制设备重启”，你会看到以下通知：

:::image type="content" source="media/3601213-restart-your-computer.png" alt-text="重启计算机的软件中心通知":::

如果推迟此通知，它将根据你配置重启提醒通知的频率再次显示。 在选择“重启”或手动重启 Windows 之前，设备不会重新启动。

> [!NOTE]
> 默认情况下，Configuration Manager 仍可强制设备重启。

## <a name="client-settings"></a>客户端设置

要控制客户端重启行为，请在“计算机重启”组中配置以下设备客户端设置。 有关详细信息，请参阅[如何配置客户端设置](configure-client-settings.md)。

### <a name="configuration-manager-can-force-a-device-to-restart"></a>Configuration Manager 可强制设备重启

<!--3601213-->

自版本 2006 起，可以配置客户端设置，以防设备在部署需要时自动重启。 Configuration Manager 默认启用此设置。

> [!IMPORTANT]
> 此客户端设置适用于设备上的所有应用程序、软件更新和包部署。 在用户手动重启设备之前：
>
> - 软件更新和应用修订版本可能未完全安装
> - 可能不会安装其他软件

如果禁用此设置，则无法指定设备重启或向用户显示最后倒计时通知的截止时间之后的时间量。

> [!NOTE]
> 若要利用 Configuration Manager 的新功能，更新站点后，还请将客户端更新到最新版本。 尽管在更新站点和控制台时 Configuration Manager 控制台中会显示新功能，但只有在客户端版本也是最新版本之后，完整方案才能正常运行。

### <a name="specify-the-amount-of-time-after-the-deadline-before-a-device-gets-restarted-minutes"></a>指定在最后期限之后、设备重启之前的时间长度(以分钟为单位)

此设置的持续时间必须比应用于计算机的最短维护时段更短。 有关维护时段的详细信息，请参阅[如何使用维护时段](../manage/collections/use-maintenance-windows.md)。

默认值为 90 分钟。 从版本 1906 开始，最大值从 1440 分钟（24小时）增加到 20160 分钟（两周）。

> [!NOTE]
> 此设置之前的标题为“向用户显示一条临时通知，以指明注销用户或重启计算机之前的间隔(分钟)”。

### <a name="specify-the-amount-of-time-that-a-user-is-presented-a-final-countdown-notification-before-a-device-gets-restarted-minutes"></a>指定在设备重启之前向用户显示最后倒计时通知的时间长度(以分钟为单位)

此设置的持续时间必须比应用于计算机的最短维护时段更短。 有关维护时段的详细信息，请参阅[如何使用维护时段](../manage/collections/use-maintenance-windows.md)。

默认值为 15 分钟。

> [!NOTE]
> 此设置之前的标题为“显示用户无法关闭的对话框，该对话框显示注销用户或重启计算机之前的倒计时间隔(分钟)”。

### <a name="specify-the-frequency-of-reminder-notifications-presented-to-the-user-after-the-deadline-before-a-device-gets-restarted-minutes"></a>指定在最后期限之后、重启设备之前向用户显示提醒通知的频率(分钟)
<!--3976435-->
_从版本 1906 开始_

此频率时间间隔值应小于“指定在最后期限之后、设备重启之前的时间长度(以分钟为单位)”的值减去“指定在设备重启之前向用户显示最后倒计时通知的时间长度(以分钟为单位)”的值之差。 否则，提醒通知将不起作用。

默认值为 240 分钟。

> [!NOTE]
> 此设置之前标题为“指定计算机重启倒计时通知的暂停持续时间(分钟)”。

### <a name="when-a-deployment-requires-a-restart-show-a-dialog-window-to-the-user-instead-of-a-toast-notification"></a>当部署要求重启时，向用户显示对话框窗口，而不是 toast 通知
<!--3555947-->
自版本 1902 起，将此设置配置为“是”会增加用户体验的侵入性。 此设置适用于应用程序、任务序列和软件更新的所有部署。 有关详细信息，请参阅[为软件中心制定计划](../../../apps/plan-design/plan-for-software-center.md#bkmk_impact)。

> [!IMPORTANT]
> 在某些情况下，Configuration Manager 1902 中的该对话框将不会替换 Toast 通知。 要解决此问题，请安装 [Configuration Manager 版本1902 的更新汇总](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902)。 <!--4404715-->

## <a name="device-restart-notifications-version-1906"></a>设备重启通知（版本 1906）
<!--3976435-->
某些客户倾向于经常发送重启通知并允许用户推迟较短的时间。 而其他客户允许用户将重启推迟更长一段时间，并且不会经常通知用户等待重启。 从 Configuration Manager 版本 1906 开始，管理员可以更好地控制重启通知的时间和频率。

### <a name="install-required-software-at-or-after-the-deadline"></a>在截止时间或之后安装所需的软件

在截止时间或截止时间之后安装所需软件时，用户将看到因所选客户端设置而异的通知。

如果设置“当部署要求重启时，向用户显示对话框窗口，而不是 toast 通知”设置为：

- **否**：当部署达到最终倒计时通知时，Windows 会显示 toast 通知。

- **是**：软件中心显示通知：

  - 如果重启时间大于 24 小时，则会显示估计的重启时间。 此通知的时间取决于以下设置：**指定在最后期限之后、设备重启之前的时间长度(以分钟为单位)** 。

    :::image type="content" source="media/3976435-notification-greater-than-24-hours.png" alt-text="重新启动时间大于 24 小时":::

  - 如果重启时间小于 24 小时，则会显示一个进度栏。 此通知的时间取决于以下设置：**指定在最后期限之后、设备重启之前的时间长度(以分钟为单位)** 。

    :::image type="content" source="media/3976435-notification-less-than-24-hours.png" alt-text="重新启动时间小于 24 小时":::

如果用户选择“推迟”，则在推迟期过后会显示另一个临时通知。 此行为假设尚未达到最终倒计时。 下一个通知的时间取决于以下设置：**指定在最后期限之后、重启设备之前向用户显示提醒通知的频率(分钟)** 。 如果用户选择“推迟”，而你的推迟间隔为 1 小时，则软件中心将在 60 分钟后再次通知用户。 此行为假设尚未达到最终倒计时。

当它达到最后倒计时时，软件中心会向用户显示无法关闭的通知。 进度条显示为红色，用户不能“推迟”它。

:::image type="content" source="media/3976435-1906-final-restart-countdown.png" alt-text="版本 1906 中的软件中心最终倒计时通知":::

### <a name="proactively-install-required-software-before-the-deadline"></a>在截止时间之前主动安装必需的软件

如果用户在截止时间之前主动安装需要重启的必需软件，他们看到的通知将有所不同。 有关配置这些设置的详细信息，请参阅[部署用户体验设置](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)和[所需部署的用户通知](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)。

当用户体验设置允许通知，并且不使用部署的 Toast 通知时，将显示以下通知：

:::image type="content" source="media/3976435-proactive-user-restart-notification.png" alt-text="主动安装的软件的通知":::

部署达到其截止时间之后，软件中心会遵循此行为[在截止时间或之后安装必需的软件](#install-required-software-at-or-after-the-deadline)。

## <a name="example-configurations"></a>示例配置

下面的示例说明如何配置客户端设置以实现特定的行为。

### <a name="reminders-are-off"></a>提醒已关闭

| 设置 | 值 |
|---------|---------|
|指定在最后期限之后、设备重启之前的时间长度(以分钟为单位)|180|
|指定在设备重启之前向用户显示最后倒计时通知的时间长度(以分钟为单位)|60|
|指定在最后期限之后、重启设备之前向用户显示提醒通知的频率(分钟)|240|
|当部署要求重启时，向用户显示对话框窗口，而不是 toast 通知|否|

设备将在部署截止时间三小时（180 分钟）后重启。 在重启之前一小时（**60** 分钟），用户会看到其无法关闭或推迟的倒计时。 首个提醒通知设置为在晚于重启时间的截止时间四小时（240 分钟）后重启。 因此，用户看不到任何提醒。

### <a name="low-reminder-frequency"></a>低提醒频率

| 设置 | 值 |
|---------|---------|
|指定在最后期限之后、设备重启之前的时间长度(以分钟为单位)|7200|
|指定在设备重启之前向用户显示最后倒计时通知的时间长度(以分钟为单位)|120|
|指定在最后期限之后、重启设备之前向用户显示提醒通知的频率(分钟)|900|
|当部署要求重启时，向用户显示对话框窗口，而不是 toast 通知|是|

设备将在部署截止时间五天（7200 分钟）后重启。 在重启前两小时（120 分钟），用户会看到其无法关闭或推迟的倒计时。 此配置允许在 118 小时内显示提醒 (`(7200 - 120) / 60`)。 截止时间 15 小时（900 分钟）后，软件中心将显示第一个提醒。 每 15 小时（900 分钟）显示最多六个额外提醒。 用户看到提醒作为窗口显示在屏幕上，而不是几秒钟后消失的通知。

### <a name="high-reminder-frequency"></a>高提醒频率

| 设置 | 值 |
|---------|---------|
|指定在最后期限之后、设备重启之前的时间长度(以分钟为单位)|2880|
|指定在设备重启之前向用户显示最后倒计时通知的时间长度(以分钟为单位)|60|
|指定在最后期限之后、重启设备之前向用户显示提醒通知的频率(分钟)|30|
|当部署要求重启时，向用户显示对话框窗口，而不是 toast 通知|是|

设备将在部署截止时间两天（2880 分钟）后重启。 在重启之前一小时（60 分钟），用户会看到其无法关闭或推迟的倒计时。 此配置允许在 47 小时内显示提醒 (`(2880 - 60) / 60`)。 截止时间 30 分钟后，软件中心将显示第一个提醒。 每 30 分钟显示最多 92 个额外提醒。 用户看到提醒作为窗口显示在屏幕上，而不是几秒钟后消失的通知。

## <a name="device-restart-notifications-version-1902"></a>设备重启通知（版本 1902）

<!--3555947-->
有时用户看不到有关重启或必需的部署的 Windows toast 通知。 然后，他们也看不到推迟提醒体验。 当客户端临近截止时间时，此行为可能导致不佳的用户体验。

从版本 1902 开始，在要求进行软件更改或部署需要重新启动时，可以选择使用侵入性更强的对话框窗口。

在客户端设置的[计算机重新启动](#client-settings)组中，启用以下选项：**当部署要求重启时，向用户显示一个对话框窗口而不是 toast 通知**。  

配置此客户端设置可更改需要重新启动 Toast 通知的所有必需部署的用户体验：

:::image type="content" source="media/3555947-restart-toast-initial.png" alt-text="需要重启的 Toast 通知":::

侵入性更强的软件中心对话框窗口：

:::image type="content" source="media/3976435-proactive-user-restart-notification.png" alt-text="重新启动计算机的对话框窗口":::

如果用户在安装后未重新启动其设备，则他们将收到通知作为提醒。 系统会根据客户端设置向用户显示此临时提醒：**向用户显示一条临时通知，指示注销用户或重新启动计算机之前的时间间隔(分钟)** 。 此设置是指在强制重新启动之前，用户必须重新启动计算机的总时间。

- 使用 Toast 通知时的临时通知：

    :::image type="content" source="media/3555947-restart-toast.png" alt-text="等待重新启动的 Toast 通知":::

- 使用软件中心对话框窗口时的临时通知，而不是 Toast 通知：

    :::image type="content" source="media/3555947-1902-hide-notification.png" alt-text="带有暂停按钮的等待重新启动软件中心通知":::

如果用户在收到临时通知后未重新启动，则会为其显示他们无法关闭的最终倒计时通知。 最终通知的显示时间取决于客户端设置：**显示用户无法关闭的对话框，该对话框显示注销用户或重新启动计算机之前的倒计时间隔(分钟)** 。 例如，如果设置为 60，则会在强制重新启动的前一小时向用户显示最终通知：

:::image type="content" source="media/3555947-1902-final-countdown.png" alt-text="软件中心最终倒计时通知":::

以下设置的持续时间必须比应用于计算机的最短[维护时段](../manage/collections/use-maintenance-windows.md)更短：

- **向用户显示一条临时通知，指示注销用户或重新启动计算机之前的间隔(分钟)**
- **显示用户无法关闭的对话框，该对话框显示注销用户或重新启动计算机之前的倒计时间隔(分钟)**

> [!IMPORTANT]
> 在某些情况下，Configuration Manager 1902 中的该对话框将不会替换 Toast 通知。 要解决此问题，请安装 [Configuration Manager 版本1902 的更新汇总](https://support.microsoft.com/help/4500571/update-rollup-for-configuration-manager-current-branch-1902)。 <!--4404715-->

## <a name="log-files"></a>日志文件

若要对设备重启进行故障排除，请在客户端上使用 RebootCoordinator.log 和 SCNotify.log 文件 。 你可能还需要根据特定的部署类型使用其他客户端[日志文件](../../plan-design/hierarchy/log-files.md)。

## <a name="next-steps"></a>后续步骤

- [如何配置客户端设置](configure-client-settings.md)
- [应用程序部署 **“用户体验”设置**](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-ux)
- [所需应用部署的用户通知](../../../apps/deploy-use/deploy-applications.md#bkmk_notify)
