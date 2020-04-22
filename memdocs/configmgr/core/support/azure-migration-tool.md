---
title: 将本地站点扩展并迁移到 Microsoft Azure
titleSuffix: Configuration Manager
description: 了解如何使用迁移工具以编程方式为 Configuration Manager 创建 Azure 虚拟机。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1c975c5e-efd1-4d47-a315-39ccb32633dc
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 00f07e20c24ea9bb7d06b18f300e0206696c5e20
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707935"
---
# <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>将本地站点扩展并迁移到 Microsoft Azure

适用范围：  Configuration Manager (Current Branch)


版本 1910 中引入的此工具有助于你以编程方式为 Configuration Manager 创建 Azure 虚拟机 (VM)。 <!--3556022--> 它可以使用默认设置站点角色（如被动站点服务器、管理点和分发点）进行安装。 验证新角色后，将其用作其他站点系统以实现高可用性。 你还可以删除本地站点系统角色，仅保留 Azure VM 角色。

## <a name="prerequisites"></a>必备条件

- Azure 订阅

- 具有 ExpressRoute 网关的 Azure 虚拟网络

<!-- - A standalone primary site. A hierarchy with a central administration site isn't currently supported. can comment this out because TP only supports a standalone primary!-->

- 你的用户帐户必须是 Configuration Manager“完全权限管理员”，并在主站点服务器上拥有管理员权限  。

- 若要添加被动服务器，主站点必须满足[站点服务器高可用性要求](../servers/deploy/configure/site-server-high-availability.md#prerequisites)。 例如，它需要一个[远程内容库](../plan-design/hierarchy/the-content-library.md#bkmk_remote)。

### <a name="required-azure-permissions"></a>必需的 Azure 权限

运行该工具时，需要在 Azure 中具有以下权限：
<!--5789222-->
Microsoft.Resources/subscriptions/resourceGroups/read <br>
Microsoft.Resources/subscriptions/resourceGroups/write <br>
Microsoft.Resources/deployments/read <br>
Microsoft.Resources/deployments/write <br>
Microsoft.Resources/deployments/validate/action <br>
Microsoft.Compute/virtualMachines/extensions/read <br>
Microsoft.Compute/virtualMachines/extensions/write <br>
Microsoft.Compute/virtualMachines/read <br>
Microsoft.Compute/virtualMachines/write <br>
Microsoft.Network/virtualNetworks/read <br>
Microsoft.Network/virtualNetworks/subnets/read <br>
Microsoft.Network/virtualNetworks/subnets/join/action <br>
Microsoft.Network/networkInterfaces/read <br>
Microsoft.Network/networkInterfaces/write <br>
Microsoft.Network/networkInterfaces/join/action <br>
Microsoft.Network/networkSecurityGroups/write <br>
Microsoft.Network/networkSecurityGroups/read <br>
Microsoft.Network/networkSecurityGroups/join/action <br>
Microsoft.Storage/storageAccounts/write <br>
Microsoft.Storage/storageAccounts/read <br>
Microsoft.Storage/storageAccounts/listkeys/action <br>
Microsoft.Storage/storageAccounts/listServiceSas/action <br>
Microsoft.Storage/storageAccounts/blobServices/containers/write <br>
Microsoft.Storage/storageAccounts/blobServices/containers/read <br>
Microsoft.KeyVault/vaults/deploy/action <br>
Microsoft.KeyVault/vaults/read <br>


有关权限和分配角色的详细信息，请参阅[使用 RBAC 管理对 Azure 资源的访问](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal)。

## <a name="run-the-tool"></a>运行该工具

1. 登录到主站点服务器，在 Configuration Manager 安装目录中运行以下工具：`Cd.Latest\SMSSETUP\TOOLS\ExtendMigrateToAzure\ExtendMigrateToAzure.exe`

1. 查看“常规”选项卡上的信息，然后切换到“Azure 信息”选项卡   。

1. 在“Azure 信息”选项卡上，选择你的“Azure 环境”，然后登录    。

    > [!TIP]
    > 可能需要将 `https://*.microsoft.com` 添加到受信任的网站列表才能正确登录。

    [![扩展和迁移工具中的“Azure 信息”选项卡](./media/3556022-azure-information-tab.png)](./media/3556022-azure-information-tab.png#lightbox)

1. 登录后，选择“订阅 ID”和“虚拟网络”   。 此工具仅列出具有 ExpressRoute 网关的网络。

## <a name="site-server-high-availability"></a>站点服务器高可用性

1. 在“站点服务器高可用性”选项卡上，选择“检查”以评估站点的就绪情况   。

    如果任何检查失败，请选择“更多详细信息”，确定如何修正该问题  。 有关这些先决条件的详细信息，请参阅[站点服务器高可用性](../servers/deploy/configure/site-server-high-availability.md#prerequisites)。

2. 如果要将站点服务器扩展或迁移到 Azure，请选择“在 Azure 中创建站点服务器”  。 然后填写以下字段：

    |名称|说明|
    |---|---|
    |**订阅**|只读。 显示订阅名称和 ID。|
    |**资源组**| 列出可用的资源组。 如果需要创建新的资源组，请使用 [Azure 门户](https://portal.azure.com)，然后重新运行此工具。|
    |**位置**| 只读。 由虚拟网络的位置确定|
    |**VM 大小**|选择要适应工作负荷的大小。 Microsoft 建议使用 Standard_DS3_v2  。|
    |**操作系统**|只读。 该工具使用 Windows Server 2019。|
    |**磁盘类型**|只读。 该工具使用高级 SSD 以获得最佳性能。|
    |**虚拟网络**|只读。|
    |**子网**|选择要使用的子网。 如果需要创建新的子网，请使用 [Azure 门户](https://portal.azure.com)。|
    |**计算机名**|在 Azure 中输入被动站点服务器 VM 的名称。 它与 [Azure 门户](https://portal.azure.com)中显示的名称相同。|
    |**本地管理员用户名**|输入 Azure VM 在加入域之前创建的本地管理用户的名称。|
    |**本地管理员密码**|本地管理员用户的密码。 若要在 Azure 部署过程中保护密码，请在 [Azure 密钥保管库](https://docs.microsoft.com/azure/key-vault/key-vault-overview)中将密码存储为机密。 然后，使用此处的参考。 如果需要，请从 [Azure 门户](https://portal.azure.com)创建一个新的。|
    |**域 FQDN**|要加入的 Active Directory 域的完全限定域名。 默认情况下，该工具从当前计算机中获取此值。|
    |**域用户名**|允许加入域的域用户的名称。 默认情况下，该工具使用当前已登录用户的名称。|
    |**域密码**|要加入域的域用户的密码。 选择“开始”后，该工具将对其进行验证  。 若要在 Azure 部署过程中保护密码，请在 [Azure 密钥保管库](https://docs.microsoft.com/azure/key-vault/key-vault-overview)中将密码存储为机密。 然后，使用此处的参考。 如果需要，请从 [Azure 门户](https://portal.azure.com)创建一个新的。|
    |**域 DNS IP**|用于加入域。 默认情况下，该工具从当前计算机中获取当前 DNS。|
    |**类型**|只读。 它显示“被动站点服务器”作为类型  。|

    > [!IMPORTANT]
    > 默认情况下，虚拟机的“使用现有 Windows Server 许可证”  设置为“否”  。 如果要通过软件保障使用本地 Windows Server 许可证，请在配置虚拟机后在 [Azure 门户](https://portal.azure.com)中配置此设置。 有关详细信息，请参阅 [Windows Server 的 Azure 混合权益](https://docs.microsoft.com/windows-server/get-started/azure-hybrid-benefit)。

1. 若要开始预配 Azure VM，请选择“开始”  。 若要监视部署状态，请切换到工具中的“Azure 中的部署”选项卡  。 若要获取最新状态，请选择“刷新部署状态”  。

    > [!TIP]
    > 你还可以使用 [Azure 门户](https://portal.azure.com)来检查状态，查找错误并确定可能的修补程序。

1. 部署完成后，请转到 SQL Server，为新的 Azure VM 授予权限。 有关详细信息，请参阅[站点服务器高可用性 - 先决条件](../servers/deploy/configure/site-server-high-availability.md#prerequisites)。

1. 若要在被动模式下将 Azure VM 添加为站点服务器，请选择“在被动模式下添加站点服务器”  。

1. 一旦站点在被动模式下添加站点服务器，“站点服务器高可用性”选项卡便会显示状态  。

   [![被动站点服务器已添加到“站点服务器高可用性”选项卡](./media/3556022-site-server-passive-mode.png)](./media/3556022-site-server-passive-mode.png#lightbox)

1. 接下来，转到[“Azure 中的部署”](#bkmk_deploy-azure)选项卡以完成部署。

## <a name="site-database"></a>站点数据库

该工具当前没有任何任务可用于将数据库从本地迁移到 Azure。 可以选择将数据库从本地 SQL Server 移到 Azure SQL Server VM。 该工具在“站点数据库”选项卡上列出了以下文章来帮助进行操作  ：

- [备份和还原数据库](../servers/manage/backup-and-recovery.md)
- [配置 SQL Always On 并允许复制数据](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#changes-for-site-backup)
- [将 SQL 数据库迁移到 Azure SQL Server VM](/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)

## <a name="site-system-roles"></a>站点系统角色

1. 切换到“站点系统角色”选项卡  。若要使用默认设置来预配新的站点系统角色，请选择“新建”  。 你可以预配角色，例如管理点、分发点和软件更新点。 并非所有角色目前都在该工具中可用。

    [![扩展和迁移工具中的“站点系统角色”选项卡](./media/3556022-site-system-roles-tab.png)](./media/3556022-site-system-roles-tab.png#lightbox)

1. 在预配窗口中，填写字段以在 Azure 中预配站点角色的 VM。 这些详细信息类似于站点服务器的上述列表。

1. 若要开始预配 Azure VM，请选择“开始”  。 若要监视部署状态，请切换到工具中的“Azure 中的部署”选项卡  。 若要获取最新状态，请选择“刷新部署状态”  。

    > [!TIP]
    > 你还可以使用 [Azure 门户](https://portal.azure.com)来检查状态，查找错误并确定可能的修补程序。

1. 重复此过程可添加更多站点系统角色。

1. 接下来，转到[“Azure 中的部署”](#bkmk_deploy-azure)选项卡以完成部署。

1. 部署完成后，请转到 Configuration Manager 控制台，对站点角色进行其他更改。

## <a name="deployments-in-azure"></a><a name="bkmk_deploy-azure"></a> Azure 中的部署

1. Azure 创建 VM 后，请切换到工具中的“Azure 中的部署”选项卡  。 选择“部署”以使用默认设置来配置角色  。

1. 选择“运行”以启动 PowerShell 脚本  。

    [![通过运行生成的 PowerShell 脚本来部署站点角色](./media/3556022-run-powershell-script-deployment.png)](./media/3556022-run-powershell-script-deployment.png#lightbox)

1. 重复执行此过程以配置更多角色。

## <a name="add-site-roles-to-an-existing-virtual-machine-deployment"></a><a name="bkmk_add_role"></a> 将站点角色添加到现有虚拟机部署
<!--5665775, 6307931-->
从 Configuration Manager 版本 2002 开始，将本地站点扩展和迁移到 Microsoft Azure 工具支持在单个 Azure 虚拟机上预配多个站点系统角色。 初始 Azure 虚拟机部署完成后，可以添加站点系统角色。 要将新角色添加到现有虚拟机，请执行以下步骤：
1. 在“Azure 中的部署”选项卡上单击状态为“已完成”的虚拟机部署   。
1. 单击“新建”按钮，将其他角色添加到虚拟机  。


## <a name="next-steps"></a>后续步骤

在 [Azure 门户](https://portal.azure.com)中查看所做更改
