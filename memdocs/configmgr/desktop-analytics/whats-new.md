---
title: Novedades de Análisis de escritorio
titleSuffix: Configuration Manager
description: Resumen de las nuevas características de la última versión mensual del servicio en la nube Análisis de escritorio.
ms.date: 08/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: fa300181-86cb-4afe-8fbf-895a7572378d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: dd188b80375861cd08784d0574e737bfce7f2d92
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993153"
---
# <a name="whats-new-in-desktop-analytics"></a>Novedades de Análisis de escritorio

Conozca las novedades mensuales de Análisis de escritorio.

> [!TIP]
> El lanzamiento de cada actualización mensual puede tardar hasta tres días. Es posible que algunas características se implementen durante varias semanas y que no estén disponibles para todos los clientes la primera semana.

Para obtener una notificación cuando se actualice esta página, copie y pegue la siguiente dirección URL en su lector de fuentes RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+desktop+analytics+-+Configuration+Manager%22&locale=en-us`
<!-- a locale is required for the RSS search string -->

## <a name="august-2020"></a>Agosto de 2020

### <a name="apps-deployed-from-configuration-manager-are-important-by-default"></a>Las aplicaciones implementadas desde Configuration Manager son importantes de forma predeterminada.

<!-- 4859763 -->

La configuración de la **importancia** de una aplicación es esencial para que Análisis de escritorio determine los dispositivos que se van a incluir en las implementaciones piloto. Un administrador necesitaba configurar manualmente la importancia de todas las aplicaciones en Análisis de escritorio. Solo una vez que validase el piloto podía continuar con una implementación de producción.

Ahora, para cualquier aplicación que implemente con Configuration Manager, Análisis de escritorio lo configura automáticamente como importante de forma predeterminada. Este comportamiento le permite configurar las aplicaciones en el entorno con más rapidez para agilizar la implementación de producción.

Para más información, vea [Recursos: aplicaciones](about-assets.md#apps).

<!-- 6049643 -->

### <a name="improved-processing-of-diagnostic-data-during-snapshot-generation"></a>Procesamiento mejorado de datos de diagnóstico durante la generación de instantáneas

Microsoft ha mejorado el modo en que recopila y procesa los datos de diagnóstico de Windows de los dispositivos inscritos en Análisis de escritorio. Estas mejoras aumentan la confiabilidad de la generación diaria de instantáneas y preparan el entorno para las nuevas características en desarrollo. Como resultado de este trabajo, Microsoft ha deshabilitado temporalmente el recuento de **Dispositivos que han iniciado esta aplicación durante los últimos 30 días** en los planes de implementación. Para más información, vea [Recursos: aplicaciones](about-assets.md#usage).

## <a name="july-2020"></a>Julio de 2020

### <a name="windows-10-version-2004-now-available-in-desktop-analytics"></a>Windows 10, versión 2004, ahora disponible en Análisis de escritorio

<!-- 7370207 -->

En el portal de Análisis de escritorio, cuando supervise la seguridad y las actualizaciones de características, ahora verá Windows 10, versión 2004. Al crear un plan de implementación, puede seleccionar Windows 10, versión 2004, como la versión de destino.

### <a name="improved-support-for-viewing-the-portal-from-any-device"></a>Compatibilidad mejorada para ver el portal desde cualquier dispositivo

<!-- 6270240 -->

Ahora puede ver el portal de Análisis de escritorio en el centro de administración de Microsoft Endpoint Manager desde diversos tipos de dispositivos. Ahora cumple con las instrucciones de accesibilidad de contenido web (WCAG) 2.1 para una resolución de pantalla tan baja de hasta 320 x 256 píxeles. Por ejemplo, la imagen siguiente es del portal en un iPhone 8 de Apple:

:::image type="content" source="media/dashboard-iphone8.png" alt-text="Portal de Análisis de escritorio en un iPhone 8":::

### <a name="notifications-for-service-impacting-events"></a>Notificaciones de eventos que afectan al servicio

<!-- 4982509 -->

Ahora el portal de Análisis de escritorio puede mostrar banners de notificación. Estas notificaciones permiten a Microsoft comunicarle eventos e incidencias importantes. Por ejemplo, problemas conocidos con el servicio, la latencia de datos o nuevos requisitos previos. Para obtener más información, vea [Notificaciones del servicio](troubleshooting.md#service-notifications).

## <a name="june-2020"></a>Junio de 2020

### <a name="improvement-to-prerequisites"></a>Mejoras de los requisitos previos

Análisis de escritorio ya no requiere la implementación de un servicio de Microsoft 365 en su inquilino de Azure Active Directory (Azure AD). La aplicación de **administración del cliente de Office 365** en Azure AD ahora es **Análisis de escritorio** para permitir a Configuration Manager recuperar información y el estado del servicio.

## <a name="may-2020"></a>Mayo de 2020

### <a name="reduce-the-number-of-apps-for-review"></a>Reducir el número de aplicaciones para revisar

<!-- 5542186 -->

Para ayudar a consolidar y reducir el número de aplicaciones que se muestran en la página Activos del portal, ahora se combinan todas las versiones de las aplicaciones con el mismo nombre y el mismo editor. El recuento de aplicaciones en el icono **Aplicaciones de interés** refleja este valor. Por ejemplo, en lugar de mostrar cientos de instancias de Microsoft Edge, hay una sola instancia para todas las versiones. Puede tomar decisiones una vez para todas las versiones. Si necesita tomar decisiones sobre versiones específicas de una aplicación, este comportamiento es configurable.

Para más información, vea [Acerca de los recursos: aplicaciones](about-assets.md#apps).

## <a name="march-2020"></a>Marzo de 2020

### <a name="support-for-multiple-hierarchies"></a>Compatibilidad con varias jerarquías

<!-- 4814075, 6079184 -->

Ahora puede conectar varias jerarquías de Configuration Manager a un único inquilino de Azure Active Directory con un único identificador comercial para Análisis de escritorio. El portal clasifica los dispositivos de diferentes jerarquías y mejora las experiencias de los planes de implementación y los pilotos globales.

- Al configurar el proyecto piloto global, si incluye recopilaciones que contienen más del 20 % del total de dispositivos inscritos, el portal muestra una advertencia.
- Al crear un plan de implementación, si selecciona recopilaciones para varias jerarquías, el portal muestra una advertencia.

> [!NOTE]
> La compatibilidad con varias jerarquías requiere la versión 1910 o posterior de Configuration Manager.

Vea los siguientes artículos para más información:

- [Piloto global](deploy-pilot.md#bkmk_GlobalPilot)
- [Creación de planes de implementación](create-deployment-plans.md)

### <a name="identify-compatibility-safeguards"></a>Identificación de medidas de seguridad de compatibilidad

<!-- 5746559 -->

Los datos de compatibilidad de Windows clasifican algunas aplicaciones y controladores con una *medida de seguridad*, lo que puede hacer que la actualización a Windows 10 no se realice correctamente o se revierta. Análisis de escritorio ahora puede ayudarle a identificar estas medidas de seguridad de antemano para que pueda corregir el recurso antes de implementar la actualización. Para más información, consulte [Evaluación de compatibilidad: Medidas de seguridad](compat-assessment.md#safeguards).

## <a name="january-2020"></a>Enero de 2020

### <a name="additional-app-usage-detail"></a>Información adicional sobre el uso de la aplicación

<!-- 5533890 -->

Cuando se selecciona una aplicación para ver más información, el panel de detalles muestra ahora información de uso adicional. Puede usar estos datos para comprender el alcance de la instalación de una aplicación, así como para ver los dispositivos en los que los usuarios usan la aplicación con regularidad. Para obtener más información, vea [Acerca de los recursos: uso de la aplicación](about-assets.md#usage).

### <a name="provide-feedback-on-desktop-analytics"></a>Comentarios sobre Análisis de escritorio

<!-- 5451636 -->

Para compartir sus comentarios sobre Análisis de escritorio, seleccione el icono **Enviar una sonrisa** en la parte superior derecha del portal. Para obtener más información, vea [Compartir comentarios sobre el producto](get-support.md#bkmk_feedback).

## <a name="october-2019"></a>Octubre de 2019

### <a name="improvements-to-compatibility-recommendations"></a>Mejoras de las recomendaciones de compatibilidad

<!-- 3594545 -->

Análisis de escritorio proporciona ahora detalles adicionales cuando detecta que la actualización de Windows quitará de forma total o parcial una aplicación o un controlador. Para más información, consulte [Evaluación de compatibilidad](compat-assessment.md#asset-is-removed-during-upgrade).

### <a name="migrate-from-windows-analytics-to-existing-tenant"></a>Migración de Windows Analytics a un inquilino existente

<!-- 5202803 -->

Ahora puede migrar entradas de un área de trabajo de Windows Analytics existente después de incorporarlas a Análisis de escritorio.

## <a name="september-2019"></a>Septiembre de 2019

### <a name="migrate-inputs-from-windows-analytics"></a>Migración de entradas de Windows Analytics

<!-- 4252663 -->

Durante la incorporación, ahora puede migrar entradas de un área de trabajo de Windows Analytics existente.

### <a name="offboard-from-desktop-analytics"></a>Anulación de la incorporación de Análisis de escritorio

<!-- 4972396 -->

Si configuró Análisis de escritorio en el entorno, pero quiere dejar de usar el servicio, ahora puede cerrar la cuenta. Si cambia de opinión en 90 días, puede volver a activarla. Para más información, consulte [Cierre de la cuenta](account-close.md).

## <a name="august-2019"></a>Agosto de 2019

### <a name="reset-your-account"></a>Restablecimiento de la cuenta

<!-- 3733897 -->

Si configuró Análisis de escritorio en el entorno, pero quiere empezar de nuevo con la incorporación y la inscripción, ahora puede restablecerlo. Para más información sobre el proceso, consulte [Restablecimiento de la cuenta](account-reset.md).

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a>Decisión de actualización automática de las aplicaciones del sistema y de la tienda

<!-- 3587232 -->

Para ayudar a reducir el trabajo de anotar las aplicaciones destacadas, determinados tipos de aplicaciones se marcan automáticamente como *No importante*. La decisión de actualizar el plan de implementación de estas aplicaciones también se marca como *Preparado*. Las siguientes aplicaciones son compatibles y deben seguir funcionando después de actualizar Windows:

- Aplicaciones del sistema y componentes publicados por Microsoft

- Aplicaciones administradas y actualizadas desde Microsoft Store

Para más información, consulte [Decisión de actualización automática de las aplicaciones del sistema y de la tienda](about-assets.md#bkmk_plan-autoapp).

## <a name="whats-new-in-configuration-manager"></a>Novedades de Configuration Manager

Los documentos de Análisis de escritorio siempre hacen referencia a la funcionalidad de la versión más reciente de la rama actual de Configuration Manager. Para más información sobre los últimos cambios de Configuration Manager, consulte los siguientes artículos:

<!-- - [What's new in version 1910](../core/plan-design/changes/whats-new-in-version-1910.md#bkmk_da) -->

- [Novedades de la versión 1906](../core/plan-design/changes/whats-new-in-version-1906.md#bkmk_da)

## <a name="deprecated-features"></a>Características en desuso

Cuando Microsoft planea quitar una característica importante del servicio Análisis de escritorio, ese cambio se anunciará con antelación como una característica en desuso de Configuration Manager. Para más información, vea [Deprecated Features](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features) (Características en desuso).
