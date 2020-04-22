---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: 08cebf6ef844e1854daa9444462f4c4470319186
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704075"
---
<!--## Enable Transport layer security (TLS) 1.2 protocol as a security provider Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

默认情况下启用 TLS 1.2。 因此，不需要更改这些项即可启用它。 在遵循本文中的其他指南并验证环境在仅启用 TLS 1.2 也可用后，可以在 `Protocols` 下进行更改以禁用 TLS 1.0 和 TLS 1.1。

验证 `\SecurityProviders\SCHANNEL\Protocols` 注册表子项设置，如 [.NET Framework 中的传输层安全性 (TLS) 最佳做法](https://docs.microsoft.com/dotnet/framework/network-programming/tls#configuring-security-via-the-windows-registry)所示。

