---
title: Solución de problemas de CMPivot
titleSuffix: Configuration Manager
description: Obtenga información sobre cómo solucionar problemas de CMPivot en Configuration Manager.
ms.date: 10/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 36385bea-f05e-4300-947f-cb3927b3bac5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7302262c0da5f48bae83f5194ce41206055ae94d
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608345"
---
# <a name="troubleshoot-cmpivot"></a>Solución de problemas de CMPivot

CMPivot es una herramienta que proporciona acceso al estado en tiempo real de los dispositivos de su entorno. CMPivot ejecuta una consulta en todos los dispositivos conectados actualmente en la colección de destino y devuelve los resultados.

En algunas ocasiones, es posible que tenga que solucionar problemas de CMPivot. Por ejemplo, si un mensaje de estado de un cliente a CMPivot resulta dañado, el servidor de sitio no puede procesar el mensaje. Este artículo le ayudará a comprender el flujo de información de CMPivot.

## <a name="troubleshoot-cmpivot-in-version-1902-and-later"></a><a name="bkmk_CMPivot-1902"></a> Solución de problemas de CMPivot en la versión 1902 y posteriores

En la versión 1902 y versiones posteriores de Configuration Manager, puede ejecutar CMPivot desde el sitio de administración central (CAS) en una jerarquía. El sitio primario sigue controlando la comunicación con el cliente.

Al ejecutar CMPivot desde CAS, se usa el canal de suscripción de mensajes de alta velocidad para comunicarse con el sitio primario. CMPivot no usa la replicación de SQL estándar entre sitios. Si la instancia de SQL Server o el proveedor de SQL son remotos, o bien si usa SQL Server Always On, tendrá un "escenario de salto doble" para CMPivot. Para obtener información sobre cómo definir la delegación restringida para un "escenario de salto doble", consulte [CMPivot a partir de la versión 1902](cmpivot-changes.md#bkmk_cmpivot1902).

>[!IMPORTANT]
> Para solucionar problemas de CMPivot, habilite el registro detallado en los puntos de administración (MP) y en el componente SMS_MESSAGE_PROCESSING_ENGINE del servidor de sitio para más información. Además, si el resultado del cliente es superior a 80 KB, habilite el registro detallado en el módulo de administración y el componente SMS_STATE_SYSTEM del servidor de sitio. Para más información sobre cómo habilitar el registro detallado, consulte las [opciones de registro del servidor de sitio](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-site).

### <a name="get-information-from-the-site-server"></a>Obtención de información del servidor de sitio

De manera predeterminada, los archivos de registro del servidor de sitio están ubicados en `C:\Program Files\Microsoft Configuration Manager\logs`. Esta ubicación podría ser distinta si se especifica un directorio de instalación no predeterminado o elementos descargados como el proveedor de SMS en otro servidor. Si ejecuta CMPivot desde el CAS, los registros se encuentran en el servidor de sitio primario.

Busque estas líneas en `smsprov.log`:

- Configuration Manager, versión 1906:
  <pre><code lang="Log">Auditing: User &ltusername> initiated client operation 145 to collection &ltCollectionId>. </code></pre>

- Configuration Manager, versión 1902:
  <pre><code lang="Log">Type parameter is 135.
  Auditing: User &ltusername> ran script 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 with hash dc6c2ad05f1bfda88d880c54121c8b5cea6a394282425a88dd4d8714547dc4a2 on collection &ltCollectionId>. </code></pre>

 `7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14` es el GUID de script para CMPivot. También puede ver este GUID en los [mensajes de estado de auditoría de CMPivot](cmpivot-changes.md#cmpivot-audit-status-messages).

A continuación, busque el identificador en la ventana de CMPivot. Este identificador es el `ClientOperationID`.

![Ventana de CMPivot con ClientOperationID resaltado, versión 1902](media/cmpivot-client-operationid-1902.png)

Busque el `TaskID` en la tabla ClientAction. El `TaskID` corresponde al `UniqueID` de la tabla ClientAction.

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

En `BgbServer.log`, busque el `TaskID` que recopiló de SQL y tenga en cuenta el `PushID`. `TaskID` se etiqueta como `TaskGUID`. Por ejemplo:

<pre><code lang="Log">Starting to send push task (<b>PushID: 9</b> TaskID: 12 <b>TaskGUID: 9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b> TaskType: 15 TaskParam: PFNjcmlwdENvbnRlbnQgU2NyaXB0R3VpZD0nN0RDNkI2RjEtRTdGNi00M0MxL (truncated log entry)
Finished sending push task (<b>PushID: 9</b> TaskID: 12) to 2 clients
</code></pre>

### <a name="client-logs"></a>Registros de cliente

Una vez que haya reunido la información del servidor de sitio, compruebe los registros de cliente. De manera predeterminada, los registros de cliente se encuentran en `C:\Windows\CCM\Logs`.

En `CcmNotificationAgent.log`, busque las entradas de registro que tengan un aspecto similar a las líneas siguientes:  

<pre><code lang="Log">Receive task from server with <b>pushid=9</b>, taskid=12, <b>taskguid=9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0</b>, tasktype=15 and taskParam=PFNjcmlwdEhhc2ggU2NyaXB0SGF (truncated log entry)
Send Task response message &ltBgbResponseMessage TimeStamp="2019-09-13T17:29:09Z"><b>&ltPushID>5</b>&lt/PushID>&ltTaskID>4&lt/TaskID>&ltReturnCode>1&lt/ReturnCode>&lt/BgbResponseMessage> successfuly.
 </code></pre>

En `Scripts.log`, busque `TaskID`. En el siguiente ejemplo, verá `Task ID` `{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}`:

<pre><code lang="Log">Sending script state message (fast): <b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Result are sent for ScriptGuid: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14 and <b>TaskID: {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
</code></pre>

> [!NOTE]
> Si no ve "(fast)" en `Scripts.log`, es probable que los datos superen los 80 KB. En este caso, la información se envía al servidor de sitio como un mensaje de estado. Use el `StateMessage.log` del cliente y el `Statesys.log` del servidor de sitio.

### <a name="review-messages-on-the-site-server"></a>Revisión de los mensajes en el servidor de sitio

Cuando el [registro detallado](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-client) está habilitado en el punto de administración, puede ver cómo se administran los mensajes de cliente entrantes. En `MP_RelayMsgMgr.log`, busque el `TaskID`.

En el ejemplo de `MP_RelayMsgMgr.log`, puede ver el identificador `(GUID:83F67728-2E6D-4E4F-8075-ED035C31B783)` del cliente y el `Task ID {9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}`. Un identificador de mensaje se asigna a la respuesta del cliente antes de enviarse al motor de procesamiento de mensajes:

<pre><code lang="Log">MessageKey: GUID:83F67728-2E6D-4E4F-8075-ED035C31B783<b>{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}</b>
Create message succeeded for <b>message id 22f00adf-181e-4bad-b35e-d18912f39f89</b>
Add message payload succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
Put message succeeded for message id 22f00adf-181e-4bad-b35e-d18912f39f89
CRelayMsgMgrHandler::HandleMessage(): ExecuteTask() succeeded
</code></pre>

Cuando el [registro detallado](../../plan-design/hierarchy/about-log-files.md#bkmk_logoptions) está habilitado en `SMS_MESSAGE_PROCESSING_ENGINE.log`, se procesan los resultados del cliente. Use el identificador de mensaje que encontró en el `MP_RelayMsgMgr.log`. Las entradas del registro de procesamiento son similares al ejemplo siguiente:

<pre><code lang="Log">Processing 2 messages with type Instant and IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]...
Processed 2 messages with type Instant. Failed to process 0 messages. All message IDs <b>22f00adf-181e-4bad-b35e-d18912f39f89[19]</b>, 434d80ae-09d4-4d84-aebf-28a4a29a9852[20]
</code></pre>

> [!TIP]
> Si obtiene una excepción durante el procesamiento, puede revisarla con la ejecución de la siguiente consulta SQL y el examen de la columna de excepciones. Una vez que se procese el mensaje, dejará de aparecer en la tabla `MPE_RequestMessages_Instant`.
>
> ```SQL
> select * from MPE_RequestMessages_Instant where MessageID=<ID from SMS_MESSAGE_PROCESSING_ENGINE.log>
> ```

En `BgbServer.log`, busque el `PushID` para ver el número de clientes con informes o con errores.

<pre><code lang="Log">Generated BGB task status report c:\ConfigMgr\inboxes\bgb.box\Bgb5c1db.BTS at 09/16/2019 16:46:39. (<b>PushID: 9</b> ReportedClients: 2 FailedClients: 0)
</code></pre>

Compruebe la vista de supervisión para CMPivot desde SQL mediante el `TaskID`.

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{9A4E59D2-2F5B-4067-A9FA-B99602A3A4A0}'
```

[ ![Consultas SQL de CMPivot para solucionar problemas en la versión 1902](media/cmpivot-sql-queries-1902.png)](media/cmpivot-sql-queries-1902.png#lightbox)

## <a name="troubleshoot-cmpivot-in-1810-and-earlier"></a><a name="bkmk_CMPivot-1810"></a> Solución de problemas de CMPivot en la versión 1810 y versiones anteriores

En la versión 1810 y versiones anteriores de Configuration Manager, el servidor de sitio controla la comunicación con el cliente.

### <a name="get-information-from-the-site-server"></a>Obtención de información del servidor de sitio

De manera predeterminada, los archivos de registro del servidor de sitio están ubicados en `C:\Program Files\Microsoft Configuration Manager\logs`. Esta ubicación podría ser distinta si se especifica un directorio de instalación no predeterminado o elementos descargados como el proveedor de SMS en otro servidor.

Busque esta línea en `smsprov.log`:

<pre><code lang="Log">Auditing: User <username> initiated client operation 135 to collection &ltCollectionId>.
</code></pre>

Busque el identificador en la ventana de CMPivot. Este identificador es el `ClientOperationID`.

![Ventana de CMPivot con ClientOperationID resaltado](media/cmpivot-clientoperationid.png)

Busque el `TaskID` en la tabla ClientAction. El `TaskID` corresponde al `UniqueID` de la tabla ClientAction.

``` SQL
select * from ClientAction where ClientOperationId=<id>
```

En `BgbServer.log`, busque el `TaskID` que recopiló de SQL. Tiene la etiqueta `TaskGUID`. Por ejemplo:

<pre><code lang="Log">Starting to send push task (PushID: 260 TaskID: 258 TaskGUID: <b>F8C7C37F-B42B-4C0A-B050-2BB44DF1098A</b> TaskType: 15
TaskParam: PFNjcmlwdEhhc2ggU2NyaXB0SGF...truncated...to 5 clients with throttling (strategy: 1 param: 42)
Finished sending push task (PushID: 260 TaskID: 258) to 5 clients
</code></pre>

### <a name="client-logs"></a>Registros de cliente

Una vez que haya reunido la información del servidor de sitio, compruebe los registros de cliente. De manera predeterminada, los registros de cliente se encuentran en `C:\Windows\CCM\Logs`.

En `CcmNotificationAgent.log`, busque registros similares a la entrada siguiente:  

<pre><code lang="Log"><b>Error! Bookmark not defined.</b>+PFNjcmlwdEhhc2ggU2NyaXB0SGFzaEFsZz0nU0hBMjU2Jz42YzZmNDY0OGYzZjU3M2MyNTQyNWZiNT
g2ZDVjYTIwNzRjNmViZmQ1NTg5MDZlMWI5NDRmYTEzNmFiMDE0ZGNjPC9TY3JpcHRIYXNoPjxTY3Jp (truncated log entry)
</code></pre>

En `Scripts.log`, busque el `TaskID`. En el ejemplo siguiente, consulte `Task ID {F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}`:

<pre><code lang="Log">Sending script state message: 7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14
State message: Task Id <b>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</b>
</code></pre>

Busque en `StateMessage.log`. En el ejemplo siguiente, verá que `TaskID` está cerca del final del mensaje junto con `<Param>`:

``` XML
StateMessage body: <?xml version="1.0" encoding="UTF-16"?>
<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>

Successfully forwarded State Messages to the MP StateMessage 7/3/2018 11:44:47 AM 5036 (0x13AC)
```

### <a name="review-messages-on-the-site-server"></a>Revisión de los mensajes en el servidor de sitio

Abra `statesys.log` para ver si el mensaje se recibió y procesó. En el ejemplo siguiente, verá `TaskID` cerca del final del mensaje junto con `<Param>`. Habilite el [registro detallado](../../plan-design/hierarchy/about-log-files.md#bkmk_logoptions) en el componente SMS_STATE_SYSTEM para ver estas entradas de registro.

``` XML
CMessageProcessor - the cmdline to DB exec dbo.spProcessStateReport N'?<?xml version="1.0" encoding="UTF-
16"?>~~<Report><ReportHeader><Identification><Machine><ClientInstalled>1</ClientInstalled><ClientType>1
</ClientType><ClientID>GUID:DBAC52C9-57E6-47D7-A8D6-E0A5A64B57E6</ClientID><ClientVersion>5.00.8670.1000</ClientVersion>
<NetBIOSName>R613924</NetBIOSName><CodePage>437</CodePage>
<SystemDefaultLCID>1033</SystemDefaultLCID><Priority>0</Priority></Machine></Identification>
<ReportDetails><ReportContent>State Message Data</ReportContent><ReportType>Full</ReportType>
<Date>20180703184447.673000+000</Date><Version>1.0</Version><Format>1.0</Format>
</ReportDetails></ReportHeader><ReportBody><StateMessage MessageTime="20180703184447.517000+000"><Topic ID="7DC6B6F1-E7F6-43C1-96E0-E1D16BC25C14" Type="9003" IDType="0" User="" UserSID=""/><State ID="1" Criticality="0"/>
<StateDetails Type="1"><![CDATA["PAA/AHgAbQBsACAAdgBlAHIAcwBpAG8AbgA9ACIAMQAuADAAIgAgAGUAbgBjAG8AZABpAG4AZwA9ACIAdQB0AGYALQAxADYAIgA/AD4APAByAGUAcwB1AGwAdAAgAFIAZQBzAHUAbAB0AEMAbwBkAGUAPQAiADAAIgA+ADwAZQAgAE4AYQBtAGUAPQAiAEkAbgB0AGUAbAAoAFIAKQAgAFgAZQBvAG4AKABSACkAIABDAFAAVQAgAEUANQAtADIANgA3ADMAIAB2ADQAIABAACAAMgAuADMAMABHAEgAegAiACAATQBhAG4AdQBmAGEAYwB0AHUAcgBlAHIAPQAiAEEAbQBlAHIAaQBjAGEAbgAgAE0AZQBnAGEAdAByAGUAbgBkAHMAIABJAG4AYwAuACIAIABWAGUAcgBzAGkAbwBuAD0AIgBWAFIAVABVAEEATAAgAC0AIAA2ADAAMAAxADcAMAAyACIAIABSAGUAbABlAGEAcwBlAEQAYQB0AGUAPQAiADIAMAAxADcALQAwADYALQAwADIAIAAwADAAOgAwADAAOgAwADAAIgAgAFMAZQByAGkAYQBsAE4AdQBtAGIAZQByAD0AIgAwADAAMAAwAC0AMAAwADEAOAAtADMANgA4ADIALQA0ADcAMAA4AC0ANwA2ADQAMAAtADcANgAwADAALQAzADMAIgAgAFMATQBCAEkATwBTAEIASQBPAFMAVgBlAHIAcwBpAG8AbgA9ACIAMAA5ADAAMAAwADcAIAAiACAALwA+ADwALwByAGUAcwB1AGwAdAA+AA=="~~]]></StateDetails><UserParameters Flags="0" Count="2">
<Param>{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}</Param><Param>0</Param></UserParameters></StateMessage></ReportBody></Report>~~'
```

Si no se procesó el mensaje, compruebe la bandeja de entrada de los mensajes de estado. La ubicación predeterminada de la bandeja de entrada es `C:\Program Files\Microsoft Configuration Manager\inboxes\auth\statesys.box\`. Busque los archivos en estas ubicaciones:

- Entrante
- Dañado
- Proceso

Compruebe la vista de supervisión para CMPivot desde SQL mediante el `TaskID`.

``` SQL
select * from vSMS_CMPivotStatus where TaskID='{F8C7C37F-B42B-4C0A-B050-2BB44DF1098A}'
```

>[!NOTE]
>En el caso de los clientes que usan la versión 1810 o posterior, no se utiliza la mensajería de estado a menos que la salida sea superior a 80 KB. A la hora de solucionar problemas de CMPivot en estos casos, puede obtener más información cuando habilite el registro detallado en los módulos de detección y el componente SMS_MESSAGE_PROCESSING_ENGINE del servidor de sitio. Para más información sobre cómo habilitar el registro detallado, consulte las [opciones de registro del servidor de sitio](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-site).
>
> Para solucionar problemas, consulte los registros siguientes:
>
> - `MP_Relay.log`
> - `SMS_MESSAGE_PROCESSING_ENGINE.log`

## <a name="next-steps"></a>Pasos siguientes

- [Uso de CMPivot](cmpivot.md)
- [Crear y ejecutar scripts de PowerShell](../../../apps/deploy-use/create-deploy-scripts.md)
