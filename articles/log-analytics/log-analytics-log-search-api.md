---
title: recherche de journal Analytique aaaLog API REST | Documents Microsoft
description: "Ce guide fournit un didacticiel de base qui décrit comment vous pouvez utiliser hello Analytique de journal rechercher l’API REST Bonjour Operations Management Suite (OMS) et fournit des exemples qui illustrent la façon dont les commandes de hello toouse."
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
ms.openlocfilehash: dafe5eeb8cc11a339f2cbf78cec657e344d87cac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-log-search-rest-api"></a><span data-ttu-id="ec738-103">API REST de recherche de journal Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ec738-103">Log Analytics log search REST API</span></span>
<span data-ttu-id="ec738-104">Ce guide fournit un didacticiel de base, y compris des exemples, vous pouvez utiliser hello journal Analytique recherche REST API.</span><span class="sxs-lookup"><span data-stu-id="ec738-104">This guide provides a basic tutorial, including examples, of how you can use hello Log Analytics Search REST API.</span></span> <span data-ttu-id="ec738-105">Analytique de journal fait partie de hello Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="ec738-105">Log Analytics is part of hello Operations Management Suite (OMS).</span></span>

> [!NOTE]
> <span data-ttu-id="ec738-106">Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis vous devez continuer de langage de requête hérité hello toouse avec les API de recherche de journal hello comme décrit dans cet article.</span><span class="sxs-lookup"><span data-stu-id="ec738-106">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then you should continue toouse hello legacy query language with hello log search API as described in this article.</span></span>  <span data-ttu-id="ec738-107">Une nouvelle API sera disponible pour les espaces de travail mis à niveau et mise à jour des hello documentation à ce moment-là.</span><span class="sxs-lookup"><span data-stu-id="ec738-107">A new API will be released for upgraded workspaces, and hello documentation will be updated at that time.</span></span> 

> [!NOTE]
> <span data-ttu-id="ec738-108">Analytique de journal s’appelait auparavant Operational Insights, c’est pourquoi il est le nom hello utilisé dans le fournisseur de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="ec738-108">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello resource provider.</span></span>
>
>

## <a name="overview-of-hello-log-search-rest-api"></a><span data-ttu-id="ec738-109">Vue d’ensemble de hello API REST de recherche journal</span><span class="sxs-lookup"><span data-stu-id="ec738-109">Overview of hello Log Search REST API</span></span>
<span data-ttu-id="ec738-110">Hello API REST de journal Analytique Search est RESTful et est accessible via hello API Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ec738-110">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager API.</span></span> <span data-ttu-id="ec738-111">Cet article fournit des exemples d’accès aux API hello via [ARMClient](https://github.com/projectkudu/ARMClient), un outil de ligne de commande open source qui simplifie l’appel hello API Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ec738-111">This article provides examples of accessing hello API through [ARMClient](https://github.com/projectkudu/ARMClient), an open source command-line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="ec738-112">utilisation de Hello d’ARMClient est une des nombreuses options de tooaccess hello API de recherche Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="ec738-112">hello use of ARMClient is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="ec738-113">Une autre option est un module d’Azure PowerShell hello toouse pour OperationalInsights, qui inclut des applets de commande pour l’accès à la recherche.</span><span class="sxs-lookup"><span data-stu-id="ec738-113">Another option is toouse hello Azure PowerShell module for OperationalInsights, which includes cmdlets for accessing search.</span></span> <span data-ttu-id="ec738-114">Grâce à ces outils, vous pouvez utiliser des espaces de travail hello API Azure Resource Manager toomake appelle tooOMS et exécuter des commandes de recherche de.</span><span class="sxs-lookup"><span data-stu-id="ec738-114">With these tools, you can utilize hello Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="ec738-115">Hello API génère des résultats de recherche au format JSON, ce qui vous toouse résultats de la recherche hello de différentes façons par programme.</span><span class="sxs-lookup"><span data-stu-id="ec738-115">hello API outputs search results in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

<span data-ttu-id="ec738-116">Bonjour Azure Resource Manager peut être utilisé via une [bibliothèque pour .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) et hello [API REST](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec738-116">hello Azure Resource Manager can be used via a [Library for .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) and hello [REST API](https://msdn.microsoft.com/library/azure/mt163658.aspx).</span></span> <span data-ttu-id="ec738-117">toolearn plus, consulter les pages web hello lié.</span><span class="sxs-lookup"><span data-stu-id="ec738-117">toolearn more, review hello linked web pages.</span></span>

> [!NOTE]
> <span data-ttu-id="ec738-118">Si vous utilisez une commande d’agrégation, telles que `|measure count()` ou `distinct`, chaque appel toosearch peut retourner au maximum 500 000 enregistrements.</span><span class="sxs-lookup"><span data-stu-id="ec738-118">If you use an aggregation command such as `|measure count()` or `distinct`, each call toosearch can return upto 500,000 records.</span></span> <span data-ttu-id="ec738-119">Les recherches qui n’incluent pas une commande d’agrégation renvoient jusqu'à 5 000 enregistrements.</span><span class="sxs-lookup"><span data-stu-id="ec738-119">Searches that do not include an aggregation command return upto 5,000 records.</span></span>
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a><span data-ttu-id="ec738-120">Didacticiel de base sur l’API de recherche de journal de Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ec738-120">Basic Log Analytics Search REST API tutorial</span></span>
### <a name="toouse-armclient"></a><span data-ttu-id="ec738-121">toouse ARMClient</span><span class="sxs-lookup"><span data-stu-id="ec738-121">toouse ARMClient</span></span>
1. <span data-ttu-id="ec738-122">Installez [Chocolatey](https://chocolatey.org/)(gestionnaire de packages open source pour Windows).</span><span class="sxs-lookup"><span data-stu-id="ec738-122">Install [Chocolatey](https://chocolatey.org/), which is an Open Source Package Manager for Windows.</span></span> <span data-ttu-id="ec738-123">Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur, puis exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ec738-123">Open a command prompt window as administrator and then run hello following command:</span></span>

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. <span data-ttu-id="ec738-124">Installez ARMClient en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ec738-124">Install ARMClient by running hello following command:</span></span>

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a><span data-ttu-id="ec738-125">tooperform une recherche à l’aide d’ARMClient</span><span class="sxs-lookup"><span data-stu-id="ec738-125">tooperform a search using ARMClient</span></span>
1. <span data-ttu-id="ec738-126">Connectez-vous à l’aide de votre compte Microsoft, ou de votre compte professionnel ou scolaire :</span><span class="sxs-lookup"><span data-stu-id="ec738-126">Log in using your Microsoft account or your work or school account:</span></span>

    ```
    armclient login
    ```

    <span data-ttu-id="ec738-127">Une connexion réussie répertorie tous les abonnements qui sont associés toohello compte donné :</span><span class="sxs-lookup"><span data-stu-id="ec738-127">A successful login lists all subscriptions tied toohello given account:</span></span>

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. <span data-ttu-id="ec738-128">Obtenir les espaces de travail hello Operations Management Suite :</span><span class="sxs-lookup"><span data-stu-id="ec738-128">Get hello Operations Management Suite workspaces:</span></span>

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    <span data-ttu-id="ec738-129">Un appel Get affiche que tous les espaces de travail lié toohello abonnement :</span><span class="sxs-lookup"><span data-stu-id="ec738-129">A successful Get call would output all workspaces tied toohello subscription:</span></span>

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
3. <span data-ttu-id="ec738-130">Créez votre variable de recherche :</span><span class="sxs-lookup"><span data-stu-id="ec738-130">Create your search variable:</span></span>

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. <span data-ttu-id="ec738-131">Lancez une recherche à l’aide de votre nouvelle variable de recherche :</span><span class="sxs-lookup"><span data-stu-id="ec738-131">Search using your new search variable:</span></span>

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a><span data-ttu-id="ec738-132">Exemples de référence de l’API REST de recherche Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ec738-132">Log Analytics Search REST API reference examples</span></span>
<span data-ttu-id="ec738-133">Hello suivant exemples vous montrent comment vous pouvez utiliser les API de recherche de hello.</span><span class="sxs-lookup"><span data-stu-id="ec738-133">hello following examples show you how you can use hello Search API.</span></span>

### <a name="search---actionread"></a><span data-ttu-id="ec738-134">Recherche - Action/lecture</span><span class="sxs-lookup"><span data-stu-id="ec738-134">Search - Action/Read</span></span>
<span data-ttu-id="ec738-135">**Exemple d’URL :**</span><span class="sxs-lookup"><span data-stu-id="ec738-135">**Sample Url:**</span></span>

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

<span data-ttu-id="ec738-136">**Requête :**</span><span class="sxs-lookup"><span data-stu-id="ec738-136">**Request:**</span></span>

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
<span data-ttu-id="ec738-137">Hello tableau suivant décrit les propriétés de hello qui sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="ec738-137">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="ec738-138">**Propriété**</span><span class="sxs-lookup"><span data-stu-id="ec738-138">**Property**</span></span> | <span data-ttu-id="ec738-139">**Description**</span><span class="sxs-lookup"><span data-stu-id="ec738-139">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="ec738-140">top</span><span class="sxs-lookup"><span data-stu-id="ec738-140">top</span></span> |<span data-ttu-id="ec738-141">nombre maximal de Hello de tooreturn de résultats.</span><span class="sxs-lookup"><span data-stu-id="ec738-141">hello maximum number of results tooreturn.</span></span> |
| <span data-ttu-id="ec738-142">highlight</span><span class="sxs-lookup"><span data-stu-id="ec738-142">highlight</span></span> |<span data-ttu-id="ec738-143">Contient des pré- et post-paramètres, utilisés généralement pour mettre en surbrillance les champs de correspondance</span><span class="sxs-lookup"><span data-stu-id="ec738-143">Contains pre and post parameters, used usually for highlighting matching fields</span></span> |
| <span data-ttu-id="ec738-144">pre</span><span class="sxs-lookup"><span data-stu-id="ec738-144">pre</span></span> |<span data-ttu-id="ec738-145">Préfixes hello donné champs tooyour mis en correspondance de chaîne.</span><span class="sxs-lookup"><span data-stu-id="ec738-145">Prefixes hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="ec738-146">post</span><span class="sxs-lookup"><span data-stu-id="ec738-146">post</span></span> |<span data-ttu-id="ec738-147">Ajoute hello donné champs tooyour mis en correspondance de chaîne.</span><span class="sxs-lookup"><span data-stu-id="ec738-147">Appends hello given string tooyour matched fields.</span></span> |
| <span data-ttu-id="ec738-148">query</span><span class="sxs-lookup"><span data-stu-id="ec738-148">query</span></span> |<span data-ttu-id="ec738-149">requête de recherche Hello utilisé toocollect et retourner des résultats.</span><span class="sxs-lookup"><span data-stu-id="ec738-149">hello search query used toocollect and return results.</span></span> |
| <span data-ttu-id="ec738-150">start</span><span class="sxs-lookup"><span data-stu-id="ec738-150">start</span></span> |<span data-ttu-id="ec738-151">début de Hello hello de fenêtre de temps de que vous souhaitez toobe résultats trouvée à partir.</span><span class="sxs-lookup"><span data-stu-id="ec738-151">hello beginning of hello time window you want results toobe found from.</span></span> |
| <span data-ttu-id="ec738-152">end</span><span class="sxs-lookup"><span data-stu-id="ec738-152">end</span></span> |<span data-ttu-id="ec738-153">fin de Hello hello de fenêtre de temps de que vous souhaitez toobe résultats trouvée à partir.</span><span class="sxs-lookup"><span data-stu-id="ec738-153">hello end of hello time window you want results toobe found from.</span></span> |

<span data-ttu-id="ec738-154">**Réponse :**</span><span class="sxs-lookup"><span data-stu-id="ec738-154">**Response:**</span></span>

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

### <a name="searchid---actionread"></a><span data-ttu-id="ec738-155">Recherche/{ID} - Action/lecture</span><span class="sxs-lookup"><span data-stu-id="ec738-155">Search/{ID} - Action/Read</span></span>
<span data-ttu-id="ec738-156">**Contenu de hello la demande d’une recherche enregistrée :**</span><span class="sxs-lookup"><span data-stu-id="ec738-156">**Request hello contents of a Saved Search:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> <span data-ttu-id="ec738-157">Si hello recherche retourne un état « En attente », résultats de l’interrogation hello mis à jour peuvent être effectuées via cette API.</span><span class="sxs-lookup"><span data-stu-id="ec738-157">If hello search returns with a ‘Pending’ status, then polling hello updated results can be done through this API.</span></span> <span data-ttu-id="ec738-158">Après 6 minutes, résultat hello de recherche de hello est supprimé du cache de hello et HTTP Gone est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="ec738-158">After 6 min, hello result of hello search will be dropped from hello cache and HTTP Gone will be returned.</span></span> <span data-ttu-id="ec738-159">Si la demande de recherche initiale hello retourne immédiatement l’état « Succès », les résultats de hello ne sont pas ajoutés de cache toohello à l’origine de cette tooreturn API HTTP Gone si elle est interrogée.</span><span class="sxs-lookup"><span data-stu-id="ec738-159">If hello initial search request returns a ‘Successful’ status immediately, hello results are not added toohello cache causing this API tooreturn HTTP Gone if queried.</span></span> <span data-ttu-id="ec738-160">Hello le contenu d’un résultat HTTP 200 est Bonjour même format que la demande de recherche initiale hello, avec des valeurs mises à jour.</span><span class="sxs-lookup"><span data-stu-id="ec738-160">hello contents of an HTTP 200 result are in hello same format as hello initial search request just with updated values.</span></span>
>
>

### <a name="saved-searches"></a><span data-ttu-id="ec738-161">Recherches enregistrées</span><span class="sxs-lookup"><span data-stu-id="ec738-161">Saved searches</span></span>
<span data-ttu-id="ec738-162">**Demander la liste des recherches enregistrées :**</span><span class="sxs-lookup"><span data-stu-id="ec738-162">**Request List of Saved Searches:**</span></span>

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

<span data-ttu-id="ec738-163">Méthodes prises en charge : GET PUT DELETE</span><span class="sxs-lookup"><span data-stu-id="ec738-163">Supported methods: GET PUT DELETE</span></span>

<span data-ttu-id="ec738-164">Méthodes de collection prises en charge : GET</span><span class="sxs-lookup"><span data-stu-id="ec738-164">Supported collection methods: GET</span></span>

<span data-ttu-id="ec738-165">Hello tableau suivant décrit les propriétés de hello qui sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="ec738-165">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="ec738-166">Propriété</span><span class="sxs-lookup"><span data-stu-id="ec738-166">Property</span></span> | <span data-ttu-id="ec738-167">Description</span><span class="sxs-lookup"><span data-stu-id="ec738-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ec738-168">Id</span><span class="sxs-lookup"><span data-stu-id="ec738-168">Id</span></span> |<span data-ttu-id="ec738-169">Identificateur unique de Hello.</span><span class="sxs-lookup"><span data-stu-id="ec738-169">hello unique identifier.</span></span> |
| <span data-ttu-id="ec738-170">Etag</span><span class="sxs-lookup"><span data-stu-id="ec738-170">Etag</span></span> |<span data-ttu-id="ec738-171">**Requis pour le correctif**.</span><span class="sxs-lookup"><span data-stu-id="ec738-171">**Required for Patch**.</span></span> <span data-ttu-id="ec738-172">Mis à jour par le serveur à chaque écriture.</span><span class="sxs-lookup"><span data-stu-id="ec738-172">Updated by server on each write.</span></span> <span data-ttu-id="ec738-173">Valeur doit être égale toohello actuelle stockée ou ' *' tooupdate.</span><span class="sxs-lookup"><span data-stu-id="ec738-173">Value must be equal toohello current stored value or ‘*’ tooupdate.</span></span> <span data-ttu-id="ec738-174">409 retourné pour les valeurs anciennes ou non valides.</span><span class="sxs-lookup"><span data-stu-id="ec738-174">409 returned for old/invalid values.</span></span> |
| <span data-ttu-id="ec738-175">properties.query</span><span class="sxs-lookup"><span data-stu-id="ec738-175">properties.query</span></span> |<span data-ttu-id="ec738-176">**Requis**.</span><span class="sxs-lookup"><span data-stu-id="ec738-176">**Required**.</span></span> <span data-ttu-id="ec738-177">requête de recherche Hello.</span><span class="sxs-lookup"><span data-stu-id="ec738-177">hello search query.</span></span> |
| <span data-ttu-id="ec738-178">properties.displayName</span><span class="sxs-lookup"><span data-stu-id="ec738-178">properties.displayName</span></span> |<span data-ttu-id="ec738-179">**Requis**.</span><span class="sxs-lookup"><span data-stu-id="ec738-179">**Required**.</span></span> <span data-ttu-id="ec738-180">nom d’affichage de défini par l’utilisateur de Hello de requête de hello.</span><span class="sxs-lookup"><span data-stu-id="ec738-180">hello user-defined display name of hello query.</span></span> |
| <span data-ttu-id="ec738-181">properties.category</span><span class="sxs-lookup"><span data-stu-id="ec738-181">properties.category</span></span> |<span data-ttu-id="ec738-182">**Requis**.</span><span class="sxs-lookup"><span data-stu-id="ec738-182">**Required**.</span></span> <span data-ttu-id="ec738-183">catégories définies par l’utilisateur Hello de requête de hello.</span><span class="sxs-lookup"><span data-stu-id="ec738-183">hello user-defined category of hello query.</span></span> |

> [!NOTE]
> <span data-ttu-id="ec738-184">Hello API de recherche Analytique de journal actuellement renvoie créés par l’utilisateur quand elle est interrogée concernant les recherches enregistrées dans un espace de travail de recherches enregistrées.</span><span class="sxs-lookup"><span data-stu-id="ec738-184">hello Log Analytics search API currently returns user-created saved searches when polled for saved searches in a workspace.</span></span> <span data-ttu-id="ec738-185">Hello API ne retourne pas de recherches enregistrées fournies par les solutions.</span><span class="sxs-lookup"><span data-stu-id="ec738-185">hello API does not return saved searches provided by solutions.</span></span>
>
>

### <a name="create-saved-searches"></a><span data-ttu-id="ec738-186">Créer des recherches enregistrées</span><span class="sxs-lookup"><span data-stu-id="ec738-186">Create saved searches</span></span>
<span data-ttu-id="ec738-187">**Requête :**</span><span class="sxs-lookup"><span data-stu-id="ec738-187">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> <span data-ttu-id="ec738-188">nom de Hello pour toutes les recherches enregistrées, planifications et créées par hello API Analytique de journal des actions doit être en minuscules.</span><span class="sxs-lookup"><span data-stu-id="ec738-188">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

### <a name="delete-saved-searches"></a><span data-ttu-id="ec738-189">Supprimer les recherches enregistrées</span><span class="sxs-lookup"><span data-stu-id="ec738-189">Delete saved searches</span></span>
<span data-ttu-id="ec738-190">**Requête :**</span><span class="sxs-lookup"><span data-stu-id="ec738-190">**Request:**</span></span>

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a><span data-ttu-id="ec738-191">Mettre à jour les recherches enregistrées</span><span class="sxs-lookup"><span data-stu-id="ec738-191">Update saved searches</span></span>
 <span data-ttu-id="ec738-192">**Requête :**</span><span class="sxs-lookup"><span data-stu-id="ec738-192">**Request:**</span></span>

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a><span data-ttu-id="ec738-193">Métadonnées - JSON uniquement</span><span class="sxs-lookup"><span data-stu-id="ec738-193">Metadata - JSON only</span></span>
<span data-ttu-id="ec738-194">Voici un moyen toosee hello des champs pour tous les types de journaux pour les données hello collectées dans votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="ec738-194">Here’s a way toosee hello fields for all log types for hello data collected in your workspace.</span></span> <span data-ttu-id="ec738-195">Par exemple, si vous souhaitez que savoir si le type d’événement de hello possède un champ nommé ordinateur, cette requête est une façon toocheck.</span><span class="sxs-lookup"><span data-stu-id="ec738-195">For example, if you want you know if hello Event type has a field named Computer, then this query is one way toocheck.</span></span>

<span data-ttu-id="ec738-196">**Requête de champs :**</span><span class="sxs-lookup"><span data-stu-id="ec738-196">**Request for Fields:**</span></span>

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

<span data-ttu-id="ec738-197">**Réponse :**</span><span class="sxs-lookup"><span data-stu-id="ec738-197">**Response:**</span></span>

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

<span data-ttu-id="ec738-198">Hello tableau suivant décrit les propriétés de hello qui sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="ec738-198">hello following table describes hello properties that are available.</span></span>

| <span data-ttu-id="ec738-199">**Propriété**</span><span class="sxs-lookup"><span data-stu-id="ec738-199">**Property**</span></span> | <span data-ttu-id="ec738-200">**Description**</span><span class="sxs-lookup"><span data-stu-id="ec738-200">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="ec738-201">name</span><span class="sxs-lookup"><span data-stu-id="ec738-201">name</span></span> |<span data-ttu-id="ec738-202">Nom du champ.</span><span class="sxs-lookup"><span data-stu-id="ec738-202">Field name.</span></span> |
| <span data-ttu-id="ec738-203">displayName</span><span class="sxs-lookup"><span data-stu-id="ec738-203">displayName</span></span> |<span data-ttu-id="ec738-204">Hello affiche le nom du champ de hello.</span><span class="sxs-lookup"><span data-stu-id="ec738-204">hello display name of hello field.</span></span> |
| <span data-ttu-id="ec738-205">type</span><span class="sxs-lookup"><span data-stu-id="ec738-205">type</span></span> |<span data-ttu-id="ec738-206">Type de valeur du champ hello de Hello.</span><span class="sxs-lookup"><span data-stu-id="ec738-206">hello Type of hello field value.</span></span> |
| <span data-ttu-id="ec738-207">facetable</span><span class="sxs-lookup"><span data-stu-id="ec738-207">facetable</span></span> |<span data-ttu-id="ec738-208">Combinaison des propriétés « indexed », « stored » et « facet » actuelles.</span><span class="sxs-lookup"><span data-stu-id="ec738-208">Combination of current ‘indexed’, ‘stored ‘and ‘facet’ properties.</span></span> |
| <span data-ttu-id="ec738-209">display</span><span class="sxs-lookup"><span data-stu-id="ec738-209">display</span></span> |<span data-ttu-id="ec738-210">Propriété « display » actuelle.</span><span class="sxs-lookup"><span data-stu-id="ec738-210">Current ‘display’ property.</span></span> <span data-ttu-id="ec738-211">True si le champ est visible dans la recherche.</span><span class="sxs-lookup"><span data-stu-id="ec738-211">True if field is visible in search.</span></span> |
| <span data-ttu-id="ec738-212">ownerType</span><span class="sxs-lookup"><span data-stu-id="ec738-212">ownerType</span></span> |<span data-ttu-id="ec738-213">Types de tooonly réduite qui appartiennent à l’adresse IP tooonboarded.</span><span class="sxs-lookup"><span data-stu-id="ec738-213">Reduced tooonly Types belonging tooonboarded IP’s.</span></span> |

## <a name="optional-parameters"></a><span data-ttu-id="ec738-214">Paramètres facultatifs</span><span class="sxs-lookup"><span data-stu-id="ec738-214">Optional parameters</span></span>
<span data-ttu-id="ec738-215">Hello informations suivantes décrit les paramètres facultatifs disponibles.</span><span class="sxs-lookup"><span data-stu-id="ec738-215">hello following information describes optional parameters available.</span></span>

### <a name="highlighting"></a><span data-ttu-id="ec738-216">Highlighting</span><span class="sxs-lookup"><span data-stu-id="ec738-216">Highlighting</span></span>
<span data-ttu-id="ec738-217">paramètre de « Highlight » Hello est un paramètre facultatif, vous pouvez utiliser le sous-système de recherche hello toorequest inclure un jeu de marqueurs dans sa réponse.</span><span class="sxs-lookup"><span data-stu-id="ec738-217">hello “Highlight” parameter is an optional parameter you may use toorequest hello search subsystem include a set of markers in its response.</span></span>

<span data-ttu-id="ec738-218">Ces marqueurs indiquent hello début et la fin du texte en surbrillance qui correspond aux critères de hello fournis dans votre requête de recherche.</span><span class="sxs-lookup"><span data-stu-id="ec738-218">These markers indicate hello start and end highlighted text that matches hello terms provided in your search query.</span></span>
<span data-ttu-id="ec738-219">Vous pouvez spécifier hello début et fin des marqueurs qui sont utilisés par le terme de recherche toowrap hello mis en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="ec738-219">You may specify hello start and end markers that are used by search toowrap hello highlighted term.</span></span>

<span data-ttu-id="ec738-220">**Exemple de requête de recherche**</span><span class="sxs-lookup"><span data-stu-id="ec738-220">**Example search query**</span></span>

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

<span data-ttu-id="ec738-221">**Exemple de résultat :**</span><span class="sxs-lookup"><span data-stu-id="ec738-221">**Sample result:**</span></span>

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

<span data-ttu-id="ec738-222">Notez que hello résultat précédent contient un message d’erreur qui a été préfixé et ajouté.</span><span class="sxs-lookup"><span data-stu-id="ec738-222">Notice that hello preceding result contains an error message that has been prefixed and appended.</span></span>

## <a name="computer-groups"></a><span data-ttu-id="ec738-223">Groupes d’ordinateurs</span><span class="sxs-lookup"><span data-stu-id="ec738-223">Computer groups</span></span>
<span data-ttu-id="ec738-224">Les groupes d'ordinateurs sont des recherches spéciales enregistrées qui retournent un ensemble d'ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="ec738-224">Computer groups are special saved searches that return a set of computers.</span></span>  <span data-ttu-id="ec738-225">Vous pouvez utiliser un groupe d’ordinateurs dans d’autres ordinateurs de toohello des résultats de requêtes toolimit hello dans le groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="ec738-225">You can use a computer group in other queries toolimit hello results toohello computers in hello group.</span></span>  <span data-ttu-id="ec738-226">Un groupe d'ordinateurs est implémenté comme une recherche enregistrée avec une balise Group dont la valeur est Computer.</span><span class="sxs-lookup"><span data-stu-id="ec738-226">A computer group is implemented as a saved search with a Group tag with a value of Computer.</span></span>

<span data-ttu-id="ec738-227">Voici un exemple de réponse pour un groupe d'ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="ec738-227">Following is a sample response for a computer group.</span></span>

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

### <a name="retrieving-computer-groups"></a><span data-ttu-id="ec738-228">Récupération de groupes d'ordinateurs</span><span class="sxs-lookup"><span data-stu-id="ec738-228">Retrieving computer groups</span></span>
<span data-ttu-id="ec738-229">ID d’un groupe d’ordinateurs, utilisez hello méthode Get avec groupe de hello tooretrieve</span><span class="sxs-lookup"><span data-stu-id="ec738-229">tooretrieve a computer group, use hello Get method with hello group ID.</span></span>

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a><span data-ttu-id="ec738-230">Création ou mise à jour d'un groupe d'ordinateurs</span><span class="sxs-lookup"><span data-stu-id="ec738-230">Creating or updating a computer group</span></span>
<span data-ttu-id="ec738-231">toocreate un groupe d’ordinateurs, utilisez hello méthode Put avec un ID de recherche enregistrée unique.</span><span class="sxs-lookup"><span data-stu-id="ec738-231">toocreate a computer group, use hello Put method with a unique saved search ID.</span></span> <span data-ttu-id="ec738-232">Si vous utilisez un ID de groupe d’ordinateurs existant, celui-ci est modifié.</span><span class="sxs-lookup"><span data-stu-id="ec738-232">If you use an existing computer group ID, then that one is modified.</span></span> <span data-ttu-id="ec738-233">Lorsque vous créez un groupe d’ordinateurs dans le portail d’Analytique de journal hello, hello ID est créé à partir de nom et le groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="ec738-233">When you create a computer group in hello Log Analytics portal, then hello ID is created from hello group and name.</span></span>

<span data-ttu-id="ec738-234">requête Hello utilisé pour la définition de groupe hello doit retourner un ensemble d’ordinateurs pour hello groupe toofunction correctement.</span><span class="sxs-lookup"><span data-stu-id="ec738-234">hello query used for hello group definition must return a set of computers for hello group toofunction properly.</span></span>  <span data-ttu-id="ec738-235">Il est recommandé que vous mettez fin à la requête avec `| Distinct Computer` hello tooensure correct de données sont retournées.</span><span class="sxs-lookup"><span data-stu-id="ec738-235">It's recommended that you end your query with `| Distinct Computer` tooensure hello correct data is returned.</span></span>

<span data-ttu-id="ec738-236">définition de Hello Hello recherche enregistrée doit inclure une balise nommée groupe avec la valeur de l’ordinateur pour toobe de recherche hello classée sous forme d’un groupe d’ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="ec738-236">hello definition of hello saved search must include a tag named Group with a value of Computer for hello search toobe classified as a computer group.</span></span>

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a><span data-ttu-id="ec738-237">Suppression de groupes d'ordinateurs</span><span class="sxs-lookup"><span data-stu-id="ec738-237">Deleting computer groups</span></span>
<span data-ttu-id="ec738-238">ID d’un groupe d’ordinateurs, utilisez hello méthode Delete avec groupe de hello toodelete</span><span class="sxs-lookup"><span data-stu-id="ec738-238">toodelete a computer group, use hello Delete method with hello group ID.</span></span>

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a><span data-ttu-id="ec738-239">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ec738-239">Next steps</span></span>
* <span data-ttu-id="ec738-240">En savoir plus sur [recherche de journal](log-analytics-log-searches.md) toobuild les requêtes à l’aide des champs personnalisés pour les critères.</span><span class="sxs-lookup"><span data-stu-id="ec738-240">Learn about [log searches](log-analytics-log-searches.md) toobuild queries using custom fields for criteria.</span></span>
