---
title: "Didacticiel : utiliser la bibliothèque cliente Azure Batch pour Node.js | Microsoft Docs"
description: "Découvrez les concepts de base d’Azure Batch et créez une solution simple à l’aide de Node.js."
services: batch
author: shwetams
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: nodejs
ms.topic: hero-article
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: shwetams
ms.openlocfilehash: c48171d8634a651718a0775183414f463c6a468c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-batch-sdk-for-nodejs"></a><span data-ttu-id="cc761-103">Bien démarrer avec le Kit de développement logiciel (SDK) Batch pour Node.js</span><span class="sxs-lookup"><span data-stu-id="cc761-103">Get started with Batch SDK for Node.js</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cc761-104">.NET</span><span class="sxs-lookup"><span data-stu-id="cc761-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="cc761-105">Python</span><span class="sxs-lookup"><span data-stu-id="cc761-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="cc761-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="cc761-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="cc761-107">Découvrez les concepts de base de création d’un client Batch dans Node.js à l’aide du [Kit de développement logiciel (SDK) Node.js pour Azure Batch](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span><span class="sxs-lookup"><span data-stu-id="cc761-107">Learn the basics of building a Batch client in Node.js using [Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span></span> <span data-ttu-id="cc761-108">Nous allons présenter pas à pas un scénario pour une application Batch, puis la configurer à l’aide d’un client Node.js.</span><span class="sxs-lookup"><span data-stu-id="cc761-108">We take a step by step approach of understanding a scenario for a batch application and then setting it up using a Node.js client.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="cc761-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cc761-109">Prerequisites</span></span>
<span data-ttu-id="cc761-110">Cet article suppose que vous avez acquis une connaissance pratique de Node.js et que vous êtes familiarisé avec Linux.</span><span class="sxs-lookup"><span data-stu-id="cc761-110">This article assumes that you have a working knowledge of Node.js and familiarity with Linux.</span></span> <span data-ttu-id="cc761-111">Il suppose également que vous disposez d’un compte Azure configuré avec des droits d’accès pour créer des services Batch et Stockage.</span><span class="sxs-lookup"><span data-stu-id="cc761-111">It also assumes that you have an Azure account setup with access rights to create Batch and Storage services.</span></span>

<span data-ttu-id="cc761-112">Nous vous recommandons de lire [Présentation technique d’Azure Batch](batch-technical-overview.md) avant d’effectuer les étapes présentées dans cet article.</span><span class="sxs-lookup"><span data-stu-id="cc761-112">We recommend reading [Azure Batch Technical Overview](batch-technical-overview.md) before you go through the steps outlined this article.</span></span>

## <a name="the-tutorial-scenario"></a><span data-ttu-id="cc761-113">Scénario du didacticiel</span><span class="sxs-lookup"><span data-stu-id="cc761-113">The tutorial scenario</span></span>
<span data-ttu-id="cc761-114">Laissez-nous vous présenter le scénario de flux de travail Batch.</span><span class="sxs-lookup"><span data-stu-id="cc761-114">Let us understand the batch workflow scenario.</span></span> <span data-ttu-id="cc761-115">Nous avons écrit un script simple dans Python qui permet de télécharger tous les fichiers csv à partir d’un conteneur de stockage Blob Azure et de les convertir au format JSON.</span><span class="sxs-lookup"><span data-stu-id="cc761-115">We have a simple script written in Python that downloads all csv files from an Azure Blob storage container and converts them to JSON.</span></span> <span data-ttu-id="cc761-116">Pour traiter plusieurs conteneurs du compte de stockage en parallèle, nous pouvons déployer le script en tant que travail Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="cc761-116">To process multiple storage account containers in parallel, we can deploy the script as an Azure Batch job.</span></span>

## <a name="azure-batch-architecture"></a><span data-ttu-id="cc761-117">Architecture Azure Batch</span><span class="sxs-lookup"><span data-stu-id="cc761-117">Azure Batch Architecture</span></span>
<span data-ttu-id="cc761-118">Le diagramme suivant illustre la façon dont nous pouvons mettre à l’échelle le script Python à l’aide d’Azure Batch et d’un client Node.js.</span><span class="sxs-lookup"><span data-stu-id="cc761-118">The following diagram depicts how we can scale the Python script using Azure Batch and a Node.js client.</span></span>

![Scénario Azure Batch](./media/batch-nodejs-get-started/BatchScenario.png)

<span data-ttu-id="cc761-120">Le client Node.js déploie un traitement par lots avec une tâche de préparation (expliquée en détail plus loin) ainsi qu’un ensemble de tâches en fonction du nombre de conteneurs du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="cc761-120">The node.js client deploys a batch job with a preparation task (explained in detail later) and a set of tasks depending on the number of containers in the storage account.</span></span> <span data-ttu-id="cc761-121">Vous pouvez télécharger les scripts à partir du référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="cc761-121">You can download the scripts from the github repository.</span></span>

* [<span data-ttu-id="cc761-122">Client Node.js</span><span class="sxs-lookup"><span data-stu-id="cc761-122">Node.js client</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [<span data-ttu-id="cc761-123">Scripts Shell de la tâche de préparation</span><span class="sxs-lookup"><span data-stu-id="cc761-123">Preparation task shell scripts</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [<span data-ttu-id="cc761-124">Processeur de fichiers csv Python au format JSON</span><span class="sxs-lookup"><span data-stu-id="cc761-124">Python csv to JSON processor</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> <span data-ttu-id="cc761-125">Le client Node.js dans le lien spécifié ne contient pas de code spécifique pour être déployé comme application de fonction Azure.</span><span class="sxs-lookup"><span data-stu-id="cc761-125">The Node.js client in the link specified does not contain specific code to be deployed as an Azure function app.</span></span> <span data-ttu-id="cc761-126">Vous pouvez vous reporter aux liens suivants pour connaître les instructions à suivre pour en créer une.</span><span class="sxs-lookup"><span data-stu-id="cc761-126">You can refer to the following links for instructions to create one.</span></span>
> - [<span data-ttu-id="cc761-127">Créer une application de fonction</span><span class="sxs-lookup"><span data-stu-id="cc761-127">Create function app</span></span>](../azure-functions/functions-create-first-azure-function.md)
> - [<span data-ttu-id="cc761-128">Créer une fonction de déclencheur de minuteur</span><span class="sxs-lookup"><span data-stu-id="cc761-128">Create timer trigger function</span></span>](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-the-application"></a><span data-ttu-id="cc761-129">Création de l'application</span><span class="sxs-lookup"><span data-stu-id="cc761-129">Build the application</span></span>

<span data-ttu-id="cc761-130">À présent, laissez-nous suivre la procédure étape par étape de création du client Node.js :</span><span class="sxs-lookup"><span data-stu-id="cc761-130">Now, let us follow the process step by step into building the Node.js client:</span></span>

### <a name="step-1-install-azure-batch-sdk"></a><span data-ttu-id="cc761-131">Étape 1 : installer le Kit de développement logiciel (SDK) Azure Batch</span><span class="sxs-lookup"><span data-stu-id="cc761-131">Step 1: Install Azure Batch SDK</span></span>

<span data-ttu-id="cc761-132">Vous pouvez installer le Kit de développement logiciel (SDK) Azure Batch pour Node.js à l’aide de la commande npm install.</span><span class="sxs-lookup"><span data-stu-id="cc761-132">You can install Azure Batch SDK for Node.js using the npm install command.</span></span>

`npm install azure-batch`

<span data-ttu-id="cc761-133">Cette commande installe la dernière version du Kit de développement logiciel (SDK) Azure Batch pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="cc761-133">This command installs the latest version of azure-batch node SDK.</span></span>

>[!Tip]
> <span data-ttu-id="cc761-134">Dans une application Azure Function App, vous pouvez accéder à « Kudu Console » dans l’onglet Paramètres de la fonction Azure pour exécuter les commandes npm install,</span><span class="sxs-lookup"><span data-stu-id="cc761-134">In an Azure Function app, you can go to "Kudu Console" in the Azure function's Settings tab to run the npm install commands.</span></span> <span data-ttu-id="cc761-135">dans ce cas, pour installer le Kit de développement logiciel (SDK) Azure Batch pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="cc761-135">In this case to install Azure Batch SDK for Node.js.</span></span>
>
>

### <a name="step-2-create-an-azure-batch-account"></a><span data-ttu-id="cc761-136">Étape 2 : Créer un compte Azure Batch</span><span class="sxs-lookup"><span data-stu-id="cc761-136">Step 2: Create an Azure Batch account</span></span>

<span data-ttu-id="cc761-137">Vous pouvez le créer à partir du [portail Azure](batch-account-create-portal.md) ou de la ligne de commande ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure CLI](https://docs.microsoft.com/cli/azure/overview)).</span><span class="sxs-lookup"><span data-stu-id="cc761-137">You can create it from the [Azure portal](batch-account-create-portal.md) or from command line ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).</span></span>

<span data-ttu-id="cc761-138">Ci-après figurent les commandes permettant d’en créer un via Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="cc761-138">Following are the commands to create one through Azure CLI.</span></span>

<span data-ttu-id="cc761-139">Créez un groupe de ressources. Ignorez cette étape si vous en avez déjà un là où vous souhaitez créer le compte Batch :</span><span class="sxs-lookup"><span data-stu-id="cc761-139">Create a Resource Group, skip this step if you already have one where you want to create the Batch Account:</span></span>

`az group create -n "<resource-group-name>" -l "<location>"`

<span data-ttu-id="cc761-140">Créez ensuite un compte Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="cc761-140">Next, create an Azure Batch account.</span></span>

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="cc761-141">Chaque compte Batch possède ses clés d’accès correspondantes.</span><span class="sxs-lookup"><span data-stu-id="cc761-141">Each Batch account has its corresponding access keys.</span></span> <span data-ttu-id="cc761-142">Ces clés sont nécessaires pour créer d’autres ressources dans un compte Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="cc761-142">These keys are needed to create further resources in Azure batch account.</span></span> <span data-ttu-id="cc761-143">Pour un environnement de production, il est conseillé d’utiliser Azure Key Vault pour stocker ces clés.</span><span class="sxs-lookup"><span data-stu-id="cc761-143">A good practice for production environment is to use Azure Key Vault to store these keys.</span></span> <span data-ttu-id="cc761-144">Vous pouvez alors créer un principal de service pour l’application.</span><span class="sxs-lookup"><span data-stu-id="cc761-144">You can then create a Service principal for the application.</span></span> <span data-ttu-id="cc761-145">En utilisant ce principal de service, l’application peut créer un jeton OAuth pour les clés d’accès dans le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="cc761-145">Using this service principal the application can create an OAuth token to access keys from the key vault.</span></span>

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="cc761-146">Copiez et stockez la clé à utiliser dans les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="cc761-146">Copy and store the key to be used in the subsequent steps.</span></span>

### <a name="step-3-create-an-azure-batch-service-client"></a><span data-ttu-id="cc761-147">Étape 3 : créer un client du service Azure Batch</span><span class="sxs-lookup"><span data-stu-id="cc761-147">Step 3: Create an Azure Batch service client</span></span>
<span data-ttu-id="cc761-148">L’extrait de code suivant importe tout d’abord le module Node.js pour Azure Batch, puis crée un client du service Batch.</span><span class="sxs-lookup"><span data-stu-id="cc761-148">Following code snippet first imports the azure-batch Node.js module and then creates a Batch Service client.</span></span> <span data-ttu-id="cc761-149">Vous devez d’abord créer un objet SharedKeyCredentials avec la clé du compte Batch copiée à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="cc761-149">You need to first create a SharedKeyCredentials object with the Batch account key copied from the previous step.</span></span>

```nodejs
// Initializing Azure Batch variables

var batch = require('azure-batch');

var accountName = '<azure-batch-account-name>';

var accountKey = '<account-key-downloaded>';

var accountUrl = '<account-url>'

// Create Batch credentials object using account name and account key

var credentials = new batch.SharedKeyCredentials(accountName,accountKey);

// Create Batch service client

var batch_client = new batch.ServiceClient(credentials,accountUrl);

```

<span data-ttu-id="cc761-150">L’URI Azure Batch se trouve dans l’onglet Vue d’ensemble du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cc761-150">The Azure Batch URI can be found in the Overview tab of the Azure portal.</span></span> <span data-ttu-id="cc761-151">Son format est le suivant :</span><span class="sxs-lookup"><span data-stu-id="cc761-151">It is of the format:</span></span>

`https://accountname.location.batch.azure.com`

<span data-ttu-id="cc761-152">Reportez-vous à la capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="cc761-152">Refer to the screenshot:</span></span>

![URI Azure Batch](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a><span data-ttu-id="cc761-154">Étape 4 : créer un pool Azure Batch</span><span class="sxs-lookup"><span data-stu-id="cc761-154">Step 4: Create an Azure Batch pool</span></span>
<span data-ttu-id="cc761-155">Un pool Azure Batch se compose de plusieurs machines virtuelles (également appelées nœuds Batch).</span><span class="sxs-lookup"><span data-stu-id="cc761-155">An Azure Batch pool consists of multiple VMs (also known as Batch Nodes).</span></span> <span data-ttu-id="cc761-156">Le service Azure Batch déploie les tâches sur ces nœuds et les gère.</span><span class="sxs-lookup"><span data-stu-id="cc761-156">Azure Batch service deploys the tasks on these nodes and manages them.</span></span> <span data-ttu-id="cc761-157">Vous pouvez définir les paramètres de configuration suivants pour le pool.</span><span class="sxs-lookup"><span data-stu-id="cc761-157">You can define the following configuration parameters for your pool.</span></span>

* <span data-ttu-id="cc761-158">Type d’image de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="cc761-158">Type of Virtual Machine image</span></span>
* <span data-ttu-id="cc761-159">Taille des nœuds de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="cc761-159">Size of Virtual Machine nodes</span></span>
* <span data-ttu-id="cc761-160">Nombre de nœuds de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="cc761-160">Number of Virtual Machine nodes</span></span>

> [!Tip]
> <span data-ttu-id="cc761-161">La taille et le nombre de nœuds de machine virtuelle dépendent en grande partie du nombre de tâches à exécuter en parallèle et également de la tâche proprement dite.</span><span class="sxs-lookup"><span data-stu-id="cc761-161">The size and number of Virtual Machine nodes largely depend on the number of tasks you want to run in parallel and also the task itself.</span></span> <span data-ttu-id="cc761-162">Nous vous recommandons d’effectuer des tests pour déterminer la taille et le nombre idéaux.</span><span class="sxs-lookup"><span data-stu-id="cc761-162">We recommend testing to determine the ideal number and size.</span></span>
>
>

<span data-ttu-id="cc761-163">L’extrait de code suivant crée les objets de paramètre de configuration.</span><span class="sxs-lookup"><span data-stu-id="cc761-163">The following code snippet creates the configuration parameter objects.</span></span>

```nodejs
// Creating Image reference configuration for Ubuntu Linux VM
var imgRef = {publisher:"Canonical",offer:"UbuntuServer",sku:"14.04.2-LTS",version:"latest"}

// Creating the VM configuration object with the SKUID
var vmconfig = {imageReference:imgRef,nodeAgentSKUId:"batch.node.ubuntu 14.04"}

// Setting the VM size to Standard F4
var vmSize = "STANDARD_F4"

//Setting number of VMs in the pool to 4
var numVMs = 4
```

> [!Tip]
> <span data-ttu-id="cc761-164">Pour obtenir la liste des images de machine virtuelle Linux disponibles pour Azure Batch et de leurs ID de référence (SKU), consultez la section [Liste des images de machine virtuelle](batch-linux-nodes.md#list-of-virtual-machine-images).</span><span class="sxs-lookup"><span data-stu-id="cc761-164">For the list of Linux VM images available for Azure Batch and their SKU IDs, see [List of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images).</span></span>
>
>

<span data-ttu-id="cc761-165">Une fois la configuration du pool définie, vous pouvez créer le pool Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="cc761-165">Once the pool configuration is defined, you can create the Azure Batch pool.</span></span> <span data-ttu-id="cc761-166">La commande du pool Batch crée des nœuds de machine virtuelle Azure et les prépare à recevoir les tâches à exécuter.</span><span class="sxs-lookup"><span data-stu-id="cc761-166">The Batch pool command creates Azure Virtual Machine nodes and prepares them to be ready to receive tasks to execute.</span></span> <span data-ttu-id="cc761-167">Chaque pool doit posséder un ID unique à titre de référence pour les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="cc761-167">Each pool should have a unique ID for reference in subsequent steps.</span></span>

<span data-ttu-id="cc761-168">L’extrait de code suivant crée un pool Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="cc761-168">The following code snippet creates an Azure Batch pool.</span></span>

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating the Pool for the specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

<span data-ttu-id="cc761-169">Vous pouvez vérifier l’état du pool créé et vous assurer que l’état est « actif » avant de poursuivre avec la soumission d’un travail à ce pool.</span><span class="sxs-lookup"><span data-stu-id="cc761-169">You can check the status of the pool created and ensure that the state is in "active" before going ahead with submission of a Job to that pool.</span></span>

```nodejs
var cloudPool = batch_client.pool.get(poolid,function(error,result,request,response){
        if(error == null)
        {

            if(result.state == "active")
            {
                console.log("Pool is active");
            }
        }
        else
        {
            if(error.statusCode==404)
            {
                console.log("Pool not found yet returned 404...");    

            }
            else
            {
                console.log("Error occurred while retrieving pool data");
            }
        }
        });
```

<span data-ttu-id="cc761-170">Ci-après figure un exemple d’objet de résultat retourné par la fonction pool.get.</span><span class="sxs-lookup"><span data-stu-id="cc761-170">Following is a sample result object returned by the pool.get function.</span></span>

```
{ id: 'processcsv_201721152',
  displayName: 'processcsv_201721152',
  url: 'https://<batch-account-name>.centralus.batch.azure.com/pools/processcsv_201721152',
  eTag: '<eTag>',
  lastModified: 2017-03-27T10:28:02.398Z,
  creationTime: 2017-03-27T10:28:02.398Z,
  state: 'active',
  stateTransitionTime: 2017-03-27T10:28:02.398Z,
  allocationState: 'resizing',
  allocationStateTransitionTime: 2017-03-27T10:28:02.398Z,
  vmSize: 'standard_a1',
  virtualMachineConfiguration:
   { imageReference:
      { publisher: 'Canonical',
        offer: 'UbuntuServer',
        sku: '14.04.2-LTS',
        version: 'latest' },
     nodeAgentSKUId: 'batch.node.ubuntu 14.04' },
  resizeTimeout:
   { [Number: 900000]
     _milliseconds: 900000,
     _days: 0,
     _months: 0,
     _data:
      { milliseconds: 0,
        seconds: 0,
        minutes: 15,
        hours: 0,
        days: 0,
        months: 0,
        years: 0 },
     _locale:
      Locale {
        _calendar: [Object],
        _longDateFormat: [Object],
        _invalidDate: 'Invalid date',
        ordinal: [Function: ordinal],
        _ordinalParse: /\d{1,2}(th|st|nd|rd)/,
        _relativeTime: [Object],
        _months: [Object],
        _monthsShort: [Object],
        _week: [Object],
        _weekdays: [Object],
        _weekdaysMin: [Object],
        _weekdaysShort: [Object],
        _meridiemParse: /[ap]\.?m?\.?/i,
        _abbr: 'en',
        _config: [Object],
        _ordinalParseLenient: /\d{1,2}(th|st|nd|rd)|\d{1,2}/ } },
  currentDedicated: 0,
  targetDedicated: 4,
  enableAutoScale: false,
  enableInterNodeCommunication: false,
  maxTasksPerNode: 1,
  taskSchedulingPolicy: { nodeFillType: 'Spread' } }
```


### <a name="step-4-submit-an-azure-batch-job"></a><span data-ttu-id="cc761-171">Étape 4 : soumettre un travail Azure Batch</span><span class="sxs-lookup"><span data-stu-id="cc761-171">Step 4: Submit an Azure Batch job</span></span>
<span data-ttu-id="cc761-172">Un travail Azure Batch est un groupe logique de tâches similaires.</span><span class="sxs-lookup"><span data-stu-id="cc761-172">An Azure Batch job is a logical group of similar tasks.</span></span> <span data-ttu-id="cc761-173">Dans notre scénario, il s’agit du travail « Process csv to JSON ».</span><span class="sxs-lookup"><span data-stu-id="cc761-173">In our scenario, it is "Process csv to JSON."</span></span> <span data-ttu-id="cc761-174">Ici, chaque tâche peut traiter les fichiers csv présents dans chaque conteneur Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="cc761-174">Each task here could be processing csv files present in each Azure Storage container.</span></span>

<span data-ttu-id="cc761-175">Ces tâches sont exécutées en parallèle et déployées sur plusieurs nœuds, et orchestrées par le service Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="cc761-175">These tasks would run in parallel and deployed across multiple nodes, orchestrated by the Azure Batch service.</span></span>

> [!Tip]
> <span data-ttu-id="cc761-176">Vous pouvez utiliser la propriété [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) pour spécifier le nombre maximal de tâches pouvant s’exécuter simultanément sur un seul nœud.</span><span class="sxs-lookup"><span data-stu-id="cc761-176">You can use the [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property to specify maximum number of tasks that can run concurrently on a single node.</span></span>
>
>

#### <a name="preparation-task"></a><span data-ttu-id="cc761-177">Tâche de préparation</span><span class="sxs-lookup"><span data-stu-id="cc761-177">Preparation task</span></span>

<span data-ttu-id="cc761-178">Les nœuds de machine virtuelle créés sont des nœuds Ubuntu vides.</span><span class="sxs-lookup"><span data-stu-id="cc761-178">The VM nodes created are blank Ubuntu nodes.</span></span> <span data-ttu-id="cc761-179">Il arrive souvent que vous deviez installer un ensemble de programmes comme composants requis.</span><span class="sxs-lookup"><span data-stu-id="cc761-179">Often, you need to install a set of programs as prerequisites.</span></span>
<span data-ttu-id="cc761-180">En règle générale, pour les nœuds Linux, vous pouvez disposer d’un script Shell qui installe les composants requis avant l’exécution des tâches réelles.</span><span class="sxs-lookup"><span data-stu-id="cc761-180">Typically, for Linux nodes you can have a shell script that installs the prerequisites before the actual tasks run.</span></span> <span data-ttu-id="cc761-181">Cependant, il peut s’agir de n’importe quel exécutable programmable.</span><span class="sxs-lookup"><span data-stu-id="cc761-181">However it could be any programmable executable.</span></span>
<span data-ttu-id="cc761-182">Le [script Shell](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) de cet exemple installe Python-pip et le Kit de développement logiciel (SDK) Stockage Azure pour Python.</span><span class="sxs-lookup"><span data-stu-id="cc761-182">The [shell script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in this example installs Python-pip and the Azure Storage SDK for Python.</span></span>

<span data-ttu-id="cc761-183">Vous pouvez charger le script sur un compte de stockage Azure et générer un URI SAS pour accéder au script.</span><span class="sxs-lookup"><span data-stu-id="cc761-183">You can upload the script on an Azure Storage Account and generate a SAS URI to access the script.</span></span> <span data-ttu-id="cc761-184">Ce processus peut également être automatisé à l’aide du Kit de développement logiciel (SDK) Node.js pour Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="cc761-184">This process can also be automated using the Azure Storage Node.js SDK.</span></span>

> [!Tip]
> <span data-ttu-id="cc761-185">Une tâche de préparation d’un travail s’exécute uniquement sur les nœuds de machine virtuelle où la tâche donnée doit s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="cc761-185">A preparation task for a job runs only on the VM nodes where the specific task needs to run.</span></span> <span data-ttu-id="cc761-186">Si vous voulez installer les composants requis sur tous les nœuds, quelles que soient les tâches exécutées dessus, vous pouvez utiliser la propriété [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) lorsque vous ajoutez un pool.</span><span class="sxs-lookup"><span data-stu-id="cc761-186">If you want prerequisites to be installed on all nodes irrespective of the tasks that run on it, you can use the [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property while adding a pool.</span></span> <span data-ttu-id="cc761-187">Vous pouvez utiliser la définition de tâche de préparation suivante à titre de référence.</span><span class="sxs-lookup"><span data-stu-id="cc761-187">You can use the following preparation task definition for reference.</span></span>
>
>

<span data-ttu-id="cc761-188">Une tâche de préparation est spécifiée lors de la soumission d’un travail Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="cc761-188">A preparation task is specified during the submission of Azure Batch job.</span></span> <span data-ttu-id="cc761-189">Ci-après figurent les paramètres de configuration de tâche de préparation :</span><span class="sxs-lookup"><span data-stu-id="cc761-189">Following are the preparation task configuration parameters:</span></span>

* <span data-ttu-id="cc761-190">**ID** : identificateur unique de la tâche de préparation</span><span class="sxs-lookup"><span data-stu-id="cc761-190">**ID**: A unique identifier for the preparation task</span></span>
* <span data-ttu-id="cc761-191">**commandLine** : ligne de commande pour exécuter la tâche exécutable</span><span class="sxs-lookup"><span data-stu-id="cc761-191">**commandLine**: Command line to execute the task executable</span></span>
* <span data-ttu-id="cc761-192">**resourceFiles** : tableau des objets qui fournissent des détails des fichiers qui doivent être téléchargés pour l’exécution de cette tâche.</span><span class="sxs-lookup"><span data-stu-id="cc761-192">**resourceFiles**: Array of objects that provide details of files needed to be downloaded for this task to run.</span></span>  <span data-ttu-id="cc761-193">Ses options sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="cc761-193">Following are its options</span></span>
    - <span data-ttu-id="cc761-194">blobSource : URI SAS du fichier</span><span class="sxs-lookup"><span data-stu-id="cc761-194">blobSource: The SAS URI of the file</span></span>
    - <span data-ttu-id="cc761-195">filePath : chemin d’accès local pour télécharger et enregistrer le fichier</span><span class="sxs-lookup"><span data-stu-id="cc761-195">filePath: Local path to download and save the file</span></span>
    - <span data-ttu-id="cc761-196">fileMode : applicable uniquement pour les nœuds Linux, fileMode est au format octal avec la valeur 0770 par défaut</span><span class="sxs-lookup"><span data-stu-id="cc761-196">fileMode: Only applicable for Linux nodes, fileMode is in octal format with a default value of 0770</span></span>
* <span data-ttu-id="cc761-197">**waitForSuccess** : si cette option est définie sur la valeur true, la tâche ne s’exécute pas en cas d’échec des tâches de préparation</span><span class="sxs-lookup"><span data-stu-id="cc761-197">**waitForSuccess**: If set to true, the task does not run on preparation task failures</span></span>
* <span data-ttu-id="cc761-198">**runElevated** : définissez cette option sur la valeur True si des privilèges élevés sont requis pour l’exécution de la tâche.</span><span class="sxs-lookup"><span data-stu-id="cc761-198">**runElevated**: Set it to true if elevated privileges are needed to run the task.</span></span>

<span data-ttu-id="cc761-199">L’extrait de code suivant illustre un exemple de configuration de script d’une tâche de préparation :</span><span class="sxs-lookup"><span data-stu-id="cc761-199">Following code snippet shows the preparation task script configuration sample:</span></span>

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

<span data-ttu-id="cc761-200">Si aucun composant requis ne doit être installé pour l’exécution de vos tâches, vous pouvez ignorer les tâches de préparation.</span><span class="sxs-lookup"><span data-stu-id="cc761-200">If there are no prerequisites to be installed for your tasks to run, you can skip the preparation tasks.</span></span> <span data-ttu-id="cc761-201">Le code suivant crée un travail dont le nom d’affichage est « process csv files ».</span><span class="sxs-lookup"><span data-stu-id="cc761-201">Following code creates a job with display name "process csv files."</span></span>

 ```nodejs
 // Setting up Batch pool configuration
 var pool_config = {poolId:poolid}
 // Setting up Job configuration along with preparation task
 var jobId = "processcsvjob"
 var job_config = {id:jobId,displayName:"process csv files",jobPreparationTask:job_prep_task_config,poolInfo:pool_config}
 // Adding Azure batch job to the pool
 var job = batch_client.job.add(job_config,function(error,result){
     if(error != null)
     {
         console.log("Error submitting job : " + error.response);
     }});
```


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a><span data-ttu-id="cc761-202">Étape 5 : soumettre des tâches Azure Batch pour un travail</span><span class="sxs-lookup"><span data-stu-id="cc761-202">Step 5: Submit Azure Batch tasks for a job</span></span>

<span data-ttu-id="cc761-203">Maintenant que le travail de traitement des fichiers csv est créé, nous allons créer des tâches pour celui-ci.</span><span class="sxs-lookup"><span data-stu-id="cc761-203">Now that our process csv job is created, let us create tasks for that job.</span></span> <span data-ttu-id="cc761-204">En supposant que nous possédons quatre conteneurs, nous devons créer quatre tâches, une par conteneur.</span><span class="sxs-lookup"><span data-stu-id="cc761-204">Assuming we have four containers, we have to create four tasks, one for each container.</span></span>

<span data-ttu-id="cc761-205">Le [script Python](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py) accepte deux paramètres :</span><span class="sxs-lookup"><span data-stu-id="cc761-205">If we look at the [Python script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), it accepts two parameters:</span></span>

* <span data-ttu-id="cc761-206">nom du conteneur : conteneur de stockage à partir duquel télécharger des fichiers</span><span class="sxs-lookup"><span data-stu-id="cc761-206">container name: The Storage container to download files from</span></span>
* <span data-ttu-id="cc761-207">modèle : paramètre facultatif d’un modèle de nom de fichier</span><span class="sxs-lookup"><span data-stu-id="cc761-207">pattern: An optional parameter of file name pattern</span></span>

<span data-ttu-id="cc761-208">En supposant que nous disposons de quatre conteneurs « con1 », « con2 », « con3 » et « con4 », le code suivant illustre la soumission des tâches pour le travail Azure Batch « process csv » que nous avons créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="cc761-208">Assuming we have four containers "con1", "con2", "con3","con4" following code shows submitting for tasks to the Azure batch job "process csv" we created earlier.</span></span>

```nodejs
// storing container names in an array
var container_list = ["con1","con2","con3","con4"]
    container_list.forEach(function(val,index){           

           var container_name = val;
           var taskID = container_name + "_process";
           var task_config = {id:taskID,displayName:'process csv in ' + container_name,commandLine:'python processcsv.py --container ' + container_name,resourceFiles:[{'blobSource':'<blob SAS URI>','filePath':'processcsv.py'}]}
           var task = batch_client.task.add(poolid,task_config,function(error,result){
                if(error != null)
                {
                    console.log(error.response);     
                }
                else
                {
                    console.log("Task for container : " + container_name + "submitted successfully");
                }



           });

    });
```

<span data-ttu-id="cc761-209">Le code permet d’ajouter plusieurs tâches au pool.</span><span class="sxs-lookup"><span data-stu-id="cc761-209">The code adds multiple tasks to the pool.</span></span> <span data-ttu-id="cc761-210">Chaque tâche est exécutée sur un nœud dans le pool de machines virtuelles créé.</span><span class="sxs-lookup"><span data-stu-id="cc761-210">And each of the tasks is executed on a node in the pool of VMs created.</span></span> <span data-ttu-id="cc761-211">Si le nombre de tâches dépasse le nombre de machines virtuelles définies dans un pool ou la propriété maxTasksPerNode, les tâches attendent qu’un nœud soit de nouveau disponible.</span><span class="sxs-lookup"><span data-stu-id="cc761-211">If the number of tasks exceeds the number of VMs in a pool or the maxTasksPerNode property, the tasks wait until a node is made available.</span></span> <span data-ttu-id="cc761-212">Cette orchestration est gérée automatiquement par Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="cc761-212">This orchestration is handled by Azure Batch automatically.</span></span>

<span data-ttu-id="cc761-213">Le portail contient des vues détaillées sur les états des tâches et du travail.</span><span class="sxs-lookup"><span data-stu-id="cc761-213">The portal has detailed views on the tasks and job statuses.</span></span> <span data-ttu-id="cc761-214">Vous pouvez également utiliser la liste et récupérer des fonctions dans le Kit de développement logiciel (SDK) Node Azure.</span><span class="sxs-lookup"><span data-stu-id="cc761-214">You can also use the list and get functions in the Azure Node SDK.</span></span> <span data-ttu-id="cc761-215">Des détails sont indiqués dans le [lien](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html) de la documentation.</span><span class="sxs-lookup"><span data-stu-id="cc761-215">Details are provided in the documentation [link](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc761-216">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cc761-216">Next steps</span></span>

- <span data-ttu-id="cc761-217">Consultez l’article [Présentation des fonctionnalités de présentation d’Azure Batch](batch-api-basics.md) , que nous vous recommandons si vous ne connaissez pas le service.</span><span class="sxs-lookup"><span data-stu-id="cc761-217">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span></span>
- <span data-ttu-id="cc761-218">Consultez la [référence Node.js Batch](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) pour explorer l’API Batch.</span><span class="sxs-lookup"><span data-stu-id="cc761-218">See the [Batch Node.js reference](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) to explore the Batch API.</span></span>

