---
title: "aaaFind de tronçon suivant avec Azure réseau observateur du prochain saut - PowerShell | Documents Microsoft"
description: "Cet article décrit comment vous pouvez trouver le hello de type de tronçon suivant est et à l’aide des adresses ip de tronçon suivant à l’aide de PowerShell."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 6a656c55-17bd-40f1-905d-90659087639c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fdb0b4a02d95fc45c103fe952fc1afa095414c18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-powershell"></a>Savoir quel type de tronçon suivant hello est à l’aide de capacité de tronçon suivant hello dans l’Observateur réseau de Azure à l’aide de PowerShell

> [!div class="op_single_selector"]
> - [Portail Azure](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [API REST Azure](network-watcher-check-next-hop-rest.md)

Tronçon suivant est une fonctionnalité de l’Observateur réseau qui offre la possibilité de hello obtenir le type de tronçon suivant hello et l’adresse IP basée sur une machine virtuelle spécifiée. Cette fonctionnalité est utile pour déterminer si le trafic en laissant une machine virtuelle traverse une passerelle, internet ou des réseaux virtuels tooget tooits destination.

## <a name="before-you-begin"></a>Avant de commencer

Dans ce scénario, vous allez utiliser hello type de tronçon suivant toofind portail Azure hello et l’adresse IP.

Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau. scénario de Hello suppose également qu’un groupe de ressources avec un ordinateur virtuel valide existe toobe utilisé.

## <a name="scenario"></a>Scénario

scénario de Hello abordée dans cet article utilise le saut suivant, une fonctionnalité de l’Observateur réseau qui recherche le type de tronçon suivant hello et une adresse IP pour une ressource. toolearn en savoir plus sur le tronçon suivant, visitez [vue d’ensemble du tronçon suivant](network-watcher-next-hop-overview.md).

## <a name="retrieve-network-watcher"></a>Récupérer Network Watcher

première étape de Hello est instance de l’Observateur réseau tooretrieve hello. Hello `$networkWatcher` variable est passée de tronçon suivant de toohello vérifier l’applet de commande.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a>Obtenir une machine virtuelle

Tronçon suivant retourne le saut suivant de hello et l’adresse IP hello saut suivant de hello à partir d’un ordinateur virtuel. Un Id d’un ordinateur virtuel est requis pour l’applet de commande hello. Si vous connaissez déjà les ID hello de hello machine virtuelle toouse, vous pouvez ignorer cette étape.

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> Tronçon suivant requiert que les ressources d’ordinateur virtuel hello est allouée toorun.

## <a name="get-hello-network-interfaces"></a>Obtenir les interfaces réseau de hello

adresse IP de Hello d’une carte réseau sur l’ordinateur virtuel de hello est nécessaire, dans cet exemple, nous récupérons hello cartes d’interface réseau sur un ordinateur virtuel. Si vous connaissez déjà hello IP d’adresses que vous souhaitez tootest sur l’ordinateur virtuel de hello, vous pouvez ignorer cette étape.

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a>Obtenir le tronçon suivant

Maintenant que nous appelons hello `Get-AzureRmNetworkWatcherNextHop` applet de commande. Nous allons passer hello d’applet de commande hello Observateur réseau, l’ordinateur virtuel Id, adresse IP source et adresse IP de destination. Dans cet exemple, adresse IP de destination hello est tooa machine virtuelle dans un autre réseau virtuel. Il existe une passerelle de réseau virtuel entre des réseaux virtuels deux hello.

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a>Passer en revue les résultats

Lorsque vous avez terminé, les résultats de hello sont fournies. adresse IP du tronçon suivant Hello est retournée, ainsi que de type hello de ressource, qu'il s’agit. Dans ce scénario, il est hello adresse IP publique de passerelle de réseau virtuel hello.

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

Hello liste suivante présente les valeurs de tronçon suivant actuellement disponibles hello :

**Type de tronçon suivant**

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* Aucun

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment tooreview vos paramètres de groupe de sécurité réseau par programme en vous rendant sur [NSG audit avec l’Observateur réseau](network-watcher-nsg-auditing-powershell.md)

















