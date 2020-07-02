---
title: 软件中心用户指南
titleSuffix: Configuration Manager
description: 了解软件中心的功能和特性
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: end-user-help
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 9e68de6e-2b33-442b-b674-a382728d9529
ms.openlocfilehash: 19b1b56c394fbf71e9117ad12fbe900e6f07e5fb
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715388"
---
# <a name="software-center-user-guide"></a>软件中心用户指南

适用范围：Configuration Manager (Current Branch)

组织的 IT 管理员可使用软件中心安装应用程序和软件更新并升级 Windows。 本用户指南为计算机用户介绍了软件中心的功能。

软件中心会自动安装在 IT 组织管理的 Windows 设备上。 若要开始操作，请参阅[如何打开软件中心](#bkmk_open)。

关于软件中心功能的一般说明：

- 本文介绍软件中心的最新功能。 如果组织正在使用较旧但仍受支持的软件中心版本，则并非所有功能都可用。 有关详细信息，请联系 IT 管理员。

- IT 管理员可能会禁用软件中心的某些方面。 用户的具体体验可能有所不同。

- 如果有多个用户同时使用设备，则具有最低会话 ID 的用户将是唯一可在软件中心内查看所有可用部署的用户。 例如，远程桌面环境中的多个用户。 具有较高会话 ID 的用户可能无法查看软件中心中的某些部署。 例如，具有较高会话 ID 的用户可能会看到已部署的应用程序，但看不到已部署的包或任务序列。 同时，具有最低会话 ID 的用户将看到所有已部署的应用程序、包和任务序列。 Windows 任务管理器的“用户”选项卡显示所有用户及其会话 ID。

- IT 管理员可以更改软件中心的颜色，并添加组织的徽标。

## <a name="how-to-open-software-center"></a><a name="bkmk_open"></a> 如何打开软件中心

软件中心会自动安装在 IT 组织管理的 Windows 设备上。 若要以最简单的方式在 Windows 10 计算机上启动软件中心，请按“开始”并键入 `Software Center`。 你可能无需为 Windows 键入整个字符串就可找到最佳匹配。

:::image type="content" source="media/start-menu-software-center.png" alt-text="“开始”菜单中的软件中心最佳匹配":::

若要在“开始”菜单中导航，请查看“Microsoft Endpoint Manager”组下的“软件中心”图标 。

:::image type="content" source="media/microsoft-endpoint-manager-start-menu.png" alt-text="Microsoft Endpoint Manager“开始”菜单图标":::

> [!NOTE]
> 上述“开始”菜单路径适用于自 2019 年 11 月（版本 1910）起的版本或更高版本。 在更早版本中，文件夹名为“Microsoft System Center”。

如果在“开始”菜单中找不到软件中心，请联系 IT 管理员。

## <a name="applications"></a>应用程序

:::image type="content" source="media/software-center-apps.png" alt-text="软件中心“应用程序”选项卡" lightbox="media/software-center-apps.png":::

选择“应用程序”选项卡 (1)，查找并安装 IT 管理员为用户或此计算机部署的应用程序。

- 全部 (2)：显示可安装的所有可用应用程序。

- 必需 (3)：IT 管理员会强制安装这些应用程序。 如果用户卸载其中一个应用程序，软件中心会重新安装它。

- 筛选器 (4)：IT 管理员可能会创建各种应用程序。 如果可用，请选择下拉列表进行筛选，以便仅查看特定类别的应用程序。 选择“全部”可显示所有应用程序。

- 排序方式 (5)：重新排列应用程序列表。 默认情况下，此列表按“最近的”排序。 最近可用的应用程序显示有“新”横幅，此横幅在七天内可见。

- 搜索 (6)：仍找不到要查找的内容？ 在“搜索”框中输入关键字来查找它！

- 切换视图 (7)：选择图标，在列表视图和磁贴视图之间进行切换。 默认情况下，应用程序列表显示为图形磁贴。

|图标|查看|说明|
|----|----|-----------|
|:::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::|多选模式|一次安装多个应用程序。 有关详细信息，请参阅[安装多个应用程序](#install-multiple-applications)。|
|:::image type="icon" source="media/software-center-apps-list-view.png" border="false":::|列表视图|此视图显示应用程序图标、名称、发布者、版本和状态。|
|:::image type="icon" source="media/software-center-apps-tile-view.png" border="false":::|磁贴视图|IT 管理员可以自定义图标。 在每个磁贴下方显示应用程序名称、发布者和版本。|

### <a name="install-an-application"></a>安装应用程序

从列表中选择一个应用程序以查看其详细信息。 选择“安装”进行安装。 如果已安装应用，则可以选择“卸载”。

某些应用可能需要在安装之前进行审批。

- 尝试安装应用后，可以输入注释，然后请求该应用。

  :::image type="content" source="media/software-center-app-approval-request.png" alt-text="待审批的软件中心应用安装请求":::

- 软件中心显示请求历史记录，你可以取消该请求。

  :::image type="content" source="media/software-center-app-approval-status.png" alt-text="已请求软件中心应用安装":::

- 当管理员批准你的请求时，可以安装应用。 如果需要等待，软件中心会在非营业时间自动安装应用。

  :::image type="content" source="media/software-center-app-approved.png" alt-text="已批准软件中心应用安装":::

### <a name="install-multiple-applications"></a>安装多个应用程序

<!-- 1357126 -->
一次安装多个应用程序，而不是等一个完成后再开始下一个。 所选应用需要满足以下条件：

- 该应用对用户可见
- 尚未下载或安装该应用
- IT 管理员不需要获得批准即可安装该应用

若要一次安装多个应用程序，请执行以下操作：

1. 选择右上角的多选图标：:::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::

2. 选择要安装的两个或多个应用。 选中列表中每个应用左侧的复选框。

3. 选择“安装选定内容”按钮开始安装。

照常安装应用，只是现在连续进行安装。

### <a name="share-an-application"></a>共享应用程序

若要共享指向特定应用的链接，请在选择应用后，选择右上角的“共享”图标：:::image type="icon" source="media/software-center-share-app-icon.png" border="false":::

:::image type="content" source="media/software-center-share-app-window.png" alt-text="从软件中心共享应用":::

复制字符串，并将其粘贴到其他位置，如电子邮件。 例如，`softwarecenter:SoftwareID=ScopeId_73F3BB5E-5EDC-4928-87BD-4E75EB4BBC34/Application_b9e438aa-f5b5-432c-9b4f-6ebeeb132a5a`。 组织中使用软件中心的其他任何人都可以使用该链接打开同一应用程序。

## <a name="updates"></a>更新

:::image type="content" source="media/software-center-updates.png" alt-text="软件中心“更新”选项卡" lightbox="media/software-center-updates.png":::

选择“更新”选项卡 (1) 可查看并安装 IT 管理员部署到此计算机的软件更新。  

- 全部 (2)：显示可安装的所有更新

- 必需 (3)：IT 管理员会强制安装这些更新。

- 排序方式 (4)：重新排列更新列表。 默认情况下，此列表按“应用程序名称：A 到 Z”排序。

- 搜索 (5)：仍找不到要查找的内容？ 在“搜索”框中输入关键字来查找它！

若要安装更新，请选择“全部安装”(6)。

若仅安装特定更新，请选择图标进入多选模式 (7)：:::image type="icon" source="media/software-center-multi-select-apps.png" border="false":::
检查要安装的更新，然后选择“安装选定更新”。

## <a name="operating-systems"></a>操作系统

:::image type="content" source="media/software-center-os.png" alt-text="软件中心“操作系统”选项卡" lightbox="media/software-center-os.png":::

选择“操作系统”选项卡 (1) 可查看并安装 IT 管理员部署到此计算机的 Windows 版本。  

- 全部 (2)：显示可安装的所有 Windows 版本

- 必需 (3)：IT 管理员会强制执行这些升级。

- 排序方式 (4)：重新排列更新列表。 默认情况下，此列表按“应用程序名称：A 到 Z”排序。

- 搜索 (5)：仍找不到要查找的内容？ 在“搜索”框中输入关键字来查找它！

## <a name="installation-status"></a>安装状态

选择“安装状态”选项卡可查看应用程序的状态。 用户可能会看到以下状态：

- **已安装**：软件中心已在此计算机上安装此应用程序。

- **正在下载**：软件中心正在下载要在此计算机上安装的软件。

- **失败**：软件中心无法安装软件。

- **计划在以下时间后安装**：显示在设备下一个维护时段安装即将推出的软件的日期和时间。 维护时段由 IT 管理员定义。<!--1358131-->

  - 可在“全部”和“即将进行”选项卡中查看状态 。

  - 可选择“立即安装”按钮，在维护时段时间之前进行安装。

## <a name="device-compliance"></a>设备符合性

选择“设备符合性”选项卡可查看此计算机的符合性状态。

选择“检查符合性”可根据 IT 管理员定义的安全策略评估此设备的设置。

## <a name="options"></a>选项

选择“选项”选项卡可查看此计算机的其他设置。

### <a name="work-information"></a>工作信息

指示用户平时的工作时间。 IT 管理员在安排软件安装时可能会避开用户的工作时间。 每天至少留出四小时执行系统维护任务。 IT 管理员仍可以在工作时间安装关键应用程序和软件更新。

- 选择此计算机的最早使用时间和最晚使用时间。 这些值默认为“早上 5:00”到“晚上 10:00”。

- 选择通常使用此计算机的每周天数。 默认情况下，软件中心只选择工作日。

指定你是否经常使用此计算机来完成工作。 你的管理员可以自动安装应用程序或为主计算机提供其他应用程序。<!--3485366--> 如果你使用的计算机是主计算机，请选择“我经常使用此计算机工作”。

### <a name="power-management"></a>电源管理

IT 管理员可能会设置电源管理策略。 这些策略可帮助组织在不使用此计算机时节约用电。

若要使此计算机免受这些策略的影响，请选中“不将 IT 部门的电源设置应用于此计算机”。 此设置默认处于禁用状态，计算机将应用电源设置。

### <a name="computer-maintenance"></a>计算机维护

指定软件中心在截止时间前向软件应用更改的方式。

- **仅在指定的工作时间之外自动安装或卸载所需软件并重新启动计算机**：默认情况下，此设置处于禁用状态。

- **当我的计算机处于演示模式时暂停软件中心活动**：默认情况下将启用此设置。

在 IT 管理员的指示下选择“同步策略”。 此计算机会检查服务器中的所有更新，比如应用程序、软件更新或操作系统。

### <a name="remote-control"></a>远程控制

指定计算机的远程访问和远程控制设置。

使用 IT 部门的远程访问设置：默认情况下，IT 部门会定义用于远程协助用户的设置。 此部分中的其他设置显示了 IT 部门所定义的设置的状态。 若要更改任何设置，请先禁用此选项。

- 允许的远程访问级别
  - 不允许远程访问：IT 管理员无法远程访问此计算机来提供帮助。
  - 仅查看：IT 管理员只能远程查看你的屏幕。
  - **全部**：IT 管理员可以远程控制此计算机。 此设置为默认选项。

- **允许管理员在我离开时远程控制此计算机**。 默认情况下，此设置为“是”。

- 当管理员尝试远程控制此计算机时
  - **每次都请求权限**：此设置为默认选项。
  - **不请求权限**

- **远程控制期间显示以下内容**：默认情况下，这些视觉通知都处于启用状态，以便你知道管理员正在远程访问设备。
  - **通知区域中的状态图标**
  - **桌面上的会话连接栏**

- **播放声音**：使用可听到的通知，你就知道管理员正在远程访问设备。
  - **当会话开始和结束时**：此设置为默认选项。
  - **在会话过程中重复**
  - **从不**

## <a name="custom-tabs"></a>自定义选项卡

IT 管理员可以删除默认选项卡，或向软件中心添加其他选项卡。 自定义选项卡由管理员命名，并打开管理员指定的网站。 例如，你可能有一个名为“支持人员”的选项卡，它打开 IT 组织的支持人员网站。 <!--1358132-->

## <a name="more-information-for-it-administrators"></a>为 IT 管理员提供的详细信息

以下文章为 IT 管理员提供了有关如何规划和配置软件中心的详细信息：

- [规划软件中心](../../apps/plan-design/plan-for-software-center.md)
- [软件中心客户端设置](../clients/deploy/about-client-settings.md#software-center)
- [设备重启通知](../clients/deploy/device-restart-notifications.md)
- [远程控制简介](../clients/manage/remote-control/introduction-to-remote-control.md)
