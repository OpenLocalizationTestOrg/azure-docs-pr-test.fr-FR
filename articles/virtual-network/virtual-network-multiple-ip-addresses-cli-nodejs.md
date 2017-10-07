---
title: "aaaVM avec plusieurs adresses IP à l’aide de hello Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment tooassign des adresses IP multiples à l’aide de machine virtuelle tooa hello Azure CLI 1.0 | Gestionnaire de ressources."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 83ad48e67309fb21d5aca967d4f2c01afdc0b5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-azure-cli-10"></a><span data-ttu-id="9234c-103">Affecter plusieurs adresses IP des ordinateurs de toovirtual à l’aide de Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9234c-103">Assign multiple IP addresses toovirtual machines using Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="9234c-104">Cet article explique comment toocreate un ordinateur virtuel (VM) l’utilisation de modèle de déploiement Azure Resource Manager hello hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="9234c-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using hello Azure CLI 1.0.</span></span> <span data-ttu-id="9234c-105">Tooresources créé via le modèle de déploiement classique hello ne peut pas être assignés à plusieurs adresses IP.</span><span class="sxs-lookup"><span data-stu-id="9234c-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="9234c-106">toolearn plus d’informations sur les modèles de déploiement Azure, lisez hello [comprendre les modèles de déploiement](../resource-manager-deployment-model.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="9234c-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="9234c-107"><a name = "create"></a>Créer une machine virtuelle avec plusieurs adresses IP</span><span class="sxs-lookup"><span data-stu-id="9234c-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="9234c-108">Vous pouvez effectuer cette tâche à l’aide de hello Azure CLI 1.0 (cet article) ou hello [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9234c-108">You can complete this task using hello Azure CLI 1.0 (this article) or hello [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span></span> <span data-ttu-id="9234c-109">Hello étapes qui suivent expliquent comment toocreate un exemple de machine virtuelle avec plusieurs IP, les adresses, comme décrit dans le scénario de hello.</span><span class="sxs-lookup"><span data-stu-id="9234c-109">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="9234c-110">Modifiez les noms des variables et les types d’adresses IP en fonction des besoins de votre implémentation.</span><span class="sxs-lookup"><span data-stu-id="9234c-110">Change variable names and IP address types as required for your implementation.</span></span>

1. <span data-ttu-id="9234c-111">Installer et configurer Azure CLI 1.0 par hello suivant les étapes de hello Bonjour [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) l’article et connectez-vous à votre compte Azure avec hello `azure-login` commande.</span><span class="sxs-lookup"><span data-stu-id="9234c-111">Install and configure hello Azure CLI 1.0 by following hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account with hello `azure-login` command.</span></span>

2. <span data-ttu-id="9234c-112">Créez un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="9234c-112">Create a resource group:</span></span>
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. <span data-ttu-id="9234c-113">Créez un réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="9234c-113">Create a virtual network:</span></span>

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. <span data-ttu-id="9234c-114">Créer un sous-réseau de réseau virtuel de hello :</span><span class="sxs-lookup"><span data-stu-id="9234c-114">Create a subnet in hello virtual network:</span></span>

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. <span data-ttu-id="9234c-115">Créer un compte de stockage pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9234c-115">Create  a storage account for hello VM.</span></span> <span data-ttu-id="9234c-116">Avant d’exécuter hello suivant de commande, remplacez *mystorageaccount* avec un nom unique.</span><span class="sxs-lookup"><span data-stu-id="9234c-116">Before running hello following command, replace *mystorageaccount* with a unique name.</span></span> <span data-ttu-id="9234c-117">nom de Hello doit être unique dans Azure :</span><span class="sxs-lookup"><span data-stu-id="9234c-117">hello name must be unique across Azure:</span></span>

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. <span data-ttu-id="9234c-118">Créer des configurations IP, une carte réseau, hello et affecter hello IP configurations toohello carte réseau.</span><span class="sxs-lookup"><span data-stu-id="9234c-118">Create hello IP configurations, a NIC, and assign hello IP configurations toohello NIC.</span></span> <span data-ttu-id="9234c-119">Vous pouvez ajouter, supprimer ou modifier les configurations de hello selon les besoins.</span><span class="sxs-lookup"><span data-stu-id="9234c-119">You can add, remove, or change hello configurations as necessary.</span></span> <span data-ttu-id="9234c-120">Hello, suivant les configurations est décrites dans le scénario de hello :</span><span class="sxs-lookup"><span data-stu-id="9234c-120">hello following configurations are described in hello scenario:</span></span>

    <span data-ttu-id="9234c-121">**IPConfig-1**</span><span class="sxs-lookup"><span data-stu-id="9234c-121">**IPConfig-1**</span></span>

    <span data-ttu-id="9234c-122">Entrez les commandes hello qui suivent toocreate :</span><span class="sxs-lookup"><span data-stu-id="9234c-122">Enter hello commands that follow toocreate:</span></span>

    - <span data-ttu-id="9234c-123">une ressource d’adresse IP publique avec une adresse IP publique statique ;</span><span class="sxs-lookup"><span data-stu-id="9234c-123">A public IP address resource with a static public IP address</span></span>
    - <span data-ttu-id="9234c-124">Une carte de réseau, affectation d’adresse IP publique de hello et un tooit d’adresse IP privée statique.</span><span class="sxs-lookup"><span data-stu-id="9234c-124">A NIC, assigning hello public IP address and a static private IP address tooit.</span></span>
    
    <span data-ttu-id="9234c-125">Remplacez *mypublicdns* avec un nom qui est unique au sein de hello emplacement Azure.</span><span class="sxs-lookup"><span data-stu-id="9234c-125">Replace *mypublicdns* with a name that is unique within hello Azure location.</span></span>

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > <span data-ttu-id="9234c-126">Les adresses IP publiques ont un coût nominal.</span><span class="sxs-lookup"><span data-stu-id="9234c-126">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="9234c-127">toolearn en savoir plus sur le protocole IP adresse tarification, lire hello [tarification d’adresse IP](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span><span class="sxs-lookup"><span data-stu-id="9234c-127">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="9234c-128">Il existe un toohello limiter le nombre d’adresses IP publiques qui peut être utilisé dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="9234c-128">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="9234c-129">toolearn plus d’informations sur les limites de hello, lire hello [Azure limite](../azure-subscription-service-limits.md#networking-limits) l’article.</span><span class="sxs-lookup"><span data-stu-id="9234c-129">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    <span data-ttu-id="9234c-130">**IPConfig-2**</span><span class="sxs-lookup"><span data-stu-id="9234c-130">**IPConfig-2**</span></span>

     <span data-ttu-id="9234c-131">Entrez hello suivant de commandes toocreate une nouvelle ressource d’adresse IP publique et une nouvelle configuration IP avec une adresse IP publique statique et une adresse IP privée statique :</span><span class="sxs-lookup"><span data-stu-id="9234c-131">Enter hello following commands toocreate a new public IP address resource and a new IP configuration with a static public IP address and a static private IP address:</span></span>
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    <span data-ttu-id="9234c-132">**IPConfig-3**</span><span class="sxs-lookup"><span data-stu-id="9234c-132">**IPConfig-3**</span></span>

    <span data-ttu-id="9234c-133">Entrez hello suivant de commandes toocreate une configuration IP avec une adresse IP privée statique et aucune adresse IP publique :</span><span class="sxs-lookup"><span data-stu-id="9234c-133">Enter hello following commands toocreate an IP configuration with a static private IP address and no public IP address:</span></span>

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    ><span data-ttu-id="9234c-134">Bien que cet article affecte tous les tooa de configurations IP carte réseau unique, vous pouvez également affecter tooany de configurations IP plusieurs cartes réseau dans une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9234c-134">Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations tooany NIC in a VM.</span></span> <span data-ttu-id="9234c-135">toolearn comment lu d’une machine virtuelle avec plusieurs cartes réseau, toocreate hello créer une machine virtuelle avec plusieurs cartes réseau article.</span><span class="sxs-lookup"><span data-stu-id="9234c-135">toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs article.</span></span>

7. <span data-ttu-id="9234c-136">Créer une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="9234c-136">Create a Linux VM</span></span> 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    <span data-ttu-id="9234c-137">hello toochange v2 de tooStandard DS2 de taille de machine virtuelle, par exemple, ajoutez simplement hello suivant propriété `--vm-size Standard_DS3_v2` toohello `azure vm create` commande à l’étape 6.</span><span class="sxs-lookup"><span data-stu-id="9234c-137">toochange hello VM size tooStandard DS2 v2, for example, simply add hello following property `--vm-size Standard_DS3_v2` toohello `azure vm create` command in step 6.</span></span>

8. <span data-ttu-id="9234c-138">Entrez hello suivant commande tooview hello NIC et hello des configurations IP associées :</span><span class="sxs-lookup"><span data-stu-id="9234c-138">Enter hello following command tooview hello NIC and hello associated IP configurations:</span></span>

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. <span data-ttu-id="9234c-139">Système d’exploitation de l’ordinateur virtuel toohello les adresses IP privée de hello ajouter en procédant comme hello pour votre système d’exploitation Bonjour [ajouter une adresse IP traite le système d’exploitation de l’ordinateur virtuel tooa](#os-config) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="9234c-139">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="9234c-140"><a name="add"></a>Ajouter tooa d’adresses IP virtuelle</span><span class="sxs-lookup"><span data-stu-id="9234c-140"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="9234c-141">Vous pouvez ajouter plus privé et public IP adresses tooan existant de carte réseau en effectuant les étapes hello qui suivent.</span><span class="sxs-lookup"><span data-stu-id="9234c-141">You can add additional private and public IP addresses tooan existing NIC by completing hello steps that follow.</span></span> <span data-ttu-id="9234c-142">les exemples Hello reposent sur hello [scénario](#Scenario) décrit dans cet article.</span><span class="sxs-lookup"><span data-stu-id="9234c-142">hello examples build upon hello [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="9234c-143">Ouvrez CLI d’Azure et complète hello restant des étapes de cette section au sein d’une seule session CLI.</span><span class="sxs-lookup"><span data-stu-id="9234c-143">Open Azure CLI and complete hello remaining steps in this section within a single CLI session.</span></span> <span data-ttu-id="9234c-144">Si vous n’avez pas encore installé et configuré CLI d’Azure, hello terminé les étapes Bonjour [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) l’article et connectez-vous à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="9234c-144">If you don't already have Azure CLI installed and configured, complete hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account.</span></span>

2. <span data-ttu-id="9234c-145">Suivez les étapes de hello dans un des hello les sections, en fonction de vos exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="9234c-145">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    - <span data-ttu-id="9234c-146">**Ajouter une adresse IP privée**</span><span class="sxs-lookup"><span data-stu-id="9234c-146">**Add a private IP address**</span></span>
    
        <span data-ttu-id="9234c-147">tooadd un tooa d’adresse IP privée carte réseau, vous devez créer une configuration IP à l’aide de la commande hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9234c-147">tooadd a private IP address tooa NIC, you must create an IP configuration using hello command below.</span></span> <span data-ttu-id="9234c-148">adresse Hello doit être une adresse non utilisée pour le sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="9234c-148">hello static address must be an unused address for hello subnet.</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        <span data-ttu-id="9234c-149">Créez autant de configurations que nécessaire, à l’aide de noms de configuration unique et d’adresses IP privées (pour les configurations avec des adresses IP statiques).</span><span class="sxs-lookup"><span data-stu-id="9234c-149">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    - <span data-ttu-id="9234c-150">**Ajouter une adresse IP publique**</span><span class="sxs-lookup"><span data-stu-id="9234c-150">**Add a public IP address**</span></span>
    
        <span data-ttu-id="9234c-151">Une adresse IP publique est ajoutée en l’associant tooeither une nouvelle configuration IP ou une configuration IP existante.</span><span class="sxs-lookup"><span data-stu-id="9234c-151">A public IP address is added by associating it tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="9234c-152">Effectuez les étapes de hello dans une des sections hello qui suivent, dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="9234c-152">Complete hello steps in one of hello sections that follow, as you require.</span></span>

        > [!NOTE]
        > <span data-ttu-id="9234c-153">Les adresses IP publiques ont un coût nominal.</span><span class="sxs-lookup"><span data-stu-id="9234c-153">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="9234c-154">toolearn en savoir plus sur le protocole IP adresse tarification, lire hello [tarification d’adresse IP](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span><span class="sxs-lookup"><span data-stu-id="9234c-154">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="9234c-155">Il existe un toohello limiter le nombre d’adresses IP publiques qui peut être utilisé dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="9234c-155">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="9234c-156">toolearn plus d’informations sur les limites de hello, lire hello [Azure limite](../azure-subscription-service-limits.md#networking-limits) l’article.</span><span class="sxs-lookup"><span data-stu-id="9234c-156">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
        >

        <span data-ttu-id="9234c-157">**Associer hello ressource tooa nouvelle configuration IP**</span><span class="sxs-lookup"><span data-stu-id="9234c-157">**Associate hello resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="9234c-158">Lorsque vous ajoutez une adresse IP publique dans une nouvelle configuration IP, vous devez également ajouter une adresse IP privée, car toutes les configurations IP doivent avoir une adresse IP privée.</span><span class="sxs-lookup"><span data-stu-id="9234c-158">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="9234c-159">Vous pouvez ajouter une ressource d’adresse IP publique existante ou en créer une.</span><span class="sxs-lookup"><span data-stu-id="9234c-159">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="9234c-160">toocreate un nouveau, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9234c-160">toocreate a new one, enter hello following command:</span></span>

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        <span data-ttu-id="9234c-161">toocreate une nouvelle configuration IP avec une adresse IP privée statique et le hello associés *myPublicIP3* adresse IP publique de ressources d’adresses, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9234c-161">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIP3* public IP address resource, enter hello following command:</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        <span data-ttu-id="9234c-162">**Associer la configuration IP existante de hello ressource tooan**</span><span class="sxs-lookup"><span data-stu-id="9234c-162">**Associate hello resource tooan existing IP configuration**</span></span>

        <span data-ttu-id="9234c-163">Une ressource d’adresse IP publique peut être uniquement la configuration IP tooan associés qui n’en avez pas encore associé.</span><span class="sxs-lookup"><span data-stu-id="9234c-163">A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="9234c-164">Vous pouvez déterminer si une configuration IP a une adresse IP publique associée en saisissant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9234c-164">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        <span data-ttu-id="9234c-165">Recherchez un toohello similaire de ligne qui suit pour 3-IPConfig Bonjour retourné de sortie :</span><span class="sxs-lookup"><span data-stu-id="9234c-165">Look for a line similar toohello one that follows for IPConfig-3 in hello returned output:</span></span>

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        <span data-ttu-id="9234c-166">Depuis hello **adresse IP publique** colonne *IpConfig-3* est vide, aucune ressource d’adresse IP publique n’est tooit actuellement associé.</span><span class="sxs-lookup"><span data-stu-id="9234c-166">Since hello **Public IP** column for *IpConfig-3* is blank, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="9234c-167">Vous pouvez ajouter un existant publique IP adresse ressource tooIpConfig-3, ou entrez hello suivant toocreate commande une :</span><span class="sxs-lookup"><span data-stu-id="9234c-167">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        <span data-ttu-id="9234c-168">Entrez hello commande hello tooassociate adresse IP publique adresse configuration IP existante toohello ressource nommée suivante *IPConfig-3*:</span><span class="sxs-lookup"><span data-stu-id="9234c-168">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IPConfig-3*:</span></span>
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. <span data-ttu-id="9234c-169">Afficher les adresses IP privées hello et hello toohello attribué ressources IP adresse publique carte réseau en entrant hello la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9234c-169">View hello private IP addresses and hello public IP address resources assigned toohello NIC by entering hello following command:</span></span>

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      <span data-ttu-id="9234c-170">Hello retourné la sortie est similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="9234c-170">hello returned output is similar toohello following:</span></span>
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. <span data-ttu-id="9234c-171">Ajouter des adresses IP privées de hello, vous avez ajouté le système d’exploitation VM toohello NIC toohello en suivant les instructions de hello Bonjour [ajouter une adresse IP traite le système d’exploitation de l’ordinateur virtuel tooa](#os-config) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="9234c-171">Add hello private IP addresses you added toohello NIC toohello VM operating system by following hello instructions in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="9234c-172">N’ajoutez pas hello publique IP adresses toohello système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="9234c-172">Do not add hello public IP addresses toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
