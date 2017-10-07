---
title: "aaaAzure démarrage rapide - CLI de machine virtuelle créer | Documents Microsoft"
description: "En savoir plus rapidement des machines virtuelles de toocreate avec hello CLI d’Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 0d9c686e2f4c7339b29b8c43cd1dd9ee56d7dc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="a60b8-103">Créer une machine virtuelle Linux avec hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="a60b8-103">Create a Linux virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="a60b8-104">Hello CLI d’Azure est utilisé toocreate et gérer des ressources Azure à partir de la ligne de commande hello ou dans des scripts.</span><span class="sxs-lookup"><span data-stu-id="a60b8-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="a60b8-105">Ce guide décrit en détail à l’aide de hello CLI d’Azure toodeploy une machine virtuelle exécutant Ubuntu server.</span><span class="sxs-lookup"><span data-stu-id="a60b8-105">This guide details using hello Azure CLI toodeploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="a60b8-106">Une fois que le serveur de hello est déployé, une connexion SSH est créée, et un serveur Web NGINX est installé.</span><span class="sxs-lookup"><span data-stu-id="a60b8-106">Once hello server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="a60b8-107">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="a60b8-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a60b8-108">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce démarrage rapide nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="a60b8-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a60b8-109">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="a60b8-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a60b8-110">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a60b8-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="a60b8-111">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="a60b8-111">Create a resource group</span></span>

<span data-ttu-id="a60b8-112">Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="a60b8-112">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="a60b8-113">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="a60b8-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="a60b8-114">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement.</span><span class="sxs-lookup"><span data-stu-id="a60b8-114">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="a60b8-115">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="a60b8-115">Create virtual machine</span></span>

<span data-ttu-id="a60b8-116">Créer une machine virtuelle avec hello [az vm créer](/cli/azure/vm#create) commande.</span><span class="sxs-lookup"><span data-stu-id="a60b8-116">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="a60b8-117">Hello exemple suivant crée un ordinateur virtuel nommé *myVM* et crée des clés SSH s’ils n’existent pas déjà dans un emplacement de la clé par défaut.</span><span class="sxs-lookup"><span data-stu-id="a60b8-117">hello following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="a60b8-118">toouse un ensemble spécifique de clés, utilisez hello `--ssh-key-value` option.</span><span class="sxs-lookup"><span data-stu-id="a60b8-118">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="a60b8-119">Lorsque hello machine virtuelle a été créé, hello CLI d’Azure affiche les informations toohello semblable l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="a60b8-119">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="a60b8-120">Prenez note de hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="a60b8-120">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="a60b8-121">Cette adresse est utilisée tooaccess hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a60b8-121">This address is used tooaccess hello VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="a60b8-122">Ouvrez le port 80 pour le trafic web</span><span class="sxs-lookup"><span data-stu-id="a60b8-122">Open port 80 for web traffic</span></span> 

<span data-ttu-id="a60b8-123">Par défaut, seules les connexions SSH sont autorisées dans les machines virtuelles Linux déployées dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a60b8-123">By default only SSH connections are allowed into Linux virtual machines deployed in Azure.</span></span> <span data-ttu-id="a60b8-124">Si cet ordinateur virtuel est toobe un serveur Web, vous devez tooopen port 80 de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="a60b8-124">If this VM is going toobe a webserver, you need tooopen port 80 from hello Internet.</span></span> <span data-ttu-id="a60b8-125">Hello d’utilisation [ouvrir un ordinateur virtuel az-port](/cli/azure/vm#open-port) commande tooopen hello souhaité de port.</span><span class="sxs-lookup"><span data-stu-id="a60b8-125">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a><span data-ttu-id="a60b8-126">Se connecter avec SSH à votre machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="a60b8-126">SSH into your VM</span></span>

<span data-ttu-id="a60b8-127">La commande suivante de hello utilisation toocreate une session SSH avec l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="a60b8-127">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="a60b8-128">Assurez-vous que tooreplace  *<publicIpAddress>*  avec hello corriger l’adresse IP publique de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a60b8-128">Make sure tooreplace *<publicIpAddress>* with hello correct public IP address of your virtual machine.</span></span>  <span data-ttu-id="a60b8-129">Dans l’exemple ci-dessus, notre adresse IP était *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="a60b8-129">In our example above our IP address was *40.68.254.142*.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a><span data-ttu-id="a60b8-130">Installer NGINX</span><span class="sxs-lookup"><span data-stu-id="a60b8-130">Install NGINX</span></span>

<span data-ttu-id="a60b8-131">Suivante de hello utilisez bash sources de package tooupdate de script et installer le dernier package de NGINX hello.</span><span class="sxs-lookup"><span data-stu-id="a60b8-131">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-nginx-welcome-page"></a><span data-ttu-id="a60b8-132">Page d’accueil de vue hello NGINX</span><span class="sxs-lookup"><span data-stu-id="a60b8-132">View hello NGINX welcome page</span></span>

<span data-ttu-id="a60b8-133">Avec NGINX installé et le port 80 maintenant ouvrir sur votre machine virtuelle à partir de hello Internet, vous pouvez utiliser un navigateur web de votre choix tooview hello par défaut NGINX page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="a60b8-133">With NGINX installed and port 80 now open on your VM from hello Internet - you can use a web browser of your choice tooview hello default NGINX welcome page.</span></span> <span data-ttu-id="a60b8-134">Être vraiment toouse hello *publicIpAddress* vous documenté au-dessus de la page par défaut toovisit hello.</span><span class="sxs-lookup"><span data-stu-id="a60b8-134">Be sure toouse hello *publicIpAddress* you documented above toovisit hello default page.</span></span> 

![Site par défaut NGINX](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a><span data-ttu-id="a60b8-136">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="a60b8-136">Clean up resources</span></span>

<span data-ttu-id="a60b8-137">Lorsque vous n’est plus nécessaire, vous pouvez utiliser hello [suppression du groupe az](/cli/azure/group#delete) groupe de ressources tooremove hello, machine virtuelle et toutes les ressources de la commande.</span><span class="sxs-lookup"><span data-stu-id="a60b8-137">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="a60b8-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a60b8-138">Next steps</span></span>

<span data-ttu-id="a60b8-139">Dans ce guide de démarrage rapide, vous avez déployé une machine virtuelle simple ainsi qu’une règle de groupe de sécurité réseau, et installé un serveur web.</span><span class="sxs-lookup"><span data-stu-id="a60b8-139">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="a60b8-140">toolearn en savoir plus sur les machines virtuelles, continuer toohello didacticiel pour les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="a60b8-140">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>


> [!div class="nextstepaction"]
> [<span data-ttu-id="a60b8-141">Didacticiels sur les machines virtuelles Azure Linux</span><span class="sxs-lookup"><span data-stu-id="a60b8-141">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
