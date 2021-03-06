---
title: 'Requisitos de Azure AD para Azure Information Protection: AIP'
description: Identifique los requisitos de Azure AD para usar Azure Information Protection de forma que los usuarios se puedan autenticar correctamente.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: ed25aa83-e272-437b-b445-3f01e985860c
ms.suite: ems
ms.openlocfilehash: 7be53f80e3de227ee2439121bc6733661274f3e1
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56258477"
---
# <a name="azure-active-directory-requirements-for-azure-information-protection"></a>Requisitos de Azure Active Directory para Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Para poder usar Azure Information Protection, se necesita un directorio de Azure AD. Se use una cuenta de este directorio para poder iniciar sesión en Azure Portal, en donde, por ejemplo, se pueden configurar y administrar las etiquetas de Azure Information Protection y las plantillas de Azure Rights Management.

Si tiene una suscripción que incluye Azure Information Protection o Azure Rights Management, el directorio de Azure AD se crea automáticamente si es necesario.  

Para obtener más información sobre Azure AD, vea [¿Qué es Azure AD Directory?](/azure/active-directory/fundamentals/active-directory-whatis)

Para integrar el directorio de Azure AD con los bosques de AD locales, consulte [Integración de los dominios locales de Active Directory con Azure Active Directory](/azure/architecture/reference-architectures/identity/azure-ad).

### <a name="scenarios-that-have-specific-requirements"></a>Escenarios que tienen requisitos específicos 

Equipos que ejecutan Office 2010: 

- Estos equipos requieren el [cliente de Azure Information Protection](./rms-client/aip-client.md) para autenticarse en Azure Information Protection y su servicio de protección de datos, Azure Rights Management.

- Si las cuentas de usuario están federadas (por ejemplo, usa AD FS), deben usar la autenticación integrada de Windows. En este escenario, la autenticación basada en formularios no puede autenticar a los usuarios en Azure Information Protection.

Compatibilidad con la autenticación basada en certificados (CBA):

- Las aplicaciones de Azure Information Protection para iOS y Android admiten la autenticación basada en certificados. Para consultar las instrucciones sobre la configuración de la autenticación basada en certificados, consulte [Introducción a la autenticación basada en certificados de Azure Active Directory](/azure/active-directory/active-directory-certificate-based-authentication-get-started).

El valor de UPN de los usuarios no coincide con su dirección de correo electrónico:

- Esta no es la configuración recomendada. Si no puede cambiar el valor de UPN, configure un identificador de inicio de sesión alternativo para los usuarios e indíqueles cómo usarlo para iniciar sesión en Office. Para más información, consulte [Configuración de identificador de inicio de sesión alternativo](/windows-server/identity/ad-fs/operations/configuring-alternate-login-id) y [Las aplicaciones de Office periódicamente piden credenciales a SharePoint Online, OneDrive y Lync Online](https://support.microsoft.com/help/2913639/office-applications-periodically-prompt-for-credentials-to-sharepoint-online,-onedrive,-and-lync-online).
    
    Cuando el nombre de dominio del valor de UPN es un dominio que se ha comprobado para el inquilino, agregue el valor de UPN del usuario como otra dirección de correo electrónico al atributo proxyAddresses de Azure AD. Esto permite que el usuario esté autorizado para Azure Rights Management si se especifica su valor de UPN en el momento en que se conceden los derechos de uso. Para más información sobre esto y cómo se autorizan las cuentas de usuario, consulte [Preparación de usuarios y grupos para Azure Information Protection](prepare.md).

Dispositivos móviles o equipos Mac que se autentican localmente mediante AD FS o un proveedor de autenticación equivalente:

- Debe usar AD FS en la versión mínima de servidor de **Windows Server 2012 R2** o un proveedor de autenticación alternativo que admita el protocolo OAuth 2.0.

## <a name="multi-factor-authentication-mfa-and-azure-information-protection"></a>Multi-Factor Authentication (MFA) y Azure Information Protection
Para usar Multi-Factor Authentication (MFA) con Azure Information Protection se necesita como mínimo uno de los dos requisitos siguientes:

-   Office 2013 (versión mínima):

    -   Si tiene Office 2013, es posible que necesite instalar una actualización adicional para que la Biblioteca de autenticación de Active Directory (ADAL) sea compatible. Por ejemplo, la [actualización para Office 2013 (KB3054853) del 9 de junio de 2015](https://support.microsoft.com/kb/3054853). Para obtener más información sobre esta actualización y sobre la manera en la que la autenticación moderna proporciona el inicio de sesión basado en la Biblioteca de autenticación de Active Directory (ADAL) para Office 2013, consulte [Anuncio de la versión preliminar pública de la autenticación moderna de Office 2013](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/) en el blog de Office.

- Cliente de Azure Information Protection:

    - El [cliente de Azure Information Protection](./rms-client/aip-client.md) para Windows y la aplicación de visor para iOS y Android siempre ha admitido MFA; no se requiere ninguna versión mínima. 

-   Aplicación Rights Management sharing para equipos Mac:

    -   La compatibilidad con MFA se incluyó en la versión de septiembre de 2015 de la aplicación para uso compartido de RMS.

A continuación, configure la solución MFA:

-   Para inquilinos administrados por Microsoft (dispone de Azure Active Directory u Office 365):

    - Configure Azure MFA para aplicar MFA en los usuarios. Para obtener instrucciones, consulte [Introducción a Azure Multi-Factor Authentication en la nube](/multi-factor-authentication/multi-factor-authentication-get-started-cloud) en la documentación de Multi-factor Authentication.

        Para más información sobre Azure MFA, consulte [¿Qué es Azure Multi-Factor Authentication?](/multi-factor-authentication/multi-factor-authentication)

- Para inquilinos federados (los servidores de federación funcionan localmente):

    - Configure los servidores de federación para Azure Active Directory u Office 365. Por ejemplo, si usa AD FS, consulte [Configurar métodos de autenticación adicionales para AD FS](https://technet.microsoft.com/library/dn758113.aspx) en TechNet.

        Para más información sobre este escenario, consulte [Programa Works with Office 365 – Identity ahora simplificado](https://blogs.office.com/2014/01/30/the-works-with-office-365-identity-program-now-streamlined/) en el blog de Office.

El conector de Rights Management y el analizador de Azure Information Protection no son compatibles con MFA. Si implementa el conector o un analizador, las cuentas siguientes no deben requerir MFA:

- La cuenta que instala y configura el conector.

- La cuenta de entidad de servicio en Azure AD, **Aadrm_S-1-7-0**, que crea el conector.
 
- La cuenta de servicio que ejecuta el analizador.

## <a name="next-steps"></a>Pasos siguientes
Para comprobar otros requisitos, vea [Requisitos para Azure Information Protection](requirements.md).

