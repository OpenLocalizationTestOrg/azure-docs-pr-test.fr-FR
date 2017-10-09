---
title: aaaAzure exemple de Script CLI - gestion de Pools dans le traitement par lots | Documents Microsoft
description: Exemple de script CLI Azure - Gestion de pools dans Batch
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
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="b8484-103">Gérer des pools Azure Batch avec l’interface CLI Azure</span><span class="sxs-lookup"><span data-stu-id="b8484-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="b8484-104">Ces script présente quelques-unes des outils de hello disponibles dans hello CLI d’Azure toocreate et gérer les pools de nœuds de calcul dans le service de traitement par lots Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b8484-104">These script demonstrates some of hello tools available in hello Azure CLI toocreate and manage pools of compute nodes in hello Azure Batch service.</span></span>

> [!NOTE]
> <span data-ttu-id="b8484-105">commandes de Hello dans cet exemple créent des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="b8484-105">hello commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="b8484-106">Machines virtuelles s’exécutant provisionner le compte de frais tooyour.</span><span class="sxs-lookup"><span data-stu-id="b8484-106">Running VMs will accrue charges tooyour account.</span></span> <span data-ttu-id="b8484-107">toominimize ces frais et supprimer des machines virtuelles de hello une fois que vous avez terminé les exemple hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="b8484-107">toominimize these charges, delete hello VMs once you're done running hello sample.</span></span> <span data-ttu-id="b8484-108">Consultez la page [Nettoyer les pools](#clean-up-pools).</span><span class="sxs-lookup"><span data-stu-id="b8484-108">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="b8484-109">Les pools Batch peuvent être configurés de deux manières, soit via une configuration de Services cloud (Windows uniquement), soit via une configuration de machine virtuelle (Windows et Linux).</span><span class="sxs-lookup"><span data-stu-id="b8484-109">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span> <span data-ttu-id="b8484-110">Hello exemples de scripts ci-dessous montrent comment toocreate regroupe avec les deux configurations.</span><span class="sxs-lookup"><span data-stu-id="b8484-110">hello sample scripts below show how toocreate pools with both configurations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8484-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b8484-111">Prerequisites</span></span>

- <span data-ttu-id="b8484-112">Installation hello CLI d’Azure à l’aide d’instructions hello de hello [guide d’installation Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), si vous n’avez pas déjà fait.</span><span class="sxs-lookup"><span data-stu-id="b8484-112">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="b8484-113">Créez un compte Azure si vous n’en avez pas.</span><span class="sxs-lookup"><span data-stu-id="b8484-113">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="b8484-114">Consultez [créer un compte de traitement par lots avec hello CLI d’Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) pour un exemple de script qui crée un compte.</span><span class="sxs-lookup"><span data-stu-id="b8484-114">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="b8484-115">Configurer un toorun d’application à partir d’une tâche de démarrage si vous n’avez pas encore fait.</span><span class="sxs-lookup"><span data-stu-id="b8484-115">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="b8484-116">Consultez [Ajout d’applications tooAzure lot avec Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) pour un exemple de script qui crée une application et télécharge un tooAzure de package d’application.</span><span class="sxs-lookup"><span data-stu-id="b8484-116">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="b8484-117">Pool avec exemple de script pour la configuration du service cloud</span><span class="sxs-lookup"><span data-stu-id="b8484-117">Pool with cloud service configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="b8484-118">Pool avec exemple de script pour la configuration de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="b8484-118">Pool with virtual machine configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a><span data-ttu-id="b8484-119">Nettoyer les pools</span><span class="sxs-lookup"><span data-stu-id="b8484-119">Clean up pools</span></span>

<span data-ttu-id="b8484-120">Après avoir exécuté hello ci-dessus un exemple de script, exécutez hello suivant des pools de commande toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="b8484-120">After you run hello above sample script, run hello following command toodelete hello pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="b8484-121">Explication du script</span><span class="sxs-lookup"><span data-stu-id="b8484-121">Script explanation</span></span>

<span data-ttu-id="b8484-122">Ce script utilise hello suivant toocreate de commandes et de manipuler les pools de lot.</span><span class="sxs-lookup"><span data-stu-id="b8484-122">This script uses hello following commands toocreate and manipulate Batch pools.</span></span>
<span data-ttu-id="b8484-123">Chaque commande dans la table de hello lie documentation toocommand spécifique.</span><span class="sxs-lookup"><span data-stu-id="b8484-123">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="b8484-124">Commande</span><span class="sxs-lookup"><span data-stu-id="b8484-124">Command</span></span> | <span data-ttu-id="b8484-125">Remarques</span><span class="sxs-lookup"><span data-stu-id="b8484-125">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b8484-126">az batch account login</span><span class="sxs-lookup"><span data-stu-id="b8484-126">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="b8484-127">Permet de s’authentifier avec un compte Batch.</span><span class="sxs-lookup"><span data-stu-id="b8484-127">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="b8484-128">az batch application summary list</span><span class="sxs-lookup"><span data-stu-id="b8484-128">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="b8484-129">Répertorier les applications disponibles de hello Bonjour compte Batch.</span><span class="sxs-lookup"><span data-stu-id="b8484-129">List hello available applications in hello Batch account.</span></span>  |
| [<span data-ttu-id="b8484-130">az batch pool create</span><span class="sxs-lookup"><span data-stu-id="b8484-130">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="b8484-131">Permet de créer un pool de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="b8484-131">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="b8484-132">az batch pool set</span><span class="sxs-lookup"><span data-stu-id="b8484-132">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="b8484-133">Permet de mettre à jour les propriétés d’un pool.</span><span class="sxs-lookup"><span data-stu-id="b8484-133">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="b8484-134">az batch pool node-agent-skus list</span><span class="sxs-lookup"><span data-stu-id="b8484-134">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="b8484-135">Permet de répertorier les SKU de l’agent de nœud et les informations de l’image.</span><span class="sxs-lookup"><span data-stu-id="b8484-135">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="b8484-136">az batch pool resize</span><span class="sxs-lookup"><span data-stu-id="b8484-136">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="b8484-137">Nombre de hello de redimensionnement de machines virtuelles s’exécutant dans hello spécifié de pool.</span><span class="sxs-lookup"><span data-stu-id="b8484-137">Resize hello number of running VMs in hello specified pool.</span></span>  |
| [<span data-ttu-id="b8484-138">az batch pool show</span><span class="sxs-lookup"><span data-stu-id="b8484-138">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="b8484-139">Afficher les propriétés de hello d’un pool.</span><span class="sxs-lookup"><span data-stu-id="b8484-139">Display hello properties of a pool.</span></span>  |
| [<span data-ttu-id="b8484-140">az batch pool delete</span><span class="sxs-lookup"><span data-stu-id="b8484-140">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="b8484-141">Supprimer hello spécifié pool.</span><span class="sxs-lookup"><span data-stu-id="b8484-141">Delete hello specified pool.</span></span>  |
| [<span data-ttu-id="b8484-142">az batch pool autoscale enable</span><span class="sxs-lookup"><span data-stu-id="b8484-142">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="b8484-143">Permet d’activer la mise à l’échelle automatique sur un pool et d’appliquer une formule.</span><span class="sxs-lookup"><span data-stu-id="b8484-143">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="b8484-144">az batch pool autoscale disable</span><span class="sxs-lookup"><span data-stu-id="b8484-144">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="b8484-145">Permet de désactiver la mise à l’échelle automatique sur un pool.</span><span class="sxs-lookup"><span data-stu-id="b8484-145">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="b8484-146">az batch node list</span><span class="sxs-lookup"><span data-stu-id="b8484-146">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="b8484-147">Liste de tous les de nœud de calcul hello Bonjour spécifié de pool.</span><span class="sxs-lookup"><span data-stu-id="b8484-147">List all hello compute node in hello specified pool.</span></span>  |
| [<span data-ttu-id="b8484-148">az batch node reboot</span><span class="sxs-lookup"><span data-stu-id="b8484-148">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="b8484-149">Redémarrer le nœud de calcul spécifié hello.</span><span class="sxs-lookup"><span data-stu-id="b8484-149">Reboot hello specified compute node.</span></span>  |
| [<span data-ttu-id="b8484-150">az batch node delete</span><span class="sxs-lookup"><span data-stu-id="b8484-150">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="b8484-151">Supprimer des nœuds de hello répertorié de hello spécifié pool.</span><span class="sxs-lookup"><span data-stu-id="b8484-151">Delete hello listed nodes from hello specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="b8484-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b8484-152">Next steps</span></span>

<span data-ttu-id="b8484-153">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b8484-153">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b8484-154">Vous trouverez des exemples supplémentaires de script CLI de lot Bonjour [documentation d’Azure Batch CLI](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b8484-154">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

