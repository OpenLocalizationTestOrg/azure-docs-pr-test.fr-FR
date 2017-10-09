---
title: aaaUpgrading toohello API REST du Service Azure Search version 2016-09-01 | Documents Microsoft
description: "La mise à niveau toohello API REST du Service Azure Search version 2016-09-01"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: d0276b9cc52996a59f9aa726c27e62c6082eb908
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a><span data-ttu-id="ebb44-103">La mise à niveau toohello API REST du Service Azure Search version 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="ebb44-103">Upgrading toohello Azure Search Service REST API version 2016-09-01</span></span>
<span data-ttu-id="ebb44-104">Si vous utilisez la version 2015-02-28 ou 2015-02-28-Preview Hello [API REST de Service Azure Search](https://msdn.microsoft.com/library/azure/dn798935.aspx), cet article va vous aider à mettre à niveau votre application toouse hello suivant disponible version de l’API, 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="ebb44-104">If you're using version 2015-02-28 or 2015-02-28-Preview of hello [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application toouse hello next generally available API version, 2016-09-01.</span></span>

<span data-ttu-id="ebb44-105">Version 2016-09-01 de l’API REST de hello contient certaines modifications à partir de versions antérieures.</span><span class="sxs-lookup"><span data-stu-id="ebb44-105">Version 2016-09-01 of hello REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="ebb44-106">Ces modifications sont, pour la plupart, à compatibilité descendante. La modification de votre code est donc facilitée, selon la version que vous utilisiez précédemment.</span><span class="sxs-lookup"><span data-stu-id="ebb44-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="ebb44-107">Consultez [étapes tooupgrade](#UpgradeSteps) pour obtenir des instructions sur la façon de toochange votre code toouse hello nouvelle version de l’API.</span><span class="sxs-lookup"><span data-stu-id="ebb44-107">See [Steps tooupgrade](#UpgradeSteps) for instructions on how toochange your code toouse hello new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="ebb44-108">Votre instance du service Azure Search prend en charge plusieurs versions de l’API REST, y compris hello version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="ebb44-108">Your Azure Search service instance supports several REST API versions, including hello latest one.</span></span> <span data-ttu-id="ebb44-109">Vous pouvez continuer toouse une version lorsqu’il n’est plus hello version la plus récente, mais nous vous recommandons de migrer votre code toouse hello dernière version.</span><span class="sxs-lookup"><span data-stu-id="ebb44-109">You can continue toouse a version when it is no longer hello latest one, but we recommend that you migrate your code toouse hello newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a><span data-ttu-id="ebb44-110">Nouveautés de la version 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="ebb44-110">What's new in version 2016-09-01</span></span>
<span data-ttu-id="ebb44-111">Version 2016-09-01 est la deuxième version généralement disponible hello Hello API REST de Service Azure Search.</span><span class="sxs-lookup"><span data-stu-id="ebb44-111">Version 2016-09-01 is hello second generally available release of hello Azure Search Service REST API.</span></span> <span data-ttu-id="ebb44-112">Cette version de l’API comprend les nouvelles fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="ebb44-112">New features in this API version include:</span></span>

* <span data-ttu-id="ebb44-113">[Analyseurs personnalisés](https://aka.ms/customanalyzers), qui vous permettent de contrôler de tootake de processus hello de conversion de texte en jetons indexables et de recherches.</span><span class="sxs-lookup"><span data-stu-id="ebb44-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you tootake control over hello process of converting text into indexable and searchable tokens.</span></span>
* <span data-ttu-id="ebb44-114">[Stockage d’objets Blob Azure](search-howto-indexing-azure-blob-storage.md) et [Azure Table Storage](search-howto-indexing-azure-tables.md) indexeurs, ce qui vous tooeasily importer des données depuis le stockage Azure dans Azure Search dans une planification ou d’une demande.</span><span class="sxs-lookup"><span data-stu-id="ebb44-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you tooeasily import data from Azure storage into Azure Search on a schedule or on-demand.</span></span>
* <span data-ttu-id="ebb44-115">[Mappages de champ](search-indexer-field-mappings.md), qui vous permettent de toocustomize comment indexeurs importer des données dans Azure Search.</span><span class="sxs-lookup"><span data-stu-id="ebb44-115">[Field mappings](search-indexer-field-mappings.md), which allow you toocustomize how indexers import data into Azure Search.</span></span>
* <span data-ttu-id="ebb44-116">ETags vous permettant de définitions de hello tooupdate d’index, indexeurs et sources de données de manière concurrentiel.</span><span class="sxs-lookup"><span data-stu-id="ebb44-116">ETags, which allow you tooupdate hello definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span></span> 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a><span data-ttu-id="ebb44-117">Étapes tooupgrade</span><span class="sxs-lookup"><span data-stu-id="ebb44-117">Steps tooupgrade</span></span>
<span data-ttu-id="ebb44-118">Si vous mettez à niveau à partir de la version 2015-02-28, vous ne disposez probablement toomake tout code tooyour de modifications, que le numéro de version toochange hello.</span><span class="sxs-lookup"><span data-stu-id="ebb44-118">If you are upgrading from version 2015-02-28, you probably won't have toomake any changes tooyour code, other than toochange hello version number.</span></span> <span data-ttu-id="ebb44-119">les situations uniquement Hello dans lesquelles vous devrez peut-être toochange code sont quand :</span><span class="sxs-lookup"><span data-stu-id="ebb44-119">hello only situations in which you may need toochange code are when:</span></span>

* <span data-ttu-id="ebb44-120">Lorsque votre code échoue, car des propriétés non reconnues sont renvoyées dans une réponse de l’API.</span><span class="sxs-lookup"><span data-stu-id="ebb44-120">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="ebb44-121">Par défaut, votre application doit ignorer les propriétés qu’elle ne comprend pas.</span><span class="sxs-lookup"><span data-stu-id="ebb44-121">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="ebb44-122">Votre code persiste des demandes de l’API et tente de tooresend les toohello nouvelle version de l’API.</span><span class="sxs-lookup"><span data-stu-id="ebb44-122">Your code persists API requests and tries tooresend them toohello new API version.</span></span> <span data-ttu-id="ebb44-123">Par exemple, cela peut se produire si votre application conserve les jetons de continuation retournés à partir de l’API de recherche de hello (pour plus d’informations, recherchez `@search.nextPageParameters` Bonjour [référence des API de recherche](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span><span class="sxs-lookup"><span data-stu-id="ebb44-123">For example, this might happen if your application persists continuation tokens returned from hello Search API (for more information, look for `@search.nextPageParameters` in hello [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span></span>

<span data-ttu-id="ebb44-124">Si une des situations suivantes s’appliquent tooyou, il vous faudra peut-être toochange votre code en conséquence.</span><span class="sxs-lookup"><span data-stu-id="ebb44-124">If either of these situations apply tooyou, then you may need toochange your code accordingly.</span></span> <span data-ttu-id="ebb44-125">Dans le cas contraire, aucune modification ne doit être nécessaire sauf si vous souhaitez toostart à l’aide de hello [nouvelles fonctionnalités](#WhatsNew) de version 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="ebb44-125">Otherwise, no changes should be necessary unless you want toostart using hello [new features](#WhatsNew) of version 2016-09-01.</span></span>

<span data-ttu-id="ebb44-126">Si vous mettez à niveau à partir de la version 2015-02-28-Preview, hello ci-dessus s’applique également, mais vous devez également être conscient que certaines fonctionnalités en version préliminaire ne sont pas disponibles dans la version 2016-09-01 :</span><span class="sxs-lookup"><span data-stu-id="ebb44-126">If you are upgrading from version 2015-02-28-Preview, hello above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span></span>

* <span data-ttu-id="ebb44-127">Prise en charge des indexeurs Stockage Blob Azure pour les fichiers CSV et les objets Blob contenant des tableaux JSON.</span><span class="sxs-lookup"><span data-stu-id="ebb44-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="ebb44-128">Synonymes</span><span class="sxs-lookup"><span data-stu-id="ebb44-128">Synonyms</span></span>
* <span data-ttu-id="ebb44-129">Requêtes « More like this »</span><span class="sxs-lookup"><span data-stu-id="ebb44-129">"More like this" queries</span></span>

<span data-ttu-id="ebb44-130">Si votre code utilise ces fonctionnalités, vous ne serez pas en mesure de tooupgrade too2016-09-01 sans supprimer l’utilisation de leur.</span><span class="sxs-lookup"><span data-stu-id="ebb44-130">If your code uses these features, you will not be able tooupgrade too2016-09-01 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ebb44-131">N’oubliez pas que les API d’évaluation sont destinées à être utilisées à des fins de test et d’évaluation, et non dans les environnements de production.</span><span class="sxs-lookup"><span data-stu-id="ebb44-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="ebb44-132">Conclusion</span><span class="sxs-lookup"><span data-stu-id="ebb44-132">Conclusion</span></span>
<span data-ttu-id="ebb44-133">Si vous avez besoin de plus de détails sur l’utilisation de hello API REST de Service Azure Search, consultez hello récemment mis à jour [référence de l’API](https://msdn.microsoft.com/library/azure/dn798935.aspx) sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="ebb44-133">If you need more details on using hello Azure Search Service REST API, see hello recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span></span>

<span data-ttu-id="ebb44-134">Vos commentaires sur la Recherche Azure sont les bienvenus.</span><span class="sxs-lookup"><span data-stu-id="ebb44-134">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="ebb44-135">Si vous rencontrez des problèmes, vous pouvez tooask libre nous de l’aide sur hello [forum MSDN de recherche Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) ou [StackOverflow](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="ebb44-135">If you encounter problems, feel free tooask us for help on hello [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="ebb44-136">Si vous êtes poser une question concernant Azure rechercher sur StackOverflow, vérifiez les tootag qu’avec `azure-search`.</span><span class="sxs-lookup"><span data-stu-id="ebb44-136">If you're asking a question about Azure Search on StackOverflow, make sure tootag it with `azure-search`.</span></span>

<span data-ttu-id="ebb44-137">Merci d’utiliser Azure Search !</span><span class="sxs-lookup"><span data-stu-id="ebb44-137">Thank you for using Azure Search!</span></span>

