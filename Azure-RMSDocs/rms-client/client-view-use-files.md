---
title: Visualización y uso de documentos protegidos con el cliente AIP
description: Instrucciones para ver y usar un documento protegido que requiere tener instalado el cliente de Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 12/12/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ce1c7d4c-b5ff-4672-8b9a-a72129bac992
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 728a0d8439f9450384d0861504f09679cd59a40f
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56255027"
---
# <a name="user-guide-view-and-use-files-that-have-been-protected-by-rights-management"></a>Manual del usuario: Ver y usar los archivos protegidos por Rights Management

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

A menudo, puede ver un documento protegido con tan solo abrirlo. Por ejemplo, podría hacer doble clic en los datos adjuntos de un mensaje de correo electrónico o en un archivo del Explorador de archivos, o podría hacer clic en un vínculo a un archivo.

Si los archivos no se abren automáticamente, es posible que el **Visor de Azure Information Protection** pueda abrirlo. Este visor puede abrir archivos de texto protegidos, archivos de imagen protegidos, archivos PDF protegidos y todos los archivos con una extensión de nombre de archivo **.pfile**.

El visor se instala automáticamente como parte del cliente de Azure Information Protection o puede instalarlo por separado. Puede instalar el cliente y el visor desde la página [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) en el sitio web de Microsoft. Para más información sobre cómo instalar el cliente, vea [Descarga e instalación del cliente de Azure Information Protection](install-client-app.md).

> [!NOTE]
> Aunque la instalación del cliente proporciona más funcionalidad, requiere permisos de administrador local y la funcionalidad completa requiere un servicio correspondiente para la organización. Por ejemplo, Azure Information Protection o Active Directory Rights Management Services.
> 
> Instale el visor si alguien de otra organización le ha enviado un documento protegido o si no tiene permisos de administrador local para el equipo.

Para poder abrir un documento protegido, la aplicación debe estar "habilitada para RMS". Las aplicaciones de Office y el visor de Azure Information Protection son ejemplos de aplicaciones habilitadas para RMS. Para ver una lista de aplicaciones por tipo y dispositivos compatibles, consulte la tabla de [aplicaciones habilitadas para RMS](../requirements-applications.md#rms-enlightened-applications).  
## <a name="messagerpmsg-as-an-email-attachment"></a>Message.rpmsg como datos adjuntos de correo electrónico

Si ve **message.rpmsg** como un archivo adjunto en un correo electrónico, no se trata de un documento protegido sino un mensaje de correo electrónico protegido que se muestra como archivo adjunto. No puede usar el visor de Azure Information Protection para Windows para ver este mensaje de correo electrónico protegido en el equipo Windows. En su lugar, necesita una aplicación de correo electrónico para Windows compatible con la protección de Rights Management, como Office Outlook. También puede usar Outlook en la Web.

Sin embargo, si tiene un dispositivo iOS o Android, puede usar la aplicación Azure Information Protection para abrir estos mensajes de correo electrónico protegidos. Puede descargar esta aplicación para estos dispositivos móviles desde la página [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) en el sitio web de Microsoft.

## <a name="prompts-for-authentication"></a>Solicitudes de autenticación

Para poder ver el archivo protegido, el servicio Rights Management utilizado para proteger el archivo primero debe confirmar que está autorizado para ver el archivo. El servicio realiza esta confirmación comprobando el nombre de usuario y la contraseña. En algunos casos, es posible que estas credenciales estén almacenadas en la caché y no vea ningún mensaje en el que se le pida que inicie sesión. En otros, se le pedirá que proporcione las credenciales.

Si la organización no tiene una cuenta en la nube para que pueda usarla (para Office 365 o Azure) y no usa una versión local equivalente (AD RMS), tiene dos opciones:

- Si recibe un correo protegido, siga las instrucciones para iniciar sesión con su proveedor de identidades sociales (como Google para una cuenta de Gmail) o solicitar un código de acceso de un solo uso.

- Puede solicitar una cuenta gratuita que aceptará las credenciales para que pueda abrir documentos que estén protegidos por Rights Management. Para solicitar esta cuenta, haga clic en el vínculo para solicitar [RMS para usuarios](https://go.microsoft.com/fwlink/?LinkId=309469) y use la dirección de correo de su empresa en lugar de una dirección de correo personal. 

## <a name="to-view-and-use-a-protected-document"></a>Para ver y usar un documento protegido

1. Abra el archivo protegido (por ejemplo, al haciendo doble clic en el archivo o los datos adjuntos o haciendo clic en el vínculo al archivo). Si se le pide que seleccione una aplicación, seleccione **Visor de Azure Information Protection**. 

2. Si ve una página para **Iniciar sesión** o **Registrarse**: Haga clic en **Iniciar sesión** y escriba sus credenciales. Si el archivo protegido se le envió como datos adjuntos, asegúrese de especificar la misma dirección de correo electrónico que la usada para enviar el archivo.
    
    Si no tiene una cuenta aceptable, vea la sección [Solicitudes de autenticación](#prompts-for-authentication) de esta página.

3. Se abre una versión de solo lectura del archivo en **Azure Information Protection Viewer**. Si tiene permisos suficientes, puede imprimir el archivo y modificarlo. 

    Puede comprobar los permisos del archivo haciendo clic en **Permisos**. En el cuadro de diálogo **Permisos**, también puede identificar el propietario del archivo al que acudir si quiere solicitar una nueva versión del archivo con permisos adicionales.
    
    Para más información sobre los permisos y los derechos de uso que contiene cada uno, consulte los [derechos incluidos en niveles de permisos](../configure-usage-rights.md#rights-included-in-permissions-levels).

4. Para editar el archivo, haga clic en **Guardar como**. Se guardará el archivo protegido con su extensión de nombre de archivo original. Luego puede editar el archivo mediante la aplicación que está asociada a ese tipo de archivo. En este momento, se quita la protección y la etiqueta del archivo.
    
    Tenga en cuenta que dado que el visor es para archivos protegidos, el botón **Guardar como** está habilitado solo para archivos protegidos.
    
5. Cuando haya terminado de editar el archivo, en el Explorador de archivos, haga clic con el botón derecho en el archivo para volver a aplicar la etiqueta. Con esta acción se vuelve a aplicar la protección.

6. Si tiene archivos protegidos adicionales para abrir, puede ir directamente a ellos desde el visor, mediante la opción **Abrir**. El archivo seleccionado reemplaza al archivo original en el visor. 

> [!TIP]
> Si el archivo protegido no se abre y tiene instalado el cliente de Azure Information Protection completo, pruebe la opción **Restablecer configuración**. Para obtener acceso a esta opción, desde una aplicación de Office, haga clic en el botón **Proteger** > **Ayuda y comentarios** > **Restablecer configuración**. 
> 
> [Más información sobre la opción Restablecer configuración](client-admin-guide.md#more-information-about-the-reset-settings-option)

## <a name="other-instructions"></a>Otras instrucciones
Puede encontrar más instrucciones sobre procedimientos en la guía del usuario de Azure Information Protection:

-   [¿Qué desea hacer?](client-user-guide.md#what-do-you-want-to-do)

