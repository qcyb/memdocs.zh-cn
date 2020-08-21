---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/13/2019
ms.openlocfilehash: 0f91860ad591e20c6f199e098a8c957f50294386
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88704344"
---
<!-- ## Update and configure the .NET Framework to support TLS 1.2 Note: the heading in in the 2 articles (enable-tls-1-2-client & enable-tls-1-2-server) to better facilitate linking. -->

### <a name="determine-net-version"></a>确定 .NET 版本

首先，确定已安装的 .NET 版本。 有关详细信息，请参阅[如何确定安装了 Microsoft .NET Framework 的哪些版本以及服务包级别](https://support.microsoft.com/help/318785/how-to-determine-which-versions-and-service-pack-levels-of-the-microso)。

### <a name="install-net-updates"></a>安装 .NET 更新

安装 .NET 更新以便启用强加密。 某些 .NET Framework 版本可能需要更新来启用强加密。 使用以下准则：

- NET Framework 4.6.2 及更高版本支持 TLS 1.1 和 TLS 1.2。 确认注册表设置，但无需额外更改。

- 更新 NET Framework 4.6 和更低版本以支持 TLS 1.1 和 TLS 1.2。 有关详细信息，请参阅 [.NET Framework 版本和依赖关系](/dotnet/framework/migration-guide/versions-and-dependencies)。

- 如果在 Windows 8.1 或 Windows Server 2012 上使用 .NET Framework 4.5.1 或 4.5.2，也可从[下载中心](https://www.microsoft.com/download/details.aspx?id=42883)获取相关更新和详细信息。


### <a name="configure-for-strong-cryptography"></a>配置强加密

将 .NET Framework 配置为支持强加密。 将 `SchUseStrongCrypto` 注册表设置设置为 `DWORD:00000001`。 此值将禁用 RC4 流密码，并需要重新启动。 若要了解有关此设置的详细信息，请参阅 [Microsoft 安全公告 296038](/security-updates/SecurityAdvisories/2015/2960358)。

请务必在跨网络与启用了 TLS 1.2 的系统通信的所有计算机上设置以下注册表项。 例如 Configuration Manager 客户端、未在站点服务器安装的远程站点系统角色，以及站点服务器本身。

对于在 32 位 OS 上运行的 32 位应用程序和在 64 位 OS 上运行的 64 位应用程序，请更新以下子项值：

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

对于在 64 位 OS 上运行的 32 位应用程序，请更新以下子项值：

``` Registry
[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v2.0.50727]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
[HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319]
      "SystemDefaultTlsVersions" = dword:00000001
      "SchUseStrongCrypto" = dword:00000001
```

> [!Note]  
> `SchUseStrongCrypto` 设置允许 .NET 使用 TLS 1.1 和 TLS 1.2。 `SystemDefaultTlsVersions` 设置允许 .NET 使用操作系统配置。 有关详细信息，请参阅 [.NET Framework 中的传输层安全性 (TLS) 最佳做法](/dotnet/framework/network-programming/tls)。