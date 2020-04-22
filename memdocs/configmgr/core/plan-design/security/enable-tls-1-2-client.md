---
title: 如何在客户端上启用传输层安全性 (TLS) 1.2
titleSuffix: Configuration Manager
description: 有关如何为 Configuration Manager 客户端启用 TLS 1.2 的信息。
ms.date: 12/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5b094a02-a425-4b67-81d3-8455e4265512
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e5b525da4a58240b34c30403db618ea0d2ca85f1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704105"
---
# <a name="how-to-enable-tls-12-on-clients"></a>如何在客户端上启用 TLS 1.2

适用范围：  Configuration Manager (Current Branch)

为 Configuration Manager 环境启用 TLS 1.2 时，请先确保客户端能够正确配置为使用 TLS 1.2，然后再在站点服务器和远程站点系统上启用 TLS 1.2 并禁用旧协议。 在客户端上启用 TLS 1.2 分为三个任务：

- 更新 Windows 和 WinHTTP
- 确保在操作系统级别启用 TLS 1.2 作为 SChannel 协议
- 更新并配置 .NET Framework 以支持 TLS 1.2

有关特定 Configuration Manager 功能和场景依赖项的详细信息，请参阅[关于启用 TLS 1.2](enable-tls-1-2.md)。

## <a name="update-windows-and-winhttp"></a><a name="bkmk_winhttp"></a> 更新 Windows 和 WinHTTP

Windows 8.1、Windows Server 2012 R2、Windows 10、Windows Server 2016 及 Windows 更高版本以本机方式支持通过 WinHTTP 进行客户端服务器通信的 TLS 1.2。 

Windows 早期版本（如 Windows 7 或 Windows Server 2012）默认不为使用 WinHTTP 的安全通信启用 TLS 1.1 或 1.2。 对于这些早期版本的 Windows，请安装[更新 3140245](https://support.microsoft.com/help/3140245) 以启用以下注册表值。可对其进行设置，将 TLS 1.1 和 TLS 1.2 添加到 WinHTTP 的默认安全协议列表。 安装修补程序后，创建以下注册表值：

> [!IMPORTANT]
> 在运行 Windows 早期版本的所有客户端上启用这些设置，然后再  在 Configuration Manager 服务器上启用 TLS 1.2 并禁用较旧的协议。 否则，可能会在无意中孤立它们。

验证 `DefaultSecureProtocols` 注册表设置的值，例如：

``` Registry
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Internet Settings\WinHttp\
      DefaultSecureProtocols = (DWORD): 0xAA0
```

若更改了此值，请重启计算机。

上面的示例显示了 WinHTTP `DefaultSecureProtocols` 设置的 `0xAA0` 的值。 [KB 3140245：更新以启用 TLS 1.1 和 TLS 1.2 并将其作为 Windows WinHTTP 的默认安全协议](https://support.microsoft.com/help/3140245)列出了各个协议的十六进制值。 默认情况下，Windows 中的此值是为 WinHTTP 启用 SSL 3.0 和 TLS 1.0 的 `0x0A0`。 上面的示例保留了这些默认值，并且还为 WinHTTP 启用了 TLS 1.1 和 TLS 1.2。 此配置将确保更改不会中断可能仍然依赖 SSL 3.0 或 TLS 1.0 的任何其他应用程序。 可以使用 `0xA00` 的值来仅启用 TLS 1.1 和 TLS 1.2。 Configuration Manager 支持 Windows 与两个设备协商的最安全的协议。

 若要完全禁用 SSL 3.0 和 TLS 1.0，请使用 Windows 中的 SChannel 禁用协议设置。 有关详细信息，请参阅[如何限制 Schannel.dll 中某些加密算法和协议的使用](https://support.microsoft.com/help/245030/how-to-restrict-the-use-of-certain-cryptographic-algorithms-and-protoc)。

## <a name="ensure-that-tls-12-is-enabled-as-a-protocol-for-schannel-at-the-operating-system-level"></a><a name="bkmk_protocol"></a> 确保在操作系统级别启用 TLS 1.2 作为 SChannel 协议

[!INCLUDE [Enable TLS 1.2 protocol as a security provider](includes/enable-tls-1-2-protocol-security-provider.md)]

## <a name="update-and-configure-the-net-framework-to-support-tls-12"></a><a name="bkmk_net"></a> 更新并配置 .NET Framework 以支持 TLS 1.2

[!INCLUDE [Update and configure the .NET framework to support TLS 1.2](includes/update-net-framework-to-support-tls-1-2.md)]


## <a name="next-steps"></a>后续步骤

- [在站点服务器和远程站点系统上启用 TLS 1.2](enable-tls-1-2-server.md)
- [启用 TLS 1.2 时的常见问题](enable-tls-1-2-troubleshoot.md)

