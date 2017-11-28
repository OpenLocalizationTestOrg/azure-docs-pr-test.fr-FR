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
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a><span data-ttu-id="12aa7-103">Azure Mobile Engagement - Configuration manuelle de l’utilisation des API pour l’authentification</span><span class="sxs-lookup"><span data-stu-id="12aa7-103">Authenticate with Mobile Engagement REST APIs - manual setup</span></span>
<span data-ttu-id="12aa7-104">Il s’agit d’une documentation annexe trop[authentifier avec les API REST Mobile Engagement](mobile-engagement-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="12aa7-104">This is an appendix documentation too[Authenticate with Mobile Engagement REST APIs](mobile-engagement-api-authentication.md).</span></span> <span data-ttu-id="12aa7-105">Assurez-vous que vous les ayez lues premier contexte de hello tooget.</span><span class="sxs-lookup"><span data-stu-id="12aa7-105">Make sure you read it first tooget hello context.</span></span> <span data-ttu-id="12aa7-106">Cette section décrit une autre façon toodo hello d’installation unique pour le paramétrage de l’authentification pour à l’aide des API de REST Mobile Engagement hello hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="12aa7-106">This describes an alternate way toodo hello One-time setup for setting up your authentication for hello Mobile Engagement REST APIs using hello Azure Portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="12aa7-107">instructions Hello ci-dessous sont basées sur ce [guide Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md) et personnalisée pour ce qui est requis pour l’authentification pour les API d’Engagement Mobile.</span><span class="sxs-lookup"><span data-stu-id="12aa7-107">hello instructions below are based on this [Active Directory guide](../azure-resource-manager/resource-group-create-service-principal-portal.md) and customized for what is required for authentication for Mobile Engagement APIs.</span></span> <span data-ttu-id="12aa7-108">Par conséquent, consultez tooit si vous souhaitez que les étapes de hello toounderstand ci-dessous en détail.</span><span class="sxs-lookup"><span data-stu-id="12aa7-108">So refer tooit if you want toounderstand hello steps below in detail.</span></span> 
> 
> 

1. <span data-ttu-id="12aa7-109">Connexion tooyour compte Azure via hello [portail classic](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="12aa7-109">Login tooyour Azure Account through hello [classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="12aa7-110">Sélectionnez **Active Directory** hello volet de gauche.</span><span class="sxs-lookup"><span data-stu-id="12aa7-110">Select **Active Directory** from hello left pane.</span></span>
   
     ![sélectionner Active Directory][1]
3. <span data-ttu-id="12aa7-112">Choisissez hello **par défaut Active Directory** dans votre portail Azure.</span><span class="sxs-lookup"><span data-stu-id="12aa7-112">Choose hello **Default Active Directory** in your Azure portal.</span></span> 
   
     ![choisir l’annuaire][2]
   
   > [!IMPORTANT]
   > <span data-ttu-id="12aa7-114">Cette approche fonctionne uniquement lorsque vous travaillez dans la valeur par défaut de hello Active Directory de votre compte et ne fonctionnera pas si vous effectuez cette opération dans Active Directory que vous avez créés dans votre compte.</span><span class="sxs-lookup"><span data-stu-id="12aa7-114">This approach works only when you are working in hello default Active Directory of your account and will not work if you are doing this in an Active Directory that you have created in your account.</span></span> 
   > 
   > 
4. <span data-ttu-id="12aa7-115">applications de hello tooview dans votre annuaire, cliquez sur **Applications**.</span><span class="sxs-lookup"><span data-stu-id="12aa7-115">tooview hello applications in your directory, click on **Applications**.</span></span>
   
     ![afficher les applications][3]
5. <span data-ttu-id="12aa7-117">Cliquez sur **AJOUTER**.</span><span class="sxs-lookup"><span data-stu-id="12aa7-117">Click on **ADD**.</span></span> 
   
     ![ajouter l’application][4]
6. <span data-ttu-id="12aa7-119">Cliquez sur **Ajouter une application développée par mon organisation**</span><span class="sxs-lookup"><span data-stu-id="12aa7-119">Click on **Add an application my organization is developing**</span></span>
   
     ![nouvelle application][5]
7. <span data-ttu-id="12aa7-121">Entrez le nom de l’application hello et de type hello select de l’application en tant que **WEB APPLICATION et/ou API WEB** et cliquez sur le bouton suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="12aa7-121">Fill in name of hello application and select hello type of application as **WEB APPLICATION AND/OR WEB API** and click hello next button.</span></span>
   
     ![nommer l’application][6]
8. <span data-ttu-id="12aa7-123">Vous pouvez fournir des URL factices pour **l’URL DE CONNEXION** et **l’URI ID D’APPLICATION**.</span><span class="sxs-lookup"><span data-stu-id="12aa7-123">You can provide any dummy URLs for **SIGN-ON URL** and **APP ID URI**.</span></span> <span data-ttu-id="12aa7-124">Ils ne sont pas utilisés dans notre scénario et URL hello eux-mêmes ne sont pas validées.</span><span class="sxs-lookup"><span data-stu-id="12aa7-124">They are not used for our scenario and hello URLs themselves are not validated.</span></span>  
   
     ![propriétés de l’application][7]
9. <span data-ttu-id="12aa7-126">Extrémité hello de cela, vous aurez une application AAD avec nom hello fourni précédemment hello suivante.</span><span class="sxs-lookup"><span data-stu-id="12aa7-126">At hello end of this, you will have an AAD app with hello name you provided previously like hello following.</span></span> <span data-ttu-id="12aa7-127">Il s’agit de votre **AD\_APP\_NAME**. Prenez-en note.</span><span class="sxs-lookup"><span data-stu-id="12aa7-127">This is your **AD\_APP\_NAME** and make a note of it.</span></span>  
   
     ![nom de l’application][8]
10. <span data-ttu-id="12aa7-129">Cliquez sur le nom de l’application hello et cliquez sur **configurer**.</span><span class="sxs-lookup"><span data-stu-id="12aa7-129">Click on hello app name and click on **Configure**.</span></span>
    
      ![configurer l’application][9]
11. <span data-ttu-id="12aa7-131">Prenez note de hello ID de CLIENT qui sera utilisé comme **CLIENT\_ID** pour votre API appelle.</span><span class="sxs-lookup"><span data-stu-id="12aa7-131">Make a note of hello CLIENT ID that will be used as **CLIENT\_ID** for your API calls.</span></span> 
    
     ![configurer l’application][10]
12. <span data-ttu-id="12aa7-133">Faites défiler vers le bas toohello **clés** section et ajouter une clé avec une durée de 2 ans (expiration), de préférence, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="12aa7-133">Scroll down toohello **Keys** section and add a key with preferably 2 years (expiry) duration and click **Save**.</span></span> 
    
     ![configurer l’application][11]
13. <span data-ttu-id="12aa7-135">Copier immédiatement la valeur hello qui est affichée pour la clé de hello lorsqu’il ne s’affiche désormais et n’est pas stockée afin de s’afficheront pas jamais.</span><span class="sxs-lookup"><span data-stu-id="12aa7-135">Immediately copy hello value which is shown for hello key as it is only shown now and is not stored so will not be displayed ever again.</span></span> <span data-ttu-id="12aa7-136">Si vous le perdez puis avoir toogenerate une nouvelle clé.</span><span class="sxs-lookup"><span data-stu-id="12aa7-136">If you lose it then you will have toogenerate a new key.</span></span> <span data-ttu-id="12aa7-137">Il s’agit de hello **CLIENT_SECRET** pour votre API appelle.</span><span class="sxs-lookup"><span data-stu-id="12aa7-137">This will be hello **CLIENT_SECRET** for your API calls.</span></span> 
    
     ![configurer l’application][12]
    
    > [!IMPORTANT]
    > <span data-ttu-id="12aa7-139">Cette clé expire à fin hello de durée de hello que vous avez spécifié dans ce toorenew vraiment rendre il hello moment venu sinon l’authentification d’API ne fonctionnera plus.</span><span class="sxs-lookup"><span data-stu-id="12aa7-139">This key will expire at hello end of hello duration that you specified so make sure toorenew it when hello time comes otherwise your API authentication will not work anymore.</span></span> <span data-ttu-id="12aa7-140">Vous pouvez également supprimer et recréer cette clé si vous pensez qu’elle a été compromise.</span><span class="sxs-lookup"><span data-stu-id="12aa7-140">You can also delete and recreate this key if you think that it has been compromised.</span></span>
    > 
    > 
14. <span data-ttu-id="12aa7-141">Cliquez sur **points de terminaison** bouton maintenant qui s’ouvre hello **points de terminaison** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="12aa7-141">Click on **VIEW ENDPOINTS** button now which will open up hello **App Endpoints** dialog box.</span></span> 
    
    ![][13]
15. <span data-ttu-id="12aa7-142">À partir de la boîte de dialogue points de terminaison hello, copiez hello **OAUTH 2.0 TOKEN ENDPOINT**.</span><span class="sxs-lookup"><span data-stu-id="12aa7-142">From hello App Endpoints dialog box, copy hello **OAUTH 2.0 TOKEN ENDPOINT**.</span></span> 
    
    ![][14]
16. <span data-ttu-id="12aa7-143">Ce point de terminaison sera Bonjour suivant formulaire où hello GUID dans l’URL de hello est votre **TENANT_ID** par conséquent, prenez note de celui-ci :</span><span class="sxs-lookup"><span data-stu-id="12aa7-143">This endpoint will be in hello following form where hello GUID in hello URL is your **TENANT_ID** so make a note of it:</span></span> 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. <span data-ttu-id="12aa7-144">Maintenant, nous continuerons tooconfigure les autorisations de hello sur cette application.</span><span class="sxs-lookup"><span data-stu-id="12aa7-144">Now we will proceed tooconfigure hello permissions on this app.</span></span> <span data-ttu-id="12aa7-145">Pour cela, vous aurez tooopen des hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="12aa7-145">For this you will have tooopen up hello [Azure portal](https://portal.azure.com).</span></span> 
18. <span data-ttu-id="12aa7-146">Cliquez sur **groupes de ressources** et recherche hello **Mobile Engagement** groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="12aa7-146">Click on **Resource Groups** and find hello **Mobile Engagement** resource group.</span></span>  
    
    ![][15]
19. <span data-ttu-id="12aa7-147">Cliquez sur hello **Mobile Engagement** ressource de groupe et accédez toohello **paramètres** panneau ici.</span><span class="sxs-lookup"><span data-stu-id="12aa7-147">Click hello **Mobile Engagement** resource group and navigate toohello **Settings** blade here.</span></span> 
    
    ![][16]
20. <span data-ttu-id="12aa7-148">Cliquez sur **utilisateurs** dans hello panneau des paramètres, puis cliquez sur **ajouter** tooadd un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="12aa7-148">Click on **Users** in hello Settings blade and then click on **Add** tooadd a user.</span></span> 
    
    ![][17]
21. <span data-ttu-id="12aa7-149">Cliquez sur **Sélectionner un rôle**</span><span class="sxs-lookup"><span data-stu-id="12aa7-149">Click on **Select a role**</span></span>
    
    ![][18]
22. <span data-ttu-id="12aa7-150">Cliquez sur **Propriétaire**</span><span class="sxs-lookup"><span data-stu-id="12aa7-150">Click on **Owner**</span></span>
    
    ![][19]
23. <span data-ttu-id="12aa7-151">Recherchez le nom hello de votre application **AD\_application\_nom** dans la zone de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="12aa7-151">Search for hello name of your application **AD\_APP\_NAME** in hello Search box.</span></span> <span data-ttu-id="12aa7-152">Il n’est pas affiché par défaut ici.</span><span class="sxs-lookup"><span data-stu-id="12aa7-152">You will not see this by default here.</span></span> <span data-ttu-id="12aa7-153">Une fois que vous trouvez, sélectionnez-la, puis cliquez sur **sélectionnez** bas hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="12aa7-153">Once you find it, select it and click on **Select** at hello bottom of hello blade.</span></span> 
    
    ![][20]
24. <span data-ttu-id="12aa7-154">Sur hello **ajouter un accès à** panneau, il apparaît comme **1 utilisateur, les groupes 0**.</span><span class="sxs-lookup"><span data-stu-id="12aa7-154">On hello **Add Access** blade, it will show up as **1 user, 0 groups**.</span></span> <span data-ttu-id="12aa7-155">Cliquez sur **OK** sur cette modification de hello tooconfirm panneau.</span><span class="sxs-lookup"><span data-stu-id="12aa7-155">Click **OK** on this blade tooconfirm hello change.</span></span> 
    
    ![][21]

<span data-ttu-id="12aa7-156">Vous avez maintenant terminé la configuration de AAD hello requis et que vous êtes hello de toocall ensemble toutes les API.</span><span class="sxs-lookup"><span data-stu-id="12aa7-156">You have now completed hello required AAD configuration and you are all set toocall hello APIs.</span></span> 

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



