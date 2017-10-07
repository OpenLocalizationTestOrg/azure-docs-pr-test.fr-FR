---
title: recherche de journal Analytique aaaLog API REST | Documents Microsoft
description: "Ce guide fournit un didacticiel de base qui décrit comment vous pouvez utiliser hello Analytique de journal rechercher l’API REST Bonjour Operations Management Suite (OMS) et fournit des exemples qui illustrent la façon dont les commandes de hello toouse."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: b4e9ebe8-80f0-418e-a855-de7954668df7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: dafe5eeb8cc11a339f2cbf78cec657e344d87cac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-log-search-rest-api"></a>API REST de recherche de journal Log Analytics
Ce guide fournit un didacticiel de base, y compris des exemples, vous pouvez utiliser hello journal Analytique recherche REST API. Analytique de journal fait partie de hello Operations Management Suite (OMS).

> [!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis vous devez continuer de langage de requête hérité hello toouse avec les API de recherche de journal hello comme décrit dans cet article.  Une nouvelle API sera disponible pour les espaces de travail mis à niveau et mise à jour des hello documentation à ce moment-là. 

> [!NOTE]
> Analytique de journal s’appelait auparavant Operational Insights, c’est pourquoi il est le nom hello utilisé dans le fournisseur de ressources hello.
>
>

## <a name="overview-of-hello-log-search-rest-api"></a>Vue d’ensemble de hello API REST de recherche journal
Hello API REST de journal Analytique Search est RESTful et est accessible via hello API Azure Resource Manager. Cet article fournit des exemples d’accès aux API hello via [ARMClient](https://github.com/projectkudu/ARMClient), un outil de ligne de commande open source qui simplifie l’appel hello API Azure Resource Manager. utilisation de Hello d’ARMClient est une des nombreuses options de tooaccess hello API de recherche Analytique de journal. Une autre option est un module d’Azure PowerShell hello toouse pour OperationalInsights, qui inclut des applets de commande pour l’accès à la recherche. Grâce à ces outils, vous pouvez utiliser des espaces de travail hello API Azure Resource Manager toomake appelle tooOMS et exécuter des commandes de recherche de. Hello API génère des résultats de recherche au format JSON, ce qui vous toouse résultats de la recherche hello de différentes façons par programme.

Bonjour Azure Resource Manager peut être utilisé via une [bibliothèque pour .NET](https://msdn.microsoft.com/library/azure/dn910477.aspx) et hello [API REST](https://msdn.microsoft.com/library/azure/mt163658.aspx). toolearn plus, consulter les pages web hello lié.

> [!NOTE]
> Si vous utilisez une commande d’agrégation, telles que `|measure count()` ou `distinct`, chaque appel toosearch peut retourner au maximum 500 000 enregistrements. Les recherches qui n’incluent pas une commande d’agrégation renvoient jusqu'à 5 000 enregistrements.
>
>

## <a name="basic-log-analytics-search-rest-api-tutorial"></a>Didacticiel de base sur l’API de recherche de journal de Log Analytics
### <a name="toouse-armclient"></a>toouse ARMClient
1. Installez [Chocolatey](https://chocolatey.org/)(gestionnaire de packages open source pour Windows). Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur, puis exécutez hello de commande suivante :

    ```
    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
    ```
2. Installez ARMClient en exécutant hello de commande suivante :

    ```
    choco install armclient
    ```

### <a name="tooperform-a-search-using-armclient"></a>tooperform une recherche à l’aide d’ARMClient
1. Connectez-vous à l’aide de votre compte Microsoft, ou de votre compte professionnel ou scolaire :

    ```
    armclient login
    ```

    Une connexion réussie répertorie tous les abonnements qui sont associés toohello compte donné :

    ```
    PS C:\Users\SampleUserName> armclient login
    Welcome YourEmail@ORG.com (Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz)
    User: YourEmail@ORG.com, Tenant: zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz (Example org)
    There are 3 subscriptions
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 1)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 2)
    Subscription xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx (Example Name 3)
    ```
2. Obtenir les espaces de travail hello Operations Management Suite :

    ```
    armclient get /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces?api-version=2015-03-20
    ```

    Un appel Get affiche que tous les espaces de travail lié toohello abonnement :

    ```
    {
    "value": [
    {
      "properties": {
    "source": "External",
    "customerId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "portalUrl": "https://eus.login.mms.microsoft.com/SignIn.aspx?returnUrl=https%3a%2f%2feus.mms.microsoft.com%2fMain.aspx%3fcid%xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
      },
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/{WORKSPACE NAME}",
      "name": "{WORKSPACE NAME}",
      "type": "Microsoft.OperationalInsights/workspaces",
      "location": "East US"
       ]
    }
    ```
3. Créez votre variable de recherche :

    ```
    $mySearch = "{ 'top':150, 'query':'Error'}";
    ```
4. Lancez une recherche à l’aide de votre nouvelle variable de recherche :

    ```
    armclient post /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{WORKSPACE NAME}/search?api-version=2015-03-20 $mySearch
    ```

## <a name="log-analytics-search-rest-api-reference-examples"></a>Exemples de référence de l’API REST de recherche Log Analytics
Hello suivant exemples vous montrent comment vous pouvez utiliser les API de recherche de hello.

### <a name="search---actionread"></a>Recherche - Action/lecture
**Exemple d’URL :**

```
    /subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search?api-version=2015-03-20
```

**Requête :**

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```
Hello tableau suivant décrit les propriétés de hello qui sont disponibles.

| **Propriété** | **Description** |
| --- | --- |
| top |nombre maximal de Hello de tooreturn de résultats. |
| highlight |Contient des pré- et post-paramètres, utilisés généralement pour mettre en surbrillance les champs de correspondance |
| pre |Préfixes hello donné champs tooyour mis en correspondance de chaîne. |
| post |Ajoute hello donné champs tooyour mis en correspondance de chaîne. |
| query |requête de recherche Hello utilisé toocollect et retourner des résultats. |
| start |début de Hello hello de fenêtre de temps de que vous souhaitez toobe résultats trouvée à partir. |
| end |fin de Hello hello de fenêtre de temps de que vous souhaitez toobe résultats trouvée à partir. |

**Réponse :**

```
    {
      "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "__metadata" : {
        "resultType" : "raw",
        "total" : 1455,
        "top" : 150,
        "StartTime" : "2015-02-11T21:09:07.0345815Z",
        "Status" : "Successful",
        "LastUpdated" : "2015-02-11T21:09:07.331463Z",
        "CoreResponses" : [],
        "sort" : [{
          "name" : "TimeGenerated",
          "order" : "desc"
        }],
        "requestTime" : 450
      },
      "value": [{
        "SourceSystem" : "OpsManager",
        "TimeGenerated" : "2015-02-07T14:07:33Z",
        "Source" : "SideBySide",
        "EventLog" : "Application",
        "Computer" : "BAMBAM",
        "EventCategory" : 0,
        "EventLevel" : 1,
        "EventLevelName" : "Error",
        "UserName" : "N/A",
        "EventID" : 78,
        "MG" : "00000000-0000-0000-0000-000000000001",
        "TimeCollected" : "2015-02-07T14:10:04.69Z",
        "ManagementGroupName" : "AOI-5bf9a37f-e841-462b-80d2-1d19cd97dc40",
        "id" : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
        "Type" : "Event",
        "__metadata" : {
          "Type" : "Event",
          "TimeGenerated" : "2015-02-07T14:07:33Z",
          "highlighting" : {
          "EventLevelName" : ["{[hl]}Error{[/hl]}"]
        }
      }]
    ],
            "start" : "2015-02-04T21:03:29.231Z",
            "end" : "2015-02-11T21:03:29.231Z"
          }
        }
      }]
    }
```

### <a name="searchid---actionread"></a>Recherche/{ID} - Action/lecture
**Contenu de hello la demande d’une recherche enregistrée :**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/search/{SearchId}?api-version=2015-03-20
```

> [!NOTE]
> Si hello recherche retourne un état « En attente », résultats de l’interrogation hello mis à jour peuvent être effectuées via cette API. Après 6 minutes, résultat hello de recherche de hello est supprimé du cache de hello et HTTP Gone est renvoyé. Si la demande de recherche initiale hello retourne immédiatement l’état « Succès », les résultats de hello ne sont pas ajoutés de cache toohello à l’origine de cette tooreturn API HTTP Gone si elle est interrogée. Hello le contenu d’un résultat HTTP 200 est Bonjour même format que la demande de recherche initiale hello, avec des valeurs mises à jour.
>
>

### <a name="saved-searches"></a>Recherches enregistrées
**Demander la liste des recherches enregistrées :**

```
    armclient post /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/savedSearches?api-version=2015-03-20
```

Méthodes prises en charge : GET PUT DELETE

Méthodes de collection prises en charge : GET

Hello tableau suivant décrit les propriétés de hello qui sont disponibles.

| Propriété | Description |
| --- | --- |
| Id |Identificateur unique de Hello. |
| Etag |**Requis pour le correctif**. Mis à jour par le serveur à chaque écriture. Valeur doit être égale toohello actuelle stockée ou ' *' tooupdate. 409 retourné pour les valeurs anciennes ou non valides. |
| properties.query |**Requis**. requête de recherche Hello. |
| properties.displayName |**Requis**. nom d’affichage de défini par l’utilisateur de Hello de requête de hello. |
| properties.category |**Requis**. catégories définies par l’utilisateur Hello de requête de hello. |

> [!NOTE]
> Hello API de recherche Analytique de journal actuellement renvoie créés par l’utilisateur quand elle est interrogée concernant les recherches enregistrées dans un espace de travail de recherches enregistrées. Hello API ne retourne pas de recherches enregistrées fournies par les solutions.
>
>

### <a name="create-saved-searches"></a>Créer des recherches enregistrées
**Requête :**

```
    $savedSearchParametersJson = "{'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisismyid?api-version=2015-03-20 $savedSearchParametersJson
```

> [!NOTE]
> nom de Hello pour toutes les recherches enregistrées, planifications et créées par hello API Analytique de journal des actions doit être en minuscules.

### <a name="delete-saved-searches"></a>Supprimer les recherches enregistrées
**Requête :**

```
    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20
```

### <a name="update-saved-searches"></a>Mettre à jour les recherches enregistrées
 **Requête :**

```
    $savedSearchParametersJson = "{'etag': 'W/`"datetime\'2015-04-16T23%3A35%3A35.3182423Z\'`"', 'properties': { 'Category': 'myCategory', 'DisplayName':'myDisplayName', 'Query':'* | measure Count() by Source', 'Version':'1'  }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/savedSearches/thisIsMyId?api-version=2015-03-20 $savedSearchParametersJson
```

### <a name="metadata---json-only"></a>Métadonnées - JSON uniquement
Voici un moyen toosee hello des champs pour tous les types de journaux pour les données hello collectées dans votre espace de travail. Par exemple, si vous souhaitez que savoir si le type d’événement de hello possède un champ nommé ordinateur, cette requête est une façon toocheck.

**Requête de champs :**

```
    armclient get /subscriptions/{SubId}/resourceGroups/{ResourceGroupId}/providers/Microsoft.OperationalInsights/workspaces/{WorkspaceName}/schema?api-version=2015-03-20
```

**Réponse :**

```
    {
      "__metadata" : {
        "schema" : {
          "name" : "Example Name",
          "version" : 2
        },
        "resultType" : "schema",
        "requestTime" : 35
      },
      "value" : [{
          "name" : "MG",
          "displayName" : "MG",
          "type" : "Guid",
          "facetable" : true,
          "display" : false,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Capacity_SMBUtilizationByHost", "Capacity_ArrayUtilization", "Capacity_SMBShareUtilization", "SQLAssessmentRecommendation", "Event", "ConfigurationChange", "ConfigurationAlert", "ADAssessmentRecommendation", "ConfigurationObject", "ConfigurationObjectProperty"]
        }, {
          "name" : "ManagementGroupName",
          "displayName" : "ManagementGroupName",
          "type" : "String",
          "facetable" : true,
          "display" : true,
          "ownerType" : ["PerfHourly", "ProtectionStatus", "Event", "ConfigurationChange", "ConfigurationAlert", "W3CIISLog", "AlertHistory", "Recommendation", "Alert", "SecurityEvent", "UpdateAgent", "RequiredUpdate", "ConfigurationObject", "ConfigurationObjectProperty"]
        }
      ]
    }
```

Hello tableau suivant décrit les propriétés de hello qui sont disponibles.

| **Propriété** | **Description** |
| --- | --- |
| name |Nom du champ. |
| displayName |Hello affiche le nom du champ de hello. |
| type |Type de valeur du champ hello de Hello. |
| facetable |Combinaison des propriétés « indexed », « stored » et « facet » actuelles. |
| display |Propriété « display » actuelle. True si le champ est visible dans la recherche. |
| ownerType |Types de tooonly réduite qui appartiennent à l’adresse IP tooonboarded. |

## <a name="optional-parameters"></a>Paramètres facultatifs
Hello informations suivantes décrit les paramètres facultatifs disponibles.

### <a name="highlighting"></a>Highlighting
paramètre de « Highlight » Hello est un paramètre facultatif, vous pouvez utiliser le sous-système de recherche hello toorequest inclure un jeu de marqueurs dans sa réponse.

Ces marqueurs indiquent hello début et la fin du texte en surbrillance qui correspond aux critères de hello fournis dans votre requête de recherche.
Vous pouvez spécifier hello début et fin des marqueurs qui sont utilisés par le terme de recherche toowrap hello mis en surbrillance.

**Exemple de requête de recherche**

```
    $savedSearchParametersJson =
    {
      "top":150,
      "highlight":{
        "pre":"{[hl]}",
        "post":"{[/hl]}"
      },
      "query":"*",
      "start":"2015-02-04T21:03:29.231Z",
      "end":"2015-02-11T21:03:29.231Z"
    }
    armclient post /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace ID}/search?api-version=2015-03-20 $searchParametersJson
```

**Exemple de résultat :**

```
    {
        "TimeGenerated":
        "2015-05-18T23:55:59Z", "Source":
        "EventLog": "Application",
        "Computer": "smokedturkey.net",
        "EventCategory": 0,
        "EventLevel":1,
        "EventLevelName":
        "Error"
        "Manager ", "__metadata":
        {
            "Type": "Event",
            "TimeGenerated": "2015-05-18T23:55:59Z",
            "highlighting": {
                "EventLevelName":
                ["{[hl]}Error{[/hl]}"]
            }
        }
    }
```

Notez que hello résultat précédent contient un message d’erreur qui a été préfixé et ajouté.

## <a name="computer-groups"></a>Groupes d’ordinateurs
Les groupes d'ordinateurs sont des recherches spéciales enregistrées qui retournent un ensemble d'ordinateurs.  Vous pouvez utiliser un groupe d’ordinateurs dans d’autres ordinateurs de toohello des résultats de requêtes toolimit hello dans le groupe de hello.  Un groupe d'ordinateurs est implémenté comme une recherche enregistrée avec une balise Group dont la valeur est Computer.

Voici un exemple de réponse pour un groupe d'ordinateurs.

```
    "etag": "W/\"datetime'2016-04-01T13%3A38%3A04.7763203Z'\"",
    "properties": {
        "Category": "My Computer Groups",
        "DisplayName": "My Computer Group",
        "Query": "srv* | Distinct Computer",
        "Tags": [{
            "Name": "Group",
            "Value": "Computer"
          }],
    "Version": 1
    }
```

### <a name="retrieving-computer-groups"></a>Récupération de groupes d'ordinateurs
ID d’un groupe d’ordinateurs, utilisez hello méthode Get avec groupe de hello tooretrieve

```
armclient get /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Group ID}`?api-version=2015-03-20
```

### <a name="creating-or-updating-a-computer-group"></a>Création ou mise à jour d'un groupe d'ordinateurs
toocreate un groupe d’ordinateurs, utilisez hello méthode Put avec un ID de recherche enregistrée unique. Si vous utilisez un ID de groupe d’ordinateurs existant, celui-ci est modifié. Lorsque vous créez un groupe d’ordinateurs dans le portail d’Analytique de journal hello, hello ID est créé à partir de nom et le groupe de hello.

requête Hello utilisé pour la définition de groupe hello doit retourner un ensemble d’ordinateurs pour hello groupe toofunction correctement.  Il est recommandé que vous mettez fin à la requête avec `| Distinct Computer` hello tooensure correct de données sont retournées.

définition de Hello Hello recherche enregistrée doit inclure une balise nommée groupe avec la valeur de l’ordinateur pour toobe de recherche hello classée sous forme d’un groupe d’ordinateurs.

```
    $etag=Get-Date -Format yyyy-MM-ddThh:mm:ss.msZ
    $groupName="My Computer Group"
    $groupQuery = "Computer=srv* | Distinct Computer"
    $groupCategory="My Computer Groups"
    $groupID = "My Computer Groups | My Computer Group"

    $groupJson = "{'etag': 'W/`"datetime\'" + $etag + "\'`"', 'properties': { 'Category': '" + $groupCategory + "', 'DisplayName':'"  + $groupName + "', 'Query':'" + $groupQuery + "', 'Tags': [{'Name': 'Group', 'Value': 'Computer'}], 'Version':'1'  }"

    armclient put /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20 $groupJson
```

### <a name="deleting-computer-groups"></a>Suppression de groupes d'ordinateurs
ID d’un groupe d’ordinateurs, utilisez hello méthode Delete avec groupe de hello toodelete

```
armclient delete /subscriptions/{Subscription ID}/resourceGroups/{Resource Group Name}/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/$groupId`?api-version=2015-03-20
```


## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur [recherche de journal](log-analytics-log-searches.md) toobuild les requêtes à l’aide des champs personnalisés pour les critères.
