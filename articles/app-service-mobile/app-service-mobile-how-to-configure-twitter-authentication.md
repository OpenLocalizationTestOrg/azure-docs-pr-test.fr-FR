---
title: "aaaHow tooconfigure Twitter l’authentification pour votre application de Services d’application"
description: "Découvrez comment l’authentification Twitter tooconfigure pour votre application de Services d’application."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 0d16ac44d7b54e3567b793a904059d31ab1d8911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-twitter-login"></a>Comment tooconfigure votre connexion de Service d’applications application toouse Twitter
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Cette rubrique vous montre comment tooconfigure Azure App Service toouse Twitter comme fournisseur d’authentification.

procédure de hello toocomplete dans cette rubrique, vous devez disposer d’un compte Twitter qui a un messagerie vérifié adresse et numéro de téléphone. toocreate un nouveau compte Twitter, accédez trop<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.

## <a name="register"></a>Inscription de votre application avec Twitter
1. Ouvrez une session sur toohello [portail Azure]et accédez tooyour application. Copiez votre **URL**. Vous utiliserez cette tooconfigure votre application Twitter.
2. Accédez toohello [aux développeurs de Twitter] site Web, connectez-vous avec vos informations d’identification du compte Twitter, puis cliquez sur **créer une application**.
3. Type Bonjour **nom** et un **Description** pour votre nouvelle application. Coller dans votre application **URL** pour hello **site Web** valeur. Ensuite, pour hello **URL de rappel**, collez hello **URL de rappel** vous avez copiée précédemment. Voici la passerelle d’application Mobile ajoutée au chemin d’accès de hello, */.auth/login/twitter/callback*. Par exemple, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`. Assurez-vous que vous utilisez le schéma HTTPS de hello.
4. Dans la page de hello hello bas, lisez et acceptez les termes du contrat de hello. Ensuite, cliquez sur **Create your Twitter application**. Cette application hello de registres affiche les détails de l’application hello.
5. Cliquez sur hello **paramètres** onglet, vérifiez **autoriser cette toosign de toobe utilisé application connecter avec Twitter**, puis cliquez sur **les paramètres de mise à jour**.
6. Sélectionnez hello **clés et les jetons d’accès** onglet. Prenez note des valeurs hello de **Consumer Key (clé d’API)** et **question secrète du client (clé secrète API)**.
   
   > [!NOTE]
   > secret de consommateur Hello est une information d’identification de sécurité importantes. Ne partagez pas cette clé secrète avec quiconque et ne la distribuez pas avec votre application.
   > 
   > 

## <a name="secrets"></a>Ajouter Twitter d’application des informations tooyour
1. Dans hello [portail Azure], accédez tooyour application. Cliquez sur **Paramètres**, puis sur **Authentification/Autorisation**.
2. Si l’authentification de hello / la fonctionnalité d’autorisation n’est pas activée, activer hello trop**sur**.
3. Cliquez sur **Twitter**. Collez hello ID d’application et Secret d’application les valeurs que vous avez obtenu précédemment. Cliquez ensuite sur **OK**.
   
   ![][1]
   
   Par défaut, le Service d’applications fournit l’authentification mais ne restreint pas les API et contenu de site tooyour autorisé à accéder. Vous devez autoriser les utilisateurs dans votre code d'application.
4. (Facultatif) toorestrict accès tooyour site tooonly les utilisateurs authentifiés par Twitter, définissez **tootake Action lors de la demande n’est pas authentifiée** trop**Twitter**. Cela requiert que toutes les demandes authentifiées, et toutes les demandes non authentifiées sont redirigée tooTwitter pour l’authentification.
5. Cliquez sur **Enregistrer**.

Vous êtes maintenant prêt toouse Twitter pour l’authentification dans votre application.

## <a name="related-content"></a>Contenu connexe
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[aux développeurs de Twitter]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[portail Azure]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
