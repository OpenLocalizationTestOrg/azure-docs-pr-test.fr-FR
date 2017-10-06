---
title: "Échec d’allocation de Service de cloud computing d’aaaTroubleshooting | Documents Microsoft"
description: "Résolution des problèmes d'échec d'allocation lors du déploiement de services cloud dans Azure"
services: azure-service-management, cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 529157eb-e4a1-4388-aa2b-09e8b923af74
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: dfd5cc4663ccc6ed1b27ca9df579182737363b0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-allocation-failure-when-you-deploy-cloud-services-in-azure"></a>Résolution des problèmes d'échec d'allocation lors du déploiement de services cloud dans Azure
## <a name="summary"></a>Résumé
Lorsque vous déployez des instances tooa Service de cloud computing ou que vous ajoutez un site web ou des instances de rôle de travail, Microsoft Azure alloue des ressources de calcul. Vous pouvez parfois recevoir des erreurs lorsque vous effectuez ces opérations avant même que vous atteigniez les limites d’abonnement Azure hello. Cet article explique les causes hello de certaines hello courants d’échecs d’allocation et suggère des corrections possibles. Hello informations peuvent également être utiles lorsque vous planifiez le déploiement de hello de vos services.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

### <a name="background--how-allocation-works"></a>Fonctionne de l’allocation en arrière-plan
serveurs Hello dans les centres de données Azure sont partitionnés en clusters. Une nouvelle demande d'allocation de service cloud est tentée dans plusieurs clusters. Lorsque la première instance de hello est service de cloud tooa déployé (en soit intermédiaire ou de production), que le service cloud obtient tooa épinglé cluster. Les autres déploiements pour le service de cloud computing hello se produira hello même cluster. Dans cet article, nous l’appellerons toothis en tant que « cluster tooa épinglé ». Le diagramme 1 ci-dessous illustre le cas hello d’une allocation normale qui est tentée dans plusieurs clusters ; Figure 2 illustre les cas de hello d’une allocation tooCluster épinglée de 2 car qui est hello où CS_1 de Service Cloud existant est hébergé.

![Schéma d’allocation](./media/cloud-services-allocation-failure/Allocation1.png)

### <a name="why-allocation-failure-happens"></a>Raisons de l’échec d’une allocation
Lorsqu’une demande d’allocation est épinglé tooa cluster, il existe un risque plus élevé d’échec toofind libérer des ressources, car le pool de ressources disponibles hello est limitée tooa cluster. En outre, si votre demande d’allocation est épinglé tooa cluster, mais de type hello de ressource que vous avez demandée n’est pas pris en charge par ce cluster, votre demande échoue même si le cluster de hello dispose des ressources gratuites. Diagramme 3 ci-dessous illustre les cas de hello où une allocation en attente échoue parce que le cluster de candidat uniquement hello n’a pas de libérer des ressources. Figure 4 illustre les cas de hello où une allocation en attente échoue parce que le cluster de candidat hello uniquement ne prend pas en charge hello demandé la taille de machine virtuelle, même si le cluster de hello a libérer des ressources.

![Échec d’allocation épinglée](./media/cloud-services-allocation-failure/Allocation2.png)

## <a name="troubleshooting-allocation-failure-for-cloud-services"></a>Résolution des problèmes d'échec d'allocation pour les services cloud
### <a name="error-message"></a>Message d’erreur
Vous pouvez voir hello message d’erreur suivant :

    "Azure operation '{operation id}' failed with code Compute.ConstrainedAllocationFailed. Details: Allocation failed; unable toosatisfy constraints in request. hello requested new service deployment is bound tooan Affinity Group, or it targets a Virtual Network, or there is an existing deployment under this hosted service. Any of these conditions constrains hello new deployment toospecific Azure resources. Please retry later or try reducing hello VM size or number of role instances. Alternatively, if possible, remove hello aforementioned constraints or try deploying tooa different region."

### <a name="common-issues"></a>Problèmes courants
Voici hello allocation scénarios courants qui provoquent un cluster unique d’allocation demande toobe tooa épinglés.

* Déploiement tooStaging emplacement - si un service cloud dispose d’un déploiement dans les deux emplacements, puis service de cloud entière hello est épinglé tooa spécifique du cluster.  Cela signifie que s’il existe déjà un déploiement dans l’emplacement de production hello, puis un nouveau déploiement intermédiaire ne peut être affecté Bonjour même cluster en tant qu’emplacement de production hello. Si le cluster de hello est proche de sa capacité, demande de hello peut échouer.
* Mise à l’échelle : ajout de nouvelles instances tooan service de cloud computing doit allouer Bonjour même cluster.  Les demandes de mise à l'échelle minime peuvent généralement être allouées, mais pas toujours. Si le cluster de hello est proche de sa capacité, demande de hello peut échouer.
* Groupe d’affinités - un nouveau service de cloud vide tooan de déploiement peut être alloué par fabric hello dans n’importe quel cluster dans cette région, sauf si le service de cloud computing hello est épinglé tooan affinité du groupe. Toohello déploiements même groupe d’affinités va être tentée sur hello même cluster. Si le cluster de hello est proche de sa capacité, demande de hello peut échouer.
* Réseau virtuel de groupe d’affinités - réseaux virtuels plus anciens ont été groupes tooaffinity liée à la place des régions, et les services de cloud computing dans ces réseaux virtuels serait cluster du groupe d’affinités toohello épinglés. Type de toothis de déploiements de réseau virtuel va être tentée sur le cluster de hello épinglée. Si le cluster de hello est proche de sa capacité, demande de hello peut échouer.

## <a name="solutions"></a>Solutions
1. Redéploiement tooa nouveau service cloud - cette solution est probablement toobe plus de succès car elle permet de toochoose de plateforme hello de tous les clusters dans cette région.

   * Déployez la charge de travail hello tooa nouveau service de cloud  
   * Mettre à jour hello CNAME ou un enregistrement toopoint trafic toohello nouveau service cloud
   * Une fois que le trafic de zéro va toohello ancien site, vous pouvez supprimer le service de cloud ancien hello. Cette solution ne devrait pas entraîner de temps d'arrêt.
2. Supprimer la production et la mise en lots d’emplacements : cette solution permet de conserver votre nom DNS existante, mais entraîne l’application de tooyour de temps d’arrêt.

   * Suppression de production de hello et intermédiaire des emplacements d’un service cloud existant afin que le service de cloud computing hello est vide, puis
   * Créer un nouveau déploiement dans le service cloud existant hello. Tooallocation sur tous les clusters dans la région de hello réessaye. Vérifiez le service de cloud computing hello n’est pas un groupe d’affinités de tooan liée.
3. Adresse IP réservée - cette solution permet de conserver votre adresse IP existante d’adresses, mais entraîne application tooyour de temps d’arrêt.  

   * Créez une IP réservée pour votre déploiement à l'aide de PowerShell

     ```
     New-AzureReservedIP -ReservedIPName {new reserved IP name} -Location {location} -ServiceName {existing service name}
     ```
   * Suivez #2 supérieure, rendre toospecify vraiment hello nouvelle adresse IP réservée dans CSCFG du service hello.
4. Supprimer le groupe d'affinités pour les nouveaux déploiements : les groupes d'affinités ne sont plus recommandés. Suivez les étapes de #1 ci-dessus toodeploy un nouveau service cloud. Vérifiez que le service cloud n'est pas dans un groupe d'affinités.
5. Convertir tooa réseau virtuel régional - voir [comment toomigrate à partir de groupes d’affinités tooa réseau virtuel régional (VNet)](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
