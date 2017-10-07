---
title: "topologie de l’Observateur réseau Azure aaaView - PowerShell | Documents Microsoft"
description: "Cet article décrit comment toouse PowerShell tooquery topologie de votre réseau."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: bd0e882d-8011-45e8-a7ce-de231a69fb85
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2bc0ecf5baa81a68be53f55c74f362a7bc97116f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a>Afficher la topologie Network Watcher par le biais de PowerShell

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [CLI 1.0](network-watcher-topology-cli-nodejs.md)
> - [CLI 2.0](network-watcher-topology-cli.md)
> - [API REST](network-watcher-topology-rest.md)

fonctionnalité de topologie Hello de l’Observateur réseau fournit une représentation visuelle des ressources du réseau hello dans un abonnement. Dans le portail hello, cette visualisation est présentée tooyou automatiquement. informations Hello derrière l’affichage de la topologie hello dans le portail de hello peuvent être récupérées via PowerShell.
Cette fonctionnalité rend les informations de topologie hello plus polyvalente que les données de salutation peuvent être utilisées par les autres toobuild outils out visualisation de hello.

interconnexion de Hello est modélisée sous deux relations.

- **Relation d’imbrication** - exemple : le réseau virtuel contient un sous-réseau qui contient une carte réseau
- **Associé** - exemple : une carte réseau est associée à une machine virtuelle

Hello Voici les propriétés qui sont retournées lors de l’interrogation hello API REST de topologie.

* **nom** hello - nom de ressource de hello
* **ID** -hello uri de ressource de hello.
* **emplacement** -hello emplacement où se trouve hello ressource.
* **associations** -liste des associations toohello référencé l’objet.
    * **nom** -nom de hello de hello référencé des ressources.
    * **ID de ressource** -hello resourceId est hello les uri de ressource hello référencé dans l’association de hello.
    * **l’associationType** -relation hello entre l’objet de hello enfant et parent de hello fait référence à cette valeur. Les valeurs valides sont **Contains** et **Associated**.

## <a name="before-you-begin"></a>Avant de commencer

Dans ce scénario, vous utilisez hello `Get-AzureRmNetworkWatcherTopology` informations de topologie d’applet de commande tooretrieve hello. Il existe également un article sur la façon de trop[récupérer la topologie du réseau avec l’API REST](network-watcher-topology-rest.md).

Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.

## <a name="scenario"></a>Scénario

scénario Hello abordée dans cet article récupère hello topologie de réponse pour un groupe de ressources donné.

## <a name="retrieve-network-watcher"></a>Récupérer Network Watcher

première étape de Hello est instance de l’Observateur réseau tooretrieve hello. Hello `$networkWatcher` variable est passée toohello `Get-AzureRmNetworkWatcherTopology` applet de commande.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a>Récupérer la topologie

Hello `Get-AzureRmNetworkWatcherTopology` applet de commande extrait la topologie hello pour un groupe de ressources donné.

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a>Résultats

Hello résultats retournés ont une propriété de nom « ressources », qui contient le corps de réponse json hello pour hello `Get-AzureRmNetworkWatcherTopology` applet de commande.  réponse de Hello contient des ressources de hello dans hello groupe de sécurité réseau et leurs associations (autrement dit, Contains, associée).

```json
Id              : 00000000-0000-0000-0000-000000000000
CreatedDateTime : 2/1/2017 7:52:21 PM
LastModified    : 2/1/2017 7:46:18 PM
Resources       : [
                    {
                      "Name": "testrg-vnet",
                      "Id":
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet/subnets/default"
                        }
                      ]
                    },
                    {
                      "Name": "default",
                      "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testr
                  g-vnet/subnets/default",
                      "Location": "westcentralus",
                      "Associations": []
                    },
                    {
                      "Name": "testrg-vnet2",
                      "Id": 
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet2",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/default"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "GatewaySubnet",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/GatewaySubnet"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "gateway2",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworkGateways/gateway2"
                        }
                      ]
                    },
                    ...
                  ]
```

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment toovisualize votre flux de groupe de sécurité réseau se connecte à Power BI en vous rendant sur [NSG de visualiser les flux de journaux avec Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)


