---
title: "Configuración de una etiqueta para aplicar la protección de Rights Management | Azure Information Protection"
description: "Puede proteger sus documentos y correos electrónicos más confidenciales mediante el servicio Rights Management, que usa directivas de autorización, identidad y cifrado para ayudar a evitar la pérdida de datos. Esta protección se aplica al configurar una etiqueta para usar una plantilla de Rights Management."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/07/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
translationtype: Human Translation
ms.sourcegitcommit: 5d1a5e3b85d5450bcb2064a6c3b95e6ad802eea3
ms.openlocfilehash: 31ef3e41e84515c02ebe97f01025331578273c71


---

# <a name="how-to-configure-a-label-to-apply-rights-management-protection"></a>Configuración de una etiqueta para aplicar protección de Rights Management

>*Se aplica a: Azure Information Protection*

Puede proteger sus documentos y correos electrónicos más confidenciales mediante el servicio Rights Management, que usa directivas de autorización, identidad y cifrado para ayudar a evitar la pérdida de datos. Esta protección se aplica al configurar una etiqueta para usar una plantilla de Rights Management. 

Esta plantilla puede ser una de las plantillas predeterminadas que se crean automáticamente al activar Azure Rights Management o una plantilla personalizada. Las plantillas departamentales de Azure Rights Management se admiten pero solo aplican la protección cuando el autor del documento o del correo electrónico está dentro del ámbito configurado de la plantilla. Si el usuario no está dentro del ámbito, verá un mensaje para indicar que Azure Information Protection no puede aplicar la etiqueta.

## <a name="how-the-protection-works"></a>Funcionamiento de la protección

Cuando un documento o un correo electrónico están protegidos con Rights Management, se cifran en reposo y en tránsito y solo los usuarios autorizados pueden descifrarlos. Este cifrado permanece con el documento o el correo electrónico, incluso si se cambia de nombre. Además, puede configurar derechos y restricciones de uso, como en los ejemplos siguientes:

- Solo los usuarios de su organización pueden abrir el documento o correo electrónico confidencial de la empresa.

- Solo los usuarios del departamento de marketing pueden editar e imprimir el documento o correo electrónico de anuncio de promoción, mientras que los demás usuarios de la organización solo pueden leerlo.

- Los usuarios no pueden reenviar un correo electrónico que contiene noticias sobre una reorganización interna.

- La lista de precios actual que se envía a asociados comerciales no se puede abrir después de una fecha especificada.

Para obtener más información sobre las plantillas de Azure Rights Management y cómo configurar estos derechos y restricciones de uso, consulte [Configuración de plantillas personalizadas para el servicio Azure Rights Management](../deploy-use/configure-custom-templates.md).

Para más información sobre Azure Rights Management y cómo funciona, consulte [¿Qué es Azure Rights Management?](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Para configurar una etiqueta para aplicar la protección de Azure Rights Management, se debe activar el servicio Azure Rights Management para la organización. Si aún no lo ha hecho, consulte [Activación de Azure Rights Management](../deploy-use/activate-service.md).

No es necesario que Exchange esté configurado para Information Rights Management (IRM) para que los usuarios puedan aplicar las etiquetas en Outlook para proteger sus mensajes de correo electrónico. Sin embargo, hasta que no se configure Exchange para IRM, no disfrutará de toda la funcionalidad derivada del uso de la protección de Azure Rights Management con Exchange. Por ejemplo, los usuarios no podrán ver los correos electrónicos protegidos en teléfonos móviles o con Outlook Web Access, los correos electrónicos protegidos no se podrán indexar para la búsqueda, y no podrá configurar Exchange Online DLP para la protección de Rights Management. A fin de configurar Exchange para admitir estos escenarios adicionales, consulte los siguientes recursos:

- Para Exchange Online, consulte las instrucciones de [Exchange Online: Configuración de IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration).

- Para Exchange local, debe implementar el [conector RMS y configurar los servidores de Exchange](../deploy-use/deploy-rms-connector.md). 


## <a name="to-configure-a-label-to-apply-rights-management-protection"></a>Para configurar una etiqueta para aplicar la protección de Rights Management

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e inicie sesión en [Azure Portal](https://portal.azure.com)como administrador global y, después, navegue hasta la hoja **Azure Information Protection**. 

    Por ejemplo, en el menú del centro, haga clic en **Más servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. Si la etiqueta que quiere configurar se va a aplicar a todos los usuarios, seleccione la etiqueta que se modificará en la hoja **Policy:Global** (Directiva:Global). 

     Si la etiqueta que quiere configurar está en una [directiva de ámbito](configure-policy-scope.md) de modo que se aplica solo a los usuarios seleccionados, seleccione primero esa directiva de ámbito en la hoja inicial de **Azure Information Protection**.

3. En la hoja **Etiqueta**, en la sección **Establecer la plantilla de RMS para proteger documentos y correos electrónicos que contengan esta etiqueta**, en **Seleccionar plantilla RMS de**, seleccione **Azure RMS** o **AD RMS**.
    
    En la mayoría de los casos, seleccionará **Azure RMS**. No seleccione AD RMS a menos que haya leído y comprendido los requisitos previos y restricciones que acompañan a esta configuración, que a veces se conoce como "*mantenga su propia clave*" (HYOK). Para obtener más información, consulte [Requisitos y restricciones de Mantenga su propia clave (HYOK) para la protección de AD RMS](configure-adrms-restrictions.md).
    
4. Si ha seleccionado Azure RMS: en **Seleccionar plantilla RMS**, haga clic en el cuadro desplegable y seleccione la [plantilla](../deploy-use/configure-custom-templates.md) o la opción de Rights Management que quiera usar para proteger documentos y correos electrónicos con esta etiqueta.
    
    Más información acerca de las opciones:
    
    - ¿Ha creado una nueva plantilla después de abrir la hoja **Etiqueta**? Cierre esta hoja y vuelva al paso 2, así la plantilla recién creada se recuperará de Azure para que la seleccione.
    
    - Si selecciona una **plantilla de departamento** o si configura los [controles de incorporación](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment):
    
        - Los usuarios que estén fuera del ámbito configurado de la plantilla o que se excluyan al aplicar la protección de Azure Rights Management seguirán viendo la etiqueta, pero no podrán aplicarla. Si seleccionan la etiqueta, verán el mensaje siguiente: **Azure Information Protection no puede aplicar esta etiqueta. Si el problema persiste, póngase en contacto con el administrador.**
        
            Observe que siempre se muestran todas las plantillas, a pesar de vaya a configurar una directiva de ámbito. Por ejemplo, va a configurar una directiva de ámbito para el grupo Marketing. Las plantillas de Azure RMS que puede seleccionar no se limitarán a las plantillas cuyo ámbito sea el grupo Marketing, y es posible seleccionar una plantilla de departamento que los usuarios seleccionados no pueden usar. Para facilitar la configuración y reducir la solución de problemas, puede nombrar la plantilla de departamento de forma que coincida con la etiqueta de la directiva de ámbito. 
            
    - Si selecciona **Quitar protección**:
        
        - Los usuarios deben tener permisos para quitar la protección de Rights Management para aplicar una etiqueta con esta opción. Esta opción requiere que tengan el **derecho de uso** **Exportar** (para documentos de Office) o [Control total](../deploy-use/configure-usage-rights.md), o que sean el propietario de Rights Management (concede automáticamente el derecho de uso Control total) o un [superusuario para Azure Rights Management](../deploy-use/configure-super-users.md). Las plantillas de Rights Management predeterminadas no incluyen los derechos de uso que permite a los usuarios quitar la protección. 

            Si los usuarios no tienen permisos para quitar la protección de Rights Management y seleccionar esta etiqueta con la opción **Quitar protección**, se muestra el mensaje indicando que **Azure Information Protection no puede aplicar esta etiqueta. Si el problema persiste, póngase en contacto con el administrador.**

5. Si ha seleccionado AD RMS: proporcione el GUID de la plantilla y la dirección URL de administración de licencias del clúster de AD RMS. [Más información](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label)

6. Haga clic en **Guardar**.

7. Para que los cambios estén disponibles para los usuarios, en la hoja **Azure Information Protection**, haga clic en **Publicar**.

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).  



<!--HONumber=Dec16_HO1-->

