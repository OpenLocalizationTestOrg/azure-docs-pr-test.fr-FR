---
title: "Obtention d’un jeton à l’aide d’une application iOS - Azure AD B2C | Microsoft Docs"
description: "Cet article vous indiquent comment toocreate une application iOS qui utilise AppAuth avec des identités d’utilisateur Azure Active Directory B2C toomanage et authentifie les utilisateurs."
services: active-directory-b2c
documentationcenter: ios
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: d818a634-42c2-4cbd-bf73-32fa0c8c69d3
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objectivec
ms.topic: article
ms.date: 03/07/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: e7cbe2de6e9ae3d45448cdd36292c457a0ef4887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a>Azure Active Directory B2C : Se connecter à l’aide d’une application iOS

plateforme d’identité Microsoft Hello utilise des normes ouvertes telles que OAuth2 et OpenID Connect. À l’aide d’un protocole standard ouvert propose plusieurs développeurs lors de la sélection d’un toointegrate de bibliothèque avec nos services. Nous vous avons fourni cette procédure pas à pas et autres similaires aux développeurs de tooaid avec l’écriture d’applications qui se connectent de plateforme de Microsoft Identity toohello. La plupart des bibliothèques qui implémentent [les spécifications hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) sont en mesure de tooconnect toohello Microsoft Identity plateforme.

> [!WARNING]
> Microsoft ne fournit pas de correctifs pour les bibliothèques tierces et ne les a pas vérifiées. Cet exemple utilise une bibliothèque tierce appelée AppAuth qui a été testé pour la compatibilité dans les scénarios de base avec hello Azure Active Directory B2C. Problèmes et des demandes de fonctionnalités doivent être projet open source de la bibliothèque toohello dirigée. Pour plus d’informations, consultez [cet article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).
>
>

Si vous êtes de nouveau tooOAuth2 ou OpenID Connect, une grande partie de cet exemple de configuration peut ne pas effectuer de tooyou sens. Nous vous recommandons de consulter un résumé [vue d’ensemble du protocole hello que nous avons présentés ici](active-directory-b2c-reference-protocols.md).

## <a name="get-an-azure-ad-b2c-directory"></a>Obtention d'un répertoire Azure AD B2C
Avant de pouvoir utiliser Azure AD B2C, vous devez créer un répertoire ou un client. Un répertoire est un conteneur destiné à recevoir tous vos utilisateurs, applications, groupes et autres. Si vous n’en possédez pas déjà un, [créez un répertoire B2C](active-directory-b2c-get-started.md) avant de continuer.

## <a name="create-an-application"></a>Création d'une application
Ensuite, vous devez toocreate une application dans votre répertoire B2C. inscription d’une application Hello fournit des informations de Azure AD lui toocommunicate en toute sécurité avec votre application. toocreate une application mobile, procédez comme [ces instructions](active-directory-b2c-app-registration.md). Veillez à effectuer les opérations suivantes :

* Inclure un **Native client** dans l’application hello.
* Hello de copie **ID d’Application** qui est attribué tooyour application. Vous aurez besoin de ce GUID ultérieurement.
* Configurez un **URI de redirection** avec un schéma personnalisé (par exemple, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect). Vous aurez besoin de cet URI ultérieurement.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Création de vos stratégies
Dans Azure AD B2C, chaque expérience utilisateur est définie par une [stratégie](active-directory-b2c-reference-policies.md). Cette application contient une seule expérience liée à l’identité : une connexion et une inscription combinées. Créez cette stratégie, comme décrit dans l’[article de référence sur les stratégies](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Lorsque vous créez la stratégie de hello, veillez à :

* Sous **des attributs d’abonnement**, sélectionnez les attributs hello **nom d’affichage**.  Vous pouvez sélectionner d’autres attributs également.
* Sous **revendications Application**, sélectionnez les revendications hello **nom d’affichage** et **ID d’objet de l’utilisateur**. Vous pouvez aussi sélectionner d’autres revendications.
* Hello de copie **nom** de chaque stratégie après l’avoir créée. Votre nom de la stratégie est préfixé avec `b2c_1_` lorsque vous enregistrez la stratégie de hello.  Vous devez nom de la stratégie hello plus tard.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Après avoir créé vos stratégies, vous êtes prêt toobuild votre application.

## <a name="download-hello-sample-code"></a>Télécharger l’exemple de code hello
Nous avons fourni un exemple fonctionnel qui utilise AppAuth avec Azure AD B2C [sur GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c). Vous pouvez télécharger le code de hello et exécutez-le. toouse votre propre B2C de AD Azure locataire, suivez les instructions de hello Bonjour [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).

Cet exemple a été créé en suivant les instructions du fichier Lisezmoi hello en hello [iOS AppAuth projet sur GitHub](https://github.com/openid/AppAuth-iOS). Pour plus d’informations sur le fonctionnement des exemple hello et bibliothèque de hello, référence hello README AppAuth sur GitHub.

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>Modification de votre toouse application Azure AD B2C avec AppAuth

> [!NOTE]
> AppAuth prend en charge iOS 7 et versions ultérieures.  Toutefois, toosupport des connexions social de Google, SFSafariViewController qui nécessite d’iOS 9 ou version ultérieure est nécessaire.
>

### <a name="configuration"></a>Configuration

Vous pouvez configurer la communication avec Azure AD B2C en spécifiant le point de terminaison d’autorisation hello et URI de point de terminaison token.  toogenerate ces URI, vous devez hello informations suivantes :
* ID client (par exemple, contoso.onmicrosoft.com)
* Nom de la stratégie (par exemple, B2C\_1\_SignUpIn)

point de terminaison token URI peut être généré en remplaçant Hello hello client\_ID et hello stratégie\_nom Bonjour suivant l’URL :

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

point de terminaison d’URI peut être généré en remplaçant Hello hello client\_ID et hello stratégie\_nom Bonjour suivant l’URL :

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

Exécutez hello suivant toocreate de code de votre objet AuthorizationServiceConfiguration :

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a>Autorisation

Après la configuration ou la récupération d’une configuration de service d’autorisation, une demande d’autorisation peut être créée. toocreate hello demande, vous devez hello informations suivantes :  
* ID client (par exemple, 00000000-0000-0000-0000-000000000000)
* URI de redirection avec un schéma personnalisé (par exemple, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)

Les deux éléments doivent avoir été enregistrés là où vous avez [inscrit votre application](#create-an-application).

```objc
OIDAuthorizationRequest *request = 
    [[OIDAuthorizationRequest alloc] initWithConfiguration:configuration
                                                  clientId:kClientId
                                                    scopes:@[OIDScopeOpenID, OIDScopeProfile]
                                               redirectURL:[NSURL URLWithString:kRedirectUri]
                                              responseType:OIDResponseTypeCode
                                      additionalParameters:nil];

AppDelegate *appDelegate = (AppDelegate *)[UIApplication sharedApplication].delegate;
appDelegate.currentAuthorizationFlow = 
    [OIDAuthState authStateByPresentingAuthorizationRequest:request
                                   presentingViewController:self
                                                   callback:^(OIDAuthState *_Nullable authState, NSError *_Nullable error) {
        if (authState) {
            NSLog(@"Got authorization tokens. Access token: %@", authState.lastTokenResponse.accessToken);
            [self setAuthState:authState];
        } else {
            NSLog(@"Authorization error: %@", [error localizedDescription]);
            [self setAuthState:nil];
        }
    }];
```

tooset de votre toohello de redirection des hello de toohandle application URI avec un jeu personnalisé de hello, vous avez besoin tooupdate hello liste de « Modèles d’URL » dans votre fichier Info.pList :
* Ouvrez Info.pList.
* Placez le curseur sur une ligne, comme « Code de Type du système d’exploitation offre groupée » et cliquez sur hello \+ symbole.
* Renommez hello nouvelle ligne 'URL types'.
* Cliquez sur hello flèche toohello gauche d’arborescence de « Types d’URL » tooopen hello.
* Cliquez sur hello flèche toohello gauche d’arborescence de hello tooopen 'Élément 0'.
* Renommez le premier élément sous l’élément 0 too'URL schémas.
* Cliquez sur hello flèche toohello gauche d’arborescence de 'schémas d’URL ' tooopen hello.
* Dans la colonne hello 'Value' ne dispose plus un champ vide toohello de 'Élément 0 », sous « Schémas d’URL ».  Définissez un jeu unique de l’application hello valeur tooyour.  valeur de Hello doit correspondre au schéma de hello utilisé dans redirectURL lors de la création d’objet de OIDAuthorizationRequest hello.  Dans notre exemple, nous avons utilisé schéma hello 'com.onmicrosoft.fabrikamb2c.exampleapp'.

Consultez toohello [AppAuth guide](https://openid.github.io/AppAuth-iOS/) sur la façon dont toocomplete hello reste du processus de hello. Si vous avez besoin de tooquickly commencer avec une application, l’extraction [notre exemple](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c). Suivez les étapes de hello Bonjour [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter votre propre configuration Azure AD B2C.

Nous sommes toujours ouvrir toofeedback ainsi que des suggestions ! Si vous rencontrez des difficultés avec cette rubrique, ou que vous avez des recommandations pour améliorer ce contenu, nous aimerions connaître votre opinion bas hello de page de hello. Pour les demandes de fonctionnalités, ajoutez-les trop[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).
