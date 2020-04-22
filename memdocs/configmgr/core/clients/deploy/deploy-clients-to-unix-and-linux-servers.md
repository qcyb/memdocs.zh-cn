---
title: 部署 Unix/Linux 客户端
titleSuffix: Configuration Manager
description: 了解如何在 Configuration Manager 中将客户端部署到 UNIX 或 Linux 服务器。
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15a4e323-9f42-4fea-bb14-f2b905d1f77c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4375867e70cb7f2989b78572c7fc8e005f95be73
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694035"
---
# <a name="how-to-deploy-clients-to-unix-and-linux-servers-in-configuration-manager"></a>如何在 Configuration Manager 中将客户端部署到 UNIX 和 Linux 服务器

适用范围：  Configuration Manager (Current Branch)

> [!Important]  
> 从版本 1902 开始，Configuration Manager 不支持 Linux 或 UNIX 客户端。 
> 
> 请考虑使用 Microsoft Azure 管理来管理 Linux 服务器。 Azure 解决方案具有广泛的 Linux 支持（包括面向 Linux 的端到端补丁管理），在大多数情况下优于 Configuration Manager 的功能。


在可以用 Configuration Manager 管理 Linux 或 UNIX 服务器之前，必须在每个 Linux 或 UNIX 服务器上安装适用于 Linux 和 UNIX 的 Configuration Manager 客户端。 可以在每台计算机上手动完成客户端安装，或远程使用安装客户端的 shell 脚本。 Configuration Manager 不支持对 Linux 或 UNIX 服务器使用客户端请求安装。 （可选）你可以为 System Center orchestrator 配置 Runbook 来自动执行 Linux 或 UNIX 服务器上的客户端安装。  

 无论你使用何种安装方法，在安装过程要求使用名为 **install** 的脚本来管理安装过程。 此脚本时，包含您下载适用于 Linux 和 UNIX 的客户端。  

 适用于 Linux 和 UNIX 的 Configuration Manager 客户端的安装脚本支持命令行属性。 某些命令行属性是必需的，其他一些则是可选的。 例如，在安装客户端时，您必须指定由其与该站点的初始联系 Linux 或 UNIX 服务器的站点中的管理点。 有关命令行属性的完整列表，请参阅[在 Linux 和 UNIX 服务器上安装客户端的命令行属性](#BKMK_CmdLineInstallLnUClient)。  

 安装客户端后，在 Configuration Manager 控制台指定客户端设置，从而用和配置基于 Windows 的客户端相同的方式配置客户端代理。 有关详细信息，请参阅  [Linux 和 UNIX 服务器的客户端设置](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ClientSettingsforLnU)。  

##  <a name="about-client-installation-packages-and-the-universal-agent"></a><a name="BKMK_AboutInstallPackages"></a>有关客户端安装包和通用代理  
 若要在特定平台上安装适用于 Linux 和 UNIX 的客户端，你必须对要安装客户端的计算机使用合适的客户端安装包。 合适的客户端安装包是从 [Microsoft 下载中心](https://go.microsoft.com/fwlink/?LinkID=525184)下载的每个客户端的一部分。 除了客户端安装包，客户端下载内容还包括在每台计算机上管理客户端安装的 **install** 脚本。  

 在安装客户端时，无论使用何种客户端安装包，都可以使用相同的过程和命令行属性。  

 有关适用于 Linux 和 UNIX 的每个版本的 Configuration Manager 客户端支持的操作系统、平台和客户端安装包的详细信息，请参阅 [Linux 和 UNIX 服务器](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#linux-and-unix-servers)。  

##  <a name="install-the-client-on-linux-and-unix-servers"></a><a name="BKMK_InstallLnUClient"></a>在 Linux 和 UNIX 服务器上安装客户端  
 若要安装适用于 Linux 和 UNIX 的客户端，请在每个 Linux 或 UNIX 的计算机上运行脚本。 该脚本名为 install  ，它支持修改安装行为和引用客户端安装包的命令行属性。 安装脚本和客户端安装包必须位于客户端上。 客户端安装程序包中包含针对特定 Linux 或 UNIX 的操作系统和平台的 Configuration Manager 客户端文件。
每个客户端安装包都包含完成客户端安装必需的所有文件，且与 Windows 计算机不同的是，不会从管理点或其他源位置下载其他文件。  

 安装适用于 Linux 和 UNIX 的 Configuration Manager 客户端后，不需要重新启动计算机。 一旦软件安装完成后，客户端所操作。 如果重新启动计算机，Configuration Manager 客户端将自动重新启动。  

 使用根凭据运行安装的客户端。 收集硬件清单和执行软件部署需要根凭据。  

 请使用以下命令格式：  

 `./install -mp <computer> -sitecode <sitecode> <property #1> <property #2> <client installation package>`  

-   `install` 是安装适用于 Linux 和 UNIX 的客户端的脚本文件的名称。 此文件提供的客户端软件。  

-   `-mp <computer>` 指定客户端使用的初始管理点。 示例：`smsmp.contoso.com`  

-   `-sitecode <site code>` 指定将客户端分配到的目标站点代码。 示例：`S01`  

-   `<property #1> <property #2>` 指定要与安装脚本搭配使用的命令行属性。  

    > [!NOTE]  
    >  有关详细信息，请参阅[在 Linux 和 UNIX 服务器上安装客户端的命令行属性](#BKMK_CmdLineInstallLnUClient)。  

-   **客户端安装包** 是此计算机的操作系统、版本和 CPU 体系结构的客户端安装 .tar 包的名称。 必须最后指定客户端安装.tar 文件。 示例：`ccm-Universal-x64.<build>.tar`  

###  <a name="to-install-the-configuration-manager-client-on-linux-and-unix-servers"></a><a name="BKMK_ToInstallLnUClinent"></a>在 Linux 和 UNIX 服务器上安装 Configuration Manager 客户端  

1.  在 Windows 计算机上，为你想要管理的 [Linux 或 UNIX 服务器下载合适的客户端文件](https://go.microsoft.com/fwlink/?LinkID=525184) 。  

2.  在 Window 计算机上运行自解压 .exe 文件以提取安装脚本和客户端安装 .tar 文件。  

3.  复制 **安装** 脚本和 .tar 文件到你想要管理的服务器上的文件夹。  

4.  在 UNIX 或 Linux 服务器上，运行以下命令以启用要作为程序运行的脚本：`chmod +x install`  

    > [!IMPORTANT]  
    >  您必须使用根凭据来安装客户端。  

5.  接下来，运行以下命令以安装 Configuration Manager 客户端：`./install -mp <hostname> -sitecode <code> ccm-Universal-x64.<build>.tar`  

     当进入此命令时，使用您所需要的其他命令行属性。 有关命令行属性的列表，请参阅[在 Linux 和 UNIX 服务器上安装客户端的命令行属性](#BKMK_CmdLineInstallLnUClient)  

6.  脚本运行后，通过查看“/var/opt/microsoft/scxcm.log”  文件验证安装 。 此外，可以通过在 Configuration Manager 控制台中“资产和符合性”  工作区的“设备”  节点中查看客户端的详细信息，确认客户端是否已安装并与站点通信。  

###  <a name="command-line-properties-for-installing-the-client-on-linux-and-unix-servers"></a><a name="BKMK_CmdLineInstallLnUClient"></a>在 Linux 和 UNIX 服务器上安装客户端的命令行属性  
 以下属性可用于修改安装脚本的行为：  

> [!NOTE]  
>  使用属性 `-h` 来显示受支持的此属性列表。  

-   `-mp <server FQDN>`  

     必需。 由 FQDN 指定，客户端用作初始联系点的管理点服务器。  

    > [!IMPORTANT]  
    >  此属性不会指定安装后将客户端分配到的目标管理点。  

    > [!NOTE]  
    >  使用 `-mp` 属性来指定配置为只接受 HTTPS 客户端连接的管理点时，还必须使用 `-UsePKICert` 属性。  

-   `-sitecode <sitecode>`  

     必需。 指定要将 Configuration Manager 客户端分配到的 Configuration Manager 主站点。 示例：`-sitecode S01`  

-   `-fsp <server_FQDN>`  

     可选。 指定通过 FQDN，客户端用于提交状态消息的回退状态点服务器。 有关详细信息，请参阅[确定是否需要回退状态点](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point)。  

-   `-dir <directory>`  

     可选。 指定替代位置以安装 Configuration Manager 客户端文件。 默认情况下，客户端安装到以下位置：`/opt/microsoft`  

-   `-nostart`  

     可选。 客户端安装完成后，阻止自动启动 Configuration Manager 客户端服务 **ccmexec.bin**。  

     在客户端安装后，您必须手动启动客户端服务。  

     默认情况下，客户端服务启动后客户端安装完成后，每次在计算机重新启动。  

-   `-clean`  

     可选。 在新的安装开始之前指定适用于 Linux 和 UNIX 的所有客户端文件和来自以前安装的客户端数据删除。 此操作会删除客户端的数据库和证书存储。  

-   `-keepdb`  

     可选。 指定保留本地客户端数据库，并在重新安装客户端时重复使用。 默认情况下，当你重新安装客户端将删除此数据库。  

-   `-UsePKICert <parameter>`  

     可选。 公钥证书标准 (PKCS #12) 格式指定完整路径和文件名为 X.509 PKI 证书的名称。 此证书用于客户端身份验证。 如果在安装过程中未指定证书，则你需要添加或更改证书，请使用 **certutil** 实用工具。 有关详细信息，请参阅[如何管理适用于 Linux 和 UNIX 的客户端上的证书](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts)。  

     使用 `-UsePKICert` 时，还必须使用 `-certpw` 命令行参数来提供与 PKCS#12 文件关联的密码。  

     如果未使用此属性指定 PKI 证书，客户端将使用自签名证书，并且与站点系统的所有通信均通过 HTTP 进行。  

     如果您在上指定了无效的证书客户端安装命令行，会返回任何错误。 客户端安装完成后会进行证书验证。 客户端启动时，将使用管理点对证书进行验证。 如果证书未通过验证，scxcm.log  中将显示以下消息：“管理点证书未通过验证”  。 默认的日志文件位置是：  **/var/opt/microsoft/scxcm.log**。  

     > [!NOTE]  
     > 安装客户端时，必须指定此属性并使用 `-mp` 属性指定配置为仅接受 HTTPS 客户端连接的管理点。  

     示例：`-UsePKICert <full path and filename> -certpw <password>`  

-   `-certpw <parameter>`  

     可选。 指定与通过 `-UsePKICert` 属性指定的 PKCS #12 文件相关联的密码。  

     示例：`-UsePKICert <full path and filename> -certpw <password>`  

-   `-NoCRLCheck`  

     可选。 指定客户端在使用 PKI 证书通过 HTTPS 进行通信时应不检查证书吊销列表 (CRL)。 如果未指定此选项，客户端将在使用 PKI 证书建立 HTTPS 连接之前检查 CRL。 有关客户端 CRL 检查的详细信息，请参阅 PKI 证书吊销的规划。  

     示例：`-UsePKICert <full path and filename> -certpw <password> -NoCRLCheck`  

-   `-rootkeypath <file location>`  

     可选。 指定 Configuration Manager 受信任的根密钥的完整路径和文件名。 Configuration Manager 受信任的根密钥提供一种机制，Linux 和 UNIX 客户端使用此机制来确认它们已连接到属于正确的层次结构的站点系统。  

     如果未在命令行上指定受信任的根密钥，客户端将信任其与之通信的第一个管理点，并将从该管理点自动检索受信任的根密钥。  

     有关详细信息，请参阅  [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)。  

     示例：`-rootkeypath <full path and filename>`  

-   `-httpport <port>`  

     可选。 指定在客户端在通过 HTTP 与管理点通信时所使用的管理点配置的端口。 如果未指定端口，将使用默认值 80。  

     示例：`-httpport 80`  

-   `-httpsport <port>`  

     可选。 指定在客户端在通过 HTTPS 与管理点通信时所使用的管理点配置的端口。 如果未指定端口，将使用默认值 443。  

     示例：`-UsePKICert <full path and certificate name> -httpsport 443`  

-   `-ignoreSHA256validation`  

     可选。 指定客户端安装将 SHA 256 验证跳过。 如果在发布时未随附支持 SHA-256 的 OpenSSL 版本的操作系统上安装客户端，请使用此选项。 有关详细信息，请参阅[关于不支持 SHA-256 的 Linux 和 UNIX 的操作系统](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256)。  

-   `-signcertpath <file location>`  

     可选。 指定的完整路径和 **.cer** 的站点服务器上的导出自签名证书的文件名。 如果 PKI 证书不可用，Configuration Manager 站点服务器将自动生成自签名证书。  

     这些证书用于验证从管理点下载的客户端策略发送从预期的站点。 如果在安装过程中未指定证书，或者你需要更改证书，请使用 **certutil** 实用工具。 有关详细信息，请参阅[如何管理适用于 Linux 和 UNIX 的客户端上的证书](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts)。  

     此证书可通过 **SMS** 证书存储检索，并且具有“站点服务器”  使用者名称以及“站点服务器签名证书”  友好名称。  

     如果安装期间未指定此选项，Linux 和 UNIX 客户端将信任与之通信的第一个管理点。 它们会自动从该管理点检索签名证书。  

     示例：`-signcertpath <full path and file name>`  

-   `-rootcerts`  

     可选。 指定要导入且不是管理点证书颁发机构 (CA) 层次结构的一部分的其他 PKI 证书。 如果在命令行中指定多个证书，它们应该是以逗号分隔。  

     如果使用的 PKI 客户端证书未链接至站点管理点信任的根 CA 证书，请使用此选项。 如果客户端证书未链接到站点的证书颁发者列表中的受信任根证书，管理点将拒绝此客户端。  

     如果不使用此选项，Linux 和 UNIX 客户端将仅使用 `-UsePKICert` 选项中的证书验证信任层次结构。  

     示例：`-rootcerts <full path and file name>,<full path and file name>`  

###  <a name="uninstalling-the-client-from-linux-and-unix-servers"></a><a name="BKMK_UninstallLnUClient"></a>从 Linux 和 UNIX 服务器卸载客户端  
 若要卸载适用于 Linux 和 UNIX 的 Configuration Manager 客户端，请使用卸载实用工具 **uninstall**。 默认情况下，此文件位于 **/选择/microsoft/configmgr/bin/** 客户端计算机上的文件夹。 此卸载命令不支持任何命令行参数，并且将从服务器删除与客户端软件相关的所有文件。  

 若要卸载客户端，请使用下面的命令行: **/opt/microsoft/configmgr/bin/uninstall**  

 卸载适用于 Linux 和 UNIX 的 Configuration Manager 客户端后，无需重新启动计算机。  

##  <a name="configure-request-ports-for-the-client-for-linux-and-unix"></a><a name="BKMK_ConfigLnUClientCommuincations"></a> 适用于 Linux 和 UNIX 客户端配置请求端口  
 与基于 Windows 的客户端类似，适用于 Linux 和 UNIX 的 Configuration Manager 客户端使用 HTTP 和 HTTPS 与 Configuration Manager 站点系统通信。 Configuration Manager 客户端用于通信的端口称为请求端口。  

 当你安装适用于 Linux 和 UNIX 的 Configuration Manager 客户端时，你可以通过指定 **-httpport** 和 **-httpsport** 安装属性更改客户端默认请求端口 。 如果未指定安装属性和自定义值，客户端将使用默认值。 默认值为 **80** 对于 HTTP 流量和 **443** HTTPS 通信。  

 安装客户端后，不能更改其请求端口配置。 相反，若要更改端口配置必须重新安装客户端并指定新的端口配置。 当你重新安装客户端以更改请求端口号时，运行类似于新客户端安装的 install  命令，但使用额外命令行属性 -keepdb  。 此开关将指示安装保留客户端数据库和文件，包括客户端 GUID 和证书存储。  

 有关客户端通信端口号的详细信息，请参阅[如何配置客户端通信端口](../../../core/clients/deploy/configure-client-communication-ports.md)。  

##  <a name="configure-the-client-for-linux-and-unix-to-locate-management-points"></a><a name="BKMK_ConfigClientMP"></a> 配置客户端适用于 Linux 和 UNIX 来查找管理点  
 在安装适用于 Linux 和 UNIX 的 Configuration Manager 客户端时，必须指定用作初始联系点的管理点。  

 适用于 Linux 和 UNIX 的 Configuration Manager 客户端将在客户端安装时联系此管理点。 如果客户端无法联系管理点，客户端软件将不断重试直到成功。  

 有关客户端如何查找管理点的详细信息，请参阅 [定位管理点](assign-clients-to-a-site.md#locating-management-points)。
