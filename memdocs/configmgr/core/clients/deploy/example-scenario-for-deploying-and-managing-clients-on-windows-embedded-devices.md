---
title: 'Escenario de ejemplo: implementación de clientes de Windows Embedded'
titleSuffix: Configuration Manager
description: Vea un escenario de ejemplo para implementar y administrar clientes de Configuration Manager en dispositivos Windows Embedded.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 10049c89-b37c-472b-b317-ce4f56cd4be7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18e6252a3528e62153e7226ff285d24cd6ecf013
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693873"
---
# <a name="example-scenario-for-deploying-and-managing-configuration-manager-clients-on-windows-embedded-devices"></a>Escenario de ejemplo para implementar y administrar clientes de Configuration Manager en dispositivos Windows Embedded

*Se aplica a: Configuration Manager (rama actual)*

En este escenario se muestra cómo administrar los dispositivos Windows Embedded con filtros de escritura habilitados con Configuration Manager. Si los dispositivos incrustados no admiten filtros de escritura, se comportan como clientes estándar de Configuration Manager y no se aplican estos procedimientos.  

Coho Vineyard & Winery está abriendo un centro de visitantes y necesita quioscos con Windows Embedded para ejecutar presentaciones interactivas. El edificio del nuevo centro de visitantes no se encuentra cerca del departamento de TI, por lo que los quioscos se tienen que administrar de forma remota. Además del software que ejecuta las presentaciones, estos dispositivos deben contar con software de protección contra malware actualizado para cumplir las directivas de seguridad de la empresa. Los quioscos deben ejecutarse 7 días a la semana, sin tiempo de inactividad mientras esté abierto el centro de visitantes.  

 Coho ya ejecuta Configuration Manager para administrar dispositivos en su red. Configuration Manager está configurado para ejecutar Endpoint Protection e instalar actualizaciones de software y aplicaciones. Pero, como el equipo de TI no ha administrado nunca dispositivos de Windows Embedded, el administrador de Configuration Manager realiza una prueba piloto para administrar dos quioscos en el vestíbulo de recepción.   

 Para administrar estos dispositivos de Windows Embedded con filtros de escritura habilitados, el administrador realiza los pasos siguientes para instalar el cliente de Configuration Manager, protegerlo mediante Endpoint Protection e instalar el software de presentación interactiva.  

1. El administrador de Configuration Manager lee cómo los dispositivos de Windows Embedded usan filtros de escritura y cómo Configuration Manager puede hacerlo más fácil al deshabilitar y volver a habilitar automáticamente los filtros de escritura para conservar una instalación de software.  

    Para obtener más información, vea [Planeación de la implementación del cliente en dispositivos Windows Embedded](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

2. Antes de instalar el cliente de Configuration Manager, el administrador crea una recopilación de dispositivos basada en consultas para los dispositivos de Windows Embedded. Como en la empresa se usan formatos de nombre estándar para identificar los equipos, el administrador puede identificar de forma exclusiva los dispositivos de Windows Embedded por las seis primeras letras del nombre de equipo: **WEMDVC**. El administrador usa la siguiente consulta WQL para crear esta recopilación: **select SMS_R_System.NetbiosName from SMS_R_System where SMS_R_System.NetbiosName like "WEMDVC%"** .  

    Esta recopilación le permite administrar los dispositivos de Windows Embedded con distintas opciones de configuración desde los demás dispositivos. El administrador usará esta recopilación para controlar los reinicios, implementar Endpoint Protection con las configuraciones de cliente e implementar la aplicación de presentación interactiva.  

    Vea [Cómo crear recopilaciones](../../../core/clients/manage/collections/create-collections.md).  

3. El administrador configura la recopilación durante una ventana de mantenimiento para asegurarse de que los reinicios que puedan requerirse para la instalación de la aplicación de presentación interactiva y cualquier actualización no se produzcan durante el horario de apertura del centro de informaciones. El horario de apertura será de 09:00 a 18:00, de lunes a domingo. El administrador configura la ventana de mantenimiento para todos los días, de 18:30 a 06:00.  

4. Para obtener más información, consulte [How to Use Maintenance Windows in Configuration Manager](../../../core/clients/manage/collections/use-maintenance-windows.md) (Uso de ventanas de mantenimiento en Configuration Manager).  

5. Después, establece una configuración cliente de dispositivo personalizada para instalar el cliente de Endpoint Protection mediante la selección de **Sí** para las siguientes opciones y, luego, implementa esta configuración de cliente personalizada en la recopilación de dispositivos de Windows Embedded:  

   - **Instalar cliente de Endpoint Protection en equipos cliente**  

   - **Para dispositivos de Windows Embedded con filtros de escritura, confirmar la instalación del cliente de Endpoint Protection (reinicio necesario)**  

   - **Permitir la instalación y los reinicios del cliente de Endpoint Protection fuera de las ventanas de mantenimiento**  

     Cuando se instala el cliente de Configuration Manager, estas opciones instalan el cliente de Endpoint Protection y aseguran que se conserven en el sistema operativo como parte de la instalación, en lugar de que solo se escriban en la superposición. Las directivas de seguridad de la empresa requieren que siempre se instale software de protección contra malware, y el administrador no quiere correr el riesgo de que los quioscos estén desprotegidos durante incluso un breve periodo de tiempo si se reinician.  

   > [!NOTE]  
   >  Los reinicios necesarios para instalar el cliente de Endpoint Protection solo se producen una vez durante el período de instalación para los dispositivos y antes de que el centro de informaciones esté operativo. A diferencia de la implementación periódica de aplicaciones o de actualizaciones de definiciones de software, la próxima vez que se instale el cliente de Endpoint Protection en el mismo dispositivo probablemente será cuando la empresa se actualice a la siguiente versión de Configuration Manager.  

    Para más información, vea [Configuración de Endpoint Protection](../../../protect/deploy-use/endpoint-protection-configure.md).  

6. Una vez establecidas las opciones de configuración del cliente, el administrador se prepara para instalar los clientes de Configuration Manager. Antes de que pueda instalar los clientes, debe deshabilitar manualmente el filtro de escritura en los dispositivos de Windows Embedded. El administrador lee la documentación del OEM que acompaña a los quioscos y sigue sus instrucciones para deshabilitar los filtros de escritura.  

    Cambia el nombre al dispositivo para que use el formato de nombres estándar de la empresa y luego instala el cliente manualmente. Para ello, ejecuta CCMSetup con el comando siguiente desde una unidad asignada que contiene los archivos de código fuente del cliente: **CCMSetup.exe /MP:mpserver.cohovineyardandwinery.com SMSSITECODE=CO1**  

    Este comando instala el cliente, lo asigna al punto de administración que tiene la intranet FQDN de **mpserver.cohovineyardandwinery.com**, y lo asigna al sitio primario denominado **CO1**.  

    El administrador sabe que siempre se tarda un tiempo en instalar los clientes y enviar su estado al sitio. Por eso, espera antes de confirmar que los clientes se instalan correctamente, se asignan al sitio y aparecen como clientes en la recopilación que ha creado para los dispositivos de Windows Embedded.  

    Como confirmación adicional, el administrador comprueba las propiedades de Configuration Manager en el Panel de control de los dispositivos y las compara con los equipos Windows estándar que administra el sitio. Por ejemplo, en la pestaña **Componentes** , el **Agente de inventario de hardware** muestra **Habilitado**, y en la pestaña **Acciones** hay 11 acciones disponibles, que incluyen **Ciclo de evaluación de implementación de aplicaciones** y **Ciclo de recopilación de datos de descubrimiento**.  

    Con la seguridad de que los clientes se han instalado correctamente, se han asignado y reciben la directiva de cliente desde el punto de administración, el administrador habilita manualmente los filtros de escritura conforme a las instrucciones del OEM.  

    Para obtener más información, vea:  

   -   [Implementar clientes en equipos Windows](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

   -   [Cómo asignar clientes a un sitio](../../../core/clients/deploy/assign-clients-to-a-site.md)  

7. Ahora que el cliente de Configuration Manager está instalado en los dispositivos de Windows Embedded, el administrador confirma que puede administrarlos como hace con los clientes de Windows estándar. Por ejemplo, desde la consola de Configuration Manager, el administrador puede administrarlos de forma remota por medio del control remoto, iniciar la directiva de cliente para los mismos y ver las propiedades del cliente y el inventario de hardware.  

    Como estos dispositivos están unidos a un dominio de Active Directory, no necesita aprobarlos de forma manual como clientes de confianza, y confirma que están aprobados desde la consola de Configuration Manager.  

    Para obtener más información, vea [Cómo administrar clientes](../../../core/clients/manage/manage-clients.md).  

8. Para instalar el software de presentación interactiva, el administrador ejecuta el **Asistente para implementar software** y configura una aplicación requerida. En la página **Experiencia del usuario** del asistente, en la sección **Tratamiento de filtros de escritura para dispositivos de Windows Embedded**, acepta la opción predeterminada que selecciona **Confirmar cambios dentro de la fecha límite o en una ventana de mantenimiento (reinicio necesario)** .  

    El administrador mantiene esta opción predeterminada para los filtros de escritura para asegurarse de que la aplicación se conserve después del reinicio, de modo que siempre esté disponible para los visitantes que usan los quioscos. La ventana de mantenimiento diaria proporciona un período seguro durante el cual pueden producirse los reinicios para la instalación y cualquier actualización.  

    El administrador implementa la aplicación en la recopilación de dispositivos de Windows Embedded.  

    Para más información, vea [Cómo implementar aplicaciones con Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

9. Para configurar las actualizaciones de definición para Endpoint Protection, el administrador usa actualizaciones de software y ejecuta el Asistente para crear regla de implementación automática. Selecciona la plantilla **Actualizaciones de definición** para rellenar previamente el asistente con opciones adecuadas para Endpoint Protection.  

     Estas opciones incluyen lo siguiente en la página **Experiencia del usuario** del asistente:  

   - **Comportamiento de la fecha límite**: la casilla **Instalación de software** no está seleccionada.  

   - **Tratamiento de filtros de escritura para dispositivos de Windows Embedded**: la casilla **Commit changes at deadline or during a maintenance window (requires restarts)** (Confirmar cambios dentro de la fecha límite o en una ventana de mantenimiento (reinicio necesario)) no está seleccionada.  

     El administrador mantiene estas opciones predeterminadas. Juntas, estas dos opciones con esta configuración permiten que se instale cualquier definición de actualizaciones de software para Endpoint Protection en la superposición durante el día y no esperar a que se instalen y confirmen durante la ventana de mantenimiento. Esta es la configuración que mejor satisface la directiva de seguridad de la empresa para que los equipos ejecuten protección contra malware actualizada.  

     > [!NOTE]  
     >  A diferencia de las instalaciones de software para aplicaciones, las definiciones de actualizaciones de software para Endpoint Protection pueden producirse con mucha frecuencia, incluso varias veces al día. Suelen ser archivos pequeños. Para estos tipos de implementaciones relacionadas con la seguridad, suele ser beneficioso realizar siempre la instalación en la superposición en lugar de esperar a la ventana de mantenimiento. El cliente de Configuration Manager volverá a instalar rápidamente las actualizaciones de definiciones de software si el dispositivo se reinicia porque esta acción inicia una comprobación de evaluación y no espera hasta la próxima evaluación programada.  

     El administrador selecciona la recopilación de dispositivos de Windows Embedded para la regla de implementación automática.  

     Para obtener más información, consulte  
               Paso 3: Configurar las actualizaciones de software de Configuration Manager para entregar actualizaciones de definiciones a los equipos cliente en el artículo [Configuración de Endpoint Protection](../../../protect/deploy-use/endpoint-protection-configure.md)  

10. El administrador decide configurar una tarea de mantenimiento que confirma periódicamente todos los cambios en la superposición. Esta tarea se realiza para admitir la implementación de las definiciones de actualizaciones de software y reducir el número de actualizaciones que se acumulan y que deben volver a instalarse, cada vez que se reinicia el dispositivo. Por experiencia, el administrador sabe que esto ayuda a que los programas de protección contra malware se ejecuten de forma más eficaz.  

    > [!NOTE]  
    >  Estas definiciones de actualizaciones de software se confirmarían de forma automática en la imagen si los dispositivos incrustados ejecutaran otra tarea de administración que admitiera la confirmación de los cambios. Por ejemplo, la instalación de una nueva versión del software de presentación interactiva también confirmaría los cambios para las definiciones de actualizaciones de software. O bien la instalación de actualizaciones de software estándar todos los meses que se instalen durante la ventana de mantenimiento también podría confirmar los cambios correspondientes a las definiciones de actualizaciones de software. Sin embargo, en este escenario, en el que no se ejecutan actualizaciones de software estándar y es probable que el software de presentación interactiva no se actualice muy a menudo, podrían pasar meses antes de que las actualizaciones de definiciones de software se confirmen de forma automática en la imagen.  

     El administrador crea primero una secuencia de tareas personalizada sin ninguna configuración más que el nombre. Ejecuta al Asistente para crear secuencia de tareas:  

    1. En la página **Crear una nueva secuencia de tareas**, el administrador selecciona **Crear una nueva secuencia de tareas personalizada** y, después, hace clic en **Siguiente**.  

    2. En la página **Información de secuencia de tareas**, el administrador escribe **Tarea de mantenimiento para confirmar cambios en los dispositivos incrustados** para el nombre de la secuencia de tareas y después hace clic en **Siguiente**.  

    3. En la página **Resumen**, el administrador selecciona **Siguiente** y completa el asistente.  

       Después, el administrador implementa esta secuencia de tareas personalizada en la colección de dispositivos de Windows Embedded, y configura la programación para que se ejecute todos los meses. Como parte de la configuración de la implementación, activa la casilla **Confirmar cambios dentro de la fecha límite o en una ventana de mantenimiento (reinicio necesario)** para conservar los cambios después del reinicio. Para configurar esta implementación, el administrador selecciona la secuencia de tareas personalizada que acaba de crear y, después, en la pestaña **Inicio**, en el grupo **Implementación**, hace clic en **Implementar** para iniciar el Asistente para implementar software:  

    4. En la página **General**, el administrador selecciona la colección de dispositivos de Windows Embedded y, después, hace clic en **Siguiente**.  

    5. En la página **Configuración de implementación**, selecciona el **Propósito** **Requerido** y, después, hace clic en **Siguiente**.  

    6. En la página **Programación**, el administrador hace clic en **Nueva** para especificar una programación semanal durante la ventana de mantenimiento y, después, hace clic en **Siguiente**.  

    7. El administrador completa al asistente sin realizar más cambios.  

       Para obtener más información, consulte  
                 [Administrar secuencias de tareas para automatizar tareas](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).  

11. Para que los quioscos se ejecuten de forma automática, el administrador escribe un script para configurar las opciones siguientes de los dispositivos:  

    - Iniciar sesión automáticamente, utilizando una cuenta de invitado sin contraseña.  

    - Ejecutar automáticamente el software de presentación interactiva durante el inicio.  

      El administrador usa paquetes y programas para implementar este script en la colección de dispositivos de Windows Embedded. Al ejecutar el Asistente para implementar software, activa de nuevo la casilla **Confirmar cambios dentro de la fecha límite o en una ventana de mantenimiento (reinicio necesario)** para conservar los cambios después del reinicio.  

      Para obtener más información, consulte [Paquetes y programas](../../../apps/deploy-use/packages-and-programs.md).  

12. La mañana siguiente, el administrador comprueba los dispositivos de Windows Embedded. Confirma lo siguiente:  

    - El quiosco inicia sesión automáticamente mediante la cuenta de usuario invitado.  

    - Se está ejecutando el software de presentación interactiva.  

    - El cliente de Endpoint Protection está instalado y tiene las últimas definiciones de actualizaciones de software.  

    - El dispositivo se reinició durante la ventana de mantenimiento.  

      Para obtener más información, vea:  

    - [Supervisión de Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md)  

    - [Supervisión de aplicaciones con Configuration Manager](../../../apps/deploy-use/monitor-applications-from-the-console.md)  

13. El administrador supervisa los quioscos e informa a su director sobre la administración correcta de los mismos. Como resultado, se produce un pedido de 20 quioscos para el centro de informaciones.  

     Para evitar la instalación manual del cliente de Configuration Manager, que precisa la deshabilitación y habilitación manual de los filtros de escritura, el administrador se asegura de que el pedido incluya una imagen personalizada con la asignación de sitio e instalación del cliente de Configuration Manager. Además, los nombres de los dispositivos se asignan en función del formato de nombres de la compañía.  

     Los quioscos se entregan al centro de informaciones una semana antes de su apertura. Durante este tiempo, los quioscos están conectados a la red, toda la administración de dispositivos es automática y no se requiere ningún administrador local. El administrador confirma que los quioscos están funcionando como corresponde:  

    -   Los clientes de los quioscos completan la asignación de sitios y descargan la clave raíz confiable de Servicios de dominio de Active Directory.  

    -   Los clientes de los quioscos se agregan automáticamente a la recopilación de dispositivos de Windows Embedded y se configuran con la ventana de mantenimiento.  

    -   El cliente de Endpoint Protection se instala y tiene las definiciones de actualizaciones de software más recientes para garantizar la protección contra malware.  

    -   El software de presentación interactiva se instala y se ejecuta automáticamente, y está listo para que los visitantes lo utilicen.  

14. Después de esta instalación inicial, los reinicios que pueden ser necesarios para las actualizaciones solo se producen cuando el centro de informaciones está cerrado.  
