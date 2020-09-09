## <a name="enable-windows-10-automatic-enrollment"></a>启用 Windows 10 自动注册

自动注册允许用户在 Intune 中注册其 Windows 10 设备。 为了进行注册，用户将其工作帐户添加到其个人拥有的设备或将公司拥有的设备加入 Azure Active Directory。 在后台，设备进行注册并加入 Azure Active Directory。 注册后，通过 Intune 管理设备。

**必备条件**

- Azure Active Directory Premium 订阅（[试用订阅](https://go.microsoft.com/fwlink/?LinkID=816845)）
- Microsoft Intune 订阅

### <a name="configure-automatic-mdm-enrollment"></a>配置自动进行 MDM 注册

1. 登录 [Azure 门户](https://portal.azure.com)，然后选择“Azure Active Directory”  。

   ![Azure 门户的屏幕截图](../enrollment/media/windows-enroll/auto-enroll-azure-main.png)

2. 选择“移动性 (MDM 和 MAM)”  。

   ![Azure 门户的屏幕截图](../enrollment/media/windows-enroll/auto-enroll-mdm.png)

3. 选择“Microsoft Intune”  。

   ![Azure 门户的屏幕截图](../enrollment/media/windows-enroll/auto-enroll-intune.png)

4. 配置“MDM 用户范围”  。 指定应由 Microsoft Intune 管理的用户设备。 这些 Windows 10 设备可自动注册，以使用 Microsoft Intune 进行管理。

   - **无** - MDM 自动注册已禁用
   - **部分** - 选择可以自动注册 Windows 10 设备的组 
   - **全部** - 所有用户都可以自动注册 Windows 10 设备

      > [!IMPORTANT]
      > 对于 Windows BYOD 设备，如果为所有用户（或同一用户组）启用了 MAM 用户范围和 MDM 用户范围（自动 MDM 注册），则 MAM 用户范围优先。 如果配置了 Windows 信息保护 (WIP) 策略，设备将应用这些策略，而不会注册 MDM。
      >
      > 如果要使 Windows BYOD 设备自动注册到 MDM：将 MDM 用户范围配置为“所有”（或“部分”，并指定一个组），并将 MAM 用户范围配置为“无”（或“部分”，并指定一个组 - 确保用户不是 MDM 和 MAM 用户范围的目标组的成员）     。
      >
      >对于[企业设备](../enrollment/enrollment-restrictions-set.md#blocking-personal-windows-devices)，如果启用了 MDM 和 MAM 两个用户范围，则 MDM 用户范围优先。 设备将自动在配置的 MDM 中注册。

   > [!NOTE]
   > 必须将 MDM 用户作用域设置为包含用户对象的 Azure AD 组。

   ![Azure 门户的屏幕截图](../enrollment/media/windows-enroll/auto-enroll-scope.png)

5. 对下列 URL 使用默认值：
    - **MDM 使用条款 URL**
    - **MDM 发现 URL**
    - **MDM 符合性 URL**

6. 选择“保存”  。

默认情况下，不会为该服务启用双重身份验证。 但是，在注册设备时，建议启用双因素身份验证。 要启用双因素身份验证，请在 Azure AD 中配置一个双因素身份验证提供程序，并为用户帐户配置多重身份验证。 请参阅[Azure 多重身份验证服务器入门](/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud)。