---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: 2ae953f6fb01f42c8140407c551ddeb3a9f39c70
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692667"
---
### <a name="server-connectivity-endpoints"></a>服务器连接终结点

服务连接点需要与以下终结点进行通信：

| 终结点  | 函数  |
|-----------|-----------|
| `https://aka.ms` | 用于查找服务 |
| `https://graph.windows.net` | 用于在将层次结构附加到桌面分析时自动检索 CommercialId 等设置（在 Configuration Manager 服务器角色上）。 有关详细信息，请参阅[配置站点系统服务器的代理](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server)。 |
| `https://*.manage.microsoft.com` | 用于使用桌面分析同步设备集合成员身份、部署计划和设备就绪状态（仅限在 Configuration Manager 服务器角色上）。 有关详细信息，请参阅[配置站点系统服务器的代理](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server)。 |
| `https://dc.services.visualstudio.com` | 用于从本地服务连接器获取诊断数据，以了解连接到云的服务的运行状况。<!--7541816--> |

### <a name="user-experience-and-diagnostic-component-endpoints"></a>用户体验和诊断组件终结点

客户端设备需要与以下终结点进行通信：

| 终结点  | 函数  |
|-----------|-----------|
| `https://v10c.events.data.microsoft.com` | 已连接的用户体验和诊断组件终结点。 由运行安装了 2018-09 累积更新或更高版本的 Windows 10 版本 1809 或更高版本或版本 1803 的设备使用。 |
| `https://v10.events.data.microsoft.com` | 已连接的用户体验和诊断组件终结点。 由运行未安装 2018-09 累积更新的 Windows 10 版本 1803 的设备使用。 |
| `https://v10.vortex-win.data.microsoft.com` | 已连接的用户体验和诊断组件终结点。 由运行 Windows 10 版本 1709 或更高版本的设备使用。 |
| `https://vortex-win.data.microsoft.com` | 已连接的用户体验和诊断组件终结点。 由运行 Windows 7 和 Windows 8.1 的设备使用 |

### <a name="client-connectivity-endpoints"></a>客户端连接终结点

客户端设备需要与以下终结点进行通信：

| 索引 | 终结点  | 函数  |
|-------|-----------|-----------|
| 1 | `https://settings-win.data.microsoft.com` | 启用兼容性更新以将数据发送到 Microsoft。 |
| 2 | `http://adl.windows.com` | 允许兼容性更新以从 Microsoft 接收最新的兼容性数据。 |
| 3 | `https://watson.telemetry.microsoft.com` | [Windows 错误报告 (WER)](/windows/win32/wer/windows-error-reporting)。 需要在 Windows 10 版本 1803 或更低版本中监视部署运行状况。 |
| 4 | `https://umwatsonc.events.data.microsoft.com` | [Windows 错误报告 (WER)](/windows/win32/wer/windows-error-reporting)。 Windows 10 版本 1809 或更高版本中的设备运行状况报告所必需的。 |
| 5 | `https://ceuswatcab01.blob.core.windows.net` | [Windows 错误报告 (WER)](/windows/win32/wer/windows-error-reporting)。 需要在 Windows 10 版本 1809 或更高版本中监视部署运行状况。 |
| 6 | `https://ceuswatcab02.blob.core.windows.net` | [Windows 错误报告 (WER)](/windows/win32/wer/windows-error-reporting)。 需要在 Windows 10 版本 1809 或更高版本中监视部署运行状况。 |
| 7 | `https://eaus2watcab01.blob.core.windows.net` | [Windows 错误报告 (WER)](/windows/win32/wer/windows-error-reporting)。 需要在 Windows 10 版本 1809 或更高版本中监视部署运行状况。 |
| 8 | `https://eaus2watcab02.blob.core.windows.net` | [Windows 错误报告 (WER)](/windows/win32/wer/windows-error-reporting)。 需要在 Windows 10 版本 1809 或更高版本中监视部署运行状况。 |
| 9 | `https://weus2watcab01.blob.core.windows.net` | [Windows 错误报告 (WER)](/windows/win32/wer/windows-error-reporting)。 需要在 Windows 10 版本 1809 或更高版本中监视部署运行状况。 |
| 10 | `https://weus2watcab02.blob.core.windows.net` | [Windows 错误报告 (WER)](/windows/win32/wer/windows-error-reporting)。 需要在 Windows 10 版本 1809 或更高版本中监视部署运行状况。 |
| 11 | `https://kmwatsonc.events.data.microsoft.com` | [联机崩溃分析 (OCA)](/windows/win32/dxtecharts/crash-dump-analysis)。 Windows 10 版本 1809 或更高版本中的设备运行状况报告所必需的。 |
| 12 | `https://oca.telemetry.microsoft.com`  | [联机崩溃分析 (OCA)](/windows/win32/dxtecharts/crash-dump-analysis)。 需要在 Windows 10 版本 1803 或更低版本中监视部署运行状况。 |
| 13 | `https://login.live.com` | 需要为桌面分析提供更可靠的设备标识。 <br> <br>若要禁用最终用户 Microsoft 帐户访问权限，请使用策略设置，而不是阻止此终结点。 有关详细信息，请参阅[企业中的 Microsoft 帐户](/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication)。 |
| 14 | `https://v20.events.data.microsoft.com` | 已连接的用户体验和诊断组件终结点。 |