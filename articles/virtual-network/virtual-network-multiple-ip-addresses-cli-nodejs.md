---
title: "Machine virtuelle avec plusieurs adresses IP à l’aide d’Azure CLI 1.0 | Microsoft Docs"
description: "Découvrez comment attribuer plusieurs adresses IP à une machine virtuelle à l’aide d’Azure CLI 1.0 | Resource Manager."
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
ms.openlocfilehash: 9f085dfa1fe4db36d58cb976bb550a46bf241ac7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-azure-cli-10"></a><span data-ttu-id="5b043-103">Attribuer plusieurs adresses IP aux machines virtuelles à l’aide d’Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5b043-103">Assign multiple IP addresses to virtual machines using Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="5b043-104">Cet article explique comment créer une machine virtuelle dans le modèle de déploiement Azure Resource Manager à l’aide d’Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="5b043-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using the Azure CLI 1.0.</span></span> <span data-ttu-id="5b043-105">Il n’est pas possible d’affecter plusieurs adresses IP à des ressources créées à l’aide du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="5b043-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="5b043-106">Pour en savoir plus sur les modèles de déploiement Azure, voir [Comprendre les modèles de déploiement](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5b043-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="5b043-107"><a name = "create"></a>Créer une machine virtuelle avec plusieurs adresses IP</span><span class="sxs-lookup"><span data-stu-id="5b043-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="5b043-108">Vous pouvez effectuer cette tâche à l’aide d’Azure CLI 1.0 (cet article) ou d’[Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5b043-108">You can complete this task using the Azure CLI 1.0 (this article) or the [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span></span> <span data-ttu-id="5b043-109">Les étapes qui suivent expliquent comment créer un exemple de machine virtuelle avec plusieurs adresses IP, comme décrit dans le scénario.</span><span class="sxs-lookup"><span data-stu-id="5b043-109">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="5b043-110">Modifiez les noms des variables et les types d’adresses IP en fonction des besoins de votre implémentation.</span><span class="sxs-lookup"><span data-stu-id="5b043-110">Change variable names and IP address types as required for your implementation.</span></span>

1. <span data-ttu-id="5b043-111">Installez et configurez Azure CLI 1.0 en suivant les étapes décrites dans l’article [Installer et configurer l’interface de ligne de commande Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) et connectez-vous à votre compte Azure par le biais de la commande `azure-login`.</span><span class="sxs-lookup"><span data-stu-id="5b043-111">Install and configure the Azure CLI 1.0 by following the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account with the `azure-login` command.</span></span>

2. <span data-ttu-id="5b043-112">Créez un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="5b043-112">Create a resource group:</span></span>
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. <span data-ttu-id="5b043-113">Créez un réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="5b043-113">Create a virtual network:</span></span>

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. <span data-ttu-id="5b043-114">Créez un sous-réseau dans le réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="5b043-114">Create a subnet in the virtual network:</span></span>

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. <span data-ttu-id="5b043-115">Créez un compte de stockage pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5b043-115">Create  a storage account for the VM.</span></span> <span data-ttu-id="5b043-116">Avant d’exécuter la commande suivante, remplacez *mystorageaccount* par un nom unique.</span><span class="sxs-lookup"><span data-stu-id="5b043-116">Before running the following command, replace *mystorageaccount* with a unique name.</span></span> <span data-ttu-id="5b043-117">Le nom doit être unique dans tout Azure :</span><span class="sxs-lookup"><span data-stu-id="5b043-117">The name must be unique across Azure:</span></span>

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. <span data-ttu-id="5b043-118">Créez les configurations IP, une carte réseau et affectez des configurations IP à la carte réseau.</span><span class="sxs-lookup"><span data-stu-id="5b043-118">Create the IP configurations, a NIC, and assign the IP configurations to the NIC.</span></span> <span data-ttu-id="5b043-119">Vous pouvez ajouter, supprimer ou modifier les configurations selon les besoins.</span><span class="sxs-lookup"><span data-stu-id="5b043-119">You can add, remove, or change the configurations as necessary.</span></span> <span data-ttu-id="5b043-120">Les configurations décrites dans le scénario sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="5b043-120">The following configurations are described in the scenario:</span></span>

    <span data-ttu-id="5b043-121">**IPConfig-1**</span><span class="sxs-lookup"><span data-stu-id="5b043-121">**IPConfig-1**</span></span>

    <span data-ttu-id="5b043-122">Entrez les commandes suivantes pour créer :</span><span class="sxs-lookup"><span data-stu-id="5b043-122">Enter the commands that follow to create:</span></span>

    - <span data-ttu-id="5b043-123">une ressource d’adresse IP publique avec une adresse IP publique statique ;</span><span class="sxs-lookup"><span data-stu-id="5b043-123">A public IP address resource with a static public IP address</span></span>
    - <span data-ttu-id="5b043-124">une carte réseau, en lui affectant l’adresse IP publique et une adresse IP privée statique.</span><span class="sxs-lookup"><span data-stu-id="5b043-124">A NIC, assigning the public IP address and a static private IP address to it.</span></span>
    
    <span data-ttu-id="5b043-125">Remplacez *mypublicdns* par un nom qui est unique dans l’emplacement Azure.</span><span class="sxs-lookup"><span data-stu-id="5b043-125">Replace *mypublicdns* with a name that is unique within the Azure location.</span></span>

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > <span data-ttu-id="5b043-126">Les adresses IP publiques ont un coût nominal.</span><span class="sxs-lookup"><span data-stu-id="5b043-126">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="5b043-127">Pour en savoir plus, lisez la page [Tarification des adresses IP](https://azure.microsoft.com/pricing/details/ip-addresses) .</span><span class="sxs-lookup"><span data-stu-id="5b043-127">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="5b043-128">Il existe une limite au nombre d’adresses IP publiques qui peuvent être utilisées dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="5b043-128">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="5b043-129">Pour plus d’informations sur les limites, voir [Limites d’Azure](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="5b043-129">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    <span data-ttu-id="5b043-130">**IPConfig-2**</span><span class="sxs-lookup"><span data-stu-id="5b043-130">**IPConfig-2**</span></span>

     <span data-ttu-id="5b043-131">Entrez les commandes suivantes pour créer une nouvelle ressource d’adresse IP publique et une nouvelle configuration IP avec une adresse IP publique statique et une adresse IP privée statique :</span><span class="sxs-lookup"><span data-stu-id="5b043-131">Enter the following commands to create a new public IP address resource and a new IP configuration with a static public IP address and a static private IP address:</span></span>
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    <span data-ttu-id="5b043-132">**IPConfig-3**</span><span class="sxs-lookup"><span data-stu-id="5b043-132">**IPConfig-3**</span></span>

    <span data-ttu-id="5b043-133">Entrez les commandes suivantes pour créer une configuration IP avec une adresse IP privée statique et aucune adresse IP publique :</span><span class="sxs-lookup"><span data-stu-id="5b043-133">Enter the following commands to create an IP configuration with a static private IP address and no public IP address:</span></span>

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    ><span data-ttu-id="5b043-134">Bien que cet article affecte toutes les configurations IP à une seule carte réseau, vous pouvez également affecter plusieurs configurations IP à une carte réseau dans une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5b043-134">Though this article assigns all IP configurations to a single NIC, you can also assign multiple IP configurations to any NIC in a VM.</span></span> <span data-ttu-id="5b043-135">Pour apprendre à créer une machine virtuelle avec plusieurs cartes d’interface réseau, lisez l’article Créer une machine virtuelle avec plusieurs cartes d’interface réseau.</span><span class="sxs-lookup"><span data-stu-id="5b043-135">To learn how to create a VM with multiple NICs, read the Create a VM with multiple NICs article.</span></span>

7. <span data-ttu-id="5b043-136">Créer une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="5b043-136">Create a Linux VM</span></span> 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    <span data-ttu-id="5b043-137">Pour modifier la taille de la machine virtuelle sur Standard DS2 v2, par exemple, ajoutez simplement la propriété suivante `--vm-size Standard_DS3_v2` à la commande `azure vm create` à l’étape 6.</span><span class="sxs-lookup"><span data-stu-id="5b043-137">To change the VM size to Standard DS2 v2, for example, simply add the following property `--vm-size Standard_DS3_v2` to the `azure vm create` command in step 6.</span></span>

8. <span data-ttu-id="5b043-138">Entrez la commande suivante pour afficher la carte d’interface réseau et les configurations IP associées :</span><span class="sxs-lookup"><span data-stu-id="5b043-138">Enter the following command to view the NIC and the associated IP configurations:</span></span>

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. <span data-ttu-id="5b043-139">Ajoutez les adresses IP privées pour le système d’exploitation de la machine virtuelle en suivant les étapes pour votre système d’exploitation dans la section [Ajouter des adresses IP à un système d’exploitation de machine virtuelle](#os-config) de cet article.</span><span class="sxs-lookup"><span data-stu-id="5b043-139">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="5b043-140"><a name="add"></a>Ajouter des adresses IP à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5b043-140"><a name="add"></a>Add IP addresses to a VM</span></span>

<span data-ttu-id="5b043-141">Vous pouvez ajouter des adresses IP privées et publiques à une carte réseau en suivant les étapes décrites ci-après.</span><span class="sxs-lookup"><span data-stu-id="5b043-141">You can add additional private and public IP addresses to an existing NIC by completing the steps that follow.</span></span> <span data-ttu-id="5b043-142">Les exemples reposent sur le [scénario](#Scenario) décrit dans cet article.</span><span class="sxs-lookup"><span data-stu-id="5b043-142">The examples build upon the [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="5b043-143">Ouvrez l’interface de ligne de commande Azure et effectuez les étapes restantes de cette section en une seule session CLI.</span><span class="sxs-lookup"><span data-stu-id="5b043-143">Open Azure CLI and complete the remaining steps in this section within a single CLI session.</span></span> <span data-ttu-id="5b043-144">Si l’interface de ligne de commande Azure n’est pas encore installée et configurée, suivez les étapes décrites dans l’article [Installer et configurer l’interface de ligne de commande Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) et connectez-vous à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="5b043-144">If you don't already have Azure CLI installed and configured, complete the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account.</span></span>

2. <span data-ttu-id="5b043-145">Suivez les étapes de l’une des sections suivantes, selon vos besoins :</span><span class="sxs-lookup"><span data-stu-id="5b043-145">Complete the steps in one of the following sections, based on your requirements:</span></span>

    - <span data-ttu-id="5b043-146">**Ajouter une adresse IP privée**</span><span class="sxs-lookup"><span data-stu-id="5b043-146">**Add a private IP address**</span></span>
    
        <span data-ttu-id="5b043-147">Pour ajouter une adresse IP privée à une carte d’interface réseau, vous devez créer une configuration IP à l’aide de la commande ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="5b043-147">To add a private IP address to a NIC, you must create an IP configuration using the command below.</span></span> <span data-ttu-id="5b043-148">L’adresse statique doit être une adresse non utilisée pour le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="5b043-148">The static address must be an unused address for the subnet.</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        <span data-ttu-id="5b043-149">Créez autant de configurations que nécessaire, à l’aide de noms de configuration unique et d’adresses IP privées (pour les configurations avec des adresses IP statiques).</span><span class="sxs-lookup"><span data-stu-id="5b043-149">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    - <span data-ttu-id="5b043-150">**Ajouter une adresse IP publique**</span><span class="sxs-lookup"><span data-stu-id="5b043-150">**Add a public IP address**</span></span>
    
        <span data-ttu-id="5b043-151">Pour ajouter une adresse IP publique, associez-la à une configuration IP nouvelle ou existante.</span><span class="sxs-lookup"><span data-stu-id="5b043-151">A public IP address is added by associating it to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="5b043-152">Suivez les étapes de l’une des sections ci-après, selon votre besoin.</span><span class="sxs-lookup"><span data-stu-id="5b043-152">Complete the steps in one of the sections that follow, as you require.</span></span>

        > [!NOTE]
        > <span data-ttu-id="5b043-153">Les adresses IP publiques ont un coût nominal.</span><span class="sxs-lookup"><span data-stu-id="5b043-153">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="5b043-154">Pour en savoir plus, lisez la page [Tarification des adresses IP](https://azure.microsoft.com/pricing/details/ip-addresses) .</span><span class="sxs-lookup"><span data-stu-id="5b043-154">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="5b043-155">Il existe une limite au nombre d’adresses IP publiques qui peuvent être utilisées dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="5b043-155">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="5b043-156">Pour plus d’informations sur les limites, voir [Limites d’Azure](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="5b043-156">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
        >

        <span data-ttu-id="5b043-157">**Associer la ressource à une nouvelle configuration IP**</span><span class="sxs-lookup"><span data-stu-id="5b043-157">**Associate the resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="5b043-158">Lorsque vous ajoutez une adresse IP publique dans une nouvelle configuration IP, vous devez également ajouter une adresse IP privée, car toutes les configurations IP doivent avoir une adresse IP privée.</span><span class="sxs-lookup"><span data-stu-id="5b043-158">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="5b043-159">Vous pouvez ajouter une ressource d’adresse IP publique existante ou en créer une.</span><span class="sxs-lookup"><span data-stu-id="5b043-159">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="5b043-160">Pour en créer une nouvelle, saisissez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5b043-160">To create a new one, enter the following command:</span></span>

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        <span data-ttu-id="5b043-161">Pour créer une nouvelle configuration IP avec une adresse IP privée statique et la ressource d’adresse IP publique *myPublicIP3*, saisissez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5b043-161">To create a new IP configuration with a static private IP address and the associated *myPublicIP3* public IP address resource, enter the following command:</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        <span data-ttu-id="5b043-162">**Association de la ressource à une configuration IP existante**</span><span class="sxs-lookup"><span data-stu-id="5b043-162">**Associate the resource to an existing IP configuration**</span></span>

        <span data-ttu-id="5b043-163">Une ressource d’adresse IP publique ne peut être associée qu’à une configuration IP n’ayant pas encore de ressource associée.</span><span class="sxs-lookup"><span data-stu-id="5b043-163">A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="5b043-164">Pour déterminer si une configuration IP a une adresse IP publique associée, entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5b043-164">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        <span data-ttu-id="5b043-165">Recherchez une ligne similaire à celle qui suit pour IPConfig-3 dans la sortie retournée :</span><span class="sxs-lookup"><span data-stu-id="5b043-165">Look for a line similar to the one that follows for IPConfig-3 in the returned output:</span></span>

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        <span data-ttu-id="5b043-166">Étant donné que l’**adresse IP publique** pour *IpConfig-3* est vide, aucune ressource d’adresse IP publique n’y est actuellement associée.</span><span class="sxs-lookup"><span data-stu-id="5b043-166">Since the **Public IP** column for *IpConfig-3* is blank, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="5b043-167">Vous pouvez ajouter une ressource d’adresse IP publique existante sur IpConfig-3, ou entrer la commande suivante pour en créer une :</span><span class="sxs-lookup"><span data-stu-id="5b043-167">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        <span data-ttu-id="5b043-168">Entrez la commande suivante pour associer la ressource d’adresse IP publique à la configuration IP existante nommée *IPConfig-3* :</span><span class="sxs-lookup"><span data-stu-id="5b043-168">Enter the following command to associate the public IP address resource to the existing IP configuration named *IPConfig-3*:</span></span>
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. <span data-ttu-id="5b043-169">Affichez les ressources d’adresses IP privées et d’adresse IP publique affectées à la carte réseau en entrant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5b043-169">View the private IP addresses and the public IP address resources assigned to the NIC by entering the following command:</span></span>

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      <span data-ttu-id="5b043-170">Le résultat retourné ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="5b043-170">The returned output is similar to the following:</span></span>
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. <span data-ttu-id="5b043-171">Ajoutez les adresses IP privées que vous avez ajoutées à l’interface réseau pour le système d’exploitation de la machine virtuelle en suivant les instructions fournies dans la section [Ajouter des adresses IP à un système d’exploitation de machine virtuelle](#os-config) de cet article.</span><span class="sxs-lookup"><span data-stu-id="5b043-171">Add the private IP addresses you added to the NIC to the VM operating system by following the instructions in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="5b043-172">N’ajoutez pas les adresses IP publiques au système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="5b043-172">Do not add the public IP addresses to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
