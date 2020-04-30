---
title: 加密恢复数据
titleSuffix: Configuration Manager
description: 在网络和 Configuration Manager 数据库中加密 BitLocker 恢复密钥、恢复包和 TPM 密码哈希。
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 1ee6541a-e243-43ea-be16-d0349f7f0c6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79f50cf4b0d241df2fc8d12dc46c833af278bd5a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709345"
---
# <a name="encrypt-recovery-data"></a>加密恢复数据

适用范围：  Configuration Manager (Current Branch)

<!--3601034-->

创建 BitLocker 管理策略时，Configuration Manager 会将恢复服务部署到管理点。 在 BitLocker 管理策略的“客户端管理”页上，客户端会在你配置 BitLocker 管理服务时将密钥恢复信息备份到站点数据库   。 此信息包括 BitLocker 恢复密钥、恢复包和 TPM 密码哈希。 用户被锁定导致用户无法访问其受保护设备时，你可以使用此信息来帮助他们恢复对设备的访问。

鉴于此信息的敏感性，需要在以下情况下对其进行保护：

- Configuration Manager 需要在客户端与恢复服务之间建立 HTTPS 连接，用于加密网络中传输的数据。 共有两个选项：

  - 使用 HTTPS 在托管恢复服务的管理点上（而不是在整个管理点角色上）启用 IIS 网站。 该选项仅适用于 Configuration Manager 版本 2002。<!-- 5925660 -->

  - 配置 HTTPS 管理点。 在管理点的属性中，“客户端连接”设置必须是 HTTPS   。 该选项适用于 Configuration Manager 版本 1910 或 2002。

    > [!NOTE]
    > 目前不支持增强型 HTTP。

- 在将数据存储在站点数据库中时，还可以考虑加密此数据。 你可以使用自己的证书和 SQL Server 单元级加密。

    如果不希望创建 BitLocker 管理加密证书，请选择加入恢复数据的纯文本存储。 创建 BitLocker 管理策略时，请启用“允许以纯文本格式存储恢复信息”选项  。

    > [!NOTE]
    > 另一个安全层是加密整个站点数据库。 如果在数据库上启用了加密，则 Configuration Manager 中没有任何功能问题。
    >
    > 请谨慎加密，尤其是在大型环境中。 根据所加密的表以及 SQL 的版本，你可能会注意到性能下降高达 25%。 更新备份和恢复计划，以便成功恢复加密数据。

## <a name="certificate-requirements"></a>证书要求

### <a name="https-server-authentication-certificate"></a>HTTPS 服务器身份验证证书

<!--5925660-->

在 Configuration Manager 当前分支版本 1910 中，要集成 BitLocker 恢复服务，需要使用 HTTPS 启用管理点。 需要 HTTPS 连接才能加密网络中从 Configuration Manager 客户端到管理点的恢复密钥。 对于许多客户而言，为 HTTPS 配置管理点和所有客户端可能比较困难。

从版本 2002 开始，只有托管恢复服务的 IIS 网站才需要满足 HTTPS 要求，而不是整个管理点角色都需要满足。 此更改放宽了证书要求，并且仍会加密传输中的恢复密钥。

现在，管理点的“客户端连接”属性可以是“HTTP”或“HTTPS”    。 如果为 HTTP 配置了管理点，那么要支持 BitLocker 恢复服务，请执行以下操作  ：

1. 获取服务器身份验证证书。 将证书绑定到托管 BitLocker 恢复服务的管理点上的 IIS 网站。

2. 将客户端配置为信任服务器身份验证证书。 有两种方法可实现此信任：

    - 使用公共和全局受信任的证书提供程序提供的证书。 例如（但不限于）DigiCert、Thawte 或 VeriSign。 Windows 客户端包括来自这些提供程序的受信任的根证书颁发机构 (CA)。 通过使用其中一个提供程序发布的服务器身份验证证书，客户端会自动信任该证书。

    - 使用组织的公钥基础结构 (PKI) 中 CA 颁发的证书。 大多数 PKI 实现会向 Windows 客户端添加受信任的根 CA。 例如，在组策略中使用 Active Directory 证书服务。 如果从客户端不自动信任的 CA 颁发服务器身份验证证书，请将 CA 受信任的根证书添加到客户端。

> [!TIP]
> 唯一需要与恢复服务进行通信的客户端是计划作为 BitLocker 管理策略的目标且包括客户端管理规则的客户端  。

在客户端上，使用 BitLockerManagementHandler.log 对此连接进行故障排除  。 对于与恢复服务的连接，该日志显示客户端正在使用的 URL。 找到以 `Checking for Recovery Service at` 开头的条目。

> [!NOTE]
> 如果站点有多个管理点，请对该站点中可能与 BitLocker 托管客户端通信的所有管理点启用 HTTPS。 如果 HTTPS 管理点不可用，客户端可能会故障转移到某个 HTTP 管理点，然后在托管其恢复密钥时会失败。
>
> 此建议适用于这两个选项：为 HTTPS 启用管理点，或启用在管理点上托管恢复服务的 IIS 网站。

### <a name="sql-encryption-certificate"></a>SQL 加密证书

使用此证书启用 BitLocker 恢复数据的 SQL Server 单元级加密。 可以按自己的流程创建和部署 BitLocker 管理加密证书，前提是它满足以下要求：

- BitLocker 管理加密证书的名称必须是 `BitLockerManagement_CERT`。

- 使用数据库主密钥加密此证书。

- 以下 SQL 用户需要证书的“控制”权限  ：
  - RecoveryAndHardwareCore
  - RecoveryAndHardwareRead
  - RecoveryAndHardwareWrite

- 在层次结构中的每个站点数据库上部署同一证书。

- 在环境中通过最新版本的 SQL Server 创建证书。 例如：
  - 通过 SQL Server 2016 或更高版本创建的证书与 SQL Server 2014 或更低版本兼容。
  - 通过 SQL Server 2014 或更低版本创建的证书与 SQL Server 2016 或更高版本不兼容。

## <a name="example-scripts"></a>示例脚本

这些是 SQL 示例脚本，用于在 Configuration Manager 站点数据库中创建和部署 BitLocker 管理加密证书。

### <a name="create-certificate"></a>创建证书

此示例脚本执行以下操作：

- 创建证书
- 设置权限
- 创建数据库主密钥

在生产环境中使用此脚本之前，请更改以下值：

- 站点数据库名称 (`CM_ABC`)
- 用于创建主密钥的密码 (`MyMasterKeyPassword`)
- 证书到期日期 (`20391022`)

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN
    CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
    WITH SUBJECT = 'BitLocker Management',
    EXPIRY_DATE = '20391022'

    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
    GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="back-up-certificate"></a>备份证书

此示例脚本用于备份证书。 将证书保存到文件中后，可以将其[还原](#restore-certificate)到层次结构中的其他站点数据库。

在生产环境中使用此脚本之前，请更改以下值：

- 站点数据库名称 (`CM_ABC`)
- 文件路径和名称 (`C:\BitLockerManagement_CERT_KEY`)
- 导出密钥密码 (`MyExportKeyPassword`)

``` SQL
USE CM_ABC
BACKUP CERTIFICATE BitLockerManagement_CERT TO FILE = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        ENCRYPTION BY PASSWORD = 'MyExportKeyPassword')
```

> [!IMPORTANT]
> 将导出的证书文件和关联密码存储在安全位置。

### <a name="restore-certificate"></a>还原证书

此示例脚本从文件中还原证书。 按此流程部署在另一个站点数据库上创建的证书。

在生产环境中使用此脚本之前，请更改以下值：

- 站点数据库名称 (`CM_ABC`)
- 主密钥密码 (`MyMasterKeyPassword`)
- 文件路径和名称 (`C:\BitLockerManagement_CERT_KEY`)
- 导出密钥密码 (`MyExportKeyPassword`)

``` SQL
USE CM_ABC
IF NOT EXISTS (SELECT name FROM sys.symmetric_keys WHERE name = '##MS_DatabaseMasterKey##')
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MyMasterKeyPassword'
END

IF NOT EXISTS (SELECT name from sys.certificates WHERE name = 'BitLockerManagement_CERT')
BEGIN

CREATE CERTIFICATE BitLockerManagement_CERT AUTHORIZATION RecoveryAndHardwareCore
FROM FILE  = 'C:\BitLockerManagement_CERT'
    WITH PRIVATE KEY ( FILE = 'C:\BitLockerManagement_CERT_KEY',
        DECRYPTION BY PASSWORD = 'MyExportKeyPassword')

GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareRead
GRANT CONTROL ON CERTIFICATE ::BitLockerManagement_CERT TO RecoveryAndHardwareWrite
END
```

### <a name="verify-certificate"></a>验证证书

使用此 SQL 脚本验证 SQL 是否成功创建了具有所需权限的证书。

``` SQL
USE CM_ABC
declare @count int
select @count = count(distinct u.name) from sys.database_principals u
join sys.database_permissions p on p.grantee_principal_id = u.principal_id or p.grantor_principal_id = u.principal_id
join sys.certificates c on c.certificate_id = p.major_id
where u.name in('RecoveryAndHardwareCore', 'RecoveryAndHardwareRead', 'RecoveryAndHardwareWrite') and
c.name = 'BitLockerManagement_CERT' and p.permission_name like 'CONTROL'
if(@count >= 3) select 1
else select 0
```

如果证书有效，脚本将返回值 `1`。

## <a name="see-also"></a>另请参阅

有关这些 SQL 命令的详细信息，请参阅以下文章：

- [SQL Server 和数据库加密密钥](https://docs.microsoft.com/sql/relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine)
- [创建证书](https://docs.microsoft.com/sql/t-sql/statements/create-certificate-transact-sql)
- [备份证书](https://docs.microsoft.com/sql/t-sql/statements/backup-certificate-transact-sql)
- [创建主密钥](https://docs.microsoft.com/sql/t-sql/statements/create-master-key-transact-sql)
- [备份主密钥](https://docs.microsoft.com/sql/t-sql/statements/backup-master-key-transact-sql)
- [授予证书权限](https://docs.microsoft.com/sql/t-sql/statements/grant-certificate-permissions-transact-sql)
