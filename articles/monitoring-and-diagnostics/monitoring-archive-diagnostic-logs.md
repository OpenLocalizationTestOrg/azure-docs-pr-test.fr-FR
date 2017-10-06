---
title: aaaArchive les journaux de Diagnostic Azure | Documents Microsoft
description: "Découvrez comment tooarchive votre Azure journaux de Diagnostic pour une rétention à long terme dans un compte de stockage."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 3a55c73f-2ef3-45f3-8956-bcf9c0cb7e05
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem
ms.openlocfilehash: bc9edbd3a649023a728b7fe77130dba2b6e6370d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="archive-azure-diagnostic-logs"></a>Archivage des journaux de diagnostic Azure
Dans cet article, nous montrons comment vous pouvez utiliser hello portail Azure, les PowerShell Cmdlets, CLI, ou placez les API tooarchive votre [des journaux de diagnostic Azure](monitoring-overview-of-diagnostic-logs.md) dans un compte de stockage. Cette option est utile si vous souhaitez que tooretain journaux de votre diagnostic avec une stratégie de rétention pour l’audit, d’analyse statique ou de sauvegarde. compte de stockage Hello n’a pas de toobe dans hello même abonnement en tant que ressource hello générant des journaux tant qu’utilisateur hello configure hello paramètre a des abonnements de tooboth accès RBAC appropriés.

## <a name="prerequisites"></a>Composants requis
Avant de commencer, vous devez trop[créer un compte de stockage](../storage/storage-create-storage-account.md) toowhich, vous pouvez archiver vos journaux de diagnostic. Nous vous recommandons vivement de ne pas utiliser un compte de stockage existant qui comporte des données d’autres, non suivi stockées afin que vous pouvez mieux contrôler les accès toomonitoring données. Toutefois, si vous archivez également votre journal d’activité et le compte de stockage tooa métriques des diagnostics, il peut être judicieux toouse ce compte de stockage pour vos journaux de diagnostic ainsi tookeep toutes les données d’analyse dans un emplacement central. compte de stockage Hello que vous utilisez doit être un compte de stockage polyvalentes, pas un compte de stockage d’objets blob.

## <a name="diagnostic-settings"></a>Paramètres de diagnostic
tooarchive votre diagnostic se connecte à l’aide d’une des méthodes hello ci-dessous, vous définissez un **paramètre de diagnostic** pour une ressource particulière. Un paramètre de diagnostic pour une ressource définit les catégories de hello des journaux et données de mesure envoyées destination tooa (compte de stockage, espace de noms de concentrateurs d’événements ou Analytique de journal). Il définit également la stratégie de rétention hello (nombre de jours tooretain) pour les événements de chaque catégorie de journaux et les données métriques stockées dans un compte de stockage. Si une stratégie de rétention est définie à toozero, événements de cette catégorie de journal sont stockés indéfiniment (c'est-à-dire toosay, indéfiniment). Une stratégie de rétention peut également être définie sur n’importe quel nombre de jours entre 1 et 2147483647. [Vous trouverez plus d’informations sur les paramètres de diagnostic ici](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings). Stratégies de rétention sont appliquées par jour, donc à hello fin d’une journée (UTC), consigne un jour hello qui est désormais au-delà de la stratégie de rétention hello seront supprimés. Par exemple, si vous aviez une stratégie de rétention d’un jour, au début de hello du jour hello aujourd'hui hello des journaux de hello avant-hier seraient supprimés

## <a name="archive-diagnostic-logs-using-hello-portal"></a>Archive des journaux de diagnostic à l’aide du portail de hello
1. Dans le portail de hello, accédez tooAzure moniteur, puis cliquez sur **les paramètres de Diagnostic**

    ![Section Surveillance d’Azure Monitor](media/monitoring-archive-diagnostic-logs/diagnostic-settings-blade.png)

2. Vous pouvez également filtrer la liste de hello par type de ressource ou le groupe de ressources, puis cliquez sur ressources hello pour laquelle vous aimeriez tooset un paramètre de diagnostic.

3. Si aucun paramètre n’existe sur la ressource hello que vous avez sélectionné, vous êtes invité à toocreate un paramètre. Cliquez sur « Activer les diagnostics ».

   ![Ajouter le paramètre de diagnostic - aucun paramètre existant](media/monitoring-archive-diagnostic-logs/diagnostic-settings-none.png)

   S’il existe des paramètres existants sur les ressources hello, vous verrez une liste de paramètres déjà configuré sur cette ressource. Cliquez sur « Ajouter le paramètre de diagnostic ».

   ![Ajouter le paramètre de diagnostic - paramètres existants](media/monitoring-archive-diagnostic-logs/diagnostic-settings-multiple.png)

3. Donnez à votre définition d’un nom et la case hello pour **exporter tooStorage compte**, puis sélectionnez un compte de stockage. Si vous le souhaitez, vous pouvez définir un nombre de jours tooretain ces journaux à l’aide de hello **rétention (jours)** curseurs. Une durée de rétention de zéro jours stocke les journaux hello indéfiniment.
   
   ![Ajouter le paramètre de diagnostic - paramètres existants](media/monitoring-archive-diagnostic-logs/diagnostic-settings-configure.png)
    
4. Cliquez sur **Enregistrer**.

Après quelques instants, le nouveau paramètre de hello s’affiche dans la liste des paramètres pour cette ressource, et les journaux de diagnostic sont archivées toothat stockage compte dès que les nouvelles données d’événement sont générées.

## <a name="archive-diagnostic-logs-via-azure-powershell"></a>Archivage des journaux de diagnostic à l’aide d’Azure PowerShell
```
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg -StorageAccountId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Categories networksecuritygroupevent,networksecuritygrouprulecounter -Enabled $true -RetentionEnabled $true -RetentionInDays 90
```

| Propriété | Requis | Description |
| --- | --- | --- |
| ResourceId |Oui |ID de ressource de la ressource hello sur lequel vous souhaitez tooset un paramètre de diagnostic. |
| StorageAccountId |Non |ID de ressource de hello toowhich de compte de stockage des journaux de Diagnostic doit être enregistré. |
| Catégories |Non |Liste de séparées par des virgules des tooenable de catégories de journal. |
| Activé |OUI |Valeur booléenne indiquant si les diagnostics sont activés ou désactivés pour cette ressource. |
| RetentionEnabled |Non |Valeur booléenne indiquant si une stratégie de rétention est activée pour cette ressource. |
| RetentionInDays |Non |Nombre de jours pendant lesquels les événements doivent être conservés, compris entre 1 et 2147483647. Une valeur égale à zéro stocke les journaux hello indéfiniment. |

## <a name="archive-diagnostic-logs-via-hello-cross-platform-cli"></a>Journaux de diagnostic archive via hello Cross-Platform CLI
```
azure insights diagnostic set --resourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg --storageId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage –categories networksecuritygroupevent,networksecuritygrouprulecounter --enabled true
```

| Propriété | Requis | Description |
| --- | --- | --- |
| ResourceId |Oui |ID de ressource de la ressource hello sur lequel vous souhaitez tooset un paramètre de diagnostic. |
| storageId |Non |ID de ressource de journaux de diagnostic de toowhich hello compte de stockage doit être enregistré. |
| Catégories |Non |Liste de séparées par des virgules des tooenable de catégories de journal. |
| Activé |OUI |Valeur booléenne indiquant si les diagnostics sont activés ou désactivés pour cette ressource. |

## <a name="archive-diagnostic-logs-via-hello-rest-api"></a>Archive des journaux de diagnostic via l’API REST de hello
[Consultez ce document](https://docs.microsoft.com/rest/api/monitor/servicediagnosticsettings) pour plus d’informations sur la façon dont vous pouvez configurer un paramètre de diagnostic à l’aide de hello API REST du moniteur de Azure.

## <a name="schema-of-diagnostic-logs-in-hello-storage-account"></a>Schéma des journaux de diagnostic dans le compte de stockage hello
Une fois que vous avez configuré d’archivage, un conteneur de stockage est créé dans le compte de stockage hello dès qu’un événement se produit dans une des catégories du journal hello que vous avez activé. BLOB Hello conteneur hello suivez hello même format entre les journaux de Diagnostic et hello journal d’activité. structure Hello de ces objets BLOB est la suivante :

> insights-logs-{nom de la catégorie de journal}/resourceId=/SUBSCRIPTIONS/{ID d’abonnement}/RESOURCEGROUPS/{nom du groupe de ressources}/PROVIDERS/{nom du fournisseur de ressources}/{type de ressource}/{nom de la ressource}/y={année, quatre chiffres}/m={mois, deux chiffres}/d={jour, deux chiffres}/h={heure, deux chiffres, format 24 h}/m=00/PT1H.json
> 
> 

Ou, plus simplement,

> insights-logs-{nom de la catégorie de journal}/resourceId=/{ID de la ressource}/y={année, quatre chiffres}/m={mois, deux chiffres}/d={jour, deux chiffres}/h={heure, deux chiffres, format 24 h}/m=00/PT1H.json
> 
> 

Voici un exemple de nom d’objet blob :

> insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json
> 
> 

Chaque objet blob PT1H.json contient un objet blob de JSON d’événements qui se sont produites dans heure hello spécifié dans l’URL de blob hello (par exemple, h = 12). Pendant hello heure actuelle, les événements sont ajoutés toohello PT1H.json fichier qu’ils se produisent. valeur de minute de Hello (m = 00) est toujours 00, étant donné que les événements du journal de diagnostics sont divisées en objets BLOB individuels par heure.

Dans le fichier de PT1H.json hello, chaque événement est stocké dans le tableau « enregistrements de hello », sous ce format :

```
{
    "records": [
        {
            "time": "2016-07-01T00:00:37.2040000Z",
            "systemId": "46cdbb41-cb9c-4f3d-a5b4-1d458d827ff1",
            "category": "NetworkSecurityGroupRuleCounter",
            "resourceId": "/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/TESTNSG",
            "operationName": "NetworkSecurityGroupCounters",
            "properties": {
                "vnetResourceGuid": "{12345678-9012-3456-7890-123456789012}",
                "subnetPrefix": "10.3.0.0/24",
                "macAddress": "000123456789",
                "ruleName": "/subscriptions/ s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg/securityRules/default-allow-rdp",
                "direction": "In",
                "type": "allow",
                "matchedConnections": 1988
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
| category |Catégorie du journal des événements de hello. |
| properties |Jeu de `<Key, Value>` paires (c'est-à-dire, Dictionary) hello décrivant les événements hello. |

> [!NOTE]
> propriétés de Hello et l’utilisation de ces propriétés peuvent varier en fonction de la ressource de hello.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* [Télécharger des objets blob pour analyse](../storage/storage-dotnet-how-to-use-blobs.md)
* [Flux diagnostic enregistre l’espace de noms tooan concentrateurs d’événements](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [En savoir plus sur les journaux de diagnostic](monitoring-overview-of-diagnostic-logs.md)
