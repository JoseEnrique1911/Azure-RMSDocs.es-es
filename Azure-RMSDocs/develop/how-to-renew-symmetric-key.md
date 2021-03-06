---
title: Renovación de la clave simétrica de Azure Information Protection
description: En este artículo se describe el proceso de renovación de una clave simétrica en Azure Information Protection.
keywords: ''
author: bryanla
manager: barbkess
ms.author: bryanla
ms.date: 03/27/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: a0b8c8f0-6ed5-48bb-8155-ac4f319ec178
ms.openlocfilehash: 8ddb8d23ad2258aaee5e2d2d7c8c949599b9abf7
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56257916"
---
# <a name="how-to-renew-the-symmetric-key-in-azure-information-protection"></a>Instrucciones: Renovación de la clave simétrica de Azure Information Protection

Una **clave simétrica** es un secreto que cifra y descifra un mensaje en criptografía de clave simétrica.  

En Azure Active Directory (Azure AD), al crear un objeto de entidad de servicio para representar una aplicación, el proceso genera también una clave simétrica de 256 bits para comprobar la aplicación. Esta clave simétrica es válida durante un año de forma predeterminada. 

En los pasos siguientes se muestra cómo renovar la clave simétrica. 

## <a name="prerequisites"></a>Requisitos previos

* El módulo Azure Active Directory (Azure AD) Powershell debe instalarse como se indica en la [referencia de Azure AD Powershell](https://docs.microsoft.com/powershell/msonline/).


## <a name="renewing-the-symmetric-key-after-expiry"></a>Renovación de la clave simétrica una vez que ha expirado

Una vez que ha expirado la clave simétrica asociada a la aplicación, no tiene que crear una nueva entidad de servicio. En su lugar, puede usar los [cmdlets de PowerShell](https://docs.microsoft.com/powershell/module/msonline) que proporciona Microsoft Online Services (MSol) para emitir una nueva clave simétrica para una entidad de servicio existente.

Para ilustrar este proceso, supongamos que ya ha creado una entidad de servicio mediante el comando [`New-MsolServicePrincipal`](https://docs.microsoft.com/powershell/msonline/v1/new-msolserviceprincipalcredential).

```
New-MsolServicePrincipalCredential -ServicePrincipalName "SupportExampleApp"
```

El proceso de creación crea una clave simétrica y un elemento **AppPrincipalId** tal como se muestra.

```
The following symmetric key was created as one was not supplied
ZYbF/lTtwE28qplQofCpi2syWd11D83+A3DRlb2Jnv8=

DisplayName : SupportExampleApp
ServicePrincipalNames : {7d9c1f38-600c-4b4d-8249-22427f016963}
ObjectId : 0ee53770-ec86-409e-8939-6d8239880518
AppPrincipalId : 7d9c1f38-600c-4b4d-8249-22427f016963
TrustedForDelegation : False
AccountEnabled : True
Addresses : []
KeyType : Symmetric
KeyId : acb9ad1b-36ce-4a7d-956c-40e5ac29dcbe
StartDate : 3/22/2017 3:27:53 PM
EndDate : 3/22/2018 3:27:53 PM
Usage : Verify
```

Esta clave simétrica expira el 22/3/2018 a las 3:27:53 p. m. Para usar la entidad de servicio después de este momento, debe renovar la clave simétrica. Para ello, use el comando [`New-MsolServicePrincipalCredential`](https://docs.microsoft.com/powershell/msonline/v1/new-msolserviceprincipalcredential). 

```
New-MsolServicePrincipalCredential -AppPrincipalId 7d9c1f38-600c-4b4d-8249-22427f016963
```

De esta forma, se crea una clave simétrica para el **AppPrincipalId** especificado.

```
The following symmetric key was created as one was not supplied ON8YYaMYNmwSfMX625Ei4eC6N1zaeCxbc219W090v28-
```
Puede usar el comando [`GetMsolServicePrincipalCredential`](https://docs.microsoft.com/powershell/msonline/v1/get-msolserviceprincipalcredential) para comprobar que la nueva clave simétrica esté asociada a la entidad de servicio correcta tal y como se muestra. Tenga en cuenta que el comando muestra todas las claves que están asociadas actualmente a la entidad de servicio.

```
Get-MsolServicePrincipalCredential -AppPrincipalId 7d9c1f38-600c-4b4d-8249-22427f016963 -ReturnKeyValues $true

Type : Symmetric
Value :
KeyId : c1ac145f-e899-4c90-8a02-2cef40054fc5
StartDate : 3/24/2017 10:11:07 PM
EndDate : 3/24/2018 10:11:07 PM
Usage : Verify

Type : Symmetric
Value :
KeyId : acb9ad1b-36ce-4a7d-956c-40e5ac29dcbe
StartDate : 3/22/2017 3:27:53 PM
EndDate : 3/22/2018 3:27:53 PM
Usage : Verify
```

Una vez que haya comprobado que la clave simétrica está realmente asociada a la entidad de servicio adecuada, puede actualizar los parámetros de autenticación de la entidad de servicio con la nueva clave. 

Después, puede quitar la clave simétrica antigua mediante el comando [`Remove-MsolServicePrincipalCredential`](https://docs.microsoft.com/powershell/msonline/v1/remove-msolserviceprincipalcredential) y comprobar que se haya quitado la clave mediante el comando `Get-MsolServicePrincipalCredential`.

```
Remove-MsolServicePrincipalCredential -KeyId acb9ad1b-36ce-4a7d-956c-40e5ac29dcbe -ObjectId 0ee53770-ec86-409e-8939-6d8239880518
```

## <a name="related-topics"></a>Temas relacionados

* [Habilitación de la aplicación de servicio para que funcione con RMS basado en la nube](how-to-use-file-api-with-aadrm-cloud.md)
* [Azure Active Directory MSOnline Powershell reference](https://docs.microsoft.com/powershell/msonline/) (Referencia de Azure Active Directory MSOnline PowerShell)
