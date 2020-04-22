---
title: 部署监视工具
titleSuffix: Configuration Manager
description: 使用部署监视工具对 Configuration Manager 客户端上的软件部署进行故障排除。
ms.date: 09/24/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9edc214f-f405-456d-80df-8adcc2a5428d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5a27e96cf69ab01b58910ae02fc732940eda8a04
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707825"
---
# <a name="deployment-monitoring-tool"></a>部署监视工具

适用范围：  Configuration Manager (Current Branch)

部署监视工具是一个 [Configuration Manager 工具](tools.md)。 它是图形用户界面，旨在帮助对 Configuration Manager 客户端上的应用程序、软件更新和配置基线部署进行故障排除。 该工具为只读状态，因为它不会改变客户端上的任何状态。 可放心用它来诊断常见部署方案。


## <a name="features"></a>功能

- 以管理员身份运行该工具，以对本地客户端上的部署进行故障排除。  

- 对远程客户端上的部署进行故障排除。 启动工具并以管理员身份连接到远程计算机。  

- 将工具中收集的所有数据以 XML 格式导出。 与其他用户共享该 XML 文件，并将其用作讨论对部署进行故障排除的常用平台。  

- 将以前导出的数据导入不同的计算机，并使用数据在脱机模式下运行工具。   


## <a name="usage"></a>用法

部署监视工具仅支持图形用户界面。 若要启动工具，以管理员身份运行 DeploymentMonitoringTool.exe  。 有三个视图：  

- **客户端属性**：关于设备和 Configuration Manager 客户端的实用特性列表。 此为默认视图。   

- **部署**：查看所有当前目标部署。 在结果窗格中选择部署，以查看详细内容窗格中的详细信息。  

- **所有更新**：查看所有软件更新及其状态。  

若要复制任意视图中的数据，选择某一单元格并按 CTRL + C   。


### <a name="actions-menu"></a>“操作”菜单

“操作”菜单中提供以下操作  ：  

- **连接到远程计算机**：选择要连接到的计算机。 如果未指定用户名和密码，则使用当前凭据。 单击“保存”以连接到远程计算机  。  

- **导出数据**：选择要将数据写入其中的文件，然后单击“保存”  。 使用导出的 XML 文件，对不同计算机进行远程故障排除。  

- **导入数据**：选择要导入到工具中的文件。  

- **查看日志**：根据视图打开关联的日志文件：  
    - 客户端属性：`\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - 部署：`\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - 所有更新：`C:\Windows\WindowsUpdate.log`



## <a name="see-also"></a>另请参阅

- [部署应用程序](../../apps/deploy-use/deploy-applications.md)
- [部署软件更新](../../sum/deploy-use/deploy-software-updates.md)
- [部署配置基线](../../compliance/deploy-use/deploy-configuration-baselines.md)
