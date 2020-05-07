---
title: WSUS 中的 Endpoint Protection 恶意软件定义
titleSuffix: Configuration Manager
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
author: mestew
ms.author: mstewart
description: 了解如何将 Windows Server 更新服务配置为自动批准定义更新。
manager: dougeby
ms.openlocfilehash: 235caff52b877177b92792bf8d9fb3a2007127a5
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126022"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-wsus-for-configuration-manager"></a>启用 Endpoint Protection 恶意软件定义，以从 Configuration Manager 的 WSUS 中下载

适用范围：  Configuration Manager (Current Branch)

如果使用 WSUS 来使反恶意软件定义保持最新，可以将其配置为自动批准定义更新。 尽管推荐使用 Configuration Manager 软件更新使定义保持最新，但你也可将 WSUS 配置为允许用户手动更新定义。 使用以下过程将 WSUS 配置为定义更新源。

## <a name="synchronize-definition-updates-for-configuration-manager"></a>同步 Configuration Manager 定义更新

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“站点配置”，然后选择“站点”    。

1. 选择包含你的软件更新点的站点。 在功能区的“设置”组中，选择“配置站点组件”，再选择“软件更新点”    。

1. 在“软件更新点组件属性”窗口中，切换到“分类”选项卡   。选择“定义更新”  。

1. 若要指定随 WSUS 一起更新产品，请切换到“产品”选项卡   。

    - 对于 Windows 10 及更高版本：在“Microsoft”>“Windows”下，选择“Windows Defender”  。

    - 对于 Windows 8.1 及更低版本：在“Microsoft”>“Forefront”下，选择“System Center Endpoint Protection”  。

1. 单击“确定”以关闭“软件更新点组件属性”窗口   。

## <a name="synchronize-definition-updates-for-standalone-wsus"></a>同步独立 WSUS 的定义更新

WSUS 服务器未集成到 Configuration Manager 环境中时，请使用以下过程来配置 Endpoint Protection 更新。

1. 在 WSUS 管理控制台中，展开“计算机”，选择“选项”，然后选择“产品和分类”    。

1. 若要指定随 WSUS 一起更新产品，请切换到“产品”选项卡   。

    - 对于 Windows 10 及更高版本：在“Microsoft”>“Windows”下，选择“Windows Defender”  。

    - 对于 Windows 8.1 及更低版本：在“Microsoft”>“Forefront”下，选择“System Center Endpoint Protection”  。

1. 切换到“分类”  选项卡。选择“定义更新”和“更新”   。

## <a name="approve-definition-updates"></a>审批定义更新

必须先批准 Endpoint Protection 定义更新并将其下载到 WSUS 服务器，然后再将其提供给请求可用更新列表的客户端。 客户端连接到 WSUS 服务器以检查适用的更新，然后请求最新批准的定义更新。

### <a name="approve-definitions-and-updates-in-wsus"></a>审批 WSUS 中的定义和更新

1. 在 WSUS 管理控制台上，选择“更新”  。 然后选择“所有更新”  或选择想要审批的更新的分类。

1. 在更新列表中，右键单击想要批准进行安装的更新，然后选择“批准”  。

1. 在“批准更新”窗口中，选择想要为其批准更新的计算机组，然后选择“批准安装”   。

### <a name="configure-an-automatic-approval-rule"></a>配置自动批准规则

还可为定义更新和 Endpoint Protection 更新设置自动批准规则。 此操作会将 WSUS 配置为自动批准 WSUS 下载的 Endpoint Protection 定义更新。

1. 在 WSUS 管理控制台中，选择“选项”，然后选择“自动批准”   。

1. 在“更新规则”选项卡上，选择“新规则”   。

1. 在“添加规则”  窗口的“步骤1:  选择属性”下，选择“当更新位于特定分类中时”选项  。

    1. 在“步骤 2:  编辑属性”下，选择“任何分类”  。

    1. 清除除“定义更新”以外的所有选项，然后选择“确定”   。

1. 在“添加规则”  窗口的“步骤1:  选择属性”下，选择“当更新位于特定产品中时”选项  。

    1. 在“步骤 2:  编辑属性”下，选择“任何产品”  。

    1. 除“System Center Endpoint Protection”（用于 Windows 8.1 及更早版本）或“Windows Defender”（用于 Windows 10 及更高版本）   外，清除其余所有选项。 然后选择“确定”  。

1. 在“步骤 3:  指定一个名称”下，为该规则输入名称，然后选择“确定”  。

1. 在“自动批准”对话框中，选择新创建的规则，然后选择“运行规则”   。

> [!NOTE]
> 若要使 WSUS 服务器和客户端计算机上的性能最大化，则拒绝旧定义更新。 若要完成此任务，可以配置自动批准修订和自动拒绝过期更新。 有关详细信息，请参阅[“Microsoft 支持”文章 938947](https://support.microsoft.com/kb/938947)。

> [!div class="nextstepaction"]
> [创建和部署反恶意软件策略](endpoint-antimalware-policies.md)
