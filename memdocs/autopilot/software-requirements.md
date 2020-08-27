---
title: Windows Autopilot 软件要求
ms.reviewer: ''
manager: laurawi
description: 自行通知 Windows Autopilot 部署的软件要求。
keywords: mdm，安装程序，windows，windows 10，oobe，管理，部署，Autopilot，ztd，0-touch，合作伙伴，msfb，intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.custom:
- CI 116757
- CSSTroubleshooting
ms.openlocfilehash: 2eb4f23fbe6126c095f049f36b08adac15c1e02c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907935"
---
# <a name="windows-autopilot-software-requirements"></a>Windows Autopilot 软件要求

**适用于： Windows 10**

Windows Autopilot 取决于 Windows 10、Azure Active Directory 和 MDM 服务中提供的特定功能，如 Microsoft Intune。 若要使用 Windows Autopilot 并访问这些功能，必须满足一些软件要求。

**注意**：有关当前支持 windows Autopilot 的 oem 列表，请参阅 [windows Autopilot](https://aka.ms/windowsAutopilot)上的 "参与者设备制造商" 部分。

## <a name="software-requirements"></a>软件要求

- 需要 Windows 10 半年频道的 [受支持版本](/windows/release-information/) 。 还支持 Windows 10 企业版2019长期服务通道 (LTSC) 。
- 支持以下版本：
  - Windows 10 专业版
  - Windows 10 专业教育版
  - Windows 10 专业工作站版
  - Windows 10 企业版
  - Windows 10 教育版
  - Windows 10 企业版 2019 LTSC

>[!NOTE]
>部署 Windows Autopilot 的过程可能是指特定的产品和版本。 此内容中包含这些产品并不表示扩展支持超出其支持生命周期的版本。 Windows Autopilot 不支持超出其支持生命周期的产品。 有关详细信息，请参阅 [Microsoft 生命周期策略](https://go.microsoft.com/fwlink/p/?LinkId=208270)。

## <a name="next-steps"></a>后续步骤

[Windows Autopilot 网络连接要求](networking-requirements.md)