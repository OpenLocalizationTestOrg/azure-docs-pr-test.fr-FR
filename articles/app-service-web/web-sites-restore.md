---
title: aaaRestore une application dans Azure
description: "Découvrez comment toorestore votre application à partir d’une sauvegarde."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 4444dbf7-363c-47e2-b24a-dbd45cb08491
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: 4b54029a9197064f990f29a3c4558c8322668714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-app-in-azure"></a>Restauration d'une application dans Azure App Service
Cet article vous montre comment toorestore une application dans [Azure App Service](../app-service/app-service-value-prop-what-is.md) que vous avez précédemment sauvegardé (voir [sauvegarder votre application dans Azure](web-sites-backup.md)). Vous pouvez restaurer votre application avec son état précédent de bases de données liées à la demande tooa, ou créer une application à partir de la sauvegarde d’origine de votre application. Service d’applications Azure prend en charge hello suivant des bases de données pour la sauvegarde et restauration :
- [Base de données SQL](https://azure.microsoft.com/en-us/services/sql-database/)
- [Azure Database pour MySQL (Version préliminaire)](https://azure.microsoft.com/en-us/services/mysql)
- [Azure Database pour PostgreSQL (Version préliminaire)](https://azure.microsoft.com/en-us/services/postgres)
- [ClearDB MySQL](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [MySQL dans l’application](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

Restauration à partir de sauvegardes est tooapps disponibles en cours d’exécution **Standard** et **Premium** couche. Pour en savoir plus sur la mise à l’échelle de votre application, consultez [Mise à l’échelle d’une application web dans Microsoft Azure App Service](web-sites-scale.md). **Premium** niveau autorise un plus grand nombre de quotidienne toobe de sauvegardes effectuée à **Standard** couche.

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a>Restauration d’une application à partir d’une sauvegarde existante
1. Sur hello **paramètres** Panneau de votre application Bonjour portail Azure, cliquez sur **sauvegardes** toodisplay hello **sauvegardes** panneau. Cliquez ensuite sur **Restaurer**.
   
    ![Sélectionner Restaurer maintenant][ChooseRestoreNow]
2. Bonjour **restaurer** panneau, la première source de sauvegarde Sélectionnez hello.
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    Hello **sauvegarde de l’application** option vous montre toutes les hello sauvegardes existantes de l’application actuelle hello et vous pouvez facilement sélectionner un.
    Hello **stockage** option vous permet de sélectionner n’importe quel fichier ZIP de sauvegarde à partir de n’importe quel compte de stockage Azure et un conteneur dans votre abonnement existant.
    Si vous essayez de toorestore une sauvegarde d’une autre application, utilisez hello **stockage** option.
3. Ensuite, spécifiez la destination hello pour la restauration d’une application hello dans **destination de restauration**.
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > Si vous choisissez **Remplacer**, toutes les données existantes dans votre application actuelle seront effacées et remplacées. Avant de cliquer sur **OK**, assurez-vous qu’il s’agit exactement ce que vous souhaitez toodo.
   > 
   > 
   
    Vous pouvez sélectionner **application existante** application hello toorestore tooanother sauvegarde d’applications Bonjour même groupe de ressource. Avant d’utiliser cette option, vous devez avoir déjà créé une autre application dans votre groupe de ressources avec mise en miroir toohello de configuration de base de données défini dans la sauvegarde d’application hello. Vous pouvez également créer un **nouveau** application toorestore votre contenu.

4. Cliquez sur **OK**.

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a>Télécharger ou supprimer une sauvegarde à partir d’un compte de stockage
1. À partir de hello principal **Parcourir** Panneau de hello portail Azure, sélectionnez **comptes de stockage**. La liste de vos comptes de stockage existants s’affiche.
2. Sélectionnez le compte de stockage hello contenant hello sauvegarde toodownload ou delete.hello panneau hello compte de stockage s’affiche.
3. Dans le panneau de compte de stockage hello, sélectionnez le conteneur hello
   
    ![Afficher les conteneurs][ViewContainers]
4. Sélectionnez le fichier de sauvegarde toodownload ou supprimer.
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. Cliquez sur **télécharger** ou **supprimer** selon ce que vous souhaitez toodo.  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a>Surveillance d’une opération de restauration
toosee plus d’informations sur la réussite de hello ou l’échec de restauration de l’application hello, accédez à toohello **le journal d’activité** panneau Bonjour portail Azure.  
 

Faites défiler toofind hello souhaité restauration opération et cliquez sur tooselect il.

Hello détails panneau affiche hello disponibles les informations relatives toohello restauration.

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez sauvegarder et restaurer des applications de Service d’applications à l’aide des API REST (voir [tooback du reste de l’utilisation et la restauration des applications de Service d’applications](websites-csm-backup.md)).


<!-- IMAGES -->
[ChooseRestoreNow]: ./media/web-sites-restore/02ChooseRestoreNow1.png
[ViewContainers]: ./media/web-sites-restore/03ViewContainers.png
[StorageAccountFile]: ./media/web-sites-restore/02StorageAccountFile.png
[BrowseCloudStorage]: ./media/web-sites-restore/03BrowseCloudStorage.png
[StorageAccountFileSelected]: ./media/web-sites-restore/04StorageAccountFileSelected.png
[ChooseRestoreSettings]: ./media/web-sites-restore/05ChooseRestoreSettings.png
[ChooseDBServer]: ./media/web-sites-restore/06ChooseDBServer.png
[RestoreToNewSQLDB]: ./media/web-sites-restore/07RestoreToNewSQLDB.png
[NewSQLDBConfig]: ./media/web-sites-restore/08NewSQLDBConfig.png
[RestoredContosoWebSite]: ./media/web-sites-restore/09RestoredContosoWebSite.png
[DashboardOperationLogsLink]: ./media/web-sites-restore/10DashboardOperationLogsLink.png
[ManagementServicesOperationLogsList]: ./media/web-sites-restore/11ManagementServicesOperationLogsList.png
[DetailsButton]: ./media/web-sites-restore/12DetailsButton.png
[OperationDetails]: ./media/web-sites-restore/13OperationDetails.png
