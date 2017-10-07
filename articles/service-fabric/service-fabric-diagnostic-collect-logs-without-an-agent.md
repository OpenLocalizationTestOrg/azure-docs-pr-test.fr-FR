---
title: "aaaCollect journaux directement à partir d’un Service Azure Fabric processus du service | Microsoft Azure"
description: "Décrit le Service Fabric, les applications peuvent envoyer les journaux directement tooa point central comme Azure Application Insights ou Elasticsearch, sans se baser sur l’agent de Diagnostics Windows Azure."
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: rwike77
editor: 
ms.assetid: ab92c99b-1edd-4677-8c28-4e591d909b47
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/18/2017
ms.author: karolz
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: d0681a2a6aaa76028d7cb469c31c006f24bbe954
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a>Collecter les journaux directement à partir d’un processus de service Azure Service Fabric
## <a name="in-process-log-collection"></a>Collecte de journaux dans le processus
Collecte d’application connecte à l’aide de [extension Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) est une bonne option pour **Azure Service Fabric** services si set hello de journal sources et destinations est petite, ne change pas souvent et il est un mappage simple entre des sources de hello et leurs destinations. Si ce n’est pas le cas, une autre solution consiste à toohave services envoyer les journaux directement tooa point central. Ce processus, appelé **collecte de journaux dans le processus**, présente plusieurs avantages potentiels :

* *Simplicité de configuration et de déploiement*

    * configuration de Hello de collecte de données de diagnostic est simplement dans le cadre de la configuration du service hello. Il s’agit de conserver facilement tooalways « synchronisé » avec hello il le reste de l’application hello.
    * Vous pouvez facilement réaliser une configuration par application ou par service.
        * Collection basée sur l’agent du journal nécessite généralement un déploiement séparé et la configuration de l’agent de diagnostic hello, qui est une tâche administrative supplémentaire et une source potentielle d’erreurs. Il existe souvent qu’une seule instance d’agent hello autorisé par l’ordinateur virtuel (nœud) et configuration de l’agent hello est partagée entre toutes les applications et services en cours d’exécution sur ce nœud. 

* *Flexibilité*
   
    * application Hello peut envoyer des données de hello qu’elle puisse toogo, tant qu’il existe une bibliothèque de client qui prend en charge le système de stockage de données hello ciblé. Vous pouvez ajouter de nouvelles destinations selon vos besoins.
    * Vous pouvez également implémenter des règles de capture, de filtrage et d’agrégation de données complexes.
    * Collection basée sur l’agent du journal est souvent limitée par les récepteurs de données hello hello prend en charge de l’agent. Certains agents sont extensibles.

* *Contexte et des données d’application toointernal accès*
   
    * sous-système de diagnostic Hello en cours d’exécution à l’intérieur du processus de service ou application hello peut accroître facilement les traces hello avec des informations contextuelles.
    * Collection basée sur l’agent de journal hello données doivent être envoyées agent tooan via un mécanisme de communication entre processus, tels que le suivi d’événements pour Windows. Ce mécanisme peut imposer des limites supplémentaires.

Il est possible toocombine et tirent parti de ces deux méthodes de collection. En effet, il peut être la meilleure solution hello pour de nombreuses applications. Collection basée sur l’agent est une solution naturelle pour la collecte de journaux associés toohello ensemble du cluster et les nœuds de cluster individuels. C’est un moyen beaucoup plus fiable, à la collection dans le processus du journal et les incidents, des problèmes de démarrage du service toodiagnose. En outre, avec de nombreux services en cours d’exécution à l’intérieur d’un cluster Service Fabric, chaque service effectuant sa propre collection de traitement du journal entraîne grand nombre de connexions sortante à partir du cluster de hello. Grand nombre de connexions sortantes est difficile à la fois pour le sous-système de réseau hello et de destination du journal hello. Un agent tel qu’[**Azure Diagnostics** ](../cloud-services/cloud-services-dotnet-diagnostics.md) peut collecter les données de plusieurs services et envoyer toutes ces données via un nombre réduit de connexions, ce qui améliore le débit. 

Dans cet article, nous montrons comment tooset un processus d’inscription du journal à l’aide de la collection [ **bibliothèque open source de EventFlow**](https://github.com/Azure/diagnostics-eventflow). Autres bibliothèques peuvent être utilisées pour hello même objectif, mais EventFlow offre hello d’ayant été conçu spécifiquement pour les services Service Fabric intra-processus journal toosupport et de la collection. Nous utilisons [ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/) en tant que destination de journal hello. D’autres destinations telles qu’[**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) ou [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) sont également prises en charge. Il s’agit simplement d’une question de l’installation de package NuGet approprié et de configuration de destination de hello dans le fichier de configuration EventFlow hello. Pour plus d’informations sur les destinations de journaux autres qu’Application Insights, consultez la [documentation relative à EventFlow](https://github.com/Azure/diagnostics-eventflow).

## <a name="adding-eventflow-library-tooa-service-fabric-service-project"></a>Ajout de projet de service Service Fabric EventFlow bibliothèque tooa
Les fichiers binaires EventFlow sont disponibles sous la forme d’un ensemble de packages NuGet. tooadd projet de service Service Fabric EventFlow tooa, avec le bouton droit de projet hello Bonjour l’Explorateur de solutions et choisissez « NuGet de gérer les packages ». Commutateur toohello « Parcourir » onglet et recherchez «`Diagnostics.EventFlow`» :

![Packages NuGet EventFlow dans l’interface utilisateur du gestionnaire de package NuGet Visual Studio][1]

service Hello EventFlow d’hébergement doit inclure les packages appropriés en fonction de la source de hello et de destination pour les journaux d’application hello. Ajoutez hello suivant des packages : 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * (toocapture à partir de la classe EventSource du service hello, des données EventSources standard tels que *Services de Microsoft ServiceFabric* et *ServiceFabric-Microsoft-acteurs*)
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * (nous allons toosend hello journaux tooan Azure Application Insights ressource)  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * (permet l’initialisation du pipeline de EventFlow hello à partir de la configuration du service Service Fabric et signale les problèmes à l’envoi de données de diagnostic sous forme de rapports d’intégrité de l’infrastructure de Service)

> [!NOTE]
> `Microsoft.Diagnostics.EventFlow.Inputs.EventSource`le package nécessite hello service projet tootarget .NET Framework 4.6 ou version ultérieure. Assurez-vous que vous définissez framework cible appropriée de hello dans Propriétés du projet avant d’installer ce package. 

Une fois toutes les hello packages sont installés, étape suivante de hello est tooconfigure et activer EventFlow dans le service hello.

## <a name="configuring-and-enabling-log-collection"></a>Configuration et activation de la collecte de journaux
Pipeline EventFlow, responsable de l’envoi de journaux de hello, est créé à partir d’une spécification stockée dans un fichier de configuration. Le package `Microsoft.Diagnostics.EventFlow.ServiceFabric` installe un fichier de configuration EventFlow de démarrage dans le dossier `PackageRoot\Config` de la solution. nom de fichier Hello est `eventFlowConfig.json`. Ce fichier de configuration a besoin de données de toocapture de toobe modifié à partir de service par défaut de hello `EventSource` classe et le service de données tooApplication Insights d’envoi.

> [!NOTE]
> Nous partons du principe que vous êtes familiarisé avec **Azure Application Insights** service et que vous disposez d’une ressource Application Insights plan toouse toomonitor votre service Service Fabric. Si vous avez besoin d’informations supplémentaires, consultez [Création d’une ressource Application Insights dans Azure](../application-insights/app-insights-create-new-resource.md).

Ouvrez hello `eventFlowConfig.json` dans l’éditeur de hello et modifie son contenu comme indiqué ci-dessous. Vérifiez que nom de ServiceEventSource tooreplace hello et clé d’instrumentation Application Insights selon toocomments. 

```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace hello following value with your service's ServiceEventSource name)
        { "providerName": "your-service-EventSource-name" }
      ]
    }
  ],
  "filters": [
    {
      "type": "drop",
      "include": "Level == Verbose"
    }
  ],
  "outputs": [
    {
      "type": "ApplicationInsights",
      // (replace hello following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

> [!NOTE]
> nom Hello de ServiceEventSource du service valeur hello Hello propriété Name de hello `EventSourceAttribute` appliqué toohello ServiceEventSource classe. Il est spécifié dans hello `ServiceEventSource.cs` fichier, qui fait partie du code de service hello. Par exemple, Bonjour suivant nom hello d’extrait de code Hello ServiceEventSource est *MyCompany-Application1-Stateless1*:
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

Notez que le fichier `eventFlowConfig.json` fait partie du package de configuration du service. Fichier toothis des modifications peut être inclus dans intégral ou configuration-uniquement les mises à niveau du service de hello, objet tooService Fabric mise à niveau les vérifications d’intégrité et restauration automatique cas d’échec de mise à niveau. Pour plus d’informations, consultez [Mise à niveau des applications Service Fabric](service-fabric-application-upgrade.md).

étape finale de Hello est le pipeline de EventFlow tooinstantiate dans le code de démarrage de votre service, situé dans `Program.cs` fichier. Bonjour ajouts de liées EventFlow exemple suivants sont marqués avec des commentaires commençant par `****`:

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric;
using Microsoft.ServiceFabric.Services.Runtime;

// **** EventFlow namespace
using Microsoft.Diagnostics.EventFlow.ServiceFabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>
        private static void Main()
        {
            try
            {
                // **** Instantiate log collection via EventFlow
                using (var diagnosticsPipeline = ServiceFabricDiagnosticPipelineFactory.CreatePipeline("MyApplication-MyService-DiagnosticsPipeline"))
                {

                    
                    ServiceRuntime.RegisterServiceAsync("Stateless1Type",
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                    ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                    Thread.Sleep(Timeout.Infinite);
                }
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
                throw;
            }
        }
    }
}
```

nom de Hello passé comme paramètre hello Hello `CreatePipeline` méthode Hello `ServiceFabricDiagnosticsPipelineFactory` hello désigne hello *entité de contrôle d’intégrité* représentant le pipeline de collection de journaux de EventFlow hello. Ce nom est utilisé en cas de EventFlow et d’erreur et la signale via hello sous-système de contrôle d’intégrité de l’infrastructure de Service.

## <a name="verification"></a>Vérification
Démarrer votre service et observez hello débogage fenêtre Sortie de Visual Studio. Après le démarrage du service de hello, vous devez commencer à voir les preuves que votre service envoie des enregistrements de « Données de télémétrie Application Insights ». Ouvrez un navigateur web et accédez de ressource d’Application Insights tooyour accédez. Ouvrez l’onglet « Recherche » (en haut de hello du Panneau de « Présentation » hello par défaut). Après un court délai vous devez commencer à voir les traces dans le portail d’Application Insights hello :

![Portail Application Insights montrant les journaux issus d’une application Service Fabric][2]

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur le diagnostic et la surveillance d’un service Fabric Service](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [Documentation relative à EventFlow](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
