---
title: 'Configuración de Optimización de distribución para Windows 10 en Microsoft Intune: Azure | Microsoft Docs'
description: Configure cómo usan la Optimización de distribución los dispositivos Windows 10 que administra con Intune. En Intune, cree un perfil de configuración de dispositivos para instalar actualizaciones desde Internet. Vea también cómo reemplazar anillos de actualización existentes con un perfil de Optimización de distribución.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: kerimh
ms.openlocfilehash: 4d491a3210229d5dd6c74ccaed7f44c4ae4eb83c
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990060"
---
# <a name="delivery-optimization-settings-in-microsoft-intune"></a>Configuración de Optimización de distribución en Microsoft Intune

Con Intune, use la opción Optimización de distribución para los dispositivos Windows 10 con el fin de reducir el consumo de ancho de banda cuando estos dispositivos descarguen aplicaciones y actualizaciones. Configure la Optimización de distribución como parte de los perfiles de configuración de dispositivos.  

En este artículo se explica cómo configurar las opciones de Optimización de distribución como parte de un perfil de configuración de dispositivos. Después de crear un perfil, este se asigna o implementa en sus dispositivos Windows 10.

Para ver una lista de las opciones de Optimización de distribución que admite Intune, vea [Configuración de Optimización de distribución para Intune](delivery-optimization-settings.md).  

Para obtener más información sobre la opción Optimización de distribución en Windows 10, consulte [Actualizaciones de optimización de Windows 10 de distribución](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) en la documentación de Windows.  

## <a name="create-the-profile"></a>Creación del perfil

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.

3. Escriba las propiedades siguientes:

   - **Plataforma**: seleccione **Windows 10 y versiones posteriores**.
   - **Perfil**: seleccione **Optimización de distribución**.

4. Seleccione **Crear**.

5. En **Básico**, escriba las propiedades siguientes:

   - **Nombre**: escriba un nombre descriptivo para el nuevo perfil.
   - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional pero recomendada.

6. Seleccione **Siguiente**.

7. En la página **Opciones de configuración**, defina cómo quiere que se descarguen las actualizaciones y aplicaciones. Para obtener más información sobre las opciones disponibles, vea [Configuración de Optimización de distribución para Intune](delivery-optimization-settings.md).

   Cuando haya finalizado la configuración, seleccione **Siguiente**.

8. En la página **Ámbito (etiquetas)** , elija **Seleccionar etiquetas de ámbito** para abrir el panel *Seleccionar etiquetas* y asignar etiquetas de ámbito al perfil.
  
   Seleccione **Siguiente** para continuar.

9. En la página **Asignaciones**, seleccione los grupos que recibirán este perfil. Para obtener más información sobre la asignación de perfiles, vea [Asignación de perfiles de usuario y dispositivo](../configuration/device-profile-assign.md).

   Seleccione **Siguiente**.

10. En la página **Reglas de aplicabilidad**, use las opciones **Regla**, **Propiedad** y **Valor** para definir cómo se aplica este perfil dentro de los grupos asignados.

11. Cuando haya terminado, elija **Crear** en la página **Revisar y crear**. El perfil se crea y se muestra en la lista.

La próxima vez que se sincronice cada dispositivo, se aplica la directiva.

## <a name="remove-delivery-optimization-from-windows-10-update-rings"></a>Eliminación de la optimización de entrega de los anillos de actualización de Windows 10

Anteriormente, la optimización de entrega se configuraba como parte de los anillos de actualización de software. A partir de febrero de 2019, la configuración de la optimización de entrega se configura como parte de un perfil de configuración de dispositivo de optimización de entrega, que incluye opciones adicionales que afectan más que a la entrega de actualizaciones de software a los dispositivos. Si todavía no lo ha hecho, establezca *Sin configurar* para quitar la configuración de Optimización de distribución de los anillos de actualización y use un perfil de Optimización de distribución para administrar el mayor número de opciones disponibles.

1. Cree un perfil de configuración de dispositivos de optimización de distribución:

    1. En el Centro de administración de Microsoft Endpoint Manager, seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.
    2. Escriba las propiedades siguientes:

        - **Plataforma**: seleccione **Windows 10 y versiones posteriores**.
        - **Perfil**: seleccione **Optimización de distribución**.

    3. Seleccione **Crear**.
    4. En **Básico**, escriba las propiedades siguientes:

        - **Nombre**: escriba un nombre descriptivo para el nuevo perfil.
        - **Descripción**: escriba una descripción para el perfil. Esta configuración es opcional pero recomendada.

    5. Seleccione **Siguiente**.
    6. En **Opciones de configuración** > **Modo de descarga**, seleccione el mismo modo que usa el anillo de actualización de software existente, *a menos* que quiera cambiar la configuración que se aplica a los dispositivos. Las opciones son:

        - **No configurado**.
        - **HTTP solo, sin emparejamiento**
        - **HTTP combinado con el emparejamiento que se encuentra en la misma NAT**
        - **HTTP combinado con el emparejamiento de un grupo privado**
        - **HTTP combinado con emparejamiento de Internet**
        - **Modo de descarga sencillo sin emparejamiento**
        - **Modo de omisión**

    7. Configure [cualquier opción adicional](delivery-optimization-settings.md) que quiera administrar y siga creando el perfil.

        En **Asignaciones**, asigne este nuevo perfil a los mismos dispositivos y usuarios que el anillo de actualización de software existente. Para obtener más información, vea [Asignación del perfil](device-profile-assign.md).

2. Quite la configuración del círculo de actualizaciones de software existente:

    1. En el Centro de administración de Microsoft Endpoint Manager, vaya a **Actualizaciones de software** &gt; Anillos de actualización de Windows 10.
    2. En la lista, seleccione el círculo de actualizaciones.
    3. En la configuración, establezca **Modo de descarga de optimización de distribución** en **Sin configurar**.
    4. **Aceptar** > **Guardar** los cambios.

## <a name="next-steps"></a>Pasos siguientes

Después de [asignar el perfil](device-profile-assign.md), [supervise su estado](device-profile-monitor.md).

Vea la [Configuración de Optimización de distribución](delivery-optimization-settings.md) para Intune.
