---
title: "Exemple de script Azure CLI : exécution d’un travail avec Batch | Microsoft Docs"
description: "Exemple de script Azure CLI : exécution d’un travail avec Batch"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 5fe1e3595d9459e60b2fd54d6f17f6822731f453
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a><span data-ttu-id="ef10b-103">Exécution de travaux sur Azure Batch avec l’interface Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ef10b-103">Running jobs on Azure Batch with Azure CLI</span></span>

<span data-ttu-id="ef10b-104">Ce script crée une tâche Batch et ajoute une série de tâches au travail.</span><span class="sxs-lookup"><span data-stu-id="ef10b-104">This script creates a Batch job and adds a series of tasks to the job.</span></span> <span data-ttu-id="ef10b-105">Il explique également comment surveiller un travail et ses tâches.</span><span class="sxs-lookup"><span data-stu-id="ef10b-105">It also demonstrates how to monitor a job and its tasks.</span></span> <span data-ttu-id="ef10b-106">Enfin, il montre comment interroger le service Batch efficacement pour obtenir des informations sur les tâches du travail.</span><span class="sxs-lookup"><span data-stu-id="ef10b-106">Finally, it shows how to query the Batch service efficiently for information about the job's tasks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef10b-107">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="ef10b-107">Prerequisites</span></span>

- <span data-ttu-id="ef10b-108">Installez Azure CLI en suivant les instructions fournies dans le [Guide d’installation d’Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), si ce n’est déjà fait.</span><span class="sxs-lookup"><span data-stu-id="ef10b-108">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="ef10b-109">Créez un compte Azure si vous n’en avez pas.</span><span class="sxs-lookup"><span data-stu-id="ef10b-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="ef10b-110">Pour un exemple de script qui crée un compte, voir [Créer un compte Batch avec Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account).</span><span class="sxs-lookup"><span data-stu-id="ef10b-110">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="ef10b-111">Configurez une application à s’exécuter à partir d’une tâche de démarrage si vous ne l’avez pas encore fait.</span><span class="sxs-lookup"><span data-stu-id="ef10b-111">Configure an application to run from a start task if you haven't yet done so.</span></span> <span data-ttu-id="ef10b-112">Pour un exemple de script qui crée une application et charge un package d’application dans Azure, voir [Ajout d’applications dans Azure Batch avec Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application).</span><span class="sxs-lookup"><span data-stu-id="ef10b-112">See [Adding applications to Azure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package to Azure.</span></span>
- <span data-ttu-id="ef10b-113">Configurer un pool sur lequel le travail sera exécuté.</span><span class="sxs-lookup"><span data-stu-id="ef10b-113">Configure a pool on which the job will run.</span></span> <span data-ttu-id="ef10b-114">Pour un exemple de script qui crée un pool avec une configuration de service cloud ou une configuration de machine virtuelle, voir [Gérer des pools Azure Batch avec CLI Azure](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool).</span><span class="sxs-lookup"><span data-stu-id="ef10b-114">See [Managing Azure Batch pools with Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) for a sample script that creates a pool with either a Cloud Service Configuration or a Virtual Machine Configuration.</span></span>

## <a name="sample-script"></a><span data-ttu-id="ef10b-115">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="ef10b-115">Sample script</span></span>

<span data-ttu-id="ef10b-116">[!code-azurecli[principal](../../../cli_scripts/batch/run-job/run-job.sh "Exécuter un travail")]</span><span class="sxs-lookup"><span data-stu-id="ef10b-116">[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]</span></span>

## <a name="clean-up-job"></a><span data-ttu-id="ef10b-117">Travail de nettoyage</span><span class="sxs-lookup"><span data-stu-id="ef10b-117">Clean up job</span></span>

<span data-ttu-id="ef10b-118">Après avoir exécuté l’exemple de script ci-dessus, lancez la commande suivante pour supprimer le travail et toutes les tâches associées.</span><span class="sxs-lookup"><span data-stu-id="ef10b-118">After you run the above sample script, run the following command to remove the job and all of its tasks.</span></span> <span data-ttu-id="ef10b-119">Notez que le pool doit être supprimé séparément.</span><span class="sxs-lookup"><span data-stu-id="ef10b-119">Note that the pool will need to be deleted separately.</span></span> <span data-ttu-id="ef10b-120">Pour plus d’informations sur la création et la suppression de pools, voir [Gérer des pools Azure Batch avec CLI Azure](./batch-cli-sample-manage-pool.md).</span><span class="sxs-lookup"><span data-stu-id="ef10b-120">See [Managing Azure Batch pools with Azure CLI](./batch-cli-sample-manage-pool.md) for more information on creating and deleting pools.</span></span>

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a><span data-ttu-id="ef10b-121">Explication du script</span><span class="sxs-lookup"><span data-stu-id="ef10b-121">Script explanation</span></span>

<span data-ttu-id="ef10b-122">Ce script a recours aux commandes suivantes pour créer un travail et des tâches Batch.</span><span class="sxs-lookup"><span data-stu-id="ef10b-122">This script uses the following commands to create a Batch job and tasks.</span></span> <span data-ttu-id="ef10b-123">Chaque commande de la table renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="ef10b-123">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="ef10b-124">Commande</span><span class="sxs-lookup"><span data-stu-id="ef10b-124">Command</span></span> | <span data-ttu-id="ef10b-125">Remarques</span><span class="sxs-lookup"><span data-stu-id="ef10b-125">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ef10b-126">az batch account login</span><span class="sxs-lookup"><span data-stu-id="ef10b-126">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="ef10b-127">Permet de s’authentifier avec un compte Batch.</span><span class="sxs-lookup"><span data-stu-id="ef10b-127">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="ef10b-128">az batch job create</span><span class="sxs-lookup"><span data-stu-id="ef10b-128">az batch job create</span></span>](https://docs.microsoft.com/cli/azure/batch/job#create) | <span data-ttu-id="ef10b-129">Crée un travail Batch.</span><span class="sxs-lookup"><span data-stu-id="ef10b-129">Creates a Batch job.</span></span>  |
| [<span data-ttu-id="ef10b-130">az batch job set</span><span class="sxs-lookup"><span data-stu-id="ef10b-130">az batch job set</span></span>](https://docs.microsoft.com/cli/azure/batch/job#set) | <span data-ttu-id="ef10b-131">Met à jour les propriétés d’un travail Batch.</span><span class="sxs-lookup"><span data-stu-id="ef10b-131">Updates properties of a Batch job.</span></span>  |
| [<span data-ttu-id="ef10b-132">az batch job show</span><span class="sxs-lookup"><span data-stu-id="ef10b-132">az batch job show</span></span>](https://docs.microsoft.com/cli/azure/batch/job#show) | <span data-ttu-id="ef10b-133">Récupère les détails relatifs au travail Batch spécifié.</span><span class="sxs-lookup"><span data-stu-id="ef10b-133">Retrieves details of a specified Batch job.</span></span>  |
| [<span data-ttu-id="ef10b-134">az batch task create</span><span class="sxs-lookup"><span data-stu-id="ef10b-134">az batch task create</span></span>](https://docs.microsoft.com/cli/azure/batch/task#create) | <span data-ttu-id="ef10b-135">Ajoute une tâche au travail Batch spécifié.</span><span class="sxs-lookup"><span data-stu-id="ef10b-135">Adds a task to the specified Batch job.</span></span>  |
| [<span data-ttu-id="ef10b-136">az batch task show</span><span class="sxs-lookup"><span data-stu-id="ef10b-136">az batch task show</span></span>](https://docs.microsoft.com/cli/azure/batch/task#show) | <span data-ttu-id="ef10b-137">Récupère les détails relatifs à une tâche du travail Batch spécifié.</span><span class="sxs-lookup"><span data-stu-id="ef10b-137">Retrieves the details of a task from the specified Batch job.</span></span>  |
| [<span data-ttu-id="ef10b-138">az batch task list</span><span class="sxs-lookup"><span data-stu-id="ef10b-138">az batch task list</span></span>](https://docs.microsoft.com/cli/azure/batch/task#list) | <span data-ttu-id="ef10b-139">Répertorie les tâches associées au travail spécifié.</span><span class="sxs-lookup"><span data-stu-id="ef10b-139">Lists the tasks associated with the specified job.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="ef10b-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ef10b-140">Next steps</span></span>

<span data-ttu-id="ef10b-141">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ef10b-141">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ef10b-142">Vous trouverez des exemples supplémentaires de scripts CLI Batch dans la [documentation relative à la CLI Azure Batch](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ef10b-142">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
