---
title: Configuración del proxy para el conector de Intune para Active Directory
description: Se explica cómo configurar el conector de Intune para Active Directory para trabajar con servidores proxy locales existentes.
keywords: ''
author: master11218
ms.author: erikje
manager: dougeby
ms.date: 4/16/2019
ms.topic: how-to
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
ms.openlocfilehash: 9c7300c03ce0ba703f423aa420e9e47534ef2968
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908690"
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>Trabajar con servidores proxy locales existentes

En este artículo se explica cómo configurar el conector de Intune para Active Directory para trabajar con servidores proxy de salida. Está dirigido a clientes con entornos de red que tienen servidores proxy.

De forma predeterminada, el conector de Intune para Active Directory intentará localizar automáticamente un servidor proxy en la red mediante la detección automática de proxy web (WPAD). Si se ha configurado en la red, puede que no sea necesaria una configuración adicional.  Si se necesitan cambios, en las siguientes secciones se describe cómo invalidar la configuración predeterminada, aprovechando [las capacidades de .NET Framework estándar para configurar los valores de proxy](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings).  En esa documentación se describen opciones adicionales.

Para más información sobre cómo funcionan los conectores, vea [Understand Azure AD Application Proxy connectors](/azure/active-directory/manage-apps/application-proxy-connectors) (Descripción de conectores de Azure AD Application Proxy).

## <a name="completely-bypass-outbound-proxies"></a>Omisión por completo de los servidores proxy de salida

Puede configurar el conector para omitir el proxy local para asegurarse de que usa una conectividad directa con los servicios de Azure. Se recomienda hacer esto siempre que lo permita la directiva de red, porque así tendrá una configuración menos que mantener.

Para deshabilitar el uso de proxy de salida para el conector, edite el archivo C:\Archivos de programa\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config y agregue la dirección y el puerto del proxy en la sección que se muestra en este ejemplo de código:

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

Para asegurarse de que el servicio Connector Updater también omite el proxy, realice un cambio similar en C:\Archivos de programa\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config.

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

Asegúrese de realizar copias de los archivos originales, en caso de que deba volver a los archivos .config predeterminados.

Una vez que se hayan modificado los archivos de configuración, deberá reiniciar el servicio de conector de Intune. 

1. Abra **services.msc**.
2. Busque y seleccione el **Servicio ODJConnector de Intune**.
3. Seleccione **Reiniciar**.

![Captura de pantalla de reinicio del servicio](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="specifying-an-alternative-proxy-server"></a>Especificación de un servidor proxy alternativo

Si es necesario usar un servidor proxy distinto (por ejemplo, uno que omite la autenticación) con el Conector de Intune para Active Directory, se puede especificar de manera similar. Para ello, edite el archivo C:\Archivos de programa\Microsoft Intune\ODJConnector\ODJConnectorUI\ODJConnectorUI.exe.config y agregue la dirección y el puerto del proxy en la sección que se muestra en este ejemplo de código:

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

Para asegurarse de que el servicio Connector Updater también omite el proxy, realice un cambio similar en C:\Archivos de programa\Microsoft Intune\ODJConnector\ODJConnectorSvc\ODJConnectorSvc.exe.config.

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

Asegúrese de realizar copias de los archivos originales, en caso de que deba volver a los archivos .config predeterminados.

Una vez que se hayan modificado los archivos de configuración, deberá reiniciar el servicio de conector de Intune. 

1. Abra **services.msc**.
2. Busque y seleccione el **Servicio ODJConnector de Intune**.
3. Seleccione **Reiniciar**.

![Captura de pantalla de reinicio del servicio](./media/autopilot-hybrid-connector-proxy/service-restart.png)


## <a name="next-steps"></a>Pasos siguientes

[Administrar los dispositivos](../remote-actions/device-management.md)