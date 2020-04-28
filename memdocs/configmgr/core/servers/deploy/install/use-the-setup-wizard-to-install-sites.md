---
title: Asistente para la instalación
titleSuffix: Configuration Manager
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e32956d2ca9385c22e9073cfa2665e1f61b3ebd3
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078641"
---
# <a name="use-the-setup-wizard-to-install-configuration-manager-sites"></a>Use el Asistente para instalación si quiere instalar sitios de Configuration Manager.

*Se aplica a: Configuration Manager (rama actual)*

Para instalar un nuevo sitio de Configuration Manager mediante una interfaz de usuario interactiva, use el Asistente para instalación de Configuration Manager (setup.exe). El asistente admite la instalación de un sitio primario o un sitio de administración central. También se usa para [actualizar una instalación de evaluación](upgrade-an-evaluation-install-to-a-full-install.md) de Configuration Manager a una instalación con licencia completa. Si no quiere usar el asistente, puede usar en su lugar un [script de instalación](use-a-command-line-to-install-sites.md) y ejecutar una instalación desatendida de línea de comandos.

Instale un sitio secundario desde la consola de Configuration Manager. Los sitios secundarios no admiten una instalación de línea de comandos por script.

> [!Note]  
> A partir de la versión 1906, el archivo **splash.hta** ya no existe en la raíz del soporte de instalación. Proporciona vínculos a la siguiente información:<!--SCCMDocs-pr#3545-->
>
> - **Instalar el sitio**: `smssetup\bin\x64\setup.exe`. Para más información, vea [Instalación de un sitio de administración central o primario](#bkmk_primary).
> - **Antes de comenzar**: [Diseñar una jerarquía de sitios](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626543 -->
> - **Evaluar la preparación del servidor**: [Comprobador de requisitos previos](prerequisite-checker.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626546 -->
> - **Descargar archivos de requisitos previos requeridos**: `smssetup\bin\x64\setupdl.exe`. Para obtener más información, consulte [Descargador del programa de instalación](setup-downloader.md).
> - **Instalar la consola de Configuration Manager**: `smssetup\bin\i386\consolesetup.exe`. Para más información, vea [Instalar consolas](install-consoles.md).
> - [**Descargar System Center Updates Publisher**](../../../../sum/tools/updates-publisher.md) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626548 -->
> - **Descarga de los clientes de sistemas operativos adicionales**: <!-- https://go.microsoft.com/fwlink/p/?LinkId=626550 -->
>   - [Microsoft Endpoint Configuration Manager: cliente macOS (64 bits)](https://www.microsoft.com/download/details.aspx?id=100850)
>   - [Clientes para UNIX y Linux](https://www.microsoft.com/download/details.aspx?id=47719)
> - [**Notas de la versión**](release-notes.md) <!-- https://go.microsoft.com/fwlink/?LinkID=626571 -->
> - [**Leer documentación**](https://docs.microsoft.com/sccm)<!-- https://go.microsoft.com/fwlink/p/?LinkId=626547 -->
> - **Obtener asistencia para la instalación**: [Foros de TechNet: Configuration Manager (rama actual): implementación de cliente y de sitio](https://social.technet.microsoft.com/Forums/en-us/home?forum=ConfigMgrDeployment) <!--NOTE: this link requires en-us locale to work-->   <!-- https://go.microsoft.com/fwlink/p/?LinkId=626549 -->
> - **Comunidad de Configuration Manager**: [Comunidad de System Center: Cómo participar](https://social.technet.microsoft.com/wiki/contents/articles/11504.system-center-community-how-to-participate.aspx) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626544 -->
> - [**Página principal de Configuration Manager**](https://www.microsoft.com/cloud-platform/system-center-configuration-manager) <!-- https://go.microsoft.com/fwlink/p/?LinkId=626545 -->


## <a name="install-a-central-administration-or-primary-site"></a><a name="bkmk_primary"></a> Instalación de un sitio de administración central o primario

Utilice el siguiente procedimiento para instalar un sitio de administración central o primario. Úselo también para actualizar un sitio de evaluación a un sitio de Configuration Manager con licencia completa.

Antes de iniciar la instalación del sitio, debe familiarizarse con los detalles que se incluyen en los artículos siguientes:

- [Preparar la instalación de sitios](prepare-to-install-sites.md)
- [Requisitos previos para instalar un sitio](prerequisites-for-installing-sites.md)

Si va a instalar un sitio de administración central como parte de un escenario de expansión del sitio, revise [Expansión de un sitio primario independiente](use-the-setup-wizard-to-install-sites.md#bkmk_expand) antes de usar el procedimiento siguiente.

### <a name="process-to-install-a-primary-or-central-administration-site"></a><a name="bkmk_installpri"></a> Proceso para instalar un sitio primario o de administración central

1. En el equipo donde quiere instalar el sitio, ejecute `<InstallationMedia>\SMSSETUP\BIN\X64\Setup.exe` para iniciar el **Asistente para instalación de Configuration Manager**.  

    > [!NOTE]  
    > Al instalar un sitio de administración central para expandir un sitio primario independiente, o al instalar un nuevo sitio primario secundario en una jerarquía existente, use medios de instalación (archivos de origen) que coincidan con la versión de los sitios existentes. Si ha instalado actualizaciones en la consola que han cambiado la versión de los sitios instalados previamente, no use los medios de instalación originales. En su lugar, use archivos de origen de la [carpeta CD.Latest](../../manage/the-cd.latest-folder.md) de un sitio actualizado. Configuration Manager requiere el uso de archivos de origen que coincidan con la versión del sitio existente al que se conectará el nuevo sitio.  

2. En la página **Antes de comenzar**, seleccione **Siguiente**.  

3. En la página **Introducción**, seleccione el tipo de sitio que quiera instalar:  

    - **Sitio de administración central**, como primer sitio de una nueva jerarquía o al expandir un sitio primario independiente:  

        Seleccione **Instalar un sitio de administración central de Configuration Manager**.  

        En un paso posterior de este procedimiento, se le ofrecerá la opción de instalar un sitio de administración central como primer sitio de una jerarquía nueva, o bien de instalar un sitio de administración central para ampliar un sitio primario independiente.  

    - **Sitio primario**, como sitio primario independiente que es el primer sitio de una jerarquía nueva, o como sitio primario secundario:  

        Seleccione **Instalar un sitio primario de Configuration Manager**.  

        > [!TIP]  
        > Normalmente, solo se selecciona la opción **Usar opciones de instalación típica para un sitio primario independiente** para instalar un sitio primario independiente en un entorno de prueba. Cuando se selecciona esta opción, el programa de instalación realiza las siguientes acciones:  
        >
        > - Configura automáticamente el sitio como un sitio primario independiente.  
        > - Usa una ruta de instalación predeterminada.  
        > - Usa una instalación local de la instancia predeterminada de SQL Server para la base de datos del sitio.  
        > - Instala un punto de administración y un punto de distribución en el equipo de servidor de sitio.  
        > - Configura el sitio con el inglés y el idioma de visualización del sistema operativo en el servidor de sitio primario, si coincide con uno de los idiomas que admite Configuration Manager.  

4. En la página **Clave de producto**:  

    - Elija si quiere instalar Configuration Manager como edición de evaluación o como edición con licencia.  

        - Si selecciona una edición con licencia, escriba la clave de producto y seleccione **Siguiente**.  

        - Si selecciona una edición de evaluación, seleccione **Siguiente** (más adelante puede actualizar una instalación de evaluación a una instalación completa).  

    - También puede especificar la **fecha de expiración de Software Assurance** de su contrato de licencia. Es un cómodo recordatorio de esa fecha. Si no la especifica durante la instalación, puede especificarla más tarde desde la consola de Configuration Manager.  

        > [!NOTE]  
        > Microsoft no valida la fecha de expiración especificada y no la usa para la validación de la licencia, pero usted puede usarla como un recordatorio de la fecha de expiración. Esta fecha es útil porque Configuration Manager comprueba periódicamente si hay nuevas actualizaciones de software que se ofrecen en línea. El estado de su licencia de Software Assurance debe ser actual para reunir los requisitos que permiten usar estas actualizaciones adicionales.  

    Para obtener más información, vea [Licencias y ramas](../../../understand/learn-more-editions.md).  

5. En la página **Términos de licencia del software de Microsoft** , lea y acepte los términos de licencia.  

6. En la página **Licencias de requisitos previos** , lea y acepte los términos de licencia del software necesario. El programa de instalación descarga e instala automáticamente el software en los sistemas de sitio o los clientes cuando sea necesario. Acepte todos los términos antes de continuar con la página siguiente.  

7. En la página **Descargas de requisitos previos**, especifique si el programa de instalación debe descargar los archivos redistribuibles necesarios más recientes desde Internet o si debe usar archivos descargados previamente:  

    - Si desea que el programa de instalación descargue los archivos en este momento, seleccione **Descargar archivos requeridos**. A continuación, especifique una ubicación para almacenar los archivos.  

    - Si previamente descargó los archivos con el [descargador del programa de instalación](setup-downloader.md), seleccione **Usar archivos descargados anteriormente**. A continuación, especifique la carpeta de descarga.  

        > [!TIP]  
        > Si usa archivos descargados previamente, compruebe que la ruta de acceso a la carpeta de descarga contenga la versión más reciente de los archivos.  

8. En la página **Selección de idioma de servidor**, seleccione los idiomas que están disponibles para la consola de Configuration Manager y para los informes (el inglés está seleccionado de forma predeterminada y no se puede quitar). Para obtener más información, consulte [Paquetes de idioma](language-packs.md).  

9. En la página **Selección de idioma de cliente**, seleccione los idiomas que están disponibles para los equipos cliente. Especifique también si desea habilitar todos los idiomas de cliente para clientes de dispositivos móviles (el inglés está seleccionado de forma predeterminada y no se puede quitar).  

    > [!IMPORTANT]  
    > Si usa un sitio de administración central, asegúrese de que los idiomas de cliente que configure en el sitio de administración central incluyen todos los idiomas de cliente que configure en cada sitio primario secundario. Los clientes que realizan la instalación desde un punto de distribución tienen acceso a los idiomas de cliente desde el sitio de nivel superior, mientras que los clientes que realizan la instalación desde un punto de administración tienen acceso a los idiomas de cliente desde su sitio primario asignado.  

10. En la página **Configuración de sitio e instalación**, especifique los siguientes valores para el nuevo sitio que va a instalar:  

    - **Código de sitio**: [Cada código de sitio en una jerarquía debe ser único](prepare-to-install-sites.md#bkmk_sitecodes). Utilice tres dígitos alfanuméricos: Entre la A y la Z y del 0 al 9. Dado que el código de sitio se usa en nombres de carpeta, no use nombres reservados para Windows, como los siguientes:  
        - AUX  
        - CON  
        - NUL  
        - PRN  
        - SMS  

        > [!NOTE]  
        > El programa de instalación no comprueba si el código de sitio especificado ya está en uso o si tiene un nombre reservado.  

    - **Nombre de sitio**: todos los sitios requieren este nombre descriptivo, que ayuda a identificar el sitio.  

    - **Carpeta de instalación**: esta es la ruta a la carpeta de instalación de Configuration Manager. No se puede cambiar la ubicación después de instalar el sitio. La ruta de acceso no puede contener caracteres Unicode ni espacios finales.  

        > [!NOTE]  
        > Considere si quiere usar la carpeta de instalación predeterminada. Si usa la partición del SO predeterminada en un entorno de producción, es posible que experimente los problemas siguientes en el futuro:  
        >
        > - Si Configuration Manager usa el espacio en disco disponible adicional en la partición del SO, ni Windows ni Configuration Manager funcionarán correctamente. Si instala Configuration Manager en otra partición, el consumo del disco no afectará al sistema operativo.
        > - El rendimiento de Configuration Manager es mejor con un disco rápido. Algunos diseños de servidor no optimizan el disco del SO para mejorar la velocidad.
        > - Puede mantener, restaurar o reinstalar el sistema operativo sin afectar la instalación de Configuration Manager.  

11. En la página **Instalación del sitio**, use la opción que coincida con su escenario:  

    - **Voy a instalar un sitio de administración central:**  

        En la página **Instalación de sitio de administración central**, seleccione **Instalar como primer sitio en una jerarquía nueva** y, después, seleccione **Siguiente** para continuar.  

    - **Voy a expandir un sitio primario independiente en una jerarquía con un sitio de administración central:**  

        En la página **Instalación de sitio de administración central**, seleccione **Expandir un sitio primario independiente existente en una jerarquía**. A continuación, especifique el FQDN del servidor de sitio primario independiente y elija **Siguiente** para continuar.  

        Los medios que use para instalar el nuevo sitio de administración central deben coincidir con la versión del sitio primario.  

    - **Voy a instalar un sitio primario independiente:**  

        En la página **Instalación de sitio primario**, seleccione**Instalar el sitio primario como un sitio independiente** y, luego, seleccione **Siguiente**.  

    - **Voy a instalar un sitio primario secundario:**  

        En la página **Instalación de sitio primario**, seleccione **Unir el sitio primario a una jerarquía existente**. Luego, especifique el FQDN para el servidor del sitio de administración central, y elija **Siguiente**.  

12. En la página **Información de base de datos**, especifique la siguiente información:  

    - **Nombre de SQL Server (FQDN):** de forma predeterminada, este valor se establece como el equipo de servidor de sitio.  

        Si usa un puerto personalizado, agréguelo al FQDN del servidor SQL Server. Escriba el FQDN seguido de SQL Server con una coma y el número de puerto. Por ejemplo, para el servidor *SQLServer1.fabrikam.com*, use este formato para especificar el puerto *1551*: `SQLServer1.fabrikam.com,1551`  

    - **Nombre de instancia:** de forma predeterminada, este valor se queda en blanco. Usa la instancia predeterminada de SQL en el equipo del servidor de sitio.  

    - **Nombre de la base de datos**: De forma predeterminada, este valor está establecido en `CM_<Sitecode>`. Puede personalizar este valor.  

    - **Puerto de Service Broker:** de forma predeterminada, este valor se establece para usar el puerto predeterminado de SQL Server Service Broker (SSB), que es el 4022. SQL lo usa para comunicarse directamente con la base de datos del sitio en otros sitios.  

13. En la segunda página de **Información de base de datos** puede especificar ubicaciones personalizadas para el archivo de datos de SQL Server y el archivo de registro de SQL Server para la base de datos del sitio:  

    - De forma predeterminada, utiliza las ubicaciones predeterminadas de archivos para SQL Server.  

    - La opción de especificar ubicaciones de archivos personalizaads no está disponible cuando se usa un clúster de SQL Server.  

    - El comprobador de requisitos previos no ejecuta una comprobación del espacio libre en disco de ubicaciones de archivos personalizadas.  

14. En la página **Configuración de proveedor de SMS** , especifique el FQDN del servidor en el que desee instalar el proveedor de SMS.  

    - De forma predeterminada, especifica el servidor de sitio.  

    - Después de haber instalado el sitio, puede configurar proveedores de SMS adicionales. Para más información, vea [Plan for the SMS Provider](../../../plan-design/hierarchy/plan-for-the-sms-provider.md) (Planear el proveedor de SMS).  

15. En la página **Configuración de comunicación de equipos cliente** , elija entre configurar todos los sistemas de sitio para que acepten solo la comunicación HTTPS de los clientes y configurar el método de comunicación para cada rol de sistema de sitio.  

    Si selecciona **Los roles de sistema de sitio aceptan solo comunicación HTTPS de los clientes**, el equipo cliente debe tener un certificado PKI válido para la autenticación de cliente. Para obtener más información, vea [Requisitos de certificados PKI](../../../plan-design/network/pki-certificate-requirements.md).  

    > [!NOTE]  
    > Este paso se aplica solo cuando se instala un sitio primario. Si va a instalar un sitio de administración central, omita este paso.  

16. En la página **Roles del sistema de sitio** , elija si desea instalar un punto de administración o un punto de distribución. Para cada rol que decida instalar con el programa de instalación:  

    - Escriba el **FQDN** del servidor que hospedará el rol. A continuación, elija el método de conexión de cliente que admitirá el servidor: HTTP o HTTPS.  

    - Si ha seleccionado **Los roles de sistema de sitio aceptan solo comunicación HTTPS de los clientes** en la página anterior, la conexión de cliente se configura automáticamente para HTTPS. No se puede este parámetro cambiar a menos que retroceda a la página anterior.  

    > [!NOTE]  
    > Este paso se aplica solo cuando se instala un sitio primario. Si va a instalar un sitio de administración central, omita este paso.  

    > [!NOTE]  
    > Para instalar roles de sistema de sitio, el programa de instalación usa la **cuenta de instalación de sistema de sitio**. De forma predeterminada, se usa la cuenta del equipo del sitio primario. Esta cuenta debe tener un administrador local en un equipo remoto para instalar el rol de sistema de sitio. Si esta cuenta no tiene los permisos necesarios, desactive los roles de sistema de sitio e instálelos más tarde desde la consola de Configuration Manager, después de configurar las cuentas adicionales que va a usar como cuentas de instalación de sistema de sitio. Para más información, vea [Cuentas](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).  

17. En la página **Datos de uso**, revise la información sobre los datos que Microsoft recopila y, después, seleccione **Siguiente**. Para obtener más información, vea [Diagnósticos y datos de uso](../../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

18. La página **Configuración de punto de conexión de servicio** solo está disponible durante los escenarios siguientes:  

    - Si va a instalar un sitio primario independiente.  

    - Si va a instalar un sitio de administración central.  

    > [!NOTE]  
    > Si va a instalar un sitio primario secundario, omita este paso.  

     Si va a instalar un sitio de administración central como parte de un escenario de expansión del sitio y este rol ya está instalado en el sitio primario independiente, primero desinstale este rol del sitio primario independiente. Se permite solo una instancia de este rol en una jerarquía, y solo en el sitio de nivel superior de la jerarquía.  

     Después de seleccionar una configuración para el **Punto de conexión de servicio**, seleccione **Siguiente**. Una vez completada la instalación, puede cambiar esta configuración desde la consola de Configuration Manager. Para obtener más información, consulte [About the service connection point](../configure/about-the-service-connection-point.md) (Sobre el punto de conexión del servicio).  

19. En la página **Resumen de configuración**, revise la configuración seleccionada. Cuando esté listo, seleccione **Siguiente** para iniciar el Comprobador de requisitos previos.  

20. En la página **Comprobar requisitos previos de instalación** aparecen todos los problemas que identifique el comprobador.  

    - Cuando el Comprobador de requisitos previos encuentre un problema, seleccione un elemento de la lista para obtener más información sobre cómo resolverlo.  

    - Antes de continuar para instalar el sitio, resuelva los elementos **con error**. Intente resolver los elementos que tienen el estado **Advertencia**, pero no impiden la instalación del sitio.  

    - Después de solucionar los problemas, seleccione **Ejecutar comprobación** para volver a ejecutar el Comprobador de requisitos previos.  

        Si al ejecutar el Comprobador de requisitos previos, ninguno de los elementos comprobados recibe el estado **Error**, puede seleccionar **Empezar la instalación** para iniciar la instalación del sitio.  

    > [!TIP]  
    > Además de los comentarios que proporciona el asistente, puede encontrar información adicional acerca de problemas de requisitos previos en el archivo **ConfigMgrPrereq.log**. Está en la raíz de la unidad del sistema del equipo en el que va a instalar el sitio. Para obtener más información, consulte la [Lista de comprobaciones de requisitos previos](list-of-prerequisite-checks.md).  

21. En la página **Instalación** , el programa de instalación muestra el estado general de la instalación. Una vez finalizada la instalación del servidor de sitio básica, puede **Cerrar** el asistente de instalación. Al cerrar el asistente, continúan la instalación y las configuraciones de sitio inicial en segundo plano.  

    - Puede conectar una consola de Configuration Manager al sitio antes de que finalice la instalación. Esta consola se conecta como de solo lectura y le permite ver objetos y configuraciones, pero no efectuar modificaciones.  

    - Cuando el programa de instalación haya finalizado, puede conectar una consola en la que puede editar objetos y configuraciones.  


## <a name="expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> Expandir un sitio primario independiente

Cuando haya instalado un sitio primario independiente como primer sitio, después tendrá la opción de expandir dicho sitio en una jerarquía más grande, instalando un sitio de administración central.

Al expandir un sitio primario independiente, instale un sitio de administración central nuevo que use la base de datos del sitio primario independiente existente como referencia. Después de instalar un nuevo sitio de administración central, el sitio primario independiente hace la función de sitio primario secundario.

- Solo puede expandir un sitio primario independiente en una jerarquía nueva.  

- Solo puede expandir un sitio primario independiente en una jerarquía específica. No se puede usar esta opción para incorporar otros sitios primarios independientes a la misma jerarquía. En lugar de eso, use el Asistente para migración para migrar datos de una jerarquía a otra. Para más información, vea [Migración de datos entre jerarquías](../../../migration/migrate-data-between-hierarchies.md).  

- Después de expandir un sitio independiente en una jerarquía con un sitio de administración central, puede agregar sitios secundarios primarios secundarios adicionales.  

- Para quitar un sitio primario de una jerarquía con un sitio de administración central, desinstale primero el sitio primario.  

Para expandir el sitio, use el Asistente para instalación de Configuration Manager para instalar un nuevo sitio de administración central con las siguientes observaciones:  

- Instale el sitio de administración central usando la misma versión de Configuration Manager que el sitio primario independiente.  

- En la página **Introducción** del Asistente para la instalación, seleccione la opción para instalar un sitio de administración central. En una fase posterior del programa de instalación, deberá elegir una opción para expandir un sitio primario independiente existente.  

- Al configurar la página **Selección del idioma de cliente** para el nuevo sitio de administración central, seleccione los mismos idiomas de cliente que están configurados para el sitio primario independiente que va a expandir.  

- En la página **Instalación del sitio**, seleccione la opción de expandir el sitio primario independiente.  

Para expandir un sitio primario independiente, vea primero los [requisitos previos para expandir un sitio](prerequisites-for-installing-sites.md#bkmk_expand). Luego, use el procedimiento [para instalar un sitio primario o de administración central](use-the-setup-wizard-to-install-sites.md#bkmk_installpri) que aparece en este artículo.


## <a name="install-a-secondary-site"></a><a name="bkmk_secondary"></a> Instalar un sitio secundario

Use la consola de Configuration Manager para instalar un sitio secundario.  

- Si la consola que usa no está conectada al sitio primario que será el sitio primario del nuevo sitio secundario, el comando para instalar el sitio se replica en el sitio primario correcto.  

- Antes de comenzar la instalación del sitio, asegúrese de que su cuenta de usuario tiene los permisos necesarios. Además, asegúrese de que el servidor que hospedará el nuevo sitio secundario cumple todos los requisitos previos para su uso como un servidor de sitio secundario.  

- Al instalar el sitio secundario, Configuration Manager configura el nuevo sitio secundario para que pueda usar los puertos de comunicación de cliente que están configurados en el sitio primario principal.  

### <a name="process-to-install-a-secondary-site"></a><a name="bkmk_installsecondary"></a> Proceso para instalar un sitio secundario  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**. Seleccione el sitio que será el sitio primario principal del nuevo sitio secundario.  

2. Para iniciar el **Asistente para crear sitio secundario**, elija **Crear sitio secundario** en la cinta de opciones.  

3. En la página **Antes de comenzar**, confirme que el sitio primario que aparece es el sitio que quiere como sitio primario del nuevo sitio secundario. Después, haga clic en **Siguiente**.  

4. En la página **General** , especifique la siguiente configuración:  

    - **Código de sitio**: Cada código de sitio en una jerarquía debe ser único. Utilice tres dígitos alfanuméricos: Entre la A y la Z y del 0 al 9. Dado que el código de sitio se usa en nombres de carpeta, no use nombres reservados para Windows, como los siguientes:  

        - AUX  
        - CON  
        - NUL  
        - PRN  
        - SMS  

    > [!NOTE]  
    > El programa de instalación no comprueba si el código de sitio especificado ya está en uso o si tiene un nombre reservado.  

    - **Nombre del servidor de sitio**: este valor es el FQDN del servidor en el que se instalará el nuevo sitio secundario.  

    - **Nombre de sitio**: todos los sitios requieren este nombre descriptivo, que ayuda a identificar el sitio.  

    - **Carpeta de instalación**: esta es la ruta a la carpeta de instalación de Configuration Manager. No se puede cambiar la ubicación después de instalar el sitio. La ruta de acceso no puede contener caracteres Unicode ni espacios finales.  

    > [!IMPORTANT]  
    > Después de especificar los detalles de esta página, puede elegir **Resumen** para ir directamente a la página **Resumen** del Asistente. Esta acción usa la configuración predeterminada para el resto de las opciones del sitio secundario.  
    > 
    > - Use esta opción solo si está familiarizado con la configuración predeterminada de este asistente y estos son los valores que quiere usar.  
    > - Cuando se usa la configuración predeterminada no se asocian grupos de límites al punto de distribución. Hasta que configure grupos de límites que incluyan el servidor de sitio secundario, los clientes no usarán el punto de distribución que está instalado en este sitio secundario como ubicación de origen de contenido.  

5. En la página **Archivos de origen de instalación** , elija el modo en el que el equipo del sitio secundario obtendrá los archivos de origen para instalar el sitio.  

    Cuando usa archivos de origen CD.Latest que se comparten en la red o se copian localmente en el servidor del sitio secundario de destino:  

    - **Windows 1802 y anteriores**

        - La ubicación del archivo de origen CD.Latest incluye una carpeta llamada **Redist**. Mueva esta carpeta **Redist** como una subcarpeta debajo de la carpeta **SMSSETUP**.  

            > [!Note]  
            > Si se producen errores de falta de coincidencia de hash durante la instalación, actualice la carpeta **Redist**. Use el [Descargador del programa de instalación](setup-downloader.md) para obtener los archivos más recientes. En el caso de los archivos que provocan un error de coincidencia de hash, cópielos también de la carpeta **Redist** actualizada a la carpeta **SMSSETUP\BIN\X64**.

    - **Versión 1806 y posteriores**<!-- SCCMDocs-pr issue 3164 -->

        - La ubicación del archivo de origen CD.Latest incluye una carpeta llamada **Redist**. Mueva esta carpeta **Redist** como una subcarpeta debajo de la carpeta **SMSSETUP**.  

        - Copie los siguientes archivos desde la carpeta **Redist** a la carpeta **SMSSETUP\BIN\X64**:  
            - SharedManagementObjects.msi
            - SQLSysClrTypes.msi
            - sqlncli.msi

    - Si alguno de los archivos de **Redist** no está disponible, el programa de instalación no puede instalar el sitio secundario.  

    - La cuenta de equipo del servidor de sitio secundario debe tener permisos de **lectura** en la carpeta de origen y el recurso compartido de los archivos.  

6. En la página **Configuración de SQL Server** , especifique la versión de SQL Server que se va a usar y después configure los valores relacionados.  

    > [!NOTE]  
    > El programa de instalación no valida la información que se escriba en esta página hasta que inicia la instalación. Antes de continuar, compruebe esta configuración.  

    - **Instalar y configurar una copia local de SQL Express en el equipo del sitio secundario**  

        - **Puerto de servicio de SQL Server**: especifique el puerto de servicio de SQL Server que SQL Server Express utilizará. Normalmente, el puerto de servicio está configurado para utilizar el puerto TCP 1433, pero se puede configurar otro puerto.  

        - **Puerto de SQL Server Broker**: especifique el puerto de SQL Server Service Broker (SSB) que SQL Server Express utilizará. Normalmente, Service Broker está configurado para utilizar el puerto TCP 4022, pero se puede configurar otro puerto. Especifique un puerto válido que no use ningún otro sitio o servicio y que no esté bloqueado por restricciones de firewall.  

    - **Usar una instancia existente de SQL Server**  

        - **FQDN de SQL Server**: revise el FQDN del equipo que ejecuta SQL Server. Debe usar un servidor local que ejecute SQL Server para hospedar la base de datos del sitio secundario; esta configuración no se puede modificar.  

        - **Instancia de SQL Server**: especifique la instancia de SQL Server que se utilizará como base de datos del sitio secundario. Deje esta opción en blanco para utilizar la instancia predeterminada.  

        - **Nombre de base de datos de sitio de ConfigMgr**: especifique el nombre que se utilizará para la base de datos del sitio secundario.  

        - **Puerto de SQL Server Broker**: especifique el puerto de SQL Server Service Broker (SSB) que SQL Server utilizará. Especifique un puerto válido que no use ningún otro sitio o servicio y que no esté bloqueado por restricciones de firewall.  

    > [!TIP]  
    > Vea [Versiones de SQL Server compatibles](../../../plan-design/configs/support-for-sql-server-versions.md) para obtener una lista de las versiones de SQL Server compatibles con Configuration Manager.  

7. En la página **Punto de distribución** , configure las opciones para el punto de distribución que se instalará en el servidor de sitio secundario.  

    - **Configuración requerida:**  

        - **Especificar cómo se comunican los dispositivos cliente con el punto de distribución**: elija entre HTTP y HTTPS.  

        - **Crear un certificado autofirmado o importar un certificado de cliente PKI**: Elija entre usar un certificado autofirmado o importar un certificado de PKI. Un certificado autofirmado le permite establecer conexiones anónimas de clientes de Configuration Manager a la biblioteca de contenido. El certificado se usa para autenticar el punto de distribución en un punto de administración antes de que el punto de distribución envíe mensajes de estado. Para obtener más información, vea [Requisitos de certificados PKI](../../../plan-design/network/pki-certificate-requirements.md).  

    - **Configuración opcional:**  

        - **Instalar y configurar IIS si lo requiere Configuration Manager**: Seleccione esta opción para permitir que Configuration Manager instale y configure Internet Information Services (IIS) en el servidor si no está ya instalado. Se requiere IIS en todos los puntos de distribución.  

            > [!NOTE]  
            > Aunque este valor es opcional, IIS se debe instalar en el servidor antes de poder instalar correctamente un punto de distribución.  

        - **Habilitar y configurar BranchCache para este punto de distribución**  

        - **Descripción**: Este valor es una descripción detallada para que el punto de distribución le facilite su reconocimiento.  

        - **Habilitar este punto de distribución para contenido preconfigurado**  

8. En la página **Configuración de unidad** , especifique la configuración del punto de distribución del sitio secundario.  

    Puede configurar hasta dos unidades de disco para la biblioteca de contenido y dos unidades de disco para el recurso compartido de paquete. En cambio, Configuration Manager puede usar otras unidades cuando las dos primeras alcancen la reserva de espacio de unidad configurada. La página **Configuración de unidad** le permite configurar la prioridad de las unidades de disco y la cantidad de espacio libre en disco que debe quedar en cada unidad de disco.  

    - **Reserva de espacio de unidad (MB)** : el valor que se configura en esta opción determina la cantidad de espacio libre de una unidad antes de que Configuration Manager elija una unidad diferente y continúe con el proceso de copia en esa unidad. Los archivos de contenido pueden ocupar varias unidades.  

    - **Ubicaciones de contenido**: especifique las ubicaciones de contenido de la biblioteca de contenido y el recurso compartido de paquete. Configuration Manager copia el contenido en la ubicación primaria de contenido hasta que la cantidad de espacio libre alcance el valor especificado en **Reserva de espacio de unidad (MB)** .  

    De forma predeterminada, las ubicaciones de contenido se establecen como **Automático**. La ubicación del contenido principal se establece en la unidad de disco que tenga más espacio en disco en el momento de efectuar la instalación. La ubicación secundaria se establece en la unidad de disco que tenga el máximo espacio libre en disco después de la unidad principal. Cuando las unidades primaria y secundaria alcanzan el valor de la reserva de espacio de unidad, Configuration Manager selecciona otra unidad que esté disponible y que tenga la mayor cantidad de espacio disponible en disco, y continúa con el proceso de copia.  

9. En la página **Validación de contenido** , especifique si desea validar la integridad de los archivos de contenido en el punto de distribución.  

    - Al habilitar la validación de contenido en una programación, Configuration Manager inicia el proceso en la hora programada. Se verifica todo el contenido en el punto de distribución.  

    - También puede configurar la **Prioridad de validación de contenido**.  

    - Para ver los resultados del proceso de validación de contenido, en la consola de Configuration Manager, vaya al área de trabajo **Supervisión**, expanda **Estado de distribución** y seleccione el nodo **Estado de contenido**. Muestra el contenido de cada tipo de paquete. Estos tipos incluyen aplicaciones, paquetes de actualización de software e imágenes de arranque.  

10. En la página **Grupos de límites**, administre los grupos de límites a los que está asignado este punto de distribución:  

    - Durante la distribución de contenido, los clientes deben estar en un grupo de límites que esté asociado con el punto de distribución para utilizarlo como una ubicación de origen para el contenido.  

    - Puede seleccionar la opción **Permitir ubicación de origen de reserva para contenido** para permitir a los clientes que están fuera de estos grupos de límites que reviertan y usen el punto de distribución como una ubicación de origen para el contenido cuando no estén disponibles otros puntos de distribución preferidos.  

        Para obtener más información, consulte [Aspectos básicos de la administración de contenido](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

11. En la página **Resumen**, compruebe la configuración y seleccione **Siguiente** para instalar el sitio secundario. Cuando el asistente muestre la página **Finalización**, puede cerrarlo. La instalación del sitio secundario continúa en segundo plano.  

### <a name="how-to-verify-the-secondary-site-installation-status"></a><a name="bkmk_verify"></a> Comprobación del estado de instalación del sitio secundario  

1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Configuración del sitio** y seleccione el nodo **Sitios**.  

2. Seleccione el servidor de sitio secundario que va a instalar y, después, seleccione **Mostrar estado de instalación** en la cinta de opciones.  

    > [!TIP]  
    > Si se instala más de un sitio secundario a la vez, el Comprobador de requisitos previos se ejecuta en los distintos sitios de uno en uno. Debe finalizar un sitio antes de empezar a comprobar el siguiente.  
