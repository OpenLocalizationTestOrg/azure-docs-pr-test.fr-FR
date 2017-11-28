---
title: aaaAuthenticate avec les API REST Mobile Engagement
description: "Décrit comment tooauthenticate avec l’API REST de Azure Mobile Engagement"
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
ms.openlocfilehash: 9b54aa5ec3da4bcf55ffe5b7e8d1759095d0c486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a><span data-ttu-id="8fd22-103">Authentifier avec l’API REST de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="8fd22-103">Authenticate with Mobile Engagement REST APIs</span></span>
## <a name="overview"></a><span data-ttu-id="8fd22-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="8fd22-104">Overview</span></span>
<span data-ttu-id="8fd22-105">Ce document décrit comment tooget un Oauth AAD valide de jeton tooauthenticate par hello Mobile Engagement REST API.</span><span class="sxs-lookup"><span data-stu-id="8fd22-105">This document describes how tooget a valid AAD Oauth token tooauthenticate with hello Mobile Engagement REST APIs.</span></span> 

<span data-ttu-id="8fd22-106">Il suppose que vous disposez d’un abonnement Azure valide et que vous avez créé une application Mobile Engagement à l'aide d'un de nos [didacticiels pour les développeurs](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8fd22-106">It is assumed that you have a valid Azure subscription and you have created a Mobile Engagement app using one of our [Developer Tutorials](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="authentication"></a><span data-ttu-id="8fd22-107">Authentification</span><span class="sxs-lookup"><span data-stu-id="8fd22-107">Authentication</span></span>
<span data-ttu-id="8fd22-108">Un jeton OAuth basé sur Microsoft Azure Active Directory est utilisé pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="8fd22-108">A Microsoft Azure Active Directory based OAuth token is used for authentication.</span></span> 

<span data-ttu-id="8fd22-109">Dans la requête d’ordre de tooauthentication une API, un en-tête d’autorisation doit être ajouté demande tooevery de hello suivant du formulaire :</span><span class="sxs-lookup"><span data-stu-id="8fd22-109">In order tooauthentication an API request, an authorization header must be added tooevery request which is of hello following form:</span></span>

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> <span data-ttu-id="8fd22-110">Les jetons Azure Active Directory expirent dans 1 heure.</span><span class="sxs-lookup"><span data-stu-id="8fd22-110">Azure Active Directory tokens expire in 1 hour.</span></span>
> 
> 

<span data-ttu-id="8fd22-111">Il existe plusieurs façons tooget un jeton.</span><span class="sxs-lookup"><span data-stu-id="8fd22-111">There are several ways tooget a token.</span></span> <span data-ttu-id="8fd22-112">Depuis hello Qu'api est généralement appelées à partir d’un service cloud, vous souhaitez toouse une clé d’API.</span><span class="sxs-lookup"><span data-stu-id="8fd22-112">Since hello APIs are generally called from a cloud service, you want toouse an API key.</span></span> <span data-ttu-id="8fd22-113">Dans la terminologie Azure, une clé d’API est appelée mot de passe principal de du service.</span><span class="sxs-lookup"><span data-stu-id="8fd22-113">An API key in Azure terminology is called a Service principal password.</span></span> <span data-ttu-id="8fd22-114">Hello procédure suivante décrit une façon toosetting il configurer manuellement.</span><span class="sxs-lookup"><span data-stu-id="8fd22-114">hello following procedure describes one way toosetting it up manually.</span></span>

### <a name="one-time-setup-using-script"></a><span data-ttu-id="8fd22-115">Installation unique (à l'aide d’un script)</span><span class="sxs-lookup"><span data-stu-id="8fd22-115">One-time setup (using script)</span></span>
<span data-ttu-id="8fd22-116">Vous devez suivez hello instructions sous le programme d’installation hello tooperform à l’aide d’un script PowerShell qui consomme du temps hello minimale pour le programme d’installation, mais utilise hello les valeurs par défaut plus autorisées.</span><span class="sxs-lookup"><span data-stu-id="8fd22-116">You should follow hello set of instructions below tooperform hello setup using a PowerShell script which takes hello minimum time for setup but uses hello most permissible defaults.</span></span> <span data-ttu-id="8fd22-117">Si vous le souhaitez, vous pouvez également suivre les instructions hello Bonjour [le programme d’installation manuelle](mobile-engagement-api-authentication-manual.md) par le biais de hello directement le portail Azure et de configuration plus précie de faire.</span><span class="sxs-lookup"><span data-stu-id="8fd22-117">Optionally, you can also follow hello instructions in hello [manual setup](mobile-engagement-api-authentication-manual.md) for doing this from hello Azure portal directly and do finer configuration.</span></span> 

1. <span data-ttu-id="8fd22-118">Obtenir la version la plus récente d’Azure PowerShell à partir de hello [ici](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="8fd22-118">Get hello latest version of Azure PowerShell from [here](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="8fd22-119">Pour plus d’informations sur les instructions de téléchargement hello, vous pouvez voir cela [lien](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8fd22-119">For more information on hello download instructions, you can see this [link](/powershell/azure/overview).</span></span>  
2. <span data-ttu-id="8fd22-120">Une fois Azure PowerShell est installé, suivant de hello utilisez commandes tooensure que vous avez hello **module Azure** installé :</span><span class="sxs-lookup"><span data-stu-id="8fd22-120">Once Azure PowerShell is installed, use hello following commands tooensure that you have hello **Azure module** installed:</span></span>
   
    <span data-ttu-id="8fd22-121">a.</span><span class="sxs-lookup"><span data-stu-id="8fd22-121">a.</span></span> <span data-ttu-id="8fd22-122">Assurez-vous que le module Azure PowerShell de hello est disponible dans la liste hello des modules disponibles.</span><span class="sxs-lookup"><span data-stu-id="8fd22-122">Make sure hello Azure PowerShell module is available in hello list of available modules.</span></span> 
   
        Get-Module –ListAvailable 
   
    ![Modules Azure disponibles][1]
   
    <span data-ttu-id="8fd22-124">b.</span><span class="sxs-lookup"><span data-stu-id="8fd22-124">b.</span></span> <span data-ttu-id="8fd22-125">Si vous ne trouvez pas le module Azure PowerShell de hello Bonjour au-dessus de liste puis toorun hello éléments suivants sont nécessaires :</span><span class="sxs-lookup"><span data-stu-id="8fd22-125">If you do not find hello Azure PowerShell module in hello above list then you need toorun hello following:</span></span>
   
        Import-Module Azure 
3. <span data-ttu-id="8fd22-126">Connexion toohello Azure Resource Manager à partir de PowerShell en exécutant hello la commande suivante et en fournissant votre nom d’utilisateur et un mot de passe pour votre compte Azure :</span><span class="sxs-lookup"><span data-stu-id="8fd22-126">Login toohello Azure Resource Manager from PowerShell by running hello following command and providing your user name and password for your Azure account:</span></span> 
   
        Login-AzureRmAccount
4. <span data-ttu-id="8fd22-127">Si vous avez plusieurs abonnements, puis vous devez exécuter les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="8fd22-127">If you have multiple subscriptions then you should run hello following:</span></span>
   
    <span data-ttu-id="8fd22-128">a.</span><span class="sxs-lookup"><span data-stu-id="8fd22-128">a.</span></span> <span data-ttu-id="8fd22-129">Obtenir une liste de tous vos abonnements et hello de copie SubscriptionId d’abonnement hello toouse.</span><span class="sxs-lookup"><span data-stu-id="8fd22-129">Get a list of all your subscriptions and copy hello SubscriptionId of hello subscription you want toouse.</span></span> <span data-ttu-id="8fd22-130">Assurez-vous que cet abonnement est hello identique à celui qui a hello l’application Mobile Engagement qui vous toointeract à l’utilisation de hello API.</span><span class="sxs-lookup"><span data-stu-id="8fd22-130">Make sure this subscription is hello same one which has hello Mobile Engagement App which you are going toointeract with using hello APIs.</span></span> 
   
        Get-AzureRmSubscription
   
    <span data-ttu-id="8fd22-131">b.</span><span class="sxs-lookup"><span data-stu-id="8fd22-131">b.</span></span> <span data-ttu-id="8fd22-132">La commande suivante d’exécution hello les toobe abonnement d’hello de tooconfigure du SubscriptionId hello fournissant utilisé.</span><span class="sxs-lookup"><span data-stu-id="8fd22-132">Run hello following command providing hello SubscriptionId tooconfigure hello subscription toobe used.</span></span>
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. <span data-ttu-id="8fd22-133">Copier le texte hello pour hello [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) ordinateur local de tooyour de script et l’enregistrer en tant qu’une applet de commande PowerShell (par exemple, `APIAuth.ps1`) et de l’exécuter `.\APIAuth.ps1`.</span><span class="sxs-lookup"><span data-stu-id="8fd22-133">Copy hello text for hello [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) script tooyour local machine and save it as a PowerShell cmdlet (e.g. `APIAuth.ps1`) and execute it `.\APIAuth.ps1`.</span></span> 
6. <span data-ttu-id="8fd22-134">Hello script vous demandera tooprovide une entrée pour **principal**.</span><span class="sxs-lookup"><span data-stu-id="8fd22-134">hello script will ask you tooprovide an input for **principalName**.</span></span> <span data-ttu-id="8fd22-135">Fournir un nom approprié que vous souhaitez toouse toocreate votre application Active Directory (par exemple, APIAuth).</span><span class="sxs-lookup"><span data-stu-id="8fd22-135">Provide a suitable name here that you want toouse toocreate your Active Directory application (e.g. APIAuth).</span></span> 
7. <span data-ttu-id="8fd22-136">Une fois hello script terminé, il affiche hello suivant quatre valeurs dont vous aurez besoin tooauthenticate par programme avec Active Directory a donc pas vraiment toocopy les.</span><span class="sxs-lookup"><span data-stu-id="8fd22-136">After hello script completes, it will display hello following four values that you will need tooauthenticate programmatically with AD so make sure toocopy them.</span></span> 
   
    <span data-ttu-id="8fd22-137">**TenantId**, **SubscriptionId**, **ApplicationId** et **Secret**.</span><span class="sxs-lookup"><span data-stu-id="8fd22-137">**TenantId**, **SubscriptionId**, **ApplicationId**, and **Secret**.</span></span>
   
    <span data-ttu-id="8fd22-138">Vous utilisez la valeur TenantId `{TENANT_ID}`, la valeur ApplicationId `{CLIENT_ID}` et la valeur Secret `{CLIENT_SECRET}`.</span><span class="sxs-lookup"><span data-stu-id="8fd22-138">You will use TenantId as `{TENANT_ID}`, ApplicationId as `{CLIENT_ID}` and Secret as `{CLIENT_SECRET}`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8fd22-139">Votre stratégie de sécurité par défaut peut vous empêche d'exécuter un script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8fd22-139">Your default security policy may block you from running a PowerShell scripts.</span></span> <span data-ttu-id="8fd22-140">Dans ce cas, vous configurez temporairement votre exécution stratégie tooallow l’exécution du script à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8fd22-140">If so, you temporarily configure your execution policy tooallow script execution using hello following command:</span></span>
   > 
   > <span data-ttu-id="8fd22-141">Set-ExecutionPolicy RemoteSigned</span><span class="sxs-lookup"><span data-stu-id="8fd22-141">Set-ExecutionPolicy RemoteSigned</span></span>
   > 
   > 
8. <span data-ttu-id="8fd22-142">Voici comment ensemble hello d’applets de commande PS ressemble à.</span><span class="sxs-lookup"><span data-stu-id="8fd22-142">Here is how hello set of PS cmdlets would look like.</span></span> 
   
    ![][3]
9. <span data-ttu-id="8fd22-143">Vérifiez dans le portail de gestion Azure hello qu’une application AD a été créée avec le nom de hello vous fourni toohello script appelé **principal** sous **afficher les Applications que ma société possède**.</span><span class="sxs-lookup"><span data-stu-id="8fd22-143">Check in hello Azure Management portal that a new AD application was created with hello name you provided toohello script called **principalName** under **Show Applications my company owns**.</span></span>
   
    ![][4]

#### <a name="steps-tooget-a-valid-token"></a><span data-ttu-id="8fd22-144">Étapes tooget un jeton valide</span><span class="sxs-lookup"><span data-stu-id="8fd22-144">Steps tooget a valid token</span></span>
1. <span data-ttu-id="8fd22-145">Appeler des API de hello avec les paramètres suivants de hello et assurez-vous que tooreplace hello client\_ID, le CLIENT\_ID et le CLIENT\_SECRET :</span><span class="sxs-lookup"><span data-stu-id="8fd22-145">Call hello API with hello following parameters and make sure tooreplace hello TENANT\_ID, CLIENT\_ID and CLIENT\_SECRET:</span></span>
   
   * <span data-ttu-id="8fd22-146">**URL de la demande** sous la forme *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span><span class="sxs-lookup"><span data-stu-id="8fd22-146">**Request URL** as *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span></span>
   * <span data-ttu-id="8fd22-147">**En-tête Content-Type HTTP** sous la forme *application/x-www-form-urlencoded*</span><span class="sxs-lookup"><span data-stu-id="8fd22-147">**HTTP Content-Type header** as *application/x-www-form-urlencoded*</span></span>
   * <span data-ttu-id="8fd22-148">**Corps de la requête HTTP** sous la forme *grant\_type=client\_credentials&amp;client_id={CLIENT\_ID}&amp;client_secret={CLIENT\_SECRET}&amp;resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span><span class="sxs-lookup"><span data-stu-id="8fd22-148">**HTTP Request Body** as *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span></span>
     
     <span data-ttu-id="8fd22-149">Hello Voici un exemple de demande :</span><span class="sxs-lookup"><span data-stu-id="8fd22-149">hello following is an example request:</span></span>
     
       <span data-ttu-id="8fd22-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span><span class="sxs-lookup"><span data-stu-id="8fd22-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span></span>
     
     <span data-ttu-id="8fd22-151">Voici un exemple de réponse :</span><span class="sxs-lookup"><span data-stu-id="8fd22-151">Here is an example response:</span></span>
     
       <span data-ttu-id="8fd22-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span><span class="sxs-lookup"><span data-stu-id="8fd22-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span></span>
     
       <span data-ttu-id="8fd22-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span><span class="sxs-lookup"><span data-stu-id="8fd22-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span></span>
     
     <span data-ttu-id="8fd22-154">Cet exemple montre comment inclure encodage URL des paramètres de publication de hello, `resource` valeur est en réalité `https://management.core.windows.net/`.</span><span class="sxs-lookup"><span data-stu-id="8fd22-154">This example included URL encoding of hello POST parameters, `resource` value is actually `https://management.core.windows.net/`.</span></span> <span data-ttu-id="8fd22-155">Veillez à coder par URL de tooalso `{CLIENT_SECRET}` comme il peut contenir des caractères spéciaux.</span><span class="sxs-lookup"><span data-stu-id="8fd22-155">Be careful tooalso URL encode `{CLIENT_SECRET}` as it may contain special characters.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="8fd22-156">Pour le test, vous pouvez utiliser un outil client HTTP comme [Fiddler](http://www.telerik.com/fiddler) ou [l’extension Postman sur Chrome](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span><span class="sxs-lookup"><span data-stu-id="8fd22-156">For testing, you can use an HTTP client tool like [Fiddler](http://www.telerik.com/fiddler) or [Chrome Postman extension](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span></span> 
     > 
     > 
2. <span data-ttu-id="8fd22-157">Dans chaque appel d’API, incluent désormais en-tête de demande d’autorisation hello :</span><span class="sxs-lookup"><span data-stu-id="8fd22-157">Now in every API call, include hello authorization request header:</span></span>
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    <span data-ttu-id="8fd22-158">Si vous obtenez un code de 401 état retourné, cocher hello corps de la réponse, il peut vous dire à hello jeton a expiré.</span><span class="sxs-lookup"><span data-stu-id="8fd22-158">If you get a 401 status code returned, check hello response body, it might tell you hello token is expired.</span></span> <span data-ttu-id="8fd22-159">Dans ce cas, récupérez un nouveau jeton.</span><span class="sxs-lookup"><span data-stu-id="8fd22-159">In that case, get a new token.</span></span>

## <a name="using-hello-apis"></a><span data-ttu-id="8fd22-160">À l’aide des API de hello</span><span class="sxs-lookup"><span data-stu-id="8fd22-160">Using hello APIs</span></span>
<span data-ttu-id="8fd22-161">Maintenant que vous avez un jeton valide, vous êtes prêt toomake hello API appels.</span><span class="sxs-lookup"><span data-stu-id="8fd22-161">Now that you have a valid token, you are ready toomake hello API calls.</span></span>

1. <span data-ttu-id="8fd22-162">Dans chaque demande d’API, vous devez toopass un jeton valide, non expiré, que vous avez obtenu dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="8fd22-162">In each API request, you will need toopass a valid, unexpired token which you obtained in hello previous section.</span></span>
2. <span data-ttu-id="8fd22-163">Vous devez tooplug dans certains paramètres dans la demande de hello URI qui identifie votre application.</span><span class="sxs-lookup"><span data-stu-id="8fd22-163">You will need tooplug in some parameters into hello request URI which identifies your application.</span></span> <span data-ttu-id="8fd22-164">URI de demande Hello ressemble à hello suivant</span><span class="sxs-lookup"><span data-stu-id="8fd22-164">hello request URI looks like hello following</span></span>
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    <span data-ttu-id="8fd22-165">paramètres de hello tooget, cliquez sur le nom de votre application et cliquez sur le tableau de bord et une page s’affiche comme suit hello avec tous les hello 3 paramètres.</span><span class="sxs-lookup"><span data-stu-id="8fd22-165">tooget hello parameters, click on your application name and click Dashboard and you will see a page like hello following with all hello 3 parameters.</span></span>
   
   * <span data-ttu-id="8fd22-166">**1**`{subscription-id}`</span><span class="sxs-lookup"><span data-stu-id="8fd22-166">**1** `{subscription-id}`</span></span>
   * <span data-ttu-id="8fd22-167">**2**`{app-collection}`</span><span class="sxs-lookup"><span data-stu-id="8fd22-167">**2** `{app-collection}`</span></span>
   * <span data-ttu-id="8fd22-168">**3**`{app-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="8fd22-168">**3** `{app-resource-name}`</span></span>
   * <span data-ttu-id="8fd22-169">**4** nom de votre groupe de ressources est en train de toobe **MobileEngagement** , sauf si vous avez créé un nouveau.</span><span class="sxs-lookup"><span data-stu-id="8fd22-169">**4** Your Resource Group name is going toobe **MobileEngagement** unless you created a new one.</span></span> 
     
     ![Paramètres URI d’API Mobile Engagement][2]

> [!NOTE]
> <br/>
> 
> 1. <span data-ttu-id="8fd22-171">Ignorer hello API racine adresse car il s’agissait de hello API précédentes.</span><span class="sxs-lookup"><span data-stu-id="8fd22-171">Ignore hello API Root Address as this was for hello previous APIs.</span></span><br/>
> 2. <span data-ttu-id="8fd22-172">Si vous avez créé l’application hello à l’aide du portail Azure Classic vous devez nom de ressource de l’Application hello toouse qui n’a pas de nom de l’Application hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="8fd22-172">If you created hello app using Azure Classic portal then you need toouse hello Application Resource name which is different than hello Application name itself.</span></span> <span data-ttu-id="8fd22-173">Si vous avez créé l’application hello Bonjour portail Azure vous devez utiliser hello nom de l’application elle-même (il n’existe aucune distinction entre le nom de ressource de l’Application et le nom de l’application pour les applications créées dans le nouveau portail de hello).</span><span class="sxs-lookup"><span data-stu-id="8fd22-173">If you created hello app in hello Azure Portal then you should use hello App Name itself (there is no differentiation between Application Resource Name and App Name for apps created in hello new portal).</span></span>  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



