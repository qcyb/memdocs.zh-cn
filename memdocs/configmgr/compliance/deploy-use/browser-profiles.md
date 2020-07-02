---
title: 配置 Microsoft Edge 设置
titleSuffix: Configuration Manager
description: 在 Windows 10 客户端上配置 Microsoft Edge 旧版 Web 浏览器设置
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/02/2020
ms.topic: how-to
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 898d5240046655ca3d13037f74c92e730ab1993e
ms.sourcegitcommit: 7f542c97ac55bbd329f5befda97d671213c24e9a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84506128"
---
# <a name="configure-microsoft-edge-legacy-settings-in-configuration-manager"></a>在 Configuration Manager 中配置 Microsoft Edge 旧版设置

> [!IMPORTANT]
> 如果你使用的是 Microsoft Edge 版本 77 或更高版本，并尝试打开“设置”窗格，请在浏览器地址栏而不是搜索中输入 `edge://settings/profiles`。 有关详细信息，请参阅[了解 Microsoft Edge](https://support.microsoft.com/help/17171/microsoft-edge-get-to-know)。
>
> 本文面向通过 Microsoft Endpoint Configuration Manager 来管理 Microsoft Edge 旧版设置的 IT 专业人员。

适用范围：Configuration Manager (Current Branch)

<!-- 1357310 -->
对于在 Windows 10 客户端上使用 [Microsoft Edge 旧版](https://docs.microsoft.com/microsoft-edge/deploy/) Web 浏览器的客户，请创建 Configuration Manager 合规性策略，以配置浏览器设置。

此策略仅适用于 Windows 10 版本 1703 或更高版本以及 Microsoft Edge 旧版 45 及更早版本中的客户端。 <!--511552-->

若要详细了解如何通过 Configuration Manager 管理 Microsoft Edge 版本 77 或更高版本，请参阅[部署 Microsoft Edge 版本 77 及更高版本](../../apps/deploy-use/deploy-edge.md)。 有关为 Microsoft Edge 版本 77 或更高版本配置策略的详细信息，请参阅 [Microsoft Edge - 策略](https://docs.microsoft.com/DeployEdge/microsoft-edge-policies)。

## <a name="policy-settings"></a>策略设置

此策略当前包括以下设置：

- 将 Microsoft Edge 浏览器设置为默认浏览器：将 Web 浏览器的 Windows 10 默认应用设置配置为 Microsoft Edge

- **允许使用地址栏下拉列表**：需要 Windows 10 版本 1703 或更高版本。 有关详细信息，请参阅 [AllowAddressBarDropdown 浏览器策略](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown)。

- **允许在 Microsoft 浏览器之间同步收藏夹**：需要 Windows 10 版本 1703 或更高版本。 有关详细信息，请参阅 [SyncFavoritesBetweenIEAndMicrosoftEdge 浏览器策略](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge)。

- **允许在退出时清除浏览数据**：需要 Windows 10 版本 1703 或更高版本。 有关详细信息，请参阅 [ClearBrowsingDataOnExit 浏览器策略](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit)。

- **允许使用 Do Not Track 标头**：有关详细信息，请参阅 [AllowDoNotTrack 浏览器策略](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack)。

- **允许自动填充**：有关详细信息，请参阅 [AllowAutofill 浏览器策略](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowautofill)。

- **允许使用 Cookie**：有关详细信息，请参阅 [AllowCookies 浏览器策略](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowcookies)。

- **允许使用弹出窗口阻止程序**：有关详细信息，请参阅 [AllowPopups 浏览器策略](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpopups)。

- **允许在地址栏中显示搜索建议**：有关详细信息，请参阅 [AllowSearchSuggestionsinAddressBar 浏览器策略](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar)。

- **允许将 Intranet 流量发送到 Internet Explorer**：有关详细信息，请参阅 [SendIntranetTraffictoInternetExplorer 浏览器策略](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer)。

- **允许使用密码管理器**：有关详细信息，请参阅 [AllowPasswordManager 浏览器策略](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)。

- **允许使用开发人员工具**：有关详细信息，请参阅 [AllowDeveloperTools 浏览器策略](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools)。

- **允许使用扩展**：有关详细信息，请参阅 [AllowExtensions 浏览器策略](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowextensions)。

> [!TIP]
> 有关使用组策略配置这些设置和其他设置的详细信息，请参阅 [Microsoft Edge 旧版组策略](https://docs.microsoft.com/microsoft-edge/deploy/group-policies/)。

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge-legacy"></a>为 Microsoft Edge 旧版配置 Windows Defender SmartScreen 设置
<!--1353701-->
此策略为 [Windows Defender SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) 添加了 3 个设置。 该策略现在包含“SmartScreen 设置”页上的以下附加设置：

- **允许 SmartScreen**：指定是否允许 Windows Defender SmartScreen。 有关详细信息，请参阅 [AllowSmartScreen 浏览器策略](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)。

- **用户可以替代站点的 SmartScreen 提示**：指定用户是否可替代有关潜在恶意网站的 Windows Defender SmartScreen 筛选器警告。 有关详细信息，请参阅 [PreventSmartScreenPromptOverride 浏览器策略](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)。

- **用户可以替代文件的 SmartScreen 提示**：指定用户是否可替代有关下载未经认证文件的 Windows Defender SmartScreen 筛选器警告。 有关详细信息，请参阅[PreventSmartScreenPromptOverrideForFiles 浏览器策略](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)。

## <a name="create-the-browser-profile"></a>创建浏览器配置文件

1. 在 Configuration Manager 控制台中，转到“资产和符合性”工作区。 展开“符合性设置”，然后选择“Microsoft Edge 浏览器配置文件”节点 。 在功能区中，选择“创建 Microsoft Edge 配置文件”。

2. 指定策略“名称”，根据需要输入“说明”，然后选择“下一步”。

3. 在“常规设置”页上，将值更改为“已配置”，使设置包含在此策略中。 要继续该向导，务必要配置“将 Edge 浏览器设为默认”设置。

4. 在“SmartScreen 设置”页上配置设置。

5. 在“支持的平台”页上，选择此策略要应用到的 OS 版本和体系结构。

6. 完成向导。

## <a name="deploy-the-policy"></a>部署策略

1. 选择策略，并在功能区中选择“部署”。

2. 单击“浏览”以选择要在其中部署策略的用户或设备集合。

3. 根据需要选择其他选项：

    1. 当策略不合规时生成警报。

    2. 设置客户端评估设备与此策略符合性所依据的计划。

4. 选择“确定”创建部署。

## <a name="next-steps"></a>后续步骤

就像任何符合性设置策略，客户端会修正指定计划的设置。 在 Configuration Manager 控制台中[监视和报告设备合规性](monitor-compliance-settings.md)。
