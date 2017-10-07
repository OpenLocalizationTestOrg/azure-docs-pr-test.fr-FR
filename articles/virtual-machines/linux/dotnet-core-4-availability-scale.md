---
title: "aaaAvailability et l’échelle dans les modèles Azure Resource Manager | Documents Microsoft"
description: Didacticiel sur DotNet Core pour les machines virtuelles Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8fcfea79-f017-4658-8c51-74242fcfb7f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6f830ca0a64e6b65859312bdf31dc0af59e2b978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="8020c-103">Disponibilité et scalabilité dans les modèles Azure Resource Manager pour les machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="8020c-103">Availability and scale in Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="8020c-104">Disponibilité et l’échelle, reportez-vous à la demande toomeet de capacité toouptime et hello.</span><span class="sxs-lookup"><span data-stu-id="8020c-104">Availability and scale refer toouptime and hello ability toomeet demand.</span></span> <span data-ttu-id="8020c-105">Si une application doit être de 99,9 % du temps de hello, il doit toohave une architecture qui permet à plusieurs ressources de calcul simultanées.</span><span class="sxs-lookup"><span data-stu-id="8020c-105">If an application must be up 99.9% of hello time, it needs toohave an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="8020c-106">Par exemple, au lieu d’avoir un seul site Web, une configuration avec un niveau plus élevé de disponibilité inclut plusieurs instances du hello même site, avec l’équilibrage de la technologie de face d’eux.</span><span class="sxs-lookup"><span data-stu-id="8020c-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of hello same site, with balancing technology in front of them.</span></span> <span data-ttu-id="8020c-107">Dans cette configuration, une seule instance de l’application hello peut être récupérée pour une maintenance, hello restant interrompre toofunction.</span><span class="sxs-lookup"><span data-stu-id="8020c-107">In this configuration, one instance of hello application can be taken down for maintenance, while hello remaining continue toofunction.</span></span> <span data-ttu-id="8020c-108">Mise à l’échelle sur hello autre part fait référence à la demande de tooan applications capacité tooserve.</span><span class="sxs-lookup"><span data-stu-id="8020c-108">Scale on hello other hand refers tooan applications ability tooserve demand.</span></span> <span data-ttu-id="8020c-109">Avec une charge application à charge équilibrée, ajouter ou supprimer des instances de pool de hello permet à une demande de toomeet tooscale application.</span><span class="sxs-lookup"><span data-stu-id="8020c-109">With a load balanced application, adding or removing instances from hello pool allows an application tooscale toomeet demand.</span></span>

<span data-ttu-id="8020c-110">Ce document décrit en détail comment hello exemple de déploiement de magasin de musique est configuré pour la disponibilité et l’échelle.</span><span class="sxs-lookup"><span data-stu-id="8020c-110">This document details how hello Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="8020c-111">Toutes les dépendances et configurations uniques sont en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="8020c-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="8020c-112">Pour une expérience optimale de hello, préalable déployer une instance de hello solution tooyour abonnement Azure et de travail en même temps que le modèle de gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8020c-112">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="8020c-113">modèle complète de Hello se trouve ici : [déploiement du magasin de musique sur Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="8020c-113">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="availability-set"></a><span data-ttu-id="8020c-114">Groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="8020c-114">Availability Set</span></span>
<span data-ttu-id="8020c-115">Un groupe à haute disponibilité étend logiquement des machines virtuelles Azure sur des hôtes physiques et d’autres composants infrastructurels, tels que l’alimentation électrique et le matériel réseau physique.</span><span class="sxs-lookup"><span data-stu-id="8020c-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="8020c-116">Des groupes à haute disponibilité garantissent que, pendant la maintenance, en cas de panne d’appareil ou lors d’autres temps d’arrêt, les machines virtuelles ne sont pas toutes affectées.</span><span class="sxs-lookup"><span data-stu-id="8020c-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="8020c-117">Un ensemble de disponibilité peuvent être ajouté tooan modèle d’Azure Resource Manager à l’aide de Visual Studio ajouter Assistant Nouvelle ressource de hello ou en insérant un JSON valide dans un modèle.</span><span class="sxs-lookup"><span data-stu-id="8020c-117">An Availability Set can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="8020c-118">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [à haute disponibilité](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span><span class="sxs-lookup"><span data-stu-id="8020c-118">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "avalibility-set"
  },
  "properties": {
    "platformUpdateDomainCount": 5,
    "platformFaultDomainCount": 3
  }
}
```

<span data-ttu-id="8020c-119">Un groupe à haute disponibilité est déclaré en tant que propriété d’une ressource de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8020c-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="8020c-120">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [association de groupe à haute disponibilité avec l’ordinateur virtuel](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span><span class="sxs-lookup"><span data-stu-id="8020c-120">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="8020c-121">Hello groupe à haute disponibilité comme hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8020c-121">hello availability set as seen from hello Azure portal.</span></span> <span data-ttu-id="8020c-122">Chaque ordinateur virtuel et les informations sur la configuration de hello sont décrits ici.</span><span class="sxs-lookup"><span data-stu-id="8020c-122">Each virtual machine and details about hello configuration are detailed here.</span></span>

![Groupe à haute disponibilité](./media/dotnet-core-4-availability-scale/aset.png)

<span data-ttu-id="8020c-124">Pour des informations détaillées sur les groupes à haute disponibilité, consultez [Gérer la disponibilité des machines virtuelles](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8020c-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="8020c-125">Équilibreur de charge réseau</span><span class="sxs-lookup"><span data-stu-id="8020c-125">Network Load Balancer</span></span>
<span data-ttu-id="8020c-126">Tandis que la haute disponibilité fournit la tolérance de panne d’application, un équilibrage de charge rend nombre d’instances de l’application hello disponibles sur une adresse réseau unique.</span><span class="sxs-lookup"><span data-stu-id="8020c-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of hello application available on a single network address.</span></span> <span data-ttu-id="8020c-127">Plusieurs instances d’une application peuvent être hébergés sur le nombre d’ordinateurs virtuels, chacun d’eux connecté équilibrage de charge tooa.</span><span class="sxs-lookup"><span data-stu-id="8020c-127">Multiple instances of an application can be hosted on many virtual machines, each one connected tooa load balancer.</span></span> <span data-ttu-id="8020c-128">Comme l’application hello est accessible, itinéraires de programme d’équilibrage de charge hello hello demande entrante entre les membres de hello attaché.</span><span class="sxs-lookup"><span data-stu-id="8020c-128">As hello application is accessed, hello load balancer routes hello incoming request across hello attached members.</span></span> <span data-ttu-id="8020c-129">Un équilibreur de charge peuvent être ajouté à l’aide de Visual Studio ajouter Assistant Nouvelle ressource de hello, ou en insérant correctement la mise en forme de ressources JSON dans le modèle du Gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8020c-129">A Load Balancer can be added using hello Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into hello Azure Resource Manager template.</span></span>

<span data-ttu-id="8020c-130">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [équilibrage de charge réseau](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span><span class="sxs-lookup"><span data-stu-id="8020c-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-front"
  },
  ........<truncated>
}
```

<span data-ttu-id="8020c-131">Exemple d’application hello étant exposée toohello internet avec une adresse IP publique, cette adresse est associée à équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="8020c-131">Because hello sample application is exposed toohello internet with a public IP address, this address is associated with hello load balancer.</span></span> 

<span data-ttu-id="8020c-132">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [association d’équilibrage de charge réseau avec adresse IP publique](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span><span class="sxs-lookup"><span data-stu-id="8020c-132">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span></span>

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

<span data-ttu-id="8020c-133">À partir de hello portail Azure, hello vue d’ensemble de programme d’équilibrage de charge réseau affiche hello association avec l’adresse IP publique de hello.</span><span class="sxs-lookup"><span data-stu-id="8020c-133">From hello Azure portal, hello network load balancer overview shows hello association with hello public IP address.</span></span>

![Équilibreur de charge réseau](./media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="8020c-135">Règle d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="8020c-135">Load Balancer Rule</span></span>
<span data-ttu-id="8020c-136">Lorsque vous utilisez un équilibrage de charge, les règles sont configurées qui contrôlent comment le trafic est équilibré entre les ressources hello prévu.</span><span class="sxs-lookup"><span data-stu-id="8020c-136">When using a load balancer, rules are configured that control how traffic is balanced across hello intended resources.</span></span> <span data-ttu-id="8020c-137">Application de magasin de musique exemple hello, le trafic arrive sur le port 80 de l’adresse IP publique de hello et est distribué sur le port 80 de tous les ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="8020c-137">With hello sample Music Store application, traffic arrives on port 80 of hello public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="8020c-138">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [règle d’équilibrage de charge](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span><span class="sxs-lookup"><span data-stu-id="8020c-138">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span>

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

<span data-ttu-id="8020c-139">Une vue du réseau de hello de charger la règle d’équilibrage à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="8020c-139">A view of hello network load balancer rule from hello portal.</span></span>

![Règle d’équilibreur de charge réseau](./media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="8020c-141">Sonde d’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="8020c-141">Load Balancer Probe</span></span>
<span data-ttu-id="8020c-142">équilibrage de charge Hello doit également toomonitor chaque ordinateur virtuel afin que les demandes sont pris en charge uniquement les systèmes toorunning.</span><span class="sxs-lookup"><span data-stu-id="8020c-142">hello load balancer also needs toomonitor each virtual machine so that requests are served only toorunning systems.</span></span> <span data-ttu-id="8020c-143">Cette surveillance s’effectue par sondage constant d’un port prédéfini.</span><span class="sxs-lookup"><span data-stu-id="8020c-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="8020c-144">déploiement du magasin de musique Hello est tooprobe configuré le port 80 sur tous les inclus virtuels.</span><span class="sxs-lookup"><span data-stu-id="8020c-144">hello Music Store deployment is configured tooprobe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="8020c-145">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [sonde d’équilibrage de charge](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span><span class="sxs-lookup"><span data-stu-id="8020c-145">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span></span>

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

<span data-ttu-id="8020c-146">Sonde d’équilibrage de charge Hello consulté à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8020c-146">hello load balancer probe seen from hello Azure portal.</span></span>

![Sonde d’équilibreur de charge réseau](./media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="8020c-148">Règles NAT de trafic entrant</span><span class="sxs-lookup"><span data-stu-id="8020c-148">Inbound NAT Rules</span></span>
<span data-ttu-id="8020c-149">Lorsque vous utilisez un équilibrage de charge, vous devez toobe règles mis en place qui fournissent l’accès à charge équilibrée de charge non tooeach Machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8020c-149">When using a Load Balancer, rules need toobe put into place that provide non-load balanced access tooeach Virtual Machine.</span></span> <span data-ttu-id="8020c-150">Par exemple, lors de la création d’une connexion SSH avec chaque machine virtuelle, ce trafic ne doit pas faire l’objet d’un équilibrage de charge. Au lieu de cela, un chemin d’accès prédéterminé doit être configuré.</span><span class="sxs-lookup"><span data-stu-id="8020c-150">For instance, when creating an SSH connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="8020c-151">Des chemins d’accès prédéterminés sont configurés à l’aide d’une ressource de règle NAT de trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="8020c-151">pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="8020c-152">À l’aide de cette ressource, les communications entrantes peuvent être mappé tooindividual Machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8020c-152">Using this resource, inbound communication can be mapped tooindividual Virtual Machines.</span></span> 

<span data-ttu-id="8020c-153">Un port en commençant à 5000 hello application de magasin de musique, est mappé tooport 22 sur chaque ordinateur virtuel pour l’accès SSH.</span><span class="sxs-lookup"><span data-stu-id="8020c-153">With hello Music Store application, a port starting at 5000 is mapped tooport 22 on each Virtual Machine for SSH access.</span></span> <span data-ttu-id="8020c-154">Hello `copyindex()` fonction est utilisée tooincrement hello port entrant, par exemple hello deuxième Machine virtuelle reçoit un port entrant de 5001, hello 5002 troisième et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="8020c-154">hello `copyindex()` function is used tooincrement hello incoming port, such that hello second Virtual Machine receives an incoming port of 5001, hello third 5002, and so on.</span></span> 

<span data-ttu-id="8020c-155">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [règles NAT de trafic entrant](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span><span class="sxs-lookup"><span data-stu-id="8020c-155">Follow this link toosee hello JSON sample within hello Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'SSH-VM', copyIndex())]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
  "location": "[resourceGroup().location]",
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
    "backendPort": 22,
    "enableFloatingIP": false
  }
}
```

<span data-ttu-id="8020c-156">Par exemple règle NAT de trafic entrant comme hello dans portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8020c-156">One example inbound NAT rule as seen in hello Azure portal.</span></span> <span data-ttu-id="8020c-157">Une règle NAT SSH est créée pour chaque ordinateur virtuel dans un déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="8020c-157">An SSH NAT rule is created for each virtual machine in hello deployment.</span></span>

![Règle NAT de trafic entrant](./media/dotnet-core-4-availability-scale/natrule.png)

<span data-ttu-id="8020c-159">Pour obtenir des informations détaillées sur hello équilibrage de charge réseau Azure, consultez [équilibrage de charge pour les services d’infrastructure Azure](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8020c-159">For in-depth information on hello Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="8020c-160">Déployer plusieurs machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="8020c-160">Deploy multiple VMs</span></span>
<span data-ttu-id="8020c-161">Enfin, pour une fonction de tooeffectively à haute disponibilité ou d’équilibrage de charge, plusieurs ordinateurs virtuels sont requis.</span><span class="sxs-lookup"><span data-stu-id="8020c-161">Finally, for an Availability Set or Load Balancer tooeffectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="8020c-162">Plusieurs machines virtuelles peuvent être déployés à l’aide de la fonction de copie de modèle Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="8020c-162">Multiple VMs can be deployed using hello Azure Resource Manager template copy function.</span></span> <span data-ttu-id="8020c-163">À l’aide de la fonction de copie hello, il n’est pas nécessaire toodefine un nombre fini de Machines virtuelles, plutôt cette valeur permettre être fournie de manière dynamique au moment de hello du déploiement.</span><span class="sxs-lookup"><span data-stu-id="8020c-163">Using hello copy function, it is not necessary toodefine a finite number of Virtual Machines, rather this value can be dynamically provided at hello time of deployment.</span></span> <span data-ttu-id="8020c-164">copier la fonction Hello consomme nombre hello de toocreated d’instances et les descripteurs de déploiement hello le nombre approprié d’ordinateurs virtuels et les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="8020c-164">hello copy function consumes hello number of instances toocreated and handles deploying hello proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="8020c-165">Dans le modèle d’exemple de magasin de musique hello, un paramètre est défini dans un nombre d’instances.</span><span class="sxs-lookup"><span data-stu-id="8020c-165">In hello Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="8020c-166">Ce numéro est utilisé dans l’ensemble du modèle de hello lors de la création d’ordinateurs virtuels et les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="8020c-166">This number is used throughout hello template when creating virtual machines and related resources.</span></span>

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 1,
  "metadata": {
    "description": "Number of VM instances toobe created behind load balancer."
  }
}
```

<span data-ttu-id="8020c-167">Hello ressource d’ordinateur virtuel, un nom est attribué à la boucle de copie hello et nombre hello du paramètre d’instances utilisé toocontrol un nombre hello de copies qui en résulte.</span><span class="sxs-lookup"><span data-stu-id="8020c-167">On hello Virtual Machine resource, hello copy loop is given a name and hello number of instances parameter used toocontrol hello number of resulting copies.</span></span>

<span data-ttu-id="8020c-168">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [fonction de copie de Machine virtuelle](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span><span class="sxs-lookup"><span data-stu-id="8020c-168">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span></span> 

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Compute/virtualMachines",
"name": "[concat(variables('vmName'),copyindex())]",
"location": "[resourceGroup().location]",
"copy": {
  "name": "virtualMachineLoop",
  "count": "[parameters('numberOfInstances')]"
}
```

<span data-ttu-id="8020c-169">itération actuelle de Hello de copier la fonction hello est accessible par hello `copyIndex()` (fonction).</span><span class="sxs-lookup"><span data-stu-id="8020c-169">hello current iteration of hello copy function can be accessed with hello `copyIndex()` function.</span></span> <span data-ttu-id="8020c-170">valeur de Hello de fonction d’index hello copie peut être utilisé tooname virtuels et autres ressources.</span><span class="sxs-lookup"><span data-stu-id="8020c-170">hello value of hello copy index function can be used tooname virtual machines and other resources.</span></span> <span data-ttu-id="8020c-171">Par exemple, si deux instances d’une machine virtuelle sont déployées, elles doivent porter des noms différents.</span><span class="sxs-lookup"><span data-stu-id="8020c-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="8020c-172">Hello `copyIndex()` fonction peut être utilisée comme nom de partie de la machine virtuelle de hello toocreate un nom unique.</span><span class="sxs-lookup"><span data-stu-id="8020c-172">hello `copyIndex()` function can be used as part of hello virtual machine name toocreate a unique name.</span></span> <span data-ttu-id="8020c-173">Un exemple de hello `copyindex()` fonction utilisée pour des raisons d’affectation de noms peut être consultée dans hello ressource d’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="8020c-173">An example of hello `copyindex()` function used for naming purposes can be seen in hello Virtual Machine resource.</span></span> <span data-ttu-id="8020c-174">Ici, le nom de l’ordinateur hello est une concaténation de hello `vmName` paramètre et hello `copyIndex()` (fonction).</span><span class="sxs-lookup"><span data-stu-id="8020c-174">Here, hello computer name is a concatenation of hello `vmName` parameter, and hello `copyIndex()` function.</span></span> 

<span data-ttu-id="8020c-175">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [copier la fonction Index](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span><span class="sxs-lookup"><span data-stu-id="8020c-175">Follow this link toosee hello JSON sample within hello Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span></span> 

```json
"osProfile": {
  "computerName": "[concat(parameters('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "linuxConfiguration": {
    "disablePasswordAuthentication": "true",
    "ssh": {
      "publicKeys": [
        {
          "path": "[variables('sshKeyPath')]",
          "keyData": "[parameters('sshKeyData')]"
        }
      ]
    }
  }
}
```

<span data-ttu-id="8020c-176">Hello `copyIndex` fonction est utilisée plusieurs fois dans l’exemple de modèle de magasin de musique hello.</span><span class="sxs-lookup"><span data-stu-id="8020c-176">hello `copyIndex` function is used several times in hello Music Store sample template.</span></span> <span data-ttu-id="8020c-177">Utilisation de fonctions et ressources `copyIndex` incluent tooa spécifique n’est pas défini une seule instance de machine virtuelle de hello comme interface de réseau, les règles d’équilibrage de charge, et les dépend des fonctions.</span><span class="sxs-lookup"><span data-stu-id="8020c-177">Resources and functions utilizing `copyIndex` include anything specific tooa single instance of hello virtual machine such as network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="8020c-178">Pour plus d’informations sur la fonction de copie hello, consultez [créer plusieurs instances de ressources dans Azure Resource Manager](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="8020c-178">For more information on hello copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="8020c-179">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="8020c-179">Next step</span></span>
<hr>

[<span data-ttu-id="8020c-180">Étape 4 : Déploiement d’application avec des modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8020c-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

