---
title: 'Herramienta de migración de reglas de firewall de seguridad de los puntos de conexión para Microsoft Intune: Azure | Microsoft Docs'
description: Descubra cómo usar la herramienta de migración de reglas de firewall de seguridad de los puntos de conexión para Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/14/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: mattsha
ms.openlocfilehash: 7dd6d3a01d18e4d8b334bdeee3f72eeaeed67c0a
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2020
ms.locfileid: "86465034"
---
# <a name="endpoint-security-firewall-rule-migration-tool-overview"></a>Información general sobre la herramienta de migración de reglas de firewall de seguridad de los puntos de conexión

Muchas organizaciones buscan trasladar su configuración de seguridad a Microsoft Endpoint Manager para usar la administración moderna basada en la nube.

La seguridad de los puntos de conexión en Endpoint Manager ofrece experiencias de administración enriquecidas de configuración del firewall de Windows y administración de reglas de firewall granulares.

En muchas organizaciones, ya cuentan con directivas de grupo para administrar las reglas de firewall de Windows. La transición hacia una administración moderna puede resultar complicada, ya que la creación manual de cientos de reglas de firewall puede ser una tarea ardua.

Para ayudar a los clientes a cambiar la configuración de las reglas de firewall a las directivas de seguridad de los puntos de conexión en Endpoint Manager, se ha desarrollado la **herramienta de migración de reglas de firewall de seguridad de los puntos de conexión**.

Los clientes pueden ejecutar la **herramienta de migración de reglas de firewall de seguridad de los puntos de conexión** en un cliente de Windows 10 de referencia o preconfigurado, y crear automáticamente directivas de reglas de firewall de seguridad de los puntos de conexión en Endpoint Manager. Una vez creados, los administradores pueden dirigir estas reglas a los grupos de Azure AD para configurar clientes MDM y otros administrados conjuntamente.

Descargue la [herramienta de migración de reglas de firewall de seguridad de los puntos de conexión](https://aka.ms/EndpointSecurityFWRuleMigrationTool):<br>
<a href="https://aka.ms/EndpointSecurityFWRuleMigrationTool"><img alt="Download the tool" src="./media/endpoint-security-firewall-rule-tool/downloadtool.png" width="170"></a>

## <a name="tool-usage"></a>Uso de la herramienta

La herramienta se ejecuta en una máquina de referencia y migra la configuración actual de las reglas del Firewall de Windows. Al ejecutar la herramienta, se exportarán todas las reglas del firewall habilitadas que haya en el dispositivo y se crearán automáticamente directivas nuevas de Intune con las reglas recopiladas.

1. Inicie sesión en la máquina de referencia con privilegios de administrador local.
2. Descargue y el archivo `Export-FirewallRules.zip` y descomprímalo. <br>
   El archivo .zip contiene el archivo de script `Export-FirewallRules.ps1`. 
3. Ejecute el script `Export-FirewallRules.ps1` en la máquina. <br>
   El script descargará todos los requisitos previos necesarios para ejecutarlo. Cuando se le solicite, proporcione las credenciales del Administrador de Intune adecuadas. Para obtener más información sobre los permisos necesarios, vea [Permisos necesarios](#required-permissions).
4. Proporcione el nombre de una directiva cuando se le solicite. <br>
   Esta directiva estará visible en [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), en el panel **Seguridad de los puntos de conexión** > **Firewall**. 

    > [!IMPORTANT]
    > El nombre de la directiva debe ser único para el inquilino.

    Si se encuentran más de 150 reglas de firewall, se crearán varias directivas.

    > [!NOTE]
    > De forma predeterminada, solo se migrarán las reglas de firewall habilitadas y las que cree el GPO. Se proporcionan modificadores para cambiar estos valores predeterminados. Para obtener más información, vea [Modificadores](#switches).
    >
    > En función del recuento de reglas de firewall encontradas, la herramienta puede tardar cierto tiempo en ejecutarse.

5. Una vez completada la operación, la herramienta generará un recuento de las reglas de firewall que no se han podido migrar automáticamente. Para obtener más información, vea, [Configuración no admitida](#unsupported-configuration).

## <a name="switches"></a>Modificadores

Puede usar los modificadores siguientes (parámetros) para cambiar la función predeterminada de la herramienta.

- `IncludeLocalRules`: si usa este modificador, se incluirán todas las reglas de firewall de Windows creadas localmente o predeterminadas en la exportación. Tenga en cuenta que, al habilitar este modificador, se puede provocar la inclusión de muchas reglas. 
- `IncludedDisabledRules`: si usa este modificador, se incluirán todas las reglas de firewall de Windows habilitadas y deshabilitadas en la exportación. Tenga en cuenta que, al habilitar este modificador, se puede provocar la inclusión de muchas reglas.

## <a name="unsupported-configuration"></a>Configuración no admitida

La configuración siguiente, basada en el registro, no se admite debido a la falta de compatibilidad con MDM en Windows. Estos valores no son habituales, pero, si los necesita, registre esta necesidad a través de los canales estándar de soporte técnico.

|     Campo de GPO    |     Motivo    |
|-|-|
|      TYPE-VALUE =/ "Security=" IFSECURE-VAL    |     La configuración relacionada con IPSec no es compatible con MDM de Windows.    |
|      TYPE-VALUE =/ "Security2_9=" IFSECURE2-9-VAL    |     La configuración relacionada con IPSec no es compatible con MDM de Windows.    |
|      TYPE-VALUE =/ "Security2=" IFSECURE2-10-VAL     |     La configuración relacionada con IPSec no es compatible con MDM de Windows.    |
|      TYPE-VALUE =/ "IF=" IF-VAL    |     El identificador de interfaz (LUID) no es administrable.    |
|      TYPE-VALUE =/ "Defer=" DEFER-VAL    |     El recorrido de NAT de entrada relacionado no se expone a través de la directiva de grupo o de MDM de Windows.    |
|      TYPE-VALUE =/ "LSM=" BOOL-VAL    |     El origen no estricto asignado no se expone a través de la directiva de grupo o de MDM de Windows.    |
|      TYPE-VALUE =/ "Platform=" PLATFORM-VAL    |     El control de versiones del sistema operativo no se expone a través de la directiva de grupo o de MDM de Windows.    |
|      TYPE-VALUE =/ "RMauth=" STR-VAL    |     La configuración relacionada con IPSec no es compatible con MDM de Windows.    |
|      TYPE-VALUE =/ "RUAuth=" STR-VAL    |     La configuración relacionada con IPSec no es compatible con MDM de Windows.    |
|      TYPE-VALUE =/ "AuthByPassOut=" BOOL-VAL    |     La configuración relacionada con IPSec no es compatible con MDM de Windows.    |
|      TYPE-VALUE =/ "LOM=" BOOL-VAL    |     Asignado solo local no se expone a través de la directiva de grupo o de MDM de Windows.    |
|      TYPE-VALUE =/ "Platform2=" PLATFORM-OP-VAL    |     El valor redundante no se expone a través de la directiva de grupo o de MDM de Windows.    |
|      TYPE-VALUE =/ "PCross=" BOOL-VAL    |     Permitir cruce de perfiles no se expone a través de la directiva de grupo o de MDM de Windows.    |
|      TYPE-VALUE =/ "LUOwn=" STR-VAL    |     SID de propietario de usuario local no es aplicable en MDM.    |
|      TYPE-VALUE =/ "TTK=" TRUST-TUPLE-KEYWORD-VAL    |     La coincidencia de tráfico con la palabra clave "trust tuple" no se expone a través de la directiva de grupo o de MDM de Windows.    |
|      TYPE-VALUE =/ “TTK2_22=” TRUST-TUPLE-KEYWORD-VAL2-22    |     La coincidencia de tráfico con la palabra clave "trust tuple" no se expone a través de la directiva de grupo o de MDM de Windows.    |
|      TYPE-VALUE =/ “TTK2_27=” TRUST-TUPLE-KEYWORD-VAL2-27    |     La coincidencia de tráfico con la palabra clave "trust tuple" no se expone a través de la directiva de grupo o de MDM de Windows.    |
|      TYPE-VALUE =/ “TTK2_28=” TRUST-TUPLE-KEYWORD-VAL2-28    |     La coincidencia de tráfico con la palabra clave "trust tuple" no se expone a través de la directiva de grupo o de MDM de Windows.    |
|      TYPE-VALUE =/ "NNm=" STR-ENC-VAL    |     La configuración relacionada con IPSec no es compatible con MDM de Windows.    |
|      TYPE-VALUE =/ "SecurityRealmId=" STR-VAL    |     La configuración relacionada con IPSec no es compatible con MDM de Windows.    |

## <a name="unsupported-setting-values"></a>Valores de configuración no admitidos
Los valores de configuración siguientes no se admiten para la migración:

**Puertos**
- `PlayToDiscovery` no se admite como un intervalo de puertos locales o remotos.

**Intervalos de direcciones**
- `LocalSubnet6` no se admite como un intervalo de direcciones locales o remotas. 
- `LocalSubnet4` no se admite como un intervalo de direcciones locales o remotas.
- `PlatToDevice` no se admite como un intervalo de direcciones locales o remotas.

Una vez que se haya ejecutado la herramienta, se generará un informe con las reglas que no se han migrado correctamente. Se puede ver cualquiera de estas reglas mediante el archivo `RulesError.csv`, disponible en `C:\<folder needed>`. 

## <a name="required-permissions"></a>Permisos necesarios
Los usuarios Administrador de seguridad de los puntos de conexión, Administrador de servicios de Intune o Administrador global pueden migrar las reglas de firewall de Windows a las directivas de seguridad del punto de conexión. Como alternativa, se puede usar un rol personalizado en el que se establezcan los permisos de las líneas base de seguridad con las concesiones **Eliminar**, **Leer**, **Asignar**, **Crear** y **Actualizar** aplicadas. Para obtener más información, vea [Conceder permisos de administrador](../fundamentals/users-add.md#grant-admin-permissions).

## <a name="next-steps"></a>Pasos siguientes

- Asigne las reglas a los grupos de Azure AD para configurar MDM y los clientes administrados conjuntamente. Para más información, consulte [Agregar grupos para organizar usuarios y dispositivos](../fundamentals/groups-add.md).
