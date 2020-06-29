---
title: Administración de directivas seguridad de puntos de conexión en Microsoft Intune | Microsoft Docs
description: Obtenga información sobre cómo los administradores de seguridad pueden usar los perfiles y directivas de seguridad de puntos de conexión para centrarse en la configuración de seguridad de los dispositivos en Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 071cab69b652193b835282603e187e4f3d0c7b0d
ms.sourcegitcommit: 97f150f8ba8be8746aa32ebc9b909bb47e22121c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84879729"
---
# <a name="manage-device-security-with-endpoint-security-policies-in-microsoft-intune"></a>Administración de la seguridad de los dispositivos con directivas seguridad de puntos de conexión en Microsoft Intune

Como administrador de seguridad, use las directivas de *seguridad de puntos de conexión* de Intune para configurar la seguridad de los dispositivos sin el engorro de tener que desplazarse por todas las opciones de los perfiles de configuración y líneas base de seguridad de los dispositivos.

Cada tipo de directiva admite uno o varios perfiles. Los perfiles es donde las opciones se configuran, y pueden agrupar opciones de diferentes plataformas o distintas áreas de importancia dentro del área de directiva, más amplia.

Encontrará estas directivas en *Administrar*, en el nodo **Seguridad de los puntos de conexión** del [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

![Administrar directivas](./media/endpoint-security-policy/endpoint-security-policies.png)

Aquí se describe brevemente de cada tipo de directiva de seguridad de puntos de conexión. Para obtener más información al respecto, incluidos los perfiles disponibles para cada una de ellas, use los vínculos que llevan a contenido dedicado a cada tipo de directiva:

- [Antivirus](../protect/endpoint-security-antivirus-policy.md): las directivas de antivirus ayudan a los administradores de seguridad a centrarse en administrar el grupo diferenciado de opciones de antivirus para dispositivos administrados. Para usar una directiva de antivirus, integre Intune con Advanced Threat Protection de Microsoft Defender (ATP de Microsoft Defender) como una solución de Mobile Threat Defense.

- [Cifrado de disco](../protect/endpoint-security-disk-encryption-policy.md): los perfiles de cifrado de disco de seguridad de puntos de conexión se centran únicamente en las opciones que son relevantes para un método de cifrado integrado de dispositivos concreto, como FileVault o BitLocker. Este método permite a los administradores de seguridad administrar fácilmente las opciones de cifrado de disco sin tener que desplazarse por numerosas opciones que no tienen nada que ver.

- [Firewall](../protect/endpoint-security-firewall-policy.md): use la directiva de firewall de seguridad de puntos de conexión de Intune para configurar un firewall integrado para los dispositivos que ejecutan macOS y Windows 10. 

- [Detección de puntos de conexión y respuesta](../protect/endpoint-security-edr-policy.md): si integra ATP de Microsoft Defender con Intune, use las directivas de seguridad de puntos de conexión para la detección de puntos de conexión y respuesta (EDR) a fin de administrar la configuración de EDR e incorporar dispositivos a ATP de Microsoft Defender.

- [Reducción de la superficie expuesta a ataques](../protect/endpoint-security-asr-policy.md): si hace uso del antivirus de defender en los dispositivos Windows 10, use las directivas de seguridad de puntos de conexión de Intune para reducir la superficie de ataque y administrar esas opciones de los dispositivos.

- [Protección de cuentas](../protect/endpoint-security-account-protection-policy.md): las directivas de protección de cuentas ayudan a proteger la identidad y las cuentas de los usuarios. La directiva de protección de cuentas se centra en las opciones de Windows Hello y Credential Guard, que forma parte de la administración de identidades y del acceso de Windows.

Las siguientes secciones se aplican a todas las directivas de seguridad de puntos de conexión.

## <a name="create-an-endpoint-security-policy"></a>Creación de una directiva de seguridad de puntos de conexión

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Seleccione **Seguridad de los puntos de conexión**, seleccione el tipo de directiva que quiera configurar y, después, seleccione **Crear directiva**. Elija de entre los tipos de directiva siguientes:
   - Antivirus
   - Cifrado de discos
   - Firewall
   - Detección de puntos de conexión y respuesta
   - Reducción de la superficie expuesta a ataques
   - Protección de cuentas

3. Escriba las propiedades siguientes:
   - **Plataforma**: elija la plataforma para la que va a crear la directiva. Las opciones disponibles dependen del tipo de directiva seleccionado:
     - macOS
     - Windows 10 y versiones posteriores
   - **Perfil**: elija de entre los perfiles disponibles según la plataforma que haya seleccionado. Para obtener más información sobre los perfiles, vea la sección dedicada de este artículo correspondiente al tipo de directiva escogido.

4. Seleccione **Crear**.

5. En la página **Datos básicos**, escriba un nombre y una descripción para el perfil y, después, elija **Siguiente**.

6. En la página **Opciones de configuración**, expanda cada grupo de opciones y configure aquellas que quiera administrar con este perfil.

   Cuando haya finalizado la configuración, seleccione **Siguiente**.

7. En la página **Etiquetas de ámbito**, seleccione **Seleccionar etiquetas de ámbito** para abrir el panel *Seleccionar etiquetas* y asignar etiquetas de ámbito al perfil.
  
   Seleccione **Siguiente** para continuar.

8. En la página **Asignaciones**, seleccione los grupos que recibirán este perfil. Para obtener más información sobre la asignación de perfiles, vea [Asignación de perfiles de usuario y dispositivo](../configuration/device-profile-assign.md).

   Seleccione **Siguiente**.

9. Cuando haya terminado, elija **Crear** en la página **Revisar y crear**. El nuevo perfil se muestra en la lista cuando se selecciona el tipo de directiva del perfil creado.

## <a name="duplicate-a-policy"></a>Duplicación de una directiva

Las directivas de seguridad de puntos de conexión admiten la duplicación, esto es, que se cree una copia de la directiva original. Un escenario en el que la duplicación de una directiva resulta útil es cuando es necesario asignar directivas similares a grupos distintos, pero no se quiere volver a crear la directiva completa manualmente. En vez de ello, se puede duplicar la directiva original y, después, introducir solo los cambios que la nueva directiva requiera. Solo se puede cambiar una opción específica y el grupo al que la directiva está asignada.

Al crear un duplicado, se le asigna un nuevo nombre a la copia. La copia se realiza con las mismas opciones de configuración y etiquetas de ámbito que la original, pero no tiene ninguna asignación. Habrá que editar la nueva directiva posteriormente para crear asignaciones.  

Los siguientes tipos de directivas admiten duplicaciones:

- Antivirus
- Cifrado de discos
- Firewall
- Detección de puntos de conexión y respuesta
- Reducción de la superficie expuesta a ataques
- Protección de cuentas

Después de crear la directiva, revísela y edítela para realizar cambios en su configuración.

### <a name="to-duplicate-a-policy"></a>Para duplicar una directiva

1. Inicie sesión en el [Centro de administración del Administrador de puntos de conexión de Microsoft](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Seleccione la directiva que quiera copiar. Después, seleccione **Duplicar**, o bien seleccione los puntos suspensivos ( **...** ) que hay a la derecha de la directiva y, tras ello, **Duplicar**.
3. Proporcione un **Nuevo nombre** a la directiva y seleccione **Guardar**.

### <a name="to-edit-a-policy"></a>Para editar una directiva

1. Seleccione la nueva directiva y, luego, **Propiedades**.
2. Seleccione Configuración para expandir una lista de las opciones de configuración de la directiva. Las opciones no se pueden modificar desde esta vista, pero sí se puede revisar cómo están configuradas.
3. Para modificar la directiva, seleccione **Editar** en cada categoría en la que quiera hacer un cambio:
   - Aspectos básicos
   - Assignments
   - Etiquetas de ámbito
   - Opciones de configuración
4. Una vez realizados los cambios, seleccione **Guardar** para guardar las modificaciones.  Las modificaciones realizadas en una categoría se deben guardar para poder especificar modificaciones en categorías adicionales.

## <a name="manage-conflicts"></a>Administración de conflictos

Muchas de las opciones de configuración de los dispositivos que se pueden administrar con directivas de seguridad de puntos de conexión (directivas de seguridad) se pueden administrar a través de otros tipos de directivas en Intune, a saber, por medio de la *configuración de dispositivos* y de *líneas base de seguridad*. Dado que una opción se puede administrar con varios tipos de directivas diferentes o varias instancias del mismo tipo de directiva, debemos estar preparados para saber identificar y resolver posibles conflictos de directivas en caso de que un dispositivo no se adhiera a las configuraciones según lo previsto.

- Las líneas base de seguridad pueden establecer un valor no predeterminado en una configuración para que cumpla con la configuración recomendada que esa línea base aborda.
- Otros tipos de directivas, incluidas las directivas de seguridad de puntos de conexión, establecen un valor *No configurado* de forma predeterminada. Estos otros tipos de directivas requieren que se configuren opciones expresamente en la directiva.

Independientemente del método de directiva empleado, la administración de una misma opción en el mismo dispositivo a través de varios tipos de directivas, o a través de varias instancias del mismo tipo de directiva, puede provocar conflictos que deben evitarse.

La información de los vínculos siguientes puede servir para identificar y resolver conflictos:

- [Solución de problemas de directivas y perfiles en Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Supervisión de las líneas de base de seguridad](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>Pasos siguientes

[Administración de la seguridad de puntos de conexión en Intune](../protect/endpoint-security.md)
