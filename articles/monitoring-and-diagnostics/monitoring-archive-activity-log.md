---
title: "aaaArchive hello journal des activités Azure | Documents Microsoft"
description: "Découvrez comment tooarchive vos activités Windows Azure du journal pour la rétention à long terme dans un compte de stockage."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 58c6d3a3a31398287f66f76999d48f2942ab5109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="archive-hello-azure-activity-log"></a>Archiver hello journal des activités Azure
Dans cet article, nous montrons comment vous pouvez utiliser hello portail Azure, les PowerShell Cmdlets ou CLI de Cross-Platform tooarchive votre [ **journal des activités Azure** ](monitoring-overview-activity-logs.md) dans un compte de stockage. Cette option est utile si vous souhaitez que tooretain plus de 90 jours (avec un contrôle total sur la stratégie de rétention hello) pour votre journal des activités d’audit, analyse statique, ou de sauvegarde. Si vous devez uniquement tooretain vos événements pendant 90 jours ou moins vous est inutile tooset archivage tooa compte de stockage, puisque les événements de journal d’activité sont conservés dans hello plateforme Azure pendant 90 jours sans l’archivage.

## <a name="prerequisites"></a>Composants requis
Avant de commencer, vous devez trop[créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) toowhich, vous pouvez archiver le journal d’activité. Nous vous recommandons vivement de ne pas utiliser un compte de stockage existant qui comporte des données d’autres, non suivi stockées afin que vous pouvez mieux contrôler les accès toomonitoring données. Toutefois, si vous archivez également les journaux de Diagnostic et de compte de stockage tooa de métriques, il peut être judicieux toouse ce compte de stockage pour votre activité du journal ainsi tookeep toutes les données d’analyse dans un emplacement central. compte de stockage Hello que vous utilisez doit être un compte de stockage polyvalentes, pas un compte de stockage d’objets blob. compte de stockage Hello n’a pas de toobe dans hello même abonnement que l’abonnement hello générant des journaux tant qu’utilisateur hello configure hello paramètre a des abonnements de tooboth accès RBAC appropriés.

## <a name="log-profile"></a>Profil de journal
tooarchive hello journal d’activité à l’aide d’une des méthodes hello ci-dessous, vous définissez hello **profil journal** pour un abonnement. définit le type hello d’événements qui sont stockés ou transmis en continu Hello profil du journal et hello sorties : concentrateur compte et/ou les événements de stockage. Il définit également la stratégie de rétention hello (nombre de jours tooretain) pour les événements stockés dans un compte de stockage. Si la stratégie de rétention hello a la valeur toozero, les événements sont stockés indéfiniment. Dans le cas contraire, cela peut être valeur tooany compris entre 1 et 2147483647. Stratégies de rétention sont appliquées par jour, donc à hello fin d’une journée (UTC), consigne un jour hello qui est désormais au-delà de la stratégie de rétention hello seront supprimés. Par exemple, si vous aviez une stratégie de rétention d’un jour, au début de hello du jour hello aujourd'hui hello les journaux à partir de hello avant-hier seraient supprimés. [Vous trouverez plus d’informations sur les profils de journal ici](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile). 

## <a name="archive-hello-activity-log-using-hello-portal"></a>Archive hello journal d’activité à l’aide du portail de hello
1. Dans le portail hello, cliquez sur hello **le journal d’activité** lien de navigation de gauche hello. Si vous ne voyez pas un lien pour hello journal d’activité, cliquez sur hello **plus Services** lier tout d’abord.
   
    ![Accédez Panneau de journal tooActivity](media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. Haut hello du Panneau de hello, cliquez sur **exporter**.
   
    ![Cliquez sur le bouton Exporter de hello](media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. Dans le panneau hello qui s’affiche, cochez la case hello **exporter le compte de stockage tooa** et sélectionnez un compte de stockage.
   
    ![Créer un compte de stockage](media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. À l’aide du curseur de hello ou zone de texte, de définir un nombre de jours pour lesquels les événements du journal d’activité doivent être conservées dans votre compte de stockage. Si vous préférez toohave vos données persistant dans le compte de stockage hello indéfiniment, ce nombre toozero.
5. Cliquez sur **Enregistrer**.

## <a name="archive-hello-activity-log-via-powershell"></a>Archiver hello journal d’activité via PowerShell
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| Propriété | Requis | Description |
| --- | --- | --- |
| StorageAccountId |Non |ID de ressource de hello toowhich de compte de stockage des journaux d’activité doit être enregistré. |
| Emplacements |Oui |Liste de séparées par des virgules des régions pour lequel vous souhaitez que les événements du journal d’activité toocollect. Vous pouvez afficher une liste de toutes les régions [en visitant cette page](https://azure.microsoft.com/en-us/regions) ou à l’aide de [hello API REST de gestion Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx). |
| RetentionInDays |OUI |Nombre de jours pendant lesquels les événements doivent être conservés, compris entre 1 et 2147483647. Une valeur égale à zéro stocke les journaux hello indéfiniment (indéfiniment). |
| Catégories |OUI |Liste séparée par des virgules des catégories d’événements qui doivent être collectées. Les valeurs possibles sont Write, Delete et Action. |

## <a name="archive-hello-activity-log-via-cli"></a>Archiver le journal d’activité via l’interface CLI de hello
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| Propriété | Requis | Description |
| --- | --- | --- |
| name |OUI |Nom de votre profil de journal. |
| storageId |Non |ID de ressource de hello toowhich de compte de stockage des journaux d’activité doit être enregistré. |
| emplacements |Oui |Liste de séparées par des virgules des régions pour lequel vous souhaitez que les événements du journal d’activité toocollect. Vous pouvez afficher une liste de toutes les régions [en visitant cette page](https://azure.microsoft.com/en-us/regions) ou à l’aide de [hello API REST de gestion Azure](https://msdn.microsoft.com/library/azure/gg441293.aspx). |
| RetentionInDays |OUI |Nombre de jours pendant lesquels les événements doivent être conservés, compris entre 1 et 2147483647. Une valeur égale à zéro stockera les journaux hello indéfiniment (indéfiniment). |
| Catégories |OUI |Liste séparée par des virgules des catégories d’événements qui doivent être collectées. Les valeurs possibles sont Write, Delete et Action. |

## <a name="storage-schema-of-hello-activity-log"></a>Schéma de stockage de hello journal d’activité
Une fois que vous avez configuré d’archivage, un conteneur de stockage sera créé dans le compte de stockage hello dès qu’un événement du journal d’activité se produit. BLOB Hello conteneur hello suivez hello même format entre hello journal d’activité et des journaux de Diagnostic. structure Hello de ces objets BLOB est la suivante :

> insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{ID de l’abonnement}/y={année, quatre chiffes}/m={mois, deux chiffres}/d={jour, deux chiffres}/h={heure, deux chiffres, format 24 heures}/m=00/PT1H.json
> 
> 

Voici un exemple de nom d’objet blob :

> insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json
> 
> 

Chaque objet blob PT1H.json contient un objet blob de JSON d’événements qui se sont produites dans heure hello spécifié dans l’URL de blob hello (par exemple, h = 12). Pendant hello heure actuelle, les événements sont ajoutés toohello PT1H.json fichier qu’ils se produisent. valeur de minute de Hello (m = 00) est toujours 00, étant donné que les événements du journal d’activité sont divisées en objets BLOB individuels par heure.

Dans le fichier de PT1H.json hello, chaque événement est stocké dans le tableau « enregistrements de hello », sous ce format :

```
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
                "claims": {
                    "aud": "https://management.core.windows.net/",
                    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
                    "iat": "1421876371",
                    "nbf": "1421876371",
                    "exp": "1421880271",
                    "ver": "1.0",
                    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
                    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
                    "puid": "20030000801A118C",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
                    "name": "John Smith",
                    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
                    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
                    "appidacr": "2",
                    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
                    "http://schemas.microsoft.com/claims/authnclassreference": "1"
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
            }
        }
    ]
}
```


| Nom de l'élément | Description |
| --- | --- |
| time |Horodatage lors de l’événement de hello a été généré par hello du traitement du service Azure hello demande événement hello correspondant. |
| resourceId |ID de ressource de hello affectées les ressources. |
| operationName |Nom de l’opération de hello. |
| category |Catégorie d’action de hello, par exemple. Écriture, Lecture, Action. |
| resultType |Bonjour type du résultat de hello, par exemple. Réussite, échec, démarrage |
| resultSignature |Varie selon le type de ressource hello. |
| durationMS |Durée de l’opération de hello en millisecondes |
| callerIpAddress |Adresse IP de l’utilisateur de hello qui a effectué les opération hello, revendication UPN ou revendication SPN basée sur la disponibilité. |
| correlationId |Généralement, un GUID au format de chaîne hello. Les événements qui partagent un ID de corrélation appartiennent toohello même action uber. |
| identité |L’objet blob JSON décrivant les revendications et l’autorisation de hello. |
| autorisation |Objet BLOB de propriétés RBAC de l’événement de hello. Inclut généralement les propriétés « action », « rôle » et « portée » hello. |
| level |Niveau d’événement de hello. Une des valeurs suivantes de hello : « Critiques », « Erreur », « Avertissement », « Information » et « Commentaires » |
| location |Région dans un emplacement hello qui s’est produite (ou global). |
| properties |Jeu de `<Key, Value>` paires (c'est-à-dire, Dictionary) hello décrivant les événements hello. |

> [!NOTE]
> propriétés de Hello et l’utilisation de ces propriétés peuvent varier en fonction de la ressource de hello.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* [Télécharger des objets blob pour analyse](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [Flux tooEvent de journal d’activité hello concentrateurs](monitoring-stream-activity-logs-event-hubs.md)
* [En savoir plus sur hello journal d’activité](monitoring-overview-activity-logs.md)

