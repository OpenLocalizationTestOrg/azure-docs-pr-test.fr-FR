---
title: "aaaAzure démarrage rapide : créer une CLI de machine virtuelle Windows | Documents Microsoft"
description: "En savoir plus rapidement toocreate des machines virtuelles Windows avec hello CLI d’Azure."
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
ms.openlocfilehash: 029bdecec219b12b80b958ceeedda214f1b13149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="b6d0a-103">Créer une machine virtuelle Windows avec hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="b6d0a-103">Create a Windows virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="b6d0a-104">Hello CLI d’Azure est utilisé toocreate et gérer des ressources Azure à partir de la ligne de commande hello ou dans des scripts.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="b6d0a-105">Ce guide décrit en détail à l’aide de hello CLI d’Azure toodeploy une machine virtuelle exécutant Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-105">This guide details using hello Azure CLI toodeploy a virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="b6d0a-106">Une fois le déploiement terminé, nous connecter toohello serveur et installez IIS.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-106">Once deployment is complete, we connect toohello server and install IIS.</span></span>

<span data-ttu-id="b6d0a-107">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b6d0a-108">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce démarrage rapide nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="b6d0a-109">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b6d0a-110">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b6d0a-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="b6d0a-111">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="b6d0a-111">Create a resource group</span></span>

<span data-ttu-id="b6d0a-112">Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="b6d0a-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="b6d0a-113">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="b6d0a-114">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-114">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="b6d0a-115">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="b6d0a-115">Create virtual machine</span></span>

<span data-ttu-id="b6d0a-116">Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="b6d0a-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> 

<span data-ttu-id="b6d0a-117">Hello exemple suivant crée un ordinateur virtuel nommé *myVM*.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-117">hello following example creates a VM named *myVM*.</span></span> <span data-ttu-id="b6d0a-118">Cet exemple utilise *azureuser* pour un nom d’utilisateur administratif et *myPassword12* comme mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-118">This example uses *azureuser* for an administrative user name and *myPassword12* as hello password.</span></span> <span data-ttu-id="b6d0a-119">Mettre à jour ces environnement tooyour approprié de toosomething valeurs.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-119">Update these values toosomething appropriate tooyour environment.</span></span> <span data-ttu-id="b6d0a-120">Ces valeurs sont nécessaires lors de la création d’une connexion avec l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-120">These values are needed when creating a connection with hello virtual machine.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

<span data-ttu-id="b6d0a-121">Lorsque hello machine virtuelle a été créé, hello CLI d’Azure affiche les informations toohello semblable l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-121">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="b6d0a-122">Prenez note de hello `publicIpAaddress`.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-122">Take note of hello `publicIpAaddress`.</span></span> <span data-ttu-id="b6d0a-123">Cette adresse est utilisée tooaccess hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-123">This address is used tooaccess hello VM.</span></span>

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

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="b6d0a-124">Ouvrez le port 80 pour le trafic web</span><span class="sxs-lookup"><span data-stu-id="b6d0a-124">Open port 80 for web traffic</span></span> 

<span data-ttu-id="b6d0a-125">Par défaut, seules les connexions RDP sont autorisées sur des machines virtuelles tooWindows déployés dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-125">By default only RDP connections are allowed in tooWindows virtual machines deployed in Azure.</span></span> <span data-ttu-id="b6d0a-126">Si cet ordinateur virtuel est toobe un serveur Web, vous devez tooopen port 80 de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-126">If this VM is going toobe a webserver, you need tooopen port 80 from hello Internet.</span></span> <span data-ttu-id="b6d0a-127">Hello d’utilisation [ouvrir un ordinateur virtuel az-port](/cli/azure/vm#open-port) commande tooopen hello souhaité de port.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-127">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="b6d0a-128">Connecter toovirtual machine</span><span class="sxs-lookup"><span data-stu-id="b6d0a-128">Connect toovirtual machine</span></span>

<span data-ttu-id="b6d0a-129">La commande suivante de hello utilisation toocreate une session Bureau à distance avec l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-129">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="b6d0a-130">Remplacer l’adresse IP de hello avec hello adresse IP publique de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-130">Replace hello IP address with hello public IP address of your virtual machine.</span></span> <span data-ttu-id="b6d0a-131">Lorsque vous y êtes invité, entrez les informations d’identification de l’hello utilisées lors de la création d’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-131">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a><span data-ttu-id="b6d0a-132">Installation de IIS à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6d0a-132">Install IIS using PowerShell</span></span>

<span data-ttu-id="b6d0a-133">Maintenant que vous êtes connecté toohello machine virtuelle Azure, vous pouvez utiliser une seule ligne de PowerShell tooinstall IIS et activer le trafic web tooallow hello pare-feu local règle.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-133">Now that you have logged in toohello Azure VM, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="b6d0a-134">Ouvrez une invite de PowerShell et exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b6d0a-134">Open a PowerShell prompt and run hello following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="b6d0a-135">Hello d’affichage page d’accueil IIS</span><span class="sxs-lookup"><span data-stu-id="b6d0a-135">View hello IIS welcome page</span></span>

<span data-ttu-id="b6d0a-136">Avec les services IIS sont installés et le port 80 maintenant ouvrir sur votre machine virtuelle à partir de hello Internet, vous pouvez utiliser un navigateur web de votre choix tooview hello par défaut IIS page d’accueil.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-136">With IIS installed and port 80 now open on your VM from hello Internet, you can use a web browser of your choice tooview hello default IIS welcome page.</span></span> <span data-ttu-id="b6d0a-137">Être vraiment toouse hello adresse IP publique vous documenté au-dessus de la page par défaut toovisit hello.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-137">Be sure toouse hello public IP address you documented above toovisit hello default page.</span></span> 

![Site IIS par défaut](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="b6d0a-139">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="b6d0a-139">Clean up resources</span></span>

<span data-ttu-id="b6d0a-140">Lorsque vous n’est plus nécessaire, vous pouvez utiliser hello [suppression du groupe az](/cli/azure/group#delete) groupe de ressources tooremove hello, machine virtuelle et toutes les ressources de la commande.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-140">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="b6d0a-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b6d0a-141">Next steps</span></span>

<span data-ttu-id="b6d0a-142">Dans ce guide de démarrage rapide, vous avez déployé une machine virtuelle simple ainsi qu’une règle de groupe de sécurité réseau, et installé un serveur web.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-142">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="b6d0a-143">toolearn en savoir plus sur les machines virtuelles, continuer toohello didacticiel pour les machines virtuelles Windows.</span><span class="sxs-lookup"><span data-stu-id="b6d0a-143">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b6d0a-144">Didacticiels sur les machines virtuelles Azure Windows</span><span class="sxs-lookup"><span data-stu-id="b6d0a-144">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
