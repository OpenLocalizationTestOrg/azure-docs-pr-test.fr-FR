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
# <a name="get-started-with-batch-sdk-for-nodejs"></a>Bien démarrer avec le Kit de développement logiciel (SDK) Batch pour Node.js

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.JS](batch-nodejs-get-started.md)
>
>

Principes fondamentaux de la création d’un client de lot à l’aide de Node.js hello [Azure Batch Node.js SDK](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/). Nous allons présenter pas à pas un scénario pour une application Batch, puis la configurer à l’aide d’un client Node.js.  

## <a name="prerequisites"></a>Composants requis
Cet article suppose que vous avez acquis une connaissance pratique de Node.js et que vous êtes familiarisé avec Linux. Il suppose également que vous disposez d’une configuration de compte Azure avec les services de stockage et de traitement par lots la toocreate des droits accès.

Nous vous recommandons de lecture [vue d’ensemble technique de Azure Batch](batch-technical-overview.md) avant de suivre les étapes de hello décrites cet article.

## <a name="hello-tutorial-scenario"></a>scénario du didacticiel Hello
Découvrons scénario de flux de travail de traitement par lots hello. Nous avons un simple script écrit dans Python qui télécharge tous les volumes partagés de cluster, les fichiers à partir d’un conteneur de stockage d’objets Blob Azure et les convertit en tooJSON. tooprocess compte de stockage de plusieurs conteneurs en parallèle, nous pouvons déployer le script hello comme un traitement par lots Azure.

## <a name="azure-batch-architecture"></a>Architecture Azure Batch
Hello diagramme suivant illustre comment nous pouvons l’échelle hello Python script à l’aide du traitement par lots Azure et un client Node.js.

![Scénario Azure Batch](./media/batch-nodejs-get-started/BatchScenario.png)

client de node.js Hello déploie un traitement par lots avec une tâche de préparation (expliquée en détail plus loin) et un ensemble de tâches en fonction du nombre de hello de conteneurs dans le compte de stockage hello. Vous pouvez télécharger les scripts de hello référentiel github de hello.

* [Client Node.js](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [Scripts Shell de la tâche de préparation](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [Processeur de Python csv tooJSON](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> client de Node.js Hello dans lien hello spécifié ne contient-elle pas de toobe code spécifique déployé comme une application Azure (fonction). Vous pouvez faire référence toohello suivant les liens pour toocreate d’instructions une.
> - [Créer une application de fonction](../azure-functions/functions-create-first-azure-function.md)
> - [Créer une fonction de déclencheur de minuteur](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-hello-application"></a>Générez l’application hello

Maintenant, nous suivez le processus de hello étape par étape dans la génération de hello Node.js client :

### <a name="step-1-install-azure-batch-sdk"></a>Étape 1 : installer le Kit de développement logiciel (SDK) Azure Batch

Vous pouvez installer le Kit de développement logiciel Azure Batch pour Node.js à l’aide de la commande d’installation npm hello.

`npm install azure-batch`

Cette commande installe la version la plus récente hello du nœud de traitement par lots d’azure SDK.

>[!Tip]
> Dans une application de la fonction d’Azure, vous pouvez passer des paramètres de « Kudu Console « Bonjour Azure fonction onglet toorun hello npm trop des commandes d’installation. Dans cette tooinstall cas SDK de traitement par lots Azure pour Node.js.
>
>

### <a name="step-2-create-an-azure-batch-account"></a>Étape 2 : Créer un compte Azure Batch

Vous pouvez le créer à partir de hello [portail Azure](batch-account-create-portal.md) ou à partir de la ligne de commande ([Powershell](batch-powershell-cmdlets-get-started.md) /[cli Azure](https://docs.microsoft.com/cli/azure/overview)).

Voici les toocreate de commandes hello une via l’interface CLI d’Azure.

Créer un groupe de ressources, ignorez cette étape si vous avez déjà une où vous souhaitez toocreate hello compte Batch :

`az group create -n "<resource-group-name>" -l "<location>"`

Créez ensuite un compte Azure Batch.

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

Chaque compte Batch possède ses clés d’accès correspondantes. Ces clés sont nécessaires toocreate des ressources supplémentaires dans le compte de traitement par lots Azure. Une bonne pratique pour l’environnement de production est toouse Azure Key Vault toostore ces clés. Vous pouvez ensuite créer un Service principal pour l’application hello. Cette application hello principal de service permet de créer un jeton tooaccess les clés OAuth hello coffre de clés.

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

Copiez et stockez hello clé toobe est utilisé dans les étapes suivantes hello.

### <a name="step-3-create-an-azure-batch-service-client"></a>Étape 3 : créer un client du service Azure Batch
Extrait de code suivant tout d’abord importe module Node.js de traitement par lots d’azure hello et crée ensuite un client de Service de traitement par lots. Vous devez toofirst créer un objet SharedKeyCredentials avec la clé du compte Batch hello copié à partir de l’étape précédente de hello.

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

Hello URI du lot Azure sont accessibles dans l’onglet vue d’ensemble de hello Hello portail Azure. Il est de format de hello :

`https://accountname.location.batch.azure.com`

Consultez la capture d’écran de toohello :

![URI Azure Batch](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a>Étape 4 : créer un pool Azure Batch
Un pool Azure Batch se compose de plusieurs machines virtuelles (également appelées nœuds Batch). Service de traitement par lots Azure déploie des tâches hello sur ces nœuds et les gère. Vous pouvez définir hello suivant les paramètres de configuration pour le pool.

* Type d’image de machine virtuelle
* Taille des nœuds de machine virtuelle
* Nombre de nœuds de machine virtuelle

> [!Tip]
> taille de Hello et le nombre de nœuds de l’ordinateur virtuel dépendent en grande partie nombre hello de tâches que vous souhaitez toorun en parallèle et également hello lui-même. Nous vous recommandons de tester le nombre idéal de toodetermine hello et la taille.
>
>

Hello extrait de code suivant crée hello les objets de paramètre de configuration.

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
> Pour hello la liste d’images Linux VM disponibles pour le traitement par lots Azure et leurs ID de référence (SKU), consultez [la liste des images de machine virtuelle](batch-linux-nodes.md#list-of-virtual-machine-images).
>
>

Une fois la configuration du pool hello est définie, vous pouvez créer le pool de traitement par lots Azure hello. Hello commande de pool de traitement par lots crée des nœuds de Machine virtuelle Azure et les prépare tooexecute de tâches toobe tooreceive prêt. Chaque pool doit posséder un ID unique à titre de référence pour les étapes suivantes.

Hello suivant extrait de code crée un pool de traitement par lots Azure.

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating hello Pool for hello specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

Vous pouvez vérifier l’état de hello du regroupement hello créé et vous assurer que hello état est « actif » avant de poursuivre avec l’envoi d’un pool de toothat de travail.

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

Voici un exemple d’objet résultat retourné par la fonction de pool.get hello.

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


### <a name="step-4-submit-an-azure-batch-job"></a>Étape 4 : soumettre un travail Azure Batch
Un travail Azure Batch est un groupe logique de tâches similaires. Dans notre scénario, il est « TooJSON csv de processus. » Ici, chaque tâche peut traiter les fichiers csv présents dans chaque conteneur Stockage Azure.

Ces tâches sont exécute en parallèle et déploiement sur plusieurs nœuds, orchestrées par le service de traitement par lots Azure hello.

> [!Tip]
> Vous pouvez utiliser hello [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) propriété toospecify maximum de tâches pouvant s’exécuter simultanément sur un nœud unique.
>
>

#### <a name="preparation-task"></a>Tâche de préparation

les nœuds de machine virtuelle Hello créés sont les nœuds de Ubuntu vides. Vous devez souvent tooinstall un ensemble de programmes comme composants requis.
En règle générale, pour les nœuds de Linux, vous pouvez avoir un script shell qui installe les composants requis de hello avant l’exécution de tâches réelles hello. Cependant, il peut s’agir de n’importe quel exécutable programmable.
Hello [script du shell](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) dans cet exemple installe le pip de Python et hello stockage Azure SDK pour Python.

Vous pouvez télécharger le script hello sur un compte Azure Storage et générer un script de hello tooaccess URI SAS. Ce processus peut également être automatisé à l’aide de hello Node.js de stockage Windows Azure SDK.

> [!Tip]
> Une tâche de préparation d’une tâche s’exécute uniquement sur les nœuds de machine virtuelle hello où les tâches spécifiques hello doit toorun. Si vous souhaitez toobe des composants requis installé sur tous les nœuds, quelles que soient les tâches hello qui s’y exécutent, vous pouvez utiliser hello [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) propriété lors de l’ajout d’un pool. Vous pouvez utiliser hello après la définition de tâche de préparation pour référence.
>
>

Une tâche de préparation est spécifiée lors de l’envoi de hello de traitement par lots Azure. Suivantes sont hello des paramètres de configuration de tâche de préparation :

* **ID**: un identificateur unique pour la tâche de préparation hello
* **ligne de commande**: ligne de commande tooexecute hello exécutable de la tâche
* **resourceFiles**: tableau d’objets qui fournissent des détails des fichiers nécessaires toobe téléchargé pour toorun de cette tâche.  Ses options sont les suivantes :
    - blobSource : hello URI SAS du fichier de hello
    - filePath : toodownload de chemin d’accès Local et enregistrez le fichier de hello
    - fileMode : applicable uniquement pour les nœuds Linux, fileMode est au format octal avec la valeur 0770 par défaut
* **waitForSuccess**: si l’ensemble tootrue, tâche hello ne fonctionne pas sur les échecs des tâches de préparation
* **runElevated**: définir tootrue si des privilèges élevés sont des tâches de hello toorun nécessaires.

Extrait de code suivant montre un exemple de configuration hello préparation tâche script :

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

S’il n’y a aucune toobe composants requis installé pour votre toorun de tâches, vous pouvez ignorer les tâches de préparation hello. Le code suivant crée un travail dont le nom d’affichage est « process csv files ».

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


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a>Étape 5 : soumettre des tâches Azure Batch pour un travail

Maintenant que le travail de traitement des fichiers csv est créé, nous allons créer des tâches pour celui-ci. En supposant que nous avons quatre conteneurs, nous avons toocreate quatre tâches, une pour chaque conteneur.

Si nous examinons hello [script Python](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), elle accepte deux paramètres :

* nom du conteneur : hello des fichiers de toodownload conteneur de stockage à partir de
* modèle : paramètre facultatif d’un modèle de nom de fichier

En supposant que nous avons quatre conteneurs « con1 », « con2 », « con3 », « con4 » de code suivant illustre soumettre pour tâches toohello Azure batch travail « processus csv » créée précédemment.

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

code de Hello ajoute un pool de toohello plusieurs tâches. Et chacune des tâches de hello est exécuté sur un nœud dans le pool hello de machines virtuelles créées. Si nombre hello de tâches dépasse le nombre hello d’ordinateurs virtuels dans une propriété maxTasksPerNode pool ou hello, les tâches hello patienter jusqu'à ce qu’un nœud est rendu disponible. Cette orchestration est gérée automatiquement par Azure Batch.

portail de Hello détaille les vues sur les États des travaux et les tâches de hello. Vous pouvez également utiliser la liste de hello et obtenir des fonctions Bonjour Azure SDK de nœud. Détails sont fournis dans la documentation de hello [lien](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).

## <a name="next-steps"></a>Étapes suivantes

- Hello de révision [les fonctionnalités de présentation d’Azure Batch](batch-api-basics.md) article, nous vous recommandons de si vous êtes de nouveau service toohello.
- Consultez hello [lot Node.js référence](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/) tooexplore hello API de lot.

