---
title: Establecer la entidad de administración de dispositivos móviles
titleSuffix: Microsoft Intune
description: Establezca la entidad de administración de dispositivos móviles en Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/16/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 8deff871-5dff-4767-9484-647428998d82
ms.reviewer: damionw
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 676e7a4db54558eaea87ad2fa8efbe8af546f035
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996578"
---
# <a name="set-the-mobile-device-management-authority"></a>Establecer la entidad de administración de dispositivos móviles

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

La configuración de la entidad de administración de dispositivos móviles (MDM) determina cómo se administran los dispositivos. Como administrador de TI, debe establecer una entidad de MDM antes de que los usuarios puedan inscribir dispositivos para la administración.

Las configuraciones posibles son:

- **Intune independiente**: administración solo en la nube, que se configura mediante el portal de Azure. Incluye el conjunto completo de funcionalidades que ofrece Intune. [Establecer la entidad de MDM en la consola de Intune](#set-mdm-authority-to-intune).

- **Administración conjunta de Intune**: integración de la solución de nube de Intune con Configuration Manager para dispositivos Windows 10. Intune se configura mediante la consola de Configuration Manager. [Configuración de la inscripción automática de dispositivos en Intune](/configmgr/comanage/tutorial-co-manage-clients#configure-auto-enrollment-of-devices-to-intune). 

- **Basic Mobility and Security for Microsoft 365** (Movilidad y seguridad básicas para Microsoft 365): si tiene esta configuración activada, verá la entidad de MDM establecida en "Office 365". Si quiere empezar a usar Intune, deberá adquirir licencias de Intune.

- **[Coexistencia](#coexistence) de Basic Mobility and Security for Microsoft 365** (Movilidad y seguridad básicas para Microsoft 365): puede agregar Intune a su inquilino si ya usa Basic Mobility and Security for Microsoft 365 y establecer la entidad de administración en Intune o en Basic Mobility and Security for Microsoft 365 para que cada usuario indique qué servicio se usará para administrar sus dispositivos inscritos en MDM. La entidad de administración del usuario se define en función de la licencia asignada al usuario: Si el usuario tiene solo una licencia básica o estándar de Microsoft 365, los dispositivos se administrarán mediante Basic Mobility and Security for Microsoft 365. Si el usuario tiene una licencia de Intune, los dispositivos se administrarán mediante Intune. Si agrega una licencia de Intune a un usuario administrado previamente por Basic Mobility and Security for Microsoft 365, sus dispositivos se cambiarán a la administración de Intune. Asegúrese de tener las configuraciones de Intune asignadas a los usuarios para reemplazar Basic Mobility and Security for Microsoft 365 antes de cambiar los usuarios a Intune; de lo contrario, sus dispositivos perderán la configuración de Basic Mobility and Security for Microsoft 365 y no recibirán ningún reemplazo de Intune.

## <a name="set-mdm-authority-to-intune"></a>Establecimiento de la entidad de MDM en Intune

En el caso de los inquilinos que usan la versión de servicio 1911 y versiones posteriores, la entidad de MDM se establece automáticamente en Intune.

En el caso de los inquilinos de versión de servicio anterior a 1911, haga lo siguiente si aún no ha establecido la entidad de MDM.

1. En el [Centro de administración de Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431), seleccione el banner naranja para abrir la configuración **Entidad de administración de dispositivos móviles**. El banner naranja aparece únicamente si aún no ha establecido la entidad de MDM.
2. En **Entidad de administración de dispositivos móviles**, elija la entidad de MDM entre las opciones siguientes:
  - **Entidad de MDM de Intune**
  - **Ninguno**

  ![Captura de pantalla de la sección para configurar Intune como la entidad de administración de dispositivos móviles](./media/mdm-authority-set/set-mdm-auth.png)

  Un mensaje indica que ha configurado correctamente su entidad de MDM en Intune.

### <a name="workflow-of-intune-administration-ui"></a>Flujo de trabajo de UI de administración de Intune
Cuando se habilita la administración de dispositivos Android o Apple, Intune envía información del usuario y dispositivo para integrar con estos servicios de terceros a fin de administrar sus dispositivos correspondientes.

Los escenarios que agregan un consentimiento para compartir datos se incluyen cuando:
- Se habilitan perfiles de trabajo Android.
- Se habilitan y cargan certificados push MDM de Apple.
- Se habilita cualquiera de los servicios de Apple, por ejemplo, el Programa de inscripción de dispositivos, School Manager o el Programa de Compras por Volumen.

En cada caso, el consentimiento está estrictamente relacionado con la ejecución de un servicio de administración de dispositivos móviles. Por ejemplo, confirmar que un administrador de TI ha autorizado a dispositivos Google o Apple para que se inscriban. La documentación para tratar qué información se comparte cuando los nuevos flujos de trabajo se publican está disponible en las siguientes ubicaciones:
- [Datos que Intune manda a Google](https://aka.ms/Data-intune-sends-to-google)
- [Data que Intune manda a Apple](https://aka.ms/data-intune-sends-to-apple)

## <a name="key-considerations"></a>Principales consideraciones
Después de cambiar a la nueva entidad de MDM, habrá probablemente un tiempo de transición (hasta ocho horas) antes de que el dispositivo se compruebe y se sincronice con el servicio. Es necesario que configure los valores de la nueva entidad de MDM para asegurarse de que los dispositivos inscritos seguirán administrados y protegidos después del cambio. 
- Los dispositivos deben conectarse al servicio después del cambio para que la configuración de la nueva entidad de MDM (Intune independiente) reemplace la configuración existente en el dispositivo.
- Después de cambiar la entidad de MDM, algunas de las opciones básicas (como los perfiles) de la entidad de MDM anterior permanecerán en el dispositivo durante siete días o hasta que el dispositivo se conecte al servicio por primera vez. Se recomienda que configure aplicaciones y valores (directivas, perfiles, aplicaciones, etc.) en la nueva entidad de MDM tan pronto como sea posible y que implemente la configuración en los grupos de usuarios que contienen usuarios con dispositivos ya inscritos. En cuanto el dispositivo se conecte con el servicio tras el cambio en la entidad de MDM, recibirá la nueva configuración desde la nueva entidad de MDM, evitando así los tiempos de inactividad en administración y protección.
- Los dispositivos sin usuarios asociados (normalmente cuando se tiene el Programa de inscripción de dispositivos iOS/iPadOS o escenarios de inscripción masiva) no se migran a la nueva entidad de MDM. Para esos dispositivos, debe llamar al soporte técnico para solicitar ayuda para trasladarlos a la nueva entidad de MDM.

## <a name="coexistence"></a>Coexistence

Habilitar la coexistencia le permite usar Intune en un nuevo conjunto de usuarios y, al mismo tiempo, seguir usando la movilidad y seguridad básicas de los usuarios existentes. Puede controlar qué dispositivos administra Intune a través del usuario. Si a un usuario se le asigna una licencia de Intune o este usa la administración conjunta de Intune con Configuration Manager, Intune administrará todos sus dispositivos inscritos. De lo contrario, el usuario se administra mediante la movilidad y seguridad básicas.

Para habilitar la coexistencia, se deben realizar principalmente tres pasos:
1. Preparación
2. Adición de la entidad de MDM de Intune
3. Migración de usuarios y dispositivos (opcional).

### <a name="preparation"></a>Preparación

Antes de habilitar la coexistencia con la movilidad y seguridad básicas, tenga en cuenta los siguientes puntos:
- Asegúrese de que dispone de suficientes [licencias de Intune](licenses.md) para los usuarios que quiere administrar mediante Intune.
- Revise qué usuarios tienen asignadas licencias de Intune. Después de habilitar la coexistencia, todos los usuarios a los que ya se les haya asignado una licencia de Intune, tendrán sus dispositivos cambiados a Intune. Para evitar cambios de dispositivo inesperados, se recomienda no asignar ninguna licencia de Intune hasta que se haya habilitado la coexistencia.
- Cree e implemente directivas de Intune para reemplazar las directivas de seguridad de dispositivos que se implementaron originalmente mediante el Portal de seguridad y cumplimiento de Office 365. Este reemplazo debe realizarse para los usuarios que pasan de la movilidad y seguridad básicas a Intune. Si no hay ninguna directiva de Intune asignada a esos usuarios, la habilitación de la coexistencia podría hacer que se perdiera la configuración de la movilidad y seguridad básicas. Esta configuración se perderá sin que se reemplace, como es el caso de los perfiles de correo electrónico administrados. Incluso al reemplazar las directivas de seguridad de dispositivos por directivas de Intune, es posible que se pida a los usuarios que vuelvan a autenticar sus perfiles de correo electrónico después de que el dispositivo se mueva a la administración de Intune.

### <a name="add-intune-mdm-authority"></a>Adición de la entidad de MDM de Intune

Para habilitar la coexistencia, debe agregar Intune como entidad de MDM a su entorno:

1. Inicie sesión en endpoint.microsoft.com con derechos de administrador global de Azure AD o del servicio Intune.
2. Vaya a **Dispositivos**.
3. Se muestra la hoja **Agregar entidad de MDM**.
4. Para cambiar la entidad de MDM de *Office 365* a *Intune* y habilitar la coexistencia, seleccione **Entidad de Intune MDM** > **Agregar**.
  ![Captura de pantalla de la pantalla Agregar entidad de MDM](./media/mdm-authority-set/add-mdm-authority.png)

### <a name="migrate-users-and-devices-optional"></a>Migración de usuarios y dispositivos (opcional)

Una vez habilitada la entidad de MDM de Intune, la coexistencia se activa y puede empezar a administrar usuarios mediante Intune. También, si quiere mover los dispositivos administrados anteriormente mediante la movilidad y seguridad básicas para que los administre Intune, asigne a esos usuarios una licencia de Intune. Los dispositivos de los usuarios cambiarán a Intune en la siguiente sincronización de MDM. La configuración que se aplica a estos dispositivos mediante la movilidad y seguridad básicas dejará de aplicarse y se quitará de los dispositivos.

## <a name="mobile-device-cleanup-after-mdm-certificate-expiration"></a>Limpieza de dispositivos móviles tras la expiración del certificado MDM

El certificado MDM se renueva automáticamente cuando los dispositivos móviles se comunican con el servicio de Intune. Si se borran los dispositivos móviles o estos no pueden comunicarse con el servicio de Intune durante un tiempo, el certificado de MDM no se renovará. El dispositivo se quita del portal de Azure 180 días después de que expire el certificado MDM.

## <a name="remove-mdm-authority"></a>Eliminación de la entidad de MDM

No se puede cambiar la entidad de MDM a Desconocido. El servicio usa la entidad de MDM para determinar a qué portal informan los dispositivos inscritos (Microsoft Intune o Basic Mobility and Security for Microsoft 365).

## <a name="what-to-expect-after-changing-the-mdm-authority"></a>Qué esperar después de cambiar la entidad de MDM

- Cuando el servicio de Intune detecta que ha cambiado la entidad de MDM de un inquilino, envía un mensaje de notificación a todos los dispositivos inscritos para que inicien el proceso de comprobación y se sincronicen en el servicio (esta notificación no forma parte de la comprobación programada regularmente). Por lo tanto, una vez que cambie la entidad de MDM para el inquilino de Intune independiente, todos los dispositivos que estén encendidos y en línea se conectarán en el servicio, recibirán la nueva entidad de MDM y serán administrados por esta. No hay ninguna interrupción en el proceso de administración y protección de estos dispositivos.
- Incluso para los dispositivos que están encendidos y en línea durante el cambio en la entidad de MDM (o poco tiempo después), pasarán hasta ocho horas (según el tiempo de la siguiente comprobación periódica programada) hasta que los dispositivos se registren en el servicio bajo la nueva entidad de MDM.  

 > [!IMPORTANT]  
 > Entre el momento en que cambie la entidad MDM y se cargue el certificado de APNs renovado en la nueva entidad, se producirá un error en las inscripciones de nuevos dispositivos y las comprobaciones de dispositivos iOS/iPadOS. Por lo tanto, es importante revisar y cargar el certificado de Apple Push Notification Service en la nueva entidad tan pronto como sea posible después del cambio de entidad de MDM.

- Los usuarios pueden cambiar rápidamente a la nueva entidad de MDM iniciando manualmente una comprobación desde el dispositivo en el servicio. Los usuarios pueden realizar este cambio con facilidad mediante la aplicación del Portal de empresa y el inicio de una comprobación de cumplimiento del dispositivo.
- Para validar que todo funciona correctamente después de que los dispositivos se hayan comprobado y sincronizado con el servicio tras el cambio de entidad de MDM, busque los dispositivos en la entidad de MDM.
- Existe un período transitorio entre el momento en que un dispositivo está sin conexión durante el cambio de entidad de MDM y el momento en que se comprueba la idoneidad de ese dispositivo para su registro en el servicio. Para garantizar que el dispositivo permanece protegido y funcional durante este período transitorio, los siguientes perfiles permanecen en el dispositivo hasta siete días (o hasta que el dispositivo se conecte con la nueva entidad de MDM y reciba la nueva configuración que sobrescribirá la actual):
   - Perfil de correo electrónico
   - Perfil de VPN
   - Perfil de certificado
   - Perfil de Wi-Fi
   - Perfiles de configuración
- Después de cambiar a la nueva entidad de MDM, los datos de cumplimiento de la consola de administración de Microsoft Intune pueden tardar hasta una semana en informar con exactitud. Pero los estados de cumplimiento de Azure Active Directory y en el dispositivo serán precisos para que el dispositivo siga estando protegido.
- Compruebe que la nueva configuración destinada a sobrescribir la configuración actual tiene el mismo nombre que la anterior para asegurarse de que efectivamente se sobrescribe. En caso contrario, los dispositivos podrían terminar con directivas y perfiles redundantes.  

 > [!TIP]  
 > Es recomendable que cree todas las configuraciones y parámetros de administración, así como las implementaciones, poco después de que se haya completado el cambio a la entidad de MDM. De esta manera se asegurará de que los dispositivos están protegidos y se administran de manera activa durante el período transitorio.

- Después de cambiar la entidad de MDM, siga estos pasos para validar que los nuevos dispositivos se inscriben correctamente en la nueva entidad:  
 - Inscripción de un dispositivo nuevo
 - Asegúrese de que el dispositivo recién inscrito aparece en la entidad de MDM.
 - Realice una acción, como el bloqueo remoto, desde la consola de administración en el dispositivo. Si se completa correctamente, el dispositivo se está administrando mediante la nueva entidad de MDM.
- Si tiene problemas con dispositivos concretos, puede anular la inscripción de esos dispositivos y realizarla de nuevo para que se conecten a la nueva entidad y se administren lo antes posible.

## <a name="next-steps"></a>Pasos siguientes

Con la entidad de MDM configurada, puede empezar a [inscribir dispositivos](../enrollment/device-enrollment.md).