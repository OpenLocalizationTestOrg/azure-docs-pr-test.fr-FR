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
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="65d1e-103">Restauration d'une application dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="65d1e-103">Restore an app in Azure</span></span>
<span data-ttu-id="65d1e-104">Cet article vous montre comment toorestore une application dans [Azure App Service](../app-service/app-service-value-prop-what-is.md) que vous avez précédemment sauvegardé (voir [sauvegarder votre application dans Azure](web-sites-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="65d1e-104">This article shows you how toorestore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="65d1e-105">Vous pouvez restaurer votre application avec son état précédent de bases de données liées à la demande tooa, ou créer une application à partir de la sauvegarde d’origine de votre application.</span><span class="sxs-lookup"><span data-stu-id="65d1e-105">You can restore your app with its linked databases on-demand tooa previous state, or create a new app based on one of your original app's backup.</span></span> <span data-ttu-id="65d1e-106">Service d’applications Azure prend en charge hello suivant des bases de données pour la sauvegarde et restauration :</span><span class="sxs-lookup"><span data-stu-id="65d1e-106">Azure App Service supports hello following databases for backup and restore:</span></span>
- [<span data-ttu-id="65d1e-107">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="65d1e-107">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
- [<span data-ttu-id="65d1e-108">Azure Database pour MySQL (Version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="65d1e-108">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
- [<span data-ttu-id="65d1e-109">Azure Database pour PostgreSQL (Version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="65d1e-109">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
- [<span data-ttu-id="65d1e-110">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="65d1e-110">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [<span data-ttu-id="65d1e-111">MySQL dans l’application</span><span class="sxs-lookup"><span data-stu-id="65d1e-111">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

<span data-ttu-id="65d1e-112">Restauration à partir de sauvegardes est tooapps disponibles en cours d’exécution **Standard** et **Premium** couche.</span><span class="sxs-lookup"><span data-stu-id="65d1e-112">Restoring from backups is available tooapps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="65d1e-113">Pour en savoir plus sur la mise à l’échelle de votre application, consultez [Mise à l’échelle d’une application web dans Microsoft Azure App Service](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="65d1e-113">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="65d1e-114">**Premium** niveau autorise un plus grand nombre de quotidienne toobe de sauvegardes effectuée à **Standard** couche.</span><span class="sxs-lookup"><span data-stu-id="65d1e-114">**Premium** tier allows a greater number of daily backups toobe performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="65d1e-115">Restauration d’une application à partir d’une sauvegarde existante</span><span class="sxs-lookup"><span data-stu-id="65d1e-115">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="65d1e-116">Sur hello **paramètres** Panneau de votre application Bonjour portail Azure, cliquez sur **sauvegardes** toodisplay hello **sauvegardes** panneau.</span><span class="sxs-lookup"><span data-stu-id="65d1e-116">On hello **Settings** blade of your app in hello Azure Portal, click **Backups** toodisplay hello **Backups** blade.</span></span> <span data-ttu-id="65d1e-117">Cliquez ensuite sur **Restaurer**.</span><span class="sxs-lookup"><span data-stu-id="65d1e-117">Then click **Restore**.</span></span>
   
    ![Sélectionner Restaurer maintenant][ChooseRestoreNow]
2. <span data-ttu-id="65d1e-119">Bonjour **restaurer** panneau, la première source de sauvegarde Sélectionnez hello.</span><span class="sxs-lookup"><span data-stu-id="65d1e-119">In hello **Restore** blade, first select hello backup source.</span></span>
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    <span data-ttu-id="65d1e-120">Hello **sauvegarde de l’application** option vous montre toutes les hello sauvegardes existantes de l’application actuelle hello et vous pouvez facilement sélectionner un.</span><span class="sxs-lookup"><span data-stu-id="65d1e-120">hello **App backup** option shows you all hello existing backups of hello current app, and you can easily select one.</span></span>
    <span data-ttu-id="65d1e-121">Hello **stockage** option vous permet de sélectionner n’importe quel fichier ZIP de sauvegarde à partir de n’importe quel compte de stockage Azure et un conteneur dans votre abonnement existant.</span><span class="sxs-lookup"><span data-stu-id="65d1e-121">hello **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="65d1e-122">Si vous essayez de toorestore une sauvegarde d’une autre application, utilisez hello **stockage** option.</span><span class="sxs-lookup"><span data-stu-id="65d1e-122">If you're trying toorestore a backup of another app, use hello **Storage** option.</span></span>
3. <span data-ttu-id="65d1e-123">Ensuite, spécifiez la destination hello pour la restauration d’une application hello dans **destination de restauration**.</span><span class="sxs-lookup"><span data-stu-id="65d1e-123">Then, specify hello destination for hello app restore in **Restore destination**.</span></span>
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > <span data-ttu-id="65d1e-124">Si vous choisissez **Remplacer**, toutes les données existantes dans votre application actuelle seront effacées et remplacées.</span><span class="sxs-lookup"><span data-stu-id="65d1e-124">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span></span> <span data-ttu-id="65d1e-125">Avant de cliquer sur **OK**, assurez-vous qu’il s’agit exactement ce que vous souhaitez toodo.</span><span class="sxs-lookup"><span data-stu-id="65d1e-125">Before you click **OK**, make sure that it is exactly what you want toodo.</span></span>
   > 
   > 
   
    <span data-ttu-id="65d1e-126">Vous pouvez sélectionner **application existante** application hello toorestore tooanother sauvegarde d’applications Bonjour même groupe de ressource.</span><span class="sxs-lookup"><span data-stu-id="65d1e-126">You can select **Existing App** toorestore hello app backup tooanother app in hello same resoure group.</span></span> <span data-ttu-id="65d1e-127">Avant d’utiliser cette option, vous devez avoir déjà créé une autre application dans votre groupe de ressources avec mise en miroir toohello de configuration de base de données défini dans la sauvegarde d’application hello.</span><span class="sxs-lookup"><span data-stu-id="65d1e-127">Before you use this option, you should have already created another app in your resource group with mirroring database configuration toohello one defined in hello app backup.</span></span> <span data-ttu-id="65d1e-128">Vous pouvez également créer un **nouveau** application toorestore votre contenu.</span><span class="sxs-lookup"><span data-stu-id="65d1e-128">You can also Create a **New** app toorestore your content to.</span></span>

4. <span data-ttu-id="65d1e-129">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="65d1e-129">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="65d1e-130">Télécharger ou supprimer une sauvegarde à partir d’un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="65d1e-130">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="65d1e-131">À partir de hello principal **Parcourir** Panneau de hello portail Azure, sélectionnez **comptes de stockage**.</span><span class="sxs-lookup"><span data-stu-id="65d1e-131">From hello main **Browse** blade of hello Azure portal, select **Storage accounts**.</span></span> <span data-ttu-id="65d1e-132">La liste de vos comptes de stockage existants s’affiche.</span><span class="sxs-lookup"><span data-stu-id="65d1e-132">A list of your existing storage accounts is displayed.</span></span>
2. <span data-ttu-id="65d1e-133">Sélectionnez le compte de stockage hello contenant hello sauvegarde toodownload ou delete.hello panneau hello compte de stockage s’affiche.</span><span class="sxs-lookup"><span data-stu-id="65d1e-133">Select hello storage account that contains hello backup that you want toodownload or delete.hello blade for hello storage account is displayed.</span></span>
3. <span data-ttu-id="65d1e-134">Dans le panneau de compte de stockage hello, sélectionnez le conteneur hello</span><span class="sxs-lookup"><span data-stu-id="65d1e-134">In hello storage account blade, select hello container you want</span></span>
   
    ![Afficher les conteneurs][ViewContainers]
4. <span data-ttu-id="65d1e-136">Sélectionnez le fichier de sauvegarde toodownload ou supprimer.</span><span class="sxs-lookup"><span data-stu-id="65d1e-136">Select backup file you want toodownload or delete.</span></span>
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="65d1e-138">Cliquez sur **télécharger** ou **supprimer** selon ce que vous souhaitez toodo.</span><span class="sxs-lookup"><span data-stu-id="65d1e-138">Click **Download** or **Delete** depending on what you want toodo.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="65d1e-139">Surveillance d’une opération de restauration</span><span class="sxs-lookup"><span data-stu-id="65d1e-139">Monitor a restore operation</span></span>
<span data-ttu-id="65d1e-140">toosee plus d’informations sur la réussite de hello ou l’échec de restauration de l’application hello, accédez à toohello **le journal d’activité** panneau Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="65d1e-140">toosee details about hello success or failure of hello app restore operation, navigate toohello **Activity Log** blade in hello Azure portal.</span></span>  
 

<span data-ttu-id="65d1e-141">Faites défiler toofind hello souhaité restauration opération et cliquez sur tooselect il.</span><span class="sxs-lookup"><span data-stu-id="65d1e-141">Scroll down toofind hello desired restore operation and click tooselect it.</span></span>

<span data-ttu-id="65d1e-142">Hello détails panneau affiche hello disponibles les informations relatives toohello restauration.</span><span class="sxs-lookup"><span data-stu-id="65d1e-142">hello details blade displays hello available information related toohello restore operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65d1e-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="65d1e-143">Next Steps</span></span>
<span data-ttu-id="65d1e-144">Vous pouvez sauvegarder et restaurer des applications de Service d’applications à l’aide des API REST (voir [tooback du reste de l’utilisation et la restauration des applications de Service d’applications](websites-csm-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="65d1e-144">You can backup and restore App Service apps using REST API (see [Use REST tooback up and restore App Service apps](websites-csm-backup.md)).</span></span>


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
