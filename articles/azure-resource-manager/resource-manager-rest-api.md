---
title: "API REST du Gestionnaire d’aaaResource | Documents Microsoft"
description: "Une vue d’ensemble de hello authentification de l’API REST du Gestionnaire de ressources et des exemples d’utilisation"
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
ms.openlocfilehash: 3ccc3575c5e06c41f2fdc5317711980fc6a2f649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-manager-rest-apis"></a><span data-ttu-id="4c8d7-103">API REST Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4c8d7-103">Resource Manager REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c8d7-104">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c8d7-104">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="4c8d7-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="4c8d7-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="4c8d7-106">Portail</span><span class="sxs-lookup"><span data-stu-id="4c8d7-106">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="4c8d7-107">API REST</span><span class="sxs-lookup"><span data-stu-id="4c8d7-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="4c8d7-108">Derrière chaque tooAzure d’appel de gestionnaire de ressources derrière chaque modèle déployé, derrière chaque compte de stockage configurés sont les API RESTful un ou plusieurs appels toohello Azure du Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-108">Behind every call tooAzure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls toohello Azure Resource Manager's RESTful API.</span></span> <span data-ttu-id="4c8d7-109">Cette rubrique est consacrée toothose API et comment vous pouvez les appeler sans utiliser un kit de développement logiciel du tout.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-109">This topic is devoted toothose APIs and how you can call them without using any SDK at all.</span></span> <span data-ttu-id="4c8d7-110">Cette approche est utile si vous souhaitez que le contrôle total de demandes tooAzure ou si hello Kit de développement logiciel pour votre langue par défaut n’est pas disponible ou ne prend pas en charge les opérations que vous devez hello.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-110">This approach is useful if you want full control of requests tooAzure, or if hello SDK for your preferred language is not available or doesn't support hello operations you need.</span></span>

<span data-ttu-id="4c8d7-111">Cet article ne passe pas par le biais des API qui sont exposée dans Azure, mais qu’il utilise certaines opérations sont des exemples de la façon dont vous vous connectez toothem.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect toothem.</span></span> <span data-ttu-id="4c8d7-112">Une fois que vous comprenez les notions de base hello, vous pouvez lire hello [référence d’API REST Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) toofind des informations détaillées sur comment reste hello toouse hello API.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-112">After you understand hello basics, you can read hello [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) toofind detailed information on how toouse hello rest of hello APIs.</span></span>

## <a name="authentication"></a><span data-ttu-id="4c8d7-113">Authentification</span><span class="sxs-lookup"><span data-stu-id="4c8d7-113">Authentication</span></span>
<span data-ttu-id="4c8d7-114">L’authentification pour Resource Manager est gérée par Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="4c8d7-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span></span> <span data-ttu-id="4c8d7-115">tooconnect tooany API, vous devez tout d’abord tooauthenticate avec Azure AD tooreceive un jeton d’authentification que vous pouvez passer à la demande de tooevery.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-115">tooconnect tooany API, you first need tooauthenticate with Azure AD tooreceive an authentication token that you can pass on tooevery request.</span></span> <span data-ttu-id="4c8d7-116">Comme nous décrivons un appel pur directement toohello API REST, nous partons du principe que vous ne souhaitez pas tooauthenticate à être invité à entrer un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-116">As we are describing a pure call directly toohello REST APIs, we assume that you don't want tooauthenticate by being prompted for a username and password.</span></span> <span data-ttu-id="4c8d7-117">Nous supposons également que vous n’utilisez pas les mécanismes d’authentification à deux facteurs.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-117">We also assume you are not using two factor authentication mechanisms.</span></span> <span data-ttu-id="4c8d7-118">Par conséquent, nous créons ce que l'on appelle une Application Azure AD et un principal de service qui sont utilisé toolog dans.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-118">Therefore, we create what is called an Azure AD Application and a service principal that are used toolog in.</span></span> <span data-ttu-id="4c8d7-119">Mais rappelez-vous que Azure AD prend en charge plusieurs procédures d’authentification et tous les peut être utilisé tooretrieve ce jeton d’authentification nécessaire pour les demandes API suivantes.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-119">But remember that Azure AD support several authentication procedures and all of them could be used tooretrieve that authentication token that we need for subsequent API requests.</span></span>
<span data-ttu-id="4c8d7-120">Pour connaître la procédure détaillée, suivez les instructions figurant dans [Créer une application Azure AD et un principal du service](resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4c8d7-120">Follow [Create Azure AD Application and Service Principal](resource-group-create-service-principal-portal.md) for step by step instructions.</span></span>

### <a name="generating-an-access-token"></a><span data-ttu-id="4c8d7-121">Génération d’un jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="4c8d7-121">Generating an Access Token</span></span>
<span data-ttu-id="4c8d7-122">L’authentification auprès d’Azure AD est effectuée en appelant tooAzure AD, situé à login.microsoftonline.com. tooauthenticate, vous devez hello toohave informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4c8d7-122">Authentication against Azure AD is done by calling out tooAzure AD, located at login.microsoftonline.com. tooauthenticate, you need toohave hello following information:</span></span>

* <span data-ttu-id="4c8d7-123">ID de locataire Azure AD (hello nom de qu’Azure AD à l’aide de toolog dans, souvent hello identique à votre entreprise mais n’est pas nécessaire)</span><span class="sxs-lookup"><span data-stu-id="4c8d7-123">Azure AD Tenant ID (hello name of that Azure AD you are using toolog in, often hello same as your company but not necessary)</span></span>
* <span data-ttu-id="4c8d7-124">ID d’application (effectuée au cours de l’étape de la création de l’application hello Azure AD)</span><span class="sxs-lookup"><span data-stu-id="4c8d7-124">Application ID (taken during hello Azure AD application creation step)</span></span>
* <span data-ttu-id="4c8d7-125">Mot de passe (que vous avez sélectionné lors de la création de hello Application Azure AD)</span><span class="sxs-lookup"><span data-stu-id="4c8d7-125">Password (that you selected while creating hello Azure AD Application)</span></span>

<span data-ttu-id="4c8d7-126">Bonjour suivant la requête HTTP, assurez-vous que tooreplace « ID de locataire Azure AD, » « ID d’Application » et « Password » avec les valeurs correctes hello.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-126">In hello following HTTP request, make sure tooreplace "Azure AD Tenant ID", "Application ID" and "Password" with hello correct values.</span></span>

<span data-ttu-id="4c8d7-127">**Requête HTTP générique :**</span><span class="sxs-lookup"><span data-stu-id="4c8d7-127">**Generic HTTP Request:**</span></span>

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

<span data-ttu-id="4c8d7-128">... va (si l’authentification réussit) entraîne un toohello similaire de réponse suivant la réponse :</span><span class="sxs-lookup"><span data-stu-id="4c8d7-128">... will (if authentication succeeds) result in a response similar toohello following response:</span></span>

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
<span data-ttu-id="4c8d7-129">(access_token hello Bonjour précédant la réponse ont été raccourcie tooincrease lisibilité)</span><span class="sxs-lookup"><span data-stu-id="4c8d7-129">(hello access_token in hello preceding response have been shortened tooincrease readability)</span></span>

<span data-ttu-id="4c8d7-130">**Génération du jeton d’accès à l’aide d’un interpréteur de commandes (Bash) :**</span><span class="sxs-lookup"><span data-stu-id="4c8d7-130">**Generating access token using Bash:**</span></span>

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

<span data-ttu-id="4c8d7-131">**Génération du jeton d’accès à l’aide de PowerShell :**</span><span class="sxs-lookup"><span data-stu-id="4c8d7-131">**Generating access token using PowerShell:**</span></span>

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

<span data-ttu-id="4c8d7-132">Hello réponse contient un jeton d’accès, d’informations sur la durée pendant laquelle ce jeton est valide et plus d’informations sur la ressource que vous pouvez utiliser ce jeton pour.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-132">hello response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span></span>
<span data-ttu-id="4c8d7-133">jeton d’accès Hello que vous avez reçu dans l’appel HTTP de la précédente hello doit être transmise pour toohello demande toutes les API du Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-133">hello access token you received in hello previous HTTP call must be passed in for all request toohello Resource Manager API.</span></span> <span data-ttu-id="4c8d7-134">Passez-le en tant qu’une valeur d’en-tête nommée « Authorization » avec la valeur de hello « Support YOUR_ACCESS_TOKEN ».</span><span class="sxs-lookup"><span data-stu-id="4c8d7-134">You pass it as a header value named "Authorization" with hello value "Bearer YOUR_ACCESS_TOKEN".</span></span> <span data-ttu-id="4c8d7-135">Notez l’espace hello entre « Support » et votre jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-135">Notice hello space between "Bearer" and your access token.</span></span>

<span data-ttu-id="4c8d7-136">Comme vous pouvez voir à partir de hello ci-dessus HTTP, jeton de hello est valide pour une période spécifique au cours de laquelle vous devez mettre en cache et réutiliser ce même jeton.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-136">As you can see from hello above HTTP Result, hello token is valid for a specific period of time during which you should cache and reuse that same token.</span></span> <span data-ttu-id="4c8d7-137">Même s’il est possible tooauthenticate auprès d’Azure AD pour chaque appel d’API, il est peu efficace.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-137">Even if it is possible tooauthenticate against Azure AD for each API call, it would be highly inefficient.</span></span>

## <a name="calling-resource-manager-rest-apis"></a><span data-ttu-id="4c8d7-138">Appel d'API REST Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4c8d7-138">Calling Resource Manager REST APIs</span></span>
<span data-ttu-id="4c8d7-139">Cette rubrique utilise uniquement quelques API tooexplain hello l’utilisation de base des opérations REST de hello.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-139">This topic only uses a few APIs tooexplain hello basic usage of hello REST operations.</span></span> <span data-ttu-id="4c8d7-140">Pour plus d’informations sur toutes les opérations de hello, consultez [API REST de Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="4c8d7-140">For information about all hello operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span></span>

### <a name="list-all-subscriptions"></a><span data-ttu-id="4c8d7-141">Répertorier tous les abonnements</span><span class="sxs-lookup"><span data-stu-id="4c8d7-141">List all subscriptions</span></span>
<span data-ttu-id="4c8d7-142">Une des opérations de la plus simple de hello que faire est toolist hello disponibles les abonnements auxquels vous pouvez accéder.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-142">One of hello simplest operations you can do is toolist hello available subscriptions that you can access.</span></span> <span data-ttu-id="4c8d7-143">Bonjour demande, vous consultez Comment jeton d’accès hello est passée comme un en-tête de :</span><span class="sxs-lookup"><span data-stu-id="4c8d7-143">In hello following request, you see how hello access token is passed in as a header:</span></span>

<span data-ttu-id="4c8d7-144">(Remplacez YOUR_ACCESS_TOKEN par votre véritable jeton d’accès.)</span><span class="sxs-lookup"><span data-stu-id="4c8d7-144">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span></span>

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="4c8d7-145">... et par conséquent, vous obtenez une liste des abonnements que ce principal du service est autorisé tooaccess</span><span class="sxs-lookup"><span data-stu-id="4c8d7-145">... and as a result, you get a list of subscriptions that this service principal is allowed tooaccess</span></span>

<span data-ttu-id="4c8d7-146">(Les ID d’abonnement ont été raccourcis pour une meilleure lisibilité)</span><span class="sxs-lookup"><span data-stu-id="4c8d7-146">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="list-all-resource-groups-in-a-specific-subscription"></a><span data-ttu-id="4c8d7-147">Répertorier tous les groupes de ressources dans un abonnement spécifique</span><span class="sxs-lookup"><span data-stu-id="4c8d7-147">List all resource groups in a specific subscription</span></span>
<span data-ttu-id="4c8d7-148">Toutes les ressources disponibles avec les API du Gestionnaire de ressources de hello sont imbriqués à l’intérieur d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-148">All resources available with hello Resource Manager APIs are nested inside a resource group.</span></span> <span data-ttu-id="4c8d7-149">Vous pouvez interroger le Gestionnaire de ressources pour les groupes de ressources existants dans votre abonnement à l’aide de hello suivant demande HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-149">You can query Resource Manager for existing resource groups in your subscription using hello following HTTP GET request.</span></span> <span data-ttu-id="4c8d7-150">Notez comment hello ID d’abonnement est passé en tant que partie de l’URL de hello instant.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-150">Notice how hello subscription ID is passed in as part of hello URL this time.</span></span>

<span data-ttu-id="4c8d7-151">(Remplacez YOUR_ACCESS_TOKEN et SUBSCRIPTION_ID par vos véritables jetons d’accès et ID d’abonnement)</span><span class="sxs-lookup"><span data-stu-id="4c8d7-151">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span></span>

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="4c8d7-152">Hello réponse varie selon que vous disposez d’aucun groupe de ressources défini et si tel est le cas, combien.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-152">hello response you get depends on whether you have any resource groups defined and if so, how many.</span></span>

<span data-ttu-id="4c8d7-153">(Les ID d’abonnement ont été raccourcis pour une meilleure lisibilité)</span><span class="sxs-lookup"><span data-stu-id="4c8d7-153">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="create-a-resource-group"></a><span data-ttu-id="4c8d7-154">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="4c8d7-154">Create a resource group</span></span>
<span data-ttu-id="4c8d7-155">Jusqu'à présent, nous avons été interrogeant uniquement hello API du Gestionnaire de ressources pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-155">So far, we've only been querying hello Resource Manager APIs for information.</span></span> <span data-ttu-id="4c8d7-156">Il est temps de créer des ressources et nous commençons par hello plus simple d'entre eux tous, un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-156">It's time we create some resources, and let's start by hello simplest of them all, a resource group.</span></span> <span data-ttu-id="4c8d7-157">Hello requête HTTP suivante crée un groupe de ressources dans une région de votre choix et ajoute un tooit de balise.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-157">hello following HTTP request creates a resource group in a region/location of your choice, and adds a tag tooit.</span></span>

<span data-ttu-id="4c8d7-158">(Remplacez YOUR_ACCESS_TOKEN, ID_ABONNEMENT, nom_groupe_ressource avec votre réel jeton d’accès, ID d’abonnement et le nom de groupe de ressources que vous voulez toocreate de hello)</span><span class="sxs-lookup"><span data-stu-id="4c8d7-158">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of hello Resource Group you want toocreate)</span></span>

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

<span data-ttu-id="4c8d7-159">En cas de réussite, vous obtenez une réponse similaire toohello suivant la réponse :</span><span class="sxs-lookup"><span data-stu-id="4c8d7-159">If successful, you get a response that is similar toohello following response:</span></span>

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

<span data-ttu-id="4c8d7-160">Vous avez créé un groupe de ressources dans Azure !</span><span class="sxs-lookup"><span data-stu-id="4c8d7-160">You've successfully created a resource group in Azure.</span></span> <span data-ttu-id="4c8d7-161">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="4c8d7-161">Congratulations!</span></span>

### <a name="deploy-resources-tooa-resource-group-using-a-resource-manager-template"></a><span data-ttu-id="4c8d7-162">Déployer le groupe de ressources tooa de ressources à l’aide d’un modèle de gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="4c8d7-162">Deploy resources tooa resource group using a Resource Manager Template</span></span>
<span data-ttu-id="4c8d7-163">Avec Resource Manager, vous pouvez déployer vos ressources à l’aide de modèles.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-163">With Resource Manager, you can deploy your resources using templates.</span></span> <span data-ttu-id="4c8d7-164">Un modèle définit plusieurs ressources et leurs dépendances.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-164">A template defines several resources and their dependencies.</span></span> <span data-ttu-id="4c8d7-165">Dans cette section, nous supposons que vous êtes familiarisé avec les modèles de gestionnaire de ressources, et nous vous montrer comment toomake hello API appeler toostart déploiement.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-165">For this section, we assume you are familiar with Resource Manager templates, and we just show you how toomake hello API call toostart deployment.</span></span> <span data-ttu-id="4c8d7-166">Pour en savoir plus sur la création de modèles, voir [Création de modèles Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4c8d7-166">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="4c8d7-167">Déploiement d’un modèle ne diffère beaucoup toohow vous appelez d’autres API.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-167">Deployment of a template doesn't differ much toohow you call other APIs.</span></span> <span data-ttu-id="4c8d7-168">Un aspect important est le fait que le déploiement d’un modèle peut prendre beaucoup de temps.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-168">One important aspect is that deployment of a template can take quite a long time.</span></span> <span data-ttu-id="4c8d7-169">appel d’API de Hello retourne simplement et c’est tooyou comme tooquery de développeur pour l’état de toofind de déploiement hello out fois hello déploiement terminé.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-169">hello API call just returns, and it's up tooyou as developer tooquery for status of hello deployment toofind out when hello deployment is done.</span></span> <span data-ttu-id="4c8d7-170">Pour plus d’informations, consultez la rubrique [Suivre les opérations asynchrones Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="4c8d7-170">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>

<span data-ttu-id="4c8d7-171">Pour cet exemple, nous utilisons un modèle exposé publiquement disponible sur [GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="4c8d7-171">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="4c8d7-172">modèle Hello que nous utilisons déploie une région ouest des États-Unis de toohello Linux VM.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-172">hello template we use deploys a Linux VM toohello West US region.</span></span> <span data-ttu-id="4c8d7-173">Bien que cet exemple utilise un modèle disponible dans un référentiel public comme GitHub, vous pouvez passer à la place les modèle complet de hello dans le cadre de la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-173">Even though this example uses a template available in a public repository like GitHub, you can instead pass hello full template as part of hello request.</span></span> <span data-ttu-id="4c8d7-174">Notez que nous fournissons des valeurs de paramètre dans la demande de hello qui servent à l’intérieur de hello déployé le modèle.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-174">Note that we provide parameter values in hello request that are used inside hello deployed template.</span></span>

<span data-ttu-id="4c8d7-175">(Remplacez toovalues ID_ABONNEMENT, nom_groupe_ressource, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD et DNS_NAME_FOR_PUBLIC_IP appropriés pour votre demande)</span><span class="sxs-lookup"><span data-stu-id="4c8d7-175">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP toovalues appropriate for your request)</span></span>

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

<span data-ttu-id="4c8d7-176">Hello temps de réponse JSON pour cette demande a été lisibilité tooimprove omis de cette documentation.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-176">hello long JSON response for this request has been omitted tooimprove readability of this documentation.</span></span> <span data-ttu-id="4c8d7-177">réponse de Hello contient des informations sur le déploiement basé sur un modèle hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="4c8d7-177">hello response contains information about hello templated deployment that you created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c8d7-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4c8d7-178">Next steps</span></span>

- <span data-ttu-id="4c8d7-179">toolearn sur la gestion des opérations asynchrones de REST, consultez [le suivi des opérations asynchrones Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="4c8d7-179">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
