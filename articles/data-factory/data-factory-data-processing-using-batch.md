---
title: "jeux de données à grande échelle aaaProcess à l’aide de la fabrique de données et de traitement par lots | Documents Microsoft"
description: "Décrit comment tooprocess de grandes quantités de données dans une fabrique de données Azure de pipeline à l’aide des capacités de traitement parallèle de traitement par lots Azure."
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
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a><span data-ttu-id="d50ae-103">Traiter des jeux de données volumineux à l’aide de Data Factory et Batch</span><span class="sxs-lookup"><span data-stu-id="d50ae-103">Process large-scale datasets using Data Factory and Batch</span></span>
<span data-ttu-id="d50ae-104">Cet article décrit une architecture d’un exemple de solution qui déplace et traite des jeux de données volumineux de manière automatique et planifiée.</span><span class="sxs-lookup"><span data-stu-id="d50ae-104">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span></span> <span data-ttu-id="d50ae-105">Il fournit également une solution de hello tooimplement procédure pas à pas de bout en bout à l’aide d’Azure Data Factory et Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="d50ae-105">It also provides an end-to-end walkthrough tooimplement hello solution using Azure Data Factory and Azure Batch.</span></span>

<span data-ttu-id="d50ae-106">Cet article est plus long que nos articles habituels car il contient une procédure pas à pas d’un exemple de solution complète.</span><span class="sxs-lookup"><span data-stu-id="d50ae-106">This article is longer than our typical article because it contains a walkthrough of an entire sample solution.</span></span> <span data-ttu-id="d50ae-107">Si vous êtes tooBatch nouvelle fabrique de données, vous pouvez en savoir plus sur ces services et comment ils fonctionnent ensemble.</span><span class="sxs-lookup"><span data-stu-id="d50ae-107">If you are new tooBatch and Data Factory, you can learn about these services and how they work together.</span></span> <span data-ttu-id="d50ae-108">Si vous connaissez vos services de hello et sont conception/élaboration d’une solution, vous pouvez concentrer uniquement sur hello [section architecture](#architecture-of-sample-solution) de hello article et si vous développez un prototype ou une solution, vous pouvez également tootry out instructions détaillées dans hello [procédure pas à pas](#implementation-of-sample-solution).</span><span class="sxs-lookup"><span data-stu-id="d50ae-108">If you know something about hello services and are designing/architecting a solution, you may focus just on hello [architecture section](#architecture-of-sample-solution) of hello article and if you are developing a prototype or a solution, you may also want tootry out step-by-step instructions in hello [walkthrough](#implementation-of-sample-solution).</span></span> <span data-ttu-id="d50ae-109">N’hésitez pas à nous faire part de vos commentaires sur ce contenu et son utilisation.</span><span class="sxs-lookup"><span data-stu-id="d50ae-109">We invite your comments about this content and how you use it.</span></span>

<span data-ttu-id="d50ae-110">Tout d’abord, nous allons voir comment les services de fabrique de données et de traitement par lots peuvent aider à avec le traitement de grands volumes de données dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-110">First, let's look at how Data Factory and Batch services can help with processing large datasets in hello cloud.</span></span>     

## <a name="why-azure-batch"></a><span data-ttu-id="d50ae-111">Pourquoi Azure Batch ?</span><span class="sxs-lookup"><span data-stu-id="d50ae-111">Why Azure Batch?</span></span>
<span data-ttu-id="d50ae-112">Traitement par lots Azure vous permet de toorun (HPC) informatique à grande échelle en parallèle et haute performance des applications efficacement dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-112">Azure Batch enables you toorun large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="d50ae-113">Il s’agit d’un service de plateforme qui planifie toorun de travail de calcul intensif sur une collection gérée de machines virtuelles, et peut automatiquement montée en puissance de calcul ressources toomeet hello aux besoins de vos tâches.</span><span class="sxs-lookup"><span data-stu-id="d50ae-113">It's a platform service that schedules compute-intensive work toorun on a managed collection of virtual machines, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span>

<span data-ttu-id="d50ae-114">Avec hello service Batch, vous définissez tooexecute des ressources de calcul Azure vos applications en parallèle et à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="d50ae-114">With hello Batch service, you define Azure compute resources tooexecute your applications in parallel, and at scale.</span></span> <span data-ttu-id="d50ae-115">Vous pouvez exécuter à la demande ou planifiées travaux et que vous n’avez pas besoin toomanually créer, configurer et gérer un cluster HPC, les machines virtuelles, les réseaux virtuels ou une tâche complexe et infrastructure de planification de tâches.</span><span class="sxs-lookup"><span data-stu-id="d50ae-115">You can run on-demand or scheduled jobs, and you don't need toomanually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span>

<span data-ttu-id="d50ae-116">Consultez hello suivant articles si vous n’êtes pas familiarisé avec Azure Batch car cela permet de comprendre l’architecture de hello/implémentation de solution hello décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="d50ae-116">See hello following articles if you are not familiar with Azure Batch as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>   

* [<span data-ttu-id="d50ae-117">Notions de base d’Azure Batch</span><span class="sxs-lookup"><span data-stu-id="d50ae-117">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
* [<span data-ttu-id="d50ae-118">Aperçu des fonctionnalités d’Azure Batch</span><span class="sxs-lookup"><span data-stu-id="d50ae-118">Batch feature overview</span></span>](../batch/batch-api-basics.md)

<span data-ttu-id="d50ae-119">(facultatif) toolearn en savoir plus sur le traitement par lots Azure, consultez hello [cursus pour Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span><span class="sxs-lookup"><span data-stu-id="d50ae-119">(optional) toolearn more about Azure Batch, see hello [Learning path for Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span></span>

## <a name="why-azure-data-factory"></a><span data-ttu-id="d50ae-120">Pourquoi Azure Data Factory ?</span><span class="sxs-lookup"><span data-stu-id="d50ae-120">Why Azure Data Factory?</span></span>
<span data-ttu-id="d50ae-121">Fabrique de données est un service d’intégration de données basés sur le cloud qui orchestre et automatise le déplacement de hello et la transformation de données.</span><span class="sxs-lookup"><span data-stu-id="d50ae-121">Data Factory is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="d50ae-122">À l’aide du service de fabrique de données hello, vous pouvez créer des pipelines de données managées déplacement les données du site et de magasin de données centralisé de données magasins tooa le cloud (par exemple : stockage d’objets Blob Azure) et le processus/transformer les données à l’aide des services tels que Azure HDInsight Azure Apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="d50ae-122">Using hello Data Factory service, you can create managed data pipelines that move data from on-premises and cloud data stores tooa centralized data store (for example: Azure Blob Storage), and process/transform data using services such as Azure HDInsight and Azure Machine Learning.</span></span> <span data-ttu-id="d50ae-123">Vous pouvez également planifier toorun des pipelines de données dans une manière planifiée (horaire, quotidienne, hebdomadaire, etc.) et un moniteur et les gérer un problèmes de tooidentify coup de œil et prenez les mesures.</span><span class="sxs-lookup"><span data-stu-id="d50ae-123">You can also schedule data pipelines toorun in a scheduled manner (hourly, daily, weekly, etc.) and monitor and manage them at a glance tooidentify issues and take action.</span></span>

<span data-ttu-id="d50ae-124">Consultez hello suivant articles si vous n’êtes pas familiarisé avec Azure Data Factory car cela permet de comprendre l’architecture de hello/implémentation de solution hello décrite dans cet article.</span><span class="sxs-lookup"><span data-stu-id="d50ae-124">See hello following articles if you are not familiar with Azure Data Factory as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>  

* [<span data-ttu-id="d50ae-125">Présentation d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d50ae-125">Introduction of Azure Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="d50ae-126">Générer votre premier pipeline de données</span><span class="sxs-lookup"><span data-stu-id="d50ae-126">Build your first data pipeline</span></span>](data-factory-build-your-first-pipeline.md)   

<span data-ttu-id="d50ae-127">(facultatif) toolearn en savoir plus sur Azure Data Factory, consultez hello [cursus pour Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="d50ae-127">(optional) toolearn more about Azure Data Factory, see hello [Learning path for Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span></span>

## <a name="data-factory-and-batch-together"></a><span data-ttu-id="d50ae-128">Intégration de Data Factory et Batch</span><span class="sxs-lookup"><span data-stu-id="d50ae-128">Data Factory and Batch together</span></span>
<span data-ttu-id="d50ae-129">Fabrique de données inclut des activités intégrées, telles que le magasin de données de toocopy/déplacement de l’activité de copie à partir de la source données tooa banque de données de destination et activité de la ruche tooprocess à l’aide (HDInsight) les clusters Hadoop sur Azure.</span><span class="sxs-lookup"><span data-stu-id="d50ae-129">Data Factory includes built-in activities such as Copy Activity toocopy/move data from a source data store tooa destination data store and Hive Activity tooprocess data using Hadoop clusters (HDInsight) on Azure.</span></span> <span data-ttu-id="d50ae-130">Consultez l’article [Activités de transformation des données](data-factory-data-transformation-activities.md) pour obtenir la liste des activités de transformation prises en charge.</span><span class="sxs-lookup"><span data-stu-id="d50ae-130">See [Data Transformation Activities](data-factory-data-transformation-activities.md) for a list of supported transformation activities.</span></span>

<span data-ttu-id="d50ae-131">Aussi, il permet de vous toocreate .NET des activités personnalisées toomove ou traitent des données avec votre propre logique et exécuter ces activités sur un cluster Azure HDInsight ou sur un pool de traitement par lots Azure des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="d50ae-131">It also allows you toocreate custom .NET activities toomove or process data with your own logic and run these activities on an Azure HDInsight cluster or on an Azure Batch pool of VMs.</span></span> <span data-ttu-id="d50ae-132">Lorsque vous utilisez le traitement par lots Azure, vous pouvez configurer hello pool tooauto à l’échelle (ajouter ou supprimer des ordinateurs virtuels en fonction de la charge de travail hello) basé sur une formule que vous fournissez.</span><span class="sxs-lookup"><span data-stu-id="d50ae-132">When you use Azure Batch, you can configure hello pool tooauto-scale (add or remove VMs based on hello workload) based on a formula you provide.</span></span>     

## <a name="architecture-of-sample-solution"></a><span data-ttu-id="d50ae-133">Architecture de l’exemple de solution</span><span class="sxs-lookup"><span data-stu-id="d50ae-133">Architecture of sample solution</span></span>
<span data-ttu-id="d50ae-134">Bien que l’architecture de hello décrite dans cet article est une solution simple, il est toocomplex pertinentes des scénarios tels que le risque de modélisation par les services financiers, le traitement d’image et rendu et analyse génomique.</span><span class="sxs-lookup"><span data-stu-id="d50ae-134">Even though hello architecture described in this article is for a simple solution, it is relevant toocomplex scenarios such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span></span>

<span data-ttu-id="d50ae-135">Hello illustre 1) la fabrique de données orchestre le déplacement des données et le traitement et 2) de quelle façon Azure Batch traite hello des données de manière parallèle.</span><span class="sxs-lookup"><span data-stu-id="d50ae-135">hello diagram illustrates 1) how Data Factory orchestrates data movement and processing and 2) how Azure Batch processes hello data in a parallel manner.</span></span> <span data-ttu-id="d50ae-136">Téléchargement et diagramme d’impression hello pour faciliter la référence (11 x 17 pouces.</span><span class="sxs-lookup"><span data-stu-id="d50ae-136">Download and print hello diagram for easy reference (11 x 17 in.</span></span> <span data-ttu-id="d50ae-137">ou format A3) : [Calcul haute performance et orchestration de données à l’aide des services Azure Batch et Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span><span class="sxs-lookup"><span data-stu-id="d50ae-137">or A3 size): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span></span>

<span data-ttu-id="d50ae-138">[![Diagramme de traitement des données à grande échelle](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="d50ae-138">[![Large-scale data processing diagram](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span></span>

<span data-ttu-id="d50ae-139">Hello liste suivante fournit les étapes de base hello du processus de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-139">hello following list provides hello basic steps of hello process.</span></span> <span data-ttu-id="d50ae-140">solution de Hello inclut le code et des explications pour les solutions de bout en bout toobuild hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-140">hello solution includes code and explanations toobuild hello end-to-end solution.</span></span>

1. <span data-ttu-id="d50ae-141">**Configurez Azure Batch avec un pool de nœuds de calcul (machines virtuelles)**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-141">**Configure Azure Batch with a pool of compute nodes (VMs)**.</span></span> <span data-ttu-id="d50ae-142">Vous pouvez spécifier le nombre de hello de nœuds et la taille de chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="d50ae-142">You can specify hello number of nodes and size of each node.</span></span>
2. <span data-ttu-id="d50ae-143">**Créez une instance Azure Data Factory** configurée avec des entités qui représentent respectivement le stockage d’objets blob Azure, le service de calcul Azure Batch, les données en entrée et sortie, ainsi qu’un flux de travail, ou pipeline, d’activités qui déplacent et transforment des données.</span><span class="sxs-lookup"><span data-stu-id="d50ae-143">**Create an Azure Data Factory instance** that is configured with entities that represent Azure blob storage, Azure Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span></span>
3. <span data-ttu-id="d50ae-144">**Créer une activité .NET personnalisée dans le pipeline de Data Factory hello**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-144">**Create a custom .NET activity in hello Data Factory pipeline**.</span></span> <span data-ttu-id="d50ae-145">activité Hello est votre code utilisateur qui s’exécute sur hello pool Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="d50ae-145">hello activity is your user code that runs on hello Azure Batch pool.</span></span>
4. <span data-ttu-id="d50ae-146">**Stockez de grandes quantités de données d’entrée en tant qu’objets blob dans Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-146">**Store large amounts of input data as blobs in Azure storage**.</span></span> <span data-ttu-id="d50ae-147">Les données sont divisées en tranches logiques (généralement basées sur l’heure).</span><span class="sxs-lookup"><span data-stu-id="d50ae-147">Data is divided into logical slices (usually by time).</span></span>
5. <span data-ttu-id="d50ae-148">**Fabrique de données copie les données traitées en parallèle** toohello les emplacement secondaire.</span><span class="sxs-lookup"><span data-stu-id="d50ae-148">**Data Factory copies data that is processed in parallel** toohello secondary location.</span></span>
6. <span data-ttu-id="d50ae-149">**Fabrique de données s’exécute l’activité personnalisée hello est à l’aide de pool hello allouée par lot**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-149">**Data Factory runs hello custom activity using hello pool allocated by Batch**.</span></span> <span data-ttu-id="d50ae-150">Data Factory peut exécuter plusieurs activités simultanément.</span><span class="sxs-lookup"><span data-stu-id="d50ae-150">Data Factory can run activities concurrently.</span></span> <span data-ttu-id="d50ae-151">Chaque activité traite une tranche de données.</span><span class="sxs-lookup"><span data-stu-id="d50ae-151">Each activity processes a slice of data.</span></span> <span data-ttu-id="d50ae-152">résultats de Hello sont stockés dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d50ae-152">hello results are stored in Azure storage.</span></span>
7. <span data-ttu-id="d50ae-153">**Fabrique de données déplace le troisième emplacement hello résultats finaux tooa**, soit pour la distribution via une application, ou pour un traitement ultérieur par d’autres outils.</span><span class="sxs-lookup"><span data-stu-id="d50ae-153">**Data Factory moves hello final results tooa third location**, either for distribution via an app, or for further processing by other tools.</span></span>

## <a name="implementation-of-sample-solution"></a><span data-ttu-id="d50ae-154">Implémentation de l’exemple de solution</span><span class="sxs-lookup"><span data-stu-id="d50ae-154">Implementation of sample solution</span></span>
<span data-ttu-id="d50ae-155">exemple de solution Hello est volontairement simple et est tooshow vous comment toouse Data Factory et traitement par lots ensemble tooprocess jeux de données.</span><span class="sxs-lookup"><span data-stu-id="d50ae-155">hello sample solution is intentionally simple and is tooshow you how toouse Data Factory and Batch together tooprocess datasets.</span></span> <span data-ttu-id="d50ae-156">solution de Hello simplement nombre hello d’occurrences d’un terme à rechercher (« Microsoft ») dans les fichiers d’entrée organisés dans une série chronologique.</span><span class="sxs-lookup"><span data-stu-id="d50ae-156">hello solution simply counts hello number of occurrences of a search term (“Microsoft”) in input files organized in a time series.</span></span> <span data-ttu-id="d50ae-157">Il génère des fichiers de toooutput hello count.</span><span class="sxs-lookup"><span data-stu-id="d50ae-157">It outputs hello count toooutput files.</span></span>

<span data-ttu-id="d50ae-158">**Heure**: Si vous êtes familiarisé avec les concepts de base d’Azure Data Factory et traitement par lots, et ont des conditions préalables de hello terminé répertoriées ci-dessous, nous estimons cette solution prend toocomplete de 1 à 2 heures.</span><span class="sxs-lookup"><span data-stu-id="d50ae-158">**Time**: If you are familiar with basics of Azure, Data Factory, and Batch, and have completed hello prerequisites listed below, we estimate this solution takes 1-2 hours toocomplete.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="d50ae-159">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d50ae-159">Prerequisites</span></span>
#### <a name="azure-subscription"></a><span data-ttu-id="d50ae-160">Abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="d50ae-160">Azure subscription</span></span>
<span data-ttu-id="d50ae-161">Si vous n’êtes pas abonné, vous pouvez créer un compte d’essai gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="d50ae-161">If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d50ae-162">Voir [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d50ae-162">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

#### <a name="azure-storage-account"></a><span data-ttu-id="d50ae-163">Compte Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d50ae-163">Azure storage account</span></span>
<span data-ttu-id="d50ae-164">Vous utilisez un compte de stockage Azure pour stocker les données de hello dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d50ae-164">You use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="d50ae-165">Si vous ne possédez pas de compte de stockage Azure, voir [Création d’un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="d50ae-165">If you don't have an Azure storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="d50ae-166">exemple de solution Hello utilise le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="d50ae-166">hello sample solution uses blob storage.</span></span>

#### <a name="azure-batch-account"></a><span data-ttu-id="d50ae-167">Compte Azure Batch</span><span class="sxs-lookup"><span data-stu-id="d50ae-167">Azure Batch account</span></span>
<span data-ttu-id="d50ae-168">Créer un compte Azure Batch hello [portail Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="d50ae-168">Create an Azure Batch account using hello [Azure portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="d50ae-169">Voir [Créer et gérer un compte Azure Batch](../batch/batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d50ae-169">See [Create and manage an Azure Batch account](../batch/batch-account-create-portal.md).</span></span> <span data-ttu-id="d50ae-170">Notez hello Azure Batch compte et le nom de clé du compte.</span><span class="sxs-lookup"><span data-stu-id="d50ae-170">Note hello Azure Batch account name and account key.</span></span> <span data-ttu-id="d50ae-171">Vous pouvez également utiliser [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) toocreate de l’applet de commande un compte Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="d50ae-171">You can also use [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate an Azure Batch account.</span></span> <span data-ttu-id="d50ae-172">Pour obtenir des instructions détaillées sur l’utilisation de cette applet de commande, voir [Prise en main des applets de commande Azure Batch PowerShell](../batch/batch-powershell-cmdlets-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="d50ae-172">See [Get started with Azure Batch PowerShell cmdlets](../batch/batch-powershell-cmdlets-get-started.md) for detailed instructions on using this cmdlet.</span></span>

<span data-ttu-id="d50ae-173">exemple de solution Hello utilise des données de tooprocess d’Azure Batch (indirectement via un pipeline Azure Data Factory) de manière parallèle sur un pool de nœuds de calcul (une collection managée d’ordinateurs virtuels).</span><span class="sxs-lookup"><span data-stu-id="d50ae-173">hello sample solution uses Azure Batch (indirectly via an Azure Data Factory pipeline) tooprocess data in a parallel manner on a pool of compute nodes (a managed collection of virtual machines).</span></span>

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a><span data-ttu-id="d50ae-174">Pool de machines virtuelles Azure Batch</span><span class="sxs-lookup"><span data-stu-id="d50ae-174">Azure Batch pool of virtual machines (VMs)</span></span>
<span data-ttu-id="d50ae-175">Créez un **pool Azure Batch** comprenant au moins 2 nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="d50ae-175">Create an **Azure Batch pool** with at least 2 compute nodes.</span></span>

1. <span data-ttu-id="d50ae-176">Bonjour [portail Azure](https://portal.azure.com), cliquez sur **Parcourir** dans hello du menu de gauche, puis cliquez sur **comptes Batch**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-176">In hello [Azure portal](https://portal.azure.com), click **Browse** in hello left menu, and click **Batch Accounts**.</span></span>
2. <span data-ttu-id="d50ae-177">Sélectionnez votre hello tooopen du compte Azure Batch **compte Batch** panneau.</span><span class="sxs-lookup"><span data-stu-id="d50ae-177">Select your Azure Batch account tooopen hello **Batch Account** blade.</span></span>
3. <span data-ttu-id="d50ae-178">Cliquez sur la vignette **Pools** .</span><span class="sxs-lookup"><span data-stu-id="d50ae-178">Click **Pools** tile.</span></span>
4. <span data-ttu-id="d50ae-179">Bonjour **Pools** panneau, cliquez sur le bouton Ajouter dans la barre d’outils de hello tooadd un pool.</span><span class="sxs-lookup"><span data-stu-id="d50ae-179">In hello **Pools** blade, click Add button on hello toolbar tooadd a pool.</span></span>
   1. <span data-ttu-id="d50ae-180">Entrez un ID de pool de hello (**ID du Pool**).</span><span class="sxs-lookup"><span data-stu-id="d50ae-180">Enter an ID for hello pool (**Pool ID**).</span></span> <span data-ttu-id="d50ae-181">Hello de note **ID de pool de hello**; vous en avez besoin lors de la création de solutions de Data Factory hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-181">Note hello **ID of hello pool**; you need it when creating hello Data Factory solution.</span></span>
   2. <span data-ttu-id="d50ae-182">Spécifiez **Windows Server 2012 R2** pour le paramètre de famille du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-182">Specify **Windows Server 2012 R2** for hello Operating System Family setting.</span></span>
   3. <span data-ttu-id="d50ae-183">Sélectionnez le **niveau tarifaire du nœud**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-183">Select a **node pricing tier**.</span></span>
   4. <span data-ttu-id="d50ae-184">Entrez **2** en tant que valeur pour hello **cible dédié** paramètre.</span><span class="sxs-lookup"><span data-stu-id="d50ae-184">Enter **2** as value for hello **Target Dedicated** setting.</span></span>
   5. <span data-ttu-id="d50ae-185">Entrez **2** en tant que valeur pour hello **nombre maximal de tâches par nœud** paramètre.</span><span class="sxs-lookup"><span data-stu-id="d50ae-185">Enter **2** as value for hello **Max tasks per node** setting.</span></span>
   6. <span data-ttu-id="d50ae-186">Cliquez sur **OK** pool de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d50ae-186">Click **OK** toocreate hello pool.</span></span>

#### <a name="azure-storage-explorer"></a><span data-ttu-id="d50ae-187">Explorateur de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="d50ae-187">Azure Storage Explorer</span></span>
<span data-ttu-id="d50ae-188">[Azure Storage Explorer 6 (outil)](https://azurestorageexplorer.codeplex.com/) ou [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (à partir du logiciel ClumsyLeaf).</span><span class="sxs-lookup"><span data-stu-id="d50ae-188">[Azure Storage Explorer 6 (tool)](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software).</span></span> <span data-ttu-id="d50ae-189">Vous utilisez ces outils pour examiner et modifier les données de salutation dans vos projets de stockage Azure, notamment les journaux de hello de vos applications hébergés dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="d50ae-189">You use these tools for inspecting and altering hello data in your Azure Storage projects including hello logs of your cloud-hosted applications.</span></span>

1. <span data-ttu-id="d50ae-190">Créez un conteneur nommé **mycontainer** avec un accès privé (par d’accès anonyme).</span><span class="sxs-lookup"><span data-stu-id="d50ae-190">Create a container named **mycontainer** with private access (no anonymous access)</span></span>
2. <span data-ttu-id="d50ae-191">Si vous utilisez **CloudXplorer**, créer des dossiers et sous-dossiers avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="d50ae-191">If you are using **CloudXplorer**, create folders and subfolders with hello following structure:</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   <span data-ttu-id="d50ae-192">`Inputfolder` et `outputfolder` sont des dossiers de niveau supérieur de `mycontainer`.</span><span class="sxs-lookup"><span data-stu-id="d50ae-192">`Inputfolder` and `outputfolder` are top-level folders in `mycontainer`.</span></span> <span data-ttu-id="d50ae-193">Hello `inputfolder` a des sous-dossiers contenant les cachets de date et d’heure (AAAA-MM-JJ-HH).</span><span class="sxs-lookup"><span data-stu-id="d50ae-193">hello `inputfolder` has subfolders with date-time stamps (YYYY-MM-DD-HH).</span></span>

   <span data-ttu-id="d50ae-194">Si vous utilisez **Azure Storage Explorer**, à l’étape suivante de hello, vous avez besoin des fichiers de tooupload avec des noms : `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="d50ae-194">If you are using **Azure Storage Explorer**, in hello next step, you need tooupload files with names: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` and so on.</span></span> <span data-ttu-id="d50ae-195">Cette étape crée automatiquement des dossiers de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-195">This step automatically creates hello folders.</span></span>
3. <span data-ttu-id="d50ae-196">Créez un fichier texte **fichier.txt** sur votre ordinateur avec un contenu qui a le mot clé de hello **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-196">Create a text file **file.txt** on your machine with content that has hello keyword **Microsoft**.</span></span> <span data-ttu-id="d50ae-197">Par exemple, « activité de test personnalisé Microsoft ».</span><span class="sxs-lookup"><span data-stu-id="d50ae-197">For example: “test custom activity Microsoft test custom activity Microsoft”.</span></span>
4. <span data-ttu-id="d50ae-198">Téléchargez toohello de fichier hello suivant des dossiers d’entrée dans le stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d50ae-198">Upload hello file toohello following input folders in Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   <span data-ttu-id="d50ae-199">Si vous utilisez **Azure Storage Explorer**, téléchargez le fichier de hello **fichier.txt** trop**mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-199">If you are using **Azure Storage Explorer**, upload hello file **file.txt** too**mycontainer**.</span></span> <span data-ttu-id="d50ae-200">Cliquez sur **copie** sur la barre d’outils de hello toocreate une copie de l’objet blob de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-200">Click **Copy** on hello toolbar toocreate a copy of hello blob.</span></span> <span data-ttu-id="d50ae-201">Bonjour **Copy Blob** boîte de dialogue, modification hello **nom d’objet blob de destination** trop`inputfolder/2015-11-16-00/file.txt`.</span><span class="sxs-lookup"><span data-stu-id="d50ae-201">In hello **Copy Blob** dialog box, change hello **destination blob name** too`inputfolder/2015-11-16-00/file.txt`.</span></span> <span data-ttu-id="d50ae-202">Répétez cette étape toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="d50ae-202">Repeat this step toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` and so on.</span></span> <span data-ttu-id="d50ae-203">Cette action crée automatiquement des dossiers de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-203">This action automatically creates hello folders.</span></span>
5. <span data-ttu-id="d50ae-204">Créez un autre conteneur nommé : `customactivitycontainer`.</span><span class="sxs-lookup"><span data-stu-id="d50ae-204">Create another container named: `customactivitycontainer`.</span></span> <span data-ttu-id="d50ae-205">Vous téléchargez des conteneurs de toothis de fichiers zip activité personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-205">You upload hello custom activity zip file toothis container.</span></span>

#### <a name="visual-studio"></a><span data-ttu-id="d50ae-206">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d50ae-206">Visual Studio</span></span>
<span data-ttu-id="d50ae-207">Installer Microsoft Visual Studio 2012 ou version ultérieure toocreate hello personnalisé lot activité toobe utilisé Bonjour solution de fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="d50ae-207">Install Microsoft Visual Studio 2012 or later toocreate hello custom Batch activity toobe used in hello Data Factory solution.</span></span>

### <a name="high-level-steps-toocreate-hello-solution"></a><span data-ttu-id="d50ae-208">Solution de hello toocreate étapes principales</span><span class="sxs-lookup"><span data-stu-id="d50ae-208">High-level steps toocreate hello solution</span></span>
1. <span data-ttu-id="d50ae-209">Créer une activité personnalisée qui contient la logique de traitement des données hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-209">Create a custom activity that contains hello data processing logic.</span></span>
2. <span data-ttu-id="d50ae-210">Créez une fabrique de données Azure qui utilise l’activité personnalisée hello :</span><span class="sxs-lookup"><span data-stu-id="d50ae-210">Create an Azure data factory that uses hello custom activity:</span></span>

### <a name="create-hello-custom-activity"></a><span data-ttu-id="d50ae-211">Créer l’activité personnalisée hello</span><span class="sxs-lookup"><span data-stu-id="d50ae-211">Create hello custom activity</span></span>
<span data-ttu-id="d50ae-212">Hello activité personnalisée de fabrique de données est le cœur de hello de cet exemple de solution.</span><span class="sxs-lookup"><span data-stu-id="d50ae-212">hello Data Factory custom activity is hello heart of this sample solution.</span></span> <span data-ttu-id="d50ae-213">exemple de solution Hello utilise l’activité personnalisée de traitement par lots Azure toorun hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-213">hello sample solution uses Azure Batch toorun hello custom activity.</span></span> <span data-ttu-id="d50ae-214">Consultez [utiliser des activités personnalisées dans un pipeline Azure Data Factory](data-factory-use-custom-activities.md) pour des activités personnalisées hello des informations de base toodevelop et l’utilisation dans Azure Data Factory pipelines.</span><span class="sxs-lookup"><span data-stu-id="d50ae-214">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) for hello basic information toodevelop custom activities and use them in Azure Data Factory pipelines.</span></span>

<span data-ttu-id="d50ae-215">toocreate une activité personnalisée .NET que vous pouvez utiliser dans un pipeline Azure Data Factory, vous devez toocreate une **bibliothèque de classes .NET** projet avec une classe qui implémente cette **IDotNetActivity** interface.</span><span class="sxs-lookup"><span data-stu-id="d50ae-215">toocreate a .NET custom activity that you can use in an Azure Data Factory pipeline, you need toocreate a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="d50ae-216">Cette interface possède une seule méthode : **Execute**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-216">This interface has only one method: **Execute**.</span></span> <span data-ttu-id="d50ae-217">Voici la signature hello de méthode hello :</span><span class="sxs-lookup"><span data-stu-id="d50ae-217">Here is hello signature of hello method:</span></span>

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

<span data-ttu-id="d50ae-218">méthode Hello a quelques composants clés que vous avez besoin de toounderstand.</span><span class="sxs-lookup"><span data-stu-id="d50ae-218">hello method has a few key components that you need toounderstand.</span></span>

* <span data-ttu-id="d50ae-219">méthode Hello accepte quatre paramètres :</span><span class="sxs-lookup"><span data-stu-id="d50ae-219">hello method takes four parameters:</span></span>

  1. <span data-ttu-id="d50ae-220">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-220">**linkedServices**.</span></span> <span data-ttu-id="d50ae-221">Une liste énumérable de services liés qui relient les sources de données d’entrée/sortie (par exemple : stockage d’objets Blob Azure) fabrique de données toohello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-221">An enumerable list of linked services that link input/output data sources (for example: Azure Blob Storage) toohello data factory.</span></span> <span data-ttu-id="d50ae-222">Dans cet exemple, il s’agit du seul service lié de type Azure Storage utilisé à la fois pour les données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="d50ae-222">In this sample, there is only one linked service of type Azure Storage used for both input and output.</span></span>
  2. <span data-ttu-id="d50ae-223">**jeux de données**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-223">**datasets**.</span></span> <span data-ttu-id="d50ae-224">liste énumérable de jeux de données.</span><span class="sxs-lookup"><span data-stu-id="d50ae-224">This is an enumerable list of datasets.</span></span> <span data-ttu-id="d50ae-225">Vous pouvez utiliser ce emplacements de paramètre tooget hello et les schémas définis par les jeux de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="d50ae-225">You can use this parameter tooget hello locations and schemas defined by input and output datasets.</span></span>
  3. <span data-ttu-id="d50ae-226">**activity**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-226">**activity**.</span></span> <span data-ttu-id="d50ae-227">Ce paramètre représente hello calcul entité actuelle - dans ce cas, un service Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="d50ae-227">This parameter represents hello current compute entity - in this case, an Azure Batch service.</span></span>
  4. <span data-ttu-id="d50ae-228">**logger**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-228">**logger**.</span></span> <span data-ttu-id="d50ae-229">vous permet d’enregistreur d’événements Hello que écrire des commentaires de débogage cette surface comme hello « Utilisateur » pour ouvrir une session hello pipeline.</span><span class="sxs-lookup"><span data-stu-id="d50ae-229">hello logger lets you write debug comments that surface as hello “User” log for hello pipeline.</span></span>
* <span data-ttu-id="d50ae-230">méthode Hello retourne un dictionnaire qui peut être des activités personnalisées toochain utilisées ensemble dans un avenir hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-230">hello method returns a dictionary that can be used toochain custom activities together in hello future.</span></span> <span data-ttu-id="d50ae-231">Cette fonctionnalité n’est pas encore implémentée, par conséquent, renvoyer un dictionnaire vide à partir de la méthode hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-231">This feature is not implemented yet, so return an empty dictionary from hello method.</span></span>

#### <a name="procedure-create-hello-custom-activity"></a><span data-ttu-id="d50ae-232">Procédure : Créer l’activité personnalisée hello</span><span class="sxs-lookup"><span data-stu-id="d50ae-232">Procedure: Create hello custom activity</span></span>
1. <span data-ttu-id="d50ae-233">Créez un projet de bibliothèque de classes .NET dans Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="d50ae-233">Create a .NET Class Library project in Visual Studio.</span></span>

   1. <span data-ttu-id="d50ae-234">Lancez **Visual Studio 2012**/**2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-234">Launch **Visual Studio 2012**/**2013/2015**.</span></span>
   2. <span data-ttu-id="d50ae-235">Cliquez sur **fichier**, pointez trop**nouveau**, puis cliquez sur **projet**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-235">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="d50ae-236">Développez **Modèles**, puis sélectionnez **Visual C\#**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-236">Expand **Templates**, and select **Visual C\#**.</span></span> <span data-ttu-id="d50ae-237">Dans cette procédure pas à pas, vous utilisez C\#, mais vous pouvez utiliser n’importe quel langage .NET toodevelop hello personnalisée activité.</span><span class="sxs-lookup"><span data-stu-id="d50ae-237">In this walkthrough, you use C\#, but you can use any .NET language toodevelop hello custom activity.</span></span>
   4. <span data-ttu-id="d50ae-238">Sélectionnez **bibliothèque de classes** à partir de la liste hello des types de projets sur hello droite.</span><span class="sxs-lookup"><span data-stu-id="d50ae-238">Select **Class Library** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="d50ae-239">Entrez **MyDotNetActivity** pour hello **nom**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-239">Enter **MyDotNetActivity** for hello **Name**.</span></span>
   6. <span data-ttu-id="d50ae-240">Sélectionnez **C:\\ADF** pour hello **emplacement**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-240">Select **C:\\ADF** for hello **Location**.</span></span> <span data-ttu-id="d50ae-241">Créer le dossier de hello **ADF** s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="d50ae-241">Create hello folder **ADF** if it does not exist.</span></span>
   7. <span data-ttu-id="d50ae-242">Cliquez sur **OK** projet hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="d50ae-242">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="d50ae-243">Cliquez sur **outils**, pointez trop**Gestionnaire de Package NuGet**, puis cliquez sur **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-243">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="d50ae-244">Bonjour **Package Manager Console**, exécutez hello suivant commande tooimport **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-244">In hello **Package Manager Console**, execute hello following command tooimport **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="d50ae-245">Hello d’importation **Azure Storage** package NuGet dans le projet de toohello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-245">Import hello **Azure Storage** NuGet package in toohello project.</span></span> <span data-ttu-id="d50ae-246">Vous avez besoin de ce package, car vous utilisez des API de stockage d’objets Blob hello dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="d50ae-246">You need this package because you use hello Blob storage API in this sample.</span></span>

    ```powershell
    Install-Package Azure.Storage
    ```
5. <span data-ttu-id="d50ae-247">Ajoutez hello suivant **à l’aide de** directives toohello source fichier hello projet.</span><span class="sxs-lookup"><span data-stu-id="d50ae-247">Add hello following **using** directives toohello source file in hello project.</span></span>

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
6. <span data-ttu-id="d50ae-248">Modifier le nom de hello hello **espace de noms** trop**MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-248">Change hello name of hello **namespace** too**MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="d50ae-249">Modifier le nom hello de classe hello trop**MyDotNetActivity** et la dériver de hello **IDotNetActivity** interface comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d50ae-249">Change hello name of hello class too**MyDotNetActivity** and derive it from hello **IDotNetActivity** interface as shown below.</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="d50ae-250">Hello d’implémenter (Ajouter) **Execute** méthode Hello **IDotNetActivity** interface toohello **MyDotNetActivity** classe et copie hello suivant l’exemple de méthode toohello de code.</span><span class="sxs-lookup"><span data-stu-id="d50ae-250">Implement (Add) hello **Execute** method of hello **IDotNetActivity** interface toohello **MyDotNetActivity** class and copy hello following sample code toohello method.</span></span> <span data-ttu-id="d50ae-251">Consultez hello [exécuter une méthode](#execute-method) section pour une explication pour la logique de hello utilisée dans cette méthode.</span><span class="sxs-lookup"><span data-stu-id="d50ae-251">See hello [Execute Method](#execute-method) section for explanation for hello logic used in this method.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
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
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // create storage client for input. Pass hello connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // initialize hello continuation token before using it in hello do-while loop.
       BlobContinuationToken continuationToken = null;
       do
       {   // get hello list of input blobs from hello input storage client object.
           BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                    true,
                                    BlobListingDetails.Metadata,
                                    null,
                                    continuationToken,
                                    null,
                                    null);
    
           // Calculate method returns hello number of occurrences of
           // hello search term (“Microsoft”) in each blob associated
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // create a blob and upload hello output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} toohello output blob", output);
       outputBlob.UploadText(output);
    
       // hello dictionary can be used toochain custom activities together in hello future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="d50ae-252">Ajoutez hello suivant classe toohello de méthodes d’assistance.</span><span class="sxs-lookup"><span data-stu-id="d50ae-252">Add hello following helper methods toohello class.</span></span> <span data-ttu-id="d50ae-253">Ces méthodes sont appelées par hello **Execute** (méthode).</span><span class="sxs-lookup"><span data-stu-id="d50ae-253">These methods are invoked by hello **Execute** method.</span></span> <span data-ttu-id="d50ae-254">Plus important encore, hello **Calculate** méthode isole code hello qui effectue une itération dans chaque objet blob.</span><span class="sxs-lookup"><span data-stu-id="d50ae-254">Most importantly, hello **Calculate** method isolates hello code that iterates through each blob.</span></span>

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
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
    /// Gets hello fileName value from hello input/output dataset.
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
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
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
               output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
           }
       }
       return output;
    }
    ```
    <span data-ttu-id="d50ae-255">Hello **GetFolderPath** méthode renvoie hello chemin toohello dossier ce Bonjour dataset points tooand Bonjour **GetFileName** méthode retourne les nom hello de hello/fichier blob qui hello pour les points de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="d50ae-255">hello **GetFolderPath** method returns hello path toohello folder that hello dataset points tooand hello **GetFileName** method returns hello name of hello blob/file that hello dataset points to.</span></span>

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    <span data-ttu-id="d50ae-256">Hello **Calculate** (méthode) calcule le nombre de hello d’instances du mot clé **Microsoft** dans les fichiers d’entrée de hello (objets BLOB dans le dossier de hello).</span><span class="sxs-lookup"><span data-stu-id="d50ae-256">hello **Calculate** method calculates hello number of instances of keyword **Microsoft** in hello input files (blobs in hello folder).</span></span> <span data-ttu-id="d50ae-257">terme de recherche Hello (« Microsoft ») est codé en dur dans le code hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-257">hello search term (“Microsoft”) is hard-coded in hello code.</span></span>

1. <span data-ttu-id="d50ae-258">Compilez le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-258">Compile hello project.</span></span> <span data-ttu-id="d50ae-259">Cliquez sur **générer** de hello menu et cliquez sur **générer la Solution**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-259">Click **Build** from hello menu and click **Build Solution**.</span></span>
2. <span data-ttu-id="d50ae-260">Lancez **l’Explorateur Windows**et accédez trop**bin\\déboguer** ou **bin\\release** dossier en fonction de type hello de build.</span><span class="sxs-lookup"><span data-stu-id="d50ae-260">Launch **Windows Explorer**, and navigate too**bin\\debug** or **bin\\release** folder depending on hello type of build.</span></span>
3. <span data-ttu-id="d50ae-261">Créer un fichier zip **MyDotNetActivity.zip** qui contient tous les fichiers binaires de hello Bonjour  **\\bin\\déboguer** dossier.</span><span class="sxs-lookup"><span data-stu-id="d50ae-261">Create a zip file **MyDotNetActivity.zip** that contains all hello binaries in hello **\\bin\\Debug** folder.</span></span> <span data-ttu-id="d50ae-262">Vous souhaiterez peut-être tooinclude hello MyDotNetActivity. **pdb** de fichiers afin que vous obtenez des informations supplémentaires telles que le numéro de ligne dans le code source hello qui a provoqué le problème de hello lorsqu’une défaillance se produit.</span><span class="sxs-lookup"><span data-stu-id="d50ae-262">You may want tooinclude hello MyDotNetActivity.**pdb** file so that you get additional details such as line number in hello source code that caused hello issue when a failure occurs.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. <span data-ttu-id="d50ae-263">Télécharger **MyDotNetActivity.zip** comme un conteneur d’objets blob blob toohello : `customactivitycontainer` Bonjour Azure stockage d’objets blob que hello **StorageLinkedService** service Bonjour lié  **ADFTutorialDataFactory** utilise.</span><span class="sxs-lookup"><span data-stu-id="d50ae-263">Upload **MyDotNetActivity.zip** as a blob toohello blob container: `customactivitycontainer` in hello Azure blob storage that hello **StorageLinkedService** linked service in hello **ADFTutorialDataFactory** uses.</span></span> <span data-ttu-id="d50ae-264">Créer le conteneur d’objets blob hello `customactivitycontainer` si elle n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="d50ae-264">Create hello blob container `customactivitycontainer` if it does not already exist.</span></span>

#### <a name="execute-method"></a><span data-ttu-id="d50ae-265">Méthode Execute</span><span class="sxs-lookup"><span data-stu-id="d50ae-265">Execute method</span></span>
<span data-ttu-id="d50ae-266">Cette section fournit plus de détails et remarques sur le code hello Bonjour méthode Execute.</span><span class="sxs-lookup"><span data-stu-id="d50ae-266">This section provides more details and notes about hello code in hello Execute method.</span></span>

1. <span data-ttu-id="d50ae-267">membres Hello pour itérer la collection d’entrée de hello sont trouvent dans hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) espace de noms.</span><span class="sxs-lookup"><span data-stu-id="d50ae-267">hello members for iterating through hello input collection are found in hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span></span> <span data-ttu-id="d50ae-268">Itération dans la collection d’objets blob hello requiert l’utilisation de hello **BlobContinuationToken** classe.</span><span class="sxs-lookup"><span data-stu-id="d50ae-268">Iterating through hello blob collection requires using hello **BlobContinuationToken** class.</span></span> <span data-ttu-id="d50ae-269">Fondamentalement, vous devez utiliser un-boucle avec jeton hello en tant que mécanisme de hello pour quitter hello boucle while.</span><span class="sxs-lookup"><span data-stu-id="d50ae-269">In essence, you must use a do-while loop with hello token as hello mechanism for exiting hello loop.</span></span> <span data-ttu-id="d50ae-270">Pour plus d’informations, consultez [comment toouse stockage d’objets Blob à partir de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="d50ae-270">For more information, see [How toouse Blob storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="d50ae-271">Une boucle de base est illustrée ici :</span><span class="sxs-lookup"><span data-stu-id="d50ae-271">A basic loop is shown here:</span></span>

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
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
   <span data-ttu-id="d50ae-272">Consultez la documentation de hello pour hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) méthode pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="d50ae-272">See hello documentation for hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method for details.</span></span>
2. <span data-ttu-id="d50ae-273">Hello code de travail dans le jeu d’objets BLOB hello logiquement dans hello faire-une boucle while.</span><span class="sxs-lookup"><span data-stu-id="d50ae-273">hello code for working through hello set of blobs logically goes within hello do-while loop.</span></span> <span data-ttu-id="d50ae-274">Bonjour **Execute** (méthode), hello-lors de la boucle transmet liste hello d’objets BLOB méthode tooa nommée **Calculate**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-274">In hello **Execute** method, hello do-while loop passes hello list of blobs tooa method named **Calculate**.</span></span> <span data-ttu-id="d50ae-275">méthode Hello retourne une variable chaîne nommée **sortie** qui est le résultat de hello d’avoir parcouru de tous les objets BLOB de hello dans le segment de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-275">hello method returns a string variable named **output** that is hello result of having iterated through all hello blobs in hello segment.</span></span>

   <span data-ttu-id="d50ae-276">Elle retourne le nombre de hello d’occurrences du terme de recherche hello (**Microsoft**) dans l’objet blob de hello passé toohello **Calculate** (méthode).</span><span class="sxs-lookup"><span data-stu-id="d50ae-276">It returns hello number of occurrences of hello search term (**Microsoft**) in hello blob passed toohello **Calculate** method.</span></span>

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. <span data-ttu-id="d50ae-277">Une fois hello **Calculate** méthode a procédé hello, elle doit être écrite tooa nouvel objet blob.</span><span class="sxs-lookup"><span data-stu-id="d50ae-277">Once hello **Calculate** method has done hello work, it must be written tooa new blob.</span></span> <span data-ttu-id="d50ae-278">Par conséquent, pour chaque jeu d’objets BLOB traité, un nouvel objet blob peut être écrites avec les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-278">So for every set of blobs processed, a new blob can be written with hello results.</span></span> <span data-ttu-id="d50ae-279">un nouvel objet blob toowrite tooa, le premier jeu de données de la sortie de hello rechercher.</span><span class="sxs-lookup"><span data-stu-id="d50ae-279">toowrite tooa new blob, first find hello output dataset.</span></span>

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. <span data-ttu-id="d50ae-280">code de Hello appelle également une méthode d’assistance : **GetFolderPath** chemin du dossier hello tooretrieve (nom de conteneur de stockage hello).</span><span class="sxs-lookup"><span data-stu-id="d50ae-280">hello code also calls a helper method: **GetFolderPath** tooretrieve hello folder path (hello storage container name).</span></span>

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   <span data-ttu-id="d50ae-281">Hello **GetFolderPath** casts hello DataSet objet tooan AzureBlobDataSet, qui a une propriété nommée FolderPath.</span><span class="sxs-lookup"><span data-stu-id="d50ae-281">hello **GetFolderPath** casts hello DataSet object tooan AzureBlobDataSet, which has a property named FolderPath.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. <span data-ttu-id="d50ae-282">appels de code Bonjour Bonjour **GetFileName** méthode tooretrieve hello fichier nom (blob).</span><span class="sxs-lookup"><span data-stu-id="d50ae-282">hello code calls hello **GetFileName** method tooretrieve hello file name (blob name).</span></span> <span data-ttu-id="d50ae-283">code de Hello est similaire toohello au-dessus de chemin d’accès du dossier code tooget hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-283">hello code is similar toohello above code tooget hello folder path.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. <span data-ttu-id="d50ae-284">nom de Hello du fichier de hello est écrit en créant un objet URI.</span><span class="sxs-lookup"><span data-stu-id="d50ae-284">hello name of hello file is written by creating a URI object.</span></span> <span data-ttu-id="d50ae-285">constructeur d’URI Hello utilise hello **BlobEndpoint** nom du conteneur de propriété tooreturn hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-285">hello URI constructor uses hello **BlobEndpoint** property tooreturn hello container name.</span></span> <span data-ttu-id="d50ae-286">nom de fichier et le chemin du dossier Hello sont ajoutés tooconstruct hello sortie URI d’objet blob.</span><span class="sxs-lookup"><span data-stu-id="d50ae-286">hello folder path and file name are added tooconstruct hello output blob URI.</span></span>  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. <span data-ttu-id="d50ae-287">Hello nom de fichier de hello a été écrit et vous pouvez maintenant écrire la chaîne de sortie hello de hello **Calculate** un nouvel objet blob méthode tooa :</span><span class="sxs-lookup"><span data-stu-id="d50ae-287">hello name of hello file has been written and now you can write hello output string from hello **Calculate** method tooa new blob:</span></span>

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a><span data-ttu-id="d50ae-288">Créer la fabrique de données hello</span><span class="sxs-lookup"><span data-stu-id="d50ae-288">Create hello data factory</span></span>
<span data-ttu-id="d50ae-289">Bonjour [créer l’activité personnalisée hello](#create-the-custom-activity) section, vous avez créé une activité personnalisée et téléchargé hello zip avec des fichiers binaires et hello PDB fichier tooan conteneur d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="d50ae-289">In hello [Create hello custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded hello zip file with binaries and hello PDB file tooan Azure blob container.</span></span> <span data-ttu-id="d50ae-290">Dans cette section, vous créez un Azure **fabrique de données** avec un **pipeline** qui utilise hello **activité personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-290">In this section, you create an Azure **data factory** with a **pipeline** that uses hello **custom activity**.</span></span>

<span data-ttu-id="d50ae-291">Hello dataset d’entrée d’activité personnalisée hello représente des objets BLOB de hello (fichiers) dans le dossier d’entrée de hello (`mycontainer\\inputfolder`) dans le stockage blob.</span><span class="sxs-lookup"><span data-stu-id="d50ae-291">hello input dataset for hello custom activity represents hello blobs (files) in hello input folder (`mycontainer\\inputfolder`) in blob storage.</span></span> <span data-ttu-id="d50ae-292">jeu de données de sortie Hello d’activité hello représente des objets BLOB de sortie hello dans le dossier de sortie hello (`mycontainer\\outputfolder`) dans le stockage blob.</span><span class="sxs-lookup"><span data-stu-id="d50ae-292">hello output dataset for hello activity represents hello output blobs in hello output folder (`mycontainer\\outputfolder`) in blob storage.</span></span>

<span data-ttu-id="d50ae-293">Supprimer un ou plusieurs fichiers dans les dossiers d’entrée hello :</span><span class="sxs-lookup"><span data-stu-id="d50ae-293">Drop one or more files in hello input folders:</span></span>

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

<span data-ttu-id="d50ae-294">Par exemple, faites glisser un fichier (fichier.txt) avec hello suivant contenu dans chacun des dossiers de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-294">For example, drop one file (file.txt) with hello following content into each of hello folders.</span></span>

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="d50ae-295">Chaque dossier d’entrée correspond tranche tooa dans Azure Data Factory, même si le dossier de hello a 2 ou plusieurs fichiers.</span><span class="sxs-lookup"><span data-stu-id="d50ae-295">Each input folder corresponds tooa slice in Azure Data Factory even if hello folder has 2 or more files.</span></span> <span data-ttu-id="d50ae-296">Lorsque chaque tranche est traitée par le pipeline de hello, activité personnalisée hello itère tous les objets BLOB de hello dans le dossier d’entrée de hello pour cette tranche.</span><span class="sxs-lookup"><span data-stu-id="d50ae-296">When each slice is processed by hello pipeline, hello custom activity iterates through all hello blobs in hello input folder for that slice.</span></span>

<span data-ttu-id="d50ae-297">Vous voyez cinq fichiers de sortie avec hello même contenu.</span><span class="sxs-lookup"><span data-stu-id="d50ae-297">You see five output files with hello same content.</span></span> <span data-ttu-id="d50ae-298">Par exemple, le fichier de sortie hello de traiter le fichier hello dans le dossier de hello 2015-11-16-00 a hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="d50ae-298">For example, hello output file from processing hello file in hello 2015-11-16-00 folder has hello following content:</span></span>

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

<span data-ttu-id="d50ae-299">Si vous supprimez plusieurs fichiers (fichier.txt, file2.txt, file3.txt) avec hello même contenu toohello des dossiers d’entrée, vous voyez hello suivant contenu dans le fichier de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-299">If you drop multiple files (file.txt, file2.txt, file3.txt) with hello same content toohello input folder, you see hello following content in hello output file.</span></span> <span data-ttu-id="d50ae-300">Chaque dossier (2015-11-16-00, etc.) correspondant tranche tooa dans cet exemple, même si le dossier de hello a plusieurs fichiers d’entrée.</span><span class="sxs-lookup"><span data-stu-id="d50ae-300">Each folder (2015-11-16-00, etc.) corresponds tooa slice in this sample even though hello folder has multiple input files.</span></span>

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

<span data-ttu-id="d50ae-301">fichier de sortie Hello a trois lignes à présent, un pour chaque fichier d’entrée (blob) dans le dossier hello associé à la tranche de hello (2015-11-16-00).</span><span class="sxs-lookup"><span data-stu-id="d50ae-301">hello output file has three lines now, one for each input file (blob) in hello folder associated with hello slice (2015-11-16-00).</span></span>

<span data-ttu-id="d50ae-302">Une tâche est créée pour chaque exécution d’activité.</span><span class="sxs-lookup"><span data-stu-id="d50ae-302">A task is created for each activity run.</span></span> <span data-ttu-id="d50ae-303">Dans cet exemple, il n'est qu’une seule activité dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-303">In this sample, there is only one activity in hello pipeline.</span></span> <span data-ttu-id="d50ae-304">Lorsqu’une tranche est traitée par le pipeline de hello, activité personnalisée hello s’exécute sur un secteur de traitement par lots Azure tooprocess hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-304">When a slice is processed by hello pipeline, hello custom activity runs on Azure Batch tooprocess hello slice.</span></span> <span data-ttu-id="d50ae-305">Étant donné qu’il y a cinq tranches (chacune pouvant comporter plusieurs objets blob ou fichiers), cinq tâches sont créées dans Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="d50ae-305">Since there are five slices (each slice can have multiple blobs or file), there are five tasks created in Azure Batch.</span></span> <span data-ttu-id="d50ae-306">Lorsqu’une tâche s’exécute sur le lot, il est réellement hello activité personnalisée qui est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="d50ae-306">When a task runs on Batch, it is actually hello custom activity that is running.</span></span>

<span data-ttu-id="d50ae-307">Hello, procédure pas à pas fournit des détails supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="d50ae-307">hello following walkthrough provides additional details.</span></span>

#### <a name="step-1-create-hello-data-factory"></a><span data-ttu-id="d50ae-308">Étape 1 : Créer la fabrique de données hello</span><span class="sxs-lookup"><span data-stu-id="d50ae-308">Step 1: Create hello data factory</span></span>
1. <span data-ttu-id="d50ae-309">Une fois connecté toohello [portail Azure](https://portal.azure.com/), hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d50ae-309">After logging in toohello [Azure portal](https://portal.azure.com/), do hello following steps:</span></span>

   1. <span data-ttu-id="d50ae-310">Cliquez sur **nouveau** sur le menu de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-310">Click **NEW** on hello left menu.</span></span>
   2. <span data-ttu-id="d50ae-311">Cliquez sur **données + Analytique** Bonjour **nouveau** panneau.</span><span class="sxs-lookup"><span data-stu-id="d50ae-311">Click **Data + Analytics** in hello **New** blade.</span></span>
   3. <span data-ttu-id="d50ae-312">Cliquez sur **Data Factory** sur hello **analytique des données** panneau.</span><span class="sxs-lookup"><span data-stu-id="d50ae-312">Click **Data Factory** on hello **Data analytics** blade.</span></span>
2. <span data-ttu-id="d50ae-313">Bonjour **nouvelle fabrique de données** panneau, entrez **CustomActivityFactory** pour hello nom.</span><span class="sxs-lookup"><span data-stu-id="d50ae-313">In hello **New data factory** blade, enter **CustomActivityFactory** for hello Name.</span></span> <span data-ttu-id="d50ae-314">nom de Hello de fabrique de données Azure hello doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="d50ae-314">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="d50ae-315">Si vous recevez une erreur de hello : **nom de fabrique de données « CustomActivityFactory » n’est pas disponible**, modifiez le nom hello hello fabrique de données (par exemple, **yournameCustomActivityFactory**) et essayez de créer à nouveau.</span><span class="sxs-lookup"><span data-stu-id="d50ae-315">If you receive hello error: **Data factory name “CustomActivityFactory” is not available**, change hello name of hello data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>
3. <span data-ttu-id="d50ae-316">Cliquez sur **NOM DU GROUPE DE RESSOURCES**pour sélectionner un groupe de ressources existant, ou créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="d50ae-316">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="d50ae-317">Vérifiez que vous utilisez le bon abonnement de hello et région où vous souhaitez toobe de fabrique de données hello créé.</span><span class="sxs-lookup"><span data-stu-id="d50ae-317">Verify that you are using hello correct subscription and region where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="d50ae-318">Cliquez sur **créer** sur hello **nouvelle fabrique de données** panneau.</span><span class="sxs-lookup"><span data-stu-id="d50ae-318">Click **Create** on hello **New data factory** blade.</span></span>
6. <span data-ttu-id="d50ae-319">Vous voyez la fabrique de données hello en cours de création dans hello **tableau de bord** de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d50ae-319">You see hello data factory being created in hello **Dashboard** of hello Azure portal.</span></span>
7. <span data-ttu-id="d50ae-320">Une fois que la fabrique de données hello a été créé avec succès, vous voyez page de fabrique de données hello, qui vous indique hello contenu hello fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="d50ae-320">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a><span data-ttu-id="d50ae-321">Étape 2 : Créer des services liés</span><span class="sxs-lookup"><span data-stu-id="d50ae-321">Step 2: Create linked services</span></span>
<span data-ttu-id="d50ae-322">Services liés lier des magasins de données ou la fabrique de données Azure tooan de services de calcul.</span><span class="sxs-lookup"><span data-stu-id="d50ae-322">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="d50ae-323">Dans cette étape, vous liez votre **Azure Storage** compte et **Azure Batch** fabrique de données tooyour de compte.</span><span class="sxs-lookup"><span data-stu-id="d50ae-323">In this step, you link your **Azure Storage** account and **Azure Batch** account tooyour data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="d50ae-324">Créer le service lié Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="d50ae-324">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="d50ae-325">Cliquez sur hello **auteur et déployer** vignette sur hello **DATA FACTORY** panneau pour **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-325">Click hello **Author and deploy** tile on hello **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="d50ae-326">Vous consultez hello éditeur Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d50ae-326">You see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="d50ae-327">Cliquez sur **nouveau magasin de données** hello de barre de commandes et choisissez **le stockage Azure.**</span><span class="sxs-lookup"><span data-stu-id="d50ae-327">Click **New data store** on hello command bar and choose **Azure storage.**</span></span> <span data-ttu-id="d50ae-328">Vous devez voir hello script JSON pour la création d’un stockage Azure lié à service dans l’éditeur de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-328">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. <span data-ttu-id="d50ae-329">Remplacez **nom de compte** avec le nom de hello de votre compte de stockage Azure et **clé de compte** avec la clé d’accès hello Hello compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d50ae-329">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="d50ae-330">toolearn comment tooget votre stockage accéder aux clés, voir [clés d’accès afficher, copier et régénérer stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="d50ae-330">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

4. <span data-ttu-id="d50ae-331">Cliquez sur **déployer** sur toodeploy hello lié service de la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-331">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="d50ae-332">Créer un service lié Azure Batch</span><span class="sxs-lookup"><span data-stu-id="d50ae-332">Create Azure Batch linked service</span></span>
<span data-ttu-id="d50ae-333">Dans cette étape, vous créez un service lié pour votre **Azure Batch** compte d’activité personnalisée de la fabrique de données utilisé toorun hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-333">In this step, you create a linked service for your **Azure Batch** account that is used toorun hello Data Factory custom activity.</span></span>

1. <span data-ttu-id="d50ae-334">Cliquez sur **nouveau calcul** hello de barre de commandes et choisissez **Azure Batch.**</span><span class="sxs-lookup"><span data-stu-id="d50ae-334">Click **New compute** on hello command bar and choose **Azure Batch.**</span></span> <span data-ttu-id="d50ae-335">Vous devez voir hello script JSON pour la création d’un traitement par lots Azure lié à service dans l’éditeur de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-335">You should see hello JSON script for creating an Azure Batch linked service in hello editor.</span></span>
2. <span data-ttu-id="d50ae-336">Bonjour script JSON :</span><span class="sxs-lookup"><span data-stu-id="d50ae-336">In hello JSON script:</span></span>

   1. <span data-ttu-id="d50ae-337">Remplacez **nom de compte** avec nom hello de votre compte Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="d50ae-337">Replace **account name** with hello name of your Azure Batch account.</span></span>
   2. <span data-ttu-id="d50ae-338">Remplacez **clé d’accès** avec la clé d’accès hello Hello compte Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="d50ae-338">Replace **access key** with hello access key of hello Azure Batch account.</span></span>
   3. <span data-ttu-id="d50ae-339">Entrez les ID de hello du pool de hello pour hello **poolName** propriété**.**</span><span class="sxs-lookup"><span data-stu-id="d50ae-339">Enter hello ID of hello pool for hello **poolName** property**.**</span></span> <span data-ttu-id="d50ae-340">Pour cette propriété, vous pouvez spécifier le nom de pool ou l’ID de pool.</span><span class="sxs-lookup"><span data-stu-id="d50ae-340">For this property, you can specify either pool name or pool ID.</span></span>
   4. <span data-ttu-id="d50ae-341">Entrez le lot hello URI pour hello **batchUri** propriété JSON.</span><span class="sxs-lookup"><span data-stu-id="d50ae-341">Enter hello batch URI for hello **batchUri** JSON property.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="d50ae-342">Hello **URL** de hello **Panneau de compte Azure Batch** est Bonjour suivant le format : \<accountname\>.\< région\>. batch.azure.com. Pourquoi **batchUri** propriété Bonjour JSON, vous devez trop**supprimer « accountname ».**</span><span class="sxs-lookup"><span data-stu-id="d50ae-342">hello **URL** from hello **Azure Batch account blade** is in hello following format: \<accountname\>.\<region\>.batch.azure.com. For hello **batchUri** property in hello JSON, you need too**remove "accountname."**</span></span> <span data-ttu-id="d50ae-343">à partir de l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-343">from hello URL.</span></span> <span data-ttu-id="d50ae-344">Exemple : `"batchUri": "https://eastus.batch.azure.com"`.</span><span class="sxs-lookup"><span data-stu-id="d50ae-344">Example: `"batchUri": "https://eastus.batch.azure.com"`.</span></span>
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      <span data-ttu-id="d50ae-345">Pourquoi **poolName** propriété, vous pouvez également spécifier d’ID hello du pool hello au lieu du nom de hello du pool de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-345">For hello **poolName** property, you can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>

      > [!NOTE]
      > <span data-ttu-id="d50ae-346">Hello service Data Factory ne prend en charge une option à la demande de traitement par lots Azure comme il le fait pour HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d50ae-346">hello Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="d50ae-347">Vous pouvez uniquement utiliser votre propre pool Azure Batch dans une fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="d50ae-347">You can only use your own Azure Batch pool in an Azure data factory.</span></span>
      >
      >
   5. <span data-ttu-id="d50ae-348">Spécifiez **StorageLinkedService** pour hello **linkedServiceName** propriété.</span><span class="sxs-lookup"><span data-stu-id="d50ae-348">Specify **StorageLinkedService** for hello **linkedServiceName** property.</span></span> <span data-ttu-id="d50ae-349">Vous avez créé ce service lié à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-349">You created this linked service in hello previous step.</span></span> <span data-ttu-id="d50ae-350">Ce stockage est utilisé en tant que zone de transit pour les fichiers et les journaux.</span><span class="sxs-lookup"><span data-stu-id="d50ae-350">This storage is used as a staging area for files and logs.</span></span>
3. <span data-ttu-id="d50ae-351">Cliquez sur **déployer** sur toodeploy hello lié service de la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-351">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

#### <a name="step-3-create-datasets"></a><span data-ttu-id="d50ae-352">Étape 3 : Créer les jeux de données</span><span class="sxs-lookup"><span data-stu-id="d50ae-352">Step 3: Create datasets</span></span>
<span data-ttu-id="d50ae-353">Dans cette étape, vous créez une entrée de toorepresent de jeux de données et les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="d50ae-353">In this step, you create datasets toorepresent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="d50ae-354">Créer le jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="d50ae-354">Create input dataset</span></span>
1. <span data-ttu-id="d50ae-355">Bonjour **éditeur** pour hello fabrique de données, cliquez sur **nouveau dataset** bouton de barre d’outils hello et cliquez sur **le stockage Blob Azure** à partir du menu déroulant de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-355">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="d50ae-356">Remplacez hello JSON dans le volet de droite hello hello suivant extrait de code JSON :</span><span class="sxs-lookup"><span data-stu-id="d50ae-356">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

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

    <span data-ttu-id="d50ae-357">Plus loin dans cette procédure pas à pas, vous allez créer un pipeline associé à l’heure de début 2015-11-16T00:00:00Z et à l’heure de fin 2015-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="d50ae-357">You create a pipeline later in this walkthrough with start time: 2015-11-16T00:00:00Z and end time: 2015-11-16T05:00:00Z.</span></span> <span data-ttu-id="d50ae-358">Elle est planifiée tooproduce données **toutes les heures**, il y a 5 tranches d’entrée/sortie (entre **00**: 00:00 -\> **05**: 00:00).</span><span class="sxs-lookup"><span data-stu-id="d50ae-358">It is scheduled tooproduce data **hourly**, so there are 5 input/output slices (between **00**:00:00 -\> **05**:00:00).</span></span>

    <span data-ttu-id="d50ae-359">Hello **fréquence** et **intervalle** de jeu de données d’entrée hello est défini trop**heure** et **1**, ce qui signifie que hello entrée tranche est disponible toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="d50ae-359">hello **frequency** and **interval** for hello input dataset is set too**Hour** and **1**, which means that hello input slice is available hourly.</span></span>

    <span data-ttu-id="d50ae-360">Voici les heures de début hello pour chaque secteur, qui sont représentées par **SliceStart** variable système Bonjour ci-dessus extrait de code JSON.</span><span class="sxs-lookup"><span data-stu-id="d50ae-360">Here are hello start times for each slice, which is represented by **SliceStart** system variable in hello above JSON snippet.</span></span>

    | <span data-ttu-id="d50ae-361">**Tranche**</span><span class="sxs-lookup"><span data-stu-id="d50ae-361">**Slice**</span></span> | <span data-ttu-id="d50ae-362">**Heure de début**</span><span class="sxs-lookup"><span data-stu-id="d50ae-362">**Start time**</span></span>          |
    |-----------|-------------------------|
    | <span data-ttu-id="d50ae-363">1</span><span class="sxs-lookup"><span data-stu-id="d50ae-363">1</span></span>         | <span data-ttu-id="d50ae-364">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="d50ae-364">2015-11-16T**00**:00:00</span></span> |
    | <span data-ttu-id="d50ae-365">2</span><span class="sxs-lookup"><span data-stu-id="d50ae-365">2</span></span>         | <span data-ttu-id="d50ae-366">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="d50ae-366">2015-11-16T**01**:00:00</span></span> |
    | <span data-ttu-id="d50ae-367">3</span><span class="sxs-lookup"><span data-stu-id="d50ae-367">3</span></span>         | <span data-ttu-id="d50ae-368">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="d50ae-368">2015-11-16T**02**:00:00</span></span> |
    | <span data-ttu-id="d50ae-369">4</span><span class="sxs-lookup"><span data-stu-id="d50ae-369">4</span></span>         | <span data-ttu-id="d50ae-370">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="d50ae-370">2015-11-16T**03**:00:00</span></span> |
    | <span data-ttu-id="d50ae-371">5</span><span class="sxs-lookup"><span data-stu-id="d50ae-371">5</span></span>         | <span data-ttu-id="d50ae-372">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="d50ae-372">2015-11-16T**04**:00:00</span></span> |

    <span data-ttu-id="d50ae-373">Hello **folderPath** est calculée à l’aide de partie de hello année, mois, jour et heure de l’heure de début de tranche hello (**SliceStart**).</span><span class="sxs-lookup"><span data-stu-id="d50ae-373">hello **folderPath** is calculated by using hello year, month, day, and hour part of hello slice start time (**SliceStart**).</span></span> <span data-ttu-id="d50ae-374">Par conséquent, voici comment un dossier d’entrée est mappé tooa tranche.</span><span class="sxs-lookup"><span data-stu-id="d50ae-374">Therefore, here is how an input folder is mapped tooa slice.</span></span>

    | <span data-ttu-id="d50ae-375">**Tranche**</span><span class="sxs-lookup"><span data-stu-id="d50ae-375">**Slice**</span></span> | <span data-ttu-id="d50ae-376">**Heure de début**</span><span class="sxs-lookup"><span data-stu-id="d50ae-376">**Start time**</span></span>          | <span data-ttu-id="d50ae-377">**Dossier d’entrée**</span><span class="sxs-lookup"><span data-stu-id="d50ae-377">**Input folder**</span></span>  |
    |-----------|-------------------------|-------------------|
    | <span data-ttu-id="d50ae-378">1</span><span class="sxs-lookup"><span data-stu-id="d50ae-378">1</span></span>         | <span data-ttu-id="d50ae-379">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="d50ae-379">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="d50ae-380">2015-11-16-**00**</span><span class="sxs-lookup"><span data-stu-id="d50ae-380">2015-11-16-**00**</span></span> |
    | <span data-ttu-id="d50ae-381">2</span><span class="sxs-lookup"><span data-stu-id="d50ae-381">2</span></span>         | <span data-ttu-id="d50ae-382">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="d50ae-382">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="d50ae-383">2015-11-16-**01**</span><span class="sxs-lookup"><span data-stu-id="d50ae-383">2015-11-16-**01**</span></span> |
    | <span data-ttu-id="d50ae-384">3</span><span class="sxs-lookup"><span data-stu-id="d50ae-384">3</span></span>         | <span data-ttu-id="d50ae-385">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="d50ae-385">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="d50ae-386">2015-11-16-**02**</span><span class="sxs-lookup"><span data-stu-id="d50ae-386">2015-11-16-**02**</span></span> |
    | <span data-ttu-id="d50ae-387">4</span><span class="sxs-lookup"><span data-stu-id="d50ae-387">4</span></span>         | <span data-ttu-id="d50ae-388">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="d50ae-388">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="d50ae-389">2015-11-16-**03**</span><span class="sxs-lookup"><span data-stu-id="d50ae-389">2015-11-16-**03**</span></span> |
    | <span data-ttu-id="d50ae-390">5</span><span class="sxs-lookup"><span data-stu-id="d50ae-390">5</span></span>         | <span data-ttu-id="d50ae-391">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="d50ae-391">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="d50ae-392">2015-11-16-**04**</span><span class="sxs-lookup"><span data-stu-id="d50ae-392">2015-11-16-**04**</span></span> |

1. <span data-ttu-id="d50ae-393">Cliquez sur **déployer** hello toocreate de barre d’outils et déployer hello **InputDataset** table.</span><span class="sxs-lookup"><span data-stu-id="d50ae-393">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset** table.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="d50ae-394">Créer un jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="d50ae-394">Create output dataset</span></span>
<span data-ttu-id="d50ae-395">Dans cette étape, vous créez un autre jeu de données de type de données de sortie AzureBlob toorepresent hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-395">In this step, you create another dataset of type AzureBlob toorepresent hello output data.</span></span>

1. <span data-ttu-id="d50ae-396">Bonjour **éditeur** pour hello fabrique de données, cliquez sur **nouveau dataset** bouton de barre d’outils hello et cliquez sur **le stockage Blob Azure** à partir du menu déroulant de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-396">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="d50ae-397">Remplacez hello JSON dans le volet de droite hello hello suivant extrait de code JSON :</span><span class="sxs-lookup"><span data-stu-id="d50ae-397">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

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

    <span data-ttu-id="d50ae-398">Un objet blob/fichier de sortie est généré pour chaque tranche d’entrée.</span><span class="sxs-lookup"><span data-stu-id="d50ae-398">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="d50ae-399">Voici la procédure de nommage des fichiers de sortie pour chaque tranche.</span><span class="sxs-lookup"><span data-stu-id="d50ae-399">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="d50ae-400">Tous les fichiers de sortie hello sont générés dans un dossier de sortie : `mycontainer\\outputfolder`.</span><span class="sxs-lookup"><span data-stu-id="d50ae-400">All hello output files are generated in one output folder: `mycontainer\\outputfolder`.</span></span>

    | <span data-ttu-id="d50ae-401">**Tranche**</span><span class="sxs-lookup"><span data-stu-id="d50ae-401">**Slice**</span></span> | <span data-ttu-id="d50ae-402">**Heure de début**</span><span class="sxs-lookup"><span data-stu-id="d50ae-402">**Start time**</span></span>          | <span data-ttu-id="d50ae-403">**Fichier de sortie**</span><span class="sxs-lookup"><span data-stu-id="d50ae-403">**Output file**</span></span>       |
    |-----------|-------------------------|-----------------------|
    | <span data-ttu-id="d50ae-404">1</span><span class="sxs-lookup"><span data-stu-id="d50ae-404">1</span></span>         | <span data-ttu-id="d50ae-405">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="d50ae-405">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="d50ae-406">2015-11-16-**00.txt**</span><span class="sxs-lookup"><span data-stu-id="d50ae-406">2015-11-16-**00.txt**</span></span> |
    | <span data-ttu-id="d50ae-407">2</span><span class="sxs-lookup"><span data-stu-id="d50ae-407">2</span></span>         | <span data-ttu-id="d50ae-408">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="d50ae-408">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="d50ae-409">2015-11-16-**01.txt**</span><span class="sxs-lookup"><span data-stu-id="d50ae-409">2015-11-16-**01.txt**</span></span> |
    | <span data-ttu-id="d50ae-410">3</span><span class="sxs-lookup"><span data-stu-id="d50ae-410">3</span></span>         | <span data-ttu-id="d50ae-411">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="d50ae-411">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="d50ae-412">2015-11-16-**02.txt**</span><span class="sxs-lookup"><span data-stu-id="d50ae-412">2015-11-16-**02.txt**</span></span> |
    | <span data-ttu-id="d50ae-413">4</span><span class="sxs-lookup"><span data-stu-id="d50ae-413">4</span></span>         | <span data-ttu-id="d50ae-414">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="d50ae-414">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="d50ae-415">2015-11-16-**03.txt**</span><span class="sxs-lookup"><span data-stu-id="d50ae-415">2015-11-16-**03.txt**</span></span> |
    | <span data-ttu-id="d50ae-416">5</span><span class="sxs-lookup"><span data-stu-id="d50ae-416">5</span></span>         | <span data-ttu-id="d50ae-417">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="d50ae-417">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="d50ae-418">2015-11-16-**04.txt**</span><span class="sxs-lookup"><span data-stu-id="d50ae-418">2015-11-16-**04.txt**</span></span> |

    <span data-ttu-id="d50ae-419">Souvenez-vous que tous les hello des fichiers dans un dossier d’entrée (par exemple : 2015-11-16-00) font partie d’une tranche avec l’heure de début hello : 2015-11-16-00.</span><span class="sxs-lookup"><span data-stu-id="d50ae-419">Remember that all hello files in an input folder (for example: 2015-11-16-00) are part of a slice with hello start time: 2015-11-16-00.</span></span> <span data-ttu-id="d50ae-420">Lorsque cette tranche est traitée, activité personnalisée hello parcourt chaque fichier et produit une ligne dans le fichier de sortie hello avec numéro hello d’occurrences du terme de recherche (« Microsoft »).</span><span class="sxs-lookup"><span data-stu-id="d50ae-420">When this slice is processed, hello custom activity scans through each file and produces a line in hello output file with hello number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="d50ae-421">S’il existe trois fichiers dans le dossier hello 2015-11-16-00, il existe trois lignes dans le fichier de sortie hello : 2015-11-16-00.txt.</span><span class="sxs-lookup"><span data-stu-id="d50ae-421">If there are three files in hello folder 2015-11-16-00, there are three lines in hello output file: 2015-11-16-00.txt.</span></span>

1. <span data-ttu-id="d50ae-422">Cliquez sur **déployer** hello toocreate de barre d’outils et déployer hello **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-422">Click **Deploy** on hello toolbar toocreate and deploy hello **OutputDataset**.</span></span>

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a><span data-ttu-id="d50ae-423">Étape 4 : Créer et exécuter le pipeline de hello avec une activité personnalisée</span><span class="sxs-lookup"><span data-stu-id="d50ae-423">Step 4: Create and run hello pipeline with custom activity</span></span>
<span data-ttu-id="d50ae-424">Dans cette étape, vous créez un pipeline avec une activité, activité personnalisée hello est créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="d50ae-424">In this step, you create a pipeline with one activity, hello custom activity you created earlier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d50ae-425">Si vous n’avez pas téléchargé hello **fichier.txt** tooinput des dossiers dans le conteneur d’objets blob hello, le faire avant de créer le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-425">If you haven't uploaded hello **file.txt** tooinput folders in hello blob container, do so before creating hello pipeline.</span></span> <span data-ttu-id="d50ae-426">Hello **isPaused** propriété a la valeur toofalse dans le pipeline hello JSON, pour que le pipeline de hello s’exécute immédiatement comme hello **Démarrer** la date est hello passée.</span><span class="sxs-lookup"><span data-stu-id="d50ae-426">hello **isPaused** property is set toofalse in hello pipeline JSON, so hello pipeline runs immediately as hello **start** date is in hello past.</span></span>
>
>

1. <span data-ttu-id="d50ae-427">Bonjour éditeur Data Factory, cliquez sur **nouveau pipeline** sur la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-427">In hello Data Factory Editor, click **New pipeline** on hello command bar.</span></span> <span data-ttu-id="d50ae-428">Si vous ne voyez pas la commande hello, cliquez sur **... (Points de suspension)**  toosee il.</span><span class="sxs-lookup"><span data-stu-id="d50ae-428">If you do not see hello command, click **... (Ellipsis)** toosee it.</span></span>
2. <span data-ttu-id="d50ae-429">Remplacez hello JSON dans le volet de droite hello hello JSON script suivant :</span><span class="sxs-lookup"><span data-stu-id="d50ae-429">Replace hello JSON in hello right pane with hello following JSON script:</span></span>

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
   <span data-ttu-id="d50ae-430">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="d50ae-430">Note hello following points:</span></span>

   * <span data-ttu-id="d50ae-431">Il n'est qu’une seule activité dans le pipeline de hello et qui est de type : **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-431">There is only one activity in hello pipeline and that is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="d50ae-432">**AssemblyName** a la valeur nom toohello Hello DLL : **MyDotNetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-432">**AssemblyName** is set toohello name of hello DLL: **MyDotNetActivity.dll**.</span></span>
   * <span data-ttu-id="d50ae-433">**Point d’entrée** est défini trop**MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-433">**EntryPoint** is set too**MyDotNetActivityNS.MyDotNetActivity**.</span></span> <span data-ttu-id="d50ae-434">Il s’agit essentiellement de \<namespace\>.\<classname\> dans votre code.</span><span class="sxs-lookup"><span data-stu-id="d50ae-434">It is basically \<namespace\>.\<classname\> in your code.</span></span>
   * <span data-ttu-id="d50ae-435">**PackageLinkedService** est défini trop**StorageLinkedService** qui pointe le stockage d’objets blob toohello qui contient le fichier zip d’activité personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-435">**PackageLinkedService** is set too**StorageLinkedService** that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="d50ae-436">Si vous utilisez des comptes de stockage Azure différents pour les fichiers d’entrée/sortie et le fichier zip d’activité personnalisée hello, vous avez toocreate un autre Azure Storage service lié.</span><span class="sxs-lookup"><span data-stu-id="d50ae-436">If you are using different Azure Storage accounts for input/output files and hello custom activity zip file, you have toocreate another Azure Storage linked service.</span></span> <span data-ttu-id="d50ae-437">Cet article suppose que vous utilisez hello même compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d50ae-437">This article assumes that you are using hello same Azure Storage account.</span></span>
   * <span data-ttu-id="d50ae-438">**PackageFile** est défini trop**customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-438">**PackageFile** is set too**customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="d50ae-439">Il est au format de hello : \<containerforthezip\>/\<nameofthezip.zip\>.</span><span class="sxs-lookup"><span data-stu-id="d50ae-439">It is in hello format: \<containerforthezip\>/\<nameofthezip.zip\>.</span></span>
   * <span data-ttu-id="d50ae-440">activité personnalisée Hello prend **InputDataset** en tant qu’entrée et **OutputDataset** en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="d50ae-440">hello custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="d50ae-441">Hello **linkedServiceName** toohello la propriété d’activité personnalisée hello pointe **AzureBatchLinkedService**, ce qui indique à Azure Data Factory pour cette activité personnalisée hello doit toorun sur Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="d50ae-441">hello **linkedServiceName** property of hello custom activity points toohello **AzureBatchLinkedService**, which tells Azure Data Factory that hello custom activity needs toorun on Azure Batch.</span></span>
   * <span data-ttu-id="d50ae-442">Hello **concurrency** paramètre est important.</span><span class="sxs-lookup"><span data-stu-id="d50ae-442">hello **concurrency** setting is important.</span></span> <span data-ttu-id="d50ae-443">Si vous utilisez la valeur par défaut de hello, qui est 1, même si vous disposez de 2 ou de plusieurs nœuds dans le pool de traitement par lots Azure hello, tranches de hello sont traitées une après l’autre.</span><span class="sxs-lookup"><span data-stu-id="d50ae-443">If you use hello default value, which is 1, even if you have 2 or more compute nodes in hello Azure Batch pool, hello slices are processed one after another.</span></span> <span data-ttu-id="d50ae-444">Par conséquent, vous prenez pas parti des capacités de traitement parallèle de hello de traitement par lots Azure.</span><span class="sxs-lookup"><span data-stu-id="d50ae-444">Therefore, you are not taking advantage of hello parallel processing capability of Azure Batch.</span></span> <span data-ttu-id="d50ae-445">Si vous définissez **concurrency** tooa plus élevée, par exemple 2, cela signifie que deux tranches (correspond tootwo des tâches de traitement par lots Azure) peuvent être traités en hello même moment, dans ce cas, les deux ordinateurs virtuels de hello Bonjour Azure Batch pool sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="d50ae-445">If you set **concurrency** tooa higher value, say 2, it means that two slices (corresponds tootwo tasks in Azure Batch) can be processed at hello same time, in which case, both hello VMs in hello Azure Batch pool are utilized.</span></span> <span data-ttu-id="d50ae-446">Par conséquent, définir concurrency, propriété hello en conséquence.</span><span class="sxs-lookup"><span data-stu-id="d50ae-446">Therefore, set hello concurrency property appropriately.</span></span>
   * <span data-ttu-id="d50ae-447">Par défaut, une seule tâche (tranche) est exécutée sur une machine virtuelle à un moment donné.</span><span class="sxs-lookup"><span data-stu-id="d50ae-447">Only one task (slice) is executed on a VM at any point by default.</span></span> <span data-ttu-id="d50ae-448">Hello raison est que, par défaut, hello **Maximum de tâches par ordinateur virtuel** a la valeur too1 pour un pool de traitement par lots Azure.</span><span class="sxs-lookup"><span data-stu-id="d50ae-448">hello reason is that, by default, hello **Maximum tasks per VM** is set too1 for an Azure Batch pool.</span></span> <span data-ttu-id="d50ae-449">Dans le cadre des conditions préalables, vous avez créé un pool avec cette too2 set de propriété, donc deux tranches de fabrique de données peuvent s’exécuter sur un ordinateur virtuel à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="d50ae-449">As part of prerequisites, you created a pool with this property set too2, so two Data Factory slices can be running on a VM at hello same time.</span></span>

    -   <span data-ttu-id="d50ae-450">**isPaused** propriété a la valeur toofalse par défaut.</span><span class="sxs-lookup"><span data-stu-id="d50ae-450">**isPaused** property is set toofalse by default.</span></span> <span data-ttu-id="d50ae-451">pipeline de Hello s’exécute immédiatement dans cet exemple, car le début des tranches de hello Bonjour passées.</span><span class="sxs-lookup"><span data-stu-id="d50ae-451">hello pipeline runs immediately in this example because hello slices start in hello past.</span></span> <span data-ttu-id="d50ae-452">Vous pouvez définir ce pipeline de propriété tootrue toopause hello et affectez-lui arrière toofalse toorestart.</span><span class="sxs-lookup"><span data-stu-id="d50ae-452">You can set this property tootrue toopause hello pipeline and set it back toofalse toorestart.</span></span>

    -   <span data-ttu-id="d50ae-453">Hello **Démarrer** temps et **fin** fois éloignés de cinq heures et tranches de produits toutes les heures, afin de cinq tranches sont produits par le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-453">hello **start** time and **end** times are five hours apart and slices are produced hourly, so five slices are produced by hello pipeline.</span></span>

1. <span data-ttu-id="d50ae-454">Cliquez sur **déployer** sur le pipeline de hello toodeploy de barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-454">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span>

#### <a name="step-5-test-hello-pipeline"></a><span data-ttu-id="d50ae-455">Étape 5 : Tester le pipeline de hello</span><span class="sxs-lookup"><span data-stu-id="d50ae-455">Step 5: Test hello pipeline</span></span>
<span data-ttu-id="d50ae-456">Dans cette étape, vous tester le pipeline de hello en supprimant les fichiers dans des dossiers d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-456">In this step, you test hello pipeline by dropping files into hello input folders.</span></span> <span data-ttu-id="d50ae-457">Commençons par le pipeline de hello test avec un fichier par un seul dossier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="d50ae-457">Let’s start with testing hello pipeline with one file per one input folder.</span></span>

1. <span data-ttu-id="d50ae-458">Dans le panneau de la fabrique de données hello Bonjour portail Azure, cliquez sur **diagramme**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-458">In hello Data Factory blade in hello Azure portal, click **Diagram**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. <span data-ttu-id="d50ae-459">Dans la vue de diagramme hello, double-cliquez sur le jeu de données d’entrée : **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-459">In hello diagram view, double-click input dataset: **InputDataset**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. <span data-ttu-id="d50ae-460">Vous devez voir hello **InputDataset** panneau avec toutes les cinq tranches prêt.</span><span class="sxs-lookup"><span data-stu-id="d50ae-460">You should see hello **InputDataset** blade with all five slices ready.</span></span> <span data-ttu-id="d50ae-461">Hello d’avis **l’heure de début de la tranche** et **heure de fin de la tranche** pour chaque secteur.</span><span class="sxs-lookup"><span data-stu-id="d50ae-461">Notice hello **SLICE START TIME** and **SLICE END TIME** for each slice.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. <span data-ttu-id="d50ae-462">Bonjour **vue de diagramme**, cliquez maintenant sur **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-462">In hello **Diagram View**, now click **OutputDataset**.</span></span>
5. <span data-ttu-id="d50ae-463">Vous devez voir que les cinq tranches de sortie hello sont dans l’état prêt hello si elles ont déjà été générés.</span><span class="sxs-lookup"><span data-stu-id="d50ae-463">You should see that hello five output slices are in hello Ready state if they have already been produced.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. <span data-ttu-id="d50ae-464">Hello de tooview portail Azure utilisation **tâches** associé hello **tranches** et voir les ordinateurs virtuels chaque tranche s’exécutait sur.</span><span class="sxs-lookup"><span data-stu-id="d50ae-464">Use Azure portal tooview hello **tasks** associated with hello **slices** and see what VM each slice ran on.</span></span> <span data-ttu-id="d50ae-465">Consultez la section [Intégration de Data Factory et Batch](#data-factory-and-batch-integration) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="d50ae-465">See [Data Factory and Batch integration](#data-factory-and-batch-integration) section for details.</span></span>
7. <span data-ttu-id="d50ae-466">Vous devez voir les fichiers de sortie hello Bonjour `outputfolder` de `mycontainer` dans votre Azure stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="d50ae-466">You should see hello output files in hello `outputfolder` of `mycontainer` in your Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   <span data-ttu-id="d50ae-467">Vous devriez voir cinq fichiers de sortie, un par tranche d’entrée.</span><span class="sxs-lookup"><span data-stu-id="d50ae-467">You should see five output files, one for each input slice.</span></span> <span data-ttu-id="d50ae-468">Chaque Hello sortie de fichier doit avoir le contenu toohello similaire suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="d50ae-468">Each of hello output file should have content similar toohello following output:</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   <span data-ttu-id="d50ae-469">Hello diagramme suivant illustre comment les tranches de Data Factory hello mappent tootasks dans Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="d50ae-469">hello following diagram illustrates how hello Data Factory slices map tootasks in Azure Batch.</span></span> <span data-ttu-id="d50ae-470">Dans cet exemple, une tranche n’est exécutée qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="d50ae-470">In this example, a slice has only one run.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. <span data-ttu-id="d50ae-471">À présent, essayons avec plusieurs fichiers dans un dossier.</span><span class="sxs-lookup"><span data-stu-id="d50ae-471">Now, let’s try with multiple files in a folder.</span></span> <span data-ttu-id="d50ae-472">Créer des fichiers : **file2.txt**, **file3.txt**, **file4.txt**, et **file5.txt** avec hello même contenu que dans fichier.txt dans le dossier de hello : **2015-11-06-01**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-472">Create files: **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with hello same content as in file.txt in hello folder: **2015-11-06-01**.</span></span>
9. <span data-ttu-id="d50ae-473">Dans le dossier de sortie hello **supprimer** fichier de sortie hello : **2015-11-16-01.txt**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-473">In hello output folder, **delete** hello output file: **2015-11-16-01.txt**.</span></span>
10. <span data-ttu-id="d50ae-474">Maintenant, dans hello **OutputDataset** panneau, la tranche de hello avec le bouton avec **l’heure de début de la tranche** défini trop**16/11/2015 01:00:00 AM**, puis cliquez sur **exécuter**tranche de hello toorerun/ré-process.</span><span class="sxs-lookup"><span data-stu-id="d50ae-474">Now, in hello **OutputDataset** blade, right-click hello slice with **SLICE START TIME** set too**11/16/2015 01:00:00 AM**, and click **Run** toorerun/re-process hello slice.</span></span> <span data-ttu-id="d50ae-475">À présent, la tranche de hello contient cinq fichiers au lieu d’un seul fichier.</span><span class="sxs-lookup"><span data-stu-id="d50ae-475">Now, hello slice has five files instead of one file.</span></span>

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. <span data-ttu-id="d50ae-476">Une fois que la tranche de hello s’exécute et son état est **prêt**, vérifiez le contenu dans le fichier de sortie hello pour cette tranche hello (**2015-11-16-01.txt**) Bonjour `outputfolder` de `mycontainer` dans votre stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="d50ae-476">After hello slice runs and its status is **Ready**, verify hello content in hello output file for this slice (**2015-11-16-01.txt**) in hello `outputfolder` of `mycontainer` in your blob storage.</span></span> <span data-ttu-id="d50ae-477">Il doit être une ligne pour chaque fichier de tranche de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-477">There should be a line for each file of hello slice.</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> <span data-ttu-id="d50ae-478">Si vous n’avez pas supprimé 2015 dans le fichier de sortie hello-11-16-01.txt avant d’essayer de cinq fichiers d’entrée, vous voyez une seule ligne à partir de la tranche de hello précédente exécution et les cinq lignes à partir de la tranche hello exécuter.</span><span class="sxs-lookup"><span data-stu-id="d50ae-478">If you did not delete hello output file 2015-11-16-01.txt before trying with five input files, you see one line from hello previous slice run and five lines from hello current slice run.</span></span> <span data-ttu-id="d50ae-479">Par défaut, le contenu de hello est ajouté toooutput fichier s’il existe déjà.</span><span class="sxs-lookup"><span data-stu-id="d50ae-479">By default, hello content is appended toooutput file if it already exists.</span></span>
>
>

#### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="d50ae-480">Intégration de Data Factory et Batch</span><span class="sxs-lookup"><span data-stu-id="d50ae-480">Data Factory and Batch integration</span></span>
<span data-ttu-id="d50ae-481">Hello service Data Factory crée un travail en traitement par lots Azure avec le nom de hello : `adf-poolname:job-xxx`.</span><span class="sxs-lookup"><span data-stu-id="d50ae-481">hello Data Factory service creates a job in Azure Batch with hello name: `adf-poolname:job-xxx`.</span></span>

![Azure Data Factory - Travaux Batch](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

<span data-ttu-id="d50ae-483">Une tâche dans la tâche de hello est créée pour chaque exécution de l’activité d’un secteur.</span><span class="sxs-lookup"><span data-stu-id="d50ae-483">A task in hello job is created for each activity run of a slice.</span></span> <span data-ttu-id="d50ae-484">S’il y a 10 toobe prêt tranches traitées, 10 tâches sont créés dans la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-484">If there are 10 slices ready toobe processed, 10 tasks are created in hello job.</span></span> <span data-ttu-id="d50ae-485">Vous pouvez avoir plusieurs tranches en cours d’exécution en parallèle si vous avez plusieurs nœuds de calcul dans le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-485">You can have more than one slice running in parallel if you have multiple compute nodes in hello pool.</span></span> <span data-ttu-id="d50ae-486">Si le nombre maximum de tâches hello par calcul nœud est défini trop > 1, il peut y avoir plusieurs une découper en cours d’exécution sur hello même calcul.</span><span class="sxs-lookup"><span data-stu-id="d50ae-486">If hello maximum tasks per compute node is set too> 1, there can be more than one slice running on hello same compute.</span></span>

<span data-ttu-id="d50ae-487">Dans cet exemple, il y a cinq tranches, donc cinq tâches dans Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="d50ae-487">In this example, there are five slices, so five tasks in Azure Batch.</span></span> <span data-ttu-id="d50ae-488">Avec hello **concurrency** défini trop**5** Bonjour pipeline JSON dans Azure Data Factory et **Maximum de tâches par ordinateur virtuel** défini trop**2** dans Azure Batch pool **2** machines virtuelles, hello l’exécution des tâches rapide (Vérifiez les heures de début et de fin pour les tâches).</span><span class="sxs-lookup"><span data-stu-id="d50ae-488">With hello **concurrency** set too**5** in hello pipeline JSON in Azure Data Factory and **Maximum tasks per VM** set too**2** in Azure Batch pool with **2** VMs, hello tasks runs fast (check start and end times for tasks).</span></span>

<span data-ttu-id="d50ae-489">Utilisez hello tooview portail hello par lots et ses tâches associées hello **tranches** et voir les ordinateurs virtuels chaque tranche s’exécutait sur.</span><span class="sxs-lookup"><span data-stu-id="d50ae-489">Use hello portal tooview hello Batch job and its tasks that are associated with hello **slices** and see what VM each slice ran on.</span></span>

![Azure Data Factory - Tâches de travaux Batch](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a><span data-ttu-id="d50ae-491">Déboguer hello pipeline</span><span class="sxs-lookup"><span data-stu-id="d50ae-491">Debug hello pipeline</span></span>
<span data-ttu-id="d50ae-492">Le débogage consiste à utiliser quelques techniques de base :</span><span class="sxs-lookup"><span data-stu-id="d50ae-492">Debugging consists of a few basic techniques:</span></span>

1. <span data-ttu-id="d50ae-493">Si la tranche de hello d’entrée n’est pas défini trop**prêt**, vérifiez que la structure de dossiers d’entrée de hello est correct et fichier.txt existe dans les dossiers d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-493">If hello input slice is not set too**Ready**, confirm that hello input folder structure is correct and file.txt exists in hello input folders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. <span data-ttu-id="d50ae-494">Bonjour **Execute** méthode de votre activité personnalisée, utilisez hello **IActivityLogger** informations toolog objet qui vous permet de résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="d50ae-494">In hello **Execute** method of your custom activity, use hello **IActivityLogger** object toolog information that helps you troubleshoot issues.</span></span> <span data-ttu-id="d50ae-495">messages Hello connecté apparaissent dans les utilisateur hello\_fichier journal de 0.</span><span class="sxs-lookup"><span data-stu-id="d50ae-495">hello logged messages show up in hello user\_0.log file.</span></span>

   <span data-ttu-id="d50ae-496">Bonjour **OutputDataset** panneau, cliquez sur Bonjour tranche toosee Bonjour **tranche de données** panneau pour ce secteur.</span><span class="sxs-lookup"><span data-stu-id="d50ae-496">In hello **OutputDataset** blade, click hello slice toosee hello **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="d50ae-497">Les **activités exécutées** pour cette tranche s’affichent.</span><span class="sxs-lookup"><span data-stu-id="d50ae-497">You see **activity runs** for that slice.</span></span> <span data-ttu-id="d50ae-498">Vous devez voir une activité à exécuter pour la tranche de hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-498">You should see one activity run for hello slice.</span></span> <span data-ttu-id="d50ae-499">Si vous cliquez sur **exécuter** dans la barre de commandes hello, vous pouvez démarrer une autre activité exécutée pour hello même secteur.</span><span class="sxs-lookup"><span data-stu-id="d50ae-499">If you click **Run** in hello command bar, you can start another activity run for hello same slice.</span></span>

   <span data-ttu-id="d50ae-500">Lorsque vous cliquez sur exécution de l’activité hello, vous voyez hello **détails de l’activité exécuter** panneau avec une liste des fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="d50ae-500">When you click hello activity run, you see hello **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="d50ae-501">Vous consultez les messages enregistrés dans hello **utilisateur\_0 journal** fichier.</span><span class="sxs-lookup"><span data-stu-id="d50ae-501">You see logged messages in hello **user\_0.log** file.</span></span> <span data-ttu-id="d50ae-502">Lorsqu’une erreur se produit, vous voyez trois exécutions d’activité, car de nouvelles tentatives hello est définie too3 dans pipeline/activité hello JSON.</span><span class="sxs-lookup"><span data-stu-id="d50ae-502">When an error occurs, you see three activity runs because hello retry count is set too3 in hello pipeline/activity JSON.</span></span> <span data-ttu-id="d50ae-503">Lorsque vous cliquez sur exécution de l’activité hello, vous voyez que vous pouvez consulter les erreurs de hello tootroubleshoot des fichiers journaux hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-503">When you click hello activity run, you see hello log files that you can review tootroubleshoot hello error.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   <span data-ttu-id="d50ae-504">Dans la liste hello des fichiers journaux, cliquez sur hello **0.log de l’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-504">In hello list of log files, click hello **user-0.log**.</span></span> <span data-ttu-id="d50ae-505">Dans le panneau droit hello sont des résultats de l’utilisation de hello hello **IActivityLogger.Write** (méthode).</span><span class="sxs-lookup"><span data-stu-id="d50ae-505">In hello right panel are hello results of using hello **IActivityLogger.Write** method.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   <span data-ttu-id="d50ae-506">Consultez le fichier system-0.log pour vérifier les exceptions et messages d’erreur système éventuels.</span><span class="sxs-lookup"><span data-stu-id="d50ae-506">Check system-0.log for any system error messages and exceptions.</span></span>

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. <span data-ttu-id="d50ae-507">Inclure hello **PDB** fichiers dans le fichier zip de hello afin que les détails de l’erreur hello ont des informations telles que **pile des appels** lorsqu’une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="d50ae-507">Include hello **PDB** file in hello zip file so that hello error details have information such as **call stack** when an error occurs.</span></span>
4. <span data-ttu-id="d50ae-508">Tous les hello des fichiers dans le fichier zip de hello pour l’activité personnalisée hello doit se trouver au hello **niveau supérieur** avec aucun des sous-dossiers.</span><span class="sxs-lookup"><span data-stu-id="d50ae-508">All hello files in hello zip file for hello custom activity must be at hello **top level** with no subfolders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. <span data-ttu-id="d50ae-509">Vérifiez que hello **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer / MyDotNetActivity.zip), et **packageLinkedService** (doit point toohello Azure stockage d’objets blob qui contient le fichier zip de hello) sont définies les valeurs toocorrect.</span><span class="sxs-lookup"><span data-stu-id="d50ae-509">Ensure that hello **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point toohello Azure blob storage that contains hello zip file) are set toocorrect values.</span></span>
6. <span data-ttu-id="d50ae-510">Si vous avez corrigé une tranche hello tooreprocess erreur et que vous souhaitez, cliquez sur tranche hello Bonjour **OutputDataset** panneau, cliquez sur **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-510">If you fixed an error and want tooreprocess hello slice, right-click hello slice in hello **OutputDataset** blade and click **Run**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > <span data-ttu-id="d50ae-511">Vous voyez un **conteneur** dans votre Stockage Blob Azure nommé `adfjobs`.</span><span class="sxs-lookup"><span data-stu-id="d50ae-511">You see a **container** in your Azure Blob storage named: `adfjobs`.</span></span> <span data-ttu-id="d50ae-512">Ce conteneur n’est pas supprimé automatiquement, mais vous pouvez le supprimer en toute sécurité après avoir effectué la solution hello test.</span><span class="sxs-lookup"><span data-stu-id="d50ae-512">This container is not automatically deleted, but you can safely delete it after you are done testing hello solution.</span></span> <span data-ttu-id="d50ae-513">De même, hello solution de fabrique de données crée un lot d’Azure **travail** nommé : `adf-\<pool ID/name\>:job-0000000001`.</span><span class="sxs-lookup"><span data-stu-id="d50ae-513">Similarly, hello Data Factory solution creates an Azure Batch **job** named: `adf-\<pool ID/name\>:job-0000000001`.</span></span> <span data-ttu-id="d50ae-514">Vous pouvez supprimer cette tâche après avoir testé les solutions hello si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="d50ae-514">You can delete this job after you test hello solution if you like.</span></span>
   >
   >
7. <span data-ttu-id="d50ae-515">activité personnalisée Hello n’utilise pas hello **app.config** fichier à partir de votre package.</span><span class="sxs-lookup"><span data-stu-id="d50ae-515">hello custom activity does not use hello **app.config** file from your package.</span></span> <span data-ttu-id="d50ae-516">Par conséquent, si votre code lit les chaînes de connexion à partir du fichier de configuration hello, il ne fonctionne pas lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="d50ae-516">Therefore, if your code reads any connection strings from hello configuration file, it does not work at runtime.</span></span> <span data-ttu-id="d50ae-517">Hello meilleures pratiques lors de l’utilisation d’Azure Batch est toohold les clés secrètes dans un **Azure KeyVault**, utilisez un keyvault de hello basée sur certificat de service principal tooprotect et distribuer le pool de traitement par lots hello certificat tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d50ae-517">hello best practice when using Azure Batch is toohold any secrets in an **Azure KeyVault**, use a certificate-based service principal tooprotect hello keyvault, and distribute hello certificate tooAzure Batch pool.</span></span> <span data-ttu-id="d50ae-518">Hello les activités personnalisées .NET puis peuvent accéder aux clés secrètes hello KeyVault lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="d50ae-518">hello .NET custom activity then can access secrets from hello KeyVault at runtime.</span></span> <span data-ttu-id="d50ae-519">Cette solution est générique et peut évoluer type tooany du secret, pas seulement les chaînes de connexion.</span><span class="sxs-lookup"><span data-stu-id="d50ae-519">This solution is a generic one and can scale tooany type of secret, not just connection string.</span></span>

    <span data-ttu-id="d50ae-520">Il existe une solution plus facile (mais pas une meilleure pratique) : vous pouvez créer un **service lié Azure SQL** avec les paramètres de chaîne de connexion, créez un dataset qu’utilise hello service lié et le jeu de données chaîne hello comme un jeu de données d’entrée factice activité de .NET personnalisée toohello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-520">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses hello linked service, and chain hello dataset as a dummy input dataset toohello custom .NET activity.</span></span> <span data-ttu-id="d50ae-521">Vous pouvez ensuite hello d’accès liées la chaîne de connexion du service dans le code d’activité personnalisée hello et il doit fonctionner correctement lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="d50ae-521">You can then access hello linked service's connection string in hello custom activity code and it should work fine at runtime.</span></span>  

#### <a name="extend-hello-sample"></a><span data-ttu-id="d50ae-522">Étendre l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="d50ae-522">Extend hello sample</span></span>
<span data-ttu-id="d50ae-523">Vous pouvez étendre cet exemple toolearn plus d’informations sur les fonctionnalités d’Azure Data Factory et Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="d50ae-523">You can extend this sample toolearn more about Azure Data Factory and Azure Batch features.</span></span> <span data-ttu-id="d50ae-524">Par exemple, les tranches tooprocess dans une plage de temps différente, hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d50ae-524">For example, tooprocess slices in a different time range, do hello following steps:</span></span>

1. <span data-ttu-id="d50ae-525">Ajouter hello suivant sous-dossiers Bonjour `inputfolder`: 2015-11-16-05, 2015-11-16-06 201-11-16-07, 2011-11-16-08, 2015-11-16-09 et place les fichiers d’entrée dans ces dossiers.</span><span class="sxs-lookup"><span data-stu-id="d50ae-525">Add hello following subfolders in hello `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 and place input files in those folders.</span></span> <span data-ttu-id="d50ae-526">Modifier l’heure de fin hello pour le pipeline hello à partir de `2015-11-16T05:00:00Z` trop`2015-11-16T10:00:00Z`.</span><span class="sxs-lookup"><span data-stu-id="d50ae-526">Change hello end time for hello pipeline from `2015-11-16T05:00:00Z` too`2015-11-16T10:00:00Z`.</span></span> <span data-ttu-id="d50ae-527">Bonjour **vue de diagramme**, double-cliquez sur hello **InputDataset**et vérifiez que les tranches d’entrée hello sont prêtes.</span><span class="sxs-lookup"><span data-stu-id="d50ae-527">In hello **Diagram View**, double-click hello **InputDataset**, and confirm that hello input slices are ready.</span></span> <span data-ttu-id="d50ae-528">Double-cliquez sur **OuptutDataset** état de hello toosee de tranches de sortie.</span><span class="sxs-lookup"><span data-stu-id="d50ae-528">Double-click **OuptutDataset** toosee hello state of output slices.</span></span> <span data-ttu-id="d50ae-529">S’ils sont dans l’état prêt, vérifiez le dossier de sortie hello pour les fichiers de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-529">If they are in Ready state, check hello output folder for hello output files.</span></span>
2. <span data-ttu-id="d50ae-530">Augmenter ou diminuer hello **concurrency** paramètre toounderstand comment il affecte les performances de hello de votre solution, en particulier hello du traitement qui se produit sur Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="d50ae-530">Increase or decrease hello **concurrency** setting toounderstand how it affects hello performance of your solution, especially hello processing that occurs on Azure Batch.</span></span> <span data-ttu-id="d50ae-531">(Consultez l’étape 4 : créer et exécuter le pipeline de hello pour plus d’informations sur hello **concurrency** paramètre.)</span><span class="sxs-lookup"><span data-stu-id="d50ae-531">(See Step 4: Create and run hello pipeline for more on hello **concurrency** setting.)</span></span>
3. <span data-ttu-id="d50ae-532">Créez un pool avec une valeur **Maximum tasks per VM**(Nombre maximal de tâches par machine virtuelle) supérieure/inférieure.</span><span class="sxs-lookup"><span data-stu-id="d50ae-532">Create a pool with higher/lower **Maximum tasks per VM**.</span></span> <span data-ttu-id="d50ae-533">toouse hello nouveau pool est créé, hello de mise à jour de service lié Azure Batch dans la solution de Data Factory hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-533">toouse hello new pool you created, update hello Azure Batch linked service in hello Data Factory solution.</span></span> <span data-ttu-id="d50ae-534">(Consultez l’étape 4 : créer et exécuter le pipeline de hello pour plus d’informations sur hello **Maximum de tâches par ordinateur virtuel** paramètre.)</span><span class="sxs-lookup"><span data-stu-id="d50ae-534">(See Step 4: Create and run hello pipeline for more on hello **Maximum tasks per VM** setting.)</span></span>
4. <span data-ttu-id="d50ae-535">Créez un pool Azure Batch avec la fonctionnalité **autoscale** .</span><span class="sxs-lookup"><span data-stu-id="d50ae-535">Create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="d50ae-536">Automatiquement mise à l’échelle des nœuds de calcul dans un pool Azure Batch est ajustement dynamique de hello de puissance utilisée par votre application de traitement.</span><span class="sxs-lookup"><span data-stu-id="d50ae-536">Automatically scaling compute nodes in an Azure Batch pool is hello dynamic adjustment of processing power used by your application.</span></span> 

    <span data-ttu-id="d50ae-537">Hello exemple de formule ici atteint hello suivant comportement : lorsque hello pool est initialement créé, il commence par 1 machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d50ae-537">hello sample formula here achieves hello following behavior: When hello pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="d50ae-538">$PendingTasks mesure définit le nombre hello de tâches en cours d’exécution + active (en file d’attente) état.</span><span class="sxs-lookup"><span data-stu-id="d50ae-538">$PendingTasks metric defines hello number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="d50ae-539">formule de Hello recherche hello moyenne d’attente de tâches Bonjour 180 dernières secondes et définit les élément TargetDedicated en conséquence.</span><span class="sxs-lookup"><span data-stu-id="d50ae-539">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="d50ae-540">Elle garantit que TargetDedicated ne va jamais au-delà de 25 machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="d50ae-540">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="d50ae-541">Par conséquent, comme les nouvelles tâches sont envoyés, pool croît automatiquement en tant que tâches se terminent, machines virtuelles deviennent libre un par un et hello échelle réduit ces machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="d50ae-541">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and hello autoscaling shrinks those VMs.</span></span> <span data-ttu-id="d50ae-542">startingNumberOfVMs et maxNumberofVMs peut être ajustée tooyour besoins.</span><span class="sxs-lookup"><span data-stu-id="d50ae-542">startingNumberOfVMs and maxNumberofVMs can be adjusted tooyour needs.</span></span>
 
    <span data-ttu-id="d50ae-543">Formule de mise à l’échelle automatique :</span><span class="sxs-lookup"><span data-stu-id="d50ae-543">Autoscale formula:</span></span>

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   <span data-ttu-id="d50ae-544">Pour plus d’informations, consultez [Mettre automatiquement à l’échelle les nœuds de calcul dans un pool Azure Batch](../batch/batch-automatic-scaling.md) .</span><span class="sxs-lookup"><span data-stu-id="d50ae-544">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

   <span data-ttu-id="d50ae-545">Si le pool de hello utilise par défaut de hello [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello service Batch peut prendre 15 à 30 minutes tooprepare hello machine virtuelle avant d’exécuter l’activité personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="d50ae-545">If hello pool is using hello default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch service could take 15-30 minutes tooprepare hello VM before running hello custom activity.</span></span>  <span data-ttu-id="d50ae-546">Si le pool de hello utilise un autre autoScaleEvaluationInterval, hello service Batch peut prendre autoScaleEvaluationInterval + 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="d50ae-546">If hello pool is using a different autoScaleEvaluationInterval, hello Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>
5. <span data-ttu-id="d50ae-547">Dans la solution de l’exemple hello hello **Execute** méthode appelle hello **Calculate** méthode qui traite une tooproduce de tranche de données d’entrée une tranche de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="d50ae-547">In hello sample solution, hello **Execute** method invokes hello **Calculate** method that processes an input data slice tooproduce an output data slice.</span></span> <span data-ttu-id="d50ae-548">Vous pouvez écrire votre propre méthode tooprocess les données d’entrée et remplacez l’appel de méthode Calculate hello dans la méthode d’exécution hello avec une méthode d’appel tooyour.</span><span class="sxs-lookup"><span data-stu-id="d50ae-548">You can write your own method tooprocess input data and replace hello Calculate method call in hello Execute method with a call tooyour method.</span></span>

### <a name="next-steps-consume-hello-data"></a><span data-ttu-id="d50ae-549">Étapes suivantes : consommer des données de hello</span><span class="sxs-lookup"><span data-stu-id="d50ae-549">Next steps: Consume hello data</span></span>
<span data-ttu-id="d50ae-550">Après avoir traité des données, vous pouvez les employer avec des outils en ligne tels que **Microsoft Power BI**.</span><span class="sxs-lookup"><span data-stu-id="d50ae-550">After you process data, you can consume it with online tools like **Microsoft Power BI**.</span></span> <span data-ttu-id="d50ae-551">Voici toohelp liens comprendre de Power BI et comment toouse dans Azure :</span><span class="sxs-lookup"><span data-stu-id="d50ae-551">Here are links toohelp you understand Power BI and how toouse it in Azure:</span></span>

* [<span data-ttu-id="d50ae-552">Explorer un jeu de données dans Power BI</span><span class="sxs-lookup"><span data-stu-id="d50ae-552">Explore a dataset in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [<span data-ttu-id="d50ae-553">Prise en main de hello Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="d50ae-553">Getting started with hello Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [<span data-ttu-id="d50ae-554">Actualisation des données dans Power BI</span><span class="sxs-lookup"><span data-stu-id="d50ae-554">Refresh data in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [<span data-ttu-id="d50ae-555">Azure et Power BI</span><span class="sxs-lookup"><span data-stu-id="d50ae-555">Azure and Power BI - basic overview</span></span>](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a><span data-ttu-id="d50ae-556">Références</span><span class="sxs-lookup"><span data-stu-id="d50ae-556">References</span></span>
* [<span data-ttu-id="d50ae-557">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d50ae-557">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

  * [<span data-ttu-id="d50ae-558">Introduction tooAzure service Data Factory</span><span class="sxs-lookup"><span data-stu-id="d50ae-558">Introduction tooAzure Data Factory service</span></span>](data-factory-introduction.md)
  * [<span data-ttu-id="d50ae-559">Prise en main d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d50ae-559">Get started with Azure Data Factory</span></span>](data-factory-build-your-first-pipeline.md)
  * [<span data-ttu-id="d50ae-560">Utilisation des activités personnalisées dans un pipeline Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d50ae-560">Use custom activities in an Azure Data Factory pipeline</span></span>](data-factory-use-custom-activities.md)
* [<span data-ttu-id="d50ae-561">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="d50ae-561">Azure Batch</span></span>](https://azure.microsoft.com/documentation/services/batch/)

  * [<span data-ttu-id="d50ae-562">Notions de base d’Azure Batch</span><span class="sxs-lookup"><span data-stu-id="d50ae-562">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
  * [<span data-ttu-id="d50ae-563">Vue d’ensemble des fonctionnalités d’Azure Batch</span><span class="sxs-lookup"><span data-stu-id="d50ae-563">Overview of Azure Batch features</span></span>](../batch/batch-api-basics.md)
  * [<span data-ttu-id="d50ae-564">Créer et gérer le compte Azure Batch Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="d50ae-564">Create and manage Azure Batch account in hello Azure portal</span></span>](../batch/batch-account-create-portal.md)
  * [<span data-ttu-id="d50ae-565">Get started with the .NET Azure Batch Library .NET</span><span class="sxs-lookup"><span data-stu-id="d50ae-565">Get started with Azure Batch Library .NET</span></span>](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
