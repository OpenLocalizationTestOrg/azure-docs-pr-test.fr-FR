---
title: "Comment tooconfigure routage (homologation) pour un circuit ExpressRoute : le Gestionnaire de ressources : PowerShell : Azure | Documents Microsoft"
description: "Cet article vous guide tout au long des étapes hello pour la création et l’approvisionnement hello privés, publics et homologation Microsoft d’un circuit ExpressRoute. Cet article vous explique également comment toocheck état de hello, mettre à jour ou supprimer des homologations pour votre circuit."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: eb3ddf5c05a086ac3e22c64417e51381ef465921
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a>Créer et modifier l’homologation d’un circuit ExpressRoute à l’aide de PowerShell

Cet article vous aide à créer et gérer la configuration de routage pour un circuit ExpressRoute dans le modèle de déploiement hello Gestionnaire de ressources à l’aide de PowerShell. Vous pouvez également vérifier l’état de hello, update ou delete et annuler le déploiement homologations pour un circuit ExpressRoute. Si vous souhaitez toouse une autre méthode de toowork avec votre circuit, sélectionnez un article à partir de hello suivant liste :

> [!div class="op_single_selector"]
> * [Portail Azure](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Interface de ligne de commande Azure](howto-routing-cli.md)
> * [Vidéo - Homologation privée](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Vidéo - Homologation publique](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Vidéo - Homologation Microsoft](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (classique)](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a>Conditions préalables à la configuration

* Vous devez hello dernière version de hello applets de commande PowerShell de gestionnaire de ressources Azure. Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview). 
* Assurez-vous que vous avez consulté hello [conditions préalables](expressroute-prerequisites.md) page hello [exigences routage](expressroute-routing.md) page et hello [workflows](expressroute-workflows.md) page avant de commencer la configuration.
* Vous devez disposer d’un circuit ExpressRoute actif. Suivez les instructions de hello trop[créer un circuit ExpressRoute](expressroute-howto-circuit-arm.md) et circuit hello activé par votre fournisseur de connectivité avant de continuer. Hello circuit ExpressRoute doit être dans un état configuré et activé pour vous toobe toorun en mesure des applets de commande hello dans cet article.

Ces instructions s’appliquent uniquement à toocircuits créé avec les fournisseurs de services offrant des services de connectivité de couche 2. Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement un VPN IP, comme MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.

> [!IMPORTANT]
> Nous n’effectuent pas homologations configurées par les fournisseurs de services via le portail de gestion des services hello. Nous travaillons sur la prochaine activation de cette fonctionnalité. Contactez votre fournisseur de services avant de configurer des homologations BGP.
> 
> 

Vous pouvez configurer une, deux ou les trois homologations (privée Azure, publique Azure et Microsoft) pour un circuit ExpressRoute. Vous pouvez configurer les homologations dans l’ordre de votre choix. Toutefois, il se peut que vous devez vous assurer que vous terminez configuration hello de chacun d’eux à la fois d’homologation. 

## <a name="azure-private-peering"></a>Homologation privée Azure

Cette section vous permet de créer, obtenir, mettre à jour et supprimer hello Azure configuration d’homologation privée pour un circuit ExpressRoute.

### <a name="toocreate-azure-private-peering"></a>toocreate l’homologation privée Azure

1. Importez le module PowerShell de hello pour ExpressRoute.

  Vous devez installer hello dernière PowerShell installer à partir de [PowerShell Gallery](http://www.powershellgallery.com/) et importer des modules du Gestionnaire de ressources Azure hello dans la session de PowerShell hello dans toostart de commande à l’aide des applets de commande hello ExpressRoute. Vous devez toorun PowerShell en tant qu’administrateur.

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  Importer tous les modules de AzureRM.* hello dans hello connu de plage de version sémantique.

  ```powershell
  Import-AzureRM
  ```

  Vous pouvez également importer un module sélectionnez hello connu de plage de version sémantique.

  ```powershell
  Import-Module AzureRM.Network 
  ```

  Tooyour compte de connexion.

  ```powershell
  Login-AzureRmAccount
  ```

  Sélectionnez l’abonnement hello circuit ExpressRoute de toocreate.

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Créez un circuit ExpressRoute.

  Suivez hello instructions toocreate un [circuit ExpressRoute](expressroute-howto-circuit-arm.md) et configuré par le fournisseur de connectivité hello.

  Si votre fournisseur de connectivité propose des services de couche 3 gérés, vous pouvez demander votre tooenable de fournisseur de connectivité Azure privé d’homologation pour vous. Dans ce cas, vous n’aurez toofollow les instructions figurant dans les sections suivantes hello. Toutefois, si votre fournisseur de connectivité ne gère pas le routage, après avoir créé votre circuit, continuer votre configuration à l’aide des étapes hello.
3. Vérifiez hello ExpressRoute circuit toomake qu’il est configuré et activé également. Utilisez hello l’exemple suivant :

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  réponse de Hello est similaire toohello l’exemple suivant :

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Configurer une homologation privée Azure pour le circuit de hello. Assurez-vous que vous disposez des éléments suivants avant de passer aux étapes suivantes de hello de hello :

  * / 30 sous-réseau pour le lien principal de hello. sous-réseau de Hello ne doit pas faire partie d’un espace d’adressage réservé pour les réseaux virtuels.
  * / 30 sous-réseau pour le lien secondaire de hello. sous-réseau de Hello ne doit pas faire partie d’un espace d’adressage réservé pour les réseaux virtuels.
  * Un tooestablish ID de VLAN valide cette homologation sur. Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.
  * Un numéro AS pour l'homologation. Vous pouvez utiliser des numéros à 2 et 4 octets. Vous pouvez utiliser un numéro AS privé pour cette homologation. Veillez à ne pas utiliser le numéro 65515.
  * **Facultatif :** un hachage MD5 si vous choisissez toouse une.

  Utilisez hello suivant exemple tooconfigure Azure privé d’homologation pour votre circuit :

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  Si vous choisissez toouse un hachage MD5, utilisez hello l’exemple suivant :

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Veillez à spécifier votre numéro AS comme ASN d’homologation et non pas comme ASN client.
  > 
  >

### <a name="tooview-azure-private-peering-details"></a>tooview Azure privé d’homologation détails

Vous pouvez obtenir les détails de configuration à l’aide de hello l’exemple suivant :

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate configuration d’homologation privée Azure

Vous pouvez mettre à jour une partie de la configuration de hello à l’aide de hello l’exemple suivant. Dans cet exemple, hello ID de VLAN de circuit de hello est mise à jour à partir de 100 too500.

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-private-peering"></a>toodelete l’homologation privée Azure

Vous pouvez supprimer votre configuration d’homologation en exécutant hello l’exemple suivant :

> [!WARNING]
> Vous devez vous assurer que tous les réseaux virtuels sont dissocier hello circuit ExpressRoute avant d’exécuter cet exemple. 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a>Homologation publique Azure

Cette section vous permet de créer, obtenir, mettre à jour et supprimer hello configuration d’homologation publique Azure pour un circuit ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate l’homologation publique Azure

1. Importez le module PowerShell de hello pour ExpressRoute.

  Vous devez installer hello dernière PowerShell installer à partir de [PowerShell Gallery](http://www.powershellgallery.com/) et importer des modules du Gestionnaire de ressources Azure hello dans la session de PowerShell hello dans toostart de commande à l’aide des applets de commande hello ExpressRoute. Vous devez toorun PowerShell en tant qu’administrateur.

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  Importer tous les modules de AzureRM.* hello dans hello connu de plage de version sémantique.

  ```powershell
  Import-AzureRM
  ```

  Vous pouvez également importer un module sélectionnez hello connu de plage de version sémantique.

  ```powershell
  Import-Module AzureRM.Network
```

  Tooyour compte de connexion.

  ```powershell
  Login-AzureRmAccount
  ```

  Sélectionnez l’abonnement hello circuit ExpressRoute de toocreate.

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Créez un circuit ExpressRoute.

  Suivez hello instructions toocreate un [circuit ExpressRoute](expressroute-howto-circuit-arm.md) et configuré par le fournisseur de connectivité hello.

  Si votre fournisseur de connectivité propose des services de couche 3 gérés, vous pouvez demander votre tooenable de fournisseur de connectivité Azure privé d’homologation pour vous. Dans ce cas, vous n’aurez toofollow les instructions figurant dans les sections suivantes hello. Toutefois, si votre fournisseur de connectivité ne gère pas le routage, après avoir créé votre circuit, continuer votre configuration à l’aide des étapes hello.
3. Vérifiez tooensure de circuit ExpressRoute hello il est configuré et activé également. Utilisez hello l’exemple suivant :

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  réponse de Hello est similaire toohello l’exemple suivant :

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                      "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Configurer l’homologation publique Azure pour le circuit de hello. Assurez-vous que vous disposez des informations suivantes avant de continuer davantage de hello.

  * / 30 sous-réseau pour le lien principal de hello. Ce doit être un préfixe IPv4 public valide.
  * / 30 sous-réseau pour le lien secondaire de hello. Ce doit être un préfixe IPv4 public valide.
  * Un tooestablish ID de VLAN valide cette homologation sur. Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.
  * Un numéro AS pour l'homologation. Vous pouvez utiliser des numéros à 2 et 4 octets.
  * **Facultatif :** un hachage MD5 si vous choisissez toouse une.

  Exécutez hello suivant exemple tooconfigure Azure public d’homologation pour votre circuit

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  Si vous choisissez toouse un hachage MD5, utilisez hello l’exemple suivant :

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > Veillez à spécifier votre numéro AS comme ASN d’homologation et non pas comme ASN client.
  > 
  >

### <a name="tooview-azure-public-peering-details"></a>tooview Azure public d’homologation détails

Vous pouvez obtenir les détails de configuration à l’aide de hello suivant l’applet de commande :

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate configuration d’homologation publique Azure

Vous pouvez mettre à jour une partie de la configuration de hello à l’aide de hello l’exemple suivant. Dans cet exemple, hello ID de VLAN de circuit de hello est mise à jour à partir de too600 200.

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-public-peering"></a>toodelete l’homologation publique Azure

Vous pouvez supprimer votre configuration d’homologation en exécutant hello l’exemple suivant :

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a>Homologation Microsoft

Cette section vous permet de créer, obtenir, mettre à jour et supprimer la configuration d’homologation Microsoft hello pour un circuit ExpressRoute.

> [!IMPORTANT]
> Homologation Microsoft des circuits ExpressRoute qui ont été configurés préalable tooAugust 1, 2017 aura tous les préfixes de service publiés par le biais d’homologation de Microsoft hello, même si les filtres de routage ne sont pas définis. Homologation Microsoft des circuits ExpressRoute qui sont configurés sur ou après le 1er août 2017 n’aura pas de préfixes publiés jusqu'à ce qu’un filtre de routage est attaché toohello circuit. Pour plus d’informations, consultez [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md) (Configurer un filtre d’itinéraire pour l’homologation Microsoft).
> 
> 

### <a name="toocreate-microsoft-peering"></a>l’homologation de Microsoft toocreate

1. Importez le module PowerShell de hello pour ExpressRoute.

  Vous devez installer hello dernière PowerShell installer à partir de [PowerShell Gallery](http://www.powershellgallery.com/) et importer des modules du Gestionnaire de ressources Azure hello dans la session de PowerShell hello dans toostart de commande à l’aide des applets de commande hello ExpressRoute. Vous devez toorun PowerShell en tant qu’administrateur.

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  Importer tous les modules de AzureRM.* hello dans hello connu de plage de version sémantique.

  ```powershell
  Import-AzureRM
  ```

  Vous pouvez également importer un module sélectionnez hello connu de plage de version sémantique.

  ```powershell
  Import-Module AzureRM.Network
  ```

  Tooyour compte de connexion.

  ```powershell
  Login-AzureRmAccount
  ```

  Sélectionnez l’abonnement hello circuit ExpressRoute de toocreate.

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. Créez un circuit ExpressRoute.

  Suivez hello instructions toocreate un [circuit ExpressRoute](expressroute-howto-circuit-arm.md) et configuré par le fournisseur de connectivité hello.

  Si votre fournisseur de connectivité propose des services de couche 3 gérés, vous pouvez demander votre tooenable de fournisseur de connectivité Azure privé d’homologation pour vous. Dans ce cas, vous n’aurez toofollow les instructions figurant dans les sections suivantes hello. Toutefois, si votre fournisseur de connectivité ne gère pas le routage, après avoir créé votre circuit, continuer votre configuration à l’aide des étapes hello.
3. Vérifiez hello ExpressRoute circuit toomake qu’il est configuré et activé également. Utilisez hello l’exemple suivant :

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  réponse de Hello est similaire toohello l’exemple suivant :

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. Configurez Microsoft d’homologation pour le circuit de hello. Assurez-vous que vous avez hello suivant informations avant de continuer.

  * / 30 sous-réseau pour le lien principal de hello. Il doit s’agir d’un préfixe IPv4 public valide vous appartenant et enregistré dans un registre RIR / IRR.
  * / 30 sous-réseau pour le lien secondaire de hello. Il doit s’agir d’un préfixe IPv4 public valide vous appartenant et enregistré dans un registre RIR / IRR.
  * Un tooestablish ID de VLAN valide cette homologation sur. Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.
  * Un numéro AS pour l'homologation. Vous pouvez utiliser des numéros à 2 et 4 octets.
  * Publié préfixes : vous devez fournir une liste de tous les préfixes que vous prévoyez tooadvertise sur la session BGP de hello. Seuls les préfixes d'adresses IP publiques sont acceptés. Si vous envisagez un jeu de préfixes de toosend, vous pouvez envoyer une liste séparée par des virgules. Ces préfixes doivent être inscrit tooyou dans un RIR / IRR.
  * **Facultatif :** client ASN : Si vous ne les préfixes de publicité qui ne sont pas inscrit toohello d’homologation en tant que nombre, vous pouvez spécifier hello en tant que nombre toowhich ils sont inscrits.
  * Nom de Registre de routage : Vous pouvez spécifier hello RIR / IRR contre le hello comme nombre et les préfixes sont inscrits.
  * **Facultatif :** un hachage MD5 si vous choisissez toouse une.

   Utilisez hello suivant exemple tooconfigure Microsoft homologation pour votre circuit :

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="tooget-microsoft-peering-details"></a>informations d’homologation de tooget Microsoft

Vous pouvez obtenir les détails de configuration à l’aide de hello l’exemple suivant :

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-microsoft-peering-configuration"></a>configuration d’homologation de tooupdate Microsoft

Vous pouvez mettre à jour une partie de la configuration de hello à l’aide de hello l’exemple suivant :

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-microsoft-peering"></a>l’homologation de Microsoft toodelete

Vous pouvez supprimer votre configuration d’homologation par hello suivant l’applet de commande en cours d’exécution :

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a>Étapes suivantes

Étape suivante, [lier un circuit ExpressRoute de tooan réseau virtuel](expressroute-howto-linkvnet-arm.md).

* Pour plus d'informations sur les workflows ExpressRoute, consultez [Workflows ExpressRoute](expressroute-workflows.md).
* Pour plus d’informations sur l’homologation du circuit, consultez [Circuits ExpressRoute et domaines de routage](expressroute-circuit-peerings.md).
* Pour plus d’informations sur l’utilisation des réseaux virtuels, consultez la page [Présentation du réseau virtuel](../virtual-network/virtual-networks-overview.md).
