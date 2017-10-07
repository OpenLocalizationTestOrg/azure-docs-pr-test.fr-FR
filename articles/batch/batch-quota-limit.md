---
title: aaaService quotas et limites pour le traitement par lots Azure | Documents Microsoft
description: "En savoir plus sur les quotas Azure Batch par défaut, les limites et les contraintes, et comment toorequest quota augmente"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6035d1c7618cfe97ebca3780e02a4ee34f54e534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="batch-service-quotas-and-limits"></a>Quotas et limites du service Batch

Comme avec d’autres services Azure, il existe des limites sur certaines ressources associées hello service Batch. La plupart de ces limites sont des quotas par défaut appliqués par Azure à l’abonnement de hello ou au niveau du compte. Cet article décrit ces paramètres par défaut, et comment vous pouvez demander une augmentation de ces quotas.

Gardez ces quotas à l’esprit lorsque vous concevez et mettez à l’échelle vos charges de travail Batch. Par exemple, si votre pool n’est pas atteindre le nombre de cibles de hello de nœuds de calcul que vous avez spécifié, vous pourrez avoir atteint limite du quota de cœurs hello pour votre compte Batch ou d’un quota de cœurs de machine virtuelle régional pour votre abonnement.

Vous pouvez exécuter plusieurs charges de travail de traitement par lots dans un seul compte de traitement par lots, ou distribuer vos charges de travail entre les comptes de traitement par lots qui se trouvent hello même abonnement, mais dans différentes régions Azure.

Si vous envisagez des charges de production toorun dans un lot, vous devrez peut-être tooincrease une ou plusieurs des quotas hello ci-dessus par défaut de hello. Si vous voulez tooraise un quota, vous pouvez ouvrir un en ligne [demande de support client](#increase-a-quota) sans frais.

> [!NOTE]
> Un quota est une limite de crédit, pas une garantie de capacité. Si vous avez des besoins de capacité à grande échelle, contactez le support Azure.
> 
> 

## <a name="resource-quotas"></a>Quotas de ressources
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a>Quotas en mode Abonnement utilisateur

Pour un compte de traitement lorsque le mode d’allocation de pool défini trop**abonnement utilisateur**, ordinateurs virtuels et autres ressources, telles que les comptes de stockage du lot, sont créés directement dans votre abonnement lorsqu’un pool est créé. quota de cœurs de traitement par lots Azure Hello n’applique pas de compte tooan créé dans ce mode. Au lieu de cela, les quotas hello dans votre abonnement pour les cœurs de calcul régional et d’autres ressources sont appliquées. Pour en savoir plus sur ces quotas, consultez [Abonnement Azure et limites, quotas et contraintes de service](../azure-subscription-service-limits.md).

Lorsque vous planifiez l’utilisation des ressources pour un compte créé dans le mode d’abonnement utilisateur, hello Remarque suivant des ressources de lot (dans les cœurs de toocompute ajout) sont requis pour toutes les machines virtuelles Linux 40 ou 20 ordinateurs virtuels de Windows :

| Ressource | Quota | Fournisseur |
| --- | ---| --- |
| Un compte de stockage | Comptes de stockage | Microsoft.Storage |
| Une seule adresse IP publique | Adresses IP publiques | Microsoft.Network | 
| Un seul réseau virtuel | Virtual Network | Microsoft.Network | 
| Un seul groupe de sécurité réseau | Groupes de sécurité réseau | Microsoft.Network | 
| Un seul jeu de mise à l’échelle de machine virtuelle | Jeux de mise à l’échelle de machine virtuelle | Microsoft.Compute | 
| Un seul équilibreur de charge | Équilibreurs de charge | Microsoft.Network | 

quota de cœurs Hello au niveau régional ou par famille de machine virtuelle doit être ensemble conséquente toohello taille de machine virtuelle requis pour votre pool de traitement par lots ou des pools :

| Quota | Fournisseur |
| --- | ---- |
| Nombre total de cœurs régionaux | Microsoft.Compute |
| … Cœurs de famille | Microsoft.Compute |



## <a name="other-limits"></a>Autres limites
| **Ressource** | **Limite maximale** |
| --- | --- |
| [Tâches simultanées](batch-parallel-node-tasks.md) par nœud de calcul |4 x nombre de cœurs de nœud |
| [Applications](batch-application-packages.md) par compte Batch |20 |
| Packages d’applications par application |40 |
| Taille de package d’application (individuel) |Environ 195 Go<sup>1</sup> |
| Taille maximale de la tâche de début | 32 768 caractères<sup>2</sup> |

<sup>1</sup> Limite Azure Storage pour la taille d’objet blob de blocs maximale<br />
<sup>2</sup> inclut les fichiers de ressources et les variables d’environnement

## <a name="view-batch-quotas"></a>Afficher les quotas Batch
Afficher les quotas de compte de votre lot Bonjour [portail Azure][portal].

1. Sélectionnez **comptes du lot** dans hello portail, puis sélectionnez du compte Batch hello vous intéresse.
2. Sélectionnez **propriétés** sur le panneau de menu du compte de traitement par lots hello.
3. panneau des propriétés Hello affiche hello **quotas** actuellement appliqué toohello du compte Batch
   
    ![Quotas de compte Batch][account_quotas]

Pour un compte de traitement par lots créé en mode d’abonnement utilisateur, hello de vue liée quotas d’abonnement Bonjour portail Azure.

1. Sélectionnez **abonnements**, puis sélectionnez l’abonnement hello que vous utilisez pour hello compte Batch.

2. Sur hello **abonnement** panneau, sélectionnez **utilisation + quotas**.



## <a name="increase-a-quota"></a>Augmenter un quota
Suivez ces toorequest étapes augmenter d’un quota de votre compte de traitement par lots ou de votre abonnement à l’aide de hello [portail Azure][portal]. type Hello d’augmentation du quota dépend du mode d’allocation de pool hello de votre compte de traitement par lots.

### <a name="increase-a-batch-cores-quota"></a>Augmenter un quota de cœurs Batch 

Si votre compte Batch a été créé dans **lot service** mode, suivez ces étapes de toorequest une augmentation du quota de cœurs par lots :

1. Sélectionnez hello **aide + support** vignette sur votre tableau de bord de portail, ou hello point d’interrogation (**?**) dans le coin supérieur droit de hello du portail de hello.
2. Sélectionnez **Nouvelle demande de support** > **De base**.
3. Sur hello **notions de base** panneau :
   
    a. **Type de problème** > **Quota**
   
    b. Sélectionnez votre abonnement.
   
    c. **Type de quota** > **Batch**
   
    d. **Plan de support** > **Support quota - Inclus**
   
    Cliquez sur **Suivant**.
4. Sur hello **problème** panneau :
   
    a. Sélectionnez un **gravité** selon tooyour [impact commercial][support_sev].
   
    b. Dans **détails**, spécifiez chaque quota que vous voulez toochange, nom du compte Batch hello et nouvelle limite de hello.
   
    Cliquez sur **Suivant**.
5. Sur hello **les informations de Contact** panneau :
   
    a. Sélectionnez une **méthode de contact préférée**.
   
    b. Vérifier et entrez les détails du contact hello requis.
   
    Cliquez sur **créer** toosubmit hello prise en charge de demande.

Une fois que vous avez envoyé votre demande de support, le support Azure vous contactera. Notez que la fin de la demande de hello peut prendre jusqu'à too2 prochains jours ouvrables.

### <a name="increase-a-subscription-cores-quota"></a>Augmenter un quota de cœurs d’abonnement

Si votre compte Batch a été créé en mode **Abonnement utilisateur** et si vous avez besoin de cœurs régionaux ou cœurs de familles de machine virtuelles supplémentaires, demandez une augmentation de quota dans votre abonnement. Pour connaître la procédure, consultez [Demandes d’augmentation du quota de base d’Azure Resource Manager](../azure-supportability/resource-manager-core-quotas-request.md).



## <a name="related-topics"></a>Rubriques connexes
* [Créer un compte Azure Batch hello portail Azure](batch-account-create-portal.md)
* [Vue d'ensemble des fonctionnalités d'Azure Batch](batch-api-basics.md)
* [Abonnement Azure et limites, quotas et contraintes de service](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
