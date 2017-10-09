---
title: "aaaAzure analyse API REST de procédure pas à pas | Documents Microsoft"
description: Comment tooauthenticate demande tooand utilisation hello API REST de surveillance Azure.
author: mcollier
manager: 
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 565e6a88-3131-4a48-8b82-3effc9a3d5c6
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: mcollier
ms.openlocfilehash: b8ae3a03fd21af872f1dc5fed40a101a24ca1652
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitoring-rest-api-walkthrough"></a>Procédure pas à pas d’utilisation de l’API REST d’Azure Monitor
Cet article vous montre comment tooperform authentification afin que votre code peut utiliser hello [référence d’API REST Microsoft Azure analyse](https://msdn.microsoft.com/library/azure/dn931943.aspx).         

Hello API d’analyse Azure permet de tooprogrammatically possible de récupérer hello disponible par défaut de définitions de métrique (type hello de mesure telles que le temps processeur, des demandes, etc.), de granularité et de valeurs de mesure. Une fois extraites, les données de hello peuvent être enregistrées dans un magasin de données distinct comme base de données SQL Azure, base de données Azure Cosmos ou Azure Data Lake. De là, une analyse supplémentaire peut être effectuée en fonction des besoins.

En plus de fonctionner avec différents points de données de mesure, comme indiqué dans cet article, hello analyse API rend possible toolist règles d’alerte, affichage des journaux d’activité et bien plus encore. Pour obtenir une liste complète des opérations disponibles, consultez hello [référence d’API REST Microsoft Azure analyse](https://msdn.microsoft.com/library/azure/dn931943.aspx).

## <a name="authenticating-azure-monitor-requests"></a>Authentification des requêtes Azure Monitor
première étape de Hello est demande de hello tooauthenticate.

Toutes les tâches hello exécutées dans hello API d’analyse Azure utilisation hello Azure Resource Manager authentification modèle. Ainsi, toutes les requêtes doivent être authentifiées avec Azure Active Directory (Azure AD). Une application cliente d’approche tooauthenticate hello est toocreate un principal du service Azure AD et récupérer le jeton d’authentification (JWT) hello. Hello exemple de script suivant montre comment créer un répertoire Azure AD via PowerShell principal du service. Pour une vue d’ensemble plus détaillée, consultez la documentation du toohello sur [une ressources tooaccess principal du service à l’aide de Azure PowerShell toocreate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-password). Il est également possible trop[créer un principal de service via le portail Azure de hello](../azure-resource-manager/resource-group-create-service-principal-portal.md).

```PowerShell
$subscriptionId = "{azure-subscription-id}"
$resourceGroupName = "{resource-group-name}"
$location = "centralus"

# Authenticate tooa specific Azure subscription.
Login-AzureRmAccount -SubscriptionId $subscriptionId

# Password for hello service principal
$pwd = "{service-principal-password}"

# Create a new Azure AD application
$azureAdApplication = New-AzureRmADApplication `
                        -DisplayName "My Azure Monitor" `
                        -HomePage "https://localhost/azure-monitor" `
                        -IdentifierUris "https://localhost/azure-monitor" `
                        -Password $pwd

# Create a new service principal associated with hello designated application
New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId

# Assign Reader role toohello newly created service principal
New-AzureRmRoleAssignment -RoleDefinitionName Reader `
                          -ServicePrincipalName $azureAdApplication.ApplicationId.Guid

```

tooquery hello Azure analyse API, application de client hello doit utiliser hello précédemment créé tooauthenticate principal de service. Hello, exemple de script PowerShell suivant montre une méthode, à l’aide de hello [bibliothèque d’authentification Active Directory](../active-directory/active-directory-authentication-libraries.md) (ADAL) toohelp obtenir un jeton d’authentification de jeton Web JSON hello. un jeton JWT Hello est passé en tant que partie d’un paramètre d’autorisation HTTP dans les demandes toohello API REST du moniteur de Azure.

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

Une fois l’étape de configuration d’authentification hello est terminée, requêtes peuvent ensuite être exécutées sur hello API REST du moniteur de Azure. Il existe deux requêtes utiles :

1. Liste des définitions de métrique hello pour une ressource
2. Récupérer les valeurs de mesure hello

## <a name="retrieve-metric-definitions"></a>Récupérer les définitions des mesures
> [!NOTE]
> les définitions de métrique tooretrieve à l’aide de hello API REST de moniteur Azure, utilisez « 2016-03-01 » comme hello version de l’API.
>
>

```PowerShell
$apiVersion = "2016-03-01"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metricDefinitions?api-version=${apiVersion}"

Invoke-RestMethod -Uri $request `
                  -Headers $authHeader `
                  -Method Get `
                  -Verbose
```
Pour une application de la logique de Azure, les définitions de métrique hello apparaîtrait toohello similaire après la capture d’écran :

![Alt « Vue JSON de la réponse de définition de mesure. »](./media/monitoring-rest-api-walkthrough/available_metric_definitions_logic_app_json_response_clean.png)

Pour plus d’informations, consultez hello [liste des définitions de métrique hello pour une ressource dans l’API REST de moniteur Azure](https://msdn.microsoft.com/library/azure/mt743621.aspx) documentation.

## <a name="retrieve-metric-values"></a>Récupérer des valeurs de mesure
Une fois que les définitions de métrique disponibles hello sont connues, il est possible tooretrieve hello métriques connexes. Utilisez nom « value » de métrique hello (pas hello 'localizedValue') pour toutes les demandes de filtrage (par exemple, extraire hello « CpuTime » et « Requêtes » métrique points de données). Si aucun filtre n’est spécifié, la métrique de hello par défaut est retourné.

> [!NOTE]
> tooretrieve les valeurs de mesure à l’aide de hello API REST de moniteur Azure, utilisez « 2016-06-01 » comme hello version de l’API.
>
>

**Méthode**: GET

**URI de demande** : https://management.azure.com/subscriptions/*{id-abonnement}*/resourceGroups/*{nom-groupe-ressources}*/providers/*{espace-de-noms-fournisseur-ressources}*/*{type-ressource}*/*{nom-ressource}*/providers/microsoft.insights/metrics?$filter=*{filtre}*&amp;api-version=*{version-api}*

Par exemple, points de données de mesure tooretrieve hello RunsSucceeded pour hello étant donné la plage de temps et pour un fragment de temps de 1 heure, demande de hello serait comme suit :

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'RunsSucceeded') and aggregationType eq 'Total' and startTime eq 2016-09-23 and endTime eq 2016-09-24 and timeGrain eq duration'PT1H'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

résultat de Hello apparaîtrait similaire toohello exemple suivant capture d’écran :

![ALT « Réponse JSON indiquant la valeur de mesure Temps de réponse moyen »](./media/monitoring-rest-api-walkthrough/available_metrics_logic_app_json_response.png)

tooretrieve plusieurs données ou une agrégation des points, ajoutez les noms de définition de métrique hello et filtre toohello des types d’agrégation, comme dans hello l’exemple suivant :

```PowerShell
$apiVersion = "2016-06-01"
$filter = "(name.value eq 'ActionsCompleted' or name.value eq 'RunsSucceeded') and (aggregationType eq 'Total' or aggregationType eq 'Average') and startTime eq 2016-09-23T13:30:00Z and endTime eq 2016-09-23T14:30:00Z and timeGrain eq duration'PT1M'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/${resourceProviderNamespace}/${resourceType}/${resourceName}/providers/microsoft.insights/metrics?`$filter=${filter}&api-version=${apiVersion}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

### <a name="use-armclient"></a>Utiliser ARMClient
Une autre toousing PowerShell (comme indiqué ci-dessus), est toouse [ARMClient](https://github.com/projectkudu/ARMClient) sur votre ordinateur Windows. ARMClient gère l’authentification hello Azure AD (et le jeton JWT résultant) automatiquement. Hello étapes suivantes décrivent l’utilisation d’ARMClient pour récupérer des données de mesure :

1. Installez [Chocolatey](https://chocolatey.org/) et [ARMClient](https://github.com/projectkudu/ARMClient).
2. Dans une fenêtre de terminal, saisissez *armclient.exe login*. Cela vous invite toolog dans tooAzure.
3. Tapez *armclient GET [id_ressource]/providers/microsoft.insights/metricdefinitions?api-version=2016-03-01*
4. Tapez *armclient GET [id_ressource]/providers/microsoft.insights/metrics?api-version=2016-06-01*

![ALT « Using ARMClient toowork avec hello API REST de surveillance Azure »](./media/monitoring-rest-api-walkthrough/armclient_metricdefinitions.png)

## <a name="retrieve-hello-resource-id"></a>Récupérer hello ID de ressource
À l’aide des API REST de hello peut aider à réellement les définitions de métrique disponibles hello toounderstand, de granularité et les valeurs associées. Cette information est utile lorsque vous utilisez hello [bibliothèque de gestion Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).

Pour hello précédant le code, hello ressource ID toouse est toohello de chemin d’accès complet hello souhaitée des ressources Azure. Par exemple, tooquery par rapport à une application Web Azure, ID de ressource hello serait :

*/subscriptions/{subscription-id}/resourceGroups/{nom-groupe-ressources}/providers/Microsoft.Web/sites/{nom-site}/*

Hello liste suivante contient quelques exemples de formats d’identificateur de ressource pour les différentes ressources Azure :

* **IoT Hub** - /subscriptions/*{id-abonnement}*/resourceGroups/*{nom-groupe-ressources}*/providers/Microsoft.Devices/IotHubs/*{nom-iot-hub}*
* **Pool SQL élastique** - /subscriptions/*{id-abonnement}*/resourceGroups/*{nom-groupe-ressources}*/providers/Microsoft.Sql/servers/*{bd-pool}*/elasticpools/*{nom-pool-sql}*
* **SQL Database (v12)** - /subscriptions/*{id-abonnement}*/resourceGroups/*{nom-groupe-ressources}*/providers/Microsoft.Sql/servers/*{nom-serveur}*/databases/*{nom-bd}*
* **Service Bus** - /subscriptions/*{id-abonnement}*/resourceGroups/*{nom-groupe-ressources}*/providers/Microsoft.ServiceBus/*{espace-noms}*/*{nom-servicebus}*
* **Groupes de machines virtuelles identiques** - /subscriptions/*{id-abonnement}*/resourceGroups/*{nom-groupe-ressources}*/providers/Microsoft.Compute/virtualMachineScaleSets/*{nom-machine-virtuelle}*
* **Machines virtuelles** - /subscriptions/*{id-abonnement}*/resourceGroups/*{nom-groupe-ressources}*/providers/Microsoft.Compute/virtualMachines/*{nom-machine-virtuelle}*
* **Event Hubs** - /subscriptions/*{id-abonnement}*/resourceGroups/*{nom-groupe-ressources}*/providers/Microsoft.EventHub/namespaces/*{espace-noms-eventhub}*

Il existe des ID de ressource de hello tooretrieving autres approches, y compris à l’aide de l’Explorateur de ressources Azure, afficher des ressources de hello souhaité dans hello portail Azure et via PowerShell ou hello CLI d’Azure.

### <a name="azure-resource-explorer"></a>Azure Resource Explorer
ID de ressource toofind hello pour une ressource de votre choix, une approche utile est toouse hello [Explorateur de ressources Azure](https://resources.azure.com) outil. Parcourir les ressources toohello souhaité, puis regardez à ID hello indiqué, comme dans hello suivant capture d’écran :

![Alt Azure Resource Explorer](./media/monitoring-rest-api-walkthrough/azure_resource_explorer.png)

### <a name="azure-portal"></a>Portail Azure
ID de ressource Hello peut également être obtenue à partir de hello portail Azure. toodo donc parcourir les ressources toohello souhaité, puis sélectionnez Propriétés. Hello ID de ressource s’affiche dans le panneau des propriétés hello, comme dans hello suivant capture d’écran :

![ALT « ID de ressource affiché dans le panneau des propriétés hello Bonjour Azure portal »](./media/monitoring-rest-api-walkthrough/resourceid_azure_portal.png)

### <a name="azure-powershell"></a>Azure PowerShell
ID de ressource Hello peut être récupéré à l’aide des applets de commande PowerShell de Azure également. Par exemple, ID de ressource tooobtain hello pour une application Web Azure, exécutez hello Get-AzureRmWebApp applet de commande, comme dans hello suivant capture d’écran :

![Alt ID ressource obtenu via PowerShell](./media/monitoring-rest-api-walkthrough/resourceid_powershell.png)

### <a name="azure-cli"></a>Interface de ligne de commande Azure
tooretrieve hello ID de ressource à l’aide de hello CLI d’Azure, d’exécuter la commande de « azure webapp afficher » hello, spécifiant hello '--json' option, comme indiqué dans hello suivant capture d’écran :

![Alt ID ressource obtenu via PowerShell](./media/monitoring-rest-api-walkthrough/resourceid_azurecli.png)

## <a name="retrieve-activity-log-data"></a>Récupérer des données du journal d’activité
Dans tooworking d’addition avec des définitions de métriques et les valeurs associées, il est également possible tooretrieve intéressantes insights tooAzure connexes des ressources supplémentaires. Par exemple, il est possible de tooquery [le journal d’activité](https://msdn.microsoft.com/library/azure/dn931934.aspx) données. Hello exemple suivant montre comment à l’aide des données de journal hello API REST de Azure moniteur tooquery activité au sein d’une plage de dates spécifique pour un abonnement Azure :

```PowerShell
$apiVersion = "2014-04-01"
$filter = "eventTimestamp ge '2016-09-23' and eventTimestamp le '2016-09-24'and eventChannels eq 'Admin, Operation'"
$request = "https://management.azure.com/subscriptions/${subscriptionId}/providers/microsoft.insights/eventtypes/management/values?api-version=${apiVersion}&`$filter=${filter}"
(Invoke-RestMethod -Uri $request `
                   -Headers $authHeader `
                   -Method Get `
                   -Verbose).Value | ConvertTo-Json
```

## <a name="next-steps"></a>Étapes suivantes
* Hello de révision [vue d’ensemble de l’analyse](monitoring-overview.md).
* Hello de vue [prise en charge des métriques avec Azure analyse](monitoring-supported-metrics.md).
* Hello de révision [référence d’API REST Microsoft Azure analyse](https://msdn.microsoft.com/library/azure/dn931943.aspx).
* Hello de révision [bibliothèque de gestion Azure](https://msdn.microsoft.com/library/azure/mt417623.aspx).
