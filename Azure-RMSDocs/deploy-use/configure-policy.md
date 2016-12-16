---
title: "Configuración de la directiva | Azure Information Protection"
description: "Para configurar la protección, la clasificación y el etiquetado, debe configurar la directiva de Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ba0e8119-886c-4830-bd26-f98fb14b2933
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5d1a5e3b85d5450bcb2064a6c3b95e6ad802eea3
ms.openlocfilehash: 808f72be7c5b6a1f18a06ecefdfdf7fbf6febff6


---

# <a name="configuring-azure-information-protection-policy"></a>Configuración de la directiva de Azure Information Protection

>*Se aplica a: Azure Information Protection*

Para configurar la protección, la clasificación y el etiquetado, debe configurar la directiva de Azure Information Protection. Esta directiva se descarga luego en los equipos que tienen instalado el [cliente de Azure Information Protection](https://www.microsoft.com/en-us/download/details.aspx?id=53018).

Para configurar la directiva de Azure Information Protection:

1. En una nueva ventana del explorador, inicie sesión en [Azure Portal](https://portal.azure.com) como administrador global.

2. Vaya a la hoja **Azure Information Protection**: por ejemplo, en el menú del centro, haga clic en **Más servicios** y comience a escribir **Information Protection** en el cuadro Filtro. De los resultados, seleccione **Azure Information Protection**. 

    Luego verá la hoja **Azure Information Protection**, que abre automáticamente la hoja de la directiva global de Information Protection que obtienen todos los usuarios. Contiene los siguientes elementos que puede configurar:

    - Etiquetas que permiten a los usuarios clasificar documentos y correos electrónicos.

    - Título e información sobre herramientas de la barra de Information Protection que ven los usuarios en sus aplicaciones de Office.

    - La opción para exigir clasificación cuando los usuarios guarden documentos y envíen correos electrónicos.

    - La opción para establecer una etiqueta predeterminada como punto de partida para clasificar documentos y correos electrónicos.

    - La opción para pedir a los usuarios que proporcionen un motivo cuando seleccionen una etiqueta con un nivel de confidencialidad inferior al original.

    - La opción para proporcionar un vínculo de ayuda personalizado para los usuarios.

Azure Information Protection viene con una [directiva predeterminada](configure-policy-default.md), que contiene las etiquetas **Personal**, **Público**, **Interno**, **Confidencial** y **Secreto**. Puede utilizar las etiquetas predeterminadas sin cambios, o puede personalizarlas. También puede eliminarlas y crear otras nuevas.

Cuando realice cambios en una hoja de Azure Information Protection, haga clic en **Guardar** para guardar los cambios o en **Descartar** para volver a la última configuración guardada. 

Cuando haya terminado de realizar los cambios que desee, haga clic en **Publicar**. 

El cliente de Azure Information Protection busca cambios cada vez que se inicia una aplicación de Office compatible y descarga los cambios en su directiva de Azure Information Protection.

## <a name="configuring-your-organizations-policy"></a>Configuración de la directiva de la organización

Use la siguiente información como ayuda para configurar la directiva de Azure Information Protection:

- [Directiva predeterminada de Azure Information Protection](configure-policy-default.md)

- [Configuración de directivas](configure-policy-settings.md)

- [Creación de una nueva etiqueta](configure-policy-new-label.md)

- [Eliminación o cambio de orden de una etiqueta](configure-policy-delete-reorder.md)

- [Cambio o personalización de una etiqueta existente](configure-policy-change-label.md)

- [Configuración de una etiqueta para aplicar protección](configure-policy-protection.md)

- [Configuración de una etiqueta para marcas visuales](configure-policy-markings.md)

- [Configuración de las condiciones para la clasificación automática y recomendada](configure-policy-classification.md)

- [Configuración de la directiva para usuarios específicos mediante directivas de ámbito](configure-policy-scope.md)

## <a name="next-steps"></a>Pasos siguientes

Para ver un ejemplo de cómo personalizar la directiva predeterminada y ver el comportamiento resultante en una aplicación de Office, pruebe el [tutorial de inicio rápido de Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).




<!--HONumber=Dec16_HO1-->

