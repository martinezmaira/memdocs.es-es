---
title: Certificados y seguridad
titleSuffix: Configuration Manager
description: Administrar certificados y seguridad de System Center Updates Publisher
ms.date: 04/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: a7f91e63-4750-402e-9970-dd14be7f76a3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: dc8e31245212136cd67f6f8cac062723c2cabefb
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696011"
---
# <a name="manage-certificates-and-security-for-updates-publisher"></a>Administrar certificados y seguridad de Updates Publisher

*Se aplica a: Configuration Manager (rama actual)*

Los procedimientos siguientes pueden ayudarle a configurar el almacén de certificados en el servidor de actualización, configurar un certificado autofirmado en el equipo cliente y configurar la directiva de grupo para permitir que el Agente de Windows Update en los equipos busque las actualizaciones publicadas.

## <a name="configure-the-certificate-store-on-the-update-server"></a>Configurar el almacén de certificados en el servidor de actualización
 Updates Publisher usa un certificado digital para firmar las actualizaciones en los catálogos que publica. Para poder publicar un catálogo en el servidor de actualización, ese certificado debe estar en el almacén de certificados del servidor de actualización y en el almacén de certificados del equipo de Updates Publisher si este equipo es remoto con respecto al servidor de actualización.

El procedimiento siguiente es uno de los distintos métodos posibles para agregar el certificado al almacén de certificados del servidor de actualización.

### <a name="to-configure-the-certificate-store"></a>Para configurar el almacén de certificados
1.  En un equipo que puede acceder al equipo de Updates Publisher y al servidor de actualización, haga clic en **Iniciar** y en **Ejecutar**, escriba **MMC** en el cuadro de texto y luego haga clic en **Aceptar** para abrir la Microsoft Management Console (MMC).

2.  Haga clic en **Archivo**, en **Agregar o quitar complemento**, en **Agregar**, en **Certificados** y en **Agregar**, seleccione **Cuenta de equipo** y luego haga clic en **Siguiente**.

3.  Seleccione **Otro equipo** y escriba el nombre del servidor de actualización o haga clic en **Examinar** para encontrar el equipo servidor de actualización, haga clic en **Finalizar**, en **Cerrar** y luego, en **Aceptar**.

4.  Expanda **Certificados (*nombre del servidor de actualización*)** , expanda **WSUS** y luego haga clic en **Certificados**.

5.  Haga clic con el botón derecho en el certificado que quiera, haga clic en **Todas las tareas** y luego, en **Exportar**.

6.  En el Asistente para exportar certificados, use la configuración predeterminada para crear un archivo de exportación con el nombre y la ubicación especificados en el asistente. Este archivo debe estar disponible en el servidor de actualización antes de continuar con el paso siguiente.

7.  Haga clic con el botón derecho en **Editores de confianza**, haga clic en **Todas las tareas** y luego, en **Importar**. Complete el Asistente para importar certificados con el archivo exportado del paso 6.

8.  Si se usa un certificado autofirmado, como **WSUS Publishers Self-signed** (Editores WSUS autofirmados), haga lic en **Entidades de certificación raíz de confianza**, en **Todas las tareas** y luego, en **Importar**. Complete el Asistente para importar certificados con el archivo exportado del paso 6.

9.  Haga clic con el botón derecho en **Certificados (*nombre del servidor de actualización*)** , haga clic en **Conectar a otro equipo**, especifique el nombre del equipo de Updates Publisher y haga clic en **Aceptar**.

10. Si Updates Publisher es remoto con respecto al servidor de actualización, repita los pasos del 7 al 9 para importar el certificado al almacén de certificados del equipo de Updates Publisher.



## <a name="configure-a-self-signing-certificate-on-client-computers"></a>Configurar un certificado autofirmado en equipos cliente
En equipos cliente, el Agente de Windows Update (WUA) buscará actualizaciones en el catálogo. Este proceso no podrá instalar actualizaciones cuando el agente no encuentre ese certificado digital en el almacén de editores de confianza del equipo local. Si se utilizó un certificado autofirmado para publicar el catálogo de actualizaciones, como **WSUS Publishers Self-signed** (Editores WSUS autofirmados), el certificado también debe estar en el almacén de certificados Entidades de certificación raíz de confianza del equipo local para que el agente pueda comprobar la validez del certificado.

Puede usar varios métodos para configurar certificados en equipos cliente, al igual que con la directiva de grupo y la **Asistente para importar certificados** o mediante la distribución de software y la herramienta Certutil.

El siguiente ejemplo muestra cómo configurar el certificado de firma en equipos cliente.

### <a name="to-configure-a-self-signing-certificate-on-client-computers"></a>Para configurar un certificado autofirmado en equipos cliente
1. En un equipo con acceso al servidor de actualización, haga clic en **Iniciar** y en **Ejecutar**, escriba **MMC** en el cuadro de texto y luego haga clic en **Aceptar** para abrir la Microsoft Management Console (MMC).

2. Haga clic en **Archivo**, en **Agregar o quitar complemento**, en **Agregar**, en **Certificados** y en **Agregar**, seleccione **Cuenta de equipo** y luego haga clic en **Siguiente**.

3. Seleccione **Otro equipo** y escriba el nombre del servidor de actualización o haga clic en **Examinar** para encontrar el equipo servidor de actualización, haga clic en **Finalizar**, en **Cerrar** y luego, en **Aceptar**.

4. Expanda **Certificados (*nombre del servidor de actualización*)** , expanda **WSUS** y luego haga clic en **Certificados**.

5. Haga clic con el botón derecho en el certificado en el panel de resultados, haga clic en **Todas las tareas** y luego, en **Exportar**. Complete el **Asistente para exportar certificados** con la configuración predeterminada para crear un archivo de exportación de certificado con el nombre y la ubicación especificados en el asistente.

6. Use uno de los métodos siguientes para agregar el certificado empleado para firmar el catálogo de actualizaciones en cada equipo cliente que usará el WUA para buscar actualizaciones en el catálogo. Agregue el certificado en el equipo cliente de la manera siguiente:

   -   Para los certificados autofirmados: agregue el certificado a los almacenes de certificados **Entidades de certificación raíz de confianza** y **Editores de confianza**.

   -   Para los certificados emitidos por entidades de certificación (CA): Agregue el certificado al almacén de certificados **Editores de confianza**.

   > [!NOTE]
   > El WUA también comprueba si la opción de directiva de grupo **Allow signed content from intranet Microsoft update service location** (Permitir contenido firmado procedente de la ubicación del servicio Microsoft Update de la intranet) está habilitada en el equipo local. Esta opción de directiva debe estar habilitada para que el Agente de Windows Update pueda examinar las actualizaciones que se crearon y publicaron con Updates Publisher. Para obtener más información sobre cómo habilitar esta opción de directiva de grupo, vea [Cómo configurar la directiva de grupo en los equipos cliente](/previous-versions/bb530967(v=technet.10)).



## <a name="configuring-group-policy-to-allow-wuaon-computers-to-scan-for-published-updates"></a>Configuración de directiva de grupo para permitir que el WUA de los equipos busque actualizaciones publicadas
Para que el Agente de Windows Update (WUA) de los equipos busque actualizaciones de software creadas y publicadas mediante Updates Publisher, se debe habilitar una configuración de la directiva que permita contenido firmado procedente de una ubicación del servicio Microsoft Update de la intranet. Si la configuración de directiva está habilitada, el WUA aceptará actualizaciones recibidas a través de una ubicación en la intranet si las actualizaciones de software están firmadas en el almacén de certificados **Editores de confianza** del equipo local. Hay varios métodos para configurar la directiva de grupo en equipos del entorno.

Para equipos que no están en el dominio, se puede configurar un valor de clave del Registro que permite contenido firmado desde una ubicación del servicio Microsoft Update de la intranet.

Los procedimientos siguientes indican los pasos básicos que pueden utilizarse para configurar la directiva de grupo de equipos del dominio y un valor de clave del Registro en equipos que no están en el dominio.

### <a name="to-configure-group-policy-to-allow-wua-to-scan-for-published-updates"></a>Configuración de directiva de grupo para permitir que el WUA busque actualizaciones publicadas
1.  Abra el complemento Editor de objetos de directiva de grupo de Microsoft Management Console (MMC) con un usuario que tenga derechos de seguridad apropiados para configurar la directiva de grupo.

2.  Haga clic en **Examinar** y seleccione el dominio, la UO o los GPO vinculados al sitio desde donde la directiva de grupo configurada se propagará a los equipos cliente que quiera. Haga clic en **Aceptar**, en **Finalizar**, en **Cerrar** y luego, en **Aceptar**.

3.  Expanda la configuración de directiva de grupo seleccionada en el árbol de la consola, **Configuración del equipo**, **Plantillas administrativas**, **Componentes de Windows** y luego, haga clic en **Windows Update**.

4.  En el panel de resultados, haga clic con el botón derecho en **Allow signed content from intranet Microsoft update service location** (Permitir contenido firmado de la ubicación del servicio Microsoft update de la intranet), haga clic en **Propiedades**, en **Habilitado** y luego, en **Aceptar**.