---
title: "Créer et modifier un circuit ExpressRoute à l’aide du portail Azure | Microsoft Docs"
description: "Cet article décrit comment toocreate, configurer, vérifier, mettre à jour, supprimer et annuler le déploiement d’un circuit ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 68d59d59-ed4d-482f-9cbc-534ebb090613
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/07/2017
ms.author: cherylmc;ganesr
ms.openlocfilehash: 200418aed6bdebace43a2f57cf532d1c8d13cb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit"></a>Création et modification d’un circuit ExpressRoute
> [!div class="op_single_selector"]
> * [Portail Azure](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Interface de ligne de commande Azure](howto-circuit-cli.md)
> * [Vidéo - portail Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (classique)](expressroute-howto-circuit-classic.md)
>

Cet article décrit comment un circuit ExpressRoute d’Azure à l’aide de toocreate hello Azure portal et hello Azure Resource Manager modèle de déploiement. Hello suit également vous montre l’état de hello toocheck du circuit de hello, mettre à jour, supprimer et ou annuler le déploiement.


## <a name="before-you-begin"></a>Avant de commencer
* Hello de révision [conditions préalables](expressroute-prerequisites.md) et [workflows](expressroute-workflows.md) avant de commencer la configuration.
* Assurez-vous d’avoir accès toohello [portail Azure](https://portal.azure.com).
* Assurez-vous que vous disposez d’autorisations des ressources mise en réseau nouvelle toocreate. Contactez votre administrateur de compte si vous n’avez pas les autorisations appropriées hello.
* Vous pouvez [visualiser une vidéo](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit) avant de commencer par ordre toobetter comprendre les étapes hello.

## <a name="create-and-provision-an-expressroute-circuit"></a>Création et approvisionnement d’un circuit ExpressRoute
### <a name="1-sign-in-toohello-azure-portal"></a>1. Se connecter toohello portail Azure
À partir d’un navigateur, accédez à toohello [portail Azure](http://portal.azure.com) et connectez-vous avec votre compte Azure.

### <a name="2-create-a-new-expressroute-circuit"></a>2. Créez un circuit ExpressRoute
> [!IMPORTANT]
> Votre circuit ExpressRoute sera facturé dès hello, qu'une clé de service est émise. Veillez à effectuer cette opération lorsque le fournisseur de connectivité hello est circuit de hello tooprovision prêt.
> 
> 

1. Vous pouvez créer un circuit ExpressRoute en sélectionnant hello option toocreate une nouvelle ressource. Cliquez sur **nouveau** > **réseau** > **ExpressRoute**, comme indiqué dans hello suivant image :
   
    ![Création d’un circuit ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit1.png)
2. Après avoir cliqué sur **ExpressRoute**, vous verrez hello **circuit ExpressRoute de créer** panneau. Lorsque vous remplacez les valeurs hello sur ce panneau, assurez-vous que vous spécifiez un niveau de référence (SKU) hello approprié et le contrôle de données.
   
   * **niveau** détermine si ExpressRoute standard ou un module complémentaire ExpressRoute Premium est activé. Vous pouvez spécifier **Standard** tooget hello référence (SKU) standard ou **Premium** pour le module complémentaire de hello premium.
   * **Contrôle de données** détermine le type de facturation hello. Vous pouvez spécifier **Limité** pour un forfait de données limité, et **Illimité** pour un forfait de données illimité. Notez que vous pouvez modifier le type de facturation hello de **Metered** trop**illimité**, mais vous ne pouvez pas modifier le type hello de **illimité** trop**Metered**.
     
     ![Configurer le niveau de référence (SKU) hello et les données de contrôle](./media/expressroute-howto-circuit-portal-resource-manager/createcircuit2.png)

> [!IMPORTANT]
> Notez que cet emplacement d’homologation hello indique hello [emplacement physique](expressroute-locations.md) où vous sont d’homologation avec Microsoft. Il s’agit de **pas** lié trop propriété « Location », ce qui fait référence geography toohello où se trouve hello fournisseur de ressources réseau Azure. Elles ne sont pas liées, mais il est un toochoose de bonnes pratiques un emplacement d’homologation du circuit de hello du fournisseur de ressources réseau géographiquement fermer toohello. 
> 
> 

### <a name="3-view-hello-circuits-and-properties"></a>3. Affichage des circuits hello et propriétés
**Afficher tous les circuits hello**

Vous pouvez afficher tous les circuits hello que vous avez créé en sélectionnant **toutes les ressources** sur le menu de gauche hello.

![Afficher les circuits](./media/expressroute-howto-circuit-portal-resource-manager/listresource.png)

**Afficher les propriétés de hello**

    You can view hello properties of hello circuit by selecting it. On this blade, note hello service key for hello circuit. You must copy hello circuit key for your circuit and pass it down toohello service provider toocomplete hello provisioning process. hello circuit key is specific tooyour circuit.

![Afficher les propriétés](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

### <a name="4-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>4. Envoyer le fournisseur de connectivité hello service tooyour clé pour la configuration
Dans ce panneau, **état du fournisseur** fournit des informations sur l’état actuel de mise en service sur le côté du fournisseur de services hello hello. **État de circuit** fournit l’état de hello sur hello côté de Microsoft. Pour plus d’informations sur les États de configuration de circuit, consultez hello [Workflows](expressroute-workflows.md#expressroute-circuit-provisioning-states) l’article.

Lorsque vous créez un nouveau circuit ExpressRoute, circuit de hello sera Bonjour suivant l’état :

Statu du fournisseur : Non approvisionné<BR>
Statut du circuit : Activé

![Lancer le processus d’approvisionnement](./media/expressroute-howto-circuit-portal-resource-manager/viewstatus.png)

circuit de Hello modifiera toohello suivant l’état lorsque le fournisseur de connectivité hello est en cours de hello de l’activer pour vous :

Statut du fournisseur : En cours d’approvisionnement <BR>
Statut du circuit : Activé

Pour vous toobe en mesure de toouse un circuit ExpressRoute, il doit être Bonjour suivant l’état :

Statut du fournisseur : Approvisionné<BR>
Statut du circuit : Activé

### <a name="5-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>5. Vérifier régulièrement le statut de hello et état hello de clé du circuit hello
Vous pouvez afficher les propriétés de hello du circuit hello qui vous intéresse en le sélectionnant. Vérifiez hello **état du fournisseur** et assurez-vous qu’il a transféré trop**configuré** avant de continuer.

![Statut du circuit et du fournisseur](./media/expressroute-howto-circuit-portal-resource-manager/viewstatusprovisioned.png)

### <a name="6-create-your-routing-configuration"></a>6. Créer votre configuration de routage
Pour obtenir des instructions, consultez toohello [circuit ExpressRoute de configuration de routage](expressroute-howto-routing-portal-resource-manager.md) toocreate de l’article et modifier des homologations de circuit.

> [!IMPORTANT]
> Ces instructions s’appliquent uniquement à toocircuits qui sont créés avec des fournisseurs de services qui offrent des services de couche 2 de connectivité. Si vous utilisez un fournisseur de services proposant des services gérés de couche 3 (généralement un VPN IP, comme MPLS), votre fournisseur de connectivité configure et gère le routage pour vous.
> 
> 

### <a name="7-link-a-virtual-network-tooan-expressroute-circuit"></a>7. Lier un circuit ExpressRoute de tooan réseau virtuel
Ensuite, lier un circuit ExpressRoute de tooyour réseau virtuel. Hello d’utilisation [liaison virtuel réseaux tooExpressRoute circuits](expressroute-howto-linkvnet-arm.md) article lorsque vous travaillez avec un modèle de déploiement du Gestionnaire de ressources hello.

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>État de hello lors de l’obtention d’un circuit ExpressRoute
Vous pouvez afficher l’état hello d’un circuit en la sélectionnant. 

![Statut d’un circuit ExpressRoute](./media/expressroute-howto-circuit-portal-resource-manager/listproperties1.png)

## <a name="modifying-an-expressroute-circuit"></a>Modification d’un circuit ExpressRoute
Vous pouvez modifier certaines propriétés d'un circuit ExpressRoute sans affecter la connectivité.

Vous pouvez effectuer hello suivant sans interruption de service :

* Activer ou désactiver le module complémentaire ExpressRoute Premium pour votre circuit ExpressRoute.
* La bande passante de hello augmentation de votre circuit ExpressRoute fourni la capacité est disponible sur le port hello. Notez que la bande passante hello d’un circuit de rétrogradation n’est pas pris en charge. 
* Modifier hello plan à partir de données de limitées tooUnlimited données de contrôle. Notez ce plan de contrôle hello modification à partir de tooMetered données illimité que données ne sont pas pris en charge.
* Vous pouvez activer et désactiver *Autoriser les opérations classiques*.

Pour plus d’informations sur les limites et limitations, consultez toohello [FAQ sur ExpressRoute](expressroute-faqs.md).

toomodify un circuit ExpressRoute, cliquez sur hello **Configuration** comme indiqué dans la figure ci-dessous hello.

![Modifier le circuit](./media/expressroute-howto-circuit-portal-resource-manager/modifycircuit.png)

Vous pouvez modifier la bande passante hello, référence (SKU), modèle de facturation et autoriser des opérations classiques dans le panneau de configuration hello.

> [!IMPORTANT]
> Vous avez peut-être circuit ExpressRoute de hello toorecreate si la capacité inadéquate est sur le port existant hello. Vous ne peut pas mettre à niveau de circuit de hello si aucune capacité supplémentaire n’est disponible à cet emplacement.
>
> Vous ne pouvez pas réduire la bande passante hello d’un circuit ExpressRoute sans interruption de service. Rétrogradation de la bande passante vous oblige le circuit ExpressRoute de hello toodeprovision et puis reconfigurez un circuit ExpressRoute de nouveau.
> 
> Désactiver un module complémentaire premium opération peut échouer si vous utilisez des ressources qui sont supérieures à ce qui est autorisé pour le circuit de standard hello.
> 
> 

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Annulation de l’approvisionnement et suppression d’un circuit ExpressRoute
Vous pouvez supprimer votre circuit ExpressRoute en sélectionnant hello **supprimer** icône. Notez hello suivantes :

* Vous devez supprimer le lien de tous les réseaux virtuels à partir de hello circuit ExpressRoute. Si cette opération échoue, vérifiez si les réseaux virtuels sont liés toohello circuit.
* Si le fournisseur de service du circuit ExpressRoute hello état d’approvisionnement est **Provisioning** ou **configuré** vous devez collaborer avec votre circuit de hello toodeprovision service fournisseur de leur côté. Nous allons continuer tooreserve ressources et vous facturer jusqu'à ce que le fournisseur de services hello termine de circuit de hello désaffectation et nous avertit.
* Si le fournisseur de services hello a annulé le circuit de hello (fournisseur de services hello état d’approvisionnement est défini trop**non préparé**) vous pouvez ensuite supprimer le circuit de hello. Cela arrêtera la facturation pour le circuit de hello

## <a name="next-steps"></a>Étapes suivantes
Après avoir créé votre circuit, assurez-vous que vous hello suivant :

* [Créer et modifier le routage le routage pour votre circuit ExpressRoute](expressroute-howto-routing-portal-resource-manager.md)
* [Lier votre réseau virtuel de tooyour circuit ExpressRoute](expressroute-howto-linkvnet-arm.md)

