---
title: 注册设备以实现本地 MDM
titleSuffix: Configuration Manager
description: 了解在 Configuration Manager 中为本地移动设备管理（MDM）注册设备的方法。
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1ca7f792bb6b419dd1d20d495bdb53bc7c2be506
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724601"
---
# <a name="enroll-devices-for-on-premises-mdm-in-configuration-manager"></a>在 Configuration Manager 中为本地 MDM 注册设备

适用范围：  Configuration Manager (Current Branch)

若要管理 Configuration Manager 本地移动设备管理（MDM）的设备，首先需要注册这些设备。 然后 Configuration Manager 可以与设备进行管理任务的通信。 Configuration Manager 提供了两种注册设备的方法：

- **用户注册**：用户在其设备上启动注册过程。 要使用户注册成功，请在设备上安装受信任的根证书，并在客户端设置中预配用于注册的用户。 若要注册设备，用户只需输入其凭据。

    有关详细信息，请参阅[用户如何注册设备](user-enroll-devices-on-premises-mdm.md)。

- **批量注册**：设备的用户不会开始注册。 在 Configuration Manager 中创建批量注册包。 在设备上打开时，包将提供注册设备所需的信息。

    有关详细信息，请参阅[如何批量注册设备](bulk-enroll-devices-on-premises-mdm.md)。

若要详细了解 Configuration Manager 支持在本地 MDM 中注册设备的操作系统版本，请参阅支持的[配置](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS)。
