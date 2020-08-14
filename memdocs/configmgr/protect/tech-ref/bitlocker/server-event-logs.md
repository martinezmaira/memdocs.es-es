---
title: Registros de eventos del servidor
titleSuffix: Configuration Manager
description: Referencia técnica de las posibles entradas del servidor de BitLocker (MBAM) en el registro de eventos de Windows
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: reference
ms.assetid: c3279b7d-654d-444b-bd17-1262894590c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe7d24bc1cad27094d720a5cb5aa487caec9199d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127872"
---
# <a name="server-event-logs"></a>Registros de eventos del servidor

*Se aplica a: Configuration Manager (rama actual)*

<!--3601034-->

Use el Visor de eventos de Windows para ver los registros de eventos de los siguientes componentes del servidor de administración de BitLocker en Configuration Manager:

- Servicio de recuperación en el punto de administración
- Portal de autoservicio
- Sitio web de administración y supervisión

En un servidor que hospeda uno o varios de estos componentes, abra el Visor de eventos. A continuación, vaya a **Registros de aplicaciones y servicios**, **Microsoft**, **Windows** y expanda **MBAM-Web**. De forma predeterminada, hay registros de eventos [administrativos](#admin) y [operativos](#operational).

Las secciones siguientes contienen mensajes e información de solución de problemas para los identificadores de eventos que se pueden producir con los componentes del servidor de administración de BitLocker.

## <a name="admin"></a>Administración

### <a name="1-webappspnerror"></a>1: WebAppSpnError

La aplicación {SiteName} {VirtualDirectory} no tiene los siguientes nombres de entidad de seguridad de servicio (SPN) {ListOfSpns} Registre los SPN necesarios en la cuenta {ExecutionAccount}.

Para que la autenticación integrada de Windows se realice correctamente, deben estar vigentes los SPN necesarios. Este mensaje indica que el SPN necesario para la aplicación no está configurado correctamente. Los detalles contenidos en este evento deben proporcionar más información.

<!-- See "Service Principal Name (SPN)" in MBAM 2.5 Server Prerequisites for Stand-alone and Configuration Manager Integration Topologies for more information. -->

### <a name="100-adminservicerecoverydberror"></a>100: AdminServiceRecoveryDbError

Posibles mensajes de error:

- GetMachineUsers: error al obtener información de usuario de la base de datos.
- GetRecoveryKey: error al obtener la clave de recuperación de la base de datos.
- GetRecoveryKey: error al obtener información de usuario de la base de datos.
- GetRecoveryKeyIds: error al obtener los identificadores de clave de recuperación de la base de datos.
- GetTpmHashForUser: error al obtener los datos hash de TPM de la base de datos de recuperación.
- GetTpmHashForUser: error al obtener los datos hash de TPM de la base de datos de recuperación.
- QueryDriveRecoveryData: error al obtener los datos de recuperación de la unidad de la base de datos.
- QueryRecoveryKeyIdsForUser: error al obtener los identificadores de clave de recuperación de la base de datos.
- QueryVolumeUsers: error al obtener información de usuario de la base de datos.

Este mensaje se registra siempre que se produce una excepción al comunicar con la base de datos de recuperación. Lea la información contenida en el seguimiento para obtener detalles concretos acerca de la excepción.

### <a name="101-adminservicecompliancedberror"></a>101: AdminServiceComplianceDbError

Posibles mensajes de error:

- GetRecoveryKey: error al registrar un evento de auditoría en la base de datos de cumplimiento.
- GetRecoveryKeyIds: error al registrar un evento de auditoría en la base de datos de cumplimiento.
- GetTpmHashForUser: error al registrar un evento de auditoría en la base de datos de cumplimiento.
- QueryRecoveryKeyIdsForUser: error al registrar un evento de auditoría en la base de datos de cumplimiento.
- QueryDriveRecoveryData: error al registrar un evento de auditoría en la base de datos de cumplimiento.

Este mensaje se registra siempre que se produce una excepción al comunicar con la base de datos de cumplimiento. Lea la información contenida en el seguimiento para obtener detalles concretos acerca de la excepción.

### <a name="102-agentservicerecoverydberror"></a>102: AgentServiceRecoveryDbError

Este mensaje indica una excepción cuando el servicio intenta comunicarse con la base de datos de recuperación. Lea el mensaje contenido en el evento para obtener información específica acerca de la excepción.

Compruebe que la cuenta del grupo de aplicaciones de MBAM tiene los permisos necesarios para conectarse a la base de datos de recuperación.

### <a name="103-agentserviceerror"></a>103: AgentServiceError

Posibles mensajes de error:

- No se puede detectar la cuenta del equipo cliente o la cuenta de usuario de migración de datos.

    Siempre que se realiza una llamada a los métodos web `PostKeyRecoveryInfo`, `IsRecoveryKeyResetRequired`, `CommitRecoveryKeyRest` o `GetTpmHash`, recupera el contexto del autor de la llamada para obtener las credenciales del autor de la llamada. Si el contexto del autor de la llamada es nulo o está vacío, el servicio registra este mensaje.

- No se pudo verificar la cuenta para comprobar la identidad del autor de la llamada.

    Este mensaje se registra si el método web espera que el autor de la llamada sea una cuenta de equipo y no lo es. También puede deberse a que el método web espera que el autor de la llamada sea una cuenta de usuario y no es una cuenta de usuario ni un miembro de una cuenta de grupo de migración de datos.

### <a name="104-statusservicecompliancedbconfigerror"></a>104: StatusServiceComplianceDbConfigError

La cadena de conexión de la base de datos de cumplimiento del Registro está vacía.

Este mensaje se registra siempre que la cadena de conexión de la base de cumplimiento no es válida. Compruebe el valor de la clave del Registro `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString`.

### <a name="105-statusservicecompliancedberror"></a>105: StatusServiceComplianceDbError

Este error indica que los sitios web o los servicios web no pudieron conectarse a la base de datos de cumplimiento. Compruebe que la cuenta del grupo de aplicaciones de IIS se puede conectar a la base de datos.

### <a name="106-helpdeskerror"></a>106: HelpdeskError

Errores conocidos y posibles causas:

- La solicitud a la dirección URL produjo un error interno.

    Se produjo una excepción no controlada en la aplicación para el sitio web de administración y supervisión (departamento de soporte técnico). Revise las entradas del registro en el registro de eventos de **administración** para encontrar la excepción concreta.

- Error al obtener la información de contexto de la ejecución. No se puede comprobar el registro del nombre de entidad de seguridad de servicio (SPN).

    Durante la operación de carga del sitio web del departamento de soporte técnico, este comprueba el SPN. Para comprobar el SPN, se necesita información de la cuenta, el parámetro Sitename de IIS y el valor ApplicationVirtualPath correspondientes al sitio web del departamento de soporte técnico. Registra este mensaje de error cuando uno o varios de estos atributos no son válidos o faltan.

- Error al comprobar el registro del nombre de entidad de seguridad de servicio (SPN).

    Este mensaje indica que se ha producido una excepción de seguridad al comprobar el SPN. Consulte la excepción contenida en los detalles del evento.

### <a name="107-selfserviceportalerror"></a>107: SelfServicePortalError

Errores conocidos y posibles causas:

- Error al obtener la clave de recuperación de un usuario

    Indica que se produjo una excepción inesperada cuando se realizó una solicitud para recuperar una clave de recuperación. Consulte el mensaje de excepción en los detalles del evento. Si el seguimiento está habilitado en la aplicación del departamento de soporte técnico, consulte los datos de seguimiento para obtener mensajes de excepción detallados.

- Error al obtener la información de contexto de la ejecución. No se puede comprobar el registro del nombre de entidad de seguridad de servicio (SPN)

    Durante una operación de carga inicial, el portal de autoservicio recupera información de la cuenta, el parámetro Sitename de IIS y el valor ApplicationVirtualPath del sitio web de autoservicio para comprobar el SPN. Este mensaje de error se registra cuando uno o varios de estos atributos no son válidos.

- Error al comprobar el registro del nombre de entidad de seguridad de servicio (SPN). EventDetails:{ExceptionMessage}

    Este mensaje indica que se ha producido una excepción de seguridad al comprobar el SPN. Consulte la excepción contenida en los detalles del evento.

### <a name="108-domaincontrollererror"></a>108: DomainControllerError

Errores conocidos y posibles causas:

- Error al resolver el nombre de dominio {DomainName}, error de asignación de memoria.

    Para resolver el nombre de dominio, llama a la API de Windows `DsGetDcName`. Este mensaje se registra cuando esta API devuelve `ERROR_NOT_ENOUGH_MEMORY`, que indica un error de asignación de memoria.

- No se pudo invocar el método DsGetDcName

    Este mensaje indica que la API de `DsGetDcName` no está disponible en el host.

### <a name="109-webapprecoverydberror"></a>109: WebAppRecoveryDbError

Errores conocidos y posibles causas:

- Error al leer la configuración de la base de datos de recuperación. La cadena de conexión a la base de datos de recuperación no está configurada.

    Este mensaje indica que la información de la cadena de conexión de la base de datos de recuperación en `HKLM\Software\Microsoft\MBAM Server\Web\RecoveryDBConnectionString` no es válida. Compruebe el valor de la clave del Registro especificado.

Si ve alguno de los mensajes siguientes, compruebe si las credenciales del grupo de aplicaciones del servidor IIS pueden establecer una conexión con la base de datos de recuperación:

- DoesUserHaveMatchingRecoveryKey: error al obtener los identificadores de clave de recuperación de un usuario.
- QueryDriveRecoveryData: error al obtener los datos de recuperación de la unidad.
- QueryRecoveryKeyIdsForUser: error al obtener los identificadores de clave de recuperación de un usuario.
- Error al obtener el hash de contraseña de TPM de la base de datos de recuperación.

### <a name="110-webappcompliancedberror"></a>110: WebAppComplianceDbError

Errores conocidos y posibles causas:

- Error al leer la configuración de la base de datos de cumplimiento. La cadena de conexión a la base de datos de cumplimiento no está configurada.

    Este mensaje indica que la información de la cadena de conexión de la base de datos de cumplimiento en `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString` no es válida. Compruebe el valor de esta clave del Registro.

Si ve alguno de los mensajes siguientes, compruebe si las credenciales del grupo de aplicaciones del servidor IIS pueden establecer una conexión con la base de datos de cumplimiento:

- GetRecoveryKeyForCurrentUser: error al registrar un evento de auditoría en la base de datos de cumplimiento.
- QueryRecoveryKeyIdsForUser: error al registrar un evento de auditoría en la base de datos de cumplimiento.
- QueryRecoveryKeyIdsForUser: error al registrar un evento de auditoría en la base de datos de cumplimiento.

### <a name="111-webappdberror"></a>111: WebAppDbError

Estos errores indican una de las dos condiciones siguientes

- Los sitios web o los servicios web de MBAM no pudieron conectarse a la base de datos de cumplimiento o recuperación
- La cuenta de ejecución de sitios web o los servicios web de MBAM (cuenta del grupo de aplicaciones) no pudo ejecutar el procedimiento almacenado `GetVersion` en la base de datos de cumplimiento o recuperación

El mensaje contenido en el evento proporciona más detalles acerca de la excepción.

Compruebe que la cuenta del grupo de aplicaciones puede conectarse a las bases de datos de cumplimiento o recuperación. Confirme que tiene permisos para ejecutar el procedimiento almacenado `GetVersion`.

### <a name="112-webapperror"></a>112: WebAppError

Error al comprobar el registro del nombre de entidad de seguridad de servicio (SPN).

Para comprobar el SPN, consulta a Active Directory para recuperar una lista de la cuenta de ejecución asignada de SPN. También consulta `ApplicationHost.config` para obtener los enlaces del sitio web. Este mensaje de error indica que no pudo comunicarse con Active Directory o que no pudo cargar el archivo `ApplicationHost.config`.

Compruebe que la cuenta del grupo de aplicaciones tiene permisos para consultar Active Directory o el archivo `ApplicationHost.config`. Compruebe también las entradas de enlace de sitio en el archivo `ApplicationHost.config`.

## <a name="operational"></a>Operativo

### <a name="4-performancecountererror"></a>4: PerformanceCounterError

Error al recuperar un contador de rendimiento.

El mensaje de seguimiento contiene el mensaje de excepción real, algunos de los cuales se enumeran aquí:

- ArgumentNullException: Esta excepción se produce si la categoría, el contador o la instancia del contador de rendimiento solicitado no es válido.
- System.InvalidOperationException: categoryName es una cadena vacía (""). counterName es una cadena vacía ("").
- La configuración de permiso de lectura y escritura solicitada no es válida para este contador.
- La categoría especificada no existe (si readOnly es true).
- La categoría especificada no es una categoría personalizada de .NET Framework (si readOnly es false).
- La categoría especificada se marca como de varias instancias y requiere que el contador de rendimiento se cree con un nombre de instancia.
- El valor de instanceName tiene más de 127 caracteres.
- categoryName y counterName se han localizado en distintos idiomas.
- System.ComponentModel.Win32Exception: error al obtener acceso a una API del sistema.
- System.UnauthorizedAccessException: Código que se ejecuta sin privilegios administrativos intentó leer un contador de rendimiento.

El mensaje del evento proporciona más detalles sobre la excepción.

Para `System.UnauthorizedAccessException`, compruebe que la cuenta del grupo de aplicaciones tiene acceso a las API del contador de rendimiento.

### <a name="200-helpdeskinformation"></a>200: HelpDeskInformation

La aplicación de sitio web de administración encontró correctamente una versión compatible de la base de datos de recuperación/cumplimiento y se ha conectado a ella.

Indica una conexión correcta a la base de datos de recuperación o cumplimiento desde el sitio web del departamento de soporte técnico.

### <a name="201-selfserviceportalinformation"></a>201: SelfServicePortalInformation

La aplicación del portal de autoservicio encontró correctamente una versión compatible de la base de datos de recuperación/cumplimiento y se ha conectado a ella.

Indica una conexión correcta a la base de datos de recuperación o cumplimiento desde el portal de autoservicio.

### <a name="202-webappinformation"></a>202: WebAppInformation

Los SPN de la aplicación se han registrado correctamente.

Indica que los SPN necesarios para el sitio web del departamento de soporte técnico se han registrado correctamente en la cuenta de ejecución.

## <a name="see-also"></a>Vea también

Para obtener más información sobre el uso de estos registros, vea [Registros de eventos de BitLocker](about-event-logs.md).

Para obtener más información acerca de la solución de problemas, vea [Solución de problemas de BitLocker](troubleshoot.md).

Para obtener más información acerca de cómo instalar estos sitios web, consulte [Configuración de informes y portales de BitLocker](../../deploy-use/bitlocker/setup-websites.md).
