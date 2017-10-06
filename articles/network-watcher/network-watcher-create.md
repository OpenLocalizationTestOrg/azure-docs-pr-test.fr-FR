---
title: "aaaCreate une instance de l’Observateur réseau Azure | Documents Microsoft"
description: "Cette page fournit hello étapes toocreate une instance de l’Observateur réseau à l’aide du portail de hello et l’API REST Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 90d4f90c9709a80e4b27863e79e5b6e16de145c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-network-watcher-instance"></a>Créer une instance d’Azure Network Watcher

Observateur réseau est un service régional qui permet de vous toomonitor et diagnostiquer des conditions à un niveau de scénario réseau, vers et depuis Azure. Surveillance au niveau du scénario vous permet de problèmes toodiagnose à une vue au niveau du réseau tooend fin. Diagnostic de réseau et les outils de visualisation disponibles avec l’Observateur réseau vous aider à comprendre, de diagnostiquer et de mieux réseau de tooyour insights dans Azure.

> [!NOTE]
> Comme l’Observateur réseau prend actuellement en charge uniquement les CLI 1.0, hello instructions toocreate une nouvelle instance de l’Observateur réseau est fournie pour CLI 1.0.

## <a name="create-a-network-watcher-in-hello-portal"></a>Créer un observateur réseau dans le portail de hello

Accédez trop**plus Services** > **réseau** > **Observateur réseau**. Vous pouvez sélectionner tous les abonnements hello souhaité tooenable Observateur réseau pour. Cette action crée un Network Watcher dans chaque région disponible.

![créer un Network Watcher][1]

Lorsque vous activez Observateur réseau à l’aide de hello Portal, nom hello d’instance de l’Observateur réseau hello aura automatiquement la valeur tooNetworkWatcher_region_name où le nom de région correspond toohello région Azure où l’instance de hello a été activé.  Par exemple, une instance de Network Watcher activée dans la région États-Unis Centre-Ouest sera nommée NetworkWatcher_westcentralus.

En outre, instance de l’Observateur réseau hello est automatiquement ajoutée à un groupe de ressources appelé NetworkWatcherRG.  Il sera créé s’il n’existe pas.

Si vous voulez que le nom de hello toocustomize d’une instance de l’Observateur réseau et d’hello groupe de ressources, il est placé dans, vous pouvez utiliser les méthodes ARMClient, hello API REST ou Powershell décrites ci-dessous.  Dans chaque option, hello groupe de ressources doit exister pour que vous placez hello Observateur réseau dans celui-ci.  

## <a name="create-a-network-watcher-with-powershell"></a>Créer un Network Watcher avec PowerShell

toocreate une instance de l’Observateur réseau, exécutez hello l’exemple suivant :

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-hello-rest-api"></a>Créer un observateur réseau avec l’API REST de hello

ARMclient est utilisé toocall hello REST API à l’aide de PowerShell. ARMClient est accessible sur le site chocolatey à partir de la page [ARMClient sur Chocolatey](https://chocolatey.org/packages/ARMClient).

### <a name="log-in-with-armclient"></a>Se connecter à ARMClient

```powerShell
armclient login
```

### <a name="create-hello-network-watcher"></a>Créer l’Observateur réseau de hello

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez une instance de l’Observateur réseau, en savoir plus sur les fonctions hello disponibles :

* [Topologie](network-watcher-topology-overview.md)
* [Capture de paquets](network-watcher-packet-capture-overview.md)
* [Vérification des flux IP](network-watcher-ip-flow-verify-overview.md)
* [Tronçon suivant](network-watcher-next-hop-overview.md)
* [Affichage des groupes de sécurité](network-watcher-security-group-view-overview.md)
* [Journalisation des flux de groupe de sécurité réseau](network-watcher-nsg-flow-logging-overview.md)
* [Résolution des problèmes de passerelle de réseau virtuel](network-watcher-troubleshoot-overview.md)

Une fois qu’une instance de l’Observateur réseau a été créée, la capture de package peut être configurée par article hello suivant : [créer une capture de paquets déclenchées alerte](network-watcher-alert-triggered-packet-capture.md)

[1]: ./media/network-watcher-create/figure1.png











