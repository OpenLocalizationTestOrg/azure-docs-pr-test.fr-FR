---
title: "Comment tooconfigure routage (homologation) pour un circuit ExpressRoute : le Gestionnaire de ressources : Azure | Documents Microsoft"
description: "Cet article vous guide tout au long des étapes hello pour la création et l’approvisionnement hello privés, publics et homologation Microsoft d’un circuit ExpressRoute. Cet article vous explique également comment toocheck état de hello, mettre à jour ou supprimer des homologations pour votre circuit."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c2a7ed2-ae5c-4e49-81f6-77cf9f2b2ac9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: a8ca25f488dde728cb3b06cd2c91873f3069feaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit"></a>Créer et modifier l’homologation pour un circuit ExpressRoute

Cet article vous aide à créer et gérer la configuration de routage pour un circuit ExpressRoute de modèle de déploiement de gestionnaire de ressources hello à l’aide de hello portail Azure. Vous pouvez également vérifier l’état de hello, update ou delete et annuler le déploiement homologations pour un circuit ExpressRoute. Si vous souhaitez toouse une autre méthode de toowork avec votre circuit, sélectionnez un article à partir de hello suivant liste :


## <a name="configuration-prerequisites"></a>Conditions préalables à la configuration

* Assurez-vous que vous avez consulté hello [conditions préalables](expressroute-prerequisites.md) page hello [exigences routage](expressroute-routing.md) page et hello [workflows](expressroute-workflows.md) page avant de commencer la configuration.
* Vous devez disposer d’un circuit ExpressRoute actif. Suivez les instructions de hello trop[créer un circuit ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) et circuit hello activé par votre fournisseur de connectivité avant de continuer. Hello circuit ExpressRoute doit être dans un état configuré et activé pour vous toobe toorun en mesure des applets de commande hello dans les sections suivantes hello.
* Si vous envisagez de toouse un hachage de clé/MD5 partagé, être toouse que cela des deux côtés de hello tunnel et limite hello le nombre de caractères au maximum de 25 tooa.

Ces instructions s’appliquent uniquement à toocircuits créé avec les fournisseurs de services offrant des services de connectivité de couche 2. Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement un VPN IP, comme MPLS), votre fournisseur de connectivité configure et gère le routage pour vous. 

> [!IMPORTANT]
> Nous n’effectuent pas homologations configurées par les fournisseurs de services via le portail de gestion des services hello. Nous travaillons sur la prochaine activation de cette fonctionnalité. Contactez votre fournisseur de services avant de configurer des homologations BGP.
> 
> 

Vous pouvez configurer une, deux ou les trois homologations (privée Azure, publique Azure et Microsoft) pour un circuit ExpressRoute. Vous pouvez configurer les homologations dans l’ordre de votre choix. Toutefois, il se peut que vous devez vous assurer que vous terminez configuration hello de chacun d’eux à la fois d’homologation.

## <a name="azure-private-peering"></a>Homologation privée Azure

Cette section vous permet de créer, obtenir, mettre à jour et supprimer hello Azure configuration d’homologation privée pour un circuit ExpressRoute.

### <a name="toocreate-azure-private-peering"></a>toocreate l’homologation privée Azure

1. Configurer le circuit ExpressRoute de hello. Vous assurer que circuit de hello est entièrement configuré par le fournisseur de connectivité hello avant de continuer.

  ![list](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Configurer une homologation privée Azure pour le circuit de hello. Assurez-vous que vous disposez des éléments suivants avant de passer aux étapes suivantes de hello de hello :

  * / 30 sous-réseau pour le lien principal de hello. sous-réseau de Hello ne doit pas faire partie d’un espace d’adressage réservé pour les réseaux virtuels.
  * / 30 sous-réseau pour le lien secondaire de hello. sous-réseau de Hello ne doit pas faire partie d’un espace d’adressage réservé pour les réseaux virtuels.
  * Un tooestablish ID de VLAN valide cette homologation sur. Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.
  * Un numéro AS pour l'homologation. Vous pouvez utiliser des numéros à 2 et 4 octets. Vous pouvez utiliser un numéro AS privé pour cette homologation. Veillez à ne pas utiliser le numéro 65515.
  * **Facultatif :** un hachage MD5 si vous choisissez toouse une.
3. Sélectionnez la ligne de d’homologation privée Azure hello, comme indiqué dans hello l’exemple suivant :

  ![private](./media/expressroute-howto-routing-portal-resource-manager/rprivate1.png)
4. Configurer l’homologation privée Azure. Hello suivant image montre un exemple de configuration :

  ![configurer l’homologation privée](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)
5. Enregistrer la configuration de hello après avoir spécifié tous les paramètres. Une fois la configuration de hello a été acceptée avec succès, vous voyez quelque chose de similaire toohello l’exemple suivant :

  ![enregistrer l’homologation privée](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooview-azure-private-peering-details"></a>tooview Azure privé d’homologation détails

Vous pouvez afficher les propriétés de hello d’une homologation privée Azure en sélectionnant hello d’homologation.

![afficher l’homologation privée](./media/expressroute-howto-routing-portal-resource-manager/rprivate3.png)

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate configuration d’homologation privée Azure

Vous pouvez sélectionner la ligne hello pour l’homologation et modifier les propriétés d’homologation hello.

![mettre à jour l’homologation privée](./media/expressroute-howto-routing-portal-resource-manager/rprivate2.png)

### <a name="toodelete-azure-private-peering"></a>toodelete l’homologation privée Azure

Vous pouvez supprimer votre configuration d’homologation en sélectionnant l’icône de suppression hello, comme indiqué dans hello suivant image :

![supprimer l’homologation privée](./media/expressroute-howto-routing-portal-resource-manager/rprivate4.png)

## <a name="azure-public-peering"></a>Homologation publique Azure

Cette section vous permet de créer, obtenir, mettre à jour et supprimer hello configuration d’homologation publique Azure pour un circuit ExpressRoute.

### <a name="toocreate-azure-public-peering"></a>toocreate l’homologation publique Azure

1. Configurer le circuit ExpressRoute. Garantissent que circuit de hello est entièrement par le fournisseur de connectivité hello avant de continuer à obtenir.

  ![énumérer l’homologation publique](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Configurer l’homologation publique Azure pour le circuit de hello. Assurez-vous que vous disposez des éléments suivants avant de passer aux étapes suivantes de hello de hello :

  * / 30 sous-réseau pour le lien principal de hello. Ce doit être un préfixe IPv4 public valide.
  * / 30 sous-réseau pour le lien secondaire de hello. Ce doit être un préfixe IPv4 public valide.
  * Un tooestablish ID de VLAN valide cette homologation sur. Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.
  * Un numéro AS pour l'homologation. Vous pouvez utiliser des numéros à 2 et 4 octets.
  * **Facultatif :** un hachage MD5 si vous choisissez toouse une.
3. Sélectionnez hello des lignes d’homologation publique Azure, comme indiqué dans hello suivant image :

  ![sélectionner la ligne d’homologation publique](./media/expressroute-howto-routing-portal-resource-manager/rpublic1.png)
4. Configurez l’homologation publique. Hello suivant image montre un exemple de configuration :

  ![Configurer l’homologation publique](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)
5. Enregistrer la configuration de hello après avoir spécifié tous les paramètres. Une fois la configuration de hello a été acceptée avec succès, vous voyez quelque chose de similaire toohello l’exemple suivant :

  ![Enregistrer la configuration d’homologation publique](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooview-azure-public-peering-details"></a>tooview Azure public d’homologation détails

Vous pouvez afficher les propriétés de hello d’homologation publique Azure en sélectionnant hello d’homologation.

![afficher les propriétés d’homologation publique](./media/expressroute-howto-routing-portal-resource-manager/rpublic3.png)

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate configuration d’homologation publique Azure

Vous pouvez sélectionner la ligne hello pour l’homologation et modifier les propriétés d’homologation hello.

![sélectionner la ligne d’homologation publique](./media/expressroute-howto-routing-portal-resource-manager/rpublic2.png)

### <a name="toodelete-azure-public-peering"></a>toodelete l’homologation publique Azure

Vous pouvez supprimer votre configuration d’homologation en sélectionnant l’icône de suppression hello, comme indiqué dans hello l’exemple suivant :

![supprimer l’homologation publique](./media/expressroute-howto-routing-portal-resource-manager/rpublic4.png)

## <a name="microsoft-peering"></a>Homologation Microsoft

Cette section vous permet de créer, obtenir, mettre à jour et supprimer la configuration d’homologation Microsoft hello pour un circuit ExpressRoute.

> [!IMPORTANT]
> Homologation Microsoft des circuits ExpressRoute qui ont été configurés préalable tooAugust 1, 2017 aura tous les préfixes de service publiés par le biais d’homologation de Microsoft hello, même si les filtres de routage ne sont pas définis. Homologation Microsoft des circuits ExpressRoute qui sont configurés sur ou après le 1er août 2017 n’aura pas de préfixes publiés jusqu'à ce qu’un filtre de routage est attaché toohello circuit. Pour plus d’informations, consultez [Configure a route filter for Microsoft peering](how-to-routefilter-powershell.md) (Configurer un filtre d’itinéraire pour l’homologation Microsoft).
> 
> 

### <a name="toocreate-microsoft-peering"></a>l’homologation de Microsoft toocreate

1. Configurer le circuit ExpressRoute. Garantissent que circuit de hello est entièrement par le fournisseur de connectivité hello avant de continuer à obtenir.

  ![énumérer l’homologation Microsoft](./media/expressroute-howto-routing-portal-resource-manager/listprovisioned.png)
2. Configurez Microsoft d’homologation pour le circuit de hello. Assurez-vous que vous avez hello suivant informations avant de continuer.

  * / 30 sous-réseau pour le lien principal de hello. Il doit s’agir d’un préfixe IPv4 public valide vous appartenant et enregistré dans un registre RIR / IRR.
  * / 30 sous-réseau pour le lien secondaire de hello. Il doit s’agir d’un préfixe IPv4 public valide vous appartenant et enregistré dans un registre RIR / IRR.
  * Un tooestablish ID de VLAN valide cette homologation sur. Ne vérifiez qu’aucune autre homologation dans le circuit de hello utilise hello même ID VLAN.
  * Un numéro AS pour l'homologation. Vous pouvez utiliser des numéros à 2 et 4 octets.
  * Publié préfixes : vous devez fournir une liste de tous les préfixes que vous prévoyez tooadvertise sur la session BGP de hello. Seuls les préfixes d'adresses IP publiques sont acceptés. Si vous envisagez un jeu de préfixes de toosend, vous pouvez envoyer une liste séparée par des virgules. Ces préfixes doivent être inscrit tooyou dans un RIR / IRR.
  * **Facultatif :** client ASN : Si vous ne les préfixes de publicité qui ne sont pas inscrit toohello d’homologation en tant que nombre, vous pouvez spécifier hello en tant que nombre toowhich ils sont inscrits.
  * Nom de Registre de routage : Vous pouvez spécifier hello RIR / IRR contre le hello comme nombre et les préfixes sont inscrits.
  * **Facultatif :** un hachage MD5 si vous choisissez toouse une.
3. Vous pouvez sélectionner hello homologation vous souhaitez tooconfigure, comme indiqué dans hello suivant exemple. Sélectionnez la ligne de d’homologation Microsoft hello.

  ![sélectionner la ligne d’homologation Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft1.png)
4. Configurez l’homologation Microsoft. Hello suivant image montre un exemple de configuration :

  ![configurer l’homologation Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft2.png)
5. Enregistrer la configuration de hello après avoir spécifié tous les paramètres.

  Si votre circuit obtient tooa 'Validation nécessaire' (comme indiqué dans l’image de hello) de l’état, vous devez ouvrir une tooshow de ticket de support preuve de possession de l’équipe de support tooour hello préfixes.

  ![Enregistrer la configuration d’homologation Microsoft](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft5.png)

  Vous pouvez ouvrir un ticket de support directement à partir de portail de hello, comme indiqué dans hello l’exemple suivant :

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft6.png)


1. Une fois la configuration de hello a été acceptée avec succès, vous voyez quelque chose de similaire toohello suivant l’image :

  ![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="tooview-microsoft-peering-details"></a>informations d’homologation de tooview Microsoft

Vous pouvez afficher les propriétés de hello d’homologation publique Azure en sélectionnant hello d’homologation.

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft3.png)

### <a name="tooupdate-microsoft-peering-configuration"></a>configuration d’homologation de tooupdate Microsoft

Vous pouvez sélectionner la ligne hello pour l’homologation et modifier les propriétés d’homologation hello.

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft7.png)

### <a name="toodelete-microsoft-peering"></a>l’homologation de Microsoft toodelete

Vous pouvez supprimer votre configuration d’homologation en sélectionnant l’icône de suppression hello, comme indiqué dans hello suivant image :

![](./media/expressroute-howto-routing-portal-resource-manager/rmicrosoft4.png)

## <a name="next-steps"></a>Étapes suivantes

Étape suivante, [lier un circuit ExpressRoute de tooan réseau virtuel](expressroute-howto-linkvnet-portal-resource-manager.md)
* Pour plus d'informations sur les workflows ExpressRoute, consultez [Workflows ExpressRoute](expressroute-workflows.md).
* Pour plus d’informations sur l’homologation du circuit, consultez [Circuits ExpressRoute et domaines de routage](expressroute-circuit-peerings.md).
* Pour plus d’informations sur l’utilisation des réseaux virtuels, consultez la page [Présentation du réseau virtuel](../virtual-network/virtual-networks-overview.md).
