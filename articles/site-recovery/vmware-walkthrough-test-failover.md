---
title: "aaaRun un test de basculement pour VMware réplication tooAzure | Documents Microsoft"
description: "Résume les étapes hello que vous avez besoin pour l’exécution d’un test de basculement pour les ordinateurs virtuels VMware tooAzure à l’aide du service d’Azure Site Recovery hello de réplication."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a640e139-3a09-4ad8-8283-8fa92544f4c6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: bed934446f0c6940089bfae24a13de4fb1556a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-12-run-a-test-failover-tooazure-for-vmware-vms"></a>Étape 12 : Exécuter un tooAzure de basculement de test pour les ordinateurs virtuels VMware

Cet article décrit comment toorun un basculement de test à partir de VMware local virtual machines tooAzure, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.

Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Avant de commencer

Avant d’exécuter un test de basculement que nous recommandons que vous vérifiez les propriétés de machine virtuelle hello et apportez les modifications vous devez. Vous pouvez accéder à des propriétés de machine virtuelle hello dans **éléments répliqués**. Hello **Essentials** panneau affiche des informations sur les paramètres des ordinateurs et l’état.

## <a name="managed-disk-considerations"></a>Remarques relatives au disque géré

[Des disques gérés par](../virtual-machines/windows/managed-disks-overview.md) simplifier la gestion des disques pour les machines virtuelles Azure, la gestion des comptes de stockage hello associées aux disques de machine virtuelle hello. 

- Lorsque vous activez la protection pour une machine virtuelle, compte de stockage tooa réplique les données des ordinateurs virtuels. Disques gérés sont créés et attaché toohello VM uniquement en cas de basculement.
- Disques gérés peuvent être créés uniquement pour les ordinateurs virtuels déployés à l’aide du modèle de gestionnaire de ressources hello.  
- Lorsque ce paramètre est activé, seuls des groupes à haute disponibilité dans les groupes de ressources pour lesquels l’option **Utiliser des disques gérés** est activée peuvent être sélectionnés. Machines virtuelles avec des disques gérés doivent se trouver dans les groupes à haute disponibilité avec **utilisation des disques gérés par** défini trop**Oui**. Si le paramètre de hello n’est pas activé pour les machines virtuelles, haute disponibilité uniquement dans les groupes de ressources sans disques gérés activées peut être sélectionné.
- [En savoir plus](https://docs.microsoft.com/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set) sur les disques gérés et les groupes à haute disponibilité.
- Si vous utilisez pour la réplication de stockage Azure hello a été chiffrée avec le chiffrement de Service de stockage, disques gérés ne peut pas être créés pendant le basculement. Dans ce cas soit n’activer l’utilisation de disques gérés, ou désactivez la protection de machine virtuelle de hello et réactiver toouse un compte de stockage qui n’a pas le chiffrement activé. [En savoir plus](https://docs.microsoft.com/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="network-considerations"></a>Remarques relatives au réseau

Vous pouvez définir l’adresse IP de hello cible pour une machine virtuelle de Azure créé après le basculement.

- Si vous ne fournissez une adresse, hello a échoué sur l’ordinateur utilise DHCP.
- Si vous définissez une adresse qui n’est pas disponible au moment du basculement, ce dernier échoue.
- Hello même adresse IP peut servir pour le test de basculement, si l’adresse de hello est disponible dans le réseau de basculement de test hello.
- nombre de Hello de cartes réseau est dicté par taille hello que vous spécifiez pour la machine virtuelle cible hello :

     - Si nombre hello de cartes réseau sur l’ordinateur source de hello est hello identique ou inférieur au nombre de hello de cartes autorisé pour la taille de la machine cible hello, cible de hello aura hello même nombre de cartes en tant que source de hello.
     - Si nombre hello de cartes pour l’ordinateur virtuel de source hello dépasse le nombre hello autorisé pour la taille cible de hello, taille maximale de la cible hello sera utilisée.
     - Par exemple, si un ordinateur source possède deux cartes réseau et la taille de la machine cible hello prend en charge quatre, l’ordinateur cible hello aura deux cartes. Si hello source ordinateur possède deux cartes, mais hello taille cible pris en charge uniquement en charge l’un de l’ordinateur cible hello aura qu’un seul adaptateur.     
   - Si l’ordinateur virtuel de hello possède plusieurs cartes réseau qu’ils seront connectent tous toohello même réseau.
   - Si l’ordinateur virtuel de hello possède plusieurs cartes réseau, hello celui affiché dans la liste de hello devient hello *par défaut* carte réseau Bonjour machine virtuelle Azure.
 - [En savoir plus](vmware-walkthrough-network.md) sur l’adressage IP.



## <a name="view-and-modify-vm-settings"></a>Afficher et modifier des paramètres de machine virtuelle

Nous vous conseillons de vérifier les propriétés de hello d’ordinateur de source de hello avant d’exécuter un basculement.

1. Dans **éléments protégés**, cliquez sur **répliquées des éléments**, puis cliquez sur hello machine virtuelle.
2. Bonjour **répliqué élément** volet, vous pouvez voir un résumé des informations, l’état d’intégrité et derniers points de récupération disponibles hello machine virtuelle. Cliquez sur **propriétés** tooview plus en détail.
3. Dans **Calcul et réseau**, vous pouvez :
    - Modifier le nom de machine virtuelle Azure hello. nom de Hello doit respecter [conditions requises pour Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
    - Spécifier un [groupe de ressources] post-basculement.
    - Spécifiez une taille cible pour hello machine virtuelle Azure
    - Sélectionner un [groupe à haute disponibilité](../virtual-machines/windows/tutorial-availability-sets.md).
    - Spécifiez si toouse [des disques gérés par](#managed-disk-considerations). Sélectionnez **Oui**, si vous voulez tooattach disques gérés tooyour machine sur tooAzure de migration.
    - Afficher ou modifier les paramètres de réseau, y compris hello/sous-réseau du réseau dans le hello machine virtuelle Azure se trouve après le basculement et adresse IP hello qui sera assigné tooit.
4. Dans **disques**, vous pouvez voir des informations sur le système d’exploitation de hello et disques de données de hello machine virtuelle.

## <a name="run-a-test-failover"></a>Exécution d’un test de basculement

Une fois que vous avez configuré tous les éléments, exécutez un toomake de basculement de test que tout fonctionne comme prévu.

- Si vous souhaitez tooconnect tooAzure machines virtuelles à l’aide du protocole RDP après le basculement, [préparer tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - test de toofully vous avez besoin de toocopy d’Active Directory et DNS dans votre environnement de test. [En savoir plus](site-recovery-active-directory.md#test-failover-considerations).
 - Pour obtenir des informations complètes sur le test de basculement, consultez [cet article](site-recovery-test-failover-to-azure.md).
- Visionnez une courte vidéo de présentation avant de commencer :


     >[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video4-Recovery-Plan-DR-Drill-and-Failover/player]


Maintenant, exécutez un basculement :

1. toofail sur un seul ordinateur, dans **paramètres** > **répliquées des éléments**, cliquez sur la machine virtuelle de hello > **+ Test de basculement** icône.

    ![Test de basculement](./media/vmware-walkthrough-test-failover/test-failover.png)

2. toofail sur la récupération d’un plan, en **paramètres** > **les Plans de récupération**, plan de hello avec le bouton droit > **Test de basculement**. toocreate un plan de récupération, [suivez ces instructions](site-recovery-create-recovery-plans.md).  

3. Dans **Test de basculement**, sélectionnez hello réseau Azure toowhich machines virtuelles Azure est connectée après le basculement se produit.

4. Cliquez sur **OK** toobegin hello basculement. Vous pouvez suivre la progression en cliquant sur hello VM tooopen ses propriétés, ou sur hello **Test de basculement** travail dans le nom du coffre > **paramètres** > **travaux**  >  **Les tâches de récupération de site**.

5. Une fois hello basculement terminé, vous devez également être en mesure de réplica de hello toosee machine Azure s’affichent dans hello portail Azure > **virtuels**. Assurez-vous que VM hello est hello approprié, qui sa connexion réseau approprié de toohello, et qu’il s’exécute.

6. Si vous préparé pour les connexions après le basculement, vous devez être en mesure de tooconnect toohello machine virtuelle Azure.

7. Une fois que vous avez terminé, cliquez sur **basculement de test de nettoyage** sur le plan de récupération hello. Dans **Notes**, enregistrer et enregistrer toutes les observations associées au basculement de test hello. Cette opération supprimera les machines virtuelles hello qui ont été créés pendant le test de basculement.



## <a name="next-steps"></a>Étapes suivantes

- [En savoir plus](site-recovery-failover.md) sur différents types de basculement et comment toorun les.
- Si vous migrez des ordinateurs au lieu de procéder à une réplication et une restauration automatique, [lisez cet article pour en savoir plus](site-recovery-migrate-to-azure.md#migrate-on-premises-vms-and-physical-servers).
- [En savoir plus sur la restauration automatique](site-recovery-failback-azure-to-vmware.md), toofail et réplication de machines virtuelles Azure sauvegarder toohello principal sur-site local.
