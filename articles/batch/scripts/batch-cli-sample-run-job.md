---
title: "aaaAzure exemple de Script CLI - exécutez un travail de traitement par lots | Documents Microsoft"
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
ms.openlocfilehash: f73a7cb341e550fd1c92f92201e20b27fa20d238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a><span data-ttu-id="e2975-103">Exécution de travaux sur Azure Batch avec l’interface Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e2975-103">Running jobs on Azure Batch with Azure CLI</span></span>

<span data-ttu-id="e2975-104">Ce script crée une tâche de traitement par lots et ajoute une série de travail toohello de tâches.</span><span class="sxs-lookup"><span data-stu-id="e2975-104">This script creates a Batch job and adds a series of tasks toohello job.</span></span> <span data-ttu-id="e2975-105">Il montre également comment toomonitor une tâche et ses tâches.</span><span class="sxs-lookup"><span data-stu-id="e2975-105">It also demonstrates how toomonitor a job and its tasks.</span></span> <span data-ttu-id="e2975-106">Enfin, il montre comment tooquery hello service Batch efficacement pour plus d’informations sur les tâches du travail hello.</span><span class="sxs-lookup"><span data-stu-id="e2975-106">Finally, it shows how tooquery hello Batch service efficiently for information about hello job's tasks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2975-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e2975-107">Prerequisites</span></span>

- <span data-ttu-id="e2975-108">Installation hello CLI d’Azure à l’aide d’instructions hello de hello [guide d’installation Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), si vous n’avez pas déjà fait.</span><span class="sxs-lookup"><span data-stu-id="e2975-108">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="e2975-109">Créez un compte Azure si vous n’en avez pas.</span><span class="sxs-lookup"><span data-stu-id="e2975-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="e2975-110">Consultez [créer un compte de traitement par lots avec hello CLI d’Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) pour un exemple de script qui crée un compte.</span><span class="sxs-lookup"><span data-stu-id="e2975-110">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="e2975-111">Configurer un toorun d’application à partir d’une tâche de démarrage si vous n’avez pas encore fait.</span><span class="sxs-lookup"><span data-stu-id="e2975-111">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="e2975-112">Consultez [Ajout d’applications tooAzure lot avec Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) pour un exemple de script qui crée une application et télécharge un tooAzure de package d’application.</span><span class="sxs-lookup"><span data-stu-id="e2975-112">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>
- <span data-ttu-id="e2975-113">Configurer un pool d’exécution de la tâche sur le hello.</span><span class="sxs-lookup"><span data-stu-id="e2975-113">Configure a pool on which hello job will run.</span></span> <span data-ttu-id="e2975-114">Pour un exemple de script qui crée un pool avec une configuration de service cloud ou une configuration de machine virtuelle, voir [Gérer des pools Azure Batch avec CLI Azure](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool).</span><span class="sxs-lookup"><span data-stu-id="e2975-114">See [Managing Azure Batch pools with Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) for a sample script that creates a pool with either a Cloud Service Configuration or a Virtual Machine Configuration.</span></span>

## <a name="sample-script"></a><span data-ttu-id="e2975-115">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="e2975-115">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a><span data-ttu-id="e2975-116">Travail de nettoyage</span><span class="sxs-lookup"><span data-stu-id="e2975-116">Clean up job</span></span>

<span data-ttu-id="e2975-117">Après avoir exécuté hello ci-dessus un exemple de script, exécutez hello suivant commande tooremove le travail et toutes ses tâches.</span><span class="sxs-lookup"><span data-stu-id="e2975-117">After you run hello above sample script, run hello following command tooremove the job and all of its tasks.</span></span> <span data-ttu-id="e2975-118">Notez que le pool de hello devez toobe supprimée séparément.</span><span class="sxs-lookup"><span data-stu-id="e2975-118">Note that hello pool will need toobe deleted separately.</span></span> <span data-ttu-id="e2975-119">Pour plus d’informations sur la création et la suppression de pools, voir [Gérer des pools Azure Batch avec CLI Azure](./batch-cli-sample-manage-pool.md).</span><span class="sxs-lookup"><span data-stu-id="e2975-119">See [Managing Azure Batch pools with Azure CLI](./batch-cli-sample-manage-pool.md) for more information on creating and deleting pools.</span></span>

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a><span data-ttu-id="e2975-120">Explication du script</span><span class="sxs-lookup"><span data-stu-id="e2975-120">Script explanation</span></span>

<span data-ttu-id="e2975-121">Ce script utilise hello suivant de commandes toocreate un traitement par lots et les tâches.</span><span class="sxs-lookup"><span data-stu-id="e2975-121">This script uses hello following commands toocreate a Batch job and tasks.</span></span> <span data-ttu-id="e2975-122">Chaque commande dans la table de hello lie documentation toocommand spécifique.</span><span class="sxs-lookup"><span data-stu-id="e2975-122">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="e2975-123">Commande</span><span class="sxs-lookup"><span data-stu-id="e2975-123">Command</span></span> | <span data-ttu-id="e2975-124">Remarques</span><span class="sxs-lookup"><span data-stu-id="e2975-124">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e2975-125">az batch account login</span><span class="sxs-lookup"><span data-stu-id="e2975-125">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="e2975-126">Permet de s’authentifier avec un compte Batch.</span><span class="sxs-lookup"><span data-stu-id="e2975-126">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="e2975-127">az batch job create</span><span class="sxs-lookup"><span data-stu-id="e2975-127">az batch job create</span></span>](https://docs.microsoft.com/cli/azure/batch/job#create) | <span data-ttu-id="e2975-128">Crée un travail Batch.</span><span class="sxs-lookup"><span data-stu-id="e2975-128">Creates a Batch job.</span></span>  |
| [<span data-ttu-id="e2975-129">az batch job set</span><span class="sxs-lookup"><span data-stu-id="e2975-129">az batch job set</span></span>](https://docs.microsoft.com/cli/azure/batch/job#set) | <span data-ttu-id="e2975-130">Met à jour les propriétés d’un travail Batch.</span><span class="sxs-lookup"><span data-stu-id="e2975-130">Updates properties of a Batch job.</span></span>  |
| [<span data-ttu-id="e2975-131">az batch job show</span><span class="sxs-lookup"><span data-stu-id="e2975-131">az batch job show</span></span>](https://docs.microsoft.com/cli/azure/batch/job#show) | <span data-ttu-id="e2975-132">Récupère les détails relatifs au travail Batch spécifié.</span><span class="sxs-lookup"><span data-stu-id="e2975-132">Retrieves details of a specified Batch job.</span></span>  |
| [<span data-ttu-id="e2975-133">az batch task create</span><span class="sxs-lookup"><span data-stu-id="e2975-133">az batch task create</span></span>](https://docs.microsoft.com/cli/azure/batch/task#create) | <span data-ttu-id="e2975-134">Ajoute qu'un toohello de la tâche spécifiée par lots.</span><span class="sxs-lookup"><span data-stu-id="e2975-134">Adds a task toohello specified Batch job.</span></span>  |
| [<span data-ttu-id="e2975-135">az batch task show</span><span class="sxs-lookup"><span data-stu-id="e2975-135">az batch task show</span></span>](https://docs.microsoft.com/cli/azure/batch/task#show) | <span data-ttu-id="e2975-136">Récupère les détails de hello d’une tâche à partir de hello spécifié par lots.</span><span class="sxs-lookup"><span data-stu-id="e2975-136">Retrieves hello details of a task from hello specified Batch job.</span></span>  |
| [<span data-ttu-id="e2975-137">az batch task list</span><span class="sxs-lookup"><span data-stu-id="e2975-137">az batch task list</span></span>](https://docs.microsoft.com/cli/azure/batch/task#list) | <span data-ttu-id="e2975-138">Répertorie les tâches hello associés au travail spécifié de hello.</span><span class="sxs-lookup"><span data-stu-id="e2975-138">Lists hello tasks associated with hello specified job.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="e2975-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e2975-139">Next steps</span></span>

<span data-ttu-id="e2975-140">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e2975-140">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e2975-141">Vous trouverez des exemples supplémentaires de script CLI de lot Bonjour [documentation d’Azure Batch CLI](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e2975-141">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
