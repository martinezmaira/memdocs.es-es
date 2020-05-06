---
title: Solución de problemas de Endpoint Protection
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo solucionar problemas con Windows Defender y Endpoint Protection.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: efd31eaee987a7e28557cf0601608ca97c914999
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709423"
---
# <a name="troubleshoot-windows-defender-or-endpoint-protection-client"></a>Solución de problemas del cliente de Windows Defender o de Endpoint Protection

*Se aplica a: Configuration Manager (rama actual)*

Si surgen problemas con Windows Defender o Endpoint Protection, use este artículo para solucionar los problemas siguientes:  

- [Actualizar Windows Defender o Endpoint Protection](#update-windows-defender-or-endpoint-protection)  
- [Iniciar el servicio de Windows Defender o Endpoint Protection](#starting-windows-defender-or-endpoint-protection-service)  
- [Problemas de conexión de Internet](#internet-connection-issues)  
- [No se puede corregir una amenaza detectada](#detected-threat-cant-be-remediated)  

## <a name="update-windows-defender-or-endpoint-protection"></a>Actualizar Windows Defender o Endpoint Protection

### <a name="symptoms"></a>Síntomas

Windows Defender o Endpoint Protection funcionan automáticamente con Microsoft Update para garantizar que las definiciones de virus y spyware se mantengan actualizadas.  

En esta sección se tratan los problemas comunes con las actualizaciones automáticas y se incluyen las siguientes situaciones:  

- Ve mensajes de error que indican que se produjeron errores en las actualizaciones.  

- Al buscar actualizaciones, recibe un mensaje de error que indica que las actualizaciones de definiciones de virus y spyware no se pueden comprobar, descargar o instalar.  

- Incluso si el dispositivo está conectado a Internet, se produce un error en las actualizaciones.  

- Las actualizaciones no se instalan automáticamente según lo programado.  

### <a name="causes"></a>Causas

Las causas más comunes de problemas de actualización son problemas con la conectividad a Internet. Si sabe que su dispositivo está conectado a Internet ya que puede ir a otros sitios web, el problema podría deberse a conflictos con la configuración de Internet en Windows.  

### <a name="options-to-resolve"></a>Opciones para resolver

#### <a name="step-1-reset-your-internet-settings"></a>Paso 1: Restablecer la configuración de Internet  

1. Cierre todos los programas abiertos, incluido el explorador web.  

    > [!NOTE]  
    > Al restablecer esta configuración de Internet, es posible que se eliminen los archivos temporales, las cookies, el historial de exploración y las contraseñas en línea del explorador. Los favoritos no se eliminan.  

2. Vaya al menú **Inicio** y abra `inetcpl.cpl`.  

3. Cambie a la pestaña **Opciones avanzadas**.  

4. En la sección **Restablecer configuración de Internet Explorer**, seleccione **Restablecer** y otra vez **Restablecer** para confirmarlo.  

5. Seleccione **Aceptar** cuando se restablezca la configuración.

6. Intente volver a actualizar Windows Defender.

Si el problema persiste, continúe con el paso siguiente.  

#### <a name="step-2-make-sure-that-the-date-and-time-are-set-correctly-on-your-computer"></a>Paso 2: Asegurarse de que la fecha y la hora están establecidas correctamente en el equipo  

Si el mensaje de error contiene el código 0x80072f8f, el problema se debe probablemente a una configuración incorrecta de la fecha o la hora del equipo. Vaya al menú **Inicio**, seleccione **Configuración**, **Hora e idioma** y **Fecha y hora**.

#### <a name="step-3-rename-the-software-distribution-folder-on-your-computer"></a>Paso 3: Cambiar la carpeta de distribución de software en el equipo  

1. Detenga el servicio **Windows Update**.  

    1. Vaya a **Inicio** y abra **services.msc**.  

    2. Seleccione el servicio **Windows Update**. Vaya al menú **Acción** y seleccione **Detener**.

2. Cambie el nombre del directorio **SoftwareDistribution**.  

    1. Abra un símbolo del sistema como administrador.  

    2. Escriba los siguientes comandos:

        ```cmd
        cd %windir%
        ren SoftwareDistribution SDTemp
        exit
        ```

3. Reinicie el servicio **Windows Update**.

    1. Vuelva a la ventana **Servicios**.  

    2. Seleccione el servicio **Windows Update**. Vaya al menú **Acción** y seleccione **Iniciar**.

    3. Cierre la ventana Servicios.  

#### <a name="step-4-reset-the-microsoft-antivirus-update-engine-on-your-computer"></a>Paso 4: Restablecer el motor de actualización antivirus de Microsoft en el equipo  

1. Abra un símbolo del sistema como administrador.

2. Escriba los siguientes comandos:

    ```cmd
    cd \

    cd program files\windows defender

    MpCmdRun -RemoveDefinitions -all

    exit
    ```

3. Reinicie el equipo.  

4. Intente volver a actualizar Windows Defender.

Si el problema persiste, continúe con el paso siguiente.  

#### <a name="step-5-manually-install-the-definition-updates"></a>Paso 5: Instalar manualmente las actualizaciones de definiciones  

[Descargue las últimas actualizaciones manualmente](https://www.microsoft.com/en-us/wdsi/defenderupdates).  

#### <a name="step-6-contact-microsoft-support"></a>Paso 6: Ponerse en contacto con el soporte técnico de Microsoft.  

Si estos pasos no resuelven el problema, póngase en contacto con el soporte técnico de Microsoft. Para obtener más información, consulte [Opciones de soporte y recursos de la comunidad](../../core/understand/find-help.md#BKMK_SupportOptions).  

## <a name="starting-windows-defender-or-endpoint-protection-service"></a>Iniciar el servicio de Windows Defender o Endpoint Protection

### <a name="symptom"></a>Síntoma

Recibe un mensaje que le notifica que **Windows Defender o Endpoint Protection no está supervisando el equipo porque se detuvo el servicio del programa. Debe reiniciarlo ahora.**

### <a name="solution"></a>Solución

#### <a name="step-1-restart-your-computer"></a>Paso 1: Reiniciar el equipo

Cierre todas las aplicaciones y reinicie el equipo.  

#### <a name="step-2-check-the-windows-service"></a>Paso 2: Comprobar el servicio de Windows

1. Vaya a **Inicio** y abra **services.msc**.  

2. Seleccione **Servicio de Antivirus de Windows Defender**.  

3. Asegúrese de que **Tipo de inicio** esté establecido en **Automático**.

4. Vaya al menú **Acción** y seleccione **Iniciar**.

    1. Si esta acción no está disponible, seleccione **Detener**. Espere a que se detenga el servicio y, después, seleccione la acción **Iniciar** para reiniciarlo.  

Anote los errores que puedan aparecer durante este proceso. [Póngase en contacto con Soporte técnico de Microsoft](../../core/understand/find-help.md#BKMK_SupportOptions) y proporcione la información del error.  

#### <a name="step-3-remove-any-third-party-security-programs"></a>Paso 3: Quitar todos los programas de seguridad de terceros  

> [!NOTE]  
> Algunas aplicaciones de seguridad no se desinstalan completamente. Es posible que tenga que descargar y ejecutar una utilidad de limpieza de la aplicación de seguridad anterior para que se quite por completo.  

1. Vaya a **Inicio** y abra **appwiz.cpl**.  

2. En la lista de programas instalados, desinstale cualquier programa de seguridad de otro fabricante.

3. Reinicie su equipo.  

> [!CAUTION]  
> Cuando quite programas de seguridad, el equipo quedará desprotegido. Si tiene problemas para instalar Windows Defender después de quitar los programas de seguridad existentes, póngase en contacto con el [soporte técnico de Microsoft](https://support.microsoft.com/supportforbusiness/productselection). Seleccione la familia de productos **Seguridad** y, después, el producto **Windows Defender**.

## <a name="internet-connection-issues"></a>Problemas de conexión de Internet

Para que el equipo reciba las últimas actualizaciones de Windows Update, conéctelo a Internet.  

1. Vaya a **Inicio** y abra **ncpa.cpl**.  

2. Abra el nombre de la conexión para ver el **Estado** de la conexión.  

3. Si el equipo está conectado, el estado de **Conectividad IPv4** o **Conectividad IPv6** es **Internet**.  

4. Si el equipo no parece estar conectado, seleccione el nombre de la conexión y, después, **Diagnosticar esta conexión**.

Cierre todos los programas abiertos y reinicie el equipo.  

## <a name="detected-threat-cant-be-remediated"></a>No se puede corregir una amenaza detectada

Cuando Windows Defender o Endpoint Protection detectan una amenaza potencial, para intentar mitigarla la ponen en cuarentena o la eliminan. Estas amenazas se pueden ocultar dentro de un archivo comprimido (`.zip`) o en un recurso compartido de red.

### <a name="remove-or-scan-the-file"></a>Quitar o examinar el archivo  

- Si la amenaza detectada estaba en un archivo de almacenamiento comprimido, vaya al archivo. Elimine el archivo o examínelo manualmente. Haga clic con el botón derecho en el archivo y seleccione **Examinar con Windows Defender**. Si Windows Defender detecta amenazas adicionales en el archivo, se lo notificará. Después, puede elegir una acción adecuada.  

- Si la amenaza detectada estaba en un recurso compartido de red, ábralo y examínelo manualmente. Haga clic con el botón derecho en el archivo y seleccione **Examinar con Windows Defender**. Si Windows Defender detecta amenazas adicionales en el recurso compartido de red, se lo notificará. Después, puede elegir una acción adecuada.  

- Si no está seguro del origen del archivo, ejecute un examen completo en el equipo. Un examen completo puede tardar algún tiempo en realizarse.  

## <a name="see-also"></a>Vea también

[Preguntas más frecuentes sobre el cliente de Endpoint Protection](endpoint-protection-client-faq.md)

[Ayuda del cliente Endpoint Protection](endpoint-protection-client-help.md)
