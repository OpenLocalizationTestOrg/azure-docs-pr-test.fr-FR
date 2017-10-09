---
title: "aaaHow tooconfigure Account Microsoft l’authentification pour votre application de Services d’application"
description: "Découvrez comment l’authentification de Microsoft Account tooconfigure pour votre application de Services d’application."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a>Comment tooconfigure votre connexion au Service d’applications application toouse Account Microsoft
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

Cette rubrique vous montre comment tooconfigure Azure App Service toouse Account Microsoft comme fournisseur d’authentification. 

## <a name="register-microsoft-account"></a>Inscription de votre application avec un compte Microsoft
1. Ouvrez une session sur toohello [portail Azure]et accédez tooyour application. Copiez votre **URL**, qui vous utiliserez tooconfigure votre application avec Account Microsoft.
2. Accédez toohello [Mes Applications] page hello Microsoft Account Developer Center et connectez-vous avec votre compte Microsoft, si nécessaire.
3. Cliquez sur **Ajouter une application**, puis tapez le nom de l’application et cliquez sur **Créer une application**.
4. Prenez note de hello **ID de l’Application**, car vous en aurez besoin plus tard. 
5. Sous « Plateformes », cliquez sur **Ajouter une plateforme** et sélectionnez « Web ».
6. Sous « URI de redirection » approvisionnement hello point de terminaison pour votre application, puis cliquez sur **enregistrer**. 
   
   > [!NOTE]
   > Votre URI de redirection est hello les URL de votre application ajoutée avec le chemin d’accès de hello, */.auth/login/microsoftaccount/callback*. Par exemple, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.   
   > Assurez-vous que vous utilisez le schéma HTTPS de hello.
   
7. Sous « Secrets de l’application », cliquez sur **Générer un nouveau mot de passe**. Notez la valeur hello qui s’affiche. Une fois que vous quittez la page de hello, il ne sera pas affiché à nouveau.

    > [!IMPORTANT]
    > mot de passe Hello est une information d’identification de sécurité importantes. Ne partagez le mot de passe de hello avec d’autres personnes ou le distribuer dans une application cliente.

## <a name="secrets"></a>Ajouter un compte Microsoft informations tooyour application de Service d’application
1. Dans hello [portail Azure], accédez tooyour application, cliquez sur **paramètres** > **l’authentification / autorisation**.
2. Si l’authentification de hello / la fonctionnalité d’autorisation n’est pas activée, connectez-le **sur**.
3. Cliquez sur **Compte Microsoft**. Coller dans les valeurs hello ID d’Application et le mot de passe que vous avez obtenu précédemment et vous pouvez éventuellement activer des étendues de que votre application requiert. Cliquez ensuite sur **OK**.
   
    ![][1]
   
    Par défaut, le Service d’applications fournit l’authentification mais ne restreint pas les API et contenu de site tooyour autorisé à accéder. Vous devez autoriser les utilisateurs dans votre code d'application.
4. (Facultatif) toorestrict tooyour site tooonly les utilisateurs d’accès authentifiés par un compte Microsoft, définissez **tootake Action lors de la demande n’est pas authentifiée** trop**Account Microsoft**. Cela requiert que toutes les demandes authentifiées, et toutes les demandes non authentifiées sont redirigées compte tooMicrosoft pour l’authentification.
5. Cliquez sur **Enregistrer**.

Vous êtes maintenant prêt toouse Account Microsoft pour l’authentification dans votre application.

## <a name="related-content"></a>Contenu connexe
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[Mes Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[portail Azure]: https://portal.azure.com/
