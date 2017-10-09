---
title: "aaaAzure l’agrégation d’événements Service Fabric avec EventFlow | Documents Microsoft"
description: "Découvrez l’agrégation et la collecte d’événements à l’aide d’EventFlow pour la surveillance et le diagnostic de clusters Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: c0141d3ed72d835139250af3589e298fd22d8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a>Agrégation et collection d’événements avec EventFlow

[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) peut acheminer les événements à partir d’un nœud tooone ou autres destinations de surveillance. Comme il est inclus en tant que package NuGet dans votre projet de service, configuration et le code de EventFlow se déplacent avec service hello, éliminant le problème de configuration de nœud par nœud hello mentionné plus haut sur les Diagnostics de Azure. EventFlow s’exécute dans votre processus de service et se connecte directement les sorties toohello configuré. En raison de la connexion directe de hello, EventFlow fonctionne pour Azure, conteneur et les déploiements de service local. Faites preuve de prudence si vous exécutez EventFlow dans des scénarios de haute densité, par exemple dans un conteneur, car chaque pipeline EventFlow établit une connexion externe. Par conséquent, si vous hébergez plusieurs processus, cela donne lieu à plusieurs connexions sortantes. Cela n’est pas autant un critère important pour les applications de Service Fabric, car tous les réplicas d’un `ServiceType` exécuter Bonjour même processus, et cela limite le nombre de hello de connexions sortantes. EventFlow offre également le filtrage d’événements, afin que seuls les événements hello qui correspondent au filtre spécifié de hello sont envoyés.

## <a name="setting-up-eventflow"></a>Configuration d’EventFlow

Les fichiers binaires EventFlow sont disponibles sous la forme d’un ensemble de packages NuGet. tooadd projet de service Service Fabric EventFlow tooa, avec le bouton droit de projet hello Bonjour l’Explorateur de solutions et choisissez « NuGet de gérer les packages ». Commutateur toohello « Parcourir » onglet et recherchez «`Diagnostics.EventFlow`» :

![Packages NuGet EventFlow dans l’interface utilisateur du gestionnaire de package NuGet Visual Studio](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

Une liste de différents packages s’affiche, étiquetés avec « Entrées » et « Sorties ». EventFlow prend en charge différents fournisseurs de journalisation et analyseurs. service Hello EventFlow d’hébergement doit inclure les packages appropriés en fonction de la source de hello et de destination pour les journaux d’application hello. En outre package de ServiceFabric toohello core, vous devez au moins une entrée et sortie configurée. Par exemple, vous pouvez ajouter hello suivant packages toosent EventSource événements tooApplication Insights :

* `Microsoft.Diagnostics.EventFlow.Input.EventSource`toocapture à partir de la classe EventSource du service hello, des données EventSources standard tels que *Services de Microsoft ServiceFabric* et *ServiceFabric-Microsoft-acteurs*)
* `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`(nous allons toosend hello journaux tooan Azure Application Insights ressource)
* `Microsoft.Diagnostics.EventFlow.ServiceFabric`(permet l’initialisation du pipeline de EventFlow hello à partir de la configuration du service Service Fabric et signale les problèmes à l’envoi de données de diagnostic sous forme de rapports d’intégrité de l’infrastructure de Service)

>[!NOTE]
>`Microsoft.Diagnostics.EventFlow.Input.EventSource`le package nécessite hello service projet tootarget .NET Framework 4.6 ou version ultérieure. Assurez-vous que vous définissez framework cible appropriée de hello dans Propriétés du projet avant d’installer ce package.

Une fois toutes les hello packages sont installés, étape suivante de hello est tooconfigure et activer EventFlow dans le service hello.

## <a name="configuring-and-enabling-log-collection"></a>Configuration et activation de la collecte de journaux
pipeline de EventFlow Hello chargé de l’envoi des journaux de hello est créé à partir d’une spécification stockée dans un fichier de configuration. Hello `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installe un fichier de configuration de départ EventFlow sous `PackageRoot\Config` dossier de solution, nommé `eventFlowConfig.json`. Ce fichier de configuration a besoin de données de toocapture de toobe modifié à partir de service par défaut de hello `EventSource` classe et autres entrées tooconfigure, envoyer et données toohello place approprié.

Voici un exemple *eventFlowConfig.json* basé sur les packages NuGet hello mentionnés ci-dessus :
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

nom Hello de ServiceEventSource du service valeur hello Hello propriété Name de hello `EventSourceAttribute` appliqué toohello ServiceEventSource classe. Il est spécifié dans hello `ServiceEventSource.cs` fichier, qui fait partie du code de service hello. Par exemple, Bonjour suivant nom hello d’extrait de code Hello ServiceEventSource est *MyCompany-Application1-Stateless1*:

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

Notez que le fichier `eventFlowConfig.json` fait partie du package de configuration du service. Fichier toothis des modifications peut être inclus dans intégral ou configuration-uniquement les mises à niveau du service de hello, objet tooService Fabric mise à niveau les vérifications d’intégrité et restauration automatique cas d’échec de mise à niveau. Pour plus d’informations, consultez [Mise à niveau des applications Service Fabric](service-fabric-application-upgrade.md).

Hello *filtres* section de la configuration de hello vous permet de toofurther personnaliser informations hello toogo continu des sorties de toohello pipeline hello EventFlow, ce qui vous toodrop ou inclure certaines informations ou modifier hello structure de données d’événement hello. Pour plus d’informations sur le filtrage, consultez les [Filtres EventFlow](https://github.com/Azure/diagnostics-eventflow#filters).

étape finale de Hello est le pipeline de EventFlow tooinstantiate dans le code de démarrage de votre service, situé dans `Program.cs` fichier :

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

### <a name="using-service-fabric-settings-and-application-parameters-tooin-eventflowconfig"></a>À l’aide des paramètres de la structure de Service et application paramètres tooin eventFlowConfig

EventFlow prend en charge à l’aide des paramètres de la structure de Service et les paramètres d’application paremeters tooconfigure EventFlow. Vous pouvez consulter les paramètres de paramètres de l’ensemble fibre optique tooService à l’aide de cette syntaxe spéciale pour les valeurs :

```json
servicefabric:/<section-name>/<setting-name>
``` 

`<section-name>`est le nom hello Hello section de configuration de l’infrastructure de Service, et `<setting-name>` configuration hello à fournissant valeur hello tooconfigure utilisé un paramètre EventFlow. plus sur la façon de tooread toodo, accédez trop[prise en charge pour les paramètres de l’infrastructure de Service et application](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).

## <a name="verification"></a>Vérification

Démarrer votre service et observez hello débogage fenêtre Sortie de Visual Studio. Après le démarrage du service de hello, vous devez commencer à voir la preuve que l’envoi de votre service enregistre la sortie toohello que vous avez configuré. Accédez tooyour événement analyse et visualisation de la plateforme et vérifiez que les journaux ont démarré tooshow up (opération peut prendre quelques minutes).

## <a name="next-steps"></a>Étapes suivantes

* [Analyse et visualisation d’événements avec Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md)
* [Analyse et visualisation d’événements avec OMS](service-fabric-diagnostics-event-analysis-oms.md)
* [Documentation relative à EventFlow](https://github.com/Azure/diagnostics-eventflow)