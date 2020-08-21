---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: a61bf84a872458f37826c3de07ede05b1b658f0c
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127286"
---
<!--3555750 FKA 1357954 --Don't apply H2/H3 in this include file since they are context driven by article-->

在启用共同管理时，可以使用“Azure 公有云”、“Azure 美国政府云”或“Microsoft Azure 中国世纪互联”（在版本 2006 中添加的）。 若要从 Configuration Manager 版本 1906 开始启用共同管理，请按照以下说明操作：

1. 在 Configuration Manager 控制台中，转到“管理”工作区，展开“云服务”，然后选择“共同管理”节点。 选择功能区中的“配置共同管理”，以打开“共同管理配置向导”。

1. 在此向导的“租户加入”页上，配置要使用的“Azure 环境”。 选择以下环境之一：

   - Azure 公有云
   - Azure 美国政府云。<!--4075452-->
   - Azure 中国云（在版本 2006 中添加的）<!--7133238-->
      - 在加入 Azure 中国云之前，在设备上将 Configuration Manager 客户端更新为最新版本。 <!--7630213--> 

   如果你选择“Azure 中国云”或“Azure 美国政府云”，用于[租户附加](../../tenant-attach/device-sync-actions.md)的“上传到 Microsoft Endpoint Manager 管理中心”选项是禁用的。

1. 选择“登录”。 以 Azure AD 全局管理员身份登录，然后选择“下一步”。 只需登录一次即可完成向导。 系统不会存储登录凭据，也不会在任何其他地方使用这些凭据。

1. 在“启用”**** 页上，选择以下设置：

   - **在 Intune 中自动注册** - 可在 Intune 中为现有的 Configuration Manager 客户端自动注册客户端。 此选项允许对客户端子集启用共同管理，以初步测试共同管理，并使用分阶段的方式推出共同管理。 如果用户取消注册某个设备，则它将在下次评估策略时重新注册。 <!--3330596-->

      - **试点** - 仅属于“Intune 自动注册”集合成员的 Configuration Manager 客户端才会自动注册到 Intune****。
      - **全部** - 为所有 Windows 10 1709 版或更高版本的客户端启用自动注册。

   - **Intune 自动注册** - 此集合应包含所有要加入共同管理的客户端。 它实质上是所有其他暂存集合的超集。

   ![指定 Intune 自动注册集合 ](../media/3555750-co-management-onboarding-enablement.png)
      
      自动注册并非对所有客户都是即时的。 此行为有助于更好地扩展大型环境的注册。 Configuration Manager 根据客户端数量随机注册。 例如，如果环境中有 100,000 个客户端，则在启用此设置时，注册将持续几天。<!--1358003-->

      > [!Note]  
      > 从版本 1906 开始：
      >
      > - 新的共同管理设备现可根据其 Azure Active Directory (Azure AD) 设备令牌自动注册到 Microsoft Intune 服务。 无需等待用户登录到设备，就能启动自动注册。 这项更改有助于减少注册状态为“挂起用户登录”的设备数量**。<!-- 4454491 --> 为支持此行为，设备需要运行 Windows 10 版本 1803 或更高版本。 有关详细信息，请参阅[共同管理注册状态](../how-to-monitor.md#co-management-enrollment-status)。
      >
      > - 如果你已将设备注册到共同管理，则新设备一旦满足[先决条件](../overview.md#prerequisites)即可立即注册。<!--4321130-->

1. 对于已在 Intune 中注册了基于 Internet 的设备，复制并保存“启用”**** 页上的命令行。 对于基于 Internet 的设备，你将使用此命令行将 Configuration Manager 客户端安装为 Intune 中的应用。 如果暂不保存此命令行，可以随时查看共同管理配置以获取此命令行。

1. 在****“工作负载”页上，为每个工作负载选择要移动的设备组以便使用 Intune 进行管理。 有关详细信息，请参阅[工作负载](../workloads.md)。 如果只想启用共同管理，则无需立即切换工作负载。 可以稍后切换工作负载。 有关详细信息，请参阅[如何切换工作负载](../how-to-switch-workloads.md)。  

    - **试点 Intune** - 将在“暂存”页上指定的试点集合中的设备切换已关联的工作负载****。 每个工作负载都可以有不同的试点集合。
    - **Intune** - 切换所有共同管理的 Windows 10 设备的关联的工作负荷。  

    > [!Important]
    > 切换任何工作负载之前，请确保在 Intune 中正确配置并部署相应的工作负载。 请确保工作负荷始终由设备的某个管理工具进行托管。  

1. 在“暂存”**** 页上，为设置为“试点 Intune”**** 的每个工作负载指定试点集合。

   ![指定 Intune 自动注册集合 ](../media/3555750-co-management-onboarding-staging.png)

1. 要启用共同管理，请完成向导。
