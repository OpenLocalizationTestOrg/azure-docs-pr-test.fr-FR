---
title: "aaaDeploying de ressources de calcul Windows avec des modèles de gestionnaire de ressources Azure | Documents Microsoft"
description: Didacticiel sur DotNet Core pour les machines virtuelles Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b026fe81-1bc1-4899-ac32-886091671498
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dee228a492b08053713829e156e5b5ba304d7588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-windows-vms"></a>Architecture d’application avec des modèles Azure Resource Manager pour les machines virtuelles Windows

Lors du développement d’un déploiement d’Azure Resource Manager, de calcul des besoins de services et des ressources de tooAzure toobe mappé. Si une application se compose de plusieurs points de terminaison http, une base de données et un service de mise en cache de données, hello des ressources Azure qui hébergent chacun de ces composants doit toobe version rationalisé. Par exemple, application de magasin de musique exemple hello inclut une application web qui est hébergée sur un ordinateur virtuel et une base de données SQL, qui est hébergé dans la base de données SQL Azure. 

Ce document décrit en détail comment les ressources de calcul du magasin de musique hello sont configurés dans le modèle de gestionnaire de ressources Azure exemple hello. Toutes les dépendances et configurations uniques sont en surbrillance. Pour une expérience optimale de hello, préalable déployer une instance de hello solution tooyour abonnement Azure et de travail en même temps que le modèle de gestionnaire de ressources Azure hello. modèle complète de Hello se trouve ici : [déploiement du magasin de musique sur Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="virtual-machine"></a>Machine virtuelle
Hello application de magasin de musique inclut une application web où les clients peuvent rechercher et acquérir de la musique. Bien qu’il existe plusieurs services Azure capables d’héberger des applications web, pour cet exemple, une machine virtuelle est utilisée. À l’aide du modèle de magasin de musique exemple hello, un ordinateur virtuel est déployé, un serveur web installer et site Web du magasin de musique hello installé et configuré. Par souci de hello de cet article, le déploiement d’ordinateurs virtuels uniquement hello est détaillé. configuration Hello du serveur web de hello et application hello est détaillée dans un article de la version ultérieure.

Modèle de tooa à l’aide de Visual Studio ajouter une nouvelle ressource, Assistant ou en insérant un JSON valide dans le modèle de déploiement hello de hello peut être ajouté à un ordinateur virtuel. Lors du déploiement d’une machine virtuelle, plusieurs ressources associées sont également nécessaires. Si vous utilisez le modèle de Visual Studio toocreate hello, ces ressources sont créés pour vous. Si vous construisez manuellement le modèle de hello, ces ressources doivent toobe inséré et configuré.

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [JSON de l’ordinateur virtuel](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).

```json
{
  {
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "tags": {
    "displayName": "virtual-machine"
  },
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('vhdStorageName'))]",
    "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]",
    "nicLoop"
  ],
  "properties": {
    "availabilitySet": {
      "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
    },
  ........<truncated>  
}
```

Une fois déployé, les propriétés d’une machine virtuelle hello peuvent être consultées dans hello portail Azure.

![Machine virtuelle](./media/dotnet-core-2-architecture/vm-win.png)

## <a name="storage-account"></a>Compte de stockage
Les comptes de stockage offrent de nombreuses options et fonctionnalités de stockage. Pour le contexte de hello de machines virtuelles Azure, un compte de stockage conserve des disques durs virtuels hello de machine virtuelle de hello et toutes les autres disques de données. exemple de magasin de musique Hello comprend un stockage compte toohold hello disque dur virtuel de chaque ordinateur virtuel dans un déploiement de hello. 

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [compte de stockage](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[variables('vhdStorageName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "storage-account"
  },
  "properties": {
    "accountType": "[variables('vhdStorageType')]"
  }
}
```

Un compte de stockage est associé à un ordinateur virtuel à l’intérieur de déclaration de modèle hello Gestionnaire de ressources de l’ordinateur virtuel de hello. 

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [association de Machine virtuelle et le compte de stockage](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).

```json
"osDisk": {
  "name": "osdisk",
  "vhd": {
    "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/',variables('vhdStorageName')), '2015-06-15').primaryEndpoints.blob,'vhds/osdisk', copyindex(), '.vhd')]"
  },
  "caching": "ReadWrite",
  "createOption": "FromImage"
}
```

Après le déploiement, compte de stockage hello peut être consultée dans hello portail Azure.

![Compte de stockage](./media/dotnet-core-2-architecture/storacct-win.png)

En cliquant sur dans le conteneur objets blob du compte de stockage hello, le fichier de disque dur virtuel hello pour chaque ordinateur virtuel déployé avec le modèle de hello peut être consulté.

![Disques durs virtuels](./media/dotnet-core-2-architecture/vhd-win.png)

Pour plus d’informations sur Stockage Azure, voir la [documentation d’Azure Storage](https://azure.microsoft.com/documentation/services/storage/).

## <a name="virtual-network"></a>Réseau virtuel
Si un ordinateur virtuel nécessite la mise en réseau interne comme toocommunicate de capacité hello avec d’autres machines virtuelles et les ressources Azure, un réseau virtuel Azure est requis.  Un réseau virtuel ne fait pas hello virtual machine accessible sur internet de hello. La connectivité publique requiert une adresse IP publique, qui est détaillée plus loin dans cette série.

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [réseau virtuel et sous-réseaux](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/networkSecurityGroups/', variables('networkSecurityGroup'))]"
  ],
  "tags": {
    "displayName": "virtual-network"
  },
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/24"
      ]
    },
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
  }
}
```

À partir de hello portail Azure, réseau virtuel de hello ressemble hello suivant l’image. Notez que tous les ordinateurs virtuels déployés avec le modèle de hello sont attachés toohello les réseaux virtuels.

![Réseau virtuel](./media/dotnet-core-2-architecture/vnet-win.png)

## <a name="network-interface"></a>Interface réseau
 Une interface réseau connecte à un réseau virtuel de machine virtuelle tooa, le plus précisément les sous-réseaux tooa a été défini dans le réseau virtuel de hello. 

 Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [Interface réseau](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceName'), copyindex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-interface"
  },
  "copy": {
    "name": "nicLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
    "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIpAddressName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'RDP-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "subnet": {
            "id": "[variables('subnetRef')]"
          },
          "loadBalancerBackendAddressPools": [
            {
              "id": "[variables('lbPoolID')]"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "[concat(variables('lbID'),'/inboundNatRules/RDP-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

Chaque ressource de machine virtuelle comprend un profil réseau. interface de réseau Hello est associé à la machine virtuelle de hello dans ce profil.  

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [profil réseau de Machine virtuelle](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceName'), copyindex()))]"
    }
  ]
}
```

À partir de hello portail Azure, interface de réseau hello ressemble hello suivant l’image. adresse IP interne de Hello et l’association de machine virtuelle hello peuvent être consultés sur la ressource d’interface réseau hello.

![Interface réseau](./media/dotnet-core-2-architecture/nic-win.png)

Pour plus d’informations sur les réseaux virtuels Azure, voir la [du réseau virtuel Azure](https://azure.microsoft.com/documentation/services/virtual-network/).

## <a name="azure-sql-database"></a>Base de données SQL Azure
En outre, ordinateur virtuel de tooa qui héberge le site Web du magasin de musique hello, une base de données SQL Azure est base de données du magasin de musique toohost déployé hello. présente l’avantage Hello ici de base de données SQL Azure est un deuxième ensemble d’ordinateurs virtuels n’est pas nécessaire que l’échelle et la disponibilité est intégrée à service de hello.

Une base de données SQL Azure peut être ajouté à l’aide de Visual Studio ajouter une nouvelle ressource, Assistant ou en insérant un JSON valide dans un modèle de hello. Hello ressource SQL Server inclut un nom d’utilisateur et un mot de passe disposant de droits d’administrateur sur l’instance SQL hello. Par ailleurs, une ressource de pare-feu SQL est ajoutée. Par défaut, les applications hébergées dans Azure sont en mesure de tooconnect avec l’instance SQL hello. application tooallow externe telle une SQL Server Management studio tooconnect toohello instance SQL, pare-feu de hello doit toobe configuré. Par souci de hello de démonstration du magasin de musique hello, configuration par défaut de hello est correct. 

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [base de données SQL Azure](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicstoresqlName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('adminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicstoresqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

Une vue de hello SQL server et de la base de données MusicStore comme Bonjour portail Azure.

![SQL Server](./media/dotnet-core-2-architecture/sql-win.png)

Pour plus d’informations sur le déploiement d’Azure SQL Database, voir la [Documentation d’Azure SQL Database](https://azure.microsoft.com/documentation/services/sql-database/).

## <a name="next-step"></a>Étape suivante
<hr>

[Étape 2 : accès et sécurité dans les modèles Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

