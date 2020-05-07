---
title: Definiciones de malware de Endpoint Protection desde WSUS
titleSuffix: Configuration Manager
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
author: mestew
ms.author: mstewart
description: Obtenga información sobre cómo configurar Windows Server Updates Services para aprobar automáticamente actualizaciones de definiciones.
manager: dougeby
ms.openlocfilehash: 235caff52b877177b92792bf8d9fb3a2007127a5
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126023"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-wsus-for-configuration-manager"></a>Habilitación de la descarga de definiciones de malware de Endpoint Protection desde WSUS para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Si usa WSUS para mantener actualizadas las definiciones de antimalware, puede configurarlo para aprobar automáticamente las actualizaciones de definiciones. Aunque el uso de las actualizaciones de software de Configuration Manager es el método recomendado para mantener actualizadas las definiciones, también se puede configurar WSUS como método que permita a los usuarios actualizar las definiciones de forma manual. Use los procedimientos siguientes para configurar WSUS como un origen de actualización de definiciones.

## <a name="synchronize-definition-updates-for-configuration-manager"></a>Sincronización de actualizaciones de definiciones para Configuration Manager

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda el nodo **Configuración del sitio** y, después, seleccione **Sitios**.

1. Seleccione el sitio que contiene el punto de actualización de software. En el grupo **Configuración** de la cinta, seleccione **Configurar componentes de sitio** y después **Punto de distribución de software**.

1. En la ventana **Propiedades de componente de punto de actualización de software**, cambie a la pestaña **Clasificaciones**. Seleccione **Actualizaciones de definiciones**.

1. Para especificar los **Productos** actualizados con WSUS, cambie a la pestaña **Productos**.

    - Para Windows 10 y versiones posteriores: En Microsoft > Windows, seleccione **Windows Defender**.

    - Para Windows 8.1 y versiones anteriores: En Microsoft > Forefront, seleccione **System Center Endpoint Protection**.

1. Seleccione **Aceptar** para cerrar la ventana **Propiedades de componente de punto de actualización de software**.

## <a name="synchronize-definition-updates-for-standalone-wsus"></a>Sincronización de actualizaciones de definiciones para WSUS independiente

Siga el procedimiento que hay a continuación para configurar las actualizaciones de Endpoint Protection si el servidor de WSUS no está integrado en el entorno de Configuration Manager.

1. En la consola de administración de WSUS, expanda **Equipos**, seleccione **Opciones** y luego **Productos y clasificaciones**.

1. Para especificar los **productos** actualizados con WSUS, cambie a la pestaña **Productos**.

    - Para Windows 10 y versiones posteriores: En Microsoft > Windows, seleccione **Windows Defender**.

    - Para Windows 8.1 y versiones anteriores: En Microsoft > Forefront, seleccione **System Center Endpoint Protection**.

1. Cambie a la pestaña **Clasificaciones**. Seleccione **Actualizaciones de definiciones** y **Actualizaciones**.

## <a name="approve-definition-updates"></a>Aprobación de actualizaciones de definiciones

Las actualizaciones de definiciones de Endpoint Protection se deben aprobar y descargar en el servidor WSUS para que se puedan ofrecer a los clientes que solicitan la lista de actualizaciones disponibles. Los clientes se conectan al servidor de WSUS para buscar las actualizaciones correspondientes y luego solicitan las últimas actualizaciones de definiciones aprobadas.

### <a name="approve-definitions-and-updates-in-wsus"></a>Aprobación de definiciones y actualizaciones en WSUS

1. En la Consola de administración de WSUS, seleccione **Actualizaciones**. Después, seleccione **Todas las actualizaciones** o la clasificación de las actualizaciones que quiera aprobar.

1. En la lista de actualizaciones, haga clic con el botón derecho en la actualización o las actualizaciones que quiere aprobar para la instalación y, después, seleccione **Aprobar**.

1. En la ventana **Aprobar actualizaciones**, seleccione el grupo de equipos para los que quiere aprobar las actualizaciones y después **Aprobada para su instalación**.

### <a name="configure-an-automatic-approval-rule"></a>Configuración de una regla de aprobación automática

También puede establecer una regla de aprobación automática para las actualizaciones de definiciones y las de Endpoint Protection. Esta acción configura WSUS para que apruebe de forma automática las actualizaciones de definiciones de Endpoint Protection descargadas por WSUS.

1. En la consola de administración de WSUS, seleccione **Opciones** y después **Aprobaciones automáticas**.

1. En la pestaña **Reglas de actualización**, seleccione **Nueva regla**.

1. En la ventana **Agregar regla**, en **Paso 1: Seleccionar las propiedades**, seleccione la opción: **Cuando una actualización está en una clasificación específica**.

    1. En el **Paso 2: Editar las propiedades**, haga clic en **cualquier clasificación**.

    1. Borre todas las opciones excepto **Actualizaciones de definiciones** y, después, seleccione **Aceptar**.

1. En la ventana **Agregar regla**, en **Paso 1: Seleccionar las propiedades**, seleccione la opción: **Cuando una actualización está en un producto específico**.

    1. En el **Paso 2: Editar las propiedades**, seleccione **cualquier producto**.

    1. Borre todas las opciones excepto **System Center Endpoint Protection** para Windows 8.1 y versiones anteriores, o bien **Windows Defender** para Windows 10 y versiones posteriores. Luego, seleccione **Aceptar**.

1. En el **Paso 3: Especificar un nombre**, escriba un nombre para la regla y, después, seleccione **Aceptar**.

1. En el cuadro de diálogo **Aprobaciones automáticas**, seleccione la regla recién creada y luego **Ejecutar regla**.

> [!NOTE]
> Para maximizar el rendimiento en los equipos cliente y el servidor de WSUS, rechace las actualizaciones de definiciones anteriores. Para ello, puede configurar la aprobación automática de las revisiones y el rechazo automático de las actualizaciones expiradas. Para obtener más información, vea [el artículo de Soporte técnico de Microsoft 938947](https://support.microsoft.com/kb/938947).

> [!div class="nextstepaction"]
> [Creación e implementación de directivas antimalware](endpoint-antimalware-policies.md)
