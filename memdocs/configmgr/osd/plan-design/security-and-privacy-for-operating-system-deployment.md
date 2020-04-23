---
title: Seguridad y privacidad para la implementación de sistema operativo
titleSuffix: Configuration Manager
description: Obtenga información sobre los procedimientos recomendados de seguridad y privacidad para la implementación de SO en Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 53256889b8bbd6a9608748a57de33b38be77cfd8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709333"
---
# <a name="security-and-privacy-for-os-deployment-in-configuration-manager"></a>Seguridad y privacidad para la implementación de SO en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Este artículo contiene información sobre seguridad y privacidad para la característica de implementación de SO en Configuration Manager.  



##  <a name="security-best-practices-for-os-deployment"></a><a name="bkmk_security"></a> Procedimientos recomendados de seguridad para la implementación de SO  

Siga las siguientes prácticas recomendadas de seguridad cuando implemente sistemas operativos con Configuration Manager:  


### <a name="implement-access-controls-to-protect-bootable-media"></a>Implemente controles de acceso para proteger el medio de arranque.

Cuando cree medios de arranque, asigne siempre una contraseña para ayudar a proteger el medio. Incluso con una contraseña, solo cifra los archivos que contienen información confidencial, y se pueden sobrescribir todos los archivos.  

Controle el acceso físico a los medios para impedir que un atacante use ataques criptográficos para obtener el certificado de autenticación del cliente.  

Para evitar que un cliente instale contenido o una directiva de cliente alterados, se aplica un algoritmo hash al contenido que debe usarse con la directiva original. Si se produce un error en el hash del contenido o no se puede comprobar que el contenido coincida con la directiva, el cliente no usará el medio de arranque. Solo se aplica hash al contenido. No se aplica hash a la directiva, pero se cifra y protege cuando se especifica una contraseña. Este comportamiento dificulta que un atacante pueda modificar correctamente la directiva.  


### <a name="use-a-secure-location-when-you-create-media-for-os-images"></a>Uso de una ubicación segura al crear los medios para las imágenes de sistema operativo

Si los usuarios no autorizados tienen acceso a la ubicación, pueden manipular los archivos que cree. También pueden usar todo el espacio disponible en disco para que no se puedan crear medios.  


### <a name="protect-certificate-files"></a>Protección de los archivos de certificado 

Proteja los archivos de certificado (.pfx) con una contraseña segura. Si los almacena en la red, proteja el canal de red al importarlos a Configuration Manager.

Cuando requiera una contraseña para importar el certificado de autenticación de cliente que usa para los medios de arranque, esta configuración ayuda a proteger el certificado de un atacante.  

Use la firma SMB o IPsec entre la ubicación de red y el servidor de sitio para impedir que un atacante pueda manipular el archivo del certificado.  


### <a name="block-or-revoke-any-compromised-certificates"></a>Bloqueo o revocación de los certificados en peligro 

Si el certificado de cliente se ve comprometido, bloquéelo desde Configuration Manager. Si es un certificado PKI, revóquelo.  

Para implementar un sistema operativo mediante un medio de arranque y un arranque PXE, debe tener un certificado de autenticación de cliente con una clave privada. Si ese certificado se ve comprometido, bloquéelo en el nodo **Certificados** del área de trabajo **Administración** , en el nodo **Seguridad** .  


### <a name="secure-the-communication-channel-between-the-site-server-and-the-sms-provider"></a>Protección del canal de comunicación entre el servidor de sitio y el proveedor de SMS

Cuando el proveedor de SMS esté en una ubicación remota con respecto al servidor de sitio, proteja el canal de comunicación para proteger las imágenes de arranque.

Cuando se modifican las imágenes de arranque y el proveedor de SMS se ejecuta en un servidor que no sea el servidor de sitio, las imágenes de arranque son vulnerables a ataques. Proteja el canal de red entre estos equipos mediante la firma SMB o IPsec.  


### <a name="enable-distribution-points-for-pxe-client-communication-only-on-secure-network-segments"></a>Habilite puntos de distribución para la comunicación de cliente PXE solo en segmentos de red segura.

Cuando un cliente envía una solicitud de arranque PXE, no dispone de ninguna manera para asegurarse de que la solicitud es atendida por un punto de distribución habilitado para PXE válido. Este escenario supone los riesgos de seguridad siguientes:  

- Un punto de distribución no autorizado que responde a las solicitudes PXE podría proporcionar una imagen modificada a los clientes.  

- Un atacante podría lanzar un ataque de tipo "Man in the middle" contra el protocolo TFTP usado por PXE. Este ataque podría enviar código malintencionado con los archivos del sistema operativo. El atacante también podría crear un cliente no autorizado para enviar solicitudes TFTP directamente al punto de distribución.  

- Un atacante podría usar a un cliente malintencionado para lanzar un ataque de denegación de servicio contra el punto de distribución.  

Use la defensa en profundidad para proteger los segmentos de red donde los clientes acceden a los puntos de distribución habilitados para PXE.  

> [!WARNING]  
>  Debido a estos riesgos de seguridad, no habilite un punto de distribución para la comunicación PXE cuando se encuentre en una red que no sea de confianza, como una red perimetral.  


### <a name="configure-pxe-enabled-distribution-points-to-respond-to-pxe-requests-only-on-specified-network-interfaces"></a>Configure puntos de distribución habilitados para PXE para responder a solicitudes PXE solo en interfaces de red especificadas.  

Si permite que el punto de distribución responda a solicitudes PXE en todas las interfaces de red, esta configuración podría exponer el servicio PXE a redes que no son de confianza.  


### <a name="require-a-password-to-pxe-boot"></a>Solicite una contraseña para el arranque PXE.

Cuando requiera una contraseña para el arranque PXE, esta configuración agrega un nivel de seguridad adicional al proceso de arranque PXE. Esta configuración ayuda a evitar que clientes no autorizados se unan a la jerarquía de Configuration Manager.  


### <a name="restrict-content-in-os-images-used-for-pxe-boot-or-multicast"></a>Restricción del contenido en imágenes de sistema operativo que se usan para el arranque PXE o la multidifusión

No incluya aplicaciones de línea de negocio ni software que contenga datos confidenciales en una imagen que se vaya a usar para el arranque PXE o la multidifusión.  

Debido a los riesgos de seguridad inherentes relacionados con la multidifusión y el arranque PXE, reduzca los riesgos si un equipo no autorizado descarga la imagen de sistema operativo.  


### <a name="restrict-content-installed-by-task-sequence-variables"></a>Restricción del contenido instalado mediante variables de secuencia de tareas

No incluya aplicaciones de línea de negocio ni software que contenga datos confidenciales en paquetes de aplicaciones que se instalen mediante variables de secuencias de tareas.  

Al implementar software mediante variables de secuencias de tareas, se podría instalar en equipos y para usuarios que no estén autorizados para recibir ese software.  


### <a name="secure-the-network-channel-when-migrating-user-state"></a>Protección del canal de red durante la migración del estado de usuario

Al migrar el estado del usuario, proteja el canal de red entre el cliente y el punto de migración de estado mediante la firma SMB o IPsec.  

Después de la conexión inicial a través de HTTP, los datos de la migración del estado de usuario se transfieren mediante SMB. Si no protege el canal de red, un atacante puede leer y modificar estos datos.  


### <a name="use-the-latest-version-of-usmt"></a>Uso de la versión más reciente de USMT

Use la versión más reciente de la Herramienta de migración de estado de usuario (USMT) que admita Configuration Manager.  

La versión más reciente de USMT proporciona mejoras de seguridad y un mayor control al migrar los datos de estado de usuario.  


### <a name="manually-delete-folders-on-state-migration-points-when-you-decommission-them"></a>Eliminación manual de las carpetas en el punto de migración de estado cuando se retiren  

Cuando quita una carpeta del punto de migración de estado en la consola de Configuration Manager en las propiedades del punto de migración de estado, el sitio no elimina la carpeta física. Para impedir la divulgación de los datos de migración de estado de usuario, quite manualmente el recurso compartido de red y elimine la carpeta.  


### <a name="dont-configure-the-deletion-policy-to-immediately-delete-user-state"></a>No configurar la directiva de eliminación para eliminar el estado de usuario inmediatamente  

Si configura la directiva de eliminación en el punto de migración de estado para quitar inmediatamente los datos marcados para su eliminación, y si un atacante consigue recuperar los datos de estado de usuario antes de que lo haga un equipo válido, el sitio elimina inmediatamente los datos de estado de usuario. Establezca el intervalo **Eliminar después de** para que sea lo suficientemente largo para comprobar la correcta restauración de los datos de estado de usuario.  


### <a name="manually-delete-computer-associations"></a>Eliminación manual de las asociaciones de equipo 

Elimine manualmente las asociaciones de equipo cuando la restauración de datos de migración de estado de usuario se haya comprobado y finalizado.

Configuration Manager no quita automáticamente las asociaciones de equipo. Ayude a proteger la identidad de los datos de estado de usuario mediante la eliminación manual de las asociaciones de equipo que ya no sean necesarias.  


### <a name="manually-back-up-the-user-state-migration-data-on-the-state-migration-point"></a>Realice manualmente una copia de seguridad de los datos de la migración de estado de usuario en el punto de migración de estado.  

La copia de seguridad de Configuration Manager no incluye los datos de la migración del estado de usuario en la copia de seguridad del sitio.  


### <a name="implement-access-controls-to-protect-the-prestaged-media"></a>Implemente controles de acceso para proteger el medio preconfigurado.  

Controle el acceso físico a los medios para impedir que un atacante use ataques criptográficos para obtener el certificado de autenticación del cliente y datos confidenciales.  


### <a name="implement-access-controls-to-protect-the-reference-computer-imaging-process"></a>Implemente controles de acceso para proteger el proceso de creación de imágenes del equipo de referencia.  

Asegúrese de que el equipo de referencia que se usa para capturar las imágenes de sistema operativo está en un entorno seguro. Use los controles de acceso apropiados para que no se pueda instalar software inesperado o malintencionado ni se incluya accidentalmente en la imagen capturada. Al capturar la imagen, asegúrese de que la ubicación de red de destino sea segura. Este proceso ayuda a asegurarse de que la imagen no se podrá manipular después de capturarla.  


### <a name="always-install-the-most-recent-security-updates-on-the-reference-computer"></a>Instale siempre las actualizaciones de seguridad más recientes en el equipo de referencia.  

Cuando el equipo de referencia tiene las actualizaciones de seguridad más recientes, se reduce la ventana de vulnerabilidad para los nuevos equipos cuando se inician por primera vez.  


### <a name="implement-access-controls-when-deploying-an-os-to-an-unknown-computer"></a>Implementación de controles de acceso al implementar un sistema operativo en un equipo desconocido

Si tiene que implementar un sistema operativo en un equipo desconocido, implemente controles de acceso para impedir que equipos no autorizados se conecten a la red.  

El aprovisionamiento de equipos desconocidos proporciona un método práctico para implementar equipos nuevos a petición. Pero también puede permitir que un atacante se convierta de forma eficaz en un cliente de confianza en la red. Restrinja el acceso físico a la red y supervise los clientes para detectar equipos no autorizados. 

Es posible que en los equipos que responden a una implementación de SO iniciada por PXE se destruyan todos los datos durante el proceso. Este comportamiento podría producir una pérdida de disponibilidad de los sistemas que se volvieron a formatear de forma inadvertida.  


### <a name="enable-encryption-for-multicast-packages"></a>Habilite el cifrado de paquetes de multidifusión.  

Por cada paquete de implementación de SO, puede habilitar el cifrado cuando Configuration Manager transfiera el paquete mediante multidifusión. Esta configuración ayuda a impedir que los equipos no autorizados se unan a la sesión de multidifusión. También ayuda a evitar que los atacantes manipulen la transmisión.  


### <a name="monitor-for-unauthorized-multicast-enabled-distribution-points"></a>Controle los puntos de distribución habilitados para la multidifusión no autorizados.  

Si los atacantes pueden obtener acceso a la red, podrán configurar servidores de multidifusión no autorizados para suplantar la implementación del sistema operativo.  


### <a name="when-you-export-task-sequences-to-a-network-location-secure-the-location-and-secure-the-network-channel"></a>Cuando exporte las secuencias de tareas a una ubicación de red, proteja la ubicación y el canal de red.

Restrinja quién puede tener acceso a la carpeta de red.  

Utilice la firma SMB o IPsec entre el servidor de sitio y la ubicación de red para impedir que un atacante manipule la secuencia de tareas exportada.  


### <a name="if-you-use-the-task-sequence-run-as-account-take-additional-security-precautions"></a>Si usa la cuenta de ejecución de secuencia de tareas, tome precauciones de seguridad adicionales

Si usa la [cuenta de ejecución de secuencia de tareas](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account), adopte las precauciones siguientes:  

- Utilice una cuenta con los mínimos permisos posibles.  

- No use la cuenta de acceso a la red para esta cuenta.  

- Nunca convierta la cuenta en administrador de dominio.  

- No configure nunca perfiles móviles para esta cuenta. Cuando se ejecuta la secuencia de tareas, descarga el perfil móvil de la cuenta, que lo deja vulnerable y se puede acceder a él en el equipo local.  

- Limite el ámbito de la cuenta. Por ejemplo, cree otras cuentas de ejecución de secuencia de tareas para cada secuencia de tareas. Si una cuenta pierde su carácter confidencial, solo estarán en peligro los equipos cliente a los que acceda esa cuenta. Si la línea de comandos requiere acceso administrativo al equipo, considere la posibilidad de crear una cuenta de administrador local solamente para la cuenta de ejecución de secuencia de tareas. Cree esta cuenta local en todos los equipos que ejecutan la secuencia de tareas y elimínela cuanto ya no sea necesaria.  


### <a name="restrict-and-monitor-the-administrative-users-who-are-granted-the-os-deployment-manager-security-role"></a>Restricción y supervisión de los usuarios administrativos a los que se concede el rol de seguridad de Administrador de implementaciones de sistema operativo

Los usuarios administrativos a los que se concede el rol de seguridad de **Administrador de implementaciones de sistema operativo** pueden crear certificados autofirmados. Después, estos certificados se pueden usar para suplantar a un cliente y obtener la directiva de cliente de Configuration Manager.  


### <a name="use-enhanced-http-to-reduce-the-need-for-a-network-access-account"></a>Uso de HTTP mejorado para reducir la necesidad de una cuenta de acceso a la red

A partir de la versión 1806, al habilitar [HTTP mejorado](../../core/plan-design/hierarchy/enhanced-http.md), en varios escenarios de implementación de sistema operativo no se necesita una cuenta de acceso a la red para descargar contenido desde un punto de distribución. Para obtener más información, vea [Secuencias de tareas y la cuenta de acceso a la red](planning-considerations-for-automating-tasks.md#BKMK_TSNetworkAccessAccount).<!--1358278--> 



## <a name="security-issues-for-os-deployment"></a>Problemas de seguridad para la implementación de SO  

Aunque la implementación de SO puede ser una forma conveniente de implementar las configuraciones y los sistemas operativos más seguros para los equipos en la red, tiene los siguientes riesgos para la seguridad:  


### <a name="information-disclosure-and-denial-of-service"></a>Divulgación de información y denegación de servicio  

Si un atacante puede obtener el control de la infraestructura de Configuration Manager, podría ejecutar cualquier secuencia de tareas. Es posible que este proceso incluya el formateo de los discos duros de todos los equipos cliente. Las secuencias de tareas pueden configurarse para contener información confidencial, como las cuentas que tienen permisos para unir el dominio y las claves de licencias por volumen.  


### <a name="impersonation-and-elevation-of-privileges"></a>Suplantación y elevación de privilegios  

Las secuencias de tareas pueden unir un equipo al dominio, lo que puede proporcionar acceso autenticado a la red a un equipo no autorizado. 

Proteja el certificado de autenticación de cliente que se usa para los medios de secuencia de tareas de arranque y la implementación de arranque PXE. Cuando capture un certificado de autenticación de cliente, este proceso permite a un atacante obtener la clave privada en el certificado. Este certificado les permite suplantar a un cliente válido en la red. En este escenario, el equipo no autorizado podrá descargar la directiva, que puede contener datos confidenciales.  

Si los clientes usan la cuenta de acceso a la red para acceder a los datos almacenados en el punto de migración de estado, estos clientes comparten la misma identidad. Podrían acceder a los datos de migración de estado desde otro cliente que usa la cuenta de acceso a la red. Los datos se cifran de manera que solo el cliente original puede leerlos, pero se podrían alterar o eliminar.  


### <a name="client-authentication-to-the-state-migration-point-is-achieved-by-using-a-configuration-manager-token-that-is-issued-by-the-management-point"></a>La autenticación de cliente en el punto de migración de estado se consigue mediante un token de Configuration Manager emitido por el punto de administración.  

Configuration Manager no limita ni administra la cantidad de datos que se almacenan en el punto de migración de estado. Un atacante podría llenar el espacio disponible en disco y provocar una denegación de servicio.  


### <a name="if-you-use-collection-variables-local-administrators-can-read-potentially-sensitive-information"></a>Si se usan variables de recopilación, los administradores locales pueden leer información potencialmente confidencial  

Aunque las variables de recopilación ofrecen un método flexible para implementar sistemas operativos, es posible que esta característica provoque la divulgación de información.  



##  <a name="privacy-information-for-os-deployment"></a><a name="bkmk_privacy"></a> Información de privacidad para la implementación de SO  

Además de implementar un sistema operativo en equipos que no tengan uno, Configuration Manager se puede usar para migrar las configuraciones y los archivos de los usuarios de un equipo a otro. El administrador configura la información que se va a transferir, como los archivos de datos personales, las opciones de configuración y las cookies del explorador.  

Configuration Manager almacena la información en un punto de migración de estado y la cifra durante la transmisión y el almacenamiento. Solo el nuevo equipo asociado a la información de estado puede recuperar la información almacenada. Si el equipo nuevo pierde la clave para recuperar la información, un administrador de Configuration Manager con el derecho **Ver información de recuperación** en los objetos de instancia de asociación de equipo puede acceder a la información y asociarla a un equipo nuevo. Después de que el equipo nuevo restaure la información de estado, de forma predeterminada, elimina los datos después de un día. Puede configurar cuándo el punto de migración de estado quitará los datos marcados para su eliminación. Configuration Manager no almacena la información de migración de estado en la base de datos de sitio y no la envía a Microsoft.  

Si usa medios de arranque para implementar imágenes de SO, use siempre la opción predeterminada para proteger con contraseña el medio de arranque. La contraseña cifra todas las variables almacenadas en la secuencia de tareas, pero la información no almacenada en una variable puede ser vulnerable a la divulgación.  

La implementación de SO puede usar secuencias de tareas para realizar varias tareas durante el proceso de implementación, como la instalación de aplicaciones y actualizaciones de software. Al configurar las secuencias de tareas, también debe tener en cuenta las implicaciones de privacidad de la instalación de software.  

Configuration Manager no implementa la implementación de SO de forma predeterminada. Requiere varios pasos de configuración antes de recopilar la información de estado de usuario o crear secuencias de tareas o imágenes de arranque.  

Antes de configurar la implementación de SO, tenga en cuenta los requisitos de privacidad.  



## <a name="see-also"></a>Vea también

[Diagnósticos y datos de uso](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)

[Seguridad y privacidad de Configuration Manager](../../core/plan-design/security/security-and-privacy.md)
