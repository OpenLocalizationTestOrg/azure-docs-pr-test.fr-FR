---
title: "Lier un circuit ExpressRoute de tooan réseau virtuel : portail Azure | Documents Microsoft"
description: "Ce document fournit une vue d’ensemble du mode toolink virtuel réseaux des circuits tooExpressRoute (réseaux virtuels)."
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f5cb5441-2fba-46d9-99a5-d1d586e7bda4
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8bedcb11df7e30281fd439afdfb76cc67626a8f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a>Se connecter à un circuit ExpressRoute de tooan réseau virtuel
> [!div class="op_single_selector"]
> * [Portail Azure](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Interface de ligne de commande Azure](howto-linkvnet-cli.md)
> * [Vidéo - portail Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (classique)](expressroute-howto-linkvnet-classic.md)
> 

Cet article vous permet de lier des circuits ExpressRoute de tooAzure des réseaux virtuels (réseaux virtuels) à l’aide du modèle de déploiement du Gestionnaire de ressources hello et hello portail Azure. Réseaux virtuels peuvent être soit Bonjour les même abonnement, ou ils peuvent faire partie d’un autre abonnement.

## <a name="before-you-begin"></a>Avant de commencer
* Hello de révision [conditions préalables](expressroute-prerequisites.md), [exigences routage](expressroute-routing.md), et [workflows](expressroute-workflows.md) avant de commencer la configuration.
* Vous devez disposer d’un circuit ExpressRoute actif.
  
  * Suivez les instructions de hello trop[créer un circuit ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) et avoir des circuits hello activé par votre fournisseur de connectivité.
  * Vérifiez que l’homologation privée Azure est configurée pour votre circuit. Consultez hello [configurer le routage](expressroute-howto-routing-portal-resource-manager.md) article pour obtenir des instructions de routage.
  * Assurez-vous que l’homologation privée Azure est configuré et est l’homologation BGP hello entre votre réseau et de Microsoft afin que vous pouvez activer la connectivité de bout en bout.
  * Vérifiez qu’un réseau virtuel et une passerelle de réseau virtuel ont été créés et entièrement approvisionnés. Suivez les instructions de hello trop[créer une passerelle de réseau virtuel pour ExpressRoute](expressroute-howto-add-gateway-resource-manager.md). Une passerelle de réseau virtuel pour ExpressRoute utilise hello « ExpressRoute », le type de passerelle VPN pas.

* Vous pouvez lier de circuit de ExpressRoute standard too10 réseaux virtuels tooa. Tous les réseaux virtuels doivent être Bonjour même région géopolitique lors de l’utilisation d’un circuit ExpressRoute standard. 
* Vous pouvez lier un réseau virtuel en dehors de la région de hello géopolitique de hello circuit ExpressRoute ou vous connecter à un plus grand nombre de réseaux virtuels tooyour circuit ExpressRoute si vous avez activé le module complémentaire de hello ExpressRoute premium. Vérifiez hello [FAQ](expressroute-faqs.md) pour plus d’informations sur le module complémentaire de hello premium.
* Vous pouvez [visualiser une vidéo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit) avant le début toobetter comprendre les étapes hello.

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Connecter un réseau virtuel Bonjour même circuit de tooa d’abonnement

### <a name="toocreate-a-connection"></a>toocreate une connexion

> [!NOTE]
> Informations sur la configuration BGP seront afficheront pas si le fournisseur de couche 3 hello configuré votre homologations. Si votre circuit est dans un état configuré, vous devez être en mesure de toocreate connexions.
>

1. Assurez-vous que votre circuit ExpressRoute et l'homologation privée Azure ont été correctement configurés. Suivez les instructions de hello dans [créer un circuit ExpressRoute](expressroute-howto-circuit-arm.md) et [configurer le routage](expressroute-howto-routing-arm.md). Votre circuit ExpressRoute doit ressembler à hello suivant image :

    ![Capture d’écran Circuit ExpressRoute](./media/expressroute-howto-linkvnet-portal-resource-manager/routing1.png)
   
2. Vous pouvez maintenant commencer l’approvisionnement un toolink connexion votre tooyour de passerelle de réseau virtuel circuit ExpressRoute. Cliquez sur **connexion** > **ajouter** tooopen hello **ajouter une connexion** panneau, puis configurez les valeurs hello.

    ![Capture d’écran Ajouter une connexion](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub1.png)  

3. Une fois que votre connexion a été correctement configurée, votre objet de connexion affiche les informations de hello pour les connexions hello.

     ![Capture d’écran Objet de connexion](./media/expressroute-howto-linkvnet-portal-resource-manager/samesub2.png)

### <a name="toodelete-a-connection"></a>toodelete une connexion
Vous pouvez supprimer une connexion en sélectionnant hello **supprimer** icône Panneau hello pour votre connexion.

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Connecter un réseau virtuel dans un circuit de tooa autre abonnement
Vous pouvez partager un circuit ExpressRoute entre plusieurs abonnements. la figure ci-dessous Hello schématique simple de fonctionnement du partage de circuits ExpressRoute entre plusieurs abonnements.

![Connectivité entre abonnements](./media/expressroute-howto-linkvnet-portal-resource-manager/cross-subscription.png)

- Chaque hello petits clouds dans cloud volumineux de hello est utilisé toorepresent abonnements appartenant aux départements toodifferent au sein d’une organisation.
- Chacun des services hello au sein de l’organisation de hello permettre utiliser leur propre abonnement pour le déploiement de leurs services, mais elles peuvent partager un réseau local ExpressRoute circuit tooconnect tooyour précédent.
- Un seul département (dans cet exemple : informatique) peut posséder de circuit ExpressRoute de hello. Autres abonnements au sein de l’organisation de hello peuvent utiliser le circuit ExpressRoute de hello.

    > [!NOTE]
    > Frais de connectivité et de bande passante pour le circuit de hello dédié sera propriétaire du circuit ExpressRoute toohello appliqué. Tous les réseaux virtuels partagent hello même bande passante.
    > 
    >

### <a name="administration---circuit-owners-and-circuit-users"></a>Administration - propriétaires de circuit et utilisateurs de circuit

Hello propriétaire du circuit est un utilisateur autorisé de la puissance de hello ressource de circuit ExpressRoute. propriétaire du circuit Hello peut créer des autorisations qui peuvent être utilisées par les utilisateurs de circuit. Les utilisateurs de circuit sont les propriétaires du réseau virtuel qui ne sont pas dans les passerelles hello même abonnement que hello circuit ExpressRoute. Les utilisateurs du circuit peuvent échanger des autorisations (une seule autorisation par réseau virtuel).

propriétaire du circuit Hello possède les autorisations hello power toomodify et révoquer à tout moment. Révocation de des résultats d’autorisation dans toutes les connexions de la liaison en cours de suppression de l’abonnement hello dont l’accès a été révoqué.

### <a name="circuit-owner-operations"></a>Opérations du propriétaire du circuit

**toocreate une autorisation de connexion**

propriétaire du circuit Hello crée une autorisation. Cela entraîne la création de hello d’une clé d’autorisation qui peut être utilisé par un tooconnect utilisateur de circuit leur toohello de passerelles de réseau virtuel circuit ExpressRoute. Une autorisation n’est valide que pour une seule connexion.

1. Dans le panneau de ExpressRoute hello, cliquez sur **autorisations** , puis tapez un **nom** pour l’autorisation de hello et cliquez sur **enregistrer**.

    ![Autorisations](./media/expressroute-howto-linkvnet-portal-resource-manager/authorization.png)

2. Une fois l’enregistrement de la configuration hello copier hello **ID de ressource** et hello **clé d’autorisation**.

    ![Clé d’autorisation](./media/expressroute-howto-linkvnet-portal-resource-manager/authkey.png)

**toodelete une autorisation de connexion**

Vous pouvez supprimer une connexion en sélectionnant hello **supprimer** icône Panneau hello pour votre connexion.

### <a name="circuit-user-operations"></a>Opérations de l’utilisateur du circuit

utilisateur du circuit Hello a besoin d’ID de ressource hello et une clé d’autorisation du propriétaire du circuit hello. 

**tooredeem une autorisation de connexion**

1.  Cliquez sur hello **+ nouveau** bouton.

    ![Click New](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection1.png)

2.  Recherchez **« Connexion »** Bonjour Marketplace, sélectionnez-le, puis cliquez sur **créer**.

    ![Rechercher une connexion](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection2.png)

3.  Vérifiez que hello **type de connexion** est défini trop « ExpressRoute ».


4.  Renseignez les détails de hello, puis cliquez sur **OK** dans le panneau des principes de base hello.

    ![Panneau Informations de base](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection3.png)

5.  Bonjour **paramètres** panneau, sélectionnez hello **passerelle de réseau virtuel** et vérifiez hello **échanger d’autorisation** case à cocher.

6.  Entrez hello **clé d’autorisation** et hello **homologue circuit URI** et renommer les connexions hello. Cliquez sur **OK**.

    ![Panneau Paramètres](./media/expressroute-howto-linkvnet-portal-resource-manager/Connection4.png)

7. Passez en revue les informations de hello Bonjour **Résumé** panneau, cliquez sur **OK**.


**toorelease une autorisation de connexion**

Vous pouvez libérer une autorisation en supprimant la connexion hello qui établit un lien réseau virtuel du toohello circuit ExpressRoute hello.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur ExpressRoute, consultez hello [FAQ sur ExpressRoute](expressroute-faqs.md).
