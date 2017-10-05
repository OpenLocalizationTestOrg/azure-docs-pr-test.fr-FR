---
title: "Exemple de script Azure CLI - Création d’une machine virtuelle Linux avec NGINX | Microsoft Docs"
description: "Exemple de script Azure CLI - Création d’une machine virtuelle Linux avec NGINX"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 416624d9e378d09f4fb0593119dbc30adeb09f91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-nginx"></a><span data-ttu-id="0eb9e-103">Créer une machine virtuelle avec NGINX</span><span class="sxs-lookup"><span data-stu-id="0eb9e-103">Create a VM with NGINX</span></span>

<span data-ttu-id="0eb9e-104">Ce script crée une machine virtuelle Azure et utilise l’extension du script personnalisé de machine virtuelle Azure pour installer NGINX.</span><span class="sxs-lookup"><span data-stu-id="0eb9e-104">This script creates an Azure Virtual Machine and uses the Azure Virtual Machine Custom Script Extension to install NGINX.</span></span> <span data-ttu-id="0eb9e-105">Une fois que vous avez exécuté le script, vous pouvez accéder à un site web de démonstration sur l’adresse IP publique de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0eb9e-105">After running the script, you can access a demo website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0eb9e-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="0eb9e-106">Sample script</span></span>

<span data-ttu-id="0eb9e-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Création rapide de machine virtuelle")]</span><span class="sxs-lookup"><span data-stu-id="0eb9e-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]</span></span>

## <a name="custom-script-extension"></a><span data-ttu-id="0eb9e-108">Extension de script personnalisé</span><span class="sxs-lookup"><span data-stu-id="0eb9e-108">Custom Script Extension</span></span>

<span data-ttu-id="0eb9e-109">L’extension du script personnalisé copie ce script sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0eb9e-109">The custom script extension copies this script onto the virtual machine.</span></span> <span data-ttu-id="0eb9e-110">Le script est ensuite exécuté pour installer et configurer le serveur web NGINX.</span><span class="sxs-lookup"><span data-stu-id="0eb9e-110">The script is then run to install and configure an NGINX web server.</span></span> 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a><span data-ttu-id="0eb9e-111">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="0eb9e-111">Clean up deployment</span></span> 

<span data-ttu-id="0eb9e-112">Exécutez la commande suivante pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="0eb9e-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="0eb9e-113">Explication du script</span><span class="sxs-lookup"><span data-stu-id="0eb9e-113">Script explanation</span></span>

<span data-ttu-id="0eb9e-114">Ce script utilise les commandes suivantes pour créer un groupe de ressources, une machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="0eb9e-114">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="0eb9e-115">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="0eb9e-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0eb9e-116">Commande</span><span class="sxs-lookup"><span data-stu-id="0eb9e-116">Command</span></span> | <span data-ttu-id="0eb9e-117">Remarques</span><span class="sxs-lookup"><span data-stu-id="0eb9e-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0eb9e-118">az group create</span><span class="sxs-lookup"><span data-stu-id="0eb9e-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0eb9e-119">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="0eb9e-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0eb9e-120">az vm create</span><span class="sxs-lookup"><span data-stu-id="0eb9e-120">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="0eb9e-121">Crée la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0eb9e-121">Creates the virtual machine.</span></span> <span data-ttu-id="0eb9e-122">Cette commande spécifie également l’image de machine virtuelle à utiliser ainsi que les informations d’identification d’administration.</span><span class="sxs-lookup"><span data-stu-id="0eb9e-122">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="0eb9e-123">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="0eb9e-123">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="0eb9e-124">Crée une règle de groupe de sécurité réseau visant à autoriser le trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="0eb9e-124">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="0eb9e-125">Dans cet exemple, le port 80 est ouvert pour le trafic HTTP.</span><span class="sxs-lookup"><span data-stu-id="0eb9e-125">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="0eb9e-126">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="0eb9e-126">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="0eb9e-127">Ajoute et exécute une extension de machine virtuelle sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0eb9e-127">Adds and runs a virtual machine extension to a VM.</span></span> <span data-ttu-id="0eb9e-128">Dans cet exemple, l’extension de script personnalisé sert à installer NGINX.</span><span class="sxs-lookup"><span data-stu-id="0eb9e-128">In this sample, the custom script extension is used to install NGINX.</span></span>|
| [<span data-ttu-id="0eb9e-129">az group delete</span><span class="sxs-lookup"><span data-stu-id="0eb9e-129">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="0eb9e-130">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="0eb9e-130">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0eb9e-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0eb9e-131">Next steps</span></span>

<span data-ttu-id="0eb9e-132">Pour plus d’informations sur l’interface Azure CLI, consultez la [documentation relative à l’interface Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0eb9e-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0eb9e-133">Vous trouverez des exemples supplémentaires de scripts CLI de machine virtuelle dans la [documentation relative aux machines virtuelles Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0eb9e-133">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
