---
title: 连接 Configuration Manager
titleSuffix: Configuration Manager
description: 关于将 Configuration Manager 与桌面分析连接的操作指南。
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 7015ab4c180ed56b00149ffbff99c9e5a8112e95
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125995"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>如何将 Configuration Manager 与桌面分析连接

桌面分析与 Configuration Manager 紧密集成。 首先，确保站点是最新的，以支持最新功能。 然后，在 Configuration Manager 中创建桌面分析连接。 最后，监视连接的运行状况。

## <a name="update-the-site"></a><a name="bkmk_hotfix"></a> 更新站点

首先，确保 Configuration Manager 站点运行的版本至少为 1902。 有关详细信息，请参阅[安装控制台内部更新](../core/servers/manage/install-in-console-updates.md)。

你还需要安装版本 1902 更新汇总 (4500571)，以支持与桌面分析的集成。 有关此更新的详细信息，请参阅 [Configuration Manager Current Branch（版本 1902）更新汇总](https://support.microsoft.com/help/4500571)。

1. 使用版本 1902 的更新汇总更新站点。 有关详细信息，请参阅[安装控制台内部更新](../core/servers/manage/install-in-console-updates.md)。

2. 更新客户端。 若要简化此过程，请考虑使用自动客户端升级。 有关详细信息，请参阅[升级客户端](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade)。

## <a name="connect-to-the-service"></a><a name="bkmk_connect"></a> 连接到服务

> [!TIP]
> 在启动向导前，请创建步骤 8 中提到的目标集合，因为启动向导后便无法在向导外部进行选择。

使用此过程将 Configuration Manager 连接到桌面分析并配置设备设置。 此过程是将层次结构连接到云服务的一次性过程。

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“Azure 服务”节点    。 在功能区中选择“配置 Azure 服务”  。

    > [!TIP]
    > 直接从“桌面分析服务”  节点连接到服务。 在 Configuration Manager 控制台中，转到“软件库”工作区，然后选择“桌面分析服务”节点   。 在“桌面分析新手？”  框中，选择第二个链接“将 Configuration Manager 连接到桌面分析服务”  。

2. 在 Azure 服务向导的“Azure 服务”页上，配置以下设置  ：

    - 指定 Configuration Manager 中的对象名称  。

    - 指定可选说明以帮助标识服务  。

    - 从可用服务列表中选择“桌面分析”  。

   选择“下一步”  。

3. 在“应用”  页上，选择相应的“Azure 环境”  。 然后选择“浏览”以查找 Web 应用  。

4. 如果你有想要为此服务重复使用的现有应用，请从列表中选择它，然后选择“确定”  。

5. 在大多数情况下，可以使用此向导创建用于桌面分析连接的应用。 选择“创建”。 <!-- 3572123 -->

    > [!TIP]
    > 如果无法从此向导创建应用，可以在 Azure AD 中手动创建应用，然后将其导入 Configuration Manager。 有关详细信息，请参阅[为 Configuration Manager 创建并导入应用](troubleshooting.md#create-and-import-app-for-configuration-manager)。

6. 在“创建服务器应用程序”  窗口中配置以下设置：

    - **应用程序名称**：Azure AD 中应用的易记名称。

    - **主页 URL**：Configuration Manager 不使用此值，但是 Azure AD 需要它。 默认情况下，此值为 `https://ConfigMgrService`。

    - **应用 ID URI**：此值在 Azure AD 租户中必须是唯一的。 它在 Configuration Manager 客户端用于请求访问服务的访问令牌中。 默认情况下，此值为 `https://ConfigMgrService`。

    - **密钥有效期**：从下拉列表中选择“1 年”或“2 年”   。 默认值为一年。

    选择“登录”  。 成功完成 Azure 身份验证后，该页面会显示 Azure AD 租户名称  以供参考。

    > [!NOTE]
    > 以“全局管理员”身份完成此步骤  。 Configuration Manager 不保存这些凭据。 此角色不需要 Configuration Manager 中的权限，其帐户也不需要与运行 Azure 服务向导的帐户相同。

    选择“确定”以在 Azure AD 中创建 Web 应用，并关闭“创建服务器应用程序”对话框  。 在“服务器应用”对话框中，选择“确定”  。 然后，在 Azure 服务向导的“应用”页上选择“下一步”  。

7. 在“诊断数据”页上配置下列设置  ：

    - **商业 ID**：此值应自动填充你的组织 ID。 如果未填充，请确保将代理服务器配置为允许所有必需的[终结点](enable-data-sharing.md#endpoints)，然后再继续。 或者，从[桌面分析门户](monitor-connection-health.md#bkmk_ViewCommercialID)中手动检索商业 ID。

    - Windows 10 诊断数据级别：至少选择“必需”。 有关详细信息，请参阅[诊断数据级别](enable-data-sharing.md#diagnostic-data-levels)。

        > [!TIP]
        > 在 Configuration Manager 版本 2002 及更低版本中，此值称为“基本”。<!-- 7363467 -->

    - **允许诊断数据中含有设备名称**：选择“启用”

        > [!NOTE]
        > 从 Windows 10 版本 1803 开始，默认情况下，不会将设备名称发送给 Microsoft。 如果不发送设备名称，它将在桌面分析中显示为“未知”。 此行为可能会导致难以识别和评估设备。

   选择“下一步”。 “可用功能”页显示了根据上一页的诊断数据设置提供的桌面分析功能。 选择“下一步”**** 继续操作，或者选择“上一步”**** 进行更改。

    ![Azure 服务向导中的可用功能页示例](media/available-functionality.png)

<a name="bkmk_Collections"></a>

8. 在“集合”页上，配置下列设置：

    - **显示名称**：桌面分析门户使用此名称显示此 Configuration Manager 连接。 用它来区分不同的层次结构和确定单独的层次结构中的集合。 使用“测试实验室”或“生产”等术语轻松区分环境中的多个层次结构 。

    - **目标集合**：此集合包括 Configuration Manager 使用你的商业 ID 和诊断数据设置配置的所有设备。 它是 Configuration Manager 连接到桌面分析服务的完整设备集。

    - **目标集合中的设备使用经用户身份验证的代理进行出站通信**：默认情况下，此值为“否”。 如果你的环境需要，请设置为“是”。

    - **选择要与桌面分析同步的特定集合**：选择“添加”以包括“目标集合”层次结构中的其他集合。 这些集合可在桌面分析门户中用于按照部署计划分组。 确保包括试点和试点排除集合。  <!-- 4097528 -->

        > [!TIP]
        > “选择集合”窗口仅显示受“目标集合”**** 限制的集合。
        >
        > 在下面的示例中，选择“CollectionA”作为目标集合。 然后，当添加其他集合时，你将看到 CollectionA、CollectionB 和 CollectionC。 不能添加 CollectionD。
        >
        > - CollectionA：受“所有系统”**** 集合的限制
        >     - CollectionB：受 CollectionA 的限制
        >         - CollectionC：受 CollectionB 的限制
        > - CollectionD：受“所有系统”**** 集合的限制
        >
        > 要管理桌面分析门户中可用的集合以按部署计划进行分组，请在 Configuration Manager 控制台中转到“管理”工作区，展开“云服务”，然后选择“Azure 服务”节点************。 选择与桌面分析 Azure 服务相关的条目，并更新“桌面分析集合”页面中的设置********。

        > [!IMPORTANT]
        > 这些集合在其成员身份更改时会继续同步。 例如，你的目标集合使用具有 Windows 7 成员身份规则的集合。 当这些设备升级到 Windows 10，并且 Configuration Manager 评估集合成员身份时，这些设备将退出集合和桌面分析。

9. 完成向导。

Configuration Manager 创建设置策略以配置目标集合中的设备。 此策略包括允许设备向 Microsoft 发送数据的诊断数据设置。 默认情况下，客户端每小时更新一次策略。 接收到新设置后，可能需要几个小时才能在桌面分析中使用这些数据。

## <a name="monitor-connection-health"></a><a name="bkmk_monitor"></a> 监视连接运行状况

监视桌面分析的设备配置。 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“桌面分析服务”节点，然后选择“连接运行状况”仪表板  。

有关详细信息，请参阅[监视连接运行状况](monitor-connection-health.md)。

Configuration Manager 会在创建连接的 60 分钟内同步集合。 在桌面分析门户中，转到“全局试点”，并查看 Configuration Manager 设备集合。

> [!NOTE]
> Configuration Manager 与桌面分析的连接依赖于服务连接点。 对此站点系统角色所做的任何更改都可能会影响与云服务的同步。 有关详细信息，请参阅[关于服务连接点](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move)。

## <a name="next-steps"></a>后续步骤

转到下一篇文章，将设备注册到桌面分析。
> [!div class="nextstepaction"]
> [注册设备](enroll-devices.md)
