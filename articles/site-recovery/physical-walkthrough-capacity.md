---
title: "aaaPlan la capacité et de mise à l’échelle pour tooAzure de réplication de serveur physique avec Azure Site Recovery | Documents Microsoft"
description: "Utilisez cette capacité tooplan de l’article et la mise à l’échelle lors de la réplication tooAzure des serveurs physiques Windows/Linux avec Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 554f59ee-0b49-4779-9737-90cb601ef6fe
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: rayne
ms.openlocfilehash: 209980963c07d13e15802a5da44769ac559217d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-physical-server-tooazure-replication"></a>Étape 3 : Planifier la capacité et la mise à l’échelle pour la réplication tooAzure serveur physique

Utiliser cette toofigure article out capacité et mise à l’échelle, lorsque vous effectuez une réplication locale tooAzure des serveurs physiques Windows/Linux avec [Azure Site Recovery](site-recovery-overview.md).

Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="plan-deployment-capacity"></a>Planifier la capacité de déploiement

1. Lire ce [article](site-recovery-plan-capacity-vmware.md) toolearn sur l’estimation des besoins de réplication et des conseils pour le redimensionnement des composants de Site Recovery.
2. Lisez les considérations de hello ci-dessous toolearn sur les serveurs des composants de mise à l’échelle et contrôler la bande passante de l’ordinateur répliqué.

## <a name="replication-considerations"></a>Informations relatives à la réplication

Utilisez ces toofigure considérations sur les exigences du serveur répliqué.

**Composant** | **Détails** 
--- | --- 
**Réplication** | **Taux de modification quotidien maximal :** un ordinateur protégé peut uniquement utiliser un serveur de traitement, et un serveur de processus unique peut gérer un taux de changement quotidien jusqu'à too2 to. 2 To est donc maximale des données quotidiennes hello modifier taux est prise en charge pour un ordinateur protégé.<br/><br/> **Débit maximal :** un ordinateur répliqué peut appartenir tooone compte de stockage dans Azure. Un compte de stockage standard peut gérer un maximum de 20 000 demandes par seconde, et nous vous recommandons de conserver nombre hello d’opérations d’entrée/sortie par seconde (IOPS) sur un too20 machine source, 000. Par exemple, si vous disposez d’un ordinateur source avec 5 disques, et chaque disque génère 120 IOPS (taille de 8 Ko) sur l’ordinateur source de hello, puis il sera dans hello Azure limite des e/s de disque de 500 par. (nombre de hello de comptes de stockage requis est machine source au total de toohello égal IOPS, divisé par 20 000.)

## <a name="configuration-server-capacity"></a>Capacité du serveur de configuration

serveur de configuration Hello doit être en mesure de toohandle hello quotidienne modification capacité dans toutes les charges de travail en cours d’exécution sur les ordinateurs protégés, et suffisamment de bande passante toocontinuously doit répliquer les données tooAzure stockage.

Comme meilleure pratique, recherchez le serveur de configuration de hello sur hello même réseau et le segment de réseau local en tant que machines que vous voulez tooprotect de hello. Il peut se trouver sur un autre réseau, mais les ordinateurs que vous souhaitez tooprotect doit avoir la couche réseau 3 visibilité tooit.

## <a name="sizing-recommendations"></a>Recommandations de dimensionnement

table de Hello résume les recommandations de dimensionnement basées sur le processeur.

**UC** | **Mémoire** | **Taille du disque cache** | **Taux de modification des données** | **Machines protégées**
--- | --- | --- | --- | ---
8 processeurs virtuels (2 sockets * 4 cœurs à 2,5 gigahertz [GHz]) | 16 Go | 300 Go | 500 Go ou moins | Répliquez moins de 100 machines.
12 processeurs virtuels (2 sockets * 6 cœurs à 2,5 GHz) | 18 Go | 600 Go | 500 Go too1 to | Répliquez entre 100 et 150 machines.
16 processeurs virtuels (2 sockets * 8 cœurs à 2,5 GHz) | 32 Go | 1 To | 1 to too2 to | Répliquez entre 150 et 200 machines.
Déployer un autre serveur de traitement | | | > 2 To | Déployer des serveurs de traitement supplémentaires si vous effectuez une réplication plus de 200 ordinateurs, ou si des modifications des données quotidiennes de hello taux dépasse 2 To.

Où :

* Chaque ordinateur source est configuré avec 3 disques de 100 Go chacune.
* Nous avons utilisé le stockage de référence de 8 disques SAP de 10 K tr/min avec RAID 10 pour les mesures de disque cache.

## <a name="process-server-capacity"></a>Capacité du serveur de processus


serveur de processus Hello reçoit des données de réplication à partir des ordinateurs protégés et il optimise avec la mise en cache, la compression et le chiffrement. Il envoie ensuite hello données tooAzure.

- ordinateur de serveur de processus Hello doit avoir suffisamment ressources tooperform ces tâches.
- premier serveur de processus Hello est installé par défaut sur le serveur de configuration hello. Vous pouvez déployer tooscale de serveurs de processus supplémentaire de votre environnement.
- serveur de processus Hello utilise un cache sur disque. Utilisez un disque distinct du cache de 600 Go ou plus de modifications données toohandle stockées dans l’événement hello d’un goulot d’étranglement du réseau ou d’une panne.
- Si vous devez tooprotect plus de 200 ordinateurs, ou les taux de modification quotidien hello sont supérieure à 2 To, vous pouvez ajouter des processus serveurs toohandle hello charge de la réplication. tooscale out, vous pouvez :
    - Augmenter le nombre de hello des serveurs de configuration. Par exemple, vous pouvez protéger les machines too400 avec deux serveurs de configuration.
    - Ajouter des serveurs de processus et utiliser ces serveurs de configuration hello toohandle le trafic au lieu de (ou en plus).


### <a name="example-process-server-scaling"></a>Exemple de mise à l’échelle du serveur de processus

Hello tableau suivant décrit un scénario dans lequel :

* Vous ne planifiez pas de serveur de configuration toouse hello en tant que processus serveur.
* Vous avez configuré un serveur de processus supplémentaire.
* Vous avez configuré le serveur de processus supplémentaire de machines virtuelles protégées toouse hello.
* Chaque ordinateur source protégé est configuré avec trois disques de 100 Go chacun.

**Serveur de configuration** | **Serveur de traitement supplémentaire** | **Taille du disque cache** | **Taux de modification des données** | **Machines protégées**
--- | --- | --- | --- | ---
8 processeurs virtuels (2 sockets * 4 cœurs @ 2,5 GHz), 16 Go de mémoire | 4 processeurs virtuels (2 sockets * 2 cœurs @ 2,5 GHz), 8 Go de mémoire | 300 Go | 250 Go ou moins | Répliquez 85 machines ou moins.
8 processeurs virtuels (2 sockets * 4 cœurs @ 2,5 GHz), 16 Go de mémoire | 8 processeurs virtuels (2 sockets * 4 cœurs @ 2,5 GHz), 12 Go de mémoire | 600 Go | 250 Go too1 to | Répliquez entre 85 et 150 machines.
12 processeurs virtuels (2 sockets * 6 cœurs @ 2,5 GHz), 18 Go de mémoire | 12 processeurs virtuels (2 sockets * 6 cœurs @ 2,5 GHz), 24 Go de mémoire | 1 To | 1 to too2 to | Répliquez entre 150 et 225 machines.

Hello dans laquelle vous mettez à l’échelle vos serveurs différemment selon votre préférence pour un modèle de montée en puissance parallèle ou la montée en puissance parallèle.  Vous pouvez aboutir à une montée en puissance avec le développement de serveurs de configuration et de processus haut de gamme, ou à une montée en charge avec le déploiement d’un nombre de serveurs supérieur avec moins de ressources. Par exemple, si vous avez besoin de machines de 220 tooprotect, vous pouvez effectuer de hello suivantes :

* Configurer le serveur de configuration hello avec 12 processeurs virtuels, 18 Go de mémoire et un serveur de processus supplémentaire avec 12 processeurs, 24 Go de mémoire. Configurer les ordinateurs protégés toouse hello serveur processus supplémentaire uniquement.
* Configurer deux serveurs de configuration (2 x 8 processeurs, 16 Go de RAM) et deux serveurs de processus supplémentaire (1 x 8 processeurs et 4 processeurs x 1 toohandle 135 + 85 [220] ordinateurs). Configurer des machines protégées toouse hello processus supplémentaire uniquement les serveurs.

## <a name="deploy-additional-process-servers"></a>Déployer d’autres serveurs de traitement

1. Suivez [ces instructions](site-recovery-vmware-setup-azure-ps-resource-manager.md) tooset d’un serveur de processus supplémentaires.
2. Si vous n’avez pas hello le mot de passe, exécutez **[SiteRecoveryInstallationFolder]\home\sysystems\bin\genpassphrase.exe – n** sur hello configuration serveur tooget il.
3. Après avoir configuré le serveur de processus hello, vous migrez source machines toouse il.

    1. Dans **paramètres** > **serveurs de récupération de Site**, cliquez sur le serveur de configuration hello > **serveurs de traitement**.
    2. Serveur de processus avec le bouton hello en cours d’utilisation > **commutateur**.
    3. Dans **serveur de processus cible sélectionnez**, sélectionnez hello processus serveur souhaité toouse, sélectionnez les ordinateurs virtuels de hello gère ce serveur hello.
    4. Cliquez sur icône d’information hello. toohelp que vous devez charger les décisions, hello moyenne espace suffisant tooreplicate chaque sélectionné toohello de machine virtuelle nouveau serveur de processus s’affiche.
    5. Cliquez sur hello coche toostart réplication toohello nouveau serveur de processus.

## <a name="control-network-bandwidth"></a>Contrôler la bande passante réseau

Après avoir exécuté [outil de planification de déploiement de hello](site-recovery-deployment-planner.md) toocalculate hello passante nécessaire pour la réplication (la réplication initiale hello et puis delta), vous pouvez contrôler la quantité hello de bande passante utilisée pour la réplication à l’aide de deux options :

* **Limiter la bande passante**: le trafic de VMware qui réplique tooAzure passe par un serveur de processus spécifique. Vous pouvez limiter la bande passante sur les ordinateurs hello en cours d’exécution en tant que serveurs de traitement.
* **Influencer la bande passante**: vous pouvez influer sur la bande passante hello utilisée pour la réplication à l’aide de deux clés de Registre :
  * Hello **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\UploadThreadsPerVM** valeur de Registre spécifie le nombre de hello de threads qui sont utilisés pour le transfert de données (la réplication initiale ou delta) d’un disque. Une valeur plus élevée augmente la bande passante du réseau hello utilisée pour la réplication.
  * Hello **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\DownloadThreadsPerVM** Spécifie le nombre de hello de threads utilisés pour le transfert de données pendant la restauration automatique.

### <a name="throttle-bandwidth"></a>Limiter la bande passante

1. Ouvrez hello le composant logiciel enfichable MMC Azure Backup sur agissant de machine hello en tant que serveur de processus hello. Par défaut, un raccourci pour la sauvegarde est disponible sur le bureau de hello ou Bonjour suivant du dossier : C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Dans le composant logiciel enfichable hello, cliquez sur **modifier les propriétés**.
3. Sur hello **limitation** onglet, sélectionnez **activer l’utilisation de la bande passante internet de limitation pour les opérations de sauvegarde**.
4. Définir des limites de hello pour le travail et non liés au travail heures. Les plages valides sont de Mbits/s des too102 de 512 Kbits/s par seconde.

    ![Limitation](./media/physical-walkthrough-capacity/throttle2.png)

Vous pouvez également utiliser hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) de limitation tooset applet de commande. Voici un exemple :

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indique qu’aucune limitation n’est requise.

### <a name="influence-network-bandwidth-for-a-vm"></a>Influer sur la bande passante réseau d’une machine virtuelle

1. Dans le Registre de hello machine virtuelle, accédez trop**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication**.
   * tooinfluence hello la bande passante le trafic sur un disque de réplication, modifier la valeur hello **UploadThreadsPerVM**, ou créez la clé de hello si elle n’existe pas.
   * la bande passante de hello tooinfluence pour le trafic de la restauration automatique d’Azure, modifier la valeur hello **DownloadThreadsPerVM**.
2. Hello par défaut est 4. Dans un réseau surapprovisionné, ces clés de Registre doivent être modifiées. Hello maximal est 32. Surveiller le trafic toooptimize hello valeur.




## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 4 : planifier la mise en réseau](physical-walkthrough-network.md).
