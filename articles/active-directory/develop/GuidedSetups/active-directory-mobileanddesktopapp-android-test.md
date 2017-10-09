---
title: aaaAzure AD v2 Android prise en main - Test | Documents Microsoft
description: "Cet article explique comment une application Android peut obtenir un jeton d’accès et appeler une ou plusieurs API Microsoft Graph qui nécessitent des jetons d’accès à partir du point de terminaison Azure Active Directory v2"
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
ms.openlocfilehash: 499f32b46fd44cca0e52179bced49b311135d8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Test de votre code

1. Déployer votre code tooyour/émulateur d’appareil.
2. Lorsque vous êtes prêt tootest, utilisez un Microsoft Azure Active Directory (compte professionnel) ou un toosign de compte Account Microsoft (live.com, outlook.com) dans. 

![Exemple d’écran](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
<br/><br/>
![Connexion](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)

### <a name="consent"></a>Consentement
Hello première fois, qu'un utilisateur se connecte à l’application de tooyour, ils seront afficheront avec un consentement écran similaire toohello ci-dessous, où ils doivent accepter les tooexplicitly : 

![Consentement](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a>Résultats attendus
Vous devez voir les résultats de hello d’un tooMicrosoft d’appel de l’API Graph 'me' point de terminaison utilisé profil_utilisateur hello tootooobtain - https://graph.microsoft.com/v1.0/me. Pour obtenir la liste des points de terminaison Microsoft Graph les plus courants, consultez cet [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Informations supplémentaires sur les étendues et les autorisations déléguées

Hello Microsoft Graph API nécessite hello `user.read` étendue tooread hello profil utilisateur. Par défaut, cette étendue est automatiquement ajoutée à toutes les applications inscrites dans notre portail d’inscription. D’autres API pour Microsoft Graph ainsi que des API personnalisées pour votre serveur principal peuvent nécessiter des étendues supplémentaires. Par exemple, pour Microsoft Graph, hello étendue `Calendars.Read` est calendriers de l’utilisateur requise toolist hello. Dans l’ordre tooaccess hello calendrier de l’utilisateur dans un contexte d’une application, vous devez tooadd hello `Calendars.Read` délégation des informations d’inscription d’autorisation toohello application, puis ajoutez hello `Calendars.Read` étendue toohello `acquireTokenSilentAsync` appeler. utilisateur de Hello peut être invité pour les autorisations supplémentaires lorsque vous augmentez le nombre de hello d’étendues.

<!--end-collapse-->
