---
title: "Démarrage rapide avec Azure - Commande pour la création d’une machine virtuelle | Microsoft Docs"
description: "Apprenez à créer rapidement des machines virtuelles avec Azure CLI."
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
ms.openlocfilehash: a7cba5b2c43704d92e36d6f808efaa9fc73fdf36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="2c371-103">Créer une machine virtuelle Linux avec Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2c371-103">Create a Linux virtual machine with the Azure CLI</span></span>

<span data-ttu-id="2c371-104">L’interface de ligne de commande (CLI) Azure permet de créer et gérer des ressources Azure à partir de la ligne de commande ou dans les scripts.</span><span class="sxs-lookup"><span data-stu-id="2c371-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="2c371-105">Ce guide détaille l’utilisation de la CLI Azure pour le déploiement d’une machine virtuelle Azure exécutant Ubuntu Server.</span><span class="sxs-lookup"><span data-stu-id="2c371-105">This guide details using the Azure CLI to deploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="2c371-106">Une fois le serveur déployé, une connexion SSH est créée, et un serveur web NGINX est installé.</span><span class="sxs-lookup"><span data-stu-id="2c371-106">Once the server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="2c371-107">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="2c371-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2c371-108">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0.4 ou une version ultérieure pour poursuivre la procédure décrite dans ce guide de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="2c371-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="2c371-109">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="2c371-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="2c371-110">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2c371-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="2c371-111">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="2c371-111">Create a resource group</span></span>

<span data-ttu-id="2c371-112">Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="2c371-112">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="2c371-113">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="2c371-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="2c371-114">L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* à l’emplacement *eastus*.</span><span class="sxs-lookup"><span data-stu-id="2c371-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="2c371-115">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="2c371-115">Create virtual machine</span></span>

<span data-ttu-id="2c371-116">Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="2c371-116">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="2c371-117">L’exemple suivant crée une machine virtuelle nommée *myVM* et des clés SSH si elles n’existent pas déjà dans un emplacement de clé par défaut.</span><span class="sxs-lookup"><span data-stu-id="2c371-117">The following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="2c371-118">Pour utiliser un ensemble spécifique de clés, utilisez l’option `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="2c371-118">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="2c371-119">Lorsque la machine virtuelle a été créée, l’interface de ligne de commande Azure affiche des informations similaires à l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="2c371-119">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="2c371-120">Notez la valeur de `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="2c371-120">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="2c371-121">Cette adresse est utilisée pour accéder à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2c371-121">This address is used to access the VM.</span></span>

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

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="2c371-122">Ouvrez le port 80 pour le trafic web</span><span class="sxs-lookup"><span data-stu-id="2c371-122">Open port 80 for web traffic</span></span> 

<span data-ttu-id="2c371-123">Par défaut, seules les connexions SSH sont autorisées dans les machines virtuelles Linux déployées dans Azure.</span><span class="sxs-lookup"><span data-stu-id="2c371-123">By default only SSH connections are allowed into Linux virtual machines deployed in Azure.</span></span> <span data-ttu-id="2c371-124">Si cet ordinateur virtuel doit être un serveur web, vous devez ouvrir le port 80 à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="2c371-124">If this VM is going to be a webserver, you need to open port 80 from the Internet.</span></span> <span data-ttu-id="2c371-125">Utilisez la commande [az vm open-port](/cli/azure/vm#open-port) pour ouvrir le port souhaité.</span><span class="sxs-lookup"><span data-stu-id="2c371-125">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a><span data-ttu-id="2c371-126">Se connecter avec SSH à votre machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="2c371-126">SSH into your VM</span></span>

<span data-ttu-id="2c371-127">Utilisez la commande suivante pour créer une session SSH avec la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2c371-127">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="2c371-128">Veillez à remplacer *<publicIpAddress>* par l’adresse IP publique correcte de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2c371-128">Make sure to replace *<publicIpAddress>* with the correct public IP address of your virtual machine.</span></span>  <span data-ttu-id="2c371-129">Dans l’exemple ci-dessus, notre adresse IP était *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="2c371-129">In our example above our IP address was *40.68.254.142*.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a><span data-ttu-id="2c371-130">Installer NGINX</span><span class="sxs-lookup"><span data-stu-id="2c371-130">Install NGINX</span></span>

<span data-ttu-id="2c371-131">Utilisez le script Bash suivant pour mettre à jour les sources de package et installer le dernier package NGINX.</span><span class="sxs-lookup"><span data-stu-id="2c371-131">Use the following bash script to update package sources and install the latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-the-nginx-welcome-page"></a><span data-ttu-id="2c371-132">Afficher la page d’accueil NGINX</span><span class="sxs-lookup"><span data-stu-id="2c371-132">View the NGINX welcome page</span></span>

<span data-ttu-id="2c371-133">Une fois NGINX installé et le port 80 ouvert sur votre machine virtuelle à partir d’Internet, vous pouvez utiliser un navigateur web de votre choix pour afficher la page d’accueil NGINX par défaut.</span><span class="sxs-lookup"><span data-stu-id="2c371-133">With NGINX installed and port 80 now open on your VM from the Internet - you can use a web browser of your choice to view the default NGINX welcome page.</span></span> <span data-ttu-id="2c371-134">Veillez à utiliser la *publicIpAddress* indiquée ci-dessus pour vous rendre sur la page par défaut.</span><span class="sxs-lookup"><span data-stu-id="2c371-134">Be sure to use the *publicIpAddress* you documented above to visit the default page.</span></span> 

![Site par défaut NGINX](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a><span data-ttu-id="2c371-136">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="2c371-136">Clean up resources</span></span>

<span data-ttu-id="2c371-137">Lorsque vous n’en avez plus besoin, vous pouvez utiliser la commande [az group delete](/cli/azure/group#delete) pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="2c371-137">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="2c371-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2c371-138">Next steps</span></span>

<span data-ttu-id="2c371-139">Dans ce guide de démarrage rapide, vous avez déployé une machine virtuelle simple ainsi qu’une règle de groupe de sécurité réseau, et installé un serveur web.</span><span class="sxs-lookup"><span data-stu-id="2c371-139">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="2c371-140">Pour en savoir plus sur les machines virtuelles Azure, suivez le didacticiel pour les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="2c371-140">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span></span>


> [!div class="nextstepaction"]
> [<span data-ttu-id="2c371-141">Didacticiels sur les machines virtuelles Azure Linux</span><span class="sxs-lookup"><span data-stu-id="2c371-141">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
