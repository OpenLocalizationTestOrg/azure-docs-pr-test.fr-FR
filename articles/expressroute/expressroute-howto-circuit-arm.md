---
title: "Créer et modifier un circuit ExpressRoute avec PowerShell et Azure Resource Manager | Microsoft Docs"
description: "Cet article explique comment créer, approvisionner, vérifier, mettre à jour, supprimer et déprovisionner un circuit ExpressRoute."
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
ms.date: 10/18/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: ef092a48994b68268109cb98bd6cd4526e259d5b
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/21/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a>Créer et modifier un circuit ExpressRoute à l’aide de PowerShell
> [!div class="op_single_selector"]
> * [Portail Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Interface de ligne de commande Azure](howto-circuit-cli.md)
> * [Vidéo - portail Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (classique)](expressroute-howto-circuit-classic.md)
>

Cet article explique comment créer un circuit ExpressRoute à l’aide des applets de commande PowerShell et du modèle de déploiement Azure Resource Manager. Cet article vous montre également comment vérifier l’état du circuit, le mettre à jour, le supprimer et annuler son approvisionnement.

## <a name="before-you-begin"></a>Avant de commencer
* Installez la dernière version des applets de commande PowerShell Azure Resource Manager. Pour plus d’informations, voir [Présentation d’Azure PowerShell](/powershell/azure/overview).
* Examinez les [conditions préalables](expressroute-prerequisites.md) et les [flux de travail](expressroute-workflows.md) avant de commencer la configuration.


## <a name="create"></a>Créer et approvisionner un circuit ExpressRoute
### <a name="1-sign-in-to-your-azure-account-and-select-your-subscription"></a>1. Vous connecter à votre compte Azure et sélectionner votre abonnement
Pour commencer votre configuration, connectez-vous à votre compte Azure. Utilisez les exemples suivants pour faciliter votre connexion :

```powershell
Login-AzureRmAccount
```

Vérifiez les abonnements du compte :

```powershell
Get-AzureRmSubscription
```

Sélectionnez l’abonnement pour lequel vous voulez créer un circuit ExpressRoute :

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-the-list-of-supported-providers-locations-and-bandwidths"></a>2. Récupérer la liste des fournisseurs, des emplacements et des bandes passantes pris en charge
Avant de créer un circuit ExpressRoute, vous avez besoin d’une liste des fournisseurs de services, des emplacements et des options de bande passante pris en charge.

L’applet de commande PowerShell **Get-AzureRmExpressRouteServiceProvider** retourne ces informations que vous utilisez dans les étapes ultérieures :

```powershell
Get-AzureRmExpressRouteServiceProvider
```

Vérifiez si votre fournisseur de connectivité y est référencé. Prenez note des éléments suivants, car vous en aurez besoin lors de la création d’un circuit :

* Nom
* PeeringLocations
* BandwidthsOffered

Vous êtes maintenant prêt à créer un circuit ExpressRoute.   

### <a name="3-create-an-expressroute-circuit"></a>3. Création d’un circuit ExpressRoute
Si vous n’avez pas déjà un groupe de ressources, vous devez en créer un avant de créer votre circuit ExpressRoute. Pour cela, vous pouvez exécuter la commande suivante :

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


L’exemple suivant montre comment créer un circuit ExpressRoute de 200 Mb/s par le biais d’Equinix dans la Silicon Valley. Si vous utilisez un autre fournisseur et des paramètres différents, utilisez ces informations quand vous créez votre requête. Utilisez l’exemple suivant pour demander une nouvelle clé de service :

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

Assurez-vous que vous spécifiez le niveau de référence (SKU) et la famille de références corrects :

* Le niveau de référence détermine si ExpressRoute standard ou un module complémentaire ExpressRoute Premium est activé. Vous pouvez spécifier *Standard* pour obtenir la référence (SKU) standard ou *Premium* pour le module complémentaire Premium.
* La famille de références détermine le type de facturation. Vous pouvez spécifier *Metereddata* pour définir un forfait de données limité et *Unlimiteddata* pour un forfait de données illimité. Vous pouvez changer le type de facturation de *Metereddata* en *Unlimiteddata*, mais que vous ne pouvez pas le changer de *Unlimiteddata* en *Metereddata*.

> [!IMPORTANT]
> Votre circuit ExpressRoute est facturé à partir de l’émission d'une clé de service. Effectuez cette opération seulement quand le fournisseur de connectivité prêt à approvisionner le circuit.
> 
> 

La réponse contient la clé de service. Vous pouvez obtenir une description détaillée de tous les paramètres en exécutant la commande suivante :

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a>4. Répertorier tous les circuits ExpressRoute
Pour obtenir la liste de tous les circuits ExpressRoute que vous avez créés, exécutez la commande **Get-AzureRmExpressRouteCircuit** :

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

La réponse ressemble à ce qui suit :

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

Vous pouvez récupérer ces informations à tout moment à l’aide de l’applet de commande `Get-AzureRmExpressRouteCircuit` . Un appel effectué sans paramètre répertorie tous les circuits. Votre clé de service apparaît dans le champ *ServiceKey* :

```powershell
Get-AzureRmExpressRouteCircuit
```


La réponse ressemble à ce qui suit :

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


Vous pouvez obtenir une description détaillée de tous les paramètres en exécutant la commande suivante :

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-the-service-key-to-your-connectivity-provider-for-provisioning"></a>5. Envoyer la clé de service à votre fournisseur de connectivité pour l’approvisionnement
*ServiceProviderProvisioningState* fournit des informations sur l’état actuel de l’approvisionnement du côté du fournisseur de service. Le statut indique l’état du côté Microsoft. Pour plus d’informations sur les états d’approvisionnement des circuits, consultez [Flux de travail](expressroute-workflows.md#expressroute-circuit-provisioning-states).

Quand vous créez un circuit ExpressRoute, ce circuit affiche l’état suivant :

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



Le circuit passe à l’état suivant quand le fournisseur de connectivité est sur le point de l’activer pour vous :

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

Pour pouvoir être utilisé, un circuit ExpressRoute doit être dans l’état suivant :

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-the-status-and-the-state-of-the-circuit-key"></a>6. Vérifier régulièrement le statut et l’état de la clé du circuit
La vérification du statut et de l’état de la clé du circuit vous permet de savoir quand votre fournisseur a activé votre circuit. Une fois le circuit configuré, *ServiceProviderProvisioningState* a la valeur *Approvisionné*, comme le montre l’exemple suivant :

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


La réponse ressemble à ce qui suit :

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
Pour obtenir des instructions pas à pas, consultez l’article [Configuration du routage des circuits ExpressRoute](expressroute-howto-routing-arm.md) pour créer et modifier des homologations de circuit.

> [!IMPORTANT]
> Ces instructions s’appliquent seulement aux circuits créés avec des fournisseurs de services proposant des services de connectivité de couche 2. Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement un VPN IP, comme MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.
> 
> 

### <a name="8-link-a-virtual-network-to-an-expressroute-circuit"></a>8. Lier un réseau virtuel à un circuit ExpressRoute
Maintenant, vous devez lier un réseau virtuel à votre circuit ExpressRoute. Utilisez l’article [Liaison de réseaux virtuels à des circuits ExpressRoute](expressroute-howto-linkvnet-arm.md) quand vous travaillez avec le modèle de déploiement Resource Manager.

## <a name="getting-the-status-of-an-expressroute-circuit"></a>Récupération de l’état d’un circuit ExpressRoute
Vous pouvez récupérer ces informations à tout moment à l’aide de l’applet de commande **Get-AzureRmExpressRouteCircuit**. Un appel effectué sans paramètre répertorie tous les circuits.

```powershell
Get-AzureRmExpressRouteCircuit
```


La réponse ressemble à ce qui suit :

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


Vous pouvez obtenir des informations sur un circuit ExpressRoute spécifique en transmettant à l’appel le nom du groupe de ressources et le nom du circuit comme paramètres :

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


La réponse ressemble à ce qui suit :

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


Vous pouvez obtenir une description détaillée de tous les paramètres en exécutant la commande suivante :

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <a name="modify"></a>Modification d’un circuit ExpressRoute
Vous pouvez modifier certaines propriétés d'un circuit ExpressRoute sans affecter la connectivité.

Vous pouvez effectuer les tâches suivantes sans entraîner de temps d’arrêt :

* Activer ou désactiver le module complémentaire ExpressRoute Premium pour votre circuit ExpressRoute.
* Augmenter la bande passante de votre circuit ExpressRoute à condition que la capacité disponible sur le port le permette. La rétrogradation de la bande passante d'un circuit n'est pas prise en charge. 
* Modifiez le plan de mesure de Données limitées à Données illimitées. La modification du plan de limitation de Données illimitées à Données limitées n’est pas prise en charge.
* Vous pouvez activer et désactiver *Autoriser les opérations classiques*.

Pour plus d’informations sur les limites et les limitations, reportez-vous au [FAQ ExpressRoute](expressroute-faqs.md).

### <a name="to-enable-the-expressroute-premium-add-on"></a>Pour activer le module complémentaire ExpressRoute Premium
Vous pouvez activer le module complémentaire ExpressRoute Premium pour votre circuit existant à l’aide de l’extrait de code PowerShell suivant :

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

Les fonctionnalités du module complémentaire ExpressRoute Premium sont ainsi activées pour votre circuit. Nous commençons à vous facturer la fonctionnalité du module complémentaire Premium dès que la commande a été exécutée avec succès.

### <a name="to-disable-the-expressroute-premium-add-on"></a>Pour désactiver le module complémentaire ExpressRoute Premium
> [!IMPORTANT]
> Cette opération peut échouer si vous utilisez des ressources supérieures à ce qui est autorisé pour le circuit standard.
> 
> 

Notez les informations suivantes :

* Avant de passer du niveau Premium au niveau Standard, vous devez vérifier que le nombre de réseaux virtuels liés au circuit est inférieur à 10. Si vous ne le faites pas, votre demande de mise à jour échoue et nous appliquons les tarifs Premium.
* Vous devez dissocier tous les réseaux virtuels dans d'autres régions géopolitiques. Si vous ne le faites pas, votre demande de mise à jour échoue et nous appliquons les tarifs Premium.
* Pour l’homologation privée, votre table de routage doit comporter moins de 4 000 routages. Si la table de routage comporte plus de 4 000 routages, la session BGP s’arrête et ne sera pas réactivée tant que le nombre de préfixes publiés ne sera pas inférieur à 4 000.

Vous pouvez désactiver le module complémentaire ExpressRoute Premium dans votre circuit existant à l’aide de l’applet de commande PowerShell suivante :

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-update-the-expressroute-circuit-bandwidth"></a>Pour mettre à jour la bande passante d’un circuit ExpressRoute
Pour connaître les options de bande passante prises en charge par votre fournisseur, consultez le [FAQ ExpressRoute](expressroute-faqs.md). Vous pouvez choisir n'importe quelle taille supérieure à la taille de votre circuit existant.

> [!IMPORTANT]
> Vous devrez peut-être recréer le circuit ExpressRoute si la capacité sur le port existant est inappropriée. Vous ne pouvez pas mettre le circuit à niveau si aucune capacité supplémentaire n’est disponible à cet emplacement.
>
> Vous ne pouvez pas réduire la bande passante d’un circuit ExpressRoute sans interrompre le service. Le fait de passer à un niveau inférieur de bande passante vous oblige à annuler l’approvisionnement du circuit ExpressRoute, puis à réapprovisionner un nouveau circuit ExpressRoute.
> 

Une fois que vous avez décidé de la taille dont vous avez besoin, utilisez la commande suivante pour redimensionner votre circuit :

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


Microsoft se charge de redimensionner votre circuit. Vous devrez ensuite contacter votre fournisseur de connectivité pour qu’il mette à jour les configurations de son côté afin de refléter cette modification. Une fois cette modification apportée, nous commençons à vous facturer pour l’option de bande passante mise à jour.

### <a name="to-move-the-sku-from-metered-to-unlimited"></a>Pour modifier la référence de limité à illimité
Vous pouvez modifier la référence d'un circuit ExpressRoute à l'aide de l'extrait de code PowerShell suivant :

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="to-control-access-to-the-classic-and-resource-manager-environments"></a>Pour contrôler l'accès aux environnements classique et Resource Manager
Consultez les instructions dans [Transférer des circuits ExpressRoute du modèle de déploiement classique vers le modèle de déploiement Resource Manager](expressroute-howto-move-arm.md).  

## <a name="delete"></a>Annulation de l’approvisionnement et suppression d’un circuit ExpressRoute
Notez les informations suivantes :

* Vous devez dissocier tous les réseaux virtuels du circuit ExpressRoute. Si cette opération échoue, vérifiez si certains de vos réseaux virtuels sont liés au circuit.
* Si l’état d’approvisionnement du fournisseur de services du circuit ExpressRoute est **En cours d’approvisionnement** ou **Approvisionné**, vous devez vous mettre en relation avec votre fournisseur de services pour annuler l’approvisionnement du circuit de son côté. Nous continuons à réserver des ressources et à vous facturer jusqu’à ce que le fournisseur de services termine le désapprovisionnement du circuit et nous en avertisse.
* Si le fournisseur de services a annulé l’approvisionnement du circuit (l’état d’approvisionnement du fournisseur de services affiche la valeur **Non approvisionné**), vous pouvez supprimer le circuit. Cette opération arrête la facturation du circuit.

Vous pouvez supprimer votre circuit ExpressRoute en exécutant la commande suivante :

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a>Étapes suivantes

Après avoir créé votre circuit, effectuez les tâches suivantes :

* [Créer et modifier le routage le routage pour votre circuit ExpressRoute](expressroute-howto-routing-arm.md)
* [Lier votre réseau virtuel à votre circuit ExpressRoute](expressroute-howto-linkvnet-arm.md)