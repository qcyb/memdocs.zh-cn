---
title: Microsoft Intune 中的 Win32 应用管理
titleSuffix: ''
description: 了解如何通过 Microsoft Intune 管理 Win32 应用。 本主题概述了 Intune Win32 应用交付和管理功能。
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: efdc196b-38f3-4678-ae16-cdec4303f8d2
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: contperfq1
ms.collection: M365-identity-device-management
ms.openlocfilehash: db28653207d7bf4341d614aeecb769dcc145caaa
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083924"
---
# <a name="win32-app-management-in-microsoft-intune"></a>Microsoft Intune 中的 Win32 应用管理

Microsoft Intune 提供 Win32 应用管理功能。 虽然连接到云的客户可以使用 Microsoft Endpoint Configuration Manager 管理 Win32 应用，但只使用 Intune 的客户将拥有更强大的 Win32 业务线 (LOB) 应用管理功能。 本主题概述了 Intune Win32 应用管理功能和相关信息。

> [!NOTE]
> 此应用管理功能支持适用于 Windows 应用程序的 32 位和 64 位操作系统体系结构。

> [!IMPORTANT]
> 部署 Win32 应用时，建议专门使用 [Intune 管理扩展](../apps/intune-management-extension.md)方法，特别是在有多文件 Win32 应用安装程序时。 如果在 AutoPilot 注册期间混合安装 Win32 应用和业务线应用，则应用安装可能会失败。 如果 PowerShell 脚本或 Win32 应用分配给用户或设备，Intune 管理扩展就会自动安装。

## <a name="prerequisites"></a>必备条件

要使用 Win32 应用管理，请确保满足以下条件：

- 使用 Windows 10 版本 1607 或更高版本（企业版、专业版和教育版）。
- 设备必须加入 Azure Active Directory (Azure AD) 并进行自动注册。 Intune 管理扩展支持已加入 Azure AD、已加入混合域和已注册组策略的设备。 
  > [!NOTE]
  > 对于组策略注册的情况，用户使用本地用户帐户将 Windows 10 设备加入 Azure AD。 用户必须使用其 Azure AD 用户帐户登录设备并注册 Intune。 如果 PowerShell 脚本或 Win32 应用以用户或设备为目标，Intune 将在设备上安装 Intune 管理扩展。
- Windows 应用程序大小的上限为每个应用 8 GB。

## <a name="prepare-the-win32-app-content-for-upload"></a>准备 Win32 应用内容以进行上传

在可以将 Win32 应用添加到 Microsoft Intune 之前，必须使用 Microsoft Win32 内容准备工具来准备应用。 可以使用 Microsoft Win32 内容准备工具预处理 Windows 经典 (Win32) 应用。 该工具将应用程序安装文件转换为 .intunewin 格式。 有关详细信息和步骤，请参阅[准备 Win32 应用内容以进行上传](apps-win32-prepare.md)。 

## <a name="add-assign-and-monitor-a-win32-app"></a>添加、分配和监视 Win32 应用

使用 Microsoft Win32 内容准备工具[准备好要上传到 Intune 的 Win32 应用](apps-win32-prepare.md)后，可以将应用添加到 Intune。 有关详细信息和步骤，请参阅[在 Microsoft Intune 中添加、分配和监视 Win32 应用](apps-win32-add.md)。

## <a name="delivery-optimization"></a>传递优化

Windows 10 1709 及更高版本的客户端将在 Windows 10 客户端上使用传递优化组件下载 Intune Win32 应用内容。 传递优化提供对等功能，此功能默认启用。 

你可以配置传递优化代理，使其基于分配在后台或前台模式下下载 Win32 应用内容。 传递优化可通过组策略和 Intune 设备配置进行配置。 有关详细信息，请参阅[适用于 Windows 10 的传递优化](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization)。 

> [!NOTE]
> 此外，也可以在 Configuration Manager 分发点上安装 Microsoft Connected Cache 服务器，用于缓存 Intune Win32 应用内容。 有关详细信息，请参阅 [Configuration Manager 中的 Microsoft Connected Cache](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune)。

## <a name="install-required-and-available-apps-on-devices"></a>在设备上安装必需和可用应用

用户将看到必需和可用应用安装的 Windows 通知。 下图显示了一个示例通知，提示应用安装直到设备重启后才能完成。 

![应用安装的 Windows 通知的屏幕截图。](./media/apps-win32-app-management/apps-win32-app-08.png)    

下图中，系统通知用户，正在对设备进行应用更改。

![通知用户正在进行应用更改的屏幕截图。](./media/apps-win32-app-management/apps-win32-app-09.png)    

此外，“公司门户”应用会向用户显示更多应用安装状态消息。 以下条件适用于 Win32 依赖项功能：
- 应用安装失败。 不符合管理员定义的依赖项。
- 应用已成功安装，但需要重启。
- 应用正在安装，但需要重启才能继续安装。

## <a name="set-win32-app-availability-and-notifications"></a>设置 Win32 应用可用性和通知
可以为 Win32 应用配置开始时间和截止时间。 在开始时间，Intune 管理扩展将启动应用内容下载并缓存它以用于所需的意图。 应用将在截止时间安装。 

对于可用应用，开始时间将指示应用在公司门户中的可见时间，并且在用户从公司门户请求应用时将下载内容。 你还可以启用重启宽限期。 

> [!IMPORTANT]
> 只有在“程序”部分的“设备重启行为”设为以下任一选项时，“分配”部分中的“重启宽限期”设置才可用：
> - **根据返回代码确定行为**
> - **Intune 将强制重启设备**

使用以下步骤，根据必需应用的日期和时间设置应用可用性：

1. 登录到 [Microsoft 终结点管理器管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)。
2. 选择“应用” > “所有应用”。
3. 在“Windows 应用(Win32)”列表中，选择一个应用。 
4. 在“应用”窗格中，选择“分配”部分旁边的“属性” > “编辑”。 然后，在“必需”分配类型下，选择“添加组”。 
   
   请注意，可以根据分配类型设置应用可用性。 “分配类型”可以是“必需”、“适用于已注册的设备”或“卸载”。
5. 在“选择组”窗格上选择一个组，以指定将向其分配应用的用户组。 

    > [!NOTE]
    > “分配类型”选项包括：<br>
    > - **必需**：可以选择“使此应用对所有用户都是必需的”和/或“使此应用在所有设备上都是必需的”。<br>
    > - **适用于已注册的设备**：可以选择“使此应用对拥有已注册设备的所有用户可用”。<br>
    > - **卸载**：可以选择“为所有用户卸载此应用”和/或“为所有设备卸载此应用”。

6. 若要修改“最终用户通知”选项，请选择“显示所有 toast 通知”。
7. 在“编辑分配”窗格中，将“最终用户通知”设置为“显示所有 toast 通知”。 请注意，可以将“最终用户通知”设置为“显示所有 Toast 通知”、“显示计算机重启的 Toast 通知”或“隐藏所有 Toast 通知”   。
8. 将“应用可用性”设置为“特定日期和时间”，并选择日期和时间。 此日期和时间指定应用下载到用户设备的时间。 
9. 将“应用安装截止时间”设置为“特定日期和时间”，并选择日期和时间。 此日期和时间指定应用安装到用户设备的时间。 如果为同一用户或设备进行了多个分配，将根据最早的时间选择应用安装截止时间。

10. 选择“重启宽限期”旁边的“启用”。 设备上的应用安装完成后，重启宽限期就会开始。 禁用此设置后，设备可以重启而不会出现警告。 

    可以自定义以下选项：
    
    - **设备重启宽限期(分钟)** ：默认值为 1440 分钟（24 小时）。 此值最多可为 2 周。
    - **选择在重启前多久显示重启倒计时对话框(分钟)** ：默认值为 15 分钟。
    - **允许用户推迟重新启动通知**：可以选择“是”或“否” 。
        - **选择推迟时间(分钟)** ：默认值为 240 分钟（4 小时）。 推迟值不能超过重启宽限期。

11. 选择“查看 + 保存”。

## <a name="notifications-for-win32-apps"></a>Win32 应用的通知 
如需要，可以隐藏每个应用分配的用户通知。 在 Intune 中，依次选择“应用” > “所有应用” > “应用” > “分配” > “包括组”。 

> [!NOTE]
> 在未注册设备上不会卸载通过 Intune 管理扩展安装的 Win32 应用。 管理员可使用分配排除避免向自带设备 (BYOD) 设备提供 Win32 应用。

## <a name="next-steps"></a>后续步骤

- 有关向 Intune 添加应用的详细信息，请参阅[向 Microsoft Intune 添加应用](apps-add.md)。
