---
title: Seguridad y privacidad de las actualizaciones de software
titleSuffix: Configuration Manager
description: Siga estos procedimientos recomendados de seguridad de las actualizaciones de software y obtenga información sobre cómo administra Configuration Manager la información de privacidad.
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 41d6d5d8-ba84-4efb-b105-4d1eed239824
author: mestew
ms.author: mstewart
ms.openlocfilehash: 5c7a1ac5e88aa669ae1d5e6bb9333e1f54fb5980
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708733"
---
# <a name="security-and-privacy-for-software-updates-in-configuration-manager"></a>Seguridad y privacidad para las actualizaciones de software en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Este tema contiene información sobre la seguridad y privacidad de las actualizaciones de software en Configuration Manager.  

##  <a name="security-best-practices-for-software-updates"></a><a name="BKMK_Security_HardwareInventory"></a> Recomendaciones de seguridad para las actualizaciones de software  
 Use las recomendaciones de seguridad siguientes al implementar actualizaciones de software en los clientes:  

-   No cambie los permisos predeterminados de los paquetes de actualización de software.  

     De manera predeterminada, los paquetes de actualización de software están configurados para permitir que los administradores tengan **Control total** y que los usuarios tengan **Acceso de lectura** . Si cambia estos permisos, los atacantes podrían agregar, quitar o eliminar actualizaciones de software.  

-   Controle el acceso a la ubicación de descarga de actualizaciones de software.  

     Las cuentas de equipo del proveedor de SMS, el servidor de sitio y el usuario administrativo que descargará las actualizaciones de software en la ubicación de descarga requieren **Acceso de escritura** en la misma. Limite el acceso a la ubicación de descarga para reducir el riesgo de que los atacantes alteren los archivos de origen de las actualizaciones de software en la misma.  

     Además, si usa un recurso compartido UNC como ubicación de descarga, proteja el canal de red mediante la firma SMB o IPsec para impedir las alteraciones de los archivos de origen de las actualizaciones de software durante su transferencia a través de la red.  

-   Use UTC para evaluar las horas de implementación.  

     Si usa la hora local en vez de UTC, los usuarios podrían retrasar la instalación de actualizaciones de software mediante el cambio de la zona horaria en sus equipos.  

-   Habilite SSL en WSUS y siga las recomendaciones de seguridad para proteger Windows Server Update Services (WSUS).  

     Identifique y siga los procedimientos recomendados de seguridad para la versión de WSUS que usa con Configuration Manager.  

    > [!IMPORTANT]  
    >  Si configura el punto de actualización de software para habilitar las comunicaciones SSL para el servidor WSUS, debe configurar las raíces virtuales para SSL en el servidor WSUS.  

-   Habilite la comprobación de CRL.  

     De manera predeterminada, Configuration Manager no comprueba la lista de revocación de certificados (CRL) para comprobar la firma en las actualizaciones de software antes de implementarlas en los equipos. La comprobación de CRL cada vez que se usa un certificado proporciona una mayor seguridad frente a certificados revocados, pero incorpora un retraso en la conexión e implica un procesamiento adicional en el equipo que realiza la comprobación de CRL.  

     Para más información sobre cómo habilitar la comprobación de la CRL para actualizaciones de software, consulte [Cómo habilitar la comprobación de CRL para actualizaciones de software](../get-started/manage-settings-for-software-updates.md#crl-checking-for-software-updates).  

-   Configure WSUS para usar un sitio web personalizado.  

     Cuando instale WSUS en el punto de actualización de software, tendrá la opción de usar el sitio web predeterminado de IIS existente o crear un sitio web WSUS personalizado. Cree un sitio web personalizado para WSUS para que IIS hospede los servicios WSUS en un sitio web virtual dedicado en vez de compartir el sitio web que también usan otros sistemas de sitio de Configuration Manager u otras aplicaciones.  

     Para obtener más información, consulte [Configurar WSUS para usar un sitio web personalizado](plan-for-software-updates.md#BKMK_CustomWebSite).  

##  <a name="privacy-information-for-software-updates"></a><a name="BKMK_Privacy_HardwareInventory"></a> Información de privacidad de las actualizaciones de software  
 Las actualizaciones de software examinan los equipos cliente para determinar las actualizaciones de software requeridas y, a continuación, envían la información a la base de datos del sitio. Durante el proceso de actualización de software, es posible que Configuration Manager transmita información entre clientes y servidores que permite identificar las cuentas de equipo y de inicio de sesión.  

 Configuration Manager mantiene información de estado sobre el proceso de implementación de software. La información de estado no se cifra durante la transmisión o el almacenamiento. La información de estado se almacena en la base de datos de Configuration Manager. Las tareas de mantenimiento de la base de datos eliminarán la información de estado. No se envía información de estado a Microsoft.  

 El uso de las actualizaciones de software de Configuration Manager para instalar actualizaciones de software en equipos cliente puede estar sujeto a los términos de licencias de software de esas actualizaciones, ya que son independientes de los términos de licencia del software de Configuration Manager. Revise y acepte los términos de licencia del software antes de instalar las actualizaciones de software mediante Configuration Manager.  

 Configuration Manager no implementa actualizaciones de software de manera predeterminada y requiere varios pasos de configuración antes de recopilar información.  

 Antes de configurar las actualizaciones de software, tenga en cuenta los requisitos de privacidad.  
