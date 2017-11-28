---
title: "sources de données aaaHow toodocument | Documents Microsoft"
description: "Mise en surbrillance de la procédure-tooarticle comment toodocument les ressources de données dans Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 053b1701-b848-4ada-b726-6f485caa9961
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 4e46838d91ab4d0c0bc569ac526a0c729134bb10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="document-data-sources"></a><span data-ttu-id="95e46-103">Documentation de sources de données</span><span class="sxs-lookup"><span data-stu-id="95e46-103">Document data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="95e46-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="95e46-104">Introduction</span></span>
<span data-ttu-id="95e46-105">**Microsoft Azure Data Catalog** est un service cloud entièrement géré qui sert de système d'inscription et de détection des sources de données d'entreprise.</span><span class="sxs-lookup"><span data-stu-id="95e46-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="95e46-106">En d’autres termes, **Azure Data Catalog** est d’aider les utilisateurs à découvrir, *comprendre*et utiliser des sources de données et de contribuer tooget organisations plus de valeur à partir de leurs données.</span><span class="sxs-lookup"><span data-stu-id="95e46-106">In other words, **Azure Data Catalog** is all about helping people discover, *understand*, and use data sources, and helping organizations tooget more value from their existing data.</span></span>

<span data-ttu-id="95e46-107">Quand une source de données est enregistrée avec **Azure Data Catalog**, ses métadonnées sont copiée et est indexée par le service de hello, mais un récit hello ne se termine pas il.</span><span class="sxs-lookup"><span data-stu-id="95e46-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by hello service, but hello story doesn’t end there.</span></span> <span data-ttu-id="95e46-108">**Azure Data Catalog** permet également aux utilisateurs tooprovide leur propre documentation complète décrivant l’utilisation de hello et des scénarios courants pour la source de données hello.</span><span class="sxs-lookup"><span data-stu-id="95e46-108">**Azure Data Catalog** also allows users tooprovide their own complete documentation that can describe hello usage and common scenarios for hello data source.</span></span>

<span data-ttu-id="95e46-109">Dans [comment tooannotate des sources de données](data-catalog-how-to-annotate.md), vous découvrez que les experts qui connaissent la source de données hello peuvent l’annoter avec balises et une description.</span><span class="sxs-lookup"><span data-stu-id="95e46-109">In [How tooannotate data sources](data-catalog-how-to-annotate.md), you learn that experts who know hello data source can annotate it with tags and a description.</span></span> <span data-ttu-id="95e46-110">Hello **Azure Data Catalog** portail inclut un éditeur de texte afin que les utilisateurs peuvent documenter entièrement les conteneurs et les ressources de données.</span><span class="sxs-lookup"><span data-stu-id="95e46-110">hello **Azure Data Catalog** portal includes a rich text editor so that users can fully document data assets and containers.</span></span> <span data-ttu-id="95e46-111">éditeur de Hello comprend de mise en forme, telles que des titres, mise en forme, les listes à puces, les listes numérotées et les tables de texte de paragraphe.</span><span class="sxs-lookup"><span data-stu-id="95e46-111">hello editor includes paragraph formatting, such as headings, text formatting, bulleted lists, numbered lists, and tables.</span></span>

<span data-ttu-id="95e46-112">Les balises et descriptions sont idéales pour ajouter des annotations simples.</span><span class="sxs-lookup"><span data-stu-id="95e46-112">Tags and descriptions are great for simple annotations.</span></span> <span data-ttu-id="95e46-113">Toutefois, les consommateurs de données toohelp mieux comprennent utilisez hello d’une source de données et les scénarios d’entreprise pour une source de données, un expert peuvent fournir la documentation complète et détaillée.</span><span class="sxs-lookup"><span data-stu-id="95e46-113">However, toohelp data consumers better understand hello use of a data source, and business scenarios for a data source, an expert can provide complete, detailed documentation.</span></span> <span data-ttu-id="95e46-114">Il est facile toodocument une source de données.</span><span class="sxs-lookup"><span data-stu-id="95e46-114">It's easy toodocument a data source.</span></span> <span data-ttu-id="95e46-115">Il suffit de sélectionner une ressource de données ou un conteneur et de choisir l’option **Documentation**.</span><span class="sxs-lookup"><span data-stu-id="95e46-115">Select a data asset or container, and choose **Documentation**.</span></span>

![](media/data-catalog-documentation/data-catalog-documentation.png)

## <a name="documenting-data-assets"></a><span data-ttu-id="95e46-116">Documentation de ressources de données</span><span class="sxs-lookup"><span data-stu-id="95e46-116">Documenting data assets</span></span>
<span data-ttu-id="95e46-117">Hello avantage de **Azure Data Catalog** documentation vous permet de toouse vos données de catalogue comme un référentiel de contenu de toocreate une narration complète de vos ressources de données.</span><span class="sxs-lookup"><span data-stu-id="95e46-117">hello benefit of **Azure Data Catalog** documentation allows you toouse your Data Catalog as a content repository toocreate a complete narrative of your data assets.</span></span> <span data-ttu-id="95e46-118">Vous pouvez explorer le contenu détaillé décrivant les conteneurs et tables.</span><span class="sxs-lookup"><span data-stu-id="95e46-118">You can explore detailed content that describes containers and tables.</span></span> <span data-ttu-id="95e46-119">Si vous avez déjà contenu dans un autre référentiel de contenu, tel que SharePoint ou un partage de fichiers, vous pouvez ajouter toohello asset documentation liens tooreference ce contenu existant.</span><span class="sxs-lookup"><span data-stu-id="95e46-119">If you already have content in another content repository, such as SharePoint or a file share, you can add toohello asset documentation links tooreference this existing content.</span></span> <span data-ttu-id="95e46-120">Vos documents existants seront ainsi mieux exposés.</span><span class="sxs-lookup"><span data-stu-id="95e46-120">This feature makes your existing documents more discoverable.</span></span>

> [!NOTE]
> <span data-ttu-id="95e46-121">La documentation n’est pas incluse dans l’index de recherche.</span><span class="sxs-lookup"><span data-stu-id="95e46-121">Documentation is not included in search index.</span></span>
>
>

![](media/data-catalog-documentation/data-catalog-documentation2.png)

<span data-ttu-id="95e46-122">au niveau de la documentation Hello peut varier de décrire les caractéristiques de hello et la valeur de données asset conteneur tooa description détaillée du schéma de la table dans un conteneur.</span><span class="sxs-lookup"><span data-stu-id="95e46-122">hello level of documentation can range from describing hello characteristics and value of a data asset container tooa detailed description of table schema within a container.</span></span> <span data-ttu-id="95e46-123">niveau Hello de documentation fournie doit être piloté par les besoins de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="95e46-123">hello level of documentation provided should be driven by your business needs.</span></span> <span data-ttu-id="95e46-124">De façon générale, voici cependant quelques avantages et inconvénients associés à la documentation de ressources de données :</span><span class="sxs-lookup"><span data-stu-id="95e46-124">But in general, here are a few pros and cons of documenting data assets:</span></span>

* <span data-ttu-id="95e46-125">Un simple conteneur de document : tout le contenu hello est dans un seul emplacement, mais peut nécessaire du manque d’informations pour les utilisateurs toomake une décision informée.</span><span class="sxs-lookup"><span data-stu-id="95e46-125">Document just a container: All hello content is in one place, but might lack necessary details for users toomake an informed decision.</span></span>
* <span data-ttu-id="95e46-126">Que les tables hello de documents : contenu est l’objet de toothat spécifique, mais vos utilisateurs disposent de plusieurs emplacements pour les documents.</span><span class="sxs-lookup"><span data-stu-id="95e46-126">Document just hello tables: Content is specific toothat object, but your users have multiple places for documents.</span></span>
* <span data-ttu-id="95e46-127">Les tables et les conteneurs de documents : une approche plus complète, mais risque de présenter plus de maintenance de documents de hello.</span><span class="sxs-lookup"><span data-stu-id="95e46-127">Document containers and tables: Most comprehensive approach, but might introduce more maintenance of hello documents.</span></span>

## <a name="summary"></a><span data-ttu-id="95e46-128">Résumé</span><span class="sxs-lookup"><span data-stu-id="95e46-128">Summary</span></span>
<span data-ttu-id="95e46-129">La documentation des sources de données avec **Azure Data Catalog** peut créer une narration sur vos ressources de données avec le degré de détail dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="95e46-129">Documenting data sources with **Azure Data Catalog** can create a narrative about your data assets in as much detail as you need.</span></span>  <span data-ttu-id="95e46-130">À l’aide de liens, vous pouvez lier toocontent stockée dans un référentiel de contenu existant, qui rassemble vos documents existants et les ressources de données.</span><span class="sxs-lookup"><span data-stu-id="95e46-130">By using links, you can link toocontent stored in an existing content repository, which brings your existing docs and data assets together.</span></span> <span data-ttu-id="95e46-131">Une fois que vos utilisateurs accèdent aux ressources de données appropriées, ils peuvent bénéficier d’un ensemble de documentation complet.</span><span class="sxs-lookup"><span data-stu-id="95e46-131">Once your users discover appropriate data assets, they can have a complete set of documentation.</span></span>