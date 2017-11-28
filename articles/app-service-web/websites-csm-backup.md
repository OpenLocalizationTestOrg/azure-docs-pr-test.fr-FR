---
title: "aaaUse REST tooback haut et restaurer des applications de Service d’applications"
description: "Découvrez comment toouse API RESTful appelle tooback et la restauration d’une application dans Azure App Service"
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
ms.openlocfilehash: f77bdfc7de1626d04d8d0c0e8979231ae1ced81a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a><span data-ttu-id="9ce6a-103">Utilisez reste tooback et restaurer des applications de Service d’applications</span><span class="sxs-lookup"><span data-stu-id="9ce6a-103">Use REST tooback up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ce6a-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ce6a-104">PowerShell</span></span>](../app-service/app-service-powershell-backup.md)
> * [<span data-ttu-id="9ce6a-105">API REST</span><span class="sxs-lookup"><span data-stu-id="9ce6a-105">REST API</span></span>](websites-csm-backup.md)
> 
> 

<span data-ttu-id="9ce6a-106">[applications App Service](https://azure.microsoft.com/services/app-service/web/) peuvent être sauvegardées en tant qu’objets blob dans Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-106">[App Service apps](https://azure.microsoft.com/services/app-service/web/) can be backed up as blobs in Azure storage.</span></span> <span data-ttu-id="9ce6a-107">sauvegarde de Hello peut également contenir des bases de données de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-107">hello backup can also contain hello app’s databases.</span></span> <span data-ttu-id="9ce6a-108">Si l’application hello n’est jamais accidentellement, ou si hello application besoins toobe restaurer la version précédente de tooa, elle peut être restaurée à partir d’une sauvegarde précédente.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-108">If hello app is ever accidentally deleted, or if hello app needs toobe reverted tooa previous version, it can be restored from any previous backup.</span></span> <span data-ttu-id="9ce6a-109">Les sauvegardes peuvent être effectuées à tout moment à la demande, ou être planifiées à des intervalles appropriés.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-109">Backups can be done at any time on demand, or backups can be scheduled at suitable intervals.</span></span>

<span data-ttu-id="9ce6a-110">Cet article explique comment toobackup demandes et restauration une application avec une API RESTful.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-110">This article explains how toobackup and restore an app with RESTful API requests.</span></span> <span data-ttu-id="9ce6a-111">Si vous souhaitez toocreate et gérer les sauvegardes d’application sous la forme de hello portail Azure, consultez [sauvegardez une application web dans Azure App Service](web-sites-backup.md)</span><span class="sxs-lookup"><span data-stu-id="9ce6a-111">If you would like toocreate and manage app backups graphically through hello Azure portal, see [Back up a web app in Azure App Service](web-sites-backup.md)</span></span>

<a name="gettingstarted"></a>

## <a name="getting-started"></a><span data-ttu-id="9ce6a-112">Mise en route</span><span class="sxs-lookup"><span data-stu-id="9ce6a-112">Getting Started</span></span>
<span data-ttu-id="9ce6a-113">demande de toosend REST, vous devez tooknow de votre application **nom**, **groupe de ressources**, et **id d’abonnement**. Ces informations sont accessibles en cliquant sur votre application Bonjour **du Service d’applications** Panneau de hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9ce6a-113">toosend REST requests, you need tooknow your app’s **name**, **resource group**, and **subscription id**. This information can be found by clicking your app in hello **App Service** blade of hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9ce6a-114">Pour obtenir des exemples hello dans cet article, nous examinons la configuration du site Web hello **backuprestoreapiexamples.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-114">For hello examples in this article, we are configuring hello website **backuprestoreapiexamples.azurewebsites.net**.</span></span> <span data-ttu-id="9ce6a-115">Il est stocké dans le groupe de ressources par défaut-Web-WestUS hello et est en cours d’exécution sur un abonnement par hello ID 00001111-2222-3333-4444-555566667777.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-115">It is stored in hello Default-Web-WestUS resource group and is running on a subscription with hello ID 00001111-2222-3333-4444-555566667777.</span></span>

![Informations de l’exemple de site web][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a><span data-ttu-id="9ce6a-117">API REST de sauvegarde et de restauration</span><span class="sxs-lookup"><span data-stu-id="9ce6a-117">Backup and restore REST API</span></span>
<span data-ttu-id="9ce6a-118">Nous allons maintenant aborder plusieurs exemples montrant comment toouse hello toobackup de l’API REST et restauration d’une application.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-118">We will now cover several examples of how toouse hello REST API toobackup and restore an app.</span></span> <span data-ttu-id="9ce6a-119">Chaque exemple inclut une URL et un corps de requête HTTP.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-119">Each example includes a URL and HTTP request body.</span></span> <span data-ttu-id="9ce6a-120">Hello, exemple d’URL contient des espaces réservés encapsulées dans des accolades, par exemple {id d’abonnement}.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-120">hello sample URL contains placeholders wrapped in curly braces, such as {subscription-id}.</span></span> <span data-ttu-id="9ce6a-121">Remplacez les espaces réservés de hello avec les informations correspondantes de hello pour votre application.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-121">Replace hello placeholders with hello corresponding information for your app.</span></span> <span data-ttu-id="9ce6a-122">Pour référence, voici une explication de chaque espace réservé qui apparaît dans les URL d’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-122">For reference, here is an explanation of each placeholder that appears in hello example URLs.</span></span>

* <span data-ttu-id="9ce6a-123">id d’abonnement : ID de l’application hello contenant de hello abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="9ce6a-123">subscription-id – ID of hello Azure subscription containing hello app</span></span>
* <span data-ttu-id="9ce6a-124">Resource-group-name : nom de l’application de conteneur hello hello ressource groupe</span><span class="sxs-lookup"><span data-stu-id="9ce6a-124">resource-group-name – Name of hello resource group containing hello app</span></span>
* <span data-ttu-id="9ce6a-125">nom : nom de l’application hello</span><span class="sxs-lookup"><span data-stu-id="9ce6a-125">name – Name of hello app</span></span>
* <span data-ttu-id="9ce6a-126">sauvegarde-id : ID de la sauvegarde d’application hello</span><span class="sxs-lookup"><span data-stu-id="9ce6a-126">backup-id – ID of hello app backup</span></span>

<span data-ttu-id="9ce6a-127">Pour une documentation complète hello Hello API, y compris plusieurs paramètres facultatifs qui peuvent être inclus dans la demande HTTP de hello, consultez hello [Explorateur de ressources Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9ce6a-127">For hello complete documentation of hello API, including several optional parameters that can be included in hello HTTP request, see hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a><span data-ttu-id="9ce6a-128">Sauvegarde d’une application à la demande</span><span class="sxs-lookup"><span data-stu-id="9ce6a-128">Backup an app on demand</span></span>
<span data-ttu-id="9ce6a-129">tooback installer une application immédiatement, envoyer un **POST** demande trop**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ sauvegarde /**.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-129">tooback up an app immediately, send a **POST** request too**https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backup/**.</span></span>

<span data-ttu-id="9ce6a-130">URL de hello ressemble à ceci à l’aide de notre site Web d’exemple.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-130">Here is what hello URL looks like using our example website.</span></span> <span data-ttu-id="9ce6a-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span><span class="sxs-lookup"><span data-stu-id="9ce6a-131">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**</span></span>

<span data-ttu-id="9ce6a-132">Fournissez un objet JSON dans le corps de hello de votre toospecify demande le toostore de toouse de compte de stockage hello sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-132">Supply a JSON object in hello body of your request toospecify which storage account toouse toostore hello backup.</span></span> <span data-ttu-id="9ce6a-133">objet JSON de Hello doit avoir une propriété nommée **storageAccountUrl**, lequel contient un [URL SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) octroi du conteneur de stockage Azure toohello un accès en écriture qui contient des objets blob de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-133">hello JSON object must have a property named **storageAccountUrl**, which holds a [SAS URL](../storage/common/storage-dotnet-shared-access-signature-part-1.md) granting write access toohello Azure Storage container that holds hello backup blob.</span></span> <span data-ttu-id="9ce6a-134">Si vous souhaitez tooback vos bases de données, vous devez également fournir une liste contenant les noms de hello, les types et les chaînes de connexion de hello toobe de bases de données sauvegardées.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-134">If you want tooback up your databases, you must also supply a list containing hello names, types, and connection strings of hello databases toobe backed up.</span></span>

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

<span data-ttu-id="9ce6a-135">Une sauvegarde de l’application hello commence immédiatement lorsque hello demande est reçue.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-135">A backup of hello app begins immediately when hello request is received.</span></span> <span data-ttu-id="9ce6a-136">processus de sauvegarde Hello peut prendre un toocomplete beaucoup de temps.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-136">hello backup process may take a long time toocomplete.</span></span> <span data-ttu-id="9ce6a-137">Hello réponse HTTP contient un ID que vous pouvez utiliser dans un autre état hello toosee de demande de sauvegarde de hello.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-137">hello HTTP response contains an ID that you can use in another request toosee hello status of hello backup.</span></span> <span data-ttu-id="9ce6a-138">Voici un exemple de corps hello de demande de tooour de réponse HTTP hello sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-138">Here is an example of hello body of hello HTTP response tooour backup request.</span></span>

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
> <span data-ttu-id="9ce6a-139">Vous trouverez des messages d’erreur dans la propriété du journal hello Hello réponse HTTP.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-139">Error messages can be found in hello log property of hello HTTP response.</span></span>
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a><span data-ttu-id="9ce6a-140">Planification de sauvegardes automatiques</span><span class="sxs-lookup"><span data-stu-id="9ce6a-140">Schedule automatic backups</span></span>
<span data-ttu-id="9ce6a-141">Dans toobacking d’ajout d’une application à la demande, vous pouvez également planifier une sauvegarde toohappen automatiquement.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-141">In addition toobacking up an app on demand, you can also schedule a backup toohappen automatically.</span></span>

### <a name="set-up-a-new-automatic-backup-schedule"></a><span data-ttu-id="9ce6a-142">Configurer une nouvelle planification de sauvegarde automatique</span><span class="sxs-lookup"><span data-stu-id="9ce6a-142">Set up a new automatic backup schedule</span></span>
<span data-ttu-id="9ce6a-143">tooset une planification de sauvegarde, envoyer un **PUT** demande trop**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config et de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-143">tooset up a backup schedule, send a **PUT** request too**https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup**.</span></span>

<span data-ttu-id="9ce6a-144">Voici les URL hello aspect de notre site Web d’exemple.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-144">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="9ce6a-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span><span class="sxs-lookup"><span data-stu-id="9ce6a-145">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**</span></span>

<span data-ttu-id="9ce6a-146">corps de la demande Hello doit avoir un objet JSON qui spécifie la configuration de la sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-146">hello request body must have a JSON object that specifies hello backup configuration.</span></span> <span data-ttu-id="9ce6a-147">Voici un exemple avec tous les paramètres de hello requis.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-147">Here is an example with all hello required parameters.</span></span>

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
        "enabled": "True", // Must be set tootrue tooenable automatic backups
        "name": “mysitebackup”,
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

<span data-ttu-id="9ce6a-148">Cet exemple configure toobe d’application hello sauvegardé automatiquement tous les sept jours.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-148">This example configures hello app toobe automatically backed up every seven days.</span></span> <span data-ttu-id="9ce6a-149">Hello paramètres **frequencyInterval** et **frequencyUnit** déterminent la fréquence à laquelle hello sauvegardes se produisent.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-149">hello parameters **frequencyInterval** and **frequencyUnit** together determine how often hello backups happen.</span></span> <span data-ttu-id="9ce6a-150">Les valeurs valides de **frequencyUnit** sont **hour** et **day**.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-150">Valid values for **frequencyUnit** are **hour** and **day**.</span></span> <span data-ttu-id="9ce6a-151">Par exemple, tooback installer une application, toutes les 12 heures, définissez frequencyInterval des toohour too12 et frequencyUnit.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-151">For example, tooback up an app every 12 hours, set frequencyInterval too12 and frequencyUnit toohour.</span></span>

<span data-ttu-id="9ce6a-152">Anciennes sauvegardes sont automatiquement supprimés de compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-152">Old backups are automatically removed from hello storage account.</span></span> <span data-ttu-id="9ce6a-153">Vous pouvez contrôler l’ancienneté hello sauvegardes peuvent être en définissant un hello **retentionPeriodInDays** paramètre.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-153">You can control how old hello backups can be by setting hello **retentionPeriodInDays** parameter.</span></span> <span data-ttu-id="9ce6a-154">Si vous souhaitez tooalways ont au moins une sauvegarde enregistrée, quelle que soit l’ancienneté il, **keepAtLeastOneBackup** tootrue.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-154">If you want tooalways have at least one backup saved, regardless of how old it is, set **keepAtLeastOneBackup** tootrue.</span></span>

### <a name="get-hello-automatic-backup-schedule"></a><span data-ttu-id="9ce6a-155">Obtenir la planification de sauvegarde automatique hello</span><span class="sxs-lookup"><span data-stu-id="9ce6a-155">Get hello automatic backup schedule</span></span>
<span data-ttu-id="9ce6a-156">tooget une application de sauvegarde de configuration, envoyer un **POST** toohello URL de demande **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ sites / {nom} / config/sauvegarde/liste**.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-156">tooget an app’s backup configuration, send a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config/backup/list**.</span></span>

<span data-ttu-id="9ce6a-157">URL de Hello pour notre exemple de site est **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-157">hello URL for our example site is **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.</span></span>

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a><span data-ttu-id="9ce6a-158">Obtenir l’état de hello d’une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="9ce6a-158">Get hello status of a backup</span></span>
<span data-ttu-id="9ce6a-159">Selon la taille application hello est, une sauvegarde peut prendre un certain temps toocomplete.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-159">Depending on how large hello app is, a backup may take a while toocomplete.</span></span> <span data-ttu-id="9ce6a-160">Les sauvegardes peuvent également échouer, dépasser le délai d’attente ou n’aboutir que partiellement.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-160">Backups might also fail, time out, or partially succeed.</span></span> <span data-ttu-id="9ce6a-161">état de hello toosee des sauvegardes de toutes les une application, envoyer un **obtenir** toohello URL de demande **https://management.azure.com/subscriptions/ {id d’abonnement} /resourceGroups/ {resource-group-name} /providers/ Microsoft.Web/sites/{name}/backups**.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-161">toosee hello status of all an app’s backups, send a **GET** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups**.</span></span>

<span data-ttu-id="9ce6a-162">état de hello toosee d’une sauvegarde spécifique, envoyer une URL toohello de demande GET **https://management.azure.com/subscriptions/ {{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ sauvegarde-id}**.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-162">toosee hello status of a specific backup, send a GET request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="9ce6a-163">Voici les URL hello aspect de notre site Web d’exemple.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-163">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="9ce6a-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="9ce6a-164">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<span data-ttu-id="9ce6a-165">corps de réponse Hello contient un exemple de toothis similaire d’objet JSON.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-165">hello response body contains a JSON object similar toothis example.</span></span>

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

<span data-ttu-id="9ce6a-166">état Hello d’une sauvegarde est un type énuméré.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-166">hello status of a backup is an enumerated type.</span></span> <span data-ttu-id="9ce6a-167">Voici la liste de tous les états possibles.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-167">Here is every possible state.</span></span>

* <span data-ttu-id="9ce6a-168">0 – InProgress : hello sauvegarde a été démarré mais qu’elle n’est pas encore terminée.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-168">0 – InProgress: hello backup has been started but has not yet completed.</span></span>
* <span data-ttu-id="9ce6a-169">1 – Échec : sauvegarde de hello a échoué.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-169">1 – Failed: hello backup was unsuccessful.</span></span>
* <span data-ttu-id="9ce6a-170">2 – a réussi : hello a été sauvegardée.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-170">2 – Succeeded: hello backup completed successfully.</span></span>
* <span data-ttu-id="9ce6a-171">3 – TimedOut : sauvegarde de hello ne s’est pas terminée dans le temps et a été annulée.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-171">3 – TimedOut: hello backup did not finish in time and was canceled.</span></span>
* <span data-ttu-id="9ce6a-172">4 – créé : demande de sauvegarde hello est mise en attente, mais n’a pas été démarré.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-172">4 – Created: hello backup request is queued but has not been started.</span></span>
* <span data-ttu-id="9ce6a-173">5 – ignoré : sauvegarde de hello n’est pas allé en raison de la planification tooa trop de sauvegardes de déclenchement.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-173">5 – Skipped: hello backup did not proceed due tooa schedule triggering too many backups.</span></span>
* <span data-ttu-id="9ce6a-174">6 – PartiallySucceeded : hello sauvegarde a réussi, mais certains fichiers n’ont pas sauvegardés, car ils ne peuvent pas être lus.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-174">6 – PartiallySucceeded: hello backup succeeded, but some files were not backed up because they could not be read.</span></span> <span data-ttu-id="9ce6a-175">Généralement, cela se produit, car un verrou exclusif est placé dans les fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-175">This usually happens because an exclusive lock was placed on hello files.</span></span>
* <span data-ttu-id="9ce6a-176">7 – DeleteInProgress : hello sauvegarde a été demandée toobe supprimé, mais qu’elle n’a pas encore été supprimée.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-176">7 – DeleteInProgress: hello backup has been requested toobe deleted, but has not yet been deleted.</span></span>
* <span data-ttu-id="9ce6a-177">8 – Échec de la suppression : sauvegarde de hello n’a pas pu être supprimé.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-177">8 – DeleteFailed: hello backup could not be deleted.</span></span> <span data-ttu-id="9ce6a-178">Cela peut se produire car hello URL SAS qui a été de sauvegarde de hello toocreate utilisé a expiré.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-178">This might happen because hello SAS URL that was used toocreate hello backup has expired.</span></span>
* <span data-ttu-id="9ce6a-179">9 – supprimé : sauvegarde de hello a été supprimé avec succès.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-179">9 – Deleted: hello backup was deleted successfully.</span></span>

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a><span data-ttu-id="9ce6a-180">Restauration d’une application à partir d’une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="9ce6a-180">Restore an app from a backup</span></span>
<span data-ttu-id="9ce6a-181">Si votre application a été supprimée, ou si vous souhaitez toorevert votre version précédente de tooa application, vous pouvez restaurer l’application hello à partir d’une sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-181">If your app has been deleted, or if you want toorevert your app tooa previous version, you can restore hello app from a backup.</span></span> <span data-ttu-id="9ce6a-182">tooinvoke une restauration, envoyer un **POST** toohello URL de demande **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ sauvegardes / {backup-id} / restaurer**.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-182">tooinvoke a restore, send a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/restore**.</span></span>

<span data-ttu-id="9ce6a-183">Voici les URL hello aspect de notre site Web d’exemple.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-183">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="9ce6a-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span><span class="sxs-lookup"><span data-stu-id="9ce6a-184">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**</span></span>

<span data-ttu-id="9ce6a-185">Dans le corps de la demande hello, envoyer un objet JSON qui contient les propriétés de hello pour l’opération de restauration hello.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-185">In hello request body, send a JSON object that contains hello properties for hello restore operation.</span></span> <span data-ttu-id="9ce6a-186">Voici un exemple contenant toutes les propriétés requises :</span><span class="sxs-lookup"><span data-stu-id="9ce6a-186">Here is an example containing all required properties:</span></span>

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
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl" // SAS URL toostorage container containing your website backup
    }
}
```

### <a name="restore-tooa-new-app"></a><span data-ttu-id="9ce6a-187">Restaurer tooa nouvelle application</span><span class="sxs-lookup"><span data-stu-id="9ce6a-187">Restore tooa new app</span></span>
<span data-ttu-id="9ce6a-188">Vous pouvez parfois toocreate une application lorsque vous restaurez une sauvegarde, au lieu de remplacer une application déjà existante.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-188">Sometimes you might want toocreate a new app when you restore a backup, instead of overwriting an already existing app.</span></span> <span data-ttu-id="9ce6a-189">toodo, modification demande URL toopoint toohello nouvelle application hello vous souhaitez toocreate et hello **remplacer** propriété hello JSON trop**false**.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-189">toodo this, change hello request URL toopoint toohello new app you want toocreate, and change hello **overwrite** property in hello JSON too**false**.</span></span>

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a><span data-ttu-id="9ce6a-190">Suppression d’une sauvegarde d’application</span><span class="sxs-lookup"><span data-stu-id="9ce6a-190">Delete an app backup</span></span>
<span data-ttu-id="9ce6a-191">Si vous souhaitez que toodelete une sauvegarde, envoyer un **supprimer** toohello URL de demande **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ sites / {nom} /backups/ {backup-id}**.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-191">If you would like toodelete a backup, send a **DELETE** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}**.</span></span>

<span data-ttu-id="9ce6a-192">Voici les URL hello aspect de notre site Web d’exemple.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-192">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="9ce6a-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span><span class="sxs-lookup"><span data-stu-id="9ce6a-193">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**</span></span>

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a><span data-ttu-id="9ce6a-194">Gestion de l’URL SAS d’une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="9ce6a-194">Manage a backup’s SAS URL</span></span>
<span data-ttu-id="9ce6a-195">Azure App Service va essayer de toodelete votre sauvegarde à partir du stockage Azure à l’aide de hello URL SAS qui a été fourni lors de la création de la sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-195">Azure App Service will attempt toodelete your backup from Azure Storage using hello SAS URL that was provided when hello backup was created.</span></span> <span data-ttu-id="9ce6a-196">Si cette URL SAS n’est plus valide, sauvegarde de hello ne peut pas être supprimée via l’API REST de hello.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-196">If this SAS URL is no longer valid, hello backup cannot be deleted through hello REST API.</span></span> <span data-ttu-id="9ce6a-197">Toutefois, vous pouvez mettre à jour hello URL SAS associée à une sauvegarde en envoyant un **POST** toohello URL de demande **https://management.azure.com/subscriptions/ {id d’abonnement} /resourceGroups/ {resource-group-name} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-197">However, you can update hello SAS URL associated with a backup by sending a **POST** request toohello URL **https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.</span></span>

<span data-ttu-id="9ce6a-198">Voici les URL hello aspect de notre site Web d’exemple.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-198">Here is what hello URL looks like for our example website.</span></span> <span data-ttu-id="9ce6a-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span><span class="sxs-lookup"><span data-stu-id="9ce6a-199">**https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**</span></span>

<span data-ttu-id="9ce6a-200">Dans le corps de la demande hello, envoyer un objet JSON qui contient la nouvelle URL de SAS hello.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-200">In hello request body, send a JSON object that contains hello new SAS URL.</span></span> <span data-ttu-id="9ce6a-201">Voici un exemple.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-201">Here is an example.</span></span>

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> <span data-ttu-id="9ce6a-202">Pour des raisons de sécurité, hello QU'URL SAS associée à une sauvegarde n’est pas renvoyé lors de l’envoi d’une demande GET pour une sauvegarde spécifique.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-202">For security reasons, hello SAS URL associated with a backup is not returned when sending a GET request for a specific backup.</span></span> <span data-ttu-id="9ce6a-203">Si vous souhaitez hello tooview URL SAS associée à une sauvegarde, envoyer un toohello de la demande POST même URL ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-203">If you want tooview hello SAS URL associated with a backup, send a POST request toohello same URL above.</span></span> <span data-ttu-id="9ce6a-204">Inclure un objet JSON vide dans le corps de la demande hello.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-204">Include an empty JSON object in hello request body.</span></span> <span data-ttu-id="9ce6a-205">réponse Hello du serveur de hello contient toutes les informations de cette sauvegarde, y compris son URL SAS.</span><span class="sxs-lookup"><span data-stu-id="9ce6a-205">hello response from hello server contains all of that backup’s information, including its SAS URL.</span></span>
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
