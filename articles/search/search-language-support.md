---
title: aaaAzure multilingue recherche | Documents Microsoft
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
ms.openlocfilehash: 9a2e567a82ee563521c12ea320f6c484a8e73f04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a><span data-ttu-id="fd8bc-103">Création d’un index de documents dans plusieurs langues dans Azure Search</span><span class="sxs-lookup"><span data-stu-id="fd8bc-103">Create an index for documents in multiple languages in Azure Search</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="fd8bc-104">Portail</span><span class="sxs-lookup"><span data-stu-id="fd8bc-104">Portal</span></span>](search-language-support.md)
> * [<span data-ttu-id="fd8bc-105">REST</span><span class="sxs-lookup"><span data-stu-id="fd8bc-105">REST</span></span>](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [<span data-ttu-id="fd8bc-106">.NET</span><span class="sxs-lookup"><span data-stu-id="fd8bc-106">.NET</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

<span data-ttu-id="fd8bc-107">Unleashing power hello des analyseurs de langage est aussi simple que la propriété d’un paramètre sur un champ de recherche dans la définition de l’index hello.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-107">Unleashing hello power of language analyzers is as easy as setting one property on a searchable field in hello index definition.</span></span> <span data-ttu-id="fd8bc-108">Maintenant, vous pouvez effectuer cette étape dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-108">Now you can do this step in hello portal.</span></span>

<span data-ttu-id="fd8bc-109">Vous trouverez ci-dessous des captures d’écran de hello panneaux du portail Azure pour Azure Search qui permettent aux utilisateurs toodefine un schéma d’index.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-109">Below are screenshots of hello Azure Portal blades for Azure Search that allow users toodefine an index schema.</span></span> <span data-ttu-id="fd8bc-110">À partir de ce panneau, les utilisateurs peuvent créer tous les champs de hello et définir la propriété d’analyseur hello pour chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-110">From this blade, users can create all of hello fields and set hello analyzer property for each of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fd8bc-111">Vous pouvez uniquement définir un analyseur de langue lors de la définition de champ, comme dans lors de la création d’un nouvel index à partir de hello d’arrière-plan, ou lors de l’ajout d’un index existant de nouveau champ tooan.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-111">You can only set a language analyzer during field definition, as in when creating a new index from hello ground up, or when adding a new field tooan existing index.</span></span> <span data-ttu-id="fd8bc-112">Assurez-vous que vous spécifiez entièrement tous les attributs, y compris l’Analyseur de hello, lors de la création du champ de hello.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-112">Make sure you fully specify all attributes, including hello analyzer, while creating hello field.</span></span> <span data-ttu-id="fd8bc-113">Vous ne seront pas être en mesure de tooedit les attributs hello ou modifier le type d’analyseur hello une fois que vous enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-113">You won't be able tooedit hello attributes or change hello analyzer type once you save your changes.</span></span>
>
>

## <a name="define-a-new-field-definition"></a><span data-ttu-id="fd8bc-114">Définir une nouvelle définition de champ</span><span class="sxs-lookup"><span data-stu-id="fd8bc-114">Define a new field definition</span></span>
1. <span data-ttu-id="fd8bc-115">Connectez-vous à toohello [portail Azure](https://portal.azure.com) et panneau de service hello ouverte de votre service de recherche.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-115">Sign in toohello [Azure portal](https://portal.azure.com) and open hello service blade of your search service.</span></span>
2. <span data-ttu-id="fd8bc-116">Cliquez sur **ajouter un index** dans la commande hello barre haut hello toostart de tableau de bord de service hello un nouvel index, ou ouvrez un tooset index existants sur les nouveaux champs que vous ajoutez un analyseur de tooan l’index existant.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-116">Click **Add index** in hello command bar at hello top of hello service dashboard toostart a new index, or open an existing index tooset an analyzer on new fields you're adding tooan existing index.</span></span>
3. <span data-ttu-id="fd8bc-117">Panneau de champs Hello s’affiche, vous propose des options pour la définition de schéma hello d’index de hello, y compris hello analyseur onglet utilisé pour le choix d’un analyseur de langage.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-117">hello Fields blade appears, giving you options for defining hello schema of hello index, including hello Analyzer tab used for choosing a language analyzer.</span></span>
4. <span data-ttu-id="fd8bc-118">Dans les champs, démarrez une définition de champ en fournissant un nom, en choisissant le type de données hello et en définissant consultables, récupérables dans les résultats de recherche, utilisables dans des structures de navigation de facette, champ de hello toomark attributs sous forme de texte complète pouvant être trié et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-118">In Fields, start a field definition by providing a name, choosing hello data type, and setting attributes toomark hello field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.</span></span>
5. <span data-ttu-id="fd8bc-119">Avant de le déplacer sur le champ suivant de toohello, ouvrez hello **analyseur** onglet.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-119">Before moving on toohello next field, open hello **Analyzer** tab.</span></span>

<span data-ttu-id="fd8bc-120">![][1]
*tooselect un analyseur, cliquez sur l’onglet d’Analyseur de hello dans Panneau de champs hello*</span><span class="sxs-lookup"><span data-stu-id="fd8bc-120">![][1]
*tooselect an analyzer, click hello Analyzer tab on hello Fields blade*</span></span>

## <a name="choose-an-analyzer"></a><span data-ttu-id="fd8bc-121">Choisir un analyseur</span><span class="sxs-lookup"><span data-stu-id="fd8bc-121">Choose an analyzer</span></span>
1. <span data-ttu-id="fd8bc-122">Faites défiler le champ de hello toofind que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-122">Scroll toofind hello field you are defining.</span></span>
2. <span data-ttu-id="fd8bc-123">Si vous n’avez pas marqué comme champ hello en tant que recherche, cliquez sur hello case à cocher maintenant toomark en tant que **Searchable**.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-123">If you haven't marked hello field as searchable, click hello checkbox now toomark it as **Searchable**.</span></span>
3. <span data-ttu-id="fd8bc-124">Cliquez sur hello analyseur zone toodisplay hello liste des analyseurs de disponibles.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-124">Click hello Analyzer area toodisplay hello list of available analyzers.</span></span>
4. <span data-ttu-id="fd8bc-125">Choisissez l’Analyseur de hello souhaité toouse.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-125">Choose hello analyzer you want toouse.</span></span>

<span data-ttu-id="fd8bc-126">![][2]
*Sélectionnez un des analyseurs hello pris en charge pour chaque champ.*</span><span class="sxs-lookup"><span data-stu-id="fd8bc-126">![][2]
*Select one of hello supported analyzers for each field*</span></span>

<span data-ttu-id="fd8bc-127">Par défaut, tous les champs interrogeables utilisent hello [Lucene Standard analyseur](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) qui est indépendant du langage.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-127">By default, all searchable fields use hello [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic.</span></span> <span data-ttu-id="fd8bc-128">liste complète de hello tooview de prise en charge des analyseurs, consultez [prise en charge linguistique dans Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd8bc-128">tooview hello full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span></span>

<span data-ttu-id="fd8bc-129">Une fois que l’Analyseur de langue hello est sélectionnée pour un champ, il sera utilisé avec chaque demande de recherche et d’indexation pour ce champ.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-129">Once hello language analyzer is selected for a field, it will be used with each indexing and search request for that field.</span></span> <span data-ttu-id="fd8bc-130">Lorsqu’une requête est émise par rapport à plusieurs champs à l’aide de différents analyseurs, hello requête ne sera traitée indépendamment par des analyseurs de droite hello pour chaque champ.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-130">When a query is issued against multiple fields using different analyzers, hello query will be processed independently by hello right analyzers for each field.</span></span>

<span data-ttu-id="fd8bc-131">Plusieurs applications web et mobiles servent utilisateurs monde hello, à l’aide de différentes langues.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-131">Many web and mobile applications serve users around hello globe using different languages.</span></span> <span data-ttu-id="fd8bc-132">Il est possible de toodefine un index pour un scénario à ceci en créant un champ pour chaque langue prise en charge.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-132">It’s possible toodefine an index for a scenario like this by creating a field for each language supported.</span></span>

<span data-ttu-id="fd8bc-133">![][3]
*Définition d'index avec un champ de description pour chaque langue prise en charge*</span><span class="sxs-lookup"><span data-stu-id="fd8bc-133">![][3]
*Index definition with a description field for each language supported*</span></span>

<span data-ttu-id="fd8bc-134">Si la langue hello d’agent hello émission d’une requête est connu, une demande de recherche peut être étendue tooa champ spécifique à l’aide de hello **searchFields** paramètre de requête.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-134">If hello language of hello agent issuing a query is known, a search request can be scoped tooa specific field using hello **searchFields** query parameter.</span></span> <span data-ttu-id="fd8bc-135">Hello requête suivante va être émise uniquement par rapport à la description de hello en polonais :</span><span class="sxs-lookup"><span data-stu-id="fd8bc-135">hello following query will be issued only against hello description in Polish:</span></span>

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

<span data-ttu-id="fd8bc-136">Vous pouvez interroger votre index à partir du portail de hello, à l’aide de **rechercher dans l’Explorateur** toopaste dans un toohello similaire requête celle qui précède.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-136">You can query your index from hello portal, using **Search explorer** toopaste in a query similar toohello one shown above.</span></span> <span data-ttu-id="fd8bc-137">Rechercher dans l’Explorateur est disponible à partir de la barre de commandes hello dans le panneau de service hello.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-137">Search explorer is available from hello command bar in hello service blade.</span></span> <span data-ttu-id="fd8bc-138">Consultez [interroger votre index Azure Search dans le portail de hello](search-explorer.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-138">See [Query your Azure Search index in hello portal](search-explorer.md) for details.</span></span>

<span data-ttu-id="fd8bc-139">Parfois hello langue de l’agent hello en émettant une requête ne connaît pas, dans quels cas hello les requête peut être exécutée simultanément sur tous les champs.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-139">Sometimes hello language of hello agent issuing a query is not known, in which case hello query can be issued against all fields simultaneously.</span></span> <span data-ttu-id="fd8bc-140">Si nécessaire, la préférence de résultats dans une langue donnée peut être définie à l'aide des [profils de score](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd8bc-140">If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span> <span data-ttu-id="fd8bc-141">Dans l’exemple hello ci-dessous, correspondances trouvées dans la description de hello en anglais auront un score supérieur toomatches relatif dans polonais et Français :</span><span class="sxs-lookup"><span data-stu-id="fd8bc-141">In hello example below, matches found in hello description in English will be scored higher relative toomatches in Polish and French:</span></span>

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

<span data-ttu-id="fd8bc-142">Si vous êtes un développeur de .NET, notez que vous pouvez configurer les analyseurs de langage à l’aide de hello [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span><span class="sxs-lookup"><span data-stu-id="fd8bc-142">If you're a .NET developer, note that you can configure language analyzers using hello [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span></span> <span data-ttu-id="fd8bc-143">Hello dernière version inclut la prise en charge des analyseurs de langage Microsoft hello également.</span><span class="sxs-lookup"><span data-stu-id="fd8bc-143">hello latest release includes support for hello Microsoft language analyzers as well.</span></span>

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
