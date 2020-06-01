---
title: 插件配置 XML
titleSuffix: Configuration Manager
description: 包转换管理器插件 XML 元素的技术参考。
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 940cc075-4066-44d5-972a-927c0b0a1143
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9178b595ba67723c623979b4c29290e42fe5f6ac
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2020
ms.locfileid: "83877753"
---
# <a name="technical-reference-for-the-package-conversion-manager-plug-in-configuration-xml"></a>包转换管理器插件配置 XML 的技术参考

适用范围：Configuration Manager (Current Branch)

<!--1357861-->

本文介绍控制包转换管理器插件操作的 Configuration Manager 配置文件 (Microsoft.ConfigurationManagement.exe.config) 中的 XML 元素。 有关如何使用此插件的详细信息，请参阅[如何使用包转换管理器插件](how-to-use-plug-in.md)。



## <a name="xml-configuration-elements"></a>XML 配置元素

下表描述了与包转换管理器插件相关的 Configuration Manager 配置文件中的 XML 元素。

|元素  |类型  |说明  |
|---------|---------|---------|
|**PcmPlugIn**|字符串|要用作包转换管理器插件的脚本或可执行文件的名称。|
|**PcmPlugInTimeoutMilliseconds**|整数|等待包转换管理器插件脚本或可执行文件完成包处理的最大时间（以毫秒计）。|
|**PcmPluginExitCode**|整数|预期的插件进程中的退出代码。 此值表示成功。 所有其他代码均视为错误。|
|**ForceRequirementsExtraction**|布尔值|允许自动转换以使用与包关联的集合要求。 此元素应仅在使用包转换管理器插件（该插件主要用于确定使用哪些要求）时设为 True。|



## <a name="sample-configuration-xml"></a>示例配置 XML

这一部分提供了 Configuration Manager 配置文件 (Microsoft.ConfigurationManagement.exe.config) 中包转换管理器配置 XML 元素的示例。默认情况下，此文件位于以下路径：  
`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

> [!IMPORTANT]
> 自版本 1910 起，此路径已更改为使用 `Microsoft Endpoint Manager` 文件夹。 请确保不使用可能存在于其他文件夹中的旧版文件。 

在示例中，与包转换管理器相关的元素在以下元素中：`Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings`

``` XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
...
    </Microsoft.ConfigurationManagement.AdminConsole.Properties.Settings>
    <Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
      <setting name="DecisionVerbosity" serializeAs="String">
        <value>2</value>
      </setting>
      <setting name="PcmPlugIn" serializeAs="String">
        <value>pcmplugin.vbs</value>
      </setting>
      <setting name="PcmPlugInTimeoutMilliseconds" serializeAs="String">
        <value>10000</value>
      </setting>
      <setting name="PcmPluginExitCode" serializeAs="String">
        <value>0</value>
      </setting>
      <setting name="ForceRequirementsExtraction" serializeAs="String">
        <value>True</value >
      </setting>
    </Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
  </applicationSettings>
...
```

