---
title: "série aaaStorSimple 8000 en tant que cible de sauvegarde avec Backup Exec | Documents Microsoft"
description: "Décrit la configuration de cible de sauvegarde hello StorSimple avec Veritas Backup Exec."
services: storsimple
documentationcenter: 
author: harshakirank
manager: matd
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/05/2016
ms.author: hkanna
ms.openlocfilehash: 270ad95e1f6b367e80048cad42beb936f205f69c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-backup-exec"></a>StorSimple comme cible de sauvegarde avec Backup Exec

## <a name="overview"></a>Vue d'ensemble

Azure StorSimple est une solution de stockage cloud hybride de Microsoft. StorSimple adresses complexités hello de croissance exponentielle des données à l’aide d’un compte de stockage Azure comme une extension de la solution locale de hello et automatiquement hiérarchisation des données sur le stockage local et le stockage cloud.

Dans cet article, nous traitons de l’intégration de StorSimple à Veritas Backup Exec et des meilleures pratiques en matière d’intégration de ces deux solutions. Nous avons aussi formuler des recommandations sur comment intégrer des tooset des Backup Exec toobest avec StorSimple. Nous différer tooVeritas meilleures pratiques, les architectes de sauvegarde et les administrateurs de hello meilleure manière tooset les exigences de sauvegarde individuelles de Backup Exec toomeet et les contrats de niveau de service (SLA).

Bien que cet article illustre les étapes de configuration et les concepts clés, cela ne constitue en aucun cas un guide de configuration ou d’installation pas à pas. Nous partons du principe qu’infrastructure et des composants de base hello sont dans l’ordre de travail et prêt toosupport hello des concepts que nous décrivons.

### <a name="who-should-read-this"></a>Qui doit lire ce document ?

informations de Hello dans cet article seront plus utiles toobackup administrateurs, les administrateurs de stockage et les architectes de stockage qui ont une connaissance de stockage, Windows Server 2012 R2, Ethernet, services de cloud computing et Backup Exec.

## <a name="supported-versions"></a>Versions prises en charge

-   [Backup Exec 16 et versions ultérieures](http://backupexec.com/compatibility)
-   [StorSimple Update 3 et versions ultérieures](storsimple-overview.md#storsimple-workload-summary)


## <a name="why-storsimple-as-a-backup-target"></a>Pourquoi utiliser StorSimple comme cible de sauvegarde ?

StorSimple est un bon choix en tant que cible de sauvegarde, car :

-   Il fournit un stockage local standard toouse des applications de sauvegarde comme destination de sauvegarde rapide, sans aucune modification. Vous pouvez utiliser StorSimple pour les restaurations rapides des sauvegardes récentes.
-   Son cloud hiérarchisation est intégrée de manière transparente avec un toouse de compte de stockage Azure cloud Azure un stockage économique.
-   StorSimple fournit automatiquement un stockage hors site pour la récupération d’urgence.

## <a name="key-concepts"></a>Concepts clés

Comme avec toute solution de stockage, une évaluation précise de performances de stockage de la solution de hello, SLA, taux de modification et les besoins en capacité croissance est toosuccess critiques. Hello principale est qu’en introduisant un niveau de cloud, votre cloud toohello heures d’accès et les débits jouent un rôle fondamental dans capacité hello de StorSimple toodo son travail.

StorSimple est conçu tooprovide stockage tooapplications qui opèrent sur un ensemble bien défini de travail de données (à chaud). Dans ce modèle, le jeu de travail hello de données est stocké sur les couches locales hello, et hello ensemble de chômés/froid/archivé restant de données est hiérarchisé toohello cloud. Ce modèle est représenté dans la figure suivante de hello. ligne de Hello presque plat verte représente des données hello stockées sur les niveaux de hello local de l’appareil StorSimple hello. Hello ligne rouge représente hello le montant total des données stockées sur hello solution StorSimple à tous les niveaux. espace Hello entre les ligne hello plat verte et une courbe exponentielle rouge hello représente la quantité totale de hello des données stockées dans le cloud de hello.

**Hiérarchisation StorSimple**
![Diagramme de la hiérarchisation StorSimple](./media/storsimple-configure-backup-target-using-backup-exec/image1.jpg)

Avec cette architecture n’oubliez pas, vous constaterez que StorSimple est parfaitement toooperate comme cible de sauvegarde. Vous pouvez utiliser StorSimple pour :
-   Effectuer votre des restaurations plus fréquentes à partir de la plage de travail local hello de données.
-   Utilisez les cloud hello pour la récupération d’urgence hors site et les données plus anciennes, où les restaurations sont moins fréquentes.

## <a name="storsimple-benefits"></a>Avantages de StorSimple

StorSimple fournit une solution locale qui s’intègrent avec Microsoft Azure, en tirant parti des transparente tooon local d’accès et le stockage cloud.

StorSimple utilise la hiérarchisation automatique entre un périphérique local hello, qui a un appareil (SSD) et serial attached SCSI (SAS) stockage et le stockage Azure. Conserve hiérarchisation automatique fréquence d’accès aux données locales sur les couches SSD et disques durs SAS hello. Il déplace les données rarement tooAzure stockage.

StorSimple offre les avantages suivants :

-   Algorithmes de déduplication et compression uniques qui utilisent des niveaux de la déduplication sans précédent tooachieve hello cloud
-   Haute disponibilité
-   Géoréplication reposant sur la fonctionnalité de géoréplication Azure
-   Intégration à Azure
-   Chiffrement des données dans le cloud de hello
-   Récupération d’urgence et conformité améliorées

Bien que StorSimple présente deux principaux scénarios de déploiement (cible de sauvegarde principale et secondaire), il s’agit essentiellement d’un dispositif de stockage de bloc. StorSimple tout hello la compression et la déduplication. Il envoie et récupère les données entre le cloud de hello et application hello et système de fichiers en toute transparence.

Pour plus d’informations sur StorSimple, consultez l’article [StorSimple série 8000 : une solution de stockage de cloud hybride](storsimple-overview.md). En outre, vous pouvez consulter hello [spécifications techniques de la série StorSimple 8000](storsimple-technical-specifications-and-compliance.md).

> [!IMPORTANT]
> L’utilisation d’un appareil StorSimple comme cible de sauvegarde n’est prise en charge que pour StorSimple 8000 Update 3 et les versions ultérieures.

## <a name="architecture-overview"></a>Présentation de l'architecture

Hello tableaux suivants indiquent les premiers conseils hello appareil-à-architecture du modèle.

**Capacités de stockage local et cloud offertes par StorSimple**

| Capacité de stockage       | 8100          | 8600            |
|------------------------|---------------|-----------------|
| Capacité de stockage local | &lt; 10 Tio\*  | &lt; 20 Tio\*  |
| Capacité de stockage cloud | &gt; 200 Tio\* | &gt; 500 Tio\* |
\* La taille de stockage indiquée ne prend en compte aucune déduplication ni compression.

**Capacités de StorSimple dans les scénarios de sauvegarde principale et secondaire**

| Scénario de sauvegarde  | Capacité de stockage local  | Capacité de stockage cloud  |
|---|---|---|
| Sauvegarde principale  | Sauvegardes récentes stockés sur le stockage local pour la récupération rapide toomeet point de récupération (RPO) | Capacité du cloud adaptée à l’historique des sauvegardes (RPO) |
| Sauvegarde secondaire | Possibilité de stocker une copie secondaire des données de sauvegarde dans la capacité du cloud  | N/A  |

## <a name="storsimple-as-a-primary-backup-target"></a>Utiliser StorSimple comme cible de sauvegarde principale

Dans ce scénario, les volumes StorSimple sont présentés toohello l’application de sauvegarde comme hello seul référentiel pour les sauvegardes. Hello figure suivante montre une architecture de solution dans lequel toutes les sauvegardes StorSimple hiérarchisé volumes pour les sauvegardes et restaurations.

![Diagramme logique de l’utilisation de StorSimple comme cible de sauvegarde principale](./media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a>Procédure logique de sauvegarde de la cible principale

1.  contacts du serveur de sauvegarde Hello hello agent de sauvegarde cible et l’agent de sauvegarde hello transmet des données toohello sauvegarde du serveur.
2.  serveur de sauvegarde Hello écrit des données toohello StorSimple à plusieurs niveaux de volumes.
3.  serveur de sauvegarde Hello met à jour la base de données de catalogue hello et puis termine le travail de sauvegarde hello.
4.  Un script d’instantané déclenche le Gestionnaire d’instantanés hello StorSimple cloud (début ou suppression).
5.  serveur de sauvegarde Hello supprime les sauvegardes ayant expirés basés sur une stratégie de rétention.


### <a name="primary-target-restore-logical-steps"></a>Procédure logique de restauration de la cible principale

1.  serveur de sauvegarde Hello démarre la restauration des données appropriées de hello à partir de l’espace de stockage hello.
2.  agent de sauvegarde Hello reçoit les données de hello hello serveur de sauvegarde.
3.  serveur de sauvegarde Hello termine le travail de restauration hello.

## <a name="storsimple-as-a-secondary-backup-target"></a>Utiliser StorSimple comme cible de sauvegarde secondaire

Dans ce scénario, les volumes StorSimple sont principalement utilisés à des fins de rétention à long terme ou d’archivage.

Hello figure suivante illustre une architecture dans laquelle les sauvegardes initiales et restaure le volume cible hautes performances. Ces sauvegardes sont copiées et archivée tooa StorSimple à plusieurs niveaux de volume sur une planification définie.

Il est important toosize votre volume de hautes performances, afin qu’il puisse gérer vos conditions de performances et la capacité de stratégie de rétention.

![Diagramme logique de l’utilisation de StorSimple comme cible de sauvegarde secondaire](./media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a>Procédure logique de sauvegarde de la cible secondaire

1.  contacts du serveur de sauvegarde Hello hello agent de sauvegarde cible et l’agent de sauvegarde hello transmet des données toohello sauvegarde du serveur.
2.  serveur de sauvegarde Hello écrit stockage toohigh-performances des données.
3.  serveur de sauvegarde Hello met à jour la base de données de catalogue hello et puis termine le travail de sauvegarde hello.
4.  Bonjour tooStorSimple de sauvegardes de copies de sauvegarde du serveur basé sur une stratégie de rétention.
5.  Un script d’instantané déclenche le Gestionnaire d’instantanés hello StorSimple cloud (début ou suppression).
6.  serveur de sauvegarde Hello supprime les sauvegardes ayant expirés basés sur une stratégie de rétention.

### <a name="secondary-target-restore-logical-steps"></a>Procédure logique de restauration de la cible secondaire

1.  serveur de sauvegarde Hello démarre la restauration des données appropriées de hello à partir de l’espace de stockage hello.
2.  agent de sauvegarde Hello reçoit les données de hello hello serveur de sauvegarde.
3.  serveur de sauvegarde Hello termine le travail de restauration hello.

## <a name="deploy-hello-solution"></a>Déployer la solution de hello

Déploiement de solutions de hello nécessite trois étapes :
1. Préparer l’infrastructure de réseau hello.
2. Déployer votre appareil StorSimple comme cible de sauvegarde.
3. Déployer Veritas Backup Exec.

Chaque étape est décrite en détail dans les sections suivantes de hello.

### <a name="set-up-hello-network"></a>La configuration du réseau de hello

StorSimple est une solution qui est intégrée à hello cloud Azure, StorSimple requiert une toohello connexion active et fonctionne cloud Azure. Cette connexion est utilisée pour les opérations telles que les instantanés cloud, gestion et le transfert de métadonnées et stockage en cloud tooAzure tootier des données plus anciennes et moins sollicitées.

Hello solution tooperform de façon optimale, nous vous recommandons que vous suivez ces conseils de mise en réseau :

-   lien Hello qui se connecte votre tooAzure hiérarchisation StorSimple doit répondre à vos besoins en bande passante. tooachieve, appliquer hello nécessaire qualité de Service (QoS) tooyour de niveau infrastructure commutateurs toomatch votre RPO et la récupération temps SLA d’objectif (RTO).
-   Les latences d’accès maximales au service Stockage Blob Azure doivent être de l’ordre de 80 ms.

### <a name="deploy-storsimple"></a>Déployer StorSimple

Pour découvrir un guide de déploiement de StorSimple pas à pas, consultez l’article [Déploiement de votre appareil StorSimple local](storsimple-deployment-walkthrough-u2.md).

### <a name="deploy-backup-exec"></a>Déployer Backup Exec

Pour découvrir les meilleures pratiques en matière d’installation de Backup Exec, consultez l’article [Best practices for Backup Exec installation (Meilleures pratiques en matière d’installation de Backup Exec)](https://www.veritas.com/support/en_US/article.000068207).

## <a name="set-up-hello-solution"></a>Configurer la solution de hello

Dans cette section, nous fournissons quelques exemples de configuration. Hello des exemples et des recommandations suivantes illustrent implémentation élémentaire et fondamental de hello. Cette implémentation ne s’appliquent pas directement les exigences de sauvegarde spécifique tooyour.

### <a name="set-up-storsimple"></a>Configurer StorSimple

| Tâches de déploiement StorSimple  | Commentaires supplémentaires |
|---|---|
| Déploiement de votre appareil StorSimple local | Versions prises en charge : Update 3 et versions ultérieures. |
| Cible de sauvegarde hello sous tension. | Utilisez ces tooturn de commandes sur ou désactiver le mode cible de sauvegarde et l’état de tooget. Pour plus d’informations, consultez [se connecter à distance de l’appareil StorSimple tooa](storsimple-remote-connect.md).</br> tooturn sur le mode de sauvegarde : `Set-HCSBackupApplianceMode -enable`. </br> tooturn désactive le mode de sauvegarde : `Set-HCSBackupApplianceMode -disable`. </br> état actuel de hello tooget des paramètres de mode de sauvegarde : `Get-HCSBackupApplianceMode`. |
| Créer un conteneur de volume commun pour le volume qui stocke les données de sauvegarde hello. Toutes les données d’un conteneur de volumes sont dédupliquées. | Les conteneurs de volumes StorSimple définissent les domaines de déduplication.  |
| Créez les volumes StorSimple. | Créer des volumes avec des tailles comme une utilisation toohello fermer anticipée que possible, car la taille du volume affecte la durée d’instantané de cloud. Pour plus d’informations sur la façon toosize un volume, pour en savoir plus sur [stratégies de rétention](#retention-policies).</br> </br> Utilisez StorSimple à plusieurs niveaux des volumes et sélectionnez hello **utiliser ce volume pour les données d’archive moins fréquemment sollicitées** case à cocher. </br> L’utilisation de volumes épinglés localement uniquement n’est pas prise en charge. |
| Créer une stratégie de sauvegarde StorSimple unique pour tous les volumes de cible de sauvegarde hello. | Une stratégie de sauvegarde StorSimple définit un groupe de cohérence de volume hello. |
| Désactiver la planification de hello expiration des instantanés de hello. | Les captures instantanées sont déclenchées sous la forme d’une opération post-traitement. |

### <a name="set-up-hello-host-backup-server-storage"></a>Configurer le stockage de sauvegarde du serveur hôte hello

Vous pouvez configurer le stockage de sauvegarde du serveur hôte hello selon les instructions toothese :  

- N’utilisez pas des volumes fractionnés (créés par le Gestionnaire de disque Windows). Les disques fractionnés ne sont pas pris en charge.
- Formatez vos volumes à l’aide du système de fichiers NTFS avec une taille d’allocation de 64 Ko.
- Mapper les volumes StorSimple hello directement le serveur de Backup Exec toohello.
    - Utilisez iSCSI pour les serveurs physiques.
    - Utilisez des disques pass-through pour les serveurs virtuels.

## <a name="best-practices-for-storsimple-and-backup-exec"></a>Meilleures pratiques pour StorSimple et Backup Exec

Configurer votre solution en fonction des instructions toohello Bonjour les sections suivantes.

### <a name="operating-system-best-practices"></a>Meilleures pratiques concernant le système d’exploitation

-   Désactiver le chiffrement de Windows Server et la déduplication pour le système de fichiers NTFS hello.
-   Désactiver la défragmentation de Windows Server sur des volumes StorSimple hello.
-   Désactiver l’indexation sur hello de volumes StorSimple de Windows Server.
-   Exécuter une analyse antivirus sur l’hôte source de hello (et non sur des volumes StorSimple hello).
-   Désactiver la valeur par défaut hello [maintenance de Windows Server](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) dans le Gestionnaire des tâches. Procédez comme suit dans un des hello suivant façons :
   - Désactiver le Configurateur de Maintenance hello dans le Planificateur de tâches Windows.
   - Téléchargez [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) à partir de Windows Sysinternals. Après avoir téléchargé PsExec, exécutez Azure PowerShell en tant qu’administrateur, puis tapez :
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a>Meilleures pratiques concernant StorSimple

  -   Assurez-vous que l’appareil StorSimple hello est mis à jour trop[mise à jour 3 ou version ultérieure](storsimple-install-update-3.md).
  -   Isolez le trafic iSCSI et cloud. Utiliser des connexions iSCSI dédié pour le trafic entre le serveur de sauvegarde StorSimple et hello.
  -   Assurez-vous que l’appareil StorSimple est une cible de sauvegarde dédiée. Les charges de travail mixtes ne sont pas prises en charge, car elles affectent le RTO et le RPO.

### <a name="backup-exec-best-practices"></a>Meilleures pratiques concernant Backup Exec

-   Exec de sauvegarde doit être installé sur un lecteur local du serveur de hello et non sur un volume StorSimple.
-   Définir un stockage de sauvegarde Exec hello **opérations d’écriture simultanées** toohello maximale autorisée.
    -   Définir un stockage de sauvegarde Exec hello **taille de bloc et de la mémoire tampon** too512 Ko.
    -   Activez les **opérations de lecture et d’écriture en mémoire tampon** de stockage Backup Exec.
-   StorSimple prend en charge les sauvegardes Backup Exec complètes et incrémentielles. Nous vous déconseillons d’utiliser les sauvegardes synthétiques et différentielles.
-   Les fichiers de données de sauvegarde doivent uniquement contenir les données d’un travail spécifique. Par exemple, aucun ajout de supports n’est autorisé entre les différents travaux.
-   Désactivez la vérification des travaux. Si nécessaire, la vérification doit être planifiée après le dernier travail de sauvegarde hello. Il est important toounderstand que ce travail affecte votre fenêtre de sauvegarde.
-   Sélectionnez **Storage (Stockage)** > **Your disk (Votre disque)** > **Details (Détails)** > **Properties (Propriétés)**. Désactivez **Pre-allocate disk space (Pré-allouer de l’espace disque)**.

Pour les derniers paramètres de sauvegarde Exec hello et meilleures pratiques pour implémenter ces exigences, consultez [site Web de Veritas hello](https://www.veritas.com).

## <a name="retention-policies"></a>Stratégies de rétention

Un des types de stratégie de rétention de sauvegarde les plus courants hello est une stratégie grand-père Père et fils (GFS). Dans une stratégie GFS, une sauvegarde incrémentielle est effectuée tous les jours et les sauvegardes complètes sont effectuées de façon hebdomadaire et mensuelle. Cette stratégie donne lieu à six volumes hiérarchisés StorSimple. Un volume contient des sauvegardes complètes hello hebdomadaires, mensuelles ou annuelles. Hello autres cinq volumes stockent des sauvegardes incrémentielles quotidiennes.

Bonjour l’exemple suivant, nous utilisons une rotation GFS. exemple de Hello suppose hello qui suit :

-   Utilisation de données non dédupliquées ni compressées.
-   Sauvegardes complètes de 1 Tio chacune.
-   Sauvegardes incrémentielles quotidiennes de 500 Gio chacune.
-   Quatre sauvegardes hebdomadaires sont conservées pendant un mois.
-   Douze sauvegardes mensuelles sont conservées pendant un an.
-   Une sauvegarde annuelle est conservée pendant 10 ans.

Hello précédant les hypothèses, créer un 26-TiB StorSimple à plusieurs niveaux de volume pour les sauvegardes complètes hello mensuel et annuel. Créer un 5-TiB StorSimple à plusieurs niveaux de volume pour chacune des sauvegardes quotidiennes incrémentielles de hello.

| Type de sauvegarde et rétention | Taille (Tio) | Multiplicateur GFS\* | Capacité totale (Tio)  |
|---|---|---|---|
| Complète hebdomadaire | 1 | 4  | 4 |
| Incrémentielle quotidienne | 0.5 | 20 (cycles correspondant au nombre de semaines par mois) | 12 (2 pour le quota supplémentaire) |
| Complète mensuelle | 1 | 12 | 12 |
| Complète annuelle | 1  | 10 | 10 |
| Exigence GFS |   | 38 |   |
| Quota supplémentaire  | 4  |   | 42 au total pour l’exigence GFS  |
\*nombre de hello est Hello multiplicateur GFS de copies vous devez tooprotect et conserver toomeet vos exigences de stratégie de sauvegarde.

## <a name="set-up-backup-exec-storage"></a>Configurer le stockage Backup Exec

### <a name="tooset-up-backup-exec-storage"></a>tooset configuration du stockage de sauvegarde Exec

1.  Dans la console de gestion de sauvegarde Exec hello, sélectionnez **stockage** > **configurer le stockage** > **le stockage sur disque**  >   **Suivant**.

    ![Console d’administration de Backup Exec, page de configuration du stockage](./media/storsimple-configure-backup-target-using-backup-exec/image4.png)

2.  Sélectionnez **Disk Storage (Stockage sur disque)**, puis sélectionnez **Next (Suivant)**.

    ![Console d’administration de Backup Exec, page de sélection du stockage](./media/storsimple-configure-backup-target-using-backup-exec/image5.png)

3.  Entrez un nom explicite, par exemple, **Samedi complète**, ainsi qu’une description. Sélectionnez **Suivant**.

    ![Console d’administration de Backup Exec, page de saisie d’un nom et d’une description](./media/storsimple-configure-backup-target-using-backup-exec/image7.png)

4.  Disque hello sélectionnez où vous souhaitez que le périphérique de stockage de disque toocreate hello, puis sélectionnez **suivant**.

    ![Console d’administration de Backup Exec, page de sélection du disque de stockage](./media/storsimple-configure-backup-target-using-backup-exec/image9.png)

5.  Incrémente le nombre de hello d’opérations d’écriture trop**16**, puis sélectionnez **suivant**.

    ![Console d’administration de Backup Exec, page des paramètres d’opérations d’écriture simultanées](./media/storsimple-configure-backup-target-using-backup-exec/image10.png)

6.  Passez en revue les paramètres hello et sélectionnez **Terminer**.

    ![Console d’administration de Backup Exec, page récapitulative de configuration du stockage](./media/storsimple-configure-backup-target-using-backup-exec/image11.png)

7.  À fin hello de chaque attribution de volume, modifiez hello stockage périphérique paramètres toomatch celles recommandées au [meilleures pratiques pour StorSimple et Backup Exec](#best-practices-for-storsimple-and-backup-exec).

    ![Console d’administration de Backup Exec, page de paramètres du dispositif de stockage](./media/storsimple-configure-backup-target-using-backup-exec/image12.png)

8.  Répétez les étapes 1 à 7 jusqu'à ce que vous avez terminé d’affecter votre tooBackup de volumes StorSimple Exec.

## <a name="set-up-storsimple-as-a-primary-backup-target"></a>Configurer StorSimple comme cible de sauvegarde principale

> [!NOTE]
> Restauration des données à partir d’une sauvegarde qui a été toohello hiérarchisé cloud se produit à des vitesses de cloud.

Hello figure suivante illustre mappage hello d’un travail de sauvegarde tooa volume classique. Dans ce cas, toutes les sauvegardes hebdomadaires hello mappent disque plein de toohello samedi, et les sauvegardes incrémentielles hello mappent les disques incrémentielle tooMonday-vendredi. Tous les hello des sauvegardes et de restaurations à partir d’un StorSimple à plusieurs niveaux de volume.

![Diagramme logique de la configuration de la cible de sauvegarde principale](./media/storsimple-configure-backup-target-using-backup-exec/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a>Exemple de planification GFS pour StorSimple comme cible de sauvegarde principale

Voici un exemple de planification de rotation GFS pour quatre semaines, mensuellement et annuellement :

| Fréquence/type de sauvegarde | Complet | Incrémentielle (jours 1-5)  |   
|---|---|---|
| Hebdomadaire (semaines 1-4) | Samedi | Lundi-vendredi |
| Mensuelle  | Samedi  |   |
| Annuelle | Samedi  |   |   |


### <a name="assign-storsimple-volumes-tooa-backup-exec-backup-job"></a>Affecter le travail de sauvegarde StorSimple volumes tooa Backup Exec

Hello séquence suivante suppose que hôte cible Backup Exec et hello est configuré conformément aux instructions de l’agent de sauvegarde Exec hello.

#### <a name="tooassign-storsimple-volumes-tooa-backup-exec-backup-job"></a>tooassign StorSimple volumes tooa Backup Exec du travail de sauvegarde

1.  Dans la console de gestion de sauvegarde Exec hello, sélectionnez **hôte** > **sauvegarde** > **sauvegarde tooDisk**.

    ![Console de gestion Exec de sauvegarde, sélectionnez toodisk de sauvegarde et de sauvegarde de l’hôte,](./media/storsimple-configure-backup-target-using-backup-exec/image14.png)

2.  Bonjour **propriétés de définition de la sauvegarde** boîte de dialogue **sauvegarde**, sélectionnez **modifier**.

    ![Console d’administration de Backup Exec, boîte de dialogue des propriétés de définition de sauvegarde](./media/storsimple-configure-backup-target-using-backup-exec/image15.png)

3.  Configurer vos sauvegardes complètes et incrémentielles afin qu’ils répondent à vos besoins RPO et RTO et conformes tooVeritas meilleures pratiques.

4.  Bonjour **Options de sauvegarde** boîte de dialogue, sélectionnez **stockage**.

    ![Console d’administration de Backup Exec, boîte de dialogue des options de sauvegarde de stockage](./media/storsimple-configure-backup-target-using-backup-exec/image16.png)

5.  Affecter correspondante StorSimple volumes tooyour planification de sauvegarde.

    > [!NOTE]
    > **La compression** et **le type de chiffrement** sont définies trop**aucun**.

6.  Sous **Vérifiez**, sélectionnez hello **ne pas vérifier les données pour ce travail** case à cocher. Cette option risque d’affecter la hiérarchisation StorSimple.

    > [!NOTE]
    > La défragmentation, l’indexation et vérification de l’arrière-plan d’affecter négativement hello hiérarchisation de StorSimple.

    ![Console d’administration de Backup Exec, paramètres de vérification des options de sauvegarde](./media/storsimple-configure-backup-target-using-backup-exec/image17.png)

7.  Lorsque vous avez configuré votre toomeet d’options de sauvegarde reste hello vos besoins, sélectionnez **OK** toofinish.

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a>Configurer StorSimple comme cible de sauvegarde secondaire

> [!NOTE]
>Restaurations de données à partir d’une sauvegarde qui a été toohello hiérarchisé cloud se produisent à des vitesses de cloud.

Dans ce modèle, vous devez avoir un tooserve de support (autres que StorSimple) de stockage comme un cache temporaire. Par exemple, vous pouvez utiliser une baie redondante de disques indépendants (RAID) volume tooaccommodate d’espace, d’entrée/sortie (e/s) et la bande passante. Nous vous recommandons d’utiliser les valeurs RAID 5, 50 et 10.

Hello figure suivante montre à court terme rétention type locale (serveur toohello) volumes les archives des volumes et rétention à long terme. Dans ce scénario, toutes les sauvegardes se hello local (serveur toohello) volume RAID. Ces sauvegardes sont dupliquées régulièrement et archivée tooan archive volume. Il est important toosize local (serveur toohello) volume RAID afin qu’il puisse gérer vos exigences de capacité et de performances rétention à court terme.

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a>Exemple GFS pour StorSimple utilisé comme cible de sauvegarde secondaire

![Diagramme logique de l’utilisation de StorSimple comme cible de sauvegarde secondaire](./media/storsimple-configure-backup-target-using-backup-exec/secondarybackuptargetdiagram.png)

tableau Hello suivant montre comment tooset des toorun de sauvegardes sur hello local et les disques de StorSimple. Il inclut les besoins en capacité individuelle et totale.

### <a name="backup-configuration-and-capacity-requirements"></a>Configuration des sauvegardes et exigences de capacité

| Type de sauvegarde et rétention | Stockage configuré | Taille (Tio) | Multiplicateur GFS | Capacité totale\* (Tio) |
|---|---|---|---|---|
| Semaine 1 (sauvegardes complètes et incrémentielles) |Disque local (court terme)| 1 | 1 | 1 |
| StorSimple semaines 2 à 4 |Disque StorSimple (long terme) | 1 | 4 | 4 |
| Complète mensuelle |Disque StorSimple (long terme) | 1 | 12 | 12 |
| Complète annuelle |Disque StorSimple (long terme) | 1 | 1 | 1 |
|Exigence en matière de taille des volumes GFS |  |  |  | 18*|
\* La capacité totale inclut 17 Tio de disques StorSimple et 1 Tio de volume RAID local.


### <a name="gfs-example-schedule-gfs-rotation-weekly-monthly-and-yearly-schedule"></a>Exemple de planification GFS : planification de rotation GFS hebdomadaire, mensuelle et annuelle

| Semaine | Complet | Incrémentielle jour 1 | Incrémentielle jour 2 | Incrémentielle jour 3 | Incrémentielle jour 4 | Incrémentielle jour 5 |
|---|---|---|---|---|---|---|
| Semaine 1 | Volume RAID local  | Volume RAID local | Volume RAID local | Volume RAID local | Volume RAID local | Volume RAID local |
| Semaine 2 | StorSimple semaines 2 à 4 |   |   |   |   |   |
| Semaine 3 | StorSimple semaines 2 à 4 |   |   |   |   |   |
| Semaine 4 | StorSimple semaines 2 à 4 |   |   |   |   |   |
| Mensuelle | StorSimple mensuelle |   |   |   |   |   |
| Annuelle | StorSimple annuelle  |   |   |   |   |   |   |


### <a name="assign-storsimple-volumes-tooa-backup-exec-archive-and-deduplication-job"></a>Affecter StorSimple volumes tooa Backup Exec archive et la déduplication de travail

#### <a name="tooassign-storsimple-volumes-tooa-backup-exec-archive-and-duplication-job"></a>tooassign StorSimple volumes tooa Backup Exec travail et d’archivage duplication

1.  Dans la console de gestion hello Backup Exec, tâche hello que vous souhaitez que le volume de tooarchive tooa StorSimple, puis sélectionnez avec le bouton droit **propriétés de définition de la sauvegarde** > **modifier**.

    ![Console d’administration de Backup Exec, onglet des propriétés de définition de sauvegarde](./media/storsimple-configure-backup-target-using-backup-exec/image19.png)

2.  Sélectionnez **ajouter une étape** > **dupliquer tooDisk** > **modifier**.

    ![Console d’administration de Backup Exec, ajouter une étape](./media/storsimple-configure-backup-target-using-backup-exec/image20.png)

3.  Bonjour **dupliquer les Options** boîte de dialogue, sélectionnez hello valeurs toouse pour **Source** et **planification**.

    ![Console d’administration de Backup Exec, propriétés de définition de sauvegarde et options de duplication](./media/storsimple-configure-backup-target-using-backup-exec/image21.png)

4.  Bonjour **stockage** liste déroulante, le volume de StorSimple hello sélectionnez où vous souhaitez hello archive travail toostore hello données.

    ![Console d’administration de Backup Exec, propriétés de définition de sauvegarde et options de duplication](./media/storsimple-configure-backup-target-using-backup-exec/image22.png)

5.  Sélectionnez **Vérifiez**, puis sélectionnez hello **ne pas vérifier les données pour ce travail** case à cocher.

    ![Console d’administration de Backup Exec, propriétés de définition de sauvegarde et options de duplication](./media/storsimple-configure-backup-target-using-backup-exec/image23.png)

6.  Sélectionnez **OK**.

    ![Console d’administration de Backup Exec, propriétés de définition de sauvegarde et options de duplication](./media/storsimple-configure-backup-target-using-backup-exec/image24.png)

7.  Bonjour **sauvegarde** colonne, ajouter une nouvelle étape. Pour la source de hello, utilisez **incrémentielle**. Pour la cible de hello, choisissez hello volume StorSimple où la tâche de sauvegarde incrémentielle hello est archivée. Répétez les étapes 1 à 6.

## <a name="storsimple-cloud-snapshots"></a>Captures instantanées cloud StorSimple

Instantanés de cloud StorSimple protéger les données de hello qui réside dans votre appareil StorSimple. Création d’un instantané cloud est facilité de tooshipping équivalentes des bandes de sauvegarde local tooan hors site. Si vous utilisez un stockage géo-redondant Azure, la création d’un instantané cloud est sites de toomultiple tooshipping équivalent bandes de sauvegarde. Si vous devez toorestore un appareil après un sinistre, vous pouvez mettre un autre appareil StorSimple en ligne et effectuer un basculement. Après le basculement de hello, vous serez en mesure de tooaccess les données de hello (à des vitesses de cloud) à partir de l’instantané cloud le plus récent hello.

Hello suivant la section décrit comment toocreate un toostart script court et delete StorSimple instantanés cloud lors du post-traitement de la sauvegarde.

> [!NOTE]
> Instantanés créés manuellement ou par programmation ne suivent pas la stratégie d’expiration de hello StorSimple snapshot. Ces captures instantanées doivent être supprimées manuellement ou par programme.

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a>Démarrer et supprimer des captures instantanées cloud avec un script

> [!NOTE]
> Évaluer avec soin la conformité de hello et des répercussions de rétention de données avant de supprimer un instantané StorSimple. Pour plus d’informations sur la façon toorun un script de postsauvegarde, consultez hello [documentation de Backup Exec](https://www.veritas.com/support/en_US/15047.html).

### <a name="backup-lifecycle"></a>Cycle de vie de sauvegarde

![Diagramme du cycle de vie de sauvegarde](./media/storsimple-configure-backup-target-using-backup-exec/backuplifecycle.png)

### <a name="requirements"></a>Configuration requise

-   serveur Hello qui exécute le script de hello doit avoir à accéder aux ressources de cloud tooAzure.
-   compte d’utilisateur Hello doit avoir les autorisations nécessaires hello.
-   Une stratégie de sauvegarde StorSimple avec hello associés StorSimple volumes doivent être configurés mais pas sous tension.
-   Vous devez hello StorSimple nom de la ressource, la clé d’enregistrement, nom de l’appareil et ID de stratégie de sauvegarde.

### <a name="toostart-or-delete-a-cloud-snapshot"></a>toostart ou supprimer un instantané cloud

1.  [Installez Azure PowerShell](/powershell/azure/overview).
2.  [Téléchargez et importez les paramètres de publication et les informations d’abonnement](https://msdn.microsoft.com/library/dn385850.aspx).
3.  Dans l’hello portail Azure classic, obtenir le nom de la ressource hello et [clé d’inscription de votre service StorSimple Manager](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).
4.  Sur serveur hello qui exécute le script de hello, exécutez PowerShell en tant qu’administrateur. Tapez la commande suivante :

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    Code de note hello stratégie de sauvegarde.
5.  Dans le bloc-notes, créez un script PowerShell à l’aide de hello suivant de code.

    Copiez et collez cet extrait de code :
    ```powershell
    Import-AzurePublishSettingsFile "c:\\CloudSnapshot Snapshot\\myAzureSettings.publishsettings"
    Disable-AzureDataCollection
    $ApplianceName = <myStorSimpleApplianceName>
    $RetentionInDays = 20
    $RetentionInDays = -$RetentionInDays
    $Today = Get-Date
    $ExpirationDate = $Today.AddDays($RetentionInDays)
    Select-AzureStorSimpleResource -ResourceName "myResource" –RegistrationKey
    Start-AzureStorSimpleDeviceBackupJob –DeviceName $ApplianceName -BackupType CloudSnapshot -BackupPolicyId <BackupId> -Verbose
    $CompletedSnapshots =@()
    $CompletedSnapshots = Get-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName
    Write-Host "hello Expiration date is " $ExpirationDate
    Write-Host

    ForEach ($SnapShot in $CompletedSnapshots)
    {
        $SnapshotStartTimeStamp = $Snapshot.CreatedOn
        if ($SnapshotStartTimeStamp -lt $ExpirationDate)

        {
            $SnapShotInstanceID = $SnapShot.InstanceId
            Write-Host "This snpashotdate was created on " $SnapshotStartTimeStamp.Date.ToShortDateString()
            Write-Host "Instance ID " $SnapShotInstanceID
            Write-Host "This snpashotdate is older and needs toobe deleted"
            Write-host "\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#"
            Remove-AzureStorSimpleDeviceBackup -DeviceName $ApplianceName -BackupId $SnapShotInstanceID -Force -Verbose
        }
    }
    ```
      Enregistrement toohello de script PowerShell hello même emplacement où vous avez enregistré votre Azure de paramètres de publication. Par exemple, C:\CloudSnapshot\StorSimpleCloudSnapshot.ps1.
6.  Complément sauvegarde hello script tooyour en modifiant les pré-traitement vos options' travail Backup Exec et après le traitement des commandes Backup Exec.

    ![Console Backup Exec, options de sauvegarde, onglet de commandes de prétraitement et de post-traitement](./media/storsimple-configure-backup-target-using-backup-exec/image25.png)

> [!NOTE]
> Nous vous conseillons d’exécuter votre stratégie de sauvegarde d’instantané cloud StorSimple en tant que script de post-traitement à fin hello de votre tâche de sauvegarde quotidienne. Pour plus d’informations sur comment tooback configuration et restauration votre toohelp d’environnement de l’application de sauvegarde vous remplissez votre RPO et RTO, veuillez consulter avec votre architecte de sauvegarde.

## <a name="storsimple-as-a-restore-source"></a>Utiliser StorSimple comme source de restauration

Les restaurations à partir d’un appareil StorSimple fonctionnent comme les restaurations effectuées à partir de n’importe quel dispositif de stockage de bloc. Restaurations de données à plusieurs niveaux toohello cloud se produit à des vitesses de cloud. Pour les données locales, les restaurations se produisent à la vitesse du disque local hello du périphérique de hello. Pour plus d’informations sur la façon tooperform une restauration, consultez la documentation de Backup Exec de hello. Il est recommandé que vous conformer meilleures pratiques tooBackup Exec restauration.

## <a name="storsimple-failover-and-disaster-recovery"></a>Basculement et récupération d’urgence StorSimple

> [!NOTE]
> Pour les scénarios relatifs aux cibles de sauvegarde, l’appliance cloud StorSimple n’est pas prise en charge en tant que cible de restauration.

Un sinistre peut être dû à plusieurs facteurs. Hello tableau suivant répertorie les scénarios de récupération d’urgence courants.

| Scénario | Impact | Comment toorecover | Remarques |
|---|---|---|---|
| Défaillance d’appareil StorSimple | Les opérations de sauvegarde et de restauration sont interrompues. | Remplacer le périphérique avec échec hello et exécuter [StorSimple basculement et récupération d’urgence](storsimple-device-failover-disaster-recovery.md). | Si vous devez tooperform une restauration après la récupération de l’appareil, les jeux de travail complète des données sont extraites hello cloud toohello nouvel appareil. Toutes les opérations sont exécutées à la vitesse du cloud. Hello l’indexation et de catalogage réanalysant processus risque de tous les jeux de sauvegarde toobe, analysés et extraite hello cloud couche toohello appareil local niveau, qui peut prendre du temps. |
| Défaillance du serveur Backup Exec | Les opérations de sauvegarde et de restauration sont interrompues. | Reconstruire le serveur de sauvegarde hello et effectuer la restauration de la base de données comme détaillé dans [comment toodo une base de données de sauvegarde et restauration de sauvegarde Exec (BEDB) manuelle](http://www.veritas.com/docs/000041083). | Vous devez reconstruire ou restaurer hello sauvegarde Exec server sur site de récupération d’urgence hello. Hello de base de données toohello plus récent point de restauration. Si hello restaurés Backup Exec base de données n’est pas synchronisée avec vos travaux de sauvegarde plus récente, l’indexation et de catalogage est requis. Cet index et le catalogue une nouvelle analyse de processus risque de tous les jeux de sauvegarde toobe, analysées et extraites de la couche de hello cloud couche toohello périphérique local. Ce processus peut donc prendre un certain temps. |
| Défaillance du site qui entraîne la perte de hello du serveur de sauvegarde hello et StorSimple | Les opérations de sauvegarde et de restauration sont interrompues. | Commencez par restaurer StorSimple, puis restaurez Backup Exec. | Commencez par restaurer StorSimple, puis restaurez Backup Exec. Si vous devez tooperform une restauration après la récupération de l’appareil, jeux de travail hello complète des données est extraites hello cloud toohello nouvel appareil. Toutes les opérations sont exécutées à la vitesse du cloud. |

## <a name="references"></a>Références

Hello suivant les documents ont été référencé pour cet article :

- [StorSimple multipath I/O setup (Configuration de StorSimple MPIO)](storsimple-configure-mpio-windows-server.md)
- [Storage scenarios: Thin provisioning (Scénarios de stockage : allocation dynamique)](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [Using GPT drives (Utilisation de disques de table de partition GUID)](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [Set up shadow copies for shared folders (Configurer des clichés instantanés de dossiers partagés)](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur la façon trop[restauration à partir d’un jeu de sauvegarde](storsimple-restore-from-backup-set-u2.md).
- En savoir plus sur la façon tooperform [appareil basculement et récupération d’urgence](storsimple-device-failover-disaster-recovery.md).
