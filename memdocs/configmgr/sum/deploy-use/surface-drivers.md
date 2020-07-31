---
title: 管理 Surface 驱动程序更新
titleSuffix: Configuration Manager
description: Configuration Manager 将要部署的 Surface 驱动程序更新同步到 Surface 设备。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 06/18/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9f9f4e6-5b4f-4b8f-94d6-db9b2b239113
ms.openlocfilehash: f276db618a2e67832ffa5575622e00eea02c7422
ms.sourcegitcommit: 8a4a86ee8044f273dcece26155132a801f3d8f9a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/30/2020
ms.locfileid: "87438631"
---
# <a name="manage-surface-drivers-with-configuration-manager"></a>使用 Configuration Manager 管理 Surface 驱动程序

适用范围：System Center Configuration Manager (Current Branch)

使用 System Center Configuration Manager，可以同步 Surface 设备的驱动程序并将其部署为软件更新。 借助此功能，可以确保 Surface 设备运行的是最新的可用驱动程序。 此同步在版本 1706 中作为预发行功能首次引入，并在 1710 中成为一项功能。 <!--3684621, 3608197, 1098490-->

## <a name="prerequisites-for-synchronizing-surface-drivers"></a>同步 Surface 驱动程序的先决条件

- 连接了 Internet 的顶层软件更新点。
- 所有软件更新点必须运行安装有累积更新 KB4025339 的 Windows Server 2016 或更高版本。
- 默认情况下，Configuration Manager 不启用此项可选功能。 在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。<!--505213-->  

## <a name="enable-sync-for-surface-drivers"></a>为 Surface 驱动程序启用同步

若要启用 Surface 驱动程序的同步，请执行以下步骤：

1. 将 Configuration Manger 控制台连接到顶层站点服务器。
1. 转到“管理” > “站点配置” > “站点”，然后单击顶层站点。
1. 在功能区中，选择“设置” > “配置站点组件” > “软件更新点”  。
1. 依次单击“分类”选项卡、“包括 Microsoft Surface 驱动程序和固件更新”复选框和“应用”  。

     ![启用软件更新点属性中的 Surface 驱动程序](media/enable-surface-driver-sync.png)

1. 在“软件更新点组件属性”中，单击“产品”选项卡。有关详细信息，请参阅 [Surface 驱动程序的产品](#bkmk_prod)和 [Surface 模型](#bkmk_models)部分。
1. 选择要支持 Surface 驱动程序的每个版本的 Windows 10 的产品。 你将注意到，驱动程序的每个产品都有两个不同版本：

   - Windows 10 版本更新及更高版本维护驱动程序
   - Windows 10 版本更新及更高版本升级和维护驱动程序。

     ![Windows 10 版本驱动程序产品列表](media/surface-driver-products-sup.png)

1. 选择产品后，单击“确定”。
1. [同步软件更新点](../get-started/synchronize-software-updates.md)，将 Surface 驱动程序引入 Configuration Manager。
1. 同步 Surface 驱动程序后，按照与部署其他更新相同的方式来部署它们。

## <a name="products-for-surface-drivers"></a><a name="bkmk_prod"></a> Surface 驱动程序的产品

大多数驱动程序属于以下产品组：

- Windows 10 及更高版本驱动程序
- Windows 10 及更高版本升级和维护驱动程序
- Windows 10 周年更新及更高版本维护驱动程序
- Windows 10 周年更新及更高版本升级和维护驱动程序
- Windows 10 创意者更新及更高版本维护驱动程序
- Windows 10 创意者更新及更高版本升级和维护驱动程序
- Windows 10 Fall Creators Update 及更高版本维护驱动程序
- Windows 10 Fall Creators Update 及更高版本升级和维护驱动程序
- Windows 10 S 及更高版本维护驱动程序
- 用于测试的 Windows 10 S 版本 1709 及更高版本维护驱动程序
- 用于测试的 Windows 10 S 版本 1709 及更高版本升级和维护驱动程序
- Windows 10 S 版本 1803 及更高版本维护驱动程序
- Windows 10 S 版本 1803 及更高版本升级和维护驱动程序
- Windows 10 S 版本 1809 及更高版本，维护驱动程序
- Windows 10 S 版本 1809 及更高版本，升级和维护驱动程序
- Windows 10 S 版本 1903 及更高版本，维护驱动程序
- Windows 10 S 版本 1903 及更高版本，升级和维护驱动程序
- Windows 10 版本 1803 及更高版本维护驱动程序
- Windows 10 版本 1803 及更高版本升级和维护驱动程序
- Windows 10 版本 1809 及更高版本，维护驱动程序
- Windows 10 版本 1809 及更高版本，升级和维护驱动程序
- Windows 10 版本 1903 及更高版本，维护驱动程序
- Windows 10 版本 1903 及更高版本，升级和维护驱动程序

> [!NOTE]
> 大多数 Surface 驱动程序属于多个 Windows 10 产品组。 可能不需要选择此处列出的所有产品。 为了帮助减少填充更新目录的产品数量，我们建议你仅选择环境进行同步所需的产品。

## <a name="surface-models"></a><a name="bkmk_models"></a> Surface 模型

下表包含 Configuration Manager 可在其上安装驱动程序的 Windows 10 的 Surface 模型和版本。 Configuration Manager 无法在将 Surface 驱动程序更新发布到 Microsoft 更新目录的同一天提供这些更新。 Configuration Manager 维护要导入的 Surface 驱动程序的列表。 将介绍需要 Windows 10 S 产品的设备。 Microsoft 旨在将 Surface 驱动程序添加到每月第二个星期二的允许列表中，以便可以同步到 Configuration Manager。 有关详细信息，请参阅[常见问题解答](#bkmk_faq)。

</br>

|Surface 模型|Windows 10 1709| Windows 10 1803|Windows 10 1809|Windows 10 1903|Windows 10 1909|
|----|----|----|----|----|----|
|Surface Pro 3|是| 是| 是 |是|是|
|Surface Pro 4|是| 是| 是 |是|是|
|Surface Pro 6|不适用| 是| 是 |是|是|
|Surface Pro 7|不适用| 不适用| 不适用 |是|是|
|Surface Pro X|不适用| 不适用| 不适用 |是|是|
|Surface Book|是| 是| 是 |是|是|
|Surface Book 2|是| 是| 是 |是|是|
|Surface Book 3|不适用| 不适用| 不适用 |是|是|
|Surface Laptop|是，已选中产品“Windows 10 S 版本 1709 及更高版本维护驱动程序”| 是，已选中产品“Windows 10 S 版本 1803 及更高版本维护驱动程序”|是，已选中产品“Windows 10 S 版本 1809 及更高版本升级和维护驱动程序”|是，已选中产品“Windows 10 S 版本 1903 及更高版本升级和维护驱动程序”|是，已选中产品“Windows 10 S 版本 1903 及更高版本升级和维护驱动程序”|
|Surface Laptop 2|不适用| 是 |是|是|是|
|Surface Laptop 3|不适用| 不适用|不适用|是 |是|
|Surface Go|不适用| 是，已选中产品“Windows 10 S 版本 1803 及更高版本维护驱动程序”|是，已选中产品“Windows 10 S 版本 1809 及更高版本升级和维护驱动程序”|是，已选中产品“Windows 10 S 版本 1903 及更高版本升级和维护驱动程序”|是，已选中产品“Windows 10 S 版本 1903 及更高版本升级和维护驱动程序”|
|Surface Go 2|不适用| 不适用| 是 |是|是，已选中产品“Windows 10 S 版本 1903 及更高版本升级和维护驱动程序”|
|Surface Studio|是| 是| 是 |是|是|
|Surface Studio 2|不适用| 是| 是 |是|是|

## <a name="verify-the-configuration"></a>验证配置

若要验证是否已正确配置软件更新点，请使用 WsyncMgr.log 和 WCM.log 。

1. 打开 WsyncMgr.log 并检查以下日志条目：

    ```text
    Surface Drivers can be supported in this hierarchy since all software update points are on Windows Server 2016, WCM SCF property Sync Catalog Drivers is set. 
    …
    Sync Catalog Drivers SCF value is set to : 1
    ```

1. 如果已在 WsyncMgr.log 中记录以下任一条目，请仔细检查是否已选中软件更新点属性中的“包括 Microsoft Surface 驱动程序和固件更新”选项 ：
   - `Sync Surface Drivers option is not set`
   - `Sync Catalog Drivers SCF value is set to : 0`

1. 打开 WCM.log 并查找类似于以下条目的项：
   ```text
   <Categories>
   <Category Id="Product:05eebf61-148b-43cf-80da-1c99ab0b8699"><![CDATA[Windows 10 and later drivers]]></Category>
   <Category Id="Product:06da2f0c-7937-4e28-b46c-a37317eade73"><![CDATA[Windows 10 Creators Update and Later Upgrade & Servicing Drivers]]></Category>
   <Category Id="Product:c1006636-eab4-4b0b-b1b0-d50282c0377e"><![CDATA[Windows 10 S and Later Servicing Drivers]]></Category>
   … …
   </Categories>
   ```

   此条目是一个 XML 元素，其中列出了当前由软件更新点服务器同步的每个产品组和分类。 如果找不到所选产品，请仔细检查是否已保存软件更新点的产品。
1. 你还可以等到下次同步完成。 然后，检查 Configuration Manager 控制台的“软件更新”中是否已列出 Surface 驱动程序和固件更新。 例如，控制台可能会显示以下信息：![已在 Configuration Manger 控制台中同步 Surface 驱动程序](media/synchronized-surface-drivers.png)

##  <a name="frequently-asked-questions-faq"></a><a name="bkmk_faq"></a>常见问题 (FAQ)

### <a name="after-i-follow-the-steps-in-this-article-my-surface-drivers-are-still-not-synchronized-why"></a>按照本文中的步骤操作后，我的 Surface 驱动程序仍未同步。 原因是什么？

如果从上游 Windows Server Update Services (WSUS) 服务器（而不是 Microsoft 更新）同步，请确保将上游 WSUS 服务器配置为支持和同步 Surface 驱动程序更新。 所有下游服务器仅限于上游 WSUS 服务器数据库中存在的更新。

在 WSUS 中，有超过 68,000 个更新分类为驱动程序。 为了防止与非 Surface 相关的驱动程序同步到 Configuration Manager，Microsoft 针对允许列表对驱动程序同步进行筛选。 在发布新的允许列表并将其合并到 Configuration Manager 后，新的驱动程序会在下次同步后添加到控制台。 Microsoft 旨在将 Surface 驱动程序添加到每月第二个星期二的允许列表中，以便可以同步到 Configuration Manager。

如果 Configuration Manager 环境处于脱机状态，则每次将[服务更新](../../core/servers/manage/use-the-service-connection-tool.md)导入到 Configuration Manager 时会导入新的允许列表。 还必须导入包含驱动程序的[新 WSUS 目录](../get-started/synchronize-software-updates-disconnected.md)，才能在 Configuration Manager 控制台中显示更新。 由于独立 WSUS 环境包含的驱动程序多于 Configuration Manager SUP，因此建议你建立一个具有联机功能的 Configuration Manager 环境，并将其配置为同步 Surface 驱动程序。 这样会提供与脱机环境最相似的较小的 WSUS 导出。

如果 Configuration Manager 环境处于联机状态且能够检测新更新，你将自动收到列表的更新。 如果看不到预期的驱动程序，请查看 WCM.log 和 WsyncMgr.log 以了解任何同步失败。

### <a name="my-configuration-manager-environment-is-offline-can-i-manually-import-surface-drivers-into-wsus"></a>我的 Configuration Manager 环境处于脱机状态，我可以手动将 Surface 驱动程序导入到 WSUS 中吗？

不能。 即使更新已导入到 WSUS 中，如果未在允许列表中列出，更新也不会导入到 Configuration Manager 控制台以进行部署。 必须使用[服务连接工具](../../core/servers/manage/use-the-service-connection-tool.md)将服务更新导入到 Configuration Manager 才能更新允许列表。

### <a name="what-alternative-methods-do-i-have-to-deploy-surface-driver-and-firmware-updates"></a>需要哪些替代方法来部署 Surface 驱动程序和固件更新？

有关如何通过备用通道部署 Surface 驱动程序和固件更新的信息，请参阅[管理 Surface 驱动程序和固件更新](https://docs.microsoft.com/surface/manage-surface-driver-and-firmware-updates)。 如果要下载 .msi 或 .exe 文件，然后通过传统软件部署通道进行部署，请参阅[使用 Configuration Manager 持续更新 Surface 固件](https://docs.microsoft.com/archive/blogs/thejoncallahan/keeping-surface-firmware-updated-with-configuration-manager)。

## <a name="next-steps"></a>后续步骤

有关 Surface 驱动程序的详细信息，请参阅以下文章：

- [Surface 和 System Center Configuration Manager 的注意事项](https://docs.microsoft.com/surface/considerations-for-surface-and-system-center-configuration-manager#deploy-surface-app-with-configuration-manager)
- [Surface 更新历史记录](https://support.microsoft.com/help/4036283/surface-surface-update-history)
- [下载适用于 Surface 设备的最新固件和驱动程序](/surface/manage-surface-driver-and-firmware-updates)
