---
title: "aaaAuthentication et l’autorisation dans les applications mobiles Azure | Documents Microsoft"
description: "Référence conceptuel et vue d’ensemble de hello d’authentification / autorisation de fonctionnalité pour les applications mobiles Azure"
services: app-service\mobile
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: a46dbf70-867d-48f6-8885-7f5207ad102e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 5255734481ada11afb65982aebe45c2a349402fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-mobile-apps"></a>Authentification et autorisation dans Azure Mobile Apps
## <a name="what-is-app-service-authentication--authorization"></a>Qu’est-ce que l’authentification/autorisation App Service ?
> [!NOTE]
> Cette rubrique sera migré tooa consolidé [App Service authentification / autorisation](../app-service/app-service-authentication-overview.md) rubrique, qui couvre les applications API Web et Mobile.
> 
> 

Application Service authentification / autorisation est une fonctionnalité qui permet de toolog de votre application dans les utilisateurs sans aucune modification de code requise sur le serveur principal d’application hello. Il fournit un moyen simple de tooprotect votre application et travailler avec des données par l’utilisateur.

Service de l’application utilise des identités fédérées, dans laquelle une partie 3 rd **fournisseur d’identité** (« IDP ») stocke les comptes et authentifie les utilisateurs et application hello utilise cette identité au lieu de son propre. Service d’applications prend en charge cinq fournisseurs d’identité en dehors de la zone de hello : *Azure Active Directory*, *Facebook*, *Google*, *Microsoft Account*, et *Twitter*. Vous pouvez également étendre cette prise en charge à vos applications en intégrant un autre fournisseur d’identité ou votre propre solution d’identité personnalisée.

Votre application peut exploiter plusieurs de ces fournisseurs d’identité, vous pouvez donc proposer à vos utilisateurs finaux plusieurs options de connexion.

Si vous le souhaitez tooget démarré immédiatement, veuillez consultez hello suivant didacticiels :

* [Ajouter une application de l’authentification tooyour iOS]
* [Ajouter une application de l’authentification tooyour Xamarin.iOS]
* [Ajouter une application de Xamarin.Android tooyour d’authentification]
* [Ajouter l’application Windows authentification tooyour]

## <a name="how-authentication-works"></a>Fonctionnement de l’authentification
Dans tooauthenticate de commande à l’aide d’un des fournisseurs d’identité hello, vous devez d’abord tooconfigure hello identité fournisseur tooknow sur votre application. fournisseur d’identité Hello vous fournira avec l’ID et les secrets que vous fournissiez arrière toohello application. Cela termine la relation d’approbation hello et du Service d’applications toovalidate identités fournies tooit.

Ces étapes sont détaillées dans hello rubriques suivantes :

* [Comment tooconfigure votre nom de connexion app toouse Azure Active Directory]
* [Comment tooconfigure votre connexion de Facebook toouse application]
* [Comment tooconfigure votre connexion de Google toouse application]
* [Comment tooconfigure votre connexion de Microsoft Account toouse application]
* [Comment tooconfigure votre connexion de Twitter toouse application]

Une fois que tout est configuré sur hello principal, vous pouvez modifier votre toolog client dans. Il existe deux approches :

* À l’aide d’une seule ligne de code, permettent de hello des applications mobiles client SDK connectez-vous aux utilisateurs.
* Tirer parti d’un kit de développement logiciel publié par une identité de tooestablish fournisseur identité donnée et ensuite obtenir l’accès tooApp Service.

> [!TIP]
> La plupart des applications doivent utiliser un tooget du Kit de développement logiciel fournisseur une expérience de connexion plus natif-sentiment et tooleverage actualisation prise en charge et d’autres avantages spécifiques au fournisseur.
> 
> 

### <a name="how-authentication-without-a-provider-sdk-works"></a>Fonctionnement de l’authentification sans Kit de développement logiciel (SDK) de fournisseur
Si vous ne souhaitez pas tooset un fournisseur de kit de développement logiciel, vous pouvez autoriser la connexion de hello tooperform applications mobiles pour vous. client des applications mobiles Hello SDK s’ouvre un fournisseur de toohello d’affichage web de votre choix et complètes hello de connexion. Occasionnellement sur les blogs et les forums, que vous pouvez voir cela appelle tooas hello « flux de serveur » ou « dirigée vers le serveur de flux » depuis le serveur de hello gère la connexion de hello et SDK de client hello ne reçoit jamais le jeton du fournisseur hello.

code de Hello nécessaire toostart que ce flux est décrite dans le didacticiel d’authentification hello pour chaque plateforme. À fin hello du flux de hello, le client de hello SDK dispose d’un jeton du Service d’applications, et jeton de hello est automatiquement attaché tooall demandes toohello principal.

### <a name="how-authentication-with-a-provider-sdk-works"></a>Fonctionnement de l’authentification avec un Kit de développement logiciel (SDK) de fournisseur
Utilisation d’un fournisseur de kit de développement logiciel permet toointeract d’ouverture de session de l’expérience hello plus étroitement avec la plateforme hello application hello de système d’exploitation est en cours d’exécution. Cela vous donne également un jeton du fournisseur et des informations utilisateur sur le client hello, ce qui rend beaucoup plus facile graphique de tooconsume API et personnaliser l’expérience utilisateur hello. Occasionnellement sur les blogs et forums vous verrez cette hello tooas référencé « flux client » ou « dirigée vers le client flux » depuis le code client de hello gère les connexion hello, et le code client hello a le jeton d’accès tooa fournisseur.

Une fois qu’un jeton du fournisseur est obtenu, il doit toobe envoyé tooApp Service pour la validation. À fin hello du flux de hello, le client de hello SDK dispose d’un jeton du Service d’applications, et jeton de hello est automatiquement attaché tooall demandes toohello principal. développeur de Hello peut également conserver un jeton du fournisseur toohello référence s’ils le souhaitent.

## <a name="how-authorization-works"></a>Fonctionnement de l’autorisation
Application Service authentification / autorisation expose plusieurs options pour **tootake Action lors de la demande n’est pas authentifiée**. Avant que votre code reçoit une demande donnée, vous pouvez avoir toosee de vérification du Service d’applications si hello requête est authentifiée et dans le cas contraire, il rejette et tentative de connexion de l’utilisateur toohave hello avant de réessayer.

Une option consiste à rediriger les demandes de toohave non authentifié tooone hello des fournisseurs d’identité. Dans un navigateur web, il faudrait réellement nouvelle page hello utilisateur tooa. En revanche, votre client mobile ne peut pas être redirigé de cette façon et les réponses non authentifiées reçoivent une erreur HTTP *401 non autorisé*. Compte tenu de cela, hello première demande permet de votre client doit toujours toohello point de terminaison de connexion, et vous pouvez faire appelle tooany autres API. Si vous essayez d’une autre API toocall avant de vous connecter, votre client reçoit une erreur.

Si vous le souhaitez toohave plus granulaire de contrôle sur les points de terminaison requièrent une authentification, vous pouvez également choisir « aucune action (autoriser la demande) » pour les demandes non authentifiées. Dans ce cas, toutes les décisions d’authentification sont différées tooyour code de l’application. Cela vous permet également aux utilisateurs toospecific tooallow accès selon les règles d’autorisation personnalisée.

## <a name="documentation"></a>Documentation
Hello suivant didacticiels indiquent comment tooadd authentification tooyour des clients mobiles à l’aide du Service d’applications :

* [Ajouter une application de l’authentification tooyour iOS]
* [Ajouter une application de l’authentification tooyour Xamarin.iOS]
* [Ajouter une application de Xamarin.Android tooyour d’authentification]
* [Ajouter l’application Windows authentification tooyour]

Hello suivant didacticiels indiquent comment tooconfigure du Service d’applications tooleverage différents fournisseurs d’authentification :

* [Comment tooconfigure votre nom de connexion app toouse Azure Active Directory]
* [Comment tooconfigure votre connexion de Facebook toouse application]
* [Comment tooconfigure votre connexion de Google toouse application]
* [Comment tooconfigure votre connexion de Microsoft Account toouse application]
* [Comment tooconfigure votre connexion de Twitter toouse application]

Si vous le souhaitez toouse un système d’identité autre que ceux hello fournies ici, vous pouvez également exploiter hello [afficher un aperçu de la prise en charge de l’authentification personnalisée dans hello .NET server SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth).

[Ajouter une application de l’authentification tooyour iOS]: app-service-mobile-ios-get-started-users.md
[Ajouter une application de l’authentification tooyour Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started-users.md
[Ajouter une application de Xamarin.Android tooyour d’authentification]: app-service-mobile-xamarin-android-get-started-users.md
[Ajouter l’application Windows authentification tooyour]: app-service-mobile-windows-store-dotnet-get-started-users.md

[Comment tooconfigure votre nom de connexion app toouse Azure Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Comment tooconfigure votre connexion de Facebook toouse application]: app-service-mobile-how-to-configure-facebook-authentication.md
[Comment tooconfigure votre connexion de Google toouse application]: app-service-mobile-how-to-configure-google-authentication.md
[Comment tooconfigure votre connexion de Microsoft Account toouse application]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Comment tooconfigure votre connexion de Twitter toouse application]: app-service-mobile-how-to-configure-twitter-authentication.md
