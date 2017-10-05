---
title: "Prise en main d’Azure Active Directory Identity Protection et de Microsoft Graph | Microsoft Docs"
description: "Fournit une introduction à l’interrogation de Microsoft Graph pour obtenir une liste d’événements à risque et des informations associées à partir d’Azure Active Directory."
services: active-directory
keywords: "azure active directory identity protection, événement à risque, vulnérabilité, stratégie de sécurité, Microsoft Graph"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 9b01ff86da6a1fd4a439a6ba59ea15ed6480cdad
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a><span data-ttu-id="fddeb-104">Prise en main d’Azure Active Directory Identity Protection et de Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="fddeb-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>
<span data-ttu-id="fddeb-105">Microsoft Graph est le point de terminaison d’API unifiée de Microsoft et accueille également les API [d’Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="fddeb-105">Microsoft Graph is the Microsoft unified API endpoint and the home of [Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs.</span></span> <span data-ttu-id="fddeb-106">La première API, **identityRiskEvents**, vous permet d’interroger Microsoft Graph pour obtenir une liste [d’événements à risque](active-directory-identityprotection-risk-events-types.md) et des informations associées.</span><span class="sxs-lookup"><span data-stu-id="fddeb-106">The first API, **identityRiskEvents**, allows you to query Microsoft Graph for a list of [risk events](active-directory-identityprotection-risk-events-types.md) and associated information.</span></span> <span data-ttu-id="fddeb-107">Cet article vous permet de vous familiariser avec l’interrogation de cette API.</span><span class="sxs-lookup"><span data-stu-id="fddeb-107">This article gets you started querying this API.</span></span> <span data-ttu-id="fddeb-108">Pour des informations détaillées ainsi qu’un accès à l’explorateur de Graph, consultez le [site de Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="fddeb-108">For an in-depth introduction, full documentation, and access to the Graph Explorer, see the [Microsoft Graph site](https://graph.microsoft.io/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fddeb-109">Microsoft recommande de gérer Azure AD à l’aide du [Centre d’administration Azure AD](https://aad.portal.azure.com) dans le portail Azure au lieu d’utiliser le portail Azure classique référencé dans cet article.</span><span class="sxs-lookup"><span data-stu-id="fddeb-109">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="fddeb-110">L’accès aux données d’Identity Protection par le biais de Microsoft Graph se fait en trois étapes :</span><span class="sxs-lookup"><span data-stu-id="fddeb-110">There are three steps to accessing Identity Protection data through Microsoft Graph:</span></span>

1. <span data-ttu-id="fddeb-111">Ajouter une application avec une clé secrète client.</span><span class="sxs-lookup"><span data-stu-id="fddeb-111">Add an application with a client secret.</span></span> 
2. <span data-ttu-id="fddeb-112">Utilisez cette clé secrète et d’autres éléments d’information pour vous authentifier auprès de Microsoft Graph ; ce dernier vous transmettra un jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="fddeb-112">Use this secret and a few other pieces of information to authenticate to Microsoft Graph, where you receive an authentication token.</span></span> 
3. <span data-ttu-id="fddeb-113">Utilisez ce jeton pour faire des demandes auprès du point de terminaison d’API et récupérer des données d’Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="fddeb-113">Use this token to make requests to the API endpoint and get Identity Protection data back.</span></span>

<span data-ttu-id="fddeb-114">Avant de commencer, vous aurez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fddeb-114">Before you get started, you’ll need:</span></span>

* <span data-ttu-id="fddeb-115">Des privilèges d’administrateur pour créer l’application dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="fddeb-115">Administrator privileges to create the application in Azure AD</span></span>
* <span data-ttu-id="fddeb-116">Le nom de domaine de votre client, par exemple contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="fddeb-116">The name of your tenant's domain (for example, contoso.onmicrosoft.com)</span></span>

## <a name="add-an-application-with-a-client-secret"></a><span data-ttu-id="fddeb-117">Ajouter une application avec une clé secrète client</span><span class="sxs-lookup"><span data-stu-id="fddeb-117">Add an application with a client secret</span></span>
1. <span data-ttu-id="fddeb-118">[Connectez-vous](https://manage.windowsazure.com) en tant qu’administrateur sur le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="fddeb-118">[Sign in](https://manage.windowsazure.com) to your Azure classic portal as an administrator.</span></span> 
2. <span data-ttu-id="fddeb-119">Dans le volet de navigation gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fddeb-119">On on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. <span data-ttu-id="fddeb-121">Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.</span><span class="sxs-lookup"><span data-stu-id="fddeb-121">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
4. <span data-ttu-id="fddeb-122">Dans le menu supérieur, cliquez sur **Applications**.</span><span class="sxs-lookup"><span data-stu-id="fddeb-122">In the menu on the top, click **Applications**.</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. <span data-ttu-id="fddeb-124">Cliquez sur **Ajouter** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="fddeb-124">Click **Add** at the bottom of the page.</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. <span data-ttu-id="fddeb-126">Sur la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application développée par mon organisation**.</span><span class="sxs-lookup"><span data-stu-id="fddeb-126">On the **What do you want to do** dialog, click **Add an application my organization is developing**.</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. <span data-ttu-id="fddeb-128">Dans la boîte de dialogue **Dites-nous en plus sur cet utilisateur** , procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="fddeb-128">On the **Tell us about your application** dialog, perform the following steps:</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    <span data-ttu-id="fddeb-130">a.</span><span class="sxs-lookup"><span data-stu-id="fddeb-130">a.</span></span> <span data-ttu-id="fddeb-131">Dans la zone de texte **Nom** , tapez un nom pour votre application (par exemple : Application d’API d’événement à risque AADIP).</span><span class="sxs-lookup"><span data-stu-id="fddeb-131">In the **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span></span>
   
    <span data-ttu-id="fddeb-132">b.</span><span class="sxs-lookup"><span data-stu-id="fddeb-132">b.</span></span> <span data-ttu-id="fddeb-133">Pour **Type**, sélectionnez **Application web et/ou API web**.</span><span class="sxs-lookup"><span data-stu-id="fddeb-133">As **Type**, select **Web Application And / Or Web API**.</span></span>
   
    <span data-ttu-id="fddeb-134">c.</span><span class="sxs-lookup"><span data-stu-id="fddeb-134">c.</span></span> <span data-ttu-id="fddeb-135">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="fddeb-135">Click **Next**.</span></span>
8. <span data-ttu-id="fddeb-136">Dans la boîte de dialogue **Propriétés de l’application** , effectuez les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="fddeb-136">On the **App properties** dialog, perform the following steps:</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    <span data-ttu-id="fddeb-138">a.</span><span class="sxs-lookup"><span data-stu-id="fddeb-138">a.</span></span> <span data-ttu-id="fddeb-139">Dans la zone de texte **URL d’authentification**, tapez `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="fddeb-139">In the **Sign-On URL** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="fddeb-140">b.</span><span class="sxs-lookup"><span data-stu-id="fddeb-140">b.</span></span> <span data-ttu-id="fddeb-141">Dans la zone de texte **URL ID d’application**, tapez `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="fddeb-141">In the **App ID URI** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="fddeb-142">c.</span><span class="sxs-lookup"><span data-stu-id="fddeb-142">c.</span></span> <span data-ttu-id="fddeb-143">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="fddeb-143">Click **Complete**.</span></span>

<span data-ttu-id="fddeb-144">Vous pouvez à présent configurer votre application.</span><span class="sxs-lookup"><span data-stu-id="fddeb-144">Your can now configure your application.</span></span>

![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-to-use-the-api"></a><span data-ttu-id="fddeb-146">Autorisation d'utilisation de l'API pour votre application</span><span class="sxs-lookup"><span data-stu-id="fddeb-146">Grant your application permission to use the API</span></span>
1. <span data-ttu-id="fddeb-147">Dans la page de votre application, dans le menu du haut, cliquez sur **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="fddeb-147">On your application's page, in the menu on the top, click **Configure**.</span></span> 
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. <span data-ttu-id="fddeb-149">Dans la section **Autorisations pour d’autres applications**, cliquez sur **Ajouter une application**.</span><span class="sxs-lookup"><span data-stu-id="fddeb-149">In the **permissions to other applications** section, click **Add application**.</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. <span data-ttu-id="fddeb-151">Dans la boîte de dialogue **Autorisations pour d’autres applications** , effectuez les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="fddeb-151">On the **permissions to other applications** dialog, perform the following steps:</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    <span data-ttu-id="fddeb-153">a.</span><span class="sxs-lookup"><span data-stu-id="fddeb-153">a.</span></span> <span data-ttu-id="fddeb-154">Sélectionnez **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="fddeb-154">Select **Microsoft Graph**.</span></span>
   
    <span data-ttu-id="fddeb-155">b.</span><span class="sxs-lookup"><span data-stu-id="fddeb-155">b.</span></span> <span data-ttu-id="fddeb-156">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="fddeb-156">Click **Complete**.</span></span>
4. <span data-ttu-id="fddeb-157">Cliquez sur **Autorisations d’application : 0**, puis sélectionnez **Read all identity risk event information** (Lire toutes les informations sur les événements à risque concernant l’identité).</span><span class="sxs-lookup"><span data-stu-id="fddeb-157">Click **Application Permissions: 0**, and then select **Read all identity risk event information**.</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. <span data-ttu-id="fddeb-159">Cliquez sur **Enregistrer** au bas de la page.</span><span class="sxs-lookup"><span data-stu-id="fddeb-159">Click **Save** at the bottom of the page.</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a><span data-ttu-id="fddeb-161">Obtenir une clé d’accès</span><span class="sxs-lookup"><span data-stu-id="fddeb-161">Get an access key</span></span>
1. <span data-ttu-id="fddeb-162">Sur la page de votre application, dans la section **Clés** , définissez la durée sur 1 an.</span><span class="sxs-lookup"><span data-stu-id="fddeb-162">On your application's page, in the **keys** section, select 1 year as duration.</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. <span data-ttu-id="fddeb-164">Cliquez sur **Enregistrer** au bas de la page.</span><span class="sxs-lookup"><span data-stu-id="fddeb-164">Click **Save** at the bottom of the page.</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. <span data-ttu-id="fddeb-166">Dans la section Clés, copiez la valeur de la clé qui vient d’être créée, puis collez-la dans un emplacement sûr.</span><span class="sxs-lookup"><span data-stu-id="fddeb-166">in the keys section, copy the value of your newly created key, and then paste it into a safe location.</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > <span data-ttu-id="fddeb-168">Si vous perdez cette clé, vous devrez revenir à cette section et créer une nouvelle clé.</span><span class="sxs-lookup"><span data-stu-id="fddeb-168">If you lose this key, you will have to return to this section and create a new key.</span></span> <span data-ttu-id="fddeb-169">Gardez cette clé secrète : toute personne la possédant peut accéder à vos données.</span><span class="sxs-lookup"><span data-stu-id="fddeb-169">Keep this key a secret: anyone who has it can access your data.</span></span>
   > 
   > 
4. <span data-ttu-id="fddeb-170">Dans la section **Propriétés**, copiez **l’ID Client**, puis collez-le dans un emplacement sûr.</span><span class="sxs-lookup"><span data-stu-id="fddeb-170">In the **properties** section, copy the **Client ID**, and then paste it into a safe location.</span></span> 

## <a name="authenticate-to-microsoft-graph-and-query-the-identity-risk-events-api"></a><span data-ttu-id="fddeb-171">Authentifiez-vous auprès de Microsoft Graph et interrogez l’API d’événements à risque concernant l’identité</span><span class="sxs-lookup"><span data-stu-id="fddeb-171">Authenticate to Microsoft Graph and query the Identity Risk Events API</span></span>
<span data-ttu-id="fddeb-172">À ce stade, vous devez avoir :</span><span class="sxs-lookup"><span data-stu-id="fddeb-172">At this point, you should have:</span></span>

* <span data-ttu-id="fddeb-173">l’ID client copié précédemment ;</span><span class="sxs-lookup"><span data-stu-id="fddeb-173">The client ID you copied above</span></span>
* <span data-ttu-id="fddeb-174">la clé copiée précédemment ;</span><span class="sxs-lookup"><span data-stu-id="fddeb-174">The key you copied above</span></span>
* <span data-ttu-id="fddeb-175">le nom de domaine de votre client ;</span><span class="sxs-lookup"><span data-stu-id="fddeb-175">The name of your tenant's domain</span></span>

<span data-ttu-id="fddeb-176">Pour l’authentification, envoyez une demande POST à `https://login.microsoft.com` , avec les paramètres suivants dans le corps :</span><span class="sxs-lookup"><span data-stu-id="fddeb-176">To authenticate, send a post request to `https://login.microsoft.com` with the following parameters in the body:</span></span>

* <span data-ttu-id="fddeb-177">grant_type : « **client_informationsidentification** »</span><span class="sxs-lookup"><span data-stu-id="fddeb-177">grant_type: “**client_credentials**”</span></span>
* <span data-ttu-id="fddeb-178">resource: “**https://graph.microsoft.com**”</span><span class="sxs-lookup"><span data-stu-id="fddeb-178">resource: “**https://graph.microsoft.com**”</span></span>
* <span data-ttu-id="fddeb-179">client_id : <your client ID></span><span class="sxs-lookup"><span data-stu-id="fddeb-179">client_id: <your client ID></span></span>
* <span data-ttu-id="fddeb-180">client_secret : <your key></span><span class="sxs-lookup"><span data-stu-id="fddeb-180">client_secret: <your key></span></span>

> [!NOTE]
> <span data-ttu-id="fddeb-181">Vous devez fournir des valeurs pour les paramètres **client_id** et **client_secret**.</span><span class="sxs-lookup"><span data-stu-id="fddeb-181">You need to provide values for the **client_id** and the **client_secret** parameter.</span></span>
> 
> 

<span data-ttu-id="fddeb-182">Si l’opération réussit, elle retourne un jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="fddeb-182">If successful, this returns an authentication token.</span></span>  
<span data-ttu-id="fddeb-183">Pour appeler l’API, créez un en-tête avec le paramètre suivant :</span><span class="sxs-lookup"><span data-stu-id="fddeb-183">To call the API, create a header with the following parameter:</span></span>

    `Authorization`=”<token_type> <access_token>"


<span data-ttu-id="fddeb-184">Lors de l’authentification, le jeton retourné contient le type de jeton ainsi que le jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="fddeb-184">When authenticating, you can find the token type and access token in the returned token.</span></span>

<span data-ttu-id="fddeb-185">Envoyez cet en-tête en tant que requête à l’URL de l’API suivante : `https://graph.microsoft.com/beta/identityRiskEvents`</span><span class="sxs-lookup"><span data-stu-id="fddeb-185">Send this header as a request to the following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span></span>

<span data-ttu-id="fddeb-186">La réponse, en cas de réussite, consiste en une collection d’événements à risque concernant l’identité ainsi que les données associées au format JSON OData, qui peuvent être analysés et gérés selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="fddeb-186">The response, if successful, is a collection of identity risk events and associated data in the OData JSON format, which can be parsed and handled as see fit.</span></span>

<span data-ttu-id="fddeb-187">Voici un exemple de code pour l’authentification et l’appel de l’API par le biais de Powershell.</span><span class="sxs-lookup"><span data-stu-id="fddeb-187">Here’s sample code for authenticating and calling the API using Powershell.</span></span>  
<span data-ttu-id="fddeb-188">Il suffit d’ajouter l’ID client, la clé ainsi que le domaine client.</span><span class="sxs-lookup"><span data-stu-id="fddeb-188">Just add your client ID, key, and tenant domain.</span></span>

    $ClientID       = "<your client ID here>"        # Should be a ~36 hex character string; insert your info here
    $ClientSecret   = "<your client secret here>"    # Should be a ~44 character string; insert your info here
    $tenantdomain   = "<your tenant domain here>"    # For example, contoso.onmicrosoft.com

    $loginURL       = "https://login.microsoft.com"
    $resource       = "https://graph.microsoft.com"

    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    Write-Output $oauth

    if ($oauth.access_token -ne $null) {
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

        $url = "https://graph.microsoft.com/beta/identityRiskEvents"
        Write-Output $url

        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)

        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output $event
        }

    } else {
        Write-Host "ERROR: No Access Token"
    } 


## <a name="next-steps"></a><span data-ttu-id="fddeb-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fddeb-189">Next steps</span></span>
<span data-ttu-id="fddeb-190">Félicitations, vous venez de créer votre premier appel à Microsoft Graph !</span><span class="sxs-lookup"><span data-stu-id="fddeb-190">Congratulations, you just made your first call to Microsoft Graph!</span></span>  
<span data-ttu-id="fddeb-191">Vous pouvez à présent interroger les événements à risque concernant l’identité et utiliser les données comme bon vous semble.</span><span class="sxs-lookup"><span data-stu-id="fddeb-191">Now you can query identity risk events and use the data however you see fit.</span></span>

<span data-ttu-id="fddeb-192">Pour en savoir plus sur Microsoft Graph et comment créer des applications à l’aide de l’API Graph, consultez la [documentation](https://graph.microsoft.io/docs) afférente et bien plus sur le [site de Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="fddeb-192">To learn more about Microsoft Graph and how to build applications using the Graph API, check out the [documentation](https://graph.microsoft.io/docs) and much more on the [Microsoft Graph site](https://graph.microsoft.io/).</span></span> <span data-ttu-id="fddeb-193">Assurez-vous également de marquer la page [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) (API Azure AD Identity Protection) à l’aide d’un signet ; cette dernière répertorie toutes les API d’Identity Protection disponibles dans Graph.</span><span class="sxs-lookup"><span data-stu-id="fddeb-193">Also, make sure to bookmark the [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of the Identity Protection APIs available in Graph.</span></span> <span data-ttu-id="fddeb-194">Sur cette page, vous pourrez consulter l’ensemble des nouvelles façons de travailler avec Identity Protection via API au fur et à mesure que nous les ajoutons.</span><span class="sxs-lookup"><span data-stu-id="fddeb-194">As we add new ways to work with Identity Protection via API, you’ll see them on that page.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fddeb-195">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="fddeb-195">Additional resources</span></span>
* [<span data-ttu-id="fddeb-196">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="fddeb-196">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
* [<span data-ttu-id="fddeb-197">Types d’événements à risque détectés par Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="fddeb-197">Types of risk events detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-risk-events-types.md)
* [<span data-ttu-id="fddeb-198">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="fddeb-198">Microsoft Graph</span></span>](https://graph.microsoft.io/)
* [<span data-ttu-id="fddeb-199">Overview of Microsoft Graph (Vue d’ensemble de Microsoft Graph)</span><span class="sxs-lookup"><span data-stu-id="fddeb-199">Overview of Microsoft Graph</span></span>](https://graph.microsoft.io/docs)
* [<span data-ttu-id="fddeb-200">Azure AD Identity Protection Service Root (Racine de service d’Azure AD Identity Protection)</span><span class="sxs-lookup"><span data-stu-id="fddeb-200">Azure AD Identity Protection Service Root</span></span>](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

