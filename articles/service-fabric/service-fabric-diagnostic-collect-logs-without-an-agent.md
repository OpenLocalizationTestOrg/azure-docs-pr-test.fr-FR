---
title: "Collecter les journaux directement à partir d’un processus de service Azure Service Fabric | Microsoft Azure"
description: "Décrit les applications Service Fabric permettant d’envoyer les journaux directement vers un emplacement central comme Azure Application Insights ou Elasticsearch, sans faire appel à un agent Azure Diagnostics."
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
ms.openlocfilehash: b7d2541928f4248750417a77d99033c8b4354dcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a><span data-ttu-id="7ee8c-103">Collecter les journaux directement à partir d’un processus de service Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7ee8c-103">Collect logs directly from an Azure Service Fabric service process</span></span>
## <a name="in-process-log-collection"></a><span data-ttu-id="7ee8c-104">Collecte de journaux dans le processus</span><span class="sxs-lookup"><span data-stu-id="7ee8c-104">In-process log collection</span></span>
<span data-ttu-id="7ee8c-105">La collecte des journaux d’application à l’aide de l’[extension Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) s’avère efficace pour **Azure Service Fabric** si l’ensemble de sources et de destinations des journaux est restreint, ne change pas souvent et s’il existe un mappage simple entre les sources et les destinations.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-105">Collecting application logs using [Azure Diagnostics extension](service-fabric-diagnostics-how-to-setup-wad.md) is a good option for **Azure Service Fabric** services if the set of log sources and destinations is small, does not change often, and there is a straightforward mapping between the sources and their destinations.</span></span> <span data-ttu-id="7ee8c-106">Si ce n’est pas le cas, une autre solution consiste à configurer les services de sorte qu’ils envoient leurs journaux directement vers un emplacement central.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-106">If not, an alternative is to have services send their logs directly to a central location.</span></span> <span data-ttu-id="7ee8c-107">Ce processus, appelé **collecte de journaux dans le processus**, présente plusieurs avantages potentiels :</span><span class="sxs-lookup"><span data-stu-id="7ee8c-107">This process is known as **in-process log collection** and has several potential advantages:</span></span>

* <span data-ttu-id="7ee8c-108">*Simplicité de configuration et de déploiement*</span><span class="sxs-lookup"><span data-stu-id="7ee8c-108">*Easy configuration and deployment*</span></span>

    * <span data-ttu-id="7ee8c-109">La configuration de la collecte des données de diagnostic s’inscrit simplement dans le cadre de la configuration du service.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-109">The configuration of diagnostic data collection is just part of the service configuration.</span></span> <span data-ttu-id="7ee8c-110">Elle reste toujours facilement « synchronisée » avec le reste de l’application.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-110">It is easy to always keep it "in sync" with the rest of the application.</span></span>
    * <span data-ttu-id="7ee8c-111">Vous pouvez facilement réaliser une configuration par application ou par service.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-111">Per-application or per-service configuration is easily achievable.</span></span>
        * <span data-ttu-id="7ee8c-112">La collecte de journaux basée sur un agent implique généralement d’effectuer séparément le déploiement et la configuration de l’agent de diagnostic, ce qui représente une tâche administrative supplémentaire potentiellement source d’erreurs.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-112">Agent-based log collection usually requires a separate deployment and configuration of the diagnostic agent, which is an extra administrative task and a potential source of errors.</span></span> <span data-ttu-id="7ee8c-113">Souvent, une seule instance de l’agent est autorisée par machine virtuelle (nœud) et la configuration de l’agent est partagée entre l’ensemble des applications et des services exécutés sur ce nœud.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-113">Often there is only one instance of the agent allowed per virtual machine (node) and the agent configuration is shared among all applications and services running on that node.</span></span> 

* <span data-ttu-id="7ee8c-114">*Flexibilité*</span><span class="sxs-lookup"><span data-stu-id="7ee8c-114">*Flexibility*</span></span>
   
    * <span data-ttu-id="7ee8c-115">L’application peut envoyer les données partout où elles sont nécessaires, tant qu’il existe une bibliothèque cliente capable de prendre en charge le système de stockage ciblé.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-115">The application can send the data wherever it needs to go, as long as there is a client library that supports the targeted data storage system.</span></span> <span data-ttu-id="7ee8c-116">Vous pouvez ajouter de nouvelles destinations selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-116">New destinations can be added as desired.</span></span>
    * <span data-ttu-id="7ee8c-117">Vous pouvez également implémenter des règles de capture, de filtrage et d’agrégation de données complexes.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-117">Complex capture, filtering, and data-aggregation rules can be implemented.</span></span>
    * <span data-ttu-id="7ee8c-118">La collecte de journaux basée sur un agent est souvent limitée par les récepteurs de données pris en charge par l’agent.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-118">Agent-based log collection is often limited by the data sinks that the agent supports.</span></span> <span data-ttu-id="7ee8c-119">Certains agents sont extensibles.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-119">Some agents are extensible.</span></span>

* <span data-ttu-id="7ee8c-120">*Accès aux données d’application internes et contexte*</span><span class="sxs-lookup"><span data-stu-id="7ee8c-120">*Access to internal application data and context*</span></span>
   
    * <span data-ttu-id="7ee8c-121">Le sous-système de diagnostic exécuté à l’intérieur du processus d’application/service peut facilement enrichir les traces d’informations contextuelles.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-121">The diagnostic subsystem running inside the application/service process can easily augment the traces with contextual information.</span></span>
    * <span data-ttu-id="7ee8c-122">Avec la collecte de journaux basée sur un agent, les données doivent être envoyées à un agent par le biais d’un mécanisme de communication entre processus, tel que le suivi d’événements pour Windows.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-122">With agent-based log collection, the data must be sent to an agent via some inter-process communication mechanism, such as Event Tracing for Windows.</span></span> <span data-ttu-id="7ee8c-123">Ce mécanisme peut imposer des limites supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-123">This mechanism could impose additional limitations.</span></span>

<span data-ttu-id="7ee8c-124">Il est possible de combiner ces deux méthodes de collecte et de tirer parti de leurs avantages respectifs.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-124">It is possible to combine and benefit from both collection methods.</span></span> <span data-ttu-id="7ee8c-125">En effet, cela peut constituer la meilleure solution pour de nombreuses applications.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-125">Indeed, it might be the best solution for many applications.</span></span> <span data-ttu-id="7ee8c-126">La collecte basée sur un agent est une solution idéale pour collecter les journaux liés au cluster dans son ensemble et aux nœuds de cluster individuels.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-126">Agent-based collection is a natural solution for collecting logs related to the whole cluster and individual cluster nodes.</span></span> <span data-ttu-id="7ee8c-127">Elle s’avère beaucoup plus fiable que la collecte de journaux dans le processus pour diagnostiquer les problèmes de démarrage de service et les incidents.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-127">It is much more reliable way, than in-process log collection, to diagnose service startup problems and crashes.</span></span> <span data-ttu-id="7ee8c-128">Par ailleurs, lorsque de nombreux services sont exécutés à l’intérieur d’un cluster Service Fabric, la collecte de journaux dans le processus par chaque service donne lieu à de nombreuses connexions sortantes à partir du cluster.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-128">Also, with many services running inside a Service Fabric cluster, each service doing its own in-process log collection results in numerous outgoing connections from the cluster.</span></span> <span data-ttu-id="7ee8c-129">Ce grand nombre de connexions sortantes affecte à la fois le sous-système réseau et la destination des journaux.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-129">Large number of outgoing connections is taxing both for the network subsystem and for the log destination.</span></span> <span data-ttu-id="7ee8c-130">Un agent tel qu’[**Azure Diagnostics** ](../cloud-services/cloud-services-dotnet-diagnostics.md) peut collecter les données de plusieurs services et envoyer toutes ces données via un nombre réduit de connexions, ce qui améliore le débit.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-130">An agent such as [**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) can gather data from multiple services and send all data through a few connections, improving throughput.</span></span> 

<span data-ttu-id="7ee8c-131">Cet article montre comment configurer une collecte de journaux dans le processus à l’aide de la [**bibliothèque open source EventFlow**](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="7ee8c-131">In this article, we show how to set up an in-process log collection using [**EventFlow open-source library**](https://github.com/Azure/diagnostics-eventflow).</span></span> <span data-ttu-id="7ee8c-132">D’autres bibliothèques peuvent être utilisées dans le même but, mais EventFlow présente l’avantage d’avoir été conçu spécifiquement pour la collecte de journaux dans le processus et pour prendre en charge les services Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-132">Other libraries might be used for the same purpose, but EventFlow has the benefit of having been designed specifically for in-process log collection and to support Service Fabric services.</span></span> <span data-ttu-id="7ee8c-133">Nous utilisons [**Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/) comme destination des journaux.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-133">We use [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) as the log destination.</span></span> <span data-ttu-id="7ee8c-134">D’autres destinations telles qu’[**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) ou [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) sont également prises en charge.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-134">Other destinations such as [**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) or [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) are also supported.</span></span> <span data-ttu-id="7ee8c-135">Il suffit simplement d’installer le package NuGet approprié et de configurer la destination dans le fichier de configuration EventFlow.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-135">It is just a question of installing appropriate NuGet package and configuring the destination in the EventFlow configuration file.</span></span> <span data-ttu-id="7ee8c-136">Pour plus d’informations sur les destinations de journaux autres qu’Application Insights, consultez la [documentation relative à EventFlow](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="7ee8c-136">For more information on log destinations other than Application Insights, see [EventFlow documentation](https://github.com/Azure/diagnostics-eventflow).</span></span>

## <a name="adding-eventflow-library-to-a-service-fabric-service-project"></a><span data-ttu-id="7ee8c-137">Ajout de la bibliothèque EventFlow à un projet de service Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7ee8c-137">Adding EventFlow library to a Service Fabric service project</span></span>
<span data-ttu-id="7ee8c-138">Les fichiers binaires EventFlow sont disponibles sous la forme d’un ensemble de packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-138">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="7ee8c-139">Pour ajouter EventFlow à un projet de service Service Fabric, cliquez sur le projet dans l’Explorateur de solutions et sélectionnez Gérer les packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-139">To add EventFlow to a Service Fabric service project, right-click the project in the Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="7ee8c-140">Basculez vers l’onglet Parcourir et recherchez « `Diagnostics.EventFlow` » :</span><span class="sxs-lookup"><span data-stu-id="7ee8c-140">Switch to the "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Packages NuGet EventFlow dans l’interface utilisateur du gestionnaire de package NuGet Visual Studio][1]

<span data-ttu-id="7ee8c-142">Le service qui héberge EventFlow doit inclure les packages appropriés en fonction de la source et de la destination des journaux d’application.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-142">The service hosting EventFlow should include appropriate packages depending on the source and destination for the application logs.</span></span> <span data-ttu-id="7ee8c-143">Ajoutez les packages suivants :</span><span class="sxs-lookup"><span data-stu-id="7ee8c-143">Add the following packages:</span></span> 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * <span data-ttu-id="7ee8c-144">(pour capturer les données à partir de la classe EventSource du service et des EventSources standard tels que *Microsoft-ServiceFabric-Services* et *Microsoft-ServiceFabric-Actors*)</span><span class="sxs-lookup"><span data-stu-id="7ee8c-144">(to capture data from the service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * <span data-ttu-id="7ee8c-145">(nous allons envoyer les journaux à une ressource Azure Application Insights)</span><span class="sxs-lookup"><span data-stu-id="7ee8c-145">(we are going to send the logs to an Azure Application Insights resource)</span></span>  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * <span data-ttu-id="7ee8c-146">(permet d’initialiser le pipeline EventFlow à partir de la configuration du service Service Fabric et de signaler tout problème lié à l’envoi des données de diagnostic sous forme de rapports d’intégrité Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="7ee8c-146">(enables initialization of the EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

> [!NOTE]
> <span data-ttu-id="7ee8c-147">Le package `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` nécessite le ciblage de .NET Framework 4.6 ou version ultérieure par le projet de service.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource` package requires the service project to target .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="7ee8c-148">Veillez à définir l’infrastructure cible appropriée dans les propriétés du projet avant d’installer ce package.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-148">Make sure you set the appropriate target framework in project properties before installing this package.</span></span> 

<span data-ttu-id="7ee8c-149">Une fois tous les packages installés, l’étape suivante consiste à configurer et à activer EventFlow dans le service.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-149">After all the packages are installed, the next step is to configure and enable EventFlow in the service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="7ee8c-150">Configuration et activation de la collecte de journaux</span><span class="sxs-lookup"><span data-stu-id="7ee8c-150">Configuring and enabling log collection</span></span>
<span data-ttu-id="7ee8c-151">Le pipeline EventFlow, chargé d’envoyer les journaux, est créé à partir d’une spécification stockée dans un fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-151">EventFlow pipeline, responsible for sending the logs, is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="7ee8c-152">Le package `Microsoft.Diagnostics.EventFlow.ServiceFabric` installe un fichier de configuration EventFlow de démarrage dans le dossier `PackageRoot\Config` de la solution.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder.</span></span> <span data-ttu-id="7ee8c-153">Le nom de ce fichier est `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-153">The file name is `eventFlowConfig.json`.</span></span> <span data-ttu-id="7ee8c-154">Ce fichier de configuration doit être modifié pour capturer les données à partir de la classe `EventSource` du service par défaut et envoyer les données au service Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-154">This configuration file needs to be modified to capture data from the default service `EventSource` class and send data to Application Insights service.</span></span>

> [!NOTE]
> <span data-ttu-id="7ee8c-155">Nous partons du principe que vous êtes familiarisé avec le service **Azure Application Insights** et que vous disposez d’une ressource Application Insights que vous prévoyez d’utiliser pour surveiller votre service Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-155">We assume that you are familiar with **Azure Application Insights** service and that you have an Application Insights resource that you plan to use to monitor your Service Fabric service.</span></span> <span data-ttu-id="7ee8c-156">Si vous avez besoin d’informations supplémentaires, consultez [Création d’une ressource Application Insights dans Azure](../application-insights/app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="7ee8c-156">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

<span data-ttu-id="7ee8c-157">Ouvrez le fichier `eventFlowConfig.json` dans l’éditeur et modifiez son contenu comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-157">Open the `eventFlowConfig.json` file in the editor and change its content as shown below.</span></span> <span data-ttu-id="7ee8c-158">Veillez à remplacer le nom de l’élément ServiceEventSource et la clé d’instrumentation Application Insights conformément aux commentaires.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-158">Make sure to replace the ServiceEventSource name and Application Insights instrumentation key according to comments.</span></span> 

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

> [!NOTE]
> <span data-ttu-id="7ee8c-159">Le nom de l’élément ServiceEventSource du service correspond à la valeur de la propriété Name de l’élément `EventSourceAttribute` appliqué à la classe ServiceEventSource.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-159">The name of service's ServiceEventSource is the value of the Name property of the `EventSourceAttribute` applied to the ServiceEventSource class.</span></span> <span data-ttu-id="7ee8c-160">Tout cela est spécifié dans le fichier `ServiceEventSource.cs`, qui est inclus dans le code du service.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-160">It is all specified in the `ServiceEventSource.cs` file, which is part of the service code.</span></span> <span data-ttu-id="7ee8c-161">Par exemple, dans l’extrait de code suivant, le nom de l’élément ServiceEventSource est *MyCompany-Application1-Stateless1* :</span><span class="sxs-lookup"><span data-stu-id="7ee8c-161">For example, in the following code snippet the name of the ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

<span data-ttu-id="7ee8c-162">Notez que le fichier `eventFlowConfig.json` fait partie du package de configuration du service.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-162">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="7ee8c-163">Les modifications apportées à ce fichier peuvent être incluses dans les mises à niveau portant sur l’intégralité du service ou sur sa configuration uniquement, qui sont soumises aux contrôles d’intégrité et à la restauration automatique de Service Fabric en cas d’échec de la mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-163">Changes to this file can be included in full- or configuration-only upgrades of the service, subject to Service Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="7ee8c-164">Pour plus d’informations, consultez [Mise à niveau des applications Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="7ee8c-164">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="7ee8c-165">L’étape finale consiste à instancier le pipeline EventFlow dans le code de démarrage de votre service, qui se trouve dans le fichier `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-165">The final step is to instantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file.</span></span> <span data-ttu-id="7ee8c-166">Dans l’exemple suivant, les ajouts liés à EventFlow sont signalés par des commentaires introduits par `****` :</span><span class="sxs-lookup"><span data-stu-id="7ee8c-166">In the following example  EventFlow-related additions are marked with comments starting with `****`:</span></span>

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

<span data-ttu-id="7ee8c-167">Le nom transmis comme paramètre de la méthode `CreatePipeline` de l’élément `ServiceFabricDiagnosticsPipelineFactory` correspond au nom de l’*entité d’intégrité* représentant le pipeline de collection des journaux EventFlow.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-167">The name passed as the parameter of the `CreatePipeline` method of the `ServiceFabricDiagnosticsPipelineFactory` is the name of the *health entity* representing the EventFlow log collection pipeline.</span></span> <span data-ttu-id="7ee8c-168">Ce nom est utilisé si EventFlow rencontre une erreur et la signale via le sous-système d’intégrité de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-168">This name is used if EventFlow encounters and error and reports it through the Service Fabric health subsystem.</span></span>

## <a name="verification"></a><span data-ttu-id="7ee8c-169">Vérification</span><span class="sxs-lookup"><span data-stu-id="7ee8c-169">Verification</span></span>
<span data-ttu-id="7ee8c-170">Démarrez votre service et observez la fenêtre de sortie Débogage de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-170">Start your service and observe the Debug output window in Visual Studio.</span></span> <span data-ttu-id="7ee8c-171">Une fois le service démarré, vous devriez commencer à voir des signes qu’il envoie des enregistrements « Application Insights Telemetry ».</span><span class="sxs-lookup"><span data-stu-id="7ee8c-171">After the service is started, you should start seeing evidence that your service is sending "Application Insights Telemetry" records.</span></span> <span data-ttu-id="7ee8c-172">Ouvrez un navigateur web et accédez à votre ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7ee8c-172">Open a web browser and navigate go to your Application Insights resource.</span></span> <span data-ttu-id="7ee8c-173">Ouvrez l’onglet Recherche (en haut du panneau Vue d’ensemble par défaut).</span><span class="sxs-lookup"><span data-stu-id="7ee8c-173">Open "Search" tab (at the top of the default "Overview" blade).</span></span> <span data-ttu-id="7ee8c-174">Après un court instant, vous devriez commencer à voir vos traces dans le portail Application Insights :</span><span class="sxs-lookup"><span data-stu-id="7ee8c-174">After a short delay you should start seeing your traces in the Application Insights portal:</span></span>

![Portail Application Insights montrant les journaux issus d’une application Service Fabric][2]

## <a name="next-steps"></a><span data-ttu-id="7ee8c-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7ee8c-176">Next steps</span></span>
* [<span data-ttu-id="7ee8c-177">En savoir plus sur le diagnostic et la surveillance d’un service Fabric Service</span><span class="sxs-lookup"><span data-stu-id="7ee8c-177">Learn more about diagnosing and monitoring a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [<span data-ttu-id="7ee8c-178">Documentation relative à EventFlow</span><span class="sxs-lookup"><span data-stu-id="7ee8c-178">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
