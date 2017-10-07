---
title: "Créer et modifier un circuit Azure ExpressRoute : CLI | Microsoft Docs"
description: "Cet article décrit comment toocreate, configurer, vérifier, mettre à jour, supprimer et annuler le déploiement d’un circuit ExpressRoute à l’aide de CLI."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 396e325658a59afadb209bb525cbb59ac775ae6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a>Créer et modifier un circuit ExpressRoute à l’aide de l’interface de ligne de commande


Cet article décrit comment un circuit ExpressRoute d’Azure à l’aide de toocreate hello Interface de ligne de commande (CLI). Cet article vous montre également comment toocheck état de hello, mettre à jour, ou supprimer et annuler le déploiement d’un circuit. Si vous voulez toouse un toowork autre méthode avec des circuits ExpressRoute, vous pouvez sélectionner l’article de hello dans hello suivant liste :

> [!div class="op_single_selector"]
> * [Portail Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Interface de ligne de commande Azure](howto-circuit-cli.md)
> * [Vidéo - portail Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (classique)](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a>Avant de commencer

* Avant de commencer, installez hello dernière version des commandes CLI de hello (version 2.0 ou version ultérieure). Pour plus d’informations sur l’installation des commandes CLI de hello, consultez [installer Azure CLI 2.0](/cli/azure/install-azure-cli) et [prise en main Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).
* Hello de révision [conditions préalables](expressroute-prerequisites.md) et [workflows](expressroute-workflows.md) avant de commencer la configuration.

## <a name="create-and-provision-an-expressroute-circuit"></a>Création et approvisionnement d’un circuit ExpressRoute

### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a>1. Connectez-vous à tooyour compte Azure et sélectionnez votre abonnement

toobegin votre configuration, de connexion tooyour compte Azure. Utilisez hello suivant toohelp exemples que vous connectez :

```azurecli
az login
```

Vérifiez les abonnements hello pour le compte de hello.

```azurecli
az account list
```

Sélectionnez l’abonnement hello pour lequel vous souhaitez toocreate un circuit ExpressRoute.

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2. Obtenir la liste de hello de fournisseurs pris en charge, des emplacements et des bandes passantes

Avant de créer un circuit ExpressRoute, vous devez liste hello de fournisseurs de connectivité pris en charge, des emplacements et des options de bande passante. Hello CLI commande 'az réseau-express route liste prestataires de service' renvoie ces informations, vous allez utiliser dans les étapes suivantes :

```azurecli
az network express-route list-service-providers
```

réponse de Hello est similaire toohello l’exemple suivant :

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

Vérifiez hello réponse toosee si votre fournisseur de connectivité n’est répertorié. Prenez note de hello informations dont vous aurez besoin lorsque vous créez un circuit suivantes :

* Nom
* PeeringLocations
* BandwidthsOffered

Vous êtes maintenant prêt toocreate un circuit ExpressRoute.

### <a name="3-create-an-expressroute-circuit"></a>3. Création d’un circuit ExpressRoute

> [!IMPORTANT]
> Votre circuit ExpressRoute est facturé à partir du moment hello qu'une clé de service est émise. Effectuer cette opération lorsque le fournisseur de connectivité hello est circuit de hello tooprovision prêt.
> 
> 

Si vous n’avez pas déjà un groupe de ressources, vous devez en créer un avant de créer votre circuit ExpressRoute. Vous pouvez créer un groupe de ressources en exécutant hello de commande suivante :

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

Bonjour à l’exemple suivant montre comment toocreate un ExpressRoute de 200 Mbits/s de circuit via Equinix dans Silicon Valley. Si vous utilisez un autre fournisseur et des paramètres différents, utilisez ces informations quand vous créez votre requête. 

Assurez-vous que vous spécifiez un niveau de référence (SKU) correct hello et famille de référence (SKU) :

* Le niveau de référence détermine si ExpressRoute standard ou un module complémentaire ExpressRoute Premium est activé. Vous pouvez spécifier « Standard » hello tooget référence (SKU) standard ou 'Premium' pour le module complémentaire de hello premium.
* Famille de référence (SKU) détermine le type de facturation hello. Vous pouvez spécifier « Metereddata » pour définir un forfait de données limité et « Unlimiteddata » pour un forfait de données illimité. Vous pouvez modifier le type de facturation hello à partir de ' Metereddata 'too'Unlimiteddata', mais vous ne pouvez pas modifier hello type à partir de 'Unlimiteddata' too'Metereddata'.


Votre circuit ExpressRoute est facturé à partir du moment hello qu'une clé de service est émise. Bonjour à l’exemple suivant est une demande pour une nouvelle clé de service :

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

réponse de Hello contient la clé de service hello.

### <a name="4-list-all-expressroute-circuits"></a>4. Répertorier tous les circuits ExpressRoute

tooget une liste de tous les circuits ExpressRoute hello que vous avez créé, exécutez la commande de « liste d’express route az réseau » de hello. Vous pouvez récupérer ces informations à tout moment à l’aide de cette commande. toolist tous les circuits, appeler hello sans paramètres.

```azurecli
az network express-route list
```

Votre clé de service est répertorié dans hello *ServiceKey* champ de réponse de hello.

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

Vous pouvez obtenir une description détaillée de tous les paramètres de hello en exécutant la commande hello à l’aide de hello '-h' paramètre.

```azurecli
az network express-route list -h
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5. Envoyer le fournisseur de connectivité hello service tooyour clé pour la configuration

« ServiceProviderProvisioningState » fournit des informations sur l’état actuel de hello de configuration sur le côté du fournisseur de services hello. état des Hello fournit l’état de hello sur hello côté de Microsoft. Pour plus d’informations, consultez hello [article du flux de travail](expressroute-workflows.md#expressroute-circuit-provisioning-states).

Lorsque vous créez un nouveau circuit ExpressRoute, circuit de hello est Bonjour suivant l’état :

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

les modifications de circuit de Hello toohello suivant l’état lorsque le fournisseur de connectivité hello est en cours de hello de l’activer pour vous :

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

Pour vous toobe en mesure de toouse un circuit ExpressRoute, il doit être Bonjour suivant l’état :

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6. Vérifier régulièrement le statut de hello et état hello de clé du circuit hello

Vérification du statut de hello et état hello de clé du circuit hello vous permet de savoir quand votre fournisseur aura activé votre circuit. Après la configuration de circuit de hello, « ServiceProviderProvisioningState » s’affiche en tant que « Configuré », comme dans hello l’exemple suivant :

```azurecli
az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
```

réponse de Hello est similaire toohello l’exemple suivant :

```azurecli
"allowClassicOperations": false,
"authorizations": [],
"circuitProvisioningState": "Enabled",
"etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
"gatewayManagerEtag": null,
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
"location": "westus",
"name": "MyCircuit",
"peerings": [],
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup",
"serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
"serviceProviderNotes": null,
"serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
},
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a>7. Créer votre configuration de routage

Pour obtenir des instructions, consultez hello [circuit ExpressRoute de configuration de routage](howto-routing-cli.md) toocreate de l’article et modifier des homologations de circuit.

> [!IMPORTANT]
> Ces instructions s’appliquent uniquement à toocircuits qui sont créés avec des fournisseurs de services qui offrent des services de couche 2 de connectivité. Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement un VPN IP, comme MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a>8. Lier un circuit ExpressRoute de tooan réseau virtuel

Ensuite, lier un circuit ExpressRoute de tooyour réseau virtuel. Hello d’utilisation [liaison virtuel réseaux tooExpressRoute circuits](howto-linkvnet-cli.md) l’article.

## <a name="modify"></a>Modification d’un circuit ExpressRoute

Vous pouvez modifier certaines propriétés d'un circuit ExpressRoute sans affecter la connectivité. Vous pouvez apporter hello modifications sans interruption de service suivantes :

* Vous pouvez activer ou désactiver le module complémentaire ExpressRoute Premium pour votre circuit ExpressRoute.
* Vous pouvez augmenter la bande passante hello de votre circuit ExpressRoute autant de capacité est disponible sur le port hello. Toutefois, la bande passante hello d’un circuit de rétrogradation n’est pas pris en charge. 
* Vous pouvez modifier le plan de contrôle hello à partir de données de limitées tooUnlimited données. Toutefois, la modification hello plan à partir de tooMetered données illimité que données ne sont pas prise en charge de contrôle.
* Vous pouvez activer et désactiver *Autoriser les opérations classiques*.

Pour plus d’informations sur les limites et limitations, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md).

### <a name="tooenable-hello-expressroute-premium-add-on"></a>module complémentaire de tooenable hello ExpressRoute premium

Vous pouvez activer un module complémentaire de hello ExpressRoute premium pour votre circuit existant à l’aide de hello de commande suivante :

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

circuit de Hello dispose désormais des fonctionnalités d’un module complémentaire hello ExpressRoute premium activées. Commencer à vous de facturation pour la fonction d’un module complémentaire hello premium dès que la commande hello a été exécutée.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>module complémentaire de toodisable hello ExpressRoute premium

> [!IMPORTANT]
> Cette opération peut échouer si vous utilisez des ressources qui sont supérieures à ce qui est autorisé pour le circuit de standard hello.
> 
> 

Avant de désactiver le module complémentaire de hello ExpressRoute premium, comprendre hello suivant des critères :

* Avant de vous rétrogradez premium toostandard, il se peut que vous devez vous assurer que vous disposez de moins de 10 circuit toohello lié de réseaux virtuels. S’il y en a plus de 10, votre demande de mise à jour échoue et nous appliquons les tarifs Premium.
* Vous devez dissocier tous les réseaux virtuels dans d'autres régions géopolitiques. Si vous ne le faites pas, votre demande de mise à jour échoue et nous appliquons les tarifs Premium.
* Pour l’homologation privée, votre table de routage doit comporter moins de 4 000 routages. Si la taille de la table de routage est supérieure à 4 000 itinéraires, la session BGP de hello supprime. session de Hello ne sera pas être réactivée jusqu'à ce que le nombre de hello de préfixes publiés est inférieur à 4 000.

Vous pouvez désactiver complémentaire hello ExpressRoute pour le circuit existant de hello à l’aide de hello l’exemple suivant :

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>bande passante du circuit ExpressRoute hello tooupdate

Pour les options de bande passante hello pris en charge pour le fournisseur, vérifiez hello [FAQ sur ExpressRoute](expressroute-faqs.md). Vous pouvez choisir n’importe quelle taille supérieure à la taille de hello de votre circuit existant.

> [!IMPORTANT]
> Si la capacité inadéquate est sur le port hello existant, vous avez peut-être circuit ExpressRoute de hello toorecreate. Vous ne peut pas mettre à niveau de circuit de hello si aucune capacité supplémentaire n’est disponible à cet emplacement.
>
> Vous ne pouvez pas réduire la bande passante hello d’un circuit ExpressRoute sans interruption de service. Rétrogradation de la bande passante nécessite vous toodeprovision hello circuit ExpressRoute et puis reconfigurez un circuit ExpressRoute de nouveau.
>

Après avoir déterminé la taille de hello que vous avez besoin, utilisez hello suivant commande tooresize votre circuit :

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

Votre circuit est dimensionnée côté de Microsoft hello. Ensuite, vous devez contacter votre configurations tooupdate de fournisseur de connectivité sur leur toomatch côté cette modification. Après avoir apporté cette notification, nous commençons à vous de facturation pour l’option de la bande passante hello mis à jour.

### <a name="toomove-hello-sku-from-metered-toounlimited"></a>toomove hello référence (SKU) à partir de toounlimited limitée

Vous pouvez modifier hello référence (SKU) d’un circuit ExpressRoute à l’aide de hello l’exemple suivant :

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a>classique de toohello toocontrol accès et les environnements de gestionnaire de ressources

Passez en revue les instructions hello dans [circuits ExpressRoute de déplacer à partir du modèle de déploiement du Gestionnaire de ressources hello classique toohello](expressroute-howto-move-arm.md).

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Annulation de l’approvisionnement et suppression d’un circuit ExpressRoute

toodeprovision et supprimer un circuit ExpressRoute, assurez-vous que vous comprenez hello suivant des critères :

* Vous devez supprimer le lien de tous les réseaux virtuels à partir de hello circuit ExpressRoute. Si cette opération échoue, vérifiez toosee si les réseaux virtuels sont liés toohello circuit.
* Si le fournisseur de service du circuit ExpressRoute hello état d’approvisionnement est **Provisioning** ou **configuré**, vous devez collaborer avec votre circuit de hello toodeprovision service fournisseur de leur côté. Nous continuer tooreserve ressources et vous facturer jusqu'à ce que le fournisseur de services hello termine de circuit de hello désaffectation et nous avertit.
* Vous pouvez supprimer le circuit de hello si le fournisseur de services hello a annulé le circuit de hello. Lorsqu’un circuit est annulé, fournisseur de services hello état d’approvisionnement est défini trop**non préparé**. Cela arrête la facturation pour le circuit de hello.

Vous pouvez supprimer votre circuit ExpressRoute en exécutant hello de commande suivante :

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a>Étapes suivantes

Après avoir créé votre circuit, assurez-vous que vous hello tâche suivantes :

* [Créer et modifier le routage le routage pour votre circuit ExpressRoute](howto-routing-cli.md)
* [Lier votre réseau virtuel de tooyour circuit ExpressRoute](howto-linkvnet-cli.md)
