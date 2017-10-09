---
title: "aaaStreaming des données de Diagnostics Azure dans le chemin d’accès à chaud hello à l’aide de concentrateurs d’événements | Documents Microsoft"
description: "Configuration des Diagnostics Azure avec des concentrateurs d’événements de fin tooend, y compris des instructions pour les scénarios courants."
services: event-hubs
documentationcenter: na
author: rboucher
manager: carmonm
editor: 
ms.assetid: edeebaac-1c47-4b43-9687-f28e7e1e446a
ms.service: monitoring-and-diagnostics
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: robb
ms.openlocfilehash: a2528ddd0688d1c23a8631e769ca016dd79e4159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-azure-diagnostics-data-in-hello-hot-path-by-using-event-hubs"></a>Diffusion en continu des données de Diagnostics Azure dans le chemin réactif hello à l’aide de concentrateurs d’événements
Diagnostics Azure fournit des méthodes souples toocollect métriques et des journaux à partir de cloud services virtual machines virtuelles et de transférer les résultats tooAzure stockage. À compter de l’intervalle de temps hello mars 2016 (Kit de développement logiciel 2.9), vous pouvez envoyer Diagnostics toocustom des sources de données et transférer des données de chemin réactif en secondes à l’aide de [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).

Les types de données pris en charge sont les suivants :

* Suivi d’événements pour les événements Windows (ETW)
* Compteurs de performances
* Journaux d’événements Windows
* Journaux d’application
* Journaux d’infrastructure de diagnostics Azure

Cet article explique comment tooconfigure Azure Diagnostics avec les concentrateurs d’événements de fin tooend. Aucune aide est également fournie pour hello les scénarios courants suivants :

* Mode de journalisation des toocustomize hello et métriques envoyées tooEvent concentrateurs
* Comment les configurations toochange dans chaque environnement
* Comment tooview concentrateurs d’événements de flux de données
* Comment tootroubleshoot hello connexion  

## <a name="prerequisites"></a>Composants requis
Des données receieving de concentrateurs d’événements à partir d’Azure Diagnostics sont prise en charge dans les Services de cloud computing, machines virtuelles, machines virtuelles identiques et l’infrastructure de Service à partir de hello Azure SDK 2.9 et hello correspondant Windows Azure Tools pour Visual Studio.

* Extension Azure Diagnostics 1.6 (ciblée par défaut par le[Kit de développement logiciel (SDK) Azure pour .NET 2.9 ou ultérieur](https://azure.microsoft.com/downloads/) )
* [Visual Studio 2013 ou une version ultérieure](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* Des configurations de Diagnostics Azure dans une application à l’aide un *.wadcfgx* fichier et l’une des méthodes suivantes de hello :
  * Visual Studio : [Configuration de Diagnostics pour les services cloud et les machines virtuelles Azure](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)
  * Windows PowerShell : [Activer les diagnostics dans Services cloud Azure à l’aide de PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)
* Espace de noms de concentrateurs événements mis en service par l’article hello, [prise en main les concentrateurs d’événements](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

## <a name="connect-azure-diagnostics-tooevent-hubs-sink"></a>Se connecter à Azure Diagnostics tooEvent concentrateurs récepteur
Par défaut, les Diagnostics Windows Azure envoie toujours des journaux et des métriques tooan compte de stockage Azure. Une application peut également envoyer des données tooEvent concentrateurs en ajoutant un nouvel **récepteurs** section sous hello **PublicConfig** / **WadCfg** élément Hello *.wadcfgx* fichier. Dans Visual Studio, hello *.wadcfgx* fichier est stocké dans hello suivant le chemin d’accès : **projet de Service Cloud** > **rôles** > **() RoleName)** > **diagnostics.wadcfgx** fichier.

```xml
<SinksConfig>
  <Sink name="HotPath">
    <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" />
  </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "HotPath",
            "EventHub": {
                "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
                "SharedAccessKeyName": "SendRule"
            }
        }
    ]
}
```

Dans cet exemple, le concentrateur d’événements hello URL a la valeur toohello entièrement qualifié espace de noms du hub d’événements hello : espace de noms de concentrateurs d’événements + « / » + nom de hub d’événements.  

concentrateur d’événements Hello URL s’affiche dans hello [portail Azure](http://go.microsoft.com/fwlink/?LinkID=213885) sur le tableau de bord hello concentrateurs d’événements.  

Hello **récepteur** nom peut être défini tooany les chaîne valide tant que hello même valeur est utilisée par tout au long de fichier de configuration hello.

> [!NOTE]
> Des récepteurs supplémentaires, tels que *applicationInsights* , peuvent être configurés dans cette section. Diagnostics Azure permet à un ou plusieurs récepteurs toobe défini si chaque récepteur est également déclaré dans hello **PrivateConfig** section.  
>
>

Hello concentrateurs d’événements récepteur doit également être déclaré et défini dans hello **PrivateConfig** section Hello *.wadcfgx* le fichier de configuration.

```XML
<PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <StorageAccount name="{account name}" key="{account key}" endpoint="{optional storage endpoint}" />
  <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
</PrivateConfig>
```
```JSON
{
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{optional storage endpoint}",
    "EventHub": {
        "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    }
}
```

Hello `SharedAccessKeyName` valeur doit correspondre à une clé de Signature d’accès partagé (SAP) et la stratégie qui a été défini dans hello **concentrateurs d’événements** espace de noms. Parcourir le tableau de bord de concentrateurs d’événements toohello Bonjour [portail Azure](https://manage.windowsazure.com), cliquez sur hello **configurer** onglet et définir une stratégie nommée (par exemple, « SendRule ») qui a *envoyer* autorisations. Hello **StorageAccount** est également déclaré dans **PrivateConfig**. Il n’est pas nécessaire ici les valeurs toochange s’ils fonctionnent. Dans cet exemple, nous ne renseignez pas les valeurs hello, qui est un signe qu’un composant en aval définira les valeurs hello. Par exemple, hello *ServiceConfiguration.Cloud.cscfg* fichier de configuration d’environnement définit les noms d’environnement approprié hello et les clés.  

> [!WARNING]
> la clé SAS de concentrateurs d’événements de Hello est stockée en texte brut dans hello *.wadcfgx* fichier. Souvent, cette clé est activée dans le contrôle de code toosource ou n’est disponible en tant qu’un élément multimédia dans votre serveur de builds, vous devez donc protéger il comme il convient. Nous vous recommandons d’utiliser une clé SAS ici avec *envoyer uniquement* autorisations afin qu’un utilisateur malveillant peut écrire toohello concentrateur d’événements, mais pas écouter tooit ou le gérer.
>
>

## <a name="configure-azure-diagnostics-toosend-logs-and-metrics-tooevent-hubs"></a>Configurer les Diagnostics Azure toosend métriques et journaux tooEvent concentrateurs
Comme indiqué précédemment, tous les par défaut et les données de diagnostic personnalisé, autrement dit, mesures et les journaux, est automatiquement envoyé tooAzure stockage dans des intervalles de salutation configurée. Avec des concentrateurs d’événements et n’importe quel récepteur supplémentaire, vous pouvez spécifier n’importe quel nœud racine ou feuille dans toobe de hiérarchie hello envoyé toohello concentrateur d’événements. Cela inclut les événements ETW, les compteurs de performances, les journaux des événements Windows et les journaux d’application.   

Il est important de tooconsider combien de points de données doit être transférées tooEvent concentrateurs. En règle générale, les développeurs transfèrent des données de chemin réactif à faible latence qui doivent être consommées et interprétées rapidement. Il s’agit, par exemple, des systèmes qui analysent les alertes ou les règles de mise à l’échelle automatique. Un développeur peut également configurer un autre magasin d’analyse ou de recherche, par exemple, Azure Stream Analytics, ElasticSearch, un système de surveillance personnalisé ou un système de surveillance tiers favori.

Hello Voici quelques exemples de configuration.

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "sinks": "HotPath",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        }
    ]
}
```

Bonjour exemple ci-dessus, l’intercepteur hello est appliqué toohello parent **PerformanceCounters** nœud dans la hiérarchie de hello, ce qui signifie que tous les enfants **PerformanceCounters** tooEvent Hubs sera envoyé.  

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" sinks="HotPath" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" sinks="HotPath"/>
  <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" sinks="HotPath"/>
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Rejected",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Queued",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        }
    ]
}
```

Dans l’exemple précédent de hello, récepteur de hello est appliqué tooonly trois compteurs : **en file d’attente de demandes**, **demandes rejetées**, et **% temps processeur**.  

Hello suivant montre comment un développeur peut limiter la quantité hello données envoyées toobe hello métriques critiques qui sont utilisés pour le contrôle d’intégrité de ce service.  

```XML
<Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
```
```JSON
"Logs": {
    "scheduledTransferPeriod": "PT1M",
    "scheduledTransferLogLevelFilter": "Error",
    "sinks": "HotPath"
}
```

Dans cet exemple, le récepteur de hello est toologs appliqués et filtré de suivi de niveau tooerror uniquement.

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a>Déploiement et mise à jour d’une configuration de diagnostics et d’application de services cloud
Visual Studio fournit l’application hello plus simple chemin d’accès toodeploy hello et configuration de récepteur de concentrateurs d’événements. fichier hello tooview et modifier, ouvrez hello *.wadcfgx* de fichiers dans Visual Studio, modifiez-le, puis enregistrez-le. chemin d’accès Hello est **projet de Service Cloud** > **rôles** > **(RoleName)** > **diagnostics.wadcfgx**.  

À ce stade, tous les déploiement déploiement mise à jour et des actions dans Visual Studio, Visual Studio Team System et toutes les commandes ou scripts qui sont basés sur MSBuild et utilisent hello **/t : publier** cible incluent hello *.wadcfgx*  dans le processus d’empaquetage hello. En outre, les mises à jour et les déploiements déploiement hello fichier tooAzure à l’aide d’extension de l’agent de Diagnostics Azure appropriée hello sur vos machines virtuelles.

Après avoir déployé l’application hello et configuration des Diagnostics Windows Azure, vous verrez immédiatement l’activité dans le tableau de bord de hello du concentrateur d’événements hello. Cela indique que vous êtes prêt toomove sur les données de chemin d’accès à chaud tooviewing hello dans hello écouteur client ou l’analyse de l’outil de votre choix.  

Dans la figure suivante de hello, tableau de bord de concentrateurs d’événements hello affiche envoi intègre de démarrage de diagnostics données toohello événement hub après 23 h 00. C'est-à-dire quand hello application a été déployée avec une mise à jour *.wadcfgx* de fichiers et hello récepteur a été configuré correctement.

![][0]  

> [!NOTE]
> Lorsque vous modifiez le fichier de configuration de Diagnostics Azure mises à jour toohello (.wadcfgx), il est recommandé que vous effectuez un push hello mises à jour toohello ensemble de l’application, ainsi qu’une configuration de hello à l’aide de la publication dans Visual Studio, ou un script Windows PowerShell.  
>
>

## <a name="view-hot-path-data"></a>Affichage des données de chemin réactif
Comme indiqué précédemment, il existe plusieurs cas d’usage pour l’écoute tooand le traitement des données de concentrateurs d’événements.

Une approche simple est toocreate un concentrateur d’événements de test peu console application toolisten toohello et impression hello le flux de sortie. Vous pouvez placer hello suivant de code, qui est expliquée plus en détail dans [prise en main les concentrateurs d’événements](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), dans une application console.  

Notez que les applications de console hello doivent inclure hello [événement processeur hôte NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).  

N’oubliez pas de valeurs de hello tooreplace figurant entre crochets Bonjour **Main** fonction avec des valeurs pour vos ressources.   

```csharp
//Console application code for EventHub test client
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.ServiceBus.Messaging;

namespace EventHubListener
{
    class SimpleEventProcessor : IEventProcessor
    {
        Stopwatch checkpointStopWatch;

        async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
            if (reason == CloseReason.Shutdown)
            {
                await context.CheckpointAsync();
            }
        }

        Task IEventProcessor.OpenAsync(PartitionContext context)
        {
            Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
            this.checkpointStopWatch = new Stopwatch();
            this.checkpointStopWatch.Start();
            return Task.FromResult<object>(null);
        }

        async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (EventData eventData in messages)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                    Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                        context.Lease.PartitionId, data));

                foreach (var x in eventData.Properties)
                {
                    Console.WriteLine(string.Format("    {0} = {1}", x.Key, x.Value));
                }
            }

            //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
            if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
            {
                await context.CheckpointAsync();
                this.checkpointStopWatch.Restart();
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string eventHubConnectionString = "Endpoint= <your connection string>”
            string eventHubName = "<Event hub name>";
            string storageAccountName = "<Storage account name>";
            string storageAccountKey = "<Storage account key>”;
            string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);

            string eventProcessorHostName = Guid.NewGuid().ToString();
            EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
            Console.WriteLine("Registering EventProcessor...");
            var options = new EventProcessorOptions();
            options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
            eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();

            Console.WriteLine("Receiving. Press enter key toostop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a>Résolution des problèmes liés aux récepteurs Event Hubs
* concentrateur d’événements Hello n’affiche pas l’activité d’événements entrants ou sortants comme prévu.

    Vérifiez que le hub d’événements a été correctement approvisionné. Toutes les informations de connexion dans hello **PrivateConfig** section de *.wadcfgx* doit correspondre à valeurs hello de votre ressource, comme indiqué dans le portail de hello. Assurez-vous que vous disposez d’une SAS stratégie définie (« SendRule » dans l’exemple de hello) dans le portail de hello et qui *envoyer* l’autorisation est accordée.  
* Après une mise à jour, concentrateur d’événements hello n’affiche plus activité d’événement entrant ou sortant.

    Tout d’abord, vérifiez que ce concentrateur d’événements hello et informations de configuration sont correcte, comme expliqué précédemment. Parfois hello **PrivateConfig** est réinitialisée dans une mise à jour du déploiement. Hello recommandé de correctif toomake toutes les modifications trop*.wadcfgx* hello du projet et ensuite, pour ajouter une mise à jour de l’application complète. Si ce n’est pas possible, assurez-vous que cette mise à jour des diagnostics hello pousse complète **PrivateConfig** qui inclut la clé SAS hello.  
* J’ai essayé les suggestions hello et concentrateur d’événements hello fonctionne toujours pas.

    Recherchez dans la table de stockage Azure hello qui contient des erreurs et des journaux de Diagnostics Azure lui-même : **WADDiagnosticInfrastructureLogsTable**. Une option consiste à toouse un outil tel que [Azure Storage Explorer](http://www.storageexplorer.com) compte de stockage tooconnect toothis, afficher ce tableau et ajouter une requête pour l’horodatage Bonjour des dernières 24 heures. Vous pouvez utiliser l’outil de hello tooexport un fichier .csv et ouvrez-le dans une application telle que Microsoft Excel. Excel rend toosearch facile pour les chaînes de la carte d’appel, tels que **EventHubs**, toosee d’indiquer l’erreur est signalée.  

## <a name="next-steps"></a>Étapes suivantes
•    [En savoir plus sur Event Hubs](https://azure.microsoft.com/services/event-hubs/)

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a>Annexe : Exemple de fichier de configuration d’Azure Diagnostics (.wadcfgx)
```xml
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticsConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <WadCfg>
      <DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="applicationInsights.errors">
        <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error" />
        <Directories scheduledTransferPeriod="PT1M">
          <IISLogs containerName="wad-iis-logfiles" />
          <FailedRequestLogs containerName="wad-failedrequestlogs" />
        </Directories>
        <PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
        </PerformanceCounters>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*" />
        </WindowsEventLog>
        <CrashDumps>
          <CrashDumpConfiguration processName="WaIISHost.exe" />
          <CrashDumpConfiguration processName="WaWorkerHost.exe" />
          <CrashDumpConfiguration processName="w3wp.exe" />
        </CrashDumps>
        <Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
      </DiagnosticMonitorConfiguration>
      <SinksConfig>
        <Sink name="HotPath">
          <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" />
        </Sink>
        <Sink name="applicationInsights">
          <ApplicationInsights />
          <Channels>
            <Channel logLevel="Error" name="errors" />
          </Channels>
        </Sink>
      </SinksConfig>
    </WadCfg>
    <StorageAccount>ACCOUNT_NAME</StorageAccount>
  </PublicConfig>
  <PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <StorageAccount name="{account name}" key="{account key}" endpoint="{storage endpoint}" />
    <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" SharedAccessKey="YOUR_KEY_HERE" />
  </PrivateConfig>
  <IsEnabled>true</IsEnabled>
</DiagnosticsConfiguration>
```

Hello complémentaire *ServiceConfiguration.Cloud.cscfg* pour cet exemple se présente comme hello suivant.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="MyFixItCloudService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2015-04.2.6">
  <Role name="MyFixIt.WorkerRole">
    <Instances count="1" />
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="YOUR_CONNECTION_STRING" />
    </ConfigurationSettings>
  </Role>
</ServiceConfiguration>
```

Les paramètres équivalents JSON pour les machines virtuelles sont les suivants :
```JSON
"settings": {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 4096,
            "sinks": "applicationInsights.errors",
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "Directories": {
                "scheduledTransferPeriod": "PT1M",
                "IISLogs": {
                    "containerName": "wad-iis-logfiles"
                },
                "FailedRequestLogs": {
                    "containerName": "wad-failedrequestlogs"
                }
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "sinks": "HotPath",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Memory\\Available MBytes",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\Bytes Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Requests/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Errors Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Queued",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Rejected",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT3M"
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT1M",
                "DataSource": [
                    {
                        "name": "Application!*"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Error",
                "sinks": "HotPath"
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "HotPath",
                    "EventHub": {
                        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
                        "SharedAccessKeyName": "SendRule"
                    }
                },
                {
                    "name": "applicationInsights",
                    "ApplicationInsights": "",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "errors"
                            }
                        ]
                    }
                }
            ]
        }
    },
    "StorageAccount": "{account name}"
}


"protectedSettings": {
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{storage endpoint}",
    "EventHub": {
        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "YOUR_KEY_HERE"
    }
}
```

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :

* [Vue d’ensemble des hubs d’événements](../event-hubs/event-hubs-what-is-event-hubs.md)
* [Créer un concentrateur d’événements](../event-hubs/event-hubs-create.md)
* [FAQ sur les hubs d'événements](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
