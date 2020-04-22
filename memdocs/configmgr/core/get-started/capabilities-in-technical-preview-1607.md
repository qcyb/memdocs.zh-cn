---
title: Technical Preview 1607 中的功能
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview（版本 1607）中的可用功能。
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bb69547-3370-4860-96b0-7fb600c56482
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 7ec5802a8931bc4397eaf302920f09d8597802fe
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705555"
---
# <a name="capabilities-in-technical-preview-1607-for-configuration-manager"></a>Configuration Manager Technical Preview 1607 中的功能

适用范围：*Configuration Manager（技术预览版分支）*

本文介绍 Configuration Manager Technical Preview 1607 中提供的功能。 你可以安装此版本，以更新 Technical Preview 站点的功能并向其添加新功能。      在安装此版本的技术预览版前，请查看介绍性主题 [Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用技术预览版的常规要求和限制、如何在版本之间进行更新，以及如何提供关于技术预览版中的功能的反馈。    


**以下是此版本可以试用的新功能。**  

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a><a name="dmp_edition"></a>对 Windows 10 版本升级策略的改进

在此版本中，已对此策略进行了以下改进：

* 现在，除了已向 Microsoft Intune 注册的 Windows 10 电脑之外，还可以对运行 Configuration Manager 客户端的 Windows 10 电脑使用版本升级策略。
* 可以从 Windows 10 专业版升级到与你的硬件兼容的向导中的任何平台。

[阅读有关 Windows 10 版本升级策略的详细信息](../../compliance/deploy-use/upgrade-windows-version.md)

### <a name="try-it-out"></a>试试看！

1. 使用[现有版本升级策略主题](../../compliance/deploy-use/upgrade-windows-version.md)中的信息创建版本升级策略。
2. 将此策略部署到运行 Configuration Manager 客户端的 Windows 10 电脑。
一旦该策略应用到目标 Windows 电脑，该电脑将在两小时内重启以应用该升级。 当前无法取消此重启。 确保通知所有要向其部署策略，或计划在其业余时间运行该策略的用户。

### <a name="known-issue-with-this-release"></a>此版本的已知问题
在 Configuration Manager 客户端设置中，可能会看到**版本升级**的设置。 在此版本中，这些设置不起作用。 使用上面给出的说明将 Windows 10 升级到较新版本。

## <a name="customizable-branding-for-software-center-dialogs"></a>软件中心可自定义的品牌的对话框

Configuration Manager 版本 1602 中引入了软件中心的自定义品牌。 在 Technical Preview 版本 1607 中，现已将该品牌功能扩展到所有关联的对话框和任务栏通知，以便为软件中心用户提供更一致的体验。

### <a name="try-it-out"></a>试试看！

根据以下规则应用软件中心的自定义品牌：

1. 如果未安装应用程序目录网站点站点服务器角色，则软件中心将显示“计算机代理”  客户端设置“软件中心中显示的组织名称”  中指定的组织名称。 有关说明，请参阅[如何配置客户端设置](../../core/clients/deploy/configure-client-settings.md)。

2. 如果已安装应用程序目录网站点站点服务器角色，则软件中心将显示在应用程序目录网站点站点服务器角色属性中指定的组织名称和颜色。 有关详细信息，请参阅[应用程序目录网站点的配置选项](../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md#BKMK_ApplicationCatalog_Website)。

3. 如果已配置 Microsoft Intune 订阅并将其连接到 Configuration Manager 环境，则软件中心将显示 Intune 订阅属性中指定的组织名称、颜色和公司徽标。

## <a name="use-the-same-network-adapter-for-multiple-pxe-initiated-deployments"></a>对多个 PXE 启动的部署使用相同的网络适配器
在 Technical Preview 版本 1607 中，当使用以太网适配器映射多个设备（如在多个设备上使用的 USB 以太网适配器）时，可以启用允许输入以太网适配器的硬件标识符的新设置。 在执行 PXE 安装和客户端注册时，Configuration Manager 忽略列表中的硬件标识符。

有关此问题的详细信息，请参阅 [Configuration Manager OSD Support Team Blog](https://blogs.technet.microsoft.com/system_center_configuration_manager_operating_system_deployment_support_blog/2015/08/27/reusing-the-same-nic-for-multiple-pxe-initiated-deployments-in-system-center-configuration-manger-osd/)（Configuration Manager OSD 支持团队博客）。  

### <a name="enable-the-feature-to-manage-duplicate-hardware-identifiers"></a>启用该功能可管理重复硬件标识符  
1. 在 Configuration Manager 控制台中，转到“管理”   > “概述”   > “云服务”   > “更新与维护服务”   > “功能”  。
2. 在显示窗格中，选择“管理重复硬件标识符”  。
3. 在“主页”  选项卡上的“功能”  组中，单击“打开”  。

### <a name="add-hardware-identifiers-for-configuration-manager-to-ignore"></a>添加 Configuration Manager 可忽略的硬件标识符  
1. 在 Configuration Manager 控制台中，转到“管理”   > “概述”   > “站点配置”   > “站点”  。
2. 在“主页”  选项卡上的“站点”  组中，单击“层次结构设置”  。
3. 转到“客户端批准和冲突的记录”  选项卡。
4. 单击“重复硬件标识符”  部分中的“添加”  ，以添加新的硬件标识符。
