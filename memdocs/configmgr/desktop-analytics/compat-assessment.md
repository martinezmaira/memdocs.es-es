---
title: Evaluación de compatibilidad
titleSuffix: Configuration Manager
description: Aprenda sobre la evaluación de compatibilidad para aplicaciones y controladores de Windows en Análisis de escritorio.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 7b2bff4f8365693c86540c9b0578307340f13a49
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268902"
---
# <a name="compatibility-assessment-in-desktop-analytics"></a>Evaluación de compatibilidad en Análisis de escritorio

Las evaluaciones de actualización de soluciones anteriores eran genéricas, por ejemplo: atención necesaria o corrección disponible. No proporcionan ningún indicador visual sobre cómo priorizar aplicaciones o controladores con problemas o actualizar información. Análisis de escritorio reemplaza esta característica por **Riesgo de compatibilidad**. Análisis de escritorio muestra la evaluación de las aplicaciones solo en la vista de implementación de un escenario previo a la actualización. Clasifica las aplicaciones en función de la información que Microsoft obtiene de las máquinas incluidas en un plan de implementación actual.

Análisis de escritorio usa las siguientes categorías de evaluación de compatibilidad:

- **Bajo**: el servicio no encontró señales de que una actualización de Windows vaya a poner en peligro esta aplicación. Es probable que funcione en el sistema operativo de destino tal cual.

- **Media**: Analytics indica que la aplicación puede tener una disparidades en la funcionalidad, aunque es probable puedan corregirse.

- **Alta**: es casi seguro que la aplicación va a generar un error durante o después de la actualización. Es posible que necesite una corrección.

- **Desconocido**: no se evaluó la aplicación. No hay ninguna otra información, como *Problemas conocidos de MS* o *Ready for Windows*.

En la lista de recursos de aplicación o controlador de un plan de implementación, verá este valor para cada recurso en la columna **Riesgo de compatibilidad**.

## <a name="app-risk-assessment"></a>Valoración del riesgo de la aplicación

![Diagrama de orígenes de evaluación de riesgos de la aplicación](media/app-risk-assessment-sources.png)

Son varios los orígenes que usa Análisis de escritorio para generar la clasificación de evaluación de las aplicaciones:

- [Problemas conocidos de Microsoft](#microsoft-known-issues)
- [Ready for Windows](#ready-for-windows)
- [Información avanzada](#advanced-insights)

Puede encontrar la evaluación de cada origen de la aplicación en Análisis de escritorio. En la lista de recursos de aplicación de un plan de implementación, seleccione una aplicación individual para abrir su panel de control flotante de propiedades. Verá una recomendación general y un nivel de evaluación. En la sección **Factores de riesgo de compatibilidad** se muestran los detalles de estas evaluaciones.

> [!TIP]
> Si en el panel de detalles de la aplicación no se muestra la evaluación de compatibilidad, puede deberse a que la opción **App Versions Details** (Detalles de versiones de la aplicación) está desactivada. Está desactivada de forma predeterminada y combina todas las versiones de las aplicaciones con el mismo nombre y el mismo editor. El servicio sigue realizando evaluaciones de riesgos de compatibilidad para cada versión. Active **App Versions Details** (Detalles de versiones de la aplicación) para ver la evaluación de riesgos de compatibilidad para una versión específica de la aplicación. Para más información, consulte [Planeamiento de recursos](about-deployment-plans.md#plan-assets).

## <a name="microsoft-known-issues"></a>Problemas conocidos de Microsoft

Análisis de escritorio examina la base de datos de compatibilidad de aplicaciones de Microsoft en busca de los problemas conocidos. Emplea esta base de datos para determinar los bloqueos de compatibilidad existentes para las aplicaciones disponibles públicamente de Microsoft u otros editores. Esta comprobación solo se aplica al sistema operativo de destino del plan de implementación que seleccione.

Verá los siguientes problemas en el panel de propiedades de la aplicación como **problemas conocidos de MS**:

### <a name="asset-is-removed-during-upgrade"></a>el recurso se quita durante la actualización

Windows detectó problemas de compatibilidad con una aplicación o un controlador. El recurso no se migrará a la nueva versión del sistema operativo. No es necesario realizar ninguna acción para que la actualización continúe. Instale una versión compatible de la aplicación o del controlador en la nueva versión del sistema operativo.

<!-- 3594545 -->
Windows puede quitar parcial o totalmente estos recursos:

- Eliminación completa: el programa de instalación de Windows quita completamente la aplicación o el controlador del dispositivo durante la actualización.
- Eliminación parcial: el programa de instalación de Windows quita parcialmente la aplicación o el controlador del dispositivo. Debe desinstalarlos manualmente después de actualizar Windows.

En ambos casos, después de actualizar Windows, el usuario no puede usar la aplicación ni el hardware asociado al controlador.

Para ver esta recomendación en el portal de Análisis de escritorio:

1. En un plan de implementación, seleccione **Preparar piloto**.
1. Seleccione la pestaña **Aplicaciones**.
1. Seleccione una aplicación y vea los factores de riesgo de compatibilidad y las recomendaciones en el panel lateral.

[![Captura de pantalla de la recomendación de recursos en el portal de Análisis de escritorio](media/3594545-app-removed.png)](media/3594545-app-removed.png#lightbox)

### <a name="blocking-upgrade"></a>Bloqueo de la actualización

Windows detectó problemas de bloqueo y no puede quitar la aplicación durante la actualización. Es posible que no funcione en la nueva versión del sistema operativo. Antes de actualizar, quite la aplicación. Vuelva a instalarla y pruébela en la nueva versión del sistema operativo.

### <a name="blocking-upgrade-but-can-be-reinstalled-after-upgrading"></a>Bloquear la actualización, pero puede reinstalarse después de actualizar

La aplicación es compatible con la nueva versión del sistema operativo, pero no se migrará. Quite la aplicación antes de actualizar Windows. Vuelva a instalarla en la nueva versión del sistema operativo.

### <a name="blocking-upgrade-update-application-to-newest-version"></a>Bloquear la actualización, actualizar la aplicación a la versión más reciente

La versión existente de la aplicación no es compatible con la nueva versión del sistema operativo y no se migrará. Hay disponible una versión compatible de la aplicación. Actualice la aplicación antes de realizar la actualización.

### <a name="disk-encryption-blocking-upgrade"></a>Actualización de bloqueo de cifrado de disco

Las características de cifrado de la aplicación bloquean la actualización. Deshabilite la característica de cifrado antes de actualizar Windows y habilítela después de la actualización.

### <a name="does-not-work-with-new-os-but-wont-block-upgrade"></a>No funciona con el nuevo sistema operativo, pero no bloquea la actualización

La aplicación no es compatible con la nueva versión del sistema operativo, pero no bloquea la actualización. No es necesario realizar ninguna acción para que la actualización continúe. Instale una versión compatible de la aplicación en la nueva versión del sistema operativo.

### <a name="does-not-work-with-new-os-and-will-block-upgrade"></a>No funciona con el nuevo sistema operativo y se bloquea la actualización

La aplicación no es compatible con la nueva versión del sistema operativo y bloqueará la actualización. Quite la aplicación antes de la actualización. Puede que haya disponible una versión compatible de la aplicación.

### <a name="evaluate-application-on-new-os"></a>Evaluación de la aplicación en el nuevo sistema operativo

Windows migra la aplicación, pero detecta problemas que pueden afectar al rendimiento de la aplicación en la nueva versión del sistema operativo. No es necesario realizar ninguna acción para que la actualización continúe. Pruebe la aplicación en la nueva versión del sistema operativo.

### <a name="may-block-upgrade-test-application"></a>Puede bloquearse la actualización, pruebe la aplicación

Windows detectó problemas que pueden interferir con la actualización, pero que es necesario investigar más a fondo. Pruebe el comportamiento de la aplicación durante la actualización. Si bloquea la actualización, quítela antes de actualizar. A continuación, vuelva a instalarla y pruebe la nueva versión del sistema operativo.

### <a name="multiple"></a>Varios

Varios problemas afectan a la aplicación. Seleccione **Consulta** para ver los detalles de los problemas detectados por Windows.

### <a name="reinstall-application-after-upgrading"></a>Reinstalar la aplicación después de la actualización

La aplicación es compatible con la nueva versión del sistema operativo, pero debe volver a instalarla después de actualizar Windows. El proceso de actualización quita la aplicación. No es necesario realizar ninguna acción para que la actualización continúe. Vuelva a instalar la aplicación en la nueva versión del sistema operativo.

### <a name="safeguards"></a>Medidas de seguridad

<!-- 5746559 -->

Los datos de compatibilidad de Windows clasifican algunas aplicaciones y controladores con unas *medidas de seguridad*, lo que puede hacer que la actualización a Windows 10 no se realice correctamente o se revierta. Windows también puede actualizar, pero quita la aplicación o el controlador. Análisis de escritorio ahora puede ayudarle a identificar estas medidas de seguridad de antemano para que pueda corregir el recurso antes de implementar la actualización.

1. En el portal de Análisis de escritorio, seleccione el plan de implementación.

1. Seleccione **Plan assets** (Planear recursos) en el menú y cambie a la pestaña **Apps** (Aplicaciones).

1. Filtre la columna de nombre para mostrar los elementos con valores que contengan la palabra `Safeguard`. Seleccione el resultado para ver más información.

    > [!NOTE]
    > Esta entrada no es una aplicación real que está instalada en los dispositivos. Es un marcador de posición que ayuda a identificar las aplicaciones o los controladores de su entorno con la etiqueta de compatibilidad de medidas de seguridad.

1. En la sección de recomendación, seleccione el vínculo a *más información*. Este vínculo abre el sitio web de Windows con la lista actual de aplicaciones o controladores con la etiqueta de medidas de seguridad.

1. Compare la lista publicada actual con la lista de recursos de su entorno. Corrija cualquier aplicación o controlador potencialmente problemático mediante una actualización a una versión compatible.

[![Captura de pantalla de la aplicación de medidas de seguridad en Análisis de escritorio](media/5746559-safeguards.png)](media/5746559-safeguards.png#lightbox)

## <a name="ready-for-windows"></a>Ready for Windows

El estado de adopción se basa en la información de los dispositivos comerciales que comparten datos con Microsoft. El estado se integra con las instrucciones de soporte técnico de los proveedores de software.

Análisis de escritorio proporciona el estado de adopción para cada versión de un recurso que se encuentra en dispositivos comerciales. Este estado no incluye datos de los dispositivos de consumidor ni de aquellos que no comparten datos. El estado puede no ser representativo de la tasa de adopción en todos los dispositivos Windows 10.

Las categorías posibles son:

- **Adopción alta**: al menos 100 000 dispositivos comerciales de Windows 10 tienen instalada esta aplicación.

- **Adoptada**: al menos 10 000 dispositivos comerciales de Windows 10 tienen instalada esta aplicación.

- **Datos insuficientes**: son muy pocos los dispositivos comerciales de Windows 10 que están compartiendo información de esta aplicación como para que Microsoft clasifique su adopción.

- **Ponerse en contacto con el desarrollador**: puede que haya problemas de compatibilidad con esta versión de la aplicación. Microsoft recomienda ponerse en contacto con el proveedor de software para obtener más información.

- **Desconocido**: no hay información disponible para esta versión de esta aplicación. Puede que haya información disponible para otras versiones de la aplicación.

### <a name="support-statement"></a>Declaración de compatibilidad

Si el proveedor de software admite una o varias versiones de esta aplicación en Windows 10, verá esta declaración en el panel de propiedades de la aplicación. En la sección de factores de riesgo de compatibilidad, vea lo que pone en **Declaración de compatibilidad**.

## <a name="advanced-insights"></a>Información avanzada

Análisis de escritorio también puede detectar problemas mediante la siguiente información adicional:

### <a name="adopted-version-available"></a>Versión adoptada disponible

Hay otra versión de esta aplicación muy adoptada por otros clientes. Esta señal usa datos de adopción del ecosistema de Windows. Si hay algún bloqueador de actualizaciones con la versión actual, considere la posibilidad de implementar la versión alternativa. Para buscar las versiones alternativas adoptadas de la aplicación, consulte el estado de la aplicación en "Preparar la producción".

### <a name="driver-dependency"></a>Dependencia del controlador

La aplicación depende de un controlador. Análisis de escritorio recomienda la prueba piloto de la aplicación para detectar posibles regresiones. Si tiene algún problema, póngase en contacto con el editor para solicitar una versión compatible con Windows 10.

### <a name="additional-insights"></a>Información adicional

<!-- 4021225 -->
Al actualizar el sitio y los clientes de Configuration Manager a la versión 1906, los clientes también notifican esta información adicional, cuando el nivel de datos de diagnóstico está establecido en Mejorado (limitado):

> [!Important]  
> Para aprovechar al máximo las nuevas características de Configuration Manager, después de actualizar el sitio, actualice también los clientes a la versión más reciente. Este escenario no funciona hasta que la versión del cliente es también la más reciente.

#### <a name="16-bit-apps"></a>Aplicaciones de 16 bits

Quite todos los componentes de 16 bits de las aplicaciones y reemplácelos por sus equivalentes de 32 o 64 bits. Para más información, consulte [La historia de los desarrolladores de Windows Vista y Windows Server 2008: Recetas de compatibilidad de aplicaciones](https://docs.microsoft.com/previous-versions/aa480152\(v=msdn.10\)).

La otra opción consiste en habilitar NT Virtual DOS Machine (NTVDM) para la compatibilidad con Windows 10.

#### <a name="requires-admin-privileges"></a>Requiere privilegios de administrador

La aplicación requiere que el usuario tenga acceso administrativo al dispositivo. Use un manifiesto de aplicación para las aplicaciones que requieran permisos de administrador. Para más información, consulte [Creación e inserción de un manifiesto de aplicación](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\)).

Análisis de escritorio recomienda la prueba piloto de la aplicación para detectar posibles regresiones.

#### <a name="java-dependency"></a>Dependencia de Java

Muchas aplicaciones Java dependen de una instancia de Java Runtime Environment instalada por separado (JRE). Aunque es posible que las versiones anteriores de JRE sigan funcionando en Windows 10, Oracle solo admite las últimas. El uso de una versión anterior de JRE no compatible puede presentar vulnerabilidades de seguridad. Compruebe que la aplicación se ejecuta en las versiones más recientes de JRE.

#### <a name="not-dpi-aware"></a>No compatible con PPP

Es posible que la aplicación tenga problemas de visualización con las resoluciones de pantalla avanzadas de Windows 10. Use un manifiesto de aplicación para evitar problemas con resoluciones de PPP altas. Para más información, consulte [Manifiestos de la aplicación](https://docs.microsoft.com/windows/desktop/SbsCs/application-manifests).

Análisis de escritorio recomienda la prueba piloto de la aplicación para detectar posibles regresiones.

#### <a name="silverlight-framework"></a>Marco de Silverlight

Microsoft recomienda que las aplicaciones no basadas en el explorador no usen Silverlight. La fecha de finalización del soporte técnico para Silverlight 5 es octubre de 2021.

La mayoría de los exploradores web actuales no admiten Silverlight.

| Explorador | Compatibilidad |
|---------|---------|
| Google Chrome | Fin de soporte técnico: Septiembre de 2015 |
| Firefox | Fin de soporte técnico: Marzo de 2017 |
| Microsoft Edge | No hay complementos disponibles |

Análisis de escritorio recomienda la prueba piloto de la aplicación para detectar posibles regresiones.

#### <a name="net-framework-1011"></a>.NET Framework 1.0/1.1

La versión 1.0 de .NET Framework no se admite en Windows 10. La versión 1.1 no es compatible con Windows 10. Si la aplicación es de un editor de terceros, póngase en contacto con el proveedor para solicitar una versión compatible con Windows 10. De lo contrario, vuelva a desarrollar la aplicación para usar una versión compatible de .NET.

#### <a name="net-framework-2030"></a>.NET Framework 2.0/3.0

Los marcos .NET 2.0 y 3.5 se admiten en Windows 10. Es posible que tenga que habilitar la característica de Windows. Para más información, consulte [Instalar .NET Framework 3.5 en Windows 10](https://docs.microsoft.com/dotnet/framework/install/dotnet-35-windows-10).

#### <a name="ui-access"></a>Acceso a la interfaz de usuario

Las aplicaciones con acceso a la interfaz de usuario pueden omitir los niveles de control de la interfaz de usuario para dirigir la entrada a ventanas de privilegios más elevados en el escritorio. Use esta opción solo para aplicaciones de tecnología de asistencia de interfaz de usuario.

Si no va a usar las características de accesibilidad de la aplicación, la marca de acceso a la interfaz de usuario en el manifiesto de la aplicación se debe establecer en false. Para más información, consulte [Creación e inserción de un manifiesto de aplicación](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\)).

Análisis de escritorio recomienda la prueba piloto de la aplicación para detectar posibles regresiones.

## <a name="driver-risk-assessment"></a>Evaluación de riesgo de controladores

Análisis de escritorio también enumera y agrupa por disponibilidad los controladores que no se migren a la versión del sistema operativo.

Puede encontrar la evaluación sobre el controlador en Análisis de escritorio. En la lista de recursos de controlador de un plan de implementación, seleccione un controlador individual para abrir su panel de control flotante de propiedades. Verá una recomendación general y un nivel de evaluación. En la sección **Factores de riesgo de compatibilidad** se muestran los detalles de estas evaluaciones.

| Disponibilidad del controlador | ¿Acción necesaria? | Significado | Instrucciones |
|---------------------|------------------|---------------|----------|
| Disponible de forma predeterminada | No, solo para reconocimiento | La versión instalada actualmente de una aplicación o de un controlador no se migrará a la nueva versión del sistema operativo. Se instala una versión compatible con la nueva versión del sistema operativo. | No es necesario realizar ninguna acción para que la actualización continúe. |
| Importar desde Windows Update | Sí | La versión instalada actualmente de un controlador no se migra a la nueva versión del sistema operativo. Una versión compatible está disponible en Windows Update. | Si el equipo recibe automáticamente actualizaciones de Windows Update, no es necesario realizar ninguna acción. De lo contrario, importe un nuevo controlador desde Windows Update después de actualizar Windows. |
| Disponible de forma predeterminada y desde Windows Update | Sí | La versión instalada actualmente de un controlador no se migra a la nueva versión del sistema operativo. Aunque se instala un nuevo controlador durante la actualización, hay una versión más reciente disponible en Windows Update. | Si el equipo recibe automáticamente actualizaciones de Windows Update, no es necesario realizar ninguna acción. De lo contrario, importe un nuevo controlador desde Windows Update después de actualizar Windows. |
| Consultar con el proveedor | Sí | El controlador no se migrará a la nueva versión del sistema operativo y Análisis de escritorio no puede encontrar una versión compatible. | En el caso de una solución, consulte con el fabricante de hardware independiente (IHV) que fabrica el controlador o con el fabricante de equipos originales (OEM) que proporcionó el dispositivo. |

## <a name="see-also"></a>Vea también

Ventajas del Centro de FastTrack para Windows 10 proporciona acceso a **Asesoría de aplicaciones de escritorio**. Esta ventaja es un nuevo servicio diseñado para solucionar problemas con la compatibilidad de Windows 10 y Aplicaciones de Microsoft 365 para empresas. Para más información, consulte [Asesoría de aplicaciones de escritorio](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).
