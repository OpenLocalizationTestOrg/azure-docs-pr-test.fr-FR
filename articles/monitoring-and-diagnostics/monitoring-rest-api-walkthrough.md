---
title: "Procédure pas à pas d’utilisation de l’API REST d’Azure Monitor | Microsoft Docs"
description: "Comment authentifier des demandes et utiliser l’API REST d’Azure Monitor pour récupérer les définitions des métriques et les valeurs des métriques disponibles."
author: mcollier
manager: 
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 565e6a88-3131-4a48-8b82-3effc9a3d5c6
ms.service: monitoring-and-diagnostics
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.search.region: 
ms.search.scope: 
ms.search.validFrom: 
ms.dyn365.ops.version: 
ms.topic: article
ms.date: 09/18/2017
ms.author: mcollier
ms.openlocfilehash: 357a63c65a4f6864dca259aad8a76f83681cd501
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/08/2017
---
# <a name="azure-monitoring-rest-api-walkthrough"></a>Procédure pas à pas d’utilisation de l’API REST d’Azure Monitor
Cet article vous montre comment effectuer l’authentification afin que votre code puisse utiliser la [Référence de l’API REST Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).         

L’API Azure Monitor permet de retrouver par programme les définitions des métriques, la granularité et les valeurs des métriques par défaut disponibles. Les données peuvent être enregistrées dans un magasin de données distinct comme Azure SQL Database, Azure Cosmos DB ou Azure Data Lake. De là, une analyse supplémentaire peut être effectuée en fonction des besoins.

En plus de fonctionner avec divers points de données de métriques, l’API Monitor permet également de répertorier les règles d’alerte, d’afficher les journaux d’activité et plus encore. Pour obtenir la liste complète des opérations disponibles, consultez la [Référence de l’API REST Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).

## <a name="authenticating-azure-monitor-requests"></a>Authentification des demandes Azure Monitor
La première étape consiste à authentifier la requête.

Toutes les tâches exécutées sur l’API Azure Monitor utilisent le modèle d’authentification d’Azure Resource Manager. Ainsi, toutes les requêtes doivent être authentifiées avec Azure Active Directory (Azure AD). Une approche pour authentifier l’application client consiste à créer un principal du service Azure AD et récupérer le jeton d’authentification (JWT). L’exemple de script suivant illustre la création d’un principal de service Azure AD via PowerShell. Pour une présentation plus détaillée, reportez-vous à la documentation sur [l’utilisation d’Azure PowerShell pour créer un principal de service pour accéder aux ressources](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password). Il est également possible de [créer un principal du service sur le portail Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md).

```PowerShell
$subscriptionId = "{azure-subscription-id}"
$resourceGroupName = "{resource-group-name}"

# Authenticate to a specific Azure subscription.
Login-AzureRmAccount -SubscriptionId $subscriptionId

# Password for the service principal
$pwd = "{service-principal-password}"

# Create a new Azure AD application
$azureAdApplication = New-AzureRmADApplication `
                        -DisplayName "My Azure Monitor" `
                        -HomePage "https://localhost/azure-monitor" `
                        -IdentifierUris "https://localhost/azure-monitor" `
                        -Password $pwd

# Create a new service principal associated with the designated application
New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

# Assign Reader role to the newly created service principal
New-AzureRmRoleAssignment -RoleDefinitionName Reader `
                          -ServicePrincipalName $azureAdApplication.ApplicationId.Guid

```

Pour interroger l’API Azure Monitor, l’application client doit utiliser le principal de service créé précédemment pour s’authentifier. L’exemple de script PowerShell suivant montre une approche utilisant la [bibliothèque d’authentification Active Directory](../active-directory/active-directory-authentication-libraries.md) (ADAL) pour obtenir le jeton d’authentification JWT. Le jeton JWT est passé en tant que partie d’un paramètre d’autorisation HTTP dans les demandes à l’API REST Azure Monitor.

```PowerShell
$azureAdApplication = Get-AzureRmADApplication -IdentifierUri "https://localhost/azure-monitor"

$subscription = Get-AzureRmSubscription -SubscriptionId $subscriptionId

$clientId = $azureAdApplication.ApplicationId.Guid
$tenantId = $subscription.TenantId
$authUrl = "https://login.microsoftonline.com/${tenantId}"

$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]$authUrl
$cred = New-Object -TypeName Microsoft.IdentityModel.Clients.ActiveDirectory.ClientCredential -ArgumentList ($clientId, $pwd)

$result = $AuthContext.AcquireToken("https://management.core.windows.net/", $cred)

# Build an array of HTTP header values
$authHeader = @{
'Content-Type'='application/json'
'Accept'='application/json'
'Authorization'=$result.CreateAuthorizationHeader()
}
```

Après l’authentification, les demandes peuvent ensuite être exécutées sur l’API REST d’Azure Monitor. Il existe deux requêtes utiles :

1. Répertorier les définitions des mesures pour une ressource
2. Récupérer les valeurs des mesures

## <a name="retrieve-metric-definitions-multi-dimensional-api"></a>Récupérer les définitions des métriques (API multidimensionnelle)

Utilisez [l’API REST de définitions de mesures Azure Monitor](https://docs.microsoft.com/rest/api/monitor/metricdefinitions) pour accéder à la liste des mesures disponibles pour un service.

**Méthode**: GET

**URI de demande** : https://management.azure.com/subscriptions/*{subscriptionId}*/resourceGroups/*{resourceGroupName}*/providers/*{resourceProviderNamespace}*/*{resourceType}*/*{resourceName*/providers/microsoft.insights/metricDefinitions?api-version=*{apiVersion}*

Par exemple, pour récupérer les définitions des métriques pour un compte Stockage Azure, la demande s’affiche comme suit :

```PowerShell
$request = "https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Storage/accounts/ContosoStorage/providers/microsoft.insights/metricDefinitions?api-version=2017-05-01-preview"

Invoke-RestMethod -Uri $request `
                  -Headers $authHeader `
                  -Method Get `
                  -OutFile ".\contosostorage-metricdef-results.json" `
                  -Verbose

```
> [!NOTE]
> Pour récupérer les définitions des métriques à l’aide de l’API REST des métriques Azure Monitor multidimensionnelle, utilisez « 2017-05-01-preview » en tant que version de l’API.
>
>

Le corps de réponse JSON résultant doit ressembler à l’exemple suivant : (notez que la deuxième métrique contient des dimensions)

```JSON
{
    "value": [
        {
            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Storage/accounts/ContosoStorage/providers/microsoft.insights/metricdefinitions/UsedCapacity",
            "resourceId": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Storage/accounts/ContosoStorage",
            "category": "Capacity",
            "name": {
                "value": "UsedCapacity",
                "localizedValue": "Used capacity"
            },
            "isDimensionRequired": false,
            "unit": "Bytes",
            "primaryAggregationType": "Average",
            "metricAvailabilities": [
                {
                    "timeGrain": "PT1M",
                    "retention": "P30D"
                },
                {
                    "timeGrain": "PT1H",
                    "retention": "P30D"
                }
            ]
        },
        {
            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Storage/accounts/ContosoStorage/providers/microsoft.insights/metricdefinitions/Transactions",
            "resourceId": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Storage/accounts/ContosoStorage",
            "category": "Transaction",
            "name": {
                "value": "Transactions",
                "localizedValue": "Transactions"
            },
            "isDimensionRequired": false,
            "unit": "Count",
            "primaryAggregationType": "Total",
            "metricAvailabilities": [
                {
                    "timeGrain": "PT1M",
                    "retention": "P30D"
                },
                {
                    "timeGrain": "PT1H",
                    "retention": "P30D"
                }
            ],
            "dimensions": [
                {
                    "value": "ResponseType",
                    "localizedValue": "Response type"
                },
                {
                    "value": "GeoType",
                    "localizedValue": "Geo type"
                },
                {
                    "value": "ApiName",
                    "localizedValue": "API name"
                }
            ]
        },
        ...
    ]
}
```

## <a name="retrieve-dimension-values-multi-dimensional-api"></a>Récupérer les valeurs de dimension (API multidimensionnelle)
Une fois que les définitions des métriques disponibles sont connues, certaines métriques peuvent contenir des dimensions. Avant d’interroger la métrique, vous souhaiterez peut-être découvrir la plage de valeurs d’une dimension. En fonction de ces valeurs de dimension, vous pouvez ensuite choisir de filtrer ou de segmenter les métriques en fonction des valeurs de dimension lors de l’interrogation des métriques. Utilisez le nom 'value' (et non ' localizedValue') de la mesure pour toutes les demandes de filtrages (par exemple, pour récupérer les points de données de mesure « CpuTime » et « Requests »). Si aucun filtre n’est spécifié, la mesure par défaut est renvoyée.

> [!NOTE]
> Pour récupérer les valeurs de dimension à l’aide de l’API REST d’Azure Monitor, utilisez « 2017-05-01-preview » en tant que version de l’API.
>
>

**Méthode**: GET

**URI de demande** : https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?metric=*{metric}*&amp;timespan=*{starttime/endtime}*&amp;$filter=*{filter}*&amp;resultType=metadata&amp;api-version=*{apiVersion}*

Par exemple, pour récupérer la liste des valeurs potentielles de la « dimension du nom de l’API » pour la métrique « Transactions » pendant une période donnée, la demande ressemble à ce qui suit :

```PowerShell
$filter = "APIName eq '*'"
$request = "https://management.azure.com/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Storage/accounts/ContosoStorage/providers/microsoft.insights/metrics?metric=Transactions&timespan=2017-09-01T00:00:00Z/2017-09-10T00:00:00Z&resultType=metadata&$filter=${filter}&api-version=2017-05-01-preview"
Invoke-RestMethod -Uri $request `
    -Headers $authHeader `
    -Method Get `
    -OutFile ".\contosostorage-dimension-values.json" `
    -Verbose
```
Le corps de réponse JSON résultant doit ressembler à l’exemple suivant :

```JSON
{
  "timespan": "2017-09-01T00:00:00Z/2017-09-10T00:00:00Z",
  "value": [
    {
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Storage/accounts/ContosoStorage/providers/Microsoft.Insights/metrics/Transactions",
      "type": "Microsoft.Insights/metrics",
      "name": {
        "value": "Transactions",
        "localizedValue": "Transactions"
      },
      "unit": "Count",
      "timeseries": [
        {
          "metadatavalues": [
            {
              "name": {
                "value": "apiname",
                "localizedValue": "apiname"
              },
              "value": "DeleteBlob"
            }
          ]
        },
        {
          "metadatavalues": [
            {
              "name": {
                "value": "apiname",
                "localizedValue": "apiname"
              },
              "value": "SetBlobProperties"
            }
          ]
        },
        {
          "metadatavalues": [
            {
              "name": {
                "value": "apiname",
                "localizedValue": "apiname"
              },
              "value": "PutPage"
            }
          ]
        },
        {
          "metadatavalues": [
            {
              "name": {
                "value": "apiname",
                "localizedValue": "apiname"
              },
              "value": "Unknown"
            }
          ]
        },
        ...
      ]    
    }
  ]
}
```

## <a name="retrieve-metric-values-multi-dimensional-api"></a>Récupérer les valeurs des métriques (API multidimensionnelle)
Une fois les définitions des métriques disponibles et les valeurs de dimension possibles connues, il est possible de récupérer les valeurs des métriques liées. Utilisez la valeur « value » du nom de la métrique (et non « localizedValue ») pour toutes les demandes de filtrage. Si aucun filtre de dimension n’est spécifié, la métrique agrégée regroupée est retournée.

> [!NOTE]
> Pour récupérer les valeurs des métriques multidimensionnelles à l’aide de l’API REST d’Azure Monitor, utilisez « 2017-05-01-preview » en tant que version de l’API.
>
>

**Méthode**: GET

**URI de demande** : https://management.azure.com/subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/*{resource-provider-namespace}*/*{resource-type}*/*{resource-name}*/providers/microsoft.insights/metrics?metric=*{metric}*&amp;timespan=*{starttime/endtime}*&amp;$filter=*{filter}*&amp;interval=*{timeGrain}*&amp;aggregation=*{aggreation}*&amp;api-version=*{apiVersion}*

Par exemple, pour récupérer les valeurs des métriques pour la métrique « Transactions » du stockage au cours d’une plage de 5 minutes, pour toutes les transactions relatives au nom de l’API « GetBlobProperties », la demande ressemble à ce qui suit :

```PowerShell
$filter = "APIName eq 'GetBlobProperties'"
$request = "https://management.azure.com/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Storage/accounts/ContosoStorage/providers/microsoft.insights/metrics?metric=Transactions&timespan=2017-09-19T02:00:00Z/2017-09-19T02:05:00Z&$filter=${filter}&interval=PT1M&aggregation=Count&api-version=2017-05-01-preview"
Invoke-RestMethod -Uri $request `
    -Headers $authHeader `
    -Method Get `
    -OutFile ".\contosostorage-metric-values.json" `
    -Verbose
```
Le corps de réponse JSON résultant doit ressembler à l’exemple suivant :

```JSON
{
  "cost": 0,
  "timespan": "2017-09-19T02:00:00Z/2017-09-19T02:05:00Z",
  "interval": "PT1M",
  "value": [
    {
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Storage/accounts/ContosoStorage/providers/Microsoft.Insights/metrics/Transactions",
      "type": "Microsoft.Insights/metrics",
      "name": {
        "value": "Transactions",
        "localizedValue": "Transactions"
      },
      "unit": "Count",
      "timeseries": [
        {
          "metadatavalues": [
            {
              "name": {
                "value": "apiname",
                "localizedValue": "apiname"
              },
              "value": "GetBlobProperties"
            }
          ],
          "data": [
            {
              "timeStamp": "2017-09-19T02:00:00Z",
              "count": 2.0
            },
            {
              "timeStamp": "2017-09-19T02:01:00Z",
              "count": 1.0
            },
            {
              "timeStamp": "2017-09-19T02:02:00Z",
              "count": 3.0
            },
            {
              "timeStamp": "2017-09-19T02:03:00Z",
              "count": 7.0
            },
            {
              "timeStamp": "2017-09-19T02:04:00Z",
              "count": 2.0
            }
          ]
        }
      ]
    }
  ]
}
```

## <a name="retrieve-metric-definitions"></a>Récupérer les définitions des métriques
Utilisez [l’API REST de définitions de mesures Azure Monitor](https://msdn.microsoft.com/library/mt743621.aspx) pour accéder à la liste des mesures disponibles pour un service.

**Méthode**: GET

**URI de demande** : https://management.azure.com/subscriptions/*{subscriptionId}*/resourceGroups/*{resourceGroupName}*/providers/*{resourceProviderNamespace}*/*{resourceType}*/*{resourceName}*/providers/microsoft.insights/metricDefinitions?api-version=*{apiVersion}*

Par exemple, pour récupérer les définitions des métriques pour une application logique Azure, la demande ressemble à ce qui suit :

```PowerShell
$request = "https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets/providers/microsoft.insights/metricDefinitions?api-version=2016-03-01"

Invoke-RestMethod -Uri $request `
                  -Headers $authHeader `
                  -Method Get `
                  -OutFile ".\contostweets-metricdef-results.json" `
                  -Verbose
```
> [!NOTE]
> Pour récupérer les définitions des mesures à l’aide de l’API REST d’Azure Monitor, utilisez « 2016-03-01 » en tant que la version de l’API.
>
>

Le corps de réponse JSON résultant doit ressembler à l’exemple suivant :
```JSON
{
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets/providers/microsoft.insights/metricdefinitions",
  "value": [
    {
      "name": {
        "value": "RunsStarted",
        "localizedValue": "Runs Started"
      },
      "category": "AllMetrics",
      "startTime": "0001-01-01T00:00:00Z",
      "endTime": "0001-01-01T00:00:00Z",
      "unit": "Count",
      "primaryAggregationType": "Total",
      "resourceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets",
      "resourceId": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets",
      "metricAvailabilities": [
        {
          "timeGrain": "PT1M",
          "retention": "P30D",
          "location": null,
          "blobLocation": null
        },
        {
          "timeGrain": "PT1H",
          "retention": "P30D",
          "location": null,
          "blobLocation": null
        }
      ],
      "properties": null,
      "dimensions": null,
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets/providers/microsoft.insights/metricdefinitions/RunsStarted",
      "supportedAggregationTypes": [ "None", "Average", "Minimum", "Maximum", "Total", "Count" ]
    }
  ]
}
```

Pour plus d’informations, consultez la documentation [Liste de définitions de mesure pour une ressource dans l’API REST d’Azure Monitor](https://msdn.microsoft.com/library/azure/mt743621.aspx) .

## <a name="retrieve-metric-values"></a>Récupération des valeurs des métriques
Une fois les définitions de mesures disponibles connues, il est possible de récupérer les valeurs de mesure liées. Utilisez le nom 'value' (et non ' localizedValue') de la mesure pour toutes les demandes de filtrages (par exemple, pour récupérer les points de données de mesure « CpuTime » et « Requests »). Si aucun filtre n’est spécifié, la mesure par défaut est renvoyée.

> [!NOTE]
> Pour récupérer les valeurs des métriques à l’aide de l’API REST d’Azure Monitor, utilisez « 2016-09-01 » en tant que version de l’API.
>
>

**Méthode**: GET

**URI de demande** : https://management.azure.com/subscriptions/*{id-abonnement}*/resourceGroups/*{nom-groupe-ressources}*/providers/*{espace-de-noms-fournisseur-ressources}*/*{type-ressource}*/*{nom-ressource}*/providers/microsoft.insights/metrics?$filter=*{filtre}*&amp;api-version=*{version-api}*

Par exemple, pour retrouver les points de données de mesure RunsSucceeded pour la plage de temps spécifiée et avec un fragment de temps de 1 heure, la requête est la suivante :

```PowerShell
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2017-08-18T19:00:00 and endTime eq 2017-08-18T23:00:00 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets/providers/microsoft.insights/metrics?$filter=${filter}&api-version=2016-09-01"
Invoke-RestMethod -Uri $request `
    -Headers $authHeader `
    -Method Get `
    -OutFile ".\contostweets-metrics-results.json" `
    -Verbose
```

Le corps de réponse JSON résultant doit ressembler à l’exemple suivant :

```JSON
{
  "value": [
    {
      "data": [
        {
          "timeStamp": "2017-08-18T19:00:00Z",
          "total": 0.0
        },
        {
          "timeStamp": "2017-08-18T20:00:00Z",
          "total": 159.0
        },
        {
          "timeStamp": "2017-08-18T21:00:00Z",
          "total": 174.0
        },
        {
          "timeStamp": "2017-08-18T22:00:00Z",
          "total": 97.0
        }
      ],
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets/providers/Microsoft.Insights/metrics/RunsSucceeded",
      "name": {
        "value": "RunsSucceeded",
        "localizedValue": "Runs Succeeded"
      },
      "type": "Microsoft.Insights/metrics",
      "unit": "Count"
    }
  ]
}
```

Pour récupérer plusieurs points de données ou d’agrégation, ajoutez les noms de définition de mesure et les types d’agrégation au filtre, comme illustré dans l’exemple suivant :

```PowerShell
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2017-08-18T21:00:00 and endTime eq 2017-08-18T21:30:00 and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets/providers/microsoft.insights/metrics?$filter=${filter}&api-version=2016-09-01"
Invoke-RestMethod -Uri $request `
    -Headers $authHeader `
    -Method Get `
    -OutFile ".\contostweets-metrics-multiple-results.json" `
    -Verbose
```
Le corps de réponse JSON résultant doit ressembler à l’exemple suivant :

```JSON
{
  "value": [
    {
      "data": [
        {
          "timeStamp": "2017-08-18T21:03:00Z",
          "total": 5.0,
          "average": 1.0
        },
        {
          "timeStamp": "2017-08-18T21:04:00Z",
          "total": 7.0,
          "average": 1.0
        }
      ],
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets/providers/Microsoft.Insights/metrics/ActionsCompleted",
      "name": {
        "value": "ActionsCompleted",
        "localizedValue": "Actions Completed "
      },
      "type": "Microsoft.Insights/metrics",
      "unit": "Count"
    },
    {
      "data": [
        {
          "timeStamp": "2017-08-18T21:03:00Z",
          "total": 5.0,
          "average": 1.0
        },
        {
          "timeStamp": "2017-08-18T21:04:00Z",
          "total": 7.0,
          "average": 1.0
        }
      ],
      "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets/providers/Microsoft.Insights/metrics/RunsSucceeded",
      "name": {
        "value": "RunsSucceeded",
        "localizedValue": "Runs Succeeded"
      },
      "type": "Microsoft.Insights/metrics",
      "unit": "Count"
    }
  ]
}
```

### <a name="use-armclient"></a>Utiliser ARMClient
Une autre approche consiste à utiliser [ARMClient](https://github.com/projectkudu/armclient) sur votre ordinateur Windows. ARMClient gère automatiquement l’authentification Azure AD (et le jeton JWT résultant). Les étapes suivantes décrivent l’utilisation d’ARMClient pour récupérer les données des métriques :

1. Installez [Chocolatey](https://chocolatey.org/) et [ARMClient](https://github.com/projectkudu/armclient).
2. Dans une fenêtre de terminal, saisissez *armclient.exe login*. Vous êtes alors invité à vous connecter à Azure.
3. Tapez *armclient GET [id_ressource]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*
4. Tapez *armclient GET [your_resource_id]/providers/microsoft.insights/metrics?api-version=2016-09-01*

Par exemple, afin de récupérer les définitions des métriques pour une application logique spécifique, exécutez la commande suivante :
```
armclient GET /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets/providers/microsoft.insights/metricDefinitions?api-version=2016-03-01
```


## <a name="retrieve-the-resource-id"></a>Récupération de l’ID de ressource
Utiliser l’API REST peut vraiment vous aider à comprendre les définitions de mesure disponibles, la granularité et les valeurs liées. Ces informations sont utiles lorsque vous utilisez la [bibliothèque de gestion Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).

Pour le code précédent, l’ID de ressource à utiliser est le chemin d’accès complet à la ressource Azure souhaitée. Par exemple, pour interroger une application web Azure, l’ID de ressource serait :

*/subscriptions/{subscription-id}/resourceGroups/{nom-groupe-ressources}/providers/Microsoft.Web/sites/{nom-site}/*

La liste suivante contient des exemples de formats d’ID de ressource pour les différentes ressources Azure :

* **IoT Hub** - /subscriptions/*{id-abonnement}*/resourceGroups/*{nom-groupe-ressources}*/providers/Microsoft.Devices/IotHubs/*{nom-iot-hub}*
* **Pool SQL élastique** - /subscriptions/*{id-abonnement}*/resourceGroups/*{nom-groupe-ressources}*/providers/Microsoft.Sql/servers/*{bd-pool}*/elasticpools/*{nom-pool-sql}*
* **SQL Database (v12)** - /subscriptions/*{id-abonnement}*/resourceGroups/*{nom-groupe-ressources}*/providers/Microsoft.Sql/servers/*{nom-serveur}*/databases/*{nom-bd}*
* **Service Bus** - /subscriptions/*{id-abonnement}*/resourceGroups/*{nom-groupe-ressources}*/providers/Microsoft.ServiceBus/*{espace-noms}*/*{nom-servicebus}*
* **Groupes de machines virtuelles identiques** - /subscriptions/*{subscription-id}*/resourceGroups/*{resource-group-name}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{vm-name}*
* **Machines virtuelles** - /subscriptions/*{id-abonnement}*/resourceGroups/*{nom-groupe-ressources}*/providers/Microsoft.Compute/virtualMachines/*{nom-machine-virtuelle}*
* **Event Hubs** - /subscriptions/*{id-abonnement}*/resourceGroups/*{nom-groupe-ressources}*/providers/Microsoft.EventHub/namespaces/*{espace-noms-eventhub}*

Il existe des approches alternatives à la récupération de l’ID de ressource, notamment avec l’Explorateur de ressources Azure, l’affichage de la ressource souhaitée dans le portail Azure et via PowerShell ou l’interface CLI Azure.

### <a name="azure-resource-explorer"></a>Azure Resource Explorer
Pour rechercher l’ID de ressource pour une ressource de votre choix, une approche utile consiste à utiliser l’outil [Explorateur de ressources Azure](https://resources.azure.com) . Naviguez vers la ressource souhaitée et observez l’ID indiqué, comme dans la capture d’écran suivante :

![Alt Azure Resource Explorer](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a>Portail Azure
L’ID de ressource peut également être obtenu à partir du portail Azure. Pour ce faire, accédez à la ressource souhaitée, puis sélectionnez Propriétés. L’ID de ressource s’affiche dans la section Propriétés, comme illustré dans la capture d’écran suivante :

![Alt « ID de ressource affiché dans le panneau Propriétés du portail Azure »](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a>Azure PowerShell
L’ID de ressource peut également être récupéré à l’aide des applets de commande d’Azure PowerShell. Par exemple, pour obtenir l’ID de ressource pour une application logique Azure, exécutez la cmdlet Get-AzureLogicApp, comme dans l’exemple suivant :

```PowerShell
Get-AzureRmLogicApp -ResourceGroupName azmon-rest-api-walkthrough -Name contosotweets
```

Le résultat doit être similaire à l’exemple suivant :
```
Id             : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Logic/workflows/ContosoTweets
Name           : ContosoTweets
Type           : Microsoft.Logic/workflows
Location       : centralus
ChangedTime    : 8/21/2017 6:58:57 PM
CreatedTime    : 8/18/2017 7:54:21 PM
AccessEndpoint : https://prod-08.centralus.logic.azure.com:443/workflows/f3a91b352fcc47e6bff989b85446c5db
State          : Enabled
Definition     : {$schema, contentVersion, parameters, triggers...}
Parameters     : {[$connections, Microsoft.Azure.Management.Logic.Models.WorkflowParameter]}
SkuName        :
AppServicePlan :
PlanType       :
PlanId         :
Version        : 08586982649483762729
```


### <a name="azure-cli"></a>Interface de ligne de commande Azure
Pour récupérer l’ID de ressource d’un compte Stockage Azure à l’aide de l’interface CLI Azure, exécutez la commande 'az storage account show', comme indiqué dans l’exemple suivant :

```
az storage account show -g azmon-rest-api-walkthrough -n contosotweets2017
```

Le résultat doit être similaire à l’exemple suivant :
```JSON
{
  "accessTier": null,
  "creationTime": "2017-08-18T19:58:41.840552+00:00",
  "customDomain": null,
  "enableHttpsTrafficOnly": false,
  "encryption": null,
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/azmon-rest-api-walkthrough/providers/Microsoft.Storage/storageAccounts/contosotweets2017",
  "identity": null,
  "kind": "Storage",
  "lastGeoFailoverTime": null,
  "location": "centralus",
  "name": "contosotweets2017",
  "networkAcls": null,
  "primaryEndpoints": {
    "blob": "https://contosotweets2017.blob.core.windows.net/",
    "file": "https://contosotweets2017.file.core.windows.net/",
    "queue": "https://contosotweets2017.queue.core.windows.net/",
    "table": "https://contosotweets2017.table.core.windows.net/"
  },
  "primaryLocation": "centralus",
  "provisioningState": "Succeeded",
  "resourceGroup": "azmon-rest-api-walkthrough",
  "secondaryEndpoints": null,
  "secondaryLocation": "eastus2",
  "sku": {
    "name": "Standard_GRS",
    "tier": "Standard"
  },
  "statusOfPrimary": "available",
  "statusOfSecondary": "available",
  "tags": {},
  "type": "Microsoft.Storage/storageAccounts"
}
```

> [!NOTE]
> Les applications Azure Logic Apps ne sont pas encore disponibles via l’interface CLI Azure, par conséquent, un compte Stockage Azure est indiqué dans l’exemple précédent.
>
>

## <a name="retrieve-activity-log-data"></a>Récupérer les données du journal d’activité
Outre les définitions des métriques et les valeurs associées, il est également possible d’utiliser l’API REST d’Azure Monitor pour récupérer des insights supplémentaires intéressants relatifs aux ressources Azure. Par exemple, il est possible d’obtenir les données du [journal d’activité](https://msdn.microsoft.com/library/azure/dn931934.aspx) par requête. L’exemple suivant montre comment utiliser des API REST Azure Monitor pour demander des données de journal d’activité au sein d’une plage de dates spécifique pour un abonnement Azure :

```PowerShell
$apiVersion = "2015-04-01"
$filter = "eventTimestamp ge '2017-08-18' and eventTimestamp le '2017-08-19'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&$filter=${filter}"
Invoke-RestMethod -Uri $request `
    -Headers $authHeader `
    -Method Get `
    -Verbose
```

## <a name="next-steps"></a>Étapes suivantes
* Consultez la [Vue d’ensemble de l’analyse](monitoring-overview.md).
* Affichez les [Mesures prises en charge avec Azure Monitor](monitoring-supported-metrics.md).
* Consultez la [Référence de l’API REST Microsoft Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).
* Consultez la [Bibliothèque de gestion Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).
