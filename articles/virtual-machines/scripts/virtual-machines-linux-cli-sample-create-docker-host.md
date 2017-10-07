---
title: "aaaAzure exemple de Script CLI - créer un hôte Docker | Documents Microsoft"
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
ms.openlocfilehash: 7df2561c428ff5d3ab0a0d53c8e046781996be77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-docker"></a><span data-ttu-id="51675-103">Créer une machine virtuelle avec Docker</span><span class="sxs-lookup"><span data-stu-id="51675-103">Create a VM with Docker</span></span>

<span data-ttu-id="51675-104">Ce script crée une machine virtuelle avec Docker activé et démarre un conteneur Docker exécutant NGINX.</span><span class="sxs-lookup"><span data-stu-id="51675-104">This script creates a virtual machine with Docker enabled and starts a Docker container running NGINX.</span></span> <span data-ttu-id="51675-105">Après avoir exécuté le script de hello, vous pouvez accéder serveur de web NGINX hello via hello nom de domaine complet de hello machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="51675-105">After running hello script, you can access hello NGINX web server through hello FQDN of hello Azure virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="51675-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="51675-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker Host")]

## <a name="clean-up-deployment"></a><span data-ttu-id="51675-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="51675-107">Clean up deployment</span></span> 

<span data-ttu-id="51675-108">Exécutez hello suivant du groupe de ressources de commande tooremove hello, machine virtuelle et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="51675-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="51675-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="51675-109">Script explanation</span></span>

<span data-ttu-id="51675-110">Ce script utilise hello après le déploiement de commandes toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="51675-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="51675-111">Chaque élément de la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="51675-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="51675-112">Commande</span><span class="sxs-lookup"><span data-stu-id="51675-112">Command</span></span> | <span data-ttu-id="51675-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="51675-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="51675-114">az group create</span><span class="sxs-lookup"><span data-stu-id="51675-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="51675-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="51675-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="51675-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="51675-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="51675-117">Crée la machine virtuelle de hello et connecte une carte réseau de toohello, du réseau virtuel, sous-réseau et groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="51675-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="51675-118">Cette commande spécifie également toobe d’image de machine virtuelle hello utilisé et les informations d’identification administratives.</span><span class="sxs-lookup"><span data-stu-id="51675-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="51675-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="51675-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="51675-120">Crée un tooallow de règle de groupe de sécurité réseau le trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="51675-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="51675-121">Dans cet exemple, le port 80 est ouvert pour le trafic HTTP.</span><span class="sxs-lookup"><span data-stu-id="51675-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="51675-122">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="51675-122">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="51675-123">Ajoute et exécute un tooa d’extension de machine virtuelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="51675-123">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="51675-124">Dans cet exemple, hello extension de machine virtuelle de Docker est tooconfigure utilisé un hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="51675-124">In this sample, hello Docker VM extension is used tooconfigure a Docker host.</span></span>|
| [<span data-ttu-id="51675-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="51675-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="51675-126">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="51675-126">Deletes a resource group, including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="51675-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="51675-127">Next steps</span></span>

<span data-ttu-id="51675-128">Pour plus d’informations sur hello CLI d’Azure, consultez [documentation relative à Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="51675-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="51675-129">Exemples de script CLI supplémentaires de l’ordinateur virtuel se trouvent dans hello [documentation de la machine virtuelle de Azure Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51675-129">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
