---
title: "aaaAvailability et l’échelle dans les modèles Azure Resource Manager | Documents Microsoft"
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
ms.openlocfilehash: a122d8e9536ea5fc2dc9c3f84042ed5c5179d783
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-windows-vms"></a>Disponibilité et scalabilité dans les modèles Azure Resource Manager pour les machines virtuelles Windows

Disponibilité et l’échelle, reportez-vous à la demande toomeet de capacité toouptime et hello. Si une application doit être de 99,9 % du temps de hello, il doit toohave une architecture qui permet à plusieurs ressources de calcul simultanées. Par exemple, au lieu d’avoir un seul site Web, une configuration avec un niveau plus élevé de disponibilité inclut plusieurs instances du hello même site, avec l’équilibrage de la technologie de face d’eux. Dans cette configuration, une seule instance de l’application hello peut être récupérée pour une maintenance, hello restant interrompre toofunction. Mise à l’échelle sur hello autre part fait référence à la demande de tooan applications capacité tooserve. Avec une charge application à charge équilibrée, ajouter ou supprimer des instances de pool de hello permet à une demande de toomeet tooscale application.

Ce document décrit en détail comment hello exemple de déploiement de magasin de musique est configuré pour la disponibilité et l’échelle. Toutes les dépendances et configurations uniques sont en surbrillance. Pour une expérience optimale de hello, préalable déployer une instance de hello solution tooyour abonnement Azure et de travail en même temps que le modèle de gestionnaire de ressources Azure hello. modèle complète de Hello se trouve ici : [déploiement du magasin de musique sur Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="availability-set"></a>Groupe à haute disponibilité
Un groupe à haute disponibilité étend logiquement des machines virtuelles Azure sur des hôtes physiques et d’autres composants infrastructurels, tels que l’alimentation électrique et le matériel réseau physique. Des groupes à haute disponibilité garantissent que, pendant la maintenance, en cas de panne d’appareil ou lors d’autres temps d’arrêt, les machines virtuelles ne sont pas toutes affectées. Un ensemble de disponibilité peuvent être ajouté tooan modèle d’Azure Resource Manager à l’aide de Visual Studio ajouter Assistant Nouvelle ressource de hello ou en insérant un JSON valide dans un modèle.

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [à haute disponibilité](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L368).

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

Un groupe à haute disponibilité est déclaré en tant que propriété d’une ressource de machine virtuelle. 

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [association de groupe à haute disponibilité avec l’ordinateur virtuel](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L302).

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
Hello groupe à haute disponibilité comme hello portail Azure. Chaque ordinateur virtuel et les informations sur la configuration de hello sont décrits ici.

![Groupe à haute disponibilité](./media/dotnet-core-4-availability-scale/ase-win.png)

Pour des informations détaillées sur les groupes à haute disponibilité, consultez [Gérer la disponibilité des machines virtuelles](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="network-load-balancer"></a>Équilibreur de charge réseau
Tandis que la haute disponibilité fournit la tolérance de panne d’application, un équilibrage de charge rend nombre d’instances de l’application hello disponibles sur une adresse réseau unique. Plusieurs instances d’une application peuvent être hébergés sur le nombre d’ordinateurs virtuels, chacun d’eux connecté équilibrage de charge tooa. Comme l’application hello est accessible, itinéraires de programme d’équilibrage de charge hello hello demande entrante entre les membres de hello attaché. Un équilibreur de charge peuvent être ajouté à l’aide de Visual Studio ajouter Assistant Nouvelle ressource de hello, ou en insérant correctement la mise en forme de ressources JSON dans le modèle du Gestionnaire de ressources Azure hello.

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [équilibrage de charge réseau](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L198).

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

Exemple d’application hello étant exposée toohello internet avec une adresse IP publique, cette adresse est associée à équilibrage de charge hello. 

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [association d’équilibrage de charge réseau avec adresse IP publique](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).

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

À partir de hello portail Azure, hello vue d’ensemble de programme d’équilibrage de charge réseau affiche hello association avec l’adresse IP publique de hello.

![Équilibreur de charge réseau](./media/dotnet-core-4-availability-scale/nlb-win.png)

## <a name="load-balancer-rule"></a>Règle d’équilibrage de charge
Lorsque vous utilisez un équilibrage de charge, les règles sont configurées qui contrôlent comment le trafic est équilibré entre les ressources hello prévu. Application de magasin de musique exemple hello, le trafic arrive sur le port 80 de l’adresse IP publique de hello et est distribué sur le port 80 de tous les ordinateurs virtuels. 

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [règle d’équilibrage de charge](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L226).

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

Une vue du réseau de hello de charger la règle d’équilibrage à partir du portail de hello.

![Règle d’équilibreur de charge réseau](./media/dotnet-core-4-availability-scale/lbrule-win.png)

## <a name="load-balancer-probe"></a>Sonde d’équilibreur de charge
équilibrage de charge Hello doit également toomonitor chaque ordinateur virtuel afin que les demandes sont pris en charge uniquement les systèmes toorunning. Cette surveillance s’effectue par sondage constant d’un port prédéfini. déploiement du magasin de musique Hello est tooprobe configuré le port 80 sur tous les inclus virtuels. 

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [sonde d’équilibrage de charge](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L247).

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

Sonde d’équilibrage de charge Hello consulté à partir de hello portail Azure.

![Sonde d’équilibreur de charge réseau](./media/dotnet-core-4-availability-scale/lbprobe-win.png)

## <a name="inbound-nat-rules"></a>Règles NAT de trafic entrant
Lorsque vous utilisez un équilibrage de charge, vous devez toobe règles mis en place qui fournissent l’accès à charge équilibrée de charge non tooeach Machine virtuelle. Par exemple, lors de la création d’une connexion RDP avec chaque machine virtuelle, ce trafic ne doit pas faire l’objet d’un équilibrage de charge. Au lieu de cela, un chemin d’accès prédéterminé doit être configuré. Des chemins d’accès prédéterminés sont configurés à l’aide d’une ressource de règle NAT de trafic entrant. À l’aide de cette ressource, les communications entrantes peuvent être mappé tooindividual Machines virtuelles. 

Un port en commençant à 5000 hello application de magasin de musique, est mappé tooport 3389 sur chaque ordinateur virtuel pour l’accès RDP. Hello `copyindex()` fonction est utilisée tooincrement hello port entrant, par exemple hello deuxième Machine virtuelle reçoit un port entrant de 5001, hello 5002 troisième et ainsi de suite.

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [règles NAT de trafic entrant](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L260). 

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

Par exemple règle NAT de trafic entrant comme hello dans portail Azure. Une règle NAT de RDP est créée pour chaque ordinateur virtuel dans un déploiement de hello.

![Règle NAT de trafic entrant](./media/dotnet-core-4-availability-scale/natrule-win.png)

Pour obtenir des informations détaillées sur hello équilibrage de charge réseau Azure, consultez [équilibrage de charge pour les services d’infrastructure Azure](load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="deploy-multiple-vms"></a>Déployer plusieurs machines virtuelles
Enfin, pour une fonction de tooeffectively à haute disponibilité ou d’équilibrage de charge, plusieurs ordinateurs virtuels sont requis. Plusieurs machines virtuelles peuvent être déployés à l’aide de la fonction de copie de modèle Azure Resource Manager hello. À l’aide de la fonction de copie hello, il n’est pas nécessaire toodefine un nombre fini de Machines virtuelles, plutôt cette valeur permettre être fournie de manière dynamique au moment de hello du déploiement. copier la fonction Hello consomme nombre hello de toobe instances créée et les handles déploiement hello le nombre approprié d’ordinateurs virtuels et les ressources associées.

Dans le modèle d’exemple de magasin de musique hello, un paramètre est défini dans un nombre d’instances. Ce numéro est utilisé dans l’ensemble du modèle de hello lors de la création d’ordinateurs virtuels et les ressources associées.

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 2,
  "metadata": {
    "description": "Number of VM instances toobe created behind load balancer."
  }
},
```

Hello ressource d’ordinateur virtuel, un nom est attribué à la boucle de copie hello et nombre hello du paramètre d’instances utilisé toocontrol un nombre hello de copies qui en résulte.

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [fonction de copie de Machine virtuelle](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L290). 

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

itération actuelle de Hello de copier la fonction hello est accessible par hello `copyIndex()` (fonction). valeur de Hello de fonction d’index hello copie peut être utilisé tooname virtuels et autres ressources. Par exemple, si deux instances d’une machine virtuelle sont déployées, elles doivent porter des noms différents. Hello `copyIndex()` fonction peut être utilisée comme nom de partie de la machine virtuelle de hello toocreate un nom unique. Un exemple de hello `copyindex()` fonction utilisée pour des raisons d’affectation de noms peut être consultée dans hello ressource d’ordinateur virtuel. Ici, le nom de l’ordinateur hello est une concaténation de hello `vmName` paramètre et hello `copyIndex()` (fonction). 

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [copier la fonction Index](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L309). 

```json
"osProfile": {
  "computerName": "[concat(variables('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "adminPassword": "[parameters('adminPassword')]"
}
```

Hello `copyIndex` fonction est utilisée plusieurs fois dans l’exemple de modèle de magasin de musique hello. Utilisation de fonctions et ressources `copyIndex` incluent tooa spécifique n’est pas défini une seule instance de hello virtuels tels et l’interface réseau, les règles d’équilibrage de charge, et les dépend des fonctions. 

Pour plus d’informations sur la fonction de copie hello, consultez [créer plusieurs instances de ressources dans Azure Resource Manager](../../resource-group-create-multiple.md).

## <a name="next-step"></a>Étape suivante
<hr>

[Étape 4 : Déploiement d’application avec des modèles Azure Resource Manager](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

