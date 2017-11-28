---
title: "aaaUsing la résolution sur Azure de noms DNS internes pour la machine virtuelle | Documents Microsoft"
description: "Utilisation de DNS interne pour la résolution de noms de machines virtuelles dans Azure."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: 94fd6577aa51ce5db4dc26649b415ddeeb410eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="bd53d-103">Utilisation de DNS interne pour la résolution de noms de machines virtuelles dans Azure</span><span class="sxs-lookup"><span data-stu-id="bd53d-103">Using internal DNS for VM name resolution on Azure</span></span>

<span data-ttu-id="bd53d-104">Cet article explique comment tooset DNS interne statique des noms pour les machines virtuelles Linux à l’aide de cartes d’interface réseau virtuelle (VNic) et les noms DNS en une partie.</span><span class="sxs-lookup"><span data-stu-id="bd53d-104">This article shows how tooset static internal DNS names for Linux VMs using Virtual NIC cards (VNic) and DNS label names.</span></span> <span data-ttu-id="bd53d-105">Les noms DNS statiques sont utilisés pour les services d’infrastructure permanents comme un serveur de builds Jenkins, qui est utilisé pour ce document, ou un serveur Git.</span><span class="sxs-lookup"><span data-stu-id="bd53d-105">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="bd53d-106">spécifications de Hello sont :</span><span class="sxs-lookup"><span data-stu-id="bd53d-106">hello requirements are:</span></span>

* [<span data-ttu-id="bd53d-107">un compte Azure</span><span class="sxs-lookup"><span data-stu-id="bd53d-107">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="bd53d-108">des fichiers de clés SSH publiques et privées</span><span class="sxs-lookup"><span data-stu-id="bd53d-108">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="bd53d-109">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="bd53d-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="bd53d-110">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="bd53d-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="bd53d-111">[Azure CLI 1.0](#quick-commands) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="bd53d-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="bd53d-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="bd53d-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="bd53d-113">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="bd53d-113">Quick commands</span></span>

<span data-ttu-id="bd53d-114">Si vous avez besoin de tooquickly accomplir la tâche hello, hello suivant la section Détails des commandes hello nécessaires.</span><span class="sxs-lookup"><span data-stu-id="bd53d-114">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="bd53d-115">Plus d’informations et le contexte de chaque étape se trouve reste hello du document de hello, [Démarrer ici](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="bd53d-115">More detailed information and context for each step can be found hello rest of hello document, [starting here](#detailed-walkthrough).</span></span>  

<span data-ttu-id="bd53d-116">Configuration requise : groupe de ressources, réseau virtuel, groupe de sécurité réseau avec SSH entrant, sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="bd53d-116">Pre-Requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span>

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a><span data-ttu-id="bd53d-117">Créer une carte réseau virtuelle avec un nom DNS interne statique</span><span class="sxs-lookup"><span data-stu-id="bd53d-117">Create a VNic with a static internal DNS name</span></span>

<span data-ttu-id="bd53d-118">Hello `-r` cli indicateur est pour le nom DNS paramètre hello, qui fournit un nom DNS statique hello pour hello une carte réseau virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bd53d-118">hello `-r` cli flag is for setting hello DNS label, which provides hello static DNS name for hello VNic.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-hello-vm-into-hello-vnet-nsg-and-connect-hello-vnic"></a><span data-ttu-id="bd53d-119">Déployer la machine virtuelle de hello en hello réseau virtuel, le groupe de sécurité réseau et, à connecter hello VNic</span><span class="sxs-lookup"><span data-stu-id="bd53d-119">Deploy hello VM into hello VNet, NSG and, connect hello VNic</span></span>

<span data-ttu-id="bd53d-120">Hello `-N` se connecte hello VNic toohello nouvelle machine virtuelle pendant hello déploiement tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bd53d-120">hello `-N` connects hello VNic toohello new VM during hello deployment tooAzure.</span></span>

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="bd53d-121">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="bd53d-121">Detailed walkthrough</span></span>

<span data-ttu-id="bd53d-122">Une intégration complète continue et un déploiement continu (CiCd) une infrastructure sur Azure requiert certains serveurs de toobe serveurs statique ou à long terme.</span><span class="sxs-lookup"><span data-stu-id="bd53d-122">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers toobe static or long-lived servers.</span></span>  <span data-ttu-id="bd53d-123">Il est recommandé que les ressources Azure telles que hello de réseaux virtuels (réseaux virtuels) et les groupes de sécurité réseau (NSG), doit être statiques et longue durée de vie ressources qui sont rarement déployées.</span><span class="sxs-lookup"><span data-stu-id="bd53d-123">It is recommended that Azure assets like hello Virtual Networks (VNets) and Network Security Groups (NSGs), should be static and long lived resources that are rarely deployed.</span></span>  <span data-ttu-id="bd53d-124">Une fois qu’un réseau virtuel a été déployé, il peut être réutilisé par nouveaux déploiements sans n’importe quelle infrastructure de toohello répercussions négatives.</span><span class="sxs-lookup"><span data-stu-id="bd53d-124">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span>  <span data-ttu-id="bd53d-125">Ajout de réseau statique de toothis un Git serveur de référentiel et un serveur automation de Jenkins remet CiCd tooyour les environnements de développement ou de test.</span><span class="sxs-lookup"><span data-stu-id="bd53d-125">Adding toothis static network a Git repository server and a Jenkins automation server delivers CiCd tooyour development or test environments.</span></span>  

<span data-ttu-id="bd53d-126">Les noms DNS internes ne peuvent être résolus qu’à l’intérieur d’un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="bd53d-126">Internal DNS names are only resolvable inside an Azure virtual network.</span></span>  <span data-ttu-id="bd53d-127">Étant donné que les noms DNS hello sont internes, ils ne sont pas toohello pouvant être résolu en dehors d’internet, en fournissant l’infrastructure toohello de sécurité supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="bd53d-127">Because hello DNS names are internal, they are not resolvable toohello outside internet, providing additional security toohello infrastructure.</span></span>

<span data-ttu-id="bd53d-128">_Remplacez les exemples par votre propre attribution de noms._</span><span class="sxs-lookup"><span data-stu-id="bd53d-128">_Replace any examples with your own naming._</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="bd53d-129">Créer le groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="bd53d-129">Create hello Resource group</span></span>

<span data-ttu-id="bd53d-130">Un groupe de ressources est tooorganize nécessaire tout ce dont nous créons cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="bd53d-130">A Resource Group is needed tooorganize everything we create in this walkthrough.</span></span>  <span data-ttu-id="bd53d-131">Pour plus d’informations sur les groupes de ressources Azure, consultez l’article [Vue d’ensemble d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bd53d-131">For more information on Azure Resource Groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-hello-vnet"></a><span data-ttu-id="bd53d-132">Créer hello réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="bd53d-132">Create hello VNet</span></span>

<span data-ttu-id="bd53d-133">première étape de Hello est toobuild un toolaunch de réseau virtuel hello des machines virtuelles dans.</span><span class="sxs-lookup"><span data-stu-id="bd53d-133">hello first step is toobuild a VNet toolaunch hello VMs into.</span></span>  <span data-ttu-id="bd53d-134">Hello réseau virtuel contient un sous-réseau pour cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="bd53d-134">hello VNet contains one subnet for this walkthrough.</span></span>  <span data-ttu-id="bd53d-135">Pour plus d’informations sur des réseaux virtuels Azure, consultez [créer un réseau virtuel à l’aide de hello CLI d’Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="bd53d-135">For more information on Azure VNets, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-hello-nsg"></a><span data-ttu-id="bd53d-136">Créer hello NSG</span><span class="sxs-lookup"><span data-stu-id="bd53d-136">Create hello NSG</span></span>

<span data-ttu-id="bd53d-137">Hello sous-réseau repose derrière un groupe de sécurité réseau existant afin de nous hello NSG hello sous-réseau avant de le générer.</span><span class="sxs-lookup"><span data-stu-id="bd53d-137">hello Subnet is built behind an existing Network Security Group so we build hello NSG before hello Subnet.</span></span>  <span data-ttu-id="bd53d-138">Groupes de sécurité réseau Azure sont pare-feu tooa équivalente à la couche réseau hello.</span><span class="sxs-lookup"><span data-stu-id="bd53d-138">Azure NSGs are equivalent tooa firewall at hello network layer.</span></span>  <span data-ttu-id="bd53d-139">Pour plus d’informations sur les groupes de sécurité réseau Azure, consultez [comment les groupes de sécurité réseau toocreate dans hello CLI d’Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="bd53d-139">For more information on Azure NSGs, see [How toocreate NSGs in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="bd53d-140">Ajouter une règle d’autorisation SSH entrante</span><span class="sxs-lookup"><span data-stu-id="bd53d-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="bd53d-141">Hello Linux VM a besoin d’accéder à partir de hello internet pour une règle autorisant le port entrant 22 trafic toobe transmises via le réseau de hello tooport 22 sur hello Linux VM est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="bd53d-141">hello Linux VM needs access from hello internet so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello Linux VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a><span data-ttu-id="bd53d-142">Ajouter un sous-réseau de toohello réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="bd53d-142">Add a subnet toohello VNet</span></span>

<span data-ttu-id="bd53d-143">Machines virtuelles au sein de hello réseau virtuel doivent se trouver dans un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="bd53d-143">VMs within hello VNet must be located in a subnet.</span></span>  <span data-ttu-id="bd53d-144">Chaque réseau virtuel peut présenter plusieurs sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="bd53d-144">Each VNet can have multiple subnets.</span></span>  <span data-ttu-id="bd53d-145">Créer des sous-réseaux de hello et associez hello sous-réseau hello NSG tooadd un sous-réseau toohello de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="bd53d-145">Create hello subnet and associate hello subnet with hello NSG tooadd a firewall toohello subnet.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

<span data-ttu-id="bd53d-146">Hello sous-réseau est désormais ajouté à l’intérieur du réseau virtuel de hello et associé hello NSG et règle de groupe de sécurité réseau hello.</span><span class="sxs-lookup"><span data-stu-id="bd53d-146">hello Subnet is now added inside hello VNet and associated with hello NSG and hello NSG rule.</span></span>

## <a name="creating-static-dns-names"></a><span data-ttu-id="bd53d-147">Création de noms DNS statiques</span><span class="sxs-lookup"><span data-stu-id="bd53d-147">Creating static DNS names</span></span>

<span data-ttu-id="bd53d-148">Azure est très souple, mais toouse les noms DNS pour la résolution de noms d’ordinateurs virtuels, vous devez toocreate en tant que virtuel cartes (cartes réseau) à l’aide de DNS étiquetage de réseau.</span><span class="sxs-lookup"><span data-stu-id="bd53d-148">Azure is very flexible, but toouse DNS names for VMs name resolution, you need toocreate them as Virtual network cards (VNics) using DNS labeling.</span></span>  <span data-ttu-id="bd53d-149">Cartes réseau est importantes que vous puissiez les réutiliser en les connectant toodifferent les machines virtuelles, ce qui maintient hello VNic comme une ressource statique hello machines virtuelles peut être temporaire.</span><span class="sxs-lookup"><span data-stu-id="bd53d-149">VNics are important as you can reuse them by connecting them toodifferent VMs, which keeps hello VNic as a static resource while hello VMs can be temporary.</span></span>  <span data-ttu-id="bd53d-150">À l’aide de DNS étiquetage sur une carte réseau virtuelle de hello, nous sommes tooenable en mesure de résolution de nom simple à partir d’autres ordinateurs virtuels hello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="bd53d-150">By using DNS labeling on hello VNic, we are able tooenable simple name resolution from other VMs in hello VNet.</span></span>  <span data-ttu-id="bd53d-151">Noms pouvant être résolus grâce à autre serveur automation de machines virtuelles tooaccess hello par nom DNS hello `Jenkins` ou serveur hello Git `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="bd53d-151">Using resolvable names enables other VMs tooaccess hello automation server by hello DNS name `Jenkins` or hello Git server as `gitrepo`.</span></span>  <span data-ttu-id="bd53d-152">Créer une carte réseau virtuelle et l’associer à hello que sous-réseau créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="bd53d-152">Create a VNic and associate it with hello Subnet created in hello previous step.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="bd53d-153">Déployer hello VM dans hello réseau virtuel et le groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="bd53d-153">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="bd53d-154">Nous disposons désormais d’un réseau virtuel, un sous-réseau à l’intérieur de ce réseau virtuel et un groupe de sécurité réseau agissant comme un tooprotect pare-feu notre sous-réseau en bloquant tout le trafic entrant, à l’exception de port 22 pour SSH.</span><span class="sxs-lookup"><span data-stu-id="bd53d-154">We now have a VNet, a subnet inside that VNet, and an NSG acting as a firewall tooprotect our subnet by blocking all inbound traffic except port 22 for SSH.</span></span>  <span data-ttu-id="bd53d-155">Hello machine virtuelle peut désormais être déployé à l’intérieur de cette infrastructure réseau existante.</span><span class="sxs-lookup"><span data-stu-id="bd53d-155">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="bd53d-156">À l’aide de hello CLI d’Azure et hello `azure vm create` hello Linux VM est déployé toohello existante du groupe de ressources Azure, du réseau virtuel, sous-réseau et une carte réseau virtuelle de la commande.</span><span class="sxs-lookup"><span data-stu-id="bd53d-156">Using hello Azure CLI, and hello `azure vm create` command, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>  <span data-ttu-id="bd53d-157">Pour plus d’informations sur l’utilisation de hello CLI toodeploy une machine virtuelle complète, consultez [créer un environnement complet de Linux à l’aide de hello CLI d’Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="bd53d-157">For more information on using hello CLI toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

<span data-ttu-id="bd53d-158">À l’aide de hello CLI indicateurs toocall les ressources existantes, nous indiquons hello toodeploy Azure VM à l’intérieur du réseau existant de hello.</span><span class="sxs-lookup"><span data-stu-id="bd53d-158">By using hello CLI flags toocall out existing resources, we instruct Azure toodeploy hello VM inside hello existing network.</span></span>  <span data-ttu-id="bd53d-159">tooreiterate, une fois qu’un réseau virtuel et le sous-réseau ont été déployés, ils peuvent rester statiques ou permanentes des ressources à l’intérieur de votre région Azure.</span><span class="sxs-lookup"><span data-stu-id="bd53d-159">tooreiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="bd53d-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bd53d-160">Next steps</span></span>
* [<span data-ttu-id="bd53d-161">Créer votre propre environnement personnalisé pour une machine virtuelle Linux à l’aide des commandes de l’interface de ligne de commande Azure directement</span><span class="sxs-lookup"><span data-stu-id="bd53d-161">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="bd53d-162">Création d’une machine virtuelle Linux sur Azure à l’aide de modèles</span><span class="sxs-lookup"><span data-stu-id="bd53d-162">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
