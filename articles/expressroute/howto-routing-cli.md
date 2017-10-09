---
title: "Comment tooconfigure routage pour un circuit ExpressRoute de Azure : CLI | Documents Microsoft"
description: "Cet article vous permet de créer et de configurer l’homologation Microsoft d’un circuit ExpressRoute de hello privé et public. Cet article vous explique également comment toocheck état de hello, mettre à jour ou supprimer des homologations pour votre circuit."
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
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a>Créer et modifier le routage d’un circuit ExpressRoute à l’aide de l’interface CLI

Cet article vous aide à créer et gérer la configuration de routage pour un circuit ExpressRoute de modèle de déploiement de gestionnaire de ressources hello à l’aide de CLI. Vous pouvez également vérifier l’état de hello, update ou delete et annuler le déploiement homologations pour un circuit ExpressRoute. Si vous souhaitez toouse une autre méthode de toowork avec votre circuit, sélectionnez un article à partir de hello suivant liste :

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

* Avant de commencer, installez hello dernière version des commandes CLI de hello (version 2.0 ou version ultérieure). Pour plus d’informations sur l’installation des commandes CLI de hello, consultez [installer Azure CLI 2.0](/cli/azure/install-azure-cli).
* Assurez-vous que vous avez consulté hello [conditions préalables](expressroute-prerequisites.md), [exigences routage](expressroute-routing.md), et [workflow](expressroute-workflows.md) avant de commencer la configuration des pages.
* Vous devez disposer d’un circuit ExpressRoute actif. Suivez les instructions de hello trop[créer un circuit ExpressRoute](howto-circuit-cli.md) et circuit hello activé par votre fournisseur de connectivité avant de continuer. Hello circuit ExpressRoute doit être dans un état configuré et activé pour vous, les commandes de hello toobe toorun en mesure de cet article.

Ces instructions s’appliquent uniquement à toocircuits créé avec les fournisseurs de services offrant des services de connectivité de couche 2. Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement un VPN IP, comme MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.

Vous pouvez configurer une, deux ou les trois homologations (privée Azure, publique Azure et Microsoft) pour un circuit ExpressRoute. Vous pouvez configurer les homologations dans l’ordre de votre choix. Toutefois, il se peut que vous devez vous assurer que vous terminez configuration hello de chacun d’eux à la fois d’homologation.

## <a name="azure-private-peering"></a>Homologation privée Azure

Cette section vous permet de créer, obtenir, mettre à jour et supprimer hello Azure configuration d’homologation privée pour un circuit ExpressRoute.

### <a name="toocreate-azure-private-peering"></a>toocreate l’homologation privée Azure

1. Installer la version la plus récente de Azure CLI hello. Vous devez utiliser la version la plus récente hello Hello Azure Interface de ligne de commande (CLI). * hello de révision [conditions préalables](expressroute-prerequisites.md) et [workflows](expressroute-workflows.md) avant de commencer la configuration.

  ```azurecli
  az login
  ```

  Sélectionnez abonnement hello circuit ExpressRoute de toocreate

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Créez un circuit ExpressRoute. Suivez hello instructions toocreate un [circuit ExpressRoute](howto-circuit-cli.md) et configuré par le fournisseur de connectivité hello.

  Si votre fournisseur de connectivité propose des services de couche 3 gérés, vous pouvez demander votre tooenable de fournisseur de connectivité Azure privé d’homologation pour vous. Dans ce cas, vous n’aurez toofollow les instructions figurant dans les sections suivantes hello. Toutefois, si votre fournisseur de connectivité ne gère pas le routage, après avoir créé votre circuit, continuer votre configuration à l’aide des étapes hello.
3. Vérifiez hello ExpressRoute circuit toomake qu’il est configuré et activé également. Utilisez hello l’exemple suivant :

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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Configurer une homologation privée Azure pour le circuit de hello. Assurez-vous que vous disposez des éléments suivants avant de passer aux étapes suivantes de hello de hello :

  * / 30 sous-réseau pour le lien principal de hello. sous-réseau de Hello ne doit pas faire partie d’un espace d’adressage réservé pour les réseaux virtuels.
  * / 30 sous-réseau pour le lien secondaire de hello. sous-réseau de Hello ne doit pas faire partie d’un espace d’adressage réservé pour les réseaux virtuels.
  * Un tooestablish ID de VLAN valide cette homologation sur. Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.
  * Un numéro AS pour l'homologation. Vous pouvez utiliser des numéros à 2 et 4 octets. Vous pouvez utiliser un numéro AS privé pour cette homologation. Veillez à ne pas utiliser le numéro 65515.
  * **Facultatif :** un hachage MD5 si vous choisissez toouse une.

  Utilisez hello suivant exemple tooconfigure Azure privé d’homologation pour votre circuit :

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  Si vous choisissez toouse un hachage MD5, utilisez hello l’exemple suivant :

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Veillez à spécifier votre numéro AS comme ASN d’homologation et non pas comme ASN client.
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a>tooview Azure privé d’homologation détails

Vous pouvez obtenir les détails de configuration à l’aide de hello l’exemple suivant :

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

Hello la sortie est similaire toohello l’exemple suivant :

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate configuration d’homologation privée Azure

Vous pouvez mettre à jour une partie de la configuration de hello à l’aide de hello l’exemple suivant. Dans cet exemple, hello ID de VLAN de circuit de hello est mise à jour à partir de 100 too500.

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a>toodelete l’homologation privée Azure

Vous pouvez supprimer votre configuration d’homologation en exécutant hello l’exemple suivant :

> [!WARNING]
> Vous devez vous assurer que tous les réseaux virtuels sont dissocier hello circuit ExpressRoute avant d’exécuter cet exemple. 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a>Homologation publique Azure

Cette section vous permet de créer, obtenir, mettre à jour et supprimer hello configuration d’homologation publique Azure pour un circuit ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate l’homologation publique Azure

1. Installer la version la plus récente de Azure CLI hello. Vous devez utiliser la version la plus récente hello Hello Azure Interface de ligne de commande (CLI). * hello de révision [conditions préalables](expressroute-prerequisites.md) et [workflows](expressroute-workflows.md) avant de commencer la configuration.

  ```azurecli
  az login
  ```

  Sélectionnez l’abonnement hello pour lequel vous souhaitez le circuit ExpressRoute de toocreate.

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Créez un circuit ExpressRoute.  Suivez hello instructions toocreate un [circuit ExpressRoute](howto-circuit-cli.md) et configuré par le fournisseur de connectivité hello.

  Si votre fournisseur de connectivité propose des services gérés de couche 3, vous pouvez lui demander d’activer l’homologation privée Azure pour vous. Dans ce cas, vous n’aurez toofollow les instructions figurant dans les sections suivantes hello. Toutefois, si votre fournisseur de connectivité ne gère pas le routage, après avoir créé votre circuit, continuer votre configuration à l’aide des étapes hello.
3. Vérifiez tooensure de circuit ExpressRoute hello il est configuré et activé également. Utilisez hello l’exemple suivant :

  ```azurecli
  az network express-route list
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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Configurer l’homologation publique Azure pour le circuit de hello. Assurez-vous que vous disposez des informations suivantes avant de continuer davantage de hello.

  * / 30 sous-réseau pour le lien principal de hello. Ce doit être un préfixe IPv4 public valide.
  * / 30 sous-réseau pour le lien secondaire de hello. Ce doit être un préfixe IPv4 public valide.
  * Un tooestablish ID de VLAN valide cette homologation sur. Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.
  * Un numéro AS pour l'homologation. Vous pouvez utiliser des numéros à 2 et 4 octets.
  * **Facultatif :** un hachage MD5 si vous choisissez toouse une.

  Exécutez hello suivant exemple tooconfigure Azure public d’homologation pour votre circuit :

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  Si vous choisissez toouse un hachage MD5, utilisez hello l’exemple suivant :

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > Veillez à spécifier votre numéro AS comme ASN d’homologation et non pas comme ASN client.

### <a name="tooview-azure-public-peering-details"></a>tooview Azure public d’homologation détails

Vous pouvez obtenir les détails de configuration à l’aide de hello l’exemple suivant :

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

Hello la sortie est similaire toohello l’exemple suivant :

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate configuration d’homologation publique Azure

Vous pouvez mettre à jour une partie de la configuration de hello à l’aide de hello l’exemple suivant. Dans cet exemple, hello ID de VLAN de circuit de hello est mise à jour à partir de too600 200.

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a>toodelete l’homologation publique Azure

Vous pouvez supprimer votre configuration d’homologation en exécutant hello l’exemple suivant :

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a>Homologation Microsoft

Cette section vous permet de créer, obtenir, mettre à jour et supprimer la configuration d’homologation Microsoft hello pour un circuit ExpressRoute.

> [!IMPORTANT]
> Homologation Microsoft des circuits ExpressRoute qui ont été configurés préalable tooAugust 1, 2017 aura tous les préfixes de service publiés par le biais d’homologation de Microsoft hello, même si les filtres de routage ne sont pas définis. Homologation Microsoft des circuits ExpressRoute qui sont configurés sur ou après le 1er août 2017 n’aura pas de préfixes publiés jusqu'à ce qu’un filtre de routage est attaché toohello circuit. Pour plus d’informations, consultez [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md) (Configurer un filtre d’itinéraire pour l’homologation Microsoft).
> 
> 

### <a name="toocreate-microsoft-peering"></a>l’homologation de Microsoft toocreate

1. Installer la version la plus récente de Azure CLI hello. Utiliser hello la dernière version de hello Azure Interface de ligne de commande (CLI). * hello de révision [conditions préalables](expressroute-prerequisites.md) et [workflows](expressroute-workflows.md) avant de commencer la configuration.

  ```azurecli
  az login
  ```

  Sélectionnez l’abonnement hello pour lequel vous souhaitez le circuit ExpressRoute de toocreate.

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. Créez un circuit ExpressRoute. Suivez hello instructions toocreate un [circuit ExpressRoute](howto-circuit-cli.md) et configuré par le fournisseur de connectivité hello.

  Si votre fournisseur de connectivité propose des services de couche 3 gérés, vous pouvez demander votre tooenable de fournisseur de connectivité Azure privé d’homologation pour vous. Dans ce cas, vous n’aurez toofollow les instructions figurant dans les sections suivantes hello. Toutefois, si votre fournisseur de connectivité ne gère pas le routage, après avoir créé votre circuit, continuer votre configuration à l’aide des étapes hello.

3. Vérifiez hello ExpressRoute circuit toomake qu’il est configuré et activé également. Utilisez hello l’exemple suivant :

  ```azurecli
  az network express-route list
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
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
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

   Exécutez hello suivant exemple tooconfigure Microsoft homologation pour votre circuit :

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a>informations d’homologation de tooget Microsoft

Vous pouvez obtenir les détails de configuration à l’aide de hello l’exemple suivant :

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

Hello la sortie est similaire toohello l’exemple suivant :

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-microsoft-peering-configuration"></a>configuration d’homologation de tooupdate Microsoft

Vous pouvez mettre à jour n’importe quelle partie de la configuration de hello. Hello publiés préfixes de circuit de hello sont mis à jour à partir de too124.1.0.0/24 123.1.0.0/24 Bonjour l’exemple suivant :

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a>l’homologation de Microsoft toodelete

Vous pouvez supprimer votre configuration d’homologation en exécutant hello l’exemple suivant :

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a>Étapes suivantes

Étape suivante, [lier un circuit ExpressRoute de tooan réseau virtuel](howto-linkvnet-cli.md).

* Pour plus d'informations sur les workflows ExpressRoute, consultez [Workflows ExpressRoute](expressroute-workflows.md).
* Pour plus d’informations sur l’homologation du circuit, consultez [Circuits ExpressRoute et domaines de routage](expressroute-circuit-peerings.md).
* Pour plus d’informations sur l’utilisation des réseaux virtuels, consultez la page [Présentation du réseau virtuel](../virtual-network/virtual-networks-overview.md).