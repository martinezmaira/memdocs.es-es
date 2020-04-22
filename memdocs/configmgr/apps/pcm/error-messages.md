---
title: Mensajes de error
titleSuffix: Configuration Manager
description: Obtenga información sobre los mensajes de error del Administrador de conversión de paquetes.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0d3cf6e1-b295-4b05-821d-e9f57c74ca14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4d4a2fa66dc1c4a8af3b3f7f16c67d58edebb5fa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688973"
---
# <a name="technical-reference-for-package-conversion-manager-error-messages"></a>Referencia técnica de mensajes de error del Administrador de conversión de paquetes

*Se aplica a: Configuration Manager (rama actual)*

<!--1357861-->

En este artículo se describen los mensajes de error que se muestran en el Administrador de conversión de paquetes. También incluye las posibles causas del error y los métodos para corregirlo. El Administrador de conversión de paquetes registra los mensajes de error en **PCMTrace.log**. Para más información, incluso sobre cómo controlar el nivel de detalle, vea [Archivos de registro](troubleshoot-pcm.md#log-files).


#### <a name="application-creation-failed-with-the-following-exception"></a>Error en la creación de aplicaciones con la siguiente excepción

La excepción especificada se produjo durante el envío del objeto de aplicación al servidor de Configuration Manager.

Compruebe sus permisos en Configuration Manager, valide la conectividad y vuelva a intentarlo. Si esas acciones no corrigen el problema, examine los archivos **PCMtrace.log** (nivel de detalle 4) y **SMSProv.log**.


#### <a name="conversion-error--applies-to-a-package-transform-status"></a>Error de conversión: SE APLICA AL ESTADO DE TRANSFORMACIÓN DE UN PAQUETE

Se ha producido una excepción general durante la conversión del paquete. Mire el archivo de registro **PCMtrace.log** (nivel de detalle 4).

Compruebe los permisos de usuario para el recurso compartido de red (origen de datos del paquete), valide su conectividad y vuelva a intentarlo. Si esas acciones no corrigen el problema, examine el archivo **PCMtrace.log** (nivel de detalle 4).


#### <a name="did-not-find-a-converted-package-and-its-resultant-application-in-the-workflow-outputs"></a>No se encontró un paquete convertido y su aplicación resultante en las salidas de flujo de trabajo
Se ha eliminado la aplicación (paquete o programa convertido).

Modifique el paquete o programa dependiente para asegurarse de que existe.


#### <a name="objects-were-not-created-successfully"></a>Los objetos no se crearon correctamente
Hay varias causas posibles.

Compruebe sus permisos en Configuration Manager, valide la conectividad y vuelva a intentarlo. Si esas acciones no corrigen el problema, examine los archivos **PCMtrace.log** (nivel de detalle 4) y **SMSProv.log**.


#### <a name="please-close-the-wizard-and-resolve-any-issues-with-the-selected-package-see-pcmtracelog-for-more-details"></a>Cierre al asistente y resuelva cualquier problema con el paquete seleccionado. Consulte PCMTrace.Log para obtener más detalles
Hay varias causas posibles.

Compruebe sus permisos en Configuration Manager, valide la conectividad y vuelva a intentarlo. Si esas acciones no corrigen el problema, examine los archivos **PCMtrace.log** (nivel de detalle 4) y **SMSProv.log**.


#### <a name="some-deployment-types-are-missing-detection-methods-all-deployment-types-must-have-detection-methods"></a>A algunos tipos de implementación les faltan métodos de detección. Todos los tipos de implementación deben tener métodos de detección
Faltan métodos de detección en el programa.

Agregue uno o varios métodos de detección durante el proceso **Corregir y convertir**.


#### <a name="there-was-an-error-preparing-the-package-for-conversion"></a>Se produjo un error al preparar el paquete para la conversión
Hay varias causas posibles.

Compruebe sus permisos en Configuration Manager, valide la conectividad y vuelva a intentarlo. Si esas acciones no corrigen el problema, examine los archivos **PCMtrace.log** (nivel de detalle 4) y **SMSProv.log**.


