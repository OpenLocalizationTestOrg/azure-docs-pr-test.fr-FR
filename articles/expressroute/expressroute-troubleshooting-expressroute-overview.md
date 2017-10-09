---
title: "Vérification de la connectivité : Guide de dépannage Azure ExpressRoute | Microsoft Docs"
description: "Cette page fournit des instructions sur la résolution des problèmes et la validation de la connectivité de tooend de fin d’un circuit ExpressRoute."
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 713c39c7eafd77a4380b2a91902a9686f2ce1d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="verifying-expressroute-connectivity"></a>Vérification de la connectivité ExpressRoute
ExpressRoute, qui étend un réseau local en hello cloud de Microsoft via une connexion privée qui est facilitée par un fournisseur de connectivité, implique hello suivant trois zones de réseau distinctes :

-   Réseau de client
-   Réseau de fournisseur
-   Centre de données Microsoft

Hello ce document vise toohelp utilisateur tooidentify où (ou même si) il existe un problème de connectivité et dans la zone, tooseek contribuant à partir de problème de hello tooresolve équipe appropriée. Si la prise en charge de Microsoft est nécessaire tooresolve un problème, ouvrez un ticket de support avec [Support technique de Microsoft][Support].

> [!IMPORTANT]
> Ce document est prévue toohelp diagnostic et résolution des problèmes de simples. Il n’est pas prévue toobe un remplacement pour le support technique de Microsoft. Ouvrez un ticket de support avec [Support technique de Microsoft] [ Support] en cas de problème de hello toosolve impossible à l’aide d’instructions hello fournies.
>
>

## <a name="overview"></a>Vue d'ensemble
Hello diagramme suivant montre connectivité logique de hello d’un client réseau tooMicrosoft réseau à l’aide d’ExpressRoute.
[![1]][1]

Bonjour précédant le diagramme, les nombres de hello indiquent les points clés du réseau. points de réseau Hello sont souvent référencés dans cet article par leur numéro associé.

En fonction de la connectivité d’ExpressRoute hello (modèle Cloud Exchange colocalisation, connexion Ethernet de point à point ou pour tout (IPVPN)) hello réseau points 3 et 4 peuvent être commutateurs (périphériques de couche 2). les points de clé réseau Hello illustrées sont les suivantes :

1.  Appareil de calcul du client (par exemple, un serveur ou un PC)
2.  CE : routeurs de périphérie du client 
3.  PE (collaborant avec des CE) : routeurs / commutateurs de périphérie du fournisseur qui collaborent avec des routeurs de périphérie du client. Appelle tooas PE-EC dans ce document.
4.  PE (collaborant avec des MSEE) : routeurs / commutateurs de périphérie du fournisseur qui collaborent avec des MSEE. Appelle tooas PE-MSEEs dans ce document.
5.  MSEE : routeurs ExpressRoute Microsoft Enterprise Edge (MSEE)
6.  Passerelle de réseau virtuel (VNet)
7.  Dispositif de hello réseau virtuel Azure de calcul

Si des modèles de connectivité Cloud Exchange colocalisation ou une connexion Ethernet de point à point hello sont utilisées, le routeur de périphérie client hello (2) serait établir BGP d’homologation avec MSEEs (5). Les points de réseau 3 et 4 existent toujours, mais sont quelque peu transparents en tant qu'appareils de couche 2.

Si le modèle de connectivité hello pour tout (IPVPN) est utilisé, hello PEs (accès MSEE) (4) établit BGP d’homologation avec MSEEs (5). Itinéraires puis propage réseau du client via le réseau de fournisseur de service de hello IPVPN toohello précédent.

>[!NOTE]
>Pour la haute disponibilité ExpressRoute, Microsoft nécessite une paire de sessions BGP redondante entre des MSEE (5) et des PE-MSEE (4). Une paire redondante de chemins d’accès au réseau est également recommandée entre le réseau du client et les PE-CE. Toutefois, dans le modèle de connexion pour tout (IPVPN), un périphérique de CE seul (2) peut être connecté tooone ou plus PEs (3).
>
>

toovalidate un circuit ExpressRoute, hello suit sont traités (avec le point de réseau hello indiqué par nombre de hello associé) :
1. [Validation de l'approvisionnement et l’état du circuit (5)](#validate-circuit-provisioning-and-state)
2. [Valider qu'au moins une homologation ExpressRoute est configurée (5)](#validate-peering-configuration)
3. [Valider ARP entre le fournisseur de services Microsoft et hello (lien entre 4 et 5)](#validate-arp-between-microsoft-and-the-service-provider)
4. [Valider le protocole BGP et itinéraires hello MSEE (BGP entre too5 4 et 5 too6 si un réseau virtuel est connecté)](#validate-bgp-and-routes-on-the-msee)
5. [Hello de vérification des statistiques de trafic (trafic passant par 5)](#check-the-traffic-statistics)

Plusieurs validations et les vérifications seront ajoutées dans hello future, vérifier tous les mois !

##<a name="validate-circuit-provisioning-and-state"></a>Validation de l'approvisionnement et l’état du circuit
Quel que soit le modèle de connectivité de hello, un circuit ExpressRoute a toobe créée et, par conséquent, un service de clé générée pour l’approvisionnement du circuit. L’approvisionnement d’un circuit ExpressRoute établit une connexion de couche 2 redondante entre les PE-MSEE (4) et les MSEE (5). Pour plus d’informations sur la façon dont toocreate, modifier, de configurer et vérifier un circuit ExpressRoute, consultez l’article de hello [créer et modifier un circuit ExpressRoute][CreateCircuit].

>[!TIP]
>Une clé de service identifie un circuit ExpressRoute de façon unique. Cette clé est requise pour la plupart des commandes powershell de hello mentionnés dans ce document. En outre, si vous avez besoin obtenir de l’aide de Microsoft ou d’un tootroubleshoot de partenaire ExpressRoute un problème d’ExpressRoute, servir hello tooreadily clé identifier circuit de hello.
>
>

###<a name="verification-via-hello-azure-portal"></a>Vérification par hello portail Azure
Bonjour portail Azure, état hello d’un circuit ExpressRoute peut être vérifiée en sélectionnant ![2][2] sur hello menu de barre de côté gauche, puis en sélectionnant hello circuit ExpressRoute. En sélectionnant un ExpressRoute circuit sous « Toutes les ressources » ouvre le panneau de circuit ExpressRoute de hello. Bonjour ![3][3] section du panneau hello, hello ExpressRoute essentials sont répertoriés comme indiqué dans hello suivant capture d’écran :

![4][4]    

Bonjour ExpressRoute Essentials, *Circuit état* indique l’état hello du circuit hello sur hello côté de Microsoft. *État du fournisseur* indique si le circuit de hello a été *préparé non configuré* côté fournisseur de services de hello. 

Pour un toobe de circuit ExpressRoute opérationnel, hello *Circuit état* doit être *activé* et hello *état du fournisseur* doit être *configuré*.

>[!NOTE]
>Si hello *Circuit état* est désactivée, contactez [Support technique de Microsoft][Support]. Si hello *état du fournisseur* est ne pas configurée, contactez votre fournisseur de services.
>
>

###<a name="verification-via-powershell"></a>Vérification par le biais de PowerShell
toolist tous hello circuits ExpressRoute dans un groupe de ressources, utilisez hello de commande suivante :

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
>Vous pouvez obtenir le nom de votre groupe de ressources via hello portail Azure. Consultez la sous-section précédente de hello de ce document et prenez note de que ce nom de groupe de ressources hello est répertorié dans la capture d’écran : exemple hello.
>
>

tooselect un circuit ExpressRoute particulier dans un groupe de ressources, hello utilisez commande suivante :

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

Voici un exemple de réponse :

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

tooconfirm si un circuit ExpressRoute est opérationnel, payer toohello une attention toute particulière champs qui suivent :

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
>Si hello *état d’approvisionnement* est désactivée, contactez [Support technique de Microsoft][Support]. Si hello *ServiceProviderProvisioningState* est ne pas configurée, contactez votre fournisseur de services.
>
>

###<a name="verification-via-powershell-classic"></a>Vérification par le biais de PowerShell (classique)
toolist tous hello circuits ExpressRoute sous un abonnement, utilisez hello commande suivante :

    Get-AzureDedicatedCircuit

tooselect un circuit ExpressRoute particulier, utilisez hello de commande suivante :

    Get-AzureDedicatedCircuit -ServiceKey **************************************

Voici un exemple de réponse :

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

tooconfirm si un circuit ExpressRoute est opérationnel, payer toohello une attention toute particulière suivant champs : ServiceProviderProvisioningState : état de mise en service : activé

>[!NOTE]
>Si hello *état* est désactivée, contactez [Support technique de Microsoft][Support]. Si hello *ServiceProviderProvisioningState* est ne pas configurée, contactez votre fournisseur de services.
>
>

##<a name="validate-peering-configuration"></a>Validation de la configuration de l’homologation
Fournisseur de services hello après hello terminé approvisionnement du circuit ExpressRoute de hello, une configuration de routage peut être créée sur hello circuit ExpressRoute entre MSEE-réservations persistantes (4) et MSEEs (5). Chaque circuit ExpressRoute peut avoir une, deux ou trois contextes de routage activés : homologation privée Azure (trafic tooprivate réseaux virtuels dans Azure), homologation publique Azure (trafic toopublic adresses dans Azure) et (le trafic tooOffice 365 d’homologation Microsoft et Dynamics 365). Pour plus d’informations sur la façon de toocreate et modifier la configuration de routage, consultez l’article hello [créer et modifier le routage pour un circuit ExpressRoute][CreatePeering].

###<a name="verification-via-hello-azure-portal"></a>Vérification par hello portail Azure
>[!IMPORTANT]
>Il existe un bogue connu dans hello portail Azure, dans laquelle les homologations ExpressRoute sont *pas* indiquées dans le portail hello si configuré par le fournisseur de services hello. Ajout des homologations ExpressRoute via le portail de hello ou PowerShell *remplace les paramètres du fournisseur de service hello*. Cette action interrompt hello routage sur le circuit ExpressRoute de hello et requiert la prise en charge de hello hello fournisseur toorestore hello de paramètres de service et rétablir le routage normal. Modifiez uniquement hello ExpressRoute homologations s’il est certain que ce fournisseur de service hello fournit uniquement les services de couche 2 !
>
>

<p/>
>[!NOTE]
>Si la couche 3 est fournie par hello homologations de fournisseur et hello du service sont vides dans le portail de hello, PowerShell peut être utilisé toosee hello service fournisseur configuré paramètres.
>
>

Bonjour portail Azure, l’état d’un circuit ExpressRoute peut être vérifiée en sélectionnant ![2][2] sur hello menu de barre de côté gauche, puis en sélectionnant hello circuit ExpressRoute. En sélectionnant un ExpressRoute circuit sous « Toutes les ressources » pour ouvrir Panneau de circuit ExpressRoute hello. Bonjour ![3][3] section du panneau hello, hello ExpressRoute essentials sont répertoriés comme indiqué dans hello suivant capture d’écran :

![5][5]

Bonjour précédent exemple, Azure indiqués contexte de routage d’homologation privée est activée, alors que Azure public et les contextes de routage d’homologation Microsoft ne sont pas activés. Un contexte d’homologation a été activé correctement aurait également les sous-réseaux de point à point principaux et secondaires (requis pour le protocole BGP) hello répertoriés. les sous-réseaux Hello /30 sont utilisés pour l’adresse IP hello interface hello MSEEs et MSEEs-PE. 

>[!NOTE]
>Si une homologation n’est pas activée, vérifiez si sous-réseaux principaux et secondaires hello affectés correspond à configuration hello sur PE-MSEEs. Si non, toochange à la configuration hello sur les routeurs MSEE, consultez trop[créer et modifier le routage pour un circuit ExpressRoute][CreatePeering]
>
>

###<a name="verification-via-powershell"></a>Vérification par le biais de PowerShell
tooget hello Azure privé d’homologation détails de configuration, utilisez hello suivant les commandes :

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

Voici un exemple de réponse pour une homologation privée correctement configurée :

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 Un contexte d’homologation a été activé correctement aurait des préfixes d’adresse principale et secondaire hello répertoriés. les sous-réseaux Hello /30 sont utilisés pour l’adresse IP hello interface hello MSEEs et MSEEs-PE.

tooget hello Azure public d’homologation détails de configuration, utilisez hello suivant les commandes :

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

tooget hello Microsoft d’homologation détails de configuration, utilisez hello suivant de commandes :

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

Si aucune homologation n’est configurée, un message d’erreur est généré. Un exemple de réponse, lorsque hello indiquée d’homologation (Azure publics d’homologation dans cet exemple) n’est pas configuré dans le circuit de hello :

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
>Si une homologation n’est pas activée, vérifiez si configuration hello sous-réseaux principaux et secondaires affectés correspondance hello hello lié PE-MSEE. Également vérifier si hello corriger *VlanId*, *AzureASN*, et *PeerASN* sont utilisés sur MSEEs et si ces valeurs est mappé toohello que ceux utilisés sur hello lié PE-MSEE. Si le hachage MD5 est choisie, doit être les même sur MSEE et PE-MSEE paire clé partagée de hello. configuration de hello toochange sur les routeurs MSEE hello, consultez trop [créer et modifier le routage pour un circuit ExpressRoute] [CreatePeering].  
>
>

### <a name="verification-via-powershell-classic"></a>Vérification par le biais de PowerShell (classique)
tooget hello Azure privé d’homologation détails de configuration, utilisez hello commande suivante :

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

Voici un exemple de réponse pour une homologation privée correctement configurée :

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

A été activée avec succès, contexte d’homologation aurait sous-réseaux homologue principal et secondaire de hello répertoriés. les sous-réseaux Hello /30 sont utilisés pour l’adresse IP hello interface hello MSEEs et MSEEs-PE.

tooget hello Azure public d’homologation détails de configuration, utilisez hello suivant les commandes :

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

tooget hello Microsoft d’homologation détails de configuration, utilisez hello suivant de commandes :

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
>Si homologations de couche 3 ont été définies par le fournisseur de services hello, paramètre homologations de ExpressRoute hello via le portail de hello ou PowerShell remplace les paramètres du fournisseur de service hello. La réinitialisation des paramètres d’homologation du côté fournisseur hello requiert la prise en charge de hello hello du fournisseur de services. Modifiez uniquement hello ExpressRoute homologations s’il est certain que ce fournisseur de service hello fournit uniquement les services de couche 2 !
>
>

<p/>
>[!NOTE]
>Si une homologation n’est pas activée, vérifiez si hello homologue principal et secondaire sous-réseaux affectés correspondance hello configuration sur hello lié PE-MSEE. Également vérifier si hello corriger *VlanId*, *AzureAsn*, et *PeerAsn* sont utilisés sur MSEEs et si ces valeurs est mappé toohello que ceux utilisés sur hello lié PE-MSEE. configuration de hello toochange sur les routeurs MSEE hello, consultez trop [créer et modifier le routage pour un circuit ExpressRoute] [CreatePeering].
>
>

## <a name="validate-arp-between-microsoft-and-hello-service-provider"></a>Valider ARP entre le fournisseur de services Microsoft et hello
Cette section utilise les commandes PowerShell (classiques). Si vous avez utilisé les commandes PowerShell Azure Resource Manager, assurez-vous que vous disposez d’abonnement de toohello d’accès d’administrateur/co-admin via [portail Azure classic][OldPortal]. Pour le dépannage à l’aide du Gestionnaire de ressources Azure commandes reportez-vous toohello [tables ARP de mise en route dans le modèle de déploiement du Gestionnaire de ressources hello] [ ARP] document.

>[!NOTE]
>tooget ARP, hello portail Azure et commandes Azure PowerShell de gestionnaire de ressources peut être utilisé. Si vous rencontrez des erreurs avec les commandes du Gestionnaire de ressources PowerShell Azure hello, les commandes PowerShell classiques doivent fonctionner en tant que PowerShell classique, les commandes fonctionnent également avec des circuits ExpressRoute de gestionnaire de ressources Azure.
>
>

tooget hello table ARP à partir du routeur MSEE principal hello pour l’homologation privée hello, utilisez hello de commande suivante :

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

Un exemple de réponse pour la commande hello, dans un scénario de réussite hello :

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

De même, vous pouvez vérifier hello table ARP de hello MSEE Bonjour *principal*/*secondaire* chemin d’accès, pour *privé* /  *Public*/*Microsoft* homologations.

Hello exemple suivant montre hello réponse de la commande hello pour une homologation n’existe pas.

    ARP Info:
       
>[!NOTE]
>Si hello table ARP ne dispose pas des adresses IP des interfaces de hello mappé tooMAC adresses, hello révision informations suivantes :
>1. Si hello première adresse IP du sous-réseau de hello /30 affecté pour la liaison hello entre hello MSEE-PR et MSEE est utilisé sur l’interface hello de MSEE-PR. Azure utilise toujours l’adresse IP de la deuxième hello pour MSEEs.
>2. Vérifiez si le client hello (C-Tag) et balises VLAN de service (S-Tag) correspondent à la fois sur la paire de MSEE-PR et MSEE.
>
>

## <a name="validate-bgp-and-routes-on-hello-msee"></a>Valider BGP et itinéraires hello MSEE
Cette section utilise les commandes PowerShell (classiques). Si vous avez utilisé les commandes PowerShell Azure Resource Manager, assurez-vous que vous disposez d’abonnement de toohello d’accès d’administrateur/co-admin via [portail Azure classic][OldPortal]

>[!NOTE]
>tooget BGP plus d’informations, les deux hello portail Azure et les commandes PowerShell de gestionnaire de ressources Azure peuvent être utilisés. Si vous rencontrez des erreurs avec les commandes du Gestionnaire de ressources PowerShell Azure hello, les commandes PowerShell classiques doivent fonctionner en tant que PowerShell classique, les commandes fonctionnent également avec des circuits ExpressRoute de gestionnaire de ressources Azure.
>
>

tooget hello table de routage (voisin BGP) pour un contexte de routage spécifique, utilisez les hello de commande suivante :

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

Voici un exemple de réponse :

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

Comme indiqué dans le précédent exemple de hello, commande hello est toodetermine utile pour la durée pendant laquelle le contexte de routage hello a été établie. Il indique également le nombre de préfixes d’itinéraire publié par routeur d’homologation de hello.

>[!NOTE]
>Si l’état du hello est actif ou inactif, vérifiez si hello homologue principal et secondaire sous-réseaux affectés correspondance hello configuration sur hello lié PE-MSEE. Également vérifier si hello corriger *VlanId*, *AzureAsn*, et *PeerAsn* sont utilisés sur MSEEs et si ces valeurs est mappé toohello que ceux utilisés sur hello lié PE-MSEE. Si le hachage MD5 est choisie, doit être les même sur MSEE et PE-MSEE paire clé partagée de hello. configuration de hello toochange sur les routeurs MSEE hello, consultez trop[créer et modifier le routage pour un circuit ExpressRoute][CreatePeering].
>
>

<p/>
>[!NOTE]
>Si certaines destinations ne sont pas accessibles via une homologation particulier, vérifiez la table d’itinéraires hello de MSEEs hello appartenant toohello de contexte d’homologation particulier. Si un préfixe correspondant (NATed IP possible) est présent dans la table de routage hello, vérifiez s’il existe des pare-feu/groupe de sécurité réseau/ACL sur le chemin d’accès hello et si elles autorisent le trafic de hello.
>
>

tooget hello table de routage complète à partir de MSEE sur hello *principal* chemin d’accès pour hello particulier *privé* contexte de routage, hello utilisez commande suivante :

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

Un résultat réussi exemple de commande hello est la suivante :

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

De même, vous pouvez vérifier la table de routage hello de hello MSEE Bonjour *principal*/*secondaire* chemin d’accès, pour *privé* / *Public*/*Microsoft* un contexte d’homologation.

Hello exemple suivant montre hello réponse de la commande hello pour une homologation n’existe pas :

    Route Table Info:

##<a name="check-hello-traffic-statistics"></a>Vérifiez hello statistiques de trafic
tooget hello combiné des statistiques de trafic du chemin d’accès primaire et secondaire--octets et l’extraction--d’un contexte d’homologation, hello utilisez commande suivante :

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

Un exemple de sortie de la commande hello est :

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

Un exemple de sortie de la commande hello pour une homologation inexistante est :

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations ou de l’aide, consultez hello suivant liens :

- [Support Microsoft][Support]
- [Création et modification d’un circuit ExpressRoute][CreateCircuit]
- [Créer et modifier le routage le routage pour un circuit ExpressRoute][CreatePeering]

<!--Image References-->
[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Connectivité logique Express Route"
[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Icône Toutes les ressources"
[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Icône Vue d’ensemble"
[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "Capture d’écran : exemple pour ExpressRoute Essentials"
[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "Capture d’écran : exemple pour ExpressRoute Essentials"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






