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
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a><span data-ttu-id="f293d-103">Collecter les journaux directement à partir d’un processus de service Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f293d-103">Collect logs directly from an Azure Service Fabric service process</span></span>
## <a name="in-process-log-collection"></a><span data-ttu-id="f293d-104">Collecte de journaux dans le processus</span><span class="sxs-lookup"><span data-stu-id="f293d-104">In-process log collection</span></span>
<span data-ttu-id="f293d-105">Collecte d’application connecte à l’aide de [extension Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) est une bonne option pour **Azure Service Fabric** services si set hello de journal sources et destinations est petite, ne change pas souvent et il est un mappage simple entre des sources de hello et leurs destinations.</span><span class="sxs-lookup"><span data-stu-id="f293d-105">Collecting application logs using [Azure Diagnostics extension](service-fabric-diagnostics-how-to-setup-wad.md) is a good option for **Azure Service Fabric** services if hello set of log sources and destinations is small, does not change often, and there is a straightforward mapping between hello sources and their destinations.</span></span> <span data-ttu-id="f293d-106">Si ce n’est pas le cas, une autre solution consiste à toohave services envoyer les journaux directement tooa point central.</span><span class="sxs-lookup"><span data-stu-id="f293d-106">If not, an alternative is toohave services send their logs directly tooa central location.</span></span> <span data-ttu-id="f293d-107">Ce processus, appelé **collecte de journaux dans le processus**, présente plusieurs avantages potentiels :</span><span class="sxs-lookup"><span data-stu-id="f293d-107">This process is known as **in-process log collection** and has several potential advantages:</span></span>

* <span data-ttu-id="f293d-108">*Simplicité de configuration et de déploiement*</span><span class="sxs-lookup"><span data-stu-id="f293d-108">*Easy configuration and deployment*</span></span>

    * <span data-ttu-id="f293d-109">configuration de Hello de collecte de données de diagnostic est simplement dans le cadre de la configuration du service hello.</span><span class="sxs-lookup"><span data-stu-id="f293d-109">hello configuration of diagnostic data collection is just part of hello service configuration.</span></span> <span data-ttu-id="f293d-110">Il s’agit de conserver facilement tooalways « synchronisé » avec hello il le reste de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="f293d-110">It is easy tooalways keep it "in sync" with hello rest of hello application.</span></span>
    * <span data-ttu-id="f293d-111">Vous pouvez facilement réaliser une configuration par application ou par service.</span><span class="sxs-lookup"><span data-stu-id="f293d-111">Per-application or per-service configuration is easily achievable.</span></span>
        * <span data-ttu-id="f293d-112">Collection basée sur l’agent du journal nécessite généralement un déploiement séparé et la configuration de l’agent de diagnostic hello, qui est une tâche administrative supplémentaire et une source potentielle d’erreurs.</span><span class="sxs-lookup"><span data-stu-id="f293d-112">Agent-based log collection usually requires a separate deployment and configuration of hello diagnostic agent, which is an extra administrative task and a potential source of errors.</span></span> <span data-ttu-id="f293d-113">Il existe souvent qu’une seule instance d’agent hello autorisé par l’ordinateur virtuel (nœud) et configuration de l’agent hello est partagée entre toutes les applications et services en cours d’exécution sur ce nœud.</span><span class="sxs-lookup"><span data-stu-id="f293d-113">Often there is only one instance of hello agent allowed per virtual machine (node) and hello agent configuration is shared among all applications and services running on that node.</span></span> 

* <span data-ttu-id="f293d-114">*Flexibilité*</span><span class="sxs-lookup"><span data-stu-id="f293d-114">*Flexibility*</span></span>
   
    * <span data-ttu-id="f293d-115">application Hello peut envoyer des données de hello qu’elle puisse toogo, tant qu’il existe une bibliothèque de client qui prend en charge le système de stockage de données hello ciblé.</span><span class="sxs-lookup"><span data-stu-id="f293d-115">hello application can send hello data wherever it needs toogo, as long as there is a client library that supports hello targeted data storage system.</span></span> <span data-ttu-id="f293d-116">Vous pouvez ajouter de nouvelles destinations selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="f293d-116">New destinations can be added as desired.</span></span>
    * <span data-ttu-id="f293d-117">Vous pouvez également implémenter des règles de capture, de filtrage et d’agrégation de données complexes.</span><span class="sxs-lookup"><span data-stu-id="f293d-117">Complex capture, filtering, and data-aggregation rules can be implemented.</span></span>
    * <span data-ttu-id="f293d-118">Collection basée sur l’agent du journal est souvent limitée par les récepteurs de données hello hello prend en charge de l’agent.</span><span class="sxs-lookup"><span data-stu-id="f293d-118">Agent-based log collection is often limited by hello data sinks that hello agent supports.</span></span> <span data-ttu-id="f293d-119">Certains agents sont extensibles.</span><span class="sxs-lookup"><span data-stu-id="f293d-119">Some agents are extensible.</span></span>

* <span data-ttu-id="f293d-120">*Contexte et des données d’application toointernal accès*</span><span class="sxs-lookup"><span data-stu-id="f293d-120">*Access toointernal application data and context*</span></span>
   
    * <span data-ttu-id="f293d-121">sous-système de diagnostic Hello en cours d’exécution à l’intérieur du processus de service ou application hello peut accroître facilement les traces hello avec des informations contextuelles.</span><span class="sxs-lookup"><span data-stu-id="f293d-121">hello diagnostic subsystem running inside hello application/service process can easily augment hello traces with contextual information.</span></span>
    * <span data-ttu-id="f293d-122">Collection basée sur l’agent de journal hello données doivent être envoyées agent tooan via un mécanisme de communication entre processus, tels que le suivi d’événements pour Windows.</span><span class="sxs-lookup"><span data-stu-id="f293d-122">With agent-based log collection, hello data must be sent tooan agent via some inter-process communication mechanism, such as Event Tracing for Windows.</span></span> <span data-ttu-id="f293d-123">Ce mécanisme peut imposer des limites supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="f293d-123">This mechanism could impose additional limitations.</span></span>

<span data-ttu-id="f293d-124">Il est possible toocombine et tirent parti de ces deux méthodes de collection.</span><span class="sxs-lookup"><span data-stu-id="f293d-124">It is possible toocombine and benefit from both collection methods.</span></span> <span data-ttu-id="f293d-125">En effet, il peut être la meilleure solution hello pour de nombreuses applications.</span><span class="sxs-lookup"><span data-stu-id="f293d-125">Indeed, it might be hello best solution for many applications.</span></span> <span data-ttu-id="f293d-126">Collection basée sur l’agent est une solution naturelle pour la collecte de journaux associés toohello ensemble du cluster et les nœuds de cluster individuels.</span><span class="sxs-lookup"><span data-stu-id="f293d-126">Agent-based collection is a natural solution for collecting logs related toohello whole cluster and individual cluster nodes.</span></span> <span data-ttu-id="f293d-127">C’est un moyen beaucoup plus fiable, à la collection dans le processus du journal et les incidents, des problèmes de démarrage du service toodiagnose.</span><span class="sxs-lookup"><span data-stu-id="f293d-127">It is much more reliable way, than in-process log collection, toodiagnose service startup problems and crashes.</span></span> <span data-ttu-id="f293d-128">En outre, avec de nombreux services en cours d’exécution à l’intérieur d’un cluster Service Fabric, chaque service effectuant sa propre collection de traitement du journal entraîne grand nombre de connexions sortante à partir du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="f293d-128">Also, with many services running inside a Service Fabric cluster, each service doing its own in-process log collection results in numerous outgoing connections from hello cluster.</span></span> <span data-ttu-id="f293d-129">Grand nombre de connexions sortantes est difficile à la fois pour le sous-système de réseau hello et de destination du journal hello.</span><span class="sxs-lookup"><span data-stu-id="f293d-129">Large number of outgoing connections is taxing both for hello network subsystem and for hello log destination.</span></span> <span data-ttu-id="f293d-130">Un agent tel qu’[**Azure Diagnostics** ](../cloud-services/cloud-services-dotnet-diagnostics.md) peut collecter les données de plusieurs services et envoyer toutes ces données via un nombre réduit de connexions, ce qui améliore le débit.</span><span class="sxs-lookup"><span data-stu-id="f293d-130">An agent such as [**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) can gather data from multiple services and send all data through a few connections, improving throughput.</span></span> 

<span data-ttu-id="f293d-131">Dans cet article, nous montrons comment tooset un processus d’inscription du journal à l’aide de la collection [ **bibliothèque open source de EventFlow**](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="f293d-131">In this article, we show how tooset up an in-process log collection using [**EventFlow open-source library**](https://github.com/Azure/diagnostics-eventflow).</span></span> <span data-ttu-id="f293d-132">Autres bibliothèques peuvent être utilisées pour hello même objectif, mais EventFlow offre hello d’ayant été conçu spécifiquement pour les services Service Fabric intra-processus journal toosupport et de la collection.</span><span class="sxs-lookup"><span data-stu-id="f293d-132">Other libraries might be used for hello same purpose, but EventFlow has hello benefit of having been designed specifically for in-process log collection and toosupport Service Fabric services.</span></span> <span data-ttu-id="f293d-133">Nous utilisons [ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/) en tant que destination de journal hello.</span><span class="sxs-lookup"><span data-stu-id="f293d-133">We use [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) as hello log destination.</span></span> <span data-ttu-id="f293d-134">D’autres destinations telles qu’[**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) ou [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) sont également prises en charge.</span><span class="sxs-lookup"><span data-stu-id="f293d-134">Other destinations such as [**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) or [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) are also supported.</span></span> <span data-ttu-id="f293d-135">Il s’agit simplement d’une question de l’installation de package NuGet approprié et de configuration de destination de hello dans le fichier de configuration EventFlow hello.</span><span class="sxs-lookup"><span data-stu-id="f293d-135">It is just a question of installing appropriate NuGet package and configuring hello destination in hello EventFlow configuration file.</span></span> <span data-ttu-id="f293d-136">Pour plus d’informations sur les destinations de journaux autres qu’Application Insights, consultez la [documentation relative à EventFlow](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="f293d-136">For more information on log destinations other than Application Insights, see [EventFlow documentation](https://github.com/Azure/diagnostics-eventflow).</span></span>

## <a name="adding-eventflow-library-tooa-service-fabric-service-project"></a><span data-ttu-id="f293d-137">Ajout de projet de service Service Fabric EventFlow bibliothèque tooa</span><span class="sxs-lookup"><span data-stu-id="f293d-137">Adding EventFlow library tooa Service Fabric service project</span></span>
<span data-ttu-id="f293d-138">Les fichiers binaires EventFlow sont disponibles sous la forme d’un ensemble de packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="f293d-138">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="f293d-139">tooadd projet de service Service Fabric EventFlow tooa, avec le bouton droit de projet hello Bonjour l’Explorateur de solutions et choisissez « NuGet de gérer les packages ».</span><span class="sxs-lookup"><span data-stu-id="f293d-139">tooadd EventFlow tooa Service Fabric service project, right-click hello project in hello Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="f293d-140">Commutateur toohello « Parcourir » onglet et recherchez «`Diagnostics.EventFlow`» :</span><span class="sxs-lookup"><span data-stu-id="f293d-140">Switch toohello "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Packages NuGet EventFlow dans l’interface utilisateur du gestionnaire de package NuGet Visual Studio][1]

<span data-ttu-id="f293d-142">service Hello EventFlow d’hébergement doit inclure les packages appropriés en fonction de la source de hello et de destination pour les journaux d’application hello.</span><span class="sxs-lookup"><span data-stu-id="f293d-142">hello service hosting EventFlow should include appropriate packages depending on hello source and destination for hello application logs.</span></span> <span data-ttu-id="f293d-143">Ajoutez hello suivant des packages :</span><span class="sxs-lookup"><span data-stu-id="f293d-143">Add hello following packages:</span></span> 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * <span data-ttu-id="f293d-144">(toocapture à partir de la classe EventSource du service hello, des données EventSources standard tels que *Services de Microsoft ServiceFabric* et *ServiceFabric-Microsoft-acteurs*)</span><span class="sxs-lookup"><span data-stu-id="f293d-144">(toocapture data from hello service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * <span data-ttu-id="f293d-145">(nous allons toosend hello journaux tooan Azure Application Insights ressource)</span><span class="sxs-lookup"><span data-stu-id="f293d-145">(we are going toosend hello logs tooan Azure Application Insights resource)</span></span>  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * <span data-ttu-id="f293d-146">(permet l’initialisation du pipeline de EventFlow hello à partir de la configuration du service Service Fabric et signale les problèmes à l’envoi de données de diagnostic sous forme de rapports d’intégrité de l’infrastructure de Service)</span><span class="sxs-lookup"><span data-stu-id="f293d-146">(enables initialization of hello EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

> [!NOTE]
> <span data-ttu-id="f293d-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource`le package nécessite hello service projet tootarget .NET Framework 4.6 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f293d-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource` package requires hello service project tootarget .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="f293d-148">Assurez-vous que vous définissez framework cible appropriée de hello dans Propriétés du projet avant d’installer ce package.</span><span class="sxs-lookup"><span data-stu-id="f293d-148">Make sure you set hello appropriate target framework in project properties before installing this package.</span></span> 

<span data-ttu-id="f293d-149">Une fois toutes les hello packages sont installés, étape suivante de hello est tooconfigure et activer EventFlow dans le service hello.</span><span class="sxs-lookup"><span data-stu-id="f293d-149">After all hello packages are installed, hello next step is tooconfigure and enable EventFlow in hello service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="f293d-150">Configuration et activation de la collecte de journaux</span><span class="sxs-lookup"><span data-stu-id="f293d-150">Configuring and enabling log collection</span></span>
<span data-ttu-id="f293d-151">Pipeline EventFlow, responsable de l’envoi de journaux de hello, est créé à partir d’une spécification stockée dans un fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="f293d-151">EventFlow pipeline, responsible for sending hello logs, is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="f293d-152">Le package `Microsoft.Diagnostics.EventFlow.ServiceFabric` installe un fichier de configuration EventFlow de démarrage dans le dossier `PackageRoot\Config` de la solution.</span><span class="sxs-lookup"><span data-stu-id="f293d-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder.</span></span> <span data-ttu-id="f293d-153">nom de fichier Hello est `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="f293d-153">hello file name is `eventFlowConfig.json`.</span></span> <span data-ttu-id="f293d-154">Ce fichier de configuration a besoin de données de toocapture de toobe modifié à partir de service par défaut de hello `EventSource` classe et le service de données tooApplication Insights d’envoi.</span><span class="sxs-lookup"><span data-stu-id="f293d-154">This configuration file needs toobe modified toocapture data from hello default service `EventSource` class and send data tooApplication Insights service.</span></span>

> [!NOTE]
> <span data-ttu-id="f293d-155">Nous partons du principe que vous êtes familiarisé avec **Azure Application Insights** service et que vous disposez d’une ressource Application Insights plan toouse toomonitor votre service Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f293d-155">We assume that you are familiar with **Azure Application Insights** service and that you have an Application Insights resource that you plan toouse toomonitor your Service Fabric service.</span></span> <span data-ttu-id="f293d-156">Si vous avez besoin d’informations supplémentaires, consultez [Création d’une ressource Application Insights dans Azure](../application-insights/app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="f293d-156">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

<span data-ttu-id="f293d-157">Ouvrez hello `eventFlowConfig.json` dans l’éditeur de hello et modifie son contenu comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f293d-157">Open hello `eventFlowConfig.json` file in hello editor and change its content as shown below.</span></span> <span data-ttu-id="f293d-158">Vérifiez que nom de ServiceEventSource tooreplace hello et clé d’instrumentation Application Insights selon toocomments.</span><span class="sxs-lookup"><span data-stu-id="f293d-158">Make sure tooreplace hello ServiceEventSource name and Application Insights instrumentation key according toocomments.</span></span> 

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
> <span data-ttu-id="f293d-159">nom Hello de ServiceEventSource du service valeur hello Hello propriété Name de hello `EventSourceAttribute` appliqué toohello ServiceEventSource classe.</span><span class="sxs-lookup"><span data-stu-id="f293d-159">hello name of service's ServiceEventSource is hello value of hello Name property of hello `EventSourceAttribute` applied toohello ServiceEventSource class.</span></span> <span data-ttu-id="f293d-160">Il est spécifié dans hello `ServiceEventSource.cs` fichier, qui fait partie du code de service hello.</span><span class="sxs-lookup"><span data-stu-id="f293d-160">It is all specified in hello `ServiceEventSource.cs` file, which is part of hello service code.</span></span> <span data-ttu-id="f293d-161">Par exemple, Bonjour suivant nom hello d’extrait de code Hello ServiceEventSource est *MyCompany-Application1-Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="f293d-161">For example, in hello following code snippet hello name of hello ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

<span data-ttu-id="f293d-162">Notez que le fichier `eventFlowConfig.json` fait partie du package de configuration du service.</span><span class="sxs-lookup"><span data-stu-id="f293d-162">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="f293d-163">Fichier toothis des modifications peut être inclus dans intégral ou configuration-uniquement les mises à niveau du service de hello, objet tooService Fabric mise à niveau les vérifications d’intégrité et restauration automatique cas d’échec de mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="f293d-163">Changes toothis file can be included in full- or configuration-only upgrades of hello service, subject tooService Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="f293d-164">Pour plus d’informations, consultez [Mise à niveau des applications Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="f293d-164">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="f293d-165">étape finale de Hello est le pipeline de EventFlow tooinstantiate dans le code de démarrage de votre service, situé dans `Program.cs` fichier.</span><span class="sxs-lookup"><span data-stu-id="f293d-165">hello final step is tooinstantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file.</span></span> <span data-ttu-id="f293d-166">Bonjour ajouts de liées EventFlow exemple suivants sont marqués avec des commentaires commençant par `****`:</span><span class="sxs-lookup"><span data-stu-id="f293d-166">In hello following example  EventFlow-related additions are marked with comments starting with `****`:</span></span>

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

<span data-ttu-id="f293d-167">nom de Hello passé comme paramètre hello Hello `CreatePipeline` méthode Hello `ServiceFabricDiagnosticsPipelineFactory` hello désigne hello *entité de contrôle d’intégrité* représentant le pipeline de collection de journaux de EventFlow hello.</span><span class="sxs-lookup"><span data-stu-id="f293d-167">hello name passed as hello parameter of hello `CreatePipeline` method of hello `ServiceFabricDiagnosticsPipelineFactory` is hello name of hello *health entity* representing hello EventFlow log collection pipeline.</span></span> <span data-ttu-id="f293d-168">Ce nom est utilisé en cas de EventFlow et d’erreur et la signale via hello sous-système de contrôle d’intégrité de l’infrastructure de Service.</span><span class="sxs-lookup"><span data-stu-id="f293d-168">This name is used if EventFlow encounters and error and reports it through hello Service Fabric health subsystem.</span></span>

## <a name="verification"></a><span data-ttu-id="f293d-169">Vérification</span><span class="sxs-lookup"><span data-stu-id="f293d-169">Verification</span></span>
<span data-ttu-id="f293d-170">Démarrer votre service et observez hello débogage fenêtre Sortie de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f293d-170">Start your service and observe hello Debug output window in Visual Studio.</span></span> <span data-ttu-id="f293d-171">Après le démarrage du service de hello, vous devez commencer à voir les preuves que votre service envoie des enregistrements de « Données de télémétrie Application Insights ».</span><span class="sxs-lookup"><span data-stu-id="f293d-171">After hello service is started, you should start seeing evidence that your service is sending "Application Insights Telemetry" records.</span></span> <span data-ttu-id="f293d-172">Ouvrez un navigateur web et accédez de ressource d’Application Insights tooyour accédez.</span><span class="sxs-lookup"><span data-stu-id="f293d-172">Open a web browser and navigate go tooyour Application Insights resource.</span></span> <span data-ttu-id="f293d-173">Ouvrez l’onglet « Recherche » (en haut de hello du Panneau de « Présentation » hello par défaut).</span><span class="sxs-lookup"><span data-stu-id="f293d-173">Open "Search" tab (at hello top of hello default "Overview" blade).</span></span> <span data-ttu-id="f293d-174">Après un court délai vous devez commencer à voir les traces dans le portail d’Application Insights hello :</span><span class="sxs-lookup"><span data-stu-id="f293d-174">After a short delay you should start seeing your traces in hello Application Insights portal:</span></span>

![Portail Application Insights montrant les journaux issus d’une application Service Fabric][2]

## <a name="next-steps"></a><span data-ttu-id="f293d-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f293d-176">Next steps</span></span>
* [<span data-ttu-id="f293d-177">En savoir plus sur le diagnostic et la surveillance d’un service Fabric Service</span><span class="sxs-lookup"><span data-stu-id="f293d-177">Learn more about diagnosing and monitoring a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [<span data-ttu-id="f293d-178">Documentation relative à EventFlow</span><span class="sxs-lookup"><span data-stu-id="f293d-178">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
