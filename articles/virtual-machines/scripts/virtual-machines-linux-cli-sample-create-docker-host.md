---
title: "Exemple de script Azure CLI - Créer un hôte Docker | Microsoft Docs"
description: "Exemple de script Azure CLI - Créer un hôte Docker"
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
ms.date: 03/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: e8704824dec66d724f2d30dab4d6bdf019c6b206
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-docker"></a><span data-ttu-id="39614-103">Créer une machine virtuelle avec Docker</span><span class="sxs-lookup"><span data-stu-id="39614-103">Create a VM with Docker</span></span>

<span data-ttu-id="39614-104">Ce script crée une machine virtuelle avec Docker activé et démarre un conteneur Docker exécutant NGINX.</span><span class="sxs-lookup"><span data-stu-id="39614-104">This script creates a virtual machine with Docker enabled and starts a Docker container running NGINX.</span></span> <span data-ttu-id="39614-105">Une fois que vous avez exécuté le script, vous pouvez accéder au serveur web NGINX par le biais du nom de domaine complet de la machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="39614-105">After running the script, you can access the NGINX web server through the FQDN of the Azure virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="39614-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="39614-106">Sample script</span></span>

<span data-ttu-id="39614-107">[!code-azurecli-interactive[principal](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Hôte Docker")]</span><span class="sxs-lookup"><span data-stu-id="39614-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker Host")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="39614-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="39614-108">Clean up deployment</span></span> 

<span data-ttu-id="39614-109">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="39614-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="39614-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="39614-110">Script explanation</span></span>

<span data-ttu-id="39614-111">Ce script a recours aux commandes suivantes pour créer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="39614-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="39614-112">Chaque élément du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="39614-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="39614-113">Commande</span><span class="sxs-lookup"><span data-stu-id="39614-113">Command</span></span> | <span data-ttu-id="39614-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="39614-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="39614-115">az group create</span><span class="sxs-lookup"><span data-stu-id="39614-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="39614-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="39614-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="39614-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="39614-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="39614-118">Crée la machine virtuelle et l’associe à la carte réseau, au réseau virtuel, au sous-réseau et au groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="39614-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="39614-119">Cette commande spécifie également l’image de machine virtuelle à utiliser ainsi que les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="39614-119">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="39614-120">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="39614-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="39614-121">Crée une règle de groupe de sécurité réseau visant à autoriser le trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="39614-121">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="39614-122">Dans cet exemple, le port 80 est ouvert pour le trafic HTTP.</span><span class="sxs-lookup"><span data-stu-id="39614-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="39614-123">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="39614-123">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="39614-124">Ajoute et exécute une extension de machine virtuelle sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="39614-124">Adds and runs a virtual machine extension to a VM.</span></span> <span data-ttu-id="39614-125">Dans cet exemple, l’extension de machine virtuelle Docker est utilisée pour configurer un hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="39614-125">In this sample, the Docker VM extension is used to configure a Docker host.</span></span>|
| [<span data-ttu-id="39614-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="39614-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="39614-127">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="39614-127">Deletes a resource group, including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="39614-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="39614-128">Next steps</span></span>

<span data-ttu-id="39614-129">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="39614-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="39614-130">Vous trouverez des exemples supplémentaires de scripts CLI de machine virtuelle dans la [documentation relative aux machines virtuelles Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="39614-130">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
