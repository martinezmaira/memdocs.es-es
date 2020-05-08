---
title: Licencias y ramas
titleSuffix: Configuration Manager
description: Obtenga información sobre los requisitos de licencia para las opciones de instalación disponibles con Configuration Manager
ms.date: 06/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 495b87ae-41a4-49ba-abe2-d4f7d22ac0d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 04ed335c65369840085fe44ba2f1b81d7806a0e3
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906049"
---
# <a name="licensing-and-branches-for-configuration-manager"></a>Licencias y ramas de Configuration Manager

*Se aplica a: Configuration Manager (rama actual) y System Center Configuration Manager (rama de mantenimiento a largo plazo)*

Use este artículo para obtener información sobre los requisitos de licencia de las opciones de instalación disponibles con Configuration Manager. Estas opciones de instalación incluyen las siguientes ramas:

- Rama actual
- Rama de mantenimiento a largo plazo (LTSB)
- Instalación de evaluación de la rama actual
- Rama de Technical Preview

## <a name="licensing-overview"></a>Introducción a las licencias

Los clientes con Software Assurance (SA) activo en licencias de Configuration Manager o con derechos de suscripción equivalentes el 1 de octubre de 2016 tienen derecho a usar la versión 1606 de octubre de 2016 de Configuration Manager. Los clientes con derechos para Configuration Manager el 1 de octubre de 2016 o después de esta fecha encontrarán dos opciones de licencia tras la instalación: la rama actual y la rama de mantenimiento a largo plazo (LTSB).

Para conocer los términos y condiciones completos de los productos que compra mediante los programas de licencias por volumen de Microsoft, consulte [Licencias y ramas](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1).


## <a name="licensed-branches"></a>Ramas con licencia

En este artículo hace referencia al contrato de Software Assurance o los derechos de suscripción equivalentes. Este contrato de licencia de Microsoft concede derechos para instalar y usar Configuration Manager.

### <a name="current-branch"></a>Rama actual

La rama actual requiere un contrato de Software Assurance activo (o derechos equivalentes) para Configuration Manager. Para obtener más información, consulte [Software Assurance y la Rama actual](#software-assurance-and-the-current-branch).

El uso de esta rama se admite en entornos de producción que desean recibir actualizaciones periódicas de calidad y de características de Microsoft. Proporciona acceso para usar todas las características y mejoras.

Desde la versión 1710, cada versión de actualización seguirá siendo compatible durante 18 meses a partir de la fecha de lanzamiento de disponibilidad general. Para más información, vea [Compatibilidad con versiones de la rama actual de System Center Configuration Manager](../servers/manage/current-branch-versions-supported.md).

### <a name="long-term-servicing-branch-ltsb"></a>Rama de mantenimiento a largo plazo (LTSB)

La LTSB requiere un contrato de Software Assurance en vigor con Microsoft a fecha de 1 de octubre de 2016. Para obtener más información, vea [Software Assurance y LTSB](#software-assurance-and-the-ltsb).

El uso de esta rama se admite en entornos de producción. Está destinado a clientes que han dejado que su contrato de Software Assurance (SA) o los derechos de suscripción equivalentes para Configuration Manager caduquen después del 1 de octubre de 2016. Esta rama tiene opciones limitadas en comparación con la Rama actual.

Las actualizaciones de seguridad críticas para Configuration Manager se ponen a disposición de esta Rama, pero no así las nuevas características.

### <a name="evaluation-installation-of-the-current-branch"></a>Instalación de evaluación de la rama actual

La versión de evaluación no requiere un contrato de Software Assurance con Microsoft. Las [instalaciones de evaluación](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) siempre son la rama actual, y pueden usarse durante 180 días.

Puede actualizar la instalación de evaluación a una instalación completa de la rama actual. No puede actualizar una instalación de evaluación a la rama de mantenimiento a largo plazo.

### <a name="technical-preview-branch"></a>Rama de Technical Preview

La [rama de Technical Preview](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) está también disponible. Esta rama es una compilación limitada de Configuration Manager que le permite probar las nuevas características. La versión Technical Preview se instala por medios diferentes que las versiones con licencia. Para obtener más información, consulte [Technical Preview](../get-started/technical-preview.md).


## <a name="software-assurance-agreements"></a>Contratos de Software Assurance

El estado de Software Assurance en sus licencias de Configuration Manager, o derechos de suscripción equivalentes, el 1 de octubre de 2016 o en una fecha posterior determina la rama que puede instalar y usar.

### <a name="software-assurance-and-the-current-branch"></a>Software Assurance y la rama actual

Los derechos para usar la rama actual de Configuration Manager pueden proporcionarse por:

- **System Center:** los clientes con SA activo en licencias de System Center Standard o Datacenter pueden instalar y usar la opción de la rama actual de Configuration Manager.

- **System Center Configuration Manager:** los clientes con SA activo en licencias de Configuration Manager, o con derechos de suscripción equivalentes, pueden instalar y usar la opción de rama actual de Configuration Manager.

Si tiene SA activo en licencias de Configuration Manager o derechos de suscripción equivalentes el 1 de octubre de 2016 o en una fecha posterior:

- Puede instalar y usar la rama actual.
- Si permite que SA o la suscripción expire, debe desinstalar la rama actual.

### <a name="software-assurance-and-the-ltsb"></a>Software Assurance y LTSB

Si tiene SA activo en licencias de Configuration Manager o derechos de suscripción equivalentes el 1 de octubre de 2016 o en una fecha posterior:

- Puede instalar y usar la LTSB. Los clientes que tengan derechos perpetuos en Configuration Manager, o que admitan que SA o la suscripción expiren, pueden instalar la versión de LTSB de Configuration Manager que esté vigente en el momento de la expiración.

LTSB se basa en la versión de la rama actual 1606 y tiene las siguientes limitaciones:

- No hay soporte para convertir una rama actual a LTSB. Si tiene actualmente un sitio de rama actual, debe instalar LTSB como un nuevo sitio.  

- LTSB no es compatible con todas las funciones de la rama actual. Para obtener más información, consulte [Introducción a la rama de mantenimiento a largo plazo](introduction-to-the-ltsb.md). Estas limitaciones incluyen un conjunto limitado de características, opciones de actualización limitadas y un ciclo de vida de soporte técnico de producto independiente.  

### <a name="software-assurance-expiration-date"></a>Fecha de expiración de Software Assurance

A partir de la versión de octubre de 2016 de los medios de línea base de la versión 1606 para Configuration Manager, puede especificar la fecha de expiración de su contrato de Software Assurance. La **fecha de expiración de Software Assurance** es un valor opcional como un recordatorio útil. Agréguela al ejecutar la instalación de Configuration Manager o posteriormente desde la consola de Configuration Manager.

> [!NOTE]
> Microsoft no valida la fecha de expiración que especifique y no la usará para la validación de la licencia. Úsela como recordatorio de la fecha de expiración. Este valor es útil cuando Configuration Manager comprueba periódicamente si hay nuevas actualizaciones de software que se ofrecen en línea. El estado de su licencia de Software Assurance debe ser actual para reunir los requisitos que permiten usar estas actualizaciones adicionales.

#### <a name="to-specify-the-software-assurance-expiration-date"></a>Para especificar la fecha de expiración de Software Assurance

- Al ejecutar el programa de instalación del medio de Configuration Manager, especifique el valor en la página **Clave de producto** del Asistente para instalación.

- En la consola de Configuration Manager, en **Propiedades de jerarquía**, especifique el valor en la pestaña **Licencia**.


## <a name="licensing-resources"></a>Recursos de licencias

Utilice los siguientes recursos para obtener más información acerca de los detalles de licencias de productos.

### <a name="microsoft-volume-licensing-service-center-vlsc"></a>Centro de servicios de licencias por volumen de Microsoft (VLSC)

- [Información general de VLSC](https://www.microsoft.com/Licensing/existing-customer/vlsc-training-and-resources.aspx)

- [Términos del programa Licencias por Volumen de Microsoft](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1)

- Los clientes de licencias por volumen pueden obtener un resumen de sus licencias en el [Centro de servicios de licencias por volumen](https://www.microsoft.com/Licensing/servicecenter/default.aspx). Vaya al menú **Licencias** y haga clic en **Licenses Summary** (Resumen de licencias).

### <a name="vlsc-videos"></a>Vídeos del Centro de servicios de licencias por volumen

- Para ver videos de formación sobre el funcionamiento del Centro de servicios de licencias por volumen, vaya a [Aprendizaje y recursos del Centro de servicios de licencias por volumen de Microsoft](https://www.microsoft.com/licensing/existing-customer/vlsc-training-and-resources) y seleccione **Vídeos de instrucciones**.

- [Dónde buscar el contrato de Software Assurance activo](https://www.microsoft.com/showcase/video.aspx?uuid=fe1846cb-1d26-49fc-b064-57b25dcc31a0) (a partir del segundo 43)  

- [Cómo obtener permisos para VLSC](https://www.microsoft.com/showcase/video.aspx?uuid=ac4ed1ca-d0a9-43cd-89fa-74ccb555dec4) Puede delegar los permisos de lectura y escritura del Centro de servicios de licencias por volumen a otras personas de su organización.
