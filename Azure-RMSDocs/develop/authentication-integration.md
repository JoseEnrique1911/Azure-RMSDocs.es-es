---
title: Registro de la aplicación con Azure AD - AIP
description: Se describen los conceptos básicos de la autenticación de usuario de la aplicación habilitada para RMS.
keywords: ''
author: bryanla
ms.author: bryanla
manager: barbkess
ms.date: 03/13/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 200D9B23-F35D-4165-9AC4-C482A5CE1D28
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.openlocfilehash: 0376665dfe09a6a29d33c414deedf79ed215bb6d
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56258528"
---
# <a name="how-to-register-and-rms-enable-your-app-with-azure-ad"></a>Cómo registrar y habilitar para RMS la aplicación con Azure AD

Este tema le guiará a través de los aspectos básicos del registro de aplicaciones y la habilitación de RMS mediante el Portal de Azure seguido de la autenticación de usuario con Azure Active Directory Authentication Library (ADAL).

## <a name="what-is-user-authentication"></a>¿Qué es la autenticación del usuario?
La autenticación de usuario es un paso esencial para establecer la comunicación entre la aplicación del dispositivo y la infraestructura de RMS. En este proceso de autenticación se usa el protocolo OAuth 2.0 estándar que necesita la información principal sobre el usuario actual y la solicitud de autenticación.

## <a name="registration-via-azure-portal"></a>Registro mediante el Portal de Azure
Para comenzar, siga esta guía para la configuración del registro de aplicaciones a través del Portal de Azure, [Configure Azure RMS for ADAL authentication (Configuración de Azure RMS para la autenticación ADAL)](adal-auth.md). Asegúrese de copiar y guardar el **Identificador de cliente** y el **URI de redirección** de este proceso para usarlos posteriormente.

## <a name="complete-your-information-protection-integration-agreement-ipia"></a>Completar un Contrato de integración de Information Protection (IPIA)
Antes de implementar la aplicación, debe completar un IPIA con el equipo de Microsoft Information Protection. Para información detallada, vea la primera sección del tema [Implementación en el entorno de producción](deploying-your-application.md).

## <a name="implement-user-authentication-for-your-app"></a>Implementar la autenticación de usuario para su aplicación
Cada API de RMS tiene una devolución de llamada que se debe implementar para habilitar la autenticación de usuario. Después, RMS SDK 4.2 usará su implementación de la devolución de llamada cuando no proporcione un token de acceso, cuando el token de acceso deba actualizarse o cuando el token de acceso haya expirado.

- Android: interfaces [AuthenticationRequestCallback](https://msdn.microsoft.com/library/dn758255.aspx) y [AuthenticationCompletionCallback](https://msdn.microsoft.com/library/dn758250.aspx).
- iOS / OS X: protocolo [MSAuthenticationCallback](https://msdn.microsoft.com/library/dn758312.aspx).
-  Windows Phone / Window RT: interfaz [IAuthenticationCallback](https://msdn.microsoft.com/library/microsoft.rightsmanagement.iauthenticationcallback.aspx).
- Linux: interfaz [IAuthenticationCallback](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1IAuthenticationCallback.html).

### <a name="what-library-to-use-for-authentication"></a>¿Qué biblioteca hay que usar para la autenticación?
Para implementar la devolución de llamada de autenticación, debe descargar una biblioteca adecuada y configurar el entorno de desarrollo para que la use. Encontrará las bibliotecas de ADAL en GitHub para cada una de las plataformas correspondientes.

Los siguientes recursos contienen instrucciones para configurar el entorno y usar la biblioteca.

-   [Windows Azure Active Directory Authentication Library (ADAL) for iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/) (Biblioteca de autenticación de Windows Azure Active Directory (ADAL) para iOS)
-   [Windows Azure Active Directory Authentication Library (ADAL) for Mac](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios/) (Biblioteca de autenticación de Windows Azure Active Directory (ADAL) para Mac)
-   [Windows Azure Active Directory Authentication Library (ADAL) for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android) (Biblioteca de autenticación de Windows Azure Active Directory (ADAL) para Android)
-   [Windows Azure Active Directory Authentication Library (ADAL) for dotnet](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet) (Biblioteca de autenticación de Windows Azure Active Directory (ADAL) para dotnet)
-   En cuanto al SDK de Linux, la biblioteca de ADAL viene empaquetada con el origen del SDK, disponible en [Github](https://github.com/AzureAD/rms-sdk-for-cpp).

> [!NOTE]
> Se recomienda usar una de las ADAL, aunque use otras bibliotecas de autenticación.

### <a name="authentication-parameters"></a>Parámetros de autenticación

ADAL necesita varias informaciones para autenticar correctamente un usuario en Azure RMS (o AD RMS). Estos son parámetros de OAuth 2.0 estándar que se suelen necesitar de cualquier aplicación de Azure AD. Encontrará las instrucciones actuales de uso de ADAL en el archivo Léame de los repositorios de Github correspondientes mencionados anteriormente.

- **Autoridad:** dirección URL del punto de conexión de autenticación, normalmente AAD o ADFS.
- **Recurso:** dirección URL o URI de la aplicación de servicio a la que se intenta tener acceso, normalmente Azure RMS o AD RMS.
- **Identificador de usuario:** UPN (normalmente, la dirección de correo) del usuario que quiere tener acceso a la aplicación. Este parámetro puede estar vacío si aún no se conoce el usuario. También se usa para almacenar en caché el token de usuario o para pedir un token de la memoria caché. Se suele usar también como *pista* para preguntar al usuario.
- **Identificador de cliente:** identificador de la aplicación cliente. Debe ser un identificador de aplicación de Azure AD válido.
y proviene del paso de registro anterior mediante el Portal de Azure.
- **URI de redirección:** proporciona la biblioteca de autenticación con un destino de URI para el código de autenticación. Formatos específicos que se necesitan para iOS y Android. Estos se explican en los archivos Léame de los repositorios de GitHub correspondientes de ADAL. Este valor proviene del paso de registro anterior mediante el Portal de Azure.

> [!NOTE]
> El **ámbito** no se usa actualmente, pero no se descarta, de modo que está reservado para un futuro uso.

    Android: `msauth://packagename/Base64UrlencodedSignature`

    iOS: `<app-scheme>://<bundle-id>`

> [!NOTE]
> Si la aplicación no respeta estas instrucciones, probablemente los flujos de trabajo de Azure RMS y Azure AD no funcionen y sean incompatibles con Microsoft.com. Es más, se corre el riesgo de infringir el contrato de licencia de Rights Management si se usa un identificador de cliente no válido en una aplicación de producción.

### <a name="what-should-an-authentication-callback-implementation-look-like"></a>¿Qué apariencia debe tener una implementación de devolución de llamada de autenticación?
**Ejemplos de código de autenticación:** este SDK tiene código de ejemplo que muestra el uso de las devoluciones de llamada de autenticación. Para su comodidad, estos ejemplos de código se muestran aquí, así como en cada uno de los siguientes temas vinculados.

**Autenticación de usuario de Android:** para más información, en [Android code examples](android-code.md) (Ejemplos de código Android), vea el **paso 2** del primer escenario sobre cómo consumir un archivo protegido de RMS.


    class MsipcAuthenticationCallback implements AuthenticationRequestCallback
    {
    ...

    @Override
    public void getToken(Map<String, String> authenticationParametersMap,
                         final AuthenticationCompletionCallback authenticationCompletionCallbackToMsipc)
    {
        String authority = authenticationParametersMap.get("oauth2.authority");
        String resource = authenticationParametersMap.get("oauth2.resource");
        String userId = authenticationParametersMap.get("userId");
        mClientId = “12345678-ABCD-ABCD-ABCD-ABCDEFGHIJ”; // get your registered Azure AD application ID here
        mRedirectUri = “urn:ietf:wg:oauth:2.0:oob”;
        final String userHint = (userId == null)? "" : userId;
        AuthenticationContext authenticationContext = App.getInstance().getAuthenticationContext();
        if (authenticationContext == null || !authenticationContext.getAuthority().equalsIgnoreCase(authority))
        {
            try
            {
                authenticationContext = new AuthenticationContext(App.getInstance().getApplicationContext(), authority, …);
                App.getInstance().setAuthenticationContext(authenticationContext);
            }
            catch (NoSuchAlgorithmException e)
            {
                …
                authenticationCompletionCallbackToMsipc.onFailure();
            }
            catch (NoSuchPaddingException e)
            {
                …
                authenticationCompletionCallbackToMsipc.onFailure();
            }
       }
        App.getInstance().getAuthenticationContext().acquireToken(mParentActivity, resource, mClientId, mRedirectURI, userId, mPromptBehavior,
                       "&USERNAME=" + userHint, new AuthenticationCallback<AuthenticationResult>()
                        {
                            @Override
                            public void onError(Exception exc)
                            {
                                …
                                if (exc instanceof AuthenticationCancelError)
                                {
                                     …
                                    authenticationCompletionCallbackToMsipc.onCancel();
                                }
                                else
                                {
                                     …
                                    authenticationCompletionCallbackToMsipc.onFailure();
                                }
                            }

                            @Override
                            public void onSuccess(AuthenticationResult result)
                            {
                                …
                                if (result == null || result.getAccessToken() == null
                                        || result.getAccessToken().isEmpty())
                                {
                                     …
                                }
                                else
                                {
                                    // request is successful
                                    …
                                    authenticationCompletionCallbackToMsipc.onSuccess(result.getAccessToken());
                                }
                            }
                        });
                         }


**Autenticación de usuario de iOS/OS X**: para obtener más información, vea [iOS/OS X code examples (Ejemplos de código iOS/OS X)](ios-os-x-code-examples.md), *Paso 2 del primer escenario sobre cómo consumir un archivo protegido de RMS*.


    // AuthenticationCallback holds the necessary information to retrieve an access token.
    @interface MsipcAuthenticationCallback : NSObject<MSAuthenticationCallback>

    @end

    @implementation MsipcAuthenticationCallback

    - (void)accessTokenWithAuthenticationParameters:
         (MSAuthenticationParameters *)authenticationParameters
                                completionBlock:
         (void(^)(NSString *accessToken, NSError *error))completionBlock
    {
    ADAuthenticationError *error;
    ADAuthenticationContext* context = [ADAuthenticationContext authenticationContextWithAuthority:authenticationParameters.authority error:&error];

    NSString *appClientId = @”12345678-ABCD-ABCD-ABCD-ABCDEFGHIJ”;

    // get your registered Azure AD application ID here

    NSURL *redirectURI = [NSURL URLWithString:@”ms-sample://com.microsoft.sampleapp”];

    // get your <app-scheme>://<bundle-id> here
    // Retrieve token using ADAL
    [context acquireTokenWithResource:authenticationParameters.resource
                             clientId:appClientId
                          redirectUri:redirectURI
                               userId:authenticationParameters.userId
                      completionBlock:^(ADAuthenticationResult *result)
                      {
                          if (result.status != AD_SUCCEEDED)
                          {
                              NSLog(@"Auth Failed");
                              completionBlock(nil, result.error);
                          }
                          else
                          {
                              completionBlock(result.accessToken, result.error);
                          }
                      }

        ];
    }



**Autenticación de usuario de Linux**: para obtener más información, vea [Linux code examples (Ejemplos de código de Linux)](linux-c-code-examples.md).



    // Class Header
    class AuthCallback : public IAuthenticationCallback {
    private:

      std::shared_ptr<rmsauth::FileCache> FileCachePtr;
      std::string clientId_;
      std::string redirectUrl_;

      public:

      AuthCallback(const std::string& clientId,
               const std::string& redirectUrl);
      virtual std::string GetToken(shared_ptr<AuthenticationParameters>& ap) override;
    };

    class ConsentCallback : public IConsentCallback {
      public:

      virtual ConsentList Consents(ConsentList& consents) override;
    };

    // Class Implementation
    AuthCallback::AuthCallback(const string& clientId, const string& redirectUrl)
    : clientId_(clientId), redirectUrl_(redirectUrl) {
      FileCachePtr = std::make_shared<FileCache>();
    }

    string AuthCallback::GetToken(shared_ptr<AuthenticationParameters>& ap)
    {
      string redirect =
      ap->Scope().empty() ? redirectUrl_ : ap->Scope();

      try
      {
        if (redirect.empty()) {
        throw rmscore::exceptions::RMSInvalidArgumentException(
              "redirect Url is empty");
      }

      if (clientId_.empty()) {
      throw rmscore::exceptions::RMSInvalidArgumentException("client Id is empty");
      }

      AuthenticationContext authContext(
        ap->Authority(), AuthorityValidationType::False, FileCachePtr);

      auto result = authContext.acquireToken(ap->Resource(),
                                           clientId_, redirect,
                                           PromptBehavior::Auto,
                                           ap->UserId());
      return result->accessToken();
      }

      catch (const rmsauth::Exception& ex)
      {
        // out logs
        throw;
      }
    }
