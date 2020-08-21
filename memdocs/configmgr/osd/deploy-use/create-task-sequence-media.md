---
title: 创建任务序列媒体
titleSuffix: Configuration Manager
description: 创建任务序列媒体并将 OS 部署到 Configuration Manager 环境中的目标计算机。
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf7ce32ed9e126b5526c68b7da03cf44d9b5062d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125162"
---
# <a name="create-task-sequence-media"></a>创建任务序列媒体

适用范围：  Configuration Manager (Current Branch)

可以使用媒体从引用计算机中捕获 OS 映像，或者将 OS 部署到 Configuration Manager 环境中的目标计算机。 你创建的媒体可以是 CD、DVD 集或者 USB 闪存驱动器。

介质主要用于在没有网络连接或与站点有低带宽连接的计算机上部署 OS。 不过，还可以使用媒体启动现有 Windows OS 之外的 OS 部署。 当没有 OS、OS 无法正常运行或你要对磁盘进行重新分区时，这种方法很有用。

部署介质包括可启动介质、独立介质和预留介质。 媒体的内容因你使用的媒体类型而异。 例如，独立介质包含部署 OS 的任务序列。 其他类型的媒体从管理点检索任务序列。

> [!IMPORTANT]
> 若要创建任务序列媒体，必须是从中运行 Configuration Manager 控制台的计算机上的管理员。 如果你不是管理员，在你启动创建任务序列媒体向导时，系统会提示你提供管理员凭据。

## <a name="capture-media"></a><a name="BKMK_PlanCaptureMedia"></a>捕获媒体

使用捕获媒体可以从引用计算机捕获 OS 映像。 捕获媒体包含用于启动引用计算机的启动映像，以及用于捕获 OS 映像的任务序列。

## <a name="bootable-media"></a><a name="BKMK_PlanBootableMedia"></a>可启动媒体

可启动媒体包含以下组件：

- 启动映像
- 可选的[预启动命令](../understand/prestart-commands-for-task-sequence-media.md)及其所需的文件
- Configuration Manager 二进制文件

在目标计算机启动时，它连接到网络，并从网络中检索任务序列、OS 映像和任何其他必需的内容。 由于任务序列不在媒体上，因此，无需重新创建媒体就能更改任务序列或内容。  

> [!IMPORTANT]  
> 可启动媒体上的包并未加密。 采取适当的安全措施（例如向媒体添加密码），确保阻止未经授权的用户访问包内容。  

自版本 2006 起，可启动介质可以下载基于云的内容。 设备仍需要与管理点建立 Intranet 连接。 它可以从已启用内容的云管理网关 (CMG) 或云分发点获取内容。<!--6209223--> 有关详细信息，请参阅[支持基于云的内容](use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content)。

## <a name="prestaged-media"></a><a name="BKMK_PlanPrestagedMedia"></a>预留媒体

使用预留媒体，可以在执行预配过程之前将可启动媒体和 OS 映像应用到硬盘。 预留媒体是 Windows 映像 (WIM) 文件。 制造商可以在生成过程中将它安装到裸机计算机上。 也可以在没有连接到生产 Configuration Manager 环境的暂存中心内使用它。

预留媒体包含用于启动目标计算机的启动映像，以及应用到目标计算机的 OS 映像。 你还可以指定要作为预留媒体的一部分包含的应用程序、包和驱动程序包。 用于部署 OS 的任务序列不包含在该媒体中。 部署使用预留媒体的任务序列时，客户端会先检查本地任务序列缓存是否存在有效的内容。 如果找不到内容或内容已被修改，客户端会从分发点或对等机中下载内容。  

在将新计算机发给用户之前，你将预留介质应用到新计算机的硬盘驱动器上。 在应用预留媒体后首次启动计算机时，计算机将在 Windows PE 中启动。 它会连接到管理点以查找将完成 OS 部署过程的任务序列。  

> [!IMPORTANT]
> 预留媒体上的包并未加密。 采取适当的安全措施（例如向媒体添加密码），确保阻止未经授权的用户访问包内容。

## <a name="standalone-media"></a><a name="BKMK_PlanStandaloneMedia"></a> 独立介质

独立介质包含部署 OS 所需的一切。 此内容包括任务序列和所需的任何其他内容。 因为此介质包含一切，所以需要的磁盘空间要比其他类型的介质大。

## <a name="considerations-when-using-https"></a>使用 HTTPS 时的注意事项

在将管理点和分发点均配置为使用 HTTPS 时，在主站点而不是管理中心站点上创建启动媒体和预留媒体。 此外，还要考虑以下两点，帮助确定是将媒体配置为动态媒体还是基于站点的媒体：  

- 若要将媒体配置为动态媒体，所有主站点均必须具有你从中创建了媒体的站点的根证书颁发机构 (CA)。 可以将根 CA 导入到层次结构中的所有主站点。  

- 在 Configuration Manager 层次结构中的主站点使用不同的根 CA 时，必须在每个站点使用基于站点的媒体。  

## <a name="next-steps"></a>后续步骤

- [创建捕获媒体](create-capture-media.md)

- [创建可启动媒体](create-bootable-media.md)

- [创建预留媒体](create-prestaged-media.md)

- [创建独立介质](create-stand-alone-media.md)
