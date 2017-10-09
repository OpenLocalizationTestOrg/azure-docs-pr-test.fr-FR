---
title: "aaaUse la résolution par hello Azure CLI 2.0 de noms DNS internes pour la machine virtuelle | Documents Microsoft"
description: "Comment les réseaux virtuels toocreate cartes d’interface et utiliser DNS interne pour la résolution de nom de machine virtuelle sur Azure avec hello Azure CLI 2.0"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: b3c4bfd3ab698f7b25d763ba9e60dd7984f6269d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="04f6d-103">Création de cartes d’interface réseau virtuelle et d’utilisation des DNS internes pour la résolution des noms de machine virtuelle sur Azure</span><span class="sxs-lookup"><span data-stu-id="04f6d-103">Create virtual network interface cards and use internal DNS for VM name resolution on Azure</span></span>
<span data-ttu-id="04f6d-104">Cet article explique comment tooset statique les noms DNS internes pour les machines virtuelles Linux à l’aide de virtual network cartes d’interface (cartes réseau) et les noms d’étiquette DNS avec hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="04f6d-104">This article shows you how tooset static internal DNS names for Linux VMs using virtual network interface cards (vNics) and DNS label names with hello Azure CLI 2.0.</span></span> <span data-ttu-id="04f6d-105">Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="04f6d-105">You can also perform these steps with hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="04f6d-106">Les noms DNS statiques sont utilisés pour les services d’infrastructure permanents comme un serveur de builds Jenkins, qui est utilisé pour ce document, ou un serveur Git.</span><span class="sxs-lookup"><span data-stu-id="04f6d-106">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="04f6d-107">spécifications de Hello sont :</span><span class="sxs-lookup"><span data-stu-id="04f6d-107">hello requirements are:</span></span>

* [<span data-ttu-id="04f6d-108">un compte Azure</span><span class="sxs-lookup"><span data-stu-id="04f6d-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="04f6d-109">des fichiers de clés SSH publiques et privées</span><span class="sxs-lookup"><span data-stu-id="04f6d-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="04f6d-110">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="04f6d-110">Quick commands</span></span>
<span data-ttu-id="04f6d-111">Si vous avez besoin de tooquickly accomplir la tâche hello, hello suivant la section Détails des commandes hello nécessaires.</span><span class="sxs-lookup"><span data-stu-id="04f6d-111">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="04f6d-112">Plus d’informations et le contexte de chaque étape se trouvent dans le reste de hello du document de hello, [Démarrer ici](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="04f6d-112">More detailed information and context for each step can be found in hello rest of hello document, [starting here](#detailed-walkthrough).</span></span> <span data-ttu-id="04f6d-113">tooperform ces étapes, vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="04f6d-113">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="04f6d-114">Conditions préalables : groupe de ressources, réseau virtuel et sous-réseau, groupe de sécurité réseau avec SSH entrant.</span><span class="sxs-lookup"><span data-stu-id="04f6d-114">Pre-Requirements: Resource Group, virtual network and subnet, Network Security Group with SSH inbound.</span></span>

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a><span data-ttu-id="04f6d-115">Création d’une carte réseau virtuelle avec un nom DNS interne statique</span><span class="sxs-lookup"><span data-stu-id="04f6d-115">Create a virtual network interface card with a static internal DNS name</span></span>
<span data-ttu-id="04f6d-116">Créer une carte réseau virtuelle de hello avec [créer des cartes réseau du réseau az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="04f6d-116">Create hello vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="04f6d-117">Hello `--internal-dns-name` CLI est pour le nom DNS paramètre hello, qui fournit un nom DNS statique hello pour une carte d’interface réseau virtuelle hello (vNic).</span><span class="sxs-lookup"><span data-stu-id="04f6d-117">hello `--internal-dns-name` CLI flag is for setting hello DNS label, which provides hello static DNS name for hello virtual network interface card (vNic).</span></span> <span data-ttu-id="04f6d-118">Hello exemple suivant crée une carte réseau virtuelle nommée `myNic`, connecte toohello `myVnet` réseau virtuel et crée un enregistrement de nom DNS interne appelé `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="04f6d-118">hello following example creates a vNic named `myNic`, connects it toohello `myVnet` virtual network, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-hello-vnic"></a><span data-ttu-id="04f6d-119">Déployer un ordinateur virtuel et vous connecter à une carte réseau virtuelle hello</span><span class="sxs-lookup"><span data-stu-id="04f6d-119">Deploy a VM and connect hello vNic</span></span>
<span data-ttu-id="04f6d-120">Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="04f6d-120">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="04f6d-121">Hello `--nics` indicateur connecte hello vNic toohello VM pendant hello déploiement tooAzure.</span><span class="sxs-lookup"><span data-stu-id="04f6d-121">hello `--nics` flag connects hello vNic toohello VM during hello deployment tooAzure.</span></span> <span data-ttu-id="04f6d-122">Hello exemple suivant crée un ordinateur virtuel nommé `myVM` avec disques gérés d’Azure et hello attache une carte réseau virtuelle nommée `myNic` de hello précédant l’étape :</span><span class="sxs-lookup"><span data-stu-id="04f6d-122">hello following example creates a VM named `myVM` with Azure Managed Disks and attaches hello vNic named `myNic` from hello preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="04f6d-123">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="04f6d-123">Detailed walkthrough</span></span>

<span data-ttu-id="04f6d-124">Une intégration complète continue et un déploiement continu (CiCd) une infrastructure sur Azure requiert certains serveurs de toobe serveurs statique ou à long terme.</span><span class="sxs-lookup"><span data-stu-id="04f6d-124">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers toobe static or long-lived servers.</span></span> <span data-ttu-id="04f6d-125">Il est recommandé que les ressources Azure telles que hello des réseaux virtuels et des groupes de sécurité réseau sont statiques et longue durée de vie ressources qui sont rarement déployées.</span><span class="sxs-lookup"><span data-stu-id="04f6d-125">It is recommended that Azure assets like hello virtual networks and Network Security Groups are static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="04f6d-126">Une fois qu’un réseau virtuel a été déployé, il peut être réutilisé par nouveaux déploiements sans n’importe quelle infrastructure de toohello répercussions négatives.</span><span class="sxs-lookup"><span data-stu-id="04f6d-126">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="04f6d-127">Vous pouvez ajouter ultérieurement un serveur de référentiel Git ou un serveur automation de Jenkins remet CiCd toothis de réseau virtuel pour vos environnements de développement ou de test.</span><span class="sxs-lookup"><span data-stu-id="04f6d-127">You can later add a Git repository server or a Jenkins automation server delivers CiCd toothis virtual network for your development or test environments.</span></span>  

<span data-ttu-id="04f6d-128">Les noms DNS internes ne peuvent être résolus qu’à l’intérieur d’un réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="04f6d-128">Internal DNS names are only resolvable inside an Azure virtual network.</span></span> <span data-ttu-id="04f6d-129">Étant donné que les noms DNS hello sont internes, ils ne sont pas toohello pouvant être résolu en dehors d’internet, en fournissant l’infrastructure toohello de sécurité supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="04f6d-129">Because hello DNS names are internal, they are not resolvable toohello outside internet, providing additional security toohello infrastructure.</span></span>

<span data-ttu-id="04f6d-130">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="04f6d-130">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="04f6d-131">Exemples de noms de paramètre : `myResourceGroup`, `myNic` et `myVM`.</span><span class="sxs-lookup"><span data-stu-id="04f6d-131">Example parameter names include `myResourceGroup`, `myNic`, and `myVM`.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="04f6d-132">Créer le groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="04f6d-132">Create hello resource group</span></span>
<span data-ttu-id="04f6d-133">Commencez par créer le groupe de ressources hello avec [az groupe créer](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="04f6d-133">First, create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="04f6d-134">Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `westus` emplacement :</span><span class="sxs-lookup"><span data-stu-id="04f6d-134">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-hello-virtual-network"></a><span data-ttu-id="04f6d-135">Créer le réseau virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="04f6d-135">Create hello virtual network</span></span>

<span data-ttu-id="04f6d-136">étape suivante de Hello est toobuild un toolaunch de réseau virtuel hello des machines virtuelles dans.</span><span class="sxs-lookup"><span data-stu-id="04f6d-136">hello next step is toobuild a virtual network toolaunch hello VMs into.</span></span> <span data-ttu-id="04f6d-137">réseau virtuel de Hello contient un sous-réseau pour cette procédure pas à pas.</span><span class="sxs-lookup"><span data-stu-id="04f6d-137">hello virtual network contains one subnet for this walkthrough.</span></span> <span data-ttu-id="04f6d-138">Pour plus d’informations sur les réseaux virtuels Azure, consultez [créer un réseau virtuel à l’aide de hello CLI d’Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="04f6d-138">For more information on Azure virtual networks, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="04f6d-139">Créer le réseau virtuel hello [créer un réseau virtuel du réseau az](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="04f6d-139">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="04f6d-140">Hello exemple suivant crée un réseau virtuel nommé `myVnet` et sous-réseau nommé `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="04f6d-140">hello following example creates a virtual network named `myVnet` and subnet named `mySubnet`:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="04f6d-141">Créer un groupe de sécurité réseau de hello</span><span class="sxs-lookup"><span data-stu-id="04f6d-141">Create hello Network Security Group</span></span>
<span data-ttu-id="04f6d-142">Les groupes de sécurité réseau Azure sont pare-feu tooa équivalente à la couche réseau hello.</span><span class="sxs-lookup"><span data-stu-id="04f6d-142">Azure Network Security Groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="04f6d-143">Pour plus d’informations sur les groupes de sécurité réseau, consultez [comment les groupes de sécurité réseau toocreate dans hello CLI d’Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="04f6d-143">For more information about Network Security Groups, see [How toocreate NSGs in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="04f6d-144">Créer le groupe de sécurité réseau hello avec [az réseau nsg créer](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="04f6d-144">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="04f6d-145">Hello exemple suivant crée un groupe de sécurité réseau nommé `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="04f6d-145">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-tooallow-ssh"></a><span data-ttu-id="04f6d-146">Ajouter une règle de trafic entrant de tooallow SSH</span><span class="sxs-lookup"><span data-stu-id="04f6d-146">Add an inbound rule tooallow SSH</span></span>
<span data-ttu-id="04f6d-147">Ajouter une règle de trafic entrant pour le groupe de sécurité réseau hello avec [créer de règle de groupe de sécurité réseau du réseau az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="04f6d-147">Add an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="04f6d-148">Hello exemple suivant crée une règle nommée `myRuleAllowSSH`:</span><span class="sxs-lookup"><span data-stu-id="04f6d-148">hello following example creates a rule named `myRuleAllowSSH`:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-hello-subnet-with-hello-network-security-group"></a><span data-ttu-id="04f6d-149">Associez hello sous-réseau hello groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="04f6d-149">Associate hello subnet with hello Network Security Group</span></span>
<span data-ttu-id="04f6d-150">sous-réseau hello tooassociate hello groupe de sécurité réseau, utilisez [mise à jour de sous-réseau de réseau virtuel az réseau](/cli/azure/network/vnet/subnet#update).</span><span class="sxs-lookup"><span data-stu-id="04f6d-150">tooassociate hello subnet with hello Network Security Group, use [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span></span> <span data-ttu-id="04f6d-151">Hello exemple suivant associe un nom de sous-réseau hello `mySubnet` avec hello groupe de sécurité réseau nommé `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="04f6d-151">hello following example associates hello subnet name `mySubnet` with hello Network Security Group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-hello-virtual-network-interface-card-and-static-dns-names"></a><span data-ttu-id="04f6d-152">Créer une carte d’interface réseau virtuelle hello et des noms DNS statiques</span><span class="sxs-lookup"><span data-stu-id="04f6d-152">Create hello virtual network interface card and static DNS names</span></span>
<span data-ttu-id="04f6d-153">Azure est très souple, mais toouse les noms DNS pour la résolution de nom de machine virtuelle, vous devez toocreate virtuel cartes d’interface réseau (cartes réseau) qui incluent un nom DNS.</span><span class="sxs-lookup"><span data-stu-id="04f6d-153">Azure is very flexible, but toouse DNS names for VM name resolution, you need toocreate virtual network interface cards (vNics) that include a DNS label.</span></span> <span data-ttu-id="04f6d-154">cartes réseau est importantes que vous puissiez les réutiliser en les connectant toodifferent VMs hello infrastructure du cycle de vie.</span><span class="sxs-lookup"><span data-stu-id="04f6d-154">vNics are important as you can reuse them by connecting them toodifferent VMs over hello infrastructure lifecycle.</span></span> <span data-ttu-id="04f6d-155">Cette approche conserve une carte réseau virtuelle hello comme une ressource statique hello machines virtuelles peut être temporaire.</span><span class="sxs-lookup"><span data-stu-id="04f6d-155">This approach keeps hello vNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="04f6d-156">À l’aide de DNS étiquetage sur une carte réseau virtuelle hello, nous sommes tooenable en mesure de résolution de nom simple à partir d’autres ordinateurs virtuels hello réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="04f6d-156">By using DNS labeling on hello vNic, we are able tooenable simple name resolution from other VMs in hello VNet.</span></span> <span data-ttu-id="04f6d-157">Noms pouvant être résolus grâce à autre serveur automation de machines virtuelles tooaccess hello par nom DNS hello `Jenkins` ou serveur hello Git `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="04f6d-157">Using resolvable names enables other VMs tooaccess hello automation server by hello DNS name `Jenkins` or hello Git server as `gitrepo`.</span></span>  

<span data-ttu-id="04f6d-158">Créer une carte réseau virtuelle de hello avec [créer des cartes réseau du réseau az](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="04f6d-158">Create hello vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="04f6d-159">Hello exemple suivant crée une carte réseau virtuelle nommée `myNic`, connecte toohello `myVnet` réseau virtuel nommé `myVnet`et crée un enregistrement de nom DNS interne appelé `jenkins`:</span><span class="sxs-lookup"><span data-stu-id="04f6d-159">hello following example creates a vNic named `myNic`, connects it toohello `myVnet` virtual network named `myVnet`, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="04f6d-160">Déployer hello VM dans l’infrastructure de réseau virtuel hello</span><span class="sxs-lookup"><span data-stu-id="04f6d-160">Deploy hello VM into hello virtual network infrastructure</span></span>
<span data-ttu-id="04f6d-161">Nous disposons désormais d’un réseau virtuel et un sous-réseau, un groupe de sécurité réseau agissant comme un tooprotect pare-feu notre sous-réseau en bloquant tout le trafic entrant, à l’exception de port 22 pour SSH et une carte réseau virtuelle.</span><span class="sxs-lookup"><span data-stu-id="04f6d-161">We now have a virtual network and subnet, a Network Security Group acting as a firewall tooprotect our subnet by blocking all inbound traffic except port 22 for SSH, and a vNic.</span></span> <span data-ttu-id="04f6d-162">Vous pouvez maintenant déployer une machine virtuelle au sein de cette infrastructure réseau existante.</span><span class="sxs-lookup"><span data-stu-id="04f6d-162">You can now deploy a VM inside this existing network infrastructure.</span></span>

<span data-ttu-id="04f6d-163">Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="04f6d-163">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="04f6d-164">Hello exemple suivant crée un ordinateur virtuel nommé `myVM` avec disques gérés d’Azure et hello attache une carte réseau virtuelle nommée `myNic` de hello précédant l’étape :</span><span class="sxs-lookup"><span data-stu-id="04f6d-164">hello following example creates a VM named `myVM` with Azure Managed Disks and attaches hello vNic named `myNic` from hello preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="04f6d-165">À l’aide de hello CLI indicateurs toocall les ressources existantes, nous indiquons hello toodeploy Azure VM à l’intérieur du réseau existant de hello.</span><span class="sxs-lookup"><span data-stu-id="04f6d-165">By using hello CLI flags toocall out existing resources, we instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="04f6d-166">tooreiterate, une fois qu’un réseau virtuel et le sous-réseau ont été déployés, ils peuvent rester statiques ou permanentes des ressources à l’intérieur de votre région Azure.</span><span class="sxs-lookup"><span data-stu-id="04f6d-166">tooreiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="04f6d-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="04f6d-167">Next steps</span></span>
* [<span data-ttu-id="04f6d-168">Créer votre propre environnement personnalisé pour une machine virtuelle Linux à l’aide des commandes de l’interface de ligne de commande Azure directement</span><span class="sxs-lookup"><span data-stu-id="04f6d-168">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="04f6d-169">Création d’une machine virtuelle Linux sur Azure à l’aide de modèles</span><span class="sxs-lookup"><span data-stu-id="04f6d-169">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
