---
title: aaaAzure AD v2 Windows Desktop mise en route - Test | Documents Microsoft
description: "Cet article explique comment les applications de bureau Windows .NET (XAML) peuvent appeler une API qui nécessite des jetons d’accès à partir d’un point de terminaison Azure Active Directory v2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 0ae9612e1585c54a3fe35ba9d18f92554099b2c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Test de votre code

Dans commande tootest votre application, appuyez sur `F5` toorun votre projet dans Visual Studio. Votre fenêtre principale doit alors s’afficher :

![Exemple d’écran](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

Lorsque vous êtes prêt tootest, cliquez sur *appeler l’API Microsoft Graph* et utiliser un annuaire Microsoft Azure Active Directory (compte professionnel) ou un toosign de compte Account Microsoft (live.com, outlook.com) dans. Il c’est hello la première fois, vous verrez une fenêtre demandant toosign utilisateur dans :

![Connexion](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a>Consentement
Hello première fois que vous vous connectez tooyour application, vous aurez un consentement écran similaire toohello ci-dessous, où vous devez accepter les tooexplicitly :

![Écran de consentement](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a>Résultats attendus
Vous devez voir les informations de profil utilisateur retournées par l’appel de l’API Microsoft Graph hello sur l’écran des résultats d’appels API hello.

Vous devez également voir les informations de base sur le jeton hello acquis `AcquireTokenAsync` ou `AcquireTokenSilentAsync` dans la zone des informations de jeton hello :

|Propriété  |Format  |Description |
|---------|---------|---------|
|Nom | {Nom complet de l’utilisateur} |utilisateur de Hello prénom et nom|
|Nom d’utilisateur |<span>user@domain.com</span> |nom d’utilisateur Hello utilisé utilisateur de hello tooidentify|
|Token Expires (Expiration du jeton) |{DateHeure}         |Hello expiration sur le hello jeton. MSAL étendra date d’expiration de hello pour vous par le renouvellement de jeton hello lorsque cela est nécessaire|
|Access token (Jeton d’accès) |{Chaîne}         |chaîne de jeton Hello envoyé des demandes de tooHTTP qui nécessitent un en-tête d’autorisation qui sera envoyé|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Informations supplémentaires sur les étendues et les autorisations déléguées
L’API Graph requiert hello `user.read` tooread profil_utilisateur d’étendue. Par défaut, cette étendue est automatiquement ajoutée à toutes les applications inscrites dans notre portail d’inscription. D’autres API Graph ainsi que des API personnalisées pour votre serveur principal nécessitent des étendues supplémentaires. Par exemple, pour un graphique, `Calendars.Read` est calendriers de l’utilisateur toolist requis. Dans l’ordre tooaccess hello calendrier de l’utilisateur dans un contexte d’une application, vous devez tooadd `Calendars.Read` délégation des informations d’inscription de l’application, puis ajoutez `Calendars.Read` toohello `AcquireTokenAsync` appeler. Utilisateur demandera peut-être d’autorisations supplémentaires lorsque vous augmentez le nombre de hello d’étendues.

<!--end-collapse-->



