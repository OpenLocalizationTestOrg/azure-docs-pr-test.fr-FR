---
title: "aaaHow tooenable SSO inter-applications sur Android à l’aide de la bibliothèque ADAL | Documents Microsoft"
description: "Comment toouse les fonctionnalités de hello de hello tooenable SDK ADAL Single Sign On dans vos applications. "
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 40710225-05ab-40a3-9aec-8b4e96b6b5e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 04/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 3867e15030e5516464e4dbd92ba35894430daf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-android-using-adal"></a>Comment tooenable l’authentification unique entre l’application sur Android à l’aide de la bibliothèque ADAL
Fournissant Single Sign-On (SSO) afin que les utilisateurs uniquement besoin de tooenter leurs informations d’identification qu’une seule fois ont ces informations d’identification du travail automatiquement entre les applications est désormais attendu par les clients. difficulté Hello en entrant leur nom d’utilisateur et un mot de passe sur un petit écran, souvent fois combinés avec un facteur supplémentaire (2FA) comme un appel téléphonique ou un code envoyé par SMS, entraîne le mécontentement rapide si un utilisateur a toodo cela plusieurs fois pour votre produit.

En outre, si vous appliquez une plateforme d’identité qui peuvent utiliser des autres applications telles que Microsoft Accounts ou un compte professionnel à partir d’Office 365, les clients attendent que ces toouse disponible de toobe informations d’identification pour toutes les applications de leurs quel que soit le fournisseur de hello.

Hello plateforme Microsoft Identity, ainsi que nos kits de développement Microsoft Identity, fait tout ce travail pour vous et donne vous hello toodelight de capacité de vos clients avec l’authentification unique au sein de votre propre suite d’applications ou, en tant que notre service broker et un authentificateur applications, sur l’ensemble de l’unité hello.

Cette procédure pas à pas explique comment tooconfigure notre kit de développement logiciel au sein de votre application de tooprovide cet avantage tooyour les clients.

Cette procédure pas à pas s’applique aux éléments suivants :

* Azure Active Directory
* Azure Active Directory B2C
* Azure Active Directory B2B
* Accès conditionnel Azure Active Directory

document Hello précédent suppose que vous savez comment trop[la configuration des applications dans le portail hérité de hello pour Azure Active Directory](active-directory-how-to-integrate.md) et d’intégrer votre application hello [SDK Android de Microsoft Identity](https://github.com/AzureAD/azure-activedirectory-library-for-android) .

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a>Concepts de l’authentification unique Bonjour plateforme d’identité Microsoft
### <a name="microsoft-identity-brokers"></a>Répartiteurs Microsoft Identity
Microsoft fournit des applications pour toutes les plateformes mobiles acceptant pour le pontage hello d’informations d’identification entre les applications provenant de différents fournisseurs et permet à des fonctionnalités améliorées spéciales qui requièrent un seul emplacement sécurisé à partir de laquelle les informations d’identification de toovalidate. Nous appelons ces applications **répartiteurs**. Sur iOS et Android, ceux-ci sont fournis par le biais des applications téléchargeables que clients installer indépendamment ou pouvant être envoyées toohello appareil par une société qui gère tout ou partie des périphériques de hello pour leurs employés. Ces services Broker prend en charge la gestion de la sécurité pour certaines applications ou certains hello ensemble de l’unité selon ce que les administrateurs informatiques souhaitent. Dans Windows, cette fonctionnalité est fournie par un sélecteur de compte de système d’exploitation de toohello, appelé techniquement hello Service Broker d’authentification Web intégré.

Pour plus d’informations sur la façon de nous utilisons ces courtiers et comment vos clients peuvent voir les leur flux de connexion pour la plateforme de Microsoft Identity hello lire sur.

### <a name="patterns-for-logging-in-on-mobile-devices"></a>Modèles de connexion sur les appareils mobiles
Deux modèles de base pour la plateforme de Microsoft Identity hello, procédez toocredentials d’accès sur les appareils :

* Connexions assistées sans répartiteur
* Connexions assistées avec répartiteur

#### <a name="non-broker-assisted-logins"></a>Connexions assistées sans répartiteur
Non-Service Broker pour les connexions assistées sont les expériences de connexion qui se produisent en ligne avec l’application hello et utilisent le stockage local de hello sur l’appareil hello pour cette application. Ce stockage peut être partagé entre les applications, mais les informations d’identification de hello sont étroitement liés toohello application ou la suite d’applications à l’aide de ces informations d’identification. Vous avez probablement rencontré cela dans de nombreuses applications mobiles lorsque vous entrez un nom d’utilisateur et un mot de passe au sein de l’application hello lui-même.

Ces connexions ont hello avantages suivants :

* Expérience utilisateur existe entièrement dans l’application hello.
* Informations d’identification peuvent être partagées entre les applications qui sont signées par hello même certificat, en fournissant une suite de tooyour une expérience d’authentification unique d’applications.
* Contrôle autour d’expérience hello de connexion est fourni toohello application avant et après la connexion.

Ces connexions ont hello suivant des inconvénients :

* L’utilisateur ne peut pas profiter de l’authentification unique sur l’ensemble des applications utilisant Microsoft Identity, uniquement sur celles que votre application a configuré.
* Votre application ne peut pas être utilisée avec des fonctionnalités d’entreprise plus avancées telles que l’accès conditionnel ou utilisez hello InTune suite de produits.
* Votre application ne peut pas prendre en charge l’authentification par certificat des utilisateurs professionnels.

Voici une représentation du fonctionnement des kits de développement logiciel hello Microsoft identité avec le stockage de vos tooenable applications SSO hello partagé :

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| Azure SDK  | | Azure SDK  |  | Azure SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a>Connexions assistées avec répartiteur
Assisté par service Broker pour les connexions sont des expériences de connexion qui se produisent dans l’application de service broker hello et d’utilisent le stockage de hello et la sécurité des informations d’identification de hello broker tooshare sur toutes les applications sur l’appareil de hello qui s’appliquent de plateforme de Microsoft Identity hello. Cela signifie que vos applications hello broker toosign utilisateurs. Sur iOS et Android ces courtiers sont fournies via des applications téléchargeables que clients installer indépendamment ou pouvant être envoyées toohello appareil par une société qui gère le périphérique hello pour leurs utilisateurs. Un exemple de ce type d’application est l’application de Microsoft Authenticator hello sur iOS. Dans Windows, cette fonctionnalité est fournie par un sélecteur de compte de système d’exploitation de toohello, appelé techniquement hello Service Broker d’authentification Web intégré.
expérience de Hello varie selon la plate-forme et peut parfois être perturbateur toousers si elle n’est pas géré correctement. Vous connaissez probablement plus ce modèle si vous disposez d’application Facebook hello et utilisez la connexion à Facebook à partir d’une autre application. Hello utilise de plateforme d’identité Microsoft hello même modèle.

Pour iOS cela entraîne l’animation tooa « transition » où votre application est envoyée arrière-plan toohello lors des applications de Microsoft Authenticator hello est fourni au premier plan toohello pour hello utilisateur tooselect quel compte il veut toosign avec.  

Pour le compte de hello Android et Windows sélecteur s’affiche au-dessus de votre application qui est moins toohello utilisateur.

#### <a name="how-hello-broker-gets-invoked"></a>Comment le service broker de hello appelée
Si un service broker compatible est installé sur le périphérique hello, comme hello application Microsoft Authenticator, hello kits de développement logiciel de Microsoft Identity sera automatiquement hello travail d’un appel de broker hello pour vous quand un utilisateur indique qu’ils souhaitent toolog à l’aide de n’importe quel compte de plateforme de Microsoft Identity Hello. Il peut s’agir d’un compte personnel Microsoft, d’un compte professionnel ou scolaire, ou d’un compte que vous fournissez et hébergez dans Microsoft Azure à l’aide de nos produits B2C et B2B. 
 
 #### <a name="how-we-ensure-hello-application-is-valid"></a>Comment nous assurer l’application hello est valide
 
 identité de hello tooensure Hello besoin d’un service Broker pour les applications appel hello est sécurité essentielle toohello que nous fournir dans les connexions de broker assistée. IOS, ni Android applique des identificateurs uniques qui sont valides uniquement pour une application donnée, afin que des applications malveillantes peuvent « usurper l’identité « identificateur d’une application légitime et recevoir des jetons hello destinées à être application légitime hello. tooensure que nous communiquons toujours avec application droite hello lors de l’exécution, nous vous demandons hello développeur tooprovide un redirectURI personnalisé lors de l’inscription de leur application auprès de Microsoft. **Nous expliquons ci-dessous comment les développeurs doivent créer cet URI de redirection.** Cette redirectURI personnalisé contient l’empreinte numérique du certificat hello de l’application hello et assurer toobe toohello unique application hello Google Play Store. Lorsqu’une application appelle le service broker hello, service broker de hello demande tooprovide du système d’exploitation Android hello avec hello empreinte numérique du certificat que broker appelée hello. service broker de Hello fournit cette tooMicrosoft de l’empreinte numérique du certificat dans le système d’identité tooour hello appel. Si certificat hello empreinte numérique de l’application hello ne correspond pas à l’empreinte numérique du certificat hello fourni toous par le développeur de hello lors de l’inscription, nous refuse l’accès toohello jetons pour l’application hello ressource hello demande. Cette vérification ne garantit que les application hello enregistrées par le développeur de hello reçoit les jetons.

**développeur de Hello a choix entre hello si hello Kit de développement logiciel de Microsoft Identity appelle le service broker de hello ou agira hello non broker assistée.** Toutefois si le développeur de hello ne choisit pas de flux d’assisté par service broker de hello toouse ils plus hello à l’aide des informations d’identification de l’authentification unique que l’utilisateur hello a peut-être déjà ajouté sur le périphérique de hello et empêche leur application d’être utilisés avec les fonctionnalités d’entreprise Microsoft fournit à ses clients, tels que l’accès conditionnel, les fonctionnalités de gestion Intune et l’authentification par certificat.

Ces connexions ont hello avantages suivants :

* Utilisateur rencontre l’authentification unique sur toutes leurs applications, quel que soit le fournisseur de hello.
* Votre application peut utiliser les fonctionnalités d’entreprise plus avancées telles que l’accès conditionnel ou utiliser suite, InTune hello de produits.
* Votre application peut prendre en charge l’authentification par certificat des utilisateurs professionnels.
* Connectez-vous beaucoup plus sûre expérience comme identité hello de l’application hello et l’utilisateur de hello sont vérifiées par application de service broker hello avec chiffrement et les algorithmes de sécurité supplémentaires.

Ces connexions ont hello suivant des inconvénients :

* Dans iOS utilisateur de hello est passée en dehors de l’expérience de votre application pendant que les informations d’identification sont choisies.
* Perte de connexion de hello hello capacité toomanage expérience pour vos clients dans votre application.

Voici une représentation sous forme de comment utiliser kits de développement logiciel de Microsoft Identity hello hello broker applications tooenable l’authentification unique :

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
|  ADAL SDK  | |  ADAL SDK  |   |  ADAL SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+

```

Grâce à ces informations en arrière-plan, vous devez être en mesure de toobetter comprendre et à implémenter l’authentification unique au sein de votre application à l’aide de la plateforme de Microsoft Identity hello et kits de développement logiciel.

## <a name="enabling-cross-app-sso-using-adal"></a>Activation de l’authentification unique entre applications à l’aide de la bibliothèque ADAL
Nous utilisons ici hello ADAL SDK Android pour :

* Activer l’authentification unique assistée sans répartiteur pour votre suite d’applications
* Activer la prise en charge de l’authentification unique assistée avec répartiteur

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a>Activation de l’authentification unique assistée sans répartiteur
Pour l’authentification unique assistée de non broker entre les applications hello kits de développement logiciel de Microsoft Identity gèrent une grande partie de la complexité de hello de l’authentification unique pour vous. Cela inclut la recherche d’utilisateur hello dans le cache de hello et en conservant une liste des utilisateurs connectés pour vous tooquery.

tooenable l’authentification unique entre les applications que vous possédez que vous devez hello toodo suivant :

1. Vérifiez tous les votre hello d’utilisateur d’applications même ID de Client ou l’ID d’Application.
2. Assurez-vous que toutes vos applications ont hello que shareduserid même valeur.
3. Vérifiez que tous vos hello de partage d’applications même certificat de signature à partir de hello Google Play stocker afin que vous pouvez partager du stockage.

#### <a name="step-1-using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a>Étape 1 : À l’aide de hello même ID de Client / ID de l’Application pour tous les hello dans votre ensemble d’applications
Par ordre de hello Microsoft Identity plateforme tooknow qu’il est autorisé tooshare jetons dans vos applications, chacune de vos applications devez hello tooshare même ID de Client ou l’ID d’Application. Il s’agit d’identificateur hello qui a été fourni tooyou lorsque vous avez inscrit votre première application dans le portail de hello.

Vous vous demandez peut-être comment vous allez identifier les différentes applications toohello service Microsoft Identity s’il utilise hello même ID d’Application. les réponses Hello sont avec hello **URI de redirection**. Chaque application peut avoir plusieurs URI de redirection inscrit dans le portail de l’intégration de hello. Chacune des applications de votre suite présente un URI de redirection propre. Voici une représentation possible :

URI de redirection App1 : `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`

URI de redirection App2 : `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`

URI de redirection App3 : `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`

....

Elles sont imbriquées sous hello même ID de client / ID d’application et recherchée hello en fonction de redirection URI vous renvoyer toous dans votre configuration du Kit de développement logiciel.

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


*Notez que le format de ces URI de redirection de hello sont expliquées ci-dessous. Vous pouvez utiliser n’importe quel URI de redirection, sauf si vous le souhaitez broker de hello toosupport, auquel cas ils doivent ressembler à hello ci-dessus*

#### <a name="step-2-configuring-shared-storage-in-android"></a>Étape 2 : Configuration du stockage partagé dans Android
Hello du paramètre `SharedUserID` est abordée dans ce document hello mais peuvent être appris en lisant hello documentation Google Android hello [manifeste](http://developer.android.com/guide/topics/manifest/manifest-element.html). L’essentiel est que vous déterminiez le nom que vous souhaitez attribuer à sharedUserID et que vous l’utilisiez dans l’ensemble de vos applications.

Une fois que vous avez hello `SharedUserID` dans toutes vos applications, vous êtes prêt toouse SSO.

> [!WARNING]
> Lorsque vous partagez le stockage dans vos applications n’importe quelle application peut supprimer des utilisateurs ou pire supprimer tous les jetons hello dans votre application. Cela est particulièrement désastreux si vous avez des applications qui reposent sur le travail d’arrière-plan toodo hello jetons. Partage du stockage signifie que vous devez être très prudent dans les opérations de suppression de tous les via hello kits de développement logiciel de Microsoft Identity.
> 
> 

Et voilà ! Hello Kit de développement logiciel de Microsoft Identity partagent maintenant informations d’identification dans toutes vos applications. liste des utilisateurs Hello est également partagé entre les instances de l’application.

### <a name="turning-on-sso-for-broker-assisted-sso"></a>Activation de l’authentification unique assistée avec répartiteur
Hello possibilité pour un toouse de l’application est de n’importe quel service broker qui est installé sur l’appareil de hello **désactivée par défaut**. Dans commande toouse votre application avec le service broker de hello, vous devez effectuer une configuration supplémentaire et ajouter une application tooyour de code.

Hello étapes toofollow sont les suivantes :

1. Activer le mode de service broker dans toohello d’appel de code de votre application MS SDK
2. Établir un nouveau URI de redirection et fournir cette application de hello tooboth et votre inscription d’une application
3. Définition des autorisations correctes de hello dans le manifeste de Android hello

#### <a name="step-1-enable-broker-mode-in-your-application"></a>Étape 1 : Activer le mode répartiteur dans votre application
possibilité de Hello pour votre courtier de hello toouse application est activée lorsque vous créez les paramètres « hello » ou la configuration initiale de votre instance de l’authentification. Pour ce faire, définissez le type ApplicationSettings dans votre code :

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a>Étape 2 : Établissez un nouvel URI de redirection avec votre schéma d’URL
Tooensure de commande que nous retournent toujours les informations d’identification de hello jetons toohello une bonne application, nous devons toomake que nous rappeler tooyour l’application d’une manière qui hello du système d’exploitation Android peut vérifier. système d’exploitation Android Hello utilise hello de hachage du certificat de hello Bonjour Google Play store. Il ne peut pas être falsifié par une application non fiable. Par conséquent, nous offrent cette possibilité avec hello URI de notre tooensure d’application de service broker que les jetons de hello sont retournés toohello une bonne application. Nous avons besoin de vous tooestablish cette redirection unique URI à la fois dans votre application et la définir en tant qu’URI de redirection dans notre portail des développeurs.

Votre URI de redirection doit être de forme correcte hello :

`msauth://packagename/Base64UrlencodedSignature`

ex. : *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*

Cet URI de redirection doit toobe spécifié dans votre inscription d’une application à l’aide de hello [portail Azure](https://portal.azure.com/). Pour plus d’informations sur l’inscription d’applications Azure AD, consultez [Intégration avec Azure Active Directory](active-directory-how-to-integrate.md).

#### <a name="step-3-set-up-hello-correct-permissions-in-your-application"></a>Étape 3 : Configurer des autorisations appropriées de hello dans votre application
Notre application de service broker dans Android utilise la fonctionnalité du Gestionnaire de comptes hello d’informations d’identification de toomanage de système d’exploitation Android hello entre les applications. Dans courtier toouse hello dans Android votre manifeste d’application doit avoir des autorisations toouse AccountManager des comptes. Cela est décrit en détail dans hello [documentation Google pour le responsable de compte ici](http://developer.android.com/reference/android/accounts/AccountManager.html)

Ces autorisations sont les suivantes :

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a>Vous avez configuré l’authentification unique !
Maintenant hello Kit de développement logiciel de Microsoft Identity automatiquement à la fois partager des informations d’identification entre vos applications et appeler le service broker de hello si elle est présente sur leur appareil.

