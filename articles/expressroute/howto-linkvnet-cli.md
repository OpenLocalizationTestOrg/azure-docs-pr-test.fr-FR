---
title: "Lier un circuit ExpressRoute de tooan réseau virtuel : CLI : Azure | Documents Microsoft"
description: "Ce document fournit une vue d’ensemble de la façon dont toolink virtuel réseaux des circuits tooExpressRoute (réseaux virtuels) en utilisant le modèle de déploiement du Gestionnaire de ressources hello et CLI."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlit
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 1251f016d9b94d3fee81de1df164cb085cbe9d78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-cli"></a>Se connecter à un circuit ExpressRoute de tooan de réseau virtuel à l’aide de CLI

Cet article vous permet de lier des circuits ExpressRoute de réseaux virtuels (réseaux virtuels) tooAzure à l’aide de CLI. toolink à l’aide de CLI d’Azure, les réseaux virtuels hello doivent être créés à l’aide du modèle de déploiement du Gestionnaire de ressources hello. Ils peuvent être dans hello même abonnement, ou une partie d’un autre abonnement. Si vous souhaitez toouse une autre méthode de tooconnect votre circuit ExpressRoute de tooan réseau virtuel, vous pouvez sélectionner un article à partir de hello suivant liste :

> [!div class="op_single_selector"]
> * [Portail Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Interface de ligne de commande Azure](howto-linkvnet-cli.md)
> * [Vidéo - portail Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (classique)](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a>Conditions préalables à la configuration

* Vous devez hello dernière version de hello interface de ligne de commande (CLI). Pour plus d’informations, consultez [Installer Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).
* Vous devez tooreview hello [conditions préalables](expressroute-prerequisites.md), [exigences routage](expressroute-routing.md), et [workflows](expressroute-workflows.md) avant de commencer la configuration.
* Vous devez disposer d’un circuit ExpressRoute actif. 
  * Suivez les instructions de hello trop[créer un circuit ExpressRoute](howto-circuit-cli.md) et avoir des circuits hello activé par votre fournisseur de connectivité. 
  * Vérifiez que l’homologation privée Azure est configurée pour votre circuit. Consultez hello [configurer le routage](howto-routing-cli.md) article pour obtenir des instructions de routage. 
  * Assurez-vous que l’homologation privée Azure est configurée. l’homologation BGP Hello entre votre réseau et de Microsoft doit être des afin que vous pouvez activer la connectivité de bout en bout.
  * Vérifiez qu’un réseau virtuel et une passerelle de réseau virtuel ont été créés et entièrement approvisionnés. Suivez les instructions de hello trop[configurer une passerelle de réseau virtuel pour ExpressRoute](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli). Être toouse vraiment `--gateway-type ExpressRoute`.

* Vous pouvez lier de circuit de ExpressRoute standard too10 réseaux virtuels tooa. Tous les réseaux virtuels doivent être Bonjour même région géopolitique lors de l’utilisation d’un circuit ExpressRoute standard. 

* Si vous activez le module complémentaire de hello ExpressRoute premium, vous pouvez lier un réseau virtuel en dehors de la région de hello géopolitique de hello circuit ExpressRoute, ou vous connecter à un plus grand nombre de réseaux virtuels tooyour circuit ExpressRoute. Pour plus d’informations sur le module complémentaire de hello premium, consultez hello [FAQ](expressroute-faqs.md).

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Connecter un réseau virtuel Bonjour même circuit de tooa d’abonnement

Vous pouvez vous connecter à un circuit ExpressRoute de réseau virtuel passerelle tooan à l’aide de hello exemple. Assurez-vous que cette passerelle de réseau virtuel hello est créée et est prête pour la liaison avant d’exécuter les commandes hello.

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Connecter un réseau virtuel dans un circuit de tooa autre abonnement

Vous pouvez partager un circuit ExpressRoute entre plusieurs abonnements. la figure ci-dessous Hello schématique simple de fonctionnement du partage de circuits ExpressRoute entre plusieurs abonnements.

Chaque hello petits clouds dans cloud volumineux de hello est utilisé toorepresent abonnements appartenant aux départements toodifferent au sein d’une organisation. Chacun des services hello au sein de l’organisation de hello permettre utiliser leur propre abonnement pour le déploiement de leurs services, mais ils peuvent partager un réseau local ExpressRoute circuit tooconnect tooyour précédent. Un seul département (dans cet exemple : informatique) peut posséder de circuit ExpressRoute de hello. Autres abonnements au sein de l’organisation de hello peuvent utiliser le circuit ExpressRoute de hello.

> [!NOTE]
> Frais de connectivité et de bande passante pour le circuit de hello dédié sera appliqué toohello propriétaire du Circuit ExpressRoute. Tous les réseaux virtuels partagent hello même bande passante.
> 
> 

![Connectivité entre abonnements](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a>Administration : propriétaires de circuit et utilisateurs du circuit

Hello propriétaire du Circuit est un utilisateur autorisé de la puissance de hello ressource de circuit ExpressRoute. Hello propriétaire du Circuit peut créer des autorisations qui peuvent être utilisées par les utilisateurs de Circuit. Les utilisateurs de circuit sont les propriétaires du réseau virtuel qui ne sont pas dans les passerelles hello même abonnement que hello circuit ExpressRoute. Les utilisateurs du circuit peuvent utiliser des autorisations (une seule autorisation par réseau virtuel).

Hello propriétaire du Circuit a les autorisations hello power toomodify et révoquer à tout moment. Lorsqu’une autorisation est révoquée, toutes les connexions de lien sont supprimées de l’abonnement hello dont l’accès a été révoqué.

### <a name="circuit-owner-operations"></a>Opérations du propriétaire du circuit

**toocreate une autorisation**

Hello propriétaire du Circuit crée une autorisation, ce qui crée une clé d’autorisation qui peut être utilisé par un utilisateur du Circuit de tooconnect leur toohello de passerelles de réseau virtuel circuit ExpressRoute. Une autorisation n’est valide que pour une seule connexion.

Hello suivant montre l’exemple de comment toocreate une autorisation :

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

réponse de Hello contient l’état et la clé d’autorisation de hello :

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

**autorisations tooreview**

Hello propriétaire du Circuit peut consulter toutes les autorisations qui sont émises sur un circuit en particulier en exécutant hello l’exemple suivant :

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

**autorisations tooadd**

Hello propriétaire du Circuit peut ajouter des autorisations à l’aide de hello l’exemple suivant :

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

**autorisations toodelete**

Hello propriétaire du Circuit peut révoquer/supprimer un autorisations toohello utilisateur en exécutant hello l’exemple suivant :

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a>Opérations de l’utilisateur du circuit

Hello Circuit utilisateur a besoin d’ID de l’homologue hello et une clé d’autorisation à partir de hello propriétaire du Circuit. clé d’autorisation de Hello est un GUID.

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

**tooredeem une autorisation de connexion**

Hello utilisateur du Circuit peut exécuter hello suivant exemple tooredeem une autorisation de lien :

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

**toorelease une autorisation de connexion**

Vous pouvez libérer une autorisation en supprimant la connexion hello qui établit un lien réseau virtuel du toohello circuit ExpressRoute hello.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur ExpressRoute, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md).
