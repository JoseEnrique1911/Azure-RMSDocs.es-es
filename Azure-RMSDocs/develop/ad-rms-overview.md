---
title: Información general - RMS SDK 2.1 | Azure RMS
description: Rights Management Services (RMS) es una tecnología de protección de la información que ayuda a proteger la información digital frente al uso no autorizado.
keywords: ''
author: bryanla
ms.author: bryanla
manager: barbkess
ms.date: 02/23/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: B546B6C1-ADC1-4EBD-95E2-B4A74E4E980B
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 692884c675115b8200df2ac9c9ca5c6d2abf30af
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56251155"
---
# <a name="overview"></a>Introducción

Rights Management Services SDK 2.1 es una tecnología de protección de la información que ayuda a proteger la información digital frente al uso no autorizado. Con aplicaciones habilitadas para derechos, los propietarios de contenido tendrán la capacidad de definir quién puede abrir, modificar, imprimir, reenviar o realizar otras acciones con su contenido.

AD RMS consta de componentes de [servidor](ad-rms-server.md) y [cliente](ad-rms-client.md). El servidor, que se ejecuta en Azure o en Windows Server, consta de varios servicios web.

El componente de [cliente](ad-rms-client.md) se puede ejecutar en un cliente o un sistema operativo de servidor y contiene funciones que permiten que una aplicación cifre y descifre el contenido, recupere plantillas y listas de revocación, adquiera licencias y certificados de un servidor y otras tareas de administración de derechos relacionadas.

Para más información, vea [Application types](application-types.md) (Tipos de aplicación).

Estos son algunos de los escenarios en los que se pueden aplicar las aplicaciones basadas en Rights Management Services SDK 2.1.

-   Un bufete de abogados desea evitar que los mensajes de correo electrónico confidenciales se impriman o reenvíen.
-   Los desarrolladores de un software de fabricación y diseño asistido por ordenador desean limitar el acceso con capacidad de dibujo a un pequeño grupo de usuarios pertenecientes a la división de investigación y sin necesidad de usar contraseñas.
-   Los propietarios de un sitio web de diseño gráfico desean usar una única licencia que permita la visualización gratuita de copias de baja resolución de sus imágenes, pero que requiera un pago para tener acceso a las versiones de alta resolución.
-   Los propietarios de una biblioteca de documentos en línea desean habilitar derechos para ver, imprimir o editar documentos basados en la identidad del usuario.
-   Una gran compañía desea publicar información confidencial de sus empleados en un sitio web interno con limitación de los privilegios de visualización y edición a determinados usuarios.

Para más información sobre el servidor de AD RMS, el cliente de AD RMS y su funcionalidad, consulte el contenido de TechNet para [Documentación para profesionales de TI para AD RMS](https://TechNet.Microsoft.Com/library/cc771234.aspx).

Los demás temas de esta sección tratan sobre la arquitectura de RMS y sus implementaciones.

## <a name="in-this-section"></a>En esta sección

| Tema | Descripción |
|-------|-------------|
|[Cliente](ad-rms-client.md) |En este tema se describe el propósito y la función del cliente de Rights Management Services 2.1. |
|[Servidor](ad-rms-server.md) | En este tema se describe el propósito y las funciones del servidor RMS para Azure y Windows Server.|


## <a name="related-topics"></a>Temas relacionados

* [Conceptos de RMS](application-types.md)
* [Introducción](getting-started-with-ad-rms-2-0.md)
* [Documentación para profesionales de TI para AD RMS](https://technet.microsoft.com/library/cc771234.aspx)
