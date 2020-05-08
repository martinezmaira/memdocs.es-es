---
title: 'Configuración de Optimización de distribución para Windows 10 en Microsoft Intune: Azure | Microsoft Docs'
description: Configure cómo los dispositivos Windows 10 usan la opción Optimización de distribución que administra con Intune. En Intune, cree un perfil de configuración de dispositivos para instalar actualizaciones desde Internet. Consulte también cómo reemplazar los círculos de actualizaciones existentes con un perfil de Optimización de distribución.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: kerimh
ms.openlocfilehash: c37563dee40d776d352dec4e0b8ef11b1dc8f67b
ms.sourcegitcommit: 7b3eed763b394075766ea080968889a8538bfe56
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/29/2020
ms.locfileid: "82506546"
---
# <a name="delivery-optimization-settings-in-microsoft-intune"></a>Configuración de la opción Optimización de distribución en Microsoft Intune

Con Intune, use la opción Optimización de distribución para los dispositivos Windows 10 con el fin de reducir el consumo de ancho de banda cuando estos dispositivos descarguen aplicaciones y actualizaciones. Configure la optimización de distribución como parte de los perfiles de configuración del dispositivo.  

En este artículo se describe cómo configurar las opciones de optimización de distribución como parte de un perfil de configuración de dispositivo. Después de crear un perfil, este se asigna o implementa en sus dispositivos Windows 10.

Para ver una lista de las opciones de optimización de distribución que admite Intune, consulte [Configuración de optimización de entrega para Intune](delivery-optimization-settings.md).  

Para obtener más información sobre la opción Optimización de distribución en Windows 10, consulte [Actualizaciones de optimización de Windows 10 de distribución](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) en la documentación de Windows.  

## <a name="create-the-profile"></a>Creación del perfil

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.

3. Escriba las propiedades siguientes:
   - **Plataforma**: seleccione **Windows 10 y versiones posteriores**.
   - **Tipo de perfil**: seleccione **Optimización de distribución**.

4. Seleccione **Crear**.

5. En la página **Datos básicos**, escriba un nombre y una descripción para el perfil y, después, elija **Siguiente**.

6. En la página **Opciones de configuración**, defina cómo quiere que se descarguen las actualizaciones y aplicaciones. Para obtener más información sobre las opciones de configuración disponibles, consulte [Delivery optimization settings for Intune](delivery-optimization-settings.md) (Configuración de la opción Optimización de distribución de Intune).

   Cuando haya finalizado la configuración, seleccione **Siguiente**.

7. En la página **Ámbito (etiquetas)** , elija **Seleccionar etiquetas de ámbito** para abrir el panel *Seleccionar etiquetas* y asignar etiquetas de ámbito al perfil.
  
   Seleccione **Siguiente** para continuar.

8. En la página **Asignaciones**, seleccione los grupos que recibirán este perfil. Para obtener más información sobre la asignación de perfiles, vea [Asignación de perfiles de usuario y dispositivo](../configuration/device-profile-assign.md).

   Seleccione **Siguiente**.

9. En la página **Reglas de aplicabilidad**, use las opciones **Regla**, **Propiedad** y **Valor** para definir cómo se aplica este perfil dentro de los grupos asignados.

10. Cuando haya terminado, elija **Crear** en la página **Revisar y crear**. El perfil se crea y se muestra en la lista. Después, [asigne el perfil](device-profile-assign.md) y [supervise su estado](device-profile-monitor.md).

## <a name="remove-delivery-optimization-from-windows-10-update-rings"></a>Eliminación de la optimización de entrega de los anillos de actualización de Windows 10

Anteriormente, la optimización de entrega se configuraba como parte de los anillos de actualización de software. A partir de febrero de 2019, la configuración de la optimización de entrega se configura como parte de un perfil de configuración de dispositivo de optimización de entrega, que incluye opciones adicionales que afectan más que a la entrega de actualizaciones de software a los dispositivos. Si todavía no lo ha hecho, establezca *No configurado* para quitar la configuración de optimización de entrega de los Anillos de actualización y, después, use un perfil de Optimización de distribución para administrar el mayor número de opciones disponibles.

1. Cree un perfil de configuración de dispositivos de optimización de distribución:

    1. En el Centro de administración de Microsoft Endpoint Manager, seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.
    2. Escriba las propiedades siguientes:

        - **Nombre**: escriba un nombre descriptivo para el nuevo perfil.
        - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional pero recomendada.
        - **Plataforma**: seleccione **Windows 10 y versiones posteriores**.
        - **Tipo de perfil**: seleccione **Optimización de distribución**.
        - **Configuración**: para **Modo de descarga de Optimización de entrega**, elija el mismo modo que usa el anillo de actualización de software existente, a menos que quiera cambiar la configuración que se aplica a los dispositivos. Las opciones son:
            - **No configurado**.
            - **HTTP solo, sin emparejamiento**
            - **HTTP combinado con el emparejamiento que se encuentra en la misma NAT** 
            - **HTTP combinado con el emparejamiento de un grupo privado**
            - **HTTP combinado con emparejamiento de Internet**
            - **Modo de descarga sencillo sin emparejamiento**
            - **Modo de omisión**
    3. Configure las opciones adicionales que pueda querer administrar.

2. Asigne este perfil nuevo a los mismos dispositivos y usuarios que el círculo de actualizaciones de software existente. [Asignar el perfil](device-profile-assign.md) muestra los pasos.

3. Quite la configuración del círculo de actualizaciones de software existente:
    1. En el Centro de administración de Microsoft Endpoint Manager, vaya a **Actualizaciones de software** &gt; Anillos de actualización de Windows 10.
    2. En la lista, seleccione el círculo de actualizaciones.
    3. En la configuración, establezca **Modo de descarga de optimización de distribución** en **No configurado**.
    4. **Aceptar** > **Guardar** los cambios.

## <a name="next-steps"></a>Pasos siguientes

[Asigne el perfil](device-profile-assign.md) y [supervise el estado](device-profile-monitor.md) el estado.  
Consulte la [configuración de la optimización de distribución](delivery-optimization-settings.md) para Intune.
