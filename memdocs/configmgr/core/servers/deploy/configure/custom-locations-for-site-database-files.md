---
title: 自定义数据库文件位置
titleSuffix: Configuration Manager
description: 了解如何为 SQL Server 数据库文件指定自定义位置。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d3f01e54ba196ee9c27295d8f970a7dbe352f63f
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906177"
---
# <a name="custom-locations-for-configuration-manager-site-database-files"></a>Configuration Manager 站点数据库文件的自定义位置

适用范围：  Configuration Manager (Current Branch)

 Configuration Manager 支持 SQL Server 数据库文件的自定义位置。  

> [!NOTE]  
>  使用 SQL Server 群集时，用于指定非默认文件位置的选项不可用。  

 在新的主站点或管理中心站点的**安装过程中**，你可以：  

-   **指定站点数据库的非默认文件位置**：然后，Configuration Manager 安装程序使用这些位置创建站点数据库。  

-   **指定使用预先创建的 SQL Server 数据库，该数据库使用自定义文件位置**：然后，Configuration Manager 安装程序使用该预先创建的数据库及其预配置的文件位置。  

**安装之后**，可以更改站点数据库文件的位置。 这需要你停止该站点并在 SQL Server 中编辑文件位置：  

-   在 Configuration Manager 站点服务器上，停止 **SMS_Executive** 服务。  

-   有关如何移动用户数据库的详细信息，请参阅[移动用户数据库](https://docs.microsoft.com/sql/relational-databases/databases/move-user-databases?view=sql-server-2014)。  

-   完成数据库文件移动后，在 Configuration Manager 站点服务器上重启 **SMS_Executive** 服务。  
