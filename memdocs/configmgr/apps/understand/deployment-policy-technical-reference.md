---
title: 应用程序部署策略技术参考
titleSuffix: Configuration Manager
description: 对 Configuration Manager 的应用程序部署策略进行故障排除的技术参考。
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: bf24fb83-521f-4a41-ab8e-df70a6c10e78
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51d260ede4ed275c401c3b9f9e131134c62ae74e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688825"
---
# <a name="application-deployment-policy"></a>应用程序部署策略

适用范围：  Configuration Manager (Current Branch)

## <a name="policy-creation"></a>策略创建

在部署应用程序时，将创建一个 [SMS_ApplicationAssignment](../../develop/reference/apps/sms_applicationassignment-server-wmi-class.md) 类的实例，该实例表示将应用程序分配到集合。 可在 SMSProv.log 中跟踪此活动  。

<pre><code class="lang-text">SMS Provider    PutInstanceAsync <b>SMS_ApplicationAssignment</b>~
SMS Provider    Auditing: User CONTOSO\Admin created an instance of class SMS_ApplicationAssignment.~
</code></pre>

在 Configuration Manager 数据库中，此信息存储在 `CI_CIAssignments` 表中，其中 `AssignmentType` 2 表示应用程序部署。 创建分配时，SMS 数据库监视器组件会检测表中的更改，然后通知对象复制管理器处理 CI 分配 (CIA) 策略。 然后，对象复制管理器组件会为数据库中的应用程序分配创建策略，策略存储在数据库中的 `Policy` 表中，并且策略 ID 基于应用程序的唯一 ID。 可通过引用分配唯一 ID 在 objreplmgr.log 中跟踪此活动，该 ID 可从[开始之前](app-deployment-technical-reference.md#before-you-begin)中引用的 SQL 查询中获取  。

<pre><code class="lang-text">***** Processing Application Assignment {<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>} *****
</code></pre>

可使用如下所示的 SQL 查询在数据库中查看应用程序分配的策略。

```sql
SELECT P.PolicyID, PA.PolicyAssignmentID, PA.PADBID, PA.IsTombstoned, PA.LastUpdateTime FROM Policy P
JOIN PolicyAssignment PA ON P.PolicyID = PA.PolicyID
WHERE P.PolicyID = '{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}' -- Replace Assignment Unique ID
```

## <a name="policy-targeting"></a>策略目标

生成策略后，策略提供程序组件会将此策略分配给应用程序部署的目标集合中的资源。 策略目标信息存储在数据库的 `ResPolicyMap` 表中。 可使用上述查询返回的 PADBID 在 policypv.log 中跟踪此活动  。 但是，如果同时处理多个策略，则日志中记录的 PADBID 可能并不总是与上述查询返回的 PADBID 一致。

<pre><code class="lang-text">~Policy or Policy Target Change Event triggered.
~Completed batch with beginning <b>PADBID = 16778403 ending PADBID = 16778403</b>.
</code></pre>

> [!NOTE]
> `ResPolicyMap` 表不包含部署为可供用户集合使用的应用程序的任何目标信息  。 软件中心从管理点查询这些应用程序的列表；当用户从软件中心请求应用程序时，会动态生成这些应用程序的策略目标信息。

## <a name="next-steps"></a>后续步骤

- [应用程序部署到设备集合](device-deployment-technical-reference.md)
- [应用程序部署到用户集合](user-deployment-technical-reference.md)
