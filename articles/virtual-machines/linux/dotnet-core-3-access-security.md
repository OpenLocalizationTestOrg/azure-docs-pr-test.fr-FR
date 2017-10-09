---
title: "aaaAccess et la sécurité dans les modèles Azure pour les machines virtuelles Linux | Documents Microsoft"
description: Didacticiel sur DotNet Core pour les machines virtuelles Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 07e47189-680e-4102-a8d4-5a8eb9c00213
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 88fedc8287c1f8ab8397a03ddefe1e60a686815e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="9fe20-103">Accès et sécurité dans les modèles Azure Resource Manager pour les machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="9fe20-103">Access and security in Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="9fe20-104">Applications hébergées sur hello dans Azure probablement être toobe accès internet ou un réseau privé virtuel / connexion Express Route avec Azure.</span><span class="sxs-lookup"><span data-stu-id="9fe20-104">Applications hosted in Azure likely need toobe access over hello internet or a VPN / Express Route connection with Azure.</span></span> <span data-ttu-id="9fe20-105">Avec l’exemple d’application hello magasin de musique, hello web site est rendue disponible sur hello internet avec une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="9fe20-105">With hello Music Store application sample, hello web site is made available on hello internet with a public IP address.</span></span> <span data-ttu-id="9fe20-106">Avec un accès établi, connexions toohello accès aux applications et toohello ressources d’ordinateur virtuel eux-mêmes doivent être sécurisés.</span><span class="sxs-lookup"><span data-stu-id="9fe20-106">With access established, connections toohello application and access toohello virtual machine resources themselves should be secured.</span></span> <span data-ttu-id="9fe20-107">Cette sécurité d’accès est assurée à l’aide d’un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="9fe20-107">This access security is provided with a Network Security Group.</span></span> 

<span data-ttu-id="9fe20-108">Ce document décrit en détail comment sécuriser la hello application de magasin de musique dans le modèle de gestionnaire de ressources Azure exemple hello.</span><span class="sxs-lookup"><span data-stu-id="9fe20-108">This document details how hello Music Store application is secured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="9fe20-109">Toutes les dépendances et configurations uniques sont en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="9fe20-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="9fe20-110">Pour une expérience optimale de hello, préalable déployer une instance de hello solution tooyour abonnement Azure et de travail en même temps que le modèle de gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9fe20-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="9fe20-111">modèle complète de Hello se trouve ici : [déploiement du magasin de musique sur Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="9fe20-111">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span> 

## <a name="public-ip-address"></a><span data-ttu-id="9fe20-112">Adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="9fe20-112">Public IP Address</span></span>
<span data-ttu-id="9fe20-113">tooprovide accès public tooan ressource Azure, une ressource d’adresse IP publique peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="9fe20-113">tooprovide public access tooan Azure resource, a public IP address resource can be used.</span></span> <span data-ttu-id="9fe20-114">Une adresse IP publique peut être configurée avec une adresse IP statique ou dynamique.</span><span class="sxs-lookup"><span data-stu-id="9fe20-114">Public IP address can be configured with a static or dynamic IP address.</span></span> <span data-ttu-id="9fe20-115">Si une adresse dynamique est utilisée et hello virtual machine est arrêtée et désallouée, les adresses hello est supprimé.</span><span class="sxs-lookup"><span data-stu-id="9fe20-115">If a dynamic address is used, and hello virtual machine is stopped and deallocated, hello addresses is removed.</span></span> <span data-ttu-id="9fe20-116">Au prochain démarrage de machine de hello, il peut être affecté à une autre adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="9fe20-116">When hello machine is started again, it may be assigned a different public IP address.</span></span> <span data-ttu-id="9fe20-117">tooprevent une IP d’adresses à partir de la modification, une adresse IP réservée peut être utilisée.</span><span class="sxs-lookup"><span data-stu-id="9fe20-117">tooprevent an IP address from changing, a reserved IP address can be used.</span></span> 

<span data-ttu-id="9fe20-118">Modèle d’Azure Resource Manager tooan à l’aide de hello Visual Studio ajouter Assistant Nouvelle ressource, peut être ajoutée à une adresse IP publique ou en insérant un JSON valide dans un modèle.</span><span class="sxs-lookup"><span data-stu-id="9fe20-118">A Public IP Address can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span> 

<span data-ttu-id="9fe20-119">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [adresse IP publique](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L121).</span><span class="sxs-lookup"><span data-stu-id="9fe20-119">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L121).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicipaddressName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "public-ip-front"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

<span data-ttu-id="9fe20-120">Une adresse IP publique peut être associée à une carte réseau virtuelle ou à un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="9fe20-120">A Public IP Address can be associated with a Virtual Network Adapter, or a Load Balancer.</span></span> <span data-ttu-id="9fe20-121">Dans cet exemple, hello du site Web du magasin de musique étant à charge équilibrée entre plusieurs machines virtuelles, hello adresse IP publique est attaché toohello équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="9fe20-121">In this example, because hello Music Store website is load balanced across several virtual machines, hello Public IP Address is attached toohello Load Balancer.</span></span>

<span data-ttu-id="9fe20-122">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [association d’adresse IP publique avec équilibrage de charge](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span><span class="sxs-lookup"><span data-stu-id="9fe20-122">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address association with Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicipaddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="9fe20-123">Hello adresse IP publique comme visibles sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9fe20-123">hello public IP Address as seen from hello Azure portal.</span></span> <span data-ttu-id="9fe20-124">Notez que l’adresse IP publique de hello est équilibrage de charge associé tooa et pas un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="9fe20-124">Notice that hello public IP address is associated tooa load balancer and not a virtual machine.</span></span> <span data-ttu-id="9fe20-125">Équilibreurs de charge réseau sont détaillées dans le document suivant de hello de cette série.</span><span class="sxs-lookup"><span data-stu-id="9fe20-125">Network load balancers are detailed in hello next document of this series.</span></span>

![Adresse IP publique](./media/dotnet-core-3-access-security/pubip.png)

<span data-ttu-id="9fe20-127">Pour plus d’informations sur les adresses IP publiques Azure, consultez [Adresses IP dans Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="9fe20-127">For more information on Azure Public IP Addresses, see [IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>

## <a name="network-security-group"></a><span data-ttu-id="9fe20-128">Groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="9fe20-128">Network Security Group</span></span>
<span data-ttu-id="9fe20-129">Une fois que l’accès a été établie tooAzure ressources, cet accès doit être limité.</span><span class="sxs-lookup"><span data-stu-id="9fe20-129">Once access has been established tooAzure resources, this access should be limited.</span></span> <span data-ttu-id="9fe20-130">Pour des machines virtuelles Azure, la sécurisation de l’accès s’effectue à l’aide d’un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="9fe20-130">For Azure virtual machines, secure access is accomplished using a network security group.</span></span> <span data-ttu-id="9fe20-131">Avec l’exemple d’application hello magasin de musique, machine virtuelle de tous les accès toohello est limitée à l’exception de via le port 80 pour l’accès http et le port 22 pour l’accès SSH.</span><span class="sxs-lookup"><span data-stu-id="9fe20-131">With hello Music Store application sample, all access toohello virtual machine is restricted except for over port 80 for http access, and port 22 for SSH access.</span></span> <span data-ttu-id="9fe20-132">Modèle d’Azure Resource Manager tooan à l’aide de hello Visual Studio ajouter Assistant Nouvelle ressource, peuvent être ajouté à un groupe de sécurité réseau ou en insérant un JSON valide dans un modèle.</span><span class="sxs-lookup"><span data-stu-id="9fe20-132">A Network Security Group can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span>

<span data-ttu-id="9fe20-133">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [groupe de sécurité réseau](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L68).</span><span class="sxs-lookup"><span data-stu-id="9fe20-133">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L68).</span></span>

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('nsgfront')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "nsg-front"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
}
```

<span data-ttu-id="9fe20-134">Dans cet exemple, un groupe de sécurité réseau hello est associé à un objet de sous-réseau hello déclaré dans une ressource de réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="9fe20-134">In this example, hello network security group is associate with hello subnet object declared in hello Virtual Network resource.</span></span> 

<span data-ttu-id="9fe20-135">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [association du groupe de sécurité réseau avec un réseau virtuel](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L158).</span><span class="sxs-lookup"><span data-stu-id="9fe20-135">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group association with Virtual Network](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L158).</span></span>

```json
"subnets": [
  {
    "name": "[variables('subnetName')]",
    "properties": {
      "addressPrefix": "10.0.0.0/24",
      "networkSecurityGroup": {
        "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
      }
    }
  }
```

<span data-ttu-id="9fe20-136">Voici le groupe de sécurité réseau hello ressemble à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9fe20-136">Here is what hello network security group looks like from hello Azure portal.</span></span> <span data-ttu-id="9fe20-137">Notez qu’un groupe de sécurité réseau peut être associé à une interface réseau et/ou un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="9fe20-137">Notice that an NSG can be associate with a subnet and / or network interface.</span></span> <span data-ttu-id="9fe20-138">Dans ce cas, hello NSG est associé tooa sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="9fe20-138">In this case, hello NSG is associated tooa subnet.</span></span> <span data-ttu-id="9fe20-139">Dans cette configuration, hello règles de trafic entrant s’appliquent tooall machines virtuelles connectées toohello sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="9fe20-139">In this configuration, hello inbound rules apply tooall virtual machines connected toohello subnet.</span></span>

![Groupe de sécurité réseau](./media/dotnet-core-3-access-security/nsg.png)

<span data-ttu-id="9fe20-141">Pour plus d’informations sur les groupes de sécurité réseau, consultez [Présentation du groupe de sécurité réseau](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span><span class="sxs-lookup"><span data-stu-id="9fe20-141">For in-depth information on Network Security Groups, see [What is a Network Security Group](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span></span>

## <a name="next-step"></a><span data-ttu-id="9fe20-142">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="9fe20-142">Next step</span></span>
<hr>

[<span data-ttu-id="9fe20-143">Étape 3 : disponibilité et mise à l’échelle dans les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9fe20-143">Step 3 - Availability and Scale in Azure Resource Manager Templates</span></span>](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

