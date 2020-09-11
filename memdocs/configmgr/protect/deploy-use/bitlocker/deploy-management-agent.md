---
title: Implementación de la administración de BitLocker
titleSuffix: Configuration Manager
description: Implementación del agente de administración de BitLocker en clientes de Configuration Manager y el servicio de recuperación en puntos de administración
ms.date: 08/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: how-to
ms.assetid: 39aa0558-742c-4171-81bc-9b1e6707f4ea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8ef60b82e6ab594689576520443bc74eac7bd17d
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606930"
---
# <a name="deploy-bitlocker-management"></a>Implementación de la administración de BitLocker

*Se aplica a: Configuration Manager (rama actual)*

<!--3601034-->

La administración de BitLocker en Configuration Manager incluye los siguientes componentes:

- **Agente de administración de BitLocker**: Configuration Manager habilita este agente en un dispositivo al [crear una directiva](#create-a-policy) e [implementarla en una colección](#deploy-a-policy).

- **Servicio de recuperación**: Componente de servidor que recibe los datos de recuperación de BitLocker de los clientes. Para obtener más información, consulte [Servicio de recuperación](#recovery-service).

Antes de crear e implementar directivas de administración de BitLocker:

- Revise los [requisitos previos](../../plan-design/bitlocker-management.md#prerequisites)

- Si es necesario, [cifre las claves de recuperación](encrypt-recovery-data.md) en la base de datos del sitio

## <a name="create-a-policy"></a>Creación de una directiva

Al crear e implementar esta directiva, el cliente de Configuration Manager habilita el agente de administración de BitLocker en el dispositivo.

> [!NOTE]
> Para crear una directiva de administración de BitLocker, necesita el rol de **Administrador total** en Configuration Manager.

1. En la consola de Configuration Manager, vaya al área de trabajo **Activos y compatibilidad**, expanda **Endpoint Protection** y seleccione el nodo **Administración de BitLocker**.

1. En la cinta de opciones, seleccione **Crear directiva de control de administración de BitLocker**.

1. En la página **General**, especifique un nombre y una descripción opcional. Seleccione los componentes que se van a habilitar en los clientes con esta directiva:  

    - **Unidad de sistema operativo**: administre si se cifra la unidad del sistema operativo.

    - **Unidad fija**: administre el cifrado de unidades de datos adicionales en un dispositivo

    - **Unidad extraíble**: administre el cifrado de las unidades que se pueden quitar de un dispositivo, como una clave USB

    - **Administración de clientes**: administre la copia de seguridad del servicio de recuperación de claves de la información de recuperación de Cifrado de unidad BitLocker.  

1. En la página **Configuración**, defina las siguientes opciones globales para Cifrado de unidad BitLocker:

    > [!NOTE]
    > Configuration Manager aplica esta configuración al habilitar BitLocker. Si la unidad ya está cifrada o está en proceso de estarlo, cualquier cambio en esta configuración de directiva no cambiará el cifrado de unidades en el dispositivo.
    >
    > Si deshabilita o no establece esta configuración, BitLocker usa el método de cifrado predeterminado (AES de 128 bits).

    - En el caso de los dispositivos Windows 8.1, habilite la opción **Método de cifrado de unidades e intensidad de cifrado**. Luego, seleccione el método de cifrado.

    - En el caso de los dispositivos Windows 10, habilite la opción **Método de cifrado de unidades e intensidad de cifrado (Windows 10)** . A continuación, seleccione individualmente el método de cifrado para las unidades de sistema operativo, las unidades de datos fijas y las unidades de datos extraíbles.

    Para obtener más información sobre estas y otras opciones de esta página, consulte [Referencia de configuración: configuración](../../tech-ref/bitlocker/settings.md#setup).

1. En la página **Unidad de sistema operativo**, especifique las opciones siguientes:  

    - **Configuración de cifrado para unidades de sistema operativo**: si habilita esta opción, el usuario tiene que proteger la unidad del sistema operativo y BitLocker cifra la unidad. Si la deshabilita, el usuario no puede proteger la unidad.  

    En dispositivos con un TPM compatible, se pueden usar dos tipos de métodos de autenticación durante el inicio para ofrecer una protección adicional para los datos cifrados. Cuando se inicia el equipo, se puede utilizar únicamente el TPM para la autenticación o también se puede requerir la entrada de un número de identificación personal (PIN). Configure las siguientes opciones:

    - **Select protector for operating system drive** (Seleccionar protector para la unidad del sistema operativo): configúrelo para usar un TPM y PIN, o simplemente el TPM.

    - **Configurar longitud mínima de PIN para el inicio**: si necesita un PIN, este valor es la longitud más corta que el usuario puede especificar. El usuario escribe este PIN cuando arranca el equipo para desbloquear la unidad. De forma predeterminada, la longitud de PIN mínima es de `4`.

    Para obtener más información sobre estas y otras opciones de esta página, consulte [Referencia de configuración: unidad del sistema operativo](../../tech-ref/bitlocker/settings.md#os-drive).

1. En la página **Unidad fija**, especifique la siguiente configuración:

    - **Cifrado de unidades de datos fijas**: Si habilita esta configuración, BitLocker requerirá que los usuarios pongan todas las unidades de datos fijas bajo protección. A continuación, cifrará las unidades de datos. Al habilitar esta directiva, habilite el desbloqueo automático o la configuración **Directiva de contraseñas de unidades de datos fijas**.

    - **Configurar el desbloqueo automático para la unidad de datos fija**: Permita o requiera que BitLocker desbloquee automáticamente cualquier unidad de datos cifrada. Para usar el desbloqueo automático, también es necesario que BitLocker cifre la unidad de sistema operativo.

    Para obtener más información sobre estas y otras opciones de esta página, consulte [Referencia de configuración: unidad fija](../../tech-ref/bitlocker/settings.md#fixed-drive).

1. En la página **Unidad extraíble**, especifique la siguiente configuración:

    - **Cifrado de unidades de datos extraíble**: Al habilitar esta opción y permitir que los usuarios apliquen la protección de BitLocker, el cliente de Configuration Manager guarda la información de recuperación de las unidades extraíbles en el servicio de recuperación del punto de administración. Este comportamiento permite que los usuarios recuperen la unidad si olvidan o pierden el protector (contraseña).

    - **Permitir a los usuarios aplicar la protección de BitLocker en unidades de datos extraíbles**: Los usuarios pueden activar la protección de BitLocker para una unidad extraíble.

    - **Directiva de contraseñas de unidades de datos extraíbles**: Use esta configuración para establecer las restricciones de las contraseñas para desbloquear las unidades extraíbles protegidas por BitLocker.

    Para obtener más información sobre estas y otras opciones de esta página, consulte [Referencia de configuración: unidad extraíble](../../tech-ref/bitlocker/settings.md#removable-drive).

1. En la página **Administración de cliente**, especifique las opciones siguientes:

    > [!IMPORTANT]
    > Si no tiene ningún punto de administración con un sitio web habilitado para HTTPS, no configure esta opción. Para obtener más información, consulte [Servicio de recuperación](#recovery-service).

    - **Configurar los servicios de administración de BitLocker**: Si habilita esta opción, Configuration Manager realizará automáticamente y de forma silenciosa una copia de seguridad de la información de recuperación de claves en la base de datos del sitio. Si deshabilita o no establece esta configuración, Configuration Manager no guardará la información de la recuperación de claves.

        - **Seleccionar la información de recuperación de BitLocker que debe almacenarse**: se puede configurar para usar un paquete de contraseña y clave de recuperación, o bien solo una contraseña de recuperación.

        - **Permitir que la información de recuperación se almacene en texto sin formato**: Sin un certificado de cifrado de administración de BitLocker, Configuration Manager almacena la información de la recuperación de claves en texto sin formato. Para obtener más información, consulte el artículo [Cifrado de los datos de recuperación](encrypt-recovery-data.md).

    Para obtener más información sobre estas y otras opciones de esta página, consulte [Referencia de configuración: administración de cliente](../../tech-ref/bitlocker/settings.md#client-management).

1. Complete el asistente.

Para cambiar la configuración de una directiva existente, selecciónela en la lista y seleccione **Propiedades**.

Al crear más de una directiva, puede configurar su prioridad relativa. Si implementa varias directivas en un cliente, usa el valor de prioridad para determinar su configuración.

A partir de la versión 2006, puede usar los cmdlets de Windows PowerShell para esta tarea. Para obtener más información, vea [New-CMBlmSetting](/powershell/module/configurationmanager/new-cmblmsetting).

## <a name="deploy-a-policy"></a>Implementación de una directiva

1. Seleccione una directiva existente en el nodo **Administración de BitLocker**. En la cinta de opciones, seleccione **Implementar**.

1. Seleccione una colección de dispositivos como destino de la implementación.

1. Si quiere que el dispositivo cifre o descifre potencialmente sus unidades en cualquier momento, seleccione la opción para **permitir la corrección fuera de la ventana de mantenimiento**. Si la colección tiene ventanas de mantenimiento, seguirá corrigiendo esta directiva de BitLocker.

1. Configure una programación **simple** o **personalizada**. El cliente evalúa su cumplimiento según la configuración especificada en la programación.

1. Seleccione **Aceptar** para implementar la directiva.

Puede crear varias implementaciones de la misma directiva. Para consultar información adicional sobre cada implementación, seleccione la directiva en el nodo **Administración de BitLocker** y, a continuación, en el panel de detalles, cambie a la pestaña **Implementaciones**.

> [!IMPORTANT]
> El cliente de MBAM no inicia las acciones de Cifrado de unidad BitLocker si está activa una conexión de protocolo de escritorio remoto. Todas las conexiones de la consola remota deben estar cerradas, y un usuario debe haber iniciado sesión en una sesión de consola física antes de que se inicie el Cifrado de unidad BitLocker.

A partir de la versión 2006, puede usar los cmdlets de Windows PowerShell para esta tarea. Para obtener más información, vea [New-CMSettingDeployment](/powershell/module/configurationmanager/new-cmsettingdeployment).

## <a name="monitor"></a>Supervisión

Consulte estadísticas básicas de cumplimiento de la implementación de directivas en el panel de detalles del nodo **Administración de BitLocker**:

- Recuento de compatibilidad
- Recuento de errores
- Recuento de no compatibilidad

Cambie a la pestaña **Implementaciones** para ver el porcentaje de cumplimiento y la acción recomendada. Seleccione la implementación y, en la cinta de opciones, seleccione **Ver estado**. Esta acción cambia la vista al área de trabajo **Supervisión**, nodo **Implementaciones**. De forma similar a la implementación de otras implementaciones de directivas de configuración, en esta vista puede ver el estado de cumplimiento más detallado.

Para comprender por qué los clientes se notifican como no conformes con la directiva de administración de BitLocker, consulte [Códigos de no conformidad](../../tech-ref/bitlocker/non-compliance-codes.md).

Para obtener más información acerca de la solución de problemas, vea [Solución de problemas de BitLocker](../../tech-ref/bitlocker/troubleshoot.md).

Use los registros siguientes para la supervisión y solución de problemas:

### <a name="client-logs"></a>Registros de cliente

- Registro de eventos de MBAM: en el Visor de eventos de Windows, vaya a Aplicaciones y servicios > Microsoft > Windows > MBAM.  Para obtener más información, consulte [Acerca de los registros de eventos de BitLocker](../../tech-ref/bitlocker/about-event-logs.md) y [Registros de eventos de cliente](../../tech-ref/bitlocker/client-event-logs.md).

- **BitlockerMangementHandler.log** en la ruta de acceso de los registros de cliente, `%WINDIR%\CCM\Logs` de forma predeterminada

### <a name="management-point-logs-recovery-service"></a>Registros de puntos de administración (servicio de recuperación)

- Registro de eventos del servicio de recuperación: en el Visor de eventos de Windows, vaya a Aplicaciones y servicios > Microsoft > Windows > MBAM-Web. Para obtener más información, vea [Registros de eventos de BitLocker](../../tech-ref/bitlocker/about-event-logs.md) y [Registros de eventos del servidor](../../tech-ref/bitlocker/server-event-logs.md).

- Registros de seguimiento del servicio de recuperación: `<Default IIS Web Root>\Microsoft BitLocker Management Solution\Logs\Recovery And Hardware Service\trace*.etl`

## <a name="recovery-service"></a>Servicio de recuperación

El servicio de recuperación de BitLocker es un componente de servidor que recibe datos de recuperación de BitLocker de los clientes de Configuration Manager. El sitio implementa el servicio de recuperación al crear una directiva de administración de BitLocker. Configuration Manager instala automáticamente el servicio de recuperación en cada punto de administración con un sitio web habilitado para HTTPS.

Configuration Manager almacena la información de recuperación en la base de datos del sitio. Sin un certificado de cifrado de administración de BitLocker, Configuration Manager almacena la información de la recuperación de claves en texto sin formato.

Para obtener más información, consulte el artículo [Cifrado de los datos de recuperación](encrypt-recovery-data.md).

## <a name="migration-considerations"></a>Consideraciones de migración

Si está usando Microsoft BitLocker Administration and Monitoring (MBAM), puede migrar la administración sin problemas a Configuration Manager. Al implementar directivas de administración de BitLocker en Configuration Manager, los clientes cargan automáticamente las claves de recuperación y los paquetes en el servicio de recuperación de Configuration Manager.

> [!IMPORTANT]
> Al migrar de MBAM independiente a la administración de BitLocker de Configuration Manager, si necesita una funcionalidad existente de MBAM independiente, no reutilice componentes ni servidores MBAM independientes con la administración de BitLocker de Configuration Manager. Si reutiliza estos servidores, el servicio MBAM independiente dejará de funcionar cuando la administración de BitLocker de Configuration Manager instale sus componentes en esos servidores. No ejecute el script MBAMWebSiteInstaller.ps1 para configurar los portales de BitLocker en servidores MBAM independientes. A la hora de configurar la administración de BitLocker de Configuration Manager, use servidores independientes.

### <a name="group-policy"></a>Directiva de grupo.

- La configuración de la administración de BitLocker es totalmente compatible con la configuración de la directiva de grupo de MBAM. Si los dispositivos reciben la configuración de la directiva de grupo y las directivas de Configuration Manager, configúrelas para que coincidan.

  > [!NOTE]
  > Si existe una configuración de directiva de grupo para MBAM independiente, esta invalidará la equivalente que intente aplicar Configuration Manager. La MBAM independiente usa la directiva de grupo de dominio, mientras que Configuration Manager establece las directivas locales para la administración de BitLocker. Las directivas de dominio invalidarán las de administración de BitLocker de Configuration Manager local. Si la directiva de grupo de dominio de MBAM independiente no coincide con la de Configuration Manager, se producirá un error de administración de BitLocker de Configuration Manager. Por ejemplo, si una directiva de grupo de dominio establece el servidor de MBAM independiente para los servicios de recuperación de claves, la administración de BitLocker de Configuration Manager no podrá establecer la misma configuración para el punto de administración. Este comportamiento hace que los clientes no notifiquen sus claves de recuperación al servicio de recuperación de claves de administración de BitLocker de Configuration Manager en el punto de administración.

- Configuration Manager no implementa todas las configuraciones de directiva de grupo de MBAM. Si configura opciones adicionales en la directiva de grupo, el agente de administración de BitLocker en los clientes de Configuration Manager respeta esta configuración.

  > [!IMPORTANT]
  > No establezca una directiva de grupo para una configuración que ya especifique la administración de BitLocker de Configuration Manager. Establezca únicamente directivas de grupo para los valores que no existen actualmente en la administración de BitLocker de Configuration Manager. La versión 2002 de Configuration Manager cuenta con paridad de características con MBAM independiente. Con la versión 2002 de Configuration Manager y versiones posteriores, en la mayoría de los casos no debería haber ninguna razón para establecer directivas de grupo de dominio para configurar directivas de BitLocker. Para evitar conflictos y problemas, procure no usar directivas de grupo para BitLocker. Configure todas las opciones mediante directivas de administración de BitLocker de Configuration Manager.

### <a name="tpm-password-hash"></a>Hash de contraseña del TPM

- Los clientes anteriores de MBAM no cargan el hash de contraseña del TPM en Configuration Manager. El cliente solo carga el hash de contraseña del TPM una vez.

- Si necesita migrar esta información al servicio de recuperación de Configuration Manager, quite el TPM del dispositivo. Una vez reiniciado, cargará el nuevo hash de contraseña del TPM en el servicio de recuperación.

### <a name="re-encryption"></a>Nuevo cifrado

Configuration Manager no vuelve a cifrar las unidades que ya están protegidas con Cifrado de unidad BitLocker. Si implementa una directiva de administración de BitLocker que no coincide con la protección actual de la unidad, lo notificará como no conforme. La unidad sigue protegida.

Por ejemplo, ha utilizado MBAM para cifrar la unidad con el algoritmo de cifrado AES-XTS 128, pero la directiva de Configuration Manager exige AES-XTS 256. La unidad no es conforme con la directiva, aunque la unidad esté cifrada.

Para evitar este comportamiento, deshabilite primero BitLocker en el dispositivo. A continuación, implemente una nueva directiva con la nueva configuración.

## <a name="co-management-and-intune"></a>Administración conjunta e Intune

<!-- SCCMDocs#2321 -->

El controlador del cliente de Configuration Manager para BitLocker es compatible con la administración conjunta. Si el dispositivo está administrado conjuntamente y cambia la [carga de trabajo de Endpoint Protection](../../../comanage/workloads.md#endpoint-protection) a Intune, el cliente de Configuration Manager omite su directiva de BitLocker. El dispositivo obtiene la directiva de cifrado de Windows de Intune.

Al cambiar las autoridades de administración del cifrado, y si el algoritmo de cifrado deseado también cambia, tendrá que planear un [nuevo cifrado](#re-encryption).

Para obtener más información sobre la administración de BitLocker con Intune, consulte los siguientes artículos:

- [Uso del cifrado de dispositivos con Intune](../../../../intune/protect/encrypt-devices.md)
- [Solución de problemas de directivas de BitLocker en Microsoft Intune](../../../../intune/protect/troubleshoot-bitlocker-policies.md)

## <a name="next-steps"></a>Pasos siguientes

[Configuración de informes y portales de BitLocker](setup-websites.md)
