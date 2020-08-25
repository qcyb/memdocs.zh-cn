---
title: 管理应用程序防护策略
titleSuffix: Configuration Manager
description: 了解如何创建和部署 Microsoft Defender 应用程序防护策略
ms.date: 06/05/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3fb7559f624afdb16ef228c61331387c163fbd54
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697103"
---
# <a name="create-and-deploy-microsoft-defender-application-guard-policy"></a>创建和部署 Microsoft Defender 应用程序防护策略

适用范围：Configuration Manager (Current Branch)
<!-- 1351960 -->  
可以使用 Configuration Manager Endpoint Potection 创建和部署 [Microsoft Defender 应用程序防护（应用程序防护）](/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview)策略。 这些策略通过在操作系统的其他部分无法访问的安全隔离容器中打开不受信任的网站来帮助保护用户安全。

## <a name="prerequisites"></a>必备条件

若要创建和部署 Microsoft Defender 应用程序防护策略，必须使用 Windows 10 Fall Creator Update (1709)。 必须使用[网络隔离策略](/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard#network-isolation-settings)配置要部署此策略的 Windows 10 设备。 有关详细信息，请参阅 [Microsoft Defender 应用程序防护概述](/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview)。

## <a name="create-a-policy-and-to-browse-the-available-settings"></a>若要创建策略，并浏览可用设置，请执行以下操作：

1. 在 Configuration Manager 控制台中，选择“资产和符合性”。
2. 在“资产和符合性”工作区中，选择“概述” > “终结点保护” > “Windows Defender 应用程序防护”。
3. 在“主页”选项卡的“创建”组中，单击“创建 Windows Defender 应用程序防护策略”。
4. 将此[文章](/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard)用作参考，浏览和配置可用的设置。 使用 Configuration Manager，可以设置某些策略设置：
   - [主机交互设置](#bkmk_HIS)
   - [应用程序行为](#bkmk_ABS)
   - [文件管理](#bkmk_FM)
5. 在“网络定义”页上，可指定公司标识并定义企业网络边界。

    > [!NOTE]
    > Windows 10 电脑仅在客户端上存储一个网络隔离列表。 可以创建两种不同的网络隔离列表，并将它们部署到客户端：
    >
    >  - 一个来自 Windows 信息保护
    >  - 一个来自 Microsoft Defender 应用程序防护
    >
    > 如果部署两个策略，两个网络隔离列表必须匹配。 如果部署的列表与同一个客户端不匹配，则部署失败。 有关详细信息，请参阅 [Windows 信息保护文档](/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)。

6. 结束后，完成向导操作，并将策略部署到一个或多个 Windows 10 1709 设备。

### <a name="host-interaction-settings"></a><a name="bkmk_HIS"></a> 主机交互设置

配置主机设备和应用程序防护容器之间的交互。 在 Configuration Manager 1802 之前的版本中，应用程序行为和主机交互都位于“设置”选项卡下。

- **剪贴板** - 在 Configuration Manager 1802 之前的版本中，位于“设置”下
  - 允许的内容类型
    - 文本
    - 图像
- **打印：**
  - 启用打印为 XPS
  - 启用打印为 PDF
  - 启用打印到本地打印机
  - 启用打印到网络打印机
- **图形：** （从 Configuration Manager 1802 版开始）
  - 虚拟图形处理器访问
- **文件：** （从 Configuration Manager 1802 版开始）
  - 将下载的文件保存到主机

### <a name="application-behavior-settings"></a><a name="bkmk_ABS"></a> 应用程序行为设置

在应用程序防护会话内配置应用程序行为。 在 Configuration Manager 1802 之前的版本中，应用程序行为和主机交互都位于“设置”选项卡下。

- **内容：**
  - 企业网站可以加载非企业内容，如第三方插件。
- **其他：**
  - 保留用户生成的浏览器数据
  - 在独立的应用程序防护会话中审核安全性事件

### <a name="file-management"></a><a name="bkmk_FM"></a> 文件管理
<!--3555858-->
自 Configuration Manager 版本 1906 起，推出了一项策略设置，允许用户信任通常在应用程序防护中打开的文件。 成功完成后，文件将在主机设备上打开，而不是在应用程序防护中打开。 有关应用程序防护策略的详细信息，请参阅[配置 Microsoft Defender 应用程序防护策略设置](/windows/security/threat-protection/microsoft-defender-application-guard/configure-md-app-guard)。

- 允许用户信任在 Windows Defender 应用程序防护中打开的文件 - 可便于用户将文件标记为“受信任”。 受信任的文件在主机（而不是应用程序防护）中打开。 适用于 Windows 10 版本 1809 或更高版本的客户端。
  - **禁止：** 不允许用户将文件标记为可信（默认）。
  - **由防病毒软件检查的文件：** 允许用户在进行防病毒检查后将文件标记为可信。
  - **所有文件：** 允许用户将任何文件标记为可信。

启用文件管理后，可能会在客户端的 DCMReporting.log 中看到记录的错误。 以下错误通常不会影响功能： <!--4619457-->

- 在兼容的设备上：
  - 找不到 FileTrustCriteria_condition
- 在不兼容的设备上：
  - 找不到 FileTrustCriteria_condition
  - FileTrustCriteria_condition 不能位于映射中
  - 在摘要中找不到 FileTrustCriteria_condition

若要编辑应用程序防护设置，请展开“资产和符合性”工作区中的“Endpoint Protection”，然后单击“Windows Defender 应用程序防护”节点。 右键单击要编辑的策略，然后选择“属性”。

## <a name="known-issues"></a>已知问题

运行 Windows 10 版本 2004 的设备将在 Microsoft Defender 应用程序防护文件信任条件的符合性报告中显示失败。 之所以出现此问题，是因为从 Windows 10 版本 2004 中的 WMI 类 `MDM_WindowsDefenderApplicationGuard_Settings01` 删除了某些子类。 所有其他 Microsoft Defender 应用程序防护设置仍适用，仅文件信任条件会失败。 当前没有可以绕过该错误的解决方法。 <!--7099444,5946790-->

## <a name="next-steps"></a>后续步骤

有关 Microsoft Defender 应用程序防护的详细信息，请参阅
 - [Microsoft Defender 应用程序防护概述](/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview)。
- [Microsoft Defender 应用程序防护常见问题解答](/windows/security/threat-protection/microsoft-defender-application-guard/faq-md-app-guard)。