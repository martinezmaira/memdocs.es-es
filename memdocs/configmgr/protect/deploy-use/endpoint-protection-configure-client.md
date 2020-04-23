---
title: Configuración del cliente de Endpoint Protection
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo configurar opciones de cliente personalizadas para Endpoint Protection.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 25a1803d7a2feebe7947478c0671e0112830b0d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709183"
---
# <a name="configure-custom-client-settings-for-endpoint-protection"></a>Establecer una configuración de cliente personalizada para Endpoint Protection

*Se aplica a: Configuration Manager (rama actual)*

En este procedimiento se establece una configuración de cliente personalizada para Endpoint Protection que puede implementar en recopilaciones de dispositivos en la jerarquía.

> [!IMPORTANT]  
>  Establezca solo la configuración de cliente de Endpoint Protection predeterminada si está seguro de que quiere aplicarla a todos los equipos de la jerarquía. 



## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>Para habilitar Endpoint Protection y establecer la configuración de cliente personalizada

1. En la consola de Configuration Manager, haga clic en **Administración**.  

2. En el área de trabajo **Administración** , haga clic en **Configuración de cliente**.  

3. En la pestaña **Inicio** , del grupo **Crear** , haga clic en **Crear configuración de dispositivo de cliente personalizada**.  

4. En el cuadro de diálogo **Crear configuración de dispositivo de cliente personalizada** , proporcione un nombre y una descripción para el grupo de opciones y luego seleccione **Endpoint Protection**.  

5. Configure las opciones de cliente de Endpoint Protection que necesite. Para obtener una lista completa de las opciones de cliente de Endpoint Protection que puede configurar, consulte la sección Endpoint Protection en [Sobre la configuración del cliente](../../core/clients/deploy/about-client-settings.md#endpoint-protection).  

   > [!IMPORTANT]  
   >  Instale el rol de sistema de sitio de Endpoint Protection antes de configurar las opciones de cliente de Endpoint Protection.  

6. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Crear configuración de dispositivo de cliente personalizada** . Las nuevas opciones de cliente se muestran en el nodo **Configuración de cliente** del área de trabajo **Administración** .  

7. Después, implemente la configuración de cliente personalizada en una colección. Seleccione la configuración de cliente personalizada que quiera implementar. En la pestaña **Inicio**, en el grupo **Configuración de cliente**, haga clic en **Implementar**.  

8. En el cuadro de diálogo **Seleccionar recopilación** , elija la recopilación en la que quiere implementar las opciones de cliente y haga clic en **Aceptar**. La nueva implementación se muestra en la pestaña **Implementaciones** del panel de detalles.  

Los clientes se configurarán con estas opciones la próxima vez que descarguen la directiva de cliente. Para obtener más información, vea [Iniciar la recuperación de directivas para un cliente de Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  



## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image"></a>Aprovisionamiento del cliente de Endpoint Protection en una imagen de disco

Instale el cliente de Endpoint Protection en un equipo que planee usar como origen de imagen del disco para la implementación del sistema operativo de Configuration Manager. Este equipo se denomina normalmente el equipo de referencia. Después de crear la imagen del SO, utilice la implementación del sistema operativo de Configuration Manager para implementar la imagen.

> [!Important]  
> Windows 10 y Windows Server 2016 incluyen Windows Defender de forma predeterminada. No necesita este procedimiento en esas versiones de Windows.  

Use los siguientes procedimientos para ayudarle a instalar y configurar el cliente de Endpoint Protection en un equipo de referencia.


### <a name="prerequisites"></a>Requisitos previos

La lista siguiente contiene los requisitos previos necesarios para la instalación del software cliente de Endpoint Protection en un equipo de referencia.

- Debe tener acceso al paquete de instalación de cliente de Endpoint Protection, **scepinstall.exe**. Busque este paquete en la carpeta **Cliente** de la carpeta de instalación de Configuration Manager en el servidor de sitio.  

- Para implementar el cliente de Endpoint Protection con la configuración necesaria de su organización, cree y exporte una directiva antimalware. Después especifique esta directiva al instalar manualmente el cliente de Endpoint Protection. Para obtener más información, vea [Cómo crear e implementar directivas antimalware](endpoint-antimalware-policies.md).  

  > [!NOTE]  
  >  No se puede exportar la **Directiva antimalware de cliente predeterminada**.  

- Si quiere instalar el cliente de Endpoint Protection con las definiciones más recientes, descárguelas desde [Windows Defender Security Intelligence](https://www.microsoft.com/wdsi).  

> [!NOTE]  
> A partir de la versión 1802 de Configuration Manager, no es necesario instalar el Agente de Endpoint Protection (SCEPInstall) en los dispositivos Windows 10. Si ya está instalado en los dispositivos Windows 10, Configuration Manager no lo quitará. Los administradores pueden quitar el Agente de Endpoint Protection en los dispositivos Windows 10 en los que se ejecute como mínimo la versión 1802 del cliente. Es posible que SCEPInstall.exe siga presente en C:\Windows\ccmsetup en algunos equipos, pero las instalaciones de cliente nuevas no deberían descargarlo. <!--503654-->


### <a name="how-to-install-the-endpoint-protection-client-on-the-reference-computer"></a>Instalación del cliente de Endpoint Protection en el equipo de referencia

Instale el cliente de Endpoint Protection localmente en el equipo de referencia desde un símbolo del sistema. Primero, obtenga el archivo de instalación **scepinstall.exe**. Para obtener más información, vea [Instalar el cliente de Endpoint Protection desde un símbolo del sistema](#bkmk_manual-install).

Si es necesario, incluya también una directiva antimalware preconfigurada o una directiva antimalware exportada anteriormente. 



## <a name="to-install-the-endpoint-protection-client-from-a-command-prompt"></a><a name="bkmk_manual-install"></a> Para instalar el cliente de Endpoint Protection desde un símbolo del sistema

1. Copie **scepinstall.exe** de la carpeta **Cliente** que se encuentra en la carpeta de instalación de Configuration Manager en el equipo en el que quiere instalar el software cliente de Endpoint Protection.  

2. Abra un símbolo del sistema como administrador. Cambie el directorio a la carpeta con el programa de instalación. Después, ejecute `scepinstall.exe`, añadiendo las propiedades de línea de comandos adicionales que necesite:


   |  Propiedad   |                                  Descripción                                   |
   |-------------|--------------------------------------------------------------------------------|
   |    `/s`     |                           Ejecutar el instalador en modo silencioso                           |
   |    `/q`     |                        Extraer los archivos de programa de instalación en modo silencioso                        |
   |    `/i`     |                           Ejecutar el instalador normalmente                           |
   |  `/policy`  | Especificar un archivo de directiva antimalware para configurar el cliente durante la instalación |
   | `/sqmoptin` |     Participar en el Programa para la mejora de la experiencia del usuario (CEIP) de Microsoft     |


3. Siga las instrucciones en pantalla para completar la instalación del cliente.  

4. Si descargó el paquete de definición de actualización más reciente, copie el paquete en el equipo cliente y, a continuación, haga doble clic en el paquete de definición para instalarlo.  

   > [!NOTE]  
   >  Después de completar la instalación del cliente de Endpoint Protection, el cliente realiza automáticamente una comprobación de actualización de definición. Si esta comprobación de actualización se realiza correctamente, no es necesario instalar manualmente el paquete de actualización de definiciones más reciente.  

#### <a name="example-install-the-client-with-an-antimalware-policy"></a>Ejemplo: instalar el cliente con una directiva antimalware

`scepinstall.exe /policy <full path>\<policy file>`



## <a name="verify-the-endpoint-protection-client-installation"></a>Verificar la instalación del cliente de Endpoint Protection

Después de instalar el cliente de Endpoint Protection en el equipo de referencia, compruebe que funciona correctamente.

1.  En el equipo de referencia, abra **System Center Endpoint Protection** desde el área de notificaciones de Windows.  

2.  En la pestaña **Inicio** del cuadro de diálogo **System Center Endpoint Protection**, compruebe que la opción **Protección en tiempo real** está configurada como **Activa**.  

3.  Compruebe que se muestra **Actualizadas** para **Definiciones de virus y spyware**.  

4.  Para asegurarse de que su equipo de referencia está listo para crear imágenes, en **Opciones de escaneado**, seleccione **Completo** y después seleccione **Escanear ahora**.  



## <a name="prepare-the-endpoint-protection-client-for-imaging"></a>Preparar el cliente de Endpoint Protection para la creación de imágenes

Realice los siguientes pasos para preparar el cliente de Endpoint Protection para la creación de imágenes:

1. En el equipo de referencia, inicie sesión como administrador.  

2. Descargue e instale **PsExec** desde [Windows SysInternals](https://docs.microsoft.com/sysinternals/downloads/psexec).  

3. Ejecute un símbolo del sistema como administrador, cambie el directorio a la carpeta donde instaló PsTools y después escriba el siguiente comando:  

   `psexec.exe -s -i regedit.exe`  

   > [!IMPORTANT]  
   >  Tenga cuidado al ejecutar el Editor del registro de esta manera. PsExec.exe lo ejecuta en el contexto LocalSystem.  

4. En el Editor del Registro, elimine las siguientes claves del Registro:  

   > [!IMPORTANT]  
   >  Elimine las claves del Registro como último paso antes de crear las imágenes en el equipo de referencia. El cliente de Endpoint Protection vuelve a crear estas claves cuando se inicia. Si reinicia el equipo de referencia, vuelva a eliminar las claves del Registro.  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID`   

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID`

Ahora tiene todo listo para preparar el equipo de referencia para la creación de imágenes.

Al implementar una imagen de sistema operativo que contenga el cliente de Endpoint Protection, envía automáticamente información al sitio de Configuration Manager asignado del dispositivo. El cliente descarga y aplica cualquier directiva antimalware de destino.  



## <a name="see-also"></a>Vea también

Para obtener más información sobre la implementación de sistema operativo en Configuration Manager, vea [Administrar imágenes de sistema operativo](../../osd/get-started/manage-operating-system-images.md).

