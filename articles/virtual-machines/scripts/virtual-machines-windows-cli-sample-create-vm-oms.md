---
title: "Exemple de script Azure CLI - Création d’une machine virtuelle Windows Server 2016 avec surveillance OMS | Microsoft Docs"
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
ms.openlocfilehash: ddb191163061dc47712e024c8c1d7a6f4bdf325b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="62474-103">Surveiller une machine virtuelle avec Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="62474-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="62474-104">Ce script crée une machine virtuelle Azure, installe l’agent Operations Management Suite (OMS) et inscrit le système avec un espace de nom OMS.</span><span class="sxs-lookup"><span data-stu-id="62474-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="62474-105">Une fois le script exécuté, la machine virtuelle est visible dans la console OMS.</span><span class="sxs-lookup"><span data-stu-id="62474-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="62474-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="62474-106">Sample script</span></span>

<span data-ttu-id="62474-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "Création rapide de machine virtuelle")]</span><span class="sxs-lookup"><span data-stu-id="62474-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="62474-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="62474-108">Clean up deployment</span></span> 

<span data-ttu-id="62474-109">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="62474-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="62474-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="62474-110">Script explanation</span></span>

<span data-ttu-id="62474-111">Ce script utilise les commandes suivantes pour créer un groupe de ressources, une machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="62474-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="62474-112">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="62474-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="62474-113">Commande</span><span class="sxs-lookup"><span data-stu-id="62474-113">Command</span></span> | <span data-ttu-id="62474-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="62474-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="62474-115">az group create</span><span class="sxs-lookup"><span data-stu-id="62474-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="62474-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="62474-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="62474-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="62474-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="62474-118">Crée la machine virtuelle et l’associe à la carte réseau, au réseau virtuel, au sous-réseau et au groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="62474-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="62474-119">Cette commande spécifie également l’image de machine virtuelle à utiliser ainsi que les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="62474-119">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="62474-120">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="62474-120">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="62474-121">Exécute une extension de machine virtuelle sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="62474-121">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="62474-122">Dans ce cas, l’extension de l’agent Operations Management Suite est utilisée pour installer l’agent OMS et inscrire la machine virtuelle dans un espace de nom OMS.</span><span class="sxs-lookup"><span data-stu-id="62474-122">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="62474-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="62474-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="62474-124">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="62474-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="62474-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="62474-125">Next steps</span></span>

<span data-ttu-id="62474-126">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="62474-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="62474-127">Vous trouverez des exemples supplémentaires de scripts CLI de machine virtuelle dans la [documentation relative aux machines virtuelles Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="62474-127">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
