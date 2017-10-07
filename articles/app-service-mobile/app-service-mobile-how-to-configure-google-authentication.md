---
title: "aaaHow tooconfigure Google l’authentification pour votre application de Services d’application"
description: "Découvrez comment l’authentification Google tooconfigure pour votre application de Services d’application."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a>Comment tooconfigure votre compte de connexion du Service d’applications application toouse Google
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Cette rubrique vous montre comment tooconfigure Azure App Service toouse Google comme fournisseur d’authentification.

procédure de hello toocomplete dans cette rubrique, vous devez disposer d’un compte Google qui possède une adresse de messagerie vérifié. toocreate un nouveau compte Google, accédez trop[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).

## <a name="register"></a>Inscription de votre application avec Google
1. Ouvrez une session sur toohello [portail Azure]et accédez tooyour application. Copiez votre **URL**, qui vous utilisez tooconfigure ultérieure de votre application de Google.
2. Accédez toohello [API Google](http://go.microsoft.com/fwlink/p/?LinkId=268303) cliquez sur le site Web, connectez-vous avec vos informations d’identification du compte Google, **créer un projet de**, fournissez un **nom du projet**, puis cliquez sur  **Créer**.
3. Sous **API sociales**, cliquez sur **API Google+** puis **Activer**.
4. Bonjour, barre de navigation gauche **informations d’identification** > **écran de consentement OAuth**, puis sélectionnez votre **adresse de messagerie**, entrez un **nomduproduit**, puis cliquez sur **enregistrer**.
5. Bonjour **informations d’identification** , cliquez sur **créer les informations d’identification** > **ID de client OAuth**, puis sélectionnez **application Web**.
6. Coller hello du Service d’applications **URL** vous avez copiée précédemment dans **origines JavaScript**, puis collez votre redirection URI en **URI de redirection autorisés**. Hello URI de redirection est hello les URL de votre application ajoutée avec le chemin d’accès de hello, */.auth/login/google/callback*. Par exemple, `https://contoso.azurewebsites.net/.auth/login/google/callback`. Assurez-vous que vous utilisez le schéma HTTPS de hello. Cliquez ensuite sur **Créer**.
7. Sur l’écran suivant de hello, prenez note des valeurs hello du client de hello secret ID et le client.

    > [!IMPORTANT]
    > question secrète du client Hello est une information d’identification de sécurité importantes. Ne partagez cette clé secrète avec personne et ne la distribuez pas dans une application cliente.


## <a name="secrets"></a>Tooyour d’application Google d’ajouter des informations
1. Dans hello [portail Azure], accédez tooyour application. Cliquez sur **Paramètres**, puis sur **Authentification/Autorisation**.
2. Si l’authentification de hello / la fonctionnalité d’autorisation n’est pas activée, activer hello trop**sur**.
3. Cliquez sur **Google**. Coller dans les valeurs d’ID d’application et le Secret de l’application hello que vous avez obtenu précédemment et vous pouvez éventuellement activer des étendues de que votre application requiert. Cliquez ensuite sur **OK**.
   
   ![][1]
   
   Par défaut, le Service d’applications fournit l’authentification mais ne restreint pas les API et contenu de site tooyour autorisé à accéder. Vous devez autoriser les utilisateurs dans votre code d'application.
4. (Facultatif) toorestrict accès tooyour site tooonly les utilisateurs authentifiés par Google, définissez **tootake Action lors de la demande n’est pas authentifiée** trop**Google**. Cela requiert que toutes les demandes authentifiées, et toutes les demandes non authentifiées sont redirigée tooGoogle pour l’authentification.
5. Cliquez sur **Enregistrer**.

Vous êtes maintenant prêt toouse Google pour l’authentification dans votre application.

## <a name="related-content"></a>Contenu connexe
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[portail Azure]: https://portal.azure.com/

