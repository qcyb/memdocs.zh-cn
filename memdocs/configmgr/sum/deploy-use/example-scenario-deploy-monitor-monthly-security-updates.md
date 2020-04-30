---
title: 部署和监视更新的示例方案
titleSuffix: Configuration Manager
description: 如何使用 Configuration Manager 中的软件更新来部署和监视每月软件更新。
ms.date: 10/21/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: c32f757a-02da-43f2-b055-5cfd097d8c43
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ea654c4ec13b95b78a65c85d9d36ce576619854e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696125"
---
# <a name="example-scenario-to-deploy-and-monitor-monthly-software-updates"></a>部署和监视每月软件更新的示例方案

适用范围：  Configuration Manager (Current Branch)

本主题提供一个示例方案，以说明如何在 Configuration Manager 中使用软件更新来部署和监视 Microsoft 每月发布的安全软件更新。  

 在此方案中，我们遵循 Woodgrove Bank 的 Configuration Manager 管理员的操作。 管理员需要创建一个具有以下条件和要求的软件更新部署策略：  

- Microsoft 在每月的第二个星期二发布安全软件更新，而一周后将会出现活跃的软件更新部署活动。 此事件通常称为“周二补丁日”。  

- 在分发点上下载并暂存软件更新。 然后，在部分客户端中测试部署，之后 ConfigMgr 管理员在生产环境中全面部署软件更新。  

- 管理员必须能够按月或按年监视软件更新的符合性。  

  此方案假定已经实施了软件更新点基础结构。 请使用以下信息在 Configuration Manager 中规划和配置软件更新。  

|过程|参考|  
|-------------|---------------|  
|查看软件更新的关键概念。|[软件更新简介](../understand/software-updates-introduction.md)|  
|规划软件更新。 此信息帮助你制定计划以全面考虑容量问题，以及确定软件更新点基础结构、软件更新点的安装、同步设置和软件更新的客户端设置。|[规划软件更新](../plan-design/plan-for-software-updates.md)|  
|配置软件更新。 此信息帮助你在层次结构中安装和配置软件更新点，并帮助你配置和同步软件更新。<br /><br /> 在此方案中，ConfigMgr 管理员将软件更新同步计划配置为在每月的第二个星期三执行，以确保他可以检索 Microsoft 发布的最新安全软件更新。|[同步软件更新](../get-started/synchronize-software-updates.md)|  

 本主题中的下列部分提供了有助于在组织中部署和监视 Configuration Manager 安全软件更新的示例步骤。

##  <a name="step-1-create-a-software-update-group-for-yearly-compliance"></a><a name="BKMK_Step1"></a>步骤 1：为每年符合性创建软件更新组  
 Configuration Manager 管理员会创建一个软件更新组，它可用于监视 2016 年发布的所有安全软件更新的符合性。 管理员执行下表中的步骤。  

|过程|参考|  
|-------------|---------------|  
|Configuration Manager 管理员从 Configuration Manager 控制台中的“所有软件更新”  节点中添加条件，以仅显示满足以下条件的于 2015 年发布或修订的安全软件更新：<br /><br /><ul><li>**条件**：发布或修订日期</li><li>**条件**：大于或等于特定日期<br />**值**：2015/1/1</li><li>**条件**：更新分类<br />**值**：安全更新</li><li>**条件**：已过期 <br />**值**：否</li></ul>|没有其他信息|
|ConfigMgr 管理员将所有经过筛选的软件更新添加到一个具有以下要求的新的软件更新组中：<br /><br /><ul><li>**名称**：符合性组 - Microsoft 安全更新 2015</li><li>**描述**：软件更新|[将软件更新添加到更新组](add-software-updates-to-an-update-group.md)|  

##  <a name="step-2-create-an-automatic-deployment-rule-for-the-current-month"></a><a name="BKMK_Step2"></a>步骤 2：为当月创建自动部署规则  
 Configuration Manager 管理员为 Microsoft 在当月发布的安全软件更新创建自动部署规则。 管理员执行下表中的步骤。  

|过程|参考|  
|-------------|---------------|  
|ConfigMgr 管理员创建具有以下要求的自动部署规则：<br /><br /><ol><li>在“常规”选项卡上，ConfigMgr 管理员进行以下配置  ：<br /> <ul><li>将名称指定为“每月安全更新”  。</li><li>选择一个包含有限客户端的测试集合。</li><li>选择“创建新的软件更新组”  。</li><li>确保未选中“运行此规则后启用部署”  。</li></ul></li><li>在“部署设置”选项卡上，ConfigMgr 管理员选择默认设置  。</li><li>在“软件更新”  页上，ConfigMgr 管理员配置以下属性筛选器和搜索条件：<br /><ul><li>发布或修订日期 **最近 1 个月**。</li><li>更新分类 **安全更新**。</li></ul></li><li>在“评估”页上，ConfigMgr 管理员使此规则能够按照为每月的第二个星期四制定的计划运行    。  ConfigMgr 管理员还确认了将同步计划设置为在每月的第二个星期三运行   。</li><li>ConfigMgr 管理员使用“部署计划”、“用户体验”、“警报”和“下载设置”页上的默认设置。</li><li>在“部署包”页面上，ConfigMgr 管理员指定新的部署包  。</li><li>ConfigMgr 管理员使用“下载位置”和“语言选择”页上的默认设置。</li></ol>|[自动部署软件更新](automatically-deploy-software-updates.md)|  

##  <a name="step-3-verify-that-software-updates-are-ready-to-deploy"></a><a name="BKMK_Step3"></a>步骤 3：验证软件更新是否做好部署准备  
 在每月的第二个星期四，ConfigMgr 管理员都会验证软件更新是否做好部署准备。 管理员执行以下步骤。  

|过程|参考|  
|-------------|---------------|  
|ConfigMgr 管理员验证软件更新同步是否已成功完成。|[软件更新同步状态](monitor-software-updates.md#BKMK_SUSyncStatus)|  

##  <a name="step-4-deploy-the-software-update-group"></a><a name="BKMK_Step4"></a>步骤 4：部署软件更新组  
 在 ConfigMgr 管理员确认软件更新已准备好部署后，他们会部署软件更新。 管理员执行下表中的步骤。  

|过程|参考|  
|-------------|---------------|  
|ConfigMgr 管理员为新的软件更新组创建两个测试部署。 管理员为每个部署设想以下环境：<br /><br /> **工作站测试部署**：对于工作站测试部署，ConfigMgr 管理员有以下考虑：<br /><br /><ul><li>指定一个包含了部分工作站客户端的部署集合，以验证部署。</li><li>配置适用于他的环境中的工作站客户端的部署设置。</li></ul><br />**服务器测试部署**：对于服务器测试部署，ConfigMgr 管理员有以下考虑：<br /><br /><ul><li>指定一个包含了部分服务器客户端的部署集合，以验证部署。</li><li>配置适用于他的环境中的服务器客户端的部署设置。</li></ul>|[部署软件更新](deploy-software-updates.md)|  
|ConfigMgr 管理员验证测试部署是否已成功部署。|[软件更新部署状态](monitor-software-updates.md#BKMK_SUDeployStatus)|  
|ConfigMgr 管理员利用包含其生产工作站和服务器的新集合更新这两个部署。|没有其他信息|  

##  <a name="step-5-monitor-compliance-for-deployed-software-updates"></a><a name="BKMK_Step5"></a>步骤 5：监视所部署的软件更新的符合性  
 ConfigMgr 管理员会监视其软件更新部署的符合性。 管理员执行下表中的步骤。  

|过程|参考|  
|-------------|---------------|  
|ConfigMgr 管理员在 Configuration Manager 控制台中监视软件更新部署状态，并检查通过该控制台提供的软件更新部署报表。|[监视软件更新](../../sum/deploy-use/monitor-software-updates.md)|  

##  <a name="step-6-add-monthly-software-updates-to-the-yearly-update-group"></a><a name="BKMK_Step6"></a>步骤 6：将每月的软件更新添加到每年更新组  
 ConfigMgr 管理员将每月软件更新组中的软件更新添加到每年软件更新组。 管理员执行下表中的步骤。  

|过程|参考|  
|-------------|---------------|  
|ConfigMgr 管理员选择每月软件更新组中的软件更新，然后将它们添加到为每年符合性创建的软件更新组。 管理员跟踪软件更新符合性，并创建用于管理的不同报表。|[将软件更新添加到已部署的更新组中](add-software-updates-to-an-update-group.md)|  

ConfigMgr 管理员已成功完成每月的安全软件更新部署。 管理员继续监视和报告软件更新符合性，以确保其环境中的客户端处于可接受的符合性级别内。  

##  <a name="recurring-monthly-process-to-deploy-software-updates"></a><a name="BKMK_MonthlyProcess"></a>每月定期进行的软件更新部署过程  
 在 ConfigMgr 管理员部署软件更新的第一个月之后，管理员执行步骤三到步骤六，以部署 Microsoft 发布的每月安全软件更新。  
