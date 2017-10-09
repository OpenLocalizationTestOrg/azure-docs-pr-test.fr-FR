---
title: "aaaAzure exemple de Script CLI - créer un ordinateur Windows Server 2016 avec IIS à l’aide de DSC | Documents Microsoft"
description: "Exemple de script Azure CLI - Création d’une machine virtuelle Windows Server 2016 avec IIS à l’aide de DSC"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.custom: mvc
ms.openlocfilehash: 9883b5925dddca3dd53d083679a0e76d0fb982e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-iis-using-dsc"></a><span data-ttu-id="51ffe-103">Créer une machine virtuelle avec IIS à l’aide de DSC</span><span class="sxs-lookup"><span data-stu-id="51ffe-103">Create a VM with IIS using DSC</span></span>

<span data-ttu-id="51ffe-104">Ce script crée un ordinateur virtuel et utilise tooinstall d’extension hello DSC de Machine virtuelle Azure script personnalisé et configurer IIS.</span><span class="sxs-lookup"><span data-stu-id="51ffe-104">This script creates a virtual machine, and uses hello Azure Virtual Machine DSC custom script extension tooinstall and configure IIS.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="51ffe-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="51ffe-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-windows-iis-using-dsc/create-windows-iis-using-dsc.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="51ffe-106">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="51ffe-106">Clean up deployment</span></span> 

<span data-ttu-id="51ffe-107">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="51ffe-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="51ffe-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="51ffe-108">Script explanation</span></span>

<span data-ttu-id="51ffe-109">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’ordinateur virtuel, et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="51ffe-109">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="51ffe-110">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="51ffe-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="51ffe-111">Commande</span><span class="sxs-lookup"><span data-stu-id="51ffe-111">Command</span></span> | <span data-ttu-id="51ffe-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="51ffe-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="51ffe-113">az group create</span><span class="sxs-lookup"><span data-stu-id="51ffe-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="51ffe-114">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="51ffe-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="51ffe-115">az vm create</span><span class="sxs-lookup"><span data-stu-id="51ffe-115">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="51ffe-116">Crée la machine virtuelle de hello et connecte une carte réseau de toohello, du réseau virtuel, sous-réseau et groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="51ffe-116">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="51ffe-117">Cette commande spécifie également toobe d’image de machine virtuelle hello utilisé et les informations d’identification administratives.</span><span class="sxs-lookup"><span data-stu-id="51ffe-117">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="51ffe-118">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="51ffe-118">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="51ffe-119">Ajoutez ordinateur hello Extension de Script personnalisé toohello virtuel qui permet d’appeler un tooinstall de script IIS.</span><span class="sxs-lookup"><span data-stu-id="51ffe-119">Add hello Custom Script Extension toohello virtual machine which invokes a script tooinstall IIS.</span></span> |
| [<span data-ttu-id="51ffe-120">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="51ffe-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="51ffe-121">Crée un tooallow de règle de groupe de sécurité réseau le trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="51ffe-121">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="51ffe-122">Dans cet exemple, le port 80 est ouvert pour le trafic HTTP.</span><span class="sxs-lookup"><span data-stu-id="51ffe-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="51ffe-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="51ffe-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="51ffe-124">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="51ffe-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="51ffe-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="51ffe-125">Next steps</span></span>

<span data-ttu-id="51ffe-126">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="51ffe-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="51ffe-127">Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de Windows Azure VM](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51ffe-127">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
