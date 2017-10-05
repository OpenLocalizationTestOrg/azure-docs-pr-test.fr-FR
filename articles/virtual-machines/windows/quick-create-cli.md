---
title: "Démarrage rapide avec Azure - Commande pour la création d’une machine virtuelle Windows | Microsoft Docs"
description: "Apprenez à créer rapidement des machines virtuelles Windows avec Azure CLI."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: fcb2f1389b3434d0d2e3145217e54ceb2326b969
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-windows-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="7eb5a-103">Créer une machine virtuelle Windows avec l’interface Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7eb5a-103">Create a Windows virtual machine with the Azure CLI</span></span>

<span data-ttu-id="7eb5a-104">L’interface de ligne de commande (CLI) Azure permet de créer et gérer des ressources Azure à partir de la ligne de commande ou dans les scripts.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="7eb5a-105">Ce guide détaille l’utilisation de l’interface de ligne de commande Azure pour le déploiement d’une machine virtuelle Azure exécutant Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-105">This guide details using the Azure CLI to deploy a virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="7eb5a-106">Une fois le déploiement terminé, connectez-vous au serveur et installez IIS.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-106">Once deployment is complete, we connect to the server and install IIS.</span></span>

<span data-ttu-id="7eb5a-107">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7eb5a-108">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0.4 ou une version ultérieure pour poursuivre la procédure décrite dans ce guide de démarrage rapide.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="7eb5a-109">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="7eb5a-110">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7eb5a-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="7eb5a-111">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="7eb5a-111">Create a resource group</span></span>

<span data-ttu-id="7eb5a-112">Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="7eb5a-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="7eb5a-113">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="7eb5a-114">L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* à l’emplacement *eastus*.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="7eb5a-115">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="7eb5a-115">Create virtual machine</span></span>

<span data-ttu-id="7eb5a-116">Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="7eb5a-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> 

<span data-ttu-id="7eb5a-117">L’exemple suivant permet de créer une machine virtuelle nommée *myVM*.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-117">The following example creates a VM named *myVM*.</span></span> <span data-ttu-id="7eb5a-118">Cet exemple utilise le nom d’utilisateur administratif *azureuser* et le mot de passe *myPassword12*.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-118">This example uses *azureuser* for an administrative user name and *myPassword12* as the password.</span></span> <span data-ttu-id="7eb5a-119">Mettez à jour ces valeurs avec quelque chose d’approprié pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-119">Update these values to something appropriate to your environment.</span></span> <span data-ttu-id="7eb5a-120">Ces valeurs sont nécessaires lors de la création d’une connexion avec la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-120">These values are needed when creating a connection with the virtual machine.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

<span data-ttu-id="7eb5a-121">Lorsque la machine virtuelle a été créée, l’interface de ligne de commande Azure affiche des informations similaires à l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-121">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="7eb5a-122">Notez la valeur de `publicIpAaddress`.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-122">Take note of the `publicIpAaddress`.</span></span> <span data-ttu-id="7eb5a-123">Cette adresse est utilisée pour accéder à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-123">This address is used to access the VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="7eb5a-124">Ouvrez le port 80 pour le trafic web</span><span class="sxs-lookup"><span data-stu-id="7eb5a-124">Open port 80 for web traffic</span></span> 

<span data-ttu-id="7eb5a-125">Par défaut, seules les connexions RDP sont autorisées pour les machines virtuelles Windows déployées dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-125">By default only RDP connections are allowed in to Windows virtual machines deployed in Azure.</span></span> <span data-ttu-id="7eb5a-126">Si cet ordinateur virtuel doit être un serveur web, vous devez ouvrir le port 80 à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-126">If this VM is going to be a webserver, you need to open port 80 from the Internet.</span></span> <span data-ttu-id="7eb5a-127">Utilisez la commande [az vm open-port](/cli/azure/vm#open-port) pour ouvrir le port souhaité.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-127">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-to-virtual-machine"></a><span data-ttu-id="7eb5a-128">Connexion à la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="7eb5a-128">Connect to virtual machine</span></span>

<span data-ttu-id="7eb5a-129">Utilisez la commande suivante pour créer une session Bureau à distance avec la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-129">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="7eb5a-130">Remplacez l’adresse IP par l’adresse IP publique de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-130">Replace the IP address with the public IP address of your virtual machine.</span></span> <span data-ttu-id="7eb5a-131">À l'invite, saisissez les informations d’identification que vous avez utilisées lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-131">When prompted, enter the credentials used when creating the virtual machine.</span></span>

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a><span data-ttu-id="7eb5a-132">Installation de IIS à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="7eb5a-132">Install IIS using PowerShell</span></span>

<span data-ttu-id="7eb5a-133">Maintenant que vous êtes connecté à la machine virtuelle Azure, vous pouvez utiliser une seule ligne de PowerShell pour installer IIS et activer la règle de pare-feu local pour autoriser le trafic web.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-133">Now that you have logged in to the Azure VM, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="7eb5a-134">Ouvrez une invite PowerShell et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7eb5a-134">Open a PowerShell prompt and run the following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="7eb5a-135">Afficher la page d’accueil IIS</span><span class="sxs-lookup"><span data-stu-id="7eb5a-135">View the IIS welcome page</span></span>

<span data-ttu-id="7eb5a-136">Une fois IIS installé et le port 80, ouvert sur votre machine virtuelle à partir d’Internet, vous pouvez utiliser un navigateur web pour afficher la page d’accueil IIS par défaut.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-136">With IIS installed and port 80 now open on your VM from the Internet, you can use a web browser of your choice to view the default IIS welcome page.</span></span> <span data-ttu-id="7eb5a-137">Veillez à utiliser l’adresse IP publique indiquée ci-dessus pour vous rendre sur la page par défaut.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-137">Be sure to use the public IP address you documented above to visit the default page.</span></span> 

![Site IIS par défaut](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="7eb5a-139">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="7eb5a-139">Clean up resources</span></span>

<span data-ttu-id="7eb5a-140">Lorsque vous n’en avez plus besoin, vous pouvez utiliser la commande [az group delete](/cli/azure/group#delete) pour supprimer le groupe de ressources, la machine virtuelle et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-140">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="7eb5a-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7eb5a-141">Next steps</span></span>

<span data-ttu-id="7eb5a-142">Dans ce guide de démarrage rapide, vous avez déployé une machine virtuelle simple ainsi qu’une règle de groupe de sécurité réseau, et installé un serveur web.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-142">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="7eb5a-143">Pour en savoir plus sur les machines virtuelles Azure, suivez le didacticiel pour les machines virtuelles Windows.</span><span class="sxs-lookup"><span data-stu-id="7eb5a-143">To learn more about Azure virtual machines, continue to the tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7eb5a-144">Didacticiels sur les machines virtuelles Azure Windows</span><span class="sxs-lookup"><span data-stu-id="7eb5a-144">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
