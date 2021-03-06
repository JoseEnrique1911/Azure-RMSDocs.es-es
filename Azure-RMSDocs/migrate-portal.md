---
title: Migración desde el Portal de Azure clásico (AIP)
description: Tareas de administración resumidas de Azure Portal que solía realizar en el Portal de Azure clásico
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/07/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 57a1073c-02e0-441b-bf49-c6b72fdba24f
ms.reviewer: demizets
ms.suite: ems
ms.openlocfilehash: c445b676a6aea817e2aef410886c22d9009519e4
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256267"
---
# <a name="tasks-that-you-used-to-do-with-the-azure-classic-portal"></a>Tareas que solía realizar con el Portal de Azure clásico

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

¿Está acostumbrado al Portal de Azure clásico para administrar el servicio Azure Rights Management y necesita algo de ayuda para migrar a Azure Portal?

El portal clásico de Azure dejó de estar disponible el **8 de enero de 2018**. Tras esta fecha, no podrá administrar el servicio Azure Rights Management y las plantillas personalizadas desde el portal clásico. Si intenta obtener acceso al portal clásico, verá un vínculo que le llevará al nuevo Azure Portal.

Para más información sobre la retirada del portal clásico, vea la entrada de blog del anuncio: [Marching into the future of the Azure AD admin experience: retiring the Azure classic portal](https://cloudblogs.microsoft.com/enterprisemobility/2017/09/18/marching-into-the-future-of-the-azure-ad-admin-experience-retiring-the-azure-classic-portal/) (El futuro de la experiencia de administración de Azure AD: retirada del Portal de Azure clásico). Para conocer la extensión temporal de la fecha de retirada original, vea [Update on retirement of Azure AD classic portal experience and migration of conditional access policies](https://cloudblogs.microsoft.com/enterprisemobility/2017/11/29/update-on-retirement-of-azure-ad-classic-portal-experience-and-migration-of-conditional-access-policies/) (Actualización sobre la retirada de la experiencia del portal clásico de Azure AD y migración de las directivas de acceso condicional).

## <a name="how-to-do-your-familiar-admin-tasks"></a>Cómo realizar tareas de administración familiares

Use la información siguiente para realizar la transición al portal actual de forma rápida.

|Portal de Azure clásico|Cómo realizar esta tarea en Azure Portal
|-----------|--------------------|
|Acceso a los valores de configuración por primera vez|1. Inicie sesión en [Azure Portal](configure-policy.md#signing-in-to-the-azure-portal).<br /><br />2. Siga las instrucciones para [acceder a la hoja de Azure Information Protection por primera vez](configure-policy.md#to-access-the-azure-information-protection-blade-for-the-first-time).
|Creación de una plantilla nueva|Cree una etiqueta que aplique protección y use **Establecer permisos** para definir los permisos, la expiración y el acceso sin conexión. <br /><br />En segundo plano, esta configuración crea una nueva plantilla personalizada a la que pueden acceder los servicios y las aplicaciones que se integran con las plantillas de Rights Management.<br /><br />Para más información, vea [Para crear una nueva plantilla](configure-policy-templates.md#to-create-a-new-template).
|Edite las propiedades de la plantilla: <br /><br />- Nombre y descripción de la plantilla<br /><br />- Configuración de derechos de uso, expiración de contenido y acceso sin conexión|Si aún no lo ha hecho, [convierta la plantilla en una etiqueta](configure-policy-templates.md#to-convert-templates-to-labels) y luego haga lo siguiente<br /><br />1. Cambie el nombre y la descripción de la etiqueta<br /><br />2. Cambie la configuración de protección de la etiqueta para actualizar la configuración de permisos, expiración y acceso sin conexión.<br /><br />Para más información, consulte [Para configurar una etiqueta para la protección de Rights Management](configure-policy-protection.md#to-configure-a-label-for-protection-settings).
|Archivo de una plantilla|Establezca el estado de la etiqueta en **Deshabilitado**.
|Creación de una plantilla con ámbito|Cree una directiva con ámbito y luego cree una etiqueta en este ámbito que aplique la protección. <br /><br />Para más información, vea [Configuración de la directiva de Azure Information Protection para usuarios específicos mediante directivas de ámbito](configure-policy-scope.md).
|Copia de una plantilla|No es posible copiar una plantilla en Azure Portal. Si quiere que dos etiquetas tengan la misma configuración de protección, debe establecer los permisos en cada etiqueta. <br /><br />Para más información, consulte [Para configurar una etiqueta para la protección de Rights Management](configure-policy-protection.md#to-configure-a-label-for-protection-settings).
|Eliminar una plantilla|La eliminación de plantillas puede dar lugar a la inaccesibilidad de los datos, por lo que Azure Portal no admite esta acción. Pero puede eliminar la etiqueta y luego usar el cmdlet de PowerShell [Remove-AadrmTemplate](/powershell/module/aadrm/remove-aadrmtemplate) para quitar la plantilla. <br /><br />Para más información, vea [Eliminación o cambio de orden de una etiqueta en Azure Information Protection](configure-policy-delete-reorder.md).
|Compatibilidad con varios idiomas|En la opción de menú **Administrar**, seleccione **Idiomas** para exportar los campos personalizables que incluyen el nombre y la descripción de la plantilla. Traduzca las cadenas y luego impórtelas al portal. <br /><br />Para más información, vea [Cómo configurar etiquetas y plantillas para distintos idiomas en Azure Information Protection](configure-policy-languages.md).
|Informes web de Rights Management|[Informes centrales para Azure Information Protection](reports-aip.md) está ahora en versión preliminar.<br /><br />También puede usar el cmdlet de PowerShell [Get-AadrmUsageLog](/powershell/module/aadrm/Get-AadrmUsageLog) para descargar registros de uso del servicio Azure Rights Management. Luego puede usar estos datos para crear informes personalizados. Para obtener más información, consulte [Registro y análisis del uso del servicio Azure Rights Management](log-analyze-usage.md).
|Activación y desactivación del servicio Rights Management|En las opciones de menú **Administrar**, seleccione **Activación de la protección**.<br /><br />Para obtener más información, vea [Cómo activar Azure Rights Management desde Azure Portal](activate-azure.md).

Antes de editar las plantillas o de convertirlas en etiquetas en Azure Portal, vea [Consideraciones para las plantillas en Azure Portal](configure-policy-templates.md#considerations-for-templates-in-the-azure-portal).


## <a name="what-else-has-changed"></a>Más cambios

Nueva funcionalidad en Azure Portal:

- Puede editar las [plantillas predeterminadas](configure-policy-templates.md#default-templates) que se crean automáticamente para la organización.

- Puede convertir plantillas en etiquetas, con lo que se administra un único objeto en lugar de una plantilla y una etiqueta de forma independiente. Para obtener instrucciones, vea [Para convertir plantillas en etiquetas](configure-policy-templates.md#to-convert-templates-to-labels).

- Compatibilidad con otros roles de administrador: mientras que en el Portal de Azure clásico había que iniciar sesión como administrador global para configurar Azure Rights Management, en Azure Portal puede iniciar sesión para configurar Azure Information Protection mediante una cuenta que tenga cualquiera de los siguientes roles de administrador: **Administrador global**, **Administrador de seguridad** o **Administrador de Information Protection**. Para más información sobre cada uno de estos roles, vea la sección [Roles disponibles](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) de la documentación de Azure Active Directory.

Los cmdlets de PowerShell para crear y administrar plantillas y para activar o desactivar el servicio siguen admitiéndose sin cambios.

## <a name="see-also"></a>Consulte también
Para obtener información detallada, vea [Configuración y administración de plantillas para Azure Information Protection](configure-policy-templates.md).

