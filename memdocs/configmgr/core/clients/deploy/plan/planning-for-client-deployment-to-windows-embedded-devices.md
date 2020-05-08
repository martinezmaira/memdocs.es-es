---
title: Planeamiento de implementación de clientes en dispositivos de Windows Embedded
titleSuffix: Configuration Manager
description: Planee la implementación de clientes en dispositivos de Windows Embedded en Configuration Manager.
ms.date: 06/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 038e61f9-f49d-41d1-9a9f-87bec9e00d5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7848e3c0c38391ab61d10ad46cbb772c812539c7
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906637"
---
# <a name="planning-for-client-deployment-to-windows-embedded-devices-in-configuration-manager"></a>Planeación de la implementación de clientes en dispositivos de Windows Embedded en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

<a name="BKMK_DeployClientEmbedded"></a> Si el dispositivo de Windows Embedded no incluye el cliente de Configuration Manager, puede usar cualquiera de los métodos de instalación de cliente si el dispositivo cumple con las dependencias necesarias. Si el dispositivo incrustado admite filtros de escritura, debe deshabilitar estos filtros antes de instalar el cliente, y volverlos a habilitar posteriormente una vez que el cliente esté instalado y asignado a un sitio.  

 Tenga en cuenta que, al deshabilitar los filtros, no debe deshabilitar los controladores de filtro. Normalmente, estos controladores se inician automáticamente cuando se inicia el equipo. La deshabilitación de los controladores impedirá la instalación del cliente o interferirá con la orquestación de filtros de escritura, con lo que se producirá un error en las operaciones del cliente. Estos son los servicios asociados a cada tipo de filtro de escritura que se deben seguir ejecutando:  

|Tipo de filtro de escritura|Controlador|Tipo|Descripción|  
|-----------------------|------------|----------|-----------------|  
|EWF|EWF|Kernel|Implementa una redirección de E/S de nivel de sector en los volúmenes protegidos.|  
|FBWF|FBWF|Sistema de archivos|Implementa una redirección de E/S de nivel de archivo en los volúmenes protegidos.|  
|UWF|uwfreg|Kernel|Redirector del registro UWF|  
|UWF|uwfs|Sistema de archivos|Redirector de archivos UWF|  
|UWF|uwfvol|Kernel|Administrador de volúmenes UWF|  

 Los filtros de escritura controlan el modo en que el dispositivo incrustado se actualiza al realizar cambios, por ejemplo, al instalar software. Cuando se habilitan los filtros de escritura, en lugar de hacer los cambios directamente en el sistema operativo, se redirigen estos cambios a una superposición temporal. Si los cambios solo se escriben en la superposición, se pierden cuando se apaga el dispositivo incrustado. No obstante, si los filtros de escritura están deshabilitados temporalmente, los cambios se pueden hacer permanentes para que no sea necesario volver a realizarlos (o volver a instalar el software) cada vez que se reinicie el dispositivo incrustado. No obstante, la deshabilitación temporal y la posterior habilitación de los filtros de escritura requiere uno o más reinicios, por lo que lo normal es que desee controlar cuándo se va a producir esto mediante la configuración de las ventanas de mantenimiento para que el reinicio se produzca fuera del horario comercial.  

 Es posible configurar opciones para deshabilitar y volver a habilitar automáticamente los filtros de escritura al implementar software como aplicaciones, secuencias de tareas, actualizaciones de software y el cliente de Endpoint Protection. La excepción a esto son las líneas de base de configuración con elementos de configuración que utilizan corrección automática. En este escenario, la corrección siempre se produce en la superposición para que esté disponible solo hasta que se reinicie el dispositivo. La corrección se vuelve a aplicar en el siguiente ciclo de evaluación, pero solo a la superposición, que está desactivada en el reinicio. Para forzar a Configuration Manager para que confirme los cambios de la corrección, es posible implementar la línea base de configuración y luego otra implementación de software que admita la confirmación del cambio tan pronto como sea posible.  

 Si los filtros de escritura están deshabilitados, es posible instalar software en dispositivos de Windows Embedded mediante el Centro de software. Pero si los filtros de escritura están habilitados, se produce un error en la instalación y Configuration Manager muestra un mensaje de error con permisos insuficientes para instalar la aplicación.  

> [!WARNING]  
>  Aunque no seleccione las opciones de Configuration Manager para confirmar los cambios, los cambios podrían confirmarse si se realiza alguna otra instalación de software o modificación que confirme los cambios. En este escenario, los cambios originales se confirman junto con los nuevos cambios.  

 Cuando Configuration Manager deshabilita los filtros de escritura para realizar cambios permanentes, solo los usuarios con derechos administrativos locales pueden iniciar sesión y usar el dispositivo incrustado. Durante este periodo, los usuarios con derechos reducidos quedan bloqueados y se muestra un mensaje indicando que el equipo no está disponible porque se están realizando tareas de mantenimiento. Esto ayuda a proteger el dispositivo cuando se encuentra en un estado en el que los cambios se pueden aplicar permanentemente, por lo que este comportamiento de bloqueo del modo de mantenimiento supone otra razón para configurar una ventana de mantenimiento en un momento en el que los usuarios no vayan a iniciar sesión en estos dispositivos.  

 Configuration Manager admite la administración de los siguientes tipos de filtros de escritura:  

- Filtro de escritura basado en archivo (FBWF): para obtener más información, vea [File-Based Write Filter (Filtro de escritura basado en archivo)](https://docs.microsoft.com/previous-versions/windows/embedded/aa940926(v=winembedded.5)) en MSDN.  

- RAM del filtro de escritura mejorado (EWF): para obtener más información, vea [Enhanced Write Filter (Filtro de escritura mejorado)](https://docs.microsoft.com/previous-versions/windows/embedded/ms912906(v=winembedded.5)).  

- Filtro de escritura unificado (UWF): para obtener más información, vea [Unified Write Filter (Filtro de escritura unificado)](https://docs.microsoft.com/windows-hardware/customize/enterprise/unified-write-filter).  

  Configuration Manager no admite las operaciones de filtro de escritura cuando el dispositivo de Windows Embedded está en modo EWF RAM Reg.  

> [!IMPORTANT]
>  Si tiene la opción, use filtros de escritura basados en archivo (FBWF) con Configuration Manager para una mayor eficiencia y una mayor escalabilidad.
> 
> **Solo para dispositivos que usen FBWF:** configure las siguientes excepciones para conservar el estado del cliente y los datos de inventario entre reinicios de dispositivo:  
> 
> - CCMINSTALLDIR\\\*.sdf  
>   -   CCMINSTALLDIR\ServiceData  
>   -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
> 
>   Los dispositivos que ejecutan Windows Embedded 8.0 y versiones posteriores no admiten las exclusiones que contienen caracteres comodín. En estos dispositivos, debe configurar las siguientes exclusiones de forma individual:  
> 
> - Todos los archivos de CCMINSTALLDIR con la extensión .sdf, normalmente:  
> 
>   -   UserAffinityStore.sdf  
>   -   InventoryStore.sdf  
>   -   CcmStore.sdf  
>   -   StateMessageStore.sdf  
>   -   CertEnrollmentStore.sdf  
>   -   CCMINSTALLDIR\ServiceData  
>   -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
> 
> **Solo para dispositivos que usen FBWF y UWF:** Cuando los clientes de un grupo de trabajo usan certificados para la autenticación en puntos de administración, también debe excluir la clave privada para asegurarse de que el cliente continúa comunicándose con el punto de administración. En estos dispositivos, configure las siguientes excepciones:  
> 
> - c:\Windows\System32\Microsoft\Protect  
>   -   c:\ProgramData\Microsoft\Crypto  
>   -   HKEY_LOCAL_MACHINE\Software\Microsoft\SystemCertificates\SMS\Certificates  

> [!NOTE]
> El cliente de Configuration Manager no necesita excepciones adicionales a las documentadas en el cuadro **Importante** anterior. La adición de excepciones adicionales relacionadas con Configuration Manager o WMI (WBEM) puede provocar errores de Configuration Manager, incluido el bloqueo de los dispositivos en el modo de mantenimiento o que experimenten bucles de reinicio. Las excepciones innecesarias incluyen el directorio de cliente de Configuration Manager, los directorios CCMcache y CCMSetup, el directorio de caché de la secuencia de tareas, el directorio WBEM y las claves del Registro relacionadas con Configuration Manager.

 Para obtener un ejemplo de cómo implementar y administrar dispositivos de Windows Embedded con el filtro de escritura habilitado en Configuration Manager, vea [Escenario de ejemplo para implementar y administrar clientes de Configuration Manager en dispositivos Windows Embedded](../../../../core/clients/deploy/example-scenario-for-deploying-and-managing-clients-on-windows-embedded-devices.md).  

 Para obtener más información acerca de la creación de imágenes para dispositivos de Windows Embedded y la configuración de filtros de escritura, consulte la documentación de Windows Embedded o póngase en contacto con el OEM.  

> [!NOTE]
>  Al seleccionar las plataformas aplicables para las implementaciones de software y los elementos de configuración, éstos muestran las familias de Windows Embedded en lugar de las versiones específicas. Utilice la lista siguiente para asignar la versión específica de Windows Embedded a las opciones del cuadro de lista:  
> 
> - **Sistemas operativos incrustados basados en Windows XP (32 bits)** incluye lo siguiente:  
> 
>   -   Windows XP Embedded  
>   -   Windows Embedded for Point of Service  
>   -   Windows Embedded Standard 2009  
>   -   Windows Embedded POSReady 2009  
>   -   **Sistemas operativos incrustados basados en Windows 7 (32 bits)** incluye lo siguiente:  
> 
>   -   Windows Embedded Standard 7 (32 bits)  
>   -   Windows Embedded POSReady 7 (32 bits)  
>   -   Windows ThinPC  
>   -   **Sistemas operativos incrustados basados en Windows 7 (64 bits)** incluye lo siguiente:  
> 
>   -   Windows Embedded Standard 7 (64 bits)  
>   -   Windows Embedded POSReady 7 (64 bits)
