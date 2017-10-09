---
title: "authentification Facebook aaaHow tooconfigure pour votre application de Services d’application"
description: "Découvrez comment tooconfigure l’authentification Facebook pour votre application de Services d’application."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 53d03445a2ad17de1d2f69f5e770d14385b48ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-facebook-login"></a>Comment tooconfigure la connexion de Facebook toouse de votre application du Service d’applications
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Cette rubrique vous montre comment tooconfigure Azure App Service toouse Facebook comme fournisseur d’authentification.

procédure de hello toocomplete dans cette rubrique, vous devez disposer d’un compte Facebook qui a une adresse de messagerie vérifié et un numéro de téléphone mobile. toocreate un nouveau compte Facebook, accédez trop[facebook.com].

## <a name="register"></a>Inscription de votre application sur Facebook
1. Ouvrez une session sur toohello [portail Azure]et accédez tooyour application. Copiez votre **URL**. Vous utiliserez cette tooconfigure votre application Facebook.
2. Dans une autre fenêtre de navigateur, accédez à toohello [aux développeurs de Facebook] site Web et connectez-vous avec votre Facebook des informations d’identification de compte.
3. (Facultatif) Si vous n’êtes pas déjà inscrit, cliquez sur **applications** > **enregistrer en tant que développeur**, acceptez la politique de hello, puis suivez les étapes d’inscription de hello.
4. Cliquez sur **Mes applications** > **Ajouter une nouvelle application** > **Site Web** > **Ignorer et créer un ID d’application**. 
5. Dans **nom d’affichage**, tapez un nom unique pour votre application, le type de votre **messagerie du Contact**, choisissez un **catégorie** pour votre application, puis cliquez sur **créer des ID d’application**et terminer la vérification de sécurité hello. Vous passez le tableau de bord du développeur de toohello pour votre nouvelle application Facebook.
6. Sous « Facebook Login » (Connexion Facebook), cliquez sur **Get Started**(Prise en main). Ajout de votre application **URI de redirection** trop**URI de redirection OAuth valide**, puis cliquez sur **enregistrer les modifications**. 
   
   > [!NOTE]
   > Votre URI de redirection est hello les URL de votre application ajoutée avec le chemin d’accès de hello, */.auth/login/facebook/callback*. Par exemple, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`. Assurez-vous que vous utilisez le schéma HTTPS de hello.
   > 
   > 
7. Dans hello navigation gauche, cliquez sur **paramètres**. Sur hello **Secret d’application** , cliquez sur **afficher**, fournir votre mot de passe si demandé, puis prenez note des valeurs hello de **ID d’application** et **Secret d’application**. Vous utilisez ces tooconfigure ultérieure de votre application dans Azure.
   
   > [!IMPORTANT]
   > secret d’application Hello est une information d’identification de sécurité importantes. Ne partagez cette clé secrète avec personne et ne la distribuez pas dans une application cliente.
   > 
   > 
8. Hello compte Facebook qui a été utilisé tooregister hello application est un administrateur de l’application hello. À ce stade, seuls les administrateurs peuvent se connecter à cette application. tooauthenticate autres comptes Facebook, cliquez sur **révision d’application** et activer **rendent < votre-app-name > publics** tooenable accès public général à l’aide de l’authentification Facebook.

## <a name="secrets"></a>Tooyour d’application Facebook d’ajouter des informations
1. Dans hello [portail Azure], accédez tooyour application. Cliquez sur **Paramètres** > **Authentification / Autorisation**, et vérifiez que **l’authentification App Service** est activée, sur **On**.
2. Cliquez sur **Facebook**, collez dans les valeurs d’ID d’application et le Secret de l’application hello que vous avez obtenu précédemment, si vous le souhaitez activer toutes les étendues requises par votre application, puis cliquez sur **OK**.
   
    ![][0]
   
    Par défaut, le Service d’applications fournit l’authentification mais ne restreint pas les API et contenu de site tooyour autorisé à accéder. Vous devez autoriser les utilisateurs dans votre code d'application.
3. (Facultatif) toorestrict accès tooyour site tooonly les utilisateurs authentifiés par Facebook, définissez **tootake Action lors de la demande n’est pas authentifiée** trop**Facebook**. Cela requiert que toutes les demandes authentifiées, et toutes les demandes non authentifiées sont redirigée tooFacebook pour l’authentification.
4. Lorsque vous avez terminé de configurer l’authentification, cliquez sur **Enregistrer**.

Vous êtes maintenant prêt toouse Facebook pour l’authentification dans votre application.

## <a name="related-content"></a>Contenu connexe
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
[aux développeurs de Facebook]: http://go.microsoft.com/fwlink/p/?LinkId=268286
[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
[portail Azure]: https://portal.azure.com/
