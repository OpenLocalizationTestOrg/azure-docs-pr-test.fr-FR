---
title: Exemple de script CLI Azure - Gestion de pools dans Batch | Microsoft Docs
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
ms.openlocfilehash: 2556b02459886390b803407c5cb828687229a44e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="981ca-103">Gérer des pools Azure Batch avec l’interface CLI Azure</span><span class="sxs-lookup"><span data-stu-id="981ca-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="981ca-104">Ces scripts montrent certains des outils disponibles dans l’interface CLI Azure pour créer et gérer des pools de nœuds de calcul dans le service Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="981ca-104">These script demonstrates some of the tools available in the Azure CLI to create and manage pools of compute nodes in the Azure Batch service.</span></span>

> [!NOTE]
> <span data-ttu-id="981ca-105">Dans cet exemple, les commandes créent des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="981ca-105">The commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="981ca-106">L’exécution de machines virtuelles engendre des frais sur votre compte.</span><span class="sxs-lookup"><span data-stu-id="981ca-106">Running VMs will accrue charges to your account.</span></span> <span data-ttu-id="981ca-107">Pour réduire ces frais, supprimez les machines virtuelles lorsque vous avez terminé l’exécution de cet exemple.</span><span class="sxs-lookup"><span data-stu-id="981ca-107">To minimize these charges, delete the VMs once you're done running the sample.</span></span> <span data-ttu-id="981ca-108">Consultez la page [Nettoyer les pools](#clean-up-pools).</span><span class="sxs-lookup"><span data-stu-id="981ca-108">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="981ca-109">Les pools Batch peuvent être configurés de deux manières, soit via une configuration de Services cloud (Windows uniquement), soit via une configuration de machine virtuelle (Windows et Linux).</span><span class="sxs-lookup"><span data-stu-id="981ca-109">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span> <span data-ttu-id="981ca-110">Les exemples de scripts ci-dessous montrent comment créer des pools avec les deux configurations.</span><span class="sxs-lookup"><span data-stu-id="981ca-110">The sample scripts below show how to create pools with both configurations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="981ca-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="981ca-111">Prerequisites</span></span>

- <span data-ttu-id="981ca-112">Installez Azure CLI en suivant les instructions fournies dans le [Guide d’installation d’Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli), si ce n’est déjà fait.</span><span class="sxs-lookup"><span data-stu-id="981ca-112">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="981ca-113">Créez un compte Azure si vous n’en avez pas.</span><span class="sxs-lookup"><span data-stu-id="981ca-113">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="981ca-114">Pour un exemple de script qui crée un compte, voir [Créer un compte Batch avec Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account).</span><span class="sxs-lookup"><span data-stu-id="981ca-114">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="981ca-115">Configurez une application à s’exécuter à partir d’une tâche de démarrage si vous ne l’avez pas encore fait.</span><span class="sxs-lookup"><span data-stu-id="981ca-115">Configure an application to run from a start task if you haven't yet done so.</span></span> <span data-ttu-id="981ca-116">Pour un exemple de script qui crée une application et charge un package d’application dans Azure, voir [Ajout d’applications dans Azure Batch avec Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application).</span><span class="sxs-lookup"><span data-stu-id="981ca-116">See [Adding applications to Azure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package to Azure.</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="981ca-117">Pool avec exemple de script pour la configuration du service cloud</span><span class="sxs-lookup"><span data-stu-id="981ca-117">Pool with cloud service configuration sample script</span></span>

<span data-ttu-id="981ca-118">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Gérer les pools de services cloud")]</span><span class="sxs-lookup"><span data-stu-id="981ca-118">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]</span></span>

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="981ca-119">Pool avec exemple de script pour la configuration de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="981ca-119">Pool with virtual machine configuration sample script</span></span>

<span data-ttu-id="981ca-120">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Gérer les pools de machines virtuelles")]</span><span class="sxs-lookup"><span data-stu-id="981ca-120">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]</span></span>

## <a name="clean-up-pools"></a><span data-ttu-id="981ca-121">Nettoyer les pools</span><span class="sxs-lookup"><span data-stu-id="981ca-121">Clean up pools</span></span>

<span data-ttu-id="981ca-122">Après avoir exécuté l’exemple de script ci-dessus, exécutez la commande suivante pour supprimer les pools.</span><span class="sxs-lookup"><span data-stu-id="981ca-122">After you run the above sample script, run the following command to delete the pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="981ca-123">Explication du script</span><span class="sxs-lookup"><span data-stu-id="981ca-123">Script explanation</span></span>

<span data-ttu-id="981ca-124">Ce script utilise les commandes suivantes pour créer et manipuler des pools Batch.</span><span class="sxs-lookup"><span data-stu-id="981ca-124">This script uses the following commands to create and manipulate Batch pools.</span></span>
<span data-ttu-id="981ca-125">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="981ca-125">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="981ca-126">Commande</span><span class="sxs-lookup"><span data-stu-id="981ca-126">Command</span></span> | <span data-ttu-id="981ca-127">Remarques</span><span class="sxs-lookup"><span data-stu-id="981ca-127">Notes</span></span> |
|---|---|
| [<span data-ttu-id="981ca-128">az batch account login</span><span class="sxs-lookup"><span data-stu-id="981ca-128">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="981ca-129">Permet de s’authentifier avec un compte Batch.</span><span class="sxs-lookup"><span data-stu-id="981ca-129">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="981ca-130">az batch application summary list</span><span class="sxs-lookup"><span data-stu-id="981ca-130">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="981ca-131">Permet de répertorier les applications disponibles dans le compte Batch.</span><span class="sxs-lookup"><span data-stu-id="981ca-131">List the available applications in the Batch account.</span></span>  |
| [<span data-ttu-id="981ca-132">az batch pool create</span><span class="sxs-lookup"><span data-stu-id="981ca-132">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="981ca-133">Permet de créer un pool de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="981ca-133">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="981ca-134">az batch pool set</span><span class="sxs-lookup"><span data-stu-id="981ca-134">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="981ca-135">Permet de mettre à jour les propriétés d’un pool.</span><span class="sxs-lookup"><span data-stu-id="981ca-135">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="981ca-136">az batch pool node-agent-skus list</span><span class="sxs-lookup"><span data-stu-id="981ca-136">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="981ca-137">Permet de répertorier les SKU de l’agent de nœud et les informations de l’image.</span><span class="sxs-lookup"><span data-stu-id="981ca-137">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="981ca-138">az batch pool resize</span><span class="sxs-lookup"><span data-stu-id="981ca-138">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="981ca-139">Permet de redimensionner le nombre de machines virtuelles en cours d’exécution dans le pool spécifié.</span><span class="sxs-lookup"><span data-stu-id="981ca-139">Resize the number of running VMs in the specified pool.</span></span>  |
| [<span data-ttu-id="981ca-140">az batch pool show</span><span class="sxs-lookup"><span data-stu-id="981ca-140">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="981ca-141">Permet d’afficher les propriétés d’un pool.</span><span class="sxs-lookup"><span data-stu-id="981ca-141">Display the properties of a pool.</span></span>  |
| [<span data-ttu-id="981ca-142">az batch pool delete</span><span class="sxs-lookup"><span data-stu-id="981ca-142">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="981ca-143">Permet de supprimer le pool spécifié.</span><span class="sxs-lookup"><span data-stu-id="981ca-143">Delete the specified pool.</span></span>  |
| [<span data-ttu-id="981ca-144">az batch pool autoscale enable</span><span class="sxs-lookup"><span data-stu-id="981ca-144">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="981ca-145">Permet d’activer la mise à l’échelle automatique sur un pool et d’appliquer une formule.</span><span class="sxs-lookup"><span data-stu-id="981ca-145">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="981ca-146">az batch pool autoscale disable</span><span class="sxs-lookup"><span data-stu-id="981ca-146">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="981ca-147">Permet de désactiver la mise à l’échelle automatique sur un pool.</span><span class="sxs-lookup"><span data-stu-id="981ca-147">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="981ca-148">az batch node list</span><span class="sxs-lookup"><span data-stu-id="981ca-148">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="981ca-149">Permet de répertorier tous les nœuds de calcul dans le pool spécifié.</span><span class="sxs-lookup"><span data-stu-id="981ca-149">List all the compute node in the specified pool.</span></span>  |
| [<span data-ttu-id="981ca-150">az batch node reboot</span><span class="sxs-lookup"><span data-stu-id="981ca-150">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="981ca-151">Permet de redémarrer le nœud de calcul spécifié.</span><span class="sxs-lookup"><span data-stu-id="981ca-151">Reboot the specified compute node.</span></span>  |
| [<span data-ttu-id="981ca-152">az batch node delete</span><span class="sxs-lookup"><span data-stu-id="981ca-152">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="981ca-153">Permet de supprimer des nœuds répertoriés dans le pool spécifié.</span><span class="sxs-lookup"><span data-stu-id="981ca-153">Delete the listed nodes from the specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="981ca-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="981ca-154">Next steps</span></span>

<span data-ttu-id="981ca-155">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="981ca-155">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="981ca-156">Vous trouverez des exemples supplémentaires de scripts CLI Batch dans la [documentation relative à la CLI Azure Batch](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="981ca-156">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

