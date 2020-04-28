---
title: Configuración de Microsoft Launcher para Android Enterprise con Intune
titleSuffix: ''
description: Use las directivas de configuración de Intune con Microsoft Launcher.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/22/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ac4a9797df1ea64a5ffbceca3ea204bd9ed13a6f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075547"
---
# <a name="configure-microsoft-launcher"></a>Configuración de Microsoft Launcher

Microsoft Launcher es una aplicación de Android que permite a los usuarios personalizar su teléfono, mantenerse organizados allá donde estén y pasar de trabajar en su teléfono al PC. 

En dispositivos Android Enterprise totalmente administrados, Launcher permite a los administradores de TI de la empresa personalizar las pantallas de inicio de los dispositivos administrados seleccionando el fondo de pantalla, las aplicaciones y las posiciones de los iconos. Esto normaliza la apariencia de todos los dispositivos Android administrados en diferentes dispositivos OEM y versiones del sistema. 

## <a name="how-to-configure-the-microsoft-launcher-app"></a>Cómo configurar la aplicación Microsoft Launcher 

Una vez que la aplicación Microsoft Launcher se haya [agregado a Intune](../apps/apps-add.md), vaya al [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) y seleccione **Aplicaciones** > **Directivas de configuración de aplicaciones**. Agregue una directiva de configuración para **Dispositivos administrados** que se ejecutan en **Android** y elija **Microsoft Launcher** como la aplicación asociada. Haga clic en **Opciones de configuración** para configurar las distintas opciones disponibles de Microsoft Launcher. 

## <a name="choosing-a-configuration-settings-format"></a>Selección de un formato de opciones de configuración 

Puede usar dos métodos para definir opciones de configuración para Microsoft Launcher: 

- El **Diseñador de configuraciones** permite configurar las opciones con una interfaz de usuario fácil de usar que le permite activar o desactivar características y establecer valores. En este método, hay algunas claves de configuración deshabilitadas con el tipo de valor BundleArray. Estas claves de configuración solo se pueden configurar mediante la especificación de datos JSON. 

- Los **datos JSON** permiten definir todas las claves de configuración posibles mediante un script JSON. 

Si agrega propiedades con el **Diseñador de configuraciones**, las puede convertir de forma automática en JSON si selecciona **Especificar datos JSON** en la lista desplegable **Formato de opciones de configuración** como se muestra a continuación.

   ![Formato de opciones de configuración - Usar diseñador de configuraciones](./media/configure-microsoft-launcher/configure-microsoft-launcher-01.png)

   > [!NOTE]
   > Una vez que las propiedades se hayan configurado mediante el Diseñador de configuraciones, los datos JSON también se actualizarán para reflejar solo estas propiedades. Para agregar claves de configuración adicionales a los datos JSON, use el [ejemplo de script JSON](../apps/configure-microsoft-launcher.md#microsoft-launcher-configuration-example) a fin de copiar las líneas necesarias para cada clave de configuración. 

Al editar las directivas de configuración de aplicaciones creadas anteriormente, si se han configurado propiedades complejas, el proceso de edición mostrará el editor de datos de JSON. Se conservarán todas las opciones configuradas previamente, y puede cambiar para usar el diseñador de configuración para modificar la configuración admitida.

## <a name="using-configuration-designer"></a>Uso del Diseñador de configuraciones

El Diseñador de configuraciones le permite seleccionar opciones preestablecidas y sus valores asociados.

   ![Formato de opciones de configuración - Especificar datos JSON](./media/configure-microsoft-launcher/configure-microsoft-launcher-02.png)

En la tabla siguiente se enumeran las claves de configuración disponibles de Microsoft Launcher, los tipos de valor, los valores predeterminados y sus descripciones. La descripción proporciona el comportamiento esperado del dispositivo según los valores seleccionados. En la tabla no se muestran las claves de configuración deshabilitadas en el Diseñador de configuraciones.

|    Configuration Key    |    Tipo de valor    |    Valor predeterminado    |    Descripción     |
|---------------------------------------------------|------------------|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Tipo de inscripción    |    String     |    Predeterminado    |    Permite establecer el tipo de inscripción al que se debe aplicar esta directiva. Actualmente, el valor **predeterminado** se refiere a **CorporateOwnedBuisnessOnly**. No hay otros tipos de inscripción compatibles en este momento.        Nombre de clave JSON: management_mode_key        |
|    Permiso para el usuario para cambiar el orden de las aplicaciones en la pantalla principal    |    Boolean    |    True    |    Le permite especificar si el usuario final puede cambiar la opción relativa al **orden de las aplicaciones en la pantalla principal**.<ul><li>Si se establece en **True**, el orden de las aplicaciones definido en la directiva solo se aplicará para la implementación inicial. Posteriormente, la directiva no se aplicará para respetar los cambios que el usuario pueda haber realizado.</li><li>Si se establece en **False**, el orden de las aplicaciones se aplicará en cada sincronización.</li></ul><br>**Nota:** El orden de las aplicaciones en la pantalla principal solo se puede configurar mediante el editor de JSON.<br><br>Nombre de clave JSON:<br>`com.microsoft.launcher.HomeScreen.AppOrder.UserChangeAllowed`    |
|    Definir tamaño de la cuadrícula    |    String    |    Auto    |    Permite establecer el tamaño de la cuadrícula para las aplicaciones que se van a colocar en la pantalla principal. Puede establecer el número de filas y columnas de la aplicación para definir el tamaño de la cuadrícula en el formato siguiente: `columns;rows`. Si define el tamaño de la cuadrícula, el número máximo de aplicaciones que se mostrarán en una fila de la pantalla principal será el número de filas que establezca, y el número máximo de aplicaciones que se mostrarán en una columna de la pantalla principal será el número de columnas que establezca.<br><br>        Nombre de clave JSON:<br>`com.microsoft.launcher.HomeScreen.GridSize`    |
|    Establecer fondo de pantalla del dispositivo    |    String    |    Null    |    Le permite establecer el fondo de pantalla que elija si escribe la dirección URL de la imagen que quiera establecer como fondo de pantalla.<br><br>Nombre de clave JSON:<br>`com.microsoft.launcher.Wallpaper.URL`    |
|    Permiso para el usuario para cambiar establecer el fondo de pantalla    |    Bool    |    True    |    Le permite especificar si el usuario final puede cambiar el valor de la opción de establecer fondo de pantalla.<ul><li>Si se establece en **True**, el fondo de pantalla definido en la directiva solo se aplicará para la implementación inicial. Posteriormente, la directiva no se aplicará para respetar los cambios que el usuario pueda haber realizado.</li><li>Si se establece en **False**, el fondo de pantalla se aplicará en cada sincronización.</li></ul><br>Nombre de clave JSON:<br>`com.microsoft.launcher.Wallpaper.URL.UserChangeAllowed`        |
|    Habilitación de fuente    |    Boolean    |    True    |    Permite habilitar la fuente de Launcher en el dispositivo cuando el usuario se desliza hacia la derecha en la pantalla principal.<ul><li>Si se establece en **True**, se habilitará la fuente.</li><li>Si se establece en **False**, se deshabilitará la fuente.</li></ul><br>Nombre de clave JSON:<br>`com.microsoft.launcher.Feed.Enabled`    |
|    Permiso para el usuario para cambiar la habilitación de la fuente    |    Boolean    |    True    |     Le permite especificar si el usuario final puede cambiar el valor de la opción de **habilitar fuente**.<ul><li>Si se establece en **True**, la fuente solo se aplicará para la implementación inicial. Posteriormente, la directiva no se aplicará para respetar los cambios que el usuario pueda haber realizado.</li><li>Si se establece en **False**, la fuente se aplicará en cada sincronización.</li></ul><br>Nombre de clave JSON:`com.microsoft.launcher.Feed.Enabled.UserChangeAllowed`    |
|    Ubicación de la barra de búsqueda   |    String    |    Inferior    |  Permite especificar la **ubicación de la barra de búsqueda** en la pantalla principal. <ul><li>Si se establece en **Inferior**, la barra de búsqueda se encontrará en la parte inferior de la pantalla principal.</li><li>Si se establece en **Superior**, la barra de búsqueda se encontrará en la parte superior de la pantalla principal.</li><li>Si se establece en **Ocultar**, la barra de búsqueda se quitará de la pantalla principal.</li></ul><br>Nombre de clave JSON:<br>`com.microsoft.launcher.Search.SearchBar.Placement`    |
|    Permiso para el usuario a fin de cambiar la ubicación de la barra de búsqueda   |    Bool    |    True    |  Permite especificar si el usuario final puede cambiar el valor de la opción **Ubicación de la barra de búsqueda**. <ul><li>Si se establece en **True**, la ubicación de la barra de búsqueda solo se aplicará para la implementación inicial. Posteriormente, la directiva no se aplicará para respetar los cambios que el usuario pueda haber realizado.</li><li>Si se establece en **False**, la ubicación de la barra de búsqueda se aplicará en cada sincronización.</li></ul><br>Nombre de clave JSON:<br>`com.microsoft.launcher.Search.SearchBar.Placement.UserChangeAllowed`    |
|    Modo de acoplamiento  |    String    |    Mostrar    | Permite habilitar el acoplamiento en el dispositivo cuando el usuario se desliza hacia la derecha en la pantalla principal.<ul><li>Si se establece en **Mostrar**, se habilitará el acoplamiento.</li><li>Si se establece en **Ocultar**, el acoplamiento se ocultará en la pantalla principal, pero el usuario podrá mostrarlo cuando sea necesario.</li><li>Si se establece en **Deshabilitado**, el acoplamiento se deshabilitará.</li></ul><br>Nombre de clave JSON:<br>`com.microsoft.launcher.Dock.Mode`    |
|   Permiso para el usuario a fin de cambiar el modo de acoplamiento   |    String    |    True    |  Permite especificar si el usuario final puede cambiar el valor de la opción Modo de acoplamiento.<ul><li>Si se establece en **True**, el modo de acoplamiento solo se aplicará para la implementación inicial. Posteriormente, la directiva no se aplicará para respetar los cambios que el usuario pueda haber realizado.</li><li>Si se establece en **False**, el modo de acoplamiento se aplicará en cada sincronización.</li></ul><br>Nombre de clave JSON:<br>`com.microsoft.launcher.Dock.Mode.UserChangeAllowed`    |

## <a name="enter-json-data"></a>Especificar datos JSON

Especifique datos JSON para configurar todas las opciones disponibles para Microsoft Launcher, así como las opciones deshabilitadas en el **Diseñador de configuraciones**, como se muestra a continuación.

   ![Diseñador de configuración: datos JSON](./media/configure-microsoft-launcher/configure-microsoft-launcher-03.png)

Además de la lista de opciones configurables enumeradas en la tabla del Diseñador de configuraciones (anterior), en la tabla siguiente se proporcionan las claves de configuración que solo se pueden configurar a través de datos JSON.

|    Configuration Key    |    Tipo de valor    |    Valor predeterminado    |    Descripción     |
|----------------------------------------------------------------------------------------------------|-------------------|-------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Establecer aplicaciones permitidas<br>Clave JSON:`com.microsoft.launcher.HomeScreen.Applications`    |    BundleArray    | Vea: [Establecer aplicaciones permitidas](configure-microsoft-launcher.md#set-allow-listed-applications)</sup>    |    Le permite definir el conjunto de aplicaciones visibles en la pantalla principal de entre las instaladas en el dispositivo. Para definir las aplicaciones, escriba el nombre del paquete de aplicación de las aplicaciones que le gustaría hacer visibles; por ejemplo, `com.android.settings` hará que se pueda acceder a la configuración desde la pantalla principal. Las aplicaciones que incluya en la lista de permitidas en esta sección ya deben estar instaladas en el dispositivo para que se vean en la pantalla principal.<p>Propiedades:<ul><li>**Paquete**: nombre del paquete de la aplicación.</li><li>**Clase**: actividad de la aplicación, que es específica de una página determinada de la aplicación. Usaría la página de aplicación predeterminada si este valor está vacío.</li></ul>      |
|    Orden de las aplicaciones en la pantalla principal<br>Clave JSON: `com.microsoft.launcher.HomeScreen.AppOrder`    |    BundleArray    |    Vea: [Orden de las aplicaciones en la pantalla principal](configure-microsoft-launcher.md#home-screen-app-order)      |    Permite especificar el orden de las aplicaciones en la pantalla principal.<p>Propiedades:<br><ul><li>**Tipo**: si se quieren especificar las posiciones de las aplicaciones, el único tipo admitido es `application`. Si se quieren especificar las posiciones de los vínculos web, el tipo es `weblink`.</li><li>**Posición:** esto especifica la ranura del icono de la aplicación en la pantalla principal. Comienza desde la posición 1 en la parte superior izquierda y va de izquierda a derecha, de arriba abajo.</li><li>**Paquete**: se trata de un nombre de paquete de aplicación que se usa para especificar el orden de la aplicación.</li><li>**Clase**: se trata de una actividad de la aplicación, que es específica de una página determinada de la aplicación. Se usará la página de aplicación predeterminada si este valor está vacío. Esta propiedad se utiliza para la aplicación.</li><li>**Etiqueta**: se trata de una actividad de la aplicación, que es específica de una página determinada de la aplicación. Se usará la página de aplicación predeterminada si este valor está vacío. Esta propiedad se utiliza para la aplicación.</li><li>**Vínculo**: dirección URL que se iniciará después de que el usuario final haga clic en el icono de vínculo web. Esta propiedad se usa para el vínculo web.</li></ul>    |
|    Establecer vínculos web anclados<br>Clave JSON: `com.microsoft.launcher.HomeScreen.WebLinks`    |    BundleArray    |    Vea: [Establecer vínculos web anclados](configure-microsoft-launcher.md#set-pinned-web-link)      |    Esta clave permite anclar sitios web como iconos de inicio rápido en la pantalla principal. De este modo, puede asegurarse de que el usuario final puede tener acceso rápido y sencillo a sitios web fundamentales. Se puede modificar la ubicación de cada icono de vínculo web en la configuración "Orden de las aplicaciones en la pantalla principal".<p>Propiedades:<br><ul><li>**Etiqueta**: título del vínculo web mostrado en la pantalla principal de Microsoft Launcher.</li><li>**Vínculo**: dirección URL que se iniciará después de que el usuario final haga clic en el icono de vínculo web.</li></ul>    |


### <a name="set-allow-listed-applications"></a>Establecer aplicaciones permitidas

```JSON
{
    "key": "com.microsoft.launcher.HomeScreen.Applications",
    "valueBundleArray": 
    [
        {
            "managedProperty": [
                {
                    "key": "package",
                    "valueString": ""
                },
                {
                    "key": "class",
                    "valueString": ""
                }
            ]
        }
    ]
}
```

### <a name="home-screen-app-order"></a>Orden de las aplicaciones en la pantalla principal

```JSON
{
    "key": "com.microsoft.launcher.HomeScreen.AppOrder",
    "valueBundleArray": 
    [
        {
            "managedProperty": [
                {
                    "key": "type",
                    "valueString": "application"
                },
                {
                    "key": "position",
                    "valueInteger": 0
                },
                {
                    "key": "package",
                    "valueString": ""
                },
                {
                    "key": "class",
                    "valueString": ""
                }
            ]
        }
    ]
}
```

### <a name="set-pinned-web-link"></a>Establecer vínculos web anclados

```JSON
{ 
    "key": "com.microsoft.launcher.HomeScreen.WebLinks",  
    "valueBundleArray": [ 
        { 
            "managedProperty": [ 
                { 
                    "key": "label",
                    "valueString": "" 
                },  
                { 
                    "key": "link", 
                    "valueString": "" 
                } 
            ] 
        }
    ] 
},
{ 
    "key": "com.microsoft.launcher.HomeScreen.AppOrder",  
    "valueBundleArray": [ 
        { 
            "managedProperty": [ 
                { 
                    "key": "type",  
                    "valueString": "" 
                },  
                { 
                    "key": "position",  
                    "valueInteger": 
                },  
                { 
                    "key": "label",  
                    "valueString": "" 
                },  
                { 
                    "key": "link",  
                    "valueString": "" 
                } 
            ] 
        }
    ] 
}
```



### <a name="microsoft-launcher-configuration-example"></a>Ejemplo de configuración de Microsoft Launcher

Este es un ejemplo de script JSON con todas las claves de configuración disponibles incluidas:

```JSON
{
    "kind": "androidenterprise#managedConfiguration", 
    "productId": "app:com.microsoft.launcher", 
    "managedProperty": [
        {
            "key": "management_mode_key", 
            "valueString": "Default"
        }, 
        {
            "key": "com.microsoft.launcher.Feed.Enable.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.Feed.Enable", 
            "valueBool": true
        }, 
        {
            "key": "com.microsoft.launcher.Wallpaper.Url.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.Wallpaper.Url", 
            "valueBool": "http://www.contoso.com/wallpaper.png"
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.GridSize", 
            "valueString": "5;5"
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.Applications", 
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.ups.mobile.android"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.teams"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.bing"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }
            ]
        }, 
        { 
            "key": "com.microsoft.launcher.HomeScreen.WebLinks",  
            "valueBundleArray": [ 
                { 
                    "managedProperty": [ 
                        { 
                            "key": "label",
                            "valueString": "News" 
                        },  
                        { 
                            "key": "link", 
                            "valueString": "https://www.bbc.com" 
                        } 
                    ] 
                }
            ] 
        },
        {
            "key": "com.microsoft.launcher.HomeScreen.AppOrder.UserChangeAllowed", 
            "valueBool": false
        }, 
        {
            "key": "com.microsoft.launcher.HomeScreen.AppOrder", 
            "valueBundleArray": [
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 17
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.ups.mobile.android"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 18
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.teams"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                }, 
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "application"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 19
                        }, 
                        {
                            "key": "package", 
                            "valueString": "com.microsoft.bing"
                        }, 
                        {
                            "key": "class", 
                            "valueString": ""
                        }
                    ]
                },
                {
                    "managedProperty": [
                        {
                            "key": "type", 
                            "valueString": "weblink"
                        }, 
                        {
                            "key": "position", 
                            "valueInteger": 20
                        }, 
                        {
                            "key": "label", 
                            "valueString": "News"
                        }, 
                        {
                            "key": "link", 
                            "valueString": "https://www.bbc.com"
                        }
                    ]
                }
            ]
        }
    ]
}

```

## <a name="next-steps"></a>Pasos siguientes

- Para más información sobre los dispositivos totalmente administrados de Android Enterprise, vea [Configuración de la inscripción en Intune de dispositivos Android Enterprise totalmente administrados](../enrollment/android-fully-managed-enroll.md).
