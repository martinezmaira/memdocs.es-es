---
title: Creación de aplicaciones de equipos Mac
titleSuffix: Configuration Manager
description: Consulte las consideraciones que debe tener en cuenta al crear e implementar aplicaciones para equipos Mac.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: ab1aecdd-d943-44f5-b0a9-e8fe7439e5d6
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3b734dc6149c1613d986205577b46160d363d31d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075795"
---
# <a name="create-mac-computer-applications-with-configuration-manager"></a>Creación de aplicaciones para equipos Mac con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Tenga en cuenta las siguientes consideraciones cuando cree e implemente aplicaciones en equipos Mac.  

> [!IMPORTANT]  
>  Los procedimientos incluidos en este tema abarcan información sobre la implementación de aplicaciones en los equipos Mac que están instalados en el cliente de Configuration Manager. Los equipos Mac que inscribe con Microsoft Intune no admiten la implementación de aplicaciones.  

## <a name="general-considerations"></a>Consideraciones generales  
 Puede usar Configuration Manager para implementar aplicaciones en equipos Mac que ejecutan el cliente Mac de Configuration Manager. Los pasos para implementar software en equipos Mac son similares a los pasos para implementar software en equipos Windows. Pero, antes de crear e implementar aplicaciones para equipos Mac administrados por Configuration Manager, debe tener en cuenta lo siguiente:  

-   Antes de implementar paquetes de aplicaciones Mac en equipos Mac, debe usar la herramienta **CMAppUtil** en un equipo Mac para convertir estas aplicaciones en un formato que Configuration Manager pueda leer.  

-   Configuration Manager no es compatible con la implementación de aplicaciones Mac en usuarios. En su lugar, estas implementaciones deben realizarse en un dispositivo. Además, para las implementaciones de aplicaciones Mac, Configuration Manager no es compatible con la opción **Implementar previamente el software en el dispositivo primario del usuario** de la página **Configuración de implementación** del **Asistente para implementar software**.  

-   Las aplicaciones de Mac admiten implementaciones simuladas.  

-   No se puede implementar aplicaciones en equipos Mac que tienen un objetivo **Disponible**.  

-   La opción para enviar paquetes de reactivación al implementar software no es compatible para equipos Mac.  

-   Los equipos Mac no son compatibles con el Servicio de transferencia inteligente en segundo plano (BITS) para descargar el contenido de la aplicación. Si se produce un error en la descarga de la aplicación, se reinicia desde el principio.  

-   Configuration Manager no admite condiciones globales al crear tipos de implementación para los equipos Mac.  

## <a name="steps-to-create-and-deploy-an-application"></a>Pasos para crear e implementar una aplicación  
 En la tabla siguiente se proporcionan los pasos, detalles e información para crear e implementar aplicaciones para equipos Mac.  


|                                         Paso                                          |                                                                                                             Detalles                                                                                                              |
|---------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|            **Paso 1**: Preparar aplicaciones Mac para Configuration Manager             | Para poder crear aplicaciones de Configuration Manager a partir de paquetes de software Mac, debe usar la herramienta **CMAppUtil** en un equipo Mac para convertir el software Mac en un archivo <strong>.cmmac</strong> de Configuration Manager. |
| **Paso 2**: Crear una aplicación de Configuration Manager que contenga el software Mac |                                                                       Use el **Asistente para crear aplicaciones** para crear una aplicación para el software Mac.                                                                       |
|             **Paso 3**: Crear un tipo de implementación para la aplicación Mac              |                                                              Este paso es necesario sólo si no se importó automáticamente esta información de la aplicación.                                                               |
|                        **Paso 4**: Implementar la aplicación Mac                         |                                                                          Use el **Asistente para implementar software** para implementar la aplicación en equipos Mac.                                                                          |
|               **Paso 5**: Supervisar la implementación de la aplicación Mac               |                                                                                 Supervise que las implementaciones de aplicaciones se han realizado correctamente en los equipos Mac.                                                                                 |

## <a name="supplemental-procedures-to-create-and-deploy-applications-for-mac-computers"></a>Procedimientos adicionales para crear e implementar aplicaciones para equipos Mac  
 Use los procedimientos siguientes para crear e implementar aplicaciones para equipos Mac administrados por Configuration Manager.  

###  <a name="step-1-prepare-mac-applications-for-configuration-manager"></a>Paso 1: Preparar aplicaciones Mac para Configuration Manager  
 El proceso para crear e implementar aplicaciones de Configuration Manager en equipos Mac es similar al proceso de implementación para equipos Windows. Pero, para poder crear aplicaciones de Configuration Manager que contengan tipos de implementación para Mac, es necesario preparar las aplicaciones con la herramienta **CMAppUtil**. Esta herramienta se descarga con los archivos de instalación del cliente Mac. La herramienta **CMAppUtil** puede recopilar información acerca de la aplicación, que incluye datos de detección de los siguientes paquetes Mac:  

-   Imagen de disco Apple (.dmg)  

-   Archivo de paquete Meta (.mpkg)  

-   Paquete de instalador de Mac OSX (.pkg)  

-   Aplicación de Mac OSX (.app)  

Después de recopilar la información de la aplicación, **CMAppUtil** crea un archivo con la extensión **.cmmac**. Este archivo contiene los archivos de instalación del software Mac e información sobre los métodos de detección que se pueden usar para evaluar si la aplicación ya está instalada. **CMAppUtil** también puede procesar archivos de **.dmg** con varias aplicaciones Mac y crear diferentes tipos de implementación para cada aplicación.  

1.  Copie el paquete de instalación de software Mac en la carpeta del equipo Mac en la que extrajo el contenido del archivo **macclient.dmg** que descargó del Centro de descarga de Microsoft.  

2.  En el mismo equipo Mac, abra una ventana de terminal y desplácese hasta la carpeta en la que extrajo el contenido del archivo **macclient.dmg** .  

3.  Desplácese hasta la carpeta **Herramientas** y escriba el siguiente comando de línea de comandos:  

     **./CMAppUtil** *<properties\>*  

     Por ejemplo, supongamos que quiere convertir el contenido de un archivo de imagen de disco de Apple denominado **MySoftware.dmg** que está almacenado en la carpeta de escritorio del usuario en un archivo **cmmac** de la misma carpeta. También quiere crear archivos **cmmac** para todas las aplicaciones que se encuentren en el archivo de imagen de disco. Para ello, utilice la siguiente línea de comandos:  

     **./CMApputil –c /Users/** *<nombre de usuario\>* **/Desktop/MySoftware.dmg -o /Users/** *<nombre de usuario\>* **/Desktop -a**  

    > [!NOTE]  
    >  El nombre de la aplicación no puede ser superior a 128 caracteres.  

     Para configurar opciones para **CMAppUtil**, utilice las propiedades de línea de comandos de la tabla siguiente:  

  	|Propiedad|Más información|  
  	|--------------|----------------------|  
  	|**-h**|Muestra las propiedades de línea de comandos disponibles.|  
  	|**-r**|Muestra el **detection.xml** del archivo de **.cmmac** proporcionado en **stdout**. El resultado contiene los parámetros de detección y la versión de **CMAppUtil** que se utilizó para crear el archivo **.cmmac** .|  
  	|**-c**|Especifica el archivo de origen que se va a convertir.|  
  	|**-o**|Especifica la ruta de acceso de salida junto con la propiedad –c.|  
  	|**-a**|Crea automáticamente archivos .cmmac junto con la propiedad –c para todas las aplicaciones y paquetes del archivo de imagen de disco.|  
  	|**-s**|Omite la generación de **detection.xml** si no se encuentran parámetros de detección y fuerza la creación del archivo **.cmmac** sin el archivo **detection.xml** .|  
  	|**-v**|Muestra un resultado más detallado de la herramienta **CMAppUtil** junto con información de diagnóstico.|  

4.  Asegúrese de que se ha creado el archivo **.cmmac** en la carpeta de salida que especificó.  

###  <a name="create-a-configuration-manager-application-that-contains-the-mac-software"></a>Crear una aplicación de Configuration Manager que contenga el software Mac  

Use el procedimiento siguiente para ayudarle a crear una aplicación para equipos Mac administrados por Configuration Manager.  

1.  En la consola de Configuration Manager, elija **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones**.  

3.  En la pestaña **Inicio**, en el grupo **Crear**, elija **Crear aplicación**.  

4.  En la página **General** del **Asistente para crear aplicaciones**, seleccione **Detectar automáticamente la información sobre esta aplicación a partir de archivos de instalación**.  

    > [!NOTE]  
    >  Seleccione **Especificar manualmente la información de la aplicación** si quiere especificar información sobre la aplicación. Para más información sobre cómo especificar manualmente la información, consulte [Crear aplicaciones en Configuration Manager](../../apps/deploy-use/create-applications.md).  

5.  En la lista desplegable **Tipo** , seleccione **Mac OS X**.  

6.  En el campo **Ubicación**, especifique la ruta UNC en el formato *\\\\<servidor\>\\<recurso compartido\>\\<nombre de archivo\>* en el archivo de instalación de la aplicación Mac (archivo **.cmmac**) que detectará la información de la aplicación. Como alternativa, pulse **Examinar** para buscar y especificar la ubicación del archivo de instalación.  

    > [!NOTE]  
    >  Debe tener acceso a la ruta UNC que contiene la aplicación.  

7.  Elija **Siguiente**.  

8.  En la página **Importar información** del **Asistente para crear aplicaciones**, revise la información que se ha importado. Si es necesario, puede pulsar **Anterior** para volver atrás y corregir los errores. Pulse **Siguiente** para continuar.  

9. En la página **Información general** del **Asistente para crear aplicaciones**, especifique información general sobre la aplicación, como el nombre de la aplicación, comentarios, la versión y una referencia opcional que le ayude a hacer referencia a la aplicación en la consola de Configuration Manager.  

    > [!NOTE]  
    >  Es posible que parte de la información de la aplicación esté ya en esta página si previamente se ha obtenido de los archivos de instalación de la aplicación.  

10. Pulse **Siguiente**, revise la información de la aplicación en la página **Resumen** y, después, complete el **Asistente para crear aplicaciones**.  

11. La nueva aplicación se muestra en el nodo **Aplicaciones** de la consola de Configuration Manager.  

###  <a name="step-3-create-a-deployment-type-for-the-mac-application"></a>Paso 3: Crear un tipo de implementación para la aplicación Mac  
 Use el procedimiento siguiente para ayudarle a crear un tipo de implementación para equipos Mac administrados por Configuration Manager.  

> [!NOTE]  
>  Si ha importado automáticamente información sobre la aplicación en el **Asistente para crear aplicaciones**, es posible que ya se haya creado un tipo de implementación para la aplicación.  

1.  En la consola de Configuration Manager, elija **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones**.  

3.  Seleccione una aplicación. Después, en la pestaña **Inicio**, en el grupo **Aplicación**, pulse **Crear tipo de implementación** para crear un nuevo tipo de implementación para esta aplicación.  

    > [!NOTE]  
    >  También puede iniciar el **Asistente para crear tipos de implementación** desde el **Asistente para crear aplicaciones** y desde la pestaña **Tipos de implementación** del cuadro de diálogo **Propiedades** de *<nombre de la aplicación>\>* .  

4.  En la página **General** del **Asistente para crear tipos de implementación**, en la lista desplegable **Tipo**, seleccione **Mac OS X**.  

5.  En el campo **Ubicación**, especifique la ruta de acceso UNC en el formato \\\\<servidor\>\\<recurso compartido\>\\<nombre de archivo\> en el archivo de instalación de la aplicación (archivo **.cmmac**). Como alternativa, pulse **Examinar** para buscar y especificar la ubicación del archivo de instalación.  

    > [!NOTE]  
    >  Debe tener acceso a la ruta UNC que contiene la aplicación.  

6.  Elija **Siguiente**.  

7.  En la página **Importar información** del **Asistente para crear tipos de implementación**, revise la información que se importó. Si es necesario, pulse **Anterior** para volver atrás y corregir los errores. Pulse **Siguiente** para continuar.  

8.  En la página **Información general** del **Asistente para crear tipos de implementación**, especifique la información sobre el nombre de la aplicación, como el nombre de la aplicación, comentarios y los idiomas en los que está disponible el tipo de implementación.  

    > [!NOTE]  
    >  Es posible que parte de la información del tipo de implementación esté ya en esta página si previamente se ha obtenido de los archivos de instalación de la aplicación.  

9. Elija **Siguiente**.  

10. En la página **Requisitos** del **Asistente para crear tipos de implementación**, puede especificar las condiciones que deben cumplirse antes de que se pueda instalar el tipo de implementación en los equipos Mac.  

11. Pulse **Agregar** para abrir el cuadro de diálogo **Crear requisito** y agregar un nuevo requisito.  

    > [!NOTE]  
    >  También puede agregar nuevos requisitos en la pestaña **Requisitos** del cuadro de diálogo **Propiedades** de *<nombre de tipo de implementación>\>* .  

12. En la lista desplegable **Categoría** , seleccione que este requisito es para un dispositivo.  

13. En la lista desplegable **Condición**, seleccione la condición que quiere usar para evaluar si el equipo Mac cumple los requisitos de instalación. El contenido de esta lista varía dependiendo de la categoría que seleccione.  

14. En la lista desplegable **Operador**, pulse el operador que se va a usar para comparar la condición seleccionada con el valor especificado para evaluar si el usuario o el dispositivo cumple los requisitos de instalación. Los operadores disponibles varían según la condición seleccionada.  

15. En el campo **Valor**, especifique los valores que se van a usar con la condición y el operador seleccionados para evaluar si el usuario o el dispositivo cumple con el requisito de instalación. Los valores disponibles varían según la condición y el operador que seleccione.

16. Pulse **Aceptar** para guardar la regla de requisitos y cierre el cuadro de diálogo **Crear requisito**.  

17. En la página **Requisitos** del **Asistente para crear tipos de implementación**, pulse **Siguiente**.  

18. En la página **Resumen** del **Asistente para crear tipos de implementación**, revise las acciones que debe realizar el asistente.  Si es necesario, pulse **Anterior** para volver atrás y cambiar la configuración del tipo de implementación. Pulse **Siguiente** para crear el tipo de implementación.  

19. Una vez que se haya completado la página **Progreso**, revise las acciones que se hayan realizado y, después, pulse **Cerrar** para completar el **Asistente para crear tipos de implementación**.  

20. Si se inició este asistente desde el **Asistente para crear aplicaciones**, volverá a la página **Tipos de implementación**.  

###  <a name="deploy-the-mac-application"></a>Implementar la aplicación Mac  
 Los pasos para implementar una aplicación en los equipos Mac son los mismos que los pasos para implementar una aplicación en equipos Windows, con la excepción de las siguientes diferencias:  

-   No se admite la implementación de aplicaciones en los usuarios.  

-   Las implementaciones que tienen un objetivo **Disponible** no son compatibles.  

-   No se admite la opción **Implementar previamente en el dispositivo primario del usuario** de la página **Configuración de implementación** del **Asistente para implementar software**.  

-   Debido a que los equipos Mac no son compatibles con el Centro de software, se omite el valor **Notificaciones de usuario** de la página **Experiencia del usuario** del **Asistente para implementar software**.  

-   La opción para enviar paquetes de reactivación al implementar software no es compatible para equipos Mac.  

> [!NOTE]  
>  Puede crear una recopilación que contenga solo equipos Mac. Para ello, cree una recopilación que use una regla de consulta y use la consulta WQL de ejemplo del tema [How to create queries](../../core/servers/manage/create-queries.md) (Cómo crear consultas).  

 Para obtener más información, consulte [Deploy applications](../../apps/deploy-use/deploy-applications.md) (Implementar aplicaciones).  

###  <a name="step-5-monitor-the-deployment-of-the-mac-application"></a>Paso 5: Supervisar la implementación de la aplicación Mac  
 Puede usar el mismo proceso para supervisar las implementaciones de aplicaciones en equipos Mac como haría para supervisar las implementaciones de aplicaciones en equipos Windows.  

 Para obtener más información, consulte [Monitor applications](../deploy-use/monitor-applications-from-the-console.md) (Supervisar aplicaciones).  
