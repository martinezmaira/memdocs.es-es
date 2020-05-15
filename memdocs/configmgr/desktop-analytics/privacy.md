---
title: Privacidad de datos de Análisis de escritorio
titleSuffix: Configuration Manager
description: Análisis de escritorio mantiene un firme compromiso con la privacidad de los datos del cliente
ms.date: 12/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: dd970dc1517a6fcc197b2bf39a141871b4999a02
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268426"
---
# <a name="desktop-analytics-data-privacy"></a>Privacidad de datos de Análisis de escritorio

Análisis del escritorio mantiene un firme compromiso con la privacidad de los datos del cliente centrándose en estos principios:

- **Transparencia**: documentamos por completo los eventos de diagnóstico de Windows. Revíselos con los equipos de cumplimiento y seguridad de su empresa. El visor de datos de diagnóstico de Windows le permite ver los datos de diagnóstico enviados desde un dispositivo determinado. para más información, consulte [Introducción al Visor de datos de diagnóstico](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview).  

- **Control:** puede controlar el nivel de los datos de diagnóstico que se van a compartir con Microsoft. Windows 10, versión 1709, agrega una nueva directiva para limitar los datos de diagnóstico mejorados al mínimo requerido por Análisis de escritorio.  

- **Seguridad:** Microsoft protege los datos con seguridad y cifrado seguros.  

- **Confianza:** Análisis de escritorio respeta la [declaración de privacidad](https://privacy.microsoft.com/privacystatement) y los [términos de servicio en línea](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46) de Microsoft.  

Para obtener más información, consulte [Servicios de Windows donde Microsoft es el encargado de tratamiento de los datos personales según la GDPR](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance#windows-services-where-microsoft-is-the-processor-under-the-gdpr).<!-- 5353168 -->

## <a name="data-flow"></a>Flujo de datos

En la ilustración siguiente se muestra cómo fluyen los datos de diagnóstico desde dispositivos individuales a través del servicio de datos de diagnóstico, el almacenamiento transitorio, al área de trabajo de Log Analytics:

![Diagrama que ilustra el flujo de datos de diagnóstico de dispositivos](media/da-data-flow.png)

1. Inicia sesión en Azure Portal e incorpora Análisis de escritorio. Crea la aplicación Azure AD para conectarse con Configuration Manager. Al configurar Análisis de escritorio, crea un área de trabajo de Log Analytics de Azure en la ubicación de su elección.  

2. Conecta Configuration Manager e inscribe dispositivos.  

    1. Configura el servicio en la nube de Análisis de escritorio en Configuration Manager con los detalles de la aplicación Azure AD.  

    2. En menos de 15 minutos, Configuration Manager sincroniza los datos siguientes con Análisis de escritorio mediante el identificador de inquilino. Este proceso se repite cada hora.

      - Información sobre las recopilaciones de dispositivos necesarias para [crear planes de implementación](create-deployment-plans.md). Esta información incluye el identificador de la recopilación, el de la jerarquía, el nombre de la recopilación y el recuento de dispositivos. 
      - Información necesaria para [inscribir dispositivos](enroll-devices.md). Esta información incluye el identificador de la recopilación, el identificador único de SMS, la versión de compilación del sistema operativo, el nombre del dispositivo y el número de serie.
      - Información del panel de [supervisión del estado de conexión](monitor-connection-health.md). Esta información incluye el recuento de dispositivos por estado de mantenimiento y las propiedades de dispositivo.
      - Información sobre los planes de implementación, que incluye el identificador de la recopilación y el de la implementación, el tipo de implementación piloto o de producción, y el recuento de dispositivos por decisión de actualización.

    3. Configuration Manager establece el identificador comercial, el nivel de datos de diagnóstico y otras opciones de configuración de los dispositivos de la recopilación de destino. Esta configuración especifica los dispositivos que aparecen en el área de trabajo de Análisis de escritorio.  

    4. Las actualizaciones de compatibilidad se implementan en todos los dispositivos de destino.  

3. Los dispositivos envían datos de diagnóstico al servicio de administración de datos de diagnóstico de Microsoft para Windows. Este servicio OMS está hospedado en Estados Unidos.  

4. Cada día, Microsoft genera una instantánea de la información centrada en TI. Esta instantánea combina los datos de diagnóstico de Windows con la entrada de dispositivos inscritos. Este proceso se produce en el almacenamiento transitorio, que solo se usa en Análisis de escritorio. El almacenamiento transitorio se hospeda en centros de datos de Microsoft en Estados Unidos. Todos los datos se envían a través de un canal cifrado SSL (HTTPS). Las instantáneas se segregan por identificador comercial.  

5. Después, las instantáneas se copian en el área de trabajo de Azure Log Analytics. Esta transferencia de datos se realiza sobre HTTPS a través del protocolo de ingesta de webhook, que es una característica de Log Analytics. Análisis de escritorio no tiene permisos de lectura o escritura en el almacenamiento de Log Analytics. Análisis de escritorio llama a la API de webhook con un URI de firma de acceso compartido (SAS). Después, Log Analytics obtiene los datos de las tablas de almacenamiento a través de HTTPS.

6. Análisis de escritorio almacena la entrada en el almacenamiento de Log Analytics. Estas configuraciones incluyen planes de implementación y decisiones de recursos en materia de actualización e importancia.  

## <a name="other-resources"></a>Otros recursos

Para ver las preguntas más frecuentes relacionadas con la privacidad de Análisis de escritorio, consulte las [preguntas más frecuentes sobre privacidad](faq.md#privacy).

Para obtener más información sobre aspectos de privacidad, vea los artículos siguientes:

- [Windows 10 y GDPR: información para administradores de TI y toma de decisiones](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configurar los datos de diagnóstico de Windows en la organización](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

- [Campos y eventos de datos de diagnóstico del evaluador de Windows 7, Windows 8 y Windows 8.1](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields)  

- [Campos y eventos de diagnóstico de Windows en el nivel básico de Windows 10, versión 1809](https://docs.microsoft.com/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)  

- [Campos y eventos de datos de diagnóstico mejorados de Windows 10, versión 1709, usados por Windows Analytics](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  

- [Introducción al Visor de datos de diagnóstico](https://docs.microsoft.com/windows/privacy/diagnostic-data-viewer-overview)  

- [Términos de licencia y documentación](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  

- [Seguridad de datos de Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/data-security)

- [Seguridad y privacidad en centros de datos de Microsoft Azure](https://azure.microsoft.com/global-infrastructure/)  

- [Confíe en su nube](https://azure.microsoft.com/overview/trusted-cloud/)  

- [Centro de confianza](https://www.microsoft.com/trustcenter)  

- [Escudo de la privacidad](https://www.privacyshield.gov/)  

De forma independiente a Análisis de escritorio, Configuration Manager envía a Microsoft datos de diagnóstico y uso. Microsoft usa estos datos para mejorar la experiencia de instalación, la calidad y la seguridad de las versiones futuras de Configuration Manager. Para obtener más información, vea [Diagnósticos y datos de uso para Configuration Manager](../core/plan-design/diagnostics/diagnostics-and-usage-data.md).
