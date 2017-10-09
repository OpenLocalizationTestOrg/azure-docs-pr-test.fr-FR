---
title: "toowork aaaHow des sources de données de « données volumineuses » | Documents Microsoft"
description: "Modèles de mise en surbrillance tooarticle de procédure pour l’utilisation d’Azure Data Catalog des sources de données de « données volumineuses », y compris le stockage d’objets Blob Azure, Azure Data Lake et Hadoop HDFS."
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
ms.openlocfilehash: e478f71f26744975a7d7e1784b74bf50b424cf65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowork-with-big-data-sources-in-azure-data-catalog"></a><span data-ttu-id="f6333-103">Comment toowork avec les données sources dans Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="f6333-103">How toowork with big data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="f6333-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="f6333-104">Introduction</span></span>
<span data-ttu-id="f6333-105">**Microsoft Azure Data Catalog** est un service cloud entièrement géré qui sert de système d'inscription et de détection des sources de données d'entreprise.</span><span class="sxs-lookup"><span data-stu-id="f6333-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="f6333-106">Il concerne toutes les personnes découvrir, comprendre et utiliser des sources de données et de contribuer aux organisations tooget plus de valeur à partir de leurs sources de données existantes, y compris les données volumineuses.</span><span class="sxs-lookup"><span data-stu-id="f6333-106">It is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data sources, including big data.</span></span>

<span data-ttu-id="f6333-107">**Azure Data Catalog** prend en charge hello d’enregistrement des objets BLOB de stockage d’objets BLOB Azure et des répertoires ainsi que des fichiers de Hadoop HDFS et des répertoires.</span><span class="sxs-lookup"><span data-stu-id="f6333-107">**Azure Data Catalog** supports hello registration of Azure Blog Storage blobs and directories as well as Hadoop HDFS files and directories.</span></span> <span data-ttu-id="f6333-108">nature de semi-structurées Hello de ces sources de données offre une grande souplesse.</span><span class="sxs-lookup"><span data-stu-id="f6333-108">hello semi-structured nature of these data sources provides great flexibility.</span></span> <span data-ttu-id="f6333-109">Toutefois, tooget hello le meilleur parti de l’inscription avec **Azure Data Catalog**, les utilisateurs doivent envisager la façon dont les sources de données hello sont organisés.</span><span class="sxs-lookup"><span data-stu-id="f6333-109">However, tooget hello most value from registering them with **Azure Data Catalog**, users must consider how hello data sources are organized.</span></span>

## <a name="directories-as-logical-data-sets"></a><span data-ttu-id="f6333-110">Répertoires sous forme de jeux de données logiques</span><span class="sxs-lookup"><span data-stu-id="f6333-110">Directories as logical data sets</span></span>
<span data-ttu-id="f6333-111">Il est courant pour organiser les sources de données volumineuses tootreat répertoires en tant que jeux de données logique.</span><span class="sxs-lookup"><span data-stu-id="f6333-111">A common pattern for organizing big data sources is tootreat directories as logical data sets.</span></span> <span data-ttu-id="f6333-112">Répertoires de niveau supérieur sont toodefine utilisé un jeu de données, tandis que les sous-dossiers définissent des partitions et des fichiers hello qu’ils contiennent stockent des données de hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="f6333-112">Top-level directories are used toodefine a data set, while subfolders define partitions, and hello files they contain store hello data itself.</span></span>

<span data-ttu-id="f6333-113">Voici quelques exemples de ce modèle :</span><span class="sxs-lookup"><span data-stu-id="f6333-113">An example of this pattern might be:</span></span>

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

<span data-ttu-id="f6333-114">Dans cet exemple, vehicle_maintenance_events et location_tracking_events représentent les jeux de données logiques.</span><span class="sxs-lookup"><span data-stu-id="f6333-114">In this example, vehicle_maintenance_events and location_tracking_events represent logical data sets.</span></span> <span data-ttu-id="f6333-115">Chacun de ces dossiers contient des fichiers de données organisés par année et par mois en sous-dossiers.</span><span class="sxs-lookup"><span data-stu-id="f6333-115">Each of these folders contains data files that are organized by year and month into subfolders.</span></span> <span data-ttu-id="f6333-116">Chacun de ces dossiers peut contenir des centaines ou des milliers de fichiers.</span><span class="sxs-lookup"><span data-stu-id="f6333-116">Each of these folders could potentially contain hundreds or thousands of files.</span></span>

<span data-ttu-id="f6333-117">Dans ce modèle, l’enregistrement des fichiers individuels auprès d’ **Azure Data Catalog** ne sert sans doute à rien.</span><span class="sxs-lookup"><span data-stu-id="f6333-117">In this pattern, registering individual files with **Azure Data Catalog** probably does not make sense.</span></span> <span data-ttu-id="f6333-118">Au lieu de cela, inscrivez les répertoires hello qui représentent des jeux de données hello être significatif toohello aux utilisateurs qui travaillent avec des données hello.</span><span class="sxs-lookup"><span data-stu-id="f6333-118">Instead, register hello directories that represent hello data sets that be meaningful toohello users working with hello data.</span></span>

## <a name="reference-data-files"></a><span data-ttu-id="f6333-119">Référence de fichiers de données</span><span class="sxs-lookup"><span data-stu-id="f6333-119">Reference data files</span></span>
<span data-ttu-id="f6333-120">Un modèle complémentaire est jeux de données de référence toostore en tant que fichiers individuels.</span><span class="sxs-lookup"><span data-stu-id="f6333-120">A complementary pattern is toostore reference data sets as individual files.</span></span> <span data-ttu-id="f6333-121">Ces jeux de données peut être considéré comme le côté « small » de hello de données volumineuses et sont souvent toodimensions similaires dans un modèle de données analytiques.</span><span class="sxs-lookup"><span data-stu-id="f6333-121">These data sets may be thought of as hello 'small' side of big data, and are often similar toodimensions in an analytical data model.</span></span> <span data-ttu-id="f6333-122">Les fichiers de données de référence contiennent des enregistrements contexte tooprovide utilisées en bloc de hello hello des fichiers de données stockés ailleurs dans le magasin de données volumineuses hello.</span><span class="sxs-lookup"><span data-stu-id="f6333-122">Reference data files contain records that are used tooprovide context for hello bulk of hello data files stored elsewhere in hello big data store.</span></span>

<span data-ttu-id="f6333-123">Voici quelques exemples de ce modèle :</span><span class="sxs-lookup"><span data-stu-id="f6333-123">An example of this pattern might be:</span></span>

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

<span data-ttu-id="f6333-124">Quand un chercheur analyste ou données collabore avec données hello contenues dans les grandes structures de répertoire hello, données hello dans ces fichiers de référence peuvent être utilisé tooprovide des informations plus détaillées pour les entités qui sont visés tooonly par nom ou ID dans les données plus grandes hello ensemble.</span><span class="sxs-lookup"><span data-stu-id="f6333-124">When an analyst or data scientist is working with hello data contained in hello larger directory structures, hello data in these reference files can be used tooprovide more detailed information for entities that are referred tooonly by name or ID in hello larger data set.</span></span>

<span data-ttu-id="f6333-125">Dans ce modèle, il est logique des fichiers de données de référence de hello tooregister avec **Azure Data Catalog**.</span><span class="sxs-lookup"><span data-stu-id="f6333-125">In this pattern, it makes sense tooregister hello individual reference data files with **Azure Data Catalog**.</span></span> <span data-ttu-id="f6333-126">Chaque fichier représente un jeu de données, et chacun d’eux peut être annoté et découvert individuellement.</span><span class="sxs-lookup"><span data-stu-id="f6333-126">Each file represents a data set, and each one can be annotated and discovered individually.</span></span>

## <a name="alternate-patterns"></a><span data-ttu-id="f6333-127">Modèles alternatifs</span><span class="sxs-lookup"><span data-stu-id="f6333-127">Alternate patterns</span></span>
<span data-ttu-id="f6333-128">Hello modèles décrits dans la précédente section de hello deux méthodes sont possibles qu'un magasin de données volumineuses peut être organisé, mais chaque implémentation est différente.</span><span class="sxs-lookup"><span data-stu-id="f6333-128">hello patterns described in hello preceding section are just two possible ways a big data store may be organized, but each implementation is different.</span></span> <span data-ttu-id="f6333-129">Quelle que soit la façon dont vos sources de données sont structurées, lors de l’inscription des sources de données volumineuses avec **Azure Data Catalog**, se concentrer sur l’enregistrement des fichiers de hello et de répertoires qui représentent des jeux de données hello de tooothers valeur au sein de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="f6333-129">Regardless of how your data sources are structured, when registering big data sources with **Azure Data Catalog**, focus on registering hello files and directories that represent hello data sets that are of value tooothers within your organization.</span></span> <span data-ttu-id="f6333-130">L’inscription de tous les fichiers et répertoires permettre encombrer catalogue hello, rend plus difficile pour les utilisateurs toofind dont ils ont besoin.</span><span class="sxs-lookup"><span data-stu-id="f6333-130">Registering all files and directories can clutter hello catalog, making it harder for users toofind what they need.</span></span>

## <a name="summary"></a><span data-ttu-id="f6333-131">Résumé</span><span class="sxs-lookup"><span data-stu-id="f6333-131">Summary</span></span>
<span data-ttu-id="f6333-132">L’inscription des sources de données avec **Azure Data Catalog** rend plus facile toodiscover et à comprendre.</span><span class="sxs-lookup"><span data-stu-id="f6333-132">Registering data sources with **Azure Data Catalog** makes them easier toodiscover and understand.</span></span> <span data-ttu-id="f6333-133">En enregistrant et annoter les fichiers de données volumineuses hello et de répertoires qui représentent des jeux de données logiques, les utilisateurs peuvent aider à trouver et utiliser des sources de données volumineuses hello que dont ils ont besoin.</span><span class="sxs-lookup"><span data-stu-id="f6333-133">By registering and annotating hello big data files and directories that represent logical data sets, you can help users find and use hello big data sources they need.</span></span>
