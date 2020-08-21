---
title: Tutorial&#58; Habilitación de la administración conjunta para clientes existentes
titleSuffix: Configuration Manager
description: Configure la administración conjunta con Microsoft Intune cuando ya administra dispositivos Windows 10 con Configuration Manager.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cc05ae5a9be6c437fab60f8c4c5a45d61e8c3e65
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694889"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>Tutorial: Habilitación de la administración conjunta para clientes existentes de Configuration Manager

Con la administración conjunta, puede mantener sus procesos estandarizados para el uso de Configuration Manager para administrar los equipos de su organización. Al mismo tiempo, está invirtiendo en la nube mediante el uso de Intune para la seguridad y el aprovisionamiento moderno.  

En este tutorial, va a configurar la administración conjunta de dispositivos Windows 10 que ya están inscritos en Configuration Manager. Este tutorial comienza con la premisa de que ya usa Configuration Manager para administrar los dispositivos Windows 10.

Use este tutorial cuando:  

- Tiene una instancia de Active Directory local que puede conectar a Azure Active Directory (Azure AD) en una configuración de Azure AD híbrida.

  Si no puede implementar una instancia híbrida de Azure Active Directory (AD) que se une a su AD local con Azure AD, se recomienda seguir nuestro tutorial complementario para la [habilitación de la administración conjunta para los nuevos dispositivos Windows 10 basados en Internet](tutorial-co-manage-new-devices.md).
- Tiene clientes existentes en Configuration Manager que desea asociar a la nube.

**En este tutorial aprenderá a:**  
> [!div class="checklist"]
> * Revisar los requisitos previos para su entorno local y Azure
> * Configuración de Azure AD híbrido  
> * Configurar los agentes de cliente de Configuration Manager para registrarse con Azure AD  
> * Configurar Intune para la inscripción automática de dispositivos  
> * Habilitación de la administración conjunta en Configuration Manager  

## <a name="prerequisites"></a>Requisitos previos  

### <a name="azure-services-and-environment"></a>Entorno y servicios de Azure

- Suscripción de Azure ([evaluación gratuita](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Suscripción a Microsoft Intune
  > [!TIP]  
  > Una suscripción a Enterprise Mobility + Security (EMS) incluye Azure Active Directory Premium y Microsoft Intune. Una suscripción a EMS ([evaluación gratuita](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

Si no está ya presente en su entorno, durante este tutorial, necesitará:

- Configurar [Azure AD Connect](/azure/active-directory/hybrid/how-to-connect-install-select-installation) entre su instancia de Active Directory local y su inquilino de Azure Active Directory (AD).

> [!TIP]
> Ya no es necesario comprar ni asignar licencias individuales de Intune o EMS a los usuarios. Para más información, vea [Preguntas más frecuentes sobre productos y licencias](../core/understand/product-and-licensing-faq.md#bkmk_mem).

### <a name="on-premises-infrastructure"></a>Infraestructura local

- Una [versión compatible](../core/servers/manage/updates.md#supported-versions) de la rama actual de Configuration Manager
- La autoridad de administración de dispositivos móviles (MDM) se debe establecer en Intune.  

### <a name="permissions"></a>Permisos

A lo largo de este tutorial, use los siguientes permisos para completar las tareas:

- Una cuenta que sea un *administrador de dominio* en su infraestructura local  
- Una cuenta que sea un *administrador total* para *todos* los ámbitos en Configuration Manager
- Una cuenta de *administrador global* en Azure Active Directory (Azure AD)
   - Asegúrese de que ha asignado una licencia de Intune a la cuenta que usa para iniciar sesión en el inquilino. De lo contrario, no se podrá iniciar sesión y aparecerá el mensaje de error "Usuario no reconocido". <!--mem issue 169-->

## <a name="set-up-hybrid-azure-ad"></a>Configuración de Azure AD híbrido

Cuando configura un entorno híbrido de Azure AD, realmente está configurando la integración de una instancia local de AD con Azure AD mediante Azure AD Connect y Servicios de federación de Active Directory (AD FS). Con una configuración correcta, los trabajadores pueden perfectamente iniciar sesión en sistemas externos mediante sus credenciales de AD locales.

> [!IMPORTANT]  
> Este tutorial detalla un proceso básico para configurar Azure AD híbrido para un dominio administrado. Se recomienda estar familiarizado con el proceso y no basarse en este tutorial como guía para comprender e implementar el entorno de Azure AD híbrido.
>
> Para obtener más información acerca de Azure AD híbrido, comience con los siguientes artículos en la documentación de Azure Active Directory:
>
> - [Planeación de la implementación de la unión a Azure AD](/azure/active-directory/devices/azureadjoin-plan)
> - [Planeamiento de la implementación de la unión a Azure Active Directory híbrido](/azure/active-directory/devices/hybrid-azuread-join-plan)
> - [Control de la unión a Azure AD híbrido de los dispositivos](/azure/active-directory/devices/hybrid-azuread-join-control)
> - [Configuración de dispositivos híbridos unidos a Azure Active Directory para dominios federados](/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  

### <a name="set-up-azure-ad-connect"></a>Configuración de Azure AD Connect

Azure AD híbrido requiere la configuración de Azure AD Connect para mantener sincronizadas las cuentas del equipo en su Active Directory (AD) local y el objeto del dispositivo en Azure AD.

A partir de la versión 1.1.819.0, Azure AD Connect proporciona un asistente para configurar la unión a Azure AD híbrido. El uso de dicho asistente simplifica el proceso de configuración.  

Para configurar Azure AD Connect, necesita credenciales de administrador global para Azure AD.  

> [!TIP]  
> El siguiente procedimiento no debe considerarse autoritativo para la configuración de Azure AD Connect, pero se proporciona aquí para ayudar a simplificar la configuración de la administración conjunta entre Intune y Configuration Manager. Para ver el contenido autoritativo sobre este y otros procedimientos relacionados para la configuración de Azure AD, consulte [Configuración de dispositivos híbridos unidos a Azure Active Directory para dominios administrados](/azure/active-directory/devices/hybrid-azuread-join-managed-domains) en la documentación de Azure AD.  

#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>Configuración de una unión a Azure AD híbrida con Azure AD Connect

1. Obtenga e instale la [versión más reciente de Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 o superior).  
2. Inicie Azure AD Connect y, a continuación, seleccione **Configurar**.
3. En la página **Tareas adicionales**, seleccione **Configurar opciones de dispositivo** y, a continuación, seleccione **Siguiente**.
4. En la página **Información general**, seleccione **Siguiente**.
5. En la página **Conectarse a Azure AD**, escriba las credenciales de administrador global para Azure AD.
6. En la página **Opciones de dispositivo**, seleccione **Configurar la combinación de Azure AD híbrido** y, a continuación, seleccione **Siguiente**.
7. En la página **Sistemas operativos de dispositivos**, seleccione los sistemas operativos que usan los dispositivos en su entorno de Active Directory y, a continuación, seleccione **Siguiente**.  

   Puede seleccionar la opción para admitir los dispositivos unidos al dominio de nivel inferior de Windows, pero tenga en cuenta que la administración conjunta de dispositivos solo se admite para Windows 10.
8. En la página **SCP**, para cada bosque local que desee que Azure AD Connect configure para el punto de conexión de servicio (SCP), realice los siguientes pasos y luego seleccione **Siguiente**:  
   1. Seleccione el bosque.  
   2. Seleccione el servicio de autenticación.  Si tiene un dominio federado, seleccione el servidor de AD FS, a menos que su organización tenga exclusivamente clientes de Windows 10 y haya configurado la sincronización de equipo o dispositivo o su organización use [SeamlessSSO](/azure/active-directory/hybrid/how-to-connect-sso).  
   3. Haga clic en **Agregar** para escribir las credenciales de administrador de empresa.  
9. Si tiene un dominio administrado, omita este paso.  

   En la página **Configuración de federación**, escriba las credenciales del administrador de AD FS y, a continuación, seleccione **Siguiente**.
10. En la página **Listo para configurar**, seleccione **Configurar**.
11. En la página **Configuración completada**, seleccione **Salir**.

Si experimenta problemas con la finalización de la unión a Azure AD híbrido para dispositivos Windows unidos a dominio, vea [Solución de problemas de dispositivos híbridos de Windows 10 y Windows Server 2016 unidos a Azure Active Directory](/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).

## <a name="configure-client-settings-to-direct-clients-to-register-with-azure-ad"></a>Configuración del cliente para dirigir a los clientes al registro con Azure AD

Use la configuración de cliente para configurar los clientes de Configuration Manager para que se registren automáticamente con Azure AD.  

1. Abra la **Consola de Configuration Manager** > **Administración** > **Información general** > **Configuración de cliente** y, luego, edite la **Configuración de cliente predeterminada**.  

2. Seleccione **Cloud Services**.  

3. En la página **Configuración predeterminada**, establezca **Registrar automáticamente los nuevos dispositivos de Windows 10 unidos a un dominio con Azure Active Directory** en = **Sí**.  

4. Haga clic en **Aceptar** para guardar esta configuración.  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>Configuración de la inscripción automática de dispositivos en Intune

A continuación se va a configurar la inscripción automática de dispositivos en Intune. Con la inscripción automática, los dispositivos administrados con Configuration Manager se inscriben automáticamente en Intune.

La inscripción automática también permite a los usuarios inscribir sus dispositivos Windows 10 en Intune. Inscriba dispositivos cuando un usuario agregue su cuenta profesional a su dispositivo personal, o cuando un dispositivo corporativo esté unido a Azure Active Directory.  

1. Inicie sesión en [Azure Portal](https://portal.azure.com/) y seleccione **Azure Active Directory** > **Movilidad (MDM y MAM)**  > **Microsoft Intune** .  

2. Configure el **ámbito de usuario de MDM**. Especifique una de las opciones siguientes para configurar qué dispositivos de los usuarios se administran mediante Microsoft Intune y acepte los valores predeterminados para la dirección URL.  

   - **Algunos**: seleccione los **Grupos** que pueden inscribir automáticamente sus dispositivos Windows 10  

   - **Todo**: todos los usuarios pueden inscribir automáticamente sus dispositivos Windows 10

   - **Ninguna**: deshabilite la inscripción automática de MDM

   > [!IMPORTANT]  
   > Si **ámbito de usuario de MAM** y la inscripción automática de MDM (el **ámbito de usuario de MDM**) están habilitados para un grupo, solo se habilitará MAM. Solo se agrega la administración de aplicaciones móviles (MAM) para los usuarios de ese grupo cuando conectan su dispositivo personal al área de trabajo. Los dispositivos no se inscriben automáticamente en MDM.  

3. Seleccione **Guardar** para completar la configuración de la inscripción automática.  

4. Vuelva a **Movilidad (MDM y MAM)** y, a continuación, seleccione **Inscripción a Microsoft Intune**.  

    > [!NOTE]
    > Es posible que algunos inquilinos no tengan estas opciones para configurar.<!-- SCCMDocs#1230 -->
    >
    > **Microsoft Intune** es la forma de configurar la aplicación MDM para Azure AD. **Inscripción de Microsoft Intune** es una aplicación concreta de Azure AD que se crea al aplicar directivas de autenticación multifactor para la inscripción de iOS y Android. Para obtener más información, vea [Autenticación multifactor para las inscripciones de dispositivos de Intune](/intune/enrollment/multi-factor-authentication).

5. Para el ámbito de usuario de MDM, seleccione **Todos** y, a continuación, **Guardar**.  

## <a name="enable-co-management-in-configuration-manager"></a>Habilitación de la administración conjunta en Configuration Manager

Con Azure AD híbrido configurado y las configuraciones cliente de Configuration Manager establecidas, está listo para accionar el interruptor y habilitar la administración conjunta de los dispositivos Windows 10.  

> [!TIP]
> - Cuando habilite la administración conjunta, asignará una recopilación como un *grupo piloto*. Se trata de un grupo que contiene un número pequeño de clientes para probar sus configuraciones de administración conjunta. Se recomienda crear una colección adecuada antes de iniciar el procedimiento. A continuación, puede seleccionar esa colección sin salir del procedimiento para ello.
> - A partir de la versión 1906 de Configuration Manager, es posible que necesite varias recopilaciones, porque puede asignar un *grupo piloto* distinto para cada carga de trabajo.

### <a name="enable-co-management-starting-in-version-1906"></a>Habilitación de la administración conjunta a partir de la versión 1906

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>Habilitación de la administración conjunta en la versión 1902 y versiones anteriores

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="next-steps"></a>Pasos siguientes

- Revise el estado de los dispositivos administrados conjuntamente con el [panel de administración conjunta](how-to-monitor.md).
- Empiece a recibir [valor inmediato](quickstarts.md#immediate-value) de la administración conjunta.
- Use el [acceso condicional](quickstart-conditional-access.md) y las reglas de cumplimiento de Intune para administrar el acceso de los usuarios a los recursos corporativos.