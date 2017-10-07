---
title: "les coffres de sauvegarde Azure aaaManage et serveurs Azure en utilisant le modèle de déploiement classique hello | Documents Microsoft"
description: Utilisez ce didacticiel toolearn comment les coffres toomanage Azure Backup et les serveurs.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 6c38b04f4a76604bfd639a9b2d58237ce44e2386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-hello-classic-deployment-model"></a>Gérer les coffres de sauvegarde Azure et les serveurs à l’aide du modèle de déploiement classique de hello
> [!div class="op_single_selector"]
> * [Gestionnaire de ressources](backup-azure-manage-windows-server.md)
> * [Classique](backup-azure-manage-windows-server-classic.md)
>
>

Dans cet article, vous trouverez une vue d’ensemble des tâches de gestion de sauvegarde hello disponibles via le portail Azure classic de hello et l’agent Microsoft Azure Backup de hello.

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

> [!IMPORTANT]
> Vous pouvez maintenant mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services. Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.<br/> Après le 15 octobre 2017, vous ne pouvez pas utiliser les coffres de sauvegarde toocreate PowerShell. **D’ici au 1er novembre 2017** :
>- Tous les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.
>- Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello. Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.
>

## <a name="management-portal-tasks"></a>Tâches du portail de gestion
1. Connectez-vous à toohello [portail de gestion](https://manage.windowsazure.com).
2. Cliquez sur **Services de récupération**, puis cliquez sur nom hello de page de démarrage rapide de coffre de sauvegarde tooview hello.

    ![Recovery Services](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

En sélectionnant les options de hello en hello haut hello démarrage rapide, vous pouvez voir les tâches de gestion disponibles hello.

![Gérer les onglets](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a>tableau de bord
Sélectionnez **tableau de bord** présentation de l’utilisation de hello toosee pour le serveur de hello. Hello **présentation de l’utilisation** inclut :

* nombre de Hello des serveurs Windows inscrits toocloud
* nombre de Hello de machines virtuelles protégées dans le cloud
* stockage total de Hello consommé dans Azure
* état Hello des tâches récentes

En bas de hello Hello du tableau de bord, vous pouvez effectuer hello tâches suivantes :

* **Gérer le certificat** - si un certificat était utilisé tooregister hello serveur, puis utiliser ce certificat de hello tooupdate. Si vous utilisez des informations d'identification de coffre, n'utilisiez pas **Manage certificate**.
* **Supprimer** -coffre de sauvegarde en cours de suppressions hello. Si un coffre de sauvegarde est n’est plus utilisé, vous pouvez le supprimer toofree l’espace de stockage. **Supprimer** est activé uniquement après la suppression de tous les serveurs inscrits dans le coffre de hello.

![Tâches du tableau de bord Backup](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a>Éléments inscrits
Sélectionnez **éléments inscrits** tooview les noms de hello des serveurs hello sont inscrits toothis coffre.

![Éléments inscrits](./media/backup-azure-manage-windows-server-classic/registered-items.png)

Hello **Type** filtre par défaut est tooAzure Machine virtuelle. les noms de hello tooview des serveurs hello toothis inscrits coffre, **Windows server** de hello menu déroulant.

À ce stade, vous pouvez effectuer hello tâches suivantes :

* **Autoriser la réinscription** - lorsque cette option est sélectionnée pour un serveur, vous pouvez utiliser hello **Assistant Inscription** dans hello Microsoft Azure Backup agent tooregister hello serveur local avec le coffre de sauvegarde hello une deuxième fois. . Vous devrez peut-être toore dans le Registre en raison de l’erreur tooan dans le certificat de hello ou si un serveur a rencontré toobe reconstruit.
* **Supprimer** -supprime un serveur d’archivage de sauvegarde hello. Toutes les données stockée hello associées avec le serveur de hello est supprimé immédiatement.

    ![Tâches d’éléments inscrits](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a>Éléments protégés
Sélectionnez **éléments protégés** éléments hello tooview qui ont été sauvegardées à partir de serveurs de hello.

![Éléments protégés](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a>Configuration
À partir de hello **configurer** onglet, vous pouvez sélectionner option de redondance de stockage approprié hello. Hello meilleur temps tooselect hello option redondance du stockage est juste après la création d’un coffre et avant tous les ordinateurs sont inscrit tooit.

> [!WARNING]
> Une fois qu’un élément a été inscrit toohello coffre, option de redondance du stockage hello est verrouillée et ne peut pas être modifiée.
>
>

![Configuration](./media/backup-azure-manage-windows-server-classic/configure.png)

Consultez cet article pour plus d’informations sur la [redondance du stockage](../storage/common/storage-redundancy.md).

## <a name="microsoft-azure-backup-agent-tasks"></a>Tâches de l’agent Microsoft Azure Backup
### <a name="console"></a>Console
Ouvrez hello **Microsoft Azure Backup agent** (vous pouvez le trouver en recherchant de votre ordinateur pour *Microsoft Azure Backup*).

![Agent Backup](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

À partir de hello **Actions** disponible à l’adresse hello à droite de la console de l’agent de sauvegarde hello effectuer hello les tâches de gestion suivantes :

* Inscription du serveur
* Planification d’une sauvegarde
* Sauvegarder maintenant
* Modifier les propriétés

![Actions de la console de l’agent](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> trop**récupérer les données**, consultez [restaurer des fichiers tooa Windows server ou la machine du client Windows](backup-azure-restore-windows-server.md).
>
>

### <a name="modify-an-existing-backup"></a>Modifier une sauvegarde existante
1. Dans l’agent Microsoft Azure Backup hello, cliquez sur **planifier la sauvegarde**.

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. Bonjour **Assistant Planification de sauvegarde** laisser hello **apporter des modifications heures ou les éléments de toobackup** option est sélectionnée, puis cliquez sur **suivant**.

    ![Modifier une sauvegarde planifiée](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. Si vous souhaitez tooadd ou de modifier les éléments sur hello **tooBackup de sélectionner les éléments** écran, cliquez sur **ajouter les éléments**.

    Vous pouvez également définir **paramètres d’Exclusion** à partir de cette page dans l’Assistant de hello. Si vous souhaitez que les fichiers tooexclude ou procédure hello pour l’ajout de lecture de types de fichiers [paramètres d’exclusion](#exclusion-settings).
4. Sélectionnez les fichiers de hello et les dossiers que vous souhaitez tooback haut et cliquez sur **OK**.

    ![Sélectionner les éléments à sauvegarder](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. Spécifiez hello **planification de sauvegarde** et cliquez sur **suivant**.

    Vous pouvez planifier des sauvegardes quotidiennes (au maximum 3 fois par jour) ou hebdomadaires.

    ![Spécifier votre planification de sauvegarde](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > Spécifier la planification de sauvegarde hello est expliquée en détail dans ce [article](backup-azure-backup-cloud-as-tape.md).
   >
   >
6. Sélectionnez hello **stratégie de rétention** pour la copie de sauvegarde hello et cliquez sur **suivant**.

    ![Sélectionner votre stratégie de rétention](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. Sur hello **Confirmation** hello consulter les informations de l’écran, puis cliquez sur **Terminer**.
8. Une fois l’Assistant de hello termine la création de hello **planification de sauvegarde**, cliquez sur **fermer**.

    Après la modification de protection, vous pouvez vérifier le déclenchement de sauvegardes par toohello de va **travaux** onglet et en s’assurant que les modifications sont répercutées dans hello des travaux de sauvegarde.

### <a name="enable-network-throttling"></a>Activation de la limitation du réseau
agent de sauvegarde Azure Hello comprend un onglet de limitation qui vous permet de toocontrol utilisation de la bande passante réseau lors du transfert de données. Ce contrôle peut être utile si vous devez tooback des données pendant les heures de travail mais que vous ne souhaitez pas que toointerfere du processus de sauvegarde hello avec tout autre trafic internet. La limitation des données de transfert s’applique tooback des activités et de restauration.  

tooenable de limitation :

1. Bonjour **agent de sauvegarde**, cliquez sur **modifier les propriétés**.
2. Sélectionnez hello **activer l’utilisation de la bande passante internet pour les opérations de sauvegarde de limitation** case à cocher.

    ![Limitation du réseau](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. Une fois que vous avez activé la limitation, spécifiez hello autorisée de la bande passante pour transférer des données de sauvegarde pendant **des heures de travail** et **heures chômées**.

    valeurs de la bande passante Hello commencent à 512 kilo-octets par seconde (Kbits/s) et peuvent atteindre la too1023 les mégaoctets par seconde (Mbits/s). Vous pouvez également désigner le début de hello et de fin de **des heures de travail**, et les jours de semaine de hello sont considérés comme travail jours. temps de Hello en dehors de hello désigné des heures de travail est toobe pris en compte les heures chômées.
4. Cliquez sur **OK**.

## <a name="exclusion-settings"></a>Paramètres d’exclusion
1. Ouvrez hello **Microsoft Azure Backup agent** (vous pouvez le trouver en recherchant de votre ordinateur pour *Microsoft Azure Backup*).

    ![Ouvrir l’agent Backup](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. Dans l’agent Microsoft Azure Backup hello, cliquez sur **planifier la sauvegarde**.

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. Bonjour Assistant Planification de sauvegarde, laissez hello **apporter des modifications heures ou les éléments de toobackup** option est sélectionnée, puis cliquez sur **suivant**.

    ![Modifier une planification](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. Cliquez sur **Paramètres d’exclusion**.

    ![Sélectionner des éléments tooexclude](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. Cliquez sur **Ajouter une exclusion**.

    ![Ajouter des exclusions](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. Sélectionnez l’emplacement de hello et cliquez ensuite sur **OK**.

    ![Sélectionnez un emplacement pour l’exclusion](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. Extension de fichier hello Bonjour **Type de fichier** champ.

    ![Exclure par type de fichier](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    Ajout d’une extension .mp3

    ![Exemple de type de fichier](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    tooadd une autre extension, cliquez sur **ajouter une Exclusion** et entrez une autre extension de fichier (l’ajout d’une extension .jpeg).

    ![Autre exemple de type de fichier](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. Lorsque vous avez ajouté toutes les extensions de hello, cliquez sur **OK**.
9. Poursuivez hello Assistant Planification de sauvegarde en cliquant sur **suivant** jusqu'à hello **page de Confirmation**, puis cliquez sur **Terminer**.

    ![Confirmation de l’exclusion](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a>Étapes suivantes
* [Restaurer un serveur Windows Server ou un client Windows à partir d’Azure](backup-azure-restore-windows-server.md)
* toolearn en savoir plus sur Azure Backup, consultez [vue d’ensemble de la sauvegarde Azure](backup-introduction-to-azure-backup.md)
* Visitez hello [Forum de sauvegarde Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)
