---
title: Supervisión de la administración conjunta
titleSuffix: Configuration Manager
description: Utilice el panel de administración conjunta para revisar información sobre los dispositivos administrados conjuntamente.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e4516ca9baa7398322c204908c25248921a69d25
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268069"
---
# <a name="how-to-monitor-co-management-in-configuration-manager"></a>Supervisión de la administración conjunta en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Después de habilitar la administración conjunta, los dispositivos de administración conjunta se supervisan con los métodos siguientes:

- [Panel de administración conjunta](#co-management-dashboard)  

- [Directivas de implementación](#deployment-policies)

- [Datos del dispositivo de WMI](#wmi-device-data)

## <a name="co-management-dashboard"></a>Panel de administración conjunta

A partir de la versión 1802, vea un panel con información sobre la administración conjunta. El panel le ayudará a revisar los equipos que se administran conjuntamente en el entorno. Los gráficos ayudan a identificar los dispositivos que podrían requerir atención.<!--1356648-->

En la consola de Configuration Manager, vaya al área de trabajo **Supervisión** y haga clic en el nodo **Administración conjunta**.

A partir de la versión 1810, el panel de administración conjunta se ha mejorado con información más detallada. <!--1358980-->

![Captura de pantalla del panel de administración conjunta](media/co-management-dashboard.png)

### <a name="co-managed-devices"></a>Dispositivos administrados conjuntamente

*Se aplica a las versiones 1802 y 1806*

Muestra el porcentaje de dispositivos administrados conjuntamente en todo el entorno.

![Mosaico de dispositivos administrados conjuntamente](media/co-management-dashboard/Percent-Co-managed-graph.PNG)

### <a name="client-os-distribution"></a>Distribución del sistema operativo cliente

*Se aplica a todas las versiones* 

Muestra el número de dispositivos cliente en función del sistema operativo por versión. Se usan las siguientes agrupaciones:  

- Windows 7 y 8.x
- Windows 10 anterior a la versión 1709  
- Windows 10 1709 y versiones posteriores  

    > [!Tip]  
    > Windows 10, versión 1709 y versiones posteriores, es un requisito previo para la administración conjunta.  

Mantenga el puntero sobre una sección del gráfico para mostrar el porcentaje de dispositivos que forman parte de ese grupo de sistemas operativos.

![Mosaico de la distribución del sistema operativo cliente](media/co-management-dashboard/Co-management-OS-distribution-graph.PNG)

### <a name="co-management-status-donut"></a>Estado de la administración conjunta (anillo)

*Se aplica a las versiones 1802 y 1806*

Muestra el desglose de los dispositivos que se ejecutan correctamente o con error en las categorías siguientes:

- Se ejecuta correctamente, Unidos a Azure AD híbrido
- Se ejecuta correctamente, Unido a Azure AD  
- Error: Error de inscripción automática  

Mantenga el puntero sobre una sección del gráfico para ver el porcentaje de los dispositivos en esa categoría.

![Mosaico del estado de la administración conjunta (anillo)](media/co-management-dashboard/Co-management-status-graph.PNG)

Seleccione una sección del gráfico para ver la lista de dispositivos de esa categoría.

![Lista de dispositivos de error de inscripción](media/co-management-dashboard/Enrollment-Failure_Device-List.PNG)

### <a name="co-management-status-funnel"></a>Estado de la administración conjunta (embudo)

*Se aplica a la versión 1810 y posteriores*

Un gráfico de embudo que muestra el número de dispositivos con los siguientes estados del proceso de inscripción:
  
- Dispositivos aptos
- Programado  
- Inscripción iniciada  
- Inscritos  

![Mosaico del estado de la administración conjunta (embudo)](media/co-management-dashboard/1358980-status-funnel.png)

### <a name="co-management-enrollment-status"></a>Estado de la inscripción de administración conjunta

*Se aplica a la versión 1810 y posteriores*

Muestra un desglose del estado de los dispositivos en las categorías siguientes:

- Se ejecuta correctamente, unido a Azure AD híbrido  
- Se ejecuta correctamente, unido a Azure AD  
- Inscribiendo, unido a Azure AD híbrido  
- Error, unido a Azure AD híbrido  
- Error, unido a Azure AD  
- Inicio de sesión de usuario pendiente  

    > [!Note]  
    > A partir de la versión 1906, para disminuir el número de dispositivos con este estado pendiente, un dispositivo administrado conjuntamente nuevo ahora se inscribe automáticamente en el servicio de Microsoft Intune en función de su token de *dispositivo* de Azure AD. No es necesario esperar a que un usuario inicie sesión en el dispositivo para iniciar la inscripción automática. Para admitir este comportamiento, el dispositivo debe ejecutar Windows 10, versión 1803 o posterior.
    >
    > Si se produce un error en el token del dispositivo, recurre al comportamiento anterior con el token de usuario. Busque en **ComanagementHandler.log** la entrada siguiente: `Enrolling device with RegisterDeviceWithManagementUsingAADDeviceCredentials`

Seleccione un estado del icono para explorar en profundidad una lista de dispositivos de ese estado.  

![Mosaico del estado de la inscripción de administración conjunta](media/co-management-dashboard/1358980-enrollment-status.png)


### <a name="workload-transition"></a>Transición de la carga de trabajo

*Se aplica a todas las versiones*

Muestra un gráfico de barras con el número de dispositivos que se han pasado a Microsoft Intune para las cargas de trabajo disponibles.

La lista de las cargas de trabajo varía según la versión de Configuration Manager. Para obtener más información, vea [Cargas de trabajo que se pueden pasar a Intune](workloads.md).

Mantenga el puntero sobre una sección del gráfico para ver el número de dispositivos que se ha pasado para la carga de trabajo. 

![Gráfico de barras de la transición de la carga de trabajo](media/co-management-dashboard/Workload-Transition.PNG)


### <a name="enrollment-errors"></a>Errores de inscripción

*Se aplica a la versión 1810 y posteriores*

Esta tabla es una lista de errores de inscripción de dispositivos. Estos errores pueden proceder del componente MDM en Windows, el SO principal de Windows o el cliente de Configuration Manager.

Existen cientos de posibles errores. La tabla siguiente incluye los errores más comunes.
<!-- SCCMDocs issue 1064, BUG 3158555 -->

| Error | Descripción |
|---------|---------|
| 2147549183 (0x8000FFFF) | La inscripción de MDM no se ha configurado todavía en Azure AD, o la dirección URL de inscripción no se espera.<br><br>[Habilitar la inscripción automática de Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) |
| 2149056536 (0x80180018)<br>MENROLL_E_USERLICENSE | La licencia del usuario está en mal estado, bloqueando la inscripción<br><br>[Asignar licencias a usuarios](https://docs.microsoft.com/intune/licenses-assign) |
| 2149056555 (0x8018002B)<br>MENROLL_E_MDM_NOT_CONFIGURED | Al intentar inscribirse automáticamente en Intune, la configuración de Azure AD no se aplica completamente. Este problema debe de ser transitorio, ya que el dispositivo reintenta la operación después de un breve período de tiempo. |
| 2149056554 (0x‭8018002A‬)<br>&nbsp; | El usuario canceló la operación<br><br>Si la inscripción de MDM requiere autenticación multifactor y el usuario no ha iniciado sesión con un segundo factor compatible, Windows muestra una notificación del sistema al usuario que se va a inscribir. Este error se produce si el usuario no responde a la notificación del sistema. Este problema debería ser transitorio, dado que Configuration Manager volverá a intentarlo y le preguntará al usuario. Los usuarios deben usar la autenticación multifactor cuando inicien sesión en Windows. Indíqueles también que este comportamiento es esperado y que, si se les pide, deben tomar medidas. | 
| 2149056533 (0x80180015)<br>MENROLL_E_NOTSUPPORTED | Por lo general, no se admite la administración de dispositivos móviles | 
| 2149056514 (0x80180002)<br>MENROLL_E_DEVICE_AUTHENTICATION_ERROR | El servidor no pudo autenticar el usuario<br><br> No hay ningún token de Azure AD para el usuario. Asegúrese de que el usuario se pueda autenticar en Azure AD. |
| 2147942450 (0x‭80070032‬)<br>&nbsp; | La inscripción automática de MDM solo se admite en Windows RS3 y versiones superiores.<br><br>Asegúrese de que el dispositivo cumple con los [requisitos mínimos](overview.md#windows-10) para la administración conjunta. |
| 3400073293 | Respuesta de cuenta de dominio de usuario de ADAL desconocida<br><br>Revise la configuración de Azure AD y asegúrese de que los usuarios se puedan autenticar correctamente. | 
| 3399548929 | Es necesario el inicio de sesión del usuario<br><br>Este problema debería ser transitorio. Se produce cuando el usuario cierra rápidamente la sesión antes de que se realice la tarea de inscripción. | 
| 3400073236 | Error de solicitud del token de seguridad de ADAL.<br><br>Revise la configuración de Azure AD y asegúrese de que los usuarios se puedan autenticar correctamente. |
| 2149122477 | Problema de HTTP genérico |
| 3400073247 | La autenticación de Windows integrada de ADAL solo se admite en el flujo federado<br><br>[Planeamiento de la implementación de la unión a Azure Active Directory híbrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) | 
| 3399942148 | No se encontró el servidor ni el proxy.<br><br>Este problema debería ser transitorio cuando el cliente no se pueda comunicar con la nube. Si persiste, asegúrese de que el cliente tiene conectividad coherente con Azure. | 
| 2149056532 | No se admite la plataforma o versión específica<br><br>Asegúrese de que el dispositivo cumple con los [requisitos mínimos](overview.md#windows-10) para la administración conjunta. |
| 2147943568 | No se encontró el elemento<br><br>Este problema debería ser transitorio. Si persiste, póngase en contacto con Soporte técnico de Microsoft. |
| 2192179208 | No hay recursos de memoria suficientes disponibles para procesar este comando.<br><br>Este problema debería ser transitorio y se debería resolver solo cuando el cliente vuelva a intentar la operación. |
| 3399614467 | Error de concesión de autorización de ADAL para esta aserción<br><br>Revise la configuración de Azure AD y asegúrese de que los usuarios se puedan autenticar correctamente. |
| 2149056517 | Error genérico del servidor de administración, como un error de acceso de DB<br><br>Este problema debería ser transitorio. Si persiste, póngase en contacto con Soporte técnico de Microsoft. |
| 2149134055 | No se puede resolver el nombre de WinHTTP<br><br>El cliente no puede resolver el nombre del servicio. Compruebe la configuración DNS. | 
| 2149134050 | Tiempo de espera de Internet<br><br>Este problema debería ser transitorio cuando el cliente no se pueda comunicar con la nube. Si persiste, asegúrese de que el cliente tiene conectividad coherente con Azure. |

Para más información, consulte [MDM Registration Error Values](https://docs.microsoft.com/windows/desktop/mdmreg/mdm-registration-constants) (Valores de error de registro de MDM).

## <a name="deployment-policies"></a>Directivas de implementación

en el nodo **Implementaciones** del área de trabajo **Supervisión** se crean dos directivas. Una es para el grupo piloto y otra para producción. Estas directivas solo informan del número de dispositivos donde Configuration Manager ha aplicado la directiva. No tienen en cuenta cuántos están inscritos en Intune, que es un requisito antes de que los dispositivos se puedan administrar conjuntamente.  

La directiva de producción (CoMgmtSettingsProd) está destinada a la colección **Todos los sistemas**. Tiene una condición de aplicabilidad que comprueba la versión y el tipo de sistema operativo. Si el cliente es un sistema operativo de servidor o no es Windows 10, la directiva no se aplica y, por tanto, no se realiza ninguna acción.

## <a name="wmi-device-data"></a>Datos del dispositivo de WMI

Consulte la clase WMI **SMS_Client_ComanagementState** en el espacio de nombres **ROOT\SMS\site_&lt;CÓDIGO DE SITIO>** en el servidor de sitio. Puede crear recopilaciones personalizadas en Configuration Manager, lo que ayudará a determinar el estado de la implementación de administración conjunta. Para más información sobre cómo crear recopilaciones personalizadas, consulte [Cómo crear recopilaciones](../core/clients/manage/collections/create-collections.md).

Los campos siguientes están disponibles en la clase WMI:  

- **MachineId**: especifica un identificador de dispositivo único para el cliente de Configuration Manager.  

- **MDMEnrolled**: especifica si el dispositivo está inscrito en MDM.  

- **Authority**: la entidad para la que el dispositivo está inscrito.  

- **ComgmtPolicyPresent**: especifica si la directiva de administración conjunta de Configuration Manager existe en el cliente. Si el valor de **MDMEnrolled** es **0**, el dispositivo no se administra conjuntamente con independencia de si la directiva de administración conjunta existe en el cliente.  

Un dispositivo se administra conjuntamente cuando los campos **MDMEnrolled** y **ComgmtPolicyPresent** tienen un valor de **1**.  
