---
title: "Comment documenter des sources de données | Microsoft Docs"
description: "Article de procédure expliquant comment documenter les ressources de données dans Azure Data Catalog."
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
ms.openlocfilehash: ffe951f60afb57524568fe1ed3b3668d0088e124
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="document-data-sources"></a><span data-ttu-id="8a81f-103">Documentation de sources de données</span><span class="sxs-lookup"><span data-stu-id="8a81f-103">Document data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="8a81f-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="8a81f-104">Introduction</span></span>
<span data-ttu-id="8a81f-105">**Microsoft Azure Data Catalog** est un service cloud entièrement géré qui sert de système d'inscription et de détection des sources de données d'entreprise.</span><span class="sxs-lookup"><span data-stu-id="8a81f-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="8a81f-106">En d’autres termes, **Microsoft Azure Data Catalog** vise essentiellement à aider les utilisateurs à détecter, *comprendre*et utiliser des sources de données, et permet aux organisations de mieux exploiter leurs données.</span><span class="sxs-lookup"><span data-stu-id="8a81f-106">In other words, **Azure Data Catalog** is all about helping people discover, *understand*, and use data sources, and helping organizations to get more value from their existing data.</span></span>

<span data-ttu-id="8a81f-107">Quand une source de données est inscrite dans **Azure Data Catalog**, ses métadonnées sont copiées et indexées par le service. Mais ce n’est pas tout.</span><span class="sxs-lookup"><span data-stu-id="8a81f-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by the service, but the story doesn’t end there.</span></span> <span data-ttu-id="8a81f-108">**Azure Data Catalog** permet également aux utilisateurs de fournir leur propre documentation complète pour décrire l’utilisation et les scénarios courants de la source de données.</span><span class="sxs-lookup"><span data-stu-id="8a81f-108">**Azure Data Catalog** also allows users to provide their own complete documentation that can describe the usage and common scenarios for the data source.</span></span>

<span data-ttu-id="8a81f-109">L’article [Annotation de sources de données](data-catalog-how-to-annotate.md)explique comment des experts qui connaissent la source de données peuvent l’annoter avec des balises et une description.</span><span class="sxs-lookup"><span data-stu-id="8a81f-109">In [How to annotate data sources](data-catalog-how-to-annotate.md), you learn that experts who know the data source can annotate it with tags and a description.</span></span> <span data-ttu-id="8a81f-110">Le portail **Azure Data Catalog** inclut un éditeur de texte qui permet aux utilisateurs de documenter entièrement les ressources de données et les conteneurs.</span><span class="sxs-lookup"><span data-stu-id="8a81f-110">The **Azure Data Catalog** portal includes a rich text editor so that users can fully document data assets and containers.</span></span> <span data-ttu-id="8a81f-111">L’éditeur inclut une mise en forme des paragraphes, avec notamment des en-têtes, la mise en forme du texte, des listes à puces, des listes numérotées et des tableaux.</span><span class="sxs-lookup"><span data-stu-id="8a81f-111">The editor includes paragraph formatting, such as headings, text formatting, bulleted lists, numbered lists, and tables.</span></span>

<span data-ttu-id="8a81f-112">Les balises et descriptions sont idéales pour ajouter des annotations simples.</span><span class="sxs-lookup"><span data-stu-id="8a81f-112">Tags and descriptions are great for simple annotations.</span></span> <span data-ttu-id="8a81f-113">Toutefois, pour aider les consommateurs de données à mieux comprendre l’utilisation d’une source de données et les scénarios commerciaux d’une source de données, un expert peut fournir une documentation complète et détaillée.</span><span class="sxs-lookup"><span data-stu-id="8a81f-113">However, to help data consumers better understand the use of a data source, and business scenarios for a data source, an expert can provide complete, detailed documentation.</span></span> <span data-ttu-id="8a81f-114">Il est facile de documenter une source de données.</span><span class="sxs-lookup"><span data-stu-id="8a81f-114">It's easy to document a data source.</span></span> <span data-ttu-id="8a81f-115">Il suffit de sélectionner une ressource de données ou un conteneur et de choisir l’option **Documentation**.</span><span class="sxs-lookup"><span data-stu-id="8a81f-115">Select a data asset or container, and choose **Documentation**.</span></span>

![](media/data-catalog-documentation/data-catalog-documentation.png)

## <a name="documenting-data-assets"></a><span data-ttu-id="8a81f-116">Documentation de ressources de données</span><span class="sxs-lookup"><span data-stu-id="8a81f-116">Documenting data assets</span></span>
<span data-ttu-id="8a81f-117">La documentation **Azure Data Catalog** vous permet d’utiliser votre catalogue de données comme référentiel de contenu pour créer une narration complète de vos ressources de données.</span><span class="sxs-lookup"><span data-stu-id="8a81f-117">The benefit of **Azure Data Catalog** documentation allows you to use your Data Catalog as a content repository to create a complete narrative of your data assets.</span></span> <span data-ttu-id="8a81f-118">Vous pouvez explorer le contenu détaillé décrivant les conteneurs et tables.</span><span class="sxs-lookup"><span data-stu-id="8a81f-118">You can explore detailed content that describes containers and tables.</span></span> <span data-ttu-id="8a81f-119">Si vous utilisez déjà un autre référentiel de contenu, tel que SharePoint ou un partage de fichiers, vous pouvez ajouter des liens de documentation à votre ressource pour référencer ce contenu existant.</span><span class="sxs-lookup"><span data-stu-id="8a81f-119">If you already have content in another content repository, such as SharePoint or a file share, you can add to the asset documentation links to reference this existing content.</span></span> <span data-ttu-id="8a81f-120">Vos documents existants seront ainsi mieux exposés.</span><span class="sxs-lookup"><span data-stu-id="8a81f-120">This feature makes your existing documents more discoverable.</span></span>

> [!NOTE]
> <span data-ttu-id="8a81f-121">La documentation n’est pas incluse dans l’index de recherche.</span><span class="sxs-lookup"><span data-stu-id="8a81f-121">Documentation is not included in search index.</span></span>
>
>

![](media/data-catalog-documentation/data-catalog-documentation2.png)

<span data-ttu-id="8a81f-122">Le niveau de documentation peut aller d’une simple description des caractéristiques et de la valeur d’un conteneur de ressources de données à une description détaillée du schéma de table dans un conteneur.</span><span class="sxs-lookup"><span data-stu-id="8a81f-122">The level of documentation can range from describing the characteristics and value of a data asset container to a detailed description of table schema within a container.</span></span> <span data-ttu-id="8a81f-123">Le niveau de documentation fourni doit être dicté par vos besoins métiers.</span><span class="sxs-lookup"><span data-stu-id="8a81f-123">The level of documentation provided should be driven by your business needs.</span></span> <span data-ttu-id="8a81f-124">De façon générale, voici cependant quelques avantages et inconvénients associés à la documentation de ressources de données :</span><span class="sxs-lookup"><span data-stu-id="8a81f-124">But in general, here are a few pros and cons of documenting data assets:</span></span>

* <span data-ttu-id="8a81f-125">Documenter uniquement un conteneur : tout le contenu se trouve dans un même emplacement, mais ne comporte sans doute pas les informations nécessaires pour permettre aux utilisateurs de prendre une décision informée.</span><span class="sxs-lookup"><span data-stu-id="8a81f-125">Document just a container: All the content is in one place, but might lack necessary details for users to make an informed decision.</span></span>
* <span data-ttu-id="8a81f-126">Documenter uniquement les tables : le contenu se rapporte à l’objet en question, mais les documents sont disséminés à plusieurs emplacements.</span><span class="sxs-lookup"><span data-stu-id="8a81f-126">Document just the tables: Content is specific to that object, but your users have multiple places for documents.</span></span>
* <span data-ttu-id="8a81f-127">Documenter les conteneurs et les tables : l’approche la plus complète, qui peut toutefois impliquer un effort supplémentaire pour la gestion des documents.</span><span class="sxs-lookup"><span data-stu-id="8a81f-127">Document containers and tables: Most comprehensive approach, but might introduce more maintenance of the documents.</span></span>

## <a name="summary"></a><span data-ttu-id="8a81f-128">Résumé</span><span class="sxs-lookup"><span data-stu-id="8a81f-128">Summary</span></span>
<span data-ttu-id="8a81f-129">La documentation des sources de données avec **Azure Data Catalog** peut créer une narration sur vos ressources de données avec le degré de détail dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="8a81f-129">Documenting data sources with **Azure Data Catalog** can create a narrative about your data assets in as much detail as you need.</span></span>  <span data-ttu-id="8a81f-130">À l’aide de liens, vous pouvez référencer du contenu stocké dans un référentiel de contenu existant qui rassemble vos documents et vos ressources de données existants.</span><span class="sxs-lookup"><span data-stu-id="8a81f-130">By using links, you can link to content stored in an existing content repository, which brings your existing docs and data assets together.</span></span> <span data-ttu-id="8a81f-131">Une fois que vos utilisateurs accèdent aux ressources de données appropriées, ils peuvent bénéficier d’un ensemble de documentation complet.</span><span class="sxs-lookup"><span data-stu-id="8a81f-131">Once your users discover appropriate data assets, they can have a complete set of documentation.</span></span>