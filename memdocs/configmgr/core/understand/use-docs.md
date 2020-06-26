---
title: Cómo usar los documentos
titleSuffix: Configuration Manager
description: Obtenga sugerencias sobre cómo usar la biblioteca de documentación técnica de Configuration Manager.
ms.date: 04/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b3d755bd-0870-4f1f-a56d-bfd3c7b492b9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 31f9b1cb083400abd36858a177e87804a916362c
ms.sourcegitcommit: 7a099ff53668f50b37adab97ecd7ba98c5324676
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2020
ms.locfileid: "84746527"
---
# <a name="how-to-use-the-configuration-manager-docs"></a>Cómo usar los documentos de Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

En este artículo se ofrecen recursos y sugerencias para usar la biblioteca de documentación de Configuration Manager.

- Procedimiento para realizar búsquedas
- Envío de errores, mejoras, preguntas y nuevas ideas sobre documentos
- Procedimiento para recibir notificaciones de los cambios
- Procedimiento para colaborar en documentación

Para obtener ayuda general sobre el producto, vea [Búsqueda de ayuda](find-help.md).

## <a name="search"></a><a name="bkmk_searchtips"></a> Buscar

Usa los consejos de búsqueda siguientes para tratar de encontrar la información que necesitas:

- Cuando use el motor de búsqueda preferido para buscar contenido de Configuration Manager, incluya `ConfigMgr` con las palabras clave de búsqueda.

  - Busque resultados de `docs.microsoft.com/mem/configmgr` de la rama actual de Configuration Manager. Los resultados de `docs.microsoft.com/previous-versions` corresponden a versiones anteriores del producto.

  - Para centrar más los resultados de búsqueda en la biblioteca de contenido actual, incluya `site:docs.microsoft.com` para definir el ámbito del motor de búsqueda.

- Use los términos de búsqueda que coincidan con la terminología en la interfaz de usuario y la documentación en línea. Evite términos no oficiales o abreviaciones que es posible que vea en el contenido de la Comunidad. Por ejemplo, busque:

  - "punto de administración" en lugar de "MP"
  - "tipo de implementación" en lugar de "DT"
  - "actualizaciones de software" en lugar de "SUM"

- Para buscar dentro del artículo actual, use la característica **Buscar** del explorador. Con los exploradores web más modernos, presione **Ctrl**+**F** y luego escriba los términos de búsqueda.

- En cada artículo de `docs.microsoft.com` se incluyen los siguientes campos para ayudar a buscar el contenido:

  - **Búsqueda** en la esquina superior derecha. Para buscar todos los artículos, escriba los términos en este campo. Los artículos de la biblioteca de Configuration Manager incluyen de forma automática el ámbito `ConfigMgr` que solo busca en esta biblioteca de documentación.

  - **Filtre por título** sobre la tabla de contenido de la izquierda. Para buscar en la tabla de contenido actual, escriba los términos en este campo. Este campo solo compara los términos que aparecen en los títulos de artículo del nodo actual. Por ejemplo, **Infraestructura central** (`docs.microsoft.com/configmgr/core`) o **Administración de aplicaciones** (`docs.microsoft.com/configmgr/apps`).

- ¿Tiene problemas para encontrar algo? [Rellene los comentarios](#bkmk_docfeedback) Al rellenar el problema, indique el motor de búsqueda que está usando, las palabras clave que ha intentado y el artículo de destino. Estos comentarios ayudan a Microsoft a optimizar el contenido para que la búsqueda sea mejor.

> [!TIP]
> A partir de la versión 1902 de Configuration Manager, hay un nodo **Documentación** en la nueva área de trabajo **Comunidad** de la consola de Configuration Manager. Este nodo incluye información actualizada acerca de los artículos de soporte técnico y la documentación de Configuration Manager. Para obtener más información, vea [Uso de la consola de Configuration Manager](../servers/manage/admin-console.md#bkmk_doc-dashboard).

## <a name="feedback"></a><a name="bkmk_docfeedback"></a> Comentarios

Seleccione el vínculo **Comentarios** de la esquina superior derecha de cualquier artículo para ir a la sección Comentarios de la parte inferior. Esta sección se integra con Incidencias con de GitHub. Para obtener más información sobre la integración con Problemas de GitHub, vea la [entrada de blog de la plataforma de documentos](https://docs.microsoft.com/teamblog/a-new-feedback-system-is-coming-to-docs).

Para compartir comentarios sobre el propio producto Configuration Manager, seleccione **Comentarios sobre el producto**. Para obtener más información, vea [Comentarios sobre el producto](find-help.md#product-feedback).

Una [cuenta de GitHub](https://github.com/join) es un requisito previo para proporcionar comentarios sobre la documentación. Una vez que inicie sesión, hay una autorización de una sola vez para la organización de MicrosoftDocs. Luego, al seleccionar **Comentarios del contenido**, escriba un título y un comentario y seleccione **Enviar comentarios**. Esta acción rellena un nuevo problema del artículo de destino en el [repositorio de SCCMdocs](https://github.com/MicrosoftDocs/SCCMdocs/issues).

Esta integración también muestra los problemas abiertos o cerrados existentes del artículo de destino. Si hubiera alguno, revíselo antes de enviar un nuevo problema. Si encuentra una incidencia relacionada, seleccione el icono de cara para agregar una reacción o expándalo para agregar un comentario.

#### <a name="types-of-feedback"></a>Tipos de comentarios

Use Problemas de GitHub para enviar los siguientes tipos de comentarios:

- Error de documento: el contenido está obsoleto, es poco claro, confuso o se ha interrumpido.
- Mejora de documento: una sugerencia para mejorar el artículo.
- Pregunta de documento: necesita ayuda para encontrar documentación existente.
- Idea de documento: una sugerencia para un artículo nuevo. Use este método en lugar de UserVoice para los comentarios sobre la documentación.
- Enhorabuena: comentarios positivos sobre un artículo útil o informativo.
- Localización: comentarios sobre la traducción del contenido.
- Optimización del motor de búsqueda (SEO): comentarios sobre problemas de búsqueda de contenido. Incluya el motor de búsqueda, las palabras clave y el artículo de destino en los comentarios.

Si crea una incidencia sobre temas no relacionados con la documentación, Microsoft la cerrará. Por ejemplo:

- [Comentarios sobre el producto](find-help.md#product-feedback)
- [Preguntas sobre el producto](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)
- [Solicitudes de soporte técnico](https://aka.ms/cmcbsupport)

Para compartir comentarios sobre la plataforma docs.microsoft.com, consulte el artículo correspondiente a los [comentarios sobre la documentación](https://aka.ms/sitefeedback). La plataforma incluye todos los componentes contenedores, como el encabezado, la tabla de contenido y el menú de la derecha. También cómo se representan los artículos en el explorador, como la fuente, los cuadros de alerta y los delimitadores de página.

## <a name="notifications"></a><a name="bkmk_notifications"></a> Notificaciones

Para recibir notificaciones cuando cambie el contenido de la biblioteca de documentación, siga estos pasos:

1. Use la [búsqueda de documentos](https://docs.microsoft.com/search/index?scope=ConfigMgr) para buscar un artículo o un conjunto de artículos. Por ejemplo:

    - Buscar un único artículo por título: ["Archivos de registro para la solución de problemas: Configuration Manager"](https://docs.microsoft.com/search/index?search=%22Log+files+for+troubleshooting+-+Configuration+Manager%22&scope=ConfigMgr)

    - Buscar cualquier artículo relacionado con [SQL](https://docs.microsoft.com/search/index?search=SQL&scope=ConfigMgr)

2. En la esquina superior derecha, seleccione el vínculo **RSS**.

3. Use esta fuente en cualquier aplicación RSS para recibir notificaciones cuando haya un cambio en cualquiera de los resultados de la búsqueda.

> [!TIP]
> También puede **Seguir el hilo** del [repositorio de SCCMdocs](https://github.com/MicrosoftDocs/SCCMdocs) en GitHub. Este método genera gran cantidad de notificaciones. Además no incluye los cambios de un repositorio privado usado por Microsoft.

## <a name="contribute"></a><a name="bkmk_contribute"></a> Contribuir

La biblioteca de documentación de Configuration Manager, al igual que la mayor parte del contenido de docs.microsoft.com, es de código abierto en GitHub. Esta biblioteca acepta y fomenta contribuciones de la comunidad. Para obtener más información sobre cómo empezar, vea la [guía para colaboradores](https://docs.microsoft.com/contribute). El único requisito previo es crear una [cuenta de GitHub](https://github.com/join).

### <a name="basic-steps-to-contribute-to-sccmdocs"></a>Pasos básicos para contribuir a SCCMdocs

1. En el artículo de destino, seleccione **Editar**. Esta acción abre el archivo de origen de GitHub.

2. Para editar el archivo de origen, seleccione el icono de lápiz.

3. Realice cambios en el origen Markdown. Para obtener más información, vea [How to use Markdown for writing Docs](https://docs.microsoft.com/contribute/markdown-reference) (Cómo usar Markdown para escribir documentos).

4. En la sección Propose file change (Proponer cambio de archivo), escriba el comentario de confirmación público que describe *qué* ha modificado. Luego, seleccione **Propose file change** (Proponer cambio de archivo).

5. Desplácese hacia abajo y compruebe los cambios realizados. Seleccione **Crear solicitud de incorporación de cambios** para abrir el formulario. Describa *por qué* ha realizado este cambio. Etiquete al autor del artículo y solicítele que revise. Seleccione **Crear solicitud de incorporación de cambios**.

### <a name="what-to-contribute"></a>Cómo contribuir

Si quiere contribuir, pero no sabe por dónde empezar, vea las siguientes sugerencias:

- Busque las etiquetas destinadas a la comunidad en la lista de problemas:

  - [good-first-issue](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:good-first-issue)
  - [help-wanted](https://github.com/MicrosoftDocs/sccmdocs/issues?q=is:open+is:issue+label:help-wanted)  

    Los autores de Microsoft asignan estas etiquetas a incidencias que son adecuadas para la contribución de la comunidad.

- Revise la precisión de un artículo. Luego actualice los metadatos **ms.date** mediante el formato `mm/dd/yyyy`. Esta contribución ayuda a mantener el contenido actualizado.

- Agregue aclaraciones, ejemplos o instrucciones en función de su experiencia. Esta contribución usa el poder de la comunidad para compartir conocimiento.

- Traducciones correctas a un idioma distinto del inglés. Esta contribución mejora la facilidad de uso del contenido localizado.

> [!NOTE]
> Las contribuciones grandes requieren la firma de un contrato de licencia de colaboración (CLA) si no es empleado de Microsoft. GitHub automáticamente requiere que firme este acuerdo cuando una contribución alcanza el umbral.

### <a name="tips"></a>Sugerencias

Siga estas pautas generales al contribuir en documentación de Configuration Manager:

- No nos sorprenda con grandes solicitudes de incorporación de cambios. En su lugar, [notifique un problema](#bkmk_docfeedback) e inicie una discusión. Así podremos acordar un rumbo antes de invertir una gran cantidad de tiempo.

- Lea la [guía de estilo de Microsoft](https://aka.ms/MicrosoftStyle). Conozca los [10 principales consejos sobre el estilo y el tono de Microsoft](https://docs.microsoft.com/style-guide/top-10-tips-style-voice).

- Use la [plantilla de solicitud de incorporación de cambios](https://github.com/MicrosoftDocs/SCCMdocs/blob/master/PULL_REQUEST_TEMPLATE.md) como punto de partida de su trabajo.

- Siga el [flujo de trabajo de GitHub Flow](https://guides.github.com/introduction/flow/).

- Publique frecuentemente en blogs o en tweets (o donde sea) los contenidos con los que contribuya.

(Esta lista la hemos tomado de la [guía del contribuidor de .NET](https://github.com/dotnet/docs/blob/master/CONTRIBUTING.md#dos-and-donts)).

## <a name="consolidation-of-documentation-for-microsoft-endpoint-manager"></a>Consolidación de la documentación sobre Microsoft Endpoint Manager

Para mejorar la compatibilidad con escenarios combinados de Intune y Configuration Manager, sus bibliotecas de documentación están consolidadas en el [sitio de Microsoft Endpoint Manager](https://docs.microsoft.com/mem). La documentación de Intune ahora está en [docs.microsoft.com/mem/intune](https://docs.microsoft.com/mem/intune), y la documentación de Configuration Manager ahora está en [docs.microsoft.com/mem/configmgr](https://docs.microsoft.com/mem/configmgr). Si todavía usa una URL antigua, se redirigirá automáticamente, por lo que no es necesario realizar ningún cambio para leer este contenido.

Si proporciona algún comentario o contribuye en algún artículo, serán necesarios algunos cambios:

- Los problemas existentes de GitHub permanecen en el repositorio original, [IntuneDocs](https://github.com/MicrosoftDocs/IntuneDocs/issues) o [SCCMDocs](https://github.com/MicrosoftDocs/SCCMDocs/issues).

  - Estos problemas no se mostrarán como problemas abiertos o cerrados en la sección de comentarios del artículo vinculado.

  - Seguiremos trabajando para resolver estas incidencias.

  - En algunos casos, puede que tomemos la difícil decisión de cerrar una incidencia que creemos que no podemos resolver.

  - Si tiene un problema en el repositorio existente y tiene un especial interés al respecto, registre un comentario sobre el artículo migrado en el [repositorio MEMDocs](https://github.com/MicrosoftDocs/MEMDocs).

- Ahora, cuando registre un comentario o edite un artículo, el problema o la solicitud de incorporación de cambios irá al repositorio MEMDocs.
