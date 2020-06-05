---
title: 在 Microsoft Intune 中添加适用于 Windows 10 设备的自定义设置 - Azure | Microsoft Docs
description: 在 Microsoft Intune 中为运行 Windows 10 的设备添加或创建自定义配置文件，以使用 OMA-URI 设置。 使用自定义配置文件添加自定义设置。
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 96074f4bea22b7468b1f210d631f0912eeafe7b5
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2020
ms.locfileid: "83428991"
---
# <a name="use-custom-settings-for-windows-10-devices-in-intune"></a>在 Intune 中使用适用于 Windows 10 设备的自定义设置

本文列出并介绍了可以在 Windows 10 和更高版本设备上控制的所有不同的自定义设置。 作为移动设备管理 (MDM) 解决方案的一部分，请使用这些设置配置未在 Intune 中内置的设置。

有关自定义配置文件的详细信息，请参阅[使用自定义设置创建配置文件](custom-settings-configure.md)。

这些设置将添加到 Intune 中的设备配置配置文件中，然后分配或部署到 Windows 10 设备。

此功能适用于：

- Windows 10 及更高版本

Windows 10 自定义配置文件使用开放移动联盟统一资源标识符 (OMA-URI) 设置配置不同的功能。 移动设备制造商通常使用这些设置来控制设备上的功能。

Windows 10 提供了许多配置服务提供程序 (CSP) 设置，例如，[策略配置服务提供程序（策略 CSP）](https://technet.microsoft.com/itpro/windows/manage/how-it-pros-can-use-configuration-service-providers)。

如果正在寻找特定设置，请记住 [Windows 10 设备限制配置文件](device-restrictions-windows-10.md)包含许多内置设置。 因此，可能不需要输入自定义值。

## <a name="before-you-begin"></a>在开始之前

[创建 Windows 10 自定义配置文件](custom-settings-configure.md#create-the-profile)。

## <a name="oma-uri-settings"></a>OMA-URI 设置

**添加**：输入以下设置：

- **名称**：输入 OMA-URI 设置的唯一名称，以帮助你在设置列表中识别它。
- **描述**：输入包含设置概述以及其他所有重要详细信息的说明。
- **OMA-URI**（区分大小写）：输入要用作设置的 OMA-URI。
- **数据类型**：选择用于此 OMA-URI 设置的数据类型。 选项包括：

  - Base64（文件）
  - 布尔值
  - 字符串（XML 文件）
  - 日期和时间
  - 字符串
  - 浮点
  - 整数

- **值**：输入要与已输入的 OMA-URI 关联的数据值。 值取决于所选的数据类型。 例如，如果选择了“日期和时间”，则从日期选取器中选择值。

添加一些设置后，可以选择“导出”。 “导出”将创建逗号分隔值 (.csv) 文件中添加的所有值的列表。

## <a name="find-the-policies-you-can-configure"></a>查找可以配置的策略

可以在[配置服务提供程序参考](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference)中找到 Windows 10 支持的所有配置服务提供程序 (CSP) 的完整列表。

并非所有设置均兼容所有 Windows 10 版本。 [配置服务提供程序参考](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference)中介绍每个 CSP 所支持的版本。

此外，Intune 并不支持[配置服务提供程序参考](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference)中列出的所有设置。 若要查明 Intune 是否支持所需的设置，请打开针对该设置的文章。 每个设置页面都将显示其支持的操作。 若要使用 Intune，设置必须支持“添加”、“替换”和“获取”操作  。 如果“Get”操作返回的值与“添加”或“替换”操作提供的值不匹配，则 Intune 报告符合性错误  。

## <a name="next-steps"></a>后续步骤

[分配配置文件](device-profile-assign.md)并[监视其状态](device-profile-monitor.md)。

[详细了解 Intune 中的自定义配置文件](custom-settings-configure.md)。
