---
title: "Mise à niveau vers la version 2016-09-01 de l’API REST du service Recherche Azure | Microsoft Docs"
description: "Mise à niveau vers la version 2016-09-01 de l’API REST du service Recherche Azure"
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
ms.openlocfilehash: f6a189c2e314b91c490583a86d8bacca8ec78a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrading-to-the-azure-search-service-rest-api-version-2016-09-01"></a><span data-ttu-id="7fd67-103">Mise à niveau vers la version 2016-09-01 de l’API REST du service Recherche Azure</span><span class="sxs-lookup"><span data-stu-id="7fd67-103">Upgrading to the Azure Search Service REST API version 2016-09-01</span></span>
<span data-ttu-id="7fd67-104">Si vous utilisez la version 2015-02-28 ou 2015-02-28-Preview de [l’API REST du service Recherche Azure](https://msdn.microsoft.com/library/azure/dn798935.aspx), cet article vous aidera à mettre à niveau votre application pour utiliser la nouvelle version de l’API (2016-09-01).</span><span class="sxs-lookup"><span data-stu-id="7fd67-104">If you're using version 2015-02-28 or 2015-02-28-Preview of the [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application to use the next generally available API version, 2016-09-01.</span></span>

<span data-ttu-id="7fd67-105">La version 2016-09-01 de l’API REST contient des modifications des versions antérieures.</span><span class="sxs-lookup"><span data-stu-id="7fd67-105">Version 2016-09-01 of the REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="7fd67-106">Ces modifications sont, pour la plupart, à compatibilité descendante. La modification de votre code est donc facilitée, selon la version que vous utilisiez précédemment.</span><span class="sxs-lookup"><span data-stu-id="7fd67-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="7fd67-107">Consultez la page [Procédure de mise à niveau](#UpgradeSteps) pour obtenir des instructions sur la façon de modifier votre code pour qu’il utilise la nouvelle version de l’API.</span><span class="sxs-lookup"><span data-stu-id="7fd67-107">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="7fd67-108">Votre instance de service Recherche Azure prend en charge plusieurs versions de l’API REST, y compris la plus récente.</span><span class="sxs-lookup"><span data-stu-id="7fd67-108">Your Azure Search service instance supports several REST API versions, including the latest one.</span></span> <span data-ttu-id="7fd67-109">Vous pouvez continuer à utiliser une version lorsqu’elle n’est pas la plus récente, mais nous vous recommandons de migrer votre code pour utiliser la dernière version.</span><span class="sxs-lookup"><span data-stu-id="7fd67-109">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a><span data-ttu-id="7fd67-110">Nouveautés de la version 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="7fd67-110">What's new in version 2016-09-01</span></span>
<span data-ttu-id="7fd67-111">La version 2016-09-01 est la deuxième version généralement disponible de l’API REST du service Recherche Azure.</span><span class="sxs-lookup"><span data-stu-id="7fd67-111">Version 2016-09-01 is the second generally available release of the Azure Search Service REST API.</span></span> <span data-ttu-id="7fd67-112">Cette version de l’API comprend les nouvelles fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="7fd67-112">New features in this API version include:</span></span>

* <span data-ttu-id="7fd67-113">Des [analyseurs personnalisés](https://aka.ms/customanalyzers), qui vous permettent de contrôler le processus de conversion de texte en jetons d’indexation et de recherche.</span><span class="sxs-lookup"><span data-stu-id="7fd67-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you to take control over the process of converting text into indexable and searchable tokens.</span></span>
* <span data-ttu-id="7fd67-114">Des indexeurs [Stockage Blob Azure](search-howto-indexing-azure-blob-storage.md) et [Stockage Table Azure](search-howto-indexing-azure-tables.md), qui vous permettent d’importer facilement des données depuis le stockage Azure dans la Recherche Azure, selon une planification ou à la demande.</span><span class="sxs-lookup"><span data-stu-id="7fd67-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you to easily import data from Azure storage into Azure Search on a schedule or on-demand.</span></span>
* <span data-ttu-id="7fd67-115">Des [mappages de champs](search-indexer-field-mappings.md), qui vous permettent de personnaliser la façon dont les indexeurs importent des données dans la Recherche Azure.</span><span class="sxs-lookup"><span data-stu-id="7fd67-115">[Field mappings](search-indexer-field-mappings.md), which allow you to customize how indexers import data into Azure Search.</span></span>
* <span data-ttu-id="7fd67-116">ETag, qui vous permet de mettre à jour les définitions d’index, les indexeurs et les sources de données avec accès concurrentiel sécurisé.</span><span class="sxs-lookup"><span data-stu-id="7fd67-116">ETags, which allow you to update the definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span></span> 

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a><span data-ttu-id="7fd67-117">Procédure de mise à niveau</span><span class="sxs-lookup"><span data-stu-id="7fd67-117">Steps to upgrade</span></span>
<span data-ttu-id="7fd67-118">Si vous effectuez une mise à niveau à partir de la version 2015-02-28, vous n’aurez probablement pas à modifier votre code, en dehors du numéro de version.</span><span class="sxs-lookup"><span data-stu-id="7fd67-118">If you are upgrading from version 2015-02-28, you probably won't have to make any changes to your code, other than to change the version number.</span></span> <span data-ttu-id="7fd67-119">Les seules situations dans lesquelles vous pouvez avoir à modifier votre code sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="7fd67-119">The only situations in which you may need to change code are when:</span></span>

* <span data-ttu-id="7fd67-120">Lorsque votre code échoue, car des propriétés non reconnues sont renvoyées dans une réponse de l’API.</span><span class="sxs-lookup"><span data-stu-id="7fd67-120">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="7fd67-121">Par défaut, votre application doit ignorer les propriétés qu’elle ne comprend pas.</span><span class="sxs-lookup"><span data-stu-id="7fd67-121">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="7fd67-122">Votre code conserve des demandes d’API et tente de les renvoyer à la nouvelle version de l’API.</span><span class="sxs-lookup"><span data-stu-id="7fd67-122">Your code persists API requests and tries to resend them to the new API version.</span></span> <span data-ttu-id="7fd67-123">Par exemple, cela peut se produire si votre application conserve les jetons de continuation renvoyés par l’API Recherche (pour plus d’informations, recherchez `@search.nextPageParameters` dans les [références sur l’API Recherche](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span><span class="sxs-lookup"><span data-stu-id="7fd67-123">For example, this might happen if your application persists continuation tokens returned from the Search API (for more information, look for `@search.nextPageParameters` in the [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span></span>

<span data-ttu-id="7fd67-124">Si vous êtes concerné par l’une de ces situations, vous aurez peut-être à modifier votre code en conséquence.</span><span class="sxs-lookup"><span data-stu-id="7fd67-124">If either of these situations apply to you, then you may need to change your code accordingly.</span></span> <span data-ttu-id="7fd67-125">Dans le cas contraire, aucune modification n’est nécessaire, sauf si vous souhaitez commencer à utiliser les [nouvelles fonctionnalités](#WhatsNew) de la version 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="7fd67-125">Otherwise, no changes should be necessary unless you want to start using the [new features](#WhatsNew) of version 2016-09-01.</span></span>

<span data-ttu-id="7fd67-126">Cela s’applique également si vous effectuez une mise à niveau à partir de la version 2015-02-28-Preview. Cependant, certaines fonctionnalités ne sont pas disponibles dans la version 2016-09-01 :</span><span class="sxs-lookup"><span data-stu-id="7fd67-126">If you are upgrading from version 2015-02-28-Preview, the above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span></span>

* <span data-ttu-id="7fd67-127">Prise en charge des indexeurs Stockage Blob Azure pour les fichiers CSV et les objets Blob contenant des tableaux JSON.</span><span class="sxs-lookup"><span data-stu-id="7fd67-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="7fd67-128">Synonymes</span><span class="sxs-lookup"><span data-stu-id="7fd67-128">Synonyms</span></span>
* <span data-ttu-id="7fd67-129">Requêtes « More like this »</span><span class="sxs-lookup"><span data-stu-id="7fd67-129">"More like this" queries</span></span>

<span data-ttu-id="7fd67-130">Si votre code utilise ces fonctionnalités, vous ne pourrez pas effectuer une mise à niveau vers la version 2016-09-01 sans supprimer votre utilisation de ces fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="7fd67-130">If your code uses these features, you will not be able to upgrade to 2016-09-01 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7fd67-131">N’oubliez pas que les API d’évaluation sont destinées à être utilisées à des fins de test et d’évaluation, et non dans les environnements de production.</span><span class="sxs-lookup"><span data-stu-id="7fd67-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="7fd67-132">Conclusion</span><span class="sxs-lookup"><span data-stu-id="7fd67-132">Conclusion</span></span>
<span data-ttu-id="7fd67-133">Pour plus d’informations sur l’utilisation de l’API REST du service Recherche Azure, consultez les [références d’API](https://msdn.microsoft.com/library/azure/dn798935.aspx) récemment mises à jour sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="7fd67-133">If you need more details on using the Azure Search Service REST API, see the recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span></span>

<span data-ttu-id="7fd67-134">Vos commentaires sur la Recherche Azure sont les bienvenus.</span><span class="sxs-lookup"><span data-stu-id="7fd67-134">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="7fd67-135">Si vous rencontrez des problèmes, n’hésitez pas à nous demander de l’aide sur le [forum MSDN de la Recherche Azure ](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) ou sur [StackOverflow](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="7fd67-135">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="7fd67-136">Si vous souhaitez poser une question sur la Recherche Azure sur StackOverflow, veillez à utiliser le mot clé `azure-search`.</span><span class="sxs-lookup"><span data-stu-id="7fd67-136">If you're asking a question about Azure Search on StackOverflow, make sure to tag it with `azure-search`.</span></span>

<span data-ttu-id="7fd67-137">Merci d’utiliser Azure Search !</span><span class="sxs-lookup"><span data-stu-id="7fd67-137">Thank you for using Azure Search!</span></span>

