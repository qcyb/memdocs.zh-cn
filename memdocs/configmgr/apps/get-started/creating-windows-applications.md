---
title: 创建 Windows 应用程序
titleSuffix: Configuration Manager
description: 了解有关在 Configuration Manager 中创建和部署 Windows 应用程序的详细信息。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 9e59d850a78a8f45f93769003e7a1de99e5634b3
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906388"
---
# <a name="create-windows-applications-in-configuration-manager"></a>在 Configuration Manager 中创建 Windows 应用程序

适用范围：  Configuration Manager (Current Branch)

除了[创建应用程序](../deploy-use/create-applications.md)的其他 Configuration Manager 要求和过程，在创建和部署适用于 Windows 设备的应用程序时还需考虑以下注意事项。  

## <a name="general-considerations"></a><a name="bkmk_general"></a> 一般注意事项  

Configuration Manager 支持为 Windows 8.1 和 Windows 10 设备部署 Windows 应用包 (.appx) 和应用程序包 (.appxbundle) 格式。

在 Configuration Manager 控制台中创建应用程序时，请将应用程序安装文件“类型”选为“Windows 应用包”（\*.appx、\*.appxbundle、\*.msix、\*.msixbundle）   。 有关一般情况下创建应用的详细信息，请参阅[创建应用程序](../deploy-use/create-applications.md)。 有关 MSIX 格式的详细信息，请参阅[支持 MSIX 格式](#bkmk_msix)。

> [!Note]  
> 若要利用新的 Configuration Manager 功能，请先将客户端更新到最新版本。 尽管在更新站点和控制台时 Configuration Manager 控制台中会显示新功能，但只有在客户端版本也是最新版本之后，完整方案才能正常运行。<!--SCCMDocs issue 646-->  

## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a><a name="bkmk_provision"></a> 为设备上的所有用户预配 Windows 应用包
<!--1358310-->
为设备上的所有用户预配包含 Windows 应用包的应用程序。 此方案的一个常见示例是将来自适用于企业和适用于教育的 Microsoft Store 的应用（如 Minecraft: Education Edition）预配到学校学生使用的所有设备。 以前，Configuration Manager 仅支持按用户安装这些应用程序。 登录到新的设备后，学生不得不等会儿时间来访问应用。 现在，将应用预配到所有用户的设备时，他们的工作更快更高效。

> [!Important]  
> 在设备上安装、预配和更新相同 Windows 应用包的不同版本时要小心，否则可能会导致意外的结果。 使用 Configuration Manager 预配应用时就需要注意些，但随后用户可从 Microsoft Store 更新应用。 有关详细信息，请在[管理来自适用于企业的 Microsoft Store 的应用](../deploy-use/manage-apps-from-the-windows-store-for-business.md#next-steps)时参阅下一步指南。  

当预配脱机许可应用时，Configuration Manager 不允许 Windows 从 Microsoft Store 自动更新它。  

Configuration Manager 在 Windows 10 所有受支持的版本上支持应用预配。<!--SCCMDocs-pr issue 2762-->

<!--
- Install action: Windows 10, version 1607 and later
- Uninstall action: Windows 10, version 1703 and later
-->

若要配置此功能的 Windows 应用部署类型，请启用“为设备上的所有用户预配此应用程序”选项  。 有关详细信息，请参阅[创建应用程序](../deploy-use/create-applications.md)。

> [!Note]  
> 如果需要从用户已经登录的设备中卸载已预配的应用程序，则需要创建两个卸载部署。 将第一个卸载部署定位到包含设备的设备集合。 将第二个卸载部署定位到包含已登录到具有预配应用程序的设备的用户的用户集合。 当在设备上卸载预配的应用时，Windows 当前不会为用户卸载该应用。

## <a name="support-for-msix-format"></a><a name="bkmk_msix"></a>支持 MSIX 格式
<!--1357427-->

Configuration Manager 支持 Windows 10 应用包 (.msix) 和应用程序包 (.msixbundle) 格式。 Windows 10 版本 1809 或更高版本支持这些格式。

- 有关 MSIX 的概述，请参阅 [MSIX 详解](https://docs.microsoft.com/archive/blogs/sgern/a-closer-look-at-msix)。  

- 有关如何创建新的 MSIX 应用，请参阅 [Insider 内部版本 17682 中引入的 MSIX 支持](https://techcommunity.microsoft.com/t5/MSIX-Blog/MSIX-support-introduced-in-Insider-Build-17682/ba-p/202376)。  

### <a name="convert-applications-to-msix"></a>将应用程序转换为 MSIX
<!--3607729, fka 1359029-->

请将现有 Windows Installer (.msi) 应用程序转换为 MSIX 格式。

#### <a name="prerequisites-for-msix"></a>MSIX 的先决条件

- 运行 Windows 10 版本 1809 或更高版本的引用设备  

- 以具有本地管理权限的用户的身份在此设备上登录到 Windows  

- 在此设备上安装以下应用：  

  - Configuration Manager 控制台  

  - 从 Microsoft Store 安装 [MSIX 打包工具](https://www.microsoft.com/store/productId/9N5LW3JBCXKF)  

  - 安装 [MSIX 打包工具驱动程序](https://docs.microsoft.com/windows/msix/packaging-tool/tool-known-issues#frameworks-and-drivers)<!--SCCMDocs-pr issue #3091-->  

不要在此设备上安装任何其他应用或服务。 此设备是你的参考系统。

#### <a name="process-to-convert-applications-to-msix-format"></a>将应用程序转换为 MSIX 格式的过程

1. 提升 Configuration Manager 控制台，转到“软件库”  工作区，展开“应用程序管理”  ，然后选择“应用程序”  节点。  

2. 选择具有 Windows Installer (.msi) 部署类型的应用程序。  

    > [!Note]  
    > 你需要能够从引用设备访问应用程序的源内容。  
    >
    > 应用程序的名称不能包含任何特殊字符。 Configuration Manager 将应用名称用作输出文件的名称。  
    >
    > 不要提前在引用设备上安装此应用程序。  

3. 选择功能区中的“转换为 .MSIX”  。

向导完成后，MSIX 打包工具将在向导中指定的位置创建一个 MSIX 文件。 在此过程中，Configuration Manager 将以无提示方式在引用设备上安装应用程序。

如果该过程失败，则摘要页指向含有更多信息的日志文件。 如果出现有关捕获用户状态的错误，请从 Windows 注销。 重新登录可能会解决此问题。

若要使用此 MSIX 应用，首先需要对其进行数字签名，以便客户端信任此应用。 有关此过程的详细信息，请参阅以下文章：

- [MSIX – MSIX 打包工具 –对 MSIX 程序包进行签名](https://docs.microsoft.com/archive/blogs/sgern/msix-the-msix-packaging-tool-signing-the-msix-package)
- [如何使用 SignTool 对应用程序包进行签名](https://docs.microsoft.com/windows/desktop/appxpkg/how-to-sign-a-package-using-signtool)

对应用进行签名后，在 Configuration Manager 中的应用程序上创建一个新的部署类型。 有关详细信息，请参阅[为应用程序创建部署类型](../deploy-use/create-applications.md#bkmk_create-dt)。

## <a name="task-sequence-deployment-type"></a><a name="bkmk_tsdt"></a> 任务序列部署类型

<!--3555953-->

> [!Note]  
> 在该 Configuration Manager 版本中，任务序列部署类型是预发行功能。 若要启用此功能，请参阅[预发行功能](../../core/servers/manage/pre-release-features.md)。  

从版本 2002 开始，可以通过应用程序模型使用任务序列安装复杂的应用程序。 将任务序列部署类型添加到应用，以安装或卸载应用。 此部署类型提供以下行为：

<!-- - Deploy an app task sequence to a user collection -->

- 在“软件中心”中使用图标显示应用任务序列。 通过图标，用户可以更轻松地查找和识别应用任务序列。

- 为应用任务序列定义其他元数据，包括本地化信息

只能在应用上添加非 OS 部署任务序列作为部署类型。 不支持影响较大的 OS 部署或 OS 升级任务序列。 <!--A user-targeted deployment still runs in the user context of the local System account.-->

将此部署类型添加到应用时，请在“任务序列”页面上配置其属性  。 有关详细信息，请参阅[部署类型“任务序列”选项](../deploy-use/create-applications.md#bkmk_dt-ts)  。

### <a name="prerequisites-for-a-task-sequence-deployment-type"></a>任务序列部署类型的先决条件

创建自定义任务序列：

- 仅使用非 OS 部署步骤，例如：安装包、运行命令行或运行 PowerShell 脚本    。 有关包括支持步骤的完整列表在内的详细信息，请参阅[为非 OS 部署创建任务序列](../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)。

- 在任务序列属性的“用户通知”选项卡上，请勿为影响较大的任务序列选择此选项  。

<!-- - If you use the **Install Application** step in the task sequence, don't add an app to that step that has a task sequence deployment type. -->

创建应用程序时，若要添加任务序列部署类型，你的用户帐户需要具备读取任务序列的权限。<!-- 6348976 --> 可使用下列选项之一配置这些权限：

- 将应用管理员的用户帐户添加到内置的“只读分析员”角色  。 此角色允许用户查看所有 Configuration Manager 对象。

- 复制内置的“应用程序管理员”角色以创建自定义角色  。 在“任务序列包”对象上添加读取权限   。

### <a name="known-issues-for-a-task-sequence-deployment-type"></a>任务序列部署类型的已知问题

- 暂时无法将应用任务序列部署到用户集合

- 请勿在此任务序列中使用“安装应用程序”步骤  。 使用[安装包](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage)步骤来安装应用。

## <a name="support-for-universal-windows-platform-uwp-apps"></a><a name="bkmk_uwp"></a> 对通用 Windows 平台 (UWP) 应用的支持  

Windows 10 设备无需旁加载密钥即可安装业务线应用。 但是，若要在 Windows 上启用旁加载，注册表项 `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps` 的值必须为 1  。  

如果未配置此注册表项，Configuration Manager 在第一次向设备部署应用时自动将此值设置为 1  。 如果将此值设置为 0，则 Configuration Manager 无法自动更改此值，业务线应用部署失败  。  

数字签名 UWP 业务线应用。 使用在部署应用的每台设备上受信任的代码签名证书。 使用组织 PKI 中的证书，或从 Windows 已信任其公共根证书的第三方提供程序购买证书。  

若要对移动应用包进行签名，请使用下表确定要使用的代码签名证书的类型：

| 包  | Symantec  | 非 Symantec  |
|---------|---------|---------|
| Windows 10 移动设备上的通用 .appx 包  | 是 | 是 |
| .xap 包  | 是 | 否 |
| 为 Windows Phone 8.1 生成的 .appx 包，可在 Windows 10 移动设备上安装  | 是 | 否 |

## <a name="deploy-windows-installer-apps-to-mdm-enrolled-windows-10-devices"></a><a name="bkmk_mdm-msi"></a> 将 Windows Installer 应用部署到已注册 MDM 的 Windows 10 设备  

**通过 MDM 的 Windows Installer (\*.msi)** 部署类型可用于创建基于 Windows Installer 的应用并将其部署到运行 Windows 10 且已注册 MDM 的设备上。  

使用此部署类型时，请考虑以下几点：

- 仅上传具有 MSI 扩展的单个文件。  

- Configuration Manager 使用文件的产品代码和产品版本进行应用检测。  

- Windows 使用应用的默认重启行为。 Configuration Manager 不会控制应用重启行为。  

- 为单个用户安装每用户 MSI 包。  

- 为设备上的所有用户安装每计算机 MSI 包。  

- Configuration Manager 支持应用更新。 每个版本的 MSI 产品代码必须相同。  
