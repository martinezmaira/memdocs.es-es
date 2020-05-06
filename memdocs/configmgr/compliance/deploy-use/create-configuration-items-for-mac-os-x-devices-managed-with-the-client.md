---
title: 'Creación de elementos de configuración para equipos Mac administrados por el cliente '
titleSuffix: Configuration Manager
description: Use el elemento de configuración de Mac OS X de Configuration Manager para administrar la configuración de los dispositivos Mac OS X.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 722d5bf5-bedc-4dfc-b324-6eeb773874e9
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 219ddd4c828cdabd022deb9fe372718184a4c024
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693433"
---
# <a name="create-configuration-items-for-mac-os-x-devices"></a>Creación de elementos de configuración para dispositivos Mac OS X
Use el elemento de configuración de **Mac OS X (personalizado)** de Configuration Manager para administrar la configuración de los dispositivos Mac OS X que administra el cliente de Configuration Manager.  
  
El sistema operativo Mac OS X usa archivos de lista de propiedades (.plist) para almacenar la configuración de la aplicación. Use la configuración de cumplimiento para evaluar y corregir la configuración en un archivo de lista de propiedades. También puede administrar la configuración de Mac OS X escribiendo un script de shell que devuelva un valor que se pueda evaluar y corregir a efectos de cumplimiento.  
  
## <a name="create-a-custom-mac-os-x-configuration-item"></a>Creación de un elemento de configuración personalizado de Mac OS X  
  
1. En la consola de Configuration Manager, seleccione **Activos y compatibilidad**.  
  
2. En el área de trabajo **Activos y compatibilidad**, expanda **Configuración de cumplimiento** y, a continuación, seleccione **Elementos de configuración**.  
  
3. En la pestaña **Inicio**, en el grupo **Crear**, seleccione **Crear elemento de configuración**.  
  
4. En la página **General** del asistente **Crear elemento de configuración**, escriba un nombre y, opcionalmente, una descripción para el elemento de configuración.  
  
5. En **Especifique el tipo de elemento de configuración que desea crear**, seleccione **Mac OS X (custom)** .  
  
6. Si crea y asigna categorías para ayudarle a buscar y filtrar elementos de configuración en la consola de Configuration Manager, seleccione **Categorías**.  
  
7. En la página **Plataformas admitidas** del asistente, seleccione las versiones de Mac OS X específicas que evaluarán el elemento de configuración.  
  
8. En la página **Configuración** del asistente, agregue nuevas configuraciones cuyo cumplimiento se evaluará en equipos Mac. Seleccione **Nuevo** para abrir el cuadro de diálogo **Crear configuración**.  
  
9. En el cuadro de diálogo **Crear configuración** , escriba un nombre único y una descripción para la configuración.  
  
10. Elija el **Tipo de configuración** que quiera y después proporcione la información necesaria:  
  
    -   **Preferencias de Mac OS X**  
  
        -   **Id. de aplicación**: especifique el identificador de aplicación del archivo de lista de propiedades del que quiere evaluar el cumplimiento de una clave.  
  
             Por ejemplo, si desea editar la configuración para el explorador Web Safari, podría usar **com.apple.Safari.plist**.  
  
        -   **Clave**: especifique el nombre de la clave que se va a evaluar para el cumplimiento en equipos Mac. Use la siguiente sintaxis: */<diccionario\>/<nombreClave\>* .  
  
            > [!IMPORTANT]  
            >  El nombre de clave distingue mayúsculas de minúsculas y no se evaluará si difiere del nombre de clave en el equipo Mac. Además, no podrá modificar el nombre de clave después de especificarlo. Si necesita modificar el nombre de clave, elimine la configuración y vuelva a crearla.  
  
    -   **Script**  
  
        -   **Script de detección**: seleccione **Agregar script** y, a continuación, escriba un script de shell para evaluar el cumplimiento de la configuración en el equipo Mac. Use el comando **echo** en el script de shell para que devuelva valores a Configuration Manager para el cumplimiento. Configuration Manager usa los resultados devueltos en **STDOUT** para evaluar el cumplimiento.  
  
            > [!IMPORTANT]  
            >  No incluya el comando **reboot** en el script de detección. Dado que el script de detección se ejecuta cada vez que se reinicia el cliente, esto hace que el equipo Mac se reinicie continuamente.  
  
        -   **Script de corrección (opcional)** : si quiere, seleccione **Agregar script** y, a continuación, escriba un script de shell que se usará para corregir cualquier configuración no conforme que se encuentre en los equipos cliente Mac.  
  
            > [!IMPORTANT]  
            >  Para asegurarse de que no se introducen caracteres de formato que el equipo Mac no pueda interpretar, no use copiar y pegar. En su lugar, escriba el script.  
  
11. Elija el **Tipo de datos** que es el formato en el que la condición devuelve los datos antes de que se usen para evaluar la configuración.  
  
    > [!NOTE]  
    >  El tipo de datos **Punto flotante** admite solo 3 dígitos después del separador decimal.  
    >   
    >  Configuration Manager no admite el uso del tipo de datos **booleano** para la configuración de scripts de elementos de configuración de Mac. En su lugar, establezca el tipo de datos en **Entero** y asegúrese de que el script devuelve un valor entero.  
  
12. Seleccione **Aceptar** para guardar la configuración y cerrar el cuadro de diálogo **Crear configuración**. Luego, continúe agregando tantos valores como sea necesario.  
  
13. En la página **Reglas de compatibilidad** del asistente, especifique las condiciones que definen el cumplimiento de un elemento de configuración. Para poder evaluar el cumplimiento de una configuración, debe tener al menos una regla de cumplimiento. Seleccione **Nueva** para agregar una regla nueva.  
  
14. En el cuadro de diálogo **Crear regla** , proporcione la siguiente información:  
  
    -   **Nombre**: escriba un nombre para la regla de cumplimiento.  
  
    -   **Descripción**: escriba una descripción para la regla de cumplimiento.  
  
    -   **Configuración seleccionada**: seleccione **Examinar** para abrir el cuadro de diálogo **Seleccionar configuración**. Seleccione la configuración para la que quiere definir una regla o haga clic en **Nueva configuración**. Cuando termine, elija **Seleccionar**.  
  
        > [!TIP]  
        >  También puede seleccionar **Propiedades** para ver información acerca de la configuración seleccionada actualmente.  
  
    -   **Tipo de regla**: seleccione el tipo de regla de cumplimiento que quiere usar:  
  
        -   **Valor**: cree una regla que compare el valor devuelto por el elemento de configuración con un valor que especifique.  
  
        -   **Existencial**: cree una regla que evalúe la configuración en función de si existe en un dispositivo.  
  
    -   Para un tipo de regla **Valor**, especifique la siguiente información:  
  
        -   **La configuración debe cumplir la siguiente regla:** : seleccione un operador y un valor cuyo cumplimiento se evalúe con la configuración seleccionada. Puede utilizar los operadores siguientes:  
  
            -   **Igual a**  
  
            -   **No es igual a**  
  
            -   **Mayor que**  
  
            -   **Menor que**  
  
            -   **Entre**  
  
            -   **Mayor o igual que**  
  
            -   **Menor o igual que**  
  
            -   **Uno de**: En el cuadro de texto, especifique una entrada en cada línea.  
  
            -   **Ninguno de**: En el cuadro de texto, especifique una entrada en cada línea.  
  
        -   **Corregir las reglas no compatibles cuando se admita**: seleccione esta opción si desea que Configuration Manager corrija automáticamente las reglas no compatibles.  
  
            > [!IMPORTANT]  
            >  Solo puede corregir reglas no conformes cuando el operador de regla se establece en **es igual a**.  
  
        -   **Notificar la no conformidad si no se encuentra la instancia de esta configuración**: el elemento de configuración notifica la no conformidad si esta configuración no se encuentra en el equipo Mac.  
  
        -   **Gravedad de la falta de cumplimiento de los informes**: especifique el nivel de gravedad que se indica si se produce un error en esta regla de cumplimiento. Los niveles de gravedad disponibles son:  
  
            -   **Ninguna**: los equipos que no respeten esta regla de cumplimiento no notificarán ninguna gravedad de error en los informes de Configuration Manager.  
  
            -   **Información**: Los equipos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Información** en los informes de Configuration Manager.  
  
            -   **Advertencia**: los equipos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Advertencia** en los informes de Configuration Manager.  
  
            -   **Crítica**: los equipos que no cumplan esta regla de compatibilidad notificarán una gravedad de error **Crítica** en los informes de Configuration Manager.  
  
            -   **Crítica con evento**: los equipos que no cumplan esta regla de compatibilidad notificarán una gravedad de error **Crítica** en los informes de Configuration Manager. El equipo cliente Mac también registra este nivel de gravedad.  
  
    -   Para un tipo de regla **Existencial**, especifique la siguiente información:  
  
        -   Elija una de las opciones siguientes:  
  
            -   **La configuración debe existir en dispositivos cliente**  
  
            -   **La configuración no debe existir en dispositivos cliente**  
  
        -   **Gravedad de la falta de cumplimiento de los informes**: especifique el nivel de gravedad que se indica si se produce un error en esta regla de cumplimiento. Los niveles de gravedad disponibles son:  
  
            -   **Ninguna**: los equipos que no respeten esta regla de cumplimiento no notificarán ninguna gravedad de error en los informes de Configuration Manager.  
  
            -   **Información**: Los equipos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Información** en los informes de Configuration Manager.  
  
            -   **Advertencia**: los equipos que no cumplan esta regla de compatibilidad notificarán una gravedad de error de **Advertencia** en los informes de Configuration Manager.  
  
            -   **Crítica**: los equipos que no cumplan esta regla de compatibilidad notificarán una gravedad de error **Crítica** en los informes de Configuration Manager.  
  
            -   **Crítica con evento**: los equipos que no cumplan esta regla de compatibilidad notificarán una gravedad de error **Crítica** en los informes de Configuration Manager. El equipo cliente Mac también registra este nivel de gravedad.  
  
        > [!NOTE]  
        >  Las opciones mostradas pueden variar según el tipo de configuración para la que define una regla.  
  
15. Seleccione **Aceptar** para cerrar el cuadro de diálogo **Crear regla**.  
  
16. En la página **Resumen**, confirme las opciones para el nuevo elemento de configuración. Después, finalice el asistente.  
  
Vea el nuevo elemento de configuración en el nodo **Elementos de configuración** del área de trabajo **Activos y compatibilidad**.  
  
Si quiere agregar este elemento de configuración a una línea base de configuración, consulte [Crear líneas base de configuración en System Center Configuration Manager](../../compliance/deploy-use/create-configuration-baselines.md).  
  
## <a name="next-steps"></a>Pasos siguientes

 [Elementos de configuración para dispositivos administrados con el cliente de Configuration Manager](../../compliance/deploy-use/create-configuration-items.md)
