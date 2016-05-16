---
# required metadata

title: Eliminación de la protección de un archivo mediante la aplicación Rights Management sharing | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: da95b938-eaad-4c83-a21e-ff1d4872aae4

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Quitar la protección de un archivo mediante la aplicación Rights Management sharing
Para quitar la protección (es decir, desproteger) de un archivo protegido anteriormente con la aplicación de RMS sharing, use la opción **Quitar protección** en el Explorador de archivos.

> [!IMPORTANT]
> Debe ser propietario del archivo para quitar la protección.

## Para quitar la protección de un archivo

1.  En el Explorador de archivos, haga clic con el botón derecho en el archivo (por ejemplo, Sample.ptxt), seleccione **Proteger con RMS**, haga clic en **Proteger en contexto** y, luego, en **Quitar protección**:

    ![](../media/ADRMS_MSRMSApp_RemoveProtection.png)

    Puede que se le soliciten las credenciales.

Nota: Si no ve estas opciones, es probable que la aplicación RMS sharing no esté instalada en el equipo, que no esté instalada la última versión o que el equipo deba reiniciarse para completar la instalación. Para más información sobre cómo instalar la aplicación de uso compartido, consulte [Descarga e instalación de la aplicación Rights Management sharing](install-sharing-app.md).

El archivo protegido original se elimina (por ejemplo, Sample.ptxt) y se reemplaza con un archivo que tiene el mismo nombre pero la extensión de nombre de archivo desprotegido (por ejemplo, Sample.txt).

## Ejemplos y otras instrucciones
Para obtener ejemplos de cómo puede usar la aplicación para uso compartido de Rights Management e instrucciones de procedimientos, consulte las siguientes secciones de la guía de usuario de la aplicación para uso compartido de Rights Management:

-   [Ejemplos de uso de la aplicación RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [¿Qué desea hacer?](sharing-app-user-guide.md##what-do-you-want-to-do-)

## Véase también
[Guía de usuario de la aplicación de uso compartido Rights Management](sharing-app-user-guide.md)



<!--HONumber=Apr16_HO3-->

