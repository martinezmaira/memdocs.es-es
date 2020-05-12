---
title: Preguntas más frecuentes sobre Análisis de escritorio
titleSuffix: Configuration Manager
description: Las preguntas más frecuentes sobre Análisis de escritorio.
ms.date: 02/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 29f063da47dc26789493b2a83ad8e0cfa6885270
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693302"
---
# <a name="desktop-analytics-faq"></a>P+F sobre Análisis de escritorio

## <a name="prerequisites"></a>Requisitos previos

### <a name="can-i-use-cloud-enabled-analytics-with-intune-managed-devices"></a><a name="bkmk_intune"></a> ¿Se pueden usar análisis habilitados para la nube con dispositivos administrados por Intune?

De momento, no, pero puede leer el aviso de Microsoft Ignite 2019 sobre la [administración de dispositivos basados en conclusiones](https://myignite.techcommunity.microsoft.com/sessions/81690?source=sessions). Esta solución planeada es la sucesora de Estado del dispositivo y Upgrade Readiness.

La gran mayoría de los clientes que pueden beneficiarse del flujo de trabajo de Análisis de escritorio usan Configuration Manager para implementar Windows. Sabemos que a los clientes de Intune les encantan las ideas adicionales de los datos de análisis, y estamos trabajando sobre formas de compartir también con ellos estas ideas.

### <a name="its-been-over-72-hours-and-the-portal-is-still-processing-data-what-next"></a>Han transcurrido más de 72 horas y el portal sigue procesando datos, ¿qué viene ahora?

La primera vez que se configura Análisis de escritorio, puede que los informes de Configuration Manager y el portal de Análisis de escritorio no muestren los datos completos de inmediato. El servicio puede tardar entre 2 y 3 días en procesar los datos. Si han transcurrido más de 72 horas y el portal todavía sigue procesando datos, siga estos pasos:

- Para confirmar que los dispositivos activos están configurados correctamente, use el panel [Estado de conexión](monitor-connection-health.md). Este panel no se actualiza en tiempo real.
- Asegúrese de que los dispositivos envían datos de diagnóstico al servicio Análisis de escritorio. Para más información, consulte [Habilitación del uso compartido de datos](enable-data-sharing.md).
- Aprovisione [aplicaciones de Azure AD](troubleshooting.md#bkmk_AzureADApps) en su instancia de Azure AD.
- Compruebe los dispositivos que ha asociado a su organización en los últimos siete días. En el [portal de Análisis de escritorio](https://aka.ms/desktopanalytics), vaya al panel **Servicios conectados**. Seleccione **Inscribir dispositivos** y **Ver datos recientes**.

  > [!IMPORTANT]
  > La opción de Análisis de escritorio para **Ver datos recientes** está en desuso. Esta acción se quitará en una versión futura del servicio de Análisis de escritorio. Para más información, vea [Deprecated Features](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md) (Características en desuso).<!--7080949-->  

Si los dispositivos están configurados correctamente y aún no ve los datos en el área de trabajo, [póngase en contacto con el servicio de soporte técnico de Microsoft](https://support.microsoft.com/hub/4343728/support-for-business).

## <a name="connect-configuration-manager"></a>Conexión de Configuration Manager

### <a name="can-i-change-the-target-or-additional-collections"></a>¿Se pueden cambiar las recopilaciones de destino o adicionales?

Sí, use el procedimiento siguiente:

- En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Cloud Services** y haga clic en el nodo **Servicios de Azure**. Abra las propiedades de la entrada asociada a su servicio Análisis de escritorio.

- En la pestaña **Conexión con Análisis de escritorio**, cambie el valor **Recopilación de destino** o administre recopilaciones adicionales.

> [!IMPORTANT]  
> Configuration Manager usa una directiva de configuración para configurar los dispositivos de la recopilación de destino. Esta directiva incluye la configuración de datos de diagnóstico para permitir que los dispositivos envíen datos a Microsoft. El cambio de la recopilación de destino no deshace la directiva de configuración en los dispositivos que ya no están en dicha recopilación. Si no quiere que los dispositivos sigan enviando datos de diagnóstico, [reconfigure los dispositivos](account-close.md#reconfigure-clients).

## <a name="windows-upgrade"></a>Actualización de Windows

### <a name="can-i-upgrade-windows-and-change-architecture"></a>¿Se puede actualizar Windows y cambiar la arquitectura?

Análisis de escritorio está diseñado para ofrecer el mejor respaldo a las actualizaciones en contexto. Las actualizaciones en contexto no admiten migraciones de arquitecturas de 32 a 64 bits. Si necesita migrar equipos en este escenario, use el escenario de actualización. Aunque la información de Análisis de escritorio sigue siendo valiosa en este escenario, se pueden omitir las instrucciones específicas de la actualización.

Para obtener más información, consulte [Actualizar un equipo existente con una nueva versión de Windows](../osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md).

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>¿Se puede cambiar de BIOS a UEFI al actualizar Windows?

Sí. Para más información, consulte [Conversión de BIOS a UEFI durante una actualización local](../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#convert-from-bios-to-uefi-during-an-in-place-upgrade).

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>¿Se puede usar Análisis de escritorio con Windows 10 LTSC?

Análisis de escritorio no admite los dispositivos de canal de mantenimiento a largo plazo (LTSC) de Windows 10. Para más información, consulte [Administración de Windows como servicio](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).

### <a name="can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal"></a>¿Se puede reducir la cantidad de tiempo que tardan los datos en actualizarse en el portal de Análisis de escritorio?

Hay dos tipos de datos en el portal de Análisis de escritorio: datos de administrador y datos de diagnóstico. Para actualizar los datos de administrador a petición, abra el control flotante de moneda de datos y seleccione **Aplicar cambios**. Esta acción desencadena inmediatamente una actualización única de los cambios de administrador pendientes en las áreas de trabajo. Los cambios se propagan y están disponibles con carácter general en un período de entre 15 y 60 minutos. El tiempo depende del tamaño del área de trabajo y del ámbito de los cambios pendientes. Puede solicitar una actualización de datos a petición hasta seis veces en un período de 24 horas.

Todos los datos se actualizan automáticamente una vez al día, aunque no solicite una actualización de datos a petición. No hay ninguna manera de desencadenar una actualización a petición de datos de diagnóstico. Para más información sobre los distintos tipos de datos de Análisis de escritorio, consulte [Latencia de datos](troubleshooting.md#data-latency).

## <a name="privacy"></a>Privacidad

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>¿Se puede usar Análisis de escritorio sin una conexión de cliente directa al servicio Administración de datos de Microsoft?

No, todo el servicio se basa en los datos de diagnóstico de Windows, lo que requiere que los dispositivos tengan esta conectividad directa.

### <a name="can-i-choose-the-data-center-location"></a>¿Se puede elegir la ubicación del centro de datos?

En Azure Log Analytics: Sí, al configurar Análisis de escritorio y crear el área de trabajo de Log Analytics.

En el servicio Administración de datos de Microsoft y Azure Storage Analytics: No, estos dos servicios se hospedan en Estados Unidos.

### <a name="where-is-my-organizations-data-stored"></a>¿Dónde se almacenan los datos de mi organización?

Los datos de diagnóstico de Windows de los equipos se cifran, se envían a centros de datos seguros administrados por Microsoft ubicados en Estados Unidos y allí se procesan. Microsoft proporciona el análisis de los datos relacionados con Análisis de escritorio a través de la solución Desktop Analytics de Azure Portal. Análisis de escritorio es compatible con la mayoría de las regiones en las que [Log Analytics está disponible](https://azure.microsoft.com/global-infrastructure/services/?products=monitor&regions=all). Si selecciona una región de Azure internacional, los datos de diagnóstico se seguirán enviando y procesando en los centros de datos seguros de Microsoft de Estados Unidos.

## <a name="existing-windows-analytics-customers"></a>Clientes existentes de Windows Analytics

> [!Important]  
> El servicio Windows Analytics se retiró el 31 de enero de 2020.
>
> Para más información, consulte [KB 4521815: Windows Analytics se retirará el 31 de enero de 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

### <a name="can-i-use-update-compliance-together-with-desktop-analytics"></a>¿Se puede usar Update Compliance junto con Análisis de escritorio?

Sí. Si actualmente usa [Update Compliance](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started) en Azure Portal, puede seguir haciéndolo ahora y después de enero de 2020.

Para más información, consulte [KB 4521815: Windows Analytics se retirará el 31 de enero de 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

### <a name="are-there-any-windows-analytics-features-that-arent-available-in-desktop-analytics"></a>¿Hay alguna característica de Windows Analytics que no estén disponibles en Análisis de escritorio?

<!-- 3616924 -->
Sí, las siguientes características de Windows Analytics se han retirado o todavía no están disponibles en Análisis de escritorio:

#### <a name="general"></a>General

- Compatibilidad con escenarios que no requieren Configuration Manager. Por ejemplo, [compatibilidad con Intune](#bkmk_intune).
- Requisitos previos de licencias de cualquier licencia de Windows válida frente a E3, E5
- Compatibilidad con varias áreas de trabajo por inquilino de Azure AD
- Capacidad de ejecutar consultas personalizadas y exportar datos de soluciones sin procesar
- Documentación del modelo de datos para informes personalizados

#### <a name="upgrade-readiness"></a>Upgrade Readiness

- Datos de detección de sitios de Internet Explorer
- Información del complemento de Office (ahora [disponible en Configuration Manager](#bkmk_office))
- Información sobre el concentrador de comentarios

#### <a name="update-compliance"></a>Update Compliance

- Compatibilidad con Windows Update para empresas
- Información de optimización de distribución
- Compatibilidad con el canal de mantenimiento a largo plazo (LTSC) de Windows 10
- Informes de Windows Insider
- Estado de Windows Defender

> [!Note]
> Todas las características de Update Compliance existentes, incluidas las que no están disponibles en Análisis de escritorio, siguen estando disponibles en la solución [Update Compliance](/windows/deployment/update/update-compliance-get-started) de Azure Portal.

#### <a name="device-health"></a>Estado del dispositivo

- Estado del controlador
- Estado de la aplicación (fuera de un plan de implementación)
- Dispositivos que se bloquean con frecuencia o bloqueos inducidos por el controlador
- Estado de inicio de sesión de Windows
- Windows Information Protection
- Compatibilidad con Windows Server

## <a name="other"></a>Otros

### <a name="can-i-use-desktop-analytics-for-my-office-365-proplus-upgrades"></a><a name="bkmk_office"></a> ¿Se puede usar Análisis de escritorio para las actualizaciones de Office 365 ProPlus?

No, Análisis de escritorio se centra en Windows. Microsoft desarrolló este servicio en estrecha colaboración con muchos clientes. Los comentarios de los clientes indican que Análisis de escritorio mejora su capacidad para administrar las implementaciones de Windows de forma segura. También nos dicen que quieren que la [preparación para Office 365 ProPlus](../sum/deploy-use/office-365-dashboard.md#bkmk_o365_readiness) se integre de manera más estrecha con las herramientas de administración de Office en Configuration Manager e Intune. Microsoft continúa invirtiendo en esas áreas, a la vez que se centra en escenarios de Windows en Análisis del escritorio.

### <a name="how-can-i-provide-feedback-about-desktop-analytics"></a>¿Cómo se pueden proporcionar comentarios sobre Análisis de escritorio?

Para compartir sus comentarios sobre Análisis de escritorio, seleccione el icono **Enviar una sonrisa** en la parte superior del portal. Incluya una captura de pantalla con su envío para ayudar a Microsoft a comprender mejor sus comentarios. También puede enviar sugerencias de productos y votar otras ideas en [UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas?category_id=366805).

> [!Note]
> No comparta nunca información privada en Enviar una sonrisa o UserVoice, por ejemplo, el identificador de inquilino o el identificador comercial. Microsoft no proporciona soporte técnico mediante los canales Enviar una sonrisa o UserVoice. Para obtener ayuda con el área de trabajo de Análisis de escritorio, seleccione el vínculo **Ayuda y soporte técnico** en el menú de navegación para abrir una incidencia de soporte técnico.
