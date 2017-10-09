---
title: aaaScale quotas et limites dans votre laboratoire dans Azure DevTest Labs | Documents Microsoft
description: "Découvrez comment tooscale un laboratoire dans Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: ae624155-9181-45fa-bd2b-1983339b7e0e
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: tarcher
ms.openlocfilehash: 7fb429c0aabdfbce3a4a5aa6d9259daa2ee270d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-quotas-and-limits-in-devtest-labs"></a>Limites et quotas de mise à l’échelle dans votre laboratoire Azure DevTest Labs
Lorsque vous travaillez dans DevTest Labs, vous pouvez remarquer qu’il existe certaine toosome de limites par défaut des ressources Azure, ce qui peuvent affecter les services de DevTest Labs hello. Ces limites sont visées tooas **quotas**.

> [!NOTE]
> Hello service de DevTest Labs n’impose des quotas. Des quotas, que vous pouvez rencontrer sont contraintes par défaut de hello abonnement global Azure.

Vous pouvez utiliser chaque ressource Azure jusqu’à ce que vous ayez atteint son quota. Chaque abonnement a des quotas distincts et l’utilisation est suivie par abonnement.

Par exemple, chaque abonnement possède un quota par défaut de 20 cœurs. Par conséquent, si vous créez des machines virtuelles dans votre laboratoire avec quatre cœurs, vous pouvez uniquement créer cinq machines virtuelles. 

[Abonnement Azure et les limites de Service](https://docs.microsoft.com/azure/azure-subscription-service-limits) répertorie certaines des quotas plus courants de hello pour les ressources Azure. Hello plus couramment utilisés dans un laboratoire de ressources, et pour lequel vous pouvez rencontrer quotas, incluent cœurs de l’ordinateur virtuel, les adresses IP publiques, interface réseau, disques gérés, attribution de rôle RBAC et circuits ExpressRoute.

## <a name="view-your-usage-and-quotas"></a>Voir votre utilisation et les quotas
Ces étapes expliquent comment tooview hello quotas actuelles dans votre abonnement pour les ressources Azure spécifiques et toosee le pourcentage de chaque quota que vous avez utilisé.

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Sélectionnez **plus Services**, puis sélectionnez **facturation** à partir de la liste de hello.
1. Dans le panneau de facturation hello, sélectionnez un abonnement.
4. Sélectionnez **Utilisation + quotas**.

   ![Bouton Utilisation et quotas](./media/devtest-lab-scale-lab/devtestlab-usage-and-quotas.png)

   Hello utilisation + quotas panneau s’affiche, qui répertorie les différentes ressources disponibles dans ce pourcentage d’abonnement et hello de quota hello qui est utilisé par la ressource.

   ![Quotas et utilisation](./media/devtest-lab-scale-lab/devtestlab-view-quotas.png)

## <a name="requesting-more-resources-in-your-subscription"></a>Demander plus de ressources dans votre abonnement
Si vous atteignez une limite de quota, hello par défaut d’une ressource dans un abonnement peut être augmenter de limite maximale de tooa, comme décrit dans [abonnement Azure et limites de Service](https://docs.microsoft.com/azure/azure-subscription-service-limits).

Ces étapes vous indiquent comment toorequest un quota augmenter via hello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Sélectionnez **Autres services**, **Facturation**, puis **Utilisation + quotas**.
1. Dans l’utilisation de hello + Panneau de quotas, sélectionnez hello **demande augmenter** bouton.

   ![Bouton Demander une augmentation](./media/devtest-lab-scale-lab/devtestlab-request-increase.png)

1. toocomplete et soumettre la demande de hello, remplissez les informations de hello requis sur tous les trois onglets de hello **nouveau prend en charge la demande** formulaire.

   ![Formulaire Demander une augmentation](./media/devtest-lab-scale-lab/devtestlab-support-form.png)

[Comprendre les limites de Azure et augmentent](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests/) fournit plus d’informations sur le contact de support Azure toorequest un quota augmentation.



[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a>Étapes suivantes
* Explorer hello [galerie de modèles de DevTest Labs Azure Resource Manager QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/Samples).
