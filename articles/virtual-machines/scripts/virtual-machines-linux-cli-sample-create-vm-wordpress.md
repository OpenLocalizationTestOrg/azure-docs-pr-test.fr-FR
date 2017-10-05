---
title: "Exemple de script Azure CLI - Création d’une machine virtuelle Linux avec WordPress | Microsoft Docs"
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
ms.openlocfilehash: cc95a190b58cb208ac0b642fc9dc2253e993ca23
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-wordpress"></a><span data-ttu-id="d07f0-103">Créer une machine virtuelle avec Wordpress</span><span class="sxs-lookup"><span data-stu-id="d07f0-103">Create a VM with WordPress</span></span>

<span data-ttu-id="d07f0-104">Ce script crée une machine virtuelle, puis utilise l’extension du script personnalisé de machine virtuelle Azure pour installer WordPress.</span><span class="sxs-lookup"><span data-stu-id="d07f0-104">This script creates a virtual machine, and then uses the Azure Virtual Machine custom script extension to install WordPress.</span></span> <span data-ttu-id="d07f0-105">Une fois que vous avez exécuté le script, vous pouvez accéder au site de configuration de WordPress à l’adresse `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="d07f0-105">After running the script, you can access the WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d07f0-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="d07f0-106">Sample script</span></span>

<span data-ttu-id="d07f0-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "Création rapide de machine virtuelle")]</span><span class="sxs-lookup"><span data-stu-id="d07f0-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d07f0-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="d07f0-108">Clean up deployment</span></span> 

<span data-ttu-id="d07f0-109">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="d07f0-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d07f0-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="d07f0-110">Script explanation</span></span>

<span data-ttu-id="d07f0-111">Ce script utilise les commandes suivantes pour créer un groupe de ressources, une machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="d07f0-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="d07f0-112">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="d07f0-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d07f0-113">Commande</span><span class="sxs-lookup"><span data-stu-id="d07f0-113">Command</span></span> | <span data-ttu-id="d07f0-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="d07f0-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d07f0-115">az group create</span><span class="sxs-lookup"><span data-stu-id="d07f0-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d07f0-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="d07f0-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d07f0-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="d07f0-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="d07f0-118">Crée la machine virtuelle et l’associe à la carte réseau, au réseau virtuel, au sous-réseau et au groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="d07f0-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="d07f0-119">Cette commande spécifie également l’image de machine virtuelle à utiliser ainsi que les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="d07f0-119">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="d07f0-120">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="d07f0-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="d07f0-121">Crée une règle de groupe de sécurité réseau visant à autoriser le trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="d07f0-121">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="d07f0-122">Dans cet exemple, le port 80 est ouvert pour le trafic HTTP.</span><span class="sxs-lookup"><span data-stu-id="d07f0-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="d07f0-123">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="d07f0-123">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="d07f0-124">Ajoute une extension de script personnalisé à la machine virtuelle, qui appelle un script pour installer WordPress.</span><span class="sxs-lookup"><span data-stu-id="d07f0-124">Add the Custom Script Extension to the virtual machine, which invokes a script to install WordPress.</span></span> |
| [<span data-ttu-id="d07f0-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="d07f0-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="d07f0-126">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="d07f0-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d07f0-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d07f0-127">Next steps</span></span>

<span data-ttu-id="d07f0-128">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d07f0-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d07f0-129">Vous trouverez des exemples supplémentaires de scripts CLI de machine virtuelle dans la [documentation relative aux machines virtuelles Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d07f0-129">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
