---
title: "série aaaStorSimple 8000 en tant que cible de sauvegarde avec NetBackup | Documents Microsoft"
description: "Décrit la configuration de cible de sauvegarde hello StorSimple avec Veritas NetBackup."
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
ms.date: 06/15/2017
ms.author: hkanna
ms.openlocfilehash: 7d032bbcf6e40e7609e51437e290fc92b232a48f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-netbackup"></a>StorSimple comme cible de sauvegarde avec NetBackup

## <a name="overview"></a>Vue d’ensemble

Azure StorSimple est une solution de stockage cloud hybride de Microsoft. StorSimple adresses complexités hello de croissance exponentielle des données à l’aide d’un compte de stockage Azure comme une extension de la solution locale de hello et automatiquement hiérarchisation des données sur le stockage local et le stockage cloud.

Dans cet article, nous traitons de l’intégration de StorSimple à NetBackup et des meilleures pratiques en matière d’intégration de ces deux solutions. Nous avons aussi formuler des recommandations sur comment intégrer des tooset de Veritas NetBackup toobest avec StorSimple. Nous différer tooVeritas meilleures pratiques, les architectes de sauvegarde et les administrateurs de hello meilleure manière tooset les exigences de sauvegarde individuelles de Veritas NetBackup toomeet et les contrats de niveau de service (SLA).

Bien que cet article illustre les étapes de configuration et les concepts clés, cela ne constitue en aucun cas un guide de configuration ou d’installation pas à pas. Nous partons du principe qu’infrastructure et des composants de base hello sont dans l’ordre de travail et prêt toosupport hello des concepts que nous décrivons.

### <a name="who-should-read-this"></a>Qui doit lire ce document ?

informations de Hello dans cet article seront plus utiles toobackup administrateurs, les administrateurs de stockage et les architectes de stockage qui ont une connaissance de stockage, Windows Server 2012 R2, Ethernet, services de cloud computing et Veritas NetBackup.

### <a name="supported-versions"></a>Versions prises en charge

-   NetBackup 7.7.x et versions ultérieures
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
![Diagramme de la hiérarchisation StorSimple](./media/storsimple-configure-backup-target-using-netbackup/image1.jpg)

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

![Diagramme logique de l’utilisation de StorSimple comme cible de sauvegarde principale](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetlogicaldiagram.png)

### <a name="primary-target-backup-logical-steps"></a>Procédure logique de sauvegarde de la cible principale

1.  contacts du serveur de sauvegarde Hello hello agent de sauvegarde cible et l’agent de sauvegarde hello transmet des données toohello sauvegarde du serveur.
2.  serveur de sauvegarde Hello écrit des données toohello StorSimple à plusieurs niveaux de volumes.
3.  serveur de sauvegarde Hello met à jour la base de données de catalogue hello et puis termine le travail de sauvegarde hello.
4.  Un script d’instantané déclenche le Gestionnaire d’instantanés StorSimple hello (début ou suppression).
5.  serveur de sauvegarde Hello supprime les sauvegardes ayant expirés basés sur une stratégie de rétention.

### <a name="primary-target-restore-logical-steps"></a>Procédure logique de restauration de la cible principale

1.  serveur de sauvegarde Hello démarre la restauration des données appropriées de hello à partir de l’espace de stockage hello.
2.  agent de sauvegarde Hello reçoit les données de hello hello serveur de sauvegarde.
3.  serveur de sauvegarde Hello termine le travail de restauration hello.

## <a name="storsimple-as-a-secondary-backup-target"></a>Utiliser StorSimple comme cible de sauvegarde secondaire

Dans ce scénario, les volumes StorSimple sont principalement utilisés à des fins de rétention à long terme ou d’archivage.

Hello figure suivante illustre une architecture dans laquelle les sauvegardes initiales et restaure le volume cible hautes performances. Ces sauvegardes sont copiées et archivée tooa StorSimple à plusieurs niveaux de volume sur une planification définie.

Il est important toosize votre volume hautes performances de sorte qu’elle puisse gérer vos conditions de performances et la capacité de stratégie de rétention.

![Diagramme logique de l’utilisation de StorSimple comme cible de sauvegarde secondaire](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetlogicaldiagram.png)

### <a name="secondary-target-backup-logical-steps"></a>Procédure logique de sauvegarde de la cible secondaire

1.  contacts du serveur de sauvegarde Hello hello agent de sauvegarde cible et l’agent de sauvegarde hello transmet des données toohello sauvegarde du serveur.
2.  serveur de sauvegarde Hello écrit stockage toohigh-performances des données.
3.  serveur de sauvegarde Hello met à jour la base de données de catalogue hello et puis termine le travail de sauvegarde hello.
4.  Bonjour tooStorSimple de sauvegardes de copies de sauvegarde du serveur basé sur une stratégie de rétention.
5.  Un script d’instantané déclenche le Gestionnaire d’instantanés StorSimple hello (début ou suppression).
6.  hello de suppressions de sauvegarde du serveur Hello expiré basés sur une stratégie de rétention des sauvegardes.

### <a name="secondary-target-restore-logical-steps"></a>Procédure logique de restauration de la cible secondaire

1.  serveur de sauvegarde Hello démarre la restauration des données appropriées de hello à partir de l’espace de stockage hello.
2.  agent de sauvegarde Hello reçoit les données de hello hello serveur de sauvegarde.
3.  serveur de sauvegarde Hello termine le travail de restauration hello.

## <a name="deploy-hello-solution"></a>Déployer la solution de hello

Trois étapes sont nécessaires pour le déploiement de la solution :
1. Préparer l’infrastructure de réseau hello.
2. Déployer votre appareil StorSimple comme cible de sauvegarde.
3. Déployer Veritas NetBackup.

Chaque étape est décrite en détail dans les sections suivantes de hello.

### <a name="set-up-hello-network"></a>La configuration du réseau de hello

StorSimple est une solution qui est intégrée à hello cloud Azure, StorSimple requiert une toohello connexion active et fonctionne cloud Azure. Cette connexion est utilisée pour les opérations telles que les instantanés cloud, gestion des données et le transfert de métadonnées et stockage en cloud tooAzure tootier des données plus anciennes et moins sollicitées.

Hello solution tooperform de façon optimale, nous vous recommandons que vous suivez ces conseils de mise en réseau :

-   lien Hello qui se connecte tooAzure de hiérarchisation hello StorSimple doit répondre aux besoins en bande passante. tooachieve, appliquer hello approprié qualité de Service (QoS) tooyour de niveau infrastructure commutateurs toomatch votre RPO et la récupération temps SLA d’objectif (RTO).

-   Les latences d’accès maximales au service Stockage Blob Azure doivent être de l’ordre de 80 ms.

### <a name="deploy-storsimple"></a>Déployer StorSimple

Pour découvrir un guide de déploiement de StorSimple pas à pas, consultez l’article [Déploiement de votre appareil StorSimple local](storsimple-deployment-walkthrough-u2.md).

### <a name="deploy-netbackup"></a>Déployer NetBackup

Pour obtenir des conseils de déploiement de 7.7.x NetBackup, consultez hello [NetBackup 7.7.x documentation](http://www.veritas.com/docs/000094423).

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

- N’utilisez pas de volumes fractionnés (créés par le Gestionnaire de disque Windows), car ces volumes ne sont pas pris en charge.
- Formatez vos volumes à l’aide du système de fichiers NTFS avec une taille d’allocation de 64 Ko.
- Mapper les volumes StorSimple hello directement toohello NetBackup server.
    - Utilisez iSCSI pour les serveurs physiques.
    - Utilisez des disques pass-through pour les serveurs virtuels.


## <a name="best-practices-for-storsimple-and-netbackup"></a>Meilleures pratiques pour StorSimple et NetBackup

Configurer votre solution en fonction des instructions toohello Bonjour les premières sections suivantes.

### <a name="operating-system-best-practices"></a>Meilleures pratiques concernant le système d’exploitation

-   Désactiver le chiffrement de Windows Server et la déduplication pour le système de fichiers NTFS hello.
-   Désactiver la défragmentation de Windows Server sur des volumes StorSimple hello.
-   Désactiver l’indexation sur hello de volumes StorSimple de Windows Server.
-   Exécuter une analyse antivirus sur l’hôte source de hello (et non sur des volumes StorSimple hello).
-   Désactiver la valeur par défaut hello [maintenance de Windows Server](https://msdn.microsoft.com/library/windows/desktop/hh848037.aspx) dans le Gestionnaire des tâches. Procédez comme suit dans un des hello suivant façons :
    - Désactiver le Configurateur de Maintenance hello dans le Planificateur de tâches Windows.
    - Téléchargez [PsExec](https://technet.microsoft.com/sysinternals/bb897553.aspx) à partir de Windows Sysinternals. Après avoir téléchargé PsExec, exécutez Windows PowerShell en tant qu’administrateur, puis tapez :
      ```powershell
      psexec \\%computername% -s schtasks /change /tn “MicrosoftWindowsTaskSchedulerMaintenance Configurator" /disable
      ```

### <a name="storsimple-best-practices"></a>Meilleures pratiques concernant StorSimple

-   Assurez-vous que l’appareil StorSimple hello est mis à jour trop[mise à jour 3 ou version ultérieure](storsimple-install-update-3.md).
-   Isolez le trafic iSCSI et cloud. Utiliser des connexions iSCSI dédié pour le trafic entre le serveur de sauvegarde StorSimple et hello.
-   Assurez-vous que l’appareil StorSimple est une cible de sauvegarde dédiée. Les charges de travail mixtes ne sont pas prises en charge, car elles affectent le RTO et le RPO.

### <a name="netbackup-best-practices"></a>Meilleures pratiques concernant NetBackup

-   base de données de NetBackup Hello doit être local toohello serveur et ne réside pas sur un volume StorSimple.
-   Récupération d’urgence, sauvegarder la base de données de NetBackup hello sur un volume StorSimple.
-   Nous prenons en charge les sauvegardes complètes et incrémentielles NetBackup (également désignée tooas différentielle des sauvegardes incrémentielles dans NetBackup) pour cette solution. Nous vous déconseillons d’utiliser les sauvegardes synthétiques et incrémentielles cumulatives.
-   Les fichiers de données de sauvegarde doivent contenir uniquement les données de salutation d’une tâche spécifique. Par exemple, aucun ajout de supports n’est autorisé entre les différents travaux.

Pourquoi NetBackup paramètres les plus récents et les meilleures pratiques pour l’implémentation de ces exigences, consultez documentation NetBackup hello [www.veritas.com](https://www.veritas.com).


## <a name="retention-policies"></a>Stratégies de rétention

Un des types de stratégie de rétention de sauvegarde les plus courants hello est une stratégie grand-père Père et fils (GFS). Dans une stratégie GFS, une sauvegarde incrémentielle est effectuée tous les jours et les sauvegardes complètes sont effectuées de façon hebdomadaire et mensuelle. Les résultats de cette stratégie de StorSimple six niveaux de volumes : un volume contient hello hebdomadaire, mensuel et annuel sauvegardes complètes ; Hello autres cinq volumes stockent des sauvegardes incrémentielles quotidiennes.

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

## <a name="set-up-netbackup-storage"></a>Configurer le stockage NetBackup

### <a name="tooset-up-netbackup-storage"></a>tooset NetBackup l’espace de stockage

1.  Dans la Console d’Administration NetBackup de hello, sélectionnez **support et la gestion des appareils** > **périphériques** > **des Pools de disques**. Bonjour Assistant de Configuration de Pool de disque, sélectionnez le type de serveur de stockage de hello **AdvancedDisk**, puis sélectionnez **suivant**.

    ![Console d’administration NetBackup, Assistant de configuration de pool de disques](./media/storsimple-configure-backup-target-using-netbackup/nbimage1.png)

2.  Sélectionnez votre serveur, puis **Next (Suivant)**.

    ![Console d’Administration NetBackup, serveur de hello select](./media/storsimple-configure-backup-target-using-netbackup/nbimage2.png)

3.  Sélectionnez votre volume StorSimple.

    ![Console d’Administration NetBackup, disque du volume StorSimple hello select](./media/storsimple-configure-backup-target-using-netbackup/nbimage3.png)

4.  Entrez un nom pour la cible de sauvegarde hello et sélectionnez **suivant** > **suivant** Assistant de hello toofinish.

5.  Passez en revue les paramètres hello et sélectionnez **Terminer**.

6.  À fin hello de chaque attribution de volume, modifiez hello stockage périphérique paramètres toomatch celles recommandées dans [meilleures pratiques pour StorSimple et NetBackup](#best-practices-for-storsimple-and-netbackup).

7. Répétez les étapes 1 à 6 jusqu’à avoir terminé d’affecter vos volumes StorSimple.

    ![Console d’administration NetBackup, configuration de disque](./media/storsimple-configure-backup-target-using-netbackup/nbimage5.png)

## <a name="set-up-storsimple-as-a-primary-backup-target"></a>Configurer StorSimple comme cible de sauvegarde principale

> [!NOTE]
> Restaurations de données à partir d’une sauvegarde qui a été toohello hiérarchisé cloud se produisent à des vitesses de cloud.

Hello figure suivante illustre mappage hello d’un travail de sauvegarde tooa volume classique. Dans ce cas, toutes les sauvegardes hebdomadaires hello mappent disque plein de toohello samedi, et les sauvegardes incrémentielles hello mappent les disques incrémentielle tooMonday-vendredi. Tous les hello des sauvegardes et de restaurations à partir d’un StorSimple à plusieurs niveaux de volume.

![Diagramme logique de la configuration de la cible de sauvegarde principale ](./media/storsimple-configure-backup-target-using-netbackup/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a>Exemple de planification GFS pour StorSimple comme cible de sauvegarde principale

Voici un exemple de planification de rotation GFS pour quatre semaines, mensuellement et annuellement :

| Fréquence/type de sauvegarde | Complet | Incrémentielle (jours 1-5)  |   
|---|---|---|
| Hebdomadaire (semaines 1-4) | Samedi | Lundi-vendredi |
| Mensuelle  | Samedi  |   |
| Annuelle | Samedi  |   |   |

## <a name="assigning-storsimple-volumes-tooa-netbackup-backup-job"></a>Affectation de tâche de sauvegarde StorSimple volumes tooa NetBackup

Hello suivant séquence suppose que cet hôte cible NetBackup et hello est configuré conformément aux instructions de l’agent NetBackup hello.

### <a name="tooassign-storsimple-volumes-tooa-netbackup-backup-job"></a>tooassign StorSimple volumes tooa NetBackup travail de sauvegarde

1.  Dans la Console d’Administration NetBackup de hello, sélectionnez **NetBackup gestion**, avec le bouton droit **stratégies**, puis sélectionnez **nouvelle stratégie**.

    ![Console d’administration NetBackup, création d’une stratégie](./media/storsimple-configure-backup-target-using-netbackup/nbimage6.png)

2.  Bonjour **ajouter une nouvelle stratégie** boîte de dialogue, entrez un nom pour la stratégie de hello et sélectionnez hello **utiliser l’Assistant Configuration de stratégie** case à cocher. Sélectionnez **OK**.

    ![Console d’administration NetBackup, boîte de dialogue d’ajout d’une nouvelle stratégie](./media/storsimple-configure-backup-target-using-netbackup/nbimage7.png)

3.  Dans l’Assistant de Configuration de stratégie de sauvegarde de hello, ectionnez hello type sauvegarde de votre choix, puis sélectionnez **suivant**.

    ![Console d’administration NetBackup, sélection du type de sauvegarde](./media/storsimple-configure-backup-target-using-netbackup/nbimage8.png)

4.  tooset hello stratégie, sélectionnez le type **Standard**, puis sélectionnez **suivant**.

    ![Console d’administration NetBackup, sélection du type de stratégie](./media/storsimple-configure-backup-target-using-netbackup/nbimage9.png)

5.  Sélectionnez votre hôte, sélectionnez hello **détecter le système d’exploitation client** case à cocher, puis sélectionnez **ajouter**. Sélectionnez **Suivant**.

    ![Console d’administration NetBackup, répertorier les clients dans une nouvelle stratégie](./media/storsimple-configure-backup-target-using-netbackup/nbimage10.png)

6.  Sélectionnez hello lecteurs tooback haut.

    ![Console d’administration NetBackup, sélections de sauvegarde pour une nouvelle stratégie](./media/storsimple-configure-backup-target-using-netbackup/nbimage11.png)

7.  Sélectionnez la fréquence de hello et de valeurs de rétention qui répondent à vos besoins de rotation des sauvegardes.

    ![Console d’administration NetBackup, fréquence et rotation de sauvegarde pour une nouvelle stratégie](./media/storsimple-configure-backup-target-using-netbackup/nbimage12.png)

8.  Sélectionnez **Next (Suivant)** > **Next (Suivant)** > **Finish (Terminer)**.  Vous pouvez modifier la planification de hello après que hello stratégie est créée.

9.  Sélectionnez stratégie hello tooexpand que vous venez créé, puis **planifications**.

    ![Console d’administration NetBackup, planifications pour une nouvelle stratégie](./media/storsimple-configure-backup-target-using-netbackup/nbimage13.png)

10.  Avec le bouton droit **différentielle-Inc**, sélectionnez **copier toonew**, puis sélectionnez **OK**.

    ![Console d’Administration NetBackup, copie planification tooa nouvelle stratégie](./media/storsimple-configure-backup-target-using-netbackup/nbimage14.png)

11.  Avec le bouton droit de la planification de hello qui vient d’être créé, puis sélectionnez **modification**.

12.  Sur hello **attributs** onglet, sélectionnez hello **remplacer la sélection de la stratégie stockage** case à cocher et volume hello puis sélectionnez où lundi adresser les sauvegardes incrémentielles.

    ![Console d’administration NetBackup, modifier la planification](./media/storsimple-configure-backup-target-using-netbackup/nbimage15.png)

13.  Sur hello **fenêtre Démarrer** onglet, la fenêtre de temps sélectionnez hello pour vos sauvegardes.

    ![Console d’administration NetBackup, modifier la fenêtre de démarrage](./media/storsimple-configure-backup-target-using-netbackup/nbimage16.png)

14.  Sélectionnez **OK**.

15.  Répétez les étapes 10 à 14 pour chaque sauvegarde incrémentielle. Sélectionnez le volume approprié de hello et de planification pour chaque sauvegarde que vous créez.

16.  Avec le bouton hello **différentielle-Inc** planifier, puis supprimez-le.

17.  Modifiez votre toomeet de planification de sauvegarde complète qu'a besoin de votre sauvegarde.

    ![Console d’administration NetBackup, modifier la planification complète](./media/storsimple-configure-backup-target-using-netbackup/nbimage17.png)

18.  Changement de fenêtre Démarrer hello.

    ![Console d’Administration NetBackup, changement de fenêtre hello début](./media/storsimple-configure-backup-target-using-netbackup/nbimage18.png)

19.  planification de Hello final ressemble à ceci :

    ![Console d’administration NetBackup, planification finale](./media/storsimple-configure-backup-target-using-netbackup/nbimage19.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a>Configurer StorSimple comme cible de sauvegarde secondaire

> [!NOTE]
>Restaurations de données à partir d’une sauvegarde qui a été toohello hiérarchisé cloud se produisent à des vitesses de cloud.

Dans ce modèle, vous devez avoir un tooserve de support (autres que StorSimple) de stockage comme un cache temporaire. Par exemple, vous pouvez utiliser une baie redondante de disques indépendants (RAID) volume tooaccommodate d’espace, d’entrée/sortie (e/s) et la bande passante. Nous vous recommandons d’utiliser les valeurs RAID 5, 50 et 10.

Hello figure suivante montre à court terme rétention type locale (serveur toohello) volumes les archives des volumes et rétention à long terme. Dans ce scénario, toutes les sauvegardes se hello local (serveur toohello) volume RAID. Ces sauvegardes sont dupliquées régulièrement et archivée tooan archive volume. Il est important toosize local (serveur toohello) volume RAID afin qu’il puisse gérer vos exigences de capacité et de performances rétention à court terme.

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a>Exemple GFS pour StorSimple utilisé comme cible de sauvegarde secondaire

![Diagramme logique de l’utilisation de StorSimple comme cible de sauvegarde secondaire](./media/storsimple-configure-backup-target-using-netbackup/secondarybackuptargetdiagram.png)

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


## <a name="assign-storsimple-volumes-tooa-netbackup-archive-and-duplication-job"></a>Affecter StorSimple volumes tooa NetBackup archive et la duplication de travail

NetBackup propose un large éventail d’options pour la gestion du stockage et de support, nous vous recommandons que vous consultez avec Veritas ou votre tooproperly d’architecte NetBackup évaluer vos besoins de la stratégie (SLP) de cycle de vie de stockage.

Une fois que vous avez défini des pools de disque initiale hello, vous devez toodefine trois stratégies de cycle de vie du stockage supplémentaire, pour un total de quatre stratégies :
* LocalRAIDVolume (VolumeRAIDLocal)
* StorSimpleWeek2-4 (StorSimpleSemaines2-4)
* StorSimpleMonthlyFulls (StorSimpleComplètesMensuelles)
* StorSimpleYearlyFulls (StorSimpleComplètesAnnuelles)

### <a name="tooassign-storsimple-volumes-tooa-netbackup-archive-and-duplication-job"></a>tooassign StorSimple volumes tooa NetBackup travail et d’archivage duplication

1.  Dans la Console d’Administration NetBackup de hello, sélectionnez **stockage** > **stratégies de cycle de vie de stockage** > **stratégie de cycle de vie de stockage**.

    ![Console d’administration de NetBackup, nouvelle stratégie de cycle de vie du stockage](./media/storsimple-configure-backup-target-using-netbackup/nbimage20.png)

2.  Entrez un nom pour la capture instantanée de hello et sélectionnez **ajouter**.

3.  Bonjour **nouvelle opération** la boîte de dialogue hello **propriétés** onglet, pour **opération**, sélectionnez **sauvegarde**. Sélectionnez valeurs hello pour **stockage de Destination**, **type de rétention**, et **période de rétention**. Sélectionnez **OK**.

    ![Console d’administration NetBackup, boîte de dialogue Nouvelle opération](./media/storsimple-configure-backup-target-using-netbackup/nbimage22.png)

    Cela définit le référentiel et la première opération de sauvegarde hello.

4.  Sélectionnez une opération précédente toohighlight hello, puis **ajouter**. Bonjour **opération de modification du stockage** boîte de dialogue, sélectionnez hello voulus pour **stockage de Destination**, **type de rétention**, et **période de rétention** .

    ![Console d’administration NetBackup, boîte de dialogue Modifier l’opération de sauvegarde](./media/storsimple-configure-backup-target-using-netbackup/nbimage23.png)

5.  Sélectionnez une opération précédente toohighlight hello, puis **ajouter**. Bonjour **stratégie de cycle de vie de stockage** boîte de dialogue zone, ajouter des sauvegardes mensuelles pour une année.

    ![Console d’administration de NetBackup, boîte de dialogue Nouvelle stratégie de cycle de vie du stockage](./media/storsimple-configure-backup-target-using-netbackup/nbimage24.png)

6.  Répétez les étapes 4 à 5 jusqu'à ce que vous avez créé hello complète SLP stratégie de rétention que vous avez besoin.

    ![Console d’Administration NetBackup, ajouter des stratégies dans la boîte de dialogue Nouvelle stratégie de cycle de vie de stockage hello](./media/storsimple-configure-backup-target-using-netbackup/nbimage25.png)

7.  Lorsque vous avez terminé de définir votre stratégie de rétention SLP sous **stratégie**, définir une stratégie de sauvegarde en suivant les étapes hello détaillées dans [tâche de sauvegarde StorSimple d’affectation de volumes tooa NetBackup](#assigning-storsimple-volumes-to-a-netbackup-backup-job).

8.  Sous **planifications**, Bonjour **modifier la planification** boîte de dialogue, avec le bouton droit **complète**, puis sélectionnez **modification**.

    ![Console d’administration NetBackup, boîte de dialogue Modifier la planification](./media/storsimple-configure-backup-target-using-netbackup/nbimage26.png)

9.  Sélectionnez hello **remplacer la sélection de la stratégie stockage** case à cocher, puis sélectionnez hello SLP de rétention que vous avez créé dans les étapes 1 à 6.

    ![Console d’Administration NetBackup, Écraser la sélection de stratégie de stockage](./media/storsimple-configure-backup-target-using-netbackup/nbimage27.png)

10.  Sélectionnez **OK**, puis répétez pour la planification de sauvegarde incrémentielle hello.

    ![Console d’administration NetBackup, boîte de dialogue Modifier la planification pour les sauvegardes incrémentielles](./media/storsimple-configure-backup-target-using-netbackup/nbimage28.png)


| Type de sauvegarde et rétention | Taille (Tio) | Multiplicateur GFS\* | Capacité totale (Tio)  |
|---|---|---|---|
| Complète hebdomadaire |  1  |  4 | 4  |
| Incrémentielle quotidienne  | 0.5  | 20 (cycles sont nombre toohello égal de semaines par mois) | 12 (2 pour le quota supplémentaire) |
| Complète mensuelle  | 1 | 12 | 12 |
| Complète annuelle | 1  | 10 | 10 |
| Exigence GFS  |     |     | 38 |
| Quota supplémentaire  | 4  |    | 42 au total pour l’exigence GFS |
\*nombre de hello est Hello multiplicateur GFS de copies vous devez tooprotect et conserver toomeet vos exigences de stratégie de sauvegarde.

## <a name="storsimple-cloud-snapshots"></a>Captures instantanées cloud StorSimple

Instantanés de cloud StorSimple protéger les données de hello qui réside dans votre appareil StorSimple. Création d’un instantané cloud est facilité de tooshipping équivalentes des bandes de sauvegarde local tooan hors site. Si vous utilisez un stockage géo-redondant Azure, la création d’un instantané cloud est sites de toomultiple tooshipping équivalent bandes de sauvegarde. Si vous devez toorestore un appareil après un sinistre, vous pouvez mettre un autre appareil StorSimple en ligne et effectuer un basculement. Après le basculement de hello, vous serez en mesure de tooaccess les données de hello (à des vitesses de cloud) à partir de l’instantané cloud le plus récent hello.

Hello suivant la section décrit comment toocreate un toostart script court et delete StorSimple instantanés cloud lors du post-traitement de la sauvegarde.

> [!NOTE]
> Instantanés créés manuellement ou par programmation ne suivent pas la stratégie d’expiration de hello StorSimple snapshot. Ces captures instantanées doivent être supprimées manuellement ou par programme.

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a>Démarrer et supprimer des captures instantanées cloud avec un script

> [!NOTE]
> Évaluer avec soin la conformité de hello et des répercussions de rétention de données avant de supprimer un instantané StorSimple. Pour plus d’informations sur la façon toorun un script de postsauvegarde, consultez hello [NetBackup documentation](http://www.veritas.com/docs/000094423).

### <a name="backup-lifecycle"></a>Cycle de vie de sauvegarde

![Diagramme du cycle de vie de sauvegarde](./media/storsimple-configure-backup-target-using-netbackup/backuplifecycle.png)

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
6.  Ajouter le travail de sauvegarde tooyour script hello dans NetBackup. toodo, modifier votre NetBackup travail options' prétraitement et après le traitement des commandes.

> [!NOTE]
> Nous vous conseillons d’exécuter votre stratégie de sauvegarde d’instantané cloud StorSimple en tant que script de post-traitement à fin hello de votre tâche de sauvegarde quotidienne. Pour plus d’informations sur comment tooback configuration et restauration votre toohelp d’environnement de l’application de sauvegarde vous remplissez votre RPO et RTO, veuillez consulter avec votre architecte de sauvegarde.

## <a name="storsimple-as-a-restore-source"></a>Utiliser StorSimple comme source de restauration

Les restaurations à partir d’un appareil StorSimple fonctionnent comme les restaurations effectuées à partir de n’importe quel dispositif de stockage de bloc. Restaurations de données à plusieurs niveaux toohello cloud se produit à des vitesses de cloud. Pour les données locales, les restaurations se produisent à la vitesse du disque local hello du périphérique de hello. Pour plus d’informations sur la façon tooperform une restauration, consultez hello [NetBackup documentation](http://www.veritas.com/docs/000094423). Il est recommandé que vous conformer tooNetBackup restauration meilleures pratiques.

## <a name="storsimple-failover-and-disaster-recovery"></a>Basculement et récupération d’urgence StorSimple

> [!NOTE]
> Pour les scénarios relatifs aux cibles de sauvegarde, l’appliance cloud StorSimple n’est pas prise en charge en tant que cible de restauration.

Un sinistre peut être dû à plusieurs facteurs. Hello tableau suivant répertorie les scénarios de récupération d’urgence courants.

| Scénario | Impact | Comment toorecover | Remarques |
|---|---|---|---|
| Défaillance d’appareil StorSimple | Les opérations de sauvegarde et de restauration sont interrompues. | Remplacer le périphérique avec échec hello et exécuter [StorSimple basculement et récupération d’urgence](storsimple-device-failover-disaster-recovery.md). | Si vous devez tooperform une restauration après la récupération de l’appareil, les jeux de travail complète des données sont extraites hello cloud toohello nouvel appareil. Toutes les opérations sont exécutées à la vitesse du cloud. index de Hello et le catalogue une nouvelle analyse de processus risque de tous les jeux de sauvegarde toobe, analysés et extraite hello cloud couche toohello appareil local niveau, qui peut prendre du temps. |
| Défaillance du serveur NetBackup | Les opérations de sauvegarde et de restauration sont interrompues. | Reconstruire le serveur de sauvegarde hello et restaurez la base de données. | Vous devez reconstruire ou restaurer hello NetBackup server sur site de récupération d’urgence hello. Hello de base de données toohello plus récent point de restauration. Si hello NetBackup base de données restaurée n’est pas synchronisée avec vos travaux de sauvegarde plus récente, l’indexation et de catalogage sont requis. Cet index et le catalogue une nouvelle analyse de processus risque de tous les jeux de sauvegarde toobe, analysées et extraites de la couche de hello cloud couche toohello périphérique local. Ce processus peut donc prendre un certain temps. |
| Défaillance du site qui entraîne la perte de hello du serveur de sauvegarde hello et StorSimple | Les opérations de sauvegarde et de restauration sont interrompues. | Commencez par restaurer StorSimple, puis restaurez NetBackup. | Commencez par restaurer StorSimple, puis restaurez NetBackup. Si vous devez tooperform une restauration après la récupération de l’appareil, jeux de travail hello complète des données est extraites hello cloud toohello nouvel appareil. Toutes les opérations sont exécutées à la vitesse du cloud. |

## <a name="references"></a>Références

Hello suivant les documents ont été référencé pour cet article :

- [StorSimple multipath I/O setup (Configuration de StorSimple MPIO)](storsimple-configure-mpio-windows-server.md)
- [Storage scenarios: Thin provisioning (Scénarios de stockage : allocation dynamique)](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [Using GPT drives (Utilisation de disques de table de partition GUID)](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [Set up shadow copies for shared folders (Configurer des clichés instantanés de dossiers partagés)](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur la façon trop[restauration à partir d’un jeu de sauvegarde](storsimple-restore-from-backup-set-u2.md).
- En savoir plus sur la façon tooperform [appareil basculement et récupération d’urgence](storsimple-device-failover-disaster-recovery.md).
