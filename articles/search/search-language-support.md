---
title: Recherche Azure multilingue | Microsoft Docs
description: Azure Search prend en charge 56 langages, tirant parti des analyseurs de langue de la technologie Lucene et Natural Language Processing de Microsoft.
services: search
documentationcenter: 
author: yahnoosh
manager: pablocas
editor: 
ms.assetid: 55a00b44-804d-41bb-9c96-e6ea498616f5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: jlembicz
ms.openlocfilehash: dbbab31bac66ce73dbf9883992713a2c16581e19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a><span data-ttu-id="9d12e-103">Création d’un index de documents dans plusieurs langues dans Azure Search</span><span class="sxs-lookup"><span data-stu-id="9d12e-103">Create an index for documents in multiple languages in Azure Search</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="9d12e-104">Portail</span><span class="sxs-lookup"><span data-stu-id="9d12e-104">Portal</span></span>](search-language-support.md)
> * [<span data-ttu-id="9d12e-105">REST</span><span class="sxs-lookup"><span data-stu-id="9d12e-105">REST</span></span>](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [<span data-ttu-id="9d12e-106">.NET</span><span class="sxs-lookup"><span data-stu-id="9d12e-106">.NET</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

<span data-ttu-id="9d12e-107">Décupler les performances des analyseurs de langue est aussi facile que de définir une propriété sur un champ de recherche dans la définition d'index.</span><span class="sxs-lookup"><span data-stu-id="9d12e-107">Unleashing the power of language analyzers is as easy as setting one property on a searchable field in the index definition.</span></span> <span data-ttu-id="9d12e-108">Maintenant, vous pouvez effectuer cette étape dans le portail.</span><span class="sxs-lookup"><span data-stu-id="9d12e-108">Now you can do this step in the portal.</span></span>

<span data-ttu-id="9d12e-109">Voici les captures d'écran des panneaux du portail Azure pour Azure Search qui permettent aux utilisateurs de définir un schéma d'index.</span><span class="sxs-lookup"><span data-stu-id="9d12e-109">Below are screenshots of the Azure Portal blades for Azure Search that allow users to define an index schema.</span></span> <span data-ttu-id="9d12e-110">À partir de ce panneau, les utilisateurs peuvent créer tous les champs et définir la propriété de l'analyseur pour chacun d'eux.</span><span class="sxs-lookup"><span data-stu-id="9d12e-110">From this blade, users can create all of the fields and set the analyzer property for each of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d12e-111">Vous pouvez uniquement définir un analyseur de langage lors de la définition du champ, comme lors de la création d'un nouvel index ou lorsque vous ajoutez un nouveau champ à un index existant.</span><span class="sxs-lookup"><span data-stu-id="9d12e-111">You can only set a language analyzer during field definition, as in when creating a new index from the ground up, or when adding a new field to an existing index.</span></span> <span data-ttu-id="9d12e-112">Veillez à spécifier entièrement tous les attributs, y compris l'analyseur, lors de la création du champ.</span><span class="sxs-lookup"><span data-stu-id="9d12e-112">Make sure you fully specify all attributes, including the analyzer, while creating the field.</span></span> <span data-ttu-id="9d12e-113">Vous ne pourrez pas modifier les attributs ou modifier le type d'analyseur une fois vos modifications enregistrées.</span><span class="sxs-lookup"><span data-stu-id="9d12e-113">You won't be able to edit the attributes or change the analyzer type once you save your changes.</span></span>
>
>

## <a name="define-a-new-field-definition"></a><span data-ttu-id="9d12e-114">Définir une nouvelle définition de champ</span><span class="sxs-lookup"><span data-stu-id="9d12e-114">Define a new field definition</span></span>
1. <span data-ttu-id="9d12e-115">Connectez-vous au [Portail Azure](https://portal.azure.com) et ouvrez le panneau de votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="9d12e-115">Sign in to the [Azure portal](https://portal.azure.com) and open the service blade of your search service.</span></span>
2. <span data-ttu-id="9d12e-116">Cliquez sur **Ajouter un index** dans la barre de commandes en haut du tableau de bord de service pour démarrer un nouvel index ou ouvrez un index existant pour définir un analyseur sur des nouveaux champs que vous ajoutez à un index existant.</span><span class="sxs-lookup"><span data-stu-id="9d12e-116">Click **Add index** in the command bar at the top of the service dashboard to start a new index, or open an existing index to set an analyzer on new fields you're adding to an existing index.</span></span>
3. <span data-ttu-id="9d12e-117">Le panneau Champs s'affiche. Il vous propose des options pour définir le schéma de l'index, y compris l'onglet Analyseur utilisé pour le choix d'un analyseur de langage.</span><span class="sxs-lookup"><span data-stu-id="9d12e-117">The Fields blade appears, giving you options for defining the schema of the index, including the Analyzer tab used for choosing a language analyzer.</span></span>
4. <span data-ttu-id="9d12e-118">Dans le panneau Champs, démarrez une définition de champ en fournissant un nom, le choix du type de données et la définition des attributs pour marquer le champ en tant que texte intégral consultable, récupérables dans les résultats de recherche, utilisable dans des structures de navigation de facette, pouvant être trié, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="9d12e-118">In Fields, start a field definition by providing a name, choosing the data type, and setting attributes to mark the field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.</span></span>
5. <span data-ttu-id="9d12e-119">Avant de passer au champ suivant, ouvrez l'onglet **Analyseur** .</span><span class="sxs-lookup"><span data-stu-id="9d12e-119">Before moving on to the next field, open the **Analyzer** tab.</span></span>

<span data-ttu-id="9d12e-120">![][1]
*Pour sélectionner un analyseur, cliquez sur l’onglet Analyseur du panneau Champs*</span><span class="sxs-lookup"><span data-stu-id="9d12e-120">![][1]
*To select an analyzer, click the Analyzer tab on the Fields blade*</span></span>

## <a name="choose-an-analyzer"></a><span data-ttu-id="9d12e-121">Choisir un analyseur</span><span class="sxs-lookup"><span data-stu-id="9d12e-121">Choose an analyzer</span></span>
1. <span data-ttu-id="9d12e-122">Faites défiler pour rechercher le champ que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="9d12e-122">Scroll to find the field you are defining.</span></span>
2. <span data-ttu-id="9d12e-123">Si vous n'avez pas activé le champ de recherche, cliquez sur la case à cocher pour indiquer qu'il peut **faire l'objet d'une recherche**.</span><span class="sxs-lookup"><span data-stu-id="9d12e-123">If you haven't marked the field as searchable, click the checkbox now to mark it as **Searchable**.</span></span>
3. <span data-ttu-id="9d12e-124">Cliquez sur la zone Analyseur pour afficher la liste des analyseurs disponibles.</span><span class="sxs-lookup"><span data-stu-id="9d12e-124">Click the Analyzer area to display the list of available analyzers.</span></span>
4. <span data-ttu-id="9d12e-125">Cliquez sur l'analyseur à utiliser.</span><span class="sxs-lookup"><span data-stu-id="9d12e-125">Choose the analyzer you want to use.</span></span>

<span data-ttu-id="9d12e-126">![][2]
*Sélectionnez un des analyseurs pris en charge pour chaque champ*</span><span class="sxs-lookup"><span data-stu-id="9d12e-126">![][2]
*Select one of the supported analyzers for each field*</span></span>

<span data-ttu-id="9d12e-127">Par défaut, tous les champs pouvant faire l'objet d'une recherche utilisent l' [analyseur Lucene Standard](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) qui est indépendant du langage.</span><span class="sxs-lookup"><span data-stu-id="9d12e-127">By default, all searchable fields use the [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic.</span></span> <span data-ttu-id="9d12e-128">Pour afficher la liste complète des analyseurs pris en charge, consultez [Prise en charge linguistique dans Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d12e-128">To view the full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span></span>

<span data-ttu-id="9d12e-129">Une fois que l'analyseur de langage est sélectionné pour un champ, il sera utilisé à chaque demande de recherche et d'indexation pour ce champ.</span><span class="sxs-lookup"><span data-stu-id="9d12e-129">Once the language analyzer is selected for a field, it will be used with each indexing and search request for that field.</span></span> <span data-ttu-id="9d12e-130">Lorsqu'une requête est émise sur plusieurs champs à l'aide de différents analyseurs, elle sera traitée indépendamment par les analyseurs corrects pour chaque champ.</span><span class="sxs-lookup"><span data-stu-id="9d12e-130">When a query is issued against multiple fields using different analyzers, the query will be processed independently by the right analyzers for each field.</span></span>

<span data-ttu-id="9d12e-131">Plusieurs applications web et mobiles servent les utilisateurs dans le monde entier à l'aide de différentes langues.</span><span class="sxs-lookup"><span data-stu-id="9d12e-131">Many web and mobile applications serve users around the globe using different languages.</span></span> <span data-ttu-id="9d12e-132">Il est possible de définir un index pour un scénario comme celui-ci en créant un champ pour chaque langue prise en charge.</span><span class="sxs-lookup"><span data-stu-id="9d12e-132">It’s possible to define an index for a scenario like this by creating a field for each language supported.</span></span>

<span data-ttu-id="9d12e-133">![][3]
*Définition d’index avec un champ de description pour chaque langue prise en charge*</span><span class="sxs-lookup"><span data-stu-id="9d12e-133">![][3]
*Index definition with a description field for each language supported*</span></span>

<span data-ttu-id="9d12e-134">Si la langue de l'agent d'émission d'une requête est connue, une demande de recherche peut être étendue à un champ spécifique à l'aide du paramètre de requête **searchFields** .</span><span class="sxs-lookup"><span data-stu-id="9d12e-134">If the language of the agent issuing a query is known, a search request can be scoped to a specific field using the **searchFields** query parameter.</span></span> <span data-ttu-id="9d12e-135">La requête suivante sera émise uniquement sur la description en polonais :</span><span class="sxs-lookup"><span data-stu-id="9d12e-135">The following query will be issued only against the description in Polish:</span></span>

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

<span data-ttu-id="9d12e-136">Vous pouvez interroger votre index à partir du portail en utilisant l **’Explorateur de recherche** pour coller une requête similaire à celle présentée ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="9d12e-136">You can query your index from the portal, using **Search explorer** to paste in a query similar to the one shown above.</span></span> <span data-ttu-id="9d12e-137">L’Explorateur de recherche est disponible dans la barre de commandes du panneau de service.</span><span class="sxs-lookup"><span data-stu-id="9d12e-137">Search explorer is available from the command bar in the service blade.</span></span> <span data-ttu-id="9d12e-138">Pour plus d’informations, consultez l’article [Interroger votre index Azure Search dans le portail](search-explorer.md) .</span><span class="sxs-lookup"><span data-stu-id="9d12e-138">See [Query your Azure Search index in the portal](search-explorer.md) for details.</span></span>

<span data-ttu-id="9d12e-139">Parfois, la langue de l'agent d'émission d'une requête n'est pas connue, auquel cas la requête peut être exécutée simultanément sur tous les champs.</span><span class="sxs-lookup"><span data-stu-id="9d12e-139">Sometimes the language of the agent issuing a query is not known, in which case the query can be issued against all fields simultaneously.</span></span> <span data-ttu-id="9d12e-140">Si nécessaire, la préférence de résultats dans une langue donnée peut être définie à l'aide des [profils de score](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d12e-140">If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span> <span data-ttu-id="9d12e-141">Dans l'exemple ci-dessous, les correspondances trouvées dans la description en anglais auront un score supérieur par rapport aux correspondances en polonais et en français :</span><span class="sxs-lookup"><span data-stu-id="9d12e-141">In the example below, matches found in the description in English will be scored higher relative to matches in Polish and French:</span></span>

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

<span data-ttu-id="9d12e-142">Si vous êtes un développeur .NET, notez que vous pouvez configurer les analyseurs de langage à l'aide du [Kit de développement logiciel (SDK) Azure Search .NET](http://www.nuget.org/packages/Microsoft.Azure.Search).</span><span class="sxs-lookup"><span data-stu-id="9d12e-142">If you're a .NET developer, note that you can configure language analyzers using the [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span></span> <span data-ttu-id="9d12e-143">La dernière version prend également en charge les analyseurs de langage Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9d12e-143">The latest release includes support for the Microsoft language analyzers as well.</span></span>

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
