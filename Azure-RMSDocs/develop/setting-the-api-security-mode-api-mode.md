---
title: Cómo establecer el modo de seguridad de API | Azure RMS
description: Elija el modo de seguridad que ejecuta la aplicación de la API de archivo.
keywords: ''
author: bryanla
ms.author: bryanla
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 3B088F14-81C5-4C78-8DED-F5F153353EE0
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 5f74099dec06ea120dd5f5e212b736e8cd3b0fba
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56251796"
---
# <a name="how-to-set-the-api-security-mode"></a>Establecimiento del modo de seguridad de API

Puede elegir el modo de seguridad en que se ejecuta la aplicación de la API de archivo con la función [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx).

Para iniciar la aplicación y ejecutarla en *modo servidor*, llame a la función [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx) y establezca el modo de seguridad en [IPC\_API\_MODE\_SERVER](https://msdn.microsoft.com/library/hh535236.aspx). De forma predeterminada, la aplicación se ejecutará en *modo cliente*, **IPC\_API\_MODE\_CLIENT**.

Para más información sobre el *modo servidor*, consulte [Tipos de aplicación](application-types.md).

**Importante**  El modo de seguridad debe establecerse antes de que se llame a cualquier otra función de Rights Management Services SDK 2.1. Una vez establecido el modo de seguridad, no podrá cambiarse para el proceso en vigor.

## <a name="related-topics"></a>Temas relacionados

* [Tipos de aplicación](application-types.md)
* [Valores del modo de API](https://msdn.microsoft.com/library/hh535236.aspx)
* [IpcSetGlobalProperty](https://msdn.microsoft.com/library/hh535270.aspx)
