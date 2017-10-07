---
title: "aaaNetworking pour les jeux de mise à l’échelle de machine virtuelle Azure | Documents Microsoft"
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
ms.openlocfilehash: ef3f0cfe648d2195c051a73987e654f0e15d13bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a><span data-ttu-id="558e3-103">Mise en réseau pour des groupes de machines virtuelles identiques Azure</span><span class="sxs-lookup"><span data-stu-id="558e3-103">Networking for Azure virtual machine scale sets</span></span>

<span data-ttu-id="558e3-104">Lorsque vous déployez une échelle de machine virtuelle Azure définie via le portail de hello, certaines propriétés de réseau sont par défaut, par exemple un équilibrage de charge Azure avec des règles de trafic entrant NAT.</span><span class="sxs-lookup"><span data-stu-id="558e3-104">When you deploy an Azure virtual machine scale set through hello portal, certain network properties are defaulted, for example an Azure Load Balancer with inbound NAT rules.</span></span> <span data-ttu-id="558e3-105">Cet article décrit comment toouse certaines hello des fonctionnalités réseau que vous pouvez configurer avec une échelle plus avancées définit.</span><span class="sxs-lookup"><span data-stu-id="558e3-105">This article describes how toouse some of hello more advanced networking features that you can configure with scale sets.</span></span>

<span data-ttu-id="558e3-106">Vous pouvez configurer toutes les fonctionnalités de hello abordées dans cet article à l’aide de modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="558e3-106">You can configure all of hello features covered in this article using Azure Resource Manager templates.</span></span> <span data-ttu-id="558e3-107">Des exemples d’interfaces de ligne de commande Azure et Powershell sont également inclus pour les fonctionnalités sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="558e3-107">Azure CLI and PowerShell examples are also included for selected features.</span></span> <span data-ttu-id="558e3-108">Utilisez CLI 2.10 et PowerShell 4.2.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="558e3-108">Use CLI 2.10, and PowerShell 4.2.0 or later.</span></span>

## <a name="accelerated-networking"></a><span data-ttu-id="558e3-109">Mise en réseau accélérée</span><span class="sxs-lookup"><span data-stu-id="558e3-109">Accelerated Networking</span></span>
<span data-ttu-id="558e3-110">Azure [Accelerated réseau](../virtual-network/virtual-network-create-vm-accelerated-networking.md) améliore les performances du réseau en e/s de racine unique (SR-IOV) de la virtualisation tooa virtual machine.</span><span class="sxs-lookup"><span data-stu-id="558e3-110">Azure [Accelerated Networking](../virtual-network/virtual-network-create-vm-accelerated-networking.md) improves  network performance by enabling single root I/O virtualization (SR-IOV) tooa virtual machine.</span></span> <span data-ttu-id="558e3-111">toouse accelerated mise en réseau avec des jeux de mise à l’échelle, définissez enableAcceleratedNetworking trop**true** dans les paramètres des configurations de votre jeu de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="558e3-111">toouse accelerated networking with scale sets, set enableAcceleratedNetworking too**true** in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="558e3-112">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="558e3-112">For example:</span></span>
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

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a><span data-ttu-id="558e3-113">Créer un groupe identique qui fait référence à un équilibrage de charge Azure existant</span><span class="sxs-lookup"><span data-stu-id="558e3-113">Create a scale set that references an existing Azure Load Balancer</span></span>
<span data-ttu-id="558e3-114">Lorsqu’un ensemble d’échelle est créé à l’aide de hello portail Azure, un nouvel équilibrage de charge est créé pour la plupart des options de configuration.</span><span class="sxs-lookup"><span data-stu-id="558e3-114">When a scale set is created using hello Azure portal, a new load balancer is created for most configuration options.</span></span> <span data-ttu-id="558e3-115">Si vous créez un ensemble d’échelle, qui doit tooreference un équilibrage de charge existante, procéder à l’aide de CLI.</span><span class="sxs-lookup"><span data-stu-id="558e3-115">If you create a scale set, which needs tooreference an existing load balancer, you can do this using CLI.</span></span> <span data-ttu-id="558e3-116">Hello, exemple de script suivant crée un équilibreur de charge, puis crée un ensemble d’échelle, ce qui fait référence :</span><span class="sxs-lookup"><span data-stu-id="558e3-116">hello following example script creates a load balancer and then creates a scale set, which references it:</span></span>
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a><span data-ttu-id="558e3-117">Paramètres DNS configurables</span><span class="sxs-lookup"><span data-stu-id="558e3-117">Configurable DNS Settings</span></span>
<span data-ttu-id="558e3-118">Par défaut, les groupes identiques de prennent les paramètres DNS spécifiques hello hello réseau virtuel et sous-réseau qu’ils ont été créés dans.</span><span class="sxs-lookup"><span data-stu-id="558e3-118">By default, scale sets take on hello specific DNS settings of hello VNET and subnet they were created in.</span></span> <span data-ttu-id="558e3-119">Toutefois, vous pouvez configurer les paramètres DNS de hello pour une échelle définie directement.</span><span class="sxs-lookup"><span data-stu-id="558e3-119">You can however, configure hello DNS settings for a scale set directly.</span></span>
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a><span data-ttu-id="558e3-120">Création d’un groupe identique avec les serveurs DNS configurables</span><span class="sxs-lookup"><span data-stu-id="558e3-120">Creating a scale set with configurable DNS servers</span></span>
<span data-ttu-id="558e3-121">toocreate une échelle définie avec une configuration DNS personnalisée à l’aide de la version 2.0 CLI, ajoutez hello **serveurs dns--** argument toohello **mise créer** commande, suivi par un espace séparées par des adresses ip de serveur.</span><span class="sxs-lookup"><span data-stu-id="558e3-121">toocreate a scale set with a custom DNS configuration using CLI 2.0, add hello **--dns-servers** argument toohello **vmss create** command, followed by space separated server ip addresses.</span></span> <span data-ttu-id="558e3-122">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="558e3-122">For example:</span></span>
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
<span data-ttu-id="558e3-123">tooconfigure des serveurs DNS personnalisés dans un modèle Azure, ajouter la section des configurations du jeu d’une échelle de toohello de propriété de paramètres DNS.</span><span class="sxs-lookup"><span data-stu-id="558e3-123">tooconfigure custom DNS servers in an Azure template, add a dnsSettings property toohello scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="558e3-124">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="558e3-124">For example:</span></span>
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a><span data-ttu-id="558e3-125">Création d’un groupe identique avec des noms de domaine de machines virtuelles configurables</span><span class="sxs-lookup"><span data-stu-id="558e3-125">Creating a scale set with configurable virtual machine domain names</span></span>
<span data-ttu-id="558e3-126">toocreate une échelle définie avec un nom DNS personnalisé pour les ordinateurs virtuels à l’aide de la version 2.0 CLI, ajoutez hello **vm--nom de domaine** argument toohello **mise créer** commande, suivi d’une chaîne représentant le nom de domaine hello.</span><span class="sxs-lookup"><span data-stu-id="558e3-126">toocreate a scale set with a custom DNS name for virtual machines using CLI 2.0, add hello **--vm-domain-name** argument toohello **vmss create** command, followed by a string representing hello domain name.</span></span>

<span data-ttu-id="558e3-127">nom de domaine tooset hello dans un modèle Azure, ajoutez un **dnsSettings** ensemble d’échelle de propriété toohello **configurations** section.</span><span class="sxs-lookup"><span data-stu-id="558e3-127">tooset hello domain name in an Azure template, add a **dnsSettings** property toohello scale set **networkInterfaceConfigurations** section.</span></span> <span data-ttu-id="558e3-128">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="558e3-128">For example:</span></span>

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

<span data-ttu-id="558e3-129">sortie Hello, d’un nom dns de chaque machine virtuelle serait Bonjour suivant du formulaire :</span><span class="sxs-lookup"><span data-stu-id="558e3-129">hello output, for an individual virtual machine dns name would be in hello following form:</span></span> 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a><span data-ttu-id="558e3-130">IPv4 publique par machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="558e3-130">Public IPv4 per virtual machine</span></span>
<span data-ttu-id="558e3-131">En règle générale, les machines virtuelles des groupes identiques Azure ne nécessitent pas leurs propres adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="558e3-131">In general, Azure scale set virtual machines do not require their own public IP addresses.</span></span> <span data-ttu-id="558e3-132">La plupart des scénarios, il est plus économique et plus sûre tooassociate un public IP adresse tooa charge équilibrage tooan individuel ordinateur virtuel ou (également appelé jumpbox), qui achemine ensuite entrant connexions tooscale ensemble les ordinateurs virtuels en fonction des besoins (par exemple, via règles NAT entrantes).</span><span class="sxs-lookup"><span data-stu-id="558e3-132">For most scenarios, it is more economical and secure tooassociate a public IP address tooa load balancer or tooan individual virtual machine (aka a jumpbox), which then routes incoming connections tooscale set virtual machines as needed (for example, through inbound NAT rules).</span></span>

<span data-ttu-id="558e3-133">Toutefois, certains scénarios nécessitent ensemble d’échelle de machines virtuelles toohave leur propre adresse IP publique adresses.</span><span class="sxs-lookup"><span data-stu-id="558e3-133">However, some scenarios do require scale set virtual machines toohave their own public IP addresses.</span></span> <span data-ttu-id="558e3-134">Un exemple de jeu, où une console doit toomake une connexion directe tooa cloud machine, qui effectue le traitement du jeu physique.</span><span class="sxs-lookup"><span data-stu-id="558e3-134">An example is gaming, where a console needs toomake a direct connection tooa cloud virtual machine, which is doing game physics processing.</span></span> <span data-ttu-id="558e3-135">Un autre exemple est où les ordinateurs virtuels doivent toomake connexions externes tooone autre régions dans une base de données distribuée.</span><span class="sxs-lookup"><span data-stu-id="558e3-135">Another example is where virtual machines need toomake external connections tooone another across regions in a distributed database.</span></span>

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a><span data-ttu-id="558e3-136">Création d’un groupe identique avec IP public par machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="558e3-136">Creating a scale set with public IP per virtual machine</span></span>
<span data-ttu-id="558e3-137">toocreate un ensemble d’échelle qui affecte un ordinateur virtuel des tooeach d’adresse publique IP CLI 2.0, ajouter hello **--public-ip-par-vm** paramètre toohello **mise créer** commande.</span><span class="sxs-lookup"><span data-stu-id="558e3-137">toocreate a scale set that assigns a public IP address tooeach virtual machine with CLI 2.0, add hello **--public-ip-per-vm** parameter toohello **vmss create** command.</span></span> 

<span data-ttu-id="558e3-138">toocreate une échelle définie à l’aide d’un modèle Azure, vérifiez que hello API version de hello Microsoft.Compute/virtualMachineScaleSets ressource est au moins **2017-03-30**et ajoutez un **publicIpAddressConfiguration**Toohello l’échelle de la propriété JSON définie la section de configurations IP.</span><span class="sxs-lookup"><span data-stu-id="558e3-138">toocreate a scale set using an Azure template, make sure hello API version of hello Microsoft.Compute/virtualMachineScaleSets resource is at least **2017-03-30**, and add a **publicIpAddressConfiguration** JSON property toohello scale set ipConfigurations section.</span></span> <span data-ttu-id="558e3-139">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="558e3-139">For example:</span></span>

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
<span data-ttu-id="558e3-140">Exemple de modèle : [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span><span class="sxs-lookup"><span data-stu-id="558e3-140">Example template: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span></span>

### <a name="querying-hello-public-ip-addresses-of-hello-virtual-machines-in-a-scale-set"></a><span data-ttu-id="558e3-141">Adresse IP publique hello l’interrogation du jeu d’ordinateurs virtuels hello dans une échelle des adresses</span><span class="sxs-lookup"><span data-stu-id="558e3-141">Querying hello public IP addresses of hello virtual machines in a scale set</span></span>
<span data-ttu-id="558e3-142">des adresses IP publiques toolist hello affecté tooscale virtuels ensemble à l’aide de la version 2.0 CLI, utilisez hello **az mise liste-instance-public-IP** commande.</span><span class="sxs-lookup"><span data-stu-id="558e3-142">toolist hello public IP addresses assigned tooscale set virtual machines using CLI 2.0, use hello **az vmss list-instance-public-ips** command.</span></span>

<span data-ttu-id="558e3-143">mise à l’échelle toolist définie les adresses IP publiques à l’aide de PowerShell, utilisez les hello _Get-AzureRmPublicIpAddress_ commande.</span><span class="sxs-lookup"><span data-stu-id="558e3-143">toolist scale set public IP addresses using PowerShell, use hello _Get-AzureRmPublicIpAddress_ command.</span></span> <span data-ttu-id="558e3-144">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="558e3-144">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

<span data-ttu-id="558e3-145">Vous pouvez également des adresses IP publiques requête hello en référençant directement les id de ressource de hello de configuration d’adresse IP publique hello.</span><span class="sxs-lookup"><span data-stu-id="558e3-145">You can also query hello public IP addresses by referencing hello resource id of hello public IP address configuration directly.</span></span> <span data-ttu-id="558e3-146">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="558e3-146">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

<span data-ttu-id="558e3-147">attribuer des adresses IP publiques de tooquery hello tooscale virtuels ensemble à l’aide de hello [Explorateur de ressources Azure](https://resources.azure.com), ou hello API REST Azure avec la version **2017-03-30** ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="558e3-147">tooquery hello public IP addresses assigned tooscale set virtual machines using hello [Azure Resource Explorer](https://resources.azure.com), or hello Azure REST API with version **2017-03-30** or higher.</span></span>

<span data-ttu-id="558e3-148">tooview des adresses IP publiques pour une échelle définie à l’aide de l’Explorateur de ressources, de hello examiner hello **publicipaddresses** section sous votre ensemble d’échelle.</span><span class="sxs-lookup"><span data-stu-id="558e3-148">tooview public IP addresses for a scale set using hello Resource Explorer, look at hello **publicipaddresses** section under your scale set.</span></span> <span data-ttu-id="558e3-149">Par exemple : https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span><span class="sxs-lookup"><span data-stu-id="558e3-149">For example: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span></span>

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

<span data-ttu-id="558e3-150">Exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="558e3-150">Example output:</span></span>
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

## <a name="multiple-ip-addresses-per-nic"></a><span data-ttu-id="558e3-151">Plusieurs adresses IP par carte réseau</span><span class="sxs-lookup"><span data-stu-id="558e3-151">Multiple IP addresses per NIC</span></span>
<span data-ttu-id="558e3-152">Chaque carte réseau attachée tooa que machine virtuelle dans un ensemble d’échelle peut avoir une ou plusieurs configurations IP associées.</span><span class="sxs-lookup"><span data-stu-id="558e3-152">Every NIC attached tooa VM in a scale set can have one or more IP configurations associated with it.</span></span> <span data-ttu-id="558e3-153">Une adresse IP privée est affectée à chaque configuration.</span><span class="sxs-lookup"><span data-stu-id="558e3-153">Each configuration is assigned one private IP address.</span></span> <span data-ttu-id="558e3-154">Une ressource d’adresse IP publique peut également être associée à chaque configuration.</span><span class="sxs-lookup"><span data-stu-id="558e3-154">Each configuration may also have one public IP address resource associated with it.</span></span> <span data-ttu-id="558e3-155">toounderstand le nombre d’adresses IP peut être affectée tooa carte réseau, et le nombre d’adresses IP publique que vous pouvez utiliser dans un abonnement Azure, consultez trop[limite Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="558e3-155">toounderstand how many IP addresses can be assigned tooa NIC, and how many public IP addresses you can use in an Azure subscription, refer too[Azure limits](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span></span>

## <a name="multiple-nics-per-virtual-machine"></a><span data-ttu-id="558e3-156">Plusieurs cartes réseau par machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="558e3-156">Multiple NICs per virtual machine</span></span>
<span data-ttu-id="558e3-157">Vous pouvez avoir des cartes réseau de too8 par machine virtuelle, en fonction de la taille de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="558e3-157">You can have up too8 NICs per virtual machine, depending on machine size.</span></span> <span data-ttu-id="558e3-158">Hello de nombre maximal de cartes réseau par machine est disponible dans hello [article de taille de machine virtuelle](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="558e3-158">hello maximum number of NICs per machine is available in hello [VM size article](../virtual-machines/windows/sizes.md).</span></span> <span data-ttu-id="558e3-159">Hello exemple suivant est qu'une échelle de définie le profil réseau affichant plusieurs entrées de la carte réseau et plusieurs adresses IP publiques par machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="558e3-159">hello following example is a scale set network profile showing multiple NIC entries, and multiple public IPs per virtual machine:</span></span>
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

## <a name="nsg-per-scale-set"></a><span data-ttu-id="558e3-160">Groupes de sécurité réseau par groupe identique</span><span class="sxs-lookup"><span data-stu-id="558e3-160">NSG per scale set</span></span>
<span data-ttu-id="558e3-161">Groupes de sécurité réseau peuvent être appliqués directement tooa un ensemble d’échelle, en ajoutant une section de configuration de référence toohello network interface de montée en puissance hello définie des propriétés de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="558e3-161">Network Security Groups can be applied directly tooa scale set, by adding a reference toohello network interface configuration section of hello scale set virtual machine properties.</span></span>

<span data-ttu-id="558e3-162">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="558e3-162">For example:</span></span> 
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

## <a name="next-steps"></a><span data-ttu-id="558e3-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="558e3-163">Next steps</span></span>
<span data-ttu-id="558e3-164">Pour plus d’informations sur les réseaux virtuels Azure, consultez trop[cette documentation](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="558e3-164">For more information about Azure virtual networks, refer too[this documentation](../virtual-network/virtual-networks-overview.md).</span></span>
