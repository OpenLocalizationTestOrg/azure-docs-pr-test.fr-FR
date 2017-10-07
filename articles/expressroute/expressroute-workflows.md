---
title: "aaaWorkflows pour la configuration d’un circuit ExpressRoute | Documents Microsoft"
description: Cette page vous guide tout au long des flux de travail hello pour la configuration des homologations et circuit ExpressRoute
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 55e0418c-e0bf-44a7-9aa1-720076df9297
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: cherylmc
ms.openlocfilehash: 8e1dfc137401e0d6d53608ae6c8de0085e182eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-workflows-for-circuit-provisioning-and-circuit-states"></a>Workflows ExpressRoute d’approvisionnement du circuit et états du circuit
Cette page vous guide de mise en service hello et routage des flux de travail de configuration à un niveau élevé.

![](./media/expressroute-workflows/expressroute-circuit-workflow.png)

Hello figure ci-dessous et les étapes correspondantes affichent hello tâches que vous devez suivre dans l’ordre toohave un ExpressRoute circuit approvisionné de bout en bout. 

1. Utilisez PowerShell tooconfigure un circuit ExpressRoute. Suivez les instructions de hello Bonjour [des circuits ExpressRoute de créer](expressroute-howto-circuit-classic.md) article pour plus d’informations.
2. Connectivité de la commande de fournisseur de services hello. Ce processus varie. Contactez votre fournisseur de connectivité pour plus d’informations sur la connectivité de tooorder.
3. Assurez-vous que le circuit de hello a été configuré correctement en vérifiant le circuit ExpressRoute de hello état via PowerShell de configuration. 
4. Configurez les domaines de routage. Si votre fournisseur de connectivité gère la couche 3 pour vous, il configurera le routage pour votre circuit. Si votre fournisseur de connectivité propose uniquement les services de couche 2, vous devez configurer le routage par indications décrites dans hello [exigences routage](expressroute-routing.md) et [configuration de routage](expressroute-howto-routing-classic.md) pages.
   
   * Activer l’homologation privée Azure, vous devez activer cette tooVMs tooconnect d’homologation / cloud services déployés dans les réseaux virtuels.
   * Activer l’homologation publique Azure - vous devez activer l’homologation publique Azure si vous souhaitez que les services de tooAzure tooconnect hébergés sur des adresses IP publiques. Il s’agit d’une exigence de tooaccess ressources Azure si vous avez choisi de routage de tooenable par défaut pour l’homologation privée Azure.
   * Activer Microsoft d’homologation - vous devez activer cette tooaccess Office 365 et Dynamics 365. 
     
     > [!IMPORTANT]
     > Vous devez vous assurer que vous utilisez un proxy distinct / bord tooconnect tooMicrosoft que celui que vous utilisez pour hello hello Internet. À l’aide de hello même bord pour ExpressRoute et hello Internet entraîne le routage asymétrique et provoquer des pannes de connexion pour votre réseau.
     > 
     > 
     
     ![](./media/expressroute-workflows/routing-workflow.png)
5. Liaison virtuel réseaux tooExpressRoute circuits - vous pouvez lier le circuit ExpressRoute de tooyour réseaux virtuels. Suivez les instructions [toolink des réseaux virtuels](expressroute-howto-linkvnet-arm.md) tooyour circuit. Ces réseaux virtuels peuvent être hello même abonnement Azure que le circuit ExpressRoute de hello ou peut être dans un autre abonnement.

## <a name="expressroute-circuit-provisioning-states"></a>États d’approvisionnement du circuit ExpressRoute
Chaque circuit ExpressRoute comporte deux états :

* État d’approvisionnement du fournisseur de service
* État

L'état représente l’état d'approvisionnement de Microsoft. Cette propriété a la valeur tooEnabled lorsque vous créez un circuit Expressroute

état d’approvisionnement Hello connectivité fournisseur représente l’état hello côté du fournisseur de connectivité hello. Il peut afficher *NotProvisioned*, *Provisioning* ou *Provisioned*. Hello circuit ExpressRoute doit être configuré pour vous toouse en mesure de toobe il.

### <a name="possible-states-of-an-expressroute-circuit"></a>États possibles d'un circuit ExpressRoute
Cette section répertorie les états possibles de hello pour un circuit ExpressRoute.

**Lors de la création**

Vous verrez le circuit ExpressRoute de hello Bonjour suivant état dès que vous exécutez circuit ExpressRoute de hello PowerShell applet de commande toocreate hello.

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


**Lorsque ce dernier est en cours de hello d’approvisionnement du circuit de hello**

Vous verrez circuit ExpressRoute de hello Bonjour suivant état dès que vous passer de fournisseur de connectivité hello service toohello clé et qu’ils ont démarré hello processus de configuration.

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled


**Lorsque ce dernier a effectué l’hello processus d’approvisionnement**

Vous verrez hello circuit ExpressRoute Bonjour suivant état dès que le fournisseur de connectivité hello terminée hello processus de configuration.

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled

Configuré et activé est hello uniquement état hello circuit peut être dans pour vous toouse en mesure de toobe il. Si vous utilisez un fournisseur de couche 2, vous pouvez configurer le routage pour votre circuit uniquement lorsqu'il est dans cet état.

**Lorsque ce dernier est mise hors service de circuit de hello**

Si vous avez demandé de circuit ExpressRoute de hello service fournisseur toodeprovision hello, vous verrez le circuit de hello définie toohello suivant état une fois fournisseur de services hello terminée hello mise hors service du processus.

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


Vous pouvez choisir d’activer toore si nécessaire, ou exécuter des applets de commande PowerShell circuit de hello toodelete.  

> [!IMPORTANT]
> Si vous exécutez hello PowerShell applet de commande toodelete circuit hello en hello ServiceProviderProvisioningState opération de hello approvisionnement ou configuré échoue. Collaborez avec votre circuit ExpressRoute de connectivité fournisseur toodeprovision hello tout d’abord, puis supprimez les circuit hello. Microsoft continuera de circuit de hello toobill jusqu'à ce que vous exécutez hello circuit de hello toodelete PowerShell applet de commande.
> 
> 

## <a name="routing-session-configuration-state"></a>État de configuration d’une session de routage
Hello état d’approvisionnement BGP permet de savoir si la session BGP de hello a été activée sur hello Microsoft edge. Hello état doit être activé pour vous toobe toouse en mesure de hello homologation.

Il est important de toocheck hello BGP en particulier pour l’homologation de Microsoft. Dans Ajout toohello BGP état d’approvisionnement, il existe un autre état appelé *publié l’état de préfixes publics*. Hello publiés préfixes publics l’état doit être dans *configuré* état, à la fois pour hello BGP session toobe haut et pour votre routage toowork de bout en bout. 

Si hello publié préfixe publique état a la valeur tooa *validation nécessitée* d’état, session BGP hello n’est pas activée, hello annoncé préfixes ne correspondait pas hello en tant que nombre dans un des registres de routage hello. 

> [!IMPORTANT]
> Si hello publié l’état de préfixes publics est en *validation manuelle* d’état, vous devez ouvrir un ticket de support avec [prise en charge Microsoft](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) et prouver que vous possédez des adresses IP hello publié le long hello associé numéro de système autonome.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* Configurez votre connexion ExpressRoute.
  
  * [Création d’un circuit ExpressRoute](expressroute-howto-circuit-arm.md)
  * [Configuration du routage](expressroute-howto-routing-arm.md)
  * [Lier un circuit ExpressRoute de tooan réseau virtuel](expressroute-howto-linkvnet-arm.md)

