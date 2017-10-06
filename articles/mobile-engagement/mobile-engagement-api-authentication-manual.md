---
title: "aaaAuthenticate avec l’API REST de Mobile Engagement - le programme d’installation manuelle"
description: "Décrit comment toomanually configurer l’authentification pour l’API REST de Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2e79f9c9-41e4-45ac-b427-3b8338675163
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3884f94afcd6b9a62bfcf498fb6ee84bb6e837b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a>Azure Mobile Engagement - Configuration manuelle de l’utilisation des API pour l’authentification
Il s’agit d’une documentation annexe trop[authentifier avec les API REST Mobile Engagement](mobile-engagement-api-authentication.md). Assurez-vous que vous les ayez lues premier contexte de hello tooget. Cette section décrit une autre façon toodo hello d’installation unique pour le paramétrage de l’authentification pour à l’aide des API de REST Mobile Engagement hello hello portail Azure. 

> [!NOTE]
> instructions Hello ci-dessous sont basées sur ce [guide Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md) et personnalisée pour ce qui est requis pour l’authentification pour les API d’Engagement Mobile. Par conséquent, consultez tooit si vous souhaitez que les étapes de hello toounderstand ci-dessous en détail. 
> 
> 

1. Connexion tooyour compte Azure via hello [portail classic](https://manage.windowsazure.com/).
2. Sélectionnez **Active Directory** hello volet de gauche.
   
     ![sélectionner Active Directory][1]
3. Choisissez hello **par défaut Active Directory** dans votre portail Azure. 
   
     ![choisir l’annuaire][2]
   
   > [!IMPORTANT]
   > Cette approche fonctionne uniquement lorsque vous travaillez dans la valeur par défaut de hello Active Directory de votre compte et ne fonctionnera pas si vous effectuez cette opération dans Active Directory que vous avez créés dans votre compte. 
   > 
   > 
4. applications de hello tooview dans votre annuaire, cliquez sur **Applications**.
   
     ![afficher les applications][3]
5. Cliquez sur **AJOUTER**. 
   
     ![ajouter l’application][4]
6. Cliquez sur **Ajouter une application développée par mon organisation**
   
     ![nouvelle application][5]
7. Entrez le nom de l’application hello et de type hello select de l’application en tant que **WEB APPLICATION et/ou API WEB** et cliquez sur le bouton suivant de hello.
   
     ![nommer l’application][6]
8. Vous pouvez fournir des URL factices pour **l’URL DE CONNEXION** et **l’URI ID D’APPLICATION**. Ils ne sont pas utilisés dans notre scénario et URL hello eux-mêmes ne sont pas validées.  
   
     ![propriétés de l’application][7]
9. Extrémité hello de cela, vous aurez une application AAD avec nom hello fourni précédemment hello suivante. Il s’agit de votre **AD\_APP\_NAME**. Prenez-en note.  
   
     ![nom de l’application][8]
10. Cliquez sur le nom de l’application hello et cliquez sur **configurer**.
    
      ![configurer l’application][9]
11. Prenez note de hello ID de CLIENT qui sera utilisé comme **CLIENT\_ID** pour votre API appelle. 
    
     ![configurer l’application][10]
12. Faites défiler vers le bas toohello **clés** section et ajouter une clé avec une durée de 2 ans (expiration), de préférence, puis cliquez sur **enregistrer**. 
    
     ![configurer l’application][11]
13. Copier immédiatement la valeur hello qui est affichée pour la clé de hello lorsqu’il ne s’affiche désormais et n’est pas stockée afin de s’afficheront pas jamais. Si vous le perdez puis avoir toogenerate une nouvelle clé. Il s’agit de hello **CLIENT_SECRET** pour votre API appelle. 
    
     ![configurer l’application][12]
    
    > [!IMPORTANT]
    > Cette clé expire à fin hello de durée de hello que vous avez spécifié dans ce toorenew vraiment rendre il hello moment venu sinon l’authentification d’API ne fonctionnera plus. Vous pouvez également supprimer et recréer cette clé si vous pensez qu’elle a été compromise.
    > 
    > 
14. Cliquez sur **points de terminaison** bouton maintenant qui s’ouvre hello **points de terminaison** boîte de dialogue. 
    
    ![][13]
15. À partir de la boîte de dialogue points de terminaison hello, copiez hello **OAUTH 2.0 TOKEN ENDPOINT**. 
    
    ![][14]
16. Ce point de terminaison sera Bonjour suivant formulaire où hello GUID dans l’URL de hello est votre **TENANT_ID** par conséquent, prenez note de celui-ci : 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. Maintenant, nous continuerons tooconfigure les autorisations de hello sur cette application. Pour cela, vous aurez tooopen des hello [portail Azure](https://portal.azure.com). 
18. Cliquez sur **groupes de ressources** et recherche hello **Mobile Engagement** groupe de ressources.  
    
    ![][15]
19. Cliquez sur hello **Mobile Engagement** ressource de groupe et accédez toohello **paramètres** panneau ici. 
    
    ![][16]
20. Cliquez sur **utilisateurs** dans hello panneau des paramètres, puis cliquez sur **ajouter** tooadd un utilisateur. 
    
    ![][17]
21. Cliquez sur **Sélectionner un rôle**
    
    ![][18]
22. Cliquez sur **Propriétaire**
    
    ![][19]
23. Recherchez le nom hello de votre application **AD\_application\_nom** dans la zone de recherche hello. Il n’est pas affiché par défaut ici. Une fois que vous trouvez, sélectionnez-la, puis cliquez sur **sélectionnez** bas hello du Panneau de hello. 
    
    ![][20]
24. Sur hello **ajouter un accès à** panneau, il apparaît comme **1 utilisateur, les groupes 0**. Cliquez sur **OK** sur cette modification de hello tooconfirm panneau. 
    
    ![][21]

Vous avez maintenant terminé la configuration de AAD hello requis et que vous êtes hello de toocall ensemble toutes les API. 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication-manual/active-directory.png
[2]: ./media/mobile-engagement-api-authentication-manual/active-directory-details.png
[3]: ./media/mobile-engagement-api-authentication-manual/view-applications.png
[4]: ./media/mobile-engagement-api-authentication-manual/add-icon.png
[5]: ./media/mobile-engagement-api-authentication-manual/what-do-you-want-to-do.png
[6]: ./media/mobile-engagement-api-authentication-manual/tell-us-about-your-application.png
[7]: ./media/mobile-engagement-api-authentication-manual/app-properties.png
[8]: ./media/mobile-engagement-api-authentication-manual/aad-app.png
[9]: ./media/mobile-engagement-api-authentication-manual/configure-menu.png
[10]: ./media/mobile-engagement-api-authentication-manual/client-id.png
[11]: ./media/mobile-engagement-api-authentication-manual/client_secret.png
[12]: ./media/mobile-engagement-api-authentication-manual/keys.png
[13]: ./media/mobile-engagement-api-authentication-manual/view-endpoints.png
[14]: ./media/mobile-engagement-api-authentication-manual/app-endpoints.png
[15]: ./media/mobile-engagement-api-authentication-manual/resource-groups.png
[16]: ./media/mobile-engagement-api-authentication-manual/resource-groups-settings.png
[17]: ./media/mobile-engagement-api-authentication-manual/add-users.png
[18]: ./media/mobile-engagement-api-authentication-manual/add-role.png
[19]: ./media/mobile-engagement-api-authentication-manual/select-role.png
[20]: ./media/mobile-engagement-api-authentication-manual/add-user-select.png
[21]: ./media/mobile-engagement-api-authentication-manual/add-access-final.png



