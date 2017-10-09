---
title: aaaAzure Search Service REST API Version 2015-02-28-Preview | Documents Microsoft
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
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a><span data-ttu-id="3fffd-103">API REST du service Azure Search : version 2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3fffd-103">Azure Search Service REST API: Version 2015-02-28-Preview</span></span>
<span data-ttu-id="3fffd-104">Cet article est la documentation de référence hello pour `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-104">This article is hello reference documentation for `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3fffd-105">Cette version préliminaire étend la version actuelle disponible de manière générale la hello, [api-version = 2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), en fournissant hello suivant les fonctionnalités expérimentales :</span><span class="sxs-lookup"><span data-stu-id="3fffd-105">This preview extends hello current generally available version, [api-version=2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), by providing hello following experimental features:</span></span>

* <span data-ttu-id="3fffd-106">`moreLikeThis`paramètre hello requête [recherche de Documents](#SearchDocs) API.</span><span class="sxs-lookup"><span data-stu-id="3fffd-106">`moreLikeThis` query parameter in hello [Search Documents](#SearchDocs) API.</span></span> <span data-ttu-id="3fffd-107">Il recherche d’autres documents qui sont pertinentes tooanother des documents spécifiques.</span><span class="sxs-lookup"><span data-stu-id="3fffd-107">It finds other documents that are relevant tooanother specific document.</span></span>

<span data-ttu-id="3fffd-108">Quelques éléments supplémentaires de hello `2015-02-28-Preview` API REST sont documentées séparément.</span><span class="sxs-lookup"><span data-stu-id="3fffd-108">A few additional parts of hello `2015-02-28-Preview` REST API are documented separately.</span></span> <span data-ttu-id="3fffd-109">Vous avez notamment vu les points suivants :</span><span class="sxs-lookup"><span data-stu-id="3fffd-109">These include:</span></span>

* [<span data-ttu-id="3fffd-110">Profils de calcul de score</span><span class="sxs-lookup"><span data-stu-id="3fffd-110">Scoring Profiles</span></span>](search-api-scoring-profiles-2015-02-28-preview.md)
* [<span data-ttu-id="3fffd-111">Indexeurs</span><span class="sxs-lookup"><span data-stu-id="3fffd-111">Indexers</span></span>](search-api-indexers-2015-02-28-preview.md)

<span data-ttu-id="3fffd-112">Le service Azure Search est disponible dans plusieurs versions.</span><span class="sxs-lookup"><span data-stu-id="3fffd-112">Azure Search service is available in multiple versions.</span></span> <span data-ttu-id="3fffd-113">Reportez-vous trop[recherche Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="3fffd-113">Please refer too[Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details.</span></span>

## <a name="apis-in-this-document"></a><span data-ttu-id="3fffd-114">API dans ce document</span><span class="sxs-lookup"><span data-stu-id="3fffd-114">APIs in this document</span></span>
<span data-ttu-id="3fffd-115">L’API du service Azure Search prend en charge deux syntaxes d’URL pour les opérations d’API : simple et OData. Pour plus d’informations, consultez [Prise en charge d’OData (API Azure Search)](http://msdn.microsoft.com/library/azure/dn798932.aspx).</span><span class="sxs-lookup"><span data-stu-id="3fffd-115">Azure Search service API supports two URL syntaxes for API operations: simple and OData (see [Support for OData (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798932.aspx) for details).</span></span> <span data-ttu-id="3fffd-116">Hello liste suivante présente une syntaxe simple hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-116">hello following list shows hello simple syntax.</span></span>

[<span data-ttu-id="3fffd-117">Création d'index</span><span class="sxs-lookup"><span data-stu-id="3fffd-117">Create Index</span></span>](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="3fffd-118">Mise à jour d'index</span><span class="sxs-lookup"><span data-stu-id="3fffd-118">Update Index</span></span>](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="3fffd-119">Obtention d'index</span><span class="sxs-lookup"><span data-stu-id="3fffd-119">Get Index</span></span>](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="3fffd-120">Liste des index</span><span class="sxs-lookup"><span data-stu-id="3fffd-120">Listing Indexes</span></span>](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[<span data-ttu-id="3fffd-121">Obtention de statistiques d'index</span><span class="sxs-lookup"><span data-stu-id="3fffd-121">Get Index Statistics</span></span>](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[<span data-ttu-id="3fffd-122">Tester l’analyseur</span><span class="sxs-lookup"><span data-stu-id="3fffd-122">Test Analyzer</span></span>](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[<span data-ttu-id="3fffd-123">Suppression d'index</span><span class="sxs-lookup"><span data-stu-id="3fffd-123">Delete an Index</span></span>](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[<span data-ttu-id="3fffd-124">Ajout, suppression et mise à jour de données dans un index</span><span class="sxs-lookup"><span data-stu-id="3fffd-124">Add, Delete, and Update Data within an Index</span></span>](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[<span data-ttu-id="3fffd-125">Recherche dans des documents</span><span class="sxs-lookup"><span data-stu-id="3fffd-125">Search Documents</span></span>](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[<span data-ttu-id="3fffd-126">Recherche de document</span><span class="sxs-lookup"><span data-stu-id="3fffd-126">Lookup Document</span></span>](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[<span data-ttu-id="3fffd-127">Nombre de documents</span><span class="sxs-lookup"><span data-stu-id="3fffd-127">Count Documents</span></span>](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[<span data-ttu-id="3fffd-128">Suggestions</span><span class="sxs-lookup"><span data-stu-id="3fffd-128">Suggestions</span></span>](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a><span data-ttu-id="3fffd-129">Opérations d'index</span><span class="sxs-lookup"><span data-stu-id="3fffd-129">Index Operations</span></span>
<span data-ttu-id="3fffd-130">Vous pouvez créer et gérer des index dans le service Azure Search via de simples requêtes HTTP (POST, GET, PUT, DELETE) sur une ressource d'index donnée.</span><span class="sxs-lookup"><span data-stu-id="3fffd-130">You can create and manage indexes in Azure Search service via simple HTTP requests (POST, GET, PUT, DELETE) against a given index resource.</span></span> <span data-ttu-id="3fffd-131">toocreate un index, vous commencez par publier un document JSON qui décrit le schéma d’index hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-131">toocreate an index, you first POST a JSON document that describes hello index schema.</span></span> <span data-ttu-id="3fffd-132">schéma de Hello définit les champs de hello de hello index, leurs types de données, et comment elles peuvent être utilisées (par exemple, dans les recherches en texte intégral, filtres, de tri ou des facettes).</span><span class="sxs-lookup"><span data-stu-id="3fffd-132">hello schema defines hello fields of hello index, their data types, and how they can be used (for example, in full-text searches, filters, sorting, or faceting).</span></span> <span data-ttu-id="3fffd-133">Il définit également des profils de calcul de score, générateurs de suggestions et d’autres comportements de hello tooconfigure attributs d’index de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-133">It also defines scoring profiles, suggesters and other attributes tooconfigure hello behavior of hello index.</span></span>

<span data-ttu-id="3fffd-134">Hello exemple suivant fournit une illustration d’un schéma utilisé pour la recherche sur les informations d’hôtel avec le champ de Description hello défini dans deux langues.</span><span class="sxs-lookup"><span data-stu-id="3fffd-134">hello following example provides an illustration of a schema used for searching on hotel information with hello Description field defined in two languages.</span></span> <span data-ttu-id="3fffd-135">Notez comment les attributs contrôlent comment le champ de hello est utilisée.</span><span class="sxs-lookup"><span data-stu-id="3fffd-135">Notice how attributes control how hello field is used.</span></span> <span data-ttu-id="3fffd-136">Par exemple hello `hotelId` est utilisé comme clé de document hello (`"key": true`) et est exclu des recherches en texte intégral (`"searchable": false`).</span><span class="sxs-lookup"><span data-stu-id="3fffd-136">For example hello `hotelId` is used as hello document key (`"key": true`) and is excluded from full-text searches (`"searchable": false`).</span></span>

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

<span data-ttu-id="3fffd-137">Après la création d’index de hello, vous allez télécharger des documents qui remplissent les index hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-137">After hello index is created, you'll upload documents that populate hello index.</span></span> <span data-ttu-id="3fffd-138">Pour cette étape, consultez [Ajout ou mise à jour de documents](#AddOrUpdateDocuments) .</span><span class="sxs-lookup"><span data-stu-id="3fffd-138">See [Add or Update Documents](#AddOrUpdateDocuments) for this next step.</span></span>

<span data-ttu-id="3fffd-139">Pour une vidéo de présentation tooindexing dans Azure Search, consultez hello [épisode de Channel 9 Cloud Cover sur Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span><span class="sxs-lookup"><span data-stu-id="3fffd-139">For a video introduction tooindexing in Azure Search, see hello [Channel 9 Cloud Cover episode on Azure Search](http://go.microsoft.com/fwlink/p/?LinkId=511509).</span></span>

<a name="CreateIndex"></a>

## <a name="create-index"></a><span data-ttu-id="3fffd-140">Création d'index</span><span class="sxs-lookup"><span data-stu-id="3fffd-140">Create Index</span></span>
<span data-ttu-id="3fffd-141">Un index est le moyen principal de hello d’organisation et de recherche de documents dans Azure Search, toohow comme une table organise les enregistrements dans une base de données.</span><span class="sxs-lookup"><span data-stu-id="3fffd-141">An index is hello primary means of organizing and searching documents in Azure Search, similar toohow a table organizes records in a database.</span></span> <span data-ttu-id="3fffd-142">Chaque index a un ensemble de documents que tout est conforme toohello schéma d’index (noms de champs, types de données et propriétés), mais spécifie également des constructions supplémentaires (générateurs de suggestions, profils de calcul de score et les options CORS) qui définissent d’autres comportements de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-142">Each index has a collection of documents that all conform toohello index schema (field names, data types, and properties), but indexes also specify additional constructs (suggesters, scoring profiles, and CORS options) that define other search behaviors.</span></span>

<span data-ttu-id="3fffd-143">Vous pouvez créer un index dans un service Azure Search à l'aide d'une requête HTTP POST ou PUT.</span><span class="sxs-lookup"><span data-stu-id="3fffd-143">You can create a new index within an Azure Search service using an HTTP POST or PUT request.</span></span> <span data-ttu-id="3fffd-144">corps de Hello de demande de hello est un schéma JSON qui spécifie les informations d’index et la configuration hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-144">hello body of hello request is a JSON schema that specifies hello index and configuration information.</span></span>

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="3fffd-145">Vous pouvez également utiliser une requête PUT et spécifiez le nom de l’index hello sur hello URI.</span><span class="sxs-lookup"><span data-stu-id="3fffd-145">Alternatively, you can use PUT and specify hello index name on hello URI.</span></span> <span data-ttu-id="3fffd-146">Si les index hello n’existe pas, il sera créé.</span><span class="sxs-lookup"><span data-stu-id="3fffd-146">If hello index does not exist, it will be created.</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

<span data-ttu-id="3fffd-147">Création d’un index détermine la structure hello de hello documents stockés et utilisés dans les opérations de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-147">Creating an index determines hello structure of hello documents stored and used in search operations.</span></span> <span data-ttu-id="3fffd-148">Index de remplissage hello est une opération distincte.</span><span class="sxs-lookup"><span data-stu-id="3fffd-148">Populating hello index is a separate operation.</span></span> <span data-ttu-id="3fffd-149">Pour cette étape, vous pouvez utiliser un [indexeur](https://msdn.microsoft.com/library/azure/mt183328.aspx) (disponible pour les sources de données prises en charge) ou une opération [Ajout, mise à jour ou suppression de documents](https://msdn.microsoft.com/library/azure/dn798930.aspx).</span><span class="sxs-lookup"><span data-stu-id="3fffd-149">For this step, you can use an [indexer](https://msdn.microsoft.com/library/azure/mt183328.aspx) (available for supported data sources) or an [Add, Update, or Delete Documents](https://msdn.microsoft.com/library/azure/dn798930.aspx) operation.</span></span> <span data-ttu-id="3fffd-150">index de Hello inversé est généré lors de la validation des documents de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-150">hello inverted index is generated when hello documents are posted.</span></span>

<span data-ttu-id="3fffd-151">**Remarque**: nombre maximal de hello d’index autorisé varie selon le niveau de tarification.</span><span class="sxs-lookup"><span data-stu-id="3fffd-151">**Note**: hello maximum number of indexes allowed varies by pricing tier.</span></span> <span data-ttu-id="3fffd-152">service gratuit de Hello permet des index de too3.</span><span class="sxs-lookup"><span data-stu-id="3fffd-152">hello free service allows up too3 indexes.</span></span> <span data-ttu-id="3fffd-153">Le service standard autorise 50 index par service de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-153">Standard service allows 50 indexes per Search service.</span></span> <span data-ttu-id="3fffd-154">Pour plus d'informations, consultez [Limites et contraintes](http://msdn.microsoft.com/library/azure/dn798934.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3fffd-154">See [Limits and constraints](http://msdn.microsoft.com/library/azure/dn798934.aspx) for details.</span></span>

<span data-ttu-id="3fffd-155">**Requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-155">**Request**</span></span>

<span data-ttu-id="3fffd-156">Le protocole HTTPS est requis pour toutes les requêtes de service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-156">HTTPS is required for all service requests.</span></span> <span data-ttu-id="3fffd-157">Hello **Create Index** demande peut être construite à l’aide d’une méthode POST ou PUT.</span><span class="sxs-lookup"><span data-stu-id="3fffd-157">hello **Create Index** request can be constructed using either a POST or PUT method.</span></span> <span data-ttu-id="3fffd-158">Lors de l’utilisation de POST, vous devez fournir un nom d’index dans le corps de la demande, ainsi que la définition de schéma d’index hello hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-158">When using POST, you must provide an index name in hello request body along with hello index schema definition.</span></span> <span data-ttu-id="3fffd-159">Avec PUT, nom de l’index hello fait partie de l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-159">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="3fffd-160">Si les index hello n’existe pas, il est créé.</span><span class="sxs-lookup"><span data-stu-id="3fffd-160">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="3fffd-161">S’il existe déjà, il est mis à jour toohello nouvelle définition.</span><span class="sxs-lookup"><span data-stu-id="3fffd-161">If it already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="3fffd-162">Hello nom d’index doit être en minuscules, commencer par une lettre ou un chiffre, contenir sans barres obliques ni points et être inférieure à 128 caractères.</span><span class="sxs-lookup"><span data-stu-id="3fffd-162">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="3fffd-163">Après avoir démarré le nom de l’index hello par une lettre ou un chiffre, reste hello du nom de hello peut inclure toute lettre, le numéro et des tirets, tant que les tirets hello ne soient pas contigus.</span><span class="sxs-lookup"><span data-stu-id="3fffd-163">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="3fffd-164">Hello `api-version` est requis.</span><span class="sxs-lookup"><span data-stu-id="3fffd-164">hello `api-version` is required.</span></span> <span data-ttu-id="3fffd-165">Pour obtenir la liste des versions disponibles, consultez [Contrôle de version du service Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3fffd-165">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for a list of available versions.</span></span>

<span data-ttu-id="3fffd-166">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-166">**Request Headers**</span></span>

<span data-ttu-id="3fffd-167">Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.</span><span class="sxs-lookup"><span data-stu-id="3fffd-167">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3fffd-168">`Content-Type`: requis.</span><span class="sxs-lookup"><span data-stu-id="3fffd-168">`Content-Type`: Required.</span></span> <span data-ttu-id="3fffd-169">Définissez cette propriété trop`application/json`</span><span class="sxs-lookup"><span data-stu-id="3fffd-169">Set this too`application/json`</span></span>
* <span data-ttu-id="3fffd-170">`api-key`: obligatoire.</span><span class="sxs-lookup"><span data-stu-id="3fffd-170">`api-key`: Required.</span></span> <span data-ttu-id="3fffd-171">Hello `api-key` est utilisé pour</span><span class="sxs-lookup"><span data-stu-id="3fffd-171">hello `api-key` is used to</span></span>
* <span data-ttu-id="3fffd-172">authentifier le service de recherche tooyour hello demande.</span><span class="sxs-lookup"><span data-stu-id="3fffd-172">authenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3fffd-173">Il s’agit d’une valeur de chaîne, d’un service de tooyour unique.</span><span class="sxs-lookup"><span data-stu-id="3fffd-173">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="3fffd-174">Hello **Create Index** demande doit inclure un `api-key` en-tête défini la clé d’administration tooyour (en tant que clé de requête tooa exécutée).</span><span class="sxs-lookup"><span data-stu-id="3fffd-174">hello **Create Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="3fffd-175">Vous devez également les URL de demande du nom tooconstruct hello hello service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-175">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3fffd-176">Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3fffd-176">You can get both hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3fffd-177">Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.</span><span class="sxs-lookup"><span data-stu-id="3fffd-177">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3fffd-178"><a name="RequestData"></a>
**Syntaxe du corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-178"><a name="RequestData"></a>
**Request Body Syntax**</span></span>

<span data-ttu-id="3fffd-179">corps de Hello de demande de hello contient une définition de schéma, qui inclut la liste hello des champs de données de documents qui alimenteront cet index, les types de données, attributs, ainsi que d’une liste facultative de l’évaluation des profils qui est utilisé tooscore mise en correspondance des documents au heure de la requête.</span><span class="sxs-lookup"><span data-stu-id="3fffd-179">hello body of hello request contains a schema definition, which includes hello list of data fields within documents that will be fed into this index, data types, attributes, as well as an optional list of scoring profiles that are used tooscore matching documents at query time.</span></span>

<span data-ttu-id="3fffd-180">Notez que pour une demande POST, vous devez spécifier nom d’index hello dans le corps de la demande hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-180">Note that for a POST request, you must specify hello index name in hello request body.</span></span>

<span data-ttu-id="3fffd-181">Il peut être uniquement un champ clé dans l’index de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-181">There can only be one key field in hello index.</span></span> <span data-ttu-id="3fffd-182">Il a toobe un champ de chaîne.</span><span class="sxs-lookup"><span data-stu-id="3fffd-182">It has toobe a string field.</span></span> <span data-ttu-id="3fffd-183">Ce champ représente l’identificateur unique de hello pour chaque document stocké dans les index hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-183">This field represents hello unique identifier for each document stored within hello index.</span></span>

<span data-ttu-id="3fffd-184">parties principales Hello un index hello suivants :</span><span class="sxs-lookup"><span data-stu-id="3fffd-184">hello main parts of an index include hello following:</span></span>

* `name`
* <span data-ttu-id="3fffd-185">`fields` qui alimenteront cet index, y compris le nom, le type de données et les propriétés qui définissent les actions autorisées sur ce champ.</span><span class="sxs-lookup"><span data-stu-id="3fffd-185">`fields` that will be fed into this index, including name, data type, and properties that define allowable actions on that field.</span></span>
* <span data-ttu-id="3fffd-186">`suggesters` utilisés pour les requêtes prédictives ou avec saisie semi-automatique.</span><span class="sxs-lookup"><span data-stu-id="3fffd-186">`suggesters` used for auto-complete or type-ahead queries.</span></span>
* <span data-ttu-id="3fffd-187">`scoringProfiles` utilisés pour le classement personnalisé des scores de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-187">`scoringProfiles` used for custom search score ranking.</span></span> <span data-ttu-id="3fffd-188">Pour plus d'informations, consultez [Ajout de profils de calcul de score](https://msdn.microsoft.com/library/azure/dn798928.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3fffd-188">See [Add scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for details.</span></span>
* <span data-ttu-id="3fffd-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` utilisé toodefine comment vos documents/requêtes sont divisées en jetons indexables/de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-189">`analyzers`, `charFilters`, `tokenizers`, `tokenFilters` used toodefine how your documents/queries are broken into indexable/searchable tokens.</span></span> <span data-ttu-id="3fffd-190">Consultez [Analyse dans Azure Search](https://aka.ms//azsanalysis) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="3fffd-190">See [Analysis in Azure Search](https://aka.ms//azsanalysis) for details.</span></span>
* <span data-ttu-id="3fffd-191">`defaultScoringProfile`utilisé par défaut de hello toooverwrite comportements de calcul de score.</span><span class="sxs-lookup"><span data-stu-id="3fffd-191">`defaultScoringProfile` used toooverwrite hello default scoring behaviors.</span></span>
* <span data-ttu-id="3fffd-192">`corsOptions`requêtes de cross-origin tooallow par rapport à votre index.</span><span class="sxs-lookup"><span data-stu-id="3fffd-192">`corsOptions` tooallow cross-origin queries against your index.</span></span>

<span data-ttu-id="3fffd-193">syntaxe Hello pour structurer la charge utile de demande hello est comme suit.</span><span class="sxs-lookup"><span data-stu-id="3fffd-193">hello syntax for structuring hello request payload is as follows.</span></span> <span data-ttu-id="3fffd-194">Vous trouverez un exemple de requête dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="3fffd-194">A sample request is provided further on in this topic.</span></span>

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
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
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
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
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

<span data-ttu-id="3fffd-195">**Attributs d'index**</span><span class="sxs-lookup"><span data-stu-id="3fffd-195">**Index Attributes**</span></span>

<span data-ttu-id="3fffd-196">Hello attributs suivants peuvent être définis lors de la création d’un index.</span><span class="sxs-lookup"><span data-stu-id="3fffd-196">hello following attributes can be set when creating an index.</span></span> <span data-ttu-id="3fffd-197">Pour plus d'informations sur le calcul de score et les profils de calcul de score, consultez [Ajout de profils de calcul de score](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="3fffd-197">For details about scoring and scoring profiles, see [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span>

<span data-ttu-id="3fffd-198">`name`-Jeux hello nom du champ de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-198">`name` - Sets hello name of hello field.</span></span>

<span data-ttu-id="3fffd-199">`type`-Jeux hello le type de données pour le champ de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-199">`type` - Sets hello data type for hello field.</span></span>

<span data-ttu-id="3fffd-200">`searchable`-Marque hello champ de texte intégral en mesure de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-200">`searchable` - Marks hello field as full-text search-able.</span></span> <span data-ttu-id="3fffd-201">Cela signifie qu'il fera l'objet d'une analyse, par exemple lexicale, lors de l'indexation.</span><span class="sxs-lookup"><span data-stu-id="3fffd-201">This means it will undergo analysis such as word-breaking during indexing.</span></span> <span data-ttu-id="3fffd-202">Si vous définissez un `searchable` champ tooa valeur comme « journée ensoleillée », en interne il sera fractionné en jetons individuels de hello « jour » et « ensoleillée ».</span><span class="sxs-lookup"><span data-stu-id="3fffd-202">If you set a `searchable` field tooa value like "sunny day", internally it will be split into hello individual tokens "sunny" and "day".</span></span> <span data-ttu-id="3fffd-203">Cela permet d'effectuer des recherches en texte intégral de ces termes.</span><span class="sxs-lookup"><span data-stu-id="3fffd-203">This enables full-text searches for these terms.</span></span> <span data-ttu-id="3fffd-204">Les champs de type `Edm.String` ou `Collection(Edm.String)` sont `searchable` par défaut.</span><span class="sxs-lookup"><span data-stu-id="3fffd-204">Fields of type `Edm.String` or `Collection(Edm.String)` are `searchable` by default.</span></span> <span data-ttu-id="3fffd-205">Les autres types de champs ne peuvent pas être `searchable`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-205">Fields of other types cannot be `searchable`.</span></span>

* <span data-ttu-id="3fffd-206">**Remarque**: `searchable` champs consomment davantage d’espace dans votre index, car Azure Search stocke une version supplémentaire sous forme de jeton de valeur du champ hello pour les recherches en texte intégral.</span><span class="sxs-lookup"><span data-stu-id="3fffd-206">**Note**: `searchable` fields consume extra space in your index since Azure Search will store an additional tokenized version of hello field value for full-text searches.</span></span> <span data-ttu-id="3fffd-207">Si vous souhaitez toosave espace dans votre index et que vous n’avez pas besoin une toobe champ inclus dans les recherches, définissez `searchable` trop`false`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-207">If you want toosave space in your index and you don't need a field toobe included in searches, set `searchable` too`false`.</span></span>

<span data-ttu-id="3fffd-208">`filterable`-Permet de hello toobe de champ référencé dans `$filter` requêtes.</span><span class="sxs-lookup"><span data-stu-id="3fffd-208">`filterable` - Allows hello field toobe referenced in `$filter` queries.</span></span> <span data-ttu-id="3fffd-209">`filterable` diffère de `searchable` du point de vue du mode de traitement des chaînes.</span><span class="sxs-lookup"><span data-stu-id="3fffd-209">`filterable` differs from `searchable` in how strings are handled.</span></span> <span data-ttu-id="3fffd-210">Les champs de type `Edm.String` ou `Collection(Edm.String)` qui sont `filterable` ne font pas l'objet d'une analyse lexicale, les comparaisons ne concernent donc que les correspondances exactes.</span><span class="sxs-lookup"><span data-stu-id="3fffd-210">Fields of type `Edm.String` or `Collection(Edm.String)` that are `filterable` do not undergo word-breaking, so comparisons are for exact matches only.</span></span> <span data-ttu-id="3fffd-211">Par exemple, si vous définissez un tel champ `f` trop « journée ensoleillée », `$filter=f eq 'sunny'` ne trouve aucune correspondance, mais `$filter=f eq 'sunny day'` sera.</span><span class="sxs-lookup"><span data-stu-id="3fffd-211">For example, if you set such a field `f` too"sunny day", `$filter=f eq 'sunny'` will find no matches, but `$filter=f eq 'sunny day'` will.</span></span> <span data-ttu-id="3fffd-212">Tous les champs sont `filterable` par défaut.</span><span class="sxs-lookup"><span data-stu-id="3fffd-212">All fields are `filterable` by default.</span></span>

<span data-ttu-id="3fffd-213">`sortable`-Par défaut système de hello trie les résultats par score, mais il est souvent les utilisateurs que toosort par les champs dans les documents de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-213">`sortable` - By default hello system sorts results by score, but in many experiences users will want toosort by fields in hello documents.</span></span> <span data-ttu-id="3fffd-214">Les champs de type `Collection(Edm.String)` ne peuvent pas être `sortable`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-214">Fields of type `Collection(Edm.String)` cannot be `sortable`.</span></span> <span data-ttu-id="3fffd-215">Tous les autres champs sont `sortable` par défaut.</span><span class="sxs-lookup"><span data-stu-id="3fffd-215">All other fields are `sortable` by default.</span></span>

<span data-ttu-id="3fffd-216">`facetable`: généralement utilisé dans une présentation des résultats de recherche qui inclut le nombre d'accès par catégorie (par exemple, vous recherchez des appareils photo numériques et regardez le nombre d'accès par marque, mégapixels, prix, etc.).</span><span class="sxs-lookup"><span data-stu-id="3fffd-216">`facetable`- Typically used in a presentation of search results that includes hit count by category (for example, search for digital cameras and see hits by brand, by megapixels, by price, etc.).</span></span> <span data-ttu-id="3fffd-217">Cette option ne peut pas être utilisée avec des champs de type `Edm.GeographyPoint`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-217">This option cannot be used with fields of type `Edm.GeographyPoint`.</span></span> <span data-ttu-id="3fffd-218">Tous les autres champs sont `facetable` par défaut.</span><span class="sxs-lookup"><span data-stu-id="3fffd-218">All other fields are `facetable` by default.</span></span>

* <span data-ttu-id="3fffd-219">**Remarque** : les champs de type `Edm.String` qui sont `filterable`, `sortable` ou `facetable` ne doivent pas dépasser 32 Ko de longueur.</span><span class="sxs-lookup"><span data-stu-id="3fffd-219">**Note**: Fields of type `Edm.String` that are `filterable`, `sortable`, or `facetable` can be at most 32KB in length.</span></span> <span data-ttu-id="3fffd-220">Il s’agit, car ces champs sont traités comme un terme de recherche et la longueur maximale de hello d’un terme dans Azure Search est de 32 Ko.</span><span class="sxs-lookup"><span data-stu-id="3fffd-220">This is because such fields are treated as a single search term, and hello maximum length of a term in Azure Search is 32KB.</span></span> <span data-ttu-id="3fffd-221">Si vous devez toostore davantage de texte dans un champ de chaîne, vous devez tooexplicitly définir `filterable`, `sortable`, et `facetable` trop`false` dans votre définition d’index.</span><span class="sxs-lookup"><span data-stu-id="3fffd-221">If you need toostore more text than this in a single string field, you will need tooexplicitly set `filterable`, `sortable`, and `facetable` too`false` in your index definition.</span></span>
* <span data-ttu-id="3fffd-222">**Remarque**: si un champ n’a aucun Hello ci-dessus attributs définis trop`true` (`searchable`, `filterable`, `sortable`, ou`facetable`) hello champ est effectivement exclu de l’index de hello inversé.</span><span class="sxs-lookup"><span data-stu-id="3fffd-222">**Note**: If a field has none of hello above attributes set too`true` (`searchable`, `filterable`, `sortable`,  or`facetable`) hello field is effectively excluded from hello inverted index.</span></span> <span data-ttu-id="3fffd-223">Cette option est utile pour les champs qui ne sont pas utilisés dans les requêtes, mais qui sont nécessaires dans les résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-223">This option is useful for fields that are not used in queries, but are needed in search results.</span></span> <span data-ttu-id="3fffd-224">À l’exclusion de ces champs à partir de l’index de hello améliore les performances.</span><span class="sxs-lookup"><span data-stu-id="3fffd-224">Excluding such fields from hello index improves performance.</span></span>

<span data-ttu-id="3fffd-225">`key`-Marques hello champ comme contenant des identificateurs uniques pour les documents dans l’index de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-225">`key` - Marks hello field as containing unique identifiers for documents within hello index.</span></span> <span data-ttu-id="3fffd-226">Un seul champ doit être choisi comme hello `key` champ et il doit être de type `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-226">Exactly one field must be chosen as hello `key` field and it must be of type `Edm.String`.</span></span> <span data-ttu-id="3fffd-227">Champs clés peuvent être utilisé toolook des documents directement par le biais de hello [API de recherche](#LookupAPI).</span><span class="sxs-lookup"><span data-stu-id="3fffd-227">Key fields can be used toolook up documents directly via hello [Lookup API](#LookupAPI).</span></span>

<span data-ttu-id="3fffd-228">`retrievable`-Définit si le champ de hello peut être retournée dans un résultat de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-228">`retrievable` - Sets whether hello field can be returned in a search result.</span></span>  <span data-ttu-id="3fffd-229">Cela est utile lorsque vous souhaitez toouse un champ (par exemple, marge) en tant que filtre, de tri ou de mécanisme de calcul de score mais que vous ne voulez pas que des utilisateurs finaux de hello champ toobe toohello visible.</span><span class="sxs-lookup"><span data-stu-id="3fffd-229">This is useful when you want toouse a field (for example, margin) as a filter, sorting, or scoring mechanism but do not want hello field toobe visible toohello end user.</span></span> <span data-ttu-id="3fffd-230">Il doit être `true` for `key` .</span><span class="sxs-lookup"><span data-stu-id="3fffd-230">This attribute must be `true` for `key` fields.</span></span>

<span data-ttu-id="3fffd-231">`analyzer`-Jeux hello nom de hello analyseur toouse hello champ au moment de la recherche au moment de l’indexation.</span><span class="sxs-lookup"><span data-stu-id="3fffd-231">`analyzer` - Sets hello name of hello analyzer toouse for hello field at search time and indexing time.</span></span> <span data-ttu-id="3fffd-232">Pourquoi autorisée du jeu de valeurs, consultez [analyseurs](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="3fffd-232">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="3fffd-233">Cette option ne peut être utilisée qu’avec les champs `searchable` et ne peut être associée à `searchAnalyzer` ou `indexAnalyzer`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-233">This option can be used only with `searchable` fields and it can't be set together with either `searchAnalyzer` or `indexAnalyzer`.</span></span>  <span data-ttu-id="3fffd-234">Une fois que l’Analyseur de hello est choisie, il ne peut pas être modifié pour le champ de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-234">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="3fffd-235">`searchAnalyzer`-Jeux hello nom de l’analyseur hello utilisée au moment de la recherche pour le champ de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-235">`searchAnalyzer` - Sets hello name of hello analyzer used at search time for hello field.</span></span> <span data-ttu-id="3fffd-236">Pourquoi autorisée du jeu de valeurs, consultez [analyseurs](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="3fffd-236">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="3fffd-237">Cette option peut être utilisée uniquement avec les champs `searchable` .</span><span class="sxs-lookup"><span data-stu-id="3fffd-237">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="3fffd-238">Elle doit être définie avec `indexAnalyzer` et ne peut pas être définie avec hello `analyzer` option.</span><span class="sxs-lookup"><span data-stu-id="3fffd-238">It must be set together with `indexAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="3fffd-239">Cet analyseur peut être mis à jour sur un champ existant.</span><span class="sxs-lookup"><span data-stu-id="3fffd-239">This analyzer can be updated on an existing field.</span></span>

<span data-ttu-id="3fffd-240">`indexAnalyzer`-Jeux hello nom de l’analyseur hello utilisée au moment de l’indexation pour le champ de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-240">`indexAnalyzer` - Sets hello name of hello analyzer used at indexing time for hello field.</span></span> <span data-ttu-id="3fffd-241">Pourquoi autorisée du jeu de valeurs, consultez [analyseurs](https://msdn.microsoft.com/library/mt605304.aspx).</span><span class="sxs-lookup"><span data-stu-id="3fffd-241">For hello allowed set of values see [Analyzers](https://msdn.microsoft.com/library/mt605304.aspx).</span></span> <span data-ttu-id="3fffd-242">Cette option peut être utilisée uniquement avec les champs `searchable` .</span><span class="sxs-lookup"><span data-stu-id="3fffd-242">This option can be used only with `searchable` fields.</span></span> <span data-ttu-id="3fffd-243">Elle doit être définie avec `searchAnalyzer` et ne peut pas être définie avec hello `analyzer` option.</span><span class="sxs-lookup"><span data-stu-id="3fffd-243">It must be set together with `searchAnalyzer` and it cannot be set together with hello `analyzer` option.</span></span> <span data-ttu-id="3fffd-244">Une fois que l’Analyseur de hello est choisie, il ne peut pas être modifié pour le champ de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-244">Once hello analyzer is chosen, it cannot be changed for hello field.</span></span>

<span data-ttu-id="3fffd-245">`suggesters`-Jeux hello mode de recherche et les champs qui sont source de hello du contenu hello pour obtenir des suggestions.</span><span class="sxs-lookup"><span data-stu-id="3fffd-245">`suggesters` - Sets hello search mode and fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="3fffd-246">Pour plus d'informations, consultez [Générateurs de suggestions](#Suggesters) .</span><span class="sxs-lookup"><span data-stu-id="3fffd-246">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="3fffd-247">`scoringProfiles` : définit les comportements de calcul de score personnalisés qui vous permettent de choisir les éléments qui s'affichent en haut des résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-247">`scoringProfiles` - Defines custom scoring behaviors that let you influence which items appear higher in search results.</span></span> <span data-ttu-id="3fffd-248">Les profils de calcul de score sont constitués de pondérations et de fonctions de champ.</span><span class="sxs-lookup"><span data-stu-id="3fffd-248">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="3fffd-249">Consultez [ajouter les profils de calcul de score](https://msdn.microsoft.com/library/azure/dn798928.aspx) pour plus d’informations sur les attributs hello utilisés dans un profil de score.</span><span class="sxs-lookup"><span data-stu-id="3fffd-249">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information about hello attributes used in a scoring profile.</span></span>

<span data-ttu-id="3fffd-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Support multilingue**</span><span class="sxs-lookup"><span data-stu-id="3fffd-250"><!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Language support**</span></span>

<span data-ttu-id="3fffd-251">Les champs pouvant faire l'objet d'une recherche subissent une analyse qui implique la plupart du temps une analyse lexicale, la normalisation du texte et le filtrage des termes.</span><span class="sxs-lookup"><span data-stu-id="3fffd-251">Searchable fields undergo analysis that most frequently involves word-breaking, text normalization, and filtering out terms.</span></span> <span data-ttu-id="3fffd-252">Par défaut, les champs interrogeables dans Azure Search sont analysés par hello [analyseur Apache Lucene Standard](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) qui découpe le texte en suivant le[« Unicode Text Segmentation »](http://unicode.org/reports/tr29/) règles.</span><span class="sxs-lookup"><span data-stu-id="3fffd-252">By default, searchable fields in Azure Search are analyzed with hello [Apache Lucene Standard analyzer](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) which breaks text into elements following the["Unicode Text Segmentation"](http://unicode.org/reports/tr29/) rules.</span></span> <span data-ttu-id="3fffd-253">En outre, analyseur standard de hello convertit écran minuscules de tous les caractères tootheir.</span><span class="sxs-lookup"><span data-stu-id="3fffd-253">Additionally, hello standard analyzer converts all characters tootheir lower case form.</span></span> <span data-ttu-id="3fffd-254">Les documents indexés et les termes de recherche accédez par l’analyse de hello durant l’indexation et de traitement des requêtes.</span><span class="sxs-lookup"><span data-stu-id="3fffd-254">Both indexed documents and search terms go through hello analysis during indexing and query processing.</span></span>

<span data-ttu-id="3fffd-255">Azure Search prend en charge l’indexation des champs dans plusieurs langues.</span><span class="sxs-lookup"><span data-stu-id="3fffd-255">Azure Search supports a variety of languages.</span></span> <span data-ttu-id="3fffd-256">Chaque langue requiert un analyseur de texte non standard qui tient compte des caractéristiques d'une langue donnée.</span><span class="sxs-lookup"><span data-stu-id="3fffd-256">Each language requires a non-standard text analyzer which accounts for characteristics of a given language.</span></span> <span data-ttu-id="3fffd-257">Azure Search propose deux types d'analyseurs :</span><span class="sxs-lookup"><span data-stu-id="3fffd-257">Azure Search offers two types of analyzers:</span></span>

* <span data-ttu-id="3fffd-258">35 analyseurs pris en charge par Lucene.</span><span class="sxs-lookup"><span data-stu-id="3fffd-258">35 analyzers backed by Lucene.</span></span>
* <span data-ttu-id="3fffd-259">50 analyseurs pris en charge par la technologie de traitement du langage naturel Microsoft propriétaire utilisée dans Office et Bing.</span><span class="sxs-lookup"><span data-stu-id="3fffd-259">50 analyzers backed by proprietary Microsoft natural language processing technology used in Office and Bing.</span></span>

<span data-ttu-id="3fffd-260">Certains développeurs préfèrent hello solution open source, simple et plus facile de Lucene.</span><span class="sxs-lookup"><span data-stu-id="3fffd-260">Some developers might prefer hello more familiar, simple, open-source solution of Lucene.</span></span> <span data-ttu-id="3fffd-261">Analyseurs Lucene sont plus rapides, mais les analyseurs de Microsoft hello ont fonctionnalités avancées, telles que lemmatisation, word decompounding (dans les langues telles que l’allemand, danois, néerlandais, suédois, norvégien, estonien, terminer, hongrois, slovaque) et reconnaissance d’entité (URL des messages électroniques, des dates, des nombres).</span><span class="sxs-lookup"><span data-stu-id="3fffd-261">Lucene analyzers are faster, but hello Microsoft analyzers have advanced capabilities, such as lemmatization, word decompounding (in languages like German, Danish, Dutch, Swedish, Norwegian, Estonian, Finish, Hungarian, Slovak) and entity recognition (URLs, emails, dates, numbers).</span></span> <span data-ttu-id="3fffd-262">Si possible, vous devez exécuter les comparaisons de deux hello Microsoft et Lucene analyseurs toodecide celui qui est plus adaptée.</span><span class="sxs-lookup"><span data-stu-id="3fffd-262">If possible, you should run comparisons of both hello Microsoft and Lucene analyzers toodecide which one is a better fit.</span></span>

<span data-ttu-id="3fffd-263">***Comparatif***</span><span class="sxs-lookup"><span data-stu-id="3fffd-263">***How they compare***</span></span>

<span data-ttu-id="3fffd-264">Analyseur de Lucene Hello pour l’anglais étend l’analyseur standard de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-264">hello Lucene analyzer for English extends hello standard analyzer.</span></span> <span data-ttu-id="3fffd-265">Il supprime la marque du possessif (le « ’s ») à la fin des mots, applique la recherche de radical conformément à [l’algorithme de recherche de radical de Porter](http://tartarus.org/~martin/PorterStemmer/) et supprime les [mots vides](http://en.wikipedia.org/wiki/Stop_words) de l’anglais.</span><span class="sxs-lookup"><span data-stu-id="3fffd-265">It removes possessives (trailing 's) from words, applies stemming as per [Porter Stemming algorithm](http://tartarus.org/~martin/PorterStemmer/), and removes English [stop words](http://en.wikipedia.org/wiki/Stop_words).</span></span>

<span data-ttu-id="3fffd-266">En comparaison, analyseur de Microsoft hello effectue lemmatisation au lieu de la recherche de radical.</span><span class="sxs-lookup"><span data-stu-id="3fffd-266">In comparison, hello Microsoft analyzer performs lemmatization instead of stemming.</span></span> <span data-ttu-id="3fffd-267">Cela signifie qu’il peut bien mieux gérer des mots infléchis et de formes irrégulières, ce qui donne des résultats de recherche plus pertinents (module espion 7 de [Présentation MVA d’Azure Search](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) pour plus de détails).</span><span class="sxs-lookup"><span data-stu-id="3fffd-267">It means it can handle inflected and irregular word forms much better what results in more relevant search results (watch module 7 of [Azure Search MVA presentation](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) for more details).</span></span>

<span data-ttu-id="3fffd-268">L’indexation avec des analyseurs de Microsoft est en moyenne deux fois toothree plus lentes que leurs équivalents Lucene, en fonction du langage de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-268">Indexing with Microsoft analyzers is on average two toothree times slower than their Lucene equivalents, depending on hello language.</span></span> <span data-ttu-id="3fffd-269">Les performances de recherche ne doivent pas être trop affectées pour les requêtes de taille moyenne.</span><span class="sxs-lookup"><span data-stu-id="3fffd-269">Search performance should not be significantly affected for average size queries.</span></span>

<span data-ttu-id="3fffd-270">***Configuration***</span><span class="sxs-lookup"><span data-stu-id="3fffd-270">***Configuration***</span></span>

<span data-ttu-id="3fffd-271">Pour chaque champ dans la définition de l’index hello, vous pouvez définir hello `analyzer` nom de l’analyseur tooan propriété qui spécifie la langue et le fournisseur.</span><span class="sxs-lookup"><span data-stu-id="3fffd-271">For each field in hello index definition, you can set hello `analyzer` property tooan analyzer name that specifies which language and vendor.</span></span> <span data-ttu-id="3fffd-272">Hello analyseur même sera appliqué lors de l’indexation et de recherche pour ce champ.</span><span class="sxs-lookup"><span data-stu-id="3fffd-272">hello same analyzer will be applied when indexing and searching for that field.</span></span>
<span data-ttu-id="3fffd-273">Par exemple, vous pouvez avoir des champs distincts pour des descriptions d’hôtel anglais, espagnol et Français qui existent côte à côte dans hello même index.</span><span class="sxs-lookup"><span data-stu-id="3fffd-273">For example, you can have separate fields for English, French, and Spanish hotel descriptions that exist side-by-side in hello same index.</span></span> <span data-ttu-id="3fffd-274">Hello d’utilisation ['searchFields' paramètre de requête](#SearchQueryParameters) toospecify le toosearch spécifiques au langage champ contre dans vos requêtes.</span><span class="sxs-lookup"><span data-stu-id="3fffd-274">Use hello ['searchFields' query parameter](#SearchQueryParameters) toospecify which language-specific field toosearch against in your queries.</span></span> <span data-ttu-id="3fffd-275">Vous pouvez consulter des exemples de requêtes qui incluent hello `analyzer` propriété dans [recherche de Documents](#SearchDocs).</span><span class="sxs-lookup"><span data-stu-id="3fffd-275">You can review query examples that include hello `analyzer` property in [Search Documents](#SearchDocs).</span></span> 

<span data-ttu-id="3fffd-276">***Liste d’analyseurs***</span><span class="sxs-lookup"><span data-stu-id="3fffd-276">***Analyzer list***</span></span>

<span data-ttu-id="3fffd-277">Vous trouverez ci-dessous la liste de hello des langues prises en charge avec les noms d’analyseur Lucene et Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3fffd-277">Below is hello list of supported languages together with Lucene and Microsoft analyzer names.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="3fffd-278">language</span><span class="sxs-lookup"><span data-stu-id="3fffd-278">Language</span></span></th>
        <th><span data-ttu-id="3fffd-279">Nom de l’analyseur Microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-279">Microsoft analyzer name</span></span></th>
        <th><span data-ttu-id="3fffd-280">Nom de l’analyseur Lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-280">Lucene analyzer name</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-281">Arabe</span><span class="sxs-lookup"><span data-stu-id="3fffd-281">Arabic</span></span></td>
        <td><span data-ttu-id="3fffd-282">ar.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-282">ar.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-283">ar.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-283">ar.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-284">Arménien</span><span class="sxs-lookup"><span data-stu-id="3fffd-284">Armenian</span></span></td>
        <td></td>
        <td><span data-ttu-id="3fffd-285">hy.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-285">hy.lucene</span></span></td>
      </tr>
    <tr>
        <td><span data-ttu-id="3fffd-286">Bangla</span><span class="sxs-lookup"><span data-stu-id="3fffd-286">Bangla</span></span></td>
        <td><span data-ttu-id="3fffd-287">bn.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-287">bn.microsoft</span></span></td>
        <td></td>
    </tr>
      <tr>
        <td><span data-ttu-id="3fffd-288">Basque</span><span class="sxs-lookup"><span data-stu-id="3fffd-288">Basque</span></span></td>
        <td></td>
        <td><span data-ttu-id="3fffd-289">eu.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-289">eu.lucene</span></span></td>
    </tr>
      <tr>
         <td><span data-ttu-id="3fffd-290">Bulgare</span><span class="sxs-lookup"><span data-stu-id="3fffd-290">Bulgarian</span></span></td>
        <td><span data-ttu-id="3fffd-291">bg.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-291">bg.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-292">bg.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-292">bg.lucene</span></span></td>
      </tr>
      <tr>
        <td><span data-ttu-id="3fffd-293">Catalan</span><span class="sxs-lookup"><span data-stu-id="3fffd-293">Catalan</span></span></td>
        <td><span data-ttu-id="3fffd-294">ca.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-294">ca.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-295">ca.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-295">ca.lucene</span></span></td>          
      </tr>
    <tr>
        <td><span data-ttu-id="3fffd-296">Chinois simplifié</span><span class="sxs-lookup"><span data-stu-id="3fffd-296">Chinese Simplified</span></span></td>
        <td><span data-ttu-id="3fffd-297">zh-Hans.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-297">zh-Hans.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-298">zh-Hans.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-298">zh-Hans.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-299">Chinois traditionnel</span><span class="sxs-lookup"><span data-stu-id="3fffd-299">Chinese Traditional</span></span></td>
        <td><span data-ttu-id="3fffd-300">zh-Hant.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-300">zh-Hant.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-301">zh-Hant.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-301">zh-Hant.lucene</span></span></td>        
    <tr>
    <tr>
        <td><span data-ttu-id="3fffd-302">Croate</span><span class="sxs-lookup"><span data-stu-id="3fffd-302">Croatian</span></span></td>
        <td><span data-ttu-id="3fffd-303">hr.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-303">hr.microsoft</span></span></td>
        <td/></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-304">Tchèque</span><span class="sxs-lookup"><span data-stu-id="3fffd-304">Czech</span></span></td>
        <td><span data-ttu-id="3fffd-305">cs.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-305">cs.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-306">cs.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-306">cs.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="3fffd-307">Danois</span><span class="sxs-lookup"><span data-stu-id="3fffd-307">Danish</span></span></td>
        <td><span data-ttu-id="3fffd-308">da.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-308">da.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-309">da.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-309">da.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="3fffd-310">Néerlandais</span><span class="sxs-lookup"><span data-stu-id="3fffd-310">Dutch</span></span></td>
        <td><span data-ttu-id="3fffd-311">nl.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-311">nl.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-312">nl.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-312">nl.lucene</span></span></td>    
    </tr>    
    <tr>
        <td><span data-ttu-id="3fffd-313">Français</span><span class="sxs-lookup"><span data-stu-id="3fffd-313">English</span></span></td>        
        <td><span data-ttu-id="3fffd-314">en.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-314">en.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-315">en.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-315">en.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-316">Estonien</span><span class="sxs-lookup"><span data-stu-id="3fffd-316">Estonian</span></span></td>
        <td><span data-ttu-id="3fffd-317">et.Microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-317">et.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-318">Finnois</span><span class="sxs-lookup"><span data-stu-id="3fffd-318">Finnish</span></span></td>
        <td><span data-ttu-id="3fffd-319">fi.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-319">fi.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-320">fi.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-320">fi.lucene</span></span></td>        
    </tr>    
    <tr>
        <td><span data-ttu-id="3fffd-321">Français</span><span class="sxs-lookup"><span data-stu-id="3fffd-321">French</span></span></td>
        <td><span data-ttu-id="3fffd-322">fr.Microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-322">fr.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-323">fr.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-323">fr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-324">Galicien</span><span class="sxs-lookup"><span data-stu-id="3fffd-324">Galician</span></span></td>
        <td></td>
        <td><span data-ttu-id="3fffd-325">gl.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-325">gl.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="3fffd-326">Allemand</span><span class="sxs-lookup"><span data-stu-id="3fffd-326">German</span></span></td>
        <td><span data-ttu-id="3fffd-327">de.Microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-327">de.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-328">de.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-328">de.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-329">Grec</span><span class="sxs-lookup"><span data-stu-id="3fffd-329">Greek</span></span></td>
        <td><span data-ttu-id="3fffd-330">el.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-330">el.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-331">el.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-331">el.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-332">Goudjrati</span><span class="sxs-lookup"><span data-stu-id="3fffd-332">Gujarati</span></span></td>
        <td><span data-ttu-id="3fffd-333">gu.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-333">gu.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-334">Hébreu</span><span class="sxs-lookup"><span data-stu-id="3fffd-334">Hebrew</span></span></td>
        <td><span data-ttu-id="3fffd-335">he.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-335">he.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-336">Hindi</span><span class="sxs-lookup"><span data-stu-id="3fffd-336">Hindi</span></span></td>
        <td><span data-ttu-id="3fffd-337">hi.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-337">hi.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-338">hi.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-338">hi.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-339">Hongrois</span><span class="sxs-lookup"><span data-stu-id="3fffd-339">Hungarian</span></span></td>        
        <td><span data-ttu-id="3fffd-340">hu.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-340">hu.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-341">hu.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-341">hu.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-342">Islandais</span><span class="sxs-lookup"><span data-stu-id="3fffd-342">Icelandic</span></span></td>
        <td><span data-ttu-id="3fffd-343">is.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-343">is.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-344">Indonésien</span><span class="sxs-lookup"><span data-stu-id="3fffd-344">Indonesian (Bahasa)</span></span></td>
        <td><span data-ttu-id="3fffd-345">id.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-345">id.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-346">id.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-346">id.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-347">Irlandais</span><span class="sxs-lookup"><span data-stu-id="3fffd-347">Irish</span></span></td>
        <td></td>
          <td><span data-ttu-id="3fffd-348">ga.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-348">ga.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-349">Italien</span><span class="sxs-lookup"><span data-stu-id="3fffd-349">Italian</span></span></td>
        <td><span data-ttu-id="3fffd-350">it.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-350">it.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-351">it.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-351">it.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-352">Japonais</span><span class="sxs-lookup"><span data-stu-id="3fffd-352">Japanese</span></span></td>
        <td><span data-ttu-id="3fffd-353">ja.Microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-353">ja.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-354">ja.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-354">ja.lucene</span></span></td>

    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-355">Kannada</span><span class="sxs-lookup"><span data-stu-id="3fffd-355">Kannada</span></span></td>
        <td><span data-ttu-id="3fffd-356">ka.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-356">ka.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-357">Coréen</span><span class="sxs-lookup"><span data-stu-id="3fffd-357">Korean</span></span></td>
        <td><span data-ttu-id="3fffd-358">ko.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-358">ko.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-359">ko.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-359">ko.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-360">Letton</span><span class="sxs-lookup"><span data-stu-id="3fffd-360">Latvian</span></span></td>        
        <td><span data-ttu-id="3fffd-361">lv.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-361">lv.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-362">lv.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-362">lv.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-363">Lituanien</span><span class="sxs-lookup"><span data-stu-id="3fffd-363">Lithuanian</span></span></td>
        <td><span data-ttu-id="3fffd-364">lt.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-364">lt.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-365">Malayalam</span><span class="sxs-lookup"><span data-stu-id="3fffd-365">Malayalam</span></span></td>
        <td><span data-ttu-id="3fffd-366">ml.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-366">ml.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-367">Malais (latin)</span><span class="sxs-lookup"><span data-stu-id="3fffd-367">Malay (Latin)</span></span></td>
        <td><span data-ttu-id="3fffd-368">ms.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-368">ms.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-369">Marathi</span><span class="sxs-lookup"><span data-stu-id="3fffd-369">Marathi</span></span></td>
        <td><span data-ttu-id="3fffd-370">mr.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-370">mr.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-371">Norvégien</span><span class="sxs-lookup"><span data-stu-id="3fffd-371">Norwegian</span></span></td>
        <td><span data-ttu-id="3fffd-372">nb.Microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-372">nb.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-373">no.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-373">no.lucene</span></span></td>        
    </tr>
      <tr>
        <td><span data-ttu-id="3fffd-374">Persan</span><span class="sxs-lookup"><span data-stu-id="3fffd-374">Persian</span></span></td>
        <td></td>
        <td><span data-ttu-id="3fffd-375">fa.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-375">fa.lucene</span></span></td>        
      </tr>
    <tr>
        <td><span data-ttu-id="3fffd-376">Polonais</span><span class="sxs-lookup"><span data-stu-id="3fffd-376">Polish</span></span></td>
        <td><span data-ttu-id="3fffd-377">pl.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-377">pl.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-378">pl.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-378">pl.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-379">Portugais (Brésil)</span><span class="sxs-lookup"><span data-stu-id="3fffd-379">Portuguese (Brazil)</span></span></td>
        <td><span data-ttu-id="3fffd-380">pt-Br.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-380">pt-Br.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-381">pt-Br.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-381">pt-Br.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-382">Portugais (Portugal)</span><span class="sxs-lookup"><span data-stu-id="3fffd-382">Portuguese (Portugal)</span></span></td>
        <td><span data-ttu-id="3fffd-383">pt-Pt.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-383">pt-Pt.microsoft</span></span></td>        
        <td><span data-ttu-id="3fffd-384">pt-Pt.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-384">pt-Pt.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-385">Pendjabi</span><span class="sxs-lookup"><span data-stu-id="3fffd-385">Punjabi</span></span></td>
        <td><span data-ttu-id="3fffd-386">pa.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-386">pa.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-387">Roumain</span><span class="sxs-lookup"><span data-stu-id="3fffd-387">Romanian</span></span></td>
        <td><span data-ttu-id="3fffd-388">ro.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-388">ro.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-389">ro.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-389">ro.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-390">Russe</span><span class="sxs-lookup"><span data-stu-id="3fffd-390">Russian</span></span></td>
        <td><span data-ttu-id="3fffd-391">ru.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-391">ru.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-392">ru.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-392">ru.lucene</span></span></td>    
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-393">Serbe (cyrillique)</span><span class="sxs-lookup"><span data-stu-id="3fffd-393">Serbian (Cyrillic)</span></span></td>
        <td><span data-ttu-id="3fffd-394">sr-cyrillic.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-394">sr-cyrillic.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-395">Serbe (latin)</span><span class="sxs-lookup"><span data-stu-id="3fffd-395">Serbian (Latin)</span></span></td>
        <td><span data-ttu-id="3fffd-396">sr-latin.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-396">sr-latin.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-397">Slovaque</span><span class="sxs-lookup"><span data-stu-id="3fffd-397">Slovak</span></span></td>
        <td><span data-ttu-id="3fffd-398">sk.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-398">sk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-399">Slovène</span><span class="sxs-lookup"><span data-stu-id="3fffd-399">Slovenian</span></span></td>
        <td><span data-ttu-id="3fffd-400">sl.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-400">sl.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-401">Espagnol</span><span class="sxs-lookup"><span data-stu-id="3fffd-401">Spanish</span></span></td>
        <td><span data-ttu-id="3fffd-402">es.Microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-402">es.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-403">es.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-403">es.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-404">Suédois</span><span class="sxs-lookup"><span data-stu-id="3fffd-404">Swedish</span></span></td>
        <td><span data-ttu-id="3fffd-405">sv.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-405">sv.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-406">sv.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-406">sv.lucene</span></span></td>
    </tr>

    <tr>
        <td><span data-ttu-id="3fffd-407">Tamoul</span><span class="sxs-lookup"><span data-stu-id="3fffd-407">Tamil</span></span></td>
        <td><span data-ttu-id="3fffd-408">ta.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-408">ta.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-409">Télougou</span><span class="sxs-lookup"><span data-stu-id="3fffd-409">Telugu</span></span></td>
        <td><span data-ttu-id="3fffd-410">te.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-410">te.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-411">Thaï</span><span class="sxs-lookup"><span data-stu-id="3fffd-411">Thai</span></span></td>
        <td><span data-ttu-id="3fffd-412">th.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-412">th.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-413">th.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-413">th.lucene</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-414">Turc</span><span class="sxs-lookup"><span data-stu-id="3fffd-414">Turkish</span></span></td>
        <td><span data-ttu-id="3fffd-415">tr.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-415">tr.microsoft</span></span></td>
        <td><span data-ttu-id="3fffd-416">tr.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-416">tr.lucene</span></span></td>        
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-417">Ukrainien</span><span class="sxs-lookup"><span data-stu-id="3fffd-417">Ukrainian</span></span></td>
        <td><span data-ttu-id="3fffd-418">uk.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-418">uk.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-419">Ourdou</span><span class="sxs-lookup"><span data-stu-id="3fffd-419">Urdu</span></span></td>
        <td><span data-ttu-id="3fffd-420">ur.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-420">ur.microsoft</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-421">Vietnamien</span><span class="sxs-lookup"><span data-stu-id="3fffd-421">Vietnamese</span></span></td>
        <td><span data-ttu-id="3fffd-422">vi.microsoft</span><span class="sxs-lookup"><span data-stu-id="3fffd-422">vi.microsoft</span></span></td>
        <td></td>
    </tr>
    <td colspan="3"><span data-ttu-id="3fffd-423">En outre, Azure Search fournit des configurations d'analyseur sans langage spécifié</span><span class="sxs-lookup"><span data-stu-id="3fffd-423">Additionally Azure Search provides language-agnostic analyzer configurations</span></span></td>
    <tr>
        <td><span data-ttu-id="3fffd-424">Pliage ASCII standard</span><span class="sxs-lookup"><span data-stu-id="3fffd-424">Standard ASCII Folding</span></span></td>
        <td><span data-ttu-id="3fffd-425">standardasciifolding.lucene</span><span class="sxs-lookup"><span data-stu-id="3fffd-425">standardasciifolding.lucene</span></span></td>
        <td>
        <ul>
            <li><span data-ttu-id="3fffd-426">Segmentation de texte Unicode (générateur de jetons standard)</span><span class="sxs-lookup"><span data-stu-id="3fffd-426">Unicode text segmentation (Standard Tokenizer)</span></span></li>
            <li><span data-ttu-id="3fffd-427">Filtre de pliage ASCII - convertit les caractères Unicode qui n’appartiennent pas ensemble toohello de 127 premiers caractères ASCII dans leurs équivalents ASCII.</span><span class="sxs-lookup"><span data-stu-id="3fffd-427">ASCII folding filter - converts Unicode characters that don't belong toohello set of first 127 ASCII characters into their ASCII equivalents.</span></span> <span data-ttu-id="3fffd-428">Cela est utile pour supprimer les signes diacritiques.</span><span class="sxs-lookup"><span data-stu-id="3fffd-428">This is useful for removing diacritics.</span></span></li>
        </ul>
        </td>
    </tr>
</table>

<span data-ttu-id="3fffd-429">Tous les analyseurs dont les noms sont annotés avec <i>lucene</i> s’appuient sur les [analyseurs de langue d’Apache Lucene](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span><span class="sxs-lookup"><span data-stu-id="3fffd-429">All analyzers with names annotated with <i>lucene</i> are powered by [Apache Lucene's language analyzers](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html).</span></span> <span data-ttu-id="3fffd-430">Plus d’informations sur le filtre pliage ASCII de hello trouverez [ici](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span><span class="sxs-lookup"><span data-stu-id="3fffd-430">More information about hello ASCII folding filter can be found [here](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).</span></span>

<span data-ttu-id="3fffd-431">**Générateurs de suggestions**</span><span class="sxs-lookup"><span data-stu-id="3fffd-431">**Suggesters**</span></span>

<span data-ttu-id="3fffd-432">A `suggester` définit les champs dans un index sont utilisé toosupport saisie semi-automatique dans les recherches.</span><span class="sxs-lookup"><span data-stu-id="3fffd-432">A `suggester` defines which fields in an index are used toosupport auto-complete in searches.</span></span> <span data-ttu-id="3fffd-433">En général, les chaînes de recherche partielles sont envoyées toohello [Suggestions API](#Suggestions) pendant hello saisie d’une requête de recherche, et hello API renvoie un ensemble d’expressions suggérées.</span><span class="sxs-lookup"><span data-stu-id="3fffd-433">Typically partial search strings are sent toohello [Suggestions API](#Suggestions) while hello user is typing a search query, and hello API returns a set of suggested phrases.</span></span> <span data-ttu-id="3fffd-434">Un générateur de suggestions que vous définissez dans les index hello détermine quels champs sont des termes de recherche prédictives hello toobuild utilisé.</span><span class="sxs-lookup"><span data-stu-id="3fffd-434">A suggester that you define in hello index determines which fields are used toobuild hello type-ahead search terms.</span></span> <span data-ttu-id="3fffd-435">Consultez [Générateurs de suggestion](#Suggesters) pour plus de détails sur la configuration.</span><span class="sxs-lookup"><span data-stu-id="3fffd-435">See [Suggesters](#Suggesters) for configuration details.</span></span>

<span data-ttu-id="3fffd-436">**Profils de score**</span><span class="sxs-lookup"><span data-stu-id="3fffd-436">**Scoring profiles**</span></span>

<span data-ttu-id="3fffd-437">A `scoringProfile` définit le calcul de score des comportements personnalisés qui vous permettent d’influencer les éléments qui apparaissent plus dans les résultats de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-437">A `scoringProfile` defines custom scoring behaviors that let you influence which items appear higher in hello search results.</span></span> <span data-ttu-id="3fffd-438">Les profils de calcul de score sont constitués de pondérations et de fonctions de champ.</span><span class="sxs-lookup"><span data-stu-id="3fffd-438">Scoring profiles are made up of field weights and functions.</span></span> <span data-ttu-id="3fffd-439">toouse les, vous spécifiez un profil par nom de chaîne de requête hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-439">toouse them, you specify a profile by name on hello query string.</span></span>

<span data-ttu-id="3fffd-440">Profil de calcul de score par défaut fonctionne derrière hello scènes toocompute un score de recherche pour chaque élément dans un jeu de résultats.</span><span class="sxs-lookup"><span data-stu-id="3fffd-440">A default scoring profile operates behind hello scenes toocompute a search score for every item in a result set.</span></span> <span data-ttu-id="3fffd-441">Vous pouvez utiliser hello interne, sans nom, le profil de score.</span><span class="sxs-lookup"><span data-stu-id="3fffd-441">You can use hello internal, unnamed scoring profile.</span></span> <span data-ttu-id="3fffd-442">Vous pouvez également définir `defaultScoringProfile` toouse un profil personnalisé comme valeur par défaut de hello, appelé chaque fois qu’un profil personnalisé n’est pas spécifié dans la chaîne de requête hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-442">Alternatively, set `defaultScoringProfile` toouse a custom profile as hello default, invoked whenever a custom profile is not specified on hello query string.</span></span>

<span data-ttu-id="3fffd-443">Consultez [ajouter score profils tooa des index de recherche (API REST Service Azure Search)](search-api-scoring-profiles-2015-02-28-preview.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="3fffd-443">See [Add scoring profiles tooa search index (Azure Search Service REST API)](search-api-scoring-profiles-2015-02-28-preview.md) for details.</span></span>

<span data-ttu-id="3fffd-444">**Options CORS**</span><span class="sxs-lookup"><span data-stu-id="3fffd-444">**CORS Options**</span></span>

<span data-ttu-id="3fffd-445">Javascript côté client ne peut pas appeler des API par défaut étant donné que hello navigateur empêche toutes les demandes cross-origin.</span><span class="sxs-lookup"><span data-stu-id="3fffd-445">Client-side Javascript cannot call any APIs by default since hello browser will prevent all cross-origin requests.</span></span> <span data-ttu-id="3fffd-446">Activer les CORS (partage des ressources Cross-Origin) en définissant les hello `corsOptions` index d’attribut tooallow requêtes cross-origin tooyour.</span><span class="sxs-lookup"><span data-stu-id="3fffd-446">Enable CORS (Cross-Origin Resource Sharing) by setting hello `corsOptions` attribute tooallow cross-origin queries tooyour index.</span></span> <span data-ttu-id="3fffd-447">Notez que, pour des raisons de sécurité, seules les API de requête prennent en charge CORS.</span><span class="sxs-lookup"><span data-stu-id="3fffd-447">Note that only query APIs support CORS for security reasons.</span></span> <span data-ttu-id="3fffd-448">Hello options suivantes peut être définie pour CORS :</span><span class="sxs-lookup"><span data-stu-id="3fffd-448">hello following options can be set for CORS:</span></span>

* <span data-ttu-id="3fffd-449">`allowedOrigins`(obligatoire) : il s’agit d’une liste d’origines qui sera octroyé l’index tooyour access.</span><span class="sxs-lookup"><span data-stu-id="3fffd-449">`allowedOrigins` (required): This is a list of origins that will be granted access tooyour index.</span></span> <span data-ttu-id="3fffd-450">Cela signifie que tout code Javascript servi à partir de ces origines sera autorisé tooquery votre index (en supposant qu’il fournit la clé d’API correcte hello).</span><span class="sxs-lookup"><span data-stu-id="3fffd-450">This means that any Javascript code served from those origins will be allowed tooquery your index (assuming it provides hello correct API key).</span></span> <span data-ttu-id="3fffd-451">Chaque origine est en général sous forme de hello `protocol://fully-qualified-domain-name:port` bien que hello port est souvent omis.</span><span class="sxs-lookup"><span data-stu-id="3fffd-451">Each origin is typically of hello form `protocol://fully-qualified-domain-name:port` although hello port is often omitted.</span></span> <span data-ttu-id="3fffd-452">Consultez [cet article](http://go.microsoft.com/fwlink/?LinkId=330822) pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="3fffd-452">See [this article](http://go.microsoft.com/fwlink/?LinkId=330822) for more details.</span></span>
  * <span data-ttu-id="3fffd-453">Si vous souhaitez origines de tooall accès tooallow, inclure `*` comme un seul élément Bonjour `allowedOrigins` tableau.</span><span class="sxs-lookup"><span data-stu-id="3fffd-453">If you want tooallow access tooall origins, include `*` as a single item in hello `allowedOrigins` array.</span></span> <span data-ttu-id="3fffd-454">Notez que **cette pratique est déconseillée pour les services de recherche de production.**</span><span class="sxs-lookup"><span data-stu-id="3fffd-454">Note that **this is not recommended practice for production search services.**</span></span> <span data-ttu-id="3fffd-455">Toutefois, elle peut être utile à des fins de développement ou de débogage.</span><span class="sxs-lookup"><span data-stu-id="3fffd-455">However, it may be useful for development or debugging purposes.</span></span>
* <span data-ttu-id="3fffd-456">`maxAgeInSeconds`(facultatif) : les navigateurs utilisent cette valeur toodetermine hello durée (en secondes) toocache réponses préliminaires CORS.</span><span class="sxs-lookup"><span data-stu-id="3fffd-456">`maxAgeInSeconds` (optional): Browsers use this value toodetermine hello duration (in seconds) toocache CORS preflight responses.</span></span> <span data-ttu-id="3fffd-457">Il doit s'agir d'un entier non négatif.</span><span class="sxs-lookup"><span data-stu-id="3fffd-457">This must be a non-negative integer.</span></span> <span data-ttu-id="3fffd-458">Hello plu que cette valeur est, améliorer les performances hello, mais hello plus long, qu'il aura pour effet de tootake de modifications de stratégie CORS.</span><span class="sxs-lookup"><span data-stu-id="3fffd-458">hello larger this value is, hello better performance will be, but hello longer it will take for CORS policy changes tootake effect.</span></span> <span data-ttu-id="3fffd-459">Si la valeur n'est pas définie, une durée par défaut de 5 minutes est utilisée.</span><span class="sxs-lookup"><span data-stu-id="3fffd-459">If it is not set, a default duration of 5 minutes will be used.</span></span>

<span data-ttu-id="3fffd-460"><a name="CreateUpdateIndexExample"></a>
**Exemple de corps de requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-460"><a name="CreateUpdateIndexExample"></a>
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

<span data-ttu-id="3fffd-461">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="3fffd-461">**Response**</span></span>

<span data-ttu-id="3fffd-462">Pour une requête correcte : « 201 Créé ».</span><span class="sxs-lookup"><span data-stu-id="3fffd-462">For a successful request: "201 Created".</span></span>

<span data-ttu-id="3fffd-463">Par défaut, les corps de réponse hello contiendra hello JSON pour la définition de l’index hello qui a été créée.</span><span class="sxs-lookup"><span data-stu-id="3fffd-463">By default hello response body will contain hello JSON for hello index definition that was created.</span></span> <span data-ttu-id="3fffd-464">Si hello `Prefer` en-tête de demande est défini trop`return=minimal`, corps de réponse hello sera vide et le code d’état de réussite hello sera « 204 pas de contenu » au lieu de « 201 créé ».</span><span class="sxs-lookup"><span data-stu-id="3fffd-464">If hello `Prefer` request header is set too`return=minimal`, hello response body will be empty and hello success status code will be "204 No Content" instead of "201 Created".</span></span> <span data-ttu-id="3fffd-465">Cela est vrai, que soient PUT ou POST index de hello toocreate utilisé.</span><span class="sxs-lookup"><span data-stu-id="3fffd-465">This is true regardless of whether PUT or POST was used toocreate hello index.</span></span>

<span data-ttu-id="3fffd-466">**Remarques**</span><span class="sxs-lookup"><span data-stu-id="3fffd-466">**Remarks**</span></span>

<span data-ttu-id="3fffd-467">Actuellement, la prise en charge des mises à jour de schéma d'index est limitée.</span><span class="sxs-lookup"><span data-stu-id="3fffd-467">Currently, there is limited support for index schema updates.</span></span> <span data-ttu-id="3fffd-468">Les mises à jour de schéma qui nécessitent une réindexation, par exemple la modification des types de champs, ne sont pas prises en charge pour le moment.</span><span class="sxs-lookup"><span data-stu-id="3fffd-468">Any schema updates that would require re-indexing such as changing field types are not currently supported.</span></span> <span data-ttu-id="3fffd-469">Bien que les champs existants ne peut pas être modifiés ou supprimés, les nouveaux champs peuvent être ajoutés à l’index existant tooan à tout moment.</span><span class="sxs-lookup"><span data-stu-id="3fffd-469">Although existing fields cannot be changed or deleted, new fields can be added tooan existing index at any time.</span></span> <span data-ttu-id="3fffd-470">Lorsqu’un nouveau champ est ajouté, tous les documents existants dans les index hello auront automatiquement une valeur null pour ce champ.</span><span class="sxs-lookup"><span data-stu-id="3fffd-470">When a new field is added, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="3fffd-471">Aucun espace de stockage supplémentaires n’est consommée jusqu'à ce que les nouveaux documents sont ajoutés toohello index.</span><span class="sxs-lookup"><span data-stu-id="3fffd-471">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<a name="Suggesters"></a>

## <a name="suggesters"></a><span data-ttu-id="3fffd-472">Générateurs de suggestions</span><span class="sxs-lookup"><span data-stu-id="3fffd-472">Suggesters</span></span>
<span data-ttu-id="3fffd-473">fonctionnalité de suggestions Hello dans Azure Search est une fonctionnalité de requête prédictives ou semi-automatique, en fournissant une liste de termes recherchés potentiels dans les entrées de chaîne toopartial de réponse entrées dans une zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-473">hello suggestions feature in Azure Search is a type-ahead or auto-complete query capability, providing a list of potential search terms in response toopartial string inputs entered into a search box.</span></span> <span data-ttu-id="3fffd-474">Vous avez probablement remarqué des suggestions de requête lors de l’utilisation de moteurs de recherche web commerciaux : la saisie de « NET » dans Bing génère une liste de termes pour « .NET 4.5 », « .NET Framework 3.5 », etc.</span><span class="sxs-lookup"><span data-stu-id="3fffd-474">You've probably noticed query suggestions when using commercial web search engines: typing ".NET" in Bing produces a list of terms for ".NET 4.5", ".NET Framework 3.5", and so forth.</span></span> <span data-ttu-id="3fffd-475">Lorsque vous utilisez l’API REST du service de recherche hello, implémentation de suggestions dans une application Azure Search personnalisée requiert des hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="3fffd-475">When using hello Search service REST API, implementing suggestions in a custom Azure Search application requires hello following:</span></span>

* <span data-ttu-id="3fffd-476">Activer les suggestions en ajoutant un **suggestions** construction dans votre index, en fournissant le nom de hello, mode de recherche et une liste de champs pour lequel prédictives est appelée.</span><span class="sxs-lookup"><span data-stu-id="3fffd-476">Enable suggestions by adding a **suggester** construction in your index, giving hello name, search mode, and a list of fields for which type-ahead is invoked.</span></span> <span data-ttu-id="3fffd-477">Par exemple, si vous spécifiez « cityName » comme un champ source, en tapant une chaîne de recherche partielle de « Sea » entraîne « Seattle », « Seaside » et « Seatac » (les trois sont des noms de ville) offerts dans les en tant qu’utilisateur de toohello des suggestions de requête.</span><span class="sxs-lookup"><span data-stu-id="3fffd-477">For example, if you specify "cityName" as a source field, typing a partial search string of "Sea" will result in "Seattle", "Seaside", and "Seatac" (all three are actual city names) offered up as query suggestions toohello user.</span></span>
* <span data-ttu-id="3fffd-478">Demander des suggestions en appelant hello [Suggestions API](#Suggestions) dans votre code d’application.</span><span class="sxs-lookup"><span data-stu-id="3fffd-478">Invoke suggestions by calling hello [Suggestions API](#Suggestions) in your application code.</span></span> <span data-ttu-id="3fffd-479">En général, les chaînes de recherche partielle sont envoyées toohello service pendant hello saisie d’une requête de recherche, et cette API renvoie un ensemble d’expressions suggérées.</span><span class="sxs-lookup"><span data-stu-id="3fffd-479">Typically partial search strings are sent toohello service while hello user is typing a search query, and this API returns a set of suggested phrases.</span></span>

<span data-ttu-id="3fffd-480">Cet article explique comment tooconfigure un **suggestions**.</span><span class="sxs-lookup"><span data-stu-id="3fffd-480">This article explains how tooconfigure a **suggester**.</span></span> <span data-ttu-id="3fffd-481">Vous devez également examiner hello [Suggestions API](#Suggestions) pour plus d’informations sur l’utilisation d’un générateur de suggestions.</span><span class="sxs-lookup"><span data-stu-id="3fffd-481">You should also review hello [Suggestions API](#Suggestions) for details on how a suggester is used.</span></span>

<span data-ttu-id="3fffd-482">**Utilisation**</span><span class="sxs-lookup"><span data-stu-id="3fffd-482">**Usage**</span></span>

<span data-ttu-id="3fffd-483">`Suggesters`sont créés dans les index hello et optimale des documents spécifiques de toosuggest plutôt que des termes ou expressions.</span><span class="sxs-lookup"><span data-stu-id="3fffd-483">`Suggesters` are created in hello index and work best when used toosuggest specific documents rather than loose terms or phrases.</span></span> <span data-ttu-id="3fffd-484">champs Hello les plus appropriés sont les titres, les noms et les autres expressions relativement courtes pouvant identifier un élément.</span><span class="sxs-lookup"><span data-stu-id="3fffd-484">hello best candidate fields are titles, names, and other relatively short phrases that can identify an item.</span></span> <span data-ttu-id="3fffd-485">Les champs les moins efficaces sont les champs répétitifs, tels que les catégories et les balises, ou les champs très longs, tels que les champs des descriptions ou des commentaires.</span><span class="sxs-lookup"><span data-stu-id="3fffd-485">Less effective are repetitive fields, such as categories and tags, or very long fields such as descriptions or comments fields.</span></span>

<span data-ttu-id="3fffd-486">Dans le cadre de la définition de l’index hello, vous pouvez ajouter un toohello unique suggestions `suggesters` collection.</span><span class="sxs-lookup"><span data-stu-id="3fffd-486">As part of hello index definition, you can add a single suggester toohello `suggesters` collection.</span></span> <span data-ttu-id="3fffd-487">Les propriétés qui définissent un générateur de suggestions hello suivants :</span><span class="sxs-lookup"><span data-stu-id="3fffd-487">Properties that define a suggester include hello following:</span></span>

* <span data-ttu-id="3fffd-488">`name`: nom de hello du Générateur de suggestions hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-488">`name`: hello name of hello suggester.</span></span> <span data-ttu-id="3fffd-489">Vous utilisez le nom hello du Générateur de suggestions hello lors de l’appel hello `suggest` API.</span><span class="sxs-lookup"><span data-stu-id="3fffd-489">You use hello name of hello suggester when calling hello `suggest` API.</span></span>
* <span data-ttu-id="3fffd-490">`searchMode`: hello toosearch stratégie utilisée pour les expressions candidates.</span><span class="sxs-lookup"><span data-stu-id="3fffd-490">`searchMode`: hello strategy used toosearch for candidate phrases.</span></span> <span data-ttu-id="3fffd-491">Bonjour seul mode actuellement pris en charge est `analyzingInfixMatching`, qui effectue des correspondances souples au début de hello ou au milieu de hello de phrases.</span><span class="sxs-lookup"><span data-stu-id="3fffd-491">hello only mode currently supported is `analyzingInfixMatching`, which performs flexible matching of phrases at hello beginning or in hello middle of sentences.</span></span>
* <span data-ttu-id="3fffd-492">`sourceFields`: Liste d’un ou plusieurs champs qui sont source de hello du contenu hello pour obtenir des suggestions.</span><span class="sxs-lookup"><span data-stu-id="3fffd-492">`sourceFields`: A list of one or more fields that are hello source of hello content for suggestions.</span></span> <span data-ttu-id="3fffd-493">Seuls les champs de type `Edm.String` et `Collection(Edm.String)` peuvent être des sources pour des suggestions.</span><span class="sxs-lookup"><span data-stu-id="3fffd-493">Only fields of type `Edm.String` and `Collection(Edm.String)` may be sources for suggestions.</span></span> <span data-ttu-id="3fffd-494">Seuls les champs qui n’ont pas un analyseur de langue personnalisé défini peuvent être utilisés.</span><span class="sxs-lookup"><span data-stu-id="3fffd-494">Only fields that don't have a custom language analyzer set can be used.</span></span>

<span data-ttu-id="3fffd-495">**Exemple de générateur de suggestions**</span><span class="sxs-lookup"><span data-stu-id="3fffd-495">**Suggester Example**</span></span>

<span data-ttu-id="3fffd-496">Un générateur de suggestions fait partie de l’index de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-496">A suggester is part of hello index.</span></span> <span data-ttu-id="3fffd-497">Générateur de suggestions qu’une seule peut exister dans hello `suggesters` collection de champs de regroupement dans la version actuelle de hello, en même temps que hello et `scoringProfiles`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-497">Only one suggester can exist in hello `suggesters` collection in hello current version, alongside hello fields collection and `scoringProfiles`.</span></span>

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
> <span data-ttu-id="3fffd-498">Si vous avez utilisé la version préliminaire publique de hello d’Azure Search, `suggesters` remplace une ancienne propriété booléenne (`"suggestions": false`) qui pris en charge uniquement des suggestions de préfixe pour les chaînes courtes (de 3 à 25 caractères).</span><span class="sxs-lookup"><span data-stu-id="3fffd-498">If you used hello public preview version of Azure Search, `suggesters` replaces an older boolean property (`"suggestions": false`) that only supported prefix suggestions for short strings (3-25 characters).</span></span> <span data-ttu-id="3fffd-499">Solution de remplacement, `suggesters`, prend en charge les correspondances infixes qui recherchent des termes au début de hello ou au milieu de hello du contenu du champ, avec une meilleure tolérance aux erreurs dans les chaînes de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-499">Its replacement, `suggesters`, supports infix matching that finds matching terms at hello beginning or in hello middle of field content, with better tolerance for mistakes in search strings.</span></span> <span data-ttu-id="3fffd-500">À compter de version généralement disponible de hello, il s’agit désormais hello uniquement implémentation de l’API des suggestions hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-500">Starting with hello generally available release, this is now hello only implementation of hello suggestions API.</span></span> <span data-ttu-id="3fffd-501">Hello plus anciens `suggestions` propriété qui a été introduite dans `api-version=2014-07-31-Preview` continue toowork dans cette version, mais n’est pas opérationnel Bonjour `2015-02-28` ou une version ultérieure d’Azure Search.</span><span class="sxs-lookup"><span data-stu-id="3fffd-501">hello older `suggestions` property that was introduced in `api-version=2014-07-31-Preview` continues toowork in that version, but is not operational in hello `2015-02-28` or later versions of Azure Search.</span></span>
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a><span data-ttu-id="3fffd-502">Mise à jour d'index</span><span class="sxs-lookup"><span data-stu-id="3fffd-502">Update Index</span></span>
<span data-ttu-id="3fffd-503">Vous pouvez mettre à jour un index existant dans Azure Search à l'aide d'une requête HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="3fffd-503">You can update an existing index within Azure Search using an HTTP PUT request.</span></span> <span data-ttu-id="3fffd-504">Les mises à jour peuvent inclure l’ajout de nouveaux champs toohello schéma existant, la modification des Cors et la modification des profils de calcul de score.</span><span class="sxs-lookup"><span data-stu-id="3fffd-504">Updates can include adding new fields toohello existing schema, modifying CORS options, and modifying scoring profiles.</span></span> <span data-ttu-id="3fffd-505">Pour plus d'informations, consultez [Ajout de profils de calcul de score](https://msdn.microsoft.com/library/azure/dn798928.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3fffd-505">See [Add scoring Profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> <span data-ttu-id="3fffd-506">Vous spécifiez le nom hello de hello index tooupdate sur l’URI de la demande hello :</span><span class="sxs-lookup"><span data-stu-id="3fffd-506">You specify hello name of hello index tooupdate on hello request URI:</span></span>

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="3fffd-507">**Important :** prise en charge des mises à jour de schéma index est toooperations limitées qui ne nécessitent pas la reconstruction d’index de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-507">**Important:** Support for index schema updates is limited toooperations that don't require rebuilding hello search index.</span></span> <span data-ttu-id="3fffd-508">Les mises à jour de schéma qui nécessitent une réindexation, par exemple la modification des types de champs, ne sont pas prises en charge pour le moment.</span><span class="sxs-lookup"><span data-stu-id="3fffd-508">Any schema updates that would require re-indexing, such as changing field types, are not currently supported.</span></span> <span data-ttu-id="3fffd-509">De nouveaux champs peuvent être ajoutés à tout moment, mais les champs existants ne peuvent pas être modifiés ni supprimés.</span><span class="sxs-lookup"><span data-stu-id="3fffd-509">New fields can be added at any time, although existing fields cannot be changed or deleted.</span></span> <span data-ttu-id="3fffd-510">Hello valable trop`suggesters`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-510">hello same applies too`suggesters`.</span></span> <span data-ttu-id="3fffd-511">Ajouter de nouveaux champs suggestions tooa au niveau des champs hello hello sont ajoutés, mais les champs ne peuvent pas être supprimés de `suggesters` et champs existants ne peuvent pas être ajoutés trop`suggesters`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-511">New fields may be added tooa suggester at hello time hello fields are added, but fields cannot be removed from `suggesters` and existing fields cannot be added too`suggesters`.</span></span>

<span data-ttu-id="3fffd-512">Lorsque vous ajoutez un nouvel index tooan de champ, tous les documents existants dans les index hello auront automatiquement une valeur null pour ce champ.</span><span class="sxs-lookup"><span data-stu-id="3fffd-512">When adding a new field tooan index, all existing documents in hello index will automatically have a null value for that field.</span></span> <span data-ttu-id="3fffd-513">Aucun espace de stockage supplémentaires n’est consommée jusqu'à ce que les nouveaux documents sont ajoutés toohello index.</span><span class="sxs-lookup"><span data-stu-id="3fffd-513">No additional storage space will be consumed until new documents are added toohello index.</span></span>

<span data-ttu-id="3fffd-514">**Requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-514">**Request**</span></span>

<span data-ttu-id="3fffd-515">Le protocole HTTPS est requis pour toutes les requêtes de service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-515">HTTPS is required for all service requests.</span></span> <span data-ttu-id="3fffd-516">Hello **Index de mise à jour** demande est construite à l’aide de HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="3fffd-516">hello **Update Index** request is constructed using HTTP PUT.</span></span> <span data-ttu-id="3fffd-517">Avec PUT, nom de l’index hello fait partie de l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-517">With PUT, hello index name is part of hello URL.</span></span> <span data-ttu-id="3fffd-518">Si les index hello n’existe pas, il est créé.</span><span class="sxs-lookup"><span data-stu-id="3fffd-518">If hello index doesn't exist, it is created.</span></span> <span data-ttu-id="3fffd-519">Si l’index hello existe déjà, il est mis à jour toohello nouvelle définition.</span><span class="sxs-lookup"><span data-stu-id="3fffd-519">If hello index already exists, it is updated toohello new definition.</span></span>

<span data-ttu-id="3fffd-520">Hello nom d’index doit être en minuscules, commencer par une lettre ou un chiffre, contenir sans barres obliques ni points et être inférieure à 128 caractères.</span><span class="sxs-lookup"><span data-stu-id="3fffd-520">hello index name must be lower case, start with a letter or number, have no slashes or dots, and be less than 128 characters.</span></span> <span data-ttu-id="3fffd-521">Après avoir démarré le nom de l’index hello par une lettre ou un chiffre, reste hello du nom de hello peut inclure toute lettre, le numéro et des tirets, tant que les tirets hello ne soient pas contigus.</span><span class="sxs-lookup"><span data-stu-id="3fffd-521">After starting hello index name with a letter or number, hello rest of hello name can include any letter, number and dashes, as long as hello dashes are not consecutive.</span></span>

<span data-ttu-id="3fffd-522">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="3fffd-522">`api-version=[string]` (required).</span></span> <span data-ttu-id="3fffd-523">version d’évaluation Hello `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-523">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3fffd-524">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3fffd-524">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3fffd-525">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-525">**Request Headers**</span></span>

<span data-ttu-id="3fffd-526">Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.</span><span class="sxs-lookup"><span data-stu-id="3fffd-526">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3fffd-527">`Content-Type`: requis.</span><span class="sxs-lookup"><span data-stu-id="3fffd-527">`Content-Type`: Required.</span></span> <span data-ttu-id="3fffd-528">Définissez cette propriété trop`application/json`</span><span class="sxs-lookup"><span data-stu-id="3fffd-528">Set this too`application/json`</span></span>
* <span data-ttu-id="3fffd-529">`api-key`: obligatoire.</span><span class="sxs-lookup"><span data-stu-id="3fffd-529">`api-key`: Required.</span></span> <span data-ttu-id="3fffd-530">Hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-530">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3fffd-531">Il s’agit d’une valeur de chaîne, d’un service de tooyour unique.</span><span class="sxs-lookup"><span data-stu-id="3fffd-531">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="3fffd-532">Hello **Index de mise à jour** demande doit inclure un `api-key` en-tête défini la clé d’administration tooyour (en tant que clé de requête tooa exécutée).</span><span class="sxs-lookup"><span data-stu-id="3fffd-532">hello **Update Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="3fffd-533">Vous devez également les URL de demande du nom tooconstruct hello hello service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-533">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3fffd-534">Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3fffd-534">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3fffd-535">Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.</span><span class="sxs-lookup"><span data-stu-id="3fffd-535">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3fffd-536">**Syntaxe du corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-536">**Request Body Syntax**</span></span>

<span data-ttu-id="3fffd-537">Lors de la mise à jour d’un index existant, les corps hello doivent inclure la définition de schéma d’origine hello plus hello nouveaux champs que vous ajoutez ainsi hello modifié des profils de calcul de score, générateurs de suggestions et les options CORS, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="3fffd-537">When updating an existing index, hello body must include hello original schema definition, plus hello new fields you are adding, as well as hello modified scoring profiles, suggesters and CORS options, if any.</span></span> <span data-ttu-id="3fffd-538">Si vous ne modifiez pas les profils de calcul de score hello et les options CORS, vous devez inclure les originaux hello lorsque les index hello a été créé.</span><span class="sxs-lookup"><span data-stu-id="3fffd-538">If you are not modifying hello scoring profiles and CORS options, you must include hello originals from when hello index was created.</span></span> <span data-ttu-id="3fffd-539">En général hello meilleur modèle toouse des mises à jour est la définition d’index hello tooretrieve avec une commande GET, modifiez-le, puis mettez-le à jour avec une méthode PUT.</span><span class="sxs-lookup"><span data-stu-id="3fffd-539">In general hello best pattern toouse for updates is tooretrieve hello index definition with a GET, modify it, then update it with PUT.</span></span>

<span data-ttu-id="3fffd-540">syntaxe de schéma Hello utilisé toocreate qu'un index est reproduit ici par commodité.</span><span class="sxs-lookup"><span data-stu-id="3fffd-540">hello schema syntax used toocreate an index is reproduced here for convenience.</span></span> <span data-ttu-id="3fffd-541">Consultez la section [Création d'index](#CreateIndex) pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="3fffd-541">See [Create Index](#CreateIndex) for more details.</span></span>

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
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
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
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
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


<span data-ttu-id="3fffd-542">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="3fffd-542">**Response**</span></span>

<span data-ttu-id="3fffd-543">Pour une requête correcte : « 204 Pas de contenu ».</span><span class="sxs-lookup"><span data-stu-id="3fffd-543">For a successful request: "204 No Content".</span></span>

<span data-ttu-id="3fffd-544">Par défaut, les corps de réponse hello sera vide.</span><span class="sxs-lookup"><span data-stu-id="3fffd-544">By default hello response body will be empty.</span></span> <span data-ttu-id="3fffd-545">Toutefois, si hello `Prefer` en-tête de demande est défini trop`return=representation`, corps de réponse hello contiendra hello JSON pour la définition de l’index hello qui a été mis à jour.</span><span class="sxs-lookup"><span data-stu-id="3fffd-545">However, if hello `Prefer` request header is set too`return=representation`, hello response body will contain hello JSON for hello index definition that was updated.</span></span> <span data-ttu-id="3fffd-546">Dans ce cas, le code d’état de réussite hello sera « 200 OK ».</span><span class="sxs-lookup"><span data-stu-id="3fffd-546">In this case, hello success status code will be "200 OK".</span></span>

<span data-ttu-id="3fffd-547">**Mise à jour de la définition d’index avec des analyseurs personnalisés**</span><span class="sxs-lookup"><span data-stu-id="3fffd-547">**Updating index definition with custom analyzers**</span></span>

<span data-ttu-id="3fffd-548">Une fois défini, un analyseur, un générateur de jetons, un filtre de jetons ou un filtre de caractères ne peut pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="3fffd-548">Once an analyzer, a tokenizer, a token filter or a char filter is defined, it cannot be modified.</span></span> <span data-ttu-id="3fffd-549">Nouveaux peut être ajoutés les index existants tooan uniquement si hello `allowIndexDowntime` indicateur a la valeur tootrue dans la demande de mise à jour d’index hello :</span><span class="sxs-lookup"><span data-stu-id="3fffd-549">New ones can be added tooan existing index only if hello `allowIndexDowntime` flag is set tootrue in hello index update request:</span></span> 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

<span data-ttu-id="3fffd-550">Notez que cette opération mettra votre index hors connexion au moins de quelques secondes, à l’origine de votre indexation et de requête demande toofail.</span><span class="sxs-lookup"><span data-stu-id="3fffd-550">Note that this operation will put your index offline for at least a few seconds, causing your indexing and query requests toofail.</span></span> <span data-ttu-id="3fffd-551">Disponibilité de performances et d’écriture de l’index de hello peut être altérée pendant plusieurs minutes après hello est mis à jour, ou plus de temps pour les très grands index.</span><span class="sxs-lookup"><span data-stu-id="3fffd-551">Performance and write availability of hello index can be impaired for several minutes after hello index is updated, or longer for very large indexes.</span></span>

<a name="ListIndexes"></a>

## <a name="list-indexes"></a><span data-ttu-id="3fffd-552">Liste des index</span><span class="sxs-lookup"><span data-stu-id="3fffd-552">List Indexes</span></span>
<span data-ttu-id="3fffd-553">Hello **liste des index** opération renvoie une liste des index de hello actuellement dans votre service Azure Search.</span><span class="sxs-lookup"><span data-stu-id="3fffd-553">hello **List Indexes** operation returns a list of hello indexes currently in your Azure Search service.</span></span>

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="3fffd-554">**Requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-554">**Request**</span></span>

<span data-ttu-id="3fffd-555">Le protocole HTTPS est requis pour toutes les requêtes de service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-555">HTTPS is required for all service requests.</span></span> <span data-ttu-id="3fffd-556">Hello **liste des index** demande peut être construite à l’aide de la méthode GET de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-556">hello **List Indexes** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="3fffd-557">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="3fffd-557">`api-version=[string]` (required).</span></span> <span data-ttu-id="3fffd-558">version d’évaluation Hello `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-558">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3fffd-559">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3fffd-559">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3fffd-560">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-560">**Request Headers**</span></span>

<span data-ttu-id="3fffd-561">Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.</span><span class="sxs-lookup"><span data-stu-id="3fffd-561">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3fffd-562">`api-key`: obligatoire.</span><span class="sxs-lookup"><span data-stu-id="3fffd-562">`api-key`: Required.</span></span> <span data-ttu-id="3fffd-563">Hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-563">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3fffd-564">Il s’agit d’une valeur de chaîne, d’un service de tooyour unique.</span><span class="sxs-lookup"><span data-stu-id="3fffd-564">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="3fffd-565">Hello **liste des index** demande doit inclure un `api-key` clé d’administration tooan ensemble (en tant que clé de requête tooa exécutée).</span><span class="sxs-lookup"><span data-stu-id="3fffd-565">hello **List Indexes** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="3fffd-566">Vous devez également les URL de demande du nom tooconstruct hello hello service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-566">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3fffd-567">Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3fffd-567">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3fffd-568">Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.</span><span class="sxs-lookup"><span data-stu-id="3fffd-568">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3fffd-569">**Corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-569">**Request Body**</span></span>

<span data-ttu-id="3fffd-570">Aucune.</span><span class="sxs-lookup"><span data-stu-id="3fffd-570">None.</span></span>

<span data-ttu-id="3fffd-571">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="3fffd-571">**Response**</span></span>

<span data-ttu-id="3fffd-572">Code d'état : 200 OK est retourné pour une réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="3fffd-572">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="3fffd-573">Voici un exemple de corps de réponse :</span><span class="sxs-lookup"><span data-stu-id="3fffd-573">Here is an example response body:</span></span>

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

<span data-ttu-id="3fffd-574">Notez que vous pouvez filtrer la réponse hello vers le bas les propriétés de hello toojust que vous intéresse.</span><span class="sxs-lookup"><span data-stu-id="3fffd-574">Note that you can filter hello response down toojust hello properties you're interested in.</span></span> <span data-ttu-id="3fffd-575">Par exemple, si vous souhaitez uniquement la liste des noms d’index, utilisez hello OData `$select` option de requête :</span><span class="sxs-lookup"><span data-stu-id="3fffd-575">For example, if you want only a list of index names, use hello OData `$select` query option:</span></span>

    GET /indexes?api-version=2015-02-28-Preview&$select=name

<span data-ttu-id="3fffd-576">Dans ce cas, réponse hello hello exemple ci-dessus apparaît comme suit :</span><span class="sxs-lookup"><span data-stu-id="3fffd-576">In this case, hello response from hello above example would appear as follows:</span></span>

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

<span data-ttu-id="3fffd-577">Il s’agit d’une bande de passante toosave technique utile si vous avez un grand nombre d’index dans votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-577">This is a useful technique toosave bandwidth if you have a lot of indexes in your Search service.</span></span>

<a name="GetIndex"></a>

## <a name="get-index"></a><span data-ttu-id="3fffd-578">Obtention d'index</span><span class="sxs-lookup"><span data-stu-id="3fffd-578">Get Index</span></span>
<span data-ttu-id="3fffd-579">Hello **obtenir l’Index** opération Obtient la définition de l’index hello à partir d’Azure Search.</span><span class="sxs-lookup"><span data-stu-id="3fffd-579">hello **Get Index** operation gets hello index definition from Azure Search.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="3fffd-580">**Requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-580">**Request**</span></span>

<span data-ttu-id="3fffd-581">Le protocole HTTPS est requis pour les requêtes de service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-581">HTTPS is required for service requests.</span></span> <span data-ttu-id="3fffd-582">Hello **obtenir l’Index** demande peut être construite à l’aide de la méthode GET de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-582">hello **Get Index** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="3fffd-583">Bonjour [nom de l’index] dans l’URI de la demande hello spécifie quels tooreturn index à partir de la collection d’index hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-583">hello [index name] in hello request URI specifies which index tooreturn from hello indexes collection.</span></span>

<span data-ttu-id="3fffd-584">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="3fffd-584">`api-version=[string]` (required).</span></span> <span data-ttu-id="3fffd-585">version d’évaluation Hello `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-585">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3fffd-586">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3fffd-586">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3fffd-587">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-587">**Request Headers**</span></span>

<span data-ttu-id="3fffd-588">Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.</span><span class="sxs-lookup"><span data-stu-id="3fffd-588">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3fffd-589">`api-key`: hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-589">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3fffd-590">Il s’agit d’une valeur de chaîne, d’un service de tooyour unique.</span><span class="sxs-lookup"><span data-stu-id="3fffd-590">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="3fffd-591">Hello **obtenir l’Index** demande doit inclure un `api-key` clé d’administration tooan ensemble (en tant que clé de requête tooa exécutée).</span><span class="sxs-lookup"><span data-stu-id="3fffd-591">hello **Get Index** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="3fffd-592">Vous devez également les URL de demande du nom tooconstruct hello hello service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-592">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3fffd-593">Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3fffd-593">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3fffd-594">Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.</span><span class="sxs-lookup"><span data-stu-id="3fffd-594">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3fffd-595">**Corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-595">**Request Body**</span></span>

<span data-ttu-id="3fffd-596">Aucune.</span><span class="sxs-lookup"><span data-stu-id="3fffd-596">None.</span></span>

<span data-ttu-id="3fffd-597">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="3fffd-597">**Response**</span></span>

<span data-ttu-id="3fffd-598">Code d'état : 200 OK est retourné pour une réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="3fffd-598">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="3fffd-599">Consultez l’exemple hello JSON dans [création et mise à jour d’un Index](#CreateUpdateIndexExample) pour obtenir un exemple de charge utile de réponse hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-599">See hello example JSON in [Creating and Updating an Index](#CreateUpdateIndexExample) for an example of hello response payload.</span></span>

<a name="DeleteIndex"></a>

## <a name="delete-index"></a><span data-ttu-id="3fffd-600">Suppression d'index</span><span class="sxs-lookup"><span data-stu-id="3fffd-600">Delete Index</span></span>
<span data-ttu-id="3fffd-601">Hello **supprimer l’Index** opération supprime un index et les documents associés à partir de votre service Azure Search.</span><span class="sxs-lookup"><span data-stu-id="3fffd-601">hello **Delete Index** operation removes an index and associated documents from your Azure Search service.</span></span> <span data-ttu-id="3fffd-602">Vous pouvez obtenir le nom de l’index hello à partir du tableau de bord de service hello Bonjour portail Azure ou hello API.</span><span class="sxs-lookup"><span data-stu-id="3fffd-602">You can get hello index name from hello service dashboard in hello Azure portal, or from hello API.</span></span> <span data-ttu-id="3fffd-603">Consultez la section [List Indexes](#ListIndexes) pour plus d'informations.</span><span class="sxs-lookup"><span data-stu-id="3fffd-603">See [List Indexes](#ListIndexes) for details.</span></span>

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

<span data-ttu-id="3fffd-604">**Requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-604">**Request**</span></span>

<span data-ttu-id="3fffd-605">Le protocole HTTPS est requis pour les requêtes de service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-605">HTTPS is required for service requests.</span></span> <span data-ttu-id="3fffd-606">Hello **supprimer l’Index** demande peut être construite à l’aide de la méthode de suppression hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-606">hello **Delete Index** request can be constructed using hello DELETE method.</span></span>

<span data-ttu-id="3fffd-607">Bonjour [nom de l’index] dans l’URI de la demande hello spécifie quels toodelete index à partir de la collection d’index hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-607">hello [index name] in hello request URI specifies which index toodelete from hello indexes collection.</span></span>

<span data-ttu-id="3fffd-608">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="3fffd-608">`api-version=[string]` (required).</span></span> <span data-ttu-id="3fffd-609">version d’évaluation Hello `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-609">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3fffd-610">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3fffd-610">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3fffd-611">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-611">**Request Headers**</span></span>

<span data-ttu-id="3fffd-612">Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.</span><span class="sxs-lookup"><span data-stu-id="3fffd-612">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3fffd-613">`api-key`: obligatoire.</span><span class="sxs-lookup"><span data-stu-id="3fffd-613">`api-key`: Required.</span></span> <span data-ttu-id="3fffd-614">Hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-614">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3fffd-615">Il est une valeur de chaîne URL du service tooyour unique.</span><span class="sxs-lookup"><span data-stu-id="3fffd-615">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="3fffd-616">Hello **supprimer l’Index** demande doit inclure un `api-key` en-tête défini la clé d’administration tooyour (en tant que clé de requête tooa exécutée).</span><span class="sxs-lookup"><span data-stu-id="3fffd-616">hello **Delete Index** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="3fffd-617">Vous devez également les URL de demande du nom tooconstruct hello hello service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-617">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3fffd-618">Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3fffd-618">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3fffd-619">Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.</span><span class="sxs-lookup"><span data-stu-id="3fffd-619">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3fffd-620">**Corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-620">**Request Body**</span></span>

<span data-ttu-id="3fffd-621">Aucune.</span><span class="sxs-lookup"><span data-stu-id="3fffd-621">None.</span></span>

<span data-ttu-id="3fffd-622">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="3fffd-622">**Response**</span></span>

<span data-ttu-id="3fffd-623">Code d'état : 204 Pas de contenu est renvoyé en cas de réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="3fffd-623">Status Code: 204 No Content is returned for a successful response.</span></span>

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a><span data-ttu-id="3fffd-624">Obtention de statistiques d'index</span><span class="sxs-lookup"><span data-stu-id="3fffd-624">Get Index Statistics</span></span>
<span data-ttu-id="3fffd-625">Hello **obtenir des statistiques d’Index** opération renvoie à partir d’Azure Search un nombre de documents pour les index en cours de hello, ainsi que l’utilisation du stockage.</span><span class="sxs-lookup"><span data-stu-id="3fffd-625">hello **Get Index Statistics** operation returns from Azure Search a document count for hello current index, plus storage usage.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> <span data-ttu-id="3fffd-626">Les statistiques sur le nombre de documents et la taille du stockage sont collectées à intervalles de quelques minutes, pas en temps réel.</span><span class="sxs-lookup"><span data-stu-id="3fffd-626">Statistics on document count and storage size are collected every few minutes, not in real time.</span></span> <span data-ttu-id="3fffd-627">Par conséquent, les statistiques hello retournés par cette API peut ne pas reflètent modifications dû à des opérations d’indexation récentes.</span><span class="sxs-lookup"><span data-stu-id="3fffd-627">Therefore, hello statistics returned by this API may not reflect changes caused by recent indexing operations.</span></span>
> 
> 

<span data-ttu-id="3fffd-628">**Requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-628">**Request**</span></span>

<span data-ttu-id="3fffd-629">Le protocole HTTPS est requis pour toutes les requêtes de services.</span><span class="sxs-lookup"><span data-stu-id="3fffd-629">HTTPS is required for all services requests.</span></span> <span data-ttu-id="3fffd-630">Hello **obtenir des statistiques d’Index** demande peut être construite à l’aide de la méthode GET de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-630">hello **Get Index Statistics** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="3fffd-631">Bonjour [nom de l’index] dans l’URI de la demande hello indique hello service tooreturn des statistiques d’index pour l’index spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-631">hello [index name] in hello request URI tells hello service tooreturn index statistics for hello specified index.</span></span>

<span data-ttu-id="3fffd-632">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="3fffd-632">`api-version=[string]` (required).</span></span> <span data-ttu-id="3fffd-633">version d’évaluation Hello `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-633">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3fffd-634">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3fffd-634">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3fffd-635">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-635">**Request Headers**</span></span>

<span data-ttu-id="3fffd-636">Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.</span><span class="sxs-lookup"><span data-stu-id="3fffd-636">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3fffd-637">`api-key`: hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-637">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3fffd-638">Il s’agit d’une valeur de chaîne, d’un service de tooyour unique.</span><span class="sxs-lookup"><span data-stu-id="3fffd-638">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="3fffd-639">Hello **obtenir des statistiques d’Index** demande doit inclure un `api-key` clé d’administration tooan ensemble (en tant que clé de requête tooa exécutée).</span><span class="sxs-lookup"><span data-stu-id="3fffd-639">hello **Get Index Statistics** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="3fffd-640">Vous devez également les URL de demande du nom tooconstruct hello hello service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-640">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3fffd-641">Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3fffd-641">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3fffd-642">Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.</span><span class="sxs-lookup"><span data-stu-id="3fffd-642">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3fffd-643">**Corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-643">**Request Body**</span></span>

<span data-ttu-id="3fffd-644">Aucune.</span><span class="sxs-lookup"><span data-stu-id="3fffd-644">None.</span></span>

<span data-ttu-id="3fffd-645">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="3fffd-645">**Response**</span></span>

<span data-ttu-id="3fffd-646">Code d'état : 200 OK est retourné pour une réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="3fffd-646">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="3fffd-647">corps de réponse Hello est Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="3fffd-647">hello response body is in hello following format:</span></span>

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a><span data-ttu-id="3fffd-648">Tester l’analyseur</span><span class="sxs-lookup"><span data-stu-id="3fffd-648">Test Analyzer</span></span>
<span data-ttu-id="3fffd-649">Hello **analyser les API** montre comment un analyseur découpe le texte en jetons.</span><span class="sxs-lookup"><span data-stu-id="3fffd-649">hello **Analyze API** shows how an analyzer breaks text into tokens.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="3fffd-650">**Requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-650">**Request**</span></span>

<span data-ttu-id="3fffd-651">Le protocole HTTPS est requis pour toutes les requêtes de services.</span><span class="sxs-lookup"><span data-stu-id="3fffd-651">HTTPS is required for all services requests.</span></span> <span data-ttu-id="3fffd-652">Hello **analyser les API** demande peut être construite à l’aide de la méthode POST de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-652">hello **Analyze API** request can be constructed using hello POST method.</span></span>

<span data-ttu-id="3fffd-653">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="3fffd-653">`api-version=[string]` (required).</span></span> <span data-ttu-id="3fffd-654">version d’évaluation Hello `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-654">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3fffd-655">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3fffd-655">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3fffd-656">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-656">**Request Headers**</span></span>

<span data-ttu-id="3fffd-657">Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.</span><span class="sxs-lookup"><span data-stu-id="3fffd-657">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3fffd-658">`api-key`: hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-658">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3fffd-659">Il s’agit d’une valeur de chaîne, d’un service de tooyour unique.</span><span class="sxs-lookup"><span data-stu-id="3fffd-659">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="3fffd-660">Hello **analyser les API** demande doit inclure un `api-key` clé d’administration tooan ensemble (en tant que clé de requête tooa exécutée).</span><span class="sxs-lookup"><span data-stu-id="3fffd-660">hello **Analyze API** request must include an `api-key` set tooan admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="3fffd-661">Vous devez également nom de l’index hello et URL de demande du nom tooconstruct hello hello service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-661">You will also need hello index name and hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3fffd-662">Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3fffd-662">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3fffd-663">Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.</span><span class="sxs-lookup"><span data-stu-id="3fffd-663">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3fffd-664">**Corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-664">**Request Body**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

<span data-ttu-id="3fffd-665">ou</span><span class="sxs-lookup"><span data-stu-id="3fffd-665">or</span></span>

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

<span data-ttu-id="3fffd-666">Hello `analyzer_name`, `tokenizer_name`, `token_filter_name` et `char_filter_name` que les noms valides de toobe d’analyseurs prédéfinies ou personnalisées, générateurs de jetons, filtres de jeton et char pour les index de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-666">hello `analyzer_name`, `tokenizer_name`, `token_filter_name` and `char_filter_name` need toobe valid names of predefined or custom analyzers, tokenizers, token filters and char filters for hello index.</span></span> <span data-ttu-id="3fffd-667">toolearn d’informations sur les processus hello de l’analyse lexicale, consultez [Analysis dans Azure Search](https://aka.ms/azsanalysis).</span><span class="sxs-lookup"><span data-stu-id="3fffd-667">toolearn more about hello process of lexical analysis see [Analysis in Azure Search](https://aka.ms/azsanalysis).</span></span>

<span data-ttu-id="3fffd-668">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="3fffd-668">**Response**</span></span>

<span data-ttu-id="3fffd-669">Code d'état : 200 OK est retourné pour une réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="3fffd-669">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="3fffd-670">corps de réponse Hello est Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="3fffd-670">hello response body is in hello following format:</span></span>

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

<span data-ttu-id="3fffd-671">**Exemple d’API Analyser**</span><span class="sxs-lookup"><span data-stu-id="3fffd-671">**Analyze API example**</span></span>

<span data-ttu-id="3fffd-672">**Requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-672">**Request**</span></span>

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

<span data-ttu-id="3fffd-673">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="3fffd-673">**Response**</span></span>

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

## <a name="document-operations"></a><span data-ttu-id="3fffd-674">Opérations de document</span><span class="sxs-lookup"><span data-stu-id="3fffd-674">Document Operations</span></span>
<span data-ttu-id="3fffd-675">Dans Azure Search, un index est stocké dans le cloud de hello et remplis à l’aide de documents JSON que vous téléchargez toohello service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-675">In Azure Search, an index is stored in hello cloud and populated using JSON documents that you upload toohello service.</span></span> <span data-ttu-id="3fffd-676">Tous les documents hello que vous chargez comprennent le corpus de hello de vos données de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-676">All hello documents that you upload comprise hello corpus of your search data.</span></span> <span data-ttu-id="3fffd-677">Les documents contiennent des champs, dont certains sont tokenisés dans les termes de recherche à mesure qu'ils sont téléchargés.</span><span class="sxs-lookup"><span data-stu-id="3fffd-677">Documents contain fields, some of which are tokenized into search terms as they are uploaded.</span></span> <span data-ttu-id="3fffd-678">Hello `/docs` segment d’URL Bonjour API Azure Search représente la collection de hello de documents dans un index.</span><span class="sxs-lookup"><span data-stu-id="3fffd-678">hello `/docs` URL segment in hello Azure Search API represents hello collection of documents in an index.</span></span> <span data-ttu-id="3fffd-679">Toutes les opérations effectuées sur le regroupement de hello telles que le téléchargement, la fusion, la suppression ou l’interrogation de documents prendre place dans le contexte de hello d’un index unique, c’est le cas hello URL pour que ces opérations commencent toujours par `/indexes/[index name]/docs` pour un nom de l’index donné.</span><span class="sxs-lookup"><span data-stu-id="3fffd-679">All operations performed on hello collection such as uploading, merging, deleting, or querying documents take place in hello context of a single index, so hello URLs for these operations will always start with `/indexes/[index name]/docs` for a given index name.</span></span>

<span data-ttu-id="3fffd-680">Code de votre application doit générer JSON documents tooupload tooAzure recherche ou vous pouvez utiliser un [indexeur](https://msdn.microsoft.com/library/dn946891.aspx) tooload documents si la source de données hello est la base de données SQL Azure ou base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="3fffd-680">Your application code must either generate JSON documents tooupload tooAzure Search or you can use an [indexer](https://msdn.microsoft.com/library/dn946891.aspx) tooload documents if hello data source is either Azure SQL Database or Azure Cosmos DB.</span></span> <span data-ttu-id="3fffd-681">En règle générale, les index sont remplis à partir d'un jeu de données unique que vous fournissez.</span><span class="sxs-lookup"><span data-stu-id="3fffd-681">Typically, indexes are populated from a single dataset that you provide.</span></span>

<span data-ttu-id="3fffd-682">Vous devez prévoir un document pour chaque élément que vous souhaitez toosearch.</span><span class="sxs-lookup"><span data-stu-id="3fffd-682">You should plan on having one document for each item that you want toosearch.</span></span> <span data-ttu-id="3fffd-683">Une application de location de films peut avoir un document par film, une application vitrine peut avoir un document par référence, une application de formation en ligne peut avoir un document par cours, un cabinet de recherche peut avoir un document pour chaque document académique de son référentiel, etc.</span><span class="sxs-lookup"><span data-stu-id="3fffd-683">A movie rental application might have one document per movie, a storefront application might have one document per SKU, an online courseware application might have one document per course, a research firm might have one document for each academic paper in their repository, and so on.</span></span>

<span data-ttu-id="3fffd-684">Les documents sont constitués d'un ou de plusieurs champs.</span><span class="sxs-lookup"><span data-stu-id="3fffd-684">Documents consist of one or more fields.</span></span> <span data-ttu-id="3fffd-685">Les champs peuvent contenir du texte tokenisé par Azure Search dans des termes de recherche, ainsi que des valeurs non tokenisées ou non textuelles pouvant être utilisées dans des filtres ou des profils de calcul de score.</span><span class="sxs-lookup"><span data-stu-id="3fffd-685">Fields can contain text that is tokenized by Azure Search into search terms, as well as non-tokenized or non-text values that can be used in filters or scoring profiles.</span></span> <span data-ttu-id="3fffd-686">Hello noms, types de données et les fonctionnalités de recherche pris en charge pour chaque champ sont déterminées par le schéma d’index hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-686">hello names, data types, and search features supported for each field are determined by hello index schema.</span></span> <span data-ttu-id="3fffd-687">Un des champs hello dans chaque schéma d’index doit être désigné en tant qu’ID, et chaque document doit avoir une valeur pour le champ hello ID qui identifie de façon unique ce document dans l’index de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-687">One of hello fields in each index schema must be designated as an ID, and each document must have a value for hello ID field that uniquely identifies that document in hello index.</span></span> <span data-ttu-id="3fffd-688">Tous les autres champs de document sont facultatifs et par défaut tooa les valeur null si non définie.</span><span class="sxs-lookup"><span data-stu-id="3fffd-688">All other document fields are optional and will default tooa null value if left unspecified.</span></span> <span data-ttu-id="3fffd-689">Notez que les valeurs null n’occupent pas d’espace dans les index de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-689">Note that null values do not take up space in hello search index.</span></span>

<span data-ttu-id="3fffd-690">Avant de pouvoir télécharger des documents, vous devez avoir déjà créé les index hello sur le service de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-690">Before you can upload documents, you must have already created hello index on hello service.</span></span> <span data-ttu-id="3fffd-691">Consultez la section [Création d'index](#CreateIndex) pour plus d'informations sur cette première étape.</span><span class="sxs-lookup"><span data-stu-id="3fffd-691">See [Create Index](#CreateIndex) for details about this first step.</span></span>

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a><span data-ttu-id="3fffd-692">Ajout, mise à jour ou suppression de documents</span><span class="sxs-lookup"><span data-stu-id="3fffd-692">Add, Update, or Delete Documents</span></span>
<span data-ttu-id="3fffd-693">Vous pouvez télécharger, fusionner, fusionner-ou-télécharger ou supprimer des documents à partir d'un index spécifié à l'aide de la requête HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="3fffd-693">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span> <span data-ttu-id="3fffd-694">Pour un grand nombre de mises à jour, le traitement par lot des documents (too1000 documents par lot) ou 16 Mo par lot est recommandé.</span><span class="sxs-lookup"><span data-stu-id="3fffd-694">For large numbers of updates, batching of documents (up too1000 documents per batch or about 16 MB per batch) is recommended.</span></span>

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

<span data-ttu-id="3fffd-695">**Requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-695">**Request**</span></span>

<span data-ttu-id="3fffd-696">Le protocole HTTPS est requis pour toutes les requêtes de service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-696">HTTPS is required for all service requests.</span></span> <span data-ttu-id="3fffd-697">Vous pouvez télécharger, fusionner, fusionner-ou-télécharger ou supprimer des documents à partir d'un index spécifié à l'aide de la requête HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="3fffd-697">You can upload, merge, merge-or-upload or delete documents from a specified index using HTTP POST.</span></span>

<span data-ttu-id="3fffd-698">Hello URI de requête inclut [nom de l’index], en spécifiant les index des documents toopost.</span><span class="sxs-lookup"><span data-stu-id="3fffd-698">hello request URI includes [index name], specifying which index toopost documents.</span></span> <span data-ttu-id="3fffd-699">Vous ne pouvez valider que les index de tooone de documents à la fois.</span><span class="sxs-lookup"><span data-stu-id="3fffd-699">You can only post documents tooone index at a time.</span></span>

<span data-ttu-id="3fffd-700">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="3fffd-700">`api-version=[string]` (required).</span></span> <span data-ttu-id="3fffd-701">version d’évaluation Hello `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-701">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3fffd-702">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3fffd-702">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3fffd-703">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-703">**Request Headers**</span></span>

<span data-ttu-id="3fffd-704">Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.</span><span class="sxs-lookup"><span data-stu-id="3fffd-704">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3fffd-705">`Content-Type`: requis.</span><span class="sxs-lookup"><span data-stu-id="3fffd-705">`Content-Type`: Required.</span></span> <span data-ttu-id="3fffd-706">Définissez cette propriété trop`application/json`</span><span class="sxs-lookup"><span data-stu-id="3fffd-706">Set this too`application/json`</span></span>
* <span data-ttu-id="3fffd-707">`api-key`: obligatoire.</span><span class="sxs-lookup"><span data-stu-id="3fffd-707">`api-key`: Required.</span></span> <span data-ttu-id="3fffd-708">Hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-708">hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3fffd-709">Il s’agit d’une valeur de chaîne, d’un service de tooyour unique.</span><span class="sxs-lookup"><span data-stu-id="3fffd-709">It is a string value, unique tooyour service.</span></span> <span data-ttu-id="3fffd-710">Hello **ajouter des Documents** demande doit inclure un `api-key` en-tête défini la clé d’administration tooyour (en tant que clé de requête tooa exécutée).</span><span class="sxs-lookup"><span data-stu-id="3fffd-710">hello **Add Documents** request must include an `api-key` header set tooyour admin key (as opposed tooa query key).</span></span>

<span data-ttu-id="3fffd-711">Vous devez également les URL de demande du nom tooconstruct hello hello service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-711">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3fffd-712">Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3fffd-712">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3fffd-713">Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.</span><span class="sxs-lookup"><span data-stu-id="3fffd-713">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3fffd-714">**Corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-714">**Request Body**</span></span>

<span data-ttu-id="3fffd-715">corps Hello de demande de hello contient un ou plusieurs documents toobe indexé.</span><span class="sxs-lookup"><span data-stu-id="3fffd-715">hello body of hello request contains one or more documents toobe indexed.</span></span> <span data-ttu-id="3fffd-716">Les documents sont identifiés par une clé unique.</span><span class="sxs-lookup"><span data-stu-id="3fffd-716">Documents are identified by a unique key.</span></span> <span data-ttu-id="3fffd-717">Chaque document est associé à une action : upload, merge, mergeOrUpload ou delete.</span><span class="sxs-lookup"><span data-stu-id="3fffd-717">Each document is associated with an action: upload, merge, mergeOrUpload or delete.</span></span> <span data-ttu-id="3fffd-718">Demande de téléchargement doit inclure les données du document hello comme un ensemble de paires clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="3fffd-718">Upload requests must include hello document data as a set of key/value pairs.</span></span>

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
> <span data-ttu-id="3fffd-719">Les clés de document ne peuvent contenir que des lettres, des chiffres, des tirets (« - »), des traits de soulignement (« _ ») et les signes égal (« = »).</span><span class="sxs-lookup"><span data-stu-id="3fffd-719">Document keys can only contain letters, numbers, dashes ("-"), underscores ("_"), and equal signs ("=").</span></span> <span data-ttu-id="3fffd-720">Pour plus d’informations, consultez les [Règles d’affectation des noms](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span><span class="sxs-lookup"><span data-stu-id="3fffd-720">For more details, see [Naming rules](https://msdn.microsoft.com/library/azure/dn857353.aspx).</span></span>
> 
> 

<span data-ttu-id="3fffd-721">**Actions de document**</span><span class="sxs-lookup"><span data-stu-id="3fffd-721">**Document Actions**</span></span>

* <span data-ttu-id="3fffd-722">`upload`: Une action de chargement est similaire tooan « upsert » où le document de hello sera inséré s’il est nouveau et mis à jour/remplacé s’il existe.</span><span class="sxs-lookup"><span data-stu-id="3fffd-722">`upload`: An upload action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> <span data-ttu-id="3fffd-723">Notez que tous les champs sont remplacés en cas de mise à jour hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-723">Note that all fields are replaced in hello update case.</span></span>
* <span data-ttu-id="3fffd-724">`merge`: Mises à jour fusion existant de document avec hello spécifié des champs.</span><span class="sxs-lookup"><span data-stu-id="3fffd-724">`merge`: Merge updates an existing document with hello specified fields.</span></span> <span data-ttu-id="3fffd-725">Si le document de hello n’existe pas, la fusion de hello échoue.</span><span class="sxs-lookup"><span data-stu-id="3fffd-725">If hello document doesn't exist, hello merge will fail.</span></span> <span data-ttu-id="3fffd-726">N’importe quel champ que vous spécifiez dans une fusion remplace le champ existant de hello dans le document de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-726">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="3fffd-727">Cela inclut les champs de type `Collection(Edm.String)`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-727">This includes fields of type `Collection(Edm.String)`.</span></span> <span data-ttu-id="3fffd-728">Par exemple, si hello document contient un champ « indicateurs » avec la valeur `["budget"]` et que vous exécutez une fusion avec la valeur `["economy", "pool"]` pour « balises », hello dernière valeur de champ hello « balises » sera `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-728">For example, if hello document contains a field "tags" with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for "tags", hello final value of hello "tags" field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="3fffd-729">Elle ne doit **pas** être `["budget", "economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-729">It will **not** be `["budget", "economy", "pool"]`.</span></span>
* <span data-ttu-id="3fffd-730">`mergeOrUpload`: se comporte comme `merge` si un document avec hello donné clé déjà existe dans les index hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-730">`mergeOrUpload`: behaves like `merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="3fffd-731">Si le document de hello n’existe pas qu’il se comporte comme `upload` avec un nouveau document.</span><span class="sxs-lookup"><span data-stu-id="3fffd-731">If hello document does not exist it behaves like `upload` with a new document.</span></span>
* <span data-ttu-id="3fffd-732">`delete`: Delete Supprime document spécifié de hello à partir de l’index de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-732">`delete`: Delete removes hello specified document from hello index.</span></span> <span data-ttu-id="3fffd-733">Notez que tous les champs que vous spécifiez dans un `delete` opération autre que du champ de clé hello sera ignorée.</span><span class="sxs-lookup"><span data-stu-id="3fffd-733">Note that any fields you specify in a `delete` operation other than hello key field will be ignored.</span></span> <span data-ttu-id="3fffd-734">Si vous souhaitez tooremove un champ individuel à partir d’un document, utilisez `merge` à la place et simplement définir hello champ explicitement trop`null`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-734">If you want tooremove an individual field from a document, use `merge` instead and simply set hello field explicitly too`null`.</span></span>

<span data-ttu-id="3fffd-735">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="3fffd-735">**Response**</span></span>

<span data-ttu-id="3fffd-736">Code d’état : 200 (OK) est retourné pour une réponse correcte, ce qui signifie que tous les éléments ont été indexés.</span><span class="sxs-lookup"><span data-stu-id="3fffd-736">Status code 200 (OK) is returned for a successful response, meaning that all items have been successfully indexed.</span></span> <span data-ttu-id="3fffd-737">Cela est indiqué par hello `status` propriété définie tootrue pour tous les éléments, ainsi que les hello `statusCode` propriété définie tooeither 201 (pour les documents qui vient d’être téléchargés) ou 200 (pour les documents fusionnés ou supprimés) :</span><span class="sxs-lookup"><span data-stu-id="3fffd-737">This is indicated by hello `status` property being set tootrue for all items, as well as hello `statusCode` property being set tooeither 201 (for newly uploaded documents) or 200 (for merged or deleted documents):</span></span>

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

<span data-ttu-id="3fffd-738">Un code d’état 207 (Multi-état) est renvoyé lorsqu’au moins un élément n’a pas été correctement indexé.</span><span class="sxs-lookup"><span data-stu-id="3fffd-738">Status code 207 (Multi-Status) is returned when at least one item was not successfully indexed.</span></span> <span data-ttu-id="3fffd-739">Les éléments qui n’ont pas été indexées ont hello `status` toofalse ensemble de champs.</span><span class="sxs-lookup"><span data-stu-id="3fffd-739">Items that have not been indexed have hello `status` field set toofalse.</span></span> <span data-ttu-id="3fffd-740">Hello `errorMessage` et `statusCode` propriétés indique la raison de hello hello erreur d’indexation :</span><span class="sxs-lookup"><span data-stu-id="3fffd-740">hello `errorMessage` and `statusCode` properties will indicate hello reason for hello indexing error:</span></span>

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
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
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

<span data-ttu-id="3fffd-741">Hello tableau suivant explique hello différentes par document codes d’état qui peuvent être retournées dans la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-741">hello following table explains hello various per-document status codes that can be returned in hello response.</span></span> <span data-ttu-id="3fffd-742">Notez que certains indiquent des problèmes avec la demande hello elle-même, alors que d’autres conditions d’erreur temporaire.</span><span class="sxs-lookup"><span data-stu-id="3fffd-742">Note that some indicate problems with hello request itself, while others indicate temporary error conditions.</span></span> <span data-ttu-id="3fffd-743">Hello ce dernier que vous devriez réessayer après un certain délai.</span><span class="sxs-lookup"><span data-stu-id="3fffd-743">hello latter you should retry after a delay.</span></span>

<table style="font-size:12">
    <tr>
        <th><span data-ttu-id="3fffd-744">Code d’état</span><span class="sxs-lookup"><span data-stu-id="3fffd-744">Status code</span></span></th>
        <th><span data-ttu-id="3fffd-745">Signification</span><span class="sxs-lookup"><span data-stu-id="3fffd-745">Meaning</span></span></th>
        <th><span data-ttu-id="3fffd-746">Nouvelle tentative possible</span><span class="sxs-lookup"><span data-stu-id="3fffd-746">Retryable</span></span></th>
        <th><span data-ttu-id="3fffd-747">Remarques</span><span class="sxs-lookup"><span data-stu-id="3fffd-747">Notes</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-748">200</span><span class="sxs-lookup"><span data-stu-id="3fffd-748">200</span></span></td>
        <td><span data-ttu-id="3fffd-749">Le document a été correctement modifié ou supprimé.</span><span class="sxs-lookup"><span data-stu-id="3fffd-749">Document was successfully modified or deleted.</span></span></td>
        <td><span data-ttu-id="3fffd-750">n/a</span><span class="sxs-lookup"><span data-stu-id="3fffd-750">n/a</span></span></td>
        <td><span data-ttu-id="3fffd-751">Les opérations de suppression sont <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentes</a>.</span><span class="sxs-lookup"><span data-stu-id="3fffd-751">Delete operations are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span> <span data-ttu-id="3fffd-752">Autrement dit, même si une clé de document n’existe pas dans l’index de hello, essayez d’une opération de suppression avec cette clé entraîne un code de 200 état.</span><span class="sxs-lookup"><span data-stu-id="3fffd-752">That is, even if a document key does not exist in hello index, attempting a delete operation with that key will result in a 200 status code.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-753">201</span><span class="sxs-lookup"><span data-stu-id="3fffd-753">201</span></span></td>
        <td><span data-ttu-id="3fffd-754">Le document a été créé avec succès.</span><span class="sxs-lookup"><span data-stu-id="3fffd-754">Document was successfully created.</span></span></td>
        <td><span data-ttu-id="3fffd-755">n/a</span><span class="sxs-lookup"><span data-stu-id="3fffd-755">n/a</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-756">400</span><span class="sxs-lookup"><span data-stu-id="3fffd-756">400</span></span></td>
        <td><span data-ttu-id="3fffd-757">Une erreur s’est produite dans le document hello qui l’a empêché d’en cours d’indexation.</span><span class="sxs-lookup"><span data-stu-id="3fffd-757">There was an error in hello document that prevented it from being indexed.</span></span></td>
        <td><span data-ttu-id="3fffd-758">Non</span><span class="sxs-lookup"><span data-stu-id="3fffd-758">No</span></span></td>
        <td><span data-ttu-id="3fffd-759">message d’erreur Hello en réponse de hello indique quel est le problème avec le document de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-759">hello error message in hello response will indicate what is wrong with hello document.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-760">404</span><span class="sxs-lookup"><span data-stu-id="3fffd-760">404</span></span></td>
        <td><span data-ttu-id="3fffd-761">Impossible de fusionner les documents Hello hello clé n’existe pas dans les index hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-761">hello document could not be merged because hello given key doesn't exist in hello index.</span></span></td>
        <td><span data-ttu-id="3fffd-762">Non</span><span class="sxs-lookup"><span data-stu-id="3fffd-762">No</span></span></td>
        <td><span data-ttu-id="3fffd-763">Cette erreur ne s’applique pas aux téléchargements dans la mesure où ils créent de nouveaux documents, de même qu’elle ne se produit pas pour les suppressions, car elles sont <a href="https://en.wikipedia.org/wiki/Idempotence">idempotentes</a>.</span><span class="sxs-lookup"><span data-stu-id="3fffd-763">This error does not occur for uploads since they create new documents, and it does not occur for deletes because they are <a href="https://en.wikipedia.org/wiki/Idempotence">idempotent</a>.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-764">409</span><span class="sxs-lookup"><span data-stu-id="3fffd-764">409</span></span></td>
        <td><span data-ttu-id="3fffd-765">Un conflit de version a été détecté lors de la tentative de tooindex un document.</span><span class="sxs-lookup"><span data-stu-id="3fffd-765">A version conflict was detected when attempting tooindex a document.</span></span></td>
        <td><span data-ttu-id="3fffd-766">Oui</span><span class="sxs-lookup"><span data-stu-id="3fffd-766">Yes</span></span></td>
        <td><span data-ttu-id="3fffd-767">Cela peut se produire quand vous essayez de hello tooindex même document plusieurs fois simultanément.</span><span class="sxs-lookup"><span data-stu-id="3fffd-767">This can happen when you're trying tooindex hello same document more than once concurrently.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-768">422</span><span class="sxs-lookup"><span data-stu-id="3fffd-768">422</span></span></td>
        <td><span data-ttu-id="3fffd-769">index de Hello est temporairement indisponible, car il a été mis à jour avec hello 'allowIndexDowntime' indicateur ensemble too'true'.</span><span class="sxs-lookup"><span data-stu-id="3fffd-769">hello index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'.</span></span></td>
        <td><span data-ttu-id="3fffd-770">Oui</span><span class="sxs-lookup"><span data-stu-id="3fffd-770">Yes</span></span></td>
        <td></td>
    </tr>
    <tr>
        <td><span data-ttu-id="3fffd-771">503</span><span class="sxs-lookup"><span data-stu-id="3fffd-771">503</span></span></td>
        <td><span data-ttu-id="3fffd-772">Votre service de recherche est temporairement indisponible, probablement en raison de la charge de tooheavy.</span><span class="sxs-lookup"><span data-stu-id="3fffd-772">Your search service is temporarily unavailable, possibly due tooheavy load.</span></span></td>
        <td><span data-ttu-id="3fffd-773">Oui</span><span class="sxs-lookup"><span data-stu-id="3fffd-773">Yes</span></span></td>
        <td><span data-ttu-id="3fffd-774">Votre code doit attendre avant de réessayer dans ce cas, ou vous risquez de prolonger l’indisponibilité de service hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-774">Your code should wait before retrying in this case or you risk prolonging hello service unavailability.</span></span></td>
    </tr>
</table> 

<span data-ttu-id="3fffd-775">**Remarque**: Si votre code client rencontre fréquemment une réponse 207, due au fait que le système de hello est sous charge.</span><span class="sxs-lookup"><span data-stu-id="3fffd-775">**Note**: If your client code frequently encounters a 207 response, one possible reason is that hello system is under load.</span></span> <span data-ttu-id="3fffd-776">Vous pouvez le vérifier en vérifiant hello `statusCode` propriété 503.</span><span class="sxs-lookup"><span data-stu-id="3fffd-776">You can confirm this by checking hello `statusCode` property for 503.</span></span> <span data-ttu-id="3fffd-777">Si cela est le cas de hello, nous vous recommandons de ***la limitation des demandes d’indexation***.</span><span class="sxs-lookup"><span data-stu-id="3fffd-777">If this is hello case, we recommend ***throttling indexing requests***.</span></span> <span data-ttu-id="3fffd-778">Sinon, si le trafic d’indexation ne diminue pas, système de hello pourrait commencer à rejeter toutes les demandes avec des 503 erreurs.</span><span class="sxs-lookup"><span data-stu-id="3fffd-778">Otherwise, if indexing traffic doesn't subside, hello system could start rejecting all requests with 503 errors.</span></span>

<span data-ttu-id="3fffd-779">Code d’état 429 indique que vous avez dépassé votre quota de nombre hello de documents par index.</span><span class="sxs-lookup"><span data-stu-id="3fffd-779">Status code 429 indicates that you have exceeded your quota on hello number of documents per index.</span></span> <span data-ttu-id="3fffd-780">Vous devez créer un autre index ou effectuer une mise à niveau pour bénéficier de limites de capacité supérieures.</span><span class="sxs-lookup"><span data-stu-id="3fffd-780">You must either create a new index or upgrade for higher capacity limits.</span></span>

<span data-ttu-id="3fffd-781">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="3fffd-781">**Example:**</span></span>

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

## <a name="search-documents"></a><span data-ttu-id="3fffd-782">Search Documents</span><span class="sxs-lookup"><span data-stu-id="3fffd-782">Search Documents</span></span>
<span data-ttu-id="3fffd-783">A **recherche** opération s’affiche comme une demande GET ou POST et spécifie les paramètres qui contiennent des critères de hello pour la sélection des documents correspondants.</span><span class="sxs-lookup"><span data-stu-id="3fffd-783">A **Search** operation is issued as a GET or POST request and specifies parameters that give hello criteria for selecting matching documents.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="3fffd-784">**Lorsque toouse VALIDEZ au lieu de GET**</span><span class="sxs-lookup"><span data-stu-id="3fffd-784">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="3fffd-785">Lorsque vous utilisez HTTP GET les hello toocall **recherche** API, vous devez toobe conscient que hello hello URL de demande ne peut pas dépasser 8 Ko.</span><span class="sxs-lookup"><span data-stu-id="3fffd-785">When you use HTTP GET toocall hello **Search** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="3fffd-786">Cela est généralement suffisamment pour la plupart des applications.</span><span class="sxs-lookup"><span data-stu-id="3fffd-786">This is usually enough for most applications.</span></span> <span data-ttu-id="3fffd-787">Toutefois, certaines applications produisent des requêtes très volumineuses ou des expressions de filtre OData.</span><span class="sxs-lookup"><span data-stu-id="3fffd-787">However, some applications produce very large queries or OData filter expressions.</span></span> <span data-ttu-id="3fffd-788">Pour ces applications, il est recommandé d'utiliser HTTP POST, car cela permet d'obtenir des filtres et des requêtes plus volumineux que GET.</span><span class="sxs-lookup"><span data-stu-id="3fffd-788">For these applications, using HTTP POST is a better choice because it allows larger filters and queries than GET.</span></span> <span data-ttu-id="3fffd-789">Avec POST, nombre hello des clauses dans une requête hello limitent facteur, la taille de hello pas des requêtes brutes de hello, car la limite de taille de demande de hello POST est d’environ 16 Mo.</span><span class="sxs-lookup"><span data-stu-id="3fffd-789">With POST, hello number of terms or clauses in a query is hello limiting factor, not hello size of hello raw query since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="3fffd-790">Bien que la limite de taille de demande POST hello est très important, les requêtes de recherche et les expressions de filtre ne peut pas être arbitrairement complexes.</span><span class="sxs-lookup"><span data-stu-id="3fffd-790">Even though hello POST request size limit is very large, search queries and filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="3fffd-791">Consultez [Syntaxe de requête Lucene](https://msdn.microsoft.com/library/mt589323.aspx) et [Syntaxe d’expression OData](https://msdn.microsoft.com/library/dn798921.aspx) pour plus d’informations sur les limites de la complexité des filtres et des requêtes de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-791">See [Lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx) and [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about search query and filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="3fffd-792">**Requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-792">**Request**</span></span>

<span data-ttu-id="3fffd-793">Le protocole HTTPS est requis pour les requêtes de service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-793">HTTPS is required for service requests.</span></span> <span data-ttu-id="3fffd-794">Hello **recherche** demande peut être construite à l’aide de hello GET ou la méthode POST.</span><span class="sxs-lookup"><span data-stu-id="3fffd-794">hello **Search** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="3fffd-795">URI de demande Hello spécifie quels index tooquery, pour tous les documents qui correspondent aux paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-795">hello request URI specifies which index tooquery, for all documents that match hello parameters.</span></span> <span data-ttu-id="3fffd-796">Paramètres sont spécifiés dans la chaîne de requête hello dans les cas de hello de demandes GET, et dans la demande hello corps dans les cas de hello de demande.</span><span class="sxs-lookup"><span data-stu-id="3fffd-796">Parameters are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="3fffd-797">Comme meilleure pratique lors de la création de demandes GET, n’oubliez pas trop[encoder en URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) paramètres lors de l’appel hello directement les API REST de requête spécifique.</span><span class="sxs-lookup"><span data-stu-id="3fffd-797">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="3fffd-798">Pour les opérations de **recherche** , cela inclut :</span><span class="sxs-lookup"><span data-stu-id="3fffd-798">For **Search** operations, this includes:</span></span>

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

<span data-ttu-id="3fffd-799">L’encodage d’URL est recommandée uniquement sur hello au-dessus de paramètres de requête.</span><span class="sxs-lookup"><span data-stu-id="3fffd-799">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="3fffd-800">Si vous par inadvertance encoder en URL hello la chaîne de requête entière (tout ce qui suit hello ?), les demandes s’interrompent.</span><span class="sxs-lookup"><span data-stu-id="3fffd-800">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="3fffd-801">En outre, l’encodage d’URL est nécessaire uniquement lors de l’appel hello obtenir de l’API REST directement à l’aide.</span><span class="sxs-lookup"><span data-stu-id="3fffd-801">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="3fffd-802">Aucun encodage d’URL n’est nécessaire lors de l’appel **recherche** à l’aide de POST, ou lorsque vous utilisez hello [bibliothèque cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx), qui gère l’encodage d’URL pour vous.</span><span class="sxs-lookup"><span data-stu-id="3fffd-802">No URL encoding is necessary when calling **Search** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="3fffd-803"><a name="SearchQueryParameters"></a>
**Paramètres de requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-803"><a name="SearchQueryParameters"></a>
**Query Parameters**</span></span>

<span data-ttu-id="3fffd-804">**Search** accepte plusieurs paramètres qui fournissent les critères de la requête et qui spécifient également le comportement de la recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-804">**Search** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="3fffd-805">Vous fournissez ces paramètres dans l’URL de hello la chaîne de requête lors de l’appel **recherche** via GET et en tant que propriétés JSON dans le corps de la demande hello lors de l’appel **recherche** via la publication.</span><span class="sxs-lookup"><span data-stu-id="3fffd-805">You provide these parameters in hello URL query string when calling **Search** via GET, and as JSON properties in hello request body when calling **Search** via POST.</span></span> <span data-ttu-id="3fffd-806">syntaxe Hello pour certains paramètres est légèrement différente entre GET et POST.</span><span class="sxs-lookup"><span data-stu-id="3fffd-806">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="3fffd-807">Ces différences sont indiquées ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3fffd-807">These differences are noted as applicable below:</span></span>

<span data-ttu-id="3fffd-808">`search=[string]`(facultatif) : hello toosearch de texte pour.</span><span class="sxs-lookup"><span data-stu-id="3fffd-808">`search=[string]` (optional) - hello text toosearch for.</span></span> <span data-ttu-id="3fffd-809">Tous les champs `searchable` sont interrogés par défaut, sauf si `searchFields` est spécifié.</span><span class="sxs-lookup"><span data-stu-id="3fffd-809">All `searchable` fields are searched by default unless `searchFields` is specified.</span></span> <span data-ttu-id="3fffd-810">Lors de la recherche `searchable` champs, rechercher du texte hello lui-même est tokenisé plusieurs termes peuvent être séparés par un espace blanc (par exemple : `search=hello world`).</span><span class="sxs-lookup"><span data-stu-id="3fffd-810">When searching `searchable` fields, hello search text itself is tokenized, so multiple terms can be separated by white space (for example: `search=hello world`).</span></span> <span data-ttu-id="3fffd-811">utilisation de tout terme, toomatch `*` (qui peut être utile pour les requêtes de filtre booléen).</span><span class="sxs-lookup"><span data-stu-id="3fffd-811">toomatch any term, use `*` (this can be useful for boolean filter queries).</span></span> <span data-ttu-id="3fffd-812">L’omission de ce paramètre est hello même effet que sa définition trop`*`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-812">Omitting this parameter has hello same effect as setting it too`*`.</span></span> <span data-ttu-id="3fffd-813">Consultez [syntaxe de requête Simple](https://msdn.microsoft.com/library/dn798920.aspx) pour plus de détails sur la syntaxe de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-813">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) for specifics on hello search syntax.</span></span>

* <span data-ttu-id="3fffd-814">**Remarque**: hello résultats peuvent parfois être surprenant lors de l’interrogation sur `searchable` champs.</span><span class="sxs-lookup"><span data-stu-id="3fffd-814">**Note**: hello results can sometimes be surprising when querying over `searchable` fields.</span></span> <span data-ttu-id="3fffd-815">Générateur de jetons Hello inclut logique toohandle cas courants tooEnglish texte tels que les apostrophes, les virgules des nombres, etc.. Par exemple, `search=123,456` correspond à un terme 123,456 plutôt que des termes hello 123 et 456, étant donné que les virgules sont utilisées comme séparateurs de milliers de grands nombres en anglais.</span><span class="sxs-lookup"><span data-stu-id="3fffd-815">hello tokenizer includes logic toohandle cases common tooEnglish text like apostrophes, commas in numbers, etc. For example, `search=123,456` will match a single term 123,456 rather than hello individual terms 123 and 456, since commas are used as thousand-separators for large numbers in English.</span></span> <span data-ttu-id="3fffd-816">Pour cette raison, nous recommandons d’utiliser un espace blanc plutôt que des termes du contrat de ponctuation tooseparate Bonjour `search` paramètre.</span><span class="sxs-lookup"><span data-stu-id="3fffd-816">For this reason, we recommend using white space rather than punctuation tooseparate terms in hello `search` parameter.</span></span>

<span data-ttu-id="3fffd-817">`searchMode=any|all`(facultatif, par défaut est trop`any`) : indique si tout ou partie des termes de recherche hello doivent correspondre dans le document de hello toocount commande comme une correspondance.</span><span class="sxs-lookup"><span data-stu-id="3fffd-817">`searchMode=any|all` (optional, defaults too`any`) - whether any or all of hello search terms must be matched in order toocount hello document as a match.</span></span>

<span data-ttu-id="3fffd-818">`searchFields=[string]`(facultatif) : liste hello de toosearch de noms de champ séparées par des virgules pour hello le texte spécifié.</span><span class="sxs-lookup"><span data-stu-id="3fffd-818">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified text.</span></span> <span data-ttu-id="3fffd-819">Les champs cibles doivent être marqués comme `searchable`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-819">Target fields must be marked as `searchable`.</span></span>

<span data-ttu-id="3fffd-820">`queryType=simple|full`(facultatif, par défaut est trop`simple`) : lorsque le texte du jeu de recherche trop « simple » est interprété à l’aide d’un langage de requête simple qui permet des symboles, tels que +, * et « ».</span><span class="sxs-lookup"><span data-stu-id="3fffd-820">`queryType=simple|full` (optional, defaults too`simple`) - when set too"simple" search text is interpreted using a simple query language that allows for symbols such as +, * and "".</span></span> <span data-ttu-id="3fffd-821">Les requêtes sont évaluées pour tous les champs pouvant faire l’objet d’une recherche (ou les champs indiqués dans `searchFields`) dans chaque document par défaut.</span><span class="sxs-lookup"><span data-stu-id="3fffd-821">Queries are evaluated across all searchable fields (or fields indicated in `searchFields`) in each document by default.</span></span> <span data-ttu-id="3fffd-822">Lorsque le type de requête hello est défini trop`full` rechercher du texte est interprété à l’aide du langage de requête Lucene hello qui permet des recherches spécifiques aux champs et pondérées.</span><span class="sxs-lookup"><span data-stu-id="3fffd-822">When hello query type is set too`full` search text is interpreted using hello Lucene query language which allows field-specific and weighted searches.</span></span> <span data-ttu-id="3fffd-823">Consultez [syntaxe de requête Simple](https://msdn.microsoft.com/library/dn798920.aspx) et [syntaxe de requête Lucene](https://msdn.microsoft.com/library/mt589323.aspx) pour plus de détails sur les syntaxes de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-823">See [Simple Query Syntax](https://msdn.microsoft.com/library/dn798920.aspx) and [Lucene Query Syntax](https://msdn.microsoft.com/library/mt589323.aspx) for specifics on hello search syntaxes.</span></span> 

> [!NOTE]
> <span data-ttu-id="3fffd-824">Plage recherche Bonjour Lucene langage de requête n’est pas pris en charge en faveur $filter qui offre des fonctionnalités similaires.</span><span class="sxs-lookup"><span data-stu-id="3fffd-824">Range search in hello Lucene query language is not supported in favor of $filter which offers similar functionality.</span></span>
> 
> 

<span data-ttu-id="3fffd-825">`moreLikeThis=[key]` (facultatif) **Important :** cette fonctionnalité est uniquement disponible dans `2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-825">`moreLikeThis=[key]` (optional) **Important:** This feature is only available in `2015-02-28-Preview`.</span></span> <span data-ttu-id="3fffd-826">Cette option ne peut pas être utilisée dans une requête qui contient le paramètre de recherche de texte hello, `search=[string]`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-826">This option cannot be used in a query that contains hello text search parameter, `search=[string]`.</span></span> <span data-ttu-id="3fffd-827">Hello `moreLikeThis` paramètre trouve les documents qui sont similaires toohello document spécifié par la clé de document hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-827">hello `moreLikeThis` parameter finds documents that are similar toohello document specified by hello document key.</span></span> <span data-ttu-id="3fffd-828">Lorsqu’une demande de recherche est effectuée avec `moreLikeThis`, une liste de termes de recherche est générée en fonction de la fréquence de hello et rareté de termes dans le document d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-828">When a search request is made with `moreLikeThis`, a list of search terms is generated based on hello frequency and rarity of terms in hello source document.</span></span> <span data-ttu-id="3fffd-829">Ces termes sont utilisé toomake hello demande.</span><span class="sxs-lookup"><span data-stu-id="3fffd-829">Those terms are then used toomake hello request.</span></span> <span data-ttu-id="3fffd-830">Par défaut, hello le contenu de tous les `searchable` champs sont considérés comme sauf si `searchFields` est utilisé toorestrict des champs de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-830">By default, hello contents of all `searchable` fields are considered unless `searchFields` is used toorestrict which fields are searched.</span></span>  

<span data-ttu-id="3fffd-831">`$skip=#`(facultatif) : nombre de hello de recherche résultats tooskip ; Ne peut pas être supérieur à 100 000.</span><span class="sxs-lookup"><span data-stu-id="3fffd-831">`$skip=#` (optional) - hello number of search results tooskip; Cannot be greater than 100,000.</span></span> <span data-ttu-id="3fffd-832">Si vous devez tooscan des documents dans l’ordre, mais ne pouvez pas utiliser `$skip` en raison de la limitation de toothis, envisagez d’utiliser `$orderby` sur une clé totalement ordonnée et `$filter` avec une plage de requête à la place.</span><span class="sxs-lookup"><span data-stu-id="3fffd-832">If you need tooscan documents in sequence but cannot use `$skip` due toothis limitation, consider using `$orderby` on a totally-ordered key and `$filter` with a range query instead.</span></span>

> [!NOTE]
> <span data-ttu-id="3fffd-833">Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `skip` au lieu de `$skip`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-833">When calling **Search** using POST, this parameter is named `skip` instead of `$skip`.</span></span>
> 
> 

<span data-ttu-id="3fffd-834">`$top=#`(facultatif) : nombre de hello de recherche résultats tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="3fffd-834">`$top=#` (optional) - hello number of search results tooretrieve.</span></span> <span data-ttu-id="3fffd-835">Cela peut être utilisé conjointement avec `$skip` tooimplement une pagination côté client des résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-835">This can be used in conjunction with `$skip` tooimplement client-side paging of search results.</span></span>

> [!NOTE]
> <span data-ttu-id="3fffd-836">Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `top` au lieu de `$top`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-836">When calling **Search** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="3fffd-837">`$count=true|false`(facultatif, par défaut est trop`false`)-Spécifie si toofetch hello nombre total de résultats.</span><span class="sxs-lookup"><span data-stu-id="3fffd-837">`$count=true|false` (optional, defaults too`false`) - Specifies whether toofetch hello total count of results.</span></span> <span data-ttu-id="3fffd-838">Il s’agit nombre hello de tous les documents qui correspondent aux hello `search` et `$filter` paramètres, en ignorant `$top` et `$skip`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-838">This is hello count of all documents that match hello `search` and `$filter` parameters, ignoring `$top` and `$skip`.</span></span> <span data-ttu-id="3fffd-839">Ce paramètre trop`true` peut avoir un impact sur les performances.</span><span class="sxs-lookup"><span data-stu-id="3fffd-839">Setting this value too`true` may have a performance impact.</span></span> <span data-ttu-id="3fffd-840">Notez que le nombre de hello retourné est une approximation.</span><span class="sxs-lookup"><span data-stu-id="3fffd-840">Note that hello count returned is an approximation.</span></span>

> [!NOTE]
> <span data-ttu-id="3fffd-841">Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `count` au lieu de `$count`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-841">When calling **Search** using POST, this parameter is named `count` instead of `$count`.</span></span>
> 
> 

<span data-ttu-id="3fffd-842">`$orderby=[string]`(facultatif) : une liste de résultats de hello toosort séparées par des virgules des expressions par.</span><span class="sxs-lookup"><span data-stu-id="3fffd-842">`$orderby=[string]` (optional) - A list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="3fffd-843">Chaque expression peut être un nom de champ ou d’un appel toohello `geo.distance()` (fonction).</span><span class="sxs-lookup"><span data-stu-id="3fffd-843">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="3fffd-844">Chaque expression peut être suivie `asc` tooindicated par ordre croissant, et `desc` tooindicate décroissant.</span><span class="sxs-lookup"><span data-stu-id="3fffd-844">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="3fffd-845">valeur par défaut Hello est l’ordre croissant.</span><span class="sxs-lookup"><span data-stu-id="3fffd-845">hello default is ascending order.</span></span> <span data-ttu-id="3fffd-846">Les liens sont rompus par scores de correspondance hello de documents.</span><span class="sxs-lookup"><span data-stu-id="3fffd-846">Ties will be broken by hello match scores of documents.</span></span> <span data-ttu-id="3fffd-847">Si aucun `$orderby` est spécifié, l’ordre de tri par défaut hello décroissant par score de correspondance.</span><span class="sxs-lookup"><span data-stu-id="3fffd-847">If no `$orderby` is specified, hello default sort order is descending by document match score.</span></span> <span data-ttu-id="3fffd-848">Il existe une limite de 32 clauses pour `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-848">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="3fffd-849">Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `orderby` au lieu de `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-849">When calling **Search** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="3fffd-850">`$select=[string]`(facultatif) : une liste de champs séparés par des virgules tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="3fffd-850">`$select=[string]` (optional) - A list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="3fffd-851">Si non spécifié, tous les champs marqués comme récupérables dans le schéma de hello sont inclus.</span><span class="sxs-lookup"><span data-stu-id="3fffd-851">If unspecified, all fields marked as retrievable in hello schema are included.</span></span> <span data-ttu-id="3fffd-852">Vous pouvez également demander explicitement tous les champs en définissant ce paramètre trop`*`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-852">You can also explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="3fffd-853">Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `select` au lieu de `$select`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-853">When calling **Search** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="3fffd-854">`facet=[string]`(zéro ou plus) - un toofacet de champ par.</span><span class="sxs-lookup"><span data-stu-id="3fffd-854">`facet=[string]` (zero or more) - A field toofacet by.</span></span> <span data-ttu-id="3fffd-855">Chaîne de hello peut contenir des facettes hello paramètres toocustomize exprimée sous la forme séparées par des virgules `name:value` paires.</span><span class="sxs-lookup"><span data-stu-id="3fffd-855">Optionally hello string may contain parameters toocustomize hello faceting expressed as comma-separated `name:value` pairs.</span></span> <span data-ttu-id="3fffd-856">Les paramètres valides sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="3fffd-856">Valid parameters are:</span></span>

* <span data-ttu-id="3fffd-857">`count` (nombre maximal de termes de facette ; la valeur par défaut est 10).</span><span class="sxs-lookup"><span data-stu-id="3fffd-857">`count` (max number of facet terms; default is 10).</span></span> <span data-ttu-id="3fffd-858">Il n’existe pas de maximum, mais les valeurs plus élevées entraînent une baisse des performances correspondante, en particulier si le champ à facettes de hello contient un grand nombre de termes uniques.</span><span class="sxs-lookup"><span data-stu-id="3fffd-858">There is no maximum, but higher values incur a corresponding performance penalty, especially if hello faceted field contains a large number of unique terms.</span></span>
  * <span data-ttu-id="3fffd-859">Par exemple : `facet=category,count:5` obtient hello cinq catégories dans les résultats de facette.</span><span class="sxs-lookup"><span data-stu-id="3fffd-859">For example: `facet=category,count:5` gets hello top five categories in facet results.</span></span>  
  * <span data-ttu-id="3fffd-860">**Remarque**: si hello `count` paramètre est inférieur au nombre de hello de termes uniques, les résultats de hello ne peuvent pas être précis.</span><span class="sxs-lookup"><span data-stu-id="3fffd-860">**Note**: If hello `count` parameter is less than hello number of unique terms, hello results may not be accurate.</span></span> <span data-ttu-id="3fffd-861">Il s’agit en raison de la façon de toohello les requêtes par facettes sont distribuées entre plusieurs partitions.</span><span class="sxs-lookup"><span data-stu-id="3fffd-861">This is due toohello way faceting queries are distributed across shards.</span></span> <span data-ttu-id="3fffd-862">Augmentation `count` généralement augmente hello précision hello des nombres de termes, mais au détriment des performances.</span><span class="sxs-lookup"><span data-stu-id="3fffd-862">Increasing `count` generally increases hello accuracy of hello term counts, but at a performance cost.</span></span>
* <span data-ttu-id="3fffd-863">`sort`(un des `count` toosort *décroissant* par nombre, `-count` toosort *croissant* par nombre, `value` toosort *croissant* par valeur, ou `-value` toosort *décroissant* par valeur)</span><span class="sxs-lookup"><span data-stu-id="3fffd-863">`sort` (one of `count` toosort *descending* by count, `-count` toosort *ascending* by count, `value` toosort *ascending* by value, or `-value` toosort *descending* by value)</span></span>
  * <span data-ttu-id="3fffd-864">Par exemple : `facet=category,count:3,sort:count` obtient hello trois premières catégories dans les résultats de facette dans l’ordre décroissant par numéro hello de documents contenant le nom de chaque ville.</span><span class="sxs-lookup"><span data-stu-id="3fffd-864">For example: `facet=category,count:3,sort:count` gets hello top three categories in facet results in descending order by hello number of documents with each city name.</span></span> <span data-ttu-id="3fffd-865">Par exemple, si hello trois premières catégories sont Budget, hôtel et luxe, Budget recueille 5 correspondances, hôtel 6, et luxe 4, puis hello compartiments sera dans l’ordre de hello hôtel, Budget et luxe.</span><span class="sxs-lookup"><span data-stu-id="3fffd-865">For example, if hello top three categories are Budget, Motel, and Luxury, and Budget has 5 hits, Motel has 6, and Luxury has 4, then hello buckets will be in hello order Motel, Budget, Luxury.</span></span>
  * <span data-ttu-id="3fffd-866">Par exemple : `facet=rating,sort:-value` génère des compartiments pour tous les classements possibles, triés par ordre décroissant des valeurs.</span><span class="sxs-lookup"><span data-stu-id="3fffd-866">For example: `facet=rating,sort:-value` produces buckets for all possible ratings, in descending order by value.</span></span> <span data-ttu-id="3fffd-867">Par exemple, si les évaluations de hello vont de 1 too5, hello ordre des compartiments est 5, 4, 3, 2, 1, quel que soit le nombre de documents correspondant à chaque évaluation.</span><span class="sxs-lookup"><span data-stu-id="3fffd-867">For example, if hello ratings are from 1 too5, hello buckets will be ordered 5, 4, 3, 2, 1, irrespective of how many documents match each rating.</span></span>
* <span data-ttu-id="3fffd-868">`values` (valeur numérique délimitée une barre verticale ou valeurs `Edm.DateTimeOffset` qui spécifient un ensemble dynamique de valeurs d'entrée de facette)</span><span class="sxs-lookup"><span data-stu-id="3fffd-868">`values` (pipe-delimited numeric or `Edm.DateTimeOffset` values specifying a dynamic set of facet entry values)</span></span>
  * <span data-ttu-id="3fffd-869">Par exemple : `facet=baseRate,values:10|20` produit trois compartiments : une pour le taux de base 0 des toobut non compris 10, l’autre pour 10 haut toobut non compris 20 et pour supérieur ou égal à 20.</span><span class="sxs-lookup"><span data-stu-id="3fffd-869">For example: `facet=baseRate,values:10|20` produces three buckets: One for base rate 0 up toobut not including 10, one for 10 up toobut not including 20, and one for 20 or higher.</span></span>
  * <span data-ttu-id="3fffd-870">Par exemple : `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` génère deux compartiments : un pour les hôtels rénovés avant février 2010 et un pour les hôtels rénovés à partir du 1er février 2010.</span><span class="sxs-lookup"><span data-stu-id="3fffd-870">For example: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` produces two buckets: One for hotels renovated before February 2010, and one for hotels renovated February 1st, 2010 or later.</span></span>
* <span data-ttu-id="3fffd-871">`interval` (intervalle d'entiers supérieur à 0 pour les nombres ou `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` pour les valeurs de date et heure)</span><span class="sxs-lookup"><span data-stu-id="3fffd-871">`interval` (integer interval greater than 0 for numbers, or `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` for date time values)</span></span>
  * <span data-ttu-id="3fffd-872">Par exemple : `facet=baseRate,interval:100` génère des compartiments basés sur des plages de taux de base comprenant 100 valeurs.</span><span class="sxs-lookup"><span data-stu-id="3fffd-872">For example: `facet=baseRate,interval:100` produces buckets based on base rate ranges of size 100.</span></span> <span data-ttu-id="3fffd-873">Par exemple, si les taux de base sont tous compris entre 60 dollars et 600 dollars, il y aura les compartiments suivants : 0-100, 100-200, 200-300, 300-400, 400-500 et 500-600.</span><span class="sxs-lookup"><span data-stu-id="3fffd-873">For example, if base rates are all between $60 and $600, there will be buckets for 0-100, 100-200, 200-300, 300-400, 400-500, and 500-600.</span></span>
  * <span data-ttu-id="3fffd-874">Par exemple : `facet=lastRenovationDate,interval:year` génère un compartiment pour chaque année de rénovation des hôtels.</span><span class="sxs-lookup"><span data-stu-id="3fffd-874">For example: `facet=lastRenovationDate,interval:year` produces one bucket for each year when hotels were renovated.</span></span>
* <span data-ttu-id="3fffd-875">`timeoffset` ([+-]hh:mm, [+-]hhmm, ou [+-]hh) `timeoffset` est facultatif.</span><span class="sxs-lookup"><span data-stu-id="3fffd-875">`timeoffset` ([+-]hh:mm, [+-]hhmm, or [+-]hh) `timeoffset` is optional.</span></span> <span data-ttu-id="3fffd-876">Il peut uniquement être combiné avec hello `interval` option et uniquement lorsqu’un champ de type tooa appliqué `Edm.DateTimeOffset`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-876">It can only be combined with hello `interval` option, and only when applied tooa field of type `Edm.DateTimeOffset`.</span></span> <span data-ttu-id="3fffd-877">valeur de Hello spécifie tooaccount de décalage de temps hello UTC pour lors de la définition des limites de temps.</span><span class="sxs-lookup"><span data-stu-id="3fffd-877">hello value specifies hello UTC time offset tooaccount for in setting time boundaries.</span></span>
  * <span data-ttu-id="3fffd-878">Par exemple : `facet=lastRenovationDate,interval:day,timeoffset:-01:00` utilise hello limite jour commençant à 01:00:00 UTC (minuit sur fuseau horaire de hello cible)</span><span class="sxs-lookup"><span data-stu-id="3fffd-878">For example: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` uses hello day boundary that starts at 01:00:00 UTC (midnight in hello target time zone)</span></span>
* <span data-ttu-id="3fffd-879">**Remarque**: `count` et `sort` peuvent être combinés dans hello même spécification de facette, mais ils ne peuvent pas être combiné avec `interval` ou `values`, et `interval` et `values` ne peut pas être combinées.</span><span class="sxs-lookup"><span data-stu-id="3fffd-879">**Note**: `count` and `sort` can be combined in hello same facet specification, but they cannot be combined with `interval` or `values`, and `interval` and `values` cannot be combined together.</span></span>
* <span data-ttu-id="3fffd-880">**Remarque** : les facettes d’intervalle de date et d’heure sont calculées en fonction de l’heure UTC si `timeoffset` n’est pas spécifié.</span><span class="sxs-lookup"><span data-stu-id="3fffd-880">**Note**: Interval facets on date time are computed based on UTC time if `timeoffset` is not specified.</span></span> <span data-ttu-id="3fffd-881">Par exemple : pour `facet=lastRenovationDate,interval:day`, limite de jour hello commence à 00:00:00 UTC.</span><span class="sxs-lookup"><span data-stu-id="3fffd-881">For example: for `facet=lastRenovationDate,interval:day`, hello day boundary starts at 00:00:00 UTC.</span></span> 

> [!NOTE]
> <span data-ttu-id="3fffd-882">Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `facets` au lieu de `facet`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-882">When calling **Search** using POST, this parameter is named `facets` instead of `facet`.</span></span> <span data-ttu-id="3fffd-883">En outre, vous le spécifiez sous forme de tableau JSON de chaînes où chaque chaîne est une expression de facette distincte.</span><span class="sxs-lookup"><span data-stu-id="3fffd-883">Also, you specify it as a JSON array of strings where each string is a separate facet expression.</span></span>
> 
> 

<span data-ttu-id="3fffd-884">`$filter=[string]` (facultatif) : expression de recherche structurée avec une syntaxe OData standard.</span><span class="sxs-lookup"><span data-stu-id="3fffd-884">`$filter=[string]` (optional) - A structured search expression in standard OData syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="3fffd-885">Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `filter` au lieu de `$filter`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-885">When calling **Search** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="3fffd-886">`highlight=[string]` (facultatif) : ensemble de noms de champ séparés par des virgules pour la mise en surbrillance des correspondances.</span><span class="sxs-lookup"><span data-stu-id="3fffd-886">`highlight=[string]` (optional) - A set of comma-separated field names used for hit highlights.</span></span> <span data-ttu-id="3fffd-887">Seuls les champs `searchable` peuvent être utilisés pour la mise en surbrillance des correspondances.</span><span class="sxs-lookup"><span data-stu-id="3fffd-887">Only `searchable` fields can be used for hit highlighting.</span></span>

<span data-ttu-id="3fffd-888">`highlightPreTag=[string]`(facultatif, par défaut est trop`<em>`) - une balise qui ajoute des mises en surbrillance toohit de chaîne.</span><span class="sxs-lookup"><span data-stu-id="3fffd-888">`highlightPreTag=[string]` (optional, defaults too`<em>`) - A string tag that prepends toohit highlights.</span></span> <span data-ttu-id="3fffd-889">Doit être défini avec `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-889">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="3fffd-890">Lors de l’appel **recherche** à l’aide de GET, les caractères réservés dans les URL hello doivent être encodés en pourcentage (par exemple, %23 au lieu de #).</span><span class="sxs-lookup"><span data-stu-id="3fffd-890">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="3fffd-891">`highlightPostTag=[string]`(facultatif, par défaut est trop`</em>`)-une balise de chaîne qui ajoute des mises en surbrillance toohit.</span><span class="sxs-lookup"><span data-stu-id="3fffd-891">`highlightPostTag=[string]` (optional, defaults too`</em>`) - a string tag that appends toohit highlights.</span></span> <span data-ttu-id="3fffd-892">Doit être défini avec `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-892">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="3fffd-893">Lors de l’appel **recherche** à l’aide de GET, les caractères réservés dans les URL hello doivent être encodés en pourcentage (par exemple, %23 au lieu de #).</span><span class="sxs-lookup"><span data-stu-id="3fffd-893">When calling **Search** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="3fffd-894">`scoringProfile=[string]`(facultatif) - nom hello d’un calcul de score tooevaluate de profil mettre en correspondance les scores de correspondance des documents dans les résultats de commande toosort hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-894">`scoringProfile=[string]` (optional) - hello name of a scoring profile tooevaluate match scores for matching documents in order toosort hello results.</span></span>

<span data-ttu-id="3fffd-895">`scoringParameter=[string]`(zéro ou plus) - indique les valeurs hello pour chaque paramètre défini dans une fonction de calcul de score (par exemple, `referencePointParameter`) à l’aide du format de hello `name-value1,value2,...`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-895">`scoringParameter=[string]` (zero or more) - Indicates hello values for each parameter defined in a scoring function (for example, `referencePointParameter`) using hello format `name-value1,value2,...`.</span></span>

* <span data-ttu-id="3fffd-896">Par exemple, si hello profil de calcul de score définit une fonction avec un paramètre appelé l’option de chaîne de requête « mylocation » hello serait `&scoringParameter=mylocation--122.2,44.8`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-896">For example, if hello scoring profile defines a function with a parameter called "mylocation" hello query string option would be `&scoringParameter=mylocation--122.2,44.8`.</span></span> <span data-ttu-id="3fffd-897">tiret de première Hello sépare les nom de hello à partir de la liste des valeurs hello, tandis que le tiret de deuxième hello fait partie de la première valeur de hello (longitude dans cet exemple).</span><span class="sxs-lookup"><span data-stu-id="3fffd-897">hello first dash separates hello name from hello value list, while hello second dash is part of hello first value (longitude in this example).</span></span>
* <span data-ttu-id="3fffd-898">Pour les paramètres de calcul de score comme balise boosting qui peut contenir des virgules, échapper tout ces valeurs dans la liste de hello à l’aide de guillemets simples.</span><span class="sxs-lookup"><span data-stu-id="3fffd-898">For scoring parameters such as for tag boosting that can contain commas, you can escape any such values in hello list using single quotes.</span></span> <span data-ttu-id="3fffd-899">Si les valeurs hello elles-mêmes contiennent des guillemets simples, vous pouvez d’échappement en doublant.</span><span class="sxs-lookup"><span data-stu-id="3fffd-899">If hello values themselves contain single quotes, you can escape them by doubling.</span></span>
  * <span data-ttu-id="3fffd-900">Par exemple, si vous disposez d’une balise de renforcement de paramètre nommé « mytag » et que vous souhaitez tooboost sur la balise de hello les valeurs « Hello, o ' Brien » et « Smith », la requête de hello chaîne option serait `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-900">For example, if you have a tag boosting parameter called "mytag" and you want tooboost on hello tag values "Hello, O'Brien" and "Smith", hello query string option would be `&scoringParameter=mytag-'Hello, O''Brien',Smith`.</span></span> <span data-ttu-id="3fffd-901">Notez que les guillemets sont uniquement requis pour les valeurs qui contiennent des virgules.</span><span class="sxs-lookup"><span data-stu-id="3fffd-901">Note that quotes are only required for values that contain commas.</span></span>

> [!NOTE]
> <span data-ttu-id="3fffd-902">Lors de l’appel de **Search** à l’aide de POST, ce paramètre est nommé `scoringParameters` au lieu de `scoringParameter`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-902">When calling **Search** using POST, this parameter is named `scoringParameters` instead of `scoringParameter`.</span></span> <span data-ttu-id="3fffd-903">En outre, vous le spécifiez sous forme de tableau JSON de chaînes où chaque chaîne est une paire `name-values` distincte.</span><span class="sxs-lookup"><span data-stu-id="3fffd-903">Also, you specify it as a JSON array of strings where each string is a separate `name-values` pair.</span></span>
> 
> 

<span data-ttu-id="3fffd-904">`minimumCoverage`(facultatif, par défaut est too100) - un nombre compris entre 0 et 100 qui indique le pourcentage hello d’index hello qui doit être couvert par une requête de recherche dans l’ordre pour hello requête toobe signalée comme un succès.</span><span class="sxs-lookup"><span data-stu-id="3fffd-904">`minimumCoverage` (optional, defaults too100) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a search query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="3fffd-905">Par défaut, la totalité de l’index hello doit être disponible ou `Search` renvoie le code d’état HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="3fffd-905">By default, hello entire index must be available or `Search` will return HTTP status code 503.</span></span> <span data-ttu-id="3fffd-906">Si vous définissez `minimumCoverage` et `Search` réussit, elle retourne HTTP 200 et inclure une `@search.coverage` valeur dans la réponse hello indiquant le pourcentage de hello d’index hello qui a été inclus dans la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-906">If you set `minimumCoverage` and `Search` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="3fffd-907">Ce paramètre paramètre tooa inférieur à 100 peut être utile pour garantir la disponibilité de recherche même pour les services avec un seul.</span><span class="sxs-lookup"><span data-stu-id="3fffd-907">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="3fffd-908">Toutefois, pas tous les documents correspondants sont garanties toobe présent dans les résultats de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-908">However, not all matching documents are guaranteed toobe present in hello search results.</span></span> <span data-ttu-id="3fffd-909">Si le rappel de recherche est l’application tooyour plus importante que la disponibilité, il est meilleure tooleave `minimumCoverage` sa valeur par défaut de 100.</span><span class="sxs-lookup"><span data-stu-id="3fffd-909">If search recall is more important tooyour application than availability, then it's best tooleave `minimumCoverage` at its default value of 100.</span></span>
> 
> 

<span data-ttu-id="3fffd-910">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="3fffd-910">`api-version=[string]` (required).</span></span> <span data-ttu-id="3fffd-911">version d’évaluation Hello `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-911">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3fffd-912">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3fffd-912">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3fffd-913">Remarque : Pour cette opération, hello `api-version` est spécifié comme un paramètre de requête dans l’URL de hello indépendamment de si vous appelez **recherche** POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="3fffd-913">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Search** with GET or POST.</span></span>

<span data-ttu-id="3fffd-914">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-914">**Request Headers**</span></span>

<span data-ttu-id="3fffd-915">Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.</span><span class="sxs-lookup"><span data-stu-id="3fffd-915">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3fffd-916">`api-key`: hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-916">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3fffd-917">Il est une valeur de chaîne URL du service tooyour unique.</span><span class="sxs-lookup"><span data-stu-id="3fffd-917">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="3fffd-918">Hello **recherche** demande peut spécifier une clé d’administration ou une clé de requête pour `api-key`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-918">hello **Search** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="3fffd-919">Vous devez également les URL de demande du nom tooconstruct hello hello service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-919">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3fffd-920">Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3fffd-920">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3fffd-921">Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.</span><span class="sxs-lookup"><span data-stu-id="3fffd-921">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3fffd-922">**Corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-922">**Request Body**</span></span>

<span data-ttu-id="3fffd-923">Pour GET : aucun.</span><span class="sxs-lookup"><span data-stu-id="3fffd-923">For GET: None.</span></span>

<span data-ttu-id="3fffd-924">Pour POST :</span><span class="sxs-lookup"><span data-stu-id="3fffd-924">For POST:</span></span>

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
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

<span data-ttu-id="3fffd-925">**Continuation des réponses de recherche partielle**</span><span class="sxs-lookup"><span data-stu-id="3fffd-925">**Continuation of Partial Search Responses**</span></span>

<span data-ttu-id="3fffd-926">Parfois, Azure Search ne peut pas retourner que toutes les hello résultats demandés dans une réponse de recherche unique.</span><span class="sxs-lookup"><span data-stu-id="3fffd-926">Sometimes Azure Search can't return all hello requested results in a single Search response.</span></span> <span data-ttu-id="3fffd-927">Cela peut se produire pour différentes raisons, telles que lorsque hello requête trop grand nombre de documents en ne spécifiant `$top` ou en spécifiant une valeur pour `$top` qui est trop grande.</span><span class="sxs-lookup"><span data-stu-id="3fffd-927">This can happen for different reasons, such as when hello query requests too many documents by not specifying `$top` or specifying a value for `$top` that is too large.</span></span> <span data-ttu-id="3fffd-928">Dans ce cas, Azure Search inclura hello `@odata.nextLink` annotation dans le corps de réponse hello et également `@search.nextPageParameters` s’il s’agissait d’une demande POST.</span><span class="sxs-lookup"><span data-stu-id="3fffd-928">In such cases, Azure Search will include hello `@odata.nextLink` annotation in hello response body, and also `@search.nextPageParameters` if it was a POST request.</span></span> <span data-ttu-id="3fffd-929">Vous pouvez utiliser les valeurs de ces tooformulate annotations hello une autre recherche demande tooget hello partie suivante de la réponse de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-929">You can use hello values of these annotations tooformulate another Search request tooget hello next part of hello search response.</span></span> <span data-ttu-id="3fffd-930">Cela s’appelle un ***continuation*** de demande de recherche d’origine hello et hello annotations sont généralement appelées ***jetons de continuation***.</span><span class="sxs-lookup"><span data-stu-id="3fffd-930">This is called a ***continuation*** of hello original Search request, and hello annotations are generally called ***continuation tokens***.</span></span> <span data-ttu-id="3fffd-931">Consultez [exemple hello ci-dessous](#SearchResponse) pour plus d’informations sur la syntaxe hello de ces annotations et où ils apparaissent dans le corps de la réponse hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-931">See [hello example below](#SearchResponse) for details on hello syntax of these annotations and where they appear in hello response body.</span></span> 

<span data-ttu-id="3fffd-932">raisons Hello pourquoi Azure Search peut renvoyer des jetons de continuation sont spécifiques à l’implémentation et l’objet toochange.</span><span class="sxs-lookup"><span data-stu-id="3fffd-932">hello reasons why Azure Search might return continuation tokens are implementation-specific and subject toochange.</span></span> <span data-ttu-id="3fffd-933">Les clients robustes doivent toujours être prêt toohandle cas où les documents moins que prévu sont retournés et un jeton de liaison toocontinue inclus, la récupération de documents.</span><span class="sxs-lookup"><span data-stu-id="3fffd-933">Robust clients should always be ready toohandle cases where fewer documents than expected are returned and a continuation token is included toocontinue retrieving documents.</span></span> <span data-ttu-id="3fffd-934">Également Notez que vous devez utiliser hello même méthode HTTP en tant que requête d’origine de hello dans l’ordre toocontinue.</span><span class="sxs-lookup"><span data-stu-id="3fffd-934">Also note that you must use hello same HTTP method as hello original request in order toocontinue.</span></span> <span data-ttu-id="3fffd-935">Par exemple, si vous avez envoyé une demande GET, toutes les demandes de continuation que vous envoyez doivent également utiliser GET (y compris pour POST).</span><span class="sxs-lookup"><span data-stu-id="3fffd-935">For example, if you sent a GET request, any continuation requests you send must also use GET (and likewise for POST).</span></span>

<span data-ttu-id="3fffd-936"><a name="SearchResponse"></a>
**Réponse**</span><span class="sxs-lookup"><span data-stu-id="3fffd-936"><a name="SearchResponse"></a>
**Response**</span></span>

<span data-ttu-id="3fffd-937">Code d'état : 200 OK est retourné pour une réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="3fffd-937">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
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
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
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
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

<span data-ttu-id="3fffd-938">**Exemples :**</span><span class="sxs-lookup"><span data-stu-id="3fffd-938">**Examples:**</span></span>

<span data-ttu-id="3fffd-939">Vous trouverez des exemples supplémentaires sur hello [syntaxe d’Expression OData pour Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.</span><span class="sxs-lookup"><span data-stu-id="3fffd-939">You can find additional examples on hello [OData Expression Syntax for Azure Search](https://msdn.microsoft.com/library/azure/dn798921.aspx) page.</span></span>

1)    <span data-ttu-id="3fffd-940">Hello de recherche Index triés par ordre décroissant par date.</span><span class="sxs-lookup"><span data-stu-id="3fffd-940">Search hello Index sorted descending by date.</span></span>

    <span data-ttu-id="3fffd-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3fffd-941">GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3fffd-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span><span class="sxs-lookup"><span data-stu-id="3fffd-942">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "orderby": "lastRenovationDate desc" }</span></span>

2)    <span data-ttu-id="3fffd-943">Dans une recherche à facettes, rechercher les index hello et récupérer des facettes de catégories, évaluation, balises, ainsi que les éléments avec la valeur baserate s’inscrit dans des plages spécifiques :</span><span class="sxs-lookup"><span data-stu-id="3fffd-943">In a faceted search, search hello index and retrieve facets for categories, rating, tags, as well as items with baseRate in specific ranges:</span></span>

    <span data-ttu-id="3fffd-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3fffd-944">GET /indexes/hotels/docs?search=test&facet=category&facet=rating&facet=tags&facet=baseRate,values:80|150|220&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3fffd-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span><span class="sxs-lookup"><span data-stu-id="3fffd-945">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "category", "rating", "tags", "baseRate,values:80|150|220" ] }</span></span>

3)    <span data-ttu-id="3fffd-946">À l’aide d’un filtre, affiner les résultats de requête à facettes précédents hello après hello utilisateur clique sur évaluation 3 et la catégorie « Motel » :</span><span class="sxs-lookup"><span data-stu-id="3fffd-946">Using a filter, narrow down hello previous faceted query results after hello user clicks on rating 3 and category "Motel":</span></span>

    <span data-ttu-id="3fffd-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3fffd-947">GET /indexes/hotels/docs?search=test&facet=tags&facet=baseRate,values:80|150|220&$filter=rating eq 3 and category eq 'Motel'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3fffd-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span><span class="sxs-lookup"><span data-stu-id="3fffd-948">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "test", "facets": [ "tags", "baseRate,values:80|150|220" ], "filter": "rating eq 3 and category eq 'Motel'" }</span></span>

4) <span data-ttu-id="3fffd-949">Dans une recherche à facettes, définir une limite supérieure sur des termes uniques retournés dans une requête.</span><span class="sxs-lookup"><span data-stu-id="3fffd-949">In a faceted search, set an upper limit on unique terms returned in a query.</span></span> <span data-ttu-id="3fffd-950">Hello par défaut 10, mais vous pouvez augmenter ou diminuer cette valeur à l’aide de hello `count` paramètre sur hello `facet` attribut :</span><span class="sxs-lookup"><span data-stu-id="3fffd-950">hello default is 10, but you can increase or decrease this value using hello `count` parameter on hello `facet` attribute:</span></span>

    <span data-ttu-id="3fffd-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3fffd-951">GET /indexes/hotels/docs?search=test&facet=city,count:5&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3fffd-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span><span class="sxs-lookup"><span data-stu-id="3fffd-952">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "test",    "facets": [ "city,count:5" ]  }</span></span>

5)    <span data-ttu-id="3fffd-953">Rechercher hello Index dans des domaines spécifiques. Par exemple, il s’agit d’un champ spécifique au langage :</span><span class="sxs-lookup"><span data-stu-id="3fffd-953">Search hello Index within specific fields; For example, a language-specific field:</span></span>

    <span data-ttu-id="3fffd-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3fffd-954">GET /indexes/hotels/docs?search=hôtel&searchFields=description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3fffd-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span><span class="sxs-lookup"><span data-stu-id="3fffd-955">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "hôtel", "searchFields": "description_fr" }</span></span>

6) <span data-ttu-id="3fffd-956">Hello Index dans plusieurs champs de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-956">Search hello Index across multiple fields.</span></span> <span data-ttu-id="3fffd-957">Par exemple, vous pouvez stocker et champs de requête recherche dans plusieurs langues, toutes les tâches dans hello même index.</span><span class="sxs-lookup"><span data-stu-id="3fffd-957">For example, you can store and query searchable fields in multiple languages, all within hello same index.</span></span>  <span data-ttu-id="3fffd-958">Si des descriptions en anglais et Français coexistent dans hello même document, vous pouvez retourner tout ou partie hello dans résultats de la requête :</span><span class="sxs-lookup"><span data-stu-id="3fffd-958">If English and French descriptions co-exist in hello same document, you can return any or all in hello query results:</span></span>

    <span data-ttu-id="3fffd-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3fffd-959">GET /indexes/hotels/docs?search=hotel&searchFields=description,description_fr&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3fffd-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span><span class="sxs-lookup"><span data-stu-id="3fffd-960">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview  {    "search": "hotel",    "searchFields": "description, description_fr"  }</span></span>

<span data-ttu-id="3fffd-961">Notez que vous pouvez interroger uniquement un index à la fois.</span><span class="sxs-lookup"><span data-stu-id="3fffd-961">Note that you can only query one index at a time.</span></span> <span data-ttu-id="3fffd-962">Ne créez pas plusieurs index pour chaque langue, sauf si vous prévoyez tooquery une à la fois.</span><span class="sxs-lookup"><span data-stu-id="3fffd-962">Do not create multiple indexes for each language unless you plan tooquery one at a time.</span></span>

7)    <span data-ttu-id="3fffd-963">Pagination - Get hello 1ère page d’éléments (taille de page est 10) :</span><span class="sxs-lookup"><span data-stu-id="3fffd-963">Paging - Get hello 1st page of items (page size is 10):</span></span>

    <span data-ttu-id="3fffd-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3fffd-964">GET /indexes/hotels/docs?search=*&$skip=0&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3fffd-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="3fffd-965">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 0, "top": 10 }</span></span>

8)    <span data-ttu-id="3fffd-966">Pagination - Get hello 2ème page d’éléments (taille de page est 10) :</span><span class="sxs-lookup"><span data-stu-id="3fffd-966">Paging - Get hello 2nd page of items (page size is 10):</span></span>

    <span data-ttu-id="3fffd-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3fffd-967">GET /indexes/hotels/docs?search=*&$skip=10&$top=10&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3fffd-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span><span class="sxs-lookup"><span data-stu-id="3fffd-968">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "skip": 10, "top": 10 }</span></span>

9)    <span data-ttu-id="3fffd-969">Récupérer un ensemble spécifique de champs :</span><span class="sxs-lookup"><span data-stu-id="3fffd-969">Retrieve a specific set of fields:</span></span>

    <span data-ttu-id="3fffd-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3fffd-970">GET /indexes/hotels/docs?search=*&$select=hotelName,description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3fffd-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span><span class="sxs-lookup"><span data-stu-id="3fffd-971">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview { "search": "*", "select": "hotelName, description" }</span></span>

10)  <span data-ttu-id="3fffd-972">Récupérer les documents correspondant à une expression de filtre spécifique :</span><span class="sxs-lookup"><span data-stu-id="3fffd-972">Retrieve documents matching a specific filter expression:</span></span>

    <span data-ttu-id="3fffd-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3fffd-973">GET /indexes/hotels/docs?$filter=(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3fffd-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span><span class="sxs-lookup"><span data-stu-id="3fffd-974">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {  "filter": "(baseRate ge 60 and baseRate lt 300) or hotelName eq 'Fancy Stay'" }</span></span>

11) <span data-ttu-id="3fffd-975">Index de recherche hello et des fragments de retournés avec des surlignages</span><span class="sxs-lookup"><span data-stu-id="3fffd-975">Search hello index and return fragments with hit highlights</span></span>

    <span data-ttu-id="3fffd-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3fffd-976">GET /indexes/hotels/docs?search=something&highlight=description&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3fffd-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span><span class="sxs-lookup"><span data-stu-id="3fffd-977">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "highlight": "description" }</span></span>

12) <span data-ttu-id="3fffd-978">Index de recherche hello et documents triés du plus proche toofarther en dehors d’un emplacement de référence de retour</span><span class="sxs-lookup"><span data-stu-id="3fffd-978">Search hello index and return documents sorted from closer toofarther away from a reference location</span></span>

    <span data-ttu-id="3fffd-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3fffd-979">GET /indexes/hotels/docs?search=something&$orderby=geo.distance(location, geography'POINT(-122.12315 47.88121)')&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3fffd-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span><span class="sxs-lookup"><span data-stu-id="3fffd-980">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "orderby": "geo.distance(location, geography'POINT(-122.12315 47.88121)')" }</span></span>

13) <span data-ttu-id="3fffd-981">Recherche hello index en supposant qu’il est un profil de score appelé « geo » avec deux fonctions de score de distance, une définition d’un paramètre nommé « currentlocation » et une définition d’un paramètre nommé « lastLocation »</span><span class="sxs-lookup"><span data-stu-id="3fffd-981">Search hello index assuming there's a scoring profile called "geo" with two distance scoring functions, one defining a parameter called "currentLocation" and one defining a parameter called "lastLocation"</span></span>

    <span data-ttu-id="3fffd-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3fffd-982">GET /indexes/hotels/docs?search=something&scoringProfile=geo&scoringParameter=currentLocation--122.123,44.77233&scoringParameter=lastLocation--121.499,44.2113&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3fffd-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span><span class="sxs-lookup"><span data-stu-id="3fffd-983">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "something",   "scoringProfile": "geo",   "scoringParameters": [ "currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113" ] }</span></span>

14) <span data-ttu-id="3fffd-984">Rechercher des documents à l’aide d’index hello [syntaxe de requête simple](https://msdn.microsoft.com/library/dn798920.aspx).</span><span class="sxs-lookup"><span data-stu-id="3fffd-984">Find documents in hello index using [simple query syntax](https://msdn.microsoft.com/library/dn798920.aspx).</span></span> <span data-ttu-id="3fffd-985">Cette requête renvoie les hôtels où les champs interrogeables contiennent hello termes « comfort » et « location » mais pas « motel » :</span><span class="sxs-lookup"><span data-stu-id="3fffd-985">This query returns hotels where searchable fields contain hello terms "comfort" and "location" but not "motel":</span></span>

    <span data-ttu-id="3fffd-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span><span class="sxs-lookup"><span data-stu-id="3fffd-986">GET /indexes/hotels/docs?search=comfort +location -motel&searchMode=all&api-version=2015-02-28-Preview</span></span>

    <span data-ttu-id="3fffd-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="3fffd-987">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "comfort +location -motel",   "searchMode": "all" }</span></span>

<span data-ttu-id="3fffd-988">Notez que hello `searchMode=all` ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="3fffd-988">Note hello use of `searchMode=all` above.</span></span> <span data-ttu-id="3fffd-989">Ce paramètre remplace hello comme valeur par défaut `searchMode=any`, en s’assurant que `-motel` signifie « Et pas » au lieu de « OR NOT ».</span><span class="sxs-lookup"><span data-stu-id="3fffd-989">Including this parameter overrides hello default of `searchMode=any`, ensuring that `-motel` means "AND NOT" instead of "OR NOT".</span></span> <span data-ttu-id="3fffd-990">Sans `searchMode=all`, vous obtenez « OR NOT » qui s’étend au lieu de limite les résultats de recherche, et cela peut être contre-intuitif toosome utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3fffd-990">Without `searchMode=all`, you get "OR NOT" which expands rather than restricts search results, and this can be counter-intuitive toosome users.</span></span>

15) <span data-ttu-id="3fffd-991">Rechercher des documents à l’aide d’index hello [syntaxe de requête lucene](https://msdn.microsoft.com/library/mt589323.aspx).</span><span class="sxs-lookup"><span data-stu-id="3fffd-991">Find documents in hello index using [lucene query syntax](https://msdn.microsoft.com/library/mt589323.aspx).</span></span> <span data-ttu-id="3fffd-992">Cette requête renvoie les hôtels où le champ de catégorie hello contient le terme hello « budget » et tous les champs contenant la phrase hello « récemment rénovée ».</span><span class="sxs-lookup"><span data-stu-id="3fffd-992">This query returns hotels where hello category field contains hello term "budget" and all searchable fields containing hello phrase "recently renovated".</span></span> <span data-ttu-id="3fffd-993">Les documents contenant « récemment rénovée » de la phrase hello rang supérieur à la suite de valeur de renforcement de terme hello (3)</span><span class="sxs-lookup"><span data-stu-id="3fffd-993">Documents containing hello phrase "recently renovated" are ranked higher as a result of hello term boost value (3)</span></span>

    <span data-ttu-id="3fffd-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span><span class="sxs-lookup"><span data-stu-id="3fffd-994">GET /indexes/hotels/docs?search=category:budget AND \"recently renovated\"^3&searchMode=all&api-version=2015-02-28-Preview&querytype=full</span></span>

    <span data-ttu-id="3fffd-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span><span class="sxs-lookup"><span data-stu-id="3fffd-995">POST /indexes/hotels/docs/search?api-version=2015-02-28-Preview {   "search": "category:budget AND \"recently renovated\"^3",   "queryType": "full",   "searchMode": "all" }</span></span>

<a name="LookupAPI"></a>

## <a name="lookup-document"></a><span data-ttu-id="3fffd-996">Recherche de document</span><span class="sxs-lookup"><span data-stu-id="3fffd-996">Lookup Document</span></span>
<span data-ttu-id="3fffd-997">Hello **recherche de Document** opération récupère un document à partir d’Azure Search.</span><span class="sxs-lookup"><span data-stu-id="3fffd-997">hello **Lookup Document** operation retrieves a document from Azure Search.</span></span> <span data-ttu-id="3fffd-998">Cela est utile lorsqu’un utilisateur clique sur un résultat de recherche, et que vous souhaitez toolook des détails spécifiques sur ce document.</span><span class="sxs-lookup"><span data-stu-id="3fffd-998">This is useful when a user clicks on a specific search result, and you want toolook up specific details about that document.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

<span data-ttu-id="3fffd-999">**Requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-999">**Request**</span></span>

<span data-ttu-id="3fffd-1000">Le protocole HTTPS est requis pour les requêtes de service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1000">HTTPS is required for service requests.</span></span> <span data-ttu-id="3fffd-1001">Hello **recherche de Document** demande peut être construite comme suit.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1001">hello **Lookup Document** request can be constructed as follows.</span></span>

    GET /indexes/[index name]/docs/key?[query parameters]

<span data-ttu-id="3fffd-1002">Vous pouvez également utiliser la syntaxe OData traditionnelle de hello pour la recherche de clé :</span><span class="sxs-lookup"><span data-stu-id="3fffd-1002">Alternatively, you can use hello traditional OData syntax for key lookup:</span></span>

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

<span data-ttu-id="3fffd-1003">Hello URI de requête inclut un [nom d’index] et [clé], en spécifiant le tooretrieve de document à partir de l’index.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1003">hello request URI includes an [index name] and [key], specifying which document tooretrieve from which index.</span></span> <span data-ttu-id="3fffd-1004">Vous ne pouvez obtenir qu'un seul document à la fois.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1004">You can only get one document at a time.</span></span> <span data-ttu-id="3fffd-1005">Utilisez **recherche** tooget plusieurs documents dans une demande unique.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1005">Use **Search** tooget multiple documents in a single request.</span></span>

<span data-ttu-id="3fffd-1006">**Paramètres de requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-1006">**Query Parameters**</span></span>

<span data-ttu-id="3fffd-1007">`$select=[string]`(facultatif) : une liste de champs séparés par des virgules tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1007">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="3fffd-1008">Si non spécifié ou défini trop`*`, tous les champs marqués comme récupérables dans le schéma de hello sont inclus dans la projection de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1008">If unspecified or set too`*`, all fields marked as retrievable in hello schema are included in hello projection.</span></span>

<span data-ttu-id="3fffd-1009">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="3fffd-1009">`api-version=[string]` (required).</span></span> <span data-ttu-id="3fffd-1010">version d’évaluation Hello `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1010">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3fffd-1011">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3fffd-1011">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3fffd-1012">Remarque : Pour cette opération, hello `api-version` est spécifié comme un paramètre de requête.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1012">Note: For this operation, hello `api-version` is specified as a query parameter.</span></span>

<span data-ttu-id="3fffd-1013">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-1013">**Request Headers**</span></span>

<span data-ttu-id="3fffd-1014">Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1014">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3fffd-1015">`api-key`: hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1015">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3fffd-1016">Il est une valeur de chaîne URL du service tooyour unique.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1016">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="3fffd-1017">Hello **recherche de Document** demande peut spécifier une clé d’administration ou une clé de requête pour `api-key`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1017">hello **Lookup Document** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="3fffd-1018">Vous devez également les URL de demande du nom tooconstruct hello hello service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1018">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3fffd-1019">Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1019">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3fffd-1020">Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1020">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3fffd-1021">**Corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-1021">**Request Body**</span></span>

<span data-ttu-id="3fffd-1022">Aucune.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1022">None.</span></span>

<span data-ttu-id="3fffd-1023">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="3fffd-1023">**Response**</span></span>

<span data-ttu-id="3fffd-1024">Code d'état : 200 OK est retourné pour une réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1024">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

<span data-ttu-id="3fffd-1025">**Exemple**</span><span class="sxs-lookup"><span data-stu-id="3fffd-1025">**Example**</span></span>

<span data-ttu-id="3fffd-1026">Recherche de document hello ayant la clé « 2 »</span><span class="sxs-lookup"><span data-stu-id="3fffd-1026">Lookup hello document that has key '2'</span></span>

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

<span data-ttu-id="3fffd-1027">Recherche de document hello ayant la clé « 3 » à l’aide de la syntaxe OData :</span><span class="sxs-lookup"><span data-stu-id="3fffd-1027">Lookup hello document that has key '3' using OData syntax:</span></span>

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a><span data-ttu-id="3fffd-1028">Nombre de documents</span><span class="sxs-lookup"><span data-stu-id="3fffd-1028">Count Documents</span></span>
<span data-ttu-id="3fffd-1029">Hello **nombre de Documents** opération récupère le nombre de hello de documents dans un index de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1029">hello **Count Documents** operation retrieves a count of hello number of documents in a search index.</span></span> <span data-ttu-id="3fffd-1030">Hello `$count` syntaxe fait partie du protocole OData de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1030">hello `$count` syntax is part of hello OData protocol.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

<span data-ttu-id="3fffd-1031">**Requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-1031">**Request**</span></span>

<span data-ttu-id="3fffd-1032">Le protocole HTTPS est requis pour les requêtes de service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1032">HTTPS is required for service requests.</span></span> <span data-ttu-id="3fffd-1033">Hello **nombre de Documents** demande peut être construite à l’aide de la méthode GET de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1033">hello **Count Documents** request can be constructed using hello GET method.</span></span>

<span data-ttu-id="3fffd-1034">Bonjour [nom de l’index] dans l’URI de la demande hello indique hello service tooreturn un nombre de tous les éléments dans la collection de documents hello de l’index spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1034">hello [index name] in hello request URI tells hello service tooreturn a count of all items in hello docs collection of hello specified index.</span></span>

<span data-ttu-id="3fffd-1035">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="3fffd-1035">`api-version=[string]` (required).</span></span> <span data-ttu-id="3fffd-1036">version d’évaluation Hello `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1036">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3fffd-1037">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3fffd-1037">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3fffd-1038">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-1038">**Request Headers**</span></span>

<span data-ttu-id="3fffd-1039">Hello suivant liste décrit hello requis et les en-têtes de demande facultatif.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1039">hello following list describes hello required and optional request headers.</span></span>

* <span data-ttu-id="3fffd-1040">`Accept`: Cette valeur doit être définie trop`text/plain`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1040">`Accept`: This value must be set too`text/plain`.</span></span>
* <span data-ttu-id="3fffd-1041">`api-key`: hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1041">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3fffd-1042">Il est une valeur de chaîne URL du service tooyour unique.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1042">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="3fffd-1043">Hello **nombre de Documents** demande peut spécifier une clé d’administration ou une clé de requête pour `api-key`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1043">hello **Count Documents** request can specify either an admin key or query key for `api-key`.</span></span>

<span data-ttu-id="3fffd-1044">Vous devez également les URL de demande du nom tooconstruct hello hello service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1044">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3fffd-1045">Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1045">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3fffd-1046">Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1046">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3fffd-1047">**Corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-1047">**Request Body**</span></span>

<span data-ttu-id="3fffd-1048">Aucune.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1048">None.</span></span>

<span data-ttu-id="3fffd-1049">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="3fffd-1049">**Response**</span></span>

<span data-ttu-id="3fffd-1050">Code d'état : 200 OK est retourné pour une réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1050">Status Code: 200 OK is returned for a successful response.</span></span>

<span data-ttu-id="3fffd-1051">corps de réponse de Hello contient la valeur du nombre de hello en tant qu’entier au format texte brut.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1051">hello response body contains hello count value as an integer formatted in plain text.</span></span>

<a name="Suggestions"></a>

## <a name="suggestions"></a><span data-ttu-id="3fffd-1052">Suggestions</span><span class="sxs-lookup"><span data-stu-id="3fffd-1052">Suggestions</span></span>
<span data-ttu-id="3fffd-1053">Hello **Suggestions** opération récupère des suggestions basées sur l’entrée de recherche partielle.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1053">hello **Suggestions** operation retrieves suggestions based on partial search input.</span></span> <span data-ttu-id="3fffd-1054">Il est généralement utilisé dans les suggestions de recherche boîtes tooprovide prédictives que les utilisateurs entrent des termes de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1054">It's typically used in search boxes tooprovide type-ahead suggestions as users are entering search terms.</span></span>

<span data-ttu-id="3fffd-1055">Demandes de suggestions visant à suggérer des documents cibles, donc hello suggéré de texte peut être répété si plusieurs documents candidats correspondent hello même entrée de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1055">Suggestion requests aim at suggesting target documents, so hello suggested text may be repeated if multiple candidate documents match hello same search input.</span></span> <span data-ttu-id="3fffd-1056">Vous pouvez utiliser `$select` tooretrieve autres champs (y compris la clé de document hello) de document afin que vous sachiez quel document constitue la source de hello de chaque suggestion.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1056">You can use `$select` tooretrieve other document fields (including hello document key) so that you can tell which document is hello source for each suggestion.</span></span>

<span data-ttu-id="3fffd-1057">Une opération **Suggestions** est publiée en tant que requête GET ou POST.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1057">A **Suggestions** operation is issued as a GET or POST request.</span></span>

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

<span data-ttu-id="3fffd-1058">**Lorsque toouse VALIDEZ au lieu de GET**</span><span class="sxs-lookup"><span data-stu-id="3fffd-1058">**When toouse POST instead of GET**</span></span>

<span data-ttu-id="3fffd-1059">Lorsque vous utilisez HTTP GET les hello toocall **Suggestions** API, vous devez toobe conscient que hello hello URL de demande ne peut pas dépasser 8 Ko.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1059">When you use HTTP GET toocall hello **Suggestions** API, you need toobe aware that hello length of hello request URL cannot exceed 8 KB.</span></span> <span data-ttu-id="3fffd-1060">Cela est généralement suffisamment pour la plupart des applications.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1060">This is usually enough for most applications.</span></span> <span data-ttu-id="3fffd-1061">Toutefois, certaines applications produisent des requêtes très volumineuses, en particulier les expressions de filtre OData.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1061">However, some applications produce very large queries, specifically OData filter expressions.</span></span> <span data-ttu-id="3fffd-1062">Pour ces applications, il est recommandé d'utiliser HTTP POST, car cela permet d'obtenir des filtres plus volumineux que GET.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1062">For these applications, using HTTP POST is a better choice because it allows larger filters than GET.</span></span> <span data-ttu-id="3fffd-1063">Avec POST, hello de clauses dans un filtre de facteur de limitation hello, ne Hello pas de taille de la chaîne de filtre brutes hello, car la limite de taille de demande de hello POST est d’environ 16 Mo.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1063">With POST, hello number of clauses in a filter is hello limiting factor, not hello size of hello raw filter string since hello request size limit for POST is approximately 16 MB.</span></span>

> [!NOTE]
> <span data-ttu-id="3fffd-1064">Bien que la limite de taille de demande POST hello est très volumineux, les expressions de filtre ne peut pas être arbitrairement complexes.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1064">Even though hello POST request size limit is very large, filter expressions cannot be arbitrarily complex.</span></span> <span data-ttu-id="3fffd-1065">Consultez [Syntaxe d’expression OData](https://msdn.microsoft.com/library/dn798921.aspx) pour plus d’informations sur les limites de complexité des filtres.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1065">See [OData expression syntax](https://msdn.microsoft.com/library/dn798921.aspx) for more information about filter complexity limitations.</span></span>
> 
> 

<span data-ttu-id="3fffd-1066">**Requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-1066">**Request**</span></span>

<span data-ttu-id="3fffd-1067">Le protocole HTTPS est requis pour les requêtes de service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1067">HTTPS is required for service requests.</span></span> <span data-ttu-id="3fffd-1068">Hello **Suggestions** demande peut être construite à l’aide de hello GET ou la méthode POST.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1068">hello **Suggestions** request can be constructed using hello GET or POST methods.</span></span>

<span data-ttu-id="3fffd-1069">URI de demande Hello Spécifie le nom hello de hello index tooquery.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1069">hello request URI specifies hello name of hello index tooquery.</span></span> <span data-ttu-id="3fffd-1070">Paramètres, tels que terme recherché partiellement entré de hello, sont spécifiés dans la chaîne de requête hello dans les cas de hello de demandes GET, et dans la demande hello corps dans les cas de hello de demande.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1070">Parameters, such as hello partially input search term, are specified on hello query string in hello case of GET requests, and in hello request body in hello case of POST requests.</span></span>

<span data-ttu-id="3fffd-1071">Comme meilleure pratique lors de la création de demandes GET, n’oubliez pas trop[encoder en URL](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) paramètres lors de l’appel hello directement les API REST de requête spécifique.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1071">As a best practice when creating GET requests, remember too[URL-encode](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) specific query parameters when calling hello REST API directly.</span></span> <span data-ttu-id="3fffd-1072">Pour les opérations **Suggestions** , cela inclut :</span><span class="sxs-lookup"><span data-stu-id="3fffd-1072">For **Suggestions** operations, this includes:</span></span>

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

<span data-ttu-id="3fffd-1073">L’encodage d’URL est recommandée uniquement sur hello au-dessus de paramètres de requête.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1073">URL encoding is only recommended on hello above query parameters.</span></span> <span data-ttu-id="3fffd-1074">Si vous par inadvertance encoder en URL hello la chaîne de requête entière (tout ce qui suit hello ?), les demandes s’interrompent.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1074">If you inadvertently URL-encode hello entire query string (everything after hello ?), requests will break.</span></span>

<span data-ttu-id="3fffd-1075">En outre, l’encodage d’URL est nécessaire uniquement lors de l’appel hello obtenir de l’API REST directement à l’aide.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1075">Also, URL encoding is only necessary when calling hello REST API directly using GET.</span></span> <span data-ttu-id="3fffd-1076">Aucun encodage d’URL n’est nécessaire lors de l’appel **Suggestions** à l’aide de POST, ou lorsque vous utilisez hello [bibliothèque cliente .NET](https://msdn.microsoft.com/library/dn951165.aspx), qui gère l’encodage d’URL pour vous.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1076">No URL encoding is necessary when calling **Suggestions** using POST, or when using hello [.NET client library](https://msdn.microsoft.com/library/dn951165.aspx), which handles URL encoding for you.</span></span>

<span data-ttu-id="3fffd-1077">**Paramètres de requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-1077">**Query Parameters**</span></span>

<span data-ttu-id="3fffd-1078">**Suggestions** accepte plusieurs paramètres qui fournissent les critères de la requête et qui spécifient également le comportement de la recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1078">**Suggestions** accepts several parameters that provide query criteria and also specify search behavior.</span></span> <span data-ttu-id="3fffd-1079">Vous fournissez ces paramètres dans l’URL de hello la chaîne de requête lors de l’appel **Suggestions** via GET et en tant que propriétés JSON dans le corps de la demande hello lors de l’appel **Suggestions** via la publication.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1079">You provide these parameters in hello URL query string when calling **Suggestions** via GET, and as JSON properties in hello request body when calling **Suggestions** via POST.</span></span> <span data-ttu-id="3fffd-1080">syntaxe Hello pour certains paramètres est légèrement différente entre GET et POST.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1080">hello syntax for some parameters is slightly different between GET and POST.</span></span> <span data-ttu-id="3fffd-1081">Ces différences sont indiquées ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="3fffd-1081">These differences are noted as applicable below:</span></span>

<span data-ttu-id="3fffd-1082">`search=[string]`-hello texte toouse toosuggest requêtes.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1082">`search=[string]` - hello search text toouse toosuggest queries.</span></span> <span data-ttu-id="3fffd-1083">Doit comprendre 1 caractère au minimum et 100 caractères au maximum.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1083">Must be at least 1 character, and no more than 100 characters.</span></span>

<span data-ttu-id="3fffd-1084">`highlightPreTag=[string]`(facultatif) : balise de chaîne qui ajoute des présences dans le toosearch.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1084">`highlightPreTag=[string]` (optional) - a string tag that prepends toosearch hits.</span></span> <span data-ttu-id="3fffd-1085">Doit être défini avec `highlightPostTag`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1085">Must be set with `highlightPostTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="3fffd-1086">Lors de l’appel **Suggestions** à l’aide de GET, les caractères réservés dans les URL hello doivent être encodés en pourcentage (par exemple, %23 au lieu de #).</span><span class="sxs-lookup"><span data-stu-id="3fffd-1086">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="3fffd-1087">`highlightPostTag=[string]`(facultatif) : balise de chaîne qui ajoute des présences dans le toosearch.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1087">`highlightPostTag=[string]` (optional) - a string tag that appends toosearch hits.</span></span> <span data-ttu-id="3fffd-1088">Doit être défini avec `highlightPreTag`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1088">Must be set with `highlightPreTag`.</span></span>

> [!NOTE]
> <span data-ttu-id="3fffd-1089">Lors de l’appel **Suggestions** à l’aide de GET, les caractères réservés dans les URL hello doivent être encodés en pourcentage (par exemple, %23 au lieu de #).</span><span class="sxs-lookup"><span data-stu-id="3fffd-1089">When calling **Suggestions** using GET, reserved characters in hello URL must be percent-encoded (for example, %23 instead of #).</span></span>
> 
> 

<span data-ttu-id="3fffd-1090">`suggesterName=[string]`-nom hello de suggestion spécifié dans hello hello `suggesters` collection qui fait partie de la définition de l’index hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1090">`suggesterName=[string]` - hello name of hello suggester as specified in hello `suggesters` collection that's part of hello index definition.</span></span> <span data-ttu-id="3fffd-1091">Un `suggester` détermine les champs qui sont analysés pour les termes de requête suggérés.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1091">A `suggester` determines which fields are scanned for suggested query terms.</span></span> <span data-ttu-id="3fffd-1092">Pour plus d'informations, consultez [Générateurs de suggestions](#Suggesters) .</span><span class="sxs-lookup"><span data-stu-id="3fffd-1092">See [Suggesters](#Suggesters) for details.</span></span>

<span data-ttu-id="3fffd-1093">`fuzzy=[boolean]`(facultatif, par défaut = false)-lorsque la valeur tootrue cette API trouve des suggestions même s’il existe un caractère erroné ou manquant dans le texte de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1093">`fuzzy=[boolean]` (optional, default = false) - when set tootrue this API will find suggestions even if there's a substituted or missing character in hello search text.</span></span> <span data-ttu-id="3fffd-1094">Bien qu'il en résulte une meilleure expérience, dans certains cas cela a un impact négatif sur les performances, car les recherches de suggestions approximatives sont plus lentes et consomment davantage de ressources.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1094">While this provides a better experience in some scenarios it comes at a performance cost as fuzzy suggestion searches are slower and consume more resources.</span></span>

<span data-ttu-id="3fffd-1095">`searchFields=[string]`(facultatif) : liste hello de toosearch de noms de champ séparées par des virgules pour hello spécifié Rechercher du texte.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1095">`searchFields=[string]` (optional) - hello list of comma-separated field names toosearch for hello specified search text.</span></span> <span data-ttu-id="3fffd-1096">Les champs cibles doivent être activés pour les suggestions.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1096">Target fields must be enabled for suggestions.</span></span>

<span data-ttu-id="3fffd-1097">`$top=#`(facultatif, par défaut = 5)-nombre de suggestions tooretrieve de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1097">`$top=#` (optional, default = 5) - hello number of suggestions tooretrieve.</span></span> <span data-ttu-id="3fffd-1098">Doit être un nombre compris entre 1 et 100.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1098">Must be a number between 1 and 100.</span></span>

> [!NOTE]
> <span data-ttu-id="3fffd-1099">Pendant l’appel de **Suggestions** à l’aide de POST, ce paramètre est nommé `top` au lieu de `$top`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1099">When calling **Suggestions** using POST, this parameter is named `top` instead of `$top`.</span></span>
> 
> 

<span data-ttu-id="3fffd-1100">`$filter=[string]`(facultatif) : une expression qui filtre les documents hello pris en compte pour obtenir des suggestions.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1100">`$filter=[string]` (optional) - an expression that filters hello documents considered for suggestions.</span></span>

> [!NOTE]
> <span data-ttu-id="3fffd-1101">Pendant l’appel de **Suggestions** à l’aide de POST, ce paramètre est nommé `filter` au lieu de `$filter`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1101">When calling **Suggestions** using POST, this parameter is named `filter` instead of `$filter`.</span></span>
> 
> 

<span data-ttu-id="3fffd-1102">`$orderby=[string]`(facultatif) : une liste de résultats de hello toosort séparées par des virgules des expressions par.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1102">`$orderby=[string]` (optional) - a list of comma-separated expressions toosort hello results by.</span></span> <span data-ttu-id="3fffd-1103">Chaque expression peut être un nom de champ ou d’un appel toohello `geo.distance()` (fonction).</span><span class="sxs-lookup"><span data-stu-id="3fffd-1103">Each expression can be either a field name or a call toohello `geo.distance()` function.</span></span> <span data-ttu-id="3fffd-1104">Chaque expression peut être suivie `asc` tooindicated par ordre croissant, et `desc` tooindicate décroissant.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1104">Each expression can be followed by `asc` tooindicated ascending, and `desc` tooindicate descending.</span></span> <span data-ttu-id="3fffd-1105">valeur par défaut Hello est l’ordre croissant.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1105">hello default is ascending order.</span></span> <span data-ttu-id="3fffd-1106">Il existe une limite de 32 clauses pour `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1106">There is a limit of 32 clauses for `$orderby`.</span></span>

> [!NOTE]
> <span data-ttu-id="3fffd-1107">Pendant l’appel de **Suggestions** à l’aide de POST, ce paramètre est nommé `orderby` au lieu de `$orderby`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1107">When calling **Suggestions** using POST, this parameter is named `orderby` instead of `$orderby`.</span></span>
> 
> 

<span data-ttu-id="3fffd-1108">`$select=[string]`(facultatif) : une liste de champs séparés par des virgules tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1108">`$select=[string]` (optional) - a list of comma-separated fields tooretrieve.</span></span> <span data-ttu-id="3fffd-1109">Si non spécifié, hello uniquement de clé de document et le texte de la suggestion est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1109">If unspecified, only hello document key and suggestion text is returned.</span></span> <span data-ttu-id="3fffd-1110">Vous pouvez demander explicitement tous les champs en définissant ce paramètre trop`*`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1110">You can explicitly request all fields by setting this parameter too`*`.</span></span>

> [!NOTE]
> <span data-ttu-id="3fffd-1111">Pendant l’appel de **Suggestions** à l’aide de POST, ce paramètre est nommé `select` au lieu de `$select`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1111">When calling **Suggestions** using POST, this parameter is named `select` instead of `$select`.</span></span>
> 
> 

<span data-ttu-id="3fffd-1112">`minimumCoverage`(facultatif, par défaut est too80) - un nombre compris entre 0 et 100 qui indique le pourcentage hello d’index hello qui doit être couvert par une requête de suggestions dans l’ordre pour hello requête toobe signalée comme un succès.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1112">`minimumCoverage` (optional, defaults too80) - a number between 0 and 100 indicating hello percentage of hello index that must be covered by a suggestions query in order for hello query toobe reported as a success.</span></span> <span data-ttu-id="3fffd-1113">Par défaut, au moins 80 % de l’index de hello doit être disponible ou `Suggest` renvoie le code d’état HTTP 503.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1113">By default, at least 80% of hello index must be available or `Suggest` will return HTTP status code 503.</span></span> <span data-ttu-id="3fffd-1114">Si vous définissez `minimumCoverage` et `Suggest` réussit, elle retourne HTTP 200 et inclure une `@search.coverage` valeur dans la réponse hello indiquant le pourcentage de hello d’index hello qui a été inclus dans la requête de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1114">If you set `minimumCoverage` and `Suggest` succeeds, it will return HTTP 200 and include a `@search.coverage` value in hello response indicating hello percentage of hello index that was included in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="3fffd-1115">Ce paramètre paramètre tooa inférieur à 100 peut être utile pour garantir la disponibilité de recherche même pour les services avec un seul.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1115">Setting this parameter tooa value lower than 100 can be useful for ensuring search availability even for services with only one replica.</span></span> <span data-ttu-id="3fffd-1116">Toutefois, pas toutes les suggestions de correspondance sont garanties toobe présent dans les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1116">However, not all matching suggestions are guaranteed toobe present in hello results.</span></span> <span data-ttu-id="3fffd-1117">Si le rappel est l’application tooyour plus importante que la disponibilité, puis ses ne meilleures pas toolower `minimumCoverage` sous sa valeur par défaut 80.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1117">If recall is more important tooyour application than availability, then it's best not toolower `minimumCoverage` below its default value of 80.</span></span>
> 
> 

<span data-ttu-id="3fffd-1118">`api-version=[string]` (obligatoire).</span><span class="sxs-lookup"><span data-stu-id="3fffd-1118">`api-version=[string]` (required).</span></span> <span data-ttu-id="3fffd-1119">version d’évaluation Hello `api-version=2015-02-28-Preview`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1119">hello preview version is `api-version=2015-02-28-Preview`.</span></span> <span data-ttu-id="3fffd-1120">Pour plus d'informations, y compris sur d'autres versions, consultez [Contrôle de version de service Azure Search](http://msdn.microsoft.com/library/azure/dn864560.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3fffd-1120">See [Search Service Versioning](http://msdn.microsoft.com/library/azure/dn864560.aspx) for details and alternative versions.</span></span>

<span data-ttu-id="3fffd-1121">Remarque : Pour cette opération, hello `api-version` est spécifié comme un paramètre de requête dans l’URL de hello indépendamment de si vous appelez **Suggestions** POST ou GET.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1121">Note: For this operation, hello `api-version` is specified as a query parameter in hello URL regardless of whether you call **Suggestions** with GET or POST.</span></span>

<span data-ttu-id="3fffd-1122">**En-têtes de requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-1122">**Request Headers**</span></span>

<span data-ttu-id="3fffd-1123">Hello suivant liste décrit hello requis et les en-têtes de demande facultatif</span><span class="sxs-lookup"><span data-stu-id="3fffd-1123">hello following list describes hello required and optional request headers</span></span>

* <span data-ttu-id="3fffd-1124">`api-key`: hello `api-key` est utilisé tooauthenticate hello demande tooyour service de recherche.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1124">`api-key`: hello `api-key` is used tooauthenticate hello request tooyour Search service.</span></span> <span data-ttu-id="3fffd-1125">Il est une valeur de chaîne URL du service tooyour unique.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1125">It is a string value, unique tooyour service URL.</span></span> <span data-ttu-id="3fffd-1126">Hello **Suggestions** demande peut spécifier une clé d’administration ou une clé de requête en tant que hello `api-key`.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1126">hello **Suggestions** request can specify either an admin key or query key as hello `api-key`.</span></span>

<span data-ttu-id="3fffd-1127">Vous devez également les URL de demande du nom tooconstruct hello hello service.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1127">You will also need hello service name tooconstruct hello request URL.</span></span> <span data-ttu-id="3fffd-1128">Vous pouvez obtenir le nom du service hello et `api-key` à partir de votre tableau de bord de service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1128">You can get hello service name and `api-key` from your service dashboard in hello Azure Portal.</span></span> <span data-ttu-id="3fffd-1129">Consultez [créer un service Azure Search dans le portail de hello](search-create-service-portal.md) de l’aide de navigation de page.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1129">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for page navigation help.</span></span>

<span data-ttu-id="3fffd-1130">**Corps de la requête**</span><span class="sxs-lookup"><span data-stu-id="3fffd-1130">**Request Body**</span></span>

<span data-ttu-id="3fffd-1131">Pour GET : aucun.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1131">For GET: None.</span></span>

<span data-ttu-id="3fffd-1132">Pour POST :</span><span class="sxs-lookup"><span data-stu-id="3fffd-1132">For POST:</span></span>

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

<span data-ttu-id="3fffd-1133">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="3fffd-1133">**Response**</span></span>

<span data-ttu-id="3fffd-1134">Code d'état : 200 OK est retourné pour une réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="3fffd-1134">Status Code: 200 OK is returned for a successful response.</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

<span data-ttu-id="3fffd-1135">Si l’option de projection hello est utilisé tooretrieve champs, ils sont inclus dans chaque élément du tableau de hello :</span><span class="sxs-lookup"><span data-stu-id="3fffd-1135">If hello projection option is used tooretrieve fields they are included in each element of hello array:</span></span>

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

<span data-ttu-id="3fffd-1136">**Exemple**</span><span class="sxs-lookup"><span data-stu-id="3fffd-1136">**Example**</span></span>

<span data-ttu-id="3fffd-1137">Récupérer 5 suggestions où entrée de recherche partielle hello est « lux »</span><span class="sxs-lookup"><span data-stu-id="3fffd-1137">Retrieve 5 suggestions where hello partial search input is 'lux'</span></span>

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
