---
title: "application Android d’aaaAzure Active Directory v2.0 | Documents Microsoft"
description: "Comment une application Android qui se connecte à la fois personnelles compte Microsoft et comptes d’établissement scolaire et passe les appels aux utilisateurs de toobuild hello API Graph en utilisant des bibliothèques tierces."
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 16294c07-f27d-45c9-833f-7dbb12083794
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1dd40bd3bcea28c629abce09abaed66b38774162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-android-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a>Ajouter une application Android de tooan connectez-vous à l’aide d’une bibliothèque tierce avec l’API Graph à l’aide du point de terminaison hello v2.0
plateforme d’identité Microsoft Hello utilise des normes ouvertes telles que OAuth2 et OpenID Connect. Les développeurs peuvent utiliser n’importe quelle bibliothèque qu’ils souhaitent toointegrate avec nos services. les développeurs de toohelp utilisent notre plateforme avec d’autres bibliothèques, nous avons comment écrit quelques procédures pas à pas, comme cette une toodemonstrate plateforme d’identité tooconnect toohello Microsoft tooconfigure des bibliothèques tierces. La plupart des bibliothèques qui implémentent [les spécifications hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) peut se connecter de plateforme d’identité Microsoft toohello.

Avec l’application hello qui crée de cette procédure pas à pas, les utilisateurs peuvent se connecter tootheir organisation et puis rechercher eux-mêmes dans leur organisation à l’aide de l’API Graph de hello.

Si vous êtes de nouveau tooOAuth2 ou OpenID Connect, une grande partie de cet exemple de configuration peut ne pas effectuer tooyou de sens. Nous vous recommandons de lire [Protocoles 2.0 - Flux du Code d’autorisation OAuth 2.0](active-directory-v2-protocols-oauth-code.md) pour plus d’informations.

> [!NOTE]
> Certaines fonctionnalités de notre plateforme qui n’ont pas une expression dans hello OAuth2 ou OpenID Connect des normes, telles que l’accès conditionnel et de gestion des stratégies Intune, requièrent vous toouse open source bibliothèques d’identité Microsoft Azure.
> 
> 

point de terminaison Hello v2.0 ne prend pas en charge toutes les fonctionnalités et scénarios d’Azure Active Directory.

> [!NOTE]
> toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).
> 
> 

## <a name="download-hello-code-from-github"></a>Télécharger le code de hello à partir de GitHub
code Hello pour ce didacticiel est maintenue [sur GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).  toofollow le long, vous pouvez [structure de l’application hello en tant qu’un fichier ZIP de téléchargement](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) ou un clone hello squelette :

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

Vous pouvez également simplement télécharger l’exemple hello et démarrer immédiatement :

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a>Inscription d’une application
Créer une application à hello [portail de l’enregistrement d’Application](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez hello étapes détaillées à [comment tooregister une application avec un point de terminaison hello v2.0](active-directory-v2-app-registration.md).  Veillez à respecter les points suivants :

* Hello de copie **Id d’Application** qui est attribué tooyour application, car vous en aurez besoin plus rapidement.
* Ajouter hello **Mobile** plate-forme pour votre application.

> Remarque : portail de l’enregistrement d’Application hello fournit un **URI de redirection** valeur. Toutefois, dans cet exemple, vous devez utiliser valeur par défaut hello `https://login.microsoftonline.com/common/oauth2/nativeclient`.
> 
> 

## <a name="download-hello-nxoauth2-third-party-library-and-create-a-workspace"></a>Télécharger des bibliothèques tierces de NXOAuth2 hello et créer un espace de travail
Pour cette procédure pas à pas, vous allez utiliser hello OIDCAndroidLib à partir de GitHub, qui est une bibliothèque OAuth2 selon hello code d’OpenID Connect de Google. Il implémente le profil d’application native hello et prend en charge le point de terminaison hello d’autorisation d’utilisateur de hello. Il s’agit de tous les éléments hello que vous devez toointegrate avec la plateforme d’identité Microsoft hello.

Cloner l’ordinateur de tooyour hello OIDCAndroidLib référentiel.

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a>Configurer votre environnement Android Studio
1. Créer un projet Android Studio et acceptez les valeurs par défaut hello dans l’Assistant de hello.
   
    ![Créer un nouveau projet dans Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Cibler des appareils Android](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Ajouter une activité toomobile](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. tooset des modules de votre projet, déplacez hello cloné dépôt toohello l’emplacement du projet. Vous pouvez également créer des projets de hello et puis clonez-le directement toohello l’emplacement du projet.
   
    ![Modules de projet](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. Ouvrez les paramètres de modules de projet hello à l’aide du menu contextuel de hello ou à l’aide du raccourci Ctrl + Alt + Maj + S de hello.
   
    ![Paramètres de modules de projet](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. Supprimer le module d’application hello par défaut parce que vous souhaitez uniquement les paramètres de conteneur de projet hello.
   
    ![module d’application Hello par défaut](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. Importer des modules à partir de projet actuel du toohello hello référentiel cloné.
   
    ![Importer un projet gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![créer une nouvelle page de module](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)
6. Répétez ces étapes pour hello `oidlib-sample` module.
7. Vérification des dépendances d’oidclib hello sur hello `oidlib-sample` module.
   
    ![oidclib des dépendances sur le module d’oidlib-exemple hello](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. Cliquez sur **OK** et attendez l’activité de synchronisation Gradle.
   
    Votre fichier settings.gradle doit ressembler à ceci :
   
    ![Capture d’écran de settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. Build hello exemple application toomake que cet exemple hello fonctionne correctement.
   
    Vous ne pourra plus être en mesure de toouse cela avec Azure Active Directory encore. Nous devrons tooconfigure certains points de terminaison tout d’abord. Il s’agit de tooensure vous n’avez pas un problème dans Android Studio avant de commencer la personnalisation de hello, exemple d’application.
10. Générez et exécutez `oidlib-sample` comme cible de hello dans Android Studio.
    
    ![Progression de la création d’oidlib-sample](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. Supprimer hello `app ` active a été laissée lorsque vous retiré module de hello hello projet car Android Studio ne le supprime pas de sécurité.
    
    ![Structure de fichier qui inclut le répertoire de l’application hello](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. Ouvrez hello **modifier les Configurations** menu tooremove hello exécuter configuration qui a été laissée également lorsque vous avez supprimé le module de hello à partir du projet de hello.
    
    ![Menu Modifier les configurations](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![Exécuter la configuration de l’application](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)

## <a name="configure-hello-endpoints-of-hello-sample"></a>Configurer des points de terminaison hello de l’exemple hello
Maintenant que vous avez hello `oidlib-sample` en cours d’exécution avec succès, permet de modifier certains points de terminaison tooget ce travail avec Azure Active Directory.

### <a name="configure-your-client-by-editing-hello-oidcclientconfxml-file"></a>Configurer votre client en modifiant le fichier de oidc_clientconf.xml hello
1. Étant donné que vous utilisez OAuth2 flux tooget uniquement un jeton et appelez hello API Graph, définissez hello client toodo OAuth2 uniquement. Nous verrons OIDC dans un autre exemple.
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. Configurez votre ID client que vous avez reçu à partir du portail de l’enregistrement hello.
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. Configurez votre URI de redirection par hello un ci-dessous.
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. Configurez vos étendues que vous avez besoin dans l’ordre tooaccess hello API Graph.
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

Hello `User.Read` valeur `oidc_scopes` permet de vous tooread hello profil de base hello utilisateur connecté.
Plus d’informations sur toutes les étendues disponibles hello à [étendues d’autorisation Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).

Si vous souhaitez des explications sur `openid` ou `offline_access` en tant qu’étendues dans OpenID Connect, consultez [Protocoles 2.0 - Flux du Code d’autorisation OAuth 2.0](active-directory-v2-protocols-oauth-code.md).

### <a name="configure-your-client-endpoints-by-editing-hello-oidcendpointsxml-file"></a>Configurer vos points de terminaison client en modifiant le fichier de oidc_endpoints.xml hello
* Ouvrez hello `oidc_endpoints.xml` et apportez hello modifications suivantes :
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

Ces points de terminaison ne doivent jamais changer si vous utilisez OAuth2 comme protocole.

> [!NOTE]
> Hello des points de terminaison pour `userInfoEndpoint` et `revocationEndpoint` ne sont actuellement pas pris en charge par Azure Active Directory. Si vous laissez ces hello valeur par défaut exemple.com, rappel qu’ils ne sont pas disponibles dans l’exemple hello  :-)
> 
> 

## <a name="configure-a-graph-api-call"></a>Configurer un appel d’API Graph
* Ouvrez hello `HomeActivity.java` et apportez hello modifications suivantes :
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

Ici, un simple appel à l’API Graph renvoie nos informations.

Ce sont toutes les modifications de hello que vous avez besoin de toodo. Exécutez hello `oidlib-sample` application, puis cliquez sur **connectez-vous**.

Une fois que vous avez été authentifié avec succès, sélectionnez hello **demander la ressource protégée** bouton tootest votre toohello appel API Graph.

## <a name="get-security-updates-for-our-product"></a>Obtenir des mises à jour de sécurité pour notre produit
Nous vous encourageons tooget des notifications sur les incidents de sécurité en visitant hello [TechCenter sur la sécurité](https://technet.microsoft.com/security/dd252948) et l’abonnement d’alerte tooSecurity.

