---
title: Integración del conector de nube de Jamf Pro con Microsoft Intune
titleSuffix: Microsoft Intune
description: Use el conector de nube de Jamf Pro con directivas de cumplimiento de Microsoft Intune con acceso condicional de Azure Active Directory para ayudar a integrar y proteger los dispositivos administrados por Jamf.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/29/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 734a1361d8889ca1463e8d8986239e088b90cd09
ms.sourcegitcommit: eb51bb38d484e8ef2ca3ae3c867561249fa413f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/29/2020
ms.locfileid: "84206373"
---
# <a name="use-the-jamf-cloud-connector-with-microsoft-intune"></a>Uso del conector de nube de Jamf con Microsoft Intune

Este artículo puede ayudarle a instalar el conector de nube de Jamf para integrar Jamf Pro con Microsoft Intune. El conector de nube automatiza muchos de los pasos que son necesarios cuando se configura manualmente la integración, tal y como se documenta en el artículo [Integración de Jamf Pro con Intune para cumplimiento](../protect/conditional-access-integrate-jamf.md).

Al configurar el conector de nube:

- La configuración crea automáticamente las aplicaciones de Jamf Pro en Azure, lo que reemplaza la necesidad de configurarlas manualmente.
- Puede integrar varias instancias de Jamf Pro con el mismo inquilino de Azure que hospeda su suscripción a Intune.

Solo se admite la conexión de varias instancias de Jamf Pro con un solo inquilino de Azure cuando se usa el conector de nube. Si se usa una conexión configurada manualmente, solo puede integrarse una instancia de Jamf con un inquilino de Azure.

El uso del conector de nube es opcional:

- En el caso de los nuevos inquilinos que todavía no están integrados con Jamf, puede configurar el conector de nube como se describe en este artículo. O bien, puede configurar manualmente la integración como se describe en el artículo [Integración de Jamf Pro con Intune para cumplimiento](../protect/conditional-access-integrate-jamf.md).
- En el caso de los inquilinos que ya tienen una configuración manual, puede quitar esa integración y, a continuación, configurar el conector de nube. En este artículo se describe cómo eliminar una integración existente y cómo configurar el conector de nube.

Si tiene previsto reemplazar la integración anterior por el conector de nube de Jamf:

- Use el [procedimiento para quitar la configuración actual](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant), que incluye la eliminación de las aplicaciones empresariales para Jamf Pro y la deshabilitación de la integración manual. Después, puede usar el [procedimiento para configurar el conector de nube](#configure-the-cloud-connector-for-a-new-tenant).
- No necesitará volver a registrar los dispositivos. Los dispositivos que ya están registrados pueden usar el conector de nube sin que sea precisa ninguna configuración adicional.
- Asegúrese de configurar el conector de nube en un plazo de 24 horas después de quitar la integración manual para garantizar que los dispositivos registrados pueden continuar informando de su estado.

Para obtener más información sobre el conector de nube de Jamf, consulte [Configuring the macOS Intune Integration using the Cloud Connector](https://docs.jamf.com/technical-papers/jamf-pro/microsoft-intune/10.17.0/Configuring_the_macOS_Intune_Integration_using_the_Cloud_Connector.html) (Configuración de la integración de Intune con macOS mediante el conector de nube) en docs.jamf.com.

## <a name="prerequisites"></a>Requisitos previos

**Productos y servicios**:  
- Jamf Pro 10.18 o versiones posteriores
- Una cuenta de usuario de Jamf Pro con privilegios de acceso condicional  
- Microsoft Intune
- Microsoft Azure AD Premium
- [Aplicación Portal de empresa para macOS](https://aka.ms/macoscompanyportal)
- Dispositivos macOS con OS X 10.12 Yosemite o versiones posteriores

**Red**:  
Los siguientes puertos y puntos de conexión deben ser accesibles para Jamf e Intune para integrarse correctamente:

- **Intune**: Puerto 443
- **Apple**: puertos 2195, 2196 y 5223 (notificaciones push a Intune)
- **Jamf**: puertos 80 y 5223

- Puntos de conexión:
  - login.microsoftonline.com
  - graph.windows.net  
  - *.manage.microsoft.com  

Para que APNS funcione correctamente en la red, debe habilitar las conexiones salientes a los destinos siguientes, que también podrán ser orígenes de redireccionamiento:

- El bloque 17.0.0.0/8 de Apple a través de los puertos TCP 5223 y 443 desde todas las redes cliente.
- Los puertos 2195 y 2196 de los servidores de Jamf Pro.

Para obtener más información sobre estos puertos, vea los artículos siguientes:

- [Ancho de banda y requisitos de configuración de red de Intune](../fundamentals/network-bandwidth-use.md).
- [Puertos de red usados por Jamf Pro](https://www.jamf.com/jamf-nation/articles/34/network-ports-used-by-jamf-pro) en jamf.com.
- [Puertos TCP y UDP usados por los productos de software de Apple](https://support.apple.com/HT202944) en support.apple.com.

**Cuentas**:  
Los procedimientos descritos en este artículo requieren el uso de cuentas con los permisos siguientes:

- **Consola de Jamf Pro**: una cuenta con permisos para administrar Jamf Pro
- **Centro de administración de Microsoft Endpoint Manager**: Administrador global
- **Azure Portal**: Administrador global

## <a name="remove-the-jamf-pro-integration-for-a-previously-configured-tenant"></a>Eliminación de la integración de Jamf Pro para un inquilino configurado previamente

Use el siguiente procedimiento para quitar una integración de Jamf Pro configurada manualmente de su inquilino de Azure *antes* de configurar el conector de nube.

Si no ha configurado previamente una conexión entre Jamf Pro e Intune, o bien tiene una o más conexiones que ya usan el conector de nube, omita este procedimiento y comience con la [configuración del conector de nube para un nuevo inquilino](#configure-the-cloud-connector-for-a-new-tenant).

### <a name="remove-a-manually-configured-jamf-pro-integration"></a>Eliminación de una integración de Jamf Pro configurada manualmente

1. Inicie sesión en la consola de Jamf Pro.

2. Seleccione **Settings** (Configuración), el icono de engranaje en la esquina superior derecha, y luego vaya a **Global Management** (Administración global) > **Conditional Access** (Acceso condicional).

   ![Navegación a "Conditional Access"](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. Seleccione **Edit** (Editar).

4. Desactive la casilla **Enable Intune Integration for macOS** (Habilitar la integración de Intune para macOS).

   Al anular la selección de esta opción, se deshabilita la conexión y se guarda la configuración.

5. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) y vaya a **Administración de inquilinos** > **Administración de dispositivos de socio**.

   En el nodo **Administración de dispositivos de socio**, elimine el **identificador de la aplicación** en el campo **Proporcione el id. de aplicación de Azure Active Directory para Jamf** y, a continuación, seleccione **Guardar**.

   El identificador de la aplicación es el id. de la aplicación empresarial de Azure que se ha creado en Azure al configurar una integración manual si Jamf Pro.

6. Inicie sesión en [Azure Portal](https://portal.azure.com/) con una cuenta que tenga permisos de administrador global y vaya a **Azure Active Directory** > **Aplicaciones empresariales**.

   Busque las dos aplicaciones de Jamf y elimínelas. Las nuevas aplicaciones se crearán automáticamente al configurar el conector de nube de Jamf mediante el procedimiento siguiente.

   ![Selección de las aplicaciones de Jamf que se van a eliminar](./media/conditional-access-jamf-cloud-connector/delete-jamf-apps.png)

   Después de deshabilitar la integración en Jamf Pro y eliminar las aplicaciones empresariales, el nodo **Administración de dispositivos de socio** muestra el estado de conexión **Terminada**.

   ![Estado de conexión "Terminada"](./media/conditional-access-jamf-cloud-connector/terminated-connection-status.png)

Ahora que ha quitado correctamente la configuración manual de la integración de Jamf Pro, puede configurar la integración mediante el conector de nube. Para ello, consulte la sección [Configuración del conector de nube para un nuevo inquilino](#configure-the-cloud-connector-for-a-new-tenant) de este artículo.

## <a name="configure-the-cloud-connector-for-a-new-tenant"></a>Configuración del conector de nube para un nuevo inquilino

Use este procedimiento para configurar el conector de nube de Jamf para integrar Jamf Pro y Microsoft Intune en estos casos:

- No tiene ninguna integración entre Jamf Pro e Intune configurada para su inquilino de Azure.
- Ya tiene un conector de nube configurado entre Jamf Pro e Intune en su inquilino de Azure y quiere integrar una instancia de Jamf adicional con su suscripción.

Si actualmente tiene una integración configurada manualmente entre Intune y Jamf Pro, consulte la sección [Eliminación de la integración de Jamf Pro para un inquilino configurado previamente](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant) de este artículo para quitar esa integración antes de continuar. Es necesario eliminar las integraciones configuradas manualmente para poder configurar correctamente el conector de nube de Jamf.

### <a name="create-a-new-connection"></a>Creación de una nueva conexión

1. Inicie sesión en la consola de Jamf Pro.

2. Seleccione **Settings** (Configuración), el icono de engranaje en la esquina superior derecha, y luego vaya a **Global Management** (Administración global) > **Conditional Access** (Acceso condicional).

   ![Navegación a "Conditional Access"](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. Seleccione **Edit** (Editar).

4. Active la casilla **Enable Intune Integration for macOS** (Habilitar la integración de Intune para macOS).
   - Seleccione esta opción para que Jamf Pro envíe actualizaciones de inventario a Microsoft Intune.
   - Puede anular la selección de esta opción para deshabilitar la conexión y guardar la configuración.

   > [!IMPORTANT]
   > Si la casilla **Enable Intune Integration for macOS** (Habilitar la integración de Intune para macOS) ya está seleccionada y el tipo de conexión (*Connection Type*) está establecido en **Manual**, debe quitar esa integración para poder continuar. Consulte la sección [Eliminación de la integración de Jamf Pro para un inquilino configurado previamente](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant) de este artículo antes de continuar.

5. En *Connection Type* (Tipo de conexión), seleccione **Cloud Connector** (Conector de nube).

   ![Selección de "Cloud Connector" en la consola de Jamf Pro](./media/conditional-access-jamf-cloud-connector/select-cloud-connector.png)

6. En el menú emergente **Sovereign Cloud** (Nube soberana), seleccione la ubicación de la nube soberana de Microsoft. Si va a reemplazar la integración anterior con el conector de nube de Jamf, puede omitir este paso si se ha especificado la ubicación.

7. Seleccione una de las siguientes opciones de página de destino para los equipos que no reconoce Microsoft Azure:
   - **La página de registro de dispositivos predeterminada de Jamf Pro**: en función del estado del dispositivo macOS, esta opción redirige a los usuarios al portal de inscripción de dispositivos de Jamf Pro (para inscribirse con Jamf Pro) o a la aplicación Portal de empresa de Intune (para registrarse con Azure AD).
   - **La página de acceso denegado**
   - **Una URL personalizada**
  
   Si va a reemplazar la integración anterior con el conector de nube de Jamf, puede omitir este paso si se ha especificado la página de aterrizaje.
  
8. Seleccione **Conectar**. Se le redirigirá para registrar las aplicaciones de Jamf Pro en Azure.

   Cuando se le solicite, especifique sus credenciales de Microsoft Azure y siga las instrucciones en pantalla para conceder los permisos solicitados. Deberá conceder permisos para el **conector de nube** y, después, para la **aplicación de registro de usuarios del conector de nube**. Ambas aplicaciones se registran en Azure como aplicaciones empresariales.

   Una vez concedidos los permisos para las dos aplicaciones, se abrirá la página **Application ID** (Identificador de la aplicación).

9. En la página **Application ID** (Identificador de la aplicación), seleccione **Copy and open Intune** (Copiar y abrir Intune).

   ![Identificador de aplicación](./media/conditional-access-jamf-cloud-connector/copy-application-id.png)

   El *identificador de la aplicación* se copia en el portapapeles del sistema para usarlo en el paso siguiente y se abre el nodo **Administración de dispositivos de socio** en el *centro de administración de Microsoft Endpoint Manager*. (**Administración de inquilinos** > **Administración de dispositivos de socio**).

10. En el nodo **Administración de dispositivos de socio**, *pegue* el **identificador de la aplicación** en el campo **Proporcione el id. de aplicación de Azure Active Directory para Jamf** y, a continuación, seleccione **Guardar**.

    ![Configuración de la administración de dispositivos de socio](./media/conditional-access-jamf-cloud-connector/partner-device-management.png)

11. Vuelva a la página "Application ID" en Jamf Pro y seleccione **Confirm** (Confirmar).

12. Jamf Pro completa y prueba la configuración, y muestra si la conexión se ha realizado correctamente o no en la página de configuración "Conditional Access". La imagen siguiente es un ejemplo de conexión satisfactoria:

    ![Configuración satisfactoria confirmada en Jamf Pro](./media/conditional-access-jamf-cloud-connector/successful-configuration.png)

13. En el centro de administración de Microsoft Endpoint Manager, actualice el nodo **Administración de dispositivos de socio**. La conexión debería aparecer ahora con el estado **Activa**:

    ![Estado de conexión "Activa"](./media/conditional-access-jamf-cloud-connector/active-connection-status.png)

Cuando la conexión entre Jamf Pro y Microsoft Intune se establece correctamente, Jamf Pro envía información de inventario a Microsoft Intune para cada equipo registrado con Azure AD (el registro con Azure AD es un flujo de trabajo del usuario final). Puede ver el estado de inventario del acceso condicional para un usuario y un equipo en la categoría Cuenta de usuario local de la información de inventario de un equipo en Jamf Pro.

Después de integrar una instancia de Jamf Pro mediante el conector de nube de Jamf, puede usar este mismo procedimiento para configurar instancias adicionales de Jamf Pro con la misma suscripción a Intune en su inquilino de Azure.  

## <a name="set-up-compliance-policies-and-register-devices"></a>Configurar directivas de cumplimiento y registrar dispositivos

Después de configurar la integración entre Intune y Jamf, tiene que [aplicar directivas de cumplimiento en los dispositivos administrados por Jamf](../protect/conditional-access-assign-jamf.md).

## <a name="disconnect-jamf-pro-and-intune"></a>Desconexión de Jamf Pro e Intune

Si necesita quitar la integración de Jamf Pro con Intune, siga los siguientes pasos para eliminar la conexión de la consola de Jamf Pro. Esta información se aplica tanto para el conector de nube como para una integración configurada manualmente.

1. En Jamf Pro, vaya a **Administración global** > **Acceso condicional**. En la pestaña **Integración de MacOS Intune**, seleccione **Editar**.

2. Desactive la casilla **Enable Intune Integration for macOS** (Habilitar la integración de Intune para macOS).

3. Seleccione **Guardar**. Jamf Pro enviará la configuración a Intune y se terminará la integración.

4. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

5. Seleccione **Administración de inquilinos** > **Conectores y tokens** > **Administración de dispositivos de socio** para comprobar que el estado es ahora **Finalizado**.

   > [!NOTE]
   > Los dispositivos Mac de la organización se retirarán en la fecha (tres meses) que se muestra en la consola.

## <a name="get-support-for-the-cloud-connector"></a>Soporte técnico para el conector de nube

Como el conector de nube crea automáticamente las aplicaciones empresariales de Azure necesarias para la integración, su primer punto de contacto para obtener soporte técnico debe ser **Jamf**. Las opciones son:

- Contacte con el soporte técnico mediante la dirección de correo electrónico: `support@jamf.com`
- Use el portal de soporte técnico de Jamf Nation: https://www.jamf.com/support/ 


Antes de ponerse en contacto con el servicio de soporte técnico:

- Revise los requisitos previos, como los puertos y la versión del producto que usa.
- Confirme que no se han modificado los permisos para las dos aplicaciones siguientes de Jamf Pro creadas en Azure. Los cambios en los permisos de las aplicaciones no son compatibles con Intune y pueden producir errores en la integración.

  **Aplicación de registro de usuarios del conector de nube**:
  - Nombre de la API: Microsoft Graph
    - Permiso: Iniciar sesión y leer el perfil de usuario
    - Tipo: delegado
    - Concedido mediante: consentimiento del administrador
    - Concedido por: un administrador

  **Aplicación del conector de nube**:
  - Nombre de la API: Microsoft Graph (instancia 1)
    - Permiso: Iniciar sesión y leer el perfil de usuario
    - Tipo: delegado
    - Concedido mediante: consentimiento del administrador
    - Concedido por: un administrador

  - Nombre de la API: Microsoft Graph (instancia 2)
    - Permiso: Leer datos de directorio
    - Tipo: Aplicación
    - Concedido mediante: consentimiento del administrador
    - Concedido por: un administrador

  - Nombre de la API: API de Intune
    - Permiso: Enviar atributos del dispositivo a Microsoft Intune
    - Tipo: Aplicación
    - Concedido mediante: consentimiento del administrador
    - Concedido por: un administrador

## <a name="common-questions-about-the-jamf-cloud-connector"></a>Preguntas frecuentes sobre el conector de nube de Jamf

### <a name="what-data-is-shared-via-the-cloud-connector"></a>¿Qué datos se comparten mediante el conector de nube?

El conector de nube se autentica con Microsoft Azure y envía datos de inventario de dispositivos de Jamf Pro a Azure. Además, el conector de nube administra la detección de servicios en Azure, el intercambio de tokens, los errores de comunicación y la recuperación ante desastres.

### <a name="where-is-device-inventory-data-stored"></a>¿Dónde se almacenan los datos de inventario de dispositivos?

Los datos de inventario de dispositivos se almacenan en la base de datos de Jamf Pro.

### <a name="what-credentials-are-stored"></a>¿Qué credenciales se almacenan?

No se almacena ninguna credencial. Al configurar el conector de nube, los administradores deben dar su consentimiento para agregar la aplicación multiinquilino de Jamf y la aplicación de conexión nativa de macOS a su inquilino de Azure AD. Una vez agregada la aplicación multiinquilino, el conector de nube solicita tokens de acceso para interactuar con la API de Azure. El acceso a la aplicación se puede revocar desde Microsoft Azure en cualquier momento para restringir el acceso.

### <a name="how-is-data-encrypted"></a>¿Cómo se cifran los datos?

El conector de nube usa Seguridad de la capa de transporte (TLS) para los datos enviados entre Jamf Pro y Microsoft Azure.

### <a name="how-does-jamf-know-which-device-is-associated-with-which-instance-of-jamf-pro"></a>¿Cómo sabe Jamf qué dispositivo está asociado a cada instancia de Jamf Pro?

Jamf Pro usa microservicios en AWS para enrutar correctamente la información de los dispositivos a la instancia correcta.

### <a name="can-i-switch-from-using-the-cloud-connector-to-the-manual-connection-type"></a>¿Puedo cambiar del conector de nube al tipo de conexión manual?

Sí. Puede volver a cambiar el tipo de conexión a manual y seguir los pasos para la configuración manual. Si tiene alguna pregunta, contacte con Jamf para obtener ayuda.

### <a name="permissions-were-modified-on-one-or-both-required-apps-cloud-connector-and-cloud-connector-user-registration-app-and-registration-is-not-working-is-this-supported"></a>Los permisos se han modificado en una o en las dos aplicaciones requeridas (la *aplicación del conector de nube* y la *aplicación de registro de usuarios del conector de nube*) y el registro no funciona, ¿se admite esto?

No se admite la modificación de los permisos en las aplicaciones.

### <a name="is-there-a-log-file-in-jamf-pro-that-shows-if-the-connection-type-has-been-changed"></a>¿Hay un archivo de registro en Jamf Pro que muestra si se ha cambiado el tipo de conexión?

Sí, los cambios se registran en el archivo JAMFChangeManagement.log. Para ver los registros de administración de cambios, inicie sesión en Jamf Pro, vaya a **Settings** > **System Settings** > **Change Management** > **Logs** (Configuración > Configuración del sistema > Administración de cambios > Registros), busque **Object type** (Tipo de objeto) para **Conditional Access** (Acceso condicional) y, después, haga clic en **Details** (Detalles) para ver los cambios.

## <a name="next-steps"></a>Pasos siguientes

- [Aplicación de directivas de cumplimiento en los dispositivos administrados por Jamf](../protect/conditional-access-assign-jamf.md)
- [Datos que Jamf envía a Intune](../protect/data-jamf-sends-to-intune.md)
