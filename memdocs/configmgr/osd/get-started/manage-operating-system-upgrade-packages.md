---
title: 管理 OS 升级包
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中管理 OS 升级包。
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cc50fc60601b63bca7b4a4b01ba3fb4a39fd8b91
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708865"
---
# <a name="manage-os-upgrade-packages-with-configuration-manager"></a>使用 Configuration Manager 管理 OS 升级包

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 中的 OS 升级包包含用于在计算机上升级现有 OS 的 Windows 安装程序源文件。 本文介绍如何添加、分发和维护 OS 升级包。

> [!NOTE]
> OS 升级包还可用于 Windows 的新安装。 不过，这取决于驱动程序是否与此方法兼容。 从 OS 升级包执行 Windows 的新安装时，仍在 Windows PE 中安装驱动程序，而不仅仅是在 Windows PE 中注入。 在 Windows PE 中安装时，某些驱动程序与之不兼容。 在 Windows PE 中安装时，如果驱动程序与之不兼容，则改为使用 [OS 映像](manage-operating-system-images.md)，如 install.wim  。

## <a name="add-an-os-upgrade-package"></a><a name="BKMK_AddOSUpgradePkgs"></a> 添加 OS 升级包  

在使用 OS 升级包之前，请先将其添加到 Configuration Manager 站点。

1. 在 Configuration Manager 控制台中，转到“软件库”工作区，展开“操作系统”，然后选择“操作系统升级包”节点    。  

2. 在功能区的“主页”选项卡上的“创建”组中，选择“添加操作系统升级包”    。 此操作将启动“添加操作系统升级向导”。  

3. 在“数据源”页面上，指定以下设置  ：

    - OS 升级包的安装源文件的网络**路径**。 例如，`\\server\share\path`。  

        > [!NOTE]  
        >  安装源文件包含 setup.exe 和其他文件以及用于安装 OS 的文件夹。  

        > [!IMPORTANT]  
        >  限制对这些安装源文件的访问，以防受到恶意篡改。  

    - 从选定升级包的 install.wim 文件中提取特定映像索引  ，然后从列表中选择映像索引。<!--4931110--> 从版本 1910 开始，此选项自动导入单个索引，而不是文件中的所有映像索引。 使用此选项会使得映像文件更小，以及脱机维护更快。 它还支持[优化映像服务](#bkmk_resetbase)的过程，适用于应用软件更新后更小的映像文件。  

        > [!IMPORTANT]  
        > Configuration Manager 覆盖 OS 升级包中的现有 install.wim。 它会将映像索引提取到临时位置，然后将其移动到原始源目录。 在导入 OS 升级包并启用此选项之前，请确保备份原始源文件。

    - 如果要在客户端上预缓存内容，请指定映像的**体系结构**和**语言**。 有关详细信息，请参阅[配置预缓存内容](../deploy-use/configure-precache-content.md)。  

4. 在“常规”页面上，指定以下信息  。 当你有多个 OS 升级包时，可利用这些信息对其进行识别。  

    - **名称**：OS 升级包的唯一名称。  

    - **版本**：可选的版本标识符。 此属性无需为该升级包的 OS 版本。 它通常为组织的包的版本。  

    - **注释**：可选的简要说明。  

5. 完成向导。  

接下来，将 OS 升级包分发到分发点。  

## <a name="distribute-content-to-a-distribution-point"></a><a name="BKMK_Distribute"></a> 将内容分发到分发点  

将 OS 升级包分发到与其他内容相同的分发点。 在部署任务序列之前，请将 OS 升级包分发到至少一个分发点。 有关详细信息，请参阅[分发内容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)。  

[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]

## <a name="next-steps"></a>后续步骤

[创建用于升级 OS 的任务序列](../deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)
