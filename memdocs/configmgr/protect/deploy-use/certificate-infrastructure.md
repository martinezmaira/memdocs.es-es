---
title: Configuración de la infraestructura de certificados
titleSuffix: Configuration Manager
description: Aprenda a configurar la inscripción de certificado en Configuration Manager.
ms.date: 07/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 29ae59b7-2695-4a0f-a9ff-4f29222f28b3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 656cc80c929eb7e829dd06b642a83cb174d3b0c8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697252"
---
# <a name="configure-certificate-infrastructure"></a>Configuración de la infraestructura de certificados

*Se aplica a: Configuration Manager (rama actual)*

Aprenda a configurar la infraestructura de certificados en Configuration Manager. Antes de empezar, compruebe los requisitos previos que se indican en [Requisitos previos para perfiles de certificado](../../protect/plan-design/prerequisites-for-certificate-profiles.md).  

Siga estos pasos para configurar la infraestructura de certificados SCEP o PFX.

## <a name="step-1---install-and-configure-the-network-device-enrollment-service-and-dependencies-for-scep-certificates-only"></a>Paso 1: instalar y configurar el Servicio de inscripción de dispositivos de red y dependencias (solo para certificados SCEP)

 Debe instalar y configurar el servicio de rol Servicio de inscripción de dispositivos de red para Servicios de certificados de Active Directory (AD CS), cambiar los permisos de seguridad en las plantillas de certificado, implementar un certificado de autenticación de cliente de infraestructura de clave pública (PKI) y editar el Registro para aumentar el límite del tamaño predeterminado de dirección URL de Internet Information Services (IIS). En caso necesario, también debe configurar la entidad de certificación (CA) emisora para que permita un periodo de validez personalizado.  

> [!IMPORTANT]  
>  Antes de configurar Configuration Manager para funcionar con el Servicio de inscripción de dispositivos de red, compruebe la instalación y la configuración de este servicio. Si estas dependencias no funcionan correctamente, tendrá dificultades para solucionar problemas de inscripción de certificados mediante Configuration Manager.  

### <a name="to-install-and-configure-the-network-device-enrollment-service-and-dependencies"></a>Para instalar y configurar el Servicio de inscripción de dispositivos de red y dependencias  

1. En un servidor que ejecute Windows Server 2012 R2, instale y configure el servicio de rol Servicio de inscripción de dispositivos de red para el rol de servidor Servicios de certificados de Active Directory. Para obtener más información, vea [Instrucciones del servicio de inscripción de dispositivos de red](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498\(v=ws.11\)).

2. Compruebe y, si es necesario, modifique los permisos de seguridad para las plantillas de certificado que está utilizando el Servicio de inscripción de dispositivos de red:  

   -   Para la cuenta que ejecuta la consola de Configuration Manager: el permiso **Leer**.  

        Este permiso es necesario para que cuando ejecute el Asistente para crear perfil de certificado, pueda examinar y seleccionar la plantilla de certificado que desee usar al crear un perfil de configuración de SCEP. Al seleccionar una plantilla de certificado, determinadas opciones del asistente se rellenarán automáticamente, por lo que deberá configurar menos opciones y la probabilidad de seleccionar opciones no compatibles con las plantillas de certificado que el Servicio de inscripción de dispositivos de red utiliza será menor.  

   -   Para la cuenta de servicio SCEP que el grupo de aplicaciones del Servicio de inscripción de dispositivos de red utiliza: los permisos **Leer** e **Inscribir**.  

        Este requisito no es específico de Configuration Manager, sino que es parte de la configuración del Servicio de inscripción de dispositivos de red. Para obtener más información, vea [Instrucciones del servicio de inscripción de dispositivos de red](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498\(v=ws.11\)).  

   > [!TIP]  
   >  Para identificar las plantillas de certificado que el Servicio de inscripción de dispositivos de red utiliza, consulte la siguiente clave del Registro en el servidor que ejecuta el Servicio de inscripción de dispositivos de red: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP.  

   > [!NOTE]  
   >  Estos son los permisos de seguridad predeterminados que serán adecuados para la mayoría de los entornos. Sin embargo, puede utilizar otra configuración de seguridad. Para más información, consulte [Planeamiento de permisos de plantilla de certificado para perfiles de certificado](../../protect/plan-design/planning-for-certificate-template-permissions.md).  

3. Implemente un certificado PKI que admita la autenticación de cliente en este servidor. Es posible que ya tenga instalado en el equipo un certificado adecuado que pueda utilizar, o tal vez precise o prefiera implementar un certificado especialmente para este propósito. Para más información sobre los requisitos de este certificado, consulte los detalles en Servidores que ejecutan el módulo de directivas de Configuration Manager con el servicio de rol Servicio de inscripción de dispositivos de red en la sección **Certificados PKI para servidores** en el tema [Requisitos de certificados PKI para Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md).  

   > [!TIP]
   >  Si necesita ayuda en la implementación de este certificado, puede usar las instrucciones de [Deploying the Client Certificate for Distribution Points (Implementación del certificado de cliente para puntos de distribución)](../../core/plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012), ya que los requisitos del certificado son los mismos, con una excepción:  
   > 
   > - No active la casilla **Permitir que la clave privada se pueda exportar** en la pestaña **Tratamiento de la solicitud** de las propiedades de la plantilla de certificado.  
   > 
   >   No tiene que exportar este certificado con la clave privada, porque podrá buscar en el almacén del equipo local y seleccionarlo al configurar el módulo de directivas de Configuration Manager.  

4. Busque el certificado raíz al que se vincula el certificado de autenticación del cliente. A continuación, exporte este certificado de CA raíz a un archivo de certificado (.cer). Guarde este archivo en una ubicación protegida a la que posteriormente pueda acceder de forma segura para instalar y configurar el servidor del sistema de sitios del punto de registro de certificado.  

5. En el mismo servidor, use el Editor del Registro para aumentar el límite del tamaño predeterminado de la dirección URL de IIS. Para ello, configure los valores DWORD de la siguiente clave del Registro en HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\HTTP\Parameters:  

   - Establezca la clave **MaxFieldLength** en **65534**.  

   - Establezca la clave **MaxRequestBytes** en **16777216**.  

     Para obtener más información, vea el artículo de Soporte técnico de Microsoft [820129: Configuración del Registro http.sys para Windows](https://support.microsoft.com/help/820129).

6. En el mismo servidor, en el Administrador de Internet Information Services (IIS), modifique la configuración de filtrado de solicitudes de la aplicación /certsrv/mscep y, a continuación, reinicie el servidor. En el cuadro de diálogo **Modificar configuración del filtrado de solicitudes** , los valores en **Límites de las solicitudes** deben ser los siguientes:  

   - **Longitud de contenido máxima permitida (bytes)** : **30000000**  

   - **Longitud máxima de dirección URL (bytes)** : **65534**  

   - **Cadena de consulta máxima (bytes)** : **65534**  

     Para obtener más información sobre estas opciones y cómo configurarlas, vea [Límites de solicitudes de IIS](/iis/configuration/system.webServer/security/requestFiltering/requestLimits/).

7. Si desea poder solicitar un certificado con un período de validez inferior al de la plantilla de certificado que está utilizando: Esta configuración está deshabilitada de forma predeterminada para una entidad de certificación (CA) empresarial. Para habilitar esta opción en una CA empresarial, utilice la herramienta de línea de comandos Certutil y, a continuación, detenga y reinicie el servicio de certificado mediante el uso de los comandos siguientes:  

   1. **certutil - setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE**  

   2. **net stop certsvc**  

   3. **net start certsvc**  

      Para obtener más información, vea [Herramientas y configuración de servicios de certificados](/previous-versions/windows/it-pro/windows-server-2003/cc780742\(v=ws.10\)).

8. Compruebe que el Servicio de inscripción de dispositivos de red funciona, mediante el vínculo siguiente de ejemplo: `https://server.contoso.com/certsrv/mscep/mscep.dll`. Se debería visualizar la página web integrada de Servicio de inscripción de dispositivos de red. En esta página web se define el servicio y se indica que los dispositivos de red utilizan la dirección URL para enviar solicitudes de certificados.  

   Ahora que están configurados el Servicio de inscripción de dispositivos de red y las dependencias, está listo para instalar y configurar el punto de Registro de certificado.


## <a name="step-2---install-and-configure-the-certificate-registration-point"></a>Paso 2: Instalar y configurar el punto de Registro de certificado

Debe instalar y configurar al menos un punto de registro de certificados en la jerarquía de Configuration Manager. Puede instalar el rol de sistema de sitio en el sitio de administración central o en un sitio primario.  

> [!IMPORTANT]  
>  Antes de instalar el punto de registro de certificado, consulte la sección **Requisitos del sistema de sitio** en el tema [Configuraciones admitidas para Configuration Manager](../../core/plan-design/configs/supported-configurations.md) para más información sobre los requisitos de sistema operativo y las dependencias del punto de registro de certificado.  

##### <a name="to-install-and-configure-the-certificate-registration-point"></a>Para instalar y configurar el punto de Registro de certificado  

1. En la consola de Configuration Manager, haga clic en **Administración**.  

2. En el área de trabajo **Administración** , expanda **Configuración del sitio**, haga clic en **Servidores y roles del sistema de sitios**y, a continuación, seleccione el servidor que desee usar para el punto de Registro de certificado.  

3. En la pestaña **Inicio** , en el grupo **Servidor** , haga clic en **Agregar roles del sistema de sitio**.  

4. En la página **General** , especifique la configuración general del sistema de sitio y, a continuación, haga clic en **Siguiente**.  

5. En la página **Proxy** , haga clic en **Siguiente**. El punto de Registro de certificado no utiliza la configuración de proxy de Internet.  

6. En la página **Selección de rol del sistema** , seleccione **Punto de Registro de certificado** en la lista de roles disponibles y, a continuación, haga clic en **Siguiente**. 

7. En la página **Modo de registro de certificados**, seleccione si desea que este registro de certificado apunte a **Procesar solicitudes de certificado SCEP** o **Procesar solicitudes de certificado PFX**. Un punto de registro de certificados no puede procesar ambos tipos de solicitudes, pero se pueden crear varios puntos de registro de certificado si trabaja con ambos tipos de certificados.

   Si se procesan certificados PFX, debe elegir una entidad de certificación: Microsoft o Entrust.

8. La página **Configuración de punto de Registro de certificado** varía según el tipo de certificado:
   - Si ha seleccionado **Procesar solicitudes de certificado SCEP**, configure lo siguiente:
     -   **Nombre del sitio web**, **Número de puerto HTTPS** y **Nombre de aplicación virtual** para el punto de registro de certificado. Estos campos se rellenan automáticamente con los valores predeterminados. 
     -   **Dirección URL para el Servicio de inscripción de dispositivos de red y certificado de CA raíz**: haga clic en **Agregar** y, en el cuadro de diálogo **Agregar dirección URL y certificado de CA raíz**, especifique lo siguiente:
         - **Dirección URL para el Servicio de inscripción de dispositivos de red**: escriba la dirección URL en este formato: https:// *<FQDN_de_servidor>* /certsrv/mscep/mscep.dll. Por ejemplo, si el FQDN del servidor que ejecuta el Servicio de inscripción de dispositivos de red es server1.contoso.com, escriba `https://server1.contoso.com/certsrv/mscep/mscep.dll`.
         - **Certificado de CA raíz**: Busque y seleccione el archivo de certificado (.cer) que creó y guardó en el **Paso 1: Instalar y configurar el Servicio de inscripción de dispositivos de red y dependencias**. Este certificado de CA raíz permite al punto de registro de certificados validar el certificado de autenticación de cliente que el módulo de directivas de Configuration Manager usará.  

   - Si seleccionó **Procesar solicitudes de certificado PFX**, configure los detalles de conexión y las credenciales de la entidad de certificación elegida.

     - Para utilizar Microsoft como la entidad de certificación, haga clic en **Agregar** y, en el cuadro de diálogo **Agregar una entidad de certificación y una cuenta**, especifique lo siguiente:
         - **Nombre del servidor de entidad de certificación**: escriba el nombre de su servidor de entidad de certificación.
         - **Cuenta de entidad de certificación**: haga clic en **Establecer** para seleccionar o crear la cuenta que tenga permisos para inscribirse en las plantillas de la entidad de certificación.
         - **Cuenta de conexión de Punto de Registro de certificado**: selecciona o crea la cuenta que conecta el punto de registro de certificados con la base de datos de Configuration Manager. De forma alternativa, puede usar la cuenta del equipo local en que se hospeda el punto de registro de certificados.
         - **Cuenta de publicación de certificados de Active Directory**: seleccione una cuenta o cree una nueva cuenta que se usará para publicar certificados en objetos de usuario en Active Directory.

         - En el cuadro de diálogo **Dirección URL para el Servicio de inscripción de dispositivos de red y certificado de CA raíz**, especifique lo siguiente y, luego, haga clic en **Aceptar**:  

     - Para usar Entrust como la entidad de certificación, especifique lo siguiente:

       - La **URL de servicio web de MDM**
       - Las credenciales de nombre de usuario y contraseña para la dirección URL.

         Cuando se utiliza la API de MDM para definir la URL de servicio web de Entrust, asegúrese de usar, como mínimo, la versión 9 de la API, tal y como se muestra en el ejemplo siguiente:

         `https://entrust.contoso.com:19443/mdmws/services/AdminServiceV9`

         Las versiones anteriores de la API no son compatibles con Entrust.

9. Haga clic en **Siguiente** y complete el asistente.  

10. Espere unos minutos para completar la instalación y, a continuación, compruebe que el punto de registro de certificado se instaló correctamente mediante cualquiera de los métodos siguientes:  

    -   En el área de trabajo **Supervisión** , expanda **Estado del sistema**, haga clic en **Estado del componente**y busque mensajes de estado del componente **SMS_CERTIFICATE_REGISTRATION_POINT** .  

    -   En el servidor de sistema de sitio, use el archivo *<ruta de instalación de Configuration Manager\>* \Logs\crpsetup.log y el archivo *<ruta de instalación de Configuration Manager\>* \Logs\crpmsi.log. Una instalación correcta devolverá un código de salida de 0.  

    -   Mediante un explorador, compruebe que puede conectarse a la dirección URL del punto de registro de certificados. Por ejemplo, `https://server1.contoso.com/CMCertificateRegistration`. Se debería visualizar una página de **error del servidor** para el nombre de la aplicación, con una descripción de HTTP 404.  

11. Busque el archivo de certificado exportado para la CA raíz que el punto de registro de certificado creó automáticamente en la carpeta siguiente en el equipo del servidor de sitio primario: *<ruta de instalación de Configuration Manager\>* \inboxes\certmgr.box. Guarde este archivo en una ubicación protegida a la que pueda acceder de forma segura posteriormente cuando instale el módulo de directivas de Configuration Manager en el servidor que ejecuta el Servicio de inscripción de dispositivos de red.  

    > [!TIP]  
    >  Este certificado no está disponible inmediatamente en esta carpeta. Es posible que tenga que esperar (por ejemplo, media hora) para que Configuration Manager copie el archivo en esta ubicación.  


## <a name="step-3----install-the-configuration-manager-policy-module-for-scep-certificates-only"></a>Paso 3: Instalar el módulo de directivas de Configuration Manager (solo para certificados SCEP).

Debe instalar y configurar el módulo de directivas de Configuration Manager en cada servidor que especificara en el **Paso 2: Instalar y configurar el punto de Registro de certificado** como **Dirección URL para el Servicio de inscripción de dispositivos de red** en las propiedades del punto de registro de certificado.  

##### <a name="to-install-the-policy-module"></a>Para instalar el módulo de directivas  

1. En el servidor que ejecuta el Servicio de inscripción de dispositivos de red, inicie sesión como administrador del dominio y copie los siguientes archivos de la carpeta <ConfigMgrInstallationMedia\>\SMSSETUP\POLICYMODULE\X64 del medio de instalación de Configuration Manager en una carpeta temporal:  

   -   PolicyModule.msi  

   -   PolicyModuleSetup.exe  

   Además, si tiene una carpeta LanguagePack en el medio de instalación, copie esta carpeta y su contenido.  

2. Desde la carpeta temporal, ejecute PolicyModuleSetup.exe para iniciar el Asistente para instalación de módulo de directivas de Configuration Manager.  

3. En la página inicial del asistente, haga clic en **Siguiente**, acepte los términos de licencia y, a continuación, haga clic en **Siguiente**.  

4. En la página **Carpeta de instalación** , acepte la carpeta de instalación predeterminada para el módulo de directivas o especifique una carpeta alternativa. A continuación, haga clic en **Siguiente**.  

5. En la página **Punto de registro de certificado** , especifique la dirección URL del punto de registro de certificado. Para ello, use el FQDN del servidor del sistema de sitios y el nombre de la aplicación virtual especificado en las propiedades del punto de registro de certificado. El nombre de la aplicación virtual predeterminado es CMCertificateRegistration. Por ejemplo, si el servidor del sistema de sitio tiene el FQDN server1.contoso.com y ha usado el nombre de la aplicación virtual predeterminada, especifique `https://server1.contoso.com/CMCertificateRegistration`.

6. Acepte el puerto predeterminado **443** o especifique otro número de puerto que use el punto de Registro de certificado. A continuación, haga clic en **Siguiente**.  

7. En la página **Certificado de cliente para el módulo de directivas**, busque y especifique el certificado de autenticación de cliente implementado en el **Paso 1: Instalar y configurar el Servicio de inscripción de dispositivos de red y las dependencias** y, a continuación, haga clic en **Siguiente**.  

8. En la página **Certificado del punto de registro de certificado**, haga clic en **Examinar** para seleccionar el archivo de certificado exportado para la CA raíz que encontró y guardó al final del **Paso 2: Instalar y configurar el punto de Registro de certificado**.  

   > [!NOTE]  
   >  Si no guardó anteriormente este archivo de certificado, lo encontrará en <ruta de instalación de Configuration Manager\>\inboxes\certmgr.box, en el equipo del servidor de sitio.  

9. Haga clic en **Siguiente** y complete el asistente.  

   Si quiere desinstalar el módulo de directivas de Configuration Manager, use **Programas y características** en el Panel de control. 

 
Ahora que ha completado los pasos de configuración, está listo para implementar certificados para usuarios y dispositivos mediante la creación e implementación de perfiles de certificado. Para más información sobre cómo crear perfiles de certificado, consulte [Creación de perfiles de certificado](../../protect/deploy-use/create-certificate-profiles.md).