---
title: 'Configuración de condiciones para una etiqueta de Azure Information Protection: AIP'
description: Las condiciones de una etiqueta le permiten asignar automáticamente una etiqueta a un documento o a un correo electrónico. O bien, puede indicar a los usuarios que seleccionen una etiqueta recomendada.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 01/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
ms.openlocfilehash: b7d0bf743d23083e2f9c6ca18044e26cb8c2ae6f
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256573"
---
# <a name="how-to-configure-conditions-for-automatic-and-recommended-classification-for-azure-information-protection"></a>Configuración de las condiciones para la clasificación automática y recomendada en Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Al configurar las condiciones de una etiqueta, puede asignar automáticamente la etiqueta a un documento o a un correo electrónico. También puede indicar a los usuarios que seleccionen la etiqueta que usted recomienda. 

Al configurar estas condiciones, puede usar patrones predefinidos, como **Número de la tarjeta de crédito** o **Número del seguro social de Estados Unidos (SSN)**. O puede definir un patrón o una cadena personalizada como condición de una clasificación automática. Estas condiciones se aplican al texto del cuerpo en documentos y correos electrónicos, así como a encabezados y pies de página. Para más información sobre las condiciones, vea el paso 5 del [siguiente procedimiento](#to-configure-recommended-or-automatic-classification-for-a-label).

Para conseguir la mejor experiencia de usuario y garantizar la continuidad empresarial, conviene comenzar con la clasificación recomendada al usuario, en lugar de la clasificación automática. Esta configuración permite a los usuarios aceptar la clasificación y cualquier protección asociada, o reemplazar estas sugerencias si no resultan adecuadas para su documento o mensaje de correo electrónico.

Mensaje de ejemplo cuando se configura una condición para aplicar una etiqueta como acción recomendada, con una sugerencia de directiva personalizada:

![Detección y recomendación de Azure Information Protection](./media/info-protect-recommend-calloutsv2.png)

En este ejemplo, el usuario puede hacer clic en **Cambiar ahora** para aplicar la etiqueta recomendada, o bien invalidar la recomendación seleccionando **Descartar**. Si el usuario decide descartar la recomendación y la condición sigue siendo válida la próxima vez que se abra el documento, se visualizará de nuevo la recomendación de etiquetas.

Si configura la clasificación automática en lugar de la recomendada, se aplica automáticamente la etiqueta y el usuario seguirá viendo una notificación en sus aplicaciones de Office. Sin embargo, los botones **Cambiar ahora** y **Descartar** se reemplazan por **Aceptar**.

> [!IMPORTANT]
>No configure una etiqueta para la clasificación automática y un permiso definido por el usuario. La opción de permisos definidos por el usuario es una [configuración de protección](configure-policy-protection.md) que permite a los usuarios especificar a quién se le deben conceder permisos.
>
>Cuando una etiqueta se configura para la clasificación automática y los permisos definidos por el usuario, se comprueba el contenido de las condiciones y no se aplica la configuración de los permisos definidos por el usuario. Puede utilizar la clasificación recomendada y los permisos definidos por el usuario.

## <a name="how-automatic-or-recommended-labels-are-applied"></a>Cómo se aplican las etiquetas automáticas o recomendadas

- La clasificación automática se aplica a Word, Excel y PowerPoint cuando se guardan documentos, y a Outlook cuando se envían correos electrónicos. 
    
    No se puede utilizar la clasificación automática para documentos y correos electrónicos etiquetados previamente de manera manual, o etiquetados previamente de manera automática, con una clasificación más alta. 

- La clasificación recomendada se aplica a Word, Excel y PowerPoint cuando se guardan documentos. No se puede utilizar la clasificación recomendada para Outlook a menos que configure un [parámetro de cliente avanzado](./rms-client/client-admin-guide-customizations.md#enable-recommended-classification-in-outlook) que está actualmente en versión preliminar.
    
    No puede usar la clasificación recomendada para los documentos etiquetados previamente con una clasificación más alta. 

Puede cambiar este comportamiento para que el cliente de Azure Information Protection compruebe periódicamente los documentos en busca de las reglas de condición que especifique. Esta configuración requiere una [configuración avanzada del cliente](./rms-client/client-admin-guide-customizations.md#turn-on-classification-to-run-continuously-in-the-background), que actualmente está en versión preliminar.

### <a name="how-multiple-conditions-are-evaluated-when-they-apply-to-more-than-one-label"></a>Cómo evaluar varias condiciones cuando se aplican a más de una etiqueta

1. Las etiquetas se ordenan para su evaluación, según la posición especificada en la directiva: la etiqueta que se coloca en primer lugar tiene la posición más baja (menos sensible) y la etiqueta que se coloca en último lugar tiene la posición más alta (más sensible).

2. Se aplica la etiqueta más sensible.
 
3. Se aplica la última subetiqueta.


## <a name="to-configure-recommended-or-automatic-classification-for-a-label"></a>Para configurar la clasificación automática o recomendada para una etiqueta

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. Desde la opción de menú **Clasificaciones** > **Etiquetas**: en la hoja **Azure Information Protection: Etiquetas**, seleccione la etiqueta que desea configurar.

3. En la hoja **Etiqueta**, en la sección **Configure conditions for automatically applying this label** (Configurar condiciones para aplicar esta etiqueta automáticamente), haga clic en **Agregar una nueva condición**(Add a new condition).

4. En la hoja **Condición**, seleccione **Tipos de información** si quiere usar una condición predefinida, o **Personalizada** si quiere especificar la suya propia:
    - En **Tipos de información**: seleccione entre las condiciones disponibles de la lista y luego elija el número mínimo de repeticiones y si la repetición debe tener un valor único para ser incluida en el recuento de repeticiones.
        
        Los tipos de información usan los tipos de información de confidencialidad de prevención de pérdida de datos (DLP) y la detección de patrones de Office 365. Puede elegir entre numerosos tipos comunes de información confidencial, algunos de los cuales son específicos de regiones determinadas. Para obtener más información, vea [Qué buscan los tipos de información confidencial](/office365/securitycompliance/what-the-sensitive-information-types-look-for) en la documentación de Office 365.
        
        La lista de tipos de información que se pueden seleccionar desde Azure Portal se actualiza periódicamente para incluir cualquier dato que se agregue a la prevención de pérdida de datos de Office. Sin embargo, la lista excluye los tipos de información confidencial personalizados que haya definido y cargado como un paquete de reglas para el Centro de seguridad y cumplimiento de Office 365.
        
        > [!IMPORTANT]
        > Algunos tipos de información requieren una versión mínima del cliente. [Más información](#sensitive-information-types-that-require-a-minimum-version-of-the-client) 
        
        Cuando Azure Information Protection evalúa los tipos de información que selecciona, no usa la configuración del nivel de confianza de DLP de Office, sino que encuentra coincidencias en función de la confianza más baja.
    
    - En **Personalizada**: especifique un nombre y una frase para buscar coincidencia, sin comillas ni caracteres especiales. A continuación, especifique si la coincidencia será una expresión regular, si se usará distinción entre mayúsculas y minúsculas y el número mínimo de repeticiones, y si la repetición deberá tener un valor único para incluirse en el recuento de repeticiones.
        
        Las expresiones regulares usan los patrones de expresiones regulares de Office 365. A fin de ayudarle a especificar expresiones regulares para sus condiciones personalizadas, consulte la siguiente versión específica de [sintaxis de expresiones regulares de Perl](https://www.boost.org/doc/libs/1_37_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html) de Boost.
        
5. Decida si tiene que cambiar **Número mínimo de repeticiones** y **Contar solo las repeticiones con valores únicos** y luego seleccione **Guardar**. 
    
    Ejemplo de las opciones de repeticiones: seleccione el tipo de información para el número del seguro social, establezca el número mínimo de repeticiones en 2, y un documento tendrá el mismo número del seguro social dos veces: si establece **Count occurrences with unique value only** (Contar solo las repeticiones con valores únicos) en **Activado**, la condición no se cumple. Si establece esta opción en **Desactivado**, la condición se cumple.

6. De vuelta en la hoja **Etiqueta**, configure lo siguiente y luego haga clic en **Guardar**:
    
    - Elija clasificación automática o recomendada: en **Select how this label is applied: automatically or recommended to user** (Seleccionar cómo se aplica esta etiqueta: automáticamente o recomendado al usuario), seleccione **Automática** o **Recomendada**.
    
    - Especifique el texto de la sugerencia de directiva o del mensaje de usuario: mantenga el texto predeterminado o especifique su propia cadena.

Al hacer clic en **Guardar**, los cambios están disponibles para los usuarios y servicios. Ya no hay una opción de publicación separada.

### <a name="sensitive-information-types-that-require-a-minimum-version-of-the-client"></a>Tipos de información confidencial que requieren una versión mínima del cliente

Los tipos de información confidencial siguientes requieren una versión mínima de 1.37.19.0 para el cliente de Azure Information Protection:

- **Número de teléfono móvil de la UE**
- **Número de pasaporte de la UE**
- **Número de licencia de conductor de la UE**
- **Número de identificación de la UE**
- **Número del seguro social (SSN) de la UE o identificación equivalente**
- **Número de identificación fiscal (NIF) de la UE**
- **Código de identificación de la población tailandesa**
- **Número de identificación nacional turco**
- **Número de la tarjeta de residencia japonesa**


Los siguientes tipos de información confidencial requieren la versión preliminar actual del cliente de Azure Information Protection:

- **Cadena de conexión de Azure Service Bus**
- **Cadena de conexión de Azure IoT**
- **Cuenta de almacenamiento de Azure**
- **Cadena de conexión de base de datos IaaS de Azure y cadena de conexión de SQL Azure**
- **Cadena de conexión de Azure Redis Cache**
- **Azure SAS**
- **Cadena de conexión de SQL Server**
- **Clave de autenticación de Azure DocumentDB**
- **Contraseña de configuración de publicación de Azure**
- **Clave de la cuenta de almacenamiento de Azure (genérica)**

Además, no se admiten los siguientes tipos de información confidencial para la versión preliminar actual del cliente de Azure Information Protection y ya no se muestran en Azure Portal:

- **Número de teléfono de la UE**
- **Coordenadas GPS de la UE**

## <a name="next-steps"></a>Pasos siguientes

Considere la posibilidad de implementar el [analizador de Azure Information Protection](deploy-aip-scanner.md), que puede usar las reglas de clasificación automática para detectar, clasificar y proteger archivos en recursos compartidos de red y almacenes de archivos locales.  

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).


