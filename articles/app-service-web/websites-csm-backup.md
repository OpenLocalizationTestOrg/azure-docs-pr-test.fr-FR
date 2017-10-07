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
# <a name="use-rest-tooback-up-and-restore-app-service-apps"></a>Utilisez reste tooback et restaurer des applications de Service d’applications
> [!div class="op_single_selector"]
> * [PowerShell](../app-service/app-service-powershell-backup.md)
> * [API REST](websites-csm-backup.md)
> 
> 

[applications App Service](https://azure.microsoft.com/services/app-service/web/) peuvent être sauvegardées en tant qu’objets blob dans Azure Storage. sauvegarde de Hello peut également contenir des bases de données de l’application hello. Si l’application hello n’est jamais accidentellement, ou si hello application besoins toobe restaurer la version précédente de tooa, elle peut être restaurée à partir d’une sauvegarde précédente. Les sauvegardes peuvent être effectuées à tout moment à la demande, ou être planifiées à des intervalles appropriés.

Cet article explique comment toobackup demandes et restauration une application avec une API RESTful. Si vous souhaitez toocreate et gérer les sauvegardes d’application sous la forme de hello portail Azure, consultez [sauvegardez une application web dans Azure App Service](web-sites-backup.md)

<a name="gettingstarted"></a>

## <a name="getting-started"></a>Mise en route
demande de toosend REST, vous devez tooknow de votre application **nom**, **groupe de ressources**, et **id d’abonnement**. Ces informations sont accessibles en cliquant sur votre application Bonjour **du Service d’applications** Panneau de hello [portail Azure](https://portal.azure.com). Pour obtenir des exemples hello dans cet article, nous examinons la configuration du site Web hello **backuprestoreapiexamples.azurewebsites.net**. Il est stocké dans le groupe de ressources par défaut-Web-WestUS hello et est en cours d’exécution sur un abonnement par hello ID 00001111-2222-3333-4444-555566667777.

![Informations de l’exemple de site web][SampleWebsiteInformation]

<a name="backup-restore-rest-api"></a>

## <a name="backup-and-restore-rest-api"></a>API REST de sauvegarde et de restauration
Nous allons maintenant aborder plusieurs exemples montrant comment toouse hello toobackup de l’API REST et restauration d’une application. Chaque exemple inclut une URL et un corps de requête HTTP. Hello, exemple d’URL contient des espaces réservés encapsulées dans des accolades, par exemple {id d’abonnement}. Remplacez les espaces réservés de hello avec les informations correspondantes de hello pour votre application. Pour référence, voici une explication de chaque espace réservé qui apparaît dans les URL d’exemple hello.

* id d’abonnement : ID de l’application hello contenant de hello abonnement Azure
* Resource-group-name : nom de l’application de conteneur hello hello ressource groupe
* nom : nom de l’application hello
* sauvegarde-id : ID de la sauvegarde d’application hello

Pour une documentation complète hello Hello API, y compris plusieurs paramètres facultatifs qui peuvent être inclus dans la demande HTTP de hello, consultez hello [Explorateur de ressources Azure](https://resources.azure.com/).

<a name="backup-on-demand"></a>

## <a name="backup-an-app-on-demand"></a>Sauvegarde d’une application à la demande
tooback installer une application immédiatement, envoyer un **POST** demande trop**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ sauvegarde /**.

URL de hello ressemble à ceci à l’aide de notre site Web d’exemple. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backup/**

Fournissez un objet JSON dans le corps de hello de votre toospecify demande le toostore de toouse de compte de stockage hello sauvegarde. objet JSON de Hello doit avoir une propriété nommée **storageAccountUrl**, lequel contient un [URL SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) octroi du conteneur de stockage Azure toohello un accès en écriture qui contient des objets blob de sauvegarde hello. Si vous souhaitez tooback vos bases de données, vous devez également fournir une liste contenant les noms de hello, les types et les chaînes de connexion de hello toobe de bases de données sauvegardées.

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

Une sauvegarde de l’application hello commence immédiatement lorsque hello demande est reçue. processus de sauvegarde Hello peut prendre un toocomplete beaucoup de temps. Hello réponse HTTP contient un ID que vous pouvez utiliser dans un autre état hello toosee de demande de sauvegarde de hello. Voici un exemple de corps hello de demande de tooour de réponse HTTP hello sauvegarde.

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
> Vous trouverez des messages d’erreur dans la propriété du journal hello Hello réponse HTTP.
> 
> 

<a name="schedule-automatic-backups"></a>

## <a name="schedule-automatic-backups"></a>Planification de sauvegardes automatiques
Dans toobacking d’ajout d’une application à la demande, vous pouvez également planifier une sauvegarde toohappen automatiquement.

### <a name="set-up-a-new-automatic-backup-schedule"></a>Configurer une nouvelle planification de sauvegarde automatique
tooset une planification de sauvegarde, envoyer un **PUT** demande trop**https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/config et de sauvegarde**.

Voici les URL hello aspect de notre site Web d’exemple. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup**

corps de la demande Hello doit avoir un objet JSON qui spécifie la configuration de la sauvegarde hello. Voici un exemple avec tous les paramètres de hello requis.

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

Cet exemple configure toobe d’application hello sauvegardé automatiquement tous les sept jours. Hello paramètres **frequencyInterval** et **frequencyUnit** déterminent la fréquence à laquelle hello sauvegardes se produisent. Les valeurs valides de **frequencyUnit** sont **hour** et **day**. Par exemple, tooback installer une application, toutes les 12 heures, définissez frequencyInterval des toohour too12 et frequencyUnit.

Anciennes sauvegardes sont automatiquement supprimés de compte de stockage hello. Vous pouvez contrôler l’ancienneté hello sauvegardes peuvent être en définissant un hello **retentionPeriodInDays** paramètre. Si vous souhaitez tooalways ont au moins une sauvegarde enregistrée, quelle que soit l’ancienneté il, **keepAtLeastOneBackup** tootrue.

### <a name="get-hello-automatic-backup-schedule"></a>Obtenir la planification de sauvegarde automatique hello
tooget une application de sauvegarde de configuration, envoyer un **POST** toohello URL de demande **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ sites / {nom} / config/sauvegarde/liste**.

URL de Hello pour notre exemple de site est **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/config/backup/list**.

<a name="get-backup-status"></a>

## <a name="get-hello-status-of-a-backup"></a>Obtenir l’état de hello d’une sauvegarde
Selon la taille application hello est, une sauvegarde peut prendre un certain temps toocomplete. Les sauvegardes peuvent également échouer, dépasser le délai d’attente ou n’aboutir que partiellement. état de hello toosee des sauvegardes de toutes les une application, envoyer un **obtenir** toohello URL de demande **https://management.azure.com/subscriptions/ {id d’abonnement} /resourceGroups/ {resource-group-name} /providers/ Microsoft.Web/sites/{name}/backups**.

état de hello toosee d’une sauvegarde spécifique, envoyer une URL toohello de demande GET **https://management.azure.com/subscriptions/ {{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/backups/ sauvegarde-id}**.

Voici les URL hello aspect de notre site Web d’exemple. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

corps de réponse Hello contient un exemple de toothis similaire d’objet JSON.

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

état Hello d’une sauvegarde est un type énuméré. Voici la liste de tous les états possibles.

* 0 – InProgress : hello sauvegarde a été démarré mais qu’elle n’est pas encore terminée.
* 1 – Échec : sauvegarde de hello a échoué.
* 2 – a réussi : hello a été sauvegardée.
* 3 – TimedOut : sauvegarde de hello ne s’est pas terminée dans le temps et a été annulée.
* 4 – créé : demande de sauvegarde hello est mise en attente, mais n’a pas été démarré.
* 5 – ignoré : sauvegarde de hello n’est pas allé en raison de la planification tooa trop de sauvegardes de déclenchement.
* 6 – PartiallySucceeded : hello sauvegarde a réussi, mais certains fichiers n’ont pas sauvegardés, car ils ne peuvent pas être lus. Généralement, cela se produit, car un verrou exclusif est placé dans les fichiers hello.
* 7 – DeleteInProgress : hello sauvegarde a été demandée toobe supprimé, mais qu’elle n’a pas encore été supprimée.
* 8 – Échec de la suppression : sauvegarde de hello n’a pas pu être supprimé. Cela peut se produire car hello URL SAS qui a été de sauvegarde de hello toocreate utilisé a expiré.
* 9 – supprimé : sauvegarde de hello a été supprimé avec succès.

<a name="restore-app"></a>

## <a name="restore-an-app-from-a-backup"></a>Restauration d’une application à partir d’une sauvegarde
Si votre application a été supprimée, ou si vous souhaitez toorevert votre version précédente de tooa application, vous pouvez restaurer l’application hello à partir d’une sauvegarde. tooinvoke une restauration, envoyer un **POST** toohello URL de demande **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/sites/{name}/ sauvegardes / {backup-id} / restaurer**.

Voici les URL hello aspect de notre site Web d’exemple. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/restore**

Dans le corps de la demande hello, envoyer un objet JSON qui contient les propriétés de hello pour l’opération de restauration hello. Voici un exemple contenant toutes les propriétés requises :

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

### <a name="restore-tooa-new-app"></a>Restaurer tooa nouvelle application
Vous pouvez parfois toocreate une application lorsque vous restaurez une sauvegarde, au lieu de remplacer une application déjà existante. toodo, modification demande URL toopoint toohello nouvelle application hello vous souhaitez toocreate et hello **remplacer** propriété hello JSON trop**false**.

<a name="delete-app-backup"></a>

## <a name="delete-an-app-backup"></a>Suppression d’une sauvegarde d’application
Si vous souhaitez que toodelete une sauvegarde, envoyer un **supprimer** toohello URL de demande **https://management.azure.com/subscriptions/ {subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Web/ sites / {nom} /backups/ {backup-id}**.

Voici les URL hello aspect de notre site Web d’exemple. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1**

<a name="manage-sas-url"></a>

## <a name="manage-a-backups-sas-url"></a>Gestion de l’URL SAS d’une sauvegarde
Azure App Service va essayer de toodelete votre sauvegarde à partir du stockage Azure à l’aide de hello URL SAS qui a été fourni lors de la création de la sauvegarde hello. Si cette URL SAS n’est plus valide, sauvegarde de hello ne peut pas être supprimée via l’API REST de hello. Toutefois, vous pouvez mettre à jour hello URL SAS associée à une sauvegarde en envoyant un **POST** toohello URL de demande **https://management.azure.com/subscriptions/ {id d’abonnement} /resourceGroups/ {resource-group-name} / providers/Microsoft.Web/sites/{name}/backups/{backup-id}/list**.

Voici les URL hello aspect de notre site Web d’exemple. **https://management.azure.com/subscriptions/00001111-2222-3333-4444-555566667777/resourceGroups/Default-Web-WestUS/providers/Microsoft.Web/sites/backuprestoreapiexamples/backups/1/list**

Dans le corps de la demande hello, envoyer un objet JSON qui contient la nouvelle URL de SAS hello. Voici un exemple.

```
{
    "properties":
    {
        "storageAccountUrl": "https://account.blob.core.windows.net/backups?sv=2015-02-21&sr=c&sig=DzlkBl7h32C8qCv%2BifdBRxE63r4iv0kZ9L7E0qP16sY%3D&se=2016-09-15T22%3A46%3A54Z&sp=rwdl"
    }
}
```

> [!NOTE]
> Pour des raisons de sécurité, hello QU'URL SAS associée à une sauvegarde n’est pas renvoyé lors de l’envoi d’une demande GET pour une sauvegarde spécifique. Si vous souhaitez hello tooview URL SAS associée à une sauvegarde, envoyer un toohello de la demande POST même URL ci-dessus. Inclure un objet JSON vide dans le corps de la demande hello. réponse Hello du serveur de hello contient toutes les informations de cette sauvegarde, y compris son URL SAS.
> 
> 

<!-- IMAGES -->
[SampleWebsiteInformation]: ./media/websites-csm-backup/01siteconfig.png
