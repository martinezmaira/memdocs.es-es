---
title: Comprobador de requisitos previos
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo usar el Comprobador de requisitos previos para identificar y corregir problemas que podrían bloquear un sitio o la instalación de un rol de sistema de sitio.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aaf13bb8-4ba2-4bd7-9fac-d36a9d88a1b6
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1ee871d99285bee3a4489d88bf0d203bf74cde3c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700713"
---
# <a name="prerequisite-checker-for-configuration-manager"></a>Comprobador de requisitos previos de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

 Antes de ejecutar el programa de instalación para instalar o actualizar un sitio de Configuration Manager, o antes de instalar un rol de sistema de sitio en un servidor nuevo, puede usar esta aplicación independiente (**Prereqchk.exe**) de la versión de Configuration Manager que quiere usar para comprobar la disponibilidad del servidor. Use el Comprobador de requisitos previos para identificar y corregir problemas que podrían bloquear un sitio o la instalación de un rol de sistema de sitio.  

> [!NOTE]  
>  El Comprobador de requisitos previos siempre se ejecuta como parte del programa de instalación.  

De forma predeterminada, cuando se ejecuta el Comprobador de requisitos previos:  

-   Se valida el servidor en el que se ejecuta.  
-   Se analiza el equipo local para detectar un servidor de sitio existente, y solo se ejecutan las comprobaciones aplicables al sitio.  
-   Si no se detecta ningún sitio existente, se ejecutan todas las reglas de requisitos previos.  
-   Comprueba las reglas para asegurarse de que el software y la configuración necesarios para la instalación están instalados. Es posible que el software necesario requiera configuraciones adicionales o actualizaciones de software que el Comprobador de requisitos previos no ha comprobado.  
-   Los resultados se registran en el archivo **ConfigMgrPrereq.log** en la unidad del sistema del equipo. El archivo de registro podría contener información adicional que no aparece en la interfaz de la aplicación.  

Al ejecutar el Comprobador de requisitos previos en el símbolo del sistema y especificar opciones de línea de comandos determinadas:  

-   El Comprobador de requisitos previos solo efectúa las comprobaciones que están asociadas con el servidor de sitio o los sistemas de sitio que especifique en la línea de comandos.  
-   Para comprobar un equipo remoto, la cuenta de usuario debe tener derechos de administrador en el equipo remoto.  

Para más información sobre las comprobaciones que lleva a cabo el Comprobador de requisitos previos, vea [Lista de comprobaciones previas de Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md).  

## <a name="copy-prerequisite-checker-files-to-another-computer"></a>Copiar los archivos del Comprobador de requisitos previos a otro equipo  

1.  En el Explorador de Windows, vaya a una de las siguientes ubicaciones:  

    -   **&lt;*Medios de instalación de Configuration Manager*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Ruta de instalación de Configuration Manager*\>\BIN\X64**  

2.  Copie los archivos siguientes a la carpeta de destino del otro equipo:  

    - prereqchk.exe
    - prereqcore.dll
    - prereqchkres.dll
      - Este archivo se encuentra en la subcarpeta del idioma de instalación. Por ejemplo, el idioma inglés se encuentra en la subcarpeta `00000409`. <!--586808-->
    - basesql.dll
    - basesvr.dll
    - baseutil.dll

##  <a name="run-prerequisite-checker-with-default-checks"></a>Ejecutar el Comprobador de requisitos previos con las comprobaciones predeterminadas  

1.  En el Explorador de Windows, vaya a una de las siguientes ubicaciones:  

    -   **&lt;*Medios de instalación de Configuration Manager*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Ruta de instalación de Configuration Manager*\>\BIN\X64**  

2.  Abra **prereqchk.exe** para iniciar el Comprobador de requisitos previos.   
    El Comprobador de requisitos previos detecta los sitios existentes y, si los encuentra, realiza comprobaciones de preparación para la actualización. En cambio, si no encuentra ningún sitio, se realizan todas las comprobaciones. En la columna **Tipo de sitio** se ofrece información sobre el servidor de sitio o el sistema de sitio con que está asociada la regla.  

##  <a name="run-prerequisite-checker-from-a-command-prompt-for-all-default-checks"></a>Ejecutar el Comprobador de requisitos previos desde el símbolo del sistema para todas las comprobaciones predeterminadas  

1.  Abra una ventana del símbolo del sistema y cambie los directorios a una de las siguientes ubicaciones:  

    -   **&lt;*Medios de instalación de Configuration Manager*\>\SMSSETUP\BIN\X64**  
    -   **&lt;*Ruta de instalación de Configuration Manager*\>\BIN\X64**  

2.  Escriba  **prereqchk.exe /LOCAL** para iniciar el Comprobador de requisitos previos y ejecutar todas las comprobaciones de requisitos previos en el servidor.  

## <a name="run-prerequisite-checker-from-a-command-prompt-to-use-options"></a>Ejecutar el Comprobador de requisitos previos desde el símbolo del sistema para usar las opciones  

1. Abra una ventana del símbolo del sistema y cambie los directorios a una de las siguientes ubicaciones:  

   -   **&lt;*Medios de instalación de Configuration Manager*\>\SMSSETUP\BIN\X64**  
   -   **&lt;*Ruta de instalación de Configuration Manager*\>\BIN\X64**  

2. Escriba **prereqchk.exe** agregando una o varias de las siguientes opciones de línea de comandos.  

   Por ejemplo, para comprobar un sitio principal puede usar lo siguiente:  

      **prereqchk.exe [/NOUI] /PRI /SQL &lt;FQDN de SQL Server\> /SDK &lt;FQDN del proveedor de SMS\> [/JOIN &lt;FQDN del sitio de administración central\>] [/MP &lt;FQDN del punto de administración\>] [/DP &lt;FQDN del punto de distribución\>]**  

   **Servidor del sitio de administración central:**  

   -   **/NOUI**  

        No es necesario. Inicia el Comprobador de requisitos previos sin mostrar la interfaz de usuario. Debe especificar esta opción antes que cualquier otra opción en la línea de comandos.  

   -   **/CAS**  

        Necesario. Comprueba que el equipo local cumple los requisitos para el sitio de administración central.  

   -   **/SQL &lt;*FQDN de SQL Server*>**  

        Necesario. Mediante el nombre de dominio completo (FQDN) se comprueba que el equipo especificado cumpla los requisitos de SQL Server para hospedar la base de datos del sitio de Configuration Manager.  

   -   **/SDK &lt;*FQDN de proveedor de SMS*>**  

        Necesario. Comprueba que el equipo especificado cumple los requisitos del proveedor de SMS.  

   -   **/Ssbport**  

        No es necesario. Comprueba que existe una excepción de firewall para permitir la comunicación en el puerto de SQL Server Service Broker (SSB). El puerto de SSB predeterminado es el 4022.  

   -   **InstallDir &lt;*ruta de instalación de Configuration Manager*>**  

        No es necesario. Comprueba el espacio mínimo en disco requerido para la instalación del sitio.  

   **Servidor de sitio primario:**  

   -   **/NOUI**  

       No es necesario. Inicia el Comprobador de requisitos previos sin mostrar la interfaz de usuario. Debe especificar esta opción antes que cualquier otra opción en la línea de comandos.  

   -   **/PRI**  

        Necesario. Comprueba que el equipo local cumple los requisitos para el sitio primario.  

   -   **/SQL &lt;*FQDN de SQL Server*>**  

        Necesario. Comprueba que el equipo especificado cumple los requisitos de SQL Server para hospedar la base de datos del sitio de Configuration Manager.  

   -   **/SDK &lt;*FQDN de proveedor de SMS*>**  

        Necesario. Comprueba que el equipo especificado cumple los requisitos del proveedor de SMS.  

   -   **/JOIN &lt;*FQDN de sitio de administración central*>**  

        No es necesario. Comprueba que el equipo local cumple los requisitos para la conexión al servidor de sitio de administración central.  

   -   **/MP &lt;*FQDN de punto de administración*>**  

        No es necesario. Comprueba que el equipo especificado cumple los requisitos para el rol de sistema de sitio de punto de administración. Esta opción solo se admite cuando se usa la opción **/PRI** .  

   -   **/DP &lt;*FQDN de punto de distribución*>**  

        No es necesario. Comprueba que el equipo especificado cumple los requisitos para el rol de sistema de sitio de punto de distribución. Esta opción solo se admite cuando se usa la opción **/PRI** .  

   -   **/Ssbport**  

        No es necesario. Comprueba que existe una excepción de firewall para permitir la comunicación en el puerto de SSB. El puerto de SSB predeterminado es el 4022.  

   -   **InstallDir &lt;*ruta de instalación de Configuration Manager*>**  

        No es necesario. Comprueba el espacio mínimo en disco requerido para la instalación del sitio.  

   **Servidor de sitio secundario:**  

   -   **/NOUI**  

        No es necesario. Inicia el Comprobador de requisitos previos sin mostrar la interfaz de usuario. Debe especificar esta opción antes que cualquier otra opción en la línea de comandos.  

   -   **/SEC &lt;*FQDN de servidor de sitio secundario*>**  

        Necesario. Comprueba que el equipo especificado cumple los requisitos para el sitio secundario.  

   -   **/INSTALLSQLEXPRESS**  

        No es necesario. Comprueba que SQL Server Express puede instalarse en el equipo especificado.  

   -   **/Ssbport**  

        No es necesario. Comprueba que existe una excepción de firewall para permitir la comunicación para el puerto de SSB. El puerto de SSB predeterminado es el 4022.  

   -   **/Sqlport**  

        No es necesario. Comprueba que existe una excepción de firewall para permitir la comunicación del puerto de servicio de SQL Server y que ninguna otra instancia con nombre de SQL Server usa el puerto. El puerto predeterminado es 1433.  

   -   **InstallDir &lt;*ruta de instalación de Configuration Manager*>**  

        No es necesario. Comprueba el espacio mínimo en disco requerido para la instalación del sitio.  

   -   **/SourceDir**  

        No es necesario. Comprueba que la cuenta de equipo del sitio secundario puede tener acceso a la carpeta que hospeda los archivos de origen del programa de instalación.  

   **Consola de Configuration Manager:**  

   -   **/Adminui**  

        Necesario. Comprueba que el equipo local cumple los requisitos para instalar Configuration Manager.  

3. En la interfaz de usuario del Comprobador de requisitos previos, el Comprobador de requisitos previos crea una lista de los problemas detectados en la sección **Resultado de requisitos previos**.  

   -   Haga clic en un elemento de la lista para obtener más información acerca de cómo resolver el problema.  
   -   Debe resolver todos los elementos de la lista que tengan un estado de **Error** antes de instalar el servidor de sitio, el sistema de sitio o la consola de Configuration Manager.  
   -   También puede abrir el archivo **ConfigMgrPrereq.log** en la raíz de la unidad del sistema para revisar los resultados del Comprobador de requisitos previos. El archivo de registro podría contener información adicional que no se muestra en la interfaz de usuario del Comprobador de requisitos previos.  
