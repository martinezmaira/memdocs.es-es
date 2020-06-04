---
title: Administración de la seguridad de puntos de conexión en Microsoft Intune | Microsoft Docs
description: Obtenga información sobre cómo los administradores de seguridad pueden usar el nodo Seguridad de los puntos de conexión para administrar la seguridad de los dispositivos y corregir problemas de dispositivos en Microsoft Endpoint Manager.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 99ac1e069386c69011543ac40878dd62a0d50527
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990825"
---
# <a name="manage-endpoint-security-in-microsoft-intune"></a>Administración de la seguridad de puntos de conexión en Microsoft Intune

Como administrador de seguridad, use el nodo *Seguridad de los puntos de conexión* de Intune para configurar la seguridad de los dispositivos y administrar las tareas de seguridad de los dispositivos cuando estos estén en riesgo. Las directivas de seguridad de los puntos de conexión están concebidas para ayudarle a centrarse en la seguridad de los dispositivos y mitigar riesgos. Las tareas que están disponibles le servirán para identificar los dispositivos que estén en riesgo, para corregir tales dispositivos y para restaurarlos a un estado compatible o más seguro.

En el nodo Seguridad de los puntos de conexión se agrupan las herramientas disponibles en Intune que usará para mantener los dispositivos seguros:

- **Revisión del estado de todos los dispositivos administrados**. Use la vista [Todos los dispositivos](#manage-devices), donde se puede ver el cumplimiento del dispositivo desde un nivel alto y, tras ello, obtener detalles de dispositivos específicos con el fin de saber qué directivas de cumplimiento no se están cumpliendo y poder resolver la situación.

- **Implementación de líneas base de seguridad que establecen configuraciones de seguridad de procedimientos recomendados de dispositivos**. Intune incluye [líneas base de seguridad](#manage-security-baselines) relativas a dispositivos Windows y una lista cada vez mayor de aplicaciones, como Advanced Threat Protection de Microsoft Defender (ATP de Defender) y Microsoft Edge. Las líneas base de seguridad son grupos preconfigurados de configuraciones de Windows que le ayudan a aplicar un grupo conocido de configuraciones y valores predeterminados que los equipos de seguridad pertinentes recomiendan.

- **Administración de configuraciones de seguridad en los dispositivos a través de directivas de enfoque estricto**.  Cada [directiva de seguridad de los puntos de conexión](#use-policies-to-manage-device-security) se centra en aspectos de seguridad del dispositivo, como el antivirus, el cifrado de discos, los firewalls o las diversas áreas disponibles a través de la integración con ATP de Defender.

- **Establecimiento de los requisitos de dispositivo y de usuario a través de la directiva de cumplimiento**. Con las [directivas de cumplimiento](../protect/device-compliance-get-started.md) se establecen las reglas que los dispositivos y los usuarios deben cumplir para que se consideren como compatibles. Estas reglas pueden incluir versiones del sistema operativo, requisitos de contraseña, niveles de amenaza de dispositivo, etc.

  Cuando Intune se integra con [directivas de acceso condicional](#configure-conditional-access) de Azure Active Directory (Azure AD) para aplicar directivas de conformidad, se puede dar acceso a los recursos corporativos tanto a dispositivos administrados como a los que aún están sin administrar.

- **Integración de Intune con el equipo de ATP de Microsoft Defender**. La [integración con ATP de Defender](#set-up-integration-with-defender-atp) le permite tener acceso a [tareas de seguridad](#review-security-tasks-from-defender-atp). Las tareas de seguridad establecen una estrecha relación entre ATP de Defender e Intune, lo que permitirá a los equipos de seguridad identificar los dispositivos que están en riesgo y proporcionar pasos de corrección detallados a los administradores de Intune para que puedan ponerlos en práctica.

En las siguientes secciones de este artículo se describen las diferentes tareas que se pueden realizar desde el nodo Seguridad de los puntos de conexión del centro de administración, así como los permisos de control de acceso basado en rol (RBAC) necesarios para usarlas.

## <a name="manage-devices"></a>Administrar los dispositivos

El nodo Seguridad de los puntos de conexión incluye la vista *Todos los dispositivos*, donde puede ver una lista de todos los dispositivos de Azure AD que hay disponibles en Microsoft Endpoint Manager.

En esta vista, se pueden seleccionar dispositivos para obtener más detalles sobre ellos, como las directivas que no están cumpliendo. Esta vista también puede servir para corregir problemas de un dispositivo, como reiniciar un dispositivo, iniciar un examen de malware o rotar las claves BitLocker de un dispositivo Windows 10.

Para más información, vea [Administración de dispositivos con seguridad de puntos de conexión en Microsoft Intune](../protect/endpoint-security-manage-devices.md).

## <a name="manage-security-baselines"></a>Administración de líneas base de seguridad

Las líneas base de seguridad de Intune son grupos de configuración predefinidos que son recomendaciones de procedimientos recomendados realizadas por los equipos de seguridad de Microsoft a cargo del producto correspondiente. Intune admite líneas base de seguridad de configuraciones de dispositivos Windows 10, de Microsoft Edge, de Microsoft Defender Advanced Threat Protection y otros muchos.

Estas líneas base de seguridad se pueden usar para implementar rápidamente una configuración de *procedimiento recomendado* de opciones de aplicación y de dispositivo para proteger a los usuarios y los dispositivos. Se admiten líneas base de seguridad en dispositivos que ejecuten Windows 10 versión 1809 y versiones posteriores.

Para más información, vea [Uso de líneas base de seguridad para configurar dispositivos Windows 10 en Intune](../protect/security-baselines.md).

Las líneas base de seguridad son uno de los diversos métodos de Intune para configurar opciones en los dispositivos. Al administrar estas opciones, es importante saber qué otros métodos hay en uso en el entorno con los que se podrían configurar los dispositivos para evitar conflictos. Vea [Cómo evitar conflictos de directivas](#avoid-policy-conflicts) más adelante en este artículo.

## <a name="review-security-tasks-from-defender-atp"></a>Revisión de tareas de seguridad de ATP de Defender

Cuando Intune se integra con Advanced Threat Protection de Microsoft Defender (ATP de Defender), se pueden revisar las *tareas de seguridad* de Intune que identifiquen los dispositivos en riesgo y proporcionar los pasos necesarios para mitigar este riesgo. Tras ello, las tareas se pueden usar para notificar a ATP de Defender cuando estos riesgos se hayan mitigado correctamente.

- El equipo de ATP de Defender determina qué dispositivos están en riesgo y transmite esa información al equipo de Intune como una tarea de seguridad. Con unos pocos clics, se crea una tarea de seguridad en Intune que identifica los dispositivos en riesgo y la vulnerabilidad, y se proporcionan instrucciones sobre cómo mitigar este riesgo.

- Los administradores de Intune revisan las tareas de seguridad y realizan las medidas oportunas en Intune para corregir esas tareas. Una vez solucionado el problema, establecen la tarea como completa, estado que se comunica de vuelta al equipo de ATP de Defender.

Gracias a las tareas de seguridad, los equipos permanecen sincronizados en cuanto a qué dispositivos están en riesgo, y cómo y cuándo esos riesgos se corrigen.

Para más información sobre cómo usar las tareas de seguridad, vea [Uso de Intune para corregir las vulnerabilidades que identifica ATP de Microsoft Defender](../protect/atp-manage-vulnerabilities.md).

## <a name="use-policies-to-manage-device-security"></a>Uso de directivas para administrar la seguridad de los dispositivos

Como administrador de seguridad, use las directivas de seguridad que se encuentran en *Administrar*, en el nodo Seguridad de los puntos de conexión. Con estas directivas, la seguridad de los dispositivos se puede configurar sin el engorro de tener que desplazarse por todas las opciones de los perfiles de configuración y líneas base de seguridad de los dispositivos.

![Administrar directivas](./media/endpoint-security/endpoint-security-policies.png)

Para más información sobre cómo usar estas directivas de seguridad, vea [Administración de la seguridad de los dispositivos con directivas de seguridad de puntos de conexión](../protect/endpoint-security-policy.md).

Las directivas de seguridad de los puntos de conexión son uno de los diversos métodos de Intune para configurar opciones en los dispositivos. Al administrar estas opciones, es importante saber qué otros métodos hay en uso en el entorno con los que se podrían configurar los dispositivos para evitar conflictos. Vea [Cómo evitar conflictos de directivas](#avoid-policy-conflicts) más adelante en este artículo.

En *Administrar* también verá las directivas *Conformidad de dispositivos*  y *Acceso condicional*. Estos tipos de directivas no son directivas de seguridad centradas en la configuración de puntos de conexión, sino herramientas importantes para la administración de dispositivos y el acceso a los recursos corporativos.

## <a name="use-device-compliance-policy"></a>Uso de la directiva de conformidad de dispositivos

Use la directiva de conformidad de dispositivos para establecer las condiciones en las que los dispositivos y usuarios pueden acceder a la red y a los recursos de la empresa.

La [configuración de conformidad disponible](../protect/device-compliance-get-started.md#next-steps) depende de la plataforma que se use, pero las reglas de directiva comunes son estas:

- Requerir que los dispositivos ejecuten una versión de sistema operativo mínima o específica
- Establecer requisitos de contraseña
- Especificar un nivel de amenaza de dispositivo máximo permitido, según lo determine ATP de Defender o cualquier otro asociado de Mobile Threat Defense

Aparte de las reglas de directiva, las directivas de conformidad contemplan lo siguiente:

- Las [ubicaciones](../protect/use-network-locations.md) definidas en Intune. Cuando se usan ubicaciones con una directiva de conformidad, esta puede asegurarse de que los dispositivos están conectados a una red de trabajo para que sean conformes.
- Las [acciones de no cumplimiento](../protect/actions-for-noncompliance.md). Estas acciones son una secuencia de acciones ordenadas en el tiempo que se aplican a los dispositivos no conformes. Entre las acciones están enviar correos electrónicos o notificaciones para avisar a los usuarios del dispositivo de que no es conforme, bloquear dispositivos de forma remota o, incluso, retirar dispositivos no conformes y eliminar los datos de la empresa que pueda haber en él.

Cuando Intune se integra con [directivas de acceso condicional](#configure-conditional-access) de Azure AD para aplicar directivas de conformidad, el acceso condicional puede usar los datos de conformidad para dar acceso a los recursos corporativos tanto a dispositivos administrados como no administrados.

Para más información, vea [Establecimiento de reglas en los dispositivos para permitir el acceso a recursos de su organización con Intune](../protect/device-compliance-get-started.md).

Las directivas de conformidad de los dispositivos son uno de los diversos métodos de Intune para configurar opciones en los dispositivos. Al administrar estas opciones, es importante saber qué otros métodos hay en uso en el entorno con los que se podrían configurar los dispositivos para evitar conflictos. Vea [Cómo evitar conflictos de directivas](#avoid-policy-conflicts) más adelante en este artículo.

## <a name="configure-conditional-access"></a>Configuración de acceso condicional

Se pueden usar directivas de acceso condicional de Azure Active Directory (Azure AD) con Intune para proteger los dispositivos y los recursos corporativos.

Intune pasa los resultados de las directivas de conformidad de los dispositivos a Azure AD, que seguidamente usa directivas de acceso condicional para establecer qué dispositivos y aplicaciones pueden acceder a los recursos corporativos. Las directivas de acceso condicional pueden ayudar a proporcionar acceso a dispositivos que no están administrados por Intune. Se pueden usar incluso los detalles de conformidad de los [asociados de Mobile Threat Defense](../protect/mobile-threat-defense.md) que haya integrados con Intune.

Aquí se describen dos métodos habituales de uso del acceso condicional con Intune:

- **Acceso condicional basado en dispositivos**, para asegurarse de que solo los dispositivos administrados y conformes pueden acceder los recursos de la red.
- **Acceso condicional basado en la aplicación**, que usa directivas de protección de aplicaciones para administrar el acceso a los recursos de red por parte de los usuarios en dispositivos que no se administran con Intune.

Para más información sobre cómo usar el acceso condicional con Intune, vea [Más información sobre el acceso condicional e Intune](../protect/conditional-access.md).

## <a name="set-up-integration-with-defender-atp"></a>Configuración de la integración con ATP de Defender

Cuando Advanced Threat Protection de Microsoft Defender (ATP de Defender) se integra con Intune, se mejora la capacidad de identificar riesgos y responder a ellos.

Aunque Intune se puede integrar con varios [asociados de Mobile Threat Defense](../protect/mobile-threat-defense.md), cuando se usa ATP de Defender, se logra una estrecha integración entre ATP de Defender e Intune, con acceso a opciones de protección de dispositivos eficaces, a saber:

- Tareas de seguridad: comunicación fluida entre los administradores de ATP y de Intune para saber qué dispositivos hay en riesgo, cómo corregirlos y tener una confirmación cuando esos riesgos se hayan mitigado.
- Incorporación sin fisuras de ATP de Defender en los clientes.
- Uso de señales de riesgo de dispositivo de ATP en las directivas de conformidad de Intune.
- Acceso a capacidades de *protección contra alteraciones*.

 Para más información sobre cómo usar ATP de Defender con Intune, vea [Aplicación del cumplimiento de ATP de Microsoft Defender con acceso condicional en Intune](../protect/advanced-threat-protection.md).

## <a name="role-based-access-control-requirements"></a>Requisitos de control de acceso basado en rol

Para administrar las tareas del nodo Seguridad de los puntos de conexión del centro de administración de Microsoft Endpoint Manager, una cuenta debe reunir las siguientes condiciones:

- Tener asignada una licencia de Intune.
- Tener los permisos de control de acceso basado en rol (RBAC) equivalentes a los permisos proporcionados por el rol de Intune integrado **Administrador de seguridad de puntos de conexión**. El rol *Administrador de seguridad de puntos de conexión* da acceso al centro de administración de Microsoft Endpoint Manager. Este rol lo pueden usar aquellas personas que administren características de seguridad y de conformidad, como las líneas base de seguridad, la conformidad de dispositivos, el acceso condicional y ATP de Microsoft Defender.

Para más información, vea [Control de acceso basado en rol (RBAC) con Microsoft Intune](../fundamentals/role-based-access-control.md).

### <a name="permissions-granted-by-the-endpoint-security-manager-role"></a>Permisos concedidos por el rol *Administrador de seguridad de puntos de conexión*

Para ver la siguiente lista de permisos en el centro de administración de Microsoft Endpoint Manager, vaya a **Administración de inquilinos** > **Roles** > **Todos los roles** y seleccione **Endpoint Security Manager** (Administrador de seguridad de puntos de conexión) > **Propiedades**.

**Permisos:**

- **Android for work**
  - Lectura
- **Datos de auditoría**
  - Lectura
- **Identificadores de dispositivo corporativos**
  - Lectura
- **Directivas de cumplimiento de dispositivos**
  - Asignar
  - Crear
  - Eliminar
  - Lectura
  - Actualizar
  - Ver informes
- **Configuraciones de dispositivo**
  - Lectura
- **Administradores de inscripción de dispositivos**
  - Lectura
- **Informes de Endpoint Protection**
  - Lectura
- **Programas de inscripción**
  - Leer dispositivo
  - Leer perfil
  - Leer token
- **Almacenamiento de datos de Intune**
  - Lectura
- **Aplicaciones administradas**
  - Lectura
- **Dispositivos administrados**
  - Eliminar
  - Lectura
  - Establecer el usuario principal
  - Actualizar
- **Aplicaciones móviles**
  - Lectura
- **Organización**
  - Lectura
- **PolicySets**
  - Lectura
- **Asistencia remota**
  - Lectura
- **Tareas remotas**
  - Obtener la clave de FileVault
- **Roles**
  - Lectura
- **Líneas base de seguridad**
  - Asignar
  - Crear
  - Eliminar
  - Lectura
  - Actualizar
- **Tareas de seguridad**
  - Lectura
  - Actualizar
- **Gastos de telecomunicaciones**
  - Lectura
- **Términos y condiciones**
  - Lectura

## <a name="avoid-policy-conflicts"></a>Cómo evitar conflictos de directivas

Muchas de las opciones de los dispositivos que se pueden configurar se pueden administrar con diferentes características de Intune. Entre estas características se incluyen las siguientes:

- Directivas de seguridad de puntos de conexión
- Líneas base de seguridad
- Directivas de configuración de dispositivos
- Directivas de inscripción de Windows 10

Por ejemplo, las opciones que hay en las directivas de seguridad de los puntos de conexión es un subconjunto de las opciones que forman parte de los perfiles de *Endpoint Protection* y de *restricción de dispositivos* de la directiva de configuración de dispositivos, y que también se administran a través de diversas líneas base de seguridad.

Una forma de evitar conflictos consiste en no usar líneas base diferentes, instancias de la misma línea base o tipos e instancias de directivas distintos para administrar las mismas opciones de un mismo dispositivo. Esto requiere planear los métodos que se van a usar para implementar configuraciones en dispositivos diferentes. Cuando use varios métodos o varias instancias del mismo método para configurar la misma opción, asegúrese de que los distintos métodos acepten o no estén implementados en los mismos dispositivos.

Si surgen conflictos, puede usar las herramientas integradas de Intune para identificar y resolver el origen de esos conflictos. Para obtener más información, vea:

- [Solución de problemas de directivas y perfiles en Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Supervisión de las líneas de base de seguridad](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>Pasos siguientes

Configurar lo siguiente:

- [Líneas base de seguridad](../protect/security-baselines.md)
- [Directivas de cumplimiento](../protect/device-compliance-get-started.md)
- [Directivas de acceso condicional](#configure-conditional-access)
- [Integración con ATP de Defender](../protect/advanced-threat-protection.md)
