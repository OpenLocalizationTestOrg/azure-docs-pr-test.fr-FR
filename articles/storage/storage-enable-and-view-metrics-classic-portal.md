---
title: "Activation des métriques de stockage dans le portail Azure | Microsoft Docs"
description: "Activation des métriques de stockage pour les services d’objet Blob, de File d’attente, de Table et de Fichier"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 2fb5b229-f099-4334-92be-4e0e7dd257d7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 4d6065597a41372ea6d320ab318b0c71d6a48b2a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-storage-metrics-and-viewing-metrics-data"></a>Activation de Storage Metrics et affichage des données de métriques
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a>Vue d'ensemble
Storage Metrics est activé par défaut lorsque vous créez un compte de stockage. Vous pouvez configurer la surveillance à l’aide du [Portail Azure Classic](https://manage.windowsazure.com), de Windows PowerShell ou par programmation avec une API de stockage.

Lorsque vous activez Storage Metrics, vous devez choisir une période de rétention des données : cette période détermine combien de temps le service de stockage conserve les métriques et la durée pendant laquelle l’espace requis pour les stocker vous est facturé. En règle générale, il est recommandé d’utiliser une période de rétention plus courte pour les métriques par minute que pour les métriques par heure, en raison de l’espace supplémentaire requis. La période de rétention que vous définissez doit être suffisamment longue pour vous donner le temps d’analyser les données et de télécharger les métriques à conserver à des fins d’analyse ou de création de rapports hors connexion. N’oubliez pas que le téléchargement des données de métriques depuis votre compte de stockage est aussi facturé.

## <a name="how-to-enable-storage-metrics-using-the-azure-classic-portal"></a>Activer les métriques de stockage à l’aide du portail Azure Classic
Dans le [portail Azure Classic](https://manage.windowsazure.com), la page Configurer d’un compte de stockage permet de contrôler les métriques de stockage. Pour la surveillance, vous pouvez définir un niveau et une période de rétention en jours pour chaque objet blob, table et file d’attente. Dans chaque cas, le niveau est l’un des suivants :

* Désactivée : aucune métrique n’est collectée.
* Minimale : les métriques de stockage recueillent un jeu de base de métriques, notamment l’entrée/sortie, la disponibilité, la latence et les pourcentages de réussite. Ces données sont ensuite regroupées pour les services BLOB, de Table et de File d’attente.
* Détaillée : les métriques de stockage recueillent un jeu complet de métriques, notamment les mêmes métriques pour chaque opération d’API de stockage, en plus des métriques au niveau du service. Les métriques détaillées permettent d’analyser plus précisément les problèmes survenant durant le fonctionnement d’une application.

Notez que le portail Azure Classic ne vous permet pas pour le moment de configurer les métriques par minute dans votre compte de stockage. Vous devez les activer avec PowerShell ou par programmation.

## <a name="how-to-enable-storage-metrics-using-powershell"></a>Comment activer les métriques de stockage avec PowerShell
Vous pouvez utiliser PowerShell sur votre ordinateur local pour configurer les métriques de stockage dans votre compte de stockage. Utilisez l’applet de commande Azure PowerShell Get-AzureStorageServiceMetricsProperty pour récupérer les paramètres actuels et l’applet de commande Set-AzureStorageServiceMetricsProperty pour modifier les paramètres actuels.

Les applets de commande qui contrôlent les métriques de stockage utilisent les paramètres suivants :

* MetricsType peut avoir pour valeur Hour ou Minute.
* ServiceType peut avoir pour valeur Blob, Queue ou Table.
* MetricsLevel peut avoir pour valeur None (équivalent à Désactivée dans le portail Azure Classic), Service (équivalent à Minimale dans le portail Azure Classic) ou ServiceAndApi (équivalent à Détaillée dans le portail Azure Classic).

Par exemple, la commande suivante active les métriques par minute pour le service BLOB dans votre compte de stockage par défaut avec une période de rétention de cinq jours :

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5
```
La commande suivante récupère le niveau actuel des métriques par heure et la période de rétention en jours pour le service BLOB dans votre compte de stockage par défaut :

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```
Pour plus d’informations sur la configuration des applets de commande Azure PowerShell avec votre abonnement Azure et sur la sélection du compte de stockage par défaut à utiliser, voir [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).

## <a name="how-to-enable-storage-metrics-programmatically"></a>Comment activer Storage Metrics par programmation
L’extrait de code C# suivant montre comment activer les métriques et la journalisation pour le service BLOB à l’aide de la bibliothèque cliente de stockage pour .NET :

```csharp
//Parse the connection string for the storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access to the Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy to 10 days. 
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at the same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set the default service version to be used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set the service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a>Affichage des métriques de stockage
Une fois Storage Metrics configuré de manière à surveiller votre compte de stockage, il enregistre les métriques dans une série de tables connues dans votre compte de stockage. Vous pouvez utiliser la page Surveiller de votre compte de stockage dans le portail Azure Classic pour afficher sur un graphique les métriques par heure à mesure qu’elles sont disponibles. Sur cette page dans le portail Azure Classic, vous pouvez :

* sélectionner les métriques à représenter sur le graphique (les métriques disponibles varient selon que vous avez choisi d’effectuer une surveillance détaillée ou minimale pour le service dans la page Configurer) ;
* sélectionner l’intervalle de temps pour les métriques affichées sur le graphique ;
* choisir d’utiliser une échelle absolue ou relative pour représenter les métriques ;
* configurer des alertes par e-mail qui vous notifient quand une métrique spécifique atteint une certaine valeur.

Si vous souhaitez télécharger les métriques pour un stockage à long terme ou pour les analyser localement, vous devez utiliser un outil ou écrire du code pour lire les tables. Vous devez télécharger les métriques par minute pour analyse. Les tables ne sont pas visibles si vous répertoriez toutes les tables dans votre compte de stockage, mais vous pouvez y accéder directement par nom. De nombreux outils tiers de consultation du stockage prennent en compte ces tables et vous permettent de les afficher directement (voir le billet de blog [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) pour obtenir la liste des outils disponibles).

### <a name="hourly-metrics"></a>Métriques toutes les heures
* $MetricsHourPrimaryTransactionsBlob
* $MetricsHourPrimaryTransactionsTable
* $MetricsHourPrimaryTransactionsQueue

### <a name="minute-metrics"></a>Métriques par minute
* $MetricsMinutePrimaryTransactionsBlob
* $MetricsMinutePrimaryTransactionsTable
* $MetricsMinutePrimaryTransactionsQueue

### <a name="capacity"></a>Capacité
* $MetricsCapacityBlob

Vous trouverez des informations complètes sur les schémas de ces tables dans [Schéma de table de métriques Storage Analytics](https://msdn.microsoft.com/library/azure/hh343264.aspx). Les exemples de lignes ci-dessous montrent uniquement un sous-ensemble des colonnes disponibles, mais ils illustrent les différentes façons dont Storage Metrics enregistre ces métriques :

| PartitionKey | RowKey | Timestamp | TotalRequests | TotalBillableRequests | TotalIngress | TotalEgress | Availability | AverageE2ELatency | AverageServerLatency | PercentSuccess |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| 20140522T1100 |user;All |2014-05-22T11:01:16.7650250Z |7 |7 |4003 |46801 |100 |104.4286 |6.857143 |100 |
| 20140522T1100 |user;QueryEntities |2014-05-22T11:01:16.7640250Z |5 |5 |2694 |45951 |100 |143.8 |7.8 |100 |
| 20140522T1100 |user;QueryEntity |2014-05-22T11:01:16.7650250Z |1 |1 |538 |633 |100 |3 |3 |100 |
| 20140522T1100 |user;UpdateEntity |2014-05-22T11:01:16.7650250Z |1 |1 |771 |217 |100 |9 |6 |100 |

Dans cet exemple de données de métriques par minute, la clé de partition (PartitionKey) utilise une résolution d’une minute. La clé de ligne (RowKey) identifie le type d’informations qui sont stockées dans la ligne. Elle se compose de deux éléments : le type d’accès et le type de demande.

* Le type d’accès a la valeur user ou system, user correspondant à toutes les demandes de l’utilisateur au service de stockage et system correspondant à toutes les demandes formulées par Storage Analytics.
* Le type de demande peut avoir la valeur all, auquel cas il s’agit d’une ligne de résumé, ou il identifie l’API spécifique comme QueryEntity ou UpdateEntity.

Les exemples de données ci-dessus montrent tous les enregistrements pour une seule minute (à partir de 11h00). Ainsi, la somme des demandes QueryEntities, QueryEntity et UpdateEntity est égale à sept, ce qui correspond bien au total indiqué sur la ligne user:All. De même, vous pouvez déduire la latence de bout en bout moyenne (104,4286) sur la ligne user:All en effectuant le calcul suivant : ((143,8 * 5) + 3 + 9)/7.

Songez à configurer des alertes dans la page Surveiller du portail Azure Classic pour que les métriques de stockage puissent vous avertir automatiquement de tout changement important dans le comportement de vos services de stockage. Si vous utilisez un explorateur de stockage pour télécharger ces données de métriques dans un format délimité, vous pouvez analyser les données dans Microsoft Excel. Voir le billet de blog [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) pour obtenir la liste des explorateurs de stockage disponibles.

## <a name="accessing-metrics-data-programmatically"></a>Accès aux données de métriques par programmation
L’exemple de code suivant en C# accède aux métriques par minute pour une plage de minutes et affiche les résultats dans une fenêtre de console. Il utilise la version 4 de la bibliothèque de stockage Azure. Celle-ci comprend la classe CloudAnalyticsClient, qui simplifie l’accès aux tables de métriques de stockage.

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert the dates to the format used in the PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} to {2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using the entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in the MetricsEntity class.
          // The PartitionKey identifies the DataTime of the metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0 
        select entity;

        // Filter on "user" transactions after fetching the metrics from Table Storage.
        // (StartsWith is not supported using LINQ with Azure table storage)
        var results = query.ToList().Where(m => m.RowKey.StartsWith("user"));
        var resultString = results.Aggregate(new StringBuilder(), (builder, metrics) => builder.AppendLine(MetricsString(metrics, opContext))).ToString();
        Console.WriteLine(resultString);
    }
}

private static string MetricsString(MetricsEntity entity, OperationContext opContext)
{
    var entityProperties = entity.WriteEntity(opContext);
    var entityString =
    string.Format("Time: {0}, ", entity.Time) +
    string.Format("AccessType: {0}, ", entity.AccessType) +
    string.Format("TransactionType: {0}, ", entity.TransactionType) +
    string.Join(",", entityProperties.Select(e => new KeyValuePair<string, string>(e.Key.ToString(), e.Value.PropertyAsObject.ToString())));
    return entityString;
}
```

## <a name="what-charges-do-you-incur-when-you-enable-storage-metrics"></a>Quels sont les frais encourus quand vous activez les métriques de stockage ?
Les demandes d’écriture pour créer des entités de table pour les métriques sont facturées au tarif standard applicable à toutes les opérations Azure Storage.

Les demandes de lecture et de suppression formulées par un client sur des données de métriques sont aussi facturées au tarif standard. Si vous avez configuré une stratégie de rétention des données, vous n’êtes pas facturé quand Azure Storage supprime les anciennes données de métriques. Toutefois, si vous supprimez des données de métriques, les opérations de suppression sont facturées à votre compte.

La capacité utilisée par les tables de métriques est également facturée ; vous pouvez utiliser les informations suivantes pour estimer la capacité utilisée pour stocker les données de métriques :

* En une heure, pour un service qui utilise toutes les API de chaque service, environ 148 Ko de données sont stockés par heure dans les tables de transaction de métriques si vous avez activé la synthèse au niveau des services et des API.
* En une heure, pour un service qui utilise toutes les API de chaque service, environ 12 Ko de données sont stockés par heure dans les tables de transaction de métriques si vous avez uniquement activé la synthèse au niveau des services.
* Deux lignes supplémentaires sont ajoutées chaque jour à la table de capacité pour les objets blob (si l’utilisateur a activé les journaux). Cela signifie que la table augmente d’environ 300 octets au maximum par jour.

## <a name="next-steps"></a>Étapes suivantes :
[Activation de la journalisation et accès aux données des journaux de stockage](https://msdn.microsoft.com/library/dn782840.aspx)
