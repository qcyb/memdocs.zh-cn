---
title: 规划站点数据库
titleSuffix: Configuration Manager
description: 规划 Configuration Manager 层次结构时，请考虑站点数据库和站点数据库服务器角色。
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 068511c5b3b0c15eb355c484b241a76d9dd512e2
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700174"
---
# <a name="plan-for-the-site-database-for-configuration-manager"></a>为 Configuration Manager 规划站点数据库

适用范围：  Configuration Manager (Current Branch)

站点数据库服务器是运行 Microsoft SQL Server 受支持版本的计算机。 SQL Server 用于存储 Configuration Manager 站点的信息。 Configuration Manager 层次结构中的每个站点都包含站点数据库以及分配了站点数据库服务器角色的服务器。  

-   对于管理中心站点和主站点，你可以在站点服务器上安装 SQL Server，或者可以在不是站点服务器的计算机上安装 SQL Server。  

-   对于辅助站点，可使用 SQL Server Express，而不是完整的 SQL Server 安装。 但是，数据库服务器必须在辅助站点服务器上运行。  

-  若要使用 SQL 可用性组，数据库恢复模式必须设置为“完全”  

-  若要使用非 SQL 可用性组，数据库恢复模式必须设置为“简单”  

有关 SQL 恢复模式的更多信息，请参阅[恢复模式 (SQL Server)](/sql/relational-databases/backup-restore/recovery-models-sql-server)。

以下 SQL Server 配置可以用于承载站点数据库：  

-   SQL Server 的默认实例  

-   运行 SQL Server 的单台计算机上的命名实例  

-   SQL Server 的群集实例上的命名实例  

-   SQL Server AlwaysOn 可用性组（从 Configuration Manager 版本 1602 开始）


若要承载站点数据库，SQL Server 必须满足[对 Configuration Manager 的 SQL Server 版本的支持](../../../core/plan-design/configs/support-for-sql-server-versions.md)中详述的要求。  



## <a name="remote-database-server-location-considerations"></a>远程数据库服务器位置的注意事项  

如果使用远程数据库服务器计算机，请确保干预网络连接是高可用的高带宽网络连接。 站点服务器和某些站点系统角色必须与托管站点数据库的远程服务器持续通信。

-   与数据库服务器通信所需的带宽量取决于多个不同站点和客户端配置的组合。 因此，无法充分预测所需的实际带宽。  

-   运行 SMS 提供程序以及连接到站点数据库的每台计算机都会增加网络带宽需求。  

-   运行 SQL Server 的计算机所在的域必须与站点服务器和运行 SMS 提供程序的所有计算机具有双向信任。  

-   当站点数据库与站点服务器并存时，你无法为站点数据库服务器使用群集 SQL Server。  


通常，站点系统服务器仅支持来自单个 Configuration Manager 站点的站点系统角色。 但是，可在运行 SQL Server 的群集/非群集服务器上使用不同的 SQL Server 实例，用于托管来自不同 Configuration Manager 站点的数据库。 为了支持不同站点中的数据库，你必须将 SQL Server 的每个实例配置为使用唯一端口进行通信。