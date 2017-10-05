---
title: "Utilisation des sources de données « Big Data » | Microsoft Docs"
description: "Article de procédure expliquant comment utiliser Azure Data Catalog avec des sources de données « volumineuses », notamment le Stockage Blob Azure, Azure Data Lake et les fichiers Hadoop HDFS."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 626d1568-0780-4726-bad1-9c5000c6b31a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 001d80ce42f0e87276e59d70dffb75eb561d96cd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-work-with-big-data-sources-in-azure-data-catalog"></a><span data-ttu-id="4b413-103">Utilisation des sources de données volumineuses dans Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="4b413-103">How to work with big data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="4b413-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="4b413-104">Introduction</span></span>
<span data-ttu-id="4b413-105">**Microsoft Azure Data Catalog** est un service cloud entièrement géré qui sert de système d'inscription et de détection des sources de données d'entreprise.</span><span class="sxs-lookup"><span data-stu-id="4b413-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="4b413-106">Il vise essentiellement à aider les utilisateurs à détecter, comprendre et utiliser des sources de données, et à permettre aux organisations de mieux exploiter leurs sources données existantes, y compris le Big Data.</span><span class="sxs-lookup"><span data-stu-id="4b413-106">It is all about helping people discover, understand, and use data sources, and helping organizations to get more value from their existing data sources, including big data.</span></span>

<span data-ttu-id="4b413-107">**Azure Data Catalog** prend en charge l’inscription d’objets et de répertoire de Stockage d’objets blob Azure ainsi que des fichiers et des répertoires HDFS Hadoop.</span><span class="sxs-lookup"><span data-stu-id="4b413-107">**Azure Data Catalog** supports the registration of Azure Blog Storage blobs and directories as well as Hadoop HDFS files and directories.</span></span> <span data-ttu-id="4b413-108">La nature semi-structurée des sources de données offre une grande flexibilité.</span><span class="sxs-lookup"><span data-stu-id="4b413-108">The semi-structured nature of these data sources provides great flexibility.</span></span> <span data-ttu-id="4b413-109">Toutefois, pour réellement profiter de leur enregistrement dans **Azure Data Catalog**, les utilisateurs doivent comprendre comment sont organisées les sources de données.</span><span class="sxs-lookup"><span data-stu-id="4b413-109">However, to get the most value from registering them with **Azure Data Catalog**, users must consider how the data sources are organized.</span></span>

## <a name="directories-as-logical-data-sets"></a><span data-ttu-id="4b413-110">Répertoires sous forme de jeux de données logiques</span><span class="sxs-lookup"><span data-stu-id="4b413-110">Directories as logical data sets</span></span>
<span data-ttu-id="4b413-111">Un modèle répandu d’organisation de source de données volumineuses consiste à traiter des répertoires sous forme de jeux de données logique.</span><span class="sxs-lookup"><span data-stu-id="4b413-111">A common pattern for organizing big data sources is to treat directories as logical data sets.</span></span> <span data-ttu-id="4b413-112">Des répertoires de niveau supérieur sont utilisés pour définir un jeu de données, les sous-dossiers définissent des partitions, et les fichiers qu’ils contiennent stockent les données elles-mêmes.</span><span class="sxs-lookup"><span data-stu-id="4b413-112">Top-level directories are used to define a data set, while subfolders define partitions, and the files they contain store the data itself.</span></span>

<span data-ttu-id="4b413-113">Voici quelques exemples de ce modèle :</span><span class="sxs-lookup"><span data-stu-id="4b413-113">An example of this pattern might be:</span></span>

    \vehicle_maintenance_events
        \2013
        \2014
        \2015
            \01
                \2015-01-trailer01.csv
                \2015-01-trailer92.csv
                \2015-01-canister9635.csv
                ...
    \location_tracking_events
        \2013
        ...

<span data-ttu-id="4b413-114">Dans cet exemple, vehicle_maintenance_events et location_tracking_events représentent les jeux de données logiques.</span><span class="sxs-lookup"><span data-stu-id="4b413-114">In this example, vehicle_maintenance_events and location_tracking_events represent logical data sets.</span></span> <span data-ttu-id="4b413-115">Chacun de ces dossiers contient des fichiers de données organisés par année et par mois en sous-dossiers.</span><span class="sxs-lookup"><span data-stu-id="4b413-115">Each of these folders contains data files that are organized by year and month into subfolders.</span></span> <span data-ttu-id="4b413-116">Chacun de ces dossiers peut contenir des centaines ou des milliers de fichiers.</span><span class="sxs-lookup"><span data-stu-id="4b413-116">Each of these folders could potentially contain hundreds or thousands of files.</span></span>

<span data-ttu-id="4b413-117">Dans ce modèle, l’enregistrement des fichiers individuels auprès d’ **Azure Data Catalog** ne sert sans doute à rien.</span><span class="sxs-lookup"><span data-stu-id="4b413-117">In this pattern, registering individual files with **Azure Data Catalog** probably does not make sense.</span></span> <span data-ttu-id="4b413-118">Au lieu de cela, enregistrez les répertoires qui représentent les jeux de données significatifs pour les utilisateurs travaillant avec ces données.</span><span class="sxs-lookup"><span data-stu-id="4b413-118">Instead, register the directories that represent the data sets that be meaningful to the users working with the data.</span></span>

## <a name="reference-data-files"></a><span data-ttu-id="4b413-119">Référence de fichiers de données</span><span class="sxs-lookup"><span data-stu-id="4b413-119">Reference data files</span></span>
<span data-ttu-id="4b413-120">Un modèle complémentaire consiste à stocker des jeux de données de référence sous forme de fichiers individuels.</span><span class="sxs-lookup"><span data-stu-id="4b413-120">A complementary pattern is to store reference data sets as individual files.</span></span> <span data-ttu-id="4b413-121">Ces ensembles de données peuvent être considérés comme le côté « émergé » des données volumineuses et sont souvent comparables aux dimensions d’un modèle de données analytiques.</span><span class="sxs-lookup"><span data-stu-id="4b413-121">These data sets may be thought of as the 'small' side of big data, and are often similar to dimensions in an analytical data model.</span></span> <span data-ttu-id="4b413-122">Les fichiers de données de référence contiennent des enregistrements utilisés pour offrir un contexte aux lots de fichiers de données stockées ailleurs dans le magasin de données volumineuses.</span><span class="sxs-lookup"><span data-stu-id="4b413-122">Reference data files contain records that are used to provide context for the bulk of the data files stored elsewhere in the big data store.</span></span>

<span data-ttu-id="4b413-123">Voici quelques exemples de ce modèle :</span><span class="sxs-lookup"><span data-stu-id="4b413-123">An example of this pattern might be:</span></span>

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

<span data-ttu-id="4b413-124">Lorsqu’un analyste ou un spécialiste des données travaille avec les données contenues dans des structures de répertoire plus grandes, les données présentes dans ces fichiers de référence fournissent des informations plus détaillées pour les entités référencées uniquement par nom ou ID du jeu de données plus grand.</span><span class="sxs-lookup"><span data-stu-id="4b413-124">When an analyst or data scientist is working with the data contained in the larger directory structures, the data in these reference files can be used to provide more detailed information for entities that are referred to only by name or ID in the larger data set.</span></span>

<span data-ttu-id="4b413-125">Dans ce modèle, il est judicieux d’enregistrer les fichiers de données de référence avec **Azure Data Catalog**.</span><span class="sxs-lookup"><span data-stu-id="4b413-125">In this pattern, it makes sense to register the individual reference data files with **Azure Data Catalog**.</span></span> <span data-ttu-id="4b413-126">Chaque fichier représente un jeu de données, et chacun d’eux peut être annoté et découvert individuellement.</span><span class="sxs-lookup"><span data-stu-id="4b413-126">Each file represents a data set, and each one can be annotated and discovered individually.</span></span>

## <a name="alternate-patterns"></a><span data-ttu-id="4b413-127">Modèles alternatifs</span><span class="sxs-lookup"><span data-stu-id="4b413-127">Alternate patterns</span></span>
<span data-ttu-id="4b413-128">Les modèles décrits dans la section précédente représentent deux organisations possibles de magasins de données Big Data, mais chaque implémentation est différente.</span><span class="sxs-lookup"><span data-stu-id="4b413-128">The patterns described in the preceding section are just two possible ways a big data store may be organized, but each implementation is different.</span></span> <span data-ttu-id="4b413-129">Quelle que soit la façon dont vos sources de données sont structurées, lors de l’enregistrement des sources de données Big Data auprès de **Azure Data Catalog**, concentrez-vous sur l’enregistrement des fichiers et des répertoires qui représentent les jeux de données qui ont une valeur pour les autres au sein de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="4b413-129">Regardless of how your data sources are structured, when registering big data sources with **Azure Data Catalog**, focus on registering the files and directories that represent the data sets that are of value to others within your organization.</span></span> <span data-ttu-id="4b413-130">L’inscription de tous les fichiers et répertoires peut encombrer le catalogue, ce qui complique les opérations de recherche pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="4b413-130">Registering all files and directories can clutter the catalog, making it harder for users to find what they need.</span></span>

## <a name="summary"></a><span data-ttu-id="4b413-131">Résumé</span><span class="sxs-lookup"><span data-stu-id="4b413-131">Summary</span></span>
<span data-ttu-id="4b413-132">L’inscription des sources de données auprès de **Azure Data Catalog** les facilite leur détection et leur compréhension.</span><span class="sxs-lookup"><span data-stu-id="4b413-132">Registering data sources with **Azure Data Catalog** makes them easier to discover and understand.</span></span> <span data-ttu-id="4b413-133">En enregistrant et en annotant les fichiers et les répertoires de données volumineuses qui représentent les jeux de données logiques, vous pouvez aider les utilisateurs à trouver et à utiliser les sources de données volumineuses dont ils ont besoin.</span><span class="sxs-lookup"><span data-stu-id="4b413-133">By registering and annotating the big data files and directories that represent logical data sets, you can help users find and use the big data sources they need.</span></span>
