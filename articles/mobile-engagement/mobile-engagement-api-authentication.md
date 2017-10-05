---
title: "Authentifier avec l’API REST de Mobile Engagement"
description: "Décrit comment authentifier avec l’API REST Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: da82cb36-957a-4e19-a805-b44733cf6597
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: b05181d9252c0a804648e01b4058019278ae5abe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a><span data-ttu-id="c2247-103">Authentifier avec l’API REST de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="c2247-103">Authenticate with Mobile Engagement REST APIs</span></span>
## <a name="overview"></a><span data-ttu-id="c2247-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="c2247-104">Overview</span></span>
<span data-ttu-id="c2247-105">Ce document décrit comment obtenir un jeton OAuth AAD valide pour s’authentifier auprès des API REST Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="c2247-105">This document describes how to get a valid AAD Oauth token to authenticate with the Mobile Engagement REST APIs.</span></span> 

<span data-ttu-id="c2247-106">Il suppose que vous disposez d’un abonnement Azure valide et que vous avez créé une application Mobile Engagement à l'aide d'un de nos [didacticiels pour les développeurs](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c2247-106">It is assumed that you have a valid Azure subscription and you have created a Mobile Engagement app using one of our [Developer Tutorials](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="authentication"></a><span data-ttu-id="c2247-107">Authentification</span><span class="sxs-lookup"><span data-stu-id="c2247-107">Authentication</span></span>
<span data-ttu-id="c2247-108">Un jeton OAuth basé sur Microsoft Azure Active Directory est utilisé pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="c2247-108">A Microsoft Azure Active Directory based OAuth token is used for authentication.</span></span> 

<span data-ttu-id="c2247-109">Pour authentifier une requête API, un en-tête d’autorisation doit être ajouté à chaque requête, qui se présente sous la forme suivante :</span><span class="sxs-lookup"><span data-stu-id="c2247-109">In order to authentication an API request, an authorization header must be added to every request which is of the following form:</span></span>

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> <span data-ttu-id="c2247-110">Les jetons Azure Active Directory expirent dans 1 heure.</span><span class="sxs-lookup"><span data-stu-id="c2247-110">Azure Active Directory tokens expire in 1 hour.</span></span>
> 
> 

<span data-ttu-id="c2247-111">Il existe plusieurs façons d’obtenir un jeton.</span><span class="sxs-lookup"><span data-stu-id="c2247-111">There are several ways to get a token.</span></span> <span data-ttu-id="c2247-112">Comme les API sont généralement appelées à partir d’un service cloud, vous voulez utiliser une clé API.</span><span class="sxs-lookup"><span data-stu-id="c2247-112">Since the APIs are generally called from a cloud service, you want to use an API key.</span></span> <span data-ttu-id="c2247-113">Dans la terminologie Azure, une clé d’API est appelée mot de passe principal de du service.</span><span class="sxs-lookup"><span data-stu-id="c2247-113">An API key in Azure terminology is called a Service principal password.</span></span> <span data-ttu-id="c2247-114">La procédure suivante décrit comment la configurer manuellement.</span><span class="sxs-lookup"><span data-stu-id="c2247-114">The following procedure describes one way to setting it up manually.</span></span>

### <a name="one-time-setup-using-script"></a><span data-ttu-id="c2247-115">Installation unique (à l'aide d’un script)</span><span class="sxs-lookup"><span data-stu-id="c2247-115">One-time setup (using script)</span></span>
<span data-ttu-id="c2247-116">Vous devez suivre l’ensemble des instructions ci-dessous pour effectuer l’installation à l’aide d’un script PowerShell qui prend le temps minimal pour l’installation, mais utilise les valeurs par défaut les plus autorisées.</span><span class="sxs-lookup"><span data-stu-id="c2247-116">You should follow the set of instructions below to perform the setup using a PowerShell script which takes the minimum time for setup but uses the most permissible defaults.</span></span> <span data-ttu-id="c2247-117">Si vous le souhaitez, vous pouvez également suivre les instructions de l’ [installation manuelle](mobile-engagement-api-authentication-manual.md) pour effectuer cette opération directement à partir du portail Azure et affiner la configuration.</span><span class="sxs-lookup"><span data-stu-id="c2247-117">Optionally, you can also follow the instructions in the [manual setup](mobile-engagement-api-authentication-manual.md) for doing this from the Azure portal directly and do finer configuration.</span></span> 

1. <span data-ttu-id="c2247-118">Récupérez la dernière version d’Azure PowerShell [ici](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="c2247-118">Get the latest version of Azure PowerShell from [here](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="c2247-119">Consultez ce [lien](/powershell/azure/overview)pour obtenir des instructions de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="c2247-119">For more information on the download instructions, you can see this [link](/powershell/azure/overview).</span></span>  
2. <span data-ttu-id="c2247-120">Une fois Azure PowerShell installé, utilisez les commandes suivantes pour vérifier que le **module Azure** est installé :</span><span class="sxs-lookup"><span data-stu-id="c2247-120">Once Azure PowerShell is installed, use the following commands to ensure that you have the **Azure module** installed:</span></span>
   
    <span data-ttu-id="c2247-121">a.</span><span class="sxs-lookup"><span data-stu-id="c2247-121">a.</span></span> <span data-ttu-id="c2247-122">Vérifiez que le module Azure PowerShell est disponible dans la liste des modules disponibles.</span><span class="sxs-lookup"><span data-stu-id="c2247-122">Make sure the Azure PowerShell module is available in the list of available modules.</span></span> 
   
        Get-Module –ListAvailable 
   
    ![Modules Azure disponibles][1]
   
    <span data-ttu-id="c2247-124">b.</span><span class="sxs-lookup"><span data-stu-id="c2247-124">b.</span></span> <span data-ttu-id="c2247-125">Si vous ne trouvez pas le module Azure PowerShell dans la liste ci-dessus, vous devez exécuter la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c2247-125">If you do not find the Azure PowerShell module in the above list then you need to run the following:</span></span>
   
        Import-Module Azure 
3. <span data-ttu-id="c2247-126">Connectez-vous à Azure Resource Manager à partir de PowerShell en exécutant la commande suivante et en fournissant vos nom d’utilisateur et mot de passe pour votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="c2247-126">Login to the Azure Resource Manager from PowerShell by running the following command and providing your user name and password for your Azure account:</span></span> 
   
        Login-AzureRmAccount
4. <span data-ttu-id="c2247-127">Si vous avez plusieurs abonnements, vous devez exécuter ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="c2247-127">If you have multiple subscriptions then you should run the following:</span></span>
   
    <span data-ttu-id="c2247-128">a.</span><span class="sxs-lookup"><span data-stu-id="c2247-128">a.</span></span> <span data-ttu-id="c2247-129">Obtenez une liste de tous vos abonnements et copiez le SubscriptionId de l’abonnement que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="c2247-129">Get a list of all your subscriptions and copy the SubscriptionId of the subscription you want to use.</span></span> <span data-ttu-id="c2247-130">Vérifiez que cet abonnement est le même que celui qui possède l’application Mobile Engagement avec laquelle vous allez interagir à l’aide des API.</span><span class="sxs-lookup"><span data-stu-id="c2247-130">Make sure this subscription is the same one which has the Mobile Engagement App which you are going to interact with using the APIs.</span></span> 
   
        Get-AzureRmSubscription
   
    <span data-ttu-id="c2247-131">b.</span><span class="sxs-lookup"><span data-stu-id="c2247-131">b.</span></span> <span data-ttu-id="c2247-132">Exécutez la commande suivante pour spécifier le SubscriptionId qui servira à configurer l’abonnement à utiliser.</span><span class="sxs-lookup"><span data-stu-id="c2247-132">Run the following command providing the SubscriptionId to configure the subscription to be used.</span></span>
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. <span data-ttu-id="c2247-133">Copiez le texte du script [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) sur votre ordinateur local puis enregistrez-le en tant qu’applet de commande PowerShell (par exemple, `APIAuth.ps1`) et exécutez-le `.\APIAuth.ps1`.</span><span class="sxs-lookup"><span data-stu-id="c2247-133">Copy the text for the [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) script to your local machine and save it as a PowerShell cmdlet (e.g. `APIAuth.ps1`) and execute it `.\APIAuth.ps1`.</span></span> 
6. <span data-ttu-id="c2247-134">Le script vous demande de fournir une entrée pour **nom_principal**.</span><span class="sxs-lookup"><span data-stu-id="c2247-134">The script will ask you to provide an input for **principalName**.</span></span> <span data-ttu-id="c2247-135">Indiquez ici un nom approprié que vous souhaitez utiliser pour créer votre application Active Directory (par exemple, APIAuth).</span><span class="sxs-lookup"><span data-stu-id="c2247-135">Provide a suitable name here that you want to use to create your Active Directory application (e.g. APIAuth).</span></span> 
7. <span data-ttu-id="c2247-136">Une fois le script terminé, il affiche les quatre valeurs suivantes nécessaires pour l’authentification par programmation auprès d’Active Directory. Veillez à bien les copier.</span><span class="sxs-lookup"><span data-stu-id="c2247-136">After the script completes, it will display the following four values that you will need to authenticate programmatically with AD so make sure to copy them.</span></span> 
   
    <span data-ttu-id="c2247-137">**TenantId**, **SubscriptionId**, **ApplicationId** et **Secret**.</span><span class="sxs-lookup"><span data-stu-id="c2247-137">**TenantId**, **SubscriptionId**, **ApplicationId**, and **Secret**.</span></span>
   
    <span data-ttu-id="c2247-138">Vous utilisez la valeur TenantId `{TENANT_ID}`, la valeur ApplicationId `{CLIENT_ID}` et la valeur Secret `{CLIENT_SECRET}`.</span><span class="sxs-lookup"><span data-stu-id="c2247-138">You will use TenantId as `{TENANT_ID}`, ApplicationId as `{CLIENT_ID}` and Secret as `{CLIENT_SECRET}`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c2247-139">Votre stratégie de sécurité par défaut peut vous empêche d'exécuter un script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2247-139">Your default security policy may block you from running a PowerShell scripts.</span></span> <span data-ttu-id="c2247-140">Dans ce cas, configurez temporairement votre stratégie d'exécution pour permettre l'exécution du script à l'aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c2247-140">If so, you temporarily configure your execution policy to allow script execution using the following command:</span></span>
   > 
   > <span data-ttu-id="c2247-141">Set-ExecutionPolicy RemoteSigned</span><span class="sxs-lookup"><span data-stu-id="c2247-141">Set-ExecutionPolicy RemoteSigned</span></span>
   > 
   > 
8. <span data-ttu-id="c2247-142">Voici à quoi ressemble le jeu d’applets de commande PS.</span><span class="sxs-lookup"><span data-stu-id="c2247-142">Here is how the set of PS cmdlets would look like.</span></span> 
   
    ![][3]
9. <span data-ttu-id="c2247-143">Vérifiez dans le Portail de gestion Azure qu’une application AD a été créée avec le nom fourni au script appelé **nom_principal** sous **Afficher les applications que ma société possède**.</span><span class="sxs-lookup"><span data-stu-id="c2247-143">Check in the Azure Management portal that a new AD application was created with the name you provided to the script called **principalName** under **Show Applications my company owns**.</span></span>
   
    ![][4]

#### <a name="steps-to-get-a-valid-token"></a><span data-ttu-id="c2247-144">Procédure d'obtention d'un jeton valide</span><span class="sxs-lookup"><span data-stu-id="c2247-144">Steps to get a valid token</span></span>
1. <span data-ttu-id="c2247-145">Appelez l’API avec les paramètres suivants et veillez à remplacer les valeurs TENANT\_ID, CLIENT\_ID et CLIENT\_SECRET :</span><span class="sxs-lookup"><span data-stu-id="c2247-145">Call the API with the following parameters and make sure to replace the TENANT\_ID, CLIENT\_ID and CLIENT\_SECRET:</span></span>
   
   * <span data-ttu-id="c2247-146">**URL de la demande** sous la forme *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span><span class="sxs-lookup"><span data-stu-id="c2247-146">**Request URL** as *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span></span>
   * <span data-ttu-id="c2247-147">**En-tête Content-Type HTTP** sous la forme *application/x-www-form-urlencoded*</span><span class="sxs-lookup"><span data-stu-id="c2247-147">**HTTP Content-Type header** as *application/x-www-form-urlencoded*</span></span>
   * <span data-ttu-id="c2247-148">**Corps de la requête HTTP** sous la forme *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span><span class="sxs-lookup"><span data-stu-id="c2247-148">**HTTP Request Body** as *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span></span>
     
     <span data-ttu-id="c2247-149">Voici un exemple de requête :</span><span class="sxs-lookup"><span data-stu-id="c2247-149">The following is an example request:</span></span>
     
       <span data-ttu-id="c2247-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span><span class="sxs-lookup"><span data-stu-id="c2247-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span></span>
     
     <span data-ttu-id="c2247-151">Voici un exemple de réponse :</span><span class="sxs-lookup"><span data-stu-id="c2247-151">Here is an example response:</span></span>
     
       <span data-ttu-id="c2247-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span><span class="sxs-lookup"><span data-stu-id="c2247-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span></span>
     
       <span data-ttu-id="c2247-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span><span class="sxs-lookup"><span data-stu-id="c2247-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span></span>
     
     <span data-ttu-id="c2247-154">Cet exemple incluait l’encodage de l’URL des paramètres POST, et la valeur `resource` est en fait `https://management.core.windows.net/`.</span><span class="sxs-lookup"><span data-stu-id="c2247-154">This example included URL encoding of the POST parameters, `resource` value is actually `https://management.core.windows.net/`.</span></span> <span data-ttu-id="c2247-155">Veillez également à encoder l’URL `{CLIENT_SECRET}` car elle peut contenir des caractères spéciaux.</span><span class="sxs-lookup"><span data-stu-id="c2247-155">Be careful to also URL encode `{CLIENT_SECRET}` as it may contain special characters.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="c2247-156">Pour le test, vous pouvez utiliser un outil client HTTP comme [Fiddler](http://www.telerik.com/fiddler) ou [l’extension Postman sur Chrome](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span><span class="sxs-lookup"><span data-stu-id="c2247-156">For testing, you can use an HTTP client tool like [Fiddler](http://www.telerik.com/fiddler) or [Chrome Postman extension](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span></span> 
     > 
     > 
2. <span data-ttu-id="c2247-157">Dans chaque appel d'API, incluez l'en-tête de requête d'autorisation :</span><span class="sxs-lookup"><span data-stu-id="c2247-157">Now in every API call, include the authorization request header:</span></span>
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    <span data-ttu-id="c2247-158">Si vous obtenez un code d'état 401, vérifiez le corps de la réponse car il peut vous indiquer que le jeton a expiré.</span><span class="sxs-lookup"><span data-stu-id="c2247-158">If you get a 401 status code returned, check the response body, it might tell you the token is expired.</span></span> <span data-ttu-id="c2247-159">Dans ce cas, récupérez un nouveau jeton.</span><span class="sxs-lookup"><span data-stu-id="c2247-159">In that case, get a new token.</span></span>

## <a name="using-the-apis"></a><span data-ttu-id="c2247-160">Utilisation des API</span><span class="sxs-lookup"><span data-stu-id="c2247-160">Using the APIs</span></span>
<span data-ttu-id="c2247-161">Maintenant que vous avez un jeton valide, vous êtes prêt à passer les appels d'API.</span><span class="sxs-lookup"><span data-stu-id="c2247-161">Now that you have a valid token, you are ready to make the API calls.</span></span>

1. <span data-ttu-id="c2247-162">Dans chaque requête API, vous devez passer un jeton valide, non expiré, que vous avez obtenu dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="c2247-162">In each API request, you will need to pass a valid, unexpired token which you obtained in the previous section.</span></span>
2. <span data-ttu-id="c2247-163">Vous devez spécifier certains paramètres dans l'URI de la requête qui identifie votre application.</span><span class="sxs-lookup"><span data-stu-id="c2247-163">You will need to plug in some parameters into the request URI which identifies your application.</span></span> <span data-ttu-id="c2247-164">L'URI de la requête ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="c2247-164">The request URI looks like the following</span></span>
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    <span data-ttu-id="c2247-165">Pour obtenir les paramètres, cliquez sur le nom de votre application puis sur Tableau de bord : vous verrez alors une page similaire à celle-ci, avec 3 paramètres.</span><span class="sxs-lookup"><span data-stu-id="c2247-165">To get the parameters, click on your application name and click Dashboard and you will see a page like the following with all the 3 parameters.</span></span>
   
   * <span data-ttu-id="c2247-166">**1** `{subscription-id}`</span><span class="sxs-lookup"><span data-stu-id="c2247-166">**1** `{subscription-id}`</span></span>
   * <span data-ttu-id="c2247-167">**2** `{app-collection}`</span><span class="sxs-lookup"><span data-stu-id="c2247-167">**2** `{app-collection}`</span></span>
   * <span data-ttu-id="c2247-168">**3** `{app-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="c2247-168">**3** `{app-resource-name}`</span></span>
   * <span data-ttu-id="c2247-169">**4** Le nom de votre groupe de ressources va être **MobileEngagement** sauf si vous en avez créé un autre.</span><span class="sxs-lookup"><span data-stu-id="c2247-169">**4** Your Resource Group name is going to be **MobileEngagement** unless you created a new one.</span></span> 
     
     ![Paramètres URI d’API Mobile Engagement][2]

> [!NOTE]
> <br/>
> 
> 1. <span data-ttu-id="c2247-171">Ignorez l’adresse racine de l’API car elle s’appliquait aux API précédentes.</span><span class="sxs-lookup"><span data-stu-id="c2247-171">Ignore the API Root Address as this was for the previous APIs.</span></span><br/>
> 2. <span data-ttu-id="c2247-172">Si vous avez créé l’application à l’aide du portail Azure Classic, vous devez utiliser le nom de ressource de l’application qui est différent du nom de l’application elle-même.</span><span class="sxs-lookup"><span data-stu-id="c2247-172">If you created the app using Azure Classic portal then you need to use the Application Resource name which is different than the Application name itself.</span></span> <span data-ttu-id="c2247-173">Si vous avez créé l’application dans le portail Azure, vous devez utiliser le nom de l’application elle-même (il n’existe aucune distinction entre le nom de ressource de l’application et le nom de l’application pour les applications créées dans le nouveau portail).</span><span class="sxs-lookup"><span data-stu-id="c2247-173">If you created the app in the Azure Portal then you should use the App Name itself (there is no differentiation between Application Resource Name and App Name for apps created in the new portal).</span></span>  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



