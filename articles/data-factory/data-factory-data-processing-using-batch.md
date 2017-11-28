---
title: "Traiter des jeux de données volumineux à l’aide de Data Factory et Batch | Microsoft Docs"
description: "Décrit comment traiter de grandes quantités de données dans un pipeline Azure Data Factory en utilisant une capacité de traitement parallèle d’Azure Batch."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 9defbf7a6a515740fa3b3cb1c67a2f5f9d9baa01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a><span data-ttu-id="605de-103">Traiter des jeux de données volumineux à l’aide de Data Factory et Batch</span><span class="sxs-lookup"><span data-stu-id="605de-103">Process large-scale datasets using Data Factory and Batch</span></span>
<span data-ttu-id="605de-104">Cet article décrit une architecture d’un exemple de solution qui déplace et traite des jeux de données volumineux de manière automatique et planifiée.</span><span class="sxs-lookup"><span data-stu-id="605de-104">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span></span> <span data-ttu-id="605de-105">Il fournit également une procédure de bout en bout pour implémenter la solution à l’aide d’Azure Data Factory et d’Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="605de-105">It also provides an end-to-end walkthrough to implement the solution using Azure Data Factory and Azure Batch.</span></span>

<span data-ttu-id="605de-106">Cet article est plus long que nos articles habituels car il contient une procédure pas à pas d’un exemple de solution complète.</span><span class="sxs-lookup"><span data-stu-id="605de-106">This article is longer than our typical article because it contains a walkthrough of an entire sample solution.</span></span> <span data-ttu-id="605de-107">Si vous débutez avec Batch et Data Factory, vous découvrirez différentes informations sur ces services et comment ils fonctionnent ensemble.</span><span class="sxs-lookup"><span data-stu-id="605de-107">If you are new to Batch and Data Factory, you can learn about these services and how they work together.</span></span> <span data-ttu-id="605de-108">Si vous connaissez déjà ces services et que vous concevez/élaborez une solution, vous pouvez vous concentrer uniquement sur la [section architecture](#architecture-of-sample-solution) de l’article. Si vous développez un prototype ou une solution, vous pouvez également suivre nos instructions détaillées dans la [procédure pas à pas](#implementation-of-sample-solution).</span><span class="sxs-lookup"><span data-stu-id="605de-108">If you know something about the services and are designing/architecting a solution, you may focus just on the [architecture section](#architecture-of-sample-solution) of the article and if you are developing a prototype or a solution, you may also want to try out step-by-step instructions in the [walkthrough](#implementation-of-sample-solution).</span></span> <span data-ttu-id="605de-109">N’hésitez pas à nous faire part de vos commentaires sur ce contenu et son utilisation.</span><span class="sxs-lookup"><span data-stu-id="605de-109">We invite your comments about this content and how you use it.</span></span>

<span data-ttu-id="605de-110">Tout d’abord, découvrons de quelle manière les services Data Factory et Batch permettent de traiter des jeux de données volumineux dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="605de-110">First, let's look at how Data Factory and Batch services can help with processing large datasets in the cloud.</span></span>     

## <a name="why-azure-batch"></a><span data-ttu-id="605de-111">Pourquoi Azure Batch ?</span><span class="sxs-lookup"><span data-stu-id="605de-111">Why Azure Batch?</span></span>
<span data-ttu-id="605de-112">Azure Batch vous permet d’exécuter efficacement dans le cloud des applications de calcul haute performance (HPC) en parallèle et à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="605de-112">Azure Batch enables you to run large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="605de-113">Ce service de plateforme planifie les travaux nécessitant une grande quantité de ressources système à exécuter sur une collection gérée de machines virtuelles. Il peut mettre automatiquement à l’échelle les ressources de calcul pour répondre aux besoins du travail.</span><span class="sxs-lookup"><span data-stu-id="605de-113">It's a platform service that schedules compute-intensive work to run on a managed collection of virtual machines, and can automatically scale compute resources to meet the needs of your jobs.</span></span>

<span data-ttu-id="605de-114">Avec le service Batch, vous définissez des ressources de calcul Azure pour exécuter vos applications en parallèle et à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="605de-114">With the Batch service, you define Azure compute resources to execute your applications in parallel, and at scale.</span></span> <span data-ttu-id="605de-115">Vous pouvez exécuter des travaux à la demande ou selon un calendrier précis, sans avoir à créer, configurer et gérer manuellement un cluster HPC, des machines virtuelles individuelles, des réseaux virtuels ou une infrastructure complexe de planification des tâches et des travaux.</span><span class="sxs-lookup"><span data-stu-id="605de-115">You can run on-demand or scheduled jobs, and you don't need to manually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span>

<span data-ttu-id="605de-116">Si vous ne connaissez pas Azure Batch, consultez les articles suivants qui vous aideront à comprendre l’architecture/l’implémentation de la solution décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="605de-116">See the following articles if you are not familiar with Azure Batch as it helps with understanding the architecture/implementation of the solution described in this article.</span></span>   

* [<span data-ttu-id="605de-117">Notions de base d’Azure Batch</span><span class="sxs-lookup"><span data-stu-id="605de-117">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
* [<span data-ttu-id="605de-118">Aperçu des fonctionnalités d’Azure Batch</span><span class="sxs-lookup"><span data-stu-id="605de-118">Batch feature overview</span></span>](../batch/batch-api-basics.md)

<span data-ttu-id="605de-119">(facultatif) Pour en savoir plus sur Azure Batch, voir [Parcours d’apprentissage pour Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span><span class="sxs-lookup"><span data-stu-id="605de-119">(optional) To learn more about Azure Batch, see the [Learning path for Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span></span>

## <a name="why-azure-data-factory"></a><span data-ttu-id="605de-120">Pourquoi Azure Data Factory ?</span><span class="sxs-lookup"><span data-stu-id="605de-120">Why Azure Data Factory?</span></span>
<span data-ttu-id="605de-121">Data Factory est un service d’intégration de données dans le cloud qui gère et automatise le déplacement et la transformation des données.</span><span class="sxs-lookup"><span data-stu-id="605de-121">Data Factory is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="605de-122">Grâce au service Data Factory, vous pouvez créer des pipelines de données gérés pour déplacer les données des magasins de données locaux et cloud vers un magasin de données centralisé (par exemple : le stockage d’objets blob Azure) et traiter/transformer les données à l’aide de services tels que Azure HDInsight et Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="605de-122">Using the Data Factory service, you can create managed data pipelines that move data from on-premises and cloud data stores to a centralized data store (for example: Azure Blob Storage), and process/transform data using services such as Azure HDInsight and Azure Machine Learning.</span></span> <span data-ttu-id="605de-123">Vous pouvez également configurer les pipelines de données pour qu’ils s’exécutent de manière programmée (toutes les heures, tous les jours, toutes les semaines, etc.), mais aussi les surveiller et les gérer en un coup d’œil afin d’identifier les problèmes et de prendre les mesures adéquates.</span><span class="sxs-lookup"><span data-stu-id="605de-123">You can also schedule data pipelines to run in a scheduled manner (hourly, daily, weekly, etc.) and monitor and manage them at a glance to identify issues and take action.</span></span>

<span data-ttu-id="605de-124">Si vous ne connaissez pas Azure Data Factory, consultez les articles suivants qui vous aideront à comprendre l’architecture/l’implémentation de la solution décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="605de-124">See the following articles if you are not familiar with Azure Data Factory as it helps with understanding the architecture/implementation of the solution described in this article.</span></span>  

* [<span data-ttu-id="605de-125">Présentation d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="605de-125">Introduction of Azure Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="605de-126">Générer votre premier pipeline de données</span><span class="sxs-lookup"><span data-stu-id="605de-126">Build your first data pipeline</span></span>](data-factory-build-your-first-pipeline.md)   

<span data-ttu-id="605de-127">(facultatif) Pour en savoir plus sur Azure Data Factory, voir [Parcours d’apprentissage Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="605de-127">(optional) To learn more about Azure Data Factory, see the [Learning path for Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span></span>

## <a name="data-factory-and-batch-together"></a><span data-ttu-id="605de-128">Intégration de Data Factory et Batch</span><span class="sxs-lookup"><span data-stu-id="605de-128">Data Factory and Batch together</span></span>
<span data-ttu-id="605de-129">Data Factory comprend des activités intégrées telles que l’activité de copie pour copier/déplacer des données à partir d’un magasin de données source vers un magasin de données de destination et l’activité Hive pour traiter les données à l’aide de clusters Hadoop (HDInsight) dans Azure.</span><span class="sxs-lookup"><span data-stu-id="605de-129">Data Factory includes built-in activities such as Copy Activity to copy/move data from a source data store to a destination data store and Hive Activity to process data using Hadoop clusters (HDInsight) on Azure.</span></span> <span data-ttu-id="605de-130">Consultez l’article [Activités de transformation des données](data-factory-data-transformation-activities.md) pour obtenir la liste des activités de transformation prises en charge.</span><span class="sxs-lookup"><span data-stu-id="605de-130">See [Data Transformation Activities](data-factory-data-transformation-activities.md) for a list of supported transformation activities.</span></span>

<span data-ttu-id="605de-131">Il vous permet également de créer des activités .NET personnalisées pour déplacer ou traiter les données selon votre propre logique et d’exécuter ces activités dans un cluster Azure HDInsight ou dans un pool de machines virtuelles Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="605de-131">It also allows you to create custom .NET activities to move or process data with your own logic and run these activities on an Azure HDInsight cluster or on an Azure Batch pool of VMs.</span></span> <span data-ttu-id="605de-132">Lorsque vous utilisez Azure Batch, vous pouvez configurer la mise à l’échelle automatique du pool (ajouter ou supprimer des machines virtuelles en fonction de la charge de travail) selon une formule que vous définissez.</span><span class="sxs-lookup"><span data-stu-id="605de-132">When you use Azure Batch, you can configure the pool to auto-scale (add or remove VMs based on the workload) based on a formula you provide.</span></span>     

## <a name="architecture-of-sample-solution"></a><span data-ttu-id="605de-133">Architecture de l’exemple de solution</span><span class="sxs-lookup"><span data-stu-id="605de-133">Architecture of sample solution</span></span>
<span data-ttu-id="605de-134">Même si l’architecture décrite dans cet article est associée à une solution simple, elle s’applique à des scénarios complexes, tels que la modélisation des risques par les services financiers, le traitement et la restitution d’images, ou encore l’analyse génomique.</span><span class="sxs-lookup"><span data-stu-id="605de-134">Even though the architecture described in this article is for a simple solution, it is relevant to complex scenarios such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span></span>

<span data-ttu-id="605de-135">Le diagramme illustre 1) la manière dont Data Factory orchestre le déplacement et le traitement des données, et (2) la manière dont Azure Batch traite les données en parallèle.</span><span class="sxs-lookup"><span data-stu-id="605de-135">The diagram illustrates 1) how Data Factory orchestrates data movement and processing and 2) how Azure Batch processes the data in a parallel manner.</span></span> <span data-ttu-id="605de-136">Téléchargez et imprimez le diagramme pour le consulter facilement (11 x 17 pouces</span><span class="sxs-lookup"><span data-stu-id="605de-136">Download and print the diagram for easy reference (11 x 17 in.</span></span> <span data-ttu-id="605de-137">ou format A3) : [Calcul haute performance et orchestration de données à l’aide des services Azure Batch et Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span><span class="sxs-lookup"><span data-stu-id="605de-137">or A3 size): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span></span>

<span data-ttu-id="605de-138">[![Diagramme de traitement des données à grande échelle](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="605de-138">[![Large-scale data processing diagram](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span></span>

<span data-ttu-id="605de-139">La liste suivante fournit les étapes de base du processus.</span><span class="sxs-lookup"><span data-stu-id="605de-139">The following list provides the basic steps of the process.</span></span> <span data-ttu-id="605de-140">La solution inclut du code et des explications relatives à la génération de la solution de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="605de-140">The solution includes code and explanations to build the end-to-end solution.</span></span>

1. <span data-ttu-id="605de-141">**Configurez Azure Batch avec un pool de nœuds de calcul (machines virtuelles)**.</span><span class="sxs-lookup"><span data-stu-id="605de-141">**Configure Azure Batch with a pool of compute nodes (VMs)**.</span></span> <span data-ttu-id="605de-142">Vous pouvez spécifier le nombre de nœuds et la taille de chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="605de-142">You can specify the number of nodes and size of each node.</span></span>
2. <span data-ttu-id="605de-143">**Créez une instance Azure Data Factory** configurée avec des entités qui représentent respectivement le stockage d’objets blob Azure, le service de calcul Azure Batch, les données en entrée et sortie, ainsi qu’un flux de travail, ou pipeline, d’activités qui déplacent et transforment des données.</span><span class="sxs-lookup"><span data-stu-id="605de-143">**Create an Azure Data Factory instance** that is configured with entities that represent Azure blob storage, Azure Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span></span>
3. <span data-ttu-id="605de-144">**Créez une activité .NET personnalisée dans le pipeline Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="605de-144">**Create a custom .NET activity in the Data Factory pipeline**.</span></span> <span data-ttu-id="605de-145">L’activité est votre code utilisateur qui s’exécute sur le pool Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="605de-145">The activity is your user code that runs on the Azure Batch pool.</span></span>
4. <span data-ttu-id="605de-146">**Stockez de grandes quantités de données d’entrée en tant qu’objets blob dans Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="605de-146">**Store large amounts of input data as blobs in Azure storage**.</span></span> <span data-ttu-id="605de-147">Les données sont divisées en tranches logiques (généralement basées sur l’heure).</span><span class="sxs-lookup"><span data-stu-id="605de-147">Data is divided into logical slices (usually by time).</span></span>
5. <span data-ttu-id="605de-148">**Data Factory copie vers l’emplacement secondaire les données qui sont traitées en parallèle**.</span><span class="sxs-lookup"><span data-stu-id="605de-148">**Data Factory copies data that is processed in parallel** to the secondary location.</span></span>
6. <span data-ttu-id="605de-149">**Data Factory exécute l’activité personnalisée à l’aide du pool alloué par Batch**.</span><span class="sxs-lookup"><span data-stu-id="605de-149">**Data Factory runs the custom activity using the pool allocated by Batch**.</span></span> <span data-ttu-id="605de-150">Data Factory peut exécuter plusieurs activités simultanément.</span><span class="sxs-lookup"><span data-stu-id="605de-150">Data Factory can run activities concurrently.</span></span> <span data-ttu-id="605de-151">Chaque activité traite une tranche de données.</span><span class="sxs-lookup"><span data-stu-id="605de-151">Each activity processes a slice of data.</span></span> <span data-ttu-id="605de-152">Les résultats sont stockés dans Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="605de-152">The results are stored in Azure storage.</span></span>
7. <span data-ttu-id="605de-153">**Data Factory déplace les résultats finaux vers un troisième emplacement**, soit pour les distribuer via une application, soit pour les traiter avec d’autres outils.</span><span class="sxs-lookup"><span data-stu-id="605de-153">**Data Factory moves the final results to a third location**, either for distribution via an app, or for further processing by other tools.</span></span>

## <a name="implementation-of-sample-solution"></a><span data-ttu-id="605de-154">Implémentation de l’exemple de solution</span><span class="sxs-lookup"><span data-stu-id="605de-154">Implementation of sample solution</span></span>
<span data-ttu-id="605de-155">L’exemple de solution est volontairement simple et a pour objectif de vous montrer comment utiliser conjointement les services Data Factory et Batch pour traiter des jeux de données.</span><span class="sxs-lookup"><span data-stu-id="605de-155">The sample solution is intentionally simple and is to show you how to use Data Factory and Batch together to process datasets.</span></span> <span data-ttu-id="605de-156">La solution compte le nombre d’occurrences d’un terme de recherche (« Microsoft ») dans les fichiers d’entrée organisés en série chronologique.</span><span class="sxs-lookup"><span data-stu-id="605de-156">The solution simply counts the number of occurrences of a search term (“Microsoft”) in input files organized in a time series.</span></span> <span data-ttu-id="605de-157">Il renvoie le nombre de fichiers de sortie.</span><span class="sxs-lookup"><span data-stu-id="605de-157">It outputs the count to output files.</span></span>

<span data-ttu-id="605de-158">**Temps** : si vous maîtrisez Azure, Data Factory et Batch et que vous disposez des composants requis listés ci-dessous, cette solution devrait vous prendre entre 1 et 2 heures.</span><span class="sxs-lookup"><span data-stu-id="605de-158">**Time**: If you are familiar with basics of Azure, Data Factory, and Batch, and have completed the prerequisites listed below, we estimate this solution takes 1-2 hours to complete.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="605de-159">Composants requis</span><span class="sxs-lookup"><span data-stu-id="605de-159">Prerequisites</span></span>
#### <a name="azure-subscription"></a><span data-ttu-id="605de-160">Abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="605de-160">Azure subscription</span></span>
<span data-ttu-id="605de-161">Si vous n’êtes pas abonné, vous pouvez créer un compte d’essai gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="605de-161">If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="605de-162">Voir [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="605de-162">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

#### <a name="azure-storage-account"></a><span data-ttu-id="605de-163">Compte Azure Storage</span><span class="sxs-lookup"><span data-stu-id="605de-163">Azure storage account</span></span>
<span data-ttu-id="605de-164">Dans ce didacticiel, vous utilisez un compte de stockage Azure pour stocker des données.</span><span class="sxs-lookup"><span data-stu-id="605de-164">You use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="605de-165">Si vous ne possédez pas de compte de stockage Azure, voir [Création d’un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="605de-165">If you don't have an Azure storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="605de-166">L’exemple de solution utilise un stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="605de-166">The sample solution uses blob storage.</span></span>

#### <a name="azure-batch-account"></a><span data-ttu-id="605de-167">Compte Azure Batch</span><span class="sxs-lookup"><span data-stu-id="605de-167">Azure Batch account</span></span>
<span data-ttu-id="605de-168">Créez un compte Azure Batch via le [portail Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="605de-168">Create an Azure Batch account using the [Azure portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="605de-169">Voir [Créer et gérer un compte Azure Batch](../batch/batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="605de-169">See [Create and manage an Azure Batch account](../batch/batch-account-create-portal.md).</span></span> <span data-ttu-id="605de-170">Notez la clé et le nom du compte Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="605de-170">Note the Azure Batch account name and account key.</span></span> <span data-ttu-id="605de-171">Vous pouvez également créer un compte Azure Batch à l’aide de l’applet de commande [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) .</span><span class="sxs-lookup"><span data-stu-id="605de-171">You can also use [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet to create an Azure Batch account.</span></span> <span data-ttu-id="605de-172">Pour obtenir des instructions détaillées sur l’utilisation de cette applet de commande, voir [Prise en main des applets de commande Azure Batch PowerShell](../batch/batch-powershell-cmdlets-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="605de-172">See [Get started with Azure Batch PowerShell cmdlets](../batch/batch-powershell-cmdlets-get-started.md) for detailed instructions on using this cmdlet.</span></span>

<span data-ttu-id="605de-173">L’exemple de solution utilise Azure Batch (indirectement via un pipeline Azure Data Factory) pour traiter des données en parallèle sur un pool de nœuds de calcul (une collection gérée de machines virtuelles).</span><span class="sxs-lookup"><span data-stu-id="605de-173">The sample solution uses Azure Batch (indirectly via an Azure Data Factory pipeline) to process data in a parallel manner on a pool of compute nodes (a managed collection of virtual machines).</span></span>

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a><span data-ttu-id="605de-174">Pool de machines virtuelles Azure Batch</span><span class="sxs-lookup"><span data-stu-id="605de-174">Azure Batch pool of virtual machines (VMs)</span></span>
<span data-ttu-id="605de-175">Créez un **pool Azure Batch** comprenant au moins 2 nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="605de-175">Create an **Azure Batch pool** with at least 2 compute nodes.</span></span>

1. <span data-ttu-id="605de-176">Dans le [portail Azure](https://portal.azure.com), cliquez sur **Parcourir** dans le menu de gauche, puis cliquez sur **Comptes Batch**.</span><span class="sxs-lookup"><span data-stu-id="605de-176">In the [Azure portal](https://portal.azure.com), click **Browse** in the left menu, and click **Batch Accounts**.</span></span>
2. <span data-ttu-id="605de-177">Sélectionnez votre compte Azure Batch pour ouvrir le panneau **Compte Batch** .</span><span class="sxs-lookup"><span data-stu-id="605de-177">Select your Azure Batch account to open the **Batch Account** blade.</span></span>
3. <span data-ttu-id="605de-178">Cliquez sur la vignette **Pools** .</span><span class="sxs-lookup"><span data-stu-id="605de-178">Click **Pools** tile.</span></span>
4. <span data-ttu-id="605de-179">Dans le panneau **Pools** , cliquez sur le bouton Ajouter de la barre d’outils pour ajouter un pool.</span><span class="sxs-lookup"><span data-stu-id="605de-179">In the **Pools** blade, click Add button on the toolbar to add a pool.</span></span>
   1. <span data-ttu-id="605de-180">Entrez un ID pour le pool (**ID du pool**).</span><span class="sxs-lookup"><span data-stu-id="605de-180">Enter an ID for the pool (**Pool ID**).</span></span> <span data-ttu-id="605de-181">Notez **l’ID du pool**, car vous en aurez besoin lors de la création de la solution Data Factory.</span><span class="sxs-lookup"><span data-stu-id="605de-181">Note the **ID of the pool**; you need it when creating the Data Factory solution.</span></span>
   2. <span data-ttu-id="605de-182">Spécifiez **Windows Server 2012 R2** pour le paramètre de famille du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="605de-182">Specify **Windows Server 2012 R2** for the Operating System Family setting.</span></span>
   3. <span data-ttu-id="605de-183">Sélectionnez le **niveau tarifaire du nœud**.</span><span class="sxs-lookup"><span data-stu-id="605de-183">Select a **node pricing tier**.</span></span>
   4. <span data-ttu-id="605de-184">Entrez **2** comme valeur du paramètre **Quantité dédiée cible**.</span><span class="sxs-lookup"><span data-stu-id="605de-184">Enter **2** as value for the **Target Dedicated** setting.</span></span>
   5. <span data-ttu-id="605de-185">Entrez **2** comme valeur du paramètre **Nombre maximal de tâches par nœud**.</span><span class="sxs-lookup"><span data-stu-id="605de-185">Enter **2** as value for the **Max tasks per node** setting.</span></span>
   6. <span data-ttu-id="605de-186">Cliquez sur **OK** pour créer le pool.</span><span class="sxs-lookup"><span data-stu-id="605de-186">Click **OK** to create the pool.</span></span>

#### <a name="azure-storage-explorer"></a><span data-ttu-id="605de-187">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="605de-187">Azure Storage Explorer</span></span>
<span data-ttu-id="605de-188">[Azure Storage Explorer 6 (outil)](https://azurestorageexplorer.codeplex.com/) ou [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (à partir du logiciel ClumsyLeaf).</span><span class="sxs-lookup"><span data-stu-id="605de-188">[Azure Storage Explorer 6 (tool)](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software).</span></span> <span data-ttu-id="605de-189">Vous utilisez ces outils pour consulter et modifier les données de vos projets Stockage Azure, notamment les journaux de vos applications hébergées dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="605de-189">You use these tools for inspecting and altering the data in your Azure Storage projects including the logs of your cloud-hosted applications.</span></span>

1. <span data-ttu-id="605de-190">Créez un conteneur nommé **mycontainer** avec un accès privé (par d’accès anonyme).</span><span class="sxs-lookup"><span data-stu-id="605de-190">Create a container named **mycontainer** with private access (no anonymous access)</span></span>
2. <span data-ttu-id="605de-191">Si vous utilisez **CloudXplorer**, créez des dossiers et sous-dossiers avec la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="605de-191">If you are using **CloudXplorer**, create folders and subfolders with the following structure:</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   <span data-ttu-id="605de-192">`Inputfolder` et `outputfolder` sont des dossiers de niveau supérieur de `mycontainer`.</span><span class="sxs-lookup"><span data-stu-id="605de-192">`Inputfolder` and `outputfolder` are top-level folders in `mycontainer`.</span></span> <span data-ttu-id="605de-193">Le dossier `inputfolder` contient des sous-dossiers horodatés (AAAA-MM-JJ-HH).</span><span class="sxs-lookup"><span data-stu-id="605de-193">The `inputfolder` has subfolders with date-time stamps (YYYY-MM-DD-HH).</span></span>

   <span data-ttu-id="605de-194">Si vous utilisez **l’Explorateur de stockage Azure**, à l’étape suivante, vous devez charger les fichiers nommés `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="605de-194">If you are using **Azure Storage Explorer**, in the next step, you need to upload files with names: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` and so on.</span></span> <span data-ttu-id="605de-195">Cette étape crée automatiquement les dossiers.</span><span class="sxs-lookup"><span data-stu-id="605de-195">This step automatically creates the folders.</span></span>
3. <span data-ttu-id="605de-196">Créez sur votre ordinateur un fichier texte **file.txt** contenant le mot clé **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="605de-196">Create a text file **file.txt** on your machine with content that has the keyword **Microsoft**.</span></span> <span data-ttu-id="605de-197">Par exemple, « activité de test personnalisé Microsoft ».</span><span class="sxs-lookup"><span data-stu-id="605de-197">For example: “test custom activity Microsoft test custom activity Microsoft”.</span></span>
4. <span data-ttu-id="605de-198">Chargez le fichier dans les dossiers d’entrée suivants du stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="605de-198">Upload the file to the following input folders in Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   <span data-ttu-id="605de-199">Si vous utilisez **l’Explorateur de stockage Azure**, chargez le fichier **file.txt** dans **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="605de-199">If you are using **Azure Storage Explorer**, upload the file **file.txt** to **mycontainer**.</span></span> <span data-ttu-id="605de-200">Cliquez sur **Copy** (Copier) dans la barre d’outils pour créer une copie de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="605de-200">Click **Copy** on the toolbar to create a copy of the blob.</span></span> <span data-ttu-id="605de-201">Dans la boîte de dialogue **Copy Blob** (Copie de l’objet blob), remplacez le **nom d’objet blob de destination** par `inputfolder/2015-11-16-00/file.txt`.</span><span class="sxs-lookup"><span data-stu-id="605de-201">In the **Copy Blob** dialog box, change the **destination blob name** to `inputfolder/2015-11-16-00/file.txt`.</span></span> <span data-ttu-id="605de-202">Répétez cette étape pour créer `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="605de-202">Repeat this step to create `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` and so on.</span></span> <span data-ttu-id="605de-203">Cette action crée automatiquement les dossiers.</span><span class="sxs-lookup"><span data-stu-id="605de-203">This action automatically creates the folders.</span></span>
5. <span data-ttu-id="605de-204">Créez un autre conteneur nommé : `customactivitycontainer`.</span><span class="sxs-lookup"><span data-stu-id="605de-204">Create another container named: `customactivitycontainer`.</span></span> <span data-ttu-id="605de-205">Vous chargez le fichier zip d’activité personnalisée dans ce conteneur.</span><span class="sxs-lookup"><span data-stu-id="605de-205">You upload the custom activity zip file to this container.</span></span>

#### <a name="visual-studio"></a><span data-ttu-id="605de-206">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="605de-206">Visual Studio</span></span>
<span data-ttu-id="605de-207">Installez Microsoft Visual Studio 2012 ou version ultérieure pour créer l’activité Batch personnalisée à utiliser dans la solution Data Factory.</span><span class="sxs-lookup"><span data-stu-id="605de-207">Install Microsoft Visual Studio 2012 or later to create the custom Batch activity to be used in the Data Factory solution.</span></span>

### <a name="high-level-steps-to-create-the-solution"></a><span data-ttu-id="605de-208">Principales étapes pour créer la solution</span><span class="sxs-lookup"><span data-stu-id="605de-208">High-level steps to create the solution</span></span>
1. <span data-ttu-id="605de-209">Créez une activité personnalisée contenant la logique de traitement des données.</span><span class="sxs-lookup"><span data-stu-id="605de-209">Create a custom activity that contains the data processing logic.</span></span>
2. <span data-ttu-id="605de-210">Créez une fabrique de données Azure qui utilise l’activité personnalisée :</span><span class="sxs-lookup"><span data-stu-id="605de-210">Create an Azure data factory that uses the custom activity:</span></span>

### <a name="create-the-custom-activity"></a><span data-ttu-id="605de-211">Création de l’activité personnalisée</span><span class="sxs-lookup"><span data-stu-id="605de-211">Create the custom activity</span></span>
<span data-ttu-id="605de-212">L’activité personnalisée de Data Factory est au cœur de cet exemple de solution.</span><span class="sxs-lookup"><span data-stu-id="605de-212">The Data Factory custom activity is the heart of this sample solution.</span></span> <span data-ttu-id="605de-213">L’exemple de solution utilise Azure Batch pour exécuter l’activité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="605de-213">The sample solution uses Azure Batch to run the custom activity.</span></span> <span data-ttu-id="605de-214">Pour les informations de base relatives au développement d’activités personnalisées et leur utilisation dans des pipelines Azure Data Factory, voir [Utilisation des activités personnalisées dans un pipeline Azure Data Factory](data-factory-use-custom-activities.md) .</span><span class="sxs-lookup"><span data-stu-id="605de-214">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) for the basic information to develop custom activities and use them in Azure Data Factory pipelines.</span></span>

<span data-ttu-id="605de-215">Pour créer une activité personnalisée .NET utilisable dans un pipeline Azure Data Factory, vous devez créer un projet de **bibliothèque de classes .NET** contenant une classe qui implémente cette interface **IDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="605de-215">To create a .NET custom activity that you can use in an Azure Data Factory pipeline, you need to create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="605de-216">Cette interface possède une seule méthode : **Execute**.</span><span class="sxs-lookup"><span data-stu-id="605de-216">This interface has only one method: **Execute**.</span></span> <span data-ttu-id="605de-217">Voici la signature de la méthode :</span><span class="sxs-lookup"><span data-stu-id="605de-217">Here is the signature of the method:</span></span>

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

<span data-ttu-id="605de-218">La méthode comporte quelques composants clés qu’il est important d’assimiler.</span><span class="sxs-lookup"><span data-stu-id="605de-218">The method has a few key components that you need to understand.</span></span>

* <span data-ttu-id="605de-219">La méthode accepte quatre paramètres :</span><span class="sxs-lookup"><span data-stu-id="605de-219">The method takes four parameters:</span></span>

  1. <span data-ttu-id="605de-220">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="605de-220">**linkedServices**.</span></span> <span data-ttu-id="605de-221">Liste énumérable de services liés qui relie les sources de données d’entrée/sortie (par exemple, Stockage Blob Azure) à la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="605de-221">An enumerable list of linked services that link input/output data sources (for example: Azure Blob Storage) to the data factory.</span></span> <span data-ttu-id="605de-222">Dans cet exemple, il s’agit du seul service lié de type Azure Storage utilisé à la fois pour les données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="605de-222">In this sample, there is only one linked service of type Azure Storage used for both input and output.</span></span>
  2. <span data-ttu-id="605de-223">**jeux de données**.</span><span class="sxs-lookup"><span data-stu-id="605de-223">**datasets**.</span></span> <span data-ttu-id="605de-224">liste énumérable de jeux de données.</span><span class="sxs-lookup"><span data-stu-id="605de-224">This is an enumerable list of datasets.</span></span> <span data-ttu-id="605de-225">Vous pouvez utiliser ce paramètre pour obtenir les emplacements et les schémas définis par les jeux de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="605de-225">You can use this parameter to get the locations and schemas defined by input and output datasets.</span></span>
  3. <span data-ttu-id="605de-226">**activity**.</span><span class="sxs-lookup"><span data-stu-id="605de-226">**activity**.</span></span> <span data-ttu-id="605de-227">ce paramètre représente l’entité de calcul actuelle (dans ce cas, un service Azure Batch).</span><span class="sxs-lookup"><span data-stu-id="605de-227">This parameter represents the current compute entity - in this case, an Azure Batch service.</span></span>
  4. <span data-ttu-id="605de-228">**logger**.</span><span class="sxs-lookup"><span data-stu-id="605de-228">**logger**.</span></span> <span data-ttu-id="605de-229">L’enregistreur vous permet d’écrire des commentaires de débogage qui apparaîtront en tant que journal « utilisateur » pour le pipeline.</span><span class="sxs-lookup"><span data-stu-id="605de-229">The logger lets you write debug comments that surface as the “User” log for the pipeline.</span></span>
* <span data-ttu-id="605de-230">La méthode retourne un dictionnaire qui peut être utilisé pour enchaîner ultérieurement des activités personnalisées.</span><span class="sxs-lookup"><span data-stu-id="605de-230">The method returns a dictionary that can be used to chain custom activities together in the future.</span></span> <span data-ttu-id="605de-231">Cette fonctionnalité n’étant pas encore implémentée, seul un dictionnaire vide est retourné par la méthode.</span><span class="sxs-lookup"><span data-stu-id="605de-231">This feature is not implemented yet, so return an empty dictionary from the method.</span></span>

#### <a name="procedure-create-the-custom-activity"></a><span data-ttu-id="605de-232">Procédure : Création de l’activité personnalisée</span><span class="sxs-lookup"><span data-stu-id="605de-232">Procedure: Create the custom activity</span></span>
1. <span data-ttu-id="605de-233">Créez un projet de bibliothèque de classes .NET dans Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="605de-233">Create a .NET Class Library project in Visual Studio.</span></span>

   1. <span data-ttu-id="605de-234">Lancez **Visual Studio 2012**/**2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="605de-234">Launch **Visual Studio 2012**/**2013/2015**.</span></span>
   2. <span data-ttu-id="605de-235">Cliquez sur **Fichier**, pointez le curseur de la souris sur **Nouveau**, puis cliquez sur **Projet**.</span><span class="sxs-lookup"><span data-stu-id="605de-235">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="605de-236">Développez **Modèles**, puis sélectionnez **Visual C\#**.</span><span class="sxs-lookup"><span data-stu-id="605de-236">Expand **Templates**, and select **Visual C\#**.</span></span> <span data-ttu-id="605de-237">Dans cette procédure pas à pas, vous utilisez C\#, mais vous pouvez utiliser un autre langage .NET pour développer l’activité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="605de-237">In this walkthrough, you use C\#, but you can use any .NET language to develop the custom activity.</span></span>
   4. <span data-ttu-id="605de-238">Sélectionnez **Bibliothèque de classes** dans la liste des types de projet, sur la droite.</span><span class="sxs-lookup"><span data-stu-id="605de-238">Select **Class Library** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="605de-239">Entrez **MyDotNetActivity** for the **Nom**.</span><span class="sxs-lookup"><span data-stu-id="605de-239">Enter **MyDotNetActivity** for the **Name**.</span></span>
   6. <span data-ttu-id="605de-240">Sélectionnez **C:\\ADF** comme **emplacement**.</span><span class="sxs-lookup"><span data-stu-id="605de-240">Select **C:\\ADF** for the **Location**.</span></span> <span data-ttu-id="605de-241">Créez le dossier **ADF** s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="605de-241">Create the folder **ADF** if it does not exist.</span></span>
   7. <span data-ttu-id="605de-242">Cliquez sur **OK** pour créer le projet.</span><span class="sxs-lookup"><span data-stu-id="605de-242">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="605de-243">Cliquez sur **Outils**, pointez le curseur de la souris sur **Gestionnaire de package NuGet**, puis cliquez sur **Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="605de-243">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="605de-244">Dans la **Console du gestionnaire de package**, exécutez la commande suivante pour importer l’élément **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="605de-244">In the **Package Manager Console**, execute the following command to import **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="605de-245">Importez le package NuGet **Azure Storage** dans le projet.</span><span class="sxs-lookup"><span data-stu-id="605de-245">Import the **Azure Storage** NuGet package in to the project.</span></span> <span data-ttu-id="605de-246">Vous en avez besoin, car vous utilisez l’API de stockage d’objets Blob dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="605de-246">You need this package because you use the Blob storage API in this sample.</span></span>

    ```powershell
    Install-Package Azure.Storage
    ```
5. <span data-ttu-id="605de-247">Ajoutez les instructions **using** suivantes au fichier source du projet.</span><span class="sxs-lookup"><span data-stu-id="605de-247">Add the following **using** directives to the source file in the project.</span></span>

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="605de-248">Remplacez le nom de **l’espace de noms** par **MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="605de-248">Change the name of the **namespace** to **MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="605de-249">Remplacez le nom de la classe par **MyDotNetActivity** et dérivez-le de l’interface **IDotNetActivity**, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="605de-249">Change the name of the class to **MyDotNetActivity** and derive it from the **IDotNetActivity** interface as shown below.</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="605de-250">Implémentez (ajoutez) la méthode **Execute** de l’interface **IDotNetActivity** dans la classe **MyDotNetActivity** et copiez l’exemple de code suivant dans la méthode.</span><span class="sxs-lookup"><span data-stu-id="605de-250">Implement (Add) the **Execute** method of the **IDotNetActivity** interface to the **MyDotNetActivity** class and copy the following sample code to the method.</span></span> <span data-ttu-id="605de-251">Pour une explication de la logique utilisée dans cette méthode, voir la section [Méthode Execute](#execute-method) .</span><span class="sxs-lookup"><span data-stu-id="605de-251">See the [Execute Method](#execute-method) section for explanation for the logic used in this method.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is the only method of IDotNetActivity interface you must implement.
    /// In this sample, the method invokes the Calculate method to perform the core logic.  
    /// </summary>
    public IDictionary<string, string> Execute(
       IEnumerable<LinkedService> linkedServices,
       IEnumerable<Dataset> datasets,
       Activity activity,
       IActivityLogger logger)
    {
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using the same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // To create an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // create storage client for input. Pass the connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // initialize the continuation token before using it in the do-while loop.
       BlobContinuationToken continuationToken = null;
       do
       {   // get the list of input blobs from the input storage client object.
           BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                    true,
                                    BlobListingDetails.Metadata,
                                    null,
                                    continuationToken,
                                    null,
                                    null);
    
           // Calculate method returns the number of occurrences of
           // the search term (“Microsoft”) in each blob associated
           // with the data slice.
           //
           // definition of the method is shown in the next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get the output dataset using the name of the dataset matched to a name in the Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob to the folder: {0}", folderPath);
    
       // create a storage object for the output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write the name of the file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // create a blob and upload the output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} to the output blob", output);
       outputBlob.UploadText(output);
    
       // The dictionary can be used to chain custom activities together in the future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="605de-252">Ajoutez les méthodes d’assistance suivantes à la classe.</span><span class="sxs-lookup"><span data-stu-id="605de-252">Add the following helper methods to the class.</span></span> <span data-ttu-id="605de-253">Ces méthodes sont appelées par la méthode **Execute** .</span><span class="sxs-lookup"><span data-stu-id="605de-253">These methods are invoked by the **Execute** method.</span></span> <span data-ttu-id="605de-254">Plus important encore, la méthode **Calculate** isole le code qui effectue une itération dans chaque objet blob.</span><span class="sxs-lookup"><span data-stu-id="605de-254">Most importantly, the **Calculate** method isolates the code that iterates through each blob.</span></span>

    ```csharp
    /// <summary>
    /// Gets the folderPath value from the input/output dataset.
    /// </summary>
    private static string GetFolderPath(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets the fileName value from the input/output dataset.
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in the folder, counts the number of instances of search term in the file,
    /// and prepares the output text that is written to the output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
       string output = string.Empty;
       logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
       foreach (IListBlobItem listBlobItem in Bresult.Results)
       {
           CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
           if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
           {
               string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
               logger.Write("input blob text: {0}", blobText);
               string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
               var matchQuery = from word in source
                                where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                select word;
               int wordCount = matchQuery.Count();
               output += string.Format("{0} occurrences(s) of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
           }
       }
       return output;
    }
    ```
    <span data-ttu-id="605de-255">La méthode **GetFolderPath** renvoie le chemin d’accès au dossier vers lequel pointe le jeu de données et la méthode **GetFileName** renvoie le nom de l’objet blob/fichier vers lequel pointe le jeu de données.</span><span class="sxs-lookup"><span data-stu-id="605de-255">The **GetFolderPath** method returns the path to the folder that the dataset points to and the **GetFileName** method returns the name of the blob/file that the dataset points to.</span></span>

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    <span data-ttu-id="605de-256">La méthode **Calculate** calcule le nombre d’instances du mot-clé **Microsoft** dans les fichiers d’entrée (objets blob du dossier).</span><span class="sxs-lookup"><span data-stu-id="605de-256">The **Calculate** method calculates the number of instances of keyword **Microsoft** in the input files (blobs in the folder).</span></span> <span data-ttu-id="605de-257">Le terme de recherche (« Microsoft ») est codé en dur dans le code.</span><span class="sxs-lookup"><span data-stu-id="605de-257">The search term (“Microsoft”) is hard-coded in the code.</span></span>

1. <span data-ttu-id="605de-258">Compilez le projet.</span><span class="sxs-lookup"><span data-stu-id="605de-258">Compile the project.</span></span> <span data-ttu-id="605de-259">Cliquez sur l’option **Générer** du menu, puis sur **Générer la solution**.</span><span class="sxs-lookup"><span data-stu-id="605de-259">Click **Build** from the menu and click **Build Solution**.</span></span>
2. <span data-ttu-id="605de-260">Lancez **l’Explorateur Windows** et accédez au dossier **bin\\debug** ou **bin\\release** (selon le type de build).</span><span class="sxs-lookup"><span data-stu-id="605de-260">Launch **Windows Explorer**, and navigate to **bin\\debug** or **bin\\release** folder depending on the type of build.</span></span>
3. <span data-ttu-id="605de-261">Créez un fichier zip **MyDotNetActivity.zip** contenant tous les fichiers binaires dans le dossier **\\bin\\Debug**.</span><span class="sxs-lookup"><span data-stu-id="605de-261">Create a zip file **MyDotNetActivity.zip** that contains all the binaries in the **\\bin\\Debug** folder.</span></span> <span data-ttu-id="605de-262">Vous pouvez également inclure le fichier MyDotNetActivity.**pdb** afin d’obtenir des détails supplémentaires, tels que le numéro de ligne du code source à l’origine du problème en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="605de-262">You may want to include the MyDotNetActivity.**pdb** file so that you get additional details such as line number in the source code that caused the issue when a failure occurs.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. <span data-ttu-id="605de-263">Chargez le fichier **MyDotNetActivity.zip** en tant qu’objet blob dans le conteneur d’objets blob `customactivitycontainer` du Stockage Blob Azure qu’utilise le service lié **StorageLinkedService** dans **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="605de-263">Upload **MyDotNetActivity.zip** as a blob to the blob container: `customactivitycontainer` in the Azure blob storage that the **StorageLinkedService** linked service in the **ADFTutorialDataFactory** uses.</span></span> <span data-ttu-id="605de-264">S’il n’existe pas déjà, créez le conteneur d’objets blob `customactivitycontainer`.</span><span class="sxs-lookup"><span data-stu-id="605de-264">Create the blob container `customactivitycontainer` if it does not already exist.</span></span>

#### <a name="execute-method"></a><span data-ttu-id="605de-265">Méthode Execute</span><span class="sxs-lookup"><span data-stu-id="605de-265">Execute method</span></span>
<span data-ttu-id="605de-266">Cette section fournit des informations et remarques supplémentaires concernant le code contenu dans la méthode Execute.</span><span class="sxs-lookup"><span data-stu-id="605de-266">This section provides more details and notes about the code in the Execute method.</span></span>

1. <span data-ttu-id="605de-267">Les membres nécessaires pour l’itération dans la collection d’entrée se trouvent dans l’espace de noms [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) .</span><span class="sxs-lookup"><span data-stu-id="605de-267">The members for iterating through the input collection are found in the [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span></span> <span data-ttu-id="605de-268">L’itération dans la collection d’objets blob requiert d’utiliser la classe **BlobContinuationToken** .</span><span class="sxs-lookup"><span data-stu-id="605de-268">Iterating through the blob collection requires using the **BlobContinuationToken** class.</span></span> <span data-ttu-id="605de-269">Vous devez utiliser une boucle do-while en utilisant le jeton pour sortir de la boucle.</span><span class="sxs-lookup"><span data-stu-id="605de-269">In essence, you must use a do-while loop with the token as the mechanism for exiting the loop.</span></span> <span data-ttu-id="605de-270">Pour plus d’informations, voir [Utilisation du stockage d’objets blob à partir de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="605de-270">For more information, see [How to use Blob storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="605de-271">Une boucle de base est illustrée ici :</span><span class="sxs-lookup"><span data-stu-id="605de-271">A basic loop is shown here:</span></span>

    ```csharp
    // Initialize the continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get the list of input blobs from the input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   <span data-ttu-id="605de-272">Pour plus de détails, voir la documentation sur la méthode [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) .</span><span class="sxs-lookup"><span data-stu-id="605de-272">See the documentation for the [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method for details.</span></span>
2. <span data-ttu-id="605de-273">Le code permettant de parcourir l’ensemble d’objets blob s’inscrit logiquement dans la boucle do-while.</span><span class="sxs-lookup"><span data-stu-id="605de-273">The code for working through the set of blobs logically goes within the do-while loop.</span></span> <span data-ttu-id="605de-274">Dans la méthode **Execute**, la boucle do-while transmet la liste d’objets blob à une méthode nommée **Calculate**.</span><span class="sxs-lookup"><span data-stu-id="605de-274">In the **Execute** method, the do-while loop passes the list of blobs to a method named **Calculate**.</span></span> <span data-ttu-id="605de-275">La méthode renvoie une variable de chaîne nommée **output** , qui correspond au résultat de l’itération dans tous les objets blob du segment.</span><span class="sxs-lookup"><span data-stu-id="605de-275">The method returns a string variable named **output** that is the result of having iterated through all the blobs in the segment.</span></span>

   <span data-ttu-id="605de-276">Elle retourne le nombre d’occurrences du terme de recherche (**Microsoft**) dans l’objet blob transmis à la méthode **Calculate**.</span><span class="sxs-lookup"><span data-stu-id="605de-276">It returns the number of occurrences of the search term (**Microsoft**) in the blob passed to the **Calculate** method.</span></span>

    ```csharp
    output += string.Format("{0} occurrences of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. <span data-ttu-id="605de-277">Une fois l’exécution de la méthode **Calculate** terminée, vous devez écrire le résultat dans un nouvel objet blob.</span><span class="sxs-lookup"><span data-stu-id="605de-277">Once the **Calculate** method has done the work, it must be written to a new blob.</span></span> <span data-ttu-id="605de-278">Par conséquent, pour chaque ensemble d’objets blob traité, un nouvel objet blob peut être écrit avec les résultats correspondants.</span><span class="sxs-lookup"><span data-stu-id="605de-278">So for every set of blobs processed, a new blob can be written with the results.</span></span> <span data-ttu-id="605de-279">Pour écrire dans un nouvel objet blob, commencez par rechercher le jeu de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="605de-279">To write to a new blob, first find the output dataset.</span></span>

    ```csharp
    // Get the output dataset using the name of the dataset matched to a name in the Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. <span data-ttu-id="605de-280">Le code appelle également une méthode d’assistance, **GetFolderPath** , pour récupérer le chemin d’accès au dossier (nom du conteneur de stockage).</span><span class="sxs-lookup"><span data-stu-id="605de-280">The code also calls a helper method: **GetFolderPath** to retrieve the folder path (the storage container name).</span></span>

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   <span data-ttu-id="605de-281">La méthode **GetFolderPath** effectue un cast de l’objet DataSet dans un AzureBlobDataSet, qui comporte une propriété nommée FolderPath.</span><span class="sxs-lookup"><span data-stu-id="605de-281">The **GetFolderPath** casts the DataSet object to an AzureBlobDataSet, which has a property named FolderPath.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. <span data-ttu-id="605de-282">Le code appelle la méthode **GetFileName** pour récupérer le nom du fichier (nom de l’objet blob).</span><span class="sxs-lookup"><span data-stu-id="605de-282">The code calls the **GetFileName** method to retrieve the file name (blob name).</span></span> <span data-ttu-id="605de-283">Le code est similaire au code présenté ci-dessus pour obtenir le chemin d’accès au dossier.</span><span class="sxs-lookup"><span data-stu-id="605de-283">The code is similar to the above code to get the folder path.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. <span data-ttu-id="605de-284">Le nom du fichier est écrit grâce à la création d’un objet URI.</span><span class="sxs-lookup"><span data-stu-id="605de-284">The name of the file is written by creating a URI object.</span></span> <span data-ttu-id="605de-285">Le constructeur d’URI utilise la propriété **BlobEndpoint** pour renvoyer le nom du conteneur.</span><span class="sxs-lookup"><span data-stu-id="605de-285">The URI constructor uses the **BlobEndpoint** property to return the container name.</span></span> <span data-ttu-id="605de-286">Le nom de fichier et le chemin du dossier sont ajoutés pour construire l’URI de l’objet blob de sortie.</span><span class="sxs-lookup"><span data-stu-id="605de-286">The folder path and file name are added to construct the output blob URI.</span></span>  

    ```csharp
    // Write the name of the file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. <span data-ttu-id="605de-287">Le nom du fichier ayant été écrit, vous pouvez à présent écrire la chaîne de sortie de la méthode **Calculate** dans un nouvel objet blob :</span><span class="sxs-lookup"><span data-stu-id="605de-287">The name of the file has been written and now you can write the output string from the **Calculate** method to a new blob:</span></span>

    ```csharp
    // Create a blob and upload the output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} to the output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-the-data-factory"></a><span data-ttu-id="605de-288">Création de la fabrique de données</span><span class="sxs-lookup"><span data-stu-id="605de-288">Create the data factory</span></span>
<span data-ttu-id="605de-289">Dans la section [Création de l’activité personnalisée](#create-the-custom-activity) , vous avez créé une activité personnalisée et chargé le fichier zip contenant les fichiers binaires et le fichier PDB dans un conteneur d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="605de-289">In the [Create the custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded the zip file with binaries and the PDB file to an Azure blob container.</span></span> <span data-ttu-id="605de-290">Dans cette section, vous allez créer une **fabrique de données** Azure avec un **pipeline** qui utilise **l’activité personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="605de-290">In this section, you create an Azure **data factory** with a **pipeline** that uses the **custom activity**.</span></span>

<span data-ttu-id="605de-291">Le jeu de données d’entrée de l’activité personnalisée représente les objets blob (fichiers) contenus dans le dossier d’entrée (`mycontainer\\inputfolder`) du stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="605de-291">The input dataset for the custom activity represents the blobs (files) in the input folder (`mycontainer\\inputfolder`) in blob storage.</span></span> <span data-ttu-id="605de-292">Le jeu de données de sortie de l’activité représente les objets blob de sortie contenus dans le dossier de sortie (`mycontainer\\outputfolder`) du stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="605de-292">The output dataset for the activity represents the output blobs in the output folder (`mycontainer\\outputfolder`) in blob storage.</span></span>

<span data-ttu-id="605de-293">Déposez un ou plusieurs fichiers dans les dossiers d’entrée :</span><span class="sxs-lookup"><span data-stu-id="605de-293">Drop one or more files in the input folders:</span></span>

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

<span data-ttu-id="605de-294">Par exemple, déposez un fichier (file.txt) avec le contenu suivant dans chacun des dossiers.</span><span class="sxs-lookup"><span data-stu-id="605de-294">For example, drop one file (file.txt) with the following content into each of the folders.</span></span>

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="605de-295">Le dossier d’entrée correspond à une tranche dans Azure Data Factory, même s’il contient plusieurs fichiers.</span><span class="sxs-lookup"><span data-stu-id="605de-295">Each input folder corresponds to a slice in Azure Data Factory even if the folder has 2 or more files.</span></span> <span data-ttu-id="605de-296">Lorsque chaque tranche est traitée par le pipeline, l’activité personnalisée effectue une itération dans tous les objets blob du dossier d’entrée pour la tranche en question.</span><span class="sxs-lookup"><span data-stu-id="605de-296">When each slice is processed by the pipeline, the custom activity iterates through all the blobs in the input folder for that slice.</span></span>

<span data-ttu-id="605de-297">Vous voyez cinq fichiers de sortie avec le même contenu.</span><span class="sxs-lookup"><span data-stu-id="605de-297">You see five output files with the same content.</span></span> <span data-ttu-id="605de-298">Par exemple, le fichier de sortie résultant du traitement du fichier figurant dans le dossier 2015-11-16-00 a le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="605de-298">For example, the output file from processing the file in the 2015-11-16-00 folder has the following content:</span></span>

```
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
```

<span data-ttu-id="605de-299">Si vous déposez plusieurs fichiers (file.txt, file2.txt, file3.txt) ayant le même contenu dans le dossier d’entrée, le contenu suivant apparaît dans le fichier de sortie.</span><span class="sxs-lookup"><span data-stu-id="605de-299">If you drop multiple files (file.txt, file2.txt, file3.txt) with the same content to the input folder, you see the following content in the output file.</span></span> <span data-ttu-id="605de-300">Dans cet exemple, chaque dossier (2015-11-16-00, etc.) correspond à une tranche, même si le dossier contient plusieurs fichiers d’entrée.</span><span class="sxs-lookup"><span data-stu-id="605de-300">Each folder (2015-11-16-00, etc.) corresponds to a slice in this sample even though the folder has multiple input files.</span></span>

```csharp
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file3.txt.
```

<span data-ttu-id="605de-301">Le fichier de sortie comprend désormais trois lignes, une par fichier d’entrée (objet blob) dans le dossier associé à la tranche (2015-11-16-00).</span><span class="sxs-lookup"><span data-stu-id="605de-301">The output file has three lines now, one for each input file (blob) in the folder associated with the slice (2015-11-16-00).</span></span>

<span data-ttu-id="605de-302">Une tâche est créée pour chaque exécution d’activité.</span><span class="sxs-lookup"><span data-stu-id="605de-302">A task is created for each activity run.</span></span> <span data-ttu-id="605de-303">Dans cet exemple, le pipeline ne contient qu’une seule activité.</span><span class="sxs-lookup"><span data-stu-id="605de-303">In this sample, there is only one activity in the pipeline.</span></span> <span data-ttu-id="605de-304">Quand le pipeline traite une tranche, l’activité personnalisée s’exécute sur Azure Batch pour traiter la tranche.</span><span class="sxs-lookup"><span data-stu-id="605de-304">When a slice is processed by the pipeline, the custom activity runs on Azure Batch to process the slice.</span></span> <span data-ttu-id="605de-305">Étant donné qu’il y a cinq tranches (chacune pouvant comporter plusieurs objets blob ou fichiers), cinq tâches sont créées dans Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="605de-305">Since there are five slices (each slice can have multiple blobs or file), there are five tasks created in Azure Batch.</span></span> <span data-ttu-id="605de-306">Quand une tâche s’exécute sur Batch, c’est en fait l’activité personnalisée qui s’exécute.</span><span class="sxs-lookup"><span data-stu-id="605de-306">When a task runs on Batch, it is actually the custom activity that is running.</span></span>

<span data-ttu-id="605de-307">La procédure pas à pas suivante fournit des détails supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="605de-307">The following walkthrough provides additional details.</span></span>

#### <a name="step-1-create-the-data-factory"></a><span data-ttu-id="605de-308">Étape 1 : Créer la fabrique de données</span><span class="sxs-lookup"><span data-stu-id="605de-308">Step 1: Create the data factory</span></span>
1. <span data-ttu-id="605de-309">Une fois connecté au [portail Azure](https://portal.azure.com/), procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="605de-309">After logging in to the [Azure portal](https://portal.azure.com/), do the following steps:</span></span>

   1. <span data-ttu-id="605de-310">Cliquez sur **NOUVEAU** dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="605de-310">Click **NEW** on the left menu.</span></span>
   2. <span data-ttu-id="605de-311">Dans le panneau **Nouveau**, cliquez sur **Données et analyses**.</span><span class="sxs-lookup"><span data-stu-id="605de-311">Click **Data + Analytics** in the **New** blade.</span></span>
   3. <span data-ttu-id="605de-312">Cliquez sur **Data Factory** dans le panneau **Analyse des données**.</span><span class="sxs-lookup"><span data-stu-id="605de-312">Click **Data Factory** on the **Data analytics** blade.</span></span>
2. <span data-ttu-id="605de-313">Dans le panneau **Nouvelle fabrique de données**, spécifiez le nom **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="605de-313">In the **New data factory** blade, enter **CustomActivityFactory** for the Name.</span></span> <span data-ttu-id="605de-314">Le nom de la fabrique de données Azure doit être un nom global unique.</span><span class="sxs-lookup"><span data-stu-id="605de-314">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="605de-315">Si l’erreur **Data factory name “CustomActivityFactory” is not available** (Le nom de la fabrique de données « CustomActivityFactory » n’est pas disponible) s’affiche, changez le nom de la fabrique de données (par exemple, **votrenomCustomActivityFactory**), puis tentez de la recréer.</span><span class="sxs-lookup"><span data-stu-id="605de-315">If you receive the error: **Data factory name “CustomActivityFactory” is not available**, change the name of the data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>
3. <span data-ttu-id="605de-316">Cliquez sur **NOM DU GROUPE DE RESSOURCES**pour sélectionner un groupe de ressources existant, ou créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="605de-316">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="605de-317">Veillez à utiliser l’abonnement et la région correspondant à ceux dans lesquels vous voulez créer la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="605de-317">Verify that you are using the correct subscription and region where you want the data factory to be created.</span></span>
5. <span data-ttu-id="605de-318">Cliquez sur **Créer** dans le panneau **Nouvelle fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="605de-318">Click **Create** on the **New data factory** blade.</span></span>
6. <span data-ttu-id="605de-319">La fabrique de données apparaît comme étant en cours de création dans le **Tableau de bord** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="605de-319">You see the data factory being created in the **Dashboard** of the Azure portal.</span></span>
7. <span data-ttu-id="605de-320">Une fois la fabrique de données créée, la page correspondante s’affiche et indique son contenu.</span><span class="sxs-lookup"><span data-stu-id="605de-320">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a><span data-ttu-id="605de-321">Étape 2 : Créer des services liés</span><span class="sxs-lookup"><span data-stu-id="605de-321">Step 2: Create linked services</span></span>
<span data-ttu-id="605de-322">Les services liés se chargent de lier des magasins de données ou des services de calcul à une fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="605de-322">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="605de-323">Dans cette étape, vous allez lier vos comptes **Stockage Azure** et **Azure Batch** à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="605de-323">In this step, you link your **Azure Storage** account and **Azure Batch** account to your data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="605de-324">Créer le service lié Azure Storage</span><span class="sxs-lookup"><span data-stu-id="605de-324">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="605de-325">Cliquez sur la vignette **Créer et déployer** dans le panneau **DATA FACTORY** de **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="605de-325">Click the **Author and deploy** tile on the **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="605de-326">Data Factory Editor s’affiche.</span><span class="sxs-lookup"><span data-stu-id="605de-326">You see the Data Factory Editor.</span></span>
2. <span data-ttu-id="605de-327">Cliquez sur **Nouvelle banque de données** dans la barre de commandes et choisissez **Stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="605de-327">Click **New data store** on the command bar and choose **Azure storage.**</span></span> <span data-ttu-id="605de-328">Le script JSON de création d’un service lié Microsoft Azure Storage doit apparaître dans l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="605de-328">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. <span data-ttu-id="605de-329">Remplacez **account name** par le nom de votre compte de stockage Azure et **account key** par sa clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="605de-329">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="605de-330">Pour savoir comment obtenir votre clé d’accès de stockage, voir [Affichage, copie et régénération de clés d’accès de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="605de-330">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

4. <span data-ttu-id="605de-331">Cliquez sur l’option **Déployer** de la barre de commandes pour déployer le service lié.</span><span class="sxs-lookup"><span data-stu-id="605de-331">Click **Deploy** on the command bar to deploy the linked service.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="605de-332">Créer un service lié Azure Batch</span><span class="sxs-lookup"><span data-stu-id="605de-332">Create Azure Batch linked service</span></span>
<span data-ttu-id="605de-333">Au cours de cette étape, vous créez un service lié pour votre compte **Azure Batch**, qui est utilisé pour exécuter l’activité personnalisée Data Factory.</span><span class="sxs-lookup"><span data-stu-id="605de-333">In this step, you create a linked service for your **Azure Batch** account that is used to run the Data Factory custom activity.</span></span>

1. <span data-ttu-id="605de-334">Cliquez sur **Nouveau calcul** dans la barre de commandes et choisissez **Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="605de-334">Click **New compute** on the command bar and choose **Azure Batch.**</span></span> <span data-ttu-id="605de-335">Le script JSON pour la création d’un service lié Azure Batch doit apparaître dans l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="605de-335">You should see the JSON script for creating an Azure Batch linked service in the editor.</span></span>
2. <span data-ttu-id="605de-336">Dans le script JSON :</span><span class="sxs-lookup"><span data-stu-id="605de-336">In the JSON script:</span></span>

   1. <span data-ttu-id="605de-337">Remplacez **nom de compte** par le nom de votre compte Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="605de-337">Replace **account name** with the name of your Azure Batch account.</span></span>
   2. <span data-ttu-id="605de-338">Remplacez **clé d’accès** avec la clé d’accès du compte Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="605de-338">Replace **access key** with the access key of the Azure Batch account.</span></span>
   3. <span data-ttu-id="605de-339">Entrez l’ID du pool pour la propriété **poolName****.**</span><span class="sxs-lookup"><span data-stu-id="605de-339">Enter the ID of the pool for the **poolName** property**.**</span></span> <span data-ttu-id="605de-340">Pour cette propriété, vous pouvez spécifier le nom de pool ou l’ID de pool.</span><span class="sxs-lookup"><span data-stu-id="605de-340">For this property, you can specify either pool name or pool ID.</span></span>
   4. <span data-ttu-id="605de-341">Entrez l’URI du lot pour la propriété JSON **batchUri** .</span><span class="sxs-lookup"><span data-stu-id="605de-341">Enter the batch URI for the **batchUri** JSON property.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="605de-342">**L’URL** figurant dans le **panneau du compte Azure Batch** est au format suivant : \<nomducompte\>.\<région\>.batch.azure.com. Pour la propriété **batchUri** dans le fichier JSON, vous devez **supprimer « nomducompte ».**</span><span class="sxs-lookup"><span data-stu-id="605de-342">The **URL** from the **Azure Batch account blade** is in the following format: \<accountname\>.\<region\>.batch.azure.com. For the **batchUri** property in the JSON, you need to **remove "accountname."**</span></span> <span data-ttu-id="605de-343">de l’URL.</span><span class="sxs-lookup"><span data-stu-id="605de-343">from the URL.</span></span> <span data-ttu-id="605de-344">Exemple : `"batchUri": "https://eastus.batch.azure.com"`.</span><span class="sxs-lookup"><span data-stu-id="605de-344">Example: `"batchUri": "https://eastus.batch.azure.com"`.</span></span>
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      <span data-ttu-id="605de-345">Pour la propriété **poolName** , vous pouvez également spécifier l’ID du pool au lieu du nom du pool.</span><span class="sxs-lookup"><span data-stu-id="605de-345">For the **poolName** property, you can also specify the ID of the pool instead of the name of the pool.</span></span>

      > [!NOTE]
      > <span data-ttu-id="605de-346">Le service Data Factory ne prend pas en charge l’option à la demande pour Azure Batch contrairement à HDInsight.</span><span class="sxs-lookup"><span data-stu-id="605de-346">The Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="605de-347">Vous pouvez uniquement utiliser votre propre pool Azure Batch dans une fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="605de-347">You can only use your own Azure Batch pool in an Azure data factory.</span></span>
      >
      >
   5. <span data-ttu-id="605de-348">Spécifiez **StorageLinkedService** for the **StorageLinkedService** .</span><span class="sxs-lookup"><span data-stu-id="605de-348">Specify **StorageLinkedService** for the **linkedServiceName** property.</span></span> <span data-ttu-id="605de-349">Vous avez créé ce service lié à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="605de-349">You created this linked service in the previous step.</span></span> <span data-ttu-id="605de-350">Ce stockage est utilisé en tant que zone de transit pour les fichiers et les journaux.</span><span class="sxs-lookup"><span data-stu-id="605de-350">This storage is used as a staging area for files and logs.</span></span>
3. <span data-ttu-id="605de-351">Cliquez sur l’option **Déployer** de la barre de commandes pour déployer le service lié.</span><span class="sxs-lookup"><span data-stu-id="605de-351">Click **Deploy** on the command bar to deploy the linked service.</span></span>

#### <a name="step-3-create-datasets"></a><span data-ttu-id="605de-352">Étape 3 : Créer les jeux de données</span><span class="sxs-lookup"><span data-stu-id="605de-352">Step 3: Create datasets</span></span>
<span data-ttu-id="605de-353">Dans cette étape, vous allez créer des jeux de données pour représenter les données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="605de-353">In this step, you create datasets to represent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="605de-354">Créer le jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="605de-354">Create input dataset</span></span>
1. <span data-ttu-id="605de-355">Dans **l’éditeur** de Data Factory, cliquez sur le bouton **Nouveau jeu de données** de la barre d’outils et sélectionnez **Stockage Blob Azure** dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="605de-355">In the **Editor** for the Data Factory, click **New dataset** button on the toolbar and click **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="605de-356">Remplacez le script JSON affiché dans le volet droit par l’extrait de code JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="605de-356">Replace the JSON in the right pane with the following JSON snippet:</span></span>

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           },
           "external": true,
           "policy": {}
       }
    }
    ```

    <span data-ttu-id="605de-357">Plus loin dans cette procédure pas à pas, vous allez créer un pipeline associé à l’heure de début 2015-11-16T00:00:00Z et à l’heure de fin 2015-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="605de-357">You create a pipeline later in this walkthrough with start time: 2015-11-16T00:00:00Z and end time: 2015-11-16T05:00:00Z.</span></span> <span data-ttu-id="605de-358">Ce pipeline est planifié pour produire des données **toutes les heures**, ce qui signifie que l’on obtient 5 tranches d’entrée/sortie (comprises entre **00**: 00:00 et \>**05**: 00:00).</span><span class="sxs-lookup"><span data-stu-id="605de-358">It is scheduled to produce data **hourly**, so there are 5 input/output slices (between **00**:00:00 -\> **05**:00:00).</span></span>

    <span data-ttu-id="605de-359">Les paramètres **frequency** et **interval** du jeu de données d’entrée sont respectivement définis sur **Hour** et sur **1**, ce qui signifie que la tranche d’entrée est disponible toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="605de-359">The **frequency** and **interval** for the input dataset is set to **Hour** and **1**, which means that the input slice is available hourly.</span></span>

    <span data-ttu-id="605de-360">Voici les heures de début de chaque tranche, représentées par la variable système **SliceStart** dans l’extrait de code JSON ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="605de-360">Here are the start times for each slice, which is represented by **SliceStart** system variable in the above JSON snippet.</span></span>

    | <span data-ttu-id="605de-361">**Tranche**</span><span class="sxs-lookup"><span data-stu-id="605de-361">**Slice**</span></span> | <span data-ttu-id="605de-362">**Heure de début**</span><span class="sxs-lookup"><span data-stu-id="605de-362">**Start time**</span></span>          |
    |-----------|-------------------------|
    | <span data-ttu-id="605de-363">1</span><span class="sxs-lookup"><span data-stu-id="605de-363">1</span></span>         | <span data-ttu-id="605de-364">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="605de-364">2015-11-16T**00**:00:00</span></span> |
    | <span data-ttu-id="605de-365">2</span><span class="sxs-lookup"><span data-stu-id="605de-365">2</span></span>         | <span data-ttu-id="605de-366">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="605de-366">2015-11-16T**01**:00:00</span></span> |
    | <span data-ttu-id="605de-367">3</span><span class="sxs-lookup"><span data-stu-id="605de-367">3</span></span>         | <span data-ttu-id="605de-368">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="605de-368">2015-11-16T**02**:00:00</span></span> |
    | <span data-ttu-id="605de-369">4</span><span class="sxs-lookup"><span data-stu-id="605de-369">4</span></span>         | <span data-ttu-id="605de-370">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="605de-370">2015-11-16T**03**:00:00</span></span> |
    | <span data-ttu-id="605de-371">5</span><span class="sxs-lookup"><span data-stu-id="605de-371">5</span></span>         | <span data-ttu-id="605de-372">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="605de-372">2015-11-16T**04**:00:00</span></span> |

    <span data-ttu-id="605de-373">La valeur **folderPath** est calculée à l’aide de la partie année, mois, jour et heure de l’heure de début de la tranche (**SliceStart**).</span><span class="sxs-lookup"><span data-stu-id="605de-373">The **folderPath** is calculated by using the year, month, day, and hour part of the slice start time (**SliceStart**).</span></span> <span data-ttu-id="605de-374">Par conséquent, voici comment un dossier d’entrée est mappé à une tranche.</span><span class="sxs-lookup"><span data-stu-id="605de-374">Therefore, here is how an input folder is mapped to a slice.</span></span>

    | <span data-ttu-id="605de-375">**Tranche**</span><span class="sxs-lookup"><span data-stu-id="605de-375">**Slice**</span></span> | <span data-ttu-id="605de-376">**Heure de début**</span><span class="sxs-lookup"><span data-stu-id="605de-376">**Start time**</span></span>          | <span data-ttu-id="605de-377">**Dossier d’entrée**</span><span class="sxs-lookup"><span data-stu-id="605de-377">**Input folder**</span></span>  |
    |-----------|-------------------------|-------------------|
    | <span data-ttu-id="605de-378">1</span><span class="sxs-lookup"><span data-stu-id="605de-378">1</span></span>         | <span data-ttu-id="605de-379">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="605de-379">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="605de-380">2015-11-16-**00**</span><span class="sxs-lookup"><span data-stu-id="605de-380">2015-11-16-**00**</span></span> |
    | <span data-ttu-id="605de-381">2</span><span class="sxs-lookup"><span data-stu-id="605de-381">2</span></span>         | <span data-ttu-id="605de-382">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="605de-382">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="605de-383">2015-11-16-**01**</span><span class="sxs-lookup"><span data-stu-id="605de-383">2015-11-16-**01**</span></span> |
    | <span data-ttu-id="605de-384">3</span><span class="sxs-lookup"><span data-stu-id="605de-384">3</span></span>         | <span data-ttu-id="605de-385">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="605de-385">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="605de-386">2015-11-16-**02**</span><span class="sxs-lookup"><span data-stu-id="605de-386">2015-11-16-**02**</span></span> |
    | <span data-ttu-id="605de-387">4</span><span class="sxs-lookup"><span data-stu-id="605de-387">4</span></span>         | <span data-ttu-id="605de-388">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="605de-388">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="605de-389">2015-11-16-**03**</span><span class="sxs-lookup"><span data-stu-id="605de-389">2015-11-16-**03**</span></span> |
    | <span data-ttu-id="605de-390">5</span><span class="sxs-lookup"><span data-stu-id="605de-390">5</span></span>         | <span data-ttu-id="605de-391">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="605de-391">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="605de-392">2015-11-16-**04**</span><span class="sxs-lookup"><span data-stu-id="605de-392">2015-11-16-**04**</span></span> |

1. <span data-ttu-id="605de-393">Dans la barre d’outils, cliquez sur **Déployer** pour créer et déployer la table **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="605de-393">Click **Deploy** on the toolbar to create and deploy the **InputDataset** table.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="605de-394">Créer un jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="605de-394">Create output dataset</span></span>
<span data-ttu-id="605de-395">Au cours de cette étape, vous créez un autre jeu de données de type AzureBlob pour représenter les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="605de-395">In this step, you create another dataset of type AzureBlob to represent the output data.</span></span>

1. <span data-ttu-id="605de-396">Dans **l’éditeur** de Data Factory, cliquez sur le bouton **Nouveau jeu de données** de la barre d’outils et sélectionnez **Stockage Blob Azure** dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="605de-396">In the **Editor** for the Data Factory, click **New dataset** button on the toolbar and click **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="605de-397">Remplacez le script JSON affiché dans le volet droit par l’extrait de code JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="605de-397">Replace the JSON in the right pane with the following JSON snippet:</span></span>

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
               "partitionedBy": [
                   {
                       "name": "slice",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy-MM-dd-HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           }
       }
    }
    ```

    <span data-ttu-id="605de-398">Un objet blob/fichier de sortie est généré pour chaque tranche d’entrée.</span><span class="sxs-lookup"><span data-stu-id="605de-398">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="605de-399">Voici la procédure de nommage des fichiers de sortie pour chaque tranche.</span><span class="sxs-lookup"><span data-stu-id="605de-399">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="605de-400">Tous les fichiers de sortie sont générés dans un seul dossier de sortie : `mycontainer\\outputfolder`.</span><span class="sxs-lookup"><span data-stu-id="605de-400">All the output files are generated in one output folder: `mycontainer\\outputfolder`.</span></span>

    | <span data-ttu-id="605de-401">**Tranche**</span><span class="sxs-lookup"><span data-stu-id="605de-401">**Slice**</span></span> | <span data-ttu-id="605de-402">**Heure de début**</span><span class="sxs-lookup"><span data-stu-id="605de-402">**Start time**</span></span>          | <span data-ttu-id="605de-403">**Fichier de sortie**</span><span class="sxs-lookup"><span data-stu-id="605de-403">**Output file**</span></span>       |
    |-----------|-------------------------|-----------------------|
    | <span data-ttu-id="605de-404">1</span><span class="sxs-lookup"><span data-stu-id="605de-404">1</span></span>         | <span data-ttu-id="605de-405">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="605de-405">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="605de-406">2015-11-16-**00.txt**</span><span class="sxs-lookup"><span data-stu-id="605de-406">2015-11-16-**00.txt**</span></span> |
    | <span data-ttu-id="605de-407">2</span><span class="sxs-lookup"><span data-stu-id="605de-407">2</span></span>         | <span data-ttu-id="605de-408">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="605de-408">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="605de-409">2015-11-16-**01.txt**</span><span class="sxs-lookup"><span data-stu-id="605de-409">2015-11-16-**01.txt**</span></span> |
    | <span data-ttu-id="605de-410">3</span><span class="sxs-lookup"><span data-stu-id="605de-410">3</span></span>         | <span data-ttu-id="605de-411">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="605de-411">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="605de-412">2015-11-16-**02.txt**</span><span class="sxs-lookup"><span data-stu-id="605de-412">2015-11-16-**02.txt**</span></span> |
    | <span data-ttu-id="605de-413">4</span><span class="sxs-lookup"><span data-stu-id="605de-413">4</span></span>         | <span data-ttu-id="605de-414">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="605de-414">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="605de-415">2015-11-16-**03.txt**</span><span class="sxs-lookup"><span data-stu-id="605de-415">2015-11-16-**03.txt**</span></span> |
    | <span data-ttu-id="605de-416">5</span><span class="sxs-lookup"><span data-stu-id="605de-416">5</span></span>         | <span data-ttu-id="605de-417">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="605de-417">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="605de-418">2015-11-16-**04.txt**</span><span class="sxs-lookup"><span data-stu-id="605de-418">2015-11-16-**04.txt**</span></span> |

    <span data-ttu-id="605de-419">N’oubliez pas que tous les fichiers figurant dans un dossier d’entrée (par exemple, 2015-11-16-00) font partie d’une tranche associée à l’heure de début (2015-11-16-00).</span><span class="sxs-lookup"><span data-stu-id="605de-419">Remember that all the files in an input folder (for example: 2015-11-16-00) are part of a slice with the start time: 2015-11-16-00.</span></span> <span data-ttu-id="605de-420">Lorsque cette tranche est traitée, l’activité personnalisée parcourt chaque fichier et génère une ligne dans le fichier de sortie avec le nombre d’occurrences du terme de recherche (« Microsoft »).</span><span class="sxs-lookup"><span data-stu-id="605de-420">When this slice is processed, the custom activity scans through each file and produces a line in the output file with the number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="605de-421">Si le dossier 2015-11-16-00 contient trois fichiers, le fichier de sortie 2015-11-16-00.txt comprend trois lignes.</span><span class="sxs-lookup"><span data-stu-id="605de-421">If there are three files in the folder 2015-11-16-00, there are three lines in the output file: 2015-11-16-00.txt.</span></span>

1. <span data-ttu-id="605de-422">Dans la barre d’outils, cliquez sur **Déployer** pour créer et déployer la table **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="605de-422">Click **Deploy** on the toolbar to create and deploy the **OutputDataset**.</span></span>

#### <a name="step-4-create-and-run-the-pipeline-with-custom-activity"></a><span data-ttu-id="605de-423">Étape 4 : Créer et exécuter le pipeline avec une activité personnalisée</span><span class="sxs-lookup"><span data-stu-id="605de-423">Step 4: Create and run the pipeline with custom activity</span></span>
<span data-ttu-id="605de-424">Au cours de cette étape, vous créez un pipeline comprenant une seule activité, l’activité personnalisée que vous avez créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="605de-424">In this step, you create a pipeline with one activity, the custom activity you created earlier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="605de-425">Si vous n’avez pas chargé le fichier **file.txt** dans les dossiers d’entrée du conteneur d’objets blob, veuillez le faire avant de créer le pipeline.</span><span class="sxs-lookup"><span data-stu-id="605de-425">If you haven't uploaded the **file.txt** to input folders in the blob container, do so before creating the pipeline.</span></span> <span data-ttu-id="605de-426">La propriété **isPaused** étant définie sur false dans le fichier JSON du pipeline, le pipeline s’exécute immédiatement, car la date de **début** se situe dans le passé.</span><span class="sxs-lookup"><span data-stu-id="605de-426">The **isPaused** property is set to false in the pipeline JSON, so the pipeline runs immediately as the **start** date is in the past.</span></span>
>
>

1. <span data-ttu-id="605de-427">Dans Data Factory Editor, cliquez sur **Nouveau pipeline** dans la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="605de-427">In the Data Factory Editor, click **New pipeline** on the command bar.</span></span> <span data-ttu-id="605de-428">Si vous ne voyez pas apparaître la commande, cliquez sur **... (points de suspension)** pour l’afficher.</span><span class="sxs-lookup"><span data-stu-id="605de-428">If you do not see the command, click **... (Ellipsis)** to see it.</span></span>
2. <span data-ttu-id="605de-429">Remplacez le script JSON affiché dans le volet droit par le script JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="605de-429">Replace the JSON in the right pane with the following JSON script:</span></span>

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   <span data-ttu-id="605de-430">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="605de-430">Note the following points:</span></span>

   * <span data-ttu-id="605de-431">Le pipeline ne comprend qu’une seule activité du type **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="605de-431">There is only one activity in the pipeline and that is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="605de-432">Le paramètre **AssemblyName** est défini sur le nom de la DLL **MyDotNetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="605de-432">**AssemblyName** is set to the name of the DLL: **MyDotNetActivity.dll**.</span></span>
   * <span data-ttu-id="605de-433">Le paramètre **EntryPoint** est défini sur **MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="605de-433">**EntryPoint** is set to **MyDotNetActivityNS.MyDotNetActivity**.</span></span> <span data-ttu-id="605de-434">Il s’agit essentiellement de \<namespace\>.\<classname\> dans votre code.</span><span class="sxs-lookup"><span data-stu-id="605de-434">It is basically \<namespace\>.\<classname\> in your code.</span></span>
   * <span data-ttu-id="605de-435">**PackageLinkedService** est défini sur **StorageLinkedService**, qui pointe vers le stockage d’objets blob contenant le fichier .zip de l’activité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="605de-435">**PackageLinkedService** is set to **StorageLinkedService** that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="605de-436">Si vous utilisez des comptes de stockage différents pour les fichiers d’entrée/sortie et le fichier zip de l’activité personnalisée, vous devez créer un autre service lié Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="605de-436">If you are using different Azure Storage accounts for input/output files and the custom activity zip file, you have to create another Azure Storage linked service.</span></span> <span data-ttu-id="605de-437">Cet article suppose que vous utilisez le même compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="605de-437">This article assumes that you are using the same Azure Storage account.</span></span>
   * <span data-ttu-id="605de-438">Le paramètre **PackageFile** est défini sur **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="605de-438">**PackageFile** is set to **customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="605de-439">Il est au format : \<conteneur_du_zip\>/\<nom_du_zip.zip\>.</span><span class="sxs-lookup"><span data-stu-id="605de-439">It is in the format: \<containerforthezip\>/\<nameofthezip.zip\>.</span></span>
   * <span data-ttu-id="605de-440">L’activité personnalisée utilise **InputDataset** comme entrée et **OutputDataset** comme sortie.</span><span class="sxs-lookup"><span data-stu-id="605de-440">The custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="605de-441">La propriété **linkedServiceName** de l’activité personnalisée pointe vers **AzureBatchLinkedService**, ce qui indique à Azure Data Factory que l’activité personnalisée doit s’exécuter sur Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="605de-441">The **linkedServiceName** property of the custom activity points to the **AzureBatchLinkedService**, which tells Azure Data Factory that the custom activity needs to run on Azure Batch.</span></span>
   * <span data-ttu-id="605de-442">Le paramètre **concurrency** est important.</span><span class="sxs-lookup"><span data-stu-id="605de-442">The **concurrency** setting is important.</span></span> <span data-ttu-id="605de-443">Si vous utilisez la valeur par défaut, 1, même si vous avez plusieurs nœuds de calcul dans le pool Azure Batch, les tranches sont traitées successivement.</span><span class="sxs-lookup"><span data-stu-id="605de-443">If you use the default value, which is 1, even if you have 2 or more compute nodes in the Azure Batch pool, the slices are processed one after another.</span></span> <span data-ttu-id="605de-444">Par conséquent, vous ne profitez pas de la capacité de traitement en parallèle d’Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="605de-444">Therefore, you are not taking advantage of the parallel processing capability of Azure Batch.</span></span> <span data-ttu-id="605de-445">Si vous définissez **concurrency** sur une valeur plus élevée, par exemple 2, deux tranches (correspondant à deux tâches dans Azure Batch) peuvent être traitées simultanément, auquel cas les deux machines virtuelles du pool Azure Batch sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="605de-445">If you set **concurrency** to a higher value, say 2, it means that two slices (corresponds to two tasks in Azure Batch) can be processed at the same time, in which case, both the VMs in the Azure Batch pool are utilized.</span></span> <span data-ttu-id="605de-446">Vous devez par conséquent définir la propriété concurrency de façon appropriée.</span><span class="sxs-lookup"><span data-stu-id="605de-446">Therefore, set the concurrency property appropriately.</span></span>
   * <span data-ttu-id="605de-447">Par défaut, une seule tâche (tranche) est exécutée sur une machine virtuelle à un moment donné.</span><span class="sxs-lookup"><span data-stu-id="605de-447">Only one task (slice) is executed on a VM at any point by default.</span></span> <span data-ttu-id="605de-448">La raison est que, par défaut, le paramètre **Maximum tasks per VM** (Nombre maximal de tâches par machine virtuelle) est défini sur 1 pour un pool Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="605de-448">The reason is that, by default, the **Maximum tasks per VM** is set to 1 for an Azure Batch pool.</span></span> <span data-ttu-id="605de-449">En rapport avec les conditions préalables, vous avez créé un pool pour lequel cette propriété est définie sur 2, de sorte que deux tranches Data Factory peuvent s’exécuter simultanément sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="605de-449">As part of prerequisites, you created a pool with this property set to 2, so two Data Factory slices can be running on a VM at the same time.</span></span>

    -   <span data-ttu-id="605de-450">**isPaused** est définie sur false.</span><span class="sxs-lookup"><span data-stu-id="605de-450">**isPaused** property is set to false by default.</span></span> <span data-ttu-id="605de-451">Le pipeline s’exécute immédiatement dans cet exemple car les tranches débutent à une date antérieure.</span><span class="sxs-lookup"><span data-stu-id="605de-451">The pipeline runs immediately in this example because the slices start in the past.</span></span> <span data-ttu-id="605de-452">Vous pouvez définir cette propriété sur true pour suspendre le pipeline et lui réaffecter la valeur false pour reprendre l’exécution.</span><span class="sxs-lookup"><span data-stu-id="605de-452">You can set this property to true to pause the pipeline and set it back to false to restart.</span></span>

    -   <span data-ttu-id="605de-453">Cinq heures séparent les heures de **début** et de **fin**, et les tranches sont produites toutes les heures, ce qui signifie que cinq tranches sont produites par le pipeline.</span><span class="sxs-lookup"><span data-stu-id="605de-453">The **start** time and **end** times are five hours apart and slices are produced hourly, so five slices are produced by the pipeline.</span></span>

1. <span data-ttu-id="605de-454">Cliquez sur **Déployer** dans la barre de commandes pour déployer le pipeline.</span><span class="sxs-lookup"><span data-stu-id="605de-454">Click **Deploy** on the command bar to deploy the pipeline.</span></span>

#### <a name="step-5-test-the-pipeline"></a><span data-ttu-id="605de-455">Étape 5 : Tester le pipeline</span><span class="sxs-lookup"><span data-stu-id="605de-455">Step 5: Test the pipeline</span></span>
<span data-ttu-id="605de-456">Au cours de cette étape, vous testez le pipeline en déposant des fichiers dans les dossiers d’entrée.</span><span class="sxs-lookup"><span data-stu-id="605de-456">In this step, you test the pipeline by dropping files into the input folders.</span></span> <span data-ttu-id="605de-457">Commençons par tester le pipeline avec un fichier par dossier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="605de-457">Let’s start with testing the pipeline with one file per one input folder.</span></span>

1. <span data-ttu-id="605de-458">Dans le panneau Data Factory du portail Azure, cliquez sur **Diagramme**.</span><span class="sxs-lookup"><span data-stu-id="605de-458">In the Data Factory blade in the Azure portal, click **Diagram**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. <span data-ttu-id="605de-459">Dans la vue de diagramme, double-cliquez sur le jeu de données d’entrée **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="605de-459">In the diagram view, double-click input dataset: **InputDataset**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. <span data-ttu-id="605de-460">Vous devriez voir le panneau **InputDataset** avec les cinq tranches prêtes.</span><span class="sxs-lookup"><span data-stu-id="605de-460">You should see the **InputDataset** blade with all five slices ready.</span></span> <span data-ttu-id="605de-461">Notez **l’HEURE DE DÉBUT DE LA TRANCHE** et **l’HEURE DE FIN DE LA TRANCHE** pour chaque tranche.</span><span class="sxs-lookup"><span data-stu-id="605de-461">Notice the **SLICE START TIME** and **SLICE END TIME** for each slice.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. <span data-ttu-id="605de-462">Dans la **vue de diagramme**, cliquez sur **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="605de-462">In the **Diagram View**, now click **OutputDataset**.</span></span>
5. <span data-ttu-id="605de-463">Si elles ont déjà été produites, les cinq tranches de sortie doivent être à l’état Prêt.</span><span class="sxs-lookup"><span data-stu-id="605de-463">You should see that the five output slices are in the Ready state if they have already been produced.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. <span data-ttu-id="605de-464">Pour afficher les **tâches** associées aux **tranches** et voir la machine virtuelle sur laquelle chaque tranche a été exécutée, utilisez le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="605de-464">Use Azure portal to view the **tasks** associated with the **slices** and see what VM each slice ran on.</span></span> <span data-ttu-id="605de-465">Consultez la section [Intégration de Data Factory et Batch](#data-factory-and-batch-integration) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="605de-465">See [Data Factory and Batch integration](#data-factory-and-batch-integration) section for details.</span></span>
7. <span data-ttu-id="605de-466">Les fichiers de sortie devraient apparaître dans le dossier `outputfolder` de `mycontainer` dans votre Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="605de-466">You should see the output files in the `outputfolder` of `mycontainer` in your Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   <span data-ttu-id="605de-467">Vous devriez voir cinq fichiers de sortie, un par tranche d’entrée.</span><span class="sxs-lookup"><span data-stu-id="605de-467">You should see five output files, one for each input slice.</span></span> <span data-ttu-id="605de-468">Chaque fichier de sortie doit avoir contenu similaire à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="605de-468">Each of the output file should have content similar to the following output:</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
    ```
   <span data-ttu-id="605de-469">Le diagramme suivant illustre la manière dont les tranches Data Factory sont mappées à des tâches dans Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="605de-469">The following diagram illustrates how the Data Factory slices map to tasks in Azure Batch.</span></span> <span data-ttu-id="605de-470">Dans cet exemple, une tranche n’est exécutée qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="605de-470">In this example, a slice has only one run.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. <span data-ttu-id="605de-471">À présent, essayons avec plusieurs fichiers dans un dossier.</span><span class="sxs-lookup"><span data-stu-id="605de-471">Now, let’s try with multiple files in a folder.</span></span> <span data-ttu-id="605de-472">Créez des fichiers **file2.txt**, **file3.txt**, **file4.txt** et **file5.txt** ayant le même contenu que le fichier file.txt dans le dossier **2015-11-06-01**.</span><span class="sxs-lookup"><span data-stu-id="605de-472">Create files: **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with the same content as in file.txt in the folder: **2015-11-06-01**.</span></span>
9. <span data-ttu-id="605de-473">Dans le dossier de sortie, **supprimez** le fichier de sortie **2015-11-16-01.txt**.</span><span class="sxs-lookup"><span data-stu-id="605de-473">In the output folder, **delete** the output file: **2015-11-16-01.txt**.</span></span>
10. <span data-ttu-id="605de-474">À présent, dans le panneau **OutputDataset**, cliquez avec le bouton droit sur la tranche dont **l’HEURE DE DÉBUT DE LA TRANCHE** a la valeur **16/11/2015 01:00:00 AM**, puis cliquez sur **Exécuter** pour réexécuter/re-traiter la tranche.</span><span class="sxs-lookup"><span data-stu-id="605de-474">Now, in the **OutputDataset** blade, right-click the slice with **SLICE START TIME** set to **11/16/2015 01:00:00 AM**, and click **Run** to rerun/re-process the slice.</span></span> <span data-ttu-id="605de-475">À présent, la tranche contient cinq fichiers au lieu d’un seul.</span><span class="sxs-lookup"><span data-stu-id="605de-475">Now, the slice has five files instead of one file.</span></span>

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. <span data-ttu-id="605de-476">Une fois la tranche exécutée, quand son état est **Prêt**, vérifiez le contenu de son fichier de sortie (**2015-11-16-01.txt**) dans le dossier `outputfolder` de `mycontainer` dans votre stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="605de-476">After the slice runs and its status is **Ready**, verify the content in the output file for this slice (**2015-11-16-01.txt**) in the `outputfolder` of `mycontainer` in your blob storage.</span></span> <span data-ttu-id="605de-477">Il doit y avoir une ligne pour chaque fichier de la tranche.</span><span class="sxs-lookup"><span data-stu-id="605de-477">There should be a line for each file of the slice.</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> <span data-ttu-id="605de-478">Si vous n’avez pas supprimé le fichier de sortie 2015-11-16-01.txt avant d’essayer avec cinq fichiers d’entrée, vous devez voir une ligne pour l’exécution de la tranche précédente, et cinq lignes pour l’exécution de la tranche actuelle.</span><span class="sxs-lookup"><span data-stu-id="605de-478">If you did not delete the output file 2015-11-16-01.txt before trying with five input files, you see one line from the previous slice run and five lines from the current slice run.</span></span> <span data-ttu-id="605de-479">Par défaut, le contenu est ajouté au fichier de sortie s’il existe.</span><span class="sxs-lookup"><span data-stu-id="605de-479">By default, the content is appended to output file if it already exists.</span></span>
>
>

#### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="605de-480">Intégration de Data Factory et Batch</span><span class="sxs-lookup"><span data-stu-id="605de-480">Data Factory and Batch integration</span></span>
<span data-ttu-id="605de-481">Le service Data Factory crée un travail dans Azure Batch sous le nom `adf-poolname:job-xxx`.</span><span class="sxs-lookup"><span data-stu-id="605de-481">The Data Factory service creates a job in Azure Batch with the name: `adf-poolname:job-xxx`.</span></span>

![Azure Data Factory - Travaux Batch](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

<span data-ttu-id="605de-483">Une tâche dans le travail est créée pour chaque exécution d’activité d’une tranche.</span><span class="sxs-lookup"><span data-stu-id="605de-483">A task in the job is created for each activity run of a slice.</span></span> <span data-ttu-id="605de-484">Si 10 tranches sont prêtes à être traitées, 10 tâches seront créées dans le travail.</span><span class="sxs-lookup"><span data-stu-id="605de-484">If there are 10 slices ready to be processed, 10 tasks are created in the job.</span></span> <span data-ttu-id="605de-485">Plusieurs tranches peuvent être exécutées en parallèle si vous disposez de plusieurs nœuds de calcul dans le pool.</span><span class="sxs-lookup"><span data-stu-id="605de-485">You can have more than one slice running in parallel if you have multiple compute nodes in the pool.</span></span> <span data-ttu-id="605de-486">Vous pouvez également avoir plusieurs tranches exécutées sur le même nœud de calcul si le nombre maximum de tâches par nœud de calcul est défini sur une valeur supérieure à 1.</span><span class="sxs-lookup"><span data-stu-id="605de-486">If the maximum tasks per compute node is set to > 1, there can be more than one slice running on the same compute.</span></span>

<span data-ttu-id="605de-487">Dans cet exemple, il y a cinq tranches, donc cinq tâches dans Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="605de-487">In this example, there are five slices, so five tasks in Azure Batch.</span></span> <span data-ttu-id="605de-488">Avec la propriété **concurrency** définie sur **5** dans le fichier JSON du pipeline dans Azure Data Factory, et le paramètre **Nombre maximal de tâches par machine virtuelle** défini sur **2** dans le pool Azure Batch avec **2** machines virtuelles, les tâches s’exécutent très rapidement (vérifiez les heures de début et de fin des tâches).</span><span class="sxs-lookup"><span data-stu-id="605de-488">With the **concurrency** set to **5** in the pipeline JSON in Azure Data Factory and **Maximum tasks per VM** set to **2** in Azure Batch pool with **2** VMs, the tasks runs fast (check start and end times for tasks).</span></span>

<span data-ttu-id="605de-489">Utilisez le portail pour afficher le travail Batch et ses tâches associées avec des **tranches** et voir sur quelle machine virtuelle chaque tranche s’est exécutée.</span><span class="sxs-lookup"><span data-stu-id="605de-489">Use the portal to view the Batch job and its tasks that are associated with the **slices** and see what VM each slice ran on.</span></span>

![Azure Data Factory - Tâches de travaux Batch](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-the-pipeline"></a><span data-ttu-id="605de-491">Déboguer le pipeline</span><span class="sxs-lookup"><span data-stu-id="605de-491">Debug the pipeline</span></span>
<span data-ttu-id="605de-492">Le débogage consiste à utiliser quelques techniques de base :</span><span class="sxs-lookup"><span data-stu-id="605de-492">Debugging consists of a few basic techniques:</span></span>

1. <span data-ttu-id="605de-493">Si la tranche d’entrée n’est pas définie sur **Prêt**, vérifiez que la structure du dossier d’entrée est correcte et que le fichier file.txt est présent dans les dossiers d’entrée.</span><span class="sxs-lookup"><span data-stu-id="605de-493">If the input slice is not set to **Ready**, confirm that the input folder structure is correct and file.txt exists in the input folders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. <span data-ttu-id="605de-494">Dans la méthode **Execute** de votre activité personnalisée, utilisez l’objet **IActivityLogger** pour journaliser les informations qui vous aident à résoudre d’éventuels problèmes.</span><span class="sxs-lookup"><span data-stu-id="605de-494">In the **Execute** method of your custom activity, use the **IActivityLogger** object to log information that helps you troubleshoot issues.</span></span> <span data-ttu-id="605de-495">Les messages consignés s’affichent dans le fichier user\_0.log.</span><span class="sxs-lookup"><span data-stu-id="605de-495">The logged messages show up in the user\_0.log file.</span></span>

   <span data-ttu-id="605de-496">Dans le panneau **OutputDataset**, cliquez sur la tranche pour afficher le panneau **TRANCHE DE DONNÉES** correspondant à cette tranche.</span><span class="sxs-lookup"><span data-stu-id="605de-496">In the **OutputDataset** blade, click the slice to see the **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="605de-497">Les **activités exécutées** pour cette tranche s’affichent.</span><span class="sxs-lookup"><span data-stu-id="605de-497">You see **activity runs** for that slice.</span></span> <span data-ttu-id="605de-498">Vous devez normalement voir une exécution d’activité pour la tranche.</span><span class="sxs-lookup"><span data-stu-id="605de-498">You should see one activity run for the slice.</span></span> <span data-ttu-id="605de-499">Si vous cliquez sur **Exécuter** dans la barre de commandes, vous pouvez démarrer une autre exécution d’activité pour la même tranche.</span><span class="sxs-lookup"><span data-stu-id="605de-499">If you click **Run** in the command bar, you can start another activity run for the same slice.</span></span>

   <span data-ttu-id="605de-500">Lorsque vous cliquez sur l’exécution d’activité, le panneau **DÉTAILS DE L’EXÉCUTION D’ACTIVITÉ** s’affiche avec une liste de fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="605de-500">When you click the activity run, you see the **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="605de-501">Les messages consignés s’affichent dans le fichier **user\_0.log**.</span><span class="sxs-lookup"><span data-stu-id="605de-501">You see logged messages in the **user\_0.log** file.</span></span> <span data-ttu-id="605de-502">Lorsqu’une erreur se produit, vous verrez trois exécutions d’activité car le nombre de tentatives est défini sur 3 dans le script JSON du pipeline et de l’activité.</span><span class="sxs-lookup"><span data-stu-id="605de-502">When an error occurs, you see three activity runs because the retry count is set to 3 in the pipeline/activity JSON.</span></span> <span data-ttu-id="605de-503">Lorsque vous cliquez sur l’exécution de l’activité, vous accédez aux fichiers journaux qui vous permettront de résoudre l’erreur.</span><span class="sxs-lookup"><span data-stu-id="605de-503">When you click the activity run, you see the log files that you can review to troubleshoot the error.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   <span data-ttu-id="605de-504">Dans la liste des fichiers journaux, cliquez sur le fichier **user-0.log**.</span><span class="sxs-lookup"><span data-stu-id="605de-504">In the list of log files, click the **user-0.log**.</span></span> <span data-ttu-id="605de-505">Le volet droit affiche les résultats de l’utilisation de la méthode **IActivityLogger.Write** .</span><span class="sxs-lookup"><span data-stu-id="605de-505">In the right panel are the results of using the **IActivityLogger.Write** method.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   <span data-ttu-id="605de-506">Consultez le fichier system-0.log pour vérifier les exceptions et messages d’erreur système éventuels.</span><span class="sxs-lookup"><span data-stu-id="605de-506">Check system-0.log for any system error messages and exceptions.</span></span>

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. <span data-ttu-id="605de-507">Incluez le fichier **PDB** dans le fichier zip afin que les détails de l’erreur incluent des informations telles que la **pile des appels** quand une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="605de-507">Include the **PDB** file in the zip file so that the error details have information such as **call stack** when an error occurs.</span></span>
4. <span data-ttu-id="605de-508">Tous les fichiers contenus dans le fichier zip de l’activité personnalisée doivent se trouver au **niveau supérieur** et ne contenir aucun sous-dossier.</span><span class="sxs-lookup"><span data-stu-id="605de-508">All the files in the zip file for the custom activity must be at the **top level** with no subfolders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. <span data-ttu-id="605de-509">Assurez-vous que les paramètres **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/Mydotnetactivity.zip) et **packageLinkedService** (qui doit pointer vers le Stockage Blob Azure contenant le fichier .zip) sont définis sur des valeurs correctes.</span><span class="sxs-lookup"><span data-stu-id="605de-509">Ensure that the **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point to the Azure blob storage that contains the zip file) are set to correct values.</span></span>
6. <span data-ttu-id="605de-510">Si vous avez corrigé une erreur et souhaitez relancer le traitement de la tranche, cliquez avec le bouton droit sur la tranche dans le panneau **OutputDataset** puis cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="605de-510">If you fixed an error and want to reprocess the slice, right-click the slice in the **OutputDataset** blade and click **Run**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > <span data-ttu-id="605de-511">Vous voyez un **conteneur** dans votre Stockage Blob Azure nommé `adfjobs`.</span><span class="sxs-lookup"><span data-stu-id="605de-511">You see a **container** in your Azure Blob storage named: `adfjobs`.</span></span> <span data-ttu-id="605de-512">Ce conteneur n’est pas automatiquement supprimé, mais vous pouvez le supprimer en toute sécurité après avoir testé la solution.</span><span class="sxs-lookup"><span data-stu-id="605de-512">This container is not automatically deleted, but you can safely delete it after you are done testing the solution.</span></span> <span data-ttu-id="605de-513">De même, la solution Data Factory crée un **travail** Azure Batch nommé `adf-\<pool ID/name\>:job-0000000001`.</span><span class="sxs-lookup"><span data-stu-id="605de-513">Similarly, the Data Factory solution creates an Azure Batch **job** named: `adf-\<pool ID/name\>:job-0000000001`.</span></span> <span data-ttu-id="605de-514">Si vous le souhaitez, vous pouvez supprimer ce travail après avoir testé la solution.</span><span class="sxs-lookup"><span data-stu-id="605de-514">You can delete this job after you test the solution if you like.</span></span>
   >
   >
7. <span data-ttu-id="605de-515">L’activité personnalisée n’utilise pas le ficher **app.config** de votre package.</span><span class="sxs-lookup"><span data-stu-id="605de-515">The custom activity does not use the **app.config** file from your package.</span></span> <span data-ttu-id="605de-516">Par conséquent, si votre code lit des chaînes de connexion dans le fichier de configuration, il ne fonctionne pas lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="605de-516">Therefore, if your code reads any connection strings from the configuration file, it does not work at runtime.</span></span> <span data-ttu-id="605de-517">Quand vous utilisez Azure Batch, la meilleure pratique consiste à stocker les clés secrètes dans un coffre de clés **Azure KeyVault**, à utiliser un principal de service basé sur certificat pour protéger le coffre de clés et à distribuer le certificat à un pool Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="605de-517">The best practice when using Azure Batch is to hold any secrets in an **Azure KeyVault**, use a certificate-based service principal to protect the keyvault, and distribute the certificate to Azure Batch pool.</span></span> <span data-ttu-id="605de-518">L’activité personnalisée .NET peut alors accéder aux secrets du coffre de clés au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="605de-518">The .NET custom activity then can access secrets from the KeyVault at runtime.</span></span> <span data-ttu-id="605de-519">Cette solution est générique et peut s’adapter à n’importe quel type de clé secrète, et pas uniquement aux chaînes de connexion.</span><span class="sxs-lookup"><span data-stu-id="605de-519">This solution is a generic one and can scale to any type of secret, not just connection string.</span></span>

    <span data-ttu-id="605de-520">Il existe une solution plus simple (mais non recommandée) : vous pouvez créer un **service lié SQL Azure** avec des paramètres de chaîne de connexion, puis créer un jeu de données qui utilise le service lié et chaîner le jeu de données à l’activité .NET personnalisée en tant que jeu de données d’entrée factice.</span><span class="sxs-lookup"><span data-stu-id="605de-520">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses the linked service, and chain the dataset as a dummy input dataset to the custom .NET activity.</span></span> <span data-ttu-id="605de-521">Vous pouvez accéder ensuite à la chaîne de connexion du service lié dans le code de l’activité personnalisée. Cette fois-ci, le code devrait fonctionner sans problème lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="605de-521">You can then access the linked service's connection string in the custom activity code and it should work fine at runtime.</span></span>  

#### <a name="extend-the-sample"></a><span data-ttu-id="605de-522">Étendre l’exemple</span><span class="sxs-lookup"><span data-stu-id="605de-522">Extend the sample</span></span>
<span data-ttu-id="605de-523">Vous pouvez étendre cet exemple pour en savoir plus sur les fonctionnalités d’Azure Data Factory et d’Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="605de-523">You can extend this sample to learn more about Azure Data Factory and Azure Batch features.</span></span> <span data-ttu-id="605de-524">Par exemple, pour traiter des tranches d’une autre plage de temps, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="605de-524">For example, to process slices in a different time range, do the following steps:</span></span>

1. <span data-ttu-id="605de-525">Ajoutez au dossier `inputfolder` les sous-dossiers 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08 et 2015-11-16-09, et placez les fichiers d’entrée dans ces dossiers.</span><span class="sxs-lookup"><span data-stu-id="605de-525">Add the following subfolders in the `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 and place input files in those folders.</span></span> <span data-ttu-id="605de-526">Modifiez l’heure de fin pour le pipeline de `2015-11-16T05:00:00Z` à `2015-11-16T10:00:00Z`.</span><span class="sxs-lookup"><span data-stu-id="605de-526">Change the end time for the pipeline from `2015-11-16T05:00:00Z` to `2015-11-16T10:00:00Z`.</span></span> <span data-ttu-id="605de-527">Dans la **vue de diagramme**, double-cliquez sur **InputDataset** et vérifiez que les tranches d’entrée sont prêtes.</span><span class="sxs-lookup"><span data-stu-id="605de-527">In the **Diagram View**, double-click the **InputDataset**, and confirm that the input slices are ready.</span></span> <span data-ttu-id="605de-528">Double-cliquez sur **OuptutDataset** pour vérifier l’état des tranches de sortie.</span><span class="sxs-lookup"><span data-stu-id="605de-528">Double-click **OuptutDataset** to see the state of output slices.</span></span> <span data-ttu-id="605de-529">Si leur état est Prêt, vérifiez les fichiers de sortie dans le dossier de sortie.</span><span class="sxs-lookup"><span data-stu-id="605de-529">If they are in Ready state, check the output folder for the output files.</span></span>
2. <span data-ttu-id="605de-530">Augmentez ou réduisez la valeur du paramètre **concurrency** pour comprendre comment il affecte les performances de votre solution, en particulier le traitement qui se produit sur Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="605de-530">Increase or decrease the **concurrency** setting to understand how it affects the performance of your solution, especially the processing that occurs on Azure Batch.</span></span> <span data-ttu-id="605de-531">(Pour plus d’informations sur le paramètre **concurrency** , voir l’étape 4 : Créer et exécuter le pipeline.)</span><span class="sxs-lookup"><span data-stu-id="605de-531">(See Step 4: Create and run the pipeline for more on the **concurrency** setting.)</span></span>
3. <span data-ttu-id="605de-532">Créez un pool avec une valeur **Maximum tasks per VM**(Nombre maximal de tâches par machine virtuelle) supérieure/inférieure.</span><span class="sxs-lookup"><span data-stu-id="605de-532">Create a pool with higher/lower **Maximum tasks per VM**.</span></span> <span data-ttu-id="605de-533">Mettez à jour le service lié Azure Batch dans la solution Data Factory pour utiliser le nouveau pool créé.</span><span class="sxs-lookup"><span data-stu-id="605de-533">To use the new pool you created, update the Azure Batch linked service in the Data Factory solution.</span></span> <span data-ttu-id="605de-534">(Pour plus d’informations sur le paramètre **Maximum tasks per VM** , voir l’étape 4 : Créer et exécuter le pipeline.)</span><span class="sxs-lookup"><span data-stu-id="605de-534">(See Step 4: Create and run the pipeline for more on the **Maximum tasks per VM** setting.)</span></span>
4. <span data-ttu-id="605de-535">Créez un pool Azure Batch avec la fonctionnalité **autoscale** .</span><span class="sxs-lookup"><span data-stu-id="605de-535">Create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="605de-536">La mise à l’échelle automatique des nœuds de calcul dans un pool Azure Batch est en fait un ajustement dynamique de la puissance de traitement utilisée par votre application.</span><span class="sxs-lookup"><span data-stu-id="605de-536">Automatically scaling compute nodes in an Azure Batch pool is the dynamic adjustment of processing power used by your application.</span></span> 

    <span data-ttu-id="605de-537">Cet exemple de formule permet d’obtenir le comportement suivant : quand le pool est créé, il commence avec 1 machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="605de-537">The sample formula here achieves the following behavior: When the pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="605de-538">La métrique $PendingTasks définit le nombre de tâches dans l’état En cours d’exécution + Actif (en file d’attente).</span><span class="sxs-lookup"><span data-stu-id="605de-538">$PendingTasks metric defines the number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="605de-539">Cette formule recherche le nombre moyen de tâches en attente au cours des 180 dernières secondes et définit TargetDedicated en conséquence.</span><span class="sxs-lookup"><span data-stu-id="605de-539">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="605de-540">Elle garantit que TargetDedicated ne va jamais au-delà de 25 machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="605de-540">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="605de-541">Par conséquent, à mesure que de nouvelles tâches sont envoyées, le pool s’accroît automatiquement et, au fil de la réalisation des tâches, les machines virtuelles se libèrent une à une et la mise à l’échelle automatique réduit ces machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="605de-541">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span></span> <span data-ttu-id="605de-542">Vous pouvez ajuster startingNumberOfVMs et maxNumberofVMs selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="605de-542">startingNumberOfVMs and maxNumberofVMs can be adjusted to your needs.</span></span>
 
    <span data-ttu-id="605de-543">Formule de mise à l’échelle automatique :</span><span class="sxs-lookup"><span data-stu-id="605de-543">Autoscale formula:</span></span>

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   <span data-ttu-id="605de-544">Pour plus d’informations, consultez [Mettre automatiquement à l’échelle les nœuds de calcul dans un pool Azure Batch](../batch/batch-automatic-scaling.md) .</span><span class="sxs-lookup"><span data-stu-id="605de-544">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

   <span data-ttu-id="605de-545">Si le pool utilise la valeur par défaut du paramètre [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), le service Batch peut mettre 15 à 30 minutes à préparer la machine virtuelle avant d’exécuter l’activité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="605de-545">If the pool is using the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service could take 15-30 minutes to prepare the VM before running the custom activity.</span></span>  <span data-ttu-id="605de-546">Si le pool utilise une autre valeur pour autoScaleEvaluationInterval, le service Batch peut prendre la durée d’autoScaleEvaluationInterval + 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="605de-546">If the pool is using a different autoScaleEvaluationInterval, the Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>
5. <span data-ttu-id="605de-547">Dans l’exemple de solution, la méthode **Execute** appelle la méthode **Calculate** qui traite une tranche de données d’entrée pour produire une tranche de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="605de-547">In the sample solution, the **Execute** method invokes the **Calculate** method that processes an input data slice to produce an output data slice.</span></span> <span data-ttu-id="605de-548">Vous pouvez écrire votre propre méthode pour traiter les données d’entrée, et remplacer l’appel de la méthode Calculate dans la méthode Execute par un appel à votre méthode.</span><span class="sxs-lookup"><span data-stu-id="605de-548">You can write your own method to process input data and replace the Calculate method call in the Execute method with a call to your method.</span></span>

### <a name="next-steps-consume-the-data"></a><span data-ttu-id="605de-549">Étapes suivantes : Consommer les données</span><span class="sxs-lookup"><span data-stu-id="605de-549">Next steps: Consume the data</span></span>
<span data-ttu-id="605de-550">Après avoir traité des données, vous pouvez les employer avec des outils en ligne tels que **Microsoft Power BI**.</span><span class="sxs-lookup"><span data-stu-id="605de-550">After you process data, you can consume it with online tools like **Microsoft Power BI**.</span></span> <span data-ttu-id="605de-551">Voici des liens pour vous aider à comprendre Power BI et comment l’utiliser dans Azure :</span><span class="sxs-lookup"><span data-stu-id="605de-551">Here are links to help you understand Power BI and how to use it in Azure:</span></span>

* [<span data-ttu-id="605de-552">Explorer un jeu de données dans Power BI</span><span class="sxs-lookup"><span data-stu-id="605de-552">Explore a dataset in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [<span data-ttu-id="605de-553">Prise en main de Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="605de-553">Getting started with the Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [<span data-ttu-id="605de-554">Actualisation des données dans Power BI</span><span class="sxs-lookup"><span data-stu-id="605de-554">Refresh data in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [<span data-ttu-id="605de-555">Azure et Power BI</span><span class="sxs-lookup"><span data-stu-id="605de-555">Azure and Power BI - basic overview</span></span>](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a><span data-ttu-id="605de-556">Références</span><span class="sxs-lookup"><span data-stu-id="605de-556">References</span></span>
* [<span data-ttu-id="605de-557">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="605de-557">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

  * [<span data-ttu-id="605de-558">Présentation du service Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="605de-558">Introduction to Azure Data Factory service</span></span>](data-factory-introduction.md)
  * [<span data-ttu-id="605de-559">Prise en main d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="605de-559">Get started with Azure Data Factory</span></span>](data-factory-build-your-first-pipeline.md)
  * [<span data-ttu-id="605de-560">Utilisation des activités personnalisées dans un pipeline Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="605de-560">Use custom activities in an Azure Data Factory pipeline</span></span>](data-factory-use-custom-activities.md)
* [<span data-ttu-id="605de-561">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="605de-561">Azure Batch</span></span>](https://azure.microsoft.com/documentation/services/batch/)

  * [<span data-ttu-id="605de-562">Notions de base d’Azure Batch</span><span class="sxs-lookup"><span data-stu-id="605de-562">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
  * [<span data-ttu-id="605de-563">Vue d’ensemble des fonctionnalités d’Azure Batch</span><span class="sxs-lookup"><span data-stu-id="605de-563">Overview of Azure Batch features</span></span>](../batch/batch-api-basics.md)
  * [<span data-ttu-id="605de-564">Création et gestion d’un compte Azure Batch dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="605de-564">Create and manage Azure Batch account in the Azure portal</span></span>](../batch/batch-account-create-portal.md)
  * [<span data-ttu-id="605de-565">Get started with the .NET Azure Batch Library .NET</span><span class="sxs-lookup"><span data-stu-id="605de-565">Get started with Azure Batch Library .NET</span></span>](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
