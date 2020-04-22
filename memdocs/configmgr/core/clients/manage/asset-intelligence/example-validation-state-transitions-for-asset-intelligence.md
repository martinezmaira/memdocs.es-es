---
title: Transiciones de estado de validación de ejemplo
titleSuffix: Configuration Manager
description: Vea ejemplos de transiciones de estado de validación de Asset Intelligence en Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6230a6e5-a1f6-459b-84f1-07fbde0e70f0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2af9243d6720d5821c641e5c80589457a33b638e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695083"
---
# <a name="example-validation-state-transitions-for-asset-intelligence"></a>Ejemplo de transiciones de estado de validación de Asset Intelligence

*Se aplica a: Configuration Manager (rama actual)*

Los estados de validación de Asset Intelligence en Configuration Manager no son estáticos y pueden cambiar debido a las acciones administrativas que realiza y que afectan a los datos almacenados en el catálogo de Asset Intelligence. En este tema se proporcionan ejemplos de posibles transiciones de estado de validación.

##  <a name="uncategorized-catalog-item-is-categorized-by-the-administrative-user"></a><a name="BKMK_UncategorizedIsCategorized"></a> El usuario administrativo categoriza un elemento de catálogo sin categoría  

|**Transición de estado**|**Descripción de la transición de estado**|  
|--------------------------|--------------------------------------|  
|**Sin categoría**|Un título de software inventariado que System Center Online no ha categorizado previamente o que el usuario administrativo ha entrado en el catálogo de Asset Intelligence.|  
|**Sin categoría** a **Definido porel usuario**|El usuario administrativo categoriza el elemento sin categoría.|  

##  <a name="categorized-catalog-item-is-recategorized-by-the-administrative-user"></a><a name="BKMK_CategorizedIsReCategorized"></a> El usuario administrativo vuelve a categorizar un elemento de catálogo con categoría  

|**Transición de estado**|**Descripción de la transición de estado**|  
|--------------------------|--------------------------------------|  
|**Validado**|Investigadores de System Center Online han definido el elemento de catálogo y está presente en el catálogo de Asset Intelligence.|  
|**Validado** a **Definido por el usuario**|El usuario administrativo vuelve a categorizar el elemento de catálogo validado.|  

> [!NOTE]  
>  Como la información de categorización obtenida de System Center Online se almacena en la base de datos y no se puede eliminar, el usuario administrativo puede revertir a la categorización de System Center Online más adelante.  

##  <a name="user-defined-catalog-item-is-recategorized-by-system-center-online"></a><a name="BKMK_UserDefinedIsRecategorized"></a> System Center Online vuelve a categorizar el elemento de catálogo definido por el usuario  

|**Transición de estado**|**Descripción de la transición de estado**|  
|--------------------------|--------------------------------------|  
|**Sin categoría**|System Center Online o el usuario administrativo no han categorizado previamente un título de software inventariado entrado en el catálogo de Asset Intelligence.|  
|**Definido por el usuario**|El usuario administrativo categoriza el elemento sin categoría.|  
|**Definido por el usuario** a **Actualizable**|System Center Online ha categorizado de forma diferente un elemento de catálogo definido por el usuario durante las actualizaciones masivas manuales subsiguientes del catálogo Asset Intelligence.<br /><br /> El usuario administrativo puede emplear el cuadro de diálogo **Resolución de conflicto de detalles de software** para decidir si quiere usar la nueva información de categorización o el valor definido por el usuario anterior.|  
|**Actualizable** a **Validado**|El usuario administrativo emplea el cuadro de diálogo **Resolución de conflicto de detalles de software** para usar la nueva información de categorización recibida de System Center Online durante la actualización del catálogo anterior.|  
|o bien||  
|**Actualizable** a **Definido por el usuario**|El usuario administrativo que emplea el cuadro de diálogo **Resolución de conflicto de detalles de software** para usar el valor definido por el usuario anterior.|  

> [!NOTE]  
>  Como la información de categorización obtenida de System Center Online se almacena en la base de datos y no se puede eliminar, el usuario administrativo puede revertir a la categorización de System Center Online más adelante.  

##  <a name="uncategorized-catalog-item-is-submitted-to-system-center-online-for-categorization"></a><a name="BKMK_UncategorizedIsSubmitted"></a> El elemento de catálogo sin categoría se envía a System Center Online para la categorización  

|**Transición de estado**|**Descripción de la transición de estado**|  
|--------------------------|--------------------------------------|  
|**Sin categoría**|System Center Online o el usuario administrativo no han categorizado previamente un título de software inventariado entrado en la base de datos de Asset Intelligence.|  
|**Sin categorizar** a **Pendiente**|El elemento sin categoría se envía a System Center Online para que el usuario administrativo lo categorice.|  
|**Pendiente** a **Validado**|System Center Online categoriza el elemento. El usuario administrativo importa el elemento al catálogo de Asset Intelligence mediante una actualización masiva del catálogo o una sincronización del catálogo de Asset Intelligence. Ambos están disponibles mediante el rol de sistema de sitio de punto de sincronización de Asset Intelligence.|  

##  <a name="user-defined-catalog-item-is-submitted-to-system-center-online-for-categorization"></a><a name="BKMK_UserDefinedIsSubmitted"></a> El elemento de catálogo definido por el usuario se envía a System Center Online para la categorización  

|**Transición de estado**|**Descripción de la transición de estado**|  
|--------------------------|--------------------------------------|  
|**Sin categoría**|System Center Online o un usuario administrativo no han categorizado previamente un título de software inventariado entrado en la base de datos de Asset Intelligence.|  
|**Definido por el usuario**|Ha categorizado el elemento sin categoría.|  
|**Definido por el usuario** a **Pendiente**|Envía el elemento definido por el usuario a System Center Online para la categorización.|  
|**Pendiente** a **Actualizable**|System Center Online ha categorizado de forma diferente un elemento de catálogo definido por el usuario durante una sincronización del catálogo posterior. Puede usar la acción **Resolver conflicto** para decidir si quiere usar la nueva información de categorización o el valor definido por el usuario anterior. Para obtener más información sobre cómo resolver conflictos, consulte [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails) (Resolver conflictos de detalles de software).|  
|**Actualizable** a **Validado**|Ha usado la acción **Resolver conflicto** y seleccionado la nueva información de categorización recibida de System Center Online durante la actualización anterior del catálogo. Para obtener más información sobre cómo resolver conflictos, consulte [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails) (Resolver conflictos de detalles de software).|  
|o bien||  
|**Actualizable** a **Definido por el usuario**|Ha usado la acción **Resolver conflicto** y seleccionado usar el valor definido por el usuario anterior. Para obtener más información sobre cómo resolver conflictos, consulte [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails) (Resolver conflictos de detalles de software).|  

> [!NOTE]  
>  Como la información de categorización obtenida de System Center Online se almacena en la base de datos y no se puede eliminar, puede revertir a la categorización de System Center Online más adelante.  
