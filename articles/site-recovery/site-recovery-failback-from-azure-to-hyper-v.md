---
title: aaaFailback dans Azure Site Recovery pour les ordinateurs virtuels Hyper-v | Documents Microsoft
description: "Azure Site Recovery coordonne la réplication hello, le basculement et récupération des ordinateurs virtuels et des serveurs physiques. En savoir plus sur la restauration à partir du centre de données Azure tooon local."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 50cda9105de6b6fb23e4c62942fdaffc55c3efa4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="failback-in-site-recovery-for-hyper-v-virtual-machines"></a>Restauration automatique dans Site Recovery pour les machines virtuelles Hyper-V

Cet article décrit comment les machines virtuelles de toofailback protégée par Site Recovery.

## <a name="prerequisites"></a>Composants requis
1. Vérifiez que ce serveur d’Hyper-V/server hello site principal VMM est connecté.
2. Vous devez avoir effectué **valider** sur l’ordinateur virtuel de hello.

## <a name="why-is-there-no-button-called-failback"></a>Pourquoi n’y a-t-il pas de bouton Restauration automatique ?
Sur le portail hello, il n’existe aucun mouvement explicite, appelée la restauration automatique. La restauration automatique est une étape où vous revenez toohello principal de site. Par définition, basculement est lorsque vous basculer hello des machines virtuelles à partir de primary(on-premises) site toorecovery (Azure) et la restauration lors de la sauvegarde tooprimary aux basculer hello des machines virtuelles à partir de la récupération.

Lorsque vous démarrez un basculement, panneau de hello vous informe sur la direction hello du travail de hello. Si direction de hello tooOn site Azure, il s’agit d’une restauration automatique.

## <a name="why-is-there-only-a-planned-failover-gesture-toofailback"></a>Pourquoi y a-t-il uniquement un toofailback de mouvement du basculement planifié ?
Azure est un environnement hautement disponible et vos machines virtuelles seront toujours disponibles. La restauration automatique est une activité planifiée que vous décidez tootake un bref temps d’arrêt afin que les charges de travail hello peuvent commencer à exécuter localement à nouveau. Il ne doit y avoir aucune perte de données. Par conséquent, uniquement un mouvement de basculement planifié est disponible, qui désactiver les machines virtuelles de hello dans Azure, télécharge les modifications les plus récentes hello et vérifiez qu’il n’existe aucune perte de données.

## <a name="initiate-failback"></a>Lancer la restauration automatique
Après basculement à partir de l’emplacement principal toosecondary de hello, les machines virtuelles répliquées ne sont pas protégés par Site Recovery et emplacement secondaire de hello joue maintenant l’emplacement actif de hello. Suivez ces procédures toofail toohello précédent site principal d’origine. Cette procédure décrit comment toorun un basculement planifié pour la récupération d’un plan. Vous pouvez également exécuter basculement hello pour une seule machine virtuelle sur hello **virtuels** onglet.

1. Sélectionnez **Plans de récupération** > *nom_planrécupération*. Cliquez sur **Type de basculement** > **Planned Type de basculement**.
2. Sur hello ** confirmer le basculement planifié ** page, choisissez les emplacements source et cible hello. Notez le sens du basculement hello. Si basculement hello du principal a fonctionné comme prévu, et toutes les machines virtuelles sont dans l’emplacement secondaire de hello qu'il s’agit d’information uniquement.
3. Si vous effectuez la restauration à partir de Microsoft Azure, sélectionnez différents paramètres dans la zone **Synchronisation des données**:

   * **Synchroniser les données avant le basculement (synchroniser seulement les modifications d’ordre différentiel)** : cette option minimise le temps d’arrêt des machines virtuelles, car elles sont synchronisées sans être arrêtées. Il hello suivant :
     * Phase 1 : Prend un instantané d’ordinateur virtuel de hello dans Azure et de copier un ordinateur hôte Hyper-V de toohello local. l’ordinateur de Hello continue s’exécutant dans Azure.
     * Phase 2 : Arrête de machine virtuelle de hello dans Azure afin qu’aucune nouvelle modification se produire il. Hello dernier ensemble de modifications delta sont transférées toohello locale server et ordinateur virtuel local, hello a démarré.

    - **Synchroniser les données uniquement lors du basculement (téléchargement complet)**: utilisez cette option si vous exécutez Azure depuis une longue période. Cette option est plus rapide, car nous prévoyons que la plupart des disques de hello a changé, et nous ne voulons pas toospend les temps de calcul de la somme de contrôle. Il effectue un téléchargement du disque de hello. Il est également utile lorsque hello local virtual machine a été supprimé.

    >[!NOTE]
    >Nous vous recommandons d’utiliser cette option si vous avez déjà exécuté Azure pendant un certain temps (mois ou plus) ou hello local virtual machine a été supprimé. Cette option n’effectue pas tous les calculs de somme de contrôle.
    >
    >




4. Si le chiffrement des données est activé pour le cloud de hello, dans **clé de chiffrement** certificat hello select qui a été émis lorsque vous avez activé le chiffrement des données pendant l’installation du fournisseur sur le serveur VMM de hello.
5. Initier un basculement hello. Vous pouvez suivre la progression du basculement hello sur hello **travaux** onglet.
6. Si vous avez sélectionné des données de salutation hello option toosynchronize avant le basculement hello, une fois les hello initiale de la synchronisation des données est terminée et vous êtes prêt tooshut arrêt des machines virtuelles de hello dans Azure, cliquez sur **travaux** nom du travail de basculement planifié **Terminer le basculement**. Cette opération arrête hello machine Azure, hello de transferts dernières modifications toohello local virtual machine, et démarre hello machine virtuelle locale.
7. Vous pouvez maintenant vous connecter sur toovalidate de machine virtuelle hello, il est disponible comme prévu.
8. machine virtuelle de Hello est dans un état d’attente de validation. Cliquez sur **valider** toocommit hello basculement.
9. Maintenant dans l’ordre de cliquer sur la restauration automatique de hello toocomplete **réplication inverse** toostart protection de machine virtuelle de hello dans le site principal de hello.

## <a name="failback-tooan-alternate-location"></a>La restauration automatique tooan autre emplacement.
Si vous avez déployé la protection entre un [site Hyper-V et Azure](site-recovery-hyper-v-site-to-azure.md) avoir tooability toofailback à partir de l’emplacement de site autre tooan Azure. Cela est utile si vous avez besoin de tooset un nouveau matériel sur site. Voici comment procéder.

1. Si vous configurez un nouveau matériel, installez Windows Server 2012 R2 et hello le rôle Hyper-V sur le serveur de hello.
2. Créer un commutateur de réseau virtuel avec hello même nom que celui que vous aviez hello serveur d’origine.
3. Sélectionnez **éléments protégés** -> **groupe de Protection**  ->  <ProtectionGroupName>  ->  <VirtualMachineName> souhaitées toofail précédent, puis sélectionnez **planifié Basculement**.
4. Cliquez sur **Confirmer le basculement planifié** select **Créer une machine virtuelle locale si elle n’existe pas**.
5. Dans **nom d’hôte** sélectionnez hello nouveau serveur hôte de Hyper-V sur lequel vous souhaitez tooplace hello virtual machine.
6. Synchronisation des données nous vous recommandons de sélectionner option de hello **synchroniser les données hello avant le basculement de hello**. Cela permet de réduire le temps d’arrêt des machines virtuelles, car elles sont synchronisées sans être arrêtées. Il hello suivant :

   * Phase 1 : Prend un instantané d’ordinateur virtuel de hello dans Azure et de copier un ordinateur hôte Hyper-V de toohello local. l’ordinateur de Hello continue s’exécutant dans Azure.
   * Phase 2 : Arrête de machine virtuelle de hello dans Azure afin qu’aucune nouvelle modification se produire il. Hello dernier ensemble de modifications sont transférées toohello locale server et ordinateur virtuel local, hello est démarré.
7. Cliquez sur hello coche toobegin hello basculement (restauration).
8. Une fois la synchronisation initiale hello est terminée et que vous êtes prêt tooshut la machine virtuelle de hello dans Azure, cliquez sur **travaux** > <planned failover job> > **terminer le basculement**. Cette opération arrête hello machine Azure, les transferts hello dernières modifications toohello machine virtuelle sur site et démarre l’application.
9. Vous pouvez vous connecter sur tooverify d’ordinateur virtuel local hello que tout fonctionne comme prévu. Puis cliquez sur **valider** toofinish hello basculement.
10. Cliquez sur **réplication inverse** toostart protection de machine virtuelle de local hello.

    > [!NOTE]
    > Si vous annulez le travail de restauration hello alors qu’il est à l’étape de la synchronisation des données, hello local machine virtuelle sera dans un état endommagé. Il s’agit, car la synchronisation des données copie les données les plus récentes hello à partir de disques de données de machine virtuelle Azure disques toohello localement, et jusqu'à ce que hello synchronisation terminée, les données de disque hello ne peuvent pas être dans un état cohérent. Si hello local VM est démarré après l’annulation de la synchronisation des données, ne peut pas démarrer. Nouveau déclencheur basculement toocomplete hello la synchronisation des données.
    >
    >



## <a name="next-steps"></a>Étapes suivantes

Une fois que vous avez terminé le travail de restauration hello, **valider** hello virtual machine. Validation supprime hello machine virtuelle Azure et ses disques et prépare hello toobe de machine virtuelle protégée à nouveau.

Après avoir **valider**, vous pouvez lancer hello *réplication inverse*. Ceci démarrera empêchant la machine virtuelle de hello tooAzure de retour locale. Notez que ceci va uniquement les modifications de réplication hello depuis hello machine virtuelle a été désactivé dans Azure et par conséquent envoie différentielle modifie uniquement.
