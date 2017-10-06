---
title: aaaMoving ExpressRoute des circuits de tooResource classique Manager | Documents Microsoft
description: "Cette page fournit une vue d’ensemble de ce que vous devez tooknow sur pontage hello classique et les modèles de déploiement du Gestionnaire de ressources hello."
documentationcenter: na
services: expressroute
author: ganesr
manager: carmonm
editor: 
ms.assetid: bdf01217-1a98-4ec0-a08e-d84fd37f78af
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: ganesr
ms.openlocfilehash: c901d2cda01aec409b528d29fc937ac6afaea511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="moving-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model"></a>Déplacement des circuits ExpressRoute à partir de toohello classique de hello modèle de déploiement de gestionnaire de ressources
Cet article fournit une vue d’ensemble de sa signification toomove un circuit ExpressRoute d’Azure à partir de toohello classique de hello modèle de déploiement Azure Resource Manager.

Vous pouvez utiliser un seul ExpressRoute circuit tooconnect toovirtual des réseaux qui sont déployés dans hello classique et les modèles de déploiement du Gestionnaire de ressources hello. Un circuit ExpressRoute, quelle que soit la façon dont il est créé, pouvez maintenant lier des réseaux de toovirtual entre les deux modèles de déploiement.

![Un circuit ExpressRoute qui établit un lien entre les deux modèles de déploiement toovirtual réseaux](./media/expressroute-move/expressroute-move-1.png)

## <a name="expressroute-circuits-that-are-created-in-hello-classic-deployment-model"></a>Circuits ExpressRoute qui sont créés dans le modèle de déploiement classique de hello
Circuits ExpressRoute qui sont créés dans le modèle de déploiement classique hello doivent toobe déplacé toohello Gestionnaire de ressources du déploiement modèle premier tooenable connectivité tooboth hello classique et hello Gestionnaire de ressources modèles de déploiement. La migration d’une connexion n’entraîne ni perte ni interruption de la connectivité. Tous les liens réseau circuit-à-virtuel dans le modèle de déploiement classique hello (dans hello même abonnement et entre abonnements) sont conservés.

Après que le déplacement de hello est terminée avec succès, hello circuit ExpressRoute recherche, effectue et estime exactement comme un circuit ExpressRoute qui a été créé dans le modèle de déploiement du Gestionnaire de ressources hello. Vous pouvez maintenant créer des connexions toovirtual réseaux dans le modèle de déploiement du Gestionnaire de ressources hello.

Lorsqu’un circuit ExpressRoute a été déplacé toohello modèle de déploiement de gestionnaire de ressources, vous pouvez gérer le cycle de vie hello Hello circuit ExpressRoute uniquement à l’aide du modèle de déploiement du Gestionnaire de ressources hello. Cela signifie que vous pouvez effectuer des opérations comme l’ajout, la mise à jour/suppression des homologations, mise à jour des propriétés de circuit (comme la bande passante, référence (SKU) et le type de facturation) et la suppression des circuits uniquement dans le modèle de déploiement du Gestionnaire de ressources hello. Consultez la section toohello ci-dessous sur les circuits créés dans le modèle de déploiement Resource Manager hello pour plus d’informations sur la façon de gérer les modèles de déploiement accès tooboth.

Vous n’avez pas de tooinvolve votre hello de tooperform de fournisseur de connectivité déplacer.

## <a name="expressroute-circuits-that-are-created-in-hello-resource-manager-deployment-model"></a>Circuits ExpressRoute qui sont créés dans le modèle de déploiement du Gestionnaire de ressources hello
Vous pouvez activer des circuits ExpressRoute sont créés dans toobe de modèle de déploiement de gestionnaire de ressources hello accessibles à partir de ces deux modèles de déploiement. Aucun circuit ExpressRoute dans votre abonnement peut être activé toobe accédé à partir de ces deux modèles de déploiement.

* Circuits ExpressRoute qui ont été créés dans le modèle de déploiement du Gestionnaire de ressources hello modèle ne sont pas accès toohello classique de déploiement par défaut.
* Circuits ExpressRoute qui ont été déplacés à partir du modèle de déploiement du Gestionnaire de ressources hello déploiement classique modèle toohello sont accessibles à partir de ces deux modèles de déploiement par défaut.
* Un circuit ExpressRoute dispose toujours de toohello Gestionnaire de ressources du déploiement modèle d’accès, qu’il a été créé dans hello Gestionnaire de ressources ou un modèle de déploiement classique. Cela signifie que vous pouvez créer des connexions créées par les réseaux toovirtual dans hello modèle de déploiement de gestionnaire de ressources en suivant les instructions sur [comment les réseaux virtuels toolink](expressroute-howto-linkvnet-arm.md).
* Modèle de déploiement classique de toohello accès est contrôlé par hello **allowClassicOperations** paramètre Bonjour circuit ExpressRoute.

> [!IMPORTANT]
> Tous les quotas sont documentées dans hello [limites de service](../azure-subscription-service-limits.md) page s’applique. Par exemple, un circuit standard peut avoir au maximum 10 connexions réseau virtuel liens/hello classique et de modèles de déploiement du Gestionnaire de ressources hello.
> 
> 

## <a name="controlling-access-toohello-classic-deployment-model"></a>Modèle de déploiement classique de contrôle accès toohello
Vous pouvez activer un seul ExpressRoute circuit toolink toovirtual des réseaux dans les deux modèles de déploiement en définissant un hello **allowClassicOperations** paramètre Hello circuit ExpressRoute.

Paramètre **allowClassicOperations** tooTRUE vous permet de toolink les réseaux virtuels à partir de ces deux toohello de modèles de déploiement circuit ExpressRoute. Vous pouvez lier des réseaux toovirtual dans le modèle de déploiement classique hello par les instructions suivantes sur [comment toolink des réseaux virtuels dans hello modèle de déploiement classique](expressroute-howto-linkvnet-classic.md). Vous pouvez lier des réseaux toovirtual dans le modèle de déploiement du Gestionnaire de ressources hello par les instructions suivantes sur [comment toolink des réseaux virtuels dans hello modèle de déploiement de gestionnaire de ressources](expressroute-howto-linkvnet-arm.md).

Paramètre **allowClassicOperations** tooFALSE blocs toohello circuit d’accès à partir du modèle de déploiement classique hello. Toutefois, toutes les liaisons de réseau virtuel dans le modèle de déploiement classique de hello sont conservés. Dans ce cas, hello circuit ExpressRoute n’est pas visible dans le modèle de déploiement classique hello.

## <a name="supported-operations-in-hello-classic-deployment-model"></a>Opérations prises en charge dans le modèle de déploiement classique de hello
Hello classiques opérations suivantes est prises en charge sur un ExpressRoute circuit lorsque **allowClassicOperations** a la valeur tooTRUE :

* Obtenir des informations sur le circuit ExpressRoute
* Réseau virtuel de création/mise à jour/get/suppression lie tooclassic des réseaux virtuels
* Créer/mettre à jour/obtenir/supprimer des autorisations de liaison de réseau virtuel pour une connectivité entre plusieurs abonnements

Vous ne pouvez effectuer hello classiques opérations suivantes lorsque **allowClassicOperations** a la valeur tooTRUE :

* Créer/mettre jour/obtenir/supprimer des homologations BGP (Border Gateway Protocol) pour les homologations privées Azure, les homologations publiques Azure et les homologations Microsoft
* Supprimer des circuits ExpressRoute

## <a name="communication-between-hello-classic-and-hello-resource-manager-deployment-models"></a>Communication entre hello classique et les modèles de déploiement du Gestionnaire de ressources hello
Hello circuit ExpressRoute agit comme un pont entre hello classique et les modèles de déploiement du Gestionnaire de ressources hello. Le trafic entre les ordinateurs virtuels dans des réseaux virtuels dans le modèle de déploiement classique hello et celles dans des réseaux virtuels dans le flux de modèle de déploiement de gestionnaire de ressources hello via ExpressRoute si les deux réseaux virtuels est lié toohello même circuit ExpressRoute.

Débit d’agrégat est limité par la capacité de débit hello de passerelle de réseau virtuel hello. Le trafic n’entre pas du fournisseur de connectivité hello ou vos réseaux dans ce cas. Flux de trafic entre les réseaux virtuels hello est entièrement contenu dans le réseau de Microsoft hello.

## <a name="access-tooazure-public-and-microsoft-peering-resources"></a>Accès tooAzure public et aux ressources d’homologation Microsoft
Vous pouvez continuer tooaccess les ressources qui sont généralement accessibles via l’homologation publique Azure et d’homologation Microsoft sans interruption.  

## <a name="whats-supported"></a>Opérations prises en charge
Cette section décrit les opérations prises en charge pour les circuits ExpressRoute :

* Vous pouvez utiliser un seul ExpressRoute circuit tooaccess réseaux virtuels qui sont déployés dans hello classique et les modèles de déploiement du Gestionnaire de ressources hello.
* Vous pouvez déplacer un circuit ExpressRoute de toohello classique de hello modèle de déploiement de gestionnaire de ressources. Après le déplacement, hello circuit ExpressRoute recherche, estime et fonctionne comme n’importe quel autre circuit ExpressRoute qui est créé dans le modèle de déploiement du Gestionnaire de ressources hello.
* Vous pouvez déplacer uniquement les circuit ExpressRoute hello. Cette opération ne permet pas de migrer les liaisons de circuit, les réseaux virtuels et les passerelles VPN.
* Lorsqu’un circuit ExpressRoute a été déplacé toohello modèle de déploiement de gestionnaire de ressources, vous pouvez gérer le cycle de vie hello Hello circuit ExpressRoute uniquement à l’aide du modèle de déploiement du Gestionnaire de ressources hello. Cela signifie que vous pouvez effectuer des opérations comme l’ajout, la mise à jour/suppression des homologations, mise à jour des propriétés de circuit (comme la bande passante, référence (SKU) et le type de facturation) et la suppression des circuits uniquement dans le modèle de déploiement du Gestionnaire de ressources hello.
* Hello circuit ExpressRoute agit comme un pont entre hello classique et les modèles de déploiement du Gestionnaire de ressources hello. Le trafic entre les ordinateurs virtuels dans des réseaux virtuels dans le modèle de déploiement classique hello et celles dans des réseaux virtuels dans le flux de modèle de déploiement de gestionnaire de ressources hello via ExpressRoute si les deux réseaux virtuels est lié toohello même circuit ExpressRoute.
* La connectivité entre abonnements prend en charge à la fois hello classique et les modèles de déploiement du Gestionnaire de ressources hello.
* Une fois que vous passez un circuit ExpressRoute de modèle de gestionnaire de ressources Azure toohello hello classique, vous pouvez [migrer hello réseaux virtuels toohello lié circuit ExpressRoute](expressroute-migration-classic-resource-manager.md).

## <a name="whats-not-supported"></a>Ce qui n'est pas pris en charge
Cette section décrit les opérations non prises en charge pour les circuits ExpressRoute :

* Gestion de cycle de vie de hello d’un circuit ExpressRoute à partir du modèle de déploiement classique hello.
* En fonction du rôle contrôle d’accès (RBAC) prise en charge pour le modèle de déploiement classique hello. Impossible d’effectuer RBAC contrôles tooa circuit dans le modèle de déploiement classique hello. N’importe quel administrateur/coadministrator d’abonnement de hello peut ou supprimer un lien circuit toohello de réseaux virtuels.

## <a name="configuration"></a>Configuration
Suivez les instructions de hello qui sont décrites dans [déplacer un circuit ExpressRoute à partir du modèle de déploiement du Gestionnaire de ressources hello classique toohello](expressroute-howto-move-arm.md).

## <a name="next-steps"></a>Étapes suivantes
* [Migrer hello réseaux virtuels toohello lié circuit ExpressRoute à partir de modèle de gestionnaire de ressources Azure hello classique toohello](expressroute-migration-classic-resource-manager.md)
* Pour plus d’informations sur les workflows, consultez [Workflows d’approvisionnement du circuit ExpressRoute et états du circuit](expressroute-workflows.md).
* tooconfigure votre connexion ExpressRoute :
  
  * [Création d’un circuit ExpressRoute](expressroute-howto-circuit-arm.md)
  * [Configuration du routage](expressroute-howto-routing-arm.md)
  * [Lier un circuit ExpressRoute de tooan réseau virtuel](expressroute-howto-linkvnet-arm.md)

