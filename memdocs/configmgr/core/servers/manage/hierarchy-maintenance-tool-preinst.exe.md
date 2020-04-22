---
title: Herramienta de mantenimiento de jerarquías
titleSuffix: Configuration Manager
description: Comprenda lo que realiza la herramienta de mantenimiento de jerarquía y por qué podría usarla. Incluye referencia de las opciones de línea de comandos.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cead6825-6113-4ba5-a381-ac3598dfee86
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b564575dfc135a9c82c7e102a02d70f1b6dbf6eb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692603"
---
# <a name="hierarchy-maintenance-tool-preinstexe-for-configuration-manager"></a>Herramienta de mantenimiento de jerarquía (Preinst.exe) para Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

La herramienta de mantenimiento de jerarquía (Preinst.exe) pasa comandos al Administrador de jerarquía de Configuration Manager mientras se ejecuta el servicio Administrador de jerarquía. La herramienta de mantenimiento de jerarquía se instala automáticamente al instalar un sitio de Configuration Manager. Encontrará Preinst.exe en la carpeta compartida del servidor de sitio \\&lt;*nombreDeServidorDeSitio*>\SMS_&lt;*códigoDeSitio*\bin\X64\00000409.  

 Puede usar la herramienta de mantenimiento de jerarquía en los siguientes escenarios:  

-   Cuando se requiere el intercambio de claves seguro, existen situaciones en las que debe realizar manualmente el intercambio de claves públicas inicial entre sitios. Para obtener más información, consulte [Intercambio manual de claves públicas entre sitios](#BKMK_ManuallyExchangeKeys) en este tema.  

-   Para quitar trabajos activos de un sitio de destino que ya no está disponible.  

-   Para eliminar un servidor de sitio desde la consola de Configuration Manager cuando no se puede desinstalar el sitio mediante el programa de instalación. Por ejemplo, si quita físicamente un sitio de Configuration Manager sin ejecutar primero el programa de instalación para desinstalar el sitio, la información del sitio todavía existirá en la base de datos del sitio primario. El sitio primario seguirá intentando comunicarse con el sitio secundario. Para resolver este problema, debe ejecutar la herramienta de mantenimiento de jerarquía y eliminar manualmente el sitio secundario de la base de datos del sitio primario.  

-   Para detener todos los servicios de Configuration Manager de un sitio sin tener que detener los servicios de forma individual.  

-   Cuando se va a recuperar un sitio, puede usar la opción CHILDKEYS para distribuir las claves públicas de varios sitios secundarios en el sitio de recuperación.  

Para ejecutar la herramienta de mantenimiento de jerarquía, el usuario actual debe tener privilegios administrativos en el equipo local. Además, el usuario debe tener explícitamente el permiso de seguridad de administrador del sitio. La herencia de este permiso por ser un miembro de un grupo que lo tenga no es suficiente.  

## <a name="hierarchy-maintenance-tool-command-line-options"></a>Opciones de línea de comandos de la herramienta de mantenimiento de jerarquía  
Cuando se utiliza la herramienta de mantenimiento de jerarquía, debe ejecutarla localmente en el servidor de sitio secundario, sitio primario o sitio de administración central.  

Al ejecutar la herramienta de mantenimiento de jerarquía, debe usar la sintaxis siguiente: preinst.exe /&lt;opción\>. A continuación se indican las opciones de la línea de comandos.  

 **/DELJOB &lt;*códigoDeSitio*>** : use esta opción en un sitio para eliminar todos los trabajos o los comandos del sitio actual para el sitio de destino especificado.  

 **/DELSITE &lt;*códigoDeSitioSecundarioParaEliminar*>** : use esta opción en un sitio primario para eliminar los datos de los sitios secundarios de la base de datos del sitio del sitio primario. Por lo general, use esta opción si se da de baja un equipo de servidor de sitio antes de desinstalar el sitio del mismo.  

> [!NOTE]  
>  La opción /DELSITE no desinstala el sitio en el equipo especificado por el parámetro CódigoDeSitioSecundarioParaEliminar. Esta opción solo quita la información del sitio de la base de datos del sitio de Configuration Manager.  

**/DUMP &lt;*códigoDeSitio*>** : use esta opción en el servidor de sitio local para escribir imágenes de control de sitio en la carpeta raíz de la unidad en la que está instalado el sitio. Puede escribir una determinada imagen de control de sitio en la carpeta o escribir todos los archivos de control de sitio en la jerarquía.  

-   /DUMP &lt;*códigoDeSitio*> escribe la imagen de control de sitio solo para el sitio especificado.  

-   /DUMP escribe los archivos de control de sitio para todos los sitios.  

Una imagen es una representación binaria del archivo de control de sitio, que se almacena en la base de datos del sitio de Configuration Manager. La imagen volcada del archivo de control de sitio es la suma de la imagen base más las imágenes delta pendientes.  

Después de volcar una imagen de archivo de control de sitio con la herramienta de mantenimiento de jerarquía, el nombre de archivo tiene el formato sitectrl_&lt;*códigoDeSitio*>.ct0.  

**/STOPSITE**: use esta opción en el servidor de sitio local para iniciar un ciclo de apagado del servicio Administrador de componentes de sitio de Configuration Manager, que restablece parcialmente el sitio. Cuando se ejecuta este ciclo de apagado, algunos servicios de Configuration Manager se detienen en el servidor de sitio y sus sistemas de sitio remotos. Estos servicios se marcan para su reinstalación. Como resultado de este ciclo de apagado, algunas contraseñas se cambian automáticamente cuando se vuelven a instalar los servicios.  

> [!NOTE]  
>  Si desea ver un registro de apagado, reinstalación y cambios de contraseñas para el Administrador de componentes de sitio, habilite el registro para este componente antes de usar esta opción de línea de comandos.  

El ciclo de apagado procede automáticamente una vez iniciado, y omitirá componentes o equipos que no respondan. Sin embargo, si el servicio Administrador de componentes de sitio no puede obtener acceso a un sistema de sitio remoto durante el ciclo de apagado, los componentes que se instalan en el sistema de sitio remoto se reinstalan cuando se reinicia el servicio Administrador de componentes de sitio. Cuando se reinicia, el servicio Administrador de componentes de sitio intenta repetidamente volver a instalar todos los servicios marcados para su reinstalación.  

Puede reiniciar el servicio Administrador de componentes de sitio mediante Service Manager. Después de reiniciarlo, todos los servicios afectados se desinstalan, reinstalan y reinician. Después de usar la opción /STOPSITE para iniciar el ciclo de apagado, no se pueden evitar los ciclos de reinstalación después de reiniciar el servicio Administrador de componentes de sitio.  

**/KEYFORPARENT**: use esta opción en un sitio para distribuir la clave pública del sitio a un sitio primario.  

La opción /KEYFORPARENT coloca la clave pública del sitio en el archivo &lt;*códigoDeSitio*>.CT4 en la raíz de la unidad de archivos de programa. Después de ejecutar preinst.exe con esta opción, copie manualmente el archivo &lt;*códigoDeSitio*>.CT4 en la carpeta del sitio primario …\Inboxes\hman.box (no hman.box\pubkey).  

**/KEYFORCHILD**: use esta opción en un sitio para distribuir la clave pública del sitio en un sitio secundario.  

La opción /KEYFORCHILD coloca la clave pública del sitio en el archivo &lt;*códigoDeSitio*>.CT5 en la raíz de la unidad de archivos de programa. Después de ejecutar preinst.exe con esta opción, copie manualmente el archivo &lt;*códigoDeSitio*>.CT5 en la carpeta del sitio secundario …\Inboxes\hman.box (no hman.box\pubkey).  

**/CHILDKEYS**: puede usar esta opción en los sitios secundarios de un sitio que se va a recuperar. Use esta opción para distribuir las claves públicas de varios sitios secundarios al sitio de recuperación.  

La opción /CHILDKEYS coloca la clave del sitio en el que se ejecutó la opción y todas las claves públicas de sus sitios secundarios en el archivo &lt;*códigoDeSitio*>.CT6.  

Después de ejecutar preinst.exe con esta opción, copie manualmente el archivo &lt;*códigoDeSitio*>.CT6 en la carpeta del sitio de recuperación …\Inboxes\hman.box (no hman.box\pubkey).  

**/PARENTKEYS**: puede usar esta opción en el sitio primario de un sitio que se va a recuperar. Use esta opción para distribuir las claves públicas de todos los sitios primarios al sitio de recuperación.  

La opción /PARENTKEYS coloca la clave del sitio en el que se ejecutó la opción y todas las claves de sus sitios primarios en el archivo &lt;códigoDeSitio\>.CT7.  

Después de ejecutar preinst.exe con esta opción, copie manualmente el archivo &lt;*códigoDeSitio*>.CT7 en la carpeta del sitio de recuperación …\Inboxes\hman.box (no hman.box\pubkey).  

##  <a name="manually-exchange-public-keys-between-sites"></a><a name="BKMK_ManuallyExchangeKeys"></a> Intercambio manual de claves públicas entre sitios  
De manera predeterminada, la opción **Requerir intercambio de claves seguro** está habilitada para los sitios de Configuration Manager. Cuando se requiere el intercambio de claves seguro, existen dos situaciones en las que debe realizar manualmente el intercambio inicial de claves entre sitios:  

-   Si el esquema de Active Directory no se ha extendido para Configuration Manager  

-   Los sitios de Configuration Manager no están publicando datos del sitio en Active Directory  

Puede utilizar la herramienta de mantenimiento de jerarquía para exportar las claves públicas para cada sitio. Cuando se han exportado, intercambie manualmente las claves entre los sitios.  

> [!NOTE]  
>  Al finalizar el intercambio manual de claves públicas, puede revisar el archivo de registro **hman.log** (registra los cambios de configuración y la publicación de información de sitio en Servicios de dominio de Active Directory) en el servidor de sitio primario para asegurarse de que el sitio primario ha procesado la nueva clave pública.  

#### <a name="to-manually-transfer-the-child-site-public-key-to-the-parent-site"></a>Para transferir manualmente la clave pública del sitio secundario al sitio primario  

1.  En una sesión en el sitio secundario, abra un símbolo del sistema y desplácese hasta la ubicación de **Preinst.exe**.  

2.  Escriba lo siguiente para exportar la clave pública del sitio secundario: **Preinst /keyforparent**  

3.  La opción /keyforparent coloca la clave pública del sitio secundario en el archivo **&lt;código de sitio\>.CT4** en la raíz de la unidad de sistema.  

4.  Mueva el archivo **&lt;código de sitio\>.CT4** a la carpeta del sitio primario **&lt;directorio de instalación\>\inboxes\hman.box**.  

#### <a name="to-manually-transfer-the-parent-site-public-key-to-the-child-site"></a>Para transferir manualmente la clave pública del sitio primario al sitio secundario  

1.  En una sesión en el sitio primario, abra un símbolo del sistema y desplácese hasta la ubicación de **Preinst.exe**.  

2.  Escriba lo siguiente para exportar la clave pública del sitio primario: **Preinst /keyforchild**.  

3.  La opción /keyforchild coloca la clave pública del sitio primario en el archivo **&lt;código de sitio\>.CT5** en la raíz de la unidad de sistema.  

4.  Mueva el archivo **&lt;código de sitio\>.CT5** al directorio del sitio secundario **&lt;directorio de instalación\>\inboxes\hman.box**.  
