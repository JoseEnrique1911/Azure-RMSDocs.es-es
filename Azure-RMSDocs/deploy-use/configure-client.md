---
title: "Cliente de Azure Information Protection&colon; instalación y configuración"
description: "Información para administradores sobre la implementación del cliente de Azure Information Protection en dispositivos móviles y equipos con Windows."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b1a19ae7-db26-40da-9e21-6620af3d0b02
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 9164ce8155f1d068ea0fa164226ff20df05da8ae
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="azure-information-protection-client-installation-and-configuration-for-clients"></a>Cliente de Azure Information Protection: instalación y configuración de clientes

>*Se aplica a: Azure Information Protection, Office 365*

Los equipos que ejecutan Office 2010 requieren el cliente de Azure Information Protection (o la aplicación Rights Management sharing) para autenticarse en el servicio Azure Rights Management y en el servicio Azure Information Protection. Este cliente también se recomienda para todos los equipos con Windows y dispositivos iOS y Android que admiten el servicio Azure Rights Management y Azure Information Protection. 

El cliente de Azure Information Protection se integra con aplicaciones de Office mediante la instalación de un complemento de Office para que los usuarios puedan etiquetar y proteger fácilmente documentos y correos electrónicos directamente desde la cinta de opciones de Office. Este cliente también ofrece etiquetado y protección para tipos de archivo que no son compatibles de forma nativa con el servicio Azure Rights Management, un visor de archivos protegidos y un sitio de seguimiento de documentos para que los usuarios controlen y revoquen los archivos que hayan protegido.

## <a name="the-azure-information-protection-client-for-windows-installation-and-configuration"></a>El cliente de Azure Information Protection para Windows: instalación y configuración
Para una instalación empresarial y la configuración del cliente para Windows, vea [Azure Information Protection administrator guide](../rms-client/client-admin-guide.md) (Guía para administradores de Azure Information Protection).

> [!TIP]
> Si desea instalar y probar rápidamente el cliente de Azure Information Protection en un solo equipo, vea [Descarga e instalación del cliente de Azure Information Protection](../rms-client/install-client-app.md) de la [Guía del usuario de Azure Information Protection](../rms-client/client-user-guide.md).

## <a name="the-azure-information-protection-client-for-ios-and-android-installation-and-management"></a>El cliente de Azure Information Protection para iOS y Android: instalación y configuración
Para instalar el cliente de Azure Information Protection en estas plataformas móviles populares, puede descargar la aplicación correspondiente con los vínculos de la [página de Microsoft Azure Information Protection](http://go.microsoft.com/fwlink/?LinkId=303970). No es necesario realizar ninguna configuración.

> [!NOTE]
> Para equipos Mac y Windows Phone, los vínculos de esta página descargan las aplicaciones RMS sharing para dispositivos móviles. Estos dispositivos no admiten actualmente el cliente de Azure Information Protection.

**Si tiene Microsoft Intune**: como la aplicación Azure Information Protection incluye el Kit de desarrollo de software de aplicaciones de Microsoft Intune, cuando los dispositivos iOS y Android están inscritos mediante Intune, puede implementar y administrar el visor de Azure Information Protection para estos dispositivos. Para más información, consulte [Configure and deploy mobile application management policies in the Microsoft Intune console](/intune/deploy-use/configure-and-deploy-mobile-application-management-policies-in-the-microsoft-intune-console) (Configuración e implementación de directivas de administración de aplicaciones móviles en la consola de Microsoft Intune). Para el paso 2, siga las instrucciones para publicar una aplicación administrada por directivas.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

