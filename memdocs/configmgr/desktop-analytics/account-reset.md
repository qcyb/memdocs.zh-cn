---
title: 如何重置帐户
titleSuffix: Configuration Manager
description: 了解如何重置桌面分析帐户。
ms.date: 08/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 884d4864-950b-4139-b778-d5368e1f6ef2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4ece2d2725b8485f55fdce7761098577485bc2d1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706565"
---
# <a name="how-to-reset-your-account"></a>如何重置帐户

<!-- 3733897 -->

如果你在环境中设置了桌面分析，但想要通过加入和注册来重新开始，可使用此进程重置您的帐户。

## <a name="prerequisites"></a>必备条件

只有“全局管理员”  才能在 Azure 门户中重置帐户。

## <a name="behaviors"></a>行为

- 此过程不会更改任何现有 Azure AD 用户、应用或权限

- 如果选择添加新的工作区，则不会保留以下用户对资产的任何输入：
    - 重要性
    - Owner
    - 升级决策
    - 修正说明

## <a name="process"></a>过程

1. 作为具有“全局管理员”  角色的用户在 Microsoft 365 设备管理中打开[“桌面分析门户”](https://aka.ms/desktopanalytics)。

1. 在“全局设置”  菜单中，选择“已连接的服务”  。 在“注册设备”部分，选择此选项进行“重置”  。

1. 如果决定继续，则帐户将被重置。 你将需要重新设置桌面分析。

## <a name="next-steps"></a>后续步骤

重置后，刷新页面，然后重新运行加入进程。 有关详细信息，请参阅[如何设置桌面分析](set-up.md)。

如果在此进程中遇到任何问题，请与 Microsoft 支持部门联系以获得进一步的帮助。
