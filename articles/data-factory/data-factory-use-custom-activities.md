---
title: "aaaUse des activités personnalisées dans un pipeline Azure Data Factory"
description: "Découvrez comment toocreate des activités personnalisées et les utiliser dans un pipeline Azure Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 23e33727b2160541ab40938ffd911fdd484b3daa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a><span data-ttu-id="aef3d-103">Utilisation des activités personnalisées dans un pipeline Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="aef3d-103">Use custom activities in an Azure Data Factory pipeline</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="aef3d-104">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="aef3d-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="aef3d-105">Activité pig</span><span class="sxs-lookup"><span data-stu-id="aef3d-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="aef3d-106">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="aef3d-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="aef3d-107">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="aef3d-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="aef3d-108">Activité Spark</span><span class="sxs-lookup"><span data-stu-id="aef3d-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="aef3d-109">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="aef3d-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="aef3d-110">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="aef3d-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="aef3d-111">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="aef3d-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="aef3d-112">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="aef3d-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="aef3d-113">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="aef3d-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="aef3d-114">Vous pouvez utiliser deux types d’activités dans un pipeline Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="aef3d-114">There are two types of activities that you can use in an Azure Data Factory pipeline.</span></span>

- <span data-ttu-id="aef3d-115">[Activités de déplacement des données](data-factory-data-movement-activities.md) toomove des données entre [prise en charge des magasins de données source et récepteur](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="aef3d-115">[Data Movement Activities](data-factory-data-movement-activities.md) toomove data between [supported source and sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>
- <span data-ttu-id="aef3d-116">[Activités de Transformation des données](data-factory-data-transformation-activities.md) tootransform les données à l’aide des services tels que Azure HDInsight, Azure Batch et Azure Machine Learning de calcul.</span><span class="sxs-lookup"><span data-stu-id="aef3d-116">[Data Transformation Activities](data-factory-data-transformation-activities.md) tootransform data using compute services such as Azure HDInsight, Azure Batch, and Azure Machine Learning.</span></span> 

<span data-ttu-id="aef3d-117">les données toomove vers/depuis un magasin de données qui fabrique de données ne prend pas en charge, créez un **activité personnalisée** avec vos propres données mouvement logique et l’utilisation hello activité dans un pipeline.</span><span class="sxs-lookup"><span data-stu-id="aef3d-117">toomove data to/from a data store that Data Factory does not support, create a **custom activity** with your own data movement logic and use hello activity in a pipeline.</span></span> <span data-ttu-id="aef3d-118">De même, tootransform/traitement des données d’une manière qui n’est pas pris en charge par la fabrique de données, créer une activité personnalisée avec votre propre logique de transformation de données et utiliser l’activité hello dans un pipeline.</span><span class="sxs-lookup"><span data-stu-id="aef3d-118">Similarly, tootransform/process data in a way that isn't supported by Data Factory, create a custom activity with your own data transformation logic and use hello activity in a pipeline.</span></span> 

<span data-ttu-id="aef3d-119">Vous pouvez configurer un toorun d’activité personnalisée sur une **Azure Batch** pool d’ordinateurs virtuels ou basé sur un Windows **Azure HDInsight** cluster.</span><span class="sxs-lookup"><span data-stu-id="aef3d-119">You can configure a custom activity toorun on an **Azure Batch** pool of virtual machines or a Windows-based **Azure HDInsight** cluster.</span></span> <span data-ttu-id="aef3d-120">Lorsque vous utilisez Azure Batch, vous pouvez utiliser uniquement un pool Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="aef3d-120">When using Azure Batch, you can use only an existing Azure Batch pool.</span></span> <span data-ttu-id="aef3d-121">À l’inverse, lorsque vous utilisez HDInsight, vous pouvez utiliser un cluster HDInsight existant ou un cluster qui est créé automatiquement pour vous à la demande lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="aef3d-121">Whereas, when using HDInsight, you can use an existing HDInsight cluster or a cluster that is automatically created for you on-demand at runtime.</span></span>  

<span data-ttu-id="aef3d-122">Hello suivant de procédure pas à pas fournit des instructions détaillées pour la création d’une activité .NET personnalisée et à l’aide d’activité personnalisée hello dans un pipeline.</span><span class="sxs-lookup"><span data-stu-id="aef3d-122">hello following walkthrough provides step-by-step instructions for creating a custom .NET activity and using hello custom activity in a pipeline.</span></span> <span data-ttu-id="aef3d-123">procédure pas à pas Hello utilise un **Azure Batch** service lié.</span><span class="sxs-lookup"><span data-stu-id="aef3d-123">hello walkthrough uses an **Azure Batch** linked service.</span></span> <span data-ttu-id="aef3d-124">toouse un HDInsight Azure lié à service au lieu de cela, vous créez un service lié de type **HDInsight** (votre propre cluster HDInsight) ou **HDInsightOnDemand** (fabrique de données crée un cluster HDInsight à la demande).</span><span class="sxs-lookup"><span data-stu-id="aef3d-124">toouse an Azure HDInsight linked service instead, you create a linked service of type **HDInsight** (your own HDInsight cluster) or **HDInsightOnDemand** (Data Factory creates an HDInsight cluster on-demand).</span></span> <span data-ttu-id="aef3d-125">Ensuite, configurez hello de toouse d’activité personnalisée service lié HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aef3d-125">Then, configure custom activity toouse hello HDInsight linked service.</span></span> <span data-ttu-id="aef3d-126">Consultez [utilisez Azure HDInsight les services liés](#use-hdinsight-compute-service) pour plus d’informations sur l’utilisation d’activités personnalisées de Azure HDInsight toorun hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-126">See [Use Azure HDInsight linked services](#use-hdinsight-compute-service) section for details on using Azure HDInsight toorun hello custom activity.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="aef3d-127">activités de .NET personnalisées Hello s’exécutent uniquement sur des clusters HDInsight de basés sur Windows.</span><span class="sxs-lookup"><span data-stu-id="aef3d-127">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="aef3d-128">Une solution de contournement pour cette limitation est toouse hello carte réduire toorun personnalisé Java code d’activité sur un cluster HDInsight de basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="aef3d-128">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="aef3d-129">Une autre option consiste à toouse un pool de traitement par lots Azure d’activités personnalisées de machines virtuelles toorun au lieu d’utiliser un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aef3d-129">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>
> - <span data-ttu-id="aef3d-130">Il n’est pas possible de toouse une passerelle de gestion des données à partir de sources de données sur site tooaccess activité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="aef3d-130">It is not possible toouse a Data Management Gateway from a custom activity tooaccess on-premises data sources.</span></span> <span data-ttu-id="aef3d-131">Actuellement, [passerelle de gestion des données](data-factory-data-management-gateway.md) prend en charge uniquement l’activité de copie hello et l’activité de procédure stockée dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="aef3d-131">Currently, [Data Management Gateway](data-factory-data-management-gateway.md) supports only hello copy activity and stored procedure activity in Data Factory.</span></span>   

## <a name="walkthrough-create-a-custom-activity"></a><span data-ttu-id="aef3d-132">Procédure pas à pas : création d’une activité personnalisée</span><span class="sxs-lookup"><span data-stu-id="aef3d-132">Walkthrough: create a custom activity</span></span>
### <a name="prerequisites"></a><span data-ttu-id="aef3d-133">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="aef3d-133">Prerequisites</span></span>
* <span data-ttu-id="aef3d-134">Visual Studio 2012/2013/2015</span><span class="sxs-lookup"><span data-stu-id="aef3d-134">Visual Studio 2012/2013/2015</span></span>
* <span data-ttu-id="aef3d-135">Téléchargez et installez le [Kit de développement logiciel (SDK) Azure .NET](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="aef3d-135">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span></span>

### <a name="azure-batch-prerequisites"></a><span data-ttu-id="aef3d-136">Configuration requise pour Azure Batch</span><span class="sxs-lookup"><span data-stu-id="aef3d-136">Azure Batch prerequisites</span></span>
<span data-ttu-id="aef3d-137">Hello procédure pas à pas, vous exécutez vos activités .NET personnalisées à l’aide du traitement par lots Azure en tant qu’une ressource de calcul.</span><span class="sxs-lookup"><span data-stu-id="aef3d-137">In hello walkthrough, you run your custom .NET activities using Azure Batch as a compute resource.</span></span> <span data-ttu-id="aef3d-138">**Traitement par lots Azure** est une plateforme de service pour l’exécution parallèle à grande échelle et hautes performances (HPC) des applications efficacement dans le cloud de hello informatiques.</span><span class="sxs-lookup"><span data-stu-id="aef3d-138">**Azure Batch** is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="aef3d-139">Traitement par lots Azure planifie toorun de travail de calcul intensif sur managé **collection de machines virtuelles**, et peut automatiquement montée en puissance de calcul ressources toomeet hello aux besoins de vos tâches.</span><span class="sxs-lookup"><span data-stu-id="aef3d-139">Azure Batch schedules compute-intensive work toorun on a managed **collection of virtual machines**, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span> <span data-ttu-id="aef3d-140">Consultez [principes de base Azure Batch] [ batch-technical-overview] l’article pour une présentation détaillée de hello service Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="aef3d-140">See [Azure Batch basics][batch-technical-overview] article for a detailed overview of hello Azure Batch service.</span></span>

<span data-ttu-id="aef3d-141">Didacticiel de hello, créez un compte Azure Batch avec un pool d’ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="aef3d-141">For hello tutorial, create an Azure Batch account with a pool of VMs.</span></span> <span data-ttu-id="aef3d-142">Voici les étapes hello :</span><span class="sxs-lookup"><span data-stu-id="aef3d-142">Here are hello steps:</span></span>

1. <span data-ttu-id="aef3d-143">Créer un **compte Azure Batch** à l’aide de hello [portail Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aef3d-143">Create an **Azure Batch account** using hello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="aef3d-144">Consultez l’article [Créer et gérer un compte Azure Batch][batch-create-account] pour obtenir des instructions.</span><span class="sxs-lookup"><span data-stu-id="aef3d-144">See [Create and manage an Azure Batch account][batch-create-account] article for instructions.</span></span>
2. <span data-ttu-id="aef3d-145">Notez le nom du compte Azure Batch hello, clé de compte, URI et nom du pool.</span><span class="sxs-lookup"><span data-stu-id="aef3d-145">Note down hello Azure Batch account name, account key, URI, and pool name.</span></span> <span data-ttu-id="aef3d-146">Vous avez besoin toocreate un service lié Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="aef3d-146">You need them toocreate an Azure Batch linked service.</span></span>
    1. <span data-ttu-id="aef3d-147">Sur la page d’accueil hello pour le compte Azure Batch, vous voyez un **URL** Bonjour suivant le format : `https://myaccount.westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="aef3d-147">On hello home page for Azure Batch account, you see a **URL** in hello following format: `https://myaccount.westus.batch.azure.com`.</span></span> <span data-ttu-id="aef3d-148">Dans cet exemple, **myaccount** hello désigne hello compte Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="aef3d-148">In this example, **myaccount** is hello name of hello Azure Batch account.</span></span> <span data-ttu-id="aef3d-149">URI que vous utilisez dans la définition de service hello lié est URL hello sans nom hello du compte de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-149">URI you use in hello linked service definition is hello URL without hello name of hello account.</span></span> <span data-ttu-id="aef3d-150">Par exemple : `https://<region>.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="aef3d-150">For example: `https://<region>.batch.azure.com`.</span></span>
    2. <span data-ttu-id="aef3d-151">Cliquez sur **clés** sur le menu de gauche hello et hello de copie **clé d’accès primaire**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-151">Click **Keys** on hello left menu, and copy hello **PRIMARY ACCESS KEY**.</span></span>
    3. <span data-ttu-id="aef3d-152">toouse un pool existant, cliquez sur **Pools** sur le menu de hello et notez les hello **ID** du pool de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-152">toouse an existing pool, click **Pools** on hello menu, and note down hello **ID** of hello pool.</span></span> <span data-ttu-id="aef3d-153">Si vous n’avez pas un pool existant, déplacer l’étape suivante de toohello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-153">If you don't have an existing pool, move toohello next step.</span></span>     
2. <span data-ttu-id="aef3d-154">Créez un **pool Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-154">Create an **Azure Batch pool**.</span></span>

   1. <span data-ttu-id="aef3d-155">Bonjour [portail Azure](https://portal.azure.com), cliquez sur **Parcourir** dans hello du menu de gauche, puis cliquez sur **comptes Batch**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-155">In hello [Azure portal](https://portal.azure.com), click **Browse** in hello left menu, and click **Batch Accounts**.</span></span>
   2. <span data-ttu-id="aef3d-156">Sélectionnez votre hello tooopen du compte Azure Batch **compte Batch** panneau.</span><span class="sxs-lookup"><span data-stu-id="aef3d-156">Select your Azure Batch account tooopen hello **Batch Account** blade.</span></span>
   3. <span data-ttu-id="aef3d-157">Cliquez sur la vignette **Pools** .</span><span class="sxs-lookup"><span data-stu-id="aef3d-157">Click **Pools** tile.</span></span>
   4. <span data-ttu-id="aef3d-158">Bonjour **Pools** panneau, cliquez sur le bouton Ajouter dans la barre d’outils de hello tooadd un pool.</span><span class="sxs-lookup"><span data-stu-id="aef3d-158">In hello **Pools** blade, click Add button on hello toolbar tooadd a pool.</span></span>
      1. <span data-ttu-id="aef3d-159">Entrez un ID de pool de hello (ID du Pool).</span><span class="sxs-lookup"><span data-stu-id="aef3d-159">Enter an ID for hello pool (Pool ID).</span></span> <span data-ttu-id="aef3d-160">Hello de note **ID de pool de hello**; vous en avez besoin lors de la création de solutions de Data Factory hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-160">Note hello **ID of hello pool**; you need it when creating hello Data Factory solution.</span></span>
      2. <span data-ttu-id="aef3d-161">Spécifiez **Windows Server 2012 R2** pour le paramètre de famille du système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-161">Specify **Windows Server 2012 R2** for hello Operating System Family setting.</span></span>
      3. <span data-ttu-id="aef3d-162">Sélectionnez le **niveau tarifaire du nœud**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-162">Select a **node pricing tier**.</span></span>
      4. <span data-ttu-id="aef3d-163">Entrez **2** en tant que valeur pour hello **cible dédié** paramètre.</span><span class="sxs-lookup"><span data-stu-id="aef3d-163">Enter **2** as value for hello **Target Dedicated** setting.</span></span>
      5. <span data-ttu-id="aef3d-164">Entrez **2** en tant que valeur pour hello **nombre maximal de tâches par nœud** paramètre.</span><span class="sxs-lookup"><span data-stu-id="aef3d-164">Enter **2** as value for hello **Max tasks per node** setting.</span></span>
   5. <span data-ttu-id="aef3d-165">Cliquez sur **OK** pool de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="aef3d-165">Click **OK** toocreate hello pool.</span></span>
   6. <span data-ttu-id="aef3d-166">Notez les hello **ID** du pool de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-166">Note down hello **ID** of hello pool.</span></span> 



### <a name="high-level-steps"></a><span data-ttu-id="aef3d-167">Procédure générale</span><span class="sxs-lookup"><span data-stu-id="aef3d-167">High-level steps</span></span>
<span data-ttu-id="aef3d-168">Voici hello deux étapes que vous effectuez dans le cadre de cette procédure pas à pas :</span><span class="sxs-lookup"><span data-stu-id="aef3d-168">Here are hello two high-level steps you perform as part of this walkthrough:</span></span> 

1. <span data-ttu-id="aef3d-169">Créer une activité personnalisée qui contient une logique simple de transformation/traitement des données.</span><span class="sxs-lookup"><span data-stu-id="aef3d-169">Create a custom activity that contains simple data transformation/processing logic.</span></span>
2. <span data-ttu-id="aef3d-170">Créez une fabrique de données Azure avec un pipeline qui utilise l’activité personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-170">Create an Azure data factory with a pipeline that uses hello custom activity.</span></span>

### <a name="create-a-custom-activity"></a><span data-ttu-id="aef3d-171">création d'une activité personnalisée</span><span class="sxs-lookup"><span data-stu-id="aef3d-171">Create a custom activity</span></span>
<span data-ttu-id="aef3d-172">toocreate une activité personnalisée .NET, créez un **bibliothèque de classes .NET** projet avec une classe qui implémente cette **IDotNetActivity** interface.</span><span class="sxs-lookup"><span data-stu-id="aef3d-172">toocreate a .NET custom activity, create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="aef3d-173">Cette interface possède une seule méthode, [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) , avec la signature suivante :</span><span class="sxs-lookup"><span data-stu-id="aef3d-173">This interface has only one method: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) and its signature is:</span></span>

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


<span data-ttu-id="aef3d-174">méthode Hello accepte quatre paramètres :</span><span class="sxs-lookup"><span data-stu-id="aef3d-174">hello method takes four parameters:</span></span>

- <span data-ttu-id="aef3d-175">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-175">**linkedServices**.</span></span> <span data-ttu-id="aef3d-176">Cette propriété est une liste énumérable de services liés de magasin de données référencées par les jeux de données d’entrée/sortie pour l’activité de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-176">This property is an enumerable list of Data Store linked services referenced by input/output datasets for hello activity.</span></span>   
- <span data-ttu-id="aef3d-177">**jeux de données**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-177">**datasets**.</span></span> <span data-ttu-id="aef3d-178">Cette propriété est une liste énumérable de jeux de données d’entrée/sortie pour l’activité de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-178">This property is an enumerable list of input/output datasets for hello activity.</span></span> <span data-ttu-id="aef3d-179">Vous pouvez utiliser ce emplacements de paramètre tooget hello et les schémas définis par les jeux de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="aef3d-179">You can use this parameter tooget hello locations and schemas defined by input and output datasets.</span></span>
- <span data-ttu-id="aef3d-180">**activity**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-180">**activity**.</span></span> <span data-ttu-id="aef3d-181">Cette propriété représente l’activité en cours hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-181">This property represents hello current activity.</span></span> <span data-ttu-id="aef3d-182">Il peut être utilisé tooaccess les propriétés étendues associées d’activité personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-182">It can be used tooaccess extended properties associated with hello custom activity.</span></span> <span data-ttu-id="aef3d-183">Consultez la section [Accéder aux propriétés étendues](#access-extended-properties) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="aef3d-183">See [Access extended properties](#access-extended-properties) for details.</span></span>
- <span data-ttu-id="aef3d-184">**logger**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-184">**logger**.</span></span> <span data-ttu-id="aef3d-185">Cet objet vous permet d’écrire des commentaires de débogage survenant dans le journal d’utilisateur hello pour le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-185">This object lets you write debug comments that surface in hello user log for hello pipeline.</span></span>

<span data-ttu-id="aef3d-186">méthode Hello retourne un dictionnaire qui peut être des activités personnalisées toochain utilisées ensemble dans un avenir hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-186">hello method returns a dictionary that can be used toochain custom activities together in hello future.</span></span> <span data-ttu-id="aef3d-187">Cette fonctionnalité n’est pas encore implémentée, par conséquent, renvoyer un dictionnaire vide à partir de la méthode hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-187">This feature is not implemented yet, so return an empty dictionary from hello method.</span></span>  

### <a name="procedure"></a><span data-ttu-id="aef3d-188">Procédure</span><span class="sxs-lookup"><span data-stu-id="aef3d-188">Procedure</span></span>
1. <span data-ttu-id="aef3d-189">Créez un projet de **bibliothèque de classes .NET** .</span><span class="sxs-lookup"><span data-stu-id="aef3d-189">Create a **.NET Class Library** project.</span></span>
   <ol type="a">
     <li><span data-ttu-id="aef3d-190">Lancez <b>Visual Studio 2017</b> ou <b>Visual Studio 2015</b> ou <b>Visual Studio 2013</b> ou <b>Visual Studio 2012</b>.</span><span class="sxs-lookup"><span data-stu-id="aef3d-190">Launch <b>Visual Studio 2017</b> or <b>Visual Studio 2015</b> or <b>Visual Studio 2013</b> or <b>Visual Studio 2012</b>.</span></span></li>
     <li><span data-ttu-id="aef3d-191">Cliquez sur <b>fichier</b>, pointez trop<b>nouveau</b>, puis cliquez sur <b>projet</b>.</span><span class="sxs-lookup"><span data-stu-id="aef3d-191">Click <b>File</b>, point too<b>New</b>, and click <b>Project</b>.</span></span></li>
     <li><span data-ttu-id="aef3d-192">Développez <b>Modèles</b>, puis sélectionnez <b>Visual C#</b>.</span><span class="sxs-lookup"><span data-stu-id="aef3d-192">Expand <b>Templates</b>, and select <b>Visual C#</b>.</span></span> <span data-ttu-id="aef3d-193">Dans cette procédure pas à pas, vous utilisez c#, mais vous pouvez utiliser n’importe quel langage .NET toodevelop hello personnalisée activité.</span><span class="sxs-lookup"><span data-stu-id="aef3d-193">In this walkthrough, you use C#, but you can use any .NET language toodevelop hello custom activity.</span></span></li>
     <li><span data-ttu-id="aef3d-194">Sélectionnez <b>bibliothèque de classes</b> à partir de la liste hello des types de projets sur hello droite.</span><span class="sxs-lookup"><span data-stu-id="aef3d-194">Select <b>Class Library</b> from hello list of project types on hello right.</span></span> <span data-ttu-id="aef3d-195">Dans VS 2017, choisissez <b>Bibliothèque de classes (.NET Framework)</b> .</span><span class="sxs-lookup"><span data-stu-id="aef3d-195">In VS 2017, choose <b>Class Library (.NET Framework)</b> </span></span></li>
     <li><span data-ttu-id="aef3d-196">Entrez <b>MyDotNetActivity</b> pour hello <b>nom</b>.</span><span class="sxs-lookup"><span data-stu-id="aef3d-196">Enter <b>MyDotNetActivity</b> for hello <b>Name</b>.</span></span></li>
     <li><span data-ttu-id="aef3d-197">Sélectionnez <b>C:\ADFGetStarted</b> pour hello <b>emplacement</b>.</span><span class="sxs-lookup"><span data-stu-id="aef3d-197">Select <b>C:\ADFGetStarted</b> for hello <b>Location</b>.</span></span></li>
     <li><span data-ttu-id="aef3d-198">Cliquez sur <b>OK</b> projet hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="aef3d-198">Click <b>OK</b> toocreate hello project.</span></span></li>
   </ol><span data-ttu-id="aef3d-199">
2.Cliquez sur **outils**, pointez trop**Gestionnaire de Package NuGet**, puis cliquez sur **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-199">
2. Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
<span data-ttu-id="aef3d-200">3.</span><span class="sxs-lookup"><span data-stu-id="aef3d-200">3.</span></span> <span data-ttu-id="aef3d-201">Dans la Console du Gestionnaire de Package de hello, exécutez hello suivant commande tooimport **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-201">In hello Package Manager Console, execute hello following command tooimport **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="aef3d-202">Hello d’importation **Azure Storage** package NuGet dans le projet de toohello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-202">Import hello **Azure Storage** NuGet package in toohello project.</span></span>

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="aef3d-203">Lanceur de service de fabrique de données nécessite la version de hello 4.3 de WindowsAzure.Storage.</span><span class="sxs-lookup"><span data-stu-id="aef3d-203">Data Factory service launcher requires hello 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="aef3d-204">Si vous ajoutez une référence tooa une version ultérieure de l’assembly de stockage Azure dans votre projet d’activité personnalisée, vous voyez une erreur lors de l’exécution de l’activité hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-204">If you add a reference tooa later version of Azure Storage assembly in your custom activity project, you see an error when hello activity executes.</span></span> <span data-ttu-id="aef3d-205">Erreur de hello tooresolve, consultez [isolement de Appdomain](#appdomain-isolation) section.</span><span class="sxs-lookup"><span data-stu-id="aef3d-205">tooresolve hello error, see [Appdomain isolation](#appdomain-isolation) section.</span></span> 
5. <span data-ttu-id="aef3d-206">Ajoutez hello suivant **à l’aide de** instructions toohello source fichier hello projet.</span><span class="sxs-lookup"><span data-stu-id="aef3d-206">Add hello following **using** statements toohello source file in hello project.</span></span>

    ```csharp

    // Comment these lines if using VS 2017
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    // --------------------

    // Comment these lines if using <= VS 2015
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    // ---------------------

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="aef3d-207">Modifier le nom de hello hello **espace de noms** trop**MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-207">Change hello name of hello **namespace** too**MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="aef3d-208">Modifier le nom hello de classe hello trop**MyDotNetActivity** et la dériver de hello **IDotNetActivity** comme indiqué dans hello suivant extrait de code de l’interface :</span><span class="sxs-lookup"><span data-stu-id="aef3d-208">Change hello name of hello class too**MyDotNetActivity** and derive it from hello **IDotNetActivity** interface as shown in hello following code snippet:</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="aef3d-209">Hello d’implémenter (Ajouter) **Execute** méthode Hello **IDotNetActivity** interface toohello **MyDotNetActivity** classe et copie hello suivant l’exemple de méthode toohello de code.</span><span class="sxs-lookup"><span data-stu-id="aef3d-209">Implement (Add) hello **Execute** method of hello **IDotNetActivity** interface toohello **MyDotNetActivity** class and copy hello following sample code toohello method.</span></span>

    <span data-ttu-id="aef3d-210">Hello exemple suivant compte hello nombre d’occurrences du terme de recherche hello (« Microsoft ») dans chaque objet blob associé à une tranche de données.</span><span class="sxs-lookup"><span data-stu-id="aef3d-210">hello following sample counts hello number of occurrences of hello search term (“Microsoft”) in each blob associated with a data slice.</span></span>

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
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // toolog information, use hello logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get hello input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables toohold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from hello dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and hello other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get hello first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using hello same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get hello connection string in hello linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get hello folder path from hello input dataset definition
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
               // with hello data slice. definition of hello method is shown in hello next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for hello output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get hello folder path from hello output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log hello output folder path 
        logger.Write("Writing blob toohello folder: {0}", folderPath);
    
        // create a storage object for hello output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write hello name of hello file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log hello output file name
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
9. <span data-ttu-id="aef3d-211">Ajoutez hello les méthodes d’assistance suivantes :</span><span class="sxs-lookup"><span data-stu-id="aef3d-211">Add hello following helper methods:</span></span> 

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

        // get type properties of hello dataset 
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello folder path found in hello type properties
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
    
        // get type properties of hello dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello blob/file name in hello type properties
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

    <span data-ttu-id="aef3d-212">Hello GetFolderPath méthode renvoie hello chemin d’accès toohello qui hello dataset pointe dossier tooand hello GetFileName retourne hello nom de méthode hello/fichier blob qui hello pour les points de jeu de données.</span><span class="sxs-lookup"><span data-stu-id="aef3d-212">hello GetFolderPath method returns hello path toohello folder that hello dataset points tooand hello GetFileName method returns hello name of hello blob/file that hello dataset points to.</span></span> <span data-ttu-id="aef3d-213">Si vous havefolderPath définit à l’aide de variables telles que {Year}, {mois}, retourne des {Day}, etc., méthode hello hello chaîne car il est sans les remplacer par les valeurs d’exécution.</span><span class="sxs-lookup"><span data-stu-id="aef3d-213">If you havefolderPath defines using variables such as {Year}, {Month}, {Day} etc., hello method returns hello string as it is without replacing them with runtime values.</span></span> <span data-ttu-id="aef3d-214">Consultez la section [Accéder aux propriétés étendues](#access-extended-properties) pour plus d’informations sur l’accès à SliceStart, SliceEnd, etc.</span><span class="sxs-lookup"><span data-stu-id="aef3d-214">See [Access extended properties](#access-extended-properties) section for details on accessing SliceStart, SliceEnd, etc.</span></span>    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    <span data-ttu-id="aef3d-215">Hello méthode Calculate calcule le nombre hello d’instances du mot clé Microsoft dans les fichiers d’entrée de hello (objets BLOB dans le dossier de hello).</span><span class="sxs-lookup"><span data-stu-id="aef3d-215">hello Calculate method calculates hello number of instances of keyword Microsoft in hello input files (blobs in hello folder).</span></span> <span data-ttu-id="aef3d-216">terme de recherche Hello (« Microsoft ») est codé en dur dans le code hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-216">hello search term (“Microsoft”) is hard-coded in hello code.</span></span>
10. <span data-ttu-id="aef3d-217">Compilez le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-217">Compile hello project.</span></span> <span data-ttu-id="aef3d-218">Cliquez sur **générer** de hello menu et cliquez sur **générer la Solution**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-218">Click **Build** from hello menu and click **Build Solution**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="aef3d-219">4.5.2 de définir la version du .NET Framework comme infrastructure cible de hello pour votre projet : droit hello projet, puis cliquez sur **propriétés** tooset hello cible de .NET framework.</span><span class="sxs-lookup"><span data-stu-id="aef3d-219">Set 4.5.2 version of .NET Framework as hello target framework for your project: right-click hello project, and click **Properties** tooset hello target framework.</span></span> <span data-ttu-id="aef3d-220">Data Factory ne prend pas en charge les activités personnalisées compilées avec les versions de .NET Framework ultérieures à la version 4.5.2.</span><span class="sxs-lookup"><span data-stu-id="aef3d-220">Data Factory does not support custom activities compiled against .NET Framework versions later than 4.5.2.</span></span>

11. <span data-ttu-id="aef3d-221">Lancez **l’Explorateur Windows**, puis accédez trop**bin\debug** ou **bin\release** dossier en fonction de type hello de build.</span><span class="sxs-lookup"><span data-stu-id="aef3d-221">Launch **Windows Explorer**, and navigate too**bin\debug** or **bin\release** folder depending on hello type of build.</span></span>
12. <span data-ttu-id="aef3d-222">Créer un fichier zip **MyDotNetActivity.zip** qui contient tous les fichiers binaires de hello Bonjour <project folder>dossier \bin\Debug.</span><span class="sxs-lookup"><span data-stu-id="aef3d-222">Create a zip file **MyDotNetActivity.zip** that contains all hello binaries in hello <project folder>\bin\Debug folder.</span></span> <span data-ttu-id="aef3d-223">Inclure hello **MyDotNetActivity.pdb** de fichiers afin que vous obtenez les détails supplémentaires tels que numéro de ligne dans le code source hello qui a provoqué le problème de hello s’il existe un échec.</span><span class="sxs-lookup"><span data-stu-id="aef3d-223">Include hello **MyDotNetActivity.pdb** file so that you get additional details such as line number in hello source code that caused hello issue if there was a failure.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="aef3d-224">Tous les hello des fichiers dans le fichier zip de hello pour l’activité personnalisée hello doit se trouver au hello **niveau supérieur** avec aucune sous-dossiers.</span><span class="sxs-lookup"><span data-stu-id="aef3d-224">All hello files in hello zip file for hello custom activity must be at hello **top level** with no sub folders.</span></span>

    ![Fichiers de sortie binaires](./media/data-factory-use-custom-activities/Binaries.png)
14. <span data-ttu-id="aef3d-226">Si nécessaire, créez un conteneur de blobs nommé **customactivitycontainer**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-226">Create a blob container named **customactivitycontainer** if it does not already exist.</span></span> 
15. <span data-ttu-id="aef3d-227">Télécharger MyDotNetActivity.zip comme un customactivitycontainer de toohello d’objets blob dans un **à usage général** stockage d’objets blob Azure (stockage d’objets Blob à chaud pas/utile) qui est référencé par AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="aef3d-227">Upload MyDotNetActivity.zip as a blob toohello customactivitycontainer in a **general-purpose** Azure blob storage (not hot/cool Blob storage) that is referred by AzureStorageLinkedService.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="aef3d-228">Si vous ajoutez cette solution de tooa .NET activité projet dans Visual Studio qui contient un projet de la fabrique de données et ajoutez un projet d’activité too.NET référence de projet d’application hello fabrique de données, vous n’avez pas besoin de tooperform hello deux dernières étapes de création manuelle fichier zip de Hello et téléchargement de stockage d’objets blob Azure à usage général toohello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-228">If you add this .NET activity project tooa solution in Visual Studio that contains a Data Factory project, and add a reference too.NET activity project from hello Data Factory application project, you do not need tooperform hello last two steps of manually creating hello zip file and uploading it toohello general-purpose Azure blob storage.</span></span> <span data-ttu-id="aef3d-229">Lorsque vous publiez des entités de fabrique de données à l’aide de Visual Studio, ces étapes sont effectuées automatiquement par le processus de publication hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-229">When you publish Data Factory entities using Visual Studio, these steps are automatically done by hello publishing process.</span></span> <span data-ttu-id="aef3d-230">Pour plus d’informations, consultez la section [Projet Data Factory dans Visual Studio](#data-factory-project-in-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="aef3d-230">For more information, see [Data Factory project in Visual Studio](#data-factory-project-in-visual-studio) section.</span></span>

## <a name="create-a-pipeline-with-custom-activity"></a><span data-ttu-id="aef3d-231">Créer un pipeline avec une activité personnalisée</span><span class="sxs-lookup"><span data-stu-id="aef3d-231">Create a pipeline with custom activity</span></span>
<span data-ttu-id="aef3d-232">Vous avez créé une activité personnalisée et téléchargé le fichier zip de hello avec le conteneur d’objets blob binaires tooa dans un **à usage général** compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="aef3d-232">You have created a custom activity and uploaded hello zip file with binaries tooa blob container in a **general-purpose** Azure Storage Account.</span></span> <span data-ttu-id="aef3d-233">Dans cette section, vous créez une fabrique de données Azure avec un pipeline qui utilise l’activité personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-233">In this section, you create an Azure data factory with a pipeline that uses hello custom activity.</span></span>

<span data-ttu-id="aef3d-234">Hello un jeu de données d’entrée pour l’activité personnalisée hello représente les objets BLOB (fichiers) dans dossier de customactivityinput hello du conteneur adftutorial dans le stockage blob hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-234">hello input dataset for hello custom activity represents blobs (files) in hello customactivityinput folder of adftutorial container in hello blob storage.</span></span> <span data-ttu-id="aef3d-235">le dataset de sortie Hello pour l’activité de hello représente des objets BLOB de sortie dans le dossier de customactivityoutput hello du conteneur adftutorial dans le stockage blob hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-235">hello output dataset for hello activity represents output blobs in hello customactivityoutput folder of adftutorial container in hello blob storage.</span></span>

<span data-ttu-id="aef3d-236">Créer **fichier.txt** fichier avec hello suivante de contenu et le télécharger trop**customactivityinput** dossier Hello **adftutorial** conteneur.</span><span class="sxs-lookup"><span data-stu-id="aef3d-236">Create **file.txt** file with hello following content and upload it too**customactivityinput** folder of hello **adftutorial** container.</span></span> <span data-ttu-id="aef3d-237">Créer le conteneur d’adftutorial hello s’il n’existe pas déjà.</span><span class="sxs-lookup"><span data-stu-id="aef3d-237">Create hello adftutorial container if it does not exist already.</span></span> 

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="aef3d-238">dossier d’entrée de Hello correspond tranche tooa dans Azure Data Factory, même si le dossier de hello a deux ou plusieurs fichiers.</span><span class="sxs-lookup"><span data-stu-id="aef3d-238">hello input folder corresponds tooa slice in Azure Data Factory even if hello folder has two or more files.</span></span> <span data-ttu-id="aef3d-239">Lorsque chaque tranche est traitée par le pipeline de hello, activité personnalisée hello itère tous les objets BLOB de hello dans le dossier d’entrée de hello pour cette tranche.</span><span class="sxs-lookup"><span data-stu-id="aef3d-239">When each slice is processed by hello pipeline, hello custom activity iterates through all hello blobs in hello input folder for that slice.</span></span>

<span data-ttu-id="aef3d-240">Vous consultez un fichier avec hello adftutorial\customactivityoutput dossier de sortie avec une ou plusieurs lignes (identique au nombre d’objets BLOB dans le dossier d’entrée de hello) :</span><span class="sxs-lookup"><span data-stu-id="aef3d-240">You see one output file with in hello adftutorial\customactivityoutput folder with one or more lines (same as number of blobs in hello input folder):</span></span>

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
```


<span data-ttu-id="aef3d-241">Voici les étapes hello que vous effectuez dans cette section :</span><span class="sxs-lookup"><span data-stu-id="aef3d-241">Here are hello steps you perform in this section:</span></span>

1. <span data-ttu-id="aef3d-242">Création d'une **fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-242">Create a **data factory**.</span></span>
2. <span data-ttu-id="aef3d-243">Créer **services liés** pour le pool de traitement par lots Azure hello de machines virtuelles sur le hello activité personnalisée s’exécute et hello le stockage Azure qui contient des objets BLOB d’entrée/sortie hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-243">Create **Linked services** for hello Azure Batch pool of VMs on which hello custom activity runs and hello Azure Storage that holds hello input/output blobs.</span></span>
3. <span data-ttu-id="aef3d-244">Créer des entrées et sorties **datasets** qui représentent l’entrée et sortie de l’activité personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-244">Create input and output **datasets** that represent input and output of hello custom activity.</span></span>
4. <span data-ttu-id="aef3d-245">Créer un **pipeline** qui utilise l’activité personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-245">Create a **pipeline** that uses hello custom activity.</span></span>

> [!NOTE]
> <span data-ttu-id="aef3d-246">Créer hello **fichier.txt** et télécharger le conteneur d’objets blob tooa si vous n’avez pas déjà fait.</span><span class="sxs-lookup"><span data-stu-id="aef3d-246">Create hello **file.txt** and upload it tooa blob container if you haven't already done so.</span></span> <span data-ttu-id="aef3d-247">Consultez les instructions dans la précédente section de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-247">See instructions in hello preceding section.</span></span>   

### <a name="step-1-create-hello-data-factory"></a><span data-ttu-id="aef3d-248">Étape 1 : Créer la fabrique de données hello</span><span class="sxs-lookup"><span data-stu-id="aef3d-248">Step 1: Create hello data factory</span></span>
1. <span data-ttu-id="aef3d-249">Après l’ouverture dans toohello le portail Azure, procédez comme hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="aef3d-249">After logging in toohello Azure portal, do hello following steps:</span></span>
   1. <span data-ttu-id="aef3d-250">Cliquez sur **nouveau** sur le menu de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-250">Click **NEW** on hello left menu.</span></span>
   2. <span data-ttu-id="aef3d-251">Cliquez sur **données + Analytique** Bonjour **nouveau** panneau.</span><span class="sxs-lookup"><span data-stu-id="aef3d-251">Click **Data + Analytics** in hello **New** blade.</span></span>
   3. <span data-ttu-id="aef3d-252">Cliquez sur **Data Factory** sur hello **analytique des données** panneau.</span><span class="sxs-lookup"><span data-stu-id="aef3d-252">Click **Data Factory** on hello **Data analytics** blade.</span></span>
   
    ![Nouveau menu Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. <span data-ttu-id="aef3d-254">Bonjour **nouvelle fabrique de données** panneau, entrez **CustomActivityFactory** pour hello nom.</span><span class="sxs-lookup"><span data-stu-id="aef3d-254">In hello **New data factory** blade, enter **CustomActivityFactory** for hello Name.</span></span> <span data-ttu-id="aef3d-255">nom de Hello de fabrique de données Azure hello doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="aef3d-255">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="aef3d-256">Si vous recevez une erreur de hello : **nom de fabrique de données « CustomActivityFactory » n’est pas disponible**, modifiez le nom hello hello fabrique de données (par exemple, **yournameCustomActivityFactory**) et essayez de créer à nouveau.</span><span class="sxs-lookup"><span data-stu-id="aef3d-256">If you receive hello error: **Data factory name “CustomActivityFactory” is not available**, change hello name of hello data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>

    ![Nouveau panneau Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. <span data-ttu-id="aef3d-258">Cliquez sur **NOM DU GROUPE DE RESSOURCES**pour sélectionner un groupe de ressources existant, ou créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="aef3d-258">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="aef3d-259">Vérifiez que vous utilisez hello correct **abonnement** et **région** où vous souhaitez toobe de fabrique de données hello créé.</span><span class="sxs-lookup"><span data-stu-id="aef3d-259">Verify that you are using hello correct **subscription** and **region** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="aef3d-260">Cliquez sur **créer** sur hello **nouvelle fabrique de données** panneau.</span><span class="sxs-lookup"><span data-stu-id="aef3d-260">Click **Create** on hello **New data factory** blade.</span></span>
6. <span data-ttu-id="aef3d-261">Vous voyez la fabrique de données hello en cours de création dans hello **tableau de bord** de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="aef3d-261">You see hello data factory being created in hello **Dashboard** of hello Azure portal.</span></span>
7. <span data-ttu-id="aef3d-262">Une fois que la fabrique de données hello a été créé avec succès, vous voyez panneau hello fabrique de données, qui vous indique hello contenu hello fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="aef3d-262">After hello data factory has been created successfully, you see hello Data Factory blade, which shows you hello contents of hello data factory.</span></span>
    
    ![Panneau Data Factory](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a><span data-ttu-id="aef3d-264">Étape 2 : Créer des services liés</span><span class="sxs-lookup"><span data-stu-id="aef3d-264">Step 2: Create linked services</span></span>
<span data-ttu-id="aef3d-265">Services liés lier des magasins de données ou la fabrique de données Azure tooan de services de calcul.</span><span class="sxs-lookup"><span data-stu-id="aef3d-265">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="aef3d-266">Dans cette étape, vous liez votre compte de stockage Azure et d’un traitement par lots Azure compte tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="aef3d-266">In this step, you link your Azure Storage account and Azure Batch account tooyour data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="aef3d-267">Créer le service lié Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="aef3d-267">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="aef3d-268">Cliquez sur hello **auteur et déployer** vignette sur hello **DATA FACTORY** panneau pour **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-268">Click hello **Author and deploy** tile on hello **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="aef3d-269">Vous consultez hello éditeur Data Factory.</span><span class="sxs-lookup"><span data-stu-id="aef3d-269">You see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="aef3d-270">Cliquez sur **nouveau magasin de données** hello de barre de commandes et choisissez **le stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-270">Click **New data store** on hello command bar and choose **Azure storage**.</span></span> <span data-ttu-id="aef3d-271">Vous devez voir hello script JSON pour la création d’un stockage Azure lié à service dans l’éditeur de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-271">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>
    
    ![Nouveau magasin de données - Stockage Azure](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. <span data-ttu-id="aef3d-273">Remplacez `<accountname>` avec le nom de votre compte de stockage Azure et `<accountkey>` avec la clé d’accès de hello compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="aef3d-273">Replace `<accountname>` with name of your Azure storage account and `<accountkey>` with access key of hello Azure storage account.</span></span> <span data-ttu-id="aef3d-274">toolearn comment tooget votre stockage accéder aux clés, voir [clés d’accès afficher, copier et régénérer stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="aef3d-274">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

    ![Service lié Stockage Azure](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. <span data-ttu-id="aef3d-276">Cliquez sur **déployer** sur toodeploy hello lié service de la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-276">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="aef3d-277">Créer un service lié Azure Batch</span><span class="sxs-lookup"><span data-stu-id="aef3d-277">Create Azure Batch linked service</span></span>
1. <span data-ttu-id="aef3d-278">Bonjour éditeur Data Factory, cliquez sur **... Plus** dans la barre de commandes hello, cliquez sur **nouveau calcul**, puis sélectionnez **Azure Batch** à partir du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-278">In hello Data Factory Editor, click **... More** on hello command bar, click **New compute**, and then select **Azure Batch** from hello menu.</span></span>

    ![Nouveau calcul - Azure Batch](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. <span data-ttu-id="aef3d-280">Rendre hello modifications toohello JSON script suivant :</span><span class="sxs-lookup"><span data-stu-id="aef3d-280">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="aef3d-281">Spécifiez le nom du compte Azure Batch pour hello **accountName** propriété.</span><span class="sxs-lookup"><span data-stu-id="aef3d-281">Specify Azure Batch account name for hello **accountName** property.</span></span> <span data-ttu-id="aef3d-282">Hello **URL** de hello **Panneau de compte Azure Batch** est Bonjour suivant le format : `http://accountname.region.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="aef3d-282">hello **URL** from hello **Azure Batch account blade** is in hello following format: `http://accountname.region.batch.azure.com`.</span></span> <span data-ttu-id="aef3d-283">Pourquoi **batchUri** propriété hello JSON, vous devez tooremove `accountname.` de hello URL et l’utilisation de hello `accountname` pour hello `accountName` propriété JSON.</span><span class="sxs-lookup"><span data-stu-id="aef3d-283">For hello **batchUri** property in hello JSON, you need tooremove `accountname.` from hello URL and use hello `accountname` for hello `accountName` JSON property.</span></span>
   2. <span data-ttu-id="aef3d-284">Spécifiez la clé de compte Azure Batch hello pour hello **accessKey** propriété.</span><span class="sxs-lookup"><span data-stu-id="aef3d-284">Specify hello Azure Batch account key for hello **accessKey** property.</span></span>
   3. <span data-ttu-id="aef3d-285">Spécifiez nom hello de pool hello vous avez créé dans le cadre de la configuration requise pour hello **poolName** propriété.</span><span class="sxs-lookup"><span data-stu-id="aef3d-285">Specify hello name of hello pool you created as part of prerequisites for hello **poolName** property.</span></span> <span data-ttu-id="aef3d-286">Vous pouvez également spécifier les ID hello du pool hello au lieu du nom de hello du pool de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-286">You can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>
   4. <span data-ttu-id="aef3d-287">Spécifiez l’URI du lot Azure pour hello **batchUri** propriété.</span><span class="sxs-lookup"><span data-stu-id="aef3d-287">Specify Azure Batch URI for hello **batchUri** property.</span></span> <span data-ttu-id="aef3d-288">Exemple : `https://westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="aef3d-288">Example: `https://westus.batch.azure.com`.</span></span>  
   5. <span data-ttu-id="aef3d-289">Spécifiez hello **AzureStorageLinkedService** pour hello **linkedServiceName** propriété.</span><span class="sxs-lookup"><span data-stu-id="aef3d-289">Specify hello **AzureStorageLinkedService** for hello **linkedServiceName** property.</span></span>

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       <span data-ttu-id="aef3d-290">Pourquoi **poolName** propriété, vous pouvez également spécifier d’ID hello du pool hello au lieu du nom de hello du pool de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-290">For hello **poolName** property, you can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="aef3d-291">Hello service Data Factory ne prend en charge une option à la demande de traitement par lots Azure comme il le fait pour HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aef3d-291">hello Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="aef3d-292">Vous pouvez uniquement utiliser votre propre pool Azure Batch dans une fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="aef3d-292">You can only use your own Azure Batch pool in an Azure data factory.</span></span>   
    

### <a name="step-3-create-datasets"></a><span data-ttu-id="aef3d-293">Étape 3 : Créer les jeux de données</span><span class="sxs-lookup"><span data-stu-id="aef3d-293">Step 3: Create datasets</span></span>
<span data-ttu-id="aef3d-294">Dans cette étape, vous créez une entrée de toorepresent de jeux de données et les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="aef3d-294">In this step, you create datasets toorepresent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="aef3d-295">Créer le jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="aef3d-295">Create input dataset</span></span>
1. <span data-ttu-id="aef3d-296">Bonjour **éditeur** pour hello fabrique de données, cliquez sur **... Plus** dans la barre de commandes hello, cliquez sur **nouveau dataset**, puis sélectionnez **le stockage Blob Azure** à partir du menu déroulant de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-296">In hello **Editor** for hello Data Factory, click **... More** on hello command bar, click **New dataset**, and then select **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="aef3d-297">Remplacez hello JSON dans le volet de droite hello hello suivant extrait de code JSON :</span><span class="sxs-lookup"><span data-stu-id="aef3d-297">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
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

   <span data-ttu-id="aef3d-298">Plus loin dans cette procédure pas à pas, vous allez créer un pipeline associé à l’heure de début 2016-11-16T00:00:00Z et à l’heure de fin 2016-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="aef3d-298">You create a pipeline later in this walkthrough with start time: 2016-11-16T00:00:00Z and end time: 2016-11-16T05:00:00Z.</span></span> <span data-ttu-id="aef3d-299">Ce sont des données de tooproduce planifiée toutes les heures, il y a cinq tranches d’entrée/sortie (entre **00**: 00:00 -> **05**: 00:00).</span><span class="sxs-lookup"><span data-stu-id="aef3d-299">It is scheduled tooproduce data hourly, so there are five input/output slices (between **00**:00:00 -> **05**:00:00).</span></span>

   <span data-ttu-id="aef3d-300">Hello **fréquence** et **intervalle** de jeu de données d’entrée hello est défini trop**heure** et **1**, ce qui signifie que hello entrée tranche est disponible toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="aef3d-300">hello **frequency** and **interval** for hello input dataset is set too**Hour** and **1**, which means that hello input slice is available hourly.</span></span> <span data-ttu-id="aef3d-301">Dans cet exemple, il est même hello hello intputfolder fichier (fichier.txt).</span><span class="sxs-lookup"><span data-stu-id="aef3d-301">In this sample, it is hello same file (file.txt) in hello intputfolder.</span></span>

   <span data-ttu-id="aef3d-302">Voici les heures de début hello pour chaque secteur, qui est représentée par la variable de système SliceStart Bonjour ci-dessus extrait de code JSON.</span><span class="sxs-lookup"><span data-stu-id="aef3d-302">Here are hello start times for each slice, which is represented by SliceStart system variable in hello above JSON snippet.</span></span>
3. <span data-ttu-id="aef3d-303">Cliquez sur **déployer** hello toocreate de barre d’outils et déployer hello **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-303">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset**.</span></span> <span data-ttu-id="aef3d-304">Vérifiez que vous voyez hello **TABLE créée avec succès** message sur la barre de titre hello Hello éditeur.</span><span class="sxs-lookup"><span data-stu-id="aef3d-304">Confirm that you see hello **TABLE CREATED SUCCESSFULLY** message on hello title bar of hello Editor.</span></span>

#### <a name="create-an-output-dataset"></a><span data-ttu-id="aef3d-305">Créer un jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="aef3d-305">Create an output dataset</span></span>
1. <span data-ttu-id="aef3d-306">Bonjour **l’éditeur Data Factory**, cliquez sur **... Plus** dans la barre de commandes hello, cliquez sur **nouveau dataset**, puis sélectionnez **le stockage Blob Azure**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-306">In hello **Data Factory editor**, click **... More** on hello command bar, click **New dataset**, and then select **Azure Blob storage**.</span></span>
2. <span data-ttu-id="aef3d-307">Remplacez script JSON de hello dans le volet de droite hello hello JSON script suivant :</span><span class="sxs-lookup"><span data-stu-id="aef3d-307">Replace hello JSON script in hello right pane with hello following JSON script:</span></span>

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
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

     <span data-ttu-id="aef3d-308">Emplacement de sortie est **adftutorial/customactivityoutput/** et le nom de fichier de sortie est AAAA-MM-JJ-HH.txt où AAAA-MM-JJ-HH est hello year, month, date et l’heure de tranche hello fabriqué.</span><span class="sxs-lookup"><span data-stu-id="aef3d-308">Output location is **adftutorial/customactivityoutput/** and output file name is yyyy-MM-dd-HH.txt where yyyy-MM-dd-HH is hello year, month, date, and hour of hello slice being produced.</span></span> <span data-ttu-id="aef3d-309">Pour en savoir plus, consultez la page [Référence du développeur][adf-developer-reference].</span><span class="sxs-lookup"><span data-stu-id="aef3d-309">See [Developer Reference][adf-developer-reference] for details.</span></span>

    <span data-ttu-id="aef3d-310">Un objet blob/fichier de sortie est généré pour chaque tranche d’entrée.</span><span class="sxs-lookup"><span data-stu-id="aef3d-310">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="aef3d-311">Voici la procédure de nommage des fichiers de sortie pour chaque tranche.</span><span class="sxs-lookup"><span data-stu-id="aef3d-311">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="aef3d-312">Tous les fichiers de sortie hello sont générés dans un dossier de sortie : **adftutorial\customactivityoutput**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-312">All hello output files are generated in one output folder: **adftutorial\customactivityoutput**.</span></span>

   | <span data-ttu-id="aef3d-313">Tranche</span><span class="sxs-lookup"><span data-stu-id="aef3d-313">Slice</span></span> | <span data-ttu-id="aef3d-314">Heure de début</span><span class="sxs-lookup"><span data-stu-id="aef3d-314">Start time</span></span> | <span data-ttu-id="aef3d-315">Fichier de sortie</span><span class="sxs-lookup"><span data-stu-id="aef3d-315">Output file</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="aef3d-316">1</span><span class="sxs-lookup"><span data-stu-id="aef3d-316">1</span></span> |<span data-ttu-id="aef3d-317">2016-11-16T00:00:00</span><span class="sxs-lookup"><span data-stu-id="aef3d-317">2016-11-16T00:00:00</span></span> |<span data-ttu-id="aef3d-318">2016-11-16-00.txt</span><span class="sxs-lookup"><span data-stu-id="aef3d-318">2016-11-16-00.txt</span></span> |
   | <span data-ttu-id="aef3d-319">2</span><span class="sxs-lookup"><span data-stu-id="aef3d-319">2</span></span> |<span data-ttu-id="aef3d-320">2016-11-16T01:00:00</span><span class="sxs-lookup"><span data-stu-id="aef3d-320">2016-11-16T01:00:00</span></span> |<span data-ttu-id="aef3d-321">2016-11-16-01.txt</span><span class="sxs-lookup"><span data-stu-id="aef3d-321">2016-11-16-01.txt</span></span> |
   | <span data-ttu-id="aef3d-322">3</span><span class="sxs-lookup"><span data-stu-id="aef3d-322">3</span></span> |<span data-ttu-id="aef3d-323">2016-11-16T02:00:00</span><span class="sxs-lookup"><span data-stu-id="aef3d-323">2016-11-16T02:00:00</span></span> |<span data-ttu-id="aef3d-324">2016-11-16-02.txt</span><span class="sxs-lookup"><span data-stu-id="aef3d-324">2016-11-16-02.txt</span></span> |
   | <span data-ttu-id="aef3d-325">4</span><span class="sxs-lookup"><span data-stu-id="aef3d-325">4</span></span> |<span data-ttu-id="aef3d-326">2016-11-16T03:00:00</span><span class="sxs-lookup"><span data-stu-id="aef3d-326">2016-11-16T03:00:00</span></span> |<span data-ttu-id="aef3d-327">2016-11-16-03.txt</span><span class="sxs-lookup"><span data-stu-id="aef3d-327">2016-11-16-03.txt</span></span> |
   | <span data-ttu-id="aef3d-328">5</span><span class="sxs-lookup"><span data-stu-id="aef3d-328">5</span></span> |<span data-ttu-id="aef3d-329">2016-11-16T04:00:00</span><span class="sxs-lookup"><span data-stu-id="aef3d-329">2016-11-16T04:00:00</span></span> |<span data-ttu-id="aef3d-330">2016-11-16-04.txt</span><span class="sxs-lookup"><span data-stu-id="aef3d-330">2016-11-16-04.txt</span></span> |

    <span data-ttu-id="aef3d-331">N’oubliez pas que tous les fichiers hello dans un dossier d’entrée font partie d’une section avec des heures de début hello mentionnés ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="aef3d-331">Remember that all hello files in an input folder are part of a slice with hello start times mentioned above.</span></span> <span data-ttu-id="aef3d-332">Lorsque cette tranche est traitée, activité personnalisée hello parcourt chaque fichier et produit une ligne dans le fichier de sortie hello avec numéro hello d’occurrences du terme de recherche (« Microsoft »).</span><span class="sxs-lookup"><span data-stu-id="aef3d-332">When this slice is processed, hello custom activity scans through each file and produces a line in hello output file with hello number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="aef3d-333">S’il existe trois fichiers dans hello inputfolder, il existe trois lignes dans le fichier de sortie hello pour chaque tranche horaire : 2016-11-16-00.txt 2016-11-16:01:00:00.txt, etc..</span><span class="sxs-lookup"><span data-stu-id="aef3d-333">If there are three files in hello inputfolder, there are three lines in hello output file for each hourly slice: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.</span></span>
3. <span data-ttu-id="aef3d-334">toodeploy hello **OutputDataset**, cliquez sur **déployer** sur la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-334">toodeploy hello **OutputDataset**, click **Deploy** on hello command bar.</span></span>

### <a name="create-and-run-a-pipeline-that-uses-hello-custom-activity"></a><span data-ttu-id="aef3d-335">Créer et exécuter un pipeline qui utilise l’activité personnalisée hello</span><span class="sxs-lookup"><span data-stu-id="aef3d-335">Create and run a pipeline that uses hello custom activity</span></span>
1. <span data-ttu-id="aef3d-336">Bonjour éditeur Data Factory, cliquez sur **... Plus**, puis sélectionnez **nouveau pipeline** sur la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-336">In hello Data Factory Editor, click **... More**, and then select **New pipeline** on hello command bar.</span></span> 
2. <span data-ttu-id="aef3d-337">Remplacez hello JSON dans le volet de droite hello hello JSON script suivant :</span><span class="sxs-lookup"><span data-stu-id="aef3d-337">Replace hello JSON in hello right pane with hello following JSON script:</span></span>

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    <span data-ttu-id="aef3d-338">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="aef3d-338">Note hello following points:</span></span>

   * <span data-ttu-id="aef3d-339">**Accès concurrentiel** est défini trop**2** afin que les deux sections sont traitées en parallèle par 2 machines virtuelles dans le pool de traitement par lots Azure hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-339">**Concurrency** is set too**2** so that two slices are processed in parallel by 2 VMs in hello Azure Batch pool.</span></span>
   * <span data-ttu-id="aef3d-340">Il existe une activité dans la section des activités hello et elle est de type : **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-340">There is one activity in hello activities section and it is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="aef3d-341">**AssemblyName** a la valeur nom toohello Hello DLL : **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-341">**AssemblyName** is set toohello name of hello DLL: **MyDotnetActivity.dll**.</span></span>
   * <span data-ttu-id="aef3d-342">**Point d’entrée** est défini trop**MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-342">**EntryPoint** is set too**MyDotNetActivityNS.MyDotNetActivity**.</span></span>
   * <span data-ttu-id="aef3d-343">**PackageLinkedService** est défini trop**AzureStorageLinkedService** qui pointe le stockage d’objets blob toohello qui contient le fichier zip d’activité personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-343">**PackageLinkedService** is set too**AzureStorageLinkedService** that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="aef3d-344">Si vous n’utilisez pas d’entrée/sortient de différents comptes de stockage Azure pour les fichiers et hello fichier zip d’activité personnalisée, vous créez un autre service lié Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="aef3d-344">If you are using different Azure Storage accounts for input/output files and hello custom activity zip file, you create another Azure Storage linked service.</span></span> <span data-ttu-id="aef3d-345">Cet article suppose que vous utilisez hello même compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="aef3d-345">This article assumes that you are using hello same Azure Storage account.</span></span>
   * <span data-ttu-id="aef3d-346">**PackageFile** est défini trop**customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-346">**PackageFile** is set too**customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="aef3d-347">Il est au format de hello : containerforthezip/nameofthezip.zip.</span><span class="sxs-lookup"><span data-stu-id="aef3d-347">It is in hello format: containerforthezip/nameofthezip.zip.</span></span>
   * <span data-ttu-id="aef3d-348">activité personnalisée Hello prend **InputDataset** en tant qu’entrée et **OutputDataset** en tant que sortie.</span><span class="sxs-lookup"><span data-stu-id="aef3d-348">hello custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="aef3d-349">propriété de linkedServiceName Hello d’activité personnalisée hello pointe toohello **AzureBatchLinkedService**, ce qui indique à Azure Data Factory pour cette activité personnalisée hello doit toorun sur des machines virtuelles de traitement par lots Azure.</span><span class="sxs-lookup"><span data-stu-id="aef3d-349">hello linkedServiceName property of hello custom activity points toohello **AzureBatchLinkedService**, which tells Azure Data Factory that hello custom activity needs toorun on Azure Batch VMs.</span></span>
   * <span data-ttu-id="aef3d-350">**isPaused** propriété a la valeur trop**false** par défaut.</span><span class="sxs-lookup"><span data-stu-id="aef3d-350">**isPaused** property is set too**false** by default.</span></span> <span data-ttu-id="aef3d-351">pipeline de Hello s’exécute immédiatement dans cet exemple, car le début des tranches de hello Bonjour passées.</span><span class="sxs-lookup"><span data-stu-id="aef3d-351">hello pipeline runs immediately in this example because hello slices start in hello past.</span></span> <span data-ttu-id="aef3d-352">Vous pouvez définir ce pipeline de propriété tootrue toopause hello et affectez-lui arrière toofalse toorestart.</span><span class="sxs-lookup"><span data-stu-id="aef3d-352">You can set this property tootrue toopause hello pipeline and set it back toofalse toorestart.</span></span>
   * <span data-ttu-id="aef3d-353">Hello **Démarrer** temps et **fin** heures sont **cinq** heures éloignés et tranches produites toutes les heures, afin de cinq tranches sont produits par le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-353">hello **start** time and **end** times are **five** hours apart and slices are produced hourly, so five slices are produced by hello pipeline.</span></span>
3. <span data-ttu-id="aef3d-354">pipeline de hello toodeploy, cliquez sur **déployer** sur la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-354">toodeploy hello pipeline, click **Deploy** on hello command bar.</span></span>

### <a name="monitor-hello-pipeline"></a><span data-ttu-id="aef3d-355">Pipeline d’analyse hello</span><span class="sxs-lookup"><span data-stu-id="aef3d-355">Monitor hello pipeline</span></span>
1. <span data-ttu-id="aef3d-356">Dans le panneau de la fabrique de données hello Bonjour portail Azure, cliquez sur **diagramme**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-356">In hello Data Factory blade in hello Azure portal, click **Diagram**.</span></span>

    ![Vignette schématique](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. <span data-ttu-id="aef3d-358">Bonjour vue de diagramme, cliquez maintenant sur hello OutputDataset.</span><span class="sxs-lookup"><span data-stu-id="aef3d-358">In hello Diagram View, now click hello OutputDataset.</span></span>

    ![Vue schématique](./media/data-factory-use-custom-activities/diagram.png)
3. <span data-ttu-id="aef3d-360">Vous devez voir que les cinq tranches de sortie hello sont dans l’état prêt hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-360">You should see that hello five output slices are in hello Ready state.</span></span> <span data-ttu-id="aef3d-361">S’ils ne sont pas dans l’état prêt hello, ils n’ont pas encore été générés.</span><span class="sxs-lookup"><span data-stu-id="aef3d-361">If they are not in hello Ready state, they haven't been produced yet.</span></span> 

   ![Tranches de sortie](./media/data-factory-use-custom-activities/OutputSlices.png)
4. <span data-ttu-id="aef3d-363">Vérifiez que les fichiers de sortie hello sont générées dans le stockage blob hello hello **adftutorial** conteneur.</span><span class="sxs-lookup"><span data-stu-id="aef3d-363">Verify that hello output files are generated in hello blob storage in hello **adftutorial** container.</span></span>

   ![Sortie de l’activité personnalisée][image-data-factory-ouput-from-custom-activity]
5. <span data-ttu-id="aef3d-365">Si vous ouvrez le fichier de sortie hello, vous devez voir hello toohello similaire après la sortie de sortie :</span><span class="sxs-lookup"><span data-stu-id="aef3d-365">If you open hello output file, you should see hello output similar toohello following output:</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
    ```
6. <span data-ttu-id="aef3d-366">Hello d’utilisation [portail Azure] [ azure-preview-portal] ou toomonitor d’applets de commande Azure PowerShell votre fabrique de données, les pipelines et les jeux de données.</span><span class="sxs-lookup"><span data-stu-id="aef3d-366">Use hello [Azure portal][azure-preview-portal] or Azure PowerShell cmdlets toomonitor your data factory, pipelines, and data sets.</span></span> <span data-ttu-id="aef3d-367">Vous pouvez voir des messages à partir de hello **ActivityLogger** dans le code hello pour une activité personnalisée hello dans les journaux de hello (spécifiquement 0.log utilisateur) que vous pouvez télécharger à partir de portail de hello ou à l’aide des applets de commande.</span><span class="sxs-lookup"><span data-stu-id="aef3d-367">You can see messages from hello **ActivityLogger** in hello code for hello custom activity in hello logs (specifically user-0.log) that you can download from hello portal or using cmdlets.</span></span>

   ![Téléchargement des journaux d’activités personnalisées][image-data-factory-download-logs-from-custom-activity]

<span data-ttu-id="aef3d-369">Pour découvrir la procédure détaillée de surveillance des jeux de données et des pipelines, consultez l’article [Surveiller et gérer les pipelines](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="aef3d-369">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) for detailed steps for monitoring datasets and pipelines.</span></span>      

## <a name="data-factory-project-in-visual-studio"></a><span data-ttu-id="aef3d-370">Projet Data Factory dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aef3d-370">Data Factory project in Visual Studio</span></span>  
<span data-ttu-id="aef3d-371">Vous pouvez créer et publier des entités Data Factory à l’aide de Visual Studio au lieu d’utiliser le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="aef3d-371">You can create and publish Data Factory entities by using Visual Studio instead of using Azure portal.</span></span> <span data-ttu-id="aef3d-372">Pour plus d’informations sur la création et les entités de fabrique de données de publication à l’aide de Visual Studio, consultez [générer votre première pipeline à l’aide de Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) et [copier les données d’objets Blob Azure tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) articles.</span><span class="sxs-lookup"><span data-stu-id="aef3d-372">For detailed information about creating and publishing Data Factory entities by using Visual Studio, See [Build your first pipeline using Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) and [Copy data from Azure Blob tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) articles.</span></span>

<span data-ttu-id="aef3d-373">Hello suivant les étapes supplémentaires si vous créez un projet de la fabrique de données dans Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="aef3d-373">Do hello following additional steps if you are creating Data Factory project in Visual Studio:</span></span>
 
1. <span data-ttu-id="aef3d-374">Ajoutez hello Data Factory projet toohello solution Visual Studio qui contient le projet d’activité personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-374">Add hello Data Factory project toohello Visual Studio solution that contains hello custom activity project.</span></span> 
2. <span data-ttu-id="aef3d-375">Ajouter un projet d’activité de référence toohello .NET à partir du projet de Data Factory hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-375">Add a reference toohello .NET activity project from hello Data Factory project.</span></span> <span data-ttu-id="aef3d-376">Cliquez sur le projet de la fabrique de données, pointez trop**ajouter**, puis cliquez sur **référence**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-376">Right-click Data Factory project, point too**Add**, and then click **Reference**.</span></span> 
3. <span data-ttu-id="aef3d-377">Bonjour **ajouter une référence** boîte de dialogue, sélectionnez hello **MyDotNetActivity** le projet, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-377">In hello **Add Reference** dialog box, select hello **MyDotNetActivity** project, and click **OK**.</span></span>
4. <span data-ttu-id="aef3d-378">Générer et publier des solutions de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-378">Build and publish hello solution.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="aef3d-379">Lorsque vous publiez des entités de fabrique de données, un fichier zip est créé automatiquement pour vous et est le conteneur d’objets blob téléchargés toohello : customactivitycontainer.</span><span class="sxs-lookup"><span data-stu-id="aef3d-379">When you publish Data Factory entities, a zip file is automatically created for you and is uploaded toohello blob container: customactivitycontainer.</span></span> <span data-ttu-id="aef3d-380">Si le conteneur d’objets blob hello n’existe pas, il est automatiquement créé trop.</span><span class="sxs-lookup"><span data-stu-id="aef3d-380">If hello blob container does not exist, it is automatically created too.</span></span>  


## <a name="data-factory-and-batch-integration"></a><span data-ttu-id="aef3d-381">Intégration de Data Factory et Batch</span><span class="sxs-lookup"><span data-stu-id="aef3d-381">Data Factory and Batch integration</span></span>
<span data-ttu-id="aef3d-382">Hello service Data Factory crée un travail en traitement par lots Azure avec le nom de hello : **adf-poolname : xxx-travail**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-382">hello Data Factory service creates a job in Azure Batch with hello name: **adf-poolname: job-xxx**.</span></span> <span data-ttu-id="aef3d-383">Cliquez sur **travaux** à partir du menu de gauche hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-383">Click **Jobs** from hello left menu.</span></span> 

![Azure Data Factory - Travaux Batch](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

<span data-ttu-id="aef3d-385">Une tâche est créée pour chaque exécution d’activité d’une tranche.</span><span class="sxs-lookup"><span data-stu-id="aef3d-385">A task is created for each activity run of a slice.</span></span> <span data-ttu-id="aef3d-386">S’il existe cinq toobe prêt tranches traitées, cinq tâches sont créés dans cette tâche.</span><span class="sxs-lookup"><span data-stu-id="aef3d-386">If there are five slices ready toobe processed, five tasks are created in this job.</span></span> <span data-ttu-id="aef3d-387">S’il existe plusieurs nœuds de calcul dans le pool de traitement par lots de hello, deux ou plusieurs secteurs peuvent s’exécuter en parallèle.</span><span class="sxs-lookup"><span data-stu-id="aef3d-387">If there are multiple compute nodes in hello Batch pool, two or more slices can run in parallel.</span></span> <span data-ttu-id="aef3d-388">Si le nombre maximum de tâches hello par jeu de nœud de calcul trop > 1, vous pouvez également avoir plusieurs tranches en cours d’exécution sur hello même calcul.</span><span class="sxs-lookup"><span data-stu-id="aef3d-388">If hello maximum tasks per compute node is set too> 1, you can also have more than one slice running on hello same compute.</span></span>

![Azure Data Factory - Tâches de travaux Batch](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

<span data-ttu-id="aef3d-390">Hello suivant schéma illustre les relations de hello entre les tâches Azure Data Factory et de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="aef3d-390">hello following diagram illustrates hello relationship between Azure Data Factory and Batch tasks.</span></span>

![Data Factory et Batch](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a><span data-ttu-id="aef3d-392">Résoudre les défaillances</span><span class="sxs-lookup"><span data-stu-id="aef3d-392">Troubleshoot failures</span></span>
<span data-ttu-id="aef3d-393">Quelques techniques de base peuvent être utilisées pour résoudre les défaillances :</span><span class="sxs-lookup"><span data-stu-id="aef3d-393">Troubleshooting consists of a few basic techniques:</span></span>

1. <span data-ttu-id="aef3d-394">Si vous voyez hello l’erreur suivante, vous utilisez peut-être un stockage d’objets blob à chaud/utile au lieu d’utiliser un stockage d’objets blob Azure à usage général.</span><span class="sxs-lookup"><span data-stu-id="aef3d-394">If you see hello following error, you may be using a Hot/Cool blob storage instead of using a general-purpose Azure blob storage.</span></span> <span data-ttu-id="aef3d-395">Télécharger hello zip fichier tooa **compte de stockage Azure à usage général**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-395">Upload hello zip file tooa **general-purpose Azure Storage Account**.</span></span> 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of hello specified Azure Blob(s).
    ``` 
2. <span data-ttu-id="aef3d-396">Si vous voyez hello l’erreur suivante, confirmez ce nom hello de classe hello hello CS nom de fichier correspond à hello vous avez spécifié pour hello **EntryPoint** propriété dans le code JSON de pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-396">If you see hello following error, confirm that hello name of hello class in hello CS file matches hello name you specified for hello **EntryPoint** property in hello pipeline JSON.</span></span> <span data-ttu-id="aef3d-397">Procédure pas à pas de hello, nom de classe hello est : MyDotNetActivity et hello EntryPoint Bonjour JSON est : MyDotNetActivityNS. **MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-397">In hello walkthrough, name of hello class is: MyDotNetActivity, and hello EntryPoint in hello JSON is: MyDotNetActivityNS.**MyDotNetActivity**.</span></span>

    ```
    MyDotNetActivity assembly does not exist or doesn't implement hello type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   <span data-ttu-id="aef3d-398">Si les noms de hello ne correspondent pas, vérifiez que tous les fichiers binaires de hello sont Bonjour **dossier racine** du fichier zip de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-398">If hello names do match, confirm that all hello binaries are in hello **root folder** of hello zip file.</span></span> <span data-ttu-id="aef3d-399">Autrement dit, lorsque vous ouvrez le fichier zip de hello, vous devez voir tous les fichiers hello dans le dossier racine de hello, et non dans les sous-dossiers.</span><span class="sxs-lookup"><span data-stu-id="aef3d-399">That is, when you open hello zip file, you should see all hello files in hello root folder, not in any sub folders.</span></span>   
3. <span data-ttu-id="aef3d-400">Si la tranche de hello d’entrée n’est pas défini trop**prêt**, vérifiez que la structure de dossiers d’entrée de hello est correcte et **fichier.txt** existe dans les dossiers d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-400">If hello input slice is not set too**Ready**, confirm that hello input folder structure is correct and **file.txt** exists in hello input folders.</span></span>
3. <span data-ttu-id="aef3d-401">Bonjour **Execute** méthode de votre activité personnalisée, utilisez hello **IActivityLogger** informations toolog objet qui vous permet de résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="aef3d-401">In hello **Execute** method of your custom activity, use hello **IActivityLogger** object toolog information that helps you troubleshoot issues.</span></span> <span data-ttu-id="aef3d-402">messages Hello connecté apparaissent dans les fichiers journaux utilisateur hello (un ou plusieurs fichiers nommés : 0.log de l’utilisateur, utilisateur-1.log, 2.log de l’utilisateur, etc..).</span><span class="sxs-lookup"><span data-stu-id="aef3d-402">hello logged messages show up in hello user log files (one or more files named: user-0.log, user-1.log, user-2.log, etc.).</span></span>

   <span data-ttu-id="aef3d-403">Bonjour **OutputDataset** panneau, cliquez sur Bonjour tranche toosee Bonjour **tranche de données** panneau pour ce secteur.</span><span class="sxs-lookup"><span data-stu-id="aef3d-403">In hello **OutputDataset** blade, click hello slice toosee hello **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="aef3d-404">Les **activités exécutées** pour cette tranche s’affichent.</span><span class="sxs-lookup"><span data-stu-id="aef3d-404">You see **activity runs** for that slice.</span></span> <span data-ttu-id="aef3d-405">Vous devez voir une activité à exécuter pour la tranche de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-405">You should see one activity run for hello slice.</span></span> <span data-ttu-id="aef3d-406">Si vous cliquez sur Exécuter dans la barre de commandes hello, vous pouvez démarrer une autre activité exécutée pour hello même secteur.</span><span class="sxs-lookup"><span data-stu-id="aef3d-406">If you click Run in hello command bar, you can start another activity run for hello same slice.</span></span>

   <span data-ttu-id="aef3d-407">Lorsque vous cliquez sur exécution de l’activité hello, vous voyez hello **détails de l’activité exécuter** panneau avec une liste des fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="aef3d-407">When you click hello activity run, you see hello **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="aef3d-408">Vous consultez les messages enregistrés dans le fichier de user_0.log hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-408">You see logged messages in hello user_0.log file.</span></span> <span data-ttu-id="aef3d-409">Lorsqu’une erreur se produit, vous voyez trois exécutions d’activité, car de nouvelles tentatives hello est définie too3 dans pipeline/activité hello JSON.</span><span class="sxs-lookup"><span data-stu-id="aef3d-409">When an error occurs, you see three activity runs because hello retry count is set too3 in hello pipeline/activity JSON.</span></span> <span data-ttu-id="aef3d-410">Lorsque vous cliquez sur exécution de l’activité hello, vous voyez que vous pouvez consulter les erreurs de hello tootroubleshoot des fichiers journaux hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-410">When you click hello activity run, you see hello log files that you can review tootroubleshoot hello error.</span></span>

   <span data-ttu-id="aef3d-411">Dans la liste hello des fichiers journaux, cliquez sur hello **0.log de l’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-411">In hello list of log files, click hello **user-0.log**.</span></span> <span data-ttu-id="aef3d-412">Dans le panneau droit hello sont des résultats de l’utilisation de hello hello **IActivityLogger.Write** (méthode).</span><span class="sxs-lookup"><span data-stu-id="aef3d-412">In hello right panel are hello results of using hello **IActivityLogger.Write** method.</span></span> <span data-ttu-id="aef3d-413">Si vous ne voyez pas tous les messages, vérifiez si vous avez plusieurs fichiers journaux nommés user_1.log, user_2.log, etc. Sinon, code de hello a peut-être échoué après que hello du dernier message connecté.</span><span class="sxs-lookup"><span data-stu-id="aef3d-413">If you don't see all messages, check if you have more log files named: user_1.log, user_2.log etc. Otherwise, hello code may have failed after hello last logged message.</span></span>

   <span data-ttu-id="aef3d-414">En outre, consultez **system-0.log** pour vérifier les exceptions et messages d’erreur système éventuels.</span><span class="sxs-lookup"><span data-stu-id="aef3d-414">In addition, check **system-0.log** for any system error messages and exceptions.</span></span>
4. <span data-ttu-id="aef3d-415">Inclure hello **PDB** fichiers dans le fichier zip de hello afin que les détails de l’erreur hello ont des informations telles que **pile des appels** lorsqu’une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="aef3d-415">Include hello **PDB** file in hello zip file so that hello error details have information such as **call stack** when an error occurs.</span></span>
5. <span data-ttu-id="aef3d-416">Tous les hello des fichiers dans le fichier zip de hello pour l’activité personnalisée hello doit se trouver au hello **niveau supérieur** avec aucune sous-dossiers.</span><span class="sxs-lookup"><span data-stu-id="aef3d-416">All hello files in hello zip file for hello custom activity must be at hello **top level** with no sub folders.</span></span>
6. <span data-ttu-id="aef3d-417">Vérifiez que hello **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer / MyDotNetActivity.zip), et **packageLinkedService** (doit pointer toohello **à usage général**stockage d’objets blob Azure qui contient le fichier zip de hello) sont définies les valeurs toocorrect.</span><span class="sxs-lookup"><span data-stu-id="aef3d-417">Ensure that hello **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point toohello **general-purpose**Azure blob storage that contains hello zip file) are set toocorrect values.</span></span>
7. <span data-ttu-id="aef3d-418">Si vous avez corrigé une tranche hello tooreprocess erreur et que vous souhaitez, cliquez sur tranche hello Bonjour **OutputDataset** panneau, cliquez sur **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-418">If you fixed an error and want tooreprocess hello slice, right-click hello slice in hello **OutputDataset** blade and click **Run**.</span></span>
8. <span data-ttu-id="aef3d-419">Si vous voyez hello l’erreur suivante, vous utilisez le package de stockage Azure hello de version > 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="aef3d-419">If you see hello following error, you are using hello Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="aef3d-420">Lanceur de service de fabrique de données nécessite la version de hello 4.3 de WindowsAzure.Storage.</span><span class="sxs-lookup"><span data-stu-id="aef3d-420">Data Factory service launcher requires hello 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="aef3d-421">Consultez [isolement de Appdomain](#appdomain-isolation) section pour résoudre ce problème, si vous devez utiliser hello une version ultérieure de l’assembly de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="aef3d-421">See [Appdomain isolation](#appdomain-isolation) section for a work-around if you must use hello later version of Azure Storage assembly.</span></span> 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by hello target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    <span data-ttu-id="aef3d-422">Si vous pouvez utiliser la version de hello 4.3.0 de package Azure Storage, supprimez hello référence tooAzure stockage package existant de version > 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="aef3d-422">If you can use hello 4.3.0 version of Azure Storage package, remove hello existing reference tooAzure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="aef3d-423">Ensuite, exécutez hello de commande suivante à partir de la Console du Gestionnaire de Package NuGet.</span><span class="sxs-lookup"><span data-stu-id="aef3d-423">Then, run hello following command from NuGet Package Manager Console.</span></span> 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    <span data-ttu-id="aef3d-424">Générez le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-424">Build hello project.</span></span> <span data-ttu-id="aef3d-425">Supprimez l’assembly Azure.Storage de version > 4.3.0 à partir du dossier bin\Debug hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-425">Delete Azure.Storage assembly of version > 4.3.0 from hello bin\Debug folder.</span></span> <span data-ttu-id="aef3d-426">Créer un fichier zip avec des fichiers binaires et le fichier PDB hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-426">Create a zip file with binaries and hello PDB file.</span></span> <span data-ttu-id="aef3d-427">Remplacer l’ancien fichier zip de hello par celui-ci dans le conteneur d’objets blob hello (customactivitycontainer).</span><span class="sxs-lookup"><span data-stu-id="aef3d-427">Replace hello old zip file with this one in hello blob container (customactivitycontainer).</span></span> <span data-ttu-id="aef3d-428">Hello de réexécuter tranches ayant échoué (tranche d’avec le bouton droit et cliquez sur Exécuter).</span><span class="sxs-lookup"><span data-stu-id="aef3d-428">Rerun hello slices that failed (right-click slice, and click Run).</span></span>   
8. <span data-ttu-id="aef3d-429">activité personnalisée Hello n’utilise pas hello **app.config** fichier à partir de votre package.</span><span class="sxs-lookup"><span data-stu-id="aef3d-429">hello custom activity does not use hello **app.config** file from your package.</span></span> <span data-ttu-id="aef3d-430">Par conséquent, si votre code lit les chaînes de connexion à partir du fichier de configuration hello, il ne fonctionne pas lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="aef3d-430">Therefore, if your code reads any connection strings from hello configuration file, it does not work at runtime.</span></span> <span data-ttu-id="aef3d-431">Hello meilleures pratiques lors de l’utilisation d’Azure Batch est toohold les clés secrètes dans un **Azure KeyVault**, utilisez un Bonjour tooprotect principal de service basé sur le certificat **keyvault**et distribuer des certificats de hello tooAzure pool de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="aef3d-431">hello best practice when using Azure Batch is toohold any secrets in an **Azure KeyVault**, use a certificate-based service principal tooprotect hello **keyvault**, and distribute hello certificate tooAzure Batch pool.</span></span> <span data-ttu-id="aef3d-432">Hello les activités personnalisées .NET puis peuvent accéder aux clés secrètes hello KeyVault lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="aef3d-432">hello .NET custom activity then can access secrets from hello KeyVault at runtime.</span></span> <span data-ttu-id="aef3d-433">Cette solution est une solution générique et peut évoluer type tooany du secret, pas seulement les chaînes de connexion.</span><span class="sxs-lookup"><span data-stu-id="aef3d-433">This solution is a generic solution and can scale tooany type of secret, not just connection string.</span></span>

   <span data-ttu-id="aef3d-434">Il existe une solution plus facile (mais pas une meilleure pratique) : vous pouvez créer un **service lié Azure SQL** avec les paramètres de chaîne de connexion, créez un dataset qu’utilise hello service lié et le jeu de données chaîne hello comme un jeu de données d’entrée factice activité de .NET personnalisée toohello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-434">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses hello linked service, and chain hello dataset as a dummy input dataset toohello custom .NET activity.</span></span> <span data-ttu-id="aef3d-435">Vous pouvez ensuite hello d’accès liées la chaîne de connexion du service dans le code d’activité personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-435">You can then access hello linked service's connection string in hello custom activity code.</span></span>  

## <a name="update-custom-activity"></a><span data-ttu-id="aef3d-436">Mettre à jour l’activité personnalisée</span><span class="sxs-lookup"><span data-stu-id="aef3d-436">Update custom activity</span></span>
<span data-ttu-id="aef3d-437">Si vous mettez à jour le code hello pour une activité personnalisée hello, générer et télécharger le fichier compressé hello qui contient le nouveau stockage d’objets blob binaires toohello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-437">If you update hello code for hello custom activity, build it, and upload hello zip file that contains new binaries toohello blob storage.</span></span>

## <a name="appdomain-isolation"></a><span data-ttu-id="aef3d-438">Isolation du domaine d’application</span><span class="sxs-lookup"><span data-stu-id="aef3d-438">Appdomain isolation</span></span>
<span data-ttu-id="aef3d-439">Consultez [exemple de AppDomain Cross](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) qui vous montre comment toocreate une activité personnalisée qui n’est pas contraint versions tooassembly utilisées hello Data Factory (exemple : WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc..).</span><span class="sxs-lookup"><span data-stu-id="aef3d-439">See [Cross AppDomain Sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) that shows you how toocreate a custom activity that is not constrained tooassembly versions used by hello Data Factory launcher (example: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.).</span></span>

## <a name="access-extended-properties"></a><span data-ttu-id="aef3d-440">Accéder aux propriétés étendues</span><span class="sxs-lookup"><span data-stu-id="aef3d-440">Access extended properties</span></span>
<span data-ttu-id="aef3d-441">Vous pouvez déclarer des propriétés étendues dans l’activité hello JSON comme indiqué dans hello suivant l’exemple :</span><span class="sxs-lookup"><span data-stu-id="aef3d-441">You can declare extended properties in hello activity JSON as shown in hello following sample:</span></span>

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


<span data-ttu-id="aef3d-442">Dans l’exemple de hello, il existe deux propriétés étendues : **SliceStart** et **DataFactoryName**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-442">In hello example, there are two extended properties: **SliceStart** and **DataFactoryName**.</span></span> <span data-ttu-id="aef3d-443">valeur de Hello pour SliceStart est basée sur la variable de système SliceStart hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-443">hello value for SliceStart is based on hello SliceStart system variable.</span></span> <span data-ttu-id="aef3d-444">Consultez [Variables système](data-factory-functions-variables.md) pour obtenir la liste des variables système prises en charge.</span><span class="sxs-lookup"><span data-stu-id="aef3d-444">See [System Variables](data-factory-functions-variables.md) for a list of supported system variables.</span></span> <span data-ttu-id="aef3d-445">valeur Hello DataFactoryName est codé en dur les tooCustomActivityFactory.</span><span class="sxs-lookup"><span data-stu-id="aef3d-445">hello value for DataFactoryName is hard-coded tooCustomActivityFactory.</span></span>

<span data-ttu-id="aef3d-446">tooaccess ces les propriétés étendues à hello **Execute** méthode toohello similaires du code utilisation suivante du code :</span><span class="sxs-lookup"><span data-stu-id="aef3d-446">tooaccess these extended properties in hello **Execute** method, use code similar toohello following code:</span></span>

```csharp
// tooget extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// toolog all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a><span data-ttu-id="aef3d-447">Mise à l’échelle automatique d’Azure Batch</span><span class="sxs-lookup"><span data-stu-id="aef3d-447">Auto-scaling of Azure Batch</span></span>
<span data-ttu-id="aef3d-448">Vous pouvez aussi créer un pool Azure Batch avec la fonctionnalité **autoscale** .</span><span class="sxs-lookup"><span data-stu-id="aef3d-448">You can also create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="aef3d-449">Par exemple, vous pouvez créer un pool de traitement par lots azure avec des machines virtuelles de dédié 0 et une formule de mise à l’échelle en fonction du nombre de hello de tâches en attente.</span><span class="sxs-lookup"><span data-stu-id="aef3d-449">For example, you could create an azure batch pool with 0 dedicated VMs and an autoscale formula based on hello number of pending tasks.</span></span> 

<span data-ttu-id="aef3d-450">Hello exemple de formule ici atteint hello suivant comportement : lorsque hello pool est initialement créé, il commence par 1 machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="aef3d-450">hello sample formula here achieves hello following behavior: When hello pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="aef3d-451">$PendingTasks mesure définit le nombre hello de tâches en cours d’exécution + active (en file d’attente) état.</span><span class="sxs-lookup"><span data-stu-id="aef3d-451">$PendingTasks metric defines hello number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="aef3d-452">formule de Hello recherche hello moyenne d’attente de tâches Bonjour 180 dernières secondes et définit les élément TargetDedicated en conséquence.</span><span class="sxs-lookup"><span data-stu-id="aef3d-452">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="aef3d-453">Elle garantit que TargetDedicated ne va jamais au-delà de 25 machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="aef3d-453">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="aef3d-454">Par conséquent, comme les nouvelles tâches sont envoyés, pool croît automatiquement en tant que tâches se terminent, machines virtuelles deviennent libre un par un et hello échelle réduit ces machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="aef3d-454">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and hello autoscaling shrinks those VMs.</span></span> <span data-ttu-id="aef3d-455">startingNumberOfVMs et maxNumberofVMs peut être ajustée tooyour besoins.</span><span class="sxs-lookup"><span data-stu-id="aef3d-455">startingNumberOfVMs and maxNumberofVMs can be adjusted tooyour needs.</span></span>

<span data-ttu-id="aef3d-456">Formule de mise à l’échelle automatique :</span><span class="sxs-lookup"><span data-stu-id="aef3d-456">Autoscale formula:</span></span>

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

<span data-ttu-id="aef3d-457">Pour plus d’informations, consultez [Mettre automatiquement à l’échelle les nœuds de calcul dans un pool Azure Batch](../batch/batch-automatic-scaling.md) .</span><span class="sxs-lookup"><span data-stu-id="aef3d-457">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

<span data-ttu-id="aef3d-458">Si le pool de hello utilise par défaut de hello [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello service Batch peut prendre 15 à 30 minutes tooprepare hello machine virtuelle avant d’exécuter l’activité personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-458">If hello pool is using hello default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch service could take 15-30 minutes tooprepare hello VM before running hello custom activity.</span></span>  <span data-ttu-id="aef3d-459">Si le pool de hello utilise un autre autoScaleEvaluationInterval, hello service Batch peut prendre autoScaleEvaluationInterval + 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="aef3d-459">If hello pool is using a different autoScaleEvaluationInterval, hello Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>

## <a name="use-hdinsight-compute-service"></a><span data-ttu-id="aef3d-460">Utiliser le service de calcul HDInsight</span><span class="sxs-lookup"><span data-stu-id="aef3d-460">Use HDInsight compute service</span></span>
<span data-ttu-id="aef3d-461">Hello procédure pas à pas, vous avez utilisé des activités personnalisées de traitement par lots Azure compute toorun hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-461">In hello walkthrough, you used Azure Batch compute toorun hello custom activity.</span></span> <span data-ttu-id="aef3d-462">Vous pouvez également utiliser votre propre cluster HDInsight de basés sur Windows ou avez Data Factory créer une cluster HDInsight de basés sur Windows sur demande et activité personnalisée hello s’exécutent sur le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-462">You can also use your own Windows-based HDInsight cluster or have Data Factory create an on-demand Windows-based HDInsight cluster and have hello custom activity run on hello HDInsight cluster.</span></span> <span data-ttu-id="aef3d-463">Voici les étapes principales hello à l’aide d’un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aef3d-463">Here are hello high-level steps for using an HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aef3d-464">activités de .NET personnalisées Hello s’exécutent uniquement sur des clusters HDInsight de basés sur Windows.</span><span class="sxs-lookup"><span data-stu-id="aef3d-464">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="aef3d-465">Une solution de contournement pour cette limitation est toouse hello carte réduire toorun personnalisé Java code d’activité sur un cluster HDInsight de basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="aef3d-465">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="aef3d-466">Une autre option consiste à toouse un pool de traitement par lots Azure d’activités personnalisées de machines virtuelles toorun au lieu d’utiliser un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aef3d-466">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>
 

1. <span data-ttu-id="aef3d-467">Créez un service lié Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aef3d-467">Create an Azure HDInsight linked service.</span></span>   
2. <span data-ttu-id="aef3d-468">Utilisez HDInsight lié service à la place de **AzureBatchLinkedService** Bonjour JSON de pipeline.</span><span class="sxs-lookup"><span data-stu-id="aef3d-468">Use HDInsight linked service in place of **AzureBatchLinkedService** in hello pipeline JSON.</span></span>

<span data-ttu-id="aef3d-469">Si vous souhaitez tootest avec hello procédure pas à pas, modification **Démarrer** et **fin** fois pour le pipeline de hello afin que vous pouvez tester le scénario hello avec hello service Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aef3d-469">If you want tootest it with hello walkthrough, change **start** and **end** times for hello pipeline so that you can test hello scenario with hello Azure HDInsight service.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="aef3d-470">Créer le service lié Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="aef3d-470">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="aef3d-471">Hello service Azure Data Factory prend en charge la création d’un cluster à la demande et données de sortie d’entrée tooproduce tooprocess l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="aef3d-471">hello Azure Data Factory service supports creation of an on-demand cluster and use it tooprocess input tooproduce output data.</span></span> <span data-ttu-id="aef3d-472">Vous pouvez également utiliser votre propre cluster tooperform hello identiques.</span><span class="sxs-lookup"><span data-stu-id="aef3d-472">You can also use your own cluster tooperform hello same.</span></span> <span data-ttu-id="aef3d-473">Lorsque vous utilisez un cluster HDInsight à la demande, un cluster est créé pour chaque tranche.</span><span class="sxs-lookup"><span data-stu-id="aef3d-473">When you use on-demand HDInsight cluster, a cluster gets created for each slice.</span></span> <span data-ttu-id="aef3d-474">Alors que, si vous utilisez votre propre cluster HDInsight, cluster de hello est prêt tooprocess hello immédiatement la tranche.</span><span class="sxs-lookup"><span data-stu-id="aef3d-474">Whereas, if you use your own HDInsight cluster, hello cluster is ready tooprocess hello slice immediately.</span></span> <span data-ttu-id="aef3d-475">Par conséquent, lorsque vous utilisez le cluster de la demande, vous ne pouvez pas voir les données de sortie hello aussi rapidement que lorsque vous utilisez votre propre cluster.</span><span class="sxs-lookup"><span data-stu-id="aef3d-475">Therefore, when you use on-demand cluster, you may not see hello output data as quickly as when you use your own cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="aef3d-476">Lors de l’exécution, une instance d’une activité .NET s’exécute uniquement sur un nœud de travail dans le cluster HDInsight de hello ; Il ne peut pas être mis à l’échelle toorun sur plusieurs nœuds.</span><span class="sxs-lookup"><span data-stu-id="aef3d-476">At runtime, an instance of a .NET activity runs only on one worker node in hello HDInsight cluster; it cannot be scaled toorun on multiple nodes.</span></span> <span data-ttu-id="aef3d-477">Plusieurs instances d’activité .NET peuvent s’exécuter en parallèle sur différents nœuds du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-477">Multiple instances of .NET activity can run in parallel on different nodes of hello HDInsight cluster.</span></span>
>
>

##### <a name="toouse-an-on-demand-hdinsight-cluster"></a><span data-ttu-id="aef3d-478">toouse un cluster de HDInsight à la demande</span><span class="sxs-lookup"><span data-stu-id="aef3d-478">toouse an on-demand HDInsight cluster</span></span>
1. <span data-ttu-id="aef3d-479">Bonjour **portail Azure**, cliquez sur **auteur et à déployer** dans la page d’accueil de Data Factory hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-479">In hello **Azure portal**, click **Author and Deploy** in hello Data Factory home page.</span></span>
2. <span data-ttu-id="aef3d-480">Bonjour éditeur Data Factory, cliquez sur **nouveau calcul** à partir de la commande hello barre et sélectionnez **cluster à la demande HDInsight** à partir du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-480">In hello Data Factory Editor, click **New compute** from hello command bar and select **On-demand HDInsight cluster** from hello menu.</span></span>
3. <span data-ttu-id="aef3d-481">Rendre hello modifications toohello JSON script suivant :</span><span class="sxs-lookup"><span data-stu-id="aef3d-481">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="aef3d-482">Pourquoi **la taille du cluster** propriété, spécifiez la taille hello du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-482">For hello **clusterSize** property, specify hello size of hello HDInsight cluster.</span></span>
   2. <span data-ttu-id="aef3d-483">Pourquoi **timeToLive** propriété, spécifiez la durée pendant laquelle les clients hello peuvent être inactif avant d’être supprimé.</span><span class="sxs-lookup"><span data-stu-id="aef3d-483">For hello **timeToLive** property, specify how long hello customer can be idle before it is deleted.</span></span>
   3. <span data-ttu-id="aef3d-484">Pourquoi **version** propriété, spécifiez la version de HDInsight hello souhaité toouse.</span><span class="sxs-lookup"><span data-stu-id="aef3d-484">For hello **version** property, specify hello HDInsight version you want toouse.</span></span> <span data-ttu-id="aef3d-485">Si vous excluez cette propriété, la version la plus récente hello est utilisée.</span><span class="sxs-lookup"><span data-stu-id="aef3d-485">If you exclude this property, hello latest version is used.</span></span>  
   4. <span data-ttu-id="aef3d-486">Pourquoi **linkedServiceName**, spécifiez **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-486">For hello **linkedServiceName**, specify **AzureStorageLinkedService**.</span></span>

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```

    > [!IMPORTANT]
    > <span data-ttu-id="aef3d-487">activités de .NET personnalisées Hello s’exécutent uniquement sur des clusters HDInsight de basés sur Windows.</span><span class="sxs-lookup"><span data-stu-id="aef3d-487">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="aef3d-488">Une solution de contournement pour cette limitation est toouse hello carte réduire toorun personnalisé Java code d’activité sur un cluster HDInsight de basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="aef3d-488">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="aef3d-489">Une autre option consiste à toouse un pool de traitement par lots Azure d’activités personnalisées de machines virtuelles toorun au lieu d’utiliser un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aef3d-489">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>

4. <span data-ttu-id="aef3d-490">Cliquez sur **déployer** sur toodeploy hello lié service de la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-490">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

##### <a name="toouse-your-own-hdinsight-cluster"></a><span data-ttu-id="aef3d-491">toouse votre propre cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="aef3d-491">toouse your own HDInsight cluster:</span></span>
1. <span data-ttu-id="aef3d-492">Bonjour **portail Azure**, cliquez sur **auteur et à déployer** dans la page d’accueil de Data Factory hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-492">In hello **Azure portal**, click **Author and Deploy** in hello Data Factory home page.</span></span>
2. <span data-ttu-id="aef3d-493">Bonjour **éditeur Data Factory**, cliquez sur **nouveau calcul** à partir de la commande hello barre et sélectionnez **cluster HDInsight** à partir du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-493">In hello **Data Factory Editor**, click **New compute** from hello command bar and select **HDInsight cluster** from hello menu.</span></span>
3. <span data-ttu-id="aef3d-494">Rendre hello modifications toohello JSON script suivant :</span><span class="sxs-lookup"><span data-stu-id="aef3d-494">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="aef3d-495">Pourquoi **clusterUri** propriété, entrez les URL hello pour votre HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aef3d-495">For hello **clusterUri** property, enter hello URL for your HDInsight.</span></span> <span data-ttu-id="aef3d-496">Par exemple : https://<clustername>.azurehdinsight.net/.</span><span class="sxs-lookup"><span data-stu-id="aef3d-496">For example: https://<clustername>.azurehdinsight.net/</span></span>     
   2. <span data-ttu-id="aef3d-497">Pourquoi **nom d’utilisateur** propriété, entrez les nom d’utilisateur hello qui possède le cluster d’accès toohello HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aef3d-497">For hello **UserName** property, enter hello user name who has access toohello HDInsight cluster.</span></span>
   3. <span data-ttu-id="aef3d-498">Pourquoi **mot de passe** propriété, entrez le mot de passe de hello pour l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-498">For hello **Password** property, enter hello password for hello user.</span></span>
   4. <span data-ttu-id="aef3d-499">Pourquoi **LinkedServiceName** propriété, entrez **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="aef3d-499">For hello **LinkedServiceName** property, enter **AzureStorageLinkedService**.</span></span>
4. <span data-ttu-id="aef3d-500">Cliquez sur **déployer** sur toodeploy hello lié service de la barre de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="aef3d-500">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

<span data-ttu-id="aef3d-501">Pour plus d’informations, consultez [Services de calcul liés](data-factory-compute-linked-services.md) .</span><span class="sxs-lookup"><span data-stu-id="aef3d-501">See [Compute linked services](data-factory-compute-linked-services.md) for details.</span></span>

<span data-ttu-id="aef3d-502">Bonjour **JSON de pipeline**, utilisez HDInsight (à la demande ou votre propre) service lié :</span><span class="sxs-lookup"><span data-stu-id="aef3d-502">In hello **pipeline JSON**, use HDInsight (on-demand or your own) linked service:</span></span>

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="create-a-custom-activity-by-using-net-sdk"></a><span data-ttu-id="aef3d-503">Créer une activité personnalisée à l’aide du kit .NET SDK</span><span class="sxs-lookup"><span data-stu-id="aef3d-503">Create a custom activity by using .NET SDK</span></span>
<span data-ttu-id="aef3d-504">Dans la procédure pas à pas hello dans cet article, vous créez une fabrique de données avec un pipeline qui utilise l’activité personnalisée hello à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="aef3d-504">In hello walkthrough in this article, you create a data factory with a pipeline that uses hello custom activity by using hello Azure portal.</span></span> <span data-ttu-id="aef3d-505">Hello suivant de code montre comment toocreate hello fabrique de données à l’aide du SDK .NET à la place.</span><span class="sxs-lookup"><span data-stu-id="aef3d-505">hello following code shows you how toocreate hello data factory by using .NET SDK instead.</span></span> <span data-ttu-id="aef3d-506">Vous trouverez plus d’informations sur l’utilisation du Kit de développement logiciel tooprogrammatically créer des pipelines dans hello [créer un pipeline avec l’activité de copie à l’aide des API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="aef3d-506">You can find more details about using SDK tooprogrammatically create pipelines in hello [create a pipeline with copy activity by using .NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md) article.</span></span> 

```csharp
using System;
using System.Configuration;
using System.Collections.ObjectModel;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.Azure;
using Microsoft.Azure.Management.DataFactories;
using Microsoft.Azure.Management.DataFactories.Models;
using Microsoft.Azure.Management.DataFactories.Common.Models;

using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Collections.Generic;

namespace DataFactoryAPITestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // create data factory management client

            // TODO: replace ADFTutorialResourceGroup with hello name of your resource group.
            string resourceGroupName = "ADFTutorialResourceGroup";

            // TODO: replace APITutorialFactory with a name that is globally unique. For example: APITutorialFactory04212017
            string dataFactoryName = "APITutorialFactory";

            TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
                ConfigurationManager.AppSettings["SubscriptionId"],
                GetAuthorizationHeader().Result);

            Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

            DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);

            Console.WriteLine("Creating a data factory");
            client.DataFactories.CreateOrUpdate(resourceGroupName,
                new DataFactoryCreateOrUpdateParameters()
                {
                    DataFactory = new DataFactory()
                    {
                        Name = dataFactoryName,
                        Location = "westus",
                        Properties = new DataFactoryProperties()
                    }
                }
            );

            // create a linked service for input data store: Azure Storage
            Console.WriteLine("Creating Azure Storage linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureStorageLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: Replace <accountname> and <accountkey> with name and key of your Azure Storage account.
                            new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>")
                        )
                    }
                }
            );

            // create a linked service for output data store: Azure SQL Database
            Console.WriteLine("Creating Azure Batch linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureBatchLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: replace <batchaccountname> and <yourbatchaccountkey> with name and key of your Azure Batch account
                            new AzureBatchLinkedService("<batchaccountname>", "https://westus.batch.azure.com", "<yourbatchaccountkey>", "myazurebatchpool", "AzureStorageLinkedService")
                        )
                    }
                }
            );

            // create input and output datasets
            Console.WriteLine("Creating input and output datasets");
            string Dataset_Source = "InputDataset";
            string Dataset_Destination = "OutputDataset";

            Console.WriteLine("Creating input dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Source,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FolderPath = "adftutorial/customactivityinput/",
                                Format = new TextFormat()
                            },
                            External = true,
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },

                            Policy = new Policy() { }
                        }
                    }
                });

            Console.WriteLine("Creating output dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Destination,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FileName = "{slice}.txt",
                                FolderPath = "adftutorial/customactivityoutput/",
                                PartitionedBy = new List<Partition>()
                                {
                                    new Partition()
                                    {
                                        Name = "slice",
                                        Value = new DateTimePartitionValue()
                                        {
                                            Date = "SliceStart",
                                            Format = "yyyy-MM-dd-HH"
                                        }
                                    }
                                }
                            },
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },
                        }
                    }
                });

            Console.WriteLine("Creating a custom activity pipeline");
            DateTime PipelineActivePeriodStartTime = new DateTime(2017, 3, 9, 0, 0, 0, 0, DateTimeKind.Utc);
            DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
            string PipelineName = "ADFTutorialPipelineCustom";

            client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new PipelineCreateOrUpdateParameters()
                {
                    Pipeline = new Pipeline()
                    {
                        Name = PipelineName,
                        Properties = new PipelineProperties()
                        {
                            Description = "Use custom activity",

                            // Initial value for pipeline's active period. With this, you won't need tooset slice status
                            Start = PipelineActivePeriodStartTime,
                            End = PipelineActivePeriodEndTime,
                            IsPaused = false,

                            Activities = new List<Activity>()
                            {
                                new Activity()
                                {
                                    Name = "MyDotNetActivity",
                                    Inputs = new List<ActivityInput>()
                                    {
                                        new ActivityInput() {
                                            Name = Dataset_Source
                                        }
                                    },
                                    Outputs = new List<ActivityOutput>()
                                    {
                                        new ActivityOutput()
                                        {
                                            Name = Dataset_Destination
                                        }
                                    },
                                    LinkedServiceName = "AzureBatchLinkedService",
                                    TypeProperties = new DotNetActivity()
                                    {
                                        AssemblyName = "MyDotNetActivity.dll",
                                        EntryPoint = "MyDotNetActivityNS.MyDotNetActivity",
                                        PackageLinkedService = "AzureStorageLinkedService",
                                        PackageFile = "customactivitycontainer/MyDotNetActivity.zip",
                                        ExtendedProperties = new Dictionary<string, string>()
                                        {
                                            { "SliceStart", "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"}
                                        }
                                    },
                                    Policy = new ActivityPolicy()
                                    {
                                        Concurrency = 2,
                                        ExecutionPriorityOrder = "OldestFirst",
                                        Retry = 3,
                                        Timeout = new TimeSpan(0,0,30,0),
                                        Delay = new TimeSpan()
                                    }
                                }
                            }
                        }
                    }
                });
        }

        public static async Task<string> GetAuthorizationHeader()
        {
            AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
            ClientCredential credential = new ClientCredential(
                ConfigurationManager.AppSettings["ApplicationId"],
                ConfigurationManager.AppSettings["Password"]);
            AuthenticationResult result = await context.AcquireTokenAsync(
                resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                clientCredential: credential);

            if (result != null)
                return result.AccessToken;

            throw new InvalidOperationException("Failed tooacquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a><span data-ttu-id="aef3d-507">Déboguer une activité personnalisée dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aef3d-507">Debug custom activity in Visual Studio</span></span>
<span data-ttu-id="aef3d-508">Hello [Azure Data Factory - environnement local](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) exemple sur GitHub inclut un outil qui vous permet de toodebug des activités .NET personnalisées dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="aef3d-508">hello [Azure Data Factory - local environment](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) sample on GitHub includes a tool that allows you toodebug custom .NET activities within Visual Studio.</span></span>  


## <a name="sample-custom-activities-on-github"></a><span data-ttu-id="aef3d-509">Exemples d’activités personnalisées sur GitHub</span><span class="sxs-lookup"><span data-stu-id="aef3d-509">Sample custom activities on GitHub</span></span>
| <span data-ttu-id="aef3d-510">Exemple</span><span class="sxs-lookup"><span data-stu-id="aef3d-510">Sample</span></span> | <span data-ttu-id="aef3d-511">Rôle des activités personnalisées</span><span class="sxs-lookup"><span data-stu-id="aef3d-511">What custom activity does</span></span> |
| --- | --- |
| <span data-ttu-id="aef3d-512">[Téléchargeur de données HTTP](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span><span class="sxs-lookup"><span data-stu-id="aef3d-512">[HTTP Data Downloader](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span></span> |<span data-ttu-id="aef3d-513">Télécharge des données à partir d’un point de terminaison HTTP de tooAzure stockage d’objets Blob à l’aide de c# activité personnalisée dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="aef3d-513">Downloads data from an HTTP Endpoint tooAzure Blob Storage using custom C# Activity in Data Factory.</span></span> |
| [<span data-ttu-id="aef3d-514">Exemple d’analyse d’opinions Twitter</span><span class="sxs-lookup"><span data-stu-id="aef3d-514">Twitter Sentiment Analysis sample</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |<span data-ttu-id="aef3d-515">Appelle un modèle Azure ML et effectue l’analyse, la notation, la prédiction, etc. des opinions.</span><span class="sxs-lookup"><span data-stu-id="aef3d-515">Invokes an Azure ML model and do sentiment analysis, scoring, prediction etc.</span></span> |
| <span data-ttu-id="aef3d-516">[Exécuter un script R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span><span class="sxs-lookup"><span data-stu-id="aef3d-516">[Run R Script](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span></span> |<span data-ttu-id="aef3d-517">Appelle un script R en exécutant RScript.exe sur votre cluster HDInsight, sur lequel R est installé.</span><span class="sxs-lookup"><span data-stu-id="aef3d-517">Invokes R script by running RScript.exe on your HDInsight cluster that already has R Installed on it.</span></span> |
| [<span data-ttu-id="aef3d-518">Activité .NET entre AppDomains</span><span class="sxs-lookup"><span data-stu-id="aef3d-518">Cross AppDomain .NET Activity</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |<span data-ttu-id="aef3d-519">Utilise des versions d’assembly différentes de celles utilisées par le service de lancement de Data Factory hello</span><span class="sxs-lookup"><span data-stu-id="aef3d-519">Uses different assembly versions from ones used by hello Data Factory launcher</span></span> |
| [<span data-ttu-id="aef3d-520">Retraiter un modèle dans Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="aef3d-520">Reprocess a model in Azure Analysis Services</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  <span data-ttu-id="aef3d-521">Retraite un modèle dans Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="aef3d-521">Reprocesses a model in Azure Analysis Services.</span></span> |

[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: ./media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: ./media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png
