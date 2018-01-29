---
title: "Journalisation des diagnostics Azure Cosmos DB | Microsoft Docs"
description: "Utilisez ce didacticiel pour vous familiariser avec la journalisation d’Azure Cosmos DB."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/12/2017
ms.author: mimig
ms.openlocfilehash: 835f6ffce9b2e1bb4b6cfd7476bb3fdb24a4f092
ms.sourcegitcommit: 0e1c4b925c778de4924c4985504a1791b8330c71
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/06/2018
---
# <a name="azure-cosmos-db-diagnostic-logging"></a>Journalisation des diagnostics Azure Cosmos DB

Lorsque vous avez commencé à utiliser une ou plusieurs bases de données Azure Cosmos DB, vous pouvez surveiller comment et quand vos bases de données font l’objet d’un accès. La journalisation des diagnostics dans Azure Cosmos DB vous permet d’effectuer cette analyse. En activant la journalisation des diagnostics, vous pouvez envoyer des journaux au [Stockage Azure](https://azure.microsoft.com/services/storage/), les transmettre à [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) et/ou les exporter vers [Log Analytics](https://azure.microsoft.com/services/log-analytics/), inclus dans [Operations Management Suite](https://www.microsoft.com/cloud-platform/operations-management-suite).

![Journalisation des diagnostics dans le Stockage, Event Hubs ou Operations Management Suite via Log Analytics](./media/logging/azure-cosmos-db-logging-overview.png)

Utilisez ce didacticiel pour commencer à utiliser la journalisation Azure Cosmos DB via le portail Azure, l’interface CLI ou PowerShell.

## <a name="what-is-logged"></a>Quels sont les éléments journalisés ?

* Toutes les demandes API REST SQL authentifiées sont enregistrées, ce qui inclut des requêtes ayant échoué suite à des demandes, des erreurs système ou des autorisations d’accès incorrectes. Actuellement, la prise en charge des API MongoDB, Graphe et Table n’est pas disponible.
* Les opérations sur la base de données même, notamment les opérations CRUD sur l’ensemble des documents, des conteneurs et des bases de données.
* Les opérations sur les clés de compte, notamment la création, la modification ou la suppression de ces clés.
* les requêtes non authentifiées qui génèrent une réponse 401. Par exemple, les requêtes qui ne possèdent pas de jeton de porteur, qui sont incorrectes, qui ont expiré ou qui comportent un jeton non valide.

## <a name="prerequisites"></a>Conditions préalables
Pour suivre ce didacticiel, vous avez besoin des ressources suivantes :

* Un compte, une base de données et un conteneur Azure Cosmos DB existants. Pour obtenir des instructions sur la création de ces ressources, consultez [Créer un compte de base de données à l’aide du portail Azure](create-sql-api-dotnet.md#create-a-database-account), [Exemples d’interface CLI](cli-samples.md) ou [Exemples PowerShell](powershell-samples.md).

<a id="#turn-on"></a>
## <a name="turn-on-logging-in-the-azure-portal"></a>Activer la journalisation dans le portail Azure

1. Dans le [portail Azure](https://portal.azure.com), dans votre compte Azure Cosmos DB, cliquez sur **Journaux de diagnostic** dans le volet de navigation de gauche, puis sur **Activer les diagnostics**.

    ![Activer la journalisation des diagnostics pour Azure Cosmos DB dans le portail Azure](./media/logging/turn-on-portal-logging.png)

2. Dans la page **Paramètres de diagnostic**, procédez comme suit : 

    * **Nom**. Entrez un nom pour les journaux à créer.

    * **Archive vers un compte de stockage**. Pour utiliser cette option, vous avez besoin d’un compte de stockage existant auquel vous connecter. Pour créer un compte de stockage dans le portail, consultez [Créer un compte de stockage](../storage/common/storage-create-storage-account.md) et suivez les instructions pour créer un compte Resource Manager à usage général. Puis revenez à cette page dans le portail pour sélectionner votre compte de stockage. L’affichage des comptes de stockage nouvellement créés dans le menu déroulant peut prendre quelques minutes.
    * **Transmettre à un Event Hub**. Pour utiliser cette option, vous avez besoin d’un espace de noms Event Hub existant et d’un Event Hub auquel vous connecter. Pour créer un espace de noms Event Hubs, consultez [Créer un espace de noms Event Hubs et un Event Hub à l’aide du portail Azure](../event-hubs/event-hubs-create.md). Puis revenez à cette page dans le portail pour sélectionner l’espace de noms Event Hub et le nom de la stratégie.
    * **Envoyer à Log Analytics**.     Pour utiliser cette option, utilisez un espace de travail existant ou créez un espace de travail Log Analytics en suivant les étapes permettant de [créer un espace de travail](../log-analytics/log-analytics-quick-collect-azurevm.md#create-a-workspace) dans le portail. Pour plus d’informations sur l’affichage de vos journaux dans Log Analytics, consultez la section [Afficher les journaux dans Log Analytics](#view-in-loganalytics).
    * **Journaliser DataPlaneRequests**. Sélectionnez cette option pour journaliser des diagnostics pour les comptes d’API SQL, Graph et Table. Si vous effectuez un archivage dans un compte de stockage, vous pouvez sélectionner la période de rétention des journaux de diagnostic. Les journaux sont supprimés automatiquement après l’expiration de la période de rétention.
    * **Log MongoRequests** (Journal MongoRequests). Sélectionnez cette option pour journaliser des diagnostics pour les comptes d’API MongoDB. Si vous effectuez un archivage dans un compte de stockage, vous pouvez sélectionner la période de rétention des journaux de diagnostic. Les journaux sont supprimés automatiquement après l’expiration de la période de rétention.
    * **Metric Requests** (Demandes de métrique). Sélectionnez cette option pour stocker des données détaillées dans les [métriques Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md). Si vous effectuez un archivage dans un compte de stockage, vous pouvez sélectionner la période de rétention des journaux de diagnostic. Les journaux sont supprimés automatiquement après l’expiration de la période de rétention.

3. Cliquez sur **Enregistrer**.

    Si vous recevez une erreur indiquant « Failed to update diagnostics for \<workspace name>. The subscription \<subscription id> is not registered to use microsoft.insights » (Échec de la mise à jour des diagnostics pour <nom de l’espace de travail>. L’abonnement <id d’abonnement> n’est pas inscrit pour utiliser microsoft.insights), suivez les instructions de la page [Résoudre les problèmes d’Azure Diagnostics](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage) pour inscrire le compte, puis recommencez cette procédure.

    Si vous souhaitez modifier la façon dont vos journaux de diagnostic seront enregistrés à l’avenir, vous pouvez revenir à cette page à tout moment et modifier les paramètres de journal de diagnostic pour votre compte.

## <a name="turn-on-logging-using-cli"></a>Activation de la journalisation à l’aide de l’interface CLI

Pour activer la journalisation des métriques et diagnostics à l’aide d’Azure CLI, utilisez les commandes suivantes :

- Pour activer le stockage des journaux de diagnostic dans un compte de stockage, utilisez cette commande :

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   `resourceId` est le nom du compte Azure Cosmos DB. `storageId` est le nom du compte de stockage auquel vous souhaitez envoyer les journaux.

- Pour activer la diffusion en continu des journaux de diagnostic vers un Event Hub, utilisez cette commande :

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   `resourceId` est le nom du compte Azure Cosmos DB. `serviceBusRuleId` est une chaîne au format suivant :

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- Pour activer l’envoi des journaux de diagnostic à un espace de travail Log Analytics, utilisez cette commande :

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of the log analytics workspace> --enabled true
   ```

Vous pouvez combiner ces paramètres pour activer plusieurs options de sortie.

## <a name="turn-on-logging-using-powershell"></a>Activation de la journalisation à l’aide de PowerShell

Pour activer la journalisation à l’aide de PowerShell, vous avez besoin d’Azure Powershell, avec la version minimale 1.0.1.

Pour installer Azure PowerShell et l’associer à votre abonnement Azure, consultez l’article [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).

Si vous avez déjà installé Azure PowerShell et que vous ne connaissez pas la version que vous utilisez, à partir de la console PowerShell, entrez `(Get-Module azure -ListAvailable).Version`.  

### <a id="connect"></a>Se connecter à vos abonnements
Démarrez une session Azure PowerShell et connectez-vous à votre compte Azure avec la commande suivante :  

```powershell
Login-AzureRmAccount
```

Dans la fenêtre contextuelle de votre navigateur, entrez votre nom d’utilisateur et votre mot de passe Azure. Azure PowerShell obtient alors tous les abonnements associés à ce compte et utilise par défaut le premier.

Si vous disposez de plusieurs abonnements, vous devrez peut-être en spécifier un en particulier, celui qui a été utilisé pour créer votre Azure Key Vault. Tapez la commande suivante pour afficher les abonnements de votre compte :

```powershell
Get-AzureRmSubscription
```

Ensuite, pour spécifier l’abonnement associé au compte Azure Cosmos DB que vous allez journaliser, tapez :

```powershell
Set-AzureRmContext -SubscriptionId <subscription ID>
```

> [!NOTE]
> Si plusieurs abonnements sont associés à votre compte, il est important de spécifier l’abonnement.
>
>

Pour plus d’informations sur la configuration d’Azure PowerShell, consultez la page [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).

### <a id="storage"></a>Création d’un nouveau compte de stockage pour vos journaux
Bien que vous puissiez utiliser un compte de stockage existant pour vos journaux, dans ce didacticiel nous en créons un nouveau qui sera dédié à vos journaux Azure Cosmos DB. Pour plus de commodité, nous stockons les détails du compte de stockage dans une variable nommée **sa**.

Pour faciliter encore la gestion, dans ce didacticiel nous utilisons le groupe de ressources qui contient notre base de données Azure Cosmos DB. Remplacez les valeurs de ContosoResourceGroup, contosocosmosdblogs et « Nord du centre des États-Unis » pour vos propres valeurs, comme il convient :

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup `
-Name contosocosmosdblogs -Type Standard_LRS -Location 'North Central US'
```

> [!NOTE]
> Si vous décidez d’utiliser un compte de stockage existant, vous devez utiliser le même abonnement que pour votre abonnement Azure Cosmos DB, ainsi que le modèle de déploiement Resource Manager plutôt que le modèle de déploiement Classic.
>
>

### <a id="identify"></a>Identifier le compte Azure Cosmos DB pour vos journaux
Définissez le nom du compte Azure Cosmos DB sur une variable nommée **account**, où ResourceName est le nom du compte Azure Cosmos DB.

```powershell
$account = Get-AzureRmResource -ResourceGroupName ContosoResourceGroup `
-ResourceName contosocosmosdb -ResourceType "Microsoft.DocumentDb/databaseAccounts"
```

### <a id="enable"></a>Activation de la journalisation
Pour activer la journalisation pour Azure Cosmos DB, utilisez la cmdlet Set-AzureRmDiagnosticSetting, ainsi que les variables pour le nouveau compte de stockage, le compte Azure Cosmos DB et la catégorie pour laquelle vous souhaitez activer les journaux. Exécutez la commande suivante, en définissant l’indicateur **-Enabled** sur **$true** :

```powershell
Set-AzureRmDiagnosticSetting  -ResourceId $account.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories DataPlaneRequests
```

La sortie de la commande doit ressembler à ce qui suit :

```powershell
    StorageAccountId            : /subscriptions/<subscription-ID>/resourceGroups/ContosoResourceGroup/providers`
    /Microsoft.Storage/storageAccounts/contosocosmosdblogs
    ServiceBusRuleId            :
    EventHubAuthorizationRuleId :
    Metrics
        TimeGrain       : PT1M
        Enabled         : False
        RetentionPolicy
        Enabled : False
        Days    : 0
    
    Logs
        Category        : DataPlaneRequests
        Enabled         : True
        RetentionPolicy
        Enabled : False
        Days    : 0
    
    WorkspaceId                 :
    Id                          : /subscriptions/<subscription-ID>/resourcegroups/ContosoResourceGroup/providers`
    /microsoft.documentdb/databaseaccounts/contosocosmosdb/providers/microsoft.insights/diagnosticSettings/service
    Name                        : service
    Type                        :
    Location                    :
    Tags                        :
```

L’activation de la journalisation de votre base de données est à présent activée et les informations sont enregistrées dans votre compte de stockage.

Si vous le souhaitez, vous pouvez également définir une stratégie de rétention pour vos journaux, par exemple la suppression automatique des anciens journaux. Par exemple, définissez une stratégie de rétention en attribuant à l’indicateur **-RetentionEnabled** la valeur **$true** et en définissant le paramètre **-RetentionInDays** sur **90** afin que les journaux antérieurs à 90 jours soient automatiquement supprimés.

```powershell
Set-AzureRmDiagnosticSetting -ResourceId $account.ResourceId`
 -StorageAccountId $sa.Id -Enabled $true -Categories DataPlaneRequests`
  -RetentionEnabled $true -RetentionInDays 90
```

### <a id="access"></a>Accéder à vos journaux
Les journaux Azure Cosmos DB pour la catégorie **DataPlaneRequests** sont stockés dans le conteneur **insights-logs-data-plane-requests** dans le compte de stockage spécifié. 

Commencez par créer une variable pour le nom du conteneur. Ce nom sera utilisé dans le reste de cette procédure pas à pas.

```powershell
    $container = 'insights-logs-dataplanerequests'
```

Pour répertorier tous les objets blob présents dans ce conteneur, saisissez :

```powershell
Get-AzureStorageBlob -Container $container -Context $sa.Context
```

Le résultat ressemble à ce qui suit :

```powershell
ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob
BlobType          : BlockBlob
Length            : 10510193
ContentType       : application/octet-stream
LastModified      : 9/28/2017 7:49:04 PM +00:00
SnapshotTime      :
ContinuationToken:
Context           : Microsoft.WindowsAzure.Commands.Common.Storage.`
                    LazyAzureStorageContext
Name              : resourceId=/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS`
/MICROSOFT.DOCUMENTDB/DATABASEACCOUNTS/CONTOSOCOSMOSDB/y=2017/m=09/d=28/h=19/m=00/PT1H.json
```

Comme vous pouvez le voir dans cette sortie, les objets blob suivent une convention d’affectation de noms : `resourceId=/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/<resource group name>/PROVIDERS/MICROSOFT.DOCUMENTDB/DATABASEACCOUNTS/<Database Account Name>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json`

Les valeurs de date et d’heure utilisent UTC.

Le même compte de stockage pouvant être utilisé pour collecter les journaux de plusieurs ressources, l’ID complet de ressource dans le nom de l’objet blob est très utile si vous voulez accéder seulement aux objets blob dont vous avez besoin et les télécharger. Mais avant cela, nous aborderons le téléchargement de tous les objets blob.

Tout d’abord, créez un dossier pour télécharger les objets blob. Par exemple : 

```powershell
New-Item -Path 'C:\Users\username\ContosoCosmosDBLogs'`
 -ItemType Directory -Force
```

Procurez-vous la liste de tous les objets blob :  

```powershell
$blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context
```

Adressez cette liste via « Get-AzureStorageBlobContent » pour télécharger les objets blob dans notre dossier de destination :

```powershell
$blobs | Get-AzureStorageBlobContent `
 -Destination 'C:\Users\username\ContosoCosmosDBLogs'
```

Lorsque vous exécutez cette seconde commande, le délimiteur **/** présent dans les noms d’objet blob crée une structure de dossiers complète sous le dossier de destination. Cette structure de dossiers est utilisée pour télécharger et stocker les objets blob en tant que fichiers.

Pour télécharger les objets blob de façon sélective, utilisez des caractères génériques. Par exemple : 

* Si vous disposez de plusieurs bases de données et souhaitez télécharger les journaux d’une seule d’entre elles nommée CONTOSOCOSMOSDB3 :

    ```powershell
    Get-AzureStorageBlob -Container $container `
     -Context $sa.Context -Blob '*/DATABASEACCOUNTS/CONTOSOCOSMOSDB3
    ```

* Si vous disposez de plusieurs groupes de ressources et souhaitez télécharger les journaux d’un seul d’entre eux, utilisez `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:

    ```powershell
    Get-AzureStorageBlob -Container $container `
    -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
    ```
* Si vous souhaitez télécharger tous les journaux du mois de juillet 2017, utilisez `-Blob '*/year=2017/m=07/*'` :

    ```powershell
    Get-AzureStorageBlob -Container $container `
     -Context $sa.Context -Blob '*/year=2017/m=07/*'
    ```

Par ailleurs :

* Pour interroger l’état des paramètres de diagnostic de votre ressource de base de données : `Get-AzureRmDiagnosticSetting -ResourceId $account.ResourceId`
* Pour désactiver la journalisation de la catégorie **DataPlaneRequests** pour votre ressource de compte de base de données : `Set-AzureRmDiagnosticSetting -ResourceId $account.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories DataPlaneRequests`


Les blobs retournés dans chacune de ces requêtes sont stockés sous forme de blob JSON au format texte, comme indiqué dans le code suivant. 

```json
{
    "records":
    [
        {
           "time": "Fri, 23 Jun 2017 19:29:50.266 GMT",
           "resourceId": "contosocosmosdb",
           "category": "DataPlaneRequests",
           "operationName": "Query",
           "resourceType": "Database",
           "properties": {"activityId": "05fcf607-6f64-48fe-81a5-f13ac13dd1eb",`
           "userAgent": "documentdb-dotnet-sdk/1.12.0 Host/64-bit MicrosoftWindowsNT/6.2.9200.0 AzureSearchIndexer/1.0.0",`
           "resourceType": "Database","statusCode": "200","documentResourceId": "",`
           "clientIpAddress": "13.92.241.0","requestCharge": "2.260","collectionRid": "",`
           "duration": "9250","requestLength": "72","responseLength": "209", "resourceTokenUserRid": ""}
        }
    ]
}
```

Pour en savoir plus sur les données de chaque blob JSON, consultez [Interpréter vos journaux Azure Cosmos DB](#interpret).

## <a name="managing-your-logs"></a>Gestion de vos journaux

Les journaux sont disponibles dans votre compte dans les deux heures suivant le moment où l’opération Azure Cosmos DB a été effectuée. C’est à vous de gérer vos journaux dans votre compte de stockage :

* Utilisez les méthodes de contrôle d’accès Azure standard pour assurer la sécurité de vos journaux en limitant l’accès à ces derniers.
* Supprimez les journaux que vous ne souhaitez plus conserver dans votre compte de stockage.
* La période de rétention pour les demandes de plan de données archivées dans un compte de stockage est configurée dans le portail lorsque l’option **Journaliser DataPlaneRequests** est sélectionnée. Pour modifier ce paramètre, consultez [Activer la journalisation dans le portail Azure](#turn-on-logging-in-the-azure-portal).


<a id="#view-in-loganalytics"></a>
## <a name="view-logs-in-log-analytics"></a>Afficher les journaux dans Log Analytics

Si vous avez sélectionné l’option **Send to Log Analytics** (Envoyer à Log Analytics) lorsque vous avez activé la journalisation, les données de diagnostic de votre collection sont transférées à Log Analytics sous deux heures. Par conséquent, si vous consultez Log Analytics immédiatement après l’activation de la journalisation, aucune donnée ne s’affichera. Il vous suffit alors d’attendre deux heures et de réessayer. 

Avant de consulter vos journaux, il est utile de vérifier que votre espace de travail Log Analytics a été mis à niveau pour utiliser le nouveau langage de requête Log Analytics. Pour effectuer cette vérification, ouvrez le [portail Azure](https://portal.azure.com), cliquez sur **Log Analytics** tout à gauche, puis sélectionnez le nom de l’espace de travail, comme indiqué dans l’image suivante. La page **Espace de travail OMS** s’affiche comme illustré dans l’image suivante.

![Log Analytics dans le portail Azure](./media/logging/azure-portal.png)

Si le message suivant s’affiche dans la page **Espace de travail OMS**, cela signifie que votre espace de travail n’a pas été mis à niveau pour utiliser le nouveau langage. Pour plus d’informations sur la mise à niveau vers le nouveau langage de requête, consultez [Mise à niveau de votre espace de travail Azure Log Analytics vers la nouvelle recherche dans les journaux](../log-analytics/log-analytics-log-search-upgrade.md). 

![Notification de mise à niveau de Log Analytics](./media/logging/upgrade-notification.png)

Pour afficher vos données de diagnostic dans Log Analytics, ouvrez la page Recherche dans les journaux à partir du menu de gauche ou de la zone de gestion de la page, comme indiqué dans l’image suivante.

![Options de recherche dans les journaux dans le portail Azure](./media/logging/log-analytics-open-log-search.png)

Maintenant que vous avez activé la collecte de données, exécutez une recherche dans les journaux en utilisant le nouveau langage de requête comme indiqué dans l’exemple suivant. Cet exemple permet d’afficher les dix derniers journaux `AzureDiagnostics | take 10`.

![Exemple de recherche (10 journaux)](./media/logging/log-analytics-query.png)

<a id="#queries"></a>
### <a name="queries"></a>Requêtes

Voici quelques requêtes supplémentaires que vous pouvez entrer dans la zone **Recherche dans les journaux**. Elles vous aideront à surveiller vos conteneurs Azure Cosmos DB. Ces requêtes fonctionnent avec le [nouveau langage](../log-analytics/log-analytics-log-search-upgrade.md). 

Pour en savoir plus sur la signification des données retournées par chaque recherche dans les journaux, consultez [Interpréter vos journaux Azure Cosmos DB](#interpret).

* Tous les journaux de diagnostic issus d’Azure Cosmos DB pour la période spécifiée

    ```
    AzureDiagnostics | where ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests"
    ```

* Les dix derniers événements consignés

    ```
    AzureDiagnostics | where ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | take 10
    ```

* Toutes les opérations regroupées par type

    ```
    AzureDiagnostics | where ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | summarize count() by OperationName
    ```

* Toutes les opérations regroupées par ressource

    ```
    AzureActivity | where ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | summarize count() by Resource
    ```

* Toutes les activités des utilisateurs regroupées par ressource. Notez qu’il s’agit d’un journal d’activité et non d’un journal de diagnostic.

    ```
    AzureActivity | where Caller == "test@company.com" and ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | summarize count() by Resource
    ```

* Opérations durant plus de 3 millisecondes.

    ```
    AzureDiagnostics | where toint(duration_s) > 30000 and ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | summarize count() by clientIpAddress_s, TimeGenerated
    ```

* Agent exécutant les opérations

    ```
    AzureDiagnostics | where ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | summarize count() by OperationName, userAgent_s
    ```

* Moment auquel des opérations de longue durée ont été exécutées

    ```
    AzureDiagnostics | where ResourceProvider=="MICROSOFT.DOCUMENTDB" and Category=="DataPlaneRequests" | project TimeGenerated , toint(duration_s)/1000 | render timechart
    ```

Pour plus d’informations sur l’utilisation du nouveau langage de recherche dans les journaux, consultez [Présentation des recherches dans les journaux dans Log Analytics](../log-analytics/log-analytics-log-search-new.md). 

## <a id="interpret"></a>Interpréter vos journaux

Les données de diagnostic stockées dans le stockage Azure et Log Analytics suivent un schéma très similaire. 

Le tableau suivant décrit le contenu de chaque entrée de journal.

| Propriété ou champ du stockage Azure | Propriété de Log Analytics | DESCRIPTION |
| --- | --- | --- |
| time | TimeGenerated | Date et heure (UTC) de l’opération. |
| ResourceId | Ressource | Le compte Azure Cosmos DB pour lequel les journaux sont activés.|
| category | Catégorie | Pour les journaux Azure Cosmos DB, DataPlaneRequests est la seule valeur disponible. |
| operationName | Nom d'opération | Nom de l’opération. Cette valeur peut être l’une des opérations suivantes : Create, Update, Read, ReadFeed, Delete, Replace, Execute, SqlQuery, Query, JSQuery, Head, HeadFeed ou Upsert.   |
| properties | n/a | Le contenu de ce champ est décrit dans les lignes suivantes. |
| activityId | activityId_g | GUID unique de l’opération journalisée. |
| userAgent | userAgent_s | Chaîne qui spécifie l’agent utilisateur client effectuant la demande. Le format est {nom de l’agent utilisateur}/{version}.|
| resourceType | ResourceType | Type de la ressource faisant l’objet de l’accès. Cette valeur peut être l’un des types de ressources suivants : Database, Collection, Document, Attachment, User, Permission, StoredProcedure, Trigger, UserDefinedFunction ou Offer. |
| statusCode |statusCode_s | État de réponse de l’opération. |
| requestResourceId | ResourceId | L’ID de ressource se rapportant à la demande, peut pointer vers databaseRid, collectionRid ou documentRid en fonction de l’opération.|
| clientIpAddress | clientIpAddress_s | Adresse IP du client. |
| requestCharge | requestCharge_s | Nombre d’unités de requête utilisées par l’opération. |
| collectionRid | collectionId_s | ID unique de la collection.|
| duration | duration_s | Durée de l’opération, en cycles. |
| requestLength | requestLength_s | Longueur de la demande, en octets. |
| responseLength | responseLength_s | Longueur de la réponse, en octets.|
| resourceTokenUserRid | resourceTokenUserRid_s | Ce champ n’est pas vide lorsque des [jetons de ressource](https://docs.microsoft.com/azure/cosmos-db/secure-access-to-data#resource-tokens) sont utilisés pour l’authentification et pointe vers l’ID de ressource de l’utilisateur. |

## <a name="next-steps"></a>étapes suivantes

- Pour comprendre non seulement comment activer la journalisation, mais aussi les métriques et les catégories de journaux prises en charge par les différents services Azure, consultez les articles [Vue d’ensemble des métriques dans Microsoft Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) et [Présentation des journaux de diagnostic Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).
- Pour en savoir plus sur les concentrateurs d’événements, lisez les articles suivants :
   - [Qu’est-ce qu’Azure Event Hubs ?](../event-hubs/event-hubs-what-is-event-hubs.md)
   - [Prise en main des hubs d’événements](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- Consultez [Télécharger les journaux de métriques et diagnostics de Stockage Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs).
- Consultez [Présentation des recherches dans les journaux dans Log Analytics](../log-analytics/log-analytics-log-search-new.md).
