---
title: Consulta de los informes de BitLocker
titleSuffix: Configuration Manager
description: Obtenga información sobre los informes de administración de BitLocker en Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 0bae9477-0500-41cf-8aa3-5e6efadd0554
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d10717f980922e1f6d1fca9224e288b4df709da2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699623"
---
# <a name="view-bitlocker-reports"></a>Consulta de los informes de BitLocker

*Se aplica a: Configuration Manager (rama actual)*

<!--3601034-->

Después de [instalar los informes](setup-websites.md) en el punto de servicios de informes, puede ver los informes. Los informes muestran el cumplimiento de BitLocker en la empresa y dispositivos individuales. Proporcionan información en tablas y gráficos, y tienen filtros que permiten ver los datos desde distintas perspectivas.

En la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Informes** y seleccione el nodo **Informes**. Los informes siguientes aparecen en la categoría **Administración de BitLocker**:

- [Cumplimiento de equipos de BitLocker](#bkmk-compliancereport)

- [Panel de cumplimiento de BitLocker Enterprise](#bkmk-dashboard)

- [Detalles de cumplimiento de BitLocker Enterprise](#bkmk-compliancedetails)

- [Resumen de cumplimiento de BitLocker Enterprise](#bkmk-compliancesummary)

- [Informe de auditoría de recuperación](#bkmk-audit)

Puede acceder a todos estos informes directamente desde el sitio web del punto de servicios de informes.

> [!NOTE]
> Para que estos informes muestren datos completos:
>
> - Cree e implemente una directiva de administración de BitLocker en una colección de dispositivos.
> - Los clientes de la colección de destino deben enviar el inventario de hardware.

## <a name="bitlocker-computer-compliance"></a><a name="bkmk-compliancereport"></a> Cumplimiento de equipos de BitLocker

Use este informe para recopilar información específica de un equipo. Proporciona información de cifrado detallada sobre la unidad del sistema operativo y las unidades de datos fijas. Para ver los detalles de cada unidad, expanda la entrada Nombre del equipo. También indica la directiva que se aplica a cada uno de los tipos de unidades del equipo.

[![Captura de pantalla de ejemplo del informe Cumplimiento de equipos de BitLocker](media/bitlocker-computer-compliance.png)](media/bitlocker-computer-compliance.png#lightbox)

También puede usar este informe para determinar el último estado conocido de cifrado de BitLocker de equipos perdidos o robados. Configuration Manager determina la compatibilidad del dispositivo en función de las directivas de BitLocker que implemente. Antes de intentar determinar el estado de cifrado de BitLocker de un dispositivo, compruebe las directivas que ha implementado.

> [!NOTE]
> En este informe no se muestra el estado de cifrado del volumen de datos extraíble.

### <a name="computer-details"></a>Detalles del equipo

|Nombre&nbsp;de columna|Descripción|
|----------------|----|
|Nombre del equipo|Nombre de equipo DNS especificado por el usuario.|
|Nombre de dominio|Nombre de dominio completo del equipo.|
|Tipo de equipo|Los tipos de equipo válidos son **No portátil** y **Portátil**.|
|Sistema operativo|Tipo de sistema operativo del equipo.|
|Cumplimiento general|Estado de cumplimiento de BitLocker general del equipo. Los estados válidos son **Conforme** y **No conforme**. El [estado de cumplimiento por unidad](#bkmk_volume) puede indicar otros estados de cumplimiento. Pero este campo representa ese estado de cumplimiento de la directiva especificada.|
|Cumplimiento del sistema operativo|Estado de cumplimiento del sistema operativo del equipo. Los estados válidos son **Conforme** y **No conforme**.|
|Cumplimiento de la unidad de datos fija|Estado de cumplimiento de una unidad de datos fija en el equipo. Los estados válidos son **Conforme** y **No conforme**.|
|Fecha de última actualización|Fecha y hora en que el equipo se ha puesto en contacto por última vez con el servidor para notificar el estado de cumplimiento.|
|Exención|Indica si el usuario está exento o no exento de la directiva de BitLocker.|
|Usuario exento|Usuario que está exento de la directiva de BitLocker.|
|Fecha de exención|Fecha en la que se ha concedido la exención.|
|Detalles del estado de cumplimiento|Mensajes de error y estado sobre el estado de cumplimiento del equipo de la directiva especificada.|
|Directiva: intensidad de cifrado|Intensidad de cifrado que ha seleccionado en la directiva de administración de BitLocker.|
|Directiva: Unidad de sistema operativo|Indica si se necesita cifrado para la unidad de sistema operativo y el tipo de protector adecuado.|
|Directiva: Unidad de datos fija|Indica si se necesita cifrado para la unidad de datos fija.|
|Fabricante|Nombre del fabricante del equipo como aparece en el BIOS del equipo.|
|Modelo|Nombre del modelo del fabricante del equipo como aparece en el BIOS del equipo.|
|Usuarios de los dispositivos|Usuarios conocidos en el equipo.|

### <a name="computer-volume"></a><a name="bkmk_volume"></a> Volumen del equipo

|Nombre&nbsp;de columna|Descripción|
|----------------|----|
|Letra de unidad|La letra de unidad del equipo.|
|Tipo de unidad|Tipo de unidad. Los valores válidos son **Unidad de sistema operativo** y **Unidad de datos fija**. Estas entradas son unidades físicas en lugar de volúmenes lógicos.|
|Intensidad de cifrado|Intensidad de cifrado que ha seleccionado durante la directiva de administración de BitLocker.|
|Tipos de protector|Tipo de protector seleccionado en la directiva para cifrar la unidad. Los tipos de protector válidos para una unidad del sistema operativo son **TPM** o **TPM+PIN**. El tipo de protector válido de una unidad de datos fija es **Contraseña**.|
|Estado del protector|Indica que el equipo ha habilitado el tipo de protector especificado en la directiva. Los estados válidos son **ACTIVADO** o  **DESACTIVADO**.|
|Estado de cifrado|Estado de cifrado de la unidad. Los estados válidos son **Cifrado**, **Sin cifrar** o **Cifrando**.|

## <a name="bitlocker-enterprise-compliance-dashboard"></a><a name="bkmk-dashboard"></a> Panel de cumplimiento de BitLocker Enterprise

En este informe se proporcionan los gráficos siguientes, que muestran el estado de cumplimiento de BitLocker en toda la organización:

- Distribución del estado de cumplimiento

- No compatible: distribución de errores

- Distribución del estado de cumplimiento por tipo de unidad

[![Captura de pantalla de ejemplo del panel de cumplimiento de BitLocker Enterprise](media/bitlocker-enterprise-compliance-dashboard.png)](media/bitlocker-enterprise-compliance-dashboard.png#lightbox)

### <a name="compliance-status-distribution"></a>Distribución del estado de cumplimiento

En este gráfico circular se muestra el estado de cumplimiento de los equipos de la organización. También muestra el porcentaje de equipos con ese estado de cumplimiento en comparación con el número total de equipos de la colección seleccionada. Además se muestra el número real de equipos con cada estado.

El gráfico circular muestra los siguientes estados de cumplimiento:

- conforme

- No compatible

- Exención del usuario

- Exención del usuario temporal

- Directiva no aplicada

- Desconocido. Estos equipos han notificado un error de estado o forman parte de la colección, pero nunca han notificado su estado de cumplimiento. La falta de un estado de cumplimiento puede producirse si el equipo se desconecta de la organización.

### <a name="non-compliant---errors-distribution"></a>No compatible: distribución de errores

En este gráfico circular se muestran las categorías de equipos de la organización que no son compatibles con la directiva Cifrado de unidad BitLocker. También se muestra el número de equipos de cada categoría. El informe calcula cada porcentaje a partir del número total de equipos no compatibles de la colección.

- Cifrado pospuesto por el usuario

- No se encuentra ningún TPM compatible

- La partición del sistema no está disponible o no es lo suficientemente grande

- TPM visible pero no inicializado

- Conflicto de directiva

- Esperando el aprovisionamiento automático de TPM

- Error desconocido

- No hay información. Estos equipos no tienen instalado el agente de administración de BitLocker, o bien está instalado pero no activado. Por ejemplo, el servicio no funciona.

### <a name="compliance-status-distribution-by-drive-type"></a>Distribución del estado de cumplimiento por tipo de unidad

Este gráfico de barras muestra el estado actual de cumplimiento de BitLocker por tipo de unidad. Los estados son **Conforme** y **No conforme**. Se muestran barras para las unidades de datos fijas y las de sistema operativo. El informe incluye los equipos sin una unidad de datos fija y solo muestra un valor en la barra **Unidad de sistema operativo**. El gráfico no incluye a los usuarios a los que se ha concedido una exención de la directiva Cifrado de unidad BitLocker o la categoría Sin directiva.

## <a name="bitlocker-enterprise-compliance-details"></a><a name="bkmk-compliancedetails"></a> Detalles de cumplimiento de BitLocker Enterprise

En este informe se muestra información sobre el cumplimiento general de BitLocker en la organización para la colección de equipos en los que ha implementado la directiva de administración de BitLocker.

[![Captura de pantalla de ejemplo de Detalles de cumplimiento de BitLocker Enterprise](media/bitlocker-enterprise-compliance-details.png)](media/bitlocker-enterprise-compliance-details.png#lightbox)

|Nombre de columna|Descripción|
|--- |--- |
|Equipos administrados|Número de equipos en los que se ha implementado una directiva de administración de BitLocker.|
|% compatible|Porcentaje de equipos compatibles de la organización.|
|% no compatible|Porcentaje de equipos no compatibles de la organización.|
|% de cumplimiento desconocido|Porcentaje de equipos con un estado de cumplimiento desconocido.|
|% exento|Porcentaje de equipos exentos del requisito de cifrado de BitLocker.|
|% no exento|Porcentaje de equipos no exentos del requisito de cifrado de BitLocker.|
|conforme|Recuento de equipos compatibles de la organización.|
|No compatible|Recuento de equipos no compatibles de la organización.|
|Cumplimiento desconocido|Recuento de equipos con un estado de cumplimiento desconocido.|
|Exento|Recuento de equipos que están exentos del requisito de cifrado de BitLocker.|
|No exento|Recuento de equipos que no están exentos del requisito de cifrado de BitLocker.|

### <a name="computer-details"></a>Detalles del equipo

|Nombre de columna|Descripción|
|--- |--- |
|Nombre del equipo|Nombre de equipo DNS del dispositivo administrado.|
|Nombre de dominio|Nombre de dominio completo del equipo.|
|Estado de cumplimiento|Estado de cumplimiento general del equipo. Los estados válidos son **Conforme** y **No conforme**.|
|Exención|Indica si el usuario está exento o no exento de la directiva de BitLocker.|
|Usuarios de los dispositivos|Usuarios del dispositivo.|
|Detalles del estado de cumplimiento|Mensajes de error y estado sobre el estado de cumplimiento del equipo de la directiva especificada.|
|Último contacto|Fecha y hora en que el equipo se ha puesto en contacto por última vez con el servidor para notificar el estado de cumplimiento.|

## <a name="bitlocker-enterprise-compliance-summary"></a><a name="bkmk-compliancesummary"></a> Resumen de cumplimiento de BitLocker Enterprise

Use este informe para mostrar el cumplimiento general de BitLocker en toda la organización. También se muestra la compatibilidad de los equipos individuales en los que se ha implementado la directiva de administración de BitLocker.

[![Captura de pantalla de ejemplo de Resumen de cumplimiento de BitLocker Enterprise](media/bitlocker-enterprise-compliance-summary.png)](media/bitlocker-enterprise-compliance-summary.png#lightbox)

|Nombre de columna|Descripción|
|--- |--- |
|Equipos administrados|Número de equipos que se administran con la directiva de BitLocker.|
|% compatible|Porcentaje de equipos compatibles de la organización.|
|% no compatible|Porcentaje de equipos no compatibles de la organización.|
|% de cumplimiento desconocido|Porcentaje de equipos con un estado de cumplimiento desconocido.|
|% exento|Porcentaje de equipos exentos del requisito de cifrado de BitLocker.|
|% no exento|Porcentaje de equipos no exentos del requisito de cifrado de BitLocker.|
|conforme|Recuento de los equipos compatibles en la organización.|
|No compatible|Recuento de los equipos no compatibles en la organización.|
|Cumplimiento desconocido|Recuento de equipos con un estado de cumplimiento desconocido.|
|Exento|Recuento de equipos que están exentos del requisito de cifrado de BitLocker.|
|No exento|Recuento de equipos que no están exentos del requisito de cifrado de BitLocker.|

## <a name="recovery-audit-report"></a><a name="bkmk-audit"></a> Informe de auditoría de recuperación

> [!NOTE]
> Este informe también está disponible en el [sitio web de administración y supervisión de BitLocker](helpdesk-portal.md#reports).
>
> Para ver este informe en la consola de Configuration Manager, vaya al área de trabajo **Supervisión**. En el panel de navegación, expanda el nodo **Informes**, luego **Informes** y después la carpeta **Administración de BitLocker**. Seleccione la subcarpeta de la versión localizada del informe, por ejemplo, **es-es**.

Use este informe para auditar a los usuarios que han solicitado acceso a las claves de recuperación de BitLocker. Puede filtrar según los criterios siguientes:

- Un tipo específico de usuario, por ejemplo, un usuario del departamento de soporte técnico o un usuario final
- Si se ha producido un error en la solicitud o se ha realizado correctamente
- El tipo específico de la clave solicitada: contraseña de clave de recuperación, id. de la clave de recuperación o hash de contraseña del TPM
- Intervalo de fechas durante el que se ha producido la recuperación

[![Captura de pantalla de ejemplo del informe de auditoría de recuperación de BitLocker](media/bitlocker-recovery-audit-report.png)](media/bitlocker-recovery-audit-report.png#lightbox)

|Nombre&nbsp;de columna|Descripción|
|----------------|----|
|Fecha y hora de solicitud|Fecha y hora en que un usuario final o el departamento de soporte técnico ha solicitado una clave.|
|Origen de la solicitud de auditoría|El sitio del que proviene la solicitud. Los valores válidos son **Portal de autoservicio** o **Departamento de soporte técnico**.|
|Resultado de la solicitud|Estado de la solicitud. Los valores válidos son **Correcto** o **Con errores**.|
|Usuario de soporte técnico|El usuario administrativo que ha solicitado la clave. Si un administrador del departamento de soporte técnico recupera la clave sin especificar el nombre de usuario, el campo **Usuario final** está en blanco. Un usuario estándar del departamento de soporte técnico debe especificar el nombre de usuario, que aparece en este campo. Para la recuperación a través del portal de autoservicio, en este campo y en el campo **Usuario final** se muestra el nombre del usuario que realiza la solicitud.|
|Usuario final|Nombre del usuario que ha solicitado la recuperación de la clave.|
|Equipo|Nombre del equipo que se ha recuperado.|
|Tipo de clave|Tipo de clave que ha solicitado el usuario. Los tres tipos de claves son los siguientes:<br/><br/>- **Contraseña de clave de recuperación**: se usa para recuperar un equipo en modo de recuperación<br/>- **Id. de la clave de recuperación**: se usa para recuperar un equipo en modo de recuperación para otro usuario<br/>- **Hash de contraseña del TPM**: se usa para recuperar un equipo con un TPM bloqueado|
|Descripción del motivo|Por qué el usuario ha solicitado el tipo de clave especificado, en función de la opción seleccionada en el formulario.|
