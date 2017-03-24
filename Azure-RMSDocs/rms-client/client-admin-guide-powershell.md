---
title: Uso de PowerShell con el cliente de Azure Information Protection
description: "Instrucciones e información para que los administradores administren el cliente de Azure Information Protection con PowerShell."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/09/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4f9d2db7-ef27-47e6-b2a8-d6c039662d3c
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 13bed15fa5fff020d77a4362e38903c5ca55d2ce
ms.sourcegitcommit: cbdbabd626fa5b91c418d84cd6228c9ca94a2525
translationtype: HT
---
# <a name="using-powershell-with-the-azure-information-protection-client"></a>Uso de PowerShell con el cliente de Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8 y Windows 7 con SP1*

Cuando se instala el cliente de Azure Information Protection, los comandos de PowerShell se instalan automáticamente para que pueda administrar el cliente mediante la ejecución de comandos que puede incluir en los scripts para la automatización.

Los cmdlets se instalan con el módulo de PowerShell **AzureInformationProtection**, que reemplaza al módulo RMSProtection que se instaló con la herramienta de protección de RMS. Si tiene instalada la herramienta RMSProtection al instalar el cliente de Azure Information Protection, el módulo RMSProtection se desinstala automáticamente.

El módulo AzureInformationProtection incluye todos los cmdlets de Rights Management de la herramienta de protección de RMS y dos nuevos cmdlets que usan el servicio Azure Information Protection (AIP) para etiquetado:

|Cmdlet de etiquetado|Ejemplo de uso|
|----------------|---------------|
|[Get-AIPFileStatus](/powershell/azureinformationprotection/vlatest/get-aipfilestatus)|Para una carpeta compartida, identifique todos los archivos con una etiqueta específica.|
|[Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel)|Para una carpeta compartida, aplique una etiqueta específica a todos los archivos que no tienen ninguna etiqueta.|

Para obtener una lista de todos los cmdlets y su ayuda correspondiente, consulte [Módulo AzureInformationProtection](/powershell/azureinformationprotection/vlatest/aip).

Este módulo se instala en **\Archivos de programa (x86)\Microsoft Azure Information Protection** y agrega esta carpeta a la variable del sistema **PSModulePath**. El archivo .dll de este módulo se denomina **AIP.dll**.

Como con el módulo RMSProtection, la versión actual del módulo AzureInformationProtection tiene las siguientes limitaciones:

- Puede desproteger carpetas personales de Outlook (archivos .pst), pero actualmente no puede proteger de forma nativa estos archivos u otros archivos de contenedor con el uso de este módulo de PowerShell.

- Puede desproteger los mensajes de correo electrónico de Outlook protegidos (archivos .rpmsg) cuando están en una carpeta personal (.pst) de Outlook, pero no puede desproteger archivos .rpmsg fuera de una carpeta personal.

Antes de empezar a usar estos cmdlets, vea los requisitos previos adicionales y las instrucciones aplicables a su implementación:

- [Servicio Azure Information Protection y servicio Azure Rights Management](#azure-information-protection-service-and-azure-rights-management-service)

    - Aplicable si usa solo la clasificación o la clasificación con Rights Management Protection: tiene una suscripción que incluye Azure Information Protection (por ejemplo, Enterprise Mobility + Security).
    - Aplicable si usa solo la protección con el servicio Azure Rights Management: tiene una suscripción que incluye el servicio Azure Rights Management (por ejemplo, Office 365 E3 y Office 365 E5).

- [Active Directory Rights Management Services](#active-directory-rights-management-services)

    - Aplicable si usa solo la protección con la versión local de Azure Rights Management; Active Directory Rights Management Services (AD RMS).


## <a name="azure-information-protection-service-and-azure-rights-management-service"></a>Servicio Azure Information Protection y servicio Azure Rights Management

Lea esta sección antes de empezar a usar los comandos de PowerShell si su organización usa Azure Information Protection y el servicio de protección de datos Azure Rights Management, o solo el servicio Azure Rights Management.


### <a name="prerequisites-for-aip-and-azure-rms"></a>Requisitos previos para AIP y Azure RMS

Además de los requisitos previos para instalar el módulo AzureInformationProtection, existen requisitos previos adicionales para el servicio Azure Information Protection y el servicio de protección de datos Azure Rights Management:

1. El servicio Azure Rights Management debe estar activado.

2. Para quitar la protección de los archivos para otros usuarios con su propia cuenta: la característica de superusuario debe habilitarse para su organización y su cuenta debe estar configurada para interactuar como superusuario en Azure Rights Management.

3. Para proteger o desproteger archivos directamente sin interacción del usuario: cree una cuenta de entidad de servicio, ejecute RMSServerAuthentication y considere la posibilidad establecer dicha entidad de servicio como un superusuario para Azure Rights Management.

4. Para regiones fuera de Estados Unidos: edite el registro para la autenticación en el servidor.

#### <a name="prerequisite-1-the-azure-rights-management-service-must-be-activated"></a>Requisito previo 1: el servicio Azure Rights Management debe estar activado

Este requisito previo se aplica si utiliza la protección de datos mediante etiquetas o con una conexión directa al servicio Azure Rights Management configurado para aplicar la protección de datos.

Si no está activado el inquilino de Azure Information Protection, vea las instrucciones en [Activar Azure Rights Management](../deploy-use/activate-service.md).

#### <a name="prerequisite-2-to-remove-protection-from-files-for-others-using-your-own-account"></a>Requisito previo 2: quitar la protección de archivos para otros usuarios con su propia cuenta

Los escenarios típicos para quitar la protección de archivos para otros usuarios incluyen la detección de datos o la recuperación de datos. Si usa etiquetas para aplicar la protección, puede quitar la protección estableciendo una nueva etiqueta que no aplica protección o quitando la etiqueta. Pero lo mejor es que se conecte directamente al servicio Azure Rights Management para quitar la protección.

Debe tener permisos de Rights Management para quitar la protección de archivos, o bien ser un superusuario. Para la detección o recuperación de datos, suele usarse la característica de superusuario. Para habilitar esta característica y configurar su cuenta como un superusuario, vea [Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos](../deploy-use/configure-super-users.md).

#### <a name="prerequisite-3-to-protect-or-unprotect-files-without-user-interaction"></a>Requisito previo 3: proteger o desproteger archivos sin interacción del usuario

Actualmente, no se pueden aplicar etiquetas de forma no interactiva, pero puede conectarse directamente al servicio Azure Rights Management de forma no interactiva para proteger o desproteger archivos.

Debe utilizar una entidad de servicio para conectarse al servicio Azure Rights Management de forma no interactiva, para lo que debe usar el cmdlet `Set-RMSServerAuthentication`. Debe hacerlo para cada sesión de Windows PowerShell que ejecuta cmdlets que se conectan directamente al servicio Azure Rights Management. Antes de ejecutar este cmdlet, asegúrese de que dispone de estos tres identificadores:

- BposTenantId

- AppPrincipalId

- Clave simétrica

En las secciones siguientes se explica cómo obtener estos identificadores.

##### <a name="to-get-the-bpostenantid"></a>Para obtener BposTenantId

Ejecute el cmdlet Get-AadrmConfiguration desde el módulo de Windows PowerShell para Azure RMS:

1. Si este módulo aún no está instalado en el equipo, vea [Instalación de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

2. Inicie Windows PowerShell con la opción **Ejecutar como administrador**.

3. Use el cmdlet `Connect-AadrmService` para conectarse al servicio Azure Rights Management:
    
        Connect-AadrmService
    
    Cuando se le pida, escriba las credenciales de administrador de inquilinos de Azure Information Protection (normalmente, usará una cuenta de administrador global de Office 365 o Azure Active Directory).
    
4. Ejecute `Get-AadrmConfiguration` y realice una copia del valor BPOSId.
    
    A continuación se muestra un ejemplo de salida de Get-AadrmConfiguration:
    
            BPOSId                                   : 23976bc6-dcd4-4173-9d96-dad1f48efd42
        
            RightsManagement ServiceId               : 1a302373-f233-440600909-4cdf305e2e76
        
            LicensingIntranetDistributionPointUrl    : https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/licensing
        
            LicensingExtranetDistributionPointUrl    : https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/licensing
        
            CertificationIntranetDistributionPointUrl: https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/certification
        
            CertificationExtranetDistributionPointUrl: https://1s302373-f233-4406-9090-4cdf305e2e76.rms.na.aadrm.com/_wmcs/certification

5. Desconéctese del servicio:
    
        Disconnect-AadrmService

##### <a name="to-get-the-appprincipalid-and-symmetric-key"></a>Para obtener AppPrincipalId y la clave simétrica

Cree una entidad de servicio nueva mediante la ejecución del cmdle `New-MsolServicePrincipal` desde el módulo MSOnline de PowerShell para Azure Active Directory, o `New-AzureADServicePrincipal` desde el último módulo de PowerShell, versión 2, de Azure Active Directory. 

Las siguientes instrucciones son para New-MsolServicePrincipal desde el módulo MSOnline de PowerShell para Azure Active Directory:

1. Si este módulo aún no está instalado en el equipo, vea [Install the Azure AD Module](/powershell/azuread/#install-the-azure-ad-module) (Instalación del módulo para Azure AD).

2. Inicie Windows PowerShell con la opción **Ejecutar como administrador**.

3. Utilice el cmdlet **Connect-MsolService** para conectarse a Azure AD:
    
        Connect-MsolService
    
    Cuando se le pida, escriba las credenciales de administrador de inquilinos de Azure AD (normalmente, usará una cuenta de administrador global de Office 365 o Azure Active Directory).

4. Ejecute el cmdlet New-MsolServicePrincipal para crear una nueva entidad de servicio:
    
        New-MsolServicePrincipal
    
    Cuando se le solicite, escriba el nombre para mostrar que haya elegido para esta entidad de servicio que le ayudará a identificar su propósito más adelante como una cuenta para conectarse al servicio Azure Rights Management, a fin de que pueda proteger y desproteger archivos.
    
    Un ejemplo de la salida de New-MsolServicePrincipal:
    
        Supply values for the following parameters:
        
        DisplayName: AzureRMSProtectionServicePrincipal
        The following symmetric key was created as one was not supplied
        zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=
        
        Display Name: AzureRMSProtectionServicePrincipal
        ServicePrincipalNames: (b5e3f7g1-b5c2-4c96-a594-a0807f65bba4)
        ObjectId: 23720996-593c-4122-bfc7-1abb5a0b5109
        AppPrincialId: b5e3f76a-b5c2-4c96-a594-a0807f65bba4
        TrustedForDelegation: False
        AccountEnabled: True
        Addresses: ()
        KeyType: Symmetric
        KeyId: 8ef61651-ca11-48ea-a350-25834a1ba17c
        StartDate: 3/7/2014 4:43:59 AM
        EndDate: 3/7/2014 4:43:59 AM
        Usage: Verify

5. En esta salida, tome nota de la clave simétrica y de AppPrincipalId.

    Es especialmente importante realizar una copia de la clave simétrica, ya que no se puede recuperar totalmente más adelante; por tanto, si no la recuerda, tendrá que crear otra entidad de servicio la próxima vez que necesite autenticarse en el servicio Azure Rights Management.

A partir de estas instrucciones y de los ejemplos expuestos, se dispone de tres identificadores necesarios para ejecutar Set-RMSServerAuthentication:

- Id. de inquilino: **23976bc6-dcd4-4173-9d96-dad1f48efd42**

- Clave simétrica: **zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=**

- AppPrincipalId: **b5e3f76a-b5c2-4c96-a594-a0807f65bba4**

El comando de ejemplo presentará el siguiente aspecto:

    Set-RMSServerAuthentication -Key zIeMu8zNJ6U377CLtppkhkbl4gjodmYSXUVwAO5ycgA=-AppPrincipalId b5e3f76a-b5c2-4c96-a594-a0807f65bba4-BposTenantId 23976bc6-dcd4-4173-9d96-dad1f48efd42

Tal como se muestra en el comando anterior, puede proporcionar los valores con un solo comando, o simplemente escribir Set-RMSServerAuthentication y proporcionar los valores uno a uno cuando se le solicite. Cuando el comando finaliza, aparece el mensaje "**The RmsServerAuthentication is set to ON**" (RmsServerAuthentication está activado), lo que significa que ahora puede proteger y desproteger archivos con la entidad de servicio.

Considere la posibilidad de establecer la entidad de servicio como superusuario: para asegurarse de que esta entidad de servicio siempre pueda desproteger los archivos para otros usuarios, se puede configurar como superusuario. Del mismo modo que configura una cuenta de usuario estándar como superusuario, utilice el mismo cmdlet de Azure RMS, [Add-AadrmSuperUser](/powershell/aadrm/vlatest/Add-AadrmSuperUser.md), pero especifique el parámetro **-ServicePrincipalId** con el valor de AppPrincipalId.

Para más información, vea [Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos](../deploy-use/configure-super-users.md).

> [!NOTE]
> Para utilizar su propia cuenta para autenticarse en el servicio Azure Rights Management, no hay necesidad de ejecutar Set-RMSServerAuthentication antes de proteger o desproteger archivos u obtener plantillas.

#### <a name="prerequisite-4-for-regions-outside-north-america"></a>Requisito previo 4: Para las regiones fuera de Estados Unidos

Para la autenticación fuera de la región de Estados Unidos de Azure, debe modificar el registro de la siguiente manera. Si el inquilino de Azure Information Protection está en Estados Unidos, no siga este paso:

1. Vuelva a ejecutar el cmdlet Get-AadrmConfiguration y anote los valores de **CertificationExtranetDistributionPointUrl** y **LicensingExtranetDistributionPointUrl**.

2. En cada equipo donde se van a ejecutar los cmdlets AzureInformationProtection, abra el Editor del Registro y vaya a: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC`

3. Si no ve una clave **ServiceLocation**, créela, para que la ruta de acceso al registro aparezca como **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation**

4. Para la clave **ServiceLocation**, cree dos claves si no existen, denominadas **EnterpriseCertification** y **EnterprisePublishing**. 
    
    Al crear estas claves REG_SZ, no cambie el nombre de "(Default)", pero modifíquelas para establecer los datos del valor:

    - Para **EnterpriseCertification**, pegue el valor de CertificationExtranetDistributionPointUrl.
    
    - Para **EnterprisePublishing**, pegue el valor de LicensingExtranetDistributionPointUrl.

5. Cierre el Editor del Registro. No es necesario reiniciar el equipo. Sin embargo, si usa una cuenta de entidad de servicio en lugar de su propia cuenta de usuario, debe ejecutar el comando Set-RMSServerAuthentication después realizar esta modificación del registro.

### <a name="example-scenarios-for-using-the-cmdlets-for-azure-information-protection-and-the-azure-rights-management-service"></a>Escenarios de ejemplo para usar los cmdlets de Azure Information Protection y del servicio Azure Rights Management

Resulta más eficaz utilizar etiquetas para clasificar y proteger archivos, porque solo necesita dos cmdlets, que se pueden ejecutar de forma autónoma o conjunta: [Get-AIPFileStatus](/powershell/azureinformationprotection/vlatest/get-aipfilestatus) y [Set-AIPFileLabel](/powershell/azureinformationprotection/vlatest/set-aipfilelabel). Recurra a la ayuda de ambos cmdlets para obtener más información y ejemplos.

Sin embargo, para proteger o desproteger archivos conectándose directamente al servicio Azure Rights Management, normalmente debe ejecutar una serie de cmdlets como se describe a continuación.

En primer lugar, si necesita autenticarse en el servicio Azure Rights Management con una entidad de servicio en lugar de utilizar su propia cuenta, en una sesión de PowerShell, escriba:

    Set-RMSServerAuthentication

Cuando se le solicite, escriba los tres identificadores como se describe en [Requisito previo 3: proteger o desproteger archivos sin interacción del usuario](client-admin-guide-powershell.md#prerequisite-3-to-protect-or-unprotect-files-without-user-interaction).

Para poder proteger los archivos, debe descargar las plantillas de Rights Management en el equipo e identificar la que se usará y el número de identificador correspondiente. En la salida, puede copiar el identificador de plantilla:

    Get-RMSTemplate
    
La salida puede ser parecida a la siguiente:

    TemplateId        : {82bf3474-6efe-4fa1-8827-d1bd93339119}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content cannot be modified.
    Name              : Contoso, Ltd - Confidential View Only
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    
    TemplateId        : {e6ee2481-26b9-45e5-b34a-f744eacd53b0}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content can be modified but cannot be copied and printed.
    Name              : Contoso, Ltd - Confidential
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    FromTemplate      : True

Tenga en cuenta que si no ejecuta el comando Set-RMSServerAuthentication, se autenticará en el servicio Azure Rights Management con su propia cuenta de usuario. Si interactúa con un equipo que no está unido a un dominio, las credenciales actuales siempre se usarán automáticamente. En cambio, si trabaja con un equipo de un grupo de trabajo, se le pedirá que inicie sesión en Azure, y estas credenciales se almacenan en la memoria caché para los comandos ulteriores. En este escenario, si más adelante necesita iniciar sesión como un usuario distinto, use el cmdlet `Clear-RMSAuthentication`.

Ahora que ya sabe el identificador de plantilla, puede utilizarlo con el cmdlet `Protect-RMSFile` para proteger un único archivo o todos los archivos de una carpeta. Por ejemplo, si desea proteger un único archivo y sobrescribir el original con el uso de la plantilla de "Contoso, Ltd - Confidencial":

    Protect-RMSFile -File C:\Test.docx -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

La salida puede ser parecida a la siguiente:

    InputFile             EncryptedFile
    ---------             -------------
    C:\Test.docx          C:\Test.docx

Para proteger todos los archivos de una carpeta, use el parámetro **-Folder** con una letra de unidad y la ruta de acceso, o la ruta de acceso UNC. Por ejemplo:

    Protect-RMSFile -Folder \Server1\Documents -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

La salida puede ser parecida a la siguiente:

    InputFile                          EncryptedFile
    ---------                          -------------
    \Server1\Documents\Test1.docx     \Server1\Documents\Test1.docx
    \Server1\Documents\Test2.docx     \Server1\Documents\Test2.docx
    \Server1\Documents\Test3.docx     \Server1\Documents\Test3.docx
    \Server1\Documents\Test4.docx     \Server1\Documents\Test4.docx

Si la extensión de nombre de archivo no cambia después de aplicar la protección, siempre se puede utilizar el cmdlet `Get-RMSFileStatus` más adelante para comprobar si el archivo está protegido. Por ejemplo:

    Get-RMSFileStatus -File \Server1\Documents\Test1.docx

La salida puede ser parecida a la siguiente:

    FileName                              Status
    --------                              ------
    \Server1\Documents\Test1.docx         Protected

Para desproteger un archivo, debe tener derechos de propietario o de extracción desde el momento en que se protegió el archivo, o bien debe ejecutar los cmdlets como superusuario. A continuación, use el cmdlet Unprotect. Por ejemplo:

    Unprotect-RMSFile C:\test.docx -InPlace

La salida puede ser parecida a la siguiente:

    InputFile                             DecryptedFile
    ---------                             -------------
    C:\Test.docx                          C:\Test.docx

Tenga en cuenta que si las plantillas de Rights Management cambian, debe volver a descargarlas con `Get-RMSTemplate -force`. 

## <a name="active-directory-rights-management-services"></a>Active Directory Rights Management Services

Lea esta sección antes de empezar a utilizar los comandos de PowerShell para proteger o desproteger archivos si su organización usa simplemente Active Directory Rights Management Services.


### <a name="prerequisites-for-ad-rms"></a>Requisitos previos para AD RMS

Además de los requisitos previos para instalar el módulo AzureInformationProtection, su cuenta debe tener permisos de lectura y ejecución para acceder a ServerCertification.asmx:

1. Inicie sesión en un servidor de AD RMS.

2. Haga clic en **Inicio** y luego en **Equipo**.

3. En el Explorador de archivos, vaya a %systemdrive%\Initpub\wwwroot\_wmsc\Certification.

4. Haga clic con el botón derecho en **ServerCertification.asmx** y luego haga clic en **Propiedades**.

5. En el cuadro de diálogo **Propiedades de ServerCertification.asmx**, haga clic en la pestaña **Seguridad**. 

6. Haga clic en los botones **Continuar** o **Editar**. 

7. En el cuadro de diálogo **Permissions for ServerCertification.asmx** (Permisos para ServerCertification.asmx), haga clic en **Agregar**. 

8. Agregue el nombre de cuenta. Si otros administradores de AD RMS también van a usar estos cmdlets para proteger y desproteger archivos, agregue también sus nombres.

9. En la columna **Permitir**, asegúrese de que las casillas **Leer y ejecutar** y **Leer** estén activadas.

10. Haga clic en **Aceptar** dos veces.

### <a name="example-scenarios-for-using-the-cmdlets-for-active-directory-rights-management-services"></a>Escenarios de ejemplo para usar los cmdlets para Active Directory Rights Management Services

Un escenario típico para estos cmdlets es proteger todos los archivos de una carpeta mediante una plantilla de directiva de permisos, o bien desproteger un archivo. 

En primer lugar, si tiene más de una implementación de AD RMS, necesitará los nombres de los servidores de AD RMS, que puede obtener con el cmdlet Get-RMSServer para mostrar una lista de los servidores disponibles:

    Get-RMSServer

La salida puede ser parecida a la siguiente:

    Number of RMS Servers that can provide templates: 2 
    ConnectionInfo             DisplayName          AllowFromScratch
    --------------             -------------        ----------------
    Microsoft.InformationAnd…  RmsContoso                       True
    Microsoft.InformationAnd…  RmsFabrikam                      True

Para poder proteger los archivos, debe obtener una lista de las plantillas de RMS para identificar cuál va a usar y el número de identificador correspondiente. Solo necesita especificar también el servidor de RMS cuando tiene más de una implementación de AD RMS. 

En la salida, puede copiar el identificador de plantilla:

    Get-RMSTemplate -RMSServer RmsContoso

La salida puede ser parecida a la siguiente:

    TemplateId        : {82bf3474-6efe-4fa1-8827-d1bd93339119}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content cannot be modified.
    Name              : Contoso, Ltd - Confidential View Only
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    
    
    TemplateId        : {e6ee2481-26b9-45e5-b34a-f744eacd53b0}
    CultureInfo       : en-US
    Description       : This content is proprietary information intended for internal users only. This content can be modified but cannot be copied and printed.
    Name              : Contoso, Ltd - Confidential
    IssuerDisplayName : Contoso, Ltd
    FromTemplate      : True
    FromTemplate      : True

Ahora que ya sabe el identificador de plantilla, puede utilizarlo con el cmdlet Protect-RMSFile para proteger un único archivo o todos los archivos de una carpeta. Por ejemplo, si desea proteger un único archivo y reemplazar el original con el uso de la plantilla de "Contoso, Ltd - Confidencial":

    Protect-RMSFile -File C:\Test.docx -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

La salida puede ser parecida a la siguiente:

    InputFile             EncryptedFile
    ---------             -------------
    C:\Test.docx          C:\Test.docx   

Para proteger todos los archivos de una carpeta, use el parámetro -Folder con una letra de unidad y la ruta de acceso, o la ruta de acceso UNC. Por ejemplo:

    Protect-RMSFile -Folder \\Server1\Documents -InPlace -TemplateId e6ee2481-26b9-45e5-b34a-f744eacd53b0

La salida puede ser parecida a la siguiente:

    InputFile                          EncryptedFile
    ---------                          -------------
    \\Server1\Documents\Test1.docx     \\Server1\Documents\Test1.docx   
    \\Server1\Documents\Test2.docx     \\Server1\Documents\Test2.docx   
    \\Server1\Documents\Test3.docx     \\Server1\Documents\Test3.docx   
    \\Server1\Documents\Test4.docx     \\Server1\Documents\Test4.docx   

Si la extensión de nombre de archivo no cambia después de aplicar la protección de RMS, siempre se puede utilizar el cmdlet Get-RMSFileStatus más adelante para comprobar si el archivo está protegido. Por ejemplo: 

    Get-RMSFileStatus -File \\Server1\Documents\Test1.docx

La salida puede ser parecida a la siguiente:

    FileName                              Status
    --------                              ------
    \\Server1\Documents\Test1.docx        Protected

Para desproteger un archivo, debe tener derechos de propietario o de extracción desde el momento en que se protegió el archivo, o bien debe estar configurado como superusuario para AD RMS. A continuación, use el cmdlet Unprotect. Por ejemplo:

    Unprotect-RMSFile C:\test.docx -InPlace

La salida puede ser parecida a la siguiente:

    InputFile                             DecryptedFile
    ---------                             -------------
    C:\Test.docx                          C:\Test.docx


## <a name="next-steps"></a>Pasos siguientes
Para acceder a la ayuda de un cmdlet en una sesión de PowerShell, use el cmdlet Get-Help <cmdlet name>, donde <cmdlet name> es el nombre del cmdlet que desea investigar. Por ejemplo: 

    Get-Help Get-RMSTemplate

Vea la información adicional siguiente que puede necesitar para la compatibilidad con el cliente de Azure Information Protection:

- [Archivos de cliente y registro de uso](client-admin-guide-files-and-logging.md)

- [Seguimiento de documentos](client-admin-guide-document-tracking.md)

- [Tipos de archivos admitidos](client-admin-guide-file-types.md)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]