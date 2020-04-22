---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/04/2019
ms.openlocfilehash: 5d65b2c250890c10c16214bcee385c39a4f58204
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697925"
---
### <a name="hardware-inventory-reports"></a><a name="ki_hinv"></a> 硬件清单报告

<!--5468413-->
若尝试运行依赖硬件清单的报告，它将返回错误。 例如，BitLocker 报告返回类似以下消息的错误：

```
Microsoft.Reporting.WinForms.ReportServerException
An error has occurred during report processing. (rsProcessingAborted)
```

还可能在 dataldr.log 文件中看到下面的错误： 

`[42S22][207][Microsoft][SQL Server Native Client 11.0][SQL Server]Invalid column name 'FileTimeStamp00'. : pOFFICE_ADDIN_DATA`

依赖硬件清单的控制台仪表板也可能受到影响。

此问题由特定硬件清单表上的数据库架构更改导致。

#### <a name="workaround"></a>解决方法

解决方法为弃用数据库中预先存在的属性。 然后数据加载程序站点组件可以创建新的属性。 在站点数据库服务器上运行以下 SQL 脚本，以修复表架构：

``` SQL
IF NOT EXISTS (SELECT * FROM SYS.columns WHERE name = 'FileTimestamp00' AND object_id = OBJECT_ID('OFFICE_ADDIN_DATA'))
BEGIN
       DELETE am
       FROM AttributeMap am
       INNER JOIN GroupMap gm ON am.GroupKey=gm.GroupKey
       WHERE gm.GroupClass='MICROSOFT|OFFICE_ADDIN|1.0'
       AND am.AttributeName='FileTimeStamp'

       PRINT 'Fix OFFICE_ADDIN_DATA schema'
END
```
