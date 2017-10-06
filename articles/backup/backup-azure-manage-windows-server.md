---
title: aaaManage Azure recovery services coffres et serveurs | Documents Microsoft
description: "Utilisez ce didacticiel toolearn comment les services de récupération Azure toomanage coffres et les serveurs."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markgal
ms.openlocfilehash: b4c35c86faa0828b3c63a13b85c095c0cbaba50e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a>Surveiller et gérer les serveurs et les coffres Azure Recovery services pour les ordinateurs Windows
> [!div class="op_single_selector"]
> * [Gestionnaire de ressources](backup-azure-manage-windows-server.md)
> * [Classique](backup-azure-manage-windows-server-classic.md)
>
>

Dans cet article vous trouverez une vue d’ensemble de hello analyse et gestion des tâches de sauvegarde disponibles via hello agent Microsoft Azure Backup Azure portal et hello. Cet article part du principe que vous disposez déjà d’un abonnement Azure et que vous avez créé au moins un coffre Recovery Services.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a>Ouvrez un coffre Recovery Services

tableau de bord coffre de Services de récupération Hello vous montre les détails de hello ou les attributs d’un coffre Recovery Services.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/) à l’aide de votre abonnement Azure.
2. Dans le menu du Hub hello, cliquez sur **plus Services**.

    ![Ouvrir une liste de Recovery Services - Étape 1](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. Vous voulez tooopen un coffre Recovery Services. Dans la boîte de dialogue hello, commencez à taper **Recovery Services**. Comme vous commencez à taper, liste de hello filtre en fonction de votre entrée. Cliquez sur **les coffres de Services de récupération** les coffres de liste de hello toodisplay des Services de récupération dans votre abonnement.

    ![Créer un archivage de Recovery Services - Étape 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    liste Hello des archivages de Recovery Services s’ouvre.

    ![Créer un archivage de Recovery Services - Étape 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. À partir de la liste de hello des coffres, sélectionnez le nom de hello Hello coffre Recovery Services tooopen. Panneau de tableau de bord coffre Hello Recovery Services s’ouvre.

    ![coffre recovery services tableau de bord](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    Maintenant que vous avez ouvert le coffre Recovery Services hello, essayez une des tâches de surveillance ni gestion hello.

## <a name="monitor-backup-jobs-and-alerts"></a>Surveiller les travaux et les alertes de sauvegarde

Vous surveillez les travaux et alertes à partir de hello Services de récupération de coffre de tableau de bord, où vous voyez :

* Les détails des alertes de sauvegarde
* Fichiers et dossiers, ainsi que les machines virtuelles protégées dans le cloud de hello
* Le stockage total consommé dans Azure
* L’état du travail de sauvegarde

![Tâches du tableau de bord Backup](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

En cliquant sur les informations de hello dans chacun de ces vignettes ouvrir Panneau associé de hello où vous gérer les tâches associées.

De haut hello Hello du tableau de bord :

* Panneau Paramètres : vous donne accès aux tâches de sauvegarde disponibles.
* Coffre de sauvegarde - permet de sauvegarder des fichiers et dossiers (ou machines virtuelles Azure) toohello Recovery Services.
* DELETE - si des services de récupération d’un coffre est n’est plus utilisé, vous pouvez le supprimer toofree l’espace de stockage. DELETE est activée uniquement après la suppression de tous les serveurs protégés à partir du coffre de hello.

![Tâches du tableau de bord Backup](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a>Alertes relatives aux sauvegardes à l’aide de l’agent de sauvegarde Azure :
| Niveau d’alerte | Alertes envoyées |
| --- | --- |
| Critique |Échec de sauvegarde, échec de récupération |
| Avertissement |Sauvegarde s’est terminée avec avertissements (si les fichiers de moins de cent ne sont pas sauvegardés en raison de problèmes de toocorruption, et plusieurs millions fichiers sont correctement sauvegardés) |
| Informations |Aucun |

## <a name="manage-backup-alerts"></a>Gérer les alertes de sauvegarde
Cliquez sur hello **les alertes de sauvegarde** vignette tooopen hello **les alertes de sauvegarde** panneau et gérer les alertes.

![Alertes de sauvegarde](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

Alertes de sauvegarde Hello vignette vous montre hello nombre de :

* le nombre d’alertes critiques non résolues dans les 24 dernières heures
* le nombre d’alertes d’avertissement non résolues dans les 24 dernières heures

En cliquant sur chacun de ces liens vous conduit toohello **les alertes de sauvegarde** panneau avec une vue filtrée de ces alertes (critiques ou avertissements).

À partir du panneau d’alertes de sauvegarde hello, vous :

* Choisissez tooinclude des informations appropriées hello avec vos alertes.

    ![Choisir les colonnes](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* Filtrer les alertes selon leur gravité, leur état et les heures de début/fin

    ![Filtrer les alertes](./media/backup-azure-manage-windows-server/filter-alerts.png)
* Configurer les paramètres de gravité, de fréquence et de destination des notifications, mais aussi activer ou désactiver les alertes

    ![Filtrer les alertes](./media/backup-azure-manage-windows-server/configure-notifications.png)

Si **par alerte** est sélectionné comme hello **notifier** fréquence aucun regroupement ou une réduction des courriers électroniques se produit. Chaque alerte génère une notification. C’est le paramètre par défaut de hello et courrier électronique de résolution hello est envoyé également immédiatement.

Si **horaire Digest** est sélectionné comme hello **notifier** fréquence un e-mail est envoyée à utilisateur toohello indiquant qu’il n’y pas résolu nouvelles alertes générés Bonjour dernière heure. Un message électronique de résolution est envoyé à fin hello d’heure de hello.

Les alertes peuvent être envoyées pour hello suivant des niveaux de gravité :

* Critique
* Avertissement
* information

Vous désactivez l’alerte hello avec hello **désactiver** bouton dans le panneau de détails de tâche hello. Lorsque vous cliquez sur Inactivate (Désactiver), vous pouvez ajouter des commentaires pour la résolution de l’alerte.

Vous choisissez les colonnes hello souhaité dans le cadre de l’alerte hello avec hello tooappear **choisir les colonnes** bouton.

> [!NOTE]
> À partir de hello **paramètres** panneau, vous gérez les alertes de sauvegarde en sélectionnant **analyse et rapports > alertes et événements > alertes de sauvegarde** , puis en cliquant sur **filtre** ou  **Configurer des Notifications**.
>
>

## <a name="manage-backup-items"></a>Gérer les éléments de sauvegarde
La gestion des sauvegardes en local est maintenant disponible dans le portail de gestion hello. Dans la section de sauvegarde hello du tableau de bord hello, hello **des éléments de sauvegarde** vignette affiche le nombre de hello des éléments de sauvegarde protégés toohello coffre.

Cliquez sur **fichiers-dossiers** Bonjour vignette d’éléments de sauvegarde.

![Mosaïque Éléments de sauvegarde](./media/backup-azure-manage-windows-server/backup-items-tile.png)

les éléments de sauvegarde Hello panneau s’ouvre avec hello filtrer ensemble tooFile-dossier dans lequel vous consultez chaque élément répertorié de sauvegarde spécifique.

![Éléments de sauvegarde](./media/backup-azure-manage-windows-server/backup-item-list.png)

Si vous sélectionnez un élément de sauvegarde spécifique à partir de la liste de hello, vous consultez des informations essentielles hello pour cet élément.

> [!NOTE]
> À partir de hello **paramètres** panneau, vous gérez des fichiers et dossiers en sélectionnant **éléments protégés > des éléments de sauvegarde** , puis en sélectionnant **dossiers de fichiers** de hello menu déroulant.
>
>

![Éléments de sauvegarde à partir des paramètres](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a>Gérer les travaux de sauvegarde
Tâches de sauvegarde pour à la fois localement (lorsque le serveur local de hello sauvegarde tooAzure) et les sauvegardes Azure sont visibles dans le tableau de bord hello.

Dans la section de sauvegarde du tableau de bord hello de hello, vignette de travail de sauvegarde hello affiche hello nombre tâches :

* en cours
* Échec de hello des dernières 24 heures.

toomanage vos travaux de sauvegarde, cliquez sur hello **les travaux de sauvegarde** vignette, qui ouvre le panneau des travaux de sauvegarde hello.

![Éléments de sauvegarde à partir des paramètres](./media/backup-azure-manage-windows-server/backup-jobs.png)

Vous modifiez les informations hello disponibles dans le panneau des travaux de sauvegarde hello avec hello **choisir les colonnes** bouton en hello haut hello.

Hello d’utilisation **filtre** tooselect bouton entre fichiers et de dossiers et de sauvegarde de la machine virtuelle Azure.

Si vous ne voyez pas votre sauvegarde des fichiers et des dossiers, cliquez sur **filtre** bouton en haut de hello de page de hello et sélectionnez **fichiers et dossiers** à partir du menu de Type d’élément hello.

> [!NOTE]
> À partir de hello **paramètres** panneau, gérer des travaux de sauvegarde en sélectionnant **analyse et rapports > travaux > travaux de sauvegarde** , puis en sélectionnant **dossiers de fichiers** de dépôt de hello vers le bas du menu.
>
>

## <a name="monitor-backup-usage"></a>Surveiller l’utilisation de la sauvegarde
Dans la section de sauvegarde du tableau de bord hello de hello, vignette d’utilisation de la sauvegarde de hello montre stockage hello consommé dans Azure. Les données d’utilisation du stockage incluent :

* Utilisation du stockage LRS cloud associée hello coffre
* Utilisation du stockage GRS cloud associée hello coffre

## <a name="manage-your-production-servers"></a>Gérer vos serveurs de production
Cliquez sur les serveurs de production, toomanage **paramètres**.

Sous Gérer, cliquez sur **Infrastructure de sauvegarde > Serveurs de Production**.

listes de panneau Hello les serveurs de Production de tous vos serveurs de production disponible. Cliquez sur un serveur dans les détails du serveur hello liste tooopen hello.

![Éléments protégés](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-hello-azure-backup-agent"></a>Agent de sauvegarde Azure hello ouvert
Ouvrez hello **Microsoft Azure Backup agent** (vous le rechercher votre ordinateur pour *Microsoft Azure Backup*).

![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)

À partir de hello **Actions** disponible à l’adresse hello à droite de la console de l’agent de sauvegarde hello vous effectuez hello les tâches de gestion suivantes :

* Inscription du serveur
* Planification d’une sauvegarde
* Sauvegarder maintenant
* Modifier les propriétés

![Actions de la console de l’agent Microsoft Azure Backup.](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> trop**récupérer les données**, consultez [restaurer des fichiers tooa Windows server ou la machine du client Windows](backup-azure-restore-windows-server.md).
>
>

## <a name="modify-hello-backup-schedule"></a>Modifier la planification de sauvegarde hello
1. Dans l’agent Microsoft Azure Backup hello, cliquez sur **planifier la sauvegarde**.

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. Bonjour **Assistant Planification de sauvegarde** laisser hello **apporter des modifications heures ou les éléments de toobackup** option est sélectionnée, puis cliquez sur **suivant**.

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. Si vous souhaitez tooadd ou de modifier les éléments sur hello **tooBackup de sélectionner les éléments** écran, cliquez sur **ajouter les éléments**.

    Vous pouvez également définir **paramètres d’Exclusion** à partir de cette page dans l’Assistant de hello. Si vous souhaitez que les fichiers tooexclude ou procédure hello pour l’ajout de lecture de types de fichiers [paramètres d’exclusion](#manage-exclusion-settings).
4. Sélectionnez les fichiers de hello et les dossiers que vous souhaitez tooback haut et cliquez sur **OK**.

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. Spécifiez hello **planification de sauvegarde** et cliquez sur **suivant**.

    Vous pouvez planifier des sauvegardes quotidiennes (au maximum 3 fois par jour) ou hebdomadaires.

    ![Éléments de sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > Spécifier la planification de sauvegarde hello est expliquée en détail dans ce [article](backup-azure-backup-cloud-as-tape.md).
   >

6. Sélectionnez hello **stratégie de rétention** pour la copie de sauvegarde hello et cliquez sur **suivant**.

    ![Éléments de sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. Sur hello **Confirmation** hello consulter les informations de l’écran, puis cliquez sur **Terminer**.
8. Une fois l’Assistant de hello termine la création de hello **planification de sauvegarde**, cliquez sur **fermer**.

    Après la modification de protection, vous pouvez vérifier le déclenchement de sauvegardes par toohello de va **travaux** onglet et en s’assurant que les modifications sont répercutées dans hello des travaux de sauvegarde.

## <a name="enable-network-throttling"></a>Activation de la limitation du réseau

agent de sauvegarde Azure Hello comprend un onglet de limitation qui vous permet de toocontrol utilisation de la bande passante réseau lors du transfert de données. Ce contrôle peut être utile si vous devez tooback des données pendant les heures de travail mais que vous ne souhaitez pas que toointerfere du processus de sauvegarde hello avec tout autre trafic internet. La limitation des données de transfert s’applique tooback des activités et de restauration.  

tooenable de limitation :

1. Bonjour **agent de sauvegarde**, cliquez sur **modifier les propriétés**.
2. Sur hello ** limitation onglet, sélectionnez **activer l’utilisation de la bande passante internet de limitation pour les opérations de sauvegarde**.

    ![Limitation du réseau](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    Une fois que vous avez activé la limitation, spécifiez hello autorisée de la bande passante pour transférer des données de sauvegarde pendant **des heures de travail** et **heures chômées**.

    valeurs de la bande passante Hello commencent à 512 kilo-octets par seconde (Kbits/s) et peuvent atteindre la too1023 les mégaoctets par seconde (Mbits/s). Vous pouvez également désigner le début de hello et de fin de **des heures de travail**, et les jours de semaine de hello sont considérés comme travail jours. temps de Hello en dehors de hello désigné des heures de travail est toobe pris en compte les heures chômées.
3. Cliquez sur **OK**.

## <a name="manage-exclusion-settings"></a>Gérer les paramètres d’exclusion
1. Ouvrez hello **Microsoft Azure Backup agent** (vous pouvez le trouver en recherchant de votre ordinateur pour *Microsoft Azure Backup*).

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. Dans l’agent Microsoft Azure Backup hello, cliquez sur **planifier la sauvegarde**.

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. Bonjour Assistant Planification de sauvegarde, laissez hello **apporter des modifications heures ou les éléments de toobackup** option est sélectionnée, puis cliquez sur **suivant**.

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. Cliquez sur **Paramètres d’exclusion**.

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. Cliquez sur **Ajouter une exclusion**.

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. Sélectionnez l’emplacement de hello et cliquez ensuite sur **OK**.

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. Extension de fichier hello Bonjour **Type de fichier** champ.

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    Ajout d’une extension .mp3

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    tooadd une autre extension, cliquez sur **ajouter une Exclusion** et entrez une autre extension de fichier (l’ajout d’une extension .jpeg).

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. Lorsque vous avez ajouté toutes les extensions de hello, cliquez sur **OK**.
9. Poursuivez hello Assistant Planification de sauvegarde en cliquant sur **suivant** jusqu'à hello **page de Confirmation**, puis cliquez sur **Terminer**.

    ![Planifier une sauvegarde de Windows Server](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a>Forum Aux Questions
**Q1. état du travail de sauvegarde Hello affiche comme étant terminée en hello agent de sauvegarde Azure, pourquoi n’il obtenir répercutée immédiatement dans le portail ?**

R1. Il est au délai maximal de 15 minutes entre l’état du travail de sauvegarde hello répercutée dans hello agent de sauvegarde Azure et hello portail Azure.

**Q.2 en cas d’échec d’une opération de sauvegarde, combien de temps faut-il tooraise une alerte ?**

A.2 une alerte est générée au sein de 20 minutes de hello Échec de sauvegarde Azure.

**Q3. Est-il possible qu’aucun e-mail ne soit envoyé alors que les notifications sont activées ?**

R3 Voici les cas de hello lorsque hello notification ne sera pas être envoyée dans un bruit de commande tooreduce hello alerte :

* Si les notifications sont configurées par heure et une alerte est déclenchée et résolue au sein de l’heure de hello
* Si le travail est annulé.
* Si le travail de sauvegarde secondaire a échoué, car un travail de sauvegarde d’origine est en cours.

## <a name="troubleshooting-monitoring-issues"></a>Résolution des problèmes de surveillance
**Problème :** travaux et/ou les alertes à partir de l’agent de sauvegarde Azure hello n’apparaissent pas dans le portail de hello.

**Étapes de dépannage :** hello processus, ```OBRecoveryServicesManagementAgent```, envoie hello toohello de données de travail et d’alerte service Azure Backup. Il peut arriver que ce processus se bloque ou s’arrête.

1. processus de hello tooverify n’est pas en cours d’exécution, ouvrez **le Gestionnaire des tâches** et vérifiez si hello ```OBRecoveryServicesManagementAgent``` est en cours.
2. En supposant que le processus de hello ne fonctionne pas, ouvrez **le panneau de configuration** et parcourir la liste hello des services. Démarrez ou redémarrez l’**Agent de gestion Microsoft Azure Recovery Services**.

    Pour plus d’informations, consultez journaux hello à :<br/>
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` Par exemple :<br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a>Étapes suivantes
* [Restaurer un serveur Windows Server ou un client Windows à partir d’Azure](backup-azure-restore-windows-server.md)
* toolearn en savoir plus sur Azure Backup, consultez [vue d’ensemble de la sauvegarde Azure](backup-introduction-to-azure-backup.md)
* Visitez hello [Forum de sauvegarde Azure](http://go.microsoft.com/fwlink/p/?LinkId=290933)
