---
title: aaaUpgrading toohello Azure Search .NET SDK version 1.1 | Documents Microsoft
description: "La mise à niveau toohello Azure Search .NET SDK version 1.1"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 66f89958-a320-4a24-87f9-69315848909f
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 291ae5731546e47b3c22c721d3552a79bdea80c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-net-sdk-version-3"></a><span data-ttu-id="63f82-103">La mise à niveau toohello Azure Search .NET SDK version 3</span><span class="sxs-lookup"><span data-stu-id="63f82-103">Upgrading toohello Azure Search .NET SDK version 3</span></span>
<span data-ttu-id="63f82-104">Si vous utilisez une version préliminaire de la version 2.0 ou antérieure de hello [Azure Search .NET SDK](https://aka.ms/search-sdk), cet article va vous aider à mettre à niveau votre version de toouse application 3.</span><span class="sxs-lookup"><span data-stu-id="63f82-104">If you're using version 2.0-preview or older of hello [Azure Search .NET SDK](https://aka.ms/search-sdk), this article will help you upgrade your application toouse version 3.</span></span>

<span data-ttu-id="63f82-105">Pour une procédure pas à pas plus de hello SDK, y compris des exemples, consultez [comment toouse Azure recherche à partir d’une Application .NET](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="63f82-105">For a more general walkthrough of hello SDK including examples, see [How toouse Azure Search from a .NET Application](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="63f82-106">Version 3 du hello Azure Search .NET SDK contient des modifications à partir de versions antérieures.</span><span class="sxs-lookup"><span data-stu-id="63f82-106">Version 3 of hello Azure Search .NET SDK contains some changes from earlier versions.</span></span> <span data-ttu-id="63f82-107">Elles sont pour la plupart mineures, et donc, la modification de votre code devrait ne nécessiter que peu d’effort.</span><span class="sxs-lookup"><span data-stu-id="63f82-107">These are mostly minor, so changing your code should require only minimal effort.</span></span> <span data-ttu-id="63f82-108">Consultez [étapes tooupgrade](#UpgradeSteps) pour obtenir des instructions sur la façon de toochange votre code toouse hello nouvelle SDK version.</span><span class="sxs-lookup"><span data-stu-id="63f82-108">See [Steps tooupgrade](#UpgradeSteps) for instructions on how toochange your code toouse hello new SDK version.</span></span>

> [!NOTE]
> <span data-ttu-id="63f82-109">Si vous utilisez la version 1.0.2-preview ou antérieure, vous devez mettre à niveau tooversion 1.1 premier et, puis mettre à niveau tooversion 3.</span><span class="sxs-lookup"><span data-stu-id="63f82-109">If you're using version 1.0.2-preview or older, you should upgrade tooversion 1.1 first, and then upgrade tooversion 3.</span></span> <span data-ttu-id="63f82-110">Consultez [annexe : étapes tooupgrade tooversion 1.1](#UpgradeStepsV1) pour obtenir des instructions.</span><span class="sxs-lookup"><span data-stu-id="63f82-110">See [Appendix: Steps tooupgrade tooversion 1.1](#UpgradeStepsV1) for instructions.</span></span>
>
> <span data-ttu-id="63f82-111">Votre instance du service Azure Search prend en charge plusieurs versions de l’API REST, y compris hello version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="63f82-111">Your Azure Search service instance supports several REST API versions, including hello latest one.</span></span> <span data-ttu-id="63f82-112">Vous pouvez continuer toouse une version lorsqu’il n’est plus hello version la plus récente, mais nous vous recommandons de migrer votre code toouse hello dernière version.</span><span class="sxs-lookup"><span data-stu-id="63f82-112">You can continue toouse a version when it is no longer hello latest one, but we recommend that you migrate your code toouse hello newest version.</span></span> <span data-ttu-id="63f82-113">Lorsque vous utilisez l’API REST de hello, vous devez spécifier la version de l’API hello dans chaque demande via un paramètre de version de l’api hello.</span><span class="sxs-lookup"><span data-stu-id="63f82-113">When using hello REST API, you must specify hello API version in every request via hello api-version parameter.</span></span> <span data-ttu-id="63f82-114">Lorsque vous utilisez hello .NET SDK, version hello Hello SDK que vous utilisez détermine hello correspond à la version de l’API REST de hello.</span><span class="sxs-lookup"><span data-stu-id="63f82-114">When using hello .NET SDK, hello version of hello SDK you’re using determines hello corresponding version of hello REST API.</span></span> <span data-ttu-id="63f82-115">Si vous utilisez un kit de développement plus anciens, vous pouvez continuer toorun que le code sans aucune modification même si le service de hello est mis à niveau toosupport une API la plus récente version.</span><span class="sxs-lookup"><span data-stu-id="63f82-115">If you are using an older SDK, you can continue toorun that code with no changes even if hello service is upgraded toosupport a newer API version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a><span data-ttu-id="63f82-116">Nouveautés de la version 3</span><span class="sxs-lookup"><span data-stu-id="63f82-116">What's new in version 3</span></span>
<span data-ttu-id="63f82-117">Version 3 du Bonjour Azure Search .NET SDK cibles Bonjour dernière version disponible de hello API REST de Azure Search, spécifiquement 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="63f82-117">Version 3 of hello Azure Search .NET SDK targets hello latest generally available version of hello Azure Search REST API, specifically 2016-09-01.</span></span> <span data-ttu-id="63f82-118">Cela rend possible toouse nombreuses nouvelles fonctionnalités d’Azure Search à partir d’une application .NET, y compris hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="63f82-118">This makes it possible toouse many new features of Azure Search from a .NET application, including hello following:</span></span>

* [<span data-ttu-id="63f82-119">Analyseurs personnalisés</span><span class="sxs-lookup"><span data-stu-id="63f82-119">Custom analyzers</span></span>](https://aka.ms/customanalyzers)
* <span data-ttu-id="63f82-120">Prise en charge des indexeurs [Stockage Blob Azure](search-howto-indexing-azure-blob-storage.md) et [Stockage Table Azure](search-howto-indexing-azure-tables.md)</span><span class="sxs-lookup"><span data-stu-id="63f82-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexer support</span></span>
* <span data-ttu-id="63f82-121">Personnalisation des indexeurs avec les [mappages de champs](search-indexer-field-mappings.md)</span><span class="sxs-lookup"><span data-stu-id="63f82-121">Indexer customization via [field mappings](search-indexer-field-mappings.md)</span></span>
* <span data-ttu-id="63f82-122">Prend en charge les ETags tooenable simultanées mise à jour sûre des index définitions, indexeurs et sources de données</span><span class="sxs-lookup"><span data-stu-id="63f82-122">ETags support tooenable safe concurrent updating of index definitions, indexers, and data sources</span></span>
* <span data-ttu-id="63f82-123">Prise en charge pour la création des définitions de champs d’index de façon déclarative à décoration de votre classe de modèle et à l’aide de nouveau hello `FieldBuilder` classe.</span><span class="sxs-lookup"><span data-stu-id="63f82-123">Support for building index field definitions declaratively by decorating your model class and using hello new `FieldBuilder` class.</span></span>
* <span data-ttu-id="63f82-124">Prise en charge de .NET Core et .NET Portable Profile 111</span><span class="sxs-lookup"><span data-stu-id="63f82-124">Support for .NET Core and .NET Portable Profile 111</span></span>

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a><span data-ttu-id="63f82-125">Étapes tooupgrade</span><span class="sxs-lookup"><span data-stu-id="63f82-125">Steps tooupgrade</span></span>
<span data-ttu-id="63f82-126">Tout d’abord, mettre à jour votre référence de NuGet pour `Microsoft.Azure.Search` soit hello Console du Gestionnaire de Package NuGet ou en cliquant sur vos références de projet et en sélectionnant « Gérer NuGet Packages... » dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="63f82-126">First, update your NuGet reference for `Microsoft.Azure.Search` using either hello NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="63f82-127">Une fois que NuGet a téléchargé les nouveaux packages de hello et leurs dépendances, régénérez votre projet.</span><span class="sxs-lookup"><span data-stu-id="63f82-127">Once NuGet has downloaded hello new packages and their dependencies, rebuild your project.</span></span> <span data-ttu-id="63f82-128">En fonction de la structure de votre code, la recompilation peut réussir.</span><span class="sxs-lookup"><span data-stu-id="63f82-128">Depending on how your code is structured, it may rebuild successfully.</span></span> <span data-ttu-id="63f82-129">Dans ce cas, vous êtes prêt toogo !</span><span class="sxs-lookup"><span data-stu-id="63f82-129">If so, you're ready toogo!</span></span>

<span data-ttu-id="63f82-130">Si votre build échoue, vous devez voir une erreur de build hello suivante :</span><span class="sxs-lookup"><span data-stu-id="63f82-130">If your build fails, you should see a build error like hello following:</span></span>

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' too'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

<span data-ttu-id="63f82-131">étape suivante de Hello est toofix cette erreur de build.</span><span class="sxs-lookup"><span data-stu-id="63f82-131">hello next step is toofix this build error.</span></span> <span data-ttu-id="63f82-132">Consultez [modifications avec rupture dans la version 3](#ListOfChanges) pour plus d’informations sur ce qui provoque l’erreur de hello et comment toofix il.</span><span class="sxs-lookup"><span data-stu-id="63f82-132">See [Breaking changes in version 3](#ListOfChanges) for details on what causes hello error and how toofix it.</span></span>

<span data-ttu-id="63f82-133">Vous pouvez voir la build supplémentaire avertissements liés tooobsolete méthodes ou propriétés.</span><span class="sxs-lookup"><span data-stu-id="63f82-133">You may see additional build warnings related tooobsolete methods or properties.</span></span> <span data-ttu-id="63f82-134">avertissements de Hello inclut des instructions sur le toouse à la place de hello fonctionnalité déconseillée.</span><span class="sxs-lookup"><span data-stu-id="63f82-134">hello warnings will include instructions on what toouse instead of hello deprecated feature.</span></span> <span data-ttu-id="63f82-135">Par exemple, si votre application utilise hello `IndexingParameters.Base64EncodeKeys` propriété, vous devez obtenir un avertissement indiquant que`"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span><span class="sxs-lookup"><span data-stu-id="63f82-135">For example, if your application uses hello `IndexingParameters.Base64EncodeKeys` property, you should get a warning that says `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span></span>

<span data-ttu-id="63f82-136">Une fois que vous avez résolu toutes les erreurs de build, vous pouvez apporter des modifications tooyour application tootake tirer parti de nouvelle fonctionnalité si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="63f82-136">Once you've fixed any build errors, you can make changes tooyour application tootake advantage of new functionality if you wish.</span></span> <span data-ttu-id="63f82-137">Nouvelles fonctionnalités dans le Kit de développement logiciel de hello sont détaillées dans [quelles sont les nouveautés dans la version 3](#WhatsNew).</span><span class="sxs-lookup"><span data-stu-id="63f82-137">New features in hello SDK are detailed in [What's new in version 3](#WhatsNew).</span></span>

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a><span data-ttu-id="63f82-138">Dernières modifications dans la version 3</span><span class="sxs-lookup"><span data-stu-id="63f82-138">Breaking changes in version 3</span></span>
<span data-ttu-id="63f82-139">Il un petit nombre de modifications avec rupture dans la version 3 qui peuvent nécessiter de code modifie en outre toorebuilding votre application.</span><span class="sxs-lookup"><span data-stu-id="63f82-139">There a small number of breaking changes in version 3 that may require code changes in addition toorebuilding your application.</span></span>

### <a name="indexesgetclient-return-type"></a><span data-ttu-id="63f82-140">Type de retour Indexes.GetClient</span><span class="sxs-lookup"><span data-stu-id="63f82-140">Indexes.GetClient return type</span></span>
<span data-ttu-id="63f82-141">Hello `Indexes.GetClient` méthode a un nouveau type de retour.</span><span class="sxs-lookup"><span data-stu-id="63f82-141">hello `Indexes.GetClient` method has a new return type.</span></span> <span data-ttu-id="63f82-142">Auparavant, elle retournait `SearchIndexClient`, mais il a été modifié trop`ISearchIndexClient` dans la version 2.0-preview et qui comporte des modification sur tooversion 3.</span><span class="sxs-lookup"><span data-stu-id="63f82-142">Previously, it returned `SearchIndexClient`, but this was changed too`ISearchIndexClient` in version 2.0-preview, and that change carries over tooversion 3.</span></span> <span data-ttu-id="63f82-143">Il s’agit de toosupport les clients qui souhaitent toomock hello `GetClient` méthode pour les tests unitaires en retournant une implémentation fictive du `ISearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="63f82-143">This is toosupport customers that wish toomock hello `GetClient` method for unit tests by returning a mock implementation of `ISearchIndexClient`.</span></span>

#### <a name="example"></a><span data-ttu-id="63f82-144">Exemple</span><span class="sxs-lookup"><span data-stu-id="63f82-144">Example</span></span>
<span data-ttu-id="63f82-145">Si votre code ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="63f82-145">If your code looks like this:</span></span>

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

<span data-ttu-id="63f82-146">Vous pouvez le modifier toothis toofix toutes les erreurs de build :</span><span class="sxs-lookup"><span data-stu-id="63f82-146">You can change it toothis toofix any build errors:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-toostrings"></a><span data-ttu-id="63f82-147">AnalyzerName, type de données et d’autres ne sont plus toostrings implicitement convertible</span><span class="sxs-lookup"><span data-stu-id="63f82-147">AnalyzerName, DataType, and others are no longer implicitly convertible toostrings</span></span>
<span data-ttu-id="63f82-148">Bonjour Azure Search .NET SDK qui dérivent de nombreux types `ExtensibleEnum`.</span><span class="sxs-lookup"><span data-stu-id="63f82-148">There are many types in hello Azure Search .NET SDK that derive from `ExtensibleEnum`.</span></span> <span data-ttu-id="63f82-149">Auparavant ces types étaient toutes implicitement convertible tootype `string`.</span><span class="sxs-lookup"><span data-stu-id="63f82-149">Previously these types were all implicitly convertible tootype `string`.</span></span> <span data-ttu-id="63f82-150">Toutefois, un bogue a été détecté dans hello `Object.Equals` implémentation de ces classes et de correction bogue hello requis la désactivation de cette conversion implicite.</span><span class="sxs-lookup"><span data-stu-id="63f82-150">However, a bug was discovered in hello `Object.Equals` implementation for these classes, and fixing hello bug required disabling this implicit conversion.</span></span> <span data-ttu-id="63f82-151">Conversion explicite trop`string` est toujours autorisé.</span><span class="sxs-lookup"><span data-stu-id="63f82-151">Explicit conversion too`string` is still allowed.</span></span>

#### <a name="example"></a><span data-ttu-id="63f82-152">Exemple</span><span class="sxs-lookup"><span data-stu-id="63f82-152">Example</span></span>
<span data-ttu-id="63f82-153">Si votre code ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="63f82-153">If your code looks like this:</span></span>

```csharp
var customTokenizerName = TokenizerName.Create("my_tokenizer"); 
var customTokenFilterName = TokenFilterName.Create("my_tokenfilter"); 
var customCharFilterName = CharFilterName.Create("my_charfilter"); 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        customTokenizerName,  
        new[] { customTokenFilterName },  
        new[] { customCharFilterName }), 
}; 
```

<span data-ttu-id="63f82-154">Vous pouvez le modifier toothis toofix toutes les erreurs de build :</span><span class="sxs-lookup"><span data-stu-id="63f82-154">You can change it toothis toofix any build errors:</span></span>

```csharp
const string CustomTokenizerName = "my_tokenizer"; 
const string CustomTokenFilterName = "my_tokenfilter"; 
const string CustomCharFilterName = "my_charfilter"; 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        CustomTokenizerName,  
        new TokenFilterName[] { CustomTokenFilterName },  
        new CharFilterName[] { CustomCharFilterName })
}; 
```

### <a name="removed-obsolete-members"></a><span data-ttu-id="63f82-155">Membres obsolètes supprimés</span><span class="sxs-lookup"><span data-stu-id="63f82-155">Removed obsolete members</span></span>

<span data-ttu-id="63f82-156">Vous pouvez voir toomethods connexes des erreurs de build ou les propriétés qui ont été marquées comme obsolètes dans la version 2.0-version préliminaire et supprimées par la suite dans la version 3.</span><span class="sxs-lookup"><span data-stu-id="63f82-156">You may see build errors related toomethods or properties that were marked as obsolete in version 2.0-preview and subsequently removed in version 3.</span></span> <span data-ttu-id="63f82-157">Si vous rencontrez ces erreurs, voici comment tooresolve les :</span><span class="sxs-lookup"><span data-stu-id="63f82-157">If you encounter such errors, here is how tooresolve them:</span></span>

- <span data-ttu-id="63f82-158">Si vous utilisiez ce constructeur : `ScoringParameter(string name, string value)`, remplacez-le par `ScoringParameter(string name, IEnumerable<string> values)`</span><span class="sxs-lookup"><span data-stu-id="63f82-158">If you were using this constructor: `ScoringParameter(string name, string value)`, use this one instead: `ScoringParameter(string name, IEnumerable<string> values)`</span></span>
- <span data-ttu-id="63f82-159">Si vous utilisiez hello `ScoringParameter.Value` propriété, utilisez hello `ScoringParameter.Values` propriété ou hello `ToString` méthode à la place.</span><span class="sxs-lookup"><span data-stu-id="63f82-159">If you were using hello `ScoringParameter.Value` property, use hello `ScoringParameter.Values` property or hello `ToString` method instead.</span></span>
- <span data-ttu-id="63f82-160">Si vous utilisiez hello `SearchRequestOptions.RequestId` propriété, utilisez hello `ClientRequestId` propriété à la place.</span><span class="sxs-lookup"><span data-stu-id="63f82-160">If you were using hello `SearchRequestOptions.RequestId` property, use hello `ClientRequestId` property instead.</span></span>

### <a name="removed-preview-features"></a><span data-ttu-id="63f82-161">Fonctionnalités préliminaires supprimées</span><span class="sxs-lookup"><span data-stu-id="63f82-161">Removed preview features</span></span>

<span data-ttu-id="63f82-162">Si vous mettez à niveau à partir de la version 2.0-preview tooversion 3, n’oubliez pas que JSON et CSV de l’analyse de la prise en charge pour les indexeurs d’objet Blob a été supprimé, car ces fonctionnalités sont encore en version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="63f82-162">If you are upgrading from version 2.0-preview tooversion 3, be aware that JSON and CSV parsing support for Blob Indexers has been removed since these features are still in preview.</span></span> <span data-ttu-id="63f82-163">Plus précisément, hello suivant les méthodes de hello `IndexingParametersExtensions` classe ont été supprimées :</span><span class="sxs-lookup"><span data-stu-id="63f82-163">Specifically, hello following methods of hello `IndexingParametersExtensions` class have been removed:</span></span>

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

<span data-ttu-id="63f82-164">Si votre application a une dépendance dure sur ces fonctionnalités, vous ne serez pas en mesure de tooupgrade tooversion 3 Hello Azure Search .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="63f82-164">If your application has a hard dependency on these features, you will not be able tooupgrade tooversion 3 of hello Azure Search .NET SDK.</span></span> <span data-ttu-id="63f82-165">Vous pouvez continuer d’aperçu toouse version 2.0.</span><span class="sxs-lookup"><span data-stu-id="63f82-165">You can continue toouse version 2.0-preview.</span></span> <span data-ttu-id="63f82-166">Mais n’oubliez pas que **nous déconseillons l’utilisation de Kits de développement logiciel en version préliminaire dans les applications de production**.</span><span class="sxs-lookup"><span data-stu-id="63f82-166">However, please keep in mind that **we do not recommend using preview SDKs in production applications**.</span></span> <span data-ttu-id="63f82-167">Les fonctionnalités préliminaires servent uniquement à des fins d’évaluation et peuvent changer.</span><span class="sxs-lookup"><span data-stu-id="63f82-167">Preview features are for evaluation only and may change.</span></span>

## <a name="conclusion"></a><span data-ttu-id="63f82-168">Conclusion</span><span class="sxs-lookup"><span data-stu-id="63f82-168">Conclusion</span></span>
<span data-ttu-id="63f82-169">Si vous avez besoin de plus de détails sur l’utilisation de hello Azure Search .NET SDK, consultez notre récemment mis à jour [procédures](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="63f82-169">If you need more details on using hello Azure Search .NET SDK, see our recently updated [How-to](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="63f82-170">Nous apprécions vos commentaires sur le Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="63f82-170">We welcome your feedback on hello SDK.</span></span> <span data-ttu-id="63f82-171">Si vous rencontrez des problèmes, vous pouvez tooask libre nous de l’aide sur hello [forum MSDN de recherche Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span><span class="sxs-lookup"><span data-stu-id="63f82-171">If you encounter problems, feel free tooask us for help on hello [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span></span> <span data-ttu-id="63f82-172">Si vous trouvez un bogue, vous pouvez signaler un problème Bonjour [référentiel GitHub de kit de développement logiciel Azure .NET](https://github.com/Azure/azure-sdk-for-net/issues).</span><span class="sxs-lookup"><span data-stu-id="63f82-172">If you find a bug, you can file an issue in hello [Azure .NET SDK GitHub repository](https://github.com/Azure/azure-sdk-for-net/issues).</span></span> <span data-ttu-id="63f82-173">Assurez-vous que tooprefix le titre de votre problème avec « Search SDK : ».</span><span class="sxs-lookup"><span data-stu-id="63f82-173">Make sure tooprefix your issue title with "Search SDK: ".</span></span>

<span data-ttu-id="63f82-174">Merci d’utiliser Azure Search !</span><span class="sxs-lookup"><span data-stu-id="63f82-174">Thank you for using Azure Search!</span></span>

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-tooupgrade-tooversion-11"></a><span data-ttu-id="63f82-175">Annexe : Étapes tooupgrade tooversion 1.1</span><span class="sxs-lookup"><span data-stu-id="63f82-175">Appendix: Steps tooupgrade tooversion 1.1</span></span>
> [!NOTE]
> <span data-ttu-id="63f82-176">Cette section s’applique uniquement les toousers de hello Azure Search .NET SDK version 1.0.2-preview et antérieures.</span><span class="sxs-lookup"><span data-stu-id="63f82-176">This section applies only toousers of hello Azure Search .NET SDK version 1.0.2-preview and older.</span></span>
> 
> 

<span data-ttu-id="63f82-177">Tout d’abord, mettre à jour votre référence de NuGet pour `Microsoft.Azure.Search` soit hello Console du Gestionnaire de Package NuGet ou en cliquant sur vos références de projet et en sélectionnant « Gérer NuGet Packages... » dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="63f82-177">First, update your NuGet reference for `Microsoft.Azure.Search` using either hello NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="63f82-178">Une fois que NuGet a téléchargé les nouveaux packages de hello et leurs dépendances, régénérez votre projet.</span><span class="sxs-lookup"><span data-stu-id="63f82-178">Once NuGet has downloaded hello new packages and their dependencies, rebuild your project.</span></span>

<span data-ttu-id="63f82-179">Si vous étiez précédemment à l’aide de la version 1.0.0-preview, 1.0.1-preview ou 1.0.2-preview, génération de hello doit réussir et vous êtes prêt toogo !</span><span class="sxs-lookup"><span data-stu-id="63f82-179">If you were previously using version 1.0.0-preview, 1.0.1-preview, or 1.0.2-preview, hello build should succeed and you're ready toogo!</span></span>

<span data-ttu-id="63f82-180">Si vous utilisiez auparavant version 0.13.0-preview ou antérieure, vous devez voir erreurs hello suivante de build :</span><span class="sxs-lookup"><span data-stu-id="63f82-180">If you were previously using version 0.13.0-preview or older, you should see build errors like hello following:</span></span>

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: hello type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

<span data-ttu-id="63f82-181">étape suivante de Hello est erreurs de build hello toofix un par un.</span><span class="sxs-lookup"><span data-stu-id="63f82-181">hello next step is toofix hello build errors one by one.</span></span> <span data-ttu-id="63f82-182">La majorité nécessite la modification de certains noms de classes et des méthodes qui ont été renommés dans hello SDK.</span><span class="sxs-lookup"><span data-stu-id="63f82-182">Most will require changing some class and method names that have been renamed in hello SDK.</span></span> <span data-ttu-id="63f82-183">[Liste des dernières modifications dans la version 1.1](#ListOfChangesV1) répertorie ces changements de nom.</span><span class="sxs-lookup"><span data-stu-id="63f82-183">[List of breaking changes in version 1.1](#ListOfChangesV1) contains a list of these name changes.</span></span>

<span data-ttu-id="63f82-184">Si vous utilisez des classes personnalisées toomodel vos documents, et ces classes ont des propriétés de types primitifs non nullable (par exemple, `int` ou `bool` en c#), il existe un bogue dans la version 1.1 de hello du SDK hello dont vous devez être conscient.</span><span class="sxs-lookup"><span data-stu-id="63f82-184">If you're using custom classes toomodel your documents, and those classes have properties of non-nullable primitive types (for example, `int` or `bool` in C#), there is a bug fix in hello 1.1 version of hello SDK of which you should be aware.</span></span> <span data-ttu-id="63f82-185">Consultez [Résolution des bogues dans la version 1.1](#BugFixesV1) pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="63f82-185">See [Bug fixes in version 1.1](#BugFixesV1) for more details.</span></span>

<span data-ttu-id="63f82-186">Enfin, une fois que vous avez résolu toutes les erreurs de build, vous pouvez apporter des modifications parti de tootake tooyour application des nouvelles fonctionnalités si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="63f82-186">Finally, once you've fixed any build errors, you can make changes tooyour application tootake advantage of new functionality if you wish.</span></span>

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a><span data-ttu-id="63f82-187">Liste des dernières modifications dans la version 1.1</span><span class="sxs-lookup"><span data-stu-id="63f82-187">List of breaking changes in version 1.1</span></span>
<span data-ttu-id="63f82-188">Hello liste suivante est classée par probabilité de hello que hello modification affecte votre code d’application.</span><span class="sxs-lookup"><span data-stu-id="63f82-188">hello following list is ordered by hello likelihood that hello change will affect your application code.</span></span>

#### <a name="indexbatch-and-indexaction-changes"></a><span data-ttu-id="63f82-189">Modifications IndexBatch et IndexAction</span><span class="sxs-lookup"><span data-stu-id="63f82-189">IndexBatch and IndexAction changes</span></span>
<span data-ttu-id="63f82-190">`IndexBatch.Create`a été renommé trop`IndexBatch.New` et n’a plus un `params` argument.</span><span class="sxs-lookup"><span data-stu-id="63f82-190">`IndexBatch.Create` has been renamed too`IndexBatch.New` and no longer has a `params` argument.</span></span> <span data-ttu-id="63f82-191">Vous pouvez utiliser `IndexBatch.New` pour les lots qui combinent différents types d’actions (fusions, suppressions, etc.).</span><span class="sxs-lookup"><span data-stu-id="63f82-191">You can use `IndexBatch.New` for batches that mix different types of actions (merges, deletes, etc.).</span></span> <span data-ttu-id="63f82-192">En outre, des nouvelles méthodes statiques pour la création de lots où toutes les actions de hello sont même hello : `Delete`, `Merge`, `MergeOrUpload`, et `Upload`.</span><span class="sxs-lookup"><span data-stu-id="63f82-192">In addition, there are new static methods for creating batches where all hello actions are hello same: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span>

<span data-ttu-id="63f82-193">`IndexAction` ne contient plus de constructeurs publics et ses propriétés sont immuables.</span><span class="sxs-lookup"><span data-stu-id="63f82-193">`IndexAction` no longer has public constructors and its properties are now immutable.</span></span> <span data-ttu-id="63f82-194">Vous devez utiliser les méthodes statiques nouvelle hello pour la création d’actions à des fins différentes : `Delete`, `Merge`, `MergeOrUpload`, et `Upload`.</span><span class="sxs-lookup"><span data-stu-id="63f82-194">You should use hello new static methods for creating actions for different purposes: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span> <span data-ttu-id="63f82-195">`IndexAction.Create` a été supprimé.</span><span class="sxs-lookup"><span data-stu-id="63f82-195">`IndexAction.Create` has been removed.</span></span> <span data-ttu-id="63f82-196">Si vous avez utilisé la surcharge qui accepte uniquement un document hello, assurez-vous que toouse `Upload` à la place.</span><span class="sxs-lookup"><span data-stu-id="63f82-196">If you used hello overload that takes only a document, make sure toouse `Upload` instead.</span></span>

##### <a name="example"></a><span data-ttu-id="63f82-197">Exemple</span><span class="sxs-lookup"><span data-stu-id="63f82-197">Example</span></span>
<span data-ttu-id="63f82-198">Si votre code ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="63f82-198">If your code looks like this:</span></span>

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="63f82-199">Vous pouvez le modifier toothis toofix toutes les erreurs de build :</span><span class="sxs-lookup"><span data-stu-id="63f82-199">You can change it toothis toofix any build errors:</span></span>

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="63f82-200">Si vous le souhaitez, vous pouvez encore simplifier il toothis :</span><span class="sxs-lookup"><span data-stu-id="63f82-200">If you want, you can further simplify it toothis:</span></span>

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a><span data-ttu-id="63f82-201">Modifications IndexBatchException</span><span class="sxs-lookup"><span data-stu-id="63f82-201">IndexBatchException changes</span></span>
<span data-ttu-id="63f82-202">Hello `IndexBatchException.IndexResponse` propriété a été renommée trop`IndexingResults`, et son type est désormais `IList<IndexingResult>`.</span><span class="sxs-lookup"><span data-stu-id="63f82-202">hello `IndexBatchException.IndexResponse` property has been renamed too`IndexingResults`, and its type is now `IList<IndexingResult>`.</span></span>

##### <a name="example"></a><span data-ttu-id="63f82-203">Exemple</span><span class="sxs-lookup"><span data-stu-id="63f82-203">Example</span></span>
<span data-ttu-id="63f82-204">Si votre code ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="63f82-204">If your code looks like this:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<span data-ttu-id="63f82-205">Vous pouvez le modifier toothis toofix toutes les erreurs de build :</span><span class="sxs-lookup"><span data-stu-id="63f82-205">You can change it toothis toofix any build errors:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a><span data-ttu-id="63f82-206">Modifications des méthodes d’opération</span><span class="sxs-lookup"><span data-stu-id="63f82-206">Operation method changes</span></span>
<span data-ttu-id="63f82-207">Chaque opération Bonjour Azure Search .NET SDK est exposée comme un ensemble de surcharges de méthode pour les appelants synchrones et asynchrones.</span><span class="sxs-lookup"><span data-stu-id="63f82-207">Each operation in hello Azure Search .NET SDK is exposed as a set of method overloads for synchronous and asynchronous callers.</span></span> <span data-ttu-id="63f82-208">Hello factorisation de ces surcharges de méthode et les signatures a changé dans la version 1.1.</span><span class="sxs-lookup"><span data-stu-id="63f82-208">hello signatures and factoring of these method overloads has changed in version 1.1.</span></span>

<span data-ttu-id="63f82-209">Par exemple, hello opération « Obtenir des statistiques d’Index » dans les versions antérieures du Kit de développement logiciel de hello exposées ces signatures :</span><span class="sxs-lookup"><span data-stu-id="63f82-209">For example, hello "Get Index Statistics" operation in older versions of hello SDK exposed these signatures:</span></span>

<span data-ttu-id="63f82-210">Dans `IIndexOperations`:</span><span class="sxs-lookup"><span data-stu-id="63f82-210">In `IIndexOperations`:</span></span>

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

<span data-ttu-id="63f82-211">Dans `IndexOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="63f82-211">In `IndexOperationsExtensions`:</span></span>

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

<span data-ttu-id="63f82-212">les signatures de méthode Hello pour hello même opération dans la version 1.1 présentent cet aspect :</span><span class="sxs-lookup"><span data-stu-id="63f82-212">hello method signatures for hello same operation in version 1.1 look like this:</span></span>

<span data-ttu-id="63f82-213">Dans `IIndexesOperations`:</span><span class="sxs-lookup"><span data-stu-id="63f82-213">In `IIndexesOperations`:</span></span>

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

<span data-ttu-id="63f82-214">Dans `IndexesOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="63f82-214">In `IndexesOperationsExtensions`:</span></span>

    // Simplified asynchronous operation
    public static Task<IndexGetStatisticsResult> GetStatisticsAsync(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        CancellationToken cancellationToken = default(CancellationToken));

    // Simplified synchronous operation
    public static IndexGetStatisticsResult GetStatistics(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions));

<span data-ttu-id="63f82-215">Depuis la version 1.1, hello Azure Search .NET SDK organise les méthodes d’opération différemment :</span><span class="sxs-lookup"><span data-stu-id="63f82-215">Starting with version 1.1, hello Azure Search .NET SDK organizes operation methods differently:</span></span>

* <span data-ttu-id="63f82-216">Les paramètres facultatifs sont désormais modélisés en tant que paramètres par défaut plutôt que les surcharges de méthode supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="63f82-216">Optional parameters are now modeled as default parameters rather than additional method overloads.</span></span> <span data-ttu-id="63f82-217">Cela réduit nombre hello des surcharges de méthode, parfois considérablement.</span><span class="sxs-lookup"><span data-stu-id="63f82-217">This reduces hello number of method overloads, sometimes dramatically.</span></span>
* <span data-ttu-id="63f82-218">méthodes d’extension Hello masquent maintenant un grand nombre de hello superflus des détails HTTP à partir de l’appelant de hello.</span><span class="sxs-lookup"><span data-stu-id="63f82-218">hello extension methods now hide a lot of hello extraneous details of HTTP from hello caller.</span></span> <span data-ttu-id="63f82-219">Par exemple, les versions antérieures du Kit de développement logiciel a retourné un objet de réponse avec un code d’état HTTP que vous pouvez souvent de hello n’a pas besoin des toocheck lever des méthodes d’opération `CloudException` sur n’importe quel code d’état qui indique une erreur.</span><span class="sxs-lookup"><span data-stu-id="63f82-219">For example, older versions of hello SDK returned a response object with an HTTP status code, which you often didn't need toocheck because operation methods throw `CloudException` for any status code that indicates an error.</span></span> <span data-ttu-id="63f82-220">Bonjour des nouveaux objets de modèle de retourner simplement de méthodes d’extension, l’enregistrement vous hello des problèmes d’avoir toounwrap dans votre code.</span><span class="sxs-lookup"><span data-stu-id="63f82-220">hello new extension methods just return model objects, saving you hello trouble of having toounwrap them in your code.</span></span>
* <span data-ttu-id="63f82-221">À l’inverse, hello interfaces principales maintenant exposent des méthodes qui vous permettent de mieux contrôler au niveau de hello HTTP si vous en avez besoin.</span><span class="sxs-lookup"><span data-stu-id="63f82-221">Conversely, hello core interfaces now expose methods that give you more control at hello HTTP level if you need it.</span></span> <span data-ttu-id="63f82-222">Vous pouvez à présent passer dans personnalisé toobe d’en-têtes HTTP inclus dans les demandes et hello nouvelle `AzureOperationResponse<T>` retourner le type vous donne un accès direct toohello `HttpRequestMessage` et `HttpResponseMessage` pour l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="63f82-222">You can now pass in custom HTTP headers toobe included in requests, and hello new `AzureOperationResponse<T>` return type gives you direct access toohello `HttpRequestMessage` and `HttpResponseMessage` for hello operation.</span></span> <span data-ttu-id="63f82-223">`AzureOperationResponse`est défini dans hello `Microsoft.Rest.Azure` espace de noms et les remplace `Hyak.Common.OperationResponse`.</span><span class="sxs-lookup"><span data-stu-id="63f82-223">`AzureOperationResponse` is defined in hello `Microsoft.Rest.Azure` namespace and replaces `Hyak.Common.OperationResponse`.</span></span>

#### <a name="scoringparameters-changes"></a><span data-ttu-id="63f82-224">Modifications ScoringParameters</span><span class="sxs-lookup"><span data-stu-id="63f82-224">ScoringParameters changes</span></span>
<span data-ttu-id="63f82-225">Une nouvelle classe nommée `ScoringParameter` a été ajoutée dans hello dernier Kit de développement logiciel toomake plus faciles profils tooscoring de paramètres tooprovide dans une requête de recherche.</span><span class="sxs-lookup"><span data-stu-id="63f82-225">A new class named `ScoringParameter` has been added in hello latest SDK toomake it easier tooprovide parameters tooscoring profiles in a search query.</span></span> <span data-ttu-id="63f82-226">Hello précédemment `ScoringProfiles` propriété Hello `SearchParameters` entré en tant que classe `IList<string>`; Maintenant qu’il est de type `IList<ScoringParameter>`.</span><span class="sxs-lookup"><span data-stu-id="63f82-226">Previously hello `ScoringProfiles` property of hello `SearchParameters` class was typed as `IList<string>`; Now it is typed as `IList<ScoringParameter>`.</span></span>

##### <a name="example"></a><span data-ttu-id="63f82-227">Exemple</span><span class="sxs-lookup"><span data-stu-id="63f82-227">Example</span></span>
<span data-ttu-id="63f82-228">Si votre code ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="63f82-228">If your code looks like this:</span></span>

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

<span data-ttu-id="63f82-229">Vous pouvez le modifier toothis toofix toutes les erreurs de build :</span><span class="sxs-lookup"><span data-stu-id="63f82-229">You can change it toothis toofix any build errors:</span></span> 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a><span data-ttu-id="63f82-230">Modifications de modèles de classe</span><span class="sxs-lookup"><span data-stu-id="63f82-230">Model class changes</span></span>
<span data-ttu-id="63f82-231">En raison de modifications de signature toohello décrites dans [changement de méthode d’opération](#OperationMethodChanges), de nombreuses classes Bonjour `Microsoft.Azure.Search.Models` espace de noms ont été renommés ou supprimés.</span><span class="sxs-lookup"><span data-stu-id="63f82-231">Due toohello signature changes described in [Operation method changes](#OperationMethodChanges), many classes in hello `Microsoft.Azure.Search.Models` namespace have been renamed or removed.</span></span> <span data-ttu-id="63f82-232">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="63f82-232">For example:</span></span>

* <span data-ttu-id="63f82-233">`IndexDefinitionResponse` a été remplacé par `AzureOperationResponse<Index>`</span><span class="sxs-lookup"><span data-stu-id="63f82-233">`IndexDefinitionResponse` has been replaced by `AzureOperationResponse<Index>`</span></span>
* <span data-ttu-id="63f82-234">`DocumentSearchResponse`a été renommé en trop`DocumentSearchResult`</span><span class="sxs-lookup"><span data-stu-id="63f82-234">`DocumentSearchResponse` has been renamed too`DocumentSearchResult`</span></span>
* <span data-ttu-id="63f82-235">`IndexResult`a été renommé en trop`IndexingResult`</span><span class="sxs-lookup"><span data-stu-id="63f82-235">`IndexResult` has been renamed too`IndexingResult`</span></span>
* <span data-ttu-id="63f82-236">`Documents.Count()`Retourne un `long` avec le nombre de documents hello au lieu d’un`DocumentCountResponse`</span><span class="sxs-lookup"><span data-stu-id="63f82-236">`Documents.Count()` now returns a `long` with hello document count instead of a `DocumentCountResponse`</span></span>
* <span data-ttu-id="63f82-237">`IndexGetStatisticsResponse`a été renommé en trop`IndexGetStatisticsResult`</span><span class="sxs-lookup"><span data-stu-id="63f82-237">`IndexGetStatisticsResponse` has been renamed too`IndexGetStatisticsResult`</span></span>
* <span data-ttu-id="63f82-238">`IndexListResponse`a été renommé en trop`IndexListResult`</span><span class="sxs-lookup"><span data-stu-id="63f82-238">`IndexListResponse` has been renamed too`IndexListResult`</span></span>

<span data-ttu-id="63f82-239">toosummarize, `OperationResponse`-classes dérivées qui existaient uniquement les toowrap un objet de modèle ont été supprimés.</span><span class="sxs-lookup"><span data-stu-id="63f82-239">toosummarize, `OperationResponse`-derived classes that existed only toowrap a model object have been removed.</span></span> <span data-ttu-id="63f82-240">Hello autres classes ont eu leur suffixe a été remplacée par `Response` trop`Result`.</span><span class="sxs-lookup"><span data-stu-id="63f82-240">hello remaining classes have had their suffix changed from `Response` too`Result`.</span></span>

##### <a name="example"></a><span data-ttu-id="63f82-241">Exemple</span><span class="sxs-lookup"><span data-stu-id="63f82-241">Example</span></span>
<span data-ttu-id="63f82-242">Si votre code ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="63f82-242">If your code looks like this:</span></span>

    IndexerGetStatusResponse statusResponse = null;

    try
    {
        statusResponse = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = statusResponse.ExecutionInfo.LastResult;

<span data-ttu-id="63f82-243">Vous pouvez le modifier toothis toofix toutes les erreurs de build :</span><span class="sxs-lookup"><span data-stu-id="63f82-243">You can change it toothis toofix any build errors:</span></span>

    IndexerExecutionInfo status = null;

    try
    {
        status = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = status.LastResult;

##### <a name="response-classes-and-ienumerable"></a><span data-ttu-id="63f82-244">Les classes de réponse et IEnumerable</span><span class="sxs-lookup"><span data-stu-id="63f82-244">Response classes and IEnumerable</span></span>
<span data-ttu-id="63f82-245">Une modification supplémentaire pouvant affecter votre code est que les classes de réponse contenant des collections ne sont plus mises en œuvre `IEnumerable<T>`.</span><span class="sxs-lookup"><span data-stu-id="63f82-245">An additional change that may affect your code is that response classes that hold collections no longer implement `IEnumerable<T>`.</span></span> <span data-ttu-id="63f82-246">Au lieu de cela, vous pouvez accéder à propriété de collection hello directement.</span><span class="sxs-lookup"><span data-stu-id="63f82-246">Instead, you can access hello collection property directly.</span></span> <span data-ttu-id="63f82-247">Par exemple, si votre code ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="63f82-247">For example, if your code looks like this:</span></span>

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

<span data-ttu-id="63f82-248">Vous pouvez le modifier toothis toofix toutes les erreurs de build :</span><span class="sxs-lookup"><span data-stu-id="63f82-248">You can change it toothis toofix any build errors:</span></span>

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a><span data-ttu-id="63f82-249">Cas particulier pour les applications web</span><span class="sxs-lookup"><span data-stu-id="63f82-249">Special case for web applications</span></span>
<span data-ttu-id="63f82-250">Si vous avez une application web qui sérialise `DocumentSearchResponse` directement les résultats de recherche de toosend toohello navigateur, vous devez toochange votre code ou les résultats hello ne sérialisent pas correctement.</span><span class="sxs-lookup"><span data-stu-id="63f82-250">If you have a web application that serializes `DocumentSearchResponse` directly toosend search results toohello browser, you will need toochange your code or hello results will not serialize correctly.</span></span> <span data-ttu-id="63f82-251">Par exemple, si votre code ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="63f82-251">For example, if your code looks like this:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

<span data-ttu-id="63f82-252">Vous pouvez le modifier en obtenant hello `.Results` propriété du rendu de résultat hello recherche réponse toofix recherche :</span><span class="sxs-lookup"><span data-stu-id="63f82-252">You can change it by getting hello `.Results` property of hello search response toofix search result rendering:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

<span data-ttu-id="63f82-253">Vous aurez toolook pour ces cas dans votre code **hello compilateur pas vous avertit** car `JsonResult.Data` est de type `object`.</span><span class="sxs-lookup"><span data-stu-id="63f82-253">You will have toolook for such cases in your code yourself; **hello compiler will not warn you** because `JsonResult.Data` is of type `object`.</span></span>

#### <a name="cloudexception-changes"></a><span data-ttu-id="63f82-254">Modifications CloudException</span><span class="sxs-lookup"><span data-stu-id="63f82-254">CloudException changes</span></span>
<span data-ttu-id="63f82-255">Hello `CloudException` classe a été déplacé de hello `Hyak.Common` toohello de l’espace de noms `Microsoft.Rest.Azure` espace de noms.</span><span class="sxs-lookup"><span data-stu-id="63f82-255">hello `CloudException` class has moved from hello `Hyak.Common` namespace toohello `Microsoft.Rest.Azure` namespace.</span></span> <span data-ttu-id="63f82-256">En outre, sa `Error` propriété a été renommée trop`Body`.</span><span class="sxs-lookup"><span data-stu-id="63f82-256">Also, its `Error` property has been renamed too`Body`.</span></span>

#### <a name="searchserviceclient-and-searchindexclient-changes"></a><span data-ttu-id="63f82-257">Modifications de SearchServiceClient et SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="63f82-257">SearchServiceClient and SearchIndexClient changes</span></span>
<span data-ttu-id="63f82-258">Hello de type Hello `Credentials` propriété a été modifiée à partir de `SearchCredentials` tooits classe de base, `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="63f82-258">hello type of hello `Credentials` property has changed from `SearchCredentials` tooits base class, `ServiceClientCredentials`.</span></span> <span data-ttu-id="63f82-259">Si vous avez besoin de tooaccess hello `SearchCredentials` d’un `SearchIndexClient` ou `SearchServiceClient`, utilisez hello nouveau `SearchCredentials` propriété.</span><span class="sxs-lookup"><span data-stu-id="63f82-259">If you need tooaccess hello `SearchCredentials` of a `SearchIndexClient` or `SearchServiceClient`, please use hello new `SearchCredentials` property.</span></span>

<span data-ttu-id="63f82-260">Dans les versions antérieures de hello SDK, `SearchServiceClient` et `SearchIndexClient` a des constructeurs qui ont eu une `HttpClient` paramètre.</span><span class="sxs-lookup"><span data-stu-id="63f82-260">In older versions of hello SDK, `SearchServiceClient` and `SearchIndexClient` had constructors that took an `HttpClient` parameter.</span></span> <span data-ttu-id="63f82-261">Ils ont été remplacés par des constructeurs qui incluent un élément `HttpClientHandler` et un tableau d’objets `DelegatingHandler`.</span><span class="sxs-lookup"><span data-stu-id="63f82-261">These have been replaced with constructors that take an `HttpClientHandler` and an array of `DelegatingHandler` objects.</span></span> <span data-ttu-id="63f82-262">Il est ainsi plus faciles tooinstall gestionnaires personnalisés toopre-traitent les requêtes HTTP si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="63f82-262">This makes it easier tooinstall custom handlers toopre-process HTTP requests if necessary.</span></span>

<span data-ttu-id="63f82-263">Enfin, hello constructeurs qui ont eu une `Uri` et `SearchCredentials` ont été modifiés.</span><span class="sxs-lookup"><span data-stu-id="63f82-263">Finally, hello constructors that took a `Uri` and `SearchCredentials` have changed.</span></span> <span data-ttu-id="63f82-264">Par exemple, si vous avez un code qui ressemble à c qui suit :</span><span class="sxs-lookup"><span data-stu-id="63f82-264">For example, if you have code that looks like this:</span></span>

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

<span data-ttu-id="63f82-265">Vous pouvez le modifier toothis toofix toutes les erreurs de build :</span><span class="sxs-lookup"><span data-stu-id="63f82-265">You can change it toothis toofix any build errors:</span></span>

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

<span data-ttu-id="63f82-266">Également Remarque informations d’identification de type hello Hello paramètre a changé trop`ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="63f82-266">Also note that hello type of hello credentials parameter has changed too`ServiceClientCredentials`.</span></span> <span data-ttu-id="63f82-267">Il s’agit de tooaffect peu probable que votre code depuis `SearchCredentials` est dérivée de `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="63f82-267">This is unlikely tooaffect your code since `SearchCredentials` is derived from `ServiceClientCredentials`.</span></span>

#### <a name="passing-a-request-id"></a><span data-ttu-id="63f82-268">Transfert d’un ID de requête</span><span class="sxs-lookup"><span data-stu-id="63f82-268">Passing a request ID</span></span>
<span data-ttu-id="63f82-269">Dans les versions antérieures de hello SDK, vous pouvez définir un ID de demande sur hello `SearchServiceClient` ou `SearchIndexClient` et il est inclus dans chaque toohello demande API REST.</span><span class="sxs-lookup"><span data-stu-id="63f82-269">In older versions of hello SDK, you could set a request ID on hello `SearchServiceClient` or `SearchIndexClient` and it would be included in every request toohello REST API.</span></span> <span data-ttu-id="63f82-270">Cela est utile pour résoudre les problèmes avec votre service de recherche si vous avez besoin de toocontact.</span><span class="sxs-lookup"><span data-stu-id="63f82-270">This is useful for troubleshooting issues with your search service if you need toocontact support.</span></span> <span data-ttu-id="63f82-271">Toutefois, il est plus utile tooset un ID de demande unique pour chaque opération plutôt que toouse hello ID même pour toutes les opérations.</span><span class="sxs-lookup"><span data-stu-id="63f82-271">However, it is more useful tooset a unique request ID for every operation rather than toouse hello same ID for all operations.</span></span> <span data-ttu-id="63f82-272">Pour cette raison, hello `SetClientRequestId` méthodes de `SearchServiceClient` et `SearchIndexClient` ont été supprimés.</span><span class="sxs-lookup"><span data-stu-id="63f82-272">For this reason, hello `SetClientRequestId` methods of `SearchServiceClient` and `SearchIndexClient` have been removed.</span></span> <span data-ttu-id="63f82-273">Au lieu de cela, vous pouvez passer une méthode d’opération de demande ID tooeach via hello facultatif `SearchRequestOptions` paramètre.</span><span class="sxs-lookup"><span data-stu-id="63f82-273">Instead, you can pass a request ID tooeach operation method via hello optional `SearchRequestOptions` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="63f82-274">Dans une prochaine version du Kit de développement logiciel de hello, nous allons ajouter un nouveau mécanisme permettant de définir globalement un ID de demande sur le client de hello objets qui est cohérent avec l’approche hello utilisé par d’autres kits de développement logiciel Azure.</span><span class="sxs-lookup"><span data-stu-id="63f82-274">In a future release of hello SDK, we will add a new mechanism for setting a request ID globally on hello client objects that is consistent with hello approach used by other Azure SDKs.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="63f82-275">Exemple</span><span class="sxs-lookup"><span data-stu-id="63f82-275">Example</span></span>
<span data-ttu-id="63f82-276">Si vous avez un code qui ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="63f82-276">If you have code that looks like this:</span></span>

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

<span data-ttu-id="63f82-277">Vous pouvez le modifier toothis toofix toutes les erreurs de build :</span><span class="sxs-lookup"><span data-stu-id="63f82-277">You can change it toothis toofix any build errors:</span></span>

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a><span data-ttu-id="63f82-278">Modifications de nom d’interface</span><span class="sxs-lookup"><span data-stu-id="63f82-278">Interface name changes</span></span>
<span data-ttu-id="63f82-279">noms d’interface Hello opération groupe ont toutes les toobe modifiées cohérentes avec les noms de propriété correspondants :</span><span class="sxs-lookup"><span data-stu-id="63f82-279">hello operation group interface names have all changed toobe consistent with their corresponding property names:</span></span>

* <span data-ttu-id="63f82-280">Hello du type de `ISearchServiceClient.Indexes` a été renommé à partir de `IIndexOperations` trop`IIndexesOperations`.</span><span class="sxs-lookup"><span data-stu-id="63f82-280">hello type of `ISearchServiceClient.Indexes` has been renamed from `IIndexOperations` too`IIndexesOperations`.</span></span>
* <span data-ttu-id="63f82-281">Hello du type de `ISearchServiceClient.Indexers` a été renommé à partir de `IIndexerOperations` trop`IIndexersOperations`.</span><span class="sxs-lookup"><span data-stu-id="63f82-281">hello type of `ISearchServiceClient.Indexers` has been renamed from `IIndexerOperations` too`IIndexersOperations`.</span></span>
* <span data-ttu-id="63f82-282">Hello du type de `ISearchServiceClient.DataSources` a été renommé à partir de `IDataSourceOperations` trop`IDataSourcesOperations`.</span><span class="sxs-lookup"><span data-stu-id="63f82-282">hello type of `ISearchServiceClient.DataSources` has been renamed from `IDataSourceOperations` too`IDataSourcesOperations`.</span></span>
* <span data-ttu-id="63f82-283">Hello du type de `ISearchIndexClient.Documents` a été renommé à partir de `IDocumentOperations` trop`IDocumentsOperations`.</span><span class="sxs-lookup"><span data-stu-id="63f82-283">hello type of `ISearchIndexClient.Documents` has been renamed from `IDocumentOperations` too`IDocumentsOperations`.</span></span>

<span data-ttu-id="63f82-284">Cette modification est peu probable tooaffect votre code, sauf si vous avez créé des objets factices de ces interfaces à des fins de test.</span><span class="sxs-lookup"><span data-stu-id="63f82-284">This change is unlikely tooaffect your code unless you created mocks of these interfaces for test purposes.</span></span>

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a><span data-ttu-id="63f82-285">Résolution des bogues dans la version 1.1</span><span class="sxs-lookup"><span data-stu-id="63f82-285">Bug fixes in version 1.1</span></span>
<span data-ttu-id="63f82-286">Il a été un bogue dans les versions antérieures de hello Azure Search .NET SDK de tooserialization concernant des classes de modèle personnalisé.</span><span class="sxs-lookup"><span data-stu-id="63f82-286">There was a bug in older versions of hello Azure Search .NET SDK relating tooserialization of custom model classes.</span></span> <span data-ttu-id="63f82-287">bogue de Hello peut se produire si vous avez créé une classe de modèle personnalisé à la propriété d’un type valeur non nullable.</span><span class="sxs-lookup"><span data-stu-id="63f82-287">hello bug could occur if you created a custom model class with a property of a non-nullable value type.</span></span>

#### <a name="steps-tooreproduce"></a><span data-ttu-id="63f82-288">Étapes tooreproduce</span><span class="sxs-lookup"><span data-stu-id="63f82-288">Steps tooreproduce</span></span>
<span data-ttu-id="63f82-289">Créez une classe de modèle personnalisé avec une propriété de type avec valeur ne pouvant être définie sur null.</span><span class="sxs-lookup"><span data-stu-id="63f82-289">Create a custom model class with a property of non-nullable value type.</span></span> <span data-ttu-id="63f82-290">Par exemple, ajoutez une propriété `UnitCount` publique de type `int` au lieu de `int?`.</span><span class="sxs-lookup"><span data-stu-id="63f82-290">For example, add a public `UnitCount` property of type `int` instead of `int?`.</span></span>

<span data-ttu-id="63f82-291">Si vous indexez un document avec la valeur par défaut de hello de ce type (par exemple, 0 pour `int`), champ de hello sera null dans Azure Search.</span><span class="sxs-lookup"><span data-stu-id="63f82-291">If you index a document with hello default value of that type (for example, 0 for `int`), hello field will be null in Azure Search.</span></span> <span data-ttu-id="63f82-292">Si vous recherchez par la suite de ce document, hello `Search` appel lève `JsonSerializationException` signale qu’il ne peut pas convertir que `null` trop`int`.</span><span class="sxs-lookup"><span data-stu-id="63f82-292">If you subsequently search for that document, hello `Search` call will throw `JsonSerializationException` complaining that it can't convert `null` too`int`.</span></span>

<span data-ttu-id="63f82-293">En outre, les filtres peuvent ne pas fonctionnent comme prévu, car la valeur null a été écrite index toohello au lieu de la valeur de hello prévu.</span><span class="sxs-lookup"><span data-stu-id="63f82-293">Also, filters may not work as expected since null was written toohello index instead of hello intended value.</span></span>

#### <a name="fix-details"></a><span data-ttu-id="63f82-294">Corriger des détails</span><span class="sxs-lookup"><span data-stu-id="63f82-294">Fix details</span></span>
<span data-ttu-id="63f82-295">Nous avons résolu ce problème dans la version 1.1 du Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="63f82-295">We have fixed this issue in version 1.1 of hello SDK.</span></span> <span data-ttu-id="63f82-296">Maintenant, si vous avez une classe de modèle comme suit :</span><span class="sxs-lookup"><span data-stu-id="63f82-296">Now, if you have a model class like this:</span></span>

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

<span data-ttu-id="63f82-297">et que vous définissez `IntValue` too0, que valeur est maintenant correctement sérialisée en tant que 0 sur le câble de hello et stockée en tant que 0 dans les index hello.</span><span class="sxs-lookup"><span data-stu-id="63f82-297">and you set `IntValue` too0, that value is now correctly serialized as 0 on hello wire and stored as 0 in hello index.</span></span> <span data-ttu-id="63f82-298">Le retour fonctionne également comme prévu.</span><span class="sxs-lookup"><span data-stu-id="63f82-298">Round tripping also works as expected.</span></span>

<span data-ttu-id="63f82-299">Il connaît une toobe problème potentiel avec cette approche : Si vous utilisez un type de modèle avec une propriété non nullable, vous avez trop**garantir** ne contenant une valeur null pour le champ correspondant de hello aucun document dans votre index.</span><span class="sxs-lookup"><span data-stu-id="63f82-299">There is one potential issue toobe aware of with this approach: If you use a model type with a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="63f82-300">Hello SDK, ni hello API REST Azure Search aidera à vous tooenforce cela.</span><span class="sxs-lookup"><span data-stu-id="63f82-300">Neither hello SDK nor hello Azure Search REST API will help you tooenforce this.</span></span>

<span data-ttu-id="63f82-301">Ce n’est pas simplement une préoccupation hypothétique : imaginez un scénario dans lequel vous ajoutez un nouveau champ tooan index existant qui est de type `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="63f82-301">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="63f82-302">Après la mise à jour de définition de l’index hello, tous les documents aura une valeur null pour ce nouveau champ (étant donné que tous les types sont nullables dans Azure Search).</span><span class="sxs-lookup"><span data-stu-id="63f82-302">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="63f82-303">Si vous utilisez ensuite une classe de modèle avec un non-nullable `int` propriété pour ce champ, vous obtenez un `JsonSerializationException` comme suit lors de la tentative de tooretrieve documents :</span><span class="sxs-lookup"><span data-stu-id="63f82-303">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="63f82-304">Pour cette raison, nous vous recommandons d’utiliser des types pour lesquels la valeur null est autorisée en tant que meilleure pratique.</span><span class="sxs-lookup"><span data-stu-id="63f82-304">For this reason, we still recommend that you use nullable types in your model classes as a best practice.</span></span>

<span data-ttu-id="63f82-305">Pour plus d’informations sur ce correctif de bogue et hello, consultez [ce problème sur GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span><span class="sxs-lookup"><span data-stu-id="63f82-305">For more details on this bug and hello fix, please see [this issue on GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span></span>

