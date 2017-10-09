---
title: aaaAzure AD v2 iOS route - Test | Documents Microsoft
description: "Cet article explique comment les applications iOS (Swift) peuvent appeler une API qui nécessite des jetons d’accès à partir d’un point de terminaison Azure Active Directory v2."
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
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 98c73eddabf9664feb19ac6878e9d7315b9aa79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="test-querying-hello-microsoft-graph-api-from-your-ios-application"></a>Test d’interrogation hello Microsoft Graph API à partir de votre application iOS

Appuyez sur `Command`  +  `R` code hello toorun simulateur de hello.

![Exemple d’écran](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

Quand vous êtes prêt tootest, appuyez sur *'Appeler l’API Microsoft Graph'* et vous est demandée tootype votre nom d’utilisateur et un mot de passe.

### <a name="consent"></a>Consentement
Hello première fois que vous vous connectez tooyour application, vous aurez un consentement écran similaire toohello ci-dessous, où vous devez accepter les tooexplicitly :

![Écran de consentement](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a>Résultats attendus
Vous devez voir les informations de profil utilisateur retournées par l’appel de l’API Microsoft Graph hello Bonjour *journalisation* section.

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Informations supplémentaires sur les étendues et les autorisations déléguées

Hello Microsoft Graph API nécessite hello `user.read` étendue tooread hello profil utilisateur. Par défaut, cette étendue est automatiquement ajoutée à toutes les applications inscrites dans notre portail d’inscription. D’autres API pour Microsoft Graph ainsi que des API personnalisées pour votre serveur principal peuvent nécessiter des étendues supplémentaires. Par exemple, pour Microsoft Graph, hello étendue `Calendars.Read` est calendriers de l’utilisateur requise toolist hello. Dans l’ordre tooaccess hello calendrier de l’utilisateur dans un contexte d’une application, vous devez tooadd hello `Calendars.Read` délégation des informations d’inscription d’autorisation toohello application, puis ajoutez hello `Calendars.Read` étendue toohello `acquireTokenSilent` appeler. utilisateur de Hello peut être invité pour les autorisations supplémentaires lorsque vous augmentez le nombre de hello d’étendues.

<!--end-collapse-->



