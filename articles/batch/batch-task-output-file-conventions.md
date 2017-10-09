---
title: "aaaPersist projet et la tâche de sortie tooAzure stockage avec la bibliothèque de Conventions pour les fichiers hello pour .NET - Azure Batch | Documents Microsoft"
description: "Découvrez comment toouse bibliothèque de Conventions pour les fichiers par lots Azure pour .NET toopersist tâche de traitement par lots et tooAzure de sortie de travail stockage et vue Bonjour persistant sortie Bonjour portail Azure."
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
ms.openlocfilehash: cf2ac8632a13d32438c1bdcf11b4b9649de1e2b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a><span data-ttu-id="db7f6-103">Conserver le travail et les données tooAzure stockage avec bibliothèque de Conventions pour les fichiers Batch hello pour .NET toopersist de tâches</span><span class="sxs-lookup"><span data-stu-id="db7f6-103">Persist job and task data tooAzure Storage with hello Batch File Conventions library for .NET toopersist</span></span> 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="db7f6-104">Une façon toopersist des données de tâche sont toouse hello [bibliothèque Conventions pour les fichiers par lots Azure pour .NET][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="db7f6-104">One way toopersist task data is toouse hello [Azure Batch File Conventions library for .NET][nuget_package].</span></span> <span data-ttu-id="db7f6-105">bibliothèque de Conventions pour les fichiers Hello simplifie les processus de hello de stocker le résultat de la tâche données tooAzure stockage et la récupération.</span><span class="sxs-lookup"><span data-stu-id="db7f6-105">hello File Conventions library simplifies hello process of storing task output data tooAzure Storage and retrieving it.</span></span> <span data-ttu-id="db7f6-106">Vous pouvez utiliser la bibliothèque de Conventions pour les fichiers de hello dans du code de tâche et le client &mdash; dans le code de tâche pour les fichiers de persistance et client toolist de code et de les récupérer.</span><span class="sxs-lookup"><span data-stu-id="db7f6-106">You can use hello File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code toolist and retrieve them.</span></span> <span data-ttu-id="db7f6-107">Votre code de tâche également utiliser hello bibliothèque tooretrieve hello sortie de tâches en amont, comme dans un [interdépendances](batch-task-dependencies.md) scénario.</span><span class="sxs-lookup"><span data-stu-id="db7f6-107">Your task code can also use hello library tooretrieve hello output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span> 

<span data-ttu-id="db7f6-108">les fichiers de bibliothèque de Conventions pour les fichiers hello en sortie tooretrieve, vous pouvez localiser les fichiers hello pour un travail donné ou une tâche en les répertoriant par ID et l’objectif.</span><span class="sxs-lookup"><span data-stu-id="db7f6-108">tooretrieve output files with hello File Conventions library, you can locate hello files for a given job or task by listing them by ID and purpose.</span></span> <span data-ttu-id="db7f6-109">Vous n’avez pas besoin les noms hello tooknow ou des emplacements de fichiers de hello.</span><span class="sxs-lookup"><span data-stu-id="db7f6-109">You don't need tooknow hello names or locations of hello files.</span></span> <span data-ttu-id="db7f6-110">Par exemple, vous pouvez utiliser toolist de hello Conventions pour les fichiers bibliothèque tous les fichiers intermédiaires pour une tâche donnée, ou obtenir un aperçu de fichier pour un travail donné.</span><span class="sxs-lookup"><span data-stu-id="db7f6-110">For example, you can use hello File Conventions library toolist all intermediate files for a given task, or get a preview file for a given job.</span></span>

> [!TIP]
> <span data-ttu-id="db7f6-111">Depuis la version 2017-05-01, hello API de service de traitement par lots prend en charge la persistance tooAzure de données de sortie stockage pour les tâches et le Gestionnaire des tâches qui s’exécutent sur des pools créés avec la configuration d’ordinateur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="db7f6-111">Starting with version 2017-05-01, hello Batch service API supports persisting output data tooAzure Storage for tasks and job manager tasks that run on pools created with hello virtual machine configuration.</span></span> <span data-ttu-id="db7f6-112">Hello API de service de traitement par lots fournit un toopersist moyen simple de sortie à partir de code hello qui crée une tâche et est considérée comme une bibliothèque de Conventions pour les fichiers toohello autre.</span><span class="sxs-lookup"><span data-stu-id="db7f6-112">hello Batch service API provides a simple way toopersist output from within hello code that creates a task and serves as an alternative toohello File Conventions library.</span></span> <span data-ttu-id="db7f6-113">Vous pouvez modifier votre sortie toopersist de lot client applications sans avoir besoin d’application hello tooupdate votre tâche est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="db7f6-113">You can modify your Batch client applications toopersist output without needing tooupdate hello application that your task is running.</span></span> <span data-ttu-id="db7f6-114">Pour plus d’informations, consultez [conserver des tâches données tooAzure stockage avec hello API de lot](batch-task-output-files.md).</span><span class="sxs-lookup"><span data-stu-id="db7f6-114">For more information, see [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md).</span></span>
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a><span data-ttu-id="db7f6-115">Quand utiliser le résultat de la tâche hello Conventions pour les fichiers bibliothèque toopersist ?</span><span class="sxs-lookup"><span data-stu-id="db7f6-115">When do I use hello File Conventions library toopersist task output?</span></span>

<span data-ttu-id="db7f6-116">Traitement par lots Azure fournit plusieurs méthodes toopersist sortie de la tâche.</span><span class="sxs-lookup"><span data-stu-id="db7f6-116">Azure Batch provides more than one way toopersist task output.</span></span> <span data-ttu-id="db7f6-117">Hello Conventions pour les fichiers est meilleure que des scénarios toothese adaptée :</span><span class="sxs-lookup"><span data-stu-id="db7f6-117">hello File Conventions is best suited toothese scenarios:</span></span>

- <span data-ttu-id="db7f6-118">Vous pouvez facilement modifier le code hello pour application hello que votre tâche est en cours d’exécution toopersist les fichiers à l’aide de la bibliothèque de Conventions pour les fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="db7f6-118">You can easily modify hello code for hello application that your task is running toopersist files using hello File Conventions library.</span></span>
- <span data-ttu-id="db7f6-119">Vous souhaitez toostream données tooAzure stockage alors que la tâche hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="db7f6-119">You want toostream data tooAzure Storage while hello task is still running.</span></span>
- <span data-ttu-id="db7f6-120">Vous souhaitez que les données de toopersist à partir des pools créés avec la configuration du service cloud hello ou de configuration d’ordinateur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="db7f6-120">You want toopersist data from pools created with either hello cloud service configuration or hello virtual machine configuration.</span></span>
- <span data-ttu-id="db7f6-121">Votre application cliente ou autres tâches dans hello toolocate des besoins de la tâche et téléchargement les fichiers de sortie de tâche par ID ou de leur rôle.</span><span class="sxs-lookup"><span data-stu-id="db7f6-121">Your client application or other tasks in hello job needs toolocate and download task output files by ID or by purpose.</span></span> 
- <span data-ttu-id="db7f6-122">Vous souhaitez obtenir une sortie tâche tooview hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="db7f6-122">You want tooview task output in hello Azure portal.</span></span>

<span data-ttu-id="db7f6-123">Si votre scénario diffère de celles répertoriées ci-dessus, vous devrez peut-être tooconsider une approche différente.</span><span class="sxs-lookup"><span data-stu-id="db7f6-123">If your scenario differs from those listed above, you may need tooconsider a different approach.</span></span> <span data-ttu-id="db7f6-124">Pour plus d’informations sur les autres options pour la sortie de tâche persistantes, consultez [tooAzure stockage de sortie de projet de la persistance et la tâche](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="db7f6-124">For more information on other options for persisting task output, see [Persist job and task output tooAzure Storage](batch-task-output.md).</span></span> 

## <a name="what-is-hello-batch-file-conventions-standard"></a><span data-ttu-id="db7f6-125">Nouveautés hello Conventions pour les fichiers Batch standard</span><span class="sxs-lookup"><span data-stu-id="db7f6-125">What is hello Batch File Conventions standard?</span></span>

<span data-ttu-id="db7f6-126">Hello [standard de Conventions pour les fichiers Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) fournit un schéma d’affectation de noms pour les conteneurs de destination hello et toowhich de chemins d’accès d’objet blob vos fichiers de sortie sont écrites.</span><span class="sxs-lookup"><span data-stu-id="db7f6-126">hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for hello destination containers and blob paths toowhich your output files are written.</span></span> <span data-ttu-id="db7f6-127">TooAzure de fichiers persistant stockage qui adhèrent toohello Conventions standard pour les fichiers sont automatiquement disponibles pour l’affichage dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="db7f6-127">Files persisted tooAzure Storage that adhere toohello File Conventions standard are automatically available for viewing in hello Azure portal.</span></span> <span data-ttu-id="db7f6-128">portail de Hello tient compte de la convention d’affectation de noms de hello et peut donc afficher des fichiers respectent tooit.</span><span class="sxs-lookup"><span data-stu-id="db7f6-128">hello portal is aware of hello naming convention and so can display files that adhere tooit.</span></span>

<span data-ttu-id="db7f6-129">bibliothèque de Conventions pour les fichiers Hello pour .NET nomme automatiquement vos conteneurs de stockage et les fichiers de sortie de tâche en fonction de toohello Conventions standard pour les fichiers.</span><span class="sxs-lookup"><span data-stu-id="db7f6-129">hello File Conventions library for .NET automatically names your storage containers and task output files according toohello File Conventions standard.</span></span> <span data-ttu-id="db7f6-130">bibliothèque de Conventions pour les fichiers Hello fournit également des fichiers de sortie tooquery de méthodes dans le stockage Azure selon toojob ID, ID de tâche ou objectif.</span><span class="sxs-lookup"><span data-stu-id="db7f6-130">hello File Conventions library also provides methods tooquery output files in Azure Storage according toojob ID, task ID, or purpose.</span></span>   

<span data-ttu-id="db7f6-131">Si vous développez avec une langue autre que .NET, vous pouvez implémenter standard de Conventions pour les fichiers hello vous-même dans votre application.</span><span class="sxs-lookup"><span data-stu-id="db7f6-131">If you are developing with a language other than .NET, you can implement hello File Conventions standard yourself in your application.</span></span> <span data-ttu-id="db7f6-132">Pour plus d’informations, consultez [sur standard de Conventions pour les fichiers Batch hello](batch-task-output.md#about-the-batch-file-conventions-standard).</span><span class="sxs-lookup"><span data-stu-id="db7f6-132">For more information, see [About hello Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span></span>

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a><span data-ttu-id="db7f6-133">Lier un tooyour de compte de stockage Azure du compte Batch</span><span class="sxs-lookup"><span data-stu-id="db7f6-133">Link an Azure Storage account tooyour Batch account</span></span>

<span data-ttu-id="db7f6-134">toopersist tooAzure de données de sortie stockage à l’aide de la bibliothèque de Conventions pour les fichiers hello, vous devez d’abord lier un tooyour de compte de stockage Azure du compte Batch.</span><span class="sxs-lookup"><span data-stu-id="db7f6-134">toopersist output data tooAzure Storage using hello File Conventions library, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="db7f6-135">Si vous n’avez pas déjà fait, lier un tooyour de compte de stockage du compte Batch à l’aide de hello [portail Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="db7f6-135">If you haven't done so already, link a Storage account tooyour Batch account by using hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="db7f6-136">Accédez à tooyour du compte Batch Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="db7f6-136">Navigate tooyour Batch account in hello Azure portal.</span></span> 
2. <span data-ttu-id="db7f6-137">Sous **Paramètres**, sélectionnez **Compte Storage**.</span><span class="sxs-lookup"><span data-stu-id="db7f6-137">Under **Settings**, select **Storage Account**.</span></span>
3. <span data-ttu-id="db7f6-138">Si vous n’avez pas déjà associé de compte Storage à votre compte Batch, cliquez sur **Compte Storage (aucun)**.</span><span class="sxs-lookup"><span data-stu-id="db7f6-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span></span>
4. <span data-ttu-id="db7f6-139">Sélectionnez un compte de stockage à partir de la liste de hello pour votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="db7f6-139">Select a Storage account from hello list for your subscription.</span></span> <span data-ttu-id="db7f6-140">Pour de meilleures performances, utilisez un compte de stockage Azure qui se trouve dans hello même région que hello compte Batch en exécutant des tâches.</span><span class="sxs-lookup"><span data-stu-id="db7f6-140">For best performance, use an Azure Storage account that is in hello same region as hello Batch account where your tasks are running.</span></span>

## <a name="persist-output-data"></a><span data-ttu-id="db7f6-141">Conserver les données de sortie</span><span class="sxs-lookup"><span data-stu-id="db7f6-141">Persist output data</span></span>

<span data-ttu-id="db7f6-142">tâche toopersist travail sortie des données avec la bibliothèque de Conventions pour les fichiers hello, créer un conteneur dans le stockage Azure, puis enregistrer le conteneur de toohello sortie hello.</span><span class="sxs-lookup"><span data-stu-id="db7f6-142">toopersist job and task output data with hello File Conventions library, create a container in Azure Storage, then save hello output toohello container.</span></span> <span data-ttu-id="db7f6-143">Hello d’utilisation [bibliothèque cliente de stockage Azure pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage) dans votre conteneur toohello de sortie de tâche tâche code tooupload hello.</span><span class="sxs-lookup"><span data-stu-id="db7f6-143">Use hello [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code tooupload hello task output toohello container.</span></span> 

<span data-ttu-id="db7f6-144">Pour en savoir plus sur les conteneurs et les objets blob dans Azure Storage, consultez l’article [Prise en main du stockage d’objets blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="db7f6-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="db7f6-145">Toutes les sorties de projet et la tâche persistant avec hello Conventions pour les fichiers bibliothèque sont stockés dans hello même conteneur.</span><span class="sxs-lookup"><span data-stu-id="db7f6-145">All job and task outputs persisted with hello File Conventions library are stored in hello same container.</span></span> <span data-ttu-id="db7f6-146">Si un grand nombre de tâches essaient toopersist les fichiers à hello même moment, [limites de stockage](../storage/common/storage-performance-checklist.md#blobs) peut être appliquée.</span><span class="sxs-lookup"><span data-stu-id="db7f6-146">If a large number of tasks try toopersist files at hello same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="db7f6-147">Créer un conteneur de stockage</span><span class="sxs-lookup"><span data-stu-id="db7f6-147">Create storage container</span></span>

<span data-ttu-id="db7f6-148">tooAzure de sortie de tâche toopersist stockage, d’abord créer un conteneur en appelant [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync].</span><span class="sxs-lookup"><span data-stu-id="db7f6-148">toopersist task output tooAzure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="db7f6-149">Cette méthode d’extension nécessite un objet [CloudStorageAccount] [ net_cloudstorageaccount] comme paramètre.</span><span class="sxs-lookup"><span data-stu-id="db7f6-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span></span> <span data-ttu-id="db7f6-150">Il crée un conteneur nommé conséquente toohello Conventions pour les fichiers standard, afin que son contenu est détectable par hello Azure méthodes de récupération de portail et hello présentés plus loin dans l’article de hello.</span><span class="sxs-lookup"><span data-stu-id="db7f6-150">It creates a container named according toohello File Conventions standard,so that its contents are discoverable by hello Azure portal and hello retrieval methods discussed later in hello article.</span></span>

<span data-ttu-id="db7f6-151">En règle générale, vous placez toocreate de code hello un conteneur dans votre application cliente &mdash; hello application qui crée des pools, des tâches et des tâches.</span><span class="sxs-lookup"><span data-stu-id="db7f6-151">You typically place hello code toocreate a container in your client application &mdash; hello application that creates your pools, jobs, and tasks.</span></span>

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference toohello linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create hello blob storage container for hello outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a><span data-ttu-id="db7f6-152">Stocker les sorties des tâches</span><span class="sxs-lookup"><span data-stu-id="db7f6-152">Store task outputs</span></span>

<span data-ttu-id="db7f6-153">Maintenant que vous avez préparé un conteneur dans le stockage Azure, les tâches peuvent enregistrer conteneur toohello de sortie à l’aide de hello [TaskOutputStorage] [ net_taskoutputstorage] classe trouvé dans la bibliothèque de Conventions pour les fichiers de hello.</span><span class="sxs-lookup"><span data-stu-id="db7f6-153">Now that you've prepared a container in Azure Storage, tasks can save output toohello container by using hello [TaskOutputStorage][net_taskoutputstorage] class found in hello File Conventions library.</span></span>

<span data-ttu-id="db7f6-154">Dans votre code de tâche, commencez par créer un [TaskOutputStorage] [ net_taskoutputstorage] de l’objet, puis lors de la tâche hello a terminé son travail, appelez hello [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] méthode toosave son tooAzure sortie stockage.</span><span class="sxs-lookup"><span data-stu-id="db7f6-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when hello task has completed its work, call hello [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method toosave its output tooAzure Storage.</span></span>

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code tooprocess data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

<span data-ttu-id="db7f6-155">Hello `kind` paramètre Hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) méthode catégorise hello persistante des fichiers.</span><span class="sxs-lookup"><span data-stu-id="db7f6-155">hello `kind` parameter of hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes hello persisted files.</span></span> <span data-ttu-id="db7f6-156">Il existe quatre types prédéfinis [TaskOutputKind][net_taskoutputkind] : `TaskOutput`, `TaskPreview`, `TaskLog`, et `TaskIntermediate.`. Vous pouvez également définir des catégories de sortie personnalisées.</span><span class="sxs-lookup"><span data-stu-id="db7f6-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span></span>

<span data-ttu-id="db7f6-157">Ces types de sortie permettent de toospecify le type de sorties toolist lorsque vous interrogez ultérieurement par lots pour hello persistante des sorties d’une tâche donnée.</span><span class="sxs-lookup"><span data-stu-id="db7f6-157">These output types allow you toospecify which type of outputs toolist when you later query Batch for hello persisted outputs of a given task.</span></span> <span data-ttu-id="db7f6-158">En d’autres termes, lorsque vous répertoriez les sorties hello pour une tâche, vous pouvez filtrer la liste hello sur l’un des types de sorties hello.</span><span class="sxs-lookup"><span data-stu-id="db7f6-158">In other words, when you list hello outputs for a task, you can filter hello list on one of hello output types.</span></span> <span data-ttu-id="db7f6-159">Par exemple, « donnez-moi hello *aperçu* de sortie de tâche *109*. »</span><span class="sxs-lookup"><span data-stu-id="db7f6-159">For example, "Give me hello *preview* output for task *109*."</span></span> <span data-ttu-id="db7f6-160">Plus d’informations sur l’affichage et la récupération des sorties apparaît dans [d’extraire la sortie](#retrieve-output) plus loin dans l’article de hello.</span><span class="sxs-lookup"><span data-stu-id="db7f6-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in hello article.</span></span>

> [!TIP]
> <span data-ttu-id="db7f6-161">Hello genre de sortie également détermine l’emplacement Bonjour Azure portal un fichier particulier : *TaskOutput*-fichiers catégorisés apparaissent sous **fichiers de sortie de la tâche**, et *TaskLog*fichiers apparaissent sous **des journaux de tâches**.</span><span class="sxs-lookup"><span data-stu-id="db7f6-161">hello output kind also determines where in hello Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="db7f6-162">Stocker les sorties des travaux</span><span class="sxs-lookup"><span data-stu-id="db7f6-162">Store job outputs</span></span>

<span data-ttu-id="db7f6-163">En outre toostoring tâche fournit en sortie, vous pouvez stocker les sorties hello associés à un travail.</span><span class="sxs-lookup"><span data-stu-id="db7f6-163">In addition toostoring task outputs, you can store hello outputs associated with an entire job.</span></span> <span data-ttu-id="db7f6-164">Par exemple, dans la tâche de fusion hello d’un travail de rendu vidéo, vous pouvez rendre les films hello entièrement rendue comme une sortie de tâche.</span><span class="sxs-lookup"><span data-stu-id="db7f6-164">For example, in hello merge task of a movie rendering job, you could persist hello fully rendered movie as a job output.</span></span> <span data-ttu-id="db7f6-165">Lorsque votre tâche est terminée, votre application cliente peut répertorier et récupèrent des sorties hello pour le travail de hello, et ne doivent pas tooquery hello tâches individuelles.</span><span class="sxs-lookup"><span data-stu-id="db7f6-165">When your job is completed, your client application can list and retrieve hello outputs for hello job, and does not need tooquery hello individual tasks.</span></span>

<span data-ttu-id="db7f6-166">Stocker la sortie de travail en appelant hello [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] (méthode) et spécifiez hello [JobOutputKind] [ net_joboutputkind] et le nom de fichier :</span><span class="sxs-lookup"><span data-stu-id="db7f6-166">Store job output by calling hello [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify hello [JobOutputKind][net_joboutputkind] and filename:</span></span>

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="db7f6-167">Comme avec hello **TaskOutputKind** type pour les sorties de la tâche, vous utilisez hello [JobOutputKind] [ net_joboutputkind] type toocategorize un travail de persistante des fichiers.</span><span class="sxs-lookup"><span data-stu-id="db7f6-167">As with hello **TaskOutputKind** type for task outputs, you use hello [JobOutputKind][net_joboutputkind] type toocategorize a job's persisted files.</span></span> <span data-ttu-id="db7f6-168">Ce paramètre vous permet de requête toolater pour un type spécifique de la sortie de la (liste).</span><span class="sxs-lookup"><span data-stu-id="db7f6-168">This parameter allows you toolater query for (list) a specific type of output.</span></span> <span data-ttu-id="db7f6-169">Hello **JobOutputKind** type inclut les catégories de sortie et aperçu et prend en charge la création de catégories personnalisées.</span><span class="sxs-lookup"><span data-stu-id="db7f6-169">hello **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="db7f6-170">Stocker les journaux de tâches</span><span class="sxs-lookup"><span data-stu-id="db7f6-170">Store task logs</span></span>

<span data-ttu-id="db7f6-171">En outre, toopersisting un stockage de toodurable fichier lorsqu’une tâche ou une tâche terminée, vous devrez peut-être toopersist les fichiers qui sont mis à jour pendant l’exécution d’une tâche hello du &mdash; des fichiers journaux ou `stdout.txt` et `stderr.txt`, par exemple.</span><span class="sxs-lookup"><span data-stu-id="db7f6-171">In addition toopersisting a file toodurable storage when a task or job completes, you may need toopersist files that are updated during hello execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="db7f6-172">Dans ce but, bibliothèque de Conventions pour les fichiers par lots Azure hello fournit hello [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] (méthode).</span><span class="sxs-lookup"><span data-stu-id="db7f6-172">For this purpose, hello Azure Batch File Conventions library provides hello [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="db7f6-173">Avec [SaveTrackedAsync][net_savetrackedasync], vous pouvez effectuer le suivi de fichier tooa de mises à jour sur le nœud hello (à un intervalle que vous spécifiez) et conserver ces mises à jour de tooAzure stockage.</span><span class="sxs-lookup"><span data-stu-id="db7f6-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates tooa file on hello node (at an interval that you specify) and persist those updates tooAzure Storage.</span></span>

<span data-ttu-id="db7f6-174">Bonjour suivant extrait de code, nous utilisons [SaveTrackedAsync] [ net_savetrackedasync] tooupdate `stdout.txt` dans le stockage Azure lors de l’exécution de hello de tâche hello toutes les 15 secondes :</span><span class="sxs-lookup"><span data-stu-id="db7f6-174">In hello following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] tooupdate `stdout.txt` in Azure Storage every 15 seconds during hello execution of hello task:</span></span>

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// hello primary task logic is wrapped in a using statement that sends updates to
// hello stdout.txt blob in Storage every 15 seconds while hello task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code tooprocess data and produce output file(s) */

    // We are tracking hello disk file toosave our standard output, but the
    // node agent may take up too3 seconds tooflush hello stdout stream to
    // disk. So give hello file a moment toocatch up.
     await Task.Delay(stdoutFlushDelay);
}
```

<span data-ttu-id="db7f6-175">Hello commenté section `Code tooprocess data and produce output file(s)` est un espace réservé pour le code hello votre tâche exécute normalement.</span><span class="sxs-lookup"><span data-stu-id="db7f6-175">hello commented section `Code tooprocess data and produce output file(s)` is a placeholder for hello code that your task would normally perform.</span></span> <span data-ttu-id="db7f6-176">Par exemple, vous pouvez insérer un code qui télécharge des données à partir d’Azure Storage et effectue sur celles-ci des transformations ou des calculs.</span><span class="sxs-lookup"><span data-stu-id="db7f6-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="db7f6-177">Hello importante pour cet extrait de code est montrant comment vous pouvez encapsuler ce code dans un `using` bloc tooperiodically mettre à jour un fichier avec [SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="db7f6-177">hello important part of this snippet is demonstrating how you can wrap such code in a `using` block tooperiodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="db7f6-178">l’agent du nœud Hello est un programme qui s’exécute sur chaque nœud dans le pool de hello et fournit l’interface de commande et contrôle hello entre le nœud de hello et service de traitement par lots hello.</span><span class="sxs-lookup"><span data-stu-id="db7f6-178">hello node agent is a program that runs on each node in hello pool and provides hello command-and-control interface between hello node and hello Batch service.</span></span> <span data-ttu-id="db7f6-179">Hello `Task.Delay` appel est nécessaire à la fin de hello de ce `using` tooensure bloc qui hello agent du nœud a contenu de hello tooflush heure de la norme fichier stdout.txt de toohello sur le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="db7f6-179">hello `Task.Delay` call is required at hello end of this `using` block tooensure that hello node agent has time tooflush hello contents of standard out toohello stdout.txt file on hello node.</span></span> <span data-ttu-id="db7f6-180">Sans ce délai, il est possible toomiss hello dernières secondes de sortie.</span><span class="sxs-lookup"><span data-stu-id="db7f6-180">Without this delay, it is possible toomiss hello last few seconds of output.</span></span> <span data-ttu-id="db7f6-181">Ce délai n’est pas forcément requis pour tous les fichiers.</span><span class="sxs-lookup"><span data-stu-id="db7f6-181">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="db7f6-182">Lorsque vous activez le suivi des modifications avec des fichiers **SaveTrackedAsync**, seule *ajoute* fichier faisant l’objet toohello sont persistante tooAzure de stockage.</span><span class="sxs-lookup"><span data-stu-id="db7f6-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* toohello tracked file are persisted tooAzure Storage.</span></span> <span data-ttu-id="db7f6-183">Utilisez cette méthode uniquement pour les en rotation des fichiers journaux de suivi ou autres fichiers qui sont écrits toowith ajouter fin de toohello d’opérations de fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="db7f6-183">Use this method only for tracking non-rotating log files or other files that are written toowith append operations toohello end of hello file.</span></span>
> 
> 

## <a name="retrieve-output-data"></a><span data-ttu-id="db7f6-184">Récupérer les données de sortie</span><span class="sxs-lookup"><span data-stu-id="db7f6-184">Retrieve output data</span></span>

<span data-ttu-id="db7f6-185">Lorsque vous récupérez votre sortie persistante à l’aide de la bibliothèque de Conventions pour les fichiers par lots Azure hello, faire de façon centrée sur la tâche et à la tâche.</span><span class="sxs-lookup"><span data-stu-id="db7f6-185">When you retrieve your persisted output using hello Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="db7f6-186">Vous pouvez demander hello de sortie de tâche ou tâche sans avoir besoin de tooknow son chemin d’accès dans le stockage Azure, ou encore son nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="db7f6-186">You can request hello output for given task or job without needing tooknow its path in Azure Storage, or even its file name.</span></span> <span data-ttu-id="db7f6-187">À la place, vous pouvez effectuer des requêtes de fichiers de sortie par ID de tâche ou travail.</span><span class="sxs-lookup"><span data-stu-id="db7f6-187">Instead, you can request output files by task or job ID.</span></span>

<span data-ttu-id="db7f6-188">Hello extrait de code suivant itère au sein des tâches d’un travail, imprime des informations sur les fichiers de sortie hello pour la tâche hello, puis télécharge les fichiers à partir du stockage.</span><span class="sxs-lookup"><span data-stu-id="db7f6-188">hello following code snippet iterates through a job's tasks, prints some information about hello output files for hello task, and then downloads its files from Storage.</span></span>

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

## <a name="view-output-files-in-hello-azure-portal"></a><span data-ttu-id="db7f6-189">Afficher les fichiers de sortie Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="db7f6-189">View output files in hello Azure portal</span></span>

<span data-ttu-id="db7f6-190">portail Azure Hello affiche les fichiers de sortie de tâche et les journaux qui sont persistante tooa liés compte de stockage Azure à l’aide de hello [standard de Conventions pour les fichiers Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span><span class="sxs-lookup"><span data-stu-id="db7f6-190">hello Azure portal displays task output files and logs that are persisted tooa linked Azure Storage account using hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="db7f6-191">Vous pouvez implémenter ces conventions vous-même Bonjour un langage de votre choix, ou vous pouvez utiliser la bibliothèque de Conventions pour les fichiers hello dans vos applications .NET.</span><span class="sxs-lookup"><span data-stu-id="db7f6-191">You can implement these conventions yourself in hello a language of your choice, or you can use hello File Conventions library in your .NET applications.</span></span>

<span data-ttu-id="db7f6-192">affichage de hello tooenable de vos fichiers de sortie dans le portail de hello, vous devez satisfaire aux hello suivant les exigences :</span><span class="sxs-lookup"><span data-stu-id="db7f6-192">tooenable hello display of your output files in hello portal, you must satisfy hello following requirements:</span></span>

1. <span data-ttu-id="db7f6-193">[Lier un compte de stockage Azure](#requirement-linked-storage-account) tooyour compte Batch.</span><span class="sxs-lookup"><span data-stu-id="db7f6-193">[Link an Azure Storage account](#requirement-linked-storage-account) tooyour Batch account.</span></span>
2. <span data-ttu-id="db7f6-194">Respecter toohello prédéfini les conventions d’affectation de noms pour les fichiers et les conteneurs de stockage lors de la persistance des sorties.</span><span class="sxs-lookup"><span data-stu-id="db7f6-194">Adhere toohello predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="db7f6-195">Vous pouvez trouver la définition de hello de ces conventions dans bibliothèque de Conventions pour les fichiers hello [Lisez-moi][github_file_conventions_readme].</span><span class="sxs-lookup"><span data-stu-id="db7f6-195">You can find hello definition of these conventions in hello File Conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="db7f6-196">Si vous utilisez hello [Conventions pour les fichiers par lots Azure] [ nuget_package] bibliothèque toopersist votre sortie, vos fichiers sont conservés en fonction de toohello Conventions standard pour les fichiers.</span><span class="sxs-lookup"><span data-stu-id="db7f6-196">If you use hello [Azure Batch File Conventions][nuget_package] library toopersist your output, your files are persisted according toohello File Conventions standard.</span></span>

<span data-ttu-id="db7f6-197">fichiers de sortie de la tâche tooview et connecte hello portail Azure, accédez de tâche toohello dont la sortie vous intéressez, puis cliquez sur **enregistré les fichiers de sortie** ou **des journaux enregistrés**.</span><span class="sxs-lookup"><span data-stu-id="db7f6-197">tooview task output files and logs in hello Azure portal, navigate toohello task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="db7f6-198">Cette image montre hello **enregistré les fichiers de sortie** pour la tâche hello avec l’ID « 007 » :</span><span class="sxs-lookup"><span data-stu-id="db7f6-198">This image shows hello **Saved output files** for hello task with ID "007":</span></span>

<span data-ttu-id="db7f6-199">![Résultats de tâches panneau Bonjour portail Azure][2]</span><span class="sxs-lookup"><span data-stu-id="db7f6-199">![Task outputs blade in hello Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="db7f6-200">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="db7f6-200">Code sample</span></span>

<span data-ttu-id="db7f6-201">Hello [PersistOutputs] [ github_persistoutputs] exemple de projet est un des hello [exemples de code Azure Batch] [ github_samples] sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="db7f6-201">hello [PersistOutputs][github_persistoutputs] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="db7f6-202">Cette solution Visual Studio montre comment tâche toopersist de toouse hello Azure Batch Conventions pour les fichiers bibliothèque de sortie toodurable stockage.</span><span class="sxs-lookup"><span data-stu-id="db7f6-202">This Visual Studio solution demonstrates how toouse hello Azure Batch File Conventions library toopersist task output toodurable storage.</span></span> <span data-ttu-id="db7f6-203">toorun hello exemple, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="db7f6-203">toorun hello sample, follow these steps:</span></span>

1. <span data-ttu-id="db7f6-204">Projet ouvert hello dans **Visual Studio 2015 ou plus récente**.</span><span class="sxs-lookup"><span data-stu-id="db7f6-204">Open hello project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="db7f6-205">Ajouter votre lot et un stockage **informations d’identification de compte** trop**AccountSettings.settings** dans le projet de Microsoft.Azure.Batch.Samples.Common hello.</span><span class="sxs-lookup"><span data-stu-id="db7f6-205">Add your Batch and Storage **account credentials** too**AccountSettings.settings** in hello Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="db7f6-206">**Build** (mais ne s’exécutent pas) hello solution.</span><span class="sxs-lookup"><span data-stu-id="db7f6-206">**Build** (but do not run) hello solution.</span></span> <span data-ttu-id="db7f6-207">Restaurez les packages NuGet si vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="db7f6-207">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="db7f6-208">Hello d’utilisation tooupload portail Azure un [package d’application](batch-application-packages.md) pour **PersistOutputsTask**.</span><span class="sxs-lookup"><span data-stu-id="db7f6-208">Use hello Azure portal tooupload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="db7f6-209">Inclure hello `PersistOutputsTask.exe` et ses assemblys dépendants dans le package .zip de hello, ID de l’application hello ensemble trop « PersistOutputsTask » et application hello version du package trop « 1.0 ».</span><span class="sxs-lookup"><span data-stu-id="db7f6-209">Include hello `PersistOutputsTask.exe` and its dependent assemblies in hello .zip package, set hello application ID too"PersistOutputsTask", and hello application package version too"1.0".</span></span>
5. <span data-ttu-id="db7f6-210">**Démarrer** hello (exécution) **PersistOutputs** projet.</span><span class="sxs-lookup"><span data-stu-id="db7f6-210">**Start** (run) hello **PersistOutputs** project.</span></span>
6. <span data-ttu-id="db7f6-211">Lorsque toochoose demandées hello persistance technologie toouse pour l’exemple hello, entrez **1** toorun hello exemple à l’aide de la sortie de la tâche hello Conventions pour les fichiers bibliothèque toopersist.</span><span class="sxs-lookup"><span data-stu-id="db7f6-211">When prompted toochoose hello persistence technology toouse for running hello sample, enter **1** toorun hello sample using hello File Conventions library toopersist task output.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="db7f6-212">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="db7f6-212">Next steps</span></span>

### <a name="get-hello-batch-file-conventions-library-for-net"></a><span data-ttu-id="db7f6-213">Obtenir la bibliothèque de Conventions pour les fichiers Batch hello pour .NET</span><span class="sxs-lookup"><span data-stu-id="db7f6-213">Get hello Batch File Conventions library for .NET</span></span>

<span data-ttu-id="db7f6-214">bibliothèque de Conventions pour les fichiers Batch Hello pour .NET est disponible sur [NuGet][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="db7f6-214">hello Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span></span> <span data-ttu-id="db7f6-215">bibliothèque de Hello étend hello [CloudJob] [ net_cloudjob] et [CloudTask] [ net_cloudtask] classes avec de nouvelles méthodes.</span><span class="sxs-lookup"><span data-stu-id="db7f6-215">hello library extends hello [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span></span> <span data-ttu-id="db7f6-216">Voir aussi hello [documentation de référence](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) pour la bibliothèque de Conventions pour les fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="db7f6-216">Also see hello [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for hello File Conventions library.</span></span>

<span data-ttu-id="db7f6-217">Hello [code source] [ github_file_conventions] hello Conventions pour les fichiers bibliothèque est disponible sur GitHub Bonjour Microsoft Azure SDK pour le référentiel de .NET.</span><span class="sxs-lookup"><span data-stu-id="db7f6-217">hello [source code][github_file_conventions] for hello File Conventions library is available on GitHub in hello Microsoft Azure SDK for .NET repository.</span></span> 

### <a name="explore-other-approaches-for-persisting-output-data"></a><span data-ttu-id="db7f6-218">Explorer d’autres approches de conservation des données de sortie</span><span class="sxs-lookup"><span data-stu-id="db7f6-218">Explore other approaches for persisting output data</span></span>

- <span data-ttu-id="db7f6-219">Consultez [tooAzure stockage de sortie de projet de la persistance et la tâche](batch-task-output.md) pour une vue d’ensemble de la persistance des données de tâche et tâche.</span><span class="sxs-lookup"><span data-stu-id="db7f6-219">See [Persist job and task output tooAzure Storage](batch-task-output.md) for an overview of persisting task and job data.</span></span>
- <span data-ttu-id="db7f6-220">Consultez [conserver des tâches données tooAzure stockage avec hello API de lot](batch-task-output-files.md) toolearn toouse hello API de lot toopersist comment les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="db7f6-220">See [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md) toolearn how toouse hello Batch service API toopersist output data.</span></span>

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
[2]: ./media/batch-task-output/task-output-02.png "Résultats de tâches panneau Bonjour portail Azure"
