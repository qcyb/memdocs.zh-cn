---
title: 配置适用于 Active Directory 的 Intune 连接器的代理设置
description: 介绍如何将适用于 Active Directory 的 Intune 连接器配置为与现有本地代理服务器结合使用。
keywords: ''
author: master11218
ms.author: erikje
manager: dougeby
ms.date: 4/16/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: tanvira
ms.suite: ems
search.appverid: ''
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 227ed78b593ce10d47b9a1cdcc14dfbd58acdd93
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "79339509"
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>与现有本地代理服务器结合使用

本文介绍如何将适用于 Active Directory 的 Intune 连接器配置为与出站代理服务器结合使用。 这适用于网络环境中已有代理的客户。

默认情况下，适用于 Active Directory 的 Intune 连接器将尝试使用 Web 代理自动发现 (WPAD) 自动定位网络上的代理服务器。 如果已在网络上配置此配置，则可能不需要其他配置。  如果需要进行更改，以下各节介绍如何利用[用于配置代理设置的标准 .NET Framework 功能](https://docs.microsoft.com/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings)替代默认设置。  该文档中介绍了其他选项。

有关连接器工作方式的详细信息，请参阅[了解 Azure AD 应用程序代理连接器](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-connectors)。

## <a name="completely-bypass-outbound-proxies"></a>完全绕过出站代理

可以将连接器配置为绕过本地代理，以确保它使用与 Azure 服务的直接连接。 只要网络策略允许，我们就建议使用此方法，因为这意味着减少了一个需要维护的配置。

若要禁用连接器的出站代理，请编辑 :\Program Files\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config 文件，并在以下代码示例所示的部分中添加代理地址和代理端口：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

若要确保连接器更新服务也绕过代理，请对 C:\Program Files\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config 做出类似更改。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>
            <defaultProxy enabled="False" /> 
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

请务必对原始文件进行备份，以应对需要还原到默认 .config 文件的情况。

修改配置文件之后，需要重新启动 Intune 连接器服务。 

1. 打开“services.msc”  。
2. 找到并选择“Intune ODJConnector 服务”  。
3. 选择“重启”  。

![服务重启的屏幕截图](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="specifying-an-alternative-proxy-server"></a>指定备用代理服务器

如果需要将其他代理服务器（例如，绕过身份验证的代理服务器）与适用于 Active Directory 的 Intune 连接器一起使用，则可以使用类似的方式来指定服务器。 为此，请编辑 :\Program Files\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config 文件，并在以下代码示例所示的部分中添加代理地址和代理端口：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <runtime>
        <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
            <dependentAssembly>
                <assemblyIdentity name="mscorlib" publicKeyToken="b77a5c561934e089" culture="neutral"/>
                <bindingRedirect oldVersion="0.0.0.0-2.0.0.0" newVersion="4.6.0.0" />
            </dependentAssembly>
        </assemblyBinding>
    </runtime>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="SignInURL" value="https://portal.manage.microsoft.com/Home/ClientLogon"/>
        <add key="LocationServiceEndpoint" value="RestUserAuthLocationService/RestUserAuthLocationService/ServiceAddresses"/>
    </appSettings>
</configuration>
```

若要确保连接器更新服务也绕过代理，请对 C:\Program Files\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config 做出类似更改。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.net>  
        <defaultProxy>   
            <proxy proxyaddress="<PROXY ADDRESS HERE>:<PORT HERE>" bypassonlocal="True" usesystemdefault="True"/>   
        </defaultProxy>  
    </system.net>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6" />
    </startup>
    <appSettings>
        <add key="BaseServiceAddress" value="https://manage.microsoft.com/" />
    </appSettings>
</configuration>
```

请务必对原始文件进行备份，以应对需要还原到默认 .config 文件的情况。

修改配置文件之后，需要重新启动 Intune 连接器服务。 

1. 打开“services.msc”  。
2. 找到并选择“Intune ODJConnector 服务”  。
3. 选择“重启”  。

![服务重启的屏幕截图](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="next-steps"></a>后续步骤

[管理设备](../remote-actions/device-management.md)
