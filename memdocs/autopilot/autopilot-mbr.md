---
title: Sustitución de la placa de Windows AutoPilot
ms.reviewer: ''
manager: laurawi
description: Escenarios MBR de implementación de Windows AutoPilot
keywords: MDM, configurar, Windows, Windows 10, Oobe, administrar, implementar, AutoPilot, ZTD, cero-Touch, Partner, msfb, Intune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 4c8e66e9fb0ac4527f10824332f8ac5ae1646181
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/04/2020
ms.locfileid: "87757399"
---
# <a name="windows-autopilot-motherboard-replacement-scenario-guidance"></a>Guía del escenario de sustitución de la placa de Windows AutoPilot

**Se aplica a**

- Windows 10

Este documento ofrece orientación para los escenarios de reparación de dispositivos de Windows AutoPilot que los asociados de Microsoft pueden usar en situaciones de sustitución de la placa base (MBR) y otros escenarios de mantenimiento.

La reparación de los dispositivos inscritos con el piloto automático es compleja, ya que intenta equilibrar los requisitos de OEM con los requisitos de Windows AutoPilot.  En concreto, los OEM requieren una singularidad estricta entre las motherboards, las direcciones MAC, etc., mientras que Windows AutoPilot requiere una singularidad estricta en el nivel de identificador de hardware de cada dispositivo para habilitar el registro correcto.  El identificador de hardware no siempre admite todos los requisitos de componentes de hardware de OEM, por lo que estos requisitos a veces son posibles, lo que provoca problemas en algunos escenarios de reparación.

**Reemplazo de la placa base (MBR)**

Si se necesita un reemplazo de la placa base en un dispositivo Windows AutoPilot, se recomienda el proceso siguiente:

1. [Anular el registro del dispositivo](#deregister-the-autopilot-device-from-the-autopilot-program) desde Windows AutoPilot
2. [Reemplazar la placa base](#replace-the-motherboard)
3. [Capturar un nuevo identificador de dispositivo (4K HH)](#capture-a-new-autopilot-device-id-4k-hh-from-the-device)
4. Volver a [registrar el dispositivo](#reregister-the-repaired-device-using-the-new-device-id) con Windows AutoPilot
5. [Restablecer el dispositivo](#reset-the-device)
6. [Devolver el dispositivo](#return-the-repaired-device-to-the-customer)

A continuación, se describen cada uno de estos pasos.

## <a name="deregister-the-autopilot-device-from-the-autopilot-program"></a>Anular el registro del dispositivo AutoPilot desde el programa AutoPilot

Antes de que el dispositivo llegue a la reparación, se debe anular el registro de la entidad que lo registró. Solo la entidad que registró el dispositivo puede anular su registro.   Podría ser el administrador de TI del cliente, el OEM o el asociado de CSP.  Si el administrador de ti registró el dispositivo, es probable que lo hiciera a través de Intune (o posiblemente el Microsoft Store para la empresa).  En ese caso, deben anular el registro del dispositivo de Intune (o MSfB).  Esto es necesario porque los dispositivos registrados en Intune no se mostrarán en MPC.  Sin embargo, si el OEM o el asociado de CSP registraron el dispositivo, probablemente lo hicieron a través del centro de Partners de Microsoft (MPC).  En ese caso, deben anular el registro del dispositivo de MPC, lo que también lo quitará de la cuenta de Intune del administrador de TI del cliente.  A continuación, se describen los pasos que puede seguir un administrador de TI para cancelar el registro de un dispositivo de Intune, así como los pasos que un OEM o CSP pasaría para anular el registro de un dispositivo de MPC.

**Nota**: cuando sea posible, un OEM o CSP debe registrar los dispositivos AutoPilot, en lugar de hacer que el cliente lo haga.  Esto evitará problemas en los que los OEM o CSP no puedan anular el registro de un dispositivo si, por ejemplo, un cliente que realiza la concesión de un dispositivo sale de la empresa antes de anular su registro.

**Excepción**: Si un cliente concede un permiso de OEM para registrar los dispositivos en su nombre a través del proceso de consentimiento automático, un OEM puede usar la API para cancelar el registro de dispositivos que no se registraron (en su lugar, el cliente registró los dispositivos).  Sin embargo, tenga en cuenta que esto solo quitará los dispositivos del programa AutoPilot, no los desscribirá de Intune ni los separará de AAD.  El cliente debe realizar esos pasos, si lo desea, a través de Intune.

### <a name="deregister-from-intune"></a>Anular el registro de Intune

Para cancelar el registro de un dispositivo AutoPilot de Intune, un administrador de TI:

1. Iniciar sesión en su cuenta de Intune
2. Vaya a Intune > grupos > todos los grupos
3. Quitar el dispositivo deseado de su grupo
4. Vaya a Intune > dispositivos > todos los dispositivos
5. Active la casilla situada junto al dispositivo que desea eliminar y, a continuación, haga clic en el botón eliminar en el menú superior.
6. Vaya a Intune > dispositivos > Azure AD dispositivos
7. Active la casilla situada junto al dispositivo que desea eliminar y, a continuación, haga clic en el botón eliminar en el menú superior.
8. Vaya a Intune > inscripción de dispositivos > la inscripción de Windows > dispositivos
9. Active la casilla situada al lado del dispositivo que desea eliminar del registro.
10. Haga clic en el icono de menú extendido ("...") en el extremo derecho de la línea que contiene el dispositivo que desea eliminar del registro para exponer un menú adicional con la opción "Cancelar asignación de usuario".
11. Haga clic en "Cancelar asignación de usuario" si el dispositivo se asignó previamente a un usuario. Si no es así, esta opción estará atenuada y se puede omitir.
12. Con el dispositivo sin asignar aún seleccionado, haga clic en el botón eliminar en el menú superior para quitar este dispositivo.

**Nota**: estos pasos anulan el registro del dispositivo desde el piloto automático, pero también anulan la inscripción del dispositivo de Intune y separan el dispositivo de AAD.  Aunque puede parecer que solo es necesario anular el registro del dispositivo desde AutoPilot, existen ciertas barreras en lugar de Intune que requieren que se realicen todos los pasos anteriores, lo que es una práctica recomendada en caso de que el dispositivo se pierda o se vuelva irrecuperable, para eliminar la posibilidad de que haya dispositivos huérfanos existentes en la base de datos de AutoPilot o en AAD.  Si un dispositivo entra en un estado irrecuperable, puede ponerse en contacto con el [alias de soporte técnico de Microsoft](autopilot-support.md) adecuado para obtener ayuda.

El proceso de anulación del registro tardará unos 15 minutos.  Puede acelerar el proceso haciendo clic en el botón "sincronizar" y luego en "actualizar" la pantalla hasta que el dispositivo ya no esté presente.

Puede encontrar más información sobre cómo cancelar el registro de dispositivos de Intune [aquí](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-device-group).

### <a name="deregister-from-mpc"></a>Anular el registro de MPC

Para cancelar el registro de un dispositivo AutoPilot del centro de Partners de Microsoft (MPC), un CSP:

1. Iniciar sesión en MPC
2. Vaya a dispositivos > cliente
3. Seleccione el dispositivo que se va a cancelar del registro y haga clic en el botón "eliminar dispositivo".

![dispositivos](images/devices.png)

**Nota**: la anulación del registro de un dispositivo de AutoPilot en MPC solo lo hace; tampoco anula la inscripción del dispositivo de MDM (Intune), ni se desconectará del dispositivo de AAD.  Por lo tanto, si es posible, el OEM o el CSP deberían trabajar con el administrador de TI del cliente para que el dispositivo se haya quitado por completo según los pasos de Intune de la sección anterior.

Como alternativa, un asociado de OEM que haya integrado las API directas de OEM puede anular el registro de un dispositivo mediante una llamada a la API AutopilotDeviceRegistration con los campos TenantID y TenantDomain que se dejan en blanco en la llamada de solicitud.  

Dado que la utilidad de reparación no tendrá acceso a las credenciales de inicio de sesión del usuario, la utilidad de reparación tendrá que restablecer la imagen inicial del dispositivo como parte del proceso de reparación.  Esto significa que el cliente debe realizar tres acciones antes de enviar el dispositivo a la reparación:
1. Copie todos los datos importantes fuera del dispositivo.
2. Deje que la utilidad de reparación sepa qué versión de Windows debe reinstalar después de la reparación.
3. Si procede, deje que la utilidad de reparación sepa qué versión de Office debe reinstalar después de la reparación.

## <a name="replace-the-motherboard"></a>Reemplazar la placa base

Los técnicos reemplazan la placa base (u otro hardware) en el dispositivo interrumpido.  Se inserta un DPK de reemplazo.

Los procesos de reparación y reemplazo de claves varían entre las instalaciones.  A veces, las instalaciones de reparación reciben piezas de repuesto de la placa base de OEM que ya tienen DPKs de reemplazo insertado, pero a veces no.  A veces, las instalaciones de reparación reciben herramientas de BIOS totalmente funcionales de OEM, pero a veces no.  Esto significa que la calidad de los datos del BIOS después de un MBR varía.  Para asegurarse de que el dispositivo reparado siga siendo compatible con el piloto automático tras su reparación, el nuevo BIOS (posterior a la reparación) debe ser capaz de recopilar y rellenar la información siguiente como mínimo:

- DiskSerialNumber
- SmbiosSystemSerialNumber
- SmbiosSystemManufacturer
- SmbiosSystemProductName
- SmbiosUuid
- EKPub de TPM
- MacAddress
- ProductKeyID
- OSType

**Nota**: para simplificar y porque los procesos varían entre las instalaciones de reparación, hemos excluido muchos de los pasos adicionales que se usan con frecuencia en un MBR, como:
- Comprobar que el dispositivo sigue siendo funcional
- Deshabilitar BitLocker *
- Reparación del datos de la configuración de arranque (BCD) (BCD)
- Reparar y comprobar la operación del controlador de red

* BitLocker se puede suspender en lugar de deshabilitarse si el técnico tiene la capacidad de reanudarlo después de la reparación.

## <a name="capture-a-new-autopilot-device-id-4k-hh-from-the-device"></a>Capturar un nuevo identificador de dispositivo AutoPilot (4K HH) del dispositivo

Los técnicos de reparación deben iniciar sesión en el dispositivo reparado para capturar el nuevo identificador de dispositivo.  Suponiendo que el técnico de reparación no tenga acceso a las credenciales de inicio de sesión del cliente, tendrá que restablecer la imagen del dispositivo para obtener acceso, según los pasos siguientes:

1. El técnico de reparaciones crea una [unidad USB de arranque de WinPE](https://docs.microsoft.com/windows-hardware/manufacture/desktop/oem-deployment-of-windows-10-for-desktop-editions#create-a-bootable-windows-pe-winpe-partition).
2. El técnico de reparación inicia el dispositivo en WinPE.
3. El técnico de reparación [aplica una nueva imagen de Windows al dispositivo](https://docs.microsoft.com/windows-hardware/manufacture/desktop/work-with-windows-images).

    **Nota**: Idealmente, se debe restablecer la imagen inicial de la misma versión de Windows en el dispositivo que estaba originalmente en el dispositivo, por lo que se necesitará cierta coordinación entre el servicio de reparación y el cliente para capturar esta información en el momento en que el dispositivo llega a la reparación.  Esto podría incluir el cliente que envía la utilidad de reparación a una imagen personalizada (archivo. PPK) a través de un stick USB, por ejemplo.
 
4. El técnico de reparación inicia el dispositivo en la nueva imagen de Windows.
5. Una vez en el escritorio, el técnico de reparaciones captura el nuevo identificador de dispositivo (4K HH) fuera del dispositivo mediante la herramienta OA3 o el script de PowerShell, como se describe a continuación.

Esas instalaciones de reparación con acceso a la herramienta OA3 (que forma parte del ADK) pueden usar la herramienta para capturar el hash de hardware de 4K (4K HH).

Como alternativa, el [script de PowerShell WindowsAutoPilotInfo](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo) se puede usar para capturar 4k HH siguiendo estos pasos:

1. Instale el script desde el [Galería de PowerShell](https://www.powershellgallery.com/packages/Get-WindowsAutoPilotInfo) o desde la línea de comandos (la instalación desde la línea de comandos se muestra a continuación).
2. Navegue hasta el directorio del script y ejecútelo en el dispositivo cuando el dispositivo esté en modo de sistema operativo completo o auditoría. Consulte el ejemplo siguiente.

    ```powershell
    md c:\HWID
    Set-Location c:\HWID
    Set-ExecutionPolicy -Scope Process -ExecutionPolicy Unrestricted -Force
    Install-Script -Name Get-WindowsAutopilotInfo -Force
    Get-WindowsAutopilotInfo.ps1 -OutputFile AutopilotHWID.csv
    ```

>Si se le pide que instale el paquete NuGet, elija **sí**.<br>
>Si, después de instalar el script, obtiene un error que Get-WindowsAutopilotInfo.ps1 no se encuentra, compruebe que C:\Archivos de Files\WindowsPowerShell\Scripts está presente en la variable PATH.<br>
>Si se produce un error en el cmdlet install-script, compruebe que tiene registrado el repositorio de PowerShell predeterminado (**Get-psrepository**) o registre el repositorio predeterminado con **Register-PSRepository-default-verbose**.

El script crea un archivo. csv que contiene la información del dispositivo, incluida la HH de 4K completa.  Guarde este archivo para poder acceder a él más adelante. La utilidad de servicio utilizará este formato de 4K HH para volver a registrar el dispositivo, tal y como se describe a continuación. Asegúrese de usar el parámetro-OutputFile al guardar el archivo, lo que garantiza que el formato del archivo sea correcto. No intente canalizar el resultado del comando a un archivo manualmente.

**Nota**: Si la utilidad de reparación no tiene la capacidad de ejecutar la herramienta OA3 o el script de PowerShell para capturar la nueva serie 4k HH, los asociados de CSP (o OEM) deben hacerlo para ellos.  Sin que alguna entidad Capture el nuevo 4K HH, no hay ninguna manera de volver a registrar este dispositivo como un dispositivo AutoPilot.


## <a name="reregister-the-repaired-device-using-the-new-device-id"></a>Volver a registrar el dispositivo reparado mediante el nuevo ID. de dispositivo

Si un OEM no puede volver a registrar el dispositivo, el servicio de reparación o el CSP debe volver a registrar el dispositivo mediante MPC, o se debe notificar al administrador de TI del cliente que vuelva a registrar el dispositivo a través de Intune (o MSfB).  A continuación se muestran las distintas formas de volver a registrar un dispositivo.

### <a name="reregister-from-intune"></a>Volver a registrar desde Intune

Para volver a registrar un dispositivo AutoPilot desde Intune, un administrador de TI:
1. Inicie sesión en Intune.
2. Vaya a inscripción de dispositivos > inscripción de Windows > dispositivos > importar.
3. Haga clic en el botón **importar** para cargar un archivo CSV que contenga el identificador de dispositivo del dispositivo que se va a volver a registrar (el ID. de dispositivo fue el 4k HH capturado por el script de PowerShell o la herramienta OA3 descrito anteriormente en este documento).

El vídeo siguiente proporciona una buena información general sobre cómo (volver a registrar los dispositivos) a través de MSfB.<br>

> [!VIDEO https://www.youtube.com/embed/IpLIZU_j7Z0]

### <a name="reregister-from-mpc"></a>Volver a registrar desde MPC

Para volver a registrar un dispositivo AutoPilot de MPC, un OEM o un CSP:

1. Inicie sesión en MPC.
2. Vaya a la página dispositivos > cliente y haga clic en el botón **Agregar dispositivos** para cargar el archivo CSV.

![device](images/device2.png)<br>
![device](images/device3.png)

En el caso de que se vuelva a registrar un dispositivo reparado mediante MPC, el archivo CSV cargado debe contener el formato 4K HH para el dispositivo, y no solo el PKID o la tupla (SerialNumber + OEMName + ModelName).  Si solo se usó el PKID o la tupla, el servicio AutoPilot no podría encontrar una coincidencia en la base de datos AutoPilot, ya que no se envió ninguna información de 4K HH anteriormente para este "nuevo" dispositivo, y se producirá un error en la carga, lo que es probable que devuelva un error ZtdDeviceNotFound.  De nuevo, solo tiene que cargar 4K HH, no la tupla o PKID.

**Nota**: cuando se incluye 4k HH en el archivo CSV, no es necesario incluir el pkid o la tupla.  Estas columnas pueden dejarse en blanco, como se muestra a continuación:

![hash](images/hh.png)

## <a name="reset-the-device"></a>Restablecer el dispositivo

Dado que el dispositivo tenía que estar en modo de sistema operativo completo o de auditoría para capturar 4K HH, el servicio de reparación debe restablecer la imagen a un estado anterior a OOBE antes de devolverlo al cliente.  Una manera de hacerlo es mediante el uso de la característica de restablecimiento integrada en Windows, como se indica a continuación:

En el dispositivo, vaya a configuración > actualizar & Security > Recovery y haga clic en introducción.  En restablecer este equipo, seleccione quitar todo y simplemente quitar mis archivos. Por último, haga clic en restablecer.

![reset](images/reset.png)

Sin embargo, es probable que el servicio de reparación no tenga acceso a Windows porque carece de las credenciales de usuario para iniciar sesión, en cuyo caso necesitan usar otros medios para restablecer la imagen inicial del dispositivo, como la [herramienta de administración y mantenimiento de imágenes de implementación](https://docs.microsoft.com/windows-hardware/manufacture/desktop/oem-deployment-of-windows-10-for-desktop-editions#use-a-deployment-script-to-apply-your-image).

## <a name="return-the-repaired-device-to-the-customer"></a>Devolver el dispositivo reparado al cliente

Después de completar los pasos anteriores, el dispositivo reparado se puede devolver al cliente y se inscribirá automáticamente en el programa AutoPilot en el primer arranque durante la ejecución de OOBE.

**Nota**: Si la reparación no ha vuelto a crear la imagen del dispositivo, podría enviarla de nuevo en un estado potencialmente dañado (por ejemplo, no hay ninguna manera de iniciar sesión en el dispositivo porque se ha disociado de la única cuenta de usuario conocida), en cuyo caso deben indicar a la organización que necesitan corregir el registro y el sistema operativo.

**Importante**: un dispositivo se puede "registrar" para el piloto automático antes de que se encienda, pero el dispositivo no está realmente "implementado" en el piloto automático (es decir, habilitado como dispositivo autopiloto) hasta que pasa a través de Oobe, que es el motivo por el que restablecer el dispositivo a un estado anterior a Oobe es un paso necesario.

## <a name="specific-repair-scenarios"></a>Escenarios de reparación específicos

En esta sección se tratan los escenarios de reparación más comunes y su impacto en la habilitación del AutoPilot.

NOTAS SOBRE LOS RESULTADOS DE PRUEBAS:

- Los escenarios siguientes se probaron solo con Intune (no se probó ningún otro MDMs).
- En la mayoría de los escenarios de prueba que se indican a continuación, el dispositivo reparado y que se ha reparado debe volver a ejecutarse en OOBE para que se habilite AutoPilot.
- Los escenarios de reemplazo de la placa base suelen producir pérdida de datos, por lo que se deben recordar centros de reparación o clientes para realizar copias de seguridad de los datos (si es posible) antes de la reparación.
- En los casos en los que una utilidad de reparación no tiene la capacidad de escribir información del dispositivo en el BIOS del dispositivo reparado, es necesario crear nuevos procesos para habilitarlo correctamente.
- El dispositivo reparado debe tener la clave de producto (DPK) insertada previamente en el BIOS antes de capturar el nuevo 4K HH (ID. de dispositivo)

En la tabla siguiente:<br>
- Compatible = **sí**: el dispositivo se puede volver a habilitar para el AutoPilot
- Compatible = **no**: no se puede volver a habilitar el dispositivo para el AutoPilot

<table border="1">
<th>Escenario<th>Compatible<th>Recomendación de Microsoft
<tr><td>Reemplazo de la placa base (MBR) en general<td>Sí<td>El curso de acción recomendado para escenarios MBR es el siguiente:

1. Se anula el registro del dispositivo AutoPilot en el programa AutoPilot
2. La placa base es reemplazar
3. Se restablece la imagen inicial del dispositivo (con la información de BIOS y DPK reinsertada) *
4. Un nuevo identificador de dispositivo AutoPilot (4K HH) se captura fuera del dispositivo
5. Se vuelve a registrar el dispositivo reparado para el programa AutoPilot con el nuevo identificador de dispositivo.
6. El dispositivo reparado se restablece para arrancar en OOBE
7. El dispositivo reparado se envía de vuelta al cliente

* No es necesario restablecer la imagen inicial del dispositivo si el técnico de reparación tiene acceso a las credenciales de inicio de sesión del cliente.  Es técnicamente posible realizar una nueva habilitación de MBR y AutoPilot sin claves o determinada información del BIOS (por ejemplo, número de serie, nombre del modelo, etc.), pero solo se recomienda para fines de pruebas o educativos.

<tr><td>MBR cuando la placa base tiene un chip TPM (habilitado) y solo una tarjeta de red incorporada (que también se reemplaza)<td>Sí<td>

1. Anular el registro del dispositivo dañado
2. Reemplazar placa base
3. Restablecer la imagen del dispositivo (para obtener acceso), a menos que tenga acceso a las credenciales de inicio de sesión de los clientes
4. Escribir la información del dispositivo en el BIOS
5. Capturar nuevo 4K HH
6. Volver a registrar el dispositivo reparado
7. Restablecer el dispositivo a OOBE
8. Pasar a través de AutoPilot OOBE (cliente)
9. AutoPilot habilitado correctamente

<tr><td>MBR cuando la placa base tiene un chip TPM (habilitado) y una segunda tarjeta de red (o interfaz de red) que no se reemplaza junto con la placa base<td>No<td>No se recomienda este escenario, ya que interrumpe la experiencia del piloto automático, ya que el identificador de dispositivo resultante no será estable hasta que se haya completado la atestación de TPM, e incluso después el registro puede proporcionar resultados incorrectos debido a la ambigüedad con la resolución de direcciones MAC.
<tr><td>MBR en el que todas las tarjetas NIC, HDD y WLAN siguen siendo las mismas después de la reparación<td>Sí<td>

1. Anular el registro del dispositivo dañado
2. Reemplazar placa base (con el nuevo RDPK insertado en el BIOS)
3. Restablecer la imagen del dispositivo (para obtener acceso), a menos que tenga acceso a las credenciales de inicio de sesión de los clientes
4. Escriba la información del dispositivo anterior en el BIOS (mismo s/n, modelo, etc.). *
5. Capturar nuevo 4K HH
6. Volver a registrar el dispositivo reparado
7. Restablecer el dispositivo a OOBE
8. Pasar a través de AutoPilot OOBE (cliente)
9. AutoPilot habilitado correctamente

* Tenga en cuenta que para este escenario y otros escenarios posteriores, la reescritura de la información de dispositivo anterior no incluiría la clave de aprobación de TPM 2,0, ya que la clave privada asociada se bloquea en el dispositivo de TPM.

<tr><td>MBR en el que la tarjeta NIC sigue siendo la misma, pero se reemplazan las unidades de disco duro y WLAN<td>Sí<td>

1. Anular el registro del dispositivo dañado
2. Reemplazar placa base (con el nuevo RDPK insertado en el BIOS)
3. Inserción de una unidad de disco duro y WLAN nuevas
4. Escriba la información del dispositivo anterior en el BIOS (mismo s/n, modelo, etc.).
5. Capturar nuevo 4K HH
6. Volver a registrar el dispositivo reparado
7. Restablecer el dispositivo a OOBE
8. Pasar a través de AutoPilot OOBE (cliente)
9. AutoPilot habilitado correctamente

<tr><td>MBR en el que la tarjeta NIC y la WLAN siguen siendo las mismas, pero se reemplaza la unidad de disco duro<td>Sí<td>

1. Anular el registro del dispositivo dañado
2. Reemplazar placa base (con el nuevo RDPK insertado en el BIOS)
3. Insertar HDD nuevo
4. Escriba la información del dispositivo anterior en el BIOS (mismo s/n, modelo, etc.).
5. Capturar nuevo 4K HH
6. Volver a registrar el dispositivo reparado
7. Restablecer el dispositivo a OOBE
8. Pasar a través de AutoPilot OOBE (cliente)
9. AutoPilot habilitado correctamente

<tr><td>MBR donde solo se reemplazan los MB (todas las demás partes siguen siendo iguales) pero se tomó un nuevo MB de un dispositivo usado anteriormente que no se había habilitado para el piloto automático antes.<td>Sí<td>

1. Anular el registro del dispositivo dañado
2. Reemplazar placa base (con el nuevo RDPK insertado en el BIOS)
3. Restablecer la imagen del dispositivo (para obtener acceso), a menos que tenga acceso a las credenciales de inicio de sesión de los clientes
4. Escriba la información del dispositivo anterior en el BIOS (mismo s/n, modelo, etc.).
5. Capturar nuevo 4K HH
6. Volver a registrar el dispositivo reparado
7. Restablecer el dispositivo a OOBE
8. Pasar a través de AutoPilot OOBE (cliente)
9. AutoPilot habilitado correctamente

<tr><td>MBR donde solo se reemplazan los MB (todas las demás partes siguen siendo la misma), pero se tomó un nuevo MB de un dispositivo usado anteriormente que antes estaba habilitado para el piloto.<td>Sí<td>

1. Anula el registro del dispositivo antiguo del que se tomarán MB
2. Anular el registro del dispositivo dañado (que desea reparar)
3. Reemplazar la placa base en el dispositivo de reparación con MB de otro dispositivo AutoPilot (con el nuevo RDPK insertado en BIOS)
4. Restablecer la imagen del dispositivo (para obtener acceso), a menos que tenga acceso a las credenciales de inicio de sesión de los clientes
5. Escriba la información del dispositivo anterior en el BIOS (mismo s/n, modelo, etc.).
6. Capturar nuevo 4K HH
7. Volver a registrar el dispositivo reparado
8. Restablecer el dispositivo a OOBE
9. Pasar a través de AutoPilot OOBE (cliente)
10. AutoPilot habilitado correctamente

<b>Nota</b>: el dispositivo reparado también puede usarse correctamente como un dispositivo piloto normal y no automático.

<tr><td>Información de BIOS excluida del dispositivo MBR<td>No<td>La utilidad de reparación no tiene la herramienta BIOS para escribir información del dispositivo en el BIOS después de MBR.

1. Anular el registro del dispositivo dañado
2. Reemplazar placa base (BIOS no contiene información del dispositivo)
3. Restablecer la imagen inicial y escribir DPK en la imagen
4. Capturar nuevo 4K HH
5. Volver a registrar el dispositivo reparado
6. Crear Perfil de AutoPilot para el dispositivo
7. Pasar a través de AutoPilot OOBE (cliente)
8. AutoPilot no reconoce el dispositivo reparado

<tr><td>MBR cuando no hay ningún chip TPM<td>Sí<td>Aunque no se recomienda habilitar los dispositivos AutoPilot sin un chip de TPM (recomendado para el cifrado de BitLocker), es posible habilitar un dispositivo AutoPilot en el modo "usuario estándar" (pero no en el modo de auto-implementación) que no tiene un chip TPM.  En este caso, debería:

1. Anular el registro del dispositivo dañado
2. Reemplazar placa base
3. Restablecer la imagen del dispositivo (para obtener acceso), a menos que tenga acceso a las credenciales de inicio de sesión de los clientes
4. Escriba la información del dispositivo anterior en el BIOS (mismo s/n, modelo, etc.).
5. Capturar nuevo 4K HH
6. Volver a registrar el dispositivo reparado
7. Restablecer el dispositivo a OOBE
8. Pasar a través de AutoPilot OOBE (cliente)
9. AutoPilot habilitado correctamente

<tr><td>Nuevos DPK escritos en la imagen en el dispositivo AutoPilot reparado con un nuevo MB<td>Sí<td>El servicio de reparación reemplaza los MB normales en el dispositivo dañado.  MB no contiene ningún DPK en el BIOS.  La utilidad de reparación escribe DPK en la imagen después de MBR.  

1. Anular el registro del dispositivo dañado
2. Reemplazar placa base: BIOS no contiene información de DPK
3. Restablecer la imagen del dispositivo (para obtener acceso), a menos que tenga acceso a las credenciales de inicio de sesión de los clientes
4. Escriba la información del dispositivo en el BIOS (mismo s/n, modelo, etc.).
5. Capturar nuevo 4K HH
6. Restablecer o restablecer la imagen inicial del dispositivo en una versión anterior a OOBE y escribir DPK en la imagen
7. Volver a registrar el dispositivo reparado
8. Pasar a través de la OOBE AutoPilot
9. AutoPilot habilitado correctamente

<tr><td>Nueva clave de producto de reparación (RDPK)<td>Sí<td>El uso de una placa base con un nuevo RDPK genera una nueva prueba de reacondicionamiento automático. 

1. Anular el registro del dispositivo dañado
2. Reemplazar placa base (con el nuevo RDPK insertado en el BIOS)
3. Restablecer imagen inicial o imagen de REST a anterior a la instalación rápida
4. Escribir la información del dispositivo en el BIOS 
5. Capturar nuevo 4K HH
6. Volver a registrar el dispositivo reparado
7. Restablecer la imagen inicial o restablecer la imagen a una versión anterior a OOBE
8. Pasar a través de la OOBE AutoPilot
9. AutoPilot habilitado correctamente

<tr><td>No se ha insertado ninguna clave de producto de reparación (RDPK)<td>No<td>Este escenario infringe la Directiva de Microsoft y interrumpe la experiencia de Windows AutoPilot.
<tr><td>Restablecer la imagen del dispositivo AutoPilot dañado que no se canceló antes de la reparación<td>Sí, pero el dispositivo seguirá estando asociado al identificador de inquilino anterior, por lo que solo se debe devolver al mismo cliente.<td>

1. Restablecer la imagen del dispositivo dañado
2. Escribir DPK en la imagen
3. Pasar a través de la OOBE AutoPilot
4. AutoPilot habilitado correctamente (para el ID. de inquilino anterior)

<tr><td>Sustitución del disco de un dispositivo que no es AutoPilot a un dispositivo AutoPilot<td>Sí<td>

1. No anular el registro de un dispositivo dañado antes de la reparación
2. Reemplazar HDD en dispositivo dañado
3. Volver a crear la imagen inicial o restablecer la imagen en OOBE
4. Pasar a través de AutoPilot OOBE (cliente)
5. El AutoPilot se habilitó correctamente (el dispositivo reparó reconocido como su propio anterior)

<tr><td>Sustitución del disco de un dispositivo AutoPilot a otro dispositivo AutoPilot<td>Es posible<td>Si el dispositivo desde el que se lleva a cabo la unidad de disco duro se ha anulado previamente del registro automático, entonces ese HDD puede usarse en un dispositivo de reparación.  Pero si la unidad de disco duro nunca se había cancelado previamente del registro automático antes de usarse en un dispositivo reparado, el dispositivo recién reparado no tendrá la experiencia de AutoPilot adecuada.

Suponiendo que se haya cancelado previamente el registro de la HDD usada (antes de usarse en esta reparación):

1. Anular el registro del dispositivo dañado
2. Reemplazar HDD en un dispositivo dañado mediante una unidad de disco duro de otro dispositivo AutoPilot desregistrado
3. Restablecer la imagen inicial o restablecer el dispositivo reparado a un estado anterior a la instalación rápida
4. Pasar a través de AutoPilot OOBE (cliente)
5. AutoPilot habilitado correctamente

<tr><td>Reemplazo de tarjeta de red que no es de Microsoft <td>No<td>Tanto si se trata de un dispositivo AutoPilot como si no lo es, desde un dispositivo AutoPilot a otro dispositivo AutoPilot o desde un dispositivo AutoPilot hasta un dispositivo piloto no automático, cualquier escenario en el que se reemplace una tarjeta de red de terceros (no incorporados) interrumpirá la experiencia de AutoPilot y no se recomienda.
<tr><td>Un dispositivo se reparó más de 3 veces<td>No<td>AutoPilot no se admite cuando un dispositivo se repara repetidamente, de modo que las partes no reemplazadas se asocian con demasiadas partes que se han reemplazado, lo que dificultaría la identificación única del dispositivo en el futuro.
<tr><td>Reemplazo de memoria<td>Sí<td>Reemplazar la memoria en un dispositivo dañado no afecta negativamente a la experiencia de AutoPilot en ese dispositivo.  No es necesario ningún/volver a registrar.  El técnico de reparación simplemente debe reemplazar la memoria.
<tr><td>Sustitución de GPU<td>Sí<td>Reemplazar las GPU en un dispositivo dañado no afecta negativamente a la experiencia de AutoPilot en ese dispositivo.  No es necesario ningún/volver a registrar.  El técnico de reparación simplemente debe reemplazar la GPU.
</table>

>Al borrar piezas de otro dispositivo AutoPilot, se recomienda anular el registro del dispositivo borrado del piloto automático, borrarlo y, a continuación, no registrar nunca el dispositivo BORRAdo (de nuevo) para el AutoPilot, ya que volver a usar las partes de esta manera puede provocar que dos dispositivos activos acaben con el mismo identificador, sin posibilidad de distinguir entre los dos.

**Nota**: las siguientes partes se pueden reemplazar sin poner en peligro la habilitación del piloto automático o requerir pasos de reparación adicionales especiales:
- Memoria (RAM o ROM)
- Fuente de alimentación
- Tarjeta de vídeo
- Lector de tarjetas
- Tarjeta de sonido
- Tarjeta de expansión
- Micrófono
- Cámara web
- Ventilador
- Disipador térmico
- Batería de CMOS

Otros escenarios de reparación que aún no se han probado y comprobado incluyen:
- Reemplazo de daughterboard
- Reemplazo de CPU
- Reemplazo de WiFi
- Reemplazo de Ethernet

## <a name="faq"></a>Preguntas más frecuentes

| Pregunta | Respuesta |
| --- | --- |
| Si tenemos una herramienta que programa la información del producto en el BIOS después del MBR, ¿todavía necesitamos enviar un informe CBR para que el dispositivo sea compatible con el piloto automático? | No.  No si la herramienta interna escribe la información mínima necesaria en el BIOS que el programa AutoPilot busca para identificar el dispositivo, tal y como se describió anteriormente en este documento. |
| ¿Qué ocurre si solo se reemplazan algunos componentes en lugar de la placa base completa? | Aunque es cierto que algunas reparaciones limitadas no impiden que el algoritmo de AutoPilot coincida correctamente con el dispositivo posterior a la reparación con el dispositivo previo a la reparación, es mejor asegurarse del 100% de éxito mediante los pasos de MBR anteriores, incluso en el caso de los dispositivos que solo necesitan reparaciones limitadas. |
| ¿Cómo obtiene acceso un técnico de reparación a un dispositivo roto si no tienen las credenciales de inicio de sesión del cliente? | El técnico tendrá que restablecer la imagen del dispositivo y usar sus propias credenciales durante el proceso de reparación. |

## <a name="related-topics"></a>Temas relacionados

[Instrucciones del dispositivo](autopilot-device-guidelines.md)<br>
