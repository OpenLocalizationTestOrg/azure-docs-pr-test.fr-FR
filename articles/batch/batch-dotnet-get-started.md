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
# <a name="get-started-building-solutions-with-hello-batch-client-library-for-net"></a>Prise en main la création de solutions avec la bibliothèque cliente de lot hello pour .NET

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.JS](batch-nodejs-get-started.md)
>
>

Principes fondamentaux de hello [Azure Batch] [ azure_batch] et hello [Batch .NET] [ net_api] bibliothèque dans cet article comme une étape de l’application d’exemple c# par les sujets abordés étape. Voyons comment exemple d’application hello exploite hello lot service tooprocess une charge de travail parallèle dans le cloud de hello et comment il interagit avec [Azure Storage](../storage/common/storage-introduction.md) intermédiaire de fichier et l’extraction. Vous allez en savoir un flux de travail courant lot application acquérir une compréhension de base du hello principaux composants du lot telles que les travaux, les tâches, les pools et nœuds de calcul.

![Flux de travail de la solution Batch (de base)][11]<br/>

## <a name="prerequisites"></a>Composants requis
Cet article suppose que vous avez acquis une connaissance pratique de C# et Visual Studio. Il suppose également que vous êtes en mesure de toosatisfy hello création exigences relatives aux comptes qui sont spécifiées ci-dessous pour Azure et hello lot et les services de stockage.

### <a name="accounts"></a>Comptes
* **Compte Azure** : si vous ne possédez pas encore d’abonnement Azure, [créez un compte Azure gratuit][azure_free_account].
* **Compte Batch**: une fois que vous disposez d’un abonnement Azure, [créez un compte Azure Batch](batch-account-create-portal.md).
* **Compte de stockage** : voir la section [Créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) de l’article [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).

> [!IMPORTANT]
> Prend en charge du lot actuellement *uniquement* hello **à usage général** type de compte de stockage, comme décrit à l’étape 5 de # [créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) dans [sur Azure comptes de stockage](../storage/common/storage-create-storage-account.md).
>
>

### <a name="visual-studio"></a>Visual Studio
Vous devez avoir **Visual Studio 2015 ou plus récente** exemple de projet toobuild hello. Vous pouvez trouver des versions gratuites et d’évaluation de Visual Studio dans hello [vue d’ensemble des produits Visual Studio][visual_studio].

### <a name="dotnettutorial-code-sample"></a>*DotNetTutorial*
Hello [DotNetTutorial] [ github_dotnettutorial] exemple est un des hello de nombreux exemples de code de lot trouvés dans hello [exemples de traitement par lots azure] [ github_samples] référentiel sur GitHub. Vous pouvez télécharger tous les exemples de hello en cliquant sur **Clone ou téléchargement > ZIP de téléchargement** sur la page d’accueil de référentiel hello, ou en cliquant sur hello [azure-lot-exemples-master.zip] [ github_samples_zip]lien direct. Une fois que vous avez extrait le contenu hello du fichier ZIP de hello, vous pouvez trouver des solutions de hello Bonjour suivant du dossier :

`\azure-batch-samples\CSharp\ArticleProjects\DotNetTutorial`

### <a name="azure-batch-explorer-optional"></a>Azure Batch Explorer (facultatif)
Hello [Azure Batch Explorer] [ github_batchexplorer] est un utilitaire gratuit qui est inclus dans hello [exemples de traitement par lots azure] [ github_samples] référentiel sur GitHub. Toocomplete non requis lors de ce didacticiel, il peut être utile lors du développement et débogage de solutions de votre lot.

## <a name="dotnettutorial-sample-project-overview"></a>Vue d’ensemble de l’exemple de projet DotNetTutorial
Hello *DotNetTutorial* exemple de code est une solution Visual Studio qui se compose de deux projets : **DotNetTutorial** et **TaskApplication**.

* **DotNetTutorial** est l’application hello client qui interagit avec tooexecute de services de stockage et de traitement par lots hello une charge de travail parallèle sur les nœuds de calcul (machines virtuelles). DotNetTutorial s’exécute sur votre station de travail locale.
* **TaskApplication** est hello programme qui s’exécute sur les nœuds de calcul dans le travail réel de tooperform Azure hello. Dans l’exemple hello, `TaskApplication.exe` analyse hello texte dans un fichier téléchargé depuis le stockage Azure (fichier d’entrée de hello). Ensuite, il génère un fichier texte (fichier de sortie hello) qui contient une liste de mots de trois premières hello qui s’affichent dans le fichier d’entrée de hello. Une fois qu’il crée le fichier de sortie hello, TaskApplication télécharge hello fichier tooAzure stockage. Cela rend application cliente de toohello disponible en téléchargement. TaskApplication s’exécute en parallèle sur plusieurs nœuds de calcul Bonjour service Batch.

Hello diagramme suivant illustre les opérations principales hello qui sont effectuées par l’application cliente de hello, *DotNetTutorial*et l’application hello qui est exécutée par les tâches de hello, *TaskApplication*. Ce flux de travail de base est caractéristique de nombreuses solutions de calcul créées avec Batch. Pendant qu’il ne présente pas toutes les fonctionnalités disponibles dans hello service Batch, presque tous les scénarios de traitement par lots inclut des parties de ce flux de travail.

![Exemple de flux de travail Batch][8]<br/>

[**Étape 1.**](#step-1-create-storage-containers) Créer des **conteneurs** dans le Stockage Blob Azure.<br/>
[**Étape 2.**](#step-2-upload-task-application-and-data-files) Fichiers d’application de tâche de téléchargement et toocontainers des fichiers d’entrée.<br/>
[**Étape 3.**](#step-3-create-batch-pool) Créer un **pool** Batch.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** Hello pool **StartTask** téléchargements hello toonodes (TaskApplication) des fichiers binaires de tâche dès qu’ils rejoignent le pool de hello.<br/>
[**Étape 4.**](#step-4-create-batch-job) Créer un **travail** Batch.<br/>
[**Étape 5.**](#step-5-add-tasks-to-job) Ajouter **tâches** toohello travail.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** les tâches de Hello sont planifiée tooexecute sur les nœuds.<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;**5b.** Chaque tâche télécharge ses données d’entrée depuis Stockage Azure, puis commence l’exécution.<br/>
[**Étape 6.**](#step-6-monitor-tasks) Surveiller les tâches.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** Comme les tâches sont effectuées, ils téléchargent leur tooAzure de données de sortie stockage.<br/>
[**Étape 7.**](#step-7-download-task-output) Télécharger la sortie des tâches à partir de Storage.

Comme mentionné, pas chaque solution de traitement exécute les étapes exactes et peut inclure bien plus encore, mais hello *DotNetTutorial* exemple d’application montre des processus courants trouvés dans une solution de traitement par lots.

## <a name="build-hello-dotnettutorial-sample-project"></a>Build hello *DotNetTutorial* exemple de projet
Avant de pouvoir exécuter correctement exemple hello, vous devez spécifier les informations d’identification du compte Batch et de stockage dans hello *DotNetTutorial* du projet `Program.cs` fichier. Si vous n’avez pas déjà fait, ouvrez la solution de hello dans Visual Studio en double-cliquant sur hello `DotNetTutorial.sln` fichier solution. Ou l’ouvrir à partir de Visual Studio à l’aide de hello **fichier > Ouvrir > Projet/Solution** menu.

Ouvrez `Program.cs` dans hello *DotNetTutorial* projet. Ajoutez ensuite vos informations d’identification comme spécifié haut hello du fichier de hello :

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
> Comme indiqué ci-dessus, vous devez spécifier actuellement les informations d’identification hello pour un **à usage général** compte de stockage dans le stockage Azure. Vos applications de traitement utilisent le stockage d’objets blob dans hello **à usage général** compte de stockage. Ne spécifiez pas les informations d’identification de hello pour un compte de stockage qui a été créé en sélectionnant hello *stockage d’objets Blob* type de compte.
>
>

Vous pouvez trouver vos informations d’identification compte Batch et de stockage dans le panneau de compte hello de chaque service Bonjour [portail Azure][azure_portal]:

![Traitement par lots les informations d’identification dans le portail de hello][9]
![informations d’identification de stockage dans le portail de hello][10]<br/>

Maintenant que vous avez mis à jour de projet de hello avec vos informations d’identification, cliquez sur la solution hello dans l’Explorateur de solutions, puis cliquez sur **générer la Solution**. Confirmer la restauration hello de tous les packages NuGet, si vous êtes invité.

> [!TIP]
> Si les packages NuGet hello ne sont pas automatiquement restaurés, ou si vous constatez des erreurs sur une panne toorestore hello les packages, assurez-vous que vous avez hello [Gestionnaire de Package NuGet] [ nuget_packagemgr] installé. Puis activez le téléchargement de hello des packages manquants. Consultez [l’activation de Package restauration au cours de génération] [ nuget_restore] tooenable téléchargement du package.
>
>

Bonjour les sections suivantes, nous réparties comme exemple d’application hello étapes hello qu’elle s’exécute tooprocess une charge de travail Bonjour service Batch et traitent de ces étapes en détail. Nous vous encourageons toorefer toohello solution ouverte dans Visual Studio pendant que vous travaillez Parcourir reste hello de cet article, étant donné que pas chaque ligne de code dans l’exemple hello est présenté.

Accédez haut toohello Hello `MainAsync` méthode Bonjour *DotNetTutorial* du projet `Program.cs` fichier toostart à l’étape 1. Chaque étape ci-dessous, puis à peu près suit la progression hello de méthode appelle `MainAsync`.

## <a name="step-1-create-storage-containers"></a>Étape 1 : créer des conteneurs de stockage
![Créer des conteneurs dans le service Stockage Azure][1]
<br/>

Batch prend en charge l’interaction avec Azure Storage. Les conteneurs dans votre compte de stockage fournissent des fichiers de hello requis par les tâches de hello qui s’exécutent dans votre compte Batch. les conteneurs de Hello fournissent également des données de sortie de hello toostore sur place qui produisent des tâches de hello. Hello première hello *DotNetTutorial* application cliente est créer trois conteneurs dans [stockage d’objets Blob Azure](../storage/common/storage-introduction.md):

* **application**: ce conteneur stockera application hello exécutée par les tâches de hello, ainsi qu’une de ses dépendances, comme les DLL.
* **d’entrée**: tâches téléchargera tooprocess de fichiers de données hello hello *d’entrée* conteneur.
* **sortie**: lorsque les tâches de terminer le traitement du fichier d’entrée, ils téléchargeront hello résultats toohello *sortie* conteneur.

Dans l’ordre des toointeract avec un stockage de compte et de créer des conteneurs, nous utilisons hello [bibliothèque cliente de stockage Azure pour .NET][net_api_storage]. Nous créons un compte toohello de référence avec [CloudStorageAccount][net_cloudstorageaccount]et de celui de créer un [CloudBlobClient][net_cloudblobclient]:

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

Nous utilisons hello `blobClient` référence dans toute application hello et passez-le en tant que paramètre tooseveral méthodes. Est un exemple dans un bloc de code hello qui suit immédiatement hello ci-dessus, où nous appeler `CreateContainerIfNotExistAsync` tooactually de créer des conteneurs de hello.

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

Une fois que les conteneurs hello ont été créées, application hello peut maintenant télécharger des fichiers de hello qui seront utilisés par les tâches hello.

> [!TIP]
> [Comment toouse stockage d’objets Blob à partir de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) fournit une bonne vue d’ensemble de l’utilisation de conteneurs Azure Storage et les objets BLOB. Il doit être haut hello de votre liste de lecture commencer à utiliser avec le lot.
>
>

## <a name="step-2-upload-task-application-and-data-files"></a>Étape 2 : charger les fichiers d’application de tâche et les fichiers de données
![Tâche de chargement d’application et d’entrée (données) des fichiers toocontainers][2]
<br/>

Dans le fichier de hello Téléchargez opération, *DotNetTutorial* définit tout d’abord les collections de **application** et **d’entrée** chemins d’accès de fichiers tels qu’ils existent sur l’ordinateur local de hello. Puis il les télécharge ces conteneurs toohello de fichiers que vous avez créé à l’étape précédente de hello.

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

Il existe deux méthodes dans `Program.cs` impliquées dans le processus de téléchargement hello :

* `UploadFilesToContainerAsync`: Cette méthode retourne une collection de [ResourceFile] [ net_resourcefile] (voir ci-dessous) des objets et en interne les appels `UploadFileToContainerAsync` tooupload chaque fichier qui est passé dans hello *filePaths* paramètre.
* `UploadFileToContainerAsync`: Cette méthode hello réellement effectue le téléchargement du fichier hello et crée hello est [ResourceFile] [ net_resourcefile] objets. Après avoir téléchargé le fichier de hello, il obtient une signature d’accès partagé (SAP) pour le fichier de hello et retourne un objet ResourceFile qui le représente. Les signatures d’accès partagé sont également décrites ci-dessous.

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

### <a name="resourcefiles"></a>Objets ResourceFile
A [ResourceFile] [ net_resourcefile] fournit des tâches dans un lot avec fichier de tooa hello URL dans le stockage Azure qui est téléchargé tooa nœud de calcul avant l’exécution de cette tâche. Hello [ResourceFile.BlobSource] [ net_resourcefile_blobsource] propriété spécifie une URL complète du fichier de hello hello telle qu’elle existe dans le stockage Azure. URL de Hello peut-être également inclure une signature d’accès partagé (SAS) qui fournit un accès sécurisé toohello fichier. La propriété *ResourceFiles* est utilisée par la plupart des types de tâche de Batch .NET, notamment :

* [CloudTask][net_task]
* [StartTask][net_pool_starttask]
* [JobPreparationTask][net_jobpreptask]
* [JobReleaseTask][net_jobreltask]

Hello DotNetTutorial exemple d’application n’utilise pas hello JobPreparationTask ou JobReleaseTask les types de tâches, mais vous pouvez en savoir plus sur les [nœuds de calcul des tâches de préparation et l’achèvement de projet sur Azure Batch exécuter](batch-job-prep-release.md).

### <a name="shared-access-signature-sas"></a>Signature d’accès partagé (SAP)
Accès partagé, les signatures sont des chaînes qui, lorsque inclus dans le cadre d’une URL, fournir un accès sécurisé toocontainers et les objets BLOB dans le stockage Azure. Hello DotNetTutorial application utilise les deux objets blob et conteneur partagé URL de signature d’accès et montre comment tooobtain ces partagés accéder aux chaînes de signature à partir de hello service de stockage.

* **Signatures d’accès partagé d’objets BLOB**: StartTask du pool hello dans DotNetTutorial utilise des signatures d’accès partagé de blob lors du téléchargement de fichiers binaires d’application hello et les fichiers de données d’entrée à partir du stockage (voir étape 3 ci-dessous). Hello `UploadFileToContainerAsync` méthode dans du DotNetTutorial `Program.cs` contient le code hello qui obtient la signature d’accès partagé de l’objet blob. Elle le fait en appelant [CloudBlob.GetSharedAccessSignature][net_sas_blob].
* **Signatures d’accès partagé de conteneur**: que chaque tâche a terminé son travail sur le nœud de calcul hello, il télécharge sa toohello de fichier de sortie *sortie* conteneur dans le stockage Azure. toodo TaskApplication utilise ainsi une signature d’accès partagé de conteneur qui fournit un accès en écriture toohello conteneur en tant que partie du chemin d’accès hello lorsqu’il télécharge les fichier hello. Signature d’accès partagé de conteneur hello obtention s’effectue de la même manière que lorsque l’objet blob de hello signature d’accès partagé. Dans DotNetTutorial, vous constaterez que hello `GetContainerSasUrl` les appels de méthode d’assistance [CloudBlobContainer.GetSharedAccessSignature] [ net_sas_container] toodo donc. Vous allez en savoir plus sur la façon dont TaskApplication utilise le conteneur de hello signature d’accès partagé dans « étape 6 : tâches de surveillance. »

> [!TIP]
> Extraction de série en deux parties hello sur les signatures d’accès partagé, [partie 1 : hello de présentation partagé le modèle de signature (SAP) d’accès](../storage/common/storage-dotnet-shared-access-signature-part-1.md) et [partie 2 : créer et utiliser une signature d’accès partagé (SAS) avec le stockage d’objets Blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn plus sur l’envoi de toodata un accès sécurisé dans votre compte de stockage.
>
>

## <a name="step-3-create-batch-pool"></a>Étape 3 : créer le pool Batch
![Créer un pool Batch][3]
<br/>

Un **pool** Batch est une collection de nœuds de calcul (machines virtuelles) sur lequel Batch exécute les tâches d’un travail.

Après avoir téléchargé l’application hello et les fichiers de données toohello compte de stockage avec l’API de stockage Azure, *DotNetTutorial* commencer des appels toohello lot service avec les API fournies par la bibliothèque de lot .NET hello. Hello code crée d’abord un [BatchClient][net_batchclient]:

```csharp
BatchSharedKeyCredentials cred = new BatchSharedKeyCredentials(
    BatchAccountUrl,
    BatchAccountName,
    BatchAccountKey);

using (BatchClient batchClient = BatchClient.Open(cred))
{
    ...
```

Ensuite, exemple hello crée un pool de nœuds de calcul dans le compte de traitement par lots hello par un appel trop`CreatePoolIfNotExistsAsync`. `CreatePoolIfNotExistsAsync`utilise hello [BatchClient.PoolOperations.CreatePool] [ net_pool_create] méthode toocreate un nouveau pool Bonjour service Batch :

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

Lorsque vous créez un pool avec [CreatePool][net_pool_create], vous spécifiez plusieurs paramètres tels que nombre hello de nœuds de calcul, hello [taille des nœuds de hello](../cloud-services/cloud-services-sizes-specs.md), et hello nœuds d’exploitation système. Dans *DotNetTutorial*, nous utilisons [CloudServiceConfiguration] [ net_cloudserviceconfiguration] toospecify Windows Server 2012 R2 à partir de [Services de cloud computing](../cloud-services/cloud-services-guestos-update-matrix.md). 

Vous pouvez également créer des pools de nœuds de calcul qui sont des Machines virtuelles (VM) Azure en spécifiant hello [VirtualMachineConfiguration] [ net_virtualmachineconfiguration] pour le pool. Vous pouvez créer un pool de nœuds de calcul de machines virtuelles à partir d’[images Windows ou Linux](batch-linux-nodes.md). source de Hello pour vos images de machine virtuelle peut être :

- Hello [Azure Marketplace de Machines virtuelles][vm_marketplace], qui fournit des images Windows et Linux qui sont prêts à l’emploi. 
- Une image personnalisée que vous préparez et fournissez. Pour en savoir plus sur les images personnalisées, consultez [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool) (Développer des solutions de calcul parallèles à grande échelle avec Batch).

> [!IMPORTANT]
> Les ressources de calcul dans Batch vous sont facturées. toominimize des coûts, vous pouvez diminuer `targetDedicatedComputeNodes` too1 avant d’exécuter les exemples hello.
>
>

Avec ces propriétés de nœud physique, vous pouvez également spécifier un [StartTask] [ net_pool_starttask] pour le pool de hello. Hello StartTask s’exécute sur chaque nœud de ce nœud rejoint le pool de hello, chaque fois qu’un nœud est redémarré. Hello StartTask est particulièrement utile pour installer des applications de calcul nœuds préalable toohello l’exécution de tâches. Par exemple, si vos tâches de traitement des données à l’aide de scripts Python, vous pouvez utiliser un tooinstall StartTask Python sur les nœuds de calcul hello.

Dans cet exemple d’application, hello StartTask copie les fichiers de hello qu’il télécharge à partir du stockage (qui sont spécifié à l’aide de hello [StartTask][net_starttask].[ ResourceFiles] [ net_starttask_resourcefiles] propriété) à partir du répertoire partagé toohello de répertoire travail hello StartTask qui *tous les* en cours d’exécution sur le nœud de hello puissent y accéder. Pour l’essentiel, cette copie `TaskApplication.exe` et toohello de ses dépendances répertoire partagé sur chaque nœud comme nœud de hello rejoint le pool de hello, afin que toutes les tâches qui s’exécutent sur le nœud de hello puissent y accéder.

> [!TIP]
> Hello **des packages d’application** fonctionnalité de traitement par lots Azure fournit une autre façon tooget votre application sur les nœuds de calcul hello dans un pool. Consultez [déployer des nœuds de toocompute d’applications avec les packages d’applications de traitement par lots](batch-application-packages.md) pour plus d’informations.
>
>

Remarquables dans l’extrait de code hello ci-dessus est également utiliser deux variables d’environnement Bonjour hello *CommandLine* propriété Hello StartTask : `%AZ_BATCH_TASK_WORKING_DIR%` et `%AZ_BATCH_NODE_SHARED_DIR%`. Chaque nœud de calcul au sein d’un pool de traitement par lots est automatiquement configuré avec plusieurs variables d’environnement qui sont tooBatch spécifique. Tout processus qui est exécutée par une tâche a des variables d’environnement toothese accès.

> [!TIP]
> toofind plus d’informations sur les variables d’environnement hello qui sont disponibles sur les nœuds de calcul dans un pool de traitement par lots et des informations sur les répertoires de travail tâche, consultez hello [paramètres d’environnement pour les tâches](batch-api-basics.md#environment-settings-for-tasks) et [fichiers et répertoires ](batch-api-basics.md#files-and-directories) sections Bonjour [vue d’ensemble de lot pour les développeurs](batch-api-basics.md).
>
>

## <a name="step-4-create-batch-job"></a>Étape 4 : créer un travail Batch
![Créer un travail Batch][4]<br/>

Un **travail** Batch constitue un ensemble de tâches et est associé à un pool de nœuds de calcul. tâches de Hello dans un travail s’exécutent sur les nœuds de calcul du pool hello associé.

Vous pouvez utiliser une tâche pour l’organisation et le suivi des tâches dans les charges de travail, mais également pour imposer certaines contraintes--par exemple hello durée d’exécution pour le travail de hello (et par extension, ses tâches), ainsi que la priorité dans les travaux de tooother relation Bonjour lot compte. Dans cet exemple, toutefois, les travaux de hello est associé uniquement à pool hello qui a été créé à l’étape 3 de #. Aucune propriété supplémentaire n’est configurée.

Tous les travaux Batch sont associés à un pool spécifique. Cette association indique les nœuds de hello tâches seront exécutent sur. Vous spécifiez en utilisant hello [CloudJob.PoolInformation] [ net_job_poolinfo] propriété, comme indiqué dans l’extrait de code hello ci-dessous.

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

Maintenant qu’un travail a été créé, les tâches sont ajoutées travail hello de tooperform.

## <a name="step-5-add-tasks-toojob"></a>Étape 5 : Ajouter des tâches toojob
![Ajouter des tâches toojob][5]<br/>
*(1) tâches sont ajoutés toohello travail, tâches de hello (2) sont planifiée toorun sur les nœuds et les tâches hello (3) téléchargement tooprocess de fichiers de données hello*

Lot **tâches** sont des nœuds de calcul hello unités de travail individuelles qui s’exécutent sur hello. Une tâche a une ligne de commande et exécute les scripts hello ou exécutables que vous spécifiez dans cette ligne de commande.

tooactually effectuer un travail, de tâches doivent être ajoutées à une tâche tooa. Chaque [CloudTask] [ net_task] est configuré à l’aide d’une propriété de ligne de commande et [ResourceFiles] [ net_task_resourcefiles] (comme avec la tâche de début du pool hello) qui tâche Hello télécharge toohello nœud avant sa ligne de commande est exécutée automatiquement. Bonjour *DotNetTutorial* exemple de projet, chaque tâche traite un seul fichier. Par conséquent, sa collection ResourceFiles contient un seul élément.

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
> Lorsque leur accès aux variables d’environnement telles que `%AZ_BATCH_NODE_SHARED_DIR%` ou exécuter une application introuvable dans du nœud hello `PATH`, lignes de commande de tâche doivent être précédés `cmd /c`. Explicitement cela exécute l’interpréteur de commandes hello et lui demander de tooterminate après avoir effectué votre commande. Cette exigence n’est pas nécessaire si vos tâches exécutent une application dans du nœud hello `PATH` (tel que *robocopy.exe* ou *powershell.exe*) et aucune variable d’environnement n’est utilisés.
>
>

Au sein de hello `foreach` boucle dans l’extrait de code hello ci-dessus, vous pouvez voir que la ligne de commande hello pour la tâche hello est construite telles que les trois arguments de ligne de commande sont passés trop*TaskApplication.exe*:

1. Hello **premier argument** est le chemin de hello de tooprocess de fichier hello. Ce fichier de toohello de chemin d’accès local hello est telle qu’elle existe sur le nœud de hello. Lorsque hello objet ResourceFile dans `UploadFileToContainerAsync` tout d’abord créée ci-dessus, le nom de fichier hello a été utilisée pour cette propriété (en tant que paramètre toohello ResourceFile constructeur). Cela indique que hello fichier se trouve dans hello même répertoire que *TaskApplication.exe*.
2. Hello **le second argument** Spécifie que haut hello *N* mots doivent être écrits en fichier de sortie toohello. Dans l’exemple hello, il est codé en dur afin que les mots de trois principaux hello sont écrites de fichier de sortie toohello.
3. Hello **troisième argument** est la signature d’accès partagé hello (SAS) qui fournit un accès en écriture toohello **sortie** conteneur dans le stockage Azure. *TaskApplication.exe* utilise cette partagée des URL de signature d’accès lorsqu’il télécharge tooAzure de fichier de sortie hello stockage. Vous trouverez le code de hello pour ce Bonjour `UploadFileToContainer` méthode de projet hello TaskApplication `Program.cs` fichier :

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

## <a name="step-6-monitor-tasks"></a>Étape 6 : surveiller les tâches
![Surveiller les tâches][6]<br/>
*Hello client application (1) analyses hello les tâches d’achèvement et état de réussite et (2) hello tâches téléchargement résultat données tooAzure stockage*

Lorsque les tâches sont ajoutées tooa travail, ils sont en file d’attente et planifiés pour l’exécution sur des nœuds de calcul dans le pool hello associé hello travail automatiquement. Selon les paramètres que vous spécifiez hello, lot gère queuing à toutes les tâches, la planification, une nouvelle tentative et autres tâches d’administration de tâche pour vous.

Il existe de nombreuses approches toomonitoring exécution de la tâche. DotNetTutorial en présente un exemple simple signalant uniquement les états d’achèvement et d’échec ou de réussite des tâches. Au sein de hello `MonitorTasks` méthode dans du DotNetTutorial `Program.cs`, il existe trois concepts Batch .NET qui garantissent la discussion. Ils sont répertoriés ci-dessous dans leur ordre d’apparition :

1. **ODATADetailLevel** : la spécification d’un élément [ODATADetailLevel][net_odatadetaillevel] dans les opérations de liste (telles que l’obtention d’une liste des tâches d’un travail) est primordiale pour garantir les performances de l’application Batch. Ajouter [interroger le service de traitement par lots Azure hello efficacement](batch-efficient-list-queries.md) tooyour lecture de la liste si vous prévoyez d’effectuer toute sorte de surveillance de l’état au sein de vos applications de traitement par lots.
2. **TaskStateMonitor** : l’élément [TaskStateMonitor][net_taskstatemonitor] fournit aux applications Batch .NET des utilitaires d’assistance pour la surveillance des états de tâche. Dans `MonitorTasks`, *DotNetTutorial* attend que toutes les tâches tooreach [TaskState.Completed] [ net_taskstate] dans un intervalle de temps. Puis il met fin à la tâche de hello.
3. **TerminateJobAsync**: arrêt d’un travail avec [JobOperations.TerminateJobAsync] [ net_joboperations_terminatejob] (ou hello blocage JobOperations.TerminateJob) marque ce travail comme terminé. Il est essentiel toodo, donc si votre solution de traitement par lots utilise un [JobReleaseTask][net_jobreltask]. Il s’agit d’un type spécial de tâche, qui est décrit dans [Tâches d’achèvement et de préparation des travaux](batch-job-prep-release.md).

Hello `MonitorTasks` méthode à partir de *DotNetTutorial*de `Program.cs` apparaît ci-dessous :

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

## <a name="step-7-download-task-output"></a>Étape 7 : télécharger la sortie des tâches
![Télécharger la sortie des tâches à partir du service Stockage][7]<br/>

Maintenant que hello tâche terminée, sortie hello des tâches de hello peut être téléchargé depuis le stockage Azure. Cette opération s’effectue avec un appel trop`DownloadBlobsFromContainerAsync` dans *DotNetTutorial*de `Program.cs`:

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
> Hello appel trop`DownloadBlobsFromContainerAsync` Bonjour *DotNetTutorial* application spécifie que les fichiers hello doivent être téléchargé tooyour `%TEMP%` dossier. Pensez toomodify libre cette sortie d’emplacement.
>
>

## <a name="step-8-delete-containers"></a>Étape 8 : supprimer les conteneurs
Vous êtes facturé pour les données qui résident dans le stockage Azure, il est toujours une bonne idée tooremove les objets BLOB qui ne sont plus nécessaires pour vos traitements par lots. Dans de DotNetTutorial `Program.cs`, cela est effectué avec la méthode d’assistance de toohello trois appels `DeleteContainerAsync`:

```csharp
// Clean up Storage resources
await DeleteContainerAsync(blobClient, appContainerName);
await DeleteContainerAsync(blobClient, inputContainerName);
await DeleteContainerAsync(blobClient, outputContainerName);
```

méthode Hello elle-même simplement Obtient un conteneur toohello de référence, puis appelle [CloudBlobContainer.DeleteIfExistsAsync][net_container_delete]:

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

## <a name="step-9-delete-hello-job-and-hello-pool"></a>Étape 9 : Supprimer le travail de hello et pool de hello
À l’étape finale de hello, vous êtes invité à toodelete hello travail et hello le pool qui ont été créés par l’application de DotNetTutorial hello. Bien que vous ne soyez pas facturé pour les travaux et les tâches à proprement parler, les nœuds de calcul vous *sont* facturés. Par conséquent, nous vous conseillons d’affecter les nœuds uniquement en fonction des besoins. La suppression des pools inutilisés peut être incluse dans votre processus de maintenance.

Hello BatchClient [JobOperations] [ net_joboperations] et [PoolOperations] [ net_pooloperations] ont tous deux des méthodes de suppression correspondantes, qui sont appelées si utilisateur de Hello confirme la suppression :

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
> N’oubliez pas que les ressources de calcul vous sont facturées et que la suppression des pools inutilisés vous permet de réduire les coûts. En outre, n’oubliez pas que la suppression d’un pool supprime tous les nœuds de calcul dans ce pool, et que toutes les données sur les nœuds hello seront irrécupérables après la suppression d’un pool de hello.
>
>

## <a name="run-hello-dotnettutorial-sample"></a>Exécutez hello *DotNetTutorial* exemple
Lorsque vous exécutez exemple d’application hello, la sortie de console hello sera similaire toohello suivant. Pendant l’exécution, vous rencontrerez une pause à `Awaiting task completion, timeout in 00:30:00...` tandis que les nœuds de calcul du pool hello sont démarrés. Hello d’utilisation [portail Azure] [ azure_portal] toomonitor votre pool, nœuds de calcul, tâche et pendant et après l’exécution des tâches. Hello d’utilisation [portail Azure] [ azure_portal] ou hello [Azure Storage Explorer] [ storage_explorers] tooview hello ressources de stockage (conteneurs et objets BLOB) qui sont créé par l’application hello.

Temps d’exécution par défaut est **environ 5 minutes** lorsque vous exécutez des application hello dans sa configuration par défaut.

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

## <a name="next-steps"></a>Étapes suivantes
Estimez les modifications toomake libre trop*DotNetTutorial* et *TaskApplication* tooexperiment avec différents scénarios de calcul. Par exemple, essayez d’ajouter un délai d’exécution trop*TaskApplication*, par exemple comme avec [Thread.Sleep][net_thread_sleep], toosimulate longue des tâches et les surveiller dans le portail de hello. Essayez d’ajouter des tâches plus ou en ajustant de nombre hello de nœuds de calcul. Ajouter toocheck logique pour et autoriser l’utilisation de hello de durée d’exécution de toospeed pool existant (*indicateur*: extraire `ArticleHelpers.cs` Bonjour [Microsoft.Azure.Batch.Samples.Common] [ github_samples_common] projet [exemples de traitement par lots azure][github_samples]).

Maintenant que vous êtes familiarisé avec les flux de travail de base hello d’une solution de traitement par lots, il est toodig de temps dans toohello des fonctionnalités supplémentaires de hello service Batch.

* Hello de révision [les fonctionnalités de présentation d’Azure Batch](batch-api-basics.md) article, nous vous recommandons de si vous êtes de nouveau service toohello.
* Démarrer sur hello autres articles de développement de lot sous **développement approfondie** Bonjour [cursus lot][batch_learning_path].
* Extraire une implémentation différente de traitement de la charge de travail hello « N premiers mots » à l’aide de lot Bonjour [TopNWords] [ github_topnwords] exemple.
* Hello de révision Batch .NET [notes de publication](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/Batch/DataPlane/changelog.md#azurebatch-release-notes) pour les modifications les plus récentes dans la bibliothèque de hello hello.

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
