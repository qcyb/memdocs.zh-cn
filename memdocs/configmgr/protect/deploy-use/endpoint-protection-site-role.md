---
title: 创建 Endpoint Protection 点站点系统角色
titleSuffix: Configuration Manager
description: 了解如何将 Endpoint Protection 配置为管理 Configuration Manager 客户端计算机上的安全和恶意软件。
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 0a9dc0fe-a942-40a2-bab1-7eeee4d95380
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5a8714f5bacf97e440bae07834ee6df5430a3d37
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690315"
---
# <a name="create-an-endpoint-protection-point-site-system-role"></a>创建 Endpoint Protection 点站点系统角色

适用范围：  Configuration Manager (Current Branch)

必须先安装 Endpoint Protection 点站点系统角色，然后才能使用 Endpoint Protection。 必须将其仅安装在一个站点系统服务器上，并且必须将其安装在管理中心站点或独立主站点上层次结构的顶部。

根据是要为 Endpoint Protection 安装新的站点系统服务器还是使用现有站点系统服务器的具体情况，使用以下过程之一：
- [安装新的站点系统服务器](#new-site-system-server)
- [安装现有站点系统服务器](#existing-site-system-server)

> [!IMPORTANT]
>  安装 Endpoint Protection 点时，会在托管 Endpoint Protection 点的服务器上安装 Endpoint Protection 客户端。 在此客户端上禁用服务和扫描以使其能够与服务器上安装的任何现有反恶意软件解决方案共存。 如果之后使此服务器由 Endpoint Protection 进行管理，并选择可删除任何第三方反恶意软件解决方案的选项，将不会删除第三方产品。 必须手动卸载此产品。

## <a name="new-site-system-server"></a>新建站点系统服务器

1.  在 Configuration Manager 控制台中，单击“管理”  。

2.  在“管理”  工作区中，展开“站点配置”  ，然后单击“服务器和站点系统角色”  。

3.  在“主页”  选项卡上的“创建”  组中，单击“创建站点系统服务器”  。

4.  在“常规”  页上，指定站点系统的常规设置，然后单击“下一步”  。

5.  在“系统角色选择”  页上的可用角色列表中选择“Endpoint Protection 点”  ，然后单击“下一步”  。

6.  在“Endpoint Protection”  页上，选择“我接受 Endpoint Protection 许可条款”  复选框，然后单击“下一步”  。

    > [!IMPORTANT]
    >  必须接受许可条款，才能在 Configuration Manager 中使用 Endpoint Protection。

7.  在“云保护服务”  页面上，选择想要发送到 Microsoft 以帮助开发新定义的信息的级别，然后单击“下一步”  。

    > [!NOTE]
    >  此选项配置默认使用的云保护服务（以前称为 Microsoft Active Protection Service 或 MAPS）设置。 然后可以为你创建的每个反恶意软件策略配置自定义设置。 加入云保护服务，通过为 Microsoft 提供有助于 Microsoft 将反恶意软件定义保持为最新状态的恶意软件示例，以此来帮助计算机保持更加安全的状态。 此外，在加入云保护服务后，Endpoint Protection 客户端可以使用动态签名服务在新定义发布到 Windows 更新前先下载这些新定义。 有关详细信息，请参阅[如何为 Endpoint Protection 创建和部署反恶意软件策略](endpoint-antimalware-policies.md)。

8.  完成向导。


## <a name="existing-site-system-server"></a>现有站点系统服务器

1.  在 Configuration Manager 控制台中，单击“管理”  。

2.  在“管理”  工作区中，展开“站点配置”  ，单击“服务器和站点系统角色”  ，然后选择想用于 Endpoint Protection 的服务器。

3.  在“主页”  选项卡上的“服务器”  组中，单击“添加站点系统角色”  。

4.  在“常规”  页上，指定站点系统的常规设置，然后单击“下一步”  。

5.  在“系统角色选择”  页上的可用角色列表中选择“Endpoint Protection 点”  ，然后单击“下一步”  。

6.  在“Endpoint Protection”  页上，选择“我接受 Endpoint Protection 许可条款”  复选框，然后单击“下一步”  。

    > [!IMPORTANT]
    >  必须接受许可条款，才能在 Configuration Manager 中使用 Endpoint Protection。

7.  在“云保护服务”  页面上，选择想要发送到 Microsoft 以帮助开发新定义的信息的级别，然后单击“下一步”  。

    > [!NOTE]
    >  此选项配置默认使用的云保护服务（以前称为 MAPS）设置。 然后可以为你配置的每个反恶意软件策略配置自定义设置。 有关详细信息，请参阅[如何为 Endpoint Protection 创建和部署反恶意软件策略](endpoint-antimalware-policies.md)。

8.  完成向导。
