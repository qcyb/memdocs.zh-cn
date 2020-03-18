<!-- This include is part of the Intune Data Warehouse documentation. -->

## <a name="azure-ad-and-intune-credential-requirements"></a>Azure AD 和 Intune 凭据要求

身份验证和授权基于 Azure AD 凭据和 Intune 基于角色的访问控制 (RBAC)。 默认情况下，租户的所有全局管理员和 Intune 服务管理员都可访问该数据仓库。 使用 Intune 角色通过让更多用户访问“Intune 数据仓库”资源，为其提供访问权限  。

访问 Intune 数据仓库（包括 API）的要求如下：

- 用户必须是以下任一身份：
  - Azure AD 全局管理员
  - Intune 服务管理员
  - 具有对“Intune 数据仓库”资源的基于角色的访问权限的用户 
  - 使用[仅应用程序身份验证](../developer/data-warehouse-app-only-auth.md)的无用户身份验证 
