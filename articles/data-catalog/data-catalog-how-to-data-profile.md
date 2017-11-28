---
title: "Comment profiler des données dans des sources de données"
description: "Article de procédure mettant en avant l’inclusion de profils de données au niveau des tables et des colonnes lors de l’inscription des sources de données dans Azure Data Catalog et expliquant comment utiliser des profils de données pour comprendre les sources de données."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 8f4174f0ed74706b8275c8b1f0a62753f2834fa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="data-profile-data-sources"></a><span data-ttu-id="d243e-103">Profilage de données dans des sources de données</span><span class="sxs-lookup"><span data-stu-id="d243e-103">Data profile data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="d243e-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="d243e-104">Introduction</span></span>
<span data-ttu-id="d243e-105">**Microsoft Azure Data Catalog** est un service cloud entièrement géré qui sert de système d'inscription et de détection des sources de données d'entreprise.</span><span class="sxs-lookup"><span data-stu-id="d243e-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="d243e-106">En d'autres termes, **Microsoft Azure Data Catalog** vise essentiellement à aider les utilisateurs à détecter, comprendre et utiliser des sources de données et permet aux organisations de mieux exploiter leurs données.</span><span class="sxs-lookup"><span data-stu-id="d243e-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations to get more value from their existing data.</span></span> <span data-ttu-id="d243e-107">Lorsqu’une source de données est inscrite dans **Azure Data Catalog**, ses métadonnées sont copiées et indexées par le service. Mais ce n’est pas tout.</span><span class="sxs-lookup"><span data-stu-id="d243e-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by the service, but the story doesn’t end there.</span></span>

<span data-ttu-id="d243e-108">La fonctionnalité **Profilage des données** dans **Azure Data Catalog** examine les données à partir des sources de données prises en charge dans votre catalogue et collecte des statistiques et des informations relatives à ces données.</span><span class="sxs-lookup"><span data-stu-id="d243e-108">The **Data Profiling** feature of **Azure Data Catalog** examines the data from supported data sources in your catalog and collects statistics and information about that data.</span></span> <span data-ttu-id="d243e-109">Vous pouvez inclure très facilement un profil de vos ressources de données.</span><span class="sxs-lookup"><span data-stu-id="d243e-109">It's easy to include a profile of your data assets.</span></span> <span data-ttu-id="d243e-110">Lorsque vous enregistrez une ressource de données, sélectionnez **Inclure le profil de données** dans l’outil d’inscription de sources de données.</span><span class="sxs-lookup"><span data-stu-id="d243e-110">When you register a data asset, choose **Include Data Profile** in the data source registration tool.</span></span>

## <a name="what-is-data-profiling"></a><span data-ttu-id="d243e-111">Qu’est-ce que le profilage de données ?</span><span class="sxs-lookup"><span data-stu-id="d243e-111">What is Data Profiling</span></span>
<span data-ttu-id="d243e-112">Le profilage des données consiste à examiner les données dans la source de données en cours d’inscription et à collecter des statistiques et des informations sur ces données.</span><span class="sxs-lookup"><span data-stu-id="d243e-112">Data profiling examines the data in the data source being registered, and collects statistics and information about that data.</span></span> <span data-ttu-id="d243e-113">Lors de la découverte de sources de données, ces statistiques peuvent vous aider à déterminer dans quelle mesure les données peuvent vous aider à résoudre vos problème métier.</span><span class="sxs-lookup"><span data-stu-id="d243e-113">During data source discovery, these statistics can help you determine the suitability of the data to solve their business problem.</span></span>

<!-- In [How to discover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How to include a data profile when registering a data source](#howto). -->

<span data-ttu-id="d243e-114">Les sources de données suivantes prennent en charge le profilage des données :</span><span class="sxs-lookup"><span data-stu-id="d243e-114">The following data sources support data profiling:</span></span>

* <span data-ttu-id="d243e-115">Vues et tables SQL Server (y compris la base de données SQL Azure et Azure SQL Data Warehouse)</span><span class="sxs-lookup"><span data-stu-id="d243e-115">SQL Server (including Azure SQL DB and Azure SQL Data Warehouse) tables and views</span></span>
* <span data-ttu-id="d243e-116">Tables et vues Oracle</span><span class="sxs-lookup"><span data-stu-id="d243e-116">Oracle tables and views</span></span>
* <span data-ttu-id="d243e-117">Tables et vues Teradata</span><span class="sxs-lookup"><span data-stu-id="d243e-117">Teradata tables and views</span></span>
* <span data-ttu-id="d243e-118">Tables Hive</span><span class="sxs-lookup"><span data-stu-id="d243e-118">Hive tables</span></span>

<span data-ttu-id="d243e-119">L’inclusion de profils de données lors de l’inscription de ressources de données permet à l’utilisateur de répondre à certaines questions sur les sources de données, notamment :</span><span class="sxs-lookup"><span data-stu-id="d243e-119">Including data profiles when registering data assets helps users answer questions about data sources, including:</span></span>

* <span data-ttu-id="d243e-120">Ces données peuvent-elles m’aider à résoudre mon problème métier ?</span><span class="sxs-lookup"><span data-stu-id="d243e-120">Can it be used to solve my business problem?</span></span>
* <span data-ttu-id="d243e-121">Les données sont-elles conformes à des normes ou modèles spécifiques ?</span><span class="sxs-lookup"><span data-stu-id="d243e-121">Does the data conform to particular standards or patterns?</span></span>
* <span data-ttu-id="d243e-122">La source de données comporte-t-elle des anomalies et, si oui, lesquelles ?</span><span class="sxs-lookup"><span data-stu-id="d243e-122">What are some of the anomalies of the data source?</span></span>
* <span data-ttu-id="d243e-123">Quelles sont les difficultés que je risque de rencontrer en intégrant ces données dans mon application ?</span><span class="sxs-lookup"><span data-stu-id="d243e-123">What are possible challenges of integrating this data into my application?</span></span>

> [!NOTE]
> <span data-ttu-id="d243e-124">Vous pouvez également ajouter de la documentation à une ressource pour décrire dans quelle mesure les données peuvent être intégrées à une application.</span><span class="sxs-lookup"><span data-stu-id="d243e-124">You can also add documentation to an asset to describe how data could be integrated into an application.</span></span> <span data-ttu-id="d243e-125">Voir [Comment documenter des sources de données](data-catalog-how-to-documentation.md).</span><span class="sxs-lookup"><span data-stu-id="d243e-125">See [How to document data sources](data-catalog-how-to-documentation.md).</span></span>
>
>

<a name="howto"/>

## <a name="how-to-include-a-data-profile-when-registering-a-data-source"></a><span data-ttu-id="d243e-126">Comment inclure un profil de données lors de l’inscription d’une source de données</span><span class="sxs-lookup"><span data-stu-id="d243e-126">How to include a data profile when registering a data source</span></span>
<span data-ttu-id="d243e-127">Vous pouvez inclure très facilement un profil de votre source de données.</span><span class="sxs-lookup"><span data-stu-id="d243e-127">It's easy to include a profile of your data source.</span></span> <span data-ttu-id="d243e-128">Lorsque vous procédez à l’inscription d’une source de données dans le panneau **Objets à inscrire** de l’outil d’inscription de sources de données, sélectionnez l’option **Inclure le profil de données**.</span><span class="sxs-lookup"><span data-stu-id="d243e-128">When you register a data source, in the **Objects to be registered** panel of the data source registration tool, choose **Include Data Profile**.</span></span>

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

<span data-ttu-id="d243e-129">Pour en savoir plus sur l’inscription des sources de données, consultez les articles [Inscription de sources de données](data-catalog-how-to-register.md) et [Prise en main d’Azure Data Catalog](data-catalog-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d243e-129">To learn more about how to register data sources, see [How to register data sources](data-catalog-how-to-register.md) and [Get started with Azure Data Catalog](data-catalog-get-started.md).</span></span>

## <a name="filtering-on-data-assets-that-include-data-profiles"></a><span data-ttu-id="d243e-130">Filtrage sur des ressources de données comprenant des profils de données</span><span class="sxs-lookup"><span data-stu-id="d243e-130">Filtering on data assets that include data profiles</span></span>
<span data-ttu-id="d243e-131">Pour découvrir des ressources de données qui incluent un profil de données, vous pouvez inclure l’élément `has:tableDataProfiles` ou `has:columnsDataProfiles` dans l’un de vos termes de recherche.</span><span class="sxs-lookup"><span data-stu-id="d243e-131">To discover data assets that include a data profile, you can include `has:tableDataProfiles` or `has:columnsDataProfiles` as one of your search terms.</span></span>

> [!NOTE]
> <span data-ttu-id="d243e-132">La sélection de l’option **Inclure le profil de données** dans l’outil d’enregistrement de la source de données inclut les informations de profil au niveau de la colonne et de la table.</span><span class="sxs-lookup"><span data-stu-id="d243e-132">Selecting **Include Data Profile** in the data source registration tool includes both table and column-level profile information.</span></span> <span data-ttu-id="d243e-133">Toutefois, l’API Data Catalog autorise l’enregistrement des ressources de données avec un seul jeu d’informations de profil.</span><span class="sxs-lookup"><span data-stu-id="d243e-133">However, the Data Catalog API allows data assets to be registered with only one set of profile information included.</span></span>
>
>

## <a name="viewing-data-profile-information"></a><span data-ttu-id="d243e-134">Affichage des informations de profil de données</span><span class="sxs-lookup"><span data-stu-id="d243e-134">Viewing data profile information</span></span>
<span data-ttu-id="d243e-135">Dès lors que vous obtenez une source de données appropriée associée à un profil, vous pouvez afficher les détails du profil de données.</span><span class="sxs-lookup"><span data-stu-id="d243e-135">Once you find a suitable data source with a profile, you can view the data profile details.</span></span> <span data-ttu-id="d243e-136">Pour afficher le profil de données, sélectionnez une ressource de données et choisissez **Profil de données** dans la fenêtre du portail Data Catalog.</span><span class="sxs-lookup"><span data-stu-id="d243e-136">To view the data profile, select a data asset and choose **Data Profile** in the Data Catalog portal window.</span></span>

![](media/data-catalog-data-profile/data-catalog-view.png)

<span data-ttu-id="d243e-137">Un profil de données dans **Azure Data Catalog** affiche les informations de profil au niveau de la table et au niveau de la colonne :</span><span class="sxs-lookup"><span data-stu-id="d243e-137">A data profile in **Azure Data Catalog** shows table and column profile information including:</span></span>

### <a name="object-data-profile"></a><span data-ttu-id="d243e-138">Profil de données au niveau objet</span><span class="sxs-lookup"><span data-stu-id="d243e-138">Object data profile</span></span>
* <span data-ttu-id="d243e-139">Nombre de lignes</span><span class="sxs-lookup"><span data-stu-id="d243e-139">Number of rows</span></span>
* <span data-ttu-id="d243e-140">Taille de la table</span><span class="sxs-lookup"><span data-stu-id="d243e-140">Table size</span></span>
* <span data-ttu-id="d243e-141">Date de dernière mise à jour de l’objet</span><span class="sxs-lookup"><span data-stu-id="d243e-141">When the object was last updated</span></span>

### <a name="column-data-profile"></a><span data-ttu-id="d243e-142">Profil de données au niveau colonne</span><span class="sxs-lookup"><span data-stu-id="d243e-142">Column data profile</span></span>
* <span data-ttu-id="d243e-143">Type de données de colonne</span><span class="sxs-lookup"><span data-stu-id="d243e-143">Column data type</span></span>
* <span data-ttu-id="d243e-144">Nombre de valeurs distinctes</span><span class="sxs-lookup"><span data-stu-id="d243e-144">Number of distinct values</span></span>
* <span data-ttu-id="d243e-145">Nombre de lignes contenant des valeurs NULL</span><span class="sxs-lookup"><span data-stu-id="d243e-145">Number of rows with NULL values</span></span>
* <span data-ttu-id="d243e-146">Valeurs minimale, maximale, moyenne et d’écart type des colonnes</span><span class="sxs-lookup"><span data-stu-id="d243e-146">Minimum, maximum, average, and standard deviation for column values</span></span>

## <a name="summary"></a><span data-ttu-id="d243e-147">Résumé</span><span class="sxs-lookup"><span data-stu-id="d243e-147">Summary</span></span>
<span data-ttu-id="d243e-148">Le profilage des données fournit des statistiques et des informations sur les ressources de données inscrites afin de vous aider à déterminer en quoi les données peuvent vous aider à résoudre vos problèmes métier.</span><span class="sxs-lookup"><span data-stu-id="d243e-148">Data profiling provides statistics and information about registered data assets to help you determine the suitability of the data to solve business problems.</span></span> <span data-ttu-id="d243e-149">Outre l’annotation et la documentation de sources de données, les profils de données peuvent permettre aux utilisateurs de mieux comprendre vos données.</span><span class="sxs-lookup"><span data-stu-id="d243e-149">Along with annotating, and documenting data sources, data profiles can give users a deeper understanding of your data.</span></span>

## <a name="see-also"></a><span data-ttu-id="d243e-150">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d243e-150">See Also</span></span>
* [<span data-ttu-id="d243e-151">Inscription de sources de données</span><span class="sxs-lookup"><span data-stu-id="d243e-151">How to register data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="d243e-152">Prise en main d’Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="d243e-152">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)
