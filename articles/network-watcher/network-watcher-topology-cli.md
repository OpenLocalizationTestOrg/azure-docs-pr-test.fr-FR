---
title: "topologie de l’Observateur réseau Azure aaaView - CLI d’Azure | Documents Microsoft"
description: "Cet article décrit comment toouse CLI d’Azure tooquery topologie de votre réseau."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 5cd279d7-3ab0-4813-aaa4-6a648bf74e7b
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: afa7e7dd844ecb2ab4c616ba99fa0a433f1e4ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli"></a>Afficher la topologie Azure Network Watcher par le biais de l’interface de ligne de commande Azure

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [CLI 1.0](network-watcher-topology-cli-nodejs.md)
> - [CLI 2.0](network-watcher-topology-cli.md)
> - [API REST](network-watcher-topology-rest.md)

fonctionnalité de topologie Hello de l’Observateur réseau fournit une représentation visuelle des ressources du réseau hello dans un abonnement. Dans le portail hello, cette visualisation est présentée tooyou automatiquement. informations Hello derrière l’affichage de la topologie hello dans le portail de hello peuvent être récupérées via PowerShell.
Cette fonctionnalité rend les informations de topologie hello plus polyvalente que les données de salutation peuvent être utilisées par les autres toobuild outils out visualisation de hello.

Cet article utilise l’interface Azure CLI 1.0 interplateforme, disponible pour Windows, Mac et Linux. Network Watcher utilise actuellement Azure CLI 1.0 pour la prise en charge d’interface CLI.

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

Dans ce scénario, vous utilisez hello `network watcher topology` informations de topologie d’applet de commande tooretrieve hello. Il existe également un article sur la façon de trop[récupérer la topologie du réseau avec l’API REST](network-watcher-topology-rest.md).

Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.

## <a name="scenario"></a>Scénario

scénario Hello abordée dans cet article récupère hello topologie de réponse pour un groupe de ressources donné.

## <a name="retrieve-topology"></a>Récupérer la topologie

Hello `network watcher topology` applet de commande extrait la topologie hello pour un groupe de ressources donné. Ajouter un argument de hello »--json « oput de hello tooview au format json

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a>Résultats

Hello résultats retournés ont une propriété de nom « ressources », qui contient le corps de réponse json hello pour hello `network watcher topology` applet de commande.  réponse de Hello contient des ressources de hello dans hello groupe de sécurité réseau et leurs associations (autrement dit, Contains, associée).

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "createdDateTime": "2017-02-17T22:20:59.461Z",
  "lastModified": "2016-12-19T22:23:02.546Z",
  "resources": [
    {
      "name": "testrg-vnet",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
      "location": "westcentralus",
      "associations": [
        {
          "name": "default",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "default",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
      "location": "westcentralus",
      "associations": []
    },
    {
      "name": "testclient",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testclient",
      "location": "westcentralus",
      "associations": [
        {
          "name": "testNic",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testNic",
          "associationType": "Contains"
        }
      ]
    },
    ...    
  ]
}
```

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur les règles de sécurité hello qui sont des ressources du réseau tooyour appliqué en vous rendant sur [présentation du mode de groupe de sécurité](network-watcher-security-group-view-overview.md)
