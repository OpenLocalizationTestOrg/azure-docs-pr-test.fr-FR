---
title: "Lier un circuit ExpressRoute de tooan réseau virtuel : PowerShell : Azure | Documents Microsoft"
description: "Ce document fournit une vue d’ensemble du mode toolink virtuel réseaux (réseaux virtuels) tooExpressRoute circuits à l’aide de PowerShell et le modèle de déploiement du Gestionnaire de ressources hello."
services: expressroute
documentationcenter: na
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: daacb6e5-705a-456f-9a03-c4fc3f8c1f7e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: ganesr
ms.openlocfilehash: e75a9f6b42fa8e1a579e4f19882ec99b277b545f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a>Se connecter à un circuit ExpressRoute de tooan réseau virtuel
> [!div class="op_single_selector"]
> * [Portail Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Interface de ligne de commande Azure](howto-linkvnet-cli.md)
> * [Vidéo - portail Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (classique)](expressroute-howto-linkvnet-classic.md)
>

Cet article vous permet de lier des circuits ExpressRoute de tooAzure des réseaux virtuels (réseaux virtuels) à l’aide de PowerShell et le modèle de déploiement du Gestionnaire de ressources hello. Réseaux virtuels peuvent être dans hello même abonnement ou une partie d’un autre abonnement. Cet article vous montre également comment lier des tooupdate un réseau virtuel. 

## <a name="before-you-begin"></a>Avant de commencer
* Installez la version la plus récente des modules d’Azure PowerShell hello hello. Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).
* Hello de révision [conditions préalables](expressroute-prerequisites.md), [exigences routage](expressroute-routing.md), et [workflows](expressroute-workflows.md) avant de commencer la configuration.
* Vous devez disposer d’un circuit ExpressRoute actif. 
  * Suivez les instructions de hello trop[créer un circuit ExpressRoute](expressroute-howto-circuit-arm.md) et avoir des circuits hello activé par votre fournisseur de connectivité. 
  * Vérifiez que l’homologation privée Azure est configurée pour votre circuit. Consultez hello [configurer le routage](expressroute-howto-routing-arm.md) article pour obtenir des instructions de routage. 
  * Assurez-vous que l’homologation privée Azure est configuré et est l’homologation BGP hello entre votre réseau et de Microsoft afin que vous pouvez activer la connectivité de bout en bout.
  * Vérifiez qu’un réseau virtuel et une passerelle de réseau virtuel ont été créés et entièrement approvisionnés. Suivez les instructions de hello trop[créer une passerelle de réseau virtuel pour ExpressRoute](expressroute-howto-add-gateway-resource-manager.md). Une passerelle de réseau virtuel pour ExpressRoute utilise hello « ExpressRoute », le type de passerelle VPN pas.

* Vous pouvez lier de circuit de ExpressRoute standard too10 réseaux virtuels tooa. Tous les réseaux virtuels doivent être Bonjour même région géopolitique lors de l’utilisation d’un circuit ExpressRoute standard. 

* Vous pouvez lier un réseau virtuel en dehors de la région de hello géopolitique de hello circuit ExpressRoute ou vous connecter à un plus grand nombre de réseaux virtuels tooyour circuit ExpressRoute si vous avez activé le module complémentaire de hello ExpressRoute premium. Vérifiez hello [FAQ](expressroute-faqs.md) pour plus d’informations sur le module complémentaire de hello premium.


## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Connecter un réseau virtuel Bonjour même circuit de tooa d’abonnement
Vous pouvez vous connecter à un tooan de passerelle de réseau virtuel circuit ExpressRoute à l’aide de hello suivant l’applet de commande. Assurez-vous que cette passerelle de réseau virtuel hello est créée et est prête pour la liaison avant d’exécuter les applets de commande hello :

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Connecter un réseau virtuel dans un circuit de tooa autre abonnement
Vous pouvez partager un circuit ExpressRoute entre plusieurs abonnements. Hello figure suivante montre une simple principe de fonctionnement du partage de circuits ExpressRoute entre plusieurs abonnements.

Chaque hello petits clouds dans cloud volumineux de hello est utilisé toorepresent abonnements appartenant aux départements toodifferent au sein d’une organisation. Chacun des services hello au sein de l’organisation de hello permettre utiliser leur propre abonnement pour le déploiement de leurs services, mais ils peuvent partager un réseau local ExpressRoute circuit tooconnect tooyour précédent. Un seul département (dans cet exemple : informatique) peut posséder de circuit ExpressRoute de hello. Autres abonnements au sein de l’organisation de hello peuvent utiliser le circuit ExpressRoute de hello.

> [!NOTE]
> Frais de connectivité et de bande passante pour le circuit ExpressRoute de hello sera appliqué toohello propriétaire de l’abonnement. Tous les réseaux virtuels partagent hello même bande passante.
> 
> 

![Connectivité entre abonnements](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a>Administration - propriétaires de circuit et utilisateurs de circuit

Hello propriétaire du circuit est un utilisateur autorisé de la puissance de hello ressource de circuit ExpressRoute. propriétaire du circuit Hello peut créer des autorisations qui peuvent être utilisées par les utilisateurs de circuit. Les utilisateurs de circuit sont les propriétaires du réseau virtuel qui ne sont pas dans les passerelles hello même abonnement que hello circuit ExpressRoute. Les utilisateurs du circuit peuvent échanger des autorisations (une seule autorisation par réseau virtuel).

propriétaire du circuit Hello possède les autorisations hello power toomodify et révoquer à tout moment. Révocation de des résultats d’autorisation dans toutes les connexions de la liaison en cours de suppression de l’abonnement hello dont l’accès a été révoqué.

### <a name="circuit-owner-operations"></a>Opérations du propriétaire du circuit

**toocreate une autorisation**

propriétaire du circuit Hello crée une autorisation. Cela entraîne la création de hello d’une clé d’autorisation qui peut être utilisé par un tooconnect utilisateur de circuit leur toohello de passerelles de réseau virtuel circuit ExpressRoute. Une autorisation n’est valide que pour une seule connexion.

Hello suivant applet de commande extrait de code montre comment une autorisation de toocreate :

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


Hello réponse toothis contiendra l’état et la clé d’autorisation de hello :

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



**autorisations tooreview**

propriétaire du circuit Hello peut consulter toutes les autorisations qui sont émises sur un circuit en particulier en exécutant hello suivant l’applet de commande :

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

**autorisations tooadd**

propriétaire du circuit Hello peut ajouter des autorisations à l’aide de hello suivant l’applet de commande :

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

**autorisations toodelete**

propriétaire du circuit Hello permettre révoquer/supprimer un autorisations toohello utilisateur en exécutant hello suivant l’applet de commande :

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a>Opérations de l’utilisateur du circuit

utilisateur du circuit Hello doit hello homologue ID et une clé d’autorisation du propriétaire du circuit hello. clé d’autorisation de Hello est un GUID.

ID de l’homologue peut être vérifiée à partir de hello de commande suivante :

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

**tooredeem une autorisation de connexion**

utilisateur du circuit Hello peut exécuter hello suivant l’applet de commande tooredeem une autorisation de lien :

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

**toorelease une autorisation de connexion**

Vous pouvez libérer une autorisation en supprimant la connexion hello qui établit un lien réseau virtuel du toohello circuit ExpressRoute hello.

## <a name="modify-a-virtual-network-connection"></a>Modifier une connexion de réseau virtuel
Vous pouvez mettre à jour certaines propriétés d’une connexion de réseau virtuel. 

**poids de connexion hello tooupdate**

Votre réseau virtuel peut être connecté toomultiple des circuits ExpressRoute. Vous pouvez recevoir le même préfixe de hello à partir de plusieurs circuits ExpressRoute. toochoose le trafic toosend connexion destinés à ce préfixe, vous pouvez modifier *RoutingWeight* d’une connexion. Le trafic sera envoyé sur connexion hello avec hello plus élevé *RoutingWeight*.

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

Hello plage de *RoutingWeight* est too32000 0. Hello par défaut est 0.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur ExpressRoute, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md).
