---
title: Revisión y sustitución de aplicaciones
titleSuffix: Configuration Manager
description: Aprenda a trabajar con las versiones de aplicaciones de Configuration Manager y sustituya las aplicaciones.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 30170d70-489f-47f7-bebf-9ed0115db26b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 87804ee2a76dea918cebb964a3672ab61bf6de8d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689233"
---
# <a name="revise-and-supersede-applications-in-configuration-manager"></a>Revisar y sustituir aplicaciones en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este tema aprenderá a trabajar con versiones de aplicaciones de Configuration Manager y a sustituir aplicaciones por una versión nueva.  

##  <a name="application-revisions"></a>Revisiones de la aplicación  
 Si se hacen revisiones en una aplicación o en un tipo de implementación contenido en una aplicación, Configuration Manager crea una revisión nueva de la aplicación. Puede mostrar el historial de cada revisión de aplicación. También puede ver sus propiedades, restaurar una revisión anterior de una aplicación o eliminar una revisión anterior.  

### <a name="to-display-an-application-revision-history"></a>Para mostrar un historial de revisiones de aplicación  

1.  En la consola de Configuration Manager, elija **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones** y, luego, elija la aplicación que desee.  

3.  En la pestaña **Inicio** , en el grupo **Aplicación**, elija **Historial de revisiones** para abrir el cuadro de diálogo **Historial de revisiones de la aplicación** .  

### <a name="to-view-an-application-revision"></a>Para ver una revisión de aplicación  

1.  En el cuadro de diálogo **Historial de revisiones de la aplicación** , seleccione una revisión de aplicación y, a continuación, elija **Ver**.  

2.  En el cuadro de diálogo **Propiedades** , examine las propiedades de la aplicación seleccionada.  

    > [!NOTE]  
    >  Las propiedades de aplicación que se muestran son de solo lectura.  

3.  Cierre el cuadro de diálogo **Propiedades** .  

### <a name="to-restore-an-application-revision"></a>Para restaurar una revisión de aplicación  

1.  En el cuadro de diálogo **Historial de revisiones de la aplicación** , seleccione una revisión de aplicación y, a continuación, elija **Restaurar**.  

2.  En el cuadro de diálogo **Confirmar restauración de revisión**, elija **Sí** para restaurar la revisión de aplicación seleccionada.  

### <a name="to-delete-an-application-revision"></a>Para eliminar una revisión de aplicación  

1.  En el cuadro de diálogo **Historial de revisiones de la aplicación** , seleccione una revisión de aplicación y, a continuación, elija **Eliminar**.  

2.  En el cuadro de diálogo **Eliminar revisión de aplicación**, elija **Sí**.  

> [!IMPORTANT]  
>  Solo se puede eliminar la revisión de aplicación actual si se retiró la aplicación y no contiene referencias.  

##  <a name="application-supersedence"></a>Sustitución de la aplicación  
 La administración de aplicaciones de Configuration Manager le permite actualizar o sustituir aplicaciones existentes mediante una relación de sustitución. Al sustituir una aplicación, puede especificar un nuevo tipo de implementación para reemplazar el tipo de implementación de la aplicación sustituida y también decidir si se debe actualizar o desinstalar la aplicación sustituida antes de instalar la aplicación de sustitución.  

> [!IMPORTANT]  
>  Cuando se selecciona la opción de desinstalar el tipo de implementación sustituida, no puede sustituirse un tipo de implementación por un tipo de implementación que se haya implementado en un tipo de recopilación diferente.  Por ejemplo, un tipo de implementación que se implementó en una recopilación de dispositivos no puede sustituirse por un tipo de implementación que se implementó en una recopilación de usuarios si se selecciona la opción de desinstalar el tipo de implementación sustituido.  

### <a name="decide-whether-to-upgrade-or-replace-an-application"></a>Decidir si actualizar o reemplazar una aplicación  
 En el cuadro de diálogo **Especificar relación de sustitución** del cuadro de diálogo de propiedades de la aplicación se especifica si se va a reemplazar o a actualizar una aplicación. El tipo de sustitución depende de si activa la opción **Desinstalar** de este cuadro de diálogo:  

-   Si desea actualizar a una versión más reciente de la misma aplicación (con el mismo identificador de aplicación), **no** active la opción **Desinstalar**.  

-   Si desea cambiar a otra aplicación (con un identificador de aplicación diferente), active **Desinstalar**. Deberá quitar la versión reemplazada de la aplicación.  

### <a name="supersede-dependent-applications"></a>Reemplazar aplicaciones dependientes  
 En este ejemplo, la **aplicación principal** hace referencia a la aplicación que implementa que tiene las dependencias.  

 Puede crear una relación de sustitución que actualice la aplicación dependiente a una versión nueva.  

1. Asegúrese de que la aplicación dependiente nueva y la aplicación dependiente original están en el mismo grupo de dependencia de la aplicación principal.  

2. Cree una relación de sustitución que sustituya a la aplicación dependiente original con la aplicación dependiente nueva.  

   Durante las instalaciones nuevas de la aplicación principal, se instalará la aplicación dependiente nueva. Las instalaciones existentes de la aplicación principal se actualizarán con la aplicación dependiente nueva.  

   El resultado final es que todas las implementaciones de la aplicación principal usarán la aplicación dependiente nueva.  

### <a name="further-considerations"></a>Otras consideraciones  

-   Puede especificar varias relaciones de sustitución para las aplicaciones dependientes. Se instala la mayor aplicación dependiente de la cadena de sustitución.  

-   Las aplicaciones dependientes deben implementarse en el dispositivo donde está instalada la aplicación principal; en caso contrario, no se instalará la aplicación dependiente.  

-   En el caso de las nuevas instalaciones de la aplicación principal, cuando hay varias dependencias, el orden de dependencia determina qué versión de la aplicación dependiente se instala.  

### <a name="to-specify-a-supersedence-relationship"></a>Para especificar una relación de sustitución  

1.  En la consola de Configuration Manager, elija **Biblioteca de software** > **Administración de aplicaciones** > **Aplicaciones** y, luego, elija la aplicación que reemplace a otra aplicación.  

3.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades** para abrir el cuadro de diálogo **Propiedades** de la aplicación.  

4.  En la pestaña **Sustitución** del cuadro de diálogo **Propiedades** de *<nombre de aplicación\>* , elija **Agregar**.  

5.  En el cuadro de diálogo **Especificar relación de sustitución** , haga clic en **Examinar**.  

6.  En el cuadro de diálogo **Elija la aplicación**, elija la aplicación que desea sustituir y, a continuación, elija **Aceptar**.  

7.  En el cuadro de diálogo **Especificar relación de sustitución** , seleccione el tipo de implementación que reemplazará el tipo de implementación de la aplicación sustituida.  

    > [!NOTE]  
    >  De forma predeterminada, el nuevo tipo de implementación no desinstala el tipo de implementación de la aplicación sustituida. Este escenario normalmente se utiliza cuando se desea implementar una actualización en una aplicación existente. Seleccione **Desinstalar** para quitar el tipo de implementación existente antes de que se instale el nuevo tipo de implementación. Si decide actualizar una aplicación, asegúrese de probar esto primero en un entorno de laboratorio.  

8.  Elija **Aceptar** para cerrar el cuadro de diálogo **Especificar relación de sustitución** .  

9. Elija **Aceptar** para cerrar el cuadro de diálogo **Propiedades** de *<nombre de la aplicación>\>* .  

### <a name="to-display-applications-that-supersede-the-current-application"></a>Para mostrar las aplicaciones que sustituyen a la aplicación actual  

1.  En la consola de Configuration Manager, elija **Biblioteca de software**.  

2.  En el área de trabajo **Biblioteca de software**, expanda **Administración de aplicaciones**, elija **Aplicaciones** y, a continuación, elija la aplicación que desee.  

3.  En la pestaña **Inicio**, en el grupo **Propiedades**, elija **Propiedades** para abrir el cuadro de diálogo **Propiedades** de *<nombre de la aplicación>\>* .  

4.  En la pestaña **Referencias** del cuadro de diálogo **Propiedades** de *<nombre de aplicación>\>* , elija **Aplicaciones que sustituyen a esta aplicación** en la lista desplegable **Tipo de relación**.  

5.  Revise la lista de aplicaciones que sustituyen a la aplicación seleccionada y, a continuación, elija **Aceptar** para cerrar el cuadro de diálogo **Propiedades** de *<nombre de aplicación>\>* .  
