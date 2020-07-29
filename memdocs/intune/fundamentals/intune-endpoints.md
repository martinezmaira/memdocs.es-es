---
title: Puntos de conexión de red de Microsoft Intune
titleSuffix: ''
description: Revise los puntos de conexión de Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 05/27/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: b8d9aef2-8757-4e22-9b24-a0833d27304c
ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8c9586b27ce5040eb683fa22510c7c9a51aeee1d
ms.sourcegitcommit: a882035696a8cc95c3ef4efdb9f7d0cc7e183a1a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87262547"
---
# <a name="network-endpoints-for-microsoft-intune"></a>Puntos de conexión de red de Microsoft Intune  

En esta página se enumeran las direcciones IP y los valores de puerto necesarios para la configuración del proxy en las implementaciones de Intune.

Como un servicio solo en la nube, Intune no requiere una infraestructura local como servidores o puertas de enlace.

## <a name="access-for-managed-devices"></a>Acceso para dispositivos administrados  

Para administrar dispositivos que se encuentren detrás de firewalls y servidores proxy, debe habilitar la comunicación para Intune.

> [!NOTE]
> La información de la sección también se aplica a Microsoft Intune Certificate Connector. El conector tiene los mismos requisitos de red que los dispositivos administrados.

- El servidor proxy debe ser compatible con **HTTP (80)** y **HTTPS (443)** , ya que los clientes de Intune usan ambos protocolos. Windows Information Protection utiliza el puerto 444.
- Para algunas tareas (como descargar actualizaciones de software para el agente de PC clásico), Intune necesita acceso de un servidor proxy no autenticado a manage.microsoft.com.

Puede modificar la configuración del servidor proxy en equipos cliente individuales. También puede usar la opción de directiva de grupo para cambiar la configuración de todos los equipos cliente que se encuentran detrás de un servidor proxy especificado.


<!--
> [!NOTE] If Windows 8.1 devices haven't cached proxy server credentials, enrollment might fail because the request doesn't prompt for credentials. Enrollment fails without warning as the request wait for a connection. If users might experience this issue, instruct them to open their browser settings and save proxy server settings to enable a connection.   -->

Los dispositivos administrados requieren configuraciones que dejen acceder a **Todos los usuarios** a los servicios a través de firewalls.


En las siguientes tablas se enumeran los puertos y los servicios a los que accede el cliente de Intune:

|Dominios    |Dirección IP      |
|-----------|----------------|
| login.microsoftonline.com <br> *.officeconfig.msocdn.com <br> config.office.com <br> graph.windows.net <br> enterpriseregistration.windows.net | Más información [URL de Office 365 e intervalos de direcciones IP](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) |
|portal.manage.microsoft.com<br> m.manage.microsoft.com |52.175.12.209<br>20.188.107.228<br>52.138.193.149<br>51.144.161.187<br>52.160.70.20<br>52.168.54.64 <br>13.72.226.202<br>52.189.220.232|
| sts.manage.microsoft.com | 13.93.223.241 <br>52.170.32.182 <br>52.164.224.159 <br>52.174.178.4 <br>13.75.122.143 <br>52.163.120.84<br>13.73.112.122<br>52.237.192.112|
|Manage.microsoft.com <br>i.manage.microsoft.com <br>r.manage.microsoft.com <br>a.manage.microsoft.com <br>p.manage.microsoft.com <br>EnterpriseEnrollment.manage.microsoft.com <br>EnterpriseEnrollment-s.manage.microsoft.com |40.83.123.72<br>13.76.177.110<br>52.169.9.87<br>52.174.26.23<br>104.40.82.191<br>13.82.96.212<br>52.147.8.239<br>40.115.69.185|
|portal.fei.msua01.manage.microsoft.com<br>m.fei.msua01.manage.microsoft.com<br>portal.fei.msua02.manage.microsoft.com<br>m.fei.msua02.manage.microsoft.com<br>portal.fei.msua04.manage.microsoft.com<br>m.fei.msua04.manage.microsoft.com<br>portal.fei.msua05.manage.microsoft.com<br>m.fei.msua05.manage.microsoft.com<br>portal.fei.amsua0502.manage.microsoft.com<br>m.fei.amsua0502.manage.microsoft.com<br>portal.fei.msua06.manage.microsoft.com<br>m.fei.msua06.manage.microsoft.com<br>portal.fei.amsua0602.manage.microsoft.com<br>m.fei.amsua0602.manage.microsoft.com<br>fei.amsua0202.manage.microsoft.com<br>portal.fei.amsua0202.manage.microsoft.com<br>m.fei.amsua0202.manage.microsoft.com<br>portal.fei.amsua0402.manage.microsoft.com<br>m.fei.amsua0402.manage.microsoft.com<br>portal.fei.amsua0801.manage.microsoft.com<br>portal.fei.msua08.manage.microsoft.com<br>m.fei.msua08.manage.microsoft.com<br>m.fei.amsua0801.manage.microsoft.com|52.160.70.20<br>52.168.54.64 |
|portal.fei.msub01.manage.microsoft.com<br>m.fei.msub01.manage.microsoft.com<br>portal.fei.amsub0102.manage.microsoft.com<br>m.fei.amsub0102.manage.microsoft.com<br>fei.msub02.manage.microsoft.com<br>portal.fei.msub02.manage.microsoft.com<br>m.fei.msub02.manage.microsoft.com<br>portal.fei.msub03.manage.microsoft.com<br>m.fei.msub03.manage.microsoft.com<br>portal.fei.msub05.manage.microsoft.com<br>m.fei.msub05.manage.microsoft.com<br>portal.fei.amsub0202.manage.microsoft.com<br>m.fei.amsub0202.manage.microsoft.com<br>portal.fei.amsub0302.manage.microsoft.com<br>m.fei.amsub0302.manage.microsoft.com<br>portal.fei.amsub0502.manage.microsoft.com<br>m.fei.amsub0502.manage.microsoft.com<br>portal.fei.amsub0601.manage.microsoft.com<br>m.fei.amsub0601.manage.microsoft.com|52.138.193.149<br>51.144.161.187|
|portal.fei.msuc01.manage.microsoft.com <br>m.fei.msuc01.manage.microsoft.com<br>portal.fei.msuc02.manage.microsoft.com <br>m.fei.msuc02.manage.microsoft.com<br>portal.fei.msuc03.manage.microsoft.com <br>m.fei.msuc03.manage.microsoft.com<br>portal.fei.msuc05.manage.microsoft.com <br>m.fei.msuc05.manage.microsoft.com|52.175.12.209<br>20.188.107.228|
|portal.fei.amsud0101.manage.microsoft.com<br>m.fei.amsud0101.manage.microsoft.com|13.72.226.202|
|fef.msua01.manage.microsoft.com|138.91.243.97|
|fef.msua02.manage.microsoft.com|52.177.194.236|
|fef.msua04.manage.microsoft.com|23.96.112.28|
|fef.msua06.manage.microsoft.com|13.78.185.97|
|fef.msub05.manage.microsoft.com|23.97.166.52|
|fef.msuc03.manage.microsoft.com|23.101.0.100|
|fef.amsua0502.manage.microsoft.com|13.85.68.142|
|fef.amsua0602.manage.microsoft.com|52.161.28.64|
|fef.amsua0102.manage.microsoft.com|52.242.211.0|
|fef.amsua0702.manage.microsoft.com|52.232.225.75|
|fef.amsub0502.manage.microsoft.com|40.67.219.144|
|fef.msud01.manage.microsoft.com|20.40.178.139|
|Admin.manage.microsoft.com|52.224.221.227<br>52.161.162.117<br>52.178.44.195<br>52.138.206.56<br>52.230.21.208<br>13.75.125.10|
|wip.mam.manage.microsoft.com|52.187.76.84<br>13.76.5.121<br>52.165.160.237<br>40.86.82.163<br>52.233.168.142<br>168.63.101.57<br>52.187.196.98<br>52.237.196.51|
|mam.manage.microsoft.com|104.40.69.125<br>13.90.192.78<br>40.85.174.177<br>40.85.77.31<br>137.116.229.43<br>52.163.215.232<br>52.174.102.180<br>52.187.196.173<br>52.156.162.48|
|*.manage.microsoft.com|40.82.248.224/28<br>20.189.105.0/24<br>20.37.153.0/24<br>20.37.192.128/25<br>20.38.81.0/24<br>20.41.1.0/24<br>20.42.1.0/24<br>20.42.130.0/24<br>20.42.224.128/25<br>20.43.129.0/24<br>40.119.8.128/25<br>40.74.25.0/24<br>40.82.249.128/25<br>40.80.184.128/25<br>52.150.137.0/25|


## <a name="network-requirements-for-powershell-scripts-and-win32-apps"></a>Requisitos de red para aplicaciones Win32 y scripts de PowerShell  

Si usa Intune para implementar scripts de PowerShell o aplicaciones Win32, también deberá conceder acceso a los puntos de conexión en los que reside actualmente el inquilino.

|ASU | Nombre de almacenamiento | CDN |
| --- | --- |--- |
|AMSUA0601<br>AMSUA0602<br>AMSUA0101<br>AMSUA0102<br>AMSUA0201<br>AMSUA0202<br>AMSUA0401<br>AMSUA0402<br>AMSUA0501<br>AMSUA0502<br>AMSUA0701<br>AMSUA0702 | naprodimedatapri<br>naprodimedatasec<br>naprodimedatahotfix | naprodimedatapri.azureedge.net<br>naprodimedatasec.azureedge.net<br>naprodimedatahotfix.azureedge.net |
| AMSUB0101<br>AMSUB0102<br>AMSUB0201<br>AMSUB0202<br>AMSUB0301<br>AMSUB0302<br>AMSUB0501<br>AMSUB0502 | euprodimedatapri<br>euprodimedatasec<br>euprodimedatahotfix | euprodimedatapri.azureedge.net<br>euprodimedatasec.azureedge.net<br>euprodimedatahotfix.azureedge.net |
| AMSUC0101<br>AMSUC0201<br>AMSUC0301<br>AMSUC0501<br>AMSUD0101| approdimedatapri<br>approdimedatasec<br>approdimedatahotifx | approdimedatapri.azureedge.net<br>approdimedatasec.azureedge.net<br>approdimedatahotfix.azureedge.net |

## <a name="windows-push-notification-services-wns"></a>Servicios de notificaciones de inserción de Windows (WNS)  

En los dispositivos de Windows administrados por Intune que se administran mediante administración de dispositivos móviles (MDM), las acciones de dispositivos y otras actividades inmediatas requieren el uso de servicios de notificaciones de inserción de Windows (WNS). Para obtener más información, consulte [Permitir el tráfico de notificaciones de Windows a través de firewalls empresariales](https://docs.microsoft.com/windows/uwp/design/shell/tiles-and-notifications/firewall-allowlist-config).  

## <a name="delivery-optimization-port-requirements"></a>Requisitos de puerto para la optimización de entrega  

### <a name="port-requirements"></a>Requisitos de puerto  

En el tráfico de punto a punto, la optimización de entrega usa 7680 para TCP/IP o 3544 para NAT transversal (si lo desea, Teredo). Para la comunicación entre servicio y cliente, utiliza HTTP o HTTPS a través del puerto 80/443.

### <a name="proxy-requirements"></a>Requisitos de proxy  

Para usar la optimización de entrega, debe permitir las solicitudes de intervalo de bytes. Para más información, vea [Requisitos de proxy para Windows Update](https://docs.microsoft.com/windows/deployment/update/windows-update-troubleshooting).

### <a name="firewall-requirements"></a>Requisitos de firewall  

Permita los nombres de host siguientes a través del firewall para admitir la optimización de entrega.
Para la comunicación entre los clientes y el servicio en la nube de la optimización de entrega:
- \*.do.dsp.mp.microsoft.com

Para los metadatos de optimización de entrega:
- \*.dl.delivery.mp.microsoft.com
- \*.emdl.ws.microsoft.com

## <a name="apple-device-network-information"></a>Información de red de dispositivos de Apple  

|Usada para|Nombre de host (dirección IP/subred)|Protocolo|Puerto|
|-----|--------|------|-------|
|Recuperación y visualización de contenido de los servidores de Apple|itunes.apple.com<br>\*.itunes.apple.com<br>\*.mzstatic.com<br>\*.phobos.apple.com<br> \*.phobos.itunes-apple.com.akadns.net |    HTTP    |      80      |
|Comunicaciones con servidores APNS|#-courier.push.apple.com<br>"#" es un número aleatorio entre 0 y 50.|    TCP     |  5223 y 443  |
|Distintas funcionalidades, como acceso a la World Wide Web, iTunes Store, App Store de macOS, iCloud, mensajería, etc. |phobos.apple.com<br>ocsp.apple.com<br>ax.itunes.apple.com<br>ax.itunes.apple.com.edgesuite.net| HTTP/HTTPS |  80 o 443   |

Para obtener más información, vea los artículos de Apple [Puertos TCP y UDP usados por los productos de software de Apple](https://support.apple.com/HT202944), [Acerca de los procesos en segundo plano de iTunes y las conexiones del host para el servidor de iTunes, iOS/iPadOS y macOS](https://support.apple.com/HT201999) y [Si tus clientes macOS e iOS/iPadOS no reciben notificaciones push de Apple](https://support.apple.com/HT203609).  

## <a name="android-port-information"></a>Información del puerto de Android

En función de cómo decida administrar los dispositivos Android, es posible que tenga que abrir los puertos de Google Android Enterprise y/o la notificación de inserción de Android. Para obtener más información sobre los métodos de administración de Android admitidos, vea la [documentación de inscripción de Android](https://docs.microsoft.com/mem/intune/enrollment/android-enroll). 

> [!NOTE]
> Como Google Mobile Services no está disponible en China, los clientes en China administrados por Intune no pueden usar características que requieran Google Mobile Services. Estas características incluyen: funciones de Google Play Protect como la atestación de dispositivos SafetyNet, la administración de aplicaciones desde Google Play Store, las funciones de Android Enterprise (consulte esta [documentación de Google](https://support.google.com/work/android/answer/6270910)). Además, la aplicación Portal de empresa de Intune para Android usa Google Mobile Services para comunicarse con el servicio Microsoft Intune. Como los servicios de Google Play no están disponible en China, algunas tareas pueden tardar hasta ocho horas en completarse. Para más información, consulte este [artículo](https://docs.microsoft.com/mem/intune/apps/manage-without-gms#limitations-of-intune-device-administrator-management-when-gms-is-unavailable).

### <a name="google-android-enterprise"></a>Google Android Enterprise 

Google proporciona documentación sobre los puertos de red y los nombres de host de destino obligatorios en la sección **Firewall** de su documento [Android Enterprise Bluebook](https://static.googleusercontent.com/media/www.android.com/en//static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf). 

### <a name="android-push-notification"></a>Notificación de inserción de Android

Intune aprovecha la Mensajería en la nube de Firebase (FCM) de Google para notificaciones de inserción a fin de desencadenar acciones e inserciones de dispositivo. Esto es necesario para el Administrador de dispositivos Android y Android Enterprise. Para obtener información sobre los requisitos de red de FCM, vea [Los puertos de FCM y el firewall](https://firebase.google.com/docs/cloud-messaging/concept-options#messaging-ports-and-your-firewall) de Google.

## <a name="endpoint-analytics"></a>Análisis de puntos de conexión

Para obtener más información sobre los puntos de conexión necesarios para al análisis de puntos de conexión, vea [Configuración de proxy para el análisis de puntos de conexión](https://docs.microsoft.com/mem/analytics/troubleshoot#bkmk_endpoints).