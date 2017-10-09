---
title: aaaUse des compteurs de performances dans les Diagnostics Azure | Documents Microsoft
description: "Utilisez les compteurs de performances dans les services de cloud computing Azure ou les goulots d’étranglement de machine virtuelle toofind et régler les performances."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a>Créer et utiliser des compteurs de performances dans une application Azure
Cet article décrit les avantages hello et la façon dont les compteurs de performances de tooput dans votre application Windows Azure. Vous pouvez utiliser les données de toocollect, trouver des goulots d’étranglement et régler les performances des applications et système.

Compteurs de performances disponibles pour Windows Server, IIS et ASP.NET peuvent également être collectés et utilisés intégrité hello toodetermine vos rôles web Azure, les rôles de travail et les Machines virtuelles. Vous pouvez également créer et utiliser des compteurs de performance personnalisés.  

Vous pouvez examiner les données du compteur de performances

1. Directement sur l’hôte d’application hello avec l’outil d’analyse des performances hello accédé à l’aide du Bureau à distance
2. Avec System Center Operations Manager à l’aide de hello Azure Management Pack
3. Avec d’autres outils d’analyses qui accèdent aux hello des données de diagnostic transférées tooAzure stockage. Voir [Stocker et afficher des données de diagnostic dans Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) pour plus d’informations.  

Pour plus d’informations sur la surveillance des performances hello de votre application Bonjour [portail Azure](http://portal.azure.com/), consultez [comment les Services de cloud computing tooMonitor](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).

Pour des instructions détaillées supplémentaires sur la création d’un enregistrement et le suivi de stratégie et à l’aide des diagnostics et autres problèmes de tootroubleshoot techniques et optimiser les applications Azure, consultez [meilleures pratiques pour le développement de Azure de dépannage Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).

## <a name="enable-performance-counter-monitoring"></a>Activer la surveillance du compteur de performance
Les compteurs de performance ne sont pas activés par défaut. Votre application ou une tâche de démarrage doit modifier les tests de diagnostic hello par défaut que vous souhaitez toomonitor pour chaque instance de rôle des compteurs de performance spécifiques de l’agent configuration tooinclude hello.

### <a name="performance-counters-available-for-microsoft-azure"></a>Compteurs de performances disponibles pour Microsoft Azure
Azure fournit un sous-ensemble des compteurs de performances hello disponibles pour Windows Server, IIS et hello pile ASP.NET. Hello tableau suivant répertorie certains des compteurs de performance hello un intérêt particulier pour les applications Azure.

| Catégorie de compteur : Objet (Instance) | Nom de compteur | Référence |
| --- | --- | --- |
| Exceptions CLR .NET (*Global*) |Nombre d’exceptions levées/s |Compteurs de performance des exceptions |
| Mémoire CLR .NET (*Global*) |% de temps dans GC |Compteurs de performance mémoire |
| ASP.NET |L’application redémarre |Compteurs de performances pour ASP.NET |
| ASP.NET |Durée d’exécution de la demande |Compteurs de performances pour ASP.NET |
| ASP.NET |Requêtes déconnectées |Compteurs de performances pour ASP.NET |
| ASP.NET |Redémarrage du processus Worker |Compteurs de performances pour ASP.NET |
| Applications ASP.NET (**Total**) |Nombre Total de demandes |Compteurs de performances pour ASP.NET |
| Applications ASP.NET (**Total**) |Demandes/s |Compteurs de performances pour ASP.NET |
| ASP.NET v4.0.30319 |Durée d’exécution de la demande |Compteurs de performances pour ASP.NET |
| ASP.NET v4.0.30319 |Délai d’attente de demande |Compteurs de performances pour ASP.NET |
| ASP.NET v4.0.30319 |Demandes actuelles |Compteurs de performances pour ASP.NET |
| ASP.NET v4.0.30319 |Demandes en file d’attente |Compteurs de performances pour ASP.NET |
| ASP.NET v4.0.30319 |Demandes rejetées |Compteurs de performances pour ASP.NET |
| Mémoire |Nombre d’octets disponibles |Compteurs de performance mémoire |
| Mémoire |Octets dédiés |Compteurs de performance mémoire |
| Processor(_Total) |% temps processeur |Compteurs de performances pour ASP.NET |
| TCPv4 |Échecs de connexion |Objet TCP |
| TCPv4 |Connexions établies |Objet TCP |
| TCPv4 |Connexions réinitialisées |Objet TCP |
| TCPv4 |Segments envoyés/s |Objet TCP |
| Interface réseau(*) |Octets reçus/s |Objet d’interface réseau |
| Interface réseau(*) |Octets envoyés/s |Objet d’interface réseau |
| Interface réseau(Microsoft Virtual Machine Bus Network Adapter _2) |Octets reçus/s |Objet d’interface réseau |
| Interface réseau(Microsoft Virtual Machine Bus Network Adapter _2) |Octets envoyés/s |Objet d’interface réseau |
| Interface réseau(Microsoft Virtual Machine Bus Network Adapter _2) |Nombre total d’octets/s |Objet d’interface réseau |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a>Créer et ajouter l’application de tooyour de compteurs de performance personnalisés
Azure a toocreate de prise en charge et de modifier des compteurs de performances personnalisés pour les rôles web et worker. les compteurs de Hello peuvent être utilisé comportement de spécifiques à l’application tootrack et le moniteur. Vous pouvez créer et supprimer des catégories de compteurs de performance personnalisés et spécificateurs depuis une tâche de démarrage, un rôle web ou un rôle de travail avec des autorisations de niveau élevé.

> [!NOTE]
> Code qui apporte des modifications des compteurs de performance toocustom doit posséder des autorisations toorun élevés. Si le code de hello est dans un rôle web ou d’un rôle de travail, les rôles hello doivent inclure la balise de hello <Runtime executionContext="elevated" /> Bonjour ServiceDefinition.csdef du fichier pour hello rôle tooinitialize correctement.
>
>

Vous pouvez envoyer le stockage de tooAzure données compteur performances personnalisés à l’aide de l’agent de diagnostics hello.

données de compteur de performances standard Hello sont générées par hello Qu'azure traite. Les données du compteur de performance personnalisé doivent être créées par votre rôle web ou votre application de travail. Consultez [les Types de compteurs de performances](https://msdn.microsoft.com/library/z573042h.aspx) pour plus d’informations sur les types de données qui peuvent être stockées dans des compteurs de performances personnalisés hello. Voir [Exemple de compteurs de performance](http://code.msdn.microsoft.com/azure/) pour obtenir un exemple créant et définissant les données de compteurs de performance personnalisés dans un rôle web.

## <a name="store-and-view-performance-counter-data"></a>Stockez et affichez les données de compteur de performance
Azure met en mémoire cache les données de compteur de performance avec d’autres informations de diagnostic. Ces données sont disponibles pour l’analyse à distance alors que l’instance de rôle hello est en cours d’exécution à l’aide des outils de tooview accès Bureau à distance tels que l’Analyseur de performances. toopersist hello en dehors de l’instance de rôle hello, agent de diagnostics hello doit de transfert de données stockage tooAzure hello. limite de taille de Hello de données de compteur de performance hello mis en cache peut être configurée dans l’agent de diagnostics hello, ou il peut être configuré partie toobe d’une limite partagée pour toutes les hello des données de diagnostic. Pour plus d’informations sur la définition de taille de mémoire tampon hello, consultez [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) et [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx). Consultez [Store et afficher les données de Diagnostic dans le stockage Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) pour une vue d’ensemble de la configuration d’un compte de stockage hello diagnostics agent tootransfer données tooa.

Chaque instance de compteur de performances configurée est enregistrée à un taux d’échantillonnage spécifié et les données hello échantillonnée sont transférées toohello compte de stockage par une demande de transfert planifiée ou une demande de transfert. Les transferts automatiques peuvent être planifiés au maximum une fois par minute. Les données de compteur de performance transférées par l’agent de diagnostics hello sont stockées dans une table, WADPerformanceCountersTable, hello compte de stockage. Cette table peut-être accessible et interrogée avec les méthodes de l’API standard de stockage Azure. Consultez [Microsoft Azure PerformanceCounters exemple](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) pour obtenir un exemple d’interrogation et affichage des données de compteur de performance à partir de la table de WADPerformanceCountersTable hello.

> [!NOTE]
> Selon la fréquence de transfert de l’agent de diagnostics hello et la latence de la file d’attente, hello dernières données de compteur de performance dans le compte de stockage hello peuvent être obsolète de plusieurs minutes.
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a>Activer les compteurs de performance à l’aide du fichier de configuration de diagnostics
Utilisez hello suivant des compteurs de performance tooenable procédure dans votre application Windows Azure.

## <a name="prerequisites"></a>Composants requis
Cette section suppose que vous avez importé le moniteur de diagnostic hello dans votre application ajoutée hello diagnostics configuration fichier tooyour solution Visual Studio (2.4 du Kit de développement logiciel et en dessous de diagnostics.wadcfg ou diagnostics.wadcfgx dans le SDK 2.5 et versions ultérieures). Voir les étapes 1 et 2 dans [Activation de Diagnostics dans Azure Cloud Services et Virtual Machines](cloud-services-dotnet-diagnostics.md)pour plus d’informations.

## <a name="step-1-collect-and-store-data-from-performance-counters"></a>Étape 1 : collecte et stockage de données de compteurs de performances
Après avoir ajouté les diagnostics hello du fichier solution Visual Studio de tooyour, vous pouvez configurer la collecte de hello et le stockage des données de compteur de performances dans une application Windows Azure. Pour cela, vous devez ajouter le fichier diagnostics de performances des compteurs toohello. Les données de diagnostic, y compris les compteurs de performance, sont d’abord collectées sur l’instance de hello. les données de salutation sont persistante toohello WADPerformanceCountersTable table hello service Table Azure, afin que vous également besoin toospecify hello compte de stockage dans votre application. Si vous testez votre application localement dans hello émulateur de calcul, vous pouvez également stocker localement les données de diagnostic Bonjour émulateur de stockage. Avant de stocker les données de diagnostic, vous devez tout d’abord accéder toohello [portail Azure](http://portal.azure.com/) et créer un compte de stockage classique. La meilleure pratique consiste à toolocate dans votre compte de stockage hello même emplacement géographique que votre application Windows Azure. En conservant les hello, compte d’application et de stockage Azure sont dans Bonjour même emplacement géographique, éviter les coûts externes de bande passante et de réduire la latence.

### <a name="add-performance-counters-toohello-diagnostics-file"></a>Ajouter le fichier de diagnostics de performances des compteurs toohello
Il existe de nombreux compteurs que vous pouvez utiliser. Hello suivant montre plusieurs compteurs de performances sont recommandés pour le web et le rôle de travail analyse.

Ouvrir le fichier de diagnostics hello (diagnostics.wadcfg dans le SDK 2.4 et versions antérieures ou diagnostics.wadcfgx dans le SDK 2.5 et versions ultérieures) et ajouter hello suivant toohello DiagnosticMonitorConfiguration élément :

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

attribut de bufferQuotaInMB Hello, qui spécifie la quantité maximale de hello du stockage de système de fichiers est disponible pour le type de collection de données hello (journaux Azure, les journaux IIS, etc.). valeur par défaut Hello est 0. Lorsque hello quota est atteint, les données les plus anciennes hello sont supprimées que les nouvelles données sont ajoutées. somme de Hello de toutes les propriétés de bufferQuotaInMB hello doit être supérieur à valeur d’attribut de OverallQuotaInMB hello hello. Pour obtenir une présentation plus détaillée de détermination de la quantité de stockage requise pour la collection hello de données de diagnostic, consultez hello section des diagnostics Windows AZURE le programme d’installation de [meilleures pratiques pour développer des Applications Azure de dépannage](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).

attribut de scheduledTransferPeriod Bonjour, qui spécifie l’intervalle de salutation entre les transferts de données planifiés, arrondi toohello minute la plus proche. Bonjour exemple suivant, il a la valeur tooPT30M (30 minutes). Paramètre hello transfert tooa période petite valeur, telle qu’une minute, impact négatif sur les performances de votre application en production, mais peut être utile pour afficher les diagnostics rapidement lorsque vous testez. période de transfert planifiée Hello doit être suffisamment petit tooensure que les données de diagnostic ne sont pas remplacées sur hello instance, mais suffisamment grand pour qu’elle n’affectera pas les performances hello de votre application.

attribut de counterSpecifier Hello spécifie toocollect de compteur de performances hello. attribut de sampleRate Hello spécifie hello fréquence à laquelle compteur de performances hello doit être échantillonné, dans ce cas 30 secondes.

Une fois que vous avez ajouté des compteurs de performance de hello que vous souhaitez toocollect, enregistrez votre fichier de diagnostics de toohello de modifications. Ensuite, vous devez le compte de stockage de hello toospecify les données de diagnostic hello sont rendues persistantes dans.

### <a name="specify-hello-storage-account"></a>Spécifiez le compte de stockage hello
toopersist votre tooyour d’informations de diagnostics Azure Storage de compte, vous devez spécifier une chaîne de connexion dans votre fichier de configuration (ServiceConfiguration.cscfg) du service.

Pour Azure SDK 2.5, hello compte de stockage peut être spécifiée dans le fichier diagnostics.wadcfgx de hello.

> [!NOTE]
> Ces instructions s’appliquent uniquement tooAzure SDK 2.4 et versions antérieures. Pour Azure SDK 2.5, hello compte de stockage peut être spécifiée dans le fichier diagnostics.wadcfgx de hello.
>
>

chaînes de connexion tooset hello :

1. Ouvrir le fichier de ServiceConfiguration.Cloud.cscfg hello à l’aide de votre éditeur de texte et la chaîne de connexion de hello de jeu de votre stockage. Hello *AccountName* et *AccountKey* valeurs trouvent Bonjour Azure portal tableau de bord de compte de stockage hello, sous les clés d’accès.

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. Enregistrez le fichier ServiceConfiguration.Cloud.cscfg de hello.
3. Ouvrez le fichier ServiceConfiguration.Local.cscfg de hello et vérifiez que UseDevelopmentStorage est tootrue.

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   Maintenant que les chaînes de connexion hello sont définis, votre application persisteront compte de stockage de diagnostics données tooyour lorsque votre application est déployée.
4. Enregistrez et générez votre projet, puis déployez votre application.

## <a name="step-2-optional-create-custom-performance-counters"></a>Étape 2 : (facultatif) création de compteurs de performances personnalisés
Toohello prédéfinis en outre les compteurs de performances, vous pouvez ajouter que vos propres performances personnalisés compteurs toomonitor des rôles web ou de travail. Compteurs de performances personnalisés peuvent utilisé de comportement tootrack et analyse spécifiques à l’application et peut être créés ou supprimés dans une tâche de démarrage, un rôle web ou un rôle de travail avec des autorisations élevées.

l’agent de diagnostics Windows Azure Hello actualise hello compteur configuration de performances à partir du fichier .wadcfg de hello une minute après le démarrage.  Si vous créez des compteurs de performances personnalisés dans hello OnStart (méthode) et vos tâches de démarrage prennent plus de tooexecute d’une minute, les compteurs de performance personnalisés ne seront pas créées lorsque l’agent de Diagnostics Windows Azure hello tente tooload les.  Dans ce scénario, vous verrez qu’Azure Diagnostics capture correctement toutes les données de diagnostic, excepté les compteurs de performance personnalisés.  tooresolve ce problème, créez des compteurs de performance de hello dans une tâche de démarrage ou déplacer certaines de vos tâches de démarrage de travail après la création des compteurs de performance hello toohello OnStart (méthode).

Effectuez hello suivant les étapes toocreate un compteur nommé « \MyCustomCounterCategory\MyButton1Counter » de performances personnalisé simple :

1. Ouvrez le fichier de définition hello service (CSDEF) de votre application.
2. Ajoutez hello élément toohello WebRole ou WorkerRole élément tooallow exécution avec des privilèges élevés :

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. Enregistrez le fichier de hello.
4. Ouvrir le fichier de diagnostics hello (diagnostics.wadcfg dans le SDK 2.4 et versions antérieures ou diagnostics.wadcfgx dans le SDK 2.5 et versions ultérieures) et ajouter hello suivant toohello DiagnosticMonitorConfiguration

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. Enregistrez le fichier de hello.
6. Créer la catégorie de compteur de performances personnalisés hello dans la méthode OnStart de hello de votre rôle, avant d’appeler la base de. OnStart. Hello exemple c# suivant crée une catégorie personnalisée, s’il n’existe pas déjà :

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. Mettre à jour les compteurs hello dans votre application. Bonjour à l’exemple suivant met à jour un compteur de performance personnalisé sur les événements Button1_Click :

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. Enregistrez le fichier de hello.  

Les données de compteur de performances personnalisés seront désormais collectées par le moniteur de diagnostic Azure hello.

## <a name="step-3-query-performance-counter-data"></a>Étape 3 : interrogation des données de compteurs de performances
Une fois que votre application est déployée et en cours d’exécution, moniteur de diagnostic hello commence la collecte des compteurs de performances et la conservation de ce stockage tooAzure de données. Vous utilisez des outils tels que l’Explorateur de serveurs dans Visual Studio, [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), ou [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) de Cerebrata des compteurs de performance de hello tooview données Bonjour Table WADPerformanceCountersTable. Vous pouvez également programmer interroger à l’aide de service de Table hello [c#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), ou [PHP](../cosmos-db/table-storage-how-to-use-php.md).

Hello exemple c# suivant illustre une requête de base dans la table de WADPerformanceCountersTable hello et enregistre le fichier CSV tooa hello diagnostics données. Une fois que les compteurs de performances hello enregistrés tooa un fichier CSV, vous pouvez utiliser hello des fonctionnalités dans Microsoft Excel ou d’autres données de hello de toovisualize outil de création de graphiques. Être vraiment tooadd tooMicrosoft.WindowsAzure.Storage.dll une référence, qui est inclus dans hello Azure SDK pour .NET octobre 2012 et versions ultérieur. l’assembly Hello est installée toohello % programme Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ active.

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

Objets tooC # à l’aide d’une classe personnalisée dérivée de mappent des entités **TableEntity**. Hello de code suivant définit une classe d’entité qui représente un compteur de performances hello **WADPerformanceCountersTable** table.

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a>Étapes suivantes
[Afficher d’autres articles sur les diagnostics Azure](../azure-diagnostics.md)
