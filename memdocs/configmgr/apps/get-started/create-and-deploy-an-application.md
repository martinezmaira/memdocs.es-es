---
title: Crear e implementar una aplicación
titleSuffix: Configuration Manager
description: Cree e implemente una aplicación que contenga una aplicación de línea de negocio y aprenda a administrar aplicaciones de forma eficaz.
ms.date: 07/19/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 3bd1e487-ea18-43c1-b7c3-acbd9b86d429
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: b2d2a3465aebf66db37722629991078093abaaa7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689863"
---
# <a name="create-and-deploy-an-application-with-configuration-manager"></a>Creación e implementación de una aplicación con Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este tema, se pondrá de inmediato a crear una aplicación con Configuration Manager. En este ejemplo, creará e implementará una aplicación que contiene una línea de aplicación empresarial para equipos de Windows denominada **Contoso.msi** que debe instalarse en todos los equipos de su empresa que ejecutan Windows 10. Al hacerlo, aprenderá muchas cosas que puede hacer para administrar aplicaciones de forma eficaz.  

 Este procedimiento está diseñado para ofrecerle una visión general de cómo crear e implementar aplicaciones de Configuration Manager. Sin embargo, no cubre todas las opciones de configuración o cómo crear e implementar aplicaciones para otras plataformas.  

 Para obtener detalles concretos relevantes para cada plataforma, vea el tema correspondiente:  

- [Crear aplicaciones de Windows](creating-windows-applications.md)
- [Crear aplicaciones de Windows Phone](../../mdm/deploy-use/management-tasks-applications.md#bkmk_winphone)
- [Crear aplicaciones de Mac](creating-mac-computer-applications.md)
- [Crear aplicaciones de servidor de UNIX y Linux](creating-linux-and-unix-server-applications.md)
- [Crear aplicaciones de Windows Embedded](creating-windows-embedded-applications.md)


Si ya está familiarizado con las aplicaciones de Configuration Manager, puede omitir este tema. Pero es posible que quiera leer el tema [Crear aplicaciones](../../apps/deploy-use/create-applications.md) para conocer todas las opciones disponibles al crear e implementar aplicaciones.  

## <a name="before-you-start"></a>Antes de empezar  

Asegúrese de revisar la información del tema [Introducción a la administración de aplicaciones](../understand/introduction-to-application-management.md) para tener preparado su sitio para instalar aplicaciones y entender la terminología que se usa en este tema.  

 Además, asegúrese de que los archivos de instalación para la aplicación **Contoso.msi** están en una ubicación accesible en la red.  

## <a name="create-the-configuration-manager-application"></a>Crear la aplicación de Configuration Manager  

### <a name="to-start-the-create-application-wizard-and-create-the-application"></a>Para iniciar el Asistente para crear aplicaciones y crear la aplicación  

1. En la consola de Configuration Manager, elija **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones**.  

2. En la pestaña **Inicio**, en el grupo **Crear**, elija **Crear aplicación**.  

3. En la página **General** del **Asistente para crear aplicaciones**, seleccione **Detectar automáticamente la información acerca de esta aplicación a partir de archivos de instalación**. Esto rellenará previamente parte de la información del asistente con la información extraída del archivo .msi de instalación. A continuación, especifique la siguiente información:  

   - **Tipo**: elija **Windows Installer (archivo \*.msi)** .  

   - **Ubicación**: escriba la ubicación (o elija **Examinar** para seleccionar la ubicación) del archivo de instalación **Contoso.msi**. Tenga en cuenta que se debe especificar la ubicación con el formato *\\\Servidor\Recurso compartido\Archivo* para que Configuration Manager busque los archivos de instalación.  

   Terminará con algo parecido a la captura de pantalla siguiente:  

   ![Página general del asistente de administración de aplicaciones](media/App-management-wizard-general-page.png)  

4. Elija **Siguiente**. En la página **Importar información**, verá información sobre la aplicación y los archivos asociados que se importaron a Configuration Manager. Cuando haya terminado, elija **Siguiente** de nuevo.  

5. En la página **Información general**, puede proporcionar más información sobre la aplicación para ordenarla y buscarla en la consola de Configuration Manager.  

    Además, el campo del **programa de instalación** permite especificar la línea de comandos completa que se usará para instalar la aplicación en los equipos. Puede editar esta opción para agregar sus propias propiedades (por ejemplo **/q** para una instalación desatendida).  

   > [!TIP]  
   > Algunos de los campos de esta página del asistente pueden haberse rellenado automáticamente al importar los archivos de instalación de la aplicación.  

    Al final, la pantalla será similar a la captura de pantalla siguiente:  

    ![Página de información general del asistente de administración de aplicaciones](media/App-management-wizard-general-information-page.png)  

6. Elija **Siguiente**. En la página Resumen, puede confirmar la configuración de la aplicación y luego completar el asistente.  

   Ha terminado de crear la aplicación. Para encontrarla, en el área de trabajo **Biblioteca de software** , expanda **Administración de aplicaciones**y, a continuación, elija **Aplicaciones**. En este ejemplo, verá:  

   ![Gráfico de la aplicación final](media/Final-app-graphic.png)  

## <a name="examine-the-properties-of-the-application-and-its-deployment-type"></a>Examinar las propiedades de la aplicación y su tipo de implementación  

Ahora que ha creado una aplicación, puede refinar la configuración de la aplicación si es necesario. Para ver las propiedades de la aplicación, seleccione la aplicación y, a continuación, en la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades**.  

 En el cuadro de diálogo **<Contoso\> Propiedades de la aplicación**, verá muchos de los elementos que se pueden configurar para restringir el comportamiento de la aplicación. Para obtener detalles de todas las opciones que puede configurar, vea [Crear aplicaciones](../../apps/deploy-use/create-applications.md). En este ejemplo, solo cambiará algunas propiedades del tipo de implementación de la aplicación.  

 Elija la pestaña **Tipos de implementación** > **Aplicación Contoso** Tipo de implementación > **Editar**.

Verá un cuadro de diálogo como este:  

![Página de propiedades de la aplicación de administración de aplicaciones](media/App-management-app-properties-page.png)  

## <a name="add-a-requirement-to-the-deployment-type"></a>Agregar un requisito al tipo de implementación

 Los requisitos especifican las condiciones que deben cumplirse para que una aplicación pueda instalarse en un dispositivo.  Puede elegir entre los requisitos integrados o crear los suyos propios. En este ejemplo, agregará el requisito de que la aplicación solo se instalará en equipos que ejecutan Windows 10.  

1. Desde la página de propiedades del tipo de implementación que acaba de abrir, elija la pestaña **Requisitos** .  

2. Elija **Agregar** para abrir el cuadro de diálogo **Crear requisito** .  

3. En el cuadro de diálogo **Crear requisito** , especifique la siguiente información:  

    - **Categoría**: **Dispositivo**  

    - **Condición**: **Sistema operativo**  

    - **Tipo de regla**: **Valor**  

    - **Operador**: **Uno de**  

    - En la lista de sistemas operativos, seleccione **Windows 10**.  

    Al final, el cuadro de diálogo tendrá este aspecto:  

    ![Página de requisitos de la administración de aplicaciones](media/App-management-requirements-page.png)  

4. Elija **Aceptar** para cerrar cada página de propiedades que abra. A continuación, vuelva a la lista **Aplicaciones** en la consola de Configuration Manager.  

> [!TIP]  
> Los requisitos pueden ayudar a reducir el número de colecciones de Configuration Manager que necesita. Dado que acaba de especificar que la aplicación solo se puede instalar en equipos que ejecutan Windows 10, puede implementar posteriormente esto en una recopilación que contiene equipos que ejecutan distintos sistemas operativos. Sin embargo, la aplicación solo se instalará en PC con Windows 10.

## <a name="add-the-application-content-to-a-distribution-point"></a>Agregar el contenido de la aplicación a un punto de distribución  

A continuación, para implementar la aplicación en PC, asegúrese de que se copie el contenido de la aplicación a un punto de distribución. Los PC tendrán acceso al punto de distribución para instalar la aplicación.  

> [!TIP]  
> Para más información sobre los puntos de distribución y la administración de contenido, vea [Manage content and content infrastructure (Administración del contenido y de la infraestructura de contenido)](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).

1. En la consola de Configuration Manager, elija **Biblioteca de software**.  

2. En el área de trabajo **Biblioteca de software**, expanda **Aplicaciones**. A continuación, en la lista de aplicaciones, seleccione la **aplicación Contoso** que creó.  

3. En la pestaña **Inicio**, en el grupo **Implementación**, elija **Distribuir contenido**.  

4. En la página **General** del **Asistente para distribuir contenido**, compruebe que el nombre de aplicación es correcto y elija **Siguiente**.  

5. En la página **Contenido** , revise la información que se copiará al punto de distribución y elija **Siguiente**.  

6. En la página **Destino del contenido**, elija **Agregar** para seleccionar uno o varios puntos de distribución o grupos de puntos de distribución en los que se va a instalar el contenido de la aplicación.  

7. Complete el asistente.  

Puede comprobar que el contenido de la aplicación se copia correctamente al punto de distribución desde el área de trabajo **Supervisión** que se encuentra en **Estado de distribución** > **Estado de contenido**.  

## <a name="deploy-the-application"></a>Implementar la aplicación  

Posteriormente, implemente la aplicación en una recopilación de dispositivos de la jerarquía. En este ejemplo, va a implementar la aplicación en la recopilación de dispositivos **Todos los sistemas** .  

> [!TIP]  
> Recuerde que solo los equipos Windows 10 instalarán la aplicación debido a los requisitos que ha seleccionado anteriormente.

1. En la consola de Configuration Manager, elija **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones**.  

2. En la lista de aplicaciones, seleccione la aplicación que creó anteriormente, **Aplicación Contoso**y, en la pestaña **Inicio** del grupo **Implementación**, elija **Implementar**.  

3. En la página **General** del **Asistente para implementar software**, elija **Examinar** para seleccionar la recopilación de dispositivos **Todos los sistemas** .  

4. En la página **Contenido**, compruebe que esté seleccionado el punto de distribución desde el que quiere que los equipos instalen la aplicación.  

5. En la página **Configuración de implementación**, asegúrese de que la acción de implementación esté establecida en **Instalar** y el propósito de la implementación en **Requerido**.  

    > [!TIP]  
    > Al establecer el propósito de la implementación en **Requerido**, garantiza que la aplicación se instale en aquellos equipos que cumplan los requisitos definidos. Si establece este valor en **Disponible**, los usuarios pueden instalar la aplicación a petición desde el Centro de software.

6. En la página **Programación** , puede configurar cuándo se instalará la aplicación. En este ejemplo, seleccione **En cuanto se cumpla el tiempo disponible**.  

7. En la página **Experiencia del usuario**, elija **Siguiente** para aceptar los valores predeterminados.  

8. Complete el asistente.  

Use los datos de la sección **Supervisar la aplicación** siguiente para ver el estado de implementación de la aplicación.  

## <a name="monitor-the-application"></a>Supervisar la aplicación

 En esta sección, echará un vistazo al estado de implementación de la aplicación que implementó hace unos instantes.  

### <a name="to-review-the-deployment-status"></a>Para revisar el estado de implementación  

1. En la consola de Configuration Manager, elija **Supervisión** > **Implementaciones**.  

2. En la lista de implementaciones, seleccione **Aplicación Contoso**.  

3. En la pestaña **Inicio** , en el grupo **Implementación** , elija **Ver estado**.  

4. Seleccione una de las siguientes pestañas para ver más actualizaciones de estado acerca de la implementación de la aplicación:  

    - **Correcto**: la aplicación está instalada correctamente en los equipos indicados.  

    - **En curso**: la aplicación no ha terminado de instalarse.  

    - **Error**: se ha producido un error al instalar la aplicación en los equipos indicados. También se muestra información adicional sobre el error.  

    - **Requisitos no cumplidos**: no se ha realizado un intento de instalación en los dispositivos indicados porque estos no cumplían con los requisitos que se han configurado (en este ejemplo, porque no ejecutan Windows 10).  

    - **Desconocido**: Configuration Manager no pudo notificar el estado de la implementación. Consulte de nuevo más tarde.  

> [!TIP]  
> Hay varias maneras de supervisar las implementaciones de aplicaciones. Para obtener todos los detalles, vea [Supervisar aplicaciones](../deploy-use/monitor-applications-from-the-console.md).

## <a name="end-user-experience"></a>Experiencia del usuario final  

Los usuarios con PC que ejecutan Windows 10 a través de Configuration Manager verán un mensaje que les indica que deben instalar la aplicación Contoso. Una vez que acepten la instalación, se instalará la aplicación.  

A partir de Configuration Manager versión 1906, la notificación **Hay nuevo software disponible** solo se mostrará una vez para cada usuario para una aplicación y una revisión determinados. El usuario ya no verá la notificación cada vez que inicie sesión. Solo ve otra notificación de una aplicación si esta ha cambiado o se ha vuelto a implementar.

## <a name="next-steps"></a>Pasos siguientes

[Supervisar aplicaciones](../deploy-use/monitor-applications-from-the-console.md)
