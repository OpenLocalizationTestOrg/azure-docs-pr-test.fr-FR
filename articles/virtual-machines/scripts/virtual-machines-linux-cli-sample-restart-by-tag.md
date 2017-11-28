---
title: "Exemple de script Azure CLI - Redémarrage de machines virtuelles | Microsoft Docs"
description: "Exemple de script Azure CLI - Redémarrer des machines virtuelles par balise et ID"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: 4d0fe95287c91a4b656904f9007ceaaf866e155f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="restart-vms"></a><span data-ttu-id="18134-103">Redémarrer les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="18134-103">Restart VMs</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="18134-104">Cet exemple montre plusieurs façons d’obtenir des machines virtuelles et de les redémarrer.</span><span class="sxs-lookup"><span data-stu-id="18134-104">This sample shows a couple of ways to get some VMs and restart them.</span></span>

<span data-ttu-id="18134-105">Le premier redémarre toutes les machines virtuelles dans le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="18134-105">The first restarts all the VMs in the resource group.</span></span>

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

<span data-ttu-id="18134-106">Le second obtient des machines virtuelles marquées à l’aide de `az resouce list` et filtre les ressources qui sont des machines virtuelles, puis les redémarre.</span><span class="sxs-lookup"><span data-stu-id="18134-106">The second gets the tagged VMs using `az resouce list` and filters to the resources that are VMs, and restarts those VMs.</span></span>

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

<span data-ttu-id="18134-107">Cet exemple fonctionne dans une interface d’interpréteur de commandes Bash.</span><span class="sxs-lookup"><span data-stu-id="18134-107">This sample works in a Bash shell.</span></span> <span data-ttu-id="18134-108">Pour en savoir plus les options d’exécution de scripts Azure CLI dans le client Windows, consultez la page [Running the Azure CLI in Windows (Exécution d’Azure CLI dans Windows)](../windows/cli-options.md).</span><span class="sxs-lookup"><span data-stu-id="18134-108">For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../windows/cli-options.md).</span></span>


## <a name="sample-script"></a><span data-ttu-id="18134-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="18134-109">Sample script</span></span>

<span data-ttu-id="18134-110">L’exemple comporte trois scripts.</span><span class="sxs-lookup"><span data-stu-id="18134-110">The sample has three scripts.</span></span>
<span data-ttu-id="18134-111">Le premier configure les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="18134-111">The first one provisions the virtual machines.</span></span>
<span data-ttu-id="18134-112">Il utilise l’option no-wait. Ainsi, la commande renvoie le résultat sans attendre l’approvisionnement de chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="18134-112">It uses the no-wait option so the command returns without waiting on each VM to be provisioned.</span></span>
<span data-ttu-id="18134-113">Le second attend que les machines virtuelles soient entièrement approvisionnées.</span><span class="sxs-lookup"><span data-stu-id="18134-113">The second waits for the VMs to be fully provisioned.</span></span>
<span data-ttu-id="18134-114">Le troisième script redémarre toutes les machines virtuelles qui ont été configurées, puis simplement les machines virtuelles marquées.</span><span class="sxs-lookup"><span data-stu-id="18134-114">The third script restarts all the VMs that were provisioned, and then just the tagged VMs.</span></span>

### <a name="provision-the-vms"></a><span data-ttu-id="18134-115">Approvisionnement des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="18134-115">Provision the VMs</span></span>

<span data-ttu-id="18134-116">Ce script crée un groupe de ressources, puis trois machines virtuelles à redémarrer.</span><span class="sxs-lookup"><span data-stu-id="18134-116">This script creates a resource group and then it creates three VMs to restart.</span></span>
<span data-ttu-id="18134-117">Deux présentent un indicateur.</span><span class="sxs-lookup"><span data-stu-id="18134-117">Two of them are tagged.</span></span>

<span data-ttu-id="18134-118">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Approvisionnement des machines virtuelles")]</span><span class="sxs-lookup"><span data-stu-id="18134-118">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision the VMs")]</span></span>

### <a name="wait"></a><span data-ttu-id="18134-119">Wait</span><span class="sxs-lookup"><span data-stu-id="18134-119">Wait</span></span>

<span data-ttu-id="18134-120">Ce script vérifie l’état de configuration toutes les 20 secondes jusqu'à ce que les trois machines virtuelles soient approvisionnées, ou qu’une d’entre elles ne puisse l’être.</span><span class="sxs-lookup"><span data-stu-id="18134-120">This script checks on the provisioning status every 20 seconds until all three VMs are provisioned, or one of them fails to provision.</span></span>

<span data-ttu-id="18134-121">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Attente du provisionnement des machines virtuelles")]</span><span class="sxs-lookup"><span data-stu-id="18134-121">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for the VMs to be provisioned")]</span></span>

### <a name="restart-the-vms"></a><span data-ttu-id="18134-122">Redémarrer les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="18134-122">Restart the VMs</span></span>

<span data-ttu-id="18134-123">Ce script redémarre toutes les machines virtuelles dans le groupe de ressources, puis redémarre uniquement les machines virtuelles marquées.</span><span class="sxs-lookup"><span data-stu-id="18134-123">This script restarts all the VMs in the resource group, and then it restarts just the tagged VMs.</span></span>

<span data-ttu-id="18134-124">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Redémarrer les machines virtuelles par balise")]</span><span class="sxs-lookup"><span data-stu-id="18134-124">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="18134-125">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="18134-125">Clean up deployment</span></span> 

<span data-ttu-id="18134-126">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer les groupes de ressources, les machines virtuelles et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="18134-126">After the script sample has been run, the following command can be used to remove the resource groups, VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a><span data-ttu-id="18134-127">Explication du script</span><span class="sxs-lookup"><span data-stu-id="18134-127">Script explanation</span></span>

<span data-ttu-id="18134-128">Ce script utilise les commandes suivantes pour créer un groupe de ressources, une machine virtuelle, un groupe à haute disponibilité, un équilibreur de charge et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="18134-128">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="18134-129">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="18134-129">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="18134-130">Commande</span><span class="sxs-lookup"><span data-stu-id="18134-130">Command</span></span> | <span data-ttu-id="18134-131">Remarques</span><span class="sxs-lookup"><span data-stu-id="18134-131">Notes</span></span> |
|---|---|
| [<span data-ttu-id="18134-132">az group create</span><span class="sxs-lookup"><span data-stu-id="18134-132">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="18134-133">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="18134-133">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="18134-134">az vm create</span><span class="sxs-lookup"><span data-stu-id="18134-134">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="18134-135">Crée les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="18134-135">Creates the virtual machines.</span></span>  |
| [<span data-ttu-id="18134-136">az vm list</span><span class="sxs-lookup"><span data-stu-id="18134-136">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="18134-137">Utilisé avec `--query` pour garantir que les machines virtuelles sont configurées avant de les redémarrer, puis pour obtenir les ID des machines virtuelles pour les redémarrer.</span><span class="sxs-lookup"><span data-stu-id="18134-137">Used with `--query` to ensure the VMs are provisioned before restarting them, and then to get the IDs of the VMs to restart them.</span></span> |
| [<span data-ttu-id="18134-138">az resource list</span><span class="sxs-lookup"><span data-stu-id="18134-138">az resource list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="18134-139">Utilisé avec `--query` pour obtenir les ID des machines virtuelles qui utilisent l’indicateur.</span><span class="sxs-lookup"><span data-stu-id="18134-139">Used with `--query` to get the IDs of the VMs using the tag.</span></span> |
| [<span data-ttu-id="18134-140">az vm restart</span><span class="sxs-lookup"><span data-stu-id="18134-140">az vm restart</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="18134-141">Redémarre les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="18134-141">Restarts the VMs.</span></span> |
| [<span data-ttu-id="18134-142">az group delete</span><span class="sxs-lookup"><span data-stu-id="18134-142">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="18134-143">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="18134-143">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="18134-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="18134-144">Next steps</span></span>

<span data-ttu-id="18134-145">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="18134-145">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="18134-146">Vous trouverez des exemples supplémentaires de scripts CLI de machine virtuelle dans la [documentation relative aux machines virtuelles Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="18134-146">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
