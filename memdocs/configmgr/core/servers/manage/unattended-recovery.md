---
title: Recuperación desatendida
titleSuffix: Configuration Manager
description: Use un script para recuperar los sitios en Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a12de673776817330a80cb68588faf225922e241
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704403"
---
# <a name="unattended-site-recovery-for-configuration-manager"></a>Recuperación de sitio desatendida de Configuration Manager   

*Se aplica a: Configuration Manager (rama actual)*

 Para realizar una [recuperación desatendida](recover-sites.md#site-recovery-procedures) de un sitio de administración central o sitio primario de Configuration Manager, puede crear un script de instalación desatendida y después usar el programa de instalación con la opción de comando **/script**. El script proporciona el mismo tipo de información que solicita el Asistente para instalación, excepto por el hecho de que no existe configuración predeterminada. Deben especificarse todos los valores para las claves de instalación que se aplican al tipo de recuperación que se utiliza.

 Para usar la opción de la línea de comandos de instalación /script, debe crear un archivo de inicialización. Luego, especifique el nombre de este archivo después de la opción /script. Más importante que el nombre del archivo es que este tenga la extensión **.ini**. Cuando haga referencia al archivo de inicialización del programa de instalación desde la línea de comandos, tendrá que proporcionar la ruta de acceso completa al archivo. Por ejemplo, si el archivo de inicialización de instalación es *setup.ini* y se almacena en la carpeta *C:\setup*, la línea de comandos sería:

 `setup /script c:\setup\setup.ini`

> [!IMPORTANT]  
>  Debe tener derechos de administrador para ejecutar el programa de instalación. Al ejecutar el programa de instalación con el script de instalación desatendida, inicie el símbolo del sistema en un contexto de administrador mediante **Ejecutar como administrador**.

 El script contiene valores, nombres de clave y nombres de sección. Los nombres de clave de sección necesarios varían en función del tipo de recuperación para el que crea el script. No hay un orden determinado para las secciones ni para las claves de las secciones. Las claves no distinguen mayúsculas de minúsculas. Cuando proporciona valores para las claves, el nombre de la clave debe ir seguido por un signo de igual (=) y el valor de la clave.

 Utilice las siguientes secciones como guía para crear un script para una recuperación de sitio desatendida. Las tablas enumeran las claves del script de instalación disponibles, sus valores correspondientes, si son necesarias o no, el tipo de instalación para el que se usan y una breve descripción de cada clave.

## <a name="recover-a-central-administration-site-unattended"></a>Recuperación de un sitio de administración central en modo desatendido
 Use la información siguiente para configurar un archivo de script de instalación desatendida para recuperar un sitio de administración central.

 **Identificación**

-   **Nombre de clave:** Acción

    -   **Obligatorio:** Sí
    -   **Valores** RecoverCCAR
    -   **Detalles:** recupera un sitio de administración central.


-   **Nombre de clave:** CDLatest

    -   **Obligatorio:** Sí, solo cuando se usan medios de la carpeta CD.Latest.
    -   **Valores** 1 Si el valor es distinto de 1, se considera que no se usa CD.Latest.
    -   **Detalles:** el script debe incluir esta clave y valor al ejecutar el programa de instalación desde medios de una carpeta CD.Latest, con el fin de instalar un sitio de administración central o principal, o bien para recuperar estos sitios. Este valor indica al programa de instalación que se están usando medios de la carpeta CD.Latest.

**RecoveryOptions**   
-   **Nombre de clave:** ServerRecoveryOptions   

    -   **Obligatorio:** Sí
    -   **Valores** 1, 2 o 4  
         1 = servidor de sitio de recuperación y SQL Server.   
         2 = recuperar sólo servidor de sitio.  
         4 = recuperar sólo SQL Server.
    -   **Detalles:** especifica si el programa de instalación recupera el servidor de sitio, SQL Server o ambos. Las claves asociadas son necesarias cuando se establece el siguiente valor para la configuración de ServerRecoveryOptions:  
        -   **Valor = 1** : tiene la opción de especificar un valor de la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.

             se requiere la clave **BackupLocation** cuando configura un valor de **10** para la clave **DatabaseRecoveryOptions** , que se utiliza para restaurar la base de datos de sitio desde la copia de seguridad.

        -   **Valor = 2** : tiene la opción de especificar un valor de la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.

        -   **Value = 4** se requiere la clave **BackupLocation** cuando configura un valor de **10** para la clave **DatabaseRecoveryOptions** , que se utiliza para restaurar la base de datos de sitio desde la copia de seguridad.

-   **Nombre de clave:** DatabaseRecoveryOptions

    -   **Obligatorio:** quizás
    -   **Valores**   
         - **10** = restaurar la base de datos de sitio desde la copia de seguridad.  
         - **20** = usar una base de datos de sitio que se ha recuperado manualmente mediante otro método.   
         - **40** = crear una base de datos para el sitio. Utilice esta opción si no hay ninguna copia de seguridad de base de datos de sitio disponible. Los datos globales y de sitio se recuperan mediante la replicación desde otros sitios.  
         - **80** = omitir recuperación de base de datos.
    -   **Detalles:** especifica cómo recupera el programa de instalación la base de datos de sitio en SQL Server. Esta clave es necesaria cuando **ServerRecoveryOptions** tiene un valor de **1** o **4**.


-   **Nombre de clave:** ReferenceSite  

    -   **Obligatorio:** quizás
    -   **Valores** &lt;FQDNSitioReferencia\>
    -   **Detalles:** especifica el sitio primario de referencia. Si la copia de seguridad de la base de datos es anterior al período de retención de seguimiento de cambios, o si se recupera el sitio sin una copia de seguridad, el sitio de administración central usa el sitio de referencia para recuperar los datos globales.

         Si no especifica ningún sitio de referencia y la copia de seguridad es anterior al período de retención de seguimiento de cambios, todos los sitios primarios se reinicializan con los datos restaurados desde el sitio de administración central.

         Si no especifica ningún sitio de referencia y la copia de seguridad pertenece al período de retención de seguimiento de cambios, solo se replicarán desde los sitios primarios los cambios que tuvieron lugar desde la copia de seguridad. Si existen cambios en conflicto de varios sitios primarios, el sitio de administración central utiliza el primero que recibe.

         Esta clave es necesaria cuando **DatabaseRecoveryOptions** tiene un valor de **40**.

-   **Nombre de clave:** SiteServerBackupLocation

    -   **Obligatorio:** No
    -   **Valores** &lt;RutaDeAccesoAlConjuntoCopiaSeguridadServidorSitio\>
    -   **Detalles:** Especifica la ruta de acceso para el conjunto de copia de seguridad del servidor de sitio. Esta clave es opcional si la opción **ServerRecoveryOptions** tiene un valor de **1** o **2**. Especifique un valor para la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.


-   **Nombre de clave:** BackupLocation

    -   **Obligatorio:** quizás
    -   **Valores** &lt;RutaDeAccesoAlConjuntoCopiaSeguridadBaseDatosSitio\>
    -   **Detalles:** especifica la ruta de acceso al conjunto de copia de seguridad de base de datos de sitio. La clave **BackupLocation** es necesaria cuando configura un valor de **1** o **4** para la clave **ServerRecoveryOptions** , y configura un valor de **10** para la clave **DatabaseRecoveryOptions** .


**Opciones**

- **Nombre de clave:** ProductID
  -   **Obligatorio:** Sí
  -   **Valores**   
       - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
       - Eval
  -   **Detalles:** la clave de producto de instalación de Configuration Manager, incluidos los guiones. Si escribe **Eval**, puede instalar la versión de evaluación de Configuration Manager.  


- **Nombre de clave:** SiteCode

  -   **Obligatorio:** Sí
  -   **Valores** &lt;Código de sitio\>
  -   **Detalles:** tres caracteres alfanuméricos que identifican de forma única el sitio en la jerarquía. Especifique el código de sitio que usó el sitio antes de que se produjera el error.


- **Nombre de clave:** SiteName

  -   **Obligatorio:** Sí
  -   **Valores** SiteName
  -   **Detalles:** descripción de este sitio.


- **Nombre de clave:** SMSInstallDir

  - **Obligatorio:** Sí
  - **Valores** &lt;*RutaDeInstalaciónDeConfigurationManager*>
  - **Detalles:** especifica la carpeta de instalación de los archivos de programa de Configuration Manager.
    > [!NOTE]   
    >  Puede especificar la ruta de acceso original o una nueva para la instalación de Configuration Manager.

- **Nombre de clave:** SDKServer

  -   **Obligatorio:** Sí
  -   **Valores** &lt;*FQDN del proveedor de SMS*>
  -   **Detalles:** especifica el FQDN del servidor que hospeda el proveedor de SMS. Especifique el servidor que hospedaba el proveedor de SMS antes de producirse el error.

       Puede configurar proveedores de SMS adicionales para el sitio después de la instalación inicial.

- **Nombre de clave:** PrerequisiteComp

  -   **Obligatorio:** Sí
  -   **Valores** 0 o 1  
       0 = descargar   
       1 = ya se ha descargado
  -   **Detalles:** especifica si se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si se usa un valor de 0, el programa de instalación descarga los archivos.  


- **Nombre de clave:** PrerequisitePath

  -   **Obligatorio:** Sí
  -   **Valores** &lt;*RutaDeArchivosDeRequisitosPreviosDeInstalación*>
  -   **Detalles:** especifica la ruta de acceso a los archivos de requisitos previos de instalación. En función del valor **PrerequisiteComp**, el programa de instalación usa esta ruta de acceso para almacenar los archivos descargados o localizar los archivos descargados previamente.

- **Nombre de clave:** AdminConsole

  -   **Obligatorio:** quizás
  -   **Valores** 0 o 1 0 = no instalar   
       1 = instalar
  -   **Detalles:** especifica si se va a instalar la consola de Configuration Manager. Esta clave es necesaria, salvo cuando **ServerRecoveryOptions** tiene un valor de **4**.


- **Nombre de clave:** JoinCEIP   
  > [!Note]  
  > A partir de la versión 1802 de Configuration Manager, la característica CEIP se ha quitado del producto.

  -   **Obligatorio:** Sí
  -   **Valores** 0 o 1  
       0 = no unir  
       1 = unir
  -   **Detalles:** especifica si se va a participar en el Programa para la mejora de la experiencia del usuario.

**SQLConfigOptions**

-   **Nombre de clave:** SQLServerName

    -   **Obligatorio:** Sí
    -   **Valores** *&lt;NombreDelServidorSQLServer\>*
    -   **Detalles:** el nombre del servidor, o bien el de la instancia en clúster, que ejecuta SQL Server y que hospeda la base de datos del sitio. Especifique el mismo servidor que hospedaba la base de datos del sitio antes de producirse el error.


-   **Nombre de clave:** DatabaseName

    -   **Obligatorio:** Sí
    -   **Valores** *&lt;NombreDeBaseDeDatosDeSitio\>* o *&lt;NombreInstancia\>* \\ *&lt;NombreDeBaseDeDatosDeSitio\>*
    -   **Detalles:** el nombre de la base de datos de SQL Server que se crea o utiliza para instalar la base de datos del sitio de administración central. Especifique el mismo nombre de base de datos que se usó antes de producirse el error.

        > [!IMPORTANT]  
        >  Si no se usa la instancia predeterminada, se debe especificar el nombre de instancia y el nombre de la base de datos del sitio.

-   **Nombre de clave:** SQLSSBPort

    -   **Obligatorio:** No
    -   **Valores** &lt;*NúmeroDePuertoSSB*>
    -   **Detalles:** especifique el puerto de SQL Server Service Broker (SSB) utilizado por SQL Server. Normalmente, SSB está configurado para utilizar el puerto TCP 4022, pero se admiten otros puertos. Especifique el mismo puerto SSB que se usó antes de producirse el error.

## <a name="recover-a-primary-site-unattended"></a>Recuperación de un sitio primario desatendido
 Use la información siguiente para configurar un archivo de script de instalación desatendida para recuperar un sitio de administración central.

 **Identificación**

-   **Nombre de clave:** Acción

    -   **Obligatorio:** Sí
    -   **Valores** RecoverPrimarySite
    -   **Detalles:** recupera un sitio primario.


-   **Nombre de clave:** CDLatest

    -   **Obligatorio:** Sí, solo cuando se usan medios de la carpeta CD.Latest.
    -   **Valores** 1 Si el valor es distinto de 1, se considera que no se usa CD.Latest.
    -   **Detalles:** el script debe incluir esta clave y valor al ejecutar el programa de instalación desde medios de una carpeta CD.Latest, con el fin de instalar un sitio de administración central o principal, o bien para recuperar estos sitios. Este valor indica al programa de instalación que se están usando medios de la carpeta CD.Latest.

**RecoveryOptions**

-   **Nombre de clave:** ServerRecoveryOptions

    -   **Obligatorio:** Sí
    -   **Valores** 1, 2 o 4    
         1 = servidor de sitio de recuperación y SQL Server.   
         2 = recuperar sólo servidor de sitio.  
         4 = recuperar sólo SQL Server.
    -   **Detalles:** especifica si el programa de instalación recupera el servidor de sitio, SQL Server o ambos. Las claves asociadas son necesarias cuando se establece el siguiente valor para la configuración de ServerRecoveryOptions:

        -   **Valor = 1** : tiene la opción de especificar un valor de la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.

             se requiere la clave **BackupLocation** cuando configura un valor de **10** para la clave **DatabaseRecoveryOptions** , que se utiliza para restaurar la base de datos de sitio desde la copia de seguridad.

        -   **Valor = 2** : tiene la opción de especificar un valor de la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.

        -   **Value = 4** se requiere la clave **BackupLocation** cuando configura un valor de **10** para la clave **DatabaseRecoveryOptions** , que se utiliza para restaurar la base de datos de sitio desde la copia de seguridad.

-   **Nombre de clave:** DatabaseRecoveryOptions

    -   **Obligatorio:** quizás
    -   **Valores**   
         - **10** = restaurar la base de datos de sitio desde la copia de seguridad.  
         - **20** = usar una base de datos de sitio que se ha recuperado manualmente mediante otro método.     
         - **40** = crear una base de datos para el sitio. Utilice esta opción si no hay ninguna copia de seguridad de base de datos de sitio disponible. Los datos globales y de sitio se recuperan mediante la replicación desde otros sitios.  
         - **80** = omitir recuperación de base de datos.
    -   **Detalles:** especifica cómo recupera el programa de instalación la base de datos de sitio en SQL Server. Esta clave es necesaria cuando **ServerRecoveryOptions** tiene un valor de **1** o **4**.


-   **Nombre de clave:** SiteServerBackupLocation

    -   **Obligatorio:** No
    -   **Valores** &lt;RutaDeAccesoAlConjuntoCopiaSeguridadServidorSitio\>
    -   **Detalles:** Especifica la ruta de acceso para el conjunto de copia de seguridad del servidor de sitio. Esta clave es opcional si la opción **ServerRecoveryOptions** tiene un valor de **1** o **2**. Especifique un valor para la clave **SiteServerBackupLocation** para recuperar el sitio mediante una copia de seguridad de sitio. Si no especifica ningún valor, se reinstala el sitio sin restaurarlo desde un conjunto de copia de seguridad.     


-   **Nombre de clave:** BackupLocation

    -   **Obligatorio:** quizás
    -   **Valores** &lt;RutaDeAccesoAlConjuntoCopiaSeguridadBaseDatosSitio\>
    -   **Detalles:** especifica la ruta de acceso al conjunto de copia de seguridad de base de datos de sitio. La clave **BackupLocation** es necesaria cuando configura un valor de **1** o **4** para la clave **ServerRecoveryOptions** , y configura un valor de **10** para la clave **DatabaseRecoveryOptions** .

**Opciones**

-   **Nombre de clave:** ProductID

    -   **Obligatorio:** Sí
    -   **Valores**     
         - xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  
         - Eval     
    -   **Detalles:** la clave de producto de instalación de Configuration Manager, incluidos los guiones. Si escribe **Eval**, puede instalar la versión de evaluación de Configuration Manager.  


-   **Nombre de clave:** SiteCode

    -   **Obligatorio:** Sí
    -   **Valores** &lt;Código de sitio\>
    -   **Detalles:** tres caracteres alfanuméricos que identifican de forma única el sitio en la jerarquía. Especifique el código de sitio que usó el sitio antes de que se produjera el error.


-   **Nombre de clave:** SiteName

    -   **Obligatorio:** Sí
    -   **Valores** SiteName
    -   **Detalles:** descripción de este sitio.


-   **Nombre de clave:** SMSInstallDir

    -   **Obligatorio:** Sí
    -   **Valores** &lt;*RutaDeInstalaciónDeConfigurationManager*>
    -   **Detalles:** especifica la carpeta de instalación de los archivos de programa de Configuration Manager.

        > [!NOTE]   
        >  Puede especificar la ruta de acceso original o una nueva para la instalación de Configuration Manager.

-   **Nombre de clave:** SDKServer

    -   **Obligatorio:** Sí
    -   **Valores** &lt;*FQDN del proveedor de SMS*>
    -   **Detalles:** especifica el FQDN del servidor que hospeda el proveedor de SMS. Especifique el servidor que hospedaba el proveedor de SMS antes de producirse el error.

         Puede configurar proveedores de SMS adicionales para el sitio después de la instalación inicial.

-   **Nombre de clave:** PrerequisiteComp

    -   **Obligatorio:** Sí
    -   **Valores** 0 o 1    
         0 = descargar   
         1 = ya se ha descargado   
    -   **Detalles:** especifica si se han descargado los archivos de requisitos previos de instalación. Por ejemplo, si se usa un valor de 0, el programa de instalación descarga los archivos.


-   **Nombre de clave:** PrerequisitePath

    -   **Obligatorio:** Sí
    -   **Valores** &lt;*RutaDeArchivosDeRequisitosPreviosDeInstalación*>
    -   **Detalles:** especifica la ruta de acceso a los archivos de requisitos previos de instalación. En función del valor **PrerequisiteComp**, el programa de instalación usa esta ruta de acceso para almacenar los archivos descargados o localizar los archivos descargados previamente.


-   **Nombre de clave:** AdminConsole

    -   **Obligatorio:** quizás
    -   **Valores** 0 o 1  
         0 = no instalar   
         1 = instalar  
    -   **Detalles:** especifica si se va a instalar la consola de Configuration Manager. Esta clave es necesaria, salvo cuando **ServerRecoveryOptions** tiene un valor de **4**.

-   **Nombre de clave:** JoinCEIP  
    > [!Note]  
    > A partir de la versión 1802 de Configuration Manager, la característica CEIP se ha quitado del producto.

    -   **Obligatorio:** Sí
    -   **Valores** 0 o 1    
         0 = no unir  
         1 = unir
    -   **Detalles:** especifica si se va a participar en el Programa para la mejora de la experiencia del usuario.


**SQLConfigOptions**

-   **Nombre de clave:** SQLServerName

    -   **Obligatorio:** Sí
    -   **Valores** *&lt;NombreDelServidorSQLServer\>*
    -   **Detalles:** el nombre del servidor, o bien el de la instancia en clúster, que ejecuta SQL Server y que hospeda la base de datos del sitio. Especifique el mismo servidor que hospedaba la base de datos del sitio antes de producirse el error.


-   **Nombre de clave:** DatabaseName

    -   **Obligatorio:** Sí
    -   **Valores** *&lt;NombreDeBaseDeDatosDeSitio\>* o *&lt;NombreInstancia\>* \\ *&lt;NombreDeBaseDeDatosDeSitio\>*
    -   **Detalles:** el nombre de la base de datos de SQL Server que se crea o utiliza para instalar la base de datos del sitio de administración central. Especifique el mismo nombre de base de datos que se usó antes de producirse el error.

        > [!IMPORTANT]    
        >  Si no se usa la instancia predeterminada, se debe especificar el nombre de instancia y el nombre de la base de datos del sitio.

-   **Nombre de clave:** SQLSSBPort

    -   **Obligatorio:** No
    -   **Valores** &lt;*NúmeroDePuertoSSB*>
    -   **Detalles:** especifique el puerto de SQL Server Service Broker (SSB) utilizado por SQL Server. Normalmente, SSB está configurado para utilizar el puerto TCP 4022, pero se admiten otros puertos. Especifique el mismo puerto SSB que se usó antes de producirse el error.

**Jerarquía ExpansionOption**

-   **Nombre de clave:** CCARSiteServer

    -   **Obligatorio:** quizás
    -   **Valores** &lt;*CódigoDeSitioParaElSitioDeAdministraciónCentral*>
    -   **Detalles:** especifica el sitio de administración central al que se asocia un sitio primario al unirse a la jerarquía de Configuration Manager. Esta configuración es necesaria si el sitio primario estaba asociado con un sitio de administración central antes de producirse el error. Especifique el código de sitio que se usó para el sitio de administración central antes de que se produjera el error.

-   **Nombre de clave:** CASRetryInterval

    -   **Obligatorio:** No
    -   **Valores** &lt;*Intervalo*>
    -   **Detalles:** especifica el intervalo de reintento (en minutos) para tratar de establecer una conexión con el sitio de administración central después de que se produce el error de conexión. Por ejemplo, si se produce un error en la conexión al sitio de administración central, el sitio primario espera el número de minutos especificado en CASRetryInterval y, después, vuelve a intentar la conexión.


-   **Nombre de clave:** WaitForCASTimeout

    -   **Obligatorio:** No
    -   **Valores** &lt;*Tiempo de espera*>
    -   **Detalles:** especifica el valor de tiempo de espera máximo (en minutos) de un sitio primario para conectarse al sitio de administración central. Por ejemplo, si se produce un error de conexión del sitio primario con el sitio de administración central, el sitio primario vuelve a tratar de establecer la conexión conforme al valor especificado para CASRetryInterval hasta que se alcanza el valor de tiempo de WaitForCASTimeout. Puede especificar un valor entre 0 y 100.
