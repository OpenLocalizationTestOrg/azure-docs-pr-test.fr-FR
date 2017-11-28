---
title: "aaaTutorial - utiliser la bibliothèque cliente Azure Batch hello pour Node.js | Documents Microsoft"
description: "Découvrez les concepts de base hello de traitement par lots Azure et créer une solution simple à l’aide de Node.js."
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
ms.openlocfilehash: d2b0ecbe764e7100affd7b02839aef3077b073cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-batch-sdk-for-nodejs"></a><span data-ttu-id="54653-103">Bien démarrer avec le Kit de développement logiciel (SDK) Batch pour Node.js</span><span class="sxs-lookup"><span data-stu-id="54653-103">Get started with Batch SDK for Node.js</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="54653-104">.NET</span><span class="sxs-lookup"><span data-stu-id="54653-104">.NET</span></span>](batch-dotnet-get-started.md)
> * [<span data-ttu-id="54653-105">Python</span><span class="sxs-lookup"><span data-stu-id="54653-105">Python</span></span>](batch-python-tutorial.md)
> * [<span data-ttu-id="54653-106">Node.JS</span><span class="sxs-lookup"><span data-stu-id="54653-106">Node.js</span></span>](batch-nodejs-get-started.md)
>
>

<span data-ttu-id="54653-107">Principes fondamentaux de la création d’un client de lot à l’aide de Node.js hello [Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span><span class="sxs-lookup"><span data-stu-id="54653-107">Learn hello basics of building a Batch client in Node.js using [Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/).</span></span> <span data-ttu-id="54653-108">Nous allons présenter pas à pas un scénario pour une application Batch, puis la configurer à l’aide d’un client Node.js.</span><span class="sxs-lookup"><span data-stu-id="54653-108">We take a step by step approach of understanding a scenario for a batch application and then setting it up using a Node.js client.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="54653-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="54653-109">Prerequisites</span></span>
<span data-ttu-id="54653-110">Cet article suppose que vous avez acquis une connaissance pratique de Node.js et que vous êtes familiarisé avec Linux.</span><span class="sxs-lookup"><span data-stu-id="54653-110">This article assumes that you have a working knowledge of Node.js and familiarity with Linux.</span></span> <span data-ttu-id="54653-111">Il suppose également que vous disposez d’une configuration de compte Azure avec les services de stockage et de traitement par lots la toocreate des droits accès.</span><span class="sxs-lookup"><span data-stu-id="54653-111">It also assumes that you have an Azure account setup with access rights toocreate Batch and Storage services.</span></span>

<span data-ttu-id="54653-112">Nous vous recommandons de lecture [vue d’ensemble technique de Azure Batch](batch-technical-overview.md) avant de suivre les étapes de hello décrites cet article.</span><span class="sxs-lookup"><span data-stu-id="54653-112">We recommend reading [Azure Batch Technical Overview](batch-technical-overview.md) before you go through hello steps outlined this article.</span></span>

## <a name="hello-tutorial-scenario"></a><span data-ttu-id="54653-113">scénario du didacticiel Hello</span><span class="sxs-lookup"><span data-stu-id="54653-113">hello tutorial scenario</span></span>
<span data-ttu-id="54653-114">Découvrons scénario de flux de travail de traitement par lots hello.</span><span class="sxs-lookup"><span data-stu-id="54653-114">Let us understand hello batch workflow scenario.</span></span> <span data-ttu-id="54653-115">Nous avons un simple script écrit dans Python qui télécharge tous les volumes partagés de cluster, les fichiers à partir d’un conteneur de stockage d’objets Blob Azure et les convertit en tooJSON.</span><span class="sxs-lookup"><span data-stu-id="54653-115">We have a simple script written in Python that downloads all csv files from an Azure Blob storage container and converts them tooJSON.</span></span> <span data-ttu-id="54653-116">tooprocess compte de stockage de plusieurs conteneurs en parallèle, nous pouvons déployer le script hello comme un traitement par lots Azure.</span><span class="sxs-lookup"><span data-stu-id="54653-116">tooprocess multiple storage account containers in parallel, we can deploy hello script as an Azure Batch job.</span></span>

## <a name="azure-batch-architecture"></a><span data-ttu-id="54653-117">Architecture Azure Batch</span><span class="sxs-lookup"><span data-stu-id="54653-117">Azure Batch Architecture</span></span>
<span data-ttu-id="54653-118">Hello diagramme suivant illustre comment nous pouvons l’échelle hello Python script à l’aide du traitement par lots Azure et un client Node.js.</span><span class="sxs-lookup"><span data-stu-id="54653-118">hello following diagram depicts how we can scale hello Python script using Azure Batch and a Node.js client.</span></span>

![Scénario Azure Batch](./media/batch-nodejs-get-started/BatchScenario.png)

<span data-ttu-id="54653-120">client de node.js Hello déploie un traitement par lots avec une tâche de préparation (expliquée en détail plus loin) et un ensemble de tâches en fonction du nombre de hello de conteneurs dans le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="54653-120">hello node.js client deploys a batch job with a preparation task (explained in detail later) and a set of tasks depending on hello number of containers in hello storage account.</span></span> <span data-ttu-id="54653-121">Vous pouvez télécharger les scripts de hello référentiel github de hello.</span><span class="sxs-lookup"><span data-stu-id="54653-121">You can download hello scripts from hello github repository.</span></span>

* [<span data-ttu-id="54653-122">Client Node.js</span><span class="sxs-lookup"><span data-stu-id="54653-122">Node.js client</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [<span data-ttu-id="54653-123">Scripts Shell de la tâche de préparation</span><span class="sxs-lookup"><span data-stu-id="54653-123">Preparation task shell scripts</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [<span data-ttu-id="54653-124">Processeur de Python csv tooJSON</span><span class="sxs-lookup"><span data-stu-id="54653-124">Python csv tooJSON processor</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> <span data-ttu-id="54653-125">client de Node.js Hello dans lien hello spécifié ne contient-elle pas de toobe code spécifique déployé comme une application Azure (fonction).</span><span class="sxs-lookup"><span data-stu-id="54653-125">hello Node.js client in hello link specified does not contain specific code toobe deployed as an Azure function app.</span></span> <span data-ttu-id="54653-126">Vous pouvez faire référence toohello suivant les liens pour toocreate d’instructions une.</span><span class="sxs-lookup"><span data-stu-id="54653-126">You can refer toohello following links for instructions toocreate one.</span></span>
> - [<span data-ttu-id="54653-127">Créer une application de fonction</span><span class="sxs-lookup"><span data-stu-id="54653-127">Create function app</span></span>](../azure-functions/functions-create-first-azure-function.md)
> - [<span data-ttu-id="54653-128">Créer une fonction de déclencheur de minuteur</span><span class="sxs-lookup"><span data-stu-id="54653-128">Create timer trigger function</span></span>](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-hello-application"></a><span data-ttu-id="54653-129">Générez l’application hello</span><span class="sxs-lookup"><span data-stu-id="54653-129">Build hello application</span></span>

<span data-ttu-id="54653-130">Maintenant, nous suivez le processus de hello étape par étape dans la génération de hello Node.js client :</span><span class="sxs-lookup"><span data-stu-id="54653-130">Now, let us follow hello process step by step into building hello Node.js client:</span></span>

### <a name="step-1-install-azure-batch-sdk"></a><span data-ttu-id="54653-131">Étape 1 : installer le Kit de développement logiciel (SDK) Azure Batch</span><span class="sxs-lookup"><span data-stu-id="54653-131">Step 1: Install Azure Batch SDK</span></span>

<span data-ttu-id="54653-132">Vous pouvez installer le Kit de développement logiciel Azure Batch pour Node.js à l’aide de la commande d’installation npm hello.</span><span class="sxs-lookup"><span data-stu-id="54653-132">You can install Azure Batch SDK for Node.js using hello npm install command.</span></span>

`npm install azure-batch`

<span data-ttu-id="54653-133">Cette commande installe la version la plus récente hello du nœud de traitement par lots d’azure SDK.</span><span class="sxs-lookup"><span data-stu-id="54653-133">This command installs hello latest version of azure-batch node SDK.</span></span>

>[!Tip]
> <span data-ttu-id="54653-134">Dans une application de la fonction d’Azure, vous pouvez passer des paramètres de « Kudu Console « Bonjour Azure fonction onglet toorun hello npm trop des commandes d’installation.</span><span class="sxs-lookup"><span data-stu-id="54653-134">In an Azure Function app, you can go too"Kudu Console" in hello Azure function's Settings tab toorun hello npm install commands.</span></span> <span data-ttu-id="54653-135">Dans cette tooinstall cas SDK de traitement par lots Azure pour Node.js.</span><span class="sxs-lookup"><span data-stu-id="54653-135">In this case tooinstall Azure Batch SDK for Node.js.</span></span>
>
>

### <a name="step-2-create-an-azure-batch-account"></a><span data-ttu-id="54653-136">Étape 2 : Créer un compte Azure Batch</span><span class="sxs-lookup"><span data-stu-id="54653-136">Step 2: Create an Azure Batch account</span></span>

<span data-ttu-id="54653-137">Vous pouvez le créer à partir de hello [portail Azure](batch-account-create-portal.md) ou à partir de la ligne de commande ([Powershell](batch-powershell-cmdlets-get-started.md) /[cli Azure](https://docs.microsoft.com/cli/azure/overview)).</span><span class="sxs-lookup"><span data-stu-id="54653-137">You can create it from hello [Azure portal](batch-account-create-portal.md) or from command line ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](https://docs.microsoft.com/cli/azure/overview)).</span></span>

<span data-ttu-id="54653-138">Voici les toocreate de commandes hello une via l’interface CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="54653-138">Following are hello commands toocreate one through Azure CLI.</span></span>

<span data-ttu-id="54653-139">Créer un groupe de ressources, ignorez cette étape si vous avez déjà une où vous souhaitez toocreate hello compte Batch :</span><span class="sxs-lookup"><span data-stu-id="54653-139">Create a Resource Group, skip this step if you already have one where you want toocreate hello Batch Account:</span></span>

`az group create -n "<resource-group-name>" -l "<location>"`

<span data-ttu-id="54653-140">Créez ensuite un compte Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="54653-140">Next, create an Azure Batch account.</span></span>

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="54653-141">Chaque compte Batch possède ses clés d’accès correspondantes.</span><span class="sxs-lookup"><span data-stu-id="54653-141">Each Batch account has its corresponding access keys.</span></span> <span data-ttu-id="54653-142">Ces clés sont nécessaires toocreate des ressources supplémentaires dans le compte de traitement par lots Azure.</span><span class="sxs-lookup"><span data-stu-id="54653-142">These keys are needed toocreate further resources in Azure batch account.</span></span> <span data-ttu-id="54653-143">Une bonne pratique pour l’environnement de production est toouse Azure Key Vault toostore ces clés.</span><span class="sxs-lookup"><span data-stu-id="54653-143">A good practice for production environment is toouse Azure Key Vault toostore these keys.</span></span> <span data-ttu-id="54653-144">Vous pouvez ensuite créer un Service principal pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="54653-144">You can then create a Service principal for hello application.</span></span> <span data-ttu-id="54653-145">Cette application hello principal de service permet de créer un jeton tooaccess les clés OAuth hello coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="54653-145">Using this service principal hello application can create an OAuth token tooaccess keys from hello key vault.</span></span>

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="54653-146">Copiez et stockez hello clé toobe est utilisé dans les étapes suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="54653-146">Copy and store hello key toobe used in hello subsequent steps.</span></span>

### <a name="step-3-create-an-azure-batch-service-client"></a><span data-ttu-id="54653-147">Étape 3 : créer un client du service Azure Batch</span><span class="sxs-lookup"><span data-stu-id="54653-147">Step 3: Create an Azure Batch service client</span></span>
<span data-ttu-id="54653-148">Extrait de code suivant tout d’abord importe module Node.js de traitement par lots d’azure hello et crée ensuite un client de Service de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="54653-148">Following code snippet first imports hello azure-batch Node.js module and then creates a Batch Service client.</span></span> <span data-ttu-id="54653-149">Vous devez toofirst créer un objet SharedKeyCredentials avec la clé du compte Batch hello copié à partir de l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="54653-149">You need toofirst create a SharedKeyCredentials object with hello Batch account key copied from hello previous step.</span></span>

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

<span data-ttu-id="54653-150">Hello URI du lot Azure sont accessibles dans l’onglet vue d’ensemble de hello Hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="54653-150">hello Azure Batch URI can be found in hello Overview tab of hello Azure portal.</span></span> <span data-ttu-id="54653-151">Il est de format de hello :</span><span class="sxs-lookup"><span data-stu-id="54653-151">It is of hello format:</span></span>

`https://accountname.location.batch.azure.com`

<span data-ttu-id="54653-152">Consultez la capture d’écran de toohello :</span><span class="sxs-lookup"><span data-stu-id="54653-152">Refer toohello screenshot:</span></span>

![URI Azure Batch](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a><span data-ttu-id="54653-154">Étape 4 : créer un pool Azure Batch</span><span class="sxs-lookup"><span data-stu-id="54653-154">Step 4: Create an Azure Batch pool</span></span>
<span data-ttu-id="54653-155">Un pool Azure Batch se compose de plusieurs machines virtuelles (également appelées nœuds Batch).</span><span class="sxs-lookup"><span data-stu-id="54653-155">An Azure Batch pool consists of multiple VMs (also known as Batch Nodes).</span></span> <span data-ttu-id="54653-156">Service de traitement par lots Azure déploie des tâches hello sur ces nœuds et les gère.</span><span class="sxs-lookup"><span data-stu-id="54653-156">Azure Batch service deploys hello tasks on these nodes and manages them.</span></span> <span data-ttu-id="54653-157">Vous pouvez définir hello suivant les paramètres de configuration pour le pool.</span><span class="sxs-lookup"><span data-stu-id="54653-157">You can define hello following configuration parameters for your pool.</span></span>

* <span data-ttu-id="54653-158">Type d’image de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="54653-158">Type of Virtual Machine image</span></span>
* <span data-ttu-id="54653-159">Taille des nœuds de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="54653-159">Size of Virtual Machine nodes</span></span>
* <span data-ttu-id="54653-160">Nombre de nœuds de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="54653-160">Number of Virtual Machine nodes</span></span>

> [!Tip]
> <span data-ttu-id="54653-161">taille de Hello et le nombre de nœuds de l’ordinateur virtuel dépendent en grande partie nombre hello de tâches que vous souhaitez toorun en parallèle et également hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="54653-161">hello size and number of Virtual Machine nodes largely depend on hello number of tasks you want toorun in parallel and also hello task itself.</span></span> <span data-ttu-id="54653-162">Nous vous recommandons de tester le nombre idéal de toodetermine hello et la taille.</span><span class="sxs-lookup"><span data-stu-id="54653-162">We recommend testing toodetermine hello ideal number and size.</span></span>
>
>

<span data-ttu-id="54653-163">Hello extrait de code suivant crée hello les objets de paramètre de configuration.</span><span class="sxs-lookup"><span data-stu-id="54653-163">hello following code snippet creates hello configuration parameter objects.</span></span>

```nodejs
// Creating Image reference configuration for Ubuntu Linux VM
var imgRef = {publisher:"Canonical",offer:"UbuntuServer",sku:"14.04.2-LTS",version:"latest"}

// Creating hello VM configuration object with hello SKUID
var vmconfig = {imageReference:imgRef,nodeAgentSKUId:"batch.node.ubuntu 14.04"}

// Setting hello VM size tooStandard F4
var vmSize = "STANDARD_F4"

//Setting number of VMs in hello pool too4
var numVMs = 4
```

> [!Tip]
> <span data-ttu-id="54653-164">Pour hello la liste d’images Linux VM disponibles pour le traitement par lots Azure et leurs ID de référence (SKU), consultez [la liste des images de machine virtuelle](batch-linux-nodes.md#list-of-virtual-machine-images).</span><span class="sxs-lookup"><span data-stu-id="54653-164">For hello list of Linux VM images available for Azure Batch and their SKU IDs, see [List of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images).</span></span>
>
>

<span data-ttu-id="54653-165">Une fois la configuration du pool hello est définie, vous pouvez créer le pool de traitement par lots Azure hello.</span><span class="sxs-lookup"><span data-stu-id="54653-165">Once hello pool configuration is defined, you can create hello Azure Batch pool.</span></span> <span data-ttu-id="54653-166">Hello commande de pool de traitement par lots crée des nœuds de Machine virtuelle Azure et les prépare tooexecute de tâches toobe tooreceive prêt.</span><span class="sxs-lookup"><span data-stu-id="54653-166">hello Batch pool command creates Azure Virtual Machine nodes and prepares them toobe ready tooreceive tasks tooexecute.</span></span> <span data-ttu-id="54653-167">Chaque pool doit posséder un ID unique à titre de référence pour les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="54653-167">Each pool should have a unique ID for reference in subsequent steps.</span></span>

<span data-ttu-id="54653-168">Hello suivant extrait de code crée un pool de traitement par lots Azure.</span><span class="sxs-lookup"><span data-stu-id="54653-168">hello following code snippet creates an Azure Batch pool.</span></span>

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating hello Pool for hello specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

<span data-ttu-id="54653-169">Vous pouvez vérifier l’état de hello du regroupement hello créé et vous assurer que hello état est « actif » avant de poursuivre avec l’envoi d’un pool de toothat de travail.</span><span class="sxs-lookup"><span data-stu-id="54653-169">You can check hello status of hello pool created and ensure that hello state is in "active" before going ahead with submission of a Job toothat pool.</span></span>

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

<span data-ttu-id="54653-170">Voici un exemple d’objet résultat retourné par la fonction de pool.get hello.</span><span class="sxs-lookup"><span data-stu-id="54653-170">Following is a sample result object returned by hello pool.get function.</span></span>

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


### <a name="step-4-submit-an-azure-batch-job"></a><span data-ttu-id="54653-171">Étape 4 : soumettre un travail Azure Batch</span><span class="sxs-lookup"><span data-stu-id="54653-171">Step 4: Submit an Azure Batch job</span></span>
<span data-ttu-id="54653-172">Un travail Azure Batch est un groupe logique de tâches similaires.</span><span class="sxs-lookup"><span data-stu-id="54653-172">An Azure Batch job is a logical group of similar tasks.</span></span> <span data-ttu-id="54653-173">Dans notre scénario, il est « TooJSON csv de processus. »</span><span class="sxs-lookup"><span data-stu-id="54653-173">In our scenario, it is "Process csv tooJSON."</span></span> <span data-ttu-id="54653-174">Ici, chaque tâche peut traiter les fichiers csv présents dans chaque conteneur Stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="54653-174">Each task here could be processing csv files present in each Azure Storage container.</span></span>

<span data-ttu-id="54653-175">Ces tâches sont exécute en parallèle et déploiement sur plusieurs nœuds, orchestrées par le service de traitement par lots Azure hello.</span><span class="sxs-lookup"><span data-stu-id="54653-175">These tasks would run in parallel and deployed across multiple nodes, orchestrated by hello Azure Batch service.</span></span>

> [!Tip]
> <span data-ttu-id="54653-176">Vous pouvez utiliser hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) propriété toospecify maximum de tâches pouvant s’exécuter simultanément sur un nœud unique.</span><span class="sxs-lookup"><span data-stu-id="54653-176">You can use hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property toospecify maximum number of tasks that can run concurrently on a single node.</span></span>
>
>

#### <a name="preparation-task"></a><span data-ttu-id="54653-177">Tâche de préparation</span><span class="sxs-lookup"><span data-stu-id="54653-177">Preparation task</span></span>

<span data-ttu-id="54653-178">les nœuds de machine virtuelle Hello créés sont les nœuds de Ubuntu vides.</span><span class="sxs-lookup"><span data-stu-id="54653-178">hello VM nodes created are blank Ubuntu nodes.</span></span> <span data-ttu-id="54653-179">Vous devez souvent tooinstall un ensemble de programmes comme composants requis.</span><span class="sxs-lookup"><span data-stu-id="54653-179">Often, you need tooinstall a set of programs as prerequisites.</span></span>
<span data-ttu-id="54653-180">En règle générale, pour les nœuds de Linux, vous pouvez avoir un script shell qui installe les composants requis de hello avant l’exécution de tâches réelles hello.</span><span class="sxs-lookup"><span data-stu-id="54653-180">Typically, for Linux nodes you can have a shell script that installs hello prerequisites before hello actual tasks run.</span></span> <span data-ttu-id="54653-181">Cependant, il peut s’agir de n’importe quel exécutable programmable.</span><span class="sxs-lookup"><span data-stu-id="54653-181">However it could be any programmable executable.</span></span>
<span data-ttu-id="54653-182">Hello [script du shell](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) dans cet exemple installe le pip de Python et hello stockage Azure SDK pour Python.</span><span class="sxs-lookup"><span data-stu-id="54653-182">hello [shell script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in this example installs Python-pip and hello Azure Storage SDK for Python.</span></span>

<span data-ttu-id="54653-183">Vous pouvez télécharger le script hello sur un compte Azure Storage et générer un script de hello tooaccess URI SAS.</span><span class="sxs-lookup"><span data-stu-id="54653-183">You can upload hello script on an Azure Storage Account and generate a SAS URI tooaccess hello script.</span></span> <span data-ttu-id="54653-184">Ce processus peut également être automatisé à l’aide de hello Node.js de stockage Windows Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="54653-184">This process can also be automated using hello Azure Storage Node.js SDK.</span></span>

> [!Tip]
> <span data-ttu-id="54653-185">Une tâche de préparation d’une tâche s’exécute uniquement sur les nœuds de machine virtuelle hello où les tâches spécifiques hello doit toorun.</span><span class="sxs-lookup"><span data-stu-id="54653-185">A preparation task for a job runs only on hello VM nodes where hello specific task needs toorun.</span></span> <span data-ttu-id="54653-186">Si vous souhaitez toobe des composants requis installé sur tous les nœuds, quelles que soient les tâches hello qui s’y exécutent, vous pouvez utiliser hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) propriété lors de l’ajout d’un pool.</span><span class="sxs-lookup"><span data-stu-id="54653-186">If you want prerequisites toobe installed on all nodes irrespective of hello tasks that run on it, you can use hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property while adding a pool.</span></span> <span data-ttu-id="54653-187">Vous pouvez utiliser hello après la définition de tâche de préparation pour référence.</span><span class="sxs-lookup"><span data-stu-id="54653-187">You can use hello following preparation task definition for reference.</span></span>
>
>

<span data-ttu-id="54653-188">Une tâche de préparation est spécifiée lors de l’envoi de hello de traitement par lots Azure.</span><span class="sxs-lookup"><span data-stu-id="54653-188">A preparation task is specified during hello submission of Azure Batch job.</span></span> <span data-ttu-id="54653-189">Suivantes sont hello des paramètres de configuration de tâche de préparation :</span><span class="sxs-lookup"><span data-stu-id="54653-189">Following are hello preparation task configuration parameters:</span></span>

* <span data-ttu-id="54653-190">**ID**: un identificateur unique pour la tâche de préparation hello</span><span class="sxs-lookup"><span data-stu-id="54653-190">**ID**: A unique identifier for hello preparation task</span></span>
* <span data-ttu-id="54653-191">**ligne de commande**: ligne de commande tooexecute hello exécutable de la tâche</span><span class="sxs-lookup"><span data-stu-id="54653-191">**commandLine**: Command line tooexecute hello task executable</span></span>
* <span data-ttu-id="54653-192">**resourceFiles**: tableau d’objets qui fournissent des détails des fichiers nécessaires toobe téléchargé pour toorun de cette tâche.</span><span class="sxs-lookup"><span data-stu-id="54653-192">**resourceFiles**: Array of objects that provide details of files needed toobe downloaded for this task toorun.</span></span>  <span data-ttu-id="54653-193">Ses options sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="54653-193">Following are its options</span></span>
    - <span data-ttu-id="54653-194">blobSource : hello URI SAS du fichier de hello</span><span class="sxs-lookup"><span data-stu-id="54653-194">blobSource: hello SAS URI of hello file</span></span>
    - <span data-ttu-id="54653-195">filePath : toodownload de chemin d’accès Local et enregistrez le fichier de hello</span><span class="sxs-lookup"><span data-stu-id="54653-195">filePath: Local path toodownload and save hello file</span></span>
    - <span data-ttu-id="54653-196">fileMode : applicable uniquement pour les nœuds Linux, fileMode est au format octal avec la valeur 0770 par défaut</span><span class="sxs-lookup"><span data-stu-id="54653-196">fileMode: Only applicable for Linux nodes, fileMode is in octal format with a default value of 0770</span></span>
* <span data-ttu-id="54653-197">**waitForSuccess**: si l’ensemble tootrue, tâche hello ne fonctionne pas sur les échecs des tâches de préparation</span><span class="sxs-lookup"><span data-stu-id="54653-197">**waitForSuccess**: If set tootrue, hello task does not run on preparation task failures</span></span>
* <span data-ttu-id="54653-198">**runElevated**: définir tootrue si des privilèges élevés sont des tâches de hello toorun nécessaires.</span><span class="sxs-lookup"><span data-stu-id="54653-198">**runElevated**: Set it tootrue if elevated privileges are needed toorun hello task.</span></span>

<span data-ttu-id="54653-199">Extrait de code suivant montre un exemple de configuration hello préparation tâche script :</span><span class="sxs-lookup"><span data-stu-id="54653-199">Following code snippet shows hello preparation task script configuration sample:</span></span>

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

<span data-ttu-id="54653-200">S’il n’y a aucune toobe composants requis installé pour votre toorun de tâches, vous pouvez ignorer les tâches de préparation hello.</span><span class="sxs-lookup"><span data-stu-id="54653-200">If there are no prerequisites toobe installed for your tasks toorun, you can skip hello preparation tasks.</span></span> <span data-ttu-id="54653-201">Le code suivant crée un travail dont le nom d’affichage est « process csv files ».</span><span class="sxs-lookup"><span data-stu-id="54653-201">Following code creates a job with display name "process csv files."</span></span>

 ```nodejs
 // Setting up Batch pool configuration
 var pool_config = {poolId:poolid}
 // Setting up Job configuration along with preparation task
 var jobId = "processcsvjob"
 var job_config = {id:jobId,displayName:"process csv files",jobPreparationTask:job_prep_task_config,poolInfo:pool_config}
 // Adding Azure batch job toohello pool
 var job = batch_client.job.add(job_config,function(error,result){
     if(error != null)
     {
         console.log("Error submitting job : " + error.response);
     }});
```


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a><span data-ttu-id="54653-202">Étape 5 : soumettre des tâches Azure Batch pour un travail</span><span class="sxs-lookup"><span data-stu-id="54653-202">Step 5: Submit Azure Batch tasks for a job</span></span>

<span data-ttu-id="54653-203">Maintenant que le travail de traitement des fichiers csv est créé, nous allons créer des tâches pour celui-ci.</span><span class="sxs-lookup"><span data-stu-id="54653-203">Now that our process csv job is created, let us create tasks for that job.</span></span> <span data-ttu-id="54653-204">En supposant que nous avons quatre conteneurs, nous avons toocreate quatre tâches, une pour chaque conteneur.</span><span class="sxs-lookup"><span data-stu-id="54653-204">Assuming we have four containers, we have toocreate four tasks, one for each container.</span></span>

<span data-ttu-id="54653-205">Si nous examinons hello [script Python](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), elle accepte deux paramètres :</span><span class="sxs-lookup"><span data-stu-id="54653-205">If we look at hello [Python script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), it accepts two parameters:</span></span>

* <span data-ttu-id="54653-206">nom du conteneur : hello des fichiers de toodownload conteneur de stockage à partir de</span><span class="sxs-lookup"><span data-stu-id="54653-206">container name: hello Storage container toodownload files from</span></span>
* <span data-ttu-id="54653-207">modèle : paramètre facultatif d’un modèle de nom de fichier</span><span class="sxs-lookup"><span data-stu-id="54653-207">pattern: An optional parameter of file name pattern</span></span>

<span data-ttu-id="54653-208">En supposant que nous avons quatre conteneurs « con1 », « con2 », « con3 », « con4 » de code suivant illustre soumettre pour tâches toohello Azure batch travail « processus csv » créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="54653-208">Assuming we have four containers "con1", "con2", "con3","con4" following code shows submitting for tasks toohello Azure batch job "process csv" we created earlier.</span></span>

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

<span data-ttu-id="54653-209">code de Hello ajoute un pool de toohello plusieurs tâches.</span><span class="sxs-lookup"><span data-stu-id="54653-209">hello code adds multiple tasks toohello pool.</span></span> <span data-ttu-id="54653-210">Et chacune des tâches de hello est exécuté sur un nœud dans le pool hello de machines virtuelles créées.</span><span class="sxs-lookup"><span data-stu-id="54653-210">And each of hello tasks is executed on a node in hello pool of VMs created.</span></span> <span data-ttu-id="54653-211">Si nombre hello de tâches dépasse le nombre hello d’ordinateurs virtuels dans une propriété maxTasksPerNode pool ou hello, les tâches hello patienter jusqu'à ce qu’un nœud est rendu disponible.</span><span class="sxs-lookup"><span data-stu-id="54653-211">If hello number of tasks exceeds hello number of VMs in a pool or hello maxTasksPerNode property, hello tasks wait until a node is made available.</span></span> <span data-ttu-id="54653-212">Cette orchestration est gérée automatiquement par Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="54653-212">This orchestration is handled by Azure Batch automatically.</span></span>

<span data-ttu-id="54653-213">portail de Hello détaille les vues sur les États des travaux et les tâches de hello.</span><span class="sxs-lookup"><span data-stu-id="54653-213">hello portal has detailed views on hello tasks and job statuses.</span></span> <span data-ttu-id="54653-214">Vous pouvez également utiliser la liste de hello et obtenir des fonctions Bonjour Azure SDK de nœud.</span><span class="sxs-lookup"><span data-stu-id="54653-214">You can also use hello list and get functions in hello Azure Node SDK.</span></span> <span data-ttu-id="54653-215">Détails sont fournis dans la documentation de hello [lien](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span><span class="sxs-lookup"><span data-stu-id="54653-215">Details are provided in hello documentation [link](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="54653-216">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="54653-216">Next steps</span></span>

- <span data-ttu-id="54653-217">Hello de révision [les fonctionnalités de présentation d’Azure Batch](batch-api-basics.md) article, nous vous recommandons de si vous êtes de nouveau service toohello.</span><span class="sxs-lookup"><span data-stu-id="54653-217">Review hello [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new toohello service.</span></span>
- <span data-ttu-id="54653-218">Consultez hello [lot Node.js référence](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore hello API de lot.</span><span class="sxs-lookup"><span data-stu-id="54653-218">See hello [Batch Node.js reference](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore hello Batch API.</span></span>

