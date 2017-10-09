---
title: "aaaRun Azure Batch travaux de bout en bout sans écrire de code (version préliminaire) | Documents Microsoft"
description: "Créer des fichiers de modèles pour les pools de lot toocreate hello CLI d’Azure, des tâches et des tâches."
services: batch
author: mscurrell
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: na
ms.topic: article
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: markscu
ms.openlocfilehash: c0434d09766451f6ba516efbad949834711ee819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="fec34-103">Utiliser des modèles d’interface CLI Azure Batch et le transfert de fichiers (préversion)</span><span class="sxs-lookup"><span data-stu-id="fec34-103">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="fec34-104">À l’aide de hello CLI d’Azure il s’agit des traitements toorun possible sans écrire de code.</span><span class="sxs-lookup"><span data-stu-id="fec34-104">Using hello Azure CLI it is possible toorun Batch jobs without writing code.</span></span>

<span data-ttu-id="fec34-105">Fichiers de modèle peuvent être créés et utilisés avec hello CLI d’Azure qui permettent de lot pools, de tâches toobe tâches créé.</span><span class="sxs-lookup"><span data-stu-id="fec34-105">Template files can be created and used with hello Azure CLI that allow Batch pools, jobs, and tasks toobe created.</span></span> <span data-ttu-id="fec34-106">Fichiers d’entrée de travail peuvent être facilement transférées au compte de stockage hello associé hello lot compte et le travail de fichiers de sortie téléchargés.</span><span class="sxs-lookup"><span data-stu-id="fec34-106">Job input files can be easily uploaded to hello storage account associated with hello Batch account and job output files downloaded.</span></span>

## <a name="overview"></a><span data-ttu-id="fec34-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="fec34-107">Overview</span></span>

<span data-ttu-id="fec34-108">Une extension de toohello CLI d’Azure permet de lot toobe utilisée de bout en bout par les utilisateurs qui ne sont pas des développeurs.</span><span class="sxs-lookup"><span data-stu-id="fec34-108">An extension toohello Azure CLI enables Batch toobe used end-to-end by users who are not developers.</span></span> <span data-ttu-id="fec34-109">Un pool peut être créé et téléchargement de données d’entrée, tâches et les tâches associées créés, hello sortie données résultantes téléchargées – aucun code requis, hello CLI utilisée directement ou intégrées dans les scripts.</span><span class="sxs-lookup"><span data-stu-id="fec34-109">A pool can be created, input data uploaded, jobs and associated tasks created, and hello resulting output data downloaded – no code required, hello CLI being used directly or being integrated into scripts.</span></span>

<span data-ttu-id="fec34-110">Générer des modèles de traitement par lots sur hello [prise en charge de traitement par lots existante Bonjour Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) qui permet de fichiers JSON toospecify les valeurs de propriété pour la création de hello de pools, travaux, tâches et autres éléments.</span><span class="sxs-lookup"><span data-stu-id="fec34-110">Batch templates build on hello [existing Batch support in hello Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) that allows JSON files toospecify property values for hello creation of pools, jobs, tasks, and other items.</span></span> <span data-ttu-id="fec34-111">Avec les modèles de lot, hello fonctionnalités suivantes sont ajoutées sur ce qui est possible avec les fichiers au format JSON hello :</span><span class="sxs-lookup"><span data-stu-id="fec34-111">With Batch templates, hello following capabilities are added over what is possible with hello JSON files:</span></span>

-   <span data-ttu-id="fec34-112">Des paramètres peuvent être définis.</span><span class="sxs-lookup"><span data-stu-id="fec34-112">Parameters can be defined.</span></span> <span data-ttu-id="fec34-113">Lorsque le modèle de hello est utilisé, seules les valeurs de paramètre hello sont des éléments de hello de toocreate spécifié, avec d’autres valeurs de propriété d’élément spécifiée dans le corps du modèle hello.</span><span class="sxs-lookup"><span data-stu-id="fec34-113">When hello template is used, only hello parameter values are specified toocreate hello item, with other item property values being specified in hello template body.</span></span> <span data-ttu-id="fec34-114">Un utilisateur qui comprend le traitement par lots et l’applications toobe exécutent par lot peut créer des modèles, en spécifiant le pool de travail et les valeurs de propriété de tâche.</span><span class="sxs-lookup"><span data-stu-id="fec34-114">A user who understands Batch and the applications toobe run by Batch can create templates, specifying pool, job, and task property values.</span></span> <span data-ttu-id="fec34-115">Un utilisateur moins familiarisés avec le lot et/ou les applications doit uniquement les valeurs hello toospecify pour les paramètres de hello défini.</span><span class="sxs-lookup"><span data-stu-id="fec34-115">A user less familiar with Batch and/or the applications only needs toospecify hello values for hello defined parameters.</span></span>

-   <span data-ttu-id="fec34-116">Fabriques de tâches de travail en créer un ou plusieurs tâches associées à un travail, ce qui évite de hello ont besoin pour de nombreux toobe de définitions de tâche créé et ce qui simplifie considérablement la soumission de travaux.</span><span class="sxs-lookup"><span data-stu-id="fec34-116">Job task factories create one or more tasks associated with a job, avoiding hello need for many task definitions toobe created and significantly simplifying job submission.</span></span>


<span data-ttu-id="fec34-117">Les fichiers de données d’entrée doivent toobe fourni pour les travaux et entraînait souvent des fichiers de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="fec34-117">Input data files need toobe supplied for jobs and output data files are often produced.</span></span> <span data-ttu-id="fec34-118">Un compte de stockage est associé, par défaut, chaque lot compte et les fichiers peuvent être facilement transféré tooand à partir de ce compte de stockage à l’aide de l’interface CLI, sans codage, et aucune information d’identification de stockage ne requis.</span><span class="sxs-lookup"><span data-stu-id="fec34-118">A storage account is associated, by default, with each Batch account and files can be easily transferred tooand from this storage account using the CLI, with no coding and no storage credentials required.</span></span>

<span data-ttu-id="fec34-119">Par exemple, [ffmpeg](http://ffmpeg.org/) est une application courante qui traite les fichiers audio et vidéo.</span><span class="sxs-lookup"><span data-stu-id="fec34-119">For example, [ffmpeg](http://ffmpeg.org/) is a popular application that processes audio and video files.</span></span> <span data-ttu-id="fec34-120">Hello CLI de traitement par lots Azure peut être utilisé tooinvoke ffmpeg tootranscode source des fichiers vidéo toodifferent résolutions.</span><span class="sxs-lookup"><span data-stu-id="fec34-120">hello Azure Batch CLI can be used tooinvoke ffmpeg tootranscode source video files toodifferent resolutions.</span></span>

-   <span data-ttu-id="fec34-121">Un modèle de pool est créé.</span><span class="sxs-lookup"><span data-stu-id="fec34-121">A pool template is created.</span></span> <span data-ttu-id="fec34-122">utilisateur Hello création hello modèle sait comment toocall hello ffmpeg application et ses besoins ; ils spécifient hello système d’exploitation approprié, la machine virtuelle de taille, comment ffmpeg est installée (à partir d’un package d’application ou à l’aide d’un gestionnaire de package, par exemple) et d’autres valeurs de propriété du pool.</span><span class="sxs-lookup"><span data-stu-id="fec34-122">hello user creating hello template knows how toocall hello ffmpeg application and its requirements; they specify hello appropriate OS, VM size, how ffmpeg is installed (from an application package or using a package manager, for example), and other pool property values.</span></span> <span data-ttu-id="fec34-123">Paramètres sont créés lorsque le modèle de hello est utilisé, seuls les id du pool hello et nombre d’ordinateurs virtuels devez toobe spécifié.</span><span class="sxs-lookup"><span data-stu-id="fec34-123">Parameters are created so when hello template is used, only hello pool id and number of VMs need toobe specified.</span></span>

-   <span data-ttu-id="fec34-124">Un modèle de travail est créé.</span><span class="sxs-lookup"><span data-stu-id="fec34-124">A job template is created.</span></span> <span data-ttu-id="fec34-125">le modèle de hello création Hello utilisateur sait comment ffmpeg besoins toobe appelé autre résolution tootranscode source vidéo tooa et spécifie la ligne de commande de tâche hello ; ils savent également qu’il existe un dossier contenant des fichiers vidéo source de hello, avec une tâche requise par le fichier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="fec34-125">hello user creating hello template knows how ffmpeg needs toobe invoked tootranscode source video tooa different resolution and specifies hello task command line; they also know that there is a folder containing hello source video files, with a task required per input file.</span></span>

-   <span data-ttu-id="fec34-126">Un utilisateur final avec un ensemble de fichiers vidéo tootranscode crée d’abord un pool à l’aide du modèle de pool hello, en spécifiant uniquement id de pool hello et le nombre d’ordinateurs virtuels requis.</span><span class="sxs-lookup"><span data-stu-id="fec34-126">An end user with a set of video files tootranscode first creates a pool using hello pool template, specifying only hello pool id and number of VMs required.</span></span> <span data-ttu-id="fec34-127">Ils peuvent ensuite télécharger tootranscode de fichiers source hello.</span><span class="sxs-lookup"><span data-stu-id="fec34-127">They can then upload hello source files tootranscode.</span></span> <span data-ttu-id="fec34-128">Un travail peut ensuite être envoyé à l’aide du modèle de projet hello, en spécifiant uniquement l’id de pool hello et emplacement des fichiers de source de hello téléchargés.</span><span class="sxs-lookup"><span data-stu-id="fec34-128">A job can then be submitted using hello job template, specifying only hello pool id and location of hello source files uploaded.</span></span> <span data-ttu-id="fec34-129">traitement par lots Hello est créé, avec une tâche par le fichier d’entrée qui est généré.</span><span class="sxs-lookup"><span data-stu-id="fec34-129">hello Batch job is created, with one task per input file being generated.</span></span> <span data-ttu-id="fec34-130">Enfin, les fichiers de sortie hello transcodé peuvent être téléchargement.</span><span class="sxs-lookup"><span data-stu-id="fec34-130">Finally, hello transcoded output files can be download.</span></span>

## <a name="installation"></a><span data-ttu-id="fec34-131">Installation</span><span class="sxs-lookup"><span data-stu-id="fec34-131">Installation</span></span>

<span data-ttu-id="fec34-132">fonctionnalités de transfert de modèle et de fichier Hello nécessitent un toobe extension installée.</span><span class="sxs-lookup"><span data-stu-id="fec34-132">hello template and file transfer capabilities require an extension toobe installed.</span></span>

<span data-ttu-id="fec34-133">Pour obtenir des instructions sur tooinstall hello CLI d’Azure voir [installer Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fec34-133">For instructions on how tooinstall hello Azure CLI see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="fec34-134">Une fois hello que CLI d’Azure a été installé, hello lot extension peut être installée à l’aide de la commande CLI suivante :</span><span class="sxs-lookup"><span data-stu-id="fec34-134">Once hello Azure CLI has been installed, hello Batch extension can be installed using the following CLI command:</span></span>

```azurecli
az component update --add batch-extensions --allow-third-party
```

<span data-ttu-id="fec34-135">Pour plus d’informations sur l’extension de traitement par lots de hello, consultez [Microsoft Azure Batch CLI Extensions pour Windows, Mac et Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span><span class="sxs-lookup"><span data-stu-id="fec34-135">For more information about hello Batch extension, see [Microsoft Azure Batch CLI Extensions for Windows, Mac and Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span></span>

## <a name="templates"></a><span data-ttu-id="fec34-136">Modèles</span><span class="sxs-lookup"><span data-stu-id="fec34-136">Templates</span></span>

<span data-ttu-id="fec34-137">Hello CLI d’Azure Batch autorise des éléments tels que les pools, toobe de tâches créée en spécifiant un fichier JSON qui contient les noms de propriété et les valeurs de tâches.</span><span class="sxs-lookup"><span data-stu-id="fec34-137">hello Azure Batch CLI allows items such as pools, jobs, and tasks toobe created by specifying a JSON file containing property names and values.</span></span> <span data-ttu-id="fec34-138">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="fec34-138">For example:</span></span>

```azurecli
az batch pool create –-json-file AppPool.json
```

<span data-ttu-id="fec34-139">Modèles de traitement par lots Azure sont des modèles de gestionnaire de ressources tooAzure similaires, dans la syntaxe et des fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="fec34-139">Azure Batch templates are similar tooAzure Resource Manager templates, in functionality and syntax.</span></span> <span data-ttu-id="fec34-140">Ils sont des fichiers JSON qui contiennent des valeurs et les noms de propriété d’élément, mais ajouter hello suivant des principaux concepts :</span><span class="sxs-lookup"><span data-stu-id="fec34-140">They are JSON files that contain item property names and values, but add hello following main concepts:</span></span>

-   <span data-ttu-id="fec34-141">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="fec34-141">**Parameters**</span></span>

    -   <span data-ttu-id="fec34-142">Autoriser toobe de valeurs de propriété spécifié dans une section de corps, avec uniquement les valeurs de paramètre nécessitant toobe fourni lorsque le modèle de hello est utilisé.</span><span class="sxs-lookup"><span data-stu-id="fec34-142">Allow property values toobe specified in a body section, with only parameter values needing toobe supplied when hello template is used.</span></span> <span data-ttu-id="fec34-143">Par exemple, définition complète de hello pour un pool peut être placée dans le corps de hello et qu’un seul paramètre défini pour l’id du pool ; uniquement une chaîne d’id pool doit par conséquent toobe fourni toocreate un pool.</span><span class="sxs-lookup"><span data-stu-id="fec34-143">For example, hello complete definition for a pool could be placed in hello body and only one parameter defined for pool id; only a pool id string therefore needs toobe supplied toocreate a pool.</span></span>
        
    -   <span data-ttu-id="fec34-144">corps de modèle Hello peuvent être créés par une personne disposant de connaissances du lot et hello applications toobe exécutée par le traitement par lots ; Seules les valeurs des paramètres définis par l’auteur de hello doivent être fournis lorsque le modèle de hello est utilisé.</span><span class="sxs-lookup"><span data-stu-id="fec34-144">hello template body can be authored by someone with knowledge of Batch and hello applications toobe run by Batch; only values for hello author-defined parameters must be supplied when hello template is used.</span></span> <span data-ttu-id="fec34-145">Un utilisateur sans hello lot détaillée et/ou des connaissances de l’application peut par conséquent utiliser les modèles.</span><span class="sxs-lookup"><span data-stu-id="fec34-145">A user without hello in-depth Batch and/or application knowledge can therefore use the templates.</span></span>

-   <span data-ttu-id="fec34-146">**Variables**</span><span class="sxs-lookup"><span data-stu-id="fec34-146">**Variables**</span></span>

    -   <span data-ttu-id="fec34-147">Autoriser toobe de valeurs de paramètre simple ou complexe spécifié dans un seul emplacement et utilisé dans un ou plusieurs emplacements dans le corps du modèle hello.</span><span class="sxs-lookup"><span data-stu-id="fec34-147">Allow simple or complex parameter values toobe specified in one place and used in one or more places in hello template body.</span></span> <span data-ttu-id="fec34-148">Les variables peuvent simplifier et réduire la taille de hello du modèle de hello, ainsi rendre plus facile à gérer en ayant en un emplacement toochange propriétés dont la valeur peut changer.</span><span class="sxs-lookup"><span data-stu-id="fec34-148">Variables can simplify and reduce hello size of hello template, as well as make it more maintainable by having one location toochange properties whose value may change.</span></span>

-   <span data-ttu-id="fec34-149">**Constructions de niveau supérieur**</span><span class="sxs-lookup"><span data-stu-id="fec34-149">**Higher-level constructs**</span></span>

    -   <span data-ttu-id="fec34-150">Certaines constructions de niveau supérieur sont disponibles dans le modèle hello qui ne sont pas encore disponibles dans hello API de lot.</span><span class="sxs-lookup"><span data-stu-id="fec34-150">Some higher-level constructs are available in hello template that are not yet available in hello Batch APIs.</span></span> <span data-ttu-id="fec34-151">Par exemple, une fabrique de tâches peut être définie dans un modèle de tâche qui crée plusieurs tâches pour la tâche hello à l’aide d’une définition de tâche commune.</span><span class="sxs-lookup"><span data-stu-id="fec34-151">For example, a task factory can be defined in a job template that creates multiple tasks for hello job using a common task definition.</span></span> <span data-ttu-id="fec34-152">Ces constructions éviter toocode besoin de hello pour dynamiquement créer plusieurs fichiers JSON, telle qu’un fichier par la tâche, ainsi que de créer de script fichiers tooinstall applications via un gestionnaire de package, par exemple.</span><span class="sxs-lookup"><span data-stu-id="fec34-152">These constructs avoid hello need toocode to dynamically create multiple JSON files, such as one file per task, as well as create script files tooinstall applications via a package manager, for example.</span></span>

    -   <span data-ttu-id="fec34-153">À un point, si applicable, que ces constructions peuvent être ajoutées toothe lot service et disponible dans hello API de lot, les interfaces utilisateur, etc..</span><span class="sxs-lookup"><span data-stu-id="fec34-153">At some point, where applicable, these constructs may be added toothe Batch service and available in hello Batch APIs, UIs, etc.</span></span>

### <a name="pool-templates"></a><span data-ttu-id="fec34-154">Modèles de pool</span><span class="sxs-lookup"><span data-stu-id="fec34-154">Pool templates</span></span>

<span data-ttu-id="fec34-155">En outre, toohello des fonctions de modèle standard des paramètres et des variables, hello suivant des structures de niveau supérieur sont pris en charge par le modèle de pool hello :</span><span class="sxs-lookup"><span data-stu-id="fec34-155">In addition toohello standard template capabilities of parameters and variables, hello following higher-level constructs are supported by hello pool template:</span></span>

-   <span data-ttu-id="fec34-156">**Références de package**</span><span class="sxs-lookup"><span data-stu-id="fec34-156">**Package references**</span></span>

    -   <span data-ttu-id="fec34-157">Si vous le souhaitez permet aux logiciels toobe copié toopool nœuds à l’aide du package gestionnaires.</span><span class="sxs-lookup"><span data-stu-id="fec34-157">Optionally allows software toobe copied toopool nodes by using package managers.</span></span> <span data-ttu-id="fec34-158">Gestionnaire de package Hello et id de package sont spécifiés.</span><span class="sxs-lookup"><span data-stu-id="fec34-158">hello package manager and package id are specified.</span></span> <span data-ttu-id="fec34-159">Qui est en mesure de toodeclare un ou plusieurs packages évite hello besoin toocreate un script qui obtient les packages de hello requis, hello script d’installation et exécuter le script de hello sur chaque nœud du pool.</span><span class="sxs-lookup"><span data-stu-id="fec34-159">Being able toodeclare one or more packages avoids hello need toocreate a script that gets hello required packages, install hello script, and run hello script on each pool node.</span></span>

<span data-ttu-id="fec34-160">Hello Voici un exemple d’un modèle qui crée un pool de machines virtuelles Linux avec ffmpeg installé et que seul nécessite un pool id chaîne hello nombre et de machines virtuelles toobe fourni toouse :</span><span class="sxs-lookup"><span data-stu-id="fec34-160">hello following is an example of a template that creates a pool of Linux VMs with ffmpeg installed and only requires a pool id string and hello number of VMs toobe supplied toouse:</span></span>

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "hello number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello pool id "
            }
        }
    },
    "pool": {
        "type": "Microsoft.Batch/batchAccounts/pools",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('poolId')]",
            "virtualMachineConfiguration": {
                "imageReference": {
                    "publisher": "Canonical",
                    "offer": "UbuntuServer",
                    "sku": "16.04.0-LTS",
                    "version": "latest"
                },
                "nodeAgentSKUId": "batch.node.ubuntu 16.04"
            },
            "vmSize": "STANDARD_D3_V2",
            "targetDedicatedNodes": "[parameters('nodeCount')]",
            "enableAutoScale": false,
            "maxTasksPerNode": 1,
            "packageReferences": [
                {
                    "type": "aptPackage",
                    "id": "ffmpeg"
                }
            ]
        }
    }
}
```

<span data-ttu-id="fec34-161">Si le fichier de modèle hello était nommé _ffmpeg.json-pool_, puis le modèle de hello serait appelé comme suit :</span><span class="sxs-lookup"><span data-stu-id="fec34-161">If hello template file was named _pool-ffmpeg.json_, then hello template would be invoked as follows:</span></span>

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a><span data-ttu-id="fec34-162">Modèles de travail</span><span class="sxs-lookup"><span data-stu-id="fec34-162">Job templates</span></span>

<span data-ttu-id="fec34-163">En outre, toohello des fonctions de modèle standard des paramètres et des variables, hello suivant des structures de niveau supérieur sont pris en charge par le modèle de tâche hello :</span><span class="sxs-lookup"><span data-stu-id="fec34-163">In addition toohello standard template capabilities of parameters and variables, hello following higher-level constructs are supported by hello job template:</span></span>

-   <span data-ttu-id="fec34-164">**Fabrique de tâches**</span><span class="sxs-lookup"><span data-stu-id="fec34-164">**Task factory**</span></span>

    -   <span data-ttu-id="fec34-165">Crée plusieurs tâches pour un travail à partir d’une définition de tâche.</span><span class="sxs-lookup"><span data-stu-id="fec34-165">Creates multiple tasks for a job from one task definition.</span></span> <span data-ttu-id="fec34-166">Trois types de fabrique de tâches sont pris en charge : balayage paramétrique, tâche par fichier et collection de tâches.</span><span class="sxs-lookup"><span data-stu-id="fec34-166">Three types of task factory are supported – parametric sweep, task per file, and task collection.</span></span>

<span data-ttu-id="fec34-167">Hello Voici un exemple d’un modèle qui crée une tâche qui utilise ffmpeg pour transcoder tooone de fichiers vidéo MP4 de deux résolutions inférieures, avec une tâche créée par le fichier vidéo source :</span><span class="sxs-lookup"><span data-stu-id="fec34-167">hello following is an example of a template that creates a job that uses ffmpeg to transcode MP4 video files tooone of two lower resolutions, with one task created per source video file:</span></span>

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch pool which runs hello job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch job"
            }
        },
        "resolution": {
            "type": "string",
            "defaultValue": "428x240",
            "allowedValues": [
                "428x240",
                "854x480"
            ],
            "metadata": {
                "description": "Target video resolution"
            }
        }
    },
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('jobId')]",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "[parameters('poolId')]"
            },
            "taskFactory": {
                "type": "taskPerFile",
                "source": { 
                    "fileGroup": "ffmpeg-input"
                },
                "repeatTask": {
                    "commandLine": "ffmpeg -i {fileName} -y -s [parameters('resolution')] -strict -2 {fileNameWithoutExtension}_[parameters('resolution')].mp4",
                    "resourceFiles": [
                        {
                            "blobSource": "{url}",
                            "filePath": "{fileName}"
                        }
                    ],
                    "outputFiles": [
                        {
                            "filePattern": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                            "destination": {
                                "autoStorage": {
                                    "path": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                                    "fileGroup": "ffmpeg-output"
                                }
                            },
                            "uploadOptions": {
                                "uploadCondition": "TaskSuccess"
                            }
                        }
                    ]
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```

<span data-ttu-id="fec34-168">Si le fichier de modèle hello était nommé _ffmpeg.json de travail_, puis le modèle de hello serait appelé comme suit :</span><span class="sxs-lookup"><span data-stu-id="fec34-168">If hello template file was named _job-ffmpeg.json_, then hello template would be invoked as follows:</span></span>

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a><span data-ttu-id="fec34-169">Groupes de fichiers et transfert de fichiers</span><span class="sxs-lookup"><span data-stu-id="fec34-169">File groups and file transfer</span></span>

<span data-ttu-id="fec34-170">La plupart des travaux et des tâches requièrent les fichiers d’entrée et produisent des fichiers de sortie.</span><span class="sxs-lookup"><span data-stu-id="fec34-170">Most jobs and tasks require input files and produce output files.</span></span> <span data-ttu-id="fec34-171">Les deux fichiers d’entrée et les fichiers de sortie est généralement nécessaire toobe transféré, à partir du nœud de toohello hello client ou à partir du client de toohello nœud hello.</span><span class="sxs-lookup"><span data-stu-id="fec34-171">Both input files and output files typically need toobe transferred, either from hello client toohello node, or from hello node toohello client.</span></span> <span data-ttu-id="fec34-172">Hello extension d’Azure Batch CLI s’approprie le transfert de fichiers absent et utilise le compte de stockage hello est créé par défaut pour chaque compte de traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="fec34-172">hello Azure Batch CLI extension abstracts away file transfer and utilizes hello storage account that is created by default for each Batch account.</span></span>

<span data-ttu-id="fec34-173">Un groupe de fichiers équivaut tooa conteneur qui est créé dans hello compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="fec34-173">A file group equates tooa container that is created in hello Azure storage account.</span></span> <span data-ttu-id="fec34-174">groupe de fichiers Hello peut comporter des sous-dossiers.</span><span class="sxs-lookup"><span data-stu-id="fec34-174">hello file group may have subfolders.</span></span>

<span data-ttu-id="fec34-175">Hello, extension de traitement par lots CLI fournit des commandes pour le téléchargement de fichiers à partir du groupe de fichiers spécifié tooa client et télécharger des fichiers à partir du client de tooa groupe hello fichier spécifié.</span><span class="sxs-lookup"><span data-stu-id="fec34-175">hello Batch CLI extension provides commands for uploading files from client tooa specified file group and downloading files from hello specified file group tooa client.</span></span>

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

<span data-ttu-id="fec34-176">Modèles de pool et de travail permettent de fichiers stockés dans toobe de groupes de fichiers spécifié pour la copie sur les nœuds de pool ou hors pool nœuds sauvegarder le groupe de fichiers tooa.</span><span class="sxs-lookup"><span data-stu-id="fec34-176">Pool and job templates allow files stored in file groups toobe specified for copy onto pool nodes or off pool nodes back tooa file group.</span></span> <span data-ttu-id="fec34-177">Par exemple, dans le modèle de projet spécifié précédemment, hello fichier groupe « ffmpeg-entrée » n’est spécifiée pour la fabrique de tâches hello en tant qu’emplacement hello des fichiers vidéo de hello source copiés vers le bas sur le nœud hello pour le transcodage ; groupe « ffmpeg-sortie de Hello fichier » est utilisé comme emplacement des fichiers de sortie hello transcodé hello copiés nœud de hello toofrom chaque tâche en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="fec34-177">For example, in the job template specified previously, hello file group “ffmpeg-input” is specified for hello task factory as hello location of hello source video files copied down onto hello node for transcoding; hello file group “ffmpeg-output” is used as hello location where hello transcoded output files are copied toofrom hello node running each task.</span></span>

## <a name="summary"></a><span data-ttu-id="fec34-178">Résumé</span><span class="sxs-lookup"><span data-stu-id="fec34-178">Summary</span></span>

<span data-ttu-id="fec34-179">Prise en charge du transfert modèle et de fichier actuellement ajoutés uniquement toohello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="fec34-179">Template and file transfer support have currently been added only toohello Azure CLI.</span></span> <span data-ttu-id="fec34-180">Hello vise audience hello tooexpand qui permet de toousers de lot qui n’ont pas besoin de code toodevelop à l’aide de hello API de lot, tels que les chercheurs, les utilisateurs et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="fec34-180">hello goal is tooexpand hello audience that can use Batch toousers who do not need toodevelop code using hello Batch APIs, such as researchers, IT users, and so on.</span></span> <span data-ttu-id="fec34-181">Sans effectuer de codage, les utilisateurs possédant des connaissances de Azure, lot et toobe d’applications hello exécutée par traitement peuvent créer des modèles pour la création de pool et de travail.</span><span class="sxs-lookup"><span data-stu-id="fec34-181">Without coding, users with knowledge of Azure, Batch, and hello applications toobe run by Batch can create templates for pool and job creation.</span></span> <span data-ttu-id="fec34-182">Paramètres de modèle, les utilisateurs sans une connaissance détaillée de lot et hello applications peuvent utiliser les modèles de hello.</span><span class="sxs-lookup"><span data-stu-id="fec34-182">With template parameters, users without detailed knowledge of Batch and hello applications can use hello templates.</span></span>

<span data-ttu-id="fec34-183">Tester hello extension de traitement par lots pour hello CLI d’Azure et nous fournir des commentaires ou des suggestions, soit hello dans les commentaires pour cet article ou via hello [forum d’Azure Batch](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span><span class="sxs-lookup"><span data-stu-id="fec34-183">Try out hello Batch extension for hello Azure CLI and provide us with any feedback or suggestions, either in hello comments for this article or via hello [Azure Batch forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fec34-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fec34-184">Next steps</span></span>

- <span data-ttu-id="fec34-185">Voir hello lot modèles blog : [des travaux en cours d’exécution de traitement par lots Azure à l’aide de hello CLI d’Azure – aucun code requis](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span><span class="sxs-lookup"><span data-stu-id="fec34-185">See hello Batch templates blog post: [Running Azure Batch jobs using hello Azure CLI – no code required](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span></span>
- <span data-ttu-id="fec34-186">Code source, des exemples et documentation d’installation et d’utilisation détaillée sont disponibles dans hello [référentiel GitHub de Azure](https://github.com/Azure/azure-batch-cli-extensions).</span><span class="sxs-lookup"><span data-stu-id="fec34-186">Detailed installation and usage documentation, samples, and source code are available in hello [Azure GitHub repository](https://github.com/Azure/azure-batch-cli-extensions).</span></span>
