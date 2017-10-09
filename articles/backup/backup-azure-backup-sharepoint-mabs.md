---
title: "aaaUse Azure Backup server tooback d’un tooAzure de batterie de serveurs SharePoint | Documents Microsoft"
description: "Utilisez Azure Backup Server tooback et restaurer vos données SharePoint. Cet article fournit hello informations tooconfigure à votre batterie de serveurs SharePoint afin que les données souhaitées peuvent être stockées dans Azure. Vous pouvez restaurer des données SharePoint protégées à partir d’un disque ou d’Azure."
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: 34ba87a4-91f1-4054-a4a1-272af1e15496
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 350c1ac0f3518f400062f3b586bbe9710a79915a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-sharepoint-farm-tooazure"></a>Sauvegarder un tooAzure de batterie de serveurs SharePoint
Vous sauvegardez un SharePoint de batterie de serveurs tooMicrosoft Azure à l’aide de Microsoft Azure Backup Server (MABS) quantité Bonjour même façon que vous sauvegardez d’autres sources de données. Sauvegarde Azure garantit la souplesse de hello planification de sauvegarde toocreate des points de sauvegarde quotidiennes, hebdomadaires, mensuels ou annuels et vous offre des options de stratégie de rétention pour les différents points de sauvegarde. Il fournit également des copies de disque local hello capacité toostore pour rapides objectifs de temps de récupération (RTO) et toostore copie tooAzure économique de rétention à long terme.

## <a name="sharepoint-supported-versions-and-related-protection-scenarios"></a>Versions SharePoint prises en charge et scénarios de protection associés
Azure Backup pour DPM prend en charge hello les scénarios suivants :

| Charge de travail | Version | Déploiement de SharePoint | Protection et récupération |
| --- | --- | --- | --- | --- | --- |
| SharePoint |SharePoint 2013, SharePoint 2010, SharePoint 2007, SharePoint 3.0 |SharePoint déployé comme un serveur physique ou une machine virtuelle Hyper-V/VMware  <br> -------------- <br> SQL AlwaysOn | Options de protection de la récupération de la batterie de serveurs SharePoint : batterie de serveurs de récupération, base de données, fichier ou élément de liste à partir de points de récupération de disque.  Récupération d’une batterie de serveurs et d’une base de données à partir de points de récupération Azure. |

## <a name="before-you-start"></a>Avant de commencer
Il existe plusieurs choses tooconfirm avant de sauvegarder un tooAzure de batterie de serveurs SharePoint.

### <a name="prerequisites"></a>Composants requis
Avant de continuer, assurez-vous que vous avez [installé et préparé hello Azure Backup Server](backup-azure-microsoft-azure-backup.md) tooprotect les charges de travail.

### <a name="protection-agent"></a>Agent de protection
agent de Protection Hello doit être installé sur le serveur hello qui exécute SharePoint, hello serveurs qui exécutent SQL Server et tous les autres serveurs qui font partie de la batterie de serveurs SharePoint hello. Pour plus d’informations sur la façon tooset d’agent de protection hello, consultez [Agent de Protection le programme d’installation](https://technet.microsoft.com/library/hh758034\(v=sc.12\).aspx).  Hello une exception est que vous installez l’agent de hello uniquement sur un serveur frontal (WFE) de web unique. DPM a besoin d’agent hello sur un serveur Web frontal serveur uniquement tooserve comme point d’entrée hello pour la protection.

### <a name="sharepoint-farm"></a>Batterie de serveurs SharePoint
Pour chaque 10 millions d’éléments dans la batterie de serveurs hello, il doit exister au moins 2 Go d’espace sur le volume de hello où se trouve le dossier MABS hello. Cet espace est nécessaire pour la génération du catalogue. Pour MABS toorecover des éléments spécifiques (collections de sites, sites, listes, bibliothèques de documents, dossiers, des documents et éléments de liste), génération de catalogue crée une liste d’URL hello qui sont contenues dans chaque base de données de contenu. Vous pouvez afficher la liste de hello d’URL dans le volet de l’élément récupérable hello Bonjour **récupération** zone de la Console Administrateur de MABS de tâches.

### <a name="sql-server"></a>SQL Server
Le serveur de sauvegarde Azure exécute un compte LocalSystem. tooback des bases de données SQL Server, MABS a besoin des privilèges d’administrateur système sur ce compte pour le serveur hello qui exécute SQL Server. Définir NT AUTHORITY\SYSTEM trop*sysadmin* sur serveur hello qui exécute SQL Server que vous effectuez une sauvegarde.

Si la batterie de serveurs SharePoint hello a des bases de données SQL Server qui sont configurés avec l’alias SQL Server, installer les composants clients de SQL Server hello sur le serveur Web frontal hello MABS protéger.

### <a name="sharepoint-server"></a>SharePoint Server
Bien que les performances dépendent de nombreux facteurs, comme la taille de la batterie de serveurs SharePoint, tenez compte du fait qu’un seul serveur de sauvegarde peut protéger une batterie de serveurs SharePoint de 25 To.

### <a name="whats-not-supported"></a>Ce qui n'est pas pris en charge
* Un serveur de sauvegarde Azure qui protège une batterie de serveurs SharePoint ne protège pas les index de recherche ni les bases de données de service d’application. Vous devez tooconfigure une protection hello de ces bases de données séparément.
* Le serveur de sauvegarde Azure ne fournit aucune sauvegarde des bases de données SQL Server SharePoint hébergées sur des partages de type SOFS (Scale-out File Server).

## <a name="configure-sharepoint-protection"></a>Configuration de la protection SharePoint
Avant de pouvoir utiliser MABS tooprotect SharePoint, vous devez configurer le service enregistreur VSS de SharePoint de hello (service Enregistreur WSS) à l’aide de **ConfigureSharePoint.exe**.

Vous pouvez trouver **ConfigureSharePoint.exe** dans le dossier \bin de hello [chemin d’Installation MABS] sur le serveur web frontal de hello. Cet outil fournit l’agent de protection hello avec informations d’identification hello pour la batterie de serveurs SharePoint hello. Vous l'exécutez sur un seul serveur Web frontal (WFE). Si vous avez plusieurs serveurs WFE, n’en sélectionnez qu’un lorsque vous configurez un groupe de protection.

### <a name="tooconfigure-hello-sharepoint-vss-writer-service"></a>tooconfigure hello service enregistreur VSS de SharePoint
1. Sur le serveur Web frontal hello, à l’invite de commandes, accédez trop [emplacement d’installation MABS] \bin\
2. Entrez ConfigureSharePoint -EnableSharePointProtection
3. Entrez les informations d’identification d’administrateur de batterie de serveurs hello. Ce compte doit être membre du groupe administrateur local de hello sur le serveur Web frontal de hello. Si l’administrateur de batterie de serveurs hello n’est pas un Bonjour de grant administrateur local les autorisations sur le serveur Web frontal de hello suivantes :
   * Grant hello WSS_Admin_WPG un contrôle total toohello DPM dossier de groupe (% programme Files%\Microsoft Azure Backup\DPM).
   * Accordez la clé de Registre de DPM toohello pour groupe WSS_Admin_WPG hello accès en lecture (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager).

> [!NOTE]
> Vous devez toorerun ConfigureSharePoint.exe chaque fois qu’il y a une modification dans les informations d’identification d’administrateur de batterie de serveurs hello SharePoint.
>
>

## <a name="back-up-a-sharepoint-farm-by-using-mabs"></a>Sauvegarde d’une batterie de serveurs SharePoint à l’aide du serveur de sauvegarde Azure
Après avoir configuré MABS et hello batterie de serveurs SharePoint comme expliqué précédemment, SharePoint peut être protégé par MABS.

### <a name="tooprotect-a-sharepoint-farm"></a>tooprotect une batterie de serveurs SharePoint
1. À partir de hello **Protection** onglet Hello Console MABS administrateur, cliquez sur **nouveau**.
    ![Onglet Nouvelle protection](./media/backup-azure-backup-sharepoint/dpm-new-protection-tab.png)
2. Sur hello **sélectionner le Type de groupe de Protection** page Hello **créer un nouveau groupe de Protection** Assistant, sélectionnez **serveurs**, puis cliquez sur **suivant** .

    ![Sélectionner le type de groupe de protection](./media/backup-azure-backup-sharepoint/select-protection-group-type.png)
3. Sur hello **sélectionner les membres du groupe** écran, sélectionnez hello case à cocher pour hello SharePoint server tooprotect et cliquez sur **suivant**.

    ![Sélectionner les membres du groupe](./media/backup-azure-backup-sharepoint/select-group-members2.png)

   > [!NOTE]
   > Hello agent de protection installé, vous pouvez voir serveur hello dans l’Assistant de hello. Le serveur de sauvegarde Azure affiche également sa structure. Étant donné que vous avez exécuté ConfigureSharePoint.exe, MABS communique avec le service enregistreur VSS de SharePoint de hello et ses bases de données SQL Server correspondantes et reconnaît la structure de batterie de serveurs SharePoint hello, hello associées aux bases de données de contenu et tous les éléments correspondants.
   >
   >
4. Sur hello **sélectionner la méthode de Protection des données** , entrez le nom hello Hello **groupe de Protection**, puis sélectionnez votre choix *méthodes de protection*. Cliquez sur **Suivant**.

    ![Sélectionner la méthode de protection des données](./media/backup-azure-backup-sharepoint/select-data-protection-method1.png)

   > [!NOTE]
   > méthode de protection de disque Hello permet toomeet court objectifs de temps de récupération.
   >
   >
5. Sur hello **spécifier les objectifs à court terme** , sélectionnez votre choix **de rétention** et identifier lorsque vous souhaitez que les sauvegardes toooccur.

    ![Spécifier les objectifs à court terme](./media/backup-azure-backup-sharepoint/specify-short-term-goals2.png)

   > [!NOTE]
   > Étant donné que la récupération est le plus souvent requise pour les données qui sont moins de cinq jours, nous sélectionné d’une plage de rétention de cinq jours sur le disque et assuré que la sauvegarde hello se produit pendant les heures de production, pour cet exemple.
   >
   >
6. Vérifiez hello espace du disque pool de stockage alloué pour le groupe de protection hello, puis cliquez sur **suivant**.
7. Pour chaque groupe de protection, MABS alloue toostore d’espace disque et gérer les réplicas. À ce stade, MABS doit créer une copie de données de salutation sélectionnée. Sélectionnez comment et quand vous voulez réplica hello créé, puis cliquez sur **suivant**.

    ![Choisir la méthode de création d’un réplica](./media/backup-azure-backup-sharepoint/choose-replica-creation-method.png)

   > [!NOTE]
   > toomake assurer que le trafic réseau n’est pas terminée, sélectionnez une heure en dehors des heures de production.
   >
   >
8. MABS garantit l’intégrité des données en effectuant des vérifications de cohérence sur le réplica de hello. Deux options sont disponibles. Vous pouvez définir une cohérence de toorun la planification, ou DPM pouvez exécuter les vérifications de cohérence automatiquement sur le réplica de hello chaque fois qu’il n’est plus cohérent. Sélectionnez votre option préférée, puis cliquez sur **Suivant**.

    ![Vérification de la cohérence](./media/backup-azure-backup-sharepoint/consistency-check.png)
9. Sur hello **spécifier les données de Protection en ligne** , sélectionnez la batterie de serveurs SharePoint hello que vous souhaitez tooprotect, puis cliquez sur **suivant**.

    ![DPM SharePoint Protection1](./media/backup-azure-backup-sharepoint/select-online-protection1.png)
10. Sur hello **spécifier la planification de sauvegarde en ligne** page, sélectionnez la planification de votre choix, puis cliquez sur **suivant**.

    ![Online_backup_schedule](./media/backup-azure-backup-sharepoint/specify-online-backup-schedule.png)

    > [!NOTE]
    > MABS fournit un maximum de deux tooAzure sauvegardes quotidiennes de hello puis le point de sauvegarde de disque plus récente disponible. Sauvegarde Azure peut également contrôler hello la bande passante WAN qui peut être utilisé pour les sauvegardes de pointe et les heures creuses à l’aide de [la limitation de réseau de sauvegarde Azure](https://azure.microsoft.com/documentation/articles/backup-configure-vault/#enable-network-throttling).
    >
    >
11. En fonction de la planification de sauvegarde hello que vous avez sélectionnés sur hello **spécifier la stratégie de rétention en ligne** page, sélectionnez hello de rétention des points de sauvegarde quotidiennes, hebdomadaire, mensuels et annuels.

    ![Online_retention_policy](./media/backup-azure-backup-sharepoint/specify-online-retention.png)

    > [!NOTE]
    > Le serveur de sauvegarde Azure utilise un schéma de rétention grand-père-père-fils, dans lequel une autre stratégie de rétention peut être choisie pour différents points de sauvegarde.
    >
    >
12. Toodisk similaire, un réplica de point de référence initiale doit toobe créé dans Azure. Sélectionnez votre toocreate option recommandée un tooAzure de copie de sauvegarde initiale, puis cliquez sur **suivant**.

    ![Online_replica](./media/backup-azure-backup-sharepoint/online-replication.png)
13. Vérifiez les paramètres sélectionnés sur hello **Résumé** page, puis cliquez sur **créer un groupe**. Vous verrez un message de réussite après que le groupe de protection hello a été créé.

    ![Résumé](./media/backup-azure-backup-sharepoint/summary.png)

## <a name="restore-a-sharepoint-item-from-disk-by-using-mabs"></a>Restauration d’un élément SharePoint à partir du disque à l’aide du serveur de sauvegarde Azure
Dans l’exemple suivant de hello, hello *élément de récupération de SharePoint* a été supprimé accidentellement et doit toobe récupérée.
![MABS SharePoint Protection4](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection5.png)

1. Ouvrez hello **la Console Administrateur DPM**. Toutes les batteries de serveurs SharePoint qui sont protégées par DPM sont affichés dans hello **Protection** onglet.

    ![MABS SharePoint Protection3](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection4.png)
2. élément select hello hello toorecover toobegin **récupération** onglet.

    ![MABS SharePoint Protection5](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection6.png)
3. Vous pouvez rechercher *l’élément de récupération SharePoint* dans SharePoint à l’aide d’une recherche avec des caractères génériques dans une plage de points de récupération.

    ![MABS SharePoint Protection6](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection7.png)
4. Sélectionnez le point de récupération approprié hello hello résultats de recherche, avec le bouton droit d’élément de hello, puis sélectionnez **récupérer**.
5. Vous pouvez également parcourir les différents points de récupération et sélectionnez un toorecover de base de données ou un élément. Sélectionnez **Date > temps de récupération**, puis sélectionnez hello correct **base de données > batterie de serveurs SharePoint > point de récupération > élément**.

    ![MABS SharePoint Protection7](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection8.png)
6. Élément de hello d’avec le bouton droit et sélectionnez **récupérer** tooopen hello **Assistant récupération**. Cliquez sur **Suivant**.

    ![Vérifier la sélection à restaurer](./media/backup-azure-backup-sharepoint/review-recovery-selection.png)
7. Sélectionnez le type hello de récupération que vous souhaitez tooperform, puis cliquez sur **suivant**.

    ![Type de récupération](./media/backup-azure-backup-sharepoint/select-recovery-type.png)

   > [!NOTE]
   > Hello sélection de **récupérer toooriginal** Bonjour nous récupérons hello article toohello d’origine SharePoint site.
   >
   >
8. Sélectionnez hello **processus de récupération** que vous souhaitez toouse.

   * Sélectionnez **récupérer sans utiliser une batterie de serveurs de récupération** si la batterie de serveurs SharePoint hello n’a pas changé et est hello identique à la récupération de hello point qui est en cours de restauration.
   * Sélectionnez **récupérer à l’aide d’une batterie de serveurs de récupération** si la batterie de serveurs SharePoint hello a changé depuis la création de point de récupération hello.

     ![processus de récupération](./media/backup-azure-backup-sharepoint/recovery-process.png)
9. Fournir une zone de transit SQL Server instance emplacement toorecover hello de base de données temporairement et un partage de fichiers intermédiaires sur serveur MABS et hello élément hello de toorecover SharePoint est en cours d’exécution.

    ![Emplacement intermédiaire1](./media/backup-azure-backup-sharepoint/staging-location1.png)

    MABS joint hello contenu de base de données qui héberge hello toohello temporaire SQL Server instance d’élément SharePoint. À partir de la base de données de contenu de hello, il récupère l’élément de hello et le place sur hello sur MABS emplacement du fichier de mise en lots. Hello récupéré un élément qui se trouve sur hello emplacement intermédiaire maintenant toohello toobe exporté de besoins emplacement sur la batterie de serveurs SharePoint hello intermédiaire.

    ![Emplacement intermédiaire2](./media/backup-azure-backup-sharepoint/staging-location2.png)
10. Sélectionnez **spécifier les options de récupération**et appliquer les paramètres de sécurité toohello batterie de serveurs SharePoint ou appliquer des paramètres de sécurité hello hello du point de récupération. Cliquez sur **Suivant**.

    ![Options de récupération](./media/backup-azure-backup-sharepoint/recovery-options.png)

    > [!NOTE]
    > Vous pouvez choisir l’utilisation de la bande passante réseau toothrottle hello. Cela réduit le serveur de production toohello impact pendant les heures de production.
    >
    >
11. Passez en revue les informations de résumé hello, puis cliquez sur **récupérer** récupération toobegin du fichier de hello.

    ![Résumé de la récupération](./media/backup-azure-backup-sharepoint/recovery-summary.png)
12. Sélectionnez à présent hello **analyse** onglet Bonjour **la Console Administrateur de MABS** tooview hello **état** de la récupération de hello.

    ![État de la récupération](./media/backup-azure-backup-sharepoint/recovery-monitoring.png)

    > [!NOTE]
    > fichier de Hello est désormais restauré. Vous pouvez actualiser le fichier hello restauré toocheck hello SharePoint site.
    >
    >

## <a name="restore-a-sharepoint-database-from-azure-by-using-dpm"></a>Restauration d’une base de données SharePoint à partir d’Azure à l'aide de DPM
1. toorecover une base de données de contenu de SharePoint, parcourir les différents points de récupération (comme indiqué précédemment) et sélectionnez le point de récupération hello que vous souhaitez toorestore.

    ![MABS SharePoint Protection8](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection9.png)
2. Double-cliquez sur hello SharePoint recovery point tooshow hello SharePoint catalogue informations disponibles.

   > [!NOTE]
   > Batterie de serveurs SharePoint hello est protégé pour la rétention à long terme dans Azure, aucune information de catalogue (métadonnées) est disponible sur MABS. Par conséquent, chaque fois qu’une base de données contenu dans le temps SharePoint doit toobe récupérée, vous devez à nouveau batterie de serveurs SharePoint toocatalog hello.
   >
   >
3. Cliquez sur **Recataloguer**.

    ![MABS SharePoint Protection10](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection12.png)

    Hello **Cloud recataloguer** fenêtre État s’affiche.

    ![MABS SharePoint Protection11](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection13.png)

    Fin de catalogues, hello devient trop*réussite*. Cliquez sur **Fermer**.

    ![MABS SharePoint Protection12](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection14.png)
4. Cliquez sur l’objet SharePoint hello illustré hello MABS **récupération** onglet structure de base de données de contenu tooget hello. Élément de hello d’avec le bouton droit, puis cliquez sur **récupérer**.

    ![MABS SharePoint Protection13](./media/backup-azure-backup-sharepoint/dpm-sharepoint-protection15.png)
5. À ce stade, suivez hello [décrites précédemment dans cet article](#restore-a-sharepoint-item-from-disk-using-dpm) toorecover une base de données de contenu SharePoint à partir du disque.

## <a name="faqs"></a>FAQ
Q : puis-je récupérer un emplacement d’origine toohello de l’élément SharePoint si SharePoint est configuré à l’aide de SQL AlwaysOn (avec la protection sur disque) ?<br>
R : Oui, hello peut être récupérée toohello un site SharePoint d’origine.

Q : puis-je récupérer un emplacement d’origine de toohello de base de données de SharePoint si SharePoint est configuré à l’aide de SQL AlwaysOn ?<br>
R : étant donné que les bases de données SharePoint sont configurés dans SQL AlwaysOn, ils ne sont pas modifiables, sauf si le groupe de disponibilité hello est supprimé. Par conséquent, MABS ne peut pas restaurer un emplacement d’origine toohello de base de données. Vous pouvez récupérer une instance de SQL Server de tooanother de base de données SQL Server.

## <a name="next-steps"></a>Étapes suivantes
* Pour en savoir plus sur la protection du serveur de sauvegarde Azure pour SharePoint, consultez la [série de vidéos - Protection DPM de SharePoint](http://channel9.msdn.com/Series/Azure-Backup/Microsoft-SCDPM-Protection-of-SharePoint-1-of-2-How-to-create-a-SharePoint-Protection-Group)
