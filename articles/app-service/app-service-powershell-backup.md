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
# <a name="use-powershell-tooback-up-and-restore-app-service-apps"></a>Utilisez PowerShell tooback et restaurer des applications de Service d’applications
> [!div class="op_single_selector"]
> * [PowerShell](app-service-powershell-backup.md)
> * [API REST](../app-service-web/websites-csm-backup.md)
> 
> 

Découvrez comment toouse Azure PowerShell tooback et de restauration [des applications de Service d’applications](https://azure.microsoft.com/services/app-service/web/). Pour plus d’informations sur les sauvegardes d’applications web, et notamment en connaître les exigences et restrictions, consultez [Sauvegarder une application web dans Azure App Service](../app-service-web/web-sites-backup.md).

## <a name="prerequisites"></a>Composants requis
toouse PowerShell toomanage vos sauvegardes de l’application, vous devez hello suivant :

* **Une URL SAS** qui permet de lire et conteneur de stockage Azure tooan un accès en écriture. Consultez [modèle de présentation hello SAP](../storage/common/storage-dotnet-shared-access-signature-part-1.md) pour une explication de l’URL de SAP. Consultez la page [Utilisation d’Azure PowerShell avec Azure Storage](../storage/common/storage-powershell-guide-full.md) pour obtenir des exemples de gestion d'Azure Storage à l’aide de PowerShell.
* **Une chaîne de connexion de base de données** si vous souhaitez tooback une base de données en même temps que votre application web.

### <a name="how-toogenerate-a-sas-url-toouse-with-hello-web-app-backup-cmdlets"></a>Comment toogenerate un toouse URL de SAP à l’application web de hello applets de commande de sauvegarde
Une URL SAP peut être générée avec PowerShell. Voici un exemple de la façon dont un qui peut être utilisé avec les applets de commande hello toogenerate abordé dans cet article.

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure tooselect hello appropriate key. Here we select hello first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a>Installer Azure PowerShell 1.3.2 ou versions ultérieures
Pour obtenir des instructions sur l’installation et l’utilisation d’Azure PowerShell, consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview) .

## <a name="create-a-backup"></a>Création d'une sauvegarde
Utilisez toocreate d’applet de commande hello AzureRmWebAppBackup de nouveau une sauvegarde d’une application web.

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

Vous obtenez une sauvegarde avec un nom généré automatiquement. Si vous souhaitez que tooprovide un nom pour votre sauvegarde, utiliser le paramètre facultatif de Nom_sauvegarde hello.

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

tooinclude une base de données dans la sauvegarde de hello, tout d’abord créer un paramètre de sauvegarde de base de données à l’aide d’applet de commande New-AzureRmWebAppDatabaseBackupSetting hello, puis fournissez ce paramètre Bonjour bases de données de l’applet de commande New-AzureRmWebAppBackup hello. paramètre de bases de données Hello accepte un tableau de paramètres de base de données, ce qui vous tooback plus d’une base de données.

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a>Obtenir des sauvegardes
applet de commande Get-AzureRmWebAppBackupList Hello retourne un tableau de toutes les sauvegardes pour une application web. Vous devez fournir le nom hello de hello web app et son groupe de ressources.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

tooget une sauvegarde spécifique, utilisez l’applet de commande Get-AzureRmWebAppBackup de hello.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

Vous pouvez également diriger un objet d’application web dans une des applets de commande de gestion de sauvegarde hello pour des raisons pratiques.

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a>Planification de sauvegardes automatiques
Vous pouvez planifier des sauvegardes toohappen automatiquement à un intervalle spécifié. tooconfigure une planification de sauvegarde, utilisez l’applet de commande de hello AzureRmWebAppBackupConfiguration de modification. Cette applet de commande accepte plusieurs paramètres :

* **Nom** hello - nom de l’application web de hello.
* **ResourceGroupName** hello - nom de l’application web contenant hello d’hello ressource groupe.
* **Slot** : facultatif. nom de Hello de l’emplacement d’application web hello.
* **StorageAccountUrl** -hello URL de SAP de conteneur de stockage Azure hello utilisé des sauvegardes toostore hello.
* **FrequencyInterval** -valeur numérique pour la fréquence à laquelle hello les sauvegardes doivent être effectuées. Cette valeur doit être un entier positif.
* **FrequencyUnit** -unité de temps pour la fréquence à laquelle hello les sauvegardes doivent être effectuées. Peut être exprimée en heures et en jours.
* **RetentionPeriodInDays** - le nombre de jours de sauvegardes automatiques hello doivent être enregistrés avant d’être automatiquement supprimés.
* **StartTime** : facultatif. heure de Hello lorsque les sauvegardes automatiques hello doivent commencer. Les sauvegardes débutent immédiatement si la valeur est null. Doit être une valeur DateTime.
* **Databases** : facultatif. Tableau de DatabaseBackupSettings pour toobackup de bases de données hello.
* **KeepAtLeastOneBackup** - paramètre à bascule facultatif. Approvisionnement cela si une sauvegarde doit toujours être conservée dans hello compte de stockage, quel que soit l’ancienneté il est.

Voici un exemple de procédure toouse cette applet de commande.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

tooget hello planification de sauvegarde actuelle, utilisez Get-AzureRmWebAppBackupConfiguration de hello applet de commande. Cela peut être utile pour modifier une planification qui a déjà été configurée.

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify hello configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply hello new configuration by piping it into hello Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a>Restauration d’une application web à partir d’une sauvegarde
toorestore une application web à partir d’une sauvegarde, l’applet de commande utilisez hello AzureRmWebAppBackup de restauration. toouse de façon plus simple de Hello cette applet de commande est toopipe dans un objet de sauvegarde récupéré à partir d’applet de commande Get-AzureRmWebAppBackup de hello ou l’applet de commande Get-AzureRmWebAppBackupList.

Une fois que vous avez un objet de sauvegarde, vous pouvez la canaliser dans l’applet de commande Restore-AzureRmWebAppBackup hello. Spécifiez hello tooindicate du paramètre commutateur de remplacement que vous envisagez de contenu de hello toooverwrite de votre application web avec hello de sauvegarde de hello. Si la sauvegarde de hello contient des bases de données, ces bases de données sont également restaurées.

        $backup | Restore-AzureRmWebAppBackup -Overwrite

Voici un exemple de comment toouse hello AzureRmWebAppBackup de restauration en spécifiant tous les paramètres de hello.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a>Supprimer une sauvegarde
toodelete une sauvegarde, utilisez l’applet de commande Remove-AzureRmWebAppBackup de hello. Sauvegarde de hello est supprimée de votre compte de stockage. Spécifiez le nom de votre application, son groupe de ressources, et hello ID Hello sauvegarde que vous souhaitez toodelete.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

Vous pouvez également diriger un objet de sauvegarde dans toodelete d’applet de commande Remove-AzureRmWebAppBackup de hello il.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
