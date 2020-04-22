---
title: 防病毒排除
titleSuffix: Configuration Manager
description: 了解在排查可能的问题时建议使用的防病毒排除。
ms.date: 10/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb470e3-6f6b-4ccf-b3d8-1598d79d3490
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: df951bfb44313cfec8dacb8c0df34abb7beb0c56
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703735"
---
# <a name="recommended-antivirus-exclusions-for-configuration-manager"></a>建议为 Configuration Manager 使用的防病毒排除

适用范围：  Configuration Manager (Current Branch)

本文包含的建议可帮助管理员确定运行受支持版本的 Configuration Manager 站点服务器、站点系统和客户端的计算机与防病毒软件一起使用时存在潜在的不稳定性的原因。

> [!IMPORTANT]
>
> - 我们建议你暂时应用这些过程来评估系统。 如果你的系统性能或稳定性通过本文所述的建议来改进，请与防病毒软件供应商联系以获取说明或更新版本的防病毒软件。
> - 本文包含的信息说明如何帮助降低安全设置或如何在计算机上暂时关闭安全功能。 可以进行这些更改来了解特定问题的性质。 在进行这些更改之前，我们建议你在特定环境中评估与实现此解决方法相关联的风险。

## <a name="possible-symptoms"></a>可能出现的症状 

防病毒实时保护会导致 Configuration Manager 站点服务器、站点系统和客户端上出现许多问题。

下面是一个不完整的可能症状列表：

- 未安装远程站点系统组件。 SiteComp.log、Distmgr.log、hman.log 或其他 Configuration Manager 日志文件可能包含错误 80070005 等错误。
- 不能使用客户端请求安装 Configuration Manager 客户端。
- 客户端清单信息不准确、丢失或过期。
- 积压工作发生在 Install_Directory\Program Files\Microsoft Configuration Manager\Inboxes 文件夹中  。
- 软件中心未通过客户端系统上部署的软件进行填充，或未启动。 此外，CCMRepair.log 文件可能包含类似于以下示例的错误：

  > 数据库验证失败，结果为：0x80004005，但 DB：C:\Windows\CCM\filename.sdf 可以打开，跳过 DB 修复。

- 无法安装部署到客户端的软件。
- 软件部署的符合性数据不准确。

## <a name="exclusions"></a>排除项

若要避免此类问题，我们建议你添加以下实时保护排除：

### <a name="default-installation-folders"></a>默认安装文件夹

|  |  |
| - | - |
|*ConfigMgr Installation Folder*  |  %ProgramFiles%\Microsoft Configuration Manager  |  
|*MP Installation Folder*  |%ProgramFiles%\SMS_CCM  |  
|*Client Installation Folder*  |%Windir%\CCM  |  

### <a name="folder-exclusions-for-site-servers"></a>站点服务器的文件夹排除

- *ConfigMgr Installation Folder*\Inboxes
- *ConfigMgr Installation Folder*\Logs
- *ConfigMgr Installation Folder*\EasySetupPayload

### <a name="folder-exclusions-for-site-systems"></a>站点系统的文件夹排除

- 管理点
  - *MP installation folder*\ServiceData
  - 以下任何一项：
    - *ConfigMgr installation folder*\MP\OUTBOXES
    - *Installation drive*\SMS\MP\OUTBOXES
- 分发点
  - *Client installation folder*\ServiceData
  - *ContentLib_Drive*\SMS_DP$
  - *ContentLib_Drive*\SMSPKG*Drive_Letter*$
  - *ContentLib_Drive*\SMSPKG
  - *ContentLib_Drive*\SMSPKGSIG
  - *ContentLib_Drive*\SMSSIG$
- 站点数据库服务器
  - [如何选择要在运行 SQL Server 的计算机上运行的防病毒软件](https://support.microsoft.com/en-us/help/309422)

### <a name="folder-exclusions-for-clients"></a>客户端的文件夹排除

- *Client Installation Folder*\\\*.sdf
- *Client Installation Folder*\ServiceData
- C:\Windows\CCMCache
- C:\Windows\CCMSetup
- *Client Installation Folder*\Logs

### <a name="file-exclusions-for-mps"></a>MP 的文件排除

- POL00000.pol（在
  - *MP Installation Folder*\PolReqStaging 中）

### <a name="process-exclusions"></a>进程排除

仅当激进的防病毒程序将 Configuration Manager 程序文件（.exe 文件）视为高风险进程时，才需要执行进程排除。

- *ConfigMgr Installation Folder*\bin\64\Smsexec.exe
- 以下任何一个进程：
  - *Client Installation Folder*\Ccmexec.exe
  - *MP Installation Folder*\Ccmexec.exe
- *Client Installation Folder*\CmRcService.exe（客户端）
- *ConfigMgr Installation Folder*\bin\64\Sitecomp.exe
- *ConfigMgr Installation Folder*\bin\64\Smswriter.exe
- *ConfigMgr Installation Folder*\bin\64\Smssqlbkup.exe 或 SMS_*SQLFQDN*\bin\x64\Smssqlbkup.exe
- *ConfigMgr Installation Folder*\bin\64\Cmupdate.exe
- *Client Installation Folder*\Ccmrepair.exe（客户端）
- %*windir*%\CCMSetup\Ccmsetup.exe（客户端）

## <a name="next-steps"></a>后续步骤

有关防病毒排除的详细信息，请参阅以下文章：

[Configuration Manager Current Branch 防病毒排除 - System Center 顶级现场工程师博客](https://blogs.technet.microsoft.com/systemcenterpfe/2017/05/24/configuration-manager-current-branch-antivirus-update/)

[更新了 System Center 2012 Configuration Manager 防病毒排除以及有关 OSD 和启动映像的更多详细信息](https://blogs.technet.microsoft.com/systemcenterpfe/2013/01/11/updated-system-center-2012-configuration-manager-antivirus-exclusions-with-more-details-on-osd-and-boot-images-etc/)

[如何选择要在运行 SQL Server 的计算机上运行的防病毒软件](https://support.microsoft.com/en-us/help/309422/how-to-choose-antivirus-software-to-run-on-computers-that-are-running-sql-server)

[针对运行当前支持的 Windows 版本的企业计算机的病毒扫描建议](https://support.microsoft.com/en-us/help/822158/virus-scanning-recommendations-for-enterprise-computers-that-are-running-currently-supported-versions-of-windows)
