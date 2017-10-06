---
title: "problèmes d’aaaDeployment pour le Forum aux questions de Microsoft Azure Cloud Services | Documents Microsoft"
description: "Cet article répertorie les hello Forum aux questions sur le déploiement pour les Services de Cloud de Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 8d67e36aa87fb5794d358e5cc235123ac7286028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problèmes de déploiement pour Azure Cloud Services : questions fréquentes (FAQ)

Cet article comprend des questions fréquentes sur les problèmes de déploiement pour [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services). Vous pouvez également consulter hello [page de taille de machine virtuelle de Services Cloud](cloud-services-sizes-specs.md) pour les informations de taille.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-does-deploying-a-cloud-service-toohello-staging-slot-sometimes-fail-with-a-resource-allocation-error-if-there-is-already-an-existing-deployment-in-hello-production-slot"></a>Pourquoi ne déployer un toohello de service cloud staging emplacement parfois échoue avec une erreur d’allocation de ressources s’il existe déjà un déploiement existant dans l’emplacement de production hello ?
Si un service cloud dispose d’un déploiement dans les deux emplacements, service de cloud entière hello est épinglé tooa spécifique. Cela signifie que s’il existe déjà un déploiement dans l’emplacement de production hello, un nouveau déploiement intermédiaire ne peut être affecté Bonjour même cluster en tant qu’emplacement de production hello.

Échecs d’allocation de se produisent lorsque le cluster hello où se trouve votre service cloud n’a pas suffisamment physique toosatisfy de ressources de calcul de votre demande de déploiement.

Pour savoir comment limiter les effets de ces échecs d’allocation, consultez [Échec d’allocation d’un service cloud : solutions](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-scaling-up-or-scaling-out-a-cloud-service-deployment-sometimes-result-in-allocation-failure"></a>Pourquoi une montée en puissance ou une augmentation de la taille des instances dans le déploiement d’un service cloud génère-t-elle parfois un échec d’allocation ?
Lorsqu’un service cloud est déployé, il obtient généralement tooa épinglé spécifique du cluster. Cela signifie que l’évolution verticale/out un cloud existant service doit allouer de nouvelles instances Bonjour même cluster. Si le cluster de hello est proche de sa capacité ou hello souhaité VM/type de taille n’est pas disponible, hello demande peut échouer.

Pour savoir comment limiter les effets de ces échecs d’allocation, consultez [Échec d’allocation d’un service cloud : solutions](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-deploying-a-cloud-service-into-an-affinity-group-sometimes-result-in-allocation-failure"></a>Pourquoi le déploiement d’un service cloud dans un groupe d’affinités provoque-t-il parfois un échec d’allocation ?
Un nouveau service de cloud vide tooan de déploiement peut être alloué par fabric hello dans n’importe quel cluster dans cette région, sauf si le service de cloud computing hello est épinglé tooan affinité du groupe. Toohello déploiements même groupe d’affinités va être tentée sur hello même cluster. Si le cluster de hello est proche de sa capacité, demande de hello peut échouer.

Pour savoir comment limiter les effets de ces échecs d’allocation, consultez [Échec d’allocation d’un service cloud : solutions](cloud-services-allocation-failures.md#solutions).

## <a name="why-does-changing-vm-size-or-adding-a-new-vm-tooan-existing-cloud-service-sometimes-result-in-allocation-failure"></a>Pourquoi la modification de taille de machine virtuelle ou l’ajout d’un service cloud existant de machines virtuelles tooan nouveau parfois entraîne Échec d’allocation ?
clusters de Hello dans un centre de données peuvent avoir différentes configurations de types d’ordinateurs (par exemple, une série, Av2 série, série D, série de Dv2, série G, série de H, etc.). Mais pas tous les clusters de hello nécessairement tous les types de hello de machines virtuelles. Par exemple, si vous essayez de tooadd une série D service de cloud tooa machine virtuelle qui est déjà déployé dans un cluster de série uniquement un, vous rencontrerez un échec d’allocation. Ceci peut également arriver si vous essayez de tailles de toochange référence (SKU) de machine virtuelle (par exemple, le passage d’une série de tooa D série A).

Pour savoir comment limiter les effets de ces échecs d’allocation, consultez [Échec d’allocation d’un service cloud : solutions](cloud-services-allocation-failures.md#solutions).

toocheck hello des tailles disponibles dans votre région, consultez [Microsoft Azure : les produits disponibles par région](https://azure.microsoft.com/regions/services).

## <a name="why-does-deploying-a-cloud-service-sometime-fail-due-toolimitsquotasconstraints-on-my-subscription-or-service"></a>Pourquoi déployer un cloud services échouent parfois toolimits/quotas/contraintes échéance sur mon abonnement ou le service ?
Déploiement d’un service cloud peut échouer si les ressources hello toobe nécessaire alloué dépassent par défaut de hello ou quota maximal autorisé pour votre service au niveau de la région/centre de données hello. Pour plus d’informations, consultez [Limites de services cloud](../azure-subscription-service-limits.md#cloud-services-limits).

Suivez également hello actuel/quota d’utilisation pour votre abonnement au portail de hello : portail Azure = > Abonnements = > \<approprié d’abonnement > = > « Utilisation + quota ».

Informations relatives à l’utilisation/la consommation des ressources peuvent également être récupérées via hello API de facturation d’Azure. Consultez [API Azure Resource Usage (version préliminaire)](../billing/billing-usage-rate-card-overview.md#azure-resource-usage-api-preview).

## <a name="how-can-i-change-hello-size-of-a-deployed-cloud-service-vm-without-redeploying-it"></a>Comment puis-je modifier taille hello d’un ordinateur virtuel de service cloud déployé sans la redéployer ?
Vous ne pouvez pas modifier la taille de machine virtuelle hello d’un service cloud déployé sans la redéployer. Hello taille de machine virtuelle est intégrée à hello CSDEF, qui peut uniquement être mis à jour avec un redéploiement.

Pour plus d’informations, consultez [comment tooupdate un service cloud](cloud-services-update-azure-service.md).

 
