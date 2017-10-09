---
title: aaaBack de votre application dans Azure
description: "Découvrez comment toocreate les sauvegardes de vos applications dans Azure App Service."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 6223b6bd-84ec-48df-943f-461d84605694
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: e41d93d322bbc48b45b28eeaa817928d83c2b9d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-your-app-in-azure"></a>Sauvegarde de votre application dans Azure
Hello sauvegarder et restaurer la fonctionnalité de [Azure App Service](../app-service/app-service-value-prop-what-is.md) vous permet de créer facilement des sauvegardes de l’application manuellement ou selon une planification. Vous pouvez restaurer l’instantané de tooa hello application d’un état antérieur par remplacement hello application ou existante restauration tooanother. 

Pour plus d’informations sur la restauration d’une application à partir d’une sauvegarde, consultez [Restauration d’une application dans Azure](web-sites-restore.md).

<a name="whatsbackedup"></a>

## <a name="what-gets-backed-up"></a>Éléments sauvegardés
Service de l’application peut effectuer des sauvegardes suivantes de hello compte de stockage Azure informations tooan et conteneur que vous avez configuré votre toouse d’application. 

* la configuration d’une application ;
* le contenu d’un fichier ;
* Base de données connectée tooyour application

Hello suivant des solutions de base de données est pris en charge avec la fonctionnalité de sauvegarde : 
   - [Base de données SQL](https://azure.microsoft.com/en-us/services/sql-database/)
   - [Azure Database pour MySQL (Version préliminaire)](https://azure.microsoft.com/en-us/services/mysql)
   - [Azure Database pour PostgreSQL (Version préliminaire)](https://azure.microsoft.com/en-us/services/postgres)
   - [ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
   - [MySQL dans l’application](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)
 

> [!NOTE]
>  Chaque sauvegarde représente une copie hors connexion complète de votre application et non une mise à jour incrémentielle.
>  

<a name="requirements"></a>

## <a name="requirements-and-restrictions"></a>Exigences et restrictions
* Hello sauvegarder et de la fonctionnalité de restauration requiert hello toobe du plan App Service Bonjour **Standard** couche ou **Premium** couche. Pour plus d’informations sur la mise à l’échelle votre toouse de plan de Service de l’application un niveau supérieur, consultez [évoluer une application dans Azure](web-sites-scale.md).  
  Le niveau **Premium** permet un plus grand nombre de sauvegardes quotidiennes que le niveau **Standard**.
* Vous avez besoin d’un compte de stockage Azure et un conteneur dans hello même abonnement que l’application hello que vous souhaitez toobackup. Pour plus d’informations sur les comptes de stockage Azure, consultez hello [liens](#moreaboutstorage) à fin hello de cet article.
* Les sauvegardes peuvent être des Go too10 du contenu d’application et de la base de données. Si la taille de la sauvegarde hello dépasse cette limite, vous obtenez une erreur.

<a name="manualbackup"></a>

## <a name="create-a-manual-backup"></a>Création d’une sauvegarde manuelle
1. Bonjour [Azure Portal](https://portal.azure.com), accédez Panneau de l’application tooyour, sélectionnez **sauvegardes**. Hello **sauvegardes** panneau s’affiche.
   
    ![Page Sauvegardes][ChooseBackupsPage]
   
   > [!NOTE]
   > Si vous voyez le message de type hello ci-dessous, cliquez dessus tooupgrade votre plan App Service avant de peut continuer avec les sauvegardes.
   > Consultez la page [Mise à l’échelle d’une application web dans Microsoft Azure App Service](web-sites-scale.md) pour plus d’informations.  
   > ![Sélection d'un compte de stockage](./media/web-sites-backup/01UpgradePlan1.png)
   > 
   > 

2. Bonjour **sauvegarde** panneau, cliquez sur **configurer**
![cliquez sur Configurer](./media/web-sites-backup/ClickConfigure1.png)
3. Bonjour **Configuration de la sauvegarde** panneau, cliquez sur **stockage : non configuré** tooconfigure un compte de stockage.
   
    ![Sélection d'un compte de stockage][ChooseStorageAccount]
4. Choisissez la destination de sauvegarde en sélectionnant un **Compte de stockage** et un **Conteneur**. compte de stockage Hello doit appartenir toohello même abonnement que hello application tooback des. Si vous le souhaitez, vous pouvez créer un compte de stockage ou un nouveau conteneur dans les panneaux respectifs hello. Quand vous avez terminé, cliquez sur **Sélectionner**.
   
    ![Sélection d'un compte de stockage](./media/web-sites-backup/02ChooseStorageAccount1-1.png)
5. Bonjour **Configuration de la sauvegarde** panneau qui reste ouvert, vous pouvez configurer **sauvegarde de base de données**, puis sélectionnez les bases de données hello souhaité tooinclude dans les sauvegardes hello (base de données SQL ou MySQL), puis cliquez sur **OK**.  
   
    ![Sélection d'un compte de stockage](./media/web-sites-backup/03ConfigureDatabase1.png)
   
   > [!NOTE]
   > Pour une base de données tooappear dans cette liste, sa chaîne de connexion doit exister dans hello **les chaînes de connexion** section Hello **paramètres de l’Application** panneau pour votre application.
   > 
   > 
6. Bonjour **Configuration de la sauvegarde** panneau, cliquez sur **enregistrer**.    
7. Bonjour **sauvegardes** panneau, cliquez sur **sauvegarde**.
   
    ![Bouton Backup Now][BackUpNow]
   
    Vous voyez un message de progression pendant le processus de sauvegarde hello.

Une fois que le compte de stockage hello et un conteneur est configuré, vous pouvez lancer une sauvegarde manuelle à tout moment.  

<a name="automatedbackups"></a>

## <a name="configure-automated-backups"></a>Configuration de sauvegardes automatisées
1. Bonjour **Configuration de la sauvegarde** panneau, définissez **planifiée sauvegarde** trop**sur**. 
   
    ![Sélection d'un compte de stockage](./media/web-sites-backup/05ScheduleBackup1.png)
2. Planification de sauvegarde seront afficheront les options définie **planifiée sauvegarde** trop**sur**, configurez la planification de sauvegarde hello selon vos besoins, puis cliquez sur **OK**.
   
    ![Activation des sauvegardes automatisées][SetAutomatedBackupOn]

<a name="partialbackups"></a>

## <a name="configure-partial-backups"></a>Configurer des sauvegardes partielles
Parfois, vous ne souhaitez toobackup tous les éléments sur votre application. Voici quelques exemples :

* Vous [configurez une sauvegarde hebdomadaire](web-sites-backup.md#configure-automated-backups) de votre application qui contient du contenu statique qui ne change jamais, comme des anciens billets de blog ou des images.
* Votre application dispose de plus de 10 Go de contenu (ce qui est la quantité maximale de hello que vous pouvez sauvegarder à la fois).
* Vous ne souhaitez pas les fichiers journaux toobackup hello.

Sauvegardes partielles vous permet de choisir exactement les fichiers auxquels vous souhaitez toobackup.

### <a name="exclude-files-from-your-backup"></a>Exclusion de fichiers de votre sauvegarde
Supposons que vous disposez d’une application qui contient les fichiers journaux et des images statiques qui ont été sauvegarde qu’une seule fois et ne vont pas toochange. Dans ce cas, vous pouvez exclure ces fichiers et dossiers du stockage lors de vos sauvegardes futures. tooexclude fichiers et dossiers à partir des sauvegardes, créer un `_backup.filter` fichier Bonjour `D:\home\site\wwwroot` dossier de votre application. Spécifiez la liste hello des fichiers et dossiers que vous souhaitez tooexclude dans ce fichier. 

Un tooaccess facilement vos fichiers est toouse Kudu. Cliquez sur **outils avancés -> accédez** définition pour votre tooaccess d’application web Kudu.

![Utilisation du portail par Kudu][kudu-portal]

Identifiez les dossiers hello que vous souhaitez tooexclude à partir de vos sauvegardes.  Par exemple, vous souhaitez toofilter dossier de mise en surbrillance de hello et fichiers de sortie.

![Dossier images][ImagesFolder]

Créez un fichier appelé `_backup.filter` et placer la liste hello ci-dessus dans le fichier de hello, mais supprimer `D:\home`. Listez un répertoire ou fichier par ligne. Par conséquent, le contenu du fichier de hello hello doit être :
 ```bash
    \site\wwwroot\Images\brand.png
    \site\wwwroot\Images\2014
    \site\wwwroot\Images\2013
```

Télécharger `_backup.filter` toohello de fichiers `D:\home\site\wwwroot\` répertoire de votre site à l’aide de [ftp](web-sites-deploy.md#ftp) ou toute autre méthode. Si vous le souhaitez, vous pouvez créer le fichier hello directement à l’aide de Kudu `DebugConsole` et insérez le contenu hello il.

Exécution de sauvegardes hello la même façon que vous feriez normalement, [manuellement](#create-a-manual-backup) ou [automatiquement](#configure-automated-backups). Maintenant, tous les fichiers et dossiers qui sont spécifiés dans `_backup.filter` est exclu de hello futures sauvegardes planifiées ou lancées manuellement. 

> [!NOTE]
> Vous restaurez les sauvegardes partielles de votre hello site manière [restaurer une sauvegarde régulière](web-sites-restore.md). processus de restauration Hello hello qu’il faut.
> 
> Lorsqu’une sauvegarde complète est restaurée, tout le contenu sur le site de hello est remplacé par tout ce qui est dans la sauvegarde de hello. Si un fichier se trouve sur le site de hello, mais pas dans la sauvegarde de hello, il est supprimé. Mais lors de la restauration d’une sauvegarde partielle, tout contenu qui se trouve dans un des répertoires de hello sur liste noire ou n’importe quel fichier sur liste noire, demeure en l’état.
> 


<a name="aboutbackups"></a>

## <a name="how-backups-are-stored"></a>Mode de stockage des sauvegardes
Après avoir effectué une ou plusieurs sauvegardes de votre application, les sauvegardes hello sont visibles sur hello **conteneurs** Panneau de votre compte de stockage et de votre application. Dans le compte de stockage hello, chaque sauvegarde se compose d’un`.zip` fichier qui contient les données de sauvegarde hello et un `.xml` fichier qui contient un manifeste de hello `.zip` le contenu du fichier. Vous pouvez décompresser et parcourir ces fichiers si vous souhaitez tooaccess vos sauvegardes sans réellement effectuer une restauration d’une application.

sauvegarde de base de données Hello pour une application hello est stocké dans la racine hello 100Ko fichier. Pour une base de données SQL, il s'agit d'un fichier BACPAC (pas d'extension de fichier) qui peut être importé. en fonction de base de données SQL toocreate de hello exportation de BACPAC, consultez [importer un fichier BACPAC de tooCreate une base de données utilisateur](http://technet.microsoft.com/library/hh710052.aspx).

> [!WARNING]
> Modification des fichiers hello dans votre **websitebackups** conteneur peut entraîner des toobecome de sauvegarde hello non valide et par conséquent non récupérable.
> 
> 

<a name="nextsteps"></a>

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur la restauration d’une application à partir d’une sauvegarde, consultez [Restauration d’une application dans Azure](web-sites-restore.md). Vous pouvez également sauvegarder et restaurer des applications de Service d’applications à l’aide des API REST (voir [utilisation reste toobackup et la restauration d’applications de Service d’applications](websites-csm-backup.md)).


<!-- IMAGES -->
[ChooseBackupsPage]: ./media/web-sites-backup/01ChooseBackupsPage1.png
[ChooseStorageAccount]: ./media/web-sites-backup/02ChooseStorageAccount-1.png
[IncludedDatabases]: ./media/web-sites-backup/03IncludedDatabases.png
[BackUpNow]: ./media/web-sites-backup/04BackUpNow1.png
[BackupProgress]: ./media/web-sites-backup/05BackupProgress.png
[SetAutomatedBackupOn]: ./media/web-sites-backup/06SetAutomatedBackupOn1.png
[Frequency]: ./media/web-sites-backup/07Frequency.png
[StartDate]: ./media/web-sites-backup/08StartDate.png
[StartTime]: ./media/web-sites-backup/09StartTime.png
[SaveIcon]: ./media/web-sites-backup/10SaveIcon.png
[ImagesFolder]: ./media/web-sites-backup/11Images.png
[LogsFolder]: ./media/web-sites-backup/12Logs.png
[GhostUpgradeWarning]: ./media/web-sites-backup/13GhostUpgradeWarning.png
[kudu-portal]:./media/web-sites-backup/kudu-portal.PNG

