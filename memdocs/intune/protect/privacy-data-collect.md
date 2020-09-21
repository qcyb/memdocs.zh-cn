---
title: Intune 中的数据收集
titleSuffix: Microsoft Intune
description: 了解 Intune 中收集个人数据的方式。
keywords: 隐私, 个人数据
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/01/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: d1171740-936d-46a5-af37-f418bd6fa63e
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: bcd7ff1ae51314bc57be2bed39c7fe8ca7114d82
ms.sourcegitcommit: e2deac196e5e79a183aaf8327b606055efcecc82
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076101"
---
# <a name="data-collection-in-intune"></a>Intune 中的数据收集

当用户使用 Intune 注册公司或个人设备时，Intune 会收集、处理和共享一些个人数据以支持业务运营、与客户开展业务并为服务提供支持。 Intune 从以下来源收集个人数据：

- 管理员在 Microsoft Endpoint Manager 管理中心对 Intune 的使用。
- 最终用户设备（注册设备以进行 Intune 管理时以及使用过程中）。
- 第三方服务中的客户帐户（按每个管理员的说明）。
- 诊断、性能和使用情况信息。

Intune 从这些来源中收集到的信息可以分为以下两类：[必需](#required-data)、[可选](#optional-data)。 在每个类别中，数据进一步分为客户数据、个人数据、诊断数据和服务生成的数据。 

> [!NOTE]
> 我们不会出于任何原因向任何第三方出售我们服务收集的任何数据。

## <a name="required-data"></a>所需数据

“必需”类别中的数据包含使我们的服务匹配客户预期的必要数据。 Intune 收集的大多数数据都是必需的数据。 此数据绑定至某个用户、设备或应用程序，对管理的性质来说至关重要。 收集的数据包含个人数据和非个人数据。 个人数据包括个人身份数据（可以直接识别最终用户），或具有系统生成的唯一标识符的匿名化数据（用于向用户提供企业服务）、支持数据和帐户数据。 非个人数据包括服务生成的系统元数据和组织/租户信息。 Intune 还收集访问控制数据，用于通过类似于[基于角色的访问控制](../fundamentals/role-based-access-control.md)的功能对管理角色和职能的访问权限进行管理。

Intune 收集的必需数据可能包括但不限于以下内容： 

- 用户信息
  - 显示的所有者名称/用户（由 AzureUserID 标识的注册了 Azure 的用户名）
  - 用户主体名称或电子邮件地址
  - 电话号码
  - 第三方用户标识（例如 AppleID）
- 硬件清单信息
  - 设备名称
  - 制造商
  - 操作系统
  - 序列号
  - IMEI 编号
  - IP 地址
  - Wi-Fi MacAddress
  - ICCID
- 审核日志信息，包括以下活动的相关数据
  - 管理
  - 创建
  - 更新（编辑）
  - 删除
  - 分配
  - 远程任务
- 支持信息
  - 联系信息（姓名、电话号码和电子邮件地址）
  - 与 Microsoft 支持部门、产品和/或客户体验团队成员之间的电子邮件讨论
- 访问控制信息 
  - 静态验证器（客户密码）
  - 证书的隐私密钥 
- 管理员和帐户信息
  - 管理员用户的名字和姓氏
  - 管理员用户名
  - UPN（电子邮件）
  - 电话号码
  - 帐户所有者的电子邮件地址
  - 每个客户的 IT 管理员的 Active Directory ID
  - 客户帐单的付款数据
  - 订阅密钥
- 应用程序清单，例如
  - 应用名称
  - 版本
  - 应用 ID
  - 大小
  - 安装位置
  - 只有在由管理员标记为公司所有的设备或者开启了符合的应用功能时，才会收集应用程序清单数据。  
- 客户第三方租户 ID（例如 Apple ID）
- 设备数据
  - Intune 设备 ID
  - Azure Active Directory 设备 ID
  - Intune 设备管理 ID
  - 租户 ID
  - 帐户 ID
  - EAS 设备 ID
  - 特定于平台的 ID
  - iOS/iPadOS 设备的 AppleID
  - Mac 设备的 Mac 地址
  - Windows 设备的 Windows ID
- 托管应用程序信息
  - 托管应用程序 ID
  - 托管应用程序设备标记
  - Intune 设备管理 ID
  - Azure Active Directory 设备 ID
  - 加密密钥
- 所有 Intune 租户中的管理员使用情况数据（例如，在与管理控制台进行交互时所选择的管理控件）
- 租户帐户信息（可从 Intune 边栏选项卡获得此数据）
  - 已注册的设备数或用户数
  - 已标识的设备平台数  
  - 已安装的设备数
  - installedDeviceCount：已安装该应用程序的设备数。
  - notApplicableDeviceCount：无法使用该应用程序的设备数。
  - notInstalledDeviceCount：可使用该应用程序但是尚未安装的设备数。
  - pendingInstallDeviceCount：可使用该应用程序但还在等待安装的设备数。

## <a name="optional-data"></a>可选数据

“可选”类别中的数据不是产品或服务体验所必需的。 客户可以控制可选数据的收集。 Intune 使客户能够选择加入或选择退出可选的数据收集。 可选数据的示例包括 Intune 为诊断和遥测收集的数据。 请注意，我们认为共享可选数据有令人信服的理由，因为它为更丰富的新体验创造了机会，但我们理解，为用户提供自行选择的机会是非常重要的。 

可选诊断数据的示例可包括应用程序使用情况数据、错误和性能数据。 Microsoft 在使用任何 Microsoft 365 企业应用版应用程序和服务期间收集的所有诊断数据均按照 ISO/IEC 19944:2017（第 8.3.3 节）标准中的定义进行了匿名处理。

## <a name="certain-end-user-data-or-content-is-never-collected"></a>从不收集某些最终用户数据或内容

Intune 不会收集、也不允许管理员查看最终用户的通话或 Web 浏览历史记录、个人电子邮件、短信、联系人、个人帐户的密码、日历事件或照片（包括“照片”应用或照相机中的照片）。 请参阅[注册设备入门](../enrollment/device-enrollment.md)。

有关数据类型和定义的详细信息，请参阅 [Microsoft 如何对联机服务的数据进行分类](https://www.microsoft.com/trust-center/privacy/customer-data-definitions)。 

## <a name="next-steps"></a>后续步骤

详细了解 Intune [存储和处理](privacy-data-store-process.md)以及[共享](privacy-data-secure-share.md)个人数据的方式。 
