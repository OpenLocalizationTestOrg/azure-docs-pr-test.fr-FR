---
title: "aaaAzure AD v2 JS SPA guidée par le programme d’installation - Test | Documents Microsoft"
description: "Comment les applications JavaScript SPA peuvent appeler une API qui nécessite des jetons d’accès à partir d’un point de terminaison Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: b2339431a070b5c4ad4058e6c1a9b19b83c84c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Test de votre code

> ### <a name="testing-with-visual-studio"></a>Test avec Visual Studio
> Si vous utilisez Visual Studio, appuyez sur `F5` toorun votre projet : navigateur de hello s’ouvre et vous dirige trop*http://localhost : {port}* où vous voyez hello *appeler l’API Microsoft Graph* bouton.

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a>Test avec Python ou un autre serveur web
> Si vous n’utilisez pas Visual Studio, assurez-vous que votre serveur web est démarré et il est configuré le port TCP toolisten tooa selon hello dossier contenant votre *index.html* fichier. Pour Python, vous pouvez démarrer l’écoute port toohello en exécutant hello dans la commande hello invite / Terminal Server, à partir du dossier de l’application hello :
> 
> ```bash
> python -m http.server 8080
> ```
>  Ensuite, ouvrez le navigateur de hello et tapez *http://localhost : 8080* ou *http://localhost : {port}* - où hello *port* correspond toohello port de votre serveur web écoute. Vous devez voir le contenu de hello de votre page index.html avec hello *appeler l’API Microsoft Graph* bouton.

## <a name="test-your-application"></a>Tester votre application

Après avoir browser de hello charge votre *index.html*, cliquez sur hello *appeler l’API Microsoft Graph* bouton. S’il s’agit hello première fois, redirections du navigateur hello vous toohello Microsoft Azure Active Directory v2 point de terminaison, dans lequel vous êtes invité à entrer toosign dans.
 
![Exemple d’écran](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a>Consentement
Hello première fois que vous vous connectez tooyour application, vous sont présentées avec un consentement écran similaire toohello qui suit, où vous avez besoin de tooaccept :

 ![Écran de consentement](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a>Résultats attendus
Vous devez voir les informations de profil utilisateur retournées par hello réponse à un appel API Graph de Microsoft.
 
 ![Résultats](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

Vous voyez également les informations de base sur le jeton hello acquis Bonjour *jeton d’accès* et *revendications de jeton d’ID* cases.

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Informations supplémentaires sur les étendues et les autorisations déléguées

Hello Microsoft Graph API nécessite hello `user.read` étendue tooread hello profil utilisateur. Par défaut, cette étendue est automatiquement ajoutée à toutes les applications inscrites dans notre portail d’inscription. D’autres API pour Microsoft Graph ainsi que des API personnalisées pour votre serveur principal peuvent nécessiter des étendues supplémentaires. Par exemple, pour Microsoft Graph, hello étendue `Calendars.Read` est calendriers de l’utilisateur requise toolist hello. Dans l’ordre tooaccess hello calendrier de l’utilisateur dans le contexte de hello d’une application, vous devez tooadd hello `Calendars.Read` délégation des informations d’inscription d’autorisation toohello application, puis ajoutez hello `Calendars.Read` étendue toohello `acquireTokenSilent` appeler. utilisateur de Hello peut être invité pour les autorisations supplémentaires lorsque vous augmentez le nombre de hello d’étendues.

Si une API de service principal ne requiert pas une étendue (non recommandée), vous pouvez utiliser hello `clientId` comme étendue hello Bonjour `acquireTokenSilent` et/ou `acquireTokenRedirect` appels.

<!--end-collapse-->
