---
title: "sources de données de profil aaaHow tooData"
description: "Tooarticle de la mise en surbrillance comment les données de niveau table ou colonne tooinclude profils lors de l’inscription des sources de données dans Azure Data Catalog et comment les données toouse profils toounderstand des sources de données."
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
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a><span data-ttu-id="8bad0-103">Profilage de données dans des sources de données</span><span class="sxs-lookup"><span data-stu-id="8bad0-103">Data profile data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="8bad0-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="8bad0-104">Introduction</span></span>
<span data-ttu-id="8bad0-105">**Microsoft Azure Data Catalog** est un service cloud entièrement géré qui sert de système d'inscription et de détection des sources de données d'entreprise.</span><span class="sxs-lookup"><span data-stu-id="8bad0-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="8bad0-106">En d’autres termes, **Azure Data Catalog** est tout sur aidant les utilisateurs à découvrir, comprendre et utiliser des sources de données, et aider les organisations tooget plus la valeur à partir de leurs données.</span><span class="sxs-lookup"><span data-stu-id="8bad0-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data.</span></span> <span data-ttu-id="8bad0-107">Quand une source de données est enregistrée avec **Azure Data Catalog**, ses métadonnées sont copiée et est indexée par le service de hello, mais un récit hello ne se termine pas il.</span><span class="sxs-lookup"><span data-stu-id="8bad0-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by hello service, but hello story doesn’t end there.</span></span>

<span data-ttu-id="8bad0-108">Hello **profilage des données** fonctionnalité de **Azure Data Catalog** examine hello des données à partir de sources de données pris en charge dans votre catalogue et collecte des statistiques et les informations relatives à ces données.</span><span class="sxs-lookup"><span data-stu-id="8bad0-108">hello **Data Profiling** feature of **Azure Data Catalog** examines hello data from supported data sources in your catalog and collects statistics and information about that data.</span></span> <span data-ttu-id="8bad0-109">Il est facile tooinclude un profil de vos ressources de données.</span><span class="sxs-lookup"><span data-stu-id="8bad0-109">It's easy tooinclude a profile of your data assets.</span></span> <span data-ttu-id="8bad0-110">Lorsque vous inscrivez une ressource de données, choisissez **inclure un profil de données** dans l’outil de l’enregistrement de source de données hello.</span><span class="sxs-lookup"><span data-stu-id="8bad0-110">When you register a data asset, choose **Include Data Profile** in hello data source registration tool.</span></span>

## <a name="what-is-data-profiling"></a><span data-ttu-id="8bad0-111">Qu’est-ce que le profilage de données ?</span><span class="sxs-lookup"><span data-stu-id="8bad0-111">What is Data Profiling</span></span>
<span data-ttu-id="8bad0-112">Profilage des données examine les données de hello dans la source de données hello en cours d’inscription et collecte des statistiques et les informations relatives à ces données.</span><span class="sxs-lookup"><span data-stu-id="8bad0-112">Data profiling examines hello data in hello data source being registered, and collects statistics and information about that data.</span></span> <span data-ttu-id="8bad0-113">Pendant la découverte de source de données, ces statistiques peuvent vous aider à déterminer adéquation hello de hello données toosolve leur problème professionnel.</span><span class="sxs-lookup"><span data-stu-id="8bad0-113">During data source discovery, these statistics can help you determine hello suitability of hello data toosolve their business problem.</span></span>

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

<span data-ttu-id="8bad0-114">Hello sources de données suivantes prennent en charge le profilage des données :</span><span class="sxs-lookup"><span data-stu-id="8bad0-114">hello following data sources support data profiling:</span></span>

* <span data-ttu-id="8bad0-115">Vues et tables SQL Server (y compris la base de données SQL Azure et Azure SQL Data Warehouse)</span><span class="sxs-lookup"><span data-stu-id="8bad0-115">SQL Server (including Azure SQL DB and Azure SQL Data Warehouse) tables and views</span></span>
* <span data-ttu-id="8bad0-116">Tables et vues Oracle</span><span class="sxs-lookup"><span data-stu-id="8bad0-116">Oracle tables and views</span></span>
* <span data-ttu-id="8bad0-117">Tables et vues Teradata</span><span class="sxs-lookup"><span data-stu-id="8bad0-117">Teradata tables and views</span></span>
* <span data-ttu-id="8bad0-118">Tables Hive</span><span class="sxs-lookup"><span data-stu-id="8bad0-118">Hive tables</span></span>

<span data-ttu-id="8bad0-119">L’inclusion de profils de données lors de l’inscription de ressources de données permet à l’utilisateur de répondre à certaines questions sur les sources de données, notamment :</span><span class="sxs-lookup"><span data-stu-id="8bad0-119">Including data profiles when registering data assets helps users answer questions about data sources, including:</span></span>

* <span data-ttu-id="8bad0-120">Il peut être utilisé toosolve mon problème d’entreprise ?</span><span class="sxs-lookup"><span data-stu-id="8bad0-120">Can it be used toosolve my business problem?</span></span>
* <span data-ttu-id="8bad0-121">Les données de salutation est conforme tooparticular normes ou modèles ?</span><span class="sxs-lookup"><span data-stu-id="8bad0-121">Does hello data conform tooparticular standards or patterns?</span></span>
* <span data-ttu-id="8bad0-122">Quelles sont les anomalies hello hello de source de données ?</span><span class="sxs-lookup"><span data-stu-id="8bad0-122">What are some of hello anomalies of hello data source?</span></span>
* <span data-ttu-id="8bad0-123">Quelles sont les difficultés que je risque de rencontrer en intégrant ces données dans mon application ?</span><span class="sxs-lookup"><span data-stu-id="8bad0-123">What are possible challenges of integrating this data into my application?</span></span>

> [!NOTE]
> <span data-ttu-id="8bad0-124">Vous pouvez également ajouter la documentation tooan asset toodescribe comment les données peuvent être intégrées dans une application.</span><span class="sxs-lookup"><span data-stu-id="8bad0-124">You can also add documentation tooan asset toodescribe how data could be integrated into an application.</span></span> <span data-ttu-id="8bad0-125">Consultez [comment toodocument des sources de données](data-catalog-how-to-documentation.md).</span><span class="sxs-lookup"><span data-stu-id="8bad0-125">See [How toodocument data sources](data-catalog-how-to-documentation.md).</span></span>
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a><span data-ttu-id="8bad0-126">Comment tooinclude une profil des données lorsque l’inscription d’une source de données</span><span class="sxs-lookup"><span data-stu-id="8bad0-126">How tooinclude a data profile when registering a data source</span></span>
<span data-ttu-id="8bad0-127">Il est facile tooinclude un profil de votre source de données.</span><span class="sxs-lookup"><span data-stu-id="8bad0-127">It's easy tooinclude a profile of your data source.</span></span> <span data-ttu-id="8bad0-128">Lorsque vous enregistrez une source de données, Bonjour **toobe objets inscrits** Panneau de configuration de l’enregistrement de source de données hello d’outils, choisissez **inclure un profil de données**.</span><span class="sxs-lookup"><span data-stu-id="8bad0-128">When you register a data source, in hello **Objects toobe registered** panel of hello data source registration tool, choose **Include Data Profile**.</span></span>

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

<span data-ttu-id="8bad0-129">toolearn savoir plus sur les sources de données tooregister, voir [comment les sources de données tooregister](data-catalog-how-to-register.md) et [prise en main Azure Data Catalog](data-catalog-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8bad0-129">toolearn more about how tooregister data sources, see [How tooregister data sources](data-catalog-how-to-register.md) and [Get started with Azure Data Catalog](data-catalog-get-started.md).</span></span>

## <a name="filtering-on-data-assets-that-include-data-profiles"></a><span data-ttu-id="8bad0-130">Filtrage sur des ressources de données comprenant des profils de données</span><span class="sxs-lookup"><span data-stu-id="8bad0-130">Filtering on data assets that include data profiles</span></span>
<span data-ttu-id="8bad0-131">toodiscover les ressources de données qui incluent un profil des données, vous pouvez inclure `has:tableDataProfiles` ou `has:columnsDataProfiles` comme l’un de vos termes de recherche.</span><span class="sxs-lookup"><span data-stu-id="8bad0-131">toodiscover data assets that include a data profile, you can include `has:tableDataProfiles` or `has:columnsDataProfiles` as one of your search terms.</span></span>

> [!NOTE]
> <span data-ttu-id="8bad0-132">En sélectionnant **inclure un profil de données** dans les données de salutation outil d’inscription source inclut table et les informations de profil au niveau de la colonne.</span><span class="sxs-lookup"><span data-stu-id="8bad0-132">Selecting **Include Data Profile** in hello data source registration tool includes both table and column-level profile information.</span></span> <span data-ttu-id="8bad0-133">Toutefois, hello API de catalogue de données permet de données actifs toobe inscrit avec un seul jeu d’informations de profil inclus.</span><span class="sxs-lookup"><span data-stu-id="8bad0-133">However, hello Data Catalog API allows data assets toobe registered with only one set of profile information included.</span></span>
>
>

## <a name="viewing-data-profile-information"></a><span data-ttu-id="8bad0-134">Affichage des informations de profil de données</span><span class="sxs-lookup"><span data-stu-id="8bad0-134">Viewing data profile information</span></span>
<span data-ttu-id="8bad0-135">Une fois que vous trouvez une source de données adapté à un profil, vous pouvez afficher les détails du profil de données hello.</span><span class="sxs-lookup"><span data-stu-id="8bad0-135">Once you find a suitable data source with a profile, you can view hello data profile details.</span></span> <span data-ttu-id="8bad0-136">les données de salutation tooview de profil, sélectionnez une ressource de données et choisissez **profil des données** dans la fenêtre du portail hello catalogue de données.</span><span class="sxs-lookup"><span data-stu-id="8bad0-136">tooview hello data profile, select a data asset and choose **Data Profile** in hello Data Catalog portal window.</span></span>

![](media/data-catalog-data-profile/data-catalog-view.png)

<span data-ttu-id="8bad0-137">Un profil de données dans **Azure Data Catalog** affiche les informations de profil au niveau de la table et au niveau de la colonne :</span><span class="sxs-lookup"><span data-stu-id="8bad0-137">A data profile in **Azure Data Catalog** shows table and column profile information including:</span></span>

### <a name="object-data-profile"></a><span data-ttu-id="8bad0-138">Profil de données au niveau objet</span><span class="sxs-lookup"><span data-stu-id="8bad0-138">Object data profile</span></span>
* <span data-ttu-id="8bad0-139">Nombre de lignes</span><span class="sxs-lookup"><span data-stu-id="8bad0-139">Number of rows</span></span>
* <span data-ttu-id="8bad0-140">Taille de la table</span><span class="sxs-lookup"><span data-stu-id="8bad0-140">Table size</span></span>
* <span data-ttu-id="8bad0-141">Lorsque les objets hello a été modifié</span><span class="sxs-lookup"><span data-stu-id="8bad0-141">When hello object was last updated</span></span>

### <a name="column-data-profile"></a><span data-ttu-id="8bad0-142">Profil de données au niveau colonne</span><span class="sxs-lookup"><span data-stu-id="8bad0-142">Column data profile</span></span>
* <span data-ttu-id="8bad0-143">Type de données de colonne</span><span class="sxs-lookup"><span data-stu-id="8bad0-143">Column data type</span></span>
* <span data-ttu-id="8bad0-144">Nombre de valeurs distinctes</span><span class="sxs-lookup"><span data-stu-id="8bad0-144">Number of distinct values</span></span>
* <span data-ttu-id="8bad0-145">Nombre de lignes contenant des valeurs NULL</span><span class="sxs-lookup"><span data-stu-id="8bad0-145">Number of rows with NULL values</span></span>
* <span data-ttu-id="8bad0-146">Valeurs minimale, maximale, moyenne et d’écart type des colonnes</span><span class="sxs-lookup"><span data-stu-id="8bad0-146">Minimum, maximum, average, and standard deviation for column values</span></span>

## <a name="summary"></a><span data-ttu-id="8bad0-147">Résumé</span><span class="sxs-lookup"><span data-stu-id="8bad0-147">Summary</span></span>
<span data-ttu-id="8bad0-148">Fournit des statistiques de profilage des données et informations inscrit toohelp actifs de données vous déterminez la capacité d’adaptation hello hello données toosolve de problèmes d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="8bad0-148">Data profiling provides statistics and information about registered data assets toohelp you determine hello suitability of hello data toosolve business problems.</span></span> <span data-ttu-id="8bad0-149">Outre l’annotation et la documentation de sources de données, les profils de données peuvent permettre aux utilisateurs de mieux comprendre vos données.</span><span class="sxs-lookup"><span data-stu-id="8bad0-149">Along with annotating, and documenting data sources, data profiles can give users a deeper understanding of your data.</span></span>

## <a name="see-also"></a><span data-ttu-id="8bad0-150">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="8bad0-150">See Also</span></span>
* [<span data-ttu-id="8bad0-151">Comment tooregister des sources de données</span><span class="sxs-lookup"><span data-stu-id="8bad0-151">How tooregister data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="8bad0-152">Prise en main d’Azure Data Catalog</span><span class="sxs-lookup"><span data-stu-id="8bad0-152">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)
