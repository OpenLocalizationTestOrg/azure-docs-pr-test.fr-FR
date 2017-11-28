---
title: "aaaAzure exemple de Script CLI - créer un ordinateur Windows Server 2016 avec l’analyse d’OMS | Documents Microsoft"
description: "Exemple de script Azure CLI - Création d’une machine virtuelle Windows Server 2016 avec surveillance OMS"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: 4f070430ccc5d5402ed4a80ead3b78eff25dcd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="bcd3d-103">Surveiller une machine virtuelle avec Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="bcd3d-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="bcd3d-104">Ce script crée une Machine virtuelle Azure installe l’agent Operations Management Suite (OMS) de hello et inscrit système hello avec un espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="bcd3d-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="bcd3d-105">Une fois le script de hello a exécuté, hello virtuels seront visibles dans la console OMS hello.</span><span class="sxs-lookup"><span data-stu-id="bcd3d-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="bcd3d-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="bcd3d-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="bcd3d-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="bcd3d-107">Clean up deployment</span></span> 

<span data-ttu-id="bcd3d-108">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="bcd3d-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="bcd3d-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="bcd3d-109">Script explanation</span></span>

<span data-ttu-id="bcd3d-110">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’ordinateur virtuel, et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="bcd3d-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="bcd3d-111">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="bcd3d-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="bcd3d-112">Commande</span><span class="sxs-lookup"><span data-stu-id="bcd3d-112">Command</span></span> | <span data-ttu-id="bcd3d-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="bcd3d-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bcd3d-114">az group create</span><span class="sxs-lookup"><span data-stu-id="bcd3d-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="bcd3d-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="bcd3d-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bcd3d-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="bcd3d-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="bcd3d-117">Crée la machine virtuelle de hello et connecte une carte réseau de toohello, du réseau virtuel, sous-réseau et groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="bcd3d-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="bcd3d-118">Cette commande spécifie également toobe d’image de machine virtuelle hello utilisé et les informations d’identification administratives.</span><span class="sxs-lookup"><span data-stu-id="bcd3d-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="bcd3d-119">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="bcd3d-119">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="bcd3d-120">Exécute une extension de machine virtuelle sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bcd3d-120">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="bcd3d-121">Dans ce cas, hello extension de l’agent Operations Management Suite est utilisé tooinstall hello OMS agent et inscrire hello machine virtuelle dans un espace de travail OMS.</span><span class="sxs-lookup"><span data-stu-id="bcd3d-121">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="bcd3d-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="bcd3d-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="bcd3d-123">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="bcd3d-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bcd3d-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bcd3d-124">Next steps</span></span>

<span data-ttu-id="bcd3d-125">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bcd3d-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="bcd3d-126">Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de Windows Azure VM](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bcd3d-126">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
