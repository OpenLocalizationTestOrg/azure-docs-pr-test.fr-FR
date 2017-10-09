---
title: "aaaAzure sauvegarde Server protège l’état du système et restaure toobare complète | Documents Microsoft"
description: "Utiliser Azure Backup Server tooback votre état du système et fournir la protection de récupération complète (BMR)."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
keywords: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.targetplatform: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: markgal,masaran
ms.openlocfilehash: d34c8bbdc7cc24c905f81ceaf199698c1ee923db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-system-state-and-restore-toobare-metal-with-azure-backup-server"></a>Sauvegarder l’état du système et de restauration complète toobare avec Azure Backup Server

Le Serveur de sauvegarde Azure sauvegarde l’état de votre système et effectue une récupération complète de celui-ci.

*   **Sauvegarde de l’état système**: sauvegarde les fichiers de système d’exploitation, afin que vous pouvez récupérer lorsqu’un ordinateur démarre, mais les fichiers système et du Registre de hello sont perdues. Une sauvegarde de l’état du système inclut ces élément suivants :
    * Membre de domaine : fichiers de démarrage, base de données d’inscription de classe COM+, Registre
    * Contrôleur de domaine : Windows Server Active Directory (NTDS), fichiers de démarrage, base de données d’inscription de classe COM+, Registre, volume système (SYSVOL)
    * Ordinateur exécutant les services de cluster : métadonnées du serveur de cluster
    * Ordinateur exécutant les services de certificats : données du certificat
* **Sauvegarde de complète** : sauvegarde les fichiers du système d’exploitation et toutes les données sur les volumes critiques (sauf les données utilisateur). Par définition, une sauvegarde complète inclut une sauvegarde de l’état du système. Il offre une protection lorsqu’un ordinateur ne démarre pas et vous avez toorecover tous les éléments.

Hello tableau suivant résume ce que vous pouvez sauvegarder et restaurer. Pour plus d’informations sur les versions d’application qui peuvent être protégées avec l’état du système et une récupération complète, voir [Qu’est-ce que le Serveur de sauvegarde Azure ?](backup-mabs-protection-matrix.md).

|Sauvegarde|Problème|Récupère à partir de la sauvegarde effectuée par le Serveur de sauvegarde Azure|Récupère à partir de la sauvegarde de l’état du système|Récupération complète|
|----------|---------|---------------------------|------------------------------------|-------|
|**Données de fichier**<br /><br />Sauvegarde des données régulières<br /><br />Récupération complète/sauvegarde de l’état du système|Données de fichiers perdues|O|N|N|
|**Données de fichier**<br /><br />Sauvegarde effectuée par le Serveur de sauvegarde Azure des données de fichier<br /><br />Récupération complète/sauvegarde de l’état du système|Système d’exploitation perdu ou endommagé|N|O|O|
|**Données de fichier**<br /><br />Sauvegarde effectuée par le Serveur de sauvegarde Azure des données de fichier<br /><br />Récupération complète/sauvegarde de l’état du système|Serveur perdu (volumes de données intacts)|N|N|O|
|**Données de fichier**<br /><br />Sauvegarde effectuée par le Serveur de sauvegarde Azure des données de fichier<br /><br />Récupération complète/sauvegarde de l’état du système|Serveur perdu (volumes de données perdus)|O|Non|Oui (récupération complète, suivie d’une récupération régulière des données de fichiers sauvegardées)|
|**Données SharePoint** :<br /><br />Sauvegarde effectuée par le Serveur de sauvegarde Azure des données de batterie de serveurs<br /><br />Récupération complète/sauvegarde de l’état du système|Site perdu, listes, éléments de liste, documents|O|N|N|
|**Données SharePoint** :<br /><br />Sauvegarde effectuée par le Serveur de sauvegarde Azure des données de batterie de serveurs<br /><br />Récupération complète/sauvegarde de l’état du système|Système d’exploitation perdu ou endommagé|N|O|O|
|**Données SharePoint** :<br /><br />Sauvegarde effectuée par le Serveur de sauvegarde Azure des données de batterie de serveurs<br /><br />Récupération complète/sauvegarde de l’état du système|Récupération d'urgence|N|N|N|
|Windows Server 2012 R2 Hyper-V<br /><br />Sauvegarde effectuée par le Serveur de sauvegarde Azure de l’hôte ou de l’invité Hyper-V<br /><br />Récupération complète/Sauvegarde de l’état du système|Machine virtuelle perdue|O|N|N|
|Hyper-V<br /><br />Sauvegarde effectuée par le Serveur de sauvegarde Azure de l’hôte ou de l’invité Hyper-V<br /><br />Récupération complète/Sauvegarde de l’état du système|Système d’exploitation perdu ou endommagé|N|O|O|
|Hyper-V<br /><br />Sauvegarde effectuée par le Serveur de sauvegarde Azure de l’hôte ou de l’invité Hyper-V<br /><br />Récupération complète/Sauvegarde de l’état du système|Hôte Hyper-V perdu (machines virtuelles intactes)|N|N|O|
|Hyper-V<br /><br />Sauvegarde effectuée par le Serveur de sauvegarde Azure de l’hôte ou de l’invité Hyper-V<br /><br />Récupération complète/Sauvegarde de l’état du système|Hôte Hyper-V perdu (machines virtuelles perdues)|N|N|O<br /><br />Récupération complète, suivie d’une récupération régulière du Serveur de sauvegarde Azure|
|SQL Server/Exchange<br /><br />Sauvegarde d’application effectuée par le Serveur de sauvegarde Azure<br /><br />Récupération complète/sauvegarde de l’état du système|Données d’application perdues|O|N|N|
|SQL Server/Exchange<br /><br />Sauvegarde d’application effectuée par le Serveur de sauvegarde Azure<br /><br />Récupération complète/sauvegarde de l’état du système|Système d’exploitation perdu ou endommagé|N|y|O|
|SQL Server/Exchange<br /><br />Sauvegarde d’application effectuée par le Serveur de sauvegarde Azure<br /><br />Récupération complète/sauvegarde de l’état du système|Serveur perdu (base de données/journaux des transactions intacts)|N|N|O|
|SQL Server/Exchange<br /><br />Sauvegarde d’application effectuée par le Serveur de sauvegarde Azure<br /><br />Récupération complète/sauvegarde de l’état du système|Serveur perdu (base de données/journaux des transactions perdus)|N|N|O<br /><br />Récupération complète, suivie d’une récupération régulière du Serveur de sauvegarde Azure|

## <a name="how-system-state-backup-works"></a>Fonctionnement de la sauvegarde de l’état du système

Lorsqu’une sauvegarde de l’état système s’exécute, serveur de sauvegarde communique avec sauvegarde Windows Server toorequest une sauvegarde de l’état du système du serveur hello. Par défaut, le serveur de sauvegarde et de la sauvegarde de Windows Server utilisent lecteur hello ayant hello plus d’espace libre. Plus d’informations sur ce lecteur sont enregistrés dans le fichier PSDataSourceConfig.xml de hello. Il s’agit de hello lecteur avec sauvegarde Windows Server pour les sauvegardes.

Vous pouvez personnaliser le lecteur hello par serveur de sauvegarde pour la sauvegarde de l’état système hello. Sur le serveur de hello protégé, accédez à tooC:\Program Files\Microsoft Manager\MABS\Datasources de Protection de données. Ouvrez le fichier de PSDataSourceConfig.xml de hello pour modification. Hello de modification \<FilesToProtect\> valeur pour la lettre de lecteur hello. Enregistrez et fermez le fichier de hello. S’il existe qu'un groupe de protection définie l’état du système hello tooprotect de l’ordinateur de hello, exécutez une vérification de cohérence. Si une alerte est générée, sélectionnez **modifier le groupe de protection** dans hello alert et Assistant de hello puis terminée. Ensuite, exécutez une autre vérification de cohérence.

Notez que si le serveur de protection hello est dans un cluster, il est possible qu’un lecteur de cluster soit sélectionné en tant que lecteur hello avec hello plus d’espace libre. Si cette propriété du lecteur a été tooanother commuté nœud et une sauvegarde de l’état système s’exécute, lecteur de hello n’est pas disponible et hello sauvegarde échoue. Dans ce scénario, modifiez PSDataSourceConfig.xml toopoint tooa le disque local.

Ensuite, la sauvegarde de Windows Server crée un dossier appelé WindowsImageBackup dans racine hello du dossier de restauration hello. Lors de la sauvegarde de Windows Server crée la sauvegarde de hello, toutes les données de hello sont placées dans ce dossier. Après la sauvegarde de hello, fichier de hello est ordinateur du serveur de sauvegarde toohello transférés. Notez hello informations suivantes :

* Ce dossier et son contenu n'est pas nettoyés lors de la sauvegarde de hello ou le transfert est terminé. Hello meilleure manière toothink de ce est que hello espace est réservé pour hello prochaine qu'une sauvegarde est terminée.
* dossier de Hello est créé chaque fois qu’une sauvegarde est effectuée. cachet de date et heure Hello reflètent les temps de hello de votre dernière sauvegarde de l’état système.

## <a name="bmr-backup"></a>Sauvegarde complète

Pour la récupération complète (y compris une sauvegarde de l’état système), du travail de sauvegarde hello est enregistré directement tooa partage sur l’ordinateur du serveur de sauvegarde hello. Il n’est pas enregistré tooa dossier sur le serveur de hello protégé.

Sauvegarde du serveur appelle la sauvegarde Windows Server et partages de volume du réplica hello pour que la sauvegarde complète. Dans ce cas, il ne faire lecteur de hello toouse de sauvegarde de Windows Server avec hello plus d’espace libre. Au lieu de cela, il utilise le partage hello qui a été créé pour le travail de hello.

Après la sauvegarde de hello, fichier de hello est ordinateur du serveur de sauvegarde toohello transférés. Les journaux sont stockés dans C:\Windows\Logs\WindowsServerBackup.

## <a name="prerequisites-and-limitations"></a>Conditions préalables et limitations

-   La récupération complète n’est pas prise en charge pour les ordinateurs exécutant Windows Server 2003 ou un système d’exploitation de client.

-   Vous ne pouvez pas protéger une récupération complète et le système d’état pour hello même ordinateur dans différents groupes de protection.

-   Un ordinateur Serveur de sauvegarde ne peut pas se protéger lui-même pour une récupération complète.

-   Tootape de protection à court terme (disque à bande ou D2T) n’est pas pris en charge pour la récupération complète. Tootape de stockage à long terme (disque à disque à bande ou D2D2T) est pris en charge.

-   Pour la protection de la récupération complète, la sauvegarde de Windows Server doit être installé sur l’ordinateur de hello protégé.

-   Pour la protection complète, contrairement à pour la protection de l’état système, sauvegarde de serveur n’a d’espace disque requis sur l’ordinateur de hello protégé. Sauvegarde Windows Server transfère directement l’ordinateur de serveur de sauvegarde toohello de sauvegardes. tâche de transfert de sauvegarde de Hello n’apparaît pas dans hello sauvegarde du serveur **travaux** vue.

-   Sauvegarde du serveur de réserve 30 Go d’espace sur le volume du réplica hello pour la récupération complète. Vous pouvez modifier ce paramètre sur hello **l’Allocation de disque** page dans l’Assistant Modifier un groupe de Protection de hello ou à l’aide des applets de commande Get-DatasourceDiskAllocation et Set-DatasourceDiskAllocation PowerShell hello. Sur le volume des points de récupération hello, la protection récupération complète nécessite environ 6 Go pour une durée de rétention de cinq jours.
    * Notez que vous ne pouvez pas réduire accessible sans hello réplica volume taille à 15 Go.
    * Serveur de sauvegarde ne calcule pas taille hello hello complète de source de données. Il suppose qu’elle est de 30 Go pour tous les serveurs. Modifier la valeur hello en fonction de taille hello des sauvegardes de la récupération complète attendues dans votre environnement. taille de Hello d’une sauvegarde de la récupération complète peut être calculée à peu près comme somme hello d’espace utilisé sur tous les volumes critiques. Volumes critiques = volume de démarrage + volume système + volume hébergeant les données d’état du système, tel qu’Active Directory.

-   Si vous modifiez à partir de la protection de tooBMR protection l’état système, la protection récupération complète nécessite moins d’espace sur hello *volume des points de récupération*. Toutefois, hello espace restant sur le volume de hello n'est pas récupéré. Vous pouvez réduire manuellement la taille du volume hello sur hello **modifier l’Allocation de disque** page de l’Assistant Modifier un groupe de Protection de hello ou à l’aide des applets de commande Get-DatasourceDiskAllocation et Set-DatasourceDiskAllocation PowerShell hello.

    Si vous modifiez à partir de la protection de tooBMR protection l’état système, la protection récupération complète nécessite davantage d’espace sur hello *volume du réplica*. Hello volume est automatiquement étendu. Si vous souhaitez que les allocations d’espace par défaut toochange hello, utilisez l’applet de commande PowerShell de Modify-DiskAllocation hello.

-   Si vous modifiez à partir de la protection de l’état toosystem protection récupération complète, vous avez besoin de davantage d’espace sur le volume des points de récupération hello. Sauvegarde du serveur peut tenter tooautomatically augmenter le volume hello. Si l’espace est insuffisant dans le pool de stockage hello, une erreur se produit.

    Si vous modifiez à partir de la protection de l’état toosystem protection récupération complète, vous avez besoin d’espace sur l’ordinateur de hello protégé. Il s’agit, car la protection de l’état système écrit d’abord ordinateur local de hello réplica toohello, puis il transfère l’ordinateur du serveur de sauvegarde toohello.

## <a name="before-you-begin"></a>Avant de commencer

1.  **Déployez le Serveur de sauvegarde Azure**. Vérifiez que le Serveur de sauvegarde est correctement déployé. Pour plus d'informations, consultez les pages suivantes :
    * [Configuration requise pour le Serveur de sauvegarde Azure](http://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites)
    * [Matrice de protection du Serveur de sauvegarde](backup-mabs-protection-matrix.md)

2.  **Configurez le stockage**. Vous pouvez stocker des données de sauvegarde sur disque, sur bande et dans le cloud hello avec Azure. Pour plus d’informations, voir [Préparer l’espace de stockage](https://docs.microsoft.com/system-center/dpm/plan-long-and-short-term-data-storage).

3.  **Configurer l’agent de protection hello**. Installer l’agent de protection hello hello sur ordinateur sur lequel vous souhaitez tooback des. Pour plus d’informations, consultez [agent de protection DPM déployer hello](http://docs.microsoft.com/system-center/dpm/deploy-dpm-protection-agent).

## <a name="back-up-system-state-and-bare-metal"></a>Sauvegarde de l’état du système et récupération complète
Configurez un groupe de protection comme décrit dans [Déployer des groupes de protection](http://docs.microsoft.com/system-center/dpm/create-dpm-protection-groups). Notez que vous ne pouvez pas protéger une récupération complète et le système d’état pour hello même ordinateur dans différents groupes. Par ailleurs, lorsque vous sélectionnez la récupération complète, la protection de l’état du système est automatiquement activée.


1.  Assistant de créer un nouveau groupe de Protection tooopen hello Bonjour Console Administrateur du serveur de sauvegarde, sélectionnez **Protection** > **Actions** > **créer groupe de Protection Groupe**.

2.  Sur hello **sélectionner le Type de groupe de Protection** , sélectionnez **serveurs**, puis sélectionnez **suivant**.

3.  Sur hello **sélectionner les membres du groupe** page, développez hello ordinateur, puis sélectionnez **BMR** ou **état du système**.

    Souvenez-vous que vous ne peut pas protéger l’état de la récupération complète et système pour hello même ordinateur dans différents groupes. Par ailleurs, lorsque vous sélectionnez la récupération complète, la protection de l’état du système est automatiquement activée. Pour plus d’informations, voir [Déployer des groupes de protection](http://docs.microsoft.com/system-center/dpm/create-dpm-protection-groups).

4.  Sur hello **sélectionner la méthode de Protection des données** page, choisissez comment vous voulez que toohandle une sauvegarde à court terme et à long terme. Sauvegarde à court terme est toujours toodisk tout d’abord, avec l’option hello de sauvegarde à partir de hello disque toohello Azure cloud à l’aide de Azure Backup (à court terme ou à long terme). Un nuage de sauvegarde toohello toolong-terme de remplacement est tooset configuration à long terme tooa sauvegarde autonome appareil ou une bande bibliothèque de bandes tooBackup Server connecté.

5.  Sur hello **sélectionner les objectifs à court terme** page, sélectionnez le mode tooback stockage tooshort à long terme sur disque :
    1. Pour **de rétention**, sélectionnez la durée pendant laquelle les données de salutation tookeep sur le disque. 
    2. Pour **la fréquence de synchronisation**, sélectionnez la fréquence à laquelle vous souhaitez toorun une toodisk de sauvegarde incrémentielle. Si vous ne souhaitez pas tooset un intervalle de sauvegarde, vous pouvez vérifier hello **juste avant un point de récupération** option. Le Serveur de sauvegarde exécute une sauvegarde complète rapide juste avant chaque point de récupération planifié.

6.  Si vous souhaitez que les données de toostore sur bande pour le stockage à long terme, sur hello **spécifier les objectifs à long terme** , sélectionnez la durée pendant laquelle vous souhaitez que les données de bande de tookeep (1 à 99 ans). 
    1. Pour **fréquence de sauvegarde**, sélectionnez la fréquence à laquelle tootape sauvegarde doit s’exécuter. fréquence de Hello est basée sur la durée de rétention hello que vous avez sélectionné :
        * Lors de la durée de rétention hello est de 1 à 99 ans, vous pouvez sélectionner des sauvegardes toooccur quotidienne, hebdomadaire, bimensuelle, mensuelle, trimestrielle, semestrielle ou annuel.
        * Lors de la durée de rétention hello est 1-11 mois, vous pouvez sélectionner des sauvegardes toooccur quotidienne, hebdomadaire, bimensuelle ou mensuelle.
        * Lors de la durée de rétention hello est 1-4 semaines, vous pouvez sélectionner toooccur des sauvegardes quotidienne ou hebdomadaire.

    2. Sur hello **détails de bibliothèque et sélectionnez la bande** page, sélectionnez hello toouse de bibliothèque et de bande, et si les données doivent être compressées et chiffrées.

7.  Sur hello **vérifier l’Allocation de disque** , vérifiez l’espace disque de pool de stockage de hello est alloué pour le groupe de protection hello.

    1. **Nombre total de taille des données** taille hello de hello données tooback des.
    2. **Toobe d’espace disque approvisionné sur Azure Backup Server** espace hello qui vous recommande de sauvegarde du serveur pour le groupe de protection hello. Sauvegarde du serveur choisit hello idéale volume de sauvegarde en fonction des paramètres de hello. Toutefois, vous pouvez modifier les choix de volume de sauvegarde hello dans **détails de l’allocation de disque**. 
    3. Pour les charges de travail, dans le menu déroulant de hello, sélectionnez hello stockage préféré. Vos modifications modifier les valeurs hello **stockage Total** et **espace de stockage** Bonjour **stockage de disque disponible** volet. Espace underprovisioned est hello que serveur de sauvegarde suggère que vous ajoutez toohello volume, les sauvegardes smooth tooensure de stockage.

8.  Sur hello **choisir la méthode de création de réplica** , sélectionnez comment vous souhaitez que la réplication initiale complète des données toohandle hello. Si vous choisissez tooreplicate réseau hello, nous vous recommandons de choisir une heure creuse. Pour de grandes quantités de données ou les conditions de réseau qui ne sont pas optimales, envisagez de répliquer des données hello hors connexion à l’aide d’un support amovible.

9. Sur hello **choisissez les Options de vérification de cohérence** , sélectionnez comment vous souhaitez que les vérifications de cohérence tooautomate. Vous pouvez choisir toorun une vérification uniquement lorsque les données du réplica deviennent incohérentes ou selon une planification. Si vous ne souhaitez pas tooconfigure vérification de cohérence automatique, vous pouvez exécuter une vérification manuelle à tout moment. toorun une vérification manuelle, Bonjour **Protection** zone Hello la Console Administrateur de serveur de sauvegarde, avec le bouton droit de la protection hello groupe et sélectionnez **effectuer une vérification de cohérence**.

10. Si vous avez sélectionné tooback des toohello cloud à l’aide d’Azure Backup, sur hello **spécifier les données de Protection en ligne** , assurez-vous que vous sélectionnez les charges de travail hello souhaité tooback des tooAzure.

11. Sur hello **spécifier la planification de sauvegarde en ligne** , sélectionnez la fréquence à laquelle incrémentielles tooAzure se produit. Vous pouvez planifier des sauvegardes toorun chaque jour, semaine, mois et année et sélectionnez hello date et l’heure à laquelle il doit s’exécuter. Les sauvegardes peuvent se produire des tootwice quotidiennement. Chaque fois qu’une sauvegarde s’exécute, un point de récupération de données est créé dans Azure à partir de la copie de hello hello des données de sauvegarde stockées sur le disque de sauvegarde du serveur hello.

12. Sur hello **spécifier la stratégie de rétention en ligne** , sélectionnez la façon dont les points de récupération hello qui sont créés à partir des sauvegardes quotidiennes, hebdomadaires, mensuelles et annuelles hello sont conservés dans Azure.

13. Sur hello **choisir la réplication en ligne** , sélectionnez comment la réplication initiale complète hello de données se produit. Vous pouvez répliquer sur hello réseau faire ou hors connexion (l’amorçage en mode hors connexion) de sauvegarde. Sauvegarde en mode hors connexion utilise la fonctionnalité d’importation Azure hello. Pour plus d’informations, voir [Flux de travail de la sauvegarde hors connexion dans la sauvegarde Azure](backup-azure-backup-import-export.md).

14. Sur hello **Résumé** page, vérifiez vos paramètres. Après avoir sélectionné **créer un groupe**, la réplication initiale des données de salutation se produit. Lorsque la réplication des données se termine, hello **état** page, état du groupe de protection hello est **OK**. Sauvegarde, a lieu par la protection de hello les paramètres de groupe.

## <a name="recover-system-state-or-bmr"></a>Récupérer l’état du système ou la récupération complète
Vous pouvez récupérer l’emplacement de réseau de tooa état système ou la récupération complète. Si vous avez sauvegardé la récupération complète, utilisez toostart de l’environnement de récupération Windows (WinRE) de votre système et le connecter toohello réseau. Ensuite, utilisez toorecover de sauvegarde de Windows Server à partir de l’emplacement de réseau hello. Si vous avez sauvegardé l’état du système, utilisez simplement toorecover de sauvegarde de Windows Server à partir de l’emplacement de réseau hello.

### <a name="restore-bmr"></a>Restaurer une récupération complète
Exécuter la récupération sur l’ordinateur du serveur de sauvegarde hello :

1.  Bonjour **récupération** volet, rechercher un ordinateur hello vous souhaitez toorecover, puis sélectionnez **la récupération complète**.

2.  Points de récupération disponibles sont indiqués en gras dans le calendrier de hello. Sélectionnez les date hello et heure hello point de récupération que vous souhaitez toouse.

3.  Sur hello **sélectionner le Type de récupération** , sélectionnez **tooa copier le dossier réseau.**

4.  Sur hello **spécifier la Destination** page, sélectionnez où vous souhaitez que les données hello toocopy. N’oubliez pas que destination sélectionnée hello doit toohave suffisamment d’espace. Nous vous recommandons de créer un dossier.

5.  Sur hello **spécifier les Options de récupération** page, sélectionnez hello sécurité paramètres tooapply. Ensuite, sélectionnez si vous souhaitez toouse stockage réseau (SAN)-en fonction des captures instantanées matérielles, pour accélérer la récupération. (Ceci est une option uniquement si vous disposez d’un réseau SAN avec cette fonctionnalité et hello toocreate de capacité et fractionner un toomake clone il est accessible en écriture. En outre, hello ordinateur protégé et l’ordinateur serveur de sauvegarde doivent être connecté toohello même réseau.)

6.  Configurez les options de notification. Sur hello **Confirmation** page, sélectionnez **récupérer**.

Vous pouvez configurer l’emplacement du partage hello :

1.  Dans l’emplacement de restauration hello, accédez à dossier toohello qui dispose d’une sauvegarde hello.

2.  Partager le dossier hello qui est un niveau au-dessus de WindowsImageBackup afin que le dossier de WindowsImageBackup hello est hello racine du dossier partagé de hello. Si vous ne le faites pas, restauration ne trouve pas les sauvegarde hello. tooconnect en utilisant l’environnement de récupération Windows (WinRE), vous devez un partage auquel vous pouvez accéder dans WinRE avec les informations d’identification et l’adresse IP hello.

Restauration du système de hello :

1.  Hello démarrer l’ordinateur sur lequel vous souhaitez que les toorestore hello image à l’aide de hello DVD Windows pour le système de hello que vous restaurez.

2.  Sur la première page de hello, vérifiez les paramètres linguistiques et régionaux. Sur hello **installer** page, sélectionnez **réparer votre ordinateur**.

3.  Sur hello **Options de récupération système** page, sélectionnez **restaurer votre ordinateur à l’aide d’une image du système que vous avez créé précédemment**.

4.  Sur hello **sélectionner une sauvegarde d’image système** , sélectionnez **sélectionner une image système** > **avancé** > **recherche pour un système image sur hello réseau**. Si un avertissement s’affiche, sélectionnez **Oui**. Passez le chemin d’accès de partage toohello, entrez les informations d’identification hello, puis sélectionnez le point de récupération hello. Cette action déclenche une analyse des sauvegardes spécifiques disponibles dans ce point de récupération. Sélectionnez le point de récupération hello que vous souhaitez toouse.

5.  Sur hello **Choisissez comment toorestore hello sauvegarde** page, sélectionnez **formater et repartitionner les disques**. Sur la page suivante de hello, vérifiez les paramètres. 

6.  restauration de hello toobegin, sélectionnez **Terminer**. Un redémarrage est requis.

### <a name="restore-system-state"></a>Restaurer l’état du système

Exécutez la récupération dans le Serveur de sauvegarde :

1.  Bonjour **récupération** volet, hello rechercher un ordinateur que vous souhaitez toorecover, puis sélectionnez **la récupération complète**.

2.  Points de récupération disponibles sont indiqués en gras dans le calendrier de hello. Sélectionnez les date hello et heure hello point de récupération que vous souhaitez toouse.

3.  Sur hello **sélectionner le Type de récupération** , sélectionnez **tooa copier le dossier réseau**.

4.  Sur hello **spécifier la Destination** page, sélectionnez où vous souhaitez toocopy hello données. N’oubliez pas de que suffisamment d’espace a besoin de cette destination sélectionnée hello. Nous vous recommandons de créer un dossier.

5.  Sur hello **spécifier les Options de récupération** page, sélectionnez hello sécurité paramètres tooapply. Ensuite, indiquez si vous souhaitez des captures instantanées matérielles basées sur SAN de toouse pour accélérer la récupération. (Ceci est une option uniquement si vous disposez d’un réseau SAN avec cette fonctionnalité et hello toocreate de capacité et fractionner un toomake clone il est accessible en écriture. En outre, hello l’ordinateur protégé et serveur de sauvegarde du serveur doit être connecté toohello même réseau.)

6.  Configurez les options de notification. Sur hello **Confirmation** page, sélectionnez **récupérer**.

Exécutez l’application Sauvegarde Windows Server :

1.  Sélectionnez **Actions** > **Récupérer** > **Ce serveur** > **Suivant**.

2.  Sélectionnez **un autre serveur**, sélectionnez hello **spécifier un Type d’emplacement** page, puis sélectionnez **dossier partagé distant**. Entrez hello chemin d’accès toohello dossier qui contient le point de récupération hello.

3.  Sur hello **sélectionner le Type de récupération** , sélectionnez **état du système**. 

4. Sur hello **sélectionner l’emplacement pour la récupération de l’état système** , sélectionnez **emplacement d’origine**.

5.  Sur hello **Confirmation** page, sélectionnez **récupérer**. Après la restauration de hello, hello chargera.

6.  Vous pouvez également exécuter hello restauration d’état du système à une invite de commandes. toodo, début de sauvegarde de Windows Server sur l’ordinateur de hello souhaité toorecover. identificateur de version hello tooget, à l’invite de commandes, entrez :```wbadmin get versions -backuptarget \<servername\sharename\>```

    Utilisez hello version identificateur toostart hello état la restauration du système. À l’invite de commandes hello, entrez :```wbadmin start systemstaterecovery -version:<versionidentified> -backuptarget:<servername\sharename>```

    Confirmer la restauration de hello toostart. Vous pouvez voir les processus hello dans la fenêtre d’invite de commandes hello. Un journal de restauration est créé. Après la restauration de hello, hello chargera.

