---
title: "aaaGet a démarré avec la Protection d’identité Azure Active Directory et Microsoft Graph | Documents Microsoft"
description: "Fournit un tooquery présentation Microsoft Graph pour obtenir la liste des événements à risque et des informations associées à partir d’Azure Active Directory."
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
ms.openlocfilehash: 75b8b7629a0120d8101f6fde0d9163122503d276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a><span data-ttu-id="3c6ea-104">Prise en main d’Azure Active Directory Identity Protection et de Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="3c6ea-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>
<span data-ttu-id="3c6ea-105">Microsoft Graph est hello Microsoft unified point de terminaison API et hello domestique de [Azure Active Directory Identity Protection](active-directory-identityprotection.md) API.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-105">Microsoft Graph is hello Microsoft unified API endpoint and hello home of [Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs.</span></span> <span data-ttu-id="3c6ea-106">Hello première API, **identityRiskEvents**, vous permet de tooquery Microsoft Graph pour obtenir la liste de [risque d’événements](active-directory-identityprotection-risk-events-types.md) et des informations associées.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-106">hello first API, **identityRiskEvents**, allows you tooquery Microsoft Graph for a list of [risk events](active-directory-identityprotection-risk-events-types.md) and associated information.</span></span> <span data-ttu-id="3c6ea-107">Cet article vous permet de vous familiariser avec l’interrogation de cette API.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-107">This article gets you started querying this API.</span></span> <span data-ttu-id="3c6ea-108">Pour une présentation approfondie, la documentation complète et accès toohello Explorateur graphique, consultez hello [site de Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="3c6ea-108">For an in-depth introduction, full documentation, and access toohello Graph Explorer, see hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c6ea-109">Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="3c6ea-110">Il existe trois étapes tooaccessing identité Protection données via Microsoft Graph :</span><span class="sxs-lookup"><span data-stu-id="3c6ea-110">There are three steps tooaccessing Identity Protection data through Microsoft Graph:</span></span>

1. <span data-ttu-id="3c6ea-111">Ajouter une application avec une clé secrète client.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-111">Add an application with a client secret.</span></span> 
2. <span data-ttu-id="3c6ea-112">Utilisez ce mot de passe et quelques autres éléments d’informations tooauthenticate tooMicrosoft graphique, lorsque vous recevez un jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-112">Use this secret and a few other pieces of information tooauthenticate tooMicrosoft Graph, where you receive an authentication token.</span></span> 
3. <span data-ttu-id="3c6ea-113">Utiliser ce point de terminaison de jeton toomake demandes toohello API et obtenir des données de Protection de l’identité.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-113">Use this token toomake requests toohello API endpoint and get Identity Protection data back.</span></span>

<span data-ttu-id="3c6ea-114">Avant de commencer, vous aurez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3c6ea-114">Before you get started, you’ll need:</span></span>

* <span data-ttu-id="3c6ea-115">Application hello toocreate du privilèges administrateur dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c6ea-115">Administrator privileges toocreate hello application in Azure AD</span></span>
* <span data-ttu-id="3c6ea-116">nom Hello du domaine de votre locataire (par exemple, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="3c6ea-116">hello name of your tenant's domain (for example, contoso.onmicrosoft.com)</span></span>

## <a name="add-an-application-with-a-client-secret"></a><span data-ttu-id="3c6ea-117">Ajouter une application avec une clé secrète client</span><span class="sxs-lookup"><span data-stu-id="3c6ea-117">Add an application with a client secret</span></span>
1. <span data-ttu-id="3c6ea-118">[Connectez-vous](https://manage.windowsazure.com) tooyour portail classique Azure en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-118">[Sign in](https://manage.windowsazure.com) tooyour Azure classic portal as an administrator.</span></span> 
2. <span data-ttu-id="3c6ea-119">Sur dans le volet de navigation gauche hello, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-119">On on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. <span data-ttu-id="3c6ea-121">À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-121">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
4. <span data-ttu-id="3c6ea-122">Dans le menu hello haut de hello, cliquez sur **Applications**.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-122">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. <span data-ttu-id="3c6ea-124">Cliquez sur **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-124">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. <span data-ttu-id="3c6ea-126">Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application développée par mon organisation**.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-126">On hello **What do you want toodo** dialog, click **Add an application my organization is developing**.</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. <span data-ttu-id="3c6ea-128">Sur hello **Parlez-nous de votre application** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3c6ea-128">On hello **Tell us about your application** dialog, perform hello following steps:</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    <span data-ttu-id="3c6ea-130">a.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-130">a.</span></span> <span data-ttu-id="3c6ea-131">Bonjour **nom** zone de texte, tapez un nom pour votre application (par exemple : Application de l’API événement AADIP risque).</span><span class="sxs-lookup"><span data-stu-id="3c6ea-131">In hello **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span></span>
   
    <span data-ttu-id="3c6ea-132">b.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-132">b.</span></span> <span data-ttu-id="3c6ea-133">Pour **Type**, sélectionnez **Application web et/ou API web**.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-133">As **Type**, select **Web Application And / Or Web API**.</span></span>
   
    <span data-ttu-id="3c6ea-134">c.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-134">c.</span></span> <span data-ttu-id="3c6ea-135">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-135">Click **Next**.</span></span>
8. <span data-ttu-id="3c6ea-136">Sur hello **propriétés de l’application** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3c6ea-136">On hello **App properties** dialog, perform hello following steps:</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    <span data-ttu-id="3c6ea-138">a.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-138">a.</span></span> <span data-ttu-id="3c6ea-139">Bonjour **URL de connexion** zone de texte, type `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-139">In hello **Sign-On URL** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="3c6ea-140">b.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-140">b.</span></span> <span data-ttu-id="3c6ea-141">Bonjour **URI ID d’application** zone de texte, type `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-141">In hello **App ID URI** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="3c6ea-142">c.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-142">c.</span></span> <span data-ttu-id="3c6ea-143">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-143">Click **Complete**.</span></span>

<span data-ttu-id="3c6ea-144">Vous pouvez à présent configurer votre application.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-144">Your can now configure your application.</span></span>

![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="3c6ea-146">Accorder votre hello de toouse autorisation application API</span><span class="sxs-lookup"><span data-stu-id="3c6ea-146">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="3c6ea-147">Dans la page de votre application, dans le menu hello haut de hello, cliquez sur **configurer**.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-147">On your application's page, in hello menu on hello top, click **Configure**.</span></span> 
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. <span data-ttu-id="3c6ea-149">Bonjour **autorisations tooother applications** , cliquez sur **ajouter application**.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-149">In hello **permissions tooother applications** section, click **Add application**.</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. <span data-ttu-id="3c6ea-151">Sur hello **autorisations tooother applications** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3c6ea-151">On hello **permissions tooother applications** dialog, perform hello following steps:</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    <span data-ttu-id="3c6ea-153">a.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-153">a.</span></span> <span data-ttu-id="3c6ea-154">Sélectionnez **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-154">Select **Microsoft Graph**.</span></span>
   
    <span data-ttu-id="3c6ea-155">b.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-155">b.</span></span> <span data-ttu-id="3c6ea-156">Cliquez sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-156">Click **Complete**.</span></span>
4. <span data-ttu-id="3c6ea-157">Cliquez sur **Autorisations d’application : 0**, puis sélectionnez **Read all identity risk event information** (Lire toutes les informations sur les événements à risque concernant l’identité).</span><span class="sxs-lookup"><span data-stu-id="3c6ea-157">Click **Application Permissions: 0**, and then select **Read all identity risk event information**.</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. <span data-ttu-id="3c6ea-159">Cliquez sur **enregistrer** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-159">Click **Save** at hello bottom of hello page.</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a><span data-ttu-id="3c6ea-161">Obtenir une clé d’accès</span><span class="sxs-lookup"><span data-stu-id="3c6ea-161">Get an access key</span></span>
1. <span data-ttu-id="3c6ea-162">Sur la page de votre application, Bonjour **clés** , sélectionnez 1 an en tant que la durée.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-162">On your application's page, in hello **keys** section, select 1 year as duration.</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. <span data-ttu-id="3c6ea-164">Cliquez sur **enregistrer** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-164">Click **Save** at hello bottom of hello page.</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. <span data-ttu-id="3c6ea-166">dans la section « clés » hello, copier la valeur hello de votre clé nouvellement créée, puis collez-le dans un emplacement sûr.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-166">in hello keys section, copy hello value of your newly created key, and then paste it into a safe location.</span></span>
   
    ![Création d’une application](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > <span data-ttu-id="3c6ea-168">Si vous perdez cette clé, vous avez tooreturn toothis section et créer une nouvelle clé.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-168">If you lose this key, you will have tooreturn toothis section and create a new key.</span></span> <span data-ttu-id="3c6ea-169">Gardez cette clé secrète : toute personne la possédant peut accéder à vos données.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-169">Keep this key a secret: anyone who has it can access your data.</span></span>
   > 
   > 
4. <span data-ttu-id="3c6ea-170">Bonjour **propriétés** section, hello de copie **ID Client**, puis collez-la dans un emplacement sûr.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-170">In hello **properties** section, copy hello **Client ID**, and then paste it into a safe location.</span></span> 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a><span data-ttu-id="3c6ea-171">Authentifier tooMicrosoft graphique et hello de requête API d’événements risque identité</span><span class="sxs-lookup"><span data-stu-id="3c6ea-171">Authenticate tooMicrosoft Graph and query hello Identity Risk Events API</span></span>
<span data-ttu-id="3c6ea-172">À ce stade, vous devez avoir :</span><span class="sxs-lookup"><span data-stu-id="3c6ea-172">At this point, you should have:</span></span>

* <span data-ttu-id="3c6ea-173">ID de client Hello vous avez copié ci-dessus</span><span class="sxs-lookup"><span data-stu-id="3c6ea-173">hello client ID you copied above</span></span>
* <span data-ttu-id="3c6ea-174">clé Hello que vous avez copié ci-dessus</span><span class="sxs-lookup"><span data-stu-id="3c6ea-174">hello key you copied above</span></span>
* <span data-ttu-id="3c6ea-175">nom de Hello du domaine de votre client</span><span class="sxs-lookup"><span data-stu-id="3c6ea-175">hello name of your tenant's domain</span></span>

<span data-ttu-id="3c6ea-176">tooauthenticate, l’envoi d’une publication demande trop`https://login.microsoft.com` avec hello paramètres dans le corps de hello suivants :</span><span class="sxs-lookup"><span data-stu-id="3c6ea-176">tooauthenticate, send a post request too`https://login.microsoft.com` with hello following parameters in hello body:</span></span>

* <span data-ttu-id="3c6ea-177">grant_type : « **client_informationsidentification** »</span><span class="sxs-lookup"><span data-stu-id="3c6ea-177">grant_type: “**client_credentials**”</span></span>
* <span data-ttu-id="3c6ea-178">resource: “**https://graph.microsoft.com**”</span><span class="sxs-lookup"><span data-stu-id="3c6ea-178">resource: “**https://graph.microsoft.com**”</span></span>
* <span data-ttu-id="3c6ea-179">client_id : <your client ID></span><span class="sxs-lookup"><span data-stu-id="3c6ea-179">client_id: <your client ID></span></span>
* <span data-ttu-id="3c6ea-180">client_secret : <your key></span><span class="sxs-lookup"><span data-stu-id="3c6ea-180">client_secret: <your key></span></span>

> [!NOTE]
> <span data-ttu-id="3c6ea-181">Vous avez besoin de valeurs de tooprovide pour hello **client_id** et hello **client_secret** paramètre.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-181">You need tooprovide values for hello **client_id** and hello **client_secret** parameter.</span></span>
> 
> 

<span data-ttu-id="3c6ea-182">Si l’opération réussit, elle retourne un jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-182">If successful, this returns an authentication token.</span></span>  
<span data-ttu-id="3c6ea-183">toocall hello API, créez un en-tête avec hello suivant paramètre :</span><span class="sxs-lookup"><span data-stu-id="3c6ea-183">toocall hello API, create a header with hello following parameter:</span></span>

    `Authorization`=”<token_type> <access_token>"


<span data-ttu-id="3c6ea-184">Lors de l’authentification, vous pouvez trouver le type de jeton hello et le jeton d’accès Bonjour renvoyé un jeton.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-184">When authenticating, you can find hello token type and access token in hello returned token.</span></span>

<span data-ttu-id="3c6ea-185">Envoyer cet en-tête comme un toohello de demande suivant l’URL de l’API :`https://graph.microsoft.com/beta/identityRiskEvents`</span><span class="sxs-lookup"><span data-stu-id="3c6ea-185">Send this header as a request toohello following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span></span>

<span data-ttu-id="3c6ea-186">réponse de Hello, en cas de réussite, est une collection d’identité événements à risque et des données associées dans hello format JSON OData, qui peut être analysé et géré convenance.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-186">hello response, if successful, is a collection of identity risk events and associated data in hello OData JSON format, which can be parsed and handled as see fit.</span></span>

<span data-ttu-id="3c6ea-187">Voici un exemple de code pour l’authentification et l’appel de l’API hello à l’aide de Powershell.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-187">Here’s sample code for authenticating and calling hello API using Powershell.</span></span>  
<span data-ttu-id="3c6ea-188">Il suffit d’ajouter l’ID client, la clé ainsi que le domaine client.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-188">Just add your client ID, key, and tenant domain.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="3c6ea-189">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3c6ea-189">Next steps</span></span>
<span data-ttu-id="3c6ea-190">Félicitations, vous venez de créer votre première tooMicrosoft d’appel de graphique.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-190">Congratulations, you just made your first call tooMicrosoft Graph!</span></span>  
<span data-ttu-id="3c6ea-191">Maintenant, vous pouvez interroger les événements à risque identité et utilisent les données hello. Toutefois, vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-191">Now you can query identity risk events and use hello data however you see fit.</span></span>

<span data-ttu-id="3c6ea-192">toolearn en savoir plus sur Microsoft Graph et comment les applications toobuild à l’aide de hello API Graph, consultez hello [documentation](https://graph.microsoft.io/docs) et bien plus encore sur hello [site de Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="3c6ea-192">toolearn more about Microsoft Graph and how toobuild applications using hello Graph API, check out hello [documentation](https://graph.microsoft.io/docs) and much more on hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span> <span data-ttu-id="3c6ea-193">En outre, assurez-vous que toobookmark hello [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page qui répertorie toutes les API de Protection d’identité disponibles dans le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-193">Also, make sure toobookmark hello [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of hello Identity Protection APIs available in Graph.</span></span> <span data-ttu-id="3c6ea-194">Comme nous ajoutons de nouvelles façons toowork, avec la Protection d’identité via l’API, vous verrez les sur cette page.</span><span class="sxs-lookup"><span data-stu-id="3c6ea-194">As we add new ways toowork with Identity Protection via API, you’ll see them on that page.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3c6ea-195">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3c6ea-195">Additional resources</span></span>
* [<span data-ttu-id="3c6ea-196">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="3c6ea-196">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
* [<span data-ttu-id="3c6ea-197">Types d’événements à risque détectés par Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="3c6ea-197">Types of risk events detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-risk-events-types.md)
* [<span data-ttu-id="3c6ea-198">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="3c6ea-198">Microsoft Graph</span></span>](https://graph.microsoft.io/)
* [<span data-ttu-id="3c6ea-199">Overview of Microsoft Graph (Vue d’ensemble de Microsoft Graph)</span><span class="sxs-lookup"><span data-stu-id="3c6ea-199">Overview of Microsoft Graph</span></span>](https://graph.microsoft.io/docs)
* [<span data-ttu-id="3c6ea-200">Azure AD Identity Protection Service Root (Racine de service d’Azure AD Identity Protection)</span><span class="sxs-lookup"><span data-stu-id="3c6ea-200">Azure AD Identity Protection Service Root</span></span>](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

