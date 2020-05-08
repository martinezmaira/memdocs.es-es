---
title: Paquetes de idioma
titleSuffix: Configuration Manager
description: Obtenga información sobre los idiomas admitidos que están disponibles en Configuration Manager.
ms.date: 06/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 53aa7e932e782254f63b422526b315f3ce91f397
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906169"
---
# <a name="language-packs-in-configuration-manager"></a>Paquetes de idioma en Configuration Manager

*Se aplica a: Configuration Manager (rama actual)*

Este artículo proporciona detalles técnicos sobre la compatibilidad de idiomas en Configuration Manager. Los clientes y servidores de sitio de Configuration Manager se consideran independientes del idioma. Agregue compatibilidad para los siguientes idiomas mediante la instalación de **paquetes de idioma de servidor** o **paquetes de idioma de cliente** en un sitio de administración central y en sitios primarios. Seleccione los idiomas de cliente y servidor que se admitirán en un sitio de los archivos de paquete de idioma disponibles durante el proceso de instalación del sitio.
 
Instale varios idiomas en cada sitio. Solo necesita instalar los idiomas que usa.  

- Cada sitio admite varios idiomas para las consolas de Configuration Manager.  

- Agregue compatibilidad solo para los idiomas de cliente que desea admitir mediante la instalación de paquetes de idioma de cliente individuales en cada sitio.  

Cuando se instala la compatibilidad para un idioma que coincide con los siguientes componentes:  

- El idioma para mostrar de un equipo: tanto la consola de Configuration Manager como la interfaz de usuario del cliente que se ejecuta en dicho equipo muestran información en dicho idioma.  

- La preferencia de idioma que está usando el explorador web de un equipo: las conexiones con información basada en web, incluido el catálogo de aplicaciones o los informes de SQL Server Reporting Services se mostrarán en dicho idioma.  


Cuando ejecuta el programa de instalación de Configuration Manager, descarga los archivos del paquete de idioma como parte de los archivos de requisitos previos y redistribuibles. También puede usar el [Descargador del programa de instalación](setup-downloader.md) para descargar estos archivos antes de ejecutar el programa de instalación.   



## <a name="server-languages"></a>Idiomas del servidor  

Utilice la tabla siguiente para asignar un identificador de configuración regional al idioma que desee admitir en servidores. Para obtener más información sobre los identificadores de configuración regional, vea [Locale IDs assigned by Microsoft (Identificadores de configuración regional asignados por Microsoft)](https://docs.microsoft.com/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).  

|Idioma del servidor|Identificador de configuración regional (LCID)|Código de tres letras|  
|---------------------|------------------------|-----------------------|  
|Inglés (predeterminado)|0409|ENU|  
|Chino (simplificado)|0804|CHS|  
|Chino (tradicional, Taiwán)|0404|CHT|  
|Checo|0405|CSY|  
|Neerlandés - Países Bajos|0413|NLD|  
|Francés|040c|FRA|  
|Alemán|0407|DEU|  
|Húngaro|040e|HUN|  
|Italiano - Italia|0410|ITA|  
|Japonés|0411|JPN|  
|Coreano|0412|KOR|  
|Polaco|0415|PLK|  
|Portugués - Brasil|0416|PTB|  
|Portugués - Portugal|0816|PTG|  
|Ruso|0419|RUS|  
|Español - España|0c0a|ESN|  
|Sueco|041d|SVE|  
|Turco|041f|TRK|  



## <a name="client-languages"></a>Idiomas del cliente  

Utilice la tabla siguiente para asignar un identificador de configuración regional al idioma que desee admitir en equipos cliente. Para obtener más información sobre los identificadores de configuración regional, vea [Locale IDs assigned by Microsoft (Identificadores de configuración regional asignados por Microsoft)](https://docs.microsoft.com/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).  

|Idioma del cliente|Identificador de configuración regional (LCID)|Código de tres letras|  
|---------------------|------------------------|-----------------------|  
|Inglés (predeterminado)|0409|ESN|  
|Chino - Simplificado|0804|CHS|  
|Chino (tradicional, Taiwán)|0404|CHT|  
|Checo|0405|CSY|  
|Danés|0406|DAN|  
|Neerlandés - Países Bajos|0413|NLD|  
|Finés|040b|FIN|  
|Francés|040c|FRA|  
|Alemán|0407|DEU|  
|Griego|0408|ELL|  
|Húngaro|040e|HUN|  
|Italiano - Italia|0410|ITA|  
|Japonés|0411|JPN|  
|Coreano|0412|KOR|  
|Noruego|0414|NOR|  
|Polaco|0415|PLK|  
|Portugués (Brasil)|0416|PTB|  
|Portugués (Portugal)|0816|PTG|  
|Ruso|0419|RUS|  
|Español - España|0c0a|ESN|  
|Sueco|041d|SVE|  
|Turco|041f|TRK|  


### <a name="mobile-device-client-languages"></a>Idiomas del cliente de dispositivos móviles  
Cuando agrega compatibilidad con idiomas de dispositivo móvil, se incluyen todos los idiomas de cliente de dispositivo móvil compatibles. No puede seleccionar paquetes de idioma individuales para la compatibilidad con dispositivos móviles.  



## <a name="identify-installed-language-packs"></a>Identificación de los paquetes de idioma instalados  
Para identificar los paquetes de idioma instalados en un equipo que ejecuta el cliente de Configuration Manager, busque el identificador de configuración regional (LCID) de los paquetes de idioma instalados en el Registro del equipo. Esta información está disponible en la siguiente ruta de acceso al registro:  

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs`  

Personalice el inventario de hardware para recopilar esta información. Después, compile un informe personalizado para ver los detalles del idioma. Para más información sobre cómo recopilar el inventario de hardware personalizado, vea [Cómo configurar el inventario de hardware](../../../clients/manage/inventory/configure-hardware-inventory.md). Para más información, vea [Creación de informes](../../manage/operations-and-maintenance-for-reporting.md#create-reports).
