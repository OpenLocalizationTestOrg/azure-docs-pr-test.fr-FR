---
title: aaaCreate un environnement Linux avec hello Azure CLI 2.0 | Documents Microsoft
description: "Créer des stockage, un VM Linux, un réseau virtuel et du sous-réseau, un équilibreur de charge, une carte réseau, une adresse IP publique et un groupe de sécurité réseau, tous les à partir de hello d’arrière-plan à l’aide de hello Azure CLI 2.0."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: 7287ea178e76001b84dade628ead04a59dc27f40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="2d938-103">Créer une machine virtuelle de Linux complète avec hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="2d938-103">Create a complete Linux virtual machine with hello Azure CLI</span></span>
<span data-ttu-id="2d938-104">tooquickly créer un ordinateur virtuel (VM) dans Azure, vous pouvez utiliser une seule commande CLI d’Azure qui utilise toocreate de valeurs par défaut tout requis prenant en charge des ressources.</span><span class="sxs-lookup"><span data-stu-id="2d938-104">tooquickly create a virtual machine (VM) in Azure, you can use a single Azure CLI command that uses default values toocreate any required supporting resources.</span></span> <span data-ttu-id="2d938-105">Les ressources telles que le réseau virtuel, l’adresse IP publique et les règles de groupe de sécurité réseau sont automatiquement créées.</span><span class="sxs-lookup"><span data-stu-id="2d938-105">Resources such as a virtual network, public IP address, and network security group rules are automatically created.</span></span> <span data-ttu-id="2d938-106">Pour plus de contrôle de votre environnement de production, utilisez, vous pouvez créer ces ressources à l’avance et puis ajoutez votre toothem de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2d938-106">For more control of your environment in production use, you may create these resources ahead of time and then add your VMs toothem.</span></span> <span data-ttu-id="2d938-107">Cet article vous guide tout au long de la toocreate une machine virtuelle et à chacun des hello une par une des ressources de support.</span><span class="sxs-lookup"><span data-stu-id="2d938-107">This article guides you through how toocreate a VM and each of hello supporting resources one by one.</span></span>

<span data-ttu-id="2d938-108">Assurez-vous que vous avez installé hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et le compte connecté tooan Azure avec [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="2d938-108">Make sure that you have installed hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and logged tooan Azure account in with [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="2d938-109">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="2d938-109">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="2d938-110">Les noms de paramètre sont par exemple *myResourceGroup*, *myVnet* et *myVM*.</span><span class="sxs-lookup"><span data-stu-id="2d938-110">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="2d938-111">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="2d938-111">Create resource group</span></span>
<span data-ttu-id="2d938-112">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="2d938-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="2d938-113">Un groupe de ressources doit être créé avant la machine virtuelle et les ressources de réseau virtuel associées.</span><span class="sxs-lookup"><span data-stu-id="2d938-113">A resource group must be created before a virtual machine and supporting virtual network resources.</span></span> <span data-ttu-id="2d938-114">Créer le groupe de ressources hello avec [az groupe créer](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="2d938-114">Create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="2d938-115">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="2d938-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="2d938-116">Par défaut, la sortie de hello des commandes CLI d’Azure est au format JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="2d938-116">By default, hello output of Azure CLI commands is in JSON (JavaScript Object Notation).</span></span> <span data-ttu-id="2d938-117">liste de tooa sortie toochange hello par défaut ou une table, par exemple, utilisez [az configurer--sortie](/cli/azure/#configure).</span><span class="sxs-lookup"><span data-stu-id="2d938-117">toochange hello default output tooa list or table, for example, use [az configure --output](/cli/azure/#configure).</span></span> <span data-ttu-id="2d938-118">Vous pouvez également ajouter `--output` commande tooany pour une seule fois modifier dans le format de sortie.</span><span class="sxs-lookup"><span data-stu-id="2d938-118">You can also add `--output` tooany command for a one time change in output format.</span></span> <span data-ttu-id="2d938-119">Hello suivant montre la sortie JSON hello de hello `az group create` commande :</span><span class="sxs-lookup"><span data-stu-id="2d938-119">hello following example shows hello JSON output from hello `az group create` command:</span></span>

```json                       
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "location": "eastus",
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="2d938-120">Créer un réseau virtuel et un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="2d938-120">Create a virtual network and subnet</span></span>
<span data-ttu-id="2d938-121">Ensuite, vous créez un réseau virtuel dans Azure et un sous-réseau dans toowhich, vous pouvez créer vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2d938-121">Next you create a virtual network in Azure and a subnet in toowhich you can create your VMs.</span></span> <span data-ttu-id="2d938-122">Utilisez [créer un réseau virtuel du réseau az](/cli/azure/network/vnet#create) toocreate un réseau virtuel nommé *myVnet* avec hello *192.168.0.0/16* préfixe d’adresse.</span><span class="sxs-lookup"><span data-stu-id="2d938-122">Use [az network vnet create](/cli/azure/network/vnet#create) toocreate a virtual network named *myVnet* with hello *192.168.0.0/16* address prefix.</span></span> <span data-ttu-id="2d938-123">Ajoutez un sous-réseau nommé *mySubnet* avec le préfixe d’adresse de hello *192.168.1.0/24*:</span><span class="sxs-lookup"><span data-stu-id="2d938-123">You also add a subnet named *mySubnet* with hello address prefix of *192.168.1.0/24*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="2d938-124">sortie de Hello montre sous-réseau hello comme logiquement créé à l’intérieur du réseau virtuel de hello :</span><span class="sxs-lookup"><span data-stu-id="2d938-124">hello output shows hello subnet as logically created inside hello virtual network:</span></span>

```json
{
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "location": "eastus",
  "name": "myVnet",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "ed62fd03-e9de-430b-84df-8a3b87cacdbb",
  "subnets": [
    {
      "addressPrefix": "192.168.1.0/24",
      "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
      "ipConfigurations": null,
      "name": "mySubnet",
      "networkSecurityGroup": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  "tags": {},
  "type": "Microsoft.Network/virtualNetworks",
  "virtualNetworkPeerings": null
}
```


## <a name="create-a-public-ip-address"></a><span data-ttu-id="2d938-125">Créer une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="2d938-125">Create a public IP address</span></span>
<span data-ttu-id="2d938-126">Créons à présent une adresse IP publique avec la commande [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="2d938-126">Now let's create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="2d938-127">Cette adresse IP publique permet de vous tooconnect tooyour machines virtuelles à partir de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="2d938-127">This public IP address enables you tooconnect tooyour VMs from hello Internet.</span></span> <span data-ttu-id="2d938-128">Comme adresse par défaut de hello est dynamique, nous avons également créer une entrée DNS nommée avec hello `--domain-name-label` option.</span><span class="sxs-lookup"><span data-stu-id="2d938-128">Because hello default address is dynamic, we also create a named DNS entry with hello `--domain-name-label` option.</span></span> <span data-ttu-id="2d938-129">Hello exemple suivant crée une adresse IP publique nommée *myPublicIP* portant le nom DNS de hello de *mypublicdns*.</span><span class="sxs-lookup"><span data-stu-id="2d938-129">hello following example creates a public IP named *myPublicIP* with hello DNS name of *mypublicdns*.</span></span> <span data-ttu-id="2d938-130">Étant donné que le nom DNS de hello doit être unique, fournir votre propre nom DNS unique :</span><span class="sxs-lookup"><span data-stu-id="2d938-130">Because hello DNS name must be unique, provide your own unique DNS name:</span></span>

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

<span data-ttu-id="2d938-131">Output:</span><span class="sxs-lookup"><span data-stu-id="2d938-131">Output:</span></span>

```json
{
  "publicIp": {
    "dnsSettings": {
      "domainNameLabel": "mypublicdns",
      "fqdn": "mypublicdns.eastus.cloudapp.azure.com",
      "reverseFqdn": null
    },
    "etag": "W/\"2632aa72-3d2d-4529-b38e-b622b4202925\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "idleTimeoutInMinutes": 4,
    "ipAddress": null,
    "ipConfiguration": null,
    "location": "eastus",
    "name": "myPublicIP",
    "provisioningState": "Succeeded",
    "publicIpAddressVersion": "IPv4",
    "publicIpAllocationMethod": "Dynamic",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "4c65de38-71f5-4684-be10-75e605b3e41f",
    "tags": null,
    "type": "Microsoft.Network/publicIPAddresses"
  }
}
```


## <a name="create-a-network-security-group"></a><span data-ttu-id="2d938-132">Créer un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="2d938-132">Create a network security group</span></span>
<span data-ttu-id="2d938-133">flux de hello toocontrol du trafic vers et depuis vos machines virtuelles, créez un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="2d938-133">toocontrol hello flow of traffic in and out of your VMs, create a network security group.</span></span> <span data-ttu-id="2d938-134">Un groupe de sécurité réseau peut être appliqué tooa carte réseau ou sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="2d938-134">A network security group can be applied tooa NIC or subnet.</span></span> <span data-ttu-id="2d938-135">Hello exemple suivant utilise [az réseau nsg créer](/cli/azure/network/nsg#create) toocreate un groupe de sécurité réseau nommé *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="2d938-135">hello following example uses [az network nsg create](/cli/azure/network/nsg#create) toocreate a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="2d938-136">Vous définissez des règles qui autorisent ou refusent un trafic spécifique hello.</span><span class="sxs-lookup"><span data-stu-id="2d938-136">You define rules that allow or deny hello specific traffic.</span></span> <span data-ttu-id="2d938-137">tooallow les connexions entrantes sur le port 22 (toosupport SSH), créez une règle de trafic entrant pour le groupe de sécurité réseau hello avec [créer de règle de groupe de sécurité réseau du réseau az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="2d938-137">tooallow inbound connections on port 22 (toosupport SSH), create an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="2d938-138">Hello exemple suivant crée une règle nommée *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="2d938-138">hello following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 22 \
    --access allow
```

<span data-ttu-id="2d938-139">tooallow les connexions entrantes sur le port 80 (trafic web de toosupport), ajoutez une autre règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="2d938-139">tooallow inbound connections on port 80 (toosupport web traffic), add another network security group rule.</span></span> <span data-ttu-id="2d938-140">Hello exemple suivant crée une règle nommée *myNetworkSecurityGroupRuleHTTP*:</span><span class="sxs-lookup"><span data-stu-id="2d938-140">hello following example creates a rule named *myNetworkSecurityGroupRuleHTTP*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleWeb \
    --protocol tcp \
    --priority 1001 \
    --destination-port-range 80 \
    --access allow
```

<span data-ttu-id="2d938-141">Examiner le groupe de sécurité réseau hello et les règles avec [az réseau nsg afficher](/cli/azure/network/nsg#show):</span><span class="sxs-lookup"><span data-stu-id="2d938-141">Examine hello network security group and rules with [az network nsg show](/cli/azure/network/nsg#show):</span></span>

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

<span data-ttu-id="2d938-142">Output:</span><span class="sxs-lookup"><span data-stu-id="2d938-142">Output:</span></span>

```json
{
  "defaultSecurityRules": [
    {
      "access": "Allow",
      "description": "Allow inbound traffic from all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetInBound",
      "name": "AllowVnetInBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow inbound traffic from azure load balancer",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowAzureLoadBalancerInBou
      "name": "AllowAzureLoadBalancerInBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "AzureLoadBalancer",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all inbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllInBound",
      "name": "DenyAllInBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs tooall VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetOutBound",
      "name": "AllowVnetOutBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs tooInternet",
      "destinationAddressPrefix": "Internet",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowInternetOutBound",
      "name": "AllowInternetOutBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all outbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllOutBound",
      "name": "DenyAllOutBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
  "location": "eastus",
  "name": "myNetworkSecurityGroup",
  "networkInterfaces": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "47a9964e-23a3-438a-a726-8d60ebbb1c3c",
  "securityRules": [
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "22",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleSSH",
      "name": "myNetworkSecurityGroupRuleSSH",
      "priority": 1000,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "80",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleWeb",
      "name": "myNetworkSecurityGroupRuleWeb",
      "priority": 1001,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "subnets": null,
  "tags": null,
  "type": "Microsoft.Network/networkSecurityGroups"
}
```

## <a name="create-a-virtual-nic"></a><span data-ttu-id="2d938-143">Créer une carte d’interface réseau virtuelle</span><span class="sxs-lookup"><span data-stu-id="2d938-143">Create a virtual NIC</span></span>
<span data-ttu-id="2d938-144">Cartes d’interface réseau virtuelle (NIC) sont disponibles par programme, car vous pouvez appliquer des règles tootheir utilisation.</span><span class="sxs-lookup"><span data-stu-id="2d938-144">Virtual network interface cards (NICs) are programmatically available because you can apply rules tootheir use.</span></span> <span data-ttu-id="2d938-145">Vous pouvez également avoir plusieurs cartes.</span><span class="sxs-lookup"><span data-stu-id="2d938-145">You can also have more than one.</span></span> <span data-ttu-id="2d938-146">Suivant de hello [créer des cartes réseau du réseau az](/cli/azure/network/nic#create) de commande, vous créez une carte réseau nommée *myNic* et l’associer à un groupe de sécurité réseau hello.</span><span class="sxs-lookup"><span data-stu-id="2d938-146">In hello following [az network nic create](/cli/azure/network/nic#create) command, you create a NIC named *myNic* and associate it with hello network security group.</span></span> <span data-ttu-id="2d938-147">adresse IP publique de Hello *myPublicIP* est également associé de la carte réseau virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="2d938-147">hello public IP address *myPublicIP* is also associated with hello virtual NIC.</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="2d938-148">Output:</span><span class="sxs-lookup"><span data-stu-id="2d938-148">Output:</span></span>

```json
{
  "NewNIC": {
    "dnsSettings": {
      "appliedDnsServers": [],
      "dnsServers": [],
      "internalDnsNameLabel": null,
      "internalDomainNameSuffix": "brqlt10lvoxedgkeuomc4pm5tb.bx.internal.cloudapp.net",
      "internalFqdn": null
    },
    "enableAcceleratedNetworking": false,
    "enableIpForwarding": false,
    "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic",
    "ipConfigurations": [
      {
        "applicationGatewayBackendAddressPools": null,
        "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic/ipConfigurations/ipconfig1",
        "loadBalancerBackendAddressPools": null,
        "loadBalancerInboundNatRules": null,
        "name": "ipconfig1",
        "primary": true,
        "privateIpAddress": "192.168.1.4",
        "privateIpAddressVersion": "IPv4",
        "privateIpAllocationMethod": "Dynamic",
        "provisioningState": "Succeeded",
        "publicIpAddress": {
          "dnsSettings": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
          "idleTimeoutInMinutes": null,
          "ipAddress": null,
          "ipConfiguration": null,
          "location": null,
          "name": null,
          "provisioningState": null,
          "publicIpAddressVersion": null,
          "publicIpAllocationMethod": null,
          "resourceGroup": "myResourceGroup",
          "resourceGuid": null,
          "tags": null,
          "type": null
        },
        "resourceGroup": "myResourceGroup",
        "subnet": {
          "addressPrefix": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
          "ipConfigurations": null,
          "name": null,
          "networkSecurityGroup": null,
          "provisioningState": null,
          "resourceGroup": "myResourceGroup",
          "resourceNavigationLinks": null,
          "routeTable": null
        }
      }
    ],
    "location": "eastus",
    "macAddress": null,
    "name": "myNic",
    "networkSecurityGroup": {
      "defaultSecurityRules": null,
      "etag": null,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
      "location": null,
      "name": null,
      "networkInterfaces": null,
      "provisioningState": null,
      "resourceGroup": "myResourceGroup",
      "resourceGuid": null,
      "securityRules": null,
      "subnets": null,
      "tags": null,
      "type": null
    },
    "primary": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "b3dbaa0e-2cf2-43be-a814-5cc49fea3304",
    "tags": null,
    "type": "Microsoft.Network/networkInterfaces",
    "virtualMachine": null
  }
}
```


## <a name="create-an-availability-set"></a><span data-ttu-id="2d938-149">Créer un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="2d938-149">Create an availability set</span></span>
<span data-ttu-id="2d938-150">Les groupes à haute disponibilité aident à diffuser vos machines virtuelles sur des domaines d’erreur et des domaines de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="2d938-150">Availability sets help spread your VMs across fault domains and update domains.</span></span> <span data-ttu-id="2d938-151">Même si vous créez uniquement une machine virtuelle dès maintenant, il s’agit des meilleures pratiques toouse disponibilité jeux toomake il plus facile tooexpand Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="2d938-151">Even though you only create one VM right now, it's best practice toouse availability sets toomake it easier tooexpand in hello future.</span></span> 

<span data-ttu-id="2d938-152">Les domaines d’erreur désignent un groupe de machines virtuelles partageant une source d’alimentation et un commutateur réseau communs.</span><span class="sxs-lookup"><span data-stu-id="2d938-152">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="2d938-153">Par défaut, hello virtuels qui sont configurés au sein de votre jeu de disponibilité sont séparées à travers des domaines d’erreur toothree.</span><span class="sxs-lookup"><span data-stu-id="2d938-153">By default, hello virtual machines that are configured within your availability set are separated across up toothree fault domains.</span></span> <span data-ttu-id="2d938-154">En cas de problème matériel dans l’un de ces domaines d’erreur, toutes les machines virtuelles exécutant votre application ne sont pas affectées.</span><span class="sxs-lookup"><span data-stu-id="2d938-154">A hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span>

<span data-ttu-id="2d938-155">Indiquent les domaines de mise à jour des ordinateurs virtuels et le matériel physique sous-jacent qui peut être redémarré à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="2d938-155">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="2d938-156">Pendant les maintenances, commande hello dans la mise à jour des domaines sont redémarrés n’est peut-être pas séquentiel, mais une mise à jour qu’un seul domaine est redémarré à la fois.</span><span class="sxs-lookup"><span data-stu-id="2d938-156">During planned maintenance, hello order in which update domains are rebooted might not be sequential, but only one update domain is rebooted at a time.</span></span>

<span data-ttu-id="2d938-157">Azure distribue automatiquement les machines virtuelles entre les domaines d’erreur et la mise à jour de hello lorsque vous les placez dans un ensemble de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="2d938-157">Azure automatically distributes VMs across hello fault and update domains when placing them in an availability set.</span></span> <span data-ttu-id="2d938-158">Pour plus d’informations, consultez [gestion de la disponibilité de hello de machines virtuelles](manage-availability.md).</span><span class="sxs-lookup"><span data-stu-id="2d938-158">For more information, see [managing hello availability of VMs](manage-availability.md).</span></span>

<span data-ttu-id="2d938-159">Créez un groupe à haute disponibilité pour votre machine virtuelle avec la commande [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="2d938-159">Create an availability set for your VM with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="2d938-160">Hello exemple suivant crée un groupe à haute disponibilité nommée *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="2d938-160">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

<span data-ttu-id="2d938-161">Hello sortie notes des domaines d’erreur et domaines de mise à jour :</span><span class="sxs-lookup"><span data-stu-id="2d938-161">hello output notes fault domains and update domains:</span></span>

```json
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet",
  "location": "eastus",
  "managed": null,
  "name": "myAvailabilitySet",
  "platformFaultDomainCount": 2,
  "platformUpdateDomainCount": 5,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": null,
    "managed": true,
    "tier": null
  },
  "statuses": null,
  "tags": {},
  "type": "Microsoft.Compute/availabilitySets",
  "virtualMachines": []
}
```


## <a name="create-hello-linux-vms"></a><span data-ttu-id="2d938-162">Créer des machines virtuelles Linux hello</span><span class="sxs-lookup"><span data-stu-id="2d938-162">Create hello Linux VMs</span></span>
<span data-ttu-id="2d938-163">Vous avez créé toosupport de ressources réseau hello machines virtuelles accessibles sur Internet.</span><span class="sxs-lookup"><span data-stu-id="2d938-163">You've created hello network resources toosupport Internet-accessible VMs.</span></span> <span data-ttu-id="2d938-164">Maintenant, créez une machine virtuelle et sécurisez-la avec une clé SSH.</span><span class="sxs-lookup"><span data-stu-id="2d938-164">Now create a VM and secure it with an SSH key.</span></span> <span data-ttu-id="2d938-165">Dans ce cas, nous allons toocreate une VM Ubuntu selon hello LTS plus récente.</span><span class="sxs-lookup"><span data-stu-id="2d938-165">In this case, we're going toocreate an Ubuntu VM based on hello most recent LTS.</span></span> <span data-ttu-id="2d938-166">Vous pouvez trouver des images supplémentaires avec la commande [az vm image list](/cli/azure/vm/image#list), comme décrit dans l’article sur la [recherche d’images de machine virtuelle Azure](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="2d938-166">You can find additional images with [az vm image list](/cli/azure/vm/image#list), as described in [finding Azure VM images](cli-ps-findimage.md).</span></span>

<span data-ttu-id="2d938-167">Nous avons également spécifier un toouse clé SSH pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="2d938-167">We also specify an SSH key toouse for authentication.</span></span> <span data-ttu-id="2d938-168">Si vous ne disposez pas d’une paire de clés publiques SSH, vous pouvez [créez-les](mac-create-ssh-keys.md) ou utilisez hello `--generate-ssh-keys` paramètre toocreate pour vous.</span><span class="sxs-lookup"><span data-stu-id="2d938-168">If you do not have an SSH public key pair, you can [create them](mac-create-ssh-keys.md) or use hello `--generate-ssh-keys` parameter toocreate them for you.</span></span> <span data-ttu-id="2d938-169">Si vous utilisez déjà une paire de clés, ce paramètre utilise les clés existantes dans `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="2d938-169">If you already a key pair, this parameter uses existing keys in `~/.ssh`.</span></span>

<span data-ttu-id="2d938-170">Créer hello machine virtuelle en rassemblant tous nos ressources et informations avec hello [az vm créer](/cli/azure/vm#create) commande.</span><span class="sxs-lookup"><span data-stu-id="2d938-170">Create hello VM by bringing all our resources and information together with hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="2d938-171">Hello exemple suivant crée un ordinateur virtuel nommé *myVM*:</span><span class="sxs-lookup"><span data-stu-id="2d938-171">hello following example creates a VM named *myVM*:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --availability-set myAvailabilitySet \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="2d938-172">SSH tooyour machine virtuelle avec hello entrée DNS que vous avez fourni lorsque vous avez créé l’adresse IP publique de hello.</span><span class="sxs-lookup"><span data-stu-id="2d938-172">SSH tooyour VM with hello DNS entry you provided when you created hello public IP address.</span></span> <span data-ttu-id="2d938-173">Cela `fqdn` est indiqué dans la sortie de hello lorsque vous créez votre machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="2d938-173">This `fqdn` is shown in hello output as you create your VM:</span></span>

```json
{
  "fqdns": "mypublicdns.eastus.cloudapp.azure.com",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-13-71-C8",
  "powerState": "VM running",
  "privateIpAddress": "192.168.1.5",
  "publicIpAddress": "13.90.94.252",
  "resourceGroup": "myResourceGroup"
}
```

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="2d938-174">Output:</span><span class="sxs-lookup"><span data-stu-id="2d938-174">Output:</span></span>

```bash
hello authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

toorun a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

<span data-ttu-id="2d938-175">Vous pouvez installer NGINX et toohello de flux de trafic hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="2d938-175">You can install NGINX and see hello traffic flow toohello VM.</span></span> <span data-ttu-id="2d938-176">Installez NGINX comme suit :</span><span class="sxs-lookup"><span data-stu-id="2d938-176">Install NGINX as follows:</span></span>

```bash
sudo apt-get install -y nginx
```

<span data-ttu-id="2d938-177">site NGINX toosee hello par défaut en action, ouvrez votre navigateur web, puis entrez votre nom de domaine complet :</span><span class="sxs-lookup"><span data-stu-id="2d938-177">toosee hello default NGINX site in action, open your web browser and enter your FQDN:</span></span>

![Site NGINX par défaut sur votre machine virtuelle](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a><span data-ttu-id="2d938-179">Exporter en tant que modèle</span><span class="sxs-lookup"><span data-stu-id="2d938-179">Export as a template</span></span>
<span data-ttu-id="2d938-180">Que se passe-t-il si vous souhaitez maintenant toocreate un environnement de développement supplémentaire avec hello mêmes paramètres, ou un environnement de production qui lui correspond ?</span><span class="sxs-lookup"><span data-stu-id="2d938-180">What if you now want toocreate an additional development environment with hello same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="2d938-181">Le Gestionnaire de ressources utilise des modèles JSON qui définissent tous les paramètres de hello pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="2d938-181">Resource Manager uses JSON templates that define all hello parameters for your environment.</span></span> <span data-ttu-id="2d938-182">Vous créez des environnements entiers en faisant référence à ce modèle JSON.</span><span class="sxs-lookup"><span data-stu-id="2d938-182">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="2d938-183">Vous pouvez [créer manuellement des modèles JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou exporter un modèle JSON environnement toocreate hello existant pour vous.</span><span class="sxs-lookup"><span data-stu-id="2d938-183">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment toocreate hello JSON template for you.</span></span> <span data-ttu-id="2d938-184">Utilisez [exportation de groupe az](/cli/azure/group#export) tooexport votre ressource de groupe comme suit :</span><span class="sxs-lookup"><span data-stu-id="2d938-184">Use [az group export](/cli/azure/group#export) tooexport your resource group as follows:</span></span>

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

<span data-ttu-id="2d938-185">Cette commande crée hello `myResourceGroup.json` fichier dans votre répertoire de travail actuel.</span><span class="sxs-lookup"><span data-stu-id="2d938-185">This command creates hello `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="2d938-186">Lorsque vous créez un environnement à partir de ce modèle, vous êtes invité pour tous les noms de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="2d938-186">When you create an environment from this template, you are prompted for all hello resource names.</span></span> <span data-ttu-id="2d938-187">Vous pouvez remplir ces noms dans votre fichier de modèle en ajoutant hello `--include-parameter-default-value` paramètre toohello `az group export` commande.</span><span class="sxs-lookup"><span data-stu-id="2d938-187">You can populate these names in your template file by adding hello `--include-parameter-default-value` parameter toohello `az group export` command.</span></span> <span data-ttu-id="2d938-188">Modifier les noms de ressources JSON modèle toospecify hello, ou [créer un fichier parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) qui spécifie les noms de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="2d938-188">Edit your JSON template toospecify hello resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies hello resource names.</span></span>

<span data-ttu-id="2d938-189">toocreate un environnement à partir de votre modèle, utilisez [créer de déploiement de groupe az](/cli/azure/group/deployment#create) comme suit :</span><span class="sxs-lookup"><span data-stu-id="2d938-189">toocreate an environment from your template, use [az group deployment create](/cli/azure/group/deployment#create) as follows:</span></span>

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

<span data-ttu-id="2d938-190">Vous souhaiterez peut-être tooread [plus sur la façon toodeploy à partir de modèles](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2d938-190">You might want tooread [more about how toodeploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="2d938-191">Découvrez comment tooincrementally les environnements de mise à jour, utilisez le fichier de paramètres hello et accéder aux modèles à partir d’un emplacement de stockage unique.</span><span class="sxs-lookup"><span data-stu-id="2d938-191">Learn about how tooincrementally update environments, use hello parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d938-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2d938-192">Next steps</span></span>
<span data-ttu-id="2d938-193">Vous êtes maintenant prêt toobegin utilisation de plusieurs composants réseau et les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="2d938-193">Now you're ready toobegin working with multiple networking components and VMs.</span></span> <span data-ttu-id="2d938-194">Vous pouvez utiliser cette toobuild d’environnement exemple votre application à l’aide de composants hello introduits ici.</span><span class="sxs-lookup"><span data-stu-id="2d938-194">You can use this sample environment toobuild out your application by using hello core components introduced here.</span></span>
