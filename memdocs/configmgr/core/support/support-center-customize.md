---
title: Personalizar el Centro de soporte técnico
titleSuffix: Configuration Manager
description: Personalice el archivo de configuración del Centro de soporte técnico.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a6f7f6b7-9ef3-4ffa-a3cf-d877ac55983b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1436f40dc989202725d7b83d551d318b970f9b5d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707443"
---
# <a name="customize-support-center"></a>Personalizar el Centro de soporte técnico

*Se aplica a: Configuration Manager (rama actual)*

La herramienta [Centro de soporte técnico](support-center.md) incluye un archivo de configuración que se puede personalizar. De forma predeterminada, al instalar el Centro de soporte técnico, este archivo se encuentra en la siguiente ruta de acceso: `C:\Program Files (x86)\Configuration Manager Support Center\ConfigMgrSupportCenter.exe.config`. El archivo de configuración cambia el comportamiento del programa:

- [Personalizar la recopilación de datos](#bkmk_datacoll): edita los conjuntos de claves del Registro y espacios de nombres de WMI que incluye durante la recopilación de datos.  

- [Personalizar los grupos de registros](#bkmk_loggroups): permite definir nuevos grupos de archivos de registro mediante expresiones regulares. Además agrega otros archivos de registro a grupos de registro.  

- [Recopilar más archivos de registro mediante caracteres comodín](#bkmk_wildcards): use búsquedas con caracteres comodín para recopilar más archivos de registro.  

Para realizar estos cambios, necesita permisos administrativos locales en el cliente en el que ha instalado el Centro de soporte técnico. Realice estas personalizaciones mediante un editor de texto o XML, como el Bloc de notas o Visual Studio.

> [!Important]  
> El archivo de configuración del Centro de soporte técnico es un archivo con formato XML. Es fundamental para el funcionamiento del Centro de soporte técnico. Se recomienda modificar este archivo única y exclusivamente a los usuarios que estén familiarizados con XML y con las expresiones regulares.  

Antes de personalizar el archivo de configuración del Centro de soporte técnico, guarde una copia de seguridad del original. Esta copia de seguridad le permite recuperar la funcionalidad original del Centro de soporte técnico si comete algún error mientras edita el archivo. Si no crea una copia de seguridad y el Centro de soporte técnico no funciona correctamente después de modificar el archivo de configuración, vuelva a instalar el Centro de soporte técnico. También puede copiar un archivo de configuración de otra instalación del Centro de soporte técnico.



## <a name="customize-data-collection"></a><a name="bkmk_datacoll"></a> Personalizar la recopilación de datos

Para personalizar la recopilación de datos en el cliente, modifique el archivo de configuración del Centro de soporte técnico mediante los elementos XML incluidos en el elemento `<dataCollectorSettings>`.


### <a name="wmi-data-collection"></a>Recopilación de datos WMI

El elemento `<CcmWmiDataCollector>` contiene un elemento `<collectionScopes>`. Use este elemento para cambiar los espacios de nombres de WMI de los que el Centro de soporte técnico recopila datos. También incluye un elemento `<ignoreScopes>`. Use este elemento para filtrar la recopilación de datos de partes de los espacios de nombres definidos en el elemento `<collectionScopes>`.  
    
#### <a name="example"></a>Ejemplo
El archivo de configuración predeterminado recopila datos del espacio de nombres `root\ccm`. Incluye esta ruta de acceso en un elemento `<add/>` de `<collectionScopes>`. 

También omite todo lo incluido en las rutas de acceso `\cimodels`, `\invagt`, `\events` y `\policy` de este espacio de nombres. Incluye estas rutas de acceso en elementos `<add/>` incluidos en `<ignoreScopes>`.

```XML
<CcmWmiDataCollector>
  <collectionScopes>
    <!-- Collect these namespaces (ignoring the sub-scopes in the ignoreScopes block) -->
    <add key="root\ccm"/>
    <add key="root\cimv2\sms"/>
  </collectionScopes>
  <ignoreScopes>
    <!-- Collecting these namespaces is known to be problematic/unnecessary -->
    <add key="root\ccm\cimodels"/>
    <add key="root\ccm\invagt"/>
    <add key="root\ccm\events"/>
    <!-- Do not collect policy, there's already a separate policy collector.-->
    <add key="root\ccm\policy"/>
  </ignoreScopes>
</CcmWmiDataCollector>
```


### <a name="registry-data-collection"></a>Recopilación de datos del Registro

El elemento `<RegistryDataCollector>` contiene un elemento `<registryKeys>`. Use este elemento para cambiar las claves y subclaves del Registro que el Centro de soporte técnico recopila en la ruta de acceso `HKEY_LOCAL_MACHINE`. El Centro de soporte técnico no admite la recopilación de datos del Registro de otras rutas de acceso raíz del Registro.

#### <a name="example"></a>Ejemplo
Para recopilar claves del Registro de los programas clásicos instalados en el dispositivo, agregue el siguiente elemento `<add/>` en el elemento `<registryKeys>`: `<add key="software\\microsoft\\windows\\currentversion\\uninstall"/>`

```XML
<RegistryDataCollector>
  <registryKeys>
    <!-- Registry keys (and all subkeys) to collect -->
    <add key="software\\microsoft\\ccm"/>
    <add key="software\\microsoft\\sms"/>
    <add key="software\\microsoft\\ccmsetup"/>
    <add key="software\\microsoft\\windows\\currentversion\\uninstall"/>
  </registryKeys>
</RegistryDataCollector>
```



## <a name="customize-log-file-groups"></a><a name="bkmk_loggroups"></a> Personalizar grupos de archivos de registro

Para personalizar los archivos de registro que recopila el Centro de soporte técnico y cómo los presenta en la lista **Grupos de registro**, use elementos del elemento `<logGroups>`. Cuando se inicia el Centro de soporte técnico, analiza esta sección del archivo de configuración. Luego crea un grupo en la lista **Grupos de registro** para cada valor de atributo de clave único que se encuentre en los elementos `<add/>` incluidos en el elemento `<logGroups>`.

- **Grupo de registros de componente**: el elemento `<componentLogGroup>` usa un atributo clave para definir el nombre del grupo de registros que aparece en la lista. También usa un atributo de valor que contiene una expresión regular (regex). Usa esta expresión regular para recopilar un conjunto de archivos de registro relacionados.  

- **Grupo de registros estático:** el elemento `<staticLogGroup>` usa un atributo clave para definir el nombre del grupo de registros que aparece en la lista. También usa un atributo de valor que define el nombre de un archivo de registro.  

Si se usa el mismo valor de atributo de clave en un elemento `<add/>` dentro del elemento `<componentLogGroup>` y el elemento `<staticLogGroup>`, el Centro de soporte técnico crea un único grupo. Este grupo incluye los archivos de registro definidos por ambos elementos que usan la misma clave.

#### <a name="example"></a>Ejemplo
```XML
<logGroups>
  <componentLogGroup>
    <add key="Application Management" value="^(app.*|ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|execmgr.*|UserAffinity.*|.*Handler$|.*Provider$)"/>
    <add key="Client Registration" value="^(clientregistration|locationservices|ccmmessaging|ccmexec)"/>
    <add key="Inventory" value="^(ccmmessaging|inventoryagent|mtrmgr|swmtrreportgen|virtualapp|mtr.*|filesystemfile)"/>
    <add key="Policy" value="^(ccmmessaging|policyagent_.*|policyevaluator_.*)"/>
    <add key="Software Updates" value="^(ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|update.*|wuahandler|xmlstore|scanagent)"/>
    <add key="Software Distribution" value="^(datatransferservice|execmgr.*|contenttransfermanager|locationservices|contentaccess|filebits)"/>
    <add key="Desired Configuration Management" value="^(ci.*|dcm.*)"/>
    <add key="Operating System Deployment" value="^(ts.*)"/>
  </componentLogGroup>
  <staticLogGroup>
    <add key="Application Management" value="ccmsdkprovider.log"/>
    <add key="Desired Configuration Management" value="ccmsdkprovider.log"/>
    <add key="Software Updates" value="ccmsdkprovider.log"/>
  </staticLogGroup>
</logGroups>
```



## <a name="collecting-additional-log-files-using-wildcards"></a><a name="bkmk_wildcards"></a> Recopilación de otros archivos de registro mediante caracteres comodín

Para recopilar otros archivos de registro, use caracteres comodín en la ruta de acceso o el nombre de archivo. Estos caracteres comodín incluyen variables de entorno de todo el sistema, como `%WINDIR%`, pero excluyen variables de entorno de ámbito de usuario, como `%USERPROFILE%`. Para recopilar más archivos de registro mediante esta búsqueda no recursiva de archivos de registro, use un elemento `<add/>` dentro del elemento `<additionalLogFiles>`. 

Estos ejemplos muestran cómo usa el Centro de soporte técnico esta característica en el archivo de configuración predeterminado.

#### <a name="example-1-collect-all-windows-update-log-files-in-the-windows-directory"></a>Ejemplo 1: recopilar todos los archivos de registro de Windows Update en el directorio de Windows
El siguiente elemento recopila cualquier archivo denominado `WindowsUpdate.log` que haya en el directorio de Windows: 

`<add key="%WINDIR%\WindowsUpdate.log" />`

#### <a name="example-2-collect-all-log-files-in-the-windows-logs-directory"></a>Ejemplo 2: recopilar todos los archivos de registro en el directorio de registros de Windows
El siguiente elemento recopila cualquier archivo que termine en `.log` que haya en el directorio de registros de Windows: 

`<add key="%WINDIR%\logs\*.log" />`

#### <a name="full-example-xml"></a>XML completo del ejemplo
```XML
<CcmLogDataCollector>
  <additionalLogFiles>
    <!-- Collect these additional log files. Can pass in a wildcard for the filename. System variables are also supported. -->
    <!--
    <add key="%WINDIR%\WindowsUpdate.log" />
    <add key="%WINDIR%\logs\*.log" />
    -->
  </additionalLogFiles>
</CcmLogDataCollector>
```
