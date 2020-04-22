---
title: 预发行功能
titleSuffix: Configuration Manager
description: 预发行功能是指 Current Branch 中的功能，用于在生产环境中的早期测试。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e341fab9f76ab6994f051dbd5e2333c3f521b4d9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703535"
---
# <a name="pre-release-features-in-configuration-manager"></a>Configuration Manager 中的预发行功能

适用范围：  Configuration Manager (Current Branch)

预发行功能是指 Current Branch 中的功能，用于在生产环境中的早期测试。 这些功能完全受支持，但仍在积极开发中。 可能会在移出预发行类别后，对它们进行更改。

## <a name="give-consent"></a>同意  

同意使用预发行功能之后，才能使用。 同意是对每个层次结构执行的一次性操作，不能撤消。 除非同意，否则不能启用更新随附的新的预发行功能。 启用预发行功能后，将无法关闭。

1. 在 Configuration Manager 控制台中，转到“管理”  工作区，展开“站点配置”  ，然后选择“站点”  节点。  

2. 单击功能区中的“层次结构设置”  。  

3. 在“层次结构设置属性”的“常规”选项卡上，启用“同意使用预发行功能”的选项   。 单击" **确定**"。  

## <a name="enable-pre-release-features"></a>启用预发行功能

安装包含预发行功能的更新时，这些功能和此次更新包含的常规功能在“更新和维护服务向导”中可见。

### <a name="if-you-have-given-consent"></a>如果已同意

在“更新和维护服务向导”中，启用预发行功能。 请选择预发行功能，就像选择任何其他功能那样。

（可选）等待稍后从“管理”工作区的“更新和维护服务”下的“功能”节点中启用预发行功能    。 选择一项功能，然后在功能区中单击“开”  。 同意后才可使用该选项。

### <a name="if-you-havent-given-consent"></a>如果尚未同意

在“更新和维护服务向导”中，预发行功能可见，但不能启用。 安装更新后，这些功能在“功能”节点中可见  。 但是，只有同意后才能启用。

> [!IMPORTANT]  
> 在多站点层次结构中，只能从管理中心站点启用可选功能或预发布功能。 此行为确保层次结构中不会出现冲突。 <!--507197-->  
>
> 如果在独立主站点中同意这样做，并通过安装新的管理中心站点扩展层次结构，则还必须在管理中心站点也同意这样做。  

启用预发行功能时，配置管理器层次结构管理器 (HMAN) 必须在该功能可用之前处理更改。 更改的处理通常是即时的。 根据 HMAN 处理周期，可能最多需要 30 分钟才能完成。 处理更改后，重启控制台，然后再使用该功能。

## <a name="list-of-pre-release-features"></a><a name="bkmk_table"></a> 预发行功能列表

<!--Note/tip for target article

> [!Note]  
> In this version of Configuration Manager, <feature name> is a pre-release feature. To enable it, see [Pre-release features](pre-release-features.md).  

> [!Tip]  
> This feature was first introduced in version 1702 as a [pre-release feature](pre-release-features.md). Beginning with version 1906, it's no longer a pre-release feature.  

-->

<!-- With each current branch release, to help purge this list a bit, remove any entries that were added as a full feature in a version that's no longer supported -->
| 功能          | 添加为预发行功能 | 添加为完整版功能 |
|------------------|----------------------|-------------------------|
| [业务流程组](../../../sum/deploy-use/orchestration-groups.md) <!--3098816--> | 版本 2002 | ![尚未发行](media/red_x.png) |
| [任务序列部署类型](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt) <!--3555953--> | 版本 2002 | ![尚未发行](media/red_x.png) |
| [删除管理中心站点](../deploy/install/remove-central-administration-site.md) <!-- 3607277 --> | 版本 2002 | ![尚未发行](media/red_x.png) |
| [任务序列调试器](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71--> | 版本 1906 | ![尚未发行](media/red_x.png) |
| [应用程序组](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D--> | 版本 1906 | ![尚未发行](media/red_x.png) |
| [Azure Active Directory 用户组发现](../deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->| 版本 1906 | 版本 2002 |
| [将集合成员身份结果同步到 Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->| 版本 1906| 版本 2002 |
| [CMPivot 独立应用](cmpivot.md#bkmk_standalone) <!--3555890/4692885,no GUID--> | 版本 1906 | 版本 2002 |
| [SMS 提供程序管理服务](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_admin-service) <!--1359052--> | 版本 1810 | 版本 1906 |
| [增强型 HTTP 站点系统](../../plan-design/hierarchy/enhanced-http.md) <!--1356889,1358228--> | 版本 1806 | 版本 1810 |
| [适用于共同管理设备的客户端应用](../../../comanage/workloads.md#client-apps) <br/> （先前称为适用于共同托管设备的移动应用  ） <!--1357892/3600959,CC3AE625-BF72-49B1-8AB1-AF0DCF2D6F4C--> | 版本 1806 | 版本 2002 |
| [包转换管理器](../../../apps/pcm/package-conversion-manager.md) <!--1357861--> | 版本 1806 | 版本 1810 |
| [分阶段部署](../../../osd/deploy-use/create-phased-deployment-for-task-sequence.md) <!--1356837--> | 版本 1802 | 版本 1806 |
| [Windows Defender 应用程序控制管理](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md) <!--3600958 (fka 1355092 & 1319346)--> | 版本 1702 | 版本 1906 |
| [维护群集感知集合（服务器组）](../../../sum/deploy-use/service-a-server-group.md) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697--> | 版本 1602 | ![尚未发行](media/red_x.png) |

<!--Image used = ![Not yet](media/red_x.png) -->

> [!TIP]  
> 若要详细了解必须先启用的非预发布功能，请参阅[启用更新中的可选功能](install-in-console-updates.md#bkmk_options)。  
>
> 若要详细了解仅在技术预览分支中可用的功能，请参阅[技术预览版](../../get-started/technical-preview.md)。  
