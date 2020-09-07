---
title: Aplicaciones del Portal de empresa
titleSuffix: Configuration Manager
description: Proporcione una experiencia de usuario uniforme para que los dispositivos administrados conjuntamente usen la aplicación Portal de empresa.
ms.date: 09/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: how-to
ms.assetid: 26456bb7-f46b-4d8d-bb0b-e3fd9a52fe14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cd49546e49d6964cfe37b0b13e1abe9175f4aa0e
ms.sourcegitcommit: 7b656712cc9340d18211c7754cb99bcaae91b0ca
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/03/2020
ms.locfileid: "89432564"
---
# <a name="use-the-company-portal-app-on-co-managed-devices"></a>Uso de la aplicación Portal de empresa en dispositivos administrados conjuntamente

*Se aplica a: Configuration Manager (rama actual)*

<!--CMADO-3601237,INADO-4297660-->

A partir de la versión 2006, el Portal de empresa es ahora la experiencia del portal de aplicaciones multiplataforma para Microsoft Endpoint Manager. Mediante la configuración de los dispositivos administrados conjuntamente para usar también el Portal de empresa, puede proporcionar una experiencia de usuario coherente en todos los dispositivos.

El Portal de empresa admite las siguientes acciones:

- Iniciar la aplicación Portal de empresa en los dispositivos administrados conjuntamente e iniciar sesión con el inicio de sesión único (SSO) de Azure Active Directory (Azure AD).
- Ver las aplicaciones de Configuration Manager disponibles e instaladas en el Portal de empresa junto con las aplicaciones de Intune.
- Instalar las aplicaciones de Configuration Manager disponibles desde el Portal de empresa y recibir la información de estado de la instalación.

:::image type="content" source="media/3601237-company-portal.png" alt-text="Portal de empresa con aplicaciones de Configuration Manager" lightbox="media/3601237-company-portal.png":::

El comportamiento del Portal de empresa depende de la configuración de la carga de trabajo de administración conjunta:

| Carga de trabajo | Setting | Comportamiento |
|----------|---------|----------|
| Aplicaciones cliente | **Configuration Manager** | Solo puede ver aplicaciones cliente de Configuration Manager. |
| Aplicaciones cliente | **Intune piloto** o **Intune** | Puede ver las aplicaciones cliente de Configuration Manager y de Intune. |
| Aplicaciones de Office para hacer clic y ejecutar | **Configuration Manager** | Solo puede ver las aplicaciones de Office para hacer clic y ejecutar de Configuration Manager. |
| Aplicaciones de Office para hacer clic y ejecutar | **Intune piloto** o **Intune** | Solo puede ver las aplicaciones de Office para hacer clic y ejecutar de Intune. |

Para más información, consulte los siguientes artículos.

- [Diagrama para cargas de trabajo de aplicaciones](workloads.md#diagram-for-app-workloads)

- [Cambio de las cargas de trabajo de Configuration Manager a Intune](how-to-switch-workloads.md)

## <a name="prerequisites"></a>Requisitos previos

- Rama actual de Configuration Manager, versión 2006 o posterior<sup>([Ver las Preguntas más frecuentes](#bkmk_ver-prereq))</sup>

- Aplicación Portal de empresa, versión 11.0.8980.0 o posterior

- Windows 10, versión 1803 o posterior:

  - Inscrito en la [administración conjunta](how-to-enable.md)

  - Acceso a [puntos de conexión de Internet para Intune](../../intune/fundamentals/intune-endpoints.md)

- Es necesario que las cuentas de usuario que inician sesión en estos dispositivos tengan las siguientes configuraciones:

  - Una identidad de Azure AD

  - Una licencia de Intune asignada.

## <a name="configure-and-deploy"></a>Configuración e implementación

### <a name="configuration-manager-client-settings"></a>Configuración de cliente de Configuration Manager

Para asegurarse de que los usuarios solo reciben notificaciones del Portal de empresa, ajuste la configuración de cliente de Configuration Manager. En la configuración del grupo de dispositivos **Centro de software**, cambie **Seleccione el portal de usuarios** a **Portal de empresa**.

Para más información sobre la configuración de cliente, vea los siguientes artículos:

- [Cómo establecer la configuración del cliente](../core/clients/deploy/configure-client-settings.md)
- [Acerca de la configuración de cliente](../core/clients/deploy/about-client-settings.md#software-center)

### <a name="deploy-the-company-portal-app"></a>Implementación de la aplicación Portal de empresa

- Los usuarios pueden instalar manualmente la aplicación Portal de empresa desde [Microsoft Store](https://www.microsoft.com/p/company-portal/9wzdncrfj3pz?activetab=pivot:overviewtab).

- Para requerir la aplicación en los dispositivos administrados conjuntamente, el proceso de implementación depende del estado de la carga de trabajo de administración conjunta [Aplicaciones cliente](workloads.md#client-apps):

  - Si la carga de trabajo de las aplicaciones cliente está con Configuration Manager, [cree e implemente una aplicación con Configuration Manager](../apps/get-started/create-and-deploy-an-application.md). Descargue la aplicación Portal de empresa sin conexión desde [Microsoft Store para Empresas](https://www.microsoft.com/business-store).

  - Si la carga de trabajo de aplicaciones cliente está con Intune, puede implementarla a través de Configuration Manager o [agregar la aplicación Portal de empresa de Windows 10 mediante Microsoft Intune](../../intune/apps/store-apps-company-portal-app.md).

Para obtener más información sobre la personalización de marca del Portal de empresa para su organización, consulte [Personalización de las aplicaciones del Portal de empresa de Intune](../../intune/apps/company-portal-app.md).

## <a name="use-the-company-portal"></a>Uso del Portal de empresa

1. Inicie el Portal de empresa desde el menú Inicio. El usuario con la sesión abierta inicia sesión automáticamente en el Portal de empresa de acuerdo con su identidad de Azure AD.

1. Seleccione la página **Aplicaciones**. Debería ver las aplicaciones de Configuration Manager en la lista.

1. Seleccione una de las aplicaciones implementadas desde Configuration Manager.

    - En la pestaña **Información general** se muestran los detalles de la aplicación, como el tamaño, la versión y la fecha de publicación.

    - Para ver si Configuration Manager es el servicio de administración de esta aplicación, cambie a la pestaña **Información adicional**.

    - Para instalar la aplicación, seleccione **Instalar**. En el Portal de empresa se muestra el estado de la instalación, y verá una notificación cuando se complete.

    - Si la aplicación ya está instalada, seleccione **Desinstalar** para quitarla.

    - Seleccione los puntos suspensivos (`...`) para acciones adicionales, como **Reparar** y **Compartir**.

        :::image type="content" source="media/3601237-company-portal-app-details.png" alt-text="Aplicación de Configuration Manager con detalles en el Portal de empresa" lightbox="media/3601237-company-portal-app-details.png":::

    - Después de instalar una aplicación web de Configuration Manager, seleccione el menú de puntos suspensivos y, a continuación, seleccione **Abrir en el explorador** para iniciar la aplicación web.

    - Si no se puede instalar una aplicación de Configuration Manager y se genera un código de error conocido, seleccione el vínculo del estado de error para buscar ese código.

Si cambia la configuración de cliente para el Portal de empresa, cuando un usuario selecciona una notificación de Configuration Manager se inicia el Portal de empresa. Si la notificación es para un escenario no compatible con el Portal de empresa, la selección de la notificación inicia el Centro de software.

Para ayudar a solucionar problemas relacionados con la instalación de aplicaciones de Configuration Manager, vaya a la sección **Ayuda y soporte técnico** del Portal de empresa. Si usa la opción **Obtener ayuda**, puede enviar archivos de registro de Configuration Manager como parte de la solicitud.

## <a name="frequently-asked-questions-faq"></a>Preguntas más frecuentes

### <a name="im-using-configuration-manager-version-2002-why-is-the-new-company-portal-showing-configuration-manager-apps"></a><a name="bkmk_ver-prereq"></a> Uso la versión 2002 de Configuration Manager, ¿por qué el Portal de empresa nuevo muestra las aplicaciones de Configuration Manager?

El Portal de empresa, versión 11.0.8980.0 o posterior, muestra las aplicaciones implementadas por Configuration Manager para todos los clientes administrados conjuntamente que la usan. El requisito previo es la versión 2006 de Configuration Manager, porque agrega la configuración de cliente para controlar las notificaciones. Si instala el Portal de empresa en un dispositivo administrado conjuntamente de una versión anterior o no ajusta la configuración de cliente, los usuarios verán las notificaciones de ambos portales. Esta experiencia puede resultar confusa para los usuarios.

### <a name="does-company-portal-support-applications-deployed-as-software-updates-from-configuration-manager"></a>¿El Portal de empresa admite las aplicaciones implementadas como actualizaciones de software de Configuration Manager?

Sí. Si implementa una aplicación mediante la característica de actualizaciones de software, el cliente la trata como si la experiencia del usuario fuera el Portal de empresa o el Centro de software.

### <a name="can-users-repair-uninstall-and-update-configuration-manager-apps-in-company-portal"></a>¿Los usuarios pueden reparar, desinstalar y actualizar aplicaciones de Configuration Manager en el Portal de empresa?

Sí. Si configura la aplicación de Configuration Manager para que admita estas acciones adicionales, el Portal de empresa admite la reparación, la desinstalación y la actualización.

## <a name="known-issues"></a>Problemas conocidos

Las siguientes características del Centro de software no están disponibles actualmente en el Portal de empresa:

- Algunos datos de la aplicación, por ejemplo, si se requiere un reinicio o el tiempo estimado para la instalación.

- [Grupos de aplicaciones](../apps/deploy-use/create-app-groups.md)

Otros problemas conocidos:

- Si implementa la misma aplicación desde Configuration Manager e Intune, esta aparece dos veces en el Portal de empresa.

- Al buscar el Portal de empresa, las aplicaciones de Intune siempre se muestran antes de las aplicaciones de Configuration Manager.

## <a name="next-steps"></a>Pasos siguientes

[Cambio de las cargas de trabajo de Configuration Manager a Intune](how-to-switch-workloads.md)

[Personalización de las aplicaciones del Portal de empresa de Intune](../../intune/apps/company-portal-app.md)
