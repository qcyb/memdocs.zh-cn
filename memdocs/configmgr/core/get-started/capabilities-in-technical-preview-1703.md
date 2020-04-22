---
title: Technical Preview 1703 中的功能
titleSuffix: Configuration Manager
description: 了解 Configuration Manager Technical Preview（版本 1703）中的可用功能。
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e801f8c-d331-41ee-8f27-908448fc0951
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: cbdcc7a4774c9b57ab4a836719ebfc408a2d771d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705275"
---
# <a name="capabilities-in-technical-preview-1703-for-configuration-manager"></a>Configuration Manager Technical Preview 1703 中的功能

适用范围：*Configuration Manager（技术预览版分支）*

本文介绍 Configuration Manager Technical Preview 1703 中提供的功能。 你可以安装此版本，以更新 Technical Preview 站点的功能并向其添加新功能。 在安装此版本的技术预览版前，请查看介绍性主题 [Configuration Manager 的 Technical Preview](../../core/get-started/technical-preview.md)，以熟悉使用技术预览版的常规要求和限制、如何在版本之间进行更新，以及如何提供关于技术预览版中的功能的反馈。    


**以下是此版本可以试用的新功能。**  

## <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>将批量采购的 iOS 应用部署到设备集合

现在可以将已授权的应用程序部署到设备以及用户。 根据应用对设备授权的支持能力，合适的许可证将在部署时按以下方式声明：

|||||
|-|-|-|-|
|Configuration Manager 版本|应用是否支持设备授权？|部署集合类型|已声明的许可证|
|早于 1702|是|用户|用户许可证|
|早于 1702|否|用户|用户许可证|
|早于 1702|是|设备|用户许可证|
|早于 1702|否|设备|用户许可证|
|1702 及更高版本|是|用户|用户许可证|
|1702 及更高版本|否|用户|用户许可证|
|1702 及更高版本|是|设备|设备许可证|
|1702 及更高版本|否|设备|用户许可证|


## <a name="direct-links-to-applications-in-software-center"></a>指向软件中心中应用程序的直接链接

现在可向最终用户提供指向软件中心中应用程序的直接链接。 这意味着最终用户不必打开软件中心搜索应用程序就可安装应用程序。 这仅适用于 Configuration Manager 应用程序，包和程序或任务序列不适用。

### <a name="try-it-out"></a>试试看                 

使用以下 URL 格式在特定应用程序中打开软件中心：

Softwarecenter:SoftwareId= 应用程序标识符  

### <a name="how-to-get-the-application-identifier-of-an-application"></a>如何获取应用程序的应用程序标识符。

1. 在 Configuration Manager 控制台中，单击“软件库”  。
2. 在“软件库”工作区中，展开“应用程序管理”  ，然后单击“应用程序”  。
3. 在“应用程序”  视图中，右键单击其中一个列标题，然后在列表中选择“CI 唯一 ID”  。 此时列表中将显示每个应用程序的唯一 ID。
4. 请注意要提供链接的应用程序的“CI 唯一 ID”，例如  ：**ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f/2**
5. 然后，删除应用程序 GUID 后的所有文本，在本例中为 **/2**。 剩下的即为应用程序标识符。
6. 最后，若要完成构造链接，请在标识符前附加 **Softwarecenter:SoftwareID=** 。 使用上面的示例，最终链接将显示为：**Softwarecenter:SoftwareId= ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f**。

通过使用此链接，最终用户可直接在指定的应用程序中打开软件中心。


## <a name="pfx-certificates-for-configuration-manager-windows-client-computers"></a>Configuration Manager Windows 客户端计算机的 PFX 证书

现在可将导入的 PFX 证书配置文件部署到运行 Windows 10 的 Configuration Manager 客户端计算机。

### <a name="try-it-out"></a>试试看

按照[如何创建 PFX 证书配置文件](../../mdm/deploy-use/create-pfx-certificate-profiles.md)中的说明来导入 PFX 配置文件、部署配置文件，然后检查是否已为目标用户安装该证书。



## <a name="configure-azure-services-wizard"></a>配置 Azure 服务 向导
Technical preview 1703 引入了**配置 Azure 服务**向导。 此向导提供了一种可替换单个工作流的常见配置体验，可供设置用于 Configuration Manager 的云服务。 可通过使用 **Azure Web 应用**提供订阅和配置详情来完成此操作，否则需要在每次使用 Azure 设置新 Configuration Manager 组件或服务时输入这些详细信息。

在 Technical Preview 1703 中，使用此向导仅可配置适用于企业的 Windows 应用商店 (WSfB)。  通过使用其单独的工作流配置其他云服务。

- 使用本预览主题中的信息替换 Current Branch 主题[使用 Configuration Manager 管理来自适用于企业的 Microsoft Store 的应用](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)的[设置适用于企业的 Microsoft Store 同步](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#bkmk_setup)部分中的配置步骤。

- 有关 Web 应用的详细信息，请参阅 [Azure 应用服务中的身份验证和授权](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview)和 [Web 应用概述](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)。

### <a name="prerequisites-and-planning"></a>先决条件和规划
在 Configuration Manager和适用于企业的 Windows 应用商店之间设置连接时，必须提供保存从应用商店同步的应用内容的文件夹。 若要确保此文件夹是安全的且可将其内容部署到设备，请确保以下权限就位：
- 安装服务连接点站点系统角色（层次结构中的顶级站点）的计算机必须具有使用 **Computer$** 帐户时指定的文件夹的读取和写入权限。  

- 应用作者必须具有所指定文件夹的读取权限。  

- 托管 SMS 提供程序实例的每台计算机的 **Computer$** 帐户必须能够使用所指定的文件夹。

在 Azure Active Directory 中，将 Configuration Manager 注册为 Web 应用程序或 Web API 管理工具。 这会创建以后将需要的客户端 ID。

### <a name="use-the-wizard-to-configure-the-wsfb-cloud-service"></a>使用向导配置 WSfB 云服务

1. 在控制台中，转到“管理”   > “概述”   > “云服务管理”   > “Azure”   > “Azure 服务”  ，然后选择“配置 Azure 服务”  以启动“Azure 服务向导”  。

2. 在“Azure 服务”  页上，选择要配置的服务，然后单击“下一步”  。 此预览版仅可配置 WSfB。

3. 在“常规”  页上，提供“Azure 服务名称”  的友好名称和可选说明，然后单击“下一步”  。

4. 在“应用”  页上，指定 Azure 环境，然后单击“浏览”  打开“服务器应用”窗口。

5. 在“服务器应用”  窗口中，选择要使用的服务器应用，然后单击“确定”  。
   服务器应用是包含 Azure 帐户配置的 Azure Web 应用，包括客户端的租户 ID、客户端 ID 和密钥。 如果没有可用的服务器应用，请使用以下操作之一：
   - **创建**：若要创建新的服务器应用，请单击“创建”  。 为应用和租户提供友好名称。 然后，登录 Azure 后，Configuration Manager 将在 Azure 中为用户创建 Web 应用，包括用于 Web 应用的客户端 ID 和密钥。 之后，可在 Azure 门户中查看这些内容。
   - **导入**：若要使用 Azure 订阅中已存在的 Web 应用，请单击“导入”  。 为应用和租户提供友好名称，然后为 Configuration Manager 要使用的 Azure Web 应用指定租户 ID、客户端 ID 和密钥。 “验证”  信息后，单击“确定”  以继续。  </br></br>

6. 查看“信息”  页，并根据指示完成所有额外步骤和配置。 这些配置是通过 Configuration Manager 使用服务所必需的。
   例如，若要配置 WSfB：

   1. 在 Azure 中，必须将 Configuration Manager 注册为 Web 应用程序或 Web API 并记录客户端 ID。 还可以指定用于管理工具 (Configuration Manager) 的客户端密钥。

   2.    在 WSfB 控制台中，必须将 Configuration Manager 配置为存储管理工具并启用对脱机许可应用的支持，然后购买至少一个应用。   </br>

   准备好继续后，单击“下一步”  。

7. 在“应用配置”  页上，完成此服务的应用目录和语言配置，然后单击“下一步”  。
8. 完成向导后，Configuration Manager 控制台将显示已将“适用于企业的 Windows 应用商店”  配置为“云服务类型”  。

现可利用 [Current Branch 内容](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md)的其余部分从 WSfB 管理应用，以同步、创建、部署和管理适用于企业的 Windows 应用商店应用。

### <a name="modify-a-cloud-service-configuration"></a>修改云服务配置
可以查看和编辑云服务属性以修改配置。

在控制台中，转到“管理”   > “概述”   > “云服务管理”   > “Azure”   > “Azure 服务”  ，然后选择“配置 Azure 服务”  ，选择一个“云服务”，然后选择“属性”  。

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>在就地升级过程中从 BIOS 转换为 UEFI
Windows 10 创意者更新引入了一个简单的转换工具，可自动执行对用于启用 UEFI 的硬件的硬盘重新分区的过程，并将该转换工具集成到 Windows 7 到 Windows 10 的就地升级过程中。 将此工具与你的操作系统升级任务序列和将固件从 BIOS 转换到 UEFI 的 OCM 工具组合使用时，可以在 Windows 10 创意者更新的就地升级过程中将你的计算机从 BIOS 转换到 UEFI。 有关详细信息，请参阅[管理 BIOS 转换为 UEFI 所采用的任务序列步骤](../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#convert-from-bios-to-uefi-during-an-in-place-upgrade)。

## <a name="collapsible-task-sequence-groups"></a>可折叠的任务序列组
此版本引入了扩展和折叠任务序列组的功能。 可以展开或折叠单个组，也可一次展开或折叠所有组。


## <a name="client-settings-to-configure-windows-analytics-for-upgrade-readiness"></a>用于配置 Windows Analytics for Upgrade Readiness 的客户端设置
自此版本起，将 Windows Analytics 解决方案（例如升级就绪情况）用于Configuration Manager 时，可以使用设备客户端设置来简化必要的 Windows 诊断数据的配置。 Configuration Manager 可以从 Windows Analytics 中检索数据，从而能够根据客户端计算机报告的 Windows 诊断数据获取有关环境当前状态的有价值见解。 Windows 诊断数据由客户端计算机报告给 Windows 诊断服务，随后相关数据被传输到在组织的 OMS 工作区之一中托管的 Windows Analytics 解决方案。 Upgrade Readiness 是一种 Windows Analytics 解决方案，可以帮助你优先做出有关受管理设备的 Windows 升级的决策。

### <a name="prerequisites"></a>必备条件
- 必须已将站点配置为使用 Upgrade Readiness 云服务。

### <a name="configure-windows-analytics-client-settings"></a>配置 Windows Analytics 客户端设置
若要配置 Windows Analytics，请在 Configuration Manager 控制台中依次转到“管理”   > “客户端设置”  ，双击“创建自定义设备客户端设置”  ，然后选中“Windows Analytics”  。  

然后，转到“Windows Analytics”  设置选项卡，配置进行以下设置：
- **商用 ID**  
商用 ID 键可用于将你管理的设备中的信息映射到托管你组织的 Windows Analytics 数据的 OMS 工作区。 如果已配置用于 Upgrade Readiness 的商用 ID 键，请使用此 ID。 如果还没有商业 ID 键，请生成商业 ID 键。

- 为 Windows 10 设备  设置诊断数据级别

- 选择“选择加入 Windows 7、8 和 8.1 设备上的商业数据收集”    

- **配置 Internet Explorer 数据收集**：在运行 Windows 8.1 或更低版本的设备上，启用 Internet Explorer 数据收集后，Upgrade Readiness 可以检测可能会阻止顺利升级到 Windows 10 的 Web 应用程序不兼容问题。 可以每 Internet 区域启用一次 Internet Explorer 数据收集。
