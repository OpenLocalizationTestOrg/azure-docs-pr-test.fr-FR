---
title: "Disponibilité et scalabilité dans les modèles Azure Resource Manager | Microsoft Docs"
description: Didacticiel sur DotNet Core pour les machines virtuelles Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 494724b5-06af-4dea-a774-ba580cf27527
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c351950fa3fc1023e339c0dc63b034c5e0d910f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="61b37-103">Disponibilité et scalabilité dans les modèles Azure Resource Manager pour les machines virtuelles Windows</span><span class="sxs-lookup"><span data-stu-id="61b37-103">Availability and scale in Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="61b37-104">La disponibilité et la scalabilité font référence au temps de fonctionnement et à la capacité de répondre à la demande.</span><span class="sxs-lookup"><span data-stu-id="61b37-104">Availability and scale refer to uptime and the ability to meet demand.</span></span> <span data-ttu-id="61b37-105">Si une application doit être opérationnelle pendant jusqu’à 99,9 % du temps, elle doit présenter une architecture permettant l’utilisation de plusieurs ressources de calcul simultanées.</span><span class="sxs-lookup"><span data-stu-id="61b37-105">If an application must be up 99.9% of the time, it needs to have an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="61b37-106">Par exemple, au lieu d’avoir un seul site web, une configuration avec un niveau supérieur de disponibilité comprend plusieurs instances du même site, avec une technologie d’équilibrage placée devant celles-ci.</span><span class="sxs-lookup"><span data-stu-id="61b37-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of the same site, with balancing technology in front of them.</span></span> <span data-ttu-id="61b37-107">Dans cette configuration, une instance de l’application peut être retirée à des fins de maintenance, tandis que les autres continuent de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="61b37-107">In this configuration, one instance of the application can be taken down for maintenance, while the remaining continue to function.</span></span> <span data-ttu-id="61b37-108">Par ailleurs, la scalabilité fait référence à la capacité d’une application à répondre à la demande.</span><span class="sxs-lookup"><span data-stu-id="61b37-108">Scale on the other hand refers to an applications ability to serve demand.</span></span> <span data-ttu-id="61b37-109">Avec une application dont la charge est équilibrée, l’ajout ou la suppression d’instances du pool permet la scalabilité d’une application pour répondre à la demande.</span><span class="sxs-lookup"><span data-stu-id="61b37-109">With a load balanced application, adding or removing instances from the pool allows an application to scale to meet demand.</span></span>

<span data-ttu-id="61b37-110">Ce document décrit en détail comment l’exemple de déploiement du Store musique est configuré pour la disponibilité et la scalabilité.</span><span class="sxs-lookup"><span data-stu-id="61b37-110">This document details how the Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="61b37-111">Toutes les dépendances et configurations uniques sont en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="61b37-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="61b37-112">Pour optimiser l’expérience, prédéployez une instance de la solution sur votre abonnement Azure et travaillez avec le modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="61b37-112">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="61b37-113">Pour accéder au modèle complet, consultez [Déploiement du Store musique sous Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="61b37-113">The complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="availability-set"></a><span data-ttu-id="61b37-114">Groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="61b37-114">Availability Set</span></span>
<span data-ttu-id="61b37-115">Un groupe à haute disponibilité étend logiquement des machines virtuelles Azure sur des hôtes physiques et d’autres composants infrastructurels, tels que l’alimentation électrique et le matériel réseau physique.</span><span class="sxs-lookup"><span data-stu-id="61b37-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="61b37-116">Des groupes à haute disponibilité garantissent que, pendant la maintenance, en cas de panne d’appareil ou lors d’autres temps d’arrêt, les machines virtuelles ne sont pas toutes affectées.</span><span class="sxs-lookup"><span data-stu-id="61b37-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="61b37-117">Il est possible d’ajouter un groupe à haute disponibilité à un modèle Azure Resource Manager à l’aide de l’Assistant Ajouter une nouvelle ressource de Visual Studio, ou d’insérer un JSON valide dans un modèle.</span><span class="sxs-lookup"><span data-stu-id="61b37-117">An Availability Set can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="61b37-118">Pour voir l’exemple JSON dans le modèle Resource Manager, suivez ce lien : [Groupe à haute disponibilité](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L368).</span><span class="sxs-lookup"><span data-stu-id="61b37-118">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L368).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "availability-set"
  },
  "properties": {
  }
}
```

<span data-ttu-id="61b37-119">Un groupe à haute disponibilité est déclaré en tant que propriété d’une ressource de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="61b37-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="61b37-120">Pour voir l’exemple JSON dans le modèle Resource Manager, suivez ce lien : [Association d’un groupe à haute disponibilité avec une machine virtuelle](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L302).</span><span class="sxs-lookup"><span data-stu-id="61b37-120">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L302).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="61b37-121">Groupe à haute disponibilité dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="61b37-121">The availability set as seen from the Azure portal.</span></span> <span data-ttu-id="61b37-122">Chaque machine virtuelle est décrite ici avec des détails sur sa configuration.</span><span class="sxs-lookup"><span data-stu-id="61b37-122">Each virtual machine and details about the configuration are detailed here.</span></span>

![Groupe à haute disponibilité](./media/dotnet-core-4-availability-scale/ase-win.png)

<span data-ttu-id="61b37-124">Pour des informations détaillées sur les groupes à haute disponibilité, consultez [Gérer la disponibilité des machines virtuelles](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="61b37-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="61b37-125">Équilibreur de charge réseau</span><span class="sxs-lookup"><span data-stu-id="61b37-125">Network Load Balancer</span></span>
<span data-ttu-id="61b37-126">Si un groupe à haute disponibilité offre à une application une tolérance de panne, un équilibreur de charge rend plusieurs instances de l’application disponibles sur une adresse réseau unique.</span><span class="sxs-lookup"><span data-stu-id="61b37-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of the application available on a single network address.</span></span> <span data-ttu-id="61b37-127">Plusieurs instances d’une application peuvent être hébergées sur un grand nombre de machines virtuelles, chacune étant connectée à un équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="61b37-127">Multiple instances of an application can be hosted on many virtual machines, each one connected to a load balancer.</span></span> <span data-ttu-id="61b37-128">Lors de l’accès à l’application, l’équilibreur de charge route la demande entrante vers les membres attachés.</span><span class="sxs-lookup"><span data-stu-id="61b37-128">As the application is accessed, the load balancer routes the incoming request across the attached members.</span></span> <span data-ttu-id="61b37-129">Il est possible d’ajouter un équilibreur de charge à l’aide de l’Assistant Ajouter une nouvelle ressource de Visual Studio, ou en insérant une ressource JSON correctement mise en forme dans le modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="61b37-129">A Load Balancer can be added using the Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into the Azure Resource Manager template.</span></span>

<span data-ttu-id="61b37-130">Pour voir l’exemple JSON dans le modèle Resource Manager, suivez ce lien : [Équilibreur de charge réseau](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L198).</span><span class="sxs-lookup"><span data-stu-id="61b37-130">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L198).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer"
  },
  ........<truncated>
}
```

<span data-ttu-id="61b37-131">Étant donné que l’exemple d’application est exposé à Internet avec une adresse IP publique, celle-ci est associée à l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="61b37-131">Because the sample application is exposed to the internet with a public IP address, this address is associated with the load balancer.</span></span> 

<span data-ttu-id="61b37-132">Pour voir l’exemple JSON dans le modèle Resource Manager, suivez ce lien : [Association d’équilibreur de charge réseau avec une adresse IP publique](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span><span class="sxs-lookup"><span data-stu-id="61b37-132">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="61b37-133">Dans le portail Azure, la vue d’ensemble de l’équilibreur de charge réseau présente l’association avec l’adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="61b37-133">From the Azure portal, the network load balancer overview shows the association with the public IP address.</span></span>

![Équilibreur de charge réseau](./media/dotnet-core-4-availability-scale/nlb-win.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="61b37-135">Règle d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="61b37-135">Load Balancer Rule</span></span>
<span data-ttu-id="61b37-136">Lorsque vous utilisez un équilibreur de charge, des règles sont configurées. Elles contrôlent la manière dont le trafic est équilibré entre les ressources souhaitées.</span><span class="sxs-lookup"><span data-stu-id="61b37-136">When using a load balancer, rules are configured that control how traffic is balanced across the intended resources.</span></span> <span data-ttu-id="61b37-137">Avec l’exemple d’application du Store musique, le trafic arrive sur le port 80 de l’adresse IP publique, puis il est distribué au port 80 de toutes les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="61b37-137">With the sample Music Store application, traffic arrives on port 80 of the public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="61b37-138">Pour voir l’exemple JSON dans le modèle Resource Manager, suivez ce lien : [Règle d’équilibreur de charge](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L226).</span><span class="sxs-lookup"><span data-stu-id="61b37-138">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L226).</span></span>

```json
"loadBalancingRules": [
  {
    "name": "[variables('loadBalencerRule')]",
    "properties": {
      "frontendIPConfiguration": {
        "id": "[concat(resourceId('Microsoft.Network/loadBalancers', variables('loadBalancerName')), '/frontendIPConfigurations/LoadBalancerFrontend')]"
      },
      "backendAddressPool": {
        "id": "[variables('lbPoolID')]"
      },
      "protocol": "Tcp",
      "frontendPort": 80,
      "backendPort": 80,
      "enableFloatingIP": false,
      "idleTimeoutInMinutes": 5,
      "probe": {
        "id": "[variables('lbProbeID')]"
      }
    }
  }
]
```

<span data-ttu-id="61b37-139">Affichage de la règle d’équilibreur de charge réseau dans le portail.</span><span class="sxs-lookup"><span data-stu-id="61b37-139">A view of the network load balancer rule from the portal.</span></span>

![Règle d’équilibreur de charge réseau](./media/dotnet-core-4-availability-scale/lbrule-win.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="61b37-141">Sonde d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="61b37-141">Load Balancer Probe</span></span>
<span data-ttu-id="61b37-142">L’équilibreur de charge doit également surveiller chaque machine virtuelle afin que les demandes soient servies uniquement aux systèmes en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="61b37-142">The load balancer also needs to monitor each virtual machine so that requests are served only to running systems.</span></span> <span data-ttu-id="61b37-143">Cette surveillance s’effectue par sondage constant d’un port prédéfini.</span><span class="sxs-lookup"><span data-stu-id="61b37-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="61b37-144">Le déploiement du Store musique est configuré pour sonder le port 80 de toutes les machines virtuelles incluses.</span><span class="sxs-lookup"><span data-stu-id="61b37-144">The Music Store deployment is configured to probe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="61b37-145">Pour voir l’exemple JSON dans le modèle Resource Manager, suivez ce lien : [Sonde d’équilibreur de charge](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L247).</span><span class="sxs-lookup"><span data-stu-id="61b37-145">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L247).</span></span>

```json
"probes": [
  {
    "properties": {
      "protocol": "Tcp",
      "port": 80,
      "intervalInSeconds": 15,
      "numberOfProbes": 2
    },
    "name": "lbprobe"
  }
]
```

<span data-ttu-id="61b37-146">Sonde d’équilibreur de charge dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="61b37-146">The load balancer probe seen from the Azure portal.</span></span>

![Sonde d’équilibreur de charge réseau](./media/dotnet-core-4-availability-scale/lbprobe-win.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="61b37-148">Règles NAT de trafic entrant</span><span class="sxs-lookup"><span data-stu-id="61b37-148">Inbound NAT Rules</span></span>
<span data-ttu-id="61b37-149">Lorsque vous utilisez un équilibreur de charge, des règles doivent être mises en place pour offrir un accès sans équilibrage de charge à chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="61b37-149">When using a Load Balancer, rules need to be put into place that provide non-load balanced access to each Virtual Machine.</span></span> <span data-ttu-id="61b37-150">Par exemple, lors de la création d’une connexion RDP avec chaque machine virtuelle, ce trafic ne doit pas faire l’objet d’un équilibrage de charge. Au lieu de cela, un chemin d’accès prédéterminé doit être configuré.</span><span class="sxs-lookup"><span data-stu-id="61b37-150">For instance, when creating an RDP connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="61b37-151">Des chemins d’accès prédéterminés sont configurés à l’aide d’une ressource de règle NAT de trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="61b37-151">Pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="61b37-152">Cette ressource permet de mapper les communications entrantes à des machines virtuelles individuelles.</span><span class="sxs-lookup"><span data-stu-id="61b37-152">Using this resource, inbound communication can be mapped to individual Virtual Machines.</span></span> 

<span data-ttu-id="61b37-153">Avec l’application Store musique, un port commençant à 5000 est mappé au port 3389 de chaque machine virtuelle pour l’accès RDP.</span><span class="sxs-lookup"><span data-stu-id="61b37-153">With the Music Store application, a port starting at 5000 is mapped to port 3389 on each Virtual Machine for RDP access.</span></span> <span data-ttu-id="61b37-154">La fonction `copyindex()` est utilisée pour incrémenter le port entrant, de façon à ce que la deuxième machine virtuelle reçoive le port entrant 5001, la troisième le port entrant 5002, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="61b37-154">The `copyindex()` function is used to increment the incoming port, such that the second Virtual Machine receives an incoming port of 5001, the third 5002, and so on.</span></span>

<span data-ttu-id="61b37-155">Pour voir l’exemple JSON dans le modèle Resource Manager, suivez ce lien : [Règles NAT de trafic entrant](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L260).</span><span class="sxs-lookup"><span data-stu-id="61b37-155">Follow this link to see the JSON sample within the Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L260).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'RDP-VM', copyIndex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
  "copy": {
    "name": "lbNatLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
  ],
  "properties": {
    "frontendIPConfiguration": {
      "id": "[variables('ipConfigID')]"
    },
    "protocol": "tcp",
    "frontendPort": "[copyIndex(5000)]",
    "backendPort": 3389,
    "enableFloatingIP": false
  }
}
```

<span data-ttu-id="61b37-156">Exemple de règle NAT de trafic entrant dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="61b37-156">One example inbound NAT rule as seen in the Azure portal.</span></span> <span data-ttu-id="61b37-157">Une règle NAT RDP est créée pour chaque machine virtuelle dans le déploiement.</span><span class="sxs-lookup"><span data-stu-id="61b37-157">An RDP NAT rule is created for each virtual machine in the deployment.</span></span>

![Règle NAT de trafic entrant](./media/dotnet-core-4-availability-scale/natrule-win.png)

<span data-ttu-id="61b37-159">Pour des informations détaillées sur l’équilibreur de charge réseau Azure, consultez [Équilibrage de charge pour les services d’infrastructure Azure](load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="61b37-159">For in-depth information on the Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="61b37-160">Déployer plusieurs machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="61b37-160">Deploy multiple VMs</span></span>
<span data-ttu-id="61b37-161">Enfin, pour qu’un groupe à haute disponibilité ou un équilibreur de charge fonctionnent effectivement, plusieurs machines virtuelles sont nécessaires.</span><span class="sxs-lookup"><span data-stu-id="61b37-161">Finally, for an Availability Set or Load Balancer to effectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="61b37-162">Plusieurs machines virtuelles peuvent être déployées à l’aide de la fonction de copie du modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="61b37-162">Multiple VMs can be deployed using the Azure Resource Manager template copy function.</span></span> <span data-ttu-id="61b37-163">En utilisant la fonction de copie, il n’est pas nécessaire de définir un nombre fini de machines virtuelles. Au lieu de cela, cette valeur peut être fournie de façon dynamique au moment du déploiement.</span><span class="sxs-lookup"><span data-stu-id="61b37-163">Using the copy function, it is not necessary to define a finite number of Virtual Machines, rather this value can be dynamically provided at the time of deployment.</span></span> <span data-ttu-id="61b37-164">La fonction de copie utilise le nombre d’instances à créer. Elle gère le déploiement du nombre approprié de machines virtuelles et de ressources associées.</span><span class="sxs-lookup"><span data-stu-id="61b37-164">The copy function consumes the number of instances to be created and handles deploying the proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="61b37-165">Dans l’exemple de modèle de Store musique, un paramètre est défini, qui prend un nombre d’instances.</span><span class="sxs-lookup"><span data-stu-id="61b37-165">In the Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="61b37-166">Ce nombre est utilisé dans le modèle lors de la création des machines virtuelles et des ressources associées.</span><span class="sxs-lookup"><span data-stu-id="61b37-166">This number is used throughout the template when creating virtual machines and related resources.</span></span>

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 2,
  "metadata": {
    "description": "Number of VM instances to be created behind load balancer."
  }
},
```

<span data-ttu-id="61b37-167">Sur la ressource de machine virtuelle, la boucle de copie reçoit un nom et le paramètre de nombre d’instances utilisé pour contrôler le nombre de copies obtenues.</span><span class="sxs-lookup"><span data-stu-id="61b37-167">On the Virtual Machine resource, the copy loop is given a name and the number of instances parameter used to control the number of resulting copies.</span></span>

<span data-ttu-id="61b37-168">Pour voir l’exemple JSON dans le modèle Resource Manager, suivez ce lien : [Fonction de copie de machine virtuelle](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L290).</span><span class="sxs-lookup"><span data-stu-id="61b37-168">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L290).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  }
```

<span data-ttu-id="61b37-169">L’itération actuelle de la fonction de copie est accessible à l’aide de la fonction `copyIndex()` .</span><span class="sxs-lookup"><span data-stu-id="61b37-169">The current iteration of the copy function can be accessed with the `copyIndex()` function.</span></span> <span data-ttu-id="61b37-170">La valeur de la fonction de copie d’index peut être utilisée pour nommer les machines virtuelles et autres ressources.</span><span class="sxs-lookup"><span data-stu-id="61b37-170">The value of the copy index function can be used to name virtual machines and other resources.</span></span> <span data-ttu-id="61b37-171">Par exemple, si deux instances d’une machine virtuelle sont déployées, elles doivent porter des noms différents.</span><span class="sxs-lookup"><span data-stu-id="61b37-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="61b37-172">La fonction `copyIndex()` peut être utilisée en tant que partie du nom de machine virtuelle pour créer un nom unique.</span><span class="sxs-lookup"><span data-stu-id="61b37-172">The `copyIndex()` function can be used as part of the virtual machine name to create a unique name.</span></span> <span data-ttu-id="61b37-173">Un exemple d’utilisation de la fonction `copyindex()` pour nommer est visible dans la ressource de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="61b37-173">An example of the `copyindex()` function used for naming purposes can be seen in the Virtual Machine resource.</span></span> <span data-ttu-id="61b37-174">Ici, le nom de la machine est une concaténation du paramètre `vmName` et de la fonction `copyIndex()`.</span><span class="sxs-lookup"><span data-stu-id="61b37-174">Here, the computer name is a concatenation of the `vmName` parameter, and the `copyIndex()` function.</span></span> 

<span data-ttu-id="61b37-175">Pour voir l’exemple JSON dans le modèle Resource Manager, suivez ce lien : [Fonction de copie d’index](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L309).</span><span class="sxs-lookup"><span data-stu-id="61b37-175">Follow this link to see the JSON sample within the Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L309).</span></span> 

```json
"osProfile": {
  "computerName": "[concat(variables('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "adminPassword": "[parameters('adminPassword')]"
}
```

<span data-ttu-id="61b37-176">La fonction `copyIndex` est utilisée plusieurs fois dans l’exemple de modèle du Store musique.</span><span class="sxs-lookup"><span data-stu-id="61b37-176">The `copyIndex` function is used several times in the Music Store sample template.</span></span> <span data-ttu-id="61b37-177">Les ressources et fonctions utilisant `copyIndex` contiennent tous les éléments spécifiques d’une instance unique de la machine virtuelles, tels que l’interface réseau, les règles d’équilibreur de charge et les fonctions de dépendance.</span><span class="sxs-lookup"><span data-stu-id="61b37-177">Resources and functions utilizing `copyIndex` include anything specific to a single instance of the virtual machine such and network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="61b37-178">Pour plus d’informations sur l’utilisation de la fonction de copie, consultez [Création de plusieurs instances de ressources dans Azure Resource Manager](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="61b37-178">For more information on the copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="61b37-179">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="61b37-179">Next step</span></span>
<hr>

[<span data-ttu-id="61b37-180">Étape 4 : Déploiement d’application avec des modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="61b37-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

