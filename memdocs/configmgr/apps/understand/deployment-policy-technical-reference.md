---
title: Referencia técnica de directivas de implementación de aplicaciones
titleSuffix: Configuration Manager
description: Referencia técnica para la solución de problemas de directivas de implementación de aplicaciones para Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: bf24fb83-521f-4a41-ab8e-df70a6c10e78
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 51d260ede4ed275c401c3b9f9e131134c62ae74e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688833"
---
# <a name="application-deployment-policy"></a>Directiva de implementación de aplicaciones

*Se aplica a: Configuration Manager (rama actual)*

## <a name="policy-creation"></a>Creación de directivas

Cuando se implementa una aplicación, se crea una instancia de la clase [SMS_ApplicationAssignment](../../develop/reference/apps/sms_applicationassignment-server-wmi-class.md), que representa la asignación de una aplicación a una colección. Se puede realizar el seguimiento de esta actividad en **SMSProv.log**.

<pre><code class="lang-text">SMS Provider    PutInstanceAsync <b>SMS_ApplicationAssignment</b>~
SMS Provider    Auditing: User CONTOSO\Admin created an instance of class SMS_ApplicationAssignment.~
</code></pre>

En la base de datos de Configuration Manager, esta información se almacena en la tabla `CI_CIAssignments`, donde `AssignmentType` 2 representa la implementación de una aplicación. Cuando se crea la asignación, el componente Monitor de base de datos de SMS detecta un cambio en la tabla y, después, notifica al Administrador de replicaciones de objetos que procese la directiva de asignación de CI (CIA). Luego, el componente Administrador de replicaciones de objetos crea la directiva para la asignación de la aplicación en la base de datos, que se almacena en la tabla `Policy` de la base de datos, y el id. de directiva se basa en el id. único de la aplicación. Se puede realizar el seguimiento de esta actividad en **objreplmgr.log** si se hace referencia al id. único de asignación, que se puede obtener de la consulta SQL a la que se hace referencia en la sección [Antes de empezar](app-deployment-technical-reference.md#before-you-begin).

<pre><code class="lang-text">***** Processing Application Assignment {<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>} *****
</code></pre>

La directiva para la asignación de la aplicación se puede ver en la base de datos mediante una consulta SQL similar a la siguiente.

```sql
SELECT P.PolicyID, PA.PolicyAssignmentID, PA.PADBID, PA.IsTombstoned, PA.LastUpdateTime FROM Policy P
JOIN PolicyAssignment PA ON P.PolicyID = PA.PolicyID
WHERE P.PolicyID = '{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}' -- Replace Assignment Unique ID
```

## <a name="policy-targeting"></a>Destino de la directiva

Una vez que se ha generado la directiva, el componente Proveedor de directivas la asigna a los recursos de la colección a la que se destina la implementación de la aplicación. La información de destino de la directiva se almacena en la tabla `ResPolicyMap` de la base de datos. Puede usar el valor PADBID que devuelve la consulta anterior para realizar el seguimiento de esta actividad en **policypv.log**. Pero es posible que el valor PADBID en el registro no siempre coincida con el que devuelve la consulta anterior si se procesan varias directivas al mismo tiempo.

<pre><code class="lang-text">~Policy or Policy Target Change Event triggered.
~Completed batch with beginning <b>PADBID = 16778403 ending PADBID = 16778403</b>.
</code></pre>

> [!NOTE]
> La tabla `ResPolicyMap` no contiene ninguna información de destino para las aplicaciones que se implementan como **Disponibles** en las colecciones de usuarios. El Centro de software consulta una lista de estas aplicaciones desde el punto de administración, y la información de destino de la directiva para estas aplicaciones se genera de forma dinámica cuando un usuario solicita una aplicación desde el Centro de software.

## <a name="next-steps"></a>Pasos siguientes

- [Implementación de aplicaciones en colecciones de dispositivos](device-deployment-technical-reference.md)
- [Implementación de aplicaciones en colecciones de usuarios](user-deployment-technical-reference.md)
