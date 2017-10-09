---
title: "aaaAzure sauvegarde pour les charges de travail de SQL Server à l’aide d’Azure Backup Server | Documents Microsoft"
description: "Un toobacking présentation des bases de données SQL Server à l’aide d’Azure Backup Server"
services: backup
documentationcenter: 
author: pvrk
manager: Shivamg
editor: 
ms.assetid: c8b1f7ec-26b1-4ef0-a3f2-91aec959daea
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 3a94338e8aca3f9d8611a72bcd223397ffb96f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-sql-server-tooazure-with-azure-backup-server"></a>Sauvegarder SQL Server tooAzure avec Azure Backup Server
Cet article vous guide tout au long des étapes de configuration hello pour la sauvegarde des bases de données SQL Server à l’aide de Microsoft Azure sauvegarde serveur (MABS).

gestion de Hello des tooAzure de sauvegarde de base de données SQL Server et de récupération à partir de Azure implique trois étapes :

1. Créer un tooAzure de bases de données de stratégie de sauvegarde tooprotect SQL Server.
2. Créer des copies de sauvegarde à la demande tooAzure.
3. Récupérer hello de base de données Azure.

## <a name="before-you-start"></a>Avant de commencer
Avant de commencer, assurez-vous d’avoir [installé et préparé hello Azure Backup Server](backup-azure-microsoft-azure-backup.md).

## <a name="create-a-backup-policy-tooprotect-sql-server-databases-tooazure"></a>Créer un tooAzure de bases de données de stratégie de sauvegarde tooprotect SQL Server
1. Sur hello l’interface utilisateur de serveur de sauvegarde Azure, cliquez sur hello **Protection** espace de travail.
2. Dans la barre d’outils hello, cliquez sur **nouveau** toocreate un nouveau groupe de protection.

    ![Créer un groupe de protection](./media/backup-azure-backup-sql/protection-group.png)
3. MABS affiche l’écran d’accueil hello grâce à l’aide de hello sur la création d’un **groupe de Protection**. Cliquez sur **Suivant**.
4. Sélectionnez **Serveurs**.

    ![Sélectionner le type de groupe de protection - « Servers »](./media/backup-azure-backup-sql/pg-servers.png)
5. Développez l’ordinateur SQL Server hello où hello toobe de bases de données sauvegardée sont présents. Le serveur de sauvegarde Microsoft Azure affiche diverses sources de données pouvant être sauvegardées à partir de ce serveur. Développez hello **tous les partages SQL** et sélectionnez les bases de données hello (dans ce cas nous sélectionné ReportServer$ MSDPM2012 et ReportServer$ MSDPM2012TempDB) toobe sauvegardé. Cliquez sur **Suivant**.

    ![Sélectionner la base de données SQL](./media/backup-azure-backup-sql/pg-databases.png)
6. Fournissez un nom pour le groupe de protection hello et sélectionnez hello **je souhaite une Protection en ligne** case à cocher.

    ![Méthode de Protection des données - disque à court terme et Azure en ligne](./media/backup-azure-backup-sql/pg-name.png)
7. Bonjour **spécifier les objectifs à court terme** écran, inclure toodisk de points de sauvegarde toocreate hello entrées nécessaires.

    Ici, nous constatons que **de rétention** est défini trop*5 jours*, **la fréquence de synchronisation** a la valeur tooonce chaque *15 minutes* qui est hello fréquence à laquelle la sauvegarde est effectuée. **Sauvegarde complète rapide** est défini trop*8 h 00*.

    ![Spécifier les objectifs à court terme](./media/backup-azure-backup-sql/pg-shortterm.png)

   > [!NOTE]
   > À 8 h 00 (selon l’entrée d’écran de toohello), un point de sauvegarde est créé chaque jour par le transfert de données hello qui a été modifiées de hello point de sauvegarde de 8 h 00 du jour précédent. Ce processus est appelé **Sauvegarde expresse rapide**. Pendant la synchronisation des journaux de transactions hello toutes les 15 minutes, si elle existe une base de données nécessaire toorecover hello à 21:00 – point de hello est créée en relisant les journaux hello de hello express dernier point de sauvegarde complète (20 h 00 dans ce cas).
   >
   >

8. Cliquez sur **Suivant**

    MABS affiche hello globale espace de stockage disponible et hello potentielle d’espace disque utilisé.

    ![Allocation de disque](./media/backup-azure-backup-sql/pg-storage.png)

    Par défaut, MABS crée un volume par la source de données (base de données SQL Server) qui est utilisé pour la copie de sauvegarde initiale hello. À l’aide de cette approche, hello Gestionnaire de disque logique (LDM) limite les sources de données too300 MABS protection (bases de données SQL Server). toowork contourner cette limitation, sélectionnez hello **colocaliser les données dans le Pool de stockage DPM**, option. Si vous utilisez cette option, MABS utilise un volume unique pour plusieurs sources de données, ce qui permet de tooprotect MABS des bases de données SQL too2000.

    Si **augmenter automatiquement les volumes hello** option est sélectionnée, MABS peut compte pour le volume de sauvegarde hello augmente à mesure que les données de production hello augmentent. Si **augmenter automatiquement les volumes hello** option n’est pas sélectionnée, MABS limite de stockage de sauvegarde utilisé hello toohello des sources de données dans le groupe de protection hello.
9. Les administrateurs obtiennent choix hello de transfert de cette surcharge de la bande passante initiale tooavoid sauvegarde manuellement (hors réseau) ou sur le réseau de hello. Ils peuvent également configurer le moment hello à quels hello transfert initial peut se produire. Cliquez sur **Suivant**.

    ![Méthode de réplication initiale](./media/backup-azure-backup-sql/pg-manual.png)

    copie de sauvegarde initiale Hello nécessite le transfert de hello toute source de données (base de données SQL Server) à partir de tooMABS (ordinateur SQL Server) de serveur de production. Ces données peuvent être volumineux et transfert de données hello réseau hello peut dépasser la bande passante. Pour cette raison, les administrateurs peuvent choisir de sauvegarde initiale de hello tootransfer : **manuellement** (à l’aide d’un support amovible) tooavoid congestion de la bande passante, ou **automatiquement sur le réseau de hello** (au niveau spécifié heure).

    Une fois la sauvegarde initiale de hello est terminée, hello autres sauvegardes de hello sont des sauvegardes incrémentielles sur la copie de sauvegarde initiale hello. Les sauvegardes incrémentielles ont tendance toobe petit et peuvent être facilement transférés réseau hello.
10. Indiquez quand vous voulez toorun de vérification de cohérence hello et cliquez sur **suivant**.

    ![Vérifier la cohérence](./media/backup-azure-backup-sql/pg-consistent.png)

    MABS peut effectuer une cohérence vérifier toocheck hello l’intégrité du point de sauvegarde hello. Il calcule la somme de contrôle hello hello du fichier de sauvegarde sur le serveur de production hello (SQL Server de l’ordinateur dans ce scénario) et hello les données sauvegardées pour ce fichier dans MABS. Dans les cas de hello d’un conflit, il est supposé que hello sauvegardé à MABS est endommagé. MABS règlent hello les données sauvegardées en envoyant des blocs hello correspondant non-concordance de somme de contrôle toohello. Comme la vérification de cohérence hello est une opération qui exigent des performances, les administrateurs ont option hello de planification de la vérification de cohérence hello ou de l’exécuter automatiquement.
11. toospecify protection en ligne de sources de données hello, toobe de bases de données Sélectionnez hello protégé tooAzure et cliquez sur **suivant**.

    ![Sélectionner les sources de données](./media/backup-azure-backup-sql/pg-sqldatabases.png)
12. Les administrateurs peuvent choisir les planifications de sauvegarde et les stratégies de rétention adaptées à leurs stratégies d’entreprise.

    ![Planification de sauvegarde et rétention](./media/backup-azure-backup-sql/pg-schedule.png)

    Dans cet exemple, les sauvegardes sont effectuées une fois par jour à 12 h 00 et 20 h 00 (partie inférieure de l’écran hello)

    > [!NOTE]
    > Il s’agit d’une bonne approche en matière toohave quelques points de récupération à court terme sur disque, pour une récupération rapide. Ces points de récupération sont utilisés pour la « restauration opérationnelle ». Azure constitue un bon emplacement hors site, avec des contrats de niveau de service supérieurs et une disponibilité garantie.
    >
    >

    **Meilleures pratiques**: Assurez-vous que les sauvegardes Azure sont planifiées après l’achèvement de hello de sauvegardes de disque local à l’aide de DPM. Cela permet de hello dernière disque toobe sauvegarde copié tooAzure.

13. Choisissez la planification de stratégie de rétention hello. plus d’informations sur le fonctionne de la stratégie de rétention hello en Hello sont assurées au [utilisez Azure Backup tooreplace l’article de votre infrastructure de bande](backup-azure-backup-cloud-as-tape.md).

    ![Stratégie de rétention](./media/backup-azure-backup-sql/pg-retentionschedule.png)

    Dans cet exemple :

    * Les sauvegardes sont effectuées une fois par jour à 12 h 00 et 20 h 00 (partie inférieure de l’écran hello) et sont conservées pendant 180 jours.
    * sauvegarde Hello le samedi à 12 h 00. est conservée pendant 104 semaines
    * sauvegarde Hello dernier samedi à 12 h 00. est conservée pendant 60 mois
    * sauvegarde Hello dernier samedi de mars à 12 h 00. est conservée pendant 10 ans
14. Cliquez sur **suivant** et sélectionnez hello option appropriée pour le transfert de tooAzure de copie de sauvegarde initiale hello. Vous pouvez choisir **automatiquement sur le réseau de hello** ou **sauvegarde hors connexion**.

    * **Automatiquement sur le réseau de hello** transferts hello tooAzure de données de sauvegarde conformément à planification hello choisie pour la sauvegarde.
    * Le fonctionnement de la **Sauvegarde en mode hors connexion** est décrit à dans la section [Flux de travail de sauvegarde en mode hors connexion dans Azure Backup](backup-azure-backup-import-export.md).

    Choisissez transfert pertinentes de hello mécanisme toosend hello copie de sauvegarde initiale tooAzure et cliquez sur **suivant**.
15. Une fois que vous passez en revue les détails de la stratégie hello Bonjour **Résumé** de l’écran, cliquez sur hello **créer un groupe** flux de travail bouton toocomplete hello. Vous pouvez cliquer sur hello **fermer** bouton et le moniteur hello progression de la tâche dans l’espace de travail surveillance.

    ![Créer un groupe de Protection en cours en progression](./media/backup-azure-backup-sql/pg-summary.png)

## <a name="on-demand-backup-of-a-sql-server-database"></a>Sauvegarde à la demande d’une base de données SQL Server
Alors que les étapes précédentes hello créé une stratégie de sauvegarde, un « point de récupération » est créé uniquement lors de la première sauvegarde de hello se produit. Au lieu d’attendre tookick de planificateur hello dans, les étapes hello ci-dessous la création de hello déclencheur d’une récupération point manuellement.

1. Attendez que l’état du groupe de protection hello montre **OK** de base de données hello avant de créer le point de récupération hello.

    ![Membres du groupe de protection](./media/backup-azure-backup-sql/sqlbackup-recoverypoint.png)
2. Avec le bouton droit sur la base de données hello et sélectionnez **créer un Point de récupération**.

    ![Créer un point de récupération en ligne](./media/backup-azure-backup-sql/sqlbackup-createrp.png)
3. Choisissez **Protection en ligne** dans le menu déroulant de hello et cliquez sur **OK**. Cela lance la création de hello d’un point de récupération dans Azure.

    ![Créer un point de récupération](./media/backup-azure-backup-sql/sqlbackup-azure.png)
4. Vous pouvez afficher la progression de la tâche hello Bonjour **analyse** où vous trouverez une progression dans un espace de travail de la tâche comme une mentionnés dans la figure suivante hello hello.

    ![Console de surveillance](./media/backup-azure-backup-sql/sqlbackup-monitoring.png)

## <a name="recover-a-sql-server-database-from-azure"></a>Récupération d'une base de données SQL Server à partir d'Azure
Hello étapes suivantes sont requise toorecover une entité protégée (base de données SQL Server) à partir d’Azure.

1. Ouvrez le serveur DPM hello Console de gestion. Accédez trop**récupération** espace de travail où vous pouvez consulter les serveurs hello sauvegardée par DPM. Parcourir la base de données requis hello (dans ce ReportServer cas MSDPM2012$). Sélectionnez une durée **Restauration depuis** qui se termine par **En ligne**.

    ![Sélectionner un point de récupération](./media/backup-azure-backup-sql/sqlbackup-restorepoint.png)
2. Cliquez sur le nom de base de données hello et cliquez sur **récupérer**.

    ![Récupérer depuis Azure](./media/backup-azure-backup-sql/sqlbackup-recover.png)
3. DPM affiche les détails de hello hello du point de récupération. Cliquez sur **Suivant**. base de données toooverwrite hello, le type de récupération hello sélectionnez **instance toooriginal de restauration de SQL Server**. Cliquez sur **Suivant**.

    ![Récupérer tooOriginal emplacement](./media/backup-azure-backup-sql/sqlbackup-recoveroriginal.png)

    Dans cet exemple, DPM permet la récupération de l’instance de SQL Server tooanother hello de base de données ou un dossier de réseau tooa autonome.
4. Bonjour **les options de récupération de spécifier** écran, vous pouvez sélectionner les options de récupération hello comme toothrottle hello la bande passante utilisée par la récupération de la limitation d’utilisation de la bande passante réseau. Cliquez sur **Suivant**.
5. Bonjour **Résumé** écran, vous voyez toutes les configurations de récupération hello fournies jusqu'à présent. Cliquez sur **Restaurer**.

    Hello état de récupération s’affiche en cours de récupération de la base de données hello. Vous pouvez cliquer sur **fermer** tooclose hello Assistant et vue hello progression Bonjour **analyse** espace de travail.

    ![Initier le processus de récupération](./media/backup-azure-backup-sql/sqlbackup-recoverying.png)

    Une fois la récupération hello est terminée, la base de données de hello restauré est cohérence de l’application.

### <a name="next-steps"></a>Étapes suivantes :
•    [Sauvegarde Azure - FAQ](backup-azure-backup-faq.md)
