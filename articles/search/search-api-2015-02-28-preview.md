---
title: "API REST du service Azure Search : version 2015-02-28-Preview | Microsoft Docs"
description: "L'API REST du service Azure Search version 2015-02-28-Preview comprend des fonctionnalités expérimentales telles que des analyseurs de langage naturel et des recherches moreLikeThis."
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: e6ad5c964bfa8421be2706cb4015980e01a271b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="fd94d-103">API REST du service Azure Search : version 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="fd94d-103">Azure Search Service REST API: Version 2015-02-28-Preview</span></span>
<span data-ttu-id="fd94d-104">Cet article constitue la documentation de référence de `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-104">This article is the reference documentation for `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="fd94d-105">Cette version préliminaire étend la version actuelle disponible, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), en fournissant les fonctionnalités expérimentales suivantes :</span><span class="sxs-lookup"><span data-stu-id="fd94d-105">This preview extends the current generally available version, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), by providing the following experimental features:</span></span>

* <span data-ttu-id="fd94d-106">`moreLikeThis` dans l’API [Search Documents](#SearchDocs) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-106">`moreLikeThis` query parameter in the [Search Documents](#SearchDocs) API.</span></span> <span data-ttu-id="fd94d-107">Il recherche d’autres documents correspondant à un autre document spécifique.</span><span class="sxs-lookup"><span data-stu-id="fd94d-107">It finds other documents that are relevant to another specific document.</span></span>

<span data-ttu-id="fd94d-108">Certains éléments supplémentaires de l’API REST `2015-02-28-Preview` sont documentés séparément.</span><span class="sxs-lookup"><span data-stu-id="fd94d-108">A few additional parts of the `2015-02-28-Preview` REST API are documented separately.</span></span> <span data-ttu-id="fd94d-109">Vous avez notamment vu les points suivants :</span><span class="sxs-lookup"><span data-stu-id="fd94d-109">These include:</span></span>

* [<span data-ttu-id="fd94d-110">Profils de calcul de score</span><span class="sxs-lookup"><span data-stu-id="fd94d-110">Scoring Profiles</span></span>](search-api-scoring-profiles-2015-02-28-preview.md)
* [<span data-ttu-id="fd94d-111">Indexeurs</span><span class="sxs-lookup"><span data-stu-id="fd94d-111">Indexers</span></span>](search-api-indexers-2015-02-28-preview.md)

<span data-ttu-id="fd94d-112">Le service Azure Search est disponible dans plusieurs versions.</span><span class="sxs-lookup"><span data-stu-id="fd94d-112">Azure Search service is available in multiple versions.</span></span> <span data-ttu-id="fd94d-113">Pour plus d'informations, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-113">Please refer to [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details.</span></span>

## <a name="apis-in-this-document"></a><span data-ttu-id="fd94d-114">API dans ce document</span><span class="sxs-lookup"><span data-stu-id="fd94d-114">APIs in this document</span></span>
<span data-ttu-id="fd94d-115">L’API du service Azure Search prend en charge deux syntaxes d’URL pour les opérations d’API : simple et OData. Pour plus d’informations, consultez [Prise en charge d’OData (API Azure Search)](http://msdn.microsoft.com/library/azure/dn798932.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd94d-115">Azure Search service API supports two URL syntaxes for API operations: simple and OData (see [Support for OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) for details).</span></span> <span data-ttu-id="fd94d-116">La liste suivante présente la syntaxe simple.</span><span class="sxs-lookup"><span data-stu-id="fd94d-116">The following list shows the simple syntax.</span></span>

[<span data-ttu-id="fd94d-117">Création d'index</span><span class="sxs-lookup"><span data-stu-id="fd94d-117">Create Index</span></span>](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="fd94d-118">Mise à jour d'index</span><span class="sxs-lookup"><span data-stu-id="fd94d-118">Update Index</span></span>](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="fd94d-119">Obtention d'index</span><span class="sxs-lookup"><span data-stu-id="fd94d-119">Get Index</span></span>](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="fd94d-120">Liste des index</span><span class="sxs-lookup"><span data-stu-id="fd94d-120">Listing Indexes</span></span>](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="fd94d-121">Obtention de statistiques d'index</span><span class="sxs-lookup"><span data-stu-id="fd94d-121">Get Index Statistics</span></span>](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[<span data-ttu-id="fd94d-122">Tester l’analyseur</span><span class="sxs-lookup"><span data-stu-id="fd94d-122">Test Analyzer</span></span>](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[<span data-ttu-id="fd94d-123">Suppression d'index</span><span class="sxs-lookup"><span data-stu-id="fd94d-123">Delete an Index</span></span>](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="fd94d-124">Ajout, suppression et mise à jour de données dans un index</span><span class="sxs-lookup"><span data-stu-id="fd94d-124">Add, Delete, and Update Data within an Index</span></span>](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[<span data-ttu-id="fd94d-125">Recherche dans des documents</span><span class="sxs-lookup"><span data-stu-id="fd94d-125">Search Documents</span></span>](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[<span data-ttu-id="fd94d-126">Recherche de document</span><span class="sxs-lookup"><span data-stu-id="fd94d-126">Lookup Document</span></span>](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[<span data-ttu-id="fd94d-127">Nombre de documents</span><span class="sxs-lookup"><span data-stu-id="fd94d-127">Count Documents</span></span>](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[<span data-ttu-id="fd94d-128">Suggestions</span><span class="sxs-lookup"><span data-stu-id="fd94d-128">Suggestions</span></span>](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a><span data-ttu-id="fd94d-129">Opérations d'index</span><span class="sxs-lookup"><span data-stu-id="fd94d-129">Index Operations</span></span>
<span data-ttu-id="fd94d-130">Vous pouvez créer et gérer des index dans le service Azure Search via de simples requêtes HTTP (POST, GET, PUT, DELETE) sur une ressource d'index donnée.</span><span class="sxs-lookup"><span data-stu-id="fd94d-130">You can create and manage indexes in Azure Search service via simple HTTP requests (POST, GET, PUT, DELETE) against a given index resource.</span></span> <span data-ttu-id="fd94d-131">Pour créer un index, vous commencez par PUBLIER un document JSON décrivant le schéma d'index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-131">To create an index, you first POST a JSON document that describes the index schema.</span></span> <span data-ttu-id="fd94d-132">Le schéma définit les champs de l'index, leurs types de données et comment les utiliser (par exemple, dans des recherches en texte intégral, des filtres, des tris ou des facettes).</span><span class="sxs-lookup"><span data-stu-id="fd94d-132">The schema defines the fields of the index, their data types, and how they can be used (for example, in full-text searches, filters, sorting, or faceting).</span></span> <span data-ttu-id="fd94d-133">Il définit également des profils de calcul de score, des générateurs de suggestions et d'autres attributs permettant de configurer le comportement de l'index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-133">It also defines scoring profiles, suggesters and other attributes to configure the behavior of the index.</span></span>

<span data-ttu-id="fd94d-134">L'exemple suivant illustre un schéma utilisé pour rechercher des informations sur des hôtels avec le champ Description défini en deux langues.</span><span class="sxs-lookup"><span data-stu-id="fd94d-134">The following example provides an illustration of a schema used for searching on hotel information with the Description field defined in two languages.</span></span> <span data-ttu-id="fd94d-135">Notez la façon dont les attributs contrôlent le mode d'utilisation du champ.</span><span class="sxs-lookup"><span data-stu-id="fd94d-135">Notice how attributes control how the field is used.</span></span> <span data-ttu-id="fd94d-136">Par exemple, `hotelId` est utilisé comme clé de document (`"key": true`) et est exclu des recherches en texte intégral (`"searchable": false`).</span><span class="sxs-lookup"><span data-stu-id="fd94d-136">For example the `hotelId` is used as the document key (`"key": true`) and is excluded from full-text searches (`"searchable": false`).</span></span>

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

<span data-ttu-id="fd94d-137">Une fois que l'index est créé, vous allez télécharger les documents qui le remplissent.</span><span class="sxs-lookup"><span data-stu-id="fd94d-137">After the index is created, you'll upload documents that populate the index.</span></span> <span data-ttu-id="fd94d-138">Pour cette étape, consultez [Ajout ou mise à jour de documents](#AddOrUpdateDocuments) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-138">See [Add or Update Documents](#AddOrUpdateDocuments) for this next step.</span></span>

<span data-ttu-id="fd94d-139">Pour obtenir une présentation vidéo de l'indexation dans Azure Search, consultez l' [épisode Cloud Cover : Azure Search sur Channel 9](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span><span class="sxs-lookup"><span data-stu-id="fd94d-139">For a video introduction to indexing in Azure Search, see the [Channel 9 Cloud Cover episode on Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span></span>

<a name="CreateIndex"></a>

## <a name="create-index"></a><span data-ttu-id="fd94d-140">Création d'index</span><span class="sxs-lookup"><span data-stu-id="fd94d-140">Create Index</span></span>
<span data-ttu-id="fd94d-141">Dans Azure Search, un index est le principal moyen d'organiser des documents et d'y faire des recherches, un peu comme une table permet d'organiser des enregistrements dans une base de données.</span><span class="sxs-lookup"><span data-stu-id="fd94d-141">An index is the primary means of organizing and searching documents in Azure Search, similar to how a table organizes records in a database.</span></span> <span data-ttu-id="fd94d-142">Chaque index englobe un ensemble de documents tous conformes à un même schéma d'index (noms de champ, types de données et propriétés), mais il spécifie également des constructions supplémentaires (générateurs de suggestions, profils de calcul de score et options CORS) qui définissent d'autres comportements de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-142">Each index has a collection of documents that all conform to the index schema (field names, data types, and properties), but indexes also specify additional constructs (suggesters, scoring profiles, and CORS options) that define other search behaviors.</span></span>

<span data-ttu-id="fd94d-143">Vous pouvez créer un index dans un service Azure Search à l'aide d'une requête HTTP POST ou PUT.</span><span class="sxs-lookup"><span data-stu-id="fd94d-143">You can create a new index within an Azure Search service using an HTTP POST or PUT request.</span></span> <span data-ttu-id="fd94d-144">Le corps de la requête est un schéma JSON qui spécifie les informations de configuration et d'index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-144">The body of the request is a JSON schema that specifies the index and configuration information.</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="fd94d-145">Vous pouvez également utiliser une requête PUT en spécifiant le nom d'index sur l'URI.</span><span class="sxs-lookup"><span data-stu-id="fd94d-145">Alternatively, you can use PUT and specify the index name on the URI.</span></span> <span data-ttu-id="fd94d-146">Si l'index n'existe pas, il est créé.</span><span class="sxs-lookup"><span data-stu-id="fd94d-146">If the index does not exist, it will be created.</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

<span data-ttu-id="fd94d-147">La création d'un index détermine la structure des documents stockés et utilisés dans les opérations de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-147">Creating an index determines the structure of the documents stored and used in search operations.</span></span> <span data-ttu-id="fd94d-148">Le remplissage de l'index est une opération distincte.</span><span class="sxs-lookup"><span data-stu-id="fd94d-148">Populating the index is a separate operation.</span></span> <span data-ttu-id="fd94d-149">Pour cette étape, vous pouvez utiliser un [indexeur](https://msdn.microsoft.com/library/azure/mt183328.aspx) (disponible pour les sources de données prises en charge) ou une opération [Ajout, mise à jour ou suppression de documents](https://msdn.microsoft.com/library/azure/dn798930.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd94d-149">For this step, you can use an [indexer](https://msdn.microsoft.com/library/azure/mt183328.aspx) (available for supported data sources) or an [Add, Update, or Delete Documents](https://msdn.microsoft.com/library/azure/dn798930.aspx) operation.</span></span> <span data-ttu-id="fd94d-150">L'index inversé est généré lors de la publication des documents.</span><span class="sxs-lookup"><span data-stu-id="fd94d-150">The inverted index is generated when the documents are posted.</span></span>

<span data-ttu-id="fd94d-151">**Remarque**: le nombre maximal d'index que vous pouvez créer varie en fonction du niveau de tarification.</span><span class="sxs-lookup"><span data-stu-id="fd94d-151">**Note**: The maximum number of indexes allowed varies by pricing tier.</span></span> <span data-ttu-id="fd94d-152">Le service gratuit autorise jusqu'à 3 index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-152">The free service allows up to 3 indexes.</span></span> <span data-ttu-id="fd94d-153">Le service standard autorise 50 index par service de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-153">Standard service allows 50 indexes per Search service.</span></span> <span data-ttu-id="fd94d-154">Pour plus d'informations, consultez [Limites et contraintes](http://msdn.microsoft.com/library/azure/dn798934.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-154">See [Limits and constraints](http://msdn.microsoft.com/library/azure/dn798934.aspx) for details.</span></span>

<span data-ttu-id="fd94d-155">**Requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-155">**Request**</span></span>

<span data-ttu-id="fd94d-156">Le protocole HTTPS est requis pour toutes les requêtes de service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-156">HTTPS is required for all service requests.</span></span> <span data-ttu-id="fd94d-157">La requête **Create Index** peut être construite à l'aide d'une méthode POST ou PUT.</span><span class="sxs-lookup"><span data-stu-id="fd94d-157">The **Create Index** request can be constructed using either a POST or PUT method.</span></span> <span data-ttu-id="fd94d-158">Si vous utilisez une méthode POST, fournissez un nom d'index dans le corps de la requête, ainsi que la définition du schéma d'index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-158">When using POST, you must provide an index name in the request body along with the index schema definition.</span></span> <span data-ttu-id="fd94d-159">Avec la méthode PUT, le nom d'index fait partie de l'URL.</span><span class="sxs-lookup"><span data-stu-id="fd94d-159">With PUT, the index name is part of the URL.</span></span> <span data-ttu-id="fd94d-160">Si l'index n'existe pas, il est créé.</span><span class="sxs-lookup"><span data-stu-id="fd94d-160">If the index doesn't exist, it is created.</span></span> <span data-ttu-id="fd94d-161">S'il existe déjà, il est mis à jour en fonction de la nouvelle définition.</span><span class="sxs-lookup"><span data-stu-id="fd94d-161">If it already exists, it is updated to the new definition.</span></span>

<span data-ttu-id="fd94d-162">Le nom d'index doit être en minuscules, commencer par une lettre ou un chiffre, ne contenir ni barres obliques ni points, et comprendre moins de 128 caractères.</span><span class="sxs-lookup"><span data-stu-id="fd94d-162">The index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="fd94d-163">Après la lettre ou le chiffre du début, le nom d'index peut comprendre des lettres, des chiffres et des tirets (non consécutifs).</span><span class="sxs-lookup"><span data-stu-id="fd94d-163">After starting the index name with a letter or number, the rest of the name can include any letter, number and dashes, as long as the dashes are not consecutive.</span></span>

<span data-ttu-id="fd94d-164">Le paramètre `api-version` est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="fd94d-164">The `api-version` is required.</span></span> <span data-ttu-id="fd94d-165">Pour obtenir la liste des versions disponibles, consultez [Contrôle de version du service Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-165">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for a list of available versions.</span></span>

<span data-ttu-id="fd94d-166">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-166">**Request Headers**</span></span>

<span data-ttu-id="fd94d-167">La liste suivante décrit les en-têtes de requête obligatoires et facultatifs.</span><span class="sxs-lookup"><span data-stu-id="fd94d-167">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="fd94d-168">`Content-Type`: requis.</span><span class="sxs-lookup"><span data-stu-id="fd94d-168">`Content-Type`: Required.</span></span> <span data-ttu-id="fd94d-169">À définir avec la valeur `application/json`</span><span class="sxs-lookup"><span data-stu-id="fd94d-169">Set this to `application/json`</span></span>
* <span data-ttu-id="fd94d-170">`api-key`: obligatoire.</span><span class="sxs-lookup"><span data-stu-id="fd94d-170">`api-key`: Required.</span></span> <span data-ttu-id="fd94d-171">L'en-tête `api-key` est utilisé pour</span><span class="sxs-lookup"><span data-stu-id="fd94d-171">The `api-key` is used to</span></span>
* <span data-ttu-id="fd94d-172">authentifier la requête auprès de votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-172">authenticate the request to your Search service.</span></span> <span data-ttu-id="fd94d-173">Il s'agit d'une valeur de type chaîne de caractères, unique pour votre service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-173">It is a string value, unique to your service.</span></span> <span data-ttu-id="fd94d-174">La requête **Create Index** doit inclure un en-tête `api-key` défini sur votre clé d'administration (par opposition à une clé de requête).</span><span class="sxs-lookup"><span data-stu-id="fd94d-174">The **Create Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="fd94d-175">Vous avez également besoin du nom du service pour construire l'URL de la requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-175">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="fd94d-176">Vous pouvez obtenir le nom du service et l'en-tête `api-key` à partir de votre tableau de bord de service dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fd94d-176">You can get both the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="fd94d-177">Pour obtenir de l'aide sur la navigation dans les pages, consultez [Création d'un service Azure Search dans le portail](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-177">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="fd94d-178"><a name="RequestData"></a>
**Syntaxe du corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-178"><a name="RequestData"></a>
**Request Body Syntax**</span></span>

<span data-ttu-id="fd94d-179">Le corps de la requête contient une définition de schéma qui inclut la liste des champs de données des documents qui alimenteront cet index, des types de données, des attributs, ainsi qu'une liste facultative de profils de calcul de score utilisés pour les documents correspondants au moment de la requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-179">The body of the request contains a schema definition, which includes the list of data fields within documents that will be fed into this index, data types, attributes, as well as an optional list of scoring profiles that are used to score matching documents at query time.</span></span>

<span data-ttu-id="fd94d-180">Notez que, pour une requête POST, vous devez spécifier le nom d'index dans le corps de la requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-180">Note that for a POST request, you must specify the index name in the request body.</span></span>

<span data-ttu-id="fd94d-181">Il ne peut exister qu'un seul champ de clé dans l'index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-181">There can only be one key field in the index.</span></span> <span data-ttu-id="fd94d-182">Il doit s'agir d'un champ de chaîne.</span><span class="sxs-lookup"><span data-stu-id="fd94d-182">It has to be a string field.</span></span> <span data-ttu-id="fd94d-183">Ce champ représente l'identificateur unique de chaque document stocké dans l'index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-183">This field represents the unique identifier for each document stored within the index.</span></span>

<span data-ttu-id="fd94d-184">Les parties principales d'un index sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="fd94d-184">The main parts of an index include the following:</span></span>

* `name`
* <span data-ttu-id="fd94d-185">`fields` qui alimenteront cet index, y compris le nom, le type de données et les propriétés qui définissent les actions autorisées sur ce champ.</span><span class="sxs-lookup"><span data-stu-id="fd94d-185">`fields` that will be fed into this index, including name, data type, and properties that define allowable actions on that field.</span></span>
* <span data-ttu-id="fd94d-186">`suggesters` utilisés pour les requêtes prédictives ou avec saisie semi-automatique.</span><span class="sxs-lookup"><span data-stu-id="fd94d-186">`suggesters` used for auto-complete or type-ahead queries.</span></span>
* <span data-ttu-id="fd94d-187">`scoringProfiles` utilisés pour le classement personnalisé des scores de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-187">`scoringProfiles` used for custom search score ranking.</span></span> <span data-ttu-id="fd94d-188">Pour plus d'informations, consultez [Ajout de profils de calcul de score](https://msdn.microsoft.com/library/azure/dn798928.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-188">See [Add scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for details.</span></span>
* <span data-ttu-id="fd94d-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` utilisés pour définir la façon dont vos documents/requêtes sont répartis en jetons indexables/cherchables.</span><span class="sxs-lookup"><span data-stu-id="fd94d-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` used to define how your documents/queries are broken into indexable/searchable tokens.</span></span> <span data-ttu-id="fd94d-190">Consultez [Analyse dans Azure Search](https://aka.ms//azsanalysis) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="fd94d-190">See [Analysis in Azure Search](https://aka.ms//azsanalysis) for details.</span></span>
* <span data-ttu-id="fd94d-191">`defaultScoringProfile` utilisé pour remplacer les comportements de calcul de score par défaut.</span><span class="sxs-lookup"><span data-stu-id="fd94d-191">`defaultScoringProfile` used to overwrite the default scoring behaviors.</span></span>
* <span data-ttu-id="fd94d-192">`corsOptions` pour autoriser les requêtes cross-origin sur votre index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-192">`corsOptions` to allow cross-origin queries against your index.</span></span>

<span data-ttu-id="fd94d-193">Vous trouverez ci-dessous la syntaxe de structuration de la charge utile de la requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-193">The syntax for structuring the request payload is as follows.</span></span> <span data-ttu-id="fd94d-194">Vous trouverez un exemple de requête dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="fd94d-194">A sample request is provided further on in this topic.</span></span>

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of the analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of the search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of the indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in the future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies to searchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading to now over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter to be passed in queries to use as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (the distance in kilometers from the reference location where the boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter to be passed in queries to specify list of tags to compare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

<span data-ttu-id="fd94d-195">**Attributs d'index**</span><span class="sxs-lookup"><span data-stu-id="fd94d-195">**Index Attributes**</span></span>

<span data-ttu-id="fd94d-196">Lors de la création d'un index, les attributs suivants peuvent être définis.</span><span class="sxs-lookup"><span data-stu-id="fd94d-196">The following attributes can be set when creating an index.</span></span> <span data-ttu-id="fd94d-197">Pour plus d'informations sur le calcul de score et les profils de calcul de score, consultez [Ajout de profils de calcul de score](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd94d-197">For details about scoring and scoring profiles, see [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span>

<span data-ttu-id="fd94d-198">`name` -Définit le nom du champ.</span><span class="sxs-lookup"><span data-stu-id="fd94d-198">`name` - Sets the name of the field.</span></span>

<span data-ttu-id="fd94d-199">`type` : définit le type de données pour le champ.</span><span class="sxs-lookup"><span data-stu-id="fd94d-199">`type` - Sets the data type for the field.</span></span>

<span data-ttu-id="fd94d-200">`searchable` : indique que le champ peut faire l'objet d'une recherche en texte intégral.</span><span class="sxs-lookup"><span data-stu-id="fd94d-200">`searchable` - Marks the field as full-text search-able.</span></span> <span data-ttu-id="fd94d-201">Cela signifie qu'il fera l'objet d'une analyse, par exemple lexicale, lors de l'indexation.</span><span class="sxs-lookup"><span data-stu-id="fd94d-201">This means it will undergo analysis such as word-breaking during indexing.</span></span> <span data-ttu-id="fd94d-202">Si vous définissez un champ `searchable` avec une valeur telle que « journée ensoleillée », cette valeur est fractionnée au niveau interne en jetons individuels « journée » et « ensoleillée ».</span><span class="sxs-lookup"><span data-stu-id="fd94d-202">If you set a `searchable` field to a value like "sunny day", internally it will be split into the individual tokens "sunny" and "day".</span></span> <span data-ttu-id="fd94d-203">Cela permet d'effectuer des recherches en texte intégral de ces termes.</span><span class="sxs-lookup"><span data-stu-id="fd94d-203">This enables full-text searches for these terms.</span></span> <span data-ttu-id="fd94d-204">Les champs de type `Edm.String` ou `Collection(Edm.String)` sont `searchable` par défaut.</span><span class="sxs-lookup"><span data-stu-id="fd94d-204">Fields of type `Edm.String` or `Collection(Edm.String)` are `searchable` by default.</span></span> <span data-ttu-id="fd94d-205">Les autres types de champs ne peuvent pas être `searchable`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-205">Fields of other types cannot be `searchable`.</span></span>

* <span data-ttu-id="fd94d-206">**Remarque** : les champs `searchable` nécessitent davantage d’espace dans votre index, car Azure Search stocke une version supplémentaire tokenisée de la valeur du champ pour les recherches en texte intégral.</span><span class="sxs-lookup"><span data-stu-id="fd94d-206">**Note**: `searchable` fields consume extra space in your index since Azure Search will store an additional tokenized version of the field value for full-text searches.</span></span> <span data-ttu-id="fd94d-207">Si vous voulez économiser de l'espace dans votre index et que vous n'avez pas besoin d'inclure un champ dans les recherches, définissez `searchable` avec la valeur `false`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-207">If you want to save space in your index and you don't need a field to be included in searches, set `searchable` to `false`.</span></span>

<span data-ttu-id="fd94d-208">`filterable` : permet de référencer le champ dans les requêtes `$filter`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-208">`filterable` - Allows the field to be referenced in `$filter` queries.</span></span> <span data-ttu-id="fd94d-209">`filterable` diffère de `searchable` du point de vue du mode de traitement des chaînes.</span><span class="sxs-lookup"><span data-stu-id="fd94d-209">`filterable` differs from `searchable` in how strings are handled.</span></span> <span data-ttu-id="fd94d-210">Les champs de type `Edm.String` ou `Collection(Edm.String)` qui sont `filterable` ne font pas l'objet d'une analyse lexicale, les comparaisons ne concernent donc que les correspondances exactes.</span><span class="sxs-lookup"><span data-stu-id="fd94d-210">Fields of type `Edm.String` or `Collection(Edm.String)` that are `filterable` do not undergo word-breaking, so comparisons are for exact matches only.</span></span> <span data-ttu-id="fd94d-211">Par exemple, si vous définissez un champ de type `f` avec la valeur « journée ensoleillée », `$filter=f eq 'sunny'` ne trouvera aucune correspondance, contrairement à `$filter=f eq 'sunny day'`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-211">For example, if you set such a field `f` to "sunny day", `$filter=f eq 'sunny'` will find no matches, but `$filter=f eq 'sunny day'` will.</span></span> <span data-ttu-id="fd94d-212">Tous les champs sont `filterable` par défaut.</span><span class="sxs-lookup"><span data-stu-id="fd94d-212">All fields are `filterable` by default.</span></span>

<span data-ttu-id="fd94d-213">`sortable` : par défaut, le système trie les résultats par score, mais souvent les utilisateurs voudront effectuer un tri par champs dans les documents.</span><span class="sxs-lookup"><span data-stu-id="fd94d-213">`sortable` - By default the system sorts results by score, but in many experiences users will want to sort by fields in the documents.</span></span> <span data-ttu-id="fd94d-214">Les champs de type `Collection(Edm.String)` ne peuvent pas être `sortable`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-214">Fields of type `Collection(Edm.String)` cannot be `sortable`.</span></span> <span data-ttu-id="fd94d-215">Tous les autres champs sont `sortable` par défaut.</span><span class="sxs-lookup"><span data-stu-id="fd94d-215">All other fields are `sortable` by default.</span></span>

<span data-ttu-id="fd94d-216">`facetable`: généralement utilisé dans une présentation des résultats de recherche qui inclut le nombre d'accès par catégorie (par exemple, vous recherchez des appareils photo numériques et regardez le nombre d'accès par marque, mégapixels, prix, etc.).</span><span class="sxs-lookup"><span data-stu-id="fd94d-216">`facetable`- Typically used in a presentation of search results that includes hit count by category (for example, search for digital cameras and see hits by brand, by megapixels, by price, etc.).</span></span> <span data-ttu-id="fd94d-217">Cette option ne peut pas être utilisée avec des champs de type `Edm.GeographyPoint`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-217">This option cannot be used with fields of type `Edm.GeographyPoint`.</span></span> <span data-ttu-id="fd94d-218">Tous les autres champs sont `facetable` par défaut.</span><span class="sxs-lookup"><span data-stu-id="fd94d-218">All other fields are `facetable` by default.</span></span>

* <span data-ttu-id="fd94d-219">**Remarque** : les champs de type `Edm.String` qui sont `filterable`, `sortable` ou `facetable` ne doivent pas dépasser 32 Ko de longueur.</span><span class="sxs-lookup"><span data-stu-id="fd94d-219">**Note**: Fields of type `Edm.String` that are `filterable`, `sortable`, or `facetable` can be at most 32KB in length.</span></span> <span data-ttu-id="fd94d-220">En effet, ces champs sont traités en tant que terme de recherche unique, et la longueur maximale d'un terme dans Azure Search est 32 Ko.</span><span class="sxs-lookup"><span data-stu-id="fd94d-220">This is because such fields are treated as a single search term, and the maximum length of a term in Azure Search is 32KB.</span></span> <span data-ttu-id="fd94d-221">Si vous devez stocker plus de texte dans un champ de chaîne unique, définissez explicitement `filterable`, `sortable` et `facetable` avec la valeur `false` dans votre définition d'index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-221">If you need to store more text than this in a single string field, you will need to explicitly set `filterable`, `sortable`, and `facetable` to `false` in your index definition.</span></span>
* <span data-ttu-id="fd94d-222">**Remarque** : si aucun des attributs ci-dessus dans un champ n’est défini avec la valeur `true` (`searchable`, `filterable`, `sortable` ou `facetable`), le champ est exclu de l’index inversé.</span><span class="sxs-lookup"><span data-stu-id="fd94d-222">**Note**: If a field has none of the above attributes set to `true` (`searchable`, `filterable`, `sortable`,  or`facetable`) the field is effectively excluded from the inverted index.</span></span> <span data-ttu-id="fd94d-223">Cette option est utile pour les champs qui ne sont pas utilisés dans les requêtes, mais qui sont nécessaires dans les résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-223">This option is useful for fields that are not used in queries, but are needed in search results.</span></span> <span data-ttu-id="fd94d-224">L'exclusion de ces champs de l'index améliore les performances.</span><span class="sxs-lookup"><span data-stu-id="fd94d-224">Excluding such fields from the index improves performance.</span></span>

<span data-ttu-id="fd94d-225">`key` : indique que le champ contient des identificateurs uniques pour les documents de l'index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-225">`key` - Marks the field as containing unique identifiers for documents within the index.</span></span> <span data-ttu-id="fd94d-226">Un seul champ doit être choisi comme champ `key` et il doit être de type `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-226">Exactly one field must be chosen as the `key` field and it must be of type `Edm.String`.</span></span> <span data-ttu-id="fd94d-227">Les champs de clés peuvent servir à rechercher des documents directement via l' [API de recherche](#LookupAPI).</span><span class="sxs-lookup"><span data-stu-id="fd94d-227">Key fields can be used to look up documents directly via the [Lookup API](#LookupAPI).</span></span>

<span data-ttu-id="fd94d-228">`retrievable` : définit si le champ peut être retourné dans un résultat de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-228">`retrievable` - Sets whether the field can be returned in a search result.</span></span>  <span data-ttu-id="fd94d-229">Cet attribut est utile quand vous voulez utiliser un champ (par exemple, la marge) comme mécanisme de filtre, de tri ou de score, mais que vous ne voulez pas qu'il soit visible par l'utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="fd94d-229">This is useful when you want to use a field (for example, margin) as a filter, sorting, or scoring mechanism but do not want the field to be visible to the end user.</span></span> <span data-ttu-id="fd94d-230">Il doit être `true` for `key` .</span><span class="sxs-lookup"><span data-stu-id="fd94d-230">This attribute must be `true` for `key` fields.</span></span>

<span data-ttu-id="fd94d-231">`analyzer` : définit le nom de l’analyseur à utiliser pour le champ au moment de la recherche et de l’indexation.</span><span class="sxs-lookup"><span data-stu-id="fd94d-231">`analyzer` - Sets the name of the analyzer to use for the field at search time and indexing time.</span></span> <span data-ttu-id="fd94d-232">Pour connaître l’ensemble des valeurs autorisées, consultez la rubrique [Analyseurs](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd94d-232">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="fd94d-233">Cette option ne peut être utilisée qu’avec les champs `searchable` et ne peut être associée à `searchAnalyzer` ou `indexAnalyzer`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-233">This option can be used only with `searchable` fields and it can't be set together with either `searchAnalyzer` or `indexAnalyzer`.</span></span>  <span data-ttu-id="fd94d-234">Une fois l'analyseur choisi, il ne peut pas être modifié pour le champ.</span><span class="sxs-lookup"><span data-stu-id="fd94d-234">Once the analyzer is chosen, it cannot be changed for the field.</span></span>

<span data-ttu-id="fd94d-235">`searchAnalyzer` : définit le nom de l’analyseur utilisé pour le champ au moment de la recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-235">`searchAnalyzer` - Sets the name of the analyzer used at search time for the field.</span></span> <span data-ttu-id="fd94d-236">Pour connaître l’ensemble des valeurs autorisées, consultez la rubrique [Analyseurs](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd94d-236">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="fd94d-237">Cette option peut être utilisée uniquement avec les champs `searchable` .</span><span class="sxs-lookup"><span data-stu-id="fd94d-237">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="fd94d-238">Elle doit être associée à `indexAnalyzer` et ne peut pas être associée à l’option `analyzer`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-238">It must be set together with `indexAnalyzer` and it cannot be set together with the `analyzer` option.</span></span> <span data-ttu-id="fd94d-239">Cet analyseur peut être mis à jour sur un champ existant.</span><span class="sxs-lookup"><span data-stu-id="fd94d-239">This analyzer can be updated on an existing field.</span></span>

<span data-ttu-id="fd94d-240">`indexAnalyzer` : définit le nom de l’analyseur utilisé pour le champ au moment de l’indexation.</span><span class="sxs-lookup"><span data-stu-id="fd94d-240">`indexAnalyzer` - Sets the name of the analyzer used at indexing time for the field.</span></span> <span data-ttu-id="fd94d-241">Pour connaître l’ensemble des valeurs autorisées, consultez la rubrique [Analyseurs](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd94d-241">For the allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="fd94d-242">Cette option peut être utilisée uniquement avec les champs `searchable` .</span><span class="sxs-lookup"><span data-stu-id="fd94d-242">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="fd94d-243">Elle doit être associée à `searchAnalyzer` et ne peut pas être associée à l’option `analyzer`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-243">It must be set together with `searchAnalyzer` and it cannot be set together with the `analyzer` option.</span></span> <span data-ttu-id="fd94d-244">Une fois l'analyseur choisi, il ne peut pas être modifié pour le champ.</span><span class="sxs-lookup"><span data-stu-id="fd94d-244">Once the analyzer is chosen, it cannot be changed for the field.</span></span>

<span data-ttu-id="fd94d-245">`suggesters` : définit le mode de recherche et les champs constituant la source du contenu pour obtenir des suggestions.</span><span class="sxs-lookup"><span data-stu-id="fd94d-245">`suggesters` - Sets the search mode and fields that are the source of the content for suggestions.</span></span> <span data-ttu-id="fd94d-246">Pour plus d'informations, consultez [Générateurs de suggestions](#Suggesters) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-246">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="fd94d-247">`scoringProfiles` : définit les comportements de calcul de score personnalisés qui vous permettent de choisir les éléments qui s'affichent en haut des résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-247">`scoringProfiles` - Defines custom scoring behaviors that let you influence which items appear higher in search results.</span></span> <span data-ttu-id="fd94d-248">Les profils de calcul de score sont constitués de pondérations et de fonctions de champ.</span><span class="sxs-lookup"><span data-stu-id="fd94d-248">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="fd94d-249">Pour plus d'informations sur les attributs utilisés dans un profil de calcul de score, consultez [Ajout de profils de calcul de score](https://msdn.microsoft.com/library/azure/dn798928.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-249">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information about the attributes used in a scoring profile.</span></span>

<span data-ttu-id="fd94d-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Support multilingue**</span><span class="sxs-lookup"><span data-stu-id="fd94d-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Language support**</span></span>

<span data-ttu-id="fd94d-251">Les champs pouvant faire l'objet d'une recherche subissent une analyse qui implique la plupart du temps une analyse lexicale, la normalisation du texte et le filtrage des termes.</span><span class="sxs-lookup"><span data-stu-id="fd94d-251">Searchable fields undergo analysis that most frequently involves word-breaking, text normalization, and filtering out terms.</span></span> <span data-ttu-id="fd94d-252">Par défaut, les champs pouvant faire l’objet d’une recherche dans Azure Search sont analysés par [l’Analyseur Apache Lucene Standard](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html), qui découpe le texte en éléments selon les règles de [« Segmentation du texte Unicode »](http://unicode.org/reports/tr29/).</span><span class="sxs-lookup"><span data-stu-id="fd94d-252">By default, searchable fields in Azure Search are analyzed with the [Apache Lucene Standard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) which breaks text into elements following the["Unicode Text Segmentation"](http://unicode.org/reports/tr29/) rules.</span></span> <span data-ttu-id="fd94d-253">Par ailleurs, l'analyseur standard convertit tous les caractères en minuscules.</span><span class="sxs-lookup"><span data-stu-id="fd94d-253">Additionally, the standard analyzer converts all characters to their lower case form.</span></span> <span data-ttu-id="fd94d-254">Les documents indexés et les termes de recherche sont analysés pendant l'indexation et le traitement des requêtes.</span><span class="sxs-lookup"><span data-stu-id="fd94d-254">Both indexed documents and search terms go through the analysis during indexing and query processing.</span></span>

<span data-ttu-id="fd94d-255">Azure Search prend en charge l’indexation des champs dans plusieurs langues.</span><span class="sxs-lookup"><span data-stu-id="fd94d-255">Azure Search supports a variety of languages.</span></span> <span data-ttu-id="fd94d-256">Chaque langue requiert un analyseur de texte non standard qui tient compte des caractéristiques d'une langue donnée.</span><span class="sxs-lookup"><span data-stu-id="fd94d-256">Each language requires a non-standard text analyzer which accounts for characteristics of a given language.</span></span> <span data-ttu-id="fd94d-257">Azure Search propose deux types d'analyseurs :</span><span class="sxs-lookup"><span data-stu-id="fd94d-257">Azure Search offers two types of analyzers:</span></span>

* <span data-ttu-id="fd94d-258">35 analyseurs pris en charge par Lucene.</span><span class="sxs-lookup"><span data-stu-id="fd94d-258">35 analyzers backed by Lucene.</span></span>
* <span data-ttu-id="fd94d-259">50 analyseurs pris en charge par la technologie de traitement du langage naturel Microsoft propriétaire utilisée dans Office et Bing.</span><span class="sxs-lookup"><span data-stu-id="fd94d-259">50 analyzers backed by proprietary Microsoft natural language processing technology used in Office and Bing.</span></span>

<span data-ttu-id="fd94d-260">Certains développeurs peuvent préférer la solution open source, plus familière et simple de Lucene.</span><span class="sxs-lookup"><span data-stu-id="fd94d-260">Some developers might prefer the more familiar, simple, open-source solution of Lucene.</span></span> <span data-ttu-id="fd94d-261">Les analyseurs Lucene sont plus rapides, mais les analyseurs Microsoft bénéficient de fonctionnalités avancées, telles que la lemmatisation, la décomposition des mots (dans les langues comme l’allemand, le danois, le néerlandais, le suédois, le norvégien, l’estonien, le finnois, le hongrois, et le slovaque) et la reconnaissance d’entité (URL, courriers électroniques, dates, numéros).</span><span class="sxs-lookup"><span data-stu-id="fd94d-261">Lucene analyzers are faster, but the Microsoft analyzers have advanced capabilities, such as lemmatization, word decompounding (in languages like German, Danish, Dutch, Swedish, Norwegian, Estonian, Finish, Hungarian, Slovak) and entity recognition (URLs, emails, dates, numbers).</span></span> <span data-ttu-id="fd94d-262">Si possible, vous devez comparer les analyseurs Microsoft et Lucene pour savoir lequel vous convient le mieux.</span><span class="sxs-lookup"><span data-stu-id="fd94d-262">If possible, you should run comparisons of both the Microsoft and Lucene analyzers to decide which one is a better fit.</span></span>

<span data-ttu-id="fd94d-263">***Comparatif***</span><span class="sxs-lookup"><span data-stu-id="fd94d-263">***How they compare***</span></span>

<span data-ttu-id="fd94d-264">L'analyseur Lucene pour l'anglais est une extension de l'analyseur standard.</span><span class="sxs-lookup"><span data-stu-id="fd94d-264">The Lucene analyzer for English extends the standard analyzer.</span></span> <span data-ttu-id="fd94d-265">Il supprime la marque du possessif (le « ’s ») à la fin des mots, applique la recherche de radical conformément à [l’algorithme de recherche de radical de Porter](http://tartarus.org/~martin/PorterStemmer/) et supprime les [mots vides](http://en.wikipedia.org/wiki/Stop_words) de l’anglais.</span><span class="sxs-lookup"><span data-stu-id="fd94d-265">It removes possessives (trailing 's) from words, applies stemming as per [Porter Stemming algorithm](http://tartarus.org/~martin/PorterStemmer/), and removes English [stop words](http://en.wikipedia.org/wiki/Stop_words).</span></span>

<span data-ttu-id="fd94d-266">En comparaison, l’analyseur Microsoft procède par lemmatisation plutôt que par recherche de radical.</span><span class="sxs-lookup"><span data-stu-id="fd94d-266">In comparison, the Microsoft analyzer performs lemmatization instead of stemming.</span></span> <span data-ttu-id="fd94d-267">Cela signifie qu’il peut bien mieux gérer des mots infléchis et de formes irrégulières, ce qui donne des résultats de recherche plus pertinents (module espion 7 de [Présentation MVA d’Azure Search](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) pour plus de détails).</span><span class="sxs-lookup"><span data-stu-id="fd94d-267">It means it can handle inflected and irregular word forms much better what results in more relevant search results (watch module 7 of [Azure Search MVA presentation](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) for more details).</span></span>

<span data-ttu-id="fd94d-268">L’indexation avec les analyseurs Microsoft est en moyenne trois fois plus lente qu’avec leurs équivalents Lucene, en fonction de la langue.</span><span class="sxs-lookup"><span data-stu-id="fd94d-268">Indexing with Microsoft analyzers is on average two to three times slower than their Lucene equivalents, depending on the language.</span></span> <span data-ttu-id="fd94d-269">Les performances de recherche ne doivent pas être trop affectées pour les requêtes de taille moyenne.</span><span class="sxs-lookup"><span data-stu-id="fd94d-269">Search performance should not be significantly affected for average size queries.</span></span>

<span data-ttu-id="fd94d-270">***Configuration***</span><span class="sxs-lookup"><span data-stu-id="fd94d-270">***Configuration***</span></span>

<span data-ttu-id="fd94d-271">Pour chaque champ dans la définition d'index, vous pouvez affecter à la propriété `analyzer` un nom d'analyseur qui spécifie la langue et le fournisseur.</span><span class="sxs-lookup"><span data-stu-id="fd94d-271">For each field in the index definition, you can set the `analyzer` property to an analyzer name that specifies which language and vendor.</span></span> <span data-ttu-id="fd94d-272">Le même analyseur sera appliqué lors de l’indexation et de la recherche pour ce champ.</span><span class="sxs-lookup"><span data-stu-id="fd94d-272">The same analyzer will be applied when indexing and searching for that field.</span></span>
<span data-ttu-id="fd94d-273">Par exemple, vous pouvez avoir des champs distincts pour des descriptions d'hôtel en anglais, français et espagnol qui existent côte à côte dans le même index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-273">For example, you can have separate fields for English, French, and Spanish hotel descriptions that exist side-by-side in the same index.</span></span> <span data-ttu-id="fd94d-274">Utilisez le [paramètre de requête « searchFields »](#SearchQueryParameters) pour spécifier le champ de langue spécifique à rechercher dans vos requêtes.</span><span class="sxs-lookup"><span data-stu-id="fd94d-274">Use the ['searchFields' query parameter](#SearchQueryParameters) to specify which language-specific field to search against in your queries.</span></span> <span data-ttu-id="fd94d-275">Vous pouvez consulter des exemples de requêtes qui incluent la propriété `analyzer` dans [Recherche dans des documents](#SearchDocs).</span><span class="sxs-lookup"><span data-stu-id="fd94d-275">You can review query examples that include the `analyzer` property in [Search Documents](#SearchDocs).</span></span> 

<span data-ttu-id="fd94d-276">***Liste d’analyseurs***</span><span class="sxs-lookup"><span data-stu-id="fd94d-276">***Analyzer list***</span></span>

<span data-ttu-id="fd94d-277">Voici la liste des langues prises en charge avec les noms d’analyseur Lucene et Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fd94d-277">Below is the list of supported languages together with Lucene and Microsoft analyzer names.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="fd94d-278">Langage</span><span class="sxs-lookup"><span data-stu-id="fd94d-278">Language</span></span></th>
        <th><span data-ttu-id="fd94d-279">Nom de l’analyseur Microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-279">Microsoft analyzer name</span></span></th>
        <th><span data-ttu-id="fd94d-280">Nom de l’analyseur Lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-280">Lucene analyzer name</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-281">Arabe</span><span class="sxs-lookup"><span data-stu-id="fd94d-281">Arabic</span></span></td>
        <td><span data-ttu-id="fd94d-282">ar.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-282">ar.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-283">ar.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-283">ar.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-284">Arménien</span><span class="sxs-lookup"><span data-stu-id="fd94d-284">Armenian</span></span></td>
        <td></td>
        <td><span data-ttu-id="fd94d-285">hy.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-285">hy.lucene</span></span></td>
      </tr>
    <tr>
        <td><span data-ttu-id="fd94d-286">Bangla</span><span class="sxs-lookup"><span data-stu-id="fd94d-286">Bangla</span></span></td>
        <td><span data-ttu-id="fd94d-287">bn.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-287">bn.microsoft</span></span></td>
        <td></td>
    </tr>
      <tr>
        <td><span data-ttu-id="fd94d-288">Basque</span><span class="sxs-lookup"><span data-stu-id="fd94d-288">Basque</span></span></td>
        <td></td>
        <td><span data-ttu-id="fd94d-289">eu.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-289">eu.lucene</span></span></td>
    </tr>
      <tr>
         <td><span data-ttu-id="fd94d-290">Bulgare</span><span class="sxs-lookup"><span data-stu-id="fd94d-290">Bulgarian</span></span></td>
        <td><span data-ttu-id="fd94d-291">bg.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-291">bg.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-292">bg.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-292">bg.lucene</span></span></td>
      </tr>
      <tr>
        <td><span data-ttu-id="fd94d-293">Catalan</span><span class="sxs-lookup"><span data-stu-id="fd94d-293">Catalan</span></span></td>
        <td><span data-ttu-id="fd94d-294">ca.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-294">ca.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-295">ca.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-295">ca.lucene</span></span></td>          
      </tr>
    <tr>
        <td><span data-ttu-id="fd94d-296">Chinois simplifié</span><span class="sxs-lookup"><span data-stu-id="fd94d-296">Chinese Simplified</span></span></td>
        <td><span data-ttu-id="fd94d-297">zh-Hans.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-297">zh-Hans.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-298">zh-Hans.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-298">zh-Hans.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-299">Chinois traditionnel</span><span class="sxs-lookup"><span data-stu-id="fd94d-299">Chinese Traditional</span></span></td>
        <td><span data-ttu-id="fd94d-300">zh-Hant.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-300">zh-Hant.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-301">zh-Hant.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-301">zh-Hant.lucene</span></span></td>        
    <tr>
    <tr>
        <td><span data-ttu-id="fd94d-302">Croate</span><span class="sxs-lookup"><span data-stu-id="fd94d-302">Croatian</span></span></td>
        <td><span data-ttu-id="fd94d-303">hr.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-303">hr.microsoft</span></span></td>
        <td/></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-304">Tchèque</span><span class="sxs-lookup"><span data-stu-id="fd94d-304">Czech</span></span></td>
        <td><span data-ttu-id="fd94d-305">cs.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-305">cs.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-306">cs.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-306">cs.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="fd94d-307">Danois</span><span class="sxs-lookup"><span data-stu-id="fd94d-307">Danish</span></span></td>
        <td><span data-ttu-id="fd94d-308">da.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-308">da.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-309">da.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-309">da.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="fd94d-310">Néerlandais</span><span class="sxs-lookup"><span data-stu-id="fd94d-310">Dutch</span></span></td>
        <td><span data-ttu-id="fd94d-311">nl.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-311">nl.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-312">nl.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-312">nl.lucene</span></span></td>    
    </tr>    
    <tr>
        <td><span data-ttu-id="fd94d-313">Français</span><span class="sxs-lookup"><span data-stu-id="fd94d-313">English</span></span></td>        
        <td><span data-ttu-id="fd94d-314">en.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-314">en.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-315">en.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-315">en.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-316">Estonien</span><span class="sxs-lookup"><span data-stu-id="fd94d-316">Estonian</span></span></td>
        <td><span data-ttu-id="fd94d-317">et.Microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-317">et.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-318">Finnois</span><span class="sxs-lookup"><span data-stu-id="fd94d-318">Finnish</span></span></td>
        <td><span data-ttu-id="fd94d-319">fi.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-319">fi.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-320">fi.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-320">fi.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="fd94d-321">Français</span><span class="sxs-lookup"><span data-stu-id="fd94d-321">French</span></span></td>
        <td><span data-ttu-id="fd94d-322">fr.Microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-322">fr.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-323">fr.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-323">fr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-324">Galicien</span><span class="sxs-lookup"><span data-stu-id="fd94d-324">Galician</span></span></td>
        <td></td>
        <td><span data-ttu-id="fd94d-325">gl.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-325">gl.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="fd94d-326">Allemand</span><span class="sxs-lookup"><span data-stu-id="fd94d-326">German</span></span></td>
        <td><span data-ttu-id="fd94d-327">de.Microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-327">de.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-328">de.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-328">de.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-329">Grec</span><span class="sxs-lookup"><span data-stu-id="fd94d-329">Greek</span></span></td>
        <td><span data-ttu-id="fd94d-330">el.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-330">el.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-331">el.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-331">el.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-332">Goudjrati</span><span class="sxs-lookup"><span data-stu-id="fd94d-332">Gujarati</span></span></td>
        <td><span data-ttu-id="fd94d-333">gu.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-333">gu.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-334">Hébreu</span><span class="sxs-lookup"><span data-stu-id="fd94d-334">Hebrew</span></span></td>
        <td><span data-ttu-id="fd94d-335">he.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-335">he.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-336">Hindi</span><span class="sxs-lookup"><span data-stu-id="fd94d-336">Hindi</span></span></td>
        <td><span data-ttu-id="fd94d-337">hi.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-337">hi.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-338">hi.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-338">hi.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-339">Hongrois</span><span class="sxs-lookup"><span data-stu-id="fd94d-339">Hungarian</span></span></td>        
        <td><span data-ttu-id="fd94d-340">hu.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-340">hu.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-341">hu.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-341">hu.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-342">Islandais</span><span class="sxs-lookup"><span data-stu-id="fd94d-342">Icelandic</span></span></td>
        <td><span data-ttu-id="fd94d-343">is.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-343">is.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-344">Indonésien</span><span class="sxs-lookup"><span data-stu-id="fd94d-344">Indonesian (Bahasa)</span></span></td>
        <td><span data-ttu-id="fd94d-345">id.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-345">id.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-346">id.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-346">id.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-347">Irlandais</span><span class="sxs-lookup"><span data-stu-id="fd94d-347">Irish</span></span></td>
        <td></td>
          <td><span data-ttu-id="fd94d-348">ga.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-348">ga.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-349">Italien</span><span class="sxs-lookup"><span data-stu-id="fd94d-349">Italian</span></span></td>
        <td><span data-ttu-id="fd94d-350">it.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-350">it.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-351">it.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-351">it.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-352">Japonais</span><span class="sxs-lookup"><span data-stu-id="fd94d-352">Japanese</span></span></td>
        <td><span data-ttu-id="fd94d-353">ja.Microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-353">ja.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-354">ja.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-354">ja.lucene</span></span></td>

    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-355">Kannada</span><span class="sxs-lookup"><span data-stu-id="fd94d-355">Kannada</span></span></td>
        <td><span data-ttu-id="fd94d-356">ka.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-356">ka.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-357">Coréen</span><span class="sxs-lookup"><span data-stu-id="fd94d-357">Korean</span></span></td>
        <td><span data-ttu-id="fd94d-358">ko.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-358">ko.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-359">ko.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-359">ko.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-360">Letton</span><span class="sxs-lookup"><span data-stu-id="fd94d-360">Latvian</span></span></td>        
        <td><span data-ttu-id="fd94d-361">lv.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-361">lv.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-362">lv.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-362">lv.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-363">Lituanien</span><span class="sxs-lookup"><span data-stu-id="fd94d-363">Lithuanian</span></span></td>
        <td><span data-ttu-id="fd94d-364">lt.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-364">lt.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-365">Malayalam</span><span class="sxs-lookup"><span data-stu-id="fd94d-365">Malayalam</span></span></td>
        <td><span data-ttu-id="fd94d-366">ml.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-366">ml.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-367">Malais (latin)</span><span class="sxs-lookup"><span data-stu-id="fd94d-367">Malay (Latin)</span></span></td>
        <td><span data-ttu-id="fd94d-368">ms.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-368">ms.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-369">Marathi</span><span class="sxs-lookup"><span data-stu-id="fd94d-369">Marathi</span></span></td>
        <td><span data-ttu-id="fd94d-370">mr.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-370">mr.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-371">Norvégien</span><span class="sxs-lookup"><span data-stu-id="fd94d-371">Norwegian</span></span></td>
        <td><span data-ttu-id="fd94d-372">nb.Microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-372">nb.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-373">no.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-373">no.lucene</span></span></td>        
    </tr>
      <tr>
        <td><span data-ttu-id="fd94d-374">Persan</span><span class="sxs-lookup"><span data-stu-id="fd94d-374">Persian</span></span></td>
        <td></td>
        <td><span data-ttu-id="fd94d-375">fa.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-375">fa.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="fd94d-376">Polonais</span><span class="sxs-lookup"><span data-stu-id="fd94d-376">Polish</span></span></td>
        <td><span data-ttu-id="fd94d-377">pl.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-377">pl.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-378">pl.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-378">pl.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-379">Portugais (Brésil)</span><span class="sxs-lookup"><span data-stu-id="fd94d-379">Portuguese (Brazil)</span></span></td>
        <td><span data-ttu-id="fd94d-380">pt-Br.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-380">pt-Br.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-381">pt-Br.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-381">pt-Br.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-382">Portugais (Portugal)</span><span class="sxs-lookup"><span data-stu-id="fd94d-382">Portuguese (Portugal)</span></span></td>
        <td><span data-ttu-id="fd94d-383">pt-Pt.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-383">pt-Pt.microsoft</span></span></td>        
        <td><span data-ttu-id="fd94d-384">pt-Pt.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-384">pt-Pt.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-385">Pendjabi</span><span class="sxs-lookup"><span data-stu-id="fd94d-385">Punjabi</span></span></td>
        <td><span data-ttu-id="fd94d-386">pa.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-386">pa.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-387">Roumain</span><span class="sxs-lookup"><span data-stu-id="fd94d-387">Romanian</span></span></td>
        <td><span data-ttu-id="fd94d-388">ro.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-388">ro.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-389">ro.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-389">ro.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-390">Russe</span><span class="sxs-lookup"><span data-stu-id="fd94d-390">Russian</span></span></td>
        <td><span data-ttu-id="fd94d-391">ru.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-391">ru.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-392">ru.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-392">ru.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-393">Serbe (cyrillique)</span><span class="sxs-lookup"><span data-stu-id="fd94d-393">Serbian (Cyrillic)</span></span></td>
        <td><span data-ttu-id="fd94d-394">sr-cyrillic.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-394">sr-cyrillic.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-395">Serbe (latin)</span><span class="sxs-lookup"><span data-stu-id="fd94d-395">Serbian (Latin)</span></span></td>
        <td><span data-ttu-id="fd94d-396">sr-latin.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-396">sr-latin.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-397">Slovaque</span><span class="sxs-lookup"><span data-stu-id="fd94d-397">Slovak</span></span></td>
        <td><span data-ttu-id="fd94d-398">sk.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-398">sk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-399">Slovène</span><span class="sxs-lookup"><span data-stu-id="fd94d-399">Slovenian</span></span></td>
        <td><span data-ttu-id="fd94d-400">sl.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-400">sl.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-401">Espagnol</span><span class="sxs-lookup"><span data-stu-id="fd94d-401">Spanish</span></span></td>
        <td><span data-ttu-id="fd94d-402">es.Microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-402">es.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-403">es.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-403">es.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-404">Suédois</span><span class="sxs-lookup"><span data-stu-id="fd94d-404">Swedish</span></span></td>
        <td><span data-ttu-id="fd94d-405">sv.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-405">sv.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-406">sv.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-406">sv.lucene</span></span></td>
    </tr>

    <tr>
        <td><span data-ttu-id="fd94d-407">Tamoul</span><span class="sxs-lookup"><span data-stu-id="fd94d-407">Tamil</span></span></td>
        <td><span data-ttu-id="fd94d-408">ta.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-408">ta.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-409">Télougou</span><span class="sxs-lookup"><span data-stu-id="fd94d-409">Telugu</span></span></td>
        <td><span data-ttu-id="fd94d-410">te.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-410">te.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-411">Thaï</span><span class="sxs-lookup"><span data-stu-id="fd94d-411">Thai</span></span></td>
        <td><span data-ttu-id="fd94d-412">th.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-412">th.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-413">th.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-413">th.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-414">Turc</span><span class="sxs-lookup"><span data-stu-id="fd94d-414">Turkish</span></span></td>
        <td><span data-ttu-id="fd94d-415">tr.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-415">tr.microsoft</span></span></td>
        <td><span data-ttu-id="fd94d-416">tr.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-416">tr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-417">Ukrainien</span><span class="sxs-lookup"><span data-stu-id="fd94d-417">Ukrainian</span></span></td>
        <td><span data-ttu-id="fd94d-418">uk.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-418">uk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-419">Ourdou</span><span class="sxs-lookup"><span data-stu-id="fd94d-419">Urdu</span></span></td>
        <td><span data-ttu-id="fd94d-420">ur.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-420">ur.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-421">Vietnamien</span><span class="sxs-lookup"><span data-stu-id="fd94d-421">Vietnamese</span></span></td>
        <td><span data-ttu-id="fd94d-422">vi.microsoft</span><span class="sxs-lookup"><span data-stu-id="fd94d-422">vi.microsoft</span></span></td>
        <td></td>
    </tr>
    <td colspan="3"><span data-ttu-id="fd94d-423">En outre, Azure Search fournit des configurations d'analyseur sans langage spécifié</span><span class="sxs-lookup"><span data-stu-id="fd94d-423">Additionally Azure Search provides language-agnostic analyzer configurations</span></span></td>
    <tr>
        <td><span data-ttu-id="fd94d-424">Pliage ASCII standard</span><span class="sxs-lookup"><span data-stu-id="fd94d-424">Standard ASCII Folding</span></span></td>
        <td><span data-ttu-id="fd94d-425">standardasciifolding.lucene</span><span class="sxs-lookup"><span data-stu-id="fd94d-425">standardasciifolding.lucene</span></span></td>
        <td>
        <ul>
            <li><span data-ttu-id="fd94d-426">Segmentation de texte Unicode (générateur de jetons standard)</span><span class="sxs-lookup"><span data-stu-id="fd94d-426">Unicode text segmentation (Standard Tokenizer)</span></span></li>
            <li><span data-ttu-id="fd94d-427">Filtre de pliage ASCII : convertit les caractères Unicode qui n'appartiennent pas au jeu des 127 premiers caractères ASCII dans leurs équivalents ASCII.</span><span class="sxs-lookup"><span data-stu-id="fd94d-427">ASCII folding filter - converts Unicode characters that don't belong to the set of first 127 ASCII characters into their ASCII equivalents.</span></span> <span data-ttu-id="fd94d-428">Cela est utile pour supprimer les signes diacritiques.</span><span class="sxs-lookup"><span data-stu-id="fd94d-428">This is useful for removing diacritics.</span></span></li>
        </ul>
        </td>
    </tr>
</table>

<span data-ttu-id="fd94d-429">Tous les analyseurs dont les noms sont annotés avec <i>lucene</i> s’appuient sur les [analyseurs de langue d’Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span><span class="sxs-lookup"><span data-stu-id="fd94d-429">All analyzers with names annotated with <i>lucene</i> are powered by [Apache Lucene's language analyzers](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span></span> <span data-ttu-id="fd94d-430">D’autres informations sur le filtre de pliage ASCII sont disponibles [ici](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span><span class="sxs-lookup"><span data-stu-id="fd94d-430">More information about the ASCII folding filter can be found [here](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span></span>

<span data-ttu-id="fd94d-431">**Générateurs de suggestions**</span><span class="sxs-lookup"><span data-stu-id="fd94d-431">**Suggesters**</span></span>

<span data-ttu-id="fd94d-432">Un `suggester` définit les champs d’un index qui sont utilisés pour prendre en charge la saisie semi-automatique dans les recherches.</span><span class="sxs-lookup"><span data-stu-id="fd94d-432">A `suggester` defines which fields in an index are used to support auto-complete in searches.</span></span> <span data-ttu-id="fd94d-433">En général, les chaînes recherchées partielles sont envoyées à l’ [API Suggestions](#Suggestions) pendant que l’utilisateur tape une requête de recherche, et l’API retourne un ensemble d’expressions suggérées.</span><span class="sxs-lookup"><span data-stu-id="fd94d-433">Typically partial search strings are sent to the [Suggestions API](#Suggestions) while the user is typing a search query, and the API returns a set of suggested phrases.</span></span> <span data-ttu-id="fd94d-434">Un générateur de suggestions que vous définissez dans l’index détermine quels champs sont utilisés pour générer les termes de recherche type-ahead.</span><span class="sxs-lookup"><span data-stu-id="fd94d-434">A suggester that you define in the index determines which fields are used to build the type-ahead search terms.</span></span> <span data-ttu-id="fd94d-435">Consultez [Générateurs de suggestion](#Suggesters) pour plus de détails sur la configuration.</span><span class="sxs-lookup"><span data-stu-id="fd94d-435">See [Suggesters](#Suggesters) for configuration details.</span></span>

<span data-ttu-id="fd94d-436">**Profils de score**</span><span class="sxs-lookup"><span data-stu-id="fd94d-436">**Scoring profiles**</span></span>

<span data-ttu-id="fd94d-437">Un `scoringProfile` définit les comportements de score personnalisés qui vous permettent de apparaître certains éléments plus haut dans les résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-437">A `scoringProfile` defines custom scoring behaviors that let you influence which items appear higher in the search results.</span></span> <span data-ttu-id="fd94d-438">Les profils de calcul de score sont constitués de pondérations et de fonctions de champ.</span><span class="sxs-lookup"><span data-stu-id="fd94d-438">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="fd94d-439">Pour les utiliser, vous spécifiez un profil par nom dans la chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-439">To use them, you specify a profile by name on the query string.</span></span>

<span data-ttu-id="fd94d-440">Un profil de score par défaut fonctionne en arrière-plan pour calculer un score de recherche pour chaque élément d’un jeu de résultats.</span><span class="sxs-lookup"><span data-stu-id="fd94d-440">A default scoring profile operates behind the scenes to compute a search score for every item in a result set.</span></span> <span data-ttu-id="fd94d-441">Vous pouvez utiliser le profil de score interne et sans nom.</span><span class="sxs-lookup"><span data-stu-id="fd94d-441">You can use the internal, unnamed scoring profile.</span></span> <span data-ttu-id="fd94d-442">Vous pouvez aussi définir `defaultScoringProfile` pour utiliser un profil personnalisé par défaut, appelé chaque fois qu’un profil personnalisé n’est pas spécifié dans la chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-442">Alternatively, set `defaultScoringProfile` to use a custom profile as the default, invoked whenever a custom profile is not specified on the query string.</span></span>

<span data-ttu-id="fd94d-443">Pour plus d’informations, consultez [Ajouter des profils de score à un index de recherche (API REST du Service Azure Search)](search-api-scoring-profiles-2015-02-28-preview.md) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-443">See [Add scoring profiles to a search index (Azure Search Service REST API)](search-api-scoring-profiles-2015-02-28-preview.md) for details.</span></span>

<span data-ttu-id="fd94d-444">**Options CORS**</span><span class="sxs-lookup"><span data-stu-id="fd94d-444">**CORS Options**</span></span>

<span data-ttu-id="fd94d-445">Le code Javascript côté client ne peut pas appeler les API par défaut, car le navigateur empêche toutes les requêtes cross-origin.</span><span class="sxs-lookup"><span data-stu-id="fd94d-445">Client-side Javascript cannot call any APIs by default since the browser will prevent all cross-origin requests.</span></span> <span data-ttu-id="fd94d-446">Activez CORS (partage des ressources cross-origin) en définissant l'attribut `corsOptions` pour autoriser les requêtes cross-origin dans l'index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-446">Enable CORS (Cross-Origin Resource Sharing) by setting the `corsOptions` attribute to allow cross-origin queries to your index.</span></span> <span data-ttu-id="fd94d-447">Notez que, pour des raisons de sécurité, seules les API de requête prennent en charge CORS.</span><span class="sxs-lookup"><span data-stu-id="fd94d-447">Note that only query APIs support CORS for security reasons.</span></span> <span data-ttu-id="fd94d-448">Les options suivantes peuvent être définies pour CORS :</span><span class="sxs-lookup"><span data-stu-id="fd94d-448">The following options can be set for CORS:</span></span>

* <span data-ttu-id="fd94d-449">`allowedOrigins` (obligatoire) : il s'agit d'une liste d'origines pouvant accéder à votre index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-449">`allowedOrigins` (required): This is a list of origins that will be granted access to your index.</span></span> <span data-ttu-id="fd94d-450">Cela signifie que le code Javascript distribué à partir de ces origines peut interroger votre index (en supposant qu'il fournisse la clé API appropriée).</span><span class="sxs-lookup"><span data-stu-id="fd94d-450">This means that any Javascript code served from those origins will be allowed to query your index (assuming it provides the correct API key).</span></span> <span data-ttu-id="fd94d-451">Chaque origine se présente généralement sous la forme `protocol://fully-qualified-domain-name:port` , bien que le port soit souvent omis.</span><span class="sxs-lookup"><span data-stu-id="fd94d-451">Each origin is typically of the form `protocol://fully-qualified-domain-name:port` although the port is often omitted.</span></span> <span data-ttu-id="fd94d-452">Consultez [cet article](http://go.microsoft.com/fwlink/?LinkId=330822) pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="fd94d-452">See [this article](http://go.microsoft.com/fwlink/?LinkId=330822) for more details.</span></span>
  * <span data-ttu-id="fd94d-453">Si vous voulez autoriser l'accès à toutes les origines, incluez `*` en tant qu'élément unique dans le tableau `allowedOrigins`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-453">If you want to allow access to all origins, include `*` as a single item in the `allowedOrigins` array.</span></span> <span data-ttu-id="fd94d-454">Notez que **cette pratique est déconseillée pour les services de recherche de production.**</span><span class="sxs-lookup"><span data-stu-id="fd94d-454">Note that **this is not recommended practice for production search services.**</span></span> <span data-ttu-id="fd94d-455">Toutefois, elle peut être utile à des fins de développement ou de débogage.</span><span class="sxs-lookup"><span data-stu-id="fd94d-455">However, it may be useful for development or debugging purposes.</span></span>
* <span data-ttu-id="fd94d-456">`maxAgeInSeconds` (facultatif) : les navigateurs utilisent cette valeur pour déterminer la durée (en secondes) de mise en cache des réponses CORS préliminaires.</span><span class="sxs-lookup"><span data-stu-id="fd94d-456">`maxAgeInSeconds` (optional): Browsers use this value to determine the duration (in seconds) to cache CORS preflight responses.</span></span> <span data-ttu-id="fd94d-457">Il doit s'agir d'un entier non négatif.</span><span class="sxs-lookup"><span data-stu-id="fd94d-457">This must be a non-negative integer.</span></span> <span data-ttu-id="fd94d-458">Plus cette valeur est importante, meilleures sont les performances, mais plus il faut de temps pour que les modifications apportées à la stratégie CORS prennent effet.</span><span class="sxs-lookup"><span data-stu-id="fd94d-458">The larger this value is, the better performance will be, but the longer it will take for CORS policy changes to take effect.</span></span> <span data-ttu-id="fd94d-459">Si la valeur n'est pas définie, une durée par défaut de 5 minutes est utilisée.</span><span class="sxs-lookup"><span data-stu-id="fd94d-459">If it is not set, a default duration of 5 minutes will be used.</span></span>

<span data-ttu-id="fd94d-460"><a name="CreateUpdateIndexExample"></a>
**Exemple de corps de requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-460"><a name="CreateUpdateIndexExample"></a>
**Request Body Example**</span></span>

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

<span data-ttu-id="fd94d-461">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="fd94d-461">**Response**</span></span>

<span data-ttu-id="fd94d-462">Pour une requête correcte : « 201 Créé ».</span><span class="sxs-lookup"><span data-stu-id="fd94d-462">For a successful request: "201 Created".</span></span>

<span data-ttu-id="fd94d-463">Par défaut, le corps de la réponse contient le code JSON de la définition d'index qui a été créée.</span><span class="sxs-lookup"><span data-stu-id="fd94d-463">By default the response body will contain the JSON for the index definition that was created.</span></span> <span data-ttu-id="fd94d-464">Si l'en-tête de la requête `Prefer` est défini avec la valeur `return=minimal`, le corps de la réponse est vide et le code d'état de réussite est « 204 Pas de contenu » au lieu de « 201 Créé ».</span><span class="sxs-lookup"><span data-stu-id="fd94d-464">If the `Prefer` request header is set to `return=minimal`, the response body will be empty and the success status code will be "204 No Content" instead of "201 Created".</span></span> <span data-ttu-id="fd94d-465">Cela est vrai, quelle que soit la méthode utilisée (PUT ou POST) pour créer l'index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-465">This is true regardless of whether PUT or POST was used to create the index.</span></span>

<span data-ttu-id="fd94d-466">**Notes**</span><span class="sxs-lookup"><span data-stu-id="fd94d-466">**Remarks**</span></span>

<span data-ttu-id="fd94d-467">Actuellement, la prise en charge des mises à jour de schéma d'index est limitée.</span><span class="sxs-lookup"><span data-stu-id="fd94d-467">Currently, there is limited support for index schema updates.</span></span> <span data-ttu-id="fd94d-468">Les mises à jour de schéma qui nécessitent une réindexation, par exemple la modification des types de champs, ne sont pas prises en charge pour le moment.</span><span class="sxs-lookup"><span data-stu-id="fd94d-468">Any schema updates that would require re-indexing such as changing field types are not currently supported.</span></span> <span data-ttu-id="fd94d-469">De nouveaux champs peuvent être ajoutés à un index existant à tout moment, mais les champs existants ne peuvent pas être modifiés ni supprimés.</span><span class="sxs-lookup"><span data-stu-id="fd94d-469">Although existing fields cannot be changed or deleted, new fields can be added to an existing index at any time.</span></span> <span data-ttu-id="fd94d-470">Quand vous ajoutez un nouveau champ, tous les documents existants de l'index auront automatiquement une valeur null pour ce champ.</span><span class="sxs-lookup"><span data-stu-id="fd94d-470">When a new field is added, all existing documents in the index will automatically have a null value for that field.</span></span> <span data-ttu-id="fd94d-471">Aucun espace de stockage supplémentaire n'est consommé jusqu'à ce que de nouveaux documents soient ajoutés à l'index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-471">No additional storage space will be consumed until new documents are added to the index.</span></span>

<a name="Suggesters"></a>

## <a name="suggesters"></a><span data-ttu-id="fd94d-472">Générateurs de suggestions</span><span class="sxs-lookup"><span data-stu-id="fd94d-472">Suggesters</span></span>
<span data-ttu-id="fd94d-473">La fonctionnalité de suggestions dans Azure Search est une fonctionnalité de requête type-ahead ou de saisie semi-automatique, qui fournit une liste de termes de recherche potentiels en réponse à des chaînes partielles entrées dans une zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-473">The suggestions feature in Azure Search is a type-ahead or auto-complete query capability, providing a list of potential search terms in response to partial string inputs entered into a search box.</span></span> <span data-ttu-id="fd94d-474">Vous avez probablement remarqué des suggestions de requête lors de l’utilisation de moteurs de recherche web commerciaux : la saisie de « NET » dans Bing génère une liste de termes pour « .NET 4.5 », « .NET Framework 3.5 », etc.</span><span class="sxs-lookup"><span data-stu-id="fd94d-474">You've probably noticed query suggestions when using commercial web search engines: typing ".NET" in Bing produces a list of terms for ".NET 4.5", ".NET Framework 3.5", and so forth.</span></span> <span data-ttu-id="fd94d-475">Lorsque vous utilisez l’API REST du service de recherche, l’implémentation des suggestions dans une application Azure Search personnalisée requiert les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fd94d-475">When using the Search service REST API, implementing suggestions in a custom Azure Search application requires the following:</span></span>

* <span data-ttu-id="fd94d-476">Activer les suggestions en ajoutant une construction de **générateur de suggestion** dans votre index, en donnant le nom, le mode de recherche et la liste des champs pour lesquels la recherche type-ahead est appelée.</span><span class="sxs-lookup"><span data-stu-id="fd94d-476">Enable suggestions by adding a **suggester** construction in your index, giving the name, search mode, and a list of fields for which type-ahead is invoked.</span></span> <span data-ttu-id="fd94d-477">Par exemple, si vous spécifiez « cityName » comme champ de la source, la saisie de la chaîne de recherche partielle « Sea » affiche « Seattle », « Seaside » et « Seatac » (trois noms réels de ville) comme suggestions de requête pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fd94d-477">For example, if you specify "cityName" as a source field, typing a partial search string of "Sea" will result in "Seattle", "Seaside", and "Seatac" (all three are actual city names) offered up as query suggestions to the user.</span></span>
* <span data-ttu-id="fd94d-478">Appeler les suggestions en invoquant l’ [API Suggestions](#Suggestions) dans votre code d’application.</span><span class="sxs-lookup"><span data-stu-id="fd94d-478">Invoke suggestions by calling the [Suggestions API](#Suggestions) in your application code.</span></span> <span data-ttu-id="fd94d-479">En général, les chaînes de recherche partielles sont envoyées au service pendant que l’utilisateur entre une requête de recherche, et l’API retourne un ensemble d’expressions suggérées.</span><span class="sxs-lookup"><span data-stu-id="fd94d-479">Typically partial search strings are sent to the service while the user is typing a search query, and this API returns a set of suggested phrases.</span></span>

<span data-ttu-id="fd94d-480">Cet article explique comment configurer un **générateur de suggestions**.</span><span class="sxs-lookup"><span data-stu-id="fd94d-480">This article explains how to configure a **suggester**.</span></span> <span data-ttu-id="fd94d-481">Vous devez également examiner l’ [API Suggestions](#Suggestions) pour plus d’informations sur l’utilisation d’un générateur de suggestions.</span><span class="sxs-lookup"><span data-stu-id="fd94d-481">You should also review the [Suggestions API](#Suggestions) for details on how a suggester is used.</span></span>

<span data-ttu-id="fd94d-482">**Utilisation**</span><span class="sxs-lookup"><span data-stu-id="fd94d-482">**Usage**</span></span>

<span data-ttu-id="fd94d-483">`Suggesters` sont créés dans l’index et fonctionnent de façon optimale quand ils sont utilisés pour suggérer des documents spécifiques plutôt que des expressions ou des termes isolés.</span><span class="sxs-lookup"><span data-stu-id="fd94d-483">`Suggesters` are created in the index and work best when used to suggest specific documents rather than loose terms or phrases.</span></span> <span data-ttu-id="fd94d-484">Les champs les plus appropriés sont les titres, les noms et d’autres expressions relativement courtes qui peuvent identifier un élément.</span><span class="sxs-lookup"><span data-stu-id="fd94d-484">The best candidate fields are titles, names, and other relatively short phrases that can identify an item.</span></span> <span data-ttu-id="fd94d-485">Les champs les moins efficaces sont les champs répétitifs, tels que les catégories et les balises, ou les champs très longs, tels que les champs des descriptions ou des commentaires.</span><span class="sxs-lookup"><span data-stu-id="fd94d-485">Less effective are repetitive fields, such as categories and tags, or very long fields such as descriptions or comments fields.</span></span>

<span data-ttu-id="fd94d-486">Dans le cadre de la définition d’index, vous pouvez ajouter un générateur de suggestions unique à la collection `suggesters` .</span><span class="sxs-lookup"><span data-stu-id="fd94d-486">As part of the index definition, you can add a single suggester to the `suggesters` collection.</span></span> <span data-ttu-id="fd94d-487">Les propriétés suivantes définissent un générateur de suggestions :</span><span class="sxs-lookup"><span data-stu-id="fd94d-487">Properties that define a suggester include the following:</span></span>

* <span data-ttu-id="fd94d-488">`name`: nom du générateur de suggestions.</span><span class="sxs-lookup"><span data-stu-id="fd94d-488">`name`: The name of the suggester.</span></span> <span data-ttu-id="fd94d-489">Vous utilisez le nom du générateur de suggestions quand vous appelez l'API `suggest` .</span><span class="sxs-lookup"><span data-stu-id="fd94d-489">You use the name of the suggester when calling the `suggest` API.</span></span>
* <span data-ttu-id="fd94d-490">`searchMode`: stratégie utilisée pour rechercher des expressions candidates.</span><span class="sxs-lookup"><span data-stu-id="fd94d-490">`searchMode`: The strategy used to search for candidate phrases.</span></span> <span data-ttu-id="fd94d-491">Le seul mode actuellement pris en charge est `analyzingInfixMatching`, qui effectue une correspondance flexible des expressions en début ou au milieu des phrases.</span><span class="sxs-lookup"><span data-stu-id="fd94d-491">The only mode currently supported is `analyzingInfixMatching`, which performs flexible matching of phrases at the beginning or in the middle of sentences.</span></span>
* <span data-ttu-id="fd94d-492">`sourceFields`: liste d’un ou de plusieurs champs constituant la source du contenu pour des suggestions.</span><span class="sxs-lookup"><span data-stu-id="fd94d-492">`sourceFields`: A list of one or more fields that are the source of the content for suggestions.</span></span> <span data-ttu-id="fd94d-493">Seuls les champs de type `Edm.String` et `Collection(Edm.String)` peuvent être des sources pour des suggestions.</span><span class="sxs-lookup"><span data-stu-id="fd94d-493">Only fields of type `Edm.String` and `Collection(Edm.String)` may be sources for suggestions.</span></span> <span data-ttu-id="fd94d-494">Seuls les champs qui n’ont pas un analyseur de langue personnalisé défini peuvent être utilisés.</span><span class="sxs-lookup"><span data-stu-id="fd94d-494">Only fields that don't have a custom language analyzer set can be used.</span></span>

<span data-ttu-id="fd94d-495">**Exemple de générateur de suggestions**</span><span class="sxs-lookup"><span data-stu-id="fd94d-495">**Suggester Example**</span></span>

<span data-ttu-id="fd94d-496">Un générateur de suggestions fait partie de l’index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-496">A suggester is part of the index.</span></span> <span data-ttu-id="fd94d-497">Un seul générateur de suggestions peut exister dans la collection `suggesters` de la version actuelle, à côté de la collection des champs et de `scoringProfiles`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-497">Only one suggester can exist in the `suggesters` collection in the current version, alongside the fields collection and `scoringProfiles`.</span></span>

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> <span data-ttu-id="fd94d-498">Si vous avez utilisé la version préliminaire publique d’Azure Search, `suggesters` remplace une propriété booléenne (`"suggestions": false`) plus ancienne qui prenait en charge uniquement des suggestions de préfixe pour les chaînes courtes (de 3 à 25 caractères).</span><span class="sxs-lookup"><span data-stu-id="fd94d-498">If you used the public preview version of Azure Search, `suggesters` replaces an older boolean property (`"suggestions": false`) that only supported prefix suggestions for short strings (3-25 characters).</span></span> <span data-ttu-id="fd94d-499">Son remplacement, `suggesters`, prend en charge la correspondance infixe qui recherche des termes correspondants au début ou au milieu du contenu du champ, avec une meilleure tolérance pour les erreurs dans les chaînes recherchées.</span><span class="sxs-lookup"><span data-stu-id="fd94d-499">Its replacement, `suggesters`, supports infix matching that finds matching terms at the beginning or in the middle of field content, with better tolerance for mistakes in search strings.</span></span> <span data-ttu-id="fd94d-500">À partir de la version disponible sur le marché, il s'agit de la seule implémentation de l'API des suggestions.</span><span class="sxs-lookup"><span data-stu-id="fd94d-500">Starting with the generally available release, this is now the only implementation of the suggestions API.</span></span> <span data-ttu-id="fd94d-501">La propriété `suggestions` plus ancienne introduite dans `api-version=2014-07-31-Preview` continue de fonctionner dans cette version, mais n’est pas opérationnelle dans la version `2015-02-28` ou les version ultérieures d’Azure Search.</span><span class="sxs-lookup"><span data-stu-id="fd94d-501">The older `suggestions` property that was introduced in `api-version=2014-07-31-Preview` continues to work in that version, but is not operational in the `2015-02-28` or later versions of Azure Search.</span></span>
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a><span data-ttu-id="fd94d-502">Mise à jour d'index</span><span class="sxs-lookup"><span data-stu-id="fd94d-502">Update Index</span></span>
<span data-ttu-id="fd94d-503">Vous pouvez mettre à jour un index existant dans Azure Search à l'aide d'une requête HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="fd94d-503">You can update an existing index within Azure Search using an HTTP PUT request.</span></span> <span data-ttu-id="fd94d-504">Les mises à jour peuvent inclure l'ajout de nouveaux champs au schéma existant, la modification des options CORS et la modification des profils de calcul de score.</span><span class="sxs-lookup"><span data-stu-id="fd94d-504">Updates can include adding new fields to the existing schema, modifying CORS options, and modifying scoring profiles.</span></span> <span data-ttu-id="fd94d-505">Pour plus d'informations, consultez [Ajout de profils de calcul de score](https://msdn.microsoft.com/library/azure/dn798928.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-505">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> <span data-ttu-id="fd94d-506">Vous spécifiez le nom de l'index à mettre à jour sur l'URI de la requête :</span><span class="sxs-lookup"><span data-stu-id="fd94d-506">You specify the name of the index to update on the request URI:</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="fd94d-507">**Important :** la prise en charge des mises à jour de schéma d'index est limitée aux opérations qui ne nécessitent pas la reconstruction de l'index de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-507">**Important:** Support for index schema updates is limited to operations that don't require rebuilding the search index.</span></span> <span data-ttu-id="fd94d-508">Les mises à jour de schéma qui nécessitent une réindexation, par exemple la modification des types de champs, ne sont pas prises en charge pour le moment.</span><span class="sxs-lookup"><span data-stu-id="fd94d-508">Any schema updates that would require re-indexing, such as changing field types, are not currently supported.</span></span> <span data-ttu-id="fd94d-509">De nouveaux champs peuvent être ajoutés à tout moment, mais les champs existants ne peuvent pas être modifiés ni supprimés.</span><span class="sxs-lookup"><span data-stu-id="fd94d-509">New fields can be added at any time, although existing fields cannot be changed or deleted.</span></span> <span data-ttu-id="fd94d-510">Il en va de même pour les `suggesters`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-510">The same applies to `suggesters`.</span></span> <span data-ttu-id="fd94d-511">De nouveaux champs peuvent être ajoutés à un générateur de suggestions au moment où les champs sont ajoutés, mais les champs ne peuvent pas être supprimés des `suggesters` et des champs existants ne peuvent pas être ajoutés à des `suggesters`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-511">New fields may be added to a suggester at the time the fields are added, but fields cannot be removed from `suggesters` and existing fields cannot be added to `suggesters`.</span></span>

<span data-ttu-id="fd94d-512">Quand vous ajoutez un nouveau champ à un index, tous les documents existants de l'index auront automatiquement une valeur null pour ce champ.</span><span class="sxs-lookup"><span data-stu-id="fd94d-512">When adding a new field to an index, all existing documents in the index will automatically have a null value for that field.</span></span> <span data-ttu-id="fd94d-513">Aucun espace de stockage supplémentaire n'est consommé jusqu'à ce que de nouveaux documents soient ajoutés à l'index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-513">No additional storage space will be consumed until new documents are added to the index.</span></span>

<span data-ttu-id="fd94d-514">**Requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-514">**Request**</span></span>

<span data-ttu-id="fd94d-515">Le protocole HTTPS est requis pour toutes les requêtes de service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-515">HTTPS is required for all service requests.</span></span> <span data-ttu-id="fd94d-516">La requête **Update Index** est construite à l'aide de HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="fd94d-516">The **Update Index** request is constructed using HTTP PUT.</span></span> <span data-ttu-id="fd94d-517">Avec la méthode PUT, le nom d'index fait partie de l'URL.</span><span class="sxs-lookup"><span data-stu-id="fd94d-517">With PUT, the index name is part of the URL.</span></span> <span data-ttu-id="fd94d-518">Si l'index n'existe pas, il est créé.</span><span class="sxs-lookup"><span data-stu-id="fd94d-518">If the index doesn't exist, it is created.</span></span> <span data-ttu-id="fd94d-519">S'il existe déjà, il est mis à jour en fonction de la nouvelle définition.</span><span class="sxs-lookup"><span data-stu-id="fd94d-519">If the index already exists, it is updated to the new definition.</span></span>

<span data-ttu-id="fd94d-520">Le nom d'index doit être en minuscules, commencer par une lettre ou un chiffre, ne contenir ni barres obliques ni points, et comprendre moins de 128 caractères.</span><span class="sxs-lookup"><span data-stu-id="fd94d-520">The index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="fd94d-521">Après la lettre ou le chiffre du début, le nom d'index peut comprendre des lettres, des chiffres et des tirets (non consécutifs).</span><span class="sxs-lookup"><span data-stu-id="fd94d-521">After starting the index name with a letter or number, the rest of the name can include any letter, number and dashes, as long as the dashes are not consecutive.</span></span>

<span data-ttu-id="fd94d-522">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="fd94d-522">`api-version=[string]` (required).</span></span> <span data-ttu-id="fd94d-523">La version préliminaire est `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-523">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="fd94d-524">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-524">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="fd94d-525">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-525">**Request Headers**</span></span>

<span data-ttu-id="fd94d-526">La liste suivante décrit les en-têtes de requête obligatoires et facultatifs.</span><span class="sxs-lookup"><span data-stu-id="fd94d-526">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="fd94d-527">`Content-Type`: requis.</span><span class="sxs-lookup"><span data-stu-id="fd94d-527">`Content-Type`: Required.</span></span> <span data-ttu-id="fd94d-528">À définir avec la valeur `application/json`</span><span class="sxs-lookup"><span data-stu-id="fd94d-528">Set this to `application/json`</span></span>
* <span data-ttu-id="fd94d-529">`api-key`: requis.</span><span class="sxs-lookup"><span data-stu-id="fd94d-529">`api-key`: Required.</span></span> <span data-ttu-id="fd94d-530">L'en-tête `api-key` est utilisé pour authentifier la requête auprès de votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-530">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="fd94d-531">Il s'agit d'une valeur de type chaîne de caractères, unique pour votre service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-531">It is a string value, unique to your service.</span></span> <span data-ttu-id="fd94d-532">La requête **Update Index** doit inclure un en-tête `api-key` défini avec la valeur de votre clé d’administration (par opposition à une clé de requête).</span><span class="sxs-lookup"><span data-stu-id="fd94d-532">The **Update Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="fd94d-533">Vous avez également besoin du nom du service pour construire l'URL de la requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-533">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="fd94d-534">Vous pouvez obtenir le nom du service et l'en-tête `api-key` à partir de votre tableau de bord de service dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fd94d-534">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="fd94d-535">Pour obtenir de l'aide sur la navigation dans les pages, consultez [Création d'un service Azure Search dans le portail](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-535">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="fd94d-536">**Syntaxe du corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-536">**Request Body Syntax**</span></span>

<span data-ttu-id="fd94d-537">Lors de la mise à jour d'un index existant, le corps doit inclure la définition de schéma d'origine et les nouveaux champs que vous ajoutez, ainsi que les profils de score modifiés et les options CORS, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="fd94d-537">When updating an existing index, the body must include the original schema definition, plus the new fields you are adding, as well as the modified scoring profiles, suggesters and CORS options, if any.</span></span> <span data-ttu-id="fd94d-538">Si vous ne modifiez pas les profils de score et les options CORS, vous devez inclure leur version d'origine, créée en même temps que l'index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-538">If you are not modifying the scoring profiles and CORS options, you must include the originals from when the index was created.</span></span> <span data-ttu-id="fd94d-539">En général, le meilleur modèle à utiliser pour les mises à jour est la récupération de la définition d'index avec une méthode GET, sa modification, puis sa mise à jour avec la méthode PUT.</span><span class="sxs-lookup"><span data-stu-id="fd94d-539">In general the best pattern to use for updates is to retrieve the index definition with a GET, modify it, then update it with PUT.</span></span>

<span data-ttu-id="fd94d-540">La syntaxe de schéma utilisée pour créer un index est reproduite ici par commodité.</span><span class="sxs-lookup"><span data-stu-id="fd94d-540">The schema syntax used to create an index is reproduced here for convenience.</span></span> <span data-ttu-id="fd94d-541">Consultez la section [Création d'index](#CreateIndex) pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="fd94d-541">See [Create Index](#CreateIndex) for more details.</span></span>

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of the analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of the search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of the indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in the future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies to searchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading to now over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter to be passed in queries to use as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (the distance in kilometers from the reference location where the boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter to be passed in queries to specify list of tags to compare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


<span data-ttu-id="fd94d-542">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="fd94d-542">**Response**</span></span>

<span data-ttu-id="fd94d-543">Pour une requête correcte : « 204 Pas de contenu ».</span><span class="sxs-lookup"><span data-stu-id="fd94d-543">For a successful request: "204 No Content".</span></span>

<span data-ttu-id="fd94d-544">Par défaut, le corps de la réponse est vide.</span><span class="sxs-lookup"><span data-stu-id="fd94d-544">By default the response body will be empty.</span></span> <span data-ttu-id="fd94d-545">Toutefois, si l'en-tête de la requête `Prefer` est défini avec la valeur `return=representation`, le corps de la réponse contient le code JSON pour la définition d'index mise à jour.</span><span class="sxs-lookup"><span data-stu-id="fd94d-545">However, if the `Prefer` request header is set to `return=representation`, the response body will contain the JSON for the index definition that was updated.</span></span> <span data-ttu-id="fd94d-546">Dans ce cas, le code d'état de réussite est « 200 OK ».</span><span class="sxs-lookup"><span data-stu-id="fd94d-546">In this case, the success status code will be "200 OK".</span></span>

<span data-ttu-id="fd94d-547">**Mise à jour de la définition d’index avec des analyseurs personnalisés**</span><span class="sxs-lookup"><span data-stu-id="fd94d-547">**Updating index definition with custom analyzers**</span></span>

<span data-ttu-id="fd94d-548">Une fois défini, un analyseur, un générateur de jetons, un filtre de jetons ou un filtre de caractères ne peut pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="fd94d-548">Once an analyzer, a tokenizer, a token filter or a char filter is defined, it cannot be modified.</span></span> <span data-ttu-id="fd94d-549">D’autres peuvent être ajoutés à un index existant à condition que l’indicateur `allowIndexDowntime` soit défini comme true dans la demande de mise à jour de l’index :</span><span class="sxs-lookup"><span data-stu-id="fd94d-549">New ones can be added to an existing index only if the `allowIndexDowntime` flag is set to true in the index update request:</span></span> 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

<span data-ttu-id="fd94d-550">Notez que cette opération placera votre index hors connexion pendant au moins quelques secondes, ce qui entraînera l’échec de vos demandes d’indexation et de requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-550">Note that this operation will put your index offline for at least a few seconds, causing your indexing and query requests to fail.</span></span> <span data-ttu-id="fd94d-551">Les performances et la disponibilité d’écriture de l’index peuvent être altérées pendant plusieurs minutes après la mise à jour de l’index, ou plus longtemps pour les très grands index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-551">Performance and write availability of the index can be impaired for several minutes after the index is updated, or longer for very large indexes.</span></span>

<a name="ListIndexes"></a>

## <a name="list-indexes"></a><span data-ttu-id="fd94d-552">Liste des index</span><span class="sxs-lookup"><span data-stu-id="fd94d-552">List Indexes</span></span>
<span data-ttu-id="fd94d-553">L'opération **List Indexes** retourne une liste des index actuellement utilisés dans votre service Azure Search.</span><span class="sxs-lookup"><span data-stu-id="fd94d-553">The **List Indexes** operation returns a list of the indexes currently in your Azure Search service.</span></span>

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="fd94d-554">**Requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-554">**Request**</span></span>

<span data-ttu-id="fd94d-555">Le protocole HTTPS est requis pour toutes les requêtes de service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-555">HTTPS is required for all service requests.</span></span> <span data-ttu-id="fd94d-556">La requête **List Indexes** peut être construite à l'aide de la méthode GET.</span><span class="sxs-lookup"><span data-stu-id="fd94d-556">The **List Indexes** request can be constructed using the GET method.</span></span>

<span data-ttu-id="fd94d-557">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="fd94d-557">`api-version=[string]` (required).</span></span> <span data-ttu-id="fd94d-558">La version préliminaire est `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-558">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="fd94d-559">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-559">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="fd94d-560">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-560">**Request Headers**</span></span>

<span data-ttu-id="fd94d-561">La liste suivante décrit les en-têtes de requête obligatoires et facultatifs.</span><span class="sxs-lookup"><span data-stu-id="fd94d-561">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="fd94d-562">`api-key`: obligatoire.</span><span class="sxs-lookup"><span data-stu-id="fd94d-562">`api-key`: Required.</span></span> <span data-ttu-id="fd94d-563">L'en-tête `api-key` est utilisé pour authentifier la requête auprès de votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-563">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="fd94d-564">Il s'agit d'une valeur de type chaîne de caractères, unique pour votre service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-564">It is a string value, unique to your service.</span></span> <span data-ttu-id="fd94d-565">La requête **List Indexes** doit inclure un en-tête `api-key` défini avec la valeur d’une clé d’administration (par opposition à une clé de requête).</span><span class="sxs-lookup"><span data-stu-id="fd94d-565">The **List Indexes** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="fd94d-566">Vous avez également besoin du nom du service pour construire l'URL de la requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-566">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="fd94d-567">Vous pouvez obtenir le nom du service et l'en-tête `api-key` à partir de votre tableau de bord de service dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fd94d-567">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="fd94d-568">Pour obtenir de l'aide sur la navigation dans les pages, consultez [Création d'un service Azure Search dans le portail](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-568">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="fd94d-569">**Corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-569">**Request Body**</span></span>

<span data-ttu-id="fd94d-570">Aucune.</span><span class="sxs-lookup"><span data-stu-id="fd94d-570">None.</span></span>

<span data-ttu-id="fd94d-571">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="fd94d-571">**Response**</span></span>

<span data-ttu-id="fd94d-572">Code d'état : 200 OK est retourné pour une réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="fd94d-572">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="fd94d-573">Voici un exemple de corps de réponse :</span><span class="sxs-lookup"><span data-stu-id="fd94d-573">Here is an example response body:</span></span>

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

<span data-ttu-id="fd94d-574">Notez que vous pouvez filtrer la réponse pour afficher uniquement les propriétés qui vous intéressent.</span><span class="sxs-lookup"><span data-stu-id="fd94d-574">Note that you can filter the response down to just the properties you're interested in.</span></span> <span data-ttu-id="fd94d-575">Par exemple, si vous voulez uniquement une liste des noms d'index, utilisez l'option de requête OData `$select` :</span><span class="sxs-lookup"><span data-stu-id="fd94d-575">For example, if you want only a list of index names, use the OData `$select` query option:</span></span>

    GET /indexes?api-version=2015-02-28-Preview&$select=name

<span data-ttu-id="fd94d-576">Dans ce cas, la réponse de l'exemple ci-dessus apparaît comme suit :</span><span class="sxs-lookup"><span data-stu-id="fd94d-576">In this case, the response from the above example would appear as follows:</span></span>

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

<span data-ttu-id="fd94d-577">Cette technique est utile pour économiser de la bande passante si votre service de recherche contient un grand nombre d'index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-577">This is a useful technique to save bandwidth if you have a lot of indexes in your Search service.</span></span>

<a name="GetIndex"></a>

## <a name="get-index"></a><span data-ttu-id="fd94d-578">Obtention d'index</span><span class="sxs-lookup"><span data-stu-id="fd94d-578">Get Index</span></span>
<span data-ttu-id="fd94d-579">L'opération **Get Index** obtient la définition d'index auprès d'Azure Search.</span><span class="sxs-lookup"><span data-stu-id="fd94d-579">The **Get Index** operation gets the index definition from Azure Search.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="fd94d-580">**Requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-580">**Request**</span></span>

<span data-ttu-id="fd94d-581">Le protocole HTTPS est requis pour les requêtes de service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-581">HTTPS is required for service requests.</span></span> <span data-ttu-id="fd94d-582">La requête **Get Index** peut être construite à l'aide de la méthode GET.</span><span class="sxs-lookup"><span data-stu-id="fd94d-582">The **Get Index** request can be constructed using the GET method.</span></span>

<span data-ttu-id="fd94d-583">Le [nom d’index] de l’URI de la requête spécifie l’index à retourner à partir de la collection d’index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-583">The [index name] in the request URI specifies which index to return from the indexes collection.</span></span>

<span data-ttu-id="fd94d-584">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="fd94d-584">`api-version=[string]` (required).</span></span> <span data-ttu-id="fd94d-585">La version préliminaire est `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-585">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="fd94d-586">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-586">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="fd94d-587">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-587">**Request Headers**</span></span>

<span data-ttu-id="fd94d-588">La liste suivante décrit les en-têtes de requête obligatoires et facultatifs.</span><span class="sxs-lookup"><span data-stu-id="fd94d-588">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="fd94d-589">`api-key` : l'en-tête `api-key` est utilisé pour authentifier la requête auprès de votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-589">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="fd94d-590">Il s'agit d'une valeur de type chaîne de caractères, unique pour votre service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-590">It is a string value, unique to your service.</span></span> <span data-ttu-id="fd94d-591">La requête **Get Index** doit inclure un en-tête `api-key` défini avec la valeur d’une clé d’administration (par opposition à une clé de requête).</span><span class="sxs-lookup"><span data-stu-id="fd94d-591">The **Get Index** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="fd94d-592">Vous avez également besoin du nom du service pour construire l'URL de la requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-592">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="fd94d-593">Vous pouvez obtenir le nom du service et l'en-tête `api-key` à partir de votre tableau de bord de service dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fd94d-593">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="fd94d-594">Pour obtenir de l'aide sur la navigation dans les pages, consultez [Création d'un service Azure Search dans le portail](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-594">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="fd94d-595">**Corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-595">**Request Body**</span></span>

<span data-ttu-id="fd94d-596">Aucune.</span><span class="sxs-lookup"><span data-stu-id="fd94d-596">None.</span></span>

<span data-ttu-id="fd94d-597">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="fd94d-597">**Response**</span></span>

<span data-ttu-id="fd94d-598">Code d'état : 200 OK est retourné pour une réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="fd94d-598">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="fd94d-599">Consultez l'exemple de document JSON dans [Création et mise à jour d'un index](#CreateUpdateIndexExample) pour obtenir un exemple de charge utile de la réponse.</span><span class="sxs-lookup"><span data-stu-id="fd94d-599">See the example JSON in [Creating and Updating an Index](#CreateUpdateIndexExample) for an example of the response payload.</span></span>

<a name="DeleteIndex"></a>

## <a name="delete-index"></a><span data-ttu-id="fd94d-600">Suppression d'index</span><span class="sxs-lookup"><span data-stu-id="fd94d-600">Delete Index</span></span>
<span data-ttu-id="fd94d-601">L'opération **Delete Index** supprime de votre service Azure Search un index et les documents associés.</span><span class="sxs-lookup"><span data-stu-id="fd94d-601">The **Delete Index** operation removes an index and associated documents from your Azure Search service.</span></span> <span data-ttu-id="fd94d-602">Vous pouvez obtenir le nom de l'index à partir du tableau de bord de service dans le portail Azure ou à partir de l'API.</span><span class="sxs-lookup"><span data-stu-id="fd94d-602">You can get the index name from the service dashboard in the Azure portal, or from the API.</span></span> <span data-ttu-id="fd94d-603">Consultez la section [List Indexes](#ListIndexes) pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="fd94d-603">See [List Indexes](#ListIndexes) for details.</span></span>

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="fd94d-604">**Requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-604">**Request**</span></span>

<span data-ttu-id="fd94d-605">Le protocole HTTPS est requis pour les requêtes de service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-605">HTTPS is required for service requests.</span></span> <span data-ttu-id="fd94d-606">La requête **Delete Index** peut être construite à l'aide de la méthode DELETE.</span><span class="sxs-lookup"><span data-stu-id="fd94d-606">The **Delete Index** request can be constructed using the DELETE method.</span></span>

<span data-ttu-id="fd94d-607">Le [nom d’index] de l’URI de la requête spécifie l’index à supprimer dans la collection d’index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-607">The [index name] in the request URI specifies which index to delete from the indexes collection.</span></span>

<span data-ttu-id="fd94d-608">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="fd94d-608">`api-version=[string]` (required).</span></span> <span data-ttu-id="fd94d-609">La version préliminaire est `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-609">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="fd94d-610">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-610">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="fd94d-611">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-611">**Request Headers**</span></span>

<span data-ttu-id="fd94d-612">La liste suivante décrit les en-têtes de requête obligatoires et facultatifs.</span><span class="sxs-lookup"><span data-stu-id="fd94d-612">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="fd94d-613">`api-key`: obligatoire.</span><span class="sxs-lookup"><span data-stu-id="fd94d-613">`api-key`: Required.</span></span> <span data-ttu-id="fd94d-614">L'en-tête `api-key` est utilisé pour authentifier la requête auprès de votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-614">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="fd94d-615">Il s'agit d'une valeur de chaîne, unique pour l'URL de votre service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-615">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="fd94d-616">La requête **Delete Index** doit inclure un en-tête `api-key` défini avec la valeur de votre clé d’administration (par opposition à une clé de requête).</span><span class="sxs-lookup"><span data-stu-id="fd94d-616">The **Delete Index** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="fd94d-617">Vous avez également besoin du nom du service pour construire l'URL de la requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-617">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="fd94d-618">Vous pouvez obtenir le nom du service et l'en-tête `api-key` à partir de votre tableau de bord de service dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fd94d-618">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="fd94d-619">Pour obtenir de l'aide sur la navigation dans les pages, consultez [Création d'un service Azure Search dans le portail](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-619">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="fd94d-620">**Corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-620">**Request Body**</span></span>

<span data-ttu-id="fd94d-621">Aucune.</span><span class="sxs-lookup"><span data-stu-id="fd94d-621">None.</span></span>

<span data-ttu-id="fd94d-622">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="fd94d-622">**Response**</span></span>

<span data-ttu-id="fd94d-623">Code d'état : 204 Pas de contenu est renvoyé en cas de réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="fd94d-623">Status Code: 204 No Content is returned for a successful response.</span></span>

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a><span data-ttu-id="fd94d-624">Obtention de statistiques d'index</span><span class="sxs-lookup"><span data-stu-id="fd94d-624">Get Index Statistics</span></span>
<span data-ttu-id="fd94d-625">L'opération **Get Index Statistics** retourne d'Azure Search un nombre de documents pour l'index actuel, ainsi que l'utilisation du stockage.</span><span class="sxs-lookup"><span data-stu-id="fd94d-625">The **Get Index Statistics** operation returns from Azure Search a document count for the current index, plus storage usage.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> <span data-ttu-id="fd94d-626">Les statistiques sur le nombre de documents et la taille du stockage sont collectées à intervalles de quelques minutes, pas en temps réel.</span><span class="sxs-lookup"><span data-stu-id="fd94d-626">Statistics on document count and storage size are collected every few minutes, not in real time.</span></span> <span data-ttu-id="fd94d-627">Par conséquent, les statistiques retournées par cette API peuvent ne pas refléter les modifications provoquées par les opérations d’indexation récentes.</span><span class="sxs-lookup"><span data-stu-id="fd94d-627">Therefore, the statistics returned by this API may not reflect changes caused by recent indexing operations.</span></span>
> 
> 

<span data-ttu-id="fd94d-628">**Requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-628">**Request**</span></span>

<span data-ttu-id="fd94d-629">Le protocole HTTPS est requis pour toutes les requêtes de services.</span><span class="sxs-lookup"><span data-stu-id="fd94d-629">HTTPS is required for all services requests.</span></span> <span data-ttu-id="fd94d-630">La requête **Get Index Statistics** peut être construite à l'aide de la méthode GET.</span><span class="sxs-lookup"><span data-stu-id="fd94d-630">The **Get Index Statistics** request can be constructed using the GET method.</span></span>

<span data-ttu-id="fd94d-631">Le [nom d’index] de l’URI de la requête indique au service de retourner les statistiques d’index pour l’index spécifié.</span><span class="sxs-lookup"><span data-stu-id="fd94d-631">The [index name] in the request URI tells the service to return index statistics for the specified index.</span></span>

<span data-ttu-id="fd94d-632">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="fd94d-632">`api-version=[string]` (required).</span></span> <span data-ttu-id="fd94d-633">La version préliminaire est `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-633">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="fd94d-634">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-634">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="fd94d-635">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-635">**Request Headers**</span></span>

<span data-ttu-id="fd94d-636">La liste suivante décrit les en-têtes de requête obligatoires et facultatifs.</span><span class="sxs-lookup"><span data-stu-id="fd94d-636">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="fd94d-637">`api-key` : l'en-tête `api-key` est utilisé pour authentifier la requête auprès de votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-637">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="fd94d-638">Il s'agit d'une valeur de type chaîne de caractères, unique pour votre service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-638">It is a string value, unique to your service.</span></span> <span data-ttu-id="fd94d-639">La requête **Get Index Statistics** doit inclure un en-tête `api-key` défini avec la valeur d’une clé d’administration (par opposition à une clé de requête).</span><span class="sxs-lookup"><span data-stu-id="fd94d-639">The **Get Index Statistics** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="fd94d-640">Vous avez également besoin du nom du service pour construire l'URL de la requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-640">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="fd94d-641">Vous pouvez obtenir le nom du service et l'en-tête `api-key` à partir de votre tableau de bord de service dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fd94d-641">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="fd94d-642">Pour obtenir de l'aide sur la navigation dans les pages, consultez [Création d'un service Azure Search dans le portail](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-642">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="fd94d-643">**Corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-643">**Request Body**</span></span>

<span data-ttu-id="fd94d-644">Aucune.</span><span class="sxs-lookup"><span data-stu-id="fd94d-644">None.</span></span>

<span data-ttu-id="fd94d-645">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="fd94d-645">**Response**</span></span>

<span data-ttu-id="fd94d-646">Code d'état : 200 OK est retourné pour une réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="fd94d-646">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="fd94d-647">Le corps de la réponse a le format suivant :</span><span class="sxs-lookup"><span data-stu-id="fd94d-647">The response body is in the following format:</span></span>

    {
      "documentCount": number,
      "storageSize": number (size of the index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a><span data-ttu-id="fd94d-648">Tester l’analyseur</span><span class="sxs-lookup"><span data-stu-id="fd94d-648">Test Analyzer</span></span>
<span data-ttu-id="fd94d-649">L’ **API Analyser** montre comment l’analyseur découpe le texte en jetons.</span><span class="sxs-lookup"><span data-stu-id="fd94d-649">The **Analyze API** shows how an analyzer breaks text into tokens.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="fd94d-650">**Requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-650">**Request**</span></span>

<span data-ttu-id="fd94d-651">Le protocole HTTPS est requis pour toutes les requêtes de services.</span><span class="sxs-lookup"><span data-stu-id="fd94d-651">HTTPS is required for all services requests.</span></span> <span data-ttu-id="fd94d-652">La requête **API Analyser** peut être construite à l’aide de la méthode POST.</span><span class="sxs-lookup"><span data-stu-id="fd94d-652">The **Analyze API** request can be constructed using the POST method.</span></span>

<span data-ttu-id="fd94d-653">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="fd94d-653">`api-version=[string]` (required).</span></span> <span data-ttu-id="fd94d-654">La version préliminaire est `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-654">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="fd94d-655">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-655">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="fd94d-656">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-656">**Request Headers**</span></span>

<span data-ttu-id="fd94d-657">La liste suivante décrit les en-têtes de requête obligatoires et facultatifs.</span><span class="sxs-lookup"><span data-stu-id="fd94d-657">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="fd94d-658">`api-key` : l'en-tête `api-key` est utilisé pour authentifier la requête auprès de votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-658">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="fd94d-659">Il s'agit d'une valeur de type chaîne de caractères, unique pour votre service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-659">It is a string value, unique to your service.</span></span> <span data-ttu-id="fd94d-660">La requête **Analyze API** doit inclure un en-tête `api-key` défini avec la valeur d’une clé d’administration (par opposition à une clé de requête).</span><span class="sxs-lookup"><span data-stu-id="fd94d-660">The **Analyze API** request must include an `api-key` set to an admin key (as opposed to a query key).</span></span>

<span data-ttu-id="fd94d-661">Vous avez également besoin du nom de l’index et du service pour construire l’URL de requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-661">You will also need the index name and the service name to construct the request URL.</span></span> <span data-ttu-id="fd94d-662">Vous pouvez obtenir le nom du service et l'en-tête `api-key` à partir de votre tableau de bord de service dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fd94d-662">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="fd94d-663">Pour obtenir de l'aide sur la navigation dans les pages, consultez [Création d'un service Azure Search dans le portail](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-663">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="fd94d-664">**Corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-664">**Request Body**</span></span>

    {
      "text": "Text to analyze",
      "analyzer": "analyzer_name"
    }

<span data-ttu-id="fd94d-665">ou</span><span class="sxs-lookup"><span data-stu-id="fd94d-665">or</span></span>

    {
      "text": "Text to analyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

<span data-ttu-id="fd94d-666">`analyzer_name`, `tokenizer_name`, `token_filter_name` et `char_filter_name` doivent être des noms valides d’analyseurs, de générateurs de jetons, de filtres de jetons et de filtres de caractères prédéfinis ou personnalisés pour l’index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-666">The `analyzer_name`, `tokenizer_name`, `token_filter_name` and `char_filter_name` need to be valid names of predefined or custom analyzers, tokenizers, token filters and char filters for the index.</span></span> <span data-ttu-id="fd94d-667">Pour en savoir plus sur le processus d’analyse lexicale, consultez [Analyse dans Azure Search](https://aka.ms/azsanalysis).</span><span class="sxs-lookup"><span data-stu-id="fd94d-667">To learn more about the process of lexical analysis see [Analysis in Azure Search](https://aka.ms/azsanalysis).</span></span>

<span data-ttu-id="fd94d-668">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="fd94d-668">**Response**</span></span>

<span data-ttu-id="fd94d-669">Code d'état : 200 OK est retourné pour une réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="fd94d-669">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="fd94d-670">Le corps de la réponse a le format suivant :</span><span class="sxs-lookup"><span data-stu-id="fd94d-670">The response body is in the following format:</span></span>

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of the first character of the token),
          "endOffset": number (index of the last character of the token),
          "position": number (position of the token in the input text)
        },
        ...
      ]
    }

<span data-ttu-id="fd94d-671">**Exemple d’API Analyser**</span><span class="sxs-lookup"><span data-stu-id="fd94d-671">**Analyze API example**</span></span>

<span data-ttu-id="fd94d-672">**Requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-672">**Request**</span></span>

    {
      "text": "Text to analyze",
      "analyzer": "standard"
    }

<span data-ttu-id="fd94d-673">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="fd94d-673">**Response**</span></span>

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a><span data-ttu-id="fd94d-674">Opérations de document</span><span class="sxs-lookup"><span data-stu-id="fd94d-674">Document Operations</span></span>
<span data-ttu-id="fd94d-675">Dans Azure Search, un index est stocké dans le cloud et rempli à l'aide de documents JSON que vous téléchargez sur le service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-675">In Azure Search, an index is stored in the cloud and populated using JSON documents that you upload to the service.</span></span> <span data-ttu-id="fd94d-676">Tous les documents que vous téléchargez comprennent le corpus de vos données de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-676">All the documents that you upload comprise the corpus of your search data.</span></span> <span data-ttu-id="fd94d-677">Les documents contiennent des champs, dont certains sont tokenisés dans les termes de recherche à mesure qu'ils sont téléchargés.</span><span class="sxs-lookup"><span data-stu-id="fd94d-677">Documents contain fields, some of which are tokenized into search terms as they are uploaded.</span></span> <span data-ttu-id="fd94d-678">Le segment d'URL `/docs` dans l'API d'Azure Search représente la collection de documents d'un index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-678">The `/docs` URL segment in the Azure Search API represents the collection of documents in an index.</span></span> <span data-ttu-id="fd94d-679">Toutes les opérations sur la collection, telles que le chargement, la fusion, la suppression ou l'interrogation de documents, sont effectuées dans un contexte d'index unique, les URL pour ces opérations commencent donc toujours par `/indexes/[index name]/docs` pour un nom d'index donné.</span><span class="sxs-lookup"><span data-stu-id="fd94d-679">All operations performed on the collection such as uploading, merging, deleting, or querying documents take place in the context of a single index, so the URLs for these operations will always start with `/indexes/[index name]/docs` for a given index name.</span></span>

<span data-ttu-id="fd94d-680">Votre code d’application doit générer des documents JSON à télécharger vers Azure Search ou vous pouvez utiliser un [indexeur](https://msdn.microsoft.com/library/dn946891.aspx) pour charger des documents si la source de données est la base de données SQL Azure ou Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fd94d-680">Your application code must either generate JSON documents to upload to Azure Search or you can use an [indexer](https://msdn.microsoft.com/library/dn946891.aspx) to load documents if the data source is either Azure SQL Database or Azure Cosmos DB.</span></span> <span data-ttu-id="fd94d-681">En règle générale, les index sont remplis à partir d'un jeu de données unique que vous fournissez.</span><span class="sxs-lookup"><span data-stu-id="fd94d-681">Typically, indexes are populated from a single dataset that you provide.</span></span>

<span data-ttu-id="fd94d-682">Vous devez prévoir un document pour chaque élément dans lequel vous voulez effectuer la recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-682">You should plan on having one document for each item that you want to search.</span></span> <span data-ttu-id="fd94d-683">Une application de location de films peut avoir un document par film, une application vitrine peut avoir un document par référence, une application de formation en ligne peut avoir un document par cours, un cabinet de recherche peut avoir un document pour chaque document académique de son référentiel, etc.</span><span class="sxs-lookup"><span data-stu-id="fd94d-683">A movie rental application might have one document per movie, a storefront application might have one document per SKU, an online courseware application might have one document per course, a research firm might have one document for each academic paper in their repository, and so on.</span></span>

<span data-ttu-id="fd94d-684">Les documents sont constitués d'un ou de plusieurs champs.</span><span class="sxs-lookup"><span data-stu-id="fd94d-684">Documents consist of one or more fields.</span></span> <span data-ttu-id="fd94d-685">Les champs peuvent contenir du texte tokenisé par Azure Search dans des termes de recherche, ainsi que des valeurs non tokenisées ou non textuelles pouvant être utilisées dans des filtres ou des profils de calcul de score.</span><span class="sxs-lookup"><span data-stu-id="fd94d-685">Fields can contain text that is tokenized by Azure Search into search terms, as well as non-tokenized or non-text values that can be used in filters or scoring profiles.</span></span> <span data-ttu-id="fd94d-686">Les noms, les types de données et les fonctionnalités de recherche prises en charge pour chaque champ sont déterminés par le schéma d'index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-686">The names, data types, and search features supported for each field are determined by the index schema.</span></span> <span data-ttu-id="fd94d-687">Un des champs de chaque schéma d'index doit être désigné en tant qu'ID, et chaque document doit avoir une valeur pour le champ d'ID qui identifie de façon unique ce document dans l'index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-687">One of the fields in each index schema must be designated as an ID, and each document must have a value for the ID field that uniquely identifies that document in the index.</span></span> <span data-ttu-id="fd94d-688">Tous les autres champs de document sont facultatifs et ont la valeur null par défaut en l'absence de spécification.</span><span class="sxs-lookup"><span data-stu-id="fd94d-688">All other document fields are optional and will default to a null value if left unspecified.</span></span> <span data-ttu-id="fd94d-689">Notez que les valeurs null n'occupent pas d'espace dans l'index de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-689">Note that null values do not take up space in the search index.</span></span>

<span data-ttu-id="fd94d-690">Avant de pouvoir télécharger des documents, vous devez avoir déjà créé l'index sur le service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-690">Before you can upload documents, you must have already created the index on the service.</span></span> <span data-ttu-id="fd94d-691">Consultez la section [Création d'index](#CreateIndex) pour plus d'informations sur cette première étape.</span><span class="sxs-lookup"><span data-stu-id="fd94d-691">See [Create Index](#CreateIndex) for details about this first step.</span></span>

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a><span data-ttu-id="fd94d-692">Ajout, mise à jour ou suppression de documents</span><span class="sxs-lookup"><span data-stu-id="fd94d-692">Add, Update, or Delete Documents</span></span>
<span data-ttu-id="fd94d-693">Vous pouvez télécharger, fusionner, fusionner-ou-télécharger ou supprimer des documents à partir d'un index spécifié à l'aide de la requête HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="fd94d-693">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span> <span data-ttu-id="fd94d-694">Pour un grand nombre de mises à jour, le traitement par lot des documents (jusqu'à 1 000 documents par lot ou 16 Mo par lot) est recommandé.</span><span class="sxs-lookup"><span data-stu-id="fd94d-694">For large numbers of updates, batching of documents (up to 1000 documents per batch or about 16 MB per batch) is recommended.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="fd94d-695">**Requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-695">**Request**</span></span>

<span data-ttu-id="fd94d-696">Le protocole HTTPS est requis pour toutes les requêtes de service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-696">HTTPS is required for all service requests.</span></span> <span data-ttu-id="fd94d-697">Vous pouvez télécharger, fusionner, fusionner-ou-télécharger ou supprimer des documents à partir d'un index spécifié à l'aide de la requête HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="fd94d-697">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span>

<span data-ttu-id="fd94d-698">L’URI de la requête inclut le [nom d’index], qui spécifie l’index pour la publication des documents.</span><span class="sxs-lookup"><span data-stu-id="fd94d-698">The request URI includes [index name], specifying which index to post documents.</span></span> <span data-ttu-id="fd94d-699">Vous pouvez publier des documents uniquement dans un index à la fois.</span><span class="sxs-lookup"><span data-stu-id="fd94d-699">You can only post documents to one index at a time.</span></span>

<span data-ttu-id="fd94d-700">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="fd94d-700">`api-version=[string]` (required).</span></span> <span data-ttu-id="fd94d-701">La version préliminaire est `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-701">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="fd94d-702">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-702">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="fd94d-703">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-703">**Request Headers**</span></span>

<span data-ttu-id="fd94d-704">La liste suivante décrit les en-têtes de requête obligatoires et facultatifs.</span><span class="sxs-lookup"><span data-stu-id="fd94d-704">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="fd94d-705">`Content-Type`: requis.</span><span class="sxs-lookup"><span data-stu-id="fd94d-705">`Content-Type`: Required.</span></span> <span data-ttu-id="fd94d-706">À définir avec la valeur `application/json`</span><span class="sxs-lookup"><span data-stu-id="fd94d-706">Set this to `application/json`</span></span>
* <span data-ttu-id="fd94d-707">`api-key`: requis.</span><span class="sxs-lookup"><span data-stu-id="fd94d-707">`api-key`: Required.</span></span> <span data-ttu-id="fd94d-708">L'en-tête `api-key` est utilisé pour authentifier la requête auprès de votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-708">The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="fd94d-709">Il s'agit d'une valeur de type chaîne de caractères, unique pour votre service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-709">It is a string value, unique to your service.</span></span> <span data-ttu-id="fd94d-710">La requête **Add Documents** doit inclure un en-tête `api-key` défini avec la valeur de votre clé d’administration (par opposition à une clé de requête).</span><span class="sxs-lookup"><span data-stu-id="fd94d-710">The **Add Documents** request must include an `api-key` header set to your admin key (as opposed to a query key).</span></span>

<span data-ttu-id="fd94d-711">Vous avez également besoin du nom du service pour construire l'URL de la requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-711">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="fd94d-712">Vous pouvez obtenir le nom du service et l'en-tête `api-key` à partir de votre tableau de bord de service dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fd94d-712">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="fd94d-713">Pour obtenir de l'aide sur la navigation dans les pages, consultez [Création d'un service Azure Search dans le portail](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-713">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="fd94d-714">**Corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-714">**Request Body**</span></span>

<span data-ttu-id="fd94d-715">Le corps de la requête contient un ou plusieurs documents à indexer.</span><span class="sxs-lookup"><span data-stu-id="fd94d-715">The body of the request contains one or more documents to be indexed.</span></span> <span data-ttu-id="fd94d-716">Les documents sont identifiés par une clé unique.</span><span class="sxs-lookup"><span data-stu-id="fd94d-716">Documents are identified by a unique key.</span></span> <span data-ttu-id="fd94d-717">Chaque document est associé à une action : upload, merge, mergeOrUpload ou delete.</span><span class="sxs-lookup"><span data-stu-id="fd94d-717">Each document is associated with an action: upload, merge, mergeOrUpload or delete.</span></span> <span data-ttu-id="fd94d-718">Les demandes de téléchargement doivent inclure les données du document sous forme de paires clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="fd94d-718">Upload requests must include the document data as a set of key/value pairs.</span></span>

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> <span data-ttu-id="fd94d-719">Les clés de document ne peuvent contenir que des lettres, des chiffres, des tirets (« - »), des traits de soulignement (« _ ») et les signes égal (« = »).</span><span class="sxs-lookup"><span data-stu-id="fd94d-719">Document keys can only contain letters, numbers, dashes ("-"), underscores ("_"), and equal signs ("=").</span></span> <span data-ttu-id="fd94d-720">Pour plus d’informations, consultez les [Règles d’affectation des noms](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd94d-720">For more details, see [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span></span>
> 
> 

<span data-ttu-id="fd94d-721">**Actions de document**</span><span class="sxs-lookup"><span data-stu-id="fd94d-721">**Document Actions**</span></span>

* <span data-ttu-id="fd94d-722">`upload`: une action de téléchargement est similaire à un « upsert », où le document est inséré s'il est nouveau et mis à jour/remplacé s'il existe déjà.</span><span class="sxs-lookup"><span data-stu-id="fd94d-722">`upload`: An upload action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> <span data-ttu-id="fd94d-723">Notez que tous les champs sont remplacés dans le cas d'une mise à jour.</span><span class="sxs-lookup"><span data-stu-id="fd94d-723">Note that all fields are replaced in the update case.</span></span>
* <span data-ttu-id="fd94d-724">`merge`: la fusion met à jour un document existant avec les champs spécifiés.</span><span class="sxs-lookup"><span data-stu-id="fd94d-724">`merge`: Merge updates an existing document with the specified fields.</span></span> <span data-ttu-id="fd94d-725">Si le document n'existe pas, la fusion échoue.</span><span class="sxs-lookup"><span data-stu-id="fd94d-725">If the document doesn't exist, the merge will fail.</span></span> <span data-ttu-id="fd94d-726">N'importe quel champ que vous spécifiez dans une fusion remplace le champ existant dans le document.</span><span class="sxs-lookup"><span data-stu-id="fd94d-726">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="fd94d-727">Cela inclut les champs de type `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-727">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="fd94d-728">Par exemple, si le document contient un champ « balises » avec la valeur `["budget"]` et que vous exécutez une fusion avec la valeur `["economy", "pool"]` pour « balises », la valeur finale du champ « balises » est `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-728">For example, if the document contains a field "tags" with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for "tags", the final value of the "tags" field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="fd94d-729">Elle ne doit **pas** être `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-729">It will **not** be `["budget", "economy", "pool"]`.</span></span>
* <span data-ttu-id="fd94d-730">`mergeOrUpload` : se comporte comme `merge` si un document avec la clé spécifiée existe déjà dans l'index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-730">`mergeOrUpload`: behaves like `merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="fd94d-731">Si le document n'existe pas, l'opération se comporte comme `upload` avec un nouveau document.</span><span class="sxs-lookup"><span data-stu-id="fd94d-731">If the document does not exist it behaves like `upload` with a new document.</span></span>
* <span data-ttu-id="fd94d-732">`delete`: cette action supprime de l'index le document spécifié.</span><span class="sxs-lookup"><span data-stu-id="fd94d-732">`delete`: Delete removes the specified document from the index.</span></span> <span data-ttu-id="fd94d-733">Notez que tous les champs que vous spécifiez dans une opération `delete` autre que le champ de clé sont ignorés.</span><span class="sxs-lookup"><span data-stu-id="fd94d-733">Note that any fields you specify in a `delete` operation other than the key field will be ignored.</span></span> <span data-ttu-id="fd94d-734">Si vous souhaitez supprimer un champ individuel dans un document, utilisez plutôt `merge` et définissez simplement le champ de manière explicite avec la valeur `null`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-734">If you want to remove an individual field from a document, use `merge` instead and simply set the field explicitly to `null`.</span></span>

<span data-ttu-id="fd94d-735">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="fd94d-735">**Response**</span></span>

<span data-ttu-id="fd94d-736">Code d’état : 200 (OK) est retourné pour une réponse correcte, ce qui signifie que tous les éléments ont été indexés.</span><span class="sxs-lookup"><span data-stu-id="fd94d-736">Status code 200 (OK) is returned for a successful response, meaning that all items have been successfully indexed.</span></span> <span data-ttu-id="fd94d-737">La propriété `status` est alors définie sur true pour tous les éléments, et la propriété `statusCode` est définie soit sur 201 (pour les documents nouvellement chargés) soit sur 200 (pour les documents fusionnés ou supprimés) :</span><span class="sxs-lookup"><span data-stu-id="fd94d-737">This is indicated by the `status` property being set to true for all items, as well as the `statusCode` property being set to either 201 (for newly uploaded documents) or 200 (for merged or deleted documents):</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

<span data-ttu-id="fd94d-738">Un code d’état 207 (Multi-état) est renvoyé lorsqu’au moins un élément n’a pas été correctement indexé.</span><span class="sxs-lookup"><span data-stu-id="fd94d-738">Status code 207 (Multi-Status) is returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="fd94d-739">Le champ `status` des éléments qui n’ont pas été indexés prend alors la valeur false.</span><span class="sxs-lookup"><span data-stu-id="fd94d-739">Items that have not been indexed have the `status` field set to false.</span></span> <span data-ttu-id="fd94d-740">Les propriétés `errorMessage` et `statusCode` indiquent la raison de l’erreur d’indexation :</span><span class="sxs-lookup"><span data-stu-id="fd94d-740">The `errorMessage` and `statusCode` properties will indicate the reason for the indexing error:</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "The search service is too busy to process this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with the 'allowIndexDowntime' flag set to 'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

<span data-ttu-id="fd94d-741">Le tableau suivant décrit, par document, les différents codes d’état pouvant être retournés dans la réponse.</span><span class="sxs-lookup"><span data-stu-id="fd94d-741">The following table explains the various per-document status codes that can be returned in the response.</span></span> <span data-ttu-id="fd94d-742">Notez que certains codes indiquent des problèmes au niveau de la requête proprement dite, tandis que d’autres indiquent des conditions d’erreur temporaires.</span><span class="sxs-lookup"><span data-stu-id="fd94d-742">Note that some indicate problems with the request itself, while others indicate temporary error conditions.</span></span> <span data-ttu-id="fd94d-743">Dans ce dernier cas, il est recommandé de réessayer l’opération après un certain délai.</span><span class="sxs-lookup"><span data-stu-id="fd94d-743">The latter you should retry after a delay.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="fd94d-744">Code d’état</span><span class="sxs-lookup"><span data-stu-id="fd94d-744">Status code</span></span></th>
        <th><span data-ttu-id="fd94d-745">Signification</span><span class="sxs-lookup"><span data-stu-id="fd94d-745">Meaning</span></span></th>
        <th><span data-ttu-id="fd94d-746">Nouvelle tentative possible</span><span class="sxs-lookup"><span data-stu-id="fd94d-746">Retryable</span></span></th>
        <th><span data-ttu-id="fd94d-747">Remarques</span><span class="sxs-lookup"><span data-stu-id="fd94d-747">Notes</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-748">200</span><span class="sxs-lookup"><span data-stu-id="fd94d-748">200</span></span></td>
        <td><span data-ttu-id="fd94d-749">Le document a été correctement modifié ou supprimé.</span><span class="sxs-lookup"><span data-stu-id="fd94d-749">Document was successfully modified or deleted.</span></span></td>
        <td><span data-ttu-id="fd94d-750">n/a</span><span class="sxs-lookup"><span data-stu-id="fd94d-750">n/a</span></span></td>
        <td><span data-ttu-id="fd94d-751">Les opérations de suppression sont <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentes</a>.</span><span class="sxs-lookup"><span data-stu-id="fd94d-751">Delete operations are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span> <span data-ttu-id="fd94d-752">Autrement dit, même si une clé de document n’existe pas dans l’index, une tentative d’opération de suppression avec cette clé générera le code d’état 200.</span><span class="sxs-lookup"><span data-stu-id="fd94d-752">That is, even if a document key does not exist in the index, attempting a delete operation with that key will result in a 200 status code.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-753">201</span><span class="sxs-lookup"><span data-stu-id="fd94d-753">201</span></span></td>
        <td><span data-ttu-id="fd94d-754">Le document a été créé avec succès.</span><span class="sxs-lookup"><span data-stu-id="fd94d-754">Document was successfully created.</span></span></td>
        <td><span data-ttu-id="fd94d-755">n/a</span><span class="sxs-lookup"><span data-stu-id="fd94d-755">n/a</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-756">400</span><span class="sxs-lookup"><span data-stu-id="fd94d-756">400</span></span></td>
        <td><span data-ttu-id="fd94d-757">Le document a rencontré une erreur qui a empêché son indexation.</span><span class="sxs-lookup"><span data-stu-id="fd94d-757">There was an error in the document that prevented it from being indexed.</span></span></td>
        <td><span data-ttu-id="fd94d-758">Non</span><span class="sxs-lookup"><span data-stu-id="fd94d-758">No</span></span></td>
        <td><span data-ttu-id="fd94d-759">Le message d’erreur dans la réponse indique le problème survenu au niveau du document.</span><span class="sxs-lookup"><span data-stu-id="fd94d-759">The error message in the response will indicate what is wrong with the document.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-760">404</span><span class="sxs-lookup"><span data-stu-id="fd94d-760">404</span></span></td>
        <td><span data-ttu-id="fd94d-761">Le document n’a pas pu être fusionné, car la clé spécifiée n’existe pas dans l’index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-761">The document could not be merged because the given key doesn't exist in the index.</span></span></td>
        <td><span data-ttu-id="fd94d-762">Non</span><span class="sxs-lookup"><span data-stu-id="fd94d-762">No</span></span></td>
        <td><span data-ttu-id="fd94d-763">Cette erreur ne s’applique pas aux téléchargements dans la mesure où ils créent de nouveaux documents, de même qu’elle ne se produit pas pour les suppressions, car elles sont <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentes</a>.</span><span class="sxs-lookup"><span data-stu-id="fd94d-763">This error does not occur for uploads since they create new documents, and it does not occur for deletes because they are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-764">409</span><span class="sxs-lookup"><span data-stu-id="fd94d-764">409</span></span></td>
        <td><span data-ttu-id="fd94d-765">Un conflit de version a été détecté lors de la tentative d’indexation d’un document.</span><span class="sxs-lookup"><span data-stu-id="fd94d-765">A version conflict was detected when attempting to index a document.</span></span></td>
        <td><span data-ttu-id="fd94d-766">Oui</span><span class="sxs-lookup"><span data-stu-id="fd94d-766">Yes</span></span></td>
        <td><span data-ttu-id="fd94d-767">Cela peut se produire lorsque vous essayez d’indexer le même document plusieurs fois simultanément.</span><span class="sxs-lookup"><span data-stu-id="fd94d-767">This can happen when you're trying to index the same document more than once concurrently.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-768">422</span><span class="sxs-lookup"><span data-stu-id="fd94d-768">422</span></span></td>
        <td><span data-ttu-id="fd94d-769">L’index est temporairement indisponible car il a été mis à jour avec l’indicateur « allowIndexDowntime » défini sur « true ».</span><span class="sxs-lookup"><span data-stu-id="fd94d-769">The index is temporarily unavailable because it was updated with the 'allowIndexDowntime' flag set to 'true'.</span></span></td>
        <td><span data-ttu-id="fd94d-770">Oui</span><span class="sxs-lookup"><span data-stu-id="fd94d-770">Yes</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="fd94d-771">503</span><span class="sxs-lookup"><span data-stu-id="fd94d-771">503</span></span></td>
        <td><span data-ttu-id="fd94d-772">Votre service de recherche est temporairement indisponible, probablement en raison d’une charge importante.</span><span class="sxs-lookup"><span data-stu-id="fd94d-772">Your search service is temporarily unavailable, possibly due to heavy load.</span></span></td>
        <td><span data-ttu-id="fd94d-773">Oui</span><span class="sxs-lookup"><span data-stu-id="fd94d-773">Yes</span></span></td>
        <td><span data-ttu-id="fd94d-774">Votre code doit attendre avant d’effectuer une nouvelle tentative, au risque de prolonger l’indisponibilité du service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-774">Your code should wait before retrying in this case or you risk prolonging the service unavailability.</span></span></td>
    </tr>
</table> 

<span data-ttu-id="fd94d-775">**Remarque**: si votre code client rencontre fréquemment une réponse 207, le système est peut-être en cours de chargement.</span><span class="sxs-lookup"><span data-stu-id="fd94d-775">**Note**: If your client code frequently encounters a 207 response, one possible reason is that the system is under load.</span></span> <span data-ttu-id="fd94d-776">Vous pouvez vous en assurer en vérifiant la propriété `statusCode` pour 503.</span><span class="sxs-lookup"><span data-stu-id="fd94d-776">You can confirm this by checking the `statusCode` property for 503.</span></span> <span data-ttu-id="fd94d-777">Si tel est le cas, nous vous recommandons de ***limiter les requêtes d’indexation***.</span><span class="sxs-lookup"><span data-stu-id="fd94d-777">If this is the case, we recommend ***throttling indexing requests***.</span></span> <span data-ttu-id="fd94d-778">Sinon, si le trafic d'indexation ne diminue pas, le système peut commencer à rejeter toutes les requêtes avec des erreurs 503.</span><span class="sxs-lookup"><span data-stu-id="fd94d-778">Otherwise, if indexing traffic doesn't subside, the system could start rejecting all requests with 503 errors.</span></span>

<span data-ttu-id="fd94d-779">Le code d’état 429 indique que vous avez dépassé votre quota du nombre de documents par index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-779">Status code 429 indicates that you have exceeded your quota on the number of documents per index.</span></span> <span data-ttu-id="fd94d-780">Vous devez créer un autre index ou effectuer une mise à niveau pour bénéficier de limites de capacité supérieures.</span><span class="sxs-lookup"><span data-stu-id="fd94d-780">You must either create a new index or upgrade for higher capacity limits.</span></span>

<span data-ttu-id="fd94d-781">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="fd94d-781">**Example:**</span></span>

    {
      "value": [
        {
          "@search.action": "upload",
          "hotelId": "1",
          "baseRate": 199.0,
          "description": "Best hotel in town",
          "description_fr": "Meilleur hôtel en ville",
          "hotelName": "Fancy Stay",
          "category": "Luxury",
          "tags": ["pool", "view", "wifi", "concierge"],
          "parkingIncluded": false,
          "smokingAllowed": false,
          "lastRenovationDate": "2010-06-27T00:00:00Z",
          "rating": 5,
          "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
          "@search.action": "upload",
          "hotelId": "2",
          "baseRate": 79.99,
          "description": "Cheapest hotel in town",
          "description_fr": "Hôtel le moins cher en ville",
          "hotelName": "Roach Motel",
          "category": "Budget",
          "tags": ["motel", "budget"],
          "parkingIncluded": true,
          "smokingAllowed": true,
          "lastRenovationDate": "1982-04-28T00:00:00Z",
          "rating": 1,
          "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a><span data-ttu-id="fd94d-782">Search Documents</span><span class="sxs-lookup"><span data-stu-id="fd94d-782">Search Documents</span></span>
<span data-ttu-id="fd94d-783">Une opération **Search** est émise en tant que requête GET ou POST et spécifie les paramètres qui donnent les critères de sélection des documents correspondants.</span><span class="sxs-lookup"><span data-stu-id="fd94d-783">A **Search** operation is issued as a GET or POST request and specifies parameters that give the criteria for selecting matching documents.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="fd94d-784">**Utilisation de POST au lieu de GET**</span><span class="sxs-lookup"><span data-stu-id="fd94d-784">**When to use POST instead of GET**</span></span>

<span data-ttu-id="fd94d-785">Lorsque vous utilisez HTTP GET pour appeler l’API de **recherche** , vous devez savoir que la longueur de l’URL de requête ne peut pas dépasser 8 Ko.</span><span class="sxs-lookup"><span data-stu-id="fd94d-785">When you use HTTP GET to call the **Search** API, you need to be aware that the length of the request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="fd94d-786">Cela est généralement suffisamment pour la plupart des applications.</span><span class="sxs-lookup"><span data-stu-id="fd94d-786">This is usually enough for most applications.</span></span> <span data-ttu-id="fd94d-787">Toutefois, certaines applications produisent des requêtes très volumineuses ou des expressions de filtre OData.</span><span class="sxs-lookup"><span data-stu-id="fd94d-787">However, some applications produce very large queries or OData filter expressions.</span></span> <span data-ttu-id="fd94d-788">Pour ces applications, il est recommandé d'utiliser HTTP POST, car cela permet d'obtenir des filtres et des requêtes plus volumineux que GET.</span><span class="sxs-lookup"><span data-stu-id="fd94d-788">For these applications, using HTTP POST is a better choice because it allows larger filters and queries than GET.</span></span> <span data-ttu-id="fd94d-789">Avec POST, le nombre de termes ou de clauses dans une requête est le facteur limitant, pas la taille de la requête brute, car la limite de la taille de la requête POST est proche de 16 Mo.</span><span class="sxs-lookup"><span data-stu-id="fd94d-789">With POST, the number of terms or clauses in a query is the limiting factor, not the size of the raw query since the request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="fd94d-790">Bien que la limite de la taille de la requête POST est très importante, les requêtes de recherche et les expressions de filtre ne peuvent pas être arbitrairement complexes.</span><span class="sxs-lookup"><span data-stu-id="fd94d-790">Even though the POST request size limit is very large, search queries and filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="fd94d-791">Consultez [Syntaxe de requête Lucene](https://msdn.microsoft.com/library/mt589323.aspx) et [Syntaxe d’expression OData](https://msdn.microsoft.com/library/dn798921.aspx) pour plus d’informations sur les limites de la complexité des filtres et des requêtes de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-791">See [Lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx) and [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about search query and filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="fd94d-792">**Requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-792">**Request**</span></span>

<span data-ttu-id="fd94d-793">Le protocole HTTPS est requis pour les requêtes de service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-793">HTTPS is required for service requests.</span></span> <span data-ttu-id="fd94d-794">La requête **Search** peut être construite à l’aide des méthodes GET ou POST.</span><span class="sxs-lookup"><span data-stu-id="fd94d-794">The **Search** request can be constructed using the GET or POST methods.</span></span>

<span data-ttu-id="fd94d-795">L'URI de la requête spécifie l'index à interroger, pour tous les documents qui correspondent aux paramètres.</span><span class="sxs-lookup"><span data-stu-id="fd94d-795">The request URI specifies which index to query, for all documents that match the parameters.</span></span> <span data-ttu-id="fd94d-796">Les paramètres sont spécifiés dans la chaîne de requête pour les requêtes GET et dans le corps de la requête pour les requêtes POST.</span><span class="sxs-lookup"><span data-stu-id="fd94d-796">Parameters are specified on the query string in the case of GET requests, and in the request body in the case of POST requests.</span></span>

<span data-ttu-id="fd94d-797">Pendant la création de requêtes GET, il est recommandé d’ [encoder par URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) les paramètres de requête spécifiques pour appeler l’API REST directement.</span><span class="sxs-lookup"><span data-stu-id="fd94d-797">As a best practice when creating GET requests, remember to [URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling the REST API directly.</span></span> <span data-ttu-id="fd94d-798">Pour les opérations de **recherche** , cela inclut :</span><span class="sxs-lookup"><span data-stu-id="fd94d-798">For **Search** operations, this includes:</span></span>

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

<span data-ttu-id="fd94d-799">L'encodage des URL est recommandé uniquement pour les paramètres de requête ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="fd94d-799">URL encoding is only recommended on the above query parameters.</span></span> <span data-ttu-id="fd94d-800">Si vous encodez par URL par inadvertance la chaîne de requête entière (tout ce qui figure après ?), les requêtes sont interrompues.</span><span class="sxs-lookup"><span data-stu-id="fd94d-800">If you inadvertently URL-encode the entire query string (everything after the ?), requests will break.</span></span>

<span data-ttu-id="fd94d-801">En outre, l'encodage des URL est nécessaire uniquement lors de l'appel direct de l'API REST à l'aide de GET.</span><span class="sxs-lookup"><span data-stu-id="fd94d-801">Also, URL encoding is only necessary when calling the REST API directly using GET.</span></span> <span data-ttu-id="fd94d-802">Aucun encodage des URL n’est nécessaire pendant l’appel de **Search** à l’aide de POST ou quand vous utilisez la [bibliothèque cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx)qui gère l’encodage des URL pour vous.</span><span class="sxs-lookup"><span data-stu-id="fd94d-802">No URL encoding is necessary when calling **Search** using POST, or when using the [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="fd94d-803"><a name="SearchQueryParameters"></a>
**Paramètres de requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-803"><a name="SearchQueryParameters"></a>
**Query Parameters**</span></span>

<span data-ttu-id="fd94d-804">**Search** accepte plusieurs paramètres qui fournissent les critères de la requête et qui spécifient également le comportement de la recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-804">**Search** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="fd94d-805">Vous fournissez ces paramètres dans la chaîne de requête de l’URL pendant l’appel de **Search** via GET et en tant que propriétés JSON dans le corps de la requête pendant l’appel de **Search** via POST.</span><span class="sxs-lookup"><span data-stu-id="fd94d-805">You provide these parameters in the URL query string when calling **Search** via GET, and as JSON properties in the request body when calling **Search** via POST.</span></span> <span data-ttu-id="fd94d-806">La syntaxe de certains paramètres est légèrement différente entre GET et POST.</span><span class="sxs-lookup"><span data-stu-id="fd94d-806">The syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="fd94d-807">Ces différences sont indiquées ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="fd94d-807">These differences are noted as applicable below:</span></span>

<span data-ttu-id="fd94d-808">`search=[string]` (facultatif) - le texte à rechercher.</span><span class="sxs-lookup"><span data-stu-id="fd94d-808">`search=[string]` (optional) - The text to search for.</span></span> <span data-ttu-id="fd94d-809">Tous les champs `searchable` sont interrogés par défaut, sauf si `searchFields` est spécifié.</span><span class="sxs-lookup"><span data-stu-id="fd94d-809">All `searchable` fields are searched by default unless `searchFields` is specified.</span></span> <span data-ttu-id="fd94d-810">Lors de l'interrogation des champs `searchable`, le texte de recherche est tokenisé, plusieurs termes peuvent donc être séparés par un espace blanc (par exemple : `search=hello world`).</span><span class="sxs-lookup"><span data-stu-id="fd94d-810">When searching `searchable` fields, the search text itself is tokenized, so multiple terms can be separated by white space (for example: `search=hello world`).</span></span> <span data-ttu-id="fd94d-811">Pour faire correspondre n'importe quel terme, utilisez `*` (ce qui peut être utile pour les requêtes de filtre booléen).</span><span class="sxs-lookup"><span data-stu-id="fd94d-811">To match any term, use `*` (this can be useful for boolean filter queries).</span></span> <span data-ttu-id="fd94d-812">L'omission de ce paramètre a le même effet que s'il est défini avec la valeur `*`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-812">Omitting this parameter has the same effect as setting it to `*`.</span></span> <span data-ttu-id="fd94d-813">Pour obtenir des détails sur la syntaxe de recherche, consultez la section [Syntaxe de requête simple](https://msdn.microsoft.com/library/dn798920.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-813">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) for specifics on the search syntax.</span></span>

* <span data-ttu-id="fd94d-814">**Remarque** : les résultats peuvent parfois être surprenants lors de l’interrogation de champs `searchable`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-814">**Note**: The results can sometimes be surprising when querying over `searchable` fields.</span></span> <span data-ttu-id="fd94d-815">Le générateur de jetons inclut une logique pour gérer les cas courants dans le texte anglais tels que les apostrophes, les virgules des nombres, etc. Par exemple, `search=123,456` correspond à un seul terme 123,456 plutôt qu'aux termes individuels 123 et 456, étant donné que les virgules sont utilisées comme séparateurs de milliers dans les grands nombres en anglais.</span><span class="sxs-lookup"><span data-stu-id="fd94d-815">The tokenizer includes logic to handle cases common to English text like apostrophes, commas in numbers, etc. For example, `search=123,456` will match a single term 123,456 rather than the individual terms 123 and 456, since commas are used as thousand-separators for large numbers in English.</span></span> <span data-ttu-id="fd94d-816">Pour cette raison, nous vous recommandons d'utiliser un espace blanc au lieu des signes de ponctuation pour séparer les termes du paramètre `search`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-816">For this reason, we recommend using white space rather than punctuation to separate terms in the `search` parameter.</span></span>

<span data-ttu-id="fd94d-817">`searchMode=any|all` (facultatif, la valeur par défaut est `any`) : indique si certains ou l'ensemble des termes de recherche doivent correspondre pour que le document soit considéré comme une correspondance.</span><span class="sxs-lookup"><span data-stu-id="fd94d-817">`searchMode=any|all` (optional, defaults to `any`) - whether any or all of the search terms must be matched in order to count the document as a match.</span></span>

<span data-ttu-id="fd94d-818">`searchFields=[string]` (facultatif) : liste des noms de champs séparés par des virgules dans lesquels rechercher le texte spécifié.</span><span class="sxs-lookup"><span data-stu-id="fd94d-818">`searchFields=[string]` (optional) - The list of comma-separated field names to search for the specified text.</span></span> <span data-ttu-id="fd94d-819">Les champs cibles doivent être marqués comme `searchable`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-819">Target fields must be marked as `searchable`.</span></span>

<span data-ttu-id="fd94d-820">`queryType=simple|full` (facultatif, la valeur par défaut est `simple`) : lorsqu’il est défini sur « simple », le texte recherché est interprété à l’aide d’un langage de requête simple qui autorise des symboles tels que +, * et "".</span><span class="sxs-lookup"><span data-stu-id="fd94d-820">`queryType=simple|full` (optional, defaults to `simple`) - when set to "simple" search text is interpreted using a simple query language that allows for symbols such as +, * and "".</span></span> <span data-ttu-id="fd94d-821">Les requêtes sont évaluées pour tous les champs pouvant faire l’objet d’une recherche (ou les champs indiqués dans `searchFields`) dans chaque document par défaut.</span><span class="sxs-lookup"><span data-stu-id="fd94d-821">Queries are evaluated across all searchable fields (or fields indicated in `searchFields`) in each document by default.</span></span> <span data-ttu-id="fd94d-822">Lorsque le type de requête a la valeur `full` , le texte recherché est interprété à l’aide du langage de requête Lucene qui autorise des recherches spécifiques aux champs et pondérées.</span><span class="sxs-lookup"><span data-stu-id="fd94d-822">When the query type is set to `full` search text is interpreted using the Lucene query language which allows field-specific and weighted searches.</span></span> <span data-ttu-id="fd94d-823">Pour obtenir des détails sur les syntaxes de recherche, consultez les sections [Syntaxe de requête simple](https://msdn.microsoft.com/library/dn798920.aspx) et [Syntaxe de requête Lucene](https://msdn.microsoft.com/library/mt589323.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd94d-823">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) and [Lucene Query Syntax](https://msdn.microsoft.com/library/mt589323.aspx) for specifics on the search syntaxes.</span></span> 

> [!NOTE]
> <span data-ttu-id="fd94d-824">La recherche de plages dans le langage de requête Lucene n’est pas prise en charge au profit de $filter qui offre des fonctionnalités similaires.</span><span class="sxs-lookup"><span data-stu-id="fd94d-824">Range search in the Lucene query language is not supported in favor of $filter which offers similar functionality.</span></span>
> 
> 

<span data-ttu-id="fd94d-825">`moreLikeThis=[key]` (facultatif) **Important :** cette fonctionnalité est uniquement disponible dans `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-825">`moreLikeThis=[key]` (optional) **Important:** This feature is only available in `2015-02-28-Preview`.</span></span> <span data-ttu-id="fd94d-826">Cette option ne peut pas être utilisée dans une requête qui contient le paramètre de recherche de texte, `search=[string]`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-826">This option cannot be used in a query that contains the text search parameter, `search=[string]`.</span></span> <span data-ttu-id="fd94d-827">Le paramètre `moreLikeThis` trouve les documents qui sont similaires au document spécifié par la clé de document.</span><span class="sxs-lookup"><span data-stu-id="fd94d-827">The `moreLikeThis` parameter finds documents that are similar to the document specified by the document key.</span></span> <span data-ttu-id="fd94d-828">Quand une requête de recherche est effectuée avec `moreLikeThis`, une liste de termes de recherche est générée en fonction de la fréquence et de la rareté des termes dans le document source.</span><span class="sxs-lookup"><span data-stu-id="fd94d-828">When a search request is made with `moreLikeThis`, a list of search terms is generated based on the frequency and rarity of terms in the source document.</span></span> <span data-ttu-id="fd94d-829">Ces termes sont ensuite utilisés pour effectuer la requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-829">Those terms are then used to make the request.</span></span> <span data-ttu-id="fd94d-830">Par défaut, le contenu de tous les champs `searchable` est pris en compte sauf si `searchFields` est utilisé pour restreindre les champs faisant l'objet de recherches.</span><span class="sxs-lookup"><span data-stu-id="fd94d-830">By default, the contents of all `searchable` fields are considered unless `searchFields` is used to restrict which fields are searched.</span></span>  

<span data-ttu-id="fd94d-831">`$skip=#` (facultatif) : nombre de résultats de recherche à ignorer. Ne peut pas être supérieur à 100 000.</span><span class="sxs-lookup"><span data-stu-id="fd94d-831">`$skip=#` (optional) - the number of search results to skip; Cannot be greater than 100,000.</span></span> <span data-ttu-id="fd94d-832">Si vous avez besoin d'analyser des documents dans l'ordre, mais que vous ne pouvez pas utiliser `$skip` en raison de cette limitation, utilisez plutôt `$orderby` sur une clé totalement ordonnée et `$filter` avec une requête de plage de données.</span><span class="sxs-lookup"><span data-stu-id="fd94d-832">If you need to scan documents in sequence but cannot use `$skip` due to this limitation, consider using `$orderby` on a totally-ordered key and `$filter` with a range query instead.</span></span>

> [!NOTE]
> <span data-ttu-id="fd94d-833">Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `skip` au lieu de `$skip`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-833">When calling **Search** using POST, this parameter is named `skip` instead of `$skip`.</span></span>
> 
> 

<span data-ttu-id="fd94d-834">`$top=#` (facultatif) : nombre de résultats de recherche à récupérer.</span><span class="sxs-lookup"><span data-stu-id="fd94d-834">`$top=#` (optional) - the number of search results to retrieve.</span></span> <span data-ttu-id="fd94d-835">Ceci peut être utilisé conjointement avec `$skip` pour implémenter la pagination côté client des résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-835">This can be used in conjunction with `$skip` to implement client-side paging of search results.</span></span>

> [!NOTE]
> <span data-ttu-id="fd94d-836">Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `top` au lieu de `$top`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-836">When calling **Search** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="fd94d-837">`$count=true|false` (facultatif, la valeur par défaut est `false`) : indique s'il faut extraire le nombre total de résultats.</span><span class="sxs-lookup"><span data-stu-id="fd94d-837">`$count=true|false` (optional, defaults to `false`) - Specifies whether to fetch the total count of results.</span></span> <span data-ttu-id="fd94d-838">Ceci est le nombre de tous les documents qui correspondent aux paramètres `search` et `$filter` en faisant abstraction de `$top` et `$skip`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-838">This is the count of all documents that match the `search` and `$filter` parameters, ignoring `$top` and `$skip`.</span></span> <span data-ttu-id="fd94d-839">La valeur `true` peut avoir un impact sur les performances.</span><span class="sxs-lookup"><span data-stu-id="fd94d-839">Setting this value to `true` may have a performance impact.</span></span> <span data-ttu-id="fd94d-840">Notez que le nombre retourné est une approximation.</span><span class="sxs-lookup"><span data-stu-id="fd94d-840">Note that the count returned is an approximation.</span></span>

> [!NOTE]
> <span data-ttu-id="fd94d-841">Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `count` au lieu de `$count`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-841">When calling **Search** using POST, this parameter is named `count` instead of `$count`.</span></span>
> 
> 

<span data-ttu-id="fd94d-842">`$orderby=[string]` (facultatif) : liste d'expressions séparées par des virgules selon lesquelles les résultats doivent être triés.</span><span class="sxs-lookup"><span data-stu-id="fd94d-842">`$orderby=[string]` (optional) - A list of comma-separated expressions to sort the results by.</span></span> <span data-ttu-id="fd94d-843">Chaque expression peut être un nom de champ ou un appel à la fonction `geo.distance()` .</span><span class="sxs-lookup"><span data-stu-id="fd94d-843">Each expression can be either a field name or a call to the `geo.distance()` function.</span></span> <span data-ttu-id="fd94d-844">Chaque expression peut être suivie par `asc` pour indiquer l'ordre croissant, et par `desc` pour indiquer l'ordre décroissant.</span><span class="sxs-lookup"><span data-stu-id="fd94d-844">Each expression can be followed by `asc` to indicated ascending, and `desc` to indicate descending.</span></span> <span data-ttu-id="fd94d-845">La valeur par défaut est l'ordre croissant.</span><span class="sxs-lookup"><span data-stu-id="fd94d-845">The default is ascending order.</span></span> <span data-ttu-id="fd94d-846">Les liens seront rompus par les scores de correspondance des documents.</span><span class="sxs-lookup"><span data-stu-id="fd94d-846">Ties will be broken by the match scores of documents.</span></span> <span data-ttu-id="fd94d-847">Si aucun `$orderby` n'est spécifié, l'ordre de tri par défaut est décroissant par score de correspondance de documents.</span><span class="sxs-lookup"><span data-stu-id="fd94d-847">If no `$orderby` is specified, the default sort order is descending by document match score.</span></span> <span data-ttu-id="fd94d-848">Il existe une limite de 32 clauses pour `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-848">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="fd94d-849">Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `orderby` au lieu de `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-849">When calling **Search** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="fd94d-850">`$select=[string]` (facultatif) : liste de champs séparés par des virgules à récupérer.</span><span class="sxs-lookup"><span data-stu-id="fd94d-850">`$select=[string]` (optional) - A list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="fd94d-851">Si aucune valeur n'est spécifiée, tous les champs marqués comme récupérables dans le schéma sont inclus.</span><span class="sxs-lookup"><span data-stu-id="fd94d-851">If unspecified, all fields marked as retrievable in the schema are included.</span></span> <span data-ttu-id="fd94d-852">Vous pouvez aussi demander explicitement tous les champs en définissant ce paramètre avec la valeur `*`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-852">You can also explicitly request all fields by setting this parameter to `*`.</span></span>

> [!NOTE]
> <span data-ttu-id="fd94d-853">Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `select` au lieu de `$select`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-853">When calling **Search** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="fd94d-854">`facet=[string]` (zéro ou plus) : champ à utiliser pour les facettes.</span><span class="sxs-lookup"><span data-stu-id="fd94d-854">`facet=[string]` (zero or more) - A field to facet by.</span></span> <span data-ttu-id="fd94d-855">La chaîne peut éventuellement contenir des paramètres pour personnaliser les facettes exprimées sous forme de paires `name:value` séparées par des virgules.</span><span class="sxs-lookup"><span data-stu-id="fd94d-855">Optionally the string may contain parameters to customize the faceting expressed as comma-separated `name:value` pairs.</span></span> <span data-ttu-id="fd94d-856">Les paramètres valides sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="fd94d-856">Valid parameters are:</span></span>

* <span data-ttu-id="fd94d-857">`count` (nombre maximal de termes de facette ; la valeur par défaut est 10).</span><span class="sxs-lookup"><span data-stu-id="fd94d-857">`count` (max number of facet terms; default is 10).</span></span> <span data-ttu-id="fd94d-858">Il n'y a pas de valeur maximale, mais les valeurs supérieures ont un impact négatif sur les performances, en particulier si le champ à facettes contient un grand nombre de termes uniques.</span><span class="sxs-lookup"><span data-stu-id="fd94d-858">There is no maximum, but higher values incur a corresponding performance penalty, especially if the faceted field contains a large number of unique terms.</span></span>
  * <span data-ttu-id="fd94d-859">Par exemple : `facet=category,count:5` obtient les cinq premières catégories des résultats de facette.</span><span class="sxs-lookup"><span data-stu-id="fd94d-859">For example: `facet=category,count:5` gets the top five categories in facet results.</span></span>  
  * <span data-ttu-id="fd94d-860">**Remarque** : si le paramètre `count` est inférieur au nombre de termes uniques, les résultats seront peut-être inexacts.</span><span class="sxs-lookup"><span data-stu-id="fd94d-860">**Note**: If the `count` parameter is less than the number of unique terms, the results may not be accurate.</span></span> <span data-ttu-id="fd94d-861">Cela s'explique par la manière dont les requêtes de facettes sont distribuées entre les partitions.</span><span class="sxs-lookup"><span data-stu-id="fd94d-861">This is due to the way faceting queries are distributed across shards.</span></span> <span data-ttu-id="fd94d-862">L'attribution d'une valeur supérieure pour `count` augmente généralement la précision du nombre de termes, mais au détriment des performances.</span><span class="sxs-lookup"><span data-stu-id="fd94d-862">Increasing `count` generally increases the accuracy of the term counts, but at a performance cost.</span></span>
* <span data-ttu-id="fd94d-863">`sort` (`count` pour effectuer un tri par nombre par ordre *décroissant*, `-count` pour effectuer un tri par nombre par ordre *croissant*, `value` pour effectuer un tri par valeur par ordre *croissant* ou `-value` pour effectuer un tri par valeur par ordre *décroissant*)</span><span class="sxs-lookup"><span data-stu-id="fd94d-863">`sort` (one of `count` to sort *descending* by count, `-count` to sort *ascending* by count, `value` to sort *ascending* by value, or `-value` to sort *descending* by value)</span></span>
  * <span data-ttu-id="fd94d-864">Par exemple : `facet=category,count:3,sort:count` obtient les trois premières catégories des résultats de facette triées par ordre décroissant du nombre de documents de chaque ville.</span><span class="sxs-lookup"><span data-stu-id="fd94d-864">For example: `facet=category,count:3,sort:count` gets the top three categories in facet results in descending order by the number of documents with each city name.</span></span> <span data-ttu-id="fd94d-865">Par exemple, si les trois premières catégories sont Budget, Motel et Luxe, que Budget a 5 accès, Motel en a 6 et Luxe en a 4, les compartiments apparaîtront dans l'ordre Motel, Budget et Luxe.</span><span class="sxs-lookup"><span data-stu-id="fd94d-865">For example, if the top three categories are Budget, Motel, and Luxury, and Budget has 5 hits, Motel has 6, and Luxury has 4, then the buckets will be in the order Motel, Budget, Luxury.</span></span>
  * <span data-ttu-id="fd94d-866">Par exemple : `facet=rating,sort:-value` génère des compartiments pour tous les classements possibles, triés par ordre décroissant des valeurs.</span><span class="sxs-lookup"><span data-stu-id="fd94d-866">For example: `facet=rating,sort:-value` produces buckets for all possible ratings, in descending order by value.</span></span> <span data-ttu-id="fd94d-867">Par exemple, si les classements vont de 1 à 5, les compartiments apparaissent dans l'ordre 5, 4, 3, 2, 1, quel que soit le nombre de documents qui correspond à chaque classement.</span><span class="sxs-lookup"><span data-stu-id="fd94d-867">For example, if the ratings are from 1 to 5, the buckets will be ordered 5, 4, 3, 2, 1, irrespective of how many documents match each rating.</span></span>
* <span data-ttu-id="fd94d-868">`values` (valeur numérique délimitée une barre verticale ou valeurs `Edm.DateTimeOffset` qui spécifient un ensemble dynamique de valeurs d'entrée de facette)</span><span class="sxs-lookup"><span data-stu-id="fd94d-868">`values` (pipe-delimited numeric or `Edm.DateTimeOffset` values specifying a dynamic set of facet entry values)</span></span>
  * <span data-ttu-id="fd94d-869">Par exemple : `facet=baseRate,values:10|20` génère trois compartiments : un pour le taux de base compris entre 0 et 10 exclus, un de 10 à 20 exclus et un pour 20 et plus.</span><span class="sxs-lookup"><span data-stu-id="fd94d-869">For example: `facet=baseRate,values:10|20` produces three buckets: One for base rate 0 up to but not including 10, one for 10 up to but not including 20, and one for 20 or higher.</span></span>
  * <span data-ttu-id="fd94d-870">Par exemple : `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` génère deux compartiments : un pour les hôtels rénovés avant février 2010 et un pour les hôtels rénovés à partir du 1er février 2010.</span><span class="sxs-lookup"><span data-stu-id="fd94d-870">For example: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produces two buckets: One for hotels renovated before February 2010, and one for hotels renovated February 1st, 2010 or later.</span></span>
* <span data-ttu-id="fd94d-871">`interval` (intervalle d'entiers supérieur à 0 pour les nombres ou `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` pour les valeurs de date et heure)</span><span class="sxs-lookup"><span data-stu-id="fd94d-871">`interval` (integer interval greater than 0 for numbers, or `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` for date time values)</span></span>
  * <span data-ttu-id="fd94d-872">Par exemple : `facet=baseRate,interval:100` génère des compartiments basés sur des plages de taux de base comprenant 100 valeurs.</span><span class="sxs-lookup"><span data-stu-id="fd94d-872">For example: `facet=baseRate,interval:100` produces buckets based on base rate ranges of size 100.</span></span> <span data-ttu-id="fd94d-873">Par exemple, si les taux de base sont tous compris entre 60 dollars et 600 dollars, il y aura les compartiments suivants : 0-100, 100-200, 200-300, 300-400, 400-500 et 500-600.</span><span class="sxs-lookup"><span data-stu-id="fd94d-873">For example, if base rates are all between $60 and $600, there will be buckets for 0-100, 100-200, 200-300, 300-400, 400-500, and 500-600.</span></span>
  * <span data-ttu-id="fd94d-874">Par exemple : `facet=lastRenovationDate,interval:year` génère un compartiment pour chaque année de rénovation des hôtels.</span><span class="sxs-lookup"><span data-stu-id="fd94d-874">For example: `facet=lastRenovationDate,interval:year` produces one bucket for each year when hotels were renovated.</span></span>
* <span data-ttu-id="fd94d-875">`timeoffset` ([+-]hh:mm, [+-]hhmm, ou [+-]hh) `timeoffset` est facultatif.</span><span class="sxs-lookup"><span data-stu-id="fd94d-875">`timeoffset` ([+-]hh:mm, [+-]hhmm, or [+-]hh) `timeoffset` is optional.</span></span> <span data-ttu-id="fd94d-876">Il peut uniquement être associé à l’option `interval`, et seulement lorsqu’il est appliqué à un champ de type `Edm.DateTimeOffset`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-876">It can only be combined with the `interval` option, and only when applied to a field of type `Edm.DateTimeOffset`.</span></span> <span data-ttu-id="fd94d-877">La valeur spécifie le décalage horaire UTC à prendre en compte lors de la définition des limites de temps.</span><span class="sxs-lookup"><span data-stu-id="fd94d-877">The value specifies the UTC time offset to account for in setting time boundaries.</span></span>
  * <span data-ttu-id="fd94d-878">Par exemple : `facet=lastRenovationDate,interval:day,timeoffset:-01:00` utilise la limite de la journée qui commence à 01:00:00 UTC (minuit dans le fuseau horaire cible)</span><span class="sxs-lookup"><span data-stu-id="fd94d-878">For example: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` uses the day boundary that starts at 01:00:00 UTC (midnight in the target time zone)</span></span>
* <span data-ttu-id="fd94d-879">**Remarque** : `count` et `sort` peuvent être combinés dans la même spécification de facette, mais ils ne peuvent pas être combinés avec `interval` ou `values`, et `interval` et `values` ne peuvent pas être combinés ensemble.</span><span class="sxs-lookup"><span data-stu-id="fd94d-879">**Note**: `count` and `sort` can be combined in the same facet specification, but they cannot be combined with `interval` or `values`, and `interval` and `values` cannot be combined together.</span></span>
* <span data-ttu-id="fd94d-880">**Remarque** : les facettes d’intervalle de date et d’heure sont calculées en fonction de l’heure UTC si `timeoffset` n’est pas spécifié.</span><span class="sxs-lookup"><span data-stu-id="fd94d-880">**Note**: Interval facets on date time are computed based on UTC time if `timeoffset` is not specified.</span></span> <span data-ttu-id="fd94d-881">Par exemple : pour `facet=lastRenovationDate,interval:day`, la limite de la journée commence à 00:00:00 UTC.</span><span class="sxs-lookup"><span data-stu-id="fd94d-881">For example: for `facet=lastRenovationDate,interval:day`, the day boundary starts at 00:00:00 UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="fd94d-882">Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `facets` au lieu de `facet`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-882">When calling **Search** using POST, this parameter is named `facets` instead of `facet`.</span></span> <span data-ttu-id="fd94d-883">En outre, vous le spécifiez sous forme de tableau JSON de chaînes où chaque chaîne est une expression de facette distincte.</span><span class="sxs-lookup"><span data-stu-id="fd94d-883">Also, you specify it as a JSON array of strings where each string is a separate facet expression.</span></span>
> 
> 

<span data-ttu-id="fd94d-884">`$filter=[string]` (facultatif) : expression de recherche structurée avec une syntaxe OData standard.</span><span class="sxs-lookup"><span data-stu-id="fd94d-884">`$filter=[string]` (optional) - A structured search expression in standard OData syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="fd94d-885">Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `filter` au lieu de `$filter`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-885">When calling **Search** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="fd94d-886">`highlight=[string]` (facultatif) : ensemble de noms de champ séparés par des virgules pour la mise en surbrillance des correspondances.</span><span class="sxs-lookup"><span data-stu-id="fd94d-886">`highlight=[string]` (optional) - A set of comma-separated field names used for hit highlights.</span></span> <span data-ttu-id="fd94d-887">Seuls les champs `searchable` peuvent être utilisés pour la mise en surbrillance des correspondances.</span><span class="sxs-lookup"><span data-stu-id="fd94d-887">Only `searchable` fields can be used for hit highlighting.</span></span>

<span data-ttu-id="fd94d-888">`highlightPreTag=[string]` (facultatif, la valeur par défaut est `<em>`) : balise de chaîne qui ajoute un préfixe aux mises en surbrillance des correspondances.</span><span class="sxs-lookup"><span data-stu-id="fd94d-888">`highlightPreTag=[string]` (optional, defaults to `<em>`) - A string tag that prepends to hit highlights.</span></span> <span data-ttu-id="fd94d-889">Doit être défini avec `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-889">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="fd94d-890">Lors de l’appel de **Search** à l’aide de GET, les caractères réservés dans l’URL doivent être codés en pourcentage (par exemple, %23 au lieu de #).</span><span class="sxs-lookup"><span data-stu-id="fd94d-890">When calling **Search** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="fd94d-891">`highlightPostTag=[string]` (facultatif, la valeur par défaut est `</em>`) : balise de chaîne qui ajoute un élément aux mises en surbrillance des correspondances.</span><span class="sxs-lookup"><span data-stu-id="fd94d-891">`highlightPostTag=[string]` (optional, defaults to `</em>`) - a string tag that appends to hit highlights.</span></span> <span data-ttu-id="fd94d-892">Doit être défini avec `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-892">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="fd94d-893">Lors de l’appel de **Search** à l’aide de GET, les caractères réservés dans l’URL doivent être codés en pourcentage (par exemple, %23 au lieu de #).</span><span class="sxs-lookup"><span data-stu-id="fd94d-893">When calling **Search** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="fd94d-894">`scoringProfile=[string]` (facultatif) : nom d'un profil de calcul de score pour évaluer les scores de correspondance des documents afin de trier les résultats.</span><span class="sxs-lookup"><span data-stu-id="fd94d-894">`scoringProfile=[string]` (optional) - The name of a scoring profile to evaluate match scores for matching documents in order to sort the results.</span></span>

<span data-ttu-id="fd94d-895">`scoringParameter=[string]` (zéro ou plus) : indique la valeur de chaque paramètre défini dans une fonction de calcul de score (par exemple, `referencePointParameter`) au format `name-value1,value2,...`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-895">`scoringParameter=[string]` (zero or more) - Indicates the values for each parameter defined in a scoring function (for example, `referencePointParameter`) using the format `name-value1,value2,...`.</span></span>

* <span data-ttu-id="fd94d-896">Par exemple, si le profil de calcul de score définit une fonction avec un paramètre appelé « mylocation » l’option de chaîne de requête est `&scoringParameter=mylocation--122.2,44.8`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-896">For example, if the scoring profile defines a function with a parameter called "mylocation" the query string option would be `&scoringParameter=mylocation--122.2,44.8`.</span></span> <span data-ttu-id="fd94d-897">Le premier tiret sépare le nom de la liste de valeurs, tandis que le second tiret fait partie de la première valeur (la longitude dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="fd94d-897">The first dash separates the name from the value list, while the second dash is part of the first value (longitude in this example).</span></span>
* <span data-ttu-id="fd94d-898">Pour les paramètres de score, par exemple pour le renforcement des balises, qui peuvent contenir des virgules, vous pouvez ignorer ces valeurs dans la liste à l’aide de guillemets simples.</span><span class="sxs-lookup"><span data-stu-id="fd94d-898">For scoring parameters such as for tag boosting that can contain commas, you can escape any such values in the list using single quotes.</span></span> <span data-ttu-id="fd94d-899">Si les valeurs elles-mêmes contiennent des guillemets simples, vous pouvez les ignorer en les doublant.</span><span class="sxs-lookup"><span data-stu-id="fd94d-899">If the values themselves contain single quotes, you can escape them by doubling.</span></span>
  * <span data-ttu-id="fd94d-900">Par exemple, si vous avez un paramètre de renforcement des balises appelé « mytag » et que vous souhaitez renforcer les valeurs de balise « Hello, O’Brien » et « Smith », l’option de la chaîne de requête serait `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-900">For example, if you have a tag boosting parameter called "mytag" and you want to boost on the tag values "Hello, O'Brien" and "Smith", the query string option would be `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span></span> <span data-ttu-id="fd94d-901">Notez que les guillemets sont uniquement requis pour les valeurs qui contiennent des virgules.</span><span class="sxs-lookup"><span data-stu-id="fd94d-901">Note that quotes are only required for values that contain commas.</span></span>

> [!NOTE]
> <span data-ttu-id="fd94d-902">Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `scoringParameters` au lieu de `scoringParameter`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-902">When calling **Search** using POST, this parameter is named `scoringParameters` instead of `scoringParameter`.</span></span> <span data-ttu-id="fd94d-903">En outre, vous le spécifiez sous forme de tableau JSON de chaînes où chaque chaîne est une paire `name-values` distincte.</span><span class="sxs-lookup"><span data-stu-id="fd94d-903">Also, you specify it as a JSON array of strings where each string is a separate `name-values` pair.</span></span>
> 
> 

<span data-ttu-id="fd94d-904">`minimumCoverage` (facultatif, valeur par défaut 100) : nombre compris entre 0 et 100 indiquant le pourcentage de l’index qui doit être couvert par une requête de recherche afin que la requête soit déclarée comme un succès.</span><span class="sxs-lookup"><span data-stu-id="fd94d-904">`minimumCoverage` (optional, defaults to 100) - a number between 0 and 100 indicating the percentage of the index that must be covered by a search query in order for the query to be reported as a success.</span></span> <span data-ttu-id="fd94d-905">Par défaut, la totalité de l’index doit être disponible ou `Search` retourne le code d’état HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="fd94d-905">By default, the entire index must be available or `Search` will return HTTP status code 503.</span></span> <span data-ttu-id="fd94d-906">Si vous définissez `minimumCoverage` et que `Search` réussit, le code HTTP 200 est retourné et inclut une valeur `@search.coverage` dans la réponse indiquant le pourcentage de l’index inclus dans la requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-906">If you set `minimumCoverage` and `Search` succeeds, it will return HTTP 200 and include a `@search.coverage` value in the response indicating the percentage of the index that was included in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="fd94d-907">La définition de ce paramètre à une valeur inférieure à 100 peut être utile pour garantir la disponibilité de la recherche même pour les services ayant un seul réplica.</span><span class="sxs-lookup"><span data-stu-id="fd94d-907">Setting this parameter to a value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="fd94d-908">Cependant, il n’y a pas de garantie que tous les documents correspondants seront présents dans les résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-908">However, not all matching documents are guaranteed to be present in the search results.</span></span> <span data-ttu-id="fd94d-909">Si le rappel de recherche est plus important pour votre application que la disponibilité, il est préférable de laisser `minimumCoverage` avec 100 comme valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="fd94d-909">If search recall is more important to your application than availability, then it's best to leave `minimumCoverage` at its default value of 100.</span></span>
> 
> 

<span data-ttu-id="fd94d-910">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="fd94d-910">`api-version=[string]` (required).</span></span> <span data-ttu-id="fd94d-911">La version préliminaire est `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-911">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="fd94d-912">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-912">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="fd94d-913">Remarque : pour cette opération, la `api-version` est spécifiée comme paramètre de requête dans l’URL, que vous appeliez **Search** à l’aide de POST ou de GET.</span><span class="sxs-lookup"><span data-stu-id="fd94d-913">Note: For this operation, the `api-version` is specified as a query parameter in the URL regardless of whether you call **Search** with GET or POST.</span></span>

<span data-ttu-id="fd94d-914">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-914">**Request Headers**</span></span>

<span data-ttu-id="fd94d-915">La liste suivante décrit les en-têtes de requête obligatoires et facultatifs.</span><span class="sxs-lookup"><span data-stu-id="fd94d-915">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="fd94d-916">`api-key` : l'en-tête `api-key` est utilisé pour authentifier la requête auprès de votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-916">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="fd94d-917">Il s'agit d'une valeur de chaîne, unique pour l'URL de votre service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-917">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="fd94d-918">La requête **Search** peut spécifier une clé d'administration ou une clé de requête pour `api-key`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-918">The **Search** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="fd94d-919">Vous avez également besoin du nom du service pour construire l'URL de la requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-919">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="fd94d-920">Vous pouvez obtenir le nom du service et l'en-tête `api-key` à partir de votre tableau de bord de service dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fd94d-920">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="fd94d-921">Pour obtenir de l'aide sur la navigation dans les pages, consultez [Création d'un service Azure Search dans le portail](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-921">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="fd94d-922">**Corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-922">**Request Body**</span></span>

<span data-ttu-id="fd94d-923">Pour GET : aucun.</span><span class="sxs-lookup"><span data-stu-id="fd94d-923">For GET: None.</span></span>

<span data-ttu-id="fd94d-924">Pour POST :</span><span class="sxs-lookup"><span data-stu-id="fd94d-924">For POST:</span></span>

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered to declare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

<span data-ttu-id="fd94d-925">**Continuation des réponses de recherche partielle**</span><span class="sxs-lookup"><span data-stu-id="fd94d-925">**Continuation of Partial Search Responses**</span></span>

<span data-ttu-id="fd94d-926">Parfois, Azure Search ne peut pas rendre tous les résultats requis dans une seule réponse de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-926">Sometimes Azure Search can't return all the requested results in a single Search response.</span></span> <span data-ttu-id="fd94d-927">Cela peut se produire pour différentes raisons, par exemple lorsque la requête nécessite un trop grand nombre de documents en ne spécifiant pas `$top` ou en spécifiant une valeur pour `$top` qui est trop grande.</span><span class="sxs-lookup"><span data-stu-id="fd94d-927">This can happen for different reasons, such as when the query requests too many documents by not specifying `$top` or specifying a value for `$top` that is too large.</span></span> <span data-ttu-id="fd94d-928">Dans ce cas, Azure Search inclura l’annotation `@odata.nextLink` dans le corps de réponse, ainsi que `@search.nextPageParameters` s’il s’agissait d’une demande POST.</span><span class="sxs-lookup"><span data-stu-id="fd94d-928">In such cases, Azure Search will include the `@odata.nextLink` annotation in the response body, and also `@search.nextPageParameters` if it was a POST request.</span></span> <span data-ttu-id="fd94d-929">Vous pouvez utiliser les valeurs de ces annotations pour formuler une autre demande de recherche afin d’obtenir la partie suivante de la réponse de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-929">You can use the values of these annotations to formulate another Search request to get the next part of the search response.</span></span> <span data-ttu-id="fd94d-930">Il s’agit d’une ***continuation*** de la demande de recherche d’origine et les annotations sont généralement appelées ***jetons de continuation***.</span><span class="sxs-lookup"><span data-stu-id="fd94d-930">This is called a ***continuation*** of the original Search request, and the annotations are generally called ***continuation tokens***.</span></span> <span data-ttu-id="fd94d-931">Consultez [l’exemple ci-dessous](#SearchResponse) pour plus d’informations sur la syntaxe de ces annotations et où elles apparaissent dans le corps de réponse.</span><span class="sxs-lookup"><span data-stu-id="fd94d-931">See [the example below](#SearchResponse) for details on the syntax of these annotations and where they appear in the response body.</span></span> 

<span data-ttu-id="fd94d-932">Les raisons pour lesquelles Azure Search peut rendre des jetons de continuation sont liées à l’implémentation et susceptibles d’être modifiées.</span><span class="sxs-lookup"><span data-stu-id="fd94d-932">The reasons why Azure Search might return continuation tokens are implementation-specific and subject to change.</span></span> <span data-ttu-id="fd94d-933">Les clients puissants doivent toujours être prêts à traiter des cas où des documents plus moins nombreux que prévu sont renvoyés et un jeton de continuation est inclus pour poursuivre la récupération des documents.</span><span class="sxs-lookup"><span data-stu-id="fd94d-933">Robust clients should always be ready to handle cases where fewer documents than expected are returned and a continuation token is included to continue retrieving documents.</span></span> <span data-ttu-id="fd94d-934">Notez également que vous devez utiliser la même méthode HTTP que pour la demande d’origine pour pouvoir poursuivre.</span><span class="sxs-lookup"><span data-stu-id="fd94d-934">Also note that you must use the same HTTP method as the original request in order to continue.</span></span> <span data-ttu-id="fd94d-935">Par exemple, si vous avez envoyé une demande GET, toutes les demandes de continuation que vous envoyez doivent également utiliser GET (y compris pour POST).</span><span class="sxs-lookup"><span data-stu-id="fd94d-935">For example, if you sent a GET request, any continuation requests you send must also use GET (and likewise for POST).</span></span>

<span data-ttu-id="fd94d-936"><a name="SearchResponse"></a>
**Réponse**</span><span class="sxs-lookup"><span data-stu-id="fd94d-936"><a name="SearchResponse"></a>
**Response**</span></span>

<span data-ttu-id="fd94d-937">Code d'état : 200 OK est retourné pour une réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="fd94d-937">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@odata.count": # (if $count=true was provided in the query),
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "@search.facets": { (if faceting was specified in the query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body to fetch the next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL to fetch the next page of results if not all results could be returned in this response; Applies to both GET and POST)
    }

<span data-ttu-id="fd94d-938">**Exemples :**</span><span class="sxs-lookup"><span data-stu-id="fd94d-938">**Examples:**</span></span>

<span data-ttu-id="fd94d-939">Vous trouverez d'autres exemples dans la page [Syntaxe d'expression OData pour Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-939">You can find additional examples on the [OData Expression Syntax for Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.</span></span>

1)    <span data-ttu-id="fd94d-940">Effectuer une recherche dans l'index trié par date par ordre décroissant.</span><span class="sxs-lookup"><span data-stu-id="fd94d-940">Search the Index sorted descending by date.</span></span>

    <span data-ttu-id="fd94d-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="fd94d-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="fd94d-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span><span class="sxs-lookup"><span data-stu-id="fd94d-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span></span>

2)    <span data-ttu-id="fd94d-943">Dans une recherche à facettes, interroger l’index et récupérer des facettes pour des catégories, des classements, des balises, ainsi que des éléments avec une valeur baseRate comprise dans des plages spécifiques :</span><span class="sxs-lookup"><span data-stu-id="fd94d-943">In a faceted search, search the index and retrieve facets for categories, rating, tags, as well as items with baseRate in specific ranges:</span></span>

    <span data-ttu-id="fd94d-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="fd94d-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="fd94d-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span><span class="sxs-lookup"><span data-stu-id="fd94d-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span></span>

3)    <span data-ttu-id="fd94d-946">À l’aide d’un filtre, limiter les résultats de la précédente requête à facettes une fois que l’utilisateur a cliqué sur le classement 3 et la catégorie « Motel » :</span><span class="sxs-lookup"><span data-stu-id="fd94d-946">Using a filter, narrow down the previous faceted query results after the user clicks on rating 3 and category "Motel":</span></span>

    <span data-ttu-id="fd94d-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="fd94d-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="fd94d-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span><span class="sxs-lookup"><span data-stu-id="fd94d-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span></span>

4) <span data-ttu-id="fd94d-949">Dans une recherche à facettes, définir une limite supérieure sur des termes uniques retournés dans une requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-949">In a faceted search, set an upper limit on unique terms returned in a query.</span></span> <span data-ttu-id="fd94d-950">La valeur par défaut est 10, mais vous pouvez augmenter ou diminuer cette valeur à l'aide du paramètre `count` sur l'attribut `facet` :</span><span class="sxs-lookup"><span data-stu-id="fd94d-950">The default is 10, but you can increase or decrease this value using the `count` parameter on the `facet` attribute:</span></span>

    <span data-ttu-id="fd94d-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="fd94d-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="fd94d-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span><span class="sxs-lookup"><span data-stu-id="fd94d-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span></span>

5)    <span data-ttu-id="fd94d-953">Effectuer une recherche dans des champs spécifiques de l’index. Par exemple, un champ propre à la langue :</span><span class="sxs-lookup"><span data-stu-id="fd94d-953">Search the Index within specific fields; For example, a language-specific field:</span></span>

    <span data-ttu-id="fd94d-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="fd94d-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="fd94d-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span><span class="sxs-lookup"><span data-stu-id="fd94d-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span></span>

6) <span data-ttu-id="fd94d-956">Effectuer une recherche dans plusieurs champs de l’index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-956">Search the Index across multiple fields.</span></span> <span data-ttu-id="fd94d-957">Par exemple, vous pouvez stocker et interroger des champs pouvant faire l'objet d'une recherche en plusieurs langues, le tout dans le même index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-957">For example, you can store and query searchable fields in multiple languages, all within the same index.</span></span>  <span data-ttu-id="fd94d-958">Si des descriptions en anglais et en français coexistent dans le même document, vous pouvez en retourner certaines ou la totalité dans les résultats de la requête :</span><span class="sxs-lookup"><span data-stu-id="fd94d-958">If English and French descriptions co-exist in the same document, you can return any or all in the query results:</span></span>

    <span data-ttu-id="fd94d-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="fd94d-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="fd94d-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span><span class="sxs-lookup"><span data-stu-id="fd94d-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span></span>

<span data-ttu-id="fd94d-961">Notez que vous pouvez interroger uniquement un index à la fois.</span><span class="sxs-lookup"><span data-stu-id="fd94d-961">Note that you can only query one index at a time.</span></span> <span data-ttu-id="fd94d-962">Ne créez pas plusieurs index pour chaque langue, sauf si vous prévoyez d'interroger un seul index à la fois.</span><span class="sxs-lookup"><span data-stu-id="fd94d-962">Do not create multiple indexes for each language unless you plan to query one at a time.</span></span>

7)    <span data-ttu-id="fd94d-963">Pagination : obtenir la 1re page d’éléments (la taille de la page est 10) :</span><span class="sxs-lookup"><span data-stu-id="fd94d-963">Paging - Get the 1st page of items (page size is 10):</span></span>

    <span data-ttu-id="fd94d-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="fd94d-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="fd94d-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="fd94d-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span></span>

8)    <span data-ttu-id="fd94d-966">Pagination : obtenir la 2e page d’éléments (la taille de la page est 10) :</span><span class="sxs-lookup"><span data-stu-id="fd94d-966">Paging - Get the 2nd page of items (page size is 10):</span></span>

    <span data-ttu-id="fd94d-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="fd94d-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="fd94d-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="fd94d-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span></span>

9)    <span data-ttu-id="fd94d-969">Récupérer un ensemble spécifique de champs :</span><span class="sxs-lookup"><span data-stu-id="fd94d-969">Retrieve a specific set of fields:</span></span>

    <span data-ttu-id="fd94d-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="fd94d-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="fd94d-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span><span class="sxs-lookup"><span data-stu-id="fd94d-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span></span>

10)  <span data-ttu-id="fd94d-972">Récupérer les documents correspondant à une expression de filtre spécifique :</span><span class="sxs-lookup"><span data-stu-id="fd94d-972">Retrieve documents matching a specific filter expression:</span></span>

    <span data-ttu-id="fd94d-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="fd94d-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="fd94d-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span><span class="sxs-lookup"><span data-stu-id="fd94d-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span></span>

11) <span data-ttu-id="fd94d-975">Effectuer une recherche dans l’index et retourner des fragments avec des mises en surbrillance des correspondances</span><span class="sxs-lookup"><span data-stu-id="fd94d-975">Search the index and return fragments with hit highlights</span></span>

    <span data-ttu-id="fd94d-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="fd94d-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="fd94d-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span><span class="sxs-lookup"><span data-stu-id="fd94d-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span></span>

12) <span data-ttu-id="fd94d-978">Effectuer une recherche dans l’index et retourner des documents triés du plus proche au plus éloigné par rapport à un emplacement de référence</span><span class="sxs-lookup"><span data-stu-id="fd94d-978">Search the index and return documents sorted from closer to farther away from a reference location</span></span>

    <span data-ttu-id="fd94d-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="fd94d-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="fd94d-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span><span class="sxs-lookup"><span data-stu-id="fd94d-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span></span>

13) <span data-ttu-id="fd94d-981">Effectuer une recherche dans l’index en supposant qu’il existe un profil de calcul de score appelé « geo » avec deux fonctions de calcul de score de distance : l’une définit un paramètre appelé « currentLocation » et l’autre un paramètre appelé « lastLocation »</span><span class="sxs-lookup"><span data-stu-id="fd94d-981">Search the index assuming there's a scoring profile called "geo" with two distance scoring functions, one defining a parameter called "currentLocation" and one defining a parameter called "lastLocation"</span></span>

    <span data-ttu-id="fd94d-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="fd94d-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="fd94d-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span><span class="sxs-lookup"><span data-stu-id="fd94d-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span></span>

14) <span data-ttu-id="fd94d-984">Rechercher des documents dans l’index à l’aide d’une [syntaxe de requête simple](https://msdn.microsoft.com/library/dn798920.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd94d-984">Find documents in the index using [simple query syntax](https://msdn.microsoft.com/library/dn798920.aspx).</span></span> <span data-ttu-id="fd94d-985">Cette requête renvoie les hôtels où les champs pouvant faire l'objet d'une recherche contiennent les termes « confort » et « emplacement », mais pas « motel » :</span><span class="sxs-lookup"><span data-stu-id="fd94d-985">This query returns hotels where searchable fields contain the terms "comfort" and "location" but not "motel":</span></span>

    <span data-ttu-id="fd94d-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="fd94d-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="fd94d-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="fd94d-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span></span>

<span data-ttu-id="fd94d-988">Notez l'utilisation de `searchMode=all` ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="fd94d-988">Note the use of `searchMode=all` above.</span></span> <span data-ttu-id="fd94d-989">L'ajout de ce paramètre remplace la valeur par défaut `searchMode=any`, ce qui garantit que `-motel` signifie « ET PAS » au lieu de « OU PAS ».</span><span class="sxs-lookup"><span data-stu-id="fd94d-989">Including this parameter overrides the default of `searchMode=any`, ensuring that `-motel` means "AND NOT" instead of "OR NOT".</span></span> <span data-ttu-id="fd94d-990">Sans `searchMode=all`, vous obtenez « OU PAS » qui étend au lieu de limiter les résultats de recherche, et cela peut être contraire à l'intuition pour certains utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="fd94d-990">Without `searchMode=all`, you get "OR NOT" which expands rather than restricts search results, and this can be counter-intuitive to some users.</span></span>

15) <span data-ttu-id="fd94d-991">Rechercher des documents dans l’index à l’aide d’une [syntaxe de requête Lucene](https://msdn.microsoft.com/library/mt589323.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd94d-991">Find documents in the index using [lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx).</span></span> <span data-ttu-id="fd94d-992">Cette requête renvoie les hôtels où le champ de catégorie contient le terme « budget » et tous les champs pouvant faire l’objet d’une recherche contenant l’expression « récemment rénové ».</span><span class="sxs-lookup"><span data-stu-id="fd94d-992">This query returns hotels where the category field contains the term "budget" and all searchable fields containing the phrase "recently renovated".</span></span> <span data-ttu-id="fd94d-993">Les documents contenant l’expression « récemment rénové » sont mieux classés en raison de la valeur de renforcement du terme (3)</span><span class="sxs-lookup"><span data-stu-id="fd94d-993">Documents containing the phrase "recently renovated" are ranked higher as a result of the term boost value (3)</span></span>

    <span data-ttu-id="fd94d-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span><span class="sxs-lookup"><span data-stu-id="fd94d-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span></span>

    <span data-ttu-id="fd94d-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="fd94d-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span></span>

<a name="LookupAPI"></a>

## <a name="lookup-document"></a><span data-ttu-id="fd94d-996">Recherche de document</span><span class="sxs-lookup"><span data-stu-id="fd94d-996">Lookup Document</span></span>
<span data-ttu-id="fd94d-997">L'opération **Lookup Document** récupère un document dans Azure Search.</span><span class="sxs-lookup"><span data-stu-id="fd94d-997">The **Lookup Document** operation retrieves a document from Azure Search.</span></span> <span data-ttu-id="fd94d-998">Cela est utile quand un utilisateur clique sur un résultat de recherche en particulier et que vous voulez rechercher des détails spécifiques sur ce document.</span><span class="sxs-lookup"><span data-stu-id="fd94d-998">This is useful when a user clicks on a specific search result, and you want to look up specific details about that document.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

<span data-ttu-id="fd94d-999">**Requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-999">**Request**</span></span>

<span data-ttu-id="fd94d-1000">Le protocole HTTPS est requis pour les requêtes de service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1000">HTTPS is required for service requests.</span></span> <span data-ttu-id="fd94d-1001">La requête **Lookup Document** peut être construite comme suit.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1001">The **Lookup Document** request can be constructed as follows.</span></span>

    GET /indexes/[index name]/docs/key?[query parameters]

<span data-ttu-id="fd94d-1002">Vous pouvez aussi utiliser la syntaxe traditionnelle OData pour la recherche de clé :</span><span class="sxs-lookup"><span data-stu-id="fd94d-1002">Alternatively, you can use the traditional OData syntax for key lookup:</span></span>

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

<span data-ttu-id="fd94d-1003">L’URI de la requête inclut un [nom d’index] et une [clé], qui spécifient le document à extraire de l’index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1003">The request URI includes an [index name] and [key], specifying which document to retrieve from which index.</span></span> <span data-ttu-id="fd94d-1004">Vous ne pouvez obtenir qu'un seul document à la fois.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1004">You can only get one document at a time.</span></span> <span data-ttu-id="fd94d-1005">Utilisez **Search** pour obtenir plusieurs documents dans une requête unique.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1005">Use **Search** to get multiple documents in a single request.</span></span>

<span data-ttu-id="fd94d-1006">**Paramètres de requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-1006">**Query Parameters**</span></span>

<span data-ttu-id="fd94d-1007">`$select=[string]` (facultatif) : liste de champs séparés par des virgules à récupérer.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1007">`$select=[string]` (optional) - a list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="fd94d-1008">Si la valeur n'est pas spécifiée ou est `*`, tous les champs marqués comme récupérables dans le schéma sont inclus dans la projection.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1008">If unspecified or set to `*`, all fields marked as retrievable in the schema are included in the projection.</span></span>

<span data-ttu-id="fd94d-1009">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="fd94d-1009">`api-version=[string]` (required).</span></span> <span data-ttu-id="fd94d-1010">La version préliminaire est `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1010">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="fd94d-1011">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-1011">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="fd94d-1012">Remarque : pour cette opération, `api-version` est spécifié en tant que paramètre de requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1012">Note: For this operation, the `api-version` is specified as a query parameter.</span></span>

<span data-ttu-id="fd94d-1013">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-1013">**Request Headers**</span></span>

<span data-ttu-id="fd94d-1014">La liste suivante décrit les en-têtes de requête obligatoires et facultatifs.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1014">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="fd94d-1015">`api-key` : l'en-tête `api-key` est utilisé pour authentifier la requête auprès de votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1015">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="fd94d-1016">Il s'agit d'une valeur de chaîne, unique pour l'URL de votre service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1016">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="fd94d-1017">La requête **Lookup Document** peut spécifier une clé d’administration ou une clé de requête pour `api-key`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1017">The **Lookup Document** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="fd94d-1018">Vous avez également besoin du nom du service pour construire l'URL de la requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1018">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="fd94d-1019">Vous pouvez obtenir le nom du service et l'en-tête `api-key` à partir de votre tableau de bord de service dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1019">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="fd94d-1020">Pour obtenir de l'aide sur la navigation dans les pages, consultez [Création d'un service Azure Search dans le portail](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-1020">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="fd94d-1021">**Corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-1021">**Request Body**</span></span>

<span data-ttu-id="fd94d-1022">Aucune.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1022">None.</span></span>

<span data-ttu-id="fd94d-1023">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="fd94d-1023">**Response**</span></span>

<span data-ttu-id="fd94d-1024">Code d'état : 200 OK est retourné pour une réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1024">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      field_name: field_value (fields matching the default or specified projection)
    }

<span data-ttu-id="fd94d-1025">**Exemple**</span><span class="sxs-lookup"><span data-stu-id="fd94d-1025">**Example**</span></span>

<span data-ttu-id="fd94d-1026">Rechercher le document qui contient la clé « 2 »</span><span class="sxs-lookup"><span data-stu-id="fd94d-1026">Lookup the document that has key '2'</span></span>

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

<span data-ttu-id="fd94d-1027">Rechercher le document qui contient la clé « 3 » à l'aide de la syntaxe OData :</span><span class="sxs-lookup"><span data-stu-id="fd94d-1027">Lookup the document that has key '3' using OData syntax:</span></span>

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a><span data-ttu-id="fd94d-1028">Nombre de documents</span><span class="sxs-lookup"><span data-stu-id="fd94d-1028">Count Documents</span></span>
<span data-ttu-id="fd94d-1029">L'opération **Count Documents** récupère le nombre de documents dans un index de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1029">The **Count Documents** operation retrieves a count of the number of documents in a search index.</span></span> <span data-ttu-id="fd94d-1030">La syntaxe `$count` fait partie du protocole OData.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1030">The `$count` syntax is part of the OData protocol.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

<span data-ttu-id="fd94d-1031">**Requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-1031">**Request**</span></span>

<span data-ttu-id="fd94d-1032">Le protocole HTTPS est requis pour les requêtes de service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1032">HTTPS is required for service requests.</span></span> <span data-ttu-id="fd94d-1033">La requête **Count Documents** peut être construite à l'aide de la méthode GET.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1033">The **Count Documents** request can be constructed using the GET method.</span></span>

<span data-ttu-id="fd94d-1034">Le [nom d’index] dans l’URI de la requête indique au service de retourner le nombre de tous les éléments de la collection de documents de l’index spécifié.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1034">The [index name] in the request URI tells the service to return a count of all items in the docs collection of the specified index.</span></span>

<span data-ttu-id="fd94d-1035">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="fd94d-1035">`api-version=[string]` (required).</span></span> <span data-ttu-id="fd94d-1036">La version préliminaire est `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1036">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="fd94d-1037">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-1037">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="fd94d-1038">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-1038">**Request Headers**</span></span>

<span data-ttu-id="fd94d-1039">La liste suivante décrit les en-têtes de requête obligatoires et facultatifs.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1039">The following list describes the required and optional request headers.</span></span>

* <span data-ttu-id="fd94d-1040">`Accept` : cette valeur doit être définie sur `text/plain`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1040">`Accept`: This value must be set to `text/plain`.</span></span>
* <span data-ttu-id="fd94d-1041">`api-key` : l'en-tête `api-key` est utilisé pour authentifier la requête auprès de votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1041">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="fd94d-1042">Il s'agit d'une valeur de chaîne, unique pour l'URL de votre service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1042">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="fd94d-1043">La requête **Count Documents** peut spécifier une clé d’administration ou une clé de requête pour `api-key`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1043">The **Count Documents** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="fd94d-1044">Vous avez également besoin du nom du service pour construire l'URL de la requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1044">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="fd94d-1045">Vous pouvez obtenir le nom du service et l'en-tête `api-key` à partir de votre tableau de bord de service dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1045">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="fd94d-1046">Pour obtenir de l'aide sur la navigation dans les pages, consultez [Création d'un service Azure Search dans le portail](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-1046">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="fd94d-1047">**Corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-1047">**Request Body**</span></span>

<span data-ttu-id="fd94d-1048">Aucune.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1048">None.</span></span>

<span data-ttu-id="fd94d-1049">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="fd94d-1049">**Response**</span></span>

<span data-ttu-id="fd94d-1050">Code d'état : 200 OK est retourné pour une réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1050">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="fd94d-1051">Le corps de la réponse contient la valeur du nombre sous forme d'entier en texte brut.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1051">The response body contains the count value as an integer formatted in plain text.</span></span>

<a name="Suggestions"></a>

## <a name="suggestions"></a><span data-ttu-id="fd94d-1052">Suggestions</span><span class="sxs-lookup"><span data-stu-id="fd94d-1052">Suggestions</span></span>
<span data-ttu-id="fd94d-1053">L'opération **Suggestions** récupère des suggestions basées sur une entrée de recherche partielle.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1053">The **Suggestions** operation retrieves suggestions based on partial search input.</span></span> <span data-ttu-id="fd94d-1054">Elle est généralement utilisée dans les zones de recherche pour fournir des suggestions à mesure que les utilisateurs entrent des termes de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1054">It's typically used in search boxes to provide type-ahead suggestions as users are entering search terms.</span></span>

<span data-ttu-id="fd94d-1055">Les requêtes de suggestions visent à suggérer des documents cibles, le texte suggéré peut donc être répété si plusieurs documents candidats correspondent à la même entrée de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1055">Suggestion requests aim at suggesting target documents, so the suggested text may be repeated if multiple candidate documents match the same search input.</span></span> <span data-ttu-id="fd94d-1056">Vous pouvez utiliser `$select` pour récupérer d'autres champs du document (y compris la clé de document) afin de savoir quel document est la source de chaque suggestion.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1056">You can use `$select` to retrieve other document fields (including the document key) so that you can tell which document is the source for each suggestion.</span></span>

<span data-ttu-id="fd94d-1057">Une opération **Suggestions** est publiée en tant que requête GET ou POST.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1057">A **Suggestions** operation is issued as a GET or POST request.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="fd94d-1058">**Utilisation de POST au lieu de GET**</span><span class="sxs-lookup"><span data-stu-id="fd94d-1058">**When to use POST instead of GET**</span></span>

<span data-ttu-id="fd94d-1059">Lorsque vous utilisez HTTP GET pour appeler l'API **Suggestions** , vous devez savoir que la longueur de l'URL de requête ne peut pas dépasser 8 Ko.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1059">When you use HTTP GET to call the **Suggestions** API, you need to be aware that the length of the request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="fd94d-1060">Cela est généralement suffisamment pour la plupart des applications.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1060">This is usually enough for most applications.</span></span> <span data-ttu-id="fd94d-1061">Toutefois, certaines applications produisent des requêtes très volumineuses, en particulier les expressions de filtre OData.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1061">However, some applications produce very large queries, specifically OData filter expressions.</span></span> <span data-ttu-id="fd94d-1062">Pour ces applications, il est recommandé d'utiliser HTTP POST, car cela permet d'obtenir des filtres plus volumineux que GET.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1062">For these applications, using HTTP POST is a better choice because it allows larger filters than GET.</span></span> <span data-ttu-id="fd94d-1063">Avec POST, le nombre de clauses dans un filtre est le facteur limitant, pas la taille de la chaîne du filtre brut, car la limite de la taille de la requête POST est proche de 16 Mo.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1063">With POST, the number of clauses in a filter is the limiting factor, not the size of the raw filter string since the request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="fd94d-1064">Bien que la limite de la taille de la requête POST est très importante, les expressions de filtre ne peuvent pas être arbitrairement complexes.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1064">Even though the POST request size limit is very large, filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="fd94d-1065">Consultez [Syntaxe d’expression OData](https://msdn.microsoft.com/library/dn798921.aspx) pour plus d’informations sur les limites de complexité des filtres.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1065">See [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="fd94d-1066">**Requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-1066">**Request**</span></span>

<span data-ttu-id="fd94d-1067">Le protocole HTTPS est requis pour les requêtes de service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1067">HTTPS is required for service requests.</span></span> <span data-ttu-id="fd94d-1068">La requête **Suggestions** peut être construite à l’aide des méthodes GET ou POST.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1068">The **Suggestions** request can be constructed using the GET or POST methods.</span></span>

<span data-ttu-id="fd94d-1069">L'URI de la requête spécifie le nom de l'index à interroger.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1069">The request URI specifies the name of the index to query.</span></span> <span data-ttu-id="fd94d-1070">Les paramètres, tels que le terme de recherche partiellement entré, sont spécifiés dans la chaîne de requête pour les requêtes GET et dans le corps de la requête pour les requêtes POST.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1070">Parameters, such as the partially input search term, are specified on the query string in the case of GET requests, and in the request body in the case of POST requests.</span></span>

<span data-ttu-id="fd94d-1071">Pendant la création de requêtes GET, il est recommandé d’ [encoder par URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) les paramètres de requête spécifiques pour appeler l’API REST directement.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1071">As a best practice when creating GET requests, remember to [URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling the REST API directly.</span></span> <span data-ttu-id="fd94d-1072">Pour les opérations **Suggestions** , cela inclut :</span><span class="sxs-lookup"><span data-stu-id="fd94d-1072">For **Suggestions** operations, this includes:</span></span>

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

<span data-ttu-id="fd94d-1073">L'encodage des URL est recommandé uniquement pour les paramètres de requête ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1073">URL encoding is only recommended on the above query parameters.</span></span> <span data-ttu-id="fd94d-1074">Si vous encodez par URL par inadvertance la chaîne de requête entière (tout ce qui figure après ?), les requêtes sont interrompues.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1074">If you inadvertently URL-encode the entire query string (everything after the ?), requests will break.</span></span>

<span data-ttu-id="fd94d-1075">En outre, l'encodage des URL est nécessaire uniquement lors de l'appel direct de l'API REST à l'aide de GET.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1075">Also, URL encoding is only necessary when calling the REST API directly using GET.</span></span> <span data-ttu-id="fd94d-1076">Aucun encodage des URL n’est nécessaire pendant l’appel de **Suggestions** à l’aide de POST, ou quand vous utilisez la [bibliothèque cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx)qui gère l’encodage des URL pour vous.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1076">No URL encoding is necessary when calling **Suggestions** using POST, or when using the [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="fd94d-1077">**Paramètres de requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-1077">**Query Parameters**</span></span>

<span data-ttu-id="fd94d-1078">**Suggestions** accepte plusieurs paramètres qui fournissent les critères de la requête et qui spécifient également le comportement de la recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1078">**Suggestions** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="fd94d-1079">Vous fournissez ces paramètres dans la chaîne de requête de l’URL pendant l’appel de **Suggestions** via GET et en tant que propriétés JSON dans le corps de la requête pendant l’appel de **Suggestions** via POST.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1079">You provide these parameters in the URL query string when calling **Suggestions** via GET, and as JSON properties in the request body when calling **Suggestions** via POST.</span></span> <span data-ttu-id="fd94d-1080">La syntaxe de certains paramètres est légèrement différente entre GET et POST.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1080">The syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="fd94d-1081">Ces différences sont indiquées ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="fd94d-1081">These differences are noted as applicable below:</span></span>

<span data-ttu-id="fd94d-1082">`search=[string]` : texte de recherche à utiliser pour suggérer des requêtes.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1082">`search=[string]` - the search text to use to suggest queries.</span></span> <span data-ttu-id="fd94d-1083">Doit comprendre 1 caractère au minimum et 100 caractères au maximum.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1083">Must be at least 1 character, and no more than 100 characters.</span></span>

<span data-ttu-id="fd94d-1084">`highlightPreTag=[string]` (facultatif) : balise de chaîne qui ajoute un préfixe aux résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1084">`highlightPreTag=[string]` (optional) - a string tag that prepends to search hits.</span></span> <span data-ttu-id="fd94d-1085">Doit être défini avec `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1085">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="fd94d-1086">Pendant l’appel de **Suggestions** à l’aide de GET, les caractères réservés dans l’URL doivent être codés en pourcentage (par exemple, %23 au lieu de #).</span><span class="sxs-lookup"><span data-stu-id="fd94d-1086">When calling **Suggestions** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="fd94d-1087">`highlightPostTag=[string]` (facultatif) : balise de chaîne qui ajoute un élément aux résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1087">`highlightPostTag=[string]` (optional) - a string tag that appends to search hits.</span></span> <span data-ttu-id="fd94d-1088">Doit être défini avec `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1088">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="fd94d-1089">Pendant l’appel de **Suggestions** à l’aide de GET, les caractères réservés dans l’URL doivent être codés en pourcentage (par exemple, %23 au lieu de #).</span><span class="sxs-lookup"><span data-stu-id="fd94d-1089">When calling **Suggestions** using GET, reserved characters in the URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="fd94d-1090">`suggesterName=[string]` : nom du générateur de suggestions, comme spécifié dans la collection `suggesters` qui fait partie de la définition d'index.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1090">`suggesterName=[string]` - the name of the suggester as specified in the `suggesters` collection that's part of the index definition.</span></span> <span data-ttu-id="fd94d-1091">Un `suggester` détermine les champs qui sont analysés pour les termes de requête suggérés.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1091">A `suggester` determines which fields are scanned for suggested query terms.</span></span> <span data-ttu-id="fd94d-1092">Pour plus d'informations, consultez [Générateurs de suggestions](#Suggesters) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-1092">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="fd94d-1093">`fuzzy=[boolean]` (facultatif, valeur par défaut = false) : quand elle est définie avec la valeur true, cette API trouve des suggestions même si un caractère est remplacé ou manquant dans le texte de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1093">`fuzzy=[boolean]` (optional, default = false) - when set to true this API will find suggestions even if there's a substituted or missing character in the search text.</span></span> <span data-ttu-id="fd94d-1094">Bien qu'il en résulte une meilleure expérience, dans certains cas cela a un impact négatif sur les performances, car les recherches de suggestions approximatives sont plus lentes et consomment davantage de ressources.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1094">While this provides a better experience in some scenarios it comes at a performance cost as fuzzy suggestion searches are slower and consume more resources.</span></span>

<span data-ttu-id="fd94d-1095">`searchFields=[string]` (facultatif) : liste des noms de champs séparés par des virgules dans lesquels rechercher le texte spécifié.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1095">`searchFields=[string]` (optional) - the list of comma-separated field names to search for the specified search text.</span></span> <span data-ttu-id="fd94d-1096">Les champs cibles doivent être activés pour les suggestions.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1096">Target fields must be enabled for suggestions.</span></span>

<span data-ttu-id="fd94d-1097">`$top=#` (facultatif, valeur par défaut = 5) : nombre de suggestions à récupérer.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1097">`$top=#` (optional, default = 5) - the number of suggestions to retrieve.</span></span> <span data-ttu-id="fd94d-1098">Doit être un nombre compris entre 1 et 100.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1098">Must be a number between 1 and 100.</span></span>

> [!NOTE]
> <span data-ttu-id="fd94d-1099">Pendant l’appel de **Suggestions** à l’aide de POST, ce paramètre est nommé `top` au lieu de `$top`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1099">When calling **Suggestions** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="fd94d-1100">`$filter=[string]` (facultatif) : expression qui filtre les documents considérés comme des suggestions.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1100">`$filter=[string]` (optional) - an expression that filters the documents considered for suggestions.</span></span>

> [!NOTE]
> <span data-ttu-id="fd94d-1101">Pendant l’appel de **Suggestions** à l’aide de POST, ce paramètre est nommé `filter` au lieu de `$filter`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1101">When calling **Suggestions** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="fd94d-1102">`$orderby=[string]` (facultatif) : liste d'expressions séparées par des virgules selon lesquelles les résultats doivent être triés.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1102">`$orderby=[string]` (optional) - a list of comma-separated expressions to sort the results by.</span></span> <span data-ttu-id="fd94d-1103">Chaque expression peut être un nom de champ ou un appel à la fonction `geo.distance()` .</span><span class="sxs-lookup"><span data-stu-id="fd94d-1103">Each expression can be either a field name or a call to the `geo.distance()` function.</span></span> <span data-ttu-id="fd94d-1104">Chaque expression peut être suivie par `asc` pour indiquer l'ordre croissant, et par `desc` pour indiquer l'ordre décroissant.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1104">Each expression can be followed by `asc` to indicated ascending, and `desc` to indicate descending.</span></span> <span data-ttu-id="fd94d-1105">La valeur par défaut est l'ordre croissant.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1105">The default is ascending order.</span></span> <span data-ttu-id="fd94d-1106">Il existe une limite de 32 clauses pour `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1106">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="fd94d-1107">Pendant l’appel de **Suggestions** à l’aide de POST, ce paramètre est nommé `orderby` au lieu de `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1107">When calling **Suggestions** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="fd94d-1108">`$select=[string]` (facultatif) : liste de champs séparés par des virgules à récupérer.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1108">`$select=[string]` (optional) - a list of comma-separated fields to retrieve.</span></span> <span data-ttu-id="fd94d-1109">Si aucune valeur n’est spécifiée, seuls la clé du document et le texte de suggestion sont retournés.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1109">If unspecified, only the document key and suggestion text is returned.</span></span> <span data-ttu-id="fd94d-1110">Vous pouvez demander explicitement tous les champs en définissant ce paramètre avec la valeur `*`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1110">You can explicitly request all fields by setting this parameter to `*`.</span></span>

> [!NOTE]
> <span data-ttu-id="fd94d-1111">Pendant l’appel de **Suggestions** à l’aide de POST, ce paramètre est nommé `select` au lieu de `$select`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1111">When calling **Suggestions** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="fd94d-1112">`minimumCoverage` (facultatif, valeur par défaut 80) : nombre compris entre 0 et 100 indiquant le pourcentage de l’index qui doit être couvert par une requête de suggestions afin que la requête soit déclarée comme un succès.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1112">`minimumCoverage` (optional, defaults to 80) - a number between 0 and 100 indicating the percentage of the index that must be covered by a suggestions query in order for the query to be reported as a success.</span></span> <span data-ttu-id="fd94d-1113">Par défaut, au moins 80 % de l’index doit être disponible ou `Suggest` retourne le code d’état HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1113">By default, at least 80% of the index must be available or `Suggest` will return HTTP status code 503.</span></span> <span data-ttu-id="fd94d-1114">Si vous définissez `minimumCoverage` et que `Suggest` réussit, le code HTTP 200 est retourné et inclut une valeur `@search.coverage` dans la réponse indiquant le pourcentage de l’index inclus dans la requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1114">If you set `minimumCoverage` and `Suggest` succeeds, it will return HTTP 200 and include a `@search.coverage` value in the response indicating the percentage of the index that was included in the query.</span></span>

> [!NOTE]
> <span data-ttu-id="fd94d-1115">La définition de ce paramètre à une valeur inférieure à 100 peut être utile pour garantir la disponibilité de la recherche même pour les services ayant un seul réplica.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1115">Setting this parameter to a value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="fd94d-1116">Cependant, il n’y a pas de garantie que toutes les suggestions correspondantes seront présentes dans les résultats.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1116">However, not all matching suggestions are guaranteed to be present in the results.</span></span> <span data-ttu-id="fd94d-1117">Si le rappel est plus important pour votre application que la disponibilité, il est préférable de ne pas baisser `minimumCoverage` en-dessous de sa valeur par défaut 80.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1117">If recall is more important to your application than availability, then it's best not to lower `minimumCoverage` below its default value of 80.</span></span>
> 
> 

<span data-ttu-id="fd94d-1118">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="fd94d-1118">`api-version=[string]` (required).</span></span> <span data-ttu-id="fd94d-1119">La version préliminaire est `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1119">The preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="fd94d-1120">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-1120">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="fd94d-1121">Remarque : pour cette opération, la `api-version` est spécifiée comme paramètre de requête dans l’URL, que vous appeliez **Suggestions** à l’aide de POST ou de GET.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1121">Note: For this operation, the `api-version` is specified as a query parameter in the URL regardless of whether you call **Suggestions** with GET or POST.</span></span>

<span data-ttu-id="fd94d-1122">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-1122">**Request Headers**</span></span>

<span data-ttu-id="fd94d-1123">La liste suivante décrit les en-têtes de requête obligatoires et facultatifs</span><span class="sxs-lookup"><span data-stu-id="fd94d-1123">The following list describes the required and optional request headers</span></span>

* <span data-ttu-id="fd94d-1124">`api-key` : l'en-tête `api-key` est utilisé pour authentifier la requête auprès de votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1124">`api-key`: The `api-key` is used to authenticate the request to your Search service.</span></span> <span data-ttu-id="fd94d-1125">Il s'agit d'une valeur de chaîne, unique pour l'URL de votre service.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1125">It is a string value, unique to your service URL.</span></span> <span data-ttu-id="fd94d-1126">La requête **Suggestions** peut spécifier une clé d’administration ou une clé de requête pour `api-key`.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1126">The **Suggestions** request can specify either an admin key or query key as the `api-key`.</span></span>

<span data-ttu-id="fd94d-1127">Vous avez également besoin du nom du service pour construire l'URL de la requête.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1127">You will also need the service name to construct the request URL.</span></span> <span data-ttu-id="fd94d-1128">Vous pouvez obtenir le nom du service et l'en-tête `api-key` à partir de votre tableau de bord de service dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1128">You can get the service name and `api-key` from your service dashboard in the Azure Portal.</span></span> <span data-ttu-id="fd94d-1129">Pour obtenir de l'aide sur la navigation dans les pages, consultez [Création d'un service Azure Search dans le portail](search-create-service-portal.md) .</span><span class="sxs-lookup"><span data-stu-id="fd94d-1129">See [Create an Azure Search service in the portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="fd94d-1130">**Corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="fd94d-1130">**Request Body**</span></span>

<span data-ttu-id="fd94d-1131">Pour GET : aucun.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1131">For GET: None.</span></span>

<span data-ttu-id="fd94d-1132">Pour POST :</span><span class="sxs-lookup"><span data-stu-id="fd94d-1132">For POST:</span></span>

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered to declare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

<span data-ttu-id="fd94d-1133">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="fd94d-1133">**Response**</span></span>

<span data-ttu-id="fd94d-1134">Code d'état : 200 OK est retourné pour une réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="fd94d-1134">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

<span data-ttu-id="fd94d-1135">Si l'option de projection est utilisée pour récupérer des champs, ils sont inclus dans chaque élément du tableau :</span><span class="sxs-lookup"><span data-stu-id="fd94d-1135">If the projection option is used to retrieve fields they are included in each element of the array:</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in the query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

<span data-ttu-id="fd94d-1136">**Exemple**</span><span class="sxs-lookup"><span data-stu-id="fd94d-1136">**Example**</span></span>

<span data-ttu-id="fd94d-1137">Récupérer 5 suggestions pour lesquelles l'entrée de recherche partielle est « lux »</span><span class="sxs-lookup"><span data-stu-id="fd94d-1137">Retrieve 5 suggestions where the partial search input is 'lux'</span></span>

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
