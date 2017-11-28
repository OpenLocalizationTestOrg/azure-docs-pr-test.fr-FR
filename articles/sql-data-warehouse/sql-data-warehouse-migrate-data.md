---
title: "Migration de vos données vers SQL Data Warehouse | Microsoft Docs"
description: "Conseils relatifs à la migration de vos données vers Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: d78f954a-f54c-4aa4-9040-919bc6414887
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/29/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: dbdf1696cd169aa7e5e23f116027a1170347f4ea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-your-data"></a><span data-ttu-id="3e1fc-103">Migration de vos données</span><span class="sxs-lookup"><span data-stu-id="3e1fc-103">Migrate Your Data</span></span>
<span data-ttu-id="3e1fc-104">Les données peuvent être déplacées à partir de différentes sources dans SQL Data Warehouse avec divers outils.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span></span>  <span data-ttu-id="3e1fc-105">Les solutions ADF Copy, SSIS et bcp peuvent toutes être utilisées à cette fin.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-105">ADF Copy, SSIS, and bcp can all be used to achieve this goal.</span></span> <span data-ttu-id="3e1fc-106">Toutefois, à mesure de l’augmentation du volume des données, vous avez tout intérêt à réfléchir à un moyen de diviser le processus de migration des données en étapes.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-106">However, as the amount of data increases you should think about breaking down the data migration process into steps.</span></span> <span data-ttu-id="3e1fc-107">Ce faisant, vous vous donnez les moyens d’optimiser chacune des phases en matière de performance et de résilience afin de garantir une migration sans heurts des données.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-107">This affords you the opportunity to optimize each step both for performance and for resilience to ensure a smooth data migration.</span></span>

<span data-ttu-id="3e1fc-108">Cet article s’intéresse tout d’abord aux scénarios simples de migration d’ADF Copy, de SSIS et de bcp.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-108">This article first discusses the simple migration scenarios of ADF Copy, SSIS, and bcp.</span></span> <span data-ttu-id="3e1fc-109">Nous évoquons ensuite de manière plus approfondie les différents moyens d’optimiser la migration.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-109">It then look a little deeper into how the migration can be optimized.</span></span>

## <a name="azure-data-factory-adf-copy"></a><span data-ttu-id="3e1fc-110">Azure Data Factory (ADF) Copy</span><span class="sxs-lookup"><span data-stu-id="3e1fc-110">Azure Data Factory (ADF) copy</span></span>
<span data-ttu-id="3e1fc-111">[ADF Copy][ADF Copy] fait partie intégrante d’[Azure Data Factory][Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="3e1fc-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span></span> <span data-ttu-id="3e1fc-112">ADF Copy peut être utilisée pour exporter vos données vers des fichiers plats hébergés sur un espace de stockage local, vers des fichiers plats distants conservés dans un espace de stockage d’objets Blob Microsoft Azure ou directement vers SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-112">You can use ADF Copy to export your data to flat files residing on local storage, to remote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span></span>

<span data-ttu-id="3e1fc-113">Si vos données sont hébergées initialement dans des fichiers plats, il vous faudra dans un premier temps les transférer vers un espace de stockage d’objets Blob Azure avant de lancer le chargement dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-113">If your data starts in flat files, then you will first need to transfer it to Azure storage blob before initiating a load it into SQL Data Warehouse.</span></span> <span data-ttu-id="3e1fc-114">Une fois que les données sont transférées dans Stockage Blob Azure, vous pouvez utiliser de nouveau [ADF Copy][ADF Copy] pour les charger dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-114">Once the data is transferred into Azure blob storage you can choose to use [ADF Copy][ADF Copy] again to push the data into SQL Data Warehouse.</span></span>

<span data-ttu-id="3e1fc-115">PolyBase propose également une option hautes performances dédiée au chargement des données.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-115">PolyBase also provides a high-performance option for loading the data.</span></span> <span data-ttu-id="3e1fc-116">Si vous optez pour cette solution, cela ne signifie pas que vous utilisez deux outils au lieu d’un.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-116">However, that does mean using two tools instead of one.</span></span> <span data-ttu-id="3e1fc-117">Si vous avez besoin de performances optimales, utilisez PolyBase.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-117">If you need the best performance then use PolyBase.</span></span> <span data-ttu-id="3e1fc-118">Si vous souhaitez profiter d’une expérience valorisant un outil unique (et que le volume de données n’est pas considérable), tournez-vous vers ADF.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-118">If you want a single tool experience (and the data is not massive) then ADF is your answer.</span></span>


> 
> 

<span data-ttu-id="3e1fc-119">Consultez l’article suivant afin de découvrir de formidables [exemples ADF][ADF samples].</span><span class="sxs-lookup"><span data-stu-id="3e1fc-119">Head over to the following article for some great [ADF samples][ADF samples].</span></span>

## <a name="integration-services"></a><span data-ttu-id="3e1fc-120">Integration Services</span><span class="sxs-lookup"><span data-stu-id="3e1fc-120">Integration Services</span></span>
<span data-ttu-id="3e1fc-121">Integration Services (SSIS) est un outil puissant et flexible d’extraction, de transformation et de chargement (ETL, Extract Transform and Load) qui prend en charge des workflows complexes, la transformation des données et diverses options de chargement des données.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span></span> <span data-ttu-id="3e1fc-122">Utilisez SSIS afin de procéder à un transfert simple de données vers Microsoft Azure, ou dans le cadre d’une migration plus importante.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-122">Use SSIS to simply transfer data to Azure or as part of a broader migration.</span></span>

> [!NOTE]
> <span data-ttu-id="3e1fc-123">SSIS peut exporter des données vers le format UTF-8 sans laisser de marque d’ordre d’octet dans le fichier.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-123">SSIS can export to UTF-8 without the byte order mark in the file.</span></span> <span data-ttu-id="3e1fc-124">Pour procéder à la configuration adéquate, vous devez tout d’abord utiliser le composant de colonne dérivée afin de convertir les données caractères dans le flux de données pour utiliser la page de code UTF-8 65001.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-124">To configure this you must first use the derived column component to convert the character data in the data flow to use the 65001 UTF-8 code page.</span></span> <span data-ttu-id="3e1fc-125">Une fois que les colonnes ont été converties, procédez à l’écriture des données sur l’adaptateur de destination du fichier plat en vérifiant que la page de code 65001 a été sélectionnée pour le fichier.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-125">Once the columns have been converted, write the data to the flat file destination adapter ensuring that 65001 has also been selected as the code page for the file.</span></span>
> 
> 

<span data-ttu-id="3e1fc-126">La solution SSIS se connecte à SQL Data Warehouse de la manière dont elle se connecte à un déploiement SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-126">SSIS connects to SQL Data Warehouse just as it would connect to a SQL Server deployment.</span></span> <span data-ttu-id="3e1fc-127">Cependant, vos connexions doivent utiliser un gestionnaire de connexions ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-127">However, your connections will need to be using an ADO.NET connection manager.</span></span> <span data-ttu-id="3e1fc-128">Vous devez également vous assurer de configurer le paramètre « Utiliser l’insertion de bloc lorsqu’elle est disponible » afin d’optimiser le débit.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-128">You should also take care to configure the "Use bulk insert when available" setting to maximize throughput.</span></span> <span data-ttu-id="3e1fc-129">Pour en savoir plus sur cette propriété, consultez l’article [Adaptateur de destination ADO.NET][ADO.NET destination adapter].</span><span class="sxs-lookup"><span data-stu-id="3e1fc-129">Please refer to the [ADO.NET destination adapter][ADO.NET destination adapter] article to learn more about this property</span></span>

> [!NOTE]
> <span data-ttu-id="3e1fc-130">La connexion à Microsoft Azure SQL Data Warehouse à l’aide d’OLEDB n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-130">Connecting to Azure SQL Data Warehouse by using OLEDB is not supported.</span></span>
> 
> 

<span data-ttu-id="3e1fc-131">Par ailleurs, il est toujours possible qu’un package soit mis en échec en raison d’une limitation ou de problèmes réseau.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-131">In addition, there is always the possibility that a package might fail due to throttling or network issues.</span></span> <span data-ttu-id="3e1fc-132">Concevez les packages afin qu’ils puissent être repris à partir du point de défaillance, sans avoir à réitérer les tâches accomplies avant la mise en échec.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-132">Design packages so they can be resumed at the point of failure, without redoing work that completed before the failure.</span></span>

<span data-ttu-id="3e1fc-133">Pour en savoir plus, consultez la [documentation relative à SSIS][SSIS documentation].</span><span class="sxs-lookup"><span data-stu-id="3e1fc-133">For more information consult the [SSIS documentation][SSIS documentation].</span></span>

## <a name="bcp"></a><span data-ttu-id="3e1fc-134">bcp</span><span class="sxs-lookup"><span data-stu-id="3e1fc-134">bcp</span></span>
<span data-ttu-id="3e1fc-135">bcp est un utilitaire de ligne de commande qui est conçu pour l’importation et l’exportation des données des fichiers plats.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-135">bcp is a command-line utility that is designed for flat file data import and export.</span></span> <span data-ttu-id="3e1fc-136">Des activités de transformation peuvent avoir lieu durant l’exportation des données.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-136">Some transformation can take place during data export.</span></span> <span data-ttu-id="3e1fc-137">Pour effectuer des transformations simples, utilisez une requête afin de sélectionner et de transformer les données.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-137">To perform simple transformations use a query to select and transform the data.</span></span> <span data-ttu-id="3e1fc-138">Une fois qu’ils sont exportés, les fichiers plats peuvent être directement chargés dans la base de données cible SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-138">Once exported, the flat files can then be loaded directly into the target the SQL Data Warehouse database.</span></span>

> [!NOTE]
> <span data-ttu-id="3e1fc-139">Il est souvent judicieux d’encapsuler les transformations utilisées durant l’exportation des données dans une vue sur le système source.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-139">It is often a good idea to encapsulate the transformations used during data export in a view on the source system.</span></span> <span data-ttu-id="3e1fc-140">Cela vous garantit que la logique est conservée et que le processus est répétable.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-140">This ensures that the logic is retained and the process is repeatable.</span></span>
> 
> 

<span data-ttu-id="3e1fc-141">Les avantages de bcp sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="3e1fc-141">Advantages of bcp are:</span></span>

* <span data-ttu-id="3e1fc-142">Simplicité.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-142">Simplicity.</span></span> <span data-ttu-id="3e1fc-143">Les commandes bcp sont simples à concevoir et à exécuter.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-143">bcp commands are simple to build and execute</span></span>
* <span data-ttu-id="3e1fc-144">Processus de chargement redémarrable.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-144">Re-startable load process.</span></span> <span data-ttu-id="3e1fc-145">Une fois que les données ont été exportées, le chargement peut être exécuté un nombre illimité de fois.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-145">Once exported the load can be executed any number of times</span></span>

<span data-ttu-id="3e1fc-146">Les limites de l’utilitaire bcp sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="3e1fc-146">Limitations of bcp are:</span></span>

* <span data-ttu-id="3e1fc-147">bcp fonctionne avec des fichiers plats en format tableau uniquement.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-147">bcp works with tabulated flat files only.</span></span> <span data-ttu-id="3e1fc-148">Cette solution ne prend pas en charge les fichiers aux formats xml ou JSON.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-148">It does not work with files such as xml or JSON</span></span>
* <span data-ttu-id="3e1fc-149">Les fonctionnalités de transformation de données sont utilisables durant la phase d’exportation uniquement, et sont simples par nature.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-149">Data transformation capabilities are limited to the export stage only and are simple in nature</span></span>
* <span data-ttu-id="3e1fc-150">L’utilitaire bcp n’a pas été modifié afin d’offrir une fiabilité acceptable durant le chargement des données sur Internet.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-150">bcp has not been adapted to be robust when loading data over the internet.</span></span> <span data-ttu-id="3e1fc-151">Toute instabilité du réseau peut provoquer une erreur de chargement.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-151">Any network instability may cause a load error.</span></span>
* <span data-ttu-id="3e1fc-152">bcp s’appuie sur le schéma initialement présent dans la base de données cible avant le chargement.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-152">bcp relies on the schema being present in the target database prior to the load</span></span>

<span data-ttu-id="3e1fc-153">Pour en savoir plus, consultez la rubrique [Utilisation de bcp pour charger des données dans SQL Data Warehouse][Use bcp to load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="3e1fc-153">For more information, see [Use bcp to load data into SQL Data Warehouse][Use bcp to load data into SQL Data Warehouse].</span></span>

## <a name="optimizing-data-migration"></a><span data-ttu-id="3e1fc-154">Optimisation de la migration des données</span><span class="sxs-lookup"><span data-stu-id="3e1fc-154">Optimizing data migration</span></span>
<span data-ttu-id="3e1fc-155">Un processus de migration des données SQLDW peut être efficacement divisé en trois étapes distinctes :</span><span class="sxs-lookup"><span data-stu-id="3e1fc-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span></span>

1. <span data-ttu-id="3e1fc-156">Exportation des données sources</span><span class="sxs-lookup"><span data-stu-id="3e1fc-156">Export of source data</span></span>
2. <span data-ttu-id="3e1fc-157">Transfert des données vers Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3e1fc-157">Transfer of data to Azure</span></span>
3. <span data-ttu-id="3e1fc-158">Chargement dans la base de données SQLDW</span><span class="sxs-lookup"><span data-stu-id="3e1fc-158">Load into the target SQLDW database</span></span>

<span data-ttu-id="3e1fc-159">Chaque étape peut être optimisée de manière isolée afin de concevoir un processus fiable, redémarrable et résistant de migration qui génère de hautes performances à chaque phase.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-159">Each step can be individually optimized to create a robust, re-startable and resilient migration process that maximizes performance at each step.</span></span>

## <a name="optimizing-data-load"></a><span data-ttu-id="3e1fc-160">Optimisation du chargement des données</span><span class="sxs-lookup"><span data-stu-id="3e1fc-160">Optimizing data load</span></span>
<span data-ttu-id="3e1fc-161">Si nous prenons le processus dans l’ordre inverse, nous constatons que PolyBase procure le moyen le plus rapide de charger des données.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-161">Looking at these in reverse order for a moment; the fastest way to load data is via PolyBase.</span></span> <span data-ttu-id="3e1fc-162">L’optimisation nécessaire à un processus de chargement PolyBase ajoutant des phases préalables à l’exécution des étapes précédentes, vous avez tout intérêt à comprendre ces phases supplémentaires en amont.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-162">Optimizing for a PolyBase load process places prerequisites on the preceding steps so it's best to understand this upfront.</span></span> <span data-ttu-id="3e1fc-163">Les voici :</span><span class="sxs-lookup"><span data-stu-id="3e1fc-163">They are:</span></span>

1. <span data-ttu-id="3e1fc-164">Encodage des fichiers de données</span><span class="sxs-lookup"><span data-stu-id="3e1fc-164">Encoding of data files</span></span>
2. <span data-ttu-id="3e1fc-165">Formatage des fichiers de données</span><span class="sxs-lookup"><span data-stu-id="3e1fc-165">Format of data files</span></span>
3. <span data-ttu-id="3e1fc-166">Définition de l’emplacement des fichiers de données</span><span class="sxs-lookup"><span data-stu-id="3e1fc-166">Location of data files</span></span>

### <a name="encoding"></a><span data-ttu-id="3e1fc-167">Encodage</span><span class="sxs-lookup"><span data-stu-id="3e1fc-167">Encoding</span></span>
<span data-ttu-id="3e1fc-168">PolyBase nécessite d’utiliser des fichiers de données au format UTF-8 ou UTF-16FE.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-168">PolyBase requires data files to be UTF-8 or UTF-16FE.</span></span> 



### <a name="format-of-data-files"></a><span data-ttu-id="3e1fc-169">Formatage des fichiers de données</span><span class="sxs-lookup"><span data-stu-id="3e1fc-169">Format of data files</span></span>
<span data-ttu-id="3e1fc-170">PolyBase requiert un terminateur de ligne fixe \n ou un renvoi à la ligne.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-170">PolyBase mandates a fixed row terminator of \n or newline.</span></span> <span data-ttu-id="3e1fc-171">Vos fichiers de données doivent être conformes à cette directive.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-171">Your data files must conform to this standard.</span></span> <span data-ttu-id="3e1fc-172">Il n’existe aucune restriction relative aux terminateurs de chaînes ou de colonnes.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-172">There aren't any restrictions on string or column terminators.</span></span>

<span data-ttu-id="3e1fc-173">Vous devrez définir chacune des colonnes du fichier en tant que composante de table externe dans PolyBase.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-173">You will have to define every column in the file as part of your external table in PolyBase.</span></span> <span data-ttu-id="3e1fc-174">Vérifiez que l’ensemble des colonnes exportées sont requises et que les types définis sont conformes aux normes requises.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-174">Make sure that all exported columns are required and that the types conform to the required standards.</span></span>

<span data-ttu-id="3e1fc-175">Veuillez vous référer à l’article [Migration de votre schéma] pour en savoir plus sur les types de données pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-175">Please refer back to the [migrate your schema] article for detail on supported data types.</span></span>

### <a name="location-of-data-files"></a><span data-ttu-id="3e1fc-176">Définition de l’emplacement des fichiers de données</span><span class="sxs-lookup"><span data-stu-id="3e1fc-176">Location of data files</span></span>
<span data-ttu-id="3e1fc-177">SQL Data Warehouse utilise PolyBase pour charger des données exclusivement à partir d’objets Blob Microsoft Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-177">SQL Data Warehouse uses PolyBase to load data from Azure Blob Storage exclusively.</span></span> <span data-ttu-id="3e1fc-178">De fait, les données doivent avoir été préalablement transférées dans des objets Blob.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-178">Consequently, the data must have been first transferred into blob storage.</span></span>

## <a name="optimizing-data-transfer"></a><span data-ttu-id="3e1fc-179">Optimisation du transfert des données</span><span class="sxs-lookup"><span data-stu-id="3e1fc-179">Optimizing data transfer</span></span>
<span data-ttu-id="3e1fc-180">Le transfert des données vers Microsoft Azure est l’une des phases les plus lentes de la migration des données.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-180">One of the slowest parts of data migration is the transfer of the data to Azure.</span></span> <span data-ttu-id="3e1fc-181">Cette étape peut être associée à une problématique de bande passante et entraver la progression, en réduisant la fiabilité du réseau.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span></span> <span data-ttu-id="3e1fc-182">Par défaut, la migration des données vers Microsoft Azure s’effectue via Internet. Ainsi, la probabilité d’erreurs de transfert est raisonnablement élevée.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-182">By default migrating data to Azure is over the internet so the chances of transfer errors occurring are reasonably likely.</span></span> <span data-ttu-id="3e1fc-183">Toutefois, ces erreurs peuvent nécessiter le renvoi complet ou partiel des données.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-183">However, these errors may require data to be re-sent either in whole or in part.</span></span>

<span data-ttu-id="3e1fc-184">Fort heureusement, vous disposez de plusieurs options permettant d’améliorer la rapidité et la résilience de ce processus :</span><span class="sxs-lookup"><span data-stu-id="3e1fc-184">Fortunately you have several options to improve the speed and resilience of this process:</span></span>

### <a name="expressrouteexpressroute"></a><span data-ttu-id="3e1fc-185">[ExpressRoute][ExpressRoute]</span><span class="sxs-lookup"><span data-stu-id="3e1fc-185">[ExpressRoute][ExpressRoute]</span></span>
<span data-ttu-id="3e1fc-186">Vous pouvez éventuellement vous tourner vers [ExpressRoute][ExpressRoute] afin d’accélérer la vitesse de transfert.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-186">You may want to consider using [ExpressRoute][ExpressRoute] to speed up the transfer.</span></span> <span data-ttu-id="3e1fc-187">[ExpressRoute][ExpressRoute] vous procure une connexion exclusivement privée avec Azure, pour que la connexion ne passe pas par l’Internet public.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-187">[ExpressRoute][ExpressRoute] provides you with an established private connection to Azure so the connection does not go over the public internet.</span></span> <span data-ttu-id="3e1fc-188">Vous n’êtes aucunement obligé de recourir à cette option.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-188">This is by no means a mandatory step.</span></span> <span data-ttu-id="3e1fc-189">Toutefois, sachez qu’elle améliore le débit de transfert des données à partir d’une installation sur site ou d’un emplacement de colocalisation vers Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-189">However, it will improve throughput when pushing data to Azure from an on-premises or co-location facility.</span></span>

<span data-ttu-id="3e1fc-190">Les avantages procurés par [ExpressRoute][ExpressRoute] sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="3e1fc-190">The benefits of using [ExpressRoute][ExpressRoute] are:</span></span>

1. <span data-ttu-id="3e1fc-191">Accroissement de la fiabilité</span><span class="sxs-lookup"><span data-stu-id="3e1fc-191">Increased reliability</span></span>
2. <span data-ttu-id="3e1fc-192">Augmentation de la vitesse du réseau</span><span class="sxs-lookup"><span data-stu-id="3e1fc-192">Faster network speed</span></span>
3. <span data-ttu-id="3e1fc-193">Réduction de la latence du réseau</span><span class="sxs-lookup"><span data-stu-id="3e1fc-193">Lower network latency</span></span>
4. <span data-ttu-id="3e1fc-194">Amélioration de la sécurité du réseau</span><span class="sxs-lookup"><span data-stu-id="3e1fc-194">higher network security</span></span>

<span data-ttu-id="3e1fc-195">[ExpressRoute][ExpressRoute] profite à de nombreux scénarios, pas uniquement à la migration.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just the migration.</span></span>

<span data-ttu-id="3e1fc-196">Vous êtes intéressé ?</span><span class="sxs-lookup"><span data-stu-id="3e1fc-196">Interested?</span></span> <span data-ttu-id="3e1fc-197">Pour plus d’informations et pour consulter la tarification, accédez à la [documentation ExpressRoute][ExpressRoute documentation].</span><span class="sxs-lookup"><span data-stu-id="3e1fc-197">For more information and pricing please visit the [ExpressRoute documentation][ExpressRoute documentation].</span></span>

### <a name="azure-import-and-export-service"></a><span data-ttu-id="3e1fc-198">Azure Import Export Service</span><span class="sxs-lookup"><span data-stu-id="3e1fc-198">Azure Import and Export Service</span></span>
<span data-ttu-id="3e1fc-199">Azure Import and Export Service est un processus de transfert de données conçu pour les transferts importants (plusieurs Go) à massifs (plusieurs To) de données dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-199">The Azure Import and Export Service is a data transfer process designed for large (GB++) to massive (TB++) transfers of data into Azure.</span></span> <span data-ttu-id="3e1fc-200">Il implique l’écriture de vos données sur des disques et leur transfert vers un centre de données Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-200">It involves writing your data to disks and shipping them to an Azure data center.</span></span> <span data-ttu-id="3e1fc-201">Ensuite, le contenu des disques est chargé dans des objets Blob Microsoft Storage en votre nom.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-201">The disk contents will then be loaded into Azure Storage Blobs on your behalf.</span></span>

<span data-ttu-id="3e1fc-202">Voici une vue de niveau supérieur du processus d’importation-exportation :</span><span class="sxs-lookup"><span data-stu-id="3e1fc-202">A high-level view of the import export process is as follows:</span></span>

1. <span data-ttu-id="3e1fc-203">Configuration d’un conteneur d’objets Blob Microsoft Storage dédié à la réception des données</span><span class="sxs-lookup"><span data-stu-id="3e1fc-203">Configure an Azure Blob Storage container to receive the data</span></span>
2. <span data-ttu-id="3e1fc-204">Exportation de vos données vers le stockage local</span><span class="sxs-lookup"><span data-stu-id="3e1fc-204">Export your data to local storage</span></span>
3. <span data-ttu-id="3e1fc-205">Copie de vos données sur des disques durs 3,5 pouces SATA II/III à l’aide de [l’outil Azure Import/Export]</span><span class="sxs-lookup"><span data-stu-id="3e1fc-205">Copy the data to 3.5 inch SATA II/III hard disk drives using the [Azure Import/Export Tool]</span></span>
4. <span data-ttu-id="3e1fc-206">Création d’une tâche d’importation à l’aide du service Azure Import Export, avec les fichiers journaux produits par [l’outil Azure Import/Export]</span><span class="sxs-lookup"><span data-stu-id="3e1fc-206">Create an Import Job using the Azure Import and Export Service providing the journal files produced by the [Azure Import/Export Tool]</span></span>
5. <span data-ttu-id="3e1fc-207">Livraison des disques à votre centre de données Microsoft Azure désigné</span><span class="sxs-lookup"><span data-stu-id="3e1fc-207">Ship the disks your nominated Azure data center</span></span>
6. <span data-ttu-id="3e1fc-208">Transfert de vos données vers votre conteneur d’objets Blob Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3e1fc-208">Your data is transferred to your Azure Blob Storage container</span></span>
7. <span data-ttu-id="3e1fc-209">Chargement de vos données dans SQLDW à l’aide de PolyBase</span><span class="sxs-lookup"><span data-stu-id="3e1fc-209">Load the data into SQLDW using PolyBase</span></span>

### <a name="azcopyazcopy-utility"></a><span data-ttu-id="3e1fc-210">Utilitaire [AZCopy][AZCopy]</span><span class="sxs-lookup"><span data-stu-id="3e1fc-210">[AZCopy][AZCopy] utility</span></span>
<span data-ttu-id="3e1fc-211">L’utilitaire [AZCopy][AZCopy] est l’outil idéal pour transférer vos données dans des objets blob de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-211">The [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span></span> <span data-ttu-id="3e1fc-212">Il est conçu pour des transferts de données modestes (plusieurs Mo) à très importants (plusieurs Go).</span><span class="sxs-lookup"><span data-stu-id="3e1fc-212">It is designed for small (MB++) to very large (GB++) data transfers.</span></span> <span data-ttu-id="3e1fc-213">[AZCopy] a également été conçu pour fournir un débit efficace et robuste lors du transfert de données vers Azure. Par conséquent, cette solution convient parfaitement au transfert de données.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-213">[AZCopy] has also been designed to provide good resilient throughput when transferring data to Azure and so is a great choice for the data transfer step.</span></span> <span data-ttu-id="3e1fc-214">Une fois que le transfert a été effectué, vous pouvez charger les données dans SQL Data Warehouse à l’aide de PolyBase.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-214">Once transferred you can load the data using PolyBase into SQL Data Warehouse.</span></span> <span data-ttu-id="3e1fc-215">Vous pouvez également intégrer AZCopy dans vos packages SSIS, en appliquant une tâche d’exécution du processus.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span></span>

<span data-ttu-id="3e1fc-216">Il vous faudra dans un premier temps télécharger et installer AZCopy.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-216">To use AZCopy you will first need to download and install it.</span></span> <span data-ttu-id="3e1fc-217">Une [version de production][production version] et une [préversion][preview version] sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-217">There is a [production version][production version] and a [preview version][preview version] available.</span></span>

<span data-ttu-id="3e1fc-218">Pour charger un fichier à partir de votre système de fichier, vous devrez recourir à une commande de ce type :</span><span class="sxs-lookup"><span data-stu-id="3e1fc-218">To upload a file from your file system you will need a command like the one below:</span></span>

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="3e1fc-219">Voici les étapes possibles d’un processus de niveau supérieur :</span><span class="sxs-lookup"><span data-stu-id="3e1fc-219">A high-level process summary could be:</span></span>

1. <span data-ttu-id="3e1fc-220">Configuration d’un conteneur de stockage d’objets Blob Microsoft Azure dédié à la réception des données</span><span class="sxs-lookup"><span data-stu-id="3e1fc-220">Configure an Azure storage blob container to receive the data</span></span>
2. <span data-ttu-id="3e1fc-221">Exportation de vos données vers le stockage local</span><span class="sxs-lookup"><span data-stu-id="3e1fc-221">Export your data to local storage</span></span>
3. <span data-ttu-id="3e1fc-222">Traitement de vos données à l’aide d’AZCopy dans le contenu de stockage d’objets Blob Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3e1fc-222">AZCopy your data in the Azure Blob Storage container</span></span>
4. <span data-ttu-id="3e1fc-223">Charger les données dans SQL Data Warehouse à l’aide de PolyBase</span><span class="sxs-lookup"><span data-stu-id="3e1fc-223">Load the data into SQL Data Warehouse using PolyBase</span></span>

<span data-ttu-id="3e1fc-224">Documentation complète disponible : [AZCopy][AZCopy].</span><span class="sxs-lookup"><span data-stu-id="3e1fc-224">Full documentation available: [AZCopy][AZCopy].</span></span>

## <a name="optimizing-data-export"></a><span data-ttu-id="3e1fc-225">Optimisation de l’exportation des données</span><span class="sxs-lookup"><span data-stu-id="3e1fc-225">Optimizing data export</span></span>
<span data-ttu-id="3e1fc-226">En plus d’assurer la conformité de l’exportation avec les exigences associées à PolyBase, vous pouvez également chercher à optimiser l’exportation des données afin d’améliorer davantage le processus.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-226">In addition to ensuring that the export conforms to the requirements laid out by PolyBase you can also seek to optimize the export of the data to improve the process further.</span></span>



### <a name="data-compression"></a><span data-ttu-id="3e1fc-227">Compression des données</span><span class="sxs-lookup"><span data-stu-id="3e1fc-227">Data compression</span></span>
<span data-ttu-id="3e1fc-228">PolyBase peut lire les données compressées au format gzip.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-228">PolyBase can read gzip compressed data.</span></span> <span data-ttu-id="3e1fc-229">Si vous n’êtes pas en mesure de compresser vos données au format gzip, il vous faudra réduire le volume de données transmis sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-229">If you are able to compress your data to gzip files then you will minimize the amount of data being pushed over the network.</span></span>

### <a name="multiple-files"></a><span data-ttu-id="3e1fc-230">Fichiers multiples</span><span class="sxs-lookup"><span data-stu-id="3e1fc-230">Multiple files</span></span>
<span data-ttu-id="3e1fc-231">La fragmentation de gros tableaux en plusieurs fichiers vous permet d’accélérer la vitesse d’exportation, mais facilite également le redémarrage des transferts et améliore la gestion globale des données transférées vers le stockage d’objets Blob Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-231">Breaking up large tables into several files not only helps to improve export speed, it also helps with transfer re-startability, and the overall manageability of the data once in the Azure blob storage.</span></span> <span data-ttu-id="3e1fc-232">PolyBase permet notamment de lire l’ensemble des fichiers stockés dans un dossier et de les traiter en tant que tableau unique.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-232">One of the many nice features of PolyBase is that it will read all the files inside a folder and treat it as one table.</span></span> <span data-ttu-id="3e1fc-233">Par conséquent, il est avisé de conserver les fichiers associés à un tableau dans un dossier séparé.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-233">It is therefore a good idea to isolate the files for each table into its own folder.</span></span>

<span data-ttu-id="3e1fc-234">PolyBase prend également en charge une fonction appelée « balayage de dossier récursif ».</span><span class="sxs-lookup"><span data-stu-id="3e1fc-234">PolyBase also supports a feature known as "recursive folder traversal".</span></span> <span data-ttu-id="3e1fc-235">Vous pouvez la mettre à profit pour optimiser l’organisation de vos données exportées et ainsi améliorer la gestion de vos données.</span><span class="sxs-lookup"><span data-stu-id="3e1fc-235">You can use this feature to further enhance the organization of your exported data to improve your data management.</span></span>

<span data-ttu-id="3e1fc-236">Pour en savoir plus sur le chargement des données à l’aide de PolyBase, consultez la section [Utilisation de PolyBase pour charger des données dans SQL Data Warehouse][Use PolyBase to load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="3e1fc-236">To learn more about loading data with PolyBase, see [Use PolyBase to load data into SQL Data Warehouse][Use PolyBase to load data into SQL Data Warehouse].</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e1fc-237">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3e1fc-237">Next steps</span></span>
<span data-ttu-id="3e1fc-238">Pour en savoir plus sur la migration, consultez la section [Migration de votre solution vers SQL Data Warehouse][Migrate your solution to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="3e1fc-238">For more about migration, see [Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse].</span></span>
<span data-ttu-id="3e1fc-239">Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].</span><span class="sxs-lookup"><span data-stu-id="3e1fc-239">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution to SQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp to load data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase to load data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
