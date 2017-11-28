---
title: "aaaTutorial - utiliser la bibliothèque cliente Azure Batch hello pour .NET | Documents Microsoft"
description: "Découvrez les concepts de base hello de traitement par lots Azure et créer une solution simple à l’aide de .NET."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 76cb9807-cbc1-405a-8136-d1e53e66e82b
ms.service: batch
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06062b3886a8081bd9a831824a981503ef55f9b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-building-solutions-with-hello-batch-client-library-for-net"></a><span data-ttu-id="ddb9e-103">Prise en main la création de solutions avec la bibliothèque cliente de lot hello pour .NET</span><span class="sxs-lookup"><span data-stu-id="ddb9e-103">Get started building solutions with hello Batch client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ddb9e-104">.NET</span><span class="sxs-lookup"><span data-stu-id="ddb9e-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="ddb9e-105">Python</span><span class="sxs-lookup"><span data-stu-id="ddb9e-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="ddb9e-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="ddb9e-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="ddb9e-107">Principes fondamentaux de hello [Azure Batch] [ azure_batch] et hello [Batch .NET] [ net_api] bibliothèque dans cet article comme une étape de l’application d’exemple c# par les sujets abordés étape.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-107">Learn hello basics of [Azure Batch][azure_batch] and hello [Batch .NET][net_api] library in this article as we discuss a C# sample application step by step.</span></span> <span data-ttu-id="ddb9e-108">Voyons comment exemple d’application hello exploite hello lot service tooprocess une charge de travail parallèle dans le cloud de hello et comment il interagit avec [Azure Storage](../storage/common/storage-introduction.md) intermédiaire de fichier et l’extraction.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-108">We look at how hello sample application leverages hello Batch service tooprocess a parallel workload in hello cloud, and how it interacts with [Azure Storage](../storage/common/storage-introduction.md) for file staging and retrieval.</span></span> <span data-ttu-id="ddb9e-109">Vous allez en savoir un flux de travail courant lot application acquérir une compréhension de base du hello principaux composants du lot telles que les travaux, les tâches, les pools et nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-109">You'll learn a common Batch application workflow and gain a base understanding of hello major components of Batch such as jobs, tasks, pools, and compute nodes.</span></span>

<span data-ttu-id="ddb9e-110">![Flux de travail de la solution Batch (de base)][11]</span><span class="sxs-lookup"><span data-stu-id="ddb9e-110">![Batch solution workflow (basic)][11]</span></span><br/>

## <a name="prerequisites"></a><span data-ttu-id="ddb9e-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ddb9e-111">Prerequisites</span></span>
<span data-ttu-id="ddb9e-112">Cet article suppose que vous avez acquis une connaissance pratique de C# et Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-112">This article assumes that you have a working knowledge of C# and Visual Studio.</span></span> <span data-ttu-id="ddb9e-113">Il suppose également que vous êtes en mesure de toosatisfy hello création exigences relatives aux comptes qui sont spécifiées ci-dessous pour Azure et hello lot et les services de stockage.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-113">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Batch and Storage services.</span></span>

### <a name="accounts"></a><span data-ttu-id="ddb9e-114">Comptes</span><span class="sxs-lookup"><span data-stu-id="ddb9e-114">Accounts</span></span>
* <span data-ttu-id="ddb9e-115">**Compte Azure** : si vous ne possédez pas encore d’abonnement Azure, [créez un compte Azure gratuit][azure_free_account].</span><span class="sxs-lookup"><span data-stu-id="ddb9e-115">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account][azure_free_account].</span></span>
* <span data-ttu-id="ddb9e-116">**Compte Batch**: une fois que vous disposez d’un abonnement Azure, [créez un compte Azure Batch](batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ddb9e-116">**Batch account**: Once you have an Azure subscription, [create an Azure Batch account](batch-account-create-portal.md).</span></span>
* <span data-ttu-id="ddb9e-117">**Compte de stockage** : voir la section [Créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) de l’article [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="ddb9e-117">**Storage account**: See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ddb9e-118">Prend en charge du lot actuellement *uniquement* hello **à usage général** type de compte de stockage, comme décrit à l’étape 5 de # [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) dans [sur Azure comptes de stockage](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="ddb9e-118">Batch currently supports *only* hello **general-purpose** storage account type, as described in step #5 [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>
>
>

### <a name="visual-studio"></a><span data-ttu-id="ddb9e-119">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ddb9e-119">Visual Studio</span></span>
<span data-ttu-id="ddb9e-120">Vous devez avoir **Visual Studio 2015 ou plus récente** exemple de projet toobuild hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-120">You must have **Visual Studio 2015 or newer** toobuild hello sample project.</span></span> <span data-ttu-id="ddb9e-121">Vous pouvez trouver des versions gratuites et d’évaluation de Visual Studio dans hello [vue d’ensemble des produits Visual Studio][visual_studio].</span><span class="sxs-lookup"><span data-stu-id="ddb9e-121">You can find free and trial versions of Visual Studio in hello [overview of Visual Studio products][visual_studio].</span></span>

### <a name="dotnettutorial-code-sample"></a><span data-ttu-id="ddb9e-122">*DotNetTutorial*</span><span class="sxs-lookup"><span data-stu-id="ddb9e-122">*DotNetTutorial* code sample</span></span>
<span data-ttu-id="ddb9e-123">Hello [DotNetTutorial] [ github_dotnettutorial] exemple est un des hello de nombreux exemples de code de lot trouvés dans hello [exemples de traitement par lots azure] [ github_samples] référentiel sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-123">hello [DotNetTutorial][github_dotnettutorial] sample is one of hello many Batch code samples found in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="ddb9e-124">Vous pouvez télécharger tous les exemples de hello en cliquant sur **Clone ou téléchargement > ZIP de téléchargement** sur la page d’accueil de référentiel hello, ou en cliquant sur hello [azure-lot-exemples-master.zip] [ github_samples_zip]lien direct.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-124">You can download all hello samples by clicking  **Clone or download > Download ZIP** on hello repository home page, or by clicking hello [azure-batch-samples-master.zip][github_samples_zip] direct download link.</span></span> <span data-ttu-id="ddb9e-125">Une fois que vous avez extrait le contenu hello du fichier ZIP de hello, vous pouvez trouver des solutions de hello Bonjour suivant du dossier :</span><span class="sxs-lookup"><span data-stu-id="ddb9e-125">Once you've extracted hello contents of hello ZIP file, you can find hello solution in hello following folder:</span></span>

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a><span data-ttu-id="ddb9e-126">Azure Batch Explorer (facultatif)</span><span class="sxs-lookup"><span data-stu-id="ddb9e-126">Azure Batch Explorer (optional)</span></span>
<span data-ttu-id="ddb9e-127">Hello [Azure Batch Explorer] [ github_batchexplorer] est un utilitaire gratuit qui est inclus dans hello [exemples de traitement par lots azure] [ github_samples] référentiel sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-127">hello [Azure Batch Explorer][github_batchexplorer] is a free utility that is included in hello [azure-batch-samples][github_samples] repository on GitHub.</span></span> <span data-ttu-id="ddb9e-128">Toocomplete non requis lors de ce didacticiel, il peut être utile lors du développement et débogage de solutions de votre lot.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-128">While not required toocomplete this tutorial, it can be useful while developing and debugging your Batch solutions.</span></span>

## <a name="dotnettutorial-sample-project-overview"></a><span data-ttu-id="ddb9e-129">Vue d’ensemble de l’exemple de projet DotNetTutorial</span><span class="sxs-lookup"><span data-stu-id="ddb9e-129">DotNetTutorial sample project overview</span></span>
<span data-ttu-id="ddb9e-130">Hello *DotNetTutorial* exemple de code est une solution Visual Studio qui se compose de deux projets : **DotNetTutorial** et **TaskApplication**.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-130">hello *DotNetTutorial* code sample is a Visual Studio solution that consists of two projects: **DotNetTutorial** and **TaskApplication**.</span></span>

* <span data-ttu-id="ddb9e-131">**DotNetTutorial** est l’application hello client qui interagit avec tooexecute de services de stockage et de traitement par lots hello une charge de travail parallèle sur les nœuds de calcul (machines virtuelles).</span><span class="sxs-lookup"><span data-stu-id="ddb9e-131">**DotNetTutorial** is hello client application that interacts with hello Batch and Storage services tooexecute a parallel workload on compute nodes (virtual machines).</span></span> <span data-ttu-id="ddb9e-132">DotNetTutorial s’exécute sur votre station de travail locale.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-132">DotNetTutorial runs on your local workstation.</span></span>
* <span data-ttu-id="ddb9e-133">**TaskApplication** est hello programme qui s’exécute sur les nœuds de calcul dans le travail réel de tooperform Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-133">**TaskApplication** is hello program that runs on compute nodes in Azure tooperform hello actual work.</span></span> <span data-ttu-id="ddb9e-134">Dans l’exemple hello, `TaskApplication.exe` analyse hello texte dans un fichier téléchargé depuis le stockage Azure (fichier d’entrée de hello).</span><span class="sxs-lookup"><span data-stu-id="ddb9e-134">In hello sample, `TaskApplication.exe` parses hello text in a file downloaded from Azure Storage (hello input file).</span></span> <span data-ttu-id="ddb9e-135">Ensuite, il génère un fichier texte (fichier de sortie hello) qui contient une liste de mots de trois premières hello qui s’affichent dans le fichier d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-135">Then it produces a text file (hello output file) that contains a list of hello top three words that appear in hello input file.</span></span> <span data-ttu-id="ddb9e-136">Une fois qu’il crée le fichier de sortie hello, TaskApplication télécharge hello fichier tooAzure stockage.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-136">After it creates hello output file, TaskApplication uploads hello file tooAzure Storage.</span></span> <span data-ttu-id="ddb9e-137">Cela rend application cliente de toohello disponible en téléchargement.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-137">This makes it available toohello client application for download.</span></span> <span data-ttu-id="ddb9e-138">TaskApplication s’exécute en parallèle sur plusieurs nœuds de calcul Bonjour service Batch.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-138">TaskApplication runs in parallel on multiple compute nodes in hello Batch service.</span></span>

<span data-ttu-id="ddb9e-139">Hello diagramme suivant illustre les opérations principales hello qui sont effectuées par l’application cliente de hello, *DotNetTutorial*et l’application hello qui est exécutée par les tâches de hello, *TaskApplication*.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-139">hello following diagram illustrates hello primary operations that are performed by hello client application, *DotNetTutorial*, and hello application that is executed by hello tasks, *TaskApplication*.</span></span> <span data-ttu-id="ddb9e-140">Ce flux de travail de base est caractéristique de nombreuses solutions de calcul créées avec Batch.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-140">This basic workflow is typical of many compute solutions that are created with Batch.</span></span> <span data-ttu-id="ddb9e-141">Pendant qu’il ne présente pas toutes les fonctionnalités disponibles dans hello service Batch, presque tous les scénarios de traitement par lots inclut des parties de ce flux de travail.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-141">While it does not demonstrate every feature available in hello Batch service, nearly every Batch scenario includes portions of this workflow.</span></span>

<span data-ttu-id="ddb9e-142">![Exemple de flux de travail Batch][8]</span><span class="sxs-lookup"><span data-stu-id="ddb9e-142">![Batch example workflow][8]</span></span><br/>

[<span data-ttu-id="ddb9e-143">**Étape 1.**</span><span class="sxs-lookup"><span data-stu-id="ddb9e-143">**Step 1.**</span></span>](#step-1-create-storage-containers) <span data-ttu-id="ddb9e-144">Créer des **conteneurs** dans le Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-144">Create **containers** in Azure Blob Storage.</span></span><br/><span data-ttu-id="ddb9e-145">
[**Étape 2.**](#step-2-upload-task-application-and-data-files)</span><span class="sxs-lookup"><span data-stu-id="ddb9e-145">
[**Step 2.**](#step-2-upload-task-application-and-data-files)</span></span> <span data-ttu-id="ddb9e-146">Fichiers d’application de tâche de téléchargement et toocontainers des fichiers d’entrée.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-146">Upload task application files and input files toocontainers.</span></span><br/><span data-ttu-id="ddb9e-147">
[**Étape 3.**](#step-3-create-batch-pool)</span><span class="sxs-lookup"><span data-stu-id="ddb9e-147">
[**Step 3.**](#step-3-create-batch-pool)</span></span> <span data-ttu-id="ddb9e-148">Créer un **pool** Batch.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-148">Create a Batch **pool**.</span></span><br/>
  <span data-ttu-id="ddb9e-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span><span class="sxs-lookup"><span data-stu-id="ddb9e-149">&nbsp;&nbsp;&nbsp;&nbsp;**3a.**</span></span> <span data-ttu-id="ddb9e-150">Hello pool **StartTask** téléchargements hello toonodes (TaskApplication) des fichiers binaires de tâche dès qu’ils rejoignent le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-150">hello pool **StartTask** downloads hello task binary files (TaskApplication) toonodes as they join hello pool.</span></span><br/><span data-ttu-id="ddb9e-151">
[**Étape 4.**](#step-4-create-batch-job)</span><span class="sxs-lookup"><span data-stu-id="ddb9e-151">
[**Step 4.**](#step-4-create-batch-job)</span></span> <span data-ttu-id="ddb9e-152">Créer un **travail** Batch.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-152">Create a Batch **job**.</span></span><br/><span data-ttu-id="ddb9e-153">
[**Étape 5.**](#step-5-add-tasks-to-job)</span><span class="sxs-lookup"><span data-stu-id="ddb9e-153">
[**Step 5.**](#step-5-add-tasks-to-job)</span></span> <span data-ttu-id="ddb9e-154">Ajouter **tâches** toohello travail.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-154">Add **tasks** toohello job.</span></span><br/>
  <span data-ttu-id="ddb9e-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span><span class="sxs-lookup"><span data-stu-id="ddb9e-155">&nbsp;&nbsp;&nbsp;&nbsp;**5a.**</span></span> <span data-ttu-id="ddb9e-156">les tâches de Hello sont planifiée tooexecute sur les nœuds.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-156">hello tasks are scheduled tooexecute on nodes.</span></span><br/>
    <span data-ttu-id="ddb9e-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span><span class="sxs-lookup"><span data-stu-id="ddb9e-157">&nbsp;&nbsp;&nbsp;&nbsp;**5b.**</span></span> <span data-ttu-id="ddb9e-158">Chaque tâche télécharge ses données d’entrée depuis Stockage Azure, puis commence l’exécution.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-158">Each task downloads its input data from Azure Storage, then begins execution.</span></span><br/><span data-ttu-id="ddb9e-159">
[**Étape 6.**](#step-6-monitor-tasks)</span><span class="sxs-lookup"><span data-stu-id="ddb9e-159">
[**Step 6.**](#step-6-monitor-tasks)</span></span> <span data-ttu-id="ddb9e-160">Surveiller les tâches.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-160">Monitor tasks.</span></span><br/>
  <span data-ttu-id="ddb9e-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span><span class="sxs-lookup"><span data-stu-id="ddb9e-161">&nbsp;&nbsp;&nbsp;&nbsp;**6a.**</span></span> <span data-ttu-id="ddb9e-162">Comme les tâches sont effectuées, ils téléchargent leur tooAzure de données de sortie stockage.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-162">As tasks are completed, they upload their output data tooAzure Storage.</span></span><br/><span data-ttu-id="ddb9e-163">
[**Étape 7.**](#step-7-download-task-output)</span><span class="sxs-lookup"><span data-stu-id="ddb9e-163">
[**Step 7.**](#step-7-download-task-output)</span></span> <span data-ttu-id="ddb9e-164">Télécharger la sortie des tâches à partir de Storage.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-164">Download task output from Storage.</span></span>

<span data-ttu-id="ddb9e-165">Comme mentionné, pas chaque solution de traitement exécute les étapes exactes et peut inclure bien plus encore, mais hello *DotNetTutorial* exemple d’application montre des processus courants trouvés dans une solution de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-165">As mentioned, not every Batch solution performs these exact steps, and may include many more, but hello *DotNetTutorial* sample application demonstrates common processes found in a Batch solution.</span></span>

## <a name="build-hello-dotnettutorial-sample-project"></a><span data-ttu-id="ddb9e-166">Build hello *DotNetTutorial* exemple de projet</span><span class="sxs-lookup"><span data-stu-id="ddb9e-166">Build hello *DotNetTutorial* sample project</span></span>
<span data-ttu-id="ddb9e-167">Avant de pouvoir exécuter correctement exemple hello, vous devez spécifier les informations d’identification du compte Batch et de stockage dans hello *DotNetTutorial* du projet `Program.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-167">Before you can successfully run hello sample, you must specify both Batch and Storage account credentials in hello *DotNetTutorial* project's `Program.cs` file.</span></span> <span data-ttu-id="ddb9e-168">Si vous n’avez pas déjà fait, ouvrez la solution de hello dans Visual Studio en double-cliquant sur hello `DotNetTutorial.sln` fichier solution.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-168">If you have not done so already, open hello solution in Visual Studio by double-clicking hello `DotNetTutorial.sln` solution file.</span></span> <span data-ttu-id="ddb9e-169">Ou l’ouvrir à partir de Visual Studio à l’aide de hello **fichier > Ouvrir > Projet/Solution** menu.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-169">Or open it from within Visual Studio by using hello **File > Open > Project/Solution** menu.</span></span>

<span data-ttu-id="ddb9e-170">Ouvrez `Program.cs` dans hello *DotNetTutorial* projet.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-170">Open `Program.cs` within hello *DotNetTutorial* project.</span></span> <span data-ttu-id="ddb9e-171">Ajoutez ensuite vos informations d’identification comme spécifié haut hello du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="ddb9e-171">Then add your credentials as specified near hello top of hello file:</span></span>

```csharp
// Update hello Batch and Storage account credential strings below with hello values
// unique tooyour accounts. These are used when constructing connection strings
// for hello Batch and Storage client objects.

// Batch account credentials
private const string BatchAccountName = "";
private const string BatchAccountKey  = "";
private const string BatchAccountUrl  = "";

// Storage account credentials
private const string StorageAccountName = "";
private const string StorageAccountKey  = "";
```

> [!IMPORTANT]
> <span data-ttu-id="ddb9e-172">Comme indiqué ci-dessus, vous devez spécifier actuellement les informations d’identification hello pour un **à usage général** compte de stockage dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-172">As mentioned above, you must currently specify hello credentials for a **general-purpose** storage account in Azure Storage.</span></span> <span data-ttu-id="ddb9e-173">Vos applications de traitement utilisent le stockage d’objets blob dans hello **à usage général** compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-173">Your Batch applications use blob storage within hello **general-purpose** storage account.</span></span> <span data-ttu-id="ddb9e-174">Ne spécifiez pas les informations d’identification de hello pour un compte de stockage qui a été créé en sélectionnant hello *stockage d’objets Blob* type de compte.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-174">Do not specify hello credentials for a Storage account that was created by selecting hello *Blob storage* account type.</span></span>
>
>

<span data-ttu-id="ddb9e-175">Vous pouvez trouver vos informations d’identification compte Batch et de stockage dans le panneau de compte hello de chaque service Bonjour [portail Azure][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="ddb9e-175">You can find your Batch and Storage account credentials within hello account blade of each service in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="ddb9e-176">![Traitement par lots les informations d’identification dans le portail de hello][9]
![informations d’identification de stockage dans le portail de hello][10]</span><span class="sxs-lookup"><span data-stu-id="ddb9e-176">![Batch credentials in hello portal][9]
![Storage credentials in hello portal][10]</span></span><br/>

<span data-ttu-id="ddb9e-177">Maintenant que vous avez mis à jour de projet de hello avec vos informations d’identification, cliquez sur la solution hello dans l’Explorateur de solutions, puis cliquez sur **générer la Solution**.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-177">Now that you've updated hello project with your credentials, right-click hello solution in Solution Explorer and click **Build Solution**.</span></span> <span data-ttu-id="ddb9e-178">Confirmer la restauration hello de tous les packages NuGet, si vous êtes invité.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-178">Confirm hello restoration of any NuGet packages, if you're prompted.</span></span>

> [!TIP]
> <span data-ttu-id="ddb9e-179">Si les packages NuGet hello ne sont pas automatiquement restaurés, ou si vous constatez des erreurs sur une panne toorestore hello les packages, assurez-vous que vous avez hello [Gestionnaire de Package NuGet] [ nuget_packagemgr] installé.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-179">If hello NuGet packages are not automatically restored, or if you see errors about a failure toorestore hello packages, ensure that you have hello [NuGet Package Manager][nuget_packagemgr] installed.</span></span> <span data-ttu-id="ddb9e-180">Puis activez le téléchargement de hello des packages manquants.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-180">Then enable hello download of missing packages.</span></span> <span data-ttu-id="ddb9e-181">Consultez [l’activation de Package restauration au cours de génération] [ nuget_restore] tooenable téléchargement du package.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-181">See [Enabling Package Restore During Build][nuget_restore] tooenable package download.</span></span>
>
>

<span data-ttu-id="ddb9e-182">Bonjour les sections suivantes, nous réparties comme exemple d’application hello étapes hello qu’elle s’exécute tooprocess une charge de travail Bonjour service Batch et traitent de ces étapes en détail.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-182">In hello following sections, we break down hello sample application into hello steps that it performs tooprocess a workload in hello Batch service, and discuss those steps in detail.</span></span> <span data-ttu-id="ddb9e-183">Nous vous encourageons toorefer toohello solution ouverte dans Visual Studio pendant que vous travaillez Parcourir reste hello de cet article, étant donné que pas chaque ligne de code dans l’exemple hello est présenté.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-183">We encourage you toorefer toohello open solution in Visual Studio while you work your way through hello rest of this article, since not every line of code in hello sample is discussed.</span></span>

<span data-ttu-id="ddb9e-184">Accédez haut toohello Hello `MainAsync` méthode Bonjour *DotNetTutorial* du projet `Program.cs` fichier toostart à l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-184">Navigate toohello top of hello `MainAsync` method in hello *DotNetTutorial* project's `Program.cs` file toostart with Step 1.</span></span> <span data-ttu-id="ddb9e-185">Chaque étape ci-dessous, puis à peu près suit la progression hello de méthode appelle `MainAsync`.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-185">Each step below then roughly follows hello progression of method calls in `MainAsync`.</span></span>

## <a name="step-1-create-storage-containers"></a><span data-ttu-id="ddb9e-186">Étape 1 : créer des conteneurs de stockage</span><span class="sxs-lookup"><span data-stu-id="ddb9e-186">Step 1: Create Storage containers</span></span>
<span data-ttu-id="ddb9e-187">![Créer des conteneurs dans le service Stockage Azure][1]
</span><span class="sxs-lookup"><span data-stu-id="ddb9e-187">![Create containers in Azure Storage][1]
</span></span><br/>

<span data-ttu-id="ddb9e-188">Batch prend en charge l’interaction avec Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-188">Batch includes built-in support for interacting with Azure Storage.</span></span> <span data-ttu-id="ddb9e-189">Les conteneurs dans votre compte de stockage fournissent des fichiers de hello requis par les tâches de hello qui s’exécutent dans votre compte Batch.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-189">Containers in your Storage account will provide hello files needed by hello tasks that run in your Batch account.</span></span> <span data-ttu-id="ddb9e-190">les conteneurs de Hello fournissent également des données de sortie de hello toostore sur place qui produisent des tâches de hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-190">hello containers also provide a place toostore hello output data that hello tasks produce.</span></span> <span data-ttu-id="ddb9e-191">Hello première hello *DotNetTutorial* application cliente est créer trois conteneurs dans [stockage d’objets Blob Azure](../storage/common/storage-introduction.md):</span><span class="sxs-lookup"><span data-stu-id="ddb9e-191">hello first thing hello *DotNetTutorial* client application does is create three containers in [Azure Blob Storage](../storage/common/storage-introduction.md):</span></span>

* <span data-ttu-id="ddb9e-192">**application**: ce conteneur stockera application hello exécutée par les tâches de hello, ainsi qu’une de ses dépendances, comme les DLL.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-192">**application**: This container will store hello application run by hello tasks, as well as any of its dependencies, such as DLLs.</span></span>
* <span data-ttu-id="ddb9e-193">**d’entrée**: tâches téléchargera tooprocess de fichiers de données hello hello *d’entrée* conteneur.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-193">**input**: Tasks will download hello data files tooprocess from hello *input* container.</span></span>
* <span data-ttu-id="ddb9e-194">**sortie**: lorsque les tâches de terminer le traitement du fichier d’entrée, ils téléchargeront hello résultats toohello *sortie* conteneur.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-194">**output**: When tasks complete input file processing, they will upload hello results toohello *output* container.</span></span>

<span data-ttu-id="ddb9e-195">Dans l’ordre des toointeract avec un stockage de compte et de créer des conteneurs, nous utilisons hello [bibliothèque cliente de stockage Azure pour .NET][net_api_storage].</span><span class="sxs-lookup"><span data-stu-id="ddb9e-195">In order toointeract with a Storage account and create containers, we use hello [Azure Storage Client Library for .NET][net_api_storage].</span></span> <span data-ttu-id="ddb9e-196">Nous créons un compte toohello de référence avec [CloudStorageAccount][net_cloudstorageaccount]et de celui de créer un [CloudBlobClient][net_cloudblobclient]:</span><span class="sxs-lookup"><span data-stu-id="ddb9e-196">We create a reference toohello account with [CloudStorageAccount][net_cloudstorageaccount], and from that create a [CloudBlobClient][net_cloudblobclient]:</span></span>

```csharp
// Construct hello Storage account connection string
string storageConnectionString = String.Format(
    "DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}",
    StorageAccountName,
    StorageAccountKey);

// Retrieve hello storage account
CloudStorageAccount storageAccount =
    CloudStorageAccount.Parse(storageConnectionString);

// Create hello blob client, for use in obtaining references to
// blob storage containers
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```

<span data-ttu-id="ddb9e-197">Nous utilisons hello `blobClient` référence dans toute application hello et passez-le en tant que paramètre tooseveral méthodes.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-197">We use hello `blobClient` reference throughout hello application and pass it as a parameter tooseveral methods.</span></span> <span data-ttu-id="ddb9e-198">Est un exemple dans un bloc de code hello qui suit immédiatement hello ci-dessus, où nous appeler `CreateContainerIfNotExistAsync` tooactually de créer des conteneurs de hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-198">An example of this is in hello code block that immediately follows hello above, where we call `CreateContainerIfNotExistAsync` tooactually create hello containers.</span></span>

```csharp
// Use hello blob client toocreate hello containers in Azure Storage if they don't
// yet exist
const string appContainerName    = "application";
const string inputContainerName  = "input";
const string outputContainerName = "output";
await CreateContainerIfNotExistAsync(blobClient, appContainerName);
await CreateContainerIfNotExistAsync(blobClient, inputContainerName);
await CreateContainerIfNotExistAsync(blobClient, outputContainerName);
```

```csharp
private static async Task CreateContainerIfNotExistAsync(
    CloudBlobClient blobClient,
    string containerName)
{
        CloudBlobContainer container =
            blobClient.GetContainerReference(containerName);

        if (await container.CreateIfNotExistsAsync())
        {
                Console.WriteLine("Container [{0}] created.", containerName);
        }
        else
        {
                Console.WriteLine("Container [{0}] exists, skipping creation.",
                    containerName);
        }
}
```

<span data-ttu-id="ddb9e-199">Une fois que les conteneurs hello ont été créées, application hello peut maintenant télécharger des fichiers de hello qui seront utilisés par les tâches hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-199">Once hello containers have been created, hello application can now upload hello files that will be used by hello tasks.</span></span>

> [!TIP]
> <span data-ttu-id="ddb9e-200">[Comment toouse stockage d’objets Blob à partir de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) fournit une bonne vue d’ensemble de l’utilisation de conteneurs Azure Storage et les objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-200">[How toouse Blob Storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) provides a good overview of working with Azure Storage containers and blobs.</span></span> <span data-ttu-id="ddb9e-201">Il doit être haut hello de votre liste de lecture commencer à utiliser avec le lot.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-201">It should be near hello top of your reading list as you start working with Batch.</span></span>
>
>

## <a name="step-2-upload-task-application-and-data-files"></a><span data-ttu-id="ddb9e-202">Étape 2 : charger les fichiers d’application de tâche et les fichiers de données</span><span class="sxs-lookup"><span data-stu-id="ddb9e-202">Step 2: Upload task application and data files</span></span>
<span data-ttu-id="ddb9e-203">![Tâche de chargement d’application et d’entrée (données) des fichiers toocontainers][2]
</span><span class="sxs-lookup"><span data-stu-id="ddb9e-203">![Upload task application and input (data) files toocontainers][2]
</span></span><br/>

<span data-ttu-id="ddb9e-204">Dans le fichier de hello Téléchargez opération, *DotNetTutorial* définit tout d’abord les collections de **application** et **d’entrée** chemins d’accès de fichiers tels qu’ils existent sur l’ordinateur local de hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-204">In hello file upload operation, *DotNetTutorial* first defines collections of **application** and **input** file paths as they exist on hello local machine.</span></span> <span data-ttu-id="ddb9e-205">Puis il les télécharge ces conteneurs toohello de fichiers que vous avez créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-205">Then it uploads these files toohello containers that you created in hello previous step.</span></span>

```csharp
// Paths toohello executable and its dependencies that will be executed by hello tasks
List<string> applicationFilePaths = new List<string>
{
    // hello DotNetTutorial project includes a project reference tooTaskApplication,
    // allowing us toodetermine hello path of hello task application binary dynamically
    typeof(TaskApplication.Program).Assembly.Location,
    "Microsoft.WindowsAzure.Storage.dll"
};

// hello collection of data files that are toobe processed by hello tasks
List<string> inputFilePaths = new List<string>
{
    @"..\..\taskdata1.txt",
    @"..\..\taskdata2.txt",
    @"..\..\taskdata3.txt"
};

// Upload hello application and its dependencies tooAzure Storage. This is the
// application that will process hello data files, and will be executed by each
// of hello tasks on hello compute nodes.
List<ResourceFile> applicationFiles = await UploadFilesToContainerAsync(
    blobClient,
    appContainerName,
    applicationFilePaths);

// Upload hello data files. This is hello data that will be processed by each of
// hello tasks that are executed on hello compute nodes within hello pool.
List<ResourceFile> inputFiles = await UploadFilesToContainerAsync(
    blobClient,
    inputContainerName,
    inputFilePaths);
```

<span data-ttu-id="ddb9e-206">Il existe deux méthodes dans `Program.cs` impliquées dans le processus de téléchargement hello :</span><span class="sxs-lookup"><span data-stu-id="ddb9e-206">There are two methods in `Program.cs` that are involved in hello upload process:</span></span>

* <span data-ttu-id="ddb9e-207">`UploadFilesToContainerAsync`: Cette méthode retourne une collection de [ResourceFile] [ net_resourcefile] (voir ci-dessous) des objets et en interne les appels `UploadFileToContainerAsync` tooupload chaque fichier qui est passé dans hello *filePaths* paramètre.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-207">`UploadFilesToContainerAsync`: This method returns a collection of [ResourceFile][net_resourcefile] objects (discussed below) and internally calls `UploadFileToContainerAsync` tooupload each file that is passed in hello *filePaths* parameter.</span></span>
* <span data-ttu-id="ddb9e-208">`UploadFileToContainerAsync`: Cette méthode hello réellement effectue le téléchargement du fichier hello et crée hello est [ResourceFile] [ net_resourcefile] objets.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-208">`UploadFileToContainerAsync`: This is hello method that actually performs hello file upload and creates hello [ResourceFile][net_resourcefile] objects.</span></span> <span data-ttu-id="ddb9e-209">Après avoir téléchargé le fichier de hello, il obtient une signature d’accès partagé (SAP) pour le fichier de hello et retourne un objet ResourceFile qui le représente.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-209">After uploading hello file, it obtains a shared access signature (SAS) for hello file and returns a ResourceFile object that represents it.</span></span> <span data-ttu-id="ddb9e-210">Les signatures d’accès partagé sont également décrites ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-210">Shared access signatures are also discussed below.</span></span>

```csharp
private static async Task<ResourceFile> UploadFileToContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string filePath)
{
        Console.WriteLine(
            "Uploading file {0} toocontainer [{1}]...", filePath, containerName);

        string blobName = Path.GetFileName(filePath);

        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlockBlob blobData = container.GetBlockBlobReference(blobName);
        await blobData.UploadFromFileAsync(filePath);

        // Set hello expiry time and permissions for hello blob shared access signature.
        // In this case, no start time is specified, so hello shared access signature
        // becomes valid immediately
        SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy
        {
                SharedAccessExpiryTime = DateTime.UtcNow.AddHours(2),
                Permissions = SharedAccessBlobPermissions.Read
        };

        // Construct hello SAS URL for blob
        string sasBlobToken = blobData.GetSharedAccessSignature(sasConstraints);
        string blobSasUri = String.Format("{0}{1}", blobData.Uri, sasBlobToken);

        return new ResourceFile(blobSasUri, blobName);
}
```

### <a name="resourcefiles"></a><span data-ttu-id="ddb9e-211">Objets ResourceFile</span><span class="sxs-lookup"><span data-stu-id="ddb9e-211">ResourceFiles</span></span>
<span data-ttu-id="ddb9e-212">A [ResourceFile] [ net_resourcefile] fournit des tâches dans un lot avec fichier de tooa hello URL dans le stockage Azure qui est téléchargé tooa nœud de calcul avant l’exécution de cette tâche.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-212">A [ResourceFile][net_resourcefile] provides tasks in Batch with hello URL tooa file in Azure Storage that is downloaded tooa compute node before that task is run.</span></span> <span data-ttu-id="ddb9e-213">Hello [ResourceFile.BlobSource] [ net_resourcefile_blobsource] propriété spécifie une URL complète du fichier de hello hello telle qu’elle existe dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-213">hello [ResourceFile.BlobSource][net_resourcefile_blobsource] property specifies hello full URL of hello file as it exists in Azure Storage.</span></span> <span data-ttu-id="ddb9e-214">URL de Hello peut-être également inclure une signature d’accès partagé (SAS) qui fournit un accès sécurisé toohello fichier.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-214">hello URL may also include a shared access signature (SAS) that provides secure access toohello file.</span></span> <span data-ttu-id="ddb9e-215">La propriété *ResourceFiles* est utilisée par la plupart des types de tâche de Batch .NET, notamment :</span><span class="sxs-lookup"><span data-stu-id="ddb9e-215">Most tasks types within Batch .NET include a *ResourceFiles* property, including:</span></span>

* <span data-ttu-id="ddb9e-216">[CloudTask][net_task]</span><span class="sxs-lookup"><span data-stu-id="ddb9e-216">[CloudTask][net_task]</span></span>
* <span data-ttu-id="ddb9e-217">[StartTask][net_pool_starttask]</span><span class="sxs-lookup"><span data-stu-id="ddb9e-217">[StartTask][net_pool_starttask]</span></span>
* <span data-ttu-id="ddb9e-218">[JobPreparationTask][net_jobpreptask]</span><span class="sxs-lookup"><span data-stu-id="ddb9e-218">[JobPreparationTask][net_jobpreptask]</span></span>
* <span data-ttu-id="ddb9e-219">[JobReleaseTask][net_jobreltask]</span><span class="sxs-lookup"><span data-stu-id="ddb9e-219">[JobReleaseTask][net_jobreltask]</span></span>

<span data-ttu-id="ddb9e-220">Hello DotNetTutorial exemple d’application n’utilise pas hello JobPreparationTask ou JobReleaseTask les types de tâches, mais vous pouvez en savoir plus sur les [nœuds de calcul des tâches de préparation et l’achèvement de projet sur Azure Batch exécuter](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="ddb9e-220">hello DotNetTutorial sample application does not use hello JobPreparationTask or JobReleaseTask task types, but you can read more about them in [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md).</span></span>

### <a name="shared-access-signature-sas"></a><span data-ttu-id="ddb9e-221">Signature d’accès partagé (SAP)</span><span class="sxs-lookup"><span data-stu-id="ddb9e-221">Shared access signature (SAS)</span></span>
<span data-ttu-id="ddb9e-222">Accès partagé, les signatures sont des chaînes qui, lorsque inclus dans le cadre d’une URL, fournir un accès sécurisé toocontainers et les objets BLOB dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-222">Shared access signatures are strings which—when included as part of a URL—provide secure access toocontainers and blobs in Azure Storage.</span></span> <span data-ttu-id="ddb9e-223">Hello DotNetTutorial application utilise les deux objets blob et conteneur partagé URL de signature d’accès et montre comment tooobtain ces partagés accéder aux chaînes de signature à partir de hello service de stockage.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-223">hello DotNetTutorial application uses both blob and container shared access signature URLs, and demonstrates how tooobtain these shared access signature strings from hello Storage service.</span></span>

* <span data-ttu-id="ddb9e-224">**Signatures d’accès partagé d’objets BLOB**: StartTask du pool hello dans DotNetTutorial utilise des signatures d’accès partagé de blob lors du téléchargement de fichiers binaires d’application hello et les fichiers de données d’entrée à partir du stockage (voir étape 3 ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="ddb9e-224">**Blob shared access signatures**: hello pool's StartTask in DotNetTutorial uses blob shared access signatures when it downloads hello application binaries and input data files from Storage (see Step #3 below).</span></span> <span data-ttu-id="ddb9e-225">Hello `UploadFileToContainerAsync` méthode dans du DotNetTutorial `Program.cs` contient le code hello qui obtient la signature d’accès partagé de l’objet blob.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-225">hello `UploadFileToContainerAsync` method in DotNetTutorial's `Program.cs` contains hello code that obtains each blob's shared access signature.</span></span> <span data-ttu-id="ddb9e-226">Elle le fait en appelant [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span><span class="sxs-lookup"><span data-stu-id="ddb9e-226">It does so by calling [CloudBlob.GetSharedAccessSignature][net_sas_blob].</span></span>
* <span data-ttu-id="ddb9e-227">**Signatures d’accès partagé de conteneur**: que chaque tâche a terminé son travail sur le nœud de calcul hello, il télécharge sa toohello de fichier de sortie *sortie* conteneur dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-227">**Container shared access signatures**: As each task finishes its work on hello compute node, it uploads its output file toohello *output* container in Azure Storage.</span></span> <span data-ttu-id="ddb9e-228">toodo TaskApplication utilise ainsi une signature d’accès partagé de conteneur qui fournit un accès en écriture toohello conteneur en tant que partie du chemin d’accès hello lorsqu’il télécharge les fichier hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-228">toodo so, TaskApplication uses a container shared access signature that provides write access toohello container as part of hello path when it uploads hello file.</span></span> <span data-ttu-id="ddb9e-229">Signature d’accès partagé de conteneur hello obtention s’effectue de la même manière que lorsque l’objet blob de hello signature d’accès partagé.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-229">Obtaining hello container shared access signature is done in a similar fashion as when obtaining hello blob shared access signature.</span></span> <span data-ttu-id="ddb9e-230">Dans DotNetTutorial, vous constaterez que hello `GetContainerSasUrl` les appels de méthode d’assistance [CloudBlobContainer.GetSharedAccessSignature] [ net_sas_container] toodo donc.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-230">In DotNetTutorial, you will find that hello `GetContainerSasUrl` helper method calls [CloudBlobContainer.GetSharedAccessSignature][net_sas_container] toodo so.</span></span> <span data-ttu-id="ddb9e-231">Vous allez en savoir plus sur la façon dont TaskApplication utilise le conteneur de hello signature d’accès partagé dans « étape 6 : tâches de surveillance. »</span><span class="sxs-lookup"><span data-stu-id="ddb9e-231">You'll read more about how TaskApplication uses hello container shared access signature in "Step 6: Monitor Tasks."</span></span>

> [!TIP]
> <span data-ttu-id="ddb9e-232">Extraction de série en deux parties hello sur les signatures d’accès partagé, [partie 1 : hello de présentation partagé le modèle de signature (SAP) d’accès](../storage/common/storage-dotnet-shared-access-signature-part-1.md) et [partie 2 : créer et utiliser une signature d’accès partagé (SAS) avec le stockage d’objets Blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn plus sur l’envoi de toodata un accès sécurisé dans votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-232">Check out hello two-part series on shared access signatures, [Part 1: Understanding hello shared access signature (SAS) model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) and [Part 2: Create and use a shared access signature (SAS) with Blob storage](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn more about providing secure access toodata in your Storage account.</span></span>
>
>

## <a name="step-3-create-batch-pool"></a><span data-ttu-id="ddb9e-233">Étape 3 : créer le pool Batch</span><span class="sxs-lookup"><span data-stu-id="ddb9e-233">Step 3: Create Batch pool</span></span>
<span data-ttu-id="ddb9e-234">![Créer un pool Batch][3]
</span><span class="sxs-lookup"><span data-stu-id="ddb9e-234">![Create a Batch pool][3]
</span></span><br/>

<span data-ttu-id="ddb9e-235">Un **pool** Batch est une collection de nœuds de calcul (machines virtuelles) sur lequel Batch exécute les tâches d’un travail.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-235">A Batch **pool** is a collection of compute nodes (virtual machines) on which Batch executes a job's tasks.</span></span>

<span data-ttu-id="ddb9e-236">Après avoir téléchargé l’application hello et les fichiers de données toohello compte de stockage avec l’API de stockage Azure, *DotNetTutorial* commencer des appels toohello lot service avec les API fournies par la bibliothèque de lot .NET hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-236">After uploading hello application and data files toohello Storage account with Azure Storage APIs, *DotNetTutorial* begins making calls toohello Batch service with APIs provided by hello Batch .NET library.</span></span> <span data-ttu-id="ddb9e-237">Hello code crée d’abord un [BatchClient][net_batchclient]:</span><span class="sxs-lookup"><span data-stu-id="ddb9e-237">hello code first creates a [BatchClient][net_batchclient]:</span></span>

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

<span data-ttu-id="ddb9e-238">Ensuite, exemple hello crée un pool de nœuds de calcul dans le compte de traitement par lots hello par un appel trop`CreatePoolIfNotExistsAsync`.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-238">Next, hello sample creates a pool of compute nodes in hello Batch account with a call too`CreatePoolIfNotExistsAsync`.</span></span> <span data-ttu-id="ddb9e-239">`CreatePoolIfNotExistsAsync`utilise hello [BatchClient.PoolOperations.CreatePool] [ net_pool_create] méthode toocreate un nouveau pool Bonjour service Batch :</span><span class="sxs-lookup"><span data-stu-id="ddb9e-239">`CreatePoolIfNotExistsAsync` uses hello [BatchClient.PoolOperations.CreatePool][net_pool_create] method toocreate a new pool in hello Batch service:</span></span>

```csharp
private static async Task CreatePoolIfNotExistAsync(BatchClient batchClient, string poolId, IList<ResourceFile> resourceFiles)
{
    CloudPool pool = null;
    try
    {
        Console.WriteLine("Creating pool [{0}]...", poolId);

        // Create hello unbound pool. Until we call CloudPool.Commit() or CommitAsync(), no pool is actually created in the
        // Batch service. This CloudPool instance is therefore considered "unbound," and we can modify its properties.
        pool = batchClient.PoolOperations.CreatePool(
            poolId: poolId,
            targetDedicatedComputeNodes: 3,                                             // 3 compute nodes
            virtualMachineSize: "small",                                                // single-core, 1.75 GB memory, 225 GB disk
            cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));   // Windows Server 2012 R2

        // Create and assign hello StartTask that will be executed when compute nodes join hello pool.
        // In this case, we copy hello StartTask's resource files (that will be automatically downloaded
        // toohello node by hello StartTask) into hello shared directory that all tasks will have access to.
        pool.StartTask = new StartTask
        {
            // Specify a command line for hello StartTask that copies hello task application files toothe
            // node's shared directory. Every compute node in a Batch pool is configured with a number
            // of pre-defined environment variables that can be referenced by commands or applications
            // run by tasks.

            // Since a successful execution of robocopy can return a non-zero exit code (e.g. 1 when one or
            // more files were successfully copied) we need toomanually exit with a 0 for Batch toorecognize
            // StartTask execution success.
            CommandLine = "cmd /c (robocopy %AZ_BATCH_TASK_WORKING_DIR% %AZ_BATCH_NODE_SHARED_DIR%) ^& IF %ERRORLEVEL% LEQ 1 exit 0",
            ResourceFiles = resourceFiles,
            WaitForSuccess = true
        };

        await pool.CommitAsync();
    }
    catch (BatchException be)
    {
        // Swallow hello specific error code PoolExists since that is expected if hello pool already exists
        if (be.RequestInformation?.BatchError != null && be.RequestInformation.BatchError.Code == BatchErrorCodeStrings.PoolExists)
        {
            Console.WriteLine("hello pool {0} already existed when we tried toocreate it", poolId);
        }
        else
        {
            throw; // Any other exception is unexpected
        }
    }
}
```

<span data-ttu-id="ddb9e-240">Lorsque vous créez un pool avec [CreatePool][net_pool_create], vous spécifiez plusieurs paramètres tels que nombre hello de nœuds de calcul, hello [taille des nœuds de hello](../cloud-services/cloud-services-sizes-specs.md), et hello nœuds d’exploitation système.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-240">When you create a pool with [CreatePool][net_pool_create], you specify several parameters such as hello number of compute nodes, hello [size of hello nodes](../cloud-services/cloud-services-sizes-specs.md), and hello nodes' operating system.</span></span> <span data-ttu-id="ddb9e-241">Dans *DotNetTutorial*, nous utilisons [CloudServiceConfiguration] [ net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 à partir de [Services de cloud computing](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="ddb9e-241">In *DotNetTutorial*, we use [CloudServiceConfiguration][net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 from [Cloud Services](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> 

<span data-ttu-id="ddb9e-242">Vous pouvez également créer des pools de nœuds de calcul qui sont des Machines virtuelles (VM) Azure en spécifiant hello [VirtualMachineConfiguration] [ net_virtualmachineconfiguration] pour le pool.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-242">You can also create pools of compute nodes that are Azure Virtual Machines (VMs) by specifying hello [VirtualMachineConfiguration][net_virtualmachineconfiguration] for your pool.</span></span> <span data-ttu-id="ddb9e-243">Vous pouvez créer un pool de nœuds de calcul de machines virtuelles à partir d’[images Windows ou Linux](batch-linux-nodes.md).</span><span class="sxs-lookup"><span data-stu-id="ddb9e-243">You can create a pool of VM compute nodes from either Windows or [Linux images](batch-linux-nodes.md).</span></span> <span data-ttu-id="ddb9e-244">source de Hello pour vos images de machine virtuelle peut être :</span><span class="sxs-lookup"><span data-stu-id="ddb9e-244">hello source for your VM images can be either:</span></span>

- <span data-ttu-id="ddb9e-245">Hello [Azure Marketplace de Machines virtuelles][vm_marketplace], qui fournit des images Windows et Linux qui sont prêts à l’emploi.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-245">hello [Azure Virtual Machines Marketplace][vm_marketplace], which provides both Windows and Linux images that are ready-to-use.</span></span> 
- <span data-ttu-id="ddb9e-246">Une image personnalisée que vous préparez et fournissez.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-246">A custom image that you prepare and provide.</span></span> <span data-ttu-id="ddb9e-247">Pour en savoir plus sur les images personnalisées, consultez [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool) (Développer des solutions de calcul parallèles à grande échelle avec Batch).</span><span class="sxs-lookup"><span data-stu-id="ddb9e-247">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ddb9e-248">Les ressources de calcul dans Batch vous sont facturées.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-248">You are charged for compute resources in Batch.</span></span> <span data-ttu-id="ddb9e-249">toominimize des coûts, vous pouvez diminuer `targetDedicatedComputeNodes` too1 avant d’exécuter les exemples hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-249">toominimize costs, you can lower `targetDedicatedComputeNodes` too1 before you run hello sample.</span></span>
>
>

<span data-ttu-id="ddb9e-250">Avec ces propriétés de nœud physique, vous pouvez également spécifier un [StartTask] [ net_pool_starttask] pour le pool de hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-250">Along with these physical node properties, you may also specify a [StartTask][net_pool_starttask] for hello pool.</span></span> <span data-ttu-id="ddb9e-251">Hello StartTask s’exécute sur chaque nœud de ce nœud rejoint le pool de hello, chaque fois qu’un nœud est redémarré.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-251">hello StartTask executes on each node as that node joins hello pool, and each time a node is restarted.</span></span> <span data-ttu-id="ddb9e-252">Hello StartTask est particulièrement utile pour installer des applications de calcul nœuds préalable toohello l’exécution de tâches.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-252">hello StartTask is especially useful for installing applications on compute nodes prior toohello execution of tasks.</span></span> <span data-ttu-id="ddb9e-253">Par exemple, si vos tâches de traitement des données à l’aide de scripts Python, vous pouvez utiliser un tooinstall StartTask Python sur les nœuds de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-253">For example, if your tasks process data by using Python scripts, you could use a StartTask tooinstall Python on hello compute nodes.</span></span>

<span data-ttu-id="ddb9e-254">Dans cet exemple d’application, hello StartTask copie les fichiers de hello qu’il télécharge à partir du stockage (qui sont spécifié à l’aide de hello [StartTask][net_starttask].[ ResourceFiles] [ net_starttask_resourcefiles] propriété) à partir du répertoire partagé toohello de répertoire travail hello StartTask qui *tous les* en cours d’exécution sur le nœud de hello puissent y accéder.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-254">In this sample application, hello StartTask copies hello files that it downloads from Storage (which are specified by using hello [StartTask][net_starttask].[ResourceFiles][net_starttask_resourcefiles] property) from hello StartTask working directory toohello shared directory that *all* tasks running on hello node can access.</span></span> <span data-ttu-id="ddb9e-255">Pour l’essentiel, cette copie `TaskApplication.exe` et toohello de ses dépendances répertoire partagé sur chaque nœud comme nœud de hello rejoint le pool de hello, afin que toutes les tâches qui s’exécutent sur le nœud de hello puissent y accéder.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-255">Essentially, this copies `TaskApplication.exe` and its dependencies toohello shared directory on each node as hello node joins hello pool, so that any tasks that run on hello node can access it.</span></span>

> [!TIP]
> <span data-ttu-id="ddb9e-256">Hello **des packages d’application** fonctionnalité de traitement par lots Azure fournit une autre façon tooget votre application sur les nœuds de calcul hello dans un pool.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-256">hello **application packages** feature of Azure Batch provides another way tooget your application onto hello compute nodes in a pool.</span></span> <span data-ttu-id="ddb9e-257">Consultez [déployer des nœuds de toocompute d’applications avec les packages d’applications de traitement par lots](batch-application-packages.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-257">See [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md) for details.</span></span>
>
>

<span data-ttu-id="ddb9e-258">Remarquables dans l’extrait de code hello ci-dessus est également utiliser deux variables d’environnement Bonjour hello *CommandLine* propriété Hello StartTask : `%AZ_BATCH_TASK_WORKING_DIR%` et `%AZ_BATCH_NODE_SHARED_DIR%`.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-258">Also notable in hello code snippet above is hello use of two environment variables in hello *CommandLine* property of hello StartTask: `%AZ_BATCH_TASK_WORKING_DIR%` and `%AZ_BATCH_NODE_SHARED_DIR%`.</span></span> <span data-ttu-id="ddb9e-259">Chaque nœud de calcul au sein d’un pool de traitement par lots est automatiquement configuré avec plusieurs variables d’environnement qui sont tooBatch spécifique.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-259">Each compute node within a Batch pool is automatically configured with several environment variables that are specific tooBatch.</span></span> <span data-ttu-id="ddb9e-260">Tout processus qui est exécutée par une tâche a des variables d’environnement toothese accès.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-260">Any process that is executed by a task has access toothese environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="ddb9e-261">toofind plus d’informations sur les variables d’environnement hello qui sont disponibles sur les nœuds de calcul dans un pool de traitement par lots et des informations sur les répertoires de travail tâche, consultez hello [paramètres d’environnement pour les tâches](batch-api-basics.md#environment-settings-for-tasks) et [fichiers et répertoires ](batch-api-basics.md#files-and-directories) sections Bonjour [vue d’ensemble de lot pour les développeurs](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="ddb9e-261">toofind out more about hello environment variables that are available on compute nodes in a Batch pool, and information on task working directories, see hello [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) and [Files and directories](batch-api-basics.md#files-and-directories) sections in hello [Batch feature overview for developers](batch-api-basics.md).</span></span>
>
>

## <a name="step-4-create-batch-job"></a><span data-ttu-id="ddb9e-262">Étape 4 : créer un travail Batch</span><span class="sxs-lookup"><span data-stu-id="ddb9e-262">Step 4: Create Batch job</span></span>
<span data-ttu-id="ddb9e-263">![Créer un travail Batch][4]</span><span class="sxs-lookup"><span data-stu-id="ddb9e-263">![Create Batch job][4]</span></span><br/>

<span data-ttu-id="ddb9e-264">Un **travail** Batch constitue un ensemble de tâches et est associé à un pool de nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-264">A Batch **job** is a collection of tasks, and is associated with a pool of compute nodes.</span></span> <span data-ttu-id="ddb9e-265">tâches de Hello dans un travail s’exécutent sur les nœuds de calcul du pool hello associé.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-265">hello tasks in a job execute on hello associated pool's compute nodes.</span></span>

<span data-ttu-id="ddb9e-266">Vous pouvez utiliser une tâche pour l’organisation et le suivi des tâches dans les charges de travail, mais également pour imposer certaines contraintes--par exemple hello durée d’exécution pour le travail de hello (et par extension, ses tâches), ainsi que la priorité dans les travaux de tooother relation Bonjour lot compte.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-266">You can use a job not only for organizing and tracking tasks in related workloads, but also for imposing certain constraints--such as hello maximum runtime for hello job (and by extension, its tasks) as well as job priority in relation tooother jobs in hello Batch account.</span></span> <span data-ttu-id="ddb9e-267">Dans cet exemple, toutefois, les travaux de hello est associé uniquement à pool hello qui a été créé à l’étape 3 de #.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-267">In this example, however, hello job is associated only with hello pool that was created in step #3.</span></span> <span data-ttu-id="ddb9e-268">Aucune propriété supplémentaire n’est configurée.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-268">No additional properties are configured.</span></span>

<span data-ttu-id="ddb9e-269">Tous les travaux Batch sont associés à un pool spécifique.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-269">All Batch jobs are associated with a specific pool.</span></span> <span data-ttu-id="ddb9e-270">Cette association indique les nœuds de hello tâches seront exécutent sur.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-270">This association indicates which nodes hello job's tasks will execute on.</span></span> <span data-ttu-id="ddb9e-271">Vous spécifiez en utilisant hello [CloudJob.PoolInformation] [ net_job_poolinfo] propriété, comme indiqué dans l’extrait de code hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-271">You specify this by using hello [CloudJob.PoolInformation][net_job_poolinfo] property, as shown in hello code snippet below.</span></span>

```csharp
private static async Task CreateJobAsync(
    BatchClient batchClient,
    string jobId,
    string poolId)
{
    Console.WriteLine("Creating job [{0}]...", jobId);

    CloudJob job = batchClient.JobOperations.CreateJob();
    job.Id = jobId;
    job.PoolInformation = new PoolInformation { PoolId = poolId };

    await job.CommitAsync();
}
```

<span data-ttu-id="ddb9e-272">Maintenant qu’un travail a été créé, les tâches sont ajoutées travail hello de tooperform.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-272">Now that a job has been created, tasks are added tooperform hello work.</span></span>

## <a name="step-5-add-tasks-toojob"></a><span data-ttu-id="ddb9e-273">Étape 5 : Ajouter des tâches toojob</span><span class="sxs-lookup"><span data-stu-id="ddb9e-273">Step 5: Add tasks toojob</span></span>
<span data-ttu-id="ddb9e-274">![Ajouter des tâches toojob][5]</span><span class="sxs-lookup"><span data-stu-id="ddb9e-274">![Add tasks toojob][5]</span></span><br/><span data-ttu-id="ddb9e-275">
*(1) tâches sont ajoutés toohello travail, tâches de hello (2) sont planifiée toorun sur les nœuds et les tâches hello (3) téléchargement tooprocess de fichiers de données hello*</span><span class="sxs-lookup"><span data-stu-id="ddb9e-275">
*(1) Tasks are added toohello job, (2) hello tasks are scheduled toorun on nodes, and (3) hello tasks download hello data files tooprocess*</span></span>

<span data-ttu-id="ddb9e-276">Lot **tâches** sont des nœuds de calcul hello unités de travail individuelles qui s’exécutent sur hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-276">Batch **tasks** are hello individual units of work that execute on hello compute nodes.</span></span> <span data-ttu-id="ddb9e-277">Une tâche a une ligne de commande et exécute les scripts hello ou exécutables que vous spécifiez dans cette ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-277">A task has a command line and runs hello scripts or executables that you specify in that command line.</span></span>

<span data-ttu-id="ddb9e-278">tooactually effectuer un travail, de tâches doivent être ajoutées à une tâche tooa.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-278">tooactually perform work, tasks must be added tooa job.</span></span> <span data-ttu-id="ddb9e-279">Chaque [CloudTask] [ net_task] est configuré à l’aide d’une propriété de ligne de commande et [ResourceFiles] [ net_task_resourcefiles] (comme avec la tâche de début du pool hello) qui tâche Hello télécharge toohello nœud avant sa ligne de commande est exécutée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-279">Each [CloudTask][net_task] is configured by using a command-line property and [ResourceFiles][net_task_resourcefiles] (as with hello pool's StartTask) that hello task downloads toohello node before its command line is automatically executed.</span></span> <span data-ttu-id="ddb9e-280">Bonjour *DotNetTutorial* exemple de projet, chaque tâche traite un seul fichier.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-280">In hello *DotNetTutorial* sample project, each task processes only one file.</span></span> <span data-ttu-id="ddb9e-281">Par conséquent, sa collection ResourceFiles contient un seul élément.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-281">Thus, its ResourceFiles collection contains a single element.</span></span>

```csharp
private static async Task<List<CloudTask>> AddTasksAsync(
    BatchClient batchClient,
    string jobId,
    List<ResourceFile> inputFiles,
    string outputContainerSasUrl)
{
    Console.WriteLine("Adding {0} tasks toojob [{1}]...", inputFiles.Count, jobId);

    // Create a collection toohold hello tasks that we'll be adding toohello job
    List<CloudTask> tasks = new List<CloudTask>();

    // Create each of hello tasks. Because we copied hello task application toothe
    // node's shared directory with hello pool's StartTask, we can access it via
    // hello shared directory on hello node that hello task runs on.
    foreach (ResourceFile inputFile in inputFiles)
    {
        string taskId = "topNtask" + inputFiles.IndexOf(inputFile);
        string taskCommandLine = String.Format(
            "cmd /c %AZ_BATCH_NODE_SHARED_DIR%\\TaskApplication.exe {0} 3 \"{1}\"",
            inputFile.FilePath,
            outputContainerSasUrl);

        CloudTask task = new CloudTask(taskId, taskCommandLine);
        task.ResourceFiles = new List<ResourceFile> { inputFile };
        tasks.Add(task);
    }

    // Add hello tasks as a collection, as opposed tooissuing a separate AddTask call
    // for each. Bulk task submission helps tooensure efficient underlying API calls
    // toohello Batch service.
    await batchClient.JobOperations.AddTaskAsync(jobId, tasks);

    return tasks;
}
```

> [!IMPORTANT]
> <span data-ttu-id="ddb9e-282">Lorsque leur accès aux variables d’environnement telles que `%AZ_BATCH_NODE_SHARED_DIR%` ou exécuter une application introuvable dans du nœud hello `PATH`, lignes de commande de tâche doivent être précédés `cmd /c`.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-282">When they access environment variables such as `%AZ_BATCH_NODE_SHARED_DIR%` or execute an application not found in hello node's `PATH`, task command lines must be prefixed with `cmd /c`.</span></span> <span data-ttu-id="ddb9e-283">Explicitement cela exécute l’interpréteur de commandes hello et lui demander de tooterminate après avoir effectué votre commande.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-283">This will explicitly execute hello command interpreter and instruct it tooterminate after carrying out your command.</span></span> <span data-ttu-id="ddb9e-284">Cette exigence n’est pas nécessaire si vos tâches exécutent une application dans du nœud hello `PATH` (tel que *robocopy.exe* ou *powershell.exe*) et aucune variable d’environnement n’est utilisés.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-284">This requirement is unnecessary if your tasks execute an application in hello node's `PATH` (such as *robocopy.exe* or *powershell.exe*) and no environment variables are used.</span></span>
>
>

<span data-ttu-id="ddb9e-285">Au sein de hello `foreach` boucle dans l’extrait de code hello ci-dessus, vous pouvez voir que la ligne de commande hello pour la tâche hello est construite telles que les trois arguments de ligne de commande sont passés trop*TaskApplication.exe*:</span><span class="sxs-lookup"><span data-stu-id="ddb9e-285">Within hello `foreach` loop in hello code snippet above, you can see that hello command line for hello task is constructed such that three command-line arguments are passed too*TaskApplication.exe*:</span></span>

1. <span data-ttu-id="ddb9e-286">Hello **premier argument** est le chemin de hello de tooprocess de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-286">hello **first argument** is hello path of hello file tooprocess.</span></span> <span data-ttu-id="ddb9e-287">Ce fichier de toohello de chemin d’accès local hello est telle qu’elle existe sur le nœud de hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-287">This is hello local path toohello file as it exists on hello node.</span></span> <span data-ttu-id="ddb9e-288">Lorsque hello objet ResourceFile dans `UploadFileToContainerAsync` tout d’abord créée ci-dessus, le nom de fichier hello a été utilisée pour cette propriété (en tant que paramètre toohello ResourceFile constructeur).</span><span class="sxs-lookup"><span data-stu-id="ddb9e-288">When hello ResourceFile object in `UploadFileToContainerAsync` was first created above, hello file name was used for this property (as a parameter toohello ResourceFile constructor).</span></span> <span data-ttu-id="ddb9e-289">Cela indique que hello fichier se trouve dans hello même répertoire que *TaskApplication.exe*.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-289">This indicates that hello file can be found in hello same directory as *TaskApplication.exe*.</span></span>
2. <span data-ttu-id="ddb9e-290">Hello **le second argument** Spécifie que haut hello *N* mots doivent être écrits en fichier de sortie toohello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-290">hello **second argument** specifies that hello top *N* words should be written toohello output file.</span></span> <span data-ttu-id="ddb9e-291">Dans l’exemple hello, il est codé en dur afin que les mots de trois principaux hello sont écrites de fichier de sortie toohello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-291">In hello sample, this is hard-coded so that hello top three words are written toohello output file.</span></span>
3. <span data-ttu-id="ddb9e-292">Hello **troisième argument** est la signature d’accès partagé hello (SAS) qui fournit un accès en écriture toohello **sortie** conteneur dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-292">hello **third argument** is hello shared access signature (SAS) that provides write access toohello **output** container in Azure Storage.</span></span> <span data-ttu-id="ddb9e-293">*TaskApplication.exe* utilise cette partagée des URL de signature d’accès lorsqu’il télécharge tooAzure de fichier de sortie hello stockage.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-293">*TaskApplication.exe* uses this shared access signature URL when it uploads hello output file tooAzure Storage.</span></span> <span data-ttu-id="ddb9e-294">Vous trouverez le code de hello pour ce Bonjour `UploadFileToContainer` méthode de projet hello TaskApplication `Program.cs` fichier :</span><span class="sxs-lookup"><span data-stu-id="ddb9e-294">You can find hello code for this in hello `UploadFileToContainer` method in hello TaskApplication project's `Program.cs` file:</span></span>

```csharp
// NOTE: From project TaskApplication Program.cs

private static void UploadFileToContainer(string filePath, string containerSas)
{
        string blobName = Path.GetFileName(filePath);

        // Obtain a reference toohello container using hello SAS URI.
        CloudBlobContainer container = new CloudBlobContainer(new Uri(containerSas));

        // Upload hello file (as a new blob) toohello container
        try
        {
                CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
                blob.UploadFromFile(filePath);

                Console.WriteLine("Write operation succeeded for SAS URL " + containerSas);
                Console.WriteLine();
        }
        catch (StorageException e)
        {

                Console.WriteLine("Write operation failed for SAS URL " + containerSas);
                Console.WriteLine("Additional error information: " + e.Message);
                Console.WriteLine();

                // Indicate that a failure has occurred so that when hello Batch service
                // sets hello CloudTask.ExecutionInformation.ExitCode for hello task that
                // executed this application, it properly indicates that there was a
                // problem with hello task.
                Environment.ExitCode = -1;
        }
}
```

## <a name="step-6-monitor-tasks"></a><span data-ttu-id="ddb9e-295">Étape 6 : surveiller les tâches</span><span class="sxs-lookup"><span data-stu-id="ddb9e-295">Step 6: Monitor tasks</span></span>
<span data-ttu-id="ddb9e-296">![Surveiller les tâches][6]</span><span class="sxs-lookup"><span data-stu-id="ddb9e-296">![Monitor tasks][6]</span></span><br/><span data-ttu-id="ddb9e-297">
*Hello client application (1) analyses hello les tâches d’achèvement et état de réussite et (2) hello tâches téléchargement résultat données tooAzure stockage*</span><span class="sxs-lookup"><span data-stu-id="ddb9e-297">
*hello client application (1) monitors hello tasks for completion and success status, and (2) hello tasks upload result data tooAzure Storage*</span></span>

<span data-ttu-id="ddb9e-298">Lorsque les tâches sont ajoutées tooa travail, ils sont en file d’attente et planifiés pour l’exécution sur des nœuds de calcul dans le pool hello associé hello travail automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-298">When tasks are added tooa job, they are automatically queued and scheduled for execution on compute nodes within hello pool associated with hello job.</span></span> <span data-ttu-id="ddb9e-299">Selon les paramètres que vous spécifiez hello, lot gère queuing à toutes les tâches, la planification, une nouvelle tentative et autres tâches d’administration de tâche pour vous.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-299">Based on hello settings you specify, Batch handles all task queuing, scheduling, retrying, and other task administration duties for you.</span></span>

<span data-ttu-id="ddb9e-300">Il existe de nombreuses approches toomonitoring exécution de la tâche.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-300">There are many approaches toomonitoring task execution.</span></span> <span data-ttu-id="ddb9e-301">DotNetTutorial en présente un exemple simple signalant uniquement les états d’achèvement et d’échec ou de réussite des tâches.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-301">DotNetTutorial shows a simple example that reports only on completion and task failure or success states.</span></span> <span data-ttu-id="ddb9e-302">Au sein de hello `MonitorTasks` méthode dans du DotNetTutorial `Program.cs`, il existe trois concepts Batch .NET qui garantissent la discussion.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-302">Within hello `MonitorTasks` method in DotNetTutorial's `Program.cs`, there are three Batch .NET concepts that warrant discussion.</span></span> <span data-ttu-id="ddb9e-303">Ils sont répertoriés ci-dessous dans leur ordre d’apparition :</span><span class="sxs-lookup"><span data-stu-id="ddb9e-303">They are listed below in their order of appearance:</span></span>

1. <span data-ttu-id="ddb9e-304">**ODATADetailLevel** : la spécification d’un élément [ODATADetailLevel][net_odatadetaillevel] dans les opérations de liste (telles que l’obtention d’une liste des tâches d’un travail) est primordiale pour garantir les performances de l’application Batch.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-304">**ODATADetailLevel**: Specifying [ODATADetailLevel][net_odatadetaillevel] in list operations (such as obtaining a list of a job's tasks) is essential in ensuring Batch application performance.</span></span> <span data-ttu-id="ddb9e-305">Ajouter [interroger le service de traitement par lots Azure hello efficacement](batch-efficient-list-queries.md) tooyour lecture de la liste si vous prévoyez d’effectuer toute sorte de surveillance de l’état au sein de vos applications de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-305">Add [Query hello Azure Batch service efficiently](batch-efficient-list-queries.md) tooyour reading list if you plan on doing any sort of status monitoring within your Batch applications.</span></span>
2. <span data-ttu-id="ddb9e-306">**TaskStateMonitor** : l’élément [TaskStateMonitor][net_taskstatemonitor] fournit aux applications Batch .NET des utilitaires d’assistance pour la surveillance des états de tâche.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-306">**TaskStateMonitor**: [TaskStateMonitor][net_taskstatemonitor] provides Batch .NET applications with helper utilities for monitoring task states.</span></span> <span data-ttu-id="ddb9e-307">Dans `MonitorTasks`, *DotNetTutorial* attend que toutes les tâches tooreach [TaskState.Completed] [ net_taskstate] dans un intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-307">In `MonitorTasks`, *DotNetTutorial* waits for all tasks tooreach [TaskState.Completed][net_taskstate] within a time limit.</span></span> <span data-ttu-id="ddb9e-308">Puis il met fin à la tâche de hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-308">Then it terminates hello job.</span></span>
3. <span data-ttu-id="ddb9e-309">**TerminateJobAsync**: arrêt d’un travail avec [JobOperations.TerminateJobAsync] [ net_joboperations_terminatejob] (ou hello blocage JobOperations.TerminateJob) marque ce travail comme terminé.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-309">**TerminateJobAsync**: Terminating a job with [JobOperations.TerminateJobAsync][net_joboperations_terminatejob] (or hello blocking JobOperations.TerminateJob) marks that job as completed.</span></span> <span data-ttu-id="ddb9e-310">Il est essentiel toodo, donc si votre solution de traitement par lots utilise un [JobReleaseTask][net_jobreltask].</span><span class="sxs-lookup"><span data-stu-id="ddb9e-310">It is essential toodo so if your Batch solution uses a [JobReleaseTask][net_jobreltask].</span></span> <span data-ttu-id="ddb9e-311">Il s’agit d’un type spécial de tâche, qui est décrit dans [Tâches d’achèvement et de préparation des travaux](batch-job-prep-release.md).</span><span class="sxs-lookup"><span data-stu-id="ddb9e-311">This is a special type of task, which is described in [Job preparation and completion tasks](batch-job-prep-release.md).</span></span>

<span data-ttu-id="ddb9e-312">Hello `MonitorTasks` méthode à partir de *DotNetTutorial*de `Program.cs` apparaît ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ddb9e-312">hello `MonitorTasks` method from *DotNetTutorial*'s `Program.cs` appears below:</span></span>

```csharp
private static async Task<bool> MonitorTasks(
    BatchClient batchClient,
    string jobId,
    TimeSpan timeout)
{
    bool allTasksSuccessful = true;
    const string successMessage = "All tasks reached state Completed.";
    const string failureMessage = "One or more tasks failed tooreach hello Completed state within hello timeout period.";

    // Obtain hello collection of tasks currently managed by hello job. Note that we use
    // a detail level too specify that only hello "id" property of each task should be
    // populated. Using a detail level for all list operations helps toolower
    // response time from hello Batch service.
    ODATADetailLevel detail = new ODATADetailLevel(selectClause: "id");
    List<CloudTask> tasks =
        await batchClient.JobOperations.ListTasks(JobId, detail).ToListAsync();

    Console.WriteLine("Awaiting task completion, timeout in {0}...",
        timeout.ToString());

    // We use a TaskStateMonitor toomonitor hello state of our tasks. In this case, we
    // will wait for all tasks tooreach hello Completed state.
    TaskStateMonitor taskStateMonitor
        = batchClient.Utilities.CreateTaskStateMonitor();

    try
    {
        await taskStateMonitor.WhenAll(tasks, TaskState.Completed, timeout);
    }
    catch (TimeoutException)
    {
        await batchClient.JobOperations.TerminateJobAsync(jobId, failureMessage);
        Console.WriteLine(failureMessage);
        return false;
    }

    await batchClient.JobOperations.TerminateJobAsync(jobId, successMessage);

    // All tasks have reached hello "Completed" state, however, this does not
    // guarantee all tasks completed successfully. Here we further check each task's
    // ExecutionInfo property tooensure that it did not encounter a failure
    // or return a non-zero exit code.

    // Update hello detail level toopopulate only hello task id and executionInfo
    // properties. We refresh hello tasks below, and need only this information for
    // each task.
    detail.SelectClause = "id, executionInfo";

    foreach (CloudTask task in tasks)
    {
        // Populate hello task's properties with hello latest info from hello Batch service
        await task.RefreshAsync(detail);

        if (task.ExecutionInformation.Result == TaskExecutionResult.Failure)
        {
            // A task with failure information set indicates there was a problem with hello task. It is important toonote that
            // hello task's state can be "Completed," yet still have encountered a failure.

            allTasksSuccessful = false;

            Console.WriteLine("WARNING: Task [{0}] encountered a failure: {1}", task.Id, task.ExecutionInformation.FailureInformation.Message);
            if (task.ExecutionInformation.ExitCode != 0)
            {
                // A non-zero exit code may indicate that hello application executed by hello task encountered an error
                // during execution. As not every application returns non-zero on failure by default (e.g. robocopy),
                // your implementation of error checking may differ from this example.

                Console.WriteLine("WARNING: Task [{0}] returned a non-zero exit code - this may indicate task execution or completion failure.", task.Id);
            }
        }
    }

    if (allTasksSuccessful)
    {
        Console.WriteLine("Success! All tasks completed successfully within hello specified timeout period.");
    }

    return allTasksSuccessful;
}
```

## <a name="step-7-download-task-output"></a><span data-ttu-id="ddb9e-313">Étape 7 : télécharger la sortie des tâches</span><span class="sxs-lookup"><span data-stu-id="ddb9e-313">Step 7: Download task output</span></span>
<span data-ttu-id="ddb9e-314">![Télécharger la sortie des tâches à partir du service Stockage][7]</span><span class="sxs-lookup"><span data-stu-id="ddb9e-314">![Download task output from Storage][7]</span></span><br/>

<span data-ttu-id="ddb9e-315">Maintenant que hello tâche terminée, sortie hello des tâches de hello peut être téléchargé depuis le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-315">Now that hello job is completed, hello output from hello tasks can be downloaded from Azure Storage.</span></span> <span data-ttu-id="ddb9e-316">Cette opération s’effectue avec un appel trop`DownloadBlobsFromContainerAsync` dans *DotNetTutorial*de `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="ddb9e-316">This is done with a call too`DownloadBlobsFromContainerAsync` in *DotNetTutorial*'s `Program.cs`:</span></span>

```csharp
private static async Task DownloadBlobsFromContainerAsync(
    CloudBlobClient blobClient,
    string containerName,
    string directoryPath)
{
        Console.WriteLine("Downloading all files from container [{0}]...", containerName);

        // Retrieve a reference tooa previously created container
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);

        // Get a flat listing of all hello block blobs in hello specified container
        foreach (IListBlobItem item in container.ListBlobs(
                    prefix: null,
                    useFlatBlobListing: true))
        {
                // Retrieve reference toohello current blob
                CloudBlob blob = (CloudBlob)item;

                // Save blob contents tooa file in hello specified folder
                string localOutputFile = Path.Combine(directoryPath, blob.Name);
                await blob.DownloadToFileAsync(localOutputFile, FileMode.Create);
        }

        Console.WriteLine("All files downloaded too{0}", directoryPath);
}
```

> [!NOTE]
> <span data-ttu-id="ddb9e-317">Hello appel trop`DownloadBlobsFromContainerAsync` Bonjour *DotNetTutorial* application spécifie que les fichiers hello doivent être téléchargé tooyour `%TEMP%` dossier.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-317">hello call too`DownloadBlobsFromContainerAsync` in hello *DotNetTutorial* application specifies that hello files should be downloaded tooyour `%TEMP%` folder.</span></span> <span data-ttu-id="ddb9e-318">Pensez toomodify libre cette sortie d’emplacement.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-318">Feel free toomodify this output location.</span></span>
>
>

## <a name="step-8-delete-containers"></a><span data-ttu-id="ddb9e-319">Étape 8 : supprimer les conteneurs</span><span class="sxs-lookup"><span data-stu-id="ddb9e-319">Step 8: Delete containers</span></span>
<span data-ttu-id="ddb9e-320">Vous êtes facturé pour les données qui résident dans le stockage Azure, il est toujours une bonne idée tooremove les objets BLOB qui ne sont plus nécessaires pour vos traitements par lots.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-320">Because you are charged for data that resides in Azure Storage, it's always a good idea tooremove blobs that are no longer needed for your Batch jobs.</span></span> <span data-ttu-id="ddb9e-321">Dans de DotNetTutorial `Program.cs`, cela est effectué avec la méthode d’assistance de toohello trois appels `DeleteContainerAsync`:</span><span class="sxs-lookup"><span data-stu-id="ddb9e-321">In DotNetTutorial's `Program.cs`, this is done with three calls toohello helper method `DeleteContainerAsync`:</span></span>

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

<span data-ttu-id="ddb9e-322">méthode Hello elle-même simplement Obtient un conteneur toohello de référence, puis appelle [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span><span class="sxs-lookup"><span data-stu-id="ddb9e-322">hello method itself merely obtains a reference toohello container, and then calls [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:</span></span>

```csharp
private static async Task DeleteContainerAsync(
    CloudBlobClient blobClient,
    string containerName)
{
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);

    if (await container.DeleteIfExistsAsync())
    {
        Console.WriteLine("Container [{0}] deleted.", containerName);
    }
    else
    {
        Console.WriteLine("Container [{0}] does not exist, skipping deletion.",
            containerName);
    }
}
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a><span data-ttu-id="ddb9e-323">Étape 9 : Supprimer le travail de hello et pool de hello</span><span class="sxs-lookup"><span data-stu-id="ddb9e-323">Step 9: Delete hello job and hello pool</span></span>
<span data-ttu-id="ddb9e-324">À l’étape finale de hello, vous êtes invité à toodelete hello travail et hello le pool qui ont été créés par l’application de DotNetTutorial hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-324">In hello final step, you're prompted toodelete hello job and hello pool that were created by hello DotNetTutorial application.</span></span> <span data-ttu-id="ddb9e-325">Bien que vous ne soyez pas facturé pour les travaux et les tâches à proprement parler, les nœuds de calcul vous *sont* facturés.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-325">Although you're not charged for jobs and tasks themselves, you *are* charged for compute nodes.</span></span> <span data-ttu-id="ddb9e-326">Par conséquent, nous vous conseillons d’affecter les nœuds uniquement en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-326">Thus, we recommend that you allocate nodes only as needed.</span></span> <span data-ttu-id="ddb9e-327">La suppression des pools inutilisés peut être incluse dans votre processus de maintenance.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-327">Deleting unused pools can be part of your maintenance process.</span></span>

<span data-ttu-id="ddb9e-328">Hello BatchClient [JobOperations] [ net_joboperations] et [PoolOperations] [ net_pooloperations] ont tous deux des méthodes de suppression correspondantes, qui sont appelées si utilisateur de Hello confirme la suppression :</span><span class="sxs-lookup"><span data-stu-id="ddb9e-328">hello BatchClient's [JobOperations][net_joboperations] and [PoolOperations][net_pooloperations] both have corresponding deletion methods, which are called if hello user confirms deletion:</span></span>

```csharp
// Clean up hello resources we've created in hello Batch account if hello user so chooses
Console.WriteLine();
Console.WriteLine("Delete job? [yes] no");
string response = Console.ReadLine().ToLower();
if (response != "n" && response != "no")
{
    await batchClient.JobOperations.DeleteJobAsync(JobId);
}

Console.WriteLine("Delete pool? [yes] no");
response = Console.ReadLine();
if (response != "n" && response != "no")
{
    await batchClient.PoolOperations.DeletePoolAsync(PoolId);
}
```

> [!IMPORTANT]
> <span data-ttu-id="ddb9e-329">N’oubliez pas que les ressources de calcul vous sont facturées et que la suppression des pools inutilisés vous permet de réduire les coûts.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-329">Keep in mind that you are charged for compute resources—deleting unused pools will minimize cost.</span></span> <span data-ttu-id="ddb9e-330">En outre, n’oubliez pas que la suppression d’un pool supprime tous les nœuds de calcul dans ce pool, et que toutes les données sur les nœuds hello seront irrécupérables après la suppression d’un pool de hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-330">Also, be aware that deleting a pool deletes all compute nodes within that pool, and that any data on hello nodes will be unrecoverable after hello pool is deleted.</span></span>
>
>

## <a name="run-hello-dotnettutorial-sample"></a><span data-ttu-id="ddb9e-331">Exécutez hello *DotNetTutorial* exemple</span><span class="sxs-lookup"><span data-stu-id="ddb9e-331">Run hello *DotNetTutorial* sample</span></span>
<span data-ttu-id="ddb9e-332">Lorsque vous exécutez exemple d’application hello, la sortie de console hello sera similaire toohello suivant.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-332">When you run hello sample application, hello console output will be similar toohello following.</span></span> <span data-ttu-id="ddb9e-333">Pendant l’exécution, vous rencontrerez une pause à `Awaiting task completion, timeout in 00:30:00...` tandis que les nœuds de calcul du pool hello sont démarrés.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-333">During execution, you will experience a pause at `Awaiting task completion, timeout in 00:30:00...` while hello pool's compute nodes are started.</span></span> <span data-ttu-id="ddb9e-334">Hello d’utilisation [portail Azure] [ azure_portal] toomonitor votre pool, nœuds de calcul, tâche et pendant et après l’exécution des tâches.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-334">Use hello [Azure portal][azure_portal] toomonitor your pool, compute nodes, job, and tasks during and after execution.</span></span> <span data-ttu-id="ddb9e-335">Hello d’utilisation [portail Azure] [ azure_portal] ou hello [Azure Storage Explorer] [ storage_explorers] tooview hello ressources de stockage (conteneurs et objets BLOB) qui sont créé par l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-335">Use hello [Azure portal][azure_portal] or hello [Azure Storage Explorer][storage_explorers] tooview hello Storage resources (containers and blobs) that are created by hello application.</span></span>

<span data-ttu-id="ddb9e-336">Temps d’exécution par défaut est **environ 5 minutes** lorsque vous exécutez des application hello dans sa configuration par défaut.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-336">Typical execution time is **approximately 5 minutes** when you run hello application in its default configuration.</span></span>

```
Sample start: 1/8/2016 09:42:58 AM

Container [application] created.
Container [input] created.
Container [output] created.
Uploading file C:\repos\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial\bin\Debug\TaskApplication.exe toocontainer [application]...
Uploading file Microsoft.WindowsAzure.Storage.dll toocontainer [application]...
Uploading file ..\..\taskdata1.txt toocontainer [input]...
Uploading file ..\..\taskdata2.txt toocontainer [input]...
Uploading file ..\..\taskdata3.txt toocontainer [input]...
Creating pool [DotNetTutorialPool]...
Creating job [DotNetTutorialJob]...
Adding 3 tasks toojob [DotNetTutorialJob]...
Awaiting task completion, timeout in 00:30:00...
Success! All tasks completed successfully within hello specified timeout period.
Downloading all files from container [output]...
All files downloaded tooC:\Users\USERNAME\AppData\Local\Temp
Container [application] deleted.
Container [input] deleted.
Container [output] deleted.

Sample end: 1/8/2016 09:47:47 AM
Elapsed time: 00:04:48.5358142

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="ddb9e-337">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ddb9e-337">Next steps</span></span>
<span data-ttu-id="ddb9e-338">Estimez les modifications toomake libre trop*DotNetTutorial* et *TaskApplication* tooexperiment avec différents scénarios de calcul.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-338">Feel free toomake changes too*DotNetTutorial* and *TaskApplication* tooexperiment with different compute scenarios.</span></span> <span data-ttu-id="ddb9e-339">Par exemple, essayez d’ajouter un délai d’exécution trop*TaskApplication*, par exemple comme avec [Thread.Sleep][net_thread_sleep], toosimulate longue des tâches et les surveiller dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-339">For example, try adding an execution delay too*TaskApplication*, such as with [Thread.Sleep][net_thread_sleep], toosimulate long-running tasks and monitor them in hello portal.</span></span> <span data-ttu-id="ddb9e-340">Essayez d’ajouter des tâches plus ou en ajustant de nombre hello de nœuds de calcul.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-340">Try adding more tasks or adjusting hello number of compute nodes.</span></span> <span data-ttu-id="ddb9e-341">Ajouter toocheck logique pour et autoriser l’utilisation de hello de durée d’exécution de toospeed pool existant (*indicateur*: extraire `ArticleHelpers.cs` Bonjour [Microsoft.Azure.Batch.Samples.Common] [ github_samples_common] projet [exemples de traitement par lots azure][github_samples]).</span><span class="sxs-lookup"><span data-stu-id="ddb9e-341">Add logic toocheck for and allow hello use of an existing pool toospeed execution time (*hint*: check out `ArticleHelpers.cs` in hello [Microsoft.Azure.Batch.Samples.Common][github_samples_common] project in [azure-batch-samples][github_samples]).</span></span>

<span data-ttu-id="ddb9e-342">Maintenant que vous êtes familiarisé avec les flux de travail de base hello d’une solution de traitement par lots, il est toodig de temps dans toohello des fonctionnalités supplémentaires de hello service Batch.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-342">Now that you're familiar with hello basic workflow of a Batch solution, it's time toodig in toohello additional features of hello Batch service.</span></span>

* <span data-ttu-id="ddb9e-343">Hello de révision [les fonctionnalités de présentation d’Azure Batch](batch-api-basics.md) article, nous vous recommandons de si vous êtes de nouveau service toohello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-343">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
* <span data-ttu-id="ddb9e-344">Démarrer sur hello autres articles de développement de lot sous **développement approfondie** Bonjour [cursus lot][batch_learning_path].</span><span class="sxs-lookup"><span data-stu-id="ddb9e-344">Start on hello other Batch development articles under **Development in-depth** in hello [Batch learning path][batch_learning_path].</span></span>
* <span data-ttu-id="ddb9e-345">Extraire une implémentation différente de traitement de la charge de travail hello « N premiers mots » à l’aide de lot Bonjour [TopNWords] [ github_topnwords] exemple.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-345">Check out a different implementation of processing hello "top N words" workload by using Batch in hello [TopNWords][github_topnwords] sample.</span></span>
* <span data-ttu-id="ddb9e-346">Hello de révision Batch .NET [notes de publication](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) pour les modifications les plus récentes dans la bibliothèque de hello hello.</span><span class="sxs-lookup"><span data-stu-id="ddb9e-346">Review hello Batch .NET [release notes](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) for hello latest changes in hello library.</span></span>

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[github_dotnettutorial]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/DotNetTutorial
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_common]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/Common
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[net_api]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[net_api_storage]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudblobclient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobclient.aspx
[net_cloudblobcontainer]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudserviceconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudserviceconfiguration.aspx
[net_container_delete]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.deleteifexistsasync.aspx
[net_job]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_poolinfo]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.protocol.models.cloudjob.poolinformation.aspx
[net_joboperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.joboperations
[net_joboperations_terminatejob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_jobpreptask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_jobreltask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[net_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.aspx
[net_odatadetaillevel]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.odatadetaillevel.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_pooloperations]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.pooloperations
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_resourcefile_blobsource]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.blobsource.aspx
[net_sas_blob]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblob.getsharedaccesssignature.aspx
[net_sas_container]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.cloudblobcontainer.getsharedaccesssignature.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.resourcefiles.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_task_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.resourcefiles.aspx
[net_taskstate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.taskstate.aspx
[net_taskstatemonitor]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskstatemonitor.aspx
[net_thread_sleep]: https://msdn.microsoft.com/library/274eh01d(v=vs.110).aspx
[net_virtualmachineconfiguration]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.virtualmachineconfiguration.aspx
[nuget_packagemgr]: https://docs.nuget.org/consume/installing-nuget
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build
[storage_explorers]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/vs/
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-dotnet-get-started/batch_workflow_01_sm.png "Créer des conteneurs dans le Stockage Azure"
[2]: ./media/batch-dotnet-get-started/batch_workflow_02_sm.png "Tâche de chargement d’application et d’entrée (données) des fichiers toocontainers"
[3]: ./media/batch-dotnet-get-started/batch_workflow_03_sm.png "Créer un pool Batch"
[4]: ./media/batch-dotnet-get-started/batch_workflow_04_sm.png "Créer un travail Batch"
[5]: ./media/batch-dotnet-get-started/batch_workflow_05_sm.png "Ajouter des tâches toojob"
[6]: ./media/batch-dotnet-get-started/batch_workflow_06_sm.png "Surveiller les tâches"
[7]: ./media/batch-dotnet-get-started/batch_workflow_07_sm.png "Télécharger la sortie des tâches à partir de Storage"
[8]: ./media/batch-dotnet-get-started/batch_workflow_sm.png "Flux de travail de la solution Batch (diagramme complet)"
[9]: ./media/batch-dotnet-get-started/credentials_batch_sm.png "Informations d’identification de compte Batch dans le portail"
[10]: ./media/batch-dotnet-get-started/credentials_storage_sm.png "Informations d’identification de compte de stockage dans le portail"
[11]: ./media/batch-dotnet-get-started/batch_workflow_minimal_sm.png "Flux de travail de la solution Batch (diagramme minimal)"
