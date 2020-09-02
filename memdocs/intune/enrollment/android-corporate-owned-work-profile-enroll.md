---
title: 设置 Android Enterprise 公司拥有的工作配置文件设备的 Intune 注册
titleSuffix: Microsoft Intune
description: 了解如何使用 Intune 注册 Android Enterprise 公司拥有的工作配置文件设备。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 7/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: shthilla
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9a19a78002d0655cf63a8b757ea252fb8992603f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915256"
---
# <a name="set-up-intune-enrollment-of-android-enterprise-corporate-owned-devices-with-work-profile"></a>设置 Android Enterprise 公司拥有的工作配置文件设备的 Intune 注册

Android Enterprise 公司拥有的工作配置文件设备是供公司和个人使用的单用户设备。

最终用户可以将其工作和个人数据分开，确保其个人数据和应用程序将保持私有。 管理员可以控制整个设备的某些设置和功能，包括：

- 设置设备密码的要求
- 控制蓝牙和数据漫游
- 配置恢复出厂设置保护

Intune 可帮助将应用和设置部署到 Android Enterprise 公司拥有的工作配置文件设备。 有关 Android Enterprise 的特定详细信息，请参阅 [Android Enterprise 要求](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012)。

## <a name="device-requirements"></a>设备要求

设备必须满足以下要求才能作为 Android Enterprise 公司拥有的工作配置文件设备进行托管：

- Android OS 版本 8.0 及更高版本。
- 设备必须运行具有 Google Mobile Services (GMS) 连接性的 Android 发行版。 设备必须有可用的 GMS，并且必须能连接到 GMS。

## <a name="set-up-android-enterprise-corporate-owned-work-profile-device-management"></a>设置 Android Enterprise 公司拥有的工作配置文件设备管理

若要设置 Android Enterprise 公司拥有的工作配置文件设备，请执行以下步骤：

1. 若准备管理移动设备，必须[将移动设备管理 (MDM) 机构设置为“Microsoft Intune”](../fundamentals/mdm-authority-set.md)以获取说明。 第一次设置 Intune 以进行移动设备管理时，只需设置一次此项。
2. [将 Intune 租户帐户连接到托管的 Google Play 帐户](connect-intune-android-enterprise.md)。
3. [创建注册配置文件](#create-an-enrollment-profile)
4. [创建设备组](#create-a-device-group)。
5. [注册公司拥有的工作配置文件设备](#enroll-the-corporate-owned-work-profile-devices)。

### <a name="create-an-enrollment-profile"></a>创建注册配置文件

> [!NOTE]
> 公司拥有的工作配置文件设备的令牌不会自动过期。 如果管理员决定撤销令牌，则与其相关联的配置文件将不会显示在“设备” > “Android” > “Android 注册” > “公司拥有的工作配置文件设备(预览)”中   。 若要查看与活动令牌和非活动令牌关联的所有配置文件，请单击“筛选”，然后选中“活动”和“非活动”策略状态对应的框。 

必须创建一个注册配置文件，用户才能可以注册公司拥有的工作配置文件设备。 创建配置文件时，它会提供注册令牌（随机字符串）和 QR 码。 可使用令牌或 QR 码[注册专用设备](#enroll-the-corporate-owned-work-profile-devices)，具体取决于 Android OS 和设备版本。

1. 登录到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，选择“设备” > “Android” > “Android 注册” > “公司拥有的工作配置文件设备(预览)”   。
2. 选择“创建配置文件”并填写字段。
    - **名称**：键入在将配置文件分配给动态设备组时使用的名称。
    - **描述**：添加配置文件说明（可选）。
3. 选择“下一步”。
5. 在“查看 + 创建”页上，选择“创建”以创建策略 。

### <a name="create-a-device-group"></a>创建设备组

可将应用和策略定位到已分配或动态设备组。 可按照以下步骤配置动态 Azure AD 设备组，以自动填充使用特定注册配置文件进行注册的设备：

1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“组” > “所有组” > “新组”  。
2. 在“组”边栏选项卡中，填写必填字段，如下所示：
    - **组类型**：安全
    - **组名称**：键入直观名称（如“出厂 1 设备”）
    - **成员身份类型**：动态设备
3. 选择“添加动态查询”。
4. 在“动态成员身份规则”边栏选项卡中，填写如下字段：
    - **添加动态成员身份规则**：简单规则
    - **添加设备位置**enrollmentProfileName
    - 在中间的框中，选择“等于”。
    - 在最后一个字段中，输入之前创建的注册配置文件名称。
    有关动态成员身份规则的详细信息，请参阅 [AAD 中的组动态成员身份规则](/azure/active-directory/users-groups-roles/groups-dynamic-membership)。 
5. 选择“添加查询” > “创建” 。

### <a name="revoke-tokens"></a>撤消令牌

可以立即让令牌/QR 码到期。 从此时起，令牌/QR 码不再可用。 在以下情况下可使用此选项：
  - 意外地与未经授权的一方共享令牌/QR 码
  - 完成所有注册，不再需要令牌/QR 码

撤销令牌/QR 码不会对已注册的设备产生任何影响。

1. 登录到 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)，选择“设备” > “Android” > “Android 注册” > “公司拥有的工作配置文件设备(预览)”   。
2. 选择要使用的配置文件。
3. 选择“令牌”。
5. 若要撤销令牌，请选择“撤销令牌” > “是” 。

## <a name="enroll-the-corporate-owned-work-profile-devices"></a>注册公司拥有的工作配置文件设备

用户现在可以[注册其公司拥有的工作配置文件设备](android-dedicated-devices-fully-managed-enroll.md)。

> [!NOTE]
> 注册公司拥有的工作配置文件设备期间将自动安装 Microsoft Intune 应用。  此应用必须进行注册，不能卸载。 

## <a name="managing-apps-on-android-enterprise-corporate-owned-work-profile-devices"></a>在 Android Enterprise 公司拥有的工作配置文件设备上管理应用

Android Enterprise 公司拥有的工作配置文件设备上只能安装分配类型[设置为必需](../apps/apps-deploy.md#assign-an-app)的应用。 从托管的 Google Play 商店安装应用与从 Android Enterprise 工作配置文件设备安装应用的方式相同。

当应用开发人员向 Google Play 发布更新时，托管设备上的应用会自动更新。

若要从 Android Enterprise 公司拥有的工作配置文件设备中删除应用，可执行以下任一操作：
- 删除所需的应用部署。
- 创建应用的卸载部署。

## <a name="next-steps"></a>后续步骤
- [部署 Android 应用](../apps/apps-deploy.md)
- [添加 Android 配置策略](../configuration/device-profiles.md)