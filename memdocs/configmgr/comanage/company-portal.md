---
title: 公司门户中的应用
titleSuffix: Configuration Manager
description: 为共同管理的设备使用公司门户应用提供一致的用户体验。
ms.date: 09/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: how-to
ms.assetid: 26456bb7-f46b-4d8d-bb0b-e3fd9a52fe14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cd49546e49d6964cfe37b0b13e1abe9175f4aa0e
ms.sourcegitcommit: 7b656712cc9340d18211c7754cb99bcaae91b0ca
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2020
ms.locfileid: "89432551"
---
# <a name="use-the-company-portal-app-on-co-managed-devices"></a>在共同管理的设备上使用公司门户应用

适用范围：  Configuration Manager (Current Branch)

<!--CMADO-3601237,INADO-4297660-->

从版本 2006 开始，公司门户现在是 Microsoft Endpoint Manager 的跨平台应用门户体验。 通过将共同管理的设备配置为同时使用公司门户，你可以在所有设备上提供一致的用户体验。

公司门户支持以下操作：

- 在共同管理的设备上启动公司门户应用，并通过 Azure Active Directory (Azure AD) 单一登录 (SSO) 登录。
- 在公司门户中查看可用和已安装的 Configuration Manager 应用及 Intune 应用。
- 从公司门户安装可用的 Configuration Manager 应用并接收安装状态信息。

:::image type="content" source="media/3601237-company-portal.png" alt-text="公司门户与来自 Configuration Manager 的应用" lightbox="media/3601237-company-portal.png":::

公司门户的行为取决于你的共同管理工作负载配置：

| 工作负荷 | 设置 | 行为 |
|----------|---------|----------|
| 客户端应用 | **Configuration Manager** | 只能看到 Configuration Manager 客户端应用 |
| 客户端应用 | 试点 Intune 或 Intune | 可以看到 Configuration Manager 和 Intune 客户端应用 |
| Office 即点即用应用 | **Configuration Manager** | 只能看到 Configuration Manager Office 即点即用应用 |
| Office 即点即用应用 | 试点 Intune 或 Intune | 只能看到 Intune Office 即点即用应用 |

有关详细信息，请参阅以下文章：

- [应用工作负载的关系图](workloads.md#diagram-for-app-workloads)

- [如何将 Configuration Manager 工作负载切换到 Intune](how-to-switch-workloads.md)

## <a name="prerequisites"></a>先决条件

- Configuration Manager Current Branch 版本 2006 或更高版本 <sup>（[请参阅“常见问题”](#bkmk_ver-prereq)）</sup>

- 公司门户应用版本 11.0.8980.0 或更高版本

- Windows 10 版本 1803 或更高版本：

  - 已注册[共同管理](how-to-enable.md)

  - 有权访问 [Intune 的 Internet 终结点](../../intune/fundamentals/intune-endpoints.md)

- 登录到这些设备的用户帐户需要以下配置：

  - Azure AD 标识

  - 已分配 Intune 许可证

## <a name="configure-and-deploy"></a>配置和部署

### <a name="configuration-manager-client-settings"></a>Configuration Manager 客户端设置

要确保用户仅接收来自公司门户的通知，请配置 Configuration Manager 客户端设置。 在设备设置的“软件中心”组中，将“选择用户门户”更改为“公司门户”。

有关客户端设置的详细信息，请参阅以下文章：

- [如何配置客户端设置](../core/clients/deploy/configure-client-settings.md)
- [关于客户端设置](../core/clients/deploy/about-client-settings.md#software-center)

### <a name="deploy-the-company-portal-app"></a>部署公司门户应用

- 用户可以从 [Microsoft Store](https://www.microsoft.com/p/company-portal/9wzdncrfj3pz?activetab=pivot:overviewtab) 手动安装公司门户应用。

- 如果需要在共同管理的设备上使用应用，则部署过程取决于[客户端应用](workloads.md#client-apps)共同管理工作负载的状态：

  - 如果客户端应用工作负载是使用 Configuration Manager，则[使用 Configuration Manager 创建和部署应用程序](../apps/get-started/create-and-deploy-an-application.md)。 从[适用于企业的 Microsoft Store](https://www.microsoft.com/business-store) 下载离线公司门户应用。

  - 如果客户端应用工作负载是使用 Intune，你可以通过 Configuration Manager 或[使用 Microsoft Intune 添加 Windows 10 公司门户应用](../../intune/apps/store-apps-company-portal-app.md)来部署它。

有关为组织的公司门户打造品牌的详细信息，请参阅[如何自定义 Intune 公司门户应用](../../intune/apps/company-portal-app.md)。

## <a name="use-the-company-portal"></a>使用公司门户

1. 从“开始”菜单启动公司门户。 当前登录的用户会根据其 Azure AD 标识自动登录到公司门户。

1. 选择“应用”页。 你应该会在列表中看到 Configuration Manager 应用。

1. 从 Configuration Manager 中选择一个已部署的应用。

    - “概述”选项卡将显示有关应用的详细信息，例如大小、版本和发布日期。

    - 若要确认 Configuration Manager 是此应用的管理服务，请切换到“其他信息”选项卡。

    - 要安装应用，请选择“安装”。 公司门户将显示安装状态，安装完成后会显示一条通知。

    - 如果应用已安装，请选择“卸载”以删除该应用。

    - 选择省略号 (`...`) 可以执行更多操作（如“修复”和“共享”）。

        :::image type="content" source="media/3601237-company-portal-app-details.png" alt-text="公司门户中的 Configuration Manager 应用详细信息" lightbox="media/3601237-company-portal-app-details.png":::

    - 安装 Configuration Manager Web 应用后，选择省略号菜单，然后选择“在浏览器中打开”，以启动 Web 应用。

    - 如果 Configuration Manager 应用程序无法安装并出现已知错误代码，请选择失败状态链接以搜索错误代码。

如果更改公司门户的客户端设置，那么，当用户选择 Configuration Manager 通知时，它将启动公司门户。 如果通知的场景是公司门户不支持的，则选择通知会启动软件中心。

若要帮助排查 Configuration Manager 应用的安装问题，请转到公司门户中的“帮助和支持”部分。 当你使用“获取帮助”选项时，可以在发送的请求中附上 Configuration Manager 日志文件。

## <a name="frequently-asked-questions-faq"></a>常见问题 (FAQ)

### <a name="im-using-configuration-manager-version-2002-why-is-the-new-company-portal-showing-configuration-manager-apps"></a><a name="bkmk_ver-prereq"></a> 我使用的是 Configuration Manager 版本 2002，为什么新公司门户会显示 Configuration Manager 应用？

公司门户版本 11.0.8980.0 或更高版本将为使用该应用程序的所有共同托管客户端显示 Configuration Manager 部署的应用程序。 Configuration Manager 版本 2006 是先决条件，因为它可添加此客户端设置来控制通知。 如果将公司门户安装在早期版本的共同托管设备上，或未配置此客户端设置，用户将看到来自这两个门户的通知。 这种体验可能会让用户感到困惑。

### <a name="does-company-portal-support-applications-deployed-as-software-updates-from-configuration-manager"></a>公司门户是否支持从 Configuration Manager 部署为软件更新的应用程序？

是的。 如果使用软件更新功能部署应用，则无论用户体验是公司门户还是软件中心，客户端的处理方式都是一样的。

### <a name="can-users-repair-uninstall-and-update-configuration-manager-apps-in-company-portal"></a>用户能否在公司门户中修复、卸载和更新 Configuration Manager 应用？

是的。 如果将 Configuration Manager 应用配置为支持这些额外的操作，则公司门户支持修复、卸载和更新。

## <a name="known-issues"></a>已知问题

软件中心的以下功能在公司门户中暂不可用：

- 某些应用信息，例如，需要重新启动或预计安装时间

- [应用组](../apps/deploy-use/create-app-groups.md)

其他已知问题：

- 如果同时从 Configuration Manager 和 Intune 部署同一应用，该应用会在公司门户中出现两次。

- 当你搜索公司门户时，Intune 应用始终显示在 Configuration Manager 应用之前。

## <a name="next-steps"></a>后续步骤

[如何将 Configuration Manager 工作负载切换到 Intune](how-to-switch-workloads.md)

[如何自定义 Intune 公司门户应用](../../intune/apps/company-portal-app.md)
