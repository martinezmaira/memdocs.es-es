---
title: Funcionalidades de Technical Preview 1512
titleSuffix: Configuration Manager
description: Conozca las características disponibles en Technical Preview de Configuration Manager, versión 1512.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e4d9e414-1346-4ed4-85d0-64d602b68731
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 03a6e7cd49bbb5a65a4364be398961c048d2a1b9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705683"
---
# <a name="capabilities-in-technical-preview-1512-for-configuration-manager"></a>Funciones de Technical Preview 1512 de Configuration Manager

*Se aplica a: Configuration Manager (rama Technical Preview)*

En este artículo se presentan las características disponibles en la versión 1512 de Technical Preview de Configuration Manager. Puede instalar esta versión para actualizar y agregar nuevas capacidades al sitio de Technical Preview de Configuration Manager. Antes de instalar esta versión de Technical Preview, lea el tema de introducción [Technical Preview de Configuration Manager](technical-preview.md) para familiarizarse con los requisitos y las limitaciones generales de una Technical Preview y para saber cómo actualizar entre versiones y cómo proporcionar comentarios sobre las características de una Technical Preview.  

 Estas son las nuevas características que puede probar con esta versión.  

##  <a name="device-health-attestation"></a><a name="bkmk_devicehealth"></a> Atestación de estado del dispositivo  
 A partir de Technical Preview 1512, los administradores pueden ver el estado de la atestación de estado de los dispositivos de Windows 10 en la consola de Configuration Manager.  Esta funcionalidad está disponible para Configuration Manager y Configuration Manager con Microsoft Intune. La atestación de estado del dispositivo permite al administrador garantizar que los equipos cliente tienen configuraciones BIOS, TPM y de arranque de software de confianza. Para admitir la atestación de estado del dispositivo, los dispositivos cliente deben ejecutar Win10 con TPM 2 habilitado. La atestación de estado del dispositivo muestra el número de dispositivos habilitados para cada una de las siguientes acciones:  

-   Antimalware de inicio temprano  

-   BitLocker  

-   Arranque seguro  

-   Integridad de código  

La consola también muestra las principales opciones de configuración de atestación de estado que faltan con el número de dispositivos.  

Para obtener una vista previa de la atestación de estado del dispositivo, en la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, haga clic en el nodo **Seguridad** y luego en **Atestación de estado**.  

##  <a name="in-console-monitoring-for-terms-and-conditions"></a><a name="bkmk_viewterms"></a> Supervisión en la consola para los términos y condiciones  
A partir de Technical Preview 1512, al integrar Configuration Manager con Microsoft Intune, puede usar la consola de Configuration Manager para ver qué usuarios han aceptado los términos y condiciones configurados por el departamento de TI, así como los que no lo han hecho.  

**Para ver información de resumen:**  

-   En la consola de Configuration Manager, vaya a **Supervisión** > **Información general** > **Implementaciones** y seleccione la implementación de términos y condiciones que quiere ver.  

**Para ver información detallada:**  

1.  En la consola de Configuration Manager, vaya a **Activos y compatibilidad** > **Información general** > **Configuración de cumplimiento** > **Términos y condiciones** y luego seleccione los términos y condiciones que quiere ver.  

2.  En la parte inferior de la consola, seleccione la pestaña **Implementaciones**, seleccione la implementación y luego haga clic en **Ver estado**.  

##  <a name="improvements-to-endpoint-protection-policy-settings"></a><a name="bkmk_EPpolicy"></a> Mejoras para la configuración de directivas de Endpoint Protection  
En 1512 Technical Preview, hemos agregado la siguiente nueva configuración de directiva antimalware de Endpoint Protection:  

-   Protección en tiempo real: **Bloqueo de aplicaciones potencialmente no deseadas en la descarga y antes de la instalación**  

    -   Aplicaciones no deseadas potenciales (PUA) es una clasificación de amenaza que se basa en la reputación y la identificación de investigación. Normalmente, se trata de aplicaciones no deseadas que instalan varios programas o sus aplicaciones empaquetadas.  

    -   La configuración de directiva de protección está habilitada de forma predeterminada (establecida en "Sí"). Cuando se habilita, esta configuración bloqueará las PUA en el momento de la descarga y la instalación. Sin embargo, puede excluir determinados archivos o carpetas para satisfacer las necesidades específicas de su entorno.  

-   Configuración de exploración: **Examinar unidades de red asignadas al ejecutar un examen completo**  

    -   Esta configuración proporciona una mayor granularidad para que el administrador permita análisis de archivos de red a petición sin el riesgo de analizar siempre unidades de red asignadas durante un examen completo programado.  

    -   La opción **Examinar archivos de red** primero debe habilitarse ("sí") para que esté disponible.  

    -   De forma predeterminada, esta configuración está establecida como "no", lo que significa que un examen completo no tendrá acceso a las unidades de red asignadas.  

-   Configuración de envío automático de archivo de ejemplo:  

     El motor de antimalware puede solicitar ejemplos de archivo que se enviarán a Microsoft para un análisis más profundo. De forma predeterminada, siempre se le preguntará antes de enviar dichos ejemplos. Los administradores pueden administrar ahora las siguientes opciones para configurar este comportamiento:  

    -   Avanzado: **Habilitar el envío automático de archivos de ejemplo para ayudar a Microsoft a averiguar si ciertos elementos encontrados son malintencionados**:  cambie esta opción a "Sí" para habilitar el envío automático de archivos de ejemplo. De forma predeterminada, esta configuración está establecida como "No", lo que significa que el envío automático de archivos de ejemplo está deshabilitado y se le preguntará a los usuarios antes de enviar ejemplos.   (Esta configuración se introdujo por primera vez en System Center 2012 R2 Configuration Manager SP1)  

    -   Avanzado: **Permitir a los usuarios modificar la configuración de envío automático de archivos de ejemplo**: Esta configuración determina si un usuario con derechos administrativos locales en un dispositivo puede cambiar la configuración de envío automático de archivos de ejemplo en la interfaz del cliente. De forma predeterminada, esta opción está establecida en "No", lo que significa que la configuración solo se puede cambiar en la consola de Configuration Manager y los administradores locales de un dispositivo no pueden cambiarla.  

         Por ejemplo, a continuación se muestra la configuración de Windows Defender en Windows 10 establecida por el administrador como habilitada, y el usuario no tiene permiso para modificarla:  

         ![TechRef&#95;WinDefender](../../core/get-started/media/TechRef_WinDefender.png "TechRef_WinDefender")  

    Además, la configuración **Excluir archivos y carpetas** existente en la sección "Configuración de exclusión" de la directiva antimalware de Endpoint Protection se ha mejorado para permitir exclusiones del dispositivo. Por ejemplo, ahora puede especificar lo siguiente como una exclusión: **\device\mvfs** (para el sistema de archivos de varias versiones). La directiva no valida la ruta de acceso del dispositivo; se proporciona la directiva de Endpoint Protection al motor de antimalware en el cliente que debe ser capaz de interpretar la cadena del dispositivo.  

**Requisitos previos para usar las directivas de Endpoint Protection:**  

Antes de usar las directivas de Endpoint Protection, debe instalar y administrar el cliente de Endpoint Protection mediante la configuración de cliente de Endpoint Protection. Esto se hace con el cliente de System Center Endpoint Protection para Windows 7, Windows 8, Windows 8.1 o lo administra Windows Defender para Windows 10. Vea [Endpoint Protection](../../protect/deploy-use/endpoint-protection.md).  
