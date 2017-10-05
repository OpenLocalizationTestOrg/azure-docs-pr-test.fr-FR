---
title: "Exécuter des travaux Azure Batch de bout en bout sans écrire de code (préversion) | Microsoft Docs"
description: "Créez des modèles de fichier pour Azure CLI afin de créer des pools, travaux et tâches Batch."
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
ms.openlocfilehash: 6b91466da46d1f4ca9f25bf1718be783603efc58
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="9b5ed-103">Utiliser des modèles d’interface CLI Azure Batch et le transfert de fichiers (préversion)</span><span class="sxs-lookup"><span data-stu-id="9b5ed-103">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="9b5ed-104">Vous pouvez utiliser l’interface Azure CLI pour exécuter des travaux Batch sans écrire de code.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-104">Using the Azure CLI it is possible to run Batch jobs without writing code.</span></span>

<span data-ttu-id="9b5ed-105">Les fichiers de modèle peuvent être créés et utilisés avec Azure CLI qui autorise la création de pools, travaux et tâches Batch.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-105">Template files can be created and used with the Azure CLI that allow Batch pools, jobs, and tasks to be created.</span></span> <span data-ttu-id="9b5ed-106">Les fichiers d’entrée des travaux peuvent être facilement chargés sur le compte de stockage associé au compte Batch et aux fichiers de sortie de travaux téléchargés.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-106">Job input files can be easily uploaded to the storage account associated with the Batch account and job output files downloaded.</span></span>

## <a name="overview"></a><span data-ttu-id="9b5ed-107">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9b5ed-107">Overview</span></span>

<span data-ttu-id="9b5ed-108">Une extension de l’interface Azure CLI permet aux utilisateurs qui ne sont pas des développeurs d’utiliser Batch de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-108">An extension to the Azure CLI enables Batch to be used end-to-end by users who are not developers.</span></span> <span data-ttu-id="9b5ed-109">Un pool peut être créé, les données d’entrée chargées, les travaux et tâches associées créés et les données de sortie produites téléchargées. Aucun code n’est nécessaire, car l’interface CLI est utilisée directement ou intégrée à des scripts.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-109">A pool can be created, input data uploaded, jobs and associated tasks created, and the resulting output data downloaded – no code required, the CLI being used directly or being integrated into scripts.</span></span>

<span data-ttu-id="9b5ed-110">Les modèles Batch s’appuient sur la [prise en charge actuelle de Batch dans l’interface Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) qui permet aux fichiers JSON de spécifier des valeurs de propriété pour la création de pools, travaux, tâches et autres éléments.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-110">Batch templates build on the [existing Batch support in the Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) that allows JSON files to specify property values for the creation of pools, jobs, tasks, and other items.</span></span> <span data-ttu-id="9b5ed-111">Avec les modèles Batch, les fonctionnalités suivantes sont ajoutées à celles déjà disponibles avec les fichiers JSON :</span><span class="sxs-lookup"><span data-stu-id="9b5ed-111">With Batch templates, the following capabilities are added over what is possible with the JSON files:</span></span>

-   <span data-ttu-id="9b5ed-112">Des paramètres peuvent être définis.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-112">Parameters can be defined.</span></span> <span data-ttu-id="9b5ed-113">Lorsque le modèle est utilisé, seules les valeurs de paramètre sont spécifiées pour créer l’élément et les autres valeurs de propriété d’élément sont spécifiées dans le corps du modèle.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-113">When the template is used, only the parameter values are specified to create the item, with other item property values being specified in the template body.</span></span> <span data-ttu-id="9b5ed-114">Un utilisateur qui comprend Batch et les applications exécutées par Batch peut créer des modèles, en spécifiant les valeurs de propriété des pools, des travaux et des tâches.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-114">A user who understands Batch and the applications to be run by Batch can create templates, specifying pool, job, and task property values.</span></span> <span data-ttu-id="9b5ed-115">Un utilisateur moins familiarisé avec Batch et/ou les applications doit uniquement spécifier les valeurs des paramètres définis.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-115">A user less familiar with Batch and/or the applications only needs to specify the values for the defined parameters.</span></span>

-   <span data-ttu-id="9b5ed-116">Les fabriques de tâches de travail créent une ou plusieurs tâches associées à un travail sans avoir à créer des définitions de tâches, simplifiant considérablement les soumissions de travaux.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-116">Job task factories create one or more tasks associated with a job, avoiding the need for many task definitions to be created and significantly simplifying job submission.</span></span>


<span data-ttu-id="9b5ed-117">Des fichiers de données d’entrée doivent être fournis pour les travaux et des fichiers de données de sortie sont souvent produits.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-117">Input data files need to be supplied for jobs and output data files are often produced.</span></span> <span data-ttu-id="9b5ed-118">Par défaut, un compte de stockage est associé à chaque compte Batch et les fichiers peuvent être facilement transférés vers ou à partir de ce compte de stockage à l’aide de l’interface CLI, sans que du codage ou des informations d’identification de stockage ne soient requis.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-118">A storage account is associated, by default, with each Batch account and files can be easily transferred to and from this storage account using the CLI, with no coding and no storage credentials required.</span></span>

<span data-ttu-id="9b5ed-119">Par exemple, [ffmpeg](http://ffmpeg.org/) est une application courante qui traite les fichiers audio et vidéo.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-119">For example, [ffmpeg](http://ffmpeg.org/) is a popular application that processes audio and video files.</span></span> <span data-ttu-id="9b5ed-120">L’interface CLI d’Azure Batch peut servir à appeler ffmpeg pour transcoder les fichiers vidéo sources dans différentes résolutions.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-120">The Azure Batch CLI can be used to invoke ffmpeg to transcode source video files to different resolutions.</span></span>

-   <span data-ttu-id="9b5ed-121">Un modèle de pool est créé.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-121">A pool template is created.</span></span> <span data-ttu-id="9b5ed-122">L’utilisateur qui crée le modèle sait comment appeler l’application ffmpeg et connaît les prérequis. Il spécifie le système d’exploitation approprié, la taille de machine virtuelle, la façon dont ffmpeg est installé (à partir d’un package d’application ou à l’aide d’un gestionnaire de package, par exemple) et d’autres valeurs de propriété du pool.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-122">The user creating the template knows how to call the ffmpeg application and its requirements; they specify the appropriate OS, VM size, how ffmpeg is installed (from an application package or using a package manager, for example), and other pool property values.</span></span> <span data-ttu-id="9b5ed-123">Les paramètres sont créés de façon à ce que, lorsque le modèle est utilisé, seul l’ID du pool et le nombre de machines virtuelles doivent être spécifiés.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-123">Parameters are created so when the template is used, only the pool id and number of VMs need to be specified.</span></span>

-   <span data-ttu-id="9b5ed-124">Un modèle de travail est créé.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-124">A job template is created.</span></span> <span data-ttu-id="9b5ed-125">L’utilisateur qui crée le modèle sait comment appeler ffmpeg pour transcoder la vidéo source dans une résolution différente et spécifie la ligne de commande de la tâche. Il sait également qu’il y a un dossier contenant les fichiers vidéo sources, avec une tâche requise pour chaque fichier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-125">The user creating the template knows how ffmpeg needs to be invoked to transcode source video to a different resolution and specifies the task command line; they also know that there is a folder containing the source video files, with a task required per input file.</span></span>

-   <span data-ttu-id="9b5ed-126">Un utilisateur final avec un ensemble de fichiers vidéo à transcoder crée d’abord un pool à l’aide du modèle de pool, en spécifiant uniquement l’ID du pool et le nombre de machines virtuelles requises.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-126">An end user with a set of video files to transcode first creates a pool using the pool template, specifying only the pool id and number of VMs required.</span></span> <span data-ttu-id="9b5ed-127">Il peut ensuite charger les fichiers sources à transcoder.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-127">They can then upload the source files to transcode.</span></span> <span data-ttu-id="9b5ed-128">Un travail peut ensuite être soumis à l’aide du modèle de travail, en spécifiant uniquement l’ID du pool et l’emplacement des fichiers source chargés.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-128">A job can then be submitted using the job template, specifying only the pool id and location of the source files uploaded.</span></span> <span data-ttu-id="9b5ed-129">Le travail Batch est créé, avec une tâche par fichier d’entrée généré.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-129">The Batch job is created, with one task per input file being generated.</span></span> <span data-ttu-id="9b5ed-130">Enfin, les fichiers de sortie transcodés peuvent être téléchargés.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-130">Finally, the transcoded output files can be download.</span></span>

## <a name="installation"></a><span data-ttu-id="9b5ed-131">Installation</span><span class="sxs-lookup"><span data-stu-id="9b5ed-131">Installation</span></span>

<span data-ttu-id="9b5ed-132">Les fonctionnalités de transfert de fichiers et de modèle requièrent l’installation d’une extension.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-132">The template and file transfer capabilities require an extension to be installed.</span></span>

<span data-ttu-id="9b5ed-133">Pour obtenir des instructions sur l’installation de l’interface Azure CLI, consultez la page [Installation d’Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9b5ed-133">For instructions on how to install the Azure CLI see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="9b5ed-134">Une fois que l’interface Azure CLI est installée, l’extension Batch peut être installée en suivant les commandes de l’interface de ligne de commande suivantes :</span><span class="sxs-lookup"><span data-stu-id="9b5ed-134">Once the Azure CLI has been installed, the Batch extension can be installed using the following CLI command:</span></span>

```azurecli
az component update --add batch-extensions --allow-third-party
```

<span data-ttu-id="9b5ed-135">Pour plus d’informations sur l’extension Batch, consultez [Extensions Microsoft Azure Batch CLI pour Windows, Mac et Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span><span class="sxs-lookup"><span data-stu-id="9b5ed-135">For more information about the Batch extension, see [Microsoft Azure Batch CLI Extensions for Windows, Mac and Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).</span></span>

## <a name="templates"></a><span data-ttu-id="9b5ed-136">Modèles</span><span class="sxs-lookup"><span data-stu-id="9b5ed-136">Templates</span></span>

<span data-ttu-id="9b5ed-137">L’interface CLI Azure Batch autorise la création d’éléments tels que des pools, travaux et tâches en spécifiant un fichier JSON qui contient les valeurs et noms de propriétés.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-137">The Azure Batch CLI allows items such as pools, jobs, and tasks to be created by specifying a JSON file containing property names and values.</span></span> <span data-ttu-id="9b5ed-138">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="9b5ed-138">For example:</span></span>

```azurecli
az batch pool create –-json-file AppPool.json
```

<span data-ttu-id="9b5ed-139">Les modèles Azure Batch sont semblables aux modèles Azure Resource Manager en termes de syntaxe et de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-139">Azure Batch templates are similar to Azure Resource Manager templates, in functionality and syntax.</span></span> <span data-ttu-id="9b5ed-140">Il s’agit de fichiers JSON qui contiennent des valeurs et noms de propriétés, mais qui intègrent en plus les concepts principaux suivants :</span><span class="sxs-lookup"><span data-stu-id="9b5ed-140">They are JSON files that contain item property names and values, but add the following main concepts:</span></span>

-   <span data-ttu-id="9b5ed-141">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="9b5ed-141">**Parameters**</span></span>

    -   <span data-ttu-id="9b5ed-142">Ils autorisent la spécification des valeurs de propriété dans une section Corps, seules les valeurs de paramètre devant être fournies lorsque le modèle est utilisé.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-142">Allow property values to be specified in a body section, with only parameter values needing to be supplied when the template is used.</span></span> <span data-ttu-id="9b5ed-143">Par exemple, la définition complète d’un pool peut être placée dans le corps et un seul paramètre défini pour l’ID du pool. Par conséquent, seule la chaîne d’ID du pool doit être fournie pour créer un pool.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-143">For example, the complete definition for a pool could be placed in the body and only one parameter defined for pool id; only a pool id string therefore needs to be supplied to create a pool.</span></span>
        
    -   <span data-ttu-id="9b5ed-144">Le corps du modèle peut être créé par une personne connaissant Batch et les applications à exécuter dans celui-ci. Seules les valeurs des paramètres définis par l’auteur doivent être fournis lorsque le modèle est utilisé.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-144">The template body can be authored by someone with knowledge of Batch and the applications to be run by Batch; only values for the author-defined parameters must be supplied when the template is used.</span></span> <span data-ttu-id="9b5ed-145">Un utilisateur sans connaissance poussée de Batch ou des applications peut par conséquent utiliser les modèles.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-145">A user without the in-depth Batch and/or application knowledge can therefore use the templates.</span></span>

-   <span data-ttu-id="9b5ed-146">**Variables**</span><span class="sxs-lookup"><span data-stu-id="9b5ed-146">**Variables**</span></span>

    -   <span data-ttu-id="9b5ed-147">Ils autorisent la spécification de valeurs de paramètre simples ou complexes dans un seul emplacement et leur utilisation dans un ou plusieurs emplacements dans le corps du modèle.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-147">Allow simple or complex parameter values to be specified in one place and used in one or more places in the template body.</span></span> <span data-ttu-id="9b5ed-148">Des variables peuvent simplifier et réduire la taille du modèle, ainsi que faciliter sa gestion, en ayant un emplacement où modifier les propriétés dont la valeur peut changer.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-148">Variables can simplify and reduce the size of the template, as well as make it more maintainable by having one location to change properties whose value may change.</span></span>

-   <span data-ttu-id="9b5ed-149">**Constructions de niveau supérieur**</span><span class="sxs-lookup"><span data-stu-id="9b5ed-149">**Higher-level constructs**</span></span>

    -   <span data-ttu-id="9b5ed-150">Certaines constructions de niveau supérieur sont disponibles dans le modèle, mais ne sont pas encore disponibles dans les API Batch.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-150">Some higher-level constructs are available in the template that are not yet available in the Batch APIs.</span></span> <span data-ttu-id="9b5ed-151">Par exemple, une fabrique de tâches peut être définie dans un modèle de travail qui crée plusieurs tâches pour le travail à l’aide d’une définition de tâche commune.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-151">For example, a task factory can be defined in a job template that creates multiple tasks for the job using a common task definition.</span></span> <span data-ttu-id="9b5ed-152">Ces constructions évitent de devoir écrire du code pour créer dynamiquement plusieurs fichiers JSON, par exemple un fichier par tâche, ainsi que de créer des fichiers de script afin d’installer des applications via un gestionnaire de package par exemple.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-152">These constructs avoid the need to code to dynamically create multiple JSON files, such as one file per task, as well as create script files to install applications via a package manager, for example.</span></span>

    -   <span data-ttu-id="9b5ed-153">À un moment donné, le cas échéant, ces constructions pourront être ajoutées au service Batch et disponibles dans les interfaces utilisateur, API Batch, etc.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-153">At some point, where applicable, these constructs may be added to the Batch service and available in the Batch APIs, UIs, etc.</span></span>

### <a name="pool-templates"></a><span data-ttu-id="9b5ed-154">Modèles de pool</span><span class="sxs-lookup"><span data-stu-id="9b5ed-154">Pool templates</span></span>

<span data-ttu-id="9b5ed-155">Outre les fonctionnalités de modèle standard des paramètres et variables, les constructions de niveau supérieur suivantes sont prises en charge par le modèle de pool :</span><span class="sxs-lookup"><span data-stu-id="9b5ed-155">In addition to the standard template capabilities of parameters and variables, the following higher-level constructs are supported by the pool template:</span></span>

-   <span data-ttu-id="9b5ed-156">**Références de package**</span><span class="sxs-lookup"><span data-stu-id="9b5ed-156">**Package references**</span></span>

    -   <span data-ttu-id="9b5ed-157">Autorise éventuellement la copie du logiciel sur les nœuds du pool à l’aide de gestionnaires de packages.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-157">Optionally allows software to be copied to pool nodes by using package managers.</span></span> <span data-ttu-id="9b5ed-158">Le gestionnaire de package et l’ID du package sont spécifiés.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-158">The package manager and package id are specified.</span></span> <span data-ttu-id="9b5ed-159">Être en mesure de déclarer un ou plusieurs packages évite de devoir créer un script qui obtient les packages requis, d’installer le script et de l’exécuter sur chaque nœud du pool.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-159">Being able to declare one or more packages avoids the need to create a script that gets the required packages, install the script, and run the script on each pool node.</span></span>

<span data-ttu-id="9b5ed-160">Voici un exemple de modèle qui crée un pool de machines virtuelles Linux avec ffmpeg installé et qui nécessite seulement de spécifier une chaîne d’ID de pool et le nombre de machines virtuelles à fournir :</span><span class="sxs-lookup"><span data-stu-id="9b5ed-160">The following is an example of a template that creates a pool of Linux VMs with ffmpeg installed and only requires a pool id string and the number of VMs to be supplied to use:</span></span>

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "The number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "The pool id "
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

<span data-ttu-id="9b5ed-161">Si le fichier de modèle est nommé _pool-ffmpeg.json_, le modèle peut être appelé comme suit :</span><span class="sxs-lookup"><span data-stu-id="9b5ed-161">If the template file was named _pool-ffmpeg.json_, then the template would be invoked as follows:</span></span>

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a><span data-ttu-id="9b5ed-162">Modèles de travail</span><span class="sxs-lookup"><span data-stu-id="9b5ed-162">Job templates</span></span>

<span data-ttu-id="9b5ed-163">Outre les fonctionnalités de modèle standard des paramètres et variables, les constructions de niveau supérieur suivantes sont prises en charge par le modèle de travail :</span><span class="sxs-lookup"><span data-stu-id="9b5ed-163">In addition to the standard template capabilities of parameters and variables, the following higher-level constructs are supported by the job template:</span></span>

-   <span data-ttu-id="9b5ed-164">**Fabrique de tâches**</span><span class="sxs-lookup"><span data-stu-id="9b5ed-164">**Task factory**</span></span>

    -   <span data-ttu-id="9b5ed-165">Crée plusieurs tâches pour un travail à partir d’une définition de tâche.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-165">Creates multiple tasks for a job from one task definition.</span></span> <span data-ttu-id="9b5ed-166">Trois types de fabrique de tâches sont pris en charge : balayage paramétrique, tâche par fichier et collection de tâches.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-166">Three types of task factory are supported – parametric sweep, task per file, and task collection.</span></span>

<span data-ttu-id="9b5ed-167">Voici un exemple de modèle qui crée un travail qui utilise ffmpeg pour transcoder des fichiers vidéo MP4 dans une des deux résolutions inférieures, avec une tâche créée par fichier vidéo source :</span><span class="sxs-lookup"><span data-stu-id="9b5ed-167">The following is an example of a template that creates a job that uses ffmpeg to transcode MP4 video files to one of two lower resolutions, with one task created per source video file:</span></span>

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "The name of Azure Batch pool which runs the job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "The name of Azure Batch job"
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

<span data-ttu-id="9b5ed-168">Si le fichier de modèle est nommé _job-ffmpeg.json_, le modèle peut être appelé comme suit :</span><span class="sxs-lookup"><span data-stu-id="9b5ed-168">If the template file was named _job-ffmpeg.json_, then the template would be invoked as follows:</span></span>

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a><span data-ttu-id="9b5ed-169">Groupes de fichiers et transfert de fichiers</span><span class="sxs-lookup"><span data-stu-id="9b5ed-169">File groups and file transfer</span></span>

<span data-ttu-id="9b5ed-170">La plupart des travaux et des tâches requièrent les fichiers d’entrée et produisent des fichiers de sortie.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-170">Most jobs and tasks require input files and produce output files.</span></span> <span data-ttu-id="9b5ed-171">Les fichiers d’entrée et de sortie doivent généralement être transférés, soit du client vers le nœud, soit du nœud vers le client.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-171">Both input files and output files typically need to be transferred, either from the client to the node, or from the node to the client.</span></span> <span data-ttu-id="9b5ed-172">L’extension CLI d’Azure Batch met de côté le transfert de fichiers et utilise le compte de stockage créé par défaut pour chaque compte Batch.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-172">The Azure Batch CLI extension abstracts away file transfer and utilizes the storage account that is created by default for each Batch account.</span></span>

<span data-ttu-id="9b5ed-173">Un groupe de fichiers correspond à un conteneur créé dans le compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-173">A file group equates to a container that is created in the Azure storage account.</span></span> <span data-ttu-id="9b5ed-174">Le groupe de fichiers peut contenir des sous-dossiers.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-174">The file group may have subfolders.</span></span>

<span data-ttu-id="9b5ed-175">L’extension Batch CLI fourni des commandes permettant de charger des fichiers du client vers un groupe de fichiers spécifié et de télécharger les fichiers du groupe de fichiers spécifié vers le client.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-175">The Batch CLI extension provides commands for uploading files from client to a specified file group and downloading files from the specified file group to a client.</span></span>

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

<span data-ttu-id="9b5ed-176">Les modèles de pool et de travail permettent de spécifier les fichiers stockés dans des groupes de fichiers pour la copie sur les nœuds de pool ou le renvoi des nœuds de pool vers un groupe de fichiers.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-176">Pool and job templates allow files stored in file groups to be specified for copy onto pool nodes or off pool nodes back to a file group.</span></span> <span data-ttu-id="9b5ed-177">Par exemple, dans le modèle de travail spécifié précédemment, le groupe de fichiers « ffmpeg-input » est spécifié pour la fabrique de tâches en tant qu’emplacement des fichiers vidéo sources copiés sur le nœud pour le transcodage ; le groupe de fichiers « ffmpeg-output » est utilisé en tant qu’emplacement où les fichiers de sortie transcodés sont copiés à partir du nœud exécutant chaque tâche.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-177">For example, in the job template specified previously, the file group “ffmpeg-input” is specified for the task factory as the location of the source video files copied down onto the node for transcoding; the file group “ffmpeg-output” is used as the location where the transcoded output files are copied to from the node running each task.</span></span>

## <a name="summary"></a><span data-ttu-id="9b5ed-178">Résumé</span><span class="sxs-lookup"><span data-stu-id="9b5ed-178">Summary</span></span>

<span data-ttu-id="9b5ed-179">La prise en charge du transfert de fichiers et des modèles a seulement été ajoutée à l’interface Azure CLI pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-179">Template and file transfer support have currently been added only to the Azure CLI.</span></span> <span data-ttu-id="9b5ed-180">L’objectif est d’étendre le public pouvant utiliser Batch aux utilisateurs qui n’ont pas besoin de développer du code à l’aide des API Batch, tels que les chercheurs, les utilisateurs, etc.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-180">The goal is to expand the audience that can use Batch to users who do not need to develop code using the Batch APIs, such as researchers, IT users, and so on.</span></span> <span data-ttu-id="9b5ed-181">Sans effectuer de codage, les utilisateurs qui connaissent bien Azure, Batch et les applications peuvent créer des modèles pour la création de pools et de travaux.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-181">Without coding, users with knowledge of Azure, Batch, and the applications to be run by Batch can create templates for pool and job creation.</span></span> <span data-ttu-id="9b5ed-182">Avec les paramètres de modèle, les utilisateurs sans connaissance approfondie de Batch et des applications d’utiliser les modèles.</span><span class="sxs-lookup"><span data-stu-id="9b5ed-182">With template parameters, users without detailed knowledge of Batch and the applications can use the templates.</span></span>

<span data-ttu-id="9b5ed-183">Testez l’extension Batch pour l’interface de ligne de commande Azure et faites-nous part de vos commentaires et de vos suggestions dans les commentaires de cet article ou via le [forum Azure Batch](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span><span class="sxs-lookup"><span data-stu-id="9b5ed-183">Try out the Batch extension for the Azure CLI and provide us with any feedback or suggestions, either in the comments for this article or via the [Azure Batch forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b5ed-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9b5ed-184">Next steps</span></span>

- <span data-ttu-id="9b5ed-185">Consultez l’article du blog au sujet des modèles de lot : [Exécution des travaux Azure Batch à l’aide de l’interface de ligne de commande Azure - aucun code requis](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span><span class="sxs-lookup"><span data-stu-id="9b5ed-185">See the Batch templates blog post: [Running Azure Batch jobs using the Azure CLI – no code required](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).</span></span>
- <span data-ttu-id="9b5ed-186">Une documentation détaillée sur l’installation et l’utilisation, des exemples et du code source sont disponibles dans le [dépôt GitHub Azure](https://github.com/Azure/azure-batch-cli-extensions).</span><span class="sxs-lookup"><span data-stu-id="9b5ed-186">Detailed installation and usage documentation, samples, and source code are available in the [Azure GitHub repository](https://github.com/Azure/azure-batch-cli-extensions).</span></span>
