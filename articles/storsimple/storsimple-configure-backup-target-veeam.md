---
title: "série aaaStorSimple 8000 en tant que cible de sauvegarde avec Veeam | Documents Microsoft"
description: "Décrit la configuration de cible de sauvegarde hello StorSimple avec Veeam."
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
ms.date: 12/06/2016
ms.author: hkanna
ms.openlocfilehash: 74a4af307fab430942f94b3e28f514a9abce227b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-as-a-backup-target-with-veeam"></a>StorSimple comme cible de sauvegarde avec Veeam

## <a name="overview"></a>Vue d'ensemble

Azure StorSimple est une solution de stockage cloud hybride de Microsoft. StorSimple adresses complexités hello de croissance exponentielle des données à l’aide d’un compte Azure Storage comme une extension de la solution locale de hello et automatiquement hiérarchisation des données sur le stockage local et le stockage cloud.

Dans cet article, nous traitons de l’intégration de StorSimple à Veeam et des meilleures pratiques en matière d’intégration de ces deux solutions. Nous avons également de recommandations sur comment intégrer des tooset des Veeam toobest avec StorSimple. Nous différer tooVeeam meilleures pratiques, les architectes de sauvegarde et les administrateurs de hello meilleure manière tooset les exigences de sauvegarde individuelles de Veeam toomeet et les contrats de niveau de service (SLA).

Bien que cet article illustre les étapes de configuration et les concepts clés, cela ne constitue en aucun cas un guide de configuration ou d’installation pas à pas. Nous partons du principe qu’infrastructure et des composants de base hello sont dans l’ordre de travail et prêt toosupport hello des concepts que nous décrivons.

### <a name="who-should-read-this"></a>Qui doit lire ce document ?

informations de Hello dans cet article seront plus utiles toobackup administrateurs, les administrateurs de stockage et les architectes de stockage qui ont une connaissance de stockage, Windows Server 2012 R2, Ethernet, services de cloud computing et Veeam.

### <a name="supported-versions"></a>Versions prises en charge

-   Veeam 9 et versions ultérieures
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
![Diagramme de la hiérarchisation StorSimple](./media/storsimple-configure-backup-target-using-veeam/image1.jpg)

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

| Capacité de stockage | 8100 | 8600 |
|---|---|---|
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

![Diagramme logique de l’utilisation de StorSimple comme cible de sauvegarde principale](./media/storsimple-configure-backup-target-using-veeam/primarybackuptargetlogicaldiagram.png)

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

![Diagramme logique de l’utilisation de StorSimple comme cible de sauvegarde secondaire](./media/storsimple-configure-backup-target-using-veeam/secondarybackuptargetlogicaldiagram.png)

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
3. Déployer Veeam.

Chaque étape est décrite en détail dans les sections suivantes de hello.

### <a name="set-up-hello-network"></a>La configuration du réseau de hello

StorSimple est une solution qui est intégrée à hello cloud Azure, StorSimple requiert une toohello connexion active et fonctionne cloud Azure. Cette connexion est utilisée pour les opérations telles que les instantanés cloud, gestion des données et le transfert de métadonnées et stockage en cloud tooAzure tootier des données plus anciennes et moins sollicitées.

Hello solution tooperform de façon optimale, nous vous recommandons que vous suivez ces conseils de mise en réseau :

-   lien Hello qui se connecte votre tooAzure hiérarchisation StorSimple doit répondre à vos besoins en bande passante. Cela en appliquant hello nécessaire qualité de Service (QoS) tooyour de niveau infrastructure commutateurs toomatch votre RPO et récupération (objectif) SLA de temps.
-   Les latences d’accès maximales au service Stockage Blob Azure doivent être de l’ordre de 80 ms.

### <a name="deploy-storsimple"></a>Déployer StorSimple

Pour découvrir un guide de déploiement de StorSimple pas à pas, consultez l’article [Déploiement de votre appareil StorSimple local](storsimple-deployment-walkthrough-u2.md).

### <a name="deploy-veeam"></a>Déployer Veeam

Pour Veeam meilleures pratiques pour l’installation, consultez [Veeam sauvegarde & réplication meilleures pratiques](https://bp.veeam.expert/), et de lire le guide de l’utilisateur à hello [Veeam centre d’aide (Documentation technique)](https://www.veeam.com/documentation-guides-datasheets.html).

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

- N’utilisez pas des volumes fractionnés (créés par le Gestionnaire de disque Windows). Les volumes fractionnés ne sont pas pris en charge.
- Formatez vos volumes à l’aide du système de fichiers NTFS avec une taille d’unité d’allocation de 64 Ko.
- Mapper les volumes StorSimple hello directement le serveur de Veeam toohello.
    - Utilisez iSCSI pour les serveurs physiques.


## <a name="best-practices-for-storsimple-and-veeam"></a>Meilleures pratiques pour StorSimple et Veeam

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

### <a name="veeam-best-practices"></a>Meilleures pratiques concernant Veeam

-   base de données de Veeam Hello doit être local toohello serveur et ne réside pas sur un volume StorSimple.
-   Récupération d’urgence, sauvegarder hello Veeam base de données sur un volume StorSimple.
-   Nous prenons en charge les sauvegardes complètes et incrémentielles Veeam pour cette solution. Nous vous déconseillons d’utiliser les sauvegardes synthétiques et différentielles.
-   Les fichiers de données de sauvegarde doivent contenir uniquement les données de salutation d’une tâche spécifique. Par exemple, aucun ajout de supports n’est autorisé entre les différents travaux.
-   Désactivez la vérification des travaux. Si nécessaire, la vérification doit être planifiée après le dernier travail de sauvegarde hello. Il est important toounderstand que ce travail affecte votre fenêtre de sauvegarde.
-   Activez la préallocation de supports.
-   Vérifiez que le traitement parallèle est activé.
-   Désactivez la compression.
-   Désactiver la déduplication sur le travail de sauvegarde hello.
-   Définir l’optimisation trop**LAN cible**.
-   Activez l’option **Create active full backup (Créer une sauvegarde complète active)** (toutes les 2 semaines).
-   Dans le référentiel de sauvegarde hello, configurez **utiliser les fichiers de sauvegarde par ordinateur virtuel**.
-   Définissez **utiliser plusieurs flux de téléchargement par travail** trop**8** (un maximum de 16 est autorisé). Ajustez ce nombre vers le haut ou vers le bas en fonction de l’utilisation du processeur sur l’appareil StorSimple hello.

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

## <a name="set-up-veeam-storage"></a>Configurer le stockage Veeam

### <a name="tooset-up-veeam-storage"></a>tooset Veeam l’espace de stockage

1.  Dans hello Veeam sauvegarde et de la console de réplication dans **référentiel outils**, accédez trop**Infrastructure de sauvegarde**. Cliquez avec le bouton droit sur **Backup Repositories (Référentiels de sauvegarde)**, puis sélectionnez **Add Backup Repository (Ajouter un référentiel de sauvegarde)**.

    ![Console d’administration de Veeam, page du référentiel de sauvegarde](./media/storsimple-configure-backup-target-using-veeam/veeamimage1.png)

2.  Bonjour **nouveau référentiel sauvegarde** boîte de dialogue, entrez un nom et une description pour le référentiel de hello. Sélectionnez **Suivant**.

    ![Console d’administration de Veeam, page de saisie d’un nom et d’une description](./media/storsimple-configure-backup-target-using-veeam/veeamimage2.png)

3.  Pour le type de hello, sélectionnez **Microsoft Windows server**. Sélectionnez le serveur de Veeam hello. Sélectionnez **Suivant**.

    ![Console d’administration de Veeam, sélection du type de référentiel de sauvegarde](./media/storsimple-configure-backup-target-using-veeam/veeamimage3.png)

4.  toospecify **emplacement**, recherchez et sélectionnez le volume hello. Sélectionnez hello **limiter le nombre maximum de tâches simultanées pour :** case à cocher et ensemble hello valeur trop**4**. Ceci garantit le fait que seulement quatre disques virtuels sont traités simultanément lorsque chaque machine virtuelle est traitée. Sélectionnez hello **avancé** bouton.

    ![Console d’administration de Veeam, sélection du volume](./media/storsimple-configure-backup-target-using-veeam/veeamimage4.png)


5.  Bonjour **les paramètres de compatibilité de stockage** boîte de dialogue, sélectionnez hello **utiliser les fichiers de sauvegarde par ordinateur virtuel** case à cocher.

    ![Console de gestion Veeam, paramètres de conformité de stockage](./media/storsimple-configure-backup-target-using-veeam/veeamimage5.png)

6.  Bonjour **nouveau référentiel sauvegarde** boîte de dialogue, sélectionnez hello **activer le service NFS vPower sur le serveur de montage hello (recommandé)** case à cocher. Sélectionnez **Suivant**.

    ![Console d’administration de Veeam, page du référentiel de sauvegarde](./media/storsimple-configure-backup-target-using-veeam/veeamimage6.png)

7.  Passez en revue les paramètres hello et sélectionnez **suivant**.

    ![Console d’administration de Veeam, page du référentiel de sauvegarde](./media/storsimple-configure-backup-target-using-veeam/veeamimage7.png)

    Un référentiel est ajouté toohello Veeam server.

## <a name="set-up-storsimple-as-a-primary-backup-target"></a>Configurer StorSimple comme cible de sauvegarde principale

> [!IMPORTANT]
> Restauration des données à partir d’une sauvegarde qui a été toohello hiérarchisé cloud se produit à des vitesses de cloud.

Hello figure suivante illustre mappage hello d’un travail de sauvegarde tooa volume classique. Dans ce cas, toutes les sauvegardes hebdomadaires hello mappent disque plein de toohello samedi, et les sauvegardes incrémentielles hello mappent les disques incrémentielle tooMonday-vendredi. Tous les hello des sauvegardes et de restaurations à partir d’un StorSimple à plusieurs niveaux de volume.

![Diagramme logique de la configuration de la cible de sauvegarde principale](./media/storsimple-configure-backup-target-using-veeam/primarybackuptargetdiagram.png)

### <a name="storsimple-as-a-primary-backup-target-gfs-schedule-example"></a>Exemple de planification GFS pour StorSimple comme cible de sauvegarde principale

Voici un exemple de planification de rotation GFS pour quatre semaines, mensuellement et annuellement :

| Fréquence/type de sauvegarde | Complet | Incrémentielle (jours 1-5)  |   
|---|---|---|
| Hebdomadaire (semaines 1-4) | Samedi | Lundi-vendredi |
| Mensuelle  | Samedi  |   |
| Annuelle | Samedi  |   |   |


### <a name="assign-storsimple-volumes-tooa-veeam-backup-job"></a>Assigner du travail de sauvegarde StorSimple volumes tooa Veeam

Pour le scénario de cible de sauvegarde principale, créez un travail quotidien avec votre volume Veeam StorSimple principal. Pour un scénario de cible de sauvegarde secondaire, créez un travail quotidien à l’aide du stockage DAS, NAS ou d’un stockage JBOD.

#### <a name="tooassign-storsimple-volumes-tooa-veeam-backup-job"></a>tooassign StorSimple volumes tooa Veeam du travail de sauvegarde

1.  Dans hello Veeam sauvegarde et la console de réplication, sélectionnez **de sauvegarde et de réplication**. Cliquez avec le bouton droit sur **Backup (Sauvegarde)**, puis sélectionnez **VMware** ou **Hyper-V** en fonction de votre environnement.

    ![Console d’administration de Veeam, nouveau travail de sauvegarde](./media/storsimple-configure-backup-target-using-veeam/veeamimage8.png)

2.  Bonjour **nouvelle opération de sauvegarde** boîte de dialogue, entrez un nom et une description pour le travail de sauvegarde quotidien hello.

    ![Console d’administration de Veeam, page du nouveau travail de sauvegarde](./media/storsimple-configure-backup-target-using-veeam/veeamimage9.png)

3.  Sélectionnez un ordinateur virtuel de tooback jusqu'à.

    ![Console d’administration de Veeam, page du nouveau travail de sauvegarde](./media/storsimple-configure-backup-target-using-veeam/veeamimage10.png)

4.  Sélectionnez valeurs hello pour **sauvegarde proxy** et **référentiel de sauvegarde**. Sélectionnez une valeur pour **tookeep des points de restauration sur disque** selon toohello définitions RPO et RTO pour votre environnement sur localement de stockage connecté. Sélectionnez **Advanced (Avancé)**.

    ![Console d’administration de Veeam, page du nouveau travail de sauvegarde](./media/storsimple-configure-backup-target-using-veeam/veeamimage11.png)

5. Bonjour **paramètres avancés** la boîte de dialogue hello **sauvegarde** onglet, sélectionnez **incrémentiel**. Veillez à ce que hello **créé régulièrement des sauvegardes complètes synthétiques** case à cocher est désactivée. Sélectionnez hello **créé régulièrement des sauvegardes complètes actives** case à cocher. Sous **sauvegarde complète Active**, sélectionnez hello **toutes les semaines pour les jours sélectionnés** case à cocher pour le samedi.

    ![Console d’administration de Veeam, page de paramètres avancés du nouveau travail de sauvegarde](./media/storsimple-configure-backup-target-using-veeam/veeamimage12.png)

6. Sur hello **stockage** onglet, vérifiez que hello **activer la déduplication des données d’inline** case à cocher est désactivée. Sélectionnez hello **blocs de fichiers d’échange exclure** case à cocher et sélectionnez hello **exclure supprimé des blocs de fichiers** case à cocher. Définissez **niveau de Compression** trop**aucun**. Pour la déduplication et de performances à charge équilibrée, définissez **l’optimisation du stockage** trop**cible de réseau local**. Sélectionnez **OK**.

    ![Console d’administration de Veeam, page de paramètres avancés du nouveau travail de sauvegarde](./media/storsimple-configure-backup-target-using-veeam/veeamimage13.png)

    Pour plus d’informations sur les paramètres de déduplication et de compression de Veeam, consultez l’article [Data Compression and Deduplication (Compression et déduplication des données)](https://helpcenter.veeam.com/backup/vsphere/compression_deduplication.html).

7.  Bonjour **modifier un travail de sauvegarde** boîte de dialogue, vous pouvez sélectionner hello **activer le traitement de l’application prenant en charge** case (facultatif).

    ![Console d’administration de Veeam, page de traitement de système d’exploitation invité du nouveau travail de sauvegarde](./media/storsimple-configure-backup-target-using-veeam/veeamimage14.png)

8.  Définissez hello planification toorun une fois par jour, à la fois, que vous pouvez spécifier.

    ![Console d’administration de Veeam, page de planification du nouveau travail de sauvegarde](./media/storsimple-configure-backup-target-using-veeam/veeamimage15.png)

## <a name="set-up-storsimple-as-a-secondary-backup-target"></a>Configurer StorSimple comme cible de sauvegarde secondaire

> [!NOTE]
> Restaurations de données à partir d’une sauvegarde qui a été toohello hiérarchisé cloud se produisent à des vitesses de cloud.

Dans ce modèle, vous devez avoir un tooserve de support (autres que StorSimple) de stockage comme un cache temporaire. Par exemple, vous pouvez utiliser une baie redondante de disques indépendants (RAID) volume tooaccommodate d’espace, d’entrée/sortie (e/s) et la bande passante. Nous vous recommandons d’utiliser les valeurs RAID 5, 50 et 10.

Hello figure suivante montre classique volumes local (serveur toohello) de rétention à court terme et les volumes d’archives de rétention à long terme. Dans ce scénario, toutes les sauvegardes se hello local (serveur toohello) volume RAID. Ces sauvegardes sont dupliquées régulièrement et archivées tooan archiver le volume. Il est important toosize local (serveur toohello) volume RAID afin qu’il puisse gérer vos exigences de capacité et de performances rétention à court terme.

![Diagramme logique de l’utilisation de StorSimple comme cible de sauvegarde secondaire](./media/storsimple-configure-backup-target-using-veeam/secondarybackuptargetdiagram.png)

### <a name="storsimple-as-a-secondary-backup-target-gfs-example"></a>Exemple GFS pour StorSimple utilisé comme cible de sauvegarde secondaire

tableau Hello suivant montre comment tooset des toorun de sauvegardes sur hello local et les disques de StorSimple. Il inclut les besoins en capacité individuelle et totale.

| Type de sauvegarde et rétention | Stockage configuré | Taille (Tio) | Multiplicateur GFS | Capacité totale\* (Tio) |
|---|---|---|---|---|
| Semaine 1 (sauvegardes complètes et incrémentielles) |Disque local (court terme)| 1 | 1 | 1 |
| StorSimple semaines 2 à 4 |Disque StorSimple (long terme) | 1 | 4 | 4 |
| Complète mensuelle |Disque StorSimple (long terme) | 1 | 12 | 12 |
| Complète annuelle |Disque StorSimple (long terme) | 1 | 1 | 1 |
|Exigence en matière de taille des volumes GFS |  |  |  | 18*|
\* La capacité totale inclut 17 Tio de disques StorSimple et 1 Tio de volume RAID local.


### <a name="gfs-example-schedule"></a>Exemple de planification GFS :

planification de rotation GFS hebdomadaire, mensuelle et annuelle

| Semaine | Complet | Incrémentielle jour 1 | Incrémentielle jour 2 | Incrémentielle jour 3 | Incrémentielle jour 4 | Incrémentielle jour 5 |
|---|---|---|---|---|---|---|
| Semaine 1 | Volume RAID local  | Volume RAID local | Volume RAID local | Volume RAID local | Volume RAID local | Volume RAID local |
| Semaine 2 | StorSimple semaines 2 à 4 |   |   |   |   |   |
| Semaine 3 | StorSimple semaines 2 à 4 |   |   |   |   |   |
| Semaine 4 | StorSimple semaines 2 à 4 |   |   |   |   |   |
| Mensuelle | StorSimple mensuelle |   |   |   |   |   |
| Annuelle | StorSimple annuelle  |   |   |   |   |   |   |

### <a name="assign-storsimple-volumes-tooa-veeam-copy-job"></a>Affecter le travail de copie StorSimple volumes tooa Veeam

#### <a name="tooassign-storsimple-volumes-tooa-veeam-copy-job"></a>travail de copie tooassign StorSimple volumes tooa Veeam

1.  Dans hello Veeam sauvegarde et la console de réplication, sélectionnez **de sauvegarde et de réplication**. Cliquez avec le bouton droit sur **Backup (Sauvegarde)**, puis sélectionnez **VMware** ou **Hyper-V** en fonction de votre environnement.

    ![Console d’administration de Veeam, page de nouveau travail de copie de sauvegarde](./media/storsimple-configure-backup-target-using-veeam/veeamimage16.png)

2.  Bonjour **nouveau travail de copie de sauvegarde** boîte de dialogue, entrez un nom et une description pour le travail de hello.

    ![Console d’administration de Veeam, page de nouveau travail de copie de sauvegarde](./media/storsimple-configure-backup-target-using-veeam/veeamimage17.png)

3.  Sélectionnez hello machines virtuelles tooprocess. Sélectionnez à partir de sauvegardes, puis sauvegarde quotidienne hello que vous avez créé précédemment.

    ![Console d’administration de Veeam, page de nouveau travail de copie de sauvegarde](./media/storsimple-configure-backup-target-using-veeam/veeamimage18.png)

4.  Exclure des objets de travail de copie de sauvegarde hello, si nécessaire.

5.  Sélectionnez votre référentiel de sauvegarde et de définir une valeur pour **tookeep des points de restauration**. Être vraiment tooselect hello **suivant hello de conserver les points de restauration à des fins d’archivage** case à cocher. Définir la fréquence de sauvegarde hello et sélectionnez **avancé**.

    ![Console d’administration de Veeam, page de nouveau travail de copie de sauvegarde](./media/storsimple-configure-backup-target-using-veeam/veeamimage19.png)

6.  Spécifiez les paramètres avancés suivants de hello :

    * Sur hello **Maintenance** , onglet de désactiver la protection contre les dommages au niveau de stockage.

    ![Console d’administration de Veeam, page de paramètres avancés du nouveau travail de copie de sauvegarde](./media/storsimple-configure-backup-target-using-veeam/veeamimage20.png)

    * Sur hello **stockage** , veillez à ce que la déduplication et la compression sont désactivés.

    ![Console d’administration de Veeam, page de paramètres avancés du nouveau travail de copie de sauvegarde](./media/storsimple-configure-backup-target-using-veeam/veeamimage21.png)

7.  Spécifiez que le transfert de données hello est direct.

8.  Définir la planification de la fenêtre copie de sauvegarde hello selon les besoins de tooyour et puis terminez hello Assistant.

Pour plus d’informations, consultez l’article [Creating backup copy jobs (Création de travaux de copie de sauvegarde)](https://helpcenter.veeam.com/backup/hyperv/backup_copy_create.html).

## <a name="storsimple-cloud-snapshots"></a>Captures instantanées cloud StorSimple

Instantanés de cloud StorSimple protéger les données de hello qui réside dans votre appareil StorSimple. Création d’un instantané cloud est facilité de tooshipping équivalentes des bandes de sauvegarde local tooan hors site. Si vous utilisez un stockage géo-redondant Azure, la création d’un instantané cloud est sites de toomultiple tooshipping équivalent bandes de sauvegarde. Si vous devez toorestore un appareil après un sinistre, vous pouvez mettre un autre appareil StorSimple en ligne et effectuer un basculement. Après le basculement de hello, vous serez en mesure de tooaccess les données de hello (à des vitesses de cloud) à partir de l’instantané cloud le plus récent hello.

Hello suivant la section décrit comment toocreate un toostart script court et delete StorSimple instantanés cloud lors du post-traitement de la sauvegarde.

> [!NOTE]
> Instantanés créés manuellement ou par programmation ne suivent pas la stratégie d’expiration de hello StorSimple snapshot. Ces captures instantanées doivent être supprimées manuellement ou par programme.

### <a name="start-and-delete-cloud-snapshots-by-using-a-script"></a>Démarrer et supprimer des captures instantanées cloud avec un script

> [!NOTE]
> Évaluer avec soin la conformité de hello et des répercussions de rétention de données avant de supprimer un instantané StorSimple. Pour plus d’informations sur la façon toorun un script de postsauvegarde, consultez la documentation de Veeam de hello.


### <a name="backup-lifecycle"></a>Cycle de vie de sauvegarde

![Diagramme du cycle de vie de sauvegarde](./media/storsimple-configure-backup-target-using-veeam/backuplifecycle.png)

### <a name="requirements"></a>Configuration requise

-   serveur Hello qui exécute le script de hello doit avoir à accéder aux ressources de cloud tooAzure.
-   compte d’utilisateur Hello doit avoir les autorisations nécessaires hello.
-   Une stratégie de sauvegarde StorSimple avec hello associés StorSimple volumes doivent être configurés mais pas sous tension.
-   Vous devez hello StorSimple nom de la ressource, la clé d’enregistrement, nom de l’appareil et ID de stratégie de sauvegarde.

### <a name="toostart-or-delete-a-cloud-snapshot"></a>toostart ou supprimer un instantané cloud

1. [Installez Azure PowerShell](/powershell/azure/overview).
2. [Téléchargez et importez les paramètres de publication et les informations d’abonnement](https://msdn.microsoft.com/library/dn385850.aspx).
3. Dans l’hello portail Azure classic, obtenir le nom de la ressource hello et [clé d’inscription de votre service StorSimple Manager](storsimple-deployment-walkthrough-u2.md#step-2-get-the-service-registration-key).
4. Sur serveur hello qui exécute le script de hello, exécutez PowerShell en tant qu’administrateur. Tapez la commande suivante :

    `Get-AzureStorSimpleDeviceBackupPolicy –DeviceName <device name>`

    Code de note hello stratégie de sauvegarde.
5. Dans le bloc-notes, créez un script PowerShell à l’aide de hello suivant de code.

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
6. sauvegarde de tooyour tooadd hello script des tâches, modifiez votre travail Veeam options avancées.

    ![Paramètres avancés de sauvegarde Veeam, onglet Scripts](./media/storsimple-configure-backup-target-using-veeam/veeamimage22.png)

Nous vous conseillons d’exécuter votre stratégie de sauvegarde d’instantané cloud StorSimple en tant que script de post-traitement à fin hello de votre tâche de sauvegarde quotidienne. Pour plus d’informations sur comment tooback configuration et restauration votre toohelp d’environnement de l’application de sauvegarde vous remplissez votre RPO et RTO, veuillez consulter avec votre architecte de sauvegarde.

## <a name="storsimple-as-a-restore-source"></a>Utiliser StorSimple comme source de restauration

Les restaurations à partir d’un appareil StorSimple fonctionnent comme les restaurations effectuées à partir de n’importe quel dispositif de stockage de bloc. Restaurations de données à plusieurs niveaux toohello cloud se produit à des vitesses de cloud. Pour les données locales, les restaurations se produisent à la vitesse du disque local hello du périphérique de hello.

Avec Veeam, vous obtenez une restauration rapide, granulaire au niveau des fichiers via StorSimple via les affichages de l’Explorateur intégrés hello dans la console Veeam hello. Utilisez les explorateurs de Veeam toorecover des éléments individuels, tels que des messages électroniques, les objets Active Directory et les éléments SharePoint à partir de sauvegardes. récupération de Hello est possible sans interruption de service de machine virtuelle sur site. Vous pouvez également effectuer la récupération jusqu’à une date et heure spécifiques pour Azure SQL Database et les bases de données Oracle. Veeam et StorSimple faciliter les processus de hello de récupération au niveau élément à partir d’Azure rapidement et facilement. Pour plus d’informations sur la façon tooperform une restauration, consultez la documentation de Veeam de hello :

- Pour [Exchange Server](https://www.veeam.com/microsoft-exchange-recovery.html)
- Pour [Active Directory](https://www.veeam.com/microsoft-active-directory-explorer.html)
- Pour [SQL Server](https://www.veeam.com/microsoft-sql-server-explorer.html)
- Pour [SharePoint](https://www.veeam.com/microsoft-sharepoint-recovery-explorer.html)
- Pour [Oracle](https://www.veeam.com/oracle-backup-recovery-explorer.html)


## <a name="storsimple-failover-and-disaster-recovery"></a>Basculement et récupération d’urgence StorSimple

> [!NOTE]
> Pour les scénarios relatifs aux cibles de sauvegarde, l’appliance cloud StorSimple n’est pas prise en charge en tant que cible de restauration.

Un sinistre peut être dû à plusieurs facteurs. Hello tableau suivant répertorie les scénarios de récupération d’urgence courants.

| Scénario | Impact | Comment toorecover | Remarques |
|---|---|---|---|
| Défaillance d’appareil StorSimple | Les opérations de sauvegarde et de restauration sont interrompues. | Remplacer le périphérique avec échec hello et exécuter [StorSimple basculement et récupération d’urgence](storsimple-device-failover-disaster-recovery.md). | Si vous devez tooperform une restauration après la récupération de l’appareil, les jeux de travail complète des données sont extraites hello cloud toohello nouvel appareil. Toutes les opérations sont exécutées à la vitesse du cloud. index de Hello et le catalogue une nouvelle analyse de processus risque de tous les jeux de sauvegarde toobe, analysés et extraite hello cloud couche toohello appareil local niveau, qui peut prendre du temps. |
| Défaillance du serveur Veeam | Les opérations de sauvegarde et de restauration sont interrompues. | Reconstruire le serveur de sauvegarde hello et effectuer la restauration de la base de données comme détaillé dans [Veeam centre d’aide (Documentation technique)](https://www.veeam.com/documentation-guides-datasheets.html).  | Vous devez reconstruire ou restaurer serveur Veeam de hello sur site de récupération d’urgence hello. Hello de base de données toohello plus récent point de restauration. Si hello Veeam base de données restaurée n’est pas synchronisée avec vos travaux de sauvegarde plus récente, l’indexation et de catalogage sont requis. Cet index et le catalogue une nouvelle analyse de processus risque de tous les jeux de sauvegarde toobe, analysées et extraites de la couche de hello cloud couche toohello périphérique local. Ce processus peut donc prendre un certain temps. |
| Défaillance du site qui entraîne la perte de hello du serveur de sauvegarde hello et StorSimple | Les opérations de sauvegarde et de restauration sont interrompues. | Commencez par restaurer StorSimple, puis restaurez Veeam. | Commencez par restaurer StorSimple, puis restaurez Veeam. Si vous devez tooperform une restauration après la récupération de l’appareil, jeux de travail hello complète des données est extraites hello cloud toohello nouvel appareil. Toutes les opérations sont exécutées à la vitesse du cloud. |


## <a name="references"></a>Références

Hello suivant les documents ont été référencé pour cet article :

- [StorSimple multipath I/O setup (Configuration de StorSimple MPIO)](storsimple-configure-mpio-windows-server.md)
- [Storage scenarios: Thin provisioning (Scénarios de stockage : allocation dynamique)](http://msdn.microsoft.com/library/windows/hardware/dn265487.aspx)
- [Using GPT drives (Utilisation de disques de table de partition GUID)](http://msdn.microsoft.com/windows/hardware/gg463524.aspx#EHD)
- [Set up shadow copies for shared folders (Configurer des clichés instantanés de dossiers partagés)](http://technet.microsoft.com/library/cc771893.aspx)

## <a name="next-steps"></a>Étapes suivantes

- En savoir plus sur la façon trop[restauration à partir d’un jeu de sauvegarde](storsimple-restore-from-backup-set-u2.md).
- En savoir plus sur la façon tooperform [appareil basculement et récupération d’urgence](storsimple-device-failover-disaster-recovery.md).
