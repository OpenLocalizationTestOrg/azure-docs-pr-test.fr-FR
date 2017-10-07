---
title: "recommandations de l’Assistant haute disponibilité aaaAzure | Documents Microsoft"
description: "Utilisez l’Assistant Azure tooimprove haute disponibilité de vos déploiements Azure."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 3ac75ce401271f0212d198d7a7dc75ab702b6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-high-availability-recommendations"></a>Recommandations du conseiller en matière de haute disponibilité

Azure Advisor vous aide à garantir et améliorer la continuité des activités de hello de vos applications critiques. Vous pouvez obtenir des recommandations de haute disponibilité par le Conseiller de hello **haute disponibilité** onglet du tableau de bord hello Advisor.

![Bouton de disponibilité élevée sur le tableau de bord hello Advisor](./media/advisor-high-availability-recommendations/advisor-high-availability-tab.png)


## <a name="ensure-virtual-machine-fault-tolerance"></a>Assurer la tolérance de panne des machines virtuelles

Le conseiller identifie les machines virtuelles qui ne font pas partie d’un groupe à haute disponibilité et recommande de les déplacer dans un groupe à haute disponibilité. Pour fournir des applications tooyour de redondance, nous vous recommandons de regrouper deux ou plusieurs machines virtuelles dans un ensemble de disponibilité. Cette configuration garantit que pendant un événement de maintenance planifiée ou non, au moins un ordinateur virtuel est disponible et répond aux hello machine virtuelle Azure SLA. Vous pouvez choisir soit toocreate une ensemble de disponibilité pour hello machine virtuelle ou tooadd hello machine virtuelle tooan à haute disponibilité existant.

> [!NOTE]
> Si vous choisissez une disponibilité toocreate défini, vous devez ajouter au moins une machine virtuelle plus dans celui-ci. Nous recommandons que vous regroupez deux ou plusieurs ordinateurs virtuels dans une disponibilité tooensure qui au moins un ordinateur est disponible pendant une panne.

![Recommandation d’Advisor : Pour la redondance des machines virtuelles, utilisez les groupes à haute disponibilité](./media/advisor-high-availability-recommendations/advisor-high-availability-create-availability-set.png)

## <a name="ensure-availability-set-fault-tolerance"></a>Assurer la tolérance de panne d’un groupe à haute disponibilité 

Advisor identifie les groupes à haute disponibilité qui contiennent une seule machine virtuelle et recommande d’ajouter un ou plusieurs tooit de machines virtuelles. Pour fournir des applications tooyour de redondance, nous vous recommandons de regrouper deux ou plusieurs machines virtuelles dans un ensemble de disponibilité. Cette configuration garantit que pendant un événement de maintenance planifiée ou non, au moins un ordinateur virtuel est disponible et répond aux hello machine virtuelle Azure SLA. Vous pouvez choisir soit toocreate une machine virtuelle ou toouse un ordinateur virtuel existant et tooadd il toohello à haute disponibilité.  

![Recommandation de l’Assistant : ajouter un ou plusieurs machines virtuelles toothis à haute disponibilité](./media/advisor-high-availability-recommendations/advisor-high-availability-add-vm-to-availability-set.png)


## <a name="ensure-application-gateway-fault-tolerance"></a>Assurer la tolérance de panne d’une passerelle
tooensure hello de continuité des applications critiques qui sont alimentées par les passerelles d’application Advisor identifie les instances de passerelle d’application qui ne sont pas configurés pour la tolérance de panne, et il suggère les actions de mise à jour que vous pouvez effectuer . Advisor identifie les passerelles d’application de moyenne ou grande taille à instance unique, et recommande d’ajouter au moins une instance de plus. Il identifie l’instance unique ou plusieurs passerelles petite application et recommande toomedium migration ou des références (SKU) volumineux. Assistant recommande ces tooensure actions que vos instances de passerelle d’application sont configurés toosatisfy hello actuels exigences du contrat SLA pour ces ressources.

![Recommandation d’Advisor : Déployez deux instances (ou plus) de passerelle d’application de moyenne ou grande taille](./media/advisor-high-availability-recommendations/advisor-high-availability-application-gateway.png)

## <a name="improve-hello-performance-and-reliability-of-virtual-machine-disks"></a>Améliorer les performances de hello et de la fiabilité des disques de machine virtuelle

Advisor identifie les machines virtuelles avec des disques standards et recommande la mise à niveau des disques toopremium.
 
Azure Premium Storage offre une prise en charge très performante et à faible latence des disques pour les machines virtuelles exécutant des charges de travail qui utilisent beaucoup d'E/S. Les disques de machine virtuelle qui utilisent des comptes Premium Storage stockent les données sur des disques SSD. Hello des performances optimales pour votre application, nous recommandons que vous migrez des disques de machine virtuelle nécessitant le stockage de toopremium IOPS élevées. 

Si votre disque ne nécessite pas une valeur élevée d’E/S par seconde, vous pouvez limiter les coûts en le maintenant en stockage standard. Le stockage standard stocke les données de disque des machines virtuelles sur des disques durs (HDD) au lieu de disques SSD. Vous pouvez choisir toomigrate vos disques de toopremium de disques de machine virtuelle. Les disques Premium sont pris en charge sur la plupart des références de machines virtuelles. Toutefois, dans certains cas, si vous souhaitez que les disques premium toouse, vous devrez peut-être tooupgrade votre ordinateur virtuel références (SKU).

![Recommandation de l’Assistant : améliorer la fiabilité de vos disques de machine virtuelle hello toopremium disques de la mise à niveau](./media/advisor-high-availability-recommendations/advisor-high-availability-upgrade-to-premium-disks.png)

## <a name="protect-your-virtual-machine-data-from-accidental-deletion"></a>Protégez les données de vos machines virtuelles d’une suppression accidentelle
Advisor identifie les machines virtuelles sur lesquelles la sauvegarde n’est pas activée, et recommande l’activation de la sauvegarde. Configuration de la sauvegarde de l’ordinateur virtuel garantit la disponibilité de hello de vos données critiques pour votre entreprise et offre une protection contre une suppression accidentelle ou d’endommagement.

![Recommandation de l’Assistant : configurer tooprotect sauvegarde d’ordinateur virtuel de vos données critiques](./media/advisor-high-availability-recommendations/advisor-high-availability-virtual-machine-backup.png)

## <a name="access-high-availability-recommendations-in-advisor"></a>Accéder aux recommandations en matière de haute disponibilité dans Advisor

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).

2. Dans le volet gauche de hello, cliquez sur **davantage de services**.

3. Bonjour service sous le volet de menu, **analyse et gestion**, cliquez sur **Azure Advisor**.  
 tableau de bord Hello Advisor s’affiche.

4. Tableau de bord du conseiller hello, cliquez sur hello **haute disponibilité** onglet et sélectionnez abonnement hello pour lequel vous souhaitez tooreceive recommandations.

> [!NOTE]
> tooaccess recommandations de l’Assistant, vous devez d’abord *enregistrer votre abonnement* avec l’Assistant. Un abonnement est enregistré quand un *abonnement propriétaire* lance hello hello de tableau de bord et clique sur Advisor **obtenir des recommandations** bouton. Cette opération ne doit être *exécutée qu’une seule fois*. Une fois l’abonnement de hello est enregistré, vous pouvez accéder à des recommandations de l’Assistant en tant que *propriétaire*, *collaborateur*, ou *lecteur* pour un abonnement, un groupe de ressources, ou un ressource spécifique.

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les recommandations d’Advisor, consultez :
* [Introduction tooAzure Advisor](advisor-overview.md)
* [Prise en main du conseiller](advisor-get-started.md)
* [Recommandations du conseiller en matière de coûts](advisor-performance-recommendations.md)
* [Recommandations du conseiller en matière de performances](advisor-performance-recommendations.md)
* [Recommandations du conseiller en matière de sécurité](advisor-security-recommendations.md)

