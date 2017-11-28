---
title: "Utilisation des activités personnalisées dans un pipeline Azure Data Factory"
description: "Découvrez comment créer des activités personnalisées et les utiliser dans un pipeline Azure Data Factory."
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
ms.openlocfilehash: f3d265f31cb653d32076747e586383d67bbccc41
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a><span data-ttu-id="270b0-103">Utilisation des activités personnalisées dans un pipeline Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="270b0-103">Use custom activities in an Azure Data Factory pipeline</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="270b0-104">Activité Hive</span><span class="sxs-lookup"><span data-stu-id="270b0-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="270b0-105">Activité pig</span><span class="sxs-lookup"><span data-stu-id="270b0-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="270b0-106">Activité MapReduce</span><span class="sxs-lookup"><span data-stu-id="270b0-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="270b0-107">Activité de diffusion en continu Hadoop</span><span class="sxs-lookup"><span data-stu-id="270b0-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="270b0-108">Activité Spark</span><span class="sxs-lookup"><span data-stu-id="270b0-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="270b0-109">Activité d’exécution par lot Machine Learning</span><span class="sxs-lookup"><span data-stu-id="270b0-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="270b0-110">Activité des ressources de mise à jour de Machine Learning</span><span class="sxs-lookup"><span data-stu-id="270b0-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="270b0-111">Activité de procédure stockée</span><span class="sxs-lookup"><span data-stu-id="270b0-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="270b0-112">Activité U-SQL Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="270b0-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="270b0-113">Activité personnalisée .NET</span><span class="sxs-lookup"><span data-stu-id="270b0-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="270b0-114">Vous pouvez utiliser deux types d’activités dans un pipeline Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="270b0-114">There are two types of activities that you can use in an Azure Data Factory pipeline.</span></span>

- <span data-ttu-id="270b0-115">Les [activités de déplacement des données](data-factory-data-movement-activities.md) permettent de déplacer des données entre des [magasins de données source et récepteur pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="270b0-115">[Data Movement Activities](data-factory-data-movement-activities.md) to move data between [supported source and sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>
- <span data-ttu-id="270b0-116">Les [activités de transformation des données](data-factory-data-transformation-activities.md) permettent de transformer des données à l’aide de services de calcul comme Azure HDInsight, Azure Batch et Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="270b0-116">[Data Transformation Activities](data-factory-data-transformation-activities.md) to transform data using compute services such as Azure HDInsight, Azure Batch, and Azure Machine Learning.</span></span> 

<span data-ttu-id="270b0-117">Pour déplacer des données vers ou à partir d’un magasin de données qui n’est pas pris en charge par Data Factory, créez une **activité personnalisée** avec votre propre logique de déplacement des données et utilisez cette activité dans un pipeline.</span><span class="sxs-lookup"><span data-stu-id="270b0-117">To move data to/from a data store that Data Factory does not support, create a **custom activity** with your own data movement logic and use the activity in a pipeline.</span></span> <span data-ttu-id="270b0-118">De même, si vous devez transformer et traiter les données d’une manière qui n’est pas prise en charge par Data Factory, créez une activité personnalisée avec votre propre logique de transformation des données et utilisez cette activité dans un pipeline.</span><span class="sxs-lookup"><span data-stu-id="270b0-118">Similarly, to transform/process data in a way that isn't supported by Data Factory, create a custom activity with your own data transformation logic and use the activity in a pipeline.</span></span> 

<span data-ttu-id="270b0-119">Vous pouvez configurer une activité personnalisée de sorte qu’elle s’exécute sur un pool **Azure Batch** de machines virtuelles ou un cluster **Azure HDInsight** basé sur Windows.</span><span class="sxs-lookup"><span data-stu-id="270b0-119">You can configure a custom activity to run on an **Azure Batch** pool of virtual machines or a Windows-based **Azure HDInsight** cluster.</span></span> <span data-ttu-id="270b0-120">Lorsque vous utilisez Azure Batch, vous pouvez utiliser uniquement un pool Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="270b0-120">When using Azure Batch, you can use only an existing Azure Batch pool.</span></span> <span data-ttu-id="270b0-121">À l’inverse, lorsque vous utilisez HDInsight, vous pouvez utiliser un cluster HDInsight existant ou un cluster qui est créé automatiquement pour vous à la demande lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="270b0-121">Whereas, when using HDInsight, you can use an existing HDInsight cluster or a cluster that is automatically created for you on-demand at runtime.</span></span>  

<span data-ttu-id="270b0-122">La procédure suivante fournit des instructions pas à pas pour créer une activité .NET personnalisée et utiliser cette activité personnalisée dans un pipeline.</span><span class="sxs-lookup"><span data-stu-id="270b0-122">The following walkthrough provides step-by-step instructions for creating a custom .NET activity and using the custom activity in a pipeline.</span></span> <span data-ttu-id="270b0-123">La procédure pas à pas utilise un service lié **Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="270b0-123">The walkthrough uses an **Azure Batch** linked service.</span></span> <span data-ttu-id="270b0-124">Pour utiliser un service lié Azure HDInsight à la place, vous créez un service lié de type **HDInsight** (votre propre cluster HDInsight) ou **HDInsightOnDemand** (Data Factory crée un cluster HDInsight à la demande).</span><span class="sxs-lookup"><span data-stu-id="270b0-124">To use an Azure HDInsight linked service instead, you create a linked service of type **HDInsight** (your own HDInsight cluster) or **HDInsightOnDemand** (Data Factory creates an HDInsight cluster on-demand).</span></span> <span data-ttu-id="270b0-125">Ensuite, configurez une activité personnalisée pour utiliser le service lié HDInsight.</span><span class="sxs-lookup"><span data-stu-id="270b0-125">Then, configure custom activity to use the HDInsight linked service.</span></span> <span data-ttu-id="270b0-126">Consultez la section [Utiliser des services liés Azure HDInsight](#use-hdinsight-compute-service) pour plus d’informations sur l’utilisation d’Azure HDInsight pour exécuter l’activité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="270b0-126">See [Use Azure HDInsight linked services](#use-hdinsight-compute-service) section for details on using Azure HDInsight to run the custom activity.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="270b0-127">Les activités .NET personnalisées s’exécutent uniquement sur des clusters HDInsight sous Windows.</span><span class="sxs-lookup"><span data-stu-id="270b0-127">The custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="270b0-128">Un moyen de contourner cette limitation consiste à utiliser l’activité Map Reduce pour exécuter du code Java personnalisé sur un cluster HDInsight sous Linux.</span><span class="sxs-lookup"><span data-stu-id="270b0-128">A workaround for this limitation is to use the Map Reduce Activity to run custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="270b0-129">Une autre option consiste à utiliser un pool Azure Batch de machines virtuelles pour exécuter des activités personnalisées au lieu d’utiliser un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="270b0-129">Another option is to use an Azure Batch pool of VMs to run custom activities instead of using a HDInsight cluster.</span></span>
> - <span data-ttu-id="270b0-130">Il n’est pas possible d’utiliser une passerelle de gestion des données à partir d’une activité personnalisée pour accéder à des sources de données locales.</span><span class="sxs-lookup"><span data-stu-id="270b0-130">It is not possible to use a Data Management Gateway from a custom activity to access on-premises data sources.</span></span> <span data-ttu-id="270b0-131">Actuellement, la [passerelle de gestion des données](data-factory-data-management-gateway.md) prend en charge uniquement l’activité de copie et l’activité de procédure stockée dans Data Factory.</span><span class="sxs-lookup"><span data-stu-id="270b0-131">Currently, [Data Management Gateway](data-factory-data-management-gateway.md) supports only the copy activity and stored procedure activity in Data Factory.</span></span>   

## <a name="walkthrough-create-a-custom-activity"></a><span data-ttu-id="270b0-132">Procédure pas à pas : création d’une activité personnalisée</span><span class="sxs-lookup"><span data-stu-id="270b0-132">Walkthrough: create a custom activity</span></span>
### <a name="prerequisites"></a><span data-ttu-id="270b0-133">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="270b0-133">Prerequisites</span></span>
* <span data-ttu-id="270b0-134">Visual Studio 2012/2013/2015</span><span class="sxs-lookup"><span data-stu-id="270b0-134">Visual Studio 2012/2013/2015</span></span>
* <span data-ttu-id="270b0-135">Téléchargez et installez le [Kit de développement logiciel (SDK) Azure .NET](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="270b0-135">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span></span>

### <a name="azure-batch-prerequisites"></a><span data-ttu-id="270b0-136">Configuration requise pour Azure Batch</span><span class="sxs-lookup"><span data-stu-id="270b0-136">Azure Batch prerequisites</span></span>
<span data-ttu-id="270b0-137">Dans la procédure pas à pas, vous allez exécuter vos activités .NET personnalisées à l’aide de la ressource de calcul Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="270b0-137">In the walkthrough, you run your custom .NET activities using Azure Batch as a compute resource.</span></span> <span data-ttu-id="270b0-138">**Azure Batch** est une plateforme qui permet d’exécuter efficacement des applications de calcul haute performance (HPC) en parallèle et à grande échelle dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="270b0-138">**Azure Batch** is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="270b0-139">Azure Batch planifie les travaux nécessitant une grande quantité de ressources système à exécuter sur une **collection gérée de machines virtuelles**. Il peut mettre automatiquement à l’échelle les ressources de calcul pour répondre aux besoins de vos travaux.</span><span class="sxs-lookup"><span data-stu-id="270b0-139">Azure Batch schedules compute-intensive work to run on a managed **collection of virtual machines**, and can automatically scale compute resources to meet the needs of your jobs.</span></span> <span data-ttu-id="270b0-140">Consultez l’article [Notions de base d’Azure Batch][batch-technical-overview] pour une présentation détaillée du service Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="270b0-140">See [Azure Batch basics][batch-technical-overview] article for a detailed overview of the Azure Batch service.</span></span>

<span data-ttu-id="270b0-141">Pour ce didacticiel, créez un compte Azure Batch avec un pool de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="270b0-141">For the tutorial, create an Azure Batch account with a pool of VMs.</span></span> <span data-ttu-id="270b0-142">Voici la procédure à suivre :</span><span class="sxs-lookup"><span data-stu-id="270b0-142">Here are the steps:</span></span>

1. <span data-ttu-id="270b0-143">Créez un compte **Azure Batch** via le [portail Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="270b0-143">Create an **Azure Batch account** using the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="270b0-144">Consultez l’article [Créer et gérer un compte Azure Batch][batch-create-account] pour obtenir des instructions.</span><span class="sxs-lookup"><span data-stu-id="270b0-144">See [Create and manage an Azure Batch account][batch-create-account] article for instructions.</span></span>
2. <span data-ttu-id="270b0-145">Notez le nom du pool, l’URI, la clé et le nom du compte Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="270b0-145">Note down the Azure Batch account name, account key, URI, and pool name.</span></span> <span data-ttu-id="270b0-146">Vous en avez besoin pour créer un service lié Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="270b0-146">You need them to create an Azure Batch linked service.</span></span>
    1. <span data-ttu-id="270b0-147">Sur la page d’accueil du compte Azure Batch, vous voyez une **URL** au format suivant : `https://myaccount.westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="270b0-147">On the home page for Azure Batch account, you see a **URL** in the following format: `https://myaccount.westus.batch.azure.com`.</span></span> <span data-ttu-id="270b0-148">Dans cet exemple, **myaccount** est le nom du compte Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="270b0-148">In this example, **myaccount** is the name of the Azure Batch account.</span></span> <span data-ttu-id="270b0-149">L’URI que vous utilisez dans la définition de service lié est l’URL sans le nom du compte.</span><span class="sxs-lookup"><span data-stu-id="270b0-149">URI you use in the linked service definition is the URL without the name of the account.</span></span> <span data-ttu-id="270b0-150">Par exemple : `https://<region>.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="270b0-150">For example: `https://<region>.batch.azure.com`.</span></span>
    2. <span data-ttu-id="270b0-151">Cliquez sur **Clés** dans le menu de gauche et copiez la **CLÉ D’ACCÈS PRIMAIRE**.</span><span class="sxs-lookup"><span data-stu-id="270b0-151">Click **Keys** on the left menu, and copy the **PRIMARY ACCESS KEY**.</span></span>
    3. <span data-ttu-id="270b0-152">Pour utiliser un pool existant, cliquez sur **Pools** dans le menu, puis notez **l’ID** du pool.</span><span class="sxs-lookup"><span data-stu-id="270b0-152">To use an existing pool, click **Pools** on the menu, and note down the **ID** of the pool.</span></span> <span data-ttu-id="270b0-153">Si vous n’avez pas de pool existant, passez à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="270b0-153">If you don't have an existing pool, move to the next step.</span></span>     
2. <span data-ttu-id="270b0-154">Créez un **pool Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="270b0-154">Create an **Azure Batch pool**.</span></span>

   1. <span data-ttu-id="270b0-155">Dans le [portail Azure](https://portal.azure.com), cliquez sur **Parcourir** dans le menu de gauche, puis cliquez sur **Comptes Batch**.</span><span class="sxs-lookup"><span data-stu-id="270b0-155">In the [Azure portal](https://portal.azure.com), click **Browse** in the left menu, and click **Batch Accounts**.</span></span>
   2. <span data-ttu-id="270b0-156">Sélectionnez votre compte Azure Batch pour ouvrir le panneau **Compte Batch** .</span><span class="sxs-lookup"><span data-stu-id="270b0-156">Select your Azure Batch account to open the **Batch Account** blade.</span></span>
   3. <span data-ttu-id="270b0-157">Cliquez sur la vignette **Pools** .</span><span class="sxs-lookup"><span data-stu-id="270b0-157">Click **Pools** tile.</span></span>
   4. <span data-ttu-id="270b0-158">Dans le panneau **Pools** , cliquez sur le bouton Ajouter de la barre d’outils pour ajouter un pool.</span><span class="sxs-lookup"><span data-stu-id="270b0-158">In the **Pools** blade, click Add button on the toolbar to add a pool.</span></span>
      1. <span data-ttu-id="270b0-159">Entrez un ID pour le pool (ID du pool).</span><span class="sxs-lookup"><span data-stu-id="270b0-159">Enter an ID for the pool (Pool ID).</span></span> <span data-ttu-id="270b0-160">Notez **l’ID du pool**, car vous en aurez besoin lors de la création de la solution Data Factory.</span><span class="sxs-lookup"><span data-stu-id="270b0-160">Note the **ID of the pool**; you need it when creating the Data Factory solution.</span></span>
      2. <span data-ttu-id="270b0-161">Spécifiez **Windows Server 2012 R2** pour le paramètre de famille du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="270b0-161">Specify **Windows Server 2012 R2** for the Operating System Family setting.</span></span>
      3. <span data-ttu-id="270b0-162">Sélectionnez le **niveau tarifaire du nœud**.</span><span class="sxs-lookup"><span data-stu-id="270b0-162">Select a **node pricing tier**.</span></span>
      4. <span data-ttu-id="270b0-163">Entrez **2** comme valeur du paramètre **Quantité dédiée cible**.</span><span class="sxs-lookup"><span data-stu-id="270b0-163">Enter **2** as value for the **Target Dedicated** setting.</span></span>
      5. <span data-ttu-id="270b0-164">Entrez **2** comme valeur du paramètre **Nombre maximal de tâches par nœud**.</span><span class="sxs-lookup"><span data-stu-id="270b0-164">Enter **2** as value for the **Max tasks per node** setting.</span></span>
   5. <span data-ttu-id="270b0-165">Cliquez sur **OK** pour créer le pool.</span><span class="sxs-lookup"><span data-stu-id="270b0-165">Click **OK** to create the pool.</span></span>
   6. <span data-ttu-id="270b0-166">Notez **l’ID** du pool.</span><span class="sxs-lookup"><span data-stu-id="270b0-166">Note down the **ID** of the pool.</span></span> 



### <a name="high-level-steps"></a><span data-ttu-id="270b0-167">Procédure générale</span><span class="sxs-lookup"><span data-stu-id="270b0-167">High-level steps</span></span>
<span data-ttu-id="270b0-168">Voici les deux étapes principales que vous effectuez dans le cadre de cette procédure pas à pas :</span><span class="sxs-lookup"><span data-stu-id="270b0-168">Here are the two high-level steps you perform as part of this walkthrough:</span></span> 

1. <span data-ttu-id="270b0-169">Créer une activité personnalisée qui contient une logique simple de transformation/traitement des données.</span><span class="sxs-lookup"><span data-stu-id="270b0-169">Create a custom activity that contains simple data transformation/processing logic.</span></span>
2. <span data-ttu-id="270b0-170">Créer une fabrique de données Azure avec un pipeline qui utilise l’activité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="270b0-170">Create an Azure data factory with a pipeline that uses the custom activity.</span></span>

### <a name="create-a-custom-activity"></a><span data-ttu-id="270b0-171">création d'une activité personnalisée</span><span class="sxs-lookup"><span data-stu-id="270b0-171">Create a custom activity</span></span>
<span data-ttu-id="270b0-172">Pour créer une activité .NET personnalisée, créez un projet de **bibliothèque de classes .NET** contenant une classe qui implémente l’interface **IDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="270b0-172">To create a .NET custom activity, create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="270b0-173">Cette interface possède une seule méthode, [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) , avec la signature suivante :</span><span class="sxs-lookup"><span data-stu-id="270b0-173">This interface has only one method: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) and its signature is:</span></span>

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


<span data-ttu-id="270b0-174">La méthode accepte quatre paramètres :</span><span class="sxs-lookup"><span data-stu-id="270b0-174">The method takes four parameters:</span></span>

- <span data-ttu-id="270b0-175">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="270b0-175">**linkedServices**.</span></span> <span data-ttu-id="270b0-176">Cette propriété est une liste énumérable de services liés Data Store référencés par les jeux de données d’entrée/sortie de l’activité.</span><span class="sxs-lookup"><span data-stu-id="270b0-176">This property is an enumerable list of Data Store linked services referenced by input/output datasets for the activity.</span></span>   
- <span data-ttu-id="270b0-177">**jeux de données**.</span><span class="sxs-lookup"><span data-stu-id="270b0-177">**datasets**.</span></span> <span data-ttu-id="270b0-178">Cette propriété est une liste énumérable de jeux de données d’entrée/sortie de l’activité.</span><span class="sxs-lookup"><span data-stu-id="270b0-178">This property is an enumerable list of input/output datasets for the activity.</span></span> <span data-ttu-id="270b0-179">Vous pouvez utiliser ce paramètre pour obtenir les emplacements et les schémas définis par les jeux de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="270b0-179">You can use this parameter to get the locations and schemas defined by input and output datasets.</span></span>
- <span data-ttu-id="270b0-180">**activity**.</span><span class="sxs-lookup"><span data-stu-id="270b0-180">**activity**.</span></span> <span data-ttu-id="270b0-181">Cette propriété représente l’activité actuelle.</span><span class="sxs-lookup"><span data-stu-id="270b0-181">This property represents the current activity.</span></span> <span data-ttu-id="270b0-182">Elle peut être utilisée pour accéder aux propriétés étendues associées à l’activité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="270b0-182">It can be used to access extended properties associated with the custom activity.</span></span> <span data-ttu-id="270b0-183">Consultez la section [Accéder aux propriétés étendues](#access-extended-properties) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="270b0-183">See [Access extended properties](#access-extended-properties) for details.</span></span>
- <span data-ttu-id="270b0-184">**logger**.</span><span class="sxs-lookup"><span data-stu-id="270b0-184">**logger**.</span></span> <span data-ttu-id="270b0-185">Cet objet vous permet d’écrire des commentaires de débogage qui apparaîtront dans le journal utilisateur pour le pipeline.</span><span class="sxs-lookup"><span data-stu-id="270b0-185">This object lets you write debug comments that surface in the user log for the pipeline.</span></span>

<span data-ttu-id="270b0-186">La méthode retourne un dictionnaire qui peut être utilisé pour enchaîner ultérieurement des activités personnalisées.</span><span class="sxs-lookup"><span data-stu-id="270b0-186">The method returns a dictionary that can be used to chain custom activities together in the future.</span></span> <span data-ttu-id="270b0-187">Cette fonctionnalité n’étant pas encore implémentée, seul un dictionnaire vide est retourné par la méthode.</span><span class="sxs-lookup"><span data-stu-id="270b0-187">This feature is not implemented yet, so return an empty dictionary from the method.</span></span>  

### <a name="procedure"></a><span data-ttu-id="270b0-188">Procédure</span><span class="sxs-lookup"><span data-stu-id="270b0-188">Procedure</span></span>
1. <span data-ttu-id="270b0-189">Créez un projet de **bibliothèque de classes .NET** .</span><span class="sxs-lookup"><span data-stu-id="270b0-189">Create a **.NET Class Library** project.</span></span>
   <ol type="a">
     <li><span data-ttu-id="270b0-190">Lancez <b>Visual Studio 2017</b> ou <b>Visual Studio 2015</b> ou <b>Visual Studio 2013</b> ou <b>Visual Studio 2012</b>.</span><span class="sxs-lookup"><span data-stu-id="270b0-190">Launch <b>Visual Studio 2017</b> or <b>Visual Studio 2015</b> or <b>Visual Studio 2013</b> or <b>Visual Studio 2012</b>.</span></span></li>
     <li><span data-ttu-id="270b0-191">Cliquez sur <b>Fichier</b>, pointez le curseur de la souris sur <b>Nouveau</b>, puis cliquez sur <b>Projet</b>.</span><span class="sxs-lookup"><span data-stu-id="270b0-191">Click <b>File</b>, point to <b>New</b>, and click <b>Project</b>.</span></span></li>
     <li><span data-ttu-id="270b0-192">Développez <b>Modèles</b>, puis sélectionnez <b>Visual C#</b>.</span><span class="sxs-lookup"><span data-stu-id="270b0-192">Expand <b>Templates</b>, and select <b>Visual C#</b>.</span></span> <span data-ttu-id="270b0-193">Dans cette procédure pas à pas, vous utilisez C#, mais vous pouvez utiliser un autre langage .NET pour développer l’activité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="270b0-193">In this walkthrough, you use C#, but you can use any .NET language to develop the custom activity.</span></span></li>
     <li><span data-ttu-id="270b0-194">Sélectionnez <b>Bibliothèque de classes</b> dans la liste des types de projet, sur la droite.</span><span class="sxs-lookup"><span data-stu-id="270b0-194">Select <b>Class Library</b> from the list of project types on the right.</span></span> <span data-ttu-id="270b0-195">Dans VS 2017, choisissez <b>Bibliothèque de classes (.NET Framework)</b> .</span><span class="sxs-lookup"><span data-stu-id="270b0-195">In VS 2017, choose <b>Class Library (.NET Framework)</b> </span></span></li>
     <li><span data-ttu-id="270b0-196">Entrez <b>MyDotNetActivity</b> pour le <b>nom</b>.</span><span class="sxs-lookup"><span data-stu-id="270b0-196">Enter <b>MyDotNetActivity</b> for the <b>Name</b>.</span></span></li>
     <li><span data-ttu-id="270b0-197">Sélectionnez <b>C:\ADFGetStarted</b> comme <b>Emplacement</b>.</span><span class="sxs-lookup"><span data-stu-id="270b0-197">Select <b>C:\ADFGetStarted</b> for the <b>Location</b>.</span></span></li>
     <li><span data-ttu-id="270b0-198">Cliquez sur <b>OK</b> pour créer le projet.</span><span class="sxs-lookup"><span data-stu-id="270b0-198">Click <b>OK</b> to create the project.</span></span></li>
   </ol><span data-ttu-id="270b0-199">
2. Cliquez sur **Outils**, pointez le curseur de la souris sur **Gestionnaire de package NuGet**, puis cliquez sur **Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="270b0-199">
2. Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
<span data-ttu-id="270b0-200">3.</span><span class="sxs-lookup"><span data-stu-id="270b0-200">3.</span></span> <span data-ttu-id="270b0-201">Dans la Console du gestionnaire de package, exécutez la commande suivante pour importer l’élément **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="270b0-201">In the Package Manager Console, execute the following command to import **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="270b0-202">Importez le package NuGet **Azure Storage** dans le projet.</span><span class="sxs-lookup"><span data-stu-id="270b0-202">Import the **Azure Storage** NuGet package in to the project.</span></span>

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="270b0-203">Le lanceur du service Data Factory requiert la version 4.3 du package Windows Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="270b0-203">Data Factory service launcher requires the 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="270b0-204">Si vous ajoutez une référence à une version ultérieure de l’assembly Azure Storage à votre projet d’activité personnalisée, vous obtenez une erreur lors de l’exécution de l’activité.</span><span class="sxs-lookup"><span data-stu-id="270b0-204">If you add a reference to a later version of Azure Storage assembly in your custom activity project, you see an error when the activity executes.</span></span> <span data-ttu-id="270b0-205">Pour résoudre l’erreur, consultez la section [Isolation du domaine d’application](#appdomain-isolation).</span><span class="sxs-lookup"><span data-stu-id="270b0-205">To resolve the error, see [Appdomain isolation](#appdomain-isolation) section.</span></span> 
5. <span data-ttu-id="270b0-206">Ajoutez les instructions **using** ci-après dans le fichier source du projet.</span><span class="sxs-lookup"><span data-stu-id="270b0-206">Add the following **using** statements to the source file in the project.</span></span>

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
6. <span data-ttu-id="270b0-207">Remplacez le nom de **l’espace de noms** par **MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="270b0-207">Change the name of the **namespace** to **MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="270b0-208">Remplacez le nom de la classe par **MyDotNetActivity** et dérivez-le de l’interface **IDotNetActivity**, comme indiqué dans l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="270b0-208">Change the name of the class to **MyDotNetActivity** and derive it from the **IDotNetActivity** interface as shown in the following code snippet:</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="270b0-209">Implémentez (ajoutez) la méthode **Execute** de l’interface **IDotNetActivity** dans la classe **MyDotNetActivity** et copiez l’exemple de code suivant dans la méthode.</span><span class="sxs-lookup"><span data-stu-id="270b0-209">Implement (Add) the **Execute** method of the **IDotNetActivity** interface to the **MyDotNetActivity** class and copy the following sample code to the method.</span></span>

    <span data-ttu-id="270b0-210">L’exemple suivant compte le nombre d’occurrences du terme recherché (Microsoft) dans chaque objet blob associé à une tranche de données.</span><span class="sxs-lookup"><span data-stu-id="270b0-210">The following sample counts the number of occurrences of the search term (“Microsoft”) in each blob associated with a data slice.</span></span>

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
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // to log information, use the logger object
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

        // get the input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables to hold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from the dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and the other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get the first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using the same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get the connection string in the linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get the folder path from the input dataset definition
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
               // with the data slice. definition of the method is shown in the next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get the output dataset using the name of the dataset matched to a name in the Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for the output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get the folder path from the output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log the output folder path   
        logger.Write("Writing blob to the folder: {0}", folderPath);
    
        // create a storage object for the output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write the name of the file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log the output file name
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
9. <span data-ttu-id="270b0-211">Ajoutez les méthodes d’assistance suivantes :</span><span class="sxs-lookup"><span data-stu-id="270b0-211">Add the following helper methods:</span></span> 

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

        // get type properties of the dataset   
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return the folder path found in the type properties
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
    
        // get type properties of the dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return the blob/file name in the type properties
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

    <span data-ttu-id="270b0-212">La méthode GetFolderPath renvoie le chemin d’accès au dossier vers lequel pointe le jeu de données et la méthode GetFileName renvoie le nom de l’objet blob/fichier vers lequel pointe le jeu de données.</span><span class="sxs-lookup"><span data-stu-id="270b0-212">The GetFolderPath method returns the path to the folder that the dataset points to and the GetFileName method returns the name of the blob/file that the dataset points to.</span></span> <span data-ttu-id="270b0-213">Si folderPath est défini avec des variables telles que {Year}, {Month}, {Day}, etc., la méthode retourne la chaîne en l’état, sans remplacer les variables par les valeurs d’exécution.</span><span class="sxs-lookup"><span data-stu-id="270b0-213">If you havefolderPath defines using variables such as {Year}, {Month}, {Day} etc., the method returns the string as it is without replacing them with runtime values.</span></span> <span data-ttu-id="270b0-214">Consultez la section [Accéder aux propriétés étendues](#access-extended-properties) pour plus d’informations sur l’accès à SliceStart, SliceEnd, etc.</span><span class="sxs-lookup"><span data-stu-id="270b0-214">See [Access extended properties](#access-extended-properties) section for details on accessing SliceStart, SliceEnd, etc.</span></span>    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    <span data-ttu-id="270b0-215">La méthode Calculate calcule le nombre d’instances du mot-clé Microsoft dans les fichiers d’entrée (objets blob du dossier).</span><span class="sxs-lookup"><span data-stu-id="270b0-215">The Calculate method calculates the number of instances of keyword Microsoft in the input files (blobs in the folder).</span></span> <span data-ttu-id="270b0-216">Le terme de recherche (« Microsoft ») est codé en dur dans le code.</span><span class="sxs-lookup"><span data-stu-id="270b0-216">The search term (“Microsoft”) is hard-coded in the code.</span></span>
10. <span data-ttu-id="270b0-217">Compilez le projet.</span><span class="sxs-lookup"><span data-stu-id="270b0-217">Compile the project.</span></span> <span data-ttu-id="270b0-218">Cliquez sur l’option **Générer** du menu, puis sur **Générer la solution**.</span><span class="sxs-lookup"><span data-stu-id="270b0-218">Click **Build** from the menu and click **Build Solution**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="270b0-219">Définissez la version 4.5.2 de .NET Framework comme infrastructure cible pour votre projet : cliquez avec le bouton droit sur le projet et cliquez sur **Propriétés** pour définir l’infrastructure cible.</span><span class="sxs-lookup"><span data-stu-id="270b0-219">Set 4.5.2 version of .NET Framework as the target framework for your project: right-click the project, and click **Properties** to set the target framework.</span></span> <span data-ttu-id="270b0-220">Data Factory ne prend pas en charge les activités personnalisées compilées avec les versions de .NET Framework ultérieures à la version 4.5.2.</span><span class="sxs-lookup"><span data-stu-id="270b0-220">Data Factory does not support custom activities compiled against .NET Framework versions later than 4.5.2.</span></span>

11. <span data-ttu-id="270b0-221">Lancez **l’Explorateur Windows** et accédez au dossier **bin\debug** ou **bin\release** (selon le type de build).</span><span class="sxs-lookup"><span data-stu-id="270b0-221">Launch **Windows Explorer**, and navigate to **bin\debug** or **bin\release** folder depending on the type of build.</span></span>
12. <span data-ttu-id="270b0-222">Créez un fichier zip **MyDotNetActivity.zip** contenant tous les fichiers binaires dans le dossier <project folder>\bin\Debug.</span><span class="sxs-lookup"><span data-stu-id="270b0-222">Create a zip file **MyDotNetActivity.zip** that contains all the binaries in the <project folder>\bin\Debug folder.</span></span> <span data-ttu-id="270b0-223">Incluez le fichier **MyDotNetActivity.pdb** afin d’obtenir des détails supplémentaires tels que le numéro de ligne du code source à l’origine du problème en cas de défaillance.</span><span class="sxs-lookup"><span data-stu-id="270b0-223">Include the **MyDotNetActivity.pdb** file so that you get additional details such as line number in the source code that caused the issue if there was a failure.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="270b0-224">Tous les fichiers contenus dans le fichier zip de l’activité personnalisée doivent se trouver au **premier niveau** et ne doivent pas contenir de sous-dossiers.</span><span class="sxs-lookup"><span data-stu-id="270b0-224">All the files in the zip file for the custom activity must be at the **top level** with no sub folders.</span></span>

    ![Fichiers de sortie binaires](./media/data-factory-use-custom-activities/Binaries.png)
14. <span data-ttu-id="270b0-226">Si nécessaire, créez un conteneur de blobs nommé **customactivitycontainer**.</span><span class="sxs-lookup"><span data-stu-id="270b0-226">Create a blob container named **customactivitycontainer** if it does not already exist.</span></span> 
15. <span data-ttu-id="270b0-227">Chargez MyDotNetActivity.zip en tant qu’objet blob dans le customactivitycontainer dans un compte Stockage Blob Azure **à usage général** (pas un Stockage Blob chaud/froid) référencé par AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="270b0-227">Upload MyDotNetActivity.zip as a blob to the customactivitycontainer in a **general-purpose** Azure blob storage (not hot/cool Blob storage) that is referred by AzureStorageLinkedService.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="270b0-228">Si vous ajoutez ce projet d’activité .NET à une solution dans Visual Studio qui contient un projet Data Factory, et que vous ajoutez une référence au projet d’activité .NET à partir du projet d’application Data Factory, vous n’avez pas besoin d’effectuer les deux dernières étapes pour créer manuellement le fichier zip et le télécharger dans le stockage Blob Azure à usage général.</span><span class="sxs-lookup"><span data-stu-id="270b0-228">If you add this .NET activity project to a solution in Visual Studio that contains a Data Factory project, and add a reference to .NET activity project from the Data Factory application project, you do not need to perform the last two steps of manually creating the zip file and uploading it to the general-purpose Azure blob storage.</span></span> <span data-ttu-id="270b0-229">Lorsque vous publiez des entités Data Factory à l'aide de Visual Studio, ces étapes sont effectuées automatiquement par le processus de publication.</span><span class="sxs-lookup"><span data-stu-id="270b0-229">When you publish Data Factory entities using Visual Studio, these steps are automatically done by the publishing process.</span></span> <span data-ttu-id="270b0-230">Pour plus d’informations, consultez la section [Projet Data Factory dans Visual Studio](#data-factory-project-in-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="270b0-230">For more information, see [Data Factory project in Visual Studio](#data-factory-project-in-visual-studio) section.</span></span>

## <a name="create-a-pipeline-with-custom-activity"></a><span data-ttu-id="270b0-231">Créer un pipeline avec une activité personnalisée</span><span class="sxs-lookup"><span data-stu-id="270b0-231">Create a pipeline with custom activity</span></span>
<span data-ttu-id="270b0-232">Vous avez créé une activité personnalisée et chargé le fichier zip avec des fichiers binaires dans un conteneur de blobs dans un compte de stockage Azure **à usage général**.</span><span class="sxs-lookup"><span data-stu-id="270b0-232">You have created a custom activity and uploaded the zip file with binaries to a blob container in a **general-purpose** Azure Storage Account.</span></span> <span data-ttu-id="270b0-233">Dans cette section, vous allez créer une fabrique de données Azure avec un pipeline qui utilise l’activité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="270b0-233">In this section, you create an Azure data factory with a pipeline that uses the custom activity.</span></span>

<span data-ttu-id="270b0-234">Le jeu de données d’entrée de l’activité personnalisée représente les blobs (fichiers) contenus dans le dossier customactivityinput du conteneur adftutorial dans le stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="270b0-234">The input dataset for the custom activity represents blobs (files) in the customactivityinput folder of adftutorial container in the blob storage.</span></span> <span data-ttu-id="270b0-235">Le jeu de données de sortie de l’activité représente les blobs de sortie contenus dans le dossier customactivityoutput du conteneur adftutorial dans le stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="270b0-235">The output dataset for the activity represents output blobs in the customactivityoutput folder of adftutorial container in the blob storage.</span></span>

<span data-ttu-id="270b0-236">Créez le fichier **file.txt** avec le contenu suivant, puis chargez-le dans le dossier **customactivityinput** du conteneur **adftutorial**.</span><span class="sxs-lookup"><span data-stu-id="270b0-236">Create **file.txt** file with the following content and upload it to **customactivityinput** folder of the **adftutorial** container.</span></span> <span data-ttu-id="270b0-237">S’il n’existe pas déjà, créez le conteneur adftutorial.</span><span class="sxs-lookup"><span data-stu-id="270b0-237">Create the adftutorial container if it does not exist already.</span></span> 

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="270b0-238">Le dossier d’entrée correspond à une tranche dans Azure Data Factory, même si le dossier contient au moins deux fichiers.</span><span class="sxs-lookup"><span data-stu-id="270b0-238">The input folder corresponds to a slice in Azure Data Factory even if the folder has two or more files.</span></span> <span data-ttu-id="270b0-239">Lorsque chaque tranche est traitée par le pipeline, l’activité personnalisée effectue une itération dans tous les objets blob du dossier d’entrée pour la tranche en question.</span><span class="sxs-lookup"><span data-stu-id="270b0-239">When each slice is processed by the pipeline, the custom activity iterates through all the blobs in the input folder for that slice.</span></span>

<span data-ttu-id="270b0-240">Un fichier de sortie à une ou plusieurs lignes (le même nombre de lignes que le nombre de blobs contenus dans le dossier d’entrée) apparaîtra dans le dossier adftutorial\customactivityoutput :</span><span class="sxs-lookup"><span data-stu-id="270b0-240">You see one output file with in the adftutorial\customactivityoutput folder with one or more lines (same as number of blobs in the input folder):</span></span>

```
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2016-11-16-00/file.txt.
```


<span data-ttu-id="270b0-241">Voici les étapes que vous effectuez dans cette section :</span><span class="sxs-lookup"><span data-stu-id="270b0-241">Here are the steps you perform in this section:</span></span>

1. <span data-ttu-id="270b0-242">Création d'une **fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="270b0-242">Create a **data factory**.</span></span>
2. <span data-ttu-id="270b0-243">Créez des **services liés** pour le pool Azure Batch de machines virtuelles sur lesquelles l’activité personnalisée doit être exécutée et le stockage Azure qui contient les blobs d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="270b0-243">Create **Linked services** for the Azure Batch pool of VMs on which the custom activity runs and the Azure Storage that holds the input/output blobs.</span></span>
3. <span data-ttu-id="270b0-244">Créez des **jeux de données** d’entrée et de sortie qui représentent les entrées/sorties de l’activité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="270b0-244">Create input and output **datasets** that represent input and output of the custom activity.</span></span>
4. <span data-ttu-id="270b0-245">Créez un **pipeline** qui utilise l’activité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="270b0-245">Create a **pipeline** that uses the custom activity.</span></span>

> [!NOTE]
> <span data-ttu-id="270b0-246">Créez le fichier **file.txt** et chargez-le dans un conteneur d’objets blob, si vous ne l’avez pas déjà fait.</span><span class="sxs-lookup"><span data-stu-id="270b0-246">Create the **file.txt** and upload it to a blob container if you haven't already done so.</span></span> <span data-ttu-id="270b0-247">Consultez les instructions fournies dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="270b0-247">See instructions in the preceding section.</span></span>   

### <a name="step-1-create-the-data-factory"></a><span data-ttu-id="270b0-248">Étape 1 : Créer la fabrique de données</span><span class="sxs-lookup"><span data-stu-id="270b0-248">Step 1: Create the data factory</span></span>
1. <span data-ttu-id="270b0-249">Une fois connecté au portail Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="270b0-249">After logging in to the Azure portal, do the following steps:</span></span>
   1. <span data-ttu-id="270b0-250">Cliquez sur **NOUVEAU** dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="270b0-250">Click **NEW** on the left menu.</span></span>
   2. <span data-ttu-id="270b0-251">Dans le panneau **Nouveau**, cliquez sur **Données et analyses**.</span><span class="sxs-lookup"><span data-stu-id="270b0-251">Click **Data + Analytics** in the **New** blade.</span></span>
   3. <span data-ttu-id="270b0-252">Cliquez sur **Data Factory** dans le panneau **Analyse des données**.</span><span class="sxs-lookup"><span data-stu-id="270b0-252">Click **Data Factory** on the **Data analytics** blade.</span></span>
   
    ![Nouveau menu Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. <span data-ttu-id="270b0-254">Dans le panneau **Nouvelle fabrique de données**, spécifiez le nom **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="270b0-254">In the **New data factory** blade, enter **CustomActivityFactory** for the Name.</span></span> <span data-ttu-id="270b0-255">Le nom de la fabrique de données Azure doit être un nom global unique.</span><span class="sxs-lookup"><span data-stu-id="270b0-255">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="270b0-256">Si l’erreur **Data factory name “CustomActivityFactory” is not available** (Le nom de la fabrique de données « CustomActivityFactory » n’est pas disponible) s’affiche, changez le nom de la fabrique de données (par exemple, **votrenomCustomActivityFactory**), puis tentez de la recréer.</span><span class="sxs-lookup"><span data-stu-id="270b0-256">If you receive the error: **Data factory name “CustomActivityFactory” is not available**, change the name of the data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>

    ![Nouveau panneau Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. <span data-ttu-id="270b0-258">Cliquez sur **NOM DU GROUPE DE RESSOURCES**pour sélectionner un groupe de ressources existant, ou créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="270b0-258">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="270b0-259">Veillez à utiliser **l’abonnement** et la **région** correspondant à ceux dans lesquels vous voulez créer la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="270b0-259">Verify that you are using the correct **subscription** and **region** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="270b0-260">Cliquez sur **Créer** dans le panneau **Nouvelle fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="270b0-260">Click **Create** on the **New data factory** blade.</span></span>
6. <span data-ttu-id="270b0-261">La fabrique de données apparaît comme étant en cours de création dans le **Tableau de bord** du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="270b0-261">You see the data factory being created in the **Dashboard** of the Azure portal.</span></span>
7. <span data-ttu-id="270b0-262">Une fois la fabrique de données créée, son contenu apparaîtra dans le panneau correspondant indiquant.</span><span class="sxs-lookup"><span data-stu-id="270b0-262">After the data factory has been created successfully, you see the Data Factory blade, which shows you the contents of the data factory.</span></span>
    
    ![Panneau Data Factory](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a><span data-ttu-id="270b0-264">Étape 2 : Créer des services liés</span><span class="sxs-lookup"><span data-stu-id="270b0-264">Step 2: Create linked services</span></span>
<span data-ttu-id="270b0-265">Les services liés se chargent de lier des magasins de données ou des services de calcul à une fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="270b0-265">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="270b0-266">Dans cette étape, vous allez lier vos comptes Stockage Azure et Azure Batch à votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="270b0-266">In this step, you link your Azure Storage account and Azure Batch account to your data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="270b0-267">Créer le service lié Stockage Azure</span><span class="sxs-lookup"><span data-stu-id="270b0-267">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="270b0-268">Cliquez sur la vignette **Créer et déployer** dans le panneau **DATA FACTORY** de **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="270b0-268">Click the **Author and deploy** tile on the **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="270b0-269">Data Factory Editor s’affiche.</span><span class="sxs-lookup"><span data-stu-id="270b0-269">You see the Data Factory Editor.</span></span>
2. <span data-ttu-id="270b0-270">Cliquez sur **Nouvelle banque de données** dans la barre de commandes et choisissez **Stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="270b0-270">Click **New data store** on the command bar and choose **Azure storage**.</span></span> <span data-ttu-id="270b0-271">Le script JSON de création d’un service lié Stockage Microsoft Azure doit apparaître dans l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="270b0-271">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>
    
    ![Nouveau magasin de données - Stockage Azure](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. <span data-ttu-id="270b0-273">Remplacez `<accountname>` par le nom de votre compte de stockage Azure et `<accountkey>` par la clé d’accès du compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="270b0-273">Replace `<accountname>` with name of your Azure storage account and `<accountkey>` with access key of the Azure storage account.</span></span> <span data-ttu-id="270b0-274">Pour savoir comment obtenir votre clé d’accès de stockage, voir [Affichage, copie et régénération de clés d’accès de stockage](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="270b0-274">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

    ![Service lié Stockage Azure](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. <span data-ttu-id="270b0-276">Cliquez sur l’option **Déployer** de la barre de commandes pour déployer le service lié.</span><span class="sxs-lookup"><span data-stu-id="270b0-276">Click **Deploy** on the command bar to deploy the linked service.</span></span>

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="270b0-277">Créer un service lié Azure Batch</span><span class="sxs-lookup"><span data-stu-id="270b0-277">Create Azure Batch linked service</span></span>
1. <span data-ttu-id="270b0-278">Dans Data Factory Editor, dans la barre d’outils, cliquez sur **... Plus** dans la barre de commandes, cliquez sur **Nouveau calcul**, puis sélectionnez **Azure Batch** dans le menu.</span><span class="sxs-lookup"><span data-stu-id="270b0-278">In the Data Factory Editor, click **... More** on the command bar, click **New compute**, and then select **Azure Batch** from the menu.</span></span>

    ![Nouveau calcul - Azure Batch](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. <span data-ttu-id="270b0-280">Apportez les modifications suivantes au script JSON :</span><span class="sxs-lookup"><span data-stu-id="270b0-280">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="270b0-281">Spécifiez le nom du compte Azure Batch pour la propriété **accountName** .</span><span class="sxs-lookup"><span data-stu-id="270b0-281">Specify Azure Batch account name for the **accountName** property.</span></span> <span data-ttu-id="270b0-282">L’**URL** dans le **panneau du compte Azure Batch** est au format suivant : `http://accountname.region.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="270b0-282">The **URL** from the **Azure Batch account blade** is in the following format: `http://accountname.region.batch.azure.com`.</span></span> <span data-ttu-id="270b0-283">Pour la propriété **batchUri** dans le JSON, vous devez supprimer `accountname.` de l’URL et utiliser `accountname` pour la propriété JSON `accountName`.</span><span class="sxs-lookup"><span data-stu-id="270b0-283">For the **batchUri** property in the JSON, you need to remove `accountname.` from the URL and use the `accountname` for the `accountName` JSON property.</span></span>
   2. <span data-ttu-id="270b0-284">Spécifiez la clé du compte Azure Batch pour la propriété **accessKey** .</span><span class="sxs-lookup"><span data-stu-id="270b0-284">Specify the Azure Batch account key for the **accessKey** property.</span></span>
   3. <span data-ttu-id="270b0-285">Spécifiez le nom du pool que vous avez créé dans le cadre de la configuration requise pour la propriété **poolName** .</span><span class="sxs-lookup"><span data-stu-id="270b0-285">Specify the name of the pool you created as part of prerequisites for the **poolName** property.</span></span> <span data-ttu-id="270b0-286">Vous pouvez aussi spécifier l’ID du pool au lieu du nom du pool.</span><span class="sxs-lookup"><span data-stu-id="270b0-286">You can also specify the ID of the pool instead of the name of the pool.</span></span>
   4. <span data-ttu-id="270b0-287">Spécifiez l’URI Azure Batch pour la propriété **batchUri** .</span><span class="sxs-lookup"><span data-stu-id="270b0-287">Specify Azure Batch URI for the **batchUri** property.</span></span> <span data-ttu-id="270b0-288">Exemple : `https://westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="270b0-288">Example: `https://westus.batch.azure.com`.</span></span>  
   5. <span data-ttu-id="270b0-289">Spécifiez **AzureStorageLinkedService** for the **linkedServiceName** .</span><span class="sxs-lookup"><span data-stu-id="270b0-289">Specify the **AzureStorageLinkedService** for the **linkedServiceName** property.</span></span>

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

       <span data-ttu-id="270b0-290">Pour la propriété **poolName** , vous pouvez également spécifier l’ID du pool au lieu du nom du pool.</span><span class="sxs-lookup"><span data-stu-id="270b0-290">For the **poolName** property, you can also specify the ID of the pool instead of the name of the pool.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="270b0-291">Le service Data Factory ne prend pas en charge l’option à la demande pour Azure Batch contrairement à HDInsight.</span><span class="sxs-lookup"><span data-stu-id="270b0-291">The Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="270b0-292">Vous pouvez uniquement utiliser votre propre pool Azure Batch dans une fabrique de données Azure.</span><span class="sxs-lookup"><span data-stu-id="270b0-292">You can only use your own Azure Batch pool in an Azure data factory.</span></span>   
    

### <a name="step-3-create-datasets"></a><span data-ttu-id="270b0-293">Étape 3 : Créer les jeux de données</span><span class="sxs-lookup"><span data-stu-id="270b0-293">Step 3: Create datasets</span></span>
<span data-ttu-id="270b0-294">Dans cette étape, vous allez créer des jeux de données pour représenter les données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="270b0-294">In this step, you create datasets to represent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="270b0-295">Créer le jeu de données d’entrée</span><span class="sxs-lookup"><span data-stu-id="270b0-295">Create input dataset</span></span>
1. <span data-ttu-id="270b0-296">Dans **l’éditeur** de la fabrique de données, cliquez sur **... Plus** dans la barre de commandes, cliquez sur **Nouveau jeu de données**, puis sélectionnez **Stockage Blob Azure** dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="270b0-296">In the **Editor** for the Data Factory, click **... More** on the command bar, click **New dataset**, and then select **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="270b0-297">Remplacez le script JSON affiché dans le volet droit par l’extrait de code JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="270b0-297">Replace the JSON in the right pane with the following JSON snippet:</span></span>

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

   <span data-ttu-id="270b0-298">Plus loin dans cette procédure pas à pas, vous allez créer un pipeline associé à l’heure de début 2016-11-16T00:00:00Z et à l’heure de fin 2016-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="270b0-298">You create a pipeline later in this walkthrough with start time: 2016-11-16T00:00:00Z and end time: 2016-11-16T05:00:00Z.</span></span> <span data-ttu-id="270b0-299">Ce pipeline est planifié pour produire des données toutes les heures, ce qui signifie que l’on obtient cinq tranches d’entrée/sortie comprises entre **00**:00:00 -> **05**:00:00.</span><span class="sxs-lookup"><span data-stu-id="270b0-299">It is scheduled to produce data hourly, so there are five input/output slices (between **00**:00:00 -> **05**:00:00).</span></span>

   <span data-ttu-id="270b0-300">Les paramètres **frequency** et **interval** du jeu de données d’entrée sont respectivement définis sur **Hour** et sur **1**, ce qui signifie que la tranche d’entrée est disponible toutes les heures.</span><span class="sxs-lookup"><span data-stu-id="270b0-300">The **frequency** and **interval** for the input dataset is set to **Hour** and **1**, which means that the input slice is available hourly.</span></span> <span data-ttu-id="270b0-301">Dans cet exemple, il s’agit du même fichier (file.txt) que celui contenu dans le dossier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="270b0-301">In this sample, it is the same file (file.txt) in the intputfolder.</span></span>

   <span data-ttu-id="270b0-302">Voici les heures de début de chaque tranche, chacune étant représentée par la variable système SliceStart dans l’extrait de code JSON ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="270b0-302">Here are the start times for each slice, which is represented by SliceStart system variable in the above JSON snippet.</span></span>
3. <span data-ttu-id="270b0-303">Cliquez sur **Déployer** sur la barre d’outils pour créer et déployer le **jeu de données d’entrée**.</span><span class="sxs-lookup"><span data-stu-id="270b0-303">Click **Deploy** on the toolbar to create and deploy the **InputDataset**.</span></span> <span data-ttu-id="270b0-304">Vérifiez que le message **TABLE CORRECTEMENT CRÉÉE** s’affiche dans la barre de titre de l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="270b0-304">Confirm that you see the **TABLE CREATED SUCCESSFULLY** message on the title bar of the Editor.</span></span>

#### <a name="create-an-output-dataset"></a><span data-ttu-id="270b0-305">Créer un jeu de données de sortie</span><span class="sxs-lookup"><span data-stu-id="270b0-305">Create an output dataset</span></span>
1. <span data-ttu-id="270b0-306">Dans **Data Factory Editor**, cliquez sur **... Plus** dans la barre de commandes, cliquez sur **Nouveau jeu de données**, puis sélectionnez **Stockage Blob Azure**.</span><span class="sxs-lookup"><span data-stu-id="270b0-306">In the **Data Factory editor**, click **... More** on the command bar, click **New dataset**, and then select **Azure Blob storage**.</span></span>
2. <span data-ttu-id="270b0-307">Remplacez le script JSON affiché dans le volet droit par le script JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="270b0-307">Replace the JSON script in the right pane with the following JSON script:</span></span>

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

     <span data-ttu-id="270b0-308">L’emplacement de sortie est le suivant : **adftutorial/customactivityoutput/** et le nom du fichier de sortie est aaaa-MM-dd-HH.txt, où « aaaa-MM-dd-HH.txt » correspond à l’année, au mois, au jour et à l’heure de la tranche produite.</span><span class="sxs-lookup"><span data-stu-id="270b0-308">Output location is **adftutorial/customactivityoutput/** and output file name is yyyy-MM-dd-HH.txt where yyyy-MM-dd-HH is the year, month, date, and hour of the slice being produced.</span></span> <span data-ttu-id="270b0-309">Pour en savoir plus, consultez la page [Référence du développeur][adf-developer-reference].</span><span class="sxs-lookup"><span data-stu-id="270b0-309">See [Developer Reference][adf-developer-reference] for details.</span></span>

    <span data-ttu-id="270b0-310">Un objet blob/fichier de sortie est généré pour chaque tranche d’entrée.</span><span class="sxs-lookup"><span data-stu-id="270b0-310">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="270b0-311">Voici la procédure de nommage des fichiers de sortie pour chaque tranche.</span><span class="sxs-lookup"><span data-stu-id="270b0-311">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="270b0-312">Tous les fichiers de sortie sont générés dans un seul dossier de sortie : **adftutorial\customactivityoutput**.</span><span class="sxs-lookup"><span data-stu-id="270b0-312">All the output files are generated in one output folder: **adftutorial\customactivityoutput**.</span></span>

   | <span data-ttu-id="270b0-313">Tranche</span><span class="sxs-lookup"><span data-stu-id="270b0-313">Slice</span></span> | <span data-ttu-id="270b0-314">Heure de début</span><span class="sxs-lookup"><span data-stu-id="270b0-314">Start time</span></span> | <span data-ttu-id="270b0-315">Fichier de sortie</span><span class="sxs-lookup"><span data-stu-id="270b0-315">Output file</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="270b0-316">1</span><span class="sxs-lookup"><span data-stu-id="270b0-316">1</span></span> |<span data-ttu-id="270b0-317">2016-11-16T00:00:00</span><span class="sxs-lookup"><span data-stu-id="270b0-317">2016-11-16T00:00:00</span></span> |<span data-ttu-id="270b0-318">2016-11-16-00.txt</span><span class="sxs-lookup"><span data-stu-id="270b0-318">2016-11-16-00.txt</span></span> |
   | <span data-ttu-id="270b0-319">2</span><span class="sxs-lookup"><span data-stu-id="270b0-319">2</span></span> |<span data-ttu-id="270b0-320">2016-11-16T01:00:00</span><span class="sxs-lookup"><span data-stu-id="270b0-320">2016-11-16T01:00:00</span></span> |<span data-ttu-id="270b0-321">2016-11-16-01.txt</span><span class="sxs-lookup"><span data-stu-id="270b0-321">2016-11-16-01.txt</span></span> |
   | <span data-ttu-id="270b0-322">3</span><span class="sxs-lookup"><span data-stu-id="270b0-322">3</span></span> |<span data-ttu-id="270b0-323">2016-11-16T02:00:00</span><span class="sxs-lookup"><span data-stu-id="270b0-323">2016-11-16T02:00:00</span></span> |<span data-ttu-id="270b0-324">2016-11-16-02.txt</span><span class="sxs-lookup"><span data-stu-id="270b0-324">2016-11-16-02.txt</span></span> |
   | <span data-ttu-id="270b0-325">4</span><span class="sxs-lookup"><span data-stu-id="270b0-325">4</span></span> |<span data-ttu-id="270b0-326">2016-11-16T03:00:00</span><span class="sxs-lookup"><span data-stu-id="270b0-326">2016-11-16T03:00:00</span></span> |<span data-ttu-id="270b0-327">2016-11-16-03.txt</span><span class="sxs-lookup"><span data-stu-id="270b0-327">2016-11-16-03.txt</span></span> |
   | <span data-ttu-id="270b0-328">5</span><span class="sxs-lookup"><span data-stu-id="270b0-328">5</span></span> |<span data-ttu-id="270b0-329">2016-11-16T04:00:00</span><span class="sxs-lookup"><span data-stu-id="270b0-329">2016-11-16T04:00:00</span></span> |<span data-ttu-id="270b0-330">2016-11-16-04.txt</span><span class="sxs-lookup"><span data-stu-id="270b0-330">2016-11-16-04.txt</span></span> |

    <span data-ttu-id="270b0-331">N’oubliez pas que tous les fichiers d’un dossier d’entrée font partie d’une tranche associée aux heures de début indiquées ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="270b0-331">Remember that all the files in an input folder are part of a slice with the start times mentioned above.</span></span> <span data-ttu-id="270b0-332">Lorsque cette tranche est traitée, l’activité personnalisée parcourt chaque fichier et génère une ligne dans le fichier de sortie avec le nombre d’occurrences du terme de recherche (« Microsoft »).</span><span class="sxs-lookup"><span data-stu-id="270b0-332">When this slice is processed, the custom activity scans through each file and produces a line in the output file with the number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="270b0-333">Si le dossier d’entrée comporte trois fichiers, trois lignes apparaissent dans le fichier de sortie pour chaque tranche horaire : 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.</span><span class="sxs-lookup"><span data-stu-id="270b0-333">If there are three files in the inputfolder, there are three lines in the output file for each hourly slice: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.</span></span>
3. <span data-ttu-id="270b0-334">Cliquez sur **Déployer** dans la barre de commandes pour déployer le **jeu de données de sortie**.</span><span class="sxs-lookup"><span data-stu-id="270b0-334">To deploy the **OutputDataset**, click **Deploy** on the command bar.</span></span>

### <a name="create-and-run-a-pipeline-that-uses-the-custom-activity"></a><span data-ttu-id="270b0-335">Créer et exécuter un pipeline qui utilise l’activité personnalisée</span><span class="sxs-lookup"><span data-stu-id="270b0-335">Create and run a pipeline that uses the custom activity</span></span>
1. <span data-ttu-id="270b0-336">Dans Data Factory Editor, dans la barre d’outils, cliquez sur **... Plus**, puis sélectionnez **Nouveau pipeline** dans la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="270b0-336">In the Data Factory Editor, click **... More**, and then select **New pipeline** on the command bar.</span></span> 
2. <span data-ttu-id="270b0-337">Remplacez le script JSON affiché dans le volet droit par le script JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="270b0-337">Replace the JSON in the right pane with the following JSON script:</span></span>

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

    <span data-ttu-id="270b0-338">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="270b0-338">Note the following points:</span></span>

   * <span data-ttu-id="270b0-339">**Concurrency** est défini sur **2** pour que les deux tranches soient traitées en parallèle sur 2 machines virtuelles dans le pool Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="270b0-339">**Concurrency** is set to **2** so that two slices are processed in parallel by 2 VMs in the Azure Batch pool.</span></span>
   * <span data-ttu-id="270b0-340">Il existe une activité dans la section des activités ; elle présente le type suivant : **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="270b0-340">There is one activity in the activities section and it is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="270b0-341">Le paramètre **AssemblyName** est défini sur le nom de la DLL **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="270b0-341">**AssemblyName** is set to the name of the DLL: **MyDotnetActivity.dll**.</span></span>
   * <span data-ttu-id="270b0-342">Le paramètre **EntryPoint** est défini sur **MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="270b0-342">**EntryPoint** is set to **MyDotNetActivityNS.MyDotNetActivity**.</span></span>
   * <span data-ttu-id="270b0-343">**PackageLinkedService** est défini sur **AzureStorageLinkedService**, qui pointe vers le stockage d’objets blob contenant le fichier .zip de l’activité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="270b0-343">**PackageLinkedService** is set to **AzureStorageLinkedService** that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="270b0-344">Si vous utilisez des comptes de stockage différents pour les fichiers d’entrée/sortie et le fichier zip de l’activité personnalisée, vous créez un autre service lié Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="270b0-344">If you are using different Azure Storage accounts for input/output files and the custom activity zip file, you create another Azure Storage linked service.</span></span> <span data-ttu-id="270b0-345">Cet article suppose que vous utilisez le même compte Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="270b0-345">This article assumes that you are using the same Azure Storage account.</span></span>
   * <span data-ttu-id="270b0-346">Le paramètre **PackageFile** est défini sur **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="270b0-346">**PackageFile** is set to **customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="270b0-347">Il est au format : conteneur_du_zip/nom_du_zip.zip.</span><span class="sxs-lookup"><span data-stu-id="270b0-347">It is in the format: containerforthezip/nameofthezip.zip.</span></span>
   * <span data-ttu-id="270b0-348">L’activité personnalisée utilise **InputDataset** comme entrée et **OutputDataset** comme sortie.</span><span class="sxs-lookup"><span data-stu-id="270b0-348">The custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="270b0-349">La propriété linkedServiceName de l’activité personnalisée pointe vers **AzureBatchLinkedService**, ce qui indique à Azure Data Factory que l’activité personnalisée doit s’exécuter sur des machines virtuelles Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="270b0-349">The linkedServiceName property of the custom activity points to the **AzureBatchLinkedService**, which tells Azure Data Factory that the custom activity needs to run on Azure Batch VMs.</span></span>
   * <span data-ttu-id="270b0-350">La propriété **isPaused** est définie sur **false**.</span><span class="sxs-lookup"><span data-stu-id="270b0-350">**isPaused** property is set to **false** by default.</span></span> <span data-ttu-id="270b0-351">Le pipeline s’exécute immédiatement dans cet exemple car les tranches débutent à une date antérieure.</span><span class="sxs-lookup"><span data-stu-id="270b0-351">The pipeline runs immediately in this example because the slices start in the past.</span></span> <span data-ttu-id="270b0-352">Vous pouvez définir cette propriété sur true pour suspendre le pipeline et lui réaffecter la valeur false pour reprendre l’exécution.</span><span class="sxs-lookup"><span data-stu-id="270b0-352">You can set this property to true to pause the pipeline and set it back to false to restart.</span></span>
   * <span data-ttu-id="270b0-353">**Cinq** heures séparent les heures de **début** et de **fin**, et les tranches sont produites toutes les heures, ce qui signifie que cinq tranches sont produites par le pipeline.</span><span class="sxs-lookup"><span data-stu-id="270b0-353">The **start** time and **end** times are **five** hours apart and slices are produced hourly, so five slices are produced by the pipeline.</span></span>
3. <span data-ttu-id="270b0-354">Cliquez sur **Déployer** dans la barre de commandes pour déployer le pipeline.</span><span class="sxs-lookup"><span data-stu-id="270b0-354">To deploy the pipeline, click **Deploy** on the command bar.</span></span>

### <a name="monitor-the-pipeline"></a><span data-ttu-id="270b0-355">Surveiller le pipeline</span><span class="sxs-lookup"><span data-stu-id="270b0-355">Monitor the pipeline</span></span>
1. <span data-ttu-id="270b0-356">Dans le panneau Data Factory du portail Azure, cliquez sur **Diagramme**.</span><span class="sxs-lookup"><span data-stu-id="270b0-356">In the Data Factory blade in the Azure portal, click **Diagram**.</span></span>

    ![Vignette schématique](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. <span data-ttu-id="270b0-358">Dans la vue de diagramme, cliquez sur OutputDataset.</span><span class="sxs-lookup"><span data-stu-id="270b0-358">In the Diagram View, now click the OutputDataset.</span></span>

    ![Vue schématique](./media/data-factory-use-custom-activities/diagram.png)
3. <span data-ttu-id="270b0-360">Les cinq tranches de sortie doivent être à l’état Prêt.</span><span class="sxs-lookup"><span data-stu-id="270b0-360">You should see that the five output slices are in the Ready state.</span></span> <span data-ttu-id="270b0-361">Dans le cas contraire, cela signifie qu’elles n’ont pas encore été générées.</span><span class="sxs-lookup"><span data-stu-id="270b0-361">If they are not in the Ready state, they haven't been produced yet.</span></span> 

   ![Tranches de sortie](./media/data-factory-use-custom-activities/OutputSlices.png)
4. <span data-ttu-id="270b0-363">Vérifiez que les fichiers de sortie sont générés dans le stockage d’objets blob, dans le conteneur **adftutorial** .</span><span class="sxs-lookup"><span data-stu-id="270b0-363">Verify that the output files are generated in the blob storage in the **adftutorial** container.</span></span>

   ![Sortie de l’activité personnalisée][image-data-factory-ouput-from-custom-activity]
5. <span data-ttu-id="270b0-365">Si vous ouvrez le fichier de sortie, la sortie doit avoir l’aspect suivant :</span><span class="sxs-lookup"><span data-stu-id="270b0-365">If you open the output file, you should see the output similar to the following output:</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2016-11-16-00/file.txt.
    ```
6. <span data-ttu-id="270b0-366">Utilisez le [portail Azure][azure-preview-portal] ou les applets de commande Azure PowerShell pour surveiller votre fabrique de données, pipelines et jeux de données.</span><span class="sxs-lookup"><span data-stu-id="270b0-366">Use the [Azure portal][azure-preview-portal] or Azure PowerShell cmdlets to monitor your data factory, pipelines, and data sets.</span></span> <span data-ttu-id="270b0-367">Vous pouvez voir les messages de l'outil **ActivityLogger** dans le code concernant l'activité personnalisée dans les journaux (plus précisément, user-0.log) que vous pouvez télécharger à partir du portail ou à l'aide d'applets de commande.</span><span class="sxs-lookup"><span data-stu-id="270b0-367">You can see messages from the **ActivityLogger** in the code for the custom activity in the logs (specifically user-0.log) that you can download from the portal or using cmdlets.</span></span>

   ![Téléchargement des journaux d’activités personnalisées][image-data-factory-download-logs-from-custom-activity]

<span data-ttu-id="270b0-369">Pour découvrir la procédure détaillée de surveillance des jeux de données et des pipelines, consultez l’article [Surveiller et gérer les pipelines](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="270b0-369">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) for detailed steps for monitoring datasets and pipelines.</span></span>      

## <a name="data-factory-project-in-visual-studio"></a><span data-ttu-id="270b0-370">Projet Data Factory dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="270b0-370">Data Factory project in Visual Studio</span></span>  
<span data-ttu-id="270b0-371">Vous pouvez créer et publier des entités Data Factory à l’aide de Visual Studio au lieu d’utiliser le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="270b0-371">You can create and publish Data Factory entities by using Visual Studio instead of using Azure portal.</span></span> <span data-ttu-id="270b0-372">Pour en savoir plus sur la création et la publication d’entités Data Factory à l’aide de Visual Studio, consultez [Créer votre premier pipeline à l’aide de Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) et [Copier des données à partir d’un objet blob Azure vers SQL Azure](data-factory-copy-activity-tutorial-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="270b0-372">For detailed information about creating and publishing Data Factory entities by using Visual Studio, See [Build your first pipeline using Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) and [Copy data from Azure Blob to Azure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) articles.</span></span>

<span data-ttu-id="270b0-373">Si vous créez un projet Data Factory dans Visual Studio, suivez les étapes supplémentaires ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="270b0-373">Do the following additional steps if you are creating Data Factory project in Visual Studio:</span></span>
 
1. <span data-ttu-id="270b0-374">Ajoutez le projet Data Factory à la solution Visual Studio qui contient le projet d’activité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="270b0-374">Add the Data Factory project to the Visual Studio solution that contains the custom activity project.</span></span> 
2. <span data-ttu-id="270b0-375">Ajoutez une référence au projet d’activité .NET à partir du projet Data Factory.</span><span class="sxs-lookup"><span data-stu-id="270b0-375">Add a reference to the .NET activity project from the Data Factory project.</span></span> <span data-ttu-id="270b0-376">Cliquez avec le bouton droit sur le projet Data Factory, pointez sur **Ajouter**, puis cliquez sur **Référence**.</span><span class="sxs-lookup"><span data-stu-id="270b0-376">Right-click Data Factory project, point to **Add**, and then click **Reference**.</span></span> 
3. <span data-ttu-id="270b0-377">Dans la boîte de dialogue **Ajouter une référence**, sélectionnez le projet **MyDotNetActivity**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="270b0-377">In the **Add Reference** dialog box, select the **MyDotNetActivity** project, and click **OK**.</span></span>
4. <span data-ttu-id="270b0-378">Créez et publiez la solution.</span><span class="sxs-lookup"><span data-stu-id="270b0-378">Build and publish the solution.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="270b0-379">Lorsque vous publiez des entités Data Factory, un fichier zip est automatiquement créé pour vous et chargé vers le conteneur d’objets blob customactivitycontainer.</span><span class="sxs-lookup"><span data-stu-id="270b0-379">When you publish Data Factory entities, a zip file is automatically created for you and is uploaded to the blob container: customactivitycontainer.</span></span> <span data-ttu-id="270b0-380">Si le conteneur n’existe pas, il est également créé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="270b0-380">If the blob container does not exist, it is automatically created too.</span></span>  


## <a name="data-factory-and-batch-integration"></a><span data-ttu-id="270b0-381">Intégration de Data Factory et Batch</span><span class="sxs-lookup"><span data-stu-id="270b0-381">Data Factory and Batch integration</span></span>
<span data-ttu-id="270b0-382">Le service Data Factory crée un travail dans Azure Batch sous le nom **adf-poolname:job-xxx**.</span><span class="sxs-lookup"><span data-stu-id="270b0-382">The Data Factory service creates a job in Azure Batch with the name: **adf-poolname: job-xxx**.</span></span> <span data-ttu-id="270b0-383">Cliquez sur **Travaux** dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="270b0-383">Click **Jobs** from the left menu.</span></span> 

![Azure Data Factory - Travaux Batch](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

<span data-ttu-id="270b0-385">Une tâche est créée pour chaque exécution d’activité d’une tranche.</span><span class="sxs-lookup"><span data-stu-id="270b0-385">A task is created for each activity run of a slice.</span></span> <span data-ttu-id="270b0-386">Si cinq tranches sont prêtes à être traitées, cinq tâches seront créées dans ce travail.</span><span class="sxs-lookup"><span data-stu-id="270b0-386">If there are five slices ready to be processed, five tasks are created in this job.</span></span> <span data-ttu-id="270b0-387">S’il existe plusieurs nœuds de calcul dans le pool Batch, deux tranches ou plus peuvent s’exécuter en parallèle.</span><span class="sxs-lookup"><span data-stu-id="270b0-387">If there are multiple compute nodes in the Batch pool, two or more slices can run in parallel.</span></span> <span data-ttu-id="270b0-388">Vous pouvez également avoir plusieurs tranches exécutées sur le même nœud de calcul si le nombre maximum de tâches par nœud de calcul est défini sur une valeur supérieure à 1.</span><span class="sxs-lookup"><span data-stu-id="270b0-388">If the maximum tasks per compute node is set to > 1, you can also have more than one slice running on the same compute.</span></span>

![Azure Data Factory - Tâches de travaux Batch](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

<span data-ttu-id="270b0-390">Le diagramme suivant illustre la relation entre les tâches Azure Data Factory et les tâches Batch.</span><span class="sxs-lookup"><span data-stu-id="270b0-390">The following diagram illustrates the relationship between Azure Data Factory and Batch tasks.</span></span>

![Data Factory et Batch](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a><span data-ttu-id="270b0-392">Résoudre les défaillances</span><span class="sxs-lookup"><span data-stu-id="270b0-392">Troubleshoot failures</span></span>
<span data-ttu-id="270b0-393">Quelques techniques de base peuvent être utilisées pour résoudre les défaillances :</span><span class="sxs-lookup"><span data-stu-id="270b0-393">Troubleshooting consists of a few basic techniques:</span></span>

1. <span data-ttu-id="270b0-394">Si vous voyez l’erreur suivante, vous utilisez peut-être un stockage Blob chaud/froid plutôt qu’un stockage Blob Azure à usage général.</span><span class="sxs-lookup"><span data-stu-id="270b0-394">If you see the following error, you may be using a Hot/Cool blob storage instead of using a general-purpose Azure blob storage.</span></span> <span data-ttu-id="270b0-395">Chargez le fichier zip dans un **compte de stockage Blob Azure à usage général**.</span><span class="sxs-lookup"><span data-stu-id="270b0-395">Upload the zip file to a **general-purpose Azure Storage Account**.</span></span> 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of the specified Azure Blob(s).
    ``` 
2. <span data-ttu-id="270b0-396">Si vous voyez l’erreur suivante, confirmez que le nom de la classe figurant dans le fichier CS correspond au nom que vous avez spécifié pour la propriété **EntryPoint** dans le JSON du pipeline.</span><span class="sxs-lookup"><span data-stu-id="270b0-396">If you see the following error, confirm that the name of the class in the CS file matches the name you specified for the **EntryPoint** property in the pipeline JSON.</span></span> <span data-ttu-id="270b0-397">Dans la procédure pas à pas, le nom de la classe est MyDotNetActivity et le point d’entrée se trouvant dans le JSON est MyDotNetActivityNS.**MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="270b0-397">In the walkthrough, name of the class is: MyDotNetActivity, and the EntryPoint in the JSON is: MyDotNetActivityNS.**MyDotNetActivity**.</span></span>

    ```
    MyDotNetActivity assembly does not exist or doesn't implement the type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   <span data-ttu-id="270b0-398">Si les noms ne correspondent pas, vérifiez que tous les fichiers binaires se trouvent dans le **dossier racine** du fichier zip.</span><span class="sxs-lookup"><span data-stu-id="270b0-398">If the names do match, confirm that all the binaries are in the **root folder** of the zip file.</span></span> <span data-ttu-id="270b0-399">Autrement dit, lorsque vous ouvrez le fichier .zip, vous devez voir tous les fichiers dans le dossier racine, et non dans les sous-dossiers.</span><span class="sxs-lookup"><span data-stu-id="270b0-399">That is, when you open the zip file, you should see all the files in the root folder, not in any sub folders.</span></span>   
3. <span data-ttu-id="270b0-400">Si la tranche d’entrée n’est pas définie sur **Prêt**, vérifiez que la structure du dossier d’entrée est correcte et que le fichier **file.txt** est présent dans les dossiers d’entrée.</span><span class="sxs-lookup"><span data-stu-id="270b0-400">If the input slice is not set to **Ready**, confirm that the input folder structure is correct and **file.txt** exists in the input folders.</span></span>
3. <span data-ttu-id="270b0-401">Dans la méthode **Execute** de votre activité personnalisée, utilisez l’objet **IActivityLogger** pour journaliser les informations qui vous aident à résoudre d’éventuels problèmes.</span><span class="sxs-lookup"><span data-stu-id="270b0-401">In the **Execute** method of your custom activity, use the **IActivityLogger** object to log information that helps you troubleshoot issues.</span></span> <span data-ttu-id="270b0-402">Les messages enregistrés s’affichent dans les fichiers journaux utilisateur (un ou plusieurs fichiers nommés user-0.log, user-1.log, user-2.log, etc.).</span><span class="sxs-lookup"><span data-stu-id="270b0-402">The logged messages show up in the user log files (one or more files named: user-0.log, user-1.log, user-2.log, etc.).</span></span>

   <span data-ttu-id="270b0-403">Dans le panneau **OutputDataset**, cliquez sur la tranche pour afficher le panneau **TRANCHE DE DONNÉES** correspondant à cette tranche.</span><span class="sxs-lookup"><span data-stu-id="270b0-403">In the **OutputDataset** blade, click the slice to see the **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="270b0-404">Les **activités exécutées** pour cette tranche s’affichent.</span><span class="sxs-lookup"><span data-stu-id="270b0-404">You see **activity runs** for that slice.</span></span> <span data-ttu-id="270b0-405">Vous devez normalement voir une exécution d’activité pour la tranche.</span><span class="sxs-lookup"><span data-stu-id="270b0-405">You should see one activity run for the slice.</span></span> <span data-ttu-id="270b0-406">Si vous cliquez sur Exécuter dans la barre de commandes, vous pouvez démarrer une autre exécution d’activité pour la même tranche.</span><span class="sxs-lookup"><span data-stu-id="270b0-406">If you click Run in the command bar, you can start another activity run for the same slice.</span></span>

   <span data-ttu-id="270b0-407">Lorsque vous cliquez sur l’exécution d’activité, le panneau **DÉTAILS DE L’EXÉCUTION D’ACTIVITÉ** s’affiche avec une liste de fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="270b0-407">When you click the activity run, you see the **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="270b0-408">Les messages consignés s’afficheront dans le fichier user_0.log.</span><span class="sxs-lookup"><span data-stu-id="270b0-408">You see logged messages in the user_0.log file.</span></span> <span data-ttu-id="270b0-409">Lorsqu’une erreur se produit, vous verrez trois exécutions d’activité car le nombre de tentatives est défini sur 3 dans le script JSON du pipeline et de l’activité.</span><span class="sxs-lookup"><span data-stu-id="270b0-409">When an error occurs, you see three activity runs because the retry count is set to 3 in the pipeline/activity JSON.</span></span> <span data-ttu-id="270b0-410">Lorsque vous cliquez sur l’exécution de l’activité, vous accédez aux fichiers journaux qui vous permettront de résoudre l’erreur.</span><span class="sxs-lookup"><span data-stu-id="270b0-410">When you click the activity run, you see the log files that you can review to troubleshoot the error.</span></span>

   <span data-ttu-id="270b0-411">Dans la liste des fichiers journaux, cliquez sur le fichier **user-0.log**.</span><span class="sxs-lookup"><span data-stu-id="270b0-411">In the list of log files, click the **user-0.log**.</span></span> <span data-ttu-id="270b0-412">Le volet droit affiche les résultats de l’utilisation de la méthode **IActivityLogger.Write** .</span><span class="sxs-lookup"><span data-stu-id="270b0-412">In the right panel are the results of using the **IActivityLogger.Write** method.</span></span> <span data-ttu-id="270b0-413">Si vous ne voyez pas tous les messages, vérifiez si vous avez plusieurs fichiers journaux nommés user_1.log, user_2.log, etc. Si ce n’est pas le cas, le code peut avoir échoué après le dernier message enregistré.</span><span class="sxs-lookup"><span data-stu-id="270b0-413">If you don't see all messages, check if you have more log files named: user_1.log, user_2.log etc. Otherwise, the code may have failed after the last logged message.</span></span>

   <span data-ttu-id="270b0-414">En outre, consultez **system-0.log** pour vérifier les exceptions et messages d’erreur système éventuels.</span><span class="sxs-lookup"><span data-stu-id="270b0-414">In addition, check **system-0.log** for any system error messages and exceptions.</span></span>
4. <span data-ttu-id="270b0-415">Incluez le fichier **PDB** dans le fichier zip afin que les détails de l’erreur incluent des informations telles que la **pile des appels** quand une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="270b0-415">Include the **PDB** file in the zip file so that the error details have information such as **call stack** when an error occurs.</span></span>
5. <span data-ttu-id="270b0-416">Tous les fichiers contenus dans le fichier zip de l’activité personnalisée doivent se trouver au **premier niveau** et ne doivent pas contenir de sous-dossiers.</span><span class="sxs-lookup"><span data-stu-id="270b0-416">All the files in the zip file for the custom activity must be at the **top level** with no sub folders.</span></span>
6. <span data-ttu-id="270b0-417">Assurez-vous que les paramètres **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/Mydotnetactivity.zip) et **packageLinkedService** (qui doit pointer vers le Stockage Blob Azure **à usage général** contenant le fichier .zip) sont définis sur des valeurs correctes.</span><span class="sxs-lookup"><span data-stu-id="270b0-417">Ensure that the **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point to the **general-purpose**Azure blob storage that contains the zip file) are set to correct values.</span></span>
7. <span data-ttu-id="270b0-418">Si vous avez corrigé une erreur et souhaitez relancer le traitement de la tranche, cliquez avec le bouton droit sur la tranche dans le panneau **OutputDataset** puis cliquez sur **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="270b0-418">If you fixed an error and want to reprocess the slice, right-click the slice in the **OutputDataset** blade and click **Run**.</span></span>
8. <span data-ttu-id="270b0-419">Si vous voyez l’erreur suivante, vous utilisez une version du package Stockage Azure supérieure à 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="270b0-419">If you see the following error, you are using the Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="270b0-420">Le lanceur du service Data Factory requiert la version 4.3 du package Windows Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="270b0-420">Data Factory service launcher requires the 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="270b0-421">Consultez la section [Isolation du domaine d’application](#appdomain-isolation) pour obtenir une autre solution si vous devez utiliser la dernière version de l’assembly du stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="270b0-421">See [Appdomain isolation](#appdomain-isolation) section for a work-around if you must use the later version of Azure Storage assembly.</span></span> 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    <span data-ttu-id="270b0-422">Si vous pouvez utiliser la version 4.3.0 du package du stockage Azure, supprimez la référence existante à la version supérieure à 4.3.0 du package du stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="270b0-422">If you can use the 4.3.0 version of Azure Storage package, remove the existing reference to Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="270b0-423">Exécutez ensuite la commande suivante à partir de la console du gestionnaire de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="270b0-423">Then, run the following command from NuGet Package Manager Console.</span></span> 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    <span data-ttu-id="270b0-424">Créez le projet.</span><span class="sxs-lookup"><span data-stu-id="270b0-424">Build the project.</span></span> <span data-ttu-id="270b0-425">Supprimez la version supérieure à 4.3.0 de l'assembly Stockage Azure du dossier bin/Debug.</span><span class="sxs-lookup"><span data-stu-id="270b0-425">Delete Azure.Storage assembly of version > 4.3.0 from the bin\Debug folder.</span></span> <span data-ttu-id="270b0-426">Créez un fichier zip avec les fichiers binaires et le fichier PDB.</span><span class="sxs-lookup"><span data-stu-id="270b0-426">Create a zip file with binaries and the PDB file.</span></span> <span data-ttu-id="270b0-427">Remplacez l’ancien fichier zip par celui-ci dans le conteneur d’objets blob (customactivitycontainer).</span><span class="sxs-lookup"><span data-stu-id="270b0-427">Replace the old zip file with this one in the blob container (customactivitycontainer).</span></span> <span data-ttu-id="270b0-428">Exécutez de nouveau les tranches ayant échoué (en cliquant avec le bouton droit sur la tranche, puis en choisissant Exécuter).</span><span class="sxs-lookup"><span data-stu-id="270b0-428">Rerun the slices that failed (right-click slice, and click Run).</span></span>   
8. <span data-ttu-id="270b0-429">L’activité personnalisée n’utilise pas le ficher **app.config** de votre package.</span><span class="sxs-lookup"><span data-stu-id="270b0-429">The custom activity does not use the **app.config** file from your package.</span></span> <span data-ttu-id="270b0-430">Par conséquent, si votre code lit des chaînes de connexion dans le fichier de configuration, il ne fonctionne pas lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="270b0-430">Therefore, if your code reads any connection strings from the configuration file, it does not work at runtime.</span></span> <span data-ttu-id="270b0-431">Quand vous utilisez Azure Batch, la meilleure pratique consiste à stocker les clés secrètes dans un coffre de clés **Azure KeyVault**, à utiliser un principal de service basé sur certificat pour protéger le **coffre de clés** et à distribuer le certificat à un pool Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="270b0-431">The best practice when using Azure Batch is to hold any secrets in an **Azure KeyVault**, use a certificate-based service principal to protect the **keyvault**, and distribute the certificate to Azure Batch pool.</span></span> <span data-ttu-id="270b0-432">L’activité personnalisée .NET peut alors accéder aux secrets du coffre de clés au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="270b0-432">The .NET custom activity then can access secrets from the KeyVault at runtime.</span></span> <span data-ttu-id="270b0-433">Cette solution est générique et peut s’adapter à n’importe quel type de clé secrète, et pas uniquement aux chaînes de connexion.</span><span class="sxs-lookup"><span data-stu-id="270b0-433">This solution is a generic solution and can scale to any type of secret, not just connection string.</span></span>

   <span data-ttu-id="270b0-434">Il existe une solution plus simple (mais non recommandée) : vous pouvez créer un **service lié SQL Azure** avec des paramètres de chaîne de connexion, puis créer un jeu de données qui utilise le service lié et chaîner le jeu de données à l’activité .NET personnalisée en tant que jeu de données d’entrée factice.</span><span class="sxs-lookup"><span data-stu-id="270b0-434">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses the linked service, and chain the dataset as a dummy input dataset to the custom .NET activity.</span></span> <span data-ttu-id="270b0-435">Vous pouvez ensuite accéder à la chaîne de connexion du service lié dans le code de l’activité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="270b0-435">You can then access the linked service's connection string in the custom activity code.</span></span>  

## <a name="update-custom-activity"></a><span data-ttu-id="270b0-436">Mettre à jour l’activité personnalisée</span><span class="sxs-lookup"><span data-stu-id="270b0-436">Update custom activity</span></span>
<span data-ttu-id="270b0-437">Si vous mettez à jour le code de l’activité personnalisée, créez et téléchargez le fichier .zip qui contient les nouveaux fichiers binaires pour le stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="270b0-437">If you update the code for the custom activity, build it, and upload the zip file that contains new binaries to the blob storage.</span></span>

## <a name="appdomain-isolation"></a><span data-ttu-id="270b0-438">Isolation du domaine d’application</span><span class="sxs-lookup"><span data-stu-id="270b0-438">Appdomain isolation</span></span>
<span data-ttu-id="270b0-439">Consultez [Cross AppDomain Sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) (Exemple d’isolation entre domaines d’application) pour savoir comment créer une activité personnalisée qui n’est pas limitée aux versions d’assembly utilisées par le lanceur d’Azure Data Factory (par exemple, WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.).</span><span class="sxs-lookup"><span data-stu-id="270b0-439">See [Cross AppDomain Sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) that shows you how to create a custom activity that is not constrained to assembly versions used by the Data Factory launcher (example: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.).</span></span>

## <a name="access-extended-properties"></a><span data-ttu-id="270b0-440">Accéder aux propriétés étendues</span><span class="sxs-lookup"><span data-stu-id="270b0-440">Access extended properties</span></span>
<span data-ttu-id="270b0-441">Vous pouvez déclarer des propriétés étendues dans l’activité JSON, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="270b0-441">You can declare extended properties in the activity JSON as shown in the following sample:</span></span>

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


<span data-ttu-id="270b0-442">Dans cet exemple, il existe deux propriétés étendues, **SliceStart** et **DataFactoryName**.</span><span class="sxs-lookup"><span data-stu-id="270b0-442">In the example, there are two extended properties: **SliceStart** and **DataFactoryName**.</span></span> <span data-ttu-id="270b0-443">La valeur de SliceStart est basée sur la variable système SliceStart.</span><span class="sxs-lookup"><span data-stu-id="270b0-443">The value for SliceStart is based on the SliceStart system variable.</span></span> <span data-ttu-id="270b0-444">Consultez [Variables système](data-factory-functions-variables.md) pour obtenir la liste des variables système prises en charge.</span><span class="sxs-lookup"><span data-stu-id="270b0-444">See [System Variables](data-factory-functions-variables.md) for a list of supported system variables.</span></span> <span data-ttu-id="270b0-445">La valeur de DataFactoryName est codée en dur sous la forme CustomActivityFactory.</span><span class="sxs-lookup"><span data-stu-id="270b0-445">The value for DataFactoryName is hard-coded to CustomActivityFactory.</span></span>

<span data-ttu-id="270b0-446">Pour accéder à ces propriétés étendues dans la méthode **Execute**, utilisez un code semblable au suivant :</span><span class="sxs-lookup"><span data-stu-id="270b0-446">To access these extended properties in the **Execute** method, use code similar to the following code:</span></span>

```csharp
// to get extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// to log all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a><span data-ttu-id="270b0-447">Mise à l’échelle automatique d’Azure Batch</span><span class="sxs-lookup"><span data-stu-id="270b0-447">Auto-scaling of Azure Batch</span></span>
<span data-ttu-id="270b0-448">Vous pouvez aussi créer un pool Azure Batch avec la fonctionnalité **autoscale** .</span><span class="sxs-lookup"><span data-stu-id="270b0-448">You can also create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="270b0-449">Par exemple, vous pouvez créer un pool Azure Batch avec 0 machine virtuelle dédiée et une formule de mise à l’échelle automatique en fonction du nombre de tâches en attente.</span><span class="sxs-lookup"><span data-stu-id="270b0-449">For example, you could create an azure batch pool with 0 dedicated VMs and an autoscale formula based on the number of pending tasks.</span></span> 

<span data-ttu-id="270b0-450">Cet exemple de formule permet d’obtenir le comportement suivant : quand le pool est créé, il commence avec 1 machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="270b0-450">The sample formula here achieves the following behavior: When the pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="270b0-451">La métrique $PendingTasks définit le nombre de tâches dans l’état En cours d’exécution + Actif (en file d’attente).</span><span class="sxs-lookup"><span data-stu-id="270b0-451">$PendingTasks metric defines the number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="270b0-452">Cette formule recherche le nombre moyen de tâches en attente au cours des 180 dernières secondes et définit TargetDedicated en conséquence.</span><span class="sxs-lookup"><span data-stu-id="270b0-452">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="270b0-453">Elle garantit que TargetDedicated ne va jamais au-delà de 25 machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="270b0-453">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="270b0-454">Par conséquent, à mesure que de nouvelles tâches sont envoyées, le pool s’accroît automatiquement et, au fil de la réalisation des tâches, les machines virtuelles se libèrent une à une et la mise à l’échelle automatique réduit ces machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="270b0-454">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span></span> <span data-ttu-id="270b0-455">Vous pouvez ajuster startingNumberOfVMs et maxNumberofVMs selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="270b0-455">startingNumberOfVMs and maxNumberofVMs can be adjusted to your needs.</span></span>

<span data-ttu-id="270b0-456">Formule de mise à l’échelle automatique :</span><span class="sxs-lookup"><span data-stu-id="270b0-456">Autoscale formula:</span></span>

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

<span data-ttu-id="270b0-457">Pour plus d’informations, consultez [Mettre automatiquement à l’échelle les nœuds de calcul dans un pool Azure Batch](../batch/batch-automatic-scaling.md) .</span><span class="sxs-lookup"><span data-stu-id="270b0-457">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

<span data-ttu-id="270b0-458">Si le pool utilise la valeur par défaut du paramètre [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), le service Batch peut mettre 15 à 30 minutes à préparer la machine virtuelle avant d’exécuter l’activité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="270b0-458">If the pool is using the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service could take 15-30 minutes to prepare the VM before running the custom activity.</span></span>  <span data-ttu-id="270b0-459">Si le pool utilise une autre valeur pour autoScaleEvaluationInterval, le service Batch peut prendre la durée d’autoScaleEvaluationInterval + 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="270b0-459">If the pool is using a different autoScaleEvaluationInterval, the Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>

## <a name="use-hdinsight-compute-service"></a><span data-ttu-id="270b0-460">Utiliser le service de calcul HDInsight</span><span class="sxs-lookup"><span data-stu-id="270b0-460">Use HDInsight compute service</span></span>
<span data-ttu-id="270b0-461">Dans la procédure pas à pas, vous avez utilisé le calcul Azure Batch pour exécuter l’activité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="270b0-461">In the walkthrough, you used Azure Batch compute to run the custom activity.</span></span> <span data-ttu-id="270b0-462">Vous pouvez également utiliser votre propre cluster HDInsight sous Windows ou configurer Data Factory pour créer un cluster HDInsight sous Windows à la demande, et utiliser le cluster HDInsight pour exécuter l’activité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="270b0-462">You can also use your own Windows-based HDInsight cluster or have Data Factory create an on-demand Windows-based HDInsight cluster and have the custom activity run on the HDInsight cluster.</span></span> <span data-ttu-id="270b0-463">Voici les cinq étapes de haut niveau pour utiliser un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="270b0-463">Here are the high-level steps for using an HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="270b0-464">Les activités .NET personnalisées s’exécutent uniquement sur des clusters HDInsight sous Windows.</span><span class="sxs-lookup"><span data-stu-id="270b0-464">The custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="270b0-465">Un moyen de contourner cette limitation consiste à utiliser l’activité Map Reduce pour exécuter du code Java personnalisé sur un cluster HDInsight sous Linux.</span><span class="sxs-lookup"><span data-stu-id="270b0-465">A workaround for this limitation is to use the Map Reduce Activity to run custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="270b0-466">Une autre option consiste à utiliser un pool Azure Batch de machines virtuelles pour exécuter des activités personnalisées au lieu d’utiliser un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="270b0-466">Another option is to use an Azure Batch pool of VMs to run custom activities instead of using a HDInsight cluster.</span></span>
 

1. <span data-ttu-id="270b0-467">Créez un service lié Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="270b0-467">Create an Azure HDInsight linked service.</span></span>   
2. <span data-ttu-id="270b0-468">Utilisez le service lié HDInsight au lieu du service **AzureBatchLinkedService** dans le code JSON du pipeline.</span><span class="sxs-lookup"><span data-stu-id="270b0-468">Use HDInsight linked service in place of **AzureBatchLinkedService** in the pipeline JSON.</span></span>

<span data-ttu-id="270b0-469">Vous pouvez modifier les heures de **début** et de **fin** du pipeline pour pouvoir tester le scénario avec le service Azure HDInsight dans le cadre de cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="270b0-469">If you want to test it with the walkthrough, change **start** and **end** times for the pipeline so that you can test the scenario with the Azure HDInsight service.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="270b0-470">Créer le service lié Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="270b0-470">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="270b0-471">Le service Azure Data Factory prend en charge la création d’un cluster à la demande et l’utilise pour traiter des données d’entrée afin de produire des données de sortie.</span><span class="sxs-lookup"><span data-stu-id="270b0-471">The Azure Data Factory service supports creation of an on-demand cluster and use it to process input to produce output data.</span></span> <span data-ttu-id="270b0-472">Vous pouvez également utiliser votre propre cluster pour effectuer cette opération.</span><span class="sxs-lookup"><span data-stu-id="270b0-472">You can also use your own cluster to perform the same.</span></span> <span data-ttu-id="270b0-473">Lorsque vous utilisez un cluster HDInsight à la demande, un cluster est créé pour chaque tranche.</span><span class="sxs-lookup"><span data-stu-id="270b0-473">When you use on-demand HDInsight cluster, a cluster gets created for each slice.</span></span> <span data-ttu-id="270b0-474">Par contre, si vous utilisez votre propre cluster HDInsight, le cluster est prêt à traiter la tranche immédiatement.</span><span class="sxs-lookup"><span data-stu-id="270b0-474">Whereas, if you use your own HDInsight cluster, the cluster is ready to process the slice immediately.</span></span> <span data-ttu-id="270b0-475">Par conséquent, lorsque vous utilisez un cluster à la demande, vous ne voyez pas les données de sortie aussi rapidement que lorsque vous utilisez votre propre cluster.</span><span class="sxs-lookup"><span data-stu-id="270b0-475">Therefore, when you use on-demand cluster, you may not see the output data as quickly as when you use your own cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="270b0-476">Lors de l’exécution, une instance d’activité .NET s’exécute uniquement sur un nœud de travail du cluster HDInsight ; elle ne peut pas être mise à l’échelle pour s’exécuter sur plusieurs nœuds.</span><span class="sxs-lookup"><span data-stu-id="270b0-476">At runtime, an instance of a .NET activity runs only on one worker node in the HDInsight cluster; it cannot be scaled to run on multiple nodes.</span></span> <span data-ttu-id="270b0-477">Cependant, plusieurs instances d’activité .NET peuvent s’exécuter en parallèle sur différents nœuds du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="270b0-477">Multiple instances of .NET activity can run in parallel on different nodes of the HDInsight cluster.</span></span>
>
>

##### <a name="to-use-an-on-demand-hdinsight-cluster"></a><span data-ttu-id="270b0-478">Pour utiliser un cluster HDInsight à la demande</span><span class="sxs-lookup"><span data-stu-id="270b0-478">To use an on-demand HDInsight cluster</span></span>
1. <span data-ttu-id="270b0-479">Dans le **portail Azure**, cliquez sur **Créer et déployer** de la page d’accueil du logiciel Data Factory.</span><span class="sxs-lookup"><span data-stu-id="270b0-479">In the **Azure portal**, click **Author and Deploy** in the Data Factory home page.</span></span>
2. <span data-ttu-id="270b0-480">Dans Data Factory Editor, cliquez sur **Nouveau calcul** dans la barre de commandes et sélectionnez l’option **Cluster HDInsight à la demande** dans le menu.</span><span class="sxs-lookup"><span data-stu-id="270b0-480">In the Data Factory Editor, click **New compute** from the command bar and select **On-demand HDInsight cluster** from the menu.</span></span>
3. <span data-ttu-id="270b0-481">Apportez les modifications suivantes au script JSON :</span><span class="sxs-lookup"><span data-stu-id="270b0-481">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="270b0-482">Pour la propriété **clusterSize** , spécifiez la taille du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="270b0-482">For the **clusterSize** property, specify the size of the HDInsight cluster.</span></span>
   2. <span data-ttu-id="270b0-483">Pour la propriété **timeToLive** , spécifiez la durée pendant laquelle le client peut être inactif avant d’être supprimé.</span><span class="sxs-lookup"><span data-stu-id="270b0-483">For the **timeToLive** property, specify how long the customer can be idle before it is deleted.</span></span>
   3. <span data-ttu-id="270b0-484">Pour la propriété **version** , spécifiez la version de Microsoft Azure HDInsight que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="270b0-484">For the **version** property, specify the HDInsight version you want to use.</span></span> <span data-ttu-id="270b0-485">Si vous excluez cette propriété, la version utilisée sera la plus récente.</span><span class="sxs-lookup"><span data-stu-id="270b0-485">If you exclude this property, the latest version is used.</span></span>  
   4. <span data-ttu-id="270b0-486">Pour la propriété **LinkedServiceName**, indiquez **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="270b0-486">For the **linkedServiceName**, specify **AzureStorageLinkedService**.</span></span>

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
    > <span data-ttu-id="270b0-487">Les activités .NET personnalisées s’exécutent uniquement sur des clusters HDInsight sous Windows.</span><span class="sxs-lookup"><span data-stu-id="270b0-487">The custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="270b0-488">Un moyen de contourner cette limitation consiste à utiliser l’activité Map Reduce pour exécuter du code Java personnalisé sur un cluster HDInsight sous Linux.</span><span class="sxs-lookup"><span data-stu-id="270b0-488">A workaround for this limitation is to use the Map Reduce Activity to run custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="270b0-489">Une autre option consiste à utiliser un pool Azure Batch de machines virtuelles pour exécuter des activités personnalisées au lieu d’utiliser un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="270b0-489">Another option is to use an Azure Batch pool of VMs to run custom activities instead of using a HDInsight cluster.</span></span>

4. <span data-ttu-id="270b0-490">Cliquez sur l’option **Déployer** de la barre de commandes pour déployer le service lié.</span><span class="sxs-lookup"><span data-stu-id="270b0-490">Click **Deploy** on the command bar to deploy the linked service.</span></span>

##### <a name="to-use-your-own-hdinsight-cluster"></a><span data-ttu-id="270b0-491">Pour utiliser votre propre cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="270b0-491">To use your own HDInsight cluster:</span></span>
1. <span data-ttu-id="270b0-492">Dans le **portail Azure**, cliquez sur **Créer et déployer** de la page d’accueil du logiciel Data Factory.</span><span class="sxs-lookup"><span data-stu-id="270b0-492">In the **Azure portal**, click **Author and Deploy** in the Data Factory home page.</span></span>
2. <span data-ttu-id="270b0-493">Dans **Data Factory Editor**, cliquez sur **Nouveau calcul** dans la barre de commandes et sélectionnez **Cluster HDInsight** dans le menu.</span><span class="sxs-lookup"><span data-stu-id="270b0-493">In the **Data Factory Editor**, click **New compute** from the command bar and select **HDInsight cluster** from the menu.</span></span>
3. <span data-ttu-id="270b0-494">Apportez les modifications suivantes au script JSON :</span><span class="sxs-lookup"><span data-stu-id="270b0-494">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="270b0-495">Pour la propriété **clusterUri** , saisissez l’URL de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="270b0-495">For the **clusterUri** property, enter the URL for your HDInsight.</span></span> <span data-ttu-id="270b0-496">Par exemple : https://<clustername>.azurehdinsight.net/.</span><span class="sxs-lookup"><span data-stu-id="270b0-496">For example: https://<clustername>.azurehdinsight.net/</span></span>     
   2. <span data-ttu-id="270b0-497">Pour la propriété **UserName** , saisissez le nom d’utilisateur ayant accès au cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="270b0-497">For the **UserName** property, enter the user name who has access to the HDInsight cluster.</span></span>
   3. <span data-ttu-id="270b0-498">Pour la propriété **Password** , spécifiez le mot de passe de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="270b0-498">For the **Password** property, enter the password for the user.</span></span>
   4. <span data-ttu-id="270b0-499">Pour la propriété **LinkedServiceName**, entrez **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="270b0-499">For the **LinkedServiceName** property, enter **AzureStorageLinkedService**.</span></span>
4. <span data-ttu-id="270b0-500">Cliquez sur l’option **Déployer** de la barre de commandes pour déployer le service lié.</span><span class="sxs-lookup"><span data-stu-id="270b0-500">Click **Deploy** on the command bar to deploy the linked service.</span></span>

<span data-ttu-id="270b0-501">Pour plus d’informations, consultez [Services de calcul liés](data-factory-compute-linked-services.md) .</span><span class="sxs-lookup"><span data-stu-id="270b0-501">See [Compute linked services](data-factory-compute-linked-services.md) for details.</span></span>

<span data-ttu-id="270b0-502">Dans le code **JSON du pipeline**, utilisez le service lié HDInsight (celui créé à la demande ou le vôtre) :</span><span class="sxs-lookup"><span data-stu-id="270b0-502">In the **pipeline JSON**, use HDInsight (on-demand or your own) linked service:</span></span>

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

## <a name="create-a-custom-activity-by-using-net-sdk"></a><span data-ttu-id="270b0-503">Créer une activité personnalisée à l’aide du kit .NET SDK</span><span class="sxs-lookup"><span data-stu-id="270b0-503">Create a custom activity by using .NET SDK</span></span>
<span data-ttu-id="270b0-504">Dans la procédure pas à pas de cet article, vous créez une fabrique de données avec un pipeline qui utilise l’activité personnalisée à l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="270b0-504">In the walkthrough in this article, you create a data factory with a pipeline that uses the custom activity by using the Azure portal.</span></span> <span data-ttu-id="270b0-505">Le code suivant montre comment créer la fabrique de données à l’aide du kit .NET SDK à la place.</span><span class="sxs-lookup"><span data-stu-id="270b0-505">The following code shows you how to create the data factory by using .NET SDK instead.</span></span> <span data-ttu-id="270b0-506">Vous trouverez plus d’informations sur l’utilisation du Kit SDK pour créer des pipelines par programme dans l’article [Créer un pipeline avec une activité de copie à l’aide de l’API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="270b0-506">You can find more details about using SDK to programmatically create pipelines in the [create a pipeline with copy activity by using .NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md) article.</span></span> 

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

            // TODO: replace ADFTutorialResourceGroup with the name of your resource group.
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

                            // Initial value for pipeline's active period. With this, you won't need to set slice status
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

            throw new InvalidOperationException("Failed to acquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a><span data-ttu-id="270b0-507">Déboguer une activité personnalisée dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="270b0-507">Debug custom activity in Visual Studio</span></span>
<span data-ttu-id="270b0-508">L’exemple [Azure Data Factory - Environnement local](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) sur GitHub inclut un outil qui vous permet de déboguer des activités .NET personnalisées dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="270b0-508">The [Azure Data Factory - local environment](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) sample on GitHub includes a tool that allows you to debug custom .NET activities within Visual Studio.</span></span>  


## <a name="sample-custom-activities-on-github"></a><span data-ttu-id="270b0-509">Exemples d’activités personnalisées sur GitHub</span><span class="sxs-lookup"><span data-stu-id="270b0-509">Sample custom activities on GitHub</span></span>
| <span data-ttu-id="270b0-510">Exemple</span><span class="sxs-lookup"><span data-stu-id="270b0-510">Sample</span></span> | <span data-ttu-id="270b0-511">Rôle des activités personnalisées</span><span class="sxs-lookup"><span data-stu-id="270b0-511">What custom activity does</span></span> |
| --- | --- |
| <span data-ttu-id="270b0-512">[Téléchargeur de données HTTP](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span><span class="sxs-lookup"><span data-stu-id="270b0-512">[HTTP Data Downloader](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span></span> |<span data-ttu-id="270b0-513">Télécharge des données à partir d'un point de terminaison HTTP vers Stockage Blob Azure à l'aide d’une activité C# personnalisée dans Data Factory.</span><span class="sxs-lookup"><span data-stu-id="270b0-513">Downloads data from an HTTP Endpoint to Azure Blob Storage using custom C# Activity in Data Factory.</span></span> |
| [<span data-ttu-id="270b0-514">Exemple d’analyse d’opinions Twitter</span><span class="sxs-lookup"><span data-stu-id="270b0-514">Twitter Sentiment Analysis sample</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |<span data-ttu-id="270b0-515">Appelle un modèle Azure ML et effectue l’analyse, la notation, la prédiction, etc. des opinions.</span><span class="sxs-lookup"><span data-stu-id="270b0-515">Invokes an Azure ML model and do sentiment analysis, scoring, prediction etc.</span></span> |
| <span data-ttu-id="270b0-516">[Exécuter un script R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span><span class="sxs-lookup"><span data-stu-id="270b0-516">[Run R Script](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span></span> |<span data-ttu-id="270b0-517">Appelle un script R en exécutant RScript.exe sur votre cluster HDInsight, sur lequel R est installé.</span><span class="sxs-lookup"><span data-stu-id="270b0-517">Invokes R script by running RScript.exe on your HDInsight cluster that already has R Installed on it.</span></span> |
| [<span data-ttu-id="270b0-518">Activité .NET entre AppDomains</span><span class="sxs-lookup"><span data-stu-id="270b0-518">Cross AppDomain .NET Activity</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |<span data-ttu-id="270b0-519">Utilise des versions d’assembly différentes de celles utilisées par le lanceur de Data Factory</span><span class="sxs-lookup"><span data-stu-id="270b0-519">Uses different assembly versions from ones used by the Data Factory launcher</span></span> |
| [<span data-ttu-id="270b0-520">Retraiter un modèle dans Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="270b0-520">Reprocess a model in Azure Analysis Services</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  <span data-ttu-id="270b0-521">Retraite un modèle dans Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="270b0-521">Reprocesses a model in Azure Analysis Services.</span></span> |

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
