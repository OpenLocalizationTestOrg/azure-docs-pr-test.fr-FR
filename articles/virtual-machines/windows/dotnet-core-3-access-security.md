---
title: "aaaAccess et la sécurité dans les modèles pour les machines virtuelles Windows Azure | Documents Microsoft"
description: Didacticiel sur DotNet Core pour les machines virtuelles Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: e671fc45-5e4d-40fd-aac5-290892713cc0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4b8227ae745b3b0a22d136e98d18479f8b1504c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a>Accès et sécurité dans les modèles Azure Resource Manager pour les machines virtuelles Windows

Applications hébergées sur hello dans Azure probablement être toobe accès internet ou un réseau privé virtuel / connexion Express Route avec Azure. Avec l’exemple d’application hello magasin de musique, hello web site est rendue disponible sur hello internet avec une adresse IP publique. Avec un accès établi, connexions toohello accès aux applications et toohello ressources d’ordinateur virtuel eux-mêmes doivent être sécurisés. Cette sécurité d’accès est assurée à l’aide d’un groupe de sécurité réseau. 

Ce document décrit en détail comment sécuriser la hello application de magasin de musique dans le modèle de gestionnaire de ressources Azure exemple hello. Toutes les dépendances et configurations uniques sont en surbrillance. Pour une expérience optimale de hello, préalable déployer une instance de hello solution tooyour abonnement Azure et de travail en même temps que le modèle de gestionnaire de ressources Azure hello. modèle complète de Hello se trouve ici : [déploiement du magasin de musique sur Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="public-ip-address"></a>Adresse IP publique
tooprovide accès public tooan ressource Azure, une ressource d’adresse IP publique peut être utilisé. Une adresse IP publique peut être configurée avec une adresse IP statique ou dynamique. Si une adresse dynamique est utilisée et hello virtual machine est arrêtée et désallouée, les adresses hello est supprimé. Au prochain démarrage de machine de hello, il peut être affecté à une autre adresse IP publique. tooprevent une IP d’adresses à partir de la modification, une adresse IP réservée peut être utilisée. 

Modèle d’Azure Resource Manager tooan à l’aide de hello Visual Studio ajouter Assistant Nouvelle ressource, peut être ajoutée à une adresse IP publique ou en insérant un JSON valide dans un modèle. 

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [adresse IP publique](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicIpAddressName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "public-ip"
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

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [association d’adresse IP publique avec équilibrage de charge](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).

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

Hello adresse IP publique comme visibles sur hello portail Azure. Notez que l’adresse IP publique de hello est équilibrage de charge associé tooa et pas un ordinateur virtuel. Équilibreurs de charge réseau sont détaillées dans le document suivant de hello de cette série.

![Adresse IP publique](./media/dotnet-core-3-access-security/pubip-win.png)

Pour plus d’informations sur les adresses IP publiques Azure, consultez [Adresses IP dans Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).

## <a name="network-security-group"></a>Groupe de sécurité réseau
Une fois que l’accès a été établie tooAzure ressources, cet accès doit être limité. Pour des machines virtuelles Azure, la sécurisation de l’accès s’effectue à l’aide d’un groupe de sécurité réseau. Avec l’exemple d’application hello magasin de musique, machine virtuelle de tous les accès toohello est limitée à l’exception de via le port 80 pour l’accès http et le port 3389 pour accès RDP. Modèle d’Azure Resource Manager tooan à l’aide de hello Visual Studio ajouter Assistant Nouvelle ressource, peuvent être ajouté à un groupe de sécurité réseau ou en insérant un JSON valide dans un modèle.

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [groupe de sécurité réseau](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('networkSecurityGroup')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-security-group"
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
},
```

Dans cet exemple, un groupe de sécurité réseau hello est associé à un objet de sous-réseau hello déclaré dans une ressource de réseau virtuel hello. 

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [association du groupe de sécurité réseau avec un réseau virtuel](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).

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
]
```

Voici le groupe de sécurité réseau hello ressemble à partir de hello portail Azure. Notez qu’un groupe de sécurité réseau peut être associé à une interface réseau et/ou un sous-réseau. Dans ce cas, hello NSG est associé tooa sous-réseau. Dans cette configuration, hello règles de trafic entrant s’appliquent tooall machines virtuelles connectées toohello sous-réseau.

![Groupe de sécurité réseau](./media/dotnet-core-3-access-security/nsg-win.png)

Pour plus d’informations sur les groupes de sécurité réseau, consultez [Présentation du groupe de sécurité réseau](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).

## <a name="next-step"></a>Étape suivante
<hr>

[Étape 3 : disponibilité et mise à l’échelle dans les modèles Azure Resource Manager](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

