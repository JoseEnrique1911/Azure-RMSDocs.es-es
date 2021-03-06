---
title: 'Directiva predeterminada para Azure Information Protection: AIP'
description: Obtenga información sobre cómo está configurada la directiva predeterminada de Azure Information Protection. Si modifica la directiva predeterminada, puede tomar estos valores como referencia para devolver la directiva a la configuración predeterminada.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/06/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: a6fd4b308413fb5bf852a5c063c54b972497289c
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56253598"
---
# <a name="the-default-azure-information-protection-policy"></a>Directiva predeterminada de Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Utilice la siguiente información para comprender cómo está configurada la directiva predeterminada de Azure Information Protection.

Cuando un administrador se conecta por primera vez al servicio Azure Information Protection mediante Azure Portal, se crea la directiva predeterminada de Azure Information Protection para ese inquilino. En ocasiones, es posible que Microsoft realice cambios en la directiva predeterminada, pero si ya estaba usando el servicio antes de que se revisara la directiva predeterminada, no se actualiza la versión anterior de la directiva predeterminada de Azure Information Protection porque podría haberla configurado e implementado en producción.

Puede hacer referencia a los siguientes valores para devolver la directiva de Azure Information Protection a los valores predeterminados o actualizar la directiva de Azure Information Protection con los valores más recientes.

## <a name="current-default-policy"></a>Directiva predeterminada actual

Esta versión de la directiva predeterminada de Azure Information Protection es del 31 de julio de 2017.

Esta directiva predeterminada de Azure Information Protection se crea cuando se activa el servicio de Azure Rights Management, que es el caso de los nuevos inquilinos a partir de febrero de 2018. Para más información, consulte el anuncio de la entrada de blog [Improvements to the protection stack in Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2018/03/08/improvements-to-the-protection-stack-in-azure-information-protection) (Mejoras para la pila de protección en Azure Information Protection).

Esta directiva predeterminada de Azure Information Protection también se crea si ha [activado el servicio](activate-service.md) manualmente antes de que se creara la directiva de Azure Information Protection. 

Si este servicio no se ha activado, la directiva predeterminada de Azure Information Protection no configurará la protección para las siguientes subetiquetas:

- **Confidencial\Todos los empleados**

- **Confidencial \ Solo destinatarios**

- **Extremadamente confidencial\Todos los empleados** 

- **Extremadamente confidencial \ Solo destinatarios** 

Cuando estas subetiquetas no se configuran automáticamente para la protección, la directiva predeterminada de Azure Information Protection es igual a la [anterior directiva predeterminada](#default-policy-before-july-31-2017).

Cuando se aplica la protección a las subetiquetas **Todos los empleados**, la protección se configura mediante las plantillas predeterminadas que se convierten automáticamente en etiquetas en Azure Portal. Para obtener más información sobre estas plantillas, vea [Configuración y administración de plantillas para Azure Information Protection](configure-policy-templates.md).

A partir del 30 de agosto de 2017, esta versión de la directiva predeterminada de Azure Information Protection incluye versiones en diversos idiomas de los nombres y las descripciones de las etiquetas. 

#### <a name="more-information-about-the-recipients-only-sublabel"></a>Más información sobre la subetiqueta Solo destinatarios

Los usuarios ven esta etiqueta solo en Outlook. No la ven en Word, Excel, PowerPoint o el Explorador de archivos. 

Cuando los usuarios seleccionan esta etiqueta, la opción No reenviar de Outlook se aplica automáticamente al correo electrónico. Los destinatarios que especifiquen los usuarios no podrán reenviar el correo electrónico y no podrán copiar o imprimir el contenido ni guardar los datos adjuntos.


### <a name="labels"></a>Etiquetas

|Etiqueta|Información sobre herramientas|Configuración|
|-------------------------------|---------------------------|-----------------|
|Personal|Datos no comerciales de uso exclusivamente personal.|**Habilitada**: En <br /><br />**Color**: verde claro<br /><br />**Marcas visuales**: Desactivado <br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|
|Público|Datos comerciales específicamente elaborados y aprobados para un uso público.|**Habilitada**: En <br /><br />**Color**: Verde<br /><br />**Marcas visuales**: Desactivado<br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|
|General|Datos comerciales que no deben ser de dominio público. Pero, si fuera necesario, podrían compartirse con asociados externos. Por ejemplo, el directorio telefónico interno de la empresa, los organigramas, las normativas internas y la mayoría de las comunicaciones internas.|**Habilitada**: En <br /><br />**Color**: Azul <br /><br />**Marcas visuales**: Desactivado<br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|
|Confidencial|Datos comerciales confidenciales que podrían ocasionar daños a la empresa si se compartieran con personas no autorizadas. Ejemplos: contratos, informes de seguridad, resúmenes de previsiones y datos de cuentas de ventas.|**Habilitada**: En <br /><br />**Color**: naranja<br /><br />**Marcas visuales**: Desactivado<br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|
|Extremadamente confidencial|Datos comerciales extremadamente confidenciales que podrían ocasionar daños a la empresa si se compartieran con personas no autorizadas. Ejemplos: información sobre empleados y clientes, contraseñas, código fuente e informes financieros previamente anunciados.|**Habilitada**: En <br /><br />**Color**: Roja<br /><br />**Marcas visuales**: Desactivado<br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|


### <a name="sublabels"></a>Subetiquetas

|Etiqueta|Información sobre herramientas|Configuración|
|-------------------------------|---------------------------|-----------------|
|Confidencial \ Todos los empleados|Datos confidenciales que requieren protección pero conceden todos los permisos a todos los empleados. Los propietarios de los datos pueden hacer un seguimiento del contenido y revocarlo.|**Habilitada**: En <br /><br />**Marcas visuales**: pie de página (documentos y correo electrónico)<br /><br />Clasificado como confidencial<br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Azure (clave de nube) [[1]](#footnote-1)|
|Confidencial \ Cualquiera (sin protección)|Datos que no requieren protección. Use esta opción con precaución y con la debida justificación comercial.|**Habilitada**: En <br /><br />**Marcas visuales**: pie de página (documentos y correo electrónico)<br /><br />Clasificado como confidencial <br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|
|Confidencial \ Solo destinatarios|Datos confidenciales que requieren protección y que solo pueden ver los destinatarios.|**Habilitada**: En <br /><br />**Marcas visuales**: pie de página (correo electrónico)<br /><br />Clasificado como confidencial <br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: establecer permisos definidos por el usuario (versión preliminar). En Outlook, seleccione No reenviar.|
|Extremadamente confidencial \ Todos los empleados|Datos extremadamente confidenciales que conceden a los empleados los permisos de visualización, edición y respuesta en relación con el contenido. Los propietarios de los datos pueden hacer un seguimiento del contenido y revocarlo.|**Habilitada**: En <br /><br />**Marcas visuales**: pie de página (documentos y correo electrónico)<br /><br />Clasificado como extremadamente confidencial<br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Azure (clave de nube) [[2]](#footnote-2)|
|Extremadamente confidencial \ Cualquiera (sin protección)|Datos que no requieren protección. Use esta opción con precaución y con la debida justificación comercial.|**Habilitada**: En <br /><br />**Marcas visuales**: pie de página (documentos y correo electrónico)<br /><br />Clasificado como extremadamente confidencial<br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|
|Extremadamente confidencial \ Solo destinatarios|Datos extremadamente confidenciales que requieren protección y que solo pueden ver los destinatarios.|**Habilitada**: En <br /><br />**Marcas visuales**: pie de página (correo electrónico)<br /><br />Clasificado como extremadamente confidencial <br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: establecer permisos definidos por el usuario (versión preliminar). En Outlook, seleccione No reenviar.|

###### <a name="footnote-1"></a>Nota al pie 1
Los permisos de protección coinciden con los de la [plantilla predeterminada](configure-policy-templates.md#default-templates), **Confidencial\Todos los empleados**.

###### <a name="footnote-2"></a>Nota al pie 2 
Los permisos de protección coinciden con los de la [plantilla predeterminada](configure-policy-templates.md#default-templates), **Extremadamente confidencial\Todos los empleados**.


### <a name="information-protection-bar"></a>Barra de Information Protection

|Setting|Valor|
|-------------------------------|---------------------------|
|Título|Sensibilidad|
|Información sobre herramientas|Etiqueta actual de este contenido. Este valor identifica el riesgo que supondría a la empresa el hecho de que este contenido se compartiera con personas no autorizadas de dentro o fuera de la organización.|


### <a name="settings"></a>Configuración

|Setting|Valor|
|-------------------------------|---------------------------|
|All documents and emails must have a label (applied automatically or by users) [Todos los documentos y correos electrónicos deben tener una etiqueta (aplicada automáticamente o por los usuarios)]|Desactivado|
|Select the default label (Seleccionar la etiqueta predeterminada)|Ninguno|
|Users must provide justification to set a lower classification label, remove a label, or remove protection (Los usuarios deben proporcionar una justificación para establecer una etiqueta de clasificación inferior, quitar una etiqueta o quitar la protección)|Desactivado|
|Para los mensajes de correo electrónico con datos adjuntos, aplicar una etiqueta que coincida con la clasificación más alta de los datos adjuntos|Desactivado|
|Proporcionar una dirección URL personalizada para la página web "Más información" del cliente de Azure Information Protection|En blanco|


## <a name="default-policy-before-july-31-2017"></a>Directiva predeterminada antes del 31 de julio de 2017

Tenga en cuenta que las descripciones de esta directiva hacen referencia a datos que necesitan protección y también al seguimiento y la revocación de datos. La directiva no configura esta protección para estas etiquetas, por lo que tendrá que realizar pasos adicionales para completar esta descripción. Por ejemplo, configure la etiqueta para aplicar la protección o use una solución de prevención de pérdida de datos (DLP). Antes de realizar el seguimiento de un documento y revocarlo mediante el sitio de seguimiento de documentos, este debe protegerse con el servicio Azure Rights Management y la persona que lo ha protegido debe seguirlo. 


### <a name="labels"></a>Etiquetas

|Etiqueta|Información sobre herramientas|Configuración|
|-------------------------------|---------------------------|-----------------|
|Personal|Datos no comerciales de uso exclusivamente personal.|**Habilitada**: En <br /><br />**Color**: verde claro<br /><br />**Marcas visuales**: Desactivado <br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|
|Público|Datos comerciales específicamente elaborados y aprobados para un uso público.|**Habilitada**: En <br /><br />**Color**: Verde<br /><br />**Marcas visuales**: Desactivado<br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|
|General|Datos comerciales que no deben ser de dominio público. Pero, si fuera necesario, podrían compartirse con asociados externos. Por ejemplo, el directorio telefónico interno de la empresa, los organigramas, las normativas internas y la mayoría de las comunicaciones internas.|**Habilitada**: En <br /><br />**Color**: Azul <br /><br />**Marcas visuales**: Desactivado<br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|
|Confidencial|Datos comerciales confidenciales que podrían ocasionar daños a la empresa si se compartieran con personas no autorizadas. Ejemplos: contratos, informes de seguridad, resúmenes de previsiones y datos de cuentas de ventas.|**Habilitada**: En <br /><br />**Color**: naranja<br /><br />**Marcas visuales**: Desactivado<br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|
|Extremadamente confidencial|Datos comerciales extremadamente confidenciales que podrían ocasionar daños a la empresa si se compartieran con personas no autorizadas. Ejemplos: información sobre empleados y clientes, contraseñas, código fuente e informes financieros previamente anunciados.|**Habilitada**: En <br /><br />**Color**: Roja<br /><br />**Marcas visuales**: Desactivado<br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|


### <a name="sublabels"></a>Subetiquetas

|Etiqueta|Información sobre herramientas|Configuración|
|-------------------------------|---------------------------|-----------------|
|Confidencial \ Todos los empleados|Datos confidenciales que requieren protección pero conceden todos los permisos a todos los empleados. Los propietarios de los datos pueden hacer un seguimiento del contenido y revocarlo.|**Habilitada**: En <br /><br />**Marcas visuales**: pie de página (documentos y correo electrónico)<br /><br />Clasificado como confidencial<br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|
|Confidencial \ Cualquiera (sin protección)|Datos que no requieren protección. Use esta opción con precaución y con la debida justificación comercial.|**Habilitada**: En <br /><br />**Marcas visuales**: pie de página (documentos y correo electrónico)<br /><br />Clasificado como confidencial <br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|
|Extremadamente confidencial \ Todos los empleados|Datos extremadamente confidenciales que conceden a los empleados los permisos de visualización, edición y respuesta en relación con el contenido. Los propietarios de los datos pueden hacer un seguimiento del contenido y revocarlo.|**Habilitada**: En <br /><br />**Marcas visuales**: pie de página (documentos y correo electrónico)<br /><br />Clasificado como extremadamente confidencial<br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|
|Extremadamente confidencial \ Cualquiera (sin protección)|Datos que no requieren protección. Use esta opción con precaución y con la debida justificación comercial.|**Habilitada**: En <br /><br />**Marcas visuales**: pie de página (documentos y correo electrónico)<br /><br />Clasificado como extremadamente confidencial<br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|

### <a name="information-protection-bar"></a>Barra de Information Protection

|Setting|Valor|
|-------------------------------|---------------------------|
|Título|Sensibilidad|
|Información sobre herramientas|Etiqueta actual de este contenido. Este valor identifica el riesgo que supondría a la empresa el hecho de que este contenido se compartiera con personas no autorizadas de dentro o fuera de la organización.|


### <a name="settings"></a>Configuración

|Setting|Valor|
|-------------------------------|---------------------------|
|All documents and emails must have a label (applied automatically or by users) [Todos los documentos y correos electrónicos deben tener una etiqueta (aplicada automáticamente o por los usuarios)]|Desactivado|
|Select the default label (Seleccionar la etiqueta predeterminada)|Ninguno|
|Users must provide justification to set a lower classification label, remove a label, or remove protection (Los usuarios deben proporcionar una justificación para establecer una etiqueta de clasificación inferior, quitar una etiqueta o quitar la protección)|Desactivado|
|Para los mensajes de correo electrónico con datos adjuntos, aplicar una etiqueta que coincida con la clasificación más alta de los datos adjuntos|Desactivado|
|Proporcionar una dirección URL personalizada para la página web "Más información" del cliente de Azure Information Protection|En blanco|

## <a name="default-policy-before-march-21-2017"></a>Directiva predeterminada antes del 21 de marzo de 2017

### <a name="labels"></a>Etiquetas

|Etiqueta|Información sobre herramientas|Configuración|
|-------------------------------|---------------------------|-----------------|
|Personal|Solo para uso personal. Estos datos no se supervisan en la organización. La información personal no debe incluir datos relacionados con el negocio.|**Habilitada**: En <br /><br />**Color**: verde claro<br /><br />**Marcas visuales**: Desactivado <br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|
|Público|Esta información es interna y todo el mundo puede usarla, tanto dentro como fuera de la empresa.|**Habilitada**: En <br /><br />**Color**: Verde<br /><br />**Marcas visuales**: Desactivado<br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|
|Interno|Esta información incluye una amplia variedad de datos empresariales internos que todos los empleados pueden usar y que se pueden compartir con clientes y asociados comerciales autorizados. Ejemplos de información interna son las directivas de empresa y la mayoría de las comunicaciones internas.|**Habilitada**: En <br /><br />**Color**: Azul <br /><br />**Marcas visuales**: pie de página (documentos y correo electrónico) <br /><br />Sensibilidad: Interno<br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|
|Confidencial|Estos datos incluyen información empresarial confidencial. Exponer estos datos a usuarios no autorizados puede provocar daños para la organización. Ejemplos de información confidencial son información de los empleados, proyectos o contratos de clientes individuales y datos de cuentas de ventas.|**Habilitada**: En <br /><br />**Color**: naranja<br /><br />**Marcas visuales**: pie de página (documentos y correo electrónico)<br /><br /> Sensibilidad: Confidencial<br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|
|Secreto|Estos datos incluyen información confidencial de la empresa que se debe proteger. Exponer datos secretos a usuarios no autorizados puede provocar daños graves para la organización. Ejemplos de información secreta son información de identificación personal, registros de cliente, código fuente e informes financieros previamente anunciados.|**Habilitada**: En <br /><br />**Color**: Roja<br /><br />**Marcas visuales**: pie de página (documentos y correo electrónico)<br /><br /> Sensibilidad: Secreto<br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|


### <a name="sublabels"></a>Subetiquetas

|Etiqueta|Información sobre herramientas|Configuración|
|-------------------------------|---------------------------|-----------------|
|Secreto \ All Company (Toda la compañía)|Estos datos incluyen información empresarial confidencial, permitida para todos los empleados de la empresa.|**Habilitada**: En <br /><br />**Marcas visuales**: Desactivado<br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|
|Secreto \ My Group (Mi grupo)|Estos datos incluyen información empresarial confidencial, permitida solo para grupos de empleados.|**Habilitada**: En <br /><br />**Marcas visuales**: Desactivado<br /><br />**Condiciones**: Ninguno<br /><br />**Protección**: Ninguno|

### <a name="information-protection-bar"></a>Barra de Information Protection

|Setting|Valor|
|-------------------------------|---------------------------|
|Título|Sensibilidad|
|Información sobre herramientas|Information Sensitivity consta de cuatro niveles distintos (Público, Interno, Confidencial y Secreto), que permiten al usuario identificar el riesgo de exposición de la información a usuarios no autorizados dentro o fuera de la empresa.|


### <a name="settings"></a>Configuración

|Setting|Valor|
|-------------------------------|---------------------------|
|All documents and emails must have a label (applied automatically or by users) [Todos los documentos y correos electrónicos deben tener una etiqueta (aplicada automáticamente o por los usuarios)]|Desactivado|
|Select the default label (Seleccionar la etiqueta predeterminada)|Ninguno|
|Users must provide justification to set a lower classification label, remove a label, or remove protection (Los usuarios deben proporcionar una justificación para establecer una etiqueta de clasificación inferior, quitar una etiqueta o quitar la protección)|Desactivado|
|Proporcionar una dirección URL personalizada para la página web "Más información" del cliente de Azure Information Protection|En blanco|


## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización). 
