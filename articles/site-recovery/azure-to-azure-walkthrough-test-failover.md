---
title: "aaaRun un test de basculement pour la réplication de machine virtuelle Azure avec Azure Site Recovery | Documents Microsoft"
description: "Résume les étapes hello que vous avez besoin pour exécuter un test de basculement pour les machines virtuelles Azure réplication tooanother région Azure à l’aide de hello Azure Site Recovery service."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: e15c1b0c-5d75-4fdf-acb0-e61def9e9339
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: c1f765aa94c59dd70b33317ebbcd04beb7977969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-run-a-test-failover-for-azure-vm-replication"></a>Étape 6 : Exécuter un test de basculement pour la réplication des machines virtuelles Azure

Une fois que vous avez activé la réplication pour la machine virtuelle Azure (VM), suivez les étapes de hello dans cet article, toorun test de basculement à partir d’une région Azure tooanother, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.

- Lorsque vous avez terminé l’article de hello, vous devez avoir vérifié avec un test de basculement, qu’au moins une machine virtuelle de Azure peut basculer tooyour de région Azure secondaire. 
- Valider les commentaires en bas de hello de cet article, ou poser des questions dans hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

>[!NOTE]
>
> La réplication de machines virtuelles Azure est actuellement disponible en préversion.


## <a name="before-you-start"></a>Avant de commencer

- Avant d’exécuter un test de basculement, nous vous recommandons de vérifier les propriétés d’ordinateurs virtuels hello et d’apporter des modifications, que vous devez. Vous pouvez accéder à des propriétés de machine virtuelle hello dans **éléments répliqués**. Hello **Essentials** panneau affiche des informations sur les paramètres des ordinateurs et l’état.
- Nous vous recommandons d’utiliser un réseau distinct de la machine virtuelle Azure pour le test de basculement hello et pas hello réseau (par défaut ou personnalisé) qui a été configuré pour le basculement de production.
- Hello test basculement échoue sur les machines virtuelles Azure (et leur stockage) toohello région Azure secondaire. Il ne réplique aucune ressource ou application dépendante. Si les applications s’exécutant sur ayant échoué sur les machines virtuelles sont dépendantes d’autres ressources, telles qu’Active Directory ou DNS, vous devez tooreplicate trop, si elles ne sont pas déjà disponibles dans votre région secondaire. [En savoir plus](site-recovery-test-failover-to-azure.md#prepare-active-directory-and-dns)
- Si vous voulez tooaccess répliquer des machines virtuelles après basculement à partir d’un site local, vous devez trop[préparer tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) toothese machines virtuelles.

## <a name="run-a-test-failover"></a>Exécution d’un test de basculement

1. Dans **paramètres** > **répliquées des éléments**, cliquez sur la machine virtuelle de hello **+ Test de basculement** icône. 

2. Dans **Test de basculement**, sélectionnez un toouse de point de récupération pour le basculement hello :

    - **Dernier traitement**: échoue hello machine virtuelle sur toohello dernier point de récupération qui a été traitée par le service de récupération de Site hello. horodatage Hello est affichée. Cette option, qui n’implique aucun traitement de données, offre un objectif de délai de récupération faible.
    - **Dernière cohérentes au niveau application**: cette option bascule toutes les machines virtuelles toohello récupération cohérents avec les applications les plus récentes. horodatage Hello est affichée. 
    - **Personnalisé** : sélectionnez n’importe quel point de récupération.
 
3. Toowhich de réseau virtuel Azure cible hello sélectionnez machines virtuelles Azure dans la région secondaire hello est connecté, après basculement hello.
4. toostart hello de basculement, cliquez sur **OK**. tootrack de progression, cliquez sur hello VM tooopen ses propriétés. Vous pouvez également cliquer sur hello **Test de basculement** travail dans le nom du coffre hello > **paramètres** > **travaux** > **les tâches de récupération de Site**.
5. Après avoir hello basculement se termine, le réplica de hello Azure VM s’affiche dans hello portail Azure > **virtuels**. Assurez-vous que cette machine virtuelle hello est la taille appropriée de hello, que sa connexion réseau approprié de toohello, et qu’il s’exécute.
6. toodelete hello machines virtuelles qui ont été créés pendant le basculement de test hello, cliquez sur **basculement de test de nettoyage** sur hello répliquées élément hello ou un plan de récupération. Dans **Notes**, enregistrer et enregistrer toutes les observations associées au basculement de test hello. 

Pour plus d’informations sur les tests de basculement, cliquez [ici](site-recovery-test-failover-to-azure.md).

## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez testé le basculement, cette procédure pas à pas est terminée. À présent, découvrez l’exécution de basculements en production :

- [En savoir plus](site-recovery-failover.md) sur différents types de basculement et comment toorun les.
- En savoir plus sur le basculement de plusieurs machines virtuelles [à l’aide d’un plan de récupération](site-recovery-create-recovery-plans.md).
- En savoir plus sur [l’utilisation des plans de récupération](site-recovery-create-recovery-plans.md).
- En savoir plus sur la [reprotection des machines virtuelles Azure](site-recovery-how-to-reprotect.md) après le basculement.

