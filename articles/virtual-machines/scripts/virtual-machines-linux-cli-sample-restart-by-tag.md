---
title: "aaaAzure exemple de Script CLI - redémarrer les machines virtuelles | Documents Microsoft"
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
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a><span data-ttu-id="a95f8-103">Redémarrer les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="a95f8-103">Restart VMs</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="a95f8-104">Cet exemple montre deux façons tooget certaines machines virtuelles et les redémarrer.</span><span class="sxs-lookup"><span data-stu-id="a95f8-104">This sample shows a couple of ways tooget some VMs and restart them.</span></span>

<span data-ttu-id="a95f8-105">Hello redémarre tout d’abord tous les ordinateurs virtuels de hello dans le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="a95f8-105">hello first restarts all hello VMs in hello resource group.</span></span>

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

<span data-ttu-id="a95f8-106">deuxième obtient hello Hello marqué à l’aide de machines virtuelles `az resouce list` filtre toohello les ressources qui sont des machines virtuelles et redémarre ces machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="a95f8-106">hello second gets hello tagged VMs using `az resouce list` and filters toohello resources that are VMs, and restarts those VMs.</span></span>

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

<span data-ttu-id="a95f8-107">Cet exemple fonctionne dans une interface d’interpréteur de commandes Bash.</span><span class="sxs-lookup"><span data-stu-id="a95f8-107">This sample works in a Bash shell.</span></span> <span data-ttu-id="a95f8-108">Pour les options sur l’exécution de scripts CLI d’Azure sur le client Windows, consultez [hello CLI d’Azure en cours d’exécution dans Windows](../windows/cli-options.md).</span><span class="sxs-lookup"><span data-stu-id="a95f8-108">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../windows/cli-options.md).</span></span>


## <a name="sample-script"></a><span data-ttu-id="a95f8-109">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="a95f8-109">Sample script</span></span>

<span data-ttu-id="a95f8-110">exemple Hello possède trois scripts.</span><span class="sxs-lookup"><span data-stu-id="a95f8-110">hello sample has three scripts.</span></span>
<span data-ttu-id="a95f8-111">Bonjour tout d’abord un approvisionne les ordinateurs virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="a95f8-111">hello first one provisions hello virtual machines.</span></span>
<span data-ttu-id="a95f8-112">Utilise hello non-wait option commande hello retourne sans attendre sur chaque toobe de machine virtuelle configurée.</span><span class="sxs-lookup"><span data-stu-id="a95f8-112">It uses hello no-wait option so hello command returns without waiting on each VM toobe provisioned.</span></span>
<span data-ttu-id="a95f8-113">Hello attend ensuite toobe de machines virtuelles hello entièrement configuré.</span><span class="sxs-lookup"><span data-stu-id="a95f8-113">hello second waits for hello VMs toobe fully provisioned.</span></span>
<span data-ttu-id="a95f8-114">script de tiers Hello redémarre tous les ordinateurs virtuels hello qui ont été configurés, et puis hello simplement marquées des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="a95f8-114">hello third script restarts all hello VMs that were provisioned, and then just hello tagged VMs.</span></span>

### <a name="provision-hello-vms"></a><span data-ttu-id="a95f8-115">Configurer des machines virtuelles de hello</span><span class="sxs-lookup"><span data-stu-id="a95f8-115">Provision hello VMs</span></span>

<span data-ttu-id="a95f8-116">Ce script crée un groupe de ressources, puis il crée trois machines virtuelles toorestart.</span><span class="sxs-lookup"><span data-stu-id="a95f8-116">This script creates a resource group and then it creates three VMs toorestart.</span></span>
<span data-ttu-id="a95f8-117">Deux présentent un indicateur.</span><span class="sxs-lookup"><span data-stu-id="a95f8-117">Two of them are tagged.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a><span data-ttu-id="a95f8-118">Wait</span><span class="sxs-lookup"><span data-stu-id="a95f8-118">Wait</span></span>

<span data-ttu-id="a95f8-119">Ce script vérifie hello toutes les 20 secondes jusqu'à ce que tous les trois machines virtuelles sont configurés, ou un d’eux échoue tooprovision état de préparation.</span><span class="sxs-lookup"><span data-stu-id="a95f8-119">This script checks on hello provisioning status every 20 seconds until all three VMs are provisioned, or one of them fails tooprovision.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a><span data-ttu-id="a95f8-120">Redémarrez les ordinateurs virtuels de hello</span><span class="sxs-lookup"><span data-stu-id="a95f8-120">Restart hello VMs</span></span>

<span data-ttu-id="a95f8-121">Ce script redémarre tous les ordinateurs virtuels de hello dans le groupe de ressources hello, puis il redémarre simplement machines virtuelles hello marquée.</span><span class="sxs-lookup"><span data-stu-id="a95f8-121">This script restarts all hello VMs in hello resource group, and then it restarts just hello tagged VMs.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a95f8-122">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="a95f8-122">Clean up deployment</span></span> 

<span data-ttu-id="a95f8-123">Après exécution de l’exemple de script hello, hello commande suivante peut être utilisé tooremove hello les groupes de ressources, de machines virtuelles et de toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="a95f8-123">After hello script sample has been run, hello following command can be used tooremove hello resource groups, VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a><span data-ttu-id="a95f8-124">Explication du script</span><span class="sxs-lookup"><span data-stu-id="a95f8-124">Script explanation</span></span>

<span data-ttu-id="a95f8-125">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, machine virtuelle, haute disponibilité, équilibrage de charge et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="a95f8-125">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="a95f8-126">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="a95f8-126">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a95f8-127">Commande</span><span class="sxs-lookup"><span data-stu-id="a95f8-127">Command</span></span> | <span data-ttu-id="a95f8-128">Remarques</span><span class="sxs-lookup"><span data-stu-id="a95f8-128">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a95f8-129">az group create</span><span class="sxs-lookup"><span data-stu-id="a95f8-129">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a95f8-130">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="a95f8-130">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a95f8-131">az vm create</span><span class="sxs-lookup"><span data-stu-id="a95f8-131">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="a95f8-132">Crée des machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="a95f8-132">Creates hello virtual machines.</span></span>  |
| [<span data-ttu-id="a95f8-133">az vm list</span><span class="sxs-lookup"><span data-stu-id="a95f8-133">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="a95f8-134">Utilisé avec `--query` tooensure hello machines virtuelles sont configurés avant de les redémarrer, et puis tooget hello ID de hello machines virtuelles toorestart les.</span><span class="sxs-lookup"><span data-stu-id="a95f8-134">Used with `--query` tooensure hello VMs are provisioned before restarting them, and then tooget hello IDs of hello VMs toorestart them.</span></span> |
| [<span data-ttu-id="a95f8-135">az resource list</span><span class="sxs-lookup"><span data-stu-id="a95f8-135">az resource list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="a95f8-136">Utilisé avec `--query` tooget hello ID des machines virtuelles de hello à l’aide de la balise de hello.</span><span class="sxs-lookup"><span data-stu-id="a95f8-136">Used with `--query` tooget hello IDs of hello VMs using hello tag.</span></span> |
| [<span data-ttu-id="a95f8-137">az vm restart</span><span class="sxs-lookup"><span data-stu-id="a95f8-137">az vm restart</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="a95f8-138">Redémarre les machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="a95f8-138">Restarts hello VMs.</span></span> |
| [<span data-ttu-id="a95f8-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="a95f8-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="a95f8-140">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="a95f8-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a95f8-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a95f8-141">Next steps</span></span>

<span data-ttu-id="a95f8-142">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a95f8-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a95f8-143">Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de la machine virtuelle de Azure Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a95f8-143">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
