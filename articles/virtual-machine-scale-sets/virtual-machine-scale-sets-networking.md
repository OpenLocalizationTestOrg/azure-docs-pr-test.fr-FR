---
title: "Mise en réseau pour les groupes de machines virtuelles identiques Azure | Microsoft Docs"
description: "Propriétés de mise en réseau de configuration pour des groupes de machines virtuelles identiques Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: guybo
ms.openlocfilehash: a8520c6d8962cc362fc935f6b515a299c0ce75b3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a><span data-ttu-id="10213-103">Mise en réseau pour des groupes de machines virtuelles identiques Azure</span><span class="sxs-lookup"><span data-stu-id="10213-103">Networking for Azure virtual machine scale sets</span></span>

<span data-ttu-id="10213-104">Lorsque vous déployez un groupe de machines virtuelles identiques Azure via le portail, certaines propriétés de réseau sont définies par défaut, comme un équilibrage de charge Azure avec des règles NAT entrantes.</span><span class="sxs-lookup"><span data-stu-id="10213-104">When you deploy an Azure virtual machine scale set through the portal, certain network properties are defaulted, for example an Azure Load Balancer with inbound NAT rules.</span></span> <span data-ttu-id="10213-105">Cet article explique comment utiliser certaines des fonctionnalités avancées de mise en réseau, que vous pouvez configurer avec les groupes identiques.</span><span class="sxs-lookup"><span data-stu-id="10213-105">This article describes how to use some of the more advanced networking features that you can configure with scale sets.</span></span>

<span data-ttu-id="10213-106">Vous pouvez configurer toutes les fonctionnalités abordées dans cet article à l’aide des modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="10213-106">You can configure all of the features covered in this article using Azure Resource Manager templates.</span></span> <span data-ttu-id="10213-107">Des exemples d’interfaces de ligne de commande Azure et Powershell sont également inclus pour les fonctionnalités sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="10213-107">Azure CLI and PowerShell examples are also included for selected features.</span></span> <span data-ttu-id="10213-108">Utilisez CLI 2.10 et PowerShell 4.2.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="10213-108">Use CLI 2.10, and PowerShell 4.2.0 or later.</span></span>

## <a name="accelerated-networking"></a><span data-ttu-id="10213-109">Mise en réseau accélérée</span><span class="sxs-lookup"><span data-stu-id="10213-109">Accelerated Networking</span></span>
<span data-ttu-id="10213-110">La [mise en réseau accélérée](../virtual-network/virtual-network-create-vm-accelerated-networking.md) Azure améliore les performances du réseau en activant la virtualisation d’E/S de racine unique (SR-IOV) sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="10213-110">Azure [Accelerated Networking](../virtual-network/virtual-network-create-vm-accelerated-networking.md) improves  network performance by enabling single root I/O virtualization (SR-IOV) to a virtual machine.</span></span> <span data-ttu-id="10213-111">Pour utiliser la mise en réseau accélérée avec des groupes identiques, définissez enableAcceleratedNetworking sur **true** dans les paramètres networkInterfaceConfigurations du groupe identique.</span><span class="sxs-lookup"><span data-stu-id="10213-111">To use accelerated networking with scale sets, set enableAcceleratedNetworking to **true** in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="10213-112">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="10213-112">For example:</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
      "name": "niconfig1",
      "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
          ...
        ]
      }
    }
   ]
}
```

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a><span data-ttu-id="10213-113">Créer un groupe identique qui fait référence à un équilibrage de charge Azure existant</span><span class="sxs-lookup"><span data-stu-id="10213-113">Create a scale set that references an existing Azure Load Balancer</span></span>
<span data-ttu-id="10213-114">Lorsqu’un groupe identique est créé à l’aide du portail Azure, un nouvel équilibrage de charge est créé pour la plupart des options de configuration.</span><span class="sxs-lookup"><span data-stu-id="10213-114">When a scale set is created using the Azure portal, a new load balancer is created for most configuration options.</span></span> <span data-ttu-id="10213-115">Si vous créez un groupe identique qui doit faire référence à un équilibrage de charge existant, vous pouvez le faire à l’aide d’une interface CLI.</span><span class="sxs-lookup"><span data-stu-id="10213-115">If you create a scale set, which needs to reference an existing load balancer, you can do this using CLI.</span></span> <span data-ttu-id="10213-116">L’exemple de script suivant crée un équilibrage de charge et crée ensuite un groupe identique qui y fait référence :</span><span class="sxs-lookup"><span data-stu-id="10213-116">The following example script creates a load balancer and then creates a scale set, which references it:</span></span>
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a><span data-ttu-id="10213-117">Paramètres DNS configurables</span><span class="sxs-lookup"><span data-stu-id="10213-117">Configurable DNS Settings</span></span>
<span data-ttu-id="10213-118">Par défaut, les groupes identiques adoptent les paramètres DNS spécifiques du réseau virtuel et du sous-réseau dans lesquels ils ont été créés.</span><span class="sxs-lookup"><span data-stu-id="10213-118">By default, scale sets take on the specific DNS settings of the VNET and subnet they were created in.</span></span> <span data-ttu-id="10213-119">Toutefois, vous pouvez configurer les paramètres DNS directement pour un groupe identique.</span><span class="sxs-lookup"><span data-stu-id="10213-119">You can however, configure the DNS settings for a scale set directly.</span></span>
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a><span data-ttu-id="10213-120">Création d’un groupe identique avec les serveurs DNS configurables</span><span class="sxs-lookup"><span data-stu-id="10213-120">Creating a scale set with configurable DNS servers</span></span>
<span data-ttu-id="10213-121">Pour créer un groupe identique avec une configuration DNS personnalisée à l’aide de CLI 2.0, ajoutez l’argument **--dns-servers** à la commande **vmss create**, suivi des adresses IP des serveurs, séparées par un espace.</span><span class="sxs-lookup"><span data-stu-id="10213-121">To create a scale set with a custom DNS configuration using CLI 2.0, add the **--dns-servers** argument to the **vmss create** command, followed by space separated server ip addresses.</span></span> <span data-ttu-id="10213-122">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="10213-122">For example:</span></span>
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
<span data-ttu-id="10213-123">Pour configurer des serveurs DNS personnalisés dans un modèle Azure, ajoutez une propriété dnsSettings à la section networkInterfaceConfigurations du groupe identique.</span><span class="sxs-lookup"><span data-stu-id="10213-123">To configure custom DNS servers in an Azure template, add a dnsSettings property to the scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="10213-124">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="10213-124">For example:</span></span>
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a><span data-ttu-id="10213-125">Création d’un groupe identique avec des noms de domaine de machines virtuelles configurables</span><span class="sxs-lookup"><span data-stu-id="10213-125">Creating a scale set with configurable virtual machine domain names</span></span>
<span data-ttu-id="10213-126">Pour créer un groupe identique avec un nom DNS personnalisé pour des machines virtuelles avec CLI 2.0, ajoutez l’argument **--vm-domain-name** à la commande **vmss create**, suivi d’une chaîne représentant le nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="10213-126">To create a scale set with a custom DNS name for virtual machines using CLI 2.0, add the **--vm-domain-name** argument to the **vmss create** command, followed by a string representing the domain name.</span></span>

<span data-ttu-id="10213-127">Pour définir le nom de domaine dans un modèle Azure, ajoutez une propriété **dnsSettings** à la section **networkInterfaceConfigurations** du groupe identique.</span><span class="sxs-lookup"><span data-stu-id="10213-127">To set the domain name in an Azure template, add a **dnsSettings** property to the scale set **networkInterfaceConfigurations** section.</span></span> <span data-ttu-id="10213-128">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="10213-128">For example:</span></span>

```json
"networkProfile": {
  "networkInterfaceConfigurations": [
    {
    "name": "nic1",
    "properties": {
      "primary": "true",
      "ipConfigurations": [
      {
        "name": "ip1",
        "properties": {
          "subnet": {
            "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
          },
          "publicIPAddressconfiguration": {
            "name": "publicip",
            "properties": {
            "idleTimeoutInMinutes": 10,
              "dnsSettings": {
                "domainNameLabel": "[parameters('vmssDnsName')]"
              }
            }
          }
        }
      }
    ]
    }
}
```

<span data-ttu-id="10213-129">Pour le nom dns d’une machine virtuelle individuelle, le résultat devrait être similaire à :</span><span class="sxs-lookup"><span data-stu-id="10213-129">The output, for an individual virtual machine dns name would be in the following form:</span></span> 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a><span data-ttu-id="10213-130">IPv4 publique par machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="10213-130">Public IPv4 per virtual machine</span></span>
<span data-ttu-id="10213-131">En règle générale, les machines virtuelles des groupes identiques Azure ne nécessitent pas leurs propres adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="10213-131">In general, Azure scale set virtual machines do not require their own public IP addresses.</span></span> <span data-ttu-id="10213-132">Dans la plupart des cas, l’association d’une adresse IP publique à un équilibrage de charge ou à une machine virtuelle individuelle (ou jumpbox) qui achemine les connexions entrantes vers les machines virtuelles de groupes identiques selon les besoins (par exemple, via des règles NAT entrantes) constitue une solution plus économique et plus sûre.</span><span class="sxs-lookup"><span data-stu-id="10213-132">For most scenarios, it is more economical and secure to associate a public IP address to a load balancer or to an individual virtual machine (aka a jumpbox), which then routes incoming connections to scale set virtual machines as needed (for example, through inbound NAT rules).</span></span>

<span data-ttu-id="10213-133">Toutefois, dans certains cas, les machines virtuelles de groupes identiques doivent posséder leurs propres adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="10213-133">However, some scenarios do require scale set virtual machines to have their own public IP addresses.</span></span> <span data-ttu-id="10213-134">Par exemple, dans le cas des jeux vidéo, lorsqu’une console doit être directement connectée à une machine virtuelle sur Cloud qui procède à un traitement physique du jeu.</span><span class="sxs-lookup"><span data-stu-id="10213-134">An example is gaming, where a console needs to make a direct connection to a cloud virtual machine, which is doing game physics processing.</span></span> <span data-ttu-id="10213-135">Autre exemple : lorsque des machines virtuelles doivent établir des connexions externes entre elles, dans différentes régions, dans une base de données distribuée.</span><span class="sxs-lookup"><span data-stu-id="10213-135">Another example is where virtual machines need to make external connections to one another across regions in a distributed database.</span></span>

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a><span data-ttu-id="10213-136">Création d’un groupe identique avec IP public par machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="10213-136">Creating a scale set with public IP per virtual machine</span></span>
<span data-ttu-id="10213-137">Pour créer un groupe identique qui attribue une adresse IP publique à chaque machine virtuelle avec CLI 2.0, ajoutez le paramètre **--public-ip-per-vm** à la commande **vmss create**.</span><span class="sxs-lookup"><span data-stu-id="10213-137">To create a scale set that assigns a public IP address to each virtual machine with CLI 2.0, add the **--public-ip-per-vm** parameter to the **vmss create** command.</span></span> 

<span data-ttu-id="10213-138">Pour créer un groupe identique à l’aide d’un modèle Azure, assurez-vous que la version API de la ressource Microsoft.Compute/virtualMachineScaleSets correspond au moins à la version du **30/03/2017**, et ajoutez une propriété JSON **publicIpAddressConfiguration** à la section ipConfigurations du groupe identique.</span><span class="sxs-lookup"><span data-stu-id="10213-138">To create a scale set using an Azure template, make sure the API version of the Microsoft.Compute/virtualMachineScaleSets resource is at least **2017-03-30**, and add a **publicIpAddressConfiguration** JSON property to the scale set ipConfigurations section.</span></span> <span data-ttu-id="10213-139">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="10213-139">For example:</span></span>

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
<span data-ttu-id="10213-140">Exemple de modèle : [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span><span class="sxs-lookup"><span data-stu-id="10213-140">Example template: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span></span>

### <a name="querying-the-public-ip-addresses-of-the-virtual-machines-in-a-scale-set"></a><span data-ttu-id="10213-141">Interrogation des adresses IP publiques des machines virtuelles dans un groupe identique</span><span class="sxs-lookup"><span data-stu-id="10213-141">Querying the public IP addresses of the virtual machines in a scale set</span></span>
<span data-ttu-id="10213-142">Pour répertorier les adresses IP publiques attribuées à des machines virtuelles d’un groupe identique avec CLI 2.0, utilisez la commande **az vmss list-instance-public-ips**.</span><span class="sxs-lookup"><span data-stu-id="10213-142">To list the public IP addresses assigned to scale set virtual machines using CLI 2.0, use the **az vmss list-instance-public-ips** command.</span></span>

<span data-ttu-id="10213-143">Pour répertorier les adresses IP publiques d’un groupe identique à l’aide de PowerShell, utilisez la commande _Get-AzureRmPublicIpAddress_.</span><span class="sxs-lookup"><span data-stu-id="10213-143">To list scale set public IP addresses using PowerShell, use the _Get-AzureRmPublicIpAddress_ command.</span></span> <span data-ttu-id="10213-144">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="10213-144">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

<span data-ttu-id="10213-145">Vous pouvez également interroger les adresses IP publiques en référençant directement l’ID de ressource de la configuration d’adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="10213-145">You can also query the public IP addresses by referencing the resource id of the public IP address configuration directly.</span></span> <span data-ttu-id="10213-146">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="10213-146">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

<span data-ttu-id="10213-147">Pour interroger les adresses IP publiques attribuées à des machines virtuelles d’un groupe identique en utilisant [Azure Resource Explorer](https://resources.azure.com) ou l’API REST Azure avec la version **30/03/2017** ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="10213-147">To query the public IP addresses assigned to scale set virtual machines using the [Azure Resource Explorer](https://resources.azure.com), or the Azure REST API with version **2017-03-30** or higher.</span></span>

<span data-ttu-id="10213-148">Pour afficher les adresses IP publiques pour un groupe identique avec Resource Explorer, reportez-vous à la section **publicipaddresses** de votre groupe identique.</span><span class="sxs-lookup"><span data-stu-id="10213-148">To view public IP addresses for a scale set using the Resource Explorer, look at the **publicipaddresses** section under your scale set.</span></span> <span data-ttu-id="10213-149">Par exemple : https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span><span class="sxs-lookup"><span data-stu-id="10213-149">For example: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span></span>

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

<span data-ttu-id="10213-150">Exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="10213-150">Example output:</span></span>
```json
{
  "value": [
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/pipvmss/virtualMachines/0/networkInterfaces/pipvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"a64060d5-4dea-4379-a11d-b23cd49a3c8d\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "ee8cb20f-af8e-4cd6-892f-441ae2bf701f",
        "ipAddress": "13.84.190.11",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/0/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    },
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"5f6ff30c-a24c-4818-883c-61ebd5f9eee8\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "036ce266-403f-41bd-8578-d446d7397c2f",
        "ipAddress": "13.84.159.176",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    }
```

## <a name="multiple-ip-addresses-per-nic"></a><span data-ttu-id="10213-151">Plusieurs adresses IP par carte réseau</span><span class="sxs-lookup"><span data-stu-id="10213-151">Multiple IP addresses per NIC</span></span>
<span data-ttu-id="10213-152">Une ou plusieurs configurations IP peuvent être associées à chaque carte réseau attachée à une machine virtuelle, dans un groupe identique.</span><span class="sxs-lookup"><span data-stu-id="10213-152">Every NIC attached to a VM in a scale set can have one or more IP configurations associated with it.</span></span> <span data-ttu-id="10213-153">Une adresse IP privée est affectée à chaque configuration.</span><span class="sxs-lookup"><span data-stu-id="10213-153">Each configuration is assigned one private IP address.</span></span> <span data-ttu-id="10213-154">Une ressource d’adresse IP publique peut également être associée à chaque configuration.</span><span class="sxs-lookup"><span data-stu-id="10213-154">Each configuration may also have one public IP address resource associated with it.</span></span> <span data-ttu-id="10213-155">Pour comprendre combien d’adresses IP peuvent être attribuées à une carte réseau et combien d’adresses IP publiques vous pouvez utiliser dans un abonnement Azure, consultez [Limites Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="10213-155">To understand how many IP addresses can be assigned to a NIC, and how many public IP addresses you can use in an Azure subscription, refer to [Azure limits](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span></span>

## <a name="multiple-nics-per-virtual-machine"></a><span data-ttu-id="10213-156">Plusieurs cartes réseau par machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="10213-156">Multiple NICs per virtual machine</span></span>
<span data-ttu-id="10213-157">Chaque machine virtuelle peut compter jusqu’à 8 cartes réseau, en fonction de la taille de la machine.</span><span class="sxs-lookup"><span data-stu-id="10213-157">You can have up to 8 NICs per virtual machine, depending on machine size.</span></span> <span data-ttu-id="10213-158">Le nombre maximal de cartes réseau par machine est indiqué dans l’[article sur la taille des machines virtuelles](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="10213-158">The maximum number of NICs per machine is available in the [VM size article](../virtual-machines/windows/sizes.md).</span></span> <span data-ttu-id="10213-159">L’exemple suivant est un profil réseau de groupe identique illustrant plusieurs entrées de cartes réseau et plusieurs adresses IP publiques par machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="10213-159">The following example is a scale set network profile showing multiple NIC entries, and multiple public IPs per virtual machine:</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
        "name": "nic1",
        "properties": {
            "primary": "true",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        },
        {
        "name": "nic2",
        "properties": {
            "primary": "false",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        }
    ]
}
```

## <a name="nsg-per-scale-set"></a><span data-ttu-id="10213-160">Groupes de sécurité réseau par groupe identique</span><span class="sxs-lookup"><span data-stu-id="10213-160">NSG per scale set</span></span>
<span data-ttu-id="10213-161">Des groupes de sécurité réseau peuvent être appliqués directement à un groupe identique en ajoutant une référence à la section de configuration de l’interface réseau des propriétés des machines virtuelles du groupe identique.</span><span class="sxs-lookup"><span data-stu-id="10213-161">Network Security Groups can be applied directly to a scale set, by adding a reference to the network interface configuration section of the scale set virtual machine properties.</span></span>

<span data-ttu-id="10213-162">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="10213-162">For example:</span></span> 
```
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="10213-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="10213-163">Next steps</span></span>
<span data-ttu-id="10213-164">Pour plus d’informations sur les réseaux virtuels Azure, consultez cette [documentation](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="10213-164">For more information about Azure virtual networks, refer to [this documentation](../virtual-network/virtual-networks-overview.md).</span></span>
