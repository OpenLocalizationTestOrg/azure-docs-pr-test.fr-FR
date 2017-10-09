---
title: "métriques de stockage aaaEnabling Bonjour portail Azure | Documents Microsoft"
description: "Comment tooenable les métriques de stockage pour hello services Blob, file d’attente, Table et fichier"
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
ms.openlocfilehash: 4c990371e08a6586d935b0535149eabd4960cfaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-storage-metrics-and-viewing-metrics-data"></a>Activation de Storage Metrics et affichage des données de métriques
[!INCLUDE [storage-selector-portal-enable-and-view-metrics](../../includes/storage-selector-portal-enable-and-view-metrics.md)]

## <a name="overview"></a>Vue d'ensemble
Storage Metrics est activé par défaut lorsque vous créez un compte de stockage. Vous pouvez configurer l’analyse à l’aide soit hello [portail classique Azure](https://manage.windowsazure.com), Windows PowerShell, ou par programmation via une API de stockage.

Lorsque vous activez Storage Metrics, vous devez choisir une période de rétention pour les données de salutation : cette période détermine pour le stockage de hello la durée pendant laquelle le service maintient les métriques hello et les frais de hello espace requis toostore les. En règle générale, vous devez utiliser une période de rétention plus courte pour les métriques par minute que pour les métriques en raison de l’espace supplémentaire hello requis pour les métriques par minute. Vous devez choisir une période de rétention telles que des données suffisantes temps tooanalyze hello et de télécharger les métriques que vous souhaitez tookeep pour une analyse hors ligne ou à des fins de création de rapports. N’oubliez pas que le téléchargement des données de métriques depuis votre compte de stockage est aussi facturé.

## <a name="how-tooenable-storage-metrics-using-hello-azure-classic-portal"></a>Comment tooenable Storage metrics à l’aide de hello portail classique Azure
Bonjour [portail classique Azure](https://manage.windowsazure.com), vous utilisez la page Configurer hello pour un toocontrol de compte de stockage des métriques de stockage. Pour la surveillance, vous pouvez définir un niveau et une période de rétention en jours pour chaque objet blob, table et file d’attente. Dans chaque cas, le niveau de hello est hello suivantes :

* Désactivée : aucune métrique n’est collectée.
* Minimal — Storage Metrics collecte un ensemble de base de métriques, notamment des entrées/sorties, la disponibilité, la latence et les pourcentages de réussite, qui sont ensuite regroupés pour les services Blob, Table et de file d’attente hello.
* Verbose : Collecte de métriques de stockage un jeu complet de métriques, notamment hello les mêmes métriques pour chaque opération de l’API de stockage, en outre toohello au niveau du service metrics. Les métriques détaillées permettent d’analyser plus précisément les problèmes survenant durant le fonctionnement d’une application.

Notez que hello portail classique Azure ne pas actuellement vous tooconfigure les métriques par minute dans votre compte de stockage ; Vous devez les activer à l’aide de PowerShell ou par programme.

## <a name="how-tooenable-storage-metrics-using-powershell"></a>Comment tooenable Storage metrics à l’aide de PowerShell
Vous pouvez utiliser PowerShell sur votre ordinateur local de tooconfigure Storage Metrics dans votre compte de stockage en utilisant les paramètres en cours hello du tooretrieve applet de commande Get-AzureStorageServiceMetricsProperty hello Azure PowerShell et hello applet de commande Set-AzureStorageServiceMetricsProperty toochange hello les paramètres actuels.

les applets de commande Hello qui contrôlent Storage Metrics utilisent hello paramètres suivants :

* MetricsType peut avoir pour valeur Hour ou Minute.
* ServiceType peut avoir pour valeur Blob, Queue ou Table.
* MetricsLevel les valeurs possibles sont None (tooOff équivalent Bonjour portail classique Azure), Service (équivalent tooMinimal Bonjour portail classique Azure) et ServiceAndApi (équivalent tooVerbose Bonjour portail classique Azure).

Par exemple, hello commande suivante active minute métriques pour le service d’objets blob hello dans votre compte de stockage par défaut avec la période de rétention hello de définir les jours de toofive :

```powershell
Set-AzureStorageServiceMetricsProperty -MetricsType Minute -ServiceType Blob -MetricsLevel ServiceAndApi  -RetentionDays 5
```
Hello commande suivante récupère hello actuel toutes les heures des métriques niveau et rétention en jours pour le service d’objets blob hello dans votre compte de stockage par défaut :

```powershell
Get-AzureStorageServiceMetricsProperty -MetricsType Hour -ServiceType Blob
```
Pour plus d’informations sur comment tooconfigure hello le toowork d’applets de commande Azure PowerShell avec votre abonnement Azure et comment tooselect hello du stockage par défaut de compte toouse, consultez : [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

## <a name="how-tooenable-storage-metrics-programmatically"></a>Comment tooenable Storage metrics par programmation
Hello suivant extrait de code c# montre comment tooenable métriques et la journalisation pour le service de l’objet Blob hello à l’aide hello bibliothèque cliente de stockage pour .NET :

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

// Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Enable Storage Analytics logging and set retention policy too10 days. 
ServiceProperties properties = new ServiceProperties();
properties.Logging.LoggingOperations = LoggingOperations.All;
properties.Logging.RetentionDays = 10;
properties.Logging.Version = "1.0";

// Configure service properties for metrics. Both metrics and logging must be set at hello same time.
properties.HourMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.HourMetrics.RetentionDays = 10;
properties.HourMetrics.Version = "1.0";

properties.MinuteMetrics.MetricsLevel = MetricsLevel.ServiceAndApi;
properties.MinuteMetrics.RetentionDays = 10;
properties.MinuteMetrics.Version = "1.0";

// Set hello default service version toobe used for anonymous requests.
properties.DefaultServiceVersion = "2015-04-05";

// Set hello service properties.
blobClient.SetServiceProperties(properties);
```

## <a name="viewing-storage-metrics"></a>Affichage des métriques de stockage
Lorsque vous avez configuré des métriques de stockage toomonitor votre compte de stockage, il enregistre les métriques hello dans un ensemble de tables connues dans votre compte de stockage. Vous pouvez utiliser la page de moniteur de hello pour votre compte de stockage dans le portail classique Azure tooview hello les métriques par heure de hello dès qu’elles sont disponibles sur un graphique. Dans cette page hello portail classique Azure, vous pouvez :

* Sélectionnez le tooplot métriques sur le graphique de hello (choix hello de métriques disponibles dépend de si vous avez choisi une surveillance détaillée ou minimale pour le service hello sur la page Configurer hello).
* Sélectionnez la plage de temps hello pour les métriques de hello affichées sur le graphique de hello.
* Choisissez toouse une métrique de hello tooplot l’échelle relative ou absolue.
* Configurer toonotify des alertes par courrier électronique lorsqu’une métrique spécifique atteint une certaine valeur.

Si vous souhaitez que les métriques de hello toodownload pour le stockage à long terme ou tooanalyze les localement, vous devez toouse un outil ou écrire du code de tables de hello tooread. Vous devez télécharger les métriques par minute hello pour analyse. les tables Hello n’apparaissent pas si vous répertoriez toutes les tables hello dans votre compte de stockage, mais vous pouvez y accéder directement par nom. Nombreux outils de consultation du stockage tiers ont connaissance de ces tables et vous permettre de tooview directement (consultez billet de blog hello [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) pour obtenir la liste des outils disponibles).

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

Vous trouverez des informations complètes sur les schémas hello pour ces tables, consultez [schéma de Table de métriques Storage Analytique](https://msdn.microsoft.com/library/azure/hh343264.aspx). lignes d’exemple Hello ci-dessous montrent uniquement un sous-ensemble de colonnes hello disponibles, mais illustrent certaines fonctionnalités importantes de façon hello que Storage Metrics enregistre ces métriques :

| PartitionKey | RowKey | Timestamp | TotalRequests | TotalBillableRequests | TotalIngress | TotalEgress | Availability | AverageE2ELatency | AverageServerLatency | PercentSuccess |
| --- |:---:| ---:| --- | --- | --- | --- | --- | --- | --- | --- |
| 20140522T1100 |user;All |2014-05-22T11:01:16.7650250Z |7 |7 |4003 |46801 |100 |104.4286 |6.857143 |100 |
| 20140522T1100 |user;QueryEntities |2014-05-22T11:01:16.7640250Z |5 |5 |2694 |45951 |100 |143.8 |7.8 |100 |
| 20140522T1100 |user;QueryEntity |2014-05-22T11:01:16.7650250Z |1 |1 |538 |633 |100 |3 |3 |100 |
| 20140522T1100 |user;UpdateEntity |2014-05-22T11:01:16.7650250Z |1 |1 |771 |217 |100 |9 |6 |100 |

Dans cet exemple de données de mesure des minutes, clé de partition hello sollicitent hello à la résolution d’une minute. clé de ligne Hello identifie le type hello des informations qui sont stockées dans la ligne de hello et elle se compose de deux éléments d’information, type d’accès hello et type de demande de hello :

* type d’accès Hello est utilisateur ou système, où utilisateur désigne le service de stockage tooall utilisateur demandes toohello et système toorequests apportées par stockage Analytique.
* type de demande de Hello est dans ce cas il s’agit d’une ligne de résumé, ou il identifie hello les API spécifiques telles que QueryEntity ou UpdateEntity.

données d’exemple Hello ci-dessus montre que tous les hello enregistre pour une seule minute (commence à 11 h 00), ce nombre de hello de demandes de QueryEntities plus hello nombre de demandes de QueryEntity plus nombre hello de demandes de UpdateEntity additionner tooseven, qui est hello total indiqué sur ligne d’user : All Hello. De même, vous pouvez dériver la latence de bout en bout moyenne hello (104,4286) sur la ligne d’user : All hello en calculant ((143.8 * 5) + 3 + 9) / 7.

Vous devez envisager de définir des alertes Bonjour portail classique Azure sur la page d’analyse hello afin que Storage Metrics puisse vous avertir automatiquement de toutes les modifications importantes de comportement hello de vos services de stockage. Si vous utilisez un toodownload d’outil de l’Explorateur de stockage de ces données métriques dans un format délimité, vous pouvez utiliser les données de Microsoft Excel tooanalyze hello. Consultez billet de blog hello [Microsoft Azure Storage Explorers](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx) pour obtenir la liste des outils de l’Explorateur de stockage disponible.

## <a name="accessing-metrics-data-programmatically"></a>Accès aux données de métriques par programmation
Hello ci-dessous montre exemple code c# qui accède aux métriques par minute hello pour une plage de minutes et affiche les résultats de hello dans une fenêtre de console. Il utilise hello version 4 incluant hello classe CloudAnalyticsClient qui simplifie l’accès aux tables de métriques hello dans le stockage de bibliothèque de stockage Azure.

```csharp
private static void PrintMinuteMetrics(CloudAnalyticsClient analyticsClient, DateTimeOffset startDateTime, DateTimeOffset endDateTime)
{
    // Convert hello dates toohello format used in hello PartitionKey
    var start = startDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");
    var end = endDateTime.ToUniversalTime().ToString("yyyyMMdd'T'HHmm");

    var services = Enum.GetValues(typeof(StorageService));
    foreach (StorageService service in services)
    {
        Console.WriteLine("Minute Metrics for Service {0} from {1} too{2} UTC", service, start, end);
        var metricsQuery = analyticsClient.CreateMinuteMetricsQuery(service, StorageLocation.Primary);
        var t = analyticsClient.GetMinuteMetricsTable(service);
        var opContext = new OperationContext();
        var query =
          from entity in metricsQuery
          // Note, you can't filter using hello entity properties Time, AccessType, or TransactionType
          // because they are calculated fields in hello MetricsEntity class.
          // hello PartitionKey identifies hello DataTime of hello metrics.
          where entity.PartitionKey.CompareTo(start) >= 0 && entity.PartitionKey.CompareTo(end) <= 0 
        select entity;

        // Filter on "user" transactions after fetching hello metrics from Table Storage.
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
Écrire des entités de table toocreate de demandes pour les métriques sont facturées au hello des frais standard applicables tooall Azure des opérations de stockage.

Les demandes de lecture et de suppression par une toometrics les données client sont aussi facturées au tarif standard. Si vous avez configuré une stratégie de rétention des données, vous n’êtes pas facturé quand Azure Storage supprime les anciennes données de métriques. Toutefois, si vous supprimez les données analytique, votre compte est facturé pour les opérations de suppression hello.

capacité de Hello utilisée par les tables de métriques hello est également facturable : vous pouvez utiliser hello suivant le montant de hello tooestimate de capacité utilisée pour stocker les données de métriques :

* Si chaque heure un service qui utilise des API de chaque service, environ 148 Ko de données sont stockée toutes les heures dans les tables de transaction de métriques hello si vous avez activé le service et le niveau de l’API résumé.
* Si chaque heure un service qui utilise des API de chaque service, environ 12 Ko de données sont stockée toutes les heures dans les tables de transaction de métriques hello si vous avez activé uniquement service au niveau du résumé.
* table de capacité pour les objets BLOB Hello a deux lignes sont ajoutées chaque jour (si l’utilisateur a activé les journaux) : cela signifie que chaque taille de hello jour de cette table augmente par des tooapproximately 300 octets.

## <a name="next-steps"></a>Étapes suivantes :
[Activation de la journalisation et accès aux données des journaux de stockage](https://msdn.microsoft.com/library/dn782840.aspx)
