---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 12/30/2018
ms.openlocfilehash: 1b4fb4fb087639d1b3c3075339ce890a9c1dbbca
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708215"
---
使用以下定义区分试点和生产：  

- **试点**：在部署到更大的设备集之前，想要验证的设备子集。 使用桌面分析将设备标记为对试点集唯一。 没有资产阻塞时，试点中的设备升级准备就绪。 阻塞的资产被标记为“严重”，“无法”进行升级   。  

- **生产**：注册到桌面分析的所有其他设备都不在试点内。 所有资产都已注销时，生产设备升级准备就绪。 桌面分析会自动注销任何非关键资产。  

