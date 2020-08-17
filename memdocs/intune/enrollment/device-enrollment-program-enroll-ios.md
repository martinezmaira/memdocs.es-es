---
title: 'Inscripción de dispositivos automatizada: inscripción de dispositivos iOS/iPadOS'
titleSuffix: Microsoft Intune
description: Obtenga información sobre cómo inscribir dispositivos iOS/iPadOS corporativos con la inscripción de dispositivos automatizada.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/10/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7ddbf360-0c61-11e8-ba89-0ed5f89f718b
ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 05a0c4e5a78281f78a986d0512abfeca155494dd
ms.sourcegitcommit: 47ed9af2652495adb539638afe4e0bb0be267b9e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/10/2020
ms.locfileid: "88051679"
---
# <a name="automatically-enroll-iosipados-devices-with-apples-automated-device-enrollment"></a>Inscripción automática de dispositivos iOS/iPadOS con la Inscripción de dispositivos automatizada de Apple

> [!IMPORTANT]
> Apple ha dejado de usar recientemente el Programa de inscripción de dispositivos (DEP) de Apple y ahora emplea la Inscripción de dispositivo automatizada (ADE) de Apple. Intune está en proceso de actualizar su interfaz de usuario para reflejarlo. Hasta que se completen estos cambios, seguirá viendo el *Programa de inscripción de dispositivos* en el portal de Intune. Cada vez que se muestre, usará la Inscripción de dispositivos automatizada.

Puede configurar Intune para inscribir dispositivos iOS/iPadOS adquiridos mediante la [inscripción de dispositivos automatizada (ADE)](https://deploy.apple.com) de Apple. La Inscripción de dispositivos automatizada permite inscribir una gran cantidad de dispositivos sin siquiera tocarlos. Los dispositivos como iPhone, iPad y MacBook se pueden enviar directamente a los usuarios. Cuando el usuario activa el dispositivo, se ejecuta el Asistente para la instalación, que incluye la típica experiencia predeterminada de los productos de Apple, con opciones preconfiguradas, y el dispositivo se inscribe en la administración.

Para habilitar ADE, se pueden usar los portales de Intune, [Apple Business Manager (ABM)](https://business.apple.com/) o [Apple School Manager (ASM)](https://school.apple.com/). Se necesita una lista de números de serie o un número de pedido de compra, de manera que pueda asignar dispositivos a Intune para la administración en cualquiera de los portales de Apple. Puede crear perfiles de inscripción de ADE en Intune que contengan opciones que se apliquen a los dispositivos durante la inscripción. ADE no se puede usar con una cuenta de [administrador de inscripciones de dispositivos](device-enrollment-manager-enroll.md).

> [!NOTE]
> ADE establece configuraciones de dispositivo que el usuario final no puede necesariamente quitar. Por lo tanto, antes de [migrar a ADE](../fundamentals/migration-guide-considerations.md), el dispositivo debe borrarse para devolverlo a su estado predeterminado (nuevo).

## <a name="automated-device-enrollment-and-the-company-portal"></a>Inscripción de dispositivos automatizada y el Portal de empresa

Las inscripciones de ADE no son compatibles con la versión de App Store de la aplicación Portal de empresa. Puede conceder acceso a los usuarios a la aplicación Portal de empresa en un dispositivo ADE. Le recomendamos que proporcione este acceso para que los usuarios puedan elegir qué aplicaciones corporativas quieren usar en el dispositivo o para usar la autenticación moderna para completar el proceso de inscripción. 

Para habilitar la autenticación moderna durante la inscripción, inserte la aplicación en el dispositivo con **Instalar Portal de empresa con VPP** (Programa de compras por volumen) en el perfil de ADE. Para obtener más información, vea [Inscripción automática de dispositivos iOS/iPadOS con ADE de Apple](device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).

Para permitir que el Portal de empresa se actualice automáticamente y proporcione la aplicación Portal de empresa en los dispositivos ya inscritos con ADE, implemente la aplicación Portal de empresa a través de Intune como una aplicación de Programa de compras por volumen (VPP) necesaria con una [directiva de Configuración de aplicación](../apps/app-configuration-policies-use-ios.md) aplicada.

## <a name="what-is-supervised-mode"></a>¿Qué es el modo de supervisión?

Apple introdujo el modo supervisado en iOS/iPadOS 5. Un dispositivo iOS/iPadOS en modo supervisado se puede administrar con más controles, como el de bloquear la captura de pantalla e impedir la instalación de aplicaciones de App Store. Por lo tanto, resulta especialmente útil para los dispositivos corporativos. Intune admite la configuración de dispositivos en el modo de supervisión como parte de ADE.

La compatibilidad con dispositivos ADE no supervisados entró en desuso en iOS/iPadOS 11. En iOS/iPadOS 11 y versiones posteriores, siempre se deben supervisar los dispositivos configurados por ADE. La marca *is_supervised* de ADE se omitirá en iOS/iPadOS 13.0 y versiones posteriores. Todos los dispositivos iOS/iPadOS con la versión 13.0 y posteriores se supervisan de forma automática cuando se inscriben con la inscripción de dispositivos automatizada. 

<!--
**Steps to enable enrollment programs from Apple**
1. [Get an Apple DEP token and assign devices](#get-the-apple-dep-token)
2. [Create an enrollment profile](#create-an-apple-enrollment-profile)
3. [Synchronize DEP-managed devices](#sync-managed-device)
4. [Assign DEP profile to devices](#assign-an-enrollment-profile-to-devices)
5. [Distribute devices to users](#end-user-experience-with-managed-devices)
-->
## <a name="prerequisites"></a>Requisitos previos
- Dispositivos adquiridos en [ADE de Apple](https://deploy.apple.com)
- [Autoridad de Administración de dispositivos móviles (MDM)](../fundamentals/mdm-authority-set.md)
- [Certificado push MDM de Apple](apple-mdm-push-certificate-get.md)

## <a name="supported-volume"></a>Volumen admitido

- Número máximo de perfiles de inscripción por token: 1.000  
- Número máximo de dispositivos de inscripción de dispositivos automatizada por perfil: sin límite (dentro del número máximo de dispositivos por token)
- Número máximo de tokens de inscripción de dispositivos automatizada por cuenta de Intune: 2,000
- Número máximo de dispositivos de inscripción de dispositivos automatizada por token: El límite de la primera sincronización es de 75 000 a 80 000 dispositivos. Intune se seguirá sincronizando con ABN o ASM con cada sincronización de 12 horas para agregar más dispositivos cada vez. Una sincronización manual (que se puede desencadenar una vez cada 15 minutos) también agregará otro lote de dispositivos a Intune. Las sincronizaciones seguirán produciéndose y los dispositivos continuarán sincronizándose desde ABN o ASM con Intune en grandes cantidades. 

## <a name="get-an-apple-automated-device-enrollment-token"></a>Obtención de un token de inscripción de dispositivo automatizada de Apple

Para poder inscribir dispositivos iOS/iPadOS con ADE, necesita un archivo de token de ADE (.p7m) de Apple. Este token permite a Intune sincronizar información sobre dispositivos corporativos de ADE. También permite a Intune cargar perfiles de inscripción en Apple y asignar dispositivos a esos perfiles.

Use el portal de [Apple Business Manager (ABM)](https://business.apple.com/) o [Apple School Manager (ASM)](https://school.apple.com/) para crear un token. También puede usar el portal de ABM/ASM para asignar dispositivos a Intune para su administración.

> [!NOTE]
> Si elimina el token desde el portal clásico de Intune antes de realizar la migración a Azure, Intune podría restaurar un token de ADE de Apple eliminado. Puede volver a eliminar el token de ADE desde Azure Portal.

### <a name="step-1-download-the-intune-public-key-certificate-required-to-create-the-token"></a>Paso 1. Descargue el certificado de clave pública de Intune necesario para crear el token.

1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), elija **Dispositivos** > **iOS/iPadOS** > **Inscripción de iOS/iPadOS**.

    ![Obtenga un token del programa de inscripción.](./media/device-enrollment-program-enroll-ios/ios-enroll.png)

2. Seleccione **Tokens del programa de inscripción** > **Agregar**.

3. Conceda a Microsoft permiso para enviar información de usuario y dispositivo a Apple al seleccionar **Acepto**.

   > [!NOTE]
   > Una vez que haya superado el paso 2 para descargar el certificado de clave pública de Intune, no cierre el asistente ni salga de esta página. Si lo hace, el certificado que ha descargado se invalidará y tendrá que repetir este proceso. Si se produce esta situación, normalmente observará que el botón **Crear** de la pestaña **Revisar y crear** está atenuado y no se puede completar el proceso.

   ![Captura de pantalla del panel Token del Programa de inscripción en el área de trabajo de Certificados de Apple para descargar la clave pública.](./media/device-enrollment-program-enroll-ios/add-enrollment-program-token-pane.png)

4. Seleccione **Descargar la clave pública** para descargar y guardar localmente el archivo de la clave de cifrado (.pem). El archivo .pem se usa para solicitar un certificado de relación de confianza en el portal de Apple.


### <a name="step-2-use-your-key-to-download-a-token-from-apple"></a>Paso 2. Use la clave para descargar un token de Apple.

1. Elija **Create a token via Apple Business Manager** (Crear un token mediante Apple Business Manager) para abrir el portal Business de Apple e iniciar sesión con el identificador de Apple de la empresa. Puede usar este id. de Apple para renovar el token de ADE.
2. En el [portal Business](https://business.apple.com) de Apple, elija **Introducción** para **Programa de inscripción de dispositivos**.

3. En la página **Administrar servidores**, pulse **Add MDM Server** (Agregar servidor de MDM).
4. Escriba el **nombre del servidor MDM** y, después, elija **Siguiente**. El nombre del servidor es su referencia para identificar el servidor de administración de dispositivos móviles (MDM). No es el nombre ni la dirección URL del servidor de Microsoft Intune.

5. Se abre el cuadro de diálogo **Agregar&lt;Nombre del servidor&gt;** , indicando **Cargar la clave pública**. Seleccione **Elegir archivo…** para cargar el archivo .pem y, después, elija **Siguiente**.

6. Vaya a **Programas de implementación** &gt; **Programa de inscripción de dispositivos** &gt; **Administrar dispositivos**.
7. En **Elegir dispositivos por**, especifique cómo se identifican los dispositivos:
    - **Número de serie**
    - **Número de pedido**
    - **Cargar archivo CSV**.

   ![Captura de pantalla sobre cómo especificar Elegir dispositivos por número de serie, estableciendo Elegir acción como Asignar al servidor y seleccionando el nombre de servidor.](./media/device-enrollment-program-enroll-ios/enrollment-program-token-specify-serial.png)

8. En **Elegir acción**, pulse **Asignar al servidor**, seleccione el &lt;NombreDeServidor&gt; especificado para Microsoft Intune y pulse **Aceptar**. El portal de Apple asigna los dispositivos especificados al servidor de Intune para la administración y, después, muestra **Asignación completa**.

   En el portal de Apple, vaya a **Programas de implementación** &gt; **Programa de inscripción de dispositivos** &gt; **View Assignment History (Ver historial de asignaciones)** para ver una lista de dispositivos y su asignación de servidor MDM.

### <a name="step-3-save-the-apple-id-used-to-create-this-token"></a>Paso 3. Guarde el identificador de Apple usado para crear este token.

En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), proporcione el identificador de Apple como referencia futura.

![Captura de pantalla sobre cómo especificar el identificador de Apple que se ha usado para crear y buscar el token del Programa de inscripción.](./media/device-enrollment-program-enroll-ios/image03.png)

### <a name="step-4-upload-your-token-and-choose-scope-tags"></a>Paso 4. Cargue el token y elija etiquetas de ámbito.

1. En el cuadro **Token de Apple**, vaya al archivo de certificado (.p7m) y elija **Abrir**.
2. Si quiere aplicar [etiquetas de ámbito](../fundamentals/scope-tags.md) en este token de DEP, elija **Ámbito (etiquetas)** y seleccione las etiquetas de ámbito que quiera. Los perfiles y dispositivos agregados a este token heredarán las etiquetas de ámbito aplicadas a un token.
3. Elija **Crear**.

Con el certificado push, Intune puede inscribir y administrar dispositivos iOS/iPadOS insertando la directiva en los dispositivos móviles inscritos. Intune se sincroniza automáticamente con Apple para ver la cuenta del programa de inscripción.

## <a name="create-an-apple-enrollment-profile"></a>Creación de un perfil de inscripción de Apple

Ahora que ha instalado el token, puede crear un perfil de inscripción para dispositivos ADE. Un perfil de inscripción de dispositivos define la configuración que se aplica a un grupo de dispositivos durante la inscripción. Hay un límite de 100 perfiles de inscripción por token de ADE.

> [!NOTE]
> Los dispositivos se bloquean si no hay suficientes licencias de Portal de empresa para un token VPP o si el token ha expirado. Intune muestra una alerta cuando un token está a punto de expirar o las licencias están a punto de terminar.
 

1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), elija **Dispositivos** > **iOS/iPadOS** > **Inscripción de iOS/iPadOS** > **Tokens del programa de inscripción**.
2. Seleccione un token, elija **Perfiles** > **Crear perfil** > **iOS/iPadOS**.

    ![Cree una captura de pantalla del perfil.](./media/device-enrollment-program-enroll-ios/image04.png)

3. En la página **Básico**, escriba la información pertinente en **Nombre** y **Descripción** para el perfil con fines administrativos. Los usuarios no ven estos detalles. 

    ![Nombre y descripción del perfil.](./media/device-enrollment-program-enroll-ios/image05.png)

4. Seleccione **Siguiente: Configuración de administración de dispositivos**.

5. En **Afinidad de usuario**, elija si los dispositivos con este perfil deben inscribirse con o sin un usuario asignado.
    - **Inscribir con afinidad de usuario**: seleccione esta opción para dispositivos que pertenezcan a usuarios y necesiten usar el Portal de empresa para hacer uso de servicios, como instalar aplicaciones. Si usa ADFS y el Asistente de configuración para realizar la autenticación, se requiere [Punto de conexión mixto/nombre de usuario de WS-Trust 1.3](https://technet.microsoft.com/library/adfs2-help-endpoints) [Más información](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint).

    - **Inscribir sin afinidad de usuario**: seleccione esta opción para dispositivos no afiliados con un usuario único. Use esta opción para los dispositivos que no tengan acceso a los datos de usuario local. Para permitir que un usuario final inicie sesión en el Portal de empresa de iOS y se establezca como el usuario principal del dispositivo, envíe la clave de `IntuneUDAUserlessDevice` al Portal de empresa de iOS en una directiva de configuración de aplicaciones para dispositivos administrados. Tenga en cuenta que solo el primer usuario que inicia sesión se establece como el usuario principal. Si el primer usuario cierra sesión y un segundo usuario inicia sesión, aquel sigue siendo el usuario principal del dispositivo. Para más información, consulte [Configuración de la aplicación Portal de empresa para que admita dispositivos iOS e iPadOS de DEP](../apps/app-configuration-policies-use-ios.md#configure-the-company-portal-app-to-support-ios-and-ipados-dep-devices). 

6. Si elige **Inscribir con afinidad de usuario**, puede permitir que los usuarios se autentiquen en el Portal de empresa en lugar de con el Asistente de configuración de Apple.

    ![Autenticación con el portal de empresa.](./media/device-enrollment-program-enroll-ios/authenticatewithcompanyportal.png)

    > [!NOTE]
    > Si desea realizar una de las siguientes acciones, establezca **Seleccionar dónde deben autenticarse los usuarios**  autenticarse en **Portal de empresa**.
    >    - usar la autenticación multifactor
    >    - pedir a los usuarios que cambien su contraseña cuando inician sesión por primera vez
    >    - pedir a los usuarios que restablezcan las contraseñas expiradas durante la inscripción
    >
    > Estas operaciones no se admiten durante la autenticación con el asistente para configuración de Apple.

7. Si elige **Portal de empresa** para **Seleccionar dónde deben autenticarse los usuarios**, puede usar un token de VPP para instalar automáticamente el Portal de empresa en el dispositivo. En este caso, el usuario no tiene que proporcionar un id. de Apple. Para instalar Portal de empresa con un token de VPP, elija un token en **Instalar Portal de empresa con VPP**. Requiere que el Portal de empresa ya se haya agregado al token de VPP. Para asegurarse de que la aplicación Portal de empresa se sigue actualizando después de la inscripción, asegúrese de que ha configurado una implementación de aplicaciones en Intune (Intune>Aplicaciones cliente). Para que no sea necesaria la interacción del usuario, lo más probable es que quiera tener el Portal de empresa como aplicación VPP para iOS/iPadOS, convertirla en una aplicación requerida y usar licencias de dispositivo para la asignación. Asegúrese de que el token no expire y de que disponga de suficientes licencias de dispositivos para la aplicación Portal de empresa. Si el token expira o se agotan las licencias, Intune instala Portal de empresa de App Store y solicita un id. de Apple. 

    > [!NOTE]
    > Cuando **Seleccionar dónde deben autenticarse los usuarios**  se establezca en **Portal de empresa**, asegúrese de que el proceso de inscripción de los dispositivos se realiza en las primeras 24 horas en las que el Portal de empresa se ha descargado en el dispositivo ADE. De lo contrario, podría producirse un error en la inscripción y se necesitará un restablecimiento de fábrica para inscribir el dispositivo.
    
    ![Captura de pantalla de la instalación de Portal de empresa con VPP.](./media/device-enrollment-program-enroll-ios/install-cp-with-vpp.png)

8. Si seleccionó **Asistente de configuración** para **Seleccionar dónde deben autenticarse los usuarios** , pero también quiere usar el acceso condicional o implementar aplicaciones de empresa en los dispositivos, debe instalar Portal de empresa en el dispositivos. Para ello, elija **Sí** para **Instalar Portal de empresa**.  Si desea que los usuarios reciban el Portal de empresa sin tener que autenticarse en la tienda de aplicaciones, elija **Instalar Portal de empresa con VPP**  y seleccione un token de VPP. Asegúrese de que el token no expire y de que disponga de suficientes licencias de dispositivos para que la aplicación Portal de empresa se implemente correctamente.

9. Si ha elegido un token para **Instalar Portal de empresa con VPP**, puede bloquear el dispositivo en modo Una aplicación (en concreto, la aplicación Portal de empresa) inmediatamente después de que finalice el Asistente de configuración. Haga clic en **Sí** en **Run Company Portal in Single App Mode until authentication** (Ejecutar el Portal de empresa en el modo de aplicación única hasta la autenticación) para establecer esta opción. Para usar el dispositivo, primero el usuario debe autenticarse iniciando sesión con el Portal de empresa.

    No se admite la autenticación multifactor en un único dispositivo bloqueado en modo Una aplicación. Esta limitación existe porque el dispositivo no puede cambiar a otra aplicación para completar el segundo factor de autenticación. Por lo tanto, si desea autenticación multifactor en un dispositivo de modo Una aplicación, el segundo factor debe estar en un dispositivo diferente.

    Esta característica solo es compatible con iOS/iPadOS 11.3.1 y versiones posteriores.

   ![Captura de pantalla del modo de aplicación única.](./media/device-enrollment-program-enroll-ios/single-app-mode.png)

10. Si desea que los dispositivos que usan este perfil se supervisen, elija **Sí** para **Supervisado**.

    ![Captura de pantalla de Configuración de administración de dispositivos.](./media/device-enrollment-program-enroll-ios/supervisedmode.png)

    Los dispositivos **supervisados** ofrecen más opciones de administración y, en este caso, el bloqueo de activación está deshabilitado de forma predeterminada. Microsoft recomienda usar ADE como mecanismo para habilitar el modo de supervisión, sobre todo si se implementa un gran número de dispositivos iOS/iPadOS. Los dispositivos iPad empresariales compartidos de Apple deben supervisarse.

    Los usuarios reciben notificaciones de que sus dispositivos están supervisados de dos maneras:

   - En la pantalla de bloqueo aparece: "This iPhone is managed by Contoso" (Contoso administra este iPhone).
   - En la pantalla **Configuración** > **General** > **Acerca de** aparece: "This iPhone is supervised. Contoso can monitor your Internet traffic and locate this device" (Este iPhone está supervisado. Contoso puede supervisar el tráfico de Internet y localizar este dispositivo)

     > [!NOTE]
     > Un dispositivo inscrito sin supervisión solo puede restablecerse a supervisado con Apple Configurator. Para restablecer el dispositivo de esta forma, es necesario conectar un dispositivo iOS/iPadOS a un Mac con un cable USB. Obtenga más información en los documentos de [Apple Configurator](http://help.apple.com/configurator/mac/2.3).

11. Elija si desea que la inscripción de dispositivos esté bloqueada con este perfil. **Inscripción bloqueada** deshabilita la configuración de iOS/iPadOS que permite que el perfil de administración se quite del menú **Configuración**. Tras la inscripción del dispositivo, no se puede cambiar esta configuración sin borrar dicho dispositivo. Estos dispositivos deben tener el modo de administración **supervisado** definido en *Sí*. 

    > [!NOTE]
    > Cuando el dispositivo se inscriba con **Inscripción bloqueada**, los usuarios no podrán usar **Quitar de dispositivo** o **Restablecimiento de fábrica** en la aplicación Portal de empresa. Las opciones no estarán disponibles para el usuario. El usuario tampoco podrá quitar el dispositivo del sitio web del Portal de empresa (https://portal.manage.microsoft.com).
    > Además, si un dispositivo BYOD se convierte en un dispositivo de inscripción de dispositivos automatizada de Apple y se inscribe con un perfil habilitado para **Inscripción bloqueada**, el usuario podrá usar **Quitar dispositivo** y **Restablecimiento de fábrica** durante 30 días y, luego, las opciones se deshabilitarán o no estarán disponibles. Referencia: https://help.apple.com/configurator/mac/2.8/#/cad99bc2a859.

12. Si seleccionó **Inscribir sin afinidad de usuario** y **Supervisado**, debe decidir si quiere configurar los dispositivos para que sean [dispositivos iPad empresariales compartidos de Apple](https://support.apple.com/guide/mdm/shared-ipad-overview-cad7e2e0cf56/web). Si elige **Sí** para **iPad compartido**, varios usuarios podrán iniciar sesión en el mismo dispositivo. Los usuarios se autenticarán con sus cuentas de autenticación federadas y el identificador de Apple administrado, o bien a través de una sesión temporal (es decir, una cuenta de invitado). Esta opción requiere iOS/iPadOS 13.4 o una versión posterior.

    Si decide configurar los dispositivos para que sean dispositivos iPad empresariales compartidos de Apple, debe establecer **Número máximo de usuarios en caché**. Establezca este valor en el número de usuarios que espera que usen el iPad compartido. Puede almacenar en caché hasta 24 usuarios en un dispositivo de 32 o 64 GB. Si elige un número muy bajo, es posible que los datos del usuario tarden un tiempo en llegar al dispositivo después del inicio de sesión. Si elige un número muy alto, es posible que los usuarios no tengan suficiente espacio en disco.  

    > [!NOTE]
    > Para configurar el iPad empresarial compartido de Apple, establezca los siguientes valores: 
    > - **Afinidad de usuario** = **Inscribir sin afinidad de usuario**. 
    > - **Supervisado** = **Sí**. 
    > - **iPad compartido** = **Sí**.
    > Las sesiones temporales están habilitadas de forma predeterminada y permiten a los usuarios iniciar sesión en un iPad compartido sin una cuenta con identificador de Apple administrado. Para deshabilitar las sesiones temporales en el iPad compartido, configure las [opciones de restricción de dispositivos](../configuration/device-restrictions-ios.md) del iPad compartido iOS/iPadOS.  

13. Elija si desea que los dispositivos que usan este perfil se puedan **sincronizar con equipos**. Si elige **Permitir Apple Configurator mediante certificado**, debe seleccionar un certificado en **Certificado de Apple Configurator**.

     > [!NOTE]
     > Si **Sincronizar con equipos** está establecido en **Denegar todo**, el puerto estará limitado en dispositivos iOS y iPadOS. El puerto solo se puede usar para la carga y nada más. No se permitirá que el puerto use iTunes o Apple Configurator 2.
     Si **Sincronizar con equipos** se establece en **Permitir Apple Configurator mediante certificado**, asegúrese de tener una copia local del certificado a la que pueda acceder más adelante. No es posible realizar cambios en la copia cargada y es importante conservar este certificado para que sea accesible en el futuro. Para conectarse al dispositivo iOS/iPadOS desde un equipo o dispositivo macOS, se debe instalar el mismo certificado en el dispositivo que establece la conexión con el dispositivo iOS/iPadOS inscrito con el perfil de Inscripción de dispositivos automatizada con esta configuración y este certificado.

14. Si selecciona **Permitir Apple Configurator mediante certificado** en el paso anterior, elija un certificado de Apple Configurator para importarlo.

15. Puede especificar un formato de nombres para los dispositivos que se aplique automáticamente cuando se inscriban y en cada protección sucesiva. Para crear una plantilla de nombres, seleccione **Sí** en **Aplicar plantilla de nombre de dispositivo**. A continuación, en el cuadro **Device Name Template** (Plantilla de nombre de dispositivo), escriba la plantilla que se usará para los nombres que usan este perfil. Puede especificar un formato de plantilla que incluya el tipo de dispositivo y el número de serie. 

16. Seleccione **Siguiente: Personalización del Asistente de configuración**.

17. En la página **Personalización del Asistente de configuración**, configure la siguiente configuración de perfil: ![Personalización del Asistente de configuración.](./media/device-enrollment-program-enroll-ios/setupassistantcustom.png)


    | Configuración de departamento | Descripción |
    |---|---|
    | <strong>Nombre de departamento</strong> | Aparece cuando los usuarios pulsan <strong>Acerca de la configuración</strong> durante la activación. |
    |    <strong>Teléfono del departamento</strong>     | Aparece cuando el usuario hace clic en el botón <strong>Necesito ayuda</strong> durante la activación. |

    Puede ocultar las pantallas del Asistente de configuración en el dispositivo durante la configuración del usuario.
    - Si elige **Ocultar**, la pantalla no se mostrará durante la configuración. Después de configurar el dispositivo, el usuario seguirá teniendo la posibilidad de ir al menú **Ajustes** para configurar la característica.
    - Si elige **Mostrar**, la pantalla se mostrará durante la configuración. A veces, el usuario puede omitir la pantalla sin realizar ninguna acción. Sin embargo, posteriormente podrá ir al menú **Ajustes** del dispositivo para configurar la característica. 


    | Configuración de pantallas del asistente | Si elige **Mostrar**, durante la configuración se producirá lo siguiente en el dispositivo: |
    |------------------------------------------|------------------------------------------|
    | <strong>Código de acceso</strong> | Se solicitará un código de acceso al usuario. Solicite siempre un código de acceso para dispositivos no protegidos a menos que el acceso esté controlado de otra manera (como el modo de quiosco que restringe el dispositivo a una aplicación). En iOS/iPadOS 7.0 y versiones posteriores. |
    | <strong>Servicios de ubicación</strong> | Se solicitará la ubicación del usuario. En macOS 10.11 y versiones posteriores y iOS/iPadOS 7.0 y versiones posteriores. |
    | <strong>Restaurar</strong> | Se mostrará la pantalla Aplicaciones y datos. En esta pantalla el usuario tendrá la opción de restaurar o transferir datos de una copia de seguridad de iCloud al configurar el dispositivo. En macOS 10.9 y versiones posteriores e iOS/iPadOS 7.0 y versiones posteriores. |
    | <strong>iCloud e identificador de Apple</strong> | El usuario tendrá la opción de iniciar sesión con su id. de Apple y usar iCloud. En macOS 10.9 y versiones posteriores e iOS/iPadOS 7.0 y versiones posteriores.   |
    | <strong>Términos y condiciones</strong> | El usuario deberá aceptar los términos y condiciones de Apple. En macOS 10.9 y versiones posteriores e iOS/iPadOS 7.0 y versiones posteriores. |
    | <strong>Touch ID</strong> | El usuario tendrá la opción de configurar una identificación con huella digital para el dispositivo. En macOS 10.12.4 y versiones posteriores e iOS/iPadOS 8.1 y versiones posteriores. |
    | <strong>Apple Pay</strong> | El usuario tendrá la opción de configurar Apple Pay en el dispositivo. En macOS 10.12.4 y versiones posteriores e iOS/iPadOS 7.0 y versiones posteriores. |
    | <strong>Zoom</strong> | El usuario tendrá la opción de ampliar el contenido de la pantalla al configurar el dispositivo. En iOS/iPadOS 8.3 y versiones posteriores. |
    | <strong>Siri</strong> | El usuario tendrá la opción de configurar Siri. En macOS 10.12 y versiones posteriores e iOS/iPadOS 7.0 y versiones posteriores. |
    | <strong>Datos de diagnóstico</strong> | Se mostrará la pantalla Diagnóstico al usuario. En esta pantalla el usuario podrá enviar datos de diagnóstico a Apple. En macOS 10.9 y versiones posteriores e iOS/iPadOS 7.0 y versiones posteriores. |
    | <strong>Tono de visualización</strong> | El usuario tendrá la opción de configurar el tono de visualización. En macOS 10.13.6 y versiones posteriores e iOS/iPadOS 9.3.2 y versiones posteriores. |
    | <strong>Privacidad</strong> | Se mostrará la pantalla Privacidad al usuario. En macOS 10.13.4 y versiones posteriores e iOS/iPadOS 11.3 y versiones posteriores. |
    | <strong>Migración de Android</strong> | El usuario tendrá la opción de migrar datos de un dispositivo Android. En iOS/iPadOS 9.0 y versiones posteriores.|
    | <strong>iMessage y FaceTime</strong> | El usuario tendrá la opción de configurar iMessage y FaceTime. En iOS/iPadOS 9.0 y versiones posteriores. |
    | <strong>Incorporación</strong> | Se mostrarán las pantallas de información de incorporación, como la portada, la multitarea y el centro de control, para informar al usuario. En iOS/iPadOS 11.0 y versiones posteriores. |
    | <strong>Migración de Watch</strong> | El usuario tendrá la opción de migrar los datos de un dispositivo Watch. En iOS/iPadOS 11.0 y versiones posteriores.|
    | <strong>Tiempo de pantalla</strong> | Se mostrará la pantalla Tiempo de pantalla. En macOS 10.15 y versiones posteriores e iOS/iPadOS 12.0 y versiones posteriores. |
    | <strong>Actualización de software</strong> | Se mostrará la pantalla de actualización de software obligatoria. En iOS/iPadOS 12.0 y versiones posteriores. |
    | <strong>Configuración de SIM</strong> | El usuario tendrá la opción de agregar un plan de datos móviles. En iOS/iPadOS 12.0 y versiones posteriores. |
    | <strong>Aspecto</strong> | Se mostrará la pantalla Aspecto al usuario. En macOS 10.14 y versiones posteriores e iOS/iPadOS 13.0 y versiones posteriores. |
    | <strong>Express Language</strong> (Idioma rápido)| Se mostrará la pantalla Express Language (Idioma rápido) al usuario. |
    | <strong>Idioma preferido</strong> | El usuario tendrá la opción de elegir su **Idioma preferido**. |
    | <strong>Device to Device Migration</strong> (Migración entre dispositivos) | El usuario tendrá la opción de migrar los datos de un dispositivo antiguo a este dispositivo. En iOS/iPadOS 13.0 y versiones posteriores. |
    | <strong>Registro</strong> | Se muestra la pantalla de registro al usuario. En macOS 10.9 y versiones posteriores. |
    | <strong>FileVault</strong> | Se muestra la pantalla de cifrado de FileVault 2 al usuario. En macOS 10.10 y versiones posteriores. |
    | <strong>Diagnósticos de iCloud</strong> | Se muestra la pantalla de análisis de iCloud al usuario. En macOS 10.12.4 y versiones posteriores. |
    | <strong>Almacenamiento en iCloud</strong> | Se muestra la pantalla de documentos y escritorio de iCloud al usuario. En macOS 10.13.4 y versiones posteriores. |
    

18. Elija **Siguiente** para ir a la página **Revisar y crear**.

19. Para guardar el perfil, elija **Crear**.

### <a name="dynamic-groups-in-azure-active-directory"></a>Grupos dinámicos en Azure Active Directory

Puede usar el campo de **nombre** de la inscripción para crear un grupo dinámico en Azure Active Directory. Para obtener más información, consulte [Grupos dinámicos de Azure Active Directory](/azure/active-directory/users-groups-roles/groups-dynamic-membership).

Puede usar el nombre de perfil para definir el [parámetro enrollmentProfileName](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices) para asignar dispositivos con este perfil de inscripción.

Para obtener la entrega de directivas más rápida en dispositivos ADE con afinidad de usuario, asegúrese de que el usuario de la inscripción es miembro, antes de la configuración del dispositivo, de un grupo de usuarios de AAD. 

La asignación de grupos dinámicos a perfiles de inscripción puede provocar un retraso en la entrega de aplicaciones y directivas a los dispositivos después de la inscripción.


## <a name="sync-managed-devices"></a>Sincronizar dispositivos administrados
Ahora que Intune tiene permiso para administrar los dispositivos, puede sincronizar Intune con Apple para ver los dispositivos administrados en Intune en Azure Portal.

1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), elija **Dispositivos** > **iOS/iPadOS** > **Inscripción de iOS/iPadOS** > **Tokens del programa de inscripción**.

2. Elija un token de la lista > **Dispositivos** > **Sincronizar**. ![Captura de pantalla del nodo Dispositivos del Programa de inscripción seleccionado y el vínculo Sincronizar.](./media/device-enrollment-program-enroll-ios/image06.png)

   Para cumplir con los términos de Apple relativos a un tráfico del programa de inscripción aceptable, Intune impone las restricciones siguientes:
   - Una sincronización completa no se puede ejecutar más de una vez cada siete días. Durante una sincronización completa, Intune captura la lista actualizada completa de números de serie asignados al servidor MDM de Apple conectado a Intune. Si se elimina un dispositivo ADE del portal de Intune, se debe cancelar la asignación del servidor MDM de Apple en el portal de ADE. Si la asignación no se ha cancelado, no se volverá a importar a Intune hasta que se ejecute la sincronización completa.   
   - Se ejecuta una sincronización automáticamente cada 12 horas. También puede sincronizar haciendo clic en el botón **Sincronizar** (no más de una vez cada 15 minutos). Todas las solicitudes de sincronización tardan 15 minutos en finalizar. El botón **Sincronizar** queda deshabilitado hasta que se completa la sincronización. Esta sincronización actualizará el estado del dispositivo existente e importará nuevos dispositivos asignados al servidor MDM de Apple.   


## <a name="assign-an-enrollment-profile-to-devices"></a>Asignar un perfil de inscripción a los dispositivos
Debe asignar un perfil del Programa de inscripción a los dispositivos para poder inscribirlos.

>[!NOTE]
>También puede asignar números de serie a perfiles en la hoja **Números de serie de Apple**.

1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), elija **Dispositivos** > **iOS/iPadOS** > **Inscripción de iOS/iPadOS** > **Tokens del programa de inscripción** > elija un token de la lista.
2. Elija **Dispositivos** > Elija los dispositivos de la lista > **Asignar perfil**.
3. En **Asignar perfil**, elija un perfil para los dispositivos y seleccione **Asignar**.

### <a name="assign-a-default-profile"></a>Asignación de un perfil predeterminado

Puede elegir un perfil predeterminado para aplicarlo a todos los dispositivos que se inscriben en un token específico.

1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), elija **Dispositivos** > **iOS/iPadOS** > **Inscripción de iOS/iPadOS** > **Tokens del programa de inscripción** > elija un token de la lista.
2. Elija **Establecer perfil predeterminado**, seleccione un perfil en la lista desplegable y después seleccione **Guardar**. Este perfil se aplicará a todos los dispositivos que se inscriben en el token.

## <a name="distribute-devices"></a>Distribución de los dispositivos
Ha habilitado la administración y sincronización entre Apple e Intune, y ha asignado un perfil para permitir que sus dispositivos ADE se inscriban. Ahora puede distribuir los dispositivos a los usuarios. Los dispositivos con afinidad de usuario necesitan que a cada usuario se le asigne una licencia de Intune. Los dispositivos sin afinidad de usuario necesitan una licencia de dispositivo. Un dispositivo activado no puede aplicar un perfil de inscripción hasta que se haya borrado.

Vea [Inscribir el dispositivo iOS/iPadOS en Intune con el Programa de inscripción de dispositivos](../user-help/enroll-your-device-dep-ios.md).

## <a name="renew-an-automated-device-enrollment-token"></a>Renovación de un token de inscripción de dispositivo automatizada  

> [!NOTE]
> Además de renovar anualmente el token de ADE, deberá renovar el token del programa de inscripción en Intune y Apple Business Manager cuando cambien la contraseña y el identificador de Apple administrados para el usuario que ha configurado el token en Apple Business Manager o si el usuario abandona la organización de Apple Business Manager.

1. Vaya a business.apple.com.
2. Haga clic en **Configuración** (esquina inferior izquierda)
3. En  **Servidores MDM**, elija el servidor MDM asociado con el archivo de token de ADE/DEP que quiera renovar.
4. Haga clic en **Descargar token**.

    ![Captura de pantalla de Generar nuevo token.](./media/device-enrollment-program-enroll-ios/generatenewtoken.png)

5. En el símbolo del sistema, seleccione "Descargar token de servidor"
> [!NOTE]
> No haga clic en **"Descargar token de servidor"** si no tiene previsto renovar el token, como se ha mencionado en el mensaje; si lo hace, se invalidará el token que Intune usa actualmente (o, en su defecto, cualquier otra solución de MDM). Si ya ha descargado el token, asegúrese de continuar con los pasos siguientes hasta que se renueve.

6. Después de descargar el token, en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), elija **Dispositivos** > **iOS/iPadOS** > **Inscripción de iOS/iPadOS** > **Tokens del programa de inscripción** > elija el token.
    ![Captura de pantalla de Tokens del programa de inscripción.](./media/device-enrollment-program-enroll-ios/enrollmentprogramtokens.png)

7. Elija **Renovar token** y escriba el identificador de Apple que ha usado para crear el token original (si no se ha rellenado de forma automática).  
    ![Captura de pantalla de Generar nuevo token.](./media/device-enrollment-program-enroll-ios/renewtoken.png)

8. Cargue el token recién descargado.

9. Seleccione **Siguiente** para ir a la página **Etiquetas de ámbito** y, si quiere, asigne etiquetas.

10. Elija **Renovar token**. Verá la confirmación de que el token se renovó.   
    ![Captura de pantalla de confirmación.](./media/device-enrollment-program-enroll-ios/confirmation.png)

## <a name="delete-an-automated-device-enrollment-token-from-intune"></a>Eliminación de un token de inscripción de dispositivo automatizada de Intune

Puede eliminar tokens de perfil de inscripción de Intune siempre y cuando:
- No haya dispositivos asignados al token
- No haya dispositivos asignados al perfil predeterminado

1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), elija **Dispositivos** > **iOS/macOS** > **Inscripción de iOS/macOS** > **Tokens del programa de inscripción** > elegir el token > **Dispositivos**.
2. Elimine todos los dispositivos asignados al token.
3. Vaya a **Dispositivos** > **iOS/macOS** > **Inscripción de iOS/macOS** > **Tokens del programa de inscripción** > elegir el token > **Perfiles**.
4. Si hay un perfil predeterminado, elimínelo.
5. Vaya a **Dispositivos** > **iOS/macOS** > **Inscripción de iOS/macOS** > **Tokens del programa de inscripción** > elegir el token > **Eliminar**.
