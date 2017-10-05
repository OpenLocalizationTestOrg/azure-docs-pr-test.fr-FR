---
title: "Navigation dans les résultats de recherche de Recherche Azure | Microsoft Docs"
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
ms.openlocfilehash: 1054e15a2751c53aad5dbc8054c4cec41102dee9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-page-search-results-in-azure-search"></a><span data-ttu-id="aa968-103">Navigation dans les résultats de recherche d’Azure Search</span><span class="sxs-lookup"><span data-stu-id="aa968-103">How to page search results in Azure Search</span></span>
<span data-ttu-id="aa968-104">Cet article explique comment utiliser l’API REST de service Azure Search pour implémenter les éléments standard d’une page de résultats de recherche, comme les totaux, l’extraction de documents, les ordres de tri et la navigation.</span><span class="sxs-lookup"><span data-stu-id="aa968-104">This article provides guidance on how to use the Azure Search Service REST API to implement standard elements of a search results page, such as total counts, document retrieval, sort orders, and navigation.</span></span>

<span data-ttu-id="aa968-105">Dans tous les cas mentionnés ci-après, les options de page qui fournissent des données ou des informations à votre page de résultats de recherche sont spécifiées par le biais des demandes [Recherche de documents](http://msdn.microsoft.com/library/azure/dn798927.aspx) envoyées à votre service Azure Search.</span><span class="sxs-lookup"><span data-stu-id="aa968-105">In every case mentioned below, page-related options that contribute data or information to your search results page are specified through the [Search Document](http://msdn.microsoft.com/library/azure/dn798927.aspx) requests sent to your Azure Search Service.</span></span> <span data-ttu-id="aa968-106">Ces demandes incluent une commande GET, un chemin d’accès et des paramètres de requête informant le service de ce qui est demandé et de la manière dont formuler la réponse.</span><span class="sxs-lookup"><span data-stu-id="aa968-106">Requests include a GET command, path, and query parameters that inform the service what is being requested, and how to formulate the response.</span></span>

> [!NOTE]
> <span data-ttu-id="aa968-107">Une demande valide inclut plusieurs éléments, parmi lesquels une URL de service et un chemin d’accès, un verbe HTTP, `api-version`, etc.</span><span class="sxs-lookup"><span data-stu-id="aa968-107">A valid request includes a number of elements, such as a service URL and path, HTTP verb, `api-version`, and so on.</span></span> <span data-ttu-id="aa968-108">Par souci de concision, nous avons tronqué les exemples afin de mettre en évidence la syntaxe se rapportant à la pagination uniquement.</span><span class="sxs-lookup"><span data-stu-id="aa968-108">For brevity, we trimmed the examples to highlight just the syntax that is relevant to pagination.</span></span> <span data-ttu-id="aa968-109">Consultez [API REST de service Azure Search](http://msdn.microsoft.com/library/azure/dn798935.aspx) pour en savoir plus sur la syntaxe de demande.</span><span class="sxs-lookup"><span data-stu-id="aa968-109">Please see the [Azure Search Service REST API](http://msdn.microsoft.com/library/azure/dn798935.aspx) documentation for details about request syntax.</span></span>
> 
> 

## <a name="total-hits-and-page-counts"></a><span data-ttu-id="aa968-110">Nombre total de résultats et nombre de pages</span><span class="sxs-lookup"><span data-stu-id="aa968-110">Total hits and Page Counts</span></span>
<span data-ttu-id="aa968-111">L’affichage du nombre total des résultats d’une requête et la présentation de ces résultats en blocs plus petits sont des éléments de base sur presque toutes les pages de recherche.</span><span class="sxs-lookup"><span data-stu-id="aa968-111">Showing the total number of results returned from a query, and then returning those results in smaller chunks, is fundamental to virtually all search pages.</span></span>

![][1]

<span data-ttu-id="aa968-112">Dans Azure Search, vous utilisez les paramètres `$count`, `$top` et `$skip` pour renvoyer ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="aa968-112">In Azure Search, you use the `$count`, `$top`, and `$skip` parameters to return these values.</span></span> <span data-ttu-id="aa968-113">L’exemple suivant illustre une demande du nombre total de résultats, renvoyé sous la forme `@OData.count`:</span><span class="sxs-lookup"><span data-stu-id="aa968-113">The following example shows a sample request for total hits, returned as `@OData.count`:</span></span>

        GET /indexes/onlineCatalog/docs?$count=true

<span data-ttu-id="aa968-114">Récupérez des documents par groupes de 15 et affichez le nombre total de résultats à partir de la première page :</span><span class="sxs-lookup"><span data-stu-id="aa968-114">Retrieve documents in groups of 15, and also show the total hits, starting at the first page:</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

<span data-ttu-id="aa968-115">La pagination des résultats nécessite `$top` et `$skip`, où `$top` indique le nombre d’éléments à renvoyer dans un lot, et `$skip` spécifie le nombre d’éléments à ignorer.</span><span class="sxs-lookup"><span data-stu-id="aa968-115">Paginating results requires both `$top` and `$skip`, where `$top` specifies how many items to return in a batch, and `$skip` specifies how many items to skip.</span></span> <span data-ttu-id="aa968-116">Dans l’exemple suivant, chaque page affiche les 15 éléments suivants, conformément aux sauts incrémentiels indiqués dans le paramètre `$skip` .</span><span class="sxs-lookup"><span data-stu-id="aa968-116">In the following example, each page shows the next 15 items, indicated by the incremental jumps in the `$skip` parameter.</span></span>

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=0&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=15&$count=true

        GET /indexes/onlineCatalog/docs?search=*$top=15&$skip=30&$count=true

## <a name="layout"></a><span data-ttu-id="aa968-117">Disposition</span><span class="sxs-lookup"><span data-stu-id="aa968-117">Layout</span></span>
<span data-ttu-id="aa968-118">Vous souhaiterez peut-être afficher une miniature, un sous-ensemble de champs et un lien vers la fiche produit complète sur vos pages de résultats de recherche.</span><span class="sxs-lookup"><span data-stu-id="aa968-118">On a search results page, you might want to show a thumbnail image, a subset of fields, and a link to a full product page.</span></span>

 ![][2]

<span data-ttu-id="aa968-119">Dans Azure Search, vous pouvez utiliser pour cela `$select` et une commande de recherche.</span><span class="sxs-lookup"><span data-stu-id="aa968-119">In Azure Search, you would use `$select` and a lookup command to implement this experience.</span></span>

<span data-ttu-id="aa968-120">Pour renvoyer un sous-ensemble de champs relatif à une disposition en mosaïque :</span><span class="sxs-lookup"><span data-stu-id="aa968-120">To return a subset of fields for a tiled layout:</span></span>

        GET /indexes/ onlineCatalog/docs?search=*&$select=productName,imageFile,description,price,rating 

<span data-ttu-id="aa968-121">Les images et les fichiers multimédias ne peuvent pas faire l’objet de recherches directes et doivent être stockés sur une autre plateforme de stockage, comme l’espace de stockage Azure Blob, afin de limiter les coûts.</span><span class="sxs-lookup"><span data-stu-id="aa968-121">Images and media files are not directly searchable and should be stored in another storage platform, such as Azure Blob storage, to reduce costs.</span></span> <span data-ttu-id="aa968-122">Dans les index et les documents, définissez un champ destiné à stocker l’adresse URL du contenu externe.</span><span class="sxs-lookup"><span data-stu-id="aa968-122">In the index and documents, define a field that stores the URL address of the external content.</span></span> <span data-ttu-id="aa968-123">Vous pourrez utiliser ce champ comme référence d’image.</span><span class="sxs-lookup"><span data-stu-id="aa968-123">You can then use the field as an image reference.</span></span> <span data-ttu-id="aa968-124">L’URL de l’image doit se trouver dans le document.</span><span class="sxs-lookup"><span data-stu-id="aa968-124">The URL to the image should be in the document.</span></span>

<span data-ttu-id="aa968-125">Pour récupérer une page de description de produit relative à un événement **onClick** , utilisez la [recherche de document](http://msdn.microsoft.com/library/azure/dn798929.aspx) afin d’indiquer la clé du document à récupérer.</span><span class="sxs-lookup"><span data-stu-id="aa968-125">To retrieve a product description page for an **onClick** event, use [Lookup Document](http://msdn.microsoft.com/library/azure/dn798929.aspx) to pass in the key of the document to retrieve.</span></span> <span data-ttu-id="aa968-126">Le type de données de la clé est `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="aa968-126">The data type of the key is `Edm.String`.</span></span> <span data-ttu-id="aa968-127">Dans cet exemple, il s’agit de *246810*.</span><span class="sxs-lookup"><span data-stu-id="aa968-127">In this example, it is *246810*.</span></span> 

        GET /indexes/onlineCatalog/docs/246810

## <a name="sort-by-relevance-rating-or-price"></a><span data-ttu-id="aa968-128">Tri par pertinence, évaluation ou prix</span><span class="sxs-lookup"><span data-stu-id="aa968-128">Sort by relevance, rating, or price</span></span>
<span data-ttu-id="aa968-129">Les données sont souvent triées par défaut en fonction de la pertinence, mais il est courant de proposer d’autres ordres de tri afin que les clients puissent rapidement réorganiser les résultats existants.</span><span class="sxs-lookup"><span data-stu-id="aa968-129">Sort orders often default to relevance, but it's common to make alternative sort orders readily available so that customers can quickly reshuffle existing results into a different rank order.</span></span>

 ![][3]

<span data-ttu-id="aa968-130">Dans Azure Search, le tri repose sur l’expression `$orderby` pour tous les champs indexés comme étant `"Sortable": true.`</span><span class="sxs-lookup"><span data-stu-id="aa968-130">In Azure Search, sorting is based on the `$orderby` expression, for all fields that are indexed as `"Sortable": true.`</span></span>

<span data-ttu-id="aa968-131">La pertinence est clairement liée aux profils de score.</span><span class="sxs-lookup"><span data-stu-id="aa968-131">Relevance is strongly associated with scoring profiles.</span></span> <span data-ttu-id="aa968-132">Vous pouvez utiliser le score par défaut, qui repose sur l’analyse de texte et les statistiques pour ordonner tous les résultats : dans ce cas, les documents présentant des correspondances plus nombreuses ou plus fortes affichent un score plus élevé.</span><span class="sxs-lookup"><span data-stu-id="aa968-132">You can use the default scoring, which relies on text analysis and statistics to rank order all results, with higher scores going to documents with more or stronger matches on a search term.</span></span>

<span data-ttu-id="aa968-133">D’autres ordres de tri sont souvent associés aux événements **onClick** qui renvoient à une méthode permettant de générer l’ordre de tri.</span><span class="sxs-lookup"><span data-stu-id="aa968-133">Alternative sort orders are typically associated with **onClick** events that call back to a method that builds the sort order.</span></span> <span data-ttu-id="aa968-134">Par exemple, avec cet élément de page :</span><span class="sxs-lookup"><span data-stu-id="aa968-134">For example, given this page element:</span></span>

 ![][4]

<span data-ttu-id="aa968-135">Vous pouvez créer la méthode qui accepte l’option de tri sélectionnée comme entrée, et renvoie une liste ordonnée conforme aux critères associés à cette option.</span><span class="sxs-lookup"><span data-stu-id="aa968-135">You would create a method that accepts the selected sort option as input, and returns an ordered list for the criteria associated with that option.</span></span>

 ![][5]

> [!NOTE]
> <span data-ttu-id="aa968-136">Si le score par défaut suffit dans de nombreuses situations, nous vous recommandons tout de même de baser la pertinence sur un profil de score personnalisé.</span><span class="sxs-lookup"><span data-stu-id="aa968-136">While the default scoring is sufficient for many scenarios, we recommend basing relevance on a custom scoring profile instead.</span></span> <span data-ttu-id="aa968-137">Un profil de score personnalisé accorde plus d’importance aux éléments qui avantagent votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="aa968-137">A custom scoring profile gives you a way to boost items that are more beneficial to your business.</span></span> <span data-ttu-id="aa968-138">Consultez [Ajout de profils de calcul de score](http://msdn.microsoft.com/library/azure/dn798928.aspx) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="aa968-138">See [Add a scoring profile](http://msdn.microsoft.com/library/azure/dn798928.aspx) for more information.</span></span> 
> 
> 

## <a name="faceted-navigation"></a><span data-ttu-id="aa968-139">Navigation à facettes</span><span class="sxs-lookup"><span data-stu-id="aa968-139">Faceted navigation</span></span>
<span data-ttu-id="aa968-140">Les options de navigation de recherche sont communes à toutes les pages de résultats et se trouvent souvent sur le côté ou en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="aa968-140">Search navigation is common on a results page, often located at the side or top of a page.</span></span> <span data-ttu-id="aa968-141">Dans Azure Search, la navigation à facettes permet une recherche autonome en fonction de filtres prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="aa968-141">In Azure Search, faceted navigation provides self-directed search based on predefined filters.</span></span> <span data-ttu-id="aa968-142">Consultez [Navigation à facettes dans Azure Search](search-faceted-navigation.md) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="aa968-142">See [Faceted navigation in Azure Search](search-faceted-navigation.md) for details.</span></span>

## <a name="filters-at-the-page-level"></a><span data-ttu-id="aa968-143">Filtres au niveau de la page</span><span class="sxs-lookup"><span data-stu-id="aa968-143">Filters at the page level</span></span>
<span data-ttu-id="aa968-144">Si votre solution inclut des pages de recherche dédiées à certains types de contenu (par exemple, une application de vente au détail en ligne avec des départements figurant en haut de la page), vous pouvez associer une expression de filtre à un événement **onClick** pour ouvrir une page préfiltrée.</span><span class="sxs-lookup"><span data-stu-id="aa968-144">If your solution design included dedicated search pages for specific types of content (for example, an online retail application that has departments listed at the top of the page), you can insert a filter expression alongside an **onClick** event to open a page in a prefiltered state.</span></span> 

<span data-ttu-id="aa968-145">Vous pouvez envoyer un filtre avec ou sans expression de recherche.</span><span class="sxs-lookup"><span data-stu-id="aa968-145">You can send a filter with or without a search expression.</span></span> <span data-ttu-id="aa968-146">Par exemple, la demande suivante applique un filtre en fonction du nom de la marque et ne renvoie que les documents correspondants.</span><span class="sxs-lookup"><span data-stu-id="aa968-146">For example, the following request will filter on brand name, returning only those documents that match it.</span></span>

        GET /indexes/onlineCatalog/docs?$filter=brandname eq ‘Microsoft’ and category eq ‘Games’

<span data-ttu-id="aa968-147">Consultez [Recherche de documents (API Recherche Azure)](http://msdn.microsoft.com/library/azure/dn798927.aspx) pour en savoir plus sur les expressions `$filter`.</span><span class="sxs-lookup"><span data-stu-id="aa968-147">See [Search Documents (Azure Search API)](http://msdn.microsoft.com/library/azure/dn798927.aspx) for more information about `$filter` expressions.</span></span>

## <a name="see-also"></a><span data-ttu-id="aa968-148">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="aa968-148">See Also</span></span>
* [<span data-ttu-id="aa968-149">API REST de service Azure Search</span><span class="sxs-lookup"><span data-stu-id="aa968-149">Azure Search Service REST API</span></span>](http://msdn.microsoft.com/library/azure/dn798935.aspx)
* [<span data-ttu-id="aa968-150">Opérations d’index</span><span class="sxs-lookup"><span data-stu-id="aa968-150">Index Operations</span></span>](http://msdn.microsoft.com/library/azure/dn798918.aspx)
* [<span data-ttu-id="aa968-151">Opérations de document</span><span class="sxs-lookup"><span data-stu-id="aa968-151">Document Operations</span></span>](http://msdn.microsoft.com/library/azure/dn800962.aspx)
* [<span data-ttu-id="aa968-152">Vidéos et didacticiels relatifs à Azure Search</span><span class="sxs-lookup"><span data-stu-id="aa968-152">Video and tutorials about Azure Search</span></span>](search-video-demo-tutorial-list.md)
* [<span data-ttu-id="aa968-153">Navigation à facettes dans Azure Search</span><span class="sxs-lookup"><span data-stu-id="aa968-153">Faceted Navigation in Azure Search</span></span>](search-faceted-navigation.md)

<!--Image references-->
[1]: ./media/search-pagination-page-layout/Pages-1-Viewing1ofNResults.PNG
[2]: ./media/search-pagination-page-layout/Pages-2-Tiled.PNG
[3]: ./media/search-pagination-page-layout/Pages-3-SortBy.png
[4]: ./media/search-pagination-page-layout/Pages-4-SortbyRelevance.png
[5]: ./media/search-pagination-page-layout/Pages-5-BuildSort.png 
