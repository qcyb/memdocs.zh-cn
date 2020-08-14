---
title: 对 macOS 设备使用直接注册
titleSuffix: Microsoft Intune
description: 了解如何使用直接注册方式注册 macOS 设备。
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/04/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: scottbreenmsft
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1f12b90dd49dc9a9783a39fb78d74c40c6838b1e
ms.sourcegitcommit: c1afc8abd0d7da48815bd2b0e45147774c72c2df
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/05/2020
ms.locfileid: "87819961"
---
# <a name="use-direct-enrollment-for-macos-devices"></a>对 macOS 设备使用直接注册

Intune 支持对企业设备使用直接注册 (DE) 注册 macOS 设备。 直接注册不会擦除设备。 它通过 macOS 设置注册设备。 此方法适仅支持“无用户关联”的设备。

## <a name="prerequisites"></a>先决条件

- 具有 macOS 设备的物理访问权限
- [设置 MDM 机构](../fundamentals/mdm-authority-set.md)
- [Apple MDM Push Certificate](apple-mdm-push-certificate-get.md)
 - 具有要注册的 macOS 设备的管理员权限

## <a name="create-an-apple-configurator-profile-for-devices"></a>为设备创建 Apple Configurator 配置文件

设备注册配置文件定义在注册期间应用的设置。 这些设置只应用一次。 按照以下步骤创建注册配置文件，以使用直接注册方式注册 macOS 设备。

1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“设备” > “注册设备” > “Apple 注册” > “Apple 配置器”   。

2.  选择“配置文件” > “创建”。

3. 在“创建注册配置文件”下，输入配置文件的“名称”和“描述”，以便于管理  。 用户看不到这些详细信息。 可使用此“名称”字段在 Azure Active Directory 中创建动态组。 使用配置文件名称定义 enrollmentProfileName 参数，以向设备分配此注册配置文件。 详细了解 Azure Active Directory 动态组。

4. 对于“用户关联”，选择“不通过用户关联进行注册”- 为不属于单个用户的设备选择此选项 。 为无需访问本地用户数据即可执行任务的设备使用此选项。 需要用户隶属关系的应用（包括用于安装业务线应用的公司门户应用）无法运行。 直接注册需要设置此选项。

     > [!NOTE]
     > 使用直接注册时，macOS 不支持“通过用户关联进行注册”。 对于要求用户关联的设备，请使用自动设备注册。

6. 选择“创建”保存该配置文件。

## <a name="direct-enrollment"></a>“直接注册”
因为直接注册只支持不通过用户关联进行注册，所以不能使用公司门户安装可用的应用程序。

### <a name="export-the-profile-and-install-on-macos-devices"></a>导出配置文件并在 macOS 设备上安装

1. 在 [Microsoft Endpoint Manager 管理中心](https://go.microsoft.com/fwlink/?linkid=2109431)中，选择“设备” > “注册设备” > “Apple 注册” > “Apple 配置器” > “配置文件”> 选择要导出的配置文件 >“导出配置文件”     。
2. 在“直接许可登记表”下，选择“下载配置文件”并保存此文件。  

     > [!NOTE]
     > 下载的注册配置文件在下载后两周内有效。 你可使用此链接根据你的需要下载注册配置文件。 下载新的配置文件并不会导致前一个配置文件无效，但也不会延长之前下载的文件到期时间。
         
3. 将该文件传输到 macOS 计算机以直接安装它。
4. 双击保存的“.mobileconfig”以在配置文件中打开该文件。
5. 系统提示安装管理配置文件时，请选择“安装”。
6. 选择“安装”后，在下一次提示时确认要安装管理配置文件。
7. 在 macOS 设备上输入管理员帐户的凭据，然后单击“确定”。
8. macOS 设备现已注册到 Intune 中，托管的目标配置文件将开始下载。

## <a name="next-steps"></a>后续步骤

注册 macOS 设备后，可以开始[对其进行管理](../remote-actions/device-management.md)。