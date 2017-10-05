---
title: "Azure Mobile Engagement - Configuration manuelle de l’utilisation des API pour l’authentification"
description: "Décrit comment configurer manuellement l’authentification pour les API REST Mobile Engagement"
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
ms.openlocfilehash: 9d6132e1a01be489b8e8e28a0219cf8a0b50b318
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a><span data-ttu-id="e07e9-103">Azure Mobile Engagement - Configuration manuelle de l’utilisation des API pour l’authentification</span><span class="sxs-lookup"><span data-stu-id="e07e9-103">Authenticate with Mobile Engagement REST APIs - manual setup</span></span>
<span data-ttu-id="e07e9-104">Ce document est une annexe de l’article [Azure Mobile Engagement - Utilisation des API pour l’authentification](mobile-engagement-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e07e9-104">This is an appendix documentation to [Authenticate with Mobile Engagement REST APIs](mobile-engagement-api-authentication.md).</span></span> <span data-ttu-id="e07e9-105">Veillez à le lire en premier pour comprendre le contexte.</span><span class="sxs-lookup"><span data-stu-id="e07e9-105">Make sure you read it first to get the context.</span></span> <span data-ttu-id="e07e9-106">Cette annexe décrit une autre méthode d’installation unique afin de configurer l’authentification pour les API REST Mobile Engagement à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e07e9-106">This describes an alternate way to do the One-time setup for setting up your authentication for the Mobile Engagement REST APIs using the Azure Portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="e07e9-107">Les instructions ci-dessous sont fondées sur ce [guide Active Directory](../azure-resource-manager/resource-group-create-service-principal-portal.md) et personnalisées en fonction des besoins propres à l’authentification pour les API Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="e07e9-107">The instructions below are based on this [Active Directory guide](../azure-resource-manager/resource-group-create-service-principal-portal.md) and customized for what is required for authentication for Mobile Engagement APIs.</span></span> <span data-ttu-id="e07e9-108">Par conséquent, consultez ce guide pour bien comprendre les étapes décrites en détail ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e07e9-108">So refer to it if you want to understand the steps below in detail.</span></span> 
> 
> 

1. <span data-ttu-id="e07e9-109">Connectez-vous à votre compte Azure via le [portail classique](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="e07e9-109">Login to your Azure Account through the [classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="e07e9-110">Sélectionnez **Active Directory** dans le volet gauche.</span><span class="sxs-lookup"><span data-stu-id="e07e9-110">Select **Active Directory** from the left pane.</span></span>
   
     ![sélectionner Active Directory][1]
3. <span data-ttu-id="e07e9-112">Choisissez le **répertoire actif par défaut** dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e07e9-112">Choose the **Default Active Directory** in your Azure portal.</span></span> 
   
     ![choisir l’annuaire][2]
   
   > [!IMPORTANT]
   > <span data-ttu-id="e07e9-114">Cette approche fonctionne uniquement quand vous travaillez dans le répertoire actif par défaut de votre compte et pas si vous l’utilisez dans un répertoire actif que vous avez créé pour votre compte.</span><span class="sxs-lookup"><span data-stu-id="e07e9-114">This approach works only when you are working in the default Active Directory of your account and will not work if you are doing this in an Active Directory that you have created in your account.</span></span> 
   > 
   > 
4. <span data-ttu-id="e07e9-115">Pour afficher les applications dans votre annuaire, cliquez sur **Applications**.</span><span class="sxs-lookup"><span data-stu-id="e07e9-115">To view the applications in your directory, click on **Applications**.</span></span>
   
     ![afficher les applications][3]
5. <span data-ttu-id="e07e9-117">Cliquez sur **AJOUTER**.</span><span class="sxs-lookup"><span data-stu-id="e07e9-117">Click on **ADD**.</span></span> 
   
     ![ajouter l’application][4]
6. <span data-ttu-id="e07e9-119">Cliquez sur **Ajouter une application développée par mon organisation**</span><span class="sxs-lookup"><span data-stu-id="e07e9-119">Click on **Add an application my organization is developing**</span></span>
   
     ![nouvelle application][5]
7. <span data-ttu-id="e07e9-121">Renseignez le nom de l’application et sélectionnez le type d’application **APPLICATION WEB ET/OU API WEB** , puis cliquez sur le bouton Suivant.</span><span class="sxs-lookup"><span data-stu-id="e07e9-121">Fill in name of the application and select the type of application as **WEB APPLICATION AND/OR WEB API** and click the next button.</span></span>
   
     ![nommer l’application][6]
8. <span data-ttu-id="e07e9-123">Vous pouvez fournir des URL factices pour **l’URL DE CONNEXION** et **l’URI ID D’APPLICATION**.</span><span class="sxs-lookup"><span data-stu-id="e07e9-123">You can provide any dummy URLs for **SIGN-ON URL** and **APP ID URI**.</span></span> <span data-ttu-id="e07e9-124">Ces URL ne sont pas utilisées pour notre scénario et les URL elles-mêmes ne sont pas validées.</span><span class="sxs-lookup"><span data-stu-id="e07e9-124">They are not used for our scenario and the URLs themselves are not validated.</span></span>  
   
     ![propriétés de l’application][7]
9. <span data-ttu-id="e07e9-126">À la fin de cette opération, vous disposerez d’une application AAD portant le nom que vous avez indiqué précédemment, comme suit.</span><span class="sxs-lookup"><span data-stu-id="e07e9-126">At the end of this, you will have an AAD app with the name you provided previously like the following.</span></span> <span data-ttu-id="e07e9-127">Il s’agit de votre **AD\_APP\_NAME**. Prenez-en note.</span><span class="sxs-lookup"><span data-stu-id="e07e9-127">This is your **AD\_APP\_NAME** and make a note of it.</span></span>  
   
     ![nom de l’application][8]
10. <span data-ttu-id="e07e9-129">Cliquez sur le nom de l’application, puis sur **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="e07e9-129">Click on the app name and click on **Configure**.</span></span>
    
      ![configurer l’application][9]
11. <span data-ttu-id="e07e9-131">Prenez note de l’ID CLIENT qui sera utilisé comme **CLIENT\_ID** pour les appels d’API.</span><span class="sxs-lookup"><span data-stu-id="e07e9-131">Make a note of the CLIENT ID that will be used as **CLIENT\_ID** for your API calls.</span></span> 
    
     ![configurer l’application][10]
12. <span data-ttu-id="e07e9-133">Faites défiler l’écran jusqu’à la section **Clés** et ajoutez une clé avec de préférence un délai d’expiration de deux ans, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e07e9-133">Scroll down to the **Keys** section and add a key with preferably 2 years (expiry) duration and click **Save**.</span></span> 
    
     ![configurer l’application][11]
13. <span data-ttu-id="e07e9-135">Copiez immédiatement la valeur affichée pour la clé, car elle est affichée uniquement maintenant et n’est pas stockée, ce qui signifie qu’elle ne s’affichera plus ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="e07e9-135">Immediately copy the value which is shown for the key as it is only shown now and is not stored so will not be displayed ever again.</span></span> <span data-ttu-id="e07e9-136">Si vous la perdez, vous devrez générer une nouvelle clé.</span><span class="sxs-lookup"><span data-stu-id="e07e9-136">If you lose it then you will have to generate a new key.</span></span> <span data-ttu-id="e07e9-137">Il s’agit de la **CLIENT_SECRET** pour les appels d’API.</span><span class="sxs-lookup"><span data-stu-id="e07e9-137">This will be the **CLIENT_SECRET** for your API calls.</span></span> 
    
     ![configurer l’application][12]
    
    > [!IMPORTANT]
    > <span data-ttu-id="e07e9-139">Cette clé expire à la fin de la durée que vous avez spécifiée. Vous devrez donc veiller à la renouveler le moment venu, sans quoi l’authentification de votre API ne fonctionnera plus.</span><span class="sxs-lookup"><span data-stu-id="e07e9-139">This key will expire at the end of the duration that you specified so make sure to renew it when the time comes otherwise your API authentication will not work anymore.</span></span> <span data-ttu-id="e07e9-140">Vous pouvez également supprimer et recréer cette clé si vous pensez qu’elle a été compromise.</span><span class="sxs-lookup"><span data-stu-id="e07e9-140">You can also delete and recreate this key if you think that it has been compromised.</span></span>
    > 
    > 
14. <span data-ttu-id="e07e9-141">Cliquez maintenant sur le bouton **VOIR LES POINTS DE TERMINAISON** pour ouvrir la boîte de dialogue **Ajouter des points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="e07e9-141">Click on **VIEW ENDPOINTS** button now which will open up the **App Endpoints** dialog box.</span></span> 
    
    ![][13]
15. <span data-ttu-id="e07e9-142">Dans la boîte de dialogue Points de terminaison d’app, copiez le **POINT DE TERMINAISON DE JETON OAUTH 2.0**.</span><span class="sxs-lookup"><span data-stu-id="e07e9-142">From the App Endpoints dialog box, copy the **OAUTH 2.0 TOKEN ENDPOINT**.</span></span> 
    
    ![][14]
16. <span data-ttu-id="e07e9-143">Ce point de terminaison se présente comme indiqué ci-dessous, le GUID de l’URL étant votre **TENANT_ID**. Prenez-en note :</span><span class="sxs-lookup"><span data-stu-id="e07e9-143">This endpoint will be in the following form where the GUID in the URL is your **TENANT_ID** so make a note of it:</span></span> 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. <span data-ttu-id="e07e9-144">Nous allons maintenant configurer les autorisations pour cette application.</span><span class="sxs-lookup"><span data-stu-id="e07e9-144">Now we will proceed to configure the permissions on this app.</span></span> <span data-ttu-id="e07e9-145">Pour cela, vous devez ouvrir le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e07e9-145">For this you will have to open up the [Azure portal](https://portal.azure.com).</span></span> 
18. <span data-ttu-id="e07e9-146">Cliquez sur **Groupes de ressources** et recherchez le groupe de ressources **Mobile Engagement**.</span><span class="sxs-lookup"><span data-stu-id="e07e9-146">Click on **Resource Groups** and find the **Mobile Engagement** resource group.</span></span>  
    
    ![][15]
19. <span data-ttu-id="e07e9-147">Cliquez sur le groupe de ressources **Mobile Engagement** et accédez au panneau **Paramètres** ici.</span><span class="sxs-lookup"><span data-stu-id="e07e9-147">Click the **Mobile Engagement** resource group and navigate to the **Settings** blade here.</span></span> 
    
    ![][16]
20. <span data-ttu-id="e07e9-148">Cliquez sur **Utilisateurs** dans le panneau Paramètres, puis cliquez sur **Ajouter** pour ajouter un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e07e9-148">Click on **Users** in the Settings blade and then click on **Add** to add a user.</span></span> 
    
    ![][17]
21. <span data-ttu-id="e07e9-149">Cliquez sur **Sélectionner un rôle**</span><span class="sxs-lookup"><span data-stu-id="e07e9-149">Click on **Select a role**</span></span>
    
    ![][18]
22. <span data-ttu-id="e07e9-150">Cliquez sur **Propriétaire**</span><span class="sxs-lookup"><span data-stu-id="e07e9-150">Click on **Owner**</span></span>
    
    ![][19]
23. <span data-ttu-id="e07e9-151">Recherchez le nom de votre application **AD\_APP\_NAME** dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="e07e9-151">Search for the name of your application **AD\_APP\_NAME** in the Search box.</span></span> <span data-ttu-id="e07e9-152">Il n’est pas affiché par défaut ici.</span><span class="sxs-lookup"><span data-stu-id="e07e9-152">You will not see this by default here.</span></span> <span data-ttu-id="e07e9-153">Une fois que vous l’avez trouvé, sélectionnez-le, puis cliquez sur **Sélectionner** en bas du panneau.</span><span class="sxs-lookup"><span data-stu-id="e07e9-153">Once you find it, select it and click on **Select** at the bottom of the blade.</span></span> 
    
    ![][20]
24. <span data-ttu-id="e07e9-154">Dans le panneau **Ajouter un accès**, il s’affiche sous la forme **1 utilisateur, 0 groupe**.</span><span class="sxs-lookup"><span data-stu-id="e07e9-154">On the **Add Access** blade, it will show up as **1 user, 0 groups**.</span></span> <span data-ttu-id="e07e9-155">Cliquez sur **OK** dans ce panneau pour confirmer la modification.</span><span class="sxs-lookup"><span data-stu-id="e07e9-155">Click **OK** on this blade to confirm the change.</span></span> 
    
    ![][21]

<span data-ttu-id="e07e9-156">Vous avez maintenant terminé la configuration AAD requise et êtes prêt à appeler les API.</span><span class="sxs-lookup"><span data-stu-id="e07e9-156">You have now completed the required AAD configuration and you are all set to call the APIs.</span></span> 

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



