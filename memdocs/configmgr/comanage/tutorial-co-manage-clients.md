---
title: 教程：为现有客户端启用共同管理
titleSuffix: Configuration Manager
description: 在已使用 Configuration Manager 管理 Windows 10 设备时，在 Microsoft Intune 中配置共同管理。
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cc05ae5a9be6c437fab60f8c4c5a45d61e8c3e65
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694876"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>教程：为现有 Configuration Manager 客户端启用共同管理

通过共同管理，可以保持完善的流程，以便使用 Configuration Manager 管理组织中的电脑。 同时，通过使用 Intune 在云上投入，实现安全性和新式预配。  

在本教程中，你对已在 Configuration Manager 中注册的 Windows 10 设备设置共同管理。 开始学习此教程的前提是，你已使用 Configuration Manager 来管理 Windows 10 设备。

若要使用本教程，需要具备以下条件：  

- 具有可以连接到混合 Azure AD 配置中的 Azure Active Directory (Azure AD) 的本地 Active Directory。

  如果无法部署联接本地 AD 与 Azure AD 联接的混合 Azure Active Directory (AD)，建议学习我们的配套教程：[为基于 Internet 的新 Windows 10 设备启用共同管理](tutorial-co-manage-new-devices.md)。
- 具有想要进行云附加的 Configuration Manager 客户端。

**在本教程中，你将：**  
> [!div class="checklist"]
> * 检查 Azure 和本地环境的先决条件
> * 设置混合 Azure AD  
> * 配置 Configuration Manager 客户端代理以注册 Azure AD  
> * 将 Intune 配置为自动注册设备  
> * 在 Configuration Manager 中启用共同管理  

## <a name="prerequisites"></a>必备条件  

### <a name="azure-services-and-environment"></a>Azure 服务和环境

- Azure 订阅（[免费试用版](https://azure.microsoft.com/free)）
- Azure Active Directory Premium
- Microsoft Intune 订阅
  > [!TIP]  
  > 企业移动性 + 安全性 (EMS) 订阅包括 Azure Active Directory Premium 和 Microsoft Intune。 EMS 订阅（[免费试用版](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)）。  

如果环境中尚不存在，在学习本教程期间，你将：

- 在本地 Active Directory 和 Azure Active Directory (AD) 租户之间配置 [Azure AD Connect](/azure/active-directory/hybrid/how-to-connect-install-select-installation)。

> [!TIP]
> 不再需要向用户购买和分配单独的 Intune 或 EMS 许可证。 有关详细信息，请参阅[产品和许可常见问题解答](../core/understand/product-and-licensing-faq.md#bkmk_mem)。

### <a name="on-premises-infrastructure"></a>本地基础结构

- [受支持的](../core/servers/manage/updates.md#supported-versions) Configuration Manager Current Branch 版本
- 必须将移动设备管理 (MDM) 机构设置为 Intune。  

### <a name="permissions"></a>权限

在本教程中，请使用以下权限来完成各项任务：

- 本地基础结构上的域管理员帐户  
- Configuration Manager 中所有范围的完全权限管理员帐户 
- 作为 Azure Active Directory (Azure AD) 中的全局管理员的帐户
   - 请确保你已将 Intune 许可证分配到自己用来登录租户的帐户。 否则，登录将失败，并显示错误消息“无法识别用户”。 <!--mem issue 169-->

## <a name="set-up-hybrid-azure-ad"></a>设置混合 Azure AD

设置混合 Azure AD 时，实际上是使用 Azure AD Connect 和 Active Directory 联合身份验证服务 (ADFS) 来设置本地 AD 与 Azure AD 的集成。 成功配置后，工作人员可以使用其本地 AD 凭据无缝登录到外部系统。

> [!IMPORTANT]  
> 本教程详细介绍了为托管域设置混合 Azure AD 的基本过程。 建议你熟悉此过程，而不依赖于本教程引导你了解和部署混合 Azure AD。
>
> 有关混合 Azure AD 的详细信息，请先参阅 Azure Active Directory 文档中的以下文章：
>
> - [规划 Azure AD 联接实现](/azure/active-directory/devices/azureadjoin-plan)
> - [规划混合 Azure AD 联接实现](/azure/active-directory/devices/hybrid-azuread-join-plan)
> - [控制设备的混合 Azure AD 联接](/azure/active-directory/devices/hybrid-azuread-join-control)
> - [为联盟域配置混合 Azure AD 联接](/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  

### <a name="set-up-azure-ad-connect"></a>设置 Azure AD Connect

混合 Azure AD 需要配置 Azure AD Connect，以使本地 Active Directory (AD) 中的计算机帐户和 Azure AD 中的设备对象保持同步。

从版本 1.1.819.0 开始，Azure AD Connect 提供了配置混合 Azure AD 联接的向导。 使用该向导可简化配置过程。  

若要配置 Azure AD Connect，需要 Azure AD 的全局管理员凭据。  

> [!TIP]  
> 以下过程不应被视为是设置 Azure AD Connect 的权威方法，但在这里提供此方法旨在帮助简化在 Intune 和 Configuration Manager 之间配置共同管理的过程。 有关此过程的权威内容和与设置 Azure AD 相关的过程，请参阅 Azure AD 文档中的[为托管域配置混合 Azure AD 联接](/azure/active-directory/devices/hybrid-azuread-join-managed-domains)。  

#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>使用 Azure AD Connect 配置混合 Azure AD 联接

1. 获取和安装[最新版本的 Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594)（1.1.819.0 或更高版本）。  
2. 启动 Azure AD Connect，然后选择“配置”。
3. 在“其他任务”页上，选择“配置设备选项”，然后选择“下一步”。
4. 在“概述”页上，选择“下一步”。
5. 在“连接到 Azure AD”页上，输入 Azure AD 的全局管理员凭据。
6. 在“设备选项”页上，选择“配置混合 Azure AD 联接”，然后选择“下一步”。
7. 在“设备操作系统”页上，选择 Active Directory 环境中的设备所使用的操作系统，然后选择“下一步”。  

   可以选择支持 Windows 下层加入域的设备的选项，但请记住，仅 Windows 10 支持设备的共同管理。
8. 在“SCP’页上，对于想要 Azure AD Connect 配置服务连接点 (SCP) 的每个本地林，执行以下步骤，然后选择“下一步”：  
   1. 选择林。  
   2. 选择身份验证服务。  如果具有联盟域，选择 AD FS 服务器，除非贵组织具有专门的 Windows 10 客户端且已配置计算机/设备同步或组织正在使用 [SeamlessSSO](/azure/active-directory/hybrid/how-to-connect-sso)。  
   3. 单击“添加”以输入企业管理员凭据。  
9. 如果有托管域，则跳过此步骤。  

   在“联合身份验证配置”页上，输入 AD FS 管理员的凭据，然后选择“下一步”。
10. 在“已准备好进行配置”页上，选择“配置”。
11. 在“配置完成”页上，选择“退出”。

如果在完成已加入域的 Windows 设备的混合 Azure AD 联接时遇到问题，请参阅[针对 Windows 当前设备混合 Azure AD 联接的故障排除](/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current)。

## <a name="configure-client-settings-to-direct-clients-to-register-with-azure-ad"></a>配置客户端设置，以引导客户端注册 Azure AD

使用客户端设置将 Configuration Manager 客户端配置自动注册 Azure AD。  

1. 打开“Configuration Manager 控制台” > “管理” > “概述” > “客户端设置”，然后编辑“默认客户端设置”。  

2. 选择“云服务”。  

3. 在“默认设置”页上，将“在 Azure Active Directory 中自动注册已加入域的新 Windows 10 设备”设置为 =“是”。  

4. 选择“确定”以保存此配置。  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>配置设备自动注册到 Intune

接下来，我们将在 Intune 中设置设备的自动注册。 借助自动注册，使用 Configuration Manager 管理的设备将在 Intune 中自动注册。

自动注册还允许用户将其 Windows 10 设备注册到 Intune。 在以下情况中注册设备：用户将其工作帐户添加到其个人拥有的设备，或将企业拥有的设备加入到 Azure Active Directory。  

1. 登录到 [Azure 门户](https://portal.azure.com/)，然后选择“Azure Active Directory” > “移动性(MDM 和 MAM)” > “Microsoft Intune”。  

2. 配置“MDM 用户范围”。 指定以下任一设置以配置由 Microsoft Intune 管理的用户设备并接受 URL 值的默认值。  

   - **部分**：选择可自动注册其 Windows 10 设备的“组”  

   - **全部**：所有用户都可以自动注册其 Windows 10 设备

   - **无**：禁用 MDM 自动注册

   > [!IMPORTANT]  
   > 如果为某个组同时启用了“MAM 用户范围”和自动 MDM 注册（MDM 用户范围），则仅启用 MAM。 当该组中用户的工作区加入个人设备时，仅为这些用户添加移动应用程序管理 (MAM)。 设备不会自动注册 MDM。  

3. 选择“保存”以完成自动注册的配置。  

4. 返回到“移动性(MDM 和 MAM)”，然选择“Microsoft Intune 注册”。  

    > [!NOTE]
    > 部分租户无需配置这些选项。<!-- SCCMDocs#1230 -->
    >
    > “Microsoft Intune”是为 Azure AD 配置 MDM 应用的方式。 “Microsoft Intune 注册”是在应用适用于 iOS 和 Android 注册的多重身份验证策略时创建的特定 Azure AD 应用。 有关详细信息，请参阅[对 Intune 设备注册要求多重身份验证](/intune/enrollment/multi-factor-authentication)。

5. 对于 MDM 用户范围，选择“全部”，然后选择“保存”。  

## <a name="enable-co-management-in-configuration-manager"></a>在 Configuration Manager 中启用共同管理

完成 Azure AD 设置和 Configuration Manager 客户端配置后，即可切换开关并启用 Windows 10 设备的共同管理。  

> [!TIP]
> - 启用共同管理后，会分配集合作为试点组。 此组包含少量客户端，用于测试共同管理配置。 建议在开始此过程前先创建合适的集合。 然后，可以选择此集合，而无需退出该过程来执行此操作。
> - 从 Configuration Manager 版本 1906 开始，可能需要多个集合，因为可以为每个工作负载分配不同的试点组。

### <a name="enable-co-management-starting-in-version-1906"></a>从版本 1906 开始启用共同管理

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>在版本 1902 及更早版本中启用共同管理

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="next-steps"></a>后续步骤

- 使用[共同管理仪表板](how-to-monitor.md)查看共同管理的设备的状态
- 开始从共同管理中获取[即时值](quickstarts.md#immediate-value)
- 使用[条件访问](quickstart-conditional-access.md)和 Intune 符合性规则来管理用户对企业资源的访问权限