---
title: "aaaAzure exemple de Script CLI - créer un VM Linux avec WordPress | Documents Microsoft"
description: "Exemple de script Azure CLI - Création d’une machine virtuelle Linux avec WordPress"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 2c5c03d08b6d5d27eb8c505b1dbd817eda5f2fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-wordpress"></a><span data-ttu-id="826e5-103">Créer une machine virtuelle avec Wordpress</span><span class="sxs-lookup"><span data-stu-id="826e5-103">Create a VM with WordPress</span></span>

<span data-ttu-id="826e5-104">Ce script crée un ordinateur virtuel et utilise ensuite tooinstall d’extension de script personnalisé de Machine virtuelle Azure hello WordPress.</span><span class="sxs-lookup"><span data-stu-id="826e5-104">This script creates a virtual machine, and then uses hello Azure Virtual Machine custom script extension tooinstall WordPress.</span></span> <span data-ttu-id="826e5-105">Après l’exécution du script hello, vous pouvez accéder à site de configuration hello WordPress à l’adresse `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="826e5-105">After running hello script, you can access hello WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="826e5-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="826e5-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="826e5-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="826e5-107">Clean up deployment</span></span> 

<span data-ttu-id="826e5-108">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="826e5-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="826e5-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="826e5-109">Script explanation</span></span>

<span data-ttu-id="826e5-110">Ce script utilise hello suivant de commandes toocreate un groupe de ressources, l’ordinateur virtuel, et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="826e5-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="826e5-111">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="826e5-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="826e5-112">Commande</span><span class="sxs-lookup"><span data-stu-id="826e5-112">Command</span></span> | <span data-ttu-id="826e5-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="826e5-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="826e5-114">az group create</span><span class="sxs-lookup"><span data-stu-id="826e5-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="826e5-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="826e5-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="826e5-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="826e5-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="826e5-117">Crée la machine virtuelle de hello et connecte une carte réseau de toohello, du réseau virtuel, sous-réseau et groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="826e5-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="826e5-118">Cette commande spécifie également toobe d’image de machine virtuelle hello utilisé et les informations d’identification administratives.</span><span class="sxs-lookup"><span data-stu-id="826e5-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="826e5-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="826e5-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="826e5-120">Crée un tooallow de règle de groupe de sécurité réseau le trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="826e5-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="826e5-121">Dans cet exemple, le port 80 est ouvert pour le trafic HTTP.</span><span class="sxs-lookup"><span data-stu-id="826e5-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="826e5-122">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="826e5-122">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="826e5-123">Ajoutez hello Extension de Script personnalisé toohello machine virtuelle, qui permet d’appeler un script de tooinstall WordPress.</span><span class="sxs-lookup"><span data-stu-id="826e5-123">Add hello Custom Script Extension toohello virtual machine, which invokes a script tooinstall WordPress.</span></span> |
| [<span data-ttu-id="826e5-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="826e5-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="826e5-125">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="826e5-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="826e5-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="826e5-126">Next steps</span></span>

<span data-ttu-id="826e5-127">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="826e5-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="826e5-128">Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de la machine virtuelle de Azure Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="826e5-128">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
