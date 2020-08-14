---
title: 创建预留媒体
titleSuffix: Configuration Manager
description: 使用 Configuration Manager 中的预留媒体来简化几个方案中的 Windows 部署。
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 82bb02d8154939b4b0e0ee89bcc6637e9393acff
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125213"
---
# <a name="create-prestaged-media"></a>创建预留媒体

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 中的预留媒体是 Windows 映像 (WIM) 文件。 它可以由制造商安装在裸机上，也可以安装在未连接到生产 Configuration Manager 环境的暂存中心。 预留媒体包含用于启动目标计算机的启动映像，以及应用到目标计算机的 OS 映像。 你还可以指定要作为预留媒体的一部分包含的应用程序、包和驱动程序包。 用于部署 OS 的任务序列不包含在该媒体中。 在将新计算机发送给最终用户之前，预留媒体将应用到此计算机的硬盘驱动器。

为以下 OS 部署方案使用预留媒体：  

- [为工厂中的 OEM 或本地 depot 创建映像](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

- [在新计算机（裸机）上安装新版的 Windows](install-new-windows-version-new-computer-bare-metal.md)  

- [部署 Windows To Go](deploy-windows-to-go.md)  


## <a name="usage"></a>用法

在应用预留媒体后首次启动计算机时，计算机将在 Windows PE 中启动。 它会连接到管理点以查找将完成 OS 部署过程的任务序列。 部署使用预留媒体的任务序列时，客户端会先检查本地任务序列缓存是否存在有效的内容。 如果找不到内容或内容已被修改，客户端会从分发点或对等机中下载内容。  


## <a name="prerequisites"></a>必备条件

在使用“创建任务序列媒体向导”创建预留媒体之前，请确保满足所有条件。

### <a name="boot-image"></a>启动映像

在任务序列中使用启动映像部署 OS 时，请考虑以下注意事项：

- 启动映像的体系结构必须适合于目标计算机的体系结构。 例如，x64 目标计算机可启动和运行 x86 或 x64 启动映像。 但是，x86 目标计算机只能启动和运行 x86 启动映像。
- 确保启动映像包含预配目标计算机所需的网络和存储驱动程序。

### <a name="create-a-task-sequence-to-deploy-an-os"></a>创建用于部署 OS 的任务序列

作为预留媒体的一部分，请指定用于部署 OS 的任务序列。 有关详细信息，请参阅[创建用于安装 OS 的任务序列](create-a-task-sequence-to-install-an-operating-system.md)。

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>分发与任务序列关联的所有内容

将任务序列所需的所有内容至少分发到一个分发点。 此内容包括启动映像、OS 映像和其他关联文件。 向导在创建预留媒体时从分发点中收集内容。

用户帐户至少需要具有对该分发点上的内容库的  读取访问权限。 有关详细信息，请参阅[分发内容](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)。

### <a name="hard-drive-on-the-destination-computer"></a>目标计算机上的硬盘驱动器

在将预留媒体应用到目标计算机的硬盘驱动器之前，必须对其进行格式化。 如果在应用媒体时硬盘驱动器未格式化，则部署 OS 的任务序列将在尝试启动目标计算机时失败。

> [!NOTE]  
> “创建任务序列媒体向导”在媒体上设置以下任务序列变量条件： **_SMSTSMediaType = OEMMedia**。 可以在任务序列中使用此相同条件。  


## <a name="process"></a>过程

 > [!NOTE]  
 > 对于 PKI 环境，由于根 CA 是在主站点处指定的，因此请确保预留媒体是在主站点处创建的。 CAS 站点没有正确创建预留媒体所需的根 CA 信息。

1. 在 Configuration Manager 控制台中，转到“软件库”  工作区，展开“操作系统”  ，选择“任务序列”  节点。  

2. 在功能区的“主页”选项卡上，在“创建”组中，选择“创建任务序列媒体”    。 此操作会启动“创建任务序列媒体向导”。  

3. 在“选择媒体类型”  页上，指定以下选项：  

    - 选择“预留媒体”  。  

    - （可选）如果你希望仅允许部署 OS 而不需要用户输入，请选择“允许无人参与的操作系统部署”  。  

        > [!IMPORTANT]  
        > 如果选择此选项，则不会提示用户输入网络配置信息或可选的任务序列。 如果针对密码保护配置媒体，则仍会提示用户输入密码。  

4. 在“媒体管理”  页上，指定以下选项之一：  

    - **动态媒体**：允许管理点根据客户端在站点边界中的位置将媒体重定向到另一个管理点。  

    - **基于站点的媒体**：媒体仅与指定的管理点联系。  

5. 在“媒体属性”  页上，指定以下信息：  

    - **创建者**：指定创建媒体的人员。  

    - **版本**：指定媒体的版本号。  

    - **注释**：指定媒体用途的唯一说明。  

    - **媒体文件**：指定输出文件的名称和路径。 向导会将输出文件写入到此位置。 例如：`\\servername\folder\outputfile.wim`  

    - **暂存文件夹**<!--1359388-->：媒体创建过程可能需要大量临时驱动器空间。 默认情况下，此位置类似于以下路径：`%UserProfile%\AppData\Local\Temp`。 从版本 1902 开始，若要更灵活地选择存储这些临时文件的位置，请将此值更改为其他驱动器和路径。  

6. 在“安全”  页上，指定以下选项：  

    - **启用未知计算机支持**：允许媒体将 OS 部署到不是由 Configuration Manager 托管的计算机上。 Configuration Manager 数据库中没有这些计算机的记录。 有关详细信息，请参阅[准备未知计算机部署](../get-started/prepare-for-unknown-computer-deployments.md)。  

    - **使用密码保护媒体**：输入强密码来帮助防止未经授权访问媒体。 如果指定密码，则用户必须提供该密码才能使用预留媒体。  

        > [!IMPORTANT]  
        > 作为最佳安全方案，请始终分配密码来帮助保护预留媒体。  
 
    - 对于 HTTP 通信，选择“创建自签名媒体证书”  。 然后指定证书的开始日期和到期日期。  
    
        > [!NOTE] 
        > 如果选择此选项，则在此向导的“启动映像”页上将无法选择 HTTPS 管理点  。

    - 对于 HTTPS 通信，选择“导入 PKI 证书”  。 然后指定要导入的证书及其密码。  

        有关用于启动映像的此客户端证书的详细信息，请参阅 [PKI 证书要求](../../core/plan-design/network/pki-certificate-requirements.md)。  

    - **用户设备相关性**：若要在 Configuration Manager 中支持以用户为中心的管理，请指定希望媒体如何将用户与目标计算机相关联。 有关 OS 部署如何支持用户设备相关性的详细信息，请参阅[如何将用户与目标计算机相关联](../get-started/associate-users-with-a-destination-computer.md)。  

        - **通过自动批准允许用户设备相关性**：媒体自动将用户与目标计算机关联。 此功能以部署 OS 的任务序列的操作为基础。 在此方案中，当任务序列将 OS 部署到目标计算机时，它会在指定的用户和目标计算机之间创建关系。  

        - **允许用户设备相关性挂起管理员批准**：在授予批准后，媒体将用户与目标计算机关联。 此功能以部署 OS 的任务序列的作用域为基础。 在此方案中，任务序列在指定用户和目标计算机之间创建关系，但在部署 OS 之前等待管理用户的批准。  

        - **不允许用户设备相关性**：媒体不会将用户与目标计算机关联。 在此方案中，当任务序列部署 OS 时，它不会将用户与目标计算机关联。  

7. 在“任务序列”  页上，选择将在目标计算机上运行的任务序列。 验证任务序列引用的内容的列表。  

    - **检测关联的应用程序依赖关系并将其添加到此媒体中**：此外，向媒体添加应用程序依赖项内容。  

        > [!TIP]  
        > 如果看不到预期的应用程序依赖项，请取消选择并重新选择此选项以刷新列表。  

8. 在“启动映像”  页上，指定以下选项：  

    > [!IMPORTANT]  
    > 分发的启动映像的体系结构必须适合于目标计算机的体系结构。 例如，x64 目标计算机可启动和运行 x86 或 x64 启动映像。 但是，x86 目标计算机只能启动和运行 x86 启动映像。  

    - **启动映像**：选择用于启动目标计算机的启动映像。  

    - **分发点**：选择具有启动映像的分发点。 向导将从分发点中检索启动映像并将其写入媒体。  

        > [!NOTE]  
        > 用户帐户至少需要具有对该分发点上的内容库的  读取权限。  

    - **管理点**：仅针对基于站点的媒体  ，从主站点中选择管理点。  

    - **关联的管理点**：仅针对动态媒体  ，选择要使用的主站点管理点以及初始通信的优先级顺序。  

        > [!NOTE]  
        > 仅当在此向导的“安全性”页面中指定了 PKI 证书时，才会显示已启用 HTTPS 的管理点  。  

9. 在“映像”  页上，指定以下选项：  

    - **映像包**：指定要使用的 OS 映像。 有关详细信息，请参阅[管理 OS 映像](../get-started/manage-operating-system-images.md)。  

    - **映像索引**：如果包包含多个 OS 映像，请指定要部署的映像的索引。  

    - **分发点**：指定具有 OS 映像包的分发点。 向导将从分发点中获取 OS 映像并将其写入媒体。  

10. 在“选择应用程序”  页上，选择要添加到预留媒体文件的其他应用程序。  

11. 在“选择包”  页上，选择要添加到预留媒体文件的其他包。  

12. 在“选择驱动程序包”  页上，选择要添加到预留媒体文件的其他驱动程序包。  

13. 在“分发点”  页上，选择要从其中获取内容的一个或多个分发点。  

    Configuration Manager 仅显示具有内容的分发点。 先将与任务序列相关联的所有内容分发到至少一个分发点上，然后再继续操作。 在分发内容后，刷新分发点列表。 删除此页中已选中的任何分发点，然后返回到“分发点”  页。 或者，重启该向导。 有关详细信息，请参阅[分发任务序列引用的内容](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS)和[管理内容和内容基础结构](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)  

14. 在“自定义”  页上，指定以下选项：  

    - 添加用于任务序列的任何变量。  

    - **启用预启动命令**：指定想要在运行任务序列之前运行的任何预启动命令。 预启动命令是一个脚本或可执行文件，它可以在任务序列运行之前在 Windows PE 中与用户交互。 有关详细信息，请参阅[任务序列媒体的预启动命令](../understand/prestart-commands-for-task-sequence-media.md)。  

        > [!TIP]  
        > 在媒体创建过程中，任务序列会将包 ID 和预启动命令行（包括任何任务序列变量的值）写入到运行 Configuration Manager 控制台的计算机上的 CreateTSMedia.log  文件。 你可以查看此日志文件以验证任务序列变量的值。  

        如果预启动命令需要任何内容，请选择“包括预启动命令的文件”  选项。  

15. 完成向导。  


## <a name="next-steps"></a>后续步骤

[为工厂中的 OEM 或本地 depot 创建映像](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)
