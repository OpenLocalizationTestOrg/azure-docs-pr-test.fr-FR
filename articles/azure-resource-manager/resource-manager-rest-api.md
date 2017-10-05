---
title: API REST Resource Manager | Microsoft Docs
description: "Une vue d’ensemble des exemples d’authentification et de cas d’utilisation des API REST Resource Manager"
services: azure-resource-manager
documentationcenter: na
author: navalev
manager: timlt
editor: 
ms.assetid: e8d7a1d2-1e82-4212-8288-8697341408c5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/13/2017
ms.author: navale;tomfitz;
ms.openlocfilehash: 2f7ba23775545637de865f9ef63680ae22c62164
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="resource-manager-rest-apis"></a><span data-ttu-id="a9de6-103">API REST Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a9de6-103">Resource Manager REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a9de6-104">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9de6-104">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="a9de6-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="a9de6-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="a9de6-106">Portail</span><span class="sxs-lookup"><span data-stu-id="a9de6-106">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="a9de6-107">API REST</span><span class="sxs-lookup"><span data-stu-id="a9de6-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="a9de6-108">Derrière chaque appel à Azure Resource Manager, derrière chaque modèle déployé, derrière chaque compte de stockage configuré se trouvent un ou plusieurs appels à une API RESTful de l’Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a9de6-108">Behind every call to Azure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls to the Azure Resource Manager's RESTful API.</span></span> <span data-ttu-id="a9de6-109">Cette rubrique est consacrée à ces API et à la manière dont vous pouvez les appeler sans utiliser aucun kit SDK.</span><span class="sxs-lookup"><span data-stu-id="a9de6-109">This topic is devoted to those APIs and how you can call them without using any SDK at all.</span></span> <span data-ttu-id="a9de6-110">Cette approche est utile si vous souhaitez un contrôle total des requêtes à Azure ou si le kit SDK pour votre langue par défaut n’est pas disponible ou ne prend pas en charge les opérations dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="a9de6-110">This approach is useful if you want full control of requests to Azure, or if the SDK for your preferred language is not available or doesn't support the operations you need.</span></span>

<span data-ttu-id="a9de6-111">Cet article ne traite pas chaque API exposée dans Azure, mais en utilise certaines comme exemple pour vous montrer comment vous y connecter.</span><span class="sxs-lookup"><span data-stu-id="a9de6-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect to them.</span></span> <span data-ttu-id="a9de6-112">Si vous comprenez les notions de base, vous pouvez lire la [Référence de l’API REST Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) (en anglais) pour trouver des informations détaillées sur la manière d’utiliser les autres API.</span><span class="sxs-lookup"><span data-stu-id="a9de6-112">After you understand the basics, you can read the [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) to find detailed information on how to use the rest of the APIs.</span></span>

## <a name="authentication"></a><span data-ttu-id="a9de6-113">Authentification</span><span class="sxs-lookup"><span data-stu-id="a9de6-113">Authentication</span></span>
<span data-ttu-id="a9de6-114">L’authentification pour Resource Manager est gérée par Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="a9de6-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span></span> <span data-ttu-id="a9de6-115">Pour vous connecter à une API quelconque, vous devez tout d’abord vous authentifier auprès d’Azure AD pour recevoir un jeton d’authentification que vous pouvez transmettre à chaque requête.</span><span class="sxs-lookup"><span data-stu-id="a9de6-115">To connect to any API, you first need to authenticate with Azure AD to receive an authentication token that you can pass on to every request.</span></span> <span data-ttu-id="a9de6-116">Comme nous décrivons un appel pur directement à l’API REST, nous partons du principe que vous ne souhaitez pas vous authentifier en étant invité à entrer un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="a9de6-116">As we are describing a pure call directly to the REST APIs, we assume that you don't want to authenticate by being prompted for a username and password.</span></span> <span data-ttu-id="a9de6-117">Nous supposons également que vous n’utilisez pas les mécanismes d’authentification à deux facteurs.</span><span class="sxs-lookup"><span data-stu-id="a9de6-117">We also assume you are not using two factor authentication mechanisms.</span></span> <span data-ttu-id="a9de6-118">Pour cette raison, nous créons ce que l’on appelle une application Azure AD et un principal du service qui sont utilisés pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="a9de6-118">Therefore, we create what is called an Azure AD Application and a service principal that are used to log in.</span></span> <span data-ttu-id="a9de6-119">Mais n’oubliez pas qu’Azure AD prend en charge plusieurs procédures d’authentification et qu’elles peuvent toutes être utilisées pour récupérer le jeton d’authentification dont nous avons besoin pour les requêtes API ultérieures.</span><span class="sxs-lookup"><span data-stu-id="a9de6-119">But remember that Azure AD support several authentication procedures and all of them could be used to retrieve that authentication token that we need for subsequent API requests.</span></span>
<span data-ttu-id="a9de6-120">Pour connaître la procédure détaillée, suivez les instructions figurant dans [Créer une application Azure AD et un principal du service](resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a9de6-120">Follow [Create Azure AD Application and Service Principal](resource-group-create-service-principal-portal.md) for step by step instructions.</span></span>

### <a name="generating-an-access-token"></a><span data-ttu-id="a9de6-121">Génération d’un jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="a9de6-121">Generating an Access Token</span></span>
<span data-ttu-id="a9de6-122">L’authentification auprès d’Azure AD est effectuée en appelant Azure AD à l’adresse login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="a9de6-122">Authentication against Azure AD is done by calling out to Azure AD, located at login.microsoftonline.com.</span></span> <span data-ttu-id="a9de6-123">Pour vous authentifier, vous devez disposer des informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="a9de6-123">To authenticate, you need to have the following information:</span></span>

* <span data-ttu-id="a9de6-124">l’ID de client Azure AD (le nom de l’Azure AD que vous utilisez pour vous connecter, souvent celui de votre entreprise, mais pas nécessairement) ;</span><span class="sxs-lookup"><span data-stu-id="a9de6-124">Azure AD Tenant ID (the name of that Azure AD you are using to log in, often the same as your company but not necessary)</span></span>
* <span data-ttu-id="a9de6-125">l’ID de l’application (récupéré au cours de l’étape de création de l’application Azure AD) ;</span><span class="sxs-lookup"><span data-stu-id="a9de6-125">Application ID (taken during the Azure AD application creation step)</span></span>
* <span data-ttu-id="a9de6-126">le mot de passe (que vous avez choisi lors de la création de l’application Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a9de6-126">Password (that you selected while creating the Azure AD Application)</span></span>

<span data-ttu-id="a9de6-127">Dans la requête HTTP suivante, veillez à remplacer l’« Azure AD Tenant ID (ID de client Azure AD) », l’« Application ID (ID de l’application) » et le « Password (Mot de passe) » par des valeurs correctes.</span><span class="sxs-lookup"><span data-stu-id="a9de6-127">In the following HTTP request, make sure to replace "Azure AD Tenant ID", "Application ID" and "Password" with the correct values.</span></span>

<span data-ttu-id="a9de6-128">**Requête HTTP générique :**</span><span class="sxs-lookup"><span data-stu-id="a9de6-128">**Generic HTTP Request:**</span></span>

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

<span data-ttu-id="a9de6-129">... générera (une fois l’authentification réussie) une réponse similaire à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="a9de6-129">... will (if authentication succeeds) result in a response similar to the following response:</span></span>

```json
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1448199959",
  "not_before": "1448196059",
  "resource": "https://management.core.windows.net/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhb...86U3JI_0InPUk_lZqWvKiEWsayA"
}
```
<span data-ttu-id="a9de6-130">(L’access_token dans la réponse précédente a été raccourci pour une meilleure lisibilité)</span><span class="sxs-lookup"><span data-stu-id="a9de6-130">(The access_token in the preceding response have been shortened to increase readability)</span></span>

<span data-ttu-id="a9de6-131">**Génération du jeton d’accès à l’aide d’un interpréteur de commandes (Bash) :**</span><span class="sxs-lookup"><span data-stu-id="a9de6-131">**Generating access token using Bash:**</span></span>

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

<span data-ttu-id="a9de6-132">**Génération du jeton d’accès à l’aide de PowerShell :**</span><span class="sxs-lookup"><span data-stu-id="a9de6-132">**Generating access token using PowerShell:**</span></span>

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

<span data-ttu-id="a9de6-133">La réponse contient un jeton d’accès, des informations sur la durée de validité du jeton est valide et sur la ressource pour laquelle vous pouvez utiliser ce jeton.</span><span class="sxs-lookup"><span data-stu-id="a9de6-133">The response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span></span>
<span data-ttu-id="a9de6-134">Le jeton d’accès que vous avez reçu dans le précédent appel HTTP doit être transmis pour toutes les demandes à l’API Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a9de6-134">The access token you received in the previous HTTP call must be passed in for all request to the Resource Manager API.</span></span> <span data-ttu-id="a9de6-135">Vous le transmettez comme une valeur d’en-tête nommée « Authorization » avec la valeur « Bearer YOUR_ACCESS_TOKEN ».</span><span class="sxs-lookup"><span data-stu-id="a9de6-135">You pass it as a header value named "Authorization" with the value "Bearer YOUR_ACCESS_TOKEN".</span></span> <span data-ttu-id="a9de6-136">Notez l’espace entre « Bearer » et votre jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="a9de6-136">Notice the space between "Bearer" and your access token.</span></span>

<span data-ttu-id="a9de6-137">Comme vous pouvez le voir à partir du résultat HTTP ci-dessus, le jeton est valide pendant un délai spécifique au cours duquel vous devez mettre en cache et réutiliser ce même jeton.</span><span class="sxs-lookup"><span data-stu-id="a9de6-137">As you can see from the above HTTP Result, the token is valid for a specific period of time during which you should cache and reuse that same token.</span></span> <span data-ttu-id="a9de6-138">Même s’il est possible de s’authentifier auprès d’Azure AD pour chaque appel d’API, cette procédure serait peu efficace.</span><span class="sxs-lookup"><span data-stu-id="a9de6-138">Even if it is possible to authenticate against Azure AD for each API call, it would be highly inefficient.</span></span>

## <a name="calling-resource-manager-rest-apis"></a><span data-ttu-id="a9de6-139">Appel d'API REST Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a9de6-139">Calling Resource Manager REST APIs</span></span>
<span data-ttu-id="a9de6-140">Cette rubrique utilise uniquement quelques API pour expliquer l’utilisation basique des opérations REST.</span><span class="sxs-lookup"><span data-stu-id="a9de6-140">This topic only uses a few APIs to explain the basic usage of the REST operations.</span></span> <span data-ttu-id="a9de6-141">Pour plus d’informations sur la totalité des opérations, consultez la rubrique [API REST Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="a9de6-141">For information about all the operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span></span>

### <a name="list-all-subscriptions"></a><span data-ttu-id="a9de6-142">Répertorier tous les abonnements</span><span class="sxs-lookup"><span data-stu-id="a9de6-142">List all subscriptions</span></span>
<span data-ttu-id="a9de6-143">L’une des opérations plus simples à exécuter consiste à répertorier les abonnements disponibles auxquels vous pouvez accéder.</span><span class="sxs-lookup"><span data-stu-id="a9de6-143">One of the simplest operations you can do is to list the available subscriptions that you can access.</span></span> <span data-ttu-id="a9de6-144">Dans la requête suivante, vous pouvez voir comment le jeton d’accès est transmis en tant qu’en-tête :</span><span class="sxs-lookup"><span data-stu-id="a9de6-144">In the following request, you see how the access token is passed in as a header:</span></span>

<span data-ttu-id="a9de6-145">(Remplacez YOUR_ACCESS_TOKEN par votre véritable jeton d’accès.)</span><span class="sxs-lookup"><span data-stu-id="a9de6-145">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span></span>

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="a9de6-146">... et vous obtenez comme résultat une liste des abonnements auxquels ce principal du service est autorisé à accéder</span><span class="sxs-lookup"><span data-stu-id="a9de6-146">... and as a result, you get a list of subscriptions that this service principal is allowed to access</span></span>

<span data-ttu-id="a9de6-147">(Les ID d’abonnement ont été raccourcis pour une meilleure lisibilité)</span><span class="sxs-lookup"><span data-stu-id="a9de6-147">(Subscription IDs have been shortened for readability)</span></span>

```json
{
  "value": [
    {
      "id": "/subscriptions/3a8555...555995",
      "subscriptionId": "3a8555...555995",
      "displayName": "Azure Subscription",
      "state": "Enabled",
      "subscriptionPolicies": {
        "locationPlacementId": "Internal_2014-09-01",
        "quotaId": "Internal_2014-09-01"
      }
    }
  ]
}
```

### <a name="list-all-resource-groups-in-a-specific-subscription"></a><span data-ttu-id="a9de6-148">Répertorier tous les groupes de ressources dans un abonnement spécifique</span><span class="sxs-lookup"><span data-stu-id="a9de6-148">List all resource groups in a specific subscription</span></span>
<span data-ttu-id="a9de6-149">Toutes les ressources disponibles avec les API Resource Manager sont imbriquées dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a9de6-149">All resources available with the Resource Manager APIs are nested inside a resource group.</span></span> <span data-ttu-id="a9de6-150">Vous pouvez interroger Resource Manager pour connaître les groupes de ressources existants dans votre abonnement à l’aide de la requête HTTP GET suivante.</span><span class="sxs-lookup"><span data-stu-id="a9de6-150">You can query Resource Manager for existing resource groups in your subscription using the following HTTP GET request.</span></span> <span data-ttu-id="a9de6-151">Notez que, cette fois, l’ID d’abonnement est transmis comme élément de l’URL.</span><span class="sxs-lookup"><span data-stu-id="a9de6-151">Notice how the subscription ID is passed in as part of the URL this time.</span></span>

<span data-ttu-id="a9de6-152">(Remplacez YOUR_ACCESS_TOKEN et SUBSCRIPTION_ID par vos véritables jetons d’accès et ID d’abonnement)</span><span class="sxs-lookup"><span data-stu-id="a9de6-152">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span></span>

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="a9de6-153">La réponse dépend de la définition ou non de groupes de ressources définis et, le cas échéant, de leur nombre.</span><span class="sxs-lookup"><span data-stu-id="a9de6-153">The response you get depends on whether you have any resource groups defined and if so, how many.</span></span>

<span data-ttu-id="a9de6-154">(Les ID d’abonnement ont été raccourcis pour une meilleure lisibilité)</span><span class="sxs-lookup"><span data-stu-id="a9de6-154">(Subscription IDs have been shortened for readability)</span></span>

```json
{
    "value": [
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/myfirstresourcegroup",
            "name": "myfirstresourcegroup",
            "location": "eastus",
            "properties": {
                "provisioningState": "Succeeded"
            }
        },
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/mysecondresourcegroup",
            "name": "mysecondresourcegroup",
            "location": "northeurope",
            "tags": {
                "tagname1": "My first tag"
            },
            "properties": {
                "provisioningState": "Succeeded"
            }
        }
    ]
}
```

### <a name="create-a-resource-group"></a><span data-ttu-id="a9de6-155">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="a9de6-155">Create a resource group</span></span>
<span data-ttu-id="a9de6-156">Jusqu’ici, nous avons interrogé uniquement les API Resource Manager pour obtenir des informations.</span><span class="sxs-lookup"><span data-stu-id="a9de6-156">So far, we've only been querying the Resource Manager APIs for information.</span></span> <span data-ttu-id="a9de6-157">Il est temps de créer des ressources, en commençant par la plus simple de toutes : un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a9de6-157">It's time we create some resources, and let's start by the simplest of them all, a resource group.</span></span> <span data-ttu-id="a9de6-158">La demande HTTP suivante crée un groupe de ressources dans une région/un emplacement de votre choix et y ajoute une balise.</span><span class="sxs-lookup"><span data-stu-id="a9de6-158">The following HTTP request creates a resource group in a region/location of your choice, and adds a tag to it.</span></span>

<span data-ttu-id="a9de6-159">(Remplacez YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID et RESOURCE_GROUP_NAME par votre jeton d’accès réel, votre ID d’abonnement et nom du groupe de ressources à créer)</span><span class="sxs-lookup"><span data-stu-id="a9de6-159">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of the Resource Group you want to create)</span></span>

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  }
}
```

<span data-ttu-id="a9de6-160">Si l’opération réussit, vous obtenez une réponse semblable à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="a9de6-160">If successful, you get a response that is similar to the following response:</span></span>

```json
{
  "id": "/subscriptions/3a8555...555995/resourceGroups/RESOURCE_GROUP_NAME",
  "name": "RESOURCE_GROUP_NAME",
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  },
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<span data-ttu-id="a9de6-161">Vous avez créé un groupe de ressources dans Azure !</span><span class="sxs-lookup"><span data-stu-id="a9de6-161">You've successfully created a resource group in Azure.</span></span> <span data-ttu-id="a9de6-162">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="a9de6-162">Congratulations!</span></span>

### <a name="deploy-resources-to-a-resource-group-using-a-resource-manager-template"></a><span data-ttu-id="a9de6-163">Déployer des ressources dans un groupe de ressources à l’aide d’un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a9de6-163">Deploy resources to a resource group using a Resource Manager Template</span></span>
<span data-ttu-id="a9de6-164">Avec Resource Manager, vous pouvez déployer vos ressources à l’aide de modèles.</span><span class="sxs-lookup"><span data-stu-id="a9de6-164">With Resource Manager, you can deploy your resources using templates.</span></span> <span data-ttu-id="a9de6-165">Un modèle définit plusieurs ressources et leurs dépendances.</span><span class="sxs-lookup"><span data-stu-id="a9de6-165">A template defines several resources and their dependencies.</span></span> <span data-ttu-id="a9de6-166">Pour cette section, nous supposons que vous êtes familiarisé avec les modèles Resource Manager et vous montrons simplement comment effectuer l’appel d’API pour en commencer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="a9de6-166">For this section, we assume you are familiar with Resource Manager templates, and we just show you how to make the API call to start deployment.</span></span> <span data-ttu-id="a9de6-167">Pour en savoir plus sur la création de modèles, voir [Création de modèles Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a9de6-167">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="a9de6-168">Le déploiement d’un modèle ne diffère pas beaucoup de la manière dont vous appelez d’autres API.</span><span class="sxs-lookup"><span data-stu-id="a9de6-168">Deployment of a template doesn't differ much to how you call other APIs.</span></span> <span data-ttu-id="a9de6-169">Un aspect important est le fait que le déploiement d’un modèle peut prendre beaucoup de temps.</span><span class="sxs-lookup"><span data-stu-id="a9de6-169">One important aspect is that deployment of a template can take quite a long time.</span></span> <span data-ttu-id="a9de6-170">L’appel de l’API retourne et c’est à vous, en tant que développeur, de déterminer l’état du déploiement pour savoir à quel moment le déploiement s’effectue.</span><span class="sxs-lookup"><span data-stu-id="a9de6-170">The API call just returns, and it's up to you as developer to query for status of the deployment to find out when the deployment is done.</span></span> <span data-ttu-id="a9de6-171">Pour plus d’informations, consultez la rubrique [Suivre les opérations asynchrones Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="a9de6-171">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>

<span data-ttu-id="a9de6-172">Pour cet exemple, nous utilisons un modèle exposé publiquement disponible sur [GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="a9de6-172">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="a9de6-173">Le modèle que nous utilisons déploie une machine virtuelle Linux pour la région États-Unis de l'Ouest.</span><span class="sxs-lookup"><span data-stu-id="a9de6-173">The template we use deploys a Linux VM to the West US region.</span></span> <span data-ttu-id="a9de6-174">Bien que cet exemple utilise un modèle disponible dans un référentiel public tel que GitHub, vous pouvez transmettre le modèle complet dans le cadre de la requête.</span><span class="sxs-lookup"><span data-stu-id="a9de6-174">Even though this example uses a template available in a public repository like GitHub, you can instead pass the full template as part of the request.</span></span> <span data-ttu-id="a9de6-175">Notez que nous fournissons des valeurs de paramètre dans la requête qui sera utilisée dans le modèle déployé.</span><span class="sxs-lookup"><span data-stu-id="a9de6-175">Note that we provide parameter values in the request that are used inside the deployed template.</span></span>

<span data-ttu-id="a9de6-176">(Remplacez SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME,ADMIN_PASSWORD et DNS_NAME_FOR_PUBLIC_IP par des valeurs appropriées pour votre requête)</span><span class="sxs-lookup"><span data-stu-id="a9de6-176">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP to values appropriate for your request)</span></span>

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME/providers/microsoft.resources/deployments/DEPLOYMENT_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "properties": {
    "templateLink": {
      "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json",
      "contentVersion": "1.0.0.0",
    },
    "mode": "Incremental",
    "parameters": {
        "newStorageAccountName": {
          "value": "GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME"
        },
        "adminUsername": {
          "value": "ADMIN_USER_NAME"
        },
        "adminPassword": {
          "value": "ADMIN_PASSWORD"
        },
        "dnsNameForPublicIP": {
          "value": "DNS_NAME_FOR_PUBLIC_IP"
        },
        "ubuntuOSVersion": {
          "value": "15.04"
        }
    }
  }
}
```

<span data-ttu-id="a9de6-177">La réponse JSON longue pour cette requête a été omise afin d’améliorer la lisibilité de cette documentation.</span><span class="sxs-lookup"><span data-stu-id="a9de6-177">The long JSON response for this request has been omitted to improve readability of this documentation.</span></span> <span data-ttu-id="a9de6-178">La réponse contient des informations sur le déploiement basé sur un modèle que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="a9de6-178">The response contains information about the templated deployment that you created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9de6-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a9de6-179">Next steps</span></span>

- <span data-ttu-id="a9de6-180">Pour en savoir plus sur la gestion des opérations REST asynchrones, consultez [Suivre les opérations asynchrones Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="a9de6-180">To learn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
