---
title: "résultats de la recherche de toopage aaaHow dans Azure Search | Documents Microsoft"
description: "Pagination dans Azure Search, un service de recherche cloud hébergé sur Microsoft Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
ms.assetid: a0a1d315-8624-4cdf-b38e-ba12569c6fcc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: heidist
ms.openlocfilehash: e3abc1ca4d5994b0a77955379081a4fcfa5a7fa7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopage-search-results-in-azure-search"></a><span data-ttu-id="12616-103">Affichage des résultats de recherche de toopage dans Azure Search</span><span class="sxs-lookup"><span data-stu-id="12616-103">How toopage search results in Azure Search</span></span>
<span data-ttu-id="12616-104">Cet article fournit des conseils sur l’affichage des résultats de page, tels que le total des nombres, récupération de document, ordres de tri et la navigation toouse hello API REST de Service Azure Search tooimplement éléments standard d’une recherche.</span><span class="sxs-lookup"><span data-stu-id="12616-104">This article provides guidance on how toouse hello Azure Search Service REST API tooimplement standard elements of a search results page, such as total counts, document retrieval, sort orders, and navigation.</span></span>

<span data-ttu-id="12616-105">Dans tous les cas mentionnés ci-dessous, les options de page qui contribuent des données ou des informations tooyour page de résultats sont spécifiées via hello [recherche dans le Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) tooyour de demandes envoyées Service Azure Search.</span><span class="sxs-lookup"><span data-stu-id="12616-105">In every case mentioned below, page-related options that contribute data or information tooyour search results page are specified through hello [Search Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) requests sent tooyour Azure Search Service.</span></span> <span data-ttu-id="12616-106">Les demandes incluent une commande GET, chemin d’accès et les paramètres de requête qui informent le service hello ce qui est demandé et comment tooformulate hello réponse.</span><span class="sxs-lookup"><span data-stu-id="12616-106">Requests include a GET command, path, and query parameters that inform hello service what is being requested, and how tooformulate hello response.</span></span>

> [!NOTE]
> <span data-ttu-id="12616-107">Une demande valide inclut plusieurs éléments, parmi lesquels une URL de service et un chemin d’accès, un verbe HTTP, `api-version`, etc.</span><span class="sxs-lookup"><span data-stu-id="12616-107">A valid request includes a number of elements, such as a service URL and path, HTTP verb, `api-version`, and so on.</span></span> <span data-ttu-id="12616-108">Par souci de concision, nous tronquées hello exemples toohighlight hello simplement la syntaxe toopagination pertinentes.</span><span class="sxs-lookup"><span data-stu-id="12616-108">For brevity, we trimmed hello examples toohighlight just hello syntax that is relevant toopagination.</span></span> <span data-ttu-id="12616-109">Consultez hello [API REST de Service Azure Search](http://msdn.microsoft.com/library/azure/dn798935.aspx) pour plus d’informations sur la syntaxe de requête.</span><span class="sxs-lookup"><span data-stu-id="12616-109">Please see hello [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentation for details about request syntax.</span></span>
> 
> 

## <a name="total-hits-and-page-counts"></a><span data-ttu-id="12616-110">Nombre total de résultats et nombre de pages</span><span class="sxs-lookup"><span data-stu-id="12616-110">Total hits and Page Counts</span></span>
<span data-ttu-id="12616-111">Affichage hello total nombre de résultats retournés à partir d’une requête, puis de retourner les résultats en segments plus petits, n’est fondamental toovirtually toutes les pages de recherche.</span><span class="sxs-lookup"><span data-stu-id="12616-111">Showing hello total number of results returned from a query, and then returning those results in smaller chunks, is fundamental toovirtually all search pages.</span></span>

![][1]

<span data-ttu-id="12616-112">Dans Azure Search, vous utilisez hello `$count`, `$top`, et `$skip` paramètres tooreturn ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="12616-112">In Azure Search, you use hello `$count`, `$top`, and `$skip` parameters tooreturn these values.</span></span> <span data-ttu-id="12616-113">Hello suivant montre un exemple de demande pour le nombre total d’accès, retourné sous la forme `@OData.count`:</span><span class="sxs-lookup"><span data-stu-id="12616-113">hello following example shows a sample request for total hits, returned as `@OData.count`:</span></span>

        GET /indexes/onlineCatalog/docs?$count=true

<span data-ttu-id="12616-114">Récupérer des documents dans des groupes de 15 et indiquent également le nombre total d’accès hello, en commençant à la première page de hello :</span><span class="sxs-lookup"><span data-stu-id="12616-114">Retrieve documents in groups of 15, and also show hello total hits, starting at hello first page:</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

<span data-ttu-id="12616-115">Pagination des résultats requiert deux `$top` et `$skip`, où `$top` spécifie combien tooreturn d’éléments dans un lot, et `$skip` spécifie combien tooskip d’éléments.</span><span class="sxs-lookup"><span data-stu-id="12616-115">Paginating results requires both `$top` and `$skip`, where `$top` specifies how many items tooreturn in a batch, and `$skip` specifies how many items tooskip.</span></span> <span data-ttu-id="12616-116">Bonjour, l’exemple suivant chaque page affiche hello ensuite 15 d’éléments, indiquée par sauts incrémentielle de hello Bonjour `$skip` paramètre.</span><span class="sxs-lookup"><span data-stu-id="12616-116">In hello following example, each page shows hello next 15 items, indicated by hello incremental jumps in hello `$skip` parameter.</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a><span data-ttu-id="12616-117">Disposition</span><span class="sxs-lookup"><span data-stu-id="12616-117">Layout</span></span>
<span data-ttu-id="12616-118">Sur une page de résultats, vous pourriez tooshow une image miniature, un sous-ensemble des champs et une page de produit complet tooa lien.</span><span class="sxs-lookup"><span data-stu-id="12616-118">On a search results page, you might want tooshow a thumbnail image, a subset of fields, and a link tooa full product page.</span></span>

 ![][2]

<span data-ttu-id="12616-119">Dans Azure Search, vous utiliseriez `$select` et une recherche des commandes tooimplement cette expérience.</span><span class="sxs-lookup"><span data-stu-id="12616-119">In Azure Search, you would use `$select` and a lookup command tooimplement this experience.</span></span>

<span data-ttu-id="12616-120">tooreturn un sous-ensemble des champs d’une disposition en mosaïque :</span><span class="sxs-lookup"><span data-stu-id="12616-120">tooreturn a subset of fields for a tiled layout:</span></span>

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

<span data-ttu-id="12616-121">Images et fichiers multimédias ne sont pas directement interrogeables et doivent être stockées dans une autre plate-forme de stockage, telles que le stockage Blob Azure, les coûts de tooreduce.</span><span class="sxs-lookup"><span data-stu-id="12616-121">Images and media files are not directly searchable and should be stored in another storage platform, such as Azure Blob storage, tooreduce costs.</span></span> <span data-ttu-id="12616-122">Dans les index hello et des documents, définissez un champ qui stocke l’adresse URL de hello du contenu externe de hello.</span><span class="sxs-lookup"><span data-stu-id="12616-122">In hello index and documents, define a field that stores hello URL address of hello external content.</span></span> <span data-ttu-id="12616-123">Vous pouvez ensuite utiliser le champ de hello comme une référence d’image.</span><span class="sxs-lookup"><span data-stu-id="12616-123">You can then use hello field as an image reference.</span></span> <span data-ttu-id="12616-124">URL d’image de toohello Hello doit être dans le document de hello.</span><span class="sxs-lookup"><span data-stu-id="12616-124">hello URL toohello image should be in hello document.</span></span>

<span data-ttu-id="12616-125">tooretrieve page d’une description de produit pour un **onClick** événement, utilisez [recherche de Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass dans la clé de hello de hello document tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="12616-125">tooretrieve a product description page for an **onClick** event, use [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) toopass in hello key of hello document tooretrieve.</span></span> <span data-ttu-id="12616-126">type de données Hello de clé de hello est `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="12616-126">hello data type of hello key is `Edm.String`.</span></span> <span data-ttu-id="12616-127">Dans cet exemple, il s’agit de *246810*.</span><span class="sxs-lookup"><span data-stu-id="12616-127">In this example, it is *246810*.</span></span> 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a><span data-ttu-id="12616-128">Tri par pertinence, évaluation ou prix</span><span class="sxs-lookup"><span data-stu-id="12616-128">Sort by relevance, rating, or price</span></span>
<span data-ttu-id="12616-129">Les ordres de tri souvent par défaut toorelevance, mais il est commun toomake autre les ordres de tri disponibles afin que les clients peuvent remanier rapidement les résultats existants dans un ordre de classement différent.</span><span class="sxs-lookup"><span data-stu-id="12616-129">Sort orders often default toorelevance, but it's common toomake alternative sort orders readily available so that customers can quickly reshuffle existing results into a different rank order.</span></span>

 ![][3]

<span data-ttu-id="12616-130">Dans Azure Search, le tri est basé sur hello `$orderby` expression pour tous les champs qui sont indexés en tant que`"Sortable": true.`</span><span class="sxs-lookup"><span data-stu-id="12616-130">In Azure Search, sorting is based on hello `$orderby` expression, for all fields that are indexed as `"Sortable": true.`</span></span>

<span data-ttu-id="12616-131">La pertinence est clairement liée aux profils de score.</span><span class="sxs-lookup"><span data-stu-id="12616-131">Relevance is strongly associated with scoring profiles.</span></span> <span data-ttu-id="12616-132">Vous pouvez utiliser hello score par défaut, qui repose sur l’ordre de toorank statistiques et d’analyse de texte tous les résultats, avec des scores élevés va toodocuments avec des correspondances plus ou plus forts sur un terme à rechercher.</span><span class="sxs-lookup"><span data-stu-id="12616-132">You can use hello default scoring, which relies on text analysis and statistics toorank order all results, with higher scores going toodocuments with more or stronger matches on a search term.</span></span>

<span data-ttu-id="12616-133">Ordres de tri de remplacement sont généralement associés **onClick** événements rappeler tooa méthode qui génère l’ordre de tri hello.</span><span class="sxs-lookup"><span data-stu-id="12616-133">Alternative sort orders are typically associated with **onClick** events that call back tooa method that builds hello sort order.</span></span> <span data-ttu-id="12616-134">Par exemple, avec cet élément de page :</span><span class="sxs-lookup"><span data-stu-id="12616-134">For example, given this page element:</span></span>

 ![][4]

<span data-ttu-id="12616-135">Vous devez créer une méthode qui accepte une option de tri hello sélectionné en tant qu’entrée et retourne une liste ordonnée de critères hello associés à cette option.</span><span class="sxs-lookup"><span data-stu-id="12616-135">You would create a method that accepts hello selected sort option as input, and returns an ordered list for hello criteria associated with that option.</span></span>

 ![][5]

> [!NOTE]
> <span data-ttu-id="12616-136">Hello de calcul de score par défaut est suffisant pour de nombreux scénarios, nous vous recommandons de baser pertinence sur un profil de score personnalisé à la place.</span><span class="sxs-lookup"><span data-stu-id="12616-136">While hello default scoring is sufficient for many scenarios, we recommend basing relevance on a custom scoring profile instead.</span></span> <span data-ttu-id="12616-137">Un profil de score personnalisé vous donne un tooboost de façon dont les éléments qui sont les plus avantageux tooyour business.</span><span class="sxs-lookup"><span data-stu-id="12616-137">A custom scoring profile gives you a way tooboost items that are more beneficial tooyour business.</span></span> <span data-ttu-id="12616-138">Consultez [Ajout de profils de calcul de score](http://msdn.microsoft.com/library/azure/dn798928.aspx) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="12616-138">See [Add a scoring profile](http://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> 
> 
> 

## <a name="faceted-navigation"></a><span data-ttu-id="12616-139">Navigation à facettes</span><span class="sxs-lookup"><span data-stu-id="12616-139">Faceted navigation</span></span>
<span data-ttu-id="12616-140">Navigation de la recherche est courante dans une page de résultats, souvent située à côté de hello ou en haut d’une page.</span><span class="sxs-lookup"><span data-stu-id="12616-140">Search navigation is common on a results page, often located at hello side or top of a page.</span></span> <span data-ttu-id="12616-141">Dans Azure Search, la navigation à facettes permet une recherche autonome en fonction de filtres prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="12616-141">In Azure Search, faceted navigation provides self-directed search based on predefined filters.</span></span> <span data-ttu-id="12616-142">Consultez [Navigation à facettes dans Azure Search](search-faceted-navigation.md) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="12616-142">See [Faceted navigation in Azure Search](search-faceted-navigation.md) for details.</span></span>

## <a name="filters-at-hello-page-level"></a><span data-ttu-id="12616-143">Filtres au niveau de la page hello</span><span class="sxs-lookup"><span data-stu-id="12616-143">Filters at hello page level</span></span>
<span data-ttu-id="12616-144">Si votre conception de solution inclus des pages de recherche dédié pour certains types de contenu (par exemple, une application de vente au détail en ligne qui a les services répertoriés en hello haut hello), vous pouvez insérer une expression de filtre avec une **onClick** événement tooopen une page dans un état pré-filtrée.</span><span class="sxs-lookup"><span data-stu-id="12616-144">If your solution design included dedicated search pages for specific types of content (for example, an online retail application that has departments listed at hello top of hello page), you can insert a filter expression alongside an **onClick** event tooopen a page in a prefiltered state.</span></span> 

<span data-ttu-id="12616-145">Vous pouvez envoyer un filtre avec ou sans expression de recherche.</span><span class="sxs-lookup"><span data-stu-id="12616-145">You can send a filter with or without a search expression.</span></span> <span data-ttu-id="12616-146">Par exemple, hello de demande suivant filtre sur le nom de marque, ne retourner que les documents qui lui correspondent.</span><span class="sxs-lookup"><span data-stu-id="12616-146">For example, hello following request will filter on brand name, returning only those documents that match it.</span></span>

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

<span data-ttu-id="12616-147">Consultez [Recherche de documents (API Recherche Azure)](http://msdn.microsoft.com/library/azure/dn798927.aspx) pour en savoir plus sur les expressions `$filter`.</span><span class="sxs-lookup"><span data-stu-id="12616-147">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for more information about `$filter` expressions.</span></span>

## <a name="see-also"></a><span data-ttu-id="12616-148">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="12616-148">See Also</span></span>
* [<span data-ttu-id="12616-149">API REST de service Azure Search</span><span class="sxs-lookup"><span data-stu-id="12616-149">Azure Search Service REST API</span></span>](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [<span data-ttu-id="12616-150">Opérations d’index</span><span class="sxs-lookup"><span data-stu-id="12616-150">Index Operations</span></span>](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [<span data-ttu-id="12616-151">Opérations de document</span><span class="sxs-lookup"><span data-stu-id="12616-151">Document Operations</span></span>](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [<span data-ttu-id="12616-152">Vidéos et didacticiels relatifs à Azure Search</span><span class="sxs-lookup"><span data-stu-id="12616-152">Video and tutorials about Azure Search</span></span>](search-video-demo-tutorial-list.md)
* [<span data-ttu-id="12616-153">Navigation à facettes dans Azure Search</span><span class="sxs-lookup"><span data-stu-id="12616-153">Faceted Navigation in Azure Search</span></span>](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
