---
title: Configuración de la integración de Wandera Mobile Threat Protection con Intune
titleSuffix: Intune on Azure
description: Cómo configurar la solución Wandera Mobile Threat Protection con Microsoft Intune para controlar el acceso de los dispositivos móviles a los recursos corporativos.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: b227148a6e16f7c9f8d62cb58eeb628afbd84123
ms.sourcegitcommit: 2e0bc4859f7e27dea20c6cc59d537a31f086c019
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86872025"
---
# <a name="integrate-wandera-mobile-threat-protection-with-intune"></a>Integración de Wandera Mobile Threat Protection con Intune  

Complete los pasos siguientes para integrar la solución Wandera Mobile Threat Defense con Intune.  

## <a name="before-you-begin"></a>Antes de comenzar  

Antes de iniciar el proceso para integrar Wandera con Intune, asegúrese de que cumple los siguientes requisitos previos:

- Suscripción a Intune
- Credenciales de administrador de Azure Active Directory y rol asignado que puede conceder los permisos siguientes:

    - Iniciar sesión y leer el perfil de usuario
    - Obtener acceso al directorio con el usuario que tiene la sesión iniciada
    - Leer datos de directorio
    - Enviar información de riesgo del dispositivo a Intune
 
- Suscripción válida a Wandera
    - Cuenta de administrador con privilegios de superadministrador

## <a name="integration-overview"></a>Información general de la integración

La habilitación de la integración de Mobile Threat Defense entre Wandera e Intune conlleva:

- la habilitación del servicio UEM Connect de Wandera para sincronizar información con Azure e Intune, lo cual incluye metadatos de administración del ciclo de vida (LCM) de usuario y dispositivo, junto con el nivel de amenaza de dispositivo de Mobile Threat Defense (MTD);
- la creación de perfiles de activación en Wandera para definir el comportamiento de inscripción de dispositivos;
- la implementación de forma inalámbrica en dispositivos iOS y Android administrados;
- la configuración de Wandera para autoservicio del usuario final con MAM-WE en dispositivos iOS y Android no administrados.

## <a name="set-up-wandera-mobile-threat-defense-integration"></a>Configuración de la integración de Wandera Mobile Threat Defense

La configuración de la integración entre Wandera e Intune no requiere soporte técnico por parte del personal de Wandera, y se puede realizar fácilmente en cuestión de minutos.

### <a name="enable-support-for-wandera-in-intune"></a>Habilitar la compatibilidad con Wandera en Intune

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione **Administración de inquilinos** > **Conectores y tokens** > **Mobile Threat Defense** > **Agregar**.
3. En la página **Agregar conector**, use la lista desplegable y seleccione **Wandera**. Después seleccione **Crear**.  
4. En el panel Mobile Threat Defense, seleccione el conector MTD de **Wandera** en la lista de conectores para abrir el panel **Editar conector**. Seleccione **Open the Wandera admin console** (Abrir la consola de administración de Wandera) para abrir [RADAR](https://radar.wandera.com/login), la consola de administración de Wandera, e inicie sesión. 
5. En la consola de RADAR de Wandera, vaya a **Integrations > UEM Integration** (Integraciones > Integración de UEM) y seleccione la pestaña **UEM Connect**. Use la lista desplegable EMM Vendor (Proveedor de EMM) y seleccione **Microsoft Intune**.
6. Aparecerá una pantalla similar a la siguiente, que indica las concesiones de permisos necesarias para completar la integración:

   ![Integraciones y permisos](./media/wandera-mtd-connector-integration/integrations-and-permissions.png) 

7. Junto a Intune User and Device Sync (Sincronización de usuarios y dispositivos de Intune), haga clic en el botón Grant (Conceder) para iniciar el proceso con el fin de dar su consentimiento a Wandera para realizar funciones de administración del ciclo de vida (LCM) con Azure e Intune.
8. Cuando se le solicite, seleccione o escriba sus credenciales de administrador de Azure. Revise los permisos solicitados y, después, active la casilla para dar su consentimiento en nombre de su organización. Por último, haga clic en Aceptar para autorizar la integración de LCM.

   ![Aceptar permisos](./media/wandera-mtd-connector-integration/permissions.png)

9. Automáticamente, regresará a la consola de administración de RADAR.  Si la autorización se ha realizado correctamente, verá una marca de verificación verde junto al botón Grant (Conceder).
10. Repita el proceso de consentimiento para las integraciones restantes de la lista; para ello, haga clic en los botones de concesión correspondientes hasta que tenga marcas de verificación verdes junto a cada una.

11. Vuelva a la consola de Intune y continúe editando el conector MTD de Wandera. Active todos los conmutadores disponibles y guarde la configuración.

    ![Habilitar Wandera](./media/wandera-mtd-connector-integration/enable-wandera.png)

Intune y Wandera ya están conectados.

## <a name="create-activation-profiles-in-wandera"></a>Creación de perfiles de activación en Wandera

Las implementaciones basadas en Intune se facilitan mediante los perfiles de activación de Wandera definidos en RADAR.  Cada perfil de activación define opciones de configuración específicas, como los requisitos de autenticación, las capacidades del servicio y la pertenencia inicial al grupo.

Después de crear un perfil de activación en Wandera, debe "asignarlo" a los usuarios y dispositivos de Intune.  Aunque un perfil de activación es universal para las distintas plataformas de dispositivos y estrategias de administración, los pasos siguientes definen cómo configurar Intune en función de estas diferencias.

En los pasos siguientes se supone que ha creado un perfil de activación en Wandera que quiere implementar mediante Intune en los dispositivos de destino. Consulte la [guía sobre los perfiles de activación](https://radar.wandera.com/?return_to=https://wandera.force.com/Customer/s/article/Enrollment-Links) para obtener más información sobre la creación y el uso de perfiles de activación de Wandera.

> [!NOTE]
> Al crear perfiles de activación para implementarlos a través de Intune o MAM-WE, asegúrese de establecer "Usuario asociado" en autenticado mediante la opción Proveedor de identidades > Azure Active Directory. De este modo, obtendrá una seguridad máxima, compatibilidad entre plataformas y una experiencia de usuario final simplificada.

## <a name="deploying-wandera-over-the-air-to-mdm-managed-devices"></a>Implementación de Wandera de forma inalámbrica en dispositivos administrados por MDM

En los dispositivos iOS y Android que están administrados por Intune, Wandera se puede implementar de forma inalámbrica para lograr activaciones push rápidas. Asegúrese de que ya ha creado los perfiles de activación que necesita antes de continuar con esta sección. La implementación de Wandera en dispositivos administrados implica:
- agregar perfiles de configuración de Wandera a Intune y asignarlos a los dispositivos de destino;
- agregar la aplicación Wandera y las respectivas configuraciones de aplicación a Intune y asignarlas a los dispositivos de destino.

### <a name="configure-and-deploy-ios-configuration-profiles"></a>Configuración e implementación de perfiles de configuración de iOS 

En esta sección, descargaremos los archivos de configuración de los dispositivos iOS **necesarios** y los entregaremos de forma inalámbrica a los administrados por Intune a través de MDM.

1. En **RADAR**, vaya al perfil de activación que quiera implementar (Devices > Activations [Dispositivos > Activaciones]) y, después, haga clic en la pestaña **Deployment Strategies > Managed Devices > Microsoft Endpoint Manager** (Estrategias de implementación > Dispositivos administrados > Microsoft Endpoint Manager).
2. Expanda las secciones **Apple iOS Supervised** (Supervisado) o **Apple iOS Unsupervised** (No supervisado), en función de la configuración de su flota de dispositivos.
3. Descargue los perfiles de configuración proporcionados y prepárese para cargarlos en el siguiente paso.
4. Abra la **Consola de administración de Microsoft Intune** y vaya a **Dispositivos > iOS/iPadOS > Perfiles de configuración**.  Haga clic en **Crear perfil**.
5. En el panel que aparece, elija **iOS/iPadOS** en **Plataforma** y **Personalizado** en Perfil. Después, haga clic en **Crear**.
6. En el campo **Nombre**, proporcione un título descriptivo para la configuración; lo ideal es que coincida con el nombre del perfil de activación en RADAR. Esto le facilitará hacer referencias cruzadas en el futuro. Si lo prefiere, también puede proporcionar el código de perfil de activación. Se recomienda agregar un sufijo al nombre para indicar si la configuración es para dispositivos supervisados o no supervisados.
7. Opcionalmente, puede proporcionar una **Descripción** en la que informe a los demás administradores sobre el propósito y el uso de la configuración. Haga clic en **Siguiente**.
8. Haga clic en **Seleccionar un archivo** y busque el perfil de configuración descargado que se corresponda con el perfil de activación correspondiente descargado en el paso 3. Preste atención para seleccionar el perfil supervisado o no supervisado adecuado, en caso de haber descargado ambos. Haga clic en **Siguiente**.
   <!-- image placeholder - ending future availability -->
9.  Defina **Etiquetas de ámbito** según sea necesario para las prácticas de RBAC de Intune.  Haga clic en **Siguiente**.
10. **Asigne** el perfil de configuración a los grupos de usuarios o dispositivos que deben tener instalado Wandera.  Se recomienda comenzar con un grupo de prueba y expandirlo después validar que las activaciones funcionan correctamente. Haga clic en **Siguiente**.
11. Compruebe que la configuración sea correcta y haga los cambios necesarios; después, haga clic en **Crear** para crear e implementar el perfil de configuración.

> [!NOTE]
> Wandera ofrece un perfil de implementación mejorado para dispositivos iOS supervisados. Si tiene una flota mixta de dispositivos supervisados y no supervisados, repita los pasos anteriores para el otro tipo de perfil según sea necesario. Estos mismos pasos deben seguirse para todos los perfiles de activación futuros que se vayan a implementar a través de Intune. Póngase en contacto con el soporte técnico de Wandera si tiene una flota mixta de dispositivos iOS supervisados y no supervisados y necesita ayuda con la asignación de directivas basadas en el modo supervisado. 

## <a name="deploying-wandera-to-mam-we-devices"></a>Implementación de Wandera en dispositivos MAM-WE
En el caso de los dispositivos que no están administrados por Intune y que son dispositivos MAM-WE, Wandera usa una experiencia de incorporación basada en la autenticación integrada para activar y proteger los datos de la empresa en aplicaciones habilitadas para MAM. 

En las secciones siguientes se describe cómo configurar Wandera e Intune de modo que los usuarios finales puedan activar Wandera de forma fácil antes de poder acceder a los datos de la empresa. 

### <a name="configure-azure-device-provisioning-in-a-wandera-activation-profile"></a>Configuración del aprovisionamiento de dispositivos de Azure en un perfil de activación de Wandera
Los perfiles de activación que se usarán con MAM-WE deben tener el usuario asociado establecido en autenticado mediante la opción Proveedor de identidades > Azure Active Directory.
1. En el portal **RADAR de Wandera**, seleccione el perfil de activación (o cree uno nuevo) que usarán los dispositivos MAM-WE durante la inscripción en Devices > Activations (Dispositivos > Activaciones). 
2. Haga clic en la pestaña **Deployment Strategies y Unmanaged Devices** (Estrategias de implementación > Dispositivos no administrados). Después, desplácese a la sección **Azure Device Provisioning** (Aprovisionamiento de dispositivos de Azure).
3. Especifique su **id. de inquilino de Azure AD** en el campo de texto correspondiente. Si no tiene a mano su identificador de inquilino, haga clic en el vínculo **Get my Tenant ID** (Obtener mi id. de inquilino) para abrir Azure AD en una nueva pestaña donde podrá copiar fácilmente este valor en el portapapeles.
4. Si quiere, especifique identificadores de grupo en **Group ID(s)** para limitar las activaciones de usuario a grupos específicos.
   - Si se definen uno o varios **identificadores de grupo**, un usuario que active MAM-WE debe ser miembro de al menos uno de los grupos especificados para poder activar con este perfil de activación.
   - Se pueden configurar varios perfiles de activación con el mismo identificador de inquilino de Azure, pero tiene que ser con identificadores de grupo diferentes. Esto permite inscribir dispositivos en Wandera en función de la pertenencia al grupo de Azure, lo que habilita funcionalidades diferenciadas por grupo en el momento de la activación.
   - Puede configurar un único perfil de activación "predeterminado" que no especifique ningún id. de grupo.  Este grupo actuará como comodín para todas las activaciones en las que el usuario autenticado no sea miembro de un grupo con una asociación a otro perfil de activación.
5. Haga clic en **Guardar** en la esquina superior derecha de la página.

## <a name="next-steps"></a>Pasos siguientes
- Una vez que haya cargado los perfiles de activación de Wandera en RADAR, cree aplicaciones cliente en Intune para implementar la aplicación de Wandera en dispositivos iOS/iPadOS y Android. La configuración de la aplicación de Wandera proporciona una funcionalidad esencial para complementar los perfiles de configuración de dispositivos insertados, y se recomienda para todas las implementaciones. Consulte [Agregar y asignar aplicaciones de Mobile Threat Defense (MTD) con Intune](mtd-apps-ios-app-configuration-policy-add-assign.md) para los procedimientos y detalles personalizados específicos de las aplicaciones de Wandera. 
- Ahora que Wandera ya está integrado con Endpoint Manager, puede ajustar la configuración, ver informes e implementarlos de manera más amplia en toda la flota de dispositivos móviles. Para consultar guías detalladas de configuración, vea la [guía de introducción del centro de soporte técnico](https://radar.wandera.com/?return_to=https://wandera.force.com/Customer/s/getting-started) en la documentación de Wandera.
