---
title: 支持的站点系统服务器
titleSuffix: Configuration Manager
description: 了解可用来托管 Configuration Manager 站点或站点系统角色的 Windows 版本。
ms.date: 02/19/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17905b4c-3895-4ad4-a69c-5e0d0fc5a8c3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cc58ae7f7b5629319d239f9c48b5c6572fb28116
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691375"
---
# <a name="supported-operating-systems-for-configuration-manager-site-system-servers"></a>Configuration Manager 站点系统服务器支持的操作系统

适用范围：  Configuration Manager (Current Branch)

本文详细介绍了可用于托管 Configuration Manager 站点或站点系统角色的 Windows 版本。

将本文中的信息和以下文章中的信息一起使用：

- [用于 Configuration Manager 的推荐硬件](recommended-hardware.md)
- [用于 Configuration Manager 的站点和站点系统先决条件](site-and-site-system-prerequisites.md)
- [用于 Configuration Manager 的大小和扩展数量](size-and-scale-numbers.md)

## <a name="windows-server-2019"></a><a name="bkmk_2019"></a>Windows Server 2019

*适用于 Windows Server 2019：Standard 和 Datacenter* 

从版本 1810 开始，此 OS 版本支持以下角色：

#### <a name="site-servers"></a>站点服务器

- 管理中心站点  
- 主站点  
- 辅助站点  

#### <a name="site-system-servers"></a>站点系统服务器

- 应用程序目录 Web 服务点  
- 应用程序目录网站点  
- 资产智能同步点  
- 证书注册点  
- 云管理网关连接点  
- 数据仓库服务点  
- 分发点 <sup>[说明 1](#bkmk_note1)</sup>  
- Endpoint Protection 点  
- 注册点  
- 注册代理点  
- 回退状态点  
- 管理点
- Reporting Services 点  
- 服务连接点  
- 站点数据库服务器 <sup>[说明 2](#bkmk_note2)</sup>  
- SMS_Provider  
- 软件更新点  
- 状态迁移点

## <a name="windows-server-2016"></a><a name="bkmk_2016"></a>Windows Server 2016

*适用于 Windows Server 2016：Standard 和 Datacenter*

此 OS 版本支持以下角色：

#### <a name="site-servers"></a>站点服务器

- 管理中心站点  
- 主站点  
- 辅助站点  

#### <a name="site-system-servers"></a>站点系统服务器

- 应用程序目录 Web 服务点  
- 应用程序目录网站点  
- 资产智能同步点  
- 证书注册点  
- 云管理网关连接点  
- 数据仓库服务点  
- 分发点 <sup>[说明 1](#bkmk_note1)</sup>  
- Endpoint Protection 点  
- 注册点  
- 注册代理点  
- 回退状态点  
- 管理点
- Reporting Services 点  
- 服务连接点  
- 站点数据库服务器 <sup>[说明 2](#bkmk_note2)</sup>  
- SMS_Provider  
- 软件更新点  
- 状态迁移点

## <a name="windows-storage-server-2016"></a><a name="bkmk_stor2016"></a> Windows Storage Server 2016

#### <a name="site-system-server"></a>站点系统服务器

- 分发点 <sup>[说明 1](#bkmk_note1)</sup>  

## <a name="windows-server-2012-r2"></a><a name="bkmk_2012r2"></a>Windows Server 2012 R2

*适用于 Windows Server 2012 R2：Standard 和 Datacenter*

#### <a name="site-servers"></a>站点服务器

- 管理中心站点  
- 主站点  
- 辅助站点  

#### <a name="site-system-servers"></a>站点系统服务器

- 应用程序目录 Web 服务点  
- 应用程序目录网站点  
- 资产智能同步点  
- 证书注册点  
- 云管理网关连接点  
- 数据仓库服务点  
- 分发点 <sup>[说明 1](#bkmk_note1)</sup>  
- Endpoint Protection 点  
- 注册点  
- 注册代理点  
- 回退状态点  
- 管理点
- Reporting Services 点  
- 服务连接点  
- 站点数据库服务器 <sup>[说明 2](#bkmk_note2)</sup>  
- SMS_Provider  
- 软件更新点  
- 状态迁移点  

## <a name="windows-server-2012"></a><a name="bkmk_2012"></a>Windows Server 2012  

*适用于 Windows Server 2012：Standard 和 Datacenter*

#### <a name="site-servers"></a>站点服务器

- 管理中心站点  
- 主站点  
- 辅助站点  

#### <a name="site-system-servers"></a>站点系统服务器

- 应用程序目录 Web 服务点  
- 应用程序目录网站点  
- 资产智能同步点  
- 证书注册点  
- 云管理网关连接点  
- 数据仓库服务点  
- 分发点 <sup>[说明 1](#bkmk_note1)</sup>  
- Endpoint Protection 点  
- 注册点  
- 注册代理点  
- 回退状态点  
- 管理点
- Reporting Services 点  
- 服务连接点  
- 站点数据库服务器 <sup>[说明 2](#bkmk_note2)</sup>  
- SMS_Provider  
- 软件更新点  
- 状态迁移点  

## <a name="client-os-versions"></a><a name="bkmk_client"></a>客户端 OS 版本

以下客户端 OS 版本支持用作分发点 <sup>[说明 1](#bkmk_note1)</sup>  ：  

- Windows 10（x86 和 x64）：专业版和企业版

    有关受支持的生成版本的详细信息，请参阅[支持 Windows 10](support-for-windows-10.md)。

- Windows 8.1（x86 和 x64）：Professional 和 Enterprise

此支持存在以下限制：  

- 此 OS 上的分发点不支持使用默认 Windows 部署服务的 PXE 或多播。 从版本 1806 开始，可选择“在没有 Windows 部署服务的情况下启用 PXE 响应程序”选项，通过 PXE 启用此 OS 上的分发点  。 有关详细信息，请参阅[安装和配置分发点](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)。  

## <a name="server-core-installations"></a><a name="bkmk_core"></a>服务器核心安装

支持将以下服务器 OS 版本的服务器核心安装用作一个分发点  ：

- Windows Server 2019（从 Configuration Manager 版本 1810 开始）  
- Windows Server 版本 1809（从 Configuration Manager 版本 1810 开始）  
- Windows Server 版本 1803（从 Configuration Manager 版本 1802 开始）  
- Windows Server 版本 1709（从 Configuration Manager 版本 1710 开始）  
- Windows Server 2016  
- Windows Server 2012 R2  
- Windows Server 2012  

此支持存在以下限制：  

- 此 OS 上的分发点不支持使用默认 Windows 部署服务的 PXE 或多播。 从版本 1806 开始，可选择“在没有 Windows 部署服务的情况下启用 PXE 响应程序”选项，通过 PXE 启用此 OS 上的分发点  。 有关详细信息，请参阅[安装和配置分发点](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe)。  

## <a name="general-notes"></a>一般注释

### <a name="note-1-distribution-points"></a><a name="bkmk_note1"></a> 注释 1：分发点

分发点支持多种不同的配置，每种配置都有不同的要求。 在某些情况下，这些配置不仅支持在服务器上安装，而且支持在客户端操作系统上安装。 有关详细信息，请参阅[管理内容和内容基础结构](../../servers/deploy/configure/manage-content-and-content-infrastructure.md)。  

### <a name="note-2-site-database-servers"></a><a name="bkmk_note2"></a> 注释 2：站点数据库服务器

只读域控制器 (RODC) 上不支持站点数据库服务器。 有关详细信息，请参阅“Microsoft 支持”文章：[在域控制器上安装 SQL Server 时可能遇到问题](https://support.microsoft.com/help/2032911)。 

此外，任何域控制器上都不支持辅助站点服务器。  
