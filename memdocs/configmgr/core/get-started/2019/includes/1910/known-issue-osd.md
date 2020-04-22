---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/17/2019
ms.openlocfilehash: 668db6aa10fbee0a078eef04f0560973e5ed9454
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697845"
---
### <a name="task-sequences-arent-available-to-pxe-or-media"></a><a name="ki_osd"></a> 任务序列对 PXE 或媒体不可用

<!--5578298-->
如果为 PXE 或媒体（USB 或 DVD）部署任务序列，则客户端不会收到此策略。 下面是 smsts.log 中的消息  ：

`There are no task sequences available to this computer.`

#### <a name="workaround"></a>解决方法

从软件中心启动任务序列。
