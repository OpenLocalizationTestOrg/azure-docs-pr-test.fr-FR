---
title: "aaaUse PowerShell tooback et la restauration des applications de Service d’applications"
description: "Découvrez comment toouse PowerShell tooback et restaurer une application dans Azure App Service"
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: 7ea8661e-aefb-4823-9626-6bff980cdebf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: 4042166f6c650841926f010056d6c80ab2de57e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooback-up-and-restore-app-service-apps"></a><span data-ttu-id="fa8b6-103">Utilisez PowerShell tooback et restaurer des applications de Service d’applications</span><span class="sxs-lookup"><span data-stu-id="fa8b6-103">Use PowerShell tooback up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fa8b6-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa8b6-104">PowerShell</span></span>](app-service-powershell-backup.md)
> * [<span data-ttu-id="fa8b6-105">API REST</span><span class="sxs-lookup"><span data-stu-id="fa8b6-105">REST API</span></span>](../app-service-web/websites-csm-backup.md)
> 
> 

<span data-ttu-id="fa8b6-106">Découvrez comment toouse Azure PowerShell tooback et de restauration [des applications de Service d’applications](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="fa8b6-106">Learn how toouse Azure PowerShell tooback up and restore [App Service apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="fa8b6-107">Pour plus d’informations sur les sauvegardes d’applications web, et notamment en connaître les exigences et restrictions, consultez [Sauvegarder une application web dans Azure App Service](../app-service-web/web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="fa8b6-107">For more information about web app backups, including requirements and restrictions, see [Back up a web app in Azure App Service](../app-service-web/web-sites-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa8b6-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fa8b6-108">Prerequisites</span></span>
<span data-ttu-id="fa8b6-109">toouse PowerShell toomanage vos sauvegardes de l’application, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="fa8b6-109">toouse PowerShell toomanage your app backups, you need hello following:</span></span>

* <span data-ttu-id="fa8b6-110">**Une URL SAS** qui permet de lire et conteneur de stockage Azure tooan un accès en écriture.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-110">**A SAS URL** that allows read and write access tooan Azure Storage container.</span></span> <span data-ttu-id="fa8b6-111">Consultez [modèle de présentation hello SAP](../storage/common/storage-dotnet-shared-access-signature-part-1.md) pour une explication de l’URL de SAP.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-111">See [Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for an explanation of SAS URLs.</span></span> <span data-ttu-id="fa8b6-112">Consultez la page [Utilisation d’Azure PowerShell avec Azure Storage](../storage/common/storage-powershell-guide-full.md) pour obtenir des exemples de gestion d'Azure Storage à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-112">See [Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) for examples of managing Azure Storage using PowerShell.</span></span>
* <span data-ttu-id="fa8b6-113">**Une chaîne de connexion de base de données** si vous souhaitez tooback une base de données en même temps que votre application web.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-113">**A database connection string** if you want tooback up a database along with your web app.</span></span>

### <a name="how-toogenerate-a-sas-url-toouse-with-hello-web-app-backup-cmdlets"></a><span data-ttu-id="fa8b6-114">Comment toogenerate un toouse URL de SAP à l’application web de hello applets de commande de sauvegarde</span><span class="sxs-lookup"><span data-stu-id="fa8b6-114">How toogenerate a SAS URL toouse with hello web app backup cmdlets</span></span>
<span data-ttu-id="fa8b6-115">Une URL SAP peut être générée avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-115">A SAS URL can be generated with PowerShell.</span></span> <span data-ttu-id="fa8b6-116">Voici un exemple de la façon dont un qui peut être utilisé avec les applets de commande hello toogenerate abordé dans cet article.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-116">Here is an example of how toogenerate one that can be used with hello cmdlets discussed in this article.</span></span>

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure tooselect hello appropriate key. Here we select hello first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a><span data-ttu-id="fa8b6-117">Installer Azure PowerShell 1.3.2 ou versions ultérieures</span><span class="sxs-lookup"><span data-stu-id="fa8b6-117">Install Azure PowerShell 1.3.2 or greater</span></span>
<span data-ttu-id="fa8b6-118">Pour obtenir des instructions sur l’installation et l’utilisation d’Azure PowerShell, consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="fa8b6-118">See [Using Azure PowerShell with Azure Resource Manager](/powershell/azure/overview) for instructions on installing and using Azure PowerShell.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="fa8b6-119">Création d'une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="fa8b6-119">Create a backup</span></span>
<span data-ttu-id="fa8b6-120">Utilisez toocreate d’applet de commande hello AzureRmWebAppBackup de nouveau une sauvegarde d’une application web.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-120">Use hello New-AzureRmWebAppBackup cmdlet toocreate a backup of a web app.</span></span>

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

<span data-ttu-id="fa8b6-121">Vous obtenez une sauvegarde avec un nom généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-121">This creates a backup with an automatically generated name.</span></span> <span data-ttu-id="fa8b6-122">Si vous souhaitez que tooprovide un nom pour votre sauvegarde, utiliser le paramètre facultatif de Nom_sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-122">If you would like tooprovide a name for your backup, use hello BackupName optional parameter.</span></span>

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

<span data-ttu-id="fa8b6-123">tooinclude une base de données dans la sauvegarde de hello, tout d’abord créer un paramètre de sauvegarde de base de données à l’aide d’applet de commande New-AzureRmWebAppDatabaseBackupSetting hello, puis fournissez ce paramètre Bonjour bases de données de l’applet de commande New-AzureRmWebAppBackup hello.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-123">tooinclude a database in hello backup, first create a database backup setting using hello New-AzureRmWebAppDatabaseBackupSetting cmdlet, then supply that setting in hello Databases parameter of hello New-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="fa8b6-124">paramètre de bases de données Hello accepte un tableau de paramètres de base de données, ce qui vous tooback plus d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-124">hello Databases parameter accepts an array of database settings, allowing you tooback up more than one database.</span></span>

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a><span data-ttu-id="fa8b6-125">Obtenir des sauvegardes</span><span class="sxs-lookup"><span data-stu-id="fa8b6-125">Get backups</span></span>
<span data-ttu-id="fa8b6-126">applet de commande Get-AzureRmWebAppBackupList Hello retourne un tableau de toutes les sauvegardes pour une application web.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-126">hello Get-AzureRmWebAppBackupList cmdlet returns an array of all backups for a web app.</span></span> <span data-ttu-id="fa8b6-127">Vous devez fournir le nom hello de hello web app et son groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-127">You must supply hello name of hello web app and its resource group.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

<span data-ttu-id="fa8b6-128">tooget une sauvegarde spécifique, utilisez l’applet de commande Get-AzureRmWebAppBackup de hello.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-128">tooget a specific backup, use hello Get-AzureRmWebAppBackup cmdlet.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

<span data-ttu-id="fa8b6-129">Vous pouvez également diriger un objet d’application web dans une des applets de commande de gestion de sauvegarde hello pour des raisons pratiques.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-129">You can also pipe a web app object into any of hello backup management cmdlets for convenience.</span></span>

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a><span data-ttu-id="fa8b6-130">Planification de sauvegardes automatiques</span><span class="sxs-lookup"><span data-stu-id="fa8b6-130">Schedule automatic backups</span></span>
<span data-ttu-id="fa8b6-131">Vous pouvez planifier des sauvegardes toohappen automatiquement à un intervalle spécifié.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-131">You can schedule backups toohappen automatically at a specified interval.</span></span> <span data-ttu-id="fa8b6-132">tooconfigure une planification de sauvegarde, utilisez l’applet de commande de hello AzureRmWebAppBackupConfiguration de modification.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-132">tooconfigure a backup schedule, use hello Edit-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="fa8b6-133">Cette applet de commande accepte plusieurs paramètres :</span><span class="sxs-lookup"><span data-stu-id="fa8b6-133">This cmdlet takes several parameters:</span></span>

* <span data-ttu-id="fa8b6-134">**Nom** hello - nom de l’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-134">**Name** - hello name of hello web app.</span></span>
* <span data-ttu-id="fa8b6-135">**ResourceGroupName** hello - nom de l’application web contenant hello d’hello ressource groupe.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-135">**ResourceGroupName** - hello name of hello resource group containing hello web app.</span></span>
* <span data-ttu-id="fa8b6-136">**Slot** : facultatif.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-136">**Slot** - Optional.</span></span> <span data-ttu-id="fa8b6-137">nom de Hello de l’emplacement d’application web hello.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-137">hello name of hello web app slot.</span></span>
* <span data-ttu-id="fa8b6-138">**StorageAccountUrl** -hello URL de SAP de conteneur de stockage Azure hello utilisé des sauvegardes toostore hello.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-138">**StorageAccountUrl** - hello SAS URL for hello Azure Storage container used toostore hello backups.</span></span>
* <span data-ttu-id="fa8b6-139">**FrequencyInterval** -valeur numérique pour la fréquence à laquelle hello les sauvegardes doivent être effectuées.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-139">**FrequencyInterval** - Numeric value for how often hello backups should be made.</span></span> <span data-ttu-id="fa8b6-140">Cette valeur doit être un entier positif.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-140">Must be a positive integer.</span></span>
* <span data-ttu-id="fa8b6-141">**FrequencyUnit** -unité de temps pour la fréquence à laquelle hello les sauvegardes doivent être effectuées.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-141">**FrequencyUnit** - Unit of time for how often hello backups should be made.</span></span> <span data-ttu-id="fa8b6-142">Peut être exprimée en heures et en jours.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-142">Options are Hour and Day.</span></span>
* <span data-ttu-id="fa8b6-143">**RetentionPeriodInDays** - le nombre de jours de sauvegardes automatiques hello doivent être enregistrés avant d’être automatiquement supprimés.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-143">**RetentionPeriodInDays** - How many days hello automatic backups should be saved before being automatically deleted.</span></span>
* <span data-ttu-id="fa8b6-144">**StartTime** : facultatif.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-144">**StartTime** - Optional.</span></span> <span data-ttu-id="fa8b6-145">heure de Hello lorsque les sauvegardes automatiques hello doivent commencer.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-145">hello time when hello automatic backups should begin.</span></span> <span data-ttu-id="fa8b6-146">Les sauvegardes débutent immédiatement si la valeur est null.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-146">Backups begin immediately if this is null.</span></span> <span data-ttu-id="fa8b6-147">Doit être une valeur DateTime.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-147">Must be a DateTime.</span></span>
* <span data-ttu-id="fa8b6-148">**Databases** : facultatif.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-148">**Databases** - Optional.</span></span> <span data-ttu-id="fa8b6-149">Tableau de DatabaseBackupSettings pour toobackup de bases de données hello.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-149">An array of DatabaseBackupSettings for hello databases toobackup.</span></span>
* <span data-ttu-id="fa8b6-150">**KeepAtLeastOneBackup** - paramètre à bascule facultatif.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-150">**KeepAtLeastOneBackup** - Optional switched parameter.</span></span> <span data-ttu-id="fa8b6-151">Approvisionnement cela si une sauvegarde doit toujours être conservée dans hello compte de stockage, quel que soit l’ancienneté il est.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-151">Supply this if one backup should always be kept in hello storage account, regardless of how old it is.</span></span>

<span data-ttu-id="fa8b6-152">Voici un exemple de procédure toouse cette applet de commande.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-152">Following is an example of how toouse this cmdlet.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

<span data-ttu-id="fa8b6-153">tooget hello planification de sauvegarde actuelle, utilisez Get-AzureRmWebAppBackupConfiguration de hello applet de commande.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-153">tooget hello current backup schedule, use hello Get-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="fa8b6-154">Cela peut être utile pour modifier une planification qui a déjà été configurée.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-154">This can be useful for modifying a schedule that has already been configured.</span></span>

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify hello configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply hello new configuration by piping it into hello Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a><span data-ttu-id="fa8b6-155">Restauration d’une application web à partir d’une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="fa8b6-155">Restore a web app from a backup</span></span>
<span data-ttu-id="fa8b6-156">toorestore une application web à partir d’une sauvegarde, l’applet de commande utilisez hello AzureRmWebAppBackup de restauration.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-156">toorestore a web app from a backup, use hello Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="fa8b6-157">toouse de façon plus simple de Hello cette applet de commande est toopipe dans un objet de sauvegarde récupéré à partir d’applet de commande Get-AzureRmWebAppBackup de hello ou l’applet de commande Get-AzureRmWebAppBackupList.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-157">hello easiest way toouse this cmdlet is toopipe in a backup object retrieved from hello Get-AzureRmWebAppBackup cmdlet or Get-AzureRmWebAppBackupList cmdlet.</span></span>

<span data-ttu-id="fa8b6-158">Une fois que vous avez un objet de sauvegarde, vous pouvez la canaliser dans l’applet de commande Restore-AzureRmWebAppBackup hello.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-158">Once you have a backup object, you can pipe it into hello Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="fa8b6-159">Spécifiez hello tooindicate du paramètre commutateur de remplacement que vous envisagez de contenu de hello toooverwrite de votre application web avec hello de sauvegarde de hello.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-159">Specify hello Overwrite switch parameter tooindicate that you intend toooverwrite hello contents of your web app with hello contents of hello backup.</span></span> <span data-ttu-id="fa8b6-160">Si la sauvegarde de hello contient des bases de données, ces bases de données sont également restaurées.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-160">If hello backup contains databases, those databases are restored as well.</span></span>

        $backup | Restore-AzureRmWebAppBackup -Overwrite

<span data-ttu-id="fa8b6-161">Voici un exemple de comment toouse hello AzureRmWebAppBackup de restauration en spécifiant tous les paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-161">Following is an example of how toouse hello Restore-AzureRmWebAppBackup by specifying all hello parameters.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a><span data-ttu-id="fa8b6-162">Supprimer une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="fa8b6-162">Delete a backup</span></span>
<span data-ttu-id="fa8b6-163">toodelete une sauvegarde, utilisez l’applet de commande Remove-AzureRmWebAppBackup de hello.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-163">toodelete a backup, use hello Remove-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="fa8b6-164">Sauvegarde de hello est supprimée de votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-164">This removes hello backup from your storage account.</span></span> <span data-ttu-id="fa8b6-165">Spécifiez le nom de votre application, son groupe de ressources, et hello ID Hello sauvegarde que vous souhaitez toodelete.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-165">Specify your app name, its resource group, and hello ID of hello backup you want toodelete.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

<span data-ttu-id="fa8b6-166">Vous pouvez également diriger un objet de sauvegarde dans toodelete d’applet de commande Remove-AzureRmWebAppBackup de hello il.</span><span class="sxs-lookup"><span data-stu-id="fa8b6-166">You can also pipe a backup object into hello Remove-AzureRmWebAppBackup cmdlet toodelete it.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
