---
title: "Créer et modifier un circuit ExpressRoute avec PowerShell et Azure Resource Manager | Microsoft Docs"
description: "Cet article décrit comment toocreate, configurer, vérifier, mettre à jour, supprimer et annuler le déploiement d’un circuit ExpressRoute."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f997182e-9b25-4a7a-b079-b004221dadcc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8d76c577a9cffdd393abac1b76cccc27d92e9e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a>Créer et modifier un circuit ExpressRoute à l’aide de PowerShell
> [!div class="op_single_selector"]
> * [Portail Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Interface de ligne de commande Azure](howto-circuit-cli.md)
> * [Vidéo - portail Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (classique)](expressroute-howto-circuit-classic.md)
>

Cet article décrit comment toocreate un Azure ExpressRoute circuit en utilisant le modèle de déploiement Azure Resource Manager hello et les applets de commande de PowerShell. Cet article vous montre également l’état de hello toocheck du circuit de hello, mettre à jour, supprimer et ou annuler le déploiement.

## <a name="before-you-begin"></a>Avant de commencer
* Installer la version la plus récente hello Hello applets de commande PowerShell de gestionnaire de ressources Azure. Pour plus d’informations, voir [Présentation d’Azure PowerShell](/powershell/azure/overview).
* Hello de révision [conditions préalables](expressroute-prerequisites.md) et [workflows](expressroute-workflows.md) avant de commencer la configuration.


## <a name="create-and-provision-an-expressroute-circuit"></a>Création et approvisionnement d’un circuit ExpressRoute
### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a>1. Connectez-vous à tooyour compte Azure et sélectionnez votre abonnement
toobegin votre configuration, de connexion tooyour compte Azure. Utilisez hello suivant toohelp exemples que vous connectez :

```powershell
Login-AzureRmAccount
```

Vérifier les abonnements hello pour le compte de hello :

```powershell
Get-AzureRmSubscription
```

Sélectionnez hello abonnement toocreate un ExpressRoute de circuit pour :

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2. Obtenir la liste de hello de fournisseurs pris en charge, des emplacements et des bandes passantes
Avant de créer un circuit ExpressRoute, vous devez liste hello de fournisseurs de connectivité pris en charge, des emplacements et des options de bande passante.

applet de commande PowerShell de Hello **Get-AzureRmExpressRouteServiceProvider** retourne cette information, vous allez utiliser dans les étapes suivantes :

```powershell
Get-AzureRmExpressRouteServiceProvider
```

Vérifiez toosee si votre fournisseur de connectivité y sont répertoriée. Prenez note de hello informations suivantes. Vous en aurez besoin ultérieurement lorsque vous créerez un circuit.

* Nom
* PeeringLocations
* BandwidthsOffered

Vous êtes maintenant prêt toocreate un circuit ExpressRoute.   

### <a name="3-create-an-expressroute-circuit"></a>3. Création d’un circuit ExpressRoute
Si vous n’avez pas déjà un groupe de ressources, vous devez en créer un avant de créer votre circuit ExpressRoute. Vous pouvez le faire en exécutant hello de commande suivante :

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


Bonjour à l’exemple suivant montre comment toocreate un ExpressRoute de 200 Mbits/s de circuit via Equinix dans Silicon Valley. Si vous utilisez un autre fournisseur et des paramètres différents, utilisez ces informations quand vous créez votre requête. Hello Voici un exemple de demande pour une nouvelle clé de service :

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

Assurez-vous que vous spécifiez un niveau de référence (SKU) correct hello et famille de référence (SKU) :

* Le niveau de référence détermine si ExpressRoute standard ou un module complémentaire ExpressRoute Premium est activé. Vous pouvez spécifier *Standard* tooget hello référence (SKU) standard ou *Premium* pour le module complémentaire de hello premium.
* Famille de référence (SKU) détermine le type de facturation hello. Vous pouvez spécifier *Metereddata* pour définir un forfait de données limité et *Unlimiteddata* pour un forfait de données illimité. Vous pouvez modifier le type de facturation hello de *Metereddata* trop*Unlimiteddata*, mais vous ne pouvez pas modifier le type hello de *Unlimiteddata* trop*Metereddata* .

> [!IMPORTANT]
> Votre circuit ExpressRoute sera facturé dès hello, qu'une clé de service est émise. Veillez à effectuer cette opération lorsque le fournisseur de connectivité hello est circuit de hello tooprovision prêt.
> 
> 

réponse de Hello contient la clé de service hello. Vous pouvez obtenir une description détaillée de tous les paramètres de hello en exécutant hello de commande suivante :

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a>4. Répertorier tous les circuits ExpressRoute
tooget une liste de tous les hello circuits ExpressRoute que vous avez créé, exécutez hello **Get-AzureRmExpressRouteCircuit** commande :

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

réponse de Hello ressemblera toohello similaire, l’exemple suivant :

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
    CircuitProvisioningState          : Enabled
    ServiceProviderProvisioningState  : NotProvisioned
    ServiceProviderNotes              :
    ServiceProviderProperties         : {
                                          "ServiceProviderName": "Equinix",
                                          "PeeringLocation": "Silicon Valley",
                                          "BandwidthInMbps": 200
                                        }
    ServiceKey                        : **************************************
    Peerings                          : []

Vous pouvez récupérer ces informations à tout moment à l’aide de hello `Get-AzureRmExpressRouteCircuit` applet de commande. Rendre hello sans paramètre répertorie tous les circuits hello. Votre clé de service s’afficheront dans hello *ServiceKey* champ :

```powershell
Get-AzureRmExpressRouteCircuit
```


réponse de Hello ressemblera toohello similaire, l’exemple suivant :

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
    ServiceProviderProvisioningState : NotProvisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


Vous pouvez obtenir une description détaillée de tous les paramètres de hello en exécutant hello de commande suivante :

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5. Envoyer le fournisseur de connectivité hello service tooyour clé pour la configuration
*ServiceProviderProvisioningState* fournit des informations sur l’état actuel de hello de configuration sur le côté du fournisseur de services hello. État fournit les état hello sur hello côté de Microsoft. Pour plus d’informations sur les États de configuration de circuit, consultez hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) l’article.

Lorsque vous créez un nouveau circuit ExpressRoute, circuit de hello sera Bonjour suivant l’état :

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



circuit de Hello modifiera toohello suivant l’état lorsque le fournisseur de connectivité hello est en cours de hello de l’activer pour vous :

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

Pour vous toobe en mesure de toouse un circuit ExpressRoute, il doit être Bonjour suivant l’état :

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6. Vérifier régulièrement le statut de hello et état hello de clé du circuit hello
Vérification du statut de hello et état hello de clé du circuit hello vous permet de savoir quand votre fournisseur aura activé votre circuit. Après la configuration de circuit de hello, *ServiceProviderProvisioningState* apparaît sous la forme *configuré*, comme indiqué dans hello l’exemple suivant :

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


réponse de Hello ressemblera toohello similaire, l’exemple suivant :

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

### <a name="7-create-your-routing-configuration"></a>7. Créer votre configuration de routage
Pour obtenir des instructions, consultez hello [circuit ExpressRoute de configuration de routage](expressroute-howto-routing-arm.md) toocreate de l’article et modifier des homologations de circuit.

> [!IMPORTANT]
> Ces instructions s’appliquent uniquement à toocircuits qui sont créés avec des fournisseurs de services qui offrent des services de couche 2 de connectivité. Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement un VPN IP, comme MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a>8. Lier un circuit ExpressRoute de tooan réseau virtuel
Ensuite, lier un circuit ExpressRoute de tooyour réseau virtuel. Hello d’utilisation [liaison virtuel réseaux tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article lorsque vous travaillez avec un modèle de déploiement du Gestionnaire de ressources hello.

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>État de hello lors de l’obtention d’un circuit ExpressRoute
Vous pouvez récupérer ces informations à tout moment à l’aide de hello **Get-AzureRmExpressRouteCircuit** applet de commande. Rendre hello sans paramètre répertorie tous les circuits hello.

```powershell
Get-AzureRmExpressRouteCircuit
```


réponse de Hello sera similaire toohello l’exemple suivant :

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


Vous pouvez obtenir des informations sur un circuit ExpressRoute spécifique en passant le nom de groupe de ressources hello et nom du circuit comme un appel de toohello paramètre :

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


réponse de Hello ressemblera toohello similaire, l’exemple suivant :

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


Vous pouvez obtenir une description détaillée de tous les paramètres de hello en exécutant hello de commande suivante :

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <a name="modify"></a>Modification d’un circuit ExpressRoute
Vous pouvez modifier certaines propriétés d'un circuit ExpressRoute sans affecter la connectivité.

Vous pouvez effectuer hello suivant sans interruption de service :

* Activer ou désactiver le module complémentaire ExpressRoute Premium pour votre circuit ExpressRoute.
* La bande passante de hello augmentation de votre circuit ExpressRoute fourni la capacité est disponible sur le port hello. Rétrogradation d’un circuit de bande passante hello n’est pas pris en charge. 
* Modifier hello plan à partir de données de limitées tooUnlimited données de contrôle. Modification de hello plan à partir de tooMetered données illimité que données ne sont pas prise en charge de contrôle.
* Vous pouvez activer et désactiver *Autoriser les opérations classiques*.

Pour plus d’informations sur les limites et limitations, consultez toohello [FAQ sur ExpressRoute](expressroute-faqs.md).

### <a name="tooenable-hello-expressroute-premium-add-on"></a>module complémentaire de tooenable hello ExpressRoute premium
Vous pouvez activer un module complémentaire de hello ExpressRoute premium pour votre circuit existant à l’aide de hello suivant extrait de code PowerShell :

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

circuit de Hello sera désormais hello ExpressRoute premium module complémentaire fonctionnalités sont activées. Nous allons commencer à vous de facturation pour la fonction d’un module complémentaire hello premium dès que la commande hello a été exécutée.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>module complémentaire de toodisable hello ExpressRoute premium
> [!IMPORTANT]
> Cette opération peut échouer si vous utilisez des ressources qui sont supérieures à ce qui est autorisé pour le circuit de standard hello.
> 
> 

Notez hello suivantes :

* Rétrogradation à partir de premium toostandard, vous devez vous assurer que nombre hello des réseaux virtuels qui sont liées toohello circuit est inférieure à 10. Si vous ne le faites pas, votre demande de mise à jour échoue et nous appliquons les tarifs Premium.
* Vous devez dissocier tous les réseaux virtuels dans d'autres régions géopolitiques. Si vous ne le faites pas, votre demande de mise à jour échoue et nous appliquons les tarifs Premium.
* Pour l’homologation privée, votre table de routage doit comporter moins de 4 000 routages. Si la taille de la table de routage est supérieure à 4 000 itinéraires, session BGP hello supprime et ne sera pas être réactivée jusqu'à ce que le nombre de hello de préfixes annoncés devient inférieur à 4 000.

Vous pouvez désactiver complémentaire hello ExpressRoute pour le circuit existant de hello à l’aide de hello suivant l’applet de commande PowerShell :

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>bande passante du circuit ExpressRoute hello tooupdate
Pour les options de la bande passante prises en charge pour le fournisseur, vérifiez hello [FAQ sur ExpressRoute](expressroute-faqs.md). Vous pouvez choisir n’importe quelle taille supérieure à la taille de hello de votre circuit existant.

> [!IMPORTANT]
> Vous avez peut-être circuit ExpressRoute de hello toorecreate si la capacité inadéquate est sur le port existant hello. Vous ne peut pas mettre à niveau de circuit de hello si aucune capacité supplémentaire n’est disponible à cet emplacement.
>
> Vous ne pouvez pas réduire la bande passante hello d’un circuit ExpressRoute sans interruption de service. Rétrogradation de la bande passante vous oblige le circuit ExpressRoute de hello toodeprovision et puis reconfigurez un circuit ExpressRoute de nouveau.
> 

Après avoir déterminé la taille que vous avez besoin, utilisez hello suivant commande tooresize votre circuit :

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


A la taille votre circuit côté de Microsoft hello. Vous devez ensuite contacter vos configurations de tooupdate de fournisseur de connectivité sur leur toomatch côté cette modification. Après avoir apporté cette notification, nous allons commencer à vous de facturation pour l’option de la bande passante hello mis à jour.

### <a name="toomove-hello-sku-from-metered-toounlimited"></a>toomove hello référence (SKU) à partir de toounlimited limitée
Vous pouvez modifier hello référence (SKU) d’un circuit ExpressRoute à l’aide de hello suivant extrait de code PowerShell :

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a>classique de toohello toocontrol accès et les environnements de gestionnaire de ressources
Passez en revue les instructions hello dans [circuits ExpressRoute de déplacer à partir du modèle de déploiement du Gestionnaire de ressources hello classique toohello](expressroute-howto-move-arm.md).  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Annulation de l’approvisionnement et suppression d’un circuit ExpressRoute
Notez hello suivantes :

* Vous devez supprimer le lien de tous les réseaux virtuels à partir de hello circuit ExpressRoute. Si cette opération échoue, vérifiez toosee si les réseaux virtuels sont liés toohello circuit.
* Si le fournisseur de service du circuit ExpressRoute hello état d’approvisionnement est **Provisioning** ou **configuré** vous devez collaborer avec votre circuit de hello toodeprovision service fournisseur de leur côté. Nous allons continuer tooreserve ressources et vous facturer jusqu'à ce que le fournisseur de services hello termine de circuit de hello désaffectation et nous avertit.
* Si le fournisseur de services hello a annulé le circuit de hello (fournisseur de services hello état d’approvisionnement est défini trop**non préparé**) vous pouvez ensuite supprimer le circuit de hello. Cela arrêtera la facturation pour le circuit de hello

Vous pouvez supprimer votre circuit ExpressRoute en exécutant hello de commande suivante :

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a>Étapes suivantes

Après avoir créé votre circuit, assurez-vous que vous hello suivant :

* [Créer et modifier le routage le routage pour votre circuit ExpressRoute](expressroute-howto-routing-arm.md)
* [Lier votre réseau virtuel de tooyour circuit ExpressRoute](expressroute-howto-linkvnet-arm.md)
