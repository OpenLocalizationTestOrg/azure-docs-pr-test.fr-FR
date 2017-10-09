---
title: "Comment tooconfigure routage (homologation) pour un circuit ExpressRoute : Azure : classique | Documents Microsoft"
description: "Cet article vous guide tout au long des étapes hello pour la création et l’approvisionnement hello privés, publics et homologation Microsoft d’un circuit ExpressRoute. Cet article vous explique également comment toocheck état de hello, mettre à jour ou supprimer des homologations pour votre circuit."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a>Créer et modifier l’homologation pour un circuit ExpressRoute (Classic)
> [!div class="op_single_selector"]
> * [Portail Azure](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Interface de ligne de commande Azure](howto-routing-cli.md)
> * [Vidéo - Homologation privée](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Vidéo - Homologation publique](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Vidéo - Homologation Microsoft](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (classique)](expressroute-howto-routing-classic.md)
> 

Cet article vous guide tout au long de hello étapes toocreate et gérer la configuration de routage pour un circuit ExpressRoute à l’aide du modèle de déploiement classique de PowerShell et hello. Hello étapes ci-dessous vous également montrent comment toocheck état de hello, mettre à jour, ou supprimez et annuler le déploiement homologations pour un circuit ExpressRoute.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**À propos des modèles de déploiement Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a>Conditions préalables à la configuration
* Vous devez hello dernière version de hello applets de commande PowerShell de gestion de Service Azure (SM). Pour en savoir plus, voir [Prise en main des applets de commande PowerShell](/powershell/azure/overview).  
* Assurez-vous que vous avez consulté hello [conditions préalables](expressroute-prerequisites.md) page hello [exigences routage](expressroute-routing.md) page et hello [workflows](expressroute-workflows.md) page avant de commencer la configuration.
* Vous devez disposer d’un circuit ExpressRoute actif. Suivez les instructions de hello trop[créer un circuit ExpressRoute](expressroute-howto-circuit-classic.md) et circuit hello activé par votre fournisseur de connectivité avant de continuer. Hello circuit ExpressRoute doit être dans un état configuré et activé pour vous toobe toorun en mesure de hello applets de commande décrites ci-dessous.

> [!IMPORTANT]
> Ces instructions s’appliquent uniquement à toocircuits créé avec les fournisseurs de services offrant des services de connectivité de couche 2. Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement IPVPN, à l’image de MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.
> 
> 

Vous pouvez configurer une, deux ou les trois homologations (privée Azure, publique Azure et Microsoft) pour un circuit ExpressRoute. Vous pouvez configurer les homologations dans l’ordre de votre choix. Toutefois, il se peut que vous devez vous assurer que vous terminez configuration hello de chacun d’eux à la fois d’homologation.


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a>Connectez-vous à tooyour compte Azure, puis sélectionnez un abonnement
1. Ouvrez la console PowerShell avec des droits élevés et tooyour compte de connexion. Utilisez hello suivant toohelp exemple que vous connectez :

        Login-AzureRmAccount

2. Vérifiez les abonnements hello pour le compte de hello.

        Get-AzureRmSubscription

3. Si vous avez plusieurs abonnements, sélectionnez l’abonnement hello que vous souhaitez toouse.

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. Ensuite, utilisez hello suivant l’applet de commande tooadd tooPowerShell de votre abonnement Azure pour le modèle de déploiement classique hello.

        Add-AzureAccount


## <a name="azure-private-peering"></a>Homologation privée Azure
Cette section fournit des instructions sur la façon dont toocreate, obtenir, mettre à jour et supprimer des hello Azure configuration d’homologation privée pour un circuit ExpressRoute. 

### <a name="toocreate-azure-private-peering"></a>toocreate l’homologation privée Azure
1. **Importez le module PowerShell de hello pour ExpressRoute.**
   
    Vous devez importer les modules Azure et ExpressRoute hello dans la session de PowerShell hello dans toostart de commande à l’aide des applets de commande hello ExpressRoute. Les commandes de suivantes de hello exécution tooimport hello Azure et ExpressRoute les modules dans la session de PowerShell hello.  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Créez un circuit ExpressRoute.**
   
    Suivez hello instructions toocreate un [circuit ExpressRoute](expressroute-howto-circuit-classic.md) et configuré par le fournisseur de connectivité hello. Si votre fournisseur de connectivité propose des services de couche 3 gérés, vous pouvez demander votre tooenable de fournisseur de connectivité Azure privé d’homologation pour vous. Dans ce cas, vous n’aurez toofollow les instructions figurant dans les sections suivantes hello. Toutefois, si votre fournisseur de connectivité ne gère pas le routage, après avoir créé votre circuit, suivez les instructions hello ci-dessous. 
3. **Vérifiez tooensure de circuit ExpressRoute hello que s’il est configuré.**
   
    Vous devez tout d’abord vérifier toosee si hello circuit ExpressRoute est configuré et également activé. Consultez l’exemple hello ci-dessous.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Assurez-vous que le circuit de hello montre comme configuré et activé. Si ce n’est pas le cas, fonctionne avec votre tooget de fournisseur de connectivité votre état toohello requis de circuit et l’état.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Configurer une homologation privée Azure pour le circuit de hello.**
   
    Assurez-vous que vous disposez des éléments suivants avant de passer aux étapes suivantes de hello de hello :
   
   * / 30 sous-réseau pour le lien principal de hello. Ce sous-réseau ne doit faire partie d’aucun espace d'adressage réservé aux réseaux virtuels.
   * / 30 sous-réseau pour le lien secondaire de hello. Ce sous-réseau ne doit faire partie d’aucun espace d'adressage réservé aux réseaux virtuels.
   * Un tooestablish ID de VLAN valide cette homologation sur. Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.
   * Un numéro AS pour l'homologation. Vous pouvez utiliser des numéros à 2 et 4 octets. Vous pouvez utiliser un numéro AS privé pour cette homologation. Veillez à ne pas utiliser le numéro 65515.
   * Un hachage MD5 si vous choisissez toouse une. **Cette étape est facultative**.
     
    Vous pouvez exécuter hello suivant tooconfigure applet de commande d’homologation privée Azure pour votre circuit.
     
        New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100
     
    Vous pouvez utiliser la cmdlet hello ci-dessous si vous choisissez toouse un hachage MD5.
     
        New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"
     
     > [!IMPORTANT]
     > Veillez à spécifier votre numéro AS comme ASN d’homologation et non pas comme ASN client.
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a>tooview Azure privé d’homologation détails
Vous pouvez obtenir les détails de configuration à l’aide de hello suivant l’applet de commande

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate configuration d’homologation privée Azure
Vous pouvez mettre à jour une partie de la configuration de hello à l’aide de hello suivant l’applet de commande. Dans l’exemple hello ci-dessous, hello ID de VLAN de circuit de hello est mise à jour à partir de 100 too500.

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a>toodelete l’homologation privée Azure
Vous pouvez supprimer la configuration d’homologation par hello suivant l’applet de commande en cours d’exécution.

> [!WARNING]
> Vous devez vous assurer que tous les réseaux virtuels sont dissocier hello circuit ExpressRoute avant d’exécuter cette applet de commande. 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a>Homologation publique Azure
Cette section fournit des instructions sur la façon dont toocreate, obtenir, mettre à jour et supprimer des hello configuration d’homologation publique Azure pour un circuit ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate l’homologation publique Azure
1. **Importez le module PowerShell de hello pour ExpressRoute.**
   
    Vous devez importer les modules Azure et ExpressRoute hello dans la session de PowerShell hello dans toostart de commande à l’aide des applets de commande hello ExpressRoute. Les commandes de suivantes de hello exécution tooimport hello Azure et ExpressRoute les modules dans la session de PowerShell hello. 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Création d’un circuit ExpressRoute**
   
    Suivez hello instructions toocreate un [circuit ExpressRoute](expressroute-howto-circuit-classic.md) et configuré par le fournisseur de connectivité hello. Si votre fournisseur de connectivité propose des services de couche 3 gérés, vous pouvez demander votre tooenable de fournisseur de connectivité Azure public d’homologation pour vous. Dans ce cas, vous n’aurez toofollow les instructions figurant dans les sections suivantes hello. Toutefois, si votre fournisseur de connectivité ne gère pas le routage, après avoir créé votre circuit, suivez les instructions hello ci-dessous.
3. **Vérifiez tooensure de circuit ExpressRoute que s’il est configuré**
   
    Vous devez tout d’abord vérifier toosee si hello circuit ExpressRoute est configuré et également activé. Consultez l’exemple hello ci-dessous.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Assurez-vous que le circuit de hello montre comme configuré et activé. Si ce n’est pas le cas, fonctionne avec votre tooget de fournisseur de connectivité votre état toohello requis de circuit et l’état.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Configurer l’homologation publique Azure pour le circuit de hello**
   
    Assurez-vous que vous disposez des informations suivantes avant de continuer davantage de hello.
   
   * / 30 sous-réseau pour le lien principal de hello. Ce doit être un préfixe IPv4 public valide.
   * / 30 sous-réseau pour le lien secondaire de hello. Ce doit être un préfixe IPv4 public valide.
   * Un tooestablish ID de VLAN valide cette homologation sur. Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.
   * Un numéro AS pour l'homologation. Vous pouvez utiliser des numéros à 2 et 4 octets.
   * Un hachage MD5 si vous choisissez toouse une. **Cette étape est facultative**.
     
    Vous pouvez exécuter hello suivant tooconfigure applet de commande pour l’homologation publique Azure pour votre circuit
     
        New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200
     
    Vous pouvez utiliser la cmdlet hello ci-dessous si vous choisissez toouse un hachage MD5
     
        New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"
     
     > [!IMPORTANT]
     > Veillez à spécifier votre numéro AS comme ASN d’homologation et non pas comme ASN client.
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a>tooview Azure public d’homologation détails
Vous pouvez obtenir les détails de configuration à l’aide de hello suivant l’applet de commande

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate configuration d’homologation publique Azure
Vous pouvez mettre à jour une partie de la configuration de hello à l’aide de hello suivant l’applet de commande

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

Hello, ID de VLAN de circuit de hello est mise à jour à partir de 200 too600 Bonjour à l’exemple ci-dessus.

### <a name="toodelete-azure-public-peering"></a>toodelete l’homologation publique Azure
Vous pouvez supprimer votre configuration d’homologation par hello suivant l’applet de commande en cours d’exécution

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a>Homologation Microsoft
Cette section fournit des instructions sur la façon dont toocreate, obtenir, mettre à jour et supprimer la configuration d’homologation Microsoft hello pour un circuit ExpressRoute. 

### <a name="toocreate-microsoft-peering"></a>l’homologation de Microsoft toocreate
1. **Importez le module PowerShell de hello pour ExpressRoute.**
   
    Vous devez importer les modules Azure et ExpressRoute hello dans la session de PowerShell hello dans toostart de commande à l’aide des applets de commande hello ExpressRoute. Les commandes de suivantes de hello exécution tooimport hello Azure et ExpressRoute les modules dans la session de PowerShell hello.  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Création d’un circuit ExpressRoute**
   
    Suivez hello instructions toocreate un [circuit ExpressRoute](expressroute-howto-circuit-classic.md) et configuré par le fournisseur de connectivité hello. Si votre fournisseur de connectivité propose des services de couche 3 gérés, vous pouvez demander votre tooenable de fournisseur de connectivité Azure privé d’homologation pour vous. Dans ce cas, vous n’aurez toofollow les instructions figurant dans les sections suivantes hello. Toutefois, si votre fournisseur de connectivité ne gère pas le routage, après avoir créé votre circuit, suivez les instructions hello ci-dessous.
3. **Vérifiez tooensure de circuit ExpressRoute que s’il est configuré**
   
    Vous devez tout d’abord vérifier toosee si hello circuit ExpressRoute est en état préparé et activé.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Assurez-vous que le circuit de hello montre comme configuré et activé. Si ce n’est pas le cas, fonctionne avec votre tooget de fournisseur de connectivité votre état toohello requis de circuit et l’état.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Configuration de Microsoft d’homologation pour le circuit de hello**
   
    Assurez-vous que vous avez hello suivant informations avant de continuer.
   
   * / 30 sous-réseau pour le lien principal de hello. Il doit s’agir d’un préfixe IPv4 public valide vous appartenant et enregistré dans un registre RIR / IRR.
   * / 30 sous-réseau pour le lien secondaire de hello. Il doit s’agir d’un préfixe IPv4 public valide vous appartenant et enregistré dans un registre RIR / IRR.
   * Un tooestablish ID de VLAN valide cette homologation sur. Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.
   * Un numéro AS pour l'homologation. Vous pouvez utiliser des numéros à 2 et 4 octets.
   * Publié préfixes : vous devez fournir une liste de tous les préfixes que vous prévoyez tooadvertise sur la session BGP de hello. Seuls les préfixes d'adresses IP publiques sont acceptés. Vous pouvez envoyer une liste séparée par des virgules si vous envisagez de toosend un jeu de préfixes. Ces préfixes doivent être inscrit tooyou dans un RIR / IRR.
   * Client ASN : Si vous publiez des préfixes qui ne sont pas inscrit toohello d’homologation en tant que nombre, vous pouvez spécifier hello en tant que nombre toowhich qu'ils sont inscrits. **Cette étape est facultative**.
   * Nom de Registre de routage : Vous pouvez spécifier hello RIR / IRR contre le hello comme nombre et les préfixes sont inscrits.
   * Un hachage MD5, si vous choisissez toouse une. **Cette étape est facultative.**
     
    Vous pouvez exécuter hello suivant pering de Microsoft tooconfigure applet de commande pour votre circuit
     
        New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="tooview-microsoft-peering-details"></a>informations d’homologation de tooview Microsoft
Vous pouvez obtenir les détails de configuration à l’aide de hello suivant l’applet de commande.

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="tooupdate-microsoft-peering-configuration"></a>configuration d’homologation de tooupdate Microsoft
Vous pouvez mettre à jour une partie de la configuration de hello à l’aide de hello suivant l’applet de commande.

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a>l’homologation de Microsoft toodelete
Vous pouvez supprimer la configuration d’homologation par hello suivant l’applet de commande en cours d’exécution.

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a>Étapes suivantes
Ensuite, [lier un circuit ExpressRoute de tooan réseau virtuel](expressroute-howto-linkvnet-classic.md).

* Pour plus d'informations sur les workflows, consultez [Workflows ExpressRoute](expressroute-workflows.md).
* Pour plus d’informations sur l’homologation du circuit, consultez [Circuits ExpressRoute et domaines de routage](expressroute-circuit-peerings.md).

