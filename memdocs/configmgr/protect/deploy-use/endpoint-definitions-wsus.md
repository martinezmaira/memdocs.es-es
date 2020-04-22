---
title: Definiciones de malware de Endpoint Protection desde WSUS
titleSuffix: Configuration Manager
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
author: mestew
ms.author: mstewart
description: Obtenga información sobre cómo configurar Windows Server Updates Services para aprobar automáticamente actualizaciones de definiciones.
manager: dougeby
ms.openlocfilehash: 301a3f318e836f2501a25ae65ebb61173b8e6231
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697213"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-windows-server-update-services-wsus-for-configuration-manager"></a>Habilite la descarga de definiciones de malware de Endpoint Protection desde Windows Server Update Services (WSUS) para Configuration Manager.

*Se aplica a: Configuration Manager (rama actual)*

 Si usa WSUS para mantener actualizadas las definiciones de antimalware, puede configurarlo para aprobar automáticamente las actualizaciones de definiciones. Si bien el uso de las actualizaciones de software de Configuration Manager es el método recomendado para mantener actualizadas las definiciones, también se puede configurar WSUS como método que permita a los usuarios iniciar manualmente la actualización de definiciones. Use los procedimientos siguientes para configurar WSUS como un origen de actualización de definiciones.

## <a name="to-synchronize-endpoint-protection-definition-updates-in-configuration-manager-software-updates"></a>Para sincronizar las actualizaciones de definiciones de Endpoint Protection en las actualizaciones de software de Configuration Manager

1. En la consola de Configuration Manager, haga clic en **Administración**.

2. En el área de trabajo **Administración** , expanda **Configuración del sitio**y, a continuación, haga clic en **Sitios**.

3. Seleccione el sitio que contiene el punto de actualización de software. En el grupo **Configuración** , haga clic en **Configurar componentes de sitio**y luego haga clic en **Punto de actualización de software**.

4. En la pestaña **Clasificaciones** del cuadro de diálogo **Propiedades de componente de punto de actualización de software** , active la casilla **Actualizaciones de definiciones** .

5. Especifique los **productos** que se actualizan con WSUS:

   -   Para Windows 8.1 y versiones anteriores, en la pestaña **Productos** del cuadro de diálogo **Propiedades de componente de punto de actualización de software** , active la casilla **Forefront Endpoint Protection 2010** .

   -   Para Windows 10 y versiones posteriores, en la pestaña **Productos** del cuadro de diálogo **Propiedades de componente de punto de actualización de software**, seleccione la casilla **Windows Defender**.

6. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Propiedades de componente de punto de actualización de software** .

   Use el procedimiento siguiente para configurar las actualizaciones de Endpoint Protection si el servidor de WSUS no está integrado en su entorno de Configuration Manager.

## <a name="to-synchronize-endpoint-protection-definition-updates-in-standalone-wsus"></a>Para sincronizar las actualizaciones de definiciones de Endpoint Protection en WSUS independiente

1.  En la consola de administración de WSUS, expanda **Equipos**, haga clic en **Opciones**y luego haga clic en **Productos y clasificaciones**.

2.  Especifique los **productos** que se actualizan con WSUS:

    -   Para Windows 8.1 y versiones anteriores, en la pestaña **Productos** del cuadro de diálogo **Propiedades de componente de punto de actualización de software** , active la casilla **Forefront Endpoint Protection 2010** .

    -   Para Windows 10 y versiones posteriores, en la pestaña **Productos** del cuadro de diálogo **Propiedades de componente de punto de actualización de software**, seleccione la casilla **Windows Defender**.

3.  En la pestaña **Clasificaciones** del cuadro de diálogo **Productos y clasificaciones** , active las casillas **Actualizaciones de definiciones** y **Actualizaciones** .

## <a name="approving-definition-updates"></a>Aprobar actualizaciones de definiciones
 Las actualizaciones de definiciones de Endpoint Protection se deben aprobar y descargar en el servidor de WSUS para que se puedan ofrecer a los clientes que solicitan la lista de actualizaciones disponibles. Los clientes se conectan al servidor de WSUS para buscar las actualizaciones correspondientes y luego solicitan las últimas actualizaciones de definiciones aprobadas.

### <a name="to-approve-definitions-and-updates-in-wsus"></a>Para aprobar definiciones y actualizaciones en WSUS

1. En la consola de administración de WSUS, haga clic en **Actualizaciones**y luego en **Todas las actualizaciones** o en la clasificación de actualizaciones que quiere aprobar.

2. En la lista de actualizaciones, haga clic con el botón derecho en la actualización o las actualizaciones que quiere aprobar para su instalación y luego haga clic en **Aprobar**.

3. En el cuadro de diálogo **Aprobar actualizaciones** , seleccione el grupo de equipos para los que quiere aprobar las actualizaciones y después haga clic en **Aprobada para su instalación**.

   Además de la aprobación manual, también puede establecer una regla de aprobación automática tanto para las actualizaciones de definiciones como para las actualizaciones de Endpoint Protection. Esta regla va a configurar WSUS para que apruebe automáticamente las actualizaciones de definiciones de Endpoint Protection descargadas por WSUS.

### <a name="to-configure-an-automatic-approval-rule"></a>Para configurar una regla de aprobación automática

1.  En la consola de administración de WSUS, haga clic en **Opciones**y en **Aprobaciones automáticas**.

2.  En la pestaña **Reglas de actualización** , haga clic en **Nueva regla**.

3.  En el cuadro de diálogo **Agregar regla**, en el **Paso 1: seleccionar propiedades**, active la casilla **Cuando una actualización está en una clasificación específica**.

4.  En el **Paso 2: editar las propiedades**, haga clic en **cualquier clasificación**.

5.  Desactive todas las casillas excepto **Actualizaciones de definiciones**y haga clic en **Aceptar**.

6.  En el cuadro de diálogo **Agregar regla**, en el **Paso 1: seleccionar propiedades**, active la casilla **Cuando una actualización está en un producto específico**.

7.  En el **Paso 2: editar las propiedades**, haga clic en **cualquier producto**.

8.  Desactive todas las casillas excepto **Forefront Endpoint Protection** para Windows 8.1 y versiones anteriores o **Windows Defender** para Windows 10 y versiones posteriores y luego haga clic en **Aceptar**.

9. En el **Paso 3: especificar un nombre**, escriba un nombre para la regla y haga clic en **Aceptar**.

10. En el cuadro de diálogo **Aprobaciones automáticas** , active la casilla de la regla creada recientemente y luego haga clic en **Ejecutar regla**.

> [!NOTE]
>  Para maximizar el rendimiento en los equipos cliente y el servidor de WSUS, rechace las actualizaciones de definiciones anteriores. Para ello, puede configurar la aprobación automática de las revisiones y el rechazo automático de las actualizaciones expiradas. Para obtener más información, vea el [artículo de Microsoft Knowledge Base 938947](https://go.microsoft.com/fwlink/p/?LinkId=204078).
> 
> [!div class="button"]
> [Paso siguiente >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Atrás >](endpoint-configure-alerts.md)
