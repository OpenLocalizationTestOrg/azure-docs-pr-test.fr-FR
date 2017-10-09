---
title: "aaaAvailability définit le didacticiel pour les machines virtuelles Linux dans Azure | Documents Microsoft"
description: "Découvrez hello haute disponibilité pour les machines virtuelles Linux dans Azure."
documentationcenter: 
services: virtual-machines-linux
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 2a91e4a6057180035ec51410d9fffccaca343758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="1e01d-103">Comment à haute disponibilité de toouse</span><span class="sxs-lookup"><span data-stu-id="1e01d-103">How toouse availability sets</span></span>


<span data-ttu-id="1e01d-104">Dans ce didacticiel, vous allez apprendre comment la disponibilité de hello tooincrease et la fiabilité de vos solutions d’ordinateur virtuel sur Azure à l’aide d’une fonctionnalité appelée haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="1e01d-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="1e01d-105">Haute disponibilité vous assurer que hello machines virtuelles que vous déployez sur Azure sont réparties entre plusieurs clusters matérielles isolées.</span><span class="sxs-lookup"><span data-stu-id="1e01d-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="1e01d-106">Cela garantit que si une défaillance matérielle ou logicielle dans Azure se produit, qu’un ensemble sous-chemin de vos machines virtuelles est concerné et que votre solution globale resteront disponibles et opérationnels du point de vue hello de vos clients à l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="1e01d-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span>

<span data-ttu-id="1e01d-107">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="1e01d-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1e01d-108">Créer un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="1e01d-108">Create an availability set</span></span>
> * <span data-ttu-id="1e01d-109">Créer une machine virtuelle dans un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="1e01d-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="1e01d-110">Vérifier les tailles de machines virtuelles disponibles</span><span class="sxs-lookup"><span data-stu-id="1e01d-110">Check available VM sizes</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1e01d-111">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1e01d-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="1e01d-112">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="1e01d-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1e01d-113">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1e01d-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="availability-set-overview"></a><span data-ttu-id="1e01d-114">Vue d’ensemble des groupes à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="1e01d-114">Availability set overview</span></span>

<span data-ttu-id="1e01d-115">Un ensemble de disponibilité d’est une fonctionnalité de regroupement logique que vous pouvez utiliser dans Azure tooensure que les ressources de machine virtuelle de hello que vous placez qu’il contient sont isolées des autres lorsqu’ils sont déployés dans un centre de données Azure.</span><span class="sxs-lookup"><span data-stu-id="1e01d-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="1e01d-116">Azure garantit que machines virtuelles que vous placez dans un ensemble de disponibilité s’exécuter sur plusieurs serveurs physiques hello, le calcul des racks, les unités de stockage et les commutateurs de réseau.</span><span class="sxs-lookup"><span data-stu-id="1e01d-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="1e01d-117">Cela garantit que dans le cas de hello d’un problème matériel ou logiciel d’Azure, uniquement un sous-ensemble de vos machines virtuelles est affecté, et continuer à et continuer toobe disponible tooyour clients de votre application globale.</span><span class="sxs-lookup"><span data-stu-id="1e01d-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="1e01d-118">À l’aide de la haute disponibilité est une fonctionnalité essentielle de tooleverage toobuild les solutions de cloud fiable.</span><span class="sxs-lookup"><span data-stu-id="1e01d-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="1e01d-119">Prenons l’exemple d’une solution basée sur une machine virtuelle classique dans laquelle vous disposez de 4 serveurs web frontaux et utilisez 2 machines virtuelles principales hébergeant une base de données.</span><span class="sxs-lookup"><span data-stu-id="1e01d-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="1e01d-120">Avec Azure, vous souhaiteriez toodefine deux groupes à haute disponibilité avant de déployer vos machines virtuelles : une disponibilité définie pour le niveau de « web » hello et une haute disponibilité pour le niveau de « base de données » hello.</span><span class="sxs-lookup"><span data-stu-id="1e01d-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="1e01d-121">Lorsque vous créez une nouvelle machine virtuelle que vous pouvez ensuite spécifier hello groupe à haute disponibilité comme une machine virtuelle de paramètre toohello az Créer commande et Azure automatiquement garantit que machines virtuelles que vous créez au sein de hello disponible hello ensemble sont isolés sur plusieurs ressources de matériel physique.</span><span class="sxs-lookup"><span data-stu-id="1e01d-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="1e01d-122">Cela signifie que si le matériel physique hello que votre serveur Web ou les machines virtuelles de serveur de base de données est en cours d’exécution sur a un problème, vous savez que hello autres instances de votre serveur Web et les machines virtuelles de base de données reste en cours d’exécution correctement, car ils sont sur un matériel différent.</span><span class="sxs-lookup"><span data-stu-id="1e01d-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="1e01d-123">Vous devez toujours utiliser des ensembles de disponibilité lorsque vous souhaitez toodeploy basée sur des ordinateurs virtuels des solutions fiables dans Azure.</span><span class="sxs-lookup"><span data-stu-id="1e01d-123">You should always use Availability Sets when you want toodeploy reliable VM-based solutions within Azure.</span></span>


## <a name="create-an-availability-set"></a><span data-ttu-id="1e01d-124">Créer un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="1e01d-124">Create an availability set</span></span>

<span data-ttu-id="1e01d-125">Vous pouvez créer un groupe à haute disponibilité à l’aide de la commande [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="1e01d-125">You can create an availability set using [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="1e01d-126">Dans cet exemple, nous avons défini à la fois nombre hello domaines de mise à jour et d’erreur à *2* pour hello groupe à haute disponibilité nommée *myAvailabilitySet* Bonjour *myResourceGroupAvailability*groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1e01d-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="1e01d-127">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="1e01d-127">Create a resource group.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAvailability --location eastus
```


```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupAvailability \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

<span data-ttu-id="1e01d-128">Haute disponibilité permettre de tooisolate ressources entre domaines d’erreur « » et « domaines de mise à jour ».</span><span class="sxs-lookup"><span data-stu-id="1e01d-128">Availability Sets allow you tooisolate resources across "fault domains" and "update domains".</span></span> <span data-ttu-id="1e01d-129">Un **domaine d’erreur** représente une collection isolée comportant un serveur, un réseau et des ressources de stockage.</span><span class="sxs-lookup"><span data-stu-id="1e01d-129">A **fault domain** represents an isolated collection of server + network + storage resources.</span></span> <span data-ttu-id="1e01d-130">Bonjour précédent exemple, nous indiquent que nous souhaitons que notre disponibilité définie toobe distribué sur au moins deux domaines d’erreur lors de notre machines virtuelles sont déployées.</span><span class="sxs-lookup"><span data-stu-id="1e01d-130">In hello preceding example, we indicate that we want our availability set toobe distributed across at least two fault domains when our VMs are deployed.</span></span> <span data-ttu-id="1e01d-131">Nous indiquons également que nous souhaitons que notre groupe à haute disponibilité soit réparti sur deux **domaines de mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="1e01d-131">We also indicate that we want our availability set distributed across two **update domains**.</span></span>  <span data-ttu-id="1e01d-132">Deux domaines de mise à jour respectent lorsque Azure effectue des mises à jour logicielles nos ressources d’ordinateur virtuel isolés, ce qui empêche tous les logiciels hello en cours d’exécution en dessous de la machine virtuelle à partir de la mise à jour à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="1e01d-132">Two update domains ensure that when Azure performs software updates our VM resources are isolated, preventing all hello software running underneath our VM from being updated at hello same time.</span></span>

## <a name="configure-virtual-network"></a><span data-ttu-id="1e01d-133">Configurer un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="1e01d-133">Configure virtual network</span></span>
<span data-ttu-id="1e01d-134">Avant de déployer des machines virtuelles et tester votre programme d’équilibrage, créer hello prenant en charge des ressources du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="1e01d-134">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="1e01d-135">Pour plus d’informations sur les réseaux virtuels, consultez hello [gérer les réseaux virtuels Azure](tutorial-virtual-network.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="1e01d-135">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="1e01d-136">Créer des ressources réseau</span><span class="sxs-lookup"><span data-stu-id="1e01d-136">Create network resources</span></span>
<span data-ttu-id="1e01d-137">Créez un réseau virtuel avec la commande [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="1e01d-137">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="1e01d-138">Hello exemple suivant crée un réseau virtuel nommé *myVnet* avec un sous-réseau nommé *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="1e01d-138">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
<span data-ttu-id="1e01d-139">Les cartes d’interface réseau virtuelles sont créées avec la commande [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="1e01d-139">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="1e01d-140">Hello exemple suivant crée trois cartes réseau virtuelles.</span><span class="sxs-lookup"><span data-stu-id="1e01d-140">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="1e01d-141">(Une carte réseau virtuelle pour chaque ordinateur virtuel que vous créez pour votre application Bonjour suivant les étapes).</span><span class="sxs-lookup"><span data-stu-id="1e01d-141">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="1e01d-142">Vous pouvez créer des cartes réseau virtuelles supplémentaires et des machines virtuelles à tout moment et ajoutez-les à équilibrage de charge toohello :</span><span class="sxs-lookup"><span data-stu-id="1e01d-142">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupAvailability \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="1e01d-143">Créer des machines virtuelles dans un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="1e01d-143">Create VMs inside an availability set</span></span>

<span data-ttu-id="1e01d-144">Machines virtuelles doivent être créées dans hello disponibilité ensemble toomake qu’ils sont correctement distribués sur les matériels hello.</span><span class="sxs-lookup"><span data-stu-id="1e01d-144">VMs must be created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="1e01d-145">Vous ne pouvez pas ajouter un groupe de machines virtuelles tooan disponibilité définie après sa création.</span><span class="sxs-lookup"><span data-stu-id="1e01d-145">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="1e01d-146">Lorsque vous créez une machine virtuelle à l’aide de [az vm créer](/cli/azure/vm#create) vous spécifiez hello haute disponibilité via hello `--availability-set` toospecify hello nom hello à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="1e01d-146">When you create a VM using [az vm create](/cli/azure/vm#create) you specify hello availability set using hello `--availability-set` parameter toospecify hello name of hello availability set.</span></span>

```azurecli-interactive 
for i in `seq 1 2`; do
   az vm create \
     --resource-group myResourceGroupAvailability \
     --name myVM$i \
     --availability-set myAvailabilitySet \
     --nics myNic$i \
     --size Standard_DS1_v2  \
     --image Canonical:UbuntuServer:14.04.4-LTS:latest \
     --admin-username azureuser \
     --generate-ssh-keys \
     --no-wait
done 
```

<span data-ttu-id="1e01d-147">Nous avons à présent deux machines virtuelles à l’intérieur du groupe à haute disponibilité que nous venons de créer.</span><span class="sxs-lookup"><span data-stu-id="1e01d-147">We now have two virtual machines within our newly created availability set.</span></span> <span data-ttu-id="1e01d-148">Parce qu’elles sont hello même groupe à haute disponibilité, Azure garantit que machines virtuelles hello et toutes leurs ressources (y compris les disques de données) sont distribués sur un matériel physique isolé.</span><span class="sxs-lookup"><span data-stu-id="1e01d-148">Because they are in hello same availability set, Azure will ensure that hello VMs and all their resources (including data disks) are distributed across isolated physical hardware.</span></span> <span data-ttu-id="1e01d-149">Cette distribution contribue à assurer une disponibilité sensiblement plus importante de notre solution globale de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1e01d-149">This distribution helps ensure much higher availability of our overall VM solution.</span></span>

<span data-ttu-id="1e01d-150">Une chose que vous pouvez rencontrer lorsque vous ajoutez des machines virtuelles est qu’une taille de machine virtuelle particulière n’est plus disponible toouse au sein de votre jeu de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="1e01d-150">One thing you may encounter as you add VMs is that a particular VM size is no longer available toouse within your availability set.</span></span> <span data-ttu-id="1e01d-151">Ce problème peut se produire si il n’est plus suffisamment tooadd capacité il tout en préservant la haute disponibilité de hello isolation règles hello impose.</span><span class="sxs-lookup"><span data-stu-id="1e01d-151">This issue can happen if there is no longer enough capacity tooadd it while preserving hello isolation rules hello availability set enforces.</span></span> <span data-ttu-id="1e01d-152">Vous pouvez vérifier toosee les tailles de machine virtuelle sont toouse disponible au sein d’un groupe de disponibilité à l’aide de hello `--availability-set list-sizes` paramètre.</span><span class="sxs-lookup"><span data-stu-id="1e01d-152">You can check toosee what VM sizes are available toouse within an existing availability set using hello `--availability-set list-sizes` parameter.</span></span>

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="1e01d-153">Vérifier les tailles de machines virtuelles disponibles</span><span class="sxs-lookup"><span data-stu-id="1e01d-153">Check for available VM sizes</span></span> 

<span data-ttu-id="1e01d-154">Vous pouvez ajouter plusieurs machines virtuelles toohello haute disponibilité plus tard, mais vous devez tooknow les tailles de machine virtuelle sont disponibles sur le matériel de hello.</span><span class="sxs-lookup"><span data-stu-id="1e01d-154">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="1e01d-155">Utilisez [az vm disponibilité liste-taille](/cli/azure/availability-set#list-sizes) toolist toutes les tailles disponibles hello sur du matériel de hello du cluster pour hello à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="1e01d-155">Use [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a><span data-ttu-id="1e01d-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1e01d-156">Next steps</span></span>

<span data-ttu-id="1e01d-157">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="1e01d-157">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1e01d-158">Créer un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="1e01d-158">Create an availability set</span></span>
> * <span data-ttu-id="1e01d-159">Créer une machine virtuelle dans un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="1e01d-159">Create a VM in an availability set</span></span>
> * <span data-ttu-id="1e01d-160">Vérifier les tailles de machines virtuelles disponibles</span><span class="sxs-lookup"><span data-stu-id="1e01d-160">Check available VM sizes</span></span>

<span data-ttu-id="1e01d-161">Avance toohello toolearn de didacticiel suivant sur les machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="1e01d-161">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1e01d-162">Créer un groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="1e01d-162">Create a VM scale set</span></span>](tutorial-create-vmss.md)

