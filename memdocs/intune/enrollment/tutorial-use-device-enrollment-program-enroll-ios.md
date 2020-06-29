---
title: 'Tutorial: Uso de Apple Business Manager o del Programa de inscripción de dispositivos para inscribir dispositivos iOS/iPadOS en Intune'
titleSuffix: Microsoft Intune
description: En este tutorial, configurará las características de inscripción de dispositivos corporativos de Apple desde ABM para inscribir dispositivos iOS/iPadOS en Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/30/2019
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
Customer intent: As an Intune admin, I want to set up the Apple's corporate device enrollment features so that corporate devices can automatically enroll in Intune.
ms.collection: M365-identity-device-management
ms.openlocfilehash: 47f249d105fbc2481dd1d66956032c91d5006834
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093513"
---
# <a name="tutorial-use-apples-corporate-device-enrollment-features-in-apple-business-manager-abm-to-enroll-iosipados-devices-in-intune"></a>Tutorial: Uso de las características de inscripción de dispositivos corporativos de Apple en Apple Business Manager (ABM) para inscribir dispositivos iOS/iPadOS en Intune
Las características de inscripción de dispositivos de Apple Business Manager simplifican la inscripción de dispositivos. Intune también admite el antiguo portal Programa de inscripción de dispositivos (DEP) de Apple, pero se recomienda empezar desde cero con Apple Business Manager. Con Microsoft Intune y la inscripción de dispositivos corporativos de Apple, los dispositivos se inscriben de forma automática y segura la primera vez que el usuario activa el dispositivo. Por tanto, puede proporcionar dispositivos a muchos usuarios sin tener que configurar cada uno de forma individual. 

En este tutorial, aprenderá a:
> [!div class="checklist"]
> * Obtener un token de inscripción de dispositivos de Apple
> * Sincronizar dispositivos administrados en Intune
> * Crear un perfil de inscripción
> * Asignar el perfil de inscripción a los dispositivos

Si no dispone de ninguna suscripción a Intune, [regístrese para obtener una cuenta de evaluación gratuita](../fundamentals/free-trial-sign-up.md).

## <a name="prerequisites"></a>Requisitos previos
- Dispositivos comprados en [Apple Business Manager](https://business.apple.com) o el [Programa de inscripción de dispositivos de Apple](http://deploy.apple.com)
- Establecer la [entidad de administración de dispositivos móviles](../fundamentals/mdm-authority-set.md)
- Obtener un [certificado push MDM de Apple](apple-mdm-push-certificate-get.md)

## <a name="get-an-apple-device-enrollment-token"></a>Obtener un token de inscripción de dispositivos de Apple
Antes de inscribir dispositivos iOS/iPadOS con las características de inscripción corporativas de Apple, necesita un archivo de token de inscripción de dispositivos de Apple (.pem). Este token permite a Intune sincronizar información sobre los dispositivos Apple de propiedad corporativa. También permite a Intune cargar perfiles de inscripción en Apple y asignar dispositivos a esos perfiles.

Para crear un token de inscripción de dispositivos se usa Azure Portal. Los portales también se usan para asignar dispositivos a Intune para la administración.

1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), elija **Dispositivos** > **iOS/iPadOS** > **Inscripción de iOS/iPadOS** > **Tokens del programa de inscripción** > **Agregar**.

2. Conceda a Microsoft permiso para enviar información de usuario y dispositivo a Apple al seleccionar **Acepto**.

   ![Captura de pantalla del panel Token del Programa de inscripción en el área de trabajo de Certificados de Apple para descargar la clave pública.](./media/tutorial-use-device-enrollment-program-enroll-ios/add-enrollment-program-token-pane.png)

3. Seleccione **Descargar la clave pública** para descargar y guardar localmente el archivo de la clave de cifrado (.pem). El archivo .pem se usa para solicitar un certificado de relación de confianza en el portal de Apple.

4. Seleccione **Crear un token mediante el Programa de inscripción de dispositivos de Apple** para abrir el portal de Programas de implementación de Apple e iniciar sesión con su id. de Apple de la empresa. Puede usar este id. de Apple para renovar el token.

5. En el [portal Programas de implementación](https://deploy.apple.com) de Apple, seleccione **Introducción** para **Programa de inscripción de dispositivos**. En [Apple Business Manager](https://business.apple.com) el proceso puede ser ligeramente distinto a los pasos siguientes.

4. En la página **Administrar servidores**, pulse **Add MDM Server** (Agregar servidor de MDM).

5. En **Nombre del servidor de MDM**, escriba *TestMDMServer* y, después, haga clic en **Siguiente**. El nombre del servidor es su referencia para identificar el servidor de administración de dispositivos móviles (MDM). No es el nombre ni la dirección URL del servidor de Microsoft Intune.

6. Se abre el cuadro de diálogo **Agregar&lt;Nombre del servidor&gt;** , indicando **Cargar la clave pública**. Seleccione **Elegir archivo…** para cargar el archivo .pem y, después, elija **Siguiente**.

6. Vaya a **Programas de implementación** > **Programa de inscripción de dispositivos** > **Administrar dispositivos**.
7. En **Elegir dispositivos por**, seleccione **Número de serie**. <!--ask Tiffany about this-->

8. En **Elegir acción**, pulse **Asignar al servidor**, seleccione el &lt;NombreDeServidor&gt; especificado para Microsoft Intune y pulse **Aceptar**. El portal de Apple asigna los dispositivos especificados al servidor de Intune para la administración y, después, muestra **Asignación completa**.

   En el portal de Apple, vaya a **Programas de implementación** &gt; **Programa de inscripción de dispositivos** &gt; **View Assignment History (Ver historial de asignaciones)** para ver una lista de dispositivos y su asignación de servidor MDM.

9. Para futuras referencias, en Intune en Azure Portal, proporcione el id. de Apple que ha usado para crear este token.

    ![Captura de pantalla sobre cómo especificar el identificador de Apple que se ha usado para crear y buscar el token del Programa de inscripción.](./media/tutorial-use-device-enrollment-program-enroll-ios/image03.png)

10. En el cuadro **Token de Apple**, vaya al archivo de certificado (.pem), seleccione **Abrir** y después **Crear**. 

11. Si quiere aplicar etiquetas de ámbito para limitar los administradores que tienen acceso a este token, seleccione los ámbitos.

## <a name="create-an-apple-enrollment-profile"></a>Creación de un perfil de inscripción de Apple
Ahora que ha instalado el token, puede crear un perfil de inscripción para los dispositivos iOS/iPadOS de propiedad corporativa. Un perfil de inscripción de dispositivos define la configuración que se aplica a un grupo de dispositivos durante la inscripción.

1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), elija **Dispositivos** > **iOS/iPadOS** > **Inscripción de iOS** > **Tokens del programa de inscripción**.

2. Seleccione el token que acaba de instalar y elija **Perfiles** > **Crear perfil** > **iOS/iPadOS**.

3. En la página **Datos básicos**, escriba *TestProfile* como **Nombre** y *Prueba de ADE para dispositivos iOS/iPadOS* como **Descripción**. Los usuarios no ven estos detalles.

4. Seleccione **Siguiente**.

5. En la página**Configuración de administración**, decida si quiere que los dispositivos se inscriban con o sin **Afinidad de usuario**. Afinidad de usuario está diseñada para los dispositivos que utilizarán usuarios concretos. Si los usuarios van a usar el portal de empresa para servicios como la instalación de aplicaciones, seleccione **Inscribir con afinidad de usuario**. Si los usuarios no necesitan el portal de empresa o quiere aprovisionar el dispositivo para muchos usuarios, elija **Inscribir sin afinidad de usuario**.

6. Si opta por inscribir con afinidad de usuario, aparecerá la opción **Seleccionar dónde deben autenticarse los usuarios**. Decida si quiere Autenticar con el Portal de empresa o el Asistente de configuración de Apple.
   - **Portal de empresa**: seleccione esta opción para usar Multi-Factor Authentication, permitir a los usuarios cambiar las contraseñas al iniciar sesión por primera vez o pedir a los usuarios que restablezcan sus contraseñas expiradas durante la inscripción. Si quiere que la aplicación Portal de empresa se actualice automáticamente en los dispositivos de los usuarios finales, implemente de forma independiente el Portal de empresa como aplicación requerida para estos usuarios a través del programa de compras por volumen (VPP) de Apple.
   - **Asistente de configuración**: seleccione esta opción para usar la autenticación HTTP básica que proporciona Apple a través del Asistente de configuración de Apple.
  
7. Si decide inscribir con afinidad de usuario y autenticar con Portal de empresa, aparece la opción **Instalar Portal de empresa con VPP**. Si instala el Portal de empresa con un token de VPP, el usuario no tendrá que escribir un identificador y una contraseña de Apple para descargar el Portal de empresa desde la tienda de aplicaciones durante la inscripción. Elija **Usar token:** en **Instalar Portal de empresa con VPP** para seleccionar un token de VPP con licencias gratuitas del Portal de empresa disponibles. Si no quiere usar VPP para implementar el Portal de empresa, elija **No usar VPP**. 

8. Si ha elegido Inscribir con afinidad de usuario, Autenticar con el Portal de empresa e Instalar Portal de empresa con VPP, decida si quiere ejecutar el Portal de empresa en el modo de aplicación única hasta la autenticación. Esta configuración le permite asegurarse de que el usuario no tendrá acceso a otras aplicaciones hasta que haya terminado la inscripción corporativa. Si quiere restringir al usuario a este flujo hasta que se haya completado la inscripción, elija **Sí** en **Ejecutar el Portal de empresa en el modo de aplicación única hasta la autenticación**. 

9. En **Configuración de administración de dispositivos**, elija **Sí** en **Supervisada** (si elige **Inscribir con afinidad de usuario**, se establece automáticamente en **Sí**). Los dispositivos supervisados proporcionan la mayoría de las opciones de administración para los dispositivos iOS/iPadOS corporativos.

10. Elija **Sí** en **Inscripción bloqueada** para asegurarse de que los usuarios no pueden quitar la administración del dispositivo corporativo. 

11. Elija una opción en **Sincronizar con equipos** para determinar si los dispositivos iOS/iPadOS se podrán sincronizar con los equipos.

12. De forma predeterminada, Apple asigna el tipo de dispositivo (por ejemplo, iPad) como nombre del dispositivo. Si quiere especificar otra plantilla de nombre, elija **Sí** en **Aplicar plantilla de nombre de dispositivo**. Escriba el nombre que quiera aplicar a los dispositivos, donde las cadenas *{{SERIAL}}* y *{{DEVICETYPE}}* sustituirán el número de serie y el tipo de cada dispositivo. En caso contrario, elija **No** en **Aplicar plantilla de nombre de dispositivo**.

13. Elija **Siguiente**.

14. En la página **Asistente de configuración**, escriba *Departamento de tutoriales* como **Nombre del departamento**. Esta cadena es lo que los usuarios verán cuando pulsen **Acerca de la configuración** durante la activación del dispositivo.

15. En **Teléfono del departamento**, escriba un número de teléfono. Este número aparece cuando los usuarios pulsan el botón **Necesito ayuda** durante la activación.

16. También puede **Mostrar** u **ocultar** diversas pantallas durante la activación del dispositivo. Para obtener la mejor experiencia de inscripción, establezca todas las pantallas en **Ocultar**.

17. Elija **Siguiente** para ir a la página **Revisar y crear**. Seleccione **Crear**.

## <a name="sync-managed-devices-to-intune"></a>Sincronizar dispositivos administrados en Intune

Después de configurar un token del programa de inscripción con el portal de ABM, ASM o ADE, y asignar los dispositivos al servidor MDM, puede esperar a que se sincronicen con el servicio de Intune, o bien insertar manualmente una sincronización. Sin una sincronización manual, los dispositivos pueden tardar hasta 24 horas en aparecer en Azure Portal.

1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), elija **Dispositivos** > **iOS/iPadOS** > **Inscripción de iOS** > **Tokens del programa de inscripción** > elija un token de la lista > **Dispositivos** > **Sincronizar**.

## <a name="assign-an-enrollment-profile-to-iosipados-devices"></a>Asignar un perfil de inscripción a los dispositivos iOS/iPadOS

Debe asignar un perfil del Programa de inscripción a los dispositivos para poder inscribirlos. Estos dispositivos se sincronizan con Intune desde Apple y se les debe asignar el token de servidor MDM correcto en el portal de ABM, ASM o ADE.

1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), elija **Dispositivos** > **iOS/iPadOS** > **Inscripción de iOS** > **Tokens del programa de inscripción** y elija un token de la lista.
2. Elija **Dispositivos** > Elija los dispositivos de la lista > **Asignar perfil**.
3. En **Asignar perfil**, elija un perfil para los dispositivos y seleccione **Asignar**.

## <a name="distribute-devices-to-users"></a>Distribuir los dispositivos a los usuarios

Ha configurado la administración y sincronización entre Apple e Intune, y ha asignado un perfil para permitir la inscripción de los dispositivos de ADE. Ahora puede distribuir los dispositivos a los usuarios. Los dispositivos con afinidad de usuario necesitan que a cada usuario se le asigne una licencia de Intune.

## <a name="next-steps"></a>Pasos siguientes

Puede encontrar más información sobre otras opciones disponibles para la inscripción de dispositivos iOS/iPadOS.

> [!div class="nextstepaction"]
> [Artículo exhaustivo sobre la inscripción de ADE de iOS/iPadOS](device-enrollment-program-enroll-ios.md)

<!--commenting out because inaccurate>
## Clean up resources
<!--If you don't want to use iOS/iPadOS corporate enrolled devices anymore, you can delete them.>
<!--- If the devices are enrolled in Intune, you must first [delete them from the Azure Active Directory portal](../remote-actions/devices-wipe.md#delete-devices-from-the-azure-active-directory-portal).>
