---
title: 创建配置基线
titleSuffix: Configuration Manager
description: 在 Configuration Manager 中创建可以部署到集合的配置基线。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1365aec90093ee24ad967e1d68e7c414b4efa254
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906667"
---
# <a name="create-configuration-baselines-in-configuration-manager"></a>创建 Configuration Manager 中的配置基线

适用范围：  Configuration Manager (Current Branch)


Configuration Manager 中的配置基线包含预定义的配置项目，还可包含其他配置基线。 在创建配置基线之后，可以将其部署到集合以便该集合中的设备下载配置基线并评估其符合性。  

> [!TIP]
> 无法指定 Configuration Manager 客户端评估基线中配置项目的顺序。 这是不确定的。<!-- MEMDocs#175 -->

## <a name="configuration-baselines"></a>配置基线

 Configuration Manager 中的配置基线可以包含配置项目的特定修订版本，或者配置为始终使用最新版的配置项目。 有关配置项目修订版本的详细信息，请参阅[针对配置数据的管理任务](../../compliance/deploy-use/management-tasks-for-configuration-data.md)。  

 可以使用两种方法来创建配置基线：  

- 从文件中导入配置数据。 要启动“导入配置数据向导”  ，请在“资产和符合性”  工作区中的“配置项目”  或“配置基线”  节点中，单击“导入配置数据”  。 有关详细信息，请参阅[导入配置数据](import-configuration-data.md)。

- 使用“创建配置基线”  对话框来创建一个新的配置基线。  

## <a name="create-a-configuration-baseline"></a>创建配置基线

若要通过“创建配置基线”对话框创建配置基线，请使用以下过程  ：  

1. 在 Configuration Manager 控制台中，单击“资产和符合性”   > “符合性设置”   > “配置基线”  。  

2. 在“主页”  选项卡上的“创建”  组中，单击“创建配置基线”  。  

3. 在“创建配置基线”  对话框中，输入配置基线的唯一名称和描述。 描述最多可使用 255 个字符，描述最多可使用 512 个字符。  

4. “配置数据”  列表将显示此配置基线中包含的所有配置项目或配置基线。 单击“添加”  可向列表中添加新配置项目或配置基线。 可以选择下列项目:  

   - <bpt id="p1">**</bpt>Configuration Items<ept id="p1">**</ept>  

   - **软件更新**  

   - <bpt id="p1">**</bpt>Configuration Baselines<ept id="p1">**</ept>  
     > [!IMPORTANT]
     > 必须将每个配置基线限制为不超过 1000 个软件更新。
5. 使用“更改目的”列表来指定在“配置数据”列表中已选择的配置项目的行为   。 可以选择下列项目：  

   -   **必需**：如果客户端设备上未检测到配置项目，则配置基线被评估为不符合要求。 如果检测到，则评估为符合要求  

   -   **可选**：只有在客户端计算机上找到它所引用的应用程序，才会评估配置项目的符合性。 如果找不到该应用程序，则不会将配置基线标记为不符合要求（仅适用于应用程序配置项目）。  

   -   **禁止**：如果客户端计算机上检测到配置项目（仅适用于应用程序配置项目），则将配置基线评估为不符合要求。  

   > [!NOTE]
   >  “更改目的”  列表只有在勾选“创建配置项目向导”  中“常规”  页面中的“此配置项目包含应用程序设置”  选项时才可用。  

6. 使用“更改修订版本”  列表可选择特定版本或最新版本的配置项目来评估客户端设备上的符合性，或选择“始终使用最新”  以始终使用最新版本。 有关配置项目修订版本的详细信息，请参阅[针对配置数据的管理任务](../../compliance/deploy-use/management-tasks-for-configuration-data.md)。  

7. 要从配置基线中删除配置项目，请选择配置项目，然后单击“删除”  。  

8. 自版本 1806 起，选择是否要“始终将此基线应用于共同管理的客户端”  。 选中时，此基线甚至将应用于由 Intune 管理的客户端。  此异常可用于配置组织所需但在 Intune 中尚不可用的设置。

9. （可选）单击“类别”，将类别分配到基线以进行搜索和筛选  。 

10. 单击“确定”  可关闭“创建配置基线”  对话框，并创建配置基线。  

>[!NOTE]
> 修改现有基线（如设置“始终将此基线应用于共同管理的客户端”）将使基线内容版本递增  。 客户端将需要评估新版本以更新基线报表。

## <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a><a name="bkmk_CAbaselines"></a> 将自定义配置基线包含在合规性策略评估中
<!--3608345-->
（从版本 1910 中引入） 

自版本 1910 开始，可以将自定义配置基线评估添加为合规性策略评估规则。 创建或编辑配置基线时，有一个选项“将此基线作为合规性策略的一部分进行评估”  。 添加或编辑合规性策略规则时，有一个名为“在合规性策略评估中包含配置的基线”的条件  。 对于共同管理的设备，当你配置 Intune 以将 Configuration Manager 合规性评估结果作为总体合规性状态的一部分时，此信息将发送到 Azure AD。 然后，你可以使用它对 Office 365 资源进行条件访问。 有关详细信息，请参阅[启用共同管理的条件访问](../../comanage/quickstart-conditional-access.md)。

若要将自定义配置基线包含在合规性策略评估中，请执行以下操作：

- 创建合规性策略并将其部署到用户集合，该集合包括[在合规性策略评估中包含配置的基线](#bkmk_CA)规则  。
- 在部署到设备集合的配置基线中，选择[将此基线作为合规性策略的一部分进行评估](#bkmk_eval-baseline)  。

> [!IMPORTANT]
> 目标为共同管理的设备时，请确保满足[共同管理先决条件](../../comanage/overview.md#prerequisites)。

### <a name="example-evaluation-scenario"></a>示例评估方案

当用户所属的集合是包含规则条件“在合规性策略评估中包含配置的基线”的合规性策略的适用对象时，将对部署到用户或用户设备的已选择“将此基线作为合规性策略的一部分进行评估”选项的所有基线进行合规性评估   。 例如：

- `User1` 属于 `User Collection 1`。
- `User1` 使用 `Device Collection 1` 和 `Device Collection 2` 中的 `Device1`。
- `Compliance Policy 1` 具有“在合规性策略评估中包含配置的基线”规则条件，并且已部署到 `User Collection 1` 。
- `Configuration Baseline 1` 已选择“将此基线作为合规性策略的一部分进行评估”，并且已部署到 `Device Collection 1` 。
- `Configuration Baseline 2` 已选择“将此基线作为合规性策略的一部分进行评估”，并且已部署到 `Device Collection 2` 。

在此方案中，当 `Compliance Policy 1` 使用 `Device1` 评估 `User1` 时，还会评估 `Configuration Baseline 1` 和 `Configuration Baseline 2`。

- `User1` 有时使用 `Device2`。
- `Device2` 是 `Device Collection 2` 和 `Device Collection 3` 的成员。
- `Device Collection 3` 已在其中部署 `Configuration Baseline 3`，但未选择“将此基线作为合规性策略的一部分进行评估”  。

当 `User1` 使用 `Device2` 时，在 `Compliance Policy 1` 评估时只会评估 `Configuration Baseline 2`。

> [!NOTE]
><!--5582516-->
> 如果合规性策略评估之前从未在客户端上评估过的新基线，则它可能会报告不合规。 如果在评估合规性时仍在运行基线评估，则会发生此情况。 要解决此问题，请单击“软件中心”中的“检查合规性”   。

### <a name="create-and-deploy-a-compliance-policy-with-a-rule-for-baseline-compliance-policy-assessment"></a><a name="bkmk_CA"></a>使用适用于基线合规性策略评估的规则创建并部署合规性策略

1. 在“资产与合规性”工作区中，展开“合规性设置”，然后选择“合规性策略”节点    。
1. 在功能区中单击“创建合规性策略”，以打开“创建合规性策略向导”   。 
1. 在“常规”页上，选择“适用于通过 Configuration Manager 客户端管理的设备的合规性规则”   。
   - 设备必须通过 Configuration Manager 客户端管理，才能在合规性策略评估中包含自定义配置基线。
1. 在“支持的平台”页上选择平台  。
1. 在“规则”页上，选择“新建”，然后选择“在合规性策略评估中包含配置的基线”条件    。

   ![“在合规性策略评估中包含配置的基线”条件](./media/3608345-create-compliance-policy-rule.png)

1. 单击“确定”，然后单击“下一步”以转到“摘要”页    。
1. 验证所做的选择，然后依次单击“下一步”和“关闭”   。
1. 在“合规性策略”节点中，右键单击所创建的策略，然后选择“部署”   。
1. 选择策略的集合、警报生成设置以及合规性评估计划。
1. 单击“确定”以部署合规性策略  。

### <a name="select-a-configuration-baseline-and-check-evaluate-this-baseline-as-part-of-compliance-policy-assessment"></a><a name="bkmk_eval-baseline"></a>选择配置基线并选中“将此基线作为合规性策略的一部分进行评估”

1. 在“资产与合规性”工作区中，展开“合规性设置”，然后选择“配置基线”节点    。
1. 右键单击部署到设备集合的现有基线，然后选择“属性”  。 如果需要，可以新建基线。
   - 基线必须部署到设备集合，而不是用户集合。
1. 启用“将此基线作为合规性策略的一部分进行评估”设置  。
   - 对于“设备配置”颁发机构是 Intune 的共同管理设备，请确保还选中了“即使对共同管理的客户端也始终应用此基线”   。
1. 单击“确定”将更改保存到配置基线  。

   ![“配置基线属性”对话框](./media/3608345-configuration-baseline-properties.png)

### <a name="log-files-for-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>将自定义配置基线包含在合规性策略评估中的日志文件

- ComplianceHandler.log
- SettingsAgent.log
- DCMAgent.log
- CIAgent.log

## <a name="next-steps"></a>后续步骤

[导入配置数据](import-configuration-data.md)
