---
title: XML de configuración del complemento
titleSuffix: Configuration Manager
description: Referencia técnica de los elementos XML del complemento del Administrador de conversión de paquetes.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 940cc075-4066-44d5-972a-927c0b0a1143
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9178b595ba67723c623979b4c29290e42fe5f6ac
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/27/2020
ms.locfileid: "83877744"
---
# <a name="technical-reference-for-the-package-conversion-manager-plug-in-configuration-xml"></a>Referencia técnica del XML de configuración del complemento del Administrador de conversión de paquetes

*Se aplica a: Configuration Manager (rama actual)*

<!--1357861-->

En este artículo se describen los elementos XML del archivo de configuración de Configuration Manager (Microsoft.ConfigurationManagement.exe.config) que controlan el funcionamiento del complemento del Administrador de conversión de paquetes. Para más información sobre cómo usar este complemento, vea [Cómo usar el complemento del Administrador de conversión de paquetes](how-to-use-plug-in.md).



## <a name="xml-configuration-elements"></a>Elementos de configuración XML

En la tabla siguiente se describen los elementos XML del archivo de configuración de Configuration Manager relacionados con el complemento del Administrador de conversión de paquetes.

|Elemento  |Tipo  |Descripción  |
|---------|---------|---------|
|**PcmPlugIn**|String|El nombre del script o archivo ejecutable que se usará como el complemento del Administrador de conversión de paquetes.|
|**PcmPlugInTimeoutMilliseconds**|Integer|La cantidad máxima de tiempo, en milisegundos, que debe esperar el script o ejecutable del complemento del Administrador de conversión de paquetes para completar el procesamiento de un paquete.|
|**PcmPluginExitCode**|Integer|Código de salida esperado del proceso del complemento. Este valor indica que la operación se ha realizado correctamente. Los demás códigos se consideran un error.|
|**ForceRequirementsExtraction**|Boolean|Permitir la conversión automática para usar los requisitos de la colección asociados a un paquete. Esto solo debe establecerse en True cuando se trabaja con un complemento del Administrador de conversión de paquetes que está diseñado para tomar decisiones sobre los requisitos para usar.|



## <a name="sample-configuration-xml"></a>XML de configuración de ejemplo

En esta sección se proporciona un ejemplo de los elementos XML de configuración del Administrador de conversión de paquetes, en el archivo de configuración de Configuration Manager, **Microsoft.ConfigurationManagement.exe.config**. De forma predeterminada, este archivo está en la ruta de acceso siguiente:  
`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

> [!IMPORTANT]
> A partir de la versión 1910, esta ruta de acceso cambió para usar la carpeta `Microsoft Endpoint Manager`. Asegúrese de que no usa una versión anterior del archivo que pudiera existir en otra carpeta. 

En el ejemplo, los elementos relacionados con el Administrador de conversión de paquetes están dentro del siguiente elemento: `Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings`

``` XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
...
    </Microsoft.ConfigurationManagement.AdminConsole.Properties.Settings>
    <Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
      <setting name="DecisionVerbosity" serializeAs="String">
        <value>2</value>
      </setting>
      <setting name="PcmPlugIn" serializeAs="String">
        <value>pcmplugin.vbs</value>
      </setting>
      <setting name="PcmPlugInTimeoutMilliseconds" serializeAs="String">
        <value>10000</value>
      </setting>
      <setting name="PcmPluginExitCode" serializeAs="String">
        <value>0</value>
      </setting>
      <setting name="ForceRequirementsExtraction" serializeAs="String">
        <value>True</value >
      </setting>
    </Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
  </applicationSettings>
...
```

