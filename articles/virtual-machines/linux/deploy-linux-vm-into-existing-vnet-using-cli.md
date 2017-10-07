---
title: "aaaDeploy les machines virtuelles Linux sur un réseau existant avec Azure CLI 2.0 | Documents Microsoft"
description: "Découvrez comment une machine virtuelle de Linux dans un réseau virtuel existant à l’aide de toodeploy hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0df44b3437002df050db56f3b3899083fb49d803
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli"></a><span data-ttu-id="93c18-103">Comment toodeploy une machine virtuelle de Linux dans un réseau virtuel Azure existant avec hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="93c18-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure CLI</span></span>

<span data-ttu-id="93c18-104">Cet article vous montre comment toouse hello Azure CLI 2.0 toodeploy un ordinateur virtuel (VM) dans un réseau virtuel existant.</span><span class="sxs-lookup"><span data-stu-id="93c18-104">This article shows you how toouse hello Azure CLI 2.0 toodeploy a virtual machine (VM) into an existing virtual network.</span></span> <span data-ttu-id="93c18-105">spécifications de Hello sont :</span><span class="sxs-lookup"><span data-stu-id="93c18-105">hello requirements are:</span></span>

- [<span data-ttu-id="93c18-106">un compte Azure</span><span class="sxs-lookup"><span data-stu-id="93c18-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="93c18-107">des fichiers de clés SSH publiques et privées</span><span class="sxs-lookup"><span data-stu-id="93c18-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

<span data-ttu-id="93c18-108">Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="93c18-108">You can also perform these steps with hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="93c18-109">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="93c18-109">Quick Commands</span></span>
<span data-ttu-id="93c18-110">Si vous avez besoin de tooquickly accomplir la tâche hello, hello suivant la section Détails des commandes hello nécessaires.</span><span class="sxs-lookup"><span data-stu-id="93c18-110">If you need tooquickly accomplish hello task, hello following section details hello  commands needed.</span></span> <span data-ttu-id="93c18-111">Plus d’informations et le contexte de chaque étape se trouve reste hello du document de hello, [Démarrer ici](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="93c18-111">More detailed information and context for each step can be found hello rest of hello document, [starting here](#detailed-walkthrough).</span></span>

<span data-ttu-id="93c18-112">toocreate cet environnement personnalisé, vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="93c18-112">toocreate this custom environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="93c18-113">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="93c18-113">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="93c18-114">Les noms de paramètre sont par exemple *myResourceGroup*, *myVnet* et *myVM*.</span><span class="sxs-lookup"><span data-stu-id="93c18-114">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

<span data-ttu-id="93c18-115">**Conditions préalables :** groupe de ressources Azure, réseau virtuel et sous-réseau, groupe de sécurité réseau avec SSH entrant et une carte d’interface réseau virtuelle.</span><span class="sxs-lookup"><span data-stu-id="93c18-115">**Pre-requirements:** Azure resource group, virtual network and subnet, network security group with SSH inbound, and a virtual network interface card.</span></span>

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="93c18-116">Déployer hello VM dans l’infrastructure de réseau virtuel hello</span><span class="sxs-lookup"><span data-stu-id="93c18-116">Deploy hello VM into hello virtual network infrastructure</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="93c18-117">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="93c18-117">Detailed walkthrough</span></span>

<span data-ttu-id="93c18-118">Les ressources Azure telles que les réseaux virtuels et les groupes de sécurité réseau doivent être des ressources statiques et durables qui sont rarement déployées.</span><span class="sxs-lookup"><span data-stu-id="93c18-118">Azure assets like virtual networks and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="93c18-119">Une fois qu’un réseau virtuel a été déployé, il peut être réutilisé par nouveaux déploiements sans n’importe quelle infrastructure de toohello répercussions négatives.</span><span class="sxs-lookup"><span data-stu-id="93c18-119">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="93c18-120">Réfléchissez à un réseau virtuel comme étant un commutateur de réseau traditionnels matériel - vous ne devez pas tooconfigure basculer d’un nouveau matériel à chaque déploiement.</span><span class="sxs-lookup"><span data-stu-id="93c18-120">Think about a virtual network as being a traditional hardware network switch - you would not need tooconfigure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="93c18-121">Avec un réseau virtuel configuré correctement, vous pouvez continuer toodeploy nouvelles machines virtuelles dans ce réseau virtuel plusieurs fois avec peu, le cas échéant, modifications requises pendant toute la durée du réseau virtuel de hello hello.</span><span class="sxs-lookup"><span data-stu-id="93c18-121">With a correctly configured virtual network, you can continue toodeploy new VMs into that virtual network over and over with few, if any, changes required over hello life of hello virtual network.</span></span>

<span data-ttu-id="93c18-122">toocreate cet environnement personnalisé, vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="93c18-122">toocreate this custom environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="93c18-123">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="93c18-123">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="93c18-124">Les noms de paramètre sont par exemple *myResourceGroup*, *myVnet* et *myVM*.</span><span class="sxs-lookup"><span data-stu-id="93c18-124">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="93c18-125">Créer le groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="93c18-125">Create hello resource group</span></span>

<span data-ttu-id="93c18-126">Commencez par créer un tooorganize de groupe de ressources Azure tout ce que vous créez dans cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="93c18-126">First, create an Azure resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="93c18-127">Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="93c18-127">For more information on resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="93c18-128">Créer le groupe de ressources hello avec [az groupe créer](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="93c18-128">Create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="93c18-129">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="93c18-129">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-hello-virtual-network"></a><span data-ttu-id="93c18-130">Créer le réseau virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="93c18-130">Create hello virtual network</span></span>

<span data-ttu-id="93c18-131">Permet de créer des machines virtuelles dans un hello toolaunch de réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="93c18-131">Lets build an Azure virtual network toolaunch hello VMs into.</span></span> <span data-ttu-id="93c18-132">Pour plus d’informations sur les réseaux virtuels, consultez [créer un réseau virtuel à l’aide de hello CLI d’Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="93c18-132">For more information on virtual networks, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md).</span></span> <span data-ttu-id="93c18-133">Créer le réseau virtuel hello [créer un réseau virtuel du réseau az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="93c18-133">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="93c18-134">Hello exemple suivant crée un réseau virtuel nommé *myVnet* et sous-réseau nommé *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="93c18-134">hello following example creates a virtual network named *myVnet* and subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="93c18-135">Créer un groupe de sécurité réseau hello</span><span class="sxs-lookup"><span data-stu-id="93c18-135">Create hello network security group</span></span>

<span data-ttu-id="93c18-136">Groupes de sécurité réseau Azure sont pare-feu tooa équivalente à la couche réseau hello.</span><span class="sxs-lookup"><span data-stu-id="93c18-136">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="93c18-137">Pour plus d’informations sur les groupes de sécurité réseau, consultez [comment les groupes de sécurité de réseau toocreate Bonjour Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="93c18-137">For more information on network security groups, see [How toocreate network security groups in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span> <span data-ttu-id="93c18-138">Créer le groupe de sécurité réseau hello avec [az réseau nsg créer](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="93c18-138">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="93c18-139">Hello exemple suivant crée un groupe de sécurité réseau nommé *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="93c18-139">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="93c18-140">Ajouter une règle d’autorisation SSH entrante</span><span class="sxs-lookup"><span data-stu-id="93c18-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="93c18-141">Hello machine virtuelle a besoin d’accéder à partir de hello internet, pour une règle autorisant le port entrant 22 trafic toobe transmises via le réseau de hello tooport 22 sur hello machine virtuelle est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="93c18-141">hello VM needs access from hello internet, so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is needed.</span></span> <span data-ttu-id="93c18-142">Ajouter une règle de trafic entrant pour le groupe de sécurité réseau hello avec [créer de règle de groupe de sécurité réseau du réseau az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="93c18-142">Add an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="93c18-143">Hello exemple suivant crée une règle nommée *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="93c18-143">hello following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-hello-subnet-toohello-network-security-group"></a><span data-ttu-id="93c18-144">Joindre le groupe de sécurité réseau hello sous-réseau toohello</span><span class="sxs-lookup"><span data-stu-id="93c18-144">Attach hello subnet toohello network security group</span></span>

<span data-ttu-id="93c18-145">règles de groupe de sécurité réseau Hello peuvent être appliqué tooa sous-réseau ou une interface de réseau virtuel spécifique.</span><span class="sxs-lookup"><span data-stu-id="93c18-145">hello network security group rules can be applied tooa subnet or a specific virtual network interface.</span></span> <span data-ttu-id="93c18-146">Permet d’attacher le sous-réseau tooour du groupe de sécurité hello réseau.</span><span class="sxs-lookup"><span data-stu-id="93c18-146">Lets attach hello network security group tooour subnet.</span></span> <span data-ttu-id="93c18-147">Attacher votre groupe de sécurité réseau de sous-réseau toohello avec [mise à jour de sous-réseau de réseau virtuel az réseau](/cli/azure/network/vnet/subnet#update):</span><span class="sxs-lookup"><span data-stu-id="93c18-147">Attach your subnet toohello network security group with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update):</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-toohello-subnet"></a><span data-ttu-id="93c18-148">Ajouter un sous-réseau de réseau virtuel interface carte toohello</span><span class="sxs-lookup"><span data-stu-id="93c18-148">Add a virtual network interface card toohello subnet</span></span>

<span data-ttu-id="93c18-149">Cartes d’interface réseau virtuelle (cartes réseau) sont importantes que vous puissiez les réutiliser en connectant les machines virtuelles de toodifferent.</span><span class="sxs-lookup"><span data-stu-id="93c18-149">Virtual network interface cards (VNics) are important as you can reuse them by connecting them toodifferent VMs.</span></span> <span data-ttu-id="93c18-150">Cette réutilisation permet tookeep hello VNic comme une ressource statique tandis que hello machines virtuelles peut être temporaire.</span><span class="sxs-lookup"><span data-stu-id="93c18-150">This reuse allows you tookeep hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="93c18-151">Créer une carte réseau virtuelle et l’associer à sous-réseau hello avec [créer des cartes réseau du réseau az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="93c18-151">Create a VNic and associate it with hello subnet with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="93c18-152">Hello exemple suivant crée une carte réseau virtuelle nommée *myNic*:</span><span class="sxs-lookup"><span data-stu-id="93c18-152">hello following example creates a VNic named *myNic*:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="93c18-153">Déployer hello VM dans l’infrastructure de réseau virtuel hello</span><span class="sxs-lookup"><span data-stu-id="93c18-153">Deploy hello VM into hello virtual network infrastructure</span></span>

<span data-ttu-id="93c18-154">Vous avez maintenant un réseau virtuel et sous-réseau et un sous-réseau hello tooprotect de groupe de sécurité réseau en bloquant tout le trafic entrant, à l’exception de port 22 pour SSH.</span><span class="sxs-lookup"><span data-stu-id="93c18-154">You now have a virtual network and subnet, and a network security group tooprotect hello subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="93c18-155">Hello machine virtuelle peut désormais être déployé à l’intérieur de cette infrastructure réseau existante.</span><span class="sxs-lookup"><span data-stu-id="93c18-155">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="93c18-156">Créez votre machine virtuelle avec [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="93c18-156">Create your VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="93c18-157">Pour plus d’informations sur hello indicateurs toouse avec hello Azure CLI 2.0 toodeploy une machine virtuelle complète, consultez [créer un environnement complet de Linux à l’aide de hello CLI d’Azure](create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="93c18-157">For more information on hello flags toouse with hello Azure CLI 2.0 toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md).</span></span>

<span data-ttu-id="93c18-158">Bonjour à l’exemple suivant crée une machine virtuelle à l’aide de disques gérés d’Azure.</span><span class="sxs-lookup"><span data-stu-id="93c18-158">hello following example creates a VM using Azure Managed Disks.</span></span> <span data-ttu-id="93c18-159">Ces disques sont gérées par hello plateforme Azure et ne nécessitent pas de n’importe quel toostore préparation ou emplacement les.</span><span class="sxs-lookup"><span data-stu-id="93c18-159">These disks are handled by hello Azure platform and do not require any preparation or location toostore them.</span></span> <span data-ttu-id="93c18-160">Pour plus d’informations sur les disques gérés, consultez [Vue d’ensemble d’Azure Managed Disks](../../storage/storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="93c18-160">For more information about managed disks, see [Azure Managed Disks overview](../../storage/storage-managed-disks-overview.md).</span></span> <span data-ttu-id="93c18-161">Si vous souhaitez les disques toouse non managée, consultez hello supplémentaires Remarque ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="93c18-161">If you wish toouse unmanaged disks, see hello additional note below.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

<span data-ttu-id="93c18-162">Si vous utilisez des disques gérés, ignorez cette étape.</span><span class="sxs-lookup"><span data-stu-id="93c18-162">If you use managed disks, skip this step.</span></span> <span data-ttu-id="93c18-163">Si vous souhaitez les disques toouse non managée, vous devez hello tooadd des paramètres supplémentaires toohello passer commande toocreate non managée disques dans le compte de stockage hello nommé suivants `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="93c18-163">If you wish toouse unmanaged disks, you need tooadd hello following additional parameters toohello proceeding command toocreate unmanaged disks in hello storage account named `mystorageaccount`:</span></span> 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

<span data-ttu-id="93c18-164">À l’aide de hello CLI indicateurs toocall les ressources existantes, vous indiquez à Azure toodeploy hello machine virtuelle à l’intérieur du réseau existant de hello.</span><span class="sxs-lookup"><span data-stu-id="93c18-164">By using hello CLI flags toocall out existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="93c18-165">Lorsqu’un réseau virtuel et un sous-réseau ont été déployés, ils peuvent être conservés en tant que ressources statiques ou permanentes à l’intérieur de votre région Azure.</span><span class="sxs-lookup"><span data-stu-id="93c18-165">Once a virtual network and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span> <span data-ttu-id="93c18-166">Dans cet exemple, vous ne pas créer et affecter un toohello d’adresse publique IP VNic, cet ordinateur virtuel n’est pas accessible publiquement sur Internet de hello.</span><span class="sxs-lookup"><span data-stu-id="93c18-166">In this example, you did not create and assign a public IP address toohello VNic, so this VM is not publicly accessible over hello Internet.</span></span> <span data-ttu-id="93c18-167">Pour plus d’informations, consultez [créer une machine virtuelle avec une adresse IP publique statique à l’aide de hello CLI d’Azure](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="93c18-167">For more information, see [Create a VM with a static public IP using hello Azure CLI](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="93c18-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="93c18-168">Next steps</span></span>
<span data-ttu-id="93c18-169">Pour plus d’informations sur les machines virtuelles toocreate manières dans Azure, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="93c18-169">For more information about ways toocreate virtual machines in Azure, see hello following resources:</span></span>

* [<span data-ttu-id="93c18-170">Utilisez un toocreate de modèle Azure Resource Manager un déploiement spécifique</span><span class="sxs-lookup"><span data-stu-id="93c18-170">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="93c18-171">Créer votre propre environnement personnalisé pour une machine virtuelle Linux à l’aide des commandes de l’interface de ligne de commande Azure directement</span><span class="sxs-lookup"><span data-stu-id="93c18-171">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="93c18-172">Création d’une machine virtuelle Linux sur Azure à l’aide de modèles</span><span class="sxs-lookup"><span data-stu-id="93c18-172">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
