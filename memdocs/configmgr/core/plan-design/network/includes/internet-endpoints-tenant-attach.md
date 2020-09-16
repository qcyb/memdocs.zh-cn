---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 27436e7cd782ca910049007d52f37e2d7945f01e
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90606726"
---
- `https://aka.ms/configmgrgateway`

- `https://*.manage.microsoft.com` <!--7424742-->

- `https://dc.services.visualstudio.com` <!--7541816-->

服务连接点与 `https://*.manage.microsoft.com` 上承载的通知服务建立了长时间的传出连接。 验证用于服务连接点的代理未过快进行超时传出连接。 对于到此 Internet 终结点的传出连接，我们建议为 3 分钟。 <!--7820969-->