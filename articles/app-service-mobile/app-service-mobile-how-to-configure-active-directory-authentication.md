---
title: "authentification d’Azure Active Directory tooconfigure aaaHow pour votre application de Services d’application"
description: "Découvrez comment tooconfigure l’authentification Azure Active Directory pour votre application de Services d’application."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: 6ec6a46c-bce4-47aa-b8a3-e133baef22eb
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 5b1d73f8fdf5831a266d900cd07f4e3b0917a7f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-azure-active-directory-login"></a>Comment tooconfigure votre connexion de Service d’applications application toouse Azure Active Directory
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Cette rubrique vous montre comment les Services d’application Azure de tooconfigure toouse Azure Active Directory comme fournisseur d’authentification.

## <a name="express"></a>Configuration d'Azure Active Directory à l'aide de la configuration rapide
1. Bonjour [portail Azure], accédez tooyour application. Cliquez sur **Paramètres**, puis sur **Authentification/Autorisation**.
2. Si l’authentification de hello / la fonctionnalité d’autorisation n’est pas activée, activer hello trop**sur**.
3. Cliquez sur **Azure Active Directory**, puis sur **Rapide** sous **Mode de gestion**.
4. Cliquez sur **OK** application hello de tooregister dans Azure Active Directory. Une nouvelle inscription est alors créée. Si vous souhaitez toochoose une inscription existante au lieu de cela, cliquez sur **sélectionner une application existante** , puis recherchez le nom hello d’une inscription précédemment créée au sein de votre client.
   Cliquez sur hello inscription tooselect il sur **OK**. Puis cliquez sur **OK** sur le panneau des paramètres Azure Active Directory hello.
   
   ![][0]
   
   Par défaut, le Service d’applications fournit l’authentification mais ne restreint pas les API et contenu de site tooyour autorisé à accéder. Vous devez autoriser les utilisateurs dans votre code d'application.
5. (Facultatif) toorestrict accès tooyour site tooonly les utilisateurs authentifiés par Azure Active Directory, définissez **tootake Action lors de la demande n’est pas authentifiée** trop**se connecter avec Azure Active Directory**. Cela requiert que toutes les demandes authentifiées, et toutes les demandes non authentifiées sont redirigée tooAzure Active Directory pour l’authentification.
6. Cliquez sur **Enregistrer**.

Vous êtes maintenant prêt toouse Azure Active Directory pour l’authentification dans votre application.

## <a name="advanced"></a>(Méthode alternative) Configurer manuellement Azure Active Directory avec des paramètres avancés
Vous pouvez également choisir tooprovide paramètres de configuration manuellement. Il s’agit de solution de hello préféré si client AAD de hello vous souhaitez toouse est différente de locataire hello avec lequel vous vous connectez à Azure. configuration de hello toocomplete, vous devez d’abord créer un enregistrement dans Azure Active Directory, et vous devez fournir des tooApp détails de l’inscription hello Service.

### <a name="register"></a>Inscription de votre application auprès d’Azure Active Directory
1. Ouvrez une session sur toohello [portail Azure]et accédez tooyour application. Copiez votre **URL**. Vous utiliserez cette tooconfigure votre application Azure Active Directory.
2. Connectez-vous à toohello [portail Azure classic] et accédez trop**Active Directory**.
   
    ![][2]
3. Sélectionnez votre annuaire, puis hello **Applications** onglet en haut de hello. Cliquez sur **ajouter** à hello bas toocreate une nouvelle inscription de l’application.
4. Cliquez sur **Ajouter une application développée par mon organisation**.
5. Dans hello Assistant Ajout de l’Application, entrez un **nom** pour hello de votre application et cliquez sur **Web Application et/ou API Web** type. Cliquez ensuite sur toocontinue.
6. Bonjour **URL de connexion** zone, collez l’URL de l’application hello vous avez copiée précédemment. Entrez cette URL même Bonjour **URI ID d’application** boîte. Cliquez ensuite sur toocontinue.
7. Une fois que l’application hello a été ajoutée, cliquez sur hello **configurer** onglet. Modifier hello **URL de réponse** sous **Single Sign-on** URL de hello toobe de votre application ajoutée avec le chemin d’accès de hello, */.auth/login/aad/callback*. Par exemple, `https://contoso.azurewebsites.net/.auth/login/aad/callback`. Assurez-vous que vous utilisez le schéma HTTPS de hello.
   
    ![][3]
8. Cliquez sur **Enregistrer**. Puis hello de copie **ID Client** pour l’application hello. Vous allez configurer votre application toouse cela plus tard.
9. Dans la barre de commandes hello bas, cliquez sur **points de terminaison**et puis copie Bonjour **Document de métadonnées de fédération** URL et le téléchargement de document ou accédez tooit dans un navigateur.
10. Dans la racine de hello **EntityDescriptor** élément, il doit y avoir un **entityID** attribut sous forme de hello `https://sts.windows.net/` suivi par un client spécifique tooyour GUID (appelé « ID client »). Copiez cette valeur qui servira d' **URL de l'émetteur**. Vous allez configurer votre application toouse cela plus tard.

### <a name="secrets"></a>Application de tooyour informations ajouter Azure Active Directory
1. Dans hello [portail Azure], accédez tooyour application. Cliquez sur **Paramètres**, puis sur **Authentification/Autorisation**.
2. Si la fonctionnalité d’authentification/autorisation hello n’est pas activée, activer hello trop**sur**.
3. Cliquez sur **Azure Active Directory**, puis sur **Avancé** sous **Mode de gestion**. Coller dans hello ID Client et l’URL de l’émetteur de valeur que vous obtenu précédemment. Cliquez ensuite sur **OK**.
   
   ![][1]
   
   Par défaut, le Service d’applications fournit l’authentification mais ne restreint pas les API et contenu de site tooyour autorisé à accéder. Vous devez autoriser les utilisateurs dans votre code d'application.
4. (Facultatif) toorestrict accès tooyour site tooonly les utilisateurs authentifiés par Azure Active Directory, définissez **tootake Action lors de la demande n’est pas authentifiée** trop**se connecter avec Azure Active Directory**. Cela requiert que toutes les demandes authentifiées, et toutes les demandes non authentifiées sont redirigée tooAzure Active Directory pour l’authentification.
5. Cliquez sur **Enregistrer**.

Vous êtes maintenant prêt toouse Azure Active Directory pour l’authentification dans votre application.

## <a name="optional-configure-a-native-client-application"></a>(Facultatif) Configurer une application cliente native
Azure Active Directory vous permet également les clients natifs tooregister, qui offre un meilleur contrôle sur les autorisations de mappage. Vous en avez besoin si vous souhaitez que les connexions tooperform à l’aide d’une bibliothèque, par exemple hello **bibliothèque d’authentification Active Directory**.

1. Accédez trop**Active Directory** Bonjour [portail Azure classic].
2. Sélectionnez votre annuaire, puis hello **Applications** onglet en haut de hello. Cliquez sur **ajouter** à hello bas toocreate une nouvelle inscription de l’application.
3. Cliquez sur **Ajouter une application développée par mon organisation**.
4. Dans hello Assistant Ajout de l’Application, entrez un **nom** pour hello de votre application et cliquez sur **Application cliente Native** type. Cliquez ensuite sur toocontinue.
5. Bonjour **URI de redirection** , entrez de votre site */.auth/login/done* point de terminaison, à l’aide du schéma HTTPS de hello. Cette valeur doit être similaire trop*https://contoso.azurewebsites.net/.auth/login/done*. Si vous créez une application Windows, à la place utiliser hello [SID du package](app-service-mobile-dotnet-how-to-use-client-library.md#package-sid) comme hello URI.
6. Une fois que l’application native hello a été ajoutée, cliquez sur hello **configurer** onglet. Recherche hello **ID Client** et prenez note de cette valeur.
7. Page hello de défilement vers le bas toohello **autorisations tooother applications** et cliquez sur **ajouter application**.
8. Recherchez application hello web que vous avez enregistré précédemment et cliquez sur l’icône plus hello. Cliquez ensuite sur la boîte de dialogue hello cocher tooclose hello. Si l’application web de hello ne peut pas être trouvé, accédez tooits inscription et ajouter une nouvelle URL de réponse (par exemple, hello version HTTP de l’URL actuelle), cliquez sur Enregistrer, puis répétez ces étapes - application hello doit apparaissent dans la liste de hello.
9. Sur l’entrée de nouveau hello vous venez d’ajouter, ouvrez hello **autorisations déléguées** liste déroulante et sélectionnez **accès (appName)**. Cliquez ensuite sur **Enregistrer**.

Vous avez maintenant configuré une application cliente native qui peut accéder à votre application App Service.

## <a name="related-content"></a>Contenu connexe
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-express-settings.png
[1]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-advanced-settings.png
[2]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-navigate-aad.png
[3]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-aad-app-configure.png

<!-- URLs. -->

[portail Azure]: https://portal.azure.com/
[portail Azure classic]: https://manage.windowsazure.com/
[alternative method]:#advanced
