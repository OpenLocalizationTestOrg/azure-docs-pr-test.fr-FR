---
title: API REST de recherche de journal Log Analytics | Microsoft Docs
description: "Ce guide fournit un didacticiel de base qui décrit comment utiliser l’API REST de recherche Log Analytics dans Operations Management Suite (OMS). Il propose aussi des exemples qui vous permettent de découvrir comment utiliser les commandes."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: b4e9ebe8-80f0-418e-a855-de7954668df7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 78afb2f065dde4a3e7a3ab787c939b3c52b72cc6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="log-analytics-log-search-rest-api"></a><span data-ttu-id="8d240-103">API REST de recherche de journal Log Analytics</span><span class="sxs-lookup"><span data-stu-id="8d240-103">Log Analytics log search REST API</span></span>
<span data-ttu-id="8d240-104">Ce guide fournit un didacticiel de base, y compris des exemples, sur la façon dont vous pouvez utiliser l’API REST de recherche de journal Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8d240-104">This guide provides a basic tutorial, including examples, of how you can use the Log Analytics Search REST API.</span></span> <span data-ttu-id="8d240-105">Log Analytics fait partie d'Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="8d240-105">Log Analytics is part of the Operations Management Suite (OMS).</span></span>

> [!NOTE]
> <span data-ttu-id="8d240-106">Si votre espace de travail a été mis à niveau avec le [nouveau langage de requête Log Analytics](log-analytics-log-search-upgrade.md), vous devez continuer à utiliser le langage de requête existant avec l’API de recherche dans les journaux, comme indiqué dans cet article.</span><span class="sxs-lookup"><span data-stu-id="8d240-106">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should continue to use the legacy query language with the log search API as described in this article.</span></span>  <span data-ttu-id="8d240-107">Une nouvelle API sera publiée pour les espaces de travail mis à niveau, et la documentation sera mise à jour à ce moment-là.</span><span class="sxs-lookup"><span data-stu-id="8d240-107">A new API will be released for upgraded workspaces, and the documentation will be updated at that time.</span></span> 

> [!NOTE]
> <span data-ttu-id="8d240-108">Avant, Log Analytics s’appelait Operational Insights, ce qui explique pourquoi ce nom est présent dans le fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="8d240-108">Log Analytics was previously called Operational Insights, which is why it is the name used in the resource provider.</span></span>
>
>

## <a name="overview-of-the-log-search-rest-api"></a><span data-ttu-id="8d240-109">Vue d’ensemble de l’API REST de recherche de journal</span><span class="sxs-lookup"><span data-stu-id="8d240-109">Overview of the Log Search REST API</span></span>
<span data-ttu-id="8d240-110">L’API REST de recherche Log Analytics est un service RESTful qui est accessible par le biais de l’API Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8d240-110">The Log Analytics Search REST API is RESTful and can be accessed via the Azure Resource Manager API.</span></span> <span data-ttu-id="8d240-111">Cet article fournit des exemples qui vous indiqueront comment accéder à l'API via [ARMClient](https://github.com/projectkudu/ARMClient), un outil de ligne de commande open source qui simplifie l'appel de l'API du Gestionnaire de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="8d240-111">This article provides examples of accessing the API through [ARMClient](https://github.com/projectkudu/ARMClient), an open source command-line tool that simplifies invoking the Azure Resource Manager API.</span></span> <span data-ttu-id="8d240-112">L'utilisation d’ARMClient est une des nombreuses options vous permettant d’accéder à l'API de recherche de journal de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="8d240-112">The use of ARMClient is one of many options to access the Log Analytics Search API.</span></span> <span data-ttu-id="8d240-113">Une autre option consiste à utiliser le module Azure PowerShell pour OperationalInsights qui inclut des applets de commande pour accéder à la recherche.</span><span class="sxs-lookup"><span data-stu-id="8d240-113">Another option is to use the Azure PowerShell module for OperationalInsights, which includes cmdlets for accessing search.</span></span> <span data-ttu-id="8d240-114">Grâce à ces outils, vous pouvez utiliser l'API Azure Resource Manager pour effectuer des appels vers les espaces de travail OMS et exécuter en leur sein des commandes de recherche.</span><span class="sxs-lookup"><span data-stu-id="8d240-114">With these tools, you can utilize the Azure Resource Manager API to make calls to OMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="8d240-115">L'API produit des résultats de recherche au format JSON, qui vous permet d'utiliser ces résultats, par programme, de différentes manières.</span><span class="sxs-lookup"><span data-stu-id="8d240-115">The API outputs search results in JSON format, allowing you to use the search results in many different ways programmatically.</span></span>

<span data-ttu-id="8d240-116">Le Gestionnaire de ressources Azure peut être utilisé via une [Bibliothèque pour .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) et l'[API REST](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span><span class="sxs-lookup"><span data-stu-id="8d240-116">The Azure Resource Manager can be used via a [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) and the [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span></span> <span data-ttu-id="8d240-117">Pour en savoir plus, consultez les pages web connexes.</span><span class="sxs-lookup"><span data-stu-id="8d240-117">To learn more, review the linked web pages.</span></span>

> [!NOTE]
> <span data-ttu-id="8d240-118">Si vous utilisez une commande d’agrégation comme `|measure count()` ou `distinct`, chaque appel à la recherche peut retourner jusqu'à 500 000 enregistrements.</span><span class="sxs-lookup"><span data-stu-id="8d240-118">If you use an aggregation command such as `|measure count()` or `distinct`, each call to search can return upto 500,000 records.</span></span> <span data-ttu-id="8d240-119">Les recherches qui n’incluent pas une commande d’agrégation renvoient jusqu'à 5 000 enregistrements.</span><span class="sxs-lookup"><span data-stu-id="8d240-119">Searches that do not include an aggregation command return upto 5,000 records.</span></span>
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a><span data-ttu-id="8d240-120">Didacticiel de base sur l’API de recherche de journal de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="8d240-120">Basic Log Analytics Search REST API tutorial</span></span>
### <a name="to-use-armclient"></a><span data-ttu-id="8d240-121">Pour utiliser ARMClient</span><span class="sxs-lookup"><span data-stu-id="8d240-121">To use ARMClient</span></span>
1. <span data-ttu-id="8d240-122">Installez [Chocolatey](https://chocolatey.org/)(gestionnaire de packages open source pour Windows).</span><span class="sxs-lookup"><span data-stu-id="8d240-122">Install [Chocolatey](https://chocolatey.org/), which is an Open Source Package Manager for Windows.</span></span> <span data-ttu-id="8d240-123">Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur, puis exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8d240-123">Open a command prompt window as administrator and then run the following command:</span></span>

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. <span data-ttu-id="8d240-124">Installez ARMClient en exécutant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8d240-124">Install ARMClient by running the following command:</span></span>

    ```
    choco install armclient
    ```

### <a name="to-perform-a-search-using-armclient"></a><span data-ttu-id="8d240-125">Pour effectuer une recherche à l’aide d’ARMClient</span><span class="sxs-lookup"><span data-stu-id="8d240-125">To perform a search using ARMClient</span></span>
1. <span data-ttu-id="8d240-126">Connectez-vous à l’aide de votre compte Microsoft, ou de votre compte professionnel ou scolaire :</span><span class="sxs-lookup"><span data-stu-id="8d240-126">Log in using your Microsoft account or your work or school account:</span></span>

    ```
    armclient login
    ```

    <span data-ttu-id="8d240-127">Une connexion réussie répertorie tous les abonnements associés au compte spécifique :</span><span class="sxs-lookup"><span data-stu-id="8d240-127">A successful login lists all subscriptions tied to the given account:</span></span>

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. <span data-ttu-id="8d240-128">Obtenez les espaces de travail Operations Management Suite :</span><span class="sxs-lookup"><span data-stu-id="8d240-128">Get the Operations Management Suite workspaces:</span></span>

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    <span data-ttu-id="8d240-129">Un appel Get réussi affiche tous les espaces de travail liés à l’abonnement :</span><span class="sxs-lookup"><span data-stu-id="8d240-129">A successful Get call would output all workspaces tied to the subscription:</span></span>

    ```
    {
    "value": [
    {
      "properties": {
    "source": "External",
    "customerId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "portalUrl": "https://eus.login.mms.microsoft.com/SignIn.aspx?returnUrl=https%3a%2f%2feus.mms.microsoft.com%2fMain.aspx%3fcid%xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
      },
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/{WORKSPACE NAME}",
      "name": "{WORKSPACE NAME}",
      "type": "Microsoft.OperationalInsights/workspaces",
      "location": "East US"
       ]
    }
    ```
3. <span data-ttu-id="8d240-130">Créez votre variable de recherche :</span><span class="sxs-lookup"><span data-stu-id="8d240-130">Create your search variable:</span></span>

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. <span data-ttu-id="8d240-131">Lancez une recherche à l’aide de votre nouvelle variable de recherche :</span><span class="sxs-lookup"><span data-stu-id="8d240-131">Search using your new search variable:</span></span>

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a><span data-ttu-id="8d240-132">Exemples de référence de l’API REST de recherche Log Analytics</span><span class="sxs-lookup"><span data-stu-id="8d240-132">Log Analytics Search REST API reference examples</span></span>
<span data-ttu-id="8d240-133">Les exemples suivants vous expliquent comment utiliser l'API de recherche.</span><span class="sxs-lookup"><span data-stu-id="8d240-133">The following examples show you how you can use the Search API.</span></span>

### <a name="search---actionread"></a><span data-ttu-id="8d240-134">Recherche - Action/lecture</span><span class="sxs-lookup"><span data-stu-id="8d240-134">Search - Action/Read</span></span>
<span data-ttu-id="8d240-135">**Exemple d’URL :**</span><span class="sxs-lookup"><span data-stu-id="8d240-135">**Sample Url:**</span></span>

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

<span data-ttu-id="8d240-136">**Requête :**</span><span class="sxs-lookup"><span data-stu-id="8d240-136">**Request:**</span></span>

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```
<span data-ttu-id="8d240-137">Le tableau suivant décrit les propriétés qui sont disponibles</span><span class="sxs-lookup"><span data-stu-id="8d240-137">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="8d240-138">**Propriété**</span><span class="sxs-lookup"><span data-stu-id="8d240-138">**Property**</span></span> | <span data-ttu-id="8d240-139">**Description**</span><span class="sxs-lookup"><span data-stu-id="8d240-139">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="8d240-140">top</span><span class="sxs-lookup"><span data-stu-id="8d240-140">top</span></span> |<span data-ttu-id="8d240-141">Le nombre maximal de résultats à renvoyer.</span><span class="sxs-lookup"><span data-stu-id="8d240-141">The maximum number of results to return.</span></span> |
| <span data-ttu-id="8d240-142">highlight</span><span class="sxs-lookup"><span data-stu-id="8d240-142">highlight</span></span> |<span data-ttu-id="8d240-143">Contient des pré- et post-paramètres, utilisés généralement pour mettre en surbrillance les champs de correspondance</span><span class="sxs-lookup"><span data-stu-id="8d240-143">Contains pre and post parameters, used usually for highlighting matching fields</span></span> |
| <span data-ttu-id="8d240-144">pre</span><span class="sxs-lookup"><span data-stu-id="8d240-144">pre</span></span> |<span data-ttu-id="8d240-145">Préfixe la chaîne spécifique à vos champs correspondants.</span><span class="sxs-lookup"><span data-stu-id="8d240-145">Prefixes the given string to your matched fields.</span></span> |
| <span data-ttu-id="8d240-146">post</span><span class="sxs-lookup"><span data-stu-id="8d240-146">post</span></span> |<span data-ttu-id="8d240-147">Ajoute la chaîne spécifique à vos champs correspondants.</span><span class="sxs-lookup"><span data-stu-id="8d240-147">Appends the given string to your matched fields.</span></span> |
| <span data-ttu-id="8d240-148">query</span><span class="sxs-lookup"><span data-stu-id="8d240-148">query</span></span> |<span data-ttu-id="8d240-149">La requête de recherche utilisée pour recueillir et renvoyer des résultats.</span><span class="sxs-lookup"><span data-stu-id="8d240-149">The search query used to collect and return results.</span></span> |
| <span data-ttu-id="8d240-150">start</span><span class="sxs-lookup"><span data-stu-id="8d240-150">start</span></span> |<span data-ttu-id="8d240-151">Le début de la plage horaire à partir de laquelle vous souhaitez obtenir des résultats.</span><span class="sxs-lookup"><span data-stu-id="8d240-151">The beginning of the time window you want results to be found from.</span></span> |
| <span data-ttu-id="8d240-152">end</span><span class="sxs-lookup"><span data-stu-id="8d240-152">end</span></span> |<span data-ttu-id="8d240-153">La fin de la plage horaire à partir de laquelle vous souhaitez obtenir des résultats.</span><span class="sxs-lookup"><span data-stu-id="8d240-153">The end of the time window you want results to be found from.</span></span> |

<span data-ttu-id="8d240-154">**Réponse :**</span><span class="sxs-lookup"><span data-stu-id="8d240-154">**Response:**</span></span>

```
    {
      "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "__metadata" : {
        "resultType" : "raw",
        "total" : 1455,
        "top" : 150,
        "StartTime" : "2015-02-11T21:09:07.0345815Z",
        "Status" : "Successful",
        "LastUpdated" : "2015-02-11T21:09:07.331463Z",
        "CoreResponses" : [],
        "sort" : [{
          "name" : "TimeGenerated",
          "order" : "desc"
        }],
        "requestTime" : 450
      },
      "value": [{
        "SourceSystem" : "OpsManager",
        "TimeGenerated" : "2015-02-07T14:07:33Z",
        "Source" : "SideBySide",
        "EventLog" : "Application",
        "Computer" : "BAMBAM",
        "EventCategory" : 0,
        "EventLevel" : 1,
        "EventLevelName" : "Error",
        "UserName" : "N/A",
        "EventID" : 78,
        "MG" : "00000000-0000-0000-0000-000000000001",
        "TimeCollected" : "2015-02-07T14:10:04.69Z",
        "ManagementGroupName" : "AOI-5bf9a37f-e841-462b-80d2-1d19cd97dc40",
        "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "Type" : "Event",
        "__metadata" : {
          "Type" : "Event",
          "TimeGenerated" : "2015-02-07T14:07:33Z",
          "highlighting" : {
          "EventLevelName" : ["{[hl]}Error{[/hl]}"]
        }
      }]
    ],
            "start" : "2015-02-04T21:03:29.231Z",
            "end" : "2015-02-11T21:03:29.231Z"
          }
        }
      }]
    }
```

### <a name="searchid---actionread"></a><span data-ttu-id="8d240-155">Recherche/{ID} - Action/lecture</span><span class="sxs-lookup"><span data-stu-id="8d240-155">Search/{ID} - Action/Read</span></span>
<span data-ttu-id="8d240-156">**Demander le contenu d'une recherche enregistrée :**</span><span class="sxs-lookup"><span data-stu-id="8d240-156">**Request the contents of a Saved Search:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> <span data-ttu-id="8d240-157">Si la recherche renvoie un état « En attente », une interrogation des résultats mis à jour peut alors être réalisée via cette API.</span><span class="sxs-lookup"><span data-stu-id="8d240-157">If the search returns with a ‘Pending’ status, then polling the updated results can be done through this API.</span></span> <span data-ttu-id="8d240-158">Après 6 minutes, le résultat de la recherche est supprimé du cache et HTTP Gone est retourné.</span><span class="sxs-lookup"><span data-stu-id="8d240-158">After 6 min, the result of the search will be dropped from the cache and HTTP Gone will be returned.</span></span> <span data-ttu-id="8d240-159">Si la demande de recherche initiale retourne immédiatement un état « Succès », les résultats ne sont pas ajoutés au cache, ce qui signifie que cette API retourne HTTP Gone si elle est interrogée.</span><span class="sxs-lookup"><span data-stu-id="8d240-159">If the initial search request returns a ‘Successful’ status immediately, the results are not added to the cache causing this API to return HTTP Gone if queried.</span></span> <span data-ttu-id="8d240-160">Le contenu d’un résultat HTTP 200 est présenté dans le même format que la demande de recherche initiale. Toutefois, les valeurs sont mises à jour.</span><span class="sxs-lookup"><span data-stu-id="8d240-160">The contents of an HTTP 200 result are in the same format as the initial search request just with updated values.</span></span>
>
>

### <a name="saved-searches"></a><span data-ttu-id="8d240-161">Recherches enregistrées</span><span class="sxs-lookup"><span data-stu-id="8d240-161">Saved searches</span></span>
<span data-ttu-id="8d240-162">**Demander la liste des recherches enregistrées :**</span><span class="sxs-lookup"><span data-stu-id="8d240-162">**Request List of Saved Searches:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

<span data-ttu-id="8d240-163">Méthodes prises en charge : GET PUT DELETE</span><span class="sxs-lookup"><span data-stu-id="8d240-163">Supported methods: GET PUT DELETE</span></span>

<span data-ttu-id="8d240-164">Méthodes de collection prises en charge : GET</span><span class="sxs-lookup"><span data-stu-id="8d240-164">Supported collection methods: GET</span></span>

<span data-ttu-id="8d240-165">Le tableau suivant décrit les propriétés qui sont disponibles</span><span class="sxs-lookup"><span data-stu-id="8d240-165">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="8d240-166">Propriété</span><span class="sxs-lookup"><span data-stu-id="8d240-166">Property</span></span> | <span data-ttu-id="8d240-167">Description</span><span class="sxs-lookup"><span data-stu-id="8d240-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8d240-168">ID</span><span class="sxs-lookup"><span data-stu-id="8d240-168">Id</span></span> |<span data-ttu-id="8d240-169">Identificateur unique.</span><span class="sxs-lookup"><span data-stu-id="8d240-169">The unique identifier.</span></span> |
| <span data-ttu-id="8d240-170">Etag</span><span class="sxs-lookup"><span data-stu-id="8d240-170">Etag</span></span> |<span data-ttu-id="8d240-171">**Requis pour le correctif**.</span><span class="sxs-lookup"><span data-stu-id="8d240-171">**Required for Patch**.</span></span> <span data-ttu-id="8d240-172">Mis à jour par le serveur à chaque écriture.</span><span class="sxs-lookup"><span data-stu-id="8d240-172">Updated by server on each write.</span></span> <span data-ttu-id="8d240-173">La valeur doit être égale à la valeur actuelle stockée ou '*' pour mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="8d240-173">Value must be equal to the current stored value or ‘*’ to update.</span></span> <span data-ttu-id="8d240-174">409 retourné pour les valeurs anciennes ou non valides.</span><span class="sxs-lookup"><span data-stu-id="8d240-174">409 returned for old/invalid values.</span></span> |
| <span data-ttu-id="8d240-175">properties.query</span><span class="sxs-lookup"><span data-stu-id="8d240-175">properties.query</span></span> |<span data-ttu-id="8d240-176">**Requis**.</span><span class="sxs-lookup"><span data-stu-id="8d240-176">**Required**.</span></span> <span data-ttu-id="8d240-177">Requête de la recherche.</span><span class="sxs-lookup"><span data-stu-id="8d240-177">The search query.</span></span> |
| <span data-ttu-id="8d240-178">properties.displayName</span><span class="sxs-lookup"><span data-stu-id="8d240-178">properties.displayName</span></span> |<span data-ttu-id="8d240-179">**Requis**.</span><span class="sxs-lookup"><span data-stu-id="8d240-179">**Required**.</span></span> <span data-ttu-id="8d240-180">Nom d'affichage de la requête défini par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8d240-180">The user-defined display name of the query.</span></span> |
| <span data-ttu-id="8d240-181">properties.category</span><span class="sxs-lookup"><span data-stu-id="8d240-181">properties.category</span></span> |<span data-ttu-id="8d240-182">**Requis**.</span><span class="sxs-lookup"><span data-stu-id="8d240-182">**Required**.</span></span> <span data-ttu-id="8d240-183">Catégorie de la requête définie par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8d240-183">The user-defined category of the query.</span></span> |

> [!NOTE]
> <span data-ttu-id="8d240-184">Actuellement, l'API de recherche Log Analytics retourne des recherches enregistrées créées par l'utilisateur lorsqu'elle est interrogée concernant les recherches enregistrées dans un espace de travail.</span><span class="sxs-lookup"><span data-stu-id="8d240-184">The Log Analytics search API currently returns user-created saved searches when polled for saved searches in a workspace.</span></span> <span data-ttu-id="8d240-185">L'API ne retourne pas de recherches enregistrées fournies par les solutions.</span><span class="sxs-lookup"><span data-stu-id="8d240-185">The API does not return saved searches provided by solutions.</span></span>
>
>

### <a name="create-saved-searches"></a><span data-ttu-id="8d240-186">Créer des recherches enregistrées</span><span class="sxs-lookup"><span data-stu-id="8d240-186">Create saved searches</span></span>
<span data-ttu-id="8d240-187">**Requête :**</span><span class="sxs-lookup"><span data-stu-id="8d240-187">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> <span data-ttu-id="8d240-188">Le nom de l’ensemble des recherches enregistrées, des planifications et des actions créées avec l’API Log Analytics doit être en minuscules.</span><span class="sxs-lookup"><span data-stu-id="8d240-188">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

### <a name="delete-saved-searches"></a><span data-ttu-id="8d240-189">Supprimer les recherches enregistrées</span><span class="sxs-lookup"><span data-stu-id="8d240-189">Delete saved searches</span></span>
<span data-ttu-id="8d240-190">**Requête :**</span><span class="sxs-lookup"><span data-stu-id="8d240-190">**Request:**</span></span>

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a><span data-ttu-id="8d240-191">Mettre à jour les recherches enregistrées</span><span class="sxs-lookup"><span data-stu-id="8d240-191">Update saved searches</span></span>
 <span data-ttu-id="8d240-192">**Requête :**</span><span class="sxs-lookup"><span data-stu-id="8d240-192">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a><span data-ttu-id="8d240-193">Métadonnées - JSON uniquement</span><span class="sxs-lookup"><span data-stu-id="8d240-193">Metadata - JSON only</span></span>
<span data-ttu-id="8d240-194">Voici un moyen d'afficher les champs pour tous les types de journaux pour les données collectées dans votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="8d240-194">Here’s a way to see the fields for all log types for the data collected in your workspace.</span></span> <span data-ttu-id="8d240-195">Par exemple, si vous voulez savoir si le type Événement possède un champ nommé Ordinateur, ceci constitue une méthode de vérification.</span><span class="sxs-lookup"><span data-stu-id="8d240-195">For example, if you want you know if the Event type has a field named Computer, then this query is one way to check.</span></span>

<span data-ttu-id="8d240-196">**Requête de champs :**</span><span class="sxs-lookup"><span data-stu-id="8d240-196">**Request for Fields:**</span></span>

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

<span data-ttu-id="8d240-197">**Réponse :**</span><span class="sxs-lookup"><span data-stu-id="8d240-197">**Response:**</span></span>

```
    {
      "__metadata" : {
        "schema" : {
          "name" : "Example Name",
          "version" : 2
        },
        "resultType" : "schema",
        "requestTime" : 35
      },
      "value" : [{
          "name" : "MG",
          "displayName" : "MG",
          "type" : "Guid",
          "facetable" : true,
          "display" : false,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Capacity_SMBUtilizationByHost", "Capacity_ArrayUtilization", "Capacity_SMBShareUtilization", "SQLAssessmentRecommendation", "Event", "ConfigurationChange", "ConfigurationAlert", "ADAssessmentRecommendation", "ConfigurationObject", "ConfigurationObjectProperty"]
        }, {
          "name" : "ManagementGroupName",
          "displayName" : "ManagementGroupName",
          "type" : "String",
          "facetable" : true,
          "display" : true,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Event", "ConfigurationChange", "ConfigurationAlert", "W3CIISLog", "AlertHistory", "Recommendation", "Alert", "SecurityEvent", "UpdateAgent", "RequiredUpdate", "ConfigurationObject", "ConfigurationObjectProperty"]
        }
      ]
    }
```

<span data-ttu-id="8d240-198">Le tableau suivant décrit les propriétés qui sont disponibles</span><span class="sxs-lookup"><span data-stu-id="8d240-198">The following table describes the properties that are available.</span></span>

| <span data-ttu-id="8d240-199">**Propriété**</span><span class="sxs-lookup"><span data-stu-id="8d240-199">**Property**</span></span> | <span data-ttu-id="8d240-200">**Description**</span><span class="sxs-lookup"><span data-stu-id="8d240-200">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="8d240-201">name</span><span class="sxs-lookup"><span data-stu-id="8d240-201">name</span></span> |<span data-ttu-id="8d240-202">Nom du champ.</span><span class="sxs-lookup"><span data-stu-id="8d240-202">Field name.</span></span> |
| <span data-ttu-id="8d240-203">displayName</span><span class="sxs-lookup"><span data-stu-id="8d240-203">displayName</span></span> |<span data-ttu-id="8d240-204">Nom d'affichage du champ.</span><span class="sxs-lookup"><span data-stu-id="8d240-204">The display name of the field.</span></span> |
| <span data-ttu-id="8d240-205">type</span><span class="sxs-lookup"><span data-stu-id="8d240-205">type</span></span> |<span data-ttu-id="8d240-206">Type de la valeur du champ.</span><span class="sxs-lookup"><span data-stu-id="8d240-206">The Type of the field value.</span></span> |
| <span data-ttu-id="8d240-207">facetable</span><span class="sxs-lookup"><span data-stu-id="8d240-207">facetable</span></span> |<span data-ttu-id="8d240-208">Combinaison des propriétés « indexed », « stored » et « facet » actuelles.</span><span class="sxs-lookup"><span data-stu-id="8d240-208">Combination of current ‘indexed’, ‘stored ‘and ‘facet’ properties.</span></span> |
| <span data-ttu-id="8d240-209">display</span><span class="sxs-lookup"><span data-stu-id="8d240-209">display</span></span> |<span data-ttu-id="8d240-210">Propriété « display » actuelle.</span><span class="sxs-lookup"><span data-stu-id="8d240-210">Current ‘display’ property.</span></span> <span data-ttu-id="8d240-211">True si le champ est visible dans la recherche.</span><span class="sxs-lookup"><span data-stu-id="8d240-211">True if field is visible in search.</span></span> |
| <span data-ttu-id="8d240-212">ownerType</span><span class="sxs-lookup"><span data-stu-id="8d240-212">ownerType</span></span> |<span data-ttu-id="8d240-213">Réduit uniquement aux types appartenant aux adresses IP intégrées.</span><span class="sxs-lookup"><span data-stu-id="8d240-213">Reduced to only Types belonging to onboarded IP’s.</span></span> |

## <a name="optional-parameters"></a><span data-ttu-id="8d240-214">Paramètres facultatifs</span><span class="sxs-lookup"><span data-stu-id="8d240-214">Optional parameters</span></span>
<span data-ttu-id="8d240-215">Les informations suivantes décrivent les paramètres facultatifs disponibles.</span><span class="sxs-lookup"><span data-stu-id="8d240-215">The following information describes optional parameters available.</span></span>

### <a name="highlighting"></a><span data-ttu-id="8d240-216">Highlighting</span><span class="sxs-lookup"><span data-stu-id="8d240-216">Highlighting</span></span>
<span data-ttu-id="8d240-217">Le paramètre « Highlight » est un paramètre facultatif que vous pouvez utiliser pour demander au sous-système de recherche d'inclure un jeu de marqueurs dans sa réponse.</span><span class="sxs-lookup"><span data-stu-id="8d240-217">The “Highlight” parameter is an optional parameter you may use to request the search subsystem include a set of markers in its response.</span></span>

<span data-ttu-id="8d240-218">Ces marqueurs indiquent le début et la fin du texte mis en surbrillance qui correspond aux critères fournis dans votre requête de recherche.</span><span class="sxs-lookup"><span data-stu-id="8d240-218">These markers indicate the start and end highlighted text that matches the terms provided in your search query.</span></span>
<span data-ttu-id="8d240-219">Vous pouvez spécifier les marqueurs de début et de fin qui sont utilisés par la recherche pour encapsuler le terme en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="8d240-219">You may specify the start and end markers that are used by search to wrap the highlighted term.</span></span>

<span data-ttu-id="8d240-220">**Exemple de requête de recherche**</span><span class="sxs-lookup"><span data-stu-id="8d240-220">**Example search query**</span></span>

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```

<span data-ttu-id="8d240-221">**Exemple de résultat :**</span><span class="sxs-lookup"><span data-stu-id="8d240-221">**Sample result:**</span></span>

```
    {
        "TimeGenerated":
        "2015-05-18T23:55:59Z", "Source":
        "EventLog": "Application",
        "Computer": "smokedturkey.net",
        "EventCategory": 0,
        "EventLevel":1,
        "EventLevelName":
        "Error"
        "Manager ", "__metadata":
        {
            "Type": "Event",
            "TimeGenerated": "2015-05-18T23:55:59Z",
            "highlighting": {
                "EventLevelName":
                ["{[hl]}Error{[/hl]}"]
            }
        }
    }
```

<span data-ttu-id="8d240-222">Notez que le résultat précédent contient un message d'erreur qui a été préfixé et ajouté.</span><span class="sxs-lookup"><span data-stu-id="8d240-222">Notice that the preceding result contains an error message that has been prefixed and appended.</span></span>

## <a name="computer-groups"></a><span data-ttu-id="8d240-223">Groupes d’ordinateurs</span><span class="sxs-lookup"><span data-stu-id="8d240-223">Computer groups</span></span>
<span data-ttu-id="8d240-224">Les groupes d'ordinateurs sont des recherches spéciales enregistrées qui retournent un ensemble d'ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="8d240-224">Computer groups are special saved searches that return a set of computers.</span></span>  <span data-ttu-id="8d240-225">Vous pouvez utiliser un groupe d'ordinateurs dans d'autres requêtes pour limiter les résultats aux ordinateurs du groupe.</span><span class="sxs-lookup"><span data-stu-id="8d240-225">You can use a computer group in other queries to limit the results to the computers in the group.</span></span>  <span data-ttu-id="8d240-226">Un groupe d'ordinateurs est implémenté comme une recherche enregistrée avec une balise Group dont la valeur est Computer.</span><span class="sxs-lookup"><span data-stu-id="8d240-226">A computer group is implemented as a saved search with a Group tag with a value of Computer.</span></span>

<span data-ttu-id="8d240-227">Voici un exemple de réponse pour un groupe d'ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="8d240-227">Following is a sample response for a computer group.</span></span>

```
    "etag": "W/\"datetime'2016-04-01T13%3A38%3A04.7763203Z'\"",
    "properties": {
        "Category": "My Computer Groups",
        "DisplayName": "My Computer Group",
        "Query": "srv* | Distinct Computer",
        "Tags": [{
            "Name": "Group",
            "Value": "Computer"
          }],
    "Version": 1
    }
```

### <a name="retrieving-computer-groups"></a><span data-ttu-id="8d240-228">Récupération de groupes d'ordinateurs</span><span class="sxs-lookup"><span data-stu-id="8d240-228">Retrieving computer groups</span></span>
<span data-ttu-id="8d240-229">pour récupérer un groupe d'ordinateurs, utilisez la méthode Get avec l'ID de groupe.</span><span class="sxs-lookup"><span data-stu-id="8d240-229">To retrieve a computer group, use the Get method with the group ID.</span></span>

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a><span data-ttu-id="8d240-230">Création ou mise à jour d'un groupe d'ordinateurs</span><span class="sxs-lookup"><span data-stu-id="8d240-230">Creating or updating a computer group</span></span>
<span data-ttu-id="8d240-231">Pour créer un groupe d'ordinateurs, utilisez la méthode Put avec un ID de recherche enregistrée unique.</span><span class="sxs-lookup"><span data-stu-id="8d240-231">To create a computer group, use the Put method with a unique saved search ID.</span></span> <span data-ttu-id="8d240-232">Si vous utilisez un ID de groupe d’ordinateurs existant, celui-ci est modifié.</span><span class="sxs-lookup"><span data-stu-id="8d240-232">If you use an existing computer group ID, then that one is modified.</span></span> <span data-ttu-id="8d240-233">Lorsque vous créez un groupe d'ordinateurs dans le portail Log Analytics, l'ID est créé à partir du groupe et du nom.</span><span class="sxs-lookup"><span data-stu-id="8d240-233">When you create a computer group in the Log Analytics portal, then the ID is created from the group and name.</span></span>

<span data-ttu-id="8d240-234">La requête utilisée pour la définition du groupe doit retourner un ensemble d'ordinateurs pour que le groupe fonctionne correctement.</span><span class="sxs-lookup"><span data-stu-id="8d240-234">The query used for the group definition must return a set of computers for the group to function properly.</span></span>  <span data-ttu-id="8d240-235">Il est recommandé de terminer la requête par `| Distinct Computer` pour s’assurer que les données correctes sont retournées.</span><span class="sxs-lookup"><span data-stu-id="8d240-235">It's recommended that you end your query with `| Distinct Computer` to ensure the correct data is returned.</span></span>

<span data-ttu-id="8d240-236">La définition de la recherche enregistrée doit inclure une balise nommée Group avec une valeur Computer pour que la recherche soit classée comme un groupe d'ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="8d240-236">The definition of the saved search must include a tag named Group with a value of Computer for the search to be classified as a computer group.</span></span>

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a><span data-ttu-id="8d240-237">Suppression de groupes d'ordinateurs</span><span class="sxs-lookup"><span data-stu-id="8d240-237">Deleting computer groups</span></span>
<span data-ttu-id="8d240-238">Pour supprimer un groupe d'ordinateurs, utilisez la méthode Delete avec l'ID de groupe.</span><span class="sxs-lookup"><span data-stu-id="8d240-238">To delete a computer group, use the Delete method with the group ID.</span></span>

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a><span data-ttu-id="8d240-239">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8d240-239">Next steps</span></span>
* <span data-ttu-id="8d240-240">En savoir plus sur les [recherches de journaux](log-analytics-log-searches.md) pour générer des requêtes utilisant des champs personnalisés comme critères.</span><span class="sxs-lookup"><span data-stu-id="8d240-240">Learn about [log searches](log-analytics-log-searches.md) to build queries using custom fields for criteria.</span></span>
