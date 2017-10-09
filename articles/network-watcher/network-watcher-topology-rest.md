---
title: "topologie de l’Observateur réseau Azure aaaView - API REST | Documents Microsoft"
description: "Cet article décrit comment toouse REST API tooquery topologie de votre réseau."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: de9af643-aea1-4c4c-89c5-21f1bf334c06
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 39292025bcd561f007c9e31271b1389be48ea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a>Afficher la topologie Azure Network Watcher par le biais de l’API REST

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

Ce scénario, vous permet de récupérer les informations de topologie hello. ARMclient est utilisé toocall hello REST API à l’aide de PowerShell. ARMClient est accessible sur le site chocolatey à partir de la page [ARMClient sur Chocolatey](https://chocolatey.org/packages/ARMClient).

Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.

## <a name="scenario"></a>Scénario

scénario Hello abordée dans cet article récupère hello topologie de réponse pour un groupe de ressources donné.

## <a name="log-in-with-armclient"></a>Se connecter à ARMClient

Ouvrez une session dans tooarmclient avec vos informations d’identification Azure.

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a>Récupérer la topologie

Hello, l’exemple suivant demande la topologie de hello hello API REST.  exemple de Hello est paramétrable tooallow pour une grande souplesse pour la création d’un exemple.  Remplacez toutes les valeurs avec \< \> qui les entoure.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name toorun topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

Hello suivant la réponse est un exemple d’une réponse raccourcie qui est retourné lorsque récupérer la topologie pour un groupe de ressources :

```json
{
  "id": "ecd6c860-9cf5-411a-bdba-512f8df7799f",
  "createdDateTime": "2017-01-18T04:13:07.1974591Z",
  "lastModified": "2017-01-17T22:11:52.3527348Z",
  "resources": [
    {
      "name": "virtualNetwork1",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}",
      "location": "westcentralus",
      "associations": [
        {
          "name": "{subnetName}",
          "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/(virtualNetworkName)/subnets
/{subnetName}",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "webtestnsg-wjplxls65qcto",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}
s65qcto",
      "associationType": "Associated"
    },
    ...
  ]
}
```

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment toovisualize votre flux de groupe de sécurité réseau se connecte à Power BI en vous rendant sur [NSG de visualiser les flux de journaux avec Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)

