---
title: "Azure Active Directory B2C : Obtenir un jeton à l’aide d’une application Android | Microsoft Docs"
description: "Cet article vous indiquent comment toocreate une application Android qui utilise AppAuth avec des identités d’utilisateur Azure Active Directory B2C toomanage et authentifie les utilisateurs."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: d00947c3-dcaa-4cb3-8c2e-d94e0746d8b2
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 03/06/2017
ms.author: parakhj
ms.openlocfilehash: 0236398673115a34951f035cb1e73e89417abf86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a>Azure Active Directory B2C : Se connecter à l’aide d’une application Android

plateforme d’identité Microsoft Hello utilise des normes ouvertes telles que OAuth2 et OpenID Connect. Cela permet aux développeurs tooleverage n’importe quelle bibliothèque qu’ils souhaitent toointegrate avec nos services. les développeurs tooaid à l’aide de notre plateforme avec d’autres bibliothèques, nous avons écrit quelques procédures pas à pas, comme ce un toodemonstrate comment tooconfigure 3e partie bibliothèques tooconnect toohello plateforme d’identité Microsoft. La plupart des bibliothèques qui implémentent [les spécifications hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) sera platform de Microsoft Identity toohello tooconnect en mesure de.

> [!WARNING]
> Microsoft ne fournit pas de correctifs pour les bibliothèques tierces et ne les a pas vérifiées. Cet exemple utilise une bibliothèque tiers 3e appelée AppAuth qui a été testé pour la compatibilité dans les scénarios de base avec hello Azure Active Directory B2C. Problèmes et des demandes de fonctionnalités doivent être projet open source de la bibliothèque toohello dirigée. Pour plus d’informations, consultez [cet article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).  
>
>

Si vous êtes tooOAuth2 nouveau ou OpenID Connect une grande partie de cet exemple de configuration peut ne pas effectuer de tooyou sens. Nous vous recommandons de consulter un résumé [vue d’ensemble du protocole hello que nous avons présentés ici](active-directory-b2c-reference-protocols.md).

## <a name="get-an-azure-ad-b2c-directory"></a>Obtention d'un répertoire Azure AD B2C

Avant de pouvoir utiliser Azure AD B2C, vous devez créer un répertoire ou un client. Un répertoire est un conteneur destiné à recevoir tous vos utilisateurs, applications, groupes, etc. Si vous n’en possédez pas déjà un, [créez un répertoire B2C](active-directory-b2c-get-started.md) avant de continuer.

## <a name="create-an-application"></a>Création d'une application

Ensuite, vous devez toocreate une application dans votre répertoire B2C. Cela fournit des informations de Azure AD lui toocommunicate en toute sécurité avec votre application. toocreate une application mobile, procédez comme [ces instructions](active-directory-b2c-app-registration.md). Veillez à effectuer les opérations suivantes :

* Inclure un **Native Client** dans l’application hello.
* Hello de copie **ID d’Application** qui est attribué tooyour application. Vous en aurez besoin ultérieurement.
* Configurez un **URI de redirection** de client natif (par exemple, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect). Vous en aurez besoin ultérieurement.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>Création de vos stratégies

Dans Azure AD B2C, chaque expérience utilisateur est définie par une [stratégie](active-directory-b2c-reference-policies.md). Cette application contient une seule expérience liée à l’identité : une connexion et une inscription combinées. Vous devez toocreate cette stratégie, comme décrit dans la [article de référence de stratégie](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Lorsque vous créez la stratégie de hello, veillez à :

* Choisissez hello **nom d’affichage** comme un attribut d’inscription de votre stratégie.
* Choisissez hello **nom d’affichage** et **ID d’objet** revendications de l’application dans chaque stratégie. Vous pouvez aussi choisir d'autres revendications.
* Hello de copie **nom** de chaque stratégie après l’avoir créée. Il doit avoir le préfixe de hello `b2c_1_`.  Vous aurez besoin nom de la stratégie hello plus tard.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Après avoir créé vos stratégies, vous êtes prêt toobuild votre application.

## <a name="download-hello-sample-code"></a>Télécharger l’exemple de code hello

Nous avons fourni un exemple fonctionnel qui utilise AppAuth avec Azure AD B2C [sur GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c). Vous pouvez télécharger le code de hello et exécutez-le. Vous pouvez rapidement commencer à utiliser votre propre application à l’aide de votre propre configuration Azure AD B2C en suivant les instructions de hello Bonjour [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).

exemple Hello est une modification de l’exemple hello fournie par [AppAuth](https://openid.github.io/AppAuth-Android/). Visitez leur toolearn page plus d’informations sur les AppAuth et de ses fonctionnalités.

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a>Modification de votre toouse application Azure AD B2C avec AppAuth

> [!NOTE]
> AppAuth prend en charge Android API 16 (Jellybean) et versions ultérieures. Nous recommandons d’utiliser API 23 et versions ultérieures.
>

### <a name="configuration"></a>Configuration

Vous pouvez configurer la communication avec Azure AD B2C par soit découverte hello en spécifiant des URI ou en spécifiant le point de terminaison d’autorisation hello et URI de point de terminaison token. Dans les deux cas, vous devez hello informations suivantes :

* ID client (par ex., contoso.onmicrosoft.com)
* Nom de la stratégie (par ex., B2C\_1\_SignUpIn)

Si vous choisissez tooautomatically découverte hello d’autorisation et le jeton de point de terminaison URI, vous aurez besoin des informations de toofetch de la découverte de hello URI. détection de Hello URI peut être généré en remplaçant hello client\_ID et hello stratégie\_nom Bonjour suivant l’URL :

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

Vous pouvez acquérir l’autorisation de hello et URI de point de terminaison token et créer un objet AuthorizationServiceConfiguration en exécutant hello suivante :

```java
final Uri issuerUri = Uri.parse(mDiscoveryURI);
AuthorizationServiceConfiguration config;

AuthorizationServiceConfiguration.fetchFromIssuer(
    issuerUri,
    new RetrieveConfigurationCallback() {
      @Override public void onFetchConfigurationCompleted(
          @Nullable AuthorizationServiceConfiguration serviceConfiguration,
          @Nullable AuthorizationException ex) {
        if (ex != null) {
            Log.w(TAG, "Failed tooretrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed tooauthorization...
        }
      }
  });
```

Au lieu d’utiliser l’autorisation de découverte tooobtain hello et URI de point de terminaison token, vous pouvez également spécifier les explicitement en remplaçant hello client\_ID et hello stratégie\_nom dans l’URL de hello ci-dessous :

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

Exécutez hello suivant toocreate de code de votre objet AuthorizationServiceConfiguration :

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a>Autorisation

Après la configuration ou la récupération d’une configuration de service d’autorisation, une demande d’autorisation peut être créée. toocreate hello demande, vous devez hello informations suivantes :

* ID client (par ex. 00000000-0000-0000-0000-000000000000)
* URI de redirection avec un schéma personnalisé (par ex., com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)

Les deux éléments doivent avoir été enregistrés là où vous avez [inscrit votre application](#create-an-application).

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

Reportez-vous toohello [AppAuth guide](https://openid.github.io/AppAuth-Android/) sur la façon dont toocomplete hello reste du processus de hello. Si vous avez besoin de tooquickly commencer avec une application, l’extraction [notre exemple](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c). Suivez les étapes de hello Bonjour [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter votre propre configuration Azure AD B2C.

Nous sommes toujours ouvrir toofeedback ainsi que des suggestions ! Si vous rencontrez des difficultés avec cette rubrique, ou que vous avez des recommandations pour améliorer ce contenu, nous aimerions connaître votre opinion bas hello de page de hello. Pour les demandes de fonctionnalités, ajoutez-les trop[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).

