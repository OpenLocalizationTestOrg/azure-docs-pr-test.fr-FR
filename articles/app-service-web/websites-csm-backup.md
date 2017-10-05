---
title: Utilisation de REST pour sauvegarder et restaurer des applications App Service
description: "Découvrez comment utiliser les appels d’API RESTful pour sauvegarder et restaurer une application dans Azure App Service"
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: f94d0aea-edc1-43ab-9b51-ea7375859276
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: c1b8fc3be3af46279bf35bddbc82acf1827b9eb9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-rest-to-back-up-and-restore-app-service-apps"></a><span data-ttu-id="a0c3c-103">Utilisation de REST pour sauvegarder et restaurer des applications App Service</span><span class="sxs-lookup"><span data-stu-id="a0c3c-103">Use REST to back up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a0c3c-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a0c3c-104">PowerShell</span></span>](../app-service/app-service-powershell-backup.md)
> * [<span data-ttu-id="a0c3c-105">API REST</span><span class="sxs-lookup"><span data-stu-id="a0c3c-105">REST API</span></span>](websites-csm-backup.md)
> 
> 

<span data-ttu-id="a0c3c-106">[applications App Service](https://azure.microsoft.com/services/app-service/web/) peuvent être sauvegardées en tant qu’objets blob dans Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-106">[App Service apps](https://azure.microsoft.com/services/app-service/web/) can be backed up as blobs in Azure storage.</span></span> <span data-ttu-id="a0c3c-107">La sauvegarde peut également contenir des bases de données de l’application.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-107">The backup can also contain the app’s databases.</span></span> <span data-ttu-id="a0c3c-108">En cas de suppression accidentelle de l’application, ou si l’application doit être rétablie à une version antérieure, il est possible de la restaurer à partir d’une sauvegarde précédente.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-108">If the app is ever accidentally deleted, or if the app needs to be reverted to a previous version, it can be restored from any previous backup.</span></span> <span data-ttu-id="a0c3c-109">Les sauvegardes peuvent être effectuées à tout moment à la demande, ou être planifiées à des intervalles appropriés.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-109">Backups can be done at any time on demand, or backups can be scheduled at suitable intervals.</span></span>

<span data-ttu-id="a0c3c-110">Cet article explique comment sauvegarder et restaurer une application à l’aide de requêtes d’API RESTful.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-110">This article explains how to backup and restore an app with RESTful API requests.</span></span> <span data-ttu-id="a0c3c-111">Si vous souhaitez créer et gérer des sauvegardes d’application sous la forme de graphiques dans le portail Azure, consultez [Sauvegarder une application web dans Azure App Service](web-sites-backup.md)</span><span class="sxs-lookup"><span data-stu-id="a0c3c-111">If you would like to create and manage app backups graphically through the Azure portal, see [Back up a web app in Azure App Service](web-sites-backup.md)</span></span>

<a name="gettingstarted"></a>

## <a name="getting-started"></a><span data-ttu-id="a0c3c-112">Mise en route</span><span class="sxs-lookup"><span data-stu-id="a0c3c-112">Getting Started</span></span>
<span data-ttu-id="a0c3c-113">Pour envoyer des requêtes REST, vous devez connaître le **nom**, le **groupe de ressources** et l’**ID d’abonnement** de votre application. Vous trouverez ces informations en cliquant sur votre application dans le panneau **App Service** du [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a0c3c-113">To send REST requests, you need to know your app’s **name**, **resource group**, and **subscription id**. This information can be found by clicking your app in the **App Service** blade of the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a0c3c-114">Pour les exemples de cet article, nous configurons le site web **backuprestoreapiexamples.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-114">For the examples in this article, we are configuring the website **backuprestoreapiexamples.azurewebsites.net**.</span></span> <span data-ttu-id="a0c3c-115">Celui-ci est stocké dans le groupe de ressources Default-Web-WestUS et s’exécute sur un abonnement associé à l’ID 00001111-2222-3333-4444-555566667777.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-115">It is stored in the Default-Web-WestUS resource group and is running on a subscription with the ID 00001111-2222-3333-4444-555566667777.</span></span>

![Informations de l’exemple de site web][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a><span data-ttu-id="a0c3c-117">API REST de sauvegarde et de restauration</span><span class="sxs-lookup"><span data-stu-id="a0c3c-117">Backup and restore REST API</span></span>
<span data-ttu-id="a0c3c-118">Nous allons maintenant présenter plusieurs exemples illustrant la manière dont il est possible d’utiliser l’API REST pour sauvegarder et restaurer une application.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-118">We will now cover several examples of how to use the REST API to backup and restore an app.</span></span> <span data-ttu-id="a0c3c-119">Chaque exemple inclut une URL et un corps de requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-119">Each example includes a URL and HTTP request body.</span></span> <span data-ttu-id="a0c3c-120">L’exemple d’URL contient des espaces réservés entre accolades, du type {subscription-id}.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-120">The sample URL contains placeholders wrapped in curly braces, such as {subscription-id}.</span></span> <span data-ttu-id="a0c3c-121">Remplacez les espaces réservés par les informations correspondantes de votre application.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-121">Replace the placeholders with the corresponding information for your app.</span></span> <span data-ttu-id="a0c3c-122">À titre de référence, voici une explication de chaque espace réservé qui apparaît dans les exemples d’URL.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-122">For reference, here is an explanation of each placeholder that appears in the example URLs.</span></span>

* <span data-ttu-id="a0c3c-123">subscription-id : ID de l’abonnement Azure contenant l’application</span><span class="sxs-lookup"><span data-stu-id="a0c3c-123">subscription-id – ID of the Azure subscription containing the app</span></span>
* <span data-ttu-id="a0c3c-124">resource-group-name : nom du groupe de ressources contenant l’application</span><span class="sxs-lookup"><span data-stu-id="a0c3c-124">resource-group-name – Name of the resource group containing the app</span></span>
* <span data-ttu-id="a0c3c-125">name : nom de l’application</span><span class="sxs-lookup"><span data-stu-id="a0c3c-125">name – Name of the app</span></span>
* <span data-ttu-id="a0c3c-126">backup-id : ID de la sauvegarde de l’application</span><span class="sxs-lookup"><span data-stu-id="a0c3c-126">backup-id – ID of the app backup</span></span>

<span data-ttu-id="a0c3c-127">Pour accéder à la documentation complète de l’API, y compris plusieurs paramètres facultatifs pouvant être inclus dans la requête HTTP, consultez l’ [Explorateur de ressources Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a0c3c-127">For the complete documentation of the API, including several optional parameters that can be included in the HTTP request, see the [Azure Resource Explorer](https://resources.azure.com/).</span></span>

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a><span data-ttu-id="a0c3c-128">Sauvegarde d’une application à la demande</span><span class="sxs-lookup"><span data-stu-id="a0c3c-128">Backup an app on demand</span></span>
<span data-ttu-id="a0c3c-129">Pour sauvegarder une application immédiatement, envoyez une demande **POST** à **https://management.azure.com/subscriptions/{id-abonnement}/resourceGroups/{nom-groupe-ressources}/providers/Microsoft.Web/sites/{nom}/backup/**.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-129">To back up an app immediately, send a **POST** request to **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.</span></span>

<span data-ttu-id="a0c3c-130">Voici à quoi ressemble l’URL dans notre exemple de site web.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-130">Here is what the URL looks like using our example website.</span></span> <span data-ttu-id="a0c3c-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span><span class="sxs-lookup"><span data-stu-id="a0c3c-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span></span>

<span data-ttu-id="a0c3c-132">Spécifiez un objet JSON dans le corps de votre requête afin de spécifier le compte de stockage à utiliser pour stocker la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-132">Supply a JSON object in the body of your request to specify which storage account to use to store the backup.</span></span> <span data-ttu-id="a0c3c-133">L’objet JSON doit avoir une propriété nommée **storageAccountUrl**, qui contient une [URL SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) qui octroie un accès en écriture au conteneur Azure Storage dans lequel l’objet blob de sauvegarde sera stocké.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-133">The JSON object must have a property named **storageAccountUrl**, which holds a [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) granting write access to the Azure Storage container that holds the backup blob.</span></span> <span data-ttu-id="a0c3c-134">Si vous souhaitez sauvegarder vos bases de données, vous devez également fournir une liste contenant les noms, les types et les chaînes de connexion des bases de données à sauvegarder.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-134">If you want to back up your databases, you must also supply a list containing the names, types, and connection strings of the databases to be backed up.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        “databases”: [
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”,
                "connectionString": "<your database connection string>"
            }
        ]
    }
}
```

<span data-ttu-id="a0c3c-135">Une sauvegarde de l’application débute immédiatement après la réception de la requête.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-135">A backup of the app begins immediately when the request is received.</span></span> <span data-ttu-id="a0c3c-136">Le processus de sauvegarde peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-136">The backup process may take a long time to complete.</span></span> <span data-ttu-id="a0c3c-137">La réponse HTTP contient un ID que vous pouvez utiliser dans une autre requête pour connaître l’état de la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-137">The HTTP response contains an ID that you can use in another request to see the status of the backup.</span></span> <span data-ttu-id="a0c3c-138">Voici un exemple du corps de la réponse HTTP à notre requête de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-138">Here is an example of the body of the HTTP response to our backup request.</span></span>

```
{
    "id": "/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples",
    "name": " backuprestoreapiexamples ",
    "type": "Microsoft.Web/sites",
    "location": "WestUS",
    "properties":    {
        "id": 1,
        "storageAccountUrl": “https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl”,
        "blobName": “backup_201509291825.zip”,
        "name": "backup_201509291825",
        "status": 4,
        "sizeInBytes": 0,
        "created": "2015-09-29T18:25:26.3992707Z",
        "log": null,
        "databases": [
            {
                "databaseType": "SqlAzure",
                "name": "MyDatabase1",
                "connectionString": "<your database connection string>"
            }
        ],
        "scheduled": false,
        "correlationId": "ea730f4d-dd06-4f7f-a090-9aa09k662h36",
    }
}
```

> [!NOTE]
> <span data-ttu-id="a0c3c-139">Vous pouvez rencontrer des messages d’erreur dans la propriété du journal de la réponse HTTP.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-139">Error messages can be found in the log property of the HTTP response.</span></span>
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a><span data-ttu-id="a0c3c-140">Planification de sauvegardes automatiques</span><span class="sxs-lookup"><span data-stu-id="a0c3c-140">Schedule automatic backups</span></span>
<span data-ttu-id="a0c3c-141">Si vous pouvez sauvegarder une application à la demande, vous avez également la possibilité de planifier l’exécution automatique d’une sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-141">In addition to backing up an app on demand, you can also schedule a backup to happen automatically.</span></span>

### <a name="set-up-a-new-automatic-backup-schedule"></a><span data-ttu-id="a0c3c-142">Configurer une nouvelle planification de sauvegarde automatique</span><span class="sxs-lookup"><span data-stu-id="a0c3c-142">Set up a new automatic backup schedule</span></span>
<span data-ttu-id="a0c3c-143">Pour configurer une planification de sauvegarde, envoyez une demande **PUT** à **https://management.azure.com/subscriptions/{id-abonnement}/resourceGroups/{nom-groupe-ressources}/providers/Microsoft.Web/sites/{nom}/config/backup/**.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-143">To set up a backup schedule, send a **PUT** request to **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.</span></span>

<span data-ttu-id="a0c3c-144">Voici à quoi ressemble l’URL dans notre exemple de site web.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-144">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="a0c3c-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span><span class="sxs-lookup"><span data-stu-id="a0c3c-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span></span>

<span data-ttu-id="a0c3c-146">Le corps de requête doit comporter un objet JSON qui spécifie la configuration de la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-146">The request body must have a JSON object that specifies the backup configuration.</span></span> <span data-ttu-id="a0c3c-147">Cet exemple reprend tous les paramètres nécessaires.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-147">Here is an example with all the required parameters.</span></span>

```
{
    "location": "WestUS",
    "properties": // Represents an app restore request
    {
        "backupSchedule": { // Required for automatically scheduled backups
            "frequencyInterval": "7",
            "frequencyUnit": "Day",
            "keepAtLeastOneBackup": "True",
            "retentionPeriodInDays": "10",
        },
        "enabled": "True", // Must be set to true to enable automatic backups
        "name": “mysitebackup”,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

<span data-ttu-id="a0c3c-148">Cet exemple configure l’application de manière à ce qu’elle soit automatiquement sauvegardée tous les sept jours.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-148">This example configures the app to be automatically backed up every seven days.</span></span> <span data-ttu-id="a0c3c-149">Les paramètres **frequencyInterval** et **frequencyUnit** déterminent la fréquence à laquelle les sauvegardes sont exécutées.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-149">The parameters **frequencyInterval** and **frequencyUnit** together determine how often the backups happen.</span></span> <span data-ttu-id="a0c3c-150">Les valeurs valides de **frequencyUnit** sont **hour** et **day**.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-150">Valid values for **frequencyUnit** are **hour** and **day**.</span></span> <span data-ttu-id="a0c3c-151">Par exemple, pour sauvegarder une application toutes les 12 heures, définissez le paramètre frequencyInterval sur 12 et attribuez la valeur « hour » au paramètre frequencyUnit.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-151">For example, to back up an app every 12 hours, set frequencyInterval to 12 and frequencyUnit to hour.</span></span>

<span data-ttu-id="a0c3c-152">Les anciennes sauvegardes sont automatiquement supprimées du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-152">Old backups are automatically removed from the storage account.</span></span> <span data-ttu-id="a0c3c-153">Vous pouvez contrôler l’ancienneté des sauvegardes en définissant le paramètre **retentionPeriodInDays** .</span><span class="sxs-lookup"><span data-stu-id="a0c3c-153">You can control how old the backups can be by setting the **retentionPeriodInDays** parameter.</span></span> <span data-ttu-id="a0c3c-154">Si vous souhaitez qu’au moins une sauvegarde soit toujours enregistrée, quelle que soit son ancienneté, définissez le paramètre **keepAtLeastOneBackup** sur true.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-154">If you want to always have at least one backup saved, regardless of how old it is, set **keepAtLeastOneBackup** to true.</span></span>

### <a name="get-the-automatic-backup-schedule"></a><span data-ttu-id="a0c3c-155">Obtenir la planification de sauvegarde automatique</span><span class="sxs-lookup"><span data-stu-id="a0c3c-155">Get the automatic backup schedule</span></span>
<span data-ttu-id="a0c3c-156">Pour obtenir la configuration de sauvegarde d’une application, envoyez une demande **POST** à l’URL **https://management.azure.com/subscriptions/{id-abonnement}/resourceGroups/{nom-groupe-ressources}/providers/Microsoft.Web/sites/{nom}/config/backup/list**.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-156">To get an app’s backup configuration, send a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.</span></span>

<span data-ttu-id="a0c3c-157">L’URL de notre exemple de site est **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-157">The URL for our example site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span></span>

<a name="get-backup-status"></a>

## <a name="get-the-status-of-a-backup"></a><span data-ttu-id="a0c3c-158">Informations sur l’état d’une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="a0c3c-158">Get the status of a backup</span></span>
<span data-ttu-id="a0c3c-159">Selon la taille de l’application, une sauvegarde peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-159">Depending on how large the app is, a backup may take a while to complete.</span></span> <span data-ttu-id="a0c3c-160">Les sauvegardes peuvent également échouer, dépasser le délai d’attente ou n’aboutir que partiellement.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-160">Backups might also fail, time out, or partially succeed.</span></span> <span data-ttu-id="a0c3c-161">Pour consulter l’état de toutes les sauvegardes d’une application, envoyez une demande **GET** à l’URL **https://management.azure.com/subscriptions/{id-abonnement}/resourceGroups/{nom-groupe-ressources}/providers/Microsoft.Web/sites/{nom}/backups**.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-161">To see the status of all an app’s backups, send a **GET** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.</span></span>

<span data-ttu-id="a0c3c-162">Pour consulter l’état d’une sauvegarde spécifique, envoyez une demande GET à l’URL **https://management.azure.com/subscriptions/{id-abonnement}/resourceGroups/{nom-groupe-ressources}/providers/Microsoft.Web/sites/{nom}/backups/{id-sauvegarde}**.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-162">To see the status of a specific backup, send a GET request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="a0c3c-163">Voici à quoi ressemble l’URL dans notre exemple de site web.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-163">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="a0c3c-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="a0c3c-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<span data-ttu-id="a0c3c-165">Le corps de la réponse contient un objet JSON similaire à cet exemple.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-165">The response body contains a JSON object similar to this example.</span></span>

```
{
    "properties":  {
        "id": 1,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl",
        "blobName": "backup_201509291734.zip",
        "name": "backup_201509291734",
        "status": 2,
        "sizeInBytes": 151973,
        "created": "2015-09-29T17:34:57.2091605",
        "scheduled": false,
        "lastRestoreTimeStamp": null,
        "finishedTimeStamp": "2015-09-29T17:35:11.3293602",
        "correlationId": "2379fc13-418a-4b9c-920d-d06e73c5028d",
        "websiteSizeInBytes": 209920
    }
}
```

<span data-ttu-id="a0c3c-166">L’état d’une sauvegarde est un type énuméré.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-166">The status of a backup is an enumerated type.</span></span> <span data-ttu-id="a0c3c-167">Voici la liste de tous les états possibles.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-167">Here is every possible state.</span></span>

* <span data-ttu-id="a0c3c-168">0 – InProgress : la sauvegarde a démarré mais n’est pas encore terminée.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-168">0 – InProgress: The backup has been started but has not yet completed.</span></span>
* <span data-ttu-id="a0c3c-169">1 – Failed : la sauvegarde a échoué.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-169">1 – Failed: The backup was unsuccessful.</span></span>
* <span data-ttu-id="a0c3c-170">2 – Succeeded : la sauvegarde s’est terminée correctement.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-170">2 – Succeeded: The backup completed successfully.</span></span>
* <span data-ttu-id="a0c3c-171">3 – TimedOut : la sauvegarde ne s’est pas terminée dans les temps et a été annulée.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-171">3 – TimedOut: The backup did not finish in time and was canceled.</span></span>
* <span data-ttu-id="a0c3c-172">4 – Created : la demande de sauvegarde est en attente mais n’a pas été démarrée.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-172">4 – Created: The backup request is queued but has not been started.</span></span>
* <span data-ttu-id="a0c3c-173">5 – Skipped : la sauvegarde ne s’est pas poursuivie en raison d’un trop grand nombre de sauvegardes planifiées.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-173">5 – Skipped: The backup did not proceed due to a schedule triggering too many backups.</span></span>
* <span data-ttu-id="a0c3c-174">6 – PartiallySucceeded : la sauvegarde a réussi, mais certains fichiers n’ont pas été sauvegardés en raison de problèmes de lecture.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-174">6 – PartiallySucceeded: The backup succeeded, but some files were not backed up because they could not be read.</span></span> <span data-ttu-id="a0c3c-175">Cela se produit généralement lorsqu’un verrou exclusif est placé sur les fichiers.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-175">This usually happens because an exclusive lock was placed on the files.</span></span>
* <span data-ttu-id="a0c3c-176">7 – DeleteInProgress : la sauvegarde a fait l’objet d’une demande de suppression, mais n’a pas encore été supprimée.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-176">7 – DeleteInProgress: The backup has been requested to be deleted, but has not yet been deleted.</span></span>
* <span data-ttu-id="a0c3c-177">8 – DeleteFailed : la sauvegarde n’a pas pu être supprimée.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-177">8 – DeleteFailed: The backup could not be deleted.</span></span> <span data-ttu-id="a0c3c-178">Cela peut se produire si l’URL SAS utilisée pour créer la sauvegarde a expiré.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-178">This might happen because the SAS URL that was used to create the backup has expired.</span></span>
* <span data-ttu-id="a0c3c-179">9 – Deleted : la sauvegarde a été supprimée avec succès.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-179">9 – Deleted: The backup was deleted successfully.</span></span>

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a><span data-ttu-id="a0c3c-180">Restauration d’une application à partir d’une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="a0c3c-180">Restore an app from a backup</span></span>
<span data-ttu-id="a0c3c-181">Si votre application a été supprimée, ou si vous voulez rétablir votre application à une version antérieure, vous pouvez restaurer l’application à partir d’une sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-181">If your app has been deleted, or if you want to revert your app to a previous version, you can restore the app from a backup.</span></span> <span data-ttu-id="a0c3c-182">Pour invoquer une restauration, envoyez une demande **POST** à l’URL **https://management.azure.com/subscriptions/{id-abonnement}/resourceGroups/{nom-groupe-ressources}/providers/Microsoft.Web/sites/{nom}/backups/{id-sauvegarde}/restore**.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-182">To invoke a restore, send a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.</span></span>

<span data-ttu-id="a0c3c-183">Voici à quoi ressemble l’URL dans notre exemple de site web.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-183">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="a0c3c-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span><span class="sxs-lookup"><span data-stu-id="a0c3c-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span></span>

<span data-ttu-id="a0c3c-185">Dans le corps de la requête, envoyez un objet JSON qui contient les propriétés de l’opération de restauration.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-185">In the request body, send a JSON object that contains the properties for the restore operation.</span></span> <span data-ttu-id="a0c3c-186">Voici un exemple contenant toutes les propriétés requises :</span><span class="sxs-lookup"><span data-stu-id="a0c3c-186">Here is an example containing all required properties:</span></span>

```
{
    "location": "WestUS",
    "properties":
    {
        "blobName": "backup_201509280431.zip",
        "databases": [ // Not required unless you’re restoring databases
            {
                “databaseType”: “SqlAzure”,
                “name”: “MyDatabase1”
        }],
        "overwrite": "true",
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl" // SAS URL to storage container containing your website backup
    }
}
```

### <a name="restore-to-a-new-app"></a><span data-ttu-id="a0c3c-187">Restauration vers une nouvelle application</span><span class="sxs-lookup"><span data-stu-id="a0c3c-187">Restore to a new app</span></span>
<span data-ttu-id="a0c3c-188">Lors de la restauration d’une sauvegarde, vous avez parfois intérêt à créer une application au lieu de remplacer une application existante.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-188">Sometimes you might want to create a new app when you restore a backup, instead of overwriting an already existing app.</span></span> <span data-ttu-id="a0c3c-189">Pour ce faire, modifiez l’URL de requête pour pointer vers la nouvelle application que vous souhaitez créer et définissez la propriété **overwrite** dans le fichier JSON sur **false**.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-189">To do this, change the request URL to point to the new app you want to create, and change the **overwrite** property in the JSON to **false**.</span></span>

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a><span data-ttu-id="a0c3c-190">Suppression d’une sauvegarde d’application</span><span class="sxs-lookup"><span data-stu-id="a0c3c-190">Delete an app backup</span></span>
<span data-ttu-id="a0c3c-191">Pour supprimer une sauvegarde, envoyez une demande **DELETE** à l’URL **https://management.azure.com/subscriptions/{id-abonnement}/resourceGroups/{nom-groupe-ressources}/providers/Microsoft.Web/sites/{nom}/backups/{id-sauvegarde}**.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-191">If you would like to delete a backup, send a **DELETE** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="a0c3c-192">Voici à quoi ressemble l’URL dans notre exemple de site web.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-192">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="a0c3c-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="a0c3c-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a><span data-ttu-id="a0c3c-194">Gestion de l’URL SAS d’une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="a0c3c-194">Manage a backup’s SAS URL</span></span>
<span data-ttu-id="a0c3c-195">Les applications Azure App Service tentent de supprimer votre sauvegarde d’Azure Storage en utilisant l’URL SAS fournie au moment de la création de la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-195">Azure App Service will attempt to delete your backup from Azure Storage using the SAS URL that was provided when the backup was created.</span></span> <span data-ttu-id="a0c3c-196">Si cette URL SAS n’est plus valide, la sauvegarde ne peut pas être supprimée via l’API REST.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-196">If this SAS URL is no longer valid, the backup cannot be deleted through the REST API.</span></span> <span data-ttu-id="a0c3c-197">Toutefois, vous pouvez mettre à jour l’URL SAS associée à une sauvegarde en envoyant une demande **POST** à l’URL **https://management.azure.com/subscriptions/{id-abonnement}/resourceGroups/{nom-groupe-ressources}/providers/Microsoft.Web/sites/{nom}/backups/{id-sauvegarde}/list**.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-197">However, you can update the SAS URL associated with a backup by sending a **POST** request to the URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span></span>

<span data-ttu-id="a0c3c-198">Voici à quoi ressemble l’URL dans notre exemple de site web.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-198">Here is what the URL looks like for our example website.</span></span> <span data-ttu-id="a0c3c-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span><span class="sxs-lookup"><span data-stu-id="a0c3c-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span></span>

<span data-ttu-id="a0c3c-200">Dans le corps de la requête, envoyez un objet JSON contenant la nouvelle URL SAS.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-200">In the request body, send a JSON object that contains the new SAS URL.</span></span> <span data-ttu-id="a0c3c-201">Voici un exemple.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-201">Here is an example.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> <span data-ttu-id="a0c3c-202">Pour des raisons de sécurité, l’URL SAS associée à une sauvegarde n’est pas renvoyée lors de l’envoi d’une requête GET pour une sauvegarde spécifique.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-202">For security reasons, the SAS URL associated with a backup is not returned when sending a GET request for a specific backup.</span></span> <span data-ttu-id="a0c3c-203">Si vous souhaitez afficher l’URL SAS associée à une sauvegarde, envoyez une requête POST à l’URL indiquée ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-203">If you want to view the SAS URL associated with a backup, send a POST request to the same URL above.</span></span> <span data-ttu-id="a0c3c-204">Incluez un objet JSON vide dans le corps de la requête.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-204">Include an empty JSON object in the request body.</span></span> <span data-ttu-id="a0c3c-205">La réponse du serveur contient toutes les informations relatives à cette sauvegarde, notamment son URL SAS.</span><span class="sxs-lookup"><span data-stu-id="a0c3c-205">The response from the server contains all of that backup’s information, including its SAS URL.</span></span>
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
