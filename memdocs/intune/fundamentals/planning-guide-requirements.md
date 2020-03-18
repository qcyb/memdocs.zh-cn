---
title: 确定用例场景要求
titleSuffix: Microsoft Intune
description: 本文旨在帮助你确定 Microsoft Intune 仅云实现的 Intune 用例以及子用例场景要求。
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: fd8cb5f7-19f0-4d80-8825-2bafa49624af
ms.reviewer: jeffbu, cgerth
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6e002b62fb00c4e2e8523848c4c64ad7a54ce024
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79357644"
---
# <a name="determine-use-case-scenario-requirements"></a>确定用例场景要求

在此部分，你将确定对每个用例场景内每个组织组的要求。 此过程有助于为其他 Intune 部署规划领域做准备，例如体系结构和设计、载入和推出。 还有助于确定与 Intune 部署项目相关的潜在缺陷和难题。

对于每个用例和子用例场景，以及其关联的组织组和移动设备平台，可能有几套不同的要求。 例如，你公司的用例场景要求可能需要设备以更严格的一套设备设置注册到 Intune 中，例如 6 个字符的 PIN 码或禁用云备份。 你的“自带办公设备”(BYOD) 用例场景，可能不那么严格，允许使用 4 个字符的 PIN 码和云备份。

你可能还会有用于公司用例场景的组织组，这些组也有几套不同的要求（例如 PIN 设置、Wi-Fi 或 VPN 配置文件、已部署的应用）。 要求还可以根据移动设备平台的功能（如指纹读取器、电子邮件配置文件）来确定。

下面是一个组织用例场景要求的几个示例，显示了针对每个用例和子用例场景、组织组以及移动设备平台的几套不同的要求。 此外，还可使用下表输入组织的用例要求：

| **用例** | **子用例** | **组** | **设备平台** | **惠?** |
|:---:|:---:|:---:|:---:|:---:|
| 企业 | 信息工作者 | 人力资源、财务 | iOS/iPadOS | 安全电子邮件、设备设置、配置文件、应用 |                                                          
| 企业 | 高级管理人员 | 人力资源、财务 | iOS/iPadOS | 安全电子邮件、设备设置、配置文件、应用 |                                                         
| 企业 | Kiosk | 零售 | Android | 设备设置、配置文件、应用 |
| BYOD | 信息工作者 | 营销、销售 | iOS/iPadOS | 安全电子邮件、设备设置、配置文件、应用 |                                                         
| BYOD | 高级管理人员 | 营销、销售 | iOS/iPadOS | 安全电子邮件、设备设置、配置文件、应用 |

你可以[下载上表的模板](https://gallery.technet.microsoft.com/Intune-deployment-planning-fae156c2?redir=0)来输入组织的用例和子用例要求。


## <a name="examples-of-requirements"></a>要求示例

下面是可在“要求”列使用的几个其他示例：

- **安全电子邮件**
  - Exchange Online/本地条件访问
  - Outlook 应用保护策略

- **设备设置**
  - 具有 4 个、6 个字符的 PIN 设置
  - 限制云备份

- **配置文件**
  - Wi-Fi
  - VPN
  - 电子邮件（Windows 10 移动版）

- **应用**
  - 具有应用保护策略的 Office 365
  - 具有应用保护策略的业务线 (LOB)

## <a name="next-steps"></a>后续步骤

下一节提供[如何开发 Intune 推出计划](planning-guide-rollout-plan.md)的相关指南。
