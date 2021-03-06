---
title: Modo de solo protección para Azure Information Protection
description: Información para los usuarios que ejecutan el cliente de Azure Information Protection en modo de solo protección.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 01/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 16042717-0d7a-41f5-87e3-12826fda35df
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 57bcea5841823cf5ae15681d247966346b14c1d2
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56253768"
---
# <a name="user-guide-protection-only-mode-for-the-azure-information-protection-client"></a>Manual del usuario: Modo de solo protección para el cliente de Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*


Cuando el cliente de Azure Information Protection no tiene etiquetas para clasificar los documentos y correos electrónicos, se ejecuta en modo **solo protección**. Por ejemplo, en este modo, podría ver lo siguiente si utiliza el Explorador de archivos de Windows y hace clic con el botón derecho en **Clasificar y proteger**:

![Modo de solo protección](../media/protection-only-mode.png)

El modo de solo protección se ejecuta en los siguientes escenarios:

- La organización no tiene una suscripción para Azure Information Protection que incluya características de clasificación y etiquetado, pero tiene una suscripción para Office 365 que incluye protección de datos mediante el uso del servicio Azure Rights Management. 
    
    - Puede utilizar el cliente de Azure Information Protection para proteger archivos y ver archivos protegidos. No se pueden clasificar o etiquetar documentos ni correos electrónicos.

- Su organización tiene una suscripción para Azure Information Protection para solo un subconjunto de usuarios:
    
    - Para esta combinación de suscripciones, el administrador es el responsable de asegurarse de que solo el subconjunto de usuarios puede usar las características de clasificación y etiquetado. El resto de usuarios debe ejecutar el cliente de Azure Information Protection en modo de solo protección. 

- Su organización tiene una suscripción de Azure Information Protection pero no tiene ninguna etiqueta configurada para usted.
    
    - Esto puede ocurrir cuando todas las etiquetas en la directiva global están deshabilitadas y su cuenta no está incluida en una directiva con ámbito. Esto podría deberse a que el departamento de TI ha comenzado a implementar Azure Information Protection, pero aún no se le han suministrado etiquetas para clasificar los documentos y correos electrónicos. Entretanto, puede usar el cliente de Azure Information Protection para proteger archivos y ver los archivos protegidos.

- La organización tiene una suscripción para Azure Information Protection, pero no puede descargar la directiva de Azure Information Protection. 
    
    - Esto puede suceder debido a una configuración incorrecta o porque el inicio de sesión no es correcto. Póngase en contacto con el Servicio de asistencia o el administrador, pero, mientras tanto, puede usar el cliente de Azure Information Protection para proteger archivos y ver los archivos protegidos.

- La organización solo usa Active Directory Rights Management Services (AD RMS). 


## <a name="limitations-for-protection-only-mode"></a>Limitaciones para el modo de solo protección

- En las aplicaciones de Office, no se muestra la barra de Azure Information Protection. Al hacer clic en **Proteger** > **Mostrar barra**, esta opción de menú no está disponible.

- Cuando se usa el cuadro de diálogo **Clasificar y proteger: Azure Information Protection** con el Explorador de archivos, no ve las etiquetas de clasificación. En su lugar, como se muestra en la imagen anterior, verá una opción para seleccionar plantillas de Rights Management (RMS). 

## <a name="supported-tasks-for-protection-only-mode"></a>Tareas admitidas para el modo de solo protección

- Proteger (y desproteger) documentos y correos electrónicos desde aplicaciones de Office mediante la característica Information Rights Management (IRM) de Office. Por ejemplo: haga clic en **Archivo** > **Información** > **Proteger documento** > **Restringir acceso**. Para más información, vea [Uso de protección de la información con Office 365, Office 2019, Office 2016 u Office 2013](../help-users.md#using-information-protection-with-Office-365-Office 2019-Office-2016-or-Office-2013).

- Proteger (y desproteger) archivos mediante el Explorador de archivos de Windows: Haga clic con el botón derecho en el archivo, los archivos o la carpeta y seleccione **Clasificar y proteger**. Para aplicar la protección que ha configurado el administrador, en el cuadro de diálogo **Clasificar y proteger: Azure Information Protection**, haga clic en **Seleccionar plantilla** y elija una de las plantillas disponibles.

- Ver los archivos protegidos mediante el visor de Azure Information Protection.

- Acceder al sitio de Seguimiento de documentos desde las aplicaciones de Office. Sin embargo, debe tener una suscripción válida para realizar un seguimiento de los documentos y revocarlos desde este sitio.
  
