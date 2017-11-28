---
title: "Conserver les sorties de travaux et de tâches dans Azure Storage avec la bibliothèque File Conventions pour .NET - Azure Batch | Microsoft Docs"
description: "Apprenez à utiliser la bibliothèque File Conventions d’Azure Batch pour conserver les sorties de travaux et de tâches dans Azure Storage et l’afficher dans le portail Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a9de327c20463469bc91d9720aa17333a36f919e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="persist-job-and-task-data-to-azure-storage-with-the-batch-file-conventions-library-for-net-to-persist"></a><span data-ttu-id="8780b-103">Conserver le résultat d’un travail et d’une tâche dans Azure Storage avec la bibliothèque File Conventions pour .NET</span><span class="sxs-lookup"><span data-stu-id="8780b-103">Persist job and task data to Azure Storage with the Batch File Conventions library for .NET to persist</span></span> 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="8780b-104">La [bibliothèque File Conventions pour .NET d’Azure Batch][nuget_package] est un moyen de conserver des données de tâches.</span><span class="sxs-lookup"><span data-stu-id="8780b-104">One way to persist task data is to use the [Azure Batch File Conventions library for .NET][nuget_package].</span></span> <span data-ttu-id="8780b-105">La bibliothèque File Conventions simplifie les processus de stockage et de récupération des données de sortie de tâches dans Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8780b-105">The File Conventions library simplifies the process of storing task output data to Azure Storage and retrieving it.</span></span> <span data-ttu-id="8780b-106">Cette bibliothèque est destinée à être utilisée dans le code de tâche et client &mdash; dans le code de tâche pour la conservation des fichiers et dans le code client pour les répertorier et les récupérer.</span><span class="sxs-lookup"><span data-stu-id="8780b-106">You can use the File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code to list and retrieve them.</span></span> <span data-ttu-id="8780b-107">Le code de tâche peut également utiliser la bibliothèque pour récupérer la sortie des tâches en amont, comme dans un cas de [dépendances de tâche](batch-task-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="8780b-107">Your task code can also use the library to retrieve the output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span> 

<span data-ttu-id="8780b-108">Pour récupérer des fichiers de sortie avec la bibliothèque File Conventions, vous pouvez localiser les fichiers d’un travail donné ou d’une tâche donnée en les répertoriant par ID et objectif.</span><span class="sxs-lookup"><span data-stu-id="8780b-108">To retrieve output files with the File Conventions library, you can locate the files for a given job or task by listing them by ID and purpose.</span></span> <span data-ttu-id="8780b-109">Vous n’avez pas besoin de connaître les noms ou les emplacements des fichiers.</span><span class="sxs-lookup"><span data-stu-id="8780b-109">You don't need to know the names or locations of the files.</span></span> <span data-ttu-id="8780b-110">Vous pouvez par exemple utiliser la bibliothèque File Conventions pour répertorier tous les fichiers intermédiaires d’une tâche donnée, ou obtenir un aperçu de fichier d’un travail donné.</span><span class="sxs-lookup"><span data-stu-id="8780b-110">For example, you can use the File Conventions library to list all intermediate files for a given task, or get a preview file for a given job.</span></span>

> [!TIP]
> <span data-ttu-id="8780b-111">À partir de la version 2017-05-01, l’API du service Batch prend en charge la conservation des données de sortie vers Azure Storage pour les tâches, y compris celles du gestionnaire de travaux, qui s’exécutent sur des pools sous la configuration de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8780b-111">Starting with version 2017-05-01, the Batch service API supports persisting output data to Azure Storage for tasks and job manager tasks that run on pools created with the virtual machine configuration.</span></span> <span data-ttu-id="8780b-112">L’API du service Batch fournit un moyen simple pour conserver les sorties depuis le code, qui crée une tâche et constitue une alternative à la bibliothèque File Conventions.</span><span class="sxs-lookup"><span data-stu-id="8780b-112">The Batch service API provides a simple way to persist output from within the code that creates a task and serves as an alternative to the File Conventions library.</span></span> <span data-ttu-id="8780b-113">Vous pouvez modifier les applications du client Batch pour conserver les sorties sans mettre à jour l’application que votre tâche exécute.</span><span class="sxs-lookup"><span data-stu-id="8780b-113">You can modify your Batch client applications to persist output without needing to update the application that your task is running.</span></span> <span data-ttu-id="8780b-114">Pour en savoir plus, consultez l’article [Conserver les données de tâche dans Azure Storage avec l’API de service Batch](batch-task-output-files.md).</span><span class="sxs-lookup"><span data-stu-id="8780b-114">For more information, see [Persist task data to Azure Storage with the Batch service API](batch-task-output-files.md).</span></span>
> 
> 

## <a name="when-do-i-use-the-file-conventions-library-to-persist-task-output"></a><span data-ttu-id="8780b-115">Quand utiliser la bibliothèque File Conventions pour conserver les sorties de tâche ?</span><span class="sxs-lookup"><span data-stu-id="8780b-115">When do I use the File Conventions library to persist task output?</span></span>

<span data-ttu-id="8780b-116">Azure Batch offre plusieurs manières de conserver les sorties de tâche.</span><span class="sxs-lookup"><span data-stu-id="8780b-116">Azure Batch provides more than one way to persist task output.</span></span> <span data-ttu-id="8780b-117">File Conventions remplit parfaitement son rôle dans les cas suivants :</span><span class="sxs-lookup"><span data-stu-id="8780b-117">The File Conventions is best suited to these scenarios:</span></span>

- <span data-ttu-id="8780b-118">Vous pouvez facilement modifier le code de l’application que votre tâche exécute afin de conserver les fichiers à l’aide de la bibliothèque File Conventions.</span><span class="sxs-lookup"><span data-stu-id="8780b-118">You can easily modify the code for the application that your task is running to persist files using the File Conventions library.</span></span>
- <span data-ttu-id="8780b-119">Vous voulez diffuser les données vers Azure Storage alors que la tâche est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="8780b-119">You want to stream data to Azure Storage while the task is still running.</span></span>
- <span data-ttu-id="8780b-120">Vous voulez conserver les données de pools créés avec la configuration de service cloud ou la configuration de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8780b-120">You want to persist data from pools created with either the cloud service configuration or the virtual machine configuration.</span></span>
- <span data-ttu-id="8780b-121">Votre application cliente ou d’autres tâches du travail doivent localiser et télécharger les fichiers de sortie de tâche par ID ou usage.</span><span class="sxs-lookup"><span data-stu-id="8780b-121">Your client application or other tasks in the job needs to locate and download task output files by ID or by purpose.</span></span> 
- <span data-ttu-id="8780b-122">Vous voulez consulter les sorties de tâche dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8780b-122">You want to view task output in the Azure portal.</span></span>

<span data-ttu-id="8780b-123">Si votre scénario diffère de ceux répertoriés ci-dessus, vous devrez peut-être envisager une approche différente.</span><span class="sxs-lookup"><span data-stu-id="8780b-123">If your scenario differs from those listed above, you may need to consider a different approach.</span></span> <span data-ttu-id="8780b-124">Pour en savoir plus sur les autres options de conservation des sorties de tâche, consultez l’article [Conserver les sorties de travail et de tâche terminées dans Azure Storage](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="8780b-124">For more information on other options for persisting task output, see [Persist job and task output to Azure Storage](batch-task-output.md).</span></span> 

## <a name="what-is-the-batch-file-conventions-standard"></a><span data-ttu-id="8780b-125">Qu’est-ce qu’un standard de nommage des fichiers Batch dans File Conventions ?</span><span class="sxs-lookup"><span data-stu-id="8780b-125">What is the Batch File Conventions standard?</span></span>

<span data-ttu-id="8780b-126">Le [standard de nommage des fichiers Batch dans File Conventions](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) fournit un schéma d’affectation de noms pour les conteneurs de destination et chemins d’accès d’objets blob dans lesquels vos fichiers de sortie sont rédigés.</span><span class="sxs-lookup"><span data-stu-id="8780b-126">The [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for the destination containers and blob paths to which your output files are written.</span></span> <span data-ttu-id="8780b-127">Les fichiers conservés dans Azure Storage qui adhèrent au standard de nommage de File Conventions sont automatiquement disponibles à la consultation dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8780b-127">Files persisted to Azure Storage that adhere to the File Conventions standard are automatically available for viewing in the Azure portal.</span></span> <span data-ttu-id="8780b-128">Le portail connait les conventions d’affectation de noms et peut donc afficher les fichiers qui y adhèrent.</span><span class="sxs-lookup"><span data-stu-id="8780b-128">The portal is aware of the naming convention and so can display files that adhere to it.</span></span>

<span data-ttu-id="8780b-129">La bibliothèque File Conventions pour .NET nomme automatiquement vos conteneurs de stockage et les fichiers de sortie de tâche en respectant le standard de nommage de File Conventions.</span><span class="sxs-lookup"><span data-stu-id="8780b-129">The File Conventions library for .NET automatically names your storage containers and task output files according to the File Conventions standard.</span></span> <span data-ttu-id="8780b-130">La bibliothèque File Conventions fournit également des méthodes de requête de fichiers de sortie dans Azure Storage selon l’ID ou usage de la tâche ou du travail.</span><span class="sxs-lookup"><span data-stu-id="8780b-130">The File Conventions library also provides methods to query output files in Azure Storage according to job ID, task ID, or purpose.</span></span>   

<span data-ttu-id="8780b-131">Si vous développez avec un autre langage que .NET, vous pouvez implémenter le standard de nommage de File Convention dans votre application.</span><span class="sxs-lookup"><span data-stu-id="8780b-131">If you are developing with a language other than .NET, you can implement the File Conventions standard yourself in your application.</span></span> <span data-ttu-id="8780b-132">Pour en savoir plus, consultez l’article [À propos du standard de nommage des fichiers Batch dans File Conventions](batch-task-output.md#about-the-batch-file-conventions-standard).</span><span class="sxs-lookup"><span data-stu-id="8780b-132">For more information, see [About the Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span></span>

## <a name="link-an-azure-storage-account-to-your-batch-account"></a><span data-ttu-id="8780b-133">Lier un compte Azure Storage à votre compte Batch</span><span class="sxs-lookup"><span data-stu-id="8780b-133">Link an Azure Storage account to your Batch account</span></span>

<span data-ttu-id="8780b-134">Pour conserver les données de sortie dans Azure Storage à l’aide de la bibliothèque File Conventions, vous devez d’abord lier un compte Azure Storage à votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="8780b-134">To persist output data to Azure Storage using the File Conventions library, you must first link an Azure Storage account to your Batch account.</span></span> <span data-ttu-id="8780b-135">Si ce n’est déjà fait, liez un compte Storage à votre compte Batch à l’aide du [portail Azure](https://portal.azure.com) :</span><span class="sxs-lookup"><span data-stu-id="8780b-135">If you haven't done so already, link a Storage account to your Batch account by using the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="8780b-136">Accédez à votre compte Batch dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8780b-136">Navigate to your Batch account in the Azure portal.</span></span> 
2. <span data-ttu-id="8780b-137">Sous **Paramètres**, sélectionnez **Compte Storage**.</span><span class="sxs-lookup"><span data-stu-id="8780b-137">Under **Settings**, select **Storage Account**.</span></span>
3. <span data-ttu-id="8780b-138">Si vous n’avez pas déjà associé de compte Storage à votre compte Batch, cliquez sur **Compte Storage (aucun)**.</span><span class="sxs-lookup"><span data-stu-id="8780b-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span></span>
4. <span data-ttu-id="8780b-139">Sélectionnez un compte Storage pour votre abonnement dans la liste.</span><span class="sxs-lookup"><span data-stu-id="8780b-139">Select a Storage account from the list for your subscription.</span></span> <span data-ttu-id="8780b-140">Pour de meilleures performances, utilisez un compte Azure Storage qui se trouve dans la même région que le compte Batch où les tâches sont exécutées.</span><span class="sxs-lookup"><span data-stu-id="8780b-140">For best performance, use an Azure Storage account that is in the same region as the Batch account where your tasks are running.</span></span>

## <a name="persist-output-data"></a><span data-ttu-id="8780b-141">Conserver les données de sortie</span><span class="sxs-lookup"><span data-stu-id="8780b-141">Persist output data</span></span>

<span data-ttu-id="8780b-142">Pour conserver les données de sortie de travail et de tâche avec la bibliothèque File Conventions, créez un conteneur dans Azure Storage, puis enregistrez la sortie dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="8780b-142">To persist job and task output data with the File Conventions library, create a container in Azure Storage, then save the output to the container.</span></span> <span data-ttu-id="8780b-143">Utilisez la [bibliothèque du client Azure Storage pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage) dans le code de tâche pour charger la sortie de tâche dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="8780b-143">Use the [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code to upload the task output to the container.</span></span> 

<span data-ttu-id="8780b-144">Pour en savoir plus sur les conteneurs et les objets blob dans Azure Storage, consultez l’article [Prise en main du stockage d’objets blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="8780b-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="8780b-145">Toutes les sorties de travail et de tâche conservées avec la bibliothèque File Conventions sont stockées dans le même conteneur.</span><span class="sxs-lookup"><span data-stu-id="8780b-145">All job and task outputs persisted with the File Conventions library are stored in the same container.</span></span> <span data-ttu-id="8780b-146">Si plusieurs tâches tentent de conserver des fichiers en même temps, des [limitations de stockage](../storage/common/storage-performance-checklist.md#blobs) peuvent être appliquées.</span><span class="sxs-lookup"><span data-stu-id="8780b-146">If a large number of tasks try to persist files at the same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="8780b-147">Créer un conteneur de stockage</span><span class="sxs-lookup"><span data-stu-id="8780b-147">Create storage container</span></span>

<span data-ttu-id="8780b-148">Pour conserver les sorties de tâche dans Azure Storage, créez d’abord un conteneur avec la commande [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span><span class="sxs-lookup"><span data-stu-id="8780b-148">To persist task output to Azure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="8780b-149">Cette méthode d’extension nécessite un objet [CloudStorageAccount] [ net_cloudstorageaccount] comme paramètre.</span><span class="sxs-lookup"><span data-stu-id="8780b-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span></span> <span data-ttu-id="8780b-150">Elle permet de créer un conteneur nommé selon le standard de nommage de File Conventions, afin que son contenu soit détectable par le portail Azure et par les méthodes de récupération présentées dont nous parlerons plus loin.</span><span class="sxs-lookup"><span data-stu-id="8780b-150">It creates a container named according to the File Conventions standard,so that its contents are discoverable by the Azure portal and the retrieval methods discussed later in the article.</span></span>

<span data-ttu-id="8780b-151">En général, vous placez ce code pour créer un conteneur dans votre application cliente &mdash;, qui crée vos pools, travaux et tâches.</span><span class="sxs-lookup"><span data-stu-id="8780b-151">You typically place the code to create a container in your client application &mdash; the application that creates your pools, jobs, and tasks.</span></span>

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference to the linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create the blob storage container for the outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a><span data-ttu-id="8780b-152">Stocker les sorties des tâches</span><span class="sxs-lookup"><span data-stu-id="8780b-152">Store task outputs</span></span>

<span data-ttu-id="8780b-153">Maintenant que vous avez préparé un conteneur dans Azure Storage, les tâches peuvent y enregistrer leur sortie à l’aide de la classe [TaskOutputStorage][net_taskoutputstorage] figurant dans la bibliothèque File Conventions.</span><span class="sxs-lookup"><span data-stu-id="8780b-153">Now that you've prepared a container in Azure Storage, tasks can save output to the container by using the [TaskOutputStorage][net_taskoutputstorage] class found in the File Conventions library.</span></span>

<span data-ttu-id="8780b-154">Dans votre code de tâche, commencez par créer un objet [TaskOutputStorage][net_taskoutputstorage], puis, lorsque la tâche a terminé son travail, appelez la méthode [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] pour enregistrer sa sortie dans le Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8780b-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when the task has completed its work, call the [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method to save its output to Azure Storage.</span></span>

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code to process data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

<span data-ttu-id="8780b-155">Le paramètre `kind` de la méthode [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) permet d’organiser les fichiers conservés.</span><span class="sxs-lookup"><span data-stu-id="8780b-155">The `kind` parameter of the [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes the persisted files.</span></span> <span data-ttu-id="8780b-156">Il existe quatre types prédéfinis [TaskOutputKind][net_taskoutputkind] : `TaskOutput`, `TaskPreview`, `TaskLog`, et `TaskIntermediate.`. Vous pouvez également définir des catégories de sortie personnalisées.</span><span class="sxs-lookup"><span data-stu-id="8780b-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span></span>

<span data-ttu-id="8780b-157">Ces types de sortie vous permettent de spécifier le type de sortie à répertorier lorsque vous interrogez ultérieurement Batch pour connaître les sorties conservées d’une tâche donnée.</span><span class="sxs-lookup"><span data-stu-id="8780b-157">These output types allow you to specify which type of outputs to list when you later query Batch for the persisted outputs of a given task.</span></span> <span data-ttu-id="8780b-158">En d’autres termes, lorsque vous répertoriez les sorties d’une tâche, vous pouvez filtrer la liste sur l’un des types de sortie.</span><span class="sxs-lookup"><span data-stu-id="8780b-158">In other words, when you list the outputs for a task, you can filter the list on one of the output types.</span></span> <span data-ttu-id="8780b-159">Par exemple, « Donnez-moi un *aperçu* de la tâche *109* ».</span><span class="sxs-lookup"><span data-stu-id="8780b-159">For example, "Give me the *preview* output for task *109*."</span></span> <span data-ttu-id="8780b-160">La section [Récupérer la sortie](#retrieve-output) plus loin dans l’article contient plus d’informations sur les listes de sorties et leur récupération.</span><span class="sxs-lookup"><span data-stu-id="8780b-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in the article.</span></span>

> [!TIP]
> <span data-ttu-id="8780b-161">Le type de sortie indique également l’emplacement d’un fichier particulier dans le portail Azure : les fichiers catégorisés par *TaskOutput* sont affichés dans les **fichiers de sortie de tâche** tandis que les fichiers *TaskLog* sont affichés dans les **journaux de tâches**.</span><span class="sxs-lookup"><span data-stu-id="8780b-161">The output kind also determines where in the Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="8780b-162">Stocker les sorties des travaux</span><span class="sxs-lookup"><span data-stu-id="8780b-162">Store job outputs</span></span>

<span data-ttu-id="8780b-163">Outre le stockage des sorties des tâches, vous pouvez stocker les sorties associées à un travail entier.</span><span class="sxs-lookup"><span data-stu-id="8780b-163">In addition to storing task outputs, you can store the outputs associated with an entire job.</span></span> <span data-ttu-id="8780b-164">Par exemple, dans la tâche de fusion d’un travail de rendu de film, vous pouvez conserver le film intégralement rendu sous forme de sortie de travail.</span><span class="sxs-lookup"><span data-stu-id="8780b-164">For example, in the merge task of a movie rendering job, you could persist the fully rendered movie as a job output.</span></span> <span data-ttu-id="8780b-165">Lorsque votre travail est terminé, votre application cliente peut répertorier et récupérer les sorties du travail, sans devoir interroger les tâches individuelles.</span><span class="sxs-lookup"><span data-stu-id="8780b-165">When your job is completed, your client application can list and retrieve the outputs for the job, and does not need to query the individual tasks.</span></span>

<span data-ttu-id="8780b-166">Stockez la sortie du travail en appelant la méthode [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] et spécifiez le paramètre [JobOutputKind][net_joboutputkind] et le nom de fichier :</span><span class="sxs-lookup"><span data-stu-id="8780b-166">Store job output by calling the [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify the [JobOutputKind][net_joboutputkind] and filename:</span></span>

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="8780b-167">Comme avec le type **TaskOutputKind** pour les sorties des tâches, vous pouvez utiliser le type [JobOutputKind][net_joboutputkind] pour catégoriser les fichiers conservés d’un travail.</span><span class="sxs-lookup"><span data-stu-id="8780b-167">As with the **TaskOutputKind** type for task outputs, you use the [JobOutputKind][net_joboutputkind] type to categorize a job's persisted files.</span></span> <span data-ttu-id="8780b-168">Ce paramètre vous permet d’interroger (répertorier) ultérieurement un type spécifique de sortie.</span><span class="sxs-lookup"><span data-stu-id="8780b-168">This parameter allows you to later query for (list) a specific type of output.</span></span> <span data-ttu-id="8780b-169">Le type **JobOutputKind** inclut les catégories de sortie et d’aperçu, et prend en charge la création de catégories personnalisées.</span><span class="sxs-lookup"><span data-stu-id="8780b-169">The **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="8780b-170">Stocker les journaux de tâches</span><span class="sxs-lookup"><span data-stu-id="8780b-170">Store task logs</span></span>

<span data-ttu-id="8780b-171">En plus de conserver un fichier dans un espace de stockage durable à l’issue d’une tâche ou d’un travail, vous pouvez avoir besoin de conserver les fichiers mis à jour pendant l’exécution d’une tâche, par exemple les fichiers journaux &mdash; ou `stdout.txt` et `stderr.txt`.</span><span class="sxs-lookup"><span data-stu-id="8780b-171">In addition to persisting a file to durable storage when a task or job completes, you may need to persist files that are updated during the execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="8780b-172">À cet effet, la bibliothèque Azure Batch File Conventions fournit la méthode [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="8780b-172">For this purpose, the Azure Batch File Conventions library provides the [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="8780b-173">Avec [SaveTrackedAsync][net_savetrackedasync], vous pouvez effectuer le suivi des mises à jour apportées à un fichier sur le nœud (à un intervalle que vous définissez) et conserver ces mises à jour dans le Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="8780b-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates to a file on the node (at an interval that you specify) and persist those updates to Azure Storage.</span></span>

<span data-ttu-id="8780b-174">Dans l’extrait de code suivant, nous utilisons [SaveTrackedAsync][net_savetrackedasync] pour mettre à jour `stdout.txt` dans le Stockage Azure toutes les 15 secondes pendant l’exécution de la tâche :</span><span class="sxs-lookup"><span data-stu-id="8780b-174">In the following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] to update `stdout.txt` in Azure Storage every 15 seconds during the execution of the task:</span></span>

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// The primary task logic is wrapped in a using statement that sends updates to
// the stdout.txt blob in Storage every 15 seconds while the task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code to process data and produce output file(s) */

    // We are tracking the disk file to save our standard output, but the
    // node agent may take up to 3 seconds to flush the stdout stream to
    // disk. So give the file a moment to catch up.
     await Task.Delay(stdoutFlushDelay);
}
```

<span data-ttu-id="8780b-175">La section commentée `Code to process data and produce output file(s)` est un espace réservé pour le code que votre tâche exécuterait normalement.</span><span class="sxs-lookup"><span data-stu-id="8780b-175">The commented section `Code to process data and produce output file(s)` is a placeholder for the code that your task would normally perform.</span></span> <span data-ttu-id="8780b-176">Par exemple, vous pouvez insérer un code qui télécharge des données à partir d’Azure Storage et effectue sur celles-ci des transformations ou des calculs.</span><span class="sxs-lookup"><span data-stu-id="8780b-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="8780b-177">La partie importante de cet extrait de code montre comment encapsuler un tel code dans un bloc `using` pour mettre régulièrement à jour un fichier avec [SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="8780b-177">The important part of this snippet is demonstrating how you can wrap such code in a `using` block to periodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="8780b-178">L’agent de nœud est un programme qui s’exécute sur chaque nœud dans le pool et fournit l’interface de commande et de contrôle entre le nœud et le service Batch.</span><span class="sxs-lookup"><span data-stu-id="8780b-178">The node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service.</span></span> <span data-ttu-id="8780b-179">L’appel `Task.Delay` est nécessaire à la fin de ce bloc `using` pour garantir que l’agent de nœud a le temps de vider le contenu du standard dans le fichier stdout.txt du nœud.</span><span class="sxs-lookup"><span data-stu-id="8780b-179">The `Task.Delay` call is required at the end of this `using` block to ensure that the node agent has time to flush the contents of standard out to the stdout.txt file on the node.</span></span> <span data-ttu-id="8780b-180">Sans ce délai, il est possible de manquer les dernières secondes de la sortie.</span><span class="sxs-lookup"><span data-stu-id="8780b-180">Without this delay, it is possible to miss the last few seconds of output.</span></span> <span data-ttu-id="8780b-181">Ce délai n’est pas forcément requis pour tous les fichiers.</span><span class="sxs-lookup"><span data-stu-id="8780b-181">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="8780b-182">Lorsque vous activez le suivi des fichiers avec **SaveTrackedAsync**, seuls les *ajouts* apportés au fichier suivi sont conservés dans Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8780b-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* to the tracked file are persisted to Azure Storage.</span></span> <span data-ttu-id="8780b-183">Utilisez cette méthode uniquement pour le suivi des fichiers journaux sans rotation ou des autres fichiers qui sont rédigés avec des opérations d’ajout à la fin du fichier.</span><span class="sxs-lookup"><span data-stu-id="8780b-183">Use this method only for tracking non-rotating log files or other files that are written to with append operations to the end of the file.</span></span>
> 
> 

## <a name="retrieve-output-data"></a><span data-ttu-id="8780b-184">Récupérer les données de sortie</span><span class="sxs-lookup"><span data-stu-id="8780b-184">Retrieve output data</span></span>

<span data-ttu-id="8780b-185">Lorsque vous récupérez votre sortie conservée à l’aide de la bibliothèque Azure Batch File Conventions, vous procédez d’une façon centrée sur les travaux et les tâches.</span><span class="sxs-lookup"><span data-stu-id="8780b-185">When you retrieve your persisted output using the Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="8780b-186">Vous pouvez demander la sortie d’une tâche ou d’un travail donné sans avoir à connaître son chemin d’accès dans Azure Storage ni même son nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="8780b-186">You can request the output for given task or job without needing to know its path in Azure Storage, or even its file name.</span></span> <span data-ttu-id="8780b-187">À la place, vous pouvez effectuer des requêtes de fichiers de sortie par ID de tâche ou travail.</span><span class="sxs-lookup"><span data-stu-id="8780b-187">Instead, you can request output files by task or job ID.</span></span>

<span data-ttu-id="8780b-188">L’extrait de code suivant itère les tâches d’un travail, imprime des informations sur les fichiers de sortie de tâche, puis télécharge les fichiers à partir d’Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8780b-188">The following code snippet iterates through a job's tasks, prints some information about the output files for the task, and then downloads its files from Storage.</span></span>

```csharp
foreach (CloudTask task in myJob.ListTasks())
{
    foreach (OutputFileReference output in
        task.OutputStorage(storageAccount).ListOutputs(
            TaskOutputKind.TaskOutput))
    {
        Console.WriteLine($"output file: {output.FilePath}");

        output.DownloadToFileAsync(
            $"{jobId}-{output.FilePath}",
            System.IO.FileMode.Create).Wait();
    }
}
```

## <a name="view-output-files-in-the-azure-portal"></a><span data-ttu-id="8780b-189">Afficher les fichiers de sortie dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="8780b-189">View output files in the Azure portal</span></span>

<span data-ttu-id="8780b-190">Le portail Azure affiche les fichiers de sortie de tâches et les journaux qui sont conservés dans un compte Azure Storage lié à l’aide du [standard de nommage des fichiers Batch dans File Conventions](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span><span class="sxs-lookup"><span data-stu-id="8780b-190">The Azure portal displays task output files and logs that are persisted to a linked Azure Storage account using the [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="8780b-191">Vous pouvez implémenter ces conventions vous-même dans le langage de votre choix ou utiliser la bibliothèque File Conventions dans vos applications .NET.</span><span class="sxs-lookup"><span data-stu-id="8780b-191">You can implement these conventions yourself in the a language of your choice, or you can use the File Conventions library in your .NET applications.</span></span>

<span data-ttu-id="8780b-192">Pour activer l’affichage de vos fichiers de sortie dans le portail, vous devez respecter les exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="8780b-192">To enable the display of your output files in the portal, you must satisfy the following requirements:</span></span>

1. <span data-ttu-id="8780b-193">[Liez un compte Azure Storage](#requirement-linked-storage-account) à votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="8780b-193">[Link an Azure Storage account](#requirement-linked-storage-account) to your Batch account.</span></span>
2. <span data-ttu-id="8780b-194">Respectez les conventions d’affectation de noms prédéfinies pour les conteneurs de stockage et les fichiers lors de la conservation des sorties.</span><span class="sxs-lookup"><span data-stu-id="8780b-194">Adhere to the predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="8780b-195">Vous trouverez la définition de ces conventions dans le fichier [LISEZMOI][github_file_conventions_readme] de la bibliothèque File Conventions.</span><span class="sxs-lookup"><span data-stu-id="8780b-195">You can find the definition of these conventions in the File Conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="8780b-196">Si vous utilisez la bibliothèque [Azure Batch File Conventions] [ nuget_package] pour conserver vos sorties, vos fichiers sont conservés selon le standard de nommage de File Conventions.</span><span class="sxs-lookup"><span data-stu-id="8780b-196">If you use the [Azure Batch File Conventions][nuget_package] library to persist your output, your files are persisted according to the File Conventions standard.</span></span>

<span data-ttu-id="8780b-197">Pour afficher les fichiers de sortie de tâches et les journaux dans le portail Azure, accédez à la tâche dont la sortie vous intéresse, puis cliquez sur **Fichiers de sortie enregistrés** ou **Journaux enregistrés**.</span><span class="sxs-lookup"><span data-stu-id="8780b-197">To view task output files and logs in the Azure portal, navigate to the task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="8780b-198">Cette image affiche l’écran **Saved output files (Fichiers de sortie enregistrés)** pour la tâche pourvue de l’ID « 007 » :</span><span class="sxs-lookup"><span data-stu-id="8780b-198">This image shows the **Saved output files** for the task with ID "007":</span></span>

<span data-ttu-id="8780b-199">![Panneau des sorties des tâches dans le Portail Azure][2]</span><span class="sxs-lookup"><span data-stu-id="8780b-199">![Task outputs blade in the Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="8780b-200">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="8780b-200">Code sample</span></span>

<span data-ttu-id="8780b-201">L’exemple de projet [PersistOutputs][github_persistoutputs] est l’un des [exemples de code Azure Batch][github_samples] disponibles sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="8780b-201">The [PersistOutputs][github_persistoutputs] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="8780b-202">Cette solution Visual Studio montre comment utiliser la bibliothèque Azure Batch File Conventions pour conserver une sortie de tâche dans l’espace de stockage durable.</span><span class="sxs-lookup"><span data-stu-id="8780b-202">This Visual Studio solution demonstrates how to use the Azure Batch File Conventions library to persist task output to durable storage.</span></span> <span data-ttu-id="8780b-203">Pour exécuter l’exemple, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="8780b-203">To run the sample, follow these steps:</span></span>

1. <span data-ttu-id="8780b-204">Ouvrez le projet dans **Visual Studio 2015 ou version ultérieure**.</span><span class="sxs-lookup"><span data-stu-id="8780b-204">Open the project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="8780b-205">Ajoutez vos **informations d’identification de compte** Batch et Stockage à **AccountSettings.settings** dans le projet Microsoft.Azure.Batch.Samples.Common.</span><span class="sxs-lookup"><span data-stu-id="8780b-205">Add your Batch and Storage **account credentials** to **AccountSettings.settings** in the Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="8780b-206">**Générez** la solution sans l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="8780b-206">**Build** (but do not run) the solution.</span></span> <span data-ttu-id="8780b-207">Restaurez les packages NuGet si vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="8780b-207">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="8780b-208">Utilisez le portail Azure pour charger un [package d’application](batch-application-packages.md) pour **PersistOutputsTask**.</span><span class="sxs-lookup"><span data-stu-id="8780b-208">Use the Azure portal to upload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="8780b-209">Insérez le fichier `PersistOutputsTask.exe` et ses assemblys dépendants dans le package .zip, puis définissez l’ID de l’application sur PersistOutputsTask et la version du package d’application sur 1.0.</span><span class="sxs-lookup"><span data-stu-id="8780b-209">Include the `PersistOutputsTask.exe` and its dependent assemblies in the .zip package, set the application ID to "PersistOutputsTask", and the application package version to "1.0".</span></span>
5. <span data-ttu-id="8780b-210">**Démarrez** (exécutez) le projet **PersistOutputs**.</span><span class="sxs-lookup"><span data-stu-id="8780b-210">**Start** (run) the **PersistOutputs** project.</span></span>
6. <span data-ttu-id="8780b-211">Quand vous êtes invité à choisir la technologie de persistance à utiliser pour l’exécution de l’exemple, entrez **1** pour exécuter l’exemple à l’aide de la bibliothèque File Conventions pour conserver les sorties de tâche.</span><span class="sxs-lookup"><span data-stu-id="8780b-211">When prompted to choose the persistence technology to use for running the sample, enter **1** to run the sample using the File Conventions library to persist task output.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8780b-212">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8780b-212">Next steps</span></span>

### <a name="get-the-batch-file-conventions-library-for-net"></a><span data-ttu-id="8780b-213">Obtenir la bibliothèque Batch File Conventions pour .NET</span><span class="sxs-lookup"><span data-stu-id="8780b-213">Get the Batch File Conventions library for .NET</span></span>

<span data-ttu-id="8780b-214">La bibliothèque Batch File Conventions pour .NET est disponible sur [NuGet][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="8780b-214">The Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span></span> <span data-ttu-id="8780b-215">La bibliothèque développe les classes [CloudJob][net_cloudjob] et [CloudTask][net_cloudtask] avec de nouvelles méthodes.</span><span class="sxs-lookup"><span data-stu-id="8780b-215">The library extends the [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span></span> <span data-ttu-id="8780b-216">Consultez également la [documentation de référence](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) pour la bibliothèque File Conventions.</span><span class="sxs-lookup"><span data-stu-id="8780b-216">Also see the [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for the File Conventions library.</span></span>

<span data-ttu-id="8780b-217">Le [code source][github_file_conventions] de la bibliothèque File Conventions est disponible sur GitHub dans le Kit de développement logiciel (SDK) Microsoft Azure pour le référentiel .NET.</span><span class="sxs-lookup"><span data-stu-id="8780b-217">The [source code][github_file_conventions] for the File Conventions library is available on GitHub in the Microsoft Azure SDK for .NET repository.</span></span> 

### <a name="explore-other-approaches-for-persisting-output-data"></a><span data-ttu-id="8780b-218">Explorer d’autres approches de conservation des données de sortie</span><span class="sxs-lookup"><span data-stu-id="8780b-218">Explore other approaches for persisting output data</span></span>

- <span data-ttu-id="8780b-219">Consultez l’article [Conserver les sorties de travaux et tâches terminés dans Azure Storage](batch-task-output.md) pour une vue d’ensemble de la conservation des données de tâche et de travail.</span><span class="sxs-lookup"><span data-stu-id="8780b-219">See [Persist job and task output to Azure Storage](batch-task-output.md) for an overview of persisting task and job data.</span></span>
- <span data-ttu-id="8780b-220">Consultez [Conserver les données de tâche dans le Stockage Azure à l’aide de l’API du service Batch](batch-task-output-files.md) pour savoir comment utiliser l’API du service Batch pour conserver des données de sortie.</span><span class="sxs-lookup"><span data-stu-id="8780b-220">See [Persist task data to Azure Storage with the Batch service API](batch-task-output-files.md) to learn how to use the Batch service API to persist output data.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_file_conventions]: https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Batch/FileConventions
[github_file_conventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_fileconventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[net_joboutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputkind.aspx
[net_joboutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.aspx
[net_joboutputstorage_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.saveasync.aspx
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_prepareoutputasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.cloudjobextensions.prepareoutputstorageasync.aspx
[net_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx
[net_savetrackedasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.savetrackedasync.aspx
[net_taskoutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputkind.aspx
[net_taskoutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx
[nuget_manager]: https://docs.nuget.org/consume/installing-nuget
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/

[1]: ./media/batch-task-output/task-output-01.png "Sélecteurs Saved output files (Fichiers de sortie enregistrés) et Fichiers enregistrés dans le portail"
[2]: ./media/batch-task-output/task-output-02.png "Panneau des sorties des tâches dans le Portail Azure"
