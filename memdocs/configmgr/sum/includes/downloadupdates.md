1.  En la consola de Configuration Manager, vaya al área de trabajo **Biblioteca de software** y haga clic en el nodo **Actualizaciones de software**.  

2.  Elija la actualización de software que desee descargar mediante uno de los métodos siguientes:  

    -   Seleccione uno o varios grupos de actualizaciones de software en el nodo **Grupos de actualizaciones de software**. Después, haga clic en **Descargar** en la cinta.  

    -   Seleccione una o varias actualizaciones de software en el nodo **Todas las actualizaciones de software**. Después, haga clic en **Descargar** en la cinta.  

        > [!NOTE]  
        >  En el nodo **Todas las actualizaciones de software**, Configuration Manager solo muestra las actualizaciones de software con una clasificación de **Crítico** y **Seguridad** que se han publicado en los últimos 30 días.  

        > [!TIP]  
        >  Haga clic en **Agregar criterios** para filtrar las actualizaciones de software que se muestran en el nodo **Todas las actualizaciones de software**. Guarde los criterios de búsqueda que use a menudo y, después, administre las búsquedas guardadas en la pestaña **Búsqueda**.  


3.  En la página **Paquete de implementación** del Asistente para descargar actualizaciones de software, configure las opciones siguientes:  

    -  **Seleccionar paquete de implementación**: elija esta opción a fin de seleccionar un paquete de implementación existente para las actualizaciones de software que se encuentran en la implementación.  

        > [!NOTE]  
        >  Las actualizaciones de software que el sitio ya ha descargado en el paquete de implementación seleccionado no se volverán a descargar.  

    -  **Crear un nuevo paquete de implementación**: seleccione esta opción a fin de crear un nuevo paquete de implementación para las actualizaciones de software de la implementación. Configure las siguientes opciones:  

        -   **Nombre**: especifica el nombre del paquete de implementación. El paquete debe tener un nombre único que describa brevemente su contenido. Está limitado a 50 caracteres.  

        -   **Descripción**: especifique una descripción que proporcione información sobre el paquete de implementación. La descripción opcional está limitada a 127 caracteres.    

        -   **Origen de paquete**: especifica la ubicación de los archivos de origen de la actualización de software. Escriba una ruta de acceso a la red para la ubicación de origen (por ejemplo, `\\server\sharename\path`) o haga clic en **Examinar** para buscar la ubicación de red. Cree la carpeta compartida para los archivos de origen del paquete de implementación antes de continuar a la página siguiente.  

             - No se puede usar la ubicación especificada como origen de otro paquete de implementación de software.  

             - Puede cambiar la ubicación de origen del paquete en las propiedades del paquete de implementación después de que Configuration Manager cree el paquete de implementación. Si lo hace, copie primero el contenido desde el origen del paquete original a la nueva ubicación de origen del paquete.  

             -  La cuenta de equipo del proveedor de SMS y el usuario que ejecuta el asistente para descargar actualizaciones de software deben tener permisos de **Escritura** en la ubicación de descarga. Restrinja el acceso a la ubicación de descarga. Esta restricción reduce el riesgo de que los atacantes alteren los archivos de origen de actualización de software.  

        - **Habilitar replicación diferencial binaria**: habilite esta opción para minimizar el tráfico de red entre sitios. La replicación diferencial binaria (BDR) solo actualiza el contenido que ha cambiado en el paquete, en lugar de actualizar todo el contenido del paquete. Para obtener más información, vea [Replicación diferencial binaria](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

4.  En la página **Puntos de distribución**, especifique los puntos de distribución o los grupos de puntos de distribución que hospedan los archivos de actualización de software. Para obtener más información sobre los puntos de distribución, consulte [Distribution point configurations](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs) (Configuraciones de punto de distribución). Esta página sólo está disponible cuando se crea un nuevo paquete de implementación de actualizaciones de software.  

5.  La página **Configuración de distribución** solo está disponible cuando se crea un paquete de implementación de actualización de software. Especifique las siguientes opciones:  

    -   **Prioridad de distribución**: utilice esta opción para especificar la prioridad de distribución del paquete de implementación. La prioridad de distribución se aplica cuando se envía el paquete de implementación a puntos de distribución en sitios secundarios. Los paquetes de implementación se envían en orden de prioridad: alta, media o baja. Los paquetes con prioridades idénticas se envían en el orden en que se crearon. Si no hay ningún trabajo pendiente, el paquete se procesa inmediatamente sin tener en cuenta su prioridad. De forma predeterminada, el sitio envía los paquetes con la prioridad **Media**.  

    -   **Habilitar para distribución a petición**: use esta opción para habilitar la distribución de contenido a petición en los puntos de distribución configurados para esta característica y en el grupo de límites actual del cliente. Cuando se habilita esta opción, el punto de administración crea un desencadenador para que el administrador de distribución distribuya el contenido en todos esos puntos de distribución cuando un cliente solicite el contenido del paquete y no esté disponible. Para obtener más información, vea [Distribución de contenido a petición](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).  

    -   **Configuración de punto de distribución preconfigurado**: utilice esta opción para especificar cómo quiere distribuir el contenido en los puntos de distribución preconfigurados. Elija una de las siguientes opciones:  

        -   **Descargar contenido automáticamente cuando los paquetes se asignen a puntos de distribución**: utilice esta opción para omitir los valores preconfigurados y distribuir contenido en el punto de distribución.   

        -   **Descargar solo los cambios de contenido en el punto de distribución**: utilice esta opción para preconfigurar el contenido inicial en el punto de distribución y luego distribuir los cambios de contenido en el punto de distribución.  

        -   **Copiar manualmente el contenido de este paquete en el punto de distribución**: utilice esta opción para preconfigurar siempre el contenido en el punto de distribución. Esta opción es el valor predeterminado.  

        Para obtener más información sobre cómo preconfigurar contenido en puntos de distribución, consulte [Use Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage)(Usar contenido preconfigurado).  


6.  En la página **Ubicación de descarga**, especifique la ubicación que usa Configuration Manager para descargar los archivos de origen de actualización de software. Utilice una de las siguientes opciones:  

    -   **Descargar actualizaciones de software de Internet**: seleccione esta opción para descargar las actualizaciones de software desde la ubicación en Internet. Esta opción es el valor predeterminado.  

    -   **Descargar actualizaciones de software de una ubicación en mi red**: seleccione esta opción para descargar las actualizaciones de software desde un directorio local o una carpeta compartida. Esta opción es útil si el equipo que ejecuta el asistente no tiene acceso a Internet. Cualquier equipo con acceso a Internet puede descargar de forma preliminar las actualizaciones de software. Después, almacénelas en una ubicación en la red local que sea accesible desde el equipo que ejecuta al asistente.  


7.  En la página **Selección del idioma**, seleccione los idiomas para los que el sitio descarga las actualizaciones de software seleccionadas. El sitio solo descarga estas actualizaciones si están disponibles en los idiomas seleccionados. Las actualizaciones de software que no son específicas de un idioma se descargan siempre. De forma predeterminada, el asistente selecciona los idiomas que se han configurado en las propiedades del punto de actualización de software. Debe seleccionar, como mínimo, un idioma para poder pasar a la página siguiente. Si solo se seleccionan idiomas que una actualización de software no admite, la descarga no se completa para esa actualización.  

8. En la página **Resumen**, compruebe la configuración seleccionada en el asistente y, después, haga clic en **Siguiente** para descargar las actualizaciones de software.  

9. En la página **Finalización**, compruebe que las actualizaciones de software se descargaron correctamente y, después, haga clic en **Cerrar**.  
