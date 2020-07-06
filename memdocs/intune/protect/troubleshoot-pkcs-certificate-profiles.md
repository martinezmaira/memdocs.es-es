---
title: Solución de problemas del uso de perfiles de certificado PKCS para aprovisionar certificados con Microsoft Intune | Microsoft Docs
description: Solución de problemas del uso de perfiles de pares de claves públicas y privadas (PKCS) por los dispositivos para solicitar el uso de certificados con Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/29/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7667cf1d62040c4435f41ffbe377452d3666a3ec
ms.sourcegitcommit: 411e9d93cbafc7585f5a0f9a05097fe589de804f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/24/2020
ms.locfileid: "85343122"
---
# <a name="troubleshoot-pkcs-certificate-deployment-in-microsoft-intune"></a>Solución de problemas de la implementación de certificados PKCS en Microsoft Intune

La información de este artículo puede ayudarlo a resolver varios problemas comunes al implementar certificados de pares de claves públicas y privadas (PKCS) en Microsoft Intune. Antes de solucionar los problemas, asegúrese de que ha completado las siguientes tareas descritas en [Configuración y uso de certificados PKCS con Intune](../protect/certficates-pfx-configure.md#export-the-root-certificate-from-the-enterprise-ca):

- Revisar los [requisitos de uso de los perfiles de certificado PKCS](../protect/certficates-pfx-configure.md#requirements)
- Exportar el certificado raíz desde la entidad de certificación (CA) empresarial
- Configuración de plantillas de certificado en la entidad de certificación
- Instalar y configurar Intune Certificate Connector
- Crear e implementar un perfil de certificado de confianza para implementar el certificado raíz
- Crear e implementar un perfil de certificado PKCS

La fuente más común de problemas de los perfiles de certificado PKCS ha sido la configuración del perfil de certificado PKCS. Revise la configuración de los perfiles y busque errores tipográficos en los nombres de servidor o nombres de dominio completos (FQDN), y confirme que los campos **Entidad de certificación** y **Nombre de la entidad de certificación** son correctos.

- **Entidad de certificación**: el FQDN interno del equipo de la entidad de certificación. Por ejemplo, server1.domain.local.
- **Nombre de la entidad de certificación**: el nombre de la entidad de certificación que se muestra en el MMC de la entidad de certificación. Mire en **Entidad de certificación (local)** .

Puede usar el [programa de línea de comandos certutil](https://docs.microsoft.com/windows-server/administration/windows-commands/certutil) en la CA para confirmar que la entidad de certificación y el nombre de la entidad de certificación son correctos.

## <a name="pkcs-communication-overview"></a>Introducción a la comunicación de PKCS

En el gráfico siguiente se proporciona una introducción al proceso de implementación de certificados PKCS en Intune.

> [!div class="mx-imgBorder"]
> ![Flujo del perfil de certificados PKCS](./media/troubleshoot-pkcs-certificate-profiles/pkcs-overview-graphic.png)

1. Un administrador crea un perfil de certificado PKCS en Intune.
2. El servicio de Intune solicita que la instancia local de Intune Certificate Connector cree un certificado para el usuario.
3. Intune Certificate Connector envía un blob y una solicitud PFX a la entidad de certificación de Microsoft.
4. La entidad de certificación emite el certificado de usuario PFX y lo envía de nuevo a Intune Certificate Connector.
5. Intune Certificate Connector carga el certificado de usuario PFX cifrado en Intune.
6. Intune descifra el certificado de usuario PFX y lo vuelve a cifrar para el dispositivo mediante el certificado de administración de dispositivos.  Luego, Intune envía el certificado de usuario PFX al dispositivo.
7. El dispositivo notifica el estado del certificado a Intune.

## <a name="data-and-log-files"></a>Archivos de datos y registro

Para identificar los problemas del flujo de trabajo de comunicación y aprovisionamiento de certificados, revise los archivos de registro de la infraestructura del servidor y de los servidores. En las secciones posteriores sobre la solución de problemas de perfiles de certificado PKCS se hace referencia a los archivos de registro mencionados en esta sección.

- [Registros de infraestructura y servidor](#logs-for-on-premises-infrastructure)

Los registros de dispositivos dependen de la plataforma del dispositivo:

- [iOS e iPadOS](#logs-for-ios-and-ipados-devices)
- [Android](#logs-for-android-devices)
- [Windows](#logs-for-windows-devices)

### <a name="logs-for-on-premises-infrastructure"></a>Registros para la infraestructura local
  
La infraestructura local que admite el uso de perfiles de certificado PKCS para las implementaciones de certificados incluye Microsoft Intune Certificate Connector, NDES que se ejecuta en una instancia de Windows Server y la entidad de certificación.

Los archivos de registro de estos roles incluyen el Visor de eventos de Windows, consolas de certificado y varios archivos de registro específicos de Intune Certificate Connector, NDES u otros roles y operaciones que forman parte de la infraestructura local.

- **NDESConnector_date_time.svclog**:

  Este registro muestra la comunicación desde Microsoft Intune Certificate Connector al servicio en la nube de Intune. Puede usar la [herramienta del visor de seguimiento de servicio](https://docs.microsoft.com/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) para ver este archivo de registro.

  Clave del Registro relacionada: *HKLM\SW\Microsoft\MicrosoftIntune\NDESConnector\ConnectionStatus*

  Ubicación: en el servidor que hospeda NDES en *%program_files%\Microsoft intune\ndesconnectorsvc\logs\logs*

- **CertificateRegistrationPoint_date_time.svclog**:

  este registro muestra el módulo de directivas de NDES que recibe y comprueba las solicitudes de certificado. Puede usar la [herramienta del visor de seguimiento de servicio](https://docs.microsoft.com/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) para ver este archivo de registro.

  Ubicación: en el servidor que hospeda NDES en *%program_files%\Microsoft intune\ndesconnectorsvc\logs\logs*

- **NDESPlugin.log**:

  este registro muestra el paso de las solicitudes de certificado al punto de registro de certificados y la comprobación que resulta de esas solicitudes.

  Ubicación: en el servidor que hospeda NDES en *%program_files%\Microsoft Intune\NDESPolicyModule\logs*

- **Registro de aplicaciones para Windows**:

  Ubicación: En el servidor que hospeda NDES: ejecute **eventvwr.msc** para abrir el Visor de eventos de Windows

### <a name="logs-for-android-devices"></a>Aplicaciones para dispositivos Android

En el caso de los dispositivos que ejecutan Android, use el archivo de registro de la aplicación **Portal de empresa de Android**, **OMADM.log**. Antes de recopilar y revisar registros, asegúrese de que la opción [Registro detallado](../user-help/use-verbose-logging-to-help-your-it-administrator-fix-device-issues-android.md) esté habilitada y, luego, reproduzca el problema.

Para recopilar OMADM.logs desde un dispositivo, consulte [Carga y envío por correo electrónico de los registros mediante un cable USB](../user-help/send-logs-to-your-it-admin-using-cable-android.md).

También puede consultar la sección sobre [carga y envío por correo electrónico de los registros](../user-help/send-logs-to-your-it-admin-by-email-android.md#upload-and-email-logs-from-microsoft-intune-app) para más ayuda.

### <a name="logs-for-ios-and-ipados-devices"></a>Registros para dispositivos iOS e iPadOS

En el caso de los dispositivos que ejecutan iOS/iPadOS, puede usar registros de depuración y **Xcode** que se ejecuta en un equipo Mac:

1. Conecte el dispositivo iOS/iPadOS con el equipo Mac y, luego, vaya a **Aplicaciones** > **Utilidades** para abrir la aplicación de consola.

2. En **Acción**, seleccione **Incluir mensajes de información** e **Incluir mensajes de depuración**.

   ![Selección de opciones de registro](../protect/media/troubleshoot-pkcs-certificate-profiles/message-options.png)

3. Reproduzca el problema y, a continuación, guarde los registros en un archivo de texto:
   1. Seleccione **Editar** > **Seleccionar todo** para seleccionar todos los mensajes de la pantalla actual y, luego, seleccione **Editar** > **Copiar** para copiar los mensajes en el Portapapeles.
   2. Abra la aplicación TextEdit, pegue los registros copiados en un archivo de texto nuevo y, a continuación, guarde el archivo.

El registro del Portal de empresa para dispositivos iOS y iPadOS no contiene información sobre los perfiles de certificado PKCS.

### <a name="logs-for-windows-devices"></a>Registros para dispositivos Windows

En el caso de los dispositivos que ejecutan Windows, use los registros de eventos de Windows para diagnosticar problemas de inscripción o de administración de dispositivos en los dispositivos que administra con Intune.

En el dispositivo, abra **Visor de eventos** > **Registros de aplicaciones y servicios-**  > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostics-Provider**

![Registros de eventos de Windows](../protect/media/troubleshoot-pkcs-certificate-profiles/windows-event-log.png)

## <a name="common-errors"></a>Errores comunes

A continuación, se indican los errores comunes que se tratan en la sección siguiente:

- [El servidor RPC no está disponible 0x800706ba](#the-rpc-server-is-unavailable-0x800706ba)
- [No se encuentra un servidor de directivas de inscripción 0x80094015](#an-enrollment-policy-server-cannot-be-located-0x80094015)
- [El envío está pendiente](#the-submission-is-pending)
- [El parámetro no es correcto 0x80070057](#the-parameter-is-incorrect-0x80070057)
- [Denegado por el módulo de directivas](#denied-by-policy-module)
- [Certificate profile stuck as Pending](#certificate-profile-stuck-as-pending) (Perfil de certificado bloqueado como pendiente)
- [Error: 2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED](#error--2146875374-certsrv_e_subject_email_required)

### <a name="the-rpc-server-is-unavailable-0x800706ba"></a>El servidor RPC no está disponible 0x800706ba

Durante la implementación de PFX, el certificado raíz de confianza aparece en el dispositivo, pero el certificado PFX no. El archivo de registro de NDESConnector contiene la cadena **El servidor RPC no está disponible. 0x800706ba**, que se muestra en la primera línea del ejemplo siguiente:

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x800706BA): CCertRequest::Submit: The RPC server is unavailable. 0x800706ba (WIN32: 1722 RPC_S_SERVER_UNAVAILABLE)
IssuePfx -Generic Exception: System.ArgumentException: CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094800): The requested certificate template is not supported by this CA. (Exception from HRESULT: 0x80094800)
```

#### <a name="cause-1---incorrect-configuration-of-the-ca-in-intune"></a>Causa 1: Configuración incorrecta de la entidad de certificación en Intune

Este problema puede producirse cuando el perfil de certificado PKCS especifica el servidor equivocado o contiene errores ortográficos en el nombre o el FQDN de la entidad de certificación. La entidad de certificación se especifica en las siguientes propiedades del perfil:

- Certification authoity
- Nombre de la entidad de certificación

**Solución**:

Revise la configuración siguiente y corríjala si es incorrecta:

- La propiedad **Entidad de certificación** muestra el nombre de dominio completo interno del servidor de la entidad de certificación.
- La propiedad **Nombre de la entidad de certificación** muestra el nombre de la entidad de certificación.

#### <a name="cause-2---ca-doesnt-support-certificate-renewal-for-requests-signed-by-previous-ca-certificates"></a>Causa 2: La entidad de certificación no admite la renovación de certificados de las solicitudes firmadas con certificados de la entidad de certificación anteriores

Si el FQDN y el nombre de la entidad de certificación son correctos en el perfil de certificado PKCS, revise el registro de aplicación de Windows que se encuentra en el servidor de la entidad de certificación. Busque un **Id. de evento 128** similar al ejemplo siguiente:

```
Log Name: Application:
Source: Microsoft-Windows-CertificationAuthority
Event ID: 128
Level: Warning
Details:
An Authority Key Identifier was passed as part of the certificate request 2268. This feature has not been enabled. To enable specifying a CA key for certificate signing, run: "certutil -setreg ca\UseDefinedCACertInRequest 1" and then restart the service.
```

Cuando se renueva el certificado de la entidad de certificación, se debe firmar el certificado de firma de respuesta del Protocolo de estado de certificado en línea (OCSP). La firma permite que el certificado de firma de respuesta de OCSP valide otros certificados mediante la comprobación de su estado de revocación. Esta firma no está habilitada de forma predeterminada.

**Solución**:

Fuerce la firma manual del certificado:

1. En el servidor de CA, abra un símbolo del sistema con privilegios elevados y ejecute el siguiente comando **certutil-setreg ca\UseDefinedCACertInRequest 1**.
2. Reinicie el servicio Servicios de Certificate Server.

A continuación de ello, los dispositivos pueden recibir certificados.

### <a name="an-enrollment-policy-server-cannot-be-located-0x80094015"></a>No se encuentra un servidor de directivas de inscripción 0x80094015

**No se encuentra un servidor de directivas de inscripción** y **0x80094015**, como en el ejemplo siguiente:

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094015): An enrollment policy server cannot be located. (Exception from HRESULT: 0x80094015)
```

#### <a name="cause---certificate-enrollment-policy-server-name"></a>Causa: El nombre del servidor de directivas de inscripción de certificados

Este problema se produce si el equipo que hospeda Intune NDES Connector no encuentra un servidor de directivas de inscripción de certificados.

**Solución**:

Configure manualmente el nombre del servidor de directivas de inscripción de certificados en el equipo que hospeda el conector NDES. Para configurar el nombre, use el cmdlet de PowerShell [Add-CertificateEnrollmentPolicyServer](https://docs.microsoft.com/powershell/module/pkiclient/add-certificateenrollmentpolicyserver?view=win10-ps).

### <a name="the-submission-is-pending"></a>El envío está pendiente

Después de implementar un perfil de certificado PKCS en los dispositivos móviles, no se adquieren los certificados y el registro NDESConnector contiene la cadena **El envío está pendiente**, como en el ejemplo siguiente:

```
IssuePfx - The submission is pending: Taken Under Submission
IssuePfx -Generic Exception: System.InvalidOperationException: IssuePfx - The submission is pending
```

Además, en el servidor de la entidad de certificación, puede ver la solicitud PFX en la carpeta **Solicitudes pendientes**:

> [!div class="mx-imgBorder"]
> ![Captura de pantalla de la carpeta de solicitudes pendientes de la entidad de certificación](./media/troubleshoot-pkcs-certificate-profiles/pending-requests.png)

#### <a name="cause---incorrect-configuration-for-request-handling"></a>Causa: Configuración incorrecta de la administración de solicitudes

Este problema se produce si la opción **Establecer el estado de solicitud de certificado en pendiente. El administrador debe emitir el certificado explícitamente** está seleccionada en el cuadro de diálogo **Propiedades** > **Módulo de directivas** > **Propiedades** de la entidad de certificación.

> [!div class="mx-imgBorder"]
> ![Captura de pantalla de las propiedades del módulo de directivas](./media/troubleshoot-pkcs-certificate-profiles/policy-module-properties.png)

**Solución**:

Edite las propiedades del módulo de directivas para establecer: **Seguir la configuración de la plantilla de certificados, si procede. En caso contrario, emitir el certificado automáticamente.**

### <a name="the-parameter-is-incorrect-0x80070057"></a>El parámetro no es correcto 0x80070057

Aunque Intune Certificate Connector está instalado y configurado correctamente, los dispositivos no reciben certificados PKCS y el registro NDESConnector contiene la cadena **El parámetro no es correcto. 0x80070057**, como en el ejemplo siguiente:

```
CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
```

#### <a name="cause---configuration-of-the-pkcs-profile"></a>Causa: Configuración del perfil PKCS

Este problema se produce si el perfil PKCS de Intune no está configurado correctamente. Estos son los errores de configuración más comunes:

- El perfil incluye un nombre incorrecto de la entidad de certificación.
- El nombre alternativo del firmante (SAN) está configurado para la dirección de correo electrónico, pero el usuario de destino no tiene aún una dirección de correo electrónico válida. Esta combinación da como resultado un valor NULL para el SAN, que no es válido.

**Solución**:

Compruebe las siguientes configuraciones del perfil PKCS y, luego, espere a que la directiva se actualice en el dispositivo:

- Configurado con el nombre de la entidad de certificación
- Asignado al grupo de usuarios correcto
- Los usuarios del grupo tienen direcciones de correo electrónico válidas

Para más información, consulte [Configuración y uso de certificados PKCS con Intune](../protect/certficates-pfx-configure.md).

### <a name="denied-by-policy-module"></a>Denegado por el módulo de directivas

Cuando los dispositivos reciben el certificado raíz de confianza, pero no reciben el certificado PFX, el registro NDESConnector contiene la cadena **Error de envío: Denegado por el módulo de directivas**, como en el ejemplo siguiente:

```
IssuePfx - The submission failed: Denied by Policy Module
IssuePfx -Generic Exception: System.InvalidOperationException: IssuePfx - The submission failed
   at Microsoft.Management.Services.NdesConnector.MicrosoftCA.GetCertificate(PfxRequestDataStorage pfxRequestData, String containerName, String& certificate, String& password)
Issuing Pfx certificate for Device ID <Device ID> failed  
```

#### <a name="cause--computer-account-permissions-to-the-certificate-template"></a>Causa: Los permisos de la cuenta de equipo para la plantilla de certificado

Este problema se produce cuando la cuenta de equipo del servidor que hospeda Intune Certificate Connector no tiene permisos para la plantilla de certificado.

**Solución**:

1. Inicie sesión en la entidad de certificación empresarial con una cuenta que tenga privilegios de administración.
2. Abra la consola de **Entidad de certificación**, haga clic con el botón derecho en **Plantillas de certificado y seleccione Administrar**.
3. Busque la plantilla de certificado y abra el cuadro de diálogo **Propiedades** de la plantilla.
4. En la pestaña **Seguridad**, agregue la cuenta de equipo del servidor donde instaló Microsoft Intune Certificate Connector. Conceda a esa cuenta los permisos de **Lectura** e **Inscripción**.
5. Seleccione **Aplicar** > **Aceptar** para guardar la plantilla de certificado y, luego, cierre la consola de **Plantillas de certificado**.
6. En la consola de la **entidad de certificación**, haga clic con el botón derecho en **Plantillas de certificado** > **Nuevo** > **Plantilla de certificado que se va a emitir**.
7. Seleccione la plantilla que ha modificado y, luego, haga clic en **Aceptar**.

Para más información, consulte [Configuración de plantillas de certificado en la CA](../protect/certficates-pfx-configure.md#configure-certificate-templates-on-the-ca).

### <a name="certificate-profile-stuck-as-pending"></a>Certificate profile stuck as Pending (Perfil de certificado bloqueado como pendiente)

En el centro de administración de Microsoft Endpoint Manager, los perfiles de certificado PKCS no se implementan y se muestra el estado **Pendiente**. No hay errores obvios en el archivo de registro de NDESConnector.
Dado que la causa de este problema no se identifica claramente en los registros, trabaje con algunas de estas causas.

#### <a name="cause-1---unprocessed-request-files"></a>Causa 1: Archivos de solicitud sin procesar

Revise los archivos de solicitud para ver si hay errores que indiquen el motivo de que no se hayan podido procesar.

1. En el equipo que hospeda el conector de NDES, use el explorador de archivos para ir a **%programfiles%\Microsoft Intune\PfxRequest**.
2. Revise los archivos de las carpetas **Con error** y **Procesando** carpetas con el editor de texto que prefiera.

   > [!div class="mx-imgBorder"]
   > ![Revisión de la carpeta PfxRequest](./media/troubleshoot-pkcs-certificate-profiles/pfxrequest-folder.png)

3. En estos archivos, busque entradas que indiquen errores o que sugieran problemas. Mediante una búsqueda basada en web, examine los mensajes de error en busca de pistas sobre el error de procesamiento de la solicitud y para encontrar soluciones a dichos problemas.

#### <a name="cause-2---misconfiguration-for-the-pkcs-certificate-profile"></a>Causa 2: Error de configuración del perfil de certificado PKCS

Cuando no se encuentren los archivos de solicitud en las carpetas **Con error**, **Procesando** o **Correcto**, puede que la causa sea que no está asociado el certificado correcto con el perfil de certificado PKCS. Por ejemplo, una entidad de certificación subordinada está asociada con el perfil o se usa el certificado raíz equivocado.

**Solución**:

1. Revise el perfil de certificado de confianza para asegurarse de que ha implementado el certificado raíz de la entidad de certificación empresarial en los dispositivos.
2. Revise el perfil de certificado PKCS para asegurarse de que hace referencia a la entidad de certificación y al tipo de certificado correctos, así como al perfil de certificado de confianza que implementa el certificado raíz en los dispositivos.

Para más información, consulte [Uso de certificados para la autenticación](../protect/certificates-configure.md) en Microsoft Intune.

### <a name="error--2146875374-certsrv_e_subject_email_required"></a>Error: 2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED

Los certificados PKCS no se implementan y la consola de certificados de la entidad de certificación emisora muestra un mensaje con la cadena **-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED**, como en el ejemplo siguiente:

```
Active Directory Certificate Services denied request abc123 because The Email name is unavailable and cannot be added to the Subject or Subject Alternate name. 0x80094812 (-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED). The request was for CN=” Common Name”.  Additional information: Denied by Policy Module”.
```

#### <a name="cause---supply-in-the-request-is-miscongifured"></a>Causa: Error de configuración de "Proporcionado por el solicitante"

Este problema se produce si la opción **Proporcionado por el solicitante** no está habilitado en la pestaña **Nombre de sujeto** en el cuadro de diálogo **Propiedades** de la plantilla de certificado.

> [!div class="mx-imgBorder"]
> ![Configuración de las propiedades de NDES](./media/troubleshoot-pkcs-certificate-profiles/supply-in-the-request.png)

**Solución**:

Edite la plantilla para resolver el problema de configuración:

1. Inicie sesión en la entidad de certificación empresarial con una cuenta que tenga privilegios de administración.
2. En la consola de la **entidad de certificación**, haga clic con el botón derecho en **Plantillas de certificado** y seleccione **Administrar**.
3. Abra el cuadro de diálogo Propiedades de la plantilla de certificado.
4. En la pestaña **Nombre del firmante** , seleccione **Proporcionado por el solicitante**.
5. Seleccione **Aceptar** para guardar la plantilla de certificado y, luego, cierre la consola de **Plantillas de certificado**.
6. En la consola de **Entidad de certificación**, haga clic con el botón derecho en **Plantillas** > **Nuevo** > **Plantilla de certificado que se va a emitir**.
7. Seleccione la plantilla que ha modificado y, luego, elija **Aceptar**.

## <a name="next-steps"></a>Pasos siguientes

Si todavía necesita una solución o busca más información sobre Intune, publique una pregunta en nuestro [foro de Microsoft Intune](https://social.technet.microsoft.com/Forums/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc). Muchos ingenieros de soporte técnico, MVP y miembros de nuestro equipo de desarrollo frecuentan los foros, así que es una buena oportunidad para que alguien pueda ayudarlo.

Para abrir una solicitud de soporte técnico con el equipo de soporte técnico de productos de Microsoft Intune, consulte [Cómo obtener asistencia para Microsoft Intune](../fundamentals/get-support.md).
Para más información sobre la implementación de certificados PKCS, consulte los siguientes artículos:

- [Configuración y uso de certificados PKCS con Intune](../protect/certficates-pfx-configure.md)
- [Configuración de un perfil de certificado para sus dispositivos en Microsoft Intune](../protect/certificates-configure.md)
- [Eliminación de certificados SCEP y PKCS en Microsoft Intune](../protect/remove-certificates.md)
