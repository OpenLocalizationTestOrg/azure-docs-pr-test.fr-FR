---
title: "aaaAzure exemple de Script CLI - déployer hello pile LAMP dans un ensemble d’échelle Balanced virtuel Ajouter | Documents Microsoft"
description: "Utiliser un toodeploy hello pile LAMP de script personnalisé extension dans une charge = en puissance des machines virtuelles à charge équilibrée sur Azure."
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
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a><span data-ttu-id="c21a0-103">Déployer la pile de feu hello dans un ensemble d’échelle équilibrage de la charge des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="c21a0-103">Deploy hello LAMP stack in a load-balanced virtual machine scale set</span></span>

<span data-ttu-id="c21a0-104">Cet exemple crée un ensemble d’échelle de machine virtuelle et s’applique à une extension qui exécute une pile LAMP de script personnalisé toodeploy hello sur chaque ordinateur virtuel dans un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="c21a0-104">This example creates a virtual machine scale set and applies an extension that runs a custom script toodeploy hello LAMP stack on each virtual machine in hello scale set.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="c21a0-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="c21a0-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a><span data-ttu-id="c21a0-106">Connecter</span><span class="sxs-lookup"><span data-stu-id="c21a0-106">Connect</span></span>

<span data-ttu-id="c21a0-107">Utilisez cette toosee code comment tooconnect tooyour machines virtuelles et l’échelle définies.</span><span class="sxs-lookup"><span data-stu-id="c21a0-107">Use this code toosee how tooconnect tooyour VMs and your scale set.</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c21a0-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="c21a0-108">Clean up deployment</span></span> 

<span data-ttu-id="c21a0-109">Exécutez hello suivant commande tooremove hello groupe de ressources, un ensemble d’échelle hello et machines virtuelles et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="c21a0-109">Run hello following command tooremove hello resource group, hello scale set and VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c21a0-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="c21a0-110">Script explanation</span></span>

<span data-ttu-id="c21a0-111">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, machine virtuelle, haute disponibilité, équilibrage de charge et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="c21a0-111">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="c21a0-112">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="c21a0-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c21a0-113">Commande</span><span class="sxs-lookup"><span data-stu-id="c21a0-113">Command</span></span> | <span data-ttu-id="c21a0-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="c21a0-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c21a0-115">az group create</span><span class="sxs-lookup"><span data-stu-id="c21a0-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c21a0-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="c21a0-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c21a0-117">az vmss create</span><span class="sxs-lookup"><span data-stu-id="c21a0-117">az vmss create</span></span>](https://docs.microsoft.com/cli/azure/vmss#create) | <span data-ttu-id="c21a0-118">Crée un groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="c21a0-118">Creates a virtual machine scale set</span></span> |
| [<span data-ttu-id="c21a0-119">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="c21a0-119">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="c21a0-120">Ajouter un point de terminaison à charge équilibrée</span><span class="sxs-lookup"><span data-stu-id="c21a0-120">Add a load-balanced endpoint</span></span> |
| [<span data-ttu-id="c21a0-121">az vmss extension set</span><span class="sxs-lookup"><span data-stu-id="c21a0-121">az vmss extension set</span></span>](https://docs.microsoft.com/cli/azure/vmss/extension#set) | <span data-ttu-id="c21a0-122">Créer une extension de hello qui exécute un script personnalisé hello sur le déploiement d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c21a0-122">Create hello extension that runs hello custom script on deployment of a VM</span></span> |
| [<span data-ttu-id="c21a0-123">az vmss update-instances</span><span class="sxs-lookup"><span data-stu-id="c21a0-123">az vmss update-instances</span></span>](https://docs.microsoft.com/cli/azure/vmss#update-instances) | <span data-ttu-id="c21a0-124">Exécuter un script personnalisé hello sur des instances de machine virtuelle hello qui ont été déployées avant l’application d’extension de hello toohello un ensemble d’échelle.</span><span class="sxs-lookup"><span data-stu-id="c21a0-124">Run hello custom script on hello VM instances that were deployed before hello extension was applied toohello scale set.</span></span> |
| [<span data-ttu-id="c21a0-125">az vmss scale</span><span class="sxs-lookup"><span data-stu-id="c21a0-125">az vmss scale</span></span>](https://docs.microsoft.com/cli/azure/vmss#scale) | <span data-ttu-id="c21a0-126">Monter en puissance hello en ajoutant d’autres instances de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c21a0-126">Scale up hello scale set by adding more VM instances.</span></span> <span data-ttu-id="c21a0-127">un script personnalisé Hello est exécuté sur ces lorsqu’ils sont déployés.</span><span class="sxs-lookup"><span data-stu-id="c21a0-127">hello custom script is run on these when they are deployed.</span></span> |
| [<span data-ttu-id="c21a0-128">az network public-ip list</span><span class="sxs-lookup"><span data-stu-id="c21a0-128">az network public-ip list</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#list) | <span data-ttu-id="c21a0-129">Obtenir les adresses IP de hello Hello machines virtuelles créées par exemple hello.</span><span class="sxs-lookup"><span data-stu-id="c21a0-129">Get hello IP addresses of hello VMs created by hello sample.</span></span> |
| [<span data-ttu-id="c21a0-130">az network lb show</span><span class="sxs-lookup"><span data-stu-id="c21a0-130">az network lb show</span></span>](https://docs.microsoft.com/cli/azure/network/lb#show) | <span data-ttu-id="c21a0-131">Obtenir des ports utilisés par l’équilibrage de charge hello principal et serveur frontal de hello.</span><span class="sxs-lookup"><span data-stu-id="c21a0-131">Get hello frontend and backend ports used by hello load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c21a0-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c21a0-132">Next steps</span></span>

<span data-ttu-id="c21a0-133">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c21a0-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c21a0-134">Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de la machine virtuelle de Azure Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c21a0-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
