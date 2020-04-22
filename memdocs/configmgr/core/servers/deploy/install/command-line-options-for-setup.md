---
title: Configuración de opciones de la línea de comandos
titleSuffix: Configuration Manager
description: Cree scripts de automatización para instalar Configuration Manager desde una línea de comandos.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8e4950e32fa5ddc0a4fc1a13ec8e584dc1ae9ff3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700823"
---
# <a name="command-line-options-for-configuration-manager-setup"></a>Opciones de línea de comandos para instalar Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Use la información siguiente para configurar scripts o para instalar Configuration Manager desde una línea de comandos.  

## <a name="command-line-options-for-setup"></a><a name="bkmk_setup"></a> Opciones de la línea de comandos para la instalación

Ejecute el programa de instalación desde el directorio `\BIN\X64` de la ruta de instalación de Configuration Manager en el servidor de sitio.

### `/DEINSTALL`

Desinstale el sitio. Ejecute el programa de instalación desde el equipo de servidor de sitio.  

### `/DONTSTARTSITECOMP`

Instala un sitio, pero evita que se inicie el servicio Administrador de componentes de sitio. El sitio estará inactivo hasta que no se inicie el servicio Administrador de componentes de sitio. El Administrador de componentes de sitio es responsable de instalar e iniciar el servicio SMS_Executive y de procesos adicionales en el sitio. Una vez completada la instalación del sitio, cuando se inicia el servicio Administrador de componentes de sitio, instala el servicio SMS_Executive y los procesos adicionales necesarios para que el sitio funcione.  

### `/HIDDEN`

Oculta la interfaz de usuario durante la instalación. Use esta opción solamente en combinación con la opción **/SCRIPT**. El archivo de script desatendido debe proporcionar todas las opciones necesarias o se produce un error en la instalación.  

### `/NOUSERINPUT`

Deshabilita la entrada del usuario durante la instalación, pero muestra el Asistente para la instalación. Use esta opción solamente en combinación con la opción **/SCRIPT**. El archivo de script desatendido debe proporcionar todas las opciones necesarias o se produce un error en la instalación.  

### `/RESETSITE`

Ejecuta el restablecimiento de un sitio; se restablecen las cuentas del servicio y la base de datos del sitio.

Para obtener más información, vea [Ejecutar un restablecimiento de sitio](../../manage/modify-your-infrastructure.md#bkmk_reset).  

### `/TESTDBUPGRADE`

Ejecuta una prueba en una copia de seguridad de la base de datos del sitio para asegurarse de que la base de datos puede actualizarse.

> [!IMPORTANT]  
> No ejecute esta opción de línea de comandos en la base de datos del sitio de producción. Ejecutar esta opción de línea de comandos en la base de datos del sitio de producción actualiza la base de datos del sitio y podría inutilizar el sitio.

#### <a name="usage"></a>Uso

Proporcione el nombre de instancia y el nombre de base de datos de la base de datos del sitio. Si solo se especifica el nombre de base de datos, el programa de instalación usa el nombre de instancia predeterminado.  

`/TESTDBUPGRADE <Instance name>\<Database name>`

`/TESTDBUPGRADE CM_ABC`

`/TESTDBUPGRADE Named\CM_ABC`

### `/UPGRADE`

Ejecuta una actualización desatendida de un sitio. Debe especificarse la clave del producto, incluidos los guiones (`-`). Además, se debe especificar la ruta de acceso a los archivos de requisitos previos de instalación descargados anteriormente.  

Para obtener más información sobre los archivos de requisitos previos de la instalación, vea [Descargador del programa de instalación](setup-downloader.md).  

#### <a name="usage"></a>Uso

`setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx <path to external component files>`  

### `/SCRIPT`

Ejecuta una instalación desatendida. Use un archivo de inicialización de instalación con esta opción. Para obtener más información sobre cómo ejecutar una instalación desatendida, vea [Usar una línea de comandos para instalar sitios de System Center Configuration Manager](use-a-command-line-to-install-sites.md).  

#### <a name="usage"></a>Uso

`/SCRIPT <setup script path>`

### `/SDKINST`

Instala el proveedor de SMS en el equipo especificado. Proporcione el nombre de dominio completo (FQDN) para el equipo del proveedor de SMS. Para obtener más información sobre el proveedor de SMS, vea [Plan para el proveedor de SMS](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

#### <a name="usage"></a>Uso

`/SDKINST <SMS Provider FQDN>`

### `/SDKDEINST`

Desinstala el proveedor de SMS en el equipo especificado. Proporcione el FQDN del equipo de proveedor de SMS.  

#### <a name="usage"></a>Uso

`/SDKDEINST <SMS Provider FQDN>`

### `/MANAGELANGS`

Administra los idiomas que están instalados en un sitio instalado previamente. Proporcione la ubicación del archivo de script de idioma que contiene la configuración de idioma. Para obtener más información, consulte la sección [Opciones de línea de comandos para administrar idiomas](#bkmk_Lang).  

#### <a name="usage"></a>Uso

`/MANAGELANGS <Language script path>`


## <a name="command-line-options-to-manage-languages"></a><a name="bkmk_Lang"></a> Opciones de línea de comandos para administrar idiomas

### <a name="identification"></a>Identificación

- **Nombre de clave:** Acción  

    - **Obligatorio:** Sí  

    - **Valores:** `ManageLanguages`  

    - **Detalles:** administra el servidor, el cliente y el soporte de idioma de cliente móvil en un sitio.  

### <a name="options"></a>Options

- **Nombre de clave:** AddServerLanguages  

    - **Obligatorio:** No  

    - **Valores** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Detalles:** especifica los idiomas de servidor que estarán disponibles para la consola de Configuration Manager, los informes y los objetos de Configuration Manager. El inglés está disponible de forma predeterminada.  

- **Nombre de clave:** AddClientLanguages  

    - **Obligatorio:** No  

    - **Valores** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Detalles:** Especifica los idiomas que estarán disponibles para los equipos cliente. El inglés está disponible de forma predeterminada.  

- **Nombre de clave:** DeleteServerLanguages  

    - **Obligatorio:** No  

    - **Valores** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Detalles:** Especifica los idiomas que se quitarán y que ya no estarán disponibles para la consola, los informes y los objetos de Configuration Manager. El inglés está disponible de forma predeterminada y no se puede quitar.  

- **Nombre de clave:** DeleteClientLanguages  

    - **Obligatorio:** No  

    - **Valores** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Detalles:** Especifica los idiomas para quitar y cuáles ya no estarán disponibles para los equipos cliente. El inglés está disponible de forma predeterminada y no se puede quitar.  

- **Nombre de clave:** MobileDeviceLanguage  

    - **Obligatorio:** Sí  

    - **Valores**

        - `0`: no instalar  

        - `1`: instalar  

    - **Detalles:** especifica si están instalados los idiomas de cliente del dispositivo móvil.  

- **Nombre de clave:** PrerequisiteComp  

    - **Obligatorio:** Sí  

    - **Valores**

        - `0`: descargar  

        - `1`: ya se ha descargado  

    - **Detalles:** especifica si se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si usa un valor de `0`, el programa de instalación descargará los archivos.  

- **Nombre de clave:** PrerequisitePath  

    - **Obligatorio:** Sí  

    - **Valores:**  <*ruta de acceso a los archivos de requisitos previos de instalación*>  

    - **Detalles:** especifica la ruta de acceso a los archivos de requisitos previos de instalación. En función del valor **PrerequisiteComp**, el programa de instalación usa esta ruta de acceso para almacenar los archivos descargados o localizar los archivos descargados previamente.  


## <a name="unattended-setup-script-file-keys"></a><a name="bkmk_Unattended"></a> Claves de archivo de scripts de instalación desatendida

Use las secciones siguientes para crear el script para la instalación desatendida. Las listas muestran:

- Claves de script de instalación disponibles y sus valores correspondientes
- Necesidad de incorporarlas
- Tipo de instalación para el que se usan
- Breve descripción de la clave

### <a name="unattended-install-for-a-central-administration-site-cas"></a>Instalación desatendida de un sitio de administración central (CAS)

Use los detalles siguientes para instalar un CAS mediante un archivo de script de instalación desatendida.  

#### <a name="identification"></a>Identificación

- **Nombre de clave:** Acción  

    - **Obligatorio:** Sí  

    - **Valores:** `InstallCAS`  

    - **Detalles:** instala un CAS.  

- **Nombre de clave:** CDLatest  

    - **Obligatorio:** sí, solo cuando se usan medios de la carpeta CD.Latest.

    - **Valores**

        - `1`: está usando medios de CD.Latest

        - Cualquier valor distinto de 1 indica que no se están usando medios de CD.Latest

    - **Detalles:** si se instala o recupera un sitio primario o CAS, y se ejecuta el programa de instalación desde la carpeta CD.Latest, debe incluirse esta clave y valor. Este valor indica al programa de instalación que se están usando medios de la carpeta CD.Latest.

#### <a name="options"></a>Options

- **Nombre de clave:** ProductID  

    - **Obligatorio:** Sí  

    - **Valores**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`: clave de producto válida con guiones

        - `Eval`: instalar la versión de evaluación de Configuration Manager

    - **Detalles:** especifica la clave de producto de instalación de Configuration Manager, incluidos los guiones.

- **Nombre de clave:** SiteCode  

    - **Obligatorio:** Sí  

    - **Valores:**  <*código de sitio*>, por ejemplo, `ABC`

    - **Detalles:** especifica los tres caracteres alfanuméricos que identifican el sitio de forma única en la jerarquía.  

- **Nombre de clave:** nombre de sitio.  

    - **Obligatorio:** Sí  

    - **Valores:**  <*nombre de sitio*>  

    - **Detalles:** especifica el nombre para este sitio.  

- **Nombre de clave:** SMSInstallDir  

    - **Obligatorio:** Sí  

    - **Valores:**  <*ruta de instalación de Configuration Manager*>  

    - **Detalles:** especifica la carpeta de instalación de los archivos de programa de Configuration Manager.  

- **Nombre de clave:** SDKServer  

    - **Obligatorio:** Sí  

    - **Valores:**  <*FQDN del proveedor de SMS*>  

    - **Detalles:** especifica el FQDN del servidor que hospedará el proveedor de SMS. Puede configurar proveedores de SMS adicionales para el sitio después de la instalación inicial.  

- **Nombre de clave:** PrerequisiteComp  

    - **Obligatorio:** Sí  

    - **Valores**

        - `0`: descargar  

        - `1`: ya se ha descargado  

    - **Detalles:** especifica si se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si usa un valor de `0`, el programa de instalación descargará los archivos.  

- **Nombre de clave:** PrerequisitePath  

    - **Obligatorio:** Sí  

    - **Valores:**  <*ruta de acceso a los archivos de requisitos previos de instalación*>  

    - **Detalles:** especifica la ruta de acceso a los archivos de requisitos previos de instalación. En función del valor **PrerequisiteComp**, el programa de instalación usa esta ruta de acceso para almacenar los archivos descargados o localizar los archivos descargados previamente.  

- **Nombre de clave:** AdminConsole  

    - **Obligatorio:** Sí  

    - **Valores**

        - `0`: no instalar  

        - `1`: instalar  

    - **Detalles:** especifica si se va a instalar la consola de Configuration Manager.  

- **Nombre de clave:** JoinCEIP  

    > [!Note]  
    > A partir de la versión 1802 de Configuration Manager, la característica CEIP se ha quitado del producto.

    - **Obligatorio:** Sí  

    - **Valores**

        - `0`: no unirse  

        - `1`: unirse  

    - **Detalles:** Especifica si se va a participar en el Programa para la mejora de la experiencia del usuario (CEIP).  

- **Nombre de clave:** AddServerLanguages  

    - **Obligatorio:** No  

    - **Valores** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Detalles:** especifica los idiomas de servidor que estarán disponibles para la consola de Configuration Manager, los informes y los objetos de Configuration Manager. El inglés está disponible de forma predeterminada.  

- **Nombre de clave:** AddClientLanguages  

    - **Obligatorio:** No  

    - **Valores** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Detalles:** Especifica los idiomas que estarán disponibles para los equipos cliente. El inglés está disponible de forma predeterminada.  

- **Nombre de clave:** DeleteServerLanguages  

    - **Obligatorio:** No  

    - **Valores** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Detalles:** modifica un sitio después de instalarlo. Especifica los idiomas que se quitarán y que ya no estarán disponibles para la consola, los informes y los objetos de Configuration Manager. El inglés está disponible de forma predeterminada y no se puede quitar.  

- **Nombre de clave:** DeleteClientLanguages  

    - **Obligatorio:** No  

    - **Valores** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Detalles:** modifica un sitio después de instalarlo. Especifica los idiomas para quitar y cuáles ya no estarán disponibles para los equipos cliente. El inglés está disponible de forma predeterminada y no se puede quitar.  

- **Nombre de clave:** MobileDeviceLanguage  

    - **Obligatorio:** Sí  

    - **Valores**

        - `0`: no instalar  

        - `1`: instalar  

    - **Detalles:** especifica si están instalados los idiomas de cliente del dispositivo móvil.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Nombre de clave:** SQLServerName  

    - **Obligatorio:** Sí  

    - **Valores:**  <*nombre de servidor SQL*>  

    - **Detalles:** especifica el nombre del servidor o de la instancia en clúster que ejecuta SQL Server donde se hospedará la base de datos del sitio.  

- **Nombre de clave:** DatabaseName  

    - **Obligatorio:** Sí  

    - **Valores:**  <*nombre de base de datos de sitio*> o <*nombre de instancia*>\\<*nombre de base de datos de sitio*>  

    - **Detalles:** especifica el nombre de la base de datos de SQL Server que se va a crear o a usar cuando el programa de instalación instala la base de datos del sitio CAS.  

        > [!IMPORTANT]  
        > Si no se usa la instancia predeterminada, se debe especificar el nombre de instancia y el nombre de la base de datos del sitio.  

- **Nombre de clave:** SQLSSBPort  

    - **Obligatorio:** No  

    - **Valores:**  <*número de puerto SSB*>  

    - **Detalles:** especifica el puerto de SQL Server Service Broker (SSB) que SQL Server utiliza. De forma predeterminada, SSB usa el puerto TCP 4022, pero puede utilizarse otro puerto.  

- **Nombre de clave:** SQLDataFilePath  

    - **Obligatorio:** No  

    - **Valores:**  <*ruta de acceso al archivo .mdb de base de datos*>  

    - **Detalles:** especifica una ubicación alternativa para crear el archivo .mdb de base de datos.  

- **Nombre de clave:** SQLLogFilePath  

    - **Obligatorio:** No  

    - **Valores:**  <*ruta de acceso al archivo .ldf de base de datos*>  

    - **Detalles:** especifica una ubicación alternativa para crear el archivo .ldf de base de datos.  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Nombre de clave:** CloudConnector  

    - **Obligatorio:** Sí  

    - **Valores**

        - `0`: no instalar  

        - `1`: instalar  

    - **Detalles:** especifica si se instala un punto de conexión de servicio en este sitio. Dado que el punto de conexión de servicio solo puede instalarse en el sitio de nivel superior de una jerarquía, este valor debe establecerse en `1` para un sitio principal secundario.  

- **Nombre de clave:** CloudConnectorServer  

    - **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1.  

    - **Valores:**  <*FQDN del servidor de punto de conexión de servicio*>  

    - **Detalles:** especifica el FQDN del servidor que hospedará el rol de sistema de sitio del punto de conexión de servicio.  

- **Nombre de clave:** UseProxy  

    - **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1.  

    - **Valores**

        - `0`: no instalar  

        - `1`: instalar  

    - **Detalles:** especifica si el punto de conexión de servicio usa un servidor proxy.  

- **Nombre de clave:** ProxyName  

    - **Obligatorio:** obligatorio cuando **UseProxy** es igual a 1.  

    - **Valores:**  <*FQDN del servidor proxy*>  

    - **Detalles:** especifica el FQDN del servidor proxy que usa el punto de conexión de servicio.  

- **Nombre de clave:** ProxyPort  

    - **Obligatorio:** obligatorio cuando **UseProxy** es igual a 1.  

    - **Valores:**  <*número de puerto*>  

    - **Detalles:** especifica el número de puerto que se usará para el puerto de proxy.  

#### <a name="sabranchoptions"></a>SABranchOptions

<!-- SCCMDocs#390 -->

- **Nombre de clave:** SAActive

    - **Obligatorio:** No

    - **Valores**

        - `0`: no tiene Software Assurance

        - `1`: Software Assurance está activo

    - **Detalles:** especifique si tiene Software Assurance activo. Para obtener más información, vea [Preguntas más frecuentes sobre productos y licencias](../../../understand/product-and-licensing-faq.md).

- **Nombre de clave:** CurrentBranch

    - **Obligatorio:** No

    - **Valores**

        - `0`: instalar el LTSB

        - `1`: instalar la rama actual

    - **Detalles:** especifique si debe usarse la rama actual de Configuration Manager o la rama de mantenimiento a largo plazo (LTSB). Consulte [¿Qué rama de Configuration Manager debo utilizar?](../../../understand/which-branch-should-i-use.md) para obtener más información.

### <a name="unattended-install-for-a-primary-site"></a>Instalación desatendida de un sitio principal

Use los detalles siguientes para instalar un sitio primario mediante un archivo de script de instalación desatendida.  

#### <a name="identification"></a>Identificación

- **Nombre de clave:** Acción  

    - **Obligatorio:** Sí  

    - **Valores:** `InstallPrimarySite`  

    - **Detalles:** instala un sitio primario.  

- **Nombre de clave:** CDLatest  

    - **Obligatorio:** sí, solo cuando se usan medios de la carpeta CD.Latest.

    - **Valores**

        - `1`: está usando medios de CD.Latest

        - Cualquier valor distinto de 1 indica que no se están usando medios de CD.Latest

    - **Detalles:** si se instala o recupera un sitio primario o CAS, y se ejecuta el programa de instalación desde la carpeta CD.Latest, debe incluirse esta clave y valor. Este valor indica al programa de instalación que se están usando medios de la carpeta CD.Latest.

#### <a name="options"></a>Options

- **Nombre de clave:** ProductID  

    - **Obligatorio:** Sí  

    - **Valores**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`: clave de producto válida con guiones

        - `Eval`: instalar la versión de evaluación de Configuration Manager

    - **Detalles:** especifica la clave de producto de instalación de Configuration Manager, incluidos los guiones.

- **Nombre de clave:** SiteCode  

    - **Obligatorio:** Sí  

    - **Valores:**  <*código de sitio*>  

    - **Detalles:** especifica los tres caracteres alfanuméricos que identifican el sitio de forma única en la jerarquía.  

- **Nombre de clave:** SiteName  

    - **Obligatorio:** Sí  

    - **Valores:**  <*nombre de sitio*>  

    - **Detalles:** especifica el nombre para este sitio.  

- **Nombre de clave:** SMSInstallDir  

    - **Obligatorio:** Sí  

    - **Valores:**  <*ruta de instalación de Configuration Manager*>

    - **Detalles:** especifica la carpeta de instalación de los archivos de programa de Configuration Manager.  

- **Nombre de clave:** SDKServer  

    - **Obligatorio:** Sí  

    - **Valores:**  <*FQDN del proveedor de SMS*>  

    - **Detalles:** especifica el FQDN del servidor que hospedará el proveedor de SMS. Puede configurar proveedores de SMS adicionales para el sitio después de la instalación inicial.  

- **Nombre de clave:** PrerequisiteComp  

    - **Obligatorio:** Sí  

    - **Valores**

        - `0`: descargar  

        - `1`: ya se ha descargado  

    - **Detalles:** especifica si se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si usa un valor de `0`, el programa de instalación descargará los archivos.  

- **Nombre de clave:** PrerequisitePath  

    - **Obligatorio:** Sí  

    - **Valores:**  <*ruta de acceso a los archivos de requisitos previos de instalación*>  

    - **Detalles:** especifica la ruta de acceso a los archivos de requisitos previos de instalación. En función del valor **PrerequisiteComp**, el programa de instalación usa esta ruta de acceso para almacenar los archivos descargados o localizar los archivos descargados previamente.  

- **Nombre de clave:** AdminConsole  

    - **Obligatorio:** Sí  

    - **Valores**

        - `0`: no instalar  

        - `1`: instalar  

    - **Detalles:** especifica si se va a instalar la consola de Configuration Manager.  

- **Nombre de clave:** JoinCEIP  

    > [!Note]  
    > A partir de la versión 1802 de Configuration Manager, la característica CEIP se ha quitado del producto.

    - **Obligatorio:** Sí  

    - **Valores**

        - `0`: no unirse  

        - `1`: unirse  

    - **Detalles:** especifica si se unirá al CEIP.  

- **Nombre de clave:** ManagementPoint  

    - **Obligatorio:** No  

    - **Valores:**  <*FQDN del servidor de sitio de punto de administración*>  

    - **Detalles:** especifica el FQDN del servidor que hospedará el rol de sistema de sitio de punto de administración.  

- **Nombre de clave:** ManagementPointProtocol  

    - **Obligatorio:** No  

    - **Valores:** `HTTPS` o `HTTP`  

    - **Detalles:** especifica el protocolo que se utilizará para el punto de administración.  

- **Nombre de clave:** DistributionPoint  

    - **Obligatorio:** No  

    - **Valores:**  <*FQDN del servidor de sitio de punto de distribución*>  

    - **Detalles:** especifica el FQDN del servidor que hospedará el rol de sistema de sitio de punto de distribución.  

- **Nombre de clave:** DistributionPointProtocol  

    - **Obligatorio:** No  

    - **Valores:** `HTTPS` o `HTTP`  

    - **Detalles:** especifica el protocolo que se utilizará para el punto de distribución.  

- **Nombre de clave:** RoleCommunicationProtocol  

    - **Obligatorio:** Sí  

    - **Valores:** `EnforceHTTPS` o `HTTPorHTTPS`  

    - **Detalles:** especifica si se van a configurar todos los sistemas de sitio para aceptar solo las comunicaciones HTTPS de los clientes, o si se va a configurar el método de comunicación para cada rol de sistema de sitio. Al seleccionar `EnforceHTTPS`, los clientes deben tener un certificado de infraestructura de clave pública (PKI) válido para la autenticación de cliente.  

- **Nombre de clave:** ClientsUsePKICertificate  

    - **Obligatorio:** Sí  

    - **Valores**

        - `0`: no usar  

        - `1`: usar  

    - **Detalles:** especifica si los clientes van a utilizar un certificado PKI de cliente para comunicarse con roles de sistema de sitio.  

- **Nombre de clave:** AddServerLanguages  

    - **Obligatorio:** No  

    - **Valores** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Detalles:** especifica los idiomas de servidor que estarán disponibles para la consola de Configuration Manager, los informes y los objetos de Configuration Manager. El inglés está disponible de forma predeterminada.  

- **Nombre de clave:** AddClientLanguages  

    - **Obligatorio:** No  

    - **Valores** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Detalles:** Especifica los idiomas que estarán disponibles para los equipos cliente. El inglés está disponible de forma predeterminada.  

- **Nombre de clave:** DeleteServerLanguages  

    - **Obligatorio:** No  

    - **Valores** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Detalles:** modifica un sitio después de instalarlo. Especifica los idiomas que se quitarán y que ya no estarán disponibles para la consola, los informes y los objetos de Configuration Manager. El inglés está disponible de forma predeterminada y no se puede quitar.  

- **Nombre de clave:** DeleteClientLanguages  

    - **Obligatorio:** No  

    - **Valores** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    - **Detalles:** modifica un sitio después de instalarlo. Especifica los idiomas para quitar y cuáles ya no estarán disponibles para los equipos cliente. El inglés está disponible de forma predeterminada y no se puede quitar.  

- **Nombre de clave:** MobileDeviceLanguage  

    - **Obligatorio:** Sí  

    - **Valores**

        - `0`: no instalar  

        - `1`: instalar  

    - **Detalles:** especifica si están instalados los idiomas de cliente del dispositivo móvil.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Nombre de clave:** SQLServerName  

    - **Obligatorio:** Sí  

    - **Valores:**  <*nombre de servidor SQL*>  

    - **Detalles:** especifica el nombre del servidor o de la instancia en clúster que ejecuta SQL Server donde se hospedará la base de datos del sitio.  

- **Nombre de clave:** DatabaseName  

    - **Obligatorio:** Sí  

    - **Valores:**  <*nombre de base de datos de sitio*> o <*nombre de instancia*>\\<*nombre de base de datos de sitio*>  

    - **Detalles:** especifica el nombre de la base de datos de SQL Server que se crea o usa para instalar la base de datos del sitio primario.  

        > [!IMPORTANT]  
        > Si no se usa la instancia predeterminada, se debe especificar el nombre de instancia y el nombre de la base de datos del sitio.  

- **Nombre de clave:** SQLSSBPort  

    - **Obligatorio:** No  

    - **Valores:**  <*número de puerto SSB*>  

    - **Detalles:** especifica el puerto SSB que usa SQL Server. De forma predeterminada, SSB usa el puerto TCP 4022, pero puede utilizarse otro puerto.  

- **Nombre de clave:** SQLDataFilePath  

    - **Obligatorio:** No  

    - **Valores:**  <*ruta de acceso al archivo .mdb de base de datos*>  

    - **Detalles:** especifica una ubicación alternativa para crear el archivo .mdb de base de datos.  

- **Nombre de clave:** SQLLogFilePath  

    - **Obligatorio:** No  

    - **Valores:**  <*ruta de acceso al archivo .ldf de base de datos*>  

    - **Detalles:** especifica una ubicación alternativa para crear el archivo .ldf de base de datos.  

#### <a name="hierarchyexpansionoption"></a>HierarchyExpansionOption

- **Nombre de clave:** CCARSiteServer  

    - **Obligatorio:** No  

    - **Valores:**  <*FQDN del sitio de administración central*>  

    - **Detalles:** especifica el CAS al que se asocia un sitio primario cuando se une a la jerarquía de Configuration Manager. Especifique el CAS durante la instalación.  

- **Nombre de clave:** CASRetryInterval  

    - **Obligatorio:** No  

    - **Valores:**  <*intervalo en minutos*>  

    - **Detalles:** especifica el intervalo de reintento en minutos para tratar de establecer una conexión con el CAS después de que se produce el error de conexión. Por ejemplo, si se produce un error en la conexión al CAS, el sitio primario espera el número de minutos especificado para el valor **CASRetryInterval** y, después, vuelve a intentar la conexión.  

- **Nombre de clave:** WaitForCASTimeout  

    - **Obligatorio:** No  

    - **Valores:**  <*tiempo de expiración en minutos de 0 a 100*>  

    - **Detalles:** especifica el valor de tiempo de espera máximo en minutos de un sitio primario para conectarse al CAS. Por ejemplo, si se produce un error de conexión del sitio primario con el CAS, el sitio primario vuelve a tratar de establecer la conexión conforme al valor **CASRetryInterval** hasta que se alcanza el valor de tiempo de **WaitForCASTimeout**. Se puede especificar un valor de `0` a `100`.  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Nombre de clave:** CloudConnector  

    - **Obligatorio:** Sí  

    - **Valores**

        - `0`: no instalar  

        - `1`: instalar  

    - **Detalles:** especifica si se instala un punto de conexión de servicio en este sitio. Dado que el punto de conexión de servicio solo puede instalarse en el sitio de nivel superior de una jerarquía, este valor debe establecerse en `0` para un sitio principal secundario.  

- **Nombre de clave:** CloudConnectorServer  

    - **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1.  

    - **Valores:**  <*FQDN del servidor de punto de conexión de servicio*\>  

    - **Detalles:** especifica el FQDN del servidor que hospedará el rol de sistema de sitio del punto de conexión de servicio.  

- **Nombre de clave:** UseProxy  

    - **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1.  

    - **Valores**

        - `0`: no instalar  

        - `1`: instalar  

    - **Detalles:** especifica si el punto de conexión de servicio usa un servidor proxy.  

- **Nombre de clave:** ProxyName  

    - **Obligatorio:** obligatorio cuando **UseProxy** es igual a 1.  

    - **Valores:**  <*FQDN del servidor proxy*>  

    - **Detalles:** especifica el FQDN del servidor proxy que usa el punto de conexión de servicio.  

- **Nombre de clave:** ProxyPort  

    - **Obligatorio:** obligatorio cuando **UseProxy** es igual a 1.  

    - **Valores:**  <*número de puerto*>  

    - **Detalles:** especifica el número de puerto que se usará para el puerto de proxy.  

#### <a name="sabranchoptions"></a>SABranchOptions

<!-- SCCMDocs#390 -->

- **Nombre de clave:** SAActive

    - **Obligatorio:** No

    - **Valores**

        - `0`: no tiene Software Assurance

        - `1`: Software Assurance está activo

    - **Detalles:** especifique si tiene Software Assurance activo. Para obtener más información, vea [Preguntas más frecuentes sobre productos y licencias](../../../understand/product-and-licensing-faq.md).

- **Nombre de clave:** CurrentBranch

    - **Obligatorio:** No

    - **Valores**

        - `0`: instalar el LTSB

        - `1`: instalar la rama actual

    - **Detalles:** especifique si debe usarse la rama actual de Configuration Manager o la rama de mantenimiento a largo plazo (LTSB). Consulte [¿Qué rama de Configuration Manager debo utilizar?](../../../understand/which-branch-should-i-use.md) para obtener más información.

### <a name="unattended-recovery-for-a-cas"></a>Recuperación desatendida de un CAS

Use los detalles siguientes para recuperar un CAS mediante un archivo de script de instalación desatendida.  

#### <a name="identification"></a>Identificación

- **Nombre de clave:** Acción  

    - **Obligatorio:** Sí  

    - **Valores:** `RecoverCCAR`  

    - **Detalles:** recupera un CAS.  

- **Nombre de clave:** CDLatest  

    - **Obligatorio:** sí, solo cuando se usan medios de la carpeta CD.Latest.

    - **Valores**

        - `1`: está usando medios de CD.Latest

        - Cualquier valor distinto de 1 indica que no se están usando medios de CD.Latest

    - **Detalles:** si se instala o recupera un sitio primario o CAS, y se ejecuta el programa de instalación desde la carpeta CD.Latest, debe incluirse esta clave y valor. Este valor indica al programa de instalación que se están usando medios de la carpeta CD.Latest.

#### <a name="recoveryoptions"></a>RecoveryOptions

- **Nombre de clave:** ServerRecoveryOptions  

    - **Obligatorio:** Sí  

    - **Valores**

        - `1`: recuperar el servidor de sitio y SQL Server

        - `2`: recuperar solo el servidor de sitio

        - `4`: recuperar solo SQL Server  

    - **Detalles:** especifica si el programa de instalación recupera el servidor de sitio, SQL Server o ambos. Las siguientes opciones también son necesarias en función del valor especificado:  

        - **1** o **2**: Para recuperar el sitio mediante una copia de seguridad de sitio, especifique un valor para **SiteServerBackupLocation**. Si no se especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

        - **4**: se requiere la clave **BackupLocation** cuando configura un valor de **10** para la clave **DatabaseRecoveryOptions** , que se utiliza para restaurar la base de datos de sitio desde la copia de seguridad.  

- **Nombre de clave:** DatabaseRecoveryOptions  

    - **Obligatorio:** Esta clave es necesaria cuando **ServerRecoveryOptions** tiene un valor de **1** o **4**.  

    - **Valores**

        - `10`: restaurar la base de datos de sitio desde la copia de seguridad.  

        - `20`: usar una base de datos de sitio que se ha recuperado manualmente mediante otro método.  

        - `40`: crear una base de datos para el sitio. Use esta opción si no hay ninguna copia de seguridad de base de datos de sitio disponible. El sitio recupera los datos globales y de sitio mediante la replicación desde otros sitios.  

        - `80`: omitir la recuperación de la base de datos.  

    - **Detalles:** especifica cómo recupera el programa de instalación la base de datos de sitio en SQL Server.  

- **Nombre de clave:** ReferenceSite  

    - **Obligatorio:** Esta clave es necesaria cuando **DatabaseRecoveryOptions** tiene un valor de **40**.  

    - **Valores:**  <*FQDN del sitio de referencia*>  

    - **Detalles:** si la copia de seguridad de la base de datos es anterior al período de retención de seguimiento de cambios, o si se recupera el sitio sin usar una copia de seguridad, especifique el sitio primario de referencia que usa el CAS para recuperar los datos globales.  

        Si no especifica ningún sitio de referencia y la copia de seguridad es anterior al período de retención de seguimiento de cambios, todos los sitios primarios se reinicializan con los datos restaurados desde el CAS.  

        Si no especifica ningún sitio de referencia y la copia de seguridad pertenece al período de retención de seguimiento de cambios, solo se replicarán desde los sitios primarios los cambios que tuvieron lugar después de la copia de seguridad. Si existen cambios en conflicto de varios sitios primarios, el CAS usa el primero que recibe.  

- **Nombre de clave:** SiteServerBackupLocation  

    - **Obligatorio:** No  

    - **Valores:**  <*ruta de acceso al conjunto de copia de seguridad de servidor de sitio*>  

    - **Detalles:** Especifica la ruta de acceso para el conjunto de copia de seguridad del servidor de sitio. Esta clave es opcional si la opción **ServerRecoveryOptions** tiene un valor de **1** o **2**. Especifique un valor para la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no se especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

- **Nombre de clave:** BackupLocation  

    - **Obligatorio:** esta clave es obligatoria cuando se configura un valor de **1** o **4** para la clave **ServerRecoveryOptions** y cuando se configura un valor de **10** para la clave **DatabaseRecoveryOptions**.  

    - **Valores:**  <*ruta de acceso al conjunto de copia de seguridad de sitio*>  

    - **Detalles:** especifica la ruta de acceso al conjunto de copia de seguridad de base de datos de sitio.  

#### <a name="options"></a>Options

- **Nombre de clave:** ProductID  

    - **Obligatorio:** Sí  

    - **Valores**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`: clave de producto válida con guiones

        - `Eval`: instalar la versión de evaluación de Configuration Manager

    - **Detalles:** especifica la clave de producto de instalación de Configuration Manager, incluidos los guiones.

- **Nombre de clave:** SiteCode  

    - **Obligatorio:** Sí  

    - **Valores:**  <*código de sitio*>  

    - **Detalles:** especifica los tres caracteres alfanuméricos que identifican el sitio de forma única en la jerarquía. Especifique el código de sitio que usó el sitio antes de producirse el error.

- **Nombre de clave:** SiteName  

    - **Obligatorio:** No  

    - **Valores:**  <*nombre de sitio*>  

    - **Detalles:** especifica el nombre para este sitio.  

- **Nombre de clave:** SMSInstallDir  

    - **Obligatorio:** Sí  

    - **Valores:**  <*ruta de instalación de Configuration Manager*>  

    - **Detalles:** especifica la carpeta de instalación de los archivos de programa de Configuration Manager.  

- **Nombre de clave:** SDKServer  

    - **Obligatorio:** Sí  

    - **Valores:**  <*FQDN del proveedor de SMS*>  

    - **Detalles:** especifica el FQDN del servidor que hospeda el proveedor de SMS. Especifique el servidor que hospedaba el proveedor de SMS antes de producirse el error.  

        Después de la instalación inicial, puede configurar otros proveedores de SMS para el sitio. Para obtener más información sobre el proveedor de SMS, vea [Plan para el proveedor de SMS](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

- **Nombre de clave:** PrerequisiteComp  

    - **Obligatorio:** Sí  

    - **Valores**

        - `0`: descargar  

        - `1`: ya se ha descargado  

    - **Detalles:** especifica si se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si usa un valor de **0**, el programa de instalación descarga los archivos.  

- **Nombre de clave:** PrerequisitePath  

    - **Obligatorio:** Sí  

    - **Valores:**  <*ruta de acceso a los archivos de requisitos previos de instalación*>  

    - **Detalles:** especifica la ruta de acceso a los archivos de requisitos previos de instalación. En función del valor **PrerequisiteComp**, el programa de instalación usa esta ruta de acceso para almacenar los archivos descargados o localizar los archivos descargados previamente.  

- **Nombre de clave:** AdminConsole  

    - **Obligatorio:** Esta clave es necesaria, salvo cuando **ServerRecoveryOptions** tiene un valor de **4**.  

    - **Valores**

        - `0`: no instalar  

        - `1`: instalar  

    - **Detalles:** especifica si se va a instalar la consola de Configuration Manager.  

- **Nombre de clave:** JoinCEIP  

    > [!Note]  
    > A partir de la versión 1802 de Configuration Manager, la característica CEIP se ha quitado del producto.

    - **Obligatorio:** Sí  

    - **Valores**

        - `0`: no unirse  

        - `1`: unirse  

    - **Detalles:** especifica si se unirá al CEIP.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Nombre de clave:** SQLServerName  

    - **Obligatorio:** Sí  

    - **Valores:**  <*nombre de servidor SQL*>  

    - **Detalles:** especifica el nombre del servidor o de la instancia en clúster que ejecuta SQL Server, y cuál hospeda la base de datos del sitio. Especifique el mismo servidor que hospedaba la base de datos del sitio antes de producirse el error.  

- **Nombre de clave:** DatabaseName  

    - **Obligatorio:** Sí  

    - **Valores:**  <*nombre de base de datos de sitio*> o <*nombre de instancia*>\\<*nombre de base de datos de sitio*>  

    - **Detalles:** especifica el nombre de la base de datos de SQL Server que se crea o usa para instalar la base de datos del CAS. Especifique el mismo nombre de base de datos que se usó antes de producirse el error.  

        > [!IMPORTANT]  
        > Si no se usa la instancia predeterminada, se debe especificar el nombre de instancia y el nombre de la base de datos del sitio.  

- **Nombre de clave:** SQLSSBPort  

    - **Obligatorio:** Sí  

    - **Valores:**  <*número de puerto SSB*>  

    - **Detalles:** especifica el puerto SSB que usa SQL Server. De forma predeterminada, SSB usa el puerto TCP 4022. Especifique el mismo puerto SSB que se usó antes de producirse el error.  

- **Nombre de clave:** SQLDataFilePath  

    - **Obligatorio:** No  

    - **Valores:**  <*ruta de acceso al archivo .mdb de base de datos*>  

    - **Detalles:** especifica una ubicación alternativa para crear el archivo .mdb de base de datos.  

- **Nombre de clave:** SQLLogFilePath  

    - **Obligatorio:** No  

    - **Valores:**  <*ruta de acceso al archivo .ldf de base de datos*>  

    - **Detalles:** especifica una ubicación alternativa para crear el archivo .ldf de base de datos.  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Nombre de clave:** CloudConnector  

    - **Obligatorio:** Sí  

    - **Valores**

        - `0`: no instalar  

        - `1`: instalar  

    - **Detalles:** especifica si se instala un punto de conexión de servicio en este sitio. Dado que el punto de conexión de servicio solo puede instalarse en el sitio de nivel superior de una jerarquía, este valor debe ser **0** para un sitio principal secundario.  

- **Nombre de clave:** CloudConnectorServer  

    - **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1.  

    - **Valores:**  <*FQDN del servidor de punto de conexión de servicio*>  

    - **Detalles:** especifica el FQDN del servidor que hospedará el rol de sistema de sitio del punto de conexión de servicio.  

- **Nombre de clave:** UseProxy  

    - **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1.  

    - **Valores**

        - `0`: no instalar  

        - `1`: instalar  

    - **Detalles:** especifica si el punto de conexión de servicio usa un servidor proxy.  

- **Nombre de clave:** ProxyName  

    - **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1.  

    - **Valores:**  <*FQDN del servidor proxy*>  

    - **Detalles:** especifica el FQDN del servidor proxy que usa el punto de conexión de servicio.  

- **Nombre de clave:** ProxyPort  

    - **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1.  

    - **Valores:**  <*número de puerto*>  

    - **Detalles:** especifica el número de puerto que se usará para el puerto de proxy.  

### <a name="unattended-recovery-for-a-primary-site"></a>Recuperación desatendida de un sitio principal

Use los datos siguientes para recuperar un sitio primario mediante un archivo de script de instalación desatendida.  

#### <a name="identification"></a>Identificación

- **Nombre de clave:** Acción  

    - **Obligatorio:** Sí  

    - **Valores:** `RecoverPrimarySite`  

    - **Detalles:** recupera un sitio primario.  

- **Nombre de clave:** CDLatest  

    - **Obligatorio:** sí, solo cuando se usan medios de la carpeta CD.Latest.

    - **Valores**

        - `1`: está usando medios de CD.Latest

        - Cualquier valor distinto de 1 indica que no se están usando medios de CD.Latest

    - **Detalles:** si se instala o recupera un sitio primario o CAS, y se ejecuta el programa de instalación desde la carpeta CD.Latest, debe incluirse esta clave y valor. Este valor indica al programa de instalación que se están usando medios de la carpeta CD.Latest.

#### <a name="recoveryoptions"></a>RecoveryOptions

- **Nombre de clave:** ServerRecoveryOptions  

    - **Obligatorio:** Sí  

    - **Valores**

        - `1`: recuperar el servidor de sitio y SQL Server

        - `2`: recuperar solo el servidor de sitio

        - `4`: recuperar solo SQL Server  

    - **Detalles:** especifica si el programa de instalación recupera el servidor de sitio, SQL Server o ambos. Las siguientes opciones también son necesarias en función del valor especificado:  

        - **1** o **2**: Para recuperar el sitio mediante una copia de seguridad de sitio, especifique un valor para **SiteServerBackupLocation**. Si no se especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

        - **4**: se requiere la clave **BackupLocation** cuando configura un valor de **10** para la clave **DatabaseRecoveryOptions** , que se utiliza para restaurar la base de datos de sitio desde la copia de seguridad.  

- **Nombre de clave:** DatabaseRecoveryOptions  

    - **Obligatorio:** Esta clave es necesaria cuando **ServerRecoveryOptions** tiene un valor de **1** o **4**.  

    - **Valores**

        - `10`: restaurar la base de datos de sitio desde la copia de seguridad.  

        - `20`: usar una base de datos de sitio que se ha recuperado manualmente mediante otro método.  

        - `40`: crear una base de datos para el sitio. Use esta opción si no hay ninguna copia de seguridad de base de datos de sitio disponible. El sitio recupera los datos globales y de sitio mediante la replicación desde otros sitios.  

        - `80`: omitir la recuperación de la base de datos.  

    - **Detalles:** especifica cómo recupera el programa de instalación la base de datos de sitio en SQL Server.  

- **Nombre de clave:** SiteServerBackupLocation  

    - **Obligatorio:** No  

    - **Valores:**  <*ruta de acceso al conjunto de copia de seguridad de servidor de sitio*>  

    - **Detalles:** Especifica la ruta de acceso para el conjunto de copia de seguridad del servidor de sitio. Esta clave es opcional si la opción **ServerRecoveryOptions** tiene un valor de **1** o **2**. Especifique un valor para la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no se especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.  

- **Nombre de clave:** BackupLocation  

    - **Obligatorio:** esta clave es necesaria cuando se configura un valor de **1** o **4** para la clave **ServerRecoveryOptions** y cuando se configura un valor de **10** para la clave **DatabaseRecoveryOptions**.  

    - **Valores:**  <*ruta de acceso al conjunto de copia de seguridad de sitio*>  

    - **Detalles:** especifica la ruta de acceso al conjunto de copia de seguridad de base de datos de sitio.  

#### <a name="options"></a>Options

- **Nombre de clave:** ProductID  

    - **Obligatorio:** Sí  

    - **Valores**

        - `<xxxxx-xxxxx-xxxxx-xxxxx-xxxxx>`: clave de producto válida con guiones

        - `Eval`: instalar la versión de evaluación de Configuration Manager

    - **Detalles:** especifica la clave de producto de instalación de Configuration Manager, incluidos los guiones.

- **Nombre de clave:** SiteCode  

    - **Obligatorio:** Sí  

    - **Valores:**  <*código de sitio*>  

    - **Detalles:** especifica los tres caracteres alfanuméricos que identifican el sitio de forma única en la jerarquía. Especifique el código de sitio que usó el sitio antes de producirse el error.

- **Nombre de clave:** SiteName  

    - **Obligatorio:** No  

    - **Valores:**  <*nombre de sitio*>  

    - **Detalles:** especifica el nombre para este sitio.  

- **Nombre de clave:** SMSInstallDir  

    - **Obligatorio:** Sí  

    - **Valores:**  <*ruta de instalación de Configuration Manager*>  

    - **Detalles:** especifica la carpeta de instalación de los archivos de programa de Configuration Manager.  

- **Nombre de clave:** SDKServer  

    - **Obligatorio:** Sí  

    - **Valores:**  <*FQDN del proveedor de SMS*>  

    - **Detalles:** especifica el FQDN del servidor que hospeda el proveedor de SMS. Especifique el servidor que hospedaba el proveedor de SMS antes de producirse el error. Después de la instalación inicial, puede configurar otros proveedores de SMS para el sitio. Para obtener más información sobre el proveedor de SMS, vea [Plan para el proveedor de SMS](../../../plan-design/hierarchy/plan-for-the-sms-provider.md).  

- **Nombre de clave:** PrerequisiteComp  

    - **Obligatorio:** Sí  

    - **Valores**

        - `0`: descargar  

        - `1`: ya se ha descargado  

    - **Detalles:** especifica si se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si usa un valor de **0**, el programa de instalación descarga los archivos.  

- **Nombre de clave:** PrerequisitePath  

    - **Obligatorio:** Sí  

    - **Valores:**  <*ruta de acceso a los archivos de requisitos previos de instalación*>  

    - **Detalles:** especifica la ruta de acceso a los archivos de requisitos previos de instalación. En función del valor **PrerequisiteComp**, el programa de instalación usa esta ruta de acceso para almacenar los archivos descargados o localizar los archivos descargados previamente.  

- **Nombre de clave:** AdminConsole  

    - **Obligatorio:** Esta clave es necesaria, salvo cuando **ServerRecoveryOptions** tiene un valor de **4**.  

    - **Valores**

        - `0`: no instalar  

        - `1`: instalar  

    - **Detalles:** especifica si se va a instalar la consola de Configuration Manager.  

- **Nombre de clave:** JoinCEIP  

    > [!Note]  
    > A partir de la versión 1802 de Configuration Manager, la característica CEIP se ha quitado del producto.

    - **Obligatorio:** Sí  

    - **Valores**

        - `0`: no unirse  

        - `1`: unirse  

    - **Detalles:** especifica si se unirá al CEIP.  

#### <a name="sqlconfigoptions"></a>SQLConfigOptions

- **Nombre de clave:** SQLServerName  

    - **Obligatorio:** Sí  

    - **Valores:**  <*nombre de servidor SQL*>  

    - **Detalles:** especifica el nombre del servidor o de la instancia en clúster que ejecuta SQL Server donde se hospedará la base de datos del sitio. Especifique el mismo servidor que hospedaba la base de datos del sitio antes de producirse el error.  

- **Nombre de clave:** DatabaseName  

    - **Obligatorio:** Sí  

    - **Valores:**  <*nombre de base de datos de sitio*> o <*nombre de instancia*>\\<*nombre de base de datos de sitio*>

    - **Detalles:** especifica el nombre de la base de datos de SQL Server que se crea o usa para instalar la base de datos del CAS. Especifique el mismo nombre de base de datos que se usó antes de producirse el error.  

        > [!IMPORTANT]  
        > Si no se usa la instancia predeterminada, se debe especificar el nombre de instancia y el nombre de la base de datos del sitio.  

- **Nombre de clave:** SQLSSBPort  

    - **Obligatorio:** Sí  

    - **Valores:**  <*número de puerto SSB*>  

    - **Detalles:** especifica el puerto SSB que usa SQL Server. De forma predeterminada, SSB usa el puerto TCP 4022. Especifique el mismo puerto SSB que se usó antes de producirse el error.  

- **Nombre de clave:** SQLDataFilePath  

    - **Obligatorio:** No  

    - **Valores:**  <*ruta de acceso al archivo .mdb de base de datos*>  

    - **Detalles:** especifica una ubicación alternativa para crear el archivo .mdb de base de datos.  

- **Nombre de clave:** SQLLogFilePath  

    - **Obligatorio:** No  

    - **Valores:**  <*ruta de acceso al archivo .ldf de base de datos*>  

    - **Detalles:** especifica una ubicación alternativa para crear el archivo .ldf de base de datos.  

#### <a name="hierarchyexpansionoptions"></a>HierarchyExpansionOptions

- **Nombre de clave:** CCARSiteServer  

    - **Obligatorio:** ver detalles.  

    - **Valores:**  <*código de sitio para CAS*>  

    - **Detalles:** especifica el CAS al que se asocia un sitio primario cuando se une a la jerarquía de Configuration Manager. Esta configuración es necesaria si el sitio primario estaba asociado con un CAS antes de producirse el error. Especifique el código de sitio que usó para el CAS antes de que se produjera el error.  

- **Nombre de clave:** CASRetryInterval  

    - **Obligatorio:** No  

    - **Valores:**  <*intervalo en minutos*>  

    - **Detalles:** especifica el intervalo de reintento en minutos para tratar de establecer una conexión con el CAS después de que se produce el error de conexión. Por ejemplo, si se produce un error en la conexión al CAS, el sitio primario espera el número de minutos especificado para el valor **CASRetryInterval** y, después, vuelve a intentar la conexión.  

- **Nombre de clave:** WaitForCASTimeout  

    - **Obligatorio:** No  

    - **Valores:**  <*tiempo de expiración en minutos*>  

    - **Detalles:** especifica el valor de tiempo de espera máximo en minutos de un sitio primario para conectarse al CAS. Por ejemplo, si se produce un error de conexión del sitio primario con el CAS, el sitio primario vuelve a tratar de establecer la conexión conforme al valor **CASRetryInterval** hasta que se alcanza el valor de tiempo de **WaitForCASTimeout**. Puede especificar un valor de `0` a `100`.  

#### <a name="cloudconnectoroptions"></a>CloudConnectorOptions

- **Nombre de clave:** CloudConnector  

    - **Obligatorio:** Sí  

    - **Valores**

        - `0`: no instalar  

        - `1`: instalar  

    - **Detalles:** especifica si se instala un punto de conexión de servicio en este sitio. Dado que el punto de conexión de servicio solo puede instalarse en el sitio de nivel superior de una jerarquía, este valor debe ser `0` para un sitio principal secundario.  

- **Nombre de clave:** CloudConnectorServer  

    - **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1.  

    - **Valores:**  <*FQDN del servidor de punto de conexión de servicio*>  

    - **Detalles:** especifica el FQDN del servidor que hospedará el rol de sistema de sitio del punto de conexión de servicio.  

- **Nombre de clave:** UseProxy  

    - **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1.  

    - **Valores**

        - `0`: no instalar  

        - `1`: instalar  

    - **Detalles:** especifica si el punto de conexión de servicio usa un servidor proxy.  

- **Nombre de clave:** ProxyName  

    - **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1.  

    - **Valores:**  <*FQDN del servidor proxy*>  

    - **Detalles:** especifica el FQDN del servidor proxy que usa el punto de conexión de servicio.  

- **Nombre de clave:** ProxyPort  

    - **Obligatorio:** obligatorio cuando **CloudConnector** es igual a 1.  

    - **Valores:**  <*número de puerto*>  

    - **Detalles:** especifica el número de puerto que se usará para el puerto de proxy.  
