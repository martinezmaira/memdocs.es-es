---
title: 'Configurar opciones de Endpoint Protection en Microsoft Intune: Azure | Microsoft Docs'
description: Cree la configuración de Endpoint Protection al crear un perfil de dispositivo de macOS o Windows 10 en Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: karthib
ms.openlocfilehash: 4071614c7cb93194eef00f49aa2e1759ba1028f6
ms.sourcegitcommit: 7687cf8fdecd225216f58b8113ad07a24e43d4a3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2020
ms.locfileid: "80359253"
---
# <a name="add-endpoint-protection-settings-in-intune"></a>Agregar la configuración de Endpoint Protection en Intune

Con Intune, puede usar perfiles de configuración de dispositivos para administrar características de seguridad de protección de puntos de conexión comunes en los dispositivos, incluidos:

- Firewall
- BitLocker
- Permitir o bloquear aplicaciones
- Microsoft Defender y cifrado

Por ejemplo, puede crear un perfil de Endpoint Protection que solo permita a los usuarios de macOS instalar aplicaciones desde Mac App Store. O bien, que habilite Windows SmartScreen al ejecutar aplicaciones en dispositivos de Windows 10.

Antes de crear un perfil, revise estos artículos que detallan la configuración de la protección de puntos de conexión que Intune puede administrar para cada plataforma compatible:

- [Configuración de macOS](endpoint-protection-macos.md)
- [Configuración de Windows 10](endpoint-protection-windows-10.md)

## <a name="create-a-device-profile-containing-endpoint-protection-settings"></a>Crear un perfil de dispositivo que contenga la configuración de Endpoint Protection

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.

3. Escriba las propiedades siguientes:

    - **Plataforma**: seleccione la plataforma de los dispositivos. Las opciones son:

        - **macOS**
        - **Windows 10 y versiones posteriores**

    - **Perfil**: seleccione **Endpoint Protection**.

4. Seleccione **Crear**.
5. En **Básico**, escriba las propiedades siguientes:

    - **Nombre**: escriba un nombre descriptivo para la directiva. Asígnele un nombre a las directivas para que pueda identificarlas de manera sencilla más adelante. Por ejemplo, un nombre de directiva válido es **macOS: perfil de Endpoint Protection que configura el firewall para todos los dispositivos macOS**.
    - **Descripción**: escriba una descripción para la directiva. Esta configuración es opcional pero recomendada.

6. Seleccione **Siguiente**.

7. En **Opciones de configuración**, las opciones que puede configurar serán diferentes, según la plataforma que haya elegido. Elija la plataforma para la configuración detallada:

   - [Configuración de macOS](endpoint-protection-macos.md)
   - [Configuración de Windows 10](endpoint-protection-windows-10.md)

8. Seleccione **Siguiente**.
9. En **Etiquetas de ámbito** (opcional), asigne una etiqueta para filtrar el perfil por grupos de TI específicos, como `US-NC IT Team` o `JohnGlenn_ITDepartment`. Para obtener más información sobre las etiquetas de ámbito, vea [Usar control de acceso basado en rol (RBAC) y etiquetas de ámbito](../fundamentals/scope-tags.md).

    Seleccione **Siguiente**.

10. En **Asignaciones**, seleccione los usuarios o grupos que van a recibir el perfil. Para obtener más información sobre la asignación de perfiles, vea [Asignación de perfiles de usuario y dispositivo](../configuration/device-profile-assign.md).

    Seleccione **Siguiente**.

11. En **Revisar y crear**, revise la configuración. Si selecciona **Crear**, se guardan los cambios y se asigna el perfil. La directiva también se muestra en la lista de perfiles.

## <a name="add-custom-firewall-rules-for-windows-10-devices"></a>Adición de reglas de firewall personalizadas para dispositivos Windows 10

Cuando se configura el firewall de Microsoft Defender como parte de un perfil que incluye reglas de protección de punto de conexión para Windows 10, se pueden configurar reglas personalizadas para los firewalls. Las reglas personalizadas permiten expandir el conjunto predefinido de reglas de firewall compatibles con Windows 10.

Cuando planee perfiles con reglas de firewall personalizadas, tenga en cuenta la siguiente información, que podría afectar a la forma en que se elige agrupar las reglas de firewall en los perfiles:

- Cada perfil admite hasta 150 reglas de firewall. Si usa más de 150 reglas, cree perfiles adicionales, cada uno de ellos limitado a 150 reglas.

- En cada perfil, si se produce un error en una sola regla, se producirá un error en todas las reglas de ese perfil y no se aplicará ninguna al dispositivo.

- Cuando se produce un error en una regla, todas las reglas del perfil se notifican como erróneas. Intune no puede identificar la regla en concreto que ha producido el error.  

Las reglas de firewall que Intune puede administrar se detallan en el [proveedor del servicio de configuración (CSP) de firewall](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) de Windows. Para revisar la lista de configuraciones de firewall personalizadas para dispositivos Windows 10 compatibles con Intune, consulte [Reglas de firewall personalizadas](endpoint-protection-windows-10.md#firewall-rules).

### <a name="to-add-custom-firewall-rules-to-an-endpoint-protection-profile"></a>Adición de reglas de firewall personalizadas a un perfil de protección de punto de conexión

1. Inicie sesión en el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Dispositivos** > **Perfiles de configuración** > **Crear perfil**.

3. En *Plataforma*, seleccione **Windows 10 y versiones posteriores** y, luego, en *Perfil* seleccione **Endpoint Protection**.

    Seleccione **Crear**.

4. Escriba un **Nombre** para el perfil > **Siguiente**.
5. En **Opciones de configuración**, seleccione **Firewall de Microsoft Defender**. En *Reglas de firewall*, seleccione **Agregar** para abrir la página **Crear regla**.

6. Especifique la configuración de la regla de firewall y luego seleccione **Aceptar** para guardarla. Para revisar las opciones de reglas de firewall personalizadas disponibles en la documentación, consulte [Reglas de firewall personalizadas](endpoint-protection-windows-10.md#firewall-rules).

    1. La regla aparece en la página *Firewall de Microsoft Defender* de la lista de reglas.
    2. Para modificar una regla, seleccione la regla de la lista para abrir la página **Editar regla**.
    3. Para eliminar una regla de un perfil, seleccione los puntos suspensivos **(...)** de la regla y, luego, seleccione **Eliminar**.
    4. Para cambiar el orden en que se muestran las reglas, seleccione el icono de *flecha arriba, flecha abajo* en la parte superior de la lista de reglas.

7. Seleccione **Siguiente** hasta llegar a **Revisar y crear**. Si selecciona **Crear**, se guardan los cambios y se asigna el perfil. La directiva también se muestra en la lista de perfiles.

## <a name="next-steps"></a>Pasos siguientes

El perfil se crea, pero puede que todavía no haga nada. Después, [asigne el perfil](../configuration/device-profile-assign.md) y [supervise el estado](../configuration/device-profile-monitor.md).
