---
title: 规划 BitLocker 管理
titleSuffix: Configuration Manager
description: 规划如何使用 Configuration Manager 管理 BitLocker 驱动器加密
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a4d8cda2-bc9b-4fb4-aa0d-23c31b4fc60b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 22e78fdba1c004554d671ba2db96c61395f95ca2
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699953"
---
# <a name="plan-for-bitlocker-management"></a>规划 BitLocker 管理

适用范围：Configuration Manager (Current Branch)

<!-- 3601034 -->

从版本 1910 开始，请使用 Configuration Manager 管理已加入 Active Directory 的本地 Windows 客户端的 BitLocker 驱动器加密 (BDE)。 不支持加入 Azure Active Directory 的客户端或工作组客户端。 它提供了可代替 Microsoft BitLocker Administration and Monitoring (MBAM) 的完整 BitLocker 生命周期管理。

> [!NOTE]
> 默认情况下，Configuration Manager 不启用此项可选功能。 必须在使用前启用此功能。 有关详细信息，请参阅[启用更新中的可选功能](../../core/servers/manage/install-in-console-updates.md#bkmk_options)。  

更多详细信息，请参阅 [BitLocker 概述](/windows/security/information-protection/bitlocker/bitlocker-overview)。

> [!TIP]
> 若要使用 Microsoft Endpoint Manager 云服务管理共同管理的 Windows 10 设备上的加密，请将 [Endpoint Protection 工作负载](../../comanage/workloads.md#endpoint-protection)切换为 Intune。 有关使用 Intune 的详细信息，请参阅 [Windows 加密](/intune/protect/endpoint-protection-windows-10#windows-encryption)。

## <a name="features"></a>功能

Configuration Manager 为 BitLocker 驱动器加密提供以下管理功能：

### <a name="client-deployment"></a>客户端部署

将 BitLocker 客户端部署到运行 Windows 10 或 Windows 8.1 的托管 Windows 设备

### <a name="manage-encryption-policies"></a>管理加密策略

- 例如：选择驱动器加密和密码强度，配置用户豁免策略，固定数据驱动器加密设置。

- 确定用于加密设备的算法，以及要加密的磁盘。

- 强制用户在使用设备前遵守新的安全策略。

- 基于每个设备自定义组织的安全配置文件。

- 用户解锁 OS 驱动器时，请指定是仅解锁 OS 驱动器还是所有连接的驱动器。

### <a name="compliance-reports"></a>符合性报表

内置报表含以下内容：

- 每个卷或每个设备的加密状态
- 设备的主要用户
- 符合性状态
- 不符合的原因

### <a name="administration-and-monitoring-website"></a>Administration and monitoring 网站

允许组织中的其他角色在 Configuration Manager 控制台外帮助进行密钥恢复，包括密钥轮换和与 BitLocker 相关的其他支持。 例如，技术支持管理员可以帮助用户进行密钥恢复。

### <a name="user-self-service-portal"></a>用户自助服务门户

允许用户自行使用一次性密钥解锁 BitLocker 加密设备。 使用此密钥后，它会为设备生成新的密钥。

## <a name="prerequisites"></a>必备条件

- 若要创建 BitLocker 管理策略，需要 Configuration Manager 中的“完全权限管理员”角色。

- BitLocker 恢复服务需要 HTTPS 连接才能加密网络中从 Configuration Manager 客户端到管理点的恢复密钥。 共有两个选项：

  - 使用 HTTPS 在托管恢复服务的管理点上启用 IIS 网站。 该选项仅适用于 Configuration Manager 版本 2002。<!-- 5925660 -->

  - 配置 HTTPS 管理点。 该选项适用于 Configuration Manager 版本 1910 或 2002。

  有关详细信息，请参阅[加密恢复数据](../deploy-use/bitlocker/encrypt-recovery-data.md)。

- 虽然 BitLocker 恢复服务安装在使用数据库副本的管理点上，但客户端无法托管恢复密钥。 这样，BitLocker 就不会对驱动器进行加密。 若要使用恢复服务，至少需要一个不在副本配置中的管理点。 在所有使用数据库副本的管理点上，禁用 BitLocker 恢复服务。<!-- 7813149 -->

- 若要使用 BitLocker 管理报表，请安装 Reporting Services 点站点系统角色。 有关详细信息，请参阅[配置报表](../../core/servers/manage/configuring-reporting.md)。

    > [!NOTE]
    > 若要使“恢复审核报表”在 Administration and Monitoring 网站中正常运行，请仅在主站点使用 Reporting Services 点。

- 若要使用自助门户或 Administration and Monitoring 网站，需要运行 IIS 的 Windows 服务器。 可以重用 Configuration Manager 站点系统，或使用连接到站点数据库服务器的独立 web 服务器。 使用[站点系统服务器支持的 OS 版本](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)。

    > [!NOTE]
    > 请仅使用主站点数据库安装自助门户以及管理和监视网站。 在层次结构中，为每个主站点安装这些网站。

- 在将承载自助服务门户的 Web 服务器上，先安装 [Microsoft ASP.NET MVC 4.0](/aspnet/mvc/mvc4) 和 .NET Framework 3.5 功能，然后再开始安装过程。 在门户安装过程中，将自动安装其他必需的 Windows 服务器角色和功能。

- 运行门户安装程序脚本的用户帐户需要站点数据库服务器上的 SQL sysadmin 权限。 在安装过程中，该脚本将设置 Web 服务器计算机帐户的登录名、用户和 SQL 角色权限。 安装自助门户和 Administration and Monitoring 网站后，可以从系统管理员角色中删除此用户帐户。

- 虚拟机 (VM) 或服务器操作系统不支持 BitLocker 管理。 出于此原因，一些功能可能无法在虚拟机或服务器操作系统上按预期运行。 例如，在虚拟机上，BitLocker 管理不会在虚拟机的固定驱动器上启动加密。 虚拟机中的其他固定驱动器可能会显示为“符合”，即使它们未加密，也不例外。

> [!TIP]
> 默认情况下，“启用 BitLocker”任务序列步骤仅加密驱动器上的已用空间。 BitLocker 管理可使用“完整磁盘”加密。 将此任务序列步骤配置为启用“使用完整磁盘加密”选项。 有关详细信息，请参阅[任务序列步骤 - 启用 BitLocker](../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker)。

## <a name="next-steps"></a>后续步骤

[加密恢复数据](../deploy-use/bitlocker/encrypt-recovery-data.md)（首次部署策略之前的可选先决条件）

[部署 BitLocker 管理客户端](../deploy-use/bitlocker/deploy-management-agent.md)