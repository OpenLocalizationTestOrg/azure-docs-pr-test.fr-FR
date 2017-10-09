---
title: "aaaMigrate votre tooSQL de données Data Warehouse | Documents Microsoft"
description: "Conseils pour migrer votre tooAzure de données SQL Data Warehouse pour développer des solutions."
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
ms.openlocfilehash: fe4c6b7e82094c59c45e06be6da225fee1b707ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data"></a><span data-ttu-id="08ea1-103">Migration de vos données</span><span class="sxs-lookup"><span data-stu-id="08ea1-103">Migrate Your Data</span></span>
<span data-ttu-id="08ea1-104">Les données peuvent être déplacées à partir de différentes sources dans SQL Data Warehouse avec divers outils.</span><span class="sxs-lookup"><span data-stu-id="08ea1-104">Data can be moved from different sources into your SQL Data Warehouse with a variety tools.</span></span>  <span data-ttu-id="08ea1-105">Copie de la définition d’application SSIS et bcp peuvent tous être utilisé tooachieve cet objectif.</span><span class="sxs-lookup"><span data-stu-id="08ea1-105">ADF Copy, SSIS, and bcp can all be used tooachieve this goal.</span></span> <span data-ttu-id="08ea1-106">Toutefois, comme la quantité hello des données augmente, vous devez considérer sur la décomposition des processus de migration de données hello en étapes.</span><span class="sxs-lookup"><span data-stu-id="08ea1-106">However, as hello amount of data increases you should think about breaking down hello data migration process into steps.</span></span> <span data-ttu-id="08ea1-107">Cela vous offre hello opportunité toooptimize chaque étape aussi bien pour les performances et résilience tooensure une migration régulier des données.</span><span class="sxs-lookup"><span data-stu-id="08ea1-107">This affords you hello opportunity toooptimize each step both for performance and for resilience tooensure a smooth data migration.</span></span>

<span data-ttu-id="08ea1-108">Cet article explique tout d’abord les scénarios de migration simple hello de copie de la définition d’application, SSIS et bcp.</span><span class="sxs-lookup"><span data-stu-id="08ea1-108">This article first discusses hello simple migration scenarios of ADF Copy, SSIS, and bcp.</span></span> <span data-ttu-id="08ea1-109">Il rechercher un peu plus loin dans la migration de hello peut être optimisée.</span><span class="sxs-lookup"><span data-stu-id="08ea1-109">It then look a little deeper into how hello migration can be optimized.</span></span>

## <a name="azure-data-factory-adf-copy"></a><span data-ttu-id="08ea1-110">Azure Data Factory (ADF) Copy</span><span class="sxs-lookup"><span data-stu-id="08ea1-110">Azure Data Factory (ADF) copy</span></span>
<span data-ttu-id="08ea1-111">[ADF Copy][ADF Copy] fait partie intégrante d’[Azure Data Factory][Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="08ea1-111">[ADF Copy][ADF Copy] is part of [Azure Data Factory][Azure Data Factory].</span></span> <span data-ttu-id="08ea1-112">Vous pouvez utiliser ADF copie tooexport vos fichiers tooflat de données résidant sur le stockage local, les fichiers plats tooremote conservées dans le stockage blob Azure, ou directement dans l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="08ea1-112">You can use ADF Copy tooexport your data tooflat files residing on local storage, tooremote flat files held in Azure blob storage or directly into SQL Data Warehouse.</span></span>

<span data-ttu-id="08ea1-113">Si vos données commencent dans les fichiers plats, vous devez tout d’abord tootransfer il tooAzure objet blob de stockage avant de lancer une charge dans l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="08ea1-113">If your data starts in flat files, then you will first need tootransfer it tooAzure storage blob before initiating a load it into SQL Data Warehouse.</span></span> <span data-ttu-id="08ea1-114">Une fois que les données de salutation sont transférées vers le stockage d’objets blob Azure, vous pouvez choisir toouse [ADF copie] [ ADF Copy] toopush à nouveau les données hello dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="08ea1-114">Once hello data is transferred into Azure blob storage you can choose toouse [ADF Copy][ADF Copy] again toopush hello data into SQL Data Warehouse.</span></span>

<span data-ttu-id="08ea1-115">PolyBase fournit également une option de hautes performances pour le chargement des données de salutation.</span><span class="sxs-lookup"><span data-stu-id="08ea1-115">PolyBase also provides a high-performance option for loading hello data.</span></span> <span data-ttu-id="08ea1-116">Si vous optez pour cette solution, cela ne signifie pas que vous utilisez deux outils au lieu d’un.</span><span class="sxs-lookup"><span data-stu-id="08ea1-116">However, that does mean using two tools instead of one.</span></span> <span data-ttu-id="08ea1-117">Si vous avez besoin des performances optimales hello, utilisez PolyBase.</span><span class="sxs-lookup"><span data-stu-id="08ea1-117">If you need hello best performance then use PolyBase.</span></span> <span data-ttu-id="08ea1-118">Si vous souhaitez une expérience unique outil (et les données de salutation ne sont pas massives) ADF est la solution.</span><span class="sxs-lookup"><span data-stu-id="08ea1-118">If you want a single tool experience (and hello data is not massive) then ADF is your answer.</span></span>


> 
> 

<span data-ttu-id="08ea1-119">Principal sur toohello article à une grande suivant [exemples d’ADF][ADF samples].</span><span class="sxs-lookup"><span data-stu-id="08ea1-119">Head over toohello following article for some great [ADF samples][ADF samples].</span></span>

## <a name="integration-services"></a><span data-ttu-id="08ea1-120">Integration Services</span><span class="sxs-lookup"><span data-stu-id="08ea1-120">Integration Services</span></span>
<span data-ttu-id="08ea1-121">Integration Services (SSIS) est un outil puissant et flexible d’extraction, de transformation et de chargement (ETL, Extract Transform and Load) qui prend en charge des workflows complexes, la transformation des données et diverses options de chargement des données.</span><span class="sxs-lookup"><span data-stu-id="08ea1-121">Integration Services (SSIS) is a powerful and flexible Extract Transform and Load (ETL) tool that supports complex workflows, data transformation, and several data loading options.</span></span> <span data-ttu-id="08ea1-122">Utiliser SSIS toosimply transfert données tooAzure ou dans le cadre d’une migration plus large.</span><span class="sxs-lookup"><span data-stu-id="08ea1-122">Use SSIS toosimply transfer data tooAzure or as part of a broader migration.</span></span>

> [!NOTE]
> <span data-ttu-id="08ea1-123">SSIS peut exporter tooUTF-8 sans marque d’ordre d’octet dans le fichier de hello hello.</span><span class="sxs-lookup"><span data-stu-id="08ea1-123">SSIS can export tooUTF-8 without hello byte order mark in hello file.</span></span> <span data-ttu-id="08ea1-124">tooconfigure cela vous devez d’abord utiliser hello dérivées des données colonne composant tooconvert hello caractère dans hello page de codes données flux toouse hello 65001 UTF-8.</span><span class="sxs-lookup"><span data-stu-id="08ea1-124">tooconfigure this you must first use hello derived column component tooconvert hello character data in hello data flow toouse hello 65001 UTF-8 code page.</span></span> <span data-ttu-id="08ea1-125">Une fois que les colonnes hello ont été convertis, écrivez hello données toohello fichier plat destination adaptateur en vérifiant que 65001 a également été sélectionné en tant que page de code hello pour le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="08ea1-125">Once hello columns have been converted, write hello data toohello flat file destination adapter ensuring that 65001 has also been selected as hello code page for hello file.</span></span>
> 
> 

<span data-ttu-id="08ea1-126">SSIS connecte tooSQL l’entrepôt de données comme il se connecte le déploiement de SQL Server tooa.</span><span class="sxs-lookup"><span data-stu-id="08ea1-126">SSIS connects tooSQL Data Warehouse just as it would connect tooa SQL Server deployment.</span></span> <span data-ttu-id="08ea1-127">Toutefois, vos connexions devrez toobe à l’aide d’un gestionnaire de connexions ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="08ea1-127">However, your connections will need toobe using an ADO.NET connection manager.</span></span> <span data-ttu-id="08ea1-128">Vous devez également prendre soin tooconfigure hello « Utiliser bulk insert lorsqu’il est disponible » débit toomaximize de paramètre.</span><span class="sxs-lookup"><span data-stu-id="08ea1-128">You should also take care tooconfigure hello "Use bulk insert when available" setting toomaximize throughput.</span></span> <span data-ttu-id="08ea1-129">Reportez-vous toohello [adaptateur de destination ADO.NET] [ ADO.NET destination adapter] toolearn article plus d’informations sur cette propriété.</span><span class="sxs-lookup"><span data-stu-id="08ea1-129">Please refer toohello [ADO.NET destination adapter][ADO.NET destination adapter] article toolearn more about this property</span></span>

> [!NOTE]
> <span data-ttu-id="08ea1-130">Connexion tooAzure SQL Data Warehouse à l’aide d’OLE DB n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="08ea1-130">Connecting tooAzure SQL Data Warehouse by using OLEDB is not supported.</span></span>
> 
> 

<span data-ttu-id="08ea1-131">En outre, il est toujours possible de hello qu’un package peut échouer en raison de problèmes réseau ou toothrottling.</span><span class="sxs-lookup"><span data-stu-id="08ea1-131">In addition, there is always hello possibility that a package might fail due toothrottling or network issues.</span></span> <span data-ttu-id="08ea1-132">Conception de packages afin qu’ils peuvent reprendre à hello point de défaillance, sans répétition de travail qui sont terminés avant la défaillance de hello.</span><span class="sxs-lookup"><span data-stu-id="08ea1-132">Design packages so they can be resumed at hello point of failure, without redoing work that completed before hello failure.</span></span>

<span data-ttu-id="08ea1-133">Pour plus d’informations, consultez hello [documentation de SSIS][SSIS documentation].</span><span class="sxs-lookup"><span data-stu-id="08ea1-133">For more information consult hello [SSIS documentation][SSIS documentation].</span></span>

## <a name="bcp"></a><span data-ttu-id="08ea1-134">bcp</span><span class="sxs-lookup"><span data-stu-id="08ea1-134">bcp</span></span>
<span data-ttu-id="08ea1-135">bcp est un utilitaire de ligne de commande qui est conçu pour l’importation et l’exportation des données des fichiers plats.</span><span class="sxs-lookup"><span data-stu-id="08ea1-135">bcp is a command-line utility that is designed for flat file data import and export.</span></span> <span data-ttu-id="08ea1-136">Des activités de transformation peuvent avoir lieu durant l’exportation des données.</span><span class="sxs-lookup"><span data-stu-id="08ea1-136">Some transformation can take place during data export.</span></span> <span data-ttu-id="08ea1-137">transformations de simple tooperform utilisent une requête tooselect et transforment des données de hello.</span><span class="sxs-lookup"><span data-stu-id="08ea1-137">tooperform simple transformations use a query tooselect and transform hello data.</span></span> <span data-ttu-id="08ea1-138">Une fois exporté, les fichiers plats hello peuvent ensuite être chargées directement dans la base de données SQL Data Warehouse hello cible hello.</span><span class="sxs-lookup"><span data-stu-id="08ea1-138">Once exported, hello flat files can then be loaded directly into hello target hello SQL Data Warehouse database.</span></span>

> [!NOTE]
> <span data-ttu-id="08ea1-139">Il est souvent une bonne idée tooencapsulate hello exporter des transformations utilisées au cours des données dans une vue de système de source de hello.</span><span class="sxs-lookup"><span data-stu-id="08ea1-139">It is often a good idea tooencapsulate hello transformations used during data export in a view on hello source system.</span></span> <span data-ttu-id="08ea1-140">Cela garantit que la logique hello est conservée et les processus hello sont répétée.</span><span class="sxs-lookup"><span data-stu-id="08ea1-140">This ensures that hello logic is retained and hello process is repeatable.</span></span>
> 
> 

<span data-ttu-id="08ea1-141">Les avantages de bcp sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="08ea1-141">Advantages of bcp are:</span></span>

* <span data-ttu-id="08ea1-142">Simplicité.</span><span class="sxs-lookup"><span data-stu-id="08ea1-142">Simplicity.</span></span> <span data-ttu-id="08ea1-143">commandes de bcp sont toobuild simple et exécuter</span><span class="sxs-lookup"><span data-stu-id="08ea1-143">bcp commands are simple toobuild and execute</span></span>
* <span data-ttu-id="08ea1-144">Processus de chargement redémarrable.</span><span class="sxs-lookup"><span data-stu-id="08ea1-144">Re-startable load process.</span></span> <span data-ttu-id="08ea1-145">Une fois exporté hello de charge peut être exécutée un nombre de fois</span><span class="sxs-lookup"><span data-stu-id="08ea1-145">Once exported hello load can be executed any number of times</span></span>

<span data-ttu-id="08ea1-146">Les limites de l’utilitaire bcp sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="08ea1-146">Limitations of bcp are:</span></span>

* <span data-ttu-id="08ea1-147">bcp fonctionne avec des fichiers plats en format tableau uniquement.</span><span class="sxs-lookup"><span data-stu-id="08ea1-147">bcp works with tabulated flat files only.</span></span> <span data-ttu-id="08ea1-148">Cette solution ne prend pas en charge les fichiers aux formats xml ou JSON.</span><span class="sxs-lookup"><span data-stu-id="08ea1-148">It does not work with files such as xml or JSON</span></span>
* <span data-ttu-id="08ea1-149">Fonctionnalités de transformation de données sont limitées toohello étape d’exportation uniquement et sont de nature simples</span><span class="sxs-lookup"><span data-stu-id="08ea1-149">Data transformation capabilities are limited toohello export stage only and are simple in nature</span></span>
* <span data-ttu-id="08ea1-150">bcp n’a pas été adapté toobe fiable lorsque le chargement des données sur hello internet.</span><span class="sxs-lookup"><span data-stu-id="08ea1-150">bcp has not been adapted toobe robust when loading data over hello internet.</span></span> <span data-ttu-id="08ea1-151">Toute instabilité du réseau peut provoquer une erreur de chargement.</span><span class="sxs-lookup"><span data-stu-id="08ea1-151">Any network instability may cause a load error.</span></span>
* <span data-ttu-id="08ea1-152">bcp s’appuie sur le schéma hello être présents dans la base de données toohello préalable charger hello cible</span><span class="sxs-lookup"><span data-stu-id="08ea1-152">bcp relies on hello schema being present in hello target database prior toohello load</span></span>

<span data-ttu-id="08ea1-153">Pour plus d’informations, consultez [utiliser des données de tooload bcp dans SQL Data Warehouse][Use bcp tooload data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="08ea1-153">For more information, see [Use bcp tooload data into SQL Data Warehouse][Use bcp tooload data into SQL Data Warehouse].</span></span>

## <a name="optimizing-data-migration"></a><span data-ttu-id="08ea1-154">Optimisation de la migration des données</span><span class="sxs-lookup"><span data-stu-id="08ea1-154">Optimizing data migration</span></span>
<span data-ttu-id="08ea1-155">Un processus de migration des données SQLDW peut être efficacement divisé en trois étapes distinctes :</span><span class="sxs-lookup"><span data-stu-id="08ea1-155">A SQLDW data migration process can be effectively broken down into three discrete steps:</span></span>

1. <span data-ttu-id="08ea1-156">Exportation des données sources</span><span class="sxs-lookup"><span data-stu-id="08ea1-156">Export of source data</span></span>
2. <span data-ttu-id="08ea1-157">Transfert de données tooAzure</span><span class="sxs-lookup"><span data-stu-id="08ea1-157">Transfer of data tooAzure</span></span>
3. <span data-ttu-id="08ea1-158">Charger dans la base de données SQLDW hello cible</span><span class="sxs-lookup"><span data-stu-id="08ea1-158">Load into hello target SQLDW database</span></span>

<span data-ttu-id="08ea1-159">Chaque étape peut être optimisée individuellement toocreate un processus de migration solide, redémarrés et fiable qui optimise les performances à chaque étape.</span><span class="sxs-lookup"><span data-stu-id="08ea1-159">Each step can be individually optimized toocreate a robust, re-startable and resilient migration process that maximizes performance at each step.</span></span>

## <a name="optimizing-data-load"></a><span data-ttu-id="08ea1-160">Optimisation du chargement des données</span><span class="sxs-lookup"><span data-stu-id="08ea1-160">Optimizing data load</span></span>
<span data-ttu-id="08ea1-161">En examinant ces valeurs dans l’ordre inverse pour un instant ; Hello plus rapide des tooload données sont via PolyBase.</span><span class="sxs-lookup"><span data-stu-id="08ea1-161">Looking at these in reverse order for a moment; hello fastest way tooload data is via PolyBase.</span></span> <span data-ttu-id="08ea1-162">Optimisation pour un processus de chargement de PolyBase impose des conditions préalables sur hello étapes précédentes afin qu’il soit meilleures toounderstand cela initial.</span><span class="sxs-lookup"><span data-stu-id="08ea1-162">Optimizing for a PolyBase load process places prerequisites on hello preceding steps so it's best toounderstand this upfront.</span></span> <span data-ttu-id="08ea1-163">Il s'agit de :</span><span class="sxs-lookup"><span data-stu-id="08ea1-163">They are:</span></span>

1. <span data-ttu-id="08ea1-164">Encodage des fichiers de données</span><span class="sxs-lookup"><span data-stu-id="08ea1-164">Encoding of data files</span></span>
2. <span data-ttu-id="08ea1-165">Formatage des fichiers de données</span><span class="sxs-lookup"><span data-stu-id="08ea1-165">Format of data files</span></span>
3. <span data-ttu-id="08ea1-166">Définition de l’emplacement des fichiers de données</span><span class="sxs-lookup"><span data-stu-id="08ea1-166">Location of data files</span></span>

### <a name="encoding"></a><span data-ttu-id="08ea1-167">Encodage</span><span class="sxs-lookup"><span data-stu-id="08ea1-167">Encoding</span></span>
<span data-ttu-id="08ea1-168">PolyBase requiert toobe de fichiers de données UTF-8 ou UTF-16FE.</span><span class="sxs-lookup"><span data-stu-id="08ea1-168">PolyBase requires data files toobe UTF-8 or UTF-16FE.</span></span> 



### <a name="format-of-data-files"></a><span data-ttu-id="08ea1-169">Formatage des fichiers de données</span><span class="sxs-lookup"><span data-stu-id="08ea1-169">Format of data files</span></span>
<span data-ttu-id="08ea1-170">PolyBase requiert un terminateur de ligne fixe \n ou un renvoi à la ligne.</span><span class="sxs-lookup"><span data-stu-id="08ea1-170">PolyBase mandates a fixed row terminator of \n or newline.</span></span> <span data-ttu-id="08ea1-171">Les fichiers de données doivent respecter les toothis standard.</span><span class="sxs-lookup"><span data-stu-id="08ea1-171">Your data files must conform toothis standard.</span></span> <span data-ttu-id="08ea1-172">Il n’existe aucune restriction relative aux terminateurs de chaînes ou de colonnes.</span><span class="sxs-lookup"><span data-stu-id="08ea1-172">There aren't any restrictions on string or column terminators.</span></span>

<span data-ttu-id="08ea1-173">Vous devez toodefine toutes les colonnes dans le fichier de hello en tant que partie de la table externe dans PolyBase.</span><span class="sxs-lookup"><span data-stu-id="08ea1-173">You will have toodefine every column in hello file as part of your external table in PolyBase.</span></span> <span data-ttu-id="08ea1-174">Assurez-vous que toutes les colonnes exportées sont requis et que les types hello sont conformes à des normes toohello requis.</span><span class="sxs-lookup"><span data-stu-id="08ea1-174">Make sure that all exported columns are required and that hello types conform toohello required standards.</span></span>

<span data-ttu-id="08ea1-175">Veuillez référer toohello [migrer votre schéma] article pour plus de détails sur les types de données pris en charge.</span><span class="sxs-lookup"><span data-stu-id="08ea1-175">Please refer back toohello [migrate your schema] article for detail on supported data types.</span></span>

### <a name="location-of-data-files"></a><span data-ttu-id="08ea1-176">Définition de l’emplacement des fichiers de données</span><span class="sxs-lookup"><span data-stu-id="08ea1-176">Location of data files</span></span>
<span data-ttu-id="08ea1-177">SQL Data Warehouse utilise exclusivement les données de tooload PolyBase à partir du stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="08ea1-177">SQL Data Warehouse uses PolyBase tooload data from Azure Blob Storage exclusively.</span></span> <span data-ttu-id="08ea1-178">Par conséquent, les données de salutation doivent avoir été tout d’abord transférées vers le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="08ea1-178">Consequently, hello data must have been first transferred into blob storage.</span></span>

## <a name="optimizing-data-transfer"></a><span data-ttu-id="08ea1-179">Optimisation du transfert des données</span><span class="sxs-lookup"><span data-stu-id="08ea1-179">Optimizing data transfer</span></span>
<span data-ttu-id="08ea1-180">Une des parties de la migration des données les plus lentes hello est transfert hello de hello données tooAzure.</span><span class="sxs-lookup"><span data-stu-id="08ea1-180">One of hello slowest parts of data migration is hello transfer of hello data tooAzure.</span></span> <span data-ttu-id="08ea1-181">Cette étape peut être associée à une problématique de bande passante et entraver la progression, en réduisant la fiabilité du réseau.</span><span class="sxs-lookup"><span data-stu-id="08ea1-181">Not only can network bandwidth be an issue but also network reliability can seriously hamper progress.</span></span> <span data-ttu-id="08ea1-182">Par défaut, migration tooAzure de données est sur internet hello ainsi le risque d’erreurs de transfert en cours sont relativement peu susceptibles de hello.</span><span class="sxs-lookup"><span data-stu-id="08ea1-182">By default migrating data tooAzure is over hello internet so hello chances of transfer errors occurring are reasonably likely.</span></span> <span data-ttu-id="08ea1-183">Toutefois, ces erreurs peuvent nécessiter toobe données envoyée à nouveau en totalité ou en partie.</span><span class="sxs-lookup"><span data-stu-id="08ea1-183">However, these errors may require data toobe re-sent either in whole or in part.</span></span>

<span data-ttu-id="08ea1-184">Heureusement, vous avez plusieurs vitesse de hello tooimprove options et la résilience de ce processus :</span><span class="sxs-lookup"><span data-stu-id="08ea1-184">Fortunately you have several options tooimprove hello speed and resilience of this process:</span></span>

### <a name="expressrouteexpressroute"></a><span data-ttu-id="08ea1-185">[ExpressRoute][ExpressRoute]</span><span class="sxs-lookup"><span data-stu-id="08ea1-185">[ExpressRoute][ExpressRoute]</span></span>
<span data-ttu-id="08ea1-186">Vous souhaiterez peut-être à l’aide de tooconsider [ExpressRoute] [ ExpressRoute] toospeed de transfert de hello.</span><span class="sxs-lookup"><span data-stu-id="08ea1-186">You may want tooconsider using [ExpressRoute][ExpressRoute] toospeed up hello transfer.</span></span> <span data-ttu-id="08ea1-187">[ExpressRoute] [ ExpressRoute] fournit vous avec un tooAzure connexion privée hello afin de la connexion de hello ne passe pas par internet public.</span><span class="sxs-lookup"><span data-stu-id="08ea1-187">[ExpressRoute][ExpressRoute] provides you with an established private connection tooAzure so hello connection does not go over hello public internet.</span></span> <span data-ttu-id="08ea1-188">Vous n’êtes aucunement obligé de recourir à cette option.</span><span class="sxs-lookup"><span data-stu-id="08ea1-188">This is by no means a mandatory step.</span></span> <span data-ttu-id="08ea1-189">Toutefois, cela permettra d’accroître le débit lors de la distribution des données tooAzure à partir d’un site local ou de colocalisation.</span><span class="sxs-lookup"><span data-stu-id="08ea1-189">However, it will improve throughput when pushing data tooAzure from an on-premises or co-location facility.</span></span>

<span data-ttu-id="08ea1-190">avantages de l’utilisation de Hello [ExpressRoute] [ ExpressRoute] sont :</span><span class="sxs-lookup"><span data-stu-id="08ea1-190">hello benefits of using [ExpressRoute][ExpressRoute] are:</span></span>

1. <span data-ttu-id="08ea1-191">Accroissement de la fiabilité</span><span class="sxs-lookup"><span data-stu-id="08ea1-191">Increased reliability</span></span>
2. <span data-ttu-id="08ea1-192">Augmentation de la vitesse du réseau</span><span class="sxs-lookup"><span data-stu-id="08ea1-192">Faster network speed</span></span>
3. <span data-ttu-id="08ea1-193">Réduction de la latence du réseau</span><span class="sxs-lookup"><span data-stu-id="08ea1-193">Lower network latency</span></span>
4. <span data-ttu-id="08ea1-194">Amélioration de la sécurité du réseau</span><span class="sxs-lookup"><span data-stu-id="08ea1-194">higher network security</span></span>

<span data-ttu-id="08ea1-195">[ExpressRoute] [ ExpressRoute] est bénéfique pour plusieurs scénarios ; hello non seulement de migration.</span><span class="sxs-lookup"><span data-stu-id="08ea1-195">[ExpressRoute][ExpressRoute] is beneficial for a number of scenarios; not just hello migration.</span></span>

<span data-ttu-id="08ea1-196">Vous êtes intéressé ?</span><span class="sxs-lookup"><span data-stu-id="08ea1-196">Interested?</span></span> <span data-ttu-id="08ea1-197">Pour plus d’informations et la tarification, visitez hello [documentation d’ExpressRoute][ExpressRoute documentation].</span><span class="sxs-lookup"><span data-stu-id="08ea1-197">For more information and pricing please visit hello [ExpressRoute documentation][ExpressRoute documentation].</span></span>

### <a name="azure-import-and-export-service"></a><span data-ttu-id="08ea1-198">Azure Import Export Service</span><span class="sxs-lookup"><span data-stu-id="08ea1-198">Azure Import and Export Service</span></span>
<span data-ttu-id="08ea1-199">Bonjour Azure Service d’importation et exportation est un processus de transfert de données conçu pour les grandes (en Go ++) toomassive (To ++) les transferts de données dans Azure.</span><span class="sxs-lookup"><span data-stu-id="08ea1-199">hello Azure Import and Export Service is a data transfer process designed for large (GB++) toomassive (TB++) transfers of data into Azure.</span></span> <span data-ttu-id="08ea1-200">Elle implique l’écriture de votre toodisks de données et copie les centre de données Azure tooan.</span><span class="sxs-lookup"><span data-stu-id="08ea1-200">It involves writing your data toodisks and shipping them tooan Azure data center.</span></span> <span data-ttu-id="08ea1-201">contenu du disque Hello est ensuite chargées dans les objets BLOB de stockage Azure à votre place.</span><span class="sxs-lookup"><span data-stu-id="08ea1-201">hello disk contents will then be loaded into Azure Storage Blobs on your behalf.</span></span>

<span data-ttu-id="08ea1-202">Une vue d’ensemble du processus d’exportation importation hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="08ea1-202">A high-level view of hello import export process is as follows:</span></span>

1. <span data-ttu-id="08ea1-203">Configurer un stockage d’objets Blob Azure conteneur tooreceive hello de données</span><span class="sxs-lookup"><span data-stu-id="08ea1-203">Configure an Azure Blob Storage container tooreceive hello data</span></span>
2. <span data-ttu-id="08ea1-204">Exportation de stockage de données toolocal</span><span class="sxs-lookup"><span data-stu-id="08ea1-204">Export your data toolocal storage</span></span>
3. <span data-ttu-id="08ea1-205">Copiez hello données too3.5 pouce SATA II/III lecteurs de disque dur à l’aide de hello [outil d’importation/exportation Azure]</span><span class="sxs-lookup"><span data-stu-id="08ea1-205">Copy hello data too3.5 inch SATA II/III hard disk drives using hello [Azure Import/Export Tool]</span></span>
4. <span data-ttu-id="08ea1-206">Créer un travail d’importation à l’aide de hello Azure Import Service et exportation qui fournit les fichiers de journal hello produits par hello [outil d’importation/exportation Azure]</span><span class="sxs-lookup"><span data-stu-id="08ea1-206">Create an Import Job using hello Azure Import and Export Service providing hello journal files produced by hello [Azure Import/Export Tool]</span></span>
5. <span data-ttu-id="08ea1-207">Expédier les disques de hello votre centre de données Azure désigné</span><span class="sxs-lookup"><span data-stu-id="08ea1-207">Ship hello disks your nominated Azure data center</span></span>
6. <span data-ttu-id="08ea1-208">Vos données sont le conteneur de stockage d’objets Blob Azure tooyour transférés</span><span class="sxs-lookup"><span data-stu-id="08ea1-208">Your data is transferred tooyour Azure Blob Storage container</span></span>
7. <span data-ttu-id="08ea1-209">Charger des données de hello dans SQLDW à l’aide de PolyBase</span><span class="sxs-lookup"><span data-stu-id="08ea1-209">Load hello data into SQLDW using PolyBase</span></span>

### <a name="azcopyazcopy-utility"></a><span data-ttu-id="08ea1-210">Utilitaire [AZCopy][AZCopy]</span><span class="sxs-lookup"><span data-stu-id="08ea1-210">[AZCopy][AZCopy] utility</span></span>
<span data-ttu-id="08ea1-211">Hello [AZCopy][AZCopy] utilitaire est un excellent outil pour obtenir vos données transférées dans les objets BLOB de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="08ea1-211">hello [AZCopy][AZCopy] utility is a great tool for getting your data transferred into Azure Storage Blobs.</span></span> <span data-ttu-id="08ea1-212">Il est conçu pour les petites (Mo ++) toovery volumineux (en Go ++) des transferts de données.</span><span class="sxs-lookup"><span data-stu-id="08ea1-212">It is designed for small (MB++) toovery large (GB++) data transfers.</span></span> <span data-ttu-id="08ea1-213">[AZCopy] a été conçue tooprovide bon résilient débit lorsque le transfert de données tooAzure, de sorte qu’est la solution idéale pour l’étape de transfert de données hello.</span><span class="sxs-lookup"><span data-stu-id="08ea1-213">[AZCopy] has also been designed tooprovide good resilient throughput when transferring data tooAzure and so is a great choice for hello data transfer step.</span></span> <span data-ttu-id="08ea1-214">Une fois transférées, vous pouvez charger des données hello à l’aide de PolyBase dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="08ea1-214">Once transferred you can load hello data using PolyBase into SQL Data Warehouse.</span></span> <span data-ttu-id="08ea1-215">Vous pouvez également intégrer AZCopy dans vos packages SSIS, en appliquant une tâche d’exécution du processus.</span><span class="sxs-lookup"><span data-stu-id="08ea1-215">You can also incorporate AZCopy into your SSIS packages using an "Execute Process" task.</span></span>

<span data-ttu-id="08ea1-216">toouse AZCopy, vous allez tout d’abord besoin toodownload et installez-le.</span><span class="sxs-lookup"><span data-stu-id="08ea1-216">toouse AZCopy you will first need toodownload and install it.</span></span> <span data-ttu-id="08ea1-217">Une [version de production][production version] et une [préversion][preview version] sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="08ea1-217">There is a [production version][production version] and a [preview version][preview version] available.</span></span>

<span data-ttu-id="08ea1-218">tooupload un fichier à partir de votre système de fichiers que vous devez une commande telle que hello une ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="08ea1-218">tooupload a file from your file system you will need a command like hello one below:</span></span>

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="08ea1-219">Voici les étapes possibles d’un processus de niveau supérieur :</span><span class="sxs-lookup"><span data-stu-id="08ea1-219">A high-level process summary could be:</span></span>

1. <span data-ttu-id="08ea1-220">Configurer un stockage Azure blob conteneur tooreceive hello de données</span><span class="sxs-lookup"><span data-stu-id="08ea1-220">Configure an Azure storage blob container tooreceive hello data</span></span>
2. <span data-ttu-id="08ea1-221">Exportation de stockage de données toolocal</span><span class="sxs-lookup"><span data-stu-id="08ea1-221">Export your data toolocal storage</span></span>
3. <span data-ttu-id="08ea1-222">AZCopy vos données dans le conteneur de stockage d’objets Blob Azure hello</span><span class="sxs-lookup"><span data-stu-id="08ea1-222">AZCopy your data in hello Azure Blob Storage container</span></span>
4. <span data-ttu-id="08ea1-223">Charger des données de hello dans l’entrepôt de données SQL à l’aide de PolyBase</span><span class="sxs-lookup"><span data-stu-id="08ea1-223">Load hello data into SQL Data Warehouse using PolyBase</span></span>

<span data-ttu-id="08ea1-224">Documentation complète disponible : [AZCopy][AZCopy].</span><span class="sxs-lookup"><span data-stu-id="08ea1-224">Full documentation available: [AZCopy][AZCopy].</span></span>

## <a name="optimizing-data-export"></a><span data-ttu-id="08ea1-225">Optimisation de l’exportation des données</span><span class="sxs-lookup"><span data-stu-id="08ea1-225">Optimizing data export</span></span>
<span data-ttu-id="08ea1-226">En outre tooensuring qu’exportation de hello est conforme toohello besoins par PolyBase vous peut également demander à exporter de hello toooptimize hello tooimprove hello du processus de données supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="08ea1-226">In addition tooensuring that hello export conforms toohello requirements laid out by PolyBase you can also seek toooptimize hello export of hello data tooimprove hello process further.</span></span>



### <a name="data-compression"></a><span data-ttu-id="08ea1-227">Compression des données</span><span class="sxs-lookup"><span data-stu-id="08ea1-227">Data compression</span></span>
<span data-ttu-id="08ea1-228">PolyBase peut lire les données compressées au format gzip.</span><span class="sxs-lookup"><span data-stu-id="08ea1-228">PolyBase can read gzip compressed data.</span></span> <span data-ttu-id="08ea1-229">Si vous êtes en mesure de toocompress votre toogzip des fichiers de données, puis vous serez minimiser hello données poussées dans le réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="08ea1-229">If you are able toocompress your data toogzip files then you will minimize hello amount of data being pushed over hello network.</span></span>

### <a name="multiple-files"></a><span data-ttu-id="08ea1-230">Fichiers multiples</span><span class="sxs-lookup"><span data-stu-id="08ea1-230">Multiple files</span></span>
<span data-ttu-id="08ea1-231">Avec rupture des tables volumineuses en plusieurs fichiers permet non seulement d’exporter la vitesse tooimprove, mais également avec transfert re-startability et hello facilité de gestion globale des données hello qu’une seule fois dans le stockage d’objets blob Azure hello.</span><span class="sxs-lookup"><span data-stu-id="08ea1-231">Breaking up large tables into several files not only helps tooimprove export speed, it also helps with transfer re-startability, and hello overall manageability of hello data once in hello Azure blob storage.</span></span> <span data-ttu-id="08ea1-232">Une des hello de nombreuses fonctionnalités intéressantes de PolyBase est sa capacité à lire tous les fichiers à l’intérieur d’un dossier hello et traiter en tant qu’une seule table.</span><span class="sxs-lookup"><span data-stu-id="08ea1-232">One of hello many nice features of PolyBase is that it will read all hello files inside a folder and treat it as one table.</span></span> <span data-ttu-id="08ea1-233">Il est donc une bonne idée tooisolate hello des fichiers pour chaque table dans son propre dossier.</span><span class="sxs-lookup"><span data-stu-id="08ea1-233">It is therefore a good idea tooisolate hello files for each table into its own folder.</span></span>

<span data-ttu-id="08ea1-234">PolyBase prend également en charge une fonction appelée « balayage de dossier récursif ».</span><span class="sxs-lookup"><span data-stu-id="08ea1-234">PolyBase also supports a feature known as "recursive folder traversal".</span></span> <span data-ttu-id="08ea1-235">Vous pouvez utiliser cette fonctionnalité toofurther améliorer votre gestion des données d’organisation hello de tooimprove de vos données exportées.</span><span class="sxs-lookup"><span data-stu-id="08ea1-235">You can use this feature toofurther enhance hello organization of your exported data tooimprove your data management.</span></span>

<span data-ttu-id="08ea1-236">toolearn en savoir plus sur le chargement des données avec PolyBase, consultez [PolyBase d’utilisation des données de tooload dans SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="08ea1-236">toolearn more about loading data with PolyBase, see [Use PolyBase tooload data into SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].</span></span>

## <a name="next-steps"></a><span data-ttu-id="08ea1-237">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="08ea1-237">Next steps</span></span>
<span data-ttu-id="08ea1-238">Pour plus d’informations sur la migration, consultez [migrer votre entrepôt de données de tooSQL solution][Migrate your solution tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="08ea1-238">For more about migration, see [Migrate your solution tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse].</span></span>
<span data-ttu-id="08ea1-239">Pour obtenir des conseils supplémentaires en matière de développement, consultez la [vue d’ensemble du développement][development overview].</span><span class="sxs-lookup"><span data-stu-id="08ea1-239">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution tooSQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp tooload data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase tooload data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
