---
title: "Agrégation d’événements Azure Service Fabric avec EventFlow | Microsoft Docs"
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
ms.openlocfilehash: 90d26a77b749e70de3a7d910f15820653e2ef39b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a><span data-ttu-id="7f5bf-103">Agrégation et collection d’événements avec EventFlow</span><span class="sxs-lookup"><span data-stu-id="7f5bf-103">Event aggregation and collection using EventFlow</span></span>

<span data-ttu-id="7f5bf-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) peut acheminer les événements d’un nœud vers une ou plusieurs destinations de surveillance.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) can route events from a node to one or more monitoring destinations.</span></span> <span data-ttu-id="7f5bf-105">Étant donné que cet outil est inclus en tant que package NuGet dans votre projet de service, le code et la configuration d’EventFlow accompagnent le service, éliminant ainsi le problème de configuration par nœud mentionné plus haut à propos des diagnostics Azure.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-105">Because it is included as a NuGet package in your service project, EventFlow code and configuration travel with the service, eliminating the per-node configuration issue mentioned earlier about Azure Diagnostics.</span></span> <span data-ttu-id="7f5bf-106">EventFlow s’exécute au sein de votre processus de service et se connecte directement aux sorties configurées.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-106">EventFlow runs within your service process, and connects directly to the configured outputs.</span></span> <span data-ttu-id="7f5bf-107">En raison de cette connexion directe, EventFlow fonctionne pour les déploiements d’un service sur Azure, dans un conteneur et en local.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-107">Because of the direct connection, EventFlow works for Azure, container, and on-premises service deployments.</span></span> <span data-ttu-id="7f5bf-108">Faites preuve de prudence si vous exécutez EventFlow dans des scénarios de haute densité, par exemple dans un conteneur, car chaque pipeline EventFlow établit une connexion externe.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-108">Be careful if you run EventFlow in high-density scenarios, such as in a container, because each EventFlow pipeline makes an external connection.</span></span> <span data-ttu-id="7f5bf-109">Par conséquent, si vous hébergez plusieurs processus, cela donne lieu à plusieurs connexions sortantes.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-109">So, if you host several processes, you get several outbound connections!</span></span> <span data-ttu-id="7f5bf-110">Ce n’est pas vraiment une préoccupation pour les applications Service Fabric, car tous les réplicas d’un événement `ServiceType` s’exécutent dans le même processus, ce qui limite le nombre de connexions sortantes.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-110">This isn't as much a concern for Service Fabric applications, because all replicas of a `ServiceType` run in the same process, and this limits the number of outbound connections.</span></span> <span data-ttu-id="7f5bf-111">EventFlow propose également le filtrage des événements. Ainsi, seuls les événements correspondant au filtre spécifié sont envoyés.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-111">EventFlow also offers event filtering, so that only the events that match the specified filter are sent.</span></span>

## <a name="setting-up-eventflow"></a><span data-ttu-id="7f5bf-112">Configuration d’EventFlow</span><span class="sxs-lookup"><span data-stu-id="7f5bf-112">Setting up EventFlow</span></span>

<span data-ttu-id="7f5bf-113">Les fichiers binaires EventFlow sont disponibles sous la forme d’un ensemble de packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-113">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="7f5bf-114">Pour ajouter EventFlow à un projet de service Service Fabric, cliquez sur le projet dans l’Explorateur de solutions et sélectionnez Gérer les packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-114">To add EventFlow to a Service Fabric service project, right-click the project in the Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="7f5bf-115">Basculez vers l’onglet Parcourir et recherchez « `Diagnostics.EventFlow` » :</span><span class="sxs-lookup"><span data-stu-id="7f5bf-115">Switch to the "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Packages NuGet EventFlow dans l’interface utilisateur du gestionnaire de package NuGet Visual Studio](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

<span data-ttu-id="7f5bf-117">Une liste de différents packages s’affiche, étiquetés avec « Entrées » et « Sorties ».</span><span class="sxs-lookup"><span data-stu-id="7f5bf-117">You will see a list of various packages show up, labeled with "Inputs" and "Outputs".</span></span> <span data-ttu-id="7f5bf-118">EventFlow prend en charge différents fournisseurs de journalisation et analyseurs.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-118">EventFlow supports various different logging providers and analyzers.</span></span> <span data-ttu-id="7f5bf-119">Le service qui héberge EventFlow doit inclure les packages appropriés en fonction de la source et de la destination des journaux d’application.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-119">The service hosting EventFlow should include appropriate packages depending on the source and destination for the application logs.</span></span> <span data-ttu-id="7f5bf-120">Outre le package ServiceFabric principal, au moins un package Entrée et un package Sortie doivent également être configurés.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-120">In addition to the core ServiceFabric package, you also need at least one Input and Output configured.</span></span> <span data-ttu-id="7f5bf-121">Par exemple, vous pouvez ajouter les packages suivants à des événements EventSource envoyés à Application Insights :</span><span class="sxs-lookup"><span data-stu-id="7f5bf-121">For exmaple, you can add the following packages to sent EventSource events to Application Insights:</span></span>

* <span data-ttu-id="7f5bf-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` (pour capturer les données à partir de la classe EventSource du service et d’EventSources standard tels que *Microsoft-ServiceFabric-Services* et *Microsoft-ServiceFabric-Actors*)</span><span class="sxs-lookup"><span data-stu-id="7f5bf-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` to capture data from the service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* <span data-ttu-id="7f5bf-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (nous allons envoyer les journaux à une ressource Azure Application Insights)</span><span class="sxs-lookup"><span data-stu-id="7f5bf-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (we are going to send the logs to an Azure Application Insights resource)</span></span>
* <span data-ttu-id="7f5bf-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric` (permet d’initialiser le pipeline EventFlow à partir de la configuration du service Service Fabric et signale tout problème lié à l’envoi des données de diagnostic sous forme de rapports d’intégrité Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="7f5bf-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(enables initialization of the EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

>[!NOTE]
><span data-ttu-id="7f5bf-125">Le package `Microsoft.Diagnostics.EventFlow.Input.EventSource` nécessite le ciblage de .NET Framework 4.6 ou version ultérieure par le projet de service.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires the service project to target .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="7f5bf-126">Veillez à définir l’infrastructure cible appropriée dans les propriétés du projet avant d’installer ce package.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-126">Make sure you set the appropriate target framework in project properties before installing this package.</span></span>

<span data-ttu-id="7f5bf-127">Une fois tous les packages installés, l’étape suivante consiste à configurer et à activer EventFlow dans le service.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-127">After all the packages are installed, the next step is to configure and enable EventFlow in the service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="7f5bf-128">Configuration et activation de la collecte de journaux</span><span class="sxs-lookup"><span data-stu-id="7f5bf-128">Configuring and enabling log collection</span></span>
<span data-ttu-id="7f5bf-129">Le pipeline EventFlow chargé d’envoyer les journaux est créé à partir d’une spécification stockée dans un fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-129">The EventFlow pipeline responsible for sending the logs is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="7f5bf-130">Le package `Microsoft.Diagnostics.EventFlow.ServiceFabric` installe un fichier de configuration EventFlow de démarrage dans le dossier de solution `PackageRoot\Config`, nommé `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-130">The `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder, named `eventFlowConfig.json`.</span></span> <span data-ttu-id="7f5bf-131">Ce fichier de configuration doit être modifié pour capturer les données à partir de la classe `EventSource` du service par défaut et toutes les autres entrées que vous voulez configurer, puis envoyer les données à l’emplacement approprié.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-131">This configuration file needs to be modified to capture data from the default service `EventSource` class, and any other inputs you want to configure, and send data to the appropriate place.</span></span>

<span data-ttu-id="7f5bf-132">Voici un exemple d’*eventFlowConfig.json* basé sur les packages NuGet mentionnés ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="7f5bf-132">Here is a sample *eventFlowConfig.json* based on the NuGet packages mentioned above:</span></span>
```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace the following value with your service's ServiceEventSource name)
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
      // (replace the following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

<span data-ttu-id="7f5bf-133">Le nom de l’élément ServiceEventSource du service correspond à la valeur de la propriété Name de l’élément `EventSourceAttribute` appliqué à la classe ServiceEventSource.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-133">The name of service's ServiceEventSource is the value of the Name property of the `EventSourceAttribute` applied to the ServiceEventSource class.</span></span> <span data-ttu-id="7f5bf-134">Tout cela est spécifié dans le fichier `ServiceEventSource.cs`, qui est inclus dans le code du service.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-134">It is all specified in the `ServiceEventSource.cs` file, which is part of the service code.</span></span> <span data-ttu-id="7f5bf-135">Par exemple, dans l’extrait de code suivant, le nom de l’élément ServiceEventSource est *MyCompany-Application1-Stateless1* :</span><span class="sxs-lookup"><span data-stu-id="7f5bf-135">For example, in the following code snippet the name of the ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

<span data-ttu-id="7f5bf-136">Notez que le fichier `eventFlowConfig.json` fait partie du package de configuration du service.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-136">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="7f5bf-137">Les modifications apportées à ce fichier peuvent être incluses dans les mises à niveau portant sur l’intégralité du service ou sur sa configuration uniquement, qui sont soumises aux contrôles d’intégrité et à la restauration automatique de Service Fabric en cas d’échec de la mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-137">Changes to this file can be included in full- or configuration-only upgrades of the service, subject to Service Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="7f5bf-138">Pour plus d’informations, consultez [Mise à niveau des applications Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="7f5bf-138">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="7f5bf-139">La section *filters* de la configuration vous permet de personnaliser davantage les informations qui vont passer à travers le pipeline EventFlow vers les sorties, ce qui vous permet de supprimer ou d’inclure certaines informations, ou de modifier la structure des données d’événement.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-139">The *filters* section of the config allows you to further customize the information that is going to go through the EventFlow pipeline to the outputs, allowing you to drop or include certain information, or change the structure of the event data.</span></span> <span data-ttu-id="7f5bf-140">Pour plus d’informations sur le filtrage, consultez les [Filtres EventFlow](https://github.com/Azure/diagnostics-eventflow#filters).</span><span class="sxs-lookup"><span data-stu-id="7f5bf-140">For more information on filtering, see [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span></span>

<span data-ttu-id="7f5bf-141">La dernière étape consiste à instancier le pipeline EventFlow dans le code de démarrage de votre service, qui se trouve dans le fichier `Program.cs` :</span><span class="sxs-lookup"><span data-stu-id="7f5bf-141">The final step is to instantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file:</span></span>

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
        /// This is the entry point of the service host process.
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

<span data-ttu-id="7f5bf-142">Le nom transmis comme paramètre de la méthode `CreatePipeline` de l’élément `ServiceFabricDiagnosticsPipelineFactory` correspond au nom de l’*entité d’intégrité* représentant le pipeline de collection des journaux EventFlow.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-142">The name passed as the parameter of the `CreatePipeline` method of the `ServiceFabricDiagnosticsPipelineFactory` is the name of the *health entity* representing the EventFlow log collection pipeline.</span></span> <span data-ttu-id="7f5bf-143">Ce nom est utilisé si EventFlow rencontre une erreur et la signale via le sous-système d’intégrité de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-143">This name is used if EventFlow encounters and error and reports it through the Service Fabric health subsystem.</span></span>

### <a name="using-service-fabric-settings-and-application-parameters-to-in-eventflowconfig"></a><span data-ttu-id="7f5bf-144">Utilisation de paramètres Service Fabric et de paramètres d’application dans eventFlowConfig</span><span class="sxs-lookup"><span data-stu-id="7f5bf-144">Using Service Fabric settings and application parameters to in eventFlowConfig</span></span>

<span data-ttu-id="7f5bf-145">EventFlow prend en charge l’utilisation de paramètres Service Fabric et de paramètres d’application pour configurer ses paramètres.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-145">EventFlow supports using Service Fabric settings and application paremeters to configure EventFlow settings.</span></span> <span data-ttu-id="7f5bf-146">Vous pouvez faire référence aux paramètres Service Fabric à l’aide de la syntaxe spéciale suivante pour les valeurs :</span><span class="sxs-lookup"><span data-stu-id="7f5bf-146">You can refer to Service Fabric settings parameters using this special syntax for values:</span></span>

```json
servicefabric:/<section-name>/<setting-name>
``` 

<span data-ttu-id="7f5bf-147">`<section-name>` est nom de la section de configuration de Service Fabric, et `<setting-name>` est le paramètre de configuration fournissant la valeur qui sera utilisée pour configurer un paramètre EventFlow.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-147">`<section-name>` is the name of the Service Fabric configuration section, and `<setting-name>` is the configuration setting providing the value that will be used to configure an EventFlow setting.</span></span> <span data-ttu-id="7f5bf-148">Pour plus d’informations sur la procédure à suivre, accédez à la rubrique [Prise en charge des paramètres Service Fabric et des paramètres d’application](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span><span class="sxs-lookup"><span data-stu-id="7f5bf-148">To read more about how to do this, go to [Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span></span>

## <a name="verification"></a><span data-ttu-id="7f5bf-149">Vérification</span><span class="sxs-lookup"><span data-stu-id="7f5bf-149">Verification</span></span>

<span data-ttu-id="7f5bf-150">Démarrez votre service et observez la fenêtre de sortie Débogage de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-150">Start your service and observe the Debug output window in Visual Studio.</span></span> <span data-ttu-id="7f5bf-151">Une fois le service démarré, vous devez commencer à voir des preuves qu’il envoie des enregistrements à la sortie que vous avez configurée.</span><span class="sxs-lookup"><span data-stu-id="7f5bf-151">After the service is started, you should start seeing evidence that your service is sending records to the output that you have configured.</span></span> <span data-ttu-id="7f5bf-152">Accédez à votre plateforme d’analyse et de visualisation des événements et vérifiez que les journaux ont commencé à s’afficher (cela peut prendre quelques minutes).</span><span class="sxs-lookup"><span data-stu-id="7f5bf-152">Navigate to your event analysis and visualization platform and confirm that logs have started to show up (could take a few minutes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f5bf-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7f5bf-153">Next steps</span></span>

* [<span data-ttu-id="7f5bf-154">Analyse et visualisation d’événements avec Application Insights</span><span class="sxs-lookup"><span data-stu-id="7f5bf-154">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="7f5bf-155">Analyse et visualisation d’événements avec OMS</span><span class="sxs-lookup"><span data-stu-id="7f5bf-155">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)
* [<span data-ttu-id="7f5bf-156">Documentation relative à EventFlow</span><span class="sxs-lookup"><span data-stu-id="7f5bf-156">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)