---
title: "aaaFind tronçon suivant avec Azure réseau observateur du tronçon suivant - REST | Documents Microsoft"
description: "Cet article décrit comment vous pouvez trouver le hello de type de tronçon suivant est et l’adresse ip à l’aide de tronçon suivant hello API REST Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a2b61b355aae8ae513ebd44837184fbc6cfd668c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a>Savoir quel type de tronçon suivant hello est à l’aide de capacité de tronçon suivant hello dans l’Observateur réseau de Aure à l’aide des API REST Azure

> [!div class="op_single_selector"]
> - [Portail Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [API REST Azure](network-watcher-check-next-hop-rest.md)

Tronçon suivant est une fonctionnalité de l’Observateur réseau qui offre la possibilité de hello obtenir le type de tronçon suivant hello et l’adresse IP basée sur une machine virtuelle spécifiée. Cette fonctionnalité est utile pour déterminer si le trafic en laissant une machine virtuelle traverse une passerelle, internet ou des réseaux virtuels tooget tooits destination.

## <a name="before-you-begin"></a>Avant de commencer

ARMclient est utilisé toocall hello REST API à l’aide de PowerShell. ARMClient est accessible sur le site chocolatey à partir de la page [ARMClient sur Chocolatey](https://chocolatey.org/packages/ARMClient).

Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.

## <a name="scenario"></a>Scénario

scénario de Hello abordée dans cet article utilise le saut suivant, une fonctionnalité de l’Observateur réseau qui recherche le type de tronçon suivant hello et une adresse IP pour une ressource. toolearn en savoir plus sur le tronçon suivant, visitez [vue d’ensemble du tronçon suivant](network-watcher-next-hop-overview.md).

Dans ce scénario, vous allez :

* Récupérer le saut suivant de hello pour un ordinateur virtuel.

## <a name="log-in-with-armclient"></a>Se connecter à ARMClient

Ouvrez une session dans tooarmclient avec vos informations d’identification Azure.

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>Récupérer une machine virtuelle

Exécutez hello suivant script tooreturn une machine virtuelle. Ces informations sont nécessaires pour l’exécution de la fonctionnalité Tronçon suivant.

Hello suivant code doit valeurs pour hello suivant variables :

- **ID d’abonnement** -hello toouse de Id d’abonnement.
- **resourceGroupName** hello - nom du groupe de ressources qui contient des machines virtuelles.

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

À partir de la sortie suivante de hello, id de hello de machine virtuelle de hello est utilisée dans hello l’exemple suivant :

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="get-next-hop"></a>Obtenir le tronçon suivant

Une fois créé, l’en-tête d’autorisation hello saut suivant de hello à partir d’un ordinateur virtuel peut être récupéré. Hello valeurs suivantes doivent être remplacées pour hello code exemple toowork.

> [!Important]
> Pour l’API REST de l’Observateur réseau appels hello nom de groupe de ressources dans la demande de hello QU'URI est le groupe de ressources hello contient hello Observateur réseau, pas les ressources hello vous effectuez des actions de diagnostic hello sur.

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> Tronçon suivant requiert que les ressources d’ordinateur virtuel hello est allouée toorun.

## <a name="results"></a>Résultats

Bonjour extrait de code suivant est un exemple de sortie hello reçu. les résultats de Hello contiennent hello valeurs suivantes :

* **type de tronçon suivant** -cette valeur est une des valeurs suivantes de hello : Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway ou None.
* **nextHopIpAddress** -hello l’adresse IP du tronçon suivant de hello.
* **routeTableId** - hello valeur est soit un uri pour la table d’itinéraires hello associé hello itinéraire, ou si non défini par l’utilisateur itinéraire valeur hello défini de *système itinéraire* est retourné.

Hello Voici les résultats hello au format json.

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez été en mesure de toofind out saut suivant de hello pour un ordinateur virtuel, vous pouvez afficher la sécurité hello de ressources de votre réseau en vous rendant sur [vue d’ensemble de la vue de la sécurité](network-watcher-security-group-view-overview.md)














