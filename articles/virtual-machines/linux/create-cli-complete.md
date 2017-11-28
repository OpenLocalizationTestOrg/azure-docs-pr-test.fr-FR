---
title: "Création d’un environnement Linux à l’aide d’Azure CLI 2.0 | Microsoft Docs"
description: "Créez un stockage, une machine virtuelle Linux, un réseau virtuel et un sous-réseau, un équilibreur de charge, une carte d’interface réseau, une adresse IP publique et un groupe de sécurité réseau à partir de zéro à l’aide de l’interface Azure CLI 2.0."
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
ms.openlocfilehash: e5c4785428b2150e951923e98079e00808a82d87
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="85a9a-103">Créer une machine virtuelle Linux complète avec Azure CLI</span><span class="sxs-lookup"><span data-stu-id="85a9a-103">Create a complete Linux virtual machine with the Azure CLI</span></span>
<span data-ttu-id="85a9a-104">Pour créer rapidement une machine virtuelle dans Azure, vous pouvez utiliser une seule commande Azure CLI qui utilise des valeurs par défaut pour créer toutes les ressources associées requises.</span><span class="sxs-lookup"><span data-stu-id="85a9a-104">To quickly create a virtual machine (VM) in Azure, you can use a single Azure CLI command that uses default values to create any required supporting resources.</span></span> <span data-ttu-id="85a9a-105">Les ressources telles que le réseau virtuel, l’adresse IP publique et les règles de groupe de sécurité réseau sont automatiquement créées.</span><span class="sxs-lookup"><span data-stu-id="85a9a-105">Resources such as a virtual network, public IP address, and network security group rules are automatically created.</span></span> <span data-ttu-id="85a9a-106">Pour un meilleur contrôle de votre environnement en production, vous pouvez créer ces ressources à l’avance, puis leur ajouter vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="85a9a-106">For more control of your environment in production use, you may create these resources ahead of time and then add your VMs to them.</span></span> <span data-ttu-id="85a9a-107">Cet article vous accompagne dans la création d’une machine virtuelle et de chacune des ressources associées.</span><span class="sxs-lookup"><span data-stu-id="85a9a-107">This article guides you through how to create a VM and each of the supporting resources one by one.</span></span>

<span data-ttu-id="85a9a-108">Assurez-vous que vous avez installé la dernière version de l’interface [Azure CLI 2.0](/cli/azure/install-az-cli2) et que vous vous êtes connecté à un compte Azure avec la commande [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="85a9a-108">Make sure that you have installed the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and logged to an Azure account in with [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="85a9a-109">Dans les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="85a9a-109">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="85a9a-110">Les noms de paramètre sont par exemple *myResourceGroup*, *myVnet* et *myVM*.</span><span class="sxs-lookup"><span data-stu-id="85a9a-110">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="85a9a-111">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="85a9a-111">Create resource group</span></span>
<span data-ttu-id="85a9a-112">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="85a9a-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="85a9a-113">Un groupe de ressources doit être créé avant la machine virtuelle et les ressources de réseau virtuel associées.</span><span class="sxs-lookup"><span data-stu-id="85a9a-113">A resource group must be created before a virtual machine and supporting virtual network resources.</span></span> <span data-ttu-id="85a9a-114">Créez le groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="85a9a-114">Create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="85a9a-115">L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* à l’emplacement *eastus* :</span><span class="sxs-lookup"><span data-stu-id="85a9a-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="85a9a-116">Par défaut, la sortie des commandes Azure CLI est au format JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="85a9a-116">By default, the output of Azure CLI commands is in JSON (JavaScript Object Notation).</span></span> <span data-ttu-id="85a9a-117">Pour remplacer la sortie par défaut pour une liste ou une table, par exemple, utilisez [az configure --output](/cli/azure/#configure).</span><span class="sxs-lookup"><span data-stu-id="85a9a-117">To change the default output to a list or table, for example, use [az configure --output](/cli/azure/#configure).</span></span> <span data-ttu-id="85a9a-118">Vous pouvez également ajouter `--output` à n’importe quelle commande pour modifier ponctuellement le format de sortie.</span><span class="sxs-lookup"><span data-stu-id="85a9a-118">You can also add `--output` to any command for a one time change in output format.</span></span> <span data-ttu-id="85a9a-119">L’exemple suivant illustre la sortie JSON obtenue avec la commande `az group create` :</span><span class="sxs-lookup"><span data-stu-id="85a9a-119">The following example shows the JSON output from the `az group create` command:</span></span>

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

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="85a9a-120">Créer un réseau virtuel et un sous-réseau</span><span class="sxs-lookup"><span data-stu-id="85a9a-120">Create a virtual network and subnet</span></span>
<span data-ttu-id="85a9a-121">Ensuite, vous créez un réseau virtuel dans Azure et un sous-réseau dans lequel vous pouvez créer vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="85a9a-121">Next you create a virtual network in Azure and a subnet in to which you can create your VMs.</span></span> <span data-ttu-id="85a9a-122">Utilisez [az network vnet create](/cli/azure/network/vnet#create) pour créer un réseau virtuel nommé *myVnet* avec le préfixe d’adresse *192.168.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="85a9a-122">Use [az network vnet create](/cli/azure/network/vnet#create) to create a virtual network named *myVnet* with the *192.168.0.0/16* address prefix.</span></span> <span data-ttu-id="85a9a-123">Vous pouvez également ajouter un sous-réseau nommé *mySubnet* avec le préfixe d’adresse *192.168.1.0/24* :</span><span class="sxs-lookup"><span data-stu-id="85a9a-123">You also add a subnet named *mySubnet* with the address prefix of *192.168.1.0/24*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="85a9a-124">La sortie montre que le sous-réseau est logiquement créé à l’intérieur du réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="85a9a-124">The output shows the subnet as logically created inside the virtual network:</span></span>

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


## <a name="create-a-public-ip-address"></a><span data-ttu-id="85a9a-125">Créer une adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="85a9a-125">Create a public IP address</span></span>
<span data-ttu-id="85a9a-126">Créons à présent une adresse IP publique avec la commande [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="85a9a-126">Now let's create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="85a9a-127">Cette adresse IP publique vous permet de vous connecter à vos machines virtuelles à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="85a9a-127">This public IP address enables you to connect to your VMs from the Internet.</span></span> <span data-ttu-id="85a9a-128">Étant donné que l’adresse par défaut est dynamique, nous créons également une entrée DNS nommée avec l’option `--domain-name-label`.</span><span class="sxs-lookup"><span data-stu-id="85a9a-128">Because the default address is dynamic, we also create a named DNS entry with the `--domain-name-label` option.</span></span> <span data-ttu-id="85a9a-129">L’exemple suivant permet de créer une adresse IP publique nommée *myPublicIP* avec le nom DNS de *mypublicdns*.</span><span class="sxs-lookup"><span data-stu-id="85a9a-129">The following example creates a public IP named *myPublicIP* with the DNS name of *mypublicdns*.</span></span> <span data-ttu-id="85a9a-130">Puisque le nom DNS doit être unique, indiquez votre propre nom DNS unique :</span><span class="sxs-lookup"><span data-stu-id="85a9a-130">Because the DNS name must be unique, provide your own unique DNS name:</span></span>

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

<span data-ttu-id="85a9a-131">Output:</span><span class="sxs-lookup"><span data-stu-id="85a9a-131">Output:</span></span>

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


## <a name="create-a-network-security-group"></a><span data-ttu-id="85a9a-132">Créer un groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="85a9a-132">Create a network security group</span></span>
<span data-ttu-id="85a9a-133">Pour contrôler le flux du trafic en direction et en provenance de vos machines virtuelles, créez un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="85a9a-133">To control the flow of traffic in and out of your VMs, create a network security group.</span></span> <span data-ttu-id="85a9a-134">Un groupe de sécurité réseau peut être appliqué à une carte d’interface réseau ou à un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="85a9a-134">A network security group can be applied to a NIC or subnet.</span></span> <span data-ttu-id="85a9a-135">L’exemple suivant utilise la commande [az network nsg create](/cli/azure/network/nsg#create) pour créer un groupe de sécurité réseau nommé *myNetworkSecurityGroup* :</span><span class="sxs-lookup"><span data-stu-id="85a9a-135">The following example uses [az network nsg create](/cli/azure/network/nsg#create) to create a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="85a9a-136">Vous définissez des règles qui autorisent ou refusent le trafic spécifique.</span><span class="sxs-lookup"><span data-stu-id="85a9a-136">You define rules that allow or deny the specific traffic.</span></span> <span data-ttu-id="85a9a-137">Pour autoriser les connexions entrantes sur le port 22 (pour prendre en charge le protocole SSH), créez une règle de trafic entrant pour le groupe de sécurité réseau avec la commande [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="85a9a-137">To allow inbound connections on port 22 (to support SSH), create an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="85a9a-138">L’exemple suivant crée une règle nommée *myNetworkSecurityGroupRuleSSH* :</span><span class="sxs-lookup"><span data-stu-id="85a9a-138">The following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

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

<span data-ttu-id="85a9a-139">Pour autoriser les connexions entrantes sur le port 80 (pour prendre en charge le trafic web), ajoutez une autre règle de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="85a9a-139">To allow inbound connections on port 80 (to support web traffic), add another network security group rule.</span></span> <span data-ttu-id="85a9a-140">L’exemple suivant crée une règle nommée *myNetworkSecurityGroupRuleHTTP* :</span><span class="sxs-lookup"><span data-stu-id="85a9a-140">The following example creates a rule named *myNetworkSecurityGroupRuleHTTP*:</span></span>

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

<span data-ttu-id="85a9a-141">Examinez le groupe et les règles de sécurité réseau avec la commande [az network nsg show](/cli/azure/network/nsg#show) :</span><span class="sxs-lookup"><span data-stu-id="85a9a-141">Examine the network security group and rules with [az network nsg show](/cli/azure/network/nsg#show):</span></span>

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

<span data-ttu-id="85a9a-142">Output:</span><span class="sxs-lookup"><span data-stu-id="85a9a-142">Output:</span></span>

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
      "description": "Allow outbound traffic from all VMs to all VMs in VNET",
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
      "description": "Allow outbound traffic from all VMs to Internet",
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

## <a name="create-a-virtual-nic"></a><span data-ttu-id="85a9a-143">Créer une carte d’interface réseau virtuelle</span><span class="sxs-lookup"><span data-stu-id="85a9a-143">Create a virtual NIC</span></span>
<span data-ttu-id="85a9a-144">La disponibilité des cartes d’interface réseau virtuelles peut être déterminée par programme car vous pouvez définir des règles régissant leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="85a9a-144">Virtual network interface cards (NICs) are programmatically available because you can apply rules to their use.</span></span> <span data-ttu-id="85a9a-145">Vous pouvez également avoir plusieurs cartes.</span><span class="sxs-lookup"><span data-stu-id="85a9a-145">You can also have more than one.</span></span> <span data-ttu-id="85a9a-146">Dans la commande [az network nic create](/cli/azure/network/nic#create) suivante, vous créez une carte d’interface réseau nommée *myNic* et vous l’associez au groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="85a9a-146">In the following [az network nic create](/cli/azure/network/nic#create) command, you create a NIC named *myNic* and associate it with the network security group.</span></span> <span data-ttu-id="85a9a-147">L’adresse IP publique *myPublicIP* est également associée à la carte d’interface réseau virtuelle.</span><span class="sxs-lookup"><span data-stu-id="85a9a-147">The public IP address *myPublicIP* is also associated with the virtual NIC.</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="85a9a-148">Output:</span><span class="sxs-lookup"><span data-stu-id="85a9a-148">Output:</span></span>

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


## <a name="create-an-availability-set"></a><span data-ttu-id="85a9a-149">Créer un groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="85a9a-149">Create an availability set</span></span>
<span data-ttu-id="85a9a-150">Les groupes à haute disponibilité aident à diffuser vos machines virtuelles sur des domaines d’erreur et des domaines de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="85a9a-150">Availability sets help spread your VMs across fault domains and update domains.</span></span> <span data-ttu-id="85a9a-151">Même si vous ne créez qu’une seule machine virtuelle tout de suite, il est recommandé d’utiliser des groupes à haute disponibilité pour faciliter leur développement à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="85a9a-151">Even though you only create one VM right now, it's best practice to use availability sets to make it easier to expand in the future.</span></span> 

<span data-ttu-id="85a9a-152">Les domaines d’erreur désignent un groupe de machines virtuelles partageant une source d’alimentation et un commutateur réseau communs.</span><span class="sxs-lookup"><span data-stu-id="85a9a-152">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="85a9a-153">Par défaut, les machines virtuelles configurées dans votre groupe à haute disponibilité sont réparties entre trois domaines de défaillance au maximum.</span><span class="sxs-lookup"><span data-stu-id="85a9a-153">By default, the virtual machines that are configured within your availability set are separated across up to three fault domains.</span></span> <span data-ttu-id="85a9a-154">En cas de problème matériel dans l’un de ces domaines d’erreur, toutes les machines virtuelles exécutant votre application ne sont pas affectées.</span><span class="sxs-lookup"><span data-stu-id="85a9a-154">A hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span>

<span data-ttu-id="85a9a-155">Les domaines de mise à jour indiquent les groupes de machines virtuelles et les équipements physiques sous-jacents pouvant être redémarrés en même temps.</span><span class="sxs-lookup"><span data-stu-id="85a9a-155">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="85a9a-156">Au cours de la maintenance planifiée, l’ordre de redémarrage des domaines de mise à jour peut ne pas être séquentiel, mais un seul domaine de mise à jour est redémarré à la fois.</span><span class="sxs-lookup"><span data-stu-id="85a9a-156">During planned maintenance, the order in which update domains are rebooted might not be sequential, but only one update domain is rebooted at a time.</span></span>

<span data-ttu-id="85a9a-157">Azure distribue automatiquement les machines virtuelles sur les domaines d’erreur et de mise à jour lorsque vous les placez dans un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="85a9a-157">Azure automatically distributes VMs across the fault and update domains when placing them in an availability set.</span></span> <span data-ttu-id="85a9a-158">Pour plus d’informations, consultez l’article sur la [gestion de la disponibilité des machines virtuelles](manage-availability.md).</span><span class="sxs-lookup"><span data-stu-id="85a9a-158">For more information, see [managing the availability of VMs](manage-availability.md).</span></span>

<span data-ttu-id="85a9a-159">Créez un groupe à haute disponibilité pour votre machine virtuelle avec la commande [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="85a9a-159">Create an availability set for your VM with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="85a9a-160">L’exemple suivant permet de créer un groupe à haute disponibilité nommé *myAvailabilitySet* :</span><span class="sxs-lookup"><span data-stu-id="85a9a-160">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

<span data-ttu-id="85a9a-161">La sortie indique les domaines d’erreur et les domaines de mise à jour :</span><span class="sxs-lookup"><span data-stu-id="85a9a-161">The output notes fault domains and update domains:</span></span>

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


## <a name="create-the-linux-vms"></a><span data-ttu-id="85a9a-162">Créer les machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="85a9a-162">Create the Linux VMs</span></span>
<span data-ttu-id="85a9a-163">Vous avez créé les ressources de réseau pour prendre en charge des machines virtuelles accessibles par Internet.</span><span class="sxs-lookup"><span data-stu-id="85a9a-163">You've created the network resources to support Internet-accessible VMs.</span></span> <span data-ttu-id="85a9a-164">Maintenant, créez une machine virtuelle et sécurisez-la avec une clé SSH.</span><span class="sxs-lookup"><span data-stu-id="85a9a-164">Now create a VM and secure it with an SSH key.</span></span> <span data-ttu-id="85a9a-165">Dans ce cas précis, nous allons créer une machine virtuelle Ubuntu basée sur la dernière version LTS.</span><span class="sxs-lookup"><span data-stu-id="85a9a-165">In this case, we're going to create an Ubuntu VM based on the most recent LTS.</span></span> <span data-ttu-id="85a9a-166">Vous pouvez trouver des images supplémentaires avec la commande [az vm image list](/cli/azure/vm/image#list), comme décrit dans l’article sur la [recherche d’images de machine virtuelle Azure](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="85a9a-166">You can find additional images with [az vm image list](/cli/azure/vm/image#list), as described in [finding Azure VM images](cli-ps-findimage.md).</span></span>

<span data-ttu-id="85a9a-167">Nous spécifions également une clé SSH à utiliser pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="85a9a-167">We also specify an SSH key to use for authentication.</span></span> <span data-ttu-id="85a9a-168">Si vous ne disposez pas d’une paire de clés publiques SSH, vous pouvez [les créer](mac-create-ssh-keys.md) ou utiliser le paramètre `--generate-ssh-keys` pour les créer automatiquement.</span><span class="sxs-lookup"><span data-stu-id="85a9a-168">If you do not have an SSH public key pair, you can [create them](mac-create-ssh-keys.md) or use the `--generate-ssh-keys` parameter to create them for you.</span></span> <span data-ttu-id="85a9a-169">Si vous utilisez déjà une paire de clés, ce paramètre utilise les clés existantes dans `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="85a9a-169">If you already a key pair, this parameter uses existing keys in `~/.ssh`.</span></span>

<span data-ttu-id="85a9a-170">Créez la machine virtuelle en regroupant toutes nos ressources et informations avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="85a9a-170">Create the VM by bringing all our resources and information together with the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="85a9a-171">L’exemple suivant crée une machine virtuelle nommée *myVM* :</span><span class="sxs-lookup"><span data-stu-id="85a9a-171">The following example creates a VM named *myVM*:</span></span>

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

<span data-ttu-id="85a9a-172">Pour configurer le protocole SSH avec votre machine virtuelle, utilisez l’entrée DNS que vous avez fournie lors de la création de l’adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="85a9a-172">SSH to your VM with the DNS entry you provided when you created the public IP address.</span></span> <span data-ttu-id="85a9a-173">Ce `fqdn` est indiqué dans la sortie quand vous créez votre machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="85a9a-173">This `fqdn` is shown in the output as you create your VM:</span></span>

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

<span data-ttu-id="85a9a-174">Output:</span><span class="sxs-lookup"><span data-stu-id="85a9a-174">Output:</span></span>

```bash
The authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

<span data-ttu-id="85a9a-175">Vous pouvez installer NGINX et voir le flux de trafic vers la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="85a9a-175">You can install NGINX and see the traffic flow to the VM.</span></span> <span data-ttu-id="85a9a-176">Installez NGINX comme suit :</span><span class="sxs-lookup"><span data-stu-id="85a9a-176">Install NGINX as follows:</span></span>

```bash
sudo apt-get install -y nginx
```

<span data-ttu-id="85a9a-177">Pour voir le site NGINX par défaut en action, ouvrez votre navigateur web, puis entrez votre nom de domaine complet :</span><span class="sxs-lookup"><span data-stu-id="85a9a-177">To see the default NGINX site in action, open your web browser and enter your FQDN:</span></span>

![Site NGINX par défaut sur votre machine virtuelle](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a><span data-ttu-id="85a9a-179">Exporter en tant que modèle</span><span class="sxs-lookup"><span data-stu-id="85a9a-179">Export as a template</span></span>
<span data-ttu-id="85a9a-180">Que se passe-t-il si vous souhaitez créer un environnement de développement supplémentaire avec les mêmes paramètres ou un environnement de production correspondant ?</span><span class="sxs-lookup"><span data-stu-id="85a9a-180">What if you now want to create an additional development environment with the same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="85a9a-181">Resource Manager utilise des modèles JSON qui définissent tous les paramètres pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="85a9a-181">Resource Manager uses JSON templates that define all the parameters for your environment.</span></span> <span data-ttu-id="85a9a-182">Vous créez des environnements entiers en faisant référence à ce modèle JSON.</span><span class="sxs-lookup"><span data-stu-id="85a9a-182">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="85a9a-183">Vous pouvez [créer manuellement des modèles JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou exporter un environnement existant qui créera le modèle JSON pour vous.</span><span class="sxs-lookup"><span data-stu-id="85a9a-183">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment to create the JSON template for you.</span></span> <span data-ttu-id="85a9a-184">Utilisez la commande [az group export](/cli/azure/group#export) pour exporter votre groupe de ressources comme suit :</span><span class="sxs-lookup"><span data-stu-id="85a9a-184">Use [az group export](/cli/azure/group#export) to export your resource group as follows:</span></span>

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

<span data-ttu-id="85a9a-185">Cette commande crée le fichier `myResourceGroup.json` dans votre répertoire de travail actuel.</span><span class="sxs-lookup"><span data-stu-id="85a9a-185">This command creates the `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="85a9a-186">Quand vous créez un environnement à partir de ce modèle, vous êtes invité à indiquer tous les noms de ressources.</span><span class="sxs-lookup"><span data-stu-id="85a9a-186">When you create an environment from this template, you are prompted for all the resource names.</span></span> <span data-ttu-id="85a9a-187">Vous pouvez renseigner ces noms dans votre fichier de modèle en ajoutant le paramètre `--include-parameter-default-value` à la commande `az group export`.</span><span class="sxs-lookup"><span data-stu-id="85a9a-187">You can populate these names in your template file by adding the `--include-parameter-default-value` parameter to the `az group export` command.</span></span> <span data-ttu-id="85a9a-188">Modifiez votre modèle JSON pour spécifier les noms de ressources, ou [créez un fichier parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) qui spécifie les noms de ressources.</span><span class="sxs-lookup"><span data-stu-id="85a9a-188">Edit your JSON template to specify the resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies the resource names.</span></span>

<span data-ttu-id="85a9a-189">Pour créer un environnement à partir de votre modèle, utilisez la commande [az group deployment create](/cli/azure/group/deployment#create) comme suit :</span><span class="sxs-lookup"><span data-stu-id="85a9a-189">To create an environment from your template, use [az group deployment create](/cli/azure/group/deployment#create) as follows:</span></span>

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

<span data-ttu-id="85a9a-190">Vous pouvez lire la section contenant [plus de détails sur le déploiement à partir de modèles](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="85a9a-190">You might want to read [more about how to deploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="85a9a-191">Découvrez notamment comment mettre à jour des environnements de manière incrémentielle, utiliser le fichier de paramètres et accéder aux modèles à partir d’un emplacement de stockage unique.</span><span class="sxs-lookup"><span data-stu-id="85a9a-191">Learn about how to incrementally update environments, use the parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85a9a-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="85a9a-192">Next steps</span></span>
<span data-ttu-id="85a9a-193">Vous voici en mesure de commencer à utiliser plusieurs composants réseau et machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="85a9a-193">Now you're ready to begin working with multiple networking components and VMs.</span></span> <span data-ttu-id="85a9a-194">Vous pouvez utiliser cet exemple d’environnement pour générer votre application en utilisant les composants de base présentés ici.</span><span class="sxs-lookup"><span data-stu-id="85a9a-194">You can use this sample environment to build out your application by using the core components introduced here.</span></span>
