---
title: 管理 VDI 客户端
titleSuffix: Configuration Manager
description: 在虚拟桌面基础结构 (VDI) 中管理 Configuration Manager 客户端。
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b01348695ac5b3b64ca87a9b42aa52ac235b533d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693855"
---
# <a name="manage-configuration-manager-clients-in-a-virtual-desktop-infrastructure-vdi"></a>在虚拟桌面基础结构 (VDI) 中管理 Configuration Manager 客户端

适用范围：  Configuration Manager (Current Branch)

Configuration Manager 支持在以下虚拟桌面基础结构 (VDI) 方案中安装 Configuration Manager 客户端：  

- **个人虚拟机** - 若要确保在会话之间在虚拟机上维护用户数据和设置时，通常使用个人虚拟机。  

- **远程桌面服务会话** - 远程桌面服务使服务器能够承载多个并发客户端会话。 用户可以连接到会话，然后在该服务器上运行应用程序。  

- **共用的虚拟机** - 在会话之间不保留共用的虚拟机。 当关闭会话时，将丢弃所有数据和设置。 当无法使用远程桌面服务时（因为所需的业务应用程序无法在承载客户端会话的 Windows Server 上运行），共用的虚拟机很有用。  

  下表列出了关于在虚拟桌面基础结构中管理 Configuration Manager 客户端的考虑事项。  

|虚拟机类型|注意事项|  
|--------------------------|--------------------|  
|个人虚拟机|Configuration Manager 将个人虚拟机同等地视为物理计算机。 可以在虚拟机映像上预先安装 Configuration Manager 客户端，或者在预配虚拟机之后部署该客户端。|  
|远程桌面服务|不会为单个远程桌面会话安装 Configuration Manager 客户端。 而是在远程桌面服务服务器上仅一次性地安装客户端。 在远程桌面服务服务器上可以使用所有的 Configuration Manager 功能。|  
|共用的虚拟机|当共用的虚拟机被解除授权时，使用 Configuration Manager 所做的任何更改都会丢失。<br /><br /> Configuration Manager 功能（如硬件清单、软件清单和软件计数）返回的数据可能与用户的需求无关，因为虚拟机可能仅运行很短一段时间。 请考虑从清单任务中排除共用的虚拟机。|  

 因为虚拟化支持在同一物理计算机上运行多个 Configuration Manager 客户端，所以对于计划操作（如硬件和软件清单、反恶意软件扫描、软件安装和软件更新扫描），许多客户端操作都具有内置的随机化延迟。 对于具有运行 Configuration Manager 客户端的多个虚拟机的计算机，此延迟有助于分发 CPU 处理以及数据传输。  

> [!NOTE]  
>  除了处于维护模式的 Windows Embedded 客户端之外，未在虚拟化环境中运行的 Configuration Manager 客户端也使用此随机化延迟。 如果具有许多部署的客户端，则此行为有助于避免网络带宽高峰，并且可以在 Configuration Manager 站点系统（如管理点和站点服务器）上减少 CPU 处理要求。 延迟间隔因 Configuration Manager 功能而异。  
>   
>  默认情况下，使用以下客户端设置为所需软件更新禁用了随机延迟：**计算机代理**：**禁用截止时间随机化**。
