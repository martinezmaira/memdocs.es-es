---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 08/23/2019
ms.openlocfilehash: d8eaaa403bd1dd97214b4eff82be79d5c2a6566e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690403"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
1. En la consola de Configuration Manager, vaya al área de trabajo **Administración**, expanda **Servicios en la nube** y seleccione el nodo **Administración conjunta**. Haga clic en **Configurar administración conjunta** en la cinta para abrir el **Asistente para la configuración de administración conjunta**.

2. En la página **Suscripción** del asistente, seleccione **Iniciar sesión**. Inicie sesión en su inquilino de Intune y después haga clic en **Siguiente**.  

3. En la página **Habilitación**, elija la opción **Inscripción automática en Intune**, ya sea **Piloto** o **Todo**. Si el usuario anula la inscripción de un dispositivo, se volverá a inscribir en la siguiente evaluación de la directiva. <!--3330596--> 

    Esta acción permite la inscripción automática de clientes en Intune para los clientes existentes de Configuration Manager. Si elige **Piloto**, solo los clientes de Configuration Manager que sean miembros de la colección piloto se inscribirán de forma automática en Intune. Esta opción permite habilitar la administración conjunta en un subconjunto de los clientes para probarla inicialmente e implementarla con un enfoque por fases. 

    > [!Note]  
    > A partir de la versión 1806, la inscripción automática no es inmediata para todos los clientes. Este comportamiento ayuda a escalar la inscripción mejor para entornos de gran tamaño. Configuration Manager aleatoriza la inscripción según el número de clientes. Por ejemplo, si el entorno tiene 100 000 clientes, cuando se habilita esta configuración, la inscripción tiene lugar durante varios días.<!--1358003-->  

4. En el caso de los dispositivos de Internet ya inscritos en Intune, copie y guarde la línea de comandos en la página **Habilitación**. Puede usar esta línea de comandos para instalar el cliente de Configuration Manager como aplicación en Intune. Si no guarda ahora esta línea de comandos, puede revisar la configuración de la administración conjunta en cualquier momento para obtener esta línea de comandos.

5. En la página **Cargas de trabajo**, elija para cada carga de trabajo el grupo de dispositivos que quiere pasar a la administración con Intune. Para más información, consulte [Cargas de trabajo](../workloads.md).  

    Si solo quiere habilitar la administración conjunta, no es necesario que cambie ahora las cargas de trabajo. Puede cambiarlas más adelante. Para más información, consulte el artículo sobre el [cambio de las cargas de trabajo](../how-to-switch-workloads.md).  

    El valor **Intune piloto** cambia la carga de trabajo asociada solo para los dispositivos de la colección Piloto. La configuración **Intune** cambia la carga de trabajo asociada para todos los dispositivos Windows 10 administrados conjuntamente.  

    > [!Important]
    > Antes de cambiar las cargas de trabajo, asegúrese de que la carga de trabajo correspondiente en Intune se configuró e implementó correctamente. Asegúrese de que las cargas de trabajo siempre se administren mediante una de las herramientas de administración para los dispositivos.  

6. En la página **Almacenamiento provisional**, configure estas opciones:  

    - **Piloto**: el grupo piloto contiene una o varias recopilaciones que seleccione. Use este grupo como parte de la implementación por fases de la administración conjunta. Comience con una colección de prueba pequeña y, luego, agregue más colecciones al grupo piloto a medida que implemente la administración conjunta en más usuarios y dispositivos. Puede cambiar las colecciones del grupo piloto en cualquier momento.  

    - **Producción**: configure el **grupo de exclusión** con una o varias recopilaciones. Los dispositivos que forman parte de cualquiera de las colecciones de este grupo se excluyen del uso de la administración conjunta.  

7. Para habilitar la administración conjunta, siga los pasos del asistente.  
