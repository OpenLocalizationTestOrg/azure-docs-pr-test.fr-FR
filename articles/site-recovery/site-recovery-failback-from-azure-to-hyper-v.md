---
title: "Restauration automatique dans Azure Site Recovery pour les machines virtuelles Hyper-V | Microsoft Docs"
description: "Azure Site Recovery coordonne la réplication, le basculement et la récupération des machines virtuelles et des serveurs physiques. Découvrez comment effectuer une restauration automatique à partir d’Azure vers un centre de données local."
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
ms.openlocfilehash: 7f478a61ee448d2d18b3ac7bc0a579b6e341c30d
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="failback-in-site-recovery-for-hyper-v-virtual-machines"></a>Restauration automatique dans Site Recovery pour les machines virtuelles Hyper-V

Cet article explique comment restaurer automatiquement des machines virtuelles protégées par Site Recovery.

## <a name="prerequisites"></a>Composants requis
1. Assurez-vous que le serveur VMM/Hyper-V du site principal est connecté.
2. Vous devez avoir effectué une **validation** sur la machine virtuelle.

## <a name="why-is-there-no-button-called-failback"></a>Pourquoi n’y a-t-il pas de bouton Restauration automatique ?
Dans le portail, il n’existe pas d’option Restauration automatique explicite. La restauration automatique est une étape consistant à revenir au site principal. Par définition, le basculement correspond au basculement des machines virtuelles du site principal (local) au site de récupération (Azure) et la restauration au rebasculement des machines virtuelles du site de récupération au site principal.

Lorsque vous lancez un basculement, le panneau vous informe du sens de la tâche. Si la tâche va être effectuée d’Azure au site local, il s’agit d’une restauration automatique.

## <a name="why-is-there-only-a-planned-failover-gesture-to-failback"></a>Pourquoi y a-t-il uniquement une option de basculement planifié pour la restauration automatique ?
Azure est un environnement hautement disponible et vos machines virtuelles seront toujours disponibles. La restauration automatique est une activité planifiée où vous décidez d’observer un bref temps d’arrêt afin que les charges de travail puissent être exécutées à nouveau en local. Il ne doit y avoir aucune perte de données. Par conséquent, vous disposez uniquement d’une option de basculement planifié qui permet de désactiver les machines virtuelles dans Azure, de télécharger les dernières modifications et de s’assurer qu’aucune donnée n’est perdue.

## <a name="do-i-need-a-process-server-in-azure-to-failback-to-hyper-v"></a>Ai-je besoin d’un serveur de processus dans Azure pour procéder à une restauration automatique vers Hyper-V ?
Non, un serveur de processus est requis uniquement si vous protégez des machines virtuelles VMware. Aucun déploiement de composants supplémentaires n’est nécessaire lors de la protection/restauration automatique de machines virtuelles Hyper-V.

## <a name="initiate-failback"></a>Lancer la restauration automatique
Après le basculement du site principal vers l’emplacement secondaire, les machines virtuelles répliquées ne sont pas protégées par Site Recovery et l’emplacement secondaire joue désormais le rôle d’emplacement actif. Suivez ces procédures pour effectuer la restauration automatique vers le site principal d’origine. Cette procédure explique comment exécuter un test de basculement planifié pour un plan de récupération. Vous pouvez également exécuter le basculement d’une machine virtuelle unique, via l’onglet **Machines virtuelles** .

1. Sélectionnez **Plans de récupération** > *nom_planrécupération*. Cliquez sur **Type de basculement** > **Planned Type de basculement**.
2. Sur la page **Confirmer le basculement planifié**, choisissez les emplacements source et cible. Notez le sens du basculement. Si le basculement depuis le site principal a fonctionné comme prévu, et si toutes les machines virtuelles se trouvent à l’emplacement secondaire, ces éléments sont fournis à titre informatif uniquement.
3. Si vous effectuez la restauration à partir de Microsoft Azure, sélectionnez différents paramètres dans la zone **Synchronisation des données**:

   * **Synchroniser les données avant le basculement (synchroniser seulement les modifications d’ordre différentiel)** : cette option minimise le temps d’arrêt des machines virtuelles, car elles sont synchronisées sans être arrêtées. Il effectue les opérations suivantes :
     * Phase 1 : Un instantané de la machine virtuelle est créé dans Microsoft Azure, puis copié sur l’hôte Hyper-V local. La machine continue de s’exécuter dans Microsoft Azure.
     * Phase 2 : La machine virtuelle est arrêtée dans Microsoft Azure, afin de ne faire l’objet d’aucune nouvelle modification. Le jeu final de modifications d’ordre différentiel est transféré vers le serveur local ; la machine virtuelle locale est démarrée.

    - **Synchroniser les données uniquement lors du basculement (téléchargement complet)**: utilisez cette option si vous exécutez Azure depuis une longue période. Cette option est plus rapide, car nous nous attendons à ce que la majeure partie du disque ait changé et nous ne voulons pas passer du temps au calcul de la somme de contrôle. Elle effectue un téléchargement du disque. C’est également utile lorsque la machine virtuelle locale a été supprimée.

    >[!NOTE]
    >Nous vous recommandons d’utiliser cette option si vous exécutez Azure depuis un certain temps (un mois ou plus) ou si la machine virtuelle locale a été supprimée. Cette option n’effectue aucun calcul de somme de contrôle.


4. Si la fonction de chiffrement des données est activée pour le cloud, accédez à la zone **Clé de chiffrement** et sélectionnez le certificat émis lorsque vous avez activé le chiffrement des données pendant l’installation du fournisseur sur le serveur VMM.
5. Lancez le basculement. Vous pouvez suivre la progression du basculement sur l’onglet **Tâches** .
6. Si vous avez sélectionné l’option de synchronisation des données avant le basculement, lorsque la synchronisation initiale des données est terminée et que vous êtes prêt à arrêter les machines virtuelles dans Microsoft Azure, cliquez sur **Tâches** nom de la tâche de basculement planifié **Terminer le basculement**. Cette action arrête la machine Microsoft Azure et transfère les dernières modifications apportées à la machine virtuelle locale, laquelle est ensuite démarrée en local.
7. Vous pouvez maintenant vous connecter à la machine virtuelle, afin de vérifier qu’elle fonctionne comme prévu.
8. Cette dernière présente un état de validation en attente. Cliquez sur **Valider** pour valider le basculement.
9. Afin de terminer la restauration automatique, cliquez sur **Réplication inverse** pour commencer à protéger la machine virtuelle sur le site principal.

## <a name="failback-to-an-alternate-location"></a>Restauration automatique vers un autre emplacement
Si vous avez déployé la fonction de protection entre un [site Hyper-V et Microsoft Azure](site-recovery-hyper-v-site-to-azure.md) , vous avez la possibilité d’effectuer une restauration automatique depuis Microsoft Azure vers un autre emplacement local. Cette opération est utile si vous devez configurer de nouveaux composants matériels locaux. Voici comment procéder.

1. Si vous configurez un nouveau composant matériel, installez le logiciel Windows Server 2012 R2 et le rôle Hyper-V sur le serveur.
2. Créez un commutateur réseau virtuel portant le même nom que celui du serveur d’origine.
3. Sélectionnez **Éléments protégés** -> **Groupe de protection** -> <ProtectionGroupName> -> <VirtualMachineName> que vous souhaitez restaurer de manière automatique, puis sélectionnez **Basculement planifié**.
4. Cliquez sur **Confirmer le basculement planifié** select **Créer une machine virtuelle locale si elle n’existe pas**.
5. Dans **Nom d’hôte** , sélectionnez le nouveau serveur hôte Hyper-V sur lequel vous souhaitez placer la machine virtuelle.
6. Dans le champ Synchronisation des données, nous vous recommandons de sélectionner l’option **Synchroniser les données avant le basculement**. Cela permet de réduire le temps d’arrêt des machines virtuelles, car elles sont synchronisées sans être arrêtées. Il effectue les opérations suivantes :

   * Phase 1 : Un instantané de la machine virtuelle est créé dans Microsoft Azure, puis copié sur l’hôte Hyper-V local. La machine continue de s’exécuter dans Microsoft Azure.
   * Phase 2 : La machine virtuelle est arrêtée dans Microsoft Azure, afin de ne faire l’objet d’aucune nouvelle modification. Le jeu de modification final est transféré vers le serveur local ; la machine virtuelle locale est démarrée.
7. Cochez la base pour commencer le basculement (restauration automatique).
8. Lorsque la synchronisation initiale se termine et que vous êtes prêt à arrêter la machine virtuelle dans Microsoft Azure, cliquez sur **Tâches** > <planned failover job> > **Terminer le basculement**. Cette action arrête la machine Microsoft Azure et transfère les dernières modifications apportées à la machine virtuelle locale, laquelle est ensuite démarrée.
9. Vous pouvez vous connecter à la machine virtuelle locale pour vérifier que tous les composants fonctionnent comme prévu. Ensuite, cliquez sur **Valider** pour terminer le basculement.
10. Cliquez sur **Réplication inverse** pour commencer à protéger la machine virtuelle locale.

    > [!NOTE]
    > Si vous annulez l’opération de restauration automatique à l’étape de synchronisation des données, l’état de la machine virtuelle locale sera corrompu. En effet, la synchronisation des données copie les données les plus récentes de la machine virtuelle Azure vers les disques de données locaux, et tant que la synchronisation n’est pas terminée, l’état du disque de données risque de ne pas être cohérent. Si la machine virtuelle locale est démarrée après l’annulation de la synchronisation des données, l’opération risque d’échouer. Relancez le basculement pour terminer la synchronisation des données.

## <a name="time-taken-to-failback"></a>Durée de la restauration automatique
Le temps nécessaire pour effectuer la synchronisation de données et démarrer la machine virtuelle dépend de différents facteurs. Nous allons vous expliquer ce qui se passe pendant la synchronisation de données pour vous donner une idée de ce temps nécessaire.

La synchronisation de données prend une capture instantanée des disques de la machine virtuelle, procède à une vérification bloc par bloc et calcule la somme de contrôle. Cette somme de contrôle calculée est envoyée au niveau local pour être comparée à la somme de contrôle locale du même bloc. Si les sommes de contrôle correspondent, le bloc de données n’est pas transféré. S’ils ne correspondent pas, le bloc de données est transféré au niveau local. La durée de ce transfert dépend de la bande passante disponible. La vitesse de la somme de contrôle correspond à quelques Go par minute. 

Pour accélérer le téléchargement des données, vous pouvez configurer votre agent MARS pour utiliser plusieurs threads parallèles pour effectuer le téléchargement. Reportez-vous au [document ici](https://support.microsoft.com/en-us/help/3056159/how-to-manage-on-premises-to-azure-protection-network-bandwidth-usage) pour savoir comment modifier les threads de téléchargement dans l’agent.


## <a name="next-steps"></a>Étapes suivantes

Une fois la tâche de restauration automatique terminée, **validez** la machine virtuelle. La validation supprime la machine virtuelle et ses disques, et prépare la machine virtuelle à protéger à nouveau.

Après la **validation**, vous pouvez lancer la *réplication inverse*. Cela démarrera la reprotection de la machine virtuelle du site local vers Azure. Notez que cette opération réplique uniquement les modifications apportées depuis que la machine virtuelle a été désactivée dans Azure et n’envoie donc que les modifications d’ordre différentiel.
