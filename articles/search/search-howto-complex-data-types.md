---
title: "types de données complexes aaaHow toomodel dans Azure Search | Documents Microsoft"
description: "Les structures de données imbriquées ou hiérarchiques peuvent être modélisées dans un index Recherche Azure à l’aide d’un ensemble de lignes aplati et du type de données Collection."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: complex data types; compound data types; aggregate data types
ms.assetid: e4bf86b4-497a-4179-b09f-c1b56c3c0bb2
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: b330c5b322f4f33123a454be11733b977684b9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomodel-complex-data-types-in-azure-search"></a><span data-ttu-id="43af2-103">Comment des types de données complexes de toomodel dans Azure Search</span><span class="sxs-lookup"><span data-stu-id="43af2-103">How toomodel complex data types in Azure Search</span></span>
<span data-ttu-id="43af2-104">Jeux de données externes utilisées toopopulate un index Azure Search incluent parfois sous-structures hiérarchiques ou imbriquées qui ne désactiver parfaitement dans un ensemble de lignes tabulaire.</span><span class="sxs-lookup"><span data-stu-id="43af2-104">External datasets used toopopulate an Azure Search index sometimes include hierarchical or nested substructures that do not break down neatly into a tabular rowset.</span></span> <span data-ttu-id="43af2-105">Des exemples de telles structures incluent les emplacements et les numéros de téléphone multiples pour un même client, les couleurs et les tailles multiples pour une même référence, les auteurs multiples pour un même livre, etc.</span><span class="sxs-lookup"><span data-stu-id="43af2-105">Examples of such structures might include multiple locations and phone numbers for a single customer, multiple colors and sizes for a single SKU, multiple authors of a single book, and so on.</span></span> <span data-ttu-id="43af2-106">En termes de modélisation, vous pouvez voir ces structures visés tooas *types de données complexes*, *composée des types de données*, *types de données composites*, ou *d’agrégation types de données*, tooname quelques.</span><span class="sxs-lookup"><span data-stu-id="43af2-106">In modeling terms, you might see these structures referred tooas *complex data types*, *compound data types*, *composite data types*, or *aggregate data types*, tooname a few.</span></span>

<span data-ttu-id="43af2-107">Types de données complexes ne sont pas pris en charge en mode natif dans Azure Search, mais une excellente solution de contournement inclut un processus en deux étapes de mise à plat de la structure de hello, puis en utilisant un **Collection** structure intérieurs de hello tooreconstitute de type de données.</span><span class="sxs-lookup"><span data-stu-id="43af2-107">Complex data types are not natively supported in Azure Search, but a proven workaround includes a two-step process of flattening hello structure and then using a **Collection** data type tooreconstitute hello interior structure.</span></span> <span data-ttu-id="43af2-108">Technique de hello décrite dans cet article permet toobe de contenu hello recherchée, à facettes, filtrées et triées.</span><span class="sxs-lookup"><span data-stu-id="43af2-108">Following hello technique described in this article allows hello content toobe searched, faceted, filtered, and sorted.</span></span>

## <a name="example-of-a-complex-data-structure"></a><span data-ttu-id="43af2-109">Exemple d’une structure de données complexe</span><span class="sxs-lookup"><span data-stu-id="43af2-109">Example of a complex data structure</span></span>
<span data-ttu-id="43af2-110">En règle générale, les données de salutation en question résident en tant qu’ensemble de documents JSON ou XML, ou en tant qu’éléments dans une banque NoSQL comme base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="43af2-110">Typically, hello data in question resides as a set of JSON or XML documents, or as items in a NoSQL store such as Azure Cosmos DB.</span></span> <span data-ttu-id="43af2-111">Point de vue structurel, défi de hello provient d’avoir plusieurs éléments enfants qui doivent toobe recherché et filtré.</span><span class="sxs-lookup"><span data-stu-id="43af2-111">Structurally, hello challenge stems from having multiple child items that need toobe searched and filtered.</span></span>  <span data-ttu-id="43af2-112">Comme point de départ pour illustrer la solution de contournement hello, prenez hello suivant du document JSON qui répertorie un ensemble de contacts, par exemple :</span><span class="sxs-lookup"><span data-stu-id="43af2-112">As a starting point for illustrating hello workaround, take hello following JSON document that lists a set of contacts as an example:</span></span>

~~~~~
[
  {
    "id": "1",
    "name": "John Smith",
    "company": "Adventureworks",
    "locations": [
      {
        "id": "1",
        "description": "Adventureworks Headquarters"
      },
      {
        "id": "2",
        "description": "Home Office"
      }
    ]
  }, 
  {
    "id": "2",
    "name": "Jen Campbell",
    "company": "Northwind",
    "locations": [
      {
        "id": "3",
        "description": "Northwind Headquarter"
      },
      {
        "id": "4",
        "description": "Home Office"
      }
    ]
}]
~~~~~

<span data-ttu-id="43af2-113">Alors que les champs hello nommée « id », « name » et « société » peuvent facilement être mappés un à un en tant que champs dans un index Azure Search, champ de « emplacements » hello contient un tableau d’emplacements, les deux un ensemble d’identificateurs de localisation, ainsi que des descriptions de l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="43af2-113">While hello fields named ‘id’, ‘name’ and ‘company’ can easily be mapped one-to-one as fields within an Azure Search index, hello ‘locations’ field contains an array of locations, having both a set of location IDs as well as location descriptions.</span></span> <span data-ttu-id="43af2-114">Étant donné que Azure Search n’a pas un type de données qui prend en charge, nous avons besoin un toomodel de manière différente dans Azure Search.</span><span class="sxs-lookup"><span data-stu-id="43af2-114">Given that Azure Search does not have a data type that supports this, we need a different way toomodel this in Azure Search.</span></span> 

> [!NOTE]
> <span data-ttu-id="43af2-115">Cette technique est également décrit par Kirk Evans dans un billet de blog [l’indexation de DocumentDB avec Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), qui montre une technique appelée « aplatissement hello données », dans laquelle vous aurait un champ appelé `locationsID` et `locationsDescription` qui sont tous deux [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (ou un tableau de chaînes).</span><span class="sxs-lookup"><span data-stu-id="43af2-115">This technique is also described by Kirk Evans in a blog post [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), which shows a technique called "flattening hello data", whereby you would have a field called `locationsID` and `locationsDescription` that are both [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span>   
> 
> 

## <a name="part-1-flatten-hello-array-into-individual-fields"></a><span data-ttu-id="43af2-116">Partie 1 : Aplanir un tableau de hello dans des champs individuels</span><span class="sxs-lookup"><span data-stu-id="43af2-116">Part 1: Flatten hello array into individual fields</span></span>
<span data-ttu-id="43af2-117">toocreate un index Azure Search adapté à ce jeu de données, créer des champs individuels de sous-structure imbriqués de hello : `locationsID` et `locationsDescription` avec un type de données [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (ou un tableau de chaînes).</span><span class="sxs-lookup"><span data-stu-id="43af2-117">toocreate an Azure Search index that accommodates this dataset, create individual fields for hello nested substructure: `locationsID` and `locationsDescription` with a data type of [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span> <span data-ttu-id="43af2-118">Dans ces champs vous serez valeurs d’index hello '1' et '2' dans hello `locationsID` champ pour les valeurs de John Smith et hello '3' & '4' dans hello `locationsID` champ Jen Campbell.</span><span class="sxs-lookup"><span data-stu-id="43af2-118">In these fields you would index hello values ‘1’ and ‘2’ into hello `locationsID` field for John Smith and hello values ‘3’ & ‘4’ into hello `locationsID` field for Jen Campbell.</span></span>  

<span data-ttu-id="43af2-119">Vos données dans Recherche Azure présentent l’aspect suivant :</span><span class="sxs-lookup"><span data-stu-id="43af2-119">Your data within Azure Search would look like this:</span></span> 

![Exemple de données, 2 lignes](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-hello-index-definition"></a><span data-ttu-id="43af2-121">Partie 2 : Ajouter un champ de regroupement dans la définition d’index hello</span><span class="sxs-lookup"><span data-stu-id="43af2-121">Part 2: Add a collection field in hello index definition</span></span>
<span data-ttu-id="43af2-122">Dans le schéma d’index hello, les définitions de champ hello peut se présenter exemple toothis similaire.</span><span class="sxs-lookup"><span data-stu-id="43af2-122">In hello index schema, hello field definitions might look similar toothis example.</span></span>

~~~~
var index = new Index()
{
    Name = indexName,
    Fields = new[]
    {
        new Field("id", DataType.String) { IsKey = true },
        new Field("name", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("company", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("locationsId", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true },
        new Field("locationsDescription", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true }
    }
};
~~~~

## <a name="validate-search-behaviors-and-optionally-extend-hello-index"></a><span data-ttu-id="43af2-123">Valider les comportements de recherche et d’éventuellement étendre les index hello</span><span class="sxs-lookup"><span data-stu-id="43af2-123">Validate search behaviors and optionally extend hello index</span></span>
<span data-ttu-id="43af2-124">Si vous indexez hello créé et les données de hello chargé, vous pouvez maintenant tester hello solution tooverify recherche l’exécution des requêtes sur hello le jeu de données.</span><span class="sxs-lookup"><span data-stu-id="43af2-124">Assuming you created hello index and loaded hello data, you can now test hello solution tooverify search query execution against hello dataset.</span></span> <span data-ttu-id="43af2-125">Chaque champ **collection** doit **pouvoir faire l’objet de recherches**, être **filtrable** et **à choix multiples**.</span><span class="sxs-lookup"><span data-stu-id="43af2-125">Each **collection** field should be **searchable**, **filterable** and **facetable**.</span></span> <span data-ttu-id="43af2-126">Vous devez être en mesure de toorun des requêtes comme :</span><span class="sxs-lookup"><span data-stu-id="43af2-126">You should be able toorun queries like:</span></span>

* <span data-ttu-id="43af2-127">Trouver toutes les personnes qui travaillent à hello « Siège social de Adventureworks ».</span><span class="sxs-lookup"><span data-stu-id="43af2-127">Find all people who work at hello ‘Adventureworks Headquarters’.</span></span>
* <span data-ttu-id="43af2-128">Obtention d’un nombre du nombre de hello de personnes qui travaillent dans un bureau « accueil ».</span><span class="sxs-lookup"><span data-stu-id="43af2-128">Get a count of hello number of people who work in a ‘Home Office’.</span></span>  
* <span data-ttu-id="43af2-129">De hello personnes travaillant dans un bureau d’accueil, afficher les autres bureaux elles fonctionnent en même temps que le nombre de personnes hello dans chaque emplacement.</span><span class="sxs-lookup"><span data-stu-id="43af2-129">Of hello people who work at a ‘Home Office’, show what other offices they work along with a count of hello people in each location.</span></span>  

<span data-ttu-id="43af2-130">Où cette technique réduit à néant est lorsque vous devez toodo une recherche qui combine des id d’emplacement hello ainsi que description de l’emplacement hello.</span><span class="sxs-lookup"><span data-stu-id="43af2-130">Where this technique falls apart is when you need toodo a search that combines both hello location id as well as hello location description.</span></span> <span data-ttu-id="43af2-131">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="43af2-131">For example:</span></span>

* <span data-ttu-id="43af2-132">Trouver toutes les personnes qui font du télétravail et dont l’ID d’emplacement est 4.</span><span class="sxs-lookup"><span data-stu-id="43af2-132">Find all people where they have a Home Office AND has a location ID of 4.</span></span>  

<span data-ttu-id="43af2-133">Si vous vous souvenez de contenu d’origine de hello présentait ainsi :</span><span class="sxs-lookup"><span data-stu-id="43af2-133">If you recall hello original content looked like this:</span></span>

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

<span data-ttu-id="43af2-134">Toutefois, maintenant que nous avons séparées par des données de salutation dans des champs distincts, nous n’avons aucun moyen de savoir si hello particuliers pour Jen Campbell concerne trop`locationsID 3` ou `locationsID 4`.</span><span class="sxs-lookup"><span data-stu-id="43af2-134">However, now that we have separated hello data into separate fields, we have no way of knowing if hello Home Office for Jen Campbell relates too`locationsID 3` or `locationsID 4`.</span></span>  

<span data-ttu-id="43af2-135">toohandle ce cas, définissez un autre champ dans l’index hello qui combine toutes les données de hello en une collection unique.</span><span class="sxs-lookup"><span data-stu-id="43af2-135">toohandle this case, define another field in hello index that combines all of hello data into a single collection.</span></span>  <span data-ttu-id="43af2-136">Dans notre exemple, nous appellerons ce champ `locationsCombined` et nous allons séparer contenu hello avec un `||` bien que vous pouvez choisir n’importe quel séparateur que vous pensez serait un jeu unique de caractères pour votre contenu.</span><span class="sxs-lookup"><span data-stu-id="43af2-136">For our example, we will call this field `locationsCombined` and we will separate hello content with a `||` although you can choose any separator that you think would be a unique set of characters for your content.</span></span> <span data-ttu-id="43af2-137">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="43af2-137">For example:</span></span> 

![Exemple de données, 2 lignes avec séparateur](./media/search-howto-complex-data-types/sample-data-2.png)

<span data-ttu-id="43af2-139">À l’aide de ce champ `locationsCombined` , nous pouvons maintenant effectuer davantage de requêtes, telles que :</span><span class="sxs-lookup"><span data-stu-id="43af2-139">Using this `locationsCombined` field, we can now accommodate even more queries, such as:</span></span>

* <span data-ttu-id="43af2-140">Afficher le nombre de personnes qui font du télétravail et dont l’ID d’emplacement est 4.</span><span class="sxs-lookup"><span data-stu-id="43af2-140">Show a count of people who work at a ‘Home Office’ with location Id of ‘4’.</span></span>  
* <span data-ttu-id="43af2-141">Rechercher les personnes qui font du télétravail et dont l’ID d’emplacement est 4.</span><span class="sxs-lookup"><span data-stu-id="43af2-141">Search for people who work at a ‘Home Office’ with location Id ‘4’.</span></span> 

## <a name="limitations"></a><span data-ttu-id="43af2-142">Limitations</span><span class="sxs-lookup"><span data-stu-id="43af2-142">Limitations</span></span>
<span data-ttu-id="43af2-143">Cette technique est utile pour un certain nombre de scénarios, mais elle n’est pas applicable dans tous les cas.</span><span class="sxs-lookup"><span data-stu-id="43af2-143">This technique is useful for a number of scenarios, but it is not applicable in every case.</span></span>  <span data-ttu-id="43af2-144">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="43af2-144">For example:</span></span>

1. <span data-ttu-id="43af2-145">Si vous n’avez pas d’un ensemble statique de champs dans votre type de données complexe et il n’a aucun toomap de façon possible de hello tous les types de champ tooa.</span><span class="sxs-lookup"><span data-stu-id="43af2-145">If you do not have a static set of fields in your complex data type and there was no way toomap all hello possible types tooa single field.</span></span> 
2. <span data-ttu-id="43af2-146">Mise à jour des objets de hello imbriqué requiert certains toodetermine travail supplémentaire à exactement ce qui doit toobe mis à jour dans l’index de recherche de Azure hello</span><span class="sxs-lookup"><span data-stu-id="43af2-146">Updating hello nested objects requires some extra work toodetermine exactly what needs toobe updated in hello Azure Search index</span></span>

## <a name="sample-code"></a><span data-ttu-id="43af2-147">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="43af2-147">Sample code</span></span>
<span data-ttu-id="43af2-148">Vous pouvez afficher un exemple de comment tooindex un complexes JSON jeu de données dans Azure Search et effectuer un nombre de requêtes sur ce jeu de données sur ce [référentiel GitHub](https://github.com/liamca/AzureSearchComplexTypes).</span><span class="sxs-lookup"><span data-stu-id="43af2-148">You can see an example on how tooindex a complex JSON data set into Azure Search and perform a number of queries over this dataset at this [GitHub repo](https://github.com/liamca/AzureSearchComplexTypes).</span></span>

## <a name="next-step"></a><span data-ttu-id="43af2-149">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="43af2-149">Next step</span></span>
<span data-ttu-id="43af2-150">[Vote pour la prise en charge native pour les types de données complexes](https://feedback.azure.com/forums/263029-azure-search) sur hello Azure recherche UserVoice page et fournir une entrée supplémentaire que vous souhaitez que nous tooconsider concernant l’implémentation des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="43af2-150">[Vote for native support for complex data types](https://feedback.azure.com/forums/263029-azure-search) on hello Azure Search UserVoice page and provide any additional input that you’d like us tooconsider regarding feature implementation.</span></span> <span data-ttu-id="43af2-151">Vous pouvez également contacter toome directement sur Twitter à @liamca.</span><span class="sxs-lookup"><span data-stu-id="43af2-151">You can also reach out toome directly on Twitter at @liamca.</span></span>

