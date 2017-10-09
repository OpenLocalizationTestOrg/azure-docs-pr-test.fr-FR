---
title: "Lier un circuit ExpressRoute de tooan réseau virtuel : PowerShell : classique : Azure | Documents Microsoft"
description: "Ce document fournit une vue d’ensemble du mode toolink virtuel réseaux (réseaux virtuels) tooExpressRoute circuits à l’aide de PowerShell et le modèle de déploiement classique hello."
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a>Se connecter à un circuit ExpressRoute de tooan de réseau virtuel à l’aide de PowerShell (classique)
> [!div class="op_single_selector"]
> * [Portail Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Interface de ligne de commande Azure](howto-linkvnet-cli.md)
> * [Vidéo - portail Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (classique)](expressroute-howto-linkvnet-classic.md)
>

Cet article vous aidera à lier des circuits ExpressRoute de tooAzure des réseaux virtuels (réseaux virtuels) à l’aide de PowerShell et le modèle de déploiement classique hello. Réseaux virtuels peuvent être dans hello même abonnement ou peuvent faire partie d’un autre abonnement.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**À propos des modèles de déploiement Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a>Conditions préalables à la configuration
1. Vous devez la version la plus récente des modules d’Azure PowerShell hello hello. Vous pouvez télécharger les modules PowerShell dernière hello hello section PowerShell de hello [page de téléchargements Azure](https://azure.microsoft.com/downloads/). Suivez les instructions de hello dans [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) pour obtenir des instructions sur la façon de tooconfigure votre ordinateur toouse hello Azure les modules PowerShell.
2. Vous devez tooreview hello [conditions préalables](expressroute-prerequisites.md), [exigences routage](expressroute-routing.md), et [workflows](expressroute-workflows.md) avant de commencer la configuration.
3. Vous devez disposer d’un circuit ExpressRoute actif.
   * Suivez les instructions de hello trop[créer un circuit ExpressRoute](expressroute-howto-circuit-classic.md) et à ce que votre fournisseur de connectivité Active circuit de hello.
   * Vérifiez que l’homologation privée Azure est configurée pour votre circuit. Consultez hello [configurer le routage](expressroute-howto-routing-classic.md) article pour obtenir des instructions de routage.
   * Assurez-vous que l’homologation privée Azure est configuré et est l’homologation BGP hello entre votre réseau et de Microsoft afin que vous pouvez activer la connectivité de bout en bout.
   * Vous devez disposer d'un réseau virtuel et d’une passerelle de réseau virtuel créés et totalement approvisionnés. Suivez les instructions de hello trop[configurer un réseau virtuel pour ExpressRoute](expressroute-howto-vnet-portal-classic.md).

Vous pouvez lier des réseaux virtuels de too10 tooan circuit ExpressRoute. Tous les réseaux virtuels doivent être Bonjour même région géopolitique. Vous pouvez lier un plus grand nombre de réseaux virtuels tooyour circuit ExpressRoute, ou lier des réseaux virtuels situés dans d’autres régions géopolitiques si vous avez activé le module complémentaire de hello ExpressRoute premium. Vérifiez hello [FAQ](expressroute-faqs.md) pour plus d’informations sur le module complémentaire de hello premium.

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Connecter un réseau virtuel Bonjour même circuit de tooa d’abonnement
Vous pouvez lier un circuit ExpressRoute de tooan réseau virtuel à l’aide de hello suivant l’applet de commande. Assurez-vous que cette passerelle de réseau virtuel hello est créée et est prête pour la liaison avant d’exécuter les applets de commande hello.

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Connecter un réseau virtuel dans un circuit de tooa autre abonnement
Vous pouvez partager un circuit ExpressRoute entre plusieurs abonnements. Hello figure suivante montre une simple principe de fonctionnement du partage de circuits ExpressRoute entre plusieurs abonnements.

Chaque hello petits clouds dans cloud volumineux de hello est utilisé toorepresent abonnements appartenant aux départements toodifferent au sein d’une organisation. Chacun des services hello au sein de l’organisation de hello permettre utiliser leur propre abonnement pour déployer leurs services--mais les services de hello peut partager un réseau local ExpressRoute circuit tooconnect tooyour précédent. Un seul département (dans cet exemple : informatique) peut posséder de circuit ExpressRoute de hello. Autres abonnements au sein de l’organisation de hello peuvent utiliser le circuit ExpressRoute de hello.

> [!NOTE]
> Frais de connectivité et de bande passante pour le circuit de hello dédié sera propriétaire du circuit ExpressRoute toohello appliqué. Tous les réseaux virtuels partagent hello même bande passante.
> 
> 

![Connectivité entre abonnements](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a>Administration
Hello *propriétaire du circuit* est hello administrateur/coadministrator d’abonnement hello dans le hello ExpressRoute circuit est créé. Hello propriétaire du circuit peut autoriser les administrateurs/coadministrators d’autres abonnements, tooas référencé *les utilisateurs de circuit*, toouse hello dédié circuit dont ils sont propriétaires. Les utilisateurs de circuit peut de circuit ExpressRoute de l’organisation autorisés toouse hello lier le réseau virtuel de hello dans leur toohello abonnement circuit ExpressRoute une fois qu’ils sont autorisés.

propriétaire du circuit Hello possède les autorisations hello power toomodify et révoquer à tout moment. Révocation d’une autorisation génère tous les liens en cours de suppression de l’abonnement hello dont l’accès a été révoqué.

### <a name="circuit-owner-operations"></a>Opérations du propriétaire du circuit

**Création d’une autorisation**

Hello propriétaire du circuit autorise les administrateurs de hello d’autres abonnements toouse hello spécifié circuit. Dans l’exemple suivant de hello, administrateur hello du circuit de hello (Contoso IT) permet d’administrateur hello d’un autre toolink d’abonnement (développement de Test) de circuit de toohello tootwo réseaux virtuels. administrateur Contoso Hello permet cela en spécifiant l’ID de développement et de Test Microsoft hello. applet de commande Hello n’envoie pas de courrier électronique toohello spécifié ID Microsoft. propriétaire du circuit Hello doit tooexplicitly notifier hello autre propriétaire d’abonnement qui hello d’autorisation est terminée.

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

**Vérification des autorisations**

propriétaire du circuit Hello peut consulter toutes les autorisations qui sont émises sur un circuit en particulier en exécutant hello suivant l’applet de commande :

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


**Mise à jour des autorisations**

propriétaire du circuit Hello peut modifier les autorisations à l’aide de hello suivant l’applet de commande :

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


**Suppression des autorisations**

propriétaire du circuit Hello permettre révoquer/supprimer un autorisations toohello utilisateur en exécutant hello suivant l’applet de commande :

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a>Opérations de l’utilisateur du circuit

**Vérification des autorisations**

utilisateur de circuit Hello peut passer en revue les autorisations à l’aide de hello suivant l’applet de commande :

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

**Échange des autorisations de lien**

utilisateur du circuit Hello peut exécuter hello suivant l’applet de commande tooredeem une autorisation de lien :

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

Exécutez cette commande dans l’abonnement hello qui vient d’être liée pour le réseau virtuel de hello :

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur ExpressRoute, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md).

