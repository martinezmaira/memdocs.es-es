---
title: archivo include
description: Archivo de inclusión
author: ErikjeMS
ms.service: microsoft-intune
ms.topic: include
ms.date: 03/30/2020
ms.author: erikje
ms.custom: include file
ms.openlocfilehash: 0b3af293ebc83c14f85abeb0dbaa38ca5187b267
ms.sourcegitcommit: 6a6a713fc1090e03893d80f4259dc7300fb1d5ff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/31/2020
ms.locfileid: "80438714"
---
Estos avisos proporcionan información importante que puede ayudarle a prepararse para las características y los cambios futuros de Intune.

### <a name="microsoft-intune-support-for-windows-10-mobile-ending--3544938--"></a>Fin del soporte técnico de Microsoft Intune para Windows 10 Mobile<!--3544938-->
El soporte técnico estándar de Microsoft para Windows 10 Mobile finalizó en diciembre de 2019. Como se ha mencionado en esta declaración de soporte técnico, los usuarios de Windows 10 Mobile dejarán de recibir de Microsoft nuevas actualizaciones de seguridad, revisiones no relacionadas con la seguridad, opciones gratuitas de soporte técnico asistido o actualizaciones de contenido técnico en línea. En lo referente a todo el soporte técnico del sistema operativo Mobile, el 11 de mayor de 2020 Microsoft Intune finalizará el soporte técnico del Portal de empresa de la aplicación de Windows 10 Mobile y del sistema operativo Windows 10 Mobile.

#### <a name="how-does-this-affect-me"></a>¿Cómo me afecta esto?
Si tiene dispositivos Windows 10 Mobile implementados en su organización, desde ahora y el 11 de mayo de 2020 puede inscribir nuevos dispositivos, agregar o quitar directivas y aplicaciones o actualizar cualquier configuración de administración. Sin embargo, a partir del 11 de mayo, se detendrán las nuevas inscripciones y, finalmente, se eliminará la administración de Windows 10 Mobile de la interfaz de usuario de Intune. Los dispositivos ya no se registrarán en el servicio de Intune y se eliminarán los datos de directivas y dispositivos.  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>¿Qué debo hacer para prepararme para este cambio?
Puede comprobar los informes de Intune para ver qué dispositivos o usuarios pueden verse afectados. Vaya a **Dispositivos** > **Todos los dispositivos** y filtre por sistema operativo. Puede agregar columnas adicionales para ayudar a identificar qué usuarios de su organización tienen dispositivos que ejecutan Windows 10 Mobile. Solicite a los usuarios finales que actualicen sus dispositivos o que dejen de usar los dispositivos para el acceso corporativo.


### <a name="updated-support-statement-for-adobe-acrobat-reader-for-intune-mobile-app--5746776--"></a>Actualizada la instrucción de soporte técnico para la aplicación móvil de Adobe Acrobat Reader para Intune<!--5746776-->
A finales de agosto, publicamos en MC188653 que la aplicación móvil de Adobe Acrobat Reader para Intune llegaría al final de su vida útil el 1 de diciembre de 2019 y que Adobe planeaba admitir las directivas de protección de aplicaciones de Intune dentro de su aplicación principal Acrobat Reader. Desde entonces, recibimos comentarios de los clientes solicitando más tiempo para permitir a los administradores de TI dirigirse a Adobe Acrobat Reader para Intune y a los usuarios finales empezar a utilizarlo. Dado el alto uso de Adobe Acrobat Reader para Intune en los dispositivos de los usuarios finales y su importancia en escenarios empresariales, queremos asegurarnos de que cualquier experiencia cumpla las necesidades de protección de las aplicaciones de su organización. 

Aunque seguimos recomendando establecer como destino la aplicación móvil de Acrobat Reader general en las directivas, ya que la aplicación móvil de Acrobat Reader es compatible con las directivas de protección de aplicaciones y ha integrado el SDK de Intune, se seguirá admitiendo la aplicación Adobe Acrobat Reader para Intune hasta el 31 de marzo de 2020. 

#### <a name="how-does-this-affect-me"></a>¿Cómo me afecta esto?
Está recibiendo este mensaje porque nuestros informes señalan que una o más directivas de la organización tienen como destino la aplicación Adobe Acrobat Reader para Intune o bien ha recibido nuestra comunicación de EOL anterior. 

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>¿Qué debo hacer para prepararme para este cambio?
Informe a los usuarios finales y el departamento de soporte técnico sobre este cambio. Puede usar la [funcionalidad de la información de soporte técnico del Portal de empresa](../apps/company-portal-app.md#support-information) para establecer un canal para preguntas relacionadas con Intune.

#### <a name="additional-information"></a>Información adicional
https://helpx.adobe.com/acrobat/kb/intune-app-end-of-life.html

### <a name="take-action-use-microsoft-edge-for-your-protected-intune-browser-experience--5728447--"></a>Realizar acción: uso de Microsoft Edge para la experiencia de explorador de Intune protegida<!--5728447-->
Como hemos venido anunciando en este último año, Microsoft Edge para dispositivos móviles admite el mismo conjunto de características de administración que Managed Browser, proporcionando al mismo tiempo una experiencia de usuario final mucho mejor. Para dar paso a las sólidas experiencias que proporciona Microsoft Edge, retiraremos Intune Managed Browser. A partir del 27 de enero de 2020, Intune ya no será compatible con Intune Managed Browser.  

#### <a name="how-does-this-affect-me"></a>¿Cómo me afecta esto? 
A partir del 1 de febrero de 2020, Intune Managed Browser ya no estará disponible en Google Play Store o ni en la App Store de iOS. En este punto, aún podrá dirigir nuevas políticas de protección de aplicaciones a Intune Managed Browser, aunque los nuevos usuarios no podrán descargar la aplicación Intune Managed Browser. Además, en iOS, los nuevos clips de web que se inserten en el dispositivo inscrito en MDM se abrirán en Microsoft Edge en lugar de hacerlo en Intune Managed Browser.  

El 31 de marzo de 2020, Intune Managed Browser se quitará de la consola de Azure. Esto significa que ya no podrá crear nuevas directivas para Intune Managed Browser. Las directivas de Intune Managed Browser que tenga actualmente no se verán afectadas. Intune Managed Browser se mostrará en la consola como una aplicación LOB sin icono, y las directivas existentes se seguirán dirigiendo a la aplicación. En este punto, también se quitará la opción de redirigir el contenido web a Intune Managed Browser en la sección Protección de datos de las directivas de protección de aplicaciones.  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>¿Qué debo hacer para prepararme para este cambio? 
Para garantizar una transición fluida de Intune Managed Browser a Microsoft Edge, se recomienda realizar los siguientes pasos de forma proactiva: 

1. Dirija la directiva de protección de aplicaciones (también conocida como MAM) y los parámetros de configuración de la aplicación a Microsoft Edge para iOS y Android. Puede reutilizar las directivas de Intune Managed Browser para Microsoft Edge destinando tales directivas también a Microsoft Edge.  
2. Asegúrese de que todas las aplicaciones protegidas por MAM del entorno tienen la opción de la directiva de protección de aplicaciones "Restringir la transferencia de contenido web con otras aplicaciones" establecida en "Exploradores administrados por directivas". 
3. Diríjase a todas las aplicaciones protegidas por MAM con el parámetro de configuración "com.microsoft.intune.useEdge" establecido en true. A partir del próximo mes, con la versión 1911, podrá llevar a cabo los pasos 2 y 3 simplemente configurando la opción "Restringir la transferencia de contenido web con otras aplicaciones" de manera que tenga "Microsoft Edge" seleccionado en la sección Protección de datos de las directivas de protección de aplicaciones. 

La compatibilidad con los clips de web en iOS y Android estará próximamente disponible. Cuando se publique esta versión, tendrá que cambiar el destino de los clips de web preexistentes para asegurarse de que se abren en Microsoft Edge, en lugar de en Managed Browser. 

#### <a name="additional-information"></a>Información adicional
Consulte la documentación sobre el [uso de Microsoft Edge con directivas de protección de aplicaciones](../apps/manage-microsoft-edge.md) para obtener más información. También puede leer nuestra [entrada de blog sobre el soporte técnico](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Use-Microsoft-Edge-for-your-Protected-Intune-Browser-Experience/ba-p/1004269).

### <a name="end-of-support-for-legacy-pc-management"></a>Fin de la compatibilidad con la administración heredada de equipos

La administración heredada de equipos dejará de ser compatible el 15 de octubre de 2020. Actualice los dispositivos a Windows 10 y vuelva a inscribirlos como dispositivos de administración de dispositivos móviles (MDM) para administrarlos por Intune.

[Más información](https://go.microsoft.com/fwlink/?linkid=2107122).


