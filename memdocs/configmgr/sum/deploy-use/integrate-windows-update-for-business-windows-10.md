---
title: 集成适用于企业的 Windows 更新
titleSuffix: Configuration Manager
description: 对于连接到 Windows 更新服务的设备，可使用适用于企业的 Windows 更新 (WUfB) 保持 Windows 10 为最新。
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/07/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.openlocfilehash: 8ea95a04977038514c00f0199df42c8070e813c3
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127648"
---
# <a name="integrate-with-windows-update-for-business"></a>集成适用于企业的 Windows 更新

适用范围：  Configuration Manager (Current Branch)

当基于 Windows 10 的设备直接连接到 Windows 更新 (WU) 服务时，适用于企业的 Windows 更新 (WUfB) 能够让组织中的这些设备始终具有最新的安全防御和 Windows 功能。 Configuration Manager 能够区分使用 WUfB 和 WSUS 来获取软件更新的 Windows 10 计算机。  

> [!WARNING]
> 如果设备使用共同管理，并且你已将 [Windows 更新策略](../../comanage/workloads.md#windows-update-policies)移动到 Intune，设备将获得 [Intune 中适用于企业的 Windows 更新策略](https://docs.microsoft.com/intune/windows-update-for-business-configure)。
> - 如果 Configuration Manager 客户端仍安装在共同管理的设备上，则累积更新和功能更新的设置由 Intune 管理。 但是，如果已在[客户端设置](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates)  中启用第三方修补，则该修补仍由 Configuration Manager 管理。  

 当 Configuration Manager 客户端配置为从 WU 接收更新后（其中包括 WUfB 或 Windows 预览体验成员），一些 Configuration Manager 功能将不再可用：  

- Windows Update 符合性报告:  
  - Configuration Manager 将不会察觉发布到 WU 的更新。 配置为从 WU 接收更新的 Configuration Manager 客户端将会在 Configuration Manager 控制台中将这些更新显示为“未知”  。  

  - 对总体符合性状态进行故障排除非常困难，因为“未知”  状态只适用于尚未报告从 WSUS 返回的扫描状态的客户端。 现在，它还包括从 WU 接收更新的 Configuration Manager 客户端。  

  - 定义更新符合性是整体更新符合性报告的一部分，也无法按预期方式工作。

- 基于更新符合性状态的 Defender 的总体 Endpoint Protection 报告不会返回准确的结果，因为缺少扫描数据。  

- Configuration Manager 无法将 Microsoft 更新（如 Microsoft 365 Apps、IE 和 Visual Studio）部署到已连接到 WUfB 来接收更新的客户端。  

- Configuration Manager 仍可将发布到 WSUS 并通过 Configuration Manager 管理的第三方更新部署到连接 WUfB 以接收更新的客户端。 如果不需要在连接到 WUfB 的客户端上安装任何第三方更新，则禁用名为[在客户端上启用软件更新](../../core/clients/deploy/about-client-settings.md#software-updates)的客户端设置。

- 使用软件更新基础结构的 Configuration Manager 完整客户端部署将不能用于连接 WUfB 以接收更新的客户端。  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>标识使用 WUfB for Windows 10 更新的客户端

使用以下过程来标识使用 WUfB 获取 Windows 10 更新和升级的客户端。 然后将这些客户端配置为停止使用 WSUS 来获取更新，并部署客户端代理设置来禁用这些客户端的软件更新工作流。  

### <a name="prerequisites-for-wufb"></a>WUfB 的先决条件

- 运行 Windows 10 桌面专业版或 Windows 10 企业版的版本 1511 或更高版本的客户端

- 部署了[Windows Update for Business](https://docs.microsoft.com/windows/deployment/update/waas-manage-updates-wufb) ，并且客户端使用 WUfB 来获取 Windows 10 更新和升级。  

### <a name="to-identify-clients-that-use-wufb"></a>标识使用 WUfB 的客户端  

1. 确保 Windows 更新代理不针对 WSUS 进行扫描（如果以前已启用）。 可使用以下注册表项来指示计算机是否针对 WSUS 或 Windows 更新进行扫描。 如果注册表项不存在，则不会针对 WSUS 进行扫描。
    - **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**
1. Configuration Manager 资源浏览器中的“Windows 更新”  节点下有一个新属性“UseWUServer”  。
1. 基于 **UserWUServer** 属性为通过 WUfB 连接以获取更新和升级的所有计算机创建一个集合。 可以基于如下所示的查询创建集合：  

    ```wql
    Select sr.* from SMS_R_System as sr join SMS_G_System_WINDOWSUPDATE as su on sr.ResourceID=su.ResourceID where su.UseWUServer is null
    ```

1. 创建客户端代理设置以禁用软件更新工作流。 将该设置部署到直接连接到 WUfB 的计算机的集合中。
1. 通过 WUfB 管理的计算机会在符合性状态中显示“未知”  ，且不会计入总体符合性百分比中。  

## <a name="configure-windows-update-for-business-deferral-policies"></a>配置 Windows Update for Business 延迟策略
<!-- 1290890 -->
从 Configuration Manager 版本 1706 开始，针对 Windows 10 功能更新或直接由 Windows Update for Business 托管的 Windows 10 设备的质量更新，可以配置延迟策略。 你可以在“软件库”   > “Windows 10 维护服务”  下方的新“Windows Update for Business 策略”  节点中管理延迟策略。

> [!NOTE]
> 从 Configuration Manager 1802 版开始，可以为 Windows 预览体验设置延迟策略。 <!--507201-->  
有关 Windows 预览体验计划的详细信息，请参阅 [Windows 预览体验计划企业版入门](https://docs.microsoft.com/windows/deployment/update/waas-windows-insider-for-business)。

### <a name="prerequisites-for-deferral-policies"></a>延迟策略的先决条件

- Windows 10 版本 1703 或更高版本
- 必须连接 Internet 才能使用适用于企业的 Windows 更新托管的 Windows 10 设备

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>创建 Windows Update for Business 延迟策略

1. 在“软件库”   > “Windows 10 维护服务”   > “Windows Update for Business 策略”  中
1. 在“主页”  选项卡的“创建”  组中，选择“创建 Windows Update for Business 策略”  ，以打开“创建 Windows Update for Business 策略向导”。
1. 在“常规”  页上，提供策略的名称和描述。
1. 在“延迟策略”  页上，配置是否要延迟或暂停功能更新。 功能更新通常是针对 Windows 的新增功能。 在配置“分支就绪级别”  设置后，你可以根据其可用性定义是否要延迟从 Microsoft 接收功能更新以及延迟时长。
    - **分支就绪级别**：设置设备将接收 Windows 更新的分支。 选择半年频道（已设定目标）、半年频道或 Windows 预览体验成员内部版本。

        > [!NOTE]
        > 将“半年频道（已设定目标）”的策略部署到 Windows 10 版本 1903 或更高版本   。 将“半年频道”的策略部署到 Windows 10 版本 1809 或更低版本   。
        >
        > 如果将“半年频道”的策略部署到 Windows 10 版本 1903 或更高版本，部署将会失败，并出现错误 0x8004100c   。<!-- 5593139 -->

    - **延迟期(天)** ：指定功能更新将被延迟的天数。 最多可以自更新发布之日起，在 365 天内延迟接收这些功能更新。
    - **暂停功能更新启动**：选择是否要在自暂停更新之日起最多 35 天内暂停设备接收功能更新。 在设置的最大天数过后，暂停功能将自动过期，并且设备将扫描 Windows 更新以获取适用的更新。 在此扫描之后，你可以再次暂停更新。 通过清除该复选框，可以取消暂停功能更新。
1. 选择是否要延迟或暂停质量更新。 质量更新通常是对现有 Windows 功能的修复和改进，通常会在每个月的第一个星期二发布，虽然 Microsoft 可以在任何时候发布。 你可以根据其可用性定义是否要延迟接收质量更新，以及它的延迟时长。
    - **延迟期(天)** ：指定质量更新将被延迟的天数。 最多可以自更新发布之日起，在 30 天内延迟接收这些质量更新。
    - **暂停质量更新启动**：选择是否要暂停设备接收质量更新，暂停时间为自暂停更新之日起的 35 天内。 在设置的最大天数过后，暂停功能将自动过期，并且设备将扫描 Windows 更新以获取适用的更新。 在此扫描之后，你可以再次暂停更新。 通过清除该复选框，可以取消暂停质量更新。
1. 选择“安装来自其他 Microsoft 产品的更新”  ，可启用使延迟设置适用于 Microsoft 更新以及 Windows 更新的组策略设置。
1. 选择“包括 Windows 更新中的驱动程序”  ，可自动更新 Windows 更新中的驱动程序。 如果清除此设置，则不会从 Windows 更新下载驱动程序更新。
1. 完成向导以创建新的延迟策略。

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>部署 Windows Update for Business 延迟策略

1. 在“软件库”   > “Windows 10 维护服务”   > “Windows Update for Business 策略”  中
1. 在“主页”  选项卡的“部署”  组中，选择“部署 Windows Update for Business 策略”  。
1. 配置下列设置：
    - **要部署的配置策略**：选择要部署的适用于企业的 Windows 更新策略。
    - **集合**：单击“浏览”，可选择要在其中部署策略的集合  。
    - **允许维护时段外的修正**：如果已为要向其部署策略的集合配置维护时段，启用此选项可以让策略设置在维护时段外修正值。 有关维护时段的详细信息，请参阅[如何使用维护时段](../../core/clients/manage/collections/use-maintenance-windows.md)。
    - **计划**：指定在客户端计算机上对部署的策略进行评估所依据的符合性评估计划。 该计划可以是简单计划或自定义计划。
1. 完成向导以部署策略。
