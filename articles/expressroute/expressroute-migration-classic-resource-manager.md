---
title: "Migrer des ExpressRoute associé des réseaux virtuels à partir de tooResource classique Manager : Azure : PowerShell | Documents Microsoft"
description: "Cette page décrit comment toomigrate associé des réseaux virtuels tooResource Manager après le déplacement de votre circuit."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: e64506c6909296f98c5dd23b1437bc0b81f31c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-expressroute-associated-virtual-networks-from-classic-tooresource-manager"></a>Migrer des ExpressRoute associé des réseaux virtuels à partir de tooResource classique Manager

Cet article explique comment toomigrate Azure ExpressRoute associé des réseaux virtuels à partir du modèle de déploiement du modèle toohello Azure Resource Manager hello déploiement classique après le déplacement de votre circuit ExpressRoute. 


## <a name="before-you-begin"></a>Avant de commencer
* Vérifiez que vous disposez de version la plus récente des modules d’Azure PowerShell hello hello. Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).
* Assurez-vous que vous avez consulté hello [conditions préalables](expressroute-prerequisites.md), [exigences routage](expressroute-routing.md), et [workflows](expressroute-workflows.md) avant de commencer la configuration.
* Passez en revue les informations hello qui sont fournies sous [déplacement d’un circuit ExpressRoute de tooResource classique Manager](expressroute-move.md). Assurez-vous de bien comprendre les limites de hello et limitations.
* Vérifiez que le circuit de hello est complètement opérationnel dans le modèle de déploiement classique hello.
* Assurez-vous que vous disposez d’un groupe de ressources qui a été créé dans le modèle de déploiement du Gestionnaire de ressources hello.
* Passez en revue hello suivant la documentation de la migration de la ressource :

    * [Plateforme prise en charge la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [Techniques détaillées sur la plateforme prise en charge la migration à partir de tooAzure classique Gestionnaire de ressources](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
    * [FAQ : Plateforme prise en charge la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [Passer en revue les erreurs les plus courantes de la migration et leur prévention](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="supported-and-unsupported-scenarios"></a>Scénarios pris en charge et non pris en charge

* Un circuit ExpressRoute peut être déplacé d’environnement de gestionnaire de ressources hello toohello classique sans interruption de service. Vous pouvez déplacer un circuit ExpressRoute de toohello classique de hello environnement du Gestionnaire de ressources sans interruption. Suivez les instructions de hello dans [déplacement des circuits ExpressRoute à partir du modèle de déploiement de gestionnaire de ressources hello toohello classique à l’aide de PowerShell](expressroute-howto-move-arm.md). Il s’agit d’un réseau virtuel de prérequis toomove ressources toohello connecté.
* Réseaux virtuels, les passerelles et les déploiements associés au sein du réseau virtuel de hello qui sont attaché tooan circuit ExpressRoute Bonjour même abonnement peut être migrés environnement du Gestionnaire de ressources toohello sans interruption de service. Vous pouvez suivre hello étapes décrites plus loin toomigrate ressources telles que les réseaux virtuels, les passerelles et les ordinateurs virtuels déployés dans le réseau virtuel de hello. Vous devez vous assurer que les réseaux virtuels hello sont configurés correctement avant leur migration. 
* Réseaux virtuels, les passerelles et les déploiements associés au sein du réseau virtuel hello qui ne sont pas dans hello même abonnement comme hello circuit ExpressRoute nécessiter la migration de hello toocomplete des temps d’arrêt. Hello dernière section du document de hello décrit hello étapes toobe suivi toomigrate ressources.
* Un réseau virtuel doté d’une passerelle ExpressRoute et d’une passerelle VPN ne peut pas être migré.

## <a name="move-an-expressroute-circuit-from-classic-tooresource-manager"></a>Déplacer un circuit ExpressRoute de tooResource classique Manager
Vous devez déplacer un circuit ExpressRoute de toohello classique de hello environnement Gestionnaire de ressources avant d’essayer de toomigrate des ressources qui sont attachés circuit ExpressRoute de toohello. tooaccomplish cette tâche, consultez hello suivant des articles :

* Passez en revue les informations hello qui sont fournies sous [déplacement d’un circuit ExpressRoute de tooResource classique Manager](expressroute-move.md).
* [Déplacer un circuit de tooResource classique Manager à l’aide d’Azure PowerShell](expressroute-howto-move-arm.md).
* Utilisez le portail de gestion des services Azure hello. Vous pouvez suivre les flux de travail hello trop[créer un circuit ExpressRoute nouveau](expressroute-howto-circuit-portal-resource-manager.md) et sélectionnez l’option d’importation hello. 

Cette opération n’implique pas de temps d’arrêt. Vous pouvez continuer tootransfer des données entre votre site et de Microsoft pour la migration de hello est en cours d’exécution.

## <a name="migrate-virtual-networks-gateways-and-associated-deployments"></a>Migrer des réseaux virtuels, des passerelles et les déploiements associés

Hello procédure vous suivez toomigrate varie selon que vos ressources sont Bonjour même abonnement, des abonnements différents ou les deux.

### <a name="migrate-virtual-networks-gateways-and-associated-deployments-in-hello-same-subscription-as-hello-expressroute-circuit"></a>Migrer des passerelles, des réseaux virtuels et les déploiements associés dans hello même abonnement que hello circuit ExpressRoute
Cette section décrit hello étapes toobe suivi toomigrate un réseau virtuel, la passerelle et les déploiements associés dans hello même abonnement que hello circuit ExpressRoute. Cette migration n’implique aucun temps d’arrêt. Vous pouvez continuer à toouse toutes les ressources via le processus de migration hello. plan de gestion Hello est verrouillée pendant la migration de hello. 

1. Assurez-vous que le circuit ExpressRoute de hello ont été déplacée à partir de l’environnement de gestionnaire de ressources hello toohello classique.
2. Assurez-vous que ce réseau virtuel hello a été préparé correctement pour la migration de hello.
3. Inscrivez votre abonnement pour la migration de ressources. tooregister votre abonnement pour la migration de la ressource, hello utilisation suivante extrait de code PowerShell :

  ```powershell 
  Select-AzureRmSubscription -SubscriptionName <Your Subscription Name>
  Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  ```
4. Effectuez la validation, la préparation et la migration. réseau virtuel toomove hello hello utilisation suivante extrait de code PowerShell :

  ```powershell
  Move-AzureVirtualNetwork -Prepare $vnetName  
  Move-AzureVirtualNetwork -Commit $vnetName
  ```

  Vous pouvez également annuler la migration en exécutant hello suivant l’applet de commande PowerShell :

  ```powershell
  Move-AzureVirtualNetwork -Abort $vnetName
  ```

## <a name="next-steps"></a>Étapes suivantes
* [Plateforme prise en charge la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [Techniques détaillées sur la plateforme prise en charge la migration à partir de tooAzure classique Gestionnaire de ressources](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
* [FAQ : Plateforme prise en charge la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [Passer en revue les erreurs les plus courantes de la migration et leur prévention](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
