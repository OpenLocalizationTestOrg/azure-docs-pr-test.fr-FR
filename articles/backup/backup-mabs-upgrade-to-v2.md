---
title: "aaaInstall v2 d’Azure Backup Server | Documents Microsoft"
description: "Le serveur de sauvegarde Azure v2 offre des capacités de sauvegarde améliorées pour protéger les machines virtuelles, les fichiers et dossiers, les charges de travail, et plus encore. Découvrez comment tooinstall ou mise à niveau tooAzure v2 de sauvegarde du serveur."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: 5b1699dadd3a173f1c0ef91a1a600bc5e12f20ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-azure-backup-server-v2"></a>Installer le serveur de sauvegarde Azure v2

Le serveur de sauvegarde Azure contribue à protéger vos machines virtuelles, vos charges de travail, vos fichiers et dossiers, et plus encore. Reposant sur le serveur de sauvegarde v1, le serveur de sauvegarde Azure v2 offre des fonctionnalités qui ne sont pas disponibles dans la première version. Pour connaître les différences entre les versions v1 et v2, consultez [Matrice de protection du serveur de sauvegarde Azure](backup-mabs-protection-matrix.md). 

fonctionnalités supplémentaires de Hello dans v2 de sauvegarde du serveur sont une mise à niveau à partir de la sauvegarde du serveur v1. Cependant, le serveur de sauvegarde v1 n’est pas requis pour installer le serveur de sauvegarde v2. Si vous souhaitez tooupgrade à partir de la sauvegarde du serveur v1 tooBackup v2 de serveur, installez v2 de sauvegarde du serveur sur le serveur de protection du serveur de sauvegarde hello. Vos paramètres de serveur de sauvegarde existants seront conservés.

Vous pouvez installer le serveur de sauvegarde v2 sur Windows Server 2012 R2 ou Windows Server 2016. tootake les parti des nouvelles fonctionnalités telles que le stockage de sauvegarde moderne données Protection Manager System Center 2016, vous devez installer le serveur de sauvegarde v2 sur Windows Server 2016. Mettre à niveau l’installation tooor v2 de sauvegarde du serveur, en savoir plus sur hello [conditions préalables d’installation](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).

> [!NOTE]
> Sauvegarde du serveur Azure a hello même code de base en tant que System Center Data Protection Manager. Sauvegarde serveur v1 est équivalent tooData Protection Manager 2012 R2 et v2 de sauvegarde du serveur est équivalent tooData Protection Manager 2016. Cet article fait parfois référence à la documentation de Data Protection Manager hello.
>
>

## <a name="upgrade-backup-server-toov2"></a>Mise à niveau du serveur de sauvegarde toov2
tooupgrade à partir de la sauvegarde du serveur v1 tooBackup v2 de serveur, assurez-vous que votre installation comprend des mises à jour hello requis :

- [Mettre à jour les agents de protection hello](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) sur hello des serveurs protégés.
- Mise à niveau de Windows Server 2012 R2 tooWindows Server 2016.
- Mettez à niveau l’outil d’administration à distance du serveur de sauvegarde Azure sur tous les serveurs de production.
- Assurez-vous que les sauvegardes sont définies toocontinue sans avoir à redémarrer votre serveur de production.


### <a name="upgrade-steps-for-backup-server-v2"></a>Procédure de mise à niveau vers le serveur de sauvegarde v2

1. Dans le centre de téléchargement de hello [télécharger le programme d’installation de la mise à niveau hello](https://go.microsoft.com/fwlink/?LinkId=626082).

2. Après avoir extrait Assistant hello, assurez-vous que **exécuter setup.exe** est sélectionné, puis sélectionnez **Terminer**.

  ![Programme d’installation - Exécuter l’installation](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. Dans l’Assistant de Microsoft Azure Backup Server hello, sous **installer**, sélectionnez **Microsoft Azure Backup Server**.

  ![Programme d’installation - Sélectionner l’installation](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. Sur hello **Bienvenue** , examinez les avertissements hello, puis sélectionnez **suivant**.

  ![Programme d’installation - Page Bienvenue](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. Assistant Installation de Hello effectue toomake vérifications des conditions préalables que votre environnement peut mettre à niveau. Sur hello **Prerequisite Checks** page, sélectionnez **vérifier**.

  ![Programme d’installation - Page Vérifications des conditions requises](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. Votre environnement doit passer les vérifications hello. Si votre environnement ne remplit pas les vérifications de hello, notez les problèmes de hello et de les corriger. Ensuite, sélectionnez **Revérifier**. Une fois que vous passez des vérifications des conditions préalables hello, sélectionnez **suivant**.

  ![Programme d’installation - Bouton Revérifier](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. Sur hello **paramètres SQL** page, l’option hello pertinentes pour votre installation de SQL, puis sélectionnez **vérifier et installer**.

  ![Programme d’installation - Page Paramètres SQL](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  vérifications de Hello peuvent prendre quelques minutes. Lorsque les vérifications de hello sont terminé, sélectionnez **suivant**.

  ![Programme d’installation - Bouton Vérifier et installer de la page Paramètres SQL](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. Sur hello **les paramètres d’Installation** page, de modifier n’importe quel emplacement de toohello modifications où la sauvegarde du serveur est installé, ou toohello emplacement de travail. Sélectionnez **Suivant**.

  ![Programme d’installation - Page Paramètres d’installation](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. toofinish hello Assistant installation, sélectionnez **Terminer**.

  ![Programme d’installation - Terminer](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a>Ajouter un stockage pour Modern Backup Storage

l’efficacité du stockage de sauvegarde tooimprove, v2 de sauvegarde du serveur ajoute la prise en charge des volumes. Comme le serveur de sauvegarde v1, le serveur de sauvegarde v2 prend en charge les disques.

### <a name="add-volumes-and-disks"></a>Ajouter des volumes et des disques
Si vous exécutez le serveur de sauvegarde v2 sur Windows Server 2016, vous pouvez utiliser les données de sauvegarde de volumes toostore. Les volumes assurent des économies en stockage et des sauvegardes plus rapides. Étant donné que les volumes sont tooBackup nouveau serveur, vous devez les ajouter. 

Lorsque vous ajoutez un serveur de tooBackup volume, vous pouvez donner un nom convivial volume de hello. Cliquez sur hello **nom convivial** colonne du volume de hello souhaité tooname. Vous pouvez modifier le nom de hello plus tard, si nécessaire. Vous pouvez également utiliser PowerShell tooadd ou modifier les noms conviviaux pour les volumes.

tooadd un volume Bonjour la Console Administrateur :

1. Dans la Console Administrateur de serveur de sauvegarde Azure de hello, sélectionnez **gestion** > **le stockage sur disque** > **ajouter**.

    ![Assistant Ajouter un stockage sur disque de hello ouvert](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    Assistant Ajouter un stockage sur disque de hello s’ouvre.

2. Sur hello **ajouter un stockage sur disque** page hello **volumes disponibles** zone, sélectionnez un volume, puis **ajouter**.
3. Bonjour **des volumes sélectionnés** zone, entrez un nom convivial pour le volume de hello, puis sélectionnez **OK**.

      ![Assistant Ajouter un stockage sur disque - Ajouter un volume](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  Si vous souhaitez tooadd une disquette, disque de hello doit appartenir à groupe de protection tooa ayant un stockage hérité. Ces disques peuvent uniquement être utilisés pour ces groupes de protection. Si le serveur de sauvegarde n’a pas sources dont la protection héritée, disque de hello n’est pas répertorié.

  Pour plus d’informations sur l’ajout de disques, consultez [Ajout des disques de stockage hérité tooincrease](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage). Vous ne pouvez pas donner de nom convivial à un disque.


### <a name="assign-workloads-toovolumes"></a>Affecter des charges de travail toovolumes

Dans la sauvegarde du serveur, vous spécifiez des charges de travail assignés toowhich volumes. Par exemple, vous pouvez définir des volumes coûteuses qui prennent en charge un grand nombre d’opérations d’entrée/sortie par seconde (IOPS) toostore uniquement les charges de travail qui nécessitent des sauvegardes fréquentes et élevées. Un exemple est SQL Server avec les journaux des transactions.

#### <a name="update-dpmdiskstorage"></a>Update-DPMDiskStorage

les propriétés de hello de tooupdate d’un volume dans le pool de stockage de hello au serveur de sauvegarde, utiliser l’applet de commande PowerShell hello DPMDiskStorage de mise à jour.

Syntaxe :

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

Toutes les modifications que vous apportez à l’aide de PowerShell sont répercutées dans l’interface utilisateur de hello.


## <a name="protect-data-sources"></a>Protéger les sources de données
toobegin protégeant les sources de données, créez un groupe de protection. Hello suivant Assistant par mise en surbrillance étapes changements ou ajouts nouveau groupe de Protection de toohello.

toocreate un groupe de protection :

1. Dans la Console Administrateur de serveur de sauvegarde de hello, sélectionnez **Protection**.

2. Dans la barre d’outils hello, sélectionnez **nouveau**.

    Assistant créer un nouveau groupe de Protection de hello s’ouvre.

  ![Assistant Création d’un nouveau groupe de protection](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. Sur hello **Bienvenue** page, sélectionnez **suivant**.
4. Sur hello **sélectionner le Type de groupe de Protection** , sélectionnez le type de hello du groupe de protection, vous souhaitez toocreate, puis sélectionnez **suivant**.

  ![Page Sélectionner le type de groupe de protection](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. Sur hello **sélectionner les membres du groupe** page hello **membres disponibles** volet, les membres de hello avec protection agents sont répertoriés. Dans cet exemple, sélectionnez le volume D:\ et E:\ et ajoutez-les toohello **membres sélectionnés** volet. Sélectionnez **Suivant**.

  ![Page Sélectionner les membres du groupe](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. Sur hello **sélectionner la méthode de Protection des données** , entrez un **nom de groupe de Protection**, sélectionnez la méthode de protection hello, puis **suivant**. Si vous souhaitez une protection à court terme, vous devez sélectionner hello **disque** méthode de sauvegarde.

  ![Page Sélectionner la méthode de protection des données](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. Sur hello **spécifier les objectifs à court terme** mise en page, sélectionnez hello pour **de rétention** et **la fréquence de synchronisation**. Ensuite, sélectionnez **Suivant**. Si vous le souhaitez, toochange planification de hello pour lorsque les points de récupération sont prises, sélectionnez **modifier**.

  ![Page Spécifier les objectifs à court terme](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. Sur hello **vérifier l’Allocation de stockage disque** , examinez les détails sur les sources de données hello choisie, leur taille et valeurs hello espace toobe est configuré, hello du volume de stockage cible.

  ![Page Vérifier l’allocation de stockage sur disque](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  Volumes de stockage sont basés sur l’allocation de volume de charge de travail hello (définie à l’aide de PowerShell) et hello du stockage disponible. Vous pouvez modifier les volumes de stockage hello en sélectionnant les autres volumes dans le menu déroulant de hello. Si vous modifiez la valeur hello pour **stockage cible**, hello valeur pour **stockage de disque disponible** modifie de façon dynamique les valeurs tooreflect sous **espace** et **Underprovisioned espace**.

  Si la croissance des sources de données hello comme prévu, hello valeur hello **Underprovisioned l’espace** colonne **stockage de disque disponible** reflète la quantité de hello de stockage supplémentaire que nécessaire. Utiliser ce plan de toohelp valeur vos besoins de stockage pour les sauvegardes lisses. Si la valeur de hello est égal à zéro, il n’existe aucun problème potentiel avec le stockage dans un futur prévisible hello. Si la valeur de hello est un nombre différent de zéro, vous n’avez pas de suffisamment de stockage alloué (basé sur la protection de stratégie et hello taille de vos données de vos membres protégés).

  ![Stockage sur disque sous-alloué](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   toofinish création de l’Assistant hello groupe, complète de votre protection.

## <a name="migrate-legacy-storage-toomodern-backup-storage"></a>Migrer le stockage existant tooModern le stockage de sauvegarde
Une fois que vous mettez à niveau tooor installation v2 de sauvegarde du serveur et mise à niveau hello tooWindows de système d’exploitation Server 2016, mettre à jour votre toouse de groupes de protection moderne le stockage de sauvegarde. Par défaut, les groupes de protection ne sont pas modifiés. Ils continuent toofunction comme elles ont été initialement définis. 

Mise à jour de groupes de protection toouse moderne le stockage de sauvegarde est facultative. groupe de protection tooupdate hello, arrêtez la protection de toutes les sources de données à l’aide de hello conserver option de données. Ajoutez ensuite hello données sources tooa nouveau groupe de protection.

1. Dans la Console Administrateur de hello, sélectionnez hello **Protection** fonctionnalité. Bonjour **membre du groupe de Protection** liste, cliquez sur le membre de hello et sélectionnez **arrêter la protection du membre**.

  ![Arrêter la protection du membre](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. Bonjour **supprimer du groupe** boîte de dialogue, l’espace de disque hello utilisée revue et hello d’espace libre pour le pool de stockage hello. valeur par défaut Hello est de points de récupération hello tooleave sur le disque de hello et leur tooexpire par leur stratégie de rétention. Cliquez sur **OK**.

  Si vous souhaitez que le pool de stockage libre du disque espace toohello tooimmediately hello retour utilisé, sélectionnez hello **supprimer le réplica sur disque** case toodelete les données de sauvegarde hello (et les points de récupération) associé à ce membre.

  ![Boîte de dialogue Supprimer du groupe](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. Créez un groupe de protection qui utilise Modern Backup Storage. Inclure des sources de données hello non protégé.


## <a name="add-disks-tooincrease-legacy-storage"></a>Ajouter des disques du stockage hérité tooincrease

Si vous souhaitez toouse de stockage existant avec le serveur de sauvegarde, vous devrez peut-être stockage hérité de tooadd disques tooincrease. 

stockage sur disque tooadd :

1. Dans la Console Administrateur de hello, sélectionnez **gestion** > **le stockage sur disque** > **ajouter**.

    ![Boîte de dialogue Ajouter un stockage sur disque](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. Bonjour **ajouter un stockage sur disque** boîte de dialogue, sélectionnez **ajouter des disques**.

5. Dans la liste hello de disques disponibles, sélectionnez les disques hello tooadd, sélectionnez **ajouter**, puis sélectionnez **OK**.

## <a name="update-hello-data-protection-manager-protection-agent"></a>Mettre à jour l’agent de protection hello Data Protection Manager

Sauvegarde du serveur utilise un agent de protection de System Center Data Protection Manager hello des mises à jour. Si vous mettez à niveau un agent de protection n’est pas connecté toohello réseau, vous ne pouvez pas utiliser hello Console d’administration DPM toocomplete une mise à niveau de l’agent. Vous devez mettre à niveau l’agent de protection hello dans un environnement de domaine non actif. Jusqu'à ce que l’ordinateur client de hello est connecté toohello réseau, hello que console d’administration DPM affiche cette mise à jour de l’agent de protection hello est en attente.

Hello sections suivantes décrivent comment tooupdate les agents de protection pour les ordinateurs clients qui sont connectés et les ordinateurs clients qui ne sont pas connectés.

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a>Mettre à jour un agent de protection pour un ordinateur client connecté

1. Dans la Console Administrateur de serveur de sauvegarde de hello, sélectionnez **gestion** > **Agents**.

2. Dans le volet d’informations hello, sélectionnez les ordinateurs clients hello pour lequel vous souhaitez l’agent de protection tooupdate hello.

  > [!NOTE]
  > Hello **mises à jour de l’Agent** colonne indique lorsqu’une mise à jour de l’agent de protection est disponible pour chaque ordinateur protégé. Bonjour **Actions** volet, hello **mise à jour** action est disponible uniquement lorsqu’un ordinateur protégé est sélectionné et les mises à jour sont disponibles.
  >
  >

3. tooinstall mis à jour les agents de protection sur les ordinateurs de hello sélectionné, Bonjour **Actions** volet, sélectionnez **mise à jour**.

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a>Mettre à jour un agent de protection pour un ordinateur client qui n’est pas connecté

1. Dans la Console Administrateur de serveur de sauvegarde de hello, sélectionnez **gestion** > **Agents**.

2. Dans le volet d’informations hello, sélectionnez les ordinateurs clients hello pour lequel vous souhaitez l’agent de protection tooupdate hello.

  > [!NOTE]
   > Hello **mises à jour de l’Agent** colonne indique lorsqu’une mise à jour de l’agent de protection est disponible pour chaque ordinateur protégé. Bonjour **Actions** volet, hello **mise à jour** action n’est pas disponible lorsqu’un ordinateur protégé est sélectionné sauf si les mises à jour sont disponibles.
  >
  >

3. tooinstall mis à jour les agents de protection sur les ordinateurs hello sélectionné, sélectionnez **mise à jour**.

4. Pour un ordinateur client qui n’est pas connecté toohello réseau, jusqu'à ce que l’ordinateur de hello est connecté toohello réseau, hello **état de l’Agent** colonne présente l’état de **mise à jour en attente**.

  Une fois un ordinateur client connecté toohello réseau, hello **mises à jour de l’Agent** présente l’état de colonne pour l’ordinateur client de hello **mise à jour**.
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-hello-new-version-with-azure"></a>Déplacer des groupes de Protection hérités à partir de l’ancienne et la synchronisation hello nouvelle version avec Azure

Une fois que le serveur de sauvegarde Azure et hello du système d’exploitation sont à jour, vous êtes prêt tooprotect nouvelles sources de données à l’aide du stockage de sauvegarde moderne. Toutefois déjà protégé des sources de données continue toobe protégé dans hello hérité de façon qu’ils étaient dans Azure Backup Server mais toute nouvelle protection utilise le stockage de sauvegarde modernes.

Étapes ci-dessous sont des sources de données toomigrate du mode hérité protection tooModern de stockage de sauvegarde.

• Ajoutez hello nouveau ou les volumes toohello DPM pool de stockage et affecter des balises de source de données et les noms conviviales si vous le souhaitez.
• Pour chaque source de données est en mode CAS hérité, arrêtez la protection des sources de données hello et « Conserver les données protégées ».  Ainsi, les anciens points de récupération peuvent être récupérés après la migration.

• Créer un nouveau groupe de protection et sélectionnez les sources de données hello qui sont stocké à l’aide du nouveau format de toobe.
• DPM effectuera une copie du réplica de stockage de sauvegarde hérité hello en hello volume de stockage de sauvegarde moderne localement.
Remarque : Cela est considéré comme un travail d’opération de postrécupération • Tous les nouveaux points de synchronisation et de récupération sont ensuite stockés dans Modern Backup Storage.
• Anciens points de récupération seront nettoyés qu’ils expirent et finalement libérer de l’espace disque hello.
• Une fois que tous les volumes hérités hello sont supprimées du stockage ancien hello, disque de hello peut être supprimée à partir du système de sauvegarde et de hello Azure.
• Créer une sauvegarde de hello Azure DPMDB.

Partie 2 :-des éléments importants > nouveau serveur de hello devez toobe même nommé en tant que serveur de sauvegarde Azure hello d’origine. Vous ne pouvez pas modifier le nom hello du serveur de sauvegarde Azure nouveau hello si vous voulez toouse ancien pool de stockage des points de récupération de tooretain DPMDB - devez avoir la sauvegarde de base de données DPM que vous devez toobe restauré

1) Arrêt hello du serveur de sauvegarde Azure d’origine ou mettez-la câble hello.
2) Réinitialiser le compte d’ordinateur hello dans active directory.
3) Installer Server 2016 sur le nouvel ordinateur, nom il hello le même nom de l’ordinateur en tant que serveur de sauvegarde Azure hello d’origine.
4) Joindre le domaine de hello
5) Installez le serveur de sauvegarde Azure, version 2 (déplacez les disques du pool de stockage de DPM depuis l’ancien serveur et effectuez l’importation).
6) Restaurer hello DPMDB obtenue à partir de la fin de la partie 2
7) Connectez le périphérique de stockage de hello hello d’origine sauvegarde toohello nouveau serveur.
8) À partir de la restauration SQL hello DPMDB
9) À partir de la ligne de commande d’administration sur le nouveau serveur de cd tooMicrosoft Azure Backup installer emplacement et le dossier bin

Exemple de chemin : C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\
tooAzure sauvegarde exécutez DPMSYNC-SYNC

10) Exécutez DPMSYNC-SYNC Remarque Si vous avez ajouté le nouveau pool de stockage DPM disques toohello au lieu de déplacer hello anciens, puis exécutez DPMSYNC - Reallocatereplica

## <a name="new-powershell-cmdlets-in-v2"></a>Nouveaux cmdlets PowerShell dans la version 2

Lorsque vous installez le serveur de sauvegarde Azure v2, deux nouveaux cmdlets sont disponibles : 
* [Mount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787159.aspx)
* [Dismount-DPMRecoveryPoint](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment tooprepare votre serveur ou pour commencer à protéger une charge de travail :
- [Préparer les charges de travail du serveur de sauvegarde](backup-azure-microsoft-azure-backup.md)
- [Utilisez tooback du serveur de sauvegarde d’un serveur VMware](backup-azure-backup-server-vmware.md)
- [Utilisez tooback de sauvegarde du serveur SQL Server](backup-azure-sql-mabs.md)
- [Utiliser Modern Backup Storage avec le serveur de sauvegarde](backup-mabs-add-storage.md)

