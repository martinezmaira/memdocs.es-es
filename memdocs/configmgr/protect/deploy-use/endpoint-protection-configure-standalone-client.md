---
title: Configuración de Endpoint Protection en un cliente independiente
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo configurar Endpoint Protection en un cliente independiente.
ms.date: 07/22/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f8d116879b0a85f3276d848b01c69d575b8b69fd
ms.sourcegitcommit: 41b2b50d5870dc127a8848a6657d56112f92515a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/04/2020
ms.locfileid: "87758319"
---
# <a name="configure-endpoint-protection-on-a-standalone-client"></a>Configuración de Endpoint Protection en un cliente independiente

*Se aplica a: Configuration Manager (rama actual)*

La organización puede tener varios clientes independientes que no se pueden administrar ni proteger con Microsoft Endpoint Configuration Manager. Sin ninguna instancia de Endpoint Protection, estos clientes independientes son vulnerables a posibles ataques de malware. Para proteger estos clientes independientes, puede configurarlos manualmente con Endpoint Protection, como se describe en este tema.

Para configurar Endpoint Protection manualmente en un cliente independiente:

- [Creación de una directiva antimalware para el cliente independiente](#create-an-antimalware-policy-for-the-standalone-client)
- [Transferencia del paquete de instalación del cliente de Endpoint Protection al cliente independiente](#transfer-endpoint-protection-client-installation-package-to-the-standalone-client)
- [Instalación de Endpoint Protection en el cliente independiente](#install-endpoint-protection-on-the-standalone-client)

## <a name="prerequisites"></a>Requisitos previos

Estos son los requisitos previos para configurar Endpoint Protection en un cliente independiente:

- Debe tener acceso al paquete de instalación de cliente de Endpoint Protection, **scepinstall.exe**. Puede encontrar este paquete en la carpeta **C:\Archivos de programa\Microsoft Configuration Manager\Client**. 
- Asegúrese de que está instalada la [actualización de la plataforma antimalware de enero de 2017 para clientes de Endpoint Protection](https://support.microsoft.com/help/3209361/january-2017-anti-malware-platform-update-for-endpoint-protection-clie). 

## <a name="create-an-antimalware-policy-for-the-standalone-client"></a>Creación de una directiva antimalware para el cliente independiente

En este paso, creará una directiva antimalware personalizada en la consola de Configuration Manager y, a continuación, la transferirá al cliente independiente.

Al crear la directiva antimalware, debe configurar el origen de la actualización de definiciones para mantener actualizadas las definiciones de la directiva en el cliente independiente. Puede configurar el origen de la actualización de definiciones como [Microsoft Update](endpoint-definitions-microsoft-updates.md) y el [Centro de protección contra malware de Microsoft](endpoint-definitions-protection-center.md), si el cliente independiente está conectado a Internet. Como alternativa, seleccione [Recurso compartido de red](endpoint-definitions-network.md) como el origen de distribución de la definición y actualícelo periódicamente con el paquete de actualización de definiciones más reciente. 

Para crear una directiva antimalware para el cliente independiente:

1. En la consola de **Configuration Manager**, haga clic en **Activos y compatibilidad**.
2. En el área de trabajo **Activos y compatibilidad** , expanda **Endpoint Protection**y haga clic en **Directivas antimalware**.
3. En el **Inicio** ficha el **crear** de grupo, haga clic en **Crear directiva Antimalware**.
4. En el **General** sección de la **Crear directiva Antimalware** diálogo cuadro, escriba un nombre y una descripción para la directiva.
5. En el **Crear directiva Antimalware** diálogo cuadro, configure las opciones que necesita para esta directiva antimalware y, a continuación, haga clic en **Aceptar**. Para obtener una lista de las opciones que puede configurar, consulte [Lista de configuración de directiva Antimalware](endpoint-antimalware-policies.md#list-of-antimalware-policy-settings).
    > [!NOTE]
    > En la configuración de **Actualizaciones de definiciones**, seleccione **Actualizaciones distribuidas desde Microsoft Update** y **Actualizaciones distribuidas desde el Centro de protección contra malware de Microsoft** si el cliente independiente está conectado a Internet.  
    > Como alternativa, seleccione **Actualizaciones desde recursos compartidos de archivos UNC** para distribuir las definiciones de directiva a través de un recurso compartido de red. A continuación, agregue una o varias rutas de acceso UNC a la ubicación de los archivos de actualizaciones de definiciones en un recurso compartido de red.

6. Exporte la directiva recién creada como XML:
    1. En la lista **Directivas antimalware**, haga clic con el botón derecho en la directiva.
    1. Seleccione **Exportar**.
    1. Guarde la directiva como XML, por ejemplo, **standalone.xml**.
7. Transfiera el nuevo XML de la directiva antimalware al cliente independiente de destino en el que desea configurar Endpoint Protection.

## <a name="transfer-endpoint-protection-client-installation-package-to-the-standalone-client"></a>Transferencia del paquete de instalación del cliente de Endpoint Protection al cliente independiente

En este paso, copiará el paquete de instalación del cliente de Endpoint Protection (**scepinstall.exe**) del servidor de Configuration Manager y lo transferirá al cliente independiente.

1. Inicie sesión en el servidor de Configuration Manager.
2. Navegue hasta la carpeta **Client** de la carpeta de instalación de Configuration Manager (**C:\Archivos de programa\Microsoft Configuration Manager\Client**).
3. Copie **scepinstall.exe**.
4. Transfiera **scepinstall.exe** al cliente independiente de destino en el que desea instalar el software cliente de Endpoint Protection.

## <a name="install-endpoint-protection-on-the-standalone-client"></a>Instalación de Endpoint Protection en el cliente independiente
En este paso, ejecutará el paquete del instalador (**scepinstall.exe**) y la directiva antimalware (que se transfirió previamente desde el servidor de Configuration Manager) desde el símbolo del sistema en el cliente independiente.

Para instalar Endpoint Protection en el cliente independiente:

1. En el cliente independiente, abra un símbolo del sistema como administrador.
2. Cambie el directorio a la carpeta donde guardó el archivo instalador **scepinstall.exe**.
3. Escriba el siguiente comando para ejecutar **scepinstall.exe** con la directiva antimalware:

    ```cmd
    scepinstall.exe /policy <full path>\<policy file>
    ```

    Reemplace `full path` por la ruta de acceso donde guardó el archivo XML de la directiva antimalware y `policy file` por el nombre de archivo de la directiva antimalware.
 
    El instalador se extrae y se inicia el Asistente para la instalación.

4. Siga las instrucciones en pantalla para completar la instalación del cliente.

    En la última pantalla del Asistente para la instalación, se selecciona de forma predeterminada la opción para examinar el equipo en busca de posibles amenazas después de obtener las actualizaciones más recientes. Puede desactivar la casilla para omitir la detección.

## <a name="change-antimalware-policy-settings-on-a-standalone-endpoint-protection-client"></a>Modificación de la configuración de la directiva antimalware en un cliente de Endpoint Protection independiente

Para cambiar o actualizar la directiva antimalware en el cliente de Endpoint Protection independiente: 

1. [Cree una directiva antimalware para el cliente independiente](#create-an-antimalware-policy-for-the-standalone-client).
2. Ejecute el siguiente comando en el cliente independiente:

```cmd
C:\Program Files\Microsoft Security Client\ConfigSecurityPolicy.exe <full path>\<policy file>
```

Reemplace `full path` por la ruta de acceso donde guardó el archivo XML nuevo de la directiva antimalware y `policy file` por el nombre de archivo de la directiva antimalware.

## <a name="next-steps"></a>Pasos siguientes

Para obtener información sobre cómo usar Endpoint Protection para administrar la seguridad y el malware en equipos cliente de Configuration Manager, vea [Configurar Endpoint Protection](endpoint-protection-configure.md).