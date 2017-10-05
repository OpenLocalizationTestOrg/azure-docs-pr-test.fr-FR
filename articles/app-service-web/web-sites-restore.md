---
title: Restauration d'une application dans Azure App Service
description: "Découvrez comment restaurer votre application à partir d'une sauvegarde."
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
ms.openlocfilehash: 5fe74d992edb7028fa4a2500e427013d98ebc250
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="restore-an-app-in-azure"></a><span data-ttu-id="0cb4c-103">Restauration d'une application dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="0cb4c-103">Restore an app in Azure</span></span>
<span data-ttu-id="0cb4c-104">Cet article vous explique comment restaurer une application dans [Azure App Service](../app-service/app-service-value-prop-what-is.md) que vous avez précédemment sauvegardée (voir [Sauvegarde de votre application dans Azure](web-sites-backup.md)).</span><span class="sxs-lookup"><span data-stu-id="0cb4c-104">This article shows you how to restore an app in [Azure App Service](../app-service/app-service-value-prop-what-is.md) that you have previously backed up (see [Back up your app in Azure](web-sites-backup.md)).</span></span> <span data-ttu-id="0cb4c-105">Vous pouvez restaurer votre application avec ses bases de données liées à la demande à un état antérieur ou créer une application à partir de la sauvegarde de votre application d’origine.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-105">You can restore your app with its linked databases on-demand to a previous state, or create a new app based on one of your original app's backup.</span></span> <span data-ttu-id="0cb4c-106">Azure App Service prend en charge les bases de données suivantes pour la sauvegarde et restauration :</span><span class="sxs-lookup"><span data-stu-id="0cb4c-106">Azure App Service supports the following databases for backup and restore:</span></span>
- [<span data-ttu-id="0cb4c-107">Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="0cb4c-107">SQL Database</span></span>](https://azure.microsoft.com/en-us/services/sql-database/)
- [<span data-ttu-id="0cb4c-108">Azure Database pour MySQL (Version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="0cb4c-108">Azure Database for MySQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/mysql)
- [<span data-ttu-id="0cb4c-109">Azure Database pour PostgreSQL (Version préliminaire)</span><span class="sxs-lookup"><span data-stu-id="0cb4c-109">Azure Database for PostgreSQL (Preview)</span></span>](https://azure.microsoft.com/en-us/services/postgres)
- [<span data-ttu-id="0cb4c-110">ClearDB MySQL</span><span class="sxs-lookup"><span data-stu-id="0cb4c-110">ClearDB MySQL</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview)
- [<span data-ttu-id="0cb4c-111">MySQL dans l’application</span><span class="sxs-lookup"><span data-stu-id="0cb4c-111">MySQL in-app</span></span>](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app)

<span data-ttu-id="0cb4c-112">La restauration à partir de sauvegardes est disponible pour des applications exécutées dans les niveaux **Standard** et **Premium**.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-112">Restoring from backups is available to apps running in **Standard** and **Premium** tier.</span></span> <span data-ttu-id="0cb4c-113">Pour en savoir plus sur la mise à l’échelle de votre application, consultez [Mise à l’échelle d’une application web dans Microsoft Azure App Service](web-sites-scale.md).</span><span class="sxs-lookup"><span data-stu-id="0cb4c-113">For information about scaling up your app, see [Scale up an app in Azure](web-sites-scale.md).</span></span> <span data-ttu-id="0cb4c-114">Notez que le niveau **Premium** autorise un plus grand nombre de sauvegardes quotidiennes que le niveau **Standard**.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-114">**Premium** tier allows a greater number of daily backups to be performed than **Standard** tier.</span></span>

<a name="PreviousBackup"></a>

## <a name="restore-an-app-from-an-existing-backup"></a><span data-ttu-id="0cb4c-115">Restauration d’une application à partir d’une sauvegarde existante</span><span class="sxs-lookup"><span data-stu-id="0cb4c-115">Restore an app from an existing backup</span></span>
1. <span data-ttu-id="0cb4c-116">Dans le panneau **Paramètres** de votre application dans le portail Azure, cliquez sur **Sauvegardes** pour afficher le panneau **Sauvegardes**.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-116">On the **Settings** blade of your app in the Azure Portal, click **Backups** to display the **Backups** blade.</span></span> <span data-ttu-id="0cb4c-117">Cliquez ensuite sur **Restaurer**.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-117">Then click **Restore**.</span></span>
   
    ![Sélectionner Restaurer maintenant][ChooseRestoreNow]
2. <span data-ttu-id="0cb4c-119">Dans le panneau **Restaurer** , sélectionnez tout d'abord la source de la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-119">In the **Restore** blade, first select the backup source.</span></span>
   
    ![](./media/web-sites-restore/021ChooseSource1.png)
   
    <span data-ttu-id="0cb4c-120">L’option de **sauvegarde d’une application** vous montre toutes les sauvegardes existantes de l’application actuelle, et vous pouvez facilement sélectionner une.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-120">The **App backup** option shows you all the existing backups of the current app, and you can easily select one.</span></span>
    <span data-ttu-id="0cb4c-121">L’option de **stockage** vous permet de sélectionner un fichier ZIP de sauvegarde quelconque à partir de n’importe quel compte de stockage Azure et conteneur existants dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-121">The **Storage** option lets you select any backup ZIP file from any existing Azure Storage account and container in your subscription.</span></span>
    <span data-ttu-id="0cb4c-122">Si vous essayez de restaurer une sauvegarde d’une autre application, utilisez l’option **Stockage** .</span><span class="sxs-lookup"><span data-stu-id="0cb4c-122">If you're trying to restore a backup of another app, use the **Storage** option.</span></span>
3. <span data-ttu-id="0cb4c-123">Ensuite, spécifiez la destination de la restauration de l'application dans **Destination de restauration**.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-123">Then, specify the destination for the app restore in **Restore destination**.</span></span>
   
    ![](./media/web-sites-restore/022ChooseDestination1.png)
   
   > [!WARNING]
   > <span data-ttu-id="0cb4c-124">Si vous choisissez **Remplacer**, toutes les données existantes dans votre application actuelle seront effacées et remplacées.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-124">If you choose **Overwrite**, all existing data in your current app is erased and overwritten.</span></span> <span data-ttu-id="0cb4c-125">Avant de cliquer sur **OK**, vérifiez que c'est bien ce que vous voulez faire.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-125">Before you click **OK**, make sure that it is exactly what you want to do.</span></span>
   > 
   > 
   
    <span data-ttu-id="0cb4c-126">Vous pouvez sélectionner **Application existante** pour restaurer la sauvegarde d'une application vers une autre application dans le même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-126">You can select **Existing App** to restore the app backup to another app in the same resoure group.</span></span> <span data-ttu-id="0cb4c-127">Avant d'utiliser cette option, vous devez avoir créé une autre application dans votre groupe de ressources avec mise en miroir de la configuration de la base de données sur celle définie dans la sauvegarde de l'application.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-127">Before you use this option, you should have already created another app in your resource group with mirroring database configuration to the one defined in the app backup.</span></span> <span data-ttu-id="0cb4c-128">Vous pouvez également créer une **nouvelle** application dans laquelle restaurer votre contenu.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-128">You can also Create a **New** app to restore your content to.</span></span>

4. <span data-ttu-id="0cb4c-129">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-129">Click **OK**.</span></span>

<a name="StorageAccount"></a>

## <a name="download-or-delete-a-backup-from-a-storage-account"></a><span data-ttu-id="0cb4c-130">Télécharger ou supprimer une sauvegarde à partir d’un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="0cb4c-130">Download or delete a backup from a storage account</span></span>
1. <span data-ttu-id="0cb4c-131">Dans le panneau **Parcourir** principal du portail Azure, sélectionnez **Comptes de stockage**.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-131">From the main **Browse** blade of the Azure portal, select **Storage accounts**.</span></span> <span data-ttu-id="0cb4c-132">La liste de vos comptes de stockage existants s’affiche.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-132">A list of your existing storage accounts is displayed.</span></span>
2. <span data-ttu-id="0cb4c-133">Sélectionnez le compte de stockage contenant la sauvegarde que vous souhaitez télécharger ou supprimer. Le panneau du compte de stockage s’affiche.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-133">Select the storage account that contains the backup that you want to download or delete.The blade for the storage account is displayed.</span></span>
3. <span data-ttu-id="0cb4c-134">Dans le panneau du compte de stockage, sélectionnez le conteneur que vous souhaitez.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-134">In the storage account blade, select the container you want</span></span>
   
    ![Afficher les conteneurs][ViewContainers]
4. <span data-ttu-id="0cb4c-136">Sélectionnez le fichier de sauvegarde à télécharger ou à supprimer.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-136">Select backup file you want to download or delete.</span></span>
   
    ![ViewContainers](./media/web-sites-restore/03ViewFiles.png)
5. <span data-ttu-id="0cb4c-138">Cliquez sur **Télécharger** ou **Supprimer** selon ce que vous souhaitez faire.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-138">Click **Download** or **Delete** depending on what you want to do.</span></span>  

<a name="OperationLogs"></a>

## <a name="monitor-a-restore-operation"></a><span data-ttu-id="0cb4c-139">Surveillance d’une opération de restauration</span><span class="sxs-lookup"><span data-stu-id="0cb4c-139">Monitor a restore operation</span></span>
<span data-ttu-id="0cb4c-140">Pour afficher les détails concernant la réussite ou l’échec de l’opération de restauration de l’application, naviguez jusqu’au panneau **Journal d’activité** dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-140">To see details about the success or failure of the app restore operation, navigate to the **Activity Log** blade in the Azure portal.</span></span>  
 

<span data-ttu-id="0cb4c-141">Faites défiler la liste pour trouver l’opération de restauration souhaitée et cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-141">Scroll down to find the desired restore operation and click to select it.</span></span>

<span data-ttu-id="0cb4c-142">Le panneau de détails affiche les informations disponibles relatives à l’opération de restauration.</span><span class="sxs-lookup"><span data-stu-id="0cb4c-142">The details blade displays the available information related to the restore operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cb4c-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0cb4c-143">Next Steps</span></span>
<span data-ttu-id="0cb4c-144">Vous pouvez sauvegarder et restaurer des applications App Service à l’aide de l’API REST. Pour cela, consultez [Utilisation de REST pour sauvegarder et restaurer des applications App Service](websites-csm-backup.md).</span><span class="sxs-lookup"><span data-stu-id="0cb4c-144">You can backup and restore App Service apps using REST API (see [Use REST to back up and restore App Service apps](websites-csm-backup.md)).</span></span>


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
