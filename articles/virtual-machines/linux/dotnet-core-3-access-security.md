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
# <a name="access-and-security-in-azure-resource-manager-templates-for-linux-vms"></a>Accès et sécurité dans les modèles Azure Resource Manager pour les machines virtuelles Linux

Applications hébergées sur hello dans Azure probablement être toobe accès internet ou un réseau privé virtuel / connexion Express Route avec Azure. Avec l’exemple d’application hello magasin de musique, hello web site est rendue disponible sur hello internet avec une adresse IP publique. Avec un accès établi, connexions toohello accès aux applications et toohello ressources d’ordinateur virtuel eux-mêmes doivent être sécurisés. Cette sécurité d’accès est assurée à l’aide d’un groupe de sécurité réseau. 

Ce document décrit en détail comment sécuriser la hello application de magasin de musique dans le modèle de gestionnaire de ressources Azure exemple hello. Toutes les dépendances et configurations uniques sont en surbrillance. Pour une expérience optimale de hello, préalable déployer une instance de hello solution tooyour abonnement Azure et de travail en même temps que le modèle de gestionnaire de ressources Azure hello. modèle complète de Hello se trouve ici : [déploiement du magasin de musique sur Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux). 

## <a name="public-ip-address"></a>Adresse IP publique
tooprovide accès public tooan ressource Azure, une ressource d’adresse IP publique peut être utilisé. Une adresse IP publique peut être configurée avec une adresse IP statique ou dynamique. Si une adresse dynamique est utilisée et hello virtual machine est arrêtée et désallouée, les adresses hello est supprimé. Au prochain démarrage de machine de hello, il peut être affecté à une autre adresse IP publique. tooprevent une IP d’adresses à partir de la modification, une adresse IP réservée peut être utilisée. 

Modèle d’Azure Resource Manager tooan à l’aide de hello Visual Studio ajouter Assistant Nouvelle ressource, peut être ajoutée à une adresse IP publique ou en insérant un JSON valide dans un modèle. 

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [adresse IP publique](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L121).

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

Une adresse IP publique peut être associée à une carte réseau virtuelle ou à un équilibreur de charge. Dans cet exemple, hello du site Web du magasin de musique étant à charge équilibrée entre plusieurs machines virtuelles, hello adresse IP publique est attaché toohello équilibrage de charge.

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [association d’adresse IP publique avec équilibrage de charge](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).

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

Hello adresse IP publique comme visibles sur hello portail Azure. Notez que l’adresse IP publique de hello est équilibrage de charge associé tooa et pas un ordinateur virtuel. Équilibreurs de charge réseau sont détaillées dans le document suivant de hello de cette série.

![Adresse IP publique](./media/dotnet-core-3-access-security/pubip.png)

Pour plus d’informations sur les adresses IP publiques Azure, consultez [Adresses IP dans Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).

## <a name="network-security-group"></a>Groupe de sécurité réseau
Une fois que l’accès a été établie tooAzure ressources, cet accès doit être limité. Pour des machines virtuelles Azure, la sécurisation de l’accès s’effectue à l’aide d’un groupe de sécurité réseau. Avec l’exemple d’application hello magasin de musique, machine virtuelle de tous les accès toohello est limitée à l’exception de via le port 80 pour l’accès http et le port 22 pour l’accès SSH. Modèle d’Azure Resource Manager tooan à l’aide de hello Visual Studio ajouter Assistant Nouvelle ressource, peuvent être ajouté à un groupe de sécurité réseau ou en insérant un JSON valide dans un modèle.

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [groupe de sécurité réseau](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L68).

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

Dans cet exemple, un groupe de sécurité réseau hello est associé à un objet de sous-réseau hello déclaré dans une ressource de réseau virtuel hello. 

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [association du groupe de sécurité réseau avec un réseau virtuel](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L158).

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

Voici le groupe de sécurité réseau hello ressemble à partir de hello portail Azure. Notez qu’un groupe de sécurité réseau peut être associé à une interface réseau et/ou un sous-réseau. Dans ce cas, hello NSG est associé tooa sous-réseau. Dans cette configuration, hello règles de trafic entrant s’appliquent tooall machines virtuelles connectées toohello sous-réseau.

![Groupe de sécurité réseau](./media/dotnet-core-3-access-security/nsg.png)

Pour plus d’informations sur les groupes de sécurité réseau, consultez [Présentation du groupe de sécurité réseau](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).

## <a name="next-step"></a>Étape suivante
<hr>

[Étape 3 : disponibilité et mise à l’échelle dans les modèles Azure Resource Manager](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

